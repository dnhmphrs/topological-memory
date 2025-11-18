<script>
	import { onMount } from 'svelte';
	import * as THREE from 'three';

	let container;
	let camera, scene, renderer;
	let width, height;

	const GRID_SIZE = 100;
	const CELL_SIZE = 1;
	const WALL_HEIGHT = 2;
	const WALL_DENSITY = 0.25; // 15% chance of wall

	function init() {
		width = window.innerWidth - 600; // Account for sidebars
		height = window.innerHeight * 0.6;

		// Camera
		const viewSize = GRID_SIZE * 1.1; // View size to cover the grid with some margin
		const aspect = width / height;
		camera = new THREE.OrthographicCamera(
			-viewSize * aspect / 2,
			viewSize * aspect / 2,
			viewSize / 2,
			-viewSize / 2,
			0.1,
			1000
		);
		camera.position.set(GRID_SIZE / 2, GRID_SIZE / 3, GRID_SIZE / 2);
		camera.lookAt(GRID_SIZE / 2, 0, GRID_SIZE / 2);

		// Scene
		scene = new THREE.Scene();
		scene.fog = new THREE.Fog(0xf8f9fa, GRID_SIZE * 0.5, GRID_SIZE * 1.2);

		// Lighting
		const ambientLight = new THREE.AmbientLight(0xffffff, 0.6);
		scene.add(ambientLight);

		const directionalLight = new THREE.DirectionalLight(0xffffff, 0.8);
		directionalLight.position.set(50, 100, 50);
		directionalLight.castShadow = true;
		scene.add(directionalLight);

		// Grid floor
		createGridFloor();

		// Random walls
		createRandomWalls();

		// Renderer
		renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
        renderer.setClearColor( 0x232323, 1 ); 
		renderer.setPixelRatio(window.devicePixelRatio);
		renderer.setSize(width, height);
		renderer.shadowMap.enabled = true;
		renderer.shadowMap.type = THREE.PCFSoftShadowMap;

		container.appendChild(renderer.domElement);

		// Handle resize
		window.addEventListener('resize', onWindowResize);

		// Animation loop
		animate();
	}

	function createGridFloor() {
		// Create a grid helper
		const gridHelper = new THREE.GridHelper(
			GRID_SIZE * CELL_SIZE,
			GRID_SIZE,
			0xcccccc,
			0xe0e0e0
		);
		gridHelper.position.set(GRID_SIZE / 2, 0, GRID_SIZE / 2);
		scene.add(gridHelper);

		// Create floor plane
		const floorGeometry = new THREE.PlaneGeometry(
			GRID_SIZE * CELL_SIZE,
			GRID_SIZE * CELL_SIZE
		);
		const floorMaterial = new THREE.MeshStandardMaterial({
			color: 0xffffff,
			roughness: 0.8,
			metalness: 0.2
		});
		const floor = new THREE.Mesh(floorGeometry, floorMaterial);
		floor.rotation.x = -Math.PI / 2;
		floor.position.set(GRID_SIZE / 2, 0, GRID_SIZE / 2);
		floor.receiveShadow = true;
		scene.add(floor);
	}

	function createRandomWalls() {
		const wallGeometry = new THREE.BoxGeometry(CELL_SIZE, WALL_HEIGHT, CELL_SIZE);
		const wallMaterial = new THREE.MeshStandardMaterial({
			color: 0x232323,
			roughness: 0.7,
			metalness: 0.3
		});

		// Create random walls
		for (let x = 0; x < GRID_SIZE; x++) {
			for (let z = 0; z < GRID_SIZE; z++) {
				// Random chance to place a wall
				if (Math.random() < WALL_DENSITY) {
					const wall = new THREE.Mesh(wallGeometry, wallMaterial);
					wall.position.set(
						x * CELL_SIZE + CELL_SIZE / 2,
						WALL_HEIGHT / 2,
						z * CELL_SIZE + CELL_SIZE / 2
					);
					wall.castShadow = false;
					wall.receiveShadow = false;
					scene.add(wall);
				}
			}
		}

		// Add boundary walls
		// createBoundaryWalls();
	}

	function createBoundaryWalls() {
		const boundaryMaterial = new THREE.MeshStandardMaterial({
			color: 0x000000,
			roughness: 0.8,
			metalness: 0.2
		});

		// North and South walls
		for (let x = 0; x < GRID_SIZE; x++) {
			// North wall
			const northWall = new THREE.Mesh(
				new THREE.BoxGeometry(CELL_SIZE, WALL_HEIGHT, CELL_SIZE),
				boundaryMaterial
			);
			northWall.position.set(x * CELL_SIZE + CELL_SIZE / 2, WALL_HEIGHT / 2, 0);
			northWall.castShadow = false;
			scene.add(northWall);

			// South wall
			const southWall = new THREE.Mesh(
				new THREE.BoxGeometry(CELL_SIZE, WALL_HEIGHT, CELL_SIZE),
				boundaryMaterial
			);
			southWall.position.set(
				x * CELL_SIZE + CELL_SIZE / 2,
				WALL_HEIGHT / 2,
				GRID_SIZE * CELL_SIZE
			);
			southWall.castShadow = true;
			scene.add(southWall);
		}

		// East and West walls
		for (let z = 0; z < GRID_SIZE; z++) {
			// West wall
			const westWall = new THREE.Mesh(
				new THREE.BoxGeometry(CELL_SIZE, WALL_HEIGHT, CELL_SIZE),
				boundaryMaterial
			);
			westWall.position.set(0, WALL_HEIGHT / 2, z * CELL_SIZE + CELL_SIZE / 2);
			westWall.castShadow = true;
			scene.add(westWall);

			// East wall
			const eastWall = new THREE.Mesh(
				new THREE.BoxGeometry(CELL_SIZE, WALL_HEIGHT, CELL_SIZE),
				boundaryMaterial
			);
			eastWall.position.set(
				GRID_SIZE * CELL_SIZE,
				WALL_HEIGHT / 2,
				z * CELL_SIZE + CELL_SIZE / 2
			);
			eastWall.castShadow = true;
			scene.add(eastWall);
		}
	}

	function onWindowResize() {
		width = window.innerWidth - 500;
		height = window.innerHeight * 0.6;

		const viewSize = GRID_SIZE * 1.2;
		const aspect = width / height;
		camera.left = -viewSize * aspect / 2;
		camera.right = viewSize * aspect / 2;
		camera.top = viewSize / 2;
		camera.bottom = -viewSize / 2;
		camera.updateProjectionMatrix();

		renderer.setSize(width, height);
	}

	function animate() {
		requestAnimationFrame(animate);

		// Slowly rotate camera around the center
		const time = Date.now() * 0.0001;
		// const radius = GRID_SIZE * 0.8;
		// camera.position.x = Math.sin(time) * radius + GRID_SIZE / 2;
		// camera.position.z = Math.cos(time) * radius + GRID_SIZE / 2;
		// camera.lookAt(GRID_SIZE / 2, 0, GRID_SIZE / 2);

		renderer.render(scene, camera);
	}

	function cleanup() {
		window.removeEventListener('resize', onWindowResize);
		if (renderer) {
			renderer.dispose();
		}
		if (scene) {
			scene.traverse((object) => {
				if (object.geometry) object.geometry.dispose();
				if (object.material) {
					if (Array.isArray(object.material)) {
						object.material.forEach((material) => material.dispose());
					} else {
						object.material.dispose();
					}
				}
			});
		}
	}

	onMount(() => {
		init();
		return cleanup;
	});
</script>

<div bind:this={container} class="room-container" />

<style>
	/* .room-container {
		width: 100%;
		height: 60vh;
		display: flex;
		justify-content: center;
		align-items: center;
		background: #f8f9fa;
		border: 1px solid #e0e0e0;
		border-radius: 4px;
		overflow: hidden;
	} */
</style>
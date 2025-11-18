<script>
	import { onMount } from 'svelte';
	
	let Room;
	
	onMount(async () => {
		// Dynamically import the room component only on client side
		const module = await import('$lib/graphics/room.svelte');
		Room = module.default;
	});
</script>

<h1>Space</h1>

<hr> 

<h2>A Room</h2>

{#if Room}
	<svelte:component this={Room} />
{:else}
	<div class="loading">Loading room...</div>
{/if}

<style>
	h1 {
		margin-bottom: 1.5rem;
	}

	h2 {
		margin-top: 2rem;
		margin-bottom: 1rem;
	}

	h3 {
		margin-top: 1.5rem;
		margin-bottom: 0.75rem;
	}

	p {
		margin-bottom: 1rem;
		line-height: 1.6;
	}

	ul {
		margin-bottom: 1rem;
		line-height: 1.6;
	}

	li {
		margin-bottom: 0.5rem;
	}
	
	.loading {
		width: 100%;
		height: 60vh;
		display: flex;
		justify-content: center;
		align-items: center;
		background: #f8f9fa;
		border: 1px solid #e0e0e0;
		border-radius: 4px;
		color: #666;
		font-style: italic;
	}
</style>
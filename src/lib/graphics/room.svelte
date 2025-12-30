<script>
  // Simple canvas-based room visualization instead of Three.js
  import { onMount } from 'svelte';
  
  let canvas;
  
  onMount(() => {
    const ctx = canvas.getContext('2d');
    // Draw a simple 2D grid
    ctx.strokeStyle = '#ccc';
    ctx.lineWidth = 1;
    
    // Draw grid
    for (let i = 0; i <= 10; i++) {
      ctx.beginPath();
      ctx.moveTo(i * 30, 0);
      ctx.lineTo(i * 30, 300);
      ctx.stroke();
      
      ctx.beginPath();
      ctx.moveTo(0, i * 30);
      ctx.lineTo(300, i * 30);
      ctx.stroke();
    }
    
    // Draw some walls
    ctx.fillStyle = '#333';
    ctx.fillRect(60, 60, 30, 30);
    ctx.fillRect(150, 120, 30, 30);
    ctx.fillRect(210, 90, 30, 30);
  });
</script>

<figure>
  <canvas bind:this={canvas} width="300" height="300"></canvas>
  <figcaption>Figure 1: A discretized spatial environment</figcaption>
</figure>

<style>
  figure {
    text-align: center;
    margin: 2em 0;
  }
  
  canvas {
    border: 1px solid #ddd;
    max-width: 100%;
  }
  
  figcaption {
    margin-top: 0.5em;
    font-size: 0.9em;
    color: #666;
  }
</style>
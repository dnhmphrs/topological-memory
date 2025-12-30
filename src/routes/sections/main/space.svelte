<script>
  import { onMount } from 'svelte';
  
  let Room;
  
  onMount(async () => {
    const module = await import('$lib/graphics/room.svelte');
    Room = module.default;
  });
</script>

<section id="space">
  <h2>2. Spatial Representation</h2>

  <h3>2.1 Discretized Environments</h3>

  <p>
    <strong>Definition 2.1.</strong> A <em>discretized environment</em> is a finite
    CW-complex <span class="math">X</span> embedded in <span class="math">ℝ<sup>2</sup></span>
    or <span class="math">ℝ<sup>3</sup></span>, where 0-cells represent locations and
    1-cells represent traversable paths.
  </p>

  <p>
    <strong>Example 2.2.</strong> Consider the following discretized room:
  </p>

  {#if Room}
    <figure>
      <svelte:component this={Room} />
      <figcaption>
        Figure 1. A 100×100 grid with randomly placed obstacles. Each cell represents
        a potential place field center.
      </figcaption>
    </figure>
  {:else}
    <div class="placeholder">Loading visualization...</div>
  {/if}

  <h3>2.2 Observable Functions</h3>

  <p>
    <strong>Definition 2.3.</strong> For each open set <span class="math">U ⊆ X</span>,
    the ring <span class="math">𝒪<sub>X</sub>(U)</span> consists of continuous functions
    <span class="math">f: U → ℝ</span> representing observable quantities.
  </p>

  <p>
    <strong>Proposition 2.4.</strong> In the discretized setting, <span class="math">𝒪<sub>X</sub>(U)</span>
    is isomorphic to <span class="math">ℝ<sup>|U|</sup></span> with pointwise operations,
    where <span class="math">|U|</span> denotes the number of cells in <span class="math">U</span>.
  </p>
</section>

<style>
  figure {
    margin: 2em 0;
    text-align: center;
  }
  
  figcaption {
    margin-top: 1em;
    font-size: 0.9em;
    font-style: italic;
  }
  
  .placeholder {
    height: 60vh;
    display: flex;
    align-items: center;
    justify-content: center;
    background: #f5f5f5;
    border: 1px solid #ddd;
    color: #666;
    font-style: italic;
  }
  
  /* Ensure the Three.js container fits properly */
  :global(.room-container) {
    width: 100%;
    height: 60vh;
    border: 1px solid #ddd;
  }
</style>
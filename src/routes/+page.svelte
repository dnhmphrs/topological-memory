<script>
  import Intro from './sections/main/intro.svelte';
  import FunctorialMemory from './sections/main/functorial-memory.svelte';
  import NeuralImplementation from './sections/main/neural-implementation.svelte';
  import Space from './sections/main/space.svelte';
</script>

<article>
  <h1>Functorial Memory</h1>
  <p class="abstract">
    <strong>Abstract.</strong> We demonstrate that hippocampal place cells implement
    a functor from topological spaces to their structure sheaves. This provides a
    rigorous mathematical framework for cognitive map theory.
  </p>

  <nav class="toc">
    <ol>
      <li><a href="#introduction">Introduction</a></li>
      <li><a href="#functorial-memory">Functorial Framework</a></li>
      <li><a href="#neural-implementation">Neural Implementation</a></li>
      <li><a href="#references">References</a></li>
    </ol>
  </nav>

  <Intro />
  <Space />
  <FunctorialMemory />
  <NeuralImplementation />

  <section id="references">
    <h2>References</h2>
    <ol class="references">
      <li>O'Keefe, J. & Dostrovsky, J. (1971). The hippocampus as a spatial map. <em>Brain Research</em>, 34, 171-175.</li>
      <li>Hartshorne, R. (1977). <em>Algebraic Geometry</em>. Springer-Verlag.</li>
      <li>Mac Lane, S. & Moerdijk, I. (1992). <em>Sheaves in Geometry and Logic</em>. Springer-Verlag.</li>
    </ol>
  </section>
</article>

<style>
  article {
    max-width: 650px;
    margin: 0 auto;
    padding: 2em;
    font-family: 'Computer Modern', Georgia, serif;
    line-height: 1.4;
  }

  h1 {
    text-align: center;
    font-size: 1.8em;
    margin-bottom: 0.5em;
  }

  .abstract {
    font-size: 0.95em;
    margin: 2em 0;
  }

  .toc {
    margin-bottom: 2em;
  }

  .toc ol {
    list-style: none;
    padding: 0;
  }

  :global(.math) {
    font-style: italic;
  }

  :global(section) {
    margin-bottom: 2em;
  }

  :global(h2) {
    font-size: 1.3em;
    margin-top: 2em;
    margin-bottom: 1em;
  }

  :global(h3) {
    font-size: 1.1em;
    margin-top: 1.5em;
    margin-bottom: 0.8em;
  }

  .references {
    font-size: 0.9em;
  }
</style>
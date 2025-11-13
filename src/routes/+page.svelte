<script>
  import { screenType } from '$lib/store/store';
  
  // Import all sections
  import Intro from './sections/intro.svelte';
  import Space from './sections/space.svelte';
  import Learning from './sections/learning.svelte';
  import Functors from './sections/functors.svelte';
  import Navigation from './sections/navigation.svelte';
  import Appendix from './sections/appendix.svelte';
  
  // Nav structure (single source of truth)
  const navStructure = [
      {
          id: 'intro',
          title: 'Introduction',
          component: Intro,
          subsections: [
              { id: 'cognitive-maps', title: 'Cognitive Maps' },
              { id: 'functors', title: 'Functors' }
          ]
      },
      {
          id: 'space',
          title: 'Space',
          component: Space,
          subsections: [
              { id: 'spaces', title: 'Spaces: X' },
              { id: 'places', title: 'Places: π₀', symbol: true },
              { id: 'circuits', title: 'Circuits: π₁', symbol: true },
              // { id: 'flows', title: 'Dynamics: ∂/∂t', symbol: true },
              // { id: 'periods', title: 'Periods: ω' }
          ]
      },
      {
          id: 'learning',
          title: 'Learning',
          component: Learning,
          subsections: [
              { id: 'neural-net', title: 'Neural Net: Γ' },
              { id: 'states', title: 'States: γ' },
              { id: 'sequences', title: 'Sequences: ϕ : γ ↦ γ\'' },
              // { id: 'sheaves', title: 'Schema: (Π,𝒪)' }
          ]
      },
    //   {
    //       id: 'representation',
    //       title: 'Representation',
    //       component: Functors,
    //       subsections: [
    //           { id: 'local', title: 'Local: [ γ, Γ ]' },
    //           { id: 'global', title: 'Global: [ γ*, J(Γ) ]' },
    //           { id: 'phase', title: 'Phase: [ (γ,γ*), T*J(Γ) ]' }
    //       ]
    //   },
    //   {
    //       id: 'navigation',
    //       title: 'Navigation',
    //       component: Navigation,
    //       subsections: [
    //           { id: 'goals', title: 'Goals: η' },
    //           { id: 'actions', title: 'Actions : ϕ: (γ,γ*) ↦ (γ\',γ*\')' },
    //           { id: 'composition', title: 'Composition : ⊕ , ⊗' },
    //           { id: 'flexible-behaviour', title: 'Flexible Behaviour' }
    //       ]
    //   },
    //   {
    //       id: 'appendix',
    //       title: 'Formal Appendix',
    //       component: Appendix,
    //       subsections: [
    //           { id: 'sheaves-formal', title: 'Sheaves: 𝒪ₓ' },
    //           { id: 'schemes-formal', title: 'Schemes: (X, 𝒪ₓ)' }
    //       ]
    //   }
  ];
</script>

<div class="container">
  <!-- Left Navigation -->
  <nav class="sidebar">
      <div class="nav-content">
          <h2>Functorial Memory</h2>
          
          {#each navStructure as section}
              <div class="section">
                  <a href="#{section.id}">{section.title}</a>
                  {#if section.subsections}
                      <div class="subsections">
                          {#each section.subsections as subsection}
                              <a href="#{subsection.id}">
                                  {#if subsection.symbol}
                                      {@html subsection.title}
                                  {:else}
                                      {subsection.title}
                                  {/if}
                              </a>
                          {/each}
                      </div>
                  {/if}
              </div>
          {/each}
      </div>
  </nav>
  
  <!-- Main Content -->
  <main class="content">
      {#each navStructure as section}
          <section id={section.id}>
              <svelte:component this={section.component} />
          </section>
      {/each}
  </main>
</div>
<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    .container {
        display: flex;
        min-height: 100vh;
    }
    
    /* Sidebar Navigation */
    .sidebar {
        position: fixed;
        top: 0;
        left: 0;
        width: 250px;
        height: 100vh;
        background: #f8f9fa;
        border-right: 1px solid #e0e0e0;
        /* padding-left: 0.5rem; */
        overflow-y: auto;
    }
    
    .nav-content {
        padding: 2rem 1rem;
    }
    
    .nav-content h2 {
        margin-bottom: 1.5rem;
        font-size: 1.2rem;
        color: #333;
    }
    
    .section {
        margin-bottom: 0.5rem;
    }
    
    .section > a {
        display: block;
        padding: 0.5rem 0.75rem;
        text-decoration: none;
        color: #555;
        font-weight: 500;
        border-left: 3px solid transparent;
        transition: all 0.2s;
    }
    
    .section > a:hover {
        background: #e8eaed;
        border-left-color: #1a73e8;
        color: #1a73e8;
    }
    
    .subsections {
        padding-left: 1rem;
    }
    
    .subsections a {
        display: block;
        padding: 0.4rem 0.75rem;
        text-decoration: none;
        color: #666;
        font-size: 0.9rem;
        transition: color 0.2s;
    }
    
    .subsections a:hover {
        color: #1a73e8;
    }
    
    /* Main Content */
    .content {
        margin-left: 250px;
        flex: 1;
        padding: 2rem 3rem;
        max-width: 900px;
    }
    
    .content section {
        margin-bottom: 2rem;
        padding-top: 0rem;
    }
    
    /* Responsive */
    /* @media (max-width: 768px) {
        .sidebar {
            position: static;
            width: 100%;
            height: auto;
            border-right: none;
            border-bottom: 1px solid #e0e0e0;
        }
        
        .content {
            margin-left: 0;
            padding: 2rem 1.5rem;
        }
    } */
</style>
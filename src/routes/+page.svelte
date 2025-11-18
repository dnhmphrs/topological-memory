<script>
    import { screenType } from '$lib/store/store';
    import { writable } from 'svelte/store';
    
    // Import main sections
    import Intro from './sections/main/intro.svelte';
    import Space from './sections/main/space.svelte';
    import Learning from './sections/main/learning.svelte';

    // Import appendix sections
    import Spaces from './sections/appendix/spaces.svelte';
    
    // Track which content to show in center panel
    const activeContent = writable({ type: 'main', id: 'intro' });
    
    // Main paper structure
    const mainStructure = [
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
                { id: 'topology', title: 'Topology' },
                { id: 'hodge-theory', title: 'Hodge Theory' },
                { id: 'dynamics', title: 'Dynamics' },
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
            ]
        },
    ];
    
    // Appendix structure
    const appendixStructure = [
        {
            id: 'spaces',
            title: 'Spaces',
            component: Space,
            subsections: [
                { id: 'spaces', title: 'Spaces: X' },
                { id: 'places', title: 'Places: π₀', symbol: true },
                { id: 'circuits', title: 'Circuits: π₁', symbol: true },
            ]
        },
    ];
    
    function setContent(type, id) {
        activeContent.set({ type, id });
    }
    
    $: currentComponent = (() => {
        const structure = $activeContent.type === 'main' ? mainStructure : appendixStructure;
        const section = structure.find(s => s.id === $activeContent.id);
        return section ? section.component : null;
    })();
  </script>
  
  <div class="container">
    <!-- Left Navigation (Main Paper) -->
    <nav class="sidebar left">
        <div class="nav-content">
            <h2>Topological Memory</h2>
            
            {#each mainStructure as section}
                <div class="section">
                    <a 
                        href="#"
                        on:click|preventDefault={() => setContent('main', section.id)}
                        class:active={$activeContent.type === 'main' && $activeContent.id === section.id}
                    >
                        {section.title}
                    </a>
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
    
    <!-- Main Content (Center) -->
    <main class="content">
        {#if currentComponent}
            <svelte:component this={currentComponent} />
        {/if}
    </main>
    
    <!-- Right Appendix Panel -->
    <aside class="sidebar right">
        <div class="nav-content">
            <h2>Appendix</h2>
            
            {#each appendixStructure as section}
                <div class="section">
                    <a 
                        href="#"
                        on:click|preventDefault={() => setContent('appendix', section.id)}
                        class:active={$activeContent.type === 'appendix' && $activeContent.id === section.id}
                    >
                        {section.title}
                    </a>
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
    </aside>
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
      
      /* Shared Sidebar Styles */
      .sidebar {
          position: fixed;
          top: 0;
          width: 250px;
          height: 100vh;
          background: #f8f9fa;
          border: 1px solid #e0e0e0;
          overflow-y: auto;
      }
      
      .sidebar.left {
          left: 0;
          border-right: 1px solid #e0e0e0;
      }
      
      .sidebar.right {
          right: 0;
          border-left: 1px solid #e0e0e0;
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
      
      .section > a:hover,
      .section > a.active {
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
          margin-right: 250px;
          flex: 1;
          padding: 2rem 3rem;
          /* max-width: 900px; */
      }
      
      /* Responsive */
      @media (max-width: 1024px) {
          .sidebar.right {
              display: none;
          }
          
          .content {
              margin-right: 0;
          }
      }
      
      @media (max-width: 768px) {
          .sidebar.left {
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
      }
  </style>
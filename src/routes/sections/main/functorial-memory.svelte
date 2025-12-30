<section id="functorial-memory">
  <h2>2. Functorial Framework</h2>

  <h3>2.1 Structure Sheaves</h3>

  <p>
    <strong>Definition 2.1.</strong> A <em>structure sheaf</em> on a topological space
    <span class="math">X</span> is a sheaf of rings <span class="math">𝒪<sub>X</sub></span>
    such that for each open <span class="math">U ⊆ X</span>, the ring 
    <span class="math">𝒪<sub>X</sub>(U)</span> represents continuous functions on
    <span class="math">U</span>.
  </p>

  <p>
    <strong>Definition 2.2.</strong> The <em>stalk</em> at <span class="math">p ∈ X</span> is
  </p>
  <div class="math" style="text-align: center; margin: 1em 0;">
    𝒪<sub>X,p</sub> = lim<sub>→</sub> 𝒪<sub>X</sub>(U)
  </div>
  <p>
    where the limit is taken over all open neighborhoods of <span class="math">p</span>.
  </p>

  <h3>2.2 The Learning Functor</h3>

  <p>
    <strong>Proposition 2.3.</strong> Spatial learning induces a functor
  </p>
  <div class="math" style="text-align: center; margin: 1em 0;">
    F: <strong>Top</strong> → <strong>Sh</strong>(Ring)
  </div>
  <p>
    from the category of topological spaces to the category of sheaves of rings.
  </p>

  <p>
    <strong>Proof sketch.</strong> An animal exploring <span class="math">X</span>
    samples observables at points. These observables form a ring structure under
    pointwise operations. Consistency constraints from overlapping observations
    enforce the sheaf conditions. □
  </p>
</section>
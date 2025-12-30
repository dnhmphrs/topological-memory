<section id="neural-implementation">
  <h2>3. Neural Implementation</h2>

  <h3>3.1 Place Cells as Stalks</h3>

  <p>
    <strong>Lemma 3.1.</strong> Each place cell <span class="math">i</span> with
    receptive field <span class="math">U<sub>i</sub> ⊆ X</span> encodes elements
    of the stalk <span class="math">𝒪<sub>X,p<sub>i</sub></sub></span> where
    <span class="math">p<sub>i</sub></span> is the field center.
  </p>

  <p>
    <strong>Proof.</strong> The firing rate <span class="math">r<sub>i</sub>(x)</span>
    depends only on observables in a neighborhood of <span class="math">p<sub>i</sub></span>.
    Two observables yielding the same firing pattern represent the same germ. □
  </p>

  <h3>3.2 Sheaf Conditions</h3>

  <p>
    <strong>Theorem 3.2.</strong> Recurrent hippocampal connectivity implements the
    sheaf gluing axiom.
  </p>

  <p>
    <strong>Proof.</strong> Let <span class="math">{'{'} U<sub>i</sub> {'}'}</span> be an open
    cover with place fields. For sections <span class="math">s<sub>i</sub> ∈ 𝒪(U<sub>i</sub>)</span>
    agreeing on overlaps, recurrent connections enforce:
  </p>
  <ol>
    <li>Consistency: <span class="math">s<sub>i</sub>|<sub>U<sub>i</sub>∩U<sub>j</sub></sub> = s<sub>j</sub>|<sub>U<sub>i</sub>∩U<sub>j</sub></sub></span></li>
    <li>Uniqueness: The global section <span class="math">s ∈ 𝒪(∪U<sub>i</sub>)</span> is determined by energy minimization</li>
  </ol>

  <p>
    <strong>Corollary 3.3.</strong> Hippocampal lesions disrupt spatial coherence by
    preventing the gluing of local observations into global representations.
  </p>
</section>
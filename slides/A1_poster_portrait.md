---
marp: true
theme: a1portrait
size: a1portrait
paginate: false
style: |
  section {
    font-family: "Segoe UI", "Tahoma", sans-serif;
    padding: 10mm;
    background: #f0f0ee;
    color: #111;
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    height: 100%;
    gap: 0;
  }

  /* ── Title bar ─────────────────────────── */
  .titlebar {
    background: #8b0000;
    color: #fff;
    border-radius: 8px;
    padding: 12px 18px;
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    gap: 16px;
    margin-bottom: 10px;
    flex-shrink: 0;
  }
  .titlebar h1 {
    color: #fff;
    font-size: 52px;
    margin: 0 0 4px 0;
    line-height: 1.1;
  }
  .titlebar p { font-size: 20px; margin: 2px 0; }
  .titlebar .meta {
    text-align: right;
    font-size: 18px;
    line-height: 1.4;
    white-space: nowrap;
    color: #fce8e8;
  }

  /* ── Rows ───────────────────────────────── */
  .row {
    display: flex;
    gap: 10px;
    min-height: 0;
  }
  .row-top    { flex: 1; margin-bottom: 10px; }
  .row-ui     { flex: 3; margin-bottom: 10px; }
  .row-bottom { flex: 1; margin-bottom: 10px; }

  /* ── Generic card ───────────────────────── */
  .card {
    background: #ffffff;
    border: 1px solid #d8d8d8;
    border-top: 7px solid #8b0000;
    border-radius: 8px;
    padding: 10px 14px;
    flex: 1;
    min-height: 0;
    overflow: hidden;
  }

  /* ── UI card (full width inside its row) ── */
  .ui-card {
    background: #ffffff;
    border: 1px solid #d8d8d8;
    border-top: 7px solid #8b0000;
    border-radius: 8px;
    padding: 10px 14px;
    flex: 1;
    min-height: 0;
    overflow: hidden;
    display: flex;
    flex-direction: column;
  }
  .ui-body {
    display: flex;
    gap: 10px;
    flex: 1;
    min-height: 0;
    margin-top: 8px;
    align-items: stretch;
  }
  .ui-main {
    flex: 0 0 52%;
    display: flex;
    flex-direction: column;
    gap: 6px;
  }
  .ui-main img {
    width: 100%;
    border-radius: 5px;
    border: 1px solid #ccc;
  }
  .ui-plots {
    flex: 1;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    gap: 8px;
  }
  .ui-plots figure {
    margin: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .ui-plots img {
    width: 100%;
    border-radius: 4px;
    border: 1px solid #ccc;
  }

  /* ── Typography ─────────────────────────── */
  h2 {
    font-size: 32px;
    color: #8b0000;
    border-bottom: 2px solid #8b0000;
    padding-bottom: 4px;
    margin: 0 0 6px 0;
  }
  h3 {
    font-size: 23px;
    color: #333;
    margin: 6px 0 4px 0;
  }
  p, li { font-size: 20px; line-height: 1.35; }
  ul { margin: 4px 0 8px 18px; padding: 0; }
  figcaption, .caption {
    font-size: 15px;
    color: #555;
    text-align: center;
    margin-top: 3px;
  }
  img { max-width: 100%; display: block; }

  /* ── Footer ─────────────────────────────── */
  .footer {
    flex-shrink: 0;
    font-size: 17px;
    display: flex;
    justify-content: space-between;
    gap: 10px;
    color: #555;
    border-top: 1px solid #bbb;
    padding-top: 6px;
  }
---

<!-- Title bar -->
<div class="titlebar">
  <div>
    <h1>EEG Analysis Platform for Predicting Behavior from Brain Activity</h1>
    <p><strong>Nantawat Suksirisunt &nbsp;·&nbsp; Naytitorn Chaovirachot</strong></p>
    <p>Kasetsart University &nbsp;·&nbsp; Department of Computer Engineering &nbsp;·&nbsp; In collaboration with BRAIN-Interfaces Lab, VISTEC</p>
  </div>
  <div class="meta">
    <strong>KU Advisor</strong><br/>
    Asst. Prof. Dr. Thanawin Rakthanmanon<br/>
    <em style="font-size:15px">Kasetsart University</em><br/>
    <br/>
    <strong>VISTEC Advisor</strong><br/>
    Assoc. Prof. Dr. Theerawit Wilaiprasitporn<br/>
    <em style="font-size:15px">BRAIN-Interfaces Lab, VISTEC</em><br/>
    <br/>
    <strong>Academic Year:</strong> 2567
  </div>
</div>

<!-- Row 1 — Project Overview | Objectives -->
<div class="row row-top">

  <div class="card">
    <h2>Project Overview</h2>
    <p><strong>What is EEG?</strong> EEG measures electrical signals from the brain using sensors on the scalp. Brain signals can reveal what a person is thinking or about to do, even before they act.</p>
    <p><strong>The Challenge:</strong> Scientists want to use brain signals to predict behavior (e.g., will this decision be correct? how fast will someone react?). But today, they must glue together different tools that don't communicate well, leading to errors and wasted time.</p>
    <p><strong>Our Solution:</strong> We built a single platform that handles the entire workflow — from raw brain recordings to predictions. Everything is connected, documented, and repeatable, so scientists can focus on discoveries instead of fixing broken pipelines.</p>
  </div>

  <div class="card">
    <h2>Objectives</h2>
    <ul>
      <li>Build a systematic, reproducible EEG analysis platform usable by domain researchers without deep engineering expertise.</li>
      <li>Evaluate whether <strong>brain signals before a task</strong> can predict:<br/>
        &nbsp;&nbsp;① Whether the trial was correct<br/>
        &nbsp;&nbsp;② How fast the person reacted
      </li>
      <li>Provide transparent experiment tracking so results can be replicated and extended.</li>
    </ul>
  </div>

</div>

<!-- Row 2 — Platform & UI (tall, software emphasis) -->
<div class="row row-ui">

  <div class="ui-card">
    <h2>Platform &amp; Visualization</h2>
    <p>The platform exposes a modal workflow — users select a <em>mode</em> (e.g. Preprocess, Epoch, Analysis) then configure and execute actions via a clean web interface. All outputs are cached and parameterised for full reproducibility.</p>

    <div class="ui-body">

      <!-- Left: main UI screenshots -->
      <div class="ui-main">
        <img src="../assets/figures/ui/EEGUI.png" alt="Main EEG platform interface" />
        <img src="../assets/figures/ui/EEGUI_cohort.png" alt="Cohort filter view" />
      </div>

      <!-- Right: 2×2 plot grid -->
      <div class="ui-plots">
        <figure>
          <img src="../assets/figures/plot/evoked_topo.png" alt="Evoked topography" />
          <figcaption>Evoked Topography</figcaption>
        </figure>
        <figure>
          <img src="../assets/figures/plot/frequency.png" alt="Frequency spectrum" />
          <figcaption>Frequency Spectrum</figcaption>
        </figure>
        <figure>
          <img src="../assets/figures/plot/psd_grid.png" alt="PSD grid" />
          <figcaption>Power Spectral Density</figcaption>
        </figure>
        <figure>
          <img src="../assets/figures/plot/epochs.png" alt="Epoch overview" />
          <figcaption>Epoch Overview</figcaption>
        </figure>
      </div>

    </div>
  </div>

</div>

<!-- Row 3 — Research | Future Work -->
<div class="row row-bottom">

  <div class="card">
    <h2>Research Findings</h2>
    <h3>Study Setup</h3>
    <ul>
      <li><strong>Dataset:</strong> Healthy Brain Network EEG data</li>
      <li><strong>Task:</strong> Contrast Change Detection (CCD)</li>
      <li><strong>Model:</strong> Deep learning neural network</li>
    </ul>
    <h3>Predictive Models</h3>
    <ul>
      <li><strong>Correctness Prediction:</strong> Model was too good at predicting "correct" responses but failed to detect "incorrect" ones. In one run: 95% of correct trials detected, but only 10% of mistakes.</li>
      <li><strong>Reaction Time Prediction:</strong> Model performed only slightly better than just guessing the average. R² score near 0, meaning the brain signals captured almost no useful pattern.</li>
      <li><strong>Why so limited?</strong> Brain signals before a task contain only weak hints about behavior. Noise from sensors and individual differences between people also mask useful patterns.</li>
    </ul>
  </div>

  <div class="card">
    <h2>Future Work</h2>
    <ul>
      <li><strong>Better model balance:</strong> Fix the imbalance problem (95% vs 10%) by changing how the model learns from mistakes vs correct trials.</li>
      <li><strong>Add more signal types:</strong> Include frequency patterns and brain connectivity to give the model richer information instead of just raw signals.</li>
      <li><strong>Easier for others to extend:</strong> Document plugin points so researchers can quickly add new preprocessing steps or feature types without rewriting code.</li>
      <li><strong>Tutorial and examples:</strong> Provide step-by-step guides and sample workflows so new users don't need developer support to run experiments.</li>
      <li><strong>User feedback:</strong> Test the interface with real users and collect satisfaction surveys to identify confusing steps.</li>
    </ul>
  </div>

</div>

<!-- Footer -->
<div class="footer">
  <div><strong>Keywords:</strong> Brain-Computer Interfaces · EEG · Behavior Prediction · Open Science · Reproducibility</div>
  <div><strong>Contact:</strong> nantawat.s / naytitorn.c @ ku.th</div>
</div>

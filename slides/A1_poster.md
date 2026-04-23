---
marp: true
theme: a1
size: a1
paginate: false
style: |
  section {
    font-family: "Segoe UI", "Tahoma", sans-serif;
    padding: 8mm;
    background: #f7f7f5;
    color: #111;
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 100%;
  }

  h1 {
    font-size: 62px;
    margin: 0 0 8px 0;
    color: #8b0000;
    line-height: 1.05;
  }

  h2 {
    font-size: 34px;
    margin: 0 0 6px 0;
    color: #8b0000;
    border-bottom: 3px solid #8b0000;
    padding-bottom: 3px;
  }

  h3 {
    font-size: 24px;
    margin: 6px 0;
    color: #222;
  }

  p, li {
    font-size: 22px;
    line-height: 1.3;
  }

  ul {
    margin: 4px 0 8px 18px;
    padding: 0;
  }

  .titlebar {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    gap: 12px;
    margin-bottom: 8px;
  }

  .meta {
    font-size: 18px;
    line-height: 1.25;
    text-align: right;
  }

  .grid {
    flex: 1;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    gap: 10px;
    min-height: 0;
  }

  .card {
    background: #ffffff;
    border: 1px solid #d8d8d8;
    border-left: 8px solid #8b0000;
    border-radius: 8px;
    padding: 8px 10px;
    min-height: 0;
    overflow: hidden;
  }

  .imgbox {
    text-align: center;
  }

  .imgbox img {
    max-width: 100%;
    max-height: 230px;
    margin: 4px auto;
  }

  table {
    width: 100%;
    border-collapse: collapse;
    font-size: 18px;
  }

  th, td {
    border: 1px solid #bbb;
    padding: 6px 8px;
    text-align: left;
  }

  th {
    background: #f1ecec;
  }

  .footer {
    margin-top: 8px;
    font-size: 18px;
    line-height: 1.3;
    display: flex;
    justify-content: space-between;
    gap: 10px;
  }
---

<div class="titlebar">
  <div>
    <h1>EEG Analysis Platform for Prestimulus EEG-Based Behavioral Prediction</h1>
    <p><strong>Nantawat Suksirisunt, Naytitorn Chaovirachot</strong></p>
    <p>Vidyasirimedhi Institute of Science and Technology (VISTEC)</p>
  </div>
  <div class="meta">
    <p><strong>Advisors</strong><br/>Asst. Prof. Dr. Thanawin Rakthanmanon<br/>Assoc. Prof. Dr. Theerawit Wilaiprasitporn</p>
    <p><strong>Academic Year:</strong> 2565</p>
  </div>
</div>

<div class="grid">

<div class="card">
<h2>Background & Problem</h2>
<ul>
  <li>EEG analysis often relies on either rigid commercial tools or ad-hoc custom scripts.</li>
  <li>Result: weak reproducibility, low reusability, and hard-to-maintain pipelines.</li>
  <li>HBN-EEG has high complexity: many tasks, high-dimensional signals, and high subject variability.</li>
</ul>
<div class="imgbox">
  <img src="../assets/figures/HBN_subjsperRelease.png" alt="HBN release and subject complexity" />
</div>
</div>

<div class="card">
<h2>Objective</h2>
<ul>
  <li>Build a systematic, reproducible EEG analysis platform for domain researchers.</li>
  <li>Evaluate whether 2-second prestimulus EEG can predict:</li>
  <li>1) Reaction Time (regression), 2) Trial Correctness (classification).</li>
</ul>
<h3>Data & Task</h3>
<ul>
  <li>Dataset: Healthy Brain Network EEG (BIDS format)</li>
  <li>Task: Contrast Change Detection (CCD)</li>
  <li>Model: EEGNet</li>
</ul>
</div>

<div class="card">
<h2>System Design</h2>
<ul>
  <li>Layered architecture: Presentation, API, Application, Domain Processing, Infrastructure.</li>
  <li>Modular extension points for preprocessors, feature extractors, and models.</li>
  <li>Caching + explicit parameter logging for reproducibility and fast iteration.</li>
</ul>
<div class="imgbox">
  <img src="../assets/figures/architecture/design-class-diagram-eeg.png" alt="System architecture" />
</div>
</div>

<div class="card">
<h2>Implementation & Deliverables</h2>
<ul>
  <li>FastAPI backend + React frontend (modular mode-action workflow).</li>
  <li>Preprocessing pipeline: loading, filtering, artifact handling, epoching.</li>
  <li>Experiment tracking with W&amp;B and reproducible notebooks.</li>
  <li>Functional workflow coverage from data loading to model execution.</li>
</ul>
</div>

<div class="card">
<h2>Results</h2>
<h3>Classification (Correctness)</h3>
<table>
  <tr><th>Best Strategy</th><th>Accuracy</th><th>Balanced Acc</th></tr>
  <tr><td>Undersampling</td><td>0.652</td><td>0.537</td></tr>
</table>
<ul>
  <li>Baseline showed majority-class collapse (high sensitivity, near-zero specificity).</li>
</ul>
<h3>Regression (Reaction Time)</h3>
<table>
  <tr><th>Best Loss</th><th>MAE</th><th>R2</th></tr>
  <tr><td>Huber</td><td>0.2874</td><td>0.0079</td></tr>
</table>
<ul>
  <li>Near-zero R2 indicates weak predictive fit in current setup.</li>
</ul>
</div>

<div class="card">
<h2>Conclusion & Future Work</h2>
<ul>
  <li><strong>Success:</strong> strong software engineering baseline with reproducible workflow.</li>
  <li><strong>Limitation:</strong> predictive performance remains limited.</li>
  <li><strong>Next:</strong> transfer learning, subject-adaptive models, richer time-frequency/connectivity features.</li>
</ul>
<div class="imgbox">
  <img src="../assets/figures/BCI.png" alt="BCI and EEG" />
</div>
</div>

</div>

<div class="footer">
  <div><strong>Keywords:</strong> EEG, Reproducibility, BCI, EEGNet, CCD, FastAPI, React</div>
  <div><strong>Contact:</strong> Add email / GitHub link here</div>
</div>

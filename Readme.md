<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>SLC6A4 SNP Variant Pipeline — Group 01</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@400;600;700;800&display=swap" rel="stylesheet"/>
<style>
  :root {
    --bg: #050e1a;
    --surface: #0a1a2e;
    --surface2: #0f2240;
    --accent: #00d4ff;
    --accent2: #7b2fff;
    --accent3: #00ff9d;
    --warn: #ffb347;
    --text: #e8f4ff;
    --muted: #6b8aaa;
    --border: rgba(0,212,255,0.15);
    --glow: 0 0 30px rgba(0,212,255,0.25);
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Syne', sans-serif;
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* STAR FIELD */
  #stars {
    position: fixed; top: 0; left: 0; width: 100%; height: 100%;
    pointer-events: none; z-index: 0;
    background: radial-gradient(ellipse at 20% 50%, rgba(123,47,255,0.08) 0%, transparent 60%),
                radial-gradient(ellipse at 80% 20%, rgba(0,212,255,0.06) 0%, transparent 50%);
  }

  .star {
    position: absolute; border-radius: 50%;
    background: #fff; opacity: 0;
    animation: twinkle var(--d, 3s) ease-in-out infinite var(--delay, 0s);
  }

  @keyframes twinkle {
    0%,100% { opacity: 0; transform: scale(1); }
    50% { opacity: var(--op, 0.6); transform: scale(1.3); }
  }

  /* HERO */
  .hero {
    position: relative; z-index: 1;
    min-height: 100vh;
    display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    text-align: center;
    padding: 60px 20px;
    border-bottom: 1px solid var(--border);
  }

  .dna-helix {
    font-size: 48px;
    margin-bottom: 20px;
    animation: float 4s ease-in-out infinite;
  }
  @keyframes float { 0%,100%{transform:translateY(0)} 50%{transform:translateY(-12px)} }

  .hero-tag {
    font-family: 'Space Mono', monospace;
    font-size: 11px; letter-spacing: 3px;
    color: var(--accent); text-transform: uppercase;
    border: 1px solid var(--border);
    padding: 6px 18px; border-radius: 100px;
    margin-bottom: 28px;
    background: rgba(0,212,255,0.05);
    animation: fadeIn 0.8s ease;
  }

  .hero h1 {
    font-size: clamp(2.4rem, 6vw, 4.5rem);
    font-weight: 800; line-height: 1.1;
    background: linear-gradient(135deg, #fff 0%, var(--accent) 50%, var(--accent2) 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    background-clip: text;
    margin-bottom: 16px;
    animation: slideUp 0.8s ease 0.1s both;
  }

  .hero-sub {
    font-size: clamp(1rem, 2vw, 1.25rem);
    color: var(--muted); max-width: 640px;
    line-height: 1.7;
    animation: slideUp 0.8s ease 0.2s both;
    margin-bottom: 40px;
  }

  @keyframes slideUp { from{opacity:0;transform:translateY(24px)} to{opacity:1;transform:translateY(0)} }
  @keyframes fadeIn { from{opacity:0} to{opacity:1} }

  .badge-row {
    display: flex; flex-wrap: wrap; gap: 10px;
    justify-content: center; margin-bottom: 48px;
    animation: slideUp 0.8s ease 0.3s both;
  }

  .badge {
    font-family: 'Space Mono', monospace;
    font-size: 11px; font-weight: 700;
    padding: 7px 16px; border-radius: 6px;
    border: 1px solid;
    letter-spacing: 0.5px;
    transition: all 0.2s;
    cursor: default;
  }
  .badge:hover { transform: translateY(-2px); box-shadow: var(--glow); }
  .badge-cyan { color: var(--accent); border-color: rgba(0,212,255,0.3); background: rgba(0,212,255,0.05); }
  .badge-purple { color: var(--accent2); border-color: rgba(123,47,255,0.3); background: rgba(123,47,255,0.05); }
  .badge-green { color: var(--accent3); border-color: rgba(0,255,157,0.3); background: rgba(0,255,157,0.05); }
  .badge-warn { color: var(--warn); border-color: rgba(255,179,71,0.3); background: rgba(255,179,71,0.05); }

  /* NAV TABS */
  .nav-tabs {
    position: sticky; top: 0; z-index: 100;
    background: rgba(5,14,26,0.95);
    backdrop-filter: blur(20px);
    border-bottom: 1px solid var(--border);
    display: flex; justify-content: center;
    padding: 0 20px;
    overflow-x: auto;
  }

  .nav-tab {
    font-family: 'Space Mono', monospace;
    font-size: 11px; font-weight: 700;
    letter-spacing: 1px; text-transform: uppercase;
    color: var(--muted);
    padding: 18px 20px;
    cursor: pointer;
    border: none; background: none;
    border-bottom: 2px solid transparent;
    transition: all 0.25s;
    white-space: nowrap;
  }
  .nav-tab:hover { color: var(--text); }
  .nav-tab.active { color: var(--accent); border-bottom-color: var(--accent); }

  /* SECTIONS */
  .section {
    display: none; position: relative; z-index: 1;
    max-width: 1100px; margin: 0 auto;
    padding: 60px 24px;
    animation: fadeIn 0.4s ease;
  }
  .section.active { display: block; }

  .section-title {
    font-size: 2rem; font-weight: 800;
    margin-bottom: 8px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    background-clip: text;
  }
  .section-desc { color: var(--muted); margin-bottom: 40px; font-size: 0.95rem; line-height: 1.7; }

  /* CARDS */
  .card-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
    gap: 20px; margin-bottom: 40px;
  }

  .card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 28px 24px;
    transition: all 0.3s;
    position: relative; overflow: hidden;
  }
  .card::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0; height: 2px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    opacity: 0; transition: opacity 0.3s;
  }
  .card:hover { border-color: rgba(0,212,255,0.4); transform: translateY(-4px); box-shadow: var(--glow); }
  .card:hover::before { opacity: 1; }

  .card-icon { font-size: 28px; margin-bottom: 12px; }
  .card-title { font-size: 0.85rem; font-weight: 700; color: var(--muted); text-transform: uppercase; letter-spacing: 1px; margin-bottom: 6px; }
  .card-value { font-size: 1.6rem; font-weight: 800; color: var(--accent); font-family: 'Space Mono', monospace; }
  .card-sub { font-size: 0.8rem; color: var(--muted); margin-top: 4px; }

  /* PIPELINE */
  .pipeline {
    display: flex; flex-wrap: wrap;
    align-items: center; justify-content: center;
    gap: 0; margin: 40px 0;
  }

  .pipe-step {
    display: flex; flex-direction: column; align-items: center;
    text-align: center;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 20px 18px;
    width: 140px;
    transition: all 0.3s;
    cursor: pointer;
    position: relative;
  }
  .pipe-step:hover {
    border-color: var(--accent);
    background: var(--surface2);
    transform: scale(1.08);
    z-index: 2;
    box-shadow: var(--glow);
  }
  .pipe-step.active-step {
    border-color: var(--accent); background: var(--surface2);
  }

  .pipe-icon { font-size: 24px; margin-bottom: 8px; }
  .pipe-num {
    font-family: 'Space Mono', monospace;
    font-size: 9px; color: var(--accent); letter-spacing: 1px;
    margin-bottom: 4px;
  }
  .pipe-label { font-size: 0.78rem; font-weight: 700; }

  .pipe-arrow {
    color: var(--muted); font-size: 20px;
    margin: 0 4px; flex-shrink: 0;
  }

  .pipe-detail {
    display: none;
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 28px 32px;
    margin-top: 24px;
    animation: slideUp 0.3s ease;
  }
  .pipe-detail.show { display: block; }
  .pipe-detail h3 { font-size: 1.1rem; font-weight: 800; color: var(--accent); margin-bottom: 12px; }
  .pipe-detail p { color: var(--muted); line-height: 1.8; font-size: 0.93rem; }

  /* CODE BLOCK */
  .code-wrap {
    background: #020b15;
    border: 1px solid var(--border);
    border-radius: 12px;
    overflow: hidden;
    margin: 24px 0;
  }
  .code-header {
    display: flex; align-items: center; justify-content: space-between;
    padding: 12px 20px;
    background: var(--surface);
    border-bottom: 1px solid var(--border);
  }
  .code-lang {
    font-family: 'Space Mono', monospace;
    font-size: 11px; color: var(--accent); letter-spacing: 1px;
  }
  .copy-btn {
    font-family: 'Space Mono', monospace;
    font-size: 10px; color: var(--muted);
    background: none; border: 1px solid var(--border);
    border-radius: 6px; padding: 4px 12px;
    cursor: pointer; transition: all 0.2s;
  }
  .copy-btn:hover { color: var(--accent); border-color: var(--accent); }
  .dots { display: flex; gap: 6px; }
  .dot { width: 10px; height: 10px; border-radius: 50%; }
  .dot-r { background: #ff5f57; }
  .dot-y { background: #febc2e; }
  .dot-g { background: #28c840; }

  pre {
    font-family: 'Space Mono', monospace;
    font-size: 12.5px; line-height: 1.8;
    padding: 24px; overflow-x: auto;
    color: #a8d8ff;
  }
  .kw { color: #c792ea; }
  .fn { color: #82aaff; }
  .str { color: #c3e88d; }
  .cm { color: #546e7a; font-style: italic; }
  .num { color: #f78c6c; }

  /* MUTATION TABLE */
  .mut-table {
    width: 100%;
    border-collapse: collapse;
    margin: 24px 0;
    font-family: 'Space Mono', monospace;
    font-size: 13px;
  }
  .mut-table th {
    background: var(--surface2);
    color: var(--accent);
    padding: 14px 20px;
    text-align: left;
    font-size: 10px; letter-spacing: 2px;
    border-bottom: 2px solid var(--border);
  }
  .mut-table td {
    padding: 14px 20px;
    border-bottom: 1px solid var(--border);
    color: var(--text);
    transition: background 0.2s;
  }
  .mut-table tr:hover td { background: var(--surface); }
  .tag-syn { color: var(--accent3); font-size: 11px; font-weight: 700; }
  .tag-nonsyn { color: var(--warn); font-size: 11px; font-weight: 700; }
  .pos-chip {
    display: inline-block;
    background: rgba(0,212,255,0.1);
    color: var(--accent);
    border: 1px solid rgba(0,212,255,0.2);
    border-radius: 6px;
    padding: 3px 10px;
    font-size: 12px;
  }

  /* NETWORK VIZ */
  .network-container {
    background: #020b15;
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 32px;
    position: relative;
    overflow: hidden;
  }
  svg.network { width: 100%; max-height: 420px; }

  /* TEAM */
  .team-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 16px;
  }
  .team-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 24px 20px; text-align: center;
    transition: all 0.3s;
  }
  .team-card:hover {
    border-color: rgba(123,47,255,0.5);
    transform: translateY(-3px);
    box-shadow: 0 0 24px rgba(123,47,255,0.2);
  }
  .team-avatar {
    width: 52px; height: 52px; border-radius: 50%;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    display: flex; align-items: center; justify-content: center;
    font-size: 22px; margin: 0 auto 14px;
  }
  .team-name { font-weight: 700; font-size: 0.9rem; margin-bottom: 4px; }
  .team-role { font-size: 0.75rem; color: var(--muted); }

  /* STAT BARS */
  .stat-bar-wrap { margin: 12px 0; }
  .stat-bar-label {
    display: flex; justify-content: space-between;
    font-size: 12px; color: var(--muted);
    margin-bottom: 6px;
  }
  .stat-bar-track {
    height: 6px; background: var(--surface2);
    border-radius: 3px; overflow: hidden;
  }
  .stat-bar-fill {
    height: 100%; border-radius: 3px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    animation: barGrow 1.2s ease both;
  }
  @keyframes barGrow { from{width:0} }

  /* TABS inside section */
  .inner-tabs { display: flex; gap: 8px; margin-bottom: 28px; flex-wrap: wrap; }
  .inner-tab {
    font-size: 12px; font-weight: 700;
    padding: 8px 18px; border-radius: 8px;
    border: 1px solid var(--border);
    background: none; color: var(--muted);
    cursor: pointer; transition: all 0.2s;
    font-family: 'Space Mono', monospace;
    letter-spacing: 0.5px;
  }
  .inner-tab:hover { color: var(--text); border-color: rgba(255,255,255,0.2); }
  .inner-tab.active { background: var(--accent); color: #000; border-color: var(--accent); }

  .inner-panel { display: none; }
  .inner-panel.active { display: block; animation: fadeIn 0.3s ease; }

  /* SCROLLBAR */
  ::-webkit-scrollbar { width: 6px; height: 6px; }
  ::-webkit-scrollbar-track { background: var(--bg); }
  ::-webkit-scrollbar-thumb { background: var(--surface2); border-radius: 3px; }

  .divider {
    height: 1px; background: var(--border);
    margin: 40px 0;
  }

  .highlight-box {
    background: rgba(0,212,255,0.04);
    border: 1px solid rgba(0,212,255,0.2);
    border-left: 3px solid var(--accent);
    border-radius: 0 10px 10px 0;
    padding: 18px 22px;
    margin: 20px 0;
    font-size: 0.92rem; line-height: 1.8;
    color: var(--text);
  }

  .two-col { display: grid; grid-template-columns: 1fr 1fr; gap: 24px; }
  @media(max-width: 640px) { .two-col { grid-template-columns: 1fr; } }

  footer {
    text-align: center;
    padding: 40px 20px;
    color: var(--muted);
    font-size: 12px;
    font-family: 'Space Mono', monospace;
    border-top: 1px solid var(--border);
    position: relative; z-index: 1;
  }
</style>
</head>
<body>

<div id="stars"></div>

<!-- HERO -->
<section class="hero">
  <div class="dna-helix">🧬</div>
  <div class="hero-tag">Group 01 · Bioinformatics Analysis Lab · COMSATS University</div>
  <h1>SLC6A4 Variant<br/>Detection Pipeline</h1>
  <p class="hero-sub">
    An end-to-end computational genomics pipeline for simulating, mapping, and functionally evaluating
    single-nucleotide polymorphisms in the human Serotonin Transporter gene.
  </p>
  <div class="badge-row">
    <span class="badge badge-cyan">Python 3.10+</span>
    <span class="badge badge-purple">Bowtie2 Alignment</span>
    <span class="badge badge-green">Galaxy Platform</span>
    <span class="badge badge-warn">Cytoscape Network</span>
    <span class="badge badge-cyan">SNP Analysis</span>
    <span class="badge badge-purple">NCBI GenBank</span>
    <span class="badge badge-green">NGS Simulation</span>
    <span class="badge badge-warn">Edit Distance</span>
  </div>
</section>

<!-- NAV -->
<nav class="nav-tabs">
  <button class="nav-tab active" onclick="showSection('overview')">Overview</button>
  <button class="nav-tab" onclick="showSection('pipeline')">Pipeline</button>
  <button class="nav-tab" onclick="showSection('mutations')">Mutations</button>
  <button class="nav-tab" onclick="showSection('code')">Code</button>
  <button class="nav-tab" onclick="showSection('results')">Results</button>
  <button class="nav-tab" onclick="showSection('network')">Network</button>
  <button class="nav-tab" onclick="showSection('team')">Team</button>
</nav>

<!-- OVERVIEW -->
<section id="s-overview" class="section active">
  <div class="section-title">Project Overview</div>
  <p class="section-desc">
    The SLC6A4 gene (Chromosome 17q11.2) encodes the integral membrane serotonin transporter protein,
    governing serotonergic signaling implicated in MDD, anxiety, OCD, and SSRI response.
  </p>

  <div class="card-grid">
    <div class="card">
      <div class="card-icon">🧬</div>
      <div class="card-title">Target Gene</div>
      <div class="card-value">SLC6A4</div>
      <div class="card-sub">Serotonin Transporter · Chr 17q11.2</div>
    </div>
    <div class="card">
      <div class="card-icon">📏</div>
      <div class="card-title">Sequence Length</div>
      <div class="card-value">2,102 bp</div>
      <div class="card-sub">Full CDS transcript</div>
    </div>
    <div class="card">
      <div class="card-icon">🔀</div>
      <div class="card-title">SNPs Introduced</div>
      <div class="card-value">3</div>
      <div class="card-sub">Positions 12, 45, 78</div>
    </div>
    <div class="card">
      <div class="card-icon">📐</div>
      <div class="card-title">Edit Distance</div>
      <div class="card-value">3</div>
      <div class="card-sub">Hamming distance validated</div>
    </div>
    <div class="card">
      <div class="card-icon">🎞️</div>
      <div class="card-title">Read Length</div>
      <div class="card-value">50 bp</div>
      <div class="card-sub">Step size: 10 bp overlap</div>
    </div>
    <div class="card">
      <div class="card-icon">📦</div>
      <div class="card-title">Total Reads</div>
      <div class="card-value">206</div>
      <div class="card-sub">Synthetic NGS fragments</div>
    </div>
    <div class="card">
      <div class="card-icon">🏆</div>
      <div class="card-title">Alignment</div>
      <div class="card-value">100%</div>
      <div class="card-sub">FLAG 0 · Forward match</div>
    </div>
    <div class="card">
      <div class="card-icon">🔬</div>
      <div class="card-title">Alignment Tool</div>
      <div class="card-value">Bowtie2</div>
      <div class="card-sub">Galaxy platform · DNA index</div>
    </div>
  </div>

  <div class="highlight-box">
    💡 <strong>Key Insight:</strong> Short-read alignment engines require unified alphabets. Running nucleotide 
    fragments against protein coordinates results in unmapped states (<code>FLAG 4</code>). Resolving this via 
    a pure DNA reference index guarantees perfect mapping execution with <code>FLAG 0</code> (forward match).
  </div>

  <div class="divider"></div>

  <div class="two-col">
    <div>
      <h3 style="font-size:1rem;font-weight:800;margin-bottom:16px;color:var(--accent)">Biological Context</h3>
      <p style="color:var(--muted);line-height:1.8;font-size:0.9rem">
        SLC6A4 transports serotonin (5-HT) from the synaptic cleft back into presynaptic neurons. 
        Variants in this gene are strongly associated with major depressive disorder (MDD), 
        obsessive-compulsive disorder (OCD), and differential response to SSRIs like fluoxetine.
        The 5-HTTLPR promoter polymorphism is among the most studied psychiatric risk variants.
      </p>
    </div>
    <div>
      <h3 style="font-size:1rem;font-weight:800;margin-bottom:16px;color:var(--accent2)">Pipeline Significance</h3>
      <p style="color:var(--muted);line-height:1.8;font-size:0.9rem">
        This pipeline simulates a real-world NGS variant calling workflow — from mutation induction
        through read simulation, alignment, and functional interpretation — entirely in silico.
        It demonstrates how bioinformatics tools can trace genotype-to-phenotype relationships 
        at single-nucleotide resolution.
      </p>
    </div>
  </div>
</section>

<!-- PIPELINE -->
<section id="s-pipeline" class="section">
  <div class="section-title">Computational Pipeline</div>
  <p class="section-desc">Click each step to learn more about the methodology.</p>

  <div class="pipeline" id="pipeline-steps">
    <div class="pipe-step" onclick="showPipeDetail(0)">
      <div class="pipe-icon">🧬</div>
      <div class="pipe-num">STEP 01</div>
      <div class="pipe-label">Sequence Acquisition</div>
    </div>
    <div class="pipe-arrow">→</div>
    <div class="pipe-step" onclick="showPipeDetail(1)">
      <div class="pipe-icon">⚡</div>
      <div class="pipe-num">STEP 02</div>
      <div class="pipe-label">SNP Induction</div>
    </div>
    <div class="pipe-arrow">→</div>
    <div class="pipe-step" onclick="showPipeDetail(2)">
      <div class="pipe-icon">📐</div>
      <div class="pipe-num">STEP 03</div>
      <div class="pipe-label">Edit Distance</div>
    </div>
    <div class="pipe-arrow">→</div>
    <div class="pipe-step" onclick="showPipeDetail(3)">
      <div class="pipe-icon">🎞️</div>
      <div class="pipe-num">STEP 04</div>
      <div class="pipe-label">NGS Simulation</div>
    </div>
    <div class="pipe-arrow">→</div>
    <div class="pipe-step" onclick="showPipeDetail(4)">
      <div class="pipe-icon">🗺️</div>
      <div class="pipe-num">STEP 05</div>
      <div class="pipe-label">Alignment</div>
    </div>
    <div class="pipe-arrow">→</div>
    <div class="pipe-step" onclick="showPipeDetail(5)">
      <div class="pipe-icon">🔍</div>
      <div class="pipe-num">STEP 06</div>
      <div class="pipe-label">Variant Detection</div>
    </div>
    <div class="pipe-arrow">→</div>
    <div class="pipe-step" onclick="showPipeDetail(6)">
      <div class="pipe-icon">🕸️</div>
      <div class="pipe-num">STEP 07</div>
      <div class="pipe-label">Network Analysis</div>
    </div>
  </div>

  <div class="pipe-detail" id="pipe-detail-box">
    <h3 id="pipe-detail-title">Select a step above</h3>
    <p id="pipe-detail-text">Click any pipeline step to see its detailed description.</p>
  </div>
</section>

<!-- MUTATIONS -->
<section id="s-mutations" class="section">
  <div class="section-title">Mutation Analysis</div>
  <p class="section-desc">Three SNPs introduced into the SLC6A4 CDS at positions 12, 45, and 78. Each classified for synonymous/non-synonymous status and polarity/charge impact.</p>

  <div class="inner-tabs">
    <button class="inner-tab active" onclick="showInner('mut-table-panel')">Mutation Table</button>
    <button class="inner-tab" onclick="showInner('mut-codon-panel')">Codon Analysis</button>
    <button class="inner-tab" onclick="showInner('mut-protein-panel')">Protein Impact</button>
  </div>

  <div id="mut-table-panel" class="inner-panel active">
    <table class="mut-table">
      <thead>
        <tr>
          <th>Position</th>
          <th>Original</th>
          <th>Mutant</th>
          <th>Codon Pos</th>
          <th>Amino Acid Change</th>
          <th>Type</th>
          <th>Polarity Impact</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><span class="pos-chip">12</span></td>
          <td style="color:#ff6b6b">A</td>
          <td style="color:var(--accent3)">T</td>
          <td>Codon 4, Pos 3</td>
          <td>Glu → Glu</td>
          <td><span class="tag-syn">SYNONYMOUS</span></td>
          <td>No change · Acidic retained</td>
        </tr>
        <tr>
          <td><span class="pos-chip">45</span></td>
          <td style="color:#ff6b6b">T</td>
          <td style="color:var(--accent3)">G</td>
          <td>Codon 15, Pos 3</td>
          <td>Asn → Lys</td>
          <td><span class="tag-nonsyn">NON-SYNONYMOUS</span></td>
          <td>Polar → Positively charged (+)</td>
        </tr>
        <tr>
          <td><span class="pos-chip">78</span></td>
          <td style="color:#ff6b6b">A</td>
          <td style="color:var(--accent3)">C</td>
          <td>Codon 26, Pos 3</td>
          <td>Arg → Pro</td>
          <td><span class="tag-nonsyn">NON-SYNONYMOUS</span></td>
          <td>Positively charged → Nonpolar (−)</td>
        </tr>
      </tbody>
    </table>

    <div class="highlight-box">
      <strong>Special Task Result:</strong> Of 3 SNPs, 2 are non-synonymous with direct polarity/charge changes.
      Position 45 (Asn→Lys) gains positive charge; position 78 (Arg→Pro) loses positive charge and introduces
      a helix-breaking residue. Position 12 is silent (synonymous) with no protein effect.
    </div>
  </div>

  <div id="mut-codon-panel" class="inner-panel">
    <div class="two-col">
      <div class="card">
        <div class="card-icon">📍</div>
        <div class="card-title">Position 12 · A→T</div>
        <div style="margin-top:14px;font-family:'Space Mono',monospace;font-size:13px">
          <div style="color:var(--muted);margin-bottom:8px">Codon 4 context:</div>
          <div style="color:var(--text)">Original: &nbsp;GAG <span style="color:var(--accent)">A</span>AT</div>
          <div style="color:var(--text)">Mutated: &nbsp;GAG <span style="color:var(--accent3)">T</span>AT</div>
          <div style="margin-top:12px;color:var(--accent3);font-size:11px">GAG → GAG · Glu = Glu</div>
          <div style="color:var(--muted);font-size:11px;margin-top:4px">Silent mutation · 3rd codon position</div>
        </div>
      </div>
      <div class="card">
        <div class="card-icon">📍</div>
        <div class="card-title">Position 45 · T→G</div>
        <div style="margin-top:14px;font-family:'Space Mono',monospace;font-size:13px">
          <div style="color:var(--muted);margin-bottom:8px">Codon 15 context:</div>
          <div style="color:var(--text)">Original: &nbsp;AA<span style="color:#ff6b6b">T</span></div>
          <div style="color:var(--text)">Mutated: &nbsp;AA<span style="color:var(--accent3)">G</span></div>
          <div style="margin-top:12px;color:var(--warn);font-size:11px">AAT → AAG · Asn → Lys</div>
          <div style="color:var(--muted);font-size:11px;margin-top:4px">Polar → Basic (+) charge change</div>
        </div>
      </div>
    </div>
    <div class="card" style="margin-top:20px">
      <div class="card-icon">📍</div>
      <div class="card-title">Position 78 · A→C</div>
      <div style="margin-top:14px;font-family:'Space Mono',monospace;font-size:13px">
        <div style="color:var(--muted);margin-bottom:8px">Codon 26 context:</div>
        <div style="color:var(--text)">Original: &nbsp;CG<span style="color:#ff6b6b">A</span> → Arg</div>
        <div style="color:var(--text)">Mutated: &nbsp;CG<span style="color:var(--accent3)">C</span> → Pro</div>
        <div style="margin-top:12px;color:var(--warn);font-size:11px">CGA → CGC · Arg → Pro</div>
        <div style="color:var(--muted);font-size:11px;margin-top:4px">Loss of positive charge + Pro introduces structural rigidity (helix-breaker)</div>
      </div>
    </div>
  </div>

  <div id="mut-protein-panel" class="inner-panel">
    <div class="highlight-box" style="border-left-color:var(--warn)">
      <strong>⚠️ Functional Significance:</strong> The SNP at position 78 (Arg→Pro) is the most impactful.
      Arginine is a positively charged residue critical for membrane interactions in transmembrane domains.
      Proline substitutions disrupt α-helical structure — a particularly damaging effect in a 12-transmembrane
      transporter protein like SERT.
    </div>

    <div class="card-grid" style="margin-top:24px">
      <div class="card">
        <div class="card-title">Synonymous SNPs</div>
        <div class="card-value" style="color:var(--accent3)">1</div>
        <div class="card-sub">Position 12 · A→T · Silent</div>
        <div class="stat-bar-wrap" style="margin-top:14px">
          <div class="stat-bar-track"><div class="stat-bar-fill" style="width:33%;background:var(--accent3)"></div></div>
        </div>
      </div>
      <div class="card">
        <div class="card-title">Non-synonymous SNPs</div>
        <div class="card-value" style="color:var(--warn)">2</div>
        <div class="card-sub">Positions 45 & 78 · Protein change</div>
        <div class="stat-bar-wrap" style="margin-top:14px">
          <div class="stat-bar-track"><div class="stat-bar-fill" style="width:67%;background:var(--warn)"></div></div>
        </div>
      </div>
      <div class="card">
        <div class="card-title">Polarity Changes</div>
        <div class="card-value" style="color:var(--accent2)">2</div>
        <div class="card-sub">Both non-syn SNPs alter charge</div>
        <div class="stat-bar-wrap" style="margin-top:14px">
          <div class="stat-bar-track"><div class="stat-bar-fill" style="width:100%;background:var(--accent2)"></div></div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- CODE -->
<section id="s-code" class="section">
  <div class="section-title">Source Code</div>
  <p class="section-desc">Core Python functions from the Jupyter Notebook pipeline.</p>

  <div class="inner-tabs">
    <button class="inner-tab active" onclick="showInner('code-snp')">SNP Introduction</button>
    <button class="inner-tab" onclick="showInner('code-edit')">Edit Distance</button>
    <button class="inner-tab" onclick="showInner('code-ngs')">NGS Simulation</button>
  </div>

  <div id="code-snp" class="inner-panel active">
    <div class="code-wrap">
      <div class="code-header">
        <div class="dots"><div class="dot dot-r"></div><div class="dot dot-y"></div><div class="dot dot-g"></div></div>
        <span class="code-lang">PYTHON · snp_introduction.py</span>
        <button class="copy-btn" onclick="copyCode('snp-code')">COPY</button>
      </div>
      <pre id="snp-code"><span class="cm"># Introduce a point SNP at a given 1-based position</span>
<span class="kw">def</span> <span class="fn">introduce_snp</span>(sequence, position, new_nucleotide):
    index = position - <span class="num">1</span>  <span class="cm"># Convert to 0-based index</span>
    
    <span class="fn">print</span>(<span class="str">f"Position {position} (Index {index}): "</span>
          <span class="str">f"Changing '{sequence[index]}' to '{new_nucleotide}'"</span>)
    
    seq_list = <span class="fn">list</span>(sequence)
    seq_list[index] = new_nucleotide
    <span class="kw">return</span> <span class="str">""</span>.<span class="fn">join</span>(seq_list)

<span class="cm"># Apply 3 SNPs sequentially</span>
mutated_sequence = original_sequence
mutated_sequence = <span class="fn">introduce_snp</span>(mutated_sequence, <span class="num">12</span>, <span class="str">'T'</span>)  <span class="cm"># A→T</span>
mutated_sequence = <span class="fn">introduce_snp</span>(mutated_sequence, <span class="num">45</span>, <span class="str">'G'</span>)  <span class="cm"># T→G</span>
mutated_sequence = <span class="fn">introduce_snp</span>(mutated_sequence, <span class="num">78</span>, <span class="str">'C'</span>)  <span class="cm"># A→C</span></pre>
    </div>
  </div>

  <div id="code-edit" class="inner-panel">
    <div class="code-wrap">
      <div class="code-header">
        <div class="dots"><div class="dot dot-r"></div><div class="dot dot-y"></div><div class="dot dot-g"></div></div>
        <span class="code-lang">PYTHON · edit_distance.py</span>
        <button class="copy-btn" onclick="copyCode('edit-code')">COPY</button>
      </div>
      <pre id="edit-code"><span class="cm"># Hamming distance (equal-length sequences)</span>
<span class="kw">def</span> <span class="fn">calculate_edit_distance</span>(seq1, seq2):
    <span class="kw">if</span> <span class="fn">len</span>(seq1) != <span class="fn">len</span>(seq2):
        <span class="kw">return</span> <span class="str">"Error: Sequences have different lengths!"</span>
    
    distance = <span class="fn">sum</span>(<span class="num">1</span> <span class="kw">for</span> a, b <span class="kw">in</span> <span class="fn">zip</span>(seq1, seq2) <span class="kw">if</span> a != b)
    <span class="kw">return</span> distance

edit_dist = <span class="fn">calculate_edit_distance</span>(original_sequence, mutated_sequence)
<span class="fn">print</span>(<span class="str">f"Edit Distance: {edit_dist}"</span>)  <span class="cm"># Output: 3 ✓</span></pre>
    </div>
  </div>

  <div id="code-ngs" class="inner-panel">
    <div class="code-wrap">
      <div class="code-header">
        <div class="dots"><div class="dot dot-r"></div><div class="dot dot-y"></div><div class="dot dot-g"></div></div>
        <span class="code-lang">PYTHON · ngs_simulation.py</span>
        <button class="copy-btn" onclick="copyCode('ngs-code')">COPY</button>
      </div>
      <pre id="ngs-code"><span class="cm"># Sliding window NGS read simulation</span>
<span class="kw">def</span> <span class="fn">simulate_ngs_reads</span>(sequence, read_length=<span class="num">50</span>, step_size=<span class="num">10</span>):
    reads = []
    start = <span class="num">0</span>
    read_count = <span class="num">1</span>

    <span class="kw">while</span> start + read_length <= <span class="fn">len</span>(sequence):
        read_seq = sequence[start : start + read_length]
        fasta_record = <span class="str">f">Read_{read_count}\n{read_seq}"</span>
        reads.<span class="fn">append</span>(fasta_record)
        start += step_size
        read_count += <span class="num">1</span>

    <span class="kw">return</span> reads

<span class="cm"># Generate 206 synthetic reads from mutated sequence</span>
reads = <span class="fn">simulate_ngs_reads</span>(mutated_sequence, read_length=<span class="num">50</span>, step_size=<span class="num">10</span>)
<span class="fn">print</span>(<span class="str">f"Generated {len(reads)} reads"</span>)  <span class="cm"># Output: 206 reads ✓</span>

<span class="cm"># Export to FASTA for Bowtie2 alignment</span>
<span class="kw">with</span> <span class="fn">open</span>(<span class="str">"simulated_mutated_reads.fasta"</span>, <span class="str">"w"</span>) <span class="kw">as</span> f:
    f.<span class="fn">write</span>(<span class="str">"\n"</span>.<span class="fn">join</span>(reads))</pre>
    </div>
  </div>
</section>

<!-- RESULTS -->
<section id="s-results" class="section">
  <div class="section-title">Pipeline Results</div>
  <p class="section-desc">Summary of alignment, ORF prediction, and variant detection outputs.</p>

  <div class="card-grid">
    <div class="card">
      <div class="card-icon">🎯</div>
      <div class="card-title">Alignment Rate</div>
      <div class="card-value">100%</div>
      <div class="stat-bar-wrap">
        <div class="stat-bar-track"><div class="stat-bar-fill" style="width:100%"></div></div>
      </div>
      <div class="card-sub">All 206 reads mapped successfully</div>
    </div>
    <div class="card">
      <div class="card-icon">🏳️</div>
      <div class="card-title">SAM Flag</div>
      <div class="card-value">FLAG 0</div>
      <div class="card-sub">Forward strand · Perfect match</div>
    </div>
    <div class="card">
      <div class="card-icon">🔭</div>
      <div class="card-title">ORF Detected</div>
      <div class="card-value">1 ORF</div>
      <div class="card-sub">ATG → TAA · Full CDS preserved</div>
    </div>
    <div class="card">
      <div class="card-icon">⚠️</div>
      <div class="card-title">Variants Called</div>
      <div class="card-value">3 SNPs</div>
      <div class="card-sub">Positions 12, 45, 78 confirmed</div>
    </div>
  </div>

  <div class="divider"></div>

  <h3 style="font-size:1rem;font-weight:800;margin-bottom:16px;color:var(--accent)">Alignment Summary</h3>
  <table class="mut-table">
    <thead>
      <tr>
        <th>Metric</th><th>Value</th><th>Notes</th>
      </tr>
    </thead>
    <tbody>
      <tr><td>Total reads simulated</td><td style="color:var(--accent3);font-family:'Space Mono',monospace">206</td><td>50 bp reads · 10 bp step</td></tr>
      <tr><td>Reads aligned</td><td style="color:var(--accent3);font-family:'Space Mono',monospace">206</td><td>100% success rate</td></tr>
      <tr><td>Alignment flag</td><td style="color:var(--accent3);font-family:'Space Mono',monospace">FLAG 0</td><td>Forward strand match</td></tr>
      <tr><td>Reference index type</td><td style="color:var(--accent3);font-family:'Space Mono',monospace">DNA</td><td>Critical: nucleotide not protein</td></tr>
      <tr><td>Mismatch positions</td><td style="color:var(--warn);font-family:'Space Mono',monospace">12, 45, 78</td><td>Confirmed variant sites</td></tr>
      <tr><td>ORF frame</td><td style="color:var(--accent3);font-family:'Space Mono',monospace">Frame +1</td><td>ATG at pos 1 → TAA at end</td></tr>
    </tbody>
  </table>

  <div class="highlight-box" style="margin-top:32px;border-left-color:var(--accent2)">
    <strong>ORF Analysis:</strong> The open reading frame was preserved across all 3 SNPs — none introduced
    a premature stop codon. The single ORF spans the full CDS (positions 1–2102), confirming that the
    SNP set does not cause frameshift or nonsense mutations. All variants are missense (positions 45, 78)
    or silent (position 12).
  </div>
</section>

<!-- NETWORK -->
<section id="s-network" class="section">
  <div class="section-title">Cytoscape Network</div>
  <p class="section-desc">Gene → Variant → Effect → Function topology. Hover nodes to explore relationships.</p>

  <div class="network-container">
    <svg class="network" viewBox="0 0 800 420" xmlns="http://www.w3.org/2000/svg">
      <defs>
        <marker id="arrow" markerWidth="8" markerHeight="8" refX="6" refY="3" orient="auto">
          <path d="M0,0 L0,6 L8,3 z" fill="#00d4ff" opacity="0.5"/>
        </marker>
        <filter id="glow">
          <feGaussianBlur stdDeviation="3" result="coloredBlur"/>
          <feMerge><feMergeNode in="coloredBlur"/><feMergeNode in="SourceGraphic"/></feMerge>
        </filter>
      </defs>

      <!-- Edges -->
      <line x1="400" y1="55" x2="200" y2="155" stroke="#00d4ff" stroke-width="1.5" opacity="0.4" marker-end="url(#arrow)"/>
      <line x1="400" y1="55" x2="400" y2="150" stroke="#00d4ff" stroke-width="1.5" opacity="0.4" marker-end="url(#arrow)"/>
      <line x1="400" y1="55" x2="600" y2="155" stroke="#00d4ff" stroke-width="1.5" opacity="0.4" marker-end="url(#arrow)"/>

      <line x1="200" y1="185" x2="130" y2="270" stroke="#7b2fff" stroke-width="1.2" opacity="0.4" marker-end="url(#arrow)"/>
      <line x1="400" y1="185" x2="310" y2="270" stroke="#7b2fff" stroke-width="1.2" opacity="0.4" marker-end="url(#arrow)"/>
      <line x1="600" y1="185" x2="530" y2="270" stroke="#7b2fff" stroke-width="1.2" opacity="0.4" marker-end="url(#arrow)"/>
      <line x1="600" y1="185" x2="620" y2="270" stroke="#7b2fff" stroke-width="1.2" opacity="0.4" marker-end="url(#arrow)"/>

      <line x1="130" y1="300" x2="200" y2="370" stroke="#00ff9d" stroke-width="1" opacity="0.35" marker-end="url(#arrow)"/>
      <line x1="310" y1="300" x2="280" y2="370" stroke="#00ff9d" stroke-width="1" opacity="0.35" marker-end="url(#arrow)"/>
      <line x1="530" y1="300" x2="430" y2="370" stroke="#00ff9d" stroke-width="1" opacity="0.35" marker-end="url(#arrow)"/>
      <line x1="620" y1="300" x2="600" y2="370" stroke="#00ff9d" stroke-width="1" opacity="0.35" marker-end="url(#arrow)"/>

      <!-- Gene Node -->
      <circle cx="400" cy="40" r="30" fill="#0a1a2e" stroke="#00d4ff" stroke-width="2" filter="url(#glow)"/>
      <text x="400" y="35" text-anchor="middle" fill="#00d4ff" font-family="Space Mono" font-size="9" font-weight="bold">SLC6A4</text>
      <text x="400" y="48" text-anchor="middle" fill="#6b8aaa" font-family="Space Mono" font-size="7">GENE</text>

      <!-- SNP Nodes -->
      <rect x="155" y="155" width="90" height="34" rx="8" fill="#0a1a2e" stroke="#7b2fff" stroke-width="1.5"/>
      <text x="200" y="169" text-anchor="middle" fill="#c792ea" font-family="Space Mono" font-size="8" font-weight="bold">SNP pos.12</text>
      <text x="200" y="181" text-anchor="middle" fill="#6b8aaa" font-family="Space Mono" font-size="7">A→T · Silent</text>

      <rect x="355" y="155" width="90" height="34" rx="8" fill="#0a1a2e" stroke="#7b2fff" stroke-width="1.5"/>
      <text x="400" y="169" text-anchor="middle" fill="#c792ea" font-family="Space Mono" font-size="8" font-weight="bold">SNP pos.45</text>
      <text x="400" y="181" text-anchor="middle" fill="#6b8aaa" font-family="Space Mono" font-size="7">T→G · Asn→Lys</text>

      <rect x="555" y="155" width="90" height="34" rx="8" fill="#0a1a2e" stroke="#7b2fff" stroke-width="1.5"/>
      <text x="600" y="169" text-anchor="middle" fill="#c792ea" font-family="Space Mono" font-size="8" font-weight="bold">SNP pos.78</text>
      <text x="600" y="181" text-anchor="middle" fill="#6b8aaa" font-family="Space Mono" font-size="7">A→C · Arg→Pro</text>

      <!-- Effect Nodes -->
      <rect x="80" y="272" width="100" height="30" rx="6" fill="#0a1a2e" stroke="#ffb347" stroke-width="1.2"/>
      <text x="130" y="289" text-anchor="middle" fill="#ffb347" font-family="Space Mono" font-size="7.5">No AA Change</text>

      <rect x="255" y="272" width="110" height="30" rx="6" fill="#0a1a2e" stroke="#ffb347" stroke-width="1.2"/>
      <text x="310" y="289" text-anchor="middle" fill="#ffb347" font-family="Space Mono" font-size="7.5">+Charge Change</text>

      <rect x="480" y="272" width="100" height="30" rx="6" fill="#0a1a2e" stroke="#ffb347" stroke-width="1.2"/>
      <text x="530" y="289" text-anchor="middle" fill="#ffb347" font-family="Space Mono" font-size="7.5">-Charge Change</text>

      <rect x="570" y="272" width="100" height="30" rx="6" fill="#0a1a2e" stroke="#ffb347" stroke-width="1.2"/>
      <text x="620" y="289" text-anchor="middle" fill="#ffb347" font-family="Space Mono" font-size="7.5">Helix Disruption</text>

      <!-- Function Nodes -->
      <rect x="155" y="358" width="90" height="28" rx="6" fill="#0a1a2e" stroke="#00ff9d" stroke-width="1"/>
      <text x="200" y="375" text-anchor="middle" fill="#00ff9d" font-family="Space Mono" font-size="7">No SSRI Impact</text>

      <rect x="238" y="358" width="84" height="28" rx="6" fill="#0a1a2e" stroke="#00ff9d" stroke-width="1"/>
      <text x="280" y="375" text-anchor="middle" fill="#00ff9d" font-family="Space Mono" font-size="7">5-HT Binding ↓</text>

      <rect x="380" y="358" width="100" height="28" rx="6" fill="#0a1a2e" stroke="#00ff9d" stroke-width="1"/>
      <text x="430" y="375" text-anchor="middle" fill="#00ff9d" font-family="Space Mono" font-size="7">Transport Rate ↓</text>

      <rect x="550" y="358" width="100" height="28" rx="6" fill="#0a1a2e" stroke="#00ff9d" stroke-width="1"/>
      <text x="600" y="375" text-anchor="middle" fill="#00ff9d" font-family="Space Mono" font-size="7">MDD Risk ↑</text>

      <!-- Legend -->
      <circle cx="30" cy="390" r="5" fill="#0a1a2e" stroke="#00d4ff" stroke-width="1.5"/>
      <text x="40" y="394" fill="#6b8aaa" font-family="Space Mono" font-size="7">Gene</text>
      <rect x="70" y="385" width="12" height="8" rx="2" fill="#0a1a2e" stroke="#7b2fff" stroke-width="1"/>
      <text x="87" y="394" fill="#6b8aaa" font-family="Space Mono" font-size="7">Variant</text>
      <rect x="120" y="385" width="12" height="8" rx="2" fill="#0a1a2e" stroke="#ffb347" stroke-width="1"/>
      <text x="137" y="394" fill="#6b8aaa" font-family="Space Mono" font-size="7">Effect</text>
      <rect x="168" y="385" width="12" height="8" rx="2" fill="#0a1a2e" stroke="#00ff9d" stroke-width="1"/>
      <text x="185" y="394" fill="#6b8aaa" font-family="Space Mono" font-size="7">Function</text>
    </svg>
  </div>

  <div class="highlight-box" style="margin-top:24px">
    The network follows the project-required topology: <strong>Gene → Variant → Effect → Function</strong>.
    The Arg→Pro substitution at position 78 is the highest-impact node, connecting to both charge loss
    and structural disruption, which collectively elevate MDD/anxiety risk by reducing SERT transport capacity.
  </div>
</section>

<!-- TEAM -->
<section id="s-team" class="section">
  <div class="section-title">Team & Academic Context</div>
  <p class="section-desc">Group 01 · Bioinformatics (BSB) · COMSATS University Islamabad · Bioinformatics Analysis Lab, Final Project</p>

  <div class="team-grid" style="margin-bottom:40px">
    <div class="team-card">
      <div class="team-avatar">👨‍🔬</div>
      <div class="team-name">Group 01</div>
      <div class="team-role">SLC6A4 · SNP Analysis</div>
    </div>
    <div class="team-card">
      <div class="team-avatar">🧬</div>
      <div class="team-name">Gene Target</div>
      <div class="team-role">Serotonin Transporter</div>
    </div>
    <div class="team-card">
      <div class="team-avatar">🏫</div>
      <div class="team-name">COMSATS Islamabad</div>
      <div class="team-role">Bioinformatics Program (BSB)</div>
    </div>
    <div class="team-card">
      <div class="team-avatar">📅</div>
      <div class="team-name">Due Date</div>
      <div class="team-role">20th May 2026</div>
    </div>
  </div>

  <div class="divider"></div>

  <h3 style="font-size:1rem;font-weight:800;margin-bottom:16px;color:var(--accent)">Repository Structure</h3>
  <div class="code-wrap">
    <div class="code-header">
      <div class="dots"><div class="dot dot-r"></div><div class="dot dot-y"></div><div class="dot dot-g"></div></div>
      <span class="code-lang">FILE TREE</span>
    </div>
    <pre>SNP_Bioinfo_Project/
├── 📓 BALabProject.ipynb              <span class="cm"># Main pipeline notebook</span>
├── 🧬 slc6a4_original_sequence.txt   <span class="cm"># Reference FASTA (2102 bp)</span>
├── ⚡ simulated_mutated_reads.txt    <span class="cm"># 206 synthetic NGS reads</span>
├── 📄 Bioinformatics_Analysis_Report  <span class="cm"># Written report (docx)</span>
├── 📋 Lab_Final_Project.pdf           <span class="cm"># Assignment brief</span>
└── README.html                        <span class="cm"># This interactive README</span></pre>
  </div>

  <div class="divider"></div>

  <h3 style="font-size:1rem;font-weight:800;margin-bottom:16px;color:var(--accent)">Viva Preparation Q&A</h3>
  <div style="display:flex;flex-direction:column;gap:12px">
    <details style="background:var(--surface);border:1px solid var(--border);border-radius:10px;padding:16px 20px;cursor:pointer">
      <summary style="font-weight:700;font-size:0.9rem;list-style:none">What is a mutation?</summary>
      <p style="color:var(--muted);margin-top:10px;font-size:0.88rem;line-height:1.8">A permanent change in the DNA sequence of an organism. SNPs (single-nucleotide polymorphisms) are the most common — a single base is substituted with another. In this project, we introduced A→T at pos.12, T→G at pos.45, and A→C at pos.78.</p>
    </details>
    <details style="background:var(--surface);border:1px solid var(--border);border-radius:10px;padding:16px 20px;cursor:pointer">
      <summary style="font-weight:700;font-size:0.9rem;list-style:none">What is edit distance?</summary>
      <p style="color:var(--muted);margin-top:10px;font-size:0.88rem;line-height:1.8">The minimum number of edit operations to transform one string into another. For equal-length sequences (SNPs only), this is the Hamming distance — simply counting positions where characters differ. Our pipeline validated edit distance = 3, confirming exactly 3 SNPs were introduced.</p>
    </details>
    <details style="background:var(--surface);border:1px solid var(--border);border-radius:10px;padding:16px 20px;cursor:pointer">
      <summary style="font-weight:700;font-size:0.9rem;list-style:none">How does Bowtie2 work?</summary>
      <p style="color:var(--muted);margin-top:10px;font-size:0.88rem;line-height:1.8">Bowtie2 uses an FM-index (Burrows-Wheeler transform) to efficiently align short reads to a reference genome. It finds the best mapping position allowing mismatches/gaps, and reports results in SAM format with alignment flags. FLAG 0 = successfully mapped to forward strand.</p>
    </details>
    <details style="background:var(--surface);border:1px solid var(--border);border-radius:10px;padding:16px 20px;cursor:pointer">
      <summary style="font-weight:700;font-size:0.9rem;list-style:none">What is biological significance?</summary>
      <p style="color:var(--muted);margin-top:10px;font-size:0.88rem;line-height:1.8">Position 78 (Arg→Pro): Arginine is critical for serotonin binding and membrane interactions in SERT's transmembrane helices. Proline substitution breaks α-helical structure, likely reducing transport efficiency — potentially increasing synaptic serotonin dwell time or reducing SSRI efficacy.</p>
    </details>
  </div>
</section>

<footer>
  <p>🧬 SLC6A4 Variant Pipeline · Group 01 · Bioinformatics Analysis Lab</p>
  <p style="margin-top:6px">COMSATS University Islamabad · BSB · 2026</p>
</footer>

<script>
// Stars
const starField = document.getElementById('stars');
for (let i = 0; i < 80; i++) {
  const star = document.createElement('div');
  star.className = 'star';
  const size = Math.random() * 2.5 + 0.5;
  star.style.cssText = `
    width:${size}px; height:${size}px;
    left:${Math.random()*100}%;
    top:${Math.random()*100}%;
    --d:${2+Math.random()*4}s;
    --delay:${-Math.random()*5}s;
    --op:${0.3+Math.random()*0.6};
  `;
  starField.appendChild(star);
}

function showSection(id) {
  document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
  document.querySelectorAll('.nav-tab').forEach(t => t.classList.remove('active'));
  document.getElementById('s-' + id).classList.add('active');
  event.currentTarget.classList.add('active');
}

const pipeDetails = [
  {
    title: "Step 01 · Sequence Acquisition",
    text: "The SLC6A4 CDS (NM_001045.5) was retrieved from NCBI GenBank in FASTA format. The full coding sequence spans 2,102 bp, encoding the 630 amino acid serotonin transporter protein. This forms the reference genome for all downstream analysis."
  },
  {
    title: "Step 02 · SNP Induction",
    text: "Three point mutations were programmatically introduced at positions 12 (A→T), 45 (T→G), and 78 (A→C) using a Python function that converts the sequence to a list, substitutes the target position, and rebuilds the string. This simulates disease-associated variants."
  },
  {
    title: "Step 03 · Edit Distance Calculation",
    text: "A Hamming distance algorithm counted positions where the original and mutated sequences differ. The expected output of exactly 3 validates that only the intended mutations were introduced — an important quality control step before proceeding to read simulation."
  },
  {
    title: "Step 04 · NGS Read Simulation",
    text: "A sliding window approach generated synthetic short reads from the mutated sequence: 50 bp fragments with a 10 bp step size (40 bp overlap), producing 206 reads in FASTA format. This mimics real Illumina short-read sequencing output."
  },
  {
    title: "Step 05 · Bowtie2 Alignment (Galaxy)",
    text: "The 206 simulated reads were aligned against a DNA reference index of the original SLC6A4 sequence using Bowtie2 on the Galaxy platform. Using a DNA index (not protein) is critical — all 206 reads mapped successfully with FLAG 0 (forward strand match)."
  },
  {
    title: "Step 06 · Variant Detection",
    text: "Mismatches in the SAM alignment output at positions 12, 45, and 78 confirm the 3 introduced SNPs. Each variant was then classified: synonymous (position 12) or non-synonymous (positions 45, 78), with further analysis of amino acid polarity and charge changes."
  },
  {
    title: "Step 07 · Cytoscape Network Visualization",
    text: "A directed Gene→Variant→Effect→Function network was built in Cytoscape to map genotype-to-phenotype relationships. The network shows how each SNP flows through protein-level effects to clinical functional consequences — including reduced serotonin transport and elevated MDD risk."
  }
];

function showPipeDetail(idx) {
  document.querySelectorAll('.pipe-step').forEach((s, i) => {
    s.classList.toggle('active-step', i === idx * 2);
  });
  const box = document.getElementById('pipe-detail-box');
  box.classList.add('show');
  document.getElementById('pipe-detail-title').textContent = pipeDetails[idx].title;
  document.getElementById('pipe-detail-text').textContent = pipeDetails[idx].text;
}

function showInner(id) {
  const parent = event.currentTarget.closest('.section');
  parent.querySelectorAll('.inner-panel').forEach(p => p.classList.remove('active'));
  parent.querySelectorAll('.inner-tab').forEach(t => t.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  event.currentTarget.classList.add('active');
}

function copyCode(id) {
  const text = document.getElementById(id).innerText;
  navigator.clipboard.writeText(text).then(() => {
    event.currentTarget.textContent = 'COPIED!';
    setTimeout(() => event.currentTarget.textContent = 'COPY', 2000);
  });
}
</script>
</body>
</html>

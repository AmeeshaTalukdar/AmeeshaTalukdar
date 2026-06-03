<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ameesha Talukdar — README</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:ital,wght@0,400;0,700;1,400&family=Syne:wght@400;700;800&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #050508;
    --fg: #e8e4dc;
    --dim: #6b6760;
    --accent: #c8f060;
    --accent2: #60d4f0;
    --accent3: #f060b8;
    --card: #0d0d14;
    --border: rgba(255,255,255,0.07);
  }

  body {
    background: var(--bg);
    color: var(--fg);
    font-family: 'Space Mono', monospace;
    font-size: 14px;
    line-height: 1.7;
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  #cursor {
    position: fixed;
    width: 12px;
    height: 12px;
    background: var(--accent);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9999;
    mix-blend-mode: difference;
    transition: transform 0.1s ease, width 0.2s, height 0.2s;
  }
  #cursor-ring {
    position: fixed;
    width: 36px;
    height: 36px;
    border: 1px solid rgba(200,240,96,0.4);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9998;
    transition: transform 0.18s ease, width 0.2s, height 0.2s, border-color 0.2s;
  }

  /* Canvas */
  #bg-canvas {
    position: fixed;
    inset: 0;
    z-index: 0;
    opacity: 0.35;
  }

  .page {
    position: relative;
    z-index: 1;
    max-width: 860px;
    margin: 0 auto;
    padding: 0 32px 120px;
  }

  /* ── HERO ── */
  .hero {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 80px 0 60px;
  }

  .hero-eyebrow {
    font-size: 11px;
    letter-spacing: 0.22em;
    color: var(--dim);
    text-transform: uppercase;
    margin-bottom: 24px;
    opacity: 0;
    animation: fadeUp 0.6s 0.2s forwards;
  }

  .hero-name {
    font-family: 'Syne', sans-serif;
    font-size: clamp(52px, 10vw, 100px);
    font-weight: 800;
    line-height: 0.95;
    letter-spacing: -0.03em;
    margin-bottom: 24px;
    opacity: 0;
    animation: fadeUp 0.7s 0.4s forwards;
  }

  .hero-name span {
    display: inline-block;
    position: relative;
  }

  .hero-name .highlight {
    color: var(--accent);
    position: relative;
  }

  .hero-tagline {
    font-size: 13px;
    color: var(--dim);
    max-width: 480px;
    margin-bottom: 48px;
    opacity: 0;
    animation: fadeUp 0.7s 0.6s forwards;
  }

  .hero-stats {
    display: flex;
    gap: 40px;
    opacity: 0;
    animation: fadeUp 0.7s 0.8s forwards;
  }

  .hero-stat-num {
    font-family: 'Syne', sans-serif;
    font-size: 32px;
    font-weight: 800;
    color: var(--accent);
    display: block;
    line-height: 1;
  }

  .hero-stat-label {
    font-size: 10px;
    letter-spacing: 0.12em;
    color: var(--dim);
    text-transform: uppercase;
    margin-top: 4px;
  }

  /* ── SCROLL INDICATOR ── */
  .scroll-hint {
    position: absolute;
    bottom: 40px;
    left: 0;
    display: flex;
    align-items: center;
    gap: 12px;
    font-size: 11px;
    color: var(--dim);
    letter-spacing: 0.1em;
    opacity: 0;
    animation: fadeIn 1s 1.4s forwards;
  }

  .scroll-line {
    width: 40px;
    height: 1px;
    background: var(--dim);
    position: relative;
    overflow: hidden;
  }

  .scroll-line::after {
    content: '';
    position: absolute;
    inset: 0;
    background: var(--accent);
    transform: translateX(-100%);
    animation: scanLine 2s 1.5s ease-in-out infinite;
  }

  /* ── SECTION ── */
  section {
    padding: 80px 0;
    border-top: 1px solid var(--border);
  }

  .section-label {
    font-size: 10px;
    letter-spacing: 0.25em;
    color: var(--dim);
    text-transform: uppercase;
    margin-bottom: 40px;
    display: flex;
    align-items: center;
    gap: 16px;
  }

  .section-label::after {
    content: '';
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  /* ── ABOUT ── */
  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2px;
  }

  .about-row {
    display: contents;
  }

  .about-key {
    padding: 12px 0;
    color: var(--dim);
    font-size: 12px;
    border-bottom: 1px solid var(--border);
  }

  .about-val {
    padding: 12px 0;
    font-size: 12px;
    border-bottom: 1px solid var(--border);
  }

  .about-val .typing-cursor {
    display: inline-block;
    width: 2px;
    height: 14px;
    background: var(--accent);
    vertical-align: middle;
    animation: blink 1s step-end infinite;
    margin-left: 2px;
  }

  /* ── STACK ── */
  .stack-group {
    margin-bottom: 32px;
  }

  .stack-group-label {
    font-size: 10px;
    letter-spacing: 0.2em;
    color: var(--dim);
    text-transform: uppercase;
    margin-bottom: 12px;
  }

  .pills {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
  }

  .pill {
    padding: 6px 14px;
    border: 1px solid var(--border);
    border-radius: 2px;
    font-size: 12px;
    color: var(--fg);
    transition: border-color 0.2s, color 0.2s, transform 0.15s;
    cursor: default;
    position: relative;
    overflow: hidden;
  }

  .pill::before {
    content: '';
    position: absolute;
    inset: 0;
    background: var(--accent);
    transform: scaleX(0);
    transform-origin: left;
    transition: transform 0.25s ease;
    z-index: -1;
  }

  .pill:hover {
    color: var(--bg);
    border-color: var(--accent);
    transform: translateY(-2px);
  }

  .pill:hover::before {
    transform: scaleX(1);
  }

  /* ── EXPERIENCE ── */
  .exp-card {
    padding: 32px 0;
    border-bottom: 1px solid var(--border);
    display: grid;
    grid-template-columns: 200px 1fr;
    gap: 32px;
    position: relative;
  }

  .exp-card::before {
    content: '';
    position: absolute;
    left: -32px;
    top: 38px;
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background: var(--border);
    border: 1px solid var(--dim);
    transition: background 0.3s, border-color 0.3s;
  }

  .exp-card:hover::before {
    background: var(--accent);
    border-color: var(--accent);
  }

  .exp-org {
    font-family: 'Syne', sans-serif;
    font-size: 11px;
    font-weight: 700;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--dim);
  }

  .exp-role {
    font-size: 18px;
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    margin: 4px 0 12px;
    color: var(--fg);
  }

  .exp-desc {
    font-size: 12px;
    color: var(--dim);
    line-height: 1.8;
    margin-bottom: 16px;
  }

  .exp-desc .highlight-num {
    color: var(--accent);
    font-weight: 700;
  }

  .exp-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
  }

  .exp-tag {
    font-size: 10px;
    letter-spacing: 0.1em;
    padding: 3px 8px;
    border: 1px solid var(--border);
    border-radius: 2px;
    color: var(--dim);
    text-transform: uppercase;
  }

  /* ── HIGHLIGHTS COUNTER ── */
  .highlights {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
    margin-bottom: 64px;
  }

  .highlight-cell {
    background: var(--bg);
    padding: 28px 24px;
    text-align: center;
  }

  .highlight-cell .num {
    font-family: 'Syne', sans-serif;
    font-size: 40px;
    font-weight: 800;
    color: var(--accent);
    display: block;
    line-height: 1;
  }

  .highlight-cell .label {
    font-size: 10px;
    letter-spacing: 0.15em;
    color: var(--dim);
    text-transform: uppercase;
    margin-top: 8px;
    display: block;
  }

  /* ── INTERESTS ── */
  .interests-list {
    list-style: none;
  }

  .interest-item {
    display: flex;
    align-items: center;
    gap: 16px;
    padding: 16px 0;
    border-bottom: 1px solid var(--border);
    font-size: 13px;
    overflow: hidden;
    cursor: default;
  }

  .interest-num {
    font-family: 'Syne', sans-serif;
    font-size: 11px;
    color: var(--dim);
    min-width: 24px;
  }

  .interest-bar {
    height: 1px;
    background: var(--border);
    flex: 1;
    position: relative;
    overflow: hidden;
  }

  .interest-bar-fill {
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;
    background: var(--accent);
    width: 0%;
    transition: width 1.2s cubic-bezier(0.25, 1, 0.5, 1);
  }

  .interest-item:hover .interest-bar-fill { filter: brightness(1.2); }
  .interest-item:hover .interest-name { color: var(--accent); }
  .interest-name { transition: color 0.2s; }

  /* ── CONNECT ── */
  .connect-links {
    display: flex;
    gap: 0;
    flex-wrap: wrap;
    border: 1px solid var(--border);
  }

  .connect-link {
    flex: 1;
    min-width: 160px;
    padding: 28px 24px;
    text-decoration: none;
    color: var(--dim);
    font-size: 12px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    border-right: 1px solid var(--border);
    display: flex;
    flex-direction: column;
    gap: 8px;
    transition: background 0.2s, color 0.2s;
    position: relative;
    overflow: hidden;
  }

  .connect-link:last-child { border-right: none; }

  .connect-link .link-icon {
    font-family: 'Syne', sans-serif;
    font-size: 24px;
    font-weight: 800;
    display: block;
    color: var(--fg);
    transition: color 0.2s;
  }

  .connect-link:hover {
    background: var(--card);
    color: var(--accent);
  }

  .connect-link:hover .link-icon { color: var(--accent); }

  /* ── FOOTER ── */
  footer {
    padding: 40px 0;
    border-top: 1px solid var(--border);
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 10px;
    color: var(--dim);
    letter-spacing: 0.1em;
  }

  /* ── GLITCH ── */
  .glitch {
    position: relative;
    display: inline-block;
  }

  .glitch::before,
  .glitch::after {
    content: attr(data-text);
    position: absolute;
    top: 0; left: 0;
    color: inherit;
    font: inherit;
  }

  .glitch::before {
    animation: glitchTop 4s 2s infinite;
    clip-path: polygon(0 0, 100% 0, 100% 35%, 0 35%);
    color: var(--accent2);
    opacity: 0.8;
  }

  .glitch::after {
    animation: glitchBot 4s 2s infinite;
    clip-path: polygon(0 65%, 100% 65%, 100% 100%, 0 100%);
    color: var(--accent3);
    opacity: 0.8;
  }

  /* ── SCAN LINE overlay ── */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background: repeating-linear-gradient(
      0deg,
      transparent,
      transparent 3px,
      rgba(0,0,0,0.08) 3px,
      rgba(0,0,0,0.08) 4px
    );
    pointer-events: none;
    z-index: 998;
  }

  /* ── NOISE ── */
  body::after {
    content: '';
    position: fixed;
    inset: -200%;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='1'/%3E%3C/svg%3E");
    opacity: 0.025;
    pointer-events: none;
    z-index: 997;
    animation: noiseShift 0.4s steps(1) infinite;
  }

  /* ── KEYFRAMES ── */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to { opacity: 1; transform: translateY(0); }
  }

  @keyframes fadeIn {
    to { opacity: 1; }
  }

  @keyframes blink {
    50% { opacity: 0; }
  }

  @keyframes scanLine {
    0% { transform: translateX(-100%); }
    100% { transform: translateX(100%); }
  }

  @keyframes noiseShift {
    0% { transform: translate(0, 0); }
    25% { transform: translate(-1%, -2%); }
    50% { transform: translate(1%, 0); }
    75% { transform: translate(-2%, 1%); }
    100% { transform: translate(0, 0); }
  }

  @keyframes glitchTop {
    0%, 90%, 100% { transform: translate(0); opacity: 0; }
    92% { transform: translate(-3px, -1px); opacity: 0.9; }
    94% { transform: translate(3px, 0); opacity: 0; }
    96% { transform: translate(-2px, 1px); opacity: 0.7; }
    98% { transform: translate(0); opacity: 0; }
  }

  @keyframes glitchBot {
    0%, 90%, 100% { transform: translate(0); opacity: 0; }
    93% { transform: translate(3px, 1px); opacity: 0.9; }
    95% { transform: translate(-3px, 0); opacity: 0; }
    97% { transform: translate(2px, -1px); opacity: 0.7; }
    99% { transform: translate(0); opacity: 0; }
  }

  @keyframes float {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-8px); }
  }

  @keyframes countUp {
    from { opacity: 0; transform: translateY(10px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* ── OBSERVE FADE ── */
  .reveal {
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }

  .reveal.visible {
    opacity: 1;
    transform: translateY(0);
  }

  .reveal-delay-1 { transition-delay: 0.1s; }
  .reveal-delay-2 { transition-delay: 0.2s; }
  .reveal-delay-3 { transition-delay: 0.3s; }

  /* mobile */
  @media (max-width: 600px) {
    .about-grid { grid-template-columns: 1fr; }
    .exp-card { grid-template-columns: 1fr; gap: 8px; }
    .highlights { grid-template-columns: 1fr; }
    .hero-stats { flex-wrap: wrap; gap: 24px; }
  }
</style>
</head>
<body>

<div id="cursor"></div>
<div id="cursor-ring"></div>
<canvas id="bg-canvas"></canvas>

<div class="page">

  <!-- HERO -->
  <div class="hero" style="position:relative;">
    <div class="hero-eyebrow">README.md — last updated: always</div>

    <h1 class="hero-name">
      <span class="glitch" data-text="AMEESHA">AMEESHA</span><br>
      <span class="highlight">TALUKDAR</span>
    </h1>

    <p class="hero-tagline">
      I build machine learning systems that survive contact with reality —<br>
      computer vision, scalable pipelines, and models that actually ship.
    </p>

    <div class="hero-stats">
      <div>
        <span class="hero-stat-num" data-count="92">0</span>
        <div class="hero-stat-label">% mAP achieved</div>
      </div>
      <div>
        <span class="hero-stat-num" data-count="3" data-suffix="×">0</span>
        <div class="hero-stat-label">data throughput lift</div>
      </div>
      <div>
        <span class="hero-stat-num" data-count="500" data-suffix="K+">0</span>
        <div class="hero-stat-label">records / day</div>
      </div>
    </div>

    <div class="scroll-hint">
      <span class="scroll-line"></span>
      scroll
    </div>
  </div>

  <!-- ABOUT -->
  <section class="reveal">
    <div class="section-label">01 — about</div>
    <div class="about-grid">
      <div class="about-key">name:</div>
      <div class="about-val">Ameesha Talukdar</div>

      <div class="about-key">role:</div>
      <div class="about-val">CS Engineer · AI/ML · Computer Vision</div>

      <div class="about-key">affiliation:</div>
      <div class="about-val">National University of Singapore (NUS)</div>

      <div class="about-key">focus:</div>
      <div class="about-val">systems that survive contact with production</div>

      <div class="about-key">currently:</div>
      <div class="about-val" id="typing-target"><span class="typing-cursor"></span></div>

      <div class="about-key">weakness:</div>
      <div class="about-val">will re-tune a YOLO model past midnight for 2% mAP</div>

      <div class="about-key">portfolio:</div>
      <div class="about-val"><a href="https://ameeshatalukdar.github.io/Portfolio/" style="color:var(--accent); text-decoration:none;">ameeshatalukdar.github.io/Portfolio ↗</a></div>
    </div>
  </section>

  <!-- HIGHLIGHTS -->
  <section class="reveal">
    <div class="section-label">02 — numbers</div>
    <div class="highlights">
      <div class="highlight-cell">
        <span class="num counter" data-target="92" data-suffix="%">—</span>
        <span class="label">mAP on detection models</span>
      </div>
      <div class="highlight-cell">
        <span class="num counter" data-target="3" data-suffix="×">—</span>
        <span class="label">pipeline throughput improvement</span>
      </div>
      <div class="highlight-cell">
        <span class="num counter" data-target="500" data-suffix="K+/day">—</span>
        <span class="label">records processed in ETL</span>
      </div>
    </div>
  </section>

  <!-- INTERESTS -->
  <section class="reveal">
    <div class="section-label">03 — core interests</div>
    <ul class="interests-list">
      <li class="interest-item">
        <span class="interest-num">01</span>
        <span class="interest-name">Computer Vision &amp; Deep Learning</span>
        <div class="interest-bar"><div class="interest-bar-fill" data-width="92"></div></div>
      </li>
      <li class="interest-item">
        <span class="interest-num">02</span>
        <span class="interest-name">ML Systems Design</span>
        <div class="interest-bar"><div class="interest-bar-fill" data-width="85"></div></div>
      </li>
      <li class="interest-item">
        <span class="interest-num">03</span>
        <span class="interest-name">Scalable Data Pipelines</span>
        <div class="interest-bar"><div class="interest-bar-fill" data-width="78"></div></div>
      </li>
      <li class="interest-item">
        <span class="interest-num">04</span>
        <span class="interest-name">Privacy-Preserving ML</span>
        <div class="interest-bar"><div class="interest-bar-fill" data-width="70"></div></div>
      </li>
      <li class="interest-item">
        <span class="interest-num">05</span>
        <span class="interest-name">Reinforcement Learning</span>
        <div class="interest-bar"><div class="interest-bar-fill" data-width="65"></div></div>
      </li>
    </ul>
  </section>

  <!-- STACK -->
  <section class="reveal">
    <div class="section-label">04 — tech stack</div>

    <div class="stack-group">
      <div class="stack-group-label">Languages</div>
      <div class="pills">
        <div class="pill">Python</div>
        <div class="pill">C++</div>
        <div class="pill">Java</div>
        <div class="pill">SQL</div>
      </div>
    </div>

    <div class="stack-group">
      <div class="stack-group-label">Vision &amp; ML</div>
      <div class="pills">
        <div class="pill">PyTorch</div>
        <div class="pill">TensorFlow</div>
        <div class="pill">OpenCV</div>
        <div class="pill">Scikit-learn</div>
        <div class="pill">YOLOv8</div>
      </div>
    </div>

    <div class="stack-group">
      <div class="stack-group-label">Data &amp; Infra</div>
      <div class="pills">
        <div class="pill">Dask</div>
        <div class="pill">Spark</div>
        <div class="pill">PostgreSQL</div>
        <div class="pill">Power BI</div>
        <div class="pill">Docker</div>
        <div class="pill">ETL</div>
      </div>
    </div>
  </section>

  <!-- EXPERIENCE -->
  <section class="reveal">
    <div class="section-label">05 — shipped</div>

    <div class="exp-card reveal reveal-delay-1">
      <div>
        <div class="exp-org">NUS · Singapore</div>
      </div>
      <div>
        <div class="exp-role">AI Research — Computer Vision</div>
        <p class="exp-desc">
          Built YOLO-based detection systems and thermal imaging pipelines that went beyond benchmark runs into deployed analysis. Achieved <span class="highlight-num">92% mAP</span> on detection-heavy tasks. Pushed real-time inference boundaries where frame counts actually matter.
        </p>
        <div class="exp-tags">
          <span class="exp-tag">YOLOv8</span>
          <span class="exp-tag">Thermal Imaging</span>
          <span class="exp-tag">PyTorch</span>
          <span class="exp-tag">OpenCV</span>
        </div>
      </div>
    </div>

    <div class="exp-card reveal reveal-delay-2">
      <div>
        <div class="exp-org">Data Engineering</div>
      </div>
      <div>
        <div class="exp-role">Scalable ML Pipelines</div>
        <p class="exp-desc">
          Designed ETL pipelines ingesting <span class="highlight-num">500K+ records daily</span> into a star-schema warehouse. Delivered a <span class="highlight-num">3× throughput improvement</span> by restructuring pipeline architecture — not just tuning parameters, but rethinking the shape of the data flow. Learned that "the data is wrong" is rarely a hypothesis.
        </p>
        <div class="exp-tags">
          <span class="exp-tag">Python</span>
          <span class="exp-tag">SQL</span>
          <span class="exp-tag">Power BI</span>
          <span class="exp-tag">ETL</span>
          <span class="exp-tag">Dask</span>
        </div>
      </div>
    </div>

  </section>

  <!-- CONNECT -->
  <section class="reveal">
    <div class="section-label">06 — find me</div>
    <div class="connect-links">
      <a class="connect-link" href="https://ameeshatalukdar.github.io/Portfolio/" target="_blank">
        <span class="link-icon">↗</span>
        Portfolio
      </a>
      <a class="connect-link" href="https://linkedin.com" target="_blank">
        <span class="link-icon">in</span>
        LinkedIn
      </a>
      <a class="connect-link" href="mailto:ameesha@example.com">
        <span class="link-icon">✉</span>
        Email
      </a>
    </div>
  </section>

  <!-- FOOTER -->
  <footer>
    <span>AMEESHA TALUKDAR · CS ENGINEER</span>
    <span id="clock">--:--:--</span>
  </footer>

</div>

<script>
// ── CURSOR ──
const cur = document.getElementById('cursor');
const ring = document.getElementById('cursor-ring');
let mx = 0, my = 0, rx = 0, ry = 0;

document.addEventListener('mousemove', e => {
  mx = e.clientX; my = e.clientY;
  cur.style.left = mx - 6 + 'px';
  cur.style.top = my - 6 + 'px';
});

(function animRing() {
  rx += (mx - rx - 18) * 0.12;
  ry += (my - ry - 18) * 0.12;
  ring.style.left = rx + 'px';
  ring.style.top = ry + 'px';
  requestAnimationFrame(animRing);
})();

document.querySelectorAll('a, .pill, .interest-item, .connect-link').forEach(el => {
  el.addEventListener('mouseenter', () => {
    cur.style.transform = 'scale(2.5)';
    ring.style.transform = 'scale(1.5)';
    ring.style.borderColor = 'rgba(200,240,96,0.8)';
  });
  el.addEventListener('mouseleave', () => {
    cur.style.transform = 'scale(1)';
    ring.style.transform = 'scale(1)';
    ring.style.borderColor = 'rgba(200,240,96,0.4)';
  });
});

// ── CANVAS PARTICLES ──
const canvas = document.getElementById('bg-canvas');
const ctx = canvas.getContext('2d');
let W, H, particles = [];

function resize() {
  W = canvas.width = window.innerWidth;
  H = canvas.height = window.innerHeight;
}
resize();
window.addEventListener('resize', resize);

class Particle {
  constructor() { this.reset(); }
  reset() {
    this.x = Math.random() * W;
    this.y = Math.random() * H;
    this.size = Math.random() * 1.5 + 0.3;
    this.speedX = (Math.random() - 0.5) * 0.3;
    this.speedY = (Math.random() - 0.5) * 0.3;
    this.opacity = Math.random() * 0.6 + 0.1;
    this.color = Math.random() > 0.85 ? '#c8f060' : Math.random() > 0.7 ? '#60d4f0' : '#6b6760';
  }
  update() {
    this.x += this.speedX;
    this.y += this.speedY;
    if (this.x < 0 || this.x > W || this.y < 0 || this.y > H) this.reset();
  }
  draw() {
    ctx.beginPath();
    ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
    ctx.fillStyle = this.color;
    ctx.globalAlpha = this.opacity;
    ctx.fill();
  }
}

for (let i = 0; i < 180; i++) particles.push(new Particle());

// connection lines
function drawConnections() {
  for (let i = 0; i < particles.length; i++) {
    for (let j = i + 1; j < particles.length; j++) {
      const dx = particles[i].x - particles[j].x;
      const dy = particles[i].y - particles[j].y;
      const dist = Math.sqrt(dx*dx + dy*dy);
      if (dist < 90) {
        ctx.beginPath();
        ctx.moveTo(particles[i].x, particles[i].y);
        ctx.lineTo(particles[j].x, particles[j].y);
        ctx.strokeStyle = '#c8f060';
        ctx.globalAlpha = (1 - dist/90) * 0.08;
        ctx.lineWidth = 0.5;
        ctx.stroke();
      }
    }
  }
}

(function animCanvas() {
  ctx.clearRect(0, 0, W, H);
  particles.forEach(p => { p.update(); p.draw(); });
  drawConnections();
  requestAnimationFrame(animCanvas);
})();

// ── TYPING ──
const phrases = [
  'making thermal images speak',
  'training models that generalize',
  'debugging pipelines at odd hours',
  'pushing mAP past what's reasonable',
  'shipping ML into the real world',
];
let pi = 0, ci = 0, deleting = false;
const typingTarget = document.getElementById('typing-target');

function typeStep() {
  const phrase = phrases[pi];
  if (!deleting) {
    ci++;
    typingTarget.innerHTML = phrase.slice(0, ci) + '<span class="typing-cursor"></span>';
    if (ci === phrase.length) { deleting = true; setTimeout(typeStep, 2200); return; }
    setTimeout(typeStep, 55);
  } else {
    ci--;
    typingTarget.innerHTML = phrase.slice(0, ci) + '<span class="typing-cursor"></span>';
    if (ci === 0) {
      deleting = false;
      pi = (pi + 1) % phrases.length;
      setTimeout(typeStep, 400);
      return;
    }
    setTimeout(typeStep, 28);
  }
}
typeStep();

// ── CLOCK ──
function updateClock() {
  document.getElementById('clock').textContent = new Date().toLocaleTimeString('en-GB');
}
updateClock();
setInterval(updateClock, 1000);

// ── COUNTER ANIMATION ──
function animateCounter(el) {
  const target = parseInt(el.dataset.target);
  const suffix = el.dataset.suffix || '';
  let start = 0;
  const duration = 1400;
  const step = timestamp => {
    if (!start) start = timestamp;
    const progress = Math.min((timestamp - start) / duration, 1);
    const eased = 1 - Math.pow(1 - progress, 3);
    el.textContent = Math.round(eased * target) + suffix;
    if (progress < 1) requestAnimationFrame(step);
  };
  requestAnimationFrame(step);
}

// ── INTERSECTION OBSERVER ──
const observer = new IntersectionObserver(entries => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('visible');

      // trigger interest bars
      entry.target.querySelectorAll('.interest-bar-fill').forEach(bar => {
        setTimeout(() => { bar.style.width = bar.dataset.width + '%'; }, 200);
      });

      // trigger counters
      entry.target.querySelectorAll('.counter').forEach(el => {
        setTimeout(() => animateCounter(el), 300);
      });

      observer.unobserve(entry.target);
    }
  });
}, { threshold: 0.15 });

document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

// ── HERO STAT COUNT ──
window.addEventListener('load', () => {
  setTimeout(() => {
    document.querySelectorAll('[data-count]').forEach(el => {
      const target = parseInt(el.dataset.count);
      const suffix = el.dataset.suffix || '';
      let start = 0;
      const duration = 1800;
      const step = ts => {
        if (!start) start = ts;
        const prog = Math.min((ts - start) / duration, 1);
        const eased = 1 - Math.pow(1 - prog, 4);
        el.textContent = Math.round(eased * target) + suffix;
        if (prog < 1) requestAnimationFrame(step);
      };
      requestAnimationFrame(step);
    });
  }, 900);
});
</script>
</body>
</html>

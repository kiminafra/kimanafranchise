<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Kimana Franchise — UI/UX Designer</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=Outfit:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0a0a0a;
    --surface: #111111;
    --surface2: #1a1a1a;
    --border: rgba(255,255,255,0.07);
    --border2: rgba(255,255,255,0.12);
    --text: #f0ede8;
    --text2: #9b9690;
    --text3: #5c5955;
    --accent: #c8a96e;
    --accent2: #e8d5aa;
    --accent-dim: rgba(200,169,110,0.12);
    --accent-dim2: rgba(200,169,110,0.06);
    --green: #4caf7d;
    --green-dim: rgba(76,175,125,0.1);
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Outfit', sans-serif;
    font-weight: 300;
    line-height: 1.7;
    cursor: none;
  }

  /* Custom cursor */
  .cursor {
    position: fixed;
    width: 10px; height: 10px;
    background: var(--accent);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9999;
    transform: translate(-50%,-50%);
    transition: transform 0.1s, width 0.2s, height 0.2s, background 0.2s;
  }
  .cursor-ring {
    position: fixed;
    width: 36px; height: 36px;
    border: 1px solid rgba(200,169,110,0.4);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9998;
    transform: translate(-50%,-50%);
    transition: transform 0.15s ease-out, width 0.2s, height 0.2s, border-color 0.2s;
  }
  body:has(a:hover) .cursor, body:has(button:hover) .cursor { width: 6px; height: 6px; }
  body:has(a:hover) .cursor-ring, body:has(button:hover) .cursor-ring {
    width: 52px; height: 52px;
    border-color: var(--accent);
  }

  /* Noise overlay */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.03'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 1000;
    opacity: 0.4;
  }

  /* Nav */
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 100;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1.25rem 3rem;
    border-bottom: 1px solid var(--border);
    background: rgba(10,10,10,0.85);
    backdrop-filter: blur(16px);
  }
  .nav-logo {
    font-family: 'Playfair Display', serif;
    font-size: 1.1rem;
    letter-spacing: 0.02em;
    color: var(--text);
    text-decoration: none;
  }
  .nav-logo span { color: var(--accent); }
  .nav-links { display: flex; gap: 2rem; list-style: none; }
  .nav-links a {
    font-size: 0.8rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--text2);
    text-decoration: none;
    transition: color 0.2s;
  }
  .nav-links a:hover { color: var(--accent); }
  .nav-badge {
    font-size: 0.72rem;
    padding: 4px 12px;
    border: 1px solid rgba(76,175,125,0.4);
    border-radius: 100px;
    color: var(--green);
    letter-spacing: 0.08em;
  }
  .nav-badge::before {
    content: '●';
    margin-right: 6px;
    animation: blink 2s infinite;
  }
  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0.3} }

  /* Hero */
  .hero {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    padding: 0 3rem 4rem;
    position: relative;
    overflow: hidden;
  }
  .hero-bg-text {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-family: 'Playfair Display', serif;
    font-size: clamp(100px, 18vw, 220px);
    font-weight: 700;
    color: rgba(255,255,255,0.02);
    white-space: nowrap;
    pointer-events: none;
    user-select: none;
    letter-spacing: -0.04em;
  }
  .hero-line {
    width: 1px;
    height: 80px;
    background: linear-gradient(to bottom, transparent, var(--accent));
    margin-bottom: 2rem;
    animation: grow 1s ease forwards;
    transform-origin: top;
  }
  @keyframes grow { from{transform:scaleY(0)} to{transform:scaleY(1)} }
  .hero-tag {
    font-size: 0.72rem;
    letter-spacing: 0.18em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 1.5rem;
    opacity: 0;
    animation: fadeUp 0.8s 0.2s forwards;
  }
  .hero-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(3rem, 7vw, 6rem);
    font-weight: 400;
    line-height: 1.05;
    letter-spacing: -0.02em;
    margin-bottom: 1.5rem;
    opacity: 0;
    animation: fadeUp 0.8s 0.4s forwards;
  }
  .hero-title em {
    font-style: italic;
    color: var(--accent);
  }
  .hero-desc {
    max-width: 500px;
    font-size: 1rem;
    color: var(--text2);
    line-height: 1.8;
    margin-bottom: 2.5rem;
    opacity: 0;
    animation: fadeUp 0.8s 0.6s forwards;
  }
  .hero-actions {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
    opacity: 0;
    animation: fadeUp 0.8s 0.8s forwards;
  }
  @keyframes fadeUp {
    from { opacity:0; transform: translateY(20px); }
    to   { opacity:1; transform: translateY(0); }
  }
  .btn-primary {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 0.85rem 2rem;
    background: var(--accent);
    color: #0a0a0a;
    font-family: 'Outfit', sans-serif;
    font-size: 0.82rem;
    font-weight: 600;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    text-decoration: none;
    border: none;
    cursor: none;
    transition: background 0.2s, transform 0.2s;
  }
  .btn-primary:hover { background: var(--accent2); transform: translateY(-2px); }
  .btn-outline {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 0.85rem 2rem;
    border: 1px solid var(--border2);
    color: var(--text2);
    font-family: 'Outfit', sans-serif;
    font-size: 0.82rem;
    font-weight: 500;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    text-decoration: none;
    cursor: none;
    transition: border-color 0.2s, color 0.2s, transform 0.2s;
  }
  .btn-outline:hover { border-color: var(--accent); color: var(--accent); transform: translateY(-2px); }
  .hero-scroll {
    position: absolute;
    bottom: 2rem;
    right: 3rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 8px;
    color: var(--text3);
    font-size: 0.7rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    opacity: 0;
    animation: fadeUp 1s 1.2s forwards;
  }
  .scroll-line {
    width: 1px; height: 48px;
    background: linear-gradient(to bottom, var(--text3), transparent);
    animation: scrollAnim 2s 1.5s infinite;
  }
  @keyframes scrollAnim { 0%,100%{opacity:1} 50%{opacity:0.3} }

  /* Sections */
  section {
    padding: 6rem 3rem;
    border-top: 1px solid var(--border);
  }
  .section-header {
    display: flex;
    align-items: center;
    gap: 1rem;
    margin-bottom: 3.5rem;
  }
  .section-num {
    font-size: 0.7rem;
    color: var(--accent);
    letter-spacing: 0.15em;
    font-family: 'Outfit', sans-serif;
  }
  .section-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(1.8rem, 3vw, 2.5rem);
    font-weight: 400;
    letter-spacing: -0.01em;
  }
  .section-line {
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  /* About */
  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 4rem;
    align-items: start;
  }
  .about-text {
    font-size: 1.1rem;
    color: var(--text2);
    line-height: 1.9;
  }
  .about-text strong { color: var(--accent); font-weight: 500; }
  .about-stats {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
  }
  .stat-box {
    background: var(--surface);
    padding: 1.75rem;
    transition: background 0.2s;
  }
  .stat-box:hover { background: var(--surface2); }
  .stat-num {
    font-family: 'Playfair Display', serif;
    font-size: 2.5rem;
    font-weight: 700;
    color: var(--accent);
    line-height: 1;
    margin-bottom: 0.4rem;
  }
  .stat-label { font-size: 0.78rem; color: var(--text3); letter-spacing: 0.06em; text-transform: uppercase; }

  /* Skills */
  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
    margin-bottom: 3rem;
  }
  .skill-item {
    background: var(--surface);
    padding: 2rem;
    position: relative;
    overflow: hidden;
    transition: background 0.3s;
  }
  .skill-item:hover { background: var(--surface2); }
  .skill-item::after {
    content: '';
    position: absolute;
    bottom: 0; left: 0;
    width: 0; height: 2px;
    background: var(--accent);
    transition: width 0.4s ease;
  }
  .skill-item:hover::after { width: 100%; }
  .skill-icon {
    width: 40px; height: 40px;
    border: 1px solid var(--border2);
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 1rem;
    font-size: 1.1rem;
  }
  .skill-name {
    font-size: 0.95rem;
    font-weight: 500;
    color: var(--text);
    margin-bottom: 0.5rem;
  }
  .skill-desc { font-size: 0.82rem; color: var(--text3); line-height: 1.6; }
  .tools-row {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
  }
  .tool-tag {
    font-size: 0.75rem;
    padding: 6px 14px;
    border: 1px solid var(--border2);
    color: var(--text2);
    letter-spacing: 0.05em;
    transition: border-color 0.2s, color 0.2s;
  }
  .tool-tag:hover { border-color: var(--accent); color: var(--accent); }

  /* Experience */
  .exp-list { display: flex; flex-direction: column; gap: 0; }
  .exp-item {
    display: grid;
    grid-template-columns: 200px 1fr;
    gap: 3rem;
    padding: 2.5rem 0;
    border-bottom: 1px solid var(--border);
  }
  .exp-item:first-child { border-top: 1px solid var(--border); }
  .exp-meta-col { padding-top: 4px; }
  .exp-period {
    font-size: 0.75rem;
    letter-spacing: 0.08em;
    color: var(--accent);
    text-transform: uppercase;
    margin-bottom: 0.4rem;
  }
  .exp-location { font-size: 0.8rem; color: var(--text3); }
  .exp-company { font-size: 1.2rem; font-weight: 500; margin-bottom: 0.25rem; color: var(--text); }
  .exp-role-label {
    display: inline-block;
    font-size: 0.72rem;
    padding: 3px 10px;
    border: 1px solid var(--border2);
    color: var(--text3);
    letter-spacing: 0.06em;
    text-transform: uppercase;
    margin-bottom: 1rem;
  }
  .exp-bullets { list-style: none; }
  .exp-bullets li {
    font-size: 0.9rem;
    color: var(--text2);
    padding: 0.35rem 0;
    padding-left: 1.2rem;
    position: relative;
    border-left: 1px solid var(--border);
    margin-left: 0;
    padding-left: 1rem;
  }
  .exp-bullets li::before {
    content: '→';
    position: absolute;
    left: -0.75rem;
    color: var(--accent);
    font-size: 0.8rem;
    background: var(--bg);
    padding: 2px 0;
  }

  /* Education */
  .edu-card {
    border: 1px solid var(--border);
    padding: 2.5rem;
    display: grid;
    grid-template-columns: 1fr auto;
    gap: 2rem;
    align-items: center;
    background: var(--surface);
    position: relative;
    overflow: hidden;
  }
  .edu-card::before {
    content: '';
    position: absolute;
    left: 0; top: 0; bottom: 0;
    width: 3px;
    background: var(--accent);
  }
  .edu-uni { font-family: 'Playfair Display', serif; font-size: 1.5rem; font-weight: 400; margin-bottom: 0.5rem; }
  .edu-degree { font-size: 0.9rem; color: var(--text2); margin-bottom: 1rem; }
  .edu-year {
    text-align: right;
    font-family: 'Playfair Display', serif;
    font-size: 2rem;
    font-weight: 700;
    color: rgba(200,169,110,0.15);
    line-height: 1;
  }

  /* Certifications */
  .certs-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 1rem;
  }
  .cert-card {
    border: 1px solid var(--border);
    padding: 1.5rem;
    background: var(--surface);
    transition: border-color 0.2s, background 0.2s;
    position: relative;
  }
  .cert-card:hover { border-color: var(--accent); background: var(--accent-dim2); }
  .cert-icon { font-size: 1.4rem; margin-bottom: 0.75rem; }
  .cert-name { font-size: 0.9rem; font-weight: 500; color: var(--text); margin-bottom: 0.25rem; }
  .cert-year { font-size: 0.75rem; color: var(--text3); letter-spacing: 0.08em; }

  /* Volunteering */
  .vol-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
  }
  .vol-item {
    background: var(--surface);
    padding: 2rem;
    transition: background 0.2s;
  }
  .vol-item:hover { background: var(--surface2); }
  .vol-org { font-size: 0.7rem; letter-spacing: 0.1em; text-transform: uppercase; color: var(--accent); margin-bottom: 0.5rem; }
  .vol-title { font-size: 1rem; font-weight: 500; color: var(--text); margin-bottom: 0.5rem; }
  .vol-desc { font-size: 0.82rem; color: var(--text3); line-height: 1.6; }
  .vol-year {
    display: inline-block;
    margin-top: 0.75rem;
    font-size: 0.7rem;
    padding: 3px 8px;
    border: 1px solid var(--border2);
    color: var(--text3);
  }

  /* Languages */
  .lang-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1rem;
  }
  .lang-card {
    border: 1px solid var(--border);
    padding: 2rem;
    background: var(--surface);
    position: relative;
    overflow: hidden;
  }
  .lang-name { font-family: 'Playfair Display', serif; font-size: 1.8rem; font-weight: 400; color: var(--text); margin-bottom: 0.4rem; }
  .lang-level { font-size: 0.75rem; letter-spacing: 0.12em; text-transform: uppercase; color: var(--accent); }
  .lang-bg {
    position: absolute;
    right: -10px; bottom: -20px;
    font-family: 'Playfair Display', serif;
    font-size: 5rem;
    font-weight: 700;
    color: rgba(200,169,110,0.04);
    line-height: 1;
    pointer-events: none;
  }

  /* References */
  .refs-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
  }
  .ref-card {
    background: var(--surface);
    padding: 2rem;
    transition: background 0.2s;
  }
  .ref-card:hover { background: var(--surface2); }
  .ref-initials {
    width: 44px; height: 44px;
    background: var(--accent-dim);
    border: 1px solid rgba(200,169,110,0.2);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 0.8rem;
    font-weight: 600;
    color: var(--accent);
    letter-spacing: 0.05em;
    margin-bottom: 1rem;
  }
  .ref-name { font-size: 1rem; font-weight: 500; color: var(--text); margin-bottom: 0.25rem; }
  .ref-role { font-size: 0.8rem; color: var(--text3); margin-bottom: 0.75rem; line-height: 1.5; }
  .ref-contact { font-size: 0.78rem; color: var(--text2); line-height: 1.8; }
  .ref-contact a { color: var(--accent); text-decoration: none; }
  .ref-contact a:hover { text-decoration: underline; }

  /* Contact / Footer */
  footer {
    padding: 5rem 3rem;
    border-top: 1px solid var(--border);
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 4rem;
    align-items: end;
  }
  .footer-big {
    font-family: 'Playfair Display', serif;
    font-size: clamp(2rem, 4vw, 3.5rem);
    font-weight: 400;
    line-height: 1.1;
    letter-spacing: -0.02em;
  }
  .footer-big em { font-style: italic; color: var(--accent); }
  .footer-contact { display: flex; flex-direction: column; gap: 1rem; align-items: flex-end; }
  .contact-row {
    display: flex;
    align-items: center;
    gap: 10px;
    font-size: 0.85rem;
    color: var(--text2);
    text-decoration: none;
    transition: color 0.2s;
  }
  .contact-row:hover { color: var(--accent); }
  .contact-row .icon { font-size: 1rem; }
  .footer-bottom {
    padding: 1.5rem 3rem;
    border-top: 1px solid var(--border);
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .footer-copy { font-size: 0.75rem; color: var(--text3); letter-spacing: 0.05em; }
  .footer-sig {
    font-family: 'Playfair Display', serif;
    font-size: 1rem;
    font-style: italic;
    color: var(--text3);
  }

  /* Scroll reveal */
  .reveal {
    opacity: 0;
    transform: translateY(24px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  .reveal.visible { opacity: 1; transform: translateY(0); }

  /* Responsive */
  @media (max-width: 768px) {
    nav { padding: 1rem 1.5rem; }
    .nav-links { display: none; }
    .hero { padding: 0 1.5rem 3rem; }
    section { padding: 4rem 1.5rem; }
    .about-grid { grid-template-columns: 1fr; gap: 2.5rem; }
    .exp-item { grid-template-columns: 1fr; gap: 0.5rem; }
    footer { grid-template-columns: 1fr; gap: 2rem; }
    .footer-contact { align-items: flex-start; }
    .footer-bottom { flex-direction: column; gap: 0.5rem; text-align: center; }
    body { cursor: auto; }
    .cursor, .cursor-ring { display: none; }
  }
</style>
</head>
<body>

<!-- Custom cursor -->
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- Nav -->
<nav>
  <a href="#" class="nav-logo">K<span>.</span>Franchise</a>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#skills">Skills</a></li>
    <li><a href="#experience">Experience</a></li>
    <li><a href="#education">Education</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
  <span class="nav-badge">Available for work</span>
</nav>

<!-- Hero -->
<section class="hero" id="home">
  <div class="hero-bg-text">KF</div>
  <div class="hero-line"></div>
  <p class="hero-tag">UI/UX Designer · Kigali, Rwanda</p>
  <h1 class="hero-title">
    Designing digital<br>
    experiences that <em>matter</em>
  </h1>
  <p class="hero-desc">
    I'm Kimana Franchise — a dedicated UI/UX designer who transforms complex user needs into intuitive, engaging interfaces. Based in Kigali, building for the world.
  </p>
  <div class="hero-actions">
    <a href="#experience" class="btn-primary">View my work →</a>
    <a href="#contact" class="btn-outline">Get in touch</a>
  </div>
  <div class="hero-scroll">
    <span>Scroll</span>
    <div class="scroll-line"></div>
  </div>
</section>

<!-- About -->
<section id="about">
  <div class="section-header reveal">
    <span class="section-num">01</span>
    <h2 class="section-title">About me</h2>
    <div class="section-line"></div>
  </div>
  <div class="about-grid" style="grid-template-columns: 280px 1fr 1fr; gap: 3rem; align-items: start;">
    <div class="reveal" style="position:relative;">
      <div style="aspect-ratio:3/4; overflow:hidden; border:1px solid var(--border2); position:relative;">
        <img src="data:image/png;base64,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" alt="Kimana Franchise">
        <div style="position:absolute;bottom:0;left:0;right:0;height:60px;background:linear-gradient(to top, rgba(10,10,10,0.5), transparent);"></div>
      </div>
      <p style="margin-top:0.75rem; font-size:0.72rem; letter-spacing:0.12em; text-transform:uppercase; color:var(--accent);">Kimana Franchise</p>
    </div>
    <div class="reveal">
      <p class="about-text">
        Dedicated UI/UX Designer with a proven ability to translate complex user needs into <strong>intuitive and engaging digital experiences</strong>. Possesses a strong foundation in user-centered design methodologies and human-centered thinking.
        <br><br>
        Eager to leverage collaborative skills and a keen eye for usability to drive impactful design solutions and enhance user satisfaction. Currently completing a <strong>Bachelor of Business Information Technology</strong> at the University of Kigali.
      </p>
    </div>
    <div class="about-stats reveal">
      <div class="stat-box">
        <div class="stat-num">3+</div>
        <div class="stat-label">Years of design study</div>
      </div>
      <div class="stat-box">
        <div class="stat-num">2</div>
        <div class="stat-label">Languages spoken</div>
      </div>
      <div class="stat-box">
        <div class="stat-num">4+</div>
        <div class="stat-label">Years of volunteering</div>
      </div>
      <div class="stat-box">
        <div class="stat-num">∞</div>
        <div class="stat-label">Passion for design</div>
      </div>
    </div>
  </div>
</section>

<!-- Skills -->
<section id="skills">
  <div class="section-header reveal">
    <span class="section-num">02</span>
    <h2 class="section-title">Skills &amp; Tools</h2>
    <div class="section-line"></div>
  </div>
  <div class="skills-grid reveal">
    <div class="skill-item">
      <div class="skill-icon">✦</div>
      <div class="skill-name">UI/UX Design</div>
      <div class="skill-desc">Mobile app and website design with a user-centered approach from wireframe to final handoff.</div>
    </div>
    <div class="skill-item">
      <div class="skill-icon">◈</div>
      <div class="skill-name">Design Systems</div>
      <div class="skill-desc">Building and contributing to scalable system design within collaborative team environments.</div>
    </div>
    <div class="skill-item">
      <div class="skill-icon">◎</div>
      <div class="skill-name">Usability &amp; Heuristics</div>
      <div class="skill-desc">Applying usability heuristics to identify and resolve design flaws before they reach users.</div>
    </div>
    <div class="skill-item">
      <div class="skill-icon">⬡</div>
      <div class="skill-name">Cross-functional Work</div>
      <div class="skill-desc">Collaborating effectively with product managers, developers, and stakeholders.</div>
    </div>
  </div>
  <div style="margin-top:2rem" class="reveal">
    <p style="font-size:0.75rem;letter-spacing:0.12em;text-transform:uppercase;color:var(--text3);margin-bottom:1rem;">Design tools</p>
    <div class="tools-row">
      <span class="tool-tag">Figma</span>
      <span class="tool-tag">Adobe XD</span>
      <span class="tool-tag">Sketch</span>
      <span class="tool-tag">Prototyping</span>
      <span class="tool-tag">Wireframing</span>
      <span class="tool-tag">User Research</span>
      <span class="tool-tag">Design Systems</span>
      <span class="tool-tag">HTML/CSS</span>
    </div>
  </div>
</section>

<!-- Experience -->
<section id="experience">
  <div class="section-header reveal">
    <span class="section-num">03</span>
    <h2 class="section-title">Experience</h2>
    <div class="section-line"></div>
  </div>
  <div class="exp-list reveal">
    <div class="exp-item">
      <div class="exp-meta-col">
        <div class="exp-period">Mar – Jun 2026</div>
        <div class="exp-location">Kigali, Kicukiro</div>
      </div>
      <div>
        <div class="exp-company">Solvit Africa</div>
        <span class="exp-role-label">UI/UX Design Intern</span>
        <ul class="exp-bullets">
          <li>Collaborated on mobile app and website UI/UX design across multiple product lines</li>
          <li>Contributed to system design and component library maintenance within a cross-functional team</li>
          <li>Delivered user-centered design solutions across web and mobile platforms</li>
        </ul>
      </div>
    </div>
    <div class="exp-item">
      <div class="exp-meta-col">
        <div class="exp-period">2017 – 2020</div>
        <div class="exp-location">Kigali, Rwanda</div>
      </div>
      <div>
        <div class="exp-company">Volunteer &amp; Community</div>
        <span class="exp-role-label">Leadership &amp; Service</span>
        <ul class="exp-bullets">
          <li>Team Leader at Maison Shalom — supported sponsored secondary school students</li>
          <li>Humanitarian worker at Save the Children Rwanda (2018)</li>
          <li>EDUFAM volunteer — helped young girls return to vocational skills training (2020)</li>
          <li>Founder of a small business providing Irembo, tax, and driving license services</li>
        </ul>
      </div>
    </div>
  </div>
</section>

<!-- Education -->
<section id="education">
  <div class="section-header reveal">
    <span class="section-num">04</span>
    <h2 class="section-title">Education</h2>
    <div class="section-line"></div>
  </div>
  <div class="edu-card reveal">
    <div>
      <div class="edu-uni">University of Kigali</div>
      <div class="edu-degree">Bachelor of Business Information Technology</div>
      <div class="tools-row" style="margin-top:1rem">
        <span class="tool-tag">Kigali, Gasabo</span>
        <span class="tool-tag">2021 – 2026</span>
      </div>
    </div>
    <div class="edu-year">2026</div>
  </div>
  <div style="margin-top:2.5rem" class="reveal">
    <p style="font-size:0.75rem;letter-spacing:0.12em;text-transform:uppercase;color:var(--text3);margin-bottom:1.5rem;">Certifications &amp; Courses</p>
    <div class="certs-grid">
      <div class="cert-card">
        <div class="cert-icon">🎓</div>
        <div class="cert-name">UI/UX Design Course</div>
        <div class="cert-year">Solvit Africa · 2026</div>
      </div>
      <div class="cert-card">
        <div class="cert-icon">💼</div>
        <div class="cert-name">Business Club</div>
        <div class="cert-year">2019</div>
      </div>
      <div class="cert-card">
        <div class="cert-icon">🌍</div>
        <div class="cert-name">Humanitarian Project</div>
        <div class="cert-year">2018</div>
      </div>
    </div>
  </div>
</section>

<!-- Languages -->
<section>
  <div class="section-header reveal">
    <span class="section-num">05</span>
    <h2 class="section-title">Languages</h2>
    <div class="section-line"></div>
  </div>
  <div class="lang-grid reveal">
    <div class="lang-card">
      <div class="lang-name">English</div>
      <div class="lang-level">Advanced</div>
      <div class="lang-bg">EN</div>
    </div>
    <div class="lang-card">
      <div class="lang-name">French</div>
      <div class="lang-level">Fluent</div>
      <div class="lang-bg">FR</div>
    </div>
  </div>
</section>

<!-- References -->
<section>
  <div class="section-header reveal">
    <span class="section-num">06</span>
    <h2 class="section-title">References</h2>
    <div class="section-line"></div>
  </div>
  <div class="refs-grid reveal">
    <div class="ref-card">
      <div class="ref-initials">ML</div>
      <div class="ref-name">Muhire Leonce</div>
      <div class="ref-role">IT Lecturer<br>University of Kigali</div>
      <div class="ref-contact">
        <a href="mailto:bmldone@gmail.com">bmldone@gmail.com</a><br>
        +250 781 604 151
      </div>
    </div>
    <div class="ref-card">
      <div class="ref-initials">KD</div>
      <div class="ref-name">Kubwimana Donate</div>
      <div class="ref-role">Assistant Registrar<br>University of Kigali</div>
      <div class="ref-contact">
        <a href="mailto:dkubwimana@uok.ac.rw">dkubwimana@uok.ac.rw</a><br>
        +250 787 876 022
      </div>
    </div>
    <div class="ref-card">
      <div class="ref-initials">MS</div>
      <div class="ref-name">Manirambona Sylvestre</div>
      <div class="ref-role">Chief Unit Maintenance IREI<br>Rwanda Air Company</div>
      <div class="ref-contact">
        <a href="mailto:manirambonasyl@asecna.org">manirambonasyl@asecna.org</a><br>
        +250 788 401 026
      </div>
    </div>
  </div>
</section>

<!-- Contact / Footer -->
<footer id="contact">
  <div>
    <p style="font-size:0.72rem;letter-spacing:0.15em;text-transform:uppercase;color:var(--accent);margin-bottom:1rem;">Let's work together</p>
    <div class="footer-big">
      Got a project?<br>
      Let's <em>talk.</em>
    </div>
  </div>
  <div class="footer-contact">
    <a href="mailto:kimanafranchise@gmail.com" class="contact-row">
      <span class="icon">✉</span>
      kimanafranchise@gmail.com
    </a>
    <a href="tel:+250780843959" class="contact-row">
      <span class="icon">☏</span>
      +250 780 843 959
    </a>
    <a href="#" class="contact-row">
      <span class="icon">◎</span>
      Kigali City, Rwanda
    </a>
    <a href="#home" class="btn-primary" style="margin-top:1rem">Back to top ↑</a>
  </div>
</footer>
<div class="footer-bottom">
  <span class="footer-copy">© 2026 Kimana Franchise. All rights reserved.</span>
  <span class="footer-sig">Kimana Franchise</span>
</div>

<script>
  // Cursor
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursorRing');
  let mx = 0, my = 0, rx = 0, ry = 0;
  document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; });
  function animCursor() {
    cursor.style.left = mx + 'px';
    cursor.style.top = my + 'px';
    rx += (mx - rx) * 0.12;
    ry += (my - ry) * 0.12;
    ring.style.left = rx + 'px';
    ring.style.top = ry + 'px';
    requestAnimationFrame(animCursor);
  }
  animCursor();

  // Scroll reveal
  const reveals = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver(entries => {
    entries.forEach(e => {
      if (e.isIntersecting) { e.target.classList.add('visible'); observer.unobserve(e.target); }
    });
  }, { threshold: 0.1 });
  reveals.forEach(el => observer.observe(el));
</script>
</body>
</html>

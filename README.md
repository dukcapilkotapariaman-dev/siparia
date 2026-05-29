<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SIPENDUK — Sistem Informasi Kependudukan Kota Pariaman</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700;900&family=DM+Sans:wght@300;400;500;600&family=DM+Mono&display=swap" rel="stylesheet">
<style>
  :root {
    --teal:    #0a7c6e;
    --teal2:   #12a08f;
    --gold:    #d4a843;
    --gold2:   #f0c96b;
    --cream:   #f7f3ec;
    --dark:    #0f1f1d;
    --dark2:   #162926;
    --muted:   #4a6b67;
    --border:  rgba(10,124,110,0.18);
    --shadow:  0 8px 40px rgba(10,124,110,0.13);
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--dark);
    color: var(--cream);
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* ── NOISE TEXTURE ── */
  body::before {
    content: '';
    position: fixed; inset: 0; pointer-events: none; z-index: 0;
    opacity: 0.03;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
  }

  /* ── HEADER ── */
  header {
    position: sticky; top: 0; z-index: 100;
    background: rgba(15,31,29,0.92);
    backdrop-filter: blur(16px);
    border-bottom: 1px solid var(--border);
    padding: 0 2rem;
    display: flex; align-items: center; justify-content: space-between;
    height: 64px;
  }

  .logo {
    display: flex; align-items: center; gap: 12px;
  }
  .logo-badge {
    width: 36px; height: 36px;
    background: linear-gradient(135deg, var(--teal), var(--gold));
    border-radius: 8px;
    display: flex; align-items: center; justify-content: center;
    font-size: 18px;
  }
  .logo-text { line-height: 1.1; }
  .logo-text strong {
    font-family: 'Playfair Display', serif;
    font-size: 1.05rem; letter-spacing: 0.02em;
    color: var(--gold2);
  }
  .logo-text span { font-size: 0.68rem; color: var(--muted); display: block; }

  nav { display: flex; gap: 1.5rem; }
  nav a {
    font-size: 0.8rem; font-weight: 500; letter-spacing: 0.05em;
    text-transform: uppercase; color: var(--muted); text-decoration: none;
    transition: color .2s;
  }
  nav a:hover { color: var(--gold2); }

  .year-badge {
    font-family: 'DM Mono'; font-size: 0.75rem;
    background: var(--border);
    border: 1px solid var(--border);
    padding: 4px 10px; border-radius: 20px; color: var(--teal2);
  }

  /* ── HERO ── */
  .hero {
    padding: 5rem 2rem 3rem;
    max-width: 1200px; margin: 0 auto;
    display: grid; grid-template-columns: 1fr 1fr; gap: 3rem; align-items: center;
  }
  .hero-label {
    font-family: 'DM Mono'; font-size: 0.7rem; letter-spacing: 0.15em;
    text-transform: uppercase; color: var(--teal2); margin-bottom: 1rem;
    display: flex; align-items: center; gap: 8px;
  }
  .hero-label::before {
    content: ''; display: block; width: 24px; height: 1px; background: var(--teal2);
  }
  .hero h1 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(2.2rem, 4vw, 3.5rem);
    line-height: 1.08; font-weight: 900;
    color: var(--cream);
    margin-bottom: 1.2rem;
  }
  .hero h1 em { color: var(--gold); font-style: normal; }
  .hero p { color: var(--muted); line-height: 1.7; font-size: 0.95rem; max-width: 420px; }

  .hero-stats {
    display: grid; grid-template-columns: 1fr 1fr; gap: 1rem;
  }
  .stat-card {
    background: var(--dark2);
    border: 1px solid var(--border);
    border-radius: 16px; padding: 1.4rem 1.2rem;
    position: relative; overflow: hidden;
    transition: transform .25s, border-color .25s;
    cursor: default;
  }
  .stat-card::before {
    content: ''; position: absolute; inset: 0;
    background: linear-gradient(135deg, rgba(10,124,110,0.08), transparent);
    opacity: 0; transition: opacity .3s;
  }
  .stat-card:hover { transform: translateY(-3px); border-color: var(--teal2); }
  .stat-card:hover::before { opacity: 1; }
  .stat-icon { font-size: 1.5rem; margin-bottom: 0.5rem; }
  .stat-num {
    font-family: 'Playfair Display', serif;
    font-size: 1.8rem; font-weight: 700; color: var(--gold2);
    line-height: 1;
  }
  .stat-label { font-size: 0.72rem; color: var(--muted); margin-top: 4px; }

  /* ── SECTION TITLE ── */
  .section-header {
    max-width: 1200px; margin: 0 auto;
    padding: 0 2rem 1.5rem;
    display: flex; align-items: flex-end; justify-content: space-between;
  }
  .section-title {
    font-family: 'Playfair Display', serif;
    font-size: 1.6rem; font-weight: 700; color: var(--cream);
  }
  .section-title span { color: var(--gold); }
  .section-sub { font-size: 0.78rem; color: var(--muted); margin-top: 4px; }
  .section-divider {
    max-width: 1200px; margin: 2.5rem auto 0;
    padding: 0 2rem;
    border-top: 1px solid var(--border);
  }

  /* ── MAP SECTION ── */
  .map-section {
    max-width: 1200px; margin: 0 auto 2rem;
    padding: 0 2rem;
    display: grid; grid-template-columns: 1fr 380px; gap: 2rem;
  }

  .map-container {
    background: var(--dark2);
    border: 1px solid var(--border);
    border-radius: 20px; padding: 1.5rem;
    position: relative;
  }
  .map-container h3 {
    font-size: 0.72rem; font-family: 'DM Mono';
    letter-spacing: 0.1em; text-transform: uppercase;
    color: var(--teal2); margin-bottom: 1rem;
    display: flex; align-items: center; gap: 8px;
  }
  .map-container h3::after {
    content: ''; flex: 1; height: 1px; background: var(--border);
  }

  /* ── SVG MAP ── */
  #pariaman-map {
    width: 100%; height: auto;
    display: block;
  }

  .kecamatan {
    fill: var(--teal);
    stroke: var(--dark);
    stroke-width: 2;
    cursor: pointer;
    transition: fill .25s, filter .25s;
    filter: drop-shadow(0 2px 6px rgba(0,0,0,0.3));
  }
  .kecamatan:hover {
    fill: var(--gold);
    filter: drop-shadow(0 4px 16px rgba(212,168,67,0.5));
  }
  .kecamatan.active {
    fill: var(--gold2);
    filter: drop-shadow(0 4px 20px rgba(240,201,107,0.6));
  }
  .kec-label {
    font-family: 'DM Sans', sans-serif;
    font-size: 11px; font-weight: 600;
    fill: white;
    text-anchor: middle;
    pointer-events: none;
    text-shadow: 0 1px 3px rgba(0,0,0,0.8);
  }
  .kec-sublabel {
    font-family: 'DM Mono';
    font-size: 9px;
    fill: rgba(255,255,255,0.7);
    text-anchor: middle;
    pointer-events: none;
  }

  /* MAP TOOLTIP */
  .map-tooltip {
    position: absolute;
    background: var(--dark);
    border: 1px solid var(--gold);
    border-radius: 10px; padding: 10px 14px;
    font-size: 0.78rem; pointer-events: none;
    opacity: 0; transition: opacity .2s;
    z-index: 10; white-space: nowrap;
    box-shadow: 0 8px 24px rgba(0,0,0,0.5);
  }
  .map-tooltip.show { opacity: 1; }
  .map-tooltip strong { color: var(--gold2); font-size: 0.85rem; display: block; }
  .map-tooltip span { color: var(--muted); }

  /* MAP LEGEND */
  .map-legend {
    margin-top: 1rem;
    display: flex; gap: 1.2rem; flex-wrap: wrap;
    font-size: 0.7rem; color: var(--muted);
  }
  .legend-item { display: flex; align-items: center; gap: 6px; }
  .legend-dot {
    width: 12px; height: 12px; border-radius: 3px;
    flex-shrink: 0;
  }

  /* ── DETAIL PANEL ── */
  .detail-panel {
    background: var(--dark2);
    border: 1px solid var(--border);
    border-radius: 20px; padding: 1.5rem;
    display: flex; flex-direction: column; gap: 1rem;
  }
  .panel-header {
    border-bottom: 1px solid var(--border);
    padding-bottom: 1rem;
  }
  .panel-header h3 {
    font-family: 'Playfair Display', serif;
    font-size: 1.2rem; color: var(--gold2);
  }
  .panel-header p { font-size: 0.75rem; color: var(--muted); margin-top: 4px; }
  .panel-hint {
    color: var(--muted); font-size: 0.8rem;
    text-align: center; padding: 2rem 0;
    line-height: 1.6;
  }
  .panel-hint .icon { font-size: 2rem; margin-bottom: 0.5rem; display: block; }

  .kec-detail { display: none; flex-direction: column; gap: 0.8rem; }
  .kec-detail.show { display: flex; }

  .kec-name-big {
    font-family: 'Playfair Display', serif;
    font-size: 1.5rem; font-weight: 700; color: var(--cream);
    line-height: 1.1;
  }
  .kec-name-big small { font-size: 0.75rem; color: var(--teal2); font-family: 'DM Mono'; display: block; }

  .metric-row {
    display: grid; grid-template-columns: 1fr 1fr; gap: 0.6rem;
  }
  .metric-box {
    background: var(--dark);
    border: 1px solid var(--border);
    border-radius: 12px; padding: 0.9rem;
    text-align: center;
  }
  .metric-box .val {
    font-family: 'Playfair Display', serif;
    font-size: 1.3rem; color: var(--gold2); font-weight: 700;
  }
  .metric-box .lbl { font-size: 0.65rem; color: var(--muted); margin-top: 3px; }

  .gender-bar { margin-top: 0.4rem; }
  .gender-bar-label {
    display: flex; justify-content: space-between;
    font-size: 0.7rem; color: var(--muted); margin-bottom: 4px;
  }
  .gender-bar-track {
    height: 8px; border-radius: 4px;
    background: var(--dark);
    overflow: hidden;
    display: flex;
  }
  .gender-bar-male {
    background: var(--teal2); height: 100%;
    transition: width .6s cubic-bezier(.4,0,.2,1);
  }
  .gender-bar-female {
    background: var(--gold); height: 100%;
    transition: width .6s cubic-bezier(.4,0,.2,1);
  }

  .kelurahan-list { margin-top: 0.4rem; }
  .kelurahan-list h4 { font-size: 0.7rem; color: var(--muted); text-transform: uppercase; letter-spacing: 0.08em; margin-bottom: 0.5rem; }
  .kel-item {
    display: flex; justify-content: space-between; align-items: center;
    padding: 6px 0; border-bottom: 1px solid rgba(255,255,255,0.05);
    font-size: 0.78rem;
  }
  .kel-item:last-child { border-bottom: none; }
  .kel-item span { color: var(--muted); font-family: 'DM Mono'; font-size: 0.72rem; }

  .density-badge {
    display: inline-flex; align-items: center; gap: 6px;
    background: rgba(10,124,110,0.15); border: 1px solid var(--teal);
    border-radius: 20px; padding: 4px 10px; font-size: 0.72rem; color: var(--teal2);
    margin-top: 0.2rem;
  }

  /* ── CHARTS SECTION ── */
  .charts-section {
    max-width: 1200px; margin: 0 auto 3rem;
    padding: 0 2rem;
    display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 1.5rem;
  }
  .chart-card {
    background: var(--dark2);
    border: 1px solid var(--border);
    border-radius: 20px; padding: 1.5rem;
  }
  .chart-card h3 {
    font-size: 0.8rem; color: var(--cream); font-weight: 600;
    margin-bottom: 0.3rem;
  }
  .chart-card p { font-size: 0.7rem; color: var(--muted); margin-bottom: 1.2rem; }

  /* BAR CHART */
  .bar-chart { display: flex; flex-direction: column; gap: 8px; }
  .bar-row { display: flex; align-items: center; gap: 8px; }
  .bar-kec { font-size: 0.68rem; color: var(--muted); width: 80px; flex-shrink: 0; }
  .bar-track {
    flex: 1; height: 22px; background: var(--dark);
    border-radius: 4px; overflow: hidden; position: relative;
  }
  .bar-fill {
    height: 100%;
    background: linear-gradient(90deg, var(--teal), var(--teal2));
    border-radius: 4px;
    transition: width 1s cubic-bezier(.4,0,.2,1);
    display: flex; align-items: center; justify-content: flex-end;
    padding-right: 6px;
    min-width: 30px;
  }
  .bar-fill span { font-size: 0.6rem; color: white; font-family: 'DM Mono'; }

  /* PIE CHART */
  .pie-wrap { display: flex; flex-direction: column; align-items: center; gap: 1rem; }
  .pie-svg { width: 160px; height: 160px; }
  .pie-legend { width: 100%; }
  .pie-legend-item { display: flex; align-items: center; gap: 8px; font-size: 0.7rem; margin-bottom: 5px; }
  .pie-dot { width: 10px; height: 10px; border-radius: 50%; flex-shrink: 0; }
  .pie-pct { margin-left: auto; font-family: 'DM Mono'; color: var(--gold2); }

  /* AGE PYRAMID  */
  .pyramid { display: flex; flex-direction: column; gap: 4px; }
  .pyr-row { display: flex; align-items: center; gap: 4px; }
  .pyr-label { font-size: 0.6rem; color: var(--muted); width: 42px; text-align: center; }
  .pyr-left { display: flex; justify-content: flex-end; flex: 1; }
  .pyr-right { flex: 1; }
  .pyr-bar {
    height: 14px; border-radius: 2px;
    transition: width .8s;
  }
  .pyr-bar.male { background: var(--teal2); }
  .pyr-bar.female { background: var(--gold); }
  .pyr-legend { display: flex; gap: 12px; font-size: 0.65rem; color: var(--muted); margin-bottom: 8px; justify-content: center; }
  .pyr-legend span { display: flex; align-items: center; gap: 5px; }
  .pyr-legend i { display: inline-block; width: 10px; height: 10px; border-radius: 2px; }

  /* ── TABLE ── */
  .table-section {
    max-width: 1200px; margin: 0 auto 4rem;
    padding: 0 2rem;
  }
  .table-card {
    background: var(--dark2);
    border: 1px solid var(--border);
    border-radius: 20px; overflow: hidden;
  }
  .table-toolbar {
    padding: 1.2rem 1.5rem;
    display: flex; align-items: center; gap: 1rem;
    border-bottom: 1px solid var(--border);
  }
  .table-toolbar h3 { font-size: 0.9rem; color: var(--cream); font-weight: 600; flex: 1; }
  .search-box {
    display: flex; align-items: center; gap: 8px;
    background: var(--dark); border: 1px solid var(--border);
    border-radius: 8px; padding: 6px 12px;
  }
  .search-box input {
    background: none; border: none; outline: none;
    font-family: 'DM Sans'; font-size: 0.78rem; color: var(--cream);
    width: 160px;
  }
  .search-box input::placeholder { color: var(--muted); }
  table { width: 100%; border-collapse: collapse; }
  thead { background: rgba(10,124,110,0.12); }
  th {
    font-size: 0.68rem; font-weight: 600; letter-spacing: 0.08em;
    text-transform: uppercase; color: var(--teal2);
    padding: 0.9rem 1.2rem; text-align: left;
    border-bottom: 1px solid var(--border);
    cursor: pointer; user-select: none;
  }
  th:hover { color: var(--gold2); }
  td {
    padding: 0.85rem 1.2rem; font-size: 0.82rem;
    border-bottom: 1px solid rgba(255,255,255,0.04);
    transition: background .15s;
  }
  tr:last-child td { border-bottom: none; }
  tr:hover td { background: rgba(10,124,110,0.06); }
  .td-num { font-family: 'DM Mono'; color: var(--gold2); }
  .td-rank {
    font-family: 'DM Mono'; font-size: 0.7rem;
    background: var(--border); color: var(--teal2);
    padding: 2px 7px; border-radius: 20px; display: inline-block;
  }

  /* ── FOOTER ── */
  footer {
    border-top: 1px solid var(--border);
    padding: 2rem; text-align: center;
    color: var(--muted); font-size: 0.75rem; line-height: 1.8;
  }
  footer strong { color: var(--teal2); }

  /* ── ANIMATIONS ── */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to   { opacity: 1; transform: translateY(0); }
  }
  .fade-up { animation: fadeUp .6s ease both; }
  .fade-up:nth-child(2) { animation-delay: .1s; }
  .fade-up:nth-child(3) { animation-delay: .2s; }
  .fade-up:nth-child(4) { animation-delay: .3s; }

  @keyframes pulse-ring {
    0%   { transform: scale(1);   opacity: .6; }
    100% { transform: scale(1.8); opacity: 0; }
  }
  .pulse {
    position: absolute;
    width: 10px; height: 10px; border-radius: 50%;
    background: var(--gold);
    animation: pulse-ring 1.5s infinite;
  }

  /* ── RESPONSIVE ── */
  @media (max-width: 900px) {
    .hero { grid-template-columns: 1fr; }
    .map-section { grid-template-columns: 1fr; }
    .charts-section { grid-template-columns: 1fr 1fr; }
    nav { display: none; }
  }
  @media (max-width: 600px) {
    .charts-section { grid-template-columns: 1fr; }
    .hero { padding: 3rem 1rem 2rem; }
    .hero-stats { grid-template-columns: 1fr 1fr; }
    .map-section, .section-header, .charts-section, .table-section { padding: 0 1rem; }
  }

  /* ── SCROLL REVEAL ── */
  .reveal { opacity: 0; transform: translateY(30px); transition: opacity .7s ease, transform .7s ease; }
  .reveal.visible { opacity: 1; transform: none; }
</style>
</head>
<body>

<!-- HEADER -->
<header>
  <div class="logo">
    <div class="logo-badge">🏛️</div>
    <div class="logo-text">
      <strong>SIPENDUK</strong>
      <span>Kota Pariaman · Sumatera Barat</span>
    </div>
  </div>
  <nav>
    <a href="#peta">Peta</a>
    <a href="#statistik">Statistik</a>
    <a href="#tabel">Tabel Data</a>
  </nav>
  <span class="year-badge">Data 2024</span>
</header>

<!-- HERO -->
<section class="hero fade-up">
  <div>
    <p class="hero-label">Sistem Informasi Kependudukan</p>
    <h1>Data Penduduk<br><em>Kota Pariaman</em></h1>
    <p>Portal resmi data kependudukan Kota Pariaman. Jelajahi informasi populasi, kepadatan, dan demografi per kecamatan secara interaktif dan real-time.</p>
  </div>
  <div class="hero-stats">
    <div class="stat-card fade-up">
      <div class="stat-icon">👥</div>
      <div class="stat-num" id="total-penduduk">0</div>
      <div class="stat-label">Total Penduduk</div>
    </div>
    <div class="stat-card fade-up">
      <div class="stat-icon">🏘️</div>
      <div class="stat-num">4</div>
      <div class="stat-label">Kecamatan</div>
    </div>
    <div class="stat-card fade-up">
      <div class="stat-icon">🗺️</div>
      <div class="stat-num">73,36</div>
      <div class="stat-label">Luas Wilayah (km²)</div>
    </div>
    <div class="stat-card fade-up">
      <div class="stat-icon">📈</div>
      <div class="stat-num" id="kepadatan-avg">0</div>
      <div class="stat-label">Kepadatan (jiwa/km²)</div>
    </div>
  </div>
</section>

<div class="section-divider reveal"></div>

<!-- MAP + DETAIL -->
<section id="peta" style="padding-top:2rem;">
  <div class="section-header reveal">
    <div>
      <div class="section-title">Peta Kecamatan <span>Interaktif</span></div>
      <div class="section-sub">Hover untuk pratinjau · Klik untuk detail lengkap</div>
    </div>
  </div>

  <div class="map-section reveal">
    <!-- MAP -->
    <div class="map-container">
      <h3>🗺️ Peta Wilayah Kota Pariaman</h3>
      <div style="position:relative;">
        <svg id="pariaman-map" viewBox="0 0 600 520" xmlns="http://www.w3.org/2000/svg">
          <defs>
            <linearGradient id="gTeal" x1="0%" y1="0%" x2="100%" y2="100%">
              <stop offset="0%" stop-color="#0a7c6e"/>
              <stop offset="100%" stop-color="#12a08f"/>
            </linearGradient>
            <linearGradient id="gGold" x1="0%" y1="0%" x2="100%" y2="100%">
              <stop offset="0%" stop-color="#d4a843"/>
              <stop offset="100%" stop-color="#f0c96b"/>
            </linearGradient>
            <filter id="shadow">
              <feDropShadow dx="0" dy="3" stdDeviation="6" flood-color="rgba(0,0,0,0.5)"/>
            </filter>
          </defs>

          <!-- OCEAN BACKGROUND -->
          <rect width="600" height="520" fill="#0c2535" rx="12"/>
          <!-- Ocean label -->
          <text x="60" y="270" fill="rgba(100,180,220,0.3)" font-size="11" font-family="DM Mono" transform="rotate(-90,60,270)">SAMUDERA HINDIA</text>

          <!-- GRID LINES -->
          <g stroke="rgba(100,180,220,0.08)" stroke-width="1">
            <line x1="0" y1="130" x2="600" y2="130"/>
            <line x1="0" y1="260" x2="600" y2="260"/>
            <line x1="0" y1="390" x2="600" y2="390"/>
            <line x1="150" y1="0" x2="150" y2="520"/>
            <line x1="300" y1="0" x2="300" y2="520"/>
            <line x1="450" y1="0" x2="450" y2="520"/>
          </g>

          <!-- ============================================================
               KECAMATAN POLYGONS
               (Disederhanakan, mencerminkan 4 kecamatan Kota Pariaman:
                Pariaman Utara, Pariaman Tengah, Pariaman Selatan, Pariaman Timur)
               ============================================================ -->

          <!-- PARIAMAN UTARA (barat laut, pinggir pantai) -->
          <path id="kec-utara"
            class="kecamatan"
            data-kec="utara"
            d="M 120,50
               L 340,50
               L 340,80
               L 380,90
               L 380,200
               L 340,210
               L 310,190
               L 270,200
               L 230,185
               L 185,210
               L 140,200
               L 120,170
               Z"
            filter="url(#shadow)"/>
          <text class="kec-label" x="250" y="128">Pariaman Utara</text>
          <text class="kec-sublabel" x="250" y="142">21.990 jiwa</text>

          <!-- PARIAMAN TENGAH (tengah, pesisir) -->
          <path id="kec-tengah"
            class="kecamatan"
            data-kec="tengah"
            d="M 120,170
               L 140,200
               L 185,210
               L 230,185
               L 270,200
               L 310,190
               L 340,210
               L 380,200
               L 400,230
               L 390,310
               L 350,320
               L 300,305
               L 260,320
               L 210,310
               L 165,320
               L 130,300
               L 105,260
               L 115,210
               Z"
            filter="url(#shadow)"/>
          <text class="kec-label" x="252" y="258">Pariaman Tengah</text>
          <text class="kec-sublabel" x="252" y="272">47.620 jiwa</text>

          <!-- PARIAMAN SELATAN (selatan, pesisir) -->
          <path id="kec-selatan"
            class="kecamatan"
            data-kec="selatan"
            d="M 105,260
               L 130,300
               L 165,320
               L 210,310
               L 260,320
               L 300,305
               L 350,320
               L 390,310
               L 405,350
               L 390,410
               L 340,430
               L 280,440
               L 220,430
               L 165,420
               L 120,395
               L 95,355
               L 98,305
               Z"
            filter="url(#shadow)"/>
          <text class="kec-label" x="248" y="376">Pariaman Selatan</text>
          <text class="kec-sublabel" x="248" y="390">18.540 jiwa</text>

          <!-- PARIAMAN TIMUR (timur, pedalaman/daratan) -->
          <path id="kec-timur"
            class="kecamatan"
            data-kec="timur"
            d="M 340,50
               L 520,50
               L 530,100
               L 520,170
               L 530,240
               L 520,310
               L 510,370
               L 490,420
               L 440,440
               L 390,410
               L 405,350
               L 390,310
               L 400,230
               L 380,200
               L 380,90
               Z"
            filter="url(#shadow)"/>
          <text class="kec-label" x="455" y="250">Pariaman</text>
          <text class="kec-label" x="455" y="265">Timur</text>
          <text class="kec-sublabel" x="455" y="280">15.180 jiwa</text>

          <!-- COAST LINE decoration -->
          <path d="M 100,50 L 120,50 L 120,170 L 105,260 L 95,355 L 98,430 L 120,480 L 100,480"
            fill="none" stroke="rgba(100,180,220,0.4)" stroke-width="2" stroke-dasharray="6,4"/>
          <text x="76" y="470" fill="rgba(100,180,220,0.4)" font-size="9" font-family="DM Mono">PANTAI</text>

          <!-- COMPASS ROSE -->
          <g transform="translate(545,85)">
            <circle r="22" fill="rgba(15,31,29,0.8)" stroke="rgba(10,124,110,0.4)" stroke-width="1"/>
            <text text-anchor="middle" y="-12" fill="#f0c96b" font-size="8" font-family="DM Mono">U</text>
            <text text-anchor="middle" y="17" fill="rgba(240,201,107,0.5)" font-size="7" font-family="DM Mono">S</text>
            <text text-anchor="end" x="-12" y="4" fill="rgba(240,201,107,0.5)" font-size="7" font-family="DM Mono">B</text>
            <text x="13" y="4" fill="rgba(240,201,107,0.5)" font-size="7" font-family="DM Mono">T</text>
            <line x1="0" y1="-16" x2="0" y2="16" stroke="#f0c96b" stroke-width="1"/>
            <line x1="-16" y1="0" x2="16" y2="0" stroke="rgba(240,201,107,0.4)" stroke-width="1"/>
            <polygon points="0,-10 -3,-2 3,-2" fill="#f0c96b"/>
          </g>

          <!-- SCALE BAR -->
          <g transform="translate(120,490)">
            <line x1="0" y1="0" x2="80" y2="0" stroke="rgba(255,255,255,0.3)" stroke-width="1.5"/>
            <line x1="0" y1="-4" x2="0" y2="4" stroke="rgba(255,255,255,0.3)" stroke-width="1.5"/>
            <line x1="80" y1="-4" x2="80" y2="4" stroke="rgba(255,255,255,0.3)" stroke-width="1.5"/>
            <text x="40" y="-7" text-anchor="middle" fill="rgba(255,255,255,0.4)" font-size="8" font-family="DM Mono">≈ 5 km</text>
          </g>

          <!-- City center dot -->
          <circle cx="252" cy="260" r="5" fill="#f0c96b" opacity="0.8"/>
          <circle cx="252" cy="260" r="12" fill="none" stroke="#f0c96b" stroke-width="1" opacity="0.4" stroke-dasharray="3,3"/>
          <text x="267" y="255" fill="#f0c96b" font-size="8" font-family="DM Mono">Pusat Kota</text>
        </svg>
        <div class="map-tooltip" id="map-tooltip">
          <strong id="tt-name">—</strong>
          <span id="tt-pop">—</span>
        </div>
      </div>
      <div class="map-legend">
        <div class="legend-item"><div class="legend-dot" style="background:var(--teal)"></div> Normal</div>
        <div class="legend-item"><div class="legend-dot" style="background:var(--gold)"></div> Hover</div>
        <div class="legend-item"><div class="legend-dot" style="background:var(--gold2)"></div> Dipilih</div>
        <div class="legend-item"><div class="legend-dot" style="background:rgba(100,180,220,0.4); border:1px dashed rgba(100,180,220,0.5)"></div> Garis Pantai</div>
      </div>
    </div>

    <!-- DETAIL PANEL -->
    <div class="detail-panel">
      <div class="panel-header">
        <h3>Detail Kecamatan</h3>
        <p>Klik kecamatan pada peta untuk informasi lengkap</p>
      </div>
      <div class="panel-hint" id="panel-hint">
        <span class="icon">🖱️</span>
        Pilih kecamatan pada peta untuk melihat data kependudukan secara detail.
      </div>
      <div class="kec-detail" id="kec-detail">
        <div class="kec-name-big" id="d-name">—<small id="d-sub"></small></div>
        <div class="density-badge" id="d-density">📍 — jiwa/km²</div>
        <div class="metric-row">
          <div class="metric-box"><div class="val" id="d-pop">0</div><div class="lbl">Total Penduduk</div></div>
          <div class="metric-box"><div class="val" id="d-luas">0</div><div class="lbl">Luas (km²)</div></div>
          <div class="metric-box"><div class="val" id="d-kel">0</div><div class="lbl">Kelurahan/Desa</div></div>
          <div class="metric-box"><div class="val" id="d-kk">0</div><div class="lbl">Kepala Keluarga</div></div>
        </div>
        <div class="gender-bar">
          <div class="gender-bar-label">
            <span>👨 Laki-laki: <strong id="d-male">—</strong></span>
            <span>👩 Perempuan: <strong id="d-female">—</strong></span>
          </div>
          <div class="gender-bar-track">
            <div class="gender-bar-male" id="d-bar-m" style="width:50%"></div>
            <div class="gender-bar-female" id="d-bar-f" style="width:50%"></div>
          </div>
        </div>
        <div class="kelurahan-list">
          <h4>Kelurahan / Desa</h4>
          <div id="d-kel-list"></div>
        </div>
      </div>
    </div>
  </div>
</section>

<div class="section-divider reveal"></div>

<!-- CHARTS -->
<section id="statistik" style="padding-top:2rem;">
  <div class="section-header reveal">
    <div>
      <div class="section-title">Statistik <span>Kependudukan</span></div>
      <div class="section-sub">Distribusi populasi, rasio gender, dan struktur usia</div>
    </div>
  </div>

  <div class="charts-section reveal">
    <!-- BAR CHART -->
    <div class="chart-card">
      <h3>Populasi per Kecamatan</h3>
      <p>Perbandingan jumlah penduduk</p>
      <div class="bar-chart" id="bar-chart"></div>
    </div>

    <!-- PIE CHART -->
    <div class="chart-card">
      <h3>Proporsi Wilayah</h3>
      <p>Persentase populasi per kecamatan</p>
      <div class="pie-wrap">
        <svg class="pie-svg" id="pie-svg" viewBox="0 0 160 160"></svg>
        <div class="pie-legend" id="pie-legend"></div>
      </div>
    </div>

    <!-- AGE PYRAMID -->
    <div class="chart-card">
      <h3>Piramida Usia</h3>
      <p>Distribusi usia kota Pariaman</p>
      <div class="pyr-legend">
        <span><i style="background:var(--teal2)"></i> Laki-laki</span>
        <span><i style="background:var(--gold)"></i> Perempuan</span>
      </div>
      <div class="pyramid" id="pyramid"></div>
    </div>
  </div>
</section>

<div class="section-divider reveal"></div>

<!-- TABLE -->
<section id="tabel" style="padding-top:2rem; padding-bottom:2rem;">
  <div class="section-header reveal">
    <div>
      <div class="section-title">Tabel <span>Data Lengkap</span></div>
      <div class="section-sub">Semua data kependudukan per kecamatan</div>
    </div>
  </div>
  <div class="table-section reveal">
    <div class="table-card">
      <div class="table-toolbar">
        <h3>Rekapitulasi Kependudukan 2024</h3>
        <div class="search-box">
          <span>🔍</span>
          <input type="text" placeholder="Cari kecamatan..." id="search-input">
        </div>
      </div>
      <table id="data-table">
        <thead>
          <tr>
            <th>No</th>
            <th onclick="sortTable('nama')">Kecamatan ↕</th>
            <th onclick="sortTable('penduduk')">Penduduk ↕</th>
            <th onclick="sortTable('laki')">Laki-laki ↕</th>
            <th onclick="sortTable('perempuan')">Perempuan ↕</th>
            <th onclick="sortTable('kk')">KK ↕</th>
            <th onclick="sortTable('luas')">Luas (km²) ↕</th>
            <th onclick="sortTable('kepadatan')">Kepadatan ↕</th>
          </tr>
        </thead>
        <tbody id="table-body"></tbody>
      </table>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <p><strong>SIPENDUK</strong> — Sistem Informasi Kependudukan Kota Pariaman</p>
  <p>Data bersumber dari Dinas Kependudukan dan Catatan Sipil Kota Pariaman · Pemutakhiran: 2024</p>
  <p style="margin-top:8px;font-size:0.68rem;">Dikembangkan untuk kepentingan informasi publik · Kota Pariaman, Sumatera Barat</p>
</footer>

<script>
// ═══════════════════════════════════════════════════════════
//  DATA
// ═══════════════════════════════════════════════════════════
const DATA = {
  utara: {
    nama: "Pariaman Utara",
    penduduk: 21990,
    laki: 10840,
    perempuan: 11150,
    kk: 6120,
    luas: 17.32,
    kepadatan: 1270,
    kelurahan: [
      {nama:"Pauh Barat", pop:3210},
      {nama:"Pauh Timur", pop:2980},
      {nama:"Manggung", pop:2760},
      {nama:"Cubadak Air Utara", pop:3450},
      {nama:"Jawi-Jawi I", pop:2890},
      {nama:"Jawi-Jawi II", pop:3100},
      {nama:"Toboh Palabah", pop:3600},
    ],
    warna: "#0e9b8a"
  },
  tengah: {
    nama: "Pariaman Tengah",
    penduduk: 47620,
    laki: 23140,
    perempuan: 24480,
    kk: 13850,
    luas: 23.45,
    kepadatan: 2030,
    kelurahan: [
      {nama:"Kampung Baru", pop:5800},
      {nama:"Lohong", pop:4920},
      {nama:"Cimparuh", pop:5300},
      {nama:"Pondok", pop:4600},
      {nama:"Pasir", pop:3900},
      {nama:"Belakang Olo", pop:5100},
      {nama:"Padusunan", pop:4700},
      {nama:"Balai Baru", pop:5200},
      {nama:"Cubadak Air", pop:4100},
      {nama:"Batang Tajongkek", pop:4000},
    ],
    warna: "#12a08f"
  },
  selatan: {
    nama: "Pariaman Selatan",
    penduduk: 18540,
    laki: 9040,
    perempuan: 9500,
    kk: 5120,
    luas: 18.90,
    kepadatan: 981,
    kelurahan: [
      {nama:"Naras I", pop:3200},
      {nama:"Naras II", pop:2900},
      {nama:"Naras Hilir", pop:2750},
      {nama:"Marunggi", pop:3100},
      {nama:"Sikapak Timur", pop:2890},
      {nama:"Sikapak Barat", pop:3700},
    ],
    warna: "#0a7c6e"
  },
  timur: {
    nama: "Pariaman Timur",
    penduduk: 15180,
    laki: 7540,
    perempuan: 7640,
    kk: 4310,
    luas: 13.69,
    kepadatan: 1109,
    kelurahan: [
      {nama:"Balai Naras", pop:2800},
      {nama:"Kampung Gadang", pop:2600},
      {nama:"Apar", pop:2400},
      {nama:"Sunur", pop:2980},
      {nama:"Toboh Gadang Timur", pop:2600},
      {nama:"Toboh Gadang Barat", pop:1800},
    ],
    warna: "#087066"
  }
};

const TOTAL = Object.values(DATA).reduce((s,d)=>s+d.penduduk,0);
const LUAS_TOTAL = Object.values(DATA).reduce((s,d)=>s+d.luas,0);

// Age pyramid data (approximate for Kota Pariaman)
const AGE_DATA = [
  {group:"0–4",   male:4.2, female:3.9},
  {group:"5–9",   male:4.8, female:4.5},
  {group:"10–14", male:5.1, female:4.8},
  {group:"15–19", male:5.4, female:5.2},
  {group:"20–24", male:5.0, female:5.3},
  {group:"25–29", male:4.6, female:4.9},
  {group:"30–34", male:4.2, female:4.5},
  {group:"35–39", male:3.9, female:4.1},
  {group:"40–44", male:3.4, female:3.5},
  {group:"45–49", male:3.0, female:3.2},
  {group:"50–54", male:2.5, female:2.7},
  {group:"55–59", male:2.0, female:2.2},
  {group:"60–64", male:1.5, female:1.7},
  {group:"65+",   male:1.8, female:2.4},
];

// ═══════════════════════════════════════════════════════════
//  INIT
// ═══════════════════════════════════════════════════════════
window.addEventListener('DOMContentLoaded', () => {
  animateNumber('total-penduduk', TOTAL);
  animateNumber('kepadatan-avg', Math.round(TOTAL/LUAS_TOTAL));
  initMap();
  initBarChart();
  initPieChart();
  initPyramid();
  initTable();
  initReveal();
});

function animateNumber(id, target) {
  const el = document.getElementById(id);
  let start = 0;
  const step = target / 60;
  const tick = () => {
    start = Math.min(start + step, target);
    el.textContent = Math.round(start).toLocaleString('id-ID');
    if (start < target) requestAnimationFrame(tick);
  };
  requestAnimationFrame(tick);
}

// ── MAP ──────────────────────────────────────────────────
let activeKec = null;
function initMap() {
  const tooltip = document.getElementById('map-tooltip');
  const mapEl   = document.getElementById('pariaman-map');

  document.querySelectorAll('.kecamatan').forEach(path => {
    const kec  = path.dataset.kec;
    const info = DATA[kec];

    path.addEventListener('mouseenter', e => {
      tooltip.querySelector('#tt-name').textContent = info.nama;
      tooltip.querySelector('#tt-pop').textContent  = `👥 ${info.penduduk.toLocaleString('id-ID')} jiwa`;
      tooltip.classList.add('show');
    });
    path.addEventListener('mousemove', e => {
      const rect = mapEl.parentElement.getBoundingClientRect();
      const x = e.clientX - rect.left + 12;
      const y = e.clientY - rect.top  - 10;
      tooltip.style.left = x + 'px';
      tooltip.style.top  = y + 'px';
    });
    path.addEventListener('mouseleave', () => tooltip.classList.remove('show'));

    path.addEventListener('click', () => {
      document.querySelectorAll('.kecamatan').forEach(p => p.classList.remove('active'));
      path.classList.add('active');
      activeKec = kec;
      showDetail(kec);
    });
  });
}

function showDetail(kec) {
  const d = DATA[kec];
  document.getElementById('panel-hint').style.display = 'none';
  const det = document.getElementById('kec-detail');
  det.classList.add('show');

  document.getElementById('d-name').childNodes[0].textContent = d.nama;
  document.getElementById('d-sub').textContent = `Kota Pariaman · Sumatera Barat`;
  document.getElementById('d-density').textContent = `📍 ${d.kepadatan.toLocaleString('id-ID')} jiwa/km²`;
  document.getElementById('d-pop').textContent  = d.penduduk.toLocaleString('id-ID');
  document.getElementById('d-luas').textContent = d.luas.toFixed(2);
  document.getElementById('d-kel').textContent  = d.kelurahan.length;
  document.getElementById('d-kk').textContent   = d.kk.toLocaleString('id-ID');
  document.getElementById('d-male').textContent   = d.laki.toLocaleString('id-ID');
  document.getElementById('d-female').textContent = d.perempuan.toLocaleString('id-ID');

  const mPct = (d.laki/d.penduduk*100).toFixed(1);
  const fPct = (d.perempuan/d.penduduk*100).toFixed(1);
  document.getElementById('d-bar-m').style.width = mPct + '%';
  document.getElementById('d-bar-f').style.width = fPct + '%';

  const list = document.getElementById('d-kel-list');
  list.innerHTML = d.kelurahan.map(k =>
    `<div class="kel-item">${k.nama}<span>${k.pop.toLocaleString('id-ID')} jiwa</span></div>`
  ).join('');
}

// ── BAR CHART ─────────────────────────────────────────────
function initBarChart() {
  const max = Math.max(...Object.values(DATA).map(d=>d.penduduk));
  const container = document.getElementById('bar-chart');
  Object.entries(DATA).forEach(([,d]) => {
    const pct = (d.penduduk/max*100).toFixed(1);
    container.innerHTML += `
      <div class="bar-row">
        <div class="bar-kec">${d.nama.replace('Pariaman ','')}</div>
        <div class="bar-track">
          <div class="bar-fill" style="width:0%" data-w="${pct}">
            <span>${(d.penduduk/1000).toFixed(1)}K</span>
          </div>
        </div>
      </div>`;
  });
  setTimeout(() => {
    container.querySelectorAll('.bar-fill').forEach(b => b.style.width = b.dataset.w + '%');
  }, 300);
}

// ── PIE CHART ─────────────────────────────────────────────
const PIE_COLORS = ['#0a7c6e','#12a08f','#d4a843','#f0c96b'];
function initPieChart() {
  const svg  = document.getElementById('pie-svg');
  const leg  = document.getElementById('pie-legend');
  const vals = Object.values(DATA).map(d=>d.penduduk);
  const sum  = vals.reduce((a,b)=>a+b,0);
  const cx=80, cy=80, r=68, ir=38;
  let startAngle = -Math.PI/2;

  Object.entries(DATA).forEach(([,d],i) => {
    const angle = (d.penduduk/sum)*2*Math.PI;
    const x1=cx+r*Math.cos(startAngle), y1=cy+r*Math.sin(startAngle);
    const x2=cx+r*Math.cos(startAngle+angle), y2=cy+r*Math.sin(startAngle+angle);
    const xi1=cx+ir*Math.cos(startAngle), yi1=cy+ir*Math.sin(startAngle);
    const xi2=cx+ir*Math.cos(startAngle+angle), yi2=cy+ir*Math.sin(startAngle+angle);
    const large = angle > Math.PI ? 1 : 0;

    const path = document.createElementNS('http://www.w3.org/2000/svg','path');
    const mid  = startAngle + angle/2;
    path.setAttribute('d',
      `M${xi1},${yi1} L${x1},${y1} A${r},${r} 0 ${large} 1 ${x2},${y2}
       L${xi2},${yi2} A${ir},${ir} 0 ${large} 0 ${xi1},${yi1} Z`);
    path.setAttribute('fill', PIE_COLORS[i]);
    path.setAttribute('stroke','#0f1f1d');
    path.setAttribute('stroke-width','2');
    path.style.cursor='pointer';
    path.style.transition='transform .25s';
    path.addEventListener('mouseenter',()=>{
      const mx=cx+8*Math.cos(mid), my=cy+8*Math.sin(mid);
      path.setAttribute('transform',`translate(${mx-cx},${my-cy})`);
    });
    path.addEventListener('mouseleave',()=>path.setAttribute('transform',''));
    svg.appendChild(path);

    // Legend
    const pct = (d.penduduk/sum*100).toFixed(1);
    leg.innerHTML += `
      <div class="pie-legend-item">
        <div class="pie-dot" style="background:${PIE_COLORS[i]}"></div>
        ${d.nama.replace('Pariaman ','')}
        <span class="pie-pct">${pct}%</span>
      </div>`;
    startAngle += angle;
  });

  // Center
  const circ = document.createElementNS('http://www.w3.org/2000/svg','circle');
  circ.setAttribute('cx',80); circ.setAttribute('cy',80);
  circ.setAttribute('r',30); circ.setAttribute('fill','#0f1f1d');
  svg.appendChild(circ);
  const txt = document.createElementNS('http://www.w3.org/2000/svg','text');
  txt.setAttribute('x',80); txt.setAttribute('y',84);
  txt.setAttribute('text-anchor','middle');
  txt.setAttribute('fill','#f0c96b');
  txt.setAttribute('font-size','9');
  txt.setAttribute('font-family','DM Mono');
  txt.textContent = '103K+';
  svg.appendChild(txt);
}

// ── PYRAMID ───────────────────────────────────────────────
function initPyramid() {
  const container = document.getElementById('pyramid');
  const maxVal = Math.max(...AGE_DATA.flatMap(d=>[d.male,d.female]));
  const W = 90;
  AGE_DATA.slice().reverse().forEach(row => {
    const mW = (row.male/maxVal*W).toFixed(1);
    const fW = (row.female/maxVal*W).toFixed(1);
    container.innerHTML += `
      <div class="pyr-row">
        <div class="pyr-left"><div class="pyr-bar male" style="width:0%" data-w="${mW}%"></div></div>
        <div class="pyr-label">${row.group}</div>
        <div class="pyr-right"><div class="pyr-bar female" style="width:0%" data-w="${fW}%"></div></div>
      </div>`;
  });
  setTimeout(() => {
    container.querySelectorAll('.pyr-bar').forEach(b => b.style.width = b.dataset.w);
  }, 500);
}

// ── TABLE ─────────────────────────────────────────────────
let tableData = Object.values(DATA).map((d,i)=>({...d, rank:i+1}));
let sortKey='penduduk', sortDir=-1;

function initTable() { renderTable(tableData); }

function renderTable(rows) {
  const tbody = document.getElementById('table-body');
  tbody.innerHTML = rows.map((d,i) => `
    <tr onclick="highlightKec('${getKey(d.nama)}')" style="cursor:pointer">
      <td><span class="td-rank">${i+1}</span></td>
      <td><strong>${d.nama}</strong></td>
      <td class="td-num">${d.penduduk.toLocaleString('id-ID')}</td>
      <td class="td-num">${d.laki.toLocaleString('id-ID')}</td>
      <td class="td-num">${d.perempuan.toLocaleString('id-ID')}</td>
      <td class="td-num">${d.kk.toLocaleString('id-ID')}</td>
      <td class="td-num">${d.luas.toFixed(2)}</td>
      <td class="td-num">${d.kepadatan.toLocaleString('id-ID')}</td>
    </tr>`).join('');
}

function getKey(nama) {
  return nama.replace('Pariaman ','').toLowerCase();
}

window.sortTable = function(key) {
  if(sortKey===key) sortDir*=-1; else { sortKey=key; sortDir=-1; }
  tableData.sort((a,b)=>{
    const av = typeof a[key]==='string' ? a[key] : a[key];
    const bv = typeof b[key]==='string' ? b[key] : b[key];
    return av < bv ? sortDir : -sortDir;
  });
  renderTable(tableData);
};

document.getElementById('search-input').addEventListener('input', e => {
  const q = e.target.value.toLowerCase();
  renderTable(tableData.filter(d=>d.nama.toLowerCase().includes(q)));
});

window.highlightKec = function(key) {
  const path = document.getElementById('kec-'+key);
  if(!path) return;
  document.querySelectorAll('.kecamatan').forEach(p=>p.classList.remove('active'));
  path.classList.add('active');
  showDetail(key);
  document.getElementById('peta').scrollIntoView({behavior:'smooth'});
};

// ── SCROLL REVEAL ──────────────────────────────────────────
function initReveal() {
  const obs = new IntersectionObserver(entries => {
    entries.forEach(e => { if(e.isIntersecting) { e.target.classList.add('visible'); obs.unobserve(e.target); }});
  }, {threshold:0.1});
  document.querySelectorAll('.reveal').forEach(el=>obs.observe(el));
}
</script>
</body>
</html>

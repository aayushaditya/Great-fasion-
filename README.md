<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Great Fashion</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  :root {
    --black: #0a0a0a;
    --white: #f5f0e8;
    --cream: #ede8dc;
    --gold: #c9a84c;
    --gold-light: #e8c96a;
    --red: #c0392b;
    --gray: #888;
    --card-bg: #111;
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--black);
    color: var(--white);
    font-family: 'DM Sans', sans-serif;
    font-weight: 300;
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  .cursor {
    position: fixed;
    width: 12px; height: 12px;
    background: var(--gold);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9999;
    transform: translate(-50%, -50%);
    transition: transform 0.1s, width 0.2s, height 0.2s, background 0.2s;
    mix-blend-mode: difference;
  }
  .cursor-ring {
    position: fixed;
    width: 40px; height: 40px;
    border: 1px solid var(--gold);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9998;
    transform: translate(-50%, -50%);
    transition: transform 0.15s ease-out, width 0.3s, height 0.3s;
    opacity: 0.6;
  }
  body:hover .cursor { opacity: 1; }

  /* NAV */
  nav {
    position: fixed; top: 0; left: 0; right: 0;
    z-index: 100;
    display: flex; align-items: center; justify-content: space-between;
    padding: 1.5rem 3rem;
    background: linear-gradient(to bottom, rgba(10,10,10,0.95), transparent);
    backdrop-filter: blur(2px);
  }

  .nav-logo {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 2rem;
    letter-spacing: 0.12em;
    color: var(--white);
    text-decoration: none;
    line-height: 1;
  }
  .nav-logo span { color: var(--gold); }

  .nav-links {
    display: flex; gap: 2.5rem; list-style: none;
  }
  .nav-links a {
    font-size: 0.75rem;
    letter-spacing: 0.18em;
    text-transform: uppercase;
    color: var(--white);
    text-decoration: none;
    opacity: 0.75;
    transition: opacity 0.2s, color 0.2s;
    position: relative;
  }
  .nav-links a::after {
    content: '';
    position: absolute; bottom: -3px; left: 0;
    width: 0; height: 1px;
    background: var(--gold);
    transition: width 0.3s;
  }
  .nav-links a:hover { opacity: 1; color: var(--gold); }
  .nav-links a:hover::after { width: 100%; }

  .nav-actions { display: flex; align-items: center; gap: 1.5rem; }
  .nav-icon {
    font-size: 1.1rem; opacity: 0.75; cursor: pointer;
    transition: opacity 0.2s;
  }
  .nav-icon:hover { opacity: 1; }
  .cart-badge {
    display: flex; align-items: center; gap: 0.4rem;
    font-size: 0.7rem; letter-spacing: 0.15em; text-transform: uppercase;
    border: 1px solid var(--gold); color: var(--gold);
    padding: 0.4rem 1rem; border-radius: 0;
    cursor: pointer; transition: background 0.2s, color 0.2s;
  }
  .cart-badge:hover { background: var(--gold); color: var(--black); }

  /* HERO */
  .hero {
    position: relative;
    height: 100vh;
    display: flex; align-items: flex-end;
    overflow: hidden;
    padding: 0 3rem 5rem;
  }

  .hero-bg {
    position: absolute; inset: 0;
    background:
      radial-gradient(ellipse at 70% 30%, rgba(201,168,76,0.12) 0%, transparent 60%),
      radial-gradient(ellipse at 20% 80%, rgba(192,57,43,0.10) 0%, transparent 50%),
      linear-gradient(135deg, #0a0a0a 0%, #1a1410 50%, #0a0a0a 100%);
  }

  .hero-grid {
    position: absolute; inset: 0;
    background-image:
      linear-gradient(rgba(201,168,76,0.04) 1px, transparent 1px),
      linear-gradient(90deg, rgba(201,168,76,0.04) 1px, transparent 1px);
    background-size: 60px 60px;
  }

  .hero-img-frame {
    position: absolute;
    right: 6%;
    top: 50%;
    transform: translateY(-50%);
    width: 38%;
    height: 75%;
    overflow: hidden;
  }
  .hero-img-frame::before {
    content: '';
    position: absolute; inset: 0;
    background: linear-gradient(to bottom, transparent 60%, var(--black) 100%),
                linear-gradient(to left, transparent 80%, var(--black) 100%);
    z-index: 1;
  }
  .hero-model {
    width: 100%; height: 100%;
    background:
      linear-gradient(160deg, #2a1f0e 0%, #1a1208 40%, #0d0a06 100%);
    display: flex; align-items: center; justify-content: center;
    font-family: 'Bebas Neue', sans-serif;
    font-size: 1rem;
    letter-spacing: 0.2em;
    color: rgba(201,168,76,0.3);
    flex-direction: column;
    gap: 1rem;
  }
  .model-placeholder {
    width: 120px; height: 120px;
    border: 1px solid rgba(201,168,76,0.2);
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-size: 3rem;
  }

  .hero-tag {
    position: absolute;
    top: 12rem; left: 3rem;
    font-size: 0.65rem;
    letter-spacing: 0.25em;
    text-transform: uppercase;
    color: var(--gold);
    opacity: 0.8;
    display: flex; align-items: center; gap: 0.75rem;
  }
  .hero-tag::before {
    content: '';
    display: inline-block;
    width: 40px; height: 1px;
    background: var(--gold);
  }

  .hero-content { position: relative; z-index: 2; max-width: 55%; }

  .hero-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(5rem, 11vw, 11rem);
    line-height: 0.88;
    letter-spacing: 0.02em;
    margin-bottom: 2rem;
  }
  .hero-title .line-accent { color: var(--gold); }
  .hero-title .line-outline {
    -webkit-text-stroke: 1px var(--white);
    color: transparent;
  }

  .hero-sub {
    font-size: 0.85rem;
    letter-spacing: 0.08em;
    color: rgba(245,240,232,0.6);
    max-width: 320px;
    line-height: 1.8;
    margin-bottom: 2.5rem;
  }

  .hero-ctas { display: flex; align-items: center; gap: 1.5rem; }

  .btn-primary {
    background: var(--gold);
    color: var(--black);
    font-family: 'DM Sans', sans-serif;
    font-size: 0.7rem;
    font-weight: 500;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    padding: 1rem 2.5rem;
    border: none; cursor: pointer;
    text-decoration: none;
    display: inline-block;
    transition: background 0.25s, transform 0.2s;
  }
  .btn-primary:hover { background: var(--gold-light); transform: translateY(-2px); }

  .btn-ghost {
    font-size: 0.7rem;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--white);
    text-decoration: none;
    opacity: 0.65;
    display: flex; align-items: center; gap: 0.6rem;
    transition: opacity 0.2s;
  }
  .btn-ghost:hover { opacity: 1; }
  .btn-ghost .arrow { font-size: 1rem; transition: transform 0.2s; }
  .btn-ghost:hover .arrow { transform: translateX(4px); }

  .hero-scroll {
    position: absolute;
    bottom: 3rem; right: 3rem;
    display: flex; flex-direction: column; align-items: center; gap: 0.5rem;
    font-size: 0.6rem; letter-spacing: 0.25em; text-transform: uppercase;
    color: rgba(245,240,232,0.4);
    z-index: 2;
  }
  .scroll-line {
    width: 1px; height: 60px;
    background: linear-gradient(to bottom, rgba(201,168,76,0.6), transparent);
    animation: scrollPulse 2s ease-in-out infinite;
  }
  @keyframes scrollPulse {
    0%, 100% { opacity: 0.4; transform: scaleY(1); }
    50% { opacity: 1; transform: scaleY(1.1); }
  }

  .hero-stats {
    position: absolute;
    bottom: 5rem; right: 48%;
    display: flex; gap: 2.5rem;
    z-index: 2;
  }
  .stat { text-align: center; }
  .stat-num {
    font-family: 'Playfair Display', serif;
    font-size: 1.8rem;
    color: var(--gold);
    display: block;
  }
  .stat-label {
    font-size: 0.6rem;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: rgba(245,240,232,0.4);
  }

  /* MARQUEE */
  .marquee-wrap {
    background: var(--gold);
    overflow: hidden;
    padding: 0.85rem 0;
  }
  .marquee-track {
    display: flex;
    animation: marquee 18s linear infinite;
    white-space: nowrap;
  }
  .marquee-track span {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 0.95rem;
    letter-spacing: 0.25em;
    color: var(--black);
    padding: 0 2.5rem;
  }
  .marquee-dot { color: var(--black); opacity: 0.5; }
  @keyframes marquee {
    from { transform: translateX(0); }
    to { transform: translateX(-50%); }
  }

  /* FEATURED */
  section { padding: 6rem 3rem; }

  .section-header {
    display: flex; align-items: flex-end; justify-content: space-between;
    margin-bottom: 3.5rem;
  }
  .section-eyebrow {
    font-size: 0.65rem;
    letter-spacing: 0.3em;
    text-transform: uppercase;
    color: var(--gold);
    margin-bottom: 0.6rem;
  }
  .section-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(2rem, 4vw, 3.5rem);
    font-weight: 400;
    line-height: 1.1;
  }
  .section-title em { font-style: italic; color: var(--gold); }
  .view-all {
    font-size: 0.7rem; letter-spacing: 0.2em; text-transform: uppercase;
    color: var(--gold); text-decoration: none;
    display: flex; align-items: center; gap: 0.5rem;
    opacity: 0.8; transition: opacity 0.2s;
    white-space: nowrap; margin-bottom: 0.5rem;
  }
  .view-all:hover { opacity: 1; }

  .products-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 1.5px;
  }

  .product-card {
    position: relative;
    background: var(--card-bg);
    overflow: hidden;
    cursor: pointer;
    group: true;
  }

  .product-card:first-child {
    grid-row: span 2;
  }

  .product-img {
    width: 100%;
    aspect-ratio: 3/4;
    display: flex; align-items: center; justify-content: center;
    position: relative;
    overflow: hidden;
    transition: transform 0.5s ease;
  }
  .product-card:first-child .product-img { aspect-ratio: auto; height: 100%; }

  .product-card:hover .product-img { transform: scale(1.03); }

  .product-img-bg {
    position: absolute; inset: 0;
    transition: transform 0.5s ease;
  }
  .bg-1 { background: linear-gradient(135deg, #1c1208 0%, #2d1f10 50%, #1a1208 100%); }
  .bg-2 { background: linear-gradient(135deg, #0e1520 0%, #162030 50%, #0c1218 100%); }
  .bg-3 { background: linear-gradient(135deg, #1a0e0e 0%, #2a1515 50%, #180c0c 100%); }
  .bg-4 { background: linear-gradient(135deg, #0d130e 0%, #142015 50%, #0b100c 100%); }
  .bg-5 { background: linear-gradient(135deg, #15120e 0%, #221d14 50%, #100e0a 100%); }

  .product-icon {
    position: relative; z-index: 1;
    font-size: 4rem;
    opacity: 0.35;
    transition: opacity 0.3s, transform 0.3s;
  }
  .product-card:hover .product-icon { opacity: 0.5; transform: scale(1.05); }

  .product-badge {
    position: absolute; top: 1rem; left: 1rem; z-index: 2;
    font-size: 0.6rem; letter-spacing: 0.2em; text-transform: uppercase;
    padding: 0.3rem 0.7rem;
  }
  .badge-new { background: var(--gold); color: var(--black); }
  .badge-hot { background: var(--red); color: var(--white); }

  .product-quick {
    position: absolute; bottom: 0; left: 0; right: 0; z-index: 3;
    background: var(--gold);
    color: var(--black);
    font-size: 0.65rem; letter-spacing: 0.2em; text-transform: uppercase;
    font-weight: 500;
    padding: 0.8rem;
    text-align: center;
    transform: translateY(100%);
    transition: transform 0.3s ease;
  }
  .product-card:hover .product-quick { transform: translateY(0); }

  .product-info {
    padding: 1.25rem 1rem;
    border-top: 1px solid rgba(255,255,255,0.05);
  }
  .product-name {
    font-family: 'Playfair Display', serif;
    font-size: 1rem;
    font-weight: 400;
    margin-bottom: 0.25rem;
  }
  .product-cat {
    font-size: 0.65rem; letter-spacing: 0.15em; text-transform: uppercase;
    color: var(--gray); margin-bottom: 0.75rem;
  }
  .product-footer { display: flex; align-items: center; justify-content: space-between; }
  .product-price { font-size: 1rem; color: var(--gold); font-weight: 500; }
  .product-price-old { font-size: 0.8rem; color: var(--gray); text-decoration: line-through; margin-left: 0.5rem; }
  .product-wish {
    width: 30px; height: 30px;
    border: 1px solid rgba(255,255,255,0.1);
    display: flex; align-items: center; justify-content: center;
    font-size: 0.85rem; cursor: pointer; transition: border-color 0.2s, color 0.2s;
    color: var(--gray);
  }
  .product-wish:hover { border-color: var(--red); color: var(--red); }

  /* EDITORIAL STRIP */
  .editorial {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1.5px;
    margin: 0;
    padding: 0;
  }
  .ed-panel {
    position: relative;
    height: 500px;
    overflow: hidden;
    cursor: pointer;
    display: flex; align-items: flex-end;
    padding: 3rem;
  }
  .ed-bg {
    position: absolute; inset: 0;
    transition: transform 0.6s ease;
  }
  .ed-panel:hover .ed-bg { transform: scale(1.04); }
  .ed-bg-1 {
    background: linear-gradient(135deg, #c9a84c22 0%, #c9a84c08 50%, #0a0a0a 100%),
                linear-gradient(to top, #0a0a0a 20%, transparent 70%),
                #111;
  }
  .ed-bg-2 {
    background: linear-gradient(135deg, #c0392b22 0%, #c0392b08 50%, #0a0a0a 100%),
                linear-gradient(to top, #0a0a0a 20%, transparent 70%),
                #111;
  }
  .ed-icon {
    position: absolute; top: 50%; left: 50%;
    transform: translate(-50%, -60%);
    font-size: 8rem; opacity: 0.12;
    transition: opacity 0.3s, transform 0.5s;
  }
  .ed-panel:hover .ed-icon { opacity: 0.18; transform: translate(-50%, -65%); }
  .ed-content { position: relative; z-index: 1; }
  .ed-eyebrow {
    font-size: 0.65rem; letter-spacing: 0.3em; text-transform: uppercase;
    margin-bottom: 0.6rem;
  }
  .ed-1 .ed-eyebrow { color: var(--gold); }
  .ed-2 .ed-eyebrow { color: var(--red); }
  .ed-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 3.5rem;
    line-height: 0.9;
    letter-spacing: 0.03em;
    margin-bottom: 1rem;
  }
  .ed-link {
    display: inline-flex; align-items: center; gap: 0.5rem;
    font-size: 0.7rem; letter-spacing: 0.2em; text-transform: uppercase;
    text-decoration: none; color: var(--white); opacity: 0.6;
    transition: opacity 0.2s;
  }
  .ed-link:hover { opacity: 1; }

  /* NEWSLETTER */
  .newsletter {
    background: var(--gold);
    padding: 5rem 3rem;
    display: grid;
    grid-template-columns: 1fr 1fr;
    align-items: center;
    gap: 4rem;
  }
  .nl-eyebrow {
    font-size: 0.65rem; letter-spacing: 0.3em; text-transform: uppercase;
    color: rgba(10,10,10,0.5); margin-bottom: 0.75rem;
  }
  .nl-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(2.5rem, 5vw, 4.5rem);
    color: var(--black);
    line-height: 0.9;
    letter-spacing: 0.02em;
  }
  .nl-form { display: flex; gap: 0; }
  .nl-input {
    flex: 1;
    background: var(--black);
    border: none;
    color: var(--white);
    padding: 1rem 1.5rem;
    font-family: 'DM Sans', sans-serif;
    font-size: 0.85rem;
    outline: none;
  }
  .nl-input::placeholder { color: rgba(245,240,232,0.3); }
  .nl-btn {
    background: var(--black);
    color: var(--gold);
    border: none;
    padding: 1rem 2rem;
    font-family: 'DM Sans', sans-serif;
    font-size: 0.7rem;
    font-weight: 500;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    cursor: pointer;
    transition: background 0.2s;
    white-space: nowrap;
  }
  .nl-btn:hover { background: #1a1a1a; }
  .nl-note { font-size: 0.7rem; color: rgba(10,10,10,0.5); margin-top: 0.75rem; }

  /* FOOTER */
  footer {
    padding: 4rem 3rem 2rem;
    border-top: 1px solid rgba(255,255,255,0.06);
  }
  .footer-top {
    display: grid; grid-template-columns: 2fr 1fr 1fr 1fr; gap: 3rem;
    margin-bottom: 4rem;
  }
  .footer-logo {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 2.5rem; letter-spacing: 0.1em;
    color: var(--white); margin-bottom: 1rem; display: block;
  }
  .footer-logo span { color: var(--gold); }
  .footer-desc { font-size: 0.8rem; color: var(--gray); line-height: 1.8; max-width: 260px; }
  .footer-col-title {
    font-size: 0.65rem; letter-spacing: 0.25em; text-transform: uppercase;
    color: var(--gold); margin-bottom: 1.25rem;
  }
  .footer-links { list-style: none; display: flex; flex-direction: column; gap: 0.65rem; }
  .footer-links a {
    font-size: 0.8rem; color: var(--gray); text-decoration: none;
    transition: color 0.2s;
  }
  .footer-links a:hover { color: var(--white); }
  .footer-bottom {
    display: flex; align-items: center; justify-content: space-between;
    padding-top: 2rem; border-top: 1px solid rgba(255,255,255,0.05);
  }
  .footer-copy { font-size: 0.7rem; color: rgba(255,255,255,0.2); }
  .social-links { display: flex; gap: 1rem; }
  .social-link {
    width: 34px; height: 34px;
    border: 1px solid rgba(255,255,255,0.1);
    display: flex; align-items: center; justify-content: center;
    font-size: 0.75rem; color: var(--gray); cursor: pointer;
    transition: border-color 0.2s, color 0.2s;
  }
  .social-link:hover { border-color: var(--gold); color: var(--gold); }

  /* ANIMATIONS */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
  }
  .hero-tag { animation: fadeUp 0.8s ease 0.2s both; }
  .hero-title { animation: fadeUp 0.8s ease 0.4s both; }
  .hero-sub { animation: fadeUp 0.8s ease 0.6s both; }
  .hero-ctas { animation: fadeUp 0.8s ease 0.8s both; }
  .hero-stats { animation: fadeUp 0.8s ease 1s both; }
  .hero-img-frame { animation: fadeUp 0.8s ease 0.3s both; }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- NAV -->
<nav>
  <a href="#" class="nav-logo">GREAT <span>F</span>ASHION</a>
  <ul class="nav-links">
    <li><a href="#">New In</a></li>
    <li><a href="#">Collections</a></li>
    <li><a href="#">Men</a></li>
    <li><a href="#">Women</a></li>
    <li><a href="#">Lookbook</a></li>
  </ul>
  <div class="nav-actions">
    <span class="nav-icon">🔍</span>
    <span class="nav-icon">♡</span>
    <div class="cart-badge">Bag · 0</div>
  </div>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="hero-bg"></div>
  <div class="hero-grid"></div>

  <div class="hero-tag">SS 2025 Collection</div>

  <div class="hero-img-frame">
    <div class="hero-model">
      <div class="model-placeholder">👗</div>
      <span>Campaign Image</span>
    </div>
  </div>

  <div class="hero-content">
    <h1 class="hero-title">
      <span class="line-outline">GREAT</span><br>
      <span class="line-accent">FASH</span><br>
      ION
    </h1>
    <p class="hero-sub">Where luxury meets the street. Curated pieces for those who refuse to blend in.</p>
    <div class="hero-ctas">
      <a href="#" class="btn-primary">Shop the Drop</a>
      <a href="#" class="btn-ghost">View Lookbook <span class="arrow">→</span></a>
    </div>
  </div>

  <div class="hero-stats">
    <div class="stat"><span class="stat-num">500+</span><span class="stat-label">Styles</span></div>
    <div class="stat"><span class="stat-num">42</span><span class="stat-label">Designers</span></div>
    <div class="stat"><span class="stat-num">98%</span><span class="stat-label">Rated ★★★★★</span></div>
  </div>

  <div class="hero-scroll">
    <div class="scroll-line"></div>
    <span>Scroll</span>
  </div>
</section>

<!-- MARQUEE -->
<div class="marquee-wrap">
  <div class="marquee-track">
    <span>NEW ARRIVALS</span><span class="marquee-dot">✦</span>
    <span>SS 2025</span><span class="marquee-dot">✦</span>
    <span>GREAT FASHION</span><span class="marquee-dot">✦</span>
    <span>FREE SHIPPING OVER $200</span><span class="marquee-dot">✦</span>
    <span>LUXURY STREETWEAR</span><span class="marquee-dot">✦</span>
    <span>NEW ARRIVALS</span><span class="marquee-dot">✦</span>
    <span>SS 2025</span><span class="marquee-dot">✦</span>
    <span>GREAT FASHION</span><span class="marquee-dot">✦</span>
    <span>FREE SHIPPING OVER $200</span><span class="marquee-dot">✦

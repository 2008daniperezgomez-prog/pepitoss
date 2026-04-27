<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>El Jardín – Santa Ana, Costa Rica</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=Cormorant+Garamond:ital,wght@0,300;0,400;1,300&family=Josefin+Sans:wght@300;400&display=swap" rel="stylesheet">
<style>
  :root {
    --green-deep: #1a3322;
    --green-mid: #2d5a3d;
    --green-light: #4a8c5c;
    --green-pale: #a8d5b5;
    --cream: #f5f0e8;
    --gold: #c9a84c;
    --gold-light: #e8c97a;
    --brown: #6b4c2a;
    --white: #fdfaf4;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; }

  body {
    font-family: 'Cormorant Garamond', serif;
    background: var(--green-deep);
    color: var(--cream);
    overflow-x: hidden;
    cursor: default;
  }

  /* Leafy background pattern */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: 
      radial-gradient(ellipse at 20% 20%, rgba(74,140,92,0.15) 0%, transparent 50%),
      radial-gradient(ellipse at 80% 80%, rgba(45,90,61,0.2) 0%, transparent 50%),
      radial-gradient(ellipse at 50% 50%, rgba(26,51,34,0.8) 0%, transparent 80%);
    pointer-events: none;
    z-index: 0;
  }

  /* ───── FLOATING LEAVES ───── */
  .leaf {
    position: fixed;
    font-size: 1.5rem;
    opacity: 0.07;
    pointer-events: none;
    z-index: 0;
    animation: drift linear infinite;
  }
  @keyframes drift {
    0%   { transform: translateY(-60px) rotate(0deg); opacity: 0; }
    10%  { opacity: 0.07; }
    90%  { opacity: 0.07; }
    100% { transform: translateY(110vh) rotate(360deg); opacity: 0; }
  }

  /* ───── NAVBAR ───── */
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 100;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1.2rem 3rem;
    background: linear-gradient(to bottom, rgba(26,51,34,0.95), transparent);
    backdrop-filter: blur(4px);
  }
  .nav-logo {
    font-family: 'Playfair Display', serif;
    font-size: 1.6rem;
    color: var(--gold);
    letter-spacing: 0.1em;
    text-decoration: none;
  }
  .nav-links { display: flex; gap: 2.5rem; list-style: none; }
  .nav-links a {
    font-family: 'Josefin Sans', sans-serif;
    font-size: 0.75rem;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--cream);
    text-decoration: none;
    transition: color 0.3s;
    opacity: 0.85;
  }
  .nav-links a:hover { color: var(--gold); opacity: 1; }

  /* ───── HERO ───── */
  .hero {
    position: relative;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    padding: 6rem 2rem 4rem;
    z-index: 1;
    overflow: hidden;
  }

  .hero-wreath {
    font-size: 8rem;
    line-height: 1;
    opacity: 0.12;
    position: absolute;
    animation: spin 60s linear infinite;
  }
  @keyframes spin { to { transform: rotate(360deg); } }

  .hero-badge {
    font-family: 'Josefin Sans', sans-serif;
    font-size: 0.7rem;
    letter-spacing: 0.35em;
    text-transform: uppercase;
    color: var(--gold);
    border: 1px solid rgba(201,168,76,0.4);
    padding: 0.5rem 1.5rem;
    margin-bottom: 2rem;
    animation: fadeUp 1s ease forwards;
    opacity: 0;
  }

  h1 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(4rem, 10vw, 8rem);
    line-height: 1;
    color: var(--white);
    animation: fadeUp 1s 0.2s ease forwards;
    opacity: 0;
  }
  h1 em {
    font-style: italic;
    color: var(--gold);
    display: block;
  }

  .hero-sub {
    font-size: 1.3rem;
    font-weight: 300;
    font-style: italic;
    color: var(--green-pale);
    margin-top: 1.5rem;
    animation: fadeUp 1s 0.4s ease forwards;
    opacity: 0;
    max-width: 500px;
  }

  .hero-divider {
    display: flex;
    align-items: center;
    gap: 1rem;
    margin: 2.5rem 0;
    animation: fadeUp 1s 0.5s ease forwards;
    opacity: 0;
  }
  .hero-divider span { color: var(--gold); font-size: 1.2rem; }
  .hero-divider::before, .hero-divider::after {
    content: '';
    width: 60px;
    height: 1px;
    background: linear-gradient(to right, transparent, var(--gold));
  }
  .hero-divider::after { background: linear-gradient(to left, transparent, var(--gold)); }

  .hero-stats {
    display: flex;
    gap: 3rem;
    animation: fadeUp 1s 0.6s ease forwards;
    opacity: 0;
  }
  .stat {
    text-align: center;
  }
  .stat-number {
    font-family: 'Playfair Display', serif;
    font-size: 2.5rem;
    color: var(--gold);
    line-height: 1;
  }
  .stat-label {
    font-family: 'Josefin Sans', sans-serif;
    font-size: 0.65rem;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--green-pale);
    margin-top: 0.3rem;
  }

  .scroll-hint {
    position: absolute;
    bottom: 2.5rem;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
    animation: bounce 2s ease infinite;
    opacity: 0.5;
  }
  .scroll-hint span {
    font-family: 'Josefin Sans', sans-serif;
    font-size: 0.6rem;
    letter-spacing: 0.3em;
    text-transform: uppercase;
    color: var(--green-pale);
  }
  .scroll-arrow { width: 20px; height: 20px; border-right: 1px solid var(--green-pale); border-bottom: 1px solid var(--green-pale); transform: rotate(45deg); }
  @keyframes bounce { 0%,100% { transform: translateX(-50%) translateY(0); } 50% { transform: translateX(-50%) translateY(8px); } }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(30px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  /* ───── SECTION BASE ───── */
  section { position: relative; z-index: 1; }

  .section-label {
    font-family: 'Josefin Sans', sans-serif;
    font-size: 0.65rem;
    letter-spacing: 0.35em;
    text-transform: uppercase;
    color: var(--gold);
    display: flex;
    align-items: center;
    gap: 1rem;
    margin-bottom: 1rem;
  }
  .section-label::before {
    content: '';
    width: 30px;
    height: 1px;
    background: var(--gold);
  }

  /* ───── ABOUT ───── */
  .about {
    padding: 8rem 4rem;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 6rem;
    max-width: 1200px;
    margin: 0 auto;
    align-items: center;
  }
  .about-text h2 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(2.5rem, 5vw, 4rem);
    line-height: 1.1;
    margin-bottom: 1.5rem;
  }
  .about-text h2 em { font-style: italic; color: var(--gold); }
  .about-text p {
    font-size: 1.15rem;
    line-height: 1.8;
    color: rgba(245,240,232,0.75);
    margin-bottom: 1rem;
    font-weight: 300;
  }

  .about-visual {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: auto auto;
    gap: 1rem;
  }
  .visual-card {
    background: rgba(45,90,61,0.3);
    border: 1px solid rgba(201,168,76,0.2);
    border-radius: 4px;
    padding: 2rem 1.5rem;
    text-align: center;
    transition: transform 0.3s, border-color 0.3s;
  }
  .visual-card:hover { transform: translateY(-4px); border-color: rgba(201,168,76,0.5); }
  .visual-card:first-child { grid-column: 1 / -1; }
  .visual-card .icon { font-size: 2.5rem; margin-bottom: 0.8rem; }
  .visual-card h3 {
    font-family: 'Playfair Display', serif;
    font-size: 1.3rem;
    color: var(--gold-light);
    margin-bottom: 0.4rem;
  }
  .visual-card p {
    font-size: 0.9rem;
    color: rgba(245,240,232,0.6);
    line-height: 1.5;
  }

  /* ───── HIGHLIGHTS ───── */
  .highlights {
    padding: 6rem 4rem;
    background: linear-gradient(135deg, rgba(45,90,61,0.2) 0%, rgba(26,51,34,0.4) 100%);
    border-top: 1px solid rgba(201,168,76,0.1);
    border-bottom: 1px solid rgba(201,168,76,0.1);
  }
  .highlights-inner { max-width: 1200px; margin: 0 auto; }
  .highlights h2 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(2rem, 4vw, 3rem);
    margin-bottom: 3rem;
    text-align: center;
  }
  .highlights h2 em { font-style: italic; color: var(--gold); }

  .highlight-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2rem;
  }
  .highlight-item {
    background: rgba(26,51,34,0.6);
    border: 1px solid rgba(201,168,76,0.15);
    border-radius: 4px;
    padding: 2.5rem 2rem;
    transition: all 0.3s;
    position: relative;
    overflow: hidden;
  }
  .highlight-item::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(to right, transparent, var(--gold), transparent);
    opacity: 0;
    transition: opacity 0.3s;
  }
  .highlight-item:hover { transform: translateY(-6px); border-color: rgba(201,168,76,0.3); }
  .highlight-item:hover::before { opacity: 1; }
  .hi-emoji { font-size: 2.5rem; margin-bottom: 1rem; display: block; }
  .hi-title {
    font-family: 'Playfair Display', serif;
    font-size: 1.4rem;
    color: var(--gold-light);
    margin-bottom: 0.7rem;
  }
  .hi-desc {
    font-size: 1rem;
    line-height: 1.7;
    color: rgba(245,240,232,0.65);
    font-weight: 300;
  }

  /* ───── MENU SPOTLIGHT ───── */
  .menu {
    padding: 8rem 4rem;
    max-width: 1200px;
    margin: 0 auto;
  }
  .menu-header { text-align: center; margin-bottom: 4rem; }
  .menu-header h2 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(2rem, 4vw, 3.5rem);
  }
  .menu-header h2 em { font-style: italic; color: var(--gold); }
  .menu-header p {
    color: rgba(245,240,232,0.6);
    font-size: 1.1rem;
    margin-top: 0.8rem;
    font-style: italic;
  }

  .menu-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 1.5rem;
  }
  .menu-card {
    background: rgba(45,90,61,0.15);
    border: 1px solid rgba(201,168,76,0.15);
    border-radius: 6px;
    padding: 2rem 1.5rem;
    text-align: center;
    transition: all 0.4s cubic-bezier(0.23, 1, 0.32, 1);
    cursor: default;
  }
  .menu-card:hover {
    background: rgba(45,90,61,0.35);
    border-color: rgba(201,168,76,0.4);
    transform: scale(1.03) translateY(-4px);
  }
  .menu-card .dish-icon { font-size: 3rem; margin-bottom: 1rem; }
  .menu-card h3 {
    font-family: 'Playfair Display', serif;
    font-size: 1.2rem;
    color: var(--white);
    margin-bottom: 0.5rem;
  }
  .menu-card p {
    font-size: 0.9rem;
    color: rgba(245,240,232,0.55);
    font-style: italic;
    line-height: 1.5;
  }
  .menu-card .tag {
    display: inline-block;
    margin-top: 1rem;
    font-family: 'Josefin Sans', sans-serif;
    font-size: 0.6rem;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--gold);
    border: 1px solid rgba(201,168,76,0.3);
    padding: 0.25rem 0.75rem;
    border-radius: 20px;
  }

  /* ───── REVIEWS ───── */
  .reviews {
    padding: 8rem 4rem;
    background: linear-gradient(to bottom, rgba(26,51,34,0.3), rgba(26,51,34,0.8));
    border-top: 1px solid rgba(201,168,76,0.1);
  }
  .reviews-inner { max-width: 1200px; margin: 0 auto; }
  .reviews-header { text-align: center; margin-bottom: 4rem; }
  .reviews-header h2 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(2rem, 4vw, 3rem);
  }
  .reviews-header h2 em { font-style: italic; color: var(--gold); }

  .reviews-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2rem;
  }
  .review-card {
    background: rgba(26,51,34,0.7);
    border: 1px solid rgba(201,168,76,0.12);
    border-radius: 6px;
    padding: 2.5rem 2rem;
    position: relative;
    transition: border-color 0.3s;
  }
  .review-card:hover { border-color: rgba(201,168,76,0.3); }
  .review-card .quote-mark {
    position: absolute;
    top: 1.2rem; right: 1.5rem;
    font-family: 'Playfair Display', serif;
    font-size: 5rem;
    line-height: 1;
    color: rgba(201,168,76,0.1);
    pointer-events: none;
  }
  .stars {
    color: var(--gold);
    font-size: 0.85rem;
    margin-bottom: 1rem;
    letter-spacing: 0.1em;
  }
  .review-text {
    font-size: 1rem;
    line-height: 1.75;
    color: rgba(245,240,232,0.75);
    font-style: italic;
    margin-bottom: 1.5rem;
    font-weight: 300;
  }
  .reviewer {
    display: flex;
    align-items: center;
    gap: 1rem;
  }
  .reviewer-avatar {
    width: 40px; height: 40px;
    border-radius: 50%;
    background: linear-gradient(135deg, var(--green-mid), var(--green-light));
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'Playfair Display', serif;
    font-size: 1rem;
    color: var(--gold);
    flex-shrink: 0;
  }
  .reviewer-name {
    font-family: 'Josefin Sans', sans-serif;
    font-size: 0.75rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--cream);
  }
  .reviewer-sub {
    font-size: 0.8rem;
    color: rgba(245,240,232,0.4);
    margin-top: 0.1rem;
  }

  /* ───── FOOTER ───── */
  footer {
    padding: 4rem;
    border-top: 1px solid rgba(201,168,76,0.15);
    background: rgba(10,25,16,0.8);
    text-align: center;
  }
  .footer-logo {
    font-family: 'Playfair Display', serif;
    font-size: 2.5rem;
    color: var(--gold);
    display: block;
    margin-bottom: 0.5rem;
  }
  .footer-tagline {
    font-style: italic;
    color: rgba(245,240,232,0.4);
    font-size: 1rem;
    margin-bottom: 2rem;
  }
  .footer-info {
    display: flex;
    justify-content: center;
    gap: 4rem;
    margin-bottom: 2rem;
    flex-wrap: wrap;
  }
  .footer-info-item {
    font-family: 'Josefin Sans', sans-serif;
    font-size: 0.7rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: rgba(245,240,232,0.45);
  }
  .footer-info-item span {
    display: block;
    color: var(--green-pale);
    font-size: 0.85rem;
    font-family: 'Cormorant Garamond', serif;
    font-style: italic;
    text-transform: none;
    letter-spacing: 0;
    margin-top: 0.3rem;
  }
  .footer-copy {
    font-size: 0.75rem;
    color: rgba(245,240,232,0.25);
    font-family: 'Josefin Sans', sans-serif;
    letter-spacing: 0.1em;
  }

  /* ───── DECORATIVE VINE ───── */
  .vine-divider {
    text-align: center;
    font-size: 2rem;
    opacity: 0.25;
    padding: 1rem 0;
    letter-spacing: 0.5rem;
  }

  /* ───── SCROLL ANIMATIONS ───── */
  .reveal {
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.8s ease, transform 0.8s ease;
  }
  .reveal.visible {
    opacity: 1;
    transform: translateY(0);
  }
  .reveal-delay-1 { transition-delay: 0.1s; }
  .reveal-delay-2 { transition-delay: 0.2s; }
  .reveal-delay-3 { transition-delay: 0.3s; }

  @media (max-width: 900px) {
    nav { padding: 1rem 1.5rem; }
    .nav-links { display: none; }
    .about { grid-template-columns: 1fr; padding: 4rem 2rem; gap: 3rem; }
    .highlight-grid { grid-template-columns: 1fr; }
    .menu-grid { grid-template-columns: 1fr 1fr; }
    .reviews-grid { grid-template-columns: 1fr; }
    .hero-stats { gap: 1.5rem; }
    .highlights, .menu, .reviews { padding: 5rem 2rem; }
    footer { padding: 3rem 2rem; }
    .footer-info { gap: 2rem; }
  }
</style>
</head>
<body>

<!-- Floating leaves -->
<div class="leaf" style="left:5%;animation-duration:18s;animation-delay:0s;font-size:2rem;">🍃</div>
<div class="leaf" style="left:20%;animation-duration:22s;animation-delay:4s;">🌿</div>
<div class="leaf" style="left:40%;animation-duration:16s;animation-delay:2s;font-size:1.2rem;">🍃</div>
<div class="leaf" style="left:60%;animation-duration:25s;animation-delay:7s;">🌿</div>
<div class="leaf" style="left:75%;animation-duration:19s;animation-delay:1s;font-size:2.2rem;">🍃</div>
<div class="leaf" style="left:90%;animation-duration:21s;animation-delay:5s;font-size:1rem;">🌱</div>

<!-- NAVBAR -->
<nav>
  <a href="#" class="nav-logo">El Jardín</a>
  <ul class="nav-links">
    <li><a href="#nosotros">Nosotros</a></li>
    <li><a href="#menu">Menú</a></li>
    <li><a href="#experiencia">Experiencia</a></li>
    <li><a href="#opiniones">Opiniones</a></li>
    <li><a href="#contacto">Contacto</a></li>
  </ul>
</nav>

<!-- HERO -->
<section class="hero" id="inicio">
  <div class="hero-wreath">🌿</div>
  <div class="hero-badge">Santa Ana · Costa Rica · Desde siempre</div>
  <h1>El<br><em>Jardín</em></h1>
  <p class="hero-sub">Pura naturaleza, sabor auténtico y un ambiente que enamora</p>
  <div class="hero-divider"><span>🌿</span></div>
  <div class="hero-stats">
    <div class="stat">
      <div class="stat-number">4.3</div>
      <div class="stat-label">Calificación</div>
    </div>
    <div class="stat">
      <div class="stat-number">+100</div>
      <div class="stat-label">Platillos</div>
    </div>
    <div class="stat">
      <div class="stat-number">3</div>
      <div class="stat-label">Ambientes</div>
    </div>
  </div>
  <div class="scroll-hint">
    <span>Explorar</span>
    <div class="scroll-arrow"></div>
  </div>
</section>

<!-- ABOUT -->
<section class="about" id="nosotros">
  <div class="about-text">
    <div class="section-label">Nuestra historia</div>
    <h2>Un rincón de <em>pura naturaleza</em> en Santa Ana</h2>
    <p>El Jardín es más que un restaurante: es un espacio donde la gastronomía costarricense tradicional se disfruta rodeada de verde, aire fresco y la calidez de nuestra gente.</p>
    <p>Con décadas sirviendo a familias, amigos y viajeros, nuestros platillos llevan el alma de Costa Rica: sabores genuinos, porciones generosas y precios que respetan tu bolsillo.</p>
    <p>Desde bocas legendarias hasta casados que reconfortan el alma, cada plato sale de una cocina con orgullo tico.</p>
  </div>
  <div class="about-visual">
    <div class="visual-card reveal">
      <div class="icon">🌿</div>
      <h3>Ambiente Natural</h3>
      <p>Mesas al aire libre rodeadas de vegetación. Un pedacito de jardín en medio de la ciudad.</p>
    </div>
    <div class="visual-card reveal reveal-delay-1">
      <div class="icon">🅿️</div>
      <h3>Amplio Parqueo</h3>
      <p>Estacionamiento seguro dentro de la propiedad para que llegues sin preocupaciones.</p>
    </div>
    <div class="visual-card reveal reveal-delay-2">
      <div class="icon">👨‍👩‍👧</div>
      <h3>Pet & Family Friendly</h3>
      <p>Espacios para niños, área de juegos y bienvenida para toda la familia, incluyendo mascotas.</p>
    </div>
  </div>
</section>

<!-- HIGHLIGHTS -->
<section class="highlights" id="experiencia">
  <div class="highlights-inner">
    <div class="section-label" style="justify-content:center;margin-bottom:0.5rem;">Lo que nos define</div>
    <h2 class="reveal" style="text-align:center;margin-bottom:3rem;">Lo <em>mejor</em> de El Jardín</h2>
    <div class="highlight-grid">
      <div class="highlight-item reveal">
        <span class="hi-emoji">🍽️</span>
        <div class="hi-title">Porciones Generosas</div>
        <p class="hi-desc">Nuestras bocas son tan abundantes que muchas veces son un plato por sí solas. Los casados alimentan de verdad, sin trucos.</p>
      </div>
      <div class="highlight-item reveal reveal-delay-1">
        <span class="hi-emoji">💰</span>
        <div class="hi-title">Precios Accesibles</div>
        <p class="hi-desc">Casados desde ₡5,000 y bocas que sorprenden por su calidad al precio. Comer bien no tiene que costar una fortuna.</p>
      </div>
      <div class="highlight-item reveal reveal-delay-2">
        <span class="hi-emoji">📺</span>
        <div class="hi-title">Ver el Partido</div>
        <p class="hi-desc">Múltiples pantallas, cerveza bien fría y un bar separado para disfrutar el fútbol en el mejor ambiente.</p>
      </div>
      <div class="highlight-item reveal">
        <span class="hi-emoji">🎶</span>
        <div class="hi-title">Música en Vivo</div>
        <p class="hi-desc">Noches especiales con artistas en vivo. El volumen perfecto para conversar y disfrutar sin perder el ritmo.</p>
      </div>
      <div class="highlight-item reveal reveal-delay-1">
        <span class="hi-emoji">🥗</span>
        <div class="hi-title">Menú Variado</div>
        <p class="hi-desc">Más de 100 platillos entre bocas y platos fuertes. Comida tica, mariscos, carnes, opciones vegetarianas y mucho más.</p>
      </div>
      <div class="highlight-item reveal reveal-delay-2">
        <span class="hi-emoji">🏡</span>
        <div class="hi-title">Arquitectura Colonial</div>
        <p class="hi-desc">Una casona al estilo cafetalero costarricense que te transporta a otra época, con ambiente acogedor y familiar.</p>
      </div>
    </div>
  </div>
</section>

<!-- MENU SPOTLIGHT -->
<section class="menu" id="menu">
  <div class="menu-header">
    <div class="section-label" style="justify-content:center;">Nuestros favoritos</div>
    <h2>Lo que más <em>enamora</em></h2>
    <p>Platos recomendados por nuestros clientes más fieles</p>
  </div>
  <div class="menu-grid">
    <div class="menu-card reveal">
      <div class="dish-icon">🦑</div>
      <h3>Sopa de Mariscos</h3>
      <p>En leche, con calamares, camarones, scallops y pulpo. La mejor que muchos han probado.</p>
      <span class="tag">⭐ Favorito</span>
    </div>
    <div class="menu-card reveal reveal-delay-1">
      <div class="dish-icon">🫔</div>
      <h3>Patacones Mixtos</h3>
      <p>Con frijoles molidos, guacamole y tomatito. Grandes, crocantes y deliciosos.</p>
      <span class="tag">Bocas</span>
    </div>
    <div class="menu-card reveal reveal-delay-2">
      <div class="dish-icon">🐟</div>
      <h3>Tacos de Pescado</h3>
      <p>Frescos, bien sazonados y con la cantidad justa. Los favoritos de quienes los prueban.</p>
      <span class="tag">Popular</span>
    </div>
    <div class="menu-card reveal reveal-delay-3">
      <div class="dish-icon">🐙</div>
      <h3>Pulpo al Ajillo</h3>
      <p>Bien cocido, sin textura hulosa. Con la cantidad perfecta de ajo y aceite de oliva.</p>
      <span class="tag">Mariscos</span>
    </div>
    <div class="menu-card reveal">
      <div class="dish-icon">🍖</div>
      <h3>Chifrijo</h3>
      <p>Un clásico tico que aquí se hace con amor. Grande, lleno y con todos los acompañamientos.</p>
      <span class="tag">⭐ Favorito</span>
    </div>
    <div class="menu-card reveal reveal-delay-1">
      <div class="dish-icon">🥩</div>
      <h3>Casado Tico</h3>
      <p>Carne, arroz, frijoles, picadillo y ensalada. Lo auténtico, bien servido, por lo justo.</p>
      <span class="tag">Almuerzo</span>
    </div>
    <div class="menu-card reveal reveal-delay-2">
      <div class="dish-icon">🍔</div>
      <h3>Mini Hamburguesas</h3>
      <p>Jugosas, bien condimentadas y perfectas para compartir. Una boca que no decepciona.</p>
      <span class="tag">Bocas</span>
    </div>
    <div class="menu-card reveal reveal-delay-3">
      <div class="dish-icon">🍹</div>
      <h3>Sangría & Cócteles</h3>
      <p>Sangría de vino blanco que muchos elogian. Cócteles bien preparados y a buen precio.</p>
      <span class="tag">Bebidas</span>
    </div>
  </div>
</section>

<!-- REVIEWS -->
<section class="reviews" id="opiniones">
  <div class="reviews-inner">
    <div class="reviews-header">
      <div class="section-label" style="justify-content:center;">Voces de nuestros clientes</div>
      <h2>Lo que dicen de <em>El Jardín</em></h2>
    </div>
    <div class="reviews-grid">

      <div class="review-card reveal">
        <div class="quote-mark">"</div>
        <div class="stars">★★★★★</div>
        <p class="review-text">Un restaurante excelente. Su comida, el ambiente precioso de pura naturaleza y la atención muy buena. Da gusto estar en ese lugar. Recomendado 100%.</p>
        <div class="reviewer">
          <div class="reviewer-avatar">P</div>
          <div>
            <div class="reviewer-name">Patricia Acevedo</div>
            <div class="reviewer-sub">Local Guide · Hace 10 meses</div>
          </div>
        </div>
      </div>

      <div class="review-card reveal reveal-delay-1">
        <div class="quote-mark">"</div>
        <div class="stars">★★★★★</div>
        <p class="review-text">Amazing place! Food is extremely good and the price is relatively cheap!</p>
        <div class="reviewer">
          <div class="reviewer-avatar">N</div>
          <div>
            <div class="reviewer-name">Niklas Baudy</div>
            <div class="reviewer-sub">Local Guide · Hace 2 meses</div>
          </div>
        </div>
      </div>

      <div class="review-card reveal reveal-delay-2">
        <div class="quote-mark">"</div>
        <div class="stars">★★★★★</div>
        <p class="review-text">Mi favorito de toda Costa Rica. La comida es deliciosa y súper accesible. Los casados salen alrededor de $7 y valen cada colón.</p>
        <div class="reviewer">
          <div class="reviewer-avatar">Y</div>
          <div>
            <div class="reviewer-name">Ysabel Ortiz</div>
            <div class="reviewer-sub">Local Guide · Hace 2 años</div>
          </div>
        </div>
      </div>

      <div class="review-card reveal">
        <div class="quote-mark">"</div>
        <div class="stars">★★★★★</div>
        <p class="review-text">Simplemente 10/10. Comida fresca, deliciosa, porciones grandes. Precios justos y hasta baratos. Ambientes para todo gusto, música en vivo muy seguido. Amplio parqueo.</p>
        <div class="reviewer">
          <div class="reviewer-avatar">I</div>
          <div>
            <div class="reviewer-name">Isaac RM</div>
            <div class="reviewer-sub">Local Guide · Hace 3 años</div>
          </div>
        </div>
      </div>

      <div class="review-card reveal reveal-delay-1">
        <div class="quote-mark">"</div>
        <div class="stars">★★★★★</div>
        <p class="review-text">Love this local favorite. Huge menu of Costa Rican and North American food. Vegetarian friendly, has the best veggie burger in Costa Rica! Service is good too.</p>
        <div class="reviewer">
          <div class="reviewer-avatar">S</div>
          <div>
            <div class="reviewer-name">Simone Kist</div>
            <div class="reviewer-sub">Local Guide · Hace un año</div>
          </div>
        </div>
      </div>

      <div class="review-card reveal reveal-delay-2">
        <div class="quote-mark">"</div>
        <div class="stars">★★★★★</div>
        <p class="review-text">El lugar es precioso. No imaginas encontrar un sitio así en medio de una carretera. Arquitectura colonial y muy cuidada. El trato fue increíble, agradables y con una sonrisa siempre.</p>
        <div class="reviewer">
          <div class="reviewer-avatar">A</div>
          <div>
            <div class="reviewer-name">Alma Gil Navas</div>
            <div class="reviewer-sub">Local Guide · Hace 3 años</div>
          </div>
        </div>
      </div>

    </div>
  </div>
</section>

<!-- FOOTER -->
<footer id="contacto">
  <span class="footer-logo">El Jardín</span>
  <p class="footer-tagline">Pura naturaleza · Sabor auténtico · Santa Ana, Costa Rica</p>
  <div class="vine-divider">🌿 · 🌱 · 🍃</div>
  <div class="footer-info">
    <div class="footer-info-item">
      Ubicación
      <span>Santa Ana, San José, Costa Rica</span>
    </div>
    <div class="footer-info-item">
      Parqueo
      <span>Amplio y seguro dentro de la propiedad</span>
    </div>
    <div class="footer-info-item">
      Ambiente
      <span>Familiar · Bar · Terraza · Eventos</span>
    </div>
    <div class="footer-info-item">
      Aceptamos
      <span>Grupos grandes · Pet friendly</span>
    </div>
  </div>
  <p class="footer-copy">© 2026 El Jardín Santa Ana · Todos los derechos reservados</p>
</footer>

<script>
  // Scroll reveal
  const reveals = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) { e.target.classList.add('visible'); }
    });
  }, { threshold: 0.15 });
  reveals.forEach(r => observer.observe(r));

  // Smooth parallax on hero wreath
  window.addEventListener('scroll', () => {
    const wreath = document.querySelector('.hero-wreath');
    if (wreath) wreath.style.transform = `rotate(${scrollY * 0.05}deg) scale(${1 + scrollY * 0.0003})`;
  });
</script>
</body>
</html>

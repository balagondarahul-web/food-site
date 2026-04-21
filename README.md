# food-site
trail food website
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>SAVOR — For Every Foodie</title>
  <link rel="preconnect" href="https://fonts.googleapis.com"/>
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin/>
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;0,900;1,400;1,700&family=DM+Sans:wght@300;400;500&family=Bebas+Neue&display=swap" rel="stylesheet"/>

  <style>
    /* ===== CSS VARIABLES ===== */
    :root {
      --cream:   #FAF6EF;
      --warm:    #F2E8D5;
      --rust:    #C84B2F;
      --ember:   #E8672A;
      --gold:    #D4A843;
      --forest:  #2C4A3E;
      --charcoal:#1A1A1A;
      --mid:     #555;
      --light:   #888;
      --white:   #FFFFFF;
      --font-display: 'Playfair Display', serif;
      --font-body:    'DM Sans', sans-serif;
      --font-impact:  'Bebas Neue', sans-serif;
      --radius: 4px;
      --transition: 0.35s cubic-bezier(0.4,0,0.2,1);
    }

    /* ===== RESET & BASE ===== */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; }
    body {
      font-family: var(--font-body);
      background: var(--cream);
      color: var(--charcoal);
      line-height: 1.65;
      overflow-x: hidden;
    }
    a { text-decoration: none; color: inherit; }
    img { max-width: 100%; display: block; }
    ul { list-style: none; }

    /* ===== UTILITY ===== */
    .container { max-width: 1200px; margin: 0 auto; padding: 0 24px; }
    .section-label {
      font-family: var(--font-body);
      font-size: 0.72rem;
      font-weight: 500;
      letter-spacing: 0.2em;
      text-transform: uppercase;
      color: var(--rust);
      display: block;
      margin-bottom: 12px;
    }
    .section-title {
      font-family: var(--font-display);
      font-size: clamp(2rem, 4vw, 3rem);
      font-weight: 900;
      line-height: 1.15;
      color: var(--charcoal);
    }
    .btn {
      display: inline-block;
      padding: 14px 32px;
      font-family: var(--font-body);
      font-size: 0.875rem;
      font-weight: 500;
      letter-spacing: 0.05em;
      border: none;
      cursor: pointer;
      transition: var(--transition);
      border-radius: var(--radius);
    }
    .btn-primary {
      background: var(--rust);
      color: var(--white);
    }
    .btn-primary:hover { background: var(--ember); transform: translateY(-2px); box-shadow: 0 8px 24px rgba(200,75,47,0.35); }
    .btn-outline {
      background: transparent;
      color: var(--white);
      border: 1.5px solid rgba(255,255,255,0.6);
    }
    .btn-outline:hover { background: rgba(255,255,255,0.1); border-color: white; }
    .btn-dark {
      background: var(--charcoal);
      color: var(--white);
    }
    .btn-dark:hover { background: var(--forest); transform: translateY(-2px); }

    /* ===== SCROLLBAR ===== */
    ::-webkit-scrollbar { width: 6px; }
    ::-webkit-scrollbar-track { background: var(--warm); }
    ::-webkit-scrollbar-thumb { background: var(--rust); border-radius: 3px; }

    /* ===== NAVBAR ===== */
    #navbar {
      position: fixed;
      top: 0; left: 0; right: 0;
      z-index: 1000;
      padding: 20px 0;
      transition: var(--transition);
    }
    #navbar.scrolled {
      background: rgba(250,246,239,0.96);
      backdrop-filter: blur(12px);
      padding: 12px 0;
      box-shadow: 0 2px 20px rgba(0,0,0,0.08);
    }
    .nav-inner {
      display: flex;
      align-items: center;
      justify-content: space-between;
    }
    .nav-logo {
      font-family: var(--font-impact);
      font-size: 2rem;
      letter-spacing: 0.08em;
      color: var(--white);
      transition: var(--transition);
    }
    #navbar.scrolled .nav-logo { color: var(--rust); }
    .nav-links {
      display: flex;
      gap: 36px;
      align-items: center;
    }
    .nav-links a {
      font-size: 0.875rem;
      font-weight: 500;
      color: rgba(255,255,255,0.9);
      position: relative;
      transition: var(--transition);
    }
    #navbar.scrolled .nav-links a { color: var(--charcoal); }
    .nav-links a::after {
      content: '';
      position: absolute;
      bottom: -4px; left: 0;
      width: 0; height: 2px;
      background: var(--rust);
      transition: var(--transition);
    }
    .nav-links a:hover::after { width: 100%; }
    .nav-links a:hover { color: var(--rust); }
    .nav-cta {
      background: var(--rust);
      color: var(--white) !important;
      padding: 8px 20px;
      border-radius: var(--radius);
    }
    .nav-cta:hover { background: var(--ember); }
    .nav-cta::after { display: none !important; }

    /* ===== HAMBURGER ===== */
    .hamburger {
      display: none;
      flex-direction: column;
      gap: 5px;
      cursor: pointer;
      background: none;
      border: none;
      padding: 4px;
    }
    .hamburger span {
      display: block;
      width: 26px; height: 2px;
      background: var(--white);
      transition: var(--transition);
      border-radius: 2px;
    }
    #navbar.scrolled .hamburger span { background: var(--charcoal); }
    .hamburger.open span:nth-child(1) { transform: translateY(7px) rotate(45deg); }
    .hamburger.open span:nth-child(2) { opacity: 0; }
    .hamburger.open span:nth-child(3) { transform: translateY(-7px) rotate(-45deg); }

    /* ===== MOBILE MENU ===== */
    .mobile-menu {
      display: none;
      flex-direction: column;
      background: var(--cream);
      border-top: 1px solid var(--warm);
      padding: 20px 24px;
      gap: 16px;
    }
    .mobile-menu.open { display: flex; }
    .mobile-menu a {
      font-size: 1rem;
      font-weight: 500;
      color: var(--charcoal);
      padding: 10px 0;
      border-bottom: 1px solid var(--warm);
    }
    .mobile-menu a:last-child { border-bottom: none; }

    /* ===== HERO ===== */
    #home {
      min-height: 100vh;
      background:
        linear-gradient(160deg, rgba(26,26,26,0.75) 0%, rgba(44,74,62,0.6) 100%),
        url('https://images.unsplash.com/photo-1504674900247-0877df9cc836?w=1600&q=80') center/cover no-repeat;
      display: flex;
      align-items: center;
      padding: 120px 0 80px;
      position: relative;
      overflow: hidden;
    }
    #home::before {
      content: '';
      position: absolute;
      bottom: 0; left: 0; right: 0;
      height: 120px;
      background: linear-gradient(to top, var(--cream), transparent);
    }
    .hero-content { position: relative; z-index: 1; max-width: 720px; }
    .hero-tag {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      background: rgba(255,255,255,0.15);
      backdrop-filter: blur(8px);
      border: 1px solid rgba(255,255,255,0.25);
      color: var(--white);
      font-size: 0.78rem;
      font-weight: 500;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      padding: 8px 16px;
      border-radius: 100px;
      margin-bottom: 28px;
    }
    .hero-tag span { color: var(--gold); font-size: 1.1em; }
    .hero-title {
      font-family: var(--font-display);
      font-size: clamp(3rem, 7vw, 5.5rem);
      font-weight: 900;
      color: var(--white);
      line-height: 1.05;
      margin-bottom: 24px;
    }
    .hero-title em {
      font-style: italic;
      color: var(--gold);
    }
    .hero-subtitle {
      font-size: 1.125rem;
      color: rgba(255,255,255,0.82);
      font-weight: 300;
      max-width: 500px;
      margin-bottom: 40px;
      line-height: 1.7;
    }
    .hero-actions { display: flex; gap: 16px; flex-wrap: wrap; }
    .hero-stats {
      display: flex;
      gap: 40px;
      margin-top: 64px;
      flex-wrap: wrap;
    }
    .stat-item { color: var(--white); }
    .stat-number {
      font-family: var(--font-impact);
      font-size: 2.5rem;
      letter-spacing: 0.04em;
      color: var(--gold);
      display: block;
    }
    .stat-label {
      font-size: 0.8rem;
      font-weight: 400;
      color: rgba(255,255,255,0.7);
      letter-spacing: 0.06em;
      text-transform: uppercase;
    }

    /* ===== TICKER ===== */
    .ticker-wrap {
      background: var(--rust);
      padding: 14px 0;
      overflow: hidden;
      white-space: nowrap;
    }
    .ticker-track {
      display: inline-block;
      animation: ticker 25s linear infinite;
    }
    .ticker-track span {
      font-family: var(--font-impact);
      font-size: 1.1rem;
      letter-spacing: 0.1em;
      color: var(--white);
      margin: 0 32px;
    }
    .ticker-track span.dot { color: var(--gold); font-size: 0.6rem; vertical-align: middle; }
    @keyframes ticker {
      0%   { transform: translateX(0); }
      100% { transform: translateX(-50%); }
    }

    /* ===== ABOUT ===== */
    #about { padding: 100px 0; }
    .about-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 80px;
      align-items: center;
    }
    .about-img-wrap {
      position: relative;
    }
    .about-img-main {
      width: 100%;
      height: 520px;
      object-fit: cover;
      border-radius: 8px;
    }
    .about-img-accent {
      position: absolute;
      bottom: -32px; right: -32px;
      width: 200px; height: 200px;
      object-fit: cover;
      border-radius: 8px;
      border: 6px solid var(--cream);
      box-shadow: 0 16px 40px rgba(0,0,0,0.15);
    }
    .about-badge {
      position: absolute;
      top: 24px; left: -20px;
      background: var(--rust);
      color: var(--white);
      padding: 16px 20px;
      border-radius: 8px;
      text-align: center;
      box-shadow: 0 8px 24px rgba(200,75,47,0.4);
    }
    .about-badge strong {
      font-family: var(--font-impact);
      font-size: 2.2rem;
      letter-spacing: 0.04em;
      display: block;
    }
    .about-badge span { font-size: 0.72rem; letter-spacing: 0.1em; text-transform: uppercase; opacity: 0.9; }
    .about-text { }
    .about-text .section-title { margin-bottom: 20px; }
    .about-lead {
      font-size: 1.1rem;
      font-weight: 500;
      color: var(--forest);
      margin-bottom: 16px;
      font-family: var(--font-display);
      font-style: italic;
    }
    .about-text p { color: var(--mid); margin-bottom: 16px; }
    .about-pills {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      margin: 28px 0;
    }
    .pill {
      background: var(--warm);
      color: var(--charcoal);
      padding: 8px 18px;
      border-radius: 100px;
      font-size: 0.82rem;
      font-weight: 500;
      transition: var(--transition);
    }
    .pill:hover { background: var(--rust); color: var(--white); }

    /* ===== SERVICES ===== */
    #services {
      padding: 100px 0;
      background: var(--charcoal);
      position: relative;
      overflow: hidden;
    }
    #services::before {
      content: 'FOOD';
      position: absolute;
      font-family: var(--font-impact);
      font-size: 22vw;
      color: rgba(255,255,255,0.03);
      top: 50%; left: 50%;
      transform: translate(-50%, -50%);
      letter-spacing: 0.1em;
      pointer-events: none;
      white-space: nowrap;
    }
    #services .section-label { color: var(--gold); }
    #services .section-title { color: var(--white); }
    .services-header {
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
      margin-bottom: 60px;
      flex-wrap: wrap;
      gap: 24px;
    }
    .services-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 24px;
    }
    .service-card {
      background: rgba(255,255,255,0.04);
      border: 1px solid rgba(255,255,255,0.08);
      border-radius: 8px;
      overflow: hidden;
      transition: var(--transition);
      position: relative;
      group: true;
    }
    .service-card:hover {
      transform: translateY(-6px);
      border-color: rgba(200,75,47,0.4);
      box-shadow: 0 20px 60px rgba(0,0,0,0.4);
    }
    .service-img {
      width: 100%; height: 220px;
      object-fit: cover;
      transition: var(--transition);
    }
    .service-card:hover .service-img { transform: scale(1.05); }
    .service-img-wrap { overflow: hidden; }
    .service-body { padding: 28px; }
    .service-icon {
      font-size: 1.8rem;
      margin-bottom: 16px;
      display: block;
    }
    .service-title {
      font-family: var(--font-display);
      font-size: 1.25rem;
      font-weight: 700;
      color: var(--white);
      margin-bottom: 10px;
    }
    .service-desc {
      font-size: 0.875rem;
      color: rgba(255,255,255,0.55);
      line-height: 1.7;
      margin-bottom: 20px;
    }
    .service-link {
      font-size: 0.82rem;
      font-weight: 500;
      color: var(--ember);
      letter-spacing: 0.06em;
      text-transform: uppercase;
      display: inline-flex;
      align-items: center;
      gap: 6px;
      transition: var(--transition);
    }
    .service-link:hover { gap: 10px; }
    .service-card.featured {
      background: var(--rust);
      border-color: var(--rust);
    }
    .service-card.featured .service-title { color: var(--white); }
    .service-card.featured .service-desc { color: rgba(255,255,255,0.8); }
    .service-card.featured .service-link { color: var(--gold); }

    /* ===== MENU HIGHLIGHTS ===== */
    #menu { padding: 100px 0; background: var(--warm); }
    .menu-header { text-align: center; margin-bottom: 60px; }
    .menu-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 20px;
    }
    .menu-card {
      background: var(--white);
      border-radius: 8px;
      overflow: hidden;
      transition: var(--transition);
      cursor: pointer;
    }
    .menu-card:hover { transform: translateY(-4px); box-shadow: 0 16px 40px rgba(0,0,0,0.12); }
    .menu-img {
      width: 100%; height: 200px;
      object-fit: cover;
      transition: var(--transition);
    }
    .menu-card:hover .menu-img { transform: scale(1.06); }
    .menu-img-wrap { overflow: hidden; }
    .menu-body { padding: 20px; }
    .menu-category {
      font-size: 0.72rem;
      font-weight: 500;
      color: var(--rust);
      text-transform: uppercase;
      letter-spacing: 0.12em;
      margin-bottom: 6px;
    }
    .menu-name {
      font-family: var(--font-display);
      font-size: 1.05rem;
      font-weight: 700;
      color: var(--charcoal);
      margin-bottom: 8px;
    }
    .menu-footer { display: flex; justify-content: space-between; align-items: center; margin-top: 12px; }
    .menu-price {
      font-family: var(--font-display);
      font-size: 1.15rem;
      font-weight: 700;
      color: var(--rust);
    }
    .menu-rating { font-size: 0.82rem; color: var(--light); }
    .menu-rating span { color: var(--gold); }

    /* ===== TESTIMONIALS ===== */
    #testimonials { padding: 100px 0; }
    .test-header { text-align: center; margin-bottom: 60px; }
    .test-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 28px;
    }
    .test-card {
      background: var(--white);
      border-radius: 8px;
      padding: 36px;
      border: 1px solid rgba(0,0,0,0.07);
      transition: var(--transition);
      position: relative;
    }
    .test-card:hover { box-shadow: 0 12px 40px rgba(0,0,0,0.1); transform: translateY(-3px); }
    .test-quote {
      font-family: var(--font-impact);
      font-size: 5rem;
      color: var(--rust);
      opacity: 0.15;
      line-height: 0.5;
      margin-bottom: 20px;
      display: block;
    }
    .test-text {
      font-family: var(--font-display);
      font-style: italic;
      font-size: 1rem;
      color: var(--charcoal);
      line-height: 1.75;
      margin-bottom: 24px;
    }
    .test-author { display: flex; align-items: center; gap: 14px; }
    .test-avatar {
      width: 46px; height: 46px;
      border-radius: 50%;
      object-fit: cover;
    }
    .test-name {
      font-weight: 600;
      font-size: 0.9rem;
      color: var(--charcoal);
    }
    .test-role { font-size: 0.78rem; color: var(--light); }
    .test-stars { color: var(--gold); font-size: 0.85rem; margin-bottom: 4px; }

    /* ===== CONTACT ===== */
    #contact { padding: 100px 0; background: var(--forest); }
    #contact .section-label { color: var(--gold); }
    #contact .section-title { color: var(--white); margin-bottom: 16px; }
    .contact-grid {
      display: grid;
      grid-template-columns: 1fr 1.4fr;
      gap: 80px;
      align-items: start;
    }
    .contact-intro { color: rgba(255,255,255,0.7); font-size: 0.95rem; line-height: 1.75; margin-bottom: 40px; }
    .contact-detail {
      display: flex;
      align-items: flex-start;
      gap: 16px;
      margin-bottom: 24px;
    }
    .contact-icon {
      width: 44px; height: 44px;
      background: rgba(255,255,255,0.08);
      border-radius: 8px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1.2rem;
      flex-shrink: 0;
    }
    .contact-detail-text strong {
      display: block;
      color: var(--white);
      font-size: 0.85rem;
      font-weight: 600;
      margin-bottom: 2px;
    }
    .contact-detail-text span { color: rgba(255,255,255,0.6); font-size: 0.875rem; }
    /* Form */
    .contact-form {
      background: rgba(255,255,255,0.06);
      border: 1px solid rgba(255,255,255,0.1);
      border-radius: 12px;
      padding: 48px;
    }
    .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
    .form-group { margin-bottom: 20px; }
    .form-group label {
      display: block;
      font-size: 0.78rem;
      font-weight: 500;
      color: rgba(255,255,255,0.7);
      letter-spacing: 0.08em;
      text-transform: uppercase;
      margin-bottom: 8px;
    }
    .form-group input,
    .form-group select,
    .form-group textarea {
      width: 100%;
      background: rgba(255,255,255,0.07);
      border: 1.5px solid rgba(255,255,255,0.12);
      border-radius: var(--radius);
      padding: 14px 16px;
      font-family: var(--font-body);
      font-size: 0.9rem;
      color: var(--white);
      outline: none;
      transition: var(--transition);
      -webkit-appearance: none;
    }
    .form-group input::placeholder,
    .form-group textarea::placeholder { color: rgba(255,255,255,0.3); }
    .form-group input:focus,
    .form-group select:focus,
    .form-group textarea:focus {
      border-color: var(--gold);
      background: rgba(255,255,255,0.1);
    }
    .form-group select option { background: var(--forest); color: var(--white); }
    .form-group textarea { resize: vertical; min-height: 120px; }
    .form-error { font-size: 0.78rem; color: #ff8a7a; margin-top: 5px; display: none; }
    .form-success {
      display: none;
      background: rgba(212,168,67,0.15);
      border: 1px solid rgba(212,168,67,0.4);
      border-radius: 8px;
      padding: 16px 20px;
      color: var(--gold);
      font-size: 0.9rem;
      margin-top: 16px;
      text-align: center;
    }

    /* ===== LOCATION ===== */
    #location { padding: 100px 0; }
    .location-grid {
      display: grid;
      grid-template-columns: 1fr 1.6fr;
      gap: 60px;
      align-items: start;
    }
    .location-info { }
    .location-card {
      background: var(--white);
      border-radius: 8px;
      padding: 32px;
      border: 1px solid rgba(0,0,0,0.07);
      margin-bottom: 20px;
      transition: var(--transition);
    }
    .location-card:hover { box-shadow: 0 8px 28px rgba(0,0,0,0.1); }
    .location-card-top {
      display: flex;
      align-items: center;
      gap: 14px;
      margin-bottom: 16px;
    }
    .loc-icon {
      width: 44px; height: 44px;
      background: var(--warm);
      border-radius: 8px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1.3rem;
    }
    .loc-name {
      font-family: var(--font-display);
      font-weight: 700;
      font-size: 1.1rem;
    }
    .loc-tag {
      font-size: 0.72rem;
      background: var(--rust);
      color: white;
      padding: 2px 8px;
      border-radius: 100px;
      font-weight: 500;
    }
    .loc-address { font-size: 0.875rem; color: var(--mid); line-height: 1.65; }
    .hours-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 8px 16px;
      margin-top: 12px;
      font-size: 0.82rem;
      color: var(--mid);
    }
    .hours-grid strong { color: var(--charcoal); }
    .map-embed {
      border-radius: 12px;
      overflow: hidden;
      box-shadow: 0 12px 40px rgba(0,0,0,0.12);
      height: 480px;
      background: var(--warm);
      position: relative;
    }
    .map-embed iframe {
      width: 100%; height: 100%;
      border: none;
    }
    .map-placeholder {
      width: 100%; height: 100%;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      gap: 16px;
      color: var(--mid);
      background:
        linear-gradient(135deg, var(--warm) 0%, var(--cream) 100%);
    }
    .map-placeholder .map-pin {
      font-size: 4rem;
      animation: bounce 2s infinite;
    }
    @keyframes bounce {
      0%,100% { transform: translateY(0); }
      50%      { transform: translateY(-12px); }
    }
    .map-placeholder p { font-family: var(--font-display); font-size: 1.2rem; color: var(--charcoal); }
    .map-placeholder span { font-size: 0.875rem; color: var(--light); }

    /* ===== FOOTER ===== */
    footer {
      background: var(--charcoal);
      padding: 64px 0 28px;
    }
    .footer-grid {
      display: grid;
      grid-template-columns: 1.8fr 1fr 1fr 1fr;
      gap: 48px;
      margin-bottom: 48px;
    }
    .footer-brand .logo {
      font-family: var(--font-impact);
      font-size: 2.4rem;
      letter-spacing: 0.08em;
      color: var(--white);
      margin-bottom: 16px;
      display: block;
    }
    .footer-brand p { font-size: 0.875rem; color: rgba(255,255,255,0.5); line-height: 1.7; max-width: 260px; }
    .footer-socials {
      display: flex;
      gap: 12px;
      margin-top: 24px;
    }
    .social-btn {
      width: 38px; height: 38px;
      border-radius: 8px;
      background: rgba(255,255,255,0.07);
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1rem;
      color: rgba(255,255,255,0.6);
      transition: var(--transition);
      border: 1px solid rgba(255,255,255,0.08);
    }
    .social-btn:hover { background: var(--rust); color: white; border-color: var(--rust); }
    .footer-col h4 {
      font-family: var(--font-body);
      font-size: 0.8rem;
      font-weight: 600;
      color: rgba(255,255,255,0.5);
      letter-spacing: 0.12em;
      text-transform: uppercase;
      margin-bottom: 20px;
    }
    .footer-col ul { display: flex; flex-direction: column; gap: 12px; }
    .footer-col ul li a {
      font-size: 0.875rem;
      color: rgba(255,255,255,0.6);
      transition: var(--transition);
    }
    .footer-col ul li a:hover { color: var(--gold); padding-left: 4px; }
    .footer-bottom {
      border-top: 1px solid rgba(255,255,255,0.08);
      padding-top: 24px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 12px;
    }
    .footer-bottom p { font-size: 0.8rem; color: rgba(255,255,255,0.35); }
    .footer-bottom span { color: var(--rust); }

    /* ===== SCROLL TO TOP ===== */
    #scrollTop {
      position: fixed;
      bottom: 32px; right: 32px;
      width: 46px; height: 46px;
      background: var(--rust);
      color: white;
      border: none;
      border-radius: 50%;
      font-size: 1.2rem;
      cursor: pointer;
      display: none;
      align-items: center;
      justify-content: center;
      box-shadow: 0 4px 20px rgba(200,75,47,0.5);
      transition: var(--transition);
      z-index: 999;
    }
    #scrollTop.visible { display: flex; }
    #scrollTop:hover { background: var(--ember); transform: translateY(-3px); }

    /* ===== ANIMATIONS ===== */
    .fade-up {
      opacity: 0;
      transform: translateY(32px);
      transition: opacity 0.7s ease, transform 0.7s ease;
    }
    .fade-up.visible { opacity: 1; transform: translateY(0); }

    /* ===== RESPONSIVE ===== */
    @media (max-width: 1024px) {
      .services-grid { grid-template-columns: repeat(2, 1fr); }
      .menu-grid { grid-template-columns: repeat(2, 1fr); }
      .footer-grid { grid-template-columns: 1fr 1fr; }
    }
    @media (max-width: 768px) {
      .nav-links { display: none; }
      .hamburger { display: flex; }
      .about-grid,
      .contact-grid,
      .location-grid { grid-template-columns: 1fr; gap: 40px; }
      .about-img-accent { display: none; }
      .about-badge { left: 16px; }
      .services-grid { grid-template-columns: 1fr; }
      .menu-grid { grid-template-columns: repeat(2, 1fr); }
      .test-grid { grid-template-columns: 1fr; }
      .form-row { grid-template-columns: 1fr; }
      .contact-form { padding: 28px 24px; }
      .footer-grid { grid-template-columns: 1fr; gap: 32px; }
      .footer-bottom { flex-direction: column; text-align: center; }
      .hero-stats { gap: 28px; }
    }
    @media (max-width: 480px) {
      .menu-grid { grid-template-columns: 1fr; }
      .hero-actions { flex-direction: column; }
      .btn { text-align: center; }
    }
  </style>
</head>
<body>

  <!-- ===== NAVBAR ===== -->
  <nav id="navbar" role="navigation" aria-label="Main navigation">
    <div class="container nav-inner">
      <a href="#home" class="nav-logo">SAVOR</a>
      <ul class="nav-links" role="list">
        <li><a href="#home">Home</a></li>
        <li><a href="#about">About</a></li>
        <li><a href="#services">Services</a></li>
        <li><a href="#menu">Menu</a></li>
        <li><a href="#contact">Contact</a></li>
        <li><a href="#location">Location</a></li>
        <li><a href="#contact" class="nav-cta">Book a Table</a></li>
      </ul>
      <button class="hamburger" id="hamburger" aria-label="Toggle menu" aria-expanded="false">
        <span></span><span></span><span></span>
      </button>
    </div>
    <!-- Mobile menu -->
    <div class="mobile-menu" id="mobileMenu" role="list">
      <a href="#home" role="listitem">Home</a>
      <a href="#about" role="listitem">About</a>
      <a href="#services" role="listitem">Services</a>
      <a href="#menu" role="listitem">Menu</a>
      <a href="#contact" role="listitem">Contact</a>
      <a href="#location" role="listitem">Location</a>
      <a href="#contact" role="listitem" style="color:var(--rust);font-weight:600;">📅 Book a Table</a>
    </div>
  </nav>

  <!-- ===== HERO ===== -->
  <section id="home" aria-label="Hero">
    <div class="container">
      <div class="hero-content">
        <div class="hero-tag">
          <span>★</span> Awarded Best Food Experience 2025
        </div>
        <h1 class="hero-title">
          Life is too short<br/>for <em>bad food.</em>
        </h1>
        <p class="hero-subtitle">
          Discover handcrafted dishes, curated culinary journeys, and unforgettable flavours — made for every foodie who believes eating is an art.
        </p>
        <div class="hero-actions">
          <a href="#menu" class="btn btn-primary">Explore Our Menu</a>
          <a href="#about" class="btn btn-outline">Our Story ↓</a>
        </div>
        <div class="hero-stats">
          <div class="stat-item">
            <span class="stat-number">250+</span>
            <span class="stat-label">Signature Dishes</span>
          </div>
          <div class="stat-item">
            <span class="stat-number">40K</span>
            <span class="stat-label">Happy Foodies</span>
          </div>
          <div class="stat-item">
            <span class="stat-number">15</span>
            <span class="stat-label">Years of Flavour</span>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- ===== TICKER ===== -->
  <div class="ticker-wrap" aria-hidden="true">
    <div class="ticker-track">
      <span>FARM TO TABLE</span><span class="dot">●</span>
      <span>ARTISAN CUISINE</span><span class="dot">●</span>
      <span>SEASONAL MENUS</span><span class="dot">●</span>
      <span>CURATED WINE LIST</span><span class="dot">●</span>
      <span>PRIVATE DINING</span><span class="dot">●</span>
      <span>COOKING CLASSES</span><span class="dot">●</span>
      <span>FOOD EVENTS</span><span class="dot">●</span>
      <span>FARM TO TABLE</span><span class="dot">●</span>
      <span>ARTISAN CUISINE</span><span class="dot">●</span>
      <span>SEASONAL MENUS</span><span class="dot">●</span>
      <span>CURATED WINE LIST</span><span class="dot">●</span>
      <span>PRIVATE DINING</span><span class="dot">●</span>
      <span>COOKING CLASSES</span><span class="dot">●</span>
      <span>FOOD EVENTS</span><span class="dot">●</span>
    </div>
  </div>

  <!-- ===== ABOUT ===== -->
  <section id="about" aria-labelledby="about-title">
    <div class="container">
      <div class="about-grid">
        <!-- Image column -->
        <div class="about-img-wrap fade-up">
          <img
            class="about-img-main"
            src="https://images.unsplash.com/photo-1556909114-f6e7ad7d3136?w=800&q=80"
            alt="Chef preparing a dish with fresh ingredients"
            loading="lazy"
          />
          <img
            class="about-img-accent"
            src="https://images.unsplash.com/photo-1414235077428-338989a2e8c0?w=400&q=80"
            alt="Elegantly plated dish"
            loading="lazy"
          />
          <div class="about-badge">
            <strong>15+</strong>
            <span>Yrs of Excellence</span>
          </div>
        </div>
        <!-- Text column -->
        <div class="about-text fade-up">
          <span class="section-label">Our Story</span>
          <h2 id="about-title" class="section-title">
            Passion for food,<br/>crafted with love.
          </h2>
          <p class="about-lead">"Every bite tells a story. Ours begins with honest ingredients."</p>
          <p>Founded in 2010 by Chef Arya Menon, SAVOR was born from a simple belief — that extraordinary food doesn't need to be complicated. Just honest, seasonal ingredients treated with respect and creativity.</p>
          <p>We source from local farms within 100 km, partner with heritage producers, and change our menu with the seasons so every visit feels new.</p>
          <div class="about-pills">
            <span class="pill">🌿 Locally Sourced</span>
            <span class="pill">🍷 Curated Wines</span>
            <span class="pill">👨‍🍳 Expert Chefs</span>
            <span class="pill">🌱 Sustainable</span>
            <span class="pill">🎉 Private Events</span>
          </div>
          <a href="#services" class="btn btn-dark">Discover Our Services →</a>
        </div>
      </div>
    </div>
  </section>

  <!-- ===== SERVICES ===== -->
  <section id="services" aria-labelledby="services-title">
    <div class="container">
      <div class="services-header">
        <div>
          <span class="section-label">What We Offer</span>
          <h2 id="services-title" class="section-title">Experiences designed<br/>for every palate.</h2>
        </div>
        <a href="#contact" class="btn btn-primary" style="align-self:flex-end;">Book Now →</a>
      </div>
      <div class="services-grid">

        <!-- Card 1 – Featured -->
        <div class="service-card featured fade-up">
          <div class="service-img-wrap">
            <img class="service-img" src="https://images.unsplash.com/photo-1467003909585-2f8a72700288?w=600&q=80" alt="Fine dining" loading="lazy"/>
          </div>
          <div class="service-body">
            <span class="service-icon">🍽️</span>
            <h3 class="service-title">Fine Dining Experience</h3>
            <p class="service-desc">Multi-course tasting menus crafted by our head chef. An unforgettable evening of flavours, textures, and stories.</p>
            <a href="#contact" class="service-link">Reserve a Table →</a>
          </div>
        </div>

        <!-- Card 2 -->
        <div class="service-card fade-up">
          <div class="service-img-wrap">
            <img class="service-img" src="https://images.unsplash.com/photo-1551218808-94e220e084d2?w=600&q=80" alt="Cooking class" loading="lazy"/>
          </div>
          <div class="service-body">
            <span class="service-icon">👨‍🍳</span>
            <h3 class="service-title">Cooking Masterclasses</h3>
            <p class="service-desc">Learn from the pros. Hands-on sessions covering techniques from sauté to soufflé — for all skill levels.</p>
            <a href="#contact" class="service-link">Join a Class →</a>
          </div>
        </div>

        <!-- Card 3 -->
        <div class="service-card fade-up">
          <div class="service-img-wrap">
            <img class="service-img" src="https://images.unsplash.com/photo-1530103862676-de8c9debad1d?w=600&q=80" alt="Private events" loading="lazy"/>
          </div>
          <div class="service-body">
            <span class="service-icon">🥂</span>
            <h3 class="service-title">Private Events & Catering</h3>
            <p class="service-desc">From intimate birthdays to large corporate gatherings — we handle every detail so you can enjoy every moment.</p>
            <a href="#contact" class="service-link">Plan Your Event →</a>
          </div>
        </div>

        <!-- Card 4 -->
        <div class="service-card fade-up">
          <div class="service-img-wrap">
            <img class="service-img" src="https://images.unsplash.com/photo-1559181567-c3190ca9959b?w=600&q=80" alt="Food delivery" loading="lazy"/>
          </div>
          <div class="service-body">
            <span class="service-icon">🚴</span>
            <h3 class="service-title">Gourmet Home Delivery</h3>
            <p class="service-desc">Signature dishes — chilled, sealed, and ready to reheat. Restaurant-quality flavour delivered to your door.</p>
            <a href="#contact" class="service-link">Order Now →</a>
          </div>
        </div>

        <!-- Card 5 -->
        <div class="service-card fade-up">
          <div class="service-img-wrap">
            <img class="service-img" src="https://images.unsplash.com/photo-1555396273-367ea4eb4db5?w=600&q=80" alt="Wine pairing" loading="lazy"/>
          </div>
          <div class="service-body">
            <span class="service-icon">🍷</span>
            <h3 class="service-title">Wine & Spirits Pairing</h3>
            <p class="service-desc">Our sommelier curates pairings that elevate your meal from memorable to magical. 200+ labels in our cellar.</p>
            <a href="#contact" class="service-link">View Wine List →</a>
          </div>
        </div>

        <!-- Card 6 -->
        <div class="service-card fade-up">
          <div class="service-img-wrap">
            <img class="service-img" src="https://images.unsplash.com/photo-1546069901-ba9599a7e63c?w=600&q=80" alt="Food subscription" loading="lazy"/>
          </div>
          <div class="service-body">
            <span class="service-icon">📦</span>
            <h3 class="service-title">Seasonal Meal Kits</h3>
            <p class="service-desc">Pre-portioned, pre-prepped weekly boxes featuring seasonal recipes and heritage ingredients. Cook like a chef, at home.</p>
            <a href="#contact" class="service-link">Subscribe →</a>
          </div>
        </div>

      </div>
    </div>
  </section>

  <!-- ===== MENU HIGHLIGHTS ===== -->
  <section id="menu" aria-labelledby="menu-title">
    <div class="container">
      <div class="menu-header fade-up">
        <span class="section-label">Taste of the Season</span>
        <h2 id="menu-title" class="section-title">Fan favourites this month</h2>
      </div>
      <div class="menu-grid">

        <div class="menu-card fade-up">
          <div class="menu-img-wrap">
            <img class="menu-img" src="https://images.unsplash.com/photo-1473093226795-af9932fe5856?w=400&q=80" alt="Truffle Pasta" loading="lazy"/>
          </div>
          <div class="menu-body">
            <div class="menu-category">Pasta</div>
            <div class="menu-name">Black Truffle Tagliatelle</div>
            <p style="font-size:.82rem;color:var(--light)">Handmade pasta with Périgord truffle & aged parmesan.</p>
            <div class="menu-footer">
              <span class="menu-price">₹1,840</span>
              <span class="menu-rating"><span>★★★★★</span> 4.9</span>
            </div>
          </div>
        </div>

        <div class="menu-card fade-up">
          <div class="menu-img-wrap">
            <img class="menu-img" src="https://images.unsplash.com/photo-1540189549336-e6e99c3679fe?w=400&q=80" alt="Buddha Bowl" loading="lazy"/>
          </div>
          <div class="menu-body">
            <div class="menu-category">Wholesome</div>
            <div class="menu-name">Heritage Grain Bowl</div>
            <p style="font-size:.82rem;color:var(--light)">Farro, roasted roots, labneh, za'atar & pomegranate.</p>
            <div class="menu-footer">
              <span class="menu-price">₹980</span>
              <span class="menu-rating"><span>★★★★★</span> 4.8</span>
            </div>
          </div>
        </div>

        <div class="menu-card fade-up">
          <div class="menu-img-wrap">
            <img class="menu-img" src="https://images.unsplash.com/photo-1565299624946-b28f40a0ae38?w=400&q=80" alt="Pizza" loading="lazy"/>
          </div>
          <div class="menu-body">
            <div class="menu-category">Wood-Fired</div>
            <div class="menu-name">Heirloom Tomato Pizza</div>
            <p style="font-size:.82rem;color:var(--light)">San Marzano base, burrata, fresh basil, sea salt.</p>
            <div class="menu-footer">
              <span class="menu-price">₹1,100</span>
              <span class="menu-rating"><span>★★★★☆</span> 4.7</span>
            </div>
          </div>
        </div>

        <div class="menu-card fade-up">
          <div class="menu-img-wrap">
            <img class="menu-img" src="https://images.unsplash.com/photo-1571091718767-18b5b1457add?w=400&q=80" alt="Burger" loading="lazy"/>
          </div>
          <div class="menu-body">
            <div class="menu-category">Signatures</div>
            <div class="menu-name">Wagyu Smash Burger</div>
            <p style="font-size:.82rem;color:var(--light)">A5 Wagyu patty, gruyère, caramelised onion, smash sauce.</p>
            <div class="menu-footer">
              <span class="menu-price">₹1,550</span>
              <span class="menu-rating"><span>★★★★★</span> 5.0</span>
            </div>
          </div>
        </div>

      </div>
      <div style="text-align:center;margin-top:48px;">
        <a href="#contact" class="btn btn-dark">View Full Menu →</a>
      </div>
    </div>
  </section>

  <!-- ===== TESTIMONIALS ===== -->
  <section id="testimonials" aria-labelledby="test-title">
    <div class="container">
      <div class="test-header fade-up">
        <span class="section-label">What Foodies Say</span>
        <h2 id="test-title" class="section-title">Loved by every kind of eater.</h2>
      </div>
      <div class="test-grid">

        <div class="test-card fade-up">
          <span class="test-quote">"</span>
          <p class="test-text">Every dish is a conversation between ingredients. The black truffle tagliatelle alone was worth the entire evening. I've eaten at Michelin-starred restaurants worldwide — SAVOR belongs in that company.</p>
          <div class="test-author">
            <img class="test-avatar" src="https://randomuser.me/api/portraits/women/44.jpg" alt="Priya S."/>
            <div>
              <div class="test-stars">★★★★★</div>
              <div class="test-name">Priya Sharma</div>
              <div class="test-role">Food Blogger, Mumbai</div>
            </div>
          </div>
        </div>

        <div class="test-card fade-up">
          <span class="test-quote">"</span>
          <p class="test-text">Hosted my company's annual dinner here. The private dining team were exceptional — attentive, creative, and utterly seamless. Our 80 guests are still talking about the dessert spread.</p>
          <div class="test-author">
            <img class="test-avatar" src="https://randomuser.me/api/portraits/men/32.jpg" alt="Rohan M."/>
            <div>
              <div class="test-stars">★★★★★</div>
              <div class="test-name">Rohan Mehta</div>
              <div class="test-role">CEO, TechVentures Bangalore</div>
            </div>
          </div>
        </div>

        <div class="test-card fade-up">
          <span class="test-quote">"</span>
          <p class="test-text">The cooking masterclass changed how I see food entirely. Chef Arya has this incredible ability to strip a recipe down to its soul, then teach you to build it back up. Truly transformative.</p>
          <div class="test-author">
            <img class="test-avatar" src="https://randomuser.me/api/portraits/women/68.jpg" alt="Ananya R."/>
            <div>
              <div class="test-stars">★★★★★</div>
              <div class="test-name">Ananya Rao</div>
              <div class="test-role">Home Cook & Foodie, Chennai</div>
            </div>
          </div>
        </div>

      </div>
    </div>
  </section>

  <!-- ===== CONTACT ===== -->
  <section id="contact" aria-labelledby="contact-title">
    <div class="container">
      <div class="contact-grid">
        <!-- Info -->
        <div class="fade-up">
          <span class="section-label">Get in Touch</span>
          <h2 id="contact-title" class="section-title">Let's make something<br/>delicious together.</h2>
          <p class="contact-intro">Whether it's booking a table, planning a private event, or just asking what's on tonight — we'd love to hear from you.</p>

          <div class="contact-detail">
            <div class="contact-icon">📍</div>
            <div class="contact-detail-text">
              <strong>Address</strong>
              <span>14 Flavour Lane, Koramangala<br/>Bangalore 560034, Karnataka</span>
            </div>
          </div>
          <div class="contact-detail">
            <div class="contact-icon">📞</div>
            <div class="contact-detail-text">
              <strong>Phone</strong>
              <span>+91 98765 43210</span>
            </div>
          </div>
          <div class="contact-detail">
            <div class="contact-icon">✉️</div>
            <div class="contact-detail-text">
              <strong>Email</strong>
              <span>hello@savorindia.com</span>
            </div>
          </div>
          <div class="contact-detail">
            <div class="contact-icon">🕐</div>
            <div class="contact-detail-text">
              <strong>Hours</strong>
              <span>Tue–Sun: 12:00 PM – 11:00 PM<br/>Monday: Closed (Private Events Only)</span>
            </div>
          </div>
        </div>

        <!-- Form -->
        <div class="contact-form fade-up" role="form" aria-label="Contact form">
          <form id="contactForm" novalidate>
            <div class="form-row">
              <div class="form-group">
                <label for="fname">First Name</label>
                <input type="text" id="fname" name="fname" placeholder="Arjun" required/>
                <span class="form-error" id="fname-err">Please enter your first name.</span>
              </div>
              <div class="form-group">
                <label for="lname">Last Name</label>
                <input type="text" id="lname" name="lname" placeholder="Patel"/>
              </div>
            </div>
            <div class="form-group">
              <label for="email">Email Address</label>
              <input type="email" id="email" name="email" placeholder="you@example.com" required/>
              <span class="form-error" id="email-err">Please enter a valid email.</span>
            </div>
            <div class="form-group">
              <label for="phone">Phone Number</label>
              <input type="tel" id="phone" name="phone" placeholder="+91 98765 00000"/>
            </div>
            <div class="form-group">
              <label for="subject">I'd like to…</label>
              <select id="subject" name="subject">
                <option value="">Select an option</option>
                <option>Book a Table</option>
                <option>Plan a Private Event</option>
                <option>Join a Cooking Class</option>
                <option>Order Meal Kits</option>
                <option>General Enquiry</option>
              </select>
            </div>
            <div class="form-group">
              <label for="message">Message</label>
              <textarea id="message" name="message" placeholder="Tell us a little more…" required></textarea>
              <span class="form-error" id="msg-err">Please enter a message.</span>
            </div>
            <button type="submit" class="btn btn-primary" style="width:100%;justify-content:center;">Send Message ✉️</button>
            <div class="form-success" id="formSuccess">
              ✅ Thank you! We'll be in touch within 24 hours.
            </div>
          </form>
        </div>
      </div>
    </div>
  </section>

  <!-- ===== LOCATION ===== -->
  <section id="location" aria-labelledby="location-title">
    <div class="container">
      <div style="text-align:center;margin-bottom:60px;" class="fade-up">
        <span class="section-label">Find Us</span>
        <h2 id="location-title" class="section-title">We're easier to find<br/>than the perfect recipe.</h2>
      </div>
      <div class="location-grid">
        <div class="location-info fade-up">
          <!-- Main Location -->
          <div class="location-card">
            <div class="location-card-top">
              <div class="loc-icon">🏠</div>
              <div>
                <div class="loc-name">SAVOR — Koramangala</div>
                <span class="loc-tag">Flagship</span>
              </div>
            </div>
            <div class="loc-address">
              14 Flavour Lane, 5th Block<br/>Koramangala, Bangalore 560034
            </div>
            <div class="hours-grid">
              <span><strong>Tue–Thu</strong></span><span>12pm – 10:30pm</span>
              <span><strong>Fri–Sat</strong></span><span>12pm – 11:30pm</span>
              <span><strong>Sunday</strong></span><span>11am – 10pm</span>
              <span><strong>Monday</strong></span><span>Private Events</span>
            </div>
          </div>
          <!-- Second Location -->
          <div class="location-card">
            <div class="location-card-top">
              <div class="loc-icon">🌿</div>
              <div>
                <div class="loc-name">SAVOR — Indiranagar</div>
                <span class="loc-tag" style="background:var(--forest)">Brunch Spot</span>
              </div>
            </div>
            <div class="loc-address">
              22 HAL Road, 12th Main<br/>Indiranagar, Bangalore 560008
            </div>
            <div class="hours-grid">
              <span><strong>Wed–Fri</strong></span><span>11am – 4pm</span>
              <span><strong>Sat–Sun</strong></span><span>9am – 5pm</span>
              <span><strong>Mon–Tue</strong></span><span>Closed</span>
            </div>
          </div>
          <a href="https://maps.google.com" target="_blank" rel="noopener noreferrer" class="btn btn-dark" style="display:block;text-align:center;">Open in Google Maps →</a>
        </div>

        <!-- Map -->
        <div class="map-embed fade-up">
          <div class="map-placeholder">
            <div class="map-pin">📍</div>
            <p>14 Flavour Lane, Koramangala</p>
            <span>Bangalore, Karnataka 560034</span>
            <a href="https://maps.google.com/?q=Koramangala+Bangalore" target="_blank" rel="noopener noreferrer" class="btn btn-primary" style="margin-top:8px;">Get Directions →</a>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- ===== FOOTER ===== -->
  <footer role="contentinfo">
    <div class="container">
      <div class="footer-grid">
        <!-- Brand -->
        <div class="footer-brand">
          <span class="logo">SAVOR</span>
          <p>A celebration of honest food, thoughtful cooking, and the joy of sharing a great meal. Made for every foodie.</p>
          <div class="footer-socials" role="list" aria-label="Social media links">
            <a href="#" class="social-btn" role="listitem" aria-label="Instagram">📸</a>
            <a href="#" class="social-btn" role="listitem" aria-label="Facebook">📘</a>
            <a href="#" class="social-btn" role="listitem" aria-label="Twitter/X">🐦</a>
            <a href="#" class="social-btn" role="listitem" aria-label="YouTube">▶️</a>
            <a href="#" class="social-btn" role="listitem" aria-label="Pinterest">📌</a>
          </div>
        </div>
        <!-- Links -->
        <div class="footer-col">
          <h4>Explore</h4>
          <ul>
            <li><a href="#home">Home</a></li>
            <li><a href="#about">About Us</a></li>
            <li><a href="#services">Services</a></li>
            <li><a href="#menu">Our Menu</a></li>
            <li><a href="#testimonials">Reviews</a></li>
          </ul>
        </div>
        <div class="footer-col">
          <h4>Services</h4>
          <ul>
            <li><a href="#services">Fine Dining</a></li>
            <li><a href="#services">Cooking Classes</a></li>
            <li><a href="#services">Private Events</a></li>
            <li><a href="#services">Home Delivery</a></li>
            <li><a href="#services">Meal Kits</a></li>
          </ul>
        </div>
        <div class="footer-col">
          <h4>Contact</h4>
          <ul>
            <li><a href="tel:+919876543210">+91 98765 43210</a></li>
            <li><a href="mailto:hello@savorindia.com">hello@savorindia.com</a></li>
            <li><a href="#location">Koramangala, Bangalore</a></li>
            <li><a href="#location">Indiranagar, Bangalore</a></li>
            <li><a href="#contact">Book a Table</a></li>
          </ul>
        </div>
      </div>
      <!-- Bottom bar -->
      <div class="footer-bottom">
        <p>© 2025 SAVOR India. All rights reserved. Made with <span>♥</span> for every foodie.</p>
        <p><a href="#" style="color:rgba(255,255,255,0.35);margin-right:20px;">Privacy Policy</a><a href="#" style="color:rgba(255,255,255,0.35);">Terms of Use</a></p>
      </div>
    </div>
  </footer>

  <!-- Scroll to Top Button -->
  <button id="scrollTop" aria-label="Scroll to top">↑</button>

  <!-- ===== JAVASCRIPT ===== -->
  <script>
    /* ---- Navbar scroll effect ---- */
    const navbar = document.getElementById('navbar');
    window.addEventListener('scroll', () => {
      if (window.scrollY > 60) navbar.classList.add('scrolled');
      else navbar.classList.remove('scrolled');
      // Scroll-to-top button
      const btn = document.getElementById('scrollTop');
      if (window.scrollY > 400) btn.classList.add('visible');
      else btn.classList.remove('visible');
    });

    /* ---- Hamburger menu toggle ---- */
    const hamburger = document.getElementById('hamburger');
    const mobileMenu = document.getElementById('mobileMenu');
    hamburger.addEventListener('click', () => {
      hamburger.classList.toggle('open');
      mobileMenu.classList.toggle('open');
      hamburger.setAttribute('aria-expanded', mobileMenu.classList.contains('open'));
    });
    // Close menu on link click
    mobileMenu.querySelectorAll('a').forEach(link => {
      link.addEventListener('click', () => {
        hamburger.classList.remove('open');
        mobileMenu.classList.remove('open');
        hamburger.setAttribute('aria-expanded', 'false');
      });
    });

    /* ---- Scroll to top ---- */
    document.getElementById('scrollTop').addEventListener('click', () => {
      window.scrollTo({ top: 0, behavior: 'smooth' });
    });

    /* ---- Intersection Observer for fade-up animations ---- */
    const observer = new IntersectionObserver((entries) => {
      entries.forEach((entry, i) => {
        if (entry.isIntersecting) {
          setTimeout(() => entry.target.classList.add('visible'), i * 80);
          observer.unobserve(entry.target);
        }
      });
    }, { threshold: 0.12 });

    document.querySelectorAll('.fade-up').forEach(el => observer.observe(el));

    /* ---- Contact form validation ---- */
    document.getElementById('contactForm').addEventListener('submit', function(e) {
      e.preventDefault();
      let valid = true;

      // First name
      const fname = document.getElementById('fname');
      const fnameErr = document.getElementById('fname-err');
      if (!fname.value.trim()) {
        fnameErr.style.display = 'block';
        fname.style.borderColor = '#ff8a7a';
        valid = false;
      } else {
        fnameErr.style.display = 'none';
        fname.style.borderColor = '';
      }

      // Email
      const email = document.getElementById('email');
      const emailErr = document.getElementById('email-err');
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      if (!emailRegex.test(email.value)) {
        emailErr.style.display = 'block';
        email.style.borderColor = '#ff8a7a';
        valid = false;
      } else {
        emailErr.style.display = 'none';
        email.style.borderColor = '';
      }

      // Message
      const message = document.getElementById('message');
      const msgErr = document.getElementById('msg-err');
      if (!message.value.trim()) {
        msgErr.style.display = 'block';
        message.style.borderColor = '#ff8a7a';
        valid = false;
      } else {
        msgErr.style.display = 'none';
        message.style.borderColor = '';
      }

      if (valid) {
        document.getElementById('formSuccess').style.display = 'block';
        this.reset();
        setTimeout(() => {
          document.getElementById('formSuccess').style.display = 'none';
        }, 5000);
      }
    });

    /* ---- Active nav link highlighting ---- */
    const sections = document.querySelectorAll('section[id]');
    const navLinks = document.querySelectorAll('.nav-links a');
    window.addEventListener('scroll', () => {
      let current = '';
      sections.forEach(sec => {
        if (window.scrollY >= sec.offsetTop - 100) current = sec.id;
      });
      navLinks.forEach(link => {
        link.style.color = '';
        if (link.getAttribute('href') === '#' + current) {
          link.style.color = 'var(--rust)';
        }
      });
    });
  </script>

</body>
</html>

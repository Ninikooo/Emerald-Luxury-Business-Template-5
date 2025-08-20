<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <meta name="color-scheme" content="dark light" />
  <title>Lux Emerald -- Multipurpose Business Template</title>
  <style>
    /* ============================
       THEME + DESIGN TOKENS
       ============================ */
    :root {
      --bg-0: #070b0a;           /* near-black */
      --bg-1: #0b1513;           /* deep green black */
      --ink-0: #eaf8f6;          /* soft white */
      --ink-dim: #b6ccc8;        
      --brand-emerald: #0e4f46;  /* dark green */
      --brand-emerald-600: #0f6b5f;
      --turquoise: #24e0d5;      /* turquoise */
      --neon-green: #39ff14;     /* neon accents */
      --neon-yellow: #d7ff00;
      --muted: rgba(255,255,255,.55);
      --glass: rgba(255,255,255,.06);
      --glass-strong: rgba(255,255,255,.12);
      --card-border: rgba(255,255,255,.14);
      --shadow: 0 10px 35px rgba(0,0,0,.45), 0 2px 8px rgba(0,0,0,.35);
      --radius-lg: 22px;
      --radius-xl: 28px;
      --radius-2xl: 36px;
      --pad: clamp(16px, 2.2vw, 28px);
      --maxw: 1200px;
      --trans-fast: .18s cubic-bezier(.2,.8,.2,1);
      --trans-slow: .6s cubic-bezier(.2,.8,.2,1);
      --grid-gap: clamp(14px, 2vw, 22px);
    }* { box-sizing: border-box; }
html, body { height: 100%; }
body {
  margin: 0; font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, "Helvetica Neue", Arial, "Apple Color Emoji", "Segoe UI Emoji";
  color: var(--ink-0); background: var(--bg-0);
  line-height: 1.55;
  overflow-x: hidden;
}

/* Animated multi-layer gradient background */
.bg {
  position: fixed; inset: -20vmax; z-index: -2;
  background:
    radial-gradient(60vmax 60vmax at 10% 10%, rgba(36,224,213,.10), transparent 70%),
    radial-gradient(70vmax 70vmax at 90% 10%, rgba(15,107,95,.25), transparent 70%),
    radial-gradient(80vmax 80vmax at 50% 110%, rgba(7,11,10,.85), rgba(7,11,10,1) 60%);
  filter: saturate(1.2);
  animation: bgMove 24s linear infinite alternate;
}
@keyframes bgMove {
  0% { transform: translate3d(0,0,0) scale(1); }
  100% { transform: translate3d(-2%, -2%, 0) scale(1.05); }
}

/* Floating neon blobs */
.blob { position: fixed; width: 42vmax; aspect-ratio: 1; inset: auto auto 5% -10%; z-index: -1; filter: blur(40px) saturate(1.3);
  background: radial-gradient(circle at 30% 30%, rgba(55,255,20,.25), transparent 60%),
              radial-gradient(circle at 70% 60%, rgba(36,224,213,.20), transparent 60%);
  border-radius: 50%; opacity: .6; animation: float 18s ease-in-out infinite;
}
.blob.b2 { inset: -10% -5% auto auto; width: 36vmax; animation-duration: 22s; opacity: .45; }
@keyframes float { 0% { transform: translateY(0) translateX(0); } 50% { transform: translateY(-3%) translateX(2%); } 100% { transform: translateY(0) translateX(0); } }

.container { width: min(100% - 2*var(--pad), var(--maxw)); margin-inline: auto; }
.stack { display: grid; gap: max(36px, 3.2vh); }

/* NAVBAR */
header { position: sticky; top: 0; z-index: 50; backdrop-filter: blur(10px); background: linear-gradient(180deg, rgba(7,11,10,.82), rgba(7,11,10,.45) 60%, transparent); border-bottom: 1px solid rgba(255,255,255,.08); }
.nav { display: flex; align-items: center; justify-content: space-between; padding: 14px var(--pad); }
.brand { display: flex; align-items: center; gap: 12px; font-weight: 800; letter-spacing: .4px; font-size: 1.05rem; }
.brand-mark { width: 36px; height: 36px; border-radius: 12px; background: conic-gradient(from 210deg, var(--turquoise), var(--neon-green), var(--brand-emerald-600), var(--turquoise)); box-shadow: 0 0 0 2px rgba(255,255,255,.08) inset, 0 10px 24px rgba(36,224,213,.12);
  position: relative; overflow: hidden; isolation: isolate; }
.brand-mark::after { content: ""; position: absolute; inset: -20% -20% auto auto; width: 60%; height: 60%; background: radial-gradient(circle at 50% 50%, rgba(255,255,255,.35), transparent 60%); filter: blur(6px); }

nav ul { display: flex; gap: 14px; align-items: center; list-style: none; margin: 0; padding: 0; }
nav a { text-decoration: none; color: var(--ink-0); opacity: .85; padding: 10px 12px; border-radius: 999px; border: 1px solid transparent; transition: border-color var(--trans-fast), background var(--trans-fast), transform var(--trans-fast); font-weight: 600; font-size: .95rem; }
nav a:hover { border-color: rgba(255,255,255,.14); background: rgba(255,255,255,.05); transform: translateY(-1px); }

.cta { background: linear-gradient(135deg, var(--turquoise), var(--neon-green)); color: #00110d; font-weight: 800; padding: 10px 14px; border-radius: 999px; box-shadow: 0 6px 26px rgba(36,224,213,.25); border: none; }
.cta:hover { filter: saturate(1.1) brightness(1.05); }
.menu { display: none; background: none; border: 1px solid rgba(255,255,255,.18); color: var(--ink-0); border-radius: 12px; padding: 8px 10px; }

/* MOBILE NAV */
@media (max-width: 920px) {
  nav ul { display: none; }
  .menu { display: grid; place-items: center; }
  .drawer { position: fixed; inset: 64px 12px auto; background: var(--bg-1); border: 1px solid rgba(255,255,255,.12); border-radius: var(--radius-xl); box-shadow: var(--shadow); padding: 10px; display: none; backdrop-filter: blur(8px); z-index: 60; }
  .drawer.open { display: block; animation: pop .18s ease-out; }
  .drawer a { display: block; padding: 12px 16px; margin: 6px; border-radius: 14px; background: rgba(255,255,255,.04); border: 1px solid rgba(255,255,255,.08); }
  @keyframes pop { from { transform: scale(.98); opacity: 0; } to { transform: scale(1); opacity: 1; } }
}

/* HERO */
.hero { padding: clamp(36px, 8vw, 96px) 0; position: relative; }
.hero .wrap { display: grid; gap: 36px; grid-template-columns: 1.1fr .9fr; align-items: center; }
@media (max-width: 980px) { .hero .wrap { grid-template-columns: 1fr; } }

h1 { font-size: clamp(2rem, 4.6vw, 3.6rem); line-height: 1.08; margin: 0 0 12px 0; letter-spacing: 0.2px; }
.lead { font-size: clamp(1rem, 1.25vw, 1.15rem); color: var(--ink-dim); max-width: 60ch; }

.actions { display: flex; flex-wrap: wrap; gap: 12px; margin-top: 18px; }
.btn { display: inline-flex; align-items: center; gap: 10px; padding: 12px 16px; border-radius: 16px; border: 1px solid var(--card-border); background: var(--glass); color: var(--ink-0); text-decoration: none; font-weight: 700; transition: transform var(--trans-fast), background var(--trans-fast); }
.btn:hover { background: var(--glass-strong); transform: translateY(-1px); }

.device { position: relative; aspect-ratio: 16/10; border-radius: var(--radius-2xl); background: linear-gradient(180deg, rgba(255,255,255,.06), rgba(255,255,255,.03)); border: 1px solid var(--card-border); box-shadow: var(--shadow); overflow: hidden; }
.device::after { content: ""; position: absolute; inset: 0; background: radial-gradient(80% 60% at 20% 10%, rgba(36,224,213,.15), transparent), radial-gradient(60% 80% at 110% 50%, rgba(57,255,20,.08), transparent); pointer-events: none; }

/* unique SVG graphic */
.mesh { position: absolute; inset: 0; opacity: .9; mix-blend-mode: screen; filter: drop-shadow(0 10px 30px rgba(36,224,213,.12)); }

/* FEATURE GRID */
.features { padding: 32px 0 8px; }
.grid { display: grid; gap: var(--grid-gap); grid-template-columns: repeat(12, 1fr); }
.col-4 { grid-column: span 4; }
.col-6 { grid-column: span 6; }
.col-12 { grid-column: span 12; }
@media (max-width: 900px) { .col-4, .col-6 { grid-column: span 12; } }

.card { background: var(--glass); border: 1px solid var(--card-border); border-radius: var(--radius-xl); padding: clamp(16px, 2vw, 22px); box-shadow: var(--shadow); position: relative; overflow: hidden; }
.card .halo { position: absolute; inset: -30% -10% auto auto; width: 150px; height: 150px; background: radial-gradient(circle at 50% 50%, rgba(215,255,0,.18), transparent 60%); filter: blur(22px); pointer-events: none; }

.icon { width: 44px; height: 44px; border-radius: 12px; display: grid; place-items: center; background: linear-gradient(135deg, rgba(36,224,213,.35), rgba(57,255,20,.22)); border: 1px solid rgba(255,255,255,.2); box-shadow: inset 0 0 0 1px rgba(0,0,0,.2); }

h2 { font-size: clamp(1.6rem, 2.8vw, 2.2rem); margin: 0 0 8px; }
h3 { font-size: 1.15rem; margin: 12px 0 6px; }
p { margin: 0; }

/* MARQUEE */
.marquee { overflow: hidden; border-radius: var(--radius-xl); border: 1px solid var(--card-border); background: rgba(255,255,255,.03); }
.marquee .track { display: flex; gap: 44px; padding: 14px; animation: scroll 24s linear infinite; }
.marquee .logo { opacity: .8; filter: grayscale(.1); white-space: nowrap; font-weight: 700; letter-spacing: .6px; }
@keyframes scroll { from { transform: translateX(0); } to { transform: translateX(-50%); } }

/* SERVICES / PRICING / TESTIMONIALS / FAQ */
.section { padding: clamp(48px, 8vw, 100px) 0; }
.section .head { display: flex; align-items: end; justify-content: space-between; gap: 18px; margin-bottom: 22px; }
.muted { color: var(--ink-dim); }

.price { font-weight: 900; font-size: clamp(1.15rem, 3vw, 1.8rem); color: var(--turquoise); }
.badge { padding: 6px 10px; border-radius: 999px; background: linear-gradient(135deg, rgba(215,255,0,.28), rgba(36,224,213,.22)); color: #03110d; font-weight: 900; letter-spacing: .4px; border: 1px solid rgba(255,255,255,.2);
}

.testimonial { display: grid; gap: 12px; }
.quote { font-size: 1.05rem; }
.avatar { width: 42px; height: 42px; border-radius: 999px; background: linear-gradient(135deg, #0f6b5f, #24e0d5); display: inline-grid; place-items: center; font-weight: 900; color: #01221d; }

/* PORTFOLIO */
.portfolio-grid { display: grid; gap: var(--grid-gap); grid-template-columns: repeat(12, 1fr); }
.tile { grid-column: span 4; aspect-ratio: 4/3; border-radius: var(--radius-2xl); overflow: hidden; border: 1px solid var(--card-border); position: relative; background: linear-gradient(145deg, rgba(36,224,213,.08), rgba(255,255,255,.03)); box-shadow: var(--shadow); }
.tile .label { position: absolute; left: 10px; top: 10px; padding: 6px 10px; border-radius: 12px; background: rgba(0,0,0,.35); border: 1px solid rgba(255,255,255,.18); backdrop-filter: blur(6px); font-weight: 700; }
.tile .shine { position: absolute; inset: 0; background: conic-gradient(from 210deg, transparent, rgba(255,255,255,.12), transparent 30%); mix-blend-mode: screen; animation: spin 8s linear infinite; }
@keyframes spin { to { transform: rotate(1turn); } }
@media (max-width: 900px) { .tile { grid-column: span 12; } }

/* BLOG PREVIEWS */
.blog-card { display: grid; grid-template-columns: 1fr 1.6fr; gap: 16px; align-items: center; }
.blog-thumb { aspect-ratio: 16/10; border-radius: 18px; background: linear-gradient(135deg, rgba(36,224,213,.22), rgba(57,255,20,.12)); border: 1px solid var(--card-border); }
@media (max-width: 800px) { .blog-card { grid-template-columns: 1fr; } }

/* CTA BAND */
.cta-band { position: relative; padding: 22px; border-radius: var(--radius-2xl); background: linear-gradient(135deg, rgba(36,224,213,.16), rgba(57,255,20,.08)); border: 1px solid var(--card-border); overflow: hidden; }
.cta-band .pulse { position: absolute; inset: -30% -10% auto auto; width: 200px; height: 200px; background: radial-gradient(circle at 50% 50%, rgba(215,255,0,.26), transparent 60%); filter: blur(24px); }

/* CONTACT */
form { display: grid; gap: 12px; }
.field { display: grid; gap: 8px; }
input, textarea, select { width: 100%; padding: 12px 14px; border-radius: 14px; border: 1px solid var(--card-border); background: rgba(255,255,255,.04); color: var(--ink-0); }
textarea { min-height: 120px; resize: vertical; }

/* FOOTER */
footer { padding: 30px 0 60px; color: var(--ink-dim); }
.foot { display: grid; gap: 16px; grid-template-columns: 1.4fr .6fr .6fr; }
@media (max-width: 900px) { .foot { grid-template-columns: 1fr; } }

/* SCROLL REVEAL */
.reveal { opacity: 0; transform: translateY(16px) scale(.99); }
.reveal.visible { opacity: 1; transform: none; transition: opacity var(--trans-slow), transform var(--trans-slow); }

/* ROUTER: page visibility */
section[data-route] { display: none; }
section[data-route].active { display: block; }

/* ACCESSIBILITY */
@media (prefers-reduced-motion: reduce) {
  .bg, .blob, .marquee .track, .tile .shine { animation: none !important; }
}

  </style>
</head>
<body>
  <div class="bg"></div>
  <div class="blob"></div>
  <div class="blob b2"></div>  <!-- NAVBAR -->  <header>
    <div class="nav container">
      <div class="brand">
        <div class="brand-mark" aria-hidden="true"></div>
        Lux Emerald
      </div>
      <nav aria-label="Primary">
        <ul>
          <li><a href="#home">Home</a></li>
          <li><a href="#services">Services</a></li>
          <li><a href="#portfolio">Portfolio</a></li>
          <li><a href="#pricing">Pricing</a></li>
          <li><a href="#blog">Blog</a></li>
          <li><a href="#contact" class="cta">Contact</a></li>
        </ul>
      </nav>
      <button class="menu" aria-label="Open menu" id="menuBtn">☰</button>
    </div>
    <div class="drawer" id="drawer" role="dialog" aria-modal="true" aria-label="Mobile Menu">
      <a href="#home">Home</a>
      <a href="#services">Services</a>
      <a href="#portfolio">Portfolio</a>
      <a href="#pricing">Pricing</a>
      <a href="#blog">Blog</a>
      <a href="#contact">Contact</a>
    </div>
  </header>  <!-- PAGES: hash router keeps everything in one file -->  <!-- HOME -->  <section class="hero container stack" data-route="home">
    <div class="wrap">
      <div>
        <span class="badge">Premium Dark × Emerald × Turquoise</span>
        <h1>Luxury-grade business template with animated gradients, glass cards & neon accents.</h1>
        <p class="lead">A multifunctional, multi-section, multi-<em>page</em> experience -- implemented in one file using a fast hash router. Rounded, partly transparent elements, and unique vector graphics throughout.</p>
        <div class="actions">
          <a class="btn" href="#pricing">View Pricing</a>
          <a class="btn" href="#portfolio">See Work</a>
          <a class="btn cta" href="#contact">Start a Project</a>
        </div>
      </div>
      <div class="device">
        <!-- Decorative mesh SVG -->
        <svg class="mesh" viewBox="0 0 600 400" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
          <defs>
            <linearGradient id="g1" x1="0" x2="1" y1="0" y2="1">
              <stop offset="0%" stop-color="rgba(36,224,213,0.65)"/>
              <stop offset="100%" stop-color="rgba(57,255,20,0.45)"/>
            </linearGradient>
          </defs>
          <g fill="none" stroke="url(#g1)" stroke-width="1.1" opacity=".9">
            <path d="M0,300 C100,280 120,220 220,220 C320,220 340,280 440,300 C540,320 560,260 600,240"/>
            <path d="M0,260 C110,240 120,180 220,180 C320,180 360,240 460,260 C560,280 560,220 600,200"/>
            <path d="M0,220 C120,200 120,140 220,140 C320,140 360,200 480,220 C560,240 560,180 600,160"/>
            <circle cx="120" cy="160" r="3"/>
            <circle cx="300" cy="210" r="3"/>
            <circle cx="520" cy="190" r="3"/>
          </g>
        </svg>
      </div>
    </div><!-- Feature cards -->
<div class="features">
  <div class="grid">
    <div class="col-4"><div class="card reveal"><div class="halo"></div><div class="icon">⚡</div><h3>Fast single-file</h3><p class="muted">Everything (HTML+CSS+JS) in one file with client-side routing for multi-page feel.</p></div></div>
    <div class="col-4"><div class="card reveal"><div class="halo"></div><div class="icon">🎨</div><h3>Signature visuals</h3><p class="muted">Animated gradients, floating neon blobs, unique SVG meshes & rounded glass cards.</p></div></div>
    <div class="col-4"><div class="card reveal"><div class="halo"></div><div class="icon">📱</div><h3>Fully responsive</h3><p class="muted">Grid-based layout adapts flawlessly from widescreen desktop to small phones.</p></div></div>
  </div>
</div>

<!-- Logo marquee -->
<div class="marquee container" aria-label="Trusted by">
  <div class="track">
    <div class="logo">AURORA</div>
    <div class="logo">NEONTIDE</div>
    <div class="logo">EMERALD CO.</div>
    <div class="logo">TURQSYS</div>
    <div class="logo">LUMINA</div>
    <div class="logo">DEEPFOREST</div>
    <div class="logo">AURORA</div>
    <div class="logo">NEONTIDE</div>
    <div class="logo">EMERALD CO.</div>
    <div class="logo">TURQSYS</div>
    <div class="logo">LUMINA</div>
    <div class="logo">DEEPFOREST</div>
  </div>
</div>

  </section>  <!-- SERVICES -->  <section class="section container stack" data-route="services">
    <div class="head">
      <h2>Services</h2>
      <span class="muted">What we can craft for your brand</span>
    </div>
    <div class="grid">
      <div class="col-6"><div class="card reveal">
        <div class="icon">🧠</div>
        <h3>Strategy & Brand</h3>
        <p class="muted">Positioning, messaging, and visual identity systems with a premium aesthetic.</p>
      </div></div>
      <div class="col-6"><div class="card reveal">
        <div class="icon">🛠️</div>
        <h3>Web Design & Build</h3>
        <p class="muted">High-performance websites with advanced interactions and accessibility built in.</p>
      </div></div>
      <div class="col-6"><div class="card reveal">
        <div class="icon">🧩</div>
        <h3>Product UI/UX</h3>
        <p class="muted">Interfaces that look luxurious and feel effortless -- desktop and mobile.</p>
      </div></div>
      <div class="col-6"><div class="card reveal">
        <div class="icon">🚀</div>
        <h3>Growth & SEO</h3>
        <p class="muted">Technical SEO, content systems, and analytics to convert attention into revenue.</p>
      </div></div>
    </div>
  </section>  <!-- PORTFOLIO -->  <section class="section container stack" data-route="portfolio">
    <div class="head">
      <h2>Portfolio</h2>
      <span class="muted">Selected work & case studies</span>
    </div>
    <div class="portfolio-grid">
      <div class="tile reveal"><span class="label">E-commerce</span><div class="shine"></div></div>
      <div class="tile reveal"><span class="label">SaaS</span><div class="shine"></div></div>
      <div class="tile reveal"><span class="label">Fintech</span><div class="shine"></div></div>
      <div class="tile reveal"><span class="label">Healthcare</span><div class="shine"></div></div>
      <div class="tile reveal"><span class="label">Education</span><div class="shine"></div></div>
      <div class="tile reveal"><span class="label">Hospitality</span><div class="shine"></div></div>
    </div>
  </section>  <!-- PRICING -->  <section class="section container stack" data-route="pricing">
    <div class="head">
      <h2>Pricing</h2>
      <span class="muted">Flexible for startups & enterprises</span>
    </div>
    <div class="grid">
      <div class="col-4"><div class="card reveal">
        <div class="badge">Starter</div>
        <h3>Launch</h3>
        <div class="price">$899</div>
        <ul class="muted">
          <li>Single-page site</li>
          <li>Basic animations</li>
          <li>SEO essentials</li>
        </ul>
        <br/>
        <a href="#contact" class="btn">Choose</a>
      </div></div>
      <div class="col-4"><div class="card reveal">
        <div class="badge">Popular</div>
        <h3>Growth</h3>
        <div class="price">$2,400</div>
        <ul class="muted">
          <li>Multi-page website</li>
          <li>Advanced animations</li>
          <li>CMS-ready structure</li>
        </ul>
        <br/>
        <a href="#contact" class="btn cta">Choose</a>
      </div></div>
      <div class="col-4"><div class="card reveal">
        <div class="badge">Enterprise</div>
        <h3>Scale</h3>
        <div class="price">Custom</div>
        <ul class="muted">
          <li>Design system</li>
          <li>Performance SLAs</li>
          <li>Dedicated support</li>
        </ul>
        <br/>
        <a href="#contact" class="btn">Contact Sales</a>
      </div></div>
    </div><div class="cta-band reveal">
  <div class="pulse"></div>
  <h3>Need a tailor‑made plan?</h3>
  <p class="muted">Tell us about your goals and we'll craft an offer that fits perfectly.</p>
  <br>
  <a href="#contact" class="btn cta">Get a custom quote</a>
</div>

  </section>  <!-- TESTIMONIALS & FAQ -->  <section class="section container stack" data-route="blog">
    <div class="head">
      <h2>Insights</h2>
      <span class="muted">Latest from the studio</span>
    </div>
    <div class="grid">
      <div class="col-12"><div class="card blog-card reveal">
        <div class="blog-thumb"></div>
        <div>
          <h3>Dark Luxury UI: Why it Converts</h3>
          <p class="muted">We explore how emeralds, turquoise, and neon accents guide attention and increase perceived value.</p>
          <br>
          <a class="btn" href="#">Read</a>
        </div>
      </div></div>
      <div class="col-12"><div class="card blog-card reveal">
        <div class="blog-thumb"></div>
        <div>
          <h3>Performance with Flair</h3>
          <p class="muted">How to combine heavy motion design with light, accessible code.</p>
          <br>
          <a class="btn" href="#">Read</a>
        </div>
      </div></div>
    </div><div class="head" style="margin-top:32px">
  <h2>What clients say</h2>
  <span class="muted">Testimonials</span>
</div>
<div class="grid">
  <div class="col-6"><div class="card testimonial reveal">
    <div class="quote">"The visuals are stunning and the site is incredibly fast. Our conversions jumped 28%."</div>
    <div class="muted"><span class="avatar">A</span> &nbsp;Alex -- E‑commerce founder</div>
  </div></div>
  <div class="col-6"><div class="card testimonial reveal">
    <div class="quote">"The team nailed luxury without sacrificing usability. Our brand finally feels premium."</div>
    <div class="muted"><span class="avatar">M</span> &nbsp;Maya -- Fintech CMO</div>
  </div></div>
</div>

<div class="head" style="margin-top:32px">
  <h2>FAQ</h2>
  <span class="muted">Answers to common questions</span>
</div>
<div class="grid">
  <div class="col-6"><div class="card reveal"><h3>Is this template really single‑file?</h3><p class="muted">Yes. All styles, scripts, and SVG graphics are embedded here. Deploy as one HTML.</p></div></div>
  <div class="col-6"><div class="card reveal"><h3>How do "pages" work?</h3><p class="muted">The hash router toggles sections like <code>#home</code>, <code>#services</code>, etc. It feels multi-page with instant transitions.</p></div></div>
</div>

  </section>  <!-- CONTACT -->  <section class="section container stack" data-route="contact">
    <div class="head">
      <h2>Contact</h2>
      <span class="muted">Tell us about your project</span>
    </div>
    <div class="grid">
      <div class="col-6">
        <div class="card reveal">
          <form id="contactForm" novalidate>
            <div class="field"><label for="name">Name</label><input id="name" name="name" required placeholder="Your name"></div>
            <div class="field"><label for="email">Email</label><input id="email" name="email" type="email" required placeholder="you@email.com"></div>
            <div class="field"><label for="budget">Budget</label>
              <select id="budget" name="budget">
                <option value="">Select…</option>
                <option>Under $1,000</option>
                <option>$1,000 – $5,000</option>
                <option>$5,000 – $20,000</option>
                <option>$20,000+</option>
              </select>
            </div>
            <div class="field"><label for="message">Message</label><textarea id="message" name="message" required placeholder="Tell us what you need…"></textarea></div>
            <button class="btn cta" type="submit">Send message</button>
          </form>
        </div>
      </div>
      <div class="col-6">
        <div class="card reveal">
          <h3>Studio</h3>
          <p class="muted">We collaborate worldwide, remotely.</p>
          <br>
          <p><strong>Email</strong><br><a class="btn" href="mailto:hello@example.com">hello@example.com</a></p>
          <br>
          <p><strong>Follow</strong></p>
          <div class="actions">
            <a class="btn" href="#">Twitter</a>
            <a class="btn" href="#">Instagram</a>
            <a class="btn" href="#">LinkedIn</a>
          </div>
        </div>
      </div>
    </div>
  </section>  <!-- FOOTER -->  <footer class="container">
    <div class="foot">
      <div>
        <div class="brand" style="margin-bottom:8px"><div class="brand-mark"></div> Lux Emerald</div>
        <div class="muted">Premium dark, emerald, and turquoise design system with neon highlights. Built for speed, elegance, and conversions.</div>
      </div>
      <div>
        <div class="muted">Pages</div>
        <a class="btn" href="#home">Home</a>
        <a class="btn" href="#services">Services</a>
        <a class="btn" href="#portfolio">Portfolio</a>
      </div>
      <div>
        <div class="muted">Legal</div>
        <a class="btn" href="#">Privacy</a>
        <a class="btn" href="#">Terms</a>
      </div>
    </div>
  </footer>  <script>
    // Simple hash router for multi-page feel
    const routes = ["home","services","portfolio","pricing","blog","contact"];
    function setRoute(hash) {
      const route = (hash || location.hash || "#home").replace('#','');
      document.querySelectorAll('section[data-route]').forEach(s => s.classList.remove('active'));
      const target = document.querySelector(`section[data-route="${route}"]`) || document.querySelector('section[data-route="home"]');
      target.classList.add('active');
      // Scroll to top on route change for better UX
      window.scrollTo({ top: 0, behavior: 'smooth' });
      // set aria-current on nav links
      document.querySelectorAll('header nav a, .drawer a').forEach(a=>{
        a.removeAttribute('aria-current');
        if(a.getAttribute('href') === `#${route}`) a.setAttribute('aria-current','page');
      });
      // Close drawer on nav
      drawer.classList.remove('open');
    }
    addEventListener('hashchange', () => setRoute(location.hash));
    addEventListener('DOMContentLoaded', () => setRoute(location.hash));

    // Mobile drawer
    const menuBtn = document.getElementById('menuBtn');
    const drawer = document.getElementById('drawer');
    menuBtn?.addEventListener('click', ()=> drawer.classList.toggle('open'));
    drawer?.addEventListener('click', e=>{ if(e.target.tagName === 'A') drawer.classList.remove('open'); });

    // IntersectionObserver for reveal animations
    const io = new IntersectionObserver((entries)=>{
      entries.forEach(e=>{ if(e.isIntersecting){ e.target.classList.add('visible'); io.unobserve(e.target); } });
    }, { threshold: .14 });
    document.querySelectorAll('.reveal').forEach(el=> io.observe(el));

    // Lightweight contact form validation (no backend)
    const form = document.getElementById('contactForm');
    form?.addEventListener('submit', (e)=>{
      e.preventDefault();
      const data = Object.fromEntries(new FormData(form));
      if(!data.name || !data.email || !data.message){
        alert('Please fill in name, email and message.');
        return;
      }
      // mailto fallback
      const body = encodeURIComponent(`${data.message}\n\nBudget: ${data.budget||'-'}\nFrom: ${data.name} <${data.email}>`);
      location.href = `mailto:hello@example.com?subject=${encodeURIComponent('Project Inquiry')}&body=${body}`;
    });
  </script></body>
</html>

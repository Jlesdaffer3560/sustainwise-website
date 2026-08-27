# SustainWise website — full source code

Live at: https://sustainwiseapp.com
Repo: https://github.com/Jlesdaffer3560/sustainwise-website

---

## index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SustainWise — Fluent in ESG, 15 minutes a day</title>
<meta name="description" content="SustainWise turns CSRD, SFDR, greenwashing rules and forced labour due diligence into short daily quizzes you'll actually remember. Free, on Android.">
<style>
  @import url('https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,400;0,9..144,500;0,9..144,600;0,9..144,700;1,9..144,500&family=Work+Sans:wght@400;500;600;700&family=Space+Mono:wght@400;700&display=swap');

  :root{
    /* Matches the SustainWise app palette (lib/theme/app_theme.dart):
       warm paper background, dark ink text, teal/tealDeep as brand green, amber as accent. */
    --bg:#fafaf7;
    --surface:#ffffff;
    --accent-soft:#e1ebe5;
    --border:#e7e5dc;
    --ink:#1d2220;
    --ink-soft:#6b7169;
    --teal:#2f6f5e;
    --teal-deep:#1e4e41;
    --amber:#b96a2e;
    --amber-deep:#9c5423;
    --amber-soft:#f3e4d3;
    --danger:#b23a2e;
    --danger-soft:#f7e4e1;
  }

  *{box-sizing:border-box;}
  html{scroll-behavior:smooth;}

  @media (prefers-reduced-motion: reduce){
    html{scroll-behavior:auto;}
    *{animation-duration:0.01ms !important; transition-duration:0.01ms !important;}
  }

  body{
    margin:0;
    background:var(--bg);
    color:var(--ink);
    font-family:'Work Sans', -apple-system, sans-serif;
    line-height:1.6;
    -webkit-font-smoothing:antialiased;
  }

  a{color:inherit;}
  img,svg{display:block;max-width:100%;}

  :focus-visible{
    outline:2px solid var(--teal-deep);
    outline-offset:3px;
    border-radius:4px;
  }

  .container{
    max-width:1140px;
    margin:0 auto;
    padding:0 28px;
  }

  h1,h2,h3{
    font-family:'Fraunces', Georgia, serif;
    font-weight:600;
    margin:0 0 18px;
    letter-spacing:-0.01em;
  }

  .eyebrow{
    font-family:'Space Mono', monospace;
    text-transform:uppercase;
    letter-spacing:0.14em;
    font-size:0.72rem;
    color:var(--teal-deep);
    margin:0 0 16px;
    display:block;
  }

  p{margin:0 0 16px;}

  .btn{
    display:inline-flex;
    align-items:center;
    gap:9px;
    padding:14px 30px;
    border-radius:999px;
    font-family:'Work Sans', sans-serif;
    font-weight:600;
    font-size:0.95rem;
    text-decoration:none;
    border:1px solid transparent;
    cursor:pointer;
    transition:transform .18s ease, box-shadow .18s ease, background .18s ease, color .18s ease, border-color .18s ease;
  }
  .btn-gold{background:var(--amber-deep); color:#fff;}
  .btn-gold:hover{background:#7f4520; transform:translateY(-2px); box-shadow:0 10px 26px rgba(156,84,35,0.32);}
  .btn-ghost{background:transparent; border-color:var(--border); color:var(--ink);}
  .btn-ghost:hover{border-color:var(--teal); color:var(--teal-deep);}
  .btn-lg{padding:17px 38px; font-size:1.05rem;}

  /* ---------- reveal on scroll ---------- */
  .reveal{opacity:0; transform:translateY(18px); transition:opacity .6s ease, transform .6s ease;}
  .reveal.is-visible{opacity:1; transform:translateY(0);}

  /* ---------- nav ---------- */
  header.site-nav{
    position:sticky; top:0; z-index:40;
    backdrop-filter:blur(10px);
    background:rgba(250,250,247,0.88);
    border-bottom:1px solid var(--border);
  }
  .nav-row{
    display:flex; align-items:center; justify-content:space-between;
    padding:16px 28px;
    max-width:1140px; margin:0 auto;
  }
  .logo{
    display:flex; align-items:center; gap:9px;
    font-family:'Fraunces', serif; font-weight:600; font-size:1.15rem;
    text-decoration:none; color:var(--ink);
  }
  .logo-mark{width:22px; height:22px; flex:none;}
  .nav-cta{
    padding:9px 20px; font-size:0.85rem;
  }

  /* ---------- hero ---------- */
  .hero{
    padding:76px 0 90px;
  }
  .hero-grid{
    display:grid;
    grid-template-columns:1.05fr 0.95fr;
    gap:56px;
    align-items:center;
  }
  .hero h1{
    font-size:clamp(2.3rem, 4.6vw, 3.7rem);
    line-height:1.06;
  }
  .hero h1 em{
    font-style:italic; font-weight:500; color:var(--amber);
  }
  .hero .lede{
    font-size:1.13rem; color:var(--ink-soft); max-width:46ch;
  }
  .hero-ctas{
    display:flex; flex-wrap:wrap; gap:14px; margin:28px 0 22px;
  }
  .hero-proof{
    font-size:0.85rem; color:var(--teal-deep);
    display:flex; align-items:center; gap:8px;
  }
  .hero-proof::before{
    content:"";
    width:6px; height:6px; border-radius:50%;
    background:var(--teal); flex:none;
  }

  /* ---------- phone / quiz demo (kept as a dark device mockup on purpose,
     for contrast against the light page — same colors as before) ---------- */
  .demo-label{
    text-align:center; font-family:'Space Mono', monospace;
    font-size:0.7rem; letter-spacing:0.12em; text-transform:uppercase;
    color:var(--teal-deep); margin-bottom:14px;
  }
  .phone-frame{
    max-width:340px; margin:0 auto;
    background:#1e4e41;
    border:1px solid rgba(255,255,255,0.18);
    border-radius:30px;
    padding:22px 20px 24px;
    box-shadow:0 30px 70px rgba(20,40,34,0.35);
  }
  .phone-notch{
    width:56px; height:5px; border-radius:4px;
    background:rgba(255,255,255,0.24);
    margin:0 auto 20px;
  }
  .quiz-tag{
    display:inline-block;
    font-family:'Space Mono', monospace;
    font-size:0.68rem; letter-spacing:0.08em; text-transform:uppercase;
    padding:5px 11px; border-radius:999px;
    margin-bottom:14px;
    background:rgba(255,255,255,0.14); color:#bfe0d3;
    transition:background .2s ease, color .2s ease;
  }
  .quiz-tag.cat-s{background:rgba(178,58,46,0.22); color:#f0b3aa;}
  .quiz-tag.cat-g{background:rgba(217,143,82,0.24); color:#f3cda0;}

  .quiz-q{
    font-family:'Fraunces', serif; font-weight:500;
    font-size:1.12rem; line-height:1.38; color:#fafaf7;
    margin-bottom:18px;
  }
  .quiz-options{
    display:flex; flex-direction:column; gap:9px; margin-bottom:6px;
  }
  .quiz-option{
    text-align:left;
    font-family:'Work Sans', sans-serif;
    font-size:0.92rem;
    color:#fafaf7;
    background:rgba(255,255,255,0.08);
    border:1px solid rgba(255,255,255,0.14);
    border-radius:12px;
    padding:11px 14px;
    cursor:pointer;
    transition:border-color .15s ease, background .15s ease;
  }
  .quiz-option:hover:not(:disabled){border-color:rgba(255,255,255,0.28);}
  .quiz-option:disabled{cursor:default;}
  .quiz-option.correct{
    background:rgba(95,169,140,0.28);
    border-color:#5fa98c; color:#d7f0e5;
  }
  .quiz-option.incorrect{
    background:rgba(178,58,46,0.24);
    border-color:#c17168;
  }
  .quiz-explanation{
    font-size:0.88rem; color:#c9d6d0;
    background:rgba(0,0,0,0.18);
    border:1px solid rgba(255,255,255,0.14);
    border-radius:10px;
    padding:12px 14px;
    margin:14px 0 0;
    display:none;
  }
  .quiz-explanation.visible{display:block;}
  .quiz-next{
    display:none;
    margin-top:14px;
    background:transparent; border:1px solid rgba(255,255,255,0.24);
    color:#f3cda0;
    font-family:'Work Sans', sans-serif; font-weight:600; font-size:0.85rem;
    padding:9px 16px; border-radius:999px; cursor:pointer;
  }
  .quiz-next.visible{display:inline-flex;}
  .quiz-next:hover{border-color:#f3cda0;}

  .quiz-progress{
    display:flex; justify-content:center; gap:7px; margin-top:20px;
  }
  .dot{width:6px; height:6px; border-radius:50%; background:rgba(255,255,255,0.24);}
  .dot.active{background:#f3cda0;}

  /* ---------- loop / stats strip ---------- */
  .loop{
    padding:70px 0;
    border-top:1px solid var(--border);
    border-bottom:1px solid var(--border);
    background:var(--accent-soft);
  }
  .loop-inner{
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:52px;
    align-items:center;
  }
  .loop h2{font-size:clamp(1.7rem,2.8vw,2.3rem);}
  .loop-copy{color:var(--ink-soft); max-width:48ch;}
  .stat-row{
    display:flex; gap:14px; flex-wrap:wrap;
  }
  .stat-card{
    flex:1; min-width:130px;
    background:var(--surface);
    border:1px solid var(--border);
    border-radius:16px;
    padding:20px 18px;
  }
  .stat-value{
    font-family:'Space Mono', monospace; font-weight:700;
    font-size:1.7rem; color:var(--amber-deep);
    display:block; margin-bottom:4px;
  }
  .stat-label{
    font-size:0.78rem; color:var(--ink-soft);
    text-transform:uppercase; letter-spacing:0.06em;
  }
  .xp-bar{
    margin-top:12px; height:6px; border-radius:4px;
    background:var(--border); overflow:hidden;
  }
  .xp-fill{height:100%; width:62%; background:var(--amber);}

  /* ---------- pillars ---------- */
  .pillars{padding:88px 0;}
  .pillars .section-head{max-width:60ch; margin-bottom:44px;}
  .pillar-grid{
    display:grid; grid-template-columns:repeat(3,1fr); gap:22px;
  }
  .pillar-card{
    background:var(--surface);
    border:1px solid var(--border);
    border-radius:18px;
    padding:28px 24px;
  }
  .pillar-mark{
    font-family:'Fraunces', serif; font-weight:700; font-size:1.9rem;
    display:inline-flex; align-items:center; justify-content:center;
    width:48px; height:48px; border-radius:12px;
    margin-bottom:18px;
  }
  .pillar-card.e .pillar-mark{background:var(--accent-soft); color:var(--teal-deep);}
  .pillar-card.s .pillar-mark{background:var(--danger-soft); color:var(--danger);}
  .pillar-card.g .pillar-mark{background:var(--amber-soft); color:var(--amber-deep);}
  .pillar-card h3{font-size:1.2rem; margin-bottom:10px;}
  .pillar-card p{color:var(--ink-soft); font-size:0.95rem; margin:0;}

  /* ---------- credibility ---------- */
  .credibility{
    padding:70px 0;
    border-top:1px solid var(--border);
  }
  .credibility-inner{max-width:62ch; margin:0 auto; text-align:center;}
  .credibility-text{font-size:1.15rem; color:var(--ink-soft); font-family:'Fraunces', serif; font-weight:400; line-height:1.55;}

  /* ---------- team cta ---------- */
  .team-cta{
    padding:70px 0;
    background:var(--accent-soft);
    border-top:1px solid var(--border);
    border-bottom:1px solid var(--border);
  }
  .team-inner{max-width:56ch; margin:0 auto; text-align:center;}
  .team-form{
    display:flex; gap:10px; margin:26px 0 12px;
    justify-content:center; flex-wrap:wrap;
  }
  .team-form input{
    flex:1; min-width:220px; max-width:320px;
    padding:14px 18px;
    border-radius:999px;
    border:1px solid var(--border);
    background:var(--surface);
    color:var(--ink);
    font-family:'Work Sans', sans-serif;
    font-size:0.95rem;
  }
  .team-form input::placeholder{color:var(--ink-soft);}
  .form-note{font-size:0.82rem; color:var(--ink-soft);}

  /* ---------- final cta ---------- */
  .final-cta{
    padding:90px 0 80px;
    text-align:center;
  }
  .final-cta h2{font-size:clamp(1.9rem,3.4vw,2.6rem); max-width:22ch; margin:0 auto 26px;}

  /* ---------- footer ---------- */
  footer{
    padding:28px 0 40px;
    border-top:1px solid var(--border);
  }
  .footer-inner{
    display:flex; flex-wrap:wrap; gap:14px;
    justify-content:space-between; align-items:center;
    font-size:0.85rem; color:var(--ink-soft);
  }
  .footer-links{display:flex; gap:20px;}
  .footer-links a{text-decoration:none; color:var(--ink-soft);}
  .footer-links a:hover{color:var(--teal-deep);}
  .inline-link{color:var(--teal-deep); text-decoration:underline; text-underline-offset:3px;}
  .inline-link:hover{color:var(--amber-deep);}

  @media (max-width:900px){
    .hero-grid{grid-template-columns:1fr; gap:48px;}
    .loop-inner{grid-template-columns:1fr;}
    .pillar-grid{grid-template-columns:1fr;}
    .hero{padding:52px 0 64px;}
  }
</style>
</head>
<body>

<header class="site-nav">
  <div class="nav-row">
    <a href="#" class="logo">
      <svg class="logo-mark" viewBox="0 0 24 24" fill="none">
        <circle cx="12" cy="12" r="10.5" stroke="#b96a2e" stroke-width="1.6"/>
        <path d="M7.5 12.3l3 3 6-6.4" stroke="#d98f52" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"/>
      </svg>
      SustainWise
    </a>
    <a href="#get-app" class="btn btn-gold nav-cta">Get the app</a>
  </div>
</header>

<section class="hero">
  <div class="container hero-grid">
    <div class="hero-text">
      <span class="eyebrow">Free · Android · ESG learning</span>
      <h1>Fluent in ESG, <em>15 minutes</em> a day.</h1>
      <p class="lede">SustainWise turns the rules most people fake their way through, CSRD, SFDR, greenwashing claims, forced labour due diligence, into short daily quizzes you'll actually remember.</p>
      <div class="hero-ctas">
        <a href="#get-app" class="btn btn-gold">Get it on Google Play</a>
        <a href="#pillars" class="btn btn-ghost">See what you'll learn</a>
      </div>
      <p class="hero-proof">Written by Jordi Lesaffer, an ESG risk consultant, not a content farm.</p>
    </div>

    <div class="hero-demo">
      <p class="demo-label">Live demo — this is the app</p>
      <div class="phone-frame">
        <div class="phone-notch"></div>
        <span class="quiz-tag" id="cardTag">Environmental · EmpCo</span>
        <p class="quiz-q" id="cardQuestion">Loading question…</p>
        <div class="quiz-options" id="cardOptions"></div>
        <p class="quiz-explanation" id="explanation"></p>
        <button type="button" id="nextBtn" class="quiz-next">Next question →</button>
        <div class="quiz-progress" id="progressDots">
          <span class="dot"></span><span class="dot"></span><span class="dot"></span>
        </div>
      </div>
    </div>
  </div>
</section>

<section class="loop reveal">
  <div class="container loop-inner">
    <div>
      <span class="eyebrow">The loop</span>
      <h2>One question a day. That's the whole habit.</h2>
      <p class="loop-copy">Miss a day and the streak resets, same as any habit worth keeping. Right answers earn XP, XP unlocks levels, and levels unlock harder questions across environmental, social and governance topics.</p>
    </div>
    <div class="stat-row">
      <div class="stat-card">
        <span class="stat-value">🔥 6</span>
        <span class="stat-label">Day streak</span>
      </div>
      <div class="stat-card">
        <span class="stat-value">★ 3</span>
        <span class="stat-label">Level</span>
      </div>
      <div class="stat-card">
        <span class="stat-value">180 XP</span>
        <span class="stat-label">To next level</span>
        <div class="xp-bar"><div class="xp-fill"></div></div>
      </div>
    </div>
  </div>
</section>

<section class="pillars reveal" id="pillars">
  <div class="container">
    <div class="section-head">
      <span class="eyebrow">What you'll actually learn</span>
      <h2>Three pillars. Every acronym lives inside one of them.</h2>
    </div>
    <div class="pillar-grid">
      <article class="pillar-card e">
        <span class="pillar-mark">E</span>
        <h3>Environmental</h3>
        <p>Climate transition plans, the EU Taxonomy, and which sustainability claims are actually allowed under EmpCo.</p>
      </article>
      <article class="pillar-card s">
        <span class="pillar-mark">S</span>
        <h3>Social</h3>
        <p>Forced labour due diligence, supply chain human rights, and what your CSRD report has to say about your own people.</p>
      </article>
      <article class="pillar-card g">
        <span class="pillar-mark">G</span>
        <h3>Governance</h3>
        <p>Double materiality, board oversight, and how ESG data actually holds up once someone checks it.</p>
      </article>
    </div>
  </div>
</section>

<section class="credibility reveal">
  <div class="container">
    <div class="credibility-inner">
      <span class="eyebrow">Who built this</span>
      <p class="credibility-text">SustainWise comes out of <a href="https://www.novarisq.com" target="_blank" rel="noopener noreferrer" class="inline-link">NOVARISQ Consulting</a>, an ESG and reputational risk consultancy based in Brussels. The questions inside it are close cousins of the ones we use to stress-test real company claims, not trivia written to fill an app.</p>
    </div>
  </div>
</section>

<section class="team-cta reveal" id="team">
  <div class="container">
    <div class="team-inner">
      <span class="eyebrow">For organisations</span>
      <h2>Bringing this to your team?</h2>
      <p>If your compliance, marketing or sustainability team needs a shared baseline in ESG literacy, get in touch — we're exploring what a team version could look like.</p>
      <form class="team-form" id="waitlistForm" action="https://formspree.io/f/mzebpqrn" method="POST">
        <input type="email" name="email" placeholder="you@company.com" aria-label="Work email" required>
        <input type="hidden" name="_subject" value="New SustainWise waitlist signup">
        <button type="submit" class="btn btn-gold">Notify me</button>
      </form>
      <p class="form-note" id="waitlistStatus" role="status" aria-live="polite"></p>
    </div>
  </div>
</section>

<section class="final-cta reveal" id="get-app">
  <div class="container">
    <h2>15 minutes today. Fluent in weeks, not years.</h2>
    <a href="#" class="btn btn-gold btn-lg">Get it on Google Play</a>
    <p class="form-note" style="margin-top:16px;">Free. No account needed to start.</p>
  </div>
</section>

<footer>
  <div class="container footer-inner">
    <span>© 2026 SustainWise — by <a href="https://www.novarisq.com" target="_blank" rel="noopener noreferrer" class="inline-link">NOVARISQ Consulting</a></span>
    <nav class="footer-links">
      <a href="privacy-policy.html">Privacy policy</a>
      <a href="mailto:jordi.lesaffer@novarisq.com">jordi.lesaffer@novarisq.com</a>
    </nav>
  </div>
</footer>

<script>
  const quizData = [
    {
      tag: "Environmental · EmpCo",
      cat: "e",
      question: "Which of these claims is automatically banned under the EU's Empowering Consumers Directive (EmpCo), regardless of whether it's true?",
      options: [
        { text: "Made with 30% recycled plastic", correct: false },
        { text: "Climate neutral by 2050, verified annually", correct: false },
        { text: "Eco-friendly", correct: true },
        { text: "Carbon offset included, certificate attached", correct: false }
      ],
      explanation: "A bare claim like “eco-friendly” with no substantiation is banned outright under EmpCo's blacklist, regardless of whether it happens to be true."
    },
    {
      tag: "Governance · CSRD",
      cat: "g",
      question: "What does “double materiality” actually require a company to report?",
      options: [
        { text: "Financial risk only", correct: false },
        { text: "How sustainability issues affect the company, and how the company affects people and the planet", correct: true },
        { text: "Two separate audited financial statements", correct: false },
        { text: "A report every six months instead of yearly", correct: false }
      ],
      explanation: "Double materiality runs both directions: risk TO the business, and impact FROM the business. Most reporting gaps come from only covering one side."
    },
    {
      tag: "Social · Forced Labour Regulation",
      cat: "s",
      question: "A supply chain audit turns up credible indicators of forced labour. Under the EU Forced Labour Regulation, what can happen to the product?",
      options: [
        { text: "Nothing, it's a labour law issue, not a trade one", correct: false },
        { text: "It can be withdrawn from the EU market, seized at the border, or ordered destroyed", correct: true },
        { text: "Only a formal warning letter is sent", correct: false },
        { text: "It requires a UN Security Council resolution first", correct: false }
      ],
      explanation: "Once a final decision is issued, products made with forced labour can be pulled from the EU market entirely, including seizure at the border."
    }
  ];

  let current = 0;

  const tagEl = document.getElementById('cardTag');
  const questionEl = document.getElementById('cardQuestion');
  const optionsEl = document.getElementById('cardOptions');
  const explanationEl = document.getElementById('explanation');
  const nextBtn = document.getElementById('nextBtn');
  const dots = document.querySelectorAll('#progressDots .dot');

  function renderQuestion(){
    const q = quizData[current];

    tagEl.textContent = q.tag;
    tagEl.className = 'quiz-tag' + (q.cat === 's' ? ' cat-s' : q.cat === 'g' ? ' cat-g' : '');
    questionEl.textContent = q.question;

    optionsEl.innerHTML = '';
    q.options.forEach((opt, i) => {
      const btn = document.createElement('button');
      btn.type = 'button';
      btn.className = 'quiz-option';
      btn.textContent = opt.text;
      btn.addEventListener('click', () => selectOption(i));
      optionsEl.appendChild(btn);
    });

    explanationEl.textContent = '';
    explanationEl.classList.remove('visible');
    nextBtn.classList.remove('visible');

    dots.forEach((d, i) => d.classList.toggle('active', i === current));
  }

  function selectOption(i){
    const q = quizData[current];
    const buttons = optionsEl.querySelectorAll('.quiz-option');
    buttons.forEach((b, idx) => {
      b.disabled = true;
      if (q.options[idx].correct) b.classList.add('correct');
      else if (idx === i) b.classList.add('incorrect');
    });
    explanationEl.textContent = q.explanation;
    explanationEl.classList.add('visible');
    nextBtn.classList.add('visible');
  }

  nextBtn.addEventListener('click', () => {
    current = (current + 1) % quizData.length;
    renderQuestion();
  });

  renderQuestion();

  // waitlist form (Formspree)
  const waitlistForm = document.getElementById('waitlistForm');
  const waitlistStatus = document.getElementById('waitlistStatus');
  if (waitlistForm) {
    waitlistForm.addEventListener('submit', async (e) => {
      e.preventDefault();
      const submitBtn = waitlistForm.querySelector('button[type="submit"]');
      submitBtn.disabled = true;
      waitlistStatus.textContent = 'Sending…';
      try {
        const response = await fetch(waitlistForm.action, {
          method: 'POST',
          body: new FormData(waitlistForm),
          headers: { 'Accept': 'application/json' }
        });
        if (response.ok) {
          waitlistForm.reset();
          waitlistStatus.textContent = "Thanks — we'll be in touch.";
        } else {
          waitlistStatus.textContent = 'Something went wrong. Please try again.';
          submitBtn.disabled = false;
        }
      } catch (err) {
        waitlistStatus.textContent = 'Something went wrong. Please try again.';
        submitBtn.disabled = false;
      }
    });
  }

  // scroll reveal
  const prefersReduced = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
  const revealEls = document.querySelectorAll('.reveal');
  if (prefersReduced || !('IntersectionObserver' in window)) {
    revealEls.forEach(el => el.classList.add('is-visible'));
  } else {
    const io = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add('is-visible');
          io.unobserve(entry.target);
        }
      });
    }, { threshold: 0.15 });
    revealEls.forEach(el => io.observe(el));
  }
</script>

</body>
</html>
```

---

## privacy-policy.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Privacy Policy — SustainWise</title>
<meta name="description" content="Privacy policy for SustainWise, the ESG learning app by NOVARISQ Consulting.">
<style>
  @import url('https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,400;0,9..144,600;1,9..144,500&family=Work+Sans:wght@400;500;600;700&family=Space+Mono:wght@400;700&display=swap');

  :root{
    --ink:#12261f;
    --ink-2:#1e4e41;
    --paper:#fafaf7;
    --paper-dim:#bfc4c0;
    --gold:#b96a2e;
    --gold-soft:#d98f52;
    --line:rgba(250,250,247,0.14);
    --line-strong:rgba(250,250,247,0.24);
  }

  *{box-sizing:border-box;}

  body{
    margin:0;
    background:var(--ink);
    color:var(--paper);
    font-family:'Work Sans', -apple-system, sans-serif;
    line-height:1.7;
    -webkit-font-smoothing:antialiased;
  }

  a{color:var(--gold-soft);}
  a:hover{color:var(--gold);}

  .container{
    max-width:760px;
    margin:0 auto;
    padding:0 28px;
  }

  header.site-nav{
    padding:16px 0;
    border-bottom:1px solid var(--line);
  }
  .logo{
    display:flex; align-items:center; gap:9px;
    font-family:'Fraunces', serif; font-weight:600; font-size:1.15rem;
    text-decoration:none; color:var(--paper);
  }
  .logo-mark{width:22px; height:22px; flex:none;}

  main{padding:56px 0 72px;}

  h1,h2{
    font-family:'Fraunces', Georgia, serif;
    font-weight:600;
    letter-spacing:-0.01em;
  }
  h1{font-size:clamp(1.8rem,3.4vw,2.4rem); margin:0 0 6px;}
  .updated{
    font-family:'Space Mono', monospace;
    font-size:0.75rem; letter-spacing:0.08em; text-transform:uppercase;
    color:var(--gold); margin:0 0 40px; display:block;
  }
  h2{font-size:1.2rem; margin:36px 0 12px;}
  p, li{color:var(--paper-dim); font-size:0.98rem;}
  ul{padding-left:20px;}

  footer{
    padding:24px 0 40px;
    border-top:1px solid var(--line);
    font-size:0.85rem; color:var(--paper-dim);
  }
</style>
</head>
<body>

<header class="site-nav">
  <div class="container">
    <a href="index.html" class="logo">
      <svg class="logo-mark" viewBox="0 0 24 24" fill="none">
        <circle cx="12" cy="12" r="10.5" stroke="#b96a2e" stroke-width="1.6"/>
        <path d="M7.5 12.3l3 3 6-6.4" stroke="#d98f52" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"/>
      </svg>
      SustainWise
    </a>
  </div>
</header>

<main class="container">
  <h1>Privacy Policy</h1>
  <span class="updated">Last updated: 27 August 2026</span>

  <p>SustainWise is developed by NOVARISQ Consulting, based in Brussels, Belgium. This page explains what happens to your data when you visit this website.</p>

  <h2>What this site collects</h2>
  <p>This is a static marketing page for the SustainWise app. It does not use cookies, analytics, or tracking scripts.</p>
  <p>The only data you can submit is your email address, through the "Notify me" waitlist form. If and when that form is connected to a mailing list, submitted addresses are used solely to notify you about the SustainWise launch and, if relevant, the team version. We do not sell or share your email address with third parties.</p>

  <h2>Third-party services</h2>
  <p>This site loads web fonts from Google Fonts (fonts.googleapis.com and fonts.gstatic.com). Loading a font causes your browser to make a request to Google's servers, which may log your IP address. See <a href="https://policies.google.com/privacy" target="_blank" rel="noopener noreferrer">Google's privacy policy</a> for details.</p>

  <h2>Your rights</h2>
  <p>Under the EU General Data Protection Regulation (GDPR), you can ask to access, correct, or delete any personal data we hold about you (such as a waitlist email address). To do so, contact us at <a href="mailto:jordi.lesaffer@novarisq.com">jordi.lesaffer@novarisq.com</a>.</p>

  <h2>Changes to this policy</h2>
  <p>We may update this policy as the app and website evolve. Check back here for the latest version.</p>
</main>

<footer>
  <div class="container">
    © 2026 SustainWise — by <a href="https://www.novarisq.com" target="_blank" rel="noopener noreferrer">NOVARISQ Consulting</a>
  </div>
</footer>

</body>
</html>
```

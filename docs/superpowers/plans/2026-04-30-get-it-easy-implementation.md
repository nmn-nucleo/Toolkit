# Get It Easy — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build the Get It Easy site as a single index.html file with 9 tabbed pages, interactive quiz, cost calculator, and all content from the 9 markdown source files.

**Architecture:** Single HTML file (index.html) with all CSS in `<style>`, all JS in `<script>`, zero external dependencies except Google Fonts. Tab-based SPA using hash routing. Content sourced from 9 markdown files in the project root.

**Tech Stack:** HTML5, CSS3 (custom properties, grid, flexbox, clamp), Vanilla JS (IntersectionObserver, localStorage, Clipboard API, Blob/URL), Google Fonts (Syne, DM Sans, JetBrains Mono).

**Source content:** Each aba-N-*.md file in the project root contains the full content and implementation notes for that tab.

---

## Task 1: HTML Head + CSS Design Tokens + Reset

**Files:**
- Create: `index.html`

- [ ] **Step 1: Create index.html with head section**

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Get It Easy — Desenvolva como uma Big Tech estando solo</title>
<meta name="description" content="Metodo + comunidade + personalizacao em portugues para operar agentes de IA. Agnostico de ferramenta.">
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;500;700;800&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;1,9..40,400&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
/* ========== RESET ========== */
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:smooth}
body{-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale}
img,svg{display:block;max-width:100%}
button{font:inherit;cursor:pointer}
a{text-decoration:none}
</style>
</head>
<body>
</body>
</html>
```

- [ ] **Step 2: Add all CSS custom properties (design tokens)**

Add inside the `<style>` tag, after the reset. Include ALL tokens from the spec: backgrounds (bg0-bg4), text (t1-t4), ouro accent (au, au1, au3, aubg), 5 tool colors (gsd, gsp, spc, sup, opc) with bg/border variants, 2 harness colors (cc, cdx) with bg/border variants, semantic (err, ok, warn), borders (b1-b3), fonts (f-display, f-body, f-mono), type scale (t-xs through t-4xl plus fluid variants), spacing (s1-s12), border radii (r-sm through r-xl), animation (ease, dur-fast, dur-base, dur-slow).

Full token block from spec — copy the `:root` blocks from the design spec sections "Mantidas do original" and "Novas (harnesses)" verbatim into the CSS.

- [ ] **Step 3: Add body base styles**

```css
body{
  font-family:var(--f-body);
  font-size:var(--t-b);
  color:var(--t2);
  background:var(--bg1);
  line-height:1.7;
  overflow-x:hidden;
}
```

- [ ] **Step 4: Open in browser, verify dark background and font loads**

Open `index.html` directly in browser. Should see blank dark page (#0e0f14). Check DevTools > Network that Google Fonts loaded.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: index.html skeleton with CSS tokens and reset"
```

---

## Task 2: Component CSS Classes

**Files:**
- Modify: `index.html` (inside `<style>`)

All reusable component styles. These are carried over from the original site design system.

- [ ] **Step 1: Add layout wrappers**

```css
.W{max-width:1280px;margin:0 auto;padding:var(--s9) var(--s6)}
.W2{max-width:860px;margin:0 auto;padding:var(--s9) var(--s6)}
.W3{max-width:680px;margin:0 auto;padding:var(--s9) var(--s6)}
```

- [ ] **Step 2: Add typography classes**

```css
.ey{font-family:var(--f-mono);font-size:var(--t-xs);text-transform:uppercase;letter-spacing:.14em;color:var(--au);margin-bottom:var(--s4)}
.DH{font-family:var(--f-display);font-weight:800;font-size:var(--t-4xl-fluid);letter-spacing:-.04em;color:var(--t1);line-height:1.08;margin-bottom:var(--s5)}
.DH em{color:var(--au);font-style:normal}
.sh{font-family:var(--f-display);font-weight:700;font-size:var(--t-lg);letter-spacing:-.03em;color:var(--t1);margin-bottom:var(--s3)}
.ss{font-size:var(--t-sm);color:var(--t3);margin-bottom:var(--s5)}
.dl{font-size:var(--t-b);color:var(--t2);line-height:1.7;max-width:520px;margin-bottom:var(--s6)}
```

- [ ] **Step 3: Add card classes**

```css
.card{background:var(--bg3);border:1px solid var(--b1);border-radius:var(--r-lg);padding:var(--s5);transition:border-color var(--dur-base),background var(--dur-base)}
.card:hover{border-color:var(--b2);background:var(--bg4)}
```

- [ ] **Step 4: Add code block classes**

```css
.code{background:var(--bg0);border:1px solid var(--b1);border-radius:var(--r-lg);padding:var(--s5) var(--s6);font-family:var(--f-mono);font-size:12px;line-height:1.9;overflow-x:auto;position:relative;white-space:pre}
.cm{color:#4a5568}.cc{color:#d4d0c8}.ch{color:var(--au1)}.cg{color:#7fdfb8}.cp{color:#a5b4fc}.cr{color:#f09595}
.cpbtn{position:absolute;top:var(--s3);right:var(--s3);background:var(--bg3);border:1px solid var(--b2);border-radius:var(--r-sm);color:var(--t3);font-family:var(--f-mono);font-size:var(--t-xs);padding:2px 10px;cursor:pointer;transition:all var(--dur-base)}
.cpbtn:hover{color:var(--t1);border-color:var(--b3)}
```

- [ ] **Step 5: Add grid classes**

```css
.g2{display:grid;grid-template-columns:1fr 1fr;gap:var(--s4)}
.g3{display:grid;grid-template-columns:repeat(3,1fr);gap:var(--s4)}
.g4{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:var(--s3)}
```

- [ ] **Step 6: Add FAQ accordion classes**

```css
.faq{display:flex;flex-direction:column;gap:2px}
.fi{border:1px solid var(--b1);border-radius:var(--r-md);overflow:hidden}
.fq{width:100%;background:var(--bg3);border:none;padding:var(--s4);color:var(--t1);font-size:var(--t-b);text-align:left;display:flex;justify-content:space-between;align-items:center;cursor:pointer;transition:background var(--dur-base)}
.fq:hover{background:var(--bg4)}
.ficon{color:var(--au);transition:transform var(--dur-base)}
.fa{max-height:0;overflow:hidden;padding:0 var(--s4);color:var(--t2);font-size:var(--t-sm);line-height:1.7;transition:max-height var(--dur-slow),padding var(--dur-slow)}
.fi.open .fa{max-height:600px;padding:0 var(--s4) var(--s4)}
.fi.open .ficon{transform:rotate(45deg)}
```

- [ ] **Step 7: Add badge classes**

```css
.badge{font-family:var(--f-mono);font-size:var(--t-xs);padding:2px 8px;border-radius:4px;letter-spacing:.02em}
.b-req{background:var(--ok-bg);color:var(--ok);border:1px solid var(--ok-b)}
.b-opt{background:var(--opc-bg);color:var(--opc);border:1px solid var(--opc-b)}
.b-ui{background:var(--sup-bg);color:var(--sup);border:1px solid var(--sup-b)}
.b-danger{background:var(--err-bg);color:var(--err);border:1px solid var(--err-b)}
.b-new{background:var(--aubg);color:var(--au);border:1px solid rgba(217,168,50,.22)}
```

- [ ] **Step 8: Add comparison, flow, scenario, table classes**

```css
/* Comparison */
.cmp{display:grid;grid-template-columns:1fr 1fr;gap:var(--s4)}
.cmp-bad{background:var(--err-bg);border:1px solid var(--err-b);border-radius:var(--r-md);padding:var(--s4)}
.cmp-good{background:var(--ok-bg);border:1px solid var(--ok-b);border-radius:var(--r-md);padding:var(--s4)}
.cmp-h{font-family:var(--f-mono);font-size:var(--t-xs);text-transform:uppercase;letter-spacing:.1em;margin-bottom:var(--s3)}
.cmp-bad .cmp-h{color:var(--err)}
.cmp-good .cmp-h{color:var(--ok)}
.cmp-b{font-size:var(--t-sm);color:var(--t2);line-height:1.6}

/* Flow */
.flow{display:flex;align-items:center;gap:var(--s2);flex-wrap:wrap}
.fb{padding:var(--s2) var(--s4);border:1px solid var(--b2);border-radius:var(--r-sm);font-family:var(--f-mono);font-size:var(--t-xs)}
.fa2{color:var(--t4);font-size:var(--t-sm)}

/* Tables */
table.mt{width:100%;border-collapse:collapse;font-size:var(--t-sm)}
table.mt th{text-align:left;padding:var(--s3) var(--s4);color:var(--t3);border-bottom:1px solid var(--b2);font-family:var(--f-mono);font-weight:500}
table.mt td{padding:var(--s3) var(--s4);border-bottom:1px solid var(--b1);color:var(--t2)}
.ck{color:var(--ok)}.cx{opacity:.2}.co{color:var(--warn)}

/* Steps */
.steps{display:flex;flex-direction:column;gap:var(--s4)}
.step{display:flex;gap:var(--s4);align-items:flex-start}
.snum{width:32px;height:32px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-family:var(--f-mono);font-size:var(--t-sm);font-weight:500;flex-shrink:0}
.stool{font-family:var(--f-mono);font-size:var(--t-sm);font-weight:500;margin-bottom:2px}
.sdesc{font-size:var(--t-sm);color:var(--t2)}
.scmd{font-family:var(--f-mono);font-size:var(--t-xs);color:var(--au1);margin-top:4px}
```

- [ ] **Step 9: Add scroll reveal + page animation**

```css
.reveal{opacity:0;transform:translateY(16px);transition:opacity var(--dur-slow) var(--ease),transform var(--dur-slow) var(--ease)}
.reveal.visible{opacity:1;transform:none}
.page{display:none}
.page.active{display:block;animation:fadeUp 220ms var(--ease) both}
@keyframes fadeUp{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:none}}
.sec-spacer{height:var(--s8)}
.sec-spacer-sm{height:var(--s6)}
.div{height:1px;background:var(--b1);margin:var(--s7) 0}
```

- [ ] **Step 10: Add responsive breakpoints**

```css
@media(max-width:768px){
  .g2,.g3,.cmp{grid-template-columns:1fr}
  .W,.W2,.W3{padding:var(--s7) var(--s4)}
  .DH{font-size:var(--t-2xl-fluid)}
}
@media(max-width:480px){
  .g4{grid-template-columns:1fr}
}
@media(prefers-reduced-motion:reduce){
  .reveal{opacity:1;transform:none;transition:none}
  .page.active{animation:none}
}
```

- [ ] **Step 11: Commit**

```bash
git add index.html
git commit -m "feat: add all component CSS classes"
```

---

## Task 3: Header + Navigation (9 tabs grouped with icons)

**Files:**
- Modify: `index.html` (add header HTML + nav CSS inside `<style>`, structure inside `<body>`)

- [ ] **Step 1: Add header/nav CSS**

```css
/* ========== HEADER ========== */
header{position:sticky;top:0;z-index:100;height:50px;background:rgba(14,15,20,.92);backdrop-filter:blur(20px);border-bottom:1px solid var(--b1);display:flex;align-items:center;padding:0 var(--s4)}
.logo{font-family:var(--f-display);font-weight:800;font-size:var(--t-md);color:var(--t1);margin-right:var(--s5);white-space:nowrap;cursor:pointer}
.logo span{color:var(--au)}
nav{display:flex;align-items:center;gap:0;overflow-x:auto;scrollbar-width:none;flex:1}
nav::-webkit-scrollbar{display:none}
.nav-sep{width:1px;height:20px;background:rgba(255,255,255,.06);margin:0 var(--s2);flex-shrink:0}
.nb{background:none;border:1px solid transparent;border-radius:var(--r-sm);color:var(--t3);font-family:var(--f-body);font-size:var(--t-sm);padding:6px 12px;white-space:nowrap;transition:all var(--dur-base);display:flex;align-items:center;gap:5px}
.nb:hover{background:var(--bg3);color:var(--t1)}
.nb.active{background:var(--au);color:var(--bg0);font-weight:500}
.nb .ico{font-size:11px;opacity:.7}
.nb.active .ico{opacity:1}
```

- [ ] **Step 2: Add skip link for accessibility**

Add as first child of `<body>`:
```html
<a href="#main" class="skip" style="position:absolute;left:-9999px;top:auto;width:1px;height:1px;overflow:hidden;z-index:200;background:var(--au);color:var(--bg0);padding:8px 16px;font-size:14px;border-radius:0 0 8px 0" onfocus="this.style.cssText='position:fixed;left:0;top:0;z-index:200;background:var(--au);color:var(--bg0);padding:8px 16px;font-size:14px;border-radius:0 0 8px 0'" onblur="this.style.cssText='position:absolute;left:-9999px'">Pular para conteudo</a>
```

- [ ] **Step 3: Add header HTML**

```html
<header>
  <div class="logo" onclick="pg('comece',document.querySelector('[data-tab=comece]'))">Get It <span>Easy</span></div>
  <nav role="tablist" aria-label="Abas do toolkit">
    <!-- Fundacao -->
    <button class="nb active" role="tab" aria-selected="true" data-tab="comece" onclick="pg('comece',this)"><span class="ico">▶</span> Comece aqui</button>
    <button class="nb" role="tab" aria-selected="false" data-tab="metodo" onclick="pg('metodo',this)"><span class="ico">◇</span> O Metodo</button>
    <button class="nb" role="tab" aria-selected="false" data-tab="oficio" onclick="pg('oficio',this)"><span class="ico">✦</span> Oficio</button>
    <div class="nav-sep"></div>
    <!-- Stack -->
    <button class="nb" role="tab" aria-selected="false" data-tab="stack" onclick="pg('stack',this)"><span class="ico">⚡</span> Stack</button>
    <button class="nb" role="tab" aria-selected="false" data-tab="skills" onclick="pg('skills',this)"><span class="ico">⚙</span> Skills</button>
    <button class="nb" role="tab" aria-selected="false" data-tab="avancado" onclick="pg('avancado',this)"><span class="ico">◆</span> Avancado</button>
    <div class="nav-sep"></div>
    <!-- Personalizacao -->
    <button class="nb" role="tab" aria-selected="false" data-tab="setup" onclick="pg('setup',this)"><span class="ico">☰</span> Setup</button>
    <button class="nb" role="tab" aria-selected="false" data-tab="cola" onclick="pg('cola',this)"><span class="ico">⌘</span> Cola & Dicas</button>
    <button class="nb" role="tab" aria-selected="false" data-tab="custos" onclick="pg('custos',this)"><span class="ico">$</span> Custos</button>
  </nav>
</header>
```

- [ ] **Step 4: Add main container with 9 empty page divs**

```html
<main id="main">
  <div id="page-comece" class="page active" role="tabpanel"></div>
  <div id="page-metodo" class="page" role="tabpanel"></div>
  <div id="page-oficio" class="page" role="tabpanel"></div>
  <div id="page-stack" class="page" role="tabpanel"></div>
  <div id="page-skills" class="page" role="tabpanel"></div>
  <div id="page-avancado" class="page" role="tabpanel"></div>
  <div id="page-setup" class="page" role="tabpanel"></div>
  <div id="page-cola" class="page" role="tabpanel"></div>
  <div id="page-custos" class="page" role="tabpanel"></div>
</main>
```

- [ ] **Step 5: Add navigation JS + hash routing**

Add before `</body>`:

```html
<script>
/* ========== NAVIGATION ========== */
function pg(id,btn){
  document.querySelectorAll('.page').forEach(function(p){p.classList.remove('active')});
  document.querySelectorAll('.nb').forEach(function(b){b.classList.remove('active');b.setAttribute('aria-selected','false')});
  document.getElementById('page-'+id).classList.add('active');
  btn.classList.add('active');btn.setAttribute('aria-selected','true');
  window.scrollTo(0,0);
  location.hash=id;
}

/* Arrow key nav for tablist */
document.querySelectorAll('[role="tablist"]').forEach(function(tl){
  tl.addEventListener('keydown',function(e){
    if(e.key!=='ArrowLeft'&&e.key!=='ArrowRight')return;
    var tabs=Array.from(tl.querySelectorAll('[role="tab"]'));
    var idx=tabs.indexOf(document.activeElement);
    if(idx<0)return;
    e.preventDefault();
    if(e.key==='ArrowRight')idx=(idx+1)%tabs.length;
    else idx=(idx-1+tabs.length)%tabs.length;
    tabs[idx].focus();tabs[idx].click();
  });
});

/* Hash routing */
window.addEventListener('hashchange',function(){
  var h=location.hash.replace('#','');
  var btn=document.querySelector('[data-tab="'+h+'"]');
  if(btn&&!btn.classList.contains('active'))pg(h,btn);
});
(function(){
  var h=location.hash.replace('#','');
  if(h){var btn=document.querySelector('[data-tab="'+h+'"]');if(btn)pg(h,btn);}
})();
</script>
```

- [ ] **Step 6: Verify in browser**

Open index.html. Should see dark page with sticky header, 9 tabs with icons grouped by separators. Clicking tabs should switch (empty) pages. Hash should update in URL. Arrow keys should navigate between tabs.

- [ ] **Step 7: Commit**

```bash
git add index.html
git commit -m "feat: header with 9 grouped tabs, hash routing, keyboard nav"
```

---

## Task 4: Hero Section (Aba 1 — above the fold)

**Files:**
- Modify: `index.html` (add hero HTML inside `#page-comece`, add hero-specific CSS)

- [ ] **Step 1: Add hero CSS (orbs, stats animation)**

Add to `<style>`:

```css
/* ========== HERO ========== */
.hero{min-height:100vh;display:flex;flex-direction:column;align-items:center;justify-content:center;text-align:center;position:relative;overflow:hidden;padding:var(--s9) var(--s6)}
.hero-orb{position:absolute;border-radius:50%;pointer-events:none}
.hero-orb-cc{top:-10%;right:-5%;width:500px;height:500px;background:radial-gradient(circle,rgba(212,119,92,.10),transparent 60%)}
.hero-orb-cdx{bottom:-10%;left:-5%;width:400px;height:400px;background:radial-gradient(circle,rgba(70,181,201,.08),transparent 60%)}
.hero-orb-au{top:35%;left:50%;transform:translate(-50%,-50%);width:600px;height:300px;background:radial-gradient(ellipse,rgba(217,168,50,.06),transparent 70%)}
.hero-content{position:relative;z-index:1;max-width:700px}
.hero .DH{margin-bottom:var(--s4)}
.hero-lead{font-size:var(--t-b);color:var(--t2);max-width:520px;margin:0 auto var(--s6);line-height:1.7}
.hero-cta{display:inline-block;padding:12px 32px;background:var(--au);color:var(--bg0);border-radius:var(--r-md);font-family:var(--f-body);font-size:var(--t-b);font-weight:600;transition:background var(--dur-base);border:none;cursor:pointer}
.hero-cta:hover{background:var(--au1)}
.hero-proof{font-size:var(--t-sm);color:var(--t3);margin-top:var(--s5);max-width:480px;margin-left:auto;margin-right:auto}
.hero-stats{display:flex;gap:var(--s6);justify-content:center;margin-top:var(--s7);flex-wrap:wrap}
.hero-stat{text-align:center}
.hero-stat-num{font-family:var(--f-mono);font-size:var(--t-xl);font-weight:700;color:var(--au)}
.hero-stat-label{font-size:var(--t-xs);color:var(--t3);margin-top:2px}
@media(max-width:768px){
  .hero{min-height:auto;padding:var(--s8) var(--s4)}
  .hero-stats{gap:var(--s4)}
}
```

- [ ] **Step 2: Add hero HTML inside #page-comece**

```html
<div class="hero">
  <div class="hero-orb hero-orb-cc"></div>
  <div class="hero-orb hero-orb-cdx"></div>
  <div class="hero-orb hero-orb-au"></div>
  <div class="hero-content">
    <div class="ey">Metodo + comunidade + personalizacao em portugues</div>
    <h1 class="DH">Desenvolva como uma<br><em>Big Tech</em> estando solo</h1>
    <p class="hero-lead">Em 2026 o problema nao e escolher entre Claude Code, Codex ou Cursor. O problema e que ninguem te ensinou a pensar com agentes de IA.</p>
    <button class="hero-cta" onclick="pg('setup',document.querySelector('[data-tab=setup]'))">Faco o quiz &rarr;</button>
    <p class="hero-proof">Construido em portugues, testado com clientes reais, agnostico de ferramenta.</p>
    <div class="hero-stats">
      <div class="hero-stat"><div class="hero-stat-num" data-count="107">0</div><div class="hero-stat-label">skills</div></div>
      <div class="hero-stat"><div class="hero-stat-num" data-count="5">0</div><div class="hero-stat-label">ferramentas</div></div>
      <div class="hero-stat"><div class="hero-stat-num" data-count="2">0</div><div class="hero-stat-label">padroes abertos</div></div>
      <div class="hero-stat"><div class="hero-stat-num" data-count="9">0</div><div class="hero-stat-label">abas</div></div>
    </div>
  </div>
</div>
```

- [ ] **Step 3: Add stats counter animation JS**

Add to the `<script>` block:

```javascript
/* ========== ANIMATED COUNTERS ========== */
var counterObserver=new IntersectionObserver(function(entries){
  entries.forEach(function(entry){
    if(!entry.isIntersecting)return;
    var el=entry.target;
    var target=parseInt(el.getAttribute('data-count'));
    var suffix=target>100?'+':'';
    var duration=800;
    var start=performance.now();
    function tick(now){
      var progress=Math.min((now-start)/duration,1);
      var eased=1-Math.pow(1-progress,3);
      el.textContent=Math.floor(eased*target)+suffix;
      if(progress<1)requestAnimationFrame(tick);
    }
    requestAnimationFrame(tick);
    counterObserver.unobserve(el);
  });
},{threshold:0.5});
document.querySelectorAll('[data-count]').forEach(function(el){counterObserver.observe(el)});
```

- [ ] **Step 4: Verify in browser**

Open index.html. Hero should fill viewport. 3 colored orbs visible behind text. Title with "Big Tech" in gold. CTA button golden. Stats should animate from 0 when visible. CTA click should navigate to setup tab.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: hero section with orbs, stats animation, CTA"
```

---

## Task 5: Ticker/Marquee + Scroll Reveal + Clipboard

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add ticker CSS**

```css
/* ========== TICKER ========== */
.ticker{overflow:hidden;background:var(--bg0);border-bottom:1px solid var(--b1);padding:6px 0;white-space:nowrap}
.ticker-track{display:inline-flex;animation:scroll-ticker 60s linear infinite}
.ticker-track span{font-family:var(--f-mono);font-size:var(--t-xs);color:var(--t4);padding:0 var(--s6)}
@keyframes scroll-ticker{0%{transform:translateX(0)}100%{transform:translateX(-50%)}}
@media(prefers-reduced-motion:reduce){.ticker-track{animation:none}}
```

- [ ] **Step 2: Add ticker HTML right after `</header>`**

```html
<div class="ticker" aria-hidden="true">
  <div class="ticker-track">
    <span>107+ skills documentadas</span><span>5 ferramentas cobertas</span><span>Claude Code + Codex lado a lado</span><span>Padrao aberto SKILL.md</span><span>Quiz personalizado em 5 min</span><span>PT-BR nativo, sem traducao</span><span>9 abas de conteudo</span><span>Zero dependencias</span>
    <span>107+ skills documentadas</span><span>5 ferramentas cobertas</span><span>Claude Code + Codex lado a lado</span><span>Padrao aberto SKILL.md</span><span>Quiz personalizado em 5 min</span><span>PT-BR nativo, sem traducao</span><span>9 abas de conteudo</span><span>Zero dependencias</span>
  </div>
</div>
```

- [ ] **Step 3: Add scroll reveal JS**

Add to `<script>`:

```javascript
/* ========== SCROLL REVEAL ========== */
var revealObserver=new IntersectionObserver(function(entries){
  entries.forEach(function(entry){
    if(entry.isIntersecting){entry.target.classList.add('visible');revealObserver.unobserve(entry.target)}
  });
},{threshold:0.1,rootMargin:'0px 0px -40px 0px'});
function initReveals(){document.querySelectorAll('.reveal').forEach(function(el){revealObserver.observe(el)})}
initReveals();
```

- [ ] **Step 4: Add clipboard JS**

Add to `<script>`:

```javascript
/* ========== CLIPBOARD ========== */
function copyToClipboard(text){
  if(navigator.clipboard&&window.isSecureContext)return navigator.clipboard.writeText(text);
  var ta=document.createElement('textarea');
  ta.value=text;ta.style.cssText='position:fixed;left:-9999px';
  document.body.appendChild(ta);ta.select();document.execCommand('copy');
  document.body.removeChild(ta);return Promise.resolve();
}
function cpCode(btn){
  var block=btn.closest('.code');
  var text=block.querySelector('.code-body')?block.querySelector('.code-body').textContent:block.textContent.replace('Copiar','').trim();
  copyToClipboard(text).then(function(){
    btn.textContent='Copiado!';btn.style.color='var(--spc)';
    setTimeout(function(){btn.textContent='Copiar';btn.style.color=''},2000);
  });
}
```

- [ ] **Step 5: Add FAQ toggle JS**

Add to `<script>`:

```javascript
/* ========== FAQ TOGGLE ========== */
function tf(el){el.closest('.fi').classList.toggle('open')}
```

- [ ] **Step 6: Verify ticker scrolls, reveal works, clipboard works on code blocks**

- [ ] **Step 7: Commit**

```bash
git add index.html
git commit -m "feat: ticker marquee, scroll reveal, clipboard, FAQ toggle"
```

---

## Task 6: Search Modal (Ctrl+K)

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add search CSS**

```css
/* ========== SEARCH ========== */
.search-overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,.6);z-index:200;align-items:flex-start;justify-content:center;padding-top:15vh}
.search-overlay.open{display:flex}
.search-box{background:var(--bg2);border:1px solid var(--b2);border-radius:var(--r-lg);width:90%;max-width:560px;overflow:hidden;box-shadow:0 24px 48px rgba(0,0,0,.4)}
.search-input{width:100%;background:none;border:none;padding:var(--s4) var(--s5);color:var(--t1);font-size:var(--t-md);font-family:var(--f-body);outline:none}
.search-input::placeholder{color:var(--t4)}
.search-results{max-height:360px;overflow-y:auto;border-top:1px solid var(--b1)}
.search-result{padding:var(--s3) var(--s5);cursor:pointer;transition:background var(--dur-fast)}
.search-result:hover{background:var(--bg3)}
.search-result-tab{font-family:var(--f-mono);font-size:var(--t-xs);color:var(--t4);margin-bottom:2px}
.search-result-text{font-size:var(--t-sm);color:var(--t2)}
.search-empty{padding:var(--s5);text-align:center;color:var(--t4);font-size:var(--t-sm)}
.search-hint{padding:var(--s3) var(--s5);font-size:var(--t-xs);color:var(--t4);border-top:1px solid var(--b1);font-family:var(--f-mono)}
```

- [ ] **Step 2: Add search HTML before `</body>`**

```html
<div class="search-overlay" id="search-overlay" onclick="if(event.target===this)closeSearch()">
  <div class="search-box">
    <input class="search-input" id="search-input" type="text" placeholder="Buscar no toolkit..." oninput="doSearch(this.value)" autocomplete="off">
    <div class="search-results" id="search-results"></div>
    <div class="search-hint">Esc pra fechar · Enter pra navegar</div>
  </div>
</div>
```

- [ ] **Step 3: Add search JS**

Add to `<script>`:

```javascript
/* ========== SEARCH ========== */
function openSearch(){
  document.getElementById('search-overlay').classList.add('open');
  document.getElementById('search-input').value='';
  document.getElementById('search-results').innerHTML='';
  setTimeout(function(){document.getElementById('search-input').focus()},50);
}
function closeSearch(){document.getElementById('search-overlay').classList.remove('open')}

document.addEventListener('keydown',function(e){
  if((e.ctrlKey||e.metaKey)&&e.key==='k'){e.preventDefault();openSearch()}
  if(e.key==='Escape')closeSearch();
});

function doSearch(q){
  var res=document.getElementById('search-results');
  if(q.length<2){res.innerHTML='';return}
  var pages=document.querySelectorAll('.page');
  var matches=[];
  var tabNames={comece:'Comece aqui',metodo:'O Metodo',oficio:'Oficio',stack:'Stack',skills:'Skills',avancado:'Avancado',setup:'Setup',cola:'Cola & Dicas',custos:'Custos & Planos'};
  pages.forEach(function(p){
    var tab=p.id.replace('page-','');
    var text=p.textContent;
    var idx=text.toLowerCase().indexOf(q.toLowerCase());
    if(idx>-1){
      var start=Math.max(0,idx-40);
      var preview=text.substring(start,idx+q.length+60).trim();
      if(start>0)preview='...'+preview;
      matches.push({tab:tab,tabName:tabNames[tab]||tab,preview:preview});
    }
  });
  if(matches.length===0){res.innerHTML='<div class="search-empty">Nenhum resultado</div>';return}
  res.innerHTML=matches.slice(0,8).map(function(m,i){
    return '<div class="search-result" onclick="closeSearch();pg(\''+m.tab+'\',document.querySelector(\'[data-tab='+m.tab+']\'))"><div class="search-result-tab">'+m.tabName+'</div><div class="search-result-text">'+m.preview+'</div></div>';
  }).join('');
}
```

- [ ] **Step 4: Verify Ctrl+K opens search, Esc closes, typing filters**

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: global search modal (Ctrl+K)"
```

---

## Task 7: Aba 1 — Comece Aqui (below the fold content)

**Files:**
- Modify: `index.html` (add HTML inside `#page-comece` after the hero div)

**Source content:** `aba1-comece-aqui.md` sections 1-8

- [ ] **Step 1: Add bifurcation cards (Secao 1)**

Two cards side by side after the hero: "Iniciante curioso" and "Dev experiente". Each with title, description, what you get (list), CTA button. Use `.g2` grid. Content from aba1 Secao 1.

- [ ] **Step 2: Add "O que e isso aqui" section (Secao 2)**

Three-layer explanation (Fundacao, Stack, Personalizacao). Use 3 numbered cards in `.g3` layout.

- [ ] **Step 3: Add pre-requisitos section (Secao 3)**

Table with Node.js, Python, Git + install commands for Claude Code and Codex. Code blocks with copy buttons.

- [ ] **Step 4: Add 8 FAQs (Secao 4)**

FAQ accordion with all 8 questions from aba1. Each answer with cross-references to other tabs.

- [ ] **Step 5: Add stats section (Secao 5)**

7 stat cards in `.g4` grid (107+ skills, 5 ferramentas, 24+ agentes, 2 padroes, 9 abas, 4M devs Codex, ~4% commits Claude).

- [ ] **Step 6: Add navigation map (Secao 6)**

"Como navegar" section organized by user objective ("Quero entender", "Quero comecar", etc.) with arrow flows.

- [ ] **Step 7: Add "primeira pergunta" highlight + CTA final (Secoes 7-8)**

Highlighted block with the key question + 3 path buttons at the bottom.

- [ ] **Step 8: Verify all sections render, links work, FAQs expand**

- [ ] **Step 9: Commit**

```bash
git add index.html
git commit -m "feat: aba 1 — comece aqui complete"
```

---

## Task 8: Aba 2 — O Metodo

**Files:**
- Modify: `index.html` (add HTML inside `#page-metodo`)

**Source content:** `aba2-o-metodo.md`

- [ ] **Step 1: Add intro (eyebrow + title + lead)**

- [ ] **Step 2: Add "A virgula que muda tudo" intro text**

- [ ] **Step 3: Add "cozinha + mochila" mental model section**

Two cards: cozinha (global) and mochila (local) side by side with descriptions.

- [ ] **Step 4: Add "Onde cada coisa mora" tables**

Two tables (Claude Code paths + Codex paths) showing global vs local directories.

- [ ] **Step 5: Add "O que vai onde" rules section**

Two columns: "Vai no GLOBAL" and "Vai no LOCAL" with bullet lists and golden rules.

- [ ] **Step 6: Add "Como os dois se combinam" numbered explanation**

3-step flow showing how global + local merge.

- [ ] **Step 7: Add anti-padrao "Globalzao" section**

Code block showing bloated global, symptoms list, cost explanation.

- [ ] **Step 8: Add "padrao certo" comparison**

Code block showing clean global + local. Comparison stats (5x less tokens, etc).

- [ ] **Step 9: Add "criando projeto do zero" step-by-step**

Code block with bash commands (works for both Claude Code and Codex).

- [ ] **Step 10: Add "3 testes" section and "resumo" highlight block**

- [ ] **Step 11: Add "O que vem depois" links**

- [ ] **Step 12: Verify all renders correctly**

- [ ] **Step 13: Commit**

```bash
git add index.html
git commit -m "feat: aba 2 — o metodo complete"
```

---

## Task 9: Aba 3 — Oficio

**Files:**
- Modify: `index.html` (add HTML inside `#page-oficio`)

**Source content:** `aba3-oficio.md` — largest tab, 9 sections

- [ ] **Step 1: Add intro + 4 pilares (Secoes 1)**

4 cards (Contexto, Objetivo, Restricoes, Formato) each with question, bad example, good example. Grid 2x2 on desktop.

- [ ] **Step 2: Add CLAUDE.md / AGENTS.md equivalence table (Secao 2)**

Comparison table + shared template code block with copy button.

- [ ] **Step 3: Add 6 prompt templates (Secao 3)**

6 templates in accordion or tab format, each with copy button. Templates: feature nova, bug fix, code review, refactor, documentar, analise de dados.

- [ ] **Step 4: Add decision table (Secao 4)**

Table mapping task type → approach → why.

- [ ] **Step 5: Add 6 interactive scenarios (Secao 5)**

Scenario selector buttons + panel showing prompt errado vs certo side by side for each.

- [ ] **Step 6: Add 6 golden rules (Secao 6)**

6 numbered cards with large number + rule + explanation. Grid 2x3.

- [ ] **Step 7: Add 5 anti-patterns (Secao 7)**

5 cards with red-tinted accent, each with name/symptom/cure.

- [ ] **Step 8: Add 8-step checklist (Secao 8)**

Checklist with interactive checkboxes persisted in localStorage. Each step with code block.

- [ ] **Step 9: Add "ciclo do dia" timeline (Secao 9)**

Horizontal timeline (4 stages: Manha, Meio, Tarde, Fim) + CTA final.

- [ ] **Step 10: Add checklist localStorage JS**

```javascript
/* ========== CHECKLIST PERSISTENCE ========== */
function toggleCheck(el){
  el.classList.toggle('checked');
  var id=el.getAttribute('data-check');
  var checks=JSON.parse(localStorage.getItem('gie-checks')||'{}');
  checks[id]=el.classList.contains('checked');
  localStorage.setItem('gie-checks',JSON.stringify(checks));
}
function loadChecks(){
  var checks=JSON.parse(localStorage.getItem('gie-checks')||'{}');
  Object.keys(checks).forEach(function(id){
    if(checks[id]){var el=document.querySelector('[data-check="'+id+'"]');if(el)el.classList.add('checked')}
  });
}
loadChecks();
```

- [ ] **Step 11: Verify all 9 sections, scenarios work, checklist persists**

- [ ] **Step 12: Commit**

```bash
git add index.html
git commit -m "feat: aba 3 — oficio complete"
```

---

## Task 10: Aba 4 — Stack

**Files:**
- Modify: `index.html` (add HTML inside `#page-stack`)

**Source content:** `aba4-stack.md`

- [ ] **Step 1: Add intro + panorama 2026 (Secoes 1)**

3-layer explanation (harnesses, ferramentas auxiliares, surfaces).

- [ ] **Step 2: Add Claude Code vs Codex cards (Secao 2)**

Two large cards SIDE BY SIDE with equal visual weight. Claude Code in terracota (--cc), Codex in cyan (--cdx). Same internal structure: who, model, surfaces, philosophy, strengths, cost, config.

- [ ] **Step 3: Add comparison table (Secao 3)**

Table: 9 dimensions (security, config, granularity, instruction, skills, multi-agent, computer use, open source, cloud). "Linguagem humana" highlight rows at bottom.

- [ ] **Step 4: Add "stack por objetivo" accordion (Secao 4)**

11 "Quero X" items as expandable cards/accordion. This is the central section of the tab.

- [ ] **Step 5: Add 5 tool cards (Secao 5)**

GSD, Spec-Kit, Superpowers, GSP, OpenCode — same format as original (stripe, problem/solution, badges).

- [ ] **Step 6: Add decision guide (Secao 6)**

9 scenario cards with icon and recommendation.

- [ ] **Step 7: Add recommended combo highlight + "what's not in stack" accordion (Secoes 7-8)**

- [ ] **Step 8: Verify paridade visual between Claude Code and Codex cards**

- [ ] **Step 9: Commit**

```bash
git add index.html
git commit -m "feat: aba 4 — stack complete"
```

---

## Task 11: Aba 5 — Skills

**Files:**
- Modify: `index.html` (add HTML inside `#page-skills`)

**Source content:** `aba5-skills.md` — 9 sections including GSP showcase

- [ ] **Step 1: Add intro + "what is a skill" (Secoes 1)**

File structure diagram, table (prompt vs skill), two types explanation.

- [ ] **Step 2: Add SKILL.md anatomy (Secao 2)**

Minimal and complete structure code blocks with frontmatter explanation.

- [ ] **Step 3: Add skill discovery tables (Secao 3)**

Claude Code (5-layer hierarchy) and Codex (2-layer) tables. Dual-folder structure example with symlink tip.

- [ ] **Step 4: Add "create your first skill" tutorial (Secao 4)**

5-step tutorial with code blocks for each step.

- [ ] **Step 5: Add 4 tool cards — GSD, Spec-Kit, Superpowers, GSP teaser (Secao 5)**

Same format as original. GSP links to Secao 6.

- [ ] **Step 6: Add GSP showcase (Secao 6)**

Dual diamond diagram, 8-phase pipeline, setup rapido vs completo, 20+ commands table organized by phase, when to use/not use, before/after comparison.

- [ ] **Step 7: Add 4 workflow combos (Secao 7)**

4 workflow cards: solo, iniciante, designer, time profissional.

- [ ] **Step 8: Add distribution levels + golden rule (Secoes 8-9)**

4 levels (local, personal, team, public) + 5 questions to ask before creating a skill.

- [ ] **Step 9: Verify, commit**

```bash
git add index.html
git commit -m "feat: aba 5 — skills complete"
```

---

## Task 12: Aba 6 — Avancado (11 sub-tabs with sticky TOC)

**Files:**
- Modify: `index.html` (add HTML inside `#page-avancado`, add sub-tab CSS + JS)

**Source content:** `aba6-avancado.md` — 11 sub-tabs

- [ ] **Step 1: Add sub-tab CSS**

```css
/* ========== SUB-TABS (Aba 6) ========== */
.subtabs{display:flex;gap:2px;overflow-x:auto;scrollbar-width:none;background:var(--bg2);border:1px solid var(--b1);border-radius:var(--r-md);padding:3px;position:sticky;top:50px;z-index:50;margin-bottom:var(--s6)}
.subtabs::-webkit-scrollbar{display:none}
.subtab{background:none;border:none;padding:6px 14px;color:var(--t3);font-family:var(--f-mono);font-size:var(--t-xs);white-space:nowrap;border-radius:var(--r-sm);transition:all var(--dur-base);cursor:pointer;display:flex;align-items:center;gap:4px}
.subtab:hover{color:var(--t1);background:var(--bg3)}
.subtab.active{color:var(--t1);background:var(--bg3);font-weight:500}
.subpage{display:none}
.subpage.active{display:block;animation:fadeUp 180ms var(--ease) both}
```

- [ ] **Step 2: Add intro + sub-tab navigation HTML**

11 sub-tab buttons with badges "NOVO" on Memoria and Plugins. 11 subpage divs.

- [ ] **Step 3: Add sub-tab switching JS**

```javascript
function subtab(id,btn){
  var parent=btn.closest('.page');
  parent.querySelectorAll('.subpage').forEach(function(p){p.classList.remove('active')});
  parent.querySelectorAll('.subtab').forEach(function(b){b.classList.remove('active')});
  parent.querySelector('#sub-'+id).classList.add('active');
  btn.classList.add('active');
}
```

- [ ] **Step 4: Add sub-tab 1 content — CLAUDE.md / AGENTS.md avancado**

5-layer hierarchy (Claude Code), 2-layer (Codex), what goes where table, advanced patterns with code blocks.

- [ ] **Step 5: Add sub-tab 2 — settings.json / config.toml**

Config examples for both Claude Code and Codex with code blocks.

- [ ] **Step 6: Add sub-tab 3 — MCP**

Explanation + config JSON + custom server example.

- [ ] **Step 7: Add sub-tab 4 — Subagents**

Fan-out vs Pipeline patterns, code example.

- [ ] **Step 8: Add sub-tab 5 — Hooks**

PreToolUse, PostToolUse, SessionStart examples.

- [ ] **Step 9: Add sub-tab 6 — Custom skills**

Template with frontmatter, full structure.

- [ ] **Step 10: Add sub-tab 7 — Performance**

3 FAQs on session management, chunking, CLAUDE.md optimization.

- [ ] **Step 11: Add sub-tab 8 — CI/CD**

GitHub Actions workflow YAML.

- [ ] **Step 12: Add sub-tab 9 — Troubleshooting**

6 common problems with solutions.

- [ ] **Step 13: Add sub-tab 10 — Memoria (NOVO)**

Content from aba6 section on semantic memory.

- [ ] **Step 14: Add sub-tab 11 — Plugins & Marketplace (NOVO)**

Content from aba6 section on plugin creation and distribution.

- [ ] **Step 15: Verify sub-tab switching, sticky behavior, badges visible**

- [ ] **Step 16: Commit**

```bash
git add index.html
git commit -m "feat: aba 6 — avancado with 11 sub-tabs complete"
```

---

## Task 13: Aba 7 — Setup Personalizado (Quiz Stepper)

**Files:**
- Modify: `index.html`

**Source content:** `aba7-setup-personalizado.md`

- [ ] **Step 1: Add quiz CSS**

```css
/* ========== QUIZ STEPPER ========== */
.quiz-progress{display:flex;align-items:center;gap:var(--s3);margin-bottom:var(--s6)}
.quiz-bar{flex:1;height:4px;background:var(--bg3);border-radius:2px;overflow:hidden}
.quiz-fill{height:100%;background:var(--au);border-radius:2px;transition:width var(--dur-slow) var(--ease)}
.quiz-counter{font-family:var(--f-mono);font-size:var(--t-xs);color:var(--t3);white-space:nowrap}
.quiz-step{display:none;animation:fadeUp 220ms var(--ease) both}
.quiz-step.active{display:block}
.quiz-q{font-family:var(--f-display);font-weight:700;font-size:var(--t-lg);color:var(--t1);margin-bottom:var(--s3)}
.quiz-why{font-size:var(--t-sm);color:var(--t3);margin-bottom:var(--s5)}
.quiz-opts{display:flex;flex-direction:column;gap:var(--s3)}
.quiz-opt{background:var(--bg3);border:1px solid var(--b1);border-radius:var(--r-md);padding:var(--s4);cursor:pointer;transition:all var(--dur-base);text-align:left;color:var(--t2);font-size:var(--t-sm)}
.quiz-opt:hover{border-color:var(--b3);background:var(--bg4)}
.quiz-opt.selected{border-color:var(--au);background:var(--aubg);color:var(--t1)}
.quiz-nav{display:flex;justify-content:space-between;margin-top:var(--s6)}
.quiz-btn{padding:8px 24px;border-radius:var(--r-sm);font-size:var(--t-sm);border:1px solid var(--b2);background:var(--bg3);color:var(--t2);transition:all var(--dur-base)}
.quiz-btn:hover{border-color:var(--b3);color:var(--t1)}
.quiz-btn-primary{background:var(--au);color:var(--bg0);border-color:var(--au);font-weight:500}
.quiz-btn-primary:hover{background:var(--au1)}
.quiz-result{margin-top:var(--s6)}
.quiz-result-tabs{display:flex;gap:2px;margin-bottom:var(--s4)}
.quiz-result-tab{padding:6px 16px;background:var(--bg3);border:1px solid var(--b1);border-radius:var(--r-sm) var(--r-sm) 0 0;color:var(--t3);font-size:var(--t-sm);cursor:pointer;border-bottom:none}
.quiz-result-tab.active{background:var(--bg2);color:var(--t1)}
.quiz-result-panel{display:none;background:var(--bg2);border:1px solid var(--b1);border-radius:0 var(--r-md) var(--r-md) var(--r-md);padding:var(--s5)}
.quiz-result-panel.active{display:block}
```

- [ ] **Step 2: Add quiz HTML structure**

Intro section (eyebrow, title, lead, free vs premium cards) + quiz container with 6 steps + result container. Content from aba7 sections 1-2.

- [ ] **Step 3: Add quiz JS (state machine, generation, localStorage)**

Full quiz engine: state management, option selection, step navigation, progress bar updates, artifact generation via template literals, localStorage persistence, download via Blob, result tab switching.

The quiz questions, options, and generation logic should match aba7-setup-personalizado.md exactly (6 questions + bonus).

- [ ] **Step 4: Add 4 case examples section (Secao 3 of aba7)**

4 persona cards showing example quiz results.

- [ ] **Step 5: Verify quiz flow end-to-end**

Complete quiz with different answers. Verify: progress bar, step transitions, option persistence on back, artifact generation, copy/download buttons, localStorage saves.

- [ ] **Step 6: Commit**

```bash
git add index.html
git commit -m "feat: aba 7 — quiz stepper with artifact generation"
```

---

## Task 14: Aba 8 — Cola & Dicas Pro

**Files:**
- Modify: `index.html`

**Source content:** `aba8-cola-dicas-pro.md`

- [ ] **Step 1: Add intro + print button**

Eyebrow, title, lead. Print button that triggers `window.print()`.

- [ ] **Step 2: Add setup completo section**

Pre-requisitos table (macOS/Windows/Linux) + install commands for Claude Code and Codex with copy buttons.

- [ ] **Step 3: Add commands grid (Claude Code vs Codex)**

Master table mapping function → command in each tool. Categories: sessao, navegacao, modelo, contexto, debug, projeto.

- [ ] **Step 4: Add 3 reference flows**

Visual flows: projeto completo, task rapida, design system.

- [ ] **Step 5: Add 8 rules in one line**

Grid of 8 rule cards.

- [ ] **Step 6: Add 18 dicas pro**

Tip cards with colored left border by category. Content from aba8 sections on permissions, navigation, workflow, think modes, tools, advanced.

- [ ] **Step 7: Add print CSS**

```css
@media print{
  header,.ticker,.search-overlay,.hero-orb{display:none!important}
  .page{display:block!important;page-break-after:always}
  .fi.open .fa,.fa{max-height:none!important;padding:8px 16px!important}
  body{background:#fff;color:#000}
  .card,.code{border:1px solid #ccc}
}
```

- [ ] **Step 8: Verify print preview shows all content expanded**

- [ ] **Step 9: Commit**

```bash
git add index.html
git commit -m "feat: aba 8 — cola & dicas pro with print CSS"
```

---

## Task 15: Aba 9 — Custos & Planos

**Files:**
- Modify: `index.html`

**Source content:** `aba9-custos-planos.md`

- [ ] **Step 1: Add intro + pricing tables (Secao 1)**

Side-by-side pricing: Anthropic (Pro, Max 5x, Max 20x, API) and OpenAI (Plus, Pro, API) with R$ equivalents. Comparison table.

- [ ] **Step 2: Add 4 real scenarios (Secao 2)**

Cards for: estudante, freelancer, time pequeno, projeto critico. Each with recommendation, cost, justification.

- [ ] **Step 3: Add interactive calculator (Secao 3)**

Calculator with: model selector (tabs), cambio input, sliders (sessions/day, days/month, devs, cache rate), presets (solo, consultor, startup, agencia), result display (R$/mes, USD/dia, cache savings).

- [ ] **Step 4: Add calculator JS**

Full calculation logic matching the original site's calculator but expanded with Codex pricing. Presets auto-fill sliders. Result updates on any input change.

- [ ] **Step 5: Add economy hacks + invisible costs sections**

Tips for reducing cost + hidden costs (time, context, rework).

- [ ] **Step 6: Verify calculator works with all presets and manual inputs**

- [ ] **Step 7: Commit**

```bash
git add index.html
git commit -m "feat: aba 9 — custos & planos with interactive calculator"
```

---

## Task 16: Cross-References + Final Polish

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Verify all internal tab links work**

Click through every "→ Aba X" link across all 9 tabs. Fix any broken references.

- [ ] **Step 2: Add `.reveal` class to content sections**

Add `class="reveal"` to major section divs across all tabs for scroll-reveal animation.

- [ ] **Step 3: Re-init reveals after page switch**

Update `pg()` function to call `initReveals()` after switching tabs so new page content gets observed.

- [ ] **Step 4: Verify mobile layout (768px and 480px)**

Check all 9 tabs at mobile viewpoints. Verify: grids collapse, tabs scroll, hero resizes, quiz is usable, calculator fits.

- [ ] **Step 5: Verify keyboard navigation**

Tab through all interactive elements. Verify: tabs, FAQs, quiz options, code copy buttons all accessible by keyboard.

- [ ] **Step 6: Verify reduced-motion**

Enable `prefers-reduced-motion` in DevTools. Verify no animations play.

- [ ] **Step 7: Final commit**

```bash
git add index.html
git commit -m "feat: cross-references, scroll reveal, accessibility polish"
```

---

## Summary

| Task | What | Commits |
|---|---|---|
| 1 | HTML head + CSS tokens + reset | 1 |
| 2 | Component CSS classes | 1 |
| 3 | Header + nav + hash routing | 1 |
| 4 | Hero (orbs, stats, CTA) | 1 |
| 5 | Ticker + reveal + clipboard + FAQ | 1 |
| 6 | Search modal (Ctrl+K) | 1 |
| 7 | Aba 1 — Comece aqui | 1 |
| 8 | Aba 2 — O Metodo | 1 |
| 9 | Aba 3 — Oficio | 1 |
| 10 | Aba 4 — Stack | 1 |
| 11 | Aba 5 — Skills | 1 |
| 12 | Aba 6 — Avancado (11 sub-tabs) | 1 |
| 13 | Aba 7 — Setup (quiz stepper) | 1 |
| 14 | Aba 8 — Cola & Dicas Pro | 1 |
| 15 | Aba 9 — Custos & Planos | 1 |
| 16 | Cross-refs + polish | 1 |

**Total: 16 tasks, 16 commits.**

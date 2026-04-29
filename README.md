<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Mortada Cherrak — AI Student & Data Scientist</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;700&display=swap" rel="stylesheet"/>
<style>
  :root {
    --purple: #c084fc;
    --indigo: #818cf8;
    --dark: #0d0221;
    --darker: #070114;
    --card: rgba(255,255,255,0.04);
    --border: rgba(192,132,252,0.2);
    --text: #e2e8f0;
    --muted: #94a3b8;
  }

  * { margin:0; padding:0; box-sizing:border-box; }

  body {
    background: var(--darker);
    color: var(--text);
    font-family: 'Space Grotesk', sans-serif;
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  #cursor {
    width: 12px; height: 12px;
    background: var(--purple);
    border-radius: 50%;
    position: fixed;
    pointer-events: none;
    z-index: 9999;
    transform: translate(-50%,-50%);
    transition: transform 0.1s, width 0.2s, height 0.2s, background 0.2s;
    mix-blend-mode: screen;
  }
  #cursor-ring {
    width: 36px; height: 36px;
    border: 1px solid rgba(192,132,252,0.5);
    border-radius: 50%;
    position: fixed;
    pointer-events: none;
    z-index: 9998;
    transform: translate(-50%,-50%);
    transition: all 0.15s ease;
  }

  /* Canvas */
  #bg-canvas {
    position: fixed;
    top:0; left:0;
    width:100%; height:100%;
    z-index: 0;
    opacity: 0.6;
  }

  /* Layout */
  .content { position: relative; z-index: 1; }

  /* ── HERO ── */
  .hero {
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    text-align: center;
    padding: 2rem;
    position: relative;
  }

  .hero-badge {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    background: rgba(192,132,252,0.1);
    border: 1px solid var(--border);
    border-radius: 999px;
    padding: 6px 16px;
    font-size: 13px;
    color: var(--purple);
    margin-bottom: 2rem;
    animation: fadeDown 0.8s ease both;
  }
  .hero-badge span { width:6px; height:6px; background:var(--purple); border-radius:50%; animation: pulse 2s infinite; }

  .hero h1 {
    font-size: clamp(2.5rem, 8vw, 5.5rem);
    font-weight: 700;
    line-height: 1.05;
    letter-spacing: -2px;
    animation: fadeDown 0.8s 0.1s ease both;
  }
  .hero h1 .accent {
    background: linear-gradient(135deg, var(--purple) 0%, var(--indigo) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  .hero-alias {
    font-family: 'JetBrains Mono', monospace;
    color: var(--purple);
    font-size: 1.1rem;
    margin-top: 0.5rem;
    animation: fadeDown 0.8s 0.2s ease both;
    opacity: 0.8;
  }

  .typing-wrap {
    margin-top: 1.5rem;
    font-size: 1.1rem;
    color: var(--muted);
    height: 1.6em;
    animation: fadeDown 0.8s 0.3s ease both;
  }
  .typing-cursor { color: var(--purple); animation: blink 0.7s infinite; }

  .hero-btns {
    margin-top: 2.5rem;
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
    justify-content: center;
    animation: fadeDown 0.8s 0.4s ease both;
  }
  .btn-primary {
    background: linear-gradient(135deg, #7c3aed, #4f46e5);
    color: white;
    border: none;
    padding: 12px 28px;
    border-radius: 8px;
    font-family: 'Space Grotesk', sans-serif;
    font-size: 15px;
    font-weight: 500;
    cursor: none;
    transition: transform 0.2s, box-shadow 0.2s;
    text-decoration: none;
  }
  .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 8px 30px rgba(124,58,237,0.4); }
  .btn-ghost {
    background: var(--card);
    color: var(--text);
    border: 1px solid var(--border);
    padding: 12px 28px;
    border-radius: 8px;
    font-family: 'Space Grotesk', sans-serif;
    font-size: 15px;
    font-weight: 500;
    cursor: none;
    transition: background 0.2s, transform 0.2s;
    text-decoration: none;
  }
  .btn-ghost:hover { background: rgba(255,255,255,0.08); transform: translateY(-2px); }

  .scroll-hint {
    position: absolute;
    bottom: 2rem;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 8px;
    color: var(--muted);
    font-size: 12px;
    animation: fadeDown 1.2s 1s ease both;
  }
  .scroll-mouse {
    width: 22px; height: 36px;
    border: 1.5px solid rgba(192,132,252,0.4);
    border-radius: 12px;
    display: flex;
    justify-content: center;
    padding-top: 6px;
  }
  .scroll-dot {
    width: 4px; height: 8px;
    background: var(--purple);
    border-radius: 2px;
    animation: scrollDown 1.5s infinite;
  }

  /* ── SECTIONS ── */
  section { padding: 6rem 2rem; max-width: 1100px; margin: 0 auto; }

  .section-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    color: var(--purple);
    letter-spacing: 3px;
    text-transform: uppercase;
    margin-bottom: 0.75rem;
  }
  .section-title {
    font-size: clamp(1.8rem, 4vw, 2.5rem);
    font-weight: 700;
    letter-spacing: -1px;
    margin-bottom: 3rem;
  }

  /* ── ABOUT ── */
  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2rem;
    align-items: start;
  }

  .code-card {
    background: #0f0a1e;
    border: 1px solid var(--border);
    border-radius: 12px;
    overflow: hidden;
    transform-style: preserve-3d;
    transition: transform 0.3s ease;
  }
  .code-card:hover { transform: rotateY(-4deg) rotateX(2deg) scale(1.02); }
  .code-header {
    background: rgba(192,132,252,0.08);
    border-bottom: 1px solid var(--border);
    padding: 10px 16px;
    display: flex;
    gap: 6px;
    align-items: center;
  }
  .dot { width:10px; height:10px; border-radius:50%; }
  .dot-r { background:#ff5f57; }
  .dot-y { background:#ffbd2e; }
  .dot-g { background:#28c840; }
  .code-filename { margin-left:8px; font-family:'JetBrains Mono',monospace; font-size:12px; color:var(--muted); }
  .code-body { padding: 1.5rem; font-family: 'JetBrains Mono', monospace; font-size: 13px; line-height: 1.9; }
  .kw { color: #c084fc; }
  .cl { color: #60a5fa; }
  .st { color: #34d399; }
  .cm { color: #4b5563; }
  .vr { color: #f9a8d4; }

  .info-cards { display: flex; flex-direction: column; gap: 1rem; }
  .info-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 1.25rem 1.5rem;
    display: flex;
    align-items: flex-start;
    gap: 1rem;
    transition: transform 0.3s ease, border-color 0.3s ease;
    transform-style: preserve-3d;
  }
  .info-card:hover { transform: translateX(6px); border-color: var(--purple); }
  .info-icon {
    font-size: 24px;
    flex-shrink: 0;
    width: 44px; height: 44px;
    background: rgba(192,132,252,0.1);
    border-radius: 10px;
    display: flex; align-items: center; justify-content: center;
  }
  .info-card h4 { font-size: 14px; font-weight: 600; margin-bottom: 4px; }
  .info-card p { font-size: 13px; color: var(--muted); line-height: 1.5; }

  /* ── ACHIEVEMENT ── */
  .trophy-card {
    background: linear-gradient(135deg, rgba(192,132,252,0.12), rgba(129,140,248,0.08));
    border: 1px solid rgba(192,132,252,0.35);
    border-radius: 16px;
    padding: 2.5rem;
    display: flex;
    align-items: center;
    gap: 2rem;
    position: relative;
    overflow: hidden;
    transform-style: preserve-3d;
    transition: transform 0.4s ease;
  }
  .trophy-card:hover { transform: rotateX(2deg) scale(1.01); }
  .trophy-card::before {
    content: '';
    position: absolute; top: -50%; right: -20%;
    width: 300px; height: 300px;
    background: radial-gradient(circle, rgba(192,132,252,0.15) 0%, transparent 60%);
    pointer-events: none;
  }
  .trophy-emoji { font-size: 4rem; flex-shrink: 0; animation: float 3s ease-in-out infinite; }
  .trophy-text h3 { font-size: 1.4rem; font-weight: 700; margin-bottom: 0.5rem; }
  .trophy-text p { color: var(--muted); font-size: 14px; line-height: 1.6; }
  .trophy-badge {
    display: inline-flex; align-items: center; gap: 6px;
    background: rgba(192,132,252,0.15);
    border: 1px solid rgba(192,132,252,0.3);
    border-radius: 999px;
    padding: 4px 12px;
    font-size: 12px;
    color: var(--purple);
    margin-top: 0.75rem;
  }

  /* ── SKILLS ── */
  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 1.25rem;
  }
  .skill-group {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 1.5rem;
    transition: transform 0.3s ease, border-color 0.3s ease, box-shadow 0.3s ease;
    transform-style: preserve-3d;
  }
  .skill-group:hover {
    transform: translateY(-6px) rotateX(2deg);
    border-color: var(--purple);
    box-shadow: 0 20px 40px rgba(124,58,237,0.15);
  }
  .skill-group-title {
    font-size: 11px;
    font-family: 'JetBrains Mono', monospace;
    letter-spacing: 2px;
    color: var(--purple);
    text-transform: uppercase;
    margin-bottom: 1.25rem;
    display: flex; align-items: center; gap: 8px;
  }
  .skill-group-title::after { content:''; flex:1; height:1px; background:var(--border); }
  .skill-items { display: flex; flex-wrap: wrap; gap: 8px; }
  .skill-tag {
    background: rgba(255,255,255,0.05);
    border: 1px solid rgba(255,255,255,0.08);
    border-radius: 6px;
    padding: 5px 12px;
    font-size: 13px;
    color: var(--text);
    transition: all 0.2s ease;
    display: flex; align-items: center; gap: 6px;
  }
  .skill-tag:hover { background: rgba(192,132,252,0.15); border-color: var(--border); color: var(--purple); transform: scale(1.05); }

  /* ── STATS ── */
  .stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
    gap: 1rem;
    margin-bottom: 2rem;
  }
  .stat-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 12px;
    overflow: hidden;
    transform-style: preserve-3d;
    transition: transform 0.3s ease;
  }
  .stat-card:hover { transform: rotateY(4deg) rotateX(-2deg) scale(1.02); }
  .stat-card img { width: 100%; display: block; }

  /* ── CONTACT ── */
  .contact-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1rem;
  }
  .contact-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 1.75rem;
    text-align: center;
    text-decoration: none;
    color: var(--text);
    transition: transform 0.3s ease, border-color 0.3s ease, box-shadow 0.3s ease;
    transform-style: preserve-3d;
  }
  .contact-card:hover {
    transform: translateY(-8px) rotateX(4deg);
    border-color: var(--purple);
    box-shadow: 0 20px 50px rgba(124,58,237,0.2);
  }
  .contact-icon { font-size: 2rem; margin-bottom: 0.75rem; }
  .contact-card h4 { font-weight: 600; font-size: 15px; }
  .contact-card p { color: var(--muted); font-size: 13px; margin-top: 4px; }

  /* ── DIVIDER ── */
  .divider {
    width: 100%;
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--border), transparent);
    margin: 0 auto;
  }

  /* ── FOOTER ── */
  footer {
    text-align: center;
    padding: 3rem 2rem;
    color: var(--muted);
    font-size: 13px;
    position: relative;
    z-index: 1;
  }
  footer span { color: var(--purple); }

  /* ── ANIMATIONS ── */
  @keyframes fadeDown {
    from { opacity:0; transform: translateY(-20px); }
    to   { opacity:1; transform: translateY(0); }
  }
  @keyframes pulse {
    0%,100% { opacity:1; transform:scale(1); }
    50%      { opacity:0.4; transform:scale(0.85); }
  }
  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }
  @keyframes float {
    0%,100% { transform: translateY(0); }
    50%      { transform: translateY(-10px); }
  }
  @keyframes scrollDown {
    0%   { opacity:1; transform:translateY(0); }
    80%  { opacity:0; transform:translateY(12px); }
    100% { opacity:0; transform:translateY(12px); }
  }

  .reveal {
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  .reveal.visible { opacity: 1; transform: translateY(0); }

  @media(max-width:768px){
    .about-grid { grid-template-columns: 1fr; }
    .contact-grid { grid-template-columns: 1fr; }
    .trophy-card { flex-direction: column; text-align: center; }
  }
</style>
</head>
<body>

<div id="cursor"></div>
<div id="cursor-ring"></div>
<canvas id="bg-canvas"></canvas>

<div class="content">

  <!-- ── HERO ── -->
  <div class="hero">
    <div class="hero-badge">
      <span></span>
      Available for Internship
    </div>
    <h1>
      Mortada<br/>
      <span class="accent">Cherrak</span>
    </h1>
    <div class="hero-alias">[ 3xTpA ]</div>
    <div class="typing-wrap">
      <span id="typing-text"></span><span class="typing-cursor">|</span>
    </div>
    <div class="hero-btns">
      <a class="btn-primary" href="https://www.linkedin.com/in/mortada-cherrak" target="_blank">Connect on LinkedIn</a>
      <a class="btn-ghost" href="https://github.com/mortadacherrak" target="_blank">GitHub Profile</a>
    </div>
    <div class="scroll-hint">
      <div class="scroll-mouse"><div class="scroll-dot"></div></div>
      scroll
    </div>
  </div>

  <div class="divider"></div>

  <!-- ── ABOUT ── -->
  <section>
    <p class="section-label reveal">01 — About</p>
    <h2 class="section-title reveal">Who I am</h2>
    <div class="about-grid">
      <div class="code-card reveal">
        <div class="code-header">
          <div class="dot dot-r"></div>
          <div class="dot dot-y"></div>
          <div class="dot dot-g"></div>
          <span class="code-filename">mortada.py</span>
        </div>
        <div class="code-body">
<span class="cm"># ── Profile ──────────────────</span><br/>
<span class="kw">class</span> <span class="cl">Mortada</span>:<br/>
&nbsp;&nbsp;<span class="vr">name</span> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;= <span class="st">"Cherrak Mortada"</span><br/>
&nbsp;&nbsp;<span class="vr">alias</span> &nbsp;&nbsp;&nbsp;&nbsp;= <span class="st">"3xTpA"</span><br/>
&nbsp;&nbsp;<span class="vr">role</span> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;= <span class="st">"AI Student"</span><br/>
&nbsp;&nbsp;<span class="vr">uni</span> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;= <span class="st">"UABT Tlemcen"</span><br/>
&nbsp;&nbsp;<span class="vr">location</span> &nbsp;= <span class="st">"Algeria 🇩🇿"</span><br/>
<br/>
&nbsp;&nbsp;<span class="vr">learning</span> = [<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="st">"Statistics"</span>,<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="st">"R"</span>, <span class="st">"MongoDB"</span>,<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="st">"Big Data"</span><br/>
&nbsp;&nbsp;]<br/>
<br/>
&nbsp;&nbsp;<span class="vr">goal</span> = <span class="st">"Data Science Internship 🚀"</span>
        </div>
      </div>
      <div class="info-cards reveal">
        <div class="info-card">
          <div class="info-icon">🎓</div>
          <div>
            <h4>Education</h4>
            <p>Abou Bekr Belkaid Tlemcen University — AI specialization</p>
          </div>
        </div>
        <div class="info-card">
          <div class="info-icon">💡</div>
          <div>
            <h4>Currently Learning</h4>
            <p>Statistics · R · MongoDB · Big Data pipelines</p>
          </div>
        </div>
        <div class="info-card">
          <div class="info-icon">⚡</div>
          <div>
            <h4>Ask Me About</h4>
            <p>Python · SQL · Linux systems · Data analysis workflows</p>
          </div>
        </div>
        <div class="info-card">
          <div class="info-icon">🤝</div>
          <div>
            <h4>Open To</h4>
            <p>Data Science & AI internships — remote or on-site</p>
          </div>
        </div>
      </div>
    </div>
  </section>

  <div class="divider"></div>

  <!-- ── ACHIEVEMENT ── -->
  <section>
    <p class="section-label reveal">02 — Achievement</p>
    <h2 class="section-title reveal">Global Recognition</h2>
    <div class="trophy-card reveal">
      <div class="trophy-emoji">🏆</div>
      <div class="trophy-text">
        <h3>1st Prize — Global Winner</h3>
        <p>Huawei ICT Competition 2023 &nbsp;·&nbsp; Cloud Track</p>
        <p style="margin-top:0.5rem;font-size:13px;">Competed against top engineering students worldwide and claimed first place in the Cloud Computing category — one of the most competitive tracks at Huawei's annual global tech competition.</p>
        <div class="trophy-badge">⭐ Global Winner · 2023</div>
      </div>
    </div>
  </section>

  <div class="divider"></div>

  <!-- ── SKILLS ── -->
  <section>
    <p class="section-label reveal">03 — Skills</p>
    <h2 class="section-title reveal">Tech Stack</h2>
    <div class="skills-grid">
      <div class="skill-group reveal">
        <div class="skill-group-title">Languages</div>
        <div class="skill-items">
          <span class="skill-tag">🐍 Python</span>
          <span class="skill-tag">⚙️ C</span>
          <span class="skill-tag">🐘 PHP</span>
          <span class="skill-tag">📊 R</span>
          <span class="skill-tag">🖥️ Bash</span>
        </div>
      </div>
      <div class="skill-group reveal">
        <div class="skill-group-title">Data & Databases</div>
        <div class="skill-items">
          <span class="skill-tag">🐬 MySQL</span>
          <span class="skill-tag">🔴 Oracle</span>
          <span class="skill-tag">🍃 MongoDB</span>
          <span class="skill-tag">📦 Big Data</span>
        </div>
      </div>
      <div class="skill-group reveal">
        <div class="skill-group-title">Web & Markup</div>
        <div class="skill-items">
          <span class="skill-tag">🌐 HTML5</span>
          <span class="skill-tag">🎨 CSS3</span>
        </div>
      </div>
      <div class="skill-group reveal">
        <div class="skill-group-title">Design Tools</div>
        <div class="skill-items">
          <span class="skill-tag">✏️ Figma</span>
          <span class="skill-tag">🖼️ Photoshop</span>
          <span class="skill-tag">🖊️ Illustrator</span>
        </div>
      </div>
      <div class="skill-group reveal">
        <div class="skill-group-title">Systems & Tools</div>
        <div class="skill-items">
          <span class="skill-tag">🐧 Linux</span>
          <span class="skill-tag">🌿 Git</span>
        </div>
      </div>
    </div>
  </section>

  <div class="divider"></div>

  <!-- ── STATS ── -->
  <section>
    <p class="section-label reveal">04 — GitHub Stats</p>
    <h2 class="section-title reveal">Activity</h2>
    <div class="stats-grid reveal">
      <div class="stat-card">
        <img src="https://github-readme-stats.vercel.app/api?username=mortadacherrak&show_icons=true&theme=radical&hide_border=true&bg_color=0d0221&title_color=c084fc&icon_color=818cf8&text_color=e2e8f0" alt="GitHub Stats" loading="lazy"/>
      </div>
      <div class="stat-card">
        <img src="https://streak-stats.demolab.com?user=mortadacherrak&theme=radical&hide_border=true&background=0d0221&ring=c084fc&fire=818cf8&currStreakLabel=c084fc" alt="Streak Stats" loading="lazy"/>
      </div>
      <div class="stat-card">
        <img src="https://github-readme-stats.vercel.app/api/top-langs?username=mortadacherrak&layout=compact&theme=radical&hide_border=true&bg_color=0d0221&title_color=c084fc&text_color=e2e8f0" alt="Top Languages" loading="lazy"/>
      </div>
    </div>
    <div class="stat-card reveal" style="border-radius:12px;overflow:hidden;">
      <img src="https://github-readme-activity-graph.vercel.app/graph?username=mortadacherrak&theme=tokyo-night&hide_border=true&bg_color=0d0221&color=c084fc&line=818cf8&point=ffffff&area=true" alt="Activity Graph" loading="lazy" style="width:100%;display:block;"/>
    </div>
  </section>

  <div class="divider"></div>

  <!-- ── CONTACT ── -->
  <section>
    <p class="section-label reveal">05 — Contact</p>
    <h2 class="section-title reveal">Get In Touch</h2>
    <div class="contact-grid">
      <a class="contact-card reveal" href="https://www.linkedin.com/in/mortada-cherrak" target="_blank">
        <div class="contact-icon">💼</div>
        <h4>LinkedIn</h4>
        <p>mortada-cherrak</p>
      </a>
      <a class="contact-card reveal" href="https://www.instagram.com/mortadacherrak" target="_blank">
        <div class="contact-icon">📸</div>
        <h4>Instagram</h4>
        <p>@mortadacherrak</p>
      </a>
      <a class="contact-card reveal" href="https://twitter.com/mortada_cherrak" target="_blank">
        <div class="contact-icon">🐦</div>
        <h4>Twitter</h4>
        <p>@mortada_cherrak</p>
      </a>
    </div>
  </section>

  <footer>
    Built with <span>♥</span> by Mortada Cherrak · <span>3xTpA</span>
  </footer>
</div>

<script>
/* ── Cursor ── */
const cursor = document.getElementById('cursor');
const ring = document.getElementById('cursor-ring');
let mx=0, my=0, rx=0, ry=0;
document.addEventListener('mousemove', e => { mx=e.clientX; my=e.clientY; cursor.style.left=mx+'px'; cursor.style.top=my+'px'; });
setInterval(()=>{ rx+=(mx-rx)*0.12; ry+=(my-ry)*0.12; ring.style.left=Math.round(rx)+'px'; ring.style.top=Math.round(ry)+'px'; }, 16);
document.querySelectorAll('a,.btn-primary,.btn-ghost').forEach(el=>{
  el.addEventListener('mouseenter',()=>{ cursor.style.width='20px'; cursor.style.height='20px'; ring.style.width='50px'; ring.style.height='50px'; ring.style.borderColor='rgba(192,132,252,0.8)'; });
  el.addEventListener('mouseleave',()=>{ cursor.style.width='12px'; cursor.style.height='12px'; ring.style.width='36px'; ring.style.height='36px'; ring.style.borderColor='rgba(192,132,252,0.5)'; });
});

/* ── Particle Canvas ── */
const canvas = document.getElementById('bg-canvas');
const ctx = canvas.getContext('2d');
let W, H, particles=[], mouse={x:null,y:null};
function resize(){ W=canvas.width=innerWidth; H=canvas.height=innerHeight; }
resize(); window.addEventListener('resize', resize);
window.addEventListener('mousemove', e=>{ mouse.x=e.clientX; mouse.y=e.clientY; });

class Particle {
  constructor(){
    this.x=Math.random()*W; this.y=Math.random()*H;
    this.vx=(Math.random()-0.5)*0.3; this.vy=(Math.random()-0.5)*0.3;
    this.r=Math.random()*1.5+0.5;
    this.a=Math.random()*0.5+0.2;
  }
  update(){
    this.x+=this.vx; this.y+=this.vy;
    if(this.x<0||this.x>W) this.vx*=-1;
    if(this.y<0||this.y>H) this.vy*=-1;
    if(mouse.x){
      const dx=mouse.x-this.x, dy=mouse.y-this.y;
      const d=Math.sqrt(dx*dx+dy*dy);
      if(d<120){ this.x-=dx*0.015; this.y-=dy*0.015; }
    }
  }
  draw(){
    ctx.beginPath();
    ctx.arc(this.x,this.y,this.r,0,Math.PI*2);
    ctx.fillStyle=`rgba(192,132,252,${this.a})`;
    ctx.fill();
  }
}

for(let i=0;i<120;i++) particles.push(new Particle());

function drawLines(){
  for(let i=0;i<particles.length;i++){
    for(let j=i+1;j<particles.length;j++){
      const dx=particles[i].x-particles[j].x;
      const dy=particles[i].y-particles[j].y;
      const d=Math.sqrt(dx*dx+dy*dy);
      if(d<130){
        ctx.beginPath();
        ctx.moveTo(particles[i].x,particles[i].y);
        ctx.lineTo(particles[j].x,particles[j].y);
        ctx.strokeStyle=`rgba(129,140,248,${0.25*(1-d/130)})`;
        ctx.lineWidth=0.5;
        ctx.stroke();
      }
    }
  }
}

function animate(){
  ctx.clearRect(0,0,W,H);
  particles.forEach(p=>{ p.update(); p.draw(); });
  drawLines();
  requestAnimationFrame(animate);
}
animate();

/* ── Typing Effect ── */
const phrases = [
  'AI Student 🧠',
  'Data Scientist 📊',
  'Cloud Champion ☁️',
  'Python Enthusiast 🐍',
  'Linux Power User 🐧'
];
let pi=0, ci=0, deleting=false;
const el = document.getElementById('typing-text');
function typeLoop(){
  const phrase=phrases[pi];
  if(!deleting){
    el.textContent=phrase.slice(0,++ci);
    if(ci===phrase.length){ deleting=true; setTimeout(typeLoop,1800); return; }
    setTimeout(typeLoop,70);
  } else {
    el.textContent=phrase.slice(0,--ci);
    if(ci===0){ deleting=false; pi=(pi+1)%phrases.length; setTimeout(typeLoop,400); return; }
    setTimeout(typeLoop,35);
  }
}
typeLoop();

/* ── Scroll Reveal ── */
const reveals = document.querySelectorAll('.reveal');
const io = new IntersectionObserver(entries=>{
  entries.forEach((e,i)=>{
    if(e.isIntersecting){
      setTimeout(()=>e.target.classList.add('visible'), i*80);
    }
  });
},{threshold:0.1});
reveals.forEach(r=>io.observe(r));

/* ── 3D Tilt on mouse ── */
document.querySelectorAll('.code-card,.skill-group,.contact-card,.trophy-card').forEach(card=>{
  card.addEventListener('mousemove',e=>{
    const rect=card.getBoundingClientRect();
    const x=((e.clientX-rect.left)/rect.width-0.5)*14;
    const y=-((e.clientY-rect.top)/rect.height-0.5)*14;
    card.style.transform=`rotateY(${x}deg) rotateX(${y}deg) scale(1.02)`;
  });
  card.addEventListener('mouseleave',()=>{ card.style.transform=''; });
});
</script>
</body>
</html>

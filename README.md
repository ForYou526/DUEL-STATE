<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NOCHTRA — DUAL STATE : FRACTURED MIND</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Anton&family=Space+Mono:ital,wght@0,400;0,700;1,400&display=swap" rel="stylesheet">
<style>
  :root{
    --cream:#F2ECDC;
    --cream-dim:#E6DCC3;
    --ink:#1C1A14;
    --navy:#1B2A4A;
    --navy-bright:#3557A0;
    --camo-1:#333B29;
    --camo-2:#5C6449;
    --camo-3:#8B8367;
    --camo-4:#20241B;
    --camo-5:#9BA37E;
    --stitch: var(--navy);
    --grain-opacity: .05;
  }
  *{box-sizing:border-box; margin:0; padding:0;}
  html{scroll-behavior:smooth;}
  body{
    background:var(--cream);
    color:var(--ink);
    font-family:'Space Mono', monospace;
    overflow-x:hidden;
    transition:background .6s ease, color .6s ease;
  }
  body.inside{
    background:var(--camo-4);
    color:var(--cream-dim);
  }
  h1,h2,h3, .display{
    font-family:'Anton', sans-serif;
    font-weight:400;
    letter-spacing:.01em;
    text-transform:uppercase;
    line-height:.95;
  }
  a{color:inherit;}
  .wrap{max-width:1180px; margin:0 auto; padding:0 28px;}
  ::selection{background:var(--navy); color:var(--cream);}

  /* grain overlay */
  .grain{
    position:fixed; inset:0; pointer-events:none; z-index:999;
    opacity:var(--grain-opacity); mix-blend-mode:multiply;
    background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='120' height='120'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='2' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
  }
  body.inside .grain{opacity:.14; mix-blend-mode:screen;}

  /* stitched seam divider */
  .seam{
    width:100%; height:2px; position:relative;
    background:repeating-linear-gradient(90deg, var(--stitch) 0 10px, transparent 10px 18px);
    opacity:.55; margin:0 0;
  }

  /* ===== NAV ===== */
  nav{
    position:sticky; top:0; z-index:100;
    display:flex; align-items:center; justify-content:space-between;
    padding:18px 28px;
    background:var(--cream); border-bottom:2px dashed var(--navy);
    transition:background .6s ease, border-color .6s ease;
  }
  body.inside nav{background:var(--camo-4); border-bottom-color:var(--camo-5);}
  .logo{font-family:'Anton',sans-serif; font-size:22px; letter-spacing:.06em;}
  .logo span{color:var(--navy-bright);}
  button:focus-visible, .toggle:focus-visible{outline:2px solid var(--navy-bright); outline-offset:3px;}

  /* toggle switch */
  .toggle{
    display:flex; align-items:center; gap:8px; cursor:pointer;
    border:2px solid var(--navy); border-radius:30px; padding:4px 6px;
    background:transparent; font-family:'Space Mono',monospace;
  }
  .toggle-label{font-size:10px; letter-spacing:.1em; padding:0 4px;}
  .toggle-track{
    width:38px; height:20px; border-radius:20px; background:var(--navy);
    position:relative; flex-shrink:0;
  }
  .toggle-knob{
    position:absolute; top:2px; left:2px; width:16px; height:16px;
    border-radius:50%; background:var(--cream); transition:left .35s cubic-bezier(.6,.1,.2,1);
  }
  body.inside .toggle-knob{left:20px; background:var(--camo-5);}

  /* ===== HERO ===== */
  .hero{
    padding:70px 0 40px; position:relative;
    display:grid; grid-template-columns:1.15fr .85fr; gap:40px; align-items:center;
  }
  .eyebrow{
    font-size:11px; letter-spacing:.2em; text-transform:uppercase;
    color:var(--navy-bright); margin-bottom:16px; display:block;
  }
  body.inside .eyebrow{color:var(--camo-5);}
  .hero h1{font-size:clamp(46px,7.2vw,96px);}
  .hero h1 .glitch-word{position:relative; display:inline-block;}
  .tagline{
    font-family:'Anton',sans-serif; text-transform:none; font-size:clamp(18px,2vw,24px);
    margin-top:18px; opacity:.85;
  }
  .hero-desc{max-width:480px; font-size:14px; line-height:1.75; margin-top:22px; opacity:.85;}
  .btn-note{font-size:11px; opacity:.6; margin-top:26px; letter-spacing:.02em;}

  /* face doodle visual */
  .face-frame{
    position:relative; aspect-ratio:3/4; border:2px solid var(--navy);
    overflow:hidden; background:var(--cream-dim);
  }
  body.inside .face-frame{border-color:var(--camo-5);}
  .face-frame svg{position:absolute; inset:0; width:100%; height:100%; display:block; transition:opacity .5s ease;}
  .face-chaos{opacity:0;}
  body.inside .face-calm{opacity:0;}
  body.inside .face-chaos{opacity:1;}
  .frame-tag{
    position:absolute; bottom:10px; left:10px; font-size:9px; letter-spacing:.08em;
    background:var(--navy); color:var(--cream); padding:5px 9px; z-index:2;
  }
  body.inside .frame-tag{background:var(--camo-5); color:var(--camo-4);}

  /* ===== SECTION GENERIC ===== */
  section{padding:80px 0;}
  .section-head{margin-bottom:44px; max-width:640px;}
  .section-head .eyebrow{margin-bottom:10px;}
  .section-head h2{font-size:clamp(30px,4.5vw,52px);}
  .section-head p{font-size:14px; line-height:1.7; opacity:.8; margin-top:14px;}

  /* ===== STORY ===== */
  .story{display:grid; grid-template-columns:1fr 1fr; gap:50px;}
  .story-block p{font-size:14px; line-height:1.85; margin-bottom:16px; opacity:.88;}
  .story-block em{font-style:italic; color:var(--navy-bright);}
  .story-quote{
    font-family:'Anton',sans-serif; text-transform:none; font-size:20px; line-height:1.4;
    border-left:3px solid var(--navy); padding-left:20px; margin:24px 0;
  }
  .camo-swatch{
    width:100%; aspect-ratio:4/3; position:relative; overflow:hidden;
    border:2px solid var(--navy);
  }

  /* ===== PHILOSOPHY CARDS ===== */
  .phil-grid{display:grid; grid-template-columns:repeat(4,1fr); gap:2px; background:var(--navy);}
  body.inside .phil-grid{background:var(--camo-5);}
  .phil-card{
    background:var(--cream); padding:30px 24px; min-height:280px;
    display:flex; flex-direction:column; gap:12px;
  }
  body.inside .phil-card{background:var(--camo-4);}
  .phil-num{font-family:'Anton',sans-serif; font-size:13px; color:var(--navy-bright);}
  .phil-card h3{font-size:20px; margin-top:4px;}
  .phil-card p{font-size:12.5px; line-height:1.7; opacity:.82;}
  .phil-joke{
    margin-top:auto; font-size:11px; font-style:italic; opacity:.6;
    border-top:1px dashed var(--navy); padding-top:10px;
  }
  body.inside .phil-joke{border-top-color:var(--camo-5);}

  /* ===== DIAGNOSTIC TERMINAL ===== */
  .diagnostic{
    background:var(--navy); color:var(--cream); padding:60px 0;
  }
  body.inside .diagnostic{background:var(--camo-4);}
  .diag-wrap{display:grid; grid-template-columns:.9fr 1.1fr; gap:44px; align-items:start;}
  .diag-wrap h2{color:var(--cream); font-size:clamp(26px,4vw,44px);}
  .diag-wrap p{font-size:13px; line-height:1.8; opacity:.8; margin-top:14px; max-width:400px;}
  .terminal{
    background:#0E1420; border:2px solid var(--navy-bright); padding:18px 20px;
    font-size:12.5px; line-height:1.9; min-height:260px; position:relative;
  }
  .terminal-head{
    display:flex; justify-content:space-between; align-items:center;
    border-bottom:1px dashed rgba(255,255,255,.2); padding-bottom:8px; margin-bottom:10px;
    font-size:10px; letter-spacing:.1em; opacity:.6; text-transform:uppercase;
  }
  .terminal-body{min-height:190px;}
  .terminal-line{opacity:0; animation:appear .4s forwards;}
  .terminal-line .ts{color:#7FA7E8; margin-right:8px;}
  @keyframes appear{to{opacity:1;}}
  .terminal-cursor{display:inline-block; width:7px; height:13px; background:var(--cream); animation:blink 1s step-end infinite; vertical-align:middle;}
  @keyframes blink{50%{opacity:0;}}
  /* ===== ROADMAP ===== */
  .roadmap{display:flex; flex-direction:column; gap:0;}
  .rm-item{
    display:grid; grid-template-columns:90px 1fr; gap:26px;
    padding:26px 0; border-top:2px dashed var(--navy); align-items:start;
  }
  body.inside .rm-item{border-top-color:var(--camo-5);}
  .rm-item:last-child{border-bottom:2px dashed var(--navy);}
  body.inside .rm-item:last-child{border-bottom-color:var(--camo-5);}
  .rm-num{font-family:'Anton',sans-serif; font-size:34px; color:var(--navy-bright); line-height:1;}
  .rm-item.current .rm-num{color:var(--ink);}
  body.inside .rm-item.current .rm-num{color:var(--cream-dim);}
  .rm-title{font-family:'Anton',sans-serif; font-size:20px; text-transform:uppercase;}
  .rm-desc{font-size:12.5px; line-height:1.7; opacity:.78; margin-top:8px; max-width:600px;}
  .rm-tag{
    display:inline-block; font-size:9px; letter-spacing:.08em; text-transform:uppercase;
    border:1px solid var(--navy); padding:3px 8px; margin-top:10px;
  }
  body.inside .rm-tag{border-color:var(--camo-5);}

  /* ===== FAQ ===== */
  .faq{max-width:720px;}
  .faq-item{border-top:1px solid var(--navy); padding:18px 0;}
  body.inside .faq-item{border-top-color:var(--camo-5);}
  .faq-item:last-child{border-bottom:1px solid var(--navy);}
  body.inside .faq-item:last-child{border-bottom-color:var(--camo-5);}
  .faq-q{
    font-family:'Anton',sans-serif; font-size:15px; text-transform:none;
  }
  .faq-a{
    font-size:12.5px; line-height:1.75; opacity:.8;
  }

  /* ===== FOOTER ===== */
  footer{padding:60px 0 30px; border-top:2px solid var(--navy);}
  body.inside footer{border-top-color:var(--camo-5);}
  .foot-grid{display:grid; grid-template-columns:1.2fr .8fr .8fr; gap:40px; margin-bottom:40px;}
  .foot-logo{font-family:'Anton',sans-serif; font-size:26px;}
  .foot-desc{font-size:12px; line-height:1.7; opacity:.75; margin-top:10px; max-width:340px;}
  .foot-col h4{font-size:10px; letter-spacing:.1em; text-transform:uppercase; opacity:.6; margin-bottom:12px;}
  .foot-bottom{
    display:flex; justify-content:space-between; flex-wrap:wrap; gap:10px;
    font-size:10.5px; opacity:.55; padding-top:20px; border-top:1px dashed var(--navy);
  }
  body.inside .foot-bottom{border-top-color:var(--camo-5);}

  /* reveal on scroll */
  .reveal{opacity:0; transform:translateY(24px); transition:opacity .7s ease, transform .7s ease;}
  .reveal.visible{opacity:1; transform:translateY(0);}

  @media (prefers-reduced-motion: reduce){
    *{animation:none !important; transition:none !important;}
  }

  @media (max-width: 880px){
    .hero{grid-template-columns:1fr; padding-top:40px;}
    .story{grid-template-columns:1fr;}
    .phil-grid{grid-template-columns:1fr 1fr;}
    .diag-wrap{grid-template-columns:1fr;}
    .foot-grid{grid-template-columns:1fr;}
    .rm-item{grid-template-columns:50px 1fr;}
  }
</style>
</head>
<body>
<div class="grain"></div>

<nav>
  <div class="logo">NOCHTRA<span>.</span></div>
  <button class="toggle" id="toggleBtn" aria-pressed="false" aria-label="Toggle antara tampilan LUAR dan DALAM">
    <span class="toggle-label" id="toggleLabel">LUAR</span>
    <span class="toggle-track"><span class="toggle-knob"></span></span>
  </button>
</nav>

<header class="hero wrap">
  <div>
    <span class="eyebrow">Collection — Dual State</span>
    <h1>FRACTURED<br><span class="glitch-word" id="glitchWord">MIND</span></h1>
    <p class="tagline">"Two realities. One mind."</p>
    <p class="hero-desc">
      Di luar terlihat tenang. Di dalam pikirannya terus berisik.
      NOCHTRA DUAL STATE dibangun dari dua sisi yang sama-sama jujur —
      satu yang dunia lihat, satu yang cuma kamu yang tahu.
    </p>
    <p class="btn-note">Koleksi pertama NOCHTRA — dua sisi manusia, digambar jadi satu wajah.</p>
  </div>

  <div class="face-frame">
    <svg class="face-calm" viewBox="0 0 400 460" preserveAspectRatio="xMidYMid meet">
      <rect width="400" height="460" fill="#E6DCC3"/>
      <circle cx="200" cy="190" r="92" fill="#F2ECDC" stroke="#1B2A4A" stroke-width="3"/>
      <path d="M115 140 Q200 90 285 140" fill="none" stroke="#1B2A4A" stroke-width="3"/>
      <path d="M168 182 h20" stroke="#1B2A4A" stroke-width="4" stroke-linecap="round"/>
      <path d="M212 182 h20" stroke="#1B2A4A" stroke-width="4" stroke-linecap="round"/>
      <path d="M172 218 Q200 234 228 218" fill="none" stroke="#1B2A4A" stroke-width="3" stroke-linecap="round"/>
      <g>
        <rect x="288" y="96" width="70" height="54" rx="2" fill="#F2ECDC" stroke="#1B2A4A" stroke-width="2" transform="rotate(8 323 123)"/>
        <path d="M300 114 l8 8 14-16" fill="none" stroke="#1B2A4A" stroke-width="2.5" stroke-linecap="round" transform="rotate(8 323 123)"/>
        <path d="M300 132 h40" stroke="#1B2A4A" stroke-width="2" stroke-dasharray="3 4" transform="rotate(8 323 123)"/>
      </g>
      <text x="200" y="420" text-anchor="middle" font-family="Space Mono, monospace" font-size="13" fill="#1B2A4A" letter-spacing="1">"udah, gapapa kok. santai aja."</text>
    </svg>
    <svg class="face-chaos" viewBox="0 0 400 460" preserveAspectRatio="xMidYMid meet">
      <rect width="400" height="460" fill="#20241B"/>
      <circle cx="200" cy="190" r="92" fill="#333B29" stroke="#9BA37E" stroke-width="3"/>
      <path d="M170 165 l16 16 M186 165 l-16 16 M214 165 l16 16 M230 165 l-16 16" stroke="#9BA37E" stroke-width="3" stroke-linecap="round"/>
      <path d="M170 222 Q182 214 194 222 T218 222 T230 214" fill="none" stroke="#9BA37E" stroke-width="3" stroke-linecap="round"/>
      <path d="M130 130 Q160 150 140 170 Q180 160 165 195 Q210 175 205 210 Q250 190 240 225" fill="none" stroke="#5C6449" stroke-width="2" opacity=".8"/>
      <g fill="none" stroke="#9BA37E" stroke-width="2.5">
        <circle cx="90" cy="110" r="17"/>
        <text x="90" y="117" text-anchor="middle" font-family="Anton, sans-serif" font-size="20" fill="#9BA37E" stroke="none">!</text>
        <circle cx="330" cy="100" r="17"/>
        <text x="330" y="107" text-anchor="middle" font-family="Anton, sans-serif" font-size="18" fill="#9BA37E" stroke="none">?</text>
        <circle cx="60" cy="240" r="15"/>
        <path d="M60 232 v10 l8 5" stroke-linecap="round"/>
        <rect x="310" y="230" width="26" height="34" rx="4"/>
        <circle cx="323" cy="238" r="2.5" fill="#9BA37E" stroke="none"/>
      </g>
      <path d="M100 300 q100 -30 200 0" fill="none" stroke="#5C6449" stroke-width="1.5" stroke-dasharray="4 6" opacity=".7"/>
      <text x="200" y="420" text-anchor="middle" font-family="Space Mono, monospace" font-size="13" fill="#9BA37E" letter-spacing="1">"47 tab kebuka, katanya semua penting."</text>
    </svg>
    <span class="frame-tag" id="frameTag">LUAR: keliatan santai</span>
  </div>
</header>

<div class="seam"></div>

<section id="story" class="wrap">
  <div class="section-head reveal">
    <span class="eyebrow">Cerita Koleksi</span>
    <h2>Two Versions Of You</h2>
  </div>
  <div class="story">
    <div class="story-block reveal">
      <p>Setiap orang membawa dua versi dirinya. Yang satu dikenal dunia. Yang satu lagi dibangun diam-diam dari memori, ketakutan, kecemasan, dan keheningan.</p>
      <p class="story-quote">"Camouflage ini bukan dibuat untuk sembunyi dari orang lain. Ia dibuat dari semua hal yang tersembunyi di dalam."</p>
      <p>Setiap jahitan adalah usaha untuk menyatukan potongan-potongan itu. Karena pikiran yang retak sekalipun, tetap berhak untuk terasa utuh.</p>
      <p><em>Bukan luka. Bekas seseorang yang terus memperbaiki dirinya.</em></p>
    </div>
    <div class="camo-swatch reveal">
      <svg viewBox="0 0 400 300" width="100%" height="100%" preserveAspectRatio="xMidYMid slice">
        <rect width="400" height="300" fill="#333B29"/>
        <circle cx="130" cy="155" r="78" fill="#F2ECDC" stroke="#1B2A4A" stroke-width="3"/>
        <path d="M110 138 l14 14 M124 138 l-14 14 M154 138 l14 14 M168 138 l-14 14" stroke="#1B2A4A" stroke-width="3" stroke-linecap="round"/>
        <path d="M110 192 h48" stroke="#1B2A4A" stroke-width="3" stroke-linecap="round"/>
        <g transform="rotate(-8 235 90)">
          <rect x="195" y="60" width="80" height="58" rx="2" fill="#9BA37E" stroke="#1B2A4A" stroke-width="2"/>
          <text x="235" y="94" text-anchor="middle" font-family="Space Mono, monospace" font-size="11" fill="#1B2A4A">kenapa bumi bulat</text>
        </g>
        <g transform="rotate(6 300 170)">
          <rect x="258" y="140" width="86" height="58" rx="2" fill="#F2ECDC" stroke="#1B2A4A" stroke-width="2"/>
          <text x="301" y="166" text-anchor="middle" font-family="Space Mono, monospace" font-size="10.5" fill="#1B2A4A">chat dia dibales</text>
          <text x="301" y="180" text-anchor="middle" font-family="Space Mono, monospace" font-size="10.5" fill="#1B2A4A">gak ya?</text>
        </g>
        <g transform="rotate(-5 100 250)">
          <rect x="55" y="222" width="92" height="52" rx="2" fill="#8B8367" stroke="#1B2A4A" stroke-width="2"/>
          <text x="101" y="252" text-anchor="middle" font-family="Space Mono, monospace" font-size="10.5" fill="#1B2A4A">lupa matiin</text>
          <text x="101" y="265" text-anchor="middle" font-family="Space Mono, monospace" font-size="10.5" fill="#1B2A4A">kompor gak?</text>
        </g>
        <g transform="rotate(4 260 250)">
          <rect x="218" y="222" width="84" height="52" rx="2" fill="#20241B" stroke="#9BA37E" stroke-width="2"/>
          <text x="260" y="252" text-anchor="middle" font-family="Space Mono, monospace" font-size="10.5" fill="#9BA37E">besok mulai</text>
          <text x="260" y="265" text-anchor="middle" font-family="Space Mono, monospace" font-size="10.5" fill="#9BA37E">diet (lagi)</text>
        </g>
      </svg>
    </div>
  </div>
</section>

<div class="seam"></div>

<section id="philosophy" class="wrap">
  <div class="section-head reveal">
    <span class="eyebrow">Filosofi Desain</span>
    <h2>Empat Elemen, Satu Pikiran</h2>
    <p>Tiap detail di garmen ini bukan estetika kosong — semua punya alasan buat ada.</p>
  </div>
  <div class="phil-grid reveal">
    <div class="phil-card">
      <span class="phil-num">01</span>
      <h3>Cream</h3>
      <p>Sisi luar manusia. Tenang, hangat, stabil, dan dapat diterima lingkungan. Versi diri yang selalu diperlihatkan ke orang lain.</p>
      <p class="phil-joke">Warna paling gampang dipuji orang tua di acara keluarga.</p>
    </div>
    <div class="phil-card">
      <span class="phil-num">02</span>
      <h3>Panel Camo</h3>
      <p>Bukan camouflage militer — ini kumpulan memori, trauma, overthinking, dan ketakutan yang saling bertumpuk jadi pola rumit.</p>
      <p class="phil-joke">Diletakkan di samping, karena sisi itu paling jarang diperhatikan orang. Sama kayak grup chat yang isinya cuma kamu yang baca.</p>
    </div>
    <div class="phil-card">
      <span class="phil-num">03</span>
      <h3>Jahitan Biru Gelap</h3>
      <p>Exposed stitching bukan sekadar detail teknis — ini usaha menyatukan dua dunia. Setiap garis adalah proses, bukan luka.</p>
      <p class="phil-joke">Paling jujur dari semua jahitan di lemarimu. Nggak ada yang disembunyiin.</p>
    </div>
    <div class="phil-card">
      <span class="phil-num">04</span>
      <h3>Fake Dual Layer</h3>
      <p>Lapisan kedua menggambarkan dua identitas — satu untuk dunia, satu untuk diri sendiri. Tak pernah benar-benar terpisah, tak pernah benar-benar menyatu.</p>
      <p class="phil-joke">Sama seperti caption Instagram-mu vs isi Notes app-mu.</p>
    </div>
  </div>
</section>

<section id="diagnostic" class="diagnostic">
  <div class="wrap diag-wrap">
    <div class="reveal">
      <span class="eyebrow">Mental Diagnostic™</span>
      <h2>Apa Kata Panel Camo-mu?</h2>
      <p>Beginilah kira-kira isi kepala tiap orang jam segini — nggak ilmiah, cuma jujur. Sama kayak wajah "santai" di atas yang ternyata isinya 47 tab kebuka.</p>
    </div>
    <div class="terminal reveal">
      <div class="terminal-head">
        <span>fractured_mind.log</span>
        <span>● AKTIF</span>
      </div>
      <div class="terminal-body">
        <div class="terminal-line" style="opacity:1"><span class="ts">02:13</span> masih mikirin chat yang di-read 3 hari lalu</div>
        <div class="terminal-line" style="opacity:1"><span class="ts">03:47</span> replay adegan malu-maluin dari 2016, volume max</div>
        <div class="terminal-line" style="opacity:1"><span class="ts">09:00</span> kerja, tapi otak lagi buka tab lain</div>
        <div class="terminal-line" style="opacity:1"><span class="ts">14:20</span> 'kayaknya tadi aku salah ngomong deh'</div>
        <div class="terminal-line" style="opacity:1"><span class="ts">23:59</span> overthinking soal overthinking</div>
        <div class="terminal-line" style="opacity:1"><span class="ts">--:--</span> diagnosis: manusia, dan itu udah cukup.<span class="terminal-cursor"></span></div>
      </div>
    </div>
  </div>
</section>

<div class="seam"></div>

<section id="roadmap" class="wrap">
  <div class="section-head reveal">
    <span class="eyebrow">Perjalanan Identitas NOCHTRA</span>
    <h2>Bukan Cuma Produk</h2>
    <p>Satu cerita yang sama: apa yang terjadi saat pikiran mulai retak, sinyal ke diri sendiri putus, dan seseorang mencoba menyatukan lagi keduanya.</p>
  </div>
  <div class="roadmap reveal">
    <div class="rm-item">
      <span class="rm-num">01</span>
      <div>
        <h3 class="rm-title">Dual State : Fractured Mind</h3>
        <p class="rm-desc">Jembatan antara "pikiran yang mulai retak" dan "kehilangan koneksi terhadap diri sendiri." Bisa dibaca sebagai titik awal (Genesis) atau titik tengah — kami sendiri masih menimbang, dan menurut kami itu justru pas dengan temanya.</p>
        <span class="rm-tag">Sedang berlangsung</span>
      </div>
    </div>
    <div class="rm-item">
      <span class="rm-num">02</span>
      <div>
        <h3 class="rm-title">SOON</h3>
        <p class="rm-desc">Momen saat seseorang ????.</p>
      </div>
    </div>
    <div class="rm-item current">
      <span class="rm-num">00</span>
      <div>
        <h3 class="rm-title">??????</h3>
        <p class="rm-desc">//</p>
      </div>
    </div>
  </div>
</section>

<div class="seam"></div>

<section id="faq" class="wrap">
  <div class="section-head reveal">
    <span class="eyebrow">Sebelum Kamu Overthinking Lagi</span>
    <h2>FAQ</h2>
  </div>
  <div class="faq reveal">
    <div class="faq-item">
      <div class="faq-q"><span>Bahannya apa?</span></div>
      <div class="faq-a" style="max-height:none; padding-top:12px;">Cream panel: 100% cotton combed 20s, hangat kayak alasan yang kamu siapin sebelum minta maaf. Camo panel: dryfit jarum, kuat menahan tekanan — sama kayak kamu tiap Senin.</div>
    </div>
    <div class="faq-item">
      <div class="faq-q"><span>Cara cucinya gimana?</span></div>
      <div class="faq-a" style="max-height:none; padding-top:12px;">Cuci air dingin, Hindari pemutih, jangan diperas keras-keras, Jangan disetrika langsung dibagian sablon, Jangan disikat, Hindari mesin pengering, Hindari air panas. Pikiran boleh panas, bajunya jangan.</div>
    </div>
    <div class="faq-item">
      <div class="faq-q"><span>Bingung pilih size?</span></div>
      <div class="faq-a" style="max-height:none; padding-top:12px;">Kalau kamu masih ragu size apa, kemungkinan besar kamu juga masih ragu banyak hal lain malam ini. Ambil size M dulu, sisanya kita pikirin bareng nanti.</div>
    </div>
    <div class="faq-item">
      <div class="faq-q"><span>Kapan restock?</span></div>
      <div class="faq-a" style="max-height:none; padding-top:12px;">Secepat produksi panel camo-nya selesai dijahit. Info lanjut menyusul nanti.</div>
    </div>
  </div>
</section>

<footer>
  <div class="wrap">
    <div class="foot-grid">
      <div>
        <div class="foot-logo">NOCHTRA<span style="color:var(--navy-bright);">.</span></div>
        <p class="foot-desc">Dua realita. Satu pikiran. Kami bikin baju, tapi sebenarnya kami cuma nyoba bilang: nggak apa-apa kalau di dalam kepalamu masih berisik.</p>
      </div>
      <div class="foot-col">
        <h4>Koleksi</h4>
        <p class="foot-desc" style="margin-top:0;">Dual State : Fractured Mind<br>02 SOON<br>00–00 ????</p>
      </div>
      <div class="foot-col">
        <h4>Catatan</h4>
        <p class="foot-desc" style="margin-top:0;">Syarat &amp; ketentuan yang jarang dibaca, kita ngerti kok. Kontak — balasnya kadang lambat, kayak kamu bales chat gebetan.</p>
      </div>
    </div>
    <div class="foot-bottom">
      <span>© 2026 NOCHTRA. Semua hak cipta dilindungi, kecuali hak untuk berhenti mikir jam 2 pagi.</span>
      <span id="stateFooter">Status kamu sekarang: LUAR — tenang.</span>
    </div>
  </div>
</footer>

<script>
  // dual state toggle
  const toggleBtn = document.getElementById('toggleBtn');
  const toggleLabel = document.getElementById('toggleLabel');
  const glitchWord = document.getElementById('glitchWord');
  const stateFooter = document.getElementById('stateFooter');
  const frameTag = document.getElementById('frameTag');
  let inside = false;
  const insideWords = ['MIND','∴MIИD∴','M!ND','MIND_','#MIND'];

  toggleBtn.addEventListener('click', () => {
    inside = !inside;
    document.body.classList.toggle('inside', inside);
    toggleBtn.setAttribute('aria-pressed', inside);
    toggleLabel.textContent = inside ? 'DALAM' : 'LUAR';
    frameTag.textContent = inside ? 'DALAM: 47 tab kebuka' : 'LUAR: keliatan santai';
    stateFooter.textContent = inside
      ? 'Status kamu sekarang: DALAM — sedikit berisik, itu wajar.'
      : 'Status kamu sekarang: LUAR — tenang.';
    if (inside){
      let i = 0;
      const iv = setInterval(() => {
        glitchWord.textContent = insideWords[i % insideWords.length];
        i++;
        if (i > 6){ clearInterval(iv); glitchWord.textContent = 'MIND'; }
      }, 90);
    } else {
      glitchWord.textContent = 'MIND';
    }
  });

  // scroll reveal
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible'); });
  }, { threshold: .15 });
  document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
</script>
</body>
</html><!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NOCHTRA — DUAL STATE : FRACTURED MIND</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Anton&family=Space+Mono:ital,wght@0,400;0,700;1,400&display=swap" rel="stylesheet">
<style>
  :root{
    --cream:#F2ECDC;
    --cream-dim:#E6DCC3;
    --ink:#1C1A14;
    --navy:#1B2A4A;
    --navy-bright:#3557A0;
    --camo-1:#333B29;
    --camo-2:#5C6449;
    --camo-3:#8B8367;
    --camo-4:#20241B;
    --camo-5:#9BA37E;
    --stitch: var(--navy);
    --grain-opacity: .05;
  }
  *{box-sizing:border-box; margin:0; padding:0;}
  html{scroll-behavior:smooth;}
  body{
    background:var(--cream);
    color:var(--ink);
    font-family:'Space Mono', monospace;
    overflow-x:hidden;
    transition:background .6s ease, color .6s ease;
  }
  body.inside{
    background:var(--camo-4);
    color:var(--cream-dim);
  }
  h1,h2,h3, .display{
    font-family:'Anton', sans-serif;
    font-weight:400;
    letter-spacing:.01em;
    text-transform:uppercase;
    line-height:.95;
  }
  a{color:inherit;}
  .wrap{max-width:1180px; margin:0 auto; padding:0 28px;}
  ::selection{background:var(--navy); color:var(--cream);}

  /* grain overlay */
  .grain{
    position:fixed; inset:0; pointer-events:none; z-index:999;
    opacity:var(--grain-opacity); mix-blend-mode:multiply;
    background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='120' height='120'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='2' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
  }
  body.inside .grain{opacity:.14; mix-blend-mode:screen;}

  /* stitched seam divider */
  .seam{
    width:100%; height:2px; position:relative;
    background:repeating-linear-gradient(90deg, var(--stitch) 0 10px, transparent 10px 18px);
    opacity:.55; margin:0 0;
  }

  /* ===== NAV ===== */
  nav{
    position:sticky; top:0; z-index:100;
    display:flex; align-items:center; justify-content:space-between;
    padding:18px 28px;
    background:var(--cream); border-bottom:2px dashed var(--navy);
    transition:background .6s ease, border-color .6s ease;
  }
  body.inside nav{background:var(--camo-4); border-bottom-color:var(--camo-5);}
  .logo{font-family:'Anton',sans-serif; font-size:22px; letter-spacing:.06em;}
  .logo span{color:var(--navy-bright);}
  button:focus-visible, .toggle:focus-visible{outline:2px solid var(--navy-bright); outline-offset:3px;}

  /* toggle switch */
  .toggle{
    display:flex; align-items:center; gap:8px; cursor:pointer;
    border:2px solid var(--navy); border-radius:30px; padding:4px 6px;
    background:transparent; font-family:'Space Mono',monospace;
  }
  .toggle-label{font-size:10px; letter-spacing:.1em; padding:0 4px;}
  .toggle-track{
    width:38px; height:20px; border-radius:20px; background:var(--navy);
    position:relative; flex-shrink:0;
  }
  .toggle-knob{
    position:absolute; top:2px; left:2px; width:16px; height:16px;
    border-radius:50%; background:var(--cream); transition:left .35s cubic-bezier(.6,.1,.2,1);
  }
  body.inside .toggle-knob{left:20px; background:var(--camo-5);}

  /* ===== HERO ===== */
  .hero{
    padding:70px 0 40px; position:relative;
    display:grid; grid-template-columns:1.15fr .85fr; gap:40px; align-items:center;
  }
  .eyebrow{
    font-size:11px; letter-spacing:.2em; text-transform:uppercase;
    color:var(--navy-bright); margin-bottom:16px; display:block;
  }
  body.inside .eyebrow{color:var(--camo-5);}
  .hero h1{font-size:clamp(46px,7.2vw,96px);}
  .hero h1 .glitch-word{position:relative; display:inline-block;}
  .tagline{
    font-family:'Anton',sans-serif; text-transform:none; font-size:clamp(18px,2vw,24px);
    margin-top:18px; opacity:.85;
  }
  .hero-desc{max-width:480px; font-size:14px; line-height:1.75; margin-top:22px; opacity:.85;}
  .btn-note{font-size:11px; opacity:.6; margin-top:26px; letter-spacing:.02em;}

  /* face doodle visual */
  .face-frame{
    position:relative; aspect-ratio:3/4; border:2px solid var(--navy);
    overflow:hidden; background:var(--cream-dim);
  }
  body.inside .face-frame{border-color:var(--camo-5);}
  .face-frame svg{position:absolute; inset:0; width:100%; height:100%; display:block; transition:opacity .5s ease;}
  .face-chaos{opacity:0;}
  body.inside .face-calm{opacity:0;}
  body.inside .face-chaos{opacity:1;}
  .frame-tag{
    position:absolute; bottom:10px; left:10px; font-size:9px; letter-spacing:.08em;
    background:var(--navy); color:var(--cream); padding:5px 9px; z-index:2;
  }
  body.inside .frame-tag{background:var(--camo-5); color:var(--camo-4);}

  /* ===== SECTION GENERIC ===== */
  section{padding:80px 0;}
  .section-head{margin-bottom:44px; max-width:640px;}
  .section-head .eyebrow{margin-bottom:10px;}
  .section-head h2{font-size:clamp(30px,4.5vw,52px);}
  .section-head p{font-size:14px; line-height:1.7; opacity:.8; margin-top:14px;}

  /* ===== STORY ===== */
  .story{display:grid; grid-template-columns:1fr 1fr; gap:50px;}
  .story-block p{font-size:14px; line-height:1.85; margin-bottom:16px; opacity:.88;}
  .story-block em{font-style:italic; color:var(--navy-bright);}
  .story-quote{
    font-family:'Anton',sans-serif; text-transform:none; font-size:20px; line-height:1.4;
    border-left:3px solid var(--navy); padding-left:20px; margin:24px 0;
  }
  .camo-swatch{
    width:100%; aspect-ratio:4/3; position:relative; overflow:hidden;
    border:2px solid var(--navy);
  }

  /* ===== PHILOSOPHY CARDS ===== */
  .phil-grid{display:grid; grid-template-columns:repeat(4,1fr); gap:2px; background:var(--navy);}
  body.inside .phil-grid{background:var(--camo-5);}
  .phil-card{
    background:var(--cream); padding:30px 24px; min-height:280px;
    display:flex; flex-direction:column; gap:12px;
  }
  body.inside .phil-card{background:var(--camo-4);}
  .phil-num{font-family:'Anton',sans-serif; font-size:13px; color:var(--navy-bright);}
  .phil-card h3{font-size:20px; margin-top:4px;}
  .phil-card p{font-size:12.5px; line-height:1.7; opacity:.82;}
  .phil-joke{
    margin-top:auto; font-size:11px; font-style:italic; opacity:.6;
    border-top:1px dashed var(--navy); padding-top:10px;
  }
  body.inside .phil-joke{border-top-color:var(--camo-5);}

  /* ===== DIAGNOSTIC TERMINAL ===== */
  .diagnostic{
    background:var(--navy); color:var(--cream); padding:60px 0;
  }
  body.inside .diagnostic{background:var(--camo-4);}
  .diag-wrap{display:grid; grid-template-columns:.9fr 1.1fr; gap:44px; align-items:start;}
  .diag-wrap h2{color:var(--cream); font-size:clamp(26px,4vw,44px);}
  .diag-wrap p{font-size:13px; line-height:1.8; opacity:.8; margin-top:14px; max-width:400px;}
  .terminal{
    background:#0E1420; border:2px solid var(--navy-bright); padding:18px 20px;
    font-size:12.5px; line-height:1.9; min-height:260px; position:relative;
  }
  .terminal-head{
    display:flex; justify-content:space-between; align-items:center;
    border-bottom:1px dashed rgba(255,255,255,.2); padding-bottom:8px; margin-bottom:10px;
    font-size:10px; letter-spacing:.1em; opacity:.6; text-transform:uppercase;
  }
  .terminal-body{min-height:190px;}
  .terminal-line{opacity:0; animation:appear .4s forwards;}
  .terminal-line .ts{color:#7FA7E8; margin-right:8px;}
  @keyframes appear{to{opacity:1;}}
  .terminal-cursor{display:inline-block; width:7px; height:13px; background:var(--cream); animation:blink 1s step-end infinite; vertical-align:middle;}
  @keyframes blink{50%{opacity:0;}}
  /* ===== ROADMAP ===== */
  .roadmap{display:flex; flex-direction:column; gap:0;}
  .rm-item{
    display:grid; grid-template-columns:90px 1fr; gap:26px;
    padding:26px 0; border-top:2px dashed var(--navy); align-items:start;
  }
  body.inside .rm-item{border-top-color:var(--camo-5);}
  .rm-item:last-child{border-bottom:2px dashed var(--navy);}
  body.inside .rm-item:last-child{border-bottom-color:var(--camo-5);}
  .rm-num{font-family:'Anton',sans-serif; font-size:34px; color:var(--navy-bright); line-height:1;}
  .rm-item.current .rm-num{color:var(--ink);}
  body.inside .rm-item.current .rm-num{color:var(--cream-dim);}
  .rm-title{font-family:'Anton',sans-serif; font-size:20px; text-transform:uppercase;}
  .rm-desc{font-size:12.5px; line-height:1.7; opacity:.78; margin-top:8px; max-width:600px;}
  .rm-tag{
    display:inline-block; font-size:9px; letter-spacing:.08em; text-transform:uppercase;
    border:1px solid var(--navy); padding:3px 8px; margin-top:10px;
  }
  body.inside .rm-tag{border-color:var(--camo-5);}

  /* ===== FAQ ===== */
  .faq{max-width:720px;}
  .faq-item{border-top:1px solid var(--navy); padding:18px 0;}
  body.inside .faq-item{border-top-color:var(--camo-5);}
  .faq-item:last-child{border-bottom:1px solid var(--navy);}
  body.inside .faq-item:last-child{border-bottom-color:var(--camo-5);}
  .faq-q{
    font-family:'Anton',sans-serif; font-size:15px; text-transform:none;
  }
  .faq-a{
    font-size:12.5px; line-height:1.75; opacity:.8;
  }

  /* ===== FOOTER ===== */
  footer{padding:60px 0 30px; border-top:2px solid var(--navy);}
  body.inside footer{border-top-color:var(--camo-5);}
  .foot-grid{display:grid; grid-template-columns:1.2fr .8fr .8fr; gap:40px; margin-bottom:40px;}
  .foot-logo{font-family:'Anton',sans-serif; font-size:26px;}
  .foot-desc{font-size:12px; line-height:1.7; opacity:.75; margin-top:10px; max-width:340px;}
  .foot-col h4{font-size:10px; letter-spacing:.1em; text-transform:uppercase; opacity:.6; margin-bottom:12px;}
  .foot-bottom{
    display:flex; justify-content:space-between; flex-wrap:wrap; gap:10px;
    font-size:10.5px; opacity:.55; padding-top:20px; border-top:1px dashed var(--navy);
  }
  body.inside .foot-bottom{border-top-color:var(--camo-5);}

  /* reveal on scroll */
  .reveal{opacity:0; transform:translateY(24px); transition:opacity .7s ease, transform .7s ease;}
  .reveal.visible{opacity:1; transform:translateY(0);}

  @media (prefers-reduced-motion: reduce){
    *{animation:none !important; transition:none !important;}
  }

  @media (max-width: 880px){
    .hero{grid-template-columns:1fr; padding-top:40px;}
    .story{grid-template-columns:1fr;}
    .phil-grid{grid-template-columns:1fr 1fr;}
    .diag-wrap{grid-template-columns:1fr;}
    .foot-grid{grid-template-columns:1fr;}
    .rm-item{grid-template-columns:50px 1fr;}
  }
</style>
</head>
<body>
<div class="grain"></div>

<nav>
  <div class="logo">NOCHTRA<span>.</span></div>
  <button class="toggle" id="toggleBtn" aria-pressed="false" aria-label="Toggle antara tampilan LUAR dan DALAM">
    <span class="toggle-label" id="toggleLabel">LUAR</span>
    <span class="toggle-track"><span class="toggle-knob"></span></span>
  </button>
</nav>

<header class="hero wrap">
  <div>
    <span class="eyebrow">Collection — Dual State</span>
    <h1>FRACTURED<br><span class="glitch-word" id="glitchWord">MIND</span></h1>
    <p class="tagline">"Two realities. One mind."</p>
    <p class="hero-desc">
      Di luar terlihat tenang. Di dalam pikirannya terus berisik.
      NOCHTRA DUAL STATE dibangun dari dua sisi yang sama-sama jujur —
      satu yang dunia lihat, satu yang cuma kamu yang tahu.
    </p>
    <p class="btn-note">Koleksi pertama NOCHTRA — dua sisi manusia, digambar jadi satu wajah.</p>
  </div>

  <div class="face-frame">
    <svg class="face-calm" viewBox="0 0 400 460" preserveAspectRatio="xMidYMid meet">
      <rect width="400" height="460" fill="#E6DCC3"/>
      <circle cx="200" cy="190" r="92" fill="#F2ECDC" stroke="#1B2A4A" stroke-width="3"/>
      <path d="M115 140 Q200 90 285 140" fill="none" stroke="#1B2A4A" stroke-width="3"/>
      <path d="M168 182 h20" stroke="#1B2A4A" stroke-width="4" stroke-linecap="round"/>
      <path d="M212 182 h20" stroke="#1B2A4A" stroke-width="4" stroke-linecap="round"/>
      <path d="M172 218 Q200 234 228 218" fill="none" stroke="#1B2A4A" stroke-width="3" stroke-linecap="round"/>
      <g>
        <rect x="288" y="96" width="70" height="54" rx="2" fill="#F2ECDC" stroke="#1B2A4A" stroke-width="2" transform="rotate(8 323 123)"/>
        <path d="M300 114 l8 8 14-16" fill="none" stroke="#1B2A4A" stroke-width="2.5" stroke-linecap="round" transform="rotate(8 323 123)"/>
        <path d="M300 132 h40" stroke="#1B2A4A" stroke-width="2" stroke-dasharray="3 4" transform="rotate(8 323 123)"/>
      </g>
      <text x="200" y="420" text-anchor="middle" font-family="Space Mono, monospace" font-size="13" fill="#1B2A4A" letter-spacing="1">"udah, gapapa kok. santai aja."</text>
    </svg>
    <svg class="face-chaos" viewBox="0 0 400 460" preserveAspectRatio="xMidYMid meet">
      <rect width="400" height="460" fill="#20241B"/>
      <circle cx="200" cy="190" r="92" fill="#333B29" stroke="#9BA37E" stroke-width="3"/>
      <path d="M170 165 l16 16 M186 165 l-16 16 M214 165 l16 16 M230 165 l-16 16" stroke="#9BA37E" stroke-width="3" stroke-linecap="round"/>
      <path d="M170 222 Q182 214 194 222 T218 222 T230 214" fill="none" stroke="#9BA37E" stroke-width="3" stroke-linecap="round"/>
      <path d="M130 130 Q160 150 140 170 Q180 160 165 195 Q210 175 205 210 Q250 190 240 225" fill="none" stroke="#5C6449" stroke-width="2" opacity=".8"/>
      <g fill="none" stroke="#9BA37E" stroke-width="2.5">
        <circle cx="90" cy="110" r="17"/>
        <text x="90" y="117" text-anchor="middle" font-family="Anton, sans-serif" font-size="20" fill="#9BA37E" stroke="none">!</text>
        <circle cx="330" cy="100" r="17"/>
        <text x="330" y="107" text-anchor="middle" font-family="Anton, sans-serif" font-size="18" fill="#9BA37E" stroke="none">?</text>
        <circle cx="60" cy="240" r="15"/>
        <path d="M60 232 v10 l8 5" stroke-linecap="round"/>
        <rect x="310" y="230" width="26" height="34" rx="4"/>
        <circle cx="323" cy="238" r="2.5" fill="#9BA37E" stroke="none"/>
      </g>
      <path d="M100 300 q100 -30 200 0" fill="none" stroke="#5C6449" stroke-width="1.5" stroke-dasharray="4 6" opacity=".7"/>
      <text x="200" y="420" text-anchor="middle" font-family="Space Mono, monospace" font-size="13" fill="#9BA37E" letter-spacing="1">"47 tab kebuka, katanya semua penting."</text>
    </svg>
    <span class="frame-tag" id="frameTag">LUAR: keliatan santai</span>
  </div>
</header>

<div class="seam"></div>

<section id="story" class="wrap">
  <div class="section-head reveal">
    <span class="eyebrow">Cerita Koleksi</span>
    <h2>Two Versions Of You</h2>
  </div>
  <div class="story">
    <div class="story-block reveal">
      <p>Setiap orang membawa dua versi dirinya. Yang satu dikenal dunia. Yang satu lagi dibangun diam-diam dari memori, ketakutan, kecemasan, dan keheningan.</p>
      <p class="story-quote">"Camouflage ini bukan dibuat untuk sembunyi dari orang lain. Ia dibuat dari semua hal yang tersembunyi di dalam."</p>
      <p>Setiap jahitan adalah usaha untuk menyatukan potongan-potongan itu. Karena pikiran yang retak sekalipun, tetap berhak untuk terasa utuh.</p>
      <p><em>Bukan luka. Bekas seseorang yang terus memperbaiki dirinya.</em></p>
    </div>
    <div class="camo-swatch reveal">
      <svg viewBox="0 0 400 300" width="100%" height="100%" preserveAspectRatio="xMidYMid slice">
        <rect width="400" height="300" fill="#333B29"/>
        <circle cx="130" cy="155" r="78" fill="#F2ECDC" stroke="#1B2A4A" stroke-width="3"/>
        <path d="M110 138 l14 14 M124 138 l-14 14 M154 138 l14 14 M168 138 l-14 14" stroke="#1B2A4A" stroke-width="3" stroke-linecap="round"/>
        <path d="M110 192 h48" stroke="#1B2A4A" stroke-width="3" stroke-linecap="round"/>
        <g transform="rotate(-8 235 90)">
          <rect x="195" y="60" width="80" height="58" rx="2" fill="#9BA37E" stroke="#1B2A4A" stroke-width="2"/>
          <text x="235" y="94" text-anchor="middle" font-family="Space Mono, monospace" font-size="11" fill="#1B2A4A">kenapa bumi bulat</text>
        </g>
        <g transform="rotate(6 300 170)">
          <rect x="258" y="140" width="86" height="58" rx="2" fill="#F2ECDC" stroke="#1B2A4A" stroke-width="2"/>
          <text x="301" y="166" text-anchor="middle" font-family="Space Mono, monospace" font-size="10.5" fill="#1B2A4A">chat dia dibales</text>
          <text x="301" y="180" text-anchor="middle" font-family="Space Mono, monospace" font-size="10.5" fill="#1B2A4A">gak ya?</text>
        </g>
        <g transform="rotate(-5 100 250)">
          <rect x="55" y="222" width="92" height="52" rx="2" fill="#8B8367" stroke="#1B2A4A" stroke-width="2"/>
          <text x="101" y="252" text-anchor="middle" font-family="Space Mono, monospace" font-size="10.5" fill="#1B2A4A">lupa matiin</text>
          <text x="101" y="265" text-anchor="middle" font-family="Space Mono, monospace" font-size="10.5" fill="#1B2A4A">kompor gak?</text>
        </g>
        <g transform="rotate(4 260 250)">
          <rect x="218" y="222" width="84" height="52" rx="2" fill="#20241B" stroke="#9BA37E" stroke-width="2"/>
          <text x="260" y="252" text-anchor="middle" font-family="Space Mono, monospace" font-size="10.5" fill="#9BA37E">besok mulai</text>
          <text x="260" y="265" text-anchor="middle" font-family="Space Mono, monospace" font-size="10.5" fill="#9BA37E">diet (lagi)</text>
        </g>
      </svg>
    </div>
  </div>
</section>

<div class="seam"></div>

<section id="philosophy" class="wrap">
  <div class="section-head reveal">
    <span class="eyebrow">Filosofi Desain</span>
    <h2>Empat Elemen, Satu Pikiran</h2>
    <p>Tiap detail di garmen ini bukan estetika kosong — semua punya alasan buat ada.</p>
  </div>
  <div class="phil-grid reveal">
    <div class="phil-card">
      <span class="phil-num">01</span>
      <h3>Cream</h3>
      <p>Sisi luar manusia. Tenang, hangat, stabil, dan dapat diterima lingkungan. Versi diri yang selalu diperlihatkan ke orang lain.</p>
      <p class="phil-joke">Warna paling gampang dipuji orang tua di acara keluarga.</p>
    </div>
    <div class="phil-card">
      <span class="phil-num">02</span>
      <h3>Panel Camo</h3>
      <p>Bukan camouflage militer — ini kumpulan memori, trauma, overthinking, dan ketakutan yang saling bertumpuk jadi pola rumit.</p>
      <p class="phil-joke">Diletakkan di samping, karena sisi itu paling jarang diperhatikan orang. Sama kayak grup chat yang isinya cuma kamu yang baca.</p>
    </div>
    <div class="phil-card">
      <span class="phil-num">03</span>
      <h3>Jahitan Biru Gelap</h3>
      <p>Exposed stitching bukan sekadar detail teknis — ini usaha menyatukan dua dunia. Setiap garis adalah proses, bukan luka.</p>
      <p class="phil-joke">Paling jujur dari semua jahitan di lemarimu. Nggak ada yang disembunyiin.</p>
    </div>
    <div class="phil-card">
      <span class="phil-num">04</span>
      <h3>Fake Dual Layer</h3>
      <p>Lapisan kedua menggambarkan dua identitas — satu untuk dunia, satu untuk diri sendiri. Tak pernah benar-benar terpisah, tak pernah benar-benar menyatu.</p>
      <p class="phil-joke">Sama seperti caption Instagram-mu vs isi Notes app-mu.</p>
    </div>
  </div>
</section>

<section id="diagnostic" class="diagnostic">
  <div class="wrap diag-wrap">
    <div class="reveal">
      <span class="eyebrow">Mental Diagnostic™</span>
      <h2>Apa Kata Panel Camo-mu?</h2>
      <p>Beginilah kira-kira isi kepala tiap orang jam segini — nggak ilmiah, cuma jujur. Sama kayak wajah "santai" di atas yang ternyata isinya 47 tab kebuka.</p>
    </div>
    <div class="terminal reveal">
      <div class="terminal-head">
        <span>fractured_mind.log</span>
        <span>● AKTIF</span>
      </div>
      <div class="terminal-body">
        <div class="terminal-line" style="opacity:1"><span class="ts">02:13</span> masih mikirin chat yang di-read 3 hari lalu</div>
        <div class="terminal-line" style="opacity:1"><span class="ts">03:47</span> replay adegan malu-maluin dari 2016, volume max</div>
        <div class="terminal-line" style="opacity:1"><span class="ts">09:00</span> kerja, tapi otak lagi buka tab lain</div>
        <div class="terminal-line" style="opacity:1"><span class="ts">14:20</span> 'kayaknya tadi aku salah ngomong deh'</div>
        <div class="terminal-line" style="opacity:1"><span class="ts">23:59</span> overthinking soal overthinking</div>
        <div class="terminal-line" style="opacity:1"><span class="ts">--:--</span> diagnosis: manusia, dan itu udah cukup.<span class="terminal-cursor"></span></div>
      </div>
    </div>
  </div>
</section>

<div class="seam"></div>

<section id="roadmap" class="wrap">
  <div class="section-head reveal">
    <span class="eyebrow">Perjalanan Identitas NOCHTRA</span>
    <h2>Bukan Cuma Produk</h2>
    <p>Satu cerita yang sama: apa yang terjadi saat pikiran mulai retak, sinyal ke diri sendiri putus, dan seseorang mencoba menyatukan lagi keduanya.</p>
  </div>
  <div class="roadmap reveal">
    <div class="rm-item">
      <span class="rm-num">01</span>
      <div>
        <h3 class="rm-title">Dual State : Fractured Mind</h3>
        <p class="rm-desc">Jembatan antara "pikiran yang mulai retak" dan "kehilangan koneksi terhadap diri sendiri." Bisa dibaca sebagai titik awal (Genesis) atau titik tengah — kami sendiri masih menimbang, dan menurut kami itu justru pas dengan temanya.</p>
        <span class="rm-tag">Sedang berlangsung</span>
      </div>
    </div>
    <div class="rm-item">
      <span class="rm-num">02</span>
      <div>
        <h3 class="rm-title">SOON</h3>
        <p class="rm-desc">Momen saat seseorang ????.</p>
      </div>
    </div>
    <div class="rm-item current">
      <span class="rm-num">00</span>
      <div>
        <h3 class="rm-title">??????</h3>
        <p class="rm-desc">//</p>
      </div>
    </div>
  </div>
</section>

<div class="seam"></div>

<section id="faq" class="wrap">
  <div class="section-head reveal">
    <span class="eyebrow">Sebelum Kamu Overthinking Lagi</span>
    <h2>FAQ</h2>
  </div>
  <div class="faq reveal">
    <div class="faq-item">
      <div class="faq-q"><span>Bahannya apa?</span></div>
      <div class="faq-a" style="max-height:none; padding-top:12px;">Cream panel: 100% cotton combed 20s, hangat kayak alasan yang kamu siapin sebelum minta maaf. Camo panel: dryfit jarum, kuat menahan tekanan — sama kayak kamu tiap Senin.</div>
    </div>
    <div class="faq-item">
      <div class="faq-q"><span>Cara cucinya gimana?</span></div>
      <div class="faq-a" style="max-height:none; padding-top:12px;">Cuci air dingin, Hindari pemutih, jangan diperas keras-keras, Jangan disetrika langsung dibagian sablon, Jangan disikat, Hindari mesin pengering, Hindari air panas. Pikiran boleh panas, bajunya jangan.</div>
    </div>
    <div class="faq-item">
      <div class="faq-q"><span>Bingung pilih size?</span></div>
      <div class="faq-a" style="max-height:none; padding-top:12px;">Kalau kamu masih ragu size apa, kemungkinan besar kamu juga masih ragu banyak hal lain malam ini. Ambil size M dulu, sisanya kita pikirin bareng nanti.</div>
    </div>
    <div class="faq-item">
      <div class="faq-q"><span>Kapan restock?</span></div>
      <div class="faq-a" style="max-height:none; padding-top:12px;">Secepat produksi panel camo-nya selesai dijahit. Info lanjut menyusul nanti.</div>
    </div>
  </div>
</section>

<footer>
  <div class="wrap">
    <div class="foot-grid">
      <div>
        <div class="foot-logo">NOCHTRA<span style="color:var(--navy-bright);">.</span></div>
        <p class="foot-desc">Dua realita. Satu pikiran. Kami bikin baju, tapi sebenarnya kami cuma nyoba bilang: nggak apa-apa kalau di dalam kepalamu masih berisik.</p>
      </div>
      <div class="foot-col">
        <h4>Koleksi</h4>
        <p class="foot-desc" style="margin-top:0;">Dual State : Fractured Mind<br>02 SOON<br>00–00 ????</p>
      </div>
      <div class="foot-col">
        <h4>Catatan</h4>
        <p class="foot-desc" style="margin-top:0;">Syarat &amp; ketentuan yang jarang dibaca, kita ngerti kok. Kontak — balasnya kadang lambat, kayak kamu bales chat gebetan.</p>
      </div>
    </div>
    <div class="foot-bottom">
      <span>© 2026 NOCHTRA. Semua hak cipta dilindungi, kecuali hak untuk berhenti mikir jam 2 pagi.</span>
      <span id="stateFooter">Status kamu sekarang: LUAR — tenang.</span>
    </div>
  </div>
</footer>

<script>
  // dual state toggle
  const toggleBtn = document.getElementById('toggleBtn');
  const toggleLabel = document.getElementById('toggleLabel');
  const glitchWord = document.getElementById('glitchWord');
  const stateFooter = document.getElementById('stateFooter');
  const frameTag = document.getElementById('frameTag');
  let inside = false;
  const insideWords = ['MIND','∴MIИD∴','M!ND','MIND_','#MIND'];

  toggleBtn.addEventListener('click', () => {
    inside = !inside;
    document.body.classList.toggle('inside', inside);
    toggleBtn.setAttribute('aria-pressed', inside);
    toggleLabel.textContent = inside ? 'DALAM' : 'LUAR';
    frameTag.textContent = inside ? 'DALAM: 47 tab kebuka' : 'LUAR: keliatan santai';
    stateFooter.textContent = inside
      ? 'Status kamu sekarang: DALAM — sedikit berisik, itu wajar.'
      : 'Status kamu sekarang: LUAR — tenang.';
    if (inside){
      let i = 0;
      const iv = setInterval(() => {
        glitchWord.textContent = insideWords[i % insideWords.length];
        i++;
        if (i > 6){ clearInterval(iv); glitchWord.textContent = 'MIND'; }
      }, 90);
    } else {
      glitchWord.textContent = 'MIND';
    }
  });

  // scroll reveal
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible'); });
  }, { threshold: .15 });
  document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
</script>
</body>
</html>

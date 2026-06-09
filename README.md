[index (3).html](https://github.com/user-attachments/files/28748606/index.3.html)
<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>Marogien — Marocain ou Algérien ?</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=Noto+Sans+Arabic:wght@400;600&display=swap" rel="stylesheet"/>
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --ma:#c1272d;--dz:#007229;
  --bg:#0e0e0e;--surface:#1a1a1a;--surface2:#242424;
  --border:rgba(255,255,255,0.08);--text:#f0ece4;--muted:rgba(240,236,228,0.45);
  --radius:20px;--font:'Syne',sans-serif;
}
html,body{height:100%;background:var(--bg);color:var(--text);font-family:var(--font);overflow-x:hidden}
#app{min-height:100vh;display:flex;flex-direction:column;align-items:center;padding:0 16px 40px;max-width:480px;margin:0 auto}
#header{width:100%;display:flex;align-items:center;justify-content:space-between;padding:20px 0 12px}
#logo{font-size:26px;font-weight:800;letter-spacing:-1px}
#logo .ma{color:var(--ma)}#logo .dz{color:var(--dz)}
#hud{display:flex;align-items:center;gap:10px}
.hud-pill{background:var(--surface);border:1px solid var(--border);border-radius:30px;padding:5px 12px;font-size:13px;font-weight:600;color:var(--muted)}
.hud-pill span{color:var(--text)}
#settings-btn{width:36px;height:36px;background:var(--surface);border:1px solid var(--border);border-radius:50%;display:flex;align-items:center;justify-content:center;cursor:pointer;font-size:18px;transition:opacity .2s}
#settings-btn:hover{opacity:.7}
#progress-wrap{width:100%;height:3px;background:var(--surface2);border-radius:3px;overflow:hidden;margin-bottom:16px}
#progress-bar{height:100%;background:linear-gradient(90deg,var(--ma),#e84545);border-radius:3px;transition:width .5s cubic-bezier(.4,0,.2,1)}
#streak-row{height:28px;display:flex;align-items:center;justify-content:center;margin-bottom:8px}
#streak-badge{display:none;align-items:center;gap:5px;background:rgba(239,171,0,.12);border:1px solid rgba(239,171,0,.25);border-radius:20px;padding:3px 12px;font-size:12px;font-weight:700;color:#efab00;letter-spacing:.5px;text-transform:uppercase;animation:pop .3s cubic-bezier(.34,1.56,.64,1)}
@keyframes pop{from{transform:scale(.6);opacity:0}to{transform:scale(1);opacity:1}}

/* Photo card */
#photo-card{width:100%;aspect-ratio:3/4;max-height:52vh;border-radius:var(--radius);overflow:hidden;position:relative;background:var(--surface);border:1px solid var(--border)}
#photo-card img{width:100%;height:100%;object-fit:cover;display:block;transition:opacity .4s}
#photo-card::after{content:'';position:absolute;bottom:0;left:0;right:0;height:35%;background:linear-gradient(to top,rgba(14,14,14,.8),transparent);pointer-events:none}
#photo-overlay{position:absolute;inset:0;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:8px;opacity:0;transition:opacity .35s;border-radius:var(--radius);z-index:5}
#photo-overlay.correct{background:rgba(0,114,41,.82);opacity:1}
#photo-overlay.wrong{background:rgba(193,39,45,.82);opacity:1}
#overlay-icon{font-size:72px;line-height:1}
#overlay-main{font-size:22px;font-weight:800;color:#fff;letter-spacing:-.5px}
#overlay-sub{font-size:14px;color:rgba(255,255,255,.82);text-align:center;padding:0 20px}
#photo-tag{position:absolute;top:14px;right:14px;background:rgba(14,14,14,.7);backdrop-filter:blur(6px);border:1px solid var(--border);border-radius:20px;padding:4px 10px;font-size:11px;font-weight:700;color:var(--muted);letter-spacing:1px;display:none;z-index:6}
#photo-type-badge{position:absolute;top:14px;left:14px;background:rgba(14,14,14,.7);backdrop-filter:blur(6px);border:1px solid var(--border);border-radius:20px;padding:4px 10px;font-size:11px;font-weight:700;color:var(--muted);z-index:6}

/* Upload prompt on placeholder */
#upload-prompt{position:absolute;bottom:60px;left:50%;transform:translateX(-50%);background:rgba(14,14,14,.85);border:1px dashed rgba(255,255,255,.2);border-radius:12px;padding:8px 16px;font-size:12px;color:rgba(255,255,255,.5);white-space:nowrap;z-index:4;cursor:pointer;transition:all .2s}
#upload-prompt:hover{border-color:rgba(255,255,255,.4);color:rgba(255,255,255,.8)}

/* Clue */
#clue-box{width:100%;display:none;align-items:flex-start;gap:8px;background:rgba(255,255,255,.04);border:1px solid var(--border);border-radius:12px;padding:10px 14px;margin-top:10px;font-size:13px;color:var(--muted);line-height:1.5}

/* Buttons */
#btn-row{display:flex;gap:10px;width:100%;margin-top:12px}
.flag-btn{flex:1;background:var(--surface);border:1px solid var(--border);border-radius:16px;padding:14px 10px;display:flex;flex-direction:column;align-items:center;gap:6px;cursor:pointer;transition:border-color .15s,transform .1s,background .15s;-webkit-tap-highlight-color:transparent}
.flag-btn:hover{border-color:rgba(255,255,255,.18);background:var(--surface2)}
.flag-btn:active{transform:scale(.97)}
.flag-btn .flag-em{font-size:36px;line-height:1}
.flag-btn .flag-name{font-size:14px;font-weight:700;color:var(--text)}
.flag-btn .flag-ar{font-family:'Noto Sans Arabic',sans-serif;font-size:11px;color:var(--muted)}
.flag-btn.correct{border-color:var(--dz);background:rgba(0,114,41,.1)}
.flag-btn.wrong{border-color:var(--ma);background:rgba(193,39,45,.1)}
.flag-btn.reveal{border-color:var(--dz);background:rgba(0,114,41,.06)}
.flag-btn:disabled{pointer-events:none}

#action-row{display:flex;gap:10px;width:100%;margin-top:10px}
#hint-btn{flex:0 0 auto;padding:11px 16px;background:none;border:1px dashed rgba(255,255,255,.15);border-radius:12px;font-family:var(--font);font-size:13px;font-weight:600;color:var(--muted);cursor:pointer;white-space:nowrap;transition:color .15s,border-color .15s}
#hint-btn:hover:not(:disabled){color:var(--text);border-color:rgba(255,255,255,.3)}
#hint-btn:disabled{opacity:.35;cursor:default}
#next-btn{flex:1;padding:13px;background:var(--surface2);border:1px solid rgba(255,255,255,.12);border-radius:12px;font-family:var(--font);font-size:15px;font-weight:700;color:var(--text);cursor:pointer;display:none;transition:background .15s}
#next-btn:hover{background:rgba(255,255,255,.1)}

/* Result */
#result-screen{display:none;flex-direction:column;align-items:center;gap:20px;width:100%;text-align:center;padding-top:20px}
#result-big{font-size:80px;line-height:1;animation:pop .5s cubic-bezier(.34,1.56,.64,1)}
#result-title{font-size:26px;font-weight:800;letter-spacing:-1px}
#result-sub{font-size:15px;color:var(--muted);max-width:300px}
#result-stats{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;width:100%}
.stat{background:var(--surface);border:1px solid var(--border);border-radius:14px;padding:14px 8px;display:flex;flex-direction:column;align-items:center;gap:4px}
.stat-val{font-size:28px;font-weight:800}
.stat-lbl{font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:.8px}
#result-breakdown{width:100%;display:flex;flex-direction:column;gap:8px;max-height:280px;overflow-y:auto}
.breakdown-item{display:flex;align-items:center;gap:10px;background:var(--surface);border:1px solid var(--border);border-radius:12px;padding:10px 14px;font-size:13px}
.breakdown-flag{font-size:20px}
.breakdown-name{flex:1;text-align:left;color:var(--text);font-weight:600}
#replay-btn{width:100%;padding:15px;background:var(--ma);border:none;border-radius:14px;font-family:var(--font);font-size:16px;font-weight:800;color:#fff;cursor:pointer;transition:background .15s}
#replay-btn:hover{background:#a81e23}

/* Settings */
#settings-panel{position:fixed;inset:0;background:rgba(0,0,0,.7);z-index:100;display:none;align-items:flex-end;justify-content:center}
#settings-panel.open{display:flex}
#settings-sheet{width:100%;max-width:480px;background:#1c1c1c;border-radius:24px 24px 0 0;padding:24px 20px 40px;border-top:1px solid var(--border);display:flex;flex-direction:column;gap:4px}
#settings-sheet h2{font-size:20px;font-weight:800;margin-bottom:16px}
.setting-row{display:flex;justify-content:space-between;align-items:center;padding:14px 0;border-bottom:1px solid var(--border);font-size:15px;font-weight:600}
.setting-row:last-of-type{border-bottom:none}
.setting-sub{font-size:12px;color:var(--muted);font-weight:400}
.toggle{width:46px;height:26px;border-radius:13px;background:var(--surface2);border:1px solid rgba(255,255,255,.1);position:relative;cursor:pointer;transition:background .2s}
.toggle.on{background:var(--dz);border-color:var(--dz)}
.toggle::after{content:'';position:absolute;top:3px;left:3px;width:20px;height:20px;border-radius:50%;background:#fff;transition:left .2s;box-shadow:0 1px 3px rgba(0,0,0,.3)}
.toggle.on::after{left:23px}
#close-settings{margin-top:16px;width:100%;padding:13px;background:var(--surface2);border:1px solid var(--border);border-radius:12px;font-family:var(--font);font-size:15px;font-weight:700;color:var(--text);cursor:pointer}
.admin-link-btn{margin-top:8px;width:100%;padding:11px;background:none;border:1px dashed rgba(255,255,255,.15);border-radius:12px;font-family:var(--font);font-size:13px;color:var(--muted);cursor:pointer;transition:color .15s}
.admin-link-btn:hover{color:var(--text)}

/* Splash */
#splash{width:100%;display:flex;flex-direction:column;align-items:center;gap:24px;padding-top:40px;text-align:center}
#splash-logo{font-size:52px;font-weight:800;letter-spacing:-2px}
#splash-logo .ma{color:var(--ma)}#splash-logo .dz{color:var(--dz)}
#splash-flags{font-size:64px;line-height:1}
#splash-desc{font-size:16px;color:var(--muted);max-width:300px;line-height:1.6}
#splash-stats{display:flex;gap:10px;width:100%}
.splash-stat{flex:1;background:var(--surface);border:1px solid var(--border);border-radius:12px;padding:12px 8px;text-align:center}
.splash-stat-val{font-size:22px;font-weight:800}
.splash-stat-lbl{font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:.5px}
#splash-rules{width:100%;display:flex;flex-direction:column;gap:8px;text-align:left}
.rule-item{display:flex;align-items:flex-start;gap:10px;background:var(--surface);border:1px solid var(--border);border-radius:12px;padding:12px 14px;font-size:13px;color:var(--muted);line-height:1.5}
.rule-icon{font-size:20px;flex-shrink:0}
#start-btn{width:100%;padding:16px;background:var(--ma);border:none;border-radius:16px;font-family:var(--font);font-size:18px;font-weight:800;color:#fff;cursor:pointer;transition:background .15s,transform .1s}
#start-btn:hover{background:#a81e23}
#start-btn:active{transform:scale(.98)}

/* ADMIN */
#admin-panel{display:none;position:fixed;inset:0;background:var(--bg);z-index:500;flex-direction:column;overflow-y:auto}
#admin-panel.open{display:flex}
#admin-header{position:sticky;top:0;background:var(--bg);border-bottom:1px solid var(--border);padding:16px 20px;display:flex;align-items:center;justify-content:space-between;z-index:10}
#admin-header h1{font-size:20px;font-weight:800;letter-spacing:-.5px}
#admin-header h1 .ma{color:var(--ma)}
#admin-header h1 .dz{color:var(--dz)}
#admin-close{background:none;border:1px solid var(--border);border-radius:10px;padding:7px 14px;font-family:var(--font);font-size:13px;font-weight:700;color:var(--text);cursor:pointer}
#admin-body{padding:20px;max-width:600px;margin:0 auto;width:100%;display:flex;flex-direction:column;gap:16px}
#admin-tabs{display:flex;gap:8px;background:var(--surface);border:1px solid var(--border);border-radius:12px;padding:4px}
.admin-tab{flex:1;padding:9px;background:none;border:none;border-radius:9px;font-family:var(--font);font-size:13px;font-weight:700;color:var(--muted);cursor:pointer;transition:background .15s,color .15s}
.admin-tab.active{background:var(--surface2);color:var(--text)}
.admin-section{background:var(--surface);border:1px solid var(--border);border-radius:16px;padding:18px;display:flex;flex-direction:column;gap:14px}
.admin-section h3{font-size:16px;font-weight:800}
.field-group{display:flex;flex-direction:column;gap:6px}
.field-group label{font-size:12px;font-weight:700;color:var(--muted);text-transform:uppercase;letter-spacing:.8px}
.field-group input,.field-group textarea,.field-group select{background:var(--surface2);border:1px solid var(--border);border-radius:10px;padding:10px 12px;font-family:var(--font);font-size:14px;color:var(--text);outline:none;transition:border-color .15s;width:100%}
.field-group input:focus,.field-group textarea:focus,.field-group select:focus{border-color:rgba(255,255,255,.3)}
.field-group textarea{resize:vertical;min-height:70px}
.field-group select option{background:#1a1a1a}
.img-preview-box{width:120px;height:160px;border-radius:12px;background:var(--surface2);border:1px solid var(--border);overflow:hidden;flex-shrink:0}
.img-preview-box img{width:100%;height:100%;object-fit:cover}
.add-form-top{display:flex;gap:14px;align-items:flex-start}
.add-form-fields{flex:1;display:flex;flex-direction:column;gap:10px}
.btn-row{display:flex;gap:10px}
.btn-primary{flex:1;padding:12px;background:var(--dz);border:none;border-radius:12px;font-family:var(--font);font-size:14px;font-weight:800;color:#fff;cursor:pointer;transition:background .15s}
.btn-primary:hover{background:#005c20}
.btn-danger{padding:12px 16px;background:rgba(193,39,45,.15);border:1px solid rgba(193,39,45,.3);border-radius:12px;font-family:var(--font);font-size:14px;font-weight:700;color:var(--ma);cursor:pointer}
.btn-secondary{flex:1;padding:12px;background:var(--surface2);border:1px solid var(--border);border-radius:12px;font-family:var(--font);font-size:14px;font-weight:700;color:var(--text);cursor:pointer}
.upload-zone{border:2px dashed rgba(255,255,255,.15);border-radius:12px;padding:24px;text-align:center;cursor:pointer;transition:border-color .15s,background .15s;position:relative}
.upload-zone:hover{border-color:rgba(255,255,255,.3);background:rgba(255,255,255,.03)}
.upload-zone input{position:absolute;inset:0;opacity:0;cursor:pointer;width:100%;height:100%}
.upload-zone .upload-icon{font-size:32px;margin-bottom:8px}
.upload-zone p{font-size:13px;color:var(--muted);line-height:1.6}
.url-row{display:flex;gap:8px}
#admin-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:10px}
.admin-card{background:var(--surface);border:1px solid var(--border);border-radius:12px;overflow:hidden;position:relative}
.admin-card-img{width:100%;aspect-ratio:3/4;object-fit:cover;display:block;background:var(--surface2)}
.admin-card-info{padding:8px 10px}
.admin-card-name{font-size:12px;font-weight:700;color:var(--text);white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.admin-card-meta{font-size:11px;color:var(--muted);display:flex;align-items:center;gap:4px;margin-top:2px;flex-wrap:wrap}
.admin-card-del{position:absolute;top:8px;right:8px;width:28px;height:28px;background:rgba(193,39,45,.85);border:none;border-radius:50%;font-size:14px;cursor:pointer;display:flex;align-items:center;justify-content:center;transition:transform .15s}
.admin-card-del:hover{transform:scale(1.1)}
.has-photo .admin-card-img{border-bottom:2px solid var(--dz)}
.no-photo .admin-card-img{border-bottom:2px dashed rgba(255,255,255,.1)}
#admin-search{background:var(--surface2);border:1px solid var(--border);border-radius:12px;padding:10px 14px;font-family:var(--font);font-size:14px;color:var(--text);outline:none;width:100%}
.filter-row{display:flex;gap:8px;flex-wrap:wrap}
.filter-btn{padding:6px 14px;background:var(--surface);border:1px solid var(--border);border-radius:20px;font-family:var(--font);font-size:12px;font-weight:700;color:var(--muted);cursor:pointer;transition:all .15s;white-space:nowrap}
.filter-btn.active{color:var(--text);border-color:rgba(255,255,255,.3);background:var(--surface2)}
#admin-count{font-size:13px;color:var(--muted)}
.stats-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:10px}
.stats-card{background:var(--surface2);border:1px solid var(--border);border-radius:12px;padding:14px;display:flex;flex-direction:column;gap:4px}
.stats-card-val{font-size:28px;font-weight:800}
.stats-card-lbl{font-size:12px;color:var(--muted)}

/* Login */
#admin-login{display:flex;flex-direction:column;align-items:center;gap:20px;padding:60px 20px;text-align:center;width:100%}
#admin-login h2{font-size:24px;font-weight:800;letter-spacing:-1px}
#admin-login p{font-size:14px;color:var(--muted)}
#pw-input{background:var(--surface2);border:1px solid var(--border);border-radius:12px;padding:12px 16px;font-family:var(--font);font-size:16px;color:var(--text);outline:none;width:100%;max-width:280px;text-align:center;letter-spacing:4px}
#pw-input:focus{border-color:rgba(255,255,255,.3)}
#pw-btn{width:100%;max-width:280px;padding:14px;background:var(--ma);border:none;border-radius:12px;font-family:var(--font);font-size:15px;font-weight:800;color:#fff;cursor:pointer}
#pw-error{font-size:13px;color:var(--ma);display:none}

/* Info banner */
.info-banner{background:rgba(193,39,45,.08);border:1px solid rgba(193,39,45,.2);border-radius:12px;padding:12px 14px;font-size:13px;color:rgba(240,236,228,.7);line-height:1.6}
.info-banner strong{color:var(--text)}

/* Toast */
#toast{position:fixed;bottom:30px;left:50%;transform:translateX(-50%) translateY(100px);background:#1c1c1c;border:1px solid var(--border);border-radius:12px;padding:12px 20px;font-size:14px;font-weight:600;color:var(--text);z-index:1000;transition:transform .3s cubic-bezier(.34,1.56,.64,1);white-space:nowrap;pointer-events:none}
#toast.show{transform:translateX(-50%) translateY(0)}
#toast.success{border-color:rgba(0,114,41,.4);color:#4ade80}
#toast.error{border-color:rgba(193,39,45,.4);color:#f87171}

/* Animations */
@keyframes slideUp{from{transform:translateY(30px);opacity:0}to{transform:translateY(0);opacity:1}}
.slide-up{animation:slideUp .4s cubic-bezier(.4,0,.2,1) both}
@keyframes flashGreen{0%,100%{box-shadow:none}50%{box-shadow:0 0 0 3px var(--dz)}}
.flash-correct{animation:flashGreen .4s ease}
@keyframes shake{0%,100%{transform:translateX(0)}25%{transform:translateX(-6px)}75%{transform:translateX(6px)}}
.shake{animation:shake .35s ease}
</style>
</head>
<body>

<div id="toast"></div>

<div id="app">
  <div id="header">
    <div id="logo"><span class="ma">Maro</span><span class="dz">gien</span></div>
    <div id="hud">
      <div class="hud-pill">Score : <span id="score-val">0</span></div>
      <div class="hud-pill" id="round-pill">1<span style="color:rgba(240,236,228,0.3)">/10</span></div>
      <button id="settings-btn">⚙️</button>
    </div>
  </div>
  <div id="progress-wrap"><div id="progress-bar" style="width:0%"></div></div>
  <div id="streak-row"><div id="streak-badge">🔥 <span id="streak-val">2</span> en série !</div></div>

  <!-- SPLASH -->
  <div id="splash" class="slide-up">
    <div id="splash-flags">🇲🇦 🇩🇿</div>
    <div id="splash-logo"><span class="ma">Maro</span><span class="dz">gien</span></div>
    <div id="splash-desc">Saurais-tu distinguer un Marocain d'un Algérien ? Teste tes connaissances !</div>
    <div id="splash-stats">
      <div class="splash-stat"><div class="splash-stat-val" id="splash-total">50</div><div class="splash-stat-lbl">Photos</div></div>
      <div class="splash-stat"><div class="splash-stat-val" id="splash-ma">25</div><div class="splash-stat-lbl">🇲🇦 Maroc</div></div>
      <div class="splash-stat"><div class="splash-stat-val" id="splash-dz">25</div><div class="splash-stat-lbl">🇩🇿 Algérie</div></div>
    </div>
    <div id="splash-rules">
      <div class="rule-item"><span class="rule-icon">📸</span>Une image apparaît — devine la nationalité</div>
      <div class="rule-item"><span class="rule-icon">💡</span>Un indice disponible (−5 pts)</div>
      <div class="rule-item"><span class="rule-icon">🔥</span>Enchaîne les bonnes réponses pour du bonus</div>
      <div class="rule-item"><span class="rule-icon">⚙️</span>Ajoute tes propres photos via le panel Admin</div>
    </div>
    <button id="start-btn">Commencer le jeu →</button>
  </div>

  <!-- GAME -->
  <div id="game-area" style="display:none;width:100%;flex-direction:column;align-items:center;gap:10px;">
    <div id="photo-card">
      <img id="person-photo" src="" alt="Devinez"/>
      <div id="photo-overlay">
        <div id="overlay-icon"></div>
        <div id="overlay-main"></div>
        <div id="overlay-sub"></div>
      </div>
      <div id="photo-tag"></div>
      <div id="photo-type-badge"></div>
    </div>
    <div id="clue-box"><span>💡</span><span id="clue-text"></span></div>
    <div id="btn-row">
      <button class="flag-btn" id="btn-ma">
        <span class="flag-em">🇲🇦</span>
        <span class="flag-name">Marocain·e</span>
        <span class="flag-ar">المغربي</span>
      </button>
      <button class="flag-btn" id="btn-dz">
        <span class="flag-em">🇩🇿</span>
        <span class="flag-name">Algérien·ne</span>
        <span class="flag-ar">الجزائري</span>
      </button>
    </div>
    <div id="action-row">
      <button id="hint-btn">💡 Indice (−5 pts)</button>
      <button id="next-btn">Suivant →</button>
    </div>
  </div>

  <!-- RESULTS -->
  <div id="result-screen">
    <div id="result-big"></div>
    <div id="result-title"></div>
    <div id="result-sub"></div>
    <div id="result-stats">
      <div class="stat"><div class="stat-val" id="r-score">0</div><div class="stat-lbl">Score</div></div>
      <div class="stat"><div class="stat-val" id="r-pct">0%</div><div class="stat-lbl">Réussite</div></div>
      <div class="stat"><div class="stat-val" id="r-streak">0</div><div class="stat-lbl">Série max</div></div>
    </div>
    <div id="result-breakdown"></div>
    <button id="replay-btn">🔁 Rejouer</button>
  </div>
</div>

<!-- SETTINGS -->
<div id="settings-panel">
  <div id="settings-sheet">
    <h2>⚙️ Paramètres</h2>
    <div class="setting-row"><div>Sons<div class="setting-sub">Effets sonores</div></div><div class="toggle on" id="toggle-sound"></div></div>
    <div class="setting-row"><div>Vibration<div class="setting-sub">Retour haptique</div></div><div class="toggle on" id="toggle-vibrate"></div></div>
    <div class="setting-row"><div>Mode difficile<div class="setting-sub">Indices désactivés</div></div><div class="toggle" id="toggle-hard"></div></div>
    <button id="close-settings">Fermer</button>
    <button class="admin-link-btn" id="open-admin-btn">🔐 Panel Admin — Gérer les photos</button>
  </div>
</div>

<!-- ADMIN -->
<div id="admin-panel">
  <div id="admin-login">
    <div style="font-size:48px">🔐</div>
    <h2><span style="color:#c1272d">Admin</span> Marogien</h2>
    <p>Entrez le mot de passe pour gérer les photos</p>
    <input type="password" id="pw-input" placeholder="••••••••"/>
    <div id="pw-error">❌ Mot de passe incorrect</div>
    <button id="pw-btn">Accéder →</button>
    <div style="font-size:11px;color:rgba(240,236,228,0.2);margin-top:8px">Mot de passe par défaut : <code style="letter-spacing:2px">marogien2024</code></div>
  </div>
  <div id="admin-content" style="display:none;flex-direction:column;width:100%">
    <div id="admin-header">
      <h1><span class="ma">Admin</span> <span class="dz">Marogien</span></h1>
      <button id="admin-close">✕ Fermer</button>
    </div>
    <div id="admin-body">
      <div id="admin-tabs">
        <button class="admin-tab active" data-tab="add">➕ Ajouter</button>
        <button class="admin-tab" data-tab="manage">🗂️ Gérer (<span id="tab-count">50</span>)</button>
        <button class="admin-tab" data-tab="stats">📊 Stats</button>
      </div>

      <!-- ADD TAB -->
      <div id="tab-add" class="admin-section">
        <h3>➕ Ajouter une photo</h3>
        <div class="info-banner">
          📌 <strong>Comment ajouter une vraie photo ?</strong><br/>
          Colle l'URL d'une image depuis <strong>Imgur</strong>, <strong>Cloudinary</strong>, ou ton repo GitHub.<br/>
          Ou utilise le bouton Upload pour importer depuis ton téléphone/PC.
        </div>

        <div class="add-form-top">
          <div class="img-preview-box">
            <img id="img-preview" src="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 120 160'><rect width='120' height='160' fill='%23242424'/><text x='60' y='88' text-anchor='middle' font-size='32'>🖼️</text></svg>" alt="Aperçu"/>
          </div>
          <div class="add-form-fields">
            <div class="field-group">
              <label>Nationalité</label>
              <select id="img-country">
                <option value="ma">🇲🇦 Marocain·e</option>
                <option value="dz">🇩🇿 Algérien·ne</option>
              </select>
            </div>
            <div class="field-group">
              <label>Catégorie</label>
              <select id="img-cat">
                <option value="portrait">📸 Portrait</option>
                <option value="comic">😂 Comique</option>
                <option value="caricature">🎨 Caricature</option>
                <option value="sport">⚽ Sport</option>
              </select>
            </div>
          </div>
        </div>

        <!-- Upload zone -->
        <div class="upload-zone" id="upload-zone">
          <input type="file" id="img-file" accept="image/*"/>
          <div class="upload-icon">📁</div>
          <p><strong>Clique ou glisse une image ici</strong><br/>JPG, PNG, WebP — max 3MB</p>
        </div>

        <div class="field-group">
          <label>Ou colle une URL directe</label>
          <div class="url-row">
            <input type="url" id="img-url" placeholder="https://i.imgur.com/xxxxx.jpg"/>
            <button class="btn-secondary" id="preview-url-btn" style="flex:0 0 auto;padding:10px 14px">👁️</button>
          </div>
        </div>

        <div class="field-group">
          <label>Label</label>
          <input type="text" id="img-label" placeholder="Ex: Femme de Casablanca"/>
        </div>
        <div class="field-group">
          <label>Indice culturel</label>
          <textarea id="img-clue" placeholder="Ex: Le style rappelle les femmes de Casablanca..."></textarea>
        </div>

        <div class="btn-row">
          <button class="btn-primary" id="add-btn">✅ Ajouter au jeu</button>
          <button class="btn-secondary" id="clear-form-btn" style="flex:0 0 auto;padding:12px 14px">🗑️</button>
        </div>
      </div>

      <!-- MANAGE TAB -->
      <div id="tab-manage" style="display:none;flex-direction:column;gap:12px">
        <div class="admin-section" style="padding:14px">
          <input type="text" id="admin-search" placeholder="🔍 Rechercher..."/>
          <div class="filter-row" style="margin-top:10px">
            <button class="filter-btn active" data-filter="all">Tous</button>
            <button class="filter-btn" data-filter="ma">🇲🇦</button>
            <button class="filter-btn" data-filter="dz">🇩🇿</button>
            <button class="filter-btn" data-filter="real">📸 Vraies photos</button>
            <button class="filter-btn" data-filter="placeholder">🎨 Silhouettes</button>
          </div>
          <div id="admin-count" style="margin-top:10px">50 images</div>
        </div>
        <div id="admin-grid"></div>
      </div>

      <!-- STATS TAB -->
      <div id="tab-stats" style="display:none;flex-direction:column;gap:12px">
        <div class="admin-section">
          <h3>📊 Statistiques</h3>
          <div class="stats-grid" id="stats-grid"></div>
        </div>
        <div class="admin-section">
          <h3>💾 Sauvegarde</h3>
          <p style="font-size:13px;color:var(--muted);line-height:1.5">Exporte ta base d'images (JSON) pour la sauvegarder ou la partager.</p>
          <div class="btn-row">
            <button class="btn-primary" id="export-btn">📤 Exporter JSON</button>
            <button class="btn-secondary" id="import-trigger">📥 Importer JSON</button>
          </div>
          <input type="file" id="import-file" accept=".json" style="display:none"/>
        </div>
        <div class="admin-section">
          <h3>⚠️ Zone de danger</h3>
          <div class="btn-row">
            <button class="btn-danger" id="reset-default-btn">🔄 Réinitialiser</button>
            <button class="btn-danger" id="clear-all-btn">🗑️ Tout vider</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<script>
const ADMIN_PASSWORD = 'marogien2024';
const STORAGE_KEY = 'marogien_v3';
const ROUNDS = 10;
const CAT_ICONS = {portrait:'📸',comic:'😂',caricature:'🎨',sport:'⚽'};
const CAT_LABELS = {portrait:'Portrait',comic:'Comique',caricature:'Caricature',sport:'Sport'};

const DEFAULT_IMAGES = [{"id": "ma01", "country": "ma", "cat": "portrait", "label": "Femme de Casablanca", "clue": "Le style rappelle les femmes des grandes villes marocaines.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcwIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cwIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2MxMjcyZCIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMCkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MCkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ1IiByeD0iNTgiIHJ5PSI2NSIgZmlsbD0iIzNhMmEzYSIvPgogICAgICAgIDxwYXRoIGQ9Ik0xNDIgMTQ1IFExNDIgMTEwIDIwMCAxMDUgUTI1OCAxMTAgMjU4IDE0NSBRMjcwIDEzMCAyNzAgMTgwIFEyNzAgMjEwIDIwMCAyMTUgUTEzMCAyMTAgMTMwIDE4MCBRMTMwIDE1MCAxNDIgMTQ1WiIgZmlsbD0iI2MxMjcyZCIgb3BhY2l0eT0iMC43Ii8+CiAgICAgICAgPHBhdGggZD0iTTYwIDUzMyBRNzAgMzEwIDIwMCAyOTUgUTMzMCAzMTAgMzQwIDUzM1oiIGZpbGw9IiMzYTJhM2EiLz4KICA8dGV4dCB4PSIyMDAiIHk9IjQ0NSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSI1MiIgZm9udC1mYW1pbHk9InNlcmlmIj7wn5GpPC90ZXh0PgogIDxyZWN0IHg9IjAiIHk9IjQ3MCIgd2lkdGg9IjQwMCIgaGVpZ2h0PSI2MyIgZmlsbD0icmdiYSgwLDAsMCwwLjUpIi8+CiAgPHRleHQgeD0iMjAwIiB5PSI0OTUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9InJnYmEoMjU1LDI1NSwyNTUsMC41KSIgZm9udC1zaXplPSIxMyIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkZlbW1lIGRlIENhc2FibGFuY2E8L3RleHQ+CiAgPHRleHQgeD0iMjAwIiB5PSI1MTgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9IiNjMTI3MmQiIGZvbnQtc2l6ZT0iMTYiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+QWpvdXRlIHVuZSBwaG90byDihpI8L3RleHQ+Cjwvc3ZnPg=="}, {"id": "ma02", "country": "ma", "cat": "portrait", "label": "Femme berbère", "clue": "Les traits évoquent la beauté berbère du Souss.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcxIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cxIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2MxMjcyZCIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMSkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MSkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTUwIiByeD0iNjAiIHJ5PSI3MCIgZmlsbD0iIzJhM2EyYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01NSA1MzMgUTY1IDMwMCAyMDAgMjg1IFEzMzUgMzAwIDM0NSA1MzNaIiBmaWxsPSIjMmEzYTJhIi8+CiAgICAgICAgPHJlY3QgeD0iMTcwIiB5PSIyMTUiIHdpZHRoPSI2MCIgaGVpZ2h0PSIxNSIgcng9IjciIGZpbGw9IiNjMTI3MmQiIG9wYWNpdHk9IjAuNSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDQ1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjUyIiBmb250LWZhbWlseT0ic2VyaWYiPvCfp5U8L3RleHQ+CiAgPHJlY3QgeD0iMCIgeT0iNDcwIiB3aWR0aD0iNDAwIiBoZWlnaHQ9IjYzIiBmaWxsPSJyZ2JhKDAsMCwwLDAuNSkiLz4KICA8dGV4dCB4PSIyMDAiIHk9IjQ5NSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZmlsbD0icmdiYSgyNTUsMjU1LDI1NSwwLjUpIiBmb250LXNpemU9IjEzIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+RmVtbWUgYmVyYsOocmU8L3RleHQ+CiAgPHRleHQgeD0iMjAwIiB5PSI1MTgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9IiNjMTI3MmQiIGZvbnQtc2l6ZT0iMTYiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+QWpvdXRlIHVuZSBwaG90byDihpI8L3RleHQ+Cjwvc3ZnPg=="}, {"id": "ma03", "country": "ma", "cat": "portrait", "label": "Homme de Fès", "clue": "La coiffure rappelle les jeunes hommes de Fès ou Meknès.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcyIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cyIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2MxMjcyZCIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMikiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MikiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ4IiByeD0iNTUiIHJ5PSI2OCIgZmlsbD0iIzJhMmEzYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01MCA1MzMgUTYwIDI5NSAyMDAgMjgwIFEzNDAgMjk1IDM1MCA1MzNaIiBmaWxsPSIjMmEyYTNhIi8+CiAgICAgICAgPHBhdGggZD0iTTE1NSAxNDAgUTE3MCAxMTAgMjAwIDEwNSBRMjMwIDExMCAyNDUgMTQwIiBmaWxsPSJub25lIiBzdHJva2U9IiNjMTI3MmQiIHN0cm9rZS13aWR0aD0iOCIgb3BhY2l0eT0iMC42Ii8+CiAgPHRleHQgeD0iMjAwIiB5PSI0NDUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iNTIiIGZvbnQtZmFtaWx5PSJzZXJpZiI+8J+nlDwvdGV4dD4KICA8cmVjdCB4PSIwIiB5PSI0NzAiIHdpZHRoPSI0MDAiIGhlaWdodD0iNjMiIGZpbGw9InJnYmEoMCwwLDAsMC41KSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDk1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJyZ2JhKDI1NSwyNTUsMjU1LDAuNSkiIGZvbnQtc2l6ZT0iMTMiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5Ib21tZSBkZSBGw6hzPC90ZXh0PgogIDx0ZXh0IHg9IjIwMCIgeT0iNTE4IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSIjYzEyNzJkIiBmb250LXNpemU9IjE2IiBmb250LXdlaWdodD0iYm9sZCIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkFqb3V0ZSB1bmUgcGhvdG8g4oaSPC90ZXh0Pgo8L3N2Zz4="}, {"id": "ma04", "country": "ma", "cat": "portrait", "label": "Femme de Marrakech", "clue": "Portrait typique des photographes de Marrakech.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmczIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3czIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2MxMjcyZCIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMykiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MykiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTUyIiByeD0iNjIiIHJ5PSI3MiIgZmlsbD0iIzNhMmEyYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01OCA1MzMgUTY4IDMwNSAyMDAgMjkwIFEzMzIgMzA1IDM0MiA1MzNaIiBmaWxsPSIjM2EyYTJhIi8+CiAgICAgICAgPGNpcmNsZSBjeD0iMjAwIiBjeT0iODAiIHI9IjM1IiBmaWxsPSJub25lIiBzdHJva2U9IiNjMTI3MmQiIHN0cm9rZS13aWR0aD0iNCIgb3BhY2l0eT0iMC40Ii8+CiAgPHRleHQgeD0iMjAwIiB5PSI0NDUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iNTIiIGZvbnQtZmFtaWx5PSJzZXJpZiI+8J+RqTwvdGV4dD4KICA8cmVjdCB4PSIwIiB5PSI0NzAiIHdpZHRoPSI0MDAiIGhlaWdodD0iNjMiIGZpbGw9InJnYmEoMCwwLDAsMC41KSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDk1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJyZ2JhKDI1NSwyNTUsMjU1LDAuNSkiIGZvbnQtc2l6ZT0iMTMiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5GZW1tZSBkZSBNYXJyYWtlY2g8L3RleHQ+CiAgPHRleHQgeD0iMjAwIiB5PSI1MTgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9IiNjMTI3MmQiIGZvbnQtc2l6ZT0iMTYiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+QWpvdXRlIHVuZSBwaG90byDihpI8L3RleHQ+Cjwvc3ZnPg=="}, {"id": "ma05", "country": "ma", "cat": "portrait", "label": "Homme du Nord", "clue": "Le port de tête rappelle les hommes du Maroc du Nord.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcwIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cwIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2MxMjcyZCIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMCkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MCkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ1IiByeD0iNTgiIHJ5PSI2NSIgZmlsbD0iIzJhM2EzYSIvPgogICAgICAgIDxwYXRoIGQ9Ik0xNDIgMTQ1IFExNDIgMTEwIDIwMCAxMDUgUTI1OCAxMTAgMjU4IDE0NSBRMjcwIDEzMCAyNzAgMTgwIFEyNzAgMjEwIDIwMCAyMTUgUTEzMCAyMTAgMTMwIDE4MCBRMTMwIDE1MCAxNDIgMTQ1WiIgZmlsbD0iI2MxMjcyZCIgb3BhY2l0eT0iMC43Ii8+CiAgICAgICAgPHBhdGggZD0iTTYwIDUzMyBRNzAgMzEwIDIwMCAyOTUgUTMzMCAzMTAgMzQwIDUzM1oiIGZpbGw9IiMyYTNhM2EiLz4KICA8dGV4dCB4PSIyMDAiIHk9IjQ0NSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSI1MiIgZm9udC1mYW1pbHk9InNlcmlmIj7wn5GoPC90ZXh0PgogIDxyZWN0IHg9IjAiIHk9IjQ3MCIgd2lkdGg9IjQwMCIgaGVpZ2h0PSI2MyIgZmlsbD0icmdiYSgwLDAsMCwwLjUpIi8+CiAgPHRleHQgeD0iMjAwIiB5PSI0OTUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9InJnYmEoMjU1LDI1NSwyNTUsMC41KSIgZm9udC1zaXplPSIxMyIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkhvbW1lIGR1IE5vcmQ8L3RleHQ+CiAgPHRleHQgeD0iMjAwIiB5PSI1MTgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9IiNjMTI3MmQiIGZvbnQtc2l6ZT0iMTYiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+QWpvdXRlIHVuZSBwaG90byDihpI8L3RleHQ+Cjwvc3ZnPg=="}, {"id": "ma06", "country": "ma", "cat": "portrait", "label": "Jeune marocain", "clue": "Traits méditerranéens typiques de Tanger ou Tétouan.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcxIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cxIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2MxMjcyZCIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMSkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MSkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTUwIiByeD0iNjAiIHJ5PSI3MCIgZmlsbD0iIzNhM2EyYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01NSA1MzMgUTY1IDMwMCAyMDAgMjg1IFEzMzUgMzAwIDM0NSA1MzNaIiBmaWxsPSIjM2EzYTJhIi8+CiAgICAgICAgPHJlY3QgeD0iMTcwIiB5PSIyMTUiIHdpZHRoPSI2MCIgaGVpZ2h0PSIxNSIgcng9IjciIGZpbGw9IiNjMTI3MmQiIG9wYWNpdHk9IjAuNSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDQ1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjUyIiBmb250LWZhbWlseT0ic2VyaWYiPvCfp5E8L3RleHQ+CiAgPHJlY3QgeD0iMCIgeT0iNDcwIiB3aWR0aD0iNDAwIiBoZWlnaHQ9IjYzIiBmaWxsPSJyZ2JhKDAsMCwwLDAuNSkiLz4KICA8dGV4dCB4PSIyMDAiIHk9IjQ5NSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZmlsbD0icmdiYSgyNTUsMjU1LDI1NSwwLjUpIiBmb250LXNpemU9IjEzIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+SmV1bmUgbWFyb2NhaW48L3RleHQ+CiAgPHRleHQgeD0iMjAwIiB5PSI1MTgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9IiNjMTI3MmQiIGZvbnQtc2l6ZT0iMTYiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+QWpvdXRlIHVuZSBwaG90byDihpI8L3RleHQ+Cjwvc3ZnPg=="}, {"id": "ma07", "country": "ma", "cat": "portrait", "label": "Femme élégante", "clue": "L'élégance naturelle rappelle les femmes de Casablanca.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcyIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cyIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2MxMjcyZCIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMikiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MikiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ4IiByeD0iNTUiIHJ5PSI2OCIgZmlsbD0iIzNhMmEzYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01MCA1MzMgUTYwIDI5NSAyMDAgMjgwIFEzNDAgMjk1IDM1MCA1MzNaIiBmaWxsPSIjM2EyYTNhIi8+CiAgICAgICAgPHBhdGggZD0iTTE1NSAxNDAgUTE3MCAxMTAgMjAwIDEwNSBRMjMwIDExMCAyNDUgMTQwIiBmaWxsPSJub25lIiBzdHJva2U9IiNjMTI3MmQiIHN0cm9rZS13aWR0aD0iOCIgb3BhY2l0eT0iMC42Ii8+CiAgPHRleHQgeD0iMjAwIiB5PSI0NDUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iNTIiIGZvbnQtZmFtaWx5PSJzZXJpZiI+8J+RqTwvdGV4dD4KICA8cmVjdCB4PSIwIiB5PSI0NzAiIHdpZHRoPSI0MDAiIGhlaWdodD0iNjMiIGZpbGw9InJnYmEoMCwwLDAsMC41KSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDk1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJyZ2JhKDI1NSwyNTUsMjU1LDAuNSkiIGZvbnQtc2l6ZT0iMTMiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5GZW1tZSDDqWzDqWdhbnRlPC90ZXh0PgogIDx0ZXh0IHg9IjIwMCIgeT0iNTE4IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSIjYzEyNzJkIiBmb250LXNpemU9IjE2IiBmb250LXdlaWdodD0iYm9sZCIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkFqb3V0ZSB1bmUgcGhvdG8g4oaSPC90ZXh0Pgo8L3N2Zz4="}, {"id": "ma08", "country": "ma", "cat": "portrait", "label": "Homme urbain", "clue": "Style sobre très répandu chez les jeunes marocains urbains.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmczIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3czIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2MxMjcyZCIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMykiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MykiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTUyIiByeD0iNjIiIHJ5PSI3MiIgZmlsbD0iIzJhMmEzYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01OCA1MzMgUTY4IDMwNSAyMDAgMjkwIFEzMzIgMzA1IDM0MiA1MzNaIiBmaWxsPSIjMmEyYTNhIi8+CiAgICAgICAgPGNpcmNsZSBjeD0iMjAwIiBjeT0iODAiIHI9IjM1IiBmaWxsPSJub25lIiBzdHJva2U9IiNjMTI3MmQiIHN0cm9rZS13aWR0aD0iNCIgb3BhY2l0eT0iMC40Ii8+CiAgPHRleHQgeD0iMjAwIiB5PSI0NDUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iNTIiIGZvbnQtZmFtaWx5PSJzZXJpZiI+8J+RqDwvdGV4dD4KICA8cmVjdCB4PSIwIiB5PSI0NzAiIHdpZHRoPSI0MDAiIGhlaWdodD0iNjMiIGZpbGw9InJnYmEoMCwwLDAsMC41KSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDk1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJyZ2JhKDI1NSwyNTUsMjU1LDAuNSkiIGZvbnQtc2l6ZT0iMTMiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5Ib21tZSB1cmJhaW48L3RleHQ+CiAgPHRleHQgeD0iMjAwIiB5PSI1MTgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9IiNjMTI3MmQiIGZvbnQtc2l6ZT0iMTYiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+QWpvdXRlIHVuZSBwaG90byDihpI8L3RleHQ+Cjwvc3ZnPg=="}, {"id": "ma09", "country": "ma", "cat": "portrait", "label": "Femme souriante", "clue": "La chaleur du sourire rappelle Marrakech.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcwIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cwIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2MxMjcyZCIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMCkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MCkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ1IiByeD0iNTgiIHJ5PSI2NSIgZmlsbD0iIzNhM2EyYSIvPgogICAgICAgIDxwYXRoIGQ9Ik0xNDIgMTQ1IFExNDIgMTEwIDIwMCAxMDUgUTI1OCAxMTAgMjU4IDE0NSBRMjcwIDEzMCAyNzAgMTgwIFEyNzAgMjEwIDIwMCAyMTUgUTEzMCAyMTAgMTMwIDE4MCBRMTMwIDE1MCAxNDIgMTQ1WiIgZmlsbD0iI2MxMjcyZCIgb3BhY2l0eT0iMC43Ii8+CiAgICAgICAgPHBhdGggZD0iTTYwIDUzMyBRNzAgMzEwIDIwMCAyOTUgUTMzMCAzMTAgMzQwIDUzM1oiIGZpbGw9IiMzYTNhMmEiLz4KICA8dGV4dCB4PSIyMDAiIHk9IjQ0NSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSI1MiIgZm9udC1mYW1pbHk9InNlcmlmIj7wn5mCPC90ZXh0PgogIDxyZWN0IHg9IjAiIHk9IjQ3MCIgd2lkdGg9IjQwMCIgaGVpZ2h0PSI2MyIgZmlsbD0icmdiYSgwLDAsMCwwLjUpIi8+CiAgPHRleHQgeD0iMjAwIiB5PSI0OTUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9InJnYmEoMjU1LDI1NSwyNTUsMC41KSIgZm9udC1zaXplPSIxMyIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkZlbW1lIHNvdXJpYW50ZTwvdGV4dD4KICA8dGV4dCB4PSIyMDAiIHk9IjUxOCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZmlsbD0iI2MxMjcyZCIgZm9udC1zaXplPSIxNiIgZm9udC13ZWlnaHQ9ImJvbGQiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5Bam91dGUgdW5lIHBob3RvIOKGkjwvdGV4dD4KPC9zdmc+"}, {"id": "ma10", "country": "ma", "cat": "comic", "label": "Thé à la menthe", "clue": "Le thé à la menthe versé de haut — rituel 100% marocain 🍵", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcxIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cxIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2MxMjcyZCIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMSkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MSkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTUwIiByeD0iNjAiIHJ5PSI3MCIgZmlsbD0iIzFhMWEwYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01NSA1MzMgUTY1IDMwMCAyMDAgMjg1IFEzMzUgMzAwIDM0NSA1MzNaIiBmaWxsPSIjMWExYTBhIi8+CiAgICAgICAgPHJlY3QgeD0iMTcwIiB5PSIyMTUiIHdpZHRoPSI2MCIgaGVpZ2h0PSIxNSIgcng9IjciIGZpbGw9IiNjMTI3MmQiIG9wYWNpdHk9IjAuNSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDQ1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjUyIiBmb250LWZhbWlseT0ic2VyaWYiPvCfjbU8L3RleHQ+CiAgPHJlY3QgeD0iMCIgeT0iNDcwIiB3aWR0aD0iNDAwIiBoZWlnaHQ9IjYzIiBmaWxsPSJyZ2JhKDAsMCwwLDAuNSkiLz4KICA8dGV4dCB4PSIyMDAiIHk9IjQ5NSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZmlsbD0icmdiYSgyNTUsMjU1LDI1NSwwLjUpIiBmb250LXNpemU9IjEzIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+VGjDqSDDoCBsYSBtZW50aGU8L3RleHQ+CiAgPHRleHQgeD0iMjAwIiB5PSI1MTgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9IiNjMTI3MmQiIGZvbnQtc2l6ZT0iMTYiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+QWpvdXRlIHVuZSBwaG90byDihpI8L3RleHQ+Cjwvc3ZnPg=="}, {"id": "ma11", "country": "ma", "cat": "comic", "label": "Tajine", "clue": "Le tajine est le plat emblématique du Maroc 🍲", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcyIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cyIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2MxMjcyZCIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMikiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MikiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ4IiByeD0iNTUiIHJ5PSI2OCIgZmlsbD0iIzFhMGEwYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01MCA1MzMgUTYwIDI5NSAyMDAgMjgwIFEzNDAgMjk1IDM1MCA1MzNaIiBmaWxsPSIjMWEwYTBhIi8+CiAgICAgICAgPHBhdGggZD0iTTE1NSAxNDAgUTE3MCAxMTAgMjAwIDEwNSBRMjMwIDExMCAyNDUgMTQwIiBmaWxsPSJub25lIiBzdHJva2U9IiNjMTI3MmQiIHN0cm9rZS13aWR0aD0iOCIgb3BhY2l0eT0iMC42Ii8+CiAgPHRleHQgeD0iMjAwIiB5PSI0NDUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iNTIiIGZvbnQtZmFtaWx5PSJzZXJpZiI+8J+NsjwvdGV4dD4KICA8cmVjdCB4PSIwIiB5PSI0NzAiIHdpZHRoPSI0MDAiIGhlaWdodD0iNjMiIGZpbGw9InJnYmEoMCwwLDAsMC41KSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDk1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJyZ2JhKDI1NSwyNTUsMjU1LDAuNSkiIGZvbnQtc2l6ZT0iMTMiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5UYWppbmU8L3RleHQ+CiAgPHRleHQgeD0iMjAwIiB5PSI1MTgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9IiNjMTI3MmQiIGZvbnQtc2l6ZT0iMTYiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+QWpvdXRlIHVuZSBwaG90byDihpI8L3RleHQ+Cjwvc3ZnPg=="}, {"id": "ma12", "country": "ma", "cat": "comic", "label": "Souk", "clue": "Les souks sont LE symbole du commerce marocain 🛍️", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmczIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3czIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2MxMjcyZCIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMykiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MykiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTUyIiByeD0iNjIiIHJ5PSI3MiIgZmlsbD0iIzJhMWEwYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01OCA1MzMgUTY4IDMwNSAyMDAgMjkwIFEzMzIgMzA1IDM0MiA1MzNaIiBmaWxsPSIjMmExYTBhIi8+CiAgICAgICAgPGNpcmNsZSBjeD0iMjAwIiBjeT0iODAiIHI9IjM1IiBmaWxsPSJub25lIiBzdHJva2U9IiNjMTI3MmQiIHN0cm9rZS13aWR0aD0iNCIgb3BhY2l0eT0iMC40Ii8+CiAgPHRleHQgeD0iMjAwIiB5PSI0NDUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iNTIiIGZvbnQtZmFtaWx5PSJzZXJpZiI+8J+bje+4jzwvdGV4dD4KICA8cmVjdCB4PSIwIiB5PSI0NzAiIHdpZHRoPSI0MDAiIGhlaWdodD0iNjMiIGZpbGw9InJnYmEoMCwwLDAsMC41KSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDk1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJyZ2JhKDI1NSwyNTUsMjU1LDAuNSkiIGZvbnQtc2l6ZT0iMTMiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5Tb3VrPC90ZXh0PgogIDx0ZXh0IHg9IjIwMCIgeT0iNTE4IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSIjYzEyNzJkIiBmb250LXNpemU9IjE2IiBmb250LXdlaWdodD0iYm9sZCIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkFqb3V0ZSB1bmUgcGhvdG8g4oaSPC90ZXh0Pgo8L3N2Zz4="}, {"id": "ma13", "country": "ma", "cat": "caricature", "label": "Médina", "clue": "Les ruelles colorées des médinas sont uniques au Maroc.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcwIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cwIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2MxMjcyZCIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMCkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MCkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ1IiByeD0iNTgiIHJ5PSI2NSIgZmlsbD0iIzFhMGExYSIvPgogICAgICAgIDxwYXRoIGQ9Ik0xNDIgMTQ1IFExNDIgMTEwIDIwMCAxMDUgUTI1OCAxMTAgMjU4IDE0NSBRMjcwIDEzMCAyNzAgMTgwIFEyNzAgMjEwIDIwMCAyMTUgUTEzMCAyMTAgMTMwIDE4MCBRMTMwIDE1MCAxNDIgMTQ1WiIgZmlsbD0iI2MxMjcyZCIgb3BhY2l0eT0iMC43Ii8+CiAgICAgICAgPHBhdGggZD0iTTYwIDUzMyBRNzAgMzEwIDIwMCAyOTUgUTMzMCAzMTAgMzQwIDUzM1oiIGZpbGw9IiMxYTBhMWEiLz4KICA8dGV4dCB4PSIyMDAiIHk9IjQ0NSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSI1MiIgZm9udC1mYW1pbHk9InNlcmlmIj7wn4+b77iPPC90ZXh0PgogIDxyZWN0IHg9IjAiIHk9IjQ3MCIgd2lkdGg9IjQwMCIgaGVpZ2h0PSI2MyIgZmlsbD0icmdiYSgwLDAsMCwwLjUpIi8+CiAgPHRleHQgeD0iMjAwIiB5PSI0OTUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9InJnYmEoMjU1LDI1NSwyNTUsMC41KSIgZm9udC1zaXplPSIxMyIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPk3DqWRpbmE8L3RleHQ+CiAgPHRleHQgeD0iMjAwIiB5PSI1MTgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9IiNjMTI3MmQiIGZvbnQtc2l6ZT0iMTYiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+QWpvdXRlIHVuZSBwaG90byDihpI8L3RleHQ+Cjwvc3ZnPg=="}, {"id": "ma14", "country": "ma", "cat": "sport", "label": "Supporter", "clue": "Les supporters marocains et leurs tambours 🥁", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcxIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cxIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2MxMjcyZCIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMSkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MSkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTUwIiByeD0iNjAiIHJ5PSI3MCIgZmlsbD0iIzBhMWEwYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01NSA1MzMgUTY1IDMwMCAyMDAgMjg1IFEzMzUgMzAwIDM0NSA1MzNaIiBmaWxsPSIjMGExYTBhIi8+CiAgICAgICAgPHJlY3QgeD0iMTcwIiB5PSIyMTUiIHdpZHRoPSI2MCIgaGVpZ2h0PSIxNSIgcng9IjciIGZpbGw9IiNjMTI3MmQiIG9wYWNpdHk9IjAuNSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDQ1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjUyIiBmb250LWZhbWlseT0ic2VyaWYiPuKavTwvdGV4dD4KICA8cmVjdCB4PSIwIiB5PSI0NzAiIHdpZHRoPSI0MDAiIGhlaWdodD0iNjMiIGZpbGw9InJnYmEoMCwwLDAsMC41KSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDk1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJyZ2JhKDI1NSwyNTUsMjU1LDAuNSkiIGZvbnQtc2l6ZT0iMTMiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5TdXBwb3J0ZXI8L3RleHQ+CiAgPHRleHQgeD0iMjAwIiB5PSI1MTgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9IiNjMTI3MmQiIGZvbnQtc2l6ZT0iMTYiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+QWpvdXRlIHVuZSBwaG90byDihpI8L3RleHQ+Cjwvc3ZnPg=="}, {"id": "ma15", "country": "ma", "cat": "portrait", "label": "Femme du Souss", "clue": "Les bijoux en argent sont caractéristiques du Sud marocain.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcyIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cyIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2MxMjcyZCIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMikiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MikiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ4IiByeD0iNTUiIHJ5PSI2OCIgZmlsbD0iIzNhMmEzYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01MCA1MzMgUTYwIDI5NSAyMDAgMjgwIFEzNDAgMjk1IDM1MCA1MzNaIiBmaWxsPSIjM2EyYTNhIi8+CiAgICAgICAgPHBhdGggZD0iTTE1NSAxNDAgUTE3MCAxMTAgMjAwIDEwNSBRMjMwIDExMCAyNDUgMTQwIiBmaWxsPSJub25lIiBzdHJva2U9IiNjMTI3MmQiIHN0cm9rZS13aWR0aD0iOCIgb3BhY2l0eT0iMC42Ii8+CiAgPHRleHQgeD0iMjAwIiB5PSI0NDUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iNTIiIGZvbnQtZmFtaWx5PSJzZXJpZiI+8J+RqTwvdGV4dD4KICA8cmVjdCB4PSIwIiB5PSI0NzAiIHdpZHRoPSI0MDAiIGhlaWdodD0iNjMiIGZpbGw9InJnYmEoMCwwLDAsMC41KSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDk1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJyZ2JhKDI1NSwyNTUsMjU1LDAuNSkiIGZvbnQtc2l6ZT0iMTMiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5GZW1tZSBkdSBTb3VzczwvdGV4dD4KICA8dGV4dCB4PSIyMDAiIHk9IjUxOCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZmlsbD0iI2MxMjcyZCIgZm9udC1zaXplPSIxNiIgZm9udC13ZWlnaHQ9ImJvbGQiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5Bam91dGUgdW5lIHBob3RvIOKGkjwvdGV4dD4KPC9zdmc+"}, {"id": "ma16", "country": "ma", "cat": "portrait", "label": "Homme barbu", "clue": "La barbe soignée est très populaire chez les marocains.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmczIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3czIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2MxMjcyZCIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMykiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MykiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTUyIiByeD0iNjIiIHJ5PSI3MiIgZmlsbD0iIzJhM2EyYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01OCA1MzMgUTY4IDMwNSAyMDAgMjkwIFEzMzIgMzA1IDM0MiA1MzNaIiBmaWxsPSIjMmEzYTJhIi8+CiAgICAgICAgPGNpcmNsZSBjeD0iMjAwIiBjeT0iODAiIHI9IjM1IiBmaWxsPSJub25lIiBzdHJva2U9IiNjMTI3MmQiIHN0cm9rZS13aWR0aD0iNCIgb3BhY2l0eT0iMC40Ii8+CiAgPHRleHQgeD0iMjAwIiB5PSI0NDUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iNTIiIGZvbnQtZmFtaWx5PSJzZXJpZiI+8J+nlDwvdGV4dD4KICA8cmVjdCB4PSIwIiB5PSI0NzAiIHdpZHRoPSI0MDAiIGhlaWdodD0iNjMiIGZpbGw9InJnYmEoMCwwLDAsMC41KSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDk1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJyZ2JhKDI1NSwyNTUsMjU1LDAuNSkiIGZvbnQtc2l6ZT0iMTMiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5Ib21tZSBiYXJidTwvdGV4dD4KICA8dGV4dCB4PSIyMDAiIHk9IjUxOCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZmlsbD0iI2MxMjcyZCIgZm9udC1zaXplPSIxNiIgZm9udC13ZWlnaHQ9ImJvbGQiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5Bam91dGUgdW5lIHBob3RvIOKGkjwvdGV4dD4KPC9zdmc+"}, {"id": "ma17", "country": "ma", "cat": "portrait", "label": "Femme moderne", "clue": "Le mix tradition-modernité est la signature de la femme marocaine.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcwIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cwIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2MxMjcyZCIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMCkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MCkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ1IiByeD0iNTgiIHJ5PSI2NSIgZmlsbD0iIzNhM2EyYSIvPgogICAgICAgIDxwYXRoIGQ9Ik0xNDIgMTQ1IFExNDIgMTEwIDIwMCAxMDUgUTI1OCAxMTAgMjU4IDE0NSBRMjcwIDEzMCAyNzAgMTgwIFEyNzAgMjEwIDIwMCAyMTUgUTEzMCAyMTAgMTMwIDE4MCBRMTMwIDE1MCAxNDIgMTQ1WiIgZmlsbD0iI2MxMjcyZCIgb3BhY2l0eT0iMC43Ii8+CiAgICAgICAgPHBhdGggZD0iTTYwIDUzMyBRNzAgMzEwIDIwMCAyOTUgUTMzMCAzMTAgMzQwIDUzM1oiIGZpbGw9IiMzYTNhMmEiLz4KICA8dGV4dCB4PSIyMDAiIHk9IjQ0NSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSI1MiIgZm9udC1mYW1pbHk9InNlcmlmIj7wn5GpPC90ZXh0PgogIDxyZWN0IHg9IjAiIHk9IjQ3MCIgd2lkdGg9IjQwMCIgaGVpZ2h0PSI2MyIgZmlsbD0icmdiYSgwLDAsMCwwLjUpIi8+CiAgPHRleHQgeD0iMjAwIiB5PSI0OTUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9InJnYmEoMjU1LDI1NSwyNTUsMC41KSIgZm9udC1zaXplPSIxMyIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkZlbW1lIG1vZGVybmU8L3RleHQ+CiAgPHRleHQgeD0iMjAwIiB5PSI1MTgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9IiNjMTI3MmQiIGZvbnQtc2l6ZT0iMTYiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+QWpvdXRlIHVuZSBwaG90byDihpI8L3RleHQ+Cjwvc3ZnPg=="}, {"id": "ma18", "country": "ma", "cat": "portrait", "label": "Jeune homme", "clue": "Ce style de portrait est typique de la jeunesse de Casablanca.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcxIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cxIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2MxMjcyZCIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMSkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MSkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTUwIiByeD0iNjAiIHJ5PSI3MCIgZmlsbD0iIzJhMmEzYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01NSA1MzMgUTY1IDMwMCAyMDAgMjg1IFEzMzUgMzAwIDM0NSA1MzNaIiBmaWxsPSIjMmEyYTNhIi8+CiAgICAgICAgPHJlY3QgeD0iMTcwIiB5PSIyMTUiIHdpZHRoPSI2MCIgaGVpZ2h0PSIxNSIgcng9IjciIGZpbGw9IiNjMTI3MmQiIG9wYWNpdHk9IjAuNSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDQ1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjUyIiBmb250LWZhbWlseT0ic2VyaWYiPvCfp5E8L3RleHQ+CiAgPHJlY3QgeD0iMCIgeT0iNDcwIiB3aWR0aD0iNDAwIiBoZWlnaHQ9IjYzIiBmaWxsPSJyZ2JhKDAsMCwwLDAuNSkiLz4KICA8dGV4dCB4PSIyMDAiIHk9IjQ5NSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZmlsbD0icmdiYSgyNTUsMjU1LDI1NSwwLjUpIiBmb250LXNpemU9IjEzIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+SmV1bmUgaG9tbWU8L3RleHQ+CiAgPHRleHQgeD0iMjAwIiB5PSI1MTgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9IiNjMTI3MmQiIGZvbnQtc2l6ZT0iMTYiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+QWpvdXRlIHVuZSBwaG90byDihpI8L3RleHQ+Cjwvc3ZnPg=="}, {"id": "ma19", "country": "ma", "cat": "portrait", "label": "Femme bijoux", "clue": "Les bijoux rappellent l'artisanat de Tiznit.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcyIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cyIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2MxMjcyZCIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMikiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MikiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ4IiByeD0iNTUiIHJ5PSI2OCIgZmlsbD0iIzNhMmEyYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01MCA1MzMgUTYwIDI5NSAyMDAgMjgwIFEzNDAgMjk1IDM1MCA1MzNaIiBmaWxsPSIjM2EyYTJhIi8+CiAgICAgICAgPHBhdGggZD0iTTE1NSAxNDAgUTE3MCAxMTAgMjAwIDEwNSBRMjMwIDExMCAyNDUgMTQwIiBmaWxsPSJub25lIiBzdHJva2U9IiNjMTI3MmQiIHN0cm9rZS13aWR0aD0iOCIgb3BhY2l0eT0iMC42Ii8+CiAgPHRleHQgeD0iMjAwIiB5PSI0NDUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iNTIiIGZvbnQtZmFtaWx5PSJzZXJpZiI+8J+SjTwvdGV4dD4KICA8cmVjdCB4PSIwIiB5PSI0NzAiIHdpZHRoPSI0MDAiIGhlaWdodD0iNjMiIGZpbGw9InJnYmEoMCwwLDAsMC41KSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDk1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJyZ2JhKDI1NSwyNTUsMjU1LDAuNSkiIGZvbnQtc2l6ZT0iMTMiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5GZW1tZSBiaWpvdXg8L3RleHQ+CiAgPHRleHQgeD0iMjAwIiB5PSI1MTgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9IiNjMTI3MmQiIGZvbnQtc2l6ZT0iMTYiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+QWpvdXRlIHVuZSBwaG90byDihpI8L3RleHQ+Cjwvc3ZnPg=="}, {"id": "ma20", "country": "ma", "cat": "caricature", "label": "Style djellaba", "clue": "La djellaba et la chéchia sont typiquement marocaines.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmczIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3czIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2MxMjcyZCIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMykiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MykiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTUyIiByeD0iNjIiIHJ5PSI3MiIgZmlsbD0iIzJhM2EzYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01OCA1MzMgUTY4IDMwNSAyMDAgMjkwIFEzMzIgMzA1IDM0MiA1MzNaIiBmaWxsPSIjMmEzYTNhIi8+CiAgICAgICAgPGNpcmNsZSBjeD0iMjAwIiBjeT0iODAiIHI9IjM1IiBmaWxsPSJub25lIiBzdHJva2U9IiNjMTI3MmQiIHN0cm9rZS13aWR0aD0iNCIgb3BhY2l0eT0iMC40Ii8+CiAgPHRleHQgeD0iMjAwIiB5PSI0NDUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iNTIiIGZvbnQtZmFtaWx5PSJzZXJpZiI+8J+RmDwvdGV4dD4KICA8cmVjdCB4PSIwIiB5PSI0NzAiIHdpZHRoPSI0MDAiIGhlaWdodD0iNjMiIGZpbGw9InJnYmEoMCwwLDAsMC41KSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDk1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJyZ2JhKDI1NSwyNTUsMjU1LDAuNSkiIGZvbnQtc2l6ZT0iMTMiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5TdHlsZSBkamVsbGFiYTwvdGV4dD4KICA8dGV4dCB4PSIyMDAiIHk9IjUxOCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZmlsbD0iI2MxMjcyZCIgZm9udC1zaXplPSIxNiIgZm9udC13ZWlnaHQ9ImJvbGQiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5Bam91dGUgdW5lIHBob3RvIOKGkjwvdGV4dD4KPC9zdmc+"}, {"id": "ma21", "country": "ma", "cat": "portrait", "label": "Femme de Fès", "clue": "Fès est célèbre pour ses femmes élégantes et cultivées.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcwIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cwIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2MxMjcyZCIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMCkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MCkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ1IiByeD0iNTgiIHJ5PSI2NSIgZmlsbD0iIzNhMmEzYSIvPgogICAgICAgIDxwYXRoIGQ9Ik0xNDIgMTQ1IFExNDIgMTEwIDIwMCAxMDUgUTI1OCAxMTAgMjU4IDE0NSBRMjcwIDEzMCAyNzAgMTgwIFEyNzAgMjEwIDIwMCAyMTUgUTEzMCAyMTAgMTMwIDE4MCBRMTMwIDE1MCAxNDIgMTQ1WiIgZmlsbD0iI2MxMjcyZCIgb3BhY2l0eT0iMC43Ii8+CiAgICAgICAgPHBhdGggZD0iTTYwIDUzMyBRNzAgMzEwIDIwMCAyOTUgUTMzMCAzMTAgMzQwIDUzM1oiIGZpbGw9IiMzYTJhM2EiLz4KICA8dGV4dCB4PSIyMDAiIHk9IjQ0NSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSI1MiIgZm9udC1mYW1pbHk9InNlcmlmIj7wn5GpPC90ZXh0PgogIDxyZWN0IHg9IjAiIHk9IjQ3MCIgd2lkdGg9IjQwMCIgaGVpZ2h0PSI2MyIgZmlsbD0icmdiYSgwLDAsMCwwLjUpIi8+CiAgPHRleHQgeD0iMjAwIiB5PSI0OTUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9InJnYmEoMjU1LDI1NSwyNTUsMC41KSIgZm9udC1zaXplPSIxMyIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkZlbW1lIGRlIEbDqHM8L3RleHQ+CiAgPHRleHQgeD0iMjAwIiB5PSI1MTgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9IiNjMTI3MmQiIGZvbnQtc2l6ZT0iMTYiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+QWpvdXRlIHVuZSBwaG90byDihpI8L3RleHQ+Cjwvc3ZnPg=="}, {"id": "ma22", "country": "ma", "cat": "portrait", "label": "Homme classique", "clue": "Le style rappelle les hommes des médinas.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcxIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cxIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2MxMjcyZCIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMSkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MSkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTUwIiByeD0iNjAiIHJ5PSI3MCIgZmlsbD0iIzJhMmEzYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01NSA1MzMgUTY1IDMwMCAyMDAgMjg1IFEzMzUgMzAwIDM0NSA1MzNaIiBmaWxsPSIjMmEyYTNhIi8+CiAgICAgICAgPHJlY3QgeD0iMTcwIiB5PSIyMTUiIHdpZHRoPSI2MCIgaGVpZ2h0PSIxNSIgcng9IjciIGZpbGw9IiNjMTI3MmQiIG9wYWNpdHk9IjAuNSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDQ1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjUyIiBmb250LWZhbWlseT0ic2VyaWYiPvCfkag8L3RleHQ+CiAgPHJlY3QgeD0iMCIgeT0iNDcwIiB3aWR0aD0iNDAwIiBoZWlnaHQ9IjYzIiBmaWxsPSJyZ2JhKDAsMCwwLDAuNSkiLz4KICA8dGV4dCB4PSIyMDAiIHk9IjQ5NSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZmlsbD0icmdiYSgyNTUsMjU1LDI1NSwwLjUpIiBmb250LXNpemU9IjEzIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+SG9tbWUgY2xhc3NpcXVlPC90ZXh0PgogIDx0ZXh0IHg9IjIwMCIgeT0iNTE4IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSIjYzEyNzJkIiBmb250LXNpemU9IjE2IiBmb250LXdlaWdodD0iYm9sZCIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkFqb3V0ZSB1bmUgcGhvdG8g4oaSPC90ZXh0Pgo8L3N2Zz4="}, {"id": "ma23", "country": "ma", "cat": "portrait", "label": "Femme voilée", "clue": "Le voile coloré rappelle les femmes du Nord du Maroc.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcyIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cyIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2MxMjcyZCIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMikiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MikiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ4IiByeD0iNTUiIHJ5PSI2OCIgZmlsbD0iIzNhM2EyYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01MCA1MzMgUTYwIDI5NSAyMDAgMjgwIFEzNDAgMjk1IDM1MCA1MzNaIiBmaWxsPSIjM2EzYTJhIi8+CiAgICAgICAgPHBhdGggZD0iTTE1NSAxNDAgUTE3MCAxMTAgMjAwIDEwNSBRMjMwIDExMCAyNDUgMTQwIiBmaWxsPSJub25lIiBzdHJva2U9IiNjMTI3MmQiIHN0cm9rZS13aWR0aD0iOCIgb3BhY2l0eT0iMC42Ii8+CiAgPHRleHQgeD0iMjAwIiB5PSI0NDUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iNTIiIGZvbnQtZmFtaWx5PSJzZXJpZiI+8J+nlTwvdGV4dD4KICA8cmVjdCB4PSIwIiB5PSI0NzAiIHdpZHRoPSI0MDAiIGhlaWdodD0iNjMiIGZpbGw9InJnYmEoMCwwLDAsMC41KSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDk1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJyZ2JhKDI1NSwyNTUsMjU1LDAuNSkiIGZvbnQtc2l6ZT0iMTMiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5GZW1tZSB2b2lsw6llPC90ZXh0PgogIDx0ZXh0IHg9IjIwMCIgeT0iNTE4IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSIjYzEyNzJkIiBmb250LXNpemU9IjE2IiBmb250LXdlaWdodD0iYm9sZCIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkFqb3V0ZSB1bmUgcGhvdG8g4oaSPC90ZXh0Pgo8L3N2Zz4="}, {"id": "ma24", "country": "ma", "cat": "comic", "label": "Hammam", "clue": "Le hammam traditionnel est une institution au Maroc 🧖", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmczIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3czIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2MxMjcyZCIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMykiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MykiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTUyIiByeD0iNjIiIHJ5PSI3MiIgZmlsbD0iIzFhMWEyYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01OCA1MzMgUTY4IDMwNSAyMDAgMjkwIFEzMzIgMzA1IDM0MiA1MzNaIiBmaWxsPSIjMWExYTJhIi8+CiAgICAgICAgPGNpcmNsZSBjeD0iMjAwIiBjeT0iODAiIHI9IjM1IiBmaWxsPSJub25lIiBzdHJva2U9IiNjMTI3MmQiIHN0cm9rZS13aWR0aD0iNCIgb3BhY2l0eT0iMC40Ii8+CiAgPHRleHQgeD0iMjAwIiB5PSI0NDUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iNTIiIGZvbnQtZmFtaWx5PSJzZXJpZiI+8J+nljwvdGV4dD4KICA8cmVjdCB4PSIwIiB5PSI0NzAiIHdpZHRoPSI0MDAiIGhlaWdodD0iNjMiIGZpbGw9InJnYmEoMCwwLDAsMC41KSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDk1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJyZ2JhKDI1NSwyNTUsMjU1LDAuNSkiIGZvbnQtc2l6ZT0iMTMiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5IYW1tYW08L3RleHQ+CiAgPHRleHQgeD0iMjAwIiB5PSI1MTgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9IiNjMTI3MmQiIGZvbnQtc2l6ZT0iMTYiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+QWpvdXRlIHVuZSBwaG90byDihpI8L3RleHQ+Cjwvc3ZnPg=="}, {"id": "ma25", "country": "ma", "cat": "portrait", "label": "Homme de Rabat", "clue": "La posture décontractée des quartiers modernes de Rabat.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcwIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzFhMWEyZSIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cwIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2MxMjcyZCIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMCkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MCkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ1IiByeD0iNTgiIHJ5PSI2NSIgZmlsbD0iIzJhM2EyYSIvPgogICAgICAgIDxwYXRoIGQ9Ik0xNDIgMTQ1IFExNDIgMTEwIDIwMCAxMDUgUTI1OCAxMTAgMjU4IDE0NSBRMjcwIDEzMCAyNzAgMTgwIFEyNzAgMjEwIDIwMCAyMTUgUTEzMCAyMTAgMTMwIDE4MCBRMTMwIDE1MCAxNDIgMTQ1WiIgZmlsbD0iI2MxMjcyZCIgb3BhY2l0eT0iMC43Ii8+CiAgICAgICAgPHBhdGggZD0iTTYwIDUzMyBRNzAgMzEwIDIwMCAyOTUgUTMzMCAzMTAgMzQwIDUzM1oiIGZpbGw9IiMyYTNhMmEiLz4KICA8dGV4dCB4PSIyMDAiIHk9IjQ0NSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSI1MiIgZm9udC1mYW1pbHk9InNlcmlmIj7wn5GoPC90ZXh0PgogIDxyZWN0IHg9IjAiIHk9IjQ3MCIgd2lkdGg9IjQwMCIgaGVpZ2h0PSI2MyIgZmlsbD0icmdiYSgwLDAsMCwwLjUpIi8+CiAgPHRleHQgeD0iMjAwIiB5PSI0OTUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9InJnYmEoMjU1LDI1NSwyNTUsMC41KSIgZm9udC1zaXplPSIxMyIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkhvbW1lIGRlIFJhYmF0PC90ZXh0PgogIDx0ZXh0IHg9IjIwMCIgeT0iNTE4IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSIjYzEyNzJkIiBmb250LXNpemU9IjE2IiBmb250LXdlaWdodD0iYm9sZCIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkFqb3V0ZSB1bmUgcGhvdG8g4oaSPC90ZXh0Pgo8L3N2Zz4="}, {"id": "dz26", "country": "dz", "cat": "portrait", "label": "Femme d'Alger", "clue": "Style élégant caractéristique des femmes d'Alger ou Oran.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcwIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cwIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwNzIyOSIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMCkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MCkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ1IiByeD0iNTgiIHJ5PSI2NSIgZmlsbD0iIzBhMWEwYSIvPgogICAgICAgIDxwYXRoIGQ9Ik0xNDIgMTQ1IFExNDIgMTEwIDIwMCAxMDUgUTI1OCAxMTAgMjU4IDE0NSBRMjcwIDEzMCAyNzAgMTgwIFEyNzAgMjEwIDIwMCAyMTUgUTEzMCAyMTAgMTMwIDE4MCBRMTMwIDE1MCAxNDIgMTQ1WiIgZmlsbD0iIzAwNzIyOSIgb3BhY2l0eT0iMC43Ii8+CiAgICAgICAgPHBhdGggZD0iTTYwIDUzMyBRNzAgMzEwIDIwMCAyOTUgUTMzMCAzMTAgMzQwIDUzM1oiIGZpbGw9IiMwYTFhMGEiLz4KICA8dGV4dCB4PSIyMDAiIHk9IjQ0NSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSI1MiIgZm9udC1mYW1pbHk9InNlcmlmIj7wn5GpPC90ZXh0PgogIDxyZWN0IHg9IjAiIHk9IjQ3MCIgd2lkdGg9IjQwMCIgaGVpZ2h0PSI2MyIgZmlsbD0icmdiYSgwLDAsMCwwLjUpIi8+CiAgPHRleHQgeD0iMjAwIiB5PSI0OTUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9InJnYmEoMjU1LDI1NSwyNTUsMC41KSIgZm9udC1zaXplPSIxMyIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkZlbW1lIGQnQWxnZXI8L3RleHQ+CiAgPHRleHQgeD0iMjAwIiB5PSI1MTgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9IiMwMDcyMjkiIGZvbnQtc2l6ZT0iMTYiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+QWpvdXRlIHVuZSBwaG90byDihpI8L3RleHQ+Cjwvc3ZnPg=="}, {"id": "dz27", "country": "dz", "cat": "portrait", "label": "Femme de Constantine", "clue": "La sérénité du regard rappelle les femmes de Constantine.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcxIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cxIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwNzIyOSIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMSkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MSkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTUwIiByeD0iNjAiIHJ5PSI3MCIgZmlsbD0iIzBhMmEwYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01NSA1MzMgUTY1IDMwMCAyMDAgMjg1IFEzMzUgMzAwIDM0NSA1MzNaIiBmaWxsPSIjMGEyYTBhIi8+CiAgICAgICAgPHJlY3QgeD0iMTcwIiB5PSIyMTUiIHdpZHRoPSI2MCIgaGVpZ2h0PSIxNSIgcng9IjciIGZpbGw9IiMwMDcyMjkiIG9wYWNpdHk9IjAuNSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDQ1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjUyIiBmb250LWZhbWlseT0ic2VyaWYiPvCfkak8L3RleHQ+CiAgPHJlY3QgeD0iMCIgeT0iNDcwIiB3aWR0aD0iNDAwIiBoZWlnaHQ9IjYzIiBmaWxsPSJyZ2JhKDAsMCwwLDAuNSkiLz4KICA8dGV4dCB4PSIyMDAiIHk9IjQ5NSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZmlsbD0icmdiYSgyNTUsMjU1LDI1NSwwLjUpIiBmb250LXNpemU9IjEzIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+RmVtbWUgZGUgQ29uc3RhbnRpbmU8L3RleHQ+CiAgPHRleHQgeD0iMjAwIiB5PSI1MTgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9IiMwMDcyMjkiIGZvbnQtc2l6ZT0iMTYiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+QWpvdXRlIHVuZSBwaG90byDihpI8L3RleHQ+Cjwvc3ZnPg=="}, {"id": "dz28", "country": "dz", "cat": "portrait", "label": "Femme algéroise", "clue": "L'allure moderne est caractéristique d'Alger-Centre.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcyIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cyIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwNzIyOSIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMikiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MikiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ4IiByeD0iNTUiIHJ5PSI2OCIgZmlsbD0iIzBhMWExYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01MCA1MzMgUTYwIDI5NSAyMDAgMjgwIFEzNDAgMjk1IDM1MCA1MzNaIiBmaWxsPSIjMGExYTFhIi8+CiAgICAgICAgPHBhdGggZD0iTTE1NSAxNDAgUTE3MCAxMTAgMjAwIDEwNSBRMjMwIDExMCAyNDUgMTQwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDcyMjkiIHN0cm9rZS13aWR0aD0iOCIgb3BhY2l0eT0iMC42Ii8+CiAgPHRleHQgeD0iMjAwIiB5PSI0NDUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iNTIiIGZvbnQtZmFtaWx5PSJzZXJpZiI+8J+nlTwvdGV4dD4KICA8cmVjdCB4PSIwIiB5PSI0NzAiIHdpZHRoPSI0MDAiIGhlaWdodD0iNjMiIGZpbGw9InJnYmEoMCwwLDAsMC41KSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDk1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJyZ2JhKDI1NSwyNTUsMjU1LDAuNSkiIGZvbnQtc2l6ZT0iMTMiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5GZW1tZSBhbGfDqXJvaXNlPC90ZXh0PgogIDx0ZXh0IHg9IjIwMCIgeT0iNTE4IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSIjMDA3MjI5IiBmb250LXNpemU9IjE2IiBmb250LXdlaWdodD0iYm9sZCIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkFqb3V0ZSB1bmUgcGhvdG8g4oaSPC90ZXh0Pgo8L3N2Zz4="}, {"id": "dz29", "country": "dz", "cat": "portrait", "label": "Femme souriante", "clue": "Ce sourire chaleureux rappelle les femmes des hauts plateaux.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmczIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3czIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwNzIyOSIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMykiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MykiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTUyIiByeD0iNjIiIHJ5PSI3MiIgZmlsbD0iIzFhMmEwYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01OCA1MzMgUTY4IDMwNSAyMDAgMjkwIFEzMzIgMzA1IDM0MiA1MzNaIiBmaWxsPSIjMWEyYTBhIi8+CiAgICAgICAgPGNpcmNsZSBjeD0iMjAwIiBjeT0iODAiIHI9IjM1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDcyMjkiIHN0cm9rZS13aWR0aD0iNCIgb3BhY2l0eT0iMC40Ii8+CiAgPHRleHQgeD0iMjAwIiB5PSI0NDUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iNTIiIGZvbnQtZmFtaWx5PSJzZXJpZiI+8J+ZgjwvdGV4dD4KICA8cmVjdCB4PSIwIiB5PSI0NzAiIHdpZHRoPSI0MDAiIGhlaWdodD0iNjMiIGZpbGw9InJnYmEoMCwwLDAsMC41KSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDk1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJyZ2JhKDI1NSwyNTUsMjU1LDAuNSkiIGZvbnQtc2l6ZT0iMTMiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5GZW1tZSBzb3VyaWFudGU8L3RleHQ+CiAgPHRleHQgeD0iMjAwIiB5PSI1MTgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9IiMwMDcyMjkiIGZvbnQtc2l6ZT0iMTYiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+QWpvdXRlIHVuZSBwaG90byDihpI8L3RleHQ+Cjwvc3ZnPg=="}, {"id": "dz30", "country": "dz", "cat": "portrait", "label": "Homme algérien", "clue": "La posture assurée rappelle les hommes de la Mitidja.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcwIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cwIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwNzIyOSIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMCkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MCkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ1IiByeD0iNTgiIHJ5PSI2NSIgZmlsbD0iIzBhMGExYSIvPgogICAgICAgIDxwYXRoIGQ9Ik0xNDIgMTQ1IFExNDIgMTEwIDIwMCAxMDUgUTI1OCAxMTAgMjU4IDE0NSBRMjcwIDEzMCAyNzAgMTgwIFEyNzAgMjEwIDIwMCAyMTUgUTEzMCAyMTAgMTMwIDE4MCBRMTMwIDE1MCAxNDIgMTQ1WiIgZmlsbD0iIzAwNzIyOSIgb3BhY2l0eT0iMC43Ii8+CiAgICAgICAgPHBhdGggZD0iTTYwIDUzMyBRNzAgMzEwIDIwMCAyOTUgUTMzMCAzMTAgMzQwIDUzM1oiIGZpbGw9IiMwYTBhMWEiLz4KICA8dGV4dCB4PSIyMDAiIHk9IjQ0NSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSI1MiIgZm9udC1mYW1pbHk9InNlcmlmIj7wn5GoPC90ZXh0PgogIDxyZWN0IHg9IjAiIHk9IjQ3MCIgd2lkdGg9IjQwMCIgaGVpZ2h0PSI2MyIgZmlsbD0icmdiYSgwLDAsMCwwLjUpIi8+CiAgPHRleHQgeD0iMjAwIiB5PSI0OTUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9InJnYmEoMjU1LDI1NSwyNTUsMC41KSIgZm9udC1zaXplPSIxMyIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkhvbW1lIGFsZ8OpcmllbjwvdGV4dD4KICA8dGV4dCB4PSIyMDAiIHk9IjUxOCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZmlsbD0iIzAwNzIyOSIgZm9udC1zaXplPSIxNiIgZm9udC13ZWlnaHQ9ImJvbGQiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5Bam91dGUgdW5lIHBob3RvIOKGkjwvdGV4dD4KPC9zdmc+"}, {"id": "dz31", "country": "dz", "cat": "portrait", "label": "Femme kabyle", "clue": "Style naturel typique de Tizi Ouzou ou Béjaïa.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcxIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cxIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwNzIyOSIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMSkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MSkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTUwIiByeD0iNjAiIHJ5PSI3MCIgZmlsbD0iIzFhMWEwYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01NSA1MzMgUTY1IDMwMCAyMDAgMjg1IFEzMzUgMzAwIDM0NSA1MzNaIiBmaWxsPSIjMWExYTBhIi8+CiAgICAgICAgPHJlY3QgeD0iMTcwIiB5PSIyMTUiIHdpZHRoPSI2MCIgaGVpZ2h0PSIxNSIgcng9IjciIGZpbGw9IiMwMDcyMjkiIG9wYWNpdHk9IjAuNSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDQ1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjUyIiBmb250LWZhbWlseT0ic2VyaWYiPvCfkak8L3RleHQ+CiAgPHJlY3QgeD0iMCIgeT0iNDcwIiB3aWR0aD0iNDAwIiBoZWlnaHQ9IjYzIiBmaWxsPSJyZ2JhKDAsMCwwLDAuNSkiLz4KICA8dGV4dCB4PSIyMDAiIHk9IjQ5NSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZmlsbD0icmdiYSgyNTUsMjU1LDI1NSwwLjUpIiBmb250LXNpemU9IjEzIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+RmVtbWUga2FieWxlPC90ZXh0PgogIDx0ZXh0IHg9IjIwMCIgeT0iNTE4IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSIjMDA3MjI5IiBmb250LXNpemU9IjE2IiBmb250LXdlaWdodD0iYm9sZCIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkFqb3V0ZSB1bmUgcGhvdG8g4oaSPC90ZXh0Pgo8L3N2Zz4="}, {"id": "dz32", "country": "dz", "cat": "portrait", "label": "Homme d'Oran", "clue": "Coiffure et style vestimentaire de la jeunesse d'Oran.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcyIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cyIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwNzIyOSIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMikiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MikiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ4IiByeD0iNTUiIHJ5PSI2OCIgZmlsbD0iIzBhMWEwYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01MCA1MzMgUTYwIDI5NSAyMDAgMjgwIFEzNDAgMjk1IDM1MCA1MzNaIiBmaWxsPSIjMGExYTBhIi8+CiAgICAgICAgPHBhdGggZD0iTTE1NSAxNDAgUTE3MCAxMTAgMjAwIDEwNSBRMjMwIDExMCAyNDUgMTQwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDcyMjkiIHN0cm9rZS13aWR0aD0iOCIgb3BhY2l0eT0iMC42Ii8+CiAgPHRleHQgeD0iMjAwIiB5PSI0NDUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iNTIiIGZvbnQtZmFtaWx5PSJzZXJpZiI+8J+nlDwvdGV4dD4KICA8cmVjdCB4PSIwIiB5PSI0NzAiIHdpZHRoPSI0MDAiIGhlaWdodD0iNjMiIGZpbGw9InJnYmEoMCwwLDAsMC41KSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDk1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJyZ2JhKDI1NSwyNTUsMjU1LDAuNSkiIGZvbnQtc2l6ZT0iMTMiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5Ib21tZSBkJ09yYW48L3RleHQ+CiAgPHRleHQgeD0iMjAwIiB5PSI1MTgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9IiMwMDcyMjkiIGZvbnQtc2l6ZT0iMTYiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+QWpvdXRlIHVuZSBwaG90byDihpI8L3RleHQ+Cjwvc3ZnPg=="}, {"id": "dz33", "country": "dz", "cat": "portrait", "label": "Femme berbère", "clue": "La vivacité du regard rappelle les femmes berbères de Kabylie.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmczIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3czIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwNzIyOSIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMykiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MykiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTUyIiByeD0iNjIiIHJ5PSI3MiIgZmlsbD0iIzFhMGExYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01OCA1MzMgUTY4IDMwNSAyMDAgMjkwIFEzMzIgMzA1IDM0MiA1MzNaIiBmaWxsPSIjMWEwYTFhIi8+CiAgICAgICAgPGNpcmNsZSBjeD0iMjAwIiBjeT0iODAiIHI9IjM1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDcyMjkiIHN0cm9rZS13aWR0aD0iNCIgb3BhY2l0eT0iMC40Ii8+CiAgPHRleHQgeD0iMjAwIiB5PSI0NDUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iNTIiIGZvbnQtZmFtaWx5PSJzZXJpZiI+8J+RqTwvdGV4dD4KICA8cmVjdCB4PSIwIiB5PSI0NzAiIHdpZHRoPSI0MDAiIGhlaWdodD0iNjMiIGZpbGw9InJnYmEoMCwwLDAsMC41KSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDk1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJyZ2JhKDI1NSwyNTUsMjU1LDAuNSkiIGZvbnQtc2l6ZT0iMTMiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5GZW1tZSBiZXJiw6hyZTwvdGV4dD4KICA8dGV4dCB4PSIyMDAiIHk9IjUxOCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZmlsbD0iIzAwNzIyOSIgZm9udC1zaXplPSIxNiIgZm9udC13ZWlnaHQ9ImJvbGQiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5Bam91dGUgdW5lIHBob3RvIOKGkjwvdGV4dD4KPC9zdmc+"}, {"id": "dz34", "country": "dz", "cat": "portrait", "label": "Homme barbu", "clue": "La barbe soignée est très populaire chez les hommes d'Alger.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcwIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cwIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwNzIyOSIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMCkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MCkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ1IiByeD0iNTgiIHJ5PSI2NSIgZmlsbD0iIzBhMmEwYSIvPgogICAgICAgIDxwYXRoIGQ9Ik0xNDIgMTQ1IFExNDIgMTEwIDIwMCAxMDUgUTI1OCAxMTAgMjU4IDE0NSBRMjcwIDEzMCAyNzAgMTgwIFEyNzAgMjEwIDIwMCAyMTUgUTEzMCAyMTAgMTMwIDE4MCBRMTMwIDE1MCAxNDIgMTQ1WiIgZmlsbD0iIzAwNzIyOSIgb3BhY2l0eT0iMC43Ii8+CiAgICAgICAgPHBhdGggZD0iTTYwIDUzMyBRNzAgMzEwIDIwMCAyOTUgUTMzMCAzMTAgMzQwIDUzM1oiIGZpbGw9IiMwYTJhMGEiLz4KICA8dGV4dCB4PSIyMDAiIHk9IjQ0NSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSI1MiIgZm9udC1mYW1pbHk9InNlcmlmIj7wn6eUPC90ZXh0PgogIDxyZWN0IHg9IjAiIHk9IjQ3MCIgd2lkdGg9IjQwMCIgaGVpZ2h0PSI2MyIgZmlsbD0icmdiYSgwLDAsMCwwLjUpIi8+CiAgPHRleHQgeD0iMjAwIiB5PSI0OTUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9InJnYmEoMjU1LDI1NSwyNTUsMC41KSIgZm9udC1zaXplPSIxMyIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkhvbW1lIGJhcmJ1PC90ZXh0PgogIDx0ZXh0IHg9IjIwMCIgeT0iNTE4IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSIjMDA3MjI5IiBmb250LXNpemU9IjE2IiBmb250LXdlaWdodD0iYm9sZCIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkFqb3V0ZSB1bmUgcGhvdG8g4oaSPC90ZXh0Pgo8L3N2Zz4="}, {"id": "dz35", "country": "dz", "cat": "portrait", "label": "Homme du Sahara", "clue": "Le regard posé rappelle les hommes du Sahara algérien.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcxIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cxIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwNzIyOSIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMSkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MSkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTUwIiByeD0iNjAiIHJ5PSI3MCIgZmlsbD0iIzFhMWEwYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01NSA1MzMgUTY1IDMwMCAyMDAgMjg1IFEzMzUgMzAwIDM0NSA1MzNaIiBmaWxsPSIjMWExYTBhIi8+CiAgICAgICAgPHJlY3QgeD0iMTcwIiB5PSIyMTUiIHdpZHRoPSI2MCIgaGVpZ2h0PSIxNSIgcng9IjciIGZpbGw9IiMwMDcyMjkiIG9wYWNpdHk9IjAuNSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDQ1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjUyIiBmb250LWZhbWlseT0ic2VyaWYiPvCfkag8L3RleHQ+CiAgPHJlY3QgeD0iMCIgeT0iNDcwIiB3aWR0aD0iNDAwIiBoZWlnaHQ9IjYzIiBmaWxsPSJyZ2JhKDAsMCwwLDAuNSkiLz4KICA8dGV4dCB4PSIyMDAiIHk9IjQ5NSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZmlsbD0icmdiYSgyNTUsMjU1LDI1NSwwLjUpIiBmb250LXNpemU9IjEzIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+SG9tbWUgZHUgU2FoYXJhPC90ZXh0PgogIDx0ZXh0IHg9IjIwMCIgeT0iNTE4IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSIjMDA3MjI5IiBmb250LXNpemU9IjE2IiBmb250LXdlaWdodD0iYm9sZCIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkFqb3V0ZSB1bmUgcGhvdG8g4oaSPC90ZXh0Pgo8L3N2Zz4="}, {"id": "dz36", "country": "dz", "cat": "portrait", "label": "Femme d'Annaba", "clue": "Style moderne des femmes d'Annaba ou Skikda.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcyIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cyIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwNzIyOSIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMikiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MikiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ4IiByeD0iNTUiIHJ5PSI2OCIgZmlsbD0iIzBhMWExYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01MCA1MzMgUTYwIDI5NSAyMDAgMjgwIFEzNDAgMjk1IDM1MCA1MzNaIiBmaWxsPSIjMGExYTFhIi8+CiAgICAgICAgPHBhdGggZD0iTTE1NSAxNDAgUTE3MCAxMTAgMjAwIDEwNSBRMjMwIDExMCAyNDUgMTQwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDcyMjkiIHN0cm9rZS13aWR0aD0iOCIgb3BhY2l0eT0iMC42Ii8+CiAgPHRleHQgeD0iMjAwIiB5PSI0NDUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iNTIiIGZvbnQtZmFtaWx5PSJzZXJpZiI+8J+RqTwvdGV4dD4KICA8cmVjdCB4PSIwIiB5PSI0NzAiIHdpZHRoPSI0MDAiIGhlaWdodD0iNjMiIGZpbGw9InJnYmEoMCwwLDAsMC41KSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDk1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJyZ2JhKDI1NSwyNTUsMjU1LDAuNSkiIGZvbnQtc2l6ZT0iMTMiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5GZW1tZSBkJ0FubmFiYTwvdGV4dD4KICA8dGV4dCB4PSIyMDAiIHk9IjUxOCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZmlsbD0iIzAwNzIyOSIgZm9udC1zaXplPSIxNiIgZm9udC13ZWlnaHQ9ImJvbGQiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5Bam91dGUgdW5lIHBob3RvIOKGkjwvdGV4dD4KPC9zdmc+"}, {"id": "dz37", "country": "dz", "cat": "portrait", "label": "Homme élégant", "clue": "L'élégance épurée des cadres des grandes villes algériennes.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmczIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3czIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwNzIyOSIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMykiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MykiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTUyIiByeD0iNjIiIHJ5PSI3MiIgZmlsbD0iIzFhMGEwYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01OCA1MzMgUTY4IDMwNSAyMDAgMjkwIFEzMzIgMzA1IDM0MiA1MzNaIiBmaWxsPSIjMWEwYTBhIi8+CiAgICAgICAgPGNpcmNsZSBjeD0iMjAwIiBjeT0iODAiIHI9IjM1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDcyMjkiIHN0cm9rZS13aWR0aD0iNCIgb3BhY2l0eT0iMC40Ii8+CiAgPHRleHQgeD0iMjAwIiB5PSI0NDUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iNTIiIGZvbnQtZmFtaWx5PSJzZXJpZiI+8J+RqDwvdGV4dD4KICA8cmVjdCB4PSIwIiB5PSI0NzAiIHdpZHRoPSI0MDAiIGhlaWdodD0iNjMiIGZpbGw9InJnYmEoMCwwLDAsMC41KSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDk1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJyZ2JhKDI1NSwyNTUsMjU1LDAuNSkiIGZvbnQtc2l6ZT0iMTMiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5Ib21tZSDDqWzDqWdhbnQ8L3RleHQ+CiAgPHRleHQgeD0iMjAwIiB5PSI1MTgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9IiMwMDcyMjkiIGZvbnQtc2l6ZT0iMTYiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+QWpvdXRlIHVuZSBwaG90byDihpI8L3RleHQ+Cjwvc3ZnPg=="}, {"id": "dz38", "country": "dz", "cat": "comic", "label": "Couscous vendredi", "clue": "Le couscous du vendredi est sacré en Algérie ! 🍽️", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcwIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cwIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwNzIyOSIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMCkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MCkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ1IiByeD0iNTgiIHJ5PSI2NSIgZmlsbD0iIzBhMWEwYSIvPgogICAgICAgIDxwYXRoIGQ9Ik0xNDIgMTQ1IFExNDIgMTEwIDIwMCAxMDUgUTI1OCAxMTAgMjU4IDE0NSBRMjcwIDEzMCAyNzAgMTgwIFEyNzAgMjEwIDIwMCAyMTUgUTEzMCAyMTAgMTMwIDE4MCBRMTMwIDE1MCAxNDIgMTQ1WiIgZmlsbD0iIzAwNzIyOSIgb3BhY2l0eT0iMC43Ii8+CiAgICAgICAgPHBhdGggZD0iTTYwIDUzMyBRNzAgMzEwIDIwMCAyOTUgUTMzMCAzMTAgMzQwIDUzM1oiIGZpbGw9IiMwYTFhMGEiLz4KICA8dGV4dCB4PSIyMDAiIHk9IjQ0NSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSI1MiIgZm9udC1mYW1pbHk9InNlcmlmIj7wn42977iPPC90ZXh0PgogIDxyZWN0IHg9IjAiIHk9IjQ3MCIgd2lkdGg9IjQwMCIgaGVpZ2h0PSI2MyIgZmlsbD0icmdiYSgwLDAsMCwwLjUpIi8+CiAgPHRleHQgeD0iMjAwIiB5PSI0OTUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9InJnYmEoMjU1LDI1NSwyNTUsMC41KSIgZm9udC1zaXplPSIxMyIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkNvdXNjb3VzIHZlbmRyZWRpPC90ZXh0PgogIDx0ZXh0IHg9IjIwMCIgeT0iNTE4IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSIjMDA3MjI5IiBmb250LXNpemU9IjE2IiBmb250LXdlaWdodD0iYm9sZCIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkFqb3V0ZSB1bmUgcGhvdG8g4oaSPC90ZXh0Pgo8L3N2Zz4="}, {"id": "dz39", "country": "dz", "cat": "comic", "label": "Café Alger", "clue": "Le café fort et la clope — rituel du matin algérien ☕", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcxIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cxIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwNzIyOSIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMSkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MSkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTUwIiByeD0iNjAiIHJ5PSI3MCIgZmlsbD0iIzBhMGExYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01NSA1MzMgUTY1IDMwMCAyMDAgMjg1IFEzMzUgMzAwIDM0NSA1MzNaIiBmaWxsPSIjMGEwYTFhIi8+CiAgICAgICAgPHJlY3QgeD0iMTcwIiB5PSIyMTUiIHdpZHRoPSI2MCIgaGVpZ2h0PSIxNSIgcng9IjciIGZpbGw9IiMwMDcyMjkiIG9wYWNpdHk9IjAuNSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDQ1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjUyIiBmb250LWZhbWlseT0ic2VyaWYiPuKYlTwvdGV4dD4KICA8cmVjdCB4PSIwIiB5PSI0NzAiIHdpZHRoPSI0MDAiIGhlaWdodD0iNjMiIGZpbGw9InJnYmEoMCwwLDAsMC41KSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDk1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJyZ2JhKDI1NSwyNTUsMjU1LDAuNSkiIGZvbnQtc2l6ZT0iMTMiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5DYWbDqSBBbGdlcjwvdGV4dD4KICA8dGV4dCB4PSIyMDAiIHk9IjUxOCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZmlsbD0iIzAwNzIyOSIgZm9udC1zaXplPSIxNiIgZm9udC13ZWlnaHQ9ImJvbGQiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5Bam91dGUgdW5lIHBob3RvIOKGkjwvdGV4dD4KPC9zdmc+"}, {"id": "dz40", "country": "dz", "cat": "caricature", "label": "Casbah", "clue": "La Casbah d'Alger est classée UNESCO 🏛️", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcyIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cyIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwNzIyOSIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMikiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MikiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ4IiByeD0iNTUiIHJ5PSI2OCIgZmlsbD0iIzFhMGExYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01MCA1MzMgUTYwIDI5NSAyMDAgMjgwIFEzNDAgMjk1IDM1MCA1MzNaIiBmaWxsPSIjMWEwYTFhIi8+CiAgICAgICAgPHBhdGggZD0iTTE1NSAxNDAgUTE3MCAxMTAgMjAwIDEwNSBRMjMwIDExMCAyNDUgMTQwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDcyMjkiIHN0cm9rZS13aWR0aD0iOCIgb3BhY2l0eT0iMC42Ii8+CiAgPHRleHQgeD0iMjAwIiB5PSI0NDUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iNTIiIGZvbnQtZmFtaWx5PSJzZXJpZiI+8J+Pm++4jzwvdGV4dD4KICA8cmVjdCB4PSIwIiB5PSI0NzAiIHdpZHRoPSI0MDAiIGhlaWdodD0iNjMiIGZpbGw9InJnYmEoMCwwLDAsMC41KSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDk1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJyZ2JhKDI1NSwyNTUsMjU1LDAuNSkiIGZvbnQtc2l6ZT0iMTMiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5DYXNiYWg8L3RleHQ+CiAgPHRleHQgeD0iMjAwIiB5PSI1MTgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9IiMwMDcyMjkiIGZvbnQtc2l6ZT0iMTYiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+QWpvdXRlIHVuZSBwaG90byDihpI8L3RleHQ+Cjwvc3ZnPg=="}, {"id": "dz41", "country": "dz", "cat": "portrait", "label": "Femme moderne", "clue": "Le mix tradition-modernité est typique de la femme algérienne.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmczIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3czIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwNzIyOSIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMykiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MykiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTUyIiByeD0iNjIiIHJ5PSI3MiIgZmlsbD0iIzBhMWEwYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01OCA1MzMgUTY4IDMwNSAyMDAgMjkwIFEzMzIgMzA1IDM0MiA1MzNaIiBmaWxsPSIjMGExYTBhIi8+CiAgICAgICAgPGNpcmNsZSBjeD0iMjAwIiBjeT0iODAiIHI9IjM1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDcyMjkiIHN0cm9rZS13aWR0aD0iNCIgb3BhY2l0eT0iMC40Ii8+CiAgPHRleHQgeD0iMjAwIiB5PSI0NDUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iNTIiIGZvbnQtZmFtaWx5PSJzZXJpZiI+8J+RqTwvdGV4dD4KICA8cmVjdCB4PSIwIiB5PSI0NzAiIHdpZHRoPSI0MDAiIGhlaWdodD0iNjMiIGZpbGw9InJnYmEoMCwwLDAsMC41KSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDk1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJyZ2JhKDI1NSwyNTUsMjU1LDAuNSkiIGZvbnQtc2l6ZT0iMTMiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5GZW1tZSBtb2Rlcm5lPC90ZXh0PgogIDx0ZXh0IHg9IjIwMCIgeT0iNTE4IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSIjMDA3MjI5IiBmb250LXNpemU9IjE2IiBmb250LXdlaWdodD0iYm9sZCIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkFqb3V0ZSB1bmUgcGhvdG8g4oaSPC90ZXh0Pgo8L3N2Zz4="}, {"id": "dz42", "country": "dz", "cat": "sport", "label": "Supporter", "clue": "Les supporters algériens sont parmi les plus passionnés d'Afrique 🟢", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcwIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cwIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwNzIyOSIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMCkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MCkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ1IiByeD0iNTgiIHJ5PSI2NSIgZmlsbD0iIzFhMWEwYSIvPgogICAgICAgIDxwYXRoIGQ9Ik0xNDIgMTQ1IFExNDIgMTEwIDIwMCAxMDUgUTI1OCAxMTAgMjU4IDE0NSBRMjcwIDEzMCAyNzAgMTgwIFEyNzAgMjEwIDIwMCAyMTUgUTEzMCAyMTAgMTMwIDE4MCBRMTMwIDE1MCAxNDIgMTQ1WiIgZmlsbD0iIzAwNzIyOSIgb3BhY2l0eT0iMC43Ii8+CiAgICAgICAgPHBhdGggZD0iTTYwIDUzMyBRNzAgMzEwIDIwMCAyOTUgUTMzMCAzMTAgMzQwIDUzM1oiIGZpbGw9IiMxYTFhMGEiLz4KICA8dGV4dCB4PSIyMDAiIHk9IjQ0NSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSI1MiIgZm9udC1mYW1pbHk9InNlcmlmIj7imr08L3RleHQ+CiAgPHJlY3QgeD0iMCIgeT0iNDcwIiB3aWR0aD0iNDAwIiBoZWlnaHQ9IjYzIiBmaWxsPSJyZ2JhKDAsMCwwLDAuNSkiLz4KICA8dGV4dCB4PSIyMDAiIHk9IjQ5NSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZmlsbD0icmdiYSgyNTUsMjU1LDI1NSwwLjUpIiBmb250LXNpemU9IjEzIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+U3VwcG9ydGVyPC90ZXh0PgogIDx0ZXh0IHg9IjIwMCIgeT0iNTE4IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSIjMDA3MjI5IiBmb250LXNpemU9IjE2IiBmb250LXdlaWdodD0iYm9sZCIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkFqb3V0ZSB1bmUgcGhvdG8g4oaSPC90ZXh0Pgo8L3N2Zz4="}, {"id": "dz43", "country": "dz", "cat": "portrait", "label": "Jeune femme", "clue": "La jeunesse algérienne est connue pour son style affirmé.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcxIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cxIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwNzIyOSIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMSkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MSkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTUwIiByeD0iNjAiIHJ5PSI3MCIgZmlsbD0iIzBhMmEwYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01NSA1MzMgUTY1IDMwMCAyMDAgMjg1IFEzMzUgMzAwIDM0NSA1MzNaIiBmaWxsPSIjMGEyYTBhIi8+CiAgICAgICAgPHJlY3QgeD0iMTcwIiB5PSIyMTUiIHdpZHRoPSI2MCIgaGVpZ2h0PSIxNSIgcng9IjciIGZpbGw9IiMwMDcyMjkiIG9wYWNpdHk9IjAuNSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDQ1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjUyIiBmb250LWZhbWlseT0ic2VyaWYiPvCfp5E8L3RleHQ+CiAgPHJlY3QgeD0iMCIgeT0iNDcwIiB3aWR0aD0iNDAwIiBoZWlnaHQ9IjYzIiBmaWxsPSJyZ2JhKDAsMCwwLDAuNSkiLz4KICA8dGV4dCB4PSIyMDAiIHk9IjQ5NSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZmlsbD0icmdiYSgyNTUsMjU1LDI1NSwwLjUpIiBmb250LXNpemU9IjEzIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+SmV1bmUgZmVtbWU8L3RleHQ+CiAgPHRleHQgeD0iMjAwIiB5PSI1MTgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9IiMwMDcyMjkiIGZvbnQtc2l6ZT0iMTYiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+QWpvdXRlIHVuZSBwaG90byDihpI8L3RleHQ+Cjwvc3ZnPg=="}, {"id": "dz44", "country": "dz", "cat": "portrait", "label": "Homme jeune", "clue": "Ce style décontracté est très répandu à Alger.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcyIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cyIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwNzIyOSIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMikiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MikiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ4IiByeD0iNTUiIHJ5PSI2OCIgZmlsbD0iIzBhMWExYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01MCA1MzMgUTYwIDI5NSAyMDAgMjgwIFEzNDAgMjk1IDM1MCA1MzNaIiBmaWxsPSIjMGExYTFhIi8+CiAgICAgICAgPHBhdGggZD0iTTE1NSAxNDAgUTE3MCAxMTAgMjAwIDEwNSBRMjMwIDExMCAyNDUgMTQwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDcyMjkiIHN0cm9rZS13aWR0aD0iOCIgb3BhY2l0eT0iMC42Ii8+CiAgPHRleHQgeD0iMjAwIiB5PSI0NDUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iNTIiIGZvbnQtZmFtaWx5PSJzZXJpZiI+8J+RqDwvdGV4dD4KICA8cmVjdCB4PSIwIiB5PSI0NzAiIHdpZHRoPSI0MDAiIGhlaWdodD0iNjMiIGZpbGw9InJnYmEoMCwwLDAsMC41KSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDk1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJyZ2JhKDI1NSwyNTUsMjU1LDAuNSkiIGZvbnQtc2l6ZT0iMTMiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5Ib21tZSBqZXVuZTwvdGV4dD4KICA8dGV4dCB4PSIyMDAiIHk9IjUxOCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZmlsbD0iIzAwNzIyOSIgZm9udC1zaXplPSIxNiIgZm9udC13ZWlnaHQ9ImJvbGQiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5Bam91dGUgdW5lIHBob3RvIOKGkjwvdGV4dD4KPC9zdmc+"}, {"id": "dz45", "country": "dz", "cat": "portrait", "label": "Femme rayonnante", "clue": "Ce sourire rayonnant est typique des femmes du nord de l'Algérie.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmczIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3czIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwNzIyOSIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMykiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MykiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTUyIiByeD0iNjIiIHJ5PSI3MiIgZmlsbD0iIzFhMGEwYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01OCA1MzMgUTY4IDMwNSAyMDAgMjkwIFEzMzIgMzA1IDM0MiA1MzNaIiBmaWxsPSIjMWEwYTBhIi8+CiAgICAgICAgPGNpcmNsZSBjeD0iMjAwIiBjeT0iODAiIHI9IjM1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDcyMjkiIHN0cm9rZS13aWR0aD0iNCIgb3BhY2l0eT0iMC40Ii8+CiAgPHRleHQgeD0iMjAwIiB5PSI0NDUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iNTIiIGZvbnQtZmFtaWx5PSJzZXJpZiI+8J+YijwvdGV4dD4KICA8cmVjdCB4PSIwIiB5PSI0NzAiIHdpZHRoPSI0MDAiIGhlaWdodD0iNjMiIGZpbGw9InJnYmEoMCwwLDAsMC41KSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDk1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJyZ2JhKDI1NSwyNTUsMjU1LDAuNSkiIGZvbnQtc2l6ZT0iMTMiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5GZW1tZSByYXlvbm5hbnRlPC90ZXh0PgogIDx0ZXh0IHg9IjIwMCIgeT0iNTE4IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSIjMDA3MjI5IiBmb250LXNpemU9IjE2IiBmb250LXdlaWdodD0iYm9sZCIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkFqb3V0ZSB1bmUgcGhvdG8g4oaSPC90ZXh0Pgo8L3N2Zz4="}, {"id": "dz46", "country": "dz", "cat": "portrait", "label": "Homme classique", "clue": "La moustache fine est une signature des hommes algériens.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcwIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cwIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwNzIyOSIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMCkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MCkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ1IiByeD0iNTgiIHJ5PSI2NSIgZmlsbD0iIzBhMGExYSIvPgogICAgICAgIDxwYXRoIGQ9Ik0xNDIgMTQ1IFExNDIgMTEwIDIwMCAxMDUgUTI1OCAxMTAgMjU4IDE0NSBRMjcwIDEzMCAyNzAgMTgwIFEyNzAgMjEwIDIwMCAyMTUgUTEzMCAyMTAgMTMwIDE4MCBRMTMwIDE1MCAxNDIgMTQ1WiIgZmlsbD0iIzAwNzIyOSIgb3BhY2l0eT0iMC43Ii8+CiAgICAgICAgPHBhdGggZD0iTTYwIDUzMyBRNzAgMzEwIDIwMCAyOTUgUTMzMCAzMTAgMzQwIDUzM1oiIGZpbGw9IiMwYTBhMWEiLz4KICA8dGV4dCB4PSIyMDAiIHk9IjQ0NSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSI1MiIgZm9udC1mYW1pbHk9InNlcmlmIj7wn5GoPC90ZXh0PgogIDxyZWN0IHg9IjAiIHk9IjQ3MCIgd2lkdGg9IjQwMCIgaGVpZ2h0PSI2MyIgZmlsbD0icmdiYSgwLDAsMCwwLjUpIi8+CiAgPHRleHQgeD0iMjAwIiB5PSI0OTUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9InJnYmEoMjU1LDI1NSwyNTUsMC41KSIgZm9udC1zaXplPSIxMyIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkhvbW1lIGNsYXNzaXF1ZTwvdGV4dD4KICA8dGV4dCB4PSIyMDAiIHk9IjUxOCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZmlsbD0iIzAwNzIyOSIgZm9udC1zaXplPSIxNiIgZm9udC13ZWlnaHQ9ImJvbGQiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5Bam91dGUgdW5lIHBob3RvIOKGkjwvdGV4dD4KPC9zdmc+"}, {"id": "dz47", "country": "dz", "cat": "portrait", "label": "Femme de Tlemcen", "clue": "Tlemcen est connue pour l'élégance de ses femmes.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcxIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cxIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwNzIyOSIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMSkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MSkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTUwIiByeD0iNjAiIHJ5PSI3MCIgZmlsbD0iIzFhMWEwYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01NSA1MzMgUTY1IDMwMCAyMDAgMjg1IFEzMzUgMzAwIDM0NSA1MzNaIiBmaWxsPSIjMWExYTBhIi8+CiAgICAgICAgPHJlY3QgeD0iMTcwIiB5PSIyMTUiIHdpZHRoPSI2MCIgaGVpZ2h0PSIxNSIgcng9IjciIGZpbGw9IiMwMDcyMjkiIG9wYWNpdHk9IjAuNSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDQ1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjUyIiBmb250LWZhbWlseT0ic2VyaWYiPvCfkak8L3RleHQ+CiAgPHJlY3QgeD0iMCIgeT0iNDcwIiB3aWR0aD0iNDAwIiBoZWlnaHQ9IjYzIiBmaWxsPSJyZ2JhKDAsMCwwLDAuNSkiLz4KICA8dGV4dCB4PSIyMDAiIHk9IjQ5NSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZmlsbD0icmdiYSgyNTUsMjU1LDI1NSwwLjUpIiBmb250LXNpemU9IjEzIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+RmVtbWUgZGUgVGxlbWNlbjwvdGV4dD4KICA8dGV4dCB4PSIyMDAiIHk9IjUxOCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZmlsbD0iIzAwNzIyOSIgZm9udC1zaXplPSIxNiIgZm9udC13ZWlnaHQ9ImJvbGQiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5Bam91dGUgdW5lIHBob3RvIOKGkjwvdGV4dD4KPC9zdmc+"}, {"id": "dz48", "country": "dz", "cat": "portrait", "label": "Homme mature", "clue": "Ce regard expérimenté rappelle les hommes du constantinois.", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcyIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cyIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwNzIyOSIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMikiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MikiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ4IiByeD0iNTUiIHJ5PSI2OCIgZmlsbD0iIzBhMWEwYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01MCA1MzMgUTYwIDI5NSAyMDAgMjgwIFEzNDAgMjk1IDM1MCA1MzNaIiBmaWxsPSIjMGExYTBhIi8+CiAgICAgICAgPHBhdGggZD0iTTE1NSAxNDAgUTE3MCAxMTAgMjAwIDEwNSBRMjMwIDExMCAyNDUgMTQwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDcyMjkiIHN0cm9rZS13aWR0aD0iOCIgb3BhY2l0eT0iMC42Ii8+CiAgPHRleHQgeD0iMjAwIiB5PSI0NDUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iNTIiIGZvbnQtZmFtaWx5PSJzZXJpZiI+8J+RtDwvdGV4dD4KICA8cmVjdCB4PSIwIiB5PSI0NzAiIHdpZHRoPSI0MDAiIGhlaWdodD0iNjMiIGZpbGw9InJnYmEoMCwwLDAsMC41KSIvPgogIDx0ZXh0IHg9IjIwMCIgeT0iNDk1IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmaWxsPSJyZ2JhKDI1NSwyNTUsMjU1LDAuNSkiIGZvbnQtc2l6ZT0iMTMiIGZvbnQtZmFtaWx5PSJzYW5zLXNlcmlmIj5Ib21tZSBtYXR1cmU8L3RleHQ+CiAgPHRleHQgeD0iMjAwIiB5PSI1MTgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9IiMwMDcyMjkiIGZvbnQtc2l6ZT0iMTYiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+QWpvdXRlIHVuZSBwaG90byDihpI8L3RleHQ+Cjwvc3ZnPg=="}, {"id": "dz49", "country": "dz", "cat": "comic", "label": "Famille algérienne", "clue": "La famille nombreuse réunie — image classique d'un dimanche algérien 👨‍👩‍👧", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmczIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3czIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwNzIyOSIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMykiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MykiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTUyIiByeD0iNjIiIHJ5PSI3MiIgZmlsbD0iIzBhMmEwYSIvPgogICAgICAgIDxwYXRoIGQ9Ik01OCA1MzMgUTY4IDMwNSAyMDAgMjkwIFEzMzIgMzA1IDM0MiA1MzNaIiBmaWxsPSIjMGEyYTBhIi8+CiAgICAgICAgPGNpcmNsZSBjeD0iMjAwIiBjeT0iODAiIHI9IjM1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDcyMjkiIHN0cm9rZS13aWR0aD0iNCIgb3BhY2l0eT0iMC40Ii8+CiAgPHRleHQgeD0iMjAwIiB5PSI0NDUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iNTIiIGZvbnQtZmFtaWx5PSJzZXJpZiI+8J+RqOKAjfCfkanigI3wn5GnPC90ZXh0PgogIDxyZWN0IHg9IjAiIHk9IjQ3MCIgd2lkdGg9IjQwMCIgaGVpZ2h0PSI2MyIgZmlsbD0icmdiYSgwLDAsMCwwLjUpIi8+CiAgPHRleHQgeD0iMjAwIiB5PSI0OTUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9InJnYmEoMjU1LDI1NSwyNTUsMC41KSIgZm9udC1zaXplPSIxMyIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkZhbWlsbGUgYWxnw6lyaWVubmU8L3RleHQ+CiAgPHRleHQgeD0iMjAwIiB5PSI1MTgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9IiMwMDcyMjkiIGZvbnQtc2l6ZT0iMTYiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+QWpvdXRlIHVuZSBwaG90byDihpI8L3RleHQ+Cjwvc3ZnPg=="}, {"id": "dz50", "country": "dz", "cat": "comic", "label": "Hammam algérien", "clue": "Le hammam est une institution en Algérie aussi ! 🧖", "photo": "data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgNDAwIDUzMyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZGVmcz4KICAgIDxsaW5lYXJHcmFkaWVudCBpZD0iYmcwIiB4MT0iMCUiIHkxPSIwJSIgeDI9IjEwMCUiIHkyPSIxMDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjUwJSIgc3RvcC1jb2xvcj0iIzBkMWIwZCIvPgogICAgICA8c3RvcCBvZmZzZXQ9IjEwMCUiIHN0b3AtY29sb3I9IiMwYTBhMGEiLz4KICAgIDwvbGluZWFyR3JhZGllbnQ+CiAgICA8cmFkaWFsR3JhZGllbnQgaWQ9Imdsb3cwIiBjeD0iNTAlIiBjeT0iNDAlIj4KICAgICAgPHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzAwNzIyOSIgc3RvcC1vcGFjaXR5PSIwLjE1Ii8+CiAgICAgIDxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0idHJhbnNwYXJlbnQiLz4KICAgIDwvcmFkaWFsR3JhZGllbnQ+CiAgPC9kZWZzPgogIDxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNTMzIiBmaWxsPSJ1cmwoI2JnMCkiLz4KICA8cmVjdCB3aWR0aD0iNDAwIiBoZWlnaHQ9IjUzMyIgZmlsbD0idXJsKCNnbG93MCkiLz4KICA8ZWxsaXBzZSBjeD0iMjAwIiBjeT0iMTQ1IiByeD0iNTgiIHJ5PSI2NSIgZmlsbD0iIzFhMGExYSIvPgogICAgICAgIDxwYXRoIGQ9Ik0xNDIgMTQ1IFExNDIgMTEwIDIwMCAxMDUgUTI1OCAxMTAgMjU4IDE0NSBRMjcwIDEzMCAyNzAgMTgwIFEyNzAgMjEwIDIwMCAyMTUgUTEzMCAyMTAgMTMwIDE4MCBRMTMwIDE1MCAxNDIgMTQ1WiIgZmlsbD0iIzAwNzIyOSIgb3BhY2l0eT0iMC43Ii8+CiAgICAgICAgPHBhdGggZD0iTTYwIDUzMyBRNzAgMzEwIDIwMCAyOTUgUTMzMCAzMTAgMzQwIDUzM1oiIGZpbGw9IiMxYTBhMWEiLz4KICA8dGV4dCB4PSIyMDAiIHk9IjQ0NSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSI1MiIgZm9udC1mYW1pbHk9InNlcmlmIj7wn6eWPC90ZXh0PgogIDxyZWN0IHg9IjAiIHk9IjQ3MCIgd2lkdGg9IjQwMCIgaGVpZ2h0PSI2MyIgZmlsbD0icmdiYSgwLDAsMCwwLjUpIi8+CiAgPHRleHQgeD0iMjAwIiB5PSI0OTUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9InJnYmEoMjU1LDI1NSwyNTUsMC41KSIgZm9udC1zaXplPSIxMyIgZm9udC1mYW1pbHk9InNhbnMtc2VyaWYiPkhhbW1hbSBhbGfDqXJpZW48L3RleHQ+CiAgPHRleHQgeD0iMjAwIiB5PSI1MTgiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZpbGw9IiMwMDcyMjkiIGZvbnQtc2l6ZT0iMTYiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiI+QWpvdXRlIHVuZSBwaG90byDihpI8L3RleHQ+Cjwvc3ZnPg=="}];

function loadImages(){try{const r=localStorage.getItem(STORAGE_KEY);if(r)return JSON.parse(r);}catch(e){}saveImages(DEFAULT_IMAGES);return[...DEFAULT_IMAGES]}
function saveImages(imgs){localStorage.setItem(STORAGE_KEY,JSON.stringify(imgs))}
let IMAGES=loadImages();

// ── GAME ──
let deck,round,score,streak,maxStreak,answered,hintUsed,roundHistory;
let soundOn=true,vibrateOn=true,hardMode=false;
const $=id=>document.getElementById(id);
function shuffle(a){const b=[...a];for(let i=b.length-1;i>0;i--){const j=Math.floor(Math.random()*(i+1));[b[i],b[j]]=[b[j],b[i]]}return b}
function playSound(t){if(!soundOn)return;try{const ctx=new(window.AudioContext||window.webkitAudioContext)();const o=ctx.createOscillator(),g=ctx.createGain();o.connect(g);g.connect(ctx.destination);if(t==='correct'){o.frequency.setValueAtTime(660,ctx.currentTime);o.frequency.setValueAtTime(880,ctx.currentTime+.1)}else{o.frequency.setValueAtTime(300,ctx.currentTime);o.frequency.setValueAtTime(200,ctx.currentTime+.1)}g.gain.value=.12;o.start();g.gain.exponentialRampToValueAtTime(.0001,ctx.currentTime+.35);o.stop(ctx.currentTime+.35)}catch(e){}}
function vibrate(p){if(vibrateOn&&navigator.vibrate)navigator.vibrate(p)}
function toast(msg,type){const t=$('toast');t.textContent=msg;t.className='show '+(type||'success');setTimeout(()=>{t.className=''},2500)}
function isPlaceholder(photo){return photo&&photo.startsWith('data:image/svg')}

function updateSplashStats(){
  const ma=IMAGES.filter(i=>i.country==='ma').length;
  const dz=IMAGES.filter(i=>i.country==='dz').length;
  $('splash-total').textContent=IMAGES.length;
  $('splash-ma').textContent=ma;
  $('splash-dz').textContent=dz;
}

function initGame(){
  const pool=IMAGES.filter(i=>i.photo&&i.country);
  if(pool.length<2){toast('Pas assez d\'images !','error');return}
  const ma=shuffle(pool.filter(i=>i.country==='ma'));
  const dz=shuffle(pool.filter(i=>i.country==='dz'));
  const half=Math.floor(ROUNDS/2);
  deck=shuffle([...ma.slice(0,Math.min(half,ma.length)),...dz.slice(0,Math.min(ROUNDS-Math.min(half,ma.length),dz.length))]).slice(0,ROUNDS);
  round=0;score=0;streak=0;maxStreak=0;roundHistory=[];
  $('score-val').textContent='0';
  $('result-screen').style.display='none';
  $('game-area').style.display='flex';
  $('header').style.display='flex';
  $('progress-wrap').style.display='block';
  $('streak-row').style.display='flex';
  loadRound();
}

function loadRound(){
  answered=false;hintUsed=false;
  const p=deck[round];
  $('round-pill').innerHTML=(round+1)+'<span style="color:rgba(240,236,228,0.3)">/'+deck.length+'</span>';
  $('progress-bar').style.width=(round/deck.length*100)+'%';
  const img=$('person-photo');
  img.style.opacity='0';img.src='';
  setTimeout(()=>{img.src=p.photo;img.onload=()=>{img.style.opacity='1'}},50);
  $('photo-overlay').className='';
  $('photo-overlay').style.opacity='0';
  $('photo-tag').style.display='none';
  $('photo-type-badge').textContent=(CAT_ICONS[p.cat]||'📸')+' '+(CAT_LABELS[p.cat]||'');
  ['btn-ma','btn-dz'].forEach(id=>{const b=$(id);b.className='flag-btn';b.disabled=false});
  $('clue-box').style.display='none';
  $('next-btn').style.display='none';
  $('hint-btn').disabled=hardMode;
  const sb=$('streak-badge');
  if(streak>=2){sb.style.display='flex';$('streak-val').textContent=streak}else sb.style.display='none';
}

function answer(choice){
  if(answered)return;answered=true;
  const p=deck[round];const correct=choice===p.country;const pts=hintUsed?5:10;
  roundHistory.push({person:p,userChoice:choice,correct});
  if(correct){
    score+=pts;streak++;if(streak>maxStreak)maxStreak=streak;
    $(choice==='ma'?'btn-ma':'btn-dz').className='flag-btn correct';
    $('photo-overlay').className='correct';$('overlay-icon').textContent='✓';
    $('overlay-main').textContent=streak>=3?'🔥 Enchaînement !':'Bravo !';
    $('overlay-sub').textContent=p.label+' — +'+pts+' pts';
    $('photo-card').classList.add('flash-correct');setTimeout(()=>$('photo-card').classList.remove('flash-correct'),400);
    playSound('correct');vibrate([40]);
  }else{
    score=Math.max(0,score-2);streak=0;
    $(choice==='ma'?'btn-ma':'btn-dz').className='flag-btn wrong';
    $(choice==='ma'?'btn-dz':'btn-ma').className='flag-btn reveal';
    $('photo-overlay').className='wrong';$('overlay-icon').textContent='✗';
    $('overlay-main').textContent='Raté !';
    $('overlay-sub').textContent='C\'était : '+p.label;
    $('photo-card').classList.add('shake');setTimeout(()=>$('photo-card').classList.remove('shake'),350);
    playSound('wrong');vibrate([80,40,80]);
  }
  $('photo-tag').textContent=p.country==='ma'?'🇲🇦 Maroc':'🇩🇿 Algérie';
  $('photo-tag').style.display='block';
  $('score-val').textContent=score;
  if(streak>=2){$('streak-badge').style.display='flex';$('streak-val').textContent=streak}else $('streak-badge').style.display='none';
  if(p.clue){$('clue-box').style.display='flex';$('clue-text').textContent=p.clue}
  ['btn-ma','btn-dz'].forEach(id=>$(id).disabled=true);
  $('hint-btn').disabled=true;
  $('next-btn').style.display='block';
  $('next-btn').textContent=(round+1<deck.length)?'Suivant →':'Voir les résultats 🏆';
}

function nextRound(){round++;if(round>=deck.length)showResults();else loadRound()}

function showResults(){
  $('game-area').style.display='none';$('streak-badge').style.display='none';
  $('progress-bar').style.width='100%';$('result-screen').style.display='flex';
  const pct=Math.round(score/(deck.length*10)*100);
  let emoji,title,sub;
  if(pct>=90){emoji='🏆';title='Légende du Maghreb !';sub='Tu es un vrai expert. Impressionnant !'}
  else if(pct>=70){emoji='🌟';title='Très bon résultat !';sub='Tu t\'en sors vraiment bien !'}
  else if(pct>=50){emoji='👍';title='Pas mal !';sub='Encore un peu d\'entraînement !'}
  else if(pct>=30){emoji='😅';title='Il faut s\'entraîner !';sub='Le Maghreb a encore des secrets pour toi.'}
  else{emoji='😂';title='Tu confonds tout !';sub='Tes amis maghrébins seraient choqués 😂'}
  $('result-big').textContent=emoji;$('result-title').textContent=title;$('result-sub').textContent=sub;
  $('r-score').textContent=score;$('r-pct').textContent=pct+'%';$('r-streak').textContent=maxStreak;
  const bd=$('result-breakdown');bd.innerHTML='';
  roundHistory.forEach(({person,correct})=>{
    const d=document.createElement('div');d.className='breakdown-item';
    d.innerHTML=`<span class="breakdown-flag">${person.country==='ma'?'🇲🇦':'🇩🇿'}</span><span class="breakdown-name">${person.label}</span><span style="font-size:10px;color:var(--muted)">${isPlaceholder(person.photo)?'🎨':'📸'}</span><span class="breakdown-result">${correct?'✅':'❌'}</span>`;
    bd.appendChild(d);
  });
}

// ── ADMIN ──
let adminLoggedIn=false,currentFilter='all';

function openAdmin(){$('admin-panel').classList.add('open');if(!adminLoggedIn){$('admin-login').style.display='flex';$('admin-content').style.display='none'}}
function closeAdmin(){$('admin-panel').classList.remove('open')}

function loginAdmin(){
  if($('pw-input').value===ADMIN_PASSWORD){
    adminLoggedIn=true;$('admin-login').style.display='none';$('admin-content').style.display='flex';
    switchTab('add');renderStats();updateTabCount();
  }else{$('pw-error').style.display='block';$('pw-input').value='';setTimeout(()=>$('pw-error').style.display='none',2000)}
}

function updateTabCount(){$('tab-count').textContent=IMAGES.length}

function switchTab(tab){
  document.querySelectorAll('.admin-tab').forEach(t=>t.classList.remove('active'));
  document.querySelector(`.admin-tab[data-tab="${tab}"]`).classList.add('active');
  $('tab-add').style.display=(tab==='add')?'flex':'none';
  $('tab-manage').style.display=(tab==='manage')?'flex':'none';
  $('tab-stats').style.display=(tab==='stats')?'flex':'none';
  if(tab==='manage')renderAdminGrid();
  if(tab==='stats')renderStats();
}

function renderAdminGrid(){
  const search=$('admin-search').value.toLowerCase();
  const grid=$('admin-grid');grid.innerHTML='';
  let imgs=[...IMAGES];
  if(currentFilter==='ma')imgs=imgs.filter(i=>i.country==='ma');
  else if(currentFilter==='dz')imgs=imgs.filter(i=>i.country==='dz');
  else if(currentFilter==='real')imgs=imgs.filter(i=>!isPlaceholder(i.photo));
  else if(currentFilter==='placeholder')imgs=imgs.filter(i=>isPlaceholder(i.photo));
  if(search)imgs=imgs.filter(i=>(i.label||'').toLowerCase().includes(search));
  $('admin-count').textContent=imgs.length+' image'+(imgs.length>1?'s':'');
  if(!imgs.length){grid.innerHTML='<div style="text-align:center;padding:40px;color:var(--muted);grid-column:1/-1">Aucune image trouvée</div>';return}
  imgs.forEach(img=>{
    const hasReal=!isPlaceholder(img.photo);
    const c=document.createElement('div');
    c.className='admin-card '+(hasReal?'has-photo':'no-photo');
    c.innerHTML=`<img class="admin-card-img" src="${img.photo.substring(0,200)+'...'}" data-src="${img.photo}" alt="${img.label||''}" loading="lazy"/>
      <button class="admin-card-del" data-id="${img.id}" title="Supprimer">🗑️</button>
      <div class="admin-card-info">
        <div class="admin-card-name">${img.label||'Sans titre'}</div>
        <div class="admin-card-meta">${img.country==='ma'?'🇲🇦':'🇩🇿'} ${CAT_ICONS[img.cat]||''} <span style="font-size:10px">${hasReal?'📸 Photo':'🎨 Silhouette'}</span></div>
      </div>`;
    // Fix image src
    const imgEl=c.querySelector('.admin-card-img');
    imgEl.src=img.photo;
    grid.appendChild(c);
    c.querySelector('.admin-card-del').addEventListener('click',()=>{
      if(confirm('Supprimer cette image ?')){
        IMAGES=IMAGES.filter(i=>i.id!==img.id);saveImages(IMAGES);
        renderAdminGrid();renderStats();updateSplashStats();updateTabCount();
        toast('Image supprimée');
      }
    });
  });
}

function renderStats(){
  const ma=IMAGES.filter(i=>i.country==='ma').length;
  const dz=IMAGES.filter(i=>i.country==='dz').length;
  const real=IMAGES.filter(i=>!isPlaceholder(i.photo)).length;
  const ph=IMAGES.filter(i=>isPlaceholder(i.photo)).length;
  $('stats-grid').innerHTML=`
    <div class="stats-card"><div class="stats-card-val">${IMAGES.length}</div><div class="stats-card-lbl">Total</div></div>
    <div class="stats-card"><div class="stats-card-val" style="color:var(--ma)">${ma}</div><div class="stats-card-lbl">🇲🇦 Maroc</div></div>
    <div class="stats-card"><div class="stats-card-val" style="color:var(--dz)">${dz}</div><div class="stats-card-lbl">🇩🇿 Algérie</div></div>
    <div class="stats-card"><div class="stats-card-val">${real}</div><div class="stats-card-lbl">📸 Vraies photos</div></div>
    <div class="stats-card"><div class="stats-card-val">${ph}</div><div class="stats-card-lbl">🎨 Silhouettes</div></div>
    <div class="stats-card"><div class="stats-card-val">${Math.max(0,250-IMAGES.length)}</div><div class="stats-card-lbl">📥 Slots libres</div></div>`;
}

function setPreview(src){$('img-preview').src=src}

function addImage(){
  const photo=$('img-url').value.trim()||$('img-preview').getAttribute('data-real-src')||'';
  const country=$('img-country').value;
  const cat=$('img-cat').value;
  const label=$('img-label').value.trim();
  const clue=$('img-clue').value.trim();
  const prevSrc=$('img-preview').src;
  const realPhoto=prevSrc.startsWith('data:image/')&&!prevSrc.includes('svg+xml,<svg')?prevSrc:(photo||'');
  if(!realPhoto){toast('Ajoute une image d\'abord !','error');return}
  if(!label){toast('Ajoute un label','error');return}
  const id=(country+Date.now()).replace(/[^a-z0-9]/g,'');
  IMAGES.push({id,country,cat,label,clue,photo:realPhoto});
  saveImages(IMAGES);toast('✅ Photo ajoutée !');
  clearForm();renderStats();updateSplashStats();updateTabCount();
}

function clearForm(){
  $('img-url').value='';$('img-label').value='';$('img-clue').value='';
  $('img-preview').src="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 120 160'><rect width='120' height='160' fill='%23242424'/><text x='60' y='88' text-anchor='middle' font-size='32'>🖼️</text></svg>";
}

// File upload
$('img-file').addEventListener('change',function(){
  const file=this.files[0];if(!file)return;
  if(file.size>3*1024*1024){toast('Image trop lourde (max 3MB)','error');return}
  const reader=new FileReader();
  reader.onload=e=>{setPreview(e.target.result);toast('Image chargée ✓')};
  reader.readAsDataURL(file);
});

// Drag & drop
const uz=$('upload-zone');
uz.addEventListener('dragover',e=>{e.preventDefault();uz.style.borderColor='rgba(255,255,255,.4)'});
uz.addEventListener('dragleave',()=>{uz.style.borderColor=''});
uz.addEventListener('drop',e=>{
  e.preventDefault();uz.style.borderColor='';
  const file=e.dataTransfer.files[0];if(!file||!file.type.startsWith('image/'))return;
  const reader=new FileReader();
  reader.onload=ev=>{setPreview(ev.target.result);toast('Image glissée ✓')};
  reader.readAsDataURL(file);
});

// Events
$('start-btn').addEventListener('click',()=>{$('splash').style.display='none';$('header').style.display='flex';$('progress-wrap').style.display='block';$('streak-row').style.display='flex';initGame()});
$('btn-ma').addEventListener('click',()=>answer('ma'));
$('btn-dz').addEventListener('click',()=>answer('dz'));
$('next-btn').addEventListener('click',nextRound);
$('hint-btn').addEventListener('click',()=>{if(answered||hardMode)return;hintUsed=true;const p=deck[round];$('clue-box').style.display='flex';$('clue-text').textContent=(p.clue||'Pas d\'indice.')+' (−5 pts si correct)';$('hint-btn').disabled=true});
$('replay-btn').addEventListener('click',()=>{$('result-screen').style.display='none';$('header').style.display='flex';initGame()});
$('settings-btn').addEventListener('click',()=>$('settings-panel').classList.add('open'));
$('close-settings').addEventListener('click',()=>$('settings-panel').classList.remove('open'));
$('settings-panel').addEventListener('click',e=>{if(e.target===$('settings-panel'))$('settings-panel').classList.remove('open')});
$('open-admin-btn').addEventListener('click',()=>{$('settings-panel').classList.remove('open');openAdmin()});
['toggle-sound','toggle-vibrate','toggle-hard'].forEach(id=>{$(id).addEventListener('click',()=>{$(id).classList.toggle('on');if(id==='toggle-sound')soundOn=$(id).classList.contains('on');if(id==='toggle-vibrate')vibrateOn=$(id).classList.contains('on');if(id==='toggle-hard')hardMode=$(id).classList.contains('on')})});
$('admin-close').addEventListener('click',closeAdmin);
$('pw-btn').addEventListener('click',loginAdmin);
$('pw-input').addEventListener('keyup',e=>{if(e.key==='Enter')loginAdmin()});
document.querySelectorAll('.admin-tab').forEach(t=>t.addEventListener('click',()=>switchTab(t.dataset.tab)));
$('add-btn').addEventListener('click',addImage);
$('clear-form-btn').addEventListener('click',clearForm);
$('preview-url-btn').addEventListener('click',()=>{const u=$('img-url').value.trim();if(u)setPreview(u)});
$('img-url').addEventListener('keyup',e=>{if(e.key==='Enter'){const u=$('img-url').value.trim();if(u)setPreview(u)}});
document.querySelectorAll('.filter-btn').forEach(btn=>btn.addEventListener('click',()=>{document.querySelectorAll('.filter-btn').forEach(b=>b.classList.remove('active'));btn.classList.add('active');currentFilter=btn.dataset.filter;renderAdminGrid()}));
$('admin-search').addEventListener('input',renderAdminGrid);
$('export-btn').addEventListener('click',()=>{
  const real=IMAGES.filter(i=>!isPlaceholder(i.photo));
  const blob=new Blob([JSON.stringify(real,null,2)],{type:'application/json'});
  const a=document.createElement('a');a.href=URL.createObjectURL(blob);a.download='marogien_photos.json';a.click();
  toast('Export téléchargé ('+real.length+' vraies photos) ✓');
});
$('import-trigger').addEventListener('click',()=>$('import-file').click());
$('import-file').addEventListener('change',function(){
  const file=this.files[0];if(!file)return;
  const reader=new FileReader();
  reader.onload=e=>{
    try{const d=JSON.parse(e.target.result);if(!Array.isArray(d))throw 0;
    const existing=new Set(IMAGES.map(i=>i.id));
    const news=d.filter(x=>!existing.has(x.id));
    IMAGES=[...IMAGES,...news];saveImages(IMAGES);renderAdminGrid();renderStats();updateSplashStats();updateTabCount();
    toast(news.length+' photos importées ✓');}
    catch{toast('JSON invalide','error')}
  };reader.readAsText(file);
});
$('reset-default-btn').addEventListener('click',()=>{if(confirm('Réinitialiser avec les 50 silhouettes par défaut ?')){IMAGES=[...DEFAULT_IMAGES];saveImages(IMAGES);renderAdminGrid();renderStats();updateSplashStats();updateTabCount();toast('Base réinitialisée')}});
$('clear-all-btn').addEventListener('click',()=>{if(confirm('Vider toute la base ?')){IMAGES=[];saveImages(IMAGES);renderAdminGrid();renderStats();updateSplashStats();updateTabCount();toast('Base vidée','error')}});

// Init
$('header').style.display='none';
$('progress-wrap').style.display='none';
$('streak-row').style.display='none';
updateSplashStats();
</script>
</body>
</html>

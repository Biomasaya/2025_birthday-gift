<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Ultimate Birthday Celebration for ERINA!</title>
<style>
  :root{
    --bg:#0a0b10; --ink:#ffe5f3; --accent:#ff6fb1; --secondary:#4169e1;
    --gold:#ffa500; --cake:#ffd1dc; --letters:#ffd86a;

    /* ===== 可変プロパティ（デフォルト＝現在の見た目） ===== */
    /* Cake タイトル/進捗 */
    --cake-title-size: 28px;        /* 「Special Cake…」の大きさ */
    --cake-title-top: 16px;         /* その高さ（上から） */
    --cake-progress-size: 18px;     /* 「Drawing…/Perfect!…」の大きさ */
    --cake-progress-bottom: 16px;   /* その高さ（下から） */

    /* クレジット */
    --credit-size: 12px;            /* 「Made by まさや」の大きさ */
    --credit-bottom: 10px;          /* 高さ（下から） */
    --credit-left: 12px;            /* 左から */

    /* ボタン */
    --controls-bottom: 20px;        /* ボタン列の高さ（下から） */
    --btn-fire-scale: 1;            /* 花火ボタンの大きさ */
    --btn-fire-shift: 0px;          /* 花火ボタンの上下移動量(+下/-上) */
    --btn-gift-scale: 1;            /* プレゼントボタンの大きさ */
    --btn-gift-shift: 0px;          /* プレゼントボタンの上下移動量 */

    /* カウントダウン */
    --count-scale: 1;               /* 盤面（丸ごと）のスケール */
    --count-ring: 6px;              /* 外周リングの太さ */
    --count-crosshair: 2px;         /* 十字線の太さ */
    --count-num-scale: 1;           /* 3,2,1 数字だけのスケール */

    /* 風船文字（HAPPY…ERINA!） */
    --letters-scale: 1;             /* 文字の大きさ（例: .8=80%） */
    --letters-shift: 0px;           /* 全体の上下移動量 */

    /* 見出し（I hope you …） */
    --headline-scale: 1;            /* 大きさ（20–40pxに乗算） */
    --headline-shift: 0px;          /* 上下移動量 */

    /* プレゼント画像の上下オフセット（縦画面で1.3倍上げたい等に） */
    --gift-offset-y: 0%;            /* マイナスで上へ */
  }

  *{ box-sizing:border-box; margin:0; padding:0; }
  html,body{ height:100%; background:#000; }
  body{
    color:var(--ink);
    font-family:ui-sans-serif,system-ui,-apple-system,"Segoe UI",Roboto,"Noto Sans JP",sans-serif;
    -webkit-font-smoothing:antialiased; -moz-osx-font-smoothing:grayscale;
    overflow:hidden;
  }

  /* ====== すべてを収めるステージ ====== */
  .stage{
    position:fixed; left:50%; top:50%; transform:translate(-50%,-50%);
    width:min(92vw, 900px);
    aspect-ratio:16/9;
    background:var(--bg);
    border-radius:18px;
    overflow:hidden;
    box-shadow:0 20px 80px rgba(0,0,0,.55);
  }

  /* ベースレイヤー配置 */
  #matrix,.hearts,.container,.ground,.headline,.img-wrap,
  .credit,.start-overlay,.countdown,.cake-overlay{
    position:absolute; inset:0;
  }

  #matrix{ display:none; z-index:1; }
  .container{ z-index:3; display:flex; align-items:center; justify-content:center; transform: translateY(var(--letters-shift)); }
  .hearts{ pointer-events:none; opacity:0; transition:opacity .6s ease; z-index:2; }
  .hearts.show{ opacity:1; }
  .ground{ bottom:0; height:4px; background:linear-gradient(to right,var(--accent),var(--secondary),var(--gold)); z-index:2; }

  .headline{
    display:grid; place-items:center; z-index:4; opacity:0; transition:opacity .8s ease;
    text-align:center; padding:0 5vw; font-weight:800; letter-spacing:.02em;
    font-size: calc(var(--headline-scale) * clamp(20px,5vw,40px));
    color:var(--ink); text-shadow:0 0 18px rgba(255,255,255,.08);
    transform: translateY(var(--headline-shift));
  }
  .headline.show{ opacity:1; }

  /* 画像オーバーレイ */
  .img-wrap{ display:grid; place-items:center; opacity:0; transition:opacity .8s ease; z-index:5;
             background:rgba(10,11,16,.8); backdrop-filter:blur(5px); }
  .img-wrap.show{ opacity:1; }
  .img-wrap img{
    max-width: 88%;
    max-height: 80%;
    width: auto; height: auto; object-fit: contain;
    transform: translateY(var(--gift-offset-y));
  }
  .close-btn{ position:absolute; top:20px; right:20px; background:rgba(255,255,255,.2); border:none; color:#fff;
              width:40px; height:40px; border-radius:50%; cursor:pointer; font-size:20px; display:flex; align-items:center; justify-content:center; }

  /* ボタン列 */
  .controls{
    position:absolute; left:50%; bottom: var(--controls-bottom);
    transform:translateX(-50%);
    display:flex; gap:15px; align-items:center;
    z-index:10; opacity:0; pointer-events:none;
    transition:opacity .4s ease, transform .2s ease;
  }
  .controls.show{ opacity:1; pointer-events:auto; transform:translateX(-50%) translateY(0); }

  .btn{
    display:inline-flex; align-items:center; justify-content:center;
    padding:12px 24px; min-height:auto; border-radius:25px;
    background:linear-gradient(135deg, var(--accent), var(--secondary));
    color:#fff; border:none; cursor:pointer; font-size:16px; font-weight:600;
    transition:transform .2s ease, box-shadow .3s ease;
    box-shadow:0 4px 15px rgba(255,111,177,.3);
    --btn-scale: 1;
    --btn-shift: 0px;
    transform: translateY(var(--btn-shift)) scale(var(--btn-scale));
    white-space: nowrap;      /* 改行しない */
    word-break: keep-all;     /* CJKの勝手な分割を抑制 */
    text-wrap: nowrap;        /* 近年のプロパティ: 念のため */
    flex: 0 0 auto;           /* 親Flexの収縮を防ぐ */
    min-width: max-content;   /* 内容幅に合わせて広がる（iOS Safari OK） */
    min-width:-webkit-max-content; /* ←念のためのフォールバック */
  }
  .btn:hover{ transform: translateY(calc(var(--btn-shift) - 2px)) scale(var(--btn-scale)); }
  .firework-btn{ --btn-scale: var(--btn-fire-scale); --btn-shift: var(--btn-fire-shift); }
  .gift-btn{    --btn-scale: var(--btn-gift-scale); --btn-shift: var(--btn-gift-shift); }

  .credit{
    left: var(--credit-left);
    bottom: var(--credit-bottom);
    font-size: var(--credit-size);
    z-index:10; pointer-events:none;
  }

  .start-overlay{ z-index:6; display:grid; place-items:center;
                  background:radial-gradient(ellipse at center, rgba(0,0,0,.2), rgba(0,0,0,.9)); }
  .start-overlay.hide{ opacity:0; pointer-events:none; transition:opacity .4s ease; }
  .player-card{ width:min(420px,90%); background:rgba(255,255,255,.06); border:1px solid rgba(255,255,255,.12);
                border-radius:18px; padding:24px 20px 28px; text-align:center; backdrop-filter:blur(8px);
                box-shadow:0 20px 80px rgba(0,0,0,.55); }
  .player-title{ font-size:28px; font-weight:800; letter-spacing:.06em; margin-bottom:14px; }
  .play-btn{ width:96px; height:96px; border-radius:50%; border:2px solid rgba(255,255,255,.35); background:rgba(255,255,255,.08);
             cursor:pointer; display:grid; place-items:center; margin:0 auto 10px; transition:transform .15s ease; }
  .play-btn:active{ transform:scale(.98); }
  .triangle{ width:0; height:0; border-left:26px solid #fff; border-top:16px solid transparent; border-bottom:16px solid transparent; margin-left:6px; }
  .hint{ opacity:.7; font-size:14px; }

  /* カウントダウン */
  .countdown{ z-index:7; display:none; place-items:center; background:rgba(0,0,0,.75); }
  .countdown.show{ display:grid; }
  .countwrap{ position:relative; width:min(420px,70%); aspect-ratio:1/1;
              transform: scale(var(--count-scale)); transform-origin: 50% 50%; }
  .ring{ position:absolute; inset:0; border: var(--count-ring) solid rgba(255,255,255,.8); border-radius:50%;
         box-shadow:0 0 40px rgba(255,255,255,.15) inset; }
  .crosshair::before,.crosshair::after{ content:""; position:absolute; left:50%; top:0; bottom:0;
         width: var(--count-crosshair); background:rgba(255,255,255,.5); transform:translateX(-50%); }
  .crosshair::after{ top:50%; left:0; right:0; height: var(--count-crosshair); width:100%; transform:translateY(-50%); }
  .num{ position:absolute; inset:0; display:grid; place-items:center; font-weight:900;
        font-size:clamp(80px,26vw,220px); text-shadow:0 0 16px rgba(0,0,0,.6);
        transform: scale(var(--count-num-scale)); transform-origin:50% 50%; }
  .wedge{ position:absolute; inset:0; border-radius:50%;
          background:conic-gradient(rgba(255,255,255,.12) 0deg, rgba(255,255,255,0) 0deg);
          animation:sweep 1s linear infinite;
          -webkit-mask:radial-gradient(circle, transparent 52%, black 53%);
          mask:radial-gradient(circle, transparent 52%, black 53%); }
  @keyframes sweep{ from{ background:conic-gradient(rgba(255,255,255,.12) 0deg, rgba(255,255,255,0) 0deg);}
                    to{   background:conic-gradient(rgba(255,255,255,.12) 360deg, rgba(255,255,255,0) 360deg);} }

  /* ケーキ描画オーバーレイ */
  .cake-overlay{ z-index:8; display:none; place-items:center; background:rgba(10,11,16,.95); }
  .cake-overlay.show{ display:grid; }
  .cake-canvas{ width:95%; height:95%; border:1px solid #e5e5e5; border-radius:12px; background:#fff; }
  .cake-title{ position:absolute; top: var(--cake-title-top); left:50%; transform:translateX(-50%);
               font-size: var(--cake-title-size); font-weight:800; color:var(--accent);
               text-shadow:0 0 10px rgba(255,111,177,.5); }
  .cake-progress{ position:absolute; bottom: var(--cake-progress-bottom); left:50%; transform:translateX(-50%);
                  text-align:center; color:var(--ink); font-size: var(--cake-progress-size); opacity:0.8; }

  /* balloons / letters */
  .letter{ display:inline-block;
           font-size: calc(var(--letters-scale) * clamp(1.6rem, 6.4vw, 4.8rem)); /* 80%指示にも対応 */
           font-weight:800; letter-spacing:.1em;
           text-shadow:0 0 20px currentColor, 0 4px 8px rgba(0,0,0,.3);
           opacity:0; transform:translateY(-100px) rotate(180deg); position:relative; margin:0 .05em; }
  .balloon{ position:absolute; width:30px; height:40px; border-radius:50% 50% 50% 50% / 60% 60% 40% 40%;
            top:-50px; left:50%; transform:translateX(-50%); opacity:0; z-index:-1; }
  .balloon::after{ content:''; position:absolute; width:2px; height:20px; background:rgba(255,255,255,.3); bottom:-20px; left:50%; transform:translateX(-50%); }
  @keyframes letterDrop{ 0%{opacity:0; transform:translateY(-100px) rotate(180deg);} 70%{transform:translateY(10px) rotate(0);} 100%{opacity:1; transform:translateY(0) rotate(0);} }
  @keyframes letterBounce{ 0%,100%{transform:translateY(0) scale(1);} 50%{transform:translateY(-10px) scale(1.1);} }
  @keyframes balloonAppear{ 0%{opacity:0; transform:translateX(-50%) scale(0);} 100%{opacity:.8; transform:translateX(-50%) scale(1);} }
  @keyframes balloonFloat{ 0%{transform:translateY(0) scale(1); opacity:1;} 100%{transform:translateY(-300px) scale(.8); opacity:0;} }
  @keyframes balloonFloatUp{ 0%{opacity:.8; transform:translateX(-50%) scale(1);} 100%{opacity:0; transform:translateX(-50%) translateY(-400px) scale(1.2);} }

  .firework-trail{ position:absolute; width:4px; height:4px; background:radial-gradient(circle,#fff 0%, #ffa500 50%, transparent 100%); border-radius:50%; box-shadow:0 0 10px #ffa500; z-index:4; }
  @keyframes fireworkLaunch{ 0%{transform:translateY(0);opacity:1;} 100%{transform:translateY(var(--launch-distance));opacity:0;} }
  .smoke{ position:absolute; width:6px; height:6px; background:radial-gradient(circle,rgba(255,255,255,.6) 0%, transparent 70%); border-radius:50%; z-index:2; }
  @keyframes smokeRise{ 0%{opacity:.6; transform:scale(1);} 100%{opacity:0; transform:scale(3) translateY(-50px);} }
  .firework-particle{ position:absolute; width:4px; height:4px; border-radius:50%; z-index:4; }
  @keyframes particleBurst{ 0%{opacity:1; transform:translate(0,0) scale(1);} 20%{opacity:1;} 100%{opacity:0; transform:translate(var(--dx), calc(var(--dy) + 70px)) scale(0);} }

  /* ===== 端末ごとの変数上書き ===== */

  /* iPhone 縦（ポートレート） */
  @media (max-width: 480px) and (orientation: portrait){
    .btn{
      font-size: 12px;
      padding: 8px 14px;
      border-radius: 20px;
      /* スケールは 1 のまま推奨 */
    }

    :root{
      /* カウントダウン一式を 60% */
      --count-scale: .6;
      --count-ring: 3.6px;
      --count-crosshair: 1.2px;
      --count-num-scale: .6;

      /* Cake テキストを 40%相当 */
      --cake-title-size: 13px;
      --cake-progress-size: 7px;

      /* クレジット・ボタン位置/大きさ */
      --credit-size: 5px;
      --controls-bottom: 5%;
      --btn-fire-scale: 1;
      --btn-gift-scale: 1;

      /* 風船文字と見出し */
      --letters-scale: .8; /* 80% */
      --headline-scale: .4;/* 40% */

      /* プレゼント画像を上へ（1.3倍相当への微調整はここで） */
      --gift-offset-y: -30%;
    }
  }

  /* iPhone 横（ランドスケープ=短辺が小さい） */
  @media (max-height: 420px){
    :root{
      --count-scale: .6;
      --count-ring: 3.6px;
      --count-crosshair: 1.2px;
      --count-num-scale: .6;

      --cake-title-size: 19px;      /* 60% */
      --cake-progress-size: 11px;   /* 60% */

      --controls-bottom: 10%;       /* 少し上へ */
      --btn-fire-scale: .9;         /* デフォルト大きさのまま微調整したいときに */
      --btn-gift-scale: .9;

      --letters-scale: .8;          /* 80% */
    }
  }

  /* PC（必要ならここでPC専用値を変更。既定(:root)がPC想定） */
  @media (min-width: 768px){
    :root{
      /* 例: PCで見出しを少し下げたいとき */
      /* --headline-shift: 0px; */
    }
  }
</style>
</head>
<body>

  <!-- ===== ステージ（全UIはこの中に） ===== -->
  <div id="stage" class="stage">

    <!-- 音源 -->
    <audio id="bgm" src="audio/birthday.mp3" preload="auto" loop></audio>
    <audio id="sfxCountdown" src="audio/Countdown.mp3" preload="auto"></audio>
    <audio id="sfxFire" src="audio/fire.mp3" preload="auto"></audio>
    <audio id="sfxWrite" src="audio/write.mp3" preload="auto" loop></audio>

    <!-- キャンバス／レイヤー -->
    <canvas id="matrix"></canvas>
    <canvas id="hearts" class="hearts"></canvas>

    <div class="ground"></div>
    <div class="container" id="container"></div>
    <div id="headline" class="headline">I hope you have another wonderful year!</div>

    <!-- 画像 -->
    <div id="imgWrap" class="img-wrap">
      <button class="close-btn" onclick="hideImage()">×</button>
      <img id="gift" src="earrings.png" alt="gift" />
    </div>

    <!-- ボタン -->
    <div class="controls">
      <button class="btn firework-btn" onclick="launchFireworks()">🎆&nbsp;花火</button>
      <button class="btn gift-btn" onclick="showImage()">🎁&nbsp;プレゼント</button>
    </div>

    <div class="credit">Made by まさや</div>

    <!-- スタート画面 -->
    <div class="start-overlay" id="startOverlay">
      <div class="player-card">
        <div class="player-title">Happy Birthday</div>
        <button id="playButton" class="play-btn" aria-label="再生"><span class="triangle"></span></button>
        <div class="hint">タップして再生</div>
      </div>
    </div>

    <!-- カウントダウン -->
    <div class="countdown" id="countdown">
      <div class="countwrap">
        <div class="ring"></div>
        <div class="wedge"></div>
        <div class="crosshair"></div>
        <div class="num" id="countNum">3</div>
      </div>
    </div>

    <!-- ケーキ描画 -->
    <div class="cake-overlay" id="cakeOverlay">
      <div class="cake-title">Special Cake for ERINA! 🎂</div>
      <canvas id="cakeCanvas" class="cake-canvas" width="900" height="900" aria-label="cake"></canvas>
      <div class="cake-progress" id="cakeProgress">Drawing your special cake...</div>
    </div>

  </div><!-- /stage -->

<script>
/* ===== 共通参照 ===== */
const stage = document.getElementById('stage');
const container = document.getElementById('container');
const matrix = document.getElementById('matrix');
const heartsCanvas = document.getElementById('hearts');
const startOverlay = document.getElementById('startOverlay');
const playButton = document.getElementById('playButton');
const countdown = document.getElementById('countdown');
const countNum = document.getElementById('countNum');
const cakeOverlay = document.getElementById('cakeOverlay');
const cakeCanvas = document.getElementById('cakeCanvas');
const cakeProgress = document.getElementById('cakeProgress');
const headline = document.getElementById('headline');

const bgm = document.getElementById('bgm');
const sfxCountdown = document.getElementById('sfxCountdown');
const sfxFire = document.getElementById('sfxFire');
const sfxWrite = document.getElementById('sfxWrite');

const controls = document.querySelector('.controls');
let isDrawingCake = false;

let letters = [];
const colors = ['#ff69b4','#ff1493','#dc143c','#ff6347','#ffa500','#4169e1','#9370db','#ff1493','#32cd32','#ff69b4','#ffa500','#ffff00','#32cd32','#00ced1','#9370db','#ff69b4','#ffff00','#32cd32','#00ced1'];
const fireworkColors = ['#ff0040','#ff4000','#ff8000','#ffbf00','#ffff00','#bfff00','#80ff00','#40ff00','#00ff00','#00ff40','#00ff80','#00ffbf','#00ffff','#00bfff','#0080ff','#0040ff','#0000ff','#4000ff','#8000ff','#bf00ff','#ff00ff','#ff00bf','#ff0080'];

/* === ステージサイズとDPR === */
function stageSize(){
  const r = stage.getBoundingClientRect();
  return { w: Math.floor(r.width), h: Math.floor(r.height) };
}
function fitCanvasToStage(cnv){
  const { w, h } = stageSize();
  const dpr = Math.max(1, window.devicePixelRatio || 1);
  cnv.width = Math.round(w * dpr);
  cnv.height = Math.round(h * dpr);
  cnv.style.width = w + 'px';
  cnv.style.height = h + 'px';
  const ctx = cnv.getContext('2d');
  ctx.setTransform(dpr, 0, 0, dpr, 0, 0);
  return ctx;
}

/* ====== 再生ボタン → カウントダウン → ケーキ描画 ====== */
playButton.addEventListener('click', async () => {
  startOverlay.classList.add('hide');
  try { sfxCountdown.currentTime = 0; await sfxCountdown.play(); } catch(e){}
  try { bgm.muted = true; await bgm.play(); bgm.pause(); bgm.currentTime = 0; bgm.muted = false; } catch(e){}

  await runCountdown();
  sfxCountdown.pause(); sfxCountdown.currentTime = 0;

  showCakeDrawing();
});

function runCountdown(){
  return new Promise((resolve)=>{
    let n = 3;
    countNum.textContent = n;
    countdown.classList.add('show');
    const tick = () => {
      if (n <= 1) { countdown.classList.remove('show'); resolve(); }
      else { n -= 1; countNum.textContent = n; setTimeout(tick, 1000); }
    };
    setTimeout(tick, 1000);
  });
}

function showCakeDrawing() {
  isDrawingCake = true;
  controls.classList.remove('show');
  cakeOverlay.classList.add('show');
  initCakeDrawing(); // 完了時に afterCakeDrawn() が走る
}

async function startPostCakeSequence(){
  isDrawingCake = false;
  controls.classList.add('show');

  startMatrixRain();
  startHearts();
  try { bgm.currentTime = 0; bgm.loop = true; await bgm.play(); } catch(e){}
  setInterval(() => { if (Math.random() > 0.4) launchFireworks(); }, 3000);

  await showLettersOnce([
    {text:'HAPPY',y:35},
    {text:'BIRTHDAY!',y:45},
    {text:'to',y:55},
    {text:'ERINA!',y:65}
  ]);
  await showHeadline("I hope you have another wonderful year！");
}

function showHeadline(text){
  return new Promise((resolve)=>{
    headline.textContent = text;
    headline.classList.add('show');
    setTimeout(resolve, 800);
  });
}

/* ====== Matrix Rain ====== */
function startMatrixRain(){
  matrix.style.display = 'block';
  const c = matrix, ctx = fitCanvasToStage(c);
  const chars = "HAPPYBIRTHDAY!💖🎂🎉".split("");
  let cols = 0, drops = [];
  const resize = () => {
    fitCanvasToStage(c);
    const { w } = stageSize();
    cols = Math.floor(w/14); drops = Array(cols).fill(1);
  };
  resize(); addEventListener('resize', resize);
  (function draw(){
    const { h } = stageSize();
    ctx.fillStyle = "rgba(10,11,16,0.35)"; ctx.fillRect(0,0,c.width,c.height);
    ctx.fillStyle = "rgba(255,111,177,0.6)"; ctx.font = "16px monospace";
    for(let i=0;i<drops.length;i++){
      const txt = chars[Math.floor(Math.random()*chars.length)];
      ctx.fillText(txt, i*14, drops[i]*18);
      if(drops[i]*18>h && Math.random()>0.975) drops[i]=0;
      drops[i]++;
    }
    requestAnimationFrame(draw);
  })();
}

/* ====== Hearts ====== */
function startHearts(){
  const cvs = heartsCanvas, ctx = fitCanvasToStage(cvs);
  const resize = () => { fitCanvasToStage(cvs); };
  resize(); addEventListener('resize', resize);
  const parts = [];
  function spawn(){ for(let i=0;i<15;i++){ parts.push({ x:Math.random()*cvs.width, y:-20, vx:(Math.random()-.5)*1.2, vy:Math.random()*1.5+.8, rot:Math.random()*Math.PI, vr:(Math.random()-.5)*.1, size:Math.random()*12+8, alpha:1 }); } }
  function heartPath(ctx,x,y,s,r){ ctx.save(); ctx.translate(x,y); ctx.rotate(r); ctx.scale(s,s); ctx.beginPath(); ctx.moveTo(0,-2); ctx.bezierCurveTo(2,-4,6,-3,6,0); ctx.bezierCurveTo(6,3,3,5,0,7); ctx.bezierCurveTo(-3,5,-6,3,-6,0); ctx.bezierCurveTo(-6,-3,-2,-4,0,-2); ctx.closePath(); ctx.restore(); }
  (function step(){
    ctx.clearRect(0,0,cvs.width,cvs.height);
    ctx.fillStyle="rgba(255,111,177,0.9)";
    parts.forEach(p=>{ p.x+=p.vx; p.y+=p.vy; p.rot+=p.vr; p.alpha*=0.996; ctx.globalAlpha=Math.max(p.alpha,0); heartPath(ctx,p.x,p.y,p.size/7,p.rot); ctx.fill(); });
    ctx.globalAlpha=1; requestAnimationFrame(step);
  })();
  setTimeout(()=>{ cvs.classList.add('show'); const t=setInterval(spawn,200); setTimeout(()=>clearInterval(t),15000); }, 4000);
}

/* ====== 文字表示 ====== */
function showLettersOnce(lines){
  return new Promise((resolve)=>{
    headline.classList.remove('show');
    createLetters(lines);
    setTimeout(()=> startAnimation(()=>{
      container.innerHTML = '';
      resolve();
    }), 100);
  });
}
function createLetters(lines){
  container.innerHTML = ''; letters = [];
  let idx=0;
  lines.forEach(line=>{
    const lineDiv=document.createElement('div');
    lineDiv.style.position='absolute'; lineDiv.style.top=`${line.y}%`; lineDiv.style.left='50%';
    lineDiv.style.transform='translateX(-50%)'; lineDiv.style.display='flex'; lineDiv.style.justifyContent='center'; lineDiv.style.whiteSpace='nowrap';
    [...line.text].forEach(ch=>{
      if(ch===' ') return;
      const box=document.createElement('div'); box.style.position='relative'; box.style.display='inline-block';
      const sp=document.createElement('span'); sp.className='letter'; sp.textContent=ch; sp.style.color=colors[idx%colors.length]; sp.style.animationDelay=`${idx*0.15}s`;
      const bal=document.createElement('div'); bal.className='balloon'; bal.style.background=colors[idx%colors.length];
      box.appendChild(bal); box.appendChild(sp); lineDiv.appendChild(box);
      letters.push({letter:sp, balloon:bal}); idx++;
    });
    container.appendChild(lineDiv);
  });
}
function startAnimation(onDone){
  letters.forEach((it,i)=>{
    const {letter}=it;
    letter.style.animation=`letterDrop 0.8s ${i*0.15}s ease-out forwards`;
    setTimeout(()=>{ letter.style.animation+=`, letterBounce 0.6s ${i*0.15+1}s ease-in-out`; }, (i*0.15+1)*1000);
  });
  const delayBeforeFloat = (letters.length*0.15+3)*1000;
  setTimeout(()=>{
    createBalloonEffect();
    setTimeout(()=>{ typeof onDone === 'function' && onDone(); }, 3500);
  }, delayBeforeFloat);
  setTimeout(()=> launchFireworks(), delayBeforeFloat);
}
function createBalloonEffect(){
  letters.forEach((it,i)=>{
    const {letter, balloon}=it;
    setTimeout(()=>{ balloon.style.animation=`balloonAppear .5s ease-out forwards`;
      setTimeout(()=>{ letter.style.animation=`balloonFloat 3s linear forwards`; balloon.style.animation=`balloonFloatUp 3s linear forwards`; }, 500);
    }, i*100);
  });
}

/* ====== 花火 ====== */
function launchFireworks(){ for(let i=0;i<4;i++) setTimeout(launchSingleFirework, i*600); }
function launchSingleFirework(){
  try { sfxFire.currentTime = 0; sfxFire.play(); } catch(e){}
  const { w, h } = stageSize();
  const x=Math.random()*(w*0.6)+w*0.2, y=h, explodeY=Math.random()*(h*0.4)+100;
  const d=y-explodeY; createLaunchTrail(x,y,d, ()=>explodeFirework(x,explodeY));
}
function createLaunchTrail(x,y,d,onDone){
  const t=document.createElement('div'); t.className='firework-trail'; t.style.left=x+'px'; t.style.top=y+'px';
  t.style.setProperty('--launch-distance',`-${d}px`); t.style.animation='fireworkLaunch 1.2s ease-out forwards'; stage.appendChild(t);
  for(let i=0;i<10;i++) setTimeout(()=>createSmoke(x+Math.random()*10-5, y-(d*i/10)), i*120);
  setTimeout(()=>{ t.remove(); onDone(); },1200);
}
function createSmoke(x,y){ const s=document.createElement('div'); s.className='smoke'; s.style.left=x+'px'; s.style.top=y+'px'; s.style.animation='smokeRise 2s ease-out forwards'; stage.appendChild(s); setTimeout(()=>s.remove(),2000); }
function explodeFirework(x,y){
  const base = fireworkColors[Math.floor(Math.random()*fireworkColors.length)];
  const types=['peony','heart','burst']; const tp=types[Math.floor(Math.random()*types.length)];
  if(tp==='peony') createPeonyFirework(x,y,base);
  if(tp==='heart') createHeartFirework(x,y,base);
  if(tp==='burst') createBurstFirework(x,y,base);
}
function createPeonyFirework(x,y,c){
  const n=100;
  for(let i=0;i<n;i++){
    const p=document.createElement('div'); p.className='firework-particle'; p.style.left=x+'px'; p.style.top=y+'px';
    const col=Math.random()>0.8?fireworkColors[Math.floor(Math.random()*fireworkColors.length)]:c;
    p.style.backgroundColor=col; p.style.boxShadow=`0 0 5px ${col}`;
    const ang=(i/n)*Math.PI*2, dist=Math.random()*100+50, dx=Math.cos(ang)*dist, dy=Math.sin(ang)*dist;
    p.style.setProperty('--dx',dx+'px'); p.style.setProperty('--dy',dy+'px');
    p.style.animation=`particleBurst ${1.8+Math.random()*0.5}s ease-out forwards`; stage.appendChild(p);
    setTimeout(()=>p.remove(),2300);
  }
}
function createHeartFirework(x,y,c){
  const n=80, s=12;
  for(let i=0;i<n;i++){
    const t=(i/n)*Math.PI*2, hx=16*Math.pow(Math.sin(t),3), hy=-(13*Math.cos(t)-5*Math.cos(2*t)-2*Math.cos(3*t)-Math.cos(4*t));
    const p=document.createElement('div'); p.className='firework-particle'; p.style.left=x+'px'; p.style.top=y+'px'; p.style.backgroundColor=c; p.style.boxShadow=`0 0 8px ${c}`;
    p.style.setProperty('--dx',(hx*s)+'px'); p.style.setProperty('--dy',(hy*s)+'px');
    p.style.animation=`particleBurst 2.5s ease-out forwards`; stage.appendChild(p);
    setTimeout(()=>p.remove(),2500);
  }
}
function createBurstFirework(x,y,c){
  const n=60;
  for(let i=0;i<n;i++){
    const p=document.createElement('div'); p.className='firework-particle'; p.style.left=x+'px'; p.style.top=y+'px';
    const col=Math.random()>0.5?fireworkColors[Math.floor(Math.random()*fireworkColors.length)]:c;
    p.style.backgroundColor=col;
    const ang=Math.random()*Math.PI*2, dist=Math.random()*120+60, dx=Math.cos(ang)*dist, dy=Math.sin(ang)*dist - Math.random()*40;
    p.style.setProperty('--dx',dx+'px'); p.style.setProperty('--dy',dy+'px');
    p.style.animation=`particleBurst ${1.2+Math.random()*0.8}s ease-out forwards`; stage.appendChild(p);
    setTimeout(()=>p.remove(),2000);
  }
}

/* ====== 画像/ユーティリティ ====== */
function showImage(){ document.getElementById('imgWrap').classList.add('show'); }
function hideImage(){ document.getElementById('imgWrap').classList.remove('show'); }
const params = new URLSearchParams(location.search);
if (params.get("img")) document.getElementById("gift").src = params.get("img");
setInterval(()=>{ const hue=Math.random()*360; document.documentElement.style.setProperty('--bg', `hsl(${hue}, 20%, 8%)`); }, 30000);

document.addEventListener('keydown', (e) => {
  if (isDrawingCake) return;
  switch(e.key){
    case 'f': case 'F': launchFireworks(); break;
    case 'p': case 'P': showImage(); break;
    case 'Escape': hideImage(); break;
  }
});
let touchStartY = 0;
document.addEventListener('touchstart',(e)=>{ touchStartY = e.touches[0].clientY; });
document.addEventListener('touchend',(e)=>{
  if (isDrawingCake) return;
  const diff = touchStartY - e.changedTouches[0].clientY;
  if (diff > 50) launchFireworks();
});

/* =========================================================
   ケーキ描画（速度UP・write.mp3再生・線リスト）
   ========================================================= */
function initCakeDrawing() {
  const INC_PER_FRAME = 140;         // 速さ
  const sq = (v) => v*v;
  const pow4 = (v) => v*v*v*v;

  const canvas = cakeCanvas;
  const ctx = fitCanvasToStage(canvas);
  const { w: CSS_W, h: CSS_H } = stageSize();

  const world = { xmin: -11, xmax: 12, ymin: -11, ymax: 24 };
  function x2px(x){ return (x - world.xmin) / (world.xmax - world.xmin) * CSS_W; }
  function y2px(y){ return CSS_H - (y - world.ymin) / (world.ymax - world.ymin) * CSS_H; }

  const linspace = (a,b,n) => Array.from({length:n}, (_,i)=> a + (b-a)*(i/(n-1)));
  const isFinitePair = (p) => Number.isFinite(p[0]) && Number.isFinite(p[1]);

  function splitByJump(points, jump=0.6){
    const parts = []; let part = [];
    for (let i=0;i<points.length;i++){
      const p = points[i];
      if (!isFinitePair(p)) { if (part.length>1) parts.push(part); part=[]; continue; }
      if (part.length){
        const q = part[part.length-1];
        const dx = p[0]-q[0], dy = p[1]-q[1];
        if (!Number.isFinite(dx) || !Number.isFinite(dy) || Math.hypot(dx,dy) > jump) {
          if (part.length>1) parts.push(part);
          part = [p];
        } else { part.push(p); }
      } else { part.push(p); }
    }
    if (part.length>1) parts.push(part);
    return parts;
  }

  function genFromX(f, x0, x1, n=900, mask=()=>true){
    const xs = linspace(x0, x1, n);
    const pts = xs.map(x => {
      const y = f(x);
      if (!Number.isFinite(y) || !mask(x,y)) return [NaN,NaN];
      return [x,y];
    });
    return splitByJump(pts);
  }
  function genFromY(g, y0, y1, n=900, mask=()=>true){
    const ys = linspace(y0, y1, n);
    const pts = ys.map(y => {
      const x = g(y);
      if (!Number.isFinite(x) || !mask(x,y)) return [NaN,NaN];
      return [x,y];
    });
    return splitByJump(pts);
  }
  function genEllipse(cx, cy, a2, b2, n=1400, mask=()=>true){
    const a = Math.sqrt(a2), b = Math.sqrt(b2);
    const ts = linspace(0, 2*Math.PI, n);
    const pts = ts.map(t=>{
      const x = cx + a*Math.cos(t);
      const y = cy + b*Math.sin(t);
      if (!mask(x,y)) return [NaN,NaN];
      return [x,y];
    });
    return splitByJump(pts);
  }
  function genCircle(cx, cy, r2, n=1000, mask=()=>true){
    const r = Math.sqrt(r2);
    return genEllipse(cx, cy, r*r, r*r, n, mask);
  }
  function genHyperbola_x(cx, cy, a2, b2, x0, x1, y0, y1, n=1200){
    const xs = linspace(x0, x1, n);
    const up=[], down=[];
    xs.forEach(x=>{
      const val = ( (x-cx)*(x-cx)/a2 ) - 1;
      if (val >= 0){
        const dy = Math.sqrt(val*b2);
        const yU = cy + dy, yD = cy - dy;
        up.push([x,yU]); down.push([x,yD]);
      } else { up.push([NaN,NaN]); down.push([NaN,NaN]); }
    });
    return [...splitByJump(up), ...splitByJump(down)];
  }

  const segments = [];
  function add(label, parts){ segments.push({label, parts}); }
  function addFromX(label, f, x0, x1, mask){ add(label, genFromX(f,x0,x1,900,mask)); }
  function addFromY(label, g, y0, y1, mask){ add(label, genFromY(g,y0,y1,900,mask)); }
  function addEllipse(label, cx,cy,a2,b2,mask){ add(label, genEllipse(cx,cy,a2,b2,1400,mask)); }
  function addCircle(label, cx,cy,r2,mask){ add(label, genCircle(cx,cy,r2,1000,mask)); }
  function addHyperbolaX(label, cx,cy,a2,b2,x0,x1,y0,y1){ add(label, genHyperbola_x(cx,cy,a2,b2,x0,x1,y0,y1)); }

  /* ==== 線リスト（省略なし・元のまま） ==== */
  addFromY("x=2.9{2.035≤y≤5}",     y=>2.9, 2.035, 5);
  addFromY("x=1.9{2≤y≤5}",         y=>1.9, 2, 5);
  addFromY("x=0.5{2.035≤y≤5}",     y=>0.5, 2.035, 5);
  addFromY("x=-0.5{2≤y≤5}",        y=>-0.5,2,5);
  addFromY("x=-1.9{2.035≤y≤5}",    y=>-1.9,2.035,5);
  addFromY("x=-2.9{2≤y≤5}",        y=>-2.9,2,5);
  addFromY("x=-5.4{-4.6≤y≤2.2}",   y=>-5.4,-4.6,2.2);
  addFromY("x=5.4{-4.6≤y≤2.2}",    y=>5.4,-4.6,2.2);

  addFromX("y=.2cos(1.3x)+0{-5.4≤x≤5.4}", x=>0.2*Math.cos(1.3*x)+0, -5.4, 5.4);
  addFromX("y=.2cos(1.3x)-.6{-5.4≤x≤5.4}", x=>0.2*Math.cos(1.3*x)-0.6, -5.4, 5.4);
  addFromX("y=.2cos(1.3x)-2.8{-5.4≤x≤5.4}", x=>0.2*Math.cos(1.3*x)-2.8, -5.4, 5.4);
  addFromX("y=.2cos(1.3x)-3.4{-5.4≤x≤5.4}", x=>0.2*Math.cos(1.3*x)-3.4, -5.4, 5.4);

  addEllipse("1=((y+4.6)^2)/.8 + x^2/29.15 {y≤-4.6}", 0,-4.6,29.15,0.8, (x,y)=> y<=-4.6);
  addEllipse("1=((y+4.8)^2)/2.2 + x^2/45 {-5.4≤x≤5.4,-10≤y≤-5}", 0,-4.8,45,2.2, (x,y)=> x>=-5.4 && x<=5.4 && y>=-10 && y<=-5);
  addEllipse("1=((y+4.8)^2)/2.2 + x^2/45 {-10≤x≤-5.4}", 0,-4.8,45,2.2, (x,y)=> x>=-10 && x<=-5.4);
  addEllipse("1=((y+4.8)^2)/2.2 + x^2/45 {5.4≤x≤10}",   0,-4.8,45,2.2,  (x,y)=> x>=5.4 && x<=10);

  addFromX("y=-.45√(x+5.7)-5.6{x≤0}", x=>{ const v=x+5.7; return v>=0? -0.45*Math.sqrt(v)-5.6 : NaN; }, -5.7, 0);
  addFromX("y=-.45√(-x+5.7)-5.6{x≥0}", x=>{ const v=-x+5.7; return v>=0? -0.45*Math.sqrt(v)-5.6 : NaN; }, 0, 5.7);

  addEllipse("1=((y-2.2)^2)/.8 + x^2/29.15 {x≤-2.9}", 0,2.2,29.15,0.8, (x,y)=> x<=-2.9);
  addEllipse("1=((y-2.2)^2)/.8 + x^2/29.15 {x≥2.9}",  0,2.2,29.15,0.8, (x,y)=> x>=2.9);
  addEllipse("1=((y-2.2)^2)/.8 + x^2/29.15 {y≤2.1}",  0,2.2,29.15,0.8, (x,y)=> y<=2.1);
  addEllipse("1=((y-2.2)^2)/.8 + x^2/29.15 {-1.9≤x≤-.5}", 0,2.2,29.15,0.8, (x,y)=> x>=-1.9 && x<=-0.5);
  addEllipse("1=((y-2.2)^2)/.8 + x^2/29.15 {.5≤x≤1.9}",    0,2.2,29.15,0.8, (x,y)=> x>=0.5 && x<=1.9);

  addFromX("y=.95log(.6(-x-1.3))+2{-3.25≤x≤-2.53}", x=>{ const a=0.6*(-x-1.3); return a>0? 0.95*Math.log(a)+2 : NaN; }, -3.25, -2.53);
  addFromX("y=.95log(.6(x+3.9))+1.96{-2.8≤x≤-1.55}", x=>{ const a=0.6*(x+3.9);  return a>0? 0.95*Math.log(a)+1.96 : NaN; }, -2.8, -1.55);
  addFromX("y=.95log(.6(-x+1.1))+2{-.85≤x≤.1}",      x=>{ const a=0.6*(-x+1.1); return a>0? 0.95*Math.log(a)+2 : NaN; }, -0.85, 0.1);
  addFromX("y=.95log(.6(x+1.5))+1.96{-.137≤x≤.85}",  x=>{ const a=0.6*(x+1.5);  return a>0? 0.95*Math.log(a)+1.96 : NaN; }, -0.137, 0.85);
  addFromX("y=.95log(.6(-x+3.5))+2{1.55≤x≤2.5}",     x=>{ const a=0.6*(-x+3.5); return a>0? 0.95*Math.log(a)+2 : NaN; }, 1.55, 2.5);
  addFromX("y=.95log(.6(x-.9))+1.96{2.263≤x≤3.25}",  x=>{ const a=0.6*(x-0.9);  return a>0? 0.95*Math.log(a)+1.96 : NaN; }, 2.263, 3.25);

  addFromX("y=5{-2.9≤x≤-1.9}", x=>5, -2.9, -1.9);
  addFromX("y=5{-.5≤x≤.5}",    x=>5, -0.5, 0.5);
  addFromX("y=5{1.9≤x≤2.9}",   x=>5, 1.9, 2.9);
  addFromY("x=-2.4{5≤y≤5.15}", y=>-2.4, 5, 5.15);
  addFromY("x=0{5≤y≤5.15}",    y=>0, 5, 5.15);
  addFromY("x=2.4{5≤y≤5.15}",  y=>2.4, 5, 5.15);

  const capMask = (x,y)=> y<=5.314;
  addFromX("y=190(x+2.4)^4+5.15{y≤5.314}", x=>190*pow4(x+2.4)+5.15, -2.7, -2.1, capMask);
  addFromX("y=190x^4+5.15{y≤5.314}",       x=>190*pow4(x)+5.15,     -0.3, 0.3,  capMask);
  addFromX("y=190(x-2.4)^4+5.15{y≤5.314}", x=>190*pow4(x-2.4)+5.15,  2.1,  2.7,  capMask);

  const vMask = (x,y)=> y>=5.314;
  addFromX("y=-4|x+2.4|+6{y≥5.314}", x=>-4*Math.abs(x+2.4)+6, -2.7, -2.1, vMask);
  addFromX("y=-4|x|+6{y≥5.314}",     x=>-4*Math.abs(x)+6,     -0.3,  0.3,  vMask);
  addFromX("y=-4|x-2.4|+6{y≥5.314}", x=>-4*Math.abs(x-2.4)+6,  2.1,  2.7,  vMask);

  addFromY("x=-9{17≤y≤22}", y=>-9, 17, 22);
  addFromY("x=-8{17≤y≤19}", y=>-8, 17, 19);
  addFromY("x=-8{20≤y≤22}", y=>-8, 20, 22);
  addFromY("x=-7{17≤y≤19}", y=>-7, 17, 19);
  addFromY("x=-7{20≤y≤22}", y=>-7, 20, 22);
  addFromY("x=-6{17≤y≤22}", y=>-6, 17, 22);

  addFromX("y=19{-8≤x≤-7}", x=>19, -8, -7);
  addFromX("y=20{-8≤x≤-7}", x=>20, -8, -7);

  addFromX("y=(x+6.5)^2+16.8{-7≤x≤-6}",   x=> sq(x+6.5) + 16.8, -7, -6);
  addFromX("y=(x+8.5)^2+16.8{-9≤x≤-8}",   x=> sq(x+8.5) + 16.8, -9, -8);
  addFromX("y=-(x+6.5)^2+22.2{-7≤x≤-6}",  x=> -sq(x+6.5) + 22.2, -7, -6);
  addFromX("y=-(x+8.5)^2+22.2{-9≤x≤-8}",  x=> -sq(x+8.5) + 22.2, -9, -8);

  addCircle("3=(x+3.3)^2+(y-18.3)^2 {x≤-1.87}", -3.3, 18.3, 3.0, (x,y)=> x<=-1.87);
  addCircle("3=(x+3.3)^2+(y-18.3)^2 {y≥18.73}", -3.3, 18.3, 3.0, (x,y)=> y>=18.73);
  addCircle(".3=(x+3.3)^2+(y-18.3)^2",          -3.3, 18.3, 0.3, ()=>true);

  addFromY("y=-2.3x+15{16.568≤y≤18.732}", y=> (15-y)/2.3, 16.568, 18.732);
  addFromY("y=-2.3x+13{16.612≤y≤17.314}", y=> (13 - y)/2.3, 16.612, 17.314);

  addFromX("y=(x+1.1)^2+16.4{-1.577≤x≤-.684}", x=> sq(x+1.1) + 16.4, -1.577, -0.684);

  addCircle("3=(x-2)^2+(y-18.3)^2 {x≥.75}", 2, 18.3, 3.0, (x,y)=> x>=0.75);
  addCircle(".3=(x-2)^2+(y-18.3)^2",        2, 18.3, 0.3, ()=>true);

  addFromY("x=0{15≤y≤20}",   y=>0, 15, 20);
  addFromY("x=.75{19.499≤y≤20}", y=>0.75, 19.499, 20);
  addFromY("x=.75{15≤y≤17.101}", y=>0.75, 15, 17.101);

  addFromX("y=-(x-.375)^2+20.14{0≤x≤.75}", x=> -sq(x-0.375) + 20.14, 0, 0.75);
  addFromX("y=(x-.375)^2+14.86{0≤x≤.75}",  x=>  sq(x-0.375) + 14.86, 0, 0.75);

  addCircle("3=(x-6.5)^2+(y-18.3)^2 {x≥5.25}", 6.5, 18.3, 3.0, (x,y)=> x>=5.25);
  addCircle(".3=(x-6.5)^2+(y-18.3)^2",         6.5, 18.3, 0.3, ()=>true);

  addFromY("x=4.5{15≤y≤20}",   y=>4.5, 15, 20);
  addFromY("x=5.25{19.499≤y≤20}", y=>5.25, 19.499, 20);
  addFromY("x=5.25{15≤y≤17.101}", y=>5.25, 15, 17.101);

  addFromX("y=-(x-4.875)^2+20.14{4.5≤x≤5.25}", x=> -sq(x-4.875) + 20.14, 4.5, 5.25);
  addFromX("y=(x-4.875)^2+14.86{4.5≤x≤5.25}",  x=>  sq(x-4.875) + 14.86, 4.5, 5.25);

  addFromY("x=10{15≤y≤17.625}", y=>10, 15, 17.625);
  addFromY("x=10.75{15≤y≤17.625}", y=>10.75, 15, 17.625);
  addFromX("y=(x-10.375)^2+14.86{10≤x≤10.75}", x=> sq(x-10.375) + 14.86, 10, 10.75);

  addFromY("y=1.5x+1.5{17.625≤y≤20}",  y=> (y-1.5)/1.5, 17.625, 20);
  addFromY("y=-1.5x+32.63{17.625≤y≤20}", y=> (32.63 - y)/1.5, 17.625, 20);
  addFromX("y=1.5|x-10.375|+18.5{y≤20}", x=> 1.5*Math.abs(x-10.375)+18.5, 9.0, 11.75, (x,y)=> y<=20);

  addFromX("y=-(x-8.91)^2+20.22{y≥20}",   x=> -sq(x-8.91)  + 20.22,  8.31,  9.51,  (x,y)=> y>=20);
  addFromX("y=-(x-11.86)^2+20.22{y≥20}",  x=> -sq(x-11.86) + 20.22, 11.26, 12.46, (x,y)=> y>=20);

  addFromY("x=-9{9.753≤y≤14}", y=>-9, 9.753, 14);

  addHyperbolaX("1=(x+5)^2/1 - (y-11)^2/.322^2 {x∈[-9,-5], y≤11.875}",   -5, 11, 1, sq(0.322), -9, -5, -99, 11.875);
  addHyperbolaX("1=(x+5)^2/1 - (y-12.75)^2/.322^2 {x∈[-9,-5], y≥11.875}", -5, 12.75, 1, sq(0.322), -9, -5, 11.875, 99);

  addHyperbolaX("1=(x+6.25)^2/1 - (y-11)^2/.2^2 {-8.4≤x≤-6}",   -6.25, 11, 1, sq(0.2), -8.4, -6, -99, 99);
  addHyperbolaX("1=(x+6.25)^2/1 - (y-12.75)^2/.2^2 {-8.4≤x≤-6}", -6.25, 12.75, 1, sq(0.2), -8.4, -6, -99, 99);

  addFromY("x=-8.4{12.369≤y≤13.131}", y=>-8.4, 12.369, 13.131);
  addFromY("x=-8.4{10.619≤y≤11.381}", y=>-8.4, 10.619, 11.381);
  addFromY("x=-5{11≤y≤11.875}",       y=>-5, 11, 11.875);
  addFromY("x=-2.5{11.45≤y≤12.3125}", y=>-2.5, 11.45, 12.3125);

  addFromX("y=.18x+11.9{-5≤x≤-2.5}",  x=> 0.18*x + 11.9, -5, -2.5);
  addFromX("y=.18x+12.76{-5≤x≤-2.5}", x=> 0.18*x + 12.76, -5, -2.5);

  addFromX("y-9.8=2·500^{-(x+1.5)}{-1.444≤x≤.5}", x=> 9.8 + 2*Math.pow(500, -(x+1.5)), -1.444, 0.5);

  addFromY("x=.5{12.125≤y≤14}", y=>0.5, 12.125, 14);
  addFromY("x=.5{9.55≤y≤9.8}",  y=>0.5, 9.55, 9.8);
  addFromY("x=1.25{9.55≤y≤14}", y=>1.25, 9.55, 14);
  addFromX("y=14{.5≤x≤1.25}",   x=>14, 0.5, 1.25);
  addFromX("y= -.5x^2 + 12.25{-1.444≤x≤.5}", x=> -0.5*x*x + 12.25, -1.444, 0.5);
  addFromX("y=9.55{.5≤x≤1.25}", x=>9.55, 0.5, 1.25);
  addCircle(".3=x^2+(y-11)^2", 0, 11, 0.3, ()=>true);
  addFromY("x-1.5=.5·sec(y-11){9.587≤y≤12.424}", y=> 1.5 + 0.5*(1/Math.cos(y-11)), 9.587, 12.424);
  addFromY("y=-5x+37{9.35≤y≤12.424}", y=> (37 - y)/5, 9.35, 12.424);
  addFromY("y=-5x+33{9.35≤y≤9.587}",  y=> (33 - y)/5, 9.35, 9.587);
  addFromX("y=9.35{4.73≤x≤5.53}", x=>9.35, 4.73, 5.53);
  addCircle(".3=(x-3.55)^2+(y-11)^2", 3.55, 11, 0.3, ()=>true);

  addFromY("y=-2x+25{12.424≥y≥10}",     y=> (25 - y)/2,    10,     12.424);
  addFromY("y=-2x+23.5{12.424≥y≥9.25}", y=> (23.5 - y)/2,  9.25,   12.424);
  addFromY("y=2x-5{10≤y≤12.424}",       y=> (y + 5)/2,     10,     12.424);
  addFromY("y=2x-5{7≤y≤9.25}",          y=> (y + 5)/2,     7,      9.25);
  addFromY("y=2x-6.5{7≤y≤12.424}",      y=> (y + 6.5)/2,   7,      12.424);
  addFromX("y=12.424{5.538≤x≤6.288}",   x=> 12.424,        5.538,  6.288);
  addFromX("y=12.424{8.712≤x≤9.462}",   x=> 12.424,        8.712,  9.462);
  addFromX("y=7{6≤x≤6.75}",             x=> 7,             6,      6.75);

  /* ===== 描画ループ ===== */
  let segIdx = 0, partial = 0;

  try { sfxWrite.currentTime = 0; sfxWrite.loop = true; sfxWrite.play(); } catch(e){}

  function drawParts(parts, upto=Infinity){
    ctx.lineWidth = 2; ctx.lineJoin = "round"; ctx.lineCap  = "round"; ctx.strokeStyle = "#111";
    let left = upto;
    for (const part of parts){
      if (part.length < 2) continue;
      const n = Math.min(part.length, left);
      if (n < 2) break;
      ctx.beginPath();
      ctx.moveTo(x2px(part[0][0]), y2px(part[0][1]));
      for (let i=1;i<n;i++) ctx.lineTo(x2px(part[i][0]), y2px(part[i][1]));
      ctx.stroke();
      left -= n;
      if (left <= 0) break;
    }
  }

  function step(){
    if (segIdx >= segments.length) { afterCakeDrawn(); return; }
    const seg = segments[segIdx];
    const parts = seg.parts;
    const count = parts.reduce((s,p)=> s + p.length, 0);
    partial += INC_PER_FRAME;
    if (partial >= count){
      drawParts(parts, count);
      segIdx++; partial = 0;
      const progress = Math.round((segIdx / segments.length) * 100);
      cakeProgress.textContent = `Drawing your special cake... ${progress}%`;
    }else{
      drawParts(parts, partial);
    }
    requestAnimationFrame(step);
  }

  function floodFillSeeds(seeds, rgba){
    const W = canvas.width, H = canvas.height;
    const img = ctx.getImageData(0,0,W,H);
    const data = img.data;
    function canFillAt(i){
      const r = data[i], g = data[i+1], b = data[i+2], a = data[i+3];
      return a >= 250 && r >= 235 && g >= 235 && b >= 235;
    }
    function setColor(i, rgba){ data[i]=rgba[0]; data[i+1]=rgba[1]; data[i+2]=rgba[2]; data[i+3]=rgba[3]; }
    for (const s of seeds){
      let px = Math.round(x2px(s.x));
      let py = Math.round(y2px(s.y));
      if (px<0||px>=W||py<0||py>=H) continue;
      const stack = [[px,py]];
      const visited = new Uint8Array(W*H);
      while (stack.length){
        const [x,y] = stack.pop();
        if (x<0||x>=W||y<0||y>=H) continue;
        const idxPix = (y*W + x);
        if (visited[idxPix]) continue; visited[idxPix]=1;
        const i = idxPix*4;
        if (!canFillAt(i)) continue;
        setColor(i, rgba);
        stack.push([x+1,y],[x-1,y],[x,y+1],[x,y-1]);
      }
    }
    ctx.putImageData(img,0,0);
  }

  function hex2rgba(hex, a=255){
    const h = hex.replace('#','').trim();
    const r = parseInt(h.slice(0,2),16);
    const g = parseInt(h.slice(2,4),16);
    const b = parseInt(h.slice(4,6),16);
    return [r,g,b,a];
  }

  function afterCakeDrawn(){
    cakeProgress.textContent = "Adding colors...";

    const cakeSeeds = [
      {x: 0, y: 0}, {x: -3.0, y: 0.0}, {x:  3.0, y: 0.0},
      {x:  0.0, y: 4.8}, {x:  0.0, y:-3.5}
    ];
    const cakeRGBA = hex2rgba('#ffd1dc', 255);
    floodFillSeeds(cakeSeeds, cakeRGBA);

    const letterSeeds = [
      {x:-7.5, y:18.5}, {x:-3.3, y:18.3}, {x: 2.0, y:18.3},
      {x: 6.5, y:18.3}, {x:10.38,y:18.9}
    ];
    const lettersRGBA = hex2rgba('#ffd86a', 255);
    floodFillSeeds(letterSeeds, lettersRGBA);

    ctx.lineWidth = 2;
    for (const seg of segments) drawParts(seg.parts);

    cakeProgress.textContent = "Perfect! Your special cake is ready! 🎂✨";
    try { sfxWrite.pause(); sfxWrite.currentTime = 0; } catch(e){}
    setTimeout(() => { cakeOverlay.classList.remove('show'); startPostCakeSequence(); }, 5000);
  }

  requestAnimationFrame(step);
}
</script>
</body>
</html>

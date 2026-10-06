# anniversaire-lucrecia. 
<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Joyeux anniversaire 🎂</title>
<style>
:root{--bg:#fff0f5;--card:#fff;--text:#4a1d3a;--accent:#ff4d8d;--muted:#8a5a75;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#2a1020;--card:#3a1830;--text:#ffe3ef;--accent:#ff6fa3;--muted:#d9a3bd}}
:root[data-theme="dark"]{--bg:#2a1020;--card:#3a1830;--text:#ffe3ef;--accent:#ff6fa3;--muted:#d9a3bd}
html,body{height:100%;margin:0}
body{background:var(--bg);color:var(--text);font-family:system-ui,-apple-system,"Segoe UI",sans-serif;display:flex;align-items:center;justify-content:center;overflow:hidden}
.card{background:var(--card);border-radius:24px;padding:32px 24px;max-width:340px;width:86%;text-align:center;box-shadow:0 10px 40px rgba(255,77,141,.25);position:relative;z-index:2}
h1{font-size:1.6rem;margin:8px 0 12px}
p{color:var(--muted);line-height:1.5;margin:0 0 20px}
.big{font-size:4rem;line-height:1}
button{font:inherit;font-weight:600;border:0;border-radius:999px;padding:12px 26px;cursor:pointer;margin:6px}
.yes{background:var(--accent);color:#fff;font-size:1.1rem}
.no{background:transparent;color:var(--muted);border:2px solid var(--muted)}
.hidden{display:none}
#c{position:fixed;inset:0;pointer-events:none;z-index:1}
</style>
</head>
<body>
<canvas id="c"></canvas>

<div class="card" id="s1">
  <div class="big">🎁</div>
  <h1>J'ai une surprise pour toi…</h1>
  <p>Tu es prête à l'ouvrir ?</p>
  <button class="yes" id="yes">Oui 💖</button>
  <button class="no" id="no">Non</button>
</div>

<div class="card hidden" id="s2">
  <div class="big">🎂</div>
  <h1>Joyeux anniversaire, Lucrecia ! 🥳</h1>
  <p>Je te souhaite de connaître un bonheur immense. Je veux te voir sourire, réussir et accomplir tes rêves.</p>
  <p><strong style="color:var(--accent)">Joyeux anniversaire 💕</strong></p>
  <button class="yes" id="again">Encore des confettis 🎉</button>
</div>

<script>
const $=id=>document.getElementById(id);
const no=$('no');
let scale=1;
function dodge(e){
  e.preventDefault();
  no.style.position='fixed';
  no.style.left=(10+Math.random()*(innerWidth-110))+'px';
  no.style.top=(10+Math.random()*(innerHeight-60))+'px';
  scale+=.15;
  $('yes').style.transform='scale('+scale+')';
}
no.addEventListener('mouseover',dodge);
no.addEventListener('touchstart',dodge,{passive:false});
no.addEventListener('click',dodge);

const cv=$('c'),ctx=cv.getContext('2d');
let parts=[],running=false;
function size(){cv.width=innerWidth;cv.height=innerHeight}
addEventListener('resize',size);size();
function burst(){
  const cols=['#ff4d8d','#ffd166','#06d6a0','#4cc9f0','#b388ff','#fff'];
  for(let i=0;i<140;i++)parts.push({x:Math.random()*cv.width,y:-20-Math.random()*cv.height*.5,vx:(Math.random()-.5)*3,vy:2+Math.random()*4,s:5+Math.random()*7,r:Math.random()*6,c:cols[i%cols.length]});
  if(!running){running=true;requestAnimationFrame(tick)}
}
function tick(){
  ctx.clearRect(0,0,cv.width,cv.height);
  parts.forEach(p=>{p.x+=p.vx;p.y+=p.vy;p.r+=.1;ctx.fillStyle=p.c;ctx.save();ctx.translate(p.x,p.y);ctx.rotate(p.r);ctx.fillRect(-p.s/2,-p.s/2,p.s,p.s*.6);ctx.restore()});
  parts=parts.filter(p=>p.y<cv.height+20);
  if(parts.length)requestAnimationFrame(tick);else running=false;
}
$('yes').addEventListener('click',()=>{$('s1').classList.add('hidden');no.style.display='none';$('s2').classList.remove('hidden');burst()});
$('again').addEventListener('click',burst);
</script>
</body>
</html>

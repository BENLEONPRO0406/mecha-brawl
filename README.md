

<!DOCTYPE html>
<html lang="nl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
<title>Mecha Brawl</title>
<style>
*{box-sizing:border-box}
body{margin:0;background:#10182b;color:white;font-family:Arial;text-align:center;overflow:hidden;touch-action:none}
h1{color:#48eaff;margin:12px}
button{background:#13bde0;color:#071525;border:0;border-radius:12px;padding:13px;font-weight:bold;font-size:16px;margin:5px}
#arena{height:65vh;max-height:550px;background:radial-gradient(#35466a,#172039);position:relative;margin:10px;border:4px solid #48eaff;border-radius:18px;overflow:hidden}
.bot{position:absolute;font-size:55px;transform:translate(-50%,-50%)}
#player{left:50%;top:75%}
.enemy{color:#ff7373}
#controls{display:flex;justify-content:space-around;align-items:center}
#stick{width:110px;height:110px;background:#52617a;border-radius:50%;position:relative;touch-action:none}
#knob{position:absolute;width:45px;height:45px;background:#48eaff;border-radius:50%;left:32px;top:32px}
#attack{background:#ff9d35}
#super{background:#c17aff}
#health{color:#75ff9b;font-size:18px}
</style>
</head>
<body>
<h1>🤖 MECHA BRAWL</h1>
<div id="menu">
<p>Kies je robot:</p>
<button onclick="choose('🤖')">Titan</button>
<button onclick="choose('🚀')">Rocket</button>
<button onclick="choose('🦾')">Crusher</button>
<button onclick="choose('⚡')">Volt</button>
</div>
<div id="health">❤️ 100 HP</div>
<div id="arena">
<div id="player" class="bot">🤖</div>
<div id="enemy" class="bot enemy" style="left:50%;top:25%">👾</div>
<div id="enemy2" class="bot enemy" style="left:20%;top:40%">👾</div>
</div>
<div id="controls">
<div id="stick"><div id="knob"></div></div>
<div>
<button id="attack" onclick="attack()">⚔️ AANVAL</button><br>
<button id="super" onclick="superAttack()">⭐ SUPER</button>
</div>
</div>
<p id="message">Kies je robot en versla de vijanden!</p>
<script>
let x=50,y=75,hp=100,chosen='🤖';
const player=document.getElementById('player');
function choose(bot){
 chosen=bot;player.textContent=bot;
 document.getElementById('menu').style.display='none';
}
function move(dx,dy){
 x=Math.max(5,Math.min(95,x+dx));
 y=Math.max(8,Math.min(92,y+dy));
 player.style.left=x+'%';player.style.top=y+'%';
}
const stick=document.getElementById('stick');
const knob=document.getElementById('knob');
let active=false;
function point(e){
 const r=stick.getBoundingClientRect();
 let dx=e.clientX-r.left-55,dy=e.clientY-r.top-55;
 const len=Math.hypot(dx,dy),scale=Math.min(1,42/(len||1));
 knob.style.left=(32+dx*scale)+'px';
 knob.style.top=(32+dy*scale)+'px';
 move(dx/42*2,dy/42*2);
}
stick.addEventListener('pointerdown',e=>{active=true;stick.setPointerCapture(e.pointerId);point(e)});
stick.addEventListener('pointermove',e=>{if(active)point(e)});
stick.addEventListener('pointerup',()=>{active=false;knob.style.left='32px';knob.style.top='32px'});
function attack(){
 document.querySelectorAll('.enemy').forEach(e=>{
 let a=e.getBoundingClientRect(),b=player.getBoundingClientRect();
 if(Math.hypot(a.x-b.x,a.y-b.y)<180){
 e.textContent='💥';
 setTimeout(()=>e.remove(),250);
 }
 });
 document.getElementById('message').textContent='Aanval uitgevoerd!';
}
function superAttack(){
 document.querySelectorAll('.enemy').forEach(e=>e.remove());
 document.getElementById('message').textContent='⭐ SUPERKRACHT!';
}
</script>
</body>
</html>

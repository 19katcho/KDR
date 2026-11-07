<!DOCTYPE html>
<html lang="no">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Hyper Games Hub</title>

<style>
:root{
--bg:#0b1220;
--card:#111827;
--accent:#00d4ff;
--text:#fff;
}

*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Segoe UI,sans-serif;
}

body{
background:var(--bg);
color:var(--text);
display:flex;
min-height:100vh;
}

.sidebar{
width:240px;
background:#08101d;
padding:20px;
position:fixed;
height:100%;
overflow:auto;
}

.logo{
font-size:28px;
font-weight:bold;
color:var(--accent);
margin-bottom:20px;
}

.menu a{
display:block;
color:white;
text-decoration:none;
padding:12px;
margin:5px 0;
border-radius:10px;
}

.menu a:hover{
background:var(--accent);
}

.main{
margin-left:240px;
width:100%;
}

.hero{
text-align:center;
padding:60px;
background:linear-gradient(135deg,#00d4ff22,#8b5cf622);
}

.hero h1{
font-size:60px;
}

.stats{
display:flex;
justify-content:center;
gap:40px;
padding:20px;
flex-wrap:wrap;
}

.stat h2{
color:var(--accent);
}

.search{
padding:20px;
text-align:center;
}

.search input{
width:70%;
padding:15px;
border:none;
border-radius:10px;
background:#161f31;
color:white;
}

.filters{
display:flex;
justify-content:center;
flex-wrap:wrap;
gap:10px;
padding:10px 20px;
}

.filter{
background:#1f2937;
border:none;
color:white;
padding:10px 15px;
cursor:pointer;
border-radius:10px;
}

.filter:hover{
background:var(--accent);
}

.games{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(260px,1fr));
gap:20px;
padding:20px;
}

.card{
background:var(--card);
border-radius:15px;
overflow:hidden;
transition:0.3s;
position:relative;
}

.card:hover{
transform:translateY(-5px);
box-shadow:0 0 15px var(--accent);
}

.card img{
width:100%;
height:170px;
object-fit:cover;
}

.card-content{
padding:15px;
}

.category{
display:inline-block;
background:#2f3444;
padding:4px 8px;
border-radius:5px;
font-size:12px;
margin-bottom:10px;
}

.play{
display:block;
margin-top:10px;
background:var(--accent);
color:white;
text-decoration:none;
text-align:center;
padding:10px;
border-radius:10px;
font-weight:bold;
}

.favorite{
position:absolute;
top:10px;
right:10px;
font-size:24px;
cursor:pointer;
}

.favorite.active{
color:gold;
}
</style>
</head>
<body>

<div class="sidebar">
<div class="logo">🎮 Hyper Games</div>

<div class="menu">
<a href="#">🏠 Hjem</a>
<a href="#">🔥 Populære</a>
<a href="#">⭐ Favoritter</a>
<a href="#">🎯 Action</a>
<a href="#">🏎 Racing</a>
<a href="#">🔫 Shooter</a>
<a href="#">🧩 Puzzle</a>
</div>
</div>

<div class="main">

<section class="hero">
<h1>Hyper Games Hub</h1>
<p>Spill direkte i nettleseren</p>
</section>

<div class="stats">
<div class="stat">
<h2 id="gamesCount">0</h2>
<p>Spill</p>
</div>

<div class="stat">
<h2>12K+</h2>
<p>Spillere</p>
</div>

<div class="stat">
<h2>99%</h2>
<p>Oppetid</p>
</div>
</div>

<div class="search">
<input id="search" placeholder="Søk spill...">
</div>

<div class="filters">
<button class="filter" onclick="filterGames('all')">Alle</button>
<button class="filter" onclick="filterGames('Shooter')">Shooter</button>
<button class="filter" onclick="filterGames('Racing')">Racing</button>
<button class="filter" onclick="filterGames('Arcade')">Arcade</button>
<button class="filter" onclick="filterGames('Adventure')">Adventure</button>
</div>

<div class="games" id="games"></div>

</div>

<script>

const games = [

{name:"PolyTrack",cat:"Racing",url:"https://www.crazygames.com/game/polytrack"},
{name:"1v1.LOL",cat:"Shooter",url:"https://www.crazygames.com/game/1v1-lol"},
{name:"Run 3",cat:"Adventure",url:"https://www.coolmathgames.com/0-run-3"},
{name:"Shell Shockers",cat:"Shooter",url:"https://shellshock.io/"},
{name:"Slope",cat:"Arcade",url:"https://www.y8.com/games/slope"},
{name:"Tunnel Rush",cat:"Arcade",url:"https://poki.com/en/g/tunnel-rush"},
{name:"Minecraft Classic",cat:"Adventure",url:"https://classic.minecraft.net/"},
{name:"Drift Boss",cat:"Racing",url:"https://www.crazygames.com/game/drift-boss"},
{name:"Moto X3M",cat:"Racing",url:"https://www.crazygames.com/game/moto-x3m"},
{name:"Krunker",cat:"Shooter",url:"https://krunker.io/"},

{name:"Basket Random",cat:"Arcade",url:"https://poki.com/en/g/basket-random"},
{name:"Soccer Random",cat:"Arcade",url:"https://poki.com/en/g/soccer-random"},
{name:"Stickman Hook",cat:"Arcade",url:"https://poki.com/en/g/stickman-hook"},
{name:"Subway Surfers",cat:"Adventure",url:"https://poki.com/en/g/subway-surfers"},
{name:"Temple Run 2",cat:"Adventure",url:"https://poki.com/en/g/temple-run-2"},
{name:"Getaway Shootout",cat:"Shooter",url:"https://poki.com/en/g/getaway-shootout"},
{name:"Bitlife",cat:"Adventure",url:"https://bitlifeonline.github.io/"},
{name:"Drive Mad",cat:"Racing",url:"https://poki.com/en/g/drive-mad"},
{name:"OvO",cat:"Arcade",url:"https://ovo-game.github.io/"},
{name:"Indian Bikes Driving 3D",cat:"Racing",url:"https://indian-bikes-driving-3d-online.github.io/"},

{name:"Happy Wheels",cat:"Arcade",url:"https://totaljerkface.com/happy_wheels.tjf"},
{name:"Monkey Mart",cat:"Adventure",url:"https://poki.com/en/g/monkey-mart"},
{name:"Agar.io",cat:"Arcade",url:"https://agar.io/"},
{name:"Paper.io",cat:"Arcade",url:"https://paper-io.com/"},
{name:"Vex 3",cat:"Adventure",url:"https://poki.com/en/g/vex-3"},
{name:"Vex 4",cat:"Adventure",url:"https://poki.com/en/g/vex-4"},
{name:"Vex 5",cat:"Adventure",url:"https://poki.com/en/g/vex-5"},
{name:"Vex 6",cat:"Adventure",url:"https://poki.com/en/g/vex-6"},
{name:"Vex 7",cat:"Adventure",url:"https://poki.com/en/g/vex-7"},
{name:"Retro Bowl",cat:"Arcade",url:"https://poki.com/en/g/retro-bowl"},

{name:"Rocket Soccer Derby",cat:"Racing",url:"https://www.crazygames.com/game/rocket-soccer-derby"},
{name:"Rooftop Snipers",cat:"Shooter",url:"https://poki.com/en/g/rooftop-snipers"},
{name:"Dreadhead Parkour",cat:"Adventure",url:"https://poki.com/en/g/dreadhead-parkour"},
{name:"Elastic Man",cat:"Arcade",url:"https://elasticman.com/"},
{name:"FNAF",cat:"Adventure",url:"https://store.steampowered.com/app/319510/Five_Nights_at_Freddys/"},
{name:"Granny",cat:"Adventure",url:"https://store.steampowered.com/app/962400/Granny/"},
{name:"Madalin Stunt Cars",cat:"Racing",url:"https://www.crazygames.com/game/madalin-stunt-cars-2"},
{name:"Snow Rider",cat:"Adventure",url:"https://poki.com/en/g/snow-rider-3d"},
{name:"Parking Fury",cat:"Racing",url:"https://www.crazygames.com/game/parking-fury"},
{name:"Crossy Road",cat:"Arcade",url:"https://poki.com/en/g/crossy-road"},

{name:"Cookie Clicker",cat:"Arcade",url:"https://orteil.dashnet.org/cookieclicker/"},
{name:"Idle Breakout",cat:"Arcade",url:"https://idlebreakout.com/"},
{name:"Fireboy & Watergirl",cat:"Adventure",url:"https://poki.com/en/g/fireboy-and-watergirl-1-forest-temple"},
{name:"Tiny Fishing",cat:"Arcade",url:"https://tinyfishing.io/"},
{name:"Dragon Simulator",cat:"Adventure",url:"https://www.crazygames.com/game/dragon-simulator-3d"},
{name:"Sky Riders",cat:"Racing",url:"https://poki.com/en/g/sky-riders"},
{name:"Bad Ice Cream",cat:"Adventure",url:"https://poki.com/en/g/bad-ice-cream"},
{name:"Time Shooter 2",cat:"Shooter",url:"https://poki.com/en/g/time-shooter-2"},
{name:"Time Shooter 3",cat:"Shooter",url:"https://poki.com/en/g/time-shooter-3-swat"},
{name:"Combat Reloaded",cat:"Shooter",url:"https://www.crazygames.com/game/combat-reloaded"}

];

document.getElementById("gamesCount").textContent = games.length;

const container = document.getElementById("games");

function render(list){

container.innerHTML="";

list.forEach((game,index)=>{

let fav = localStorage.getItem(game.name);

container.innerHTML += `
<div class="card">

<div class="favorite ${fav?'active':''}"
onclick="toggleFav(this,'${game.name}')">
⭐
</div>

<img src="https://picsum.photos/400/250?random=${index+1}">

<div class="card-content">

<div class="category">${game.cat}</div>

<h3>${game.name}</h3>

<a class="play"
href="${game.url}"
target="_blank"
rel="noopener noreferrer">
Spill Nå
</a>

</div>
</div>`;
});

}

function toggleFav(el,name){

el.classList.toggle("active");

if(el.classList.contains("active")){
localStorage.setItem(name,"1");
}else{
localStorage.removeItem(name);
}

}

function filterGames(cat){

if(cat==="all"){
render(games);
return;
}

render(games.filter(g=>g.cat===cat));

}

document
.getElementById("search")
.addEventListener("keyup",e=>{

let value=e.target.value.toLowerCase();

render(
games.filter(g=>
g.name.toLowerCase().includes(value))
);

});

render(games);

</script>
</body>
</html>

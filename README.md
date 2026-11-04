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
--card2:#1f2937;
--accent:#00d4ff;
--accent2:#8b5cf6;
--text:#ffffff;
}

*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Segoe UI,sans-serif;
}

body{
background:var(--bg);
color:white;
display:flex;
min-height:100vh;
}

.sidebar{
width:250px;
background:#08101d;
padding:20px;
position:fixed;
height:100%;
overflow:auto;
border-right:1px solid #1f2937;
}

.logo{
font-size:28px;
font-weight:bold;
color:var(--accent);
margin-bottom:20px;
}

.menu a{
display:block;
padding:12px;
margin:5px 0;
text-decoration:none;
color:white;
border-radius:10px;
}

.menu a:hover{
background:var(--accent);
}

.main{
margin-left:250px;
width:100%;
}

.hero{
padding:60px;
text-align:center;
background:
linear-gradient(
135deg,
#00d4ff22,
#8b5cf622
);
}

.hero h1{
font-size:60px;
}

.hero p{
opacity:.8;
margin-top:10px;
}

.stats{
display:flex;
justify-content:center;
gap:40px;
padding:20px;
}

.stat{
text-align:center;
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
background:var(--card);
border:none;
border-radius:10px;
color:white;
}

.filters{
display:flex;
justify-content:center;
gap:10px;
flex-wrap:wrap;
padding-bottom:20px;
}

.filter{
padding:10px 15px;
cursor:pointer;
background:var(--card);
border:none;
color:white;
border-radius:10px;
}

.filter:hover{
background:var(--accent);
}

.games{
display:grid;
grid-template-columns:
repeat(auto-fit,minmax(250px,1fr));
gap:20px;
padding:20px;
}

.card{
background:var(--card);
border-radius:15px;
overflow:hidden;
transition:.3s;
position:relative;
}

.card:hover{
transform:translateY(-5px);
box-shadow:0 0 20px var(--accent);
}

.card img{
width:100%;
height:160px;
object-fit:cover;
}

.card-content{
padding:15px;
}

.card h3{
margin-bottom:10px;
}

.play{
display:block;
padding:10px;
background:var(--accent);
text-align:center;
border-radius:10px;
text-decoration:none;
color:white;
margin-top:12px;
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

.category{
display:inline-block;
padding:4px 8px;
background:#333;
border-radius:5px;
font-size:12px;
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
<h2 id="gamesCount">50</h2>
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

{name:"PolyTrack",cat:"Racing"},
{name:"1v1.LOL",cat:"Shooter"},
{name:"Run 3",cat:"Adventure"},
{name:"Shell Shockers",cat:"Shooter"},
{name:"Slope",cat:"Arcade"},
{name:"Tunnel Rush",cat:"Arcade"},
{name:"Minecraft Classic",cat:"Adventure"},
{name:"Drift Boss",cat:"Racing"},
{name:"Moto X3M",cat:"Racing"},
{name:"Krunker",cat:"Shooter"},
{name:"Basket Random",cat:"Arcade"},
{name:"Soccer Random",cat:"Arcade"},
{name:"Stickman Hook",cat:"Arcade"},
{name:"Subway Surfers",cat:"Adventure"},
{name:"Temple Run 2",cat:"Adventure"},
{name:"Getaway Shootout",cat:"Shooter"},
{name:"Bitlife",cat:"Adventure"},
{name:"Drive Mad",cat:"Racing"},
{name:"OvO",cat:"Arcade"},
{name:"Indian Bikes Driving 3D",cat:"Racing"},
{name:"Happy Wheels",cat:"Arcade"},
{name:"Monkey Mart",cat:"Adventure"},
{name:"Agar.io",cat:"Arcade"},
{name:"Paper.io",cat:"Arcade"},
{name:"Vex 3",cat:"Adventure"},
{name:"Vex 4",cat:"Adventure"},
{name:"Vex 5",cat:"Adventure"},
{name:"Vex 6",cat:"Adventure"},
{name:"Vex 7",cat:"Adventure"},
{name:"Retro Bowl",cat:"Arcade"},
{name:"Rocket Soccer Derby",cat:"Racing"},
{name:"Rooftop Snipers",cat:"Shooter"},
{name:"Dreadhead Parkour",cat:"Adventure"},
{name:"Elastic Man",cat:"Arcade"},
{name:"FNAF",cat:"Adventure"},
{name:"Granny",cat:"Adventure"},
{name:"Madalin Stunt Cars",cat:"Racing"},
{name:"Snow Rider",cat:"Adventure"},
{name:"Parking Fury",cat:"Racing"},
{name:"Crossy Road",cat:"Arcade"},
{name:"Cookie Clicker",cat:"Arcade"},
{name:"Idle Breakout",cat:"Arcade"},
{name:"Fireboy & Watergirl",cat:"Adventure"},
{name:"Tiny Fishing",cat:"Arcade"},
{name:"Dragon Simulator",cat:"Adventure"},
{name:"Sky Riders",cat:"Racing"},
{name:"Bad Ice Cream",cat:"Adventure"},
{name:"Time Shooter 2",cat:"Shooter"},
{name:"Time Shooter 3",cat:"Shooter"},
{name:"Combat Reloaded",cat:"Shooter"}

];

const container =
document.getElementById("games");

function render(list){

container.innerHTML="";

list.forEach((game,index)=>{

let fav =
localStorage.getItem(game.name);

container.innerHTML += `

<div class="card">

<div
class="favorite ${fav?'active':''}"
onclick="toggleFav(this,'${game.name}')"
>
⭐
</div>

<img src="https://picsum.photos/400/250?random=${index}">

<div class="card-content">

<div class="category">${game.cat}</div>

<h3>${game.name}</h3>

<a class="play"
href="#"
onclick="alert('Legg til spill-URL her');">
Spill Nå
</a>

</div>

</div>

`;

});
}

render(games);

function toggleFav(el,name){

el.classList.toggle("active");

if(el.classList.contains("active")){
localStorage.setItem(name,"1");
}else{
localStorage.removeItem(name);
}

}

document
.getElementById("search")
.addEventListener("keyup",(e)=>{

let value =
e.target.value.toLowerCase();

let filtered =
games.filter(g=>
g.name.toLowerCase()
.includes(value)
);

render(filtered);

});

function filterGames(cat){

if(cat==="all"){
render(games);
return;
}

render(
games.filter(
g=>g.cat===cat
)
);

}

</script>

</body>
</html>

<!DOCTYPE html>
<html>
<head>
  <title>PEAK Hub</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <style>
    body {
      margin: 0;
      font-family: Arial;
      display: flex;
      color: white;
      background: #020617;
    }

    #intro {
      position: fixed;
      width: 100%;
      height: 100%;
      background: black;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      z-index: 9999;
    }

    .intro-logo {
      font-size: 70px;
      color: #38bdf8;
      text-shadow: 0 0 20px #38bdf8;
      animation: pulse 1.5s infinite alternate;
    }

    @keyframes pulse {
      from { transform: scale(1); }
      to { transform: scale(1.2); }
    }

    .sidebar {
      width: 200px;
      height: 100vh;
      background: #020617;
      padding: 20px;
    }

    .sidebar h2 {
      color: #38bdf8;
      text-align: center;
    }

    .nav div {
      padding: 10px;
      margin: 10px 0;
      background: #1e293b;
      border-radius: 10px;
      cursor: pointer;
      text-align: center;
    }

    .nav div:hover {
      background: #38bdf8;
      color: black;
    }

    .main {
      flex: 1;
      padding: 20px;
    }

    .container {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
    }

    .card {
      background: #1e293b;
      margin: 10px;
      padding: 15px;
      border-radius: 12px;
      width: 220px;
      text-align: center;
    }

    iframe {
      width: 100%;
      height: 140px;
      border-radius: 10px;
      border: none;
    }

    input, textarea {
      padding: 8px;
      margin: 5px;
      border-radius: 8px;
      border: none;
      background: #0f172a;
      color: white;
    }

    button {
      padding: 6px 10px;
      border: none;
      border-radius: 8px;
      background: #38bdf8;
      cursor: pointer;
    }

  </style>
</head>

<body>

<!-- INTRO -->
<div id="intro">
  <div class="intro-logo">⚡ PEAK ⚡</div>
  <p>Loading...</p>
</div>

<!-- MUSIC -->
<audio id="bgMusic" loop>
  <source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" type="audio/mpeg">
</audio>

<div style="position:fixed;bottom:10px;right:10px;background:#1e293b;padding:10px;border-radius:10px;">
  <button onclick="toggleMusic()">⏯️</button>
  <input type="range" min="0" max="1" step="0.1" onchange="setVolume(this.value)">
</div>

<!-- SIDEBAR -->
<div class="sidebar">
  <h2>⚡ PEAK</h2>
  <div class="nav">
    <div onclick="showPage('home')">🏠 Home</div>
    <div onclick="showPage('games')">🎮 Games</div>
    <div onclick="showPage('sites')">🌐 Sites</div>
    <div onclick="showPage('ai')">🤖 AI</div>
    <div onclick="showPage('study')">📚 Study</div>
    <div onclick="secretMode()">🔐 Secret</div>
  </div>
</div>

<!-- MAIN -->
<div class="main">

  <div id="home">
    <h1 style="text-align:center;">Welcome to PEAK Hub 🔥</h1>
  </div>

  <div id="gamesPage" style="display:none;">
    <div class="container" id="games"></div>
  </div>

  <div id="sitesPage" style="display:none;">
    <div class="container">
      <div class="card"><a href="https://youtube.com" target="_blank">YouTube</a></div>
      <div class="card"><a href="https://discord.com" target="_blank">Discord</a></div>
      <div class="card"><a href="https://spotify.com" target="_blank">Spotify</a></div>
    </div>
  </div>

  <div id="aiPage" style="display:none;">
    <div class="container">
      <div class="card"><a href="https://chat.openai.com" target="_blank">ChatGPT</a></div>
      <div class="card"><a href="https://gemini.google.com" target="_blank">Gemini</a></div>
    </div>
  </div>

  <div id="studyPage" style="display:none;">
    <h2>📚 Study</h2>

    <div class="container">

      <div class="card">
        <h3>Tasks</h3>
        <input id="taskInput">
        <button onclick="addTask()">Add</button>
        <ul id="taskList"></ul>
      </div>

      <div class="card">
        <h3>Timer</h3>
        <p id="timer">25:00</p>
        <button onclick="startTimer()">Start</button>
      </div>

      <div class="card">
        <h3>Notes</h3>
        <textarea id="notes"></textarea>
        <button onclick="saveNotes()">Save</button>
      </div>

    </div>
  </div>

</div>

<script>

/* INTRO */
setTimeout(()=>{document.getElementById("intro").style.display="none";},2000);

/* MUSIC */
let music=document.getElementById("bgMusic");
document.addEventListener("click",()=>{music.play();},{once:true});

function toggleMusic(){
  music.paused ? music.play() : music.pause();
}

function setVolume(val){
  music.volume=val;
}

/* NAV */
function showPage(page){
  ["home","gamesPage","sitesPage","aiPage","studyPage"].forEach(id=>{
    document.getElementById(id).style.display="none";
  });

  if(page==="home") home.style.display="block";
  if(page==="games") gamesPage.style.display="block";
  if(page==="sites") sitesPage.style.display="block";
  if(page==="ai") aiPage.style.display="block";
  if(page==="study") studyPage.style.display="block";
}

/* GAMES */
let games=[
  {name:"Krunker",url:"https://krunker.io"},
  {name:"1v1.LOL",url:"https://1v1.lol"},
  {name:"Run 3",url:"https://run3.io"},
  {name:"Slope",url:"https://slopegame.io"}
];

let container=document.getElementById("games");

games.forEach(g=>{
  let div=document.createElement("div");
  div.className="card";
  div.innerHTML=`<h3>${g.name}</h3><iframe src="${g.url}"></iframe>`;
  container.appendChild(div);
});

/* SECRET */
function secretMode(){
  let pass=prompt("Password:");
  if(pass==="G1itch?!"){
    document.body.innerHTML="<h1 style='text-align:center;color:#00ffcc;'>🔐 SECRET MODE</h1>";
  }else alert("Wrong");
}

/* STUDY */
function addTask(){
  let li=document.createElement("li");
  li.textContent=taskInput.value;
  taskList.appendChild(li);
}

let time=1500;
function startTimer(){
  setInterval(()=>{
    let m=Math.floor(time/60);
    let s=time%60;
    timer.textContent=`${m}:${s<10?"0":""}${s}`;
    time--;
  },1000);
}

function saveNotes(){
  localStorage.setItem("notes",notes.value);
}

window.onload=()=>{
  notes.value=localStorage.getItem("notes")||"";
};

</script>

</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Peak Hub</title>

<style>
body {
  margin: 0;
  font-family: Arial;
  background: black;
  color: white;
}

/* 🌌 Galaxy /
body::before {
  content:"";
  position:fixed;
  width:100%;
  height:100%;
  background:url('https://wallpaperaccess.com/full/1465233.jpg') center/cover;
  filter:brightness(0.4);
  z-index:-1;
}

/ Lock + Profile /
.screen {
  position:fixed;
  width:100%;
  height:100%;
  background:black;
  display:flex;
  justify-content:center;
  align-items:center;
  flex-direction:column;
  z-index:999;
}

input, button {
  padding:10px;
  margin:5px;
}

button {
  background:purple;
  border:none;
  color:white;
  cursor:pointer;
}

/ Top /
#topbar {
  display:flex;
  justify-content:space-between;
  padding:10px;
}

/ Rows /
.row { margin:20px; }

.scroll {
  display:flex;
  overflow-x:auto;
  gap:12px;
}

.card {
  min-width:180px;
  transition:0.3s;
  cursor:pointer;
}

.card img {
  width:100%;
  border-radius:10px;
}

.card:hover { transform:scale(1.1); }

/ Popup /
#popup {
  position:fixed;
  width:100%;
  height:100%;
  background:rgba(0,0,0,0.9);
  display:none;
  justify-content:center;
  align-items:center;
}

iframe { width:80%; height:60%; }

.close {
  position:absolute;
  top:20px;
  right:30px;
  font-size:30px;
  cursor:pointer;
}

/ Search */
#search {
  width:60%;
  padding:10px;
  display:block;
  margin:10px auto;
}
</style>
</head>

<body>

<!-- 🔐 Lock -->
<div id="lock" class="screen">
  <h1>Enter Passcode</h1>
  <input type="password" id="code">
  <button onclick="unlock()">Enter</button>
</div>

<!-- 👤 Profiles -->
<div id="profiles" class="screen">
  <h1>Who's Watching?</h1>
  <button onclick="enter()">Player</button>
  <button onclick="enter()">Guest</button>
</div>

<!-- Top -->
<div id="topbar">
  <button onclick="schoolMode()">📚 School Mode</button>
  <button onclick="toggleMusic()">🎧 Music</button>
</div>

<h1 style="text-align:center;">🌌 Peak Hub</h1>

<input id="search" placeholder="Search..." onkeyup="search()">

<!-- 🎬 Movies -->
<div class="row">
  <h2>🔥 Movies</h2>
  <div class="scroll">

    <div class="card" data-name="spiderman" onclick="play('t06RUxPbp_c')">
      <img src="https://image.tmdb.org/t/p/w500/8UlWHLMpgZm9bx6QYh0NFoq67TZ.jpg">
    </div>

    <div class="card" data-name="avengers" onclick="play('EXeTwQWrcwY')">
      <img src="https://image.tmdb.org/t/p/w500/qNBAXBIQlnOThrVvA6mA2B5ggV6.jpg">
    </div>

    <div class="card" data-name="jumanji" onclick="play('2g811Eo7K8U')">
      <img src="https://image.tmdb.org/t/p/w500/9Gtg2DzBhmYamXBS1hKAhiwbBKS.jpg">
    </div>

  </div>
</div>

<!-- 📺 Shows -->
<div class="row">
  <h2>📺 Shows</h2>
  <div class="scroll">

    <div class="card" data-name="euphoria" onclick="play('UR4Pxgnm-GA')">
      <img src="https://image.tmdb.org/t/p/w500/3NTAbAiao4JLzFQw6YxP1YZppM8.jpg">
    </div>

    <div class="card" data-name="daredevil" onclick="play('sXrU1Zx7QkM')">
      <img src="https://image.tmdb.org/t/p/w500/qJ2tW6WMUDux911r6m7haRef0WH.jpg">
    </div>

  </div>
</div>

<!-- 🎮 Game -->
<div class="row">
  <h2>🎮 Game</h2>
  <iframe src="https://www.crazygames.com/embed/slope"></iframe>
</div>

<!-- 🤖 AI -->
<div class="row">
  <h2>🤖 AI Homework</h2>
  <div id="chat"></div>
  <input id="aiInput" placeholder="Ask...">
  <button onclick="askAI()">Send</button>
</div>

<!-- 🎥 Popup -->
<div id="popup">
  <span class="close" onclick="closePlayer()">✖</span>
  <iframe id="frame"></iframe>
</div>

<audio id="music" src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3"></audio>

<script>
// Unlock
function unlock(){
  if(code.value==="1234"){
    lock.style.display="none";
  }
}

// Profile
function enter(){
  profiles.style.display="none";
}

// Play
function play(id){
  popup.style.display="flex";
  frame.src="https://youtube.com/embed/"+id;
  localStorage.setItem("last",id);
}

// Close
function closePlayer(){
  popup.style.display="none";
  frame.src="";
}

// Search
function search(){
  let v=search.value.toLowerCase();
  document.querySelectorAll(".card").forEach(c=>{
    c.style.display=c.dataset.name.includes(v)?"block":"none";
  });
}

// Music
let playing=false;
function toggleMusic(){
  if(!playing){ music.play(); playing=true; }
  else{ music.pause(); playing=false; }
}

// School mode
function schoolMode(){
  document.body.innerHTML="<h1 style='color:black'>Google Classroom</h1>";
}

// Continue
window.onload=()=>{
  let last=localStorage.getItem("last");
  if(last) play(last);
}

// Fake AI (hook ready)
function askAI(){
  let input=aiInput.value;
  chat.innerHTML += "<p>You: "+input+"</p>";
  chat.innerHTML += "<p>AI: Working on it...</p>";
  aiInput.value="";
}
</script>

</body>
</html>
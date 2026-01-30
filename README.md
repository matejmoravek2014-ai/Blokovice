<!DOCTYPE html>
<html lang="cs">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Blokovice | Minecraft Portál</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;800&display=swap" rel="stylesheet">

<style>
:root{--primary:#00ff88;--bg:#0f1011;--card:#191b1d;--text:#e0e0e0}
body{margin:0;font-family:Poppins,sans-serif;background:var(--bg);color:var(--text)}
nav{position:fixed;top:0;width:100%;background:#0f1011f0;padding:18px 0;border-bottom:1px solid #222}
.nav-content{display:flex;justify-content:center;gap:30px}
.nav-content a{color:white;text-decoration:none;font-weight:600}
header{height:100vh;display:flex;flex-direction:column;justify-content:center;align-items:center;text-align:center}
h1{font-size:5rem}
.btn-copy{background:var(--primary);border:none;padding:20px 40px;border-radius:50px;font-weight:800}
section{padding:120px 20px;max-width:1100px;margin:auto}
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(300px,1fr));gap:30px}
.card{background:var(--card);padding:30px;border-radius:20px}
.chat-window{background:black;border-radius:20px;height:400px;display:flex;flex-direction:column}
#messages{flex:1;padding:15px;overflow-y:auto}
.msg{background:#111;padding:10px;border-left:4px solid var(--primary);margin-bottom:8px}
.chat-input{display:flex;gap:10px;padding:10px}
.chat-input input{flex:1;background:#151515;border:1px solid #333;color:white;padding:10px}
</style>
</head>

<body>

<nav>
<div class="nav-content">
<a href="#">DOMŮ</a>
<a href="#chat">CHAT</a>
</div>
</nav>

<header>
<h1>BLOKOVICE</h1>
<button class="btn-copy" onclick="copyIP()">KOPÍROVAT IP</button>
</header>

<section id="chat">
<h2>LIVE CHAT</h2>

<div class="chat-window">
<div id="messages"></div>

<div class="chat-input">
<input id="nick" placeholder="Jméno">
<input id="text" placeholder="Zpráva">
<button onclick="sendMessage()">POSLAT</button>
</div>
</div>
</section>

<script type="module">

import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
import { getDatabase, ref, push, onChildAdded } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

/* 🔴 SEM VLOŽ SVŮJ FIREBASE CONFIG */
const firebaseConfig = {
 apiKey: "SEM_DOPLN",
 authDomain: "SEM_DOPLN",
 databaseURL: "SEM_DOPLN",
 projectId: "SEM_DOPLN",
 storageBucket: "SEM_DOPLN",
 messagingSenderId: "SEM_DOPLN",
 appId: "SEM_DOPLN"
};
/* 🔴 KONEC CONFIGU */

const app = initializeApp(firebaseConfig);
const db = getDatabase(app);
const chatRef = ref(db,"chat");

window.sendMessage = function(){
 const nick=document.getElementById("nick").value||"Hráč";
 const text=document.getElementById("text").value;
 if(!text)return;

 push(chatRef,{nick,text,time:Date.now()});
 document.getElementById("text").value="";
}

onChildAdded(chatRef,(snap)=>{
 const d=snap.val();
 const m=document.createElement("div");
 m.className="msg";
 m.innerHTML=`<b>${d.nick}:</b> ${d.text}`;
 document.getElementById("messages").appendChild(m);
 document.getElementById("messages").scrollTop=999999;
});

window.copyIP=function(){
navigator.clipboard.writeText("Blokovice-2.aternos.me:36662");
alert("IP zkopírována!");
}

</script>

</body>
</html>

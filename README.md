<!DOCTYPE html>
<html>
<head>
<title>For You 💖</title>

<style>
body {
  margin: 0;
  text-align: center;
  background: black;
  color: white;
  font-family: Arial;
  overflow: hidden;
}

h1 {
  margin-top: 15%;
  font-size: 40px;
}

#countdown {
  font-size: 25px;
  margin-top: 20px;
}

button {
  padding: 10px 20px;
  font-size: 18px;
  border-radius: 20px;
  border: none;
  cursor: pointer;
}

canvas {
  position: fixed;
  top: 0;
  left: 0;
}
</style>

</head>

<body>

<h1 id="typing"></h1>
<div id="countdown"></div>

<button onclick="reveal()">Open Your Gift 🎁</button>

<audio autoplay loop>
  <source src="song.mp3" type="audio/mpeg">
</audio>

<canvas id="confetti"></canvas>

<script>
// 🎯 TYPING EFFECT
let text = "Happy 18th Birthday 💖 [Samprada]";
let i = 0;
function type() {
  if (i < text.length) {
    document.getElementById("typing").innerHTML += text.charAt(i);
    i++;
    setTimeout(type, 80);
  }
}
type();

let countDate = new Date().getTime() + 5000; // 5 seconds



let x = setInterval(function() {
  let now = new Date().getTime();
  let dist = countDate - now;

  let d = Math.floor(dist / (1000*60*60*24));
  let h = Math.floor((dist % (1000*60*60*24)) / (1000*60*60));
  let m = Math.floor((dist % (1000*60*60)) / (1000*60));
  let s = Math.floor((dist % (1000*60)) / 1000);

  document.getElementById("countdown").innerHTML =
  d + "d " + h + "h " + m + "m " + s + "s ";

  if (dist < 0) {
    clearInterval(x);
    document.getElementById("countdown").innerHTML = "It's your day 🎉";
  }
}, 1000);

// 💌 SECRET MESSAGE
function reveal() {
  alert("You are one of the most special people in my life ❤️");
  startConfetti();
}

// 🎉 CONFETTI
let canvas = document.getElementById("confetti");
let ctx = canvas.getContext("2d");
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let pieces = [];

for (let i=0; i<100; i++) {
  pieces.push({
    x: Math.random()*canvas.width,
    y: Math.random()*canvas.height,
    r: Math.random()*6+2,
    d: Math.random()*100
  });
}

function draw() {
  ctx.clearRect(0,0,canvas.width,canvas.height);
  for (let i=0; i<pieces.length; i++) {
    let p = pieces[i];
    ctx.beginPath();
    ctx.arc(p.x, p.y, p.r, 0, Math.PI*2);
    ctx.fillStyle = "white";
    ctx.fill();
  }
  update();
}

function update() {
  for (let i=0; i<pieces.length; i++) {
    let p = pieces[i];
    p.y += Math.cos(p.d) + 1;
    if (p.y > canvas.height) {
      p.y = 0;
    }
  }
}

function startConfetti() {
  setInterval(draw, 20);
}
</script>

</body>
</html>

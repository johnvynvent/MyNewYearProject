<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Interactive New Year</title>
<style>
body {
    margin:0;
    height:100vh;
    font-family:"Segoe UI", Arial, sans-serif;
    position:relative;
    overflow:hidden;
    background: linear-gradient(180deg, #cce7ff 0%, #ffffff 100%);
    display:flex;
    justify-content:center;
    align-items:center;
}

canvas#snowCanvas, canvas#rgbCanvas {
    position:absolute;
    top:0;
    left:0;
    width:100%;
    height:100%;
    pointer-events:none;
}

.card {
    background: rgba(255, 255, 255, 0.65);
    border-radius: 24px;
    padding: 40px;
    width: 520px;
    text-align:center;
    box-shadow: 0 20px 40px rgba(0,0,0,0.2);
    opacity:0;
    transform: translateY(20px);
    transition: opacity 0.35s ease-in-out, transform 0.35s ease-in-out;
    position:relative;
    display:flex;
    flex-direction:column;
    align-items:center;
    z-index: 10;
}

.card.hidden { display:none; }

.card.opening {
    animation: fadeInZoom 1s ease forwards;
}

@keyframes fadeInZoom {
    0% { opacity:0; transform: scale(0.8);}
    100% { opacity:1; transform: scale(1);}
}

.card-image, .card-video {
    width:100%;
    height:260px;
    object-fit:cover;
    border-radius:18px;
    margin:22px 0;
}

.btn {
    padding:14px 34px;
    font-size:18px;
    border-radius:30px;
    border:none;
    cursor:pointer;
    background:#b7a58c;
    color:#fff;
    margin-top:10px;
    transition: transform 0.2s;
    position:relative;
}

.btn:hover { transform: scale(1.07); background-color:#a39179; }
.btn.previous { margin-right:auto; background-color:#8c7b65; }
.btn.previous:hover { background-color:#75624f; }

.btn-container { display:flex; justify-content:space-between; width:100%; margin-top:15px; }
.choices { display:flex; justify-content:center; gap:20px; position:relative; }

.floating-text {
    position:absolute;
    background:#ffffffcc;
    padding:18px 22px;
    border-radius:20px;
    box-shadow:0 4px 12px rgba(0,0,0,0.1);
    max-width:350px;
    font-size:18px;
    line-height:1.5;
    text-align:center;
    display:none;
    opacity:0;
    transform:translateY(20px);
    transition:opacity 0.6s ease, transform 0.6s ease;
}

.segment1 { top:5%; right:5%; }
.segment2 { top:40%; left:5%; }
.segment3 { bottom:5%; right:5%; }

</style>
</head>
<body>

<!-- Floating segments outside cards -->
<div class="floating-text segment1" id="segment1">
  Altho the previous year was filled with challenges and hardships, let me tell u how proud I am on how u managed to survive this year wonderfully!!  
  May this New Year be a chance for self-improvement and growth. Filled by challenges that can change us and surrounded by people u love dearly.
</div>
<div class="floating-text segment2" id="segment2">
  I hope this New Year is gentle to u and will treat u kindly. I hope that u're going into this year without looking back to what was and what could be.  
  Always remember that what matters is the present.
</div>
<div class="floating-text segment3" id="segment3">
  Ulitt, HAPPIII NEW YEAARR, DAISSYYY!!!!!  
</div>

<!-- Cards 1–27 individually added -->
<!-- CARD 1 -->
<div id="card1" class="card opening">
  <h1>HAPPI NEWW YEARRR, DAISY!!!</h1>
  <img src="card1.jpg" alt="Happy New Year Image" class="card-image">
  <div class="btn-container">
    <button class="btn previous" disabled>Previous</button>
    <button class="btn" onclick="goNext()">Proceed</button>
  </div>
</div>

<!-- CARD 2 -->
<div id="card2" class="card hidden">
  <img src="card1_1.jpg" alt="Happy New Year Chapters" class="card-image">
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card2','card1')">Previous</button>
    <button class="btn" onclick="toCard3()">Proceed</button>
  </div>
</div>

<!-- CARD 3 -->
<div id="card3" class="card hidden">
  <h1>Celebrate and spend this new year with me :></h1>
  <img src="card3.jpg" alt="newyearcat" class="card-image">
  <div class="choices">
    <button class="btn" onclick="chooseYes()">YESZ</button>
    <button class="btn" id="naurBtn">NAUR</button>
  </div>
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card3','card2')">Previous</button>
  </div>
</div>

<!-- CARD 4 -->
<div id="card4" class="card hidden">
  <h1>Wrong choice <br>mwhwhhahah</h1>
  <img src="card4.jpg" alt="Wrong choice image" class="card-image">
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card4','card3',true)">Previous</button>
  </div>
</div>

<!-- CARD 5 -->
<div id="card5" class="card hidden">
  <h1>Tamaaa<br>(U don’t have any other choice anyway)</h1>
  <img src="card5.jpg" alt="tama" class="card-image">
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card5','card3')">Previous</button>
    <button class="btn" onclick="toCard6()">Proceed</button>
  </div>
</div>

<!-- CARD 6 -->
<div id="card6" class="card hidden">
  <h1>One last thing before you say yes… I wanna tell u why I wanna spend this new year with u<br>(unmute moo and mute if done)</h1>
  <video class="card-video" controls autoplay muted loop playsinline preload="auto">
    <source src="card6.1vid.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card6','card5')">Previous</button>
    <button class="btn" onclick="toCard7()">Proceed</button>
  </div>
</div>

<!-- CARD 7 -->
<div id="card7" class="card hidden">
  <h1>No.1 <br>U match my energy and u don't get weirded out by me<br>(unmute moo po and mute if natapos na:>)</h1>
  <video class="card-video" controls autoplay muted loop playsinline preload="auto">
    <source src="card7vid.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card7','card6')">Previous</button>
    <button class="btn" onclick="toCard8()">Proceed</button>
  </div>
</div>

<!-- CARD 8 -->
<div id="card8" class="card hidden">
  <h1>No.2<br>U love books and poetry (iloveebookworms)</h1>
  <img src="card8.jpg" alt="Card 8 image" class="card-image">
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card8','card7')">Previous</button>
    <button class="btn" onclick="toCard9()">Proceed</button>
  </div>
</div>

<!-- CARD 9 -->
<div id="card9" class="card hidden">
  <h1>No.3<br>U’re "performative" and I adore that (sipsipmatcha)</h1>
  <img src="card9.jpg" alt="Card 9 image" class="card-image">
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card9','card8')">Previous</button>
    <button class="btn" onclick="toCard10()">Proceed</button>
  </div>
</div>

<!-- CARD 10 -->
<div id="card10" class="card hidden">
  <h1>No.4<br>Altho this is superficial, one thing I like most are ur gorgeous eyes. Hypnotize me, pls pull me into ur world</h1>
  <img src="card10.jpg" alt="Card 10 image" class="card-image">
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card10','card9')">Previous</button>
    <button class="btn" onclick="toCard11()">Proceed</button>
  </div>
</div>

<!-- CARD 11 -->
<div id="card11" class="card hidden">
  <h1>No.5<br>I love how u smile at me whenever I try to talk to you</h1>
  <img src="card11.jpg" alt="Card 11 image" class="card-image">
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card11','card10')">Previous</button>
    <button class="btn" onclick="toCard12()">Proceed</button>
  </div>
</div>

<!-- CARD 12 -->
<div id="card12" class="card hidden">
  <h1>No.6<br>I love how u get shy when I’m near</h1>
  <img src="card12.jpg" alt="Card 12 image" class="card-image">
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card12','card11')">Previous</button>
    <button class="btn" onclick="toCard13()">Proceed</button>
  </div>
</div>

<!-- CARD 13 -->
<div id="card13" class="card hidden">
  <h1>No.7<br>U were born in June, mango season peaks and I LOVEEE MANGOES</h1>
  <img src="card13.jpg" alt="Card 13 image" class="card-image">
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card13','card12')">Previous</button>
    <button class="btn" onclick="toCard14()">Proceed</button>
  </div>
</div>

<!-- CARD 14 -->
<div id="card14" class="card hidden">
  <h1>No.8<br>Summer in Europe reminds me of ur warmth</h1>
  <img src="card14.jpg" alt="Card 14 image" class="card-image">
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card14','card13')">Previous</button>
    <button class="btn" onclick="toCard15()">Proceed</button>
  </div>
</div>

<!-- CARD 15 -->
<div id="card15" class="card hidden">
  <h1>No.9<br>Ur kindness is unmatched</h1>
  <img src="card15.jpg" alt="Card 15 image" class="card-image">
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card15','card14')">Previous</button>
    <button class="btn" onclick="toCard16()">Proceed</button>
  </div>
</div>

<!-- CARD 16 -->
<div id="card16" class="card hidden">
  <h1>No.10<br>U’re very thoughtful</h1>
  <img src="card16.jpg" alt="Card 16 image" class="card-image">
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card16','card15')">Previous</button>
    <button class="btn" onclick="toCard17()">Proceed</button>
  </div>
</div>

<!-- CARD 17 -->
<div id="card17" class="card hidden">
  <h1>No.11<br>U have an amazing smile</h1>
  <img src="card17.jpg" alt="Card 17 image" class="card-image">
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card17','card16')">Previous</button>
    <button class="btn" onclick="toCard18()">Proceed</button>
  </div>
</div>

<!-- CARD 18 -->
<div id="card18" class="card hidden">
  <h1>No.12<br>U have a creative mind</h1>
  <img src="card18.jpg" alt="Card 18 image" class="card-image">
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card18','card17')">Previous</button>
    <button class="btn" onclick="toCard19()">Proceed</button>
  </div>
</div>

<!-- CARD 19 -->
<div id="card19" class="card hidden">
  <h1>No.13<br>U inspire me</h1>
  <img src="card19.jpg" alt="Card 19 image" class="card-image">
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card19','card18')">Previous</button>
    <button class="btn" onclick="toCard20()">Proceed</button>
  </div>
</div>

<!-- CARD 20 -->
<div id="card20" class="card hidden">
  <h1>No.14<br>U’re honest and trustworthy, napaka dali ko mag open up sayo and u're so comfortable to talk to</h1>
  <img src="card20.jpg" alt="Card 20 image" class="card-image">
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card20','card19')">Previous</button>
    <button class="btn" onclick="toCard21()">Proceed</button>
  </div>
</div>

<!-- CARD 21 -->
<div id="card21" class="card hidden">
  <h1>No.15<br>U're such a cutiee</h1>
  <img src="card21.jpg" alt="Card 21 image" class="card-image">
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card21','card20')">Previous</button>
    <button class="btn" onclick="toCard22()">Proceed</button>
  </div>
</div>

<!-- CARD 22 -->
<div id="card22" class="card hidden">
  <h1>No.16<br>U have a warm heart</h1>
  <img src="card22.jpg" alt="Card 22 image" class="card-image">
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card22','card21')">Previous</button>
    <button class="btn" onclick="toCard23()">Proceed</button>
  </div>
</div>

<!-- CARD 23 -->
<div id="card23" class="card hidden">
  <h1>No.17<br>U’re supportive</h1>
  <img src="card23.jpg" alt="Card 23 image" class="card-image">
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card23','card22')">Previous</button>
    <button class="btn" onclick="toCard24()">Proceed</button>
  </div>
</div>

<!-- CARD 24 -->
<div id="card24" class="card hidden">
  <h1>No.18<br>U listen carefully</h1>
  <img src="card24.jpg" alt="Card 24 image" class="card-image">
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card24','card23')">Previous</button>
    <button class="btn" onclick="toCard25()">Proceed</button>
  </div>
</div>

<!-- CARD 25 -->
<div id="card25" class="card hidden">
  <h1>No.19<br>U have a beautiful personality</h1>
  <img src="card25.jpg" alt="Card 25 image" class="card-image">
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card25','card24')">Previous</button>
    <button class="btn" onclick="toCard26()">Proceed</button>
  </div>
</div>

<!-- CARD 26 -->
<div id="card26" class="card hidden">
  <h1>No.20<br>U always make me smile</h1>
  <img src="card26.jpg" alt="Card 26 image" class="card-image">
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card26','card25')">Previous</button>
    <button class="btn" onclick="toCard27()">Proceed</button>
  </div>
</div>

<!-- CARD 27 -->
<div id="card27" class="card hidden">
  <h1>No.21 Finally…<br>I'll just leave this empty muna in case I get to know u better. There's still so many things that I don't know about u and I'll keep on loving the idea of getting to know u better, pls don't explode at the meantime... U are simply amazing, Daisy!</h1>
  <img src="card27.jpg" alt="Card 27 image" class="card-image">
  <div class="btn-container">
    <button class="btn previous" onclick="switchCard('card27','card26')">Previous</button>
  </div>
</div>

<!-- Snow and RGB sparkles canvas -->
<canvas id="snowCanvas"></canvas>
<canvas id="rgbCanvas"></canvas>

<script>
let naurClickCount=0;
const naurBtn=document.getElementById('naurBtn');

if(naurBtn){
  naurBtn.addEventListener('click',()=>{
    naurClickCount++;
    if(naurClickCount<4){
      naurBtn.style.position='fixed';
      naurBtn.style.top=Math.random()*80+'%';
      naurBtn.style.left=Math.random()*80+'%';
    } else {
      naurClickCount=0;
      naurBtn.style.position='static';
      chooseNaur();
    }
  });
}

function switchCard(from,to,fromCard4=false){
  const f=document.getElementById(from), t=document.getElementById(to);

  // Hide NAUR button when returning from card4
  if(from==='card4' && to==='card3'){
    naurBtn.style.display='none';
  }
  // Show NAUR button only when coming from card2
  if(from==='card2' && to==='card3'){
    naurBtn.style.display='inline-block';
  }

  if(from==='card2'){
    document.getElementById("segment1").style.display='none';
    document.getElementById("segment2").style.display='none';
    document.getElementById("segment3").style.display='none';
  }

  f.style.opacity=0;
  setTimeout(()=>{
    f.classList.add("hidden");
    t.classList.remove("hidden");
    t.style.opacity=1;
    t.style.transform="translateY(0)";
  },350);
}

// Floating segments animation
function animateSegment(id, delay){ 
  const el=document.getElementById(id);
  el.style.display="block";
  setTimeout(()=>{ el.style.opacity=1; el.style.transform="translateY(0)"; }, delay); 
}

function goNext(){
  switchCard("card1","card2");
  animateSegment("segment1",500);
  animateSegment("segment2",2500);
  animateSegment("segment3",4500);
}

function toCard3(){ switchCard("card2","card3"); }
function toCard6(){ switchCard("card5","card6"); }
function toCard7(){ switchCard("card6","card7"); }
function toCard8(){ switchCard("card7","card8"); }
function toCard9(){ switchCard("card8","card9"); }
function toCard10(){ switchCard("card9","card10"); }
function toCard11(){ switchCard("card10","card11"); }
function toCard12(){ switchCard("card11","card12"); }
function toCard13(){ switchCard("card12","card13"); }
function toCard14(){ switchCard("card13","card14"); }
function toCard15(){ switchCard("card14","card15"); }
function toCard16(){ switchCard("card15","card16"); }
function toCard17(){ switchCard("card16","card17"); }
function toCard18(){ switchCard("card17","card18"); }
function toCard19(){ switchCard("card18","card19"); }
function toCard20(){ switchCard("card19","card20"); }
function toCard21(){ switchCard("card20","card21"); }
function toCard22(){ switchCard("card21","card22"); }
function toCard23(){ switchCard("card22","card23"); }
function toCard24(){ switchCard("card23","card24"); }
function toCard25(){ switchCard("card24","card25"); }
function toCard26(){ switchCard("card25","card26"); }
function toCard27(){ switchCard("card26","card27"); }

function chooseYes(){ switchCard("card3","card5"); }
function chooseNaur(){ switchCard("card3","card4"); }

// Snow and RGB sparkles
function startEffects(){
  const snowCanvas=document.getElementById('snowCanvas');
  const ctx=snowCanvas.getContext('2d');
  snowCanvas.width=window.innerWidth;
  snowCanvas.height=window.innerHeight;

  const rgbCanvas=document.getElementById('rgbCanvas');
  const ctxRGB=rgbCanvas.getContext('2d');
  rgbCanvas.width=window.innerWidth;
  rgbCanvas.height=window.innerHeight;

  const numFlakes=150;
  const flakes=[];
  for(let i=0;i<numFlakes;i++){
    flakes.push({x:Math.random()*snowCanvas.width, y:Math.random()*snowCanvas.height, r:Math.random()*4+1, d:Math.random()*1});
  }

  const numSparks=25;
  const sparks=[];
  for(let i=0;i<numSparks;i++){
    sparks.push({x:Math.random()*rgbCanvas.width, y:Math.random()*rgbCanvas.height, r:Math.random()*2+1, color:`rgb(${Math.floor(Math.random()*255)},${Math.floor(Math.random()*255)},${Math.floor(Math.random()*255)})`});
  }

  function draw(){
    ctx.clearRect(0,0,snowCanvas.width,snowCanvas.height);
    for(let i=0;i<numFlakes;i++){
      ctx.beginPath();
      ctx.arc(flakes[i].x,flakes[i].y,flakes[i].r,0,Math.PI*2);
      ctx.fillStyle='white';
      ctx.fill();
      flakes[i].y+=Math.sqrt(flakes[i].r)*0.5;
      flakes[i].x+=Math.sin(flakes[i].d);
      if(flakes[i].y>snowCanvas.height){ flakes[i].y=0; flakes[i].x=Math.random()*snowCanvas.width; }
    }

    ctxRGB.clearRect(0,0,rgbCanvas.width,rgbCanvas.height);
    for(let i=0;i<numSparks;i++){
      ctxRGB.beginPath();
      ctxRGB.arc(sparks[i].x,sparks[i].y,sparks[i].r,0,Math.PI*2);
      ctxRGB.fillStyle=sparks[i].color;
      ctxRGB.fill();
      if(Math.random()<0.01){
        sparks[i].x=Math.random()*rgbCanvas.width;
        sparks[i].y=Math.random()*rgbCanvas.height;
        sparks[i].color=`rgb(${Math.floor(Math.random()*255)},${Math.floor(Math.random()*255)},${Math.floor(Math.random()*255)})`;
      }
    }

    requestAnimationFrame(draw);
  }

  draw();
}

window.addEventListener('load', startEffects);
</script>
</body>
</html>

<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>Tsalhou</title>
<style>
  html, body {
    margin: 0;
    padding: 0;
    width: 100%;
    height: 100%;
    font-family: Arial, sans-serif;
  }
  #container {
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 100vw;
    height: 100vh;
    text-align: center;
    gap: 2rem;
    background: #FAECE7;
    overflow: hidden;
  }
  #heartsLayer {
    position: absolute;
    inset: 0;
    pointer-events: none;
  }
  #question {
    position: relative;
    font-size: 42px;
    font-weight: 500;
    margin: 0;
    color: #993C1D;
  }
  #btns {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 28px;
    flex-wrap: wrap;
  }
  button {
    cursor: pointer;
    border-radius: 32px;
    font-size: 24px;
  }
  #yesBtn {
    background: #D4537E;
    color: #FBEAF0;
    border: none;
    padding: 20px 44px;
    font-weight: 500;
    transition: font-size 0.2s, padding 0.2s;
  }
  #noBtn {
    background: transparent;
    border: 1px solid #D85A30;
    color: #993C1D;
    padding: 20px 44px;
  }
</style>
</head>
<body>
<div id="container">
  <div id="heartsLayer"></div>
  <svg id="moon" width="70" height="70" viewBox="0 0 64 64" style="position:absolute; top:8%; left:10%; opacity:0.9;">
    <path d="M40 8 C24 8 12 20 12 36 C12 52 24 64 40 64 C28 60 20 48 20 34 C20 20 28 10 40 8 Z" fill="#EF9F27"/>
  </svg>
  <svg id="roseLeft" width="60" height="60" viewBox="0 0 64 64" style="position:absolute; bottom:6%; left:6%;">
    <circle cx="32" cy="26" r="14" fill="#D4537E"/>
    <circle cx="32" cy="26" r="9" fill="#993556"/>
    <path d="M32 40 C32 52 24 56 20 60" stroke="#3B6D11" stroke-width="4" fill="none" stroke-linecap="round"/>
    <ellipse cx="24" cy="50" rx="7" ry="4" fill="#639922" transform="rotate(-30 24 50)"/>
  </svg>
  <svg id="roseRight" width="60" height="60" viewBox="0 0 64 64" style="position:absolute; bottom:6%; right:6%;">
    <circle cx="32" cy="26" r="14" fill="#D4537E"/>
    <circle cx="32" cy="26" r="9" fill="#993556"/>
    <path d="M32 40 C32 52 40 56 44 60" stroke="#3B6D11" stroke-width="4" fill="none" stroke-linecap="round"/>
    <ellipse cx="40" cy="50" rx="7" ry="4" fill="#639922" transform="rotate(30 40 50)"/>
  </svg>
  <p id="question">Wach bghiti ntsalhou?</p>
  <div id="btns">
    <button id="yesBtn">Yes</button>
    <button id="noBtn">No</button>
  </div>
</div>
<script>
const heartsLayer = document.getElementById('heartsLayer');
const heartSVG = '<svg width="100%" height="100%" viewBox="0 0 32 32"><path d="M16 28 C4 20 2 12 8 8 C12 5 16 8 16 12 C16 8 20 5 24 8 C30 12 28 20 16 28 Z" fill="#D4537E"/></svg>';
function spawnHeart(){
  const h = document.createElement('div');
  h.innerHTML = heartSVG;
  const size = 20 + Math.random() * 30;
  h.style.position = 'absolute';
  h.style.width = size + 'px';
  h.style.height = size + 'px';
  h.style.left = Math.random() * 92 + '%';
  h.style.bottom = '-20px';
  h.style.opacity = '0.85';
  h.style.transition = 'transform 4s linear, opacity 4s linear';
  heartsLayer.appendChild(h);
  requestAnimationFrame(function(){
    h.style.transform = 'translateY(-' + (window.innerHeight + 100) + 'px)';
    h.style.opacity = '0';
  });
  setTimeout(function(){ h.remove(); }, 4200);
}
setInterval(spawnHeart, 300);
for (let i = 0; i < 10; i++) { setTimeout(spawnHeart, i * 100); }
let noClicks = 0;
const noBtn = document.getElementById('noBtn');
const yesBtn = document.getElementById('yesBtn');
const question = document.getElementById('question');
const btns = document.getElementById('btns');
function finish(msg){
  question.textContent = msg;
  btns.style.display = 'none';
}
noBtn.addEventListener('click', function(){
  noClicks++;
  if (noClicks >= 5) {
    finish('Safi, tsalehna! 😂');
    return;
  }
  const newSize = 24 + noClicks * 9;
  const newPad = 20 + noClicks * 6;
  yesBtn.style.fontSize = newSize + 'px';
  yesBtn.style.padding = newPad + 'px ' + (newPad + 22) + 'px';
});
yesBtn.addEventListener('click', function(){
  finish('Safi, tsalehna! 😂');
});
</script>
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Happy Birthday, My Love 💖</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&family=Great+Vibes&display=swap" rel="stylesheet">
  <style>
    :root{
      --bg1:#ff9a9e;
      --bg2:#fad0c4;
      --accent:#ff6b6b;
      --card:#ffffffee;
      --text:#2d2a32;
    }
    *{box-sizing:border-box}
    html,body{height:100%;}
    body{
      margin:0;
      font-family:"Poppins", sans-serif;
      color:var(--text);
      background: linear-gradient(135deg,var(--bg1),var(--bg2));
      overflow-x:hidden;
    }
    .wrap{
      min-height:100vh;
      display:grid;
      place-items:center;
      padding:24px;
      position:relative;
      isolation:isolate;
    }
    .card{
      width:min(1580px, 92vw);
      background:var(--card);
      border-radius:28px;
      box-shadow:0 20px 60px rgba(0,0,0,.15);
      padding:28px;
      backdrop-filter: blur(6px);
    }
    .top{
      display:flex;
      flex-wrap:wrap;
      gap:24px;
      align-items:center;
      justify-content:center;
    }
    .photo{
      width:572px; height: 1280px;
      border-radius:24px;
      overflow:hidden;
      box-shadow:0 12px 30px rgba(0,0,0,.18);
    }
    .photo img{width:100%; height:100%; object-fit:cover;}
    .text{
      flex:1 1 320px;
      padding:10px 6px;
    }
    h1{
      margin:0 0 10px;
      font-family:"Great Vibes", cursive;
      font-size: clamp(40px, 6vw, 68px);
      color:#d7263d;
      text-shadow:0 3px 0 rgba(0,0,0,.06);
    }
    h2{
      margin:14px 0 22px;
      font-size: clamp(18px, 3.2vw, 24px);
      font-weight:600;
      color:#444;
    }
    p{
      margin:0 0 14px;
      font-size: clamp(15px, 2.6vw, 18px);
    }
    .btns{
      display:flex; gap:12px; flex-wrap:wrap; margin-top:10px;
    }
    button{
      border:0; padding:12px 18px; border-radius:999px; font-weight:600; cursor:pointer;
      box-shadow:0 8px 20px rgba(0,0,0,.12);
      transition: transform .08s ease, box-shadow .2s ease;
    }
    .primary{ background:var(--accent); color:#fff; }
    .ghost{ background:#fff; color:#d7263d; }
    button:active{ transform: translateY(1px); box-shadow:0 4px 10px rgba(0,0,0,.14); }
    .audio-bar{ margin-top:16px; background:#fff; border-radius:14px; padding:8px 10px; }
    audio{ width:100%; height:40px; }
    .footer{
      margin-top:18px; font-size:14px; opacity:.7; text-align:center;
    }
    .hearts{ position:fixed; inset:0; pointer-events:none; z-index:-1; }
    .heart{ position:absolute; font-size:14px; animation: floatUp linear forwards; opacity:.9; }
    @keyframes floatUp{
      from{ transform: translateY(0) scale(1) rotate(0); opacity:.95; }
      to{ transform: translateY(-120vh) scale(1.6) rotate(180deg); opacity:0; }
    }
    .confetti{ position:fixed; inset:0; pointer-events:none; overflow:hidden; z-index:50; }
    .confetti-piece{ position:absolute; width:10px; height:16px; top:-20px; opacity:.9; animation: fall linear forwards; }
    @keyframes fall{ to{ transform: translateY(120vh) rotate(720deg); opacity:.95;} }
    @media (max-width:480px){
      .photo{ width:572px; height:1280px; border-radius:20px; }
      .card{ padding:22px; border-radius:22px; }
    }
  </style>
</head>
<body>
  <div class="wrap">
    <div class="hearts" id="hearts"></div>
    <div class="confetti" id="confetti"></div>

    <div class="card">
      <div class="top">
        <figure class="photo">
          <img src="maggie.jpg" alt="My Love" />
        </figure>
        <div class="text">
          <h1>Happy Birthday, My Maggie! 💕</h1>
          <h2>To: <span id="toName">My Maggie</span> • From: <span id="fromName">Your Suraj</span></h2>
          <p>
            On your special day, I just want to remind you how deeply you are loved.
            Your smile lights up my world, and every moment with you is my favorite.
            Here's to more laughter, more adventures, and a lifetime of us. 💖
          </p>
          <div class="btns">
            <button class="primary" id="playBtn">Play our song ▶</button>
            <button class="ghost" id="confettiBtn">Celebrate 🎉</button>
          </div>
          <div class="audio-bar">
            <audio id="song" src="music.mp3" preload="auto" autoplay></audio>
          </div>
          <div class="footer">Made with love ❤️ and a little bit of magic.</div>
        </div>
      </div>
    </div>
  </div>

  <script>
    // Personalize
    const TO_NAME = "My Maggie";
    const FROM_NAME = "Your Suraj";
    document.getElementById("toName").textContent = TO_NAME;
    document.getElementById("fromName").textContent = FROM_NAME;

    // Audio controls
    const song = document.getElementById('song');
    const playBtn = document.getElementById('playBtn');
    playBtn.addEventListener('click', async () => {
      try {
        if (song.paused) {
          await song.play();
          playBtn.textContent = 'Pause ⏸';
          burstConfetti(120);
        } else {
          song.pause();
          playBtn.textContent = 'Play our song ▶';
        }
      } catch (e) {
        alert('Please click anywhere first to allow audio playback.');
      }
    });

    // Confetti
    document.getElementById('confettiBtn').addEventListener('click', () => burstConfetti(160));

    // Hearts background
    const hearts = document.getElementById('hearts');
    const heartChars = ['❤','💖','💗','💓','💞','💘'];
    setInterval(() => {
      const h = document.createElement('div');
      h.className = 'heart';
      h.textContent = heartChars[Math.floor(Math.random()*heartChars.length)];
      h.style.left = Math.random()*100 + 'vw';
      h.style.animationDuration = (6 + Math.random()*6) + 's';
      h.style.fontSize = (12 + Math.random()*22) + 'px';
      hearts.appendChild(h);
      setTimeout(() => h.remove(), 14000);
    }, 600);

    // Confetti generator
    const confetti = document.getElementById('confetti');
    function burstConfetti(count = 120){
      for(let i=0;i<count;i++){
        const piece = document.createElement('div');
        piece.className = 'confetti-piece';
        piece.style.left = Math.random()*100 + 'vw';
        piece.style.background = `hsl(${Math.random()*360}, 90%, 60%)`;
        piece.style.transform = `translateY(-20px) rotate(${Math.random()*360}deg)`;
        piece.style.animationDuration = (4 + Math.random()*3) + 's';
        piece.style.width = (6 + Math.random()*8) + 'px';
        piece.style.height = (10 + Math.random()*14) + 'px';
        piece.style.borderRadius = Math.random() > 0.5 ? '2px' : '999px';
        confetti.appendChild(piece);
        setTimeout(() => piece.remove(), 8000);
      }
    }
  </script>
</body>
</html>

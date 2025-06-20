<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Happy 16th Birthday Aaru</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      background: linear-gradient(to right, #ffdde1, #ee9ca7);
      font-family: 'Segoe UI', sans-serif;
      color: #333;
      text-align: center;
      overflow-x: hidden;
    }

    h1 {
      margin-top: 40px;
      font-size: 2.8rem;
      color: #d6336c;
      animation: pulse 2s infinite;
    }

    p {
      max-width: 600px;
      margin: 20px auto;
      font-size: 1.2rem;
      line-height: 1.6;
    }

    .game-container {
      margin-top: 40px;
    }

    .heart {
      position: absolute;
      width: 30px;
      height: 30px;
      background: url('https://cdn-icons-png.flaticon.com/512/833/833472.png') no-repeat center;
      background-size: contain;
      cursor: pointer;
      animation: fall 5s linear infinite;
    }

    @keyframes fall {
      0% { top: -40px; }
      100% { top: 100vh; }
    }

    @keyframes pulse {
      0% { transform: scale(1); }
      50% { transform: scale(1.05); }
      100% { transform: scale(1); }
    }

    #score {
      font-size: 1.5rem;
      font-weight: bold;
    }

    #finalMessage {
      display: none;
      margin-top: 40px;
      font-size: 1.4rem;
      color: #444;
    }

    canvas {
      position: fixed;
      top: 0;
      left: 0;
      pointer-events: none;
      z-index: 0;
    }
  </style>
</head>
<body>
  <canvas id="confetti-canvas"></canvas>

  <h1>Happy 16th Birthday, Aaru! 🎉</h1>

  <p>
    I may no longer be the one standing beside you, but that doesn’t change the fact that today is a special day — your sweet sixteen.  
    Thank you for the memories. I hope this little surprise brings a smile to your face. You deserve all the happiness in the world.
  </p>

  <div class="game-container">
    <h2>🎮 Catch the Hearts Game</h2>
    <p>Tap the falling hearts! Catch 10 to unlock a final message 💖</p>
    <div id="score">Score: 0</div>
  </div>

  <div id="finalMessage">
    💌 You've caught 10 hearts!  
    <br/>No matter where life takes us, you’ll always be someone I once cared for deeply.  
    <br/><strong>Happy Sweet 16, Aaru.</strong>
  </div>

  <script>
    let score = 0;

    function createHeart() {
      const heart = document.createElement('div');
      heart.classList.add('heart');
      heart.style.left = Math.random() * 90 + "vw";
      document.body.appendChild(heart);

      heart.addEventListener('click', () => {
        score++;
        document.getElementById('score').innerText = `Score: ${score}`;
        heart.remove();

        if (score === 10) {
          document.getElementById('finalMessage').style.display = 'block';
        }
      });

      setTimeout(() => {
        heart.remove();
      }, 6000);
    }

    setInterval(createHeart, 800);
  </script>

  <script>
    // Confetti animation
    const canvas = document.getElementById('confetti-canvas');
    const ctx = canvas.getContext('2d');
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    let particles = [];

    for (let i = 0; i < 100; i++) {
      particles.push({
        x: Math.random() * canvas.width,
        y: Math.random() * canvas.height,
        r: Math.random() * 4 + 1,
        d: Math.random() * 100
      });
    }

    function draw() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      ctx.fillStyle = "#fff";
      ctx.beginPath();
      for (let i = 0; i < particles.length; i++) {
        let p = particles[i];
        ctx.moveTo(p.x, p.y);
        ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2, true);
      }
      ctx.fill();
      update();
    }

    let angle = 0;
    function update() {
      angle += 0.01;
      for (let i = 0; i < particles.length; i++) {
        let p = particles[i];
        p.y += Math.cos(angle + p.d) + 1 + p.r / 2;
        p.x += Math.sin(angle) * 2;

        if (p.y > canvas.height) {
          particles[i] = {
            x: Math.random() * canvas.width,
            y: 0,
            r: p.r,
            d: p.d
          };
        }
      }
    }

    setInterval(draw, 33);
  </script>
</body>
</html>

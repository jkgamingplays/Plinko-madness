<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Plinko Madness - PLINK ME FOR CASH</title>
  <style>
    body {
      background-color: #111;
      color: limegreen;
      font-family: 'Courier New', Courier, monospace;
      text-align: center;
      padding-top: 20px;
    }

    #plinkButton {
      font-size: 24px;
      padding: 10px 20px;
      margin-bottom: 20px;
      background: linear-gradient(to right, #00ffcc, #ff00cc);
      border: none;
      border-radius: 10px;
      color: black;
      font-weight: bold;
      cursor: pointer;
      box-shadow: 0 0 10px lime;
      animation: wiggle 1s infinite alternate;
    }

    @keyframes wiggle {
      from { transform: rotate(-2deg); }
      to { transform: rotate(2deg); }
    }

    canvas {
      background-color: #222;
      border: 2px solid limegreen;
    }
  </style>
</head>
<body>
  <h1>Plinko Madness</h1>
  <p>Drop a ball and support the madness!</p>

  <!-- PLINK ME BUTTON OF LEGEND -->
  <button id="plinkButton">PLINK ME!</button>

  <!-- Plinko Canvas -->
  <canvas id="plinkoCanvas" width="400" height="600"></canvas>

  <!-- The Chaos JS -->
  <script>
    const canvas = document.getElementById("plinkoCanvas");
    const ctx = canvas.getContext("2d");
    const pegs = [];
    const balls = [];

    document.getElementById("plinkButton").addEventListener("click", () => {
      dropBall(); // Immediate chaos
      setTimeout(() => {
        window.open("https://paypal.me/qmeeboss4900/1", "_blank");
      }, 500); // Chaos delay
    });

    function createPegs() {
      const rows = 10;
      const spacing = 40;
      for (let y = spacing; y < canvas.height - 100; y += spacing) {
        for (let x = (y / spacing) % 2 === 0 ? spacing : spacing * 1.5; x < canvas.width; x += spacing * 2) {
          pegs.push({ x, y });
        }
      }
    }

    function dropBall() {
      balls.push({
        x: canvas.width / 2,
        y: 0,
        radius: 5,
        vx: 0,
        vy: 2
      });
    }

    function draw() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);

      // Draw pegs
      ctx.fillStyle = "white";
      for (const peg of pegs) {
        ctx.beginPath();
        ctx.arc(peg.x, peg.y, 5, 0, Math.PI * 2);
        ctx.fill();
      }

      // Draw balls
      for (const ball of balls) {
        ball.vy += 0.1;
        ball.x += ball.vx;
        ball.y += ball.vy;

        for (const peg of pegs) {
          const dx = peg.x - ball.x;
          const dy = peg.y - ball.y;
          const dist = Math.sqrt(dx * dx + dy * dy);
          if (dist < 10) {
            ball.vx += (Math.random() - 0.5) * 2;
            ball.vy *= -0.7;
          }
        }

        if (ball.x < 0 || ball.x > canvas.width) ball.vx *= -1;

        ctx.beginPath();
        ctx.arc(ball.x, ball.y, ball.radius, 0, Math.PI * 2);
        ctx.fillStyle = "lime";
        ctx.fill();
      }

      requestAnimationFrame(draw);
    }

    createPegs();
    draw();
  </script>
</body>
</html>

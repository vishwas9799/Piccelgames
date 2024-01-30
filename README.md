<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Endless Bubble Shooter Game</title>
    <style>
        body {
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f1f1f1;
        }

        #game-container {
            text-align: center;
        }

        canvas {
            border: 2px solid #333;
        }
    </style>
</head>
<body>
    <div id="game-container">
        <canvas id="gameCanvas" width="480" height="640"></canvas>
    </div>
    <script>
        window.onload = function () {
            const canvas = document.getElementById("gameCanvas");
            const ctx = canvas.getContext("2d");
            const bubbleRadius = 20;
            const bubbleColors = ["red", "green", "blue", "yellow", "purple", "orange"];

            let bubbles = [];
            let shooter = { x: canvas.width / 2, y: canvas.height - bubbleRadius, color: bubbleColors[0] };
            let isGameRunning = true;

            function createBubbles() {
                const row = Math.floor(Math.random() * 5);
                const col = Math.floor(Math.random() * 8);
                const x = col * 60 + 30;
                const y = row * 60 + 30;
                const color = bubbleColors[Math.floor(Math.random() * bubbleColors.length)];
                bubbles.push({ x, y, color });
            }

            function drawBubbles() {
                ctx.clearRect(0, 0, canvas.width, canvas.height);

                bubbles.forEach(bubble => {
                    ctx.beginPath();
                    ctx.arc(bubble.x, bubble.y, bubbleRadius, 0, Math.PI * 2);
                    ctx.fillStyle = bubble.color;
                    ctx.fill();
                    ctx.strokeStyle = "#333";
                    ctx.stroke();
                    ctx.closePath();
                });
            }

            function drawShooter() {
                ctx.beginPath();
                ctx.arc(shooter.x, shooter.y, bubbleRadius, 0, Math.PI * 2);
                ctx.fillStyle = shooter.color;
                ctx.fill();
                ctx.strokeStyle = "#333";
                ctx.stroke();
                ctx.closePath();
            }

            function updateGame() {
                if (isGameRunning) {
                    createBubbles();
                    drawBubbles();
                    drawShooter();
                }

                requestAnimationFrame(updateGame);
            }

            function shootBubble() {
                if (isGameRunning) {
                    bubbles.pop(); // Remove the top bubble
                }
            }

            // Handle player input for shooting
            document.addEventListener('keydown', (event) => {
                if (event.key === ' ') {
                    shootBubble();
                }
            });

            // Start the game loop when the window is fully loaded
            updateGame();
        };
    </script>
</body>
</html>

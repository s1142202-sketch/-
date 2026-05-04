<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>地鐵衝刺 - 跑酷遊戲</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f3460 100%);
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            overflow: hidden;
        }
        .game-container {
            position: relative;
            border: 4px solid #e94560;
            border-radius: 12px;
            box-shadow: 0 0 40px rgba(233, 69, 96, 0.4);
        }
        canvas {
            display: block;
            background: linear-gradient(180deg, #2d2d44 0%, #1a1a2e 100%);
        }
        .ui-overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
        }
        .score-display {
            position: absolute;
            top: 20px;
            left: 20px;
            color: #fff;
            font-size: 24px;
            font-weight: bold;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
        }
        .score-display span {
            color: #ffd700;
        }
        .start-screen, .game-over-screen {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            background: rgba(0, 0, 0, 0.85);
            pointer-events: auto;
        }
        .game-over-screen {
            display: none;
        }
        .title {
            font-size: 48px;
            font-weight: bold;
            color: #e94560;
            text-shadow: 3px 3px 6px rgba(0,0,0,0.5);
            margin-bottom: 20px;
        }
        .subtitle {
            font-size: 20px;
            color: #aaa;
            margin-bottom: 40px;
        }
        .final-score {
            font-size: 32px;
            color: #ffd700;
            margin-bottom: 10px;
        }
        .high-score {
            font-size: 18px;
            color: #4ecca3;
            margin-bottom: 30px;
        }
        .btn {
            padding: 15px 50px;
            font-size: 22px;
            font-weight: bold;
            color: #fff;
            background: linear-gradient(135deg, #e94560 0%, #c73e54 100%);
            border: none;
            border-radius: 30px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 6px 20px rgba(233, 69, 96, 0.4);
            pointer-events: auto;
        }
        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 30px rgba(233, 69, 96, 0.6);
        }
        .instructions {
            margin-top: 30px;
            color: #888;
            font-size: 14px;
            text-align: center;
        }
        .instructions kbd {
            background: #333;
            padding: 4px 10px;
            border-radius: 4px;
            color: #fff;
            margin: 0 5px;
        }
    </style>
</head>
<body>
    <div class="game-container">
        <canvas id="gameCanvas" width="600" height="500"></canvas>
        <div class="ui-overlay">
            <div class="score-display">分數: <span id="score">0</span></div>
            
            <div class="start-screen" id="startScreen">
                <div class="title">地鐵衝刺</div>
                <div class="subtitle">地鐵跑酷遊戲</div>
                <button class="btn" id="startBtn">開始遊戲</button>
                <div class="instructions">
                    <kbd>←</kbd> <kbd>→</kbd> 移動<br>
                    <kbd>↑</kbd> 跳躍
                </div>
            </div>
            
            <div class="game-over-screen" id="gameOverScreen">
                <div class="title">遊戲結束</div>
                <div class="final-score">分數: <span id="finalScore">0</span></div>
                <div class="high-score">最高分: <span id="highScore">0</span></div>
                <button class="btn" id="restartBtn">再來一次</button>
            </div>
        </div>
    </div>

    <script>
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        
        const TRACK_COUNT = 3;
        const TRACK_HEIGHT = canvas.height / TRACK_COUNT;
        const PLAYER_SIZE = 50;
        const OBSTACLE_WIDTH = 60;
        const OBSTACLE_HEIGHT = 70;
        const COIN_SIZE = 30;
        
        let gameRunning = false;
        let score = 0;
        let highScore = localStorage.getItem('subwayRunnerHighScore') || 0;
        let gameSpeed = 5;
        let animationId;
        
        const player = {
            track: 1,
            x: 80,
            y: 0,
            jumping: false,
            jumpVelocity: 0,
            jumpHeight: 0,
            maxJumpHeight: 120,
            grounded: true,
            width: PLAYER_SIZE,
            height: PLAYER_SIZE
        };
        
        let obstacles = [];
        let coins = [];
        let particles = [];
        
        const keys = {
            left: false,
            right: false,
            up: false
        };
        
        function updatePlayerY() {
            player.y = player.track * TRACK_HEIGHT + (TRACK_HEIGHT - player.height) / 2;
        }
        
        function drawBackground() {
            const gradient = ctx.createLinearGradient(0, 0, 0, canvas.height);
            gradient.addColorStop(0, '#1a1a2e');
            gradient.addColorStop(1, '#0f0f1a');
            ctx.fillStyle = gradient;
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            ctx.strokeStyle = 'rgba(233, 69, 96, 0.3)';
            ctx.lineWidth = 2;
            for (let i = 1; i < TRACK_COUNT; i++) {
                const y = i * TRACK_HEIGHT;
                ctx.beginPath();
                ctx.moveTo(0, y);
                ctx.lineTo(canvas.width, y);
                ctx.stroke();
            }
            
            ctx.fillStyle = 'rgba(233, 69, 96, 0.1)';
            for (let i = 0; i < TRACK_COUNT; i++) {
                const y = i * TRACK_HEIGHT + TRACK_HEIGHT / 2;
                ctx.fillRect(0, y - 30, canvas.width, 60);
            }
            
            for (let i = 0; i < 20; i++) {
                const x = (Date.now() / 10 + i * 100) % (canvas.width + 100) - 50;
                const y = (i * 37) % canvas.height;
                ctx.fillStyle = 'rgba(255, 255, 255, 0.3)';
                ctx.beginPath();
                ctx.arc(x, y, 1, 0, Math.PI * 2);
                ctx.fill();
            }
        }
        
        function drawPlayer() {
            const drawY = player.y + player.jumpHeight;
            
            ctx.save();
            ctx.translate(player.x + player.width / 2, drawY + player.height / 2);
            
            ctx.fillStyle = '#e94560';
            ctx.beginPath();
            ctx.ellipse(0, 5, player.width / 2, player.height / 2 - 5, 0, 0, Math.PI * 2);
            ctx.fill();
            
            ctx.fillStyle = '#ffdbac';
            ctx.beginPath();
            ctx.arc(0, -10, 18, 0, Math.PI * 2);
            ctx.fill();
            
            ctx.fillStyle = '#2d2d44';
            ctx.fillRect(-12, -25, 24, 8);
            
            ctx.fillStyle = '#fff';
            ctx.beginPath();
            ctx.arc(-5, -12, 4, 0, Math.PI * 2);
            ctx.arc(5, -12, 4, 0, Math.PI * 2);
            ctx.fill();
            
            ctx.fillStyle = '#000';
            ctx.beginPath();
            ctx.arc(-4, -12, 2, 0, Math.PI * 2);
            ctx.arc(6, -12, 2, 0, Math.PI * 2);
            ctx.fill();
            
            if (player.jumping) {
                ctx.fillStyle = '#c73e54';
                ctx.fillRect(-8, -5, 16, 15);
            } else {
                ctx.fillStyle = '#e94560';
                ctx.fillRect(-12, 0, 10, 20);
                ctx.fillRect(2, 0, 10, 20);
            }
            
            ctx.restore();
        }
        
        function drawObstacle(obstacle) {
            ctx.save();
            ctx.translate(obstacle.x + OBSTACLE_WIDTH / 2, obstacle.y + OBSTACLE_HEIGHT / 2);
            
            ctx.fillStyle = '#4a4a6a';
            ctx.fillRect(-OBSTACLE_WIDTH / 2 + 5, -OBSTACLE_HEIGHT / 2 + 5, OBSTACLE_WIDTH - 10, OBSTACLE_HEIGHT - 10);
            
            const gradient = ctx.createLinearGradient(-OBSTACLE_WIDTH / 2, 0, OBSTACLE_WIDTH / 2, 0);
            gradient.addColorStop(0, '#ff6b6b');
            gradient.addColorStop(0.5, '#ee5a5a');
            gradient.addColorStop(1, '#ff6b6b');
            ctx.fillStyle = gradient;
            ctx.fillRect(-OBSTACLE_WIDTH / 2, -OBSTACLE_HEIGHT / 2, OBSTACLE_WIDTH - 10, OBSTACLE_HEIGHT - 10);
            
            ctx.fillStyle = '#ffeaa7';
            ctx.fillRect(-20, -20, 15, 15);
            ctx.fillRect(5, -20, 15, 15);
            
            ctx.fillStyle = '#2d2d44';
            ctx.fillRect(-OBSTACLE_WIDTH / 2 + 10, OBSTACLE_HEIGHT / 2 - 15, OBSTACLE_WIDTH - 20, 10);
            
            ctx.restore();
        }
        
        function drawCoin(coin) {
            ctx.save();
            ctx.translate(coin.x + COIN_SIZE / 2, coin.y + COIN_SIZE / 2);
            
            const scale = 0.8 + Math.sin(Date.now() / 100) * 0.2;
            ctx.scale(scale, scale);
            
            ctx.fillStyle = '#ffd700';
            ctx.beginPath();
            ctx.arc(0, 0, COIN_SIZE / 2, 0, Math.PI * 2);
            ctx.fill();
            
            ctx.fillStyle = '#ffed4a';
            ctx.beginPath();
            ctx.arc(-3, -3, COIN_SIZE / 3, 0, Math.PI * 2);
            ctx.fill();
            
            ctx.fillStyle = '#b8860b';
            ctx.font = 'bold 16px Arial';
            ctx.textAlign = 'center';
            ctx.textBaseline = 'middle';
            ctx.fillText('$', 0, 1);
            
            ctx.restore();
        }
        
        function drawParticles() {
            particles.forEach((p, index) => {
                p.x += p.vx;
                p.y += p.vy;
                p.life -= 0.02;
                
                if (p.life <= 0) {
                    particles.splice(index, 1);
                    return;
                }
                
                ctx.fillStyle = `rgba(255, 215, 0, ${p.life})`;
                ctx.beginPath();
                ctx.arc(p.x, p.y, p.size * p.life, 0, Math.PI * 2);
                ctx.fill();
            });
        }
        
        function createParticles(x, y) {
            for (let i = 0; i < 10; i++) {
                particles.push({
                    x: x,
                    y: y,
                    vx: (Math.random() - 0.5) * 8,
                    vy: (Math.random() - 0.5) * 8,
                    size: Math.random() * 6 + 2,
                    life: 1
                });
            }
        }
        
        function spawnObstacle() {
            const track = Math.floor(Math.random() * TRACK_COUNT);
            const types = ['train', 'barrier'];
            const type = types[Math.floor(Math.random() * types.length)];
            
            obstacles.push({
                x: canvas.width,
                y: track * TRACK_HEIGHT + (TRACK_HEIGHT - OBSTACLE_HEIGHT) / 2,
                track: track,
                type: type,
                width: OBSTACLE_WIDTH,
                height: OBSTACLE_HEIGHT
            });
        }
        
        function spawnCoin() {
            const track = Math.floor(Math.random() * TRACK_COUNT);
            
            while (obstacles.some(o => o.track === track && o.x > canvas.width - 100)) {
                return;
            }
            
            coins.push({
                x: canvas.width + 50 + Math.random() * 200,
                y: track * TRACK_HEIGHT + (TRACK_HEIGHT - COIN_SIZE) / 2,
                track: track,
                width: COIN_SIZE,
                height: COIN_SIZE,
                collected: false
            });
        }
        
        function checkCollision(rect1, rect2) {
            return rect1.x < rect2.x + rect2.width &&
                   rect1.x + rect1.width > rect2.x &&
                   rect1.y < rect2.y + rect2.height &&
                   rect1.y + rect1.height > rect2.y;
        }
        
        function update() {
            if (!gameRunning) return;
            
            if (keys.left && player.track > 0) {
                player.track--;
                keys.left = false;
            }
            if (keys.right && player.track < TRACK_COUNT - 1) {
                player.track++;
                keys.right = false;
            }
            
            if (keys.up && player.grounded && !player.jumping) {
                player.jumping = true;
                player.grounded = false;
                player.jumpVelocity = 15;
            }
            
            if (player.jumping) {
                player.jumpHeight += player.jumpVelocity;
                player.jumpVelocity -= 0.8;
                
                if (player.jumpHeight <= 0) {
                    player.jumpHeight = 0;
                    player.jumping = false;
                    player.grounded = true;
                    player.jumpVelocity = 0;
                }
            }
            
            updatePlayerY();
            
            if (Math.random() < 0.02) {
                spawnObstacle();
            }
            
            if (Math.random() < 0.03) {
                spawnCoin();
            }
            
            obstacles.forEach((obstacle, index) => {
                obstacle.x -= gameSpeed;
                
                if (obstacle.x + obstacle.width < 0) {
                    obstacles.splice(index, 1);
                    score += 10;
                    document.getElementById('score').textContent = score;
                }
                
                const playerRect = {
                    x: player.x,
                    y: player.y + player.jumpHeight,
                    width: player.width,
                    height: player.height
                };
                
                if (player.jumpHeight < 30 && checkCollision(playerRect, obstacle)) {
                    gameOver();
                }
            });
            
            coins.forEach((coin, index) => {
                coin.x -= gameSpeed;
                
                if (coin.x + coin.width < 0) {
                    coins.splice(index, 1);
                }
                
                if (!coin.collected) {
                    const playerRect = {
                        x: player.x,
                        y: player.y + player.jumpHeight,
                        width: player.width,
                        height: player.height
                    };
                    
                    if (checkCollision(playerRect, coin)) {
                        coin.collected = true;
                        score += 50;
                        document.getElementById('score').textContent = score;
                        createParticles(coin.x + COIN_SIZE / 2, coin.y + COIN_SIZE / 2);
                        coins.splice(index, 1);
                    }
                }
            });
            
            gameSpeed = 5 + score / 500;
            
            draw();
            
            animationId = requestAnimationFrame(update);
        }
        
        function draw() {
            drawBackground();
            
            obstacles.forEach(drawObstacle);
            coins.forEach(drawCoin);
            drawParticles();
            drawPlayer();
        }
        
        function gameOver() {
            gameRunning = false;
            cancelAnimationFrame(animationId);
            
            if (score > highScore) {
                highScore = score;
                localStorage.setItem('subwayRunnerHighScore', highScore);
            }
            
            document.getElementById('finalScore').textContent = score;
            document.getElementById('highScore').textContent = highScore;
            document.getElementById('gameOverScreen').style.display = 'flex';
            document.getElementById('score').textContent = '0';
        }
        
        function startGame() {
            score = 0;
            gameSpeed = 5;
            player.track = 1;
            player.jumping = false;
            player.jumpHeight = 0;
            player.grounded = true;
            obstacles = [];
            coins = [];
            particles = [];
            
            updatePlayerY();
            
            document.getElementById('startScreen').style.display = 'none';
            document.getElementById('gameOverScreen').style.display = 'none';
            document.getElementById('score').textContent = '0';
            
            gameRunning = true;
            update();
        }
        
        document.getElementById('startBtn').addEventListener('click', startGame);
        document.getElementById('restartBtn').addEventListener('click', startGame);
        
        document.addEventListener('keydown', (e) => {
            if (e.key === 'ArrowLeft' || e.key === 'a') keys.left = true;
            if (e.key === 'ArrowRight' || e.key === 'd') keys.right = true;
            if (e.key === 'ArrowUp' || e.key === 'w' || e.key === ' ') keys.up = true;
        });
        
        document.addEventListener('keyup', (e) => {
            if (e.key === 'ArrowLeft' || e.key === 'a') keys.left = false;
            if (e.key === 'ArrowRight' || e.key === 'd') keys.right = false;
            if (e.key === 'ArrowUp' || e.key === 'w' || e.key === ' ') keys.up = false;
        });
        
        drawBackground();
        drawPlayer();
    </script>
</body>
</html>

# 🐍 Welcome to My GitHub Profile

[Interactive Snake Game Below! ](#-snake-game)

## 🎮 Snake Game

```html
<style>
  #gameContainer {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 20px;
    padding: 20px;
    background:  #1a1a1a;
    border-radius: 10px;
    max-width: 400px;
  }
  
  #gameCanvas {
    border: 2px solid #00ff00;
    background: #000;
    cursor: pointer;
  }
  
  .gameControls {
    color: #00ff00;
    font-family: monospace;
    text-align: center;
  }
  
  .score {
    font-size: 18px;
    font-weight: bold;
  }
</style>

<div id="gameContainer">
  <div class="gameControls">
    <div class="score">Score: <span id="score">0</span></div>
    <div style="font-size: 14px; margin-top: 10px;">
      Use Arrow Keys to Play | Space to Pause
    </div>
  </div>
  <canvas id="gameCanvas" width="300" height="300"></canvas>
</div>

<script>
  const canvas = document.getElementById('gameCanvas');
  const ctx = canvas.getContext('2d');
  const scoreDisplay = document.getElementById('score');
  
  const gridSize = 20;
  const tileCount = canvas.width / gridSize;
  
  let snake = [
    {x: Math.floor(tileCount / 2), y: Math.floor(tileCount / 2)}
  ];
  
  let food = {x: Math.floor(Math.random() * tileCount), y: Math.floor(Math.random() * tileCount)};
  let direction = {x: 1, y: 0};
  let nextDirection = {x: 1, y: 0};
  let score = 0;
  let gameRunning = true;
  
  function drawRect(x, y, color) {
    ctx.fillStyle = color;
    ctx.fillRect(x * gridSize, y * gridSize, gridSize - 1, gridSize - 1);
  }
  
  function update() {
    if (gameRunning) {
      direction = nextDirection;
      const head = snake[0];
      const newHead = {x: head. x + direction.x, y: head.y + direction.y};
      
      // Check collisions with walls
      if (newHead. x < 0 || newHead.x >= tileCount || newHead.y < 0 || newHead.y >= tileCount) {
        gameRunning = false;
        alert('Game Over! Final Score: ' + score);
        resetGame();
        return;
      }
      
      // Check collision with self
      for (let i = 0; i < snake.length; i++) {
        if (newHead.x === snake[i].x && newHead.y === snake[i].y) {
          gameRunning = false;
          alert('Game Over! Final Score: ' + score);
          resetGame();
          return;
        }
      }
      
      snake.unshift(newHead);
      
      // Check if eaten food
      if (newHead.x === food.x && newHead. y === food.y) {
        score += 10;
        scoreDisplay.textContent = score;
        food = {x: Math.floor(Math.random() * tileCount), y: Math.floor(Math.random() * tileCount)};
      } else {
        snake.pop();
      }
    }
  }
  
  function draw() {
    ctx.fillStyle = '#000';
    ctx.fillRect(0, 0, canvas.width, canvas.height);
    
    // Draw snake
    ctx.fillStyle = '#00ff00';
    for (let segment of snake) {
      drawRect(segment.x, segment.y, '#00ff00');
    }
    
    // Draw food
    drawRect(food.x, food.y, '#ff0000');
  }
  
  function resetGame() {
    snake = [{x: Math.floor(tileCount / 2), y: Math.floor(tileCount / 2)}];
    direction = {x: 1, y: 0};
    nextDirection = {x: 1, y: 0};
    score = 0;
    scoreDisplay.textContent = score;
    gameRunning = true;
  }
  
  function gameLoop() {
    update();
    draw();
    setTimeout(gameLoop, 100);
  }
  
  document.addEventListener('keydown', (e) => {
    switch(e.key) {
      case 'ArrowUp': 
        if (direction.y === 0) nextDirection = {x: 0, y: -1};
        e.preventDefault();
        break;
      case 'ArrowDown': 
        if (direction.y === 0) nextDirection = {x: 0, y: 1};
        e.preventDefault();
        break;
      case 'ArrowLeft':
        if (direction.x === 0) nextDirection = {x: -1, y: 0};
        e.preventDefault();
        break;
      case 'ArrowRight': 
        if (direction.x === 0) nextDirection = {x: 1, y: 0};
        e.preventDefault();
        break;
      case ' ':
        gameRunning = ! gameRunning;
        e. preventDefault();
        break;
    }
  });
  
  gameLoop();
</script>
```

## How to Play

- **Arrow Keys**: Control the snake direction
- **Space Bar**: Pause/Resume
- **Goal**: Eat the red food to grow and earn points
- **Avoid**:  Walls and your own tail! 

---

*Thanks for visiting my profile! 🚀*
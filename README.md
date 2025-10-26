<!DOCTYPE html>
<html>
<head>
    <title>Pixel Game</title>
    <style>
        #gameContainer {
            display: grid;
            grid-template-columns: repeat(20, 20px);
            grid-template-rows: repeat(20, 20px);
            gap: 1px;
            background-color: #333;
            padding: 10px;
            width: fit-content;   
        .pixel {
            width: 20px;
            height: 20px;
            background-color: #fff;
        }
            .player {
            background-color: red;
        }
        .food {
            background-color: green;
        }
        #score {
            margin: 20px 0;
            font-size: 24px;
        }
    </style>
</head>
<body>
    <div id="score">Score: 0</div>
    <div id="gameContainer"></div>
    <script>
        const container = document.getElementById('gameContainer');
        const scoreElement = document.getElementById('score');
        const gridSize = 20;
        let score = 0;
        let playerPosition = {x: 0, y: 0};
        let foodPosition = {x: 10, y: 10};
        // Create grid
        for (let i = 0; i < gridSize * gridSize; i++) {
            const pixel = document.createElement('div');
            pixel.className = 'pixel';
            container.appendChild(pixel);
        }
        // Update game display
        function updateGame() {
            const pixels = document.getElementsByClassName('pixel');
            for (let i = 0; i < pixels.length; i++) {
                pixels[i].classList.remove('player', 'food');
            }
            const playerIndex = playerPosition.y * gridSize + playerPosition.x;
            const foodIndex = foodPosition.y * gridSize + foodPosition.x; 
            pixels[playerIndex].classList.add('player');
            pixels[foodIndex].classList.add('food');
        }
         // Move player
        document.addEventListener('keydown', (event) => {
            const oldPosition = {...playerPosition};
            switch(event.key) {
                case 'ArrowUp':
                    if (playerPosition.y > 0) playerPosition.y--;
                    break;
                case 'ArrowDown':
                    if (playerPosition.y < gridSize - 1) playerPosition.y++;
                    break;
                case 'ArrowLeft':
                    if (playerPosition.x > 0) playerPosition.x--;
                    break;
                case 'ArrowRight':
                    if (playerPosition.x < gridSize - 1) playerPosition.x++;
                    break;
            }
            // Check if player got food
            if (playerPosition.x === foodPosition.x && playerPosition.y === foodPosition.y) {
                score += 10;
                scoreElement.textContent = `Score: ${score}`;
                // Generate new food position
                foodPosition.x = Math.floor(Math.random() * gridSize);
                foodPosition.y = Math.floor(Math.random() * gridSize);
            }
           updateGame();
        });
        // Initial game render
        updateGame();
    </script>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
    <title>Pixel Game</title>
    <style>
        body {
            background-color: #0a0a0a;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            padding: 20px;
            overflow: hidden;
        }
        /* RGB Border Animation */
        @keyframes rgb {
            0% { box-shadow: 0 0 50px rgb(255, 0, 0, 0.5); }
            33% { box-shadow: 0 0 50px rgb(0, 255, 0, 0.5); }
            66% { box-shadow: 0 0 50px rgb(0, 0, 255, 0.5); }
            100% { box-shadow: 0 0 50px rgb(255, 0, 0, 0.5); }
        }
        #gameContainer {
            display: grid;
            grid-template-columns: repeat(20, 20px);
            grid-template-rows: repeat(20, 20px);
            gap: 1px;
            background-color: #222;
            padding: 20px;
            width: fit-content;
            border-radius: 10px;
            animation: rgb 5s infinite;
            backdrop-filter: blur(5px);
        }
        .pixel {
            width: 20px;
            height: 20px;
            background-color: #333;
            border-radius: 3px;
        }  
        .player {
            background-color: #ff3e3e;
            box-shadow: 0 0 10px #ff3e3e;
        }   
        .food {
            background-color: #4eff4e;
            box-shadow: 0 0 10px #4eff4e;
        }    
        #score {
            margin: 20px 0;
            font-size: 24px;
            color: #fff;
            text-shadow: 0 0 10px #fff;
            font-family: Arial, sans-serif;
        }
        /* Control Buttons */
        .controls {
            margin-top: 20px;
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
        }
        .control-btn {
            padding: 15px 25px;
            font-size: 18px;
            background-color: #333;
            border: none;
            color: #fff;
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.3s;
            text-shadow: 0 0 5px #fff;
            box-shadow: 0 0 10px rgba(255,255,255,0.2);
        }
        .control-btn:hover {
            background-color: #444;
            box-shadow: 0 0 15px rgba(255,255,255,0.4);
        }
        #up { grid-column: 2; }
        #left { grid-column: 1; grid-row: 2; }
        #right { grid-column: 3; grid-row: 2; }
        #down { grid-column: 2; grid-row: 3; }
    </style>
</head>
<body>
    <div id="score">Score: 0</div>
    <div id="gameContainer"></div>
    <div class="controls">
        <button id="up" class="control-btn">↑</button>
        <button id="left" class="control-btn">←</button>
        <button id="right" class="control-btn">→</button>
        <button id="down" class="control-btn">↓</button>
    </div>
    
<script>
        // ...existing code...

        // Add button controls
        document.getElementById('up').addEventListener('click', () => movePlayer('ArrowUp'));
        document.getElementById('down').addEventListener('click', () => movePlayer('ArrowDown'));
        document.getElementById('left').addEventListener('click', () => movePlayer('ArrowLeft'));
        document.getElementById('right').addEventListener('click', () => movePlayer('ArrowRight'));

        function movePlayer(direction) {
            const event = { key: direction };
            handleMovement(event);
        }

        // Modify the keydown event listener
        function handleMovement(event) {
            const oldPosition = {...playerPosition};

            switch(event.key) {
                case 'ArrowUp':
                    if (playerPosition.y > 0) playerPosition.y--;
                    break;
                case 'ArrowDown':
                    if (playerPosition.y < gridSize - 1) playerPosition.y++;
                    break;
                case 'ArrowLeft':
                    if (playerPosition.x > 0) playerPosition.x--;
                    break;
                case 'ArrowRight':
                    if (playerPosition.x < gridSize - 1) playerPosition.x++;
                    break;
            }

            if (playerPosition.x === foodPosition.x && playerPosition.y === foodPosition.y) {
                score += 10;
                scoreElement.textContent = `Score: ${score}`;
                foodPosition.x = Math.floor(Math.random() * gridSize);
                foodPosition.y = Math.floor(Math.random() * gridSize);
            }

            updateGame();
        }

        document.addEventListener('keydown', handleMovement);

        updateGame();
    </script>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
    <title>Pixel Game</title>
    <style>
        body {
            background-color: rgba(10, 10, 10, 0.8);
            background-image: 
                radial-gradient(circle at 20% 20%, rgba(255, 0, 0, 0.15), transparent 40%),
                radial-gradient(circle at 80% 80%, rgba(0, 255, 0, 0.15), transparent 40%),
                radial-gradient(circle at 50% 50%, rgba(0, 0, 255, 0.15), transparent 40%);
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            padding: 20px;
            overflow: hidden;
        }
        /* Glowing RGB Animation */
        @keyframes rgbPulse {
            0% { 
                box-shadow: 0 0 50px rgba(255, 0, 0, 0.3),
                           inset 0 0 20px rgba(255, 0, 0, 0.3);
            }
            33% { 
                box-shadow: 0 0 50px rgba(0, 255, 0, 0.3),
                           inset 0 0 20px rgba(0, 255, 0, 0.3);
            }
            66% { 
                box-shadow: 0 0 50px rgba(0, 0, 255, 0.3),
                           inset 0 0 20px rgba(0, 0, 255, 0.3);
            }
            100% { 
                box-shadow: 0 0 50px rgba(255, 0, 0, 0.3),
                           inset 0 0 20px rgba(255, 0, 0, 0.3);
            }
        }
        #gameContainer {
            display: grid;
            grid-template-columns: repeat(20, 20px);
            grid-template-rows: repeat(20, 20px);
            gap: 1px;
            background-color: rgba(34, 34, 34, 0.5);
            padding: 20px;
            width: fit-content;
            border-radius: 15px;
            animation: rgbPulse 8s infinite;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        .pixel {
            width: 20px;
            height: 20px;
            background-color: rgba(51, 51, 51, 0.3);
            border-radius: 3px;
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.05);
        }
        .player {
            background-color: rgba(255, 62, 62, 0.8);
            box-shadow: 0 0 15px #ff3e3e;
        }
        .food {
            background-color: rgba(78, 255, 78, 0.8);
            box-shadow: 0 0 15px #4eff4e;
        }
        #score {
            margin: 20px 0;
            font-size: 28px;
            color: rgba(255, 255, 255, 0.9);
            text-shadow: 0 0 15px rgba(255, 255, 255, 0.8);
            font-family: Arial, sans-serif;
            backdrop-filter: blur(5px);
            padding: 10px 20px;
            border-radius: 10px;
            background-color: rgba(255, 255, 255, 0.1);
        }
        .controls {
            margin-top: 20px;
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
        }
        .control-btn {
            padding: 15px 25px;
            font-size: 18px;
            background-color: rgba(51, 51, 51, 0.5);
            border: 1px solid rgba(255, 255, 255, 0.1);
            color: rgba(255, 255, 255, 0.9);
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s;
            text-shadow: 0 0 5px rgba(255, 255, 255, 0.5);
            box-shadow: 0 0 10px rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(5px);
        }
        .control-btn:hover {
            background-color: rgba(68, 68, 68, 0.7);
            box-shadow: 0 0 20px rgba(255, 255, 255, 0.2);
            transform: scale(1.05);
        }
        /* Keep existing button positioning */
        #up { grid-column: 2; }
        #left { grid-column: 1; grid-row: 2; }
        #right { grid-column: 3; grid-row: 2; }
        #down { grid-column: 2; grid-row: 3; }
    </style>
</head>

<!DOCTYPE html>
<html>
<head>
    <title>OnexMix Pixel Game</title>
    <style>
        /* Add these new styles */
        .game-title {
            font-size: 48px;
            color: rgba(255, 255, 255, 0.9);
            text-shadow: 
                0 0 10px rgba(255, 255, 255, 0.8),
                0 0 20px rgba(255, 255, 255, 0.5),
                0 0 30px rgba(255, 255, 255, 0.3);
            margin: 20px 0;
            font-family: 'Arial Black', sans-serif;
            letter-spacing: 3px;
            animation: titleGlow 2s infinite alternate;
            text-align: center;
            background: linear-gradient(45deg, #ff3e3e, #4eff4e, #3e9fff);
            -webkit-background-clip: text;
            background-clip: text;
            -webkit-text-fill-color: transparent;
            filter: drop-shadow(0 0 10px rgba(255, 255, 255, 0.5));
        }
        @keyframes titleGlow {
            from {
                filter: drop-shadow(0 0 5px rgba(255, 255, 255, 0.5));
            }
            to {
                filter: drop-shadow(0 0 20px rgba(255, 255, 255, 0.8));
            }
        }
        .mobile-controls {
            position: fixed;
            bottom: 20px;
            display: grid;
            grid-template-columns: repeat(3, 60px);
            grid-template-rows: repeat(3, 60px);
            gap: 5px;
            padding: 10px;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .mobile-btn {
            width: 60px;
            height: 60px;
            border: none;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.2);
            color: white;
            font-size: 24px;
            cursor: pointer;
            transition: all 0.3s;
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.3);
            display: flex;
            align-items: center;
            justify-content: center;
            text-shadow: 0 0 5px rgba(255, 255, 255, 0.5);
            box-shadow: 
                0 0 10px rgba(255, 255, 255, 0.2),
                inset 0 0 10px rgba(255, 255, 255, 0.2);
        }
        .mobile-btn:hover {
            background: rgba(255, 255, 255, 0.3);
            transform: scale(1.1);
            box-shadow: 
                0 0 20px rgba(255, 255, 255, 0.4),
                inset 0 0 20px rgba(255, 255, 255, 0.4);
        }
        #mobileUp { grid-area: 1/2/2/3; }
        #mobileLeft { grid-area: 2/1/3/2; }
        #mobileRight { grid-area: 2/3/3/4; }
        #mobileDown { grid-area: 3/2/4/3; }
        /* Add floating light effects */
        .light-effect {
            position: fixed;
            width: 200px;
            height: 200px;
            border-radius: 50%;
            pointer-events: none;
            z-index: -1;
            animation: floatLight 10s infinite linear;
        }
        .light-1 { 
            top: 10%;
            left: 10%;
            background: radial-gradient(circle, rgba(255,0,0,0.1) 0%, transparent 70%);
        }
        .light-2 {
            bottom: 10%;
            right: 10%;
            background: radial-gradient(circle, rgba(0,255,0,0.1) 0%, transparent 70%);
            animation-delay: -5s;
        }
        @keyframes floatLight {
            0% { transform: translate(0, 0) scale(1); }
            50% { transform: translate(50px, 50px) scale(1.5); }
            100% { transform: translate(0, 0) scale(1); }
        }
    </style>
</head>
<body>
    <!-- Add these elements after body tag -->
    <div class="light-effect light-1"></div>
    <div class="light-effect light-2"></div>
    <h1 class="game-title">OnexMix</h1>
    <!-- Add mobile controls before closing body tag -->
    <div class="mobile-controls">
        <button class="mobile-btn" id="mobileUp">↑</button>
        <button class="mobile-btn" id="mobileLeft">←</button>
        <button class="mobile-btn" id="mobileRight">→</button>
        <button class="mobile-btn" id="mobileDown">↓</button>
    </div>
    <!-- Add this to your existing script -->
    <script>
        // Add mobile controls
        document.getElementById('mobileUp').addEventListener('click', () => movePlayer('ArrowUp'));
        document.getElementById('mobileDown').addEventListener('click', () => movePlayer('ArrowDown'));
        document.getElementById('mobileLeft').addEventListener('click', () => movePlayer('ArrowLeft'));
        document.getElementById('mobileRight').addEventListener('click', () => movePlayer('ArrowRight'));
        // Add touch support for mobile buttons
        const mobileButtons = document.querySelectorAll('.mobile-btn');
        mobileButtons.forEach(button => {
            button.addEventListener('touchstart', (e) => {
                e.preventDefault();
                button.click();
            });
        });
    </script>
</body>
</html><style>
/* Add these new styles for score bubble effect */
@keyframes scoreBubble {
    0% {
        transform: scale(1);
        opacity: 1;
    }
    100% {
        transform: scale(2);
        opacity: 0;
    }
}
.score-bubble {
    position: fixed;
    color: rgba(255, 255, 255, 0.9);
    font-size: 24px;
    pointer-events: none;
    animation: scoreBubble 1s ease-out forwards;
    text-shadow: 0 0 10px rgba(255, 255, 255, 0.8);
    background: rgba(255, 255, 255, 0.1);
    padding: 10px 20px;
    border-radius: 20px;
    backdrop-filter: blur(5px);
    border: 1px solid rgba(255, 255, 255, 0.2);
    box-shadow: 
        0 0 20px rgba(255, 255, 255, 0.2),
        inset 0 0 10px rgba(255, 255, 255, 0.2);
}
/* Enhanced button styles */
.mobile-btn {
    width: 60px;
    height: 60px;
    border: none;
    border-radius: 50%;
    background: rgba(255, 255, 255, 0.15);
    color: white;
    font-size: 24px;
    cursor: pointer;
    transition: all 0.3s;
    backdrop-filter: blur(8px);
    border: 1px solid rgba(255, 255, 255, 0.3);
    display: flex;
    align-items: center;
    justify-content: center;
    text-shadow: 0 0 5px rgba(255, 255, 255, 0.5);
    box-shadow: 
        0 0 15px rgba(255, 255, 255, 0.2),
        inset 0 0 15px rgba(255, 255, 255, 0.2),
        0 5px 15px rgba(0, 0, 0, 0.3);
}
.mobile-btn:hover {
    background: rgba(255, 255, 255, 0.25);
    transform: scale(1.1) translateY(-2px);
    box-shadow: 
        0 0 25px rgba(255, 255, 255, 0.4),
        inset 0 0 25px rgba(255, 255, 255, 0.4),
        0 8px 20px rgba(0, 0, 0, 0.4);
}
.mobile-btn:active {
    transform: scale(0.95) translateY(2px);
    box-shadow: 
        0 0 15px rgba(255, 255, 255, 0.2),
        inset 0 0 15px rgba(255, 255, 255, 0.2),
        0 2px 10px rgba(0, 0, 0, 0.2);
}
/* Add this to your existing script section */
</style>

<script>
// Add this function to create score bubble effect
function createScoreBubble(x, y) {
    const bubble = document.createElement('div');
    bubble.className = 'score-bubble';
    bubble.textContent = '+10';
    bubble.style.left = `${x}px`;
    bubble.style.top = `${y}px`;
    document.body.appendChild(bubble);
    
    // Remove bubble after animation
    bubble.addEventListener('animationend', () => {
        bubble.remove();
    });
}

// Modify the part where score is updated
if (playerPosition.x === foodPosition.x && playerPosition.y === foodPosition.y) {
    score += 10;
    scoreElement.textContent = `Score: ${score}`;
    
    // Get the food position on screen
    const foodElement = document.querySelector('.food');
    const rect = foodElement.getBoundingClientRect();
    createScoreBubble(rect.left, rect.top);
    
    // Generate new food position
    foodPosition.x = Math.floor(Math.random() * gridSize);
    foodPosition.y = Math.floor(Math.random() * gridSize);
}
</script><!-- Add this in the <head> section -->
<style>
/* Audio controls styling */
.audio-controls {
    position: fixed;
    top: 20px;
    right: 20px;
    background: rgba(255, 255, 255, 0.1);
    padding: 10px;
    border-radius: 10px;
    backdrop-filter: blur(5px);
    border: 1px solid rgba(255, 255, 255, 0.2);
}

.audio-btn {
    background: rgba(255, 255, 255, 0.2);
    border: 1px solid rgba(255, 255, 255, 0.3);
    color: white;
    padding: 5px 10px;
    border-radius: 5px;
    cursor: pointer;
    margin: 0 5px;
    transition: all 0.3s;
}

.audio-btn:hover {
    background: rgba(255, 255, 255, 0.3);
    transform: scale(1.1);
}
</style>

<!-- Add this right after the <body> tag -->
<div class="audio-controls">
    <button class="audio-btn" id="toggleMusic">🎵 Music</button>
    <button class="audio-btn" id="toggleSound">🔊 Sound</button>
</div>

<audio id="bgMusic" loop>
    <source src="https://assets.mixkit.co/music/preview/mixkit-game-level-music-689.mp3" type="audio/mp3">
</audio>

<audio id="scoreSound">
    <source src="https://assets.mixkit.co/sfx/preview/mixkit-arcade-game-jump-coin-216.mp3" type="audio/mp3">
</audio>

<!-- Add this to your existing script section -->
<script>
const bgMusic = document.getElementById('bgMusic');
const scoreSound = document.getElementById('scoreSound');
const toggleMusicBtn = document.getElementById('toggleMusic');
const toggleSoundBtn = document.getElementById('toggleSound');

let isMusicOn = false;
let isSoundOn = true;

// Music controls
toggleMusicBtn.addEventListener('click', () => {
    isMusicOn = !isMusicOn;
    if (isMusicOn) {
        bgMusic.play();
        toggleMusicBtn.style.background = 'rgba(0, 255, 0, 0.2)';
    } else {
        bgMusic.pause();
        toggleMusicBtn.style.background = 'rgba(255, 255, 255, 0.2)';
    }
});

// Sound effects controls
toggleSoundBtn.addEventListener('click', () => {
    isSoundOn = !isSoundOn;
    toggleSoundBtn.style.background = isSoundOn ? 
        'rgba(0, 255, 0, 0.2)' : 'rgba(255, 255, 255, 0.2)';
});

// Modify your score update logic to include sound
if (playerPosition.x === foodPosition.x && playerPosition.y === foodPosition.y) {
    score += 10;
    scoreElement.textContent = `Score: ${score}`;
    
    // Play score sound if enabled
    if (isSoundOn) {
        scoreSound.currentTime = 0; // Reset sound to start
        scoreSound.play();
    }
    
    // Create score bubble
    const foodElement = document.querySelector('.food');
    const rect = foodElement.getBoundingClientRect();
    createScoreBubble(rect.left, rect.top);
    
    // Generate new food position
    foodPosition.x = Math.floor(Math.random() * gridSize);
    foodPosition.y = Math.floor(Math.random() * gridSize);
}

// Add volume controls
bgMusic.volume = 0.3; // 30% volume for background music
scoreSound.volume = 0.5; // 50% volume for score sound

// Initialize music button state
toggleMusicBtn.style.background = 'rgba(255, 255, 255, 0.2)';
toggleSoundBtn.style.background = 'rgba(0, 255, 0, 0.2)';

// Handle page visibility changes
document.addEventListener('visibilitychange', () => {
    if (document.hidden && isMusicOn) {
        bgMusic.pause();
    } else if (!document.hidden && isMusicOn) {
        bgMusic.play();
    }
});
</script>

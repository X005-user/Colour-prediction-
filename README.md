# Colour-prediction-
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Color Prediction Game</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>

    <div class="container">
        <h1>Color Prediction Game</h1>

        <div class="game-board">
            <div id="result">
                <h2>Result: <span id="resultColor">--</span></h2>
            </div>

            <div id="colorChoices">
                <button class="color-btn" id="red">Red</button>
                <button class="color-btn" id="green">Green</button>
                <button class="color-btn" id="blue">Blue</button>
            </div>

            <div id="bettingArea">
                <label for="betAmount">Enter Bet Amount: </label>
                <input type="number" id="betAmount" value="10">
                <button id="placeBet">Place Bet</button>
            </div>

            <div id="gameHistory">
                <h3>Game History</h3>
                <ul id="historyList">
                    <!-- Game result history will be shown here -->
                </ul>
            </div>
        </div>
    </div>

    <script sr
c="script.js"></script>
</body>
</html>
/* styles.css */
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f9;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
}

.container {
    background-color: #fff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    width: 300px;
}

h1 {
    text-align: center;
    color: #333;
}

.game-board {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.color-btn {
    margin: 10px;
    padding: 15px;
    font-size: 16px;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background 0.3s;
}

#red {
    background-color: red;
}

#green {
    background-color: green;
}

#blue {
    background-color: blue;
}

.color-btn:hover {
    opacity: 0.8;
}

#bettingArea {
    margin-top: 20px;
    text-align: center;
}

#betAmount {
    padding: 5px;
    width: 80px;
}

#placeBet {
    margin-top: 10px;
    padding: 8px 20px;
    background-color: #007BFF;
    color: white;
    border: none;
    cursor: pointer;
}

#placeBet:hover {
    background-c
olor: #0056b3;
}

#historyList {
    list-style-type: none;
    padding: 0;
// script.js

let betAmount = 10;  // Default bet amount
let playerBet = null; // Player's color bet

// Handle color button clicks to place a bet
document.getElementById('red').addEventListener('click', function() {
    playerBet = 'red';
    updateBetUI();
});

document.getElementById('green').addEventListener('click', function() {
    playerBet = 'green';
    updateBetUI();
});

document.getElementById('blue').addEventListener('click', function() {
    playerBet = 'blue';
    updateBetUI();
});

// Update UI with player's chosen color and bet amount
function updateBetUI() {
    if (playerBet) {
        document.getElementById('placeBet').disabled = false;
    }
}

// Handle bet placement
document.getElementById('placeBet').addEventListener('click', function() {
    const result = getRandomColor();
    displayResult(result);
    checkWin(result);
    recordGameHistory(result);
});

// Generate random color (Red, Green, or Blue)
function getRandomColor() {
    const colors = ['red', 'green', 'blue'];
    const randomIndex = Math.floor(Math.random() * colors.length);
    return colors[randomIndex];
}

// Display result
function displayResult(color) {
    document.getElementById('resultColor').innerText = color;
}

// Check if player's bet is correct
function checkWin(result) {
    if (playerBet === result) {
        alert(`You Win! The color was ${result}`);
    } else {
        alert(`You Lose! The color was ${result}`);
    }
    playerBet = null; // Reset bet after each game
    document.getElementById('placeBet').disabled = true; // Disable bet until next selection
}

// Record game history
function recordGameHistory(result) {
    const historyList = document.getElementById('historyList');
    const listItem = document.createElement('li');
    listItem.textContent
 = `Color: ${result}`;
    historyList.appendChild(listItem);
}
// server.js
const express = require('express');
const http = require('http');
const socketIo = require('socket.io');
const app = express();
const server = http.createServer(app);
const io = socketIo(server);

app.use(express.static('public')); // Assuming front-end files are in 'public' folder

io.on('connection', (socket) => {
    console.log('A user connected');
    socket.on('disconnect', () => {
        console.log('User disconnected');
    });
});

server.listen(3000, () => {
    console.log('Server running on http://loc
alhost:3000');
});
}

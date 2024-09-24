---
title: Tic Tac Toe
layout: post
description: Simple game
categories: [Javascript]
permalink: /javascript/project/tic-tac-toe
menu: nav/javascript_project.html
toc: true
comments: true
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic Tac Toe</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-top: 50px;
        }
        .board {
            display: grid;
            grid-template-columns: repeat(3, 100px);
            gap: 5px;
        }
        .cell {
            width: 100px;
            height: 100px;
            background-color: #f0f0f0;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2em;
            cursor: pointer;
        }
        .cell:hover {
            background-color: #d0d0d0;
        }
        h1 {
            margin-bottom: 20px;
        }
    </style>
</head>
<body>
    <h1>Tic Tac Toe</h1>
    <div class="board" id="board">
        <div class="cell" data-index="0"></div>
        <div class="cell" data-index="1"></div>
        <div class="cell" data-index="2"></div>
        <div class="cell" data-index="3"></div>
        <div class="cell" data-index="4"></div>
        <div class="cell" data-index="5"></div>
        <div class="cell" data-index="6"></div>
        <div class="cell" data-index="7"></div>
        <div class="cell" data-index="8"></div>
    </div>
    <button id="restart">Restart</button>

    <script>
        const board = document.getElementById('board');
        const cells = document.querySelectorAll('.cell');
        const restartButton = document.getElementById('restart');

        let currentPlayer = 'X';
        let gameActive = true;
        let gameState = ['', '', '', '', '', '', '', '', ''];

        const winningConditions = [
            [0, 1, 2],
            [3, 4, 5],
            [6, 7, 8],
            [0, 3, 6],
            [1, 4, 7],
            [2, 5, 8],
            [0, 4, 8],
            [2, 4, 6],
        ];

        function handleCellClick(event) {
            const clickedCell = event.target;
            const clickedCellIndex = parseInt(clickedCell.getAttribute('data-index'));

            if (gameState[clickedCellIndex] !== '' || !gameActive) {
                return;
            }

            gameState[clickedCellIndex] = currentPlayer;
            clickedCell.textContent = currentPlayer;

            checkResult();
        }

        function checkResult() {
            let roundWon = false;

            for (let i = 0; i < winningConditions.length; i++) {
                const [a, b, c] = winningConditions[i];
                if (gameState[a] === '' || gameState[b] === '' || gameState[c] === '') {
                    continue;
                }
                if (gameState[a] === gameState[b] && gameState[a] === gameState[c]) {
                    roundWon = true;
                    break;
                }
            }

            if (roundWon) {
                alert(`Player ${currentPlayer} wins!`);
                gameActive = false;
                return;
            }

            if (!gameState.includes('')) {
                alert("It's a draw!");
                gameActive = false;
                return;
            }

            currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
        }

        function restartGame() {
            gameActive = true;
            currentPlayer = 'X';
            gameState = ['', '', '', '', '', '', '', '', ''];
            cells.forEach(cell => {
                cell.textContent = '';
            });
        }

        cells.forEach(cell => cell.addEventListener('click', handleCellClick));
        restartButton.addEventListener('click', restartGame);
    </script>
</body>
</html>

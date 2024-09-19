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
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f0f0f0;
        }
        #game {
            display: grid;
            grid-template-columns: repeat(3, 100px);
            grid-template-rows: repeat(3, 100px);
            gap: 5px;
        }
        .cell {
            width: 100px;
            height: 100px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 2em;
            background-color: #fff;
            border: 2px solid #ccc;
            cursor: pointer;
        }
        .cell:hover {
            background-color: #e0e0e0;
        }
        #status {
            margin-top: 20px;
            font-size: 1.2em;
        }
    </style>
</head>
<body>

<div id="game"></div>
<div id="status"></div>

<script>
    const gameBoard = document.getElementById('game');
    const statusDisplay = document.getElementById('status');
    let board = ['', '', '', '', '', '', '', '', ''];
    let currentPlayer = 'X';
    let isGameActive = true;

    const winningConditions = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6]
    ];

    function handleCellClick(index) {
        if (board[index] !== '' || !isGameActive) return;
        
        board[index] = currentPlayer;
        renderBoard();
        checkResult();
    }

    function renderBoard() {
        gameBoard.innerHTML = '';
        board.forEach((cell, index) => {
            const cellElement = document.createElement('div');
            cellElement.classList.add('cell');
            cellElement.textContent = cell;
            cellElement.addEventListener('click', () => handleCellClick(index));
            gameBoard.appendChild(cellElement);
        });
    }

    function checkResult() {
        let roundWon = false;
        for (let i = 0; i < winningConditions.length; i++) {
            const [a, b, c] = winningConditions[i];
            if (board[a] === '' || board[b] === '' || board[c] === '') continue;
            if (board[a] === board[b] && board[b] === board[c]) {
                roundWon = true;
                break;
            }
        }

        if (roundWon) {
            statusDisplay.textContent = `Player ${currentPlayer} Wins!`;
            isGameActive = false;
            return;
        }

        if (!board.includes('')) {
            statusDisplay.textContent = 'It\'s a Draw!';
            isGameActive = false;
            return;
        }

        currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
        statusDisplay.textContent = `Player ${currentPlayer}'s Turn`;
    }

    renderBoard();
    statusDisplay.textContent = `Player ${currentPlayer}'s Turn`;
</script>

</body>
</html>
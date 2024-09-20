---
title: Cookie Clicker
layout: post
description: Cookie clicker something
categories: [Javascript]
permalink: /javascript/project/cookie
menu: nav/javascript_project.html
toc: true
comments: true
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cookie Clicker</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            background-color: #f8f8f8;
        }
        #cookie {
            width: 200px;
            height: 200px;
            cursor: pointer;
            margin-bottom: 20px;
        }
        #score {
            font-size: 2em;
            margin-bottom: 20px;
        }
        button {
            padding: 10px 20px;
            font-size: 1em;
            cursor: pointer;
            margin: 5px;
        }
        .shop {
            margin-top: 20px;
        }
    </style>
</head>
<body>

<div id="score">Cookies: 0</div>
<img id="cookie" src="https://assets.bonappetit.com/photos/5ca534485e96521ff23b382b/1:1/w_2700,h_2700,c_limit/chocolate-chip-cookie.jpg" alt="Cookie" onclick="cookieClicked()" />
<button id="upgrade" onclick="buyUpgrade()" disabled>Buy Upgrade (Cost: 50 cookies)</button>

<!-- Audio element for sound effect -->
<audio id="click-sound" src="https://youtu.be/IPhQz0MA0AI"></audio>

<div class="shop">
    <h2>Shop</h2>
    <button id="hire-worker" onclick="hireWorker()">Hire Worker (Cost: 100 cookies)</button>
    <div id="worker-info">Workers: 0 (Cookies per second: 0)</div>
</div>

<script>
    let cookies = 0;
    let cookiePerClick = 1;
    let upgradeCost = 50;
    let workerCost = 100;
    let workers = 0;
    let cookiesPerSecond = 0;

    // Function to handle cookie clicks
    function cookieClicked() {
        const sound = document.getElementById('click-sound');
        sound.currentTime = 0; // Rewind to the start
        sound.play();

        cookies += cookiePerClick;
        document.getElementById('score').innerText = `Cookies: ${cookies}`;
        checkUpgrade();
    }

    // Check if the upgrade button should be enabled
    function checkUpgrade() {
        document.getElementById('upgrade').disabled = cookies < upgradeCost;
    }

    // Buy upgrade functionality
    function buyUpgrade() {
        if (cookies >= upgradeCost) {
            cookies -= upgradeCost;
            cookiePerClick *= 2; // Double the cookies per click
            upgradeCost *= 2; // Double the cost for the next upgrade
            document.getElementById('score').innerText = `Cookies: ${cookies}`;
            document.getElementById('upgrade').innerText = `Buy Upgrade (Cost: ${upgradeCost} cookies)`;
            checkUpgrade();
        }
    }

    // Hire worker functionality
    function hireWorker() {
        if (cookies >= workerCost) {
            cookies -= workerCost;
            workers++;
            cookiesPerSecond++; // Increase cookies per second
            workerCost *= 2; // Double the cost for the next worker
            document.getElementById('worker-info').innerText = `Workers: ${workers} (Cookies per second: ${cookiesPerSecond})`;
            updateShopButton();
        }
    }

    // Update shop button based on available cookies
    function updateShopButton() {
        document.getElementById('hire-worker').innerText = `Hire Worker (Cost: ${workerCost} cookies)`;
    }

    // Function to generate cookies over time
    setInterval(() => {
        cookies += cookiesPerSecond;
        document.getElementById('score').innerText = `Cookies: ${cookies}`;
        checkUpgrade();
        updateShopButton();
    }, 1000);
</script>

</body>
</html>
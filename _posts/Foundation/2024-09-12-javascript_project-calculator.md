---
layout: post
title: Javascript Calculator
description: A common way to become familiar with a language is to build a calculator.  This calculator shows off button with actions.
categories: [Javascript]
permalink: /javascript/project/calculator
menu: nav/javascript_project.html
toc: true
comments: true
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f0f0f0;
        }
        #calculator {
            background: white;
            padding: 20px;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            width: 250px;
        }
        input[type="text"] {
            width: 100%;
            padding: 10px;
            margin-bottom: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 1.5em;
            text-align: right;
        }
        button {
            width: 23%;
            padding: 10px;
            margin: 1%;
            border: none;
            border-radius: 5px;
            font-size: 1.2em;
            cursor: pointer;
            background-color: #3498db;
            color: white;
        }
        button:hover {
            background-color: #2980b9;
        }
        .button-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
        }
    </style>
</head>
<body>

<div id="calculator">
    <input type="text" id="result" disabled />
    <div class="button-container">
        <button onclick="clearResult()">C</button>
        <button onclick="appendToResult('7')">7</button>
        <button onclick="appendToResult('8')">8</button>
        <button onclick="appendToResult('9')">9</button>
        <button onclick="appendToResult('/')">/</button>

        <button onclick="appendToResult('4')">4</button>
        <button onclick="appendToResult('5')">5</button>
        <button onclick="appendToResult('6')">6</button>
        <button onclick="appendToResult('*')">*</button>

        <button onclick="appendToResult('1')">1</button>
        <button onclick="appendToResult('2')">2</button>
        <button onclick="appendToResult('3')">3</button>
        <button onclick="appendToResult('-')">-</button>

        <button onclick="appendToResult('0')">0</button>
        <button onclick="calculateResult()">=</button>
        <button onclick="appendToResult('+')">+</button>
    </div>
</div>

<script>
    function appendToResult(value) {
        const resultField = document.getElementById('result');
        resultField.value += value;
    }

    function clearResult() {
        const resultField = document.getElementById('result');
        resultField.value = '';
    }

    function calculateResult() {
        const resultField = document.getElementById('result');
        try {
            resultField.value = eval(resultField.value);
        } catch (error) {
            resultField.value = 'Error';
        }
    }
</script>




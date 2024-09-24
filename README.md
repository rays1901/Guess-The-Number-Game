<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Guess the Number Game</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            background: linear-gradient(to right, #ffccf2, #ffb3e6);
            color: #333;
            animation: fadeIn 1s;
        }
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        h1 {
            font-size: 2.5em;
            margin-bottom: 0.5em;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
        }
        p {
            font-size: 1.2em;
            margin-bottom: 1em;
        }
        input {
            padding: 10px;
            width: 80px;
            text-align: center;
            font-size: 1.5em;
            border: 2px solid #ff69b4;
            border-radius: 5px;
            margin-right: 10px;
            transition: border 0.3s;
        }
        input:focus {
            border-color: #ff1493;
            outline: none;
        }
        button {
            padding: 10px 20px;
            font-size: 1.2em;
            cursor: pointer;
            border: none;
            border-radius: 5px;
            background: #ff69b4;
            color: #fff;
            transition: background 0.3s;
        }
        button:hover {
            background: #ff1493;
        }
        .message {
            margin-top: 20px;
            font-size: 1.5em;
            text-align: center;
            color: #333;
        }
        #restartGame {
            display: none;
            margin-top: 20px;
        }
    </style>
</head>
<body>

<h1>Guess the Number Game</h1>
<p>Guess a number between 1 and 100</p>
<div>
    <input type="number" id="guessInput" min="1" max="100" />
    <button id="submitGuess">Submit Guess</button>
</div>
<div class="message" id="message"></div>
<button id="restartGame">Play Again</button>

<audio id="correctSound" src="https://www.soundjay.com/button/sounds/button-3.mp3"></audio>

<script>
    let randomNumber = Math.floor(Math.random() * 100) + 1;
    let attempts = 0;

    document.getElementById('submitGuess').addEventListener('click', function() {
        const userGuess = Number(document.getElementById('guessInput').value);
        attempts++;

        let message = '';
        if (userGuess < randomNumber) {
            message = 'Too low! Try again.';
        } else if (userGuess > randomNumber) {
            message = 'Too high! Try again.';
        } else {
            message = `🎉 Congratulations! You guessed it in ${attempts} attempts. 🎉`;
            document.getElementById('correctSound').play();
            document.getElementById('restartGame').style.display = 'block';
        }

        document.getElementById('message').textContent = message;
        document.getElementById('guessInput').value = '';
    });

    document.getElementById('restartGame').addEventListener('click', function() {
        randomNumber = Math.floor(Math.random() * 100) + 1;
        attempts = 0;
        document.getElementById('message').textContent = '';
        document.getElementById('restartGame').style.display = 'none';
    });
</script>

</body>
</html>

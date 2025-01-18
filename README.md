# PRODIGY_WD_03
This is a simple Tic-Tac-Toe web application built using HTML, CSS, and JavaScript. The game allows two players to play against each other in a traditional grid format, where players take turns to place their marks ('X' or 'O') on the grid, aiming to get three markers in a row (either horizontally, vertically, or diagonally) to win.

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic-Tac-Toe</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f7f7f7;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }

        .game-container {
            text-align: center;
            background-color: #ffffff;
            padding: 40px;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            width: 400px;
        }

        h1 {
            color: #333;
            font-size: 2.5rem;
            margin-bottom: 20px;
        }

        .board {
            display: grid;
            grid-template-columns: repeat(3, 120px);
            grid-template-rows: repeat(3, 120px);
            gap: 15px;
            margin-bottom: 20px;
        }
        .square {
            width: 120px;
            height: 120px;
            background-color: #dfe6e9;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 2.5rem;
            font-weight: bold;
            cursor: pointer;
            border-radius: 10px;
            transition: transform 0.2s ease, background-color 0.3s ease;
        }
        .square:hover {
            background-color: #a4b0be;
            transform: scale(1.1);
        }

        .player-x {
            color: #ff6347; 
        }

        .player-o {
            color: #1e90ff; 
        }
        button {
            padding: 12px 20px;
            font-size: 1.2rem;
            background-color: #0984e3;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s ease;
            margin-top: 20px;
        }

        button:hover {
            background-color: #74b9ff;
        }
        #status {
            font-size: 1.2rem;
            color: #333;
            margin-top: 20px;
        }

    </style>
</head>
<body>
    <div class="game-container">
        <h1>Tic-Tac-Toe</h1>
        <div class="board" id="board">
           
            <div class="square" data-index="0"></div>
            <div class="square" data-index="1"></div>
            <div class="square" data-index="2"></div>
            <div class="square" data-index="3"></div>
            <div class="square" data-index="4"></div>
            <div class="square" data-index="5"></div>
            <div class="square" data-index="6"></div>
            <div class="square" data-index="7"></div>
            <div class="square" data-index="8"></div>
        </div>
        <button id="reset">Restart Game</button>
        <div id="status">Player X's turn</div>
    </div>

    <script>
        const board = Array(9).fill(null);
        let currentPlayer = 'X'; 
        let gameOver = false;
        const squares = document.querySelectorAll('.square');
        const status = document.getElementById('status');
        const resetButton = document.getElementById('reset');
        squares.forEach(square => {
            square.addEventListener('click', handleClick);
        });
        resetButton.addEventListener('click', resetGame);

        function handleClick(event) {
            const index = event.target.dataset.index;

            if (board[index] || gameOver) return; 
            board[index] = currentPlayer;
            event.target.textContent = currentPlayer;
            event.target.classList.add(`player-${currentPlayer.toLowerCase()}`);

            
            if (checkWinner()) {
                status.textContent = `${currentPlayer} wins!`;
                gameOver = true;
                return;
            }

            if (board.every(cell => cell !== null)) {
                status.textContent = "It's a draw!";
                gameOver = true;
                return;
            }

           
            currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
            status.textContent = `Player ${currentPlayer}'s turn`;
        }

        
        function checkWinner() {
            const winningCombos = [
                [0, 1, 2], [3, 4, 5], [6, 7, 8], 
                [0, 3, 6], [1, 4, 7], [2, 5, 8], 
                [0, 4, 8], [2, 4, 6]              
            ];

            return winningCombos.some(combo => {
                const [a, b, c] = combo;
                return board[a] && board[a] === board[b] && board[a] === board[c];
            });
        }

        function resetGame() {
            board.fill(null);
            gameOver = false;
            currentPlayer = 'X';
            squares.forEach(square => {
                square.textContent = '';
                square.classList.remove('player-x', 'player-o');
            });
            status.textContent = `Player ${currentPlayer}'s turn`;
        }
    </script>
</body>
</html>

<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tic Tac Toe — @ethsign Edition</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #0b0e12;
      color: #fff;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
    }
    h1 {
      color: #ff7a00;
    }
    #board {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      grid-gap: 5px;
    }
    .cell {
      width: 100px;
      height: 100px;
      background: #12161c;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 2rem;
      font-weight: bold;
      cursor: pointer;
      border-radius: 10px;
      color: #ff7a00;
    }
    .cell.taken {
      cursor: default;
    }
    #status {
      margin-top: 20px;
      font-size: 1.2rem;
    }
    button {
      margin-top: 15px;
      padding: 10px 20px;
      border: none;
      border-radius: 6px;
      background: #ff7a00;
      color: #000;
      font-weight: bold;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <h1>Tic Tac Toe — <span style="color:#ff7a00">@ethsign</span> Edition</h1>
  <div id="board"></div>
  <div id="status">Player $SIGN's turn</div>
  <button onclick="resetGame()">Reset</button>  <script>
    const boardEl = document.getElementById('board');
    const statusEl = document.getElementById('status');
    let board = Array(9).fill(null);
    let xIsNext = true;

    function renderBoard() {
      boardEl.innerHTML = '';
      board.forEach((cell, i) => {
        const cellEl = document.createElement('div');
        cellEl.classList.add('cell');
        if (cell) {
          cellEl.textContent = cell;
          cellEl.classList.add('taken');
        } else {
          cellEl.addEventListener('click', () => handleMove(i));
        }
        boardEl.appendChild(cellEl);
      });
    }

    function handleMove(i) {
      if (board[i] || calculateWinner()) return;
      board[i] = xIsNext ? '$SIGN' : '🍊';
      xIsNext = !xIsNext;
      renderBoard();
      const winner = calculateWinner();
      if (winner) {
        statusEl.textContent = winner === 'Draw' ? 'It\'s a draw!' : `${winner} wins!`;
      } else {
        statusEl.textContent = `Player ${xIsNext ? '$SIGN' : '🍊'}'s turn`;
      }
    }

    function calculateWinner() {
      const lines = [
        [0,1,2],[3,4,5],[6,7,8],
        [0,3,6],[1,4,7],[2,5,8],
        [0,4,8],[2,4,6]
      ];
      for (const [a,b,c] of lines) {
        if (board[a] && board[a] === board[b] && board[a] === board[c]) {
          return board[a];
        }
      }
      return board.every(Boolean) ? 'Draw' : null;
    }

    function resetGame() {
      board = Array(9).fill(null);
      xIsNext = true;
      statusEl.textContent = "Player $SIGN's turn";
      renderBoard();
    }

    renderBoard();
  </script></body>
</html>

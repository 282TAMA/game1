<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Permainan Tic-Tac-Toe</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f9;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
      animation: fadeIn 1s ease-in;
    }

    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }

    .game-container {
      text-align: center;
      border-radius: 10px;
      background-color: #fff;
      box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
      padding: 30px;
      width: 350px;
      animation: slideUp 0.6s ease-in;
    }

    @keyframes slideUp {
      from { transform: translateY(50px); opacity: 0; }
      to { transform: translateY(0); opacity: 1; }
    }

    .title {
      font-size: 24px;
      margin-bottom: 20px;
      font-weight: bold;
    }

    .board {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      grid-template-rows: repeat(3, 100px);
      gap: 5px;
      margin: 20px 0;
    }

    .cell {
      width: 100px;
      height: 100px;
      background-color: #e2e2e2;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 36px;
      font-weight: bold;
      cursor: pointer;
      border-radius: 8px;
      transition: background-color 0.3s;
    }

    .cell:hover {
      background-color: #c2c2c2;
    }

    .turn {
      margin-bottom: 20px;
    }

    .result {
      font-size: 18px;
      font-weight: bold;
      margin-top: 20px;
      color: #333;
    }

    .reset-btn {
      padding: 10px 20px;
      font-size: 16px;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      transition: background-color 0.3s;
    }

    .reset-btn:hover {
      background-color: #45a049;
    }
  </style>
</head>
<body>

<div class="game-container">
  <div class="title">Tama vs Yana</div>
  <div class="turn">Giliran: <span id="turn">Tama</span></div>
  <div class="board">
    <div class="cell" onclick="play(0)"></div>
    <div class="cell" onclick="play(1)"></div>
    <div class="cell" onclick="play(2)"></div>
    <div class="cell" onclick="play(3)"></div>
    <div class="cell" onclick="play(4)"></div>
    <div class="cell" onclick="play(5)"></div>
    <div class="cell" onclick="play(6)"></div>
    <div class="cell" onclick="play(7)"></div>
    <div class="cell" onclick="play(8)"></div>
  </div>
  <div class="result" id="result"></div>
  <button class="reset-btn" onclick="resetGame()">Mulai Ulang</button>
</div>

<script>
  let board = ['', '', '', '', '', '', '', '', '']; // Array untuk board
  let currentPlayer = 'Tama'; // Player pertama
  let gameOver = false;

  // Daftar kombinasi pemenang
  const winningCombos = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];

  // Fungsi untuk memainkan giliran
  function play(index) {
    if (gameOver || board[index] !== '') return; // Jangan bermain jika game selesai atau cell sudah terisi

    board[index] = currentPlayer === 'Tama' ? 'X' : 'O'; // Simpan simbol 'X' atau 'O'
    document.getElementsByClassName('cell')[index].innerText = board[index];

    // Periksa jika ada pemenang
    if (checkWinner()) {
      document.getElementById('result').innerText = `${currentPlayer} Menang!`;
      gameOver = true;
    } else if (board.every(cell => cell !== '')) {
      // Cek jika papan sudah penuh (seri)
      document.getElementById('result').innerText = 'Seri!';
      gameOver = true;
    } else {
      // Ganti giliran
      currentPlayer = currentPlayer === 'Tama' ? 'Yana' : 'Tama';
      document.getElementById('turn').innerText = currentPlayer;
    }
  }

  // Fungsi untuk memeriksa pemenang
  function checkWinner() {
    return winningCombos.some(combo => {
      const [a, b, c] = combo;
      return board[a] !== '' && board[a] === board[b] && board[a] === board[c];
    });
  }

  // Fungsi untuk mengulang permainan
  function resetGame() {
    board = ['', '', '', '', '', '', '', '', ''];
    currentPlayer = 'Tama';
    gameOver = false;
    document.getElementById('turn').innerText = currentPlayer;
    document.getElementById('result').innerText = '';
    const cells = document.getElementsByClassName('cell');
    for (let i = 0; i < cells.length; i++) {
      cells[i].innerText = '';
    }
  }
</script>

</body>
</html>

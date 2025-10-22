<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Para Minha Futura Espoa</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      font-family: 'Georgia', serif;
      background: linear-gradient(to bottom right, #4c1d95, #1e3a8a);
      color: #fff;
      text-align: center;
      overflow-x: hidden;
    }
    header { padding: 30px; font-size: 2em; font-weight: bold; }
    .carta {
      background: rgba(255, 255, 255, 0.1);
      margin: 20px auto; padding: 20px;
      border-radius: 15px; max-width: 900px;
      backdrop-filter: blur(8px);
      box-shadow: 0px 4px 15px rgba(0,0,0,0.5);
      display: none;
    }
    .texto { font-size: 1.2em; margin: 15px 0; line-height: 1.6em; min-height: 100px; }
    .galeria img, .galeria video {
      width: 100%; max-width: 500px; margin: 10px 0;
      border-radius: 12px; box-shadow: 0px 4px 10px rgba(0,0,0,0.5);
    }
    audio { margin-top: 20px; }

    /* Tela de senha */
    #senhaContainer {
      display: flex; flex-direction: column;
      justify-content: center; align-items: center; height: 100vh;
    }
    #senhaInput {
      padding: 10px; font-size: 18px; border-radius: 10px;
      border: none; outline: none; text-align: center;
    }
    #botaoSenha {
      margin-top: 15px; padding: 10px 20px; font-size: 18px;
      border: none; border-radius: 10px; background: #9333ea;
      color: white; cursor: pointer; transition: 0.3s;
    }
    #botaoSenha:hover { background: #7e22ce; }

    /* Corações */
    .heart { position: fixed; top: -10px; font-size: 20px; color: red;
      animation: fall 6s linear infinite; }
    @keyframes fall {
      to { transform: translateY(110vh) rotate(360deg); opacity: 0; }
    }

    /* Botões de jogos */
    .game-buttons { margin-top: 30px; }
    .game-buttons button {
      margin: 10px; padding: 10px 20px; font-size: 18px;
      border: none; border-radius: 10px; cursor: pointer;
      transition: 0.3s;
    }
    .velhaBtn { background: #ff4b5c; color: white; }
    .memoriaBtn { background: #22c55e; color: white; }
    .quizBtn { background: #3b82f6; color: white; }
    .game-buttons button:hover { opacity: 0.8; }

    /* Containers de jogos */
    .game-container { display: none; margin-top: 30px; }

    /* Jogo da Velha */
    .board { display: grid; grid-template-columns: repeat(3, 100px);
      gap: 10px; justify-content: center; }
    .cell { width: 100px; height: 100px; background: white; display: flex;
      align-items: center; justify-content: center; cursor: pointer;
      border-radius: 12px; font-weight: bold; overflow: hidden; }
    .cell img { width: 100%; height: 100%; object-fit: cover; border-radius: 12px; }
    .cell.taken { pointer-events: none; }
    #winner { margin-top: 20px; font-size: 1.5rem; font-weight: bold; }
    #resetBtn, #resetMemoria, #resetQuiz {
      margin-top: 20px; padding: 10px 20px; border: none;
      border-radius: 8px; background: #ff4b5c; color: white;
      font-size: 1rem; cursor: pointer;
    }

    /* Jogo da Memória */
    .memory-grid {
      display: grid;
      grid-template-columns: repeat(6, 100px);
      gap: 10px;
      justify-content: center;
    }
    .memory-card {
      width: 100px; height: 100px; background: #fff;
      border-radius: 10px; cursor: pointer;
      display: flex; align-items: center; justify-content: center;
      overflow: hidden; position: relative;
    }
    .memory-card img {
      width: 100%; height: 100%; object-fit: cover;
      display: none; border-radius: 10px;
    }
    .memory-card.flipped img { display: block; }

    /* Quiz */
    .quiz-question { font-size: 1.2em; margin-bottom: 15px; }
    .quiz-options button {
      display: block; margin: 5px auto;
      padding: 8px 15px; border: none; border-radius: 8px;
      background: #2563eb; color: white; cursor: pointer;
    }
    #quizResult { margin-top: 20px; font-size: 1.3em; font-weight: bold; }
  </style>
</head>
<body>
  <!-- Tela de senha -->
  <div id="senhaContainer">
    <h2>💌 Digite a senha para abrir sua carta 💌</h2>
    <input type="password" id="senhaInput" placeholder="Digite a senha">
    <button id="botaoSenha">Abrir Carta</button>
  </div>

  <!-- Conteúdo da carta -->
  <div class="carta" id="carta">
    <header>💌 Para Minha Princesa 💌</header>
    <div class="texto" id="texto"></div>

    <div class="galeria">
      <h2>📸 Nossas Fotos</h2>
      <img src="fotos/casal 01.jpg" alt="Foto 1">
      <img src="fotos/casal 02.jpg" alt="Foto 2">

      <h2>🎥 Momentos em Vídeo</h2>
      <video controls>
        <source src="video/video lindo.mp4" type="video/mp4">
        Seu navegador não suporta vídeo.
      </video>
    </div>

    <h2>🎶 Nossa Música</h2>
    <audio controls autoplay loop>
      <source src="music/musica.mp3" type="audio/mp3">
    </audio>

    <!-- Botões dos jogos -->
    <div class="game-buttons">
      <button class="velhaBtn" onclick="toggleGame('velha')">🎮 Jogo da Velha</button>
      <button class="memoriaBtn" onclick="toggleGame('memoria')">🃏 Jogo da Memória</button>
      <button class="quizBtn" onclick="toggleGame('quiz')">💘 Quiz de Casal</button>
    </div>

    <!-- Jogo da Velha -->
    <div class="game-container" id="velha">
      <h2>Jogo da Velha ❤️</h2>
      <div class="board" id="board"></div>
      <div id="winner"></div>
      <button id="resetBtn">Recomeçar</button>
    </div>

    <!-- Jogo da Memória -->
    <div class="game-container" id="memoria">
      <h2>Jogo da Memória 🃏</h2>
      <div class="memory-grid" id="memoryGrid"></div>
      <button id="resetMemoria">Recomeçar</button>
    </div>

    <!-- Quiz de Casal -->
    <div class="game-container" id="quiz">
      <h2>Quiz de Casal 💘</h2>
      <div id="quizContainer"></div>
      <button id="resetQuiz">Recomeçar</button>
      <div id="quizResult"></div>
    </div>
  </div>

  <script>
    const senhaCorreta = "123"; 

    document.getElementById("botaoSenha").addEventListener("click", () => {
      const senhaDigitada = document.getElementById("senhaInput").value;
      if (senhaDigitada === senhaCorreta) {
        document.getElementById("senhaContainer").style.display = "none";
        document.getElementById("carta").style.display = "block";
        iniciarCarta();
      } else alert("Senha incorreta! 💔");
    });

    // Texto animado
    function iniciarCarta() {
      const texto = "Meu amor, cada momento ao seu lado é único. Você é meu presente mais lindo, minha razão de sorrir e acreditar em dias melhores. Te amo infinitamente! ❤️";
      let i = 0;
      function typeWriter() {
        if (i < texto.length) {
          document.getElementById("texto").innerHTML += texto.charAt(i);
          i++; setTimeout(typeWriter, 50);
        }
      }
      typeWriter();
      setInterval(() => {
        const heart = document.createElement("div");
        heart.classList.add("heart"); heart.innerHTML = "❤️";
        heart.style.left = Math.random() * 100 + "vw";
        heart.style.fontSize = Math.random() * 20 + 15 + "px";
        document.body.appendChild(heart);
        setTimeout(() => heart.remove(), 6000);
      }, 500);
    }

    // Alternar jogos
    function toggleGame(id) {
      document.querySelectorAll('.game-container').forEach(g => g.style.display = "none");
      document.getElementById(id).style.display = "block";
    }

    /* ====== Jogo da Velha ====== */
    const board = document.getElementById("board");
    const winnerText = document.getElementById("winner");
    let currentPlayer = "X";
    const images = {
      "X": "fotos/01.jpg", // troque por suas fotos 
      "O": "fotos/02.webp"
    };
    function createBoard() {
      board.innerHTML = ""; winnerText.textContent = "";
      for (let i = 0; i < 9; i++) {
        const cell = document.createElement("div");
        cell.classList.add("cell");
        cell.addEventListener("click", () => makeMove(cell));
        board.appendChild(cell);
      }
    }
    function makeMove(cell) {
      if (!cell.hasChildNodes()) {
        const img = document.createElement("img");
        img.src = images[currentPlayer]; cell.appendChild(img);
        cell.classList.add("taken");
        if (checkWinner()) { winnerText.textContent = `🎉 ${currentPlayer} venceu!`; disableBoard(); return; }
        currentPlayer = currentPlayer === "X" ? "O" : "X";
      }
    }
    function checkWinner() {
      const cells = document.querySelectorAll(".cell");
      const combos = [[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];
      return combos.some(comb => comb.every(i => cells[i].hasChildNodes() && cells[i].firstChild.src.includes(images[currentPlayer])));
    }
    function disableBoard() { document.querySelectorAll(".cell").forEach(c => c.classList.add("taken")); }
    document.getElementById("resetBtn").addEventListener("click", () => { currentPlayer="X"; createBoard(); });
    createBoard();

    /* ====== Jogo da Memória ====== */
    const memoryGrid = document.getElementById("memoryGrid");
    let firstCard, secondCard, lockBoard=false;
    const fotos = [
      "fotos/01.jpg","fotos/02.webp","fotos/03.jpg","fotos/04.webp","fotos/casal 01.jpg","fotos/casal 02.jpg",
      "fotos/cr7 01.jpg","fotos/cr7 02.jpg","fotos/cr7 03.jpg","fotos/cr7 04.jpg","fotos/casal 03.jpg","fotos/casal 04.jpg"
    ];
    function loadMemory() {
      memoryGrid.innerHTML=""; 
      let cards = [...fotos, ...fotos];
      cards.sort(() => 0.5 - Math.random());
      cards.forEach(src => {
        const card = document.createElement("div");
        card.classList.add("memory-card");
        const img = document.createElement("img");
        img.src = src; card.appendChild(img);
        card.addEventListener("click", ()=>flipCard(card));
        memoryGrid.appendChild(card);
      });
    }
    function flipCard(card) {
      if(lockBoard || card.classList.contains("flipped")) return;
      card.classList.add("flipped");
      if(!firstCard) { firstCard=card; return; }
      secondCard=card; checkMatch();
    }
    function checkMatch() {
      lockBoard=true;
      let match = firstCard.firstChild.src===secondCard.firstChild.src;
      if(match) resetTurn(); else setTimeout(()=>{firstCard.classList.remove("flipped");secondCard.classList.remove("flipped");resetTurn();},1000);
    }
    function resetTurn() { [firstCard,secondCard]=[null,null]; lockBoard=false; }
    document.getElementById("resetMemoria").addEventListener("click", loadMemory);
    loadMemory();

    /* ====== Quiz de Casal ====== */
    const quizData = [
      {q:"Onde nos conhecemos?",o:["Na escola","Na internet","Num encontro"],a:1},
      {q:"Qual nosso mês mais especial?",o:["Janeiro","Abril","Dezembro"],a:1},
      {q:"Quem disse 'eu te amo' primeiro?",o:["Eu 😎","Você 😍","Dissemos juntos"],a:0},
      {q:"Nosso lugar favorito é:",o:["Praia","Cinema","Parque"],a:0},
      {q:"Qual comida você mais gosta?",o:["Pizza","Sushi","Hambúrguer"],a:2},
      {q:"Nossa primeira viagem foi para:",o:["Cidade vizinha","Praia","Serra"],a:1},
      {q:"Qual apelido mais carinhoso usamos?",o:["Amor","Princesa","Bebê"],a:1},
      {q:"Qual música lembra a gente?",o:["Romântica","Funk","Sertanejo"],a:0},
      {q:"Se pudéssemos viajar, iríamos para:",o:["Paris","Nova York","Maldivas"],a:2},
      {q:"O que mais define nosso amor?",o:["Amizade","Paixão","Companheirismo"],a:2}
    ];
    const quizContainer=document.getElementById("quizContainer");
    const quizResult=document.getElementById("quizResult");
    let currentQ=0, score=0;
    function loadQuiz() {
      quizResult.textContent=""; currentQ=0; score=0;
      showQuestion();
    }
    function showQuestion() {
      if(currentQ>=quizData.length){ quizResult.textContent=`Você acertou ${score}/${quizData.length} 💖`; return; }
      quizContainer.innerHTML="";
      const q=document.createElement("div"); q.classList.add("quiz-question"); q.textContent=quizData[currentQ].q;
      quizContainer.appendChild(q);
      const opts=document.createElement("div"); opts.classList.add("quiz-options");
      quizData[currentQ].o.forEach((opt,i)=>{
        const btn=document.createElement("button"); btn.textContent=opt;
        btn.onclick=()=>{ if(i===quizData[currentQ].a) score++; currentQ++; showQuestion(); };
        opts.appendChild(btn);
      });
      quizContainer.appendChild(opts);
    }
    document.getElementById("resetQuiz").addEventListener("click", loadQuiz);
    loadQuiz();
  </script>
</body>
</html>

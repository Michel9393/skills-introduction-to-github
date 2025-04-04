<!DOCTYPE html>
<html lang="it">
<head>
  <meta charset="UTF-8">
  <title>Alice e Michel</title>
  <style>
    body {
      margin: 0;
      font-family: "Comic Sans MS", cursive, sans-serif;
      background: #f0f8ff;
      overflow-x: hidden;
      position: relative;
    }
    /* Animazione per le scritte d’amore in background */
    .love-text {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      z-index: -1;
      overflow: hidden;
    }
    .love-text span {
      position: absolute;
      font-size: 2rem;
      color: rgba(255, 0, 0, 0.2);
      animation: float 10s infinite;
    }
    @keyframes float {
      0% { transform: translateY(100vh) rotate(0deg); opacity: 0; }
      50% { opacity: 1; }
      100% { transform: translateY(-100vh) rotate(360deg); opacity: 0; }
    }
    /* Header e titolo */
    header {
      background: #fff;
      padding: 20px;
      border-bottom: 2px solid #ccc;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    header h1 {
      margin: 0;
      font-size: 3rem;
      color: #000;
    }
    #clock {
      font-size: 1.2rem;
      color: #333;
    }
    /* Menu di navigazione */
    nav {
      background: #ffe4e1;
      padding: 10px;
      display: flex;
      justify-content: space-around;
      flex-wrap: wrap;
    }
    nav a {
      text-decoration: none;
      color: #000;
      padding: 10px 15px;
      border-radius: 5px;
      transition: background 0.3s;
    }
    nav a:hover {
      background: #ffb6c1;
    }
    /* Sezioni del sito */
    .section {
      padding: 20px;
      margin: 20px;
      background: #fff;
      border: 1px solid #ddd;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    /* Agenda/Calendario */
    #agenda {
      padding: 20px;
      margin: 20px;
      background: #e6ffe6;
      border: 1px solid #cfc;
      border-radius: 10px;
    }
    /* Pulsanti */
    .btn {
      padding: 5px 10px;
      margin: 5px;
      border: none;
      border-radius: 5px;
      background: #ff69b4;
      color: #fff;
      cursor: pointer;
    }
    .btn:hover {
      background: #ff1493;
    }
  </style>
</head>
<body>
  <!-- Scritte d'amore animate in background -->
  <div class="love-text" id="loveTextContainer"></div>

  <!-- Header con titolo e orologio -->
  <header>
    <h1>Alice e Michel</h1>
    <div id="clock"></div>
  </header>

  <!-- Menu di navigazione -->
  <nav>
    <a href="#entrate-uscite">Entrate / Uscite</a>
    <a href="#spese-mensili">Spese mensili fisse</a>
    <a href="#michel-lavoro">Michel lavoro</a>
    <a href="#alice-lavoro">Alice lavoro</a>
    <a href="#documenti">Documenti e sanitari</a>
    <a href="#percorso-michel">Percorso Michel</a>
    <a href="#cassetto-desideri">Cassetto dei desideri</a>
    <a href="#agenda">Agenda - Calendario</a>
  </nav>

  <!-- Sezioni del sito -->
  <section id="entrate-uscite" class="section">
    <h2>Entrate / Uscite</h2>
    <p>Inserisci qui le entrate (tue e di Alice) e le uscite (finanziamento, bollette, Vodafone, spesa, ordini cibo, aperitivi e cene fuori, unghie, abbonamento, sigarette).</p>
    <button class="btn">Aggiungi voce</button>
  </section>

  <section id="spese-mensili" class="section">
    <h2>Spese mensili fisse</h2>
    <p>Inserisci qui le spese fisse del mese.</p>
    <button class="btn">Aggiungi spesa</button>
  </section>

  <section id="michel-lavoro" class="section">
    <h2>Michel lavoro</h2>
    <p>Gestisci qui le cartelle e i file relativi al tuo lavoro (es. disoccupazione ecc.).</p>
    <button class="btn">Carica file</button>
  </section>

  <section id="alice-lavoro" class="section">
    <h2>Alice lavoro</h2>
    <p>Gestisci qui le cartelle e i file relativi al lavoro di Alice.</p>
    <button class="btn">Carica file</button>
  </section>

  <section id="documenti" class="section">
    <h2>Documenti e sanitari</h2>
    <p>Inserisci tutti i documenti importanti e sanitari.</p>
    <button class="btn">Carica documento</button>
  </section>

  <section id="percorso-michel" class="section">
    <h2>Percorso Michel</h2>
    <p>Spazio dedicato al progetto per smettere di fumare. Qui andranno le informazioni relative.</p>
    <button class="btn">Aggiungi aggiornamento</button>
  </section>

  <section id="cassetto-desideri" class="section">
    <h2>Cassetto dei desideri</h2>
    <p>Inserisci qui gli oggetti che vorresti acquistare. Se possibile, evidenzia in verde quelli accessibili in base ai risparmi.</p>
    <ul id="wishlist">
      <li data-price="100">Nuovo televisore <button class="btn">Elimina</button> <button class="btn">Modifica</button> <button class="btn">Acquistato</button></li>
      <li data-price="50">Cena romantica <button class="btn">Elimina</button> <button class="btn">Modifica</button> <button class="btn">Acquistato</button></li>
    </ul>
    <button class="btn">Aggiungi desiderio</button>
  </section>

  <section id="agenda" class="section">
    <h2>Agenda - Calendario</h2>
    <p>Aggiungi i tuoi impegni e ricevi alert per pagamenti o eventi importanti.</p>
    <form id="agendaForm">
      <label for="evento">Evento:</label>
      <input type="text" id="evento" name="evento" required>
      <br>
      <label for="dataEvento">Data e Ora:</label>
      <input type="datetime-local" id="dataEvento" name="dataEvento" required>
      <br>
      <button class="btn" type="submit">Aggiungi evento</button>
    </form>
    <ul id="eventList"></ul>
  </section>

  <script>
    // Aggiornamento dell'orologio
    function updateClock() {
      const now = new Date();
      document.getElementById("clock").textContent = now.toLocaleDateString('it-IT') + " " + now.toLocaleTimeString('it-IT');
    }
    setInterval(updateClock, 1000);
    updateClock();

    // Scritte d'amore animate in background
    const loveMessages = [
      "Ti amo",
      "Per sempre insieme",
      "Il nostro amore è magico",
      "Sei la mia stella",
      "Insieme, tutto è possibile"
    ];
    const loveContainer = document.getElementById("loveTextContainer");
    function createLoveMessage() {
      const span = document.createElement("span");
      span.textContent = loveMessages[Math.floor(Math.random() * loveMessages.length)];
      span.style.left = Math.random() * 100 + "%";
      span.style.top = Math.random() * 100 + "%";
      span.style.animationDuration = (8 + Math.random() * 4) + "s";
      loveContainer.appendChild(span);
      setTimeout(() => {
        loveContainer.removeChild(span);
      }, 10000);
    }
    setInterval(createLoveMessage, 3000);

    // Funzione base per l'agenda
    document.getElementById("agendaForm").addEventListener("submit", function(e) {
      e.preventDefault();
      const evento = document.getElementById("evento").value;
      const dataEvento = document.getElementById("dataEvento").value;
      const li = document.createElement("li");
      li.textContent = evento + " - " + new Date(dataEvento).toLocaleString('it-IT');
      document.getElementById("eventList").appendChild(li);
      this.reset();
    });
  </script>
</body>
</html>
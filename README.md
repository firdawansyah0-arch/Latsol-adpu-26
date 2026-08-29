<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <title>Latihan Soal Administrasi Negara</title>
  <link rel="stylesheet" href="style.css">
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <script src="script.js" defer></script>
</head>
<body>
  <header>
    <h1>Website Latihan Soal Prodi Administrasi Negara</h1>
    <nav>
      <button onclick="showPage('quiz')">Latihan Soal</button>
      <button onclick="showPage('materi')">Materi</button>
      <button onclick="showPage('dashboard')">Dashboard</button>
    </nav>
  </header>

  <main>
    <!-- Latihan Soal -->
    <section id="quiz" class="page">
      <h2>Latihan Soal</h2>
      <div id="question"></div>
      <div id="options"></div>
      <button onclick="nextQuestion()">Soal Berikutnya</button>
      <p id="result"></p>
    </section>

    <!-- Materi -->
    <section id="materi" class="page hidden">
      <h2>Materi Kuliah</h2>
      <p><strong>Kebijakan Publik:</strong> Kebijakan publik adalah keputusan pemerintah untuk mengatasi masalah masyarakat.</p>
      <p><strong>Manajemen Pemerintahan:</strong> Fokus pada pengelolaan sumber daya dan birokrasi untuk mencapai tujuan negara.</p>
    </section>

    <!-- Dashboard -->
    <section id="dashboard" class="page hidden">
      <h2>Dashboard</h2>
      <p>Total Soal Dikerjakan: <span id="total"></span></p>
      <p>Skor Benar: <span id="score"></span></p>
      <canvas id="scoreChart" width="400" height="200"></canvas>
    </section>
  </main>
</body>
</html>
body { font-family: Arial, sans-serif; margin: 0; background: #f4f4f4; }
header { background: #004080; color: white; padding: 10px; text-align: center; }
nav button { margin: 5px; padding: 10px; background: #0080ff; color: white; border: none; cursor: pointer; }
.page { padding: 20px; }
.hidden { display: none; }
button { margin-top: 10px; }
@media (max-width: 600px) {
  nav button { display: block; width: 100%; margin: 5px 0; }
}
const questions = [
  {
    text: "Apa definisi kebijakan publik?",
    options: ["Keputusan pemerintah", "Pendapat masyarakat", "Program swasta"],
    correct: 0,
    explanation: "Kebijakan publik adalah keputusan pemerintah untuk mengatasi masalah masyarakat."
  },
  {
    text: "Siapa yang bertanggung jawab atas manajemen pemerintahan?",
    options: ["Birokrasi", "Swasta", "Masyarakat umum"],
    correct: 0,
    explanation: "Manajemen pemerintahan dijalankan oleh birokrasi dan aparatur negara."
  }
];

let current = 0;
let score = 0;
let wrong = 0;
let chart;

function showPage(page) {
  document.querySelectorAll('.page').forEach(p => p.classList.add('hidden'));
  document.getElementById(page).classList.remove('hidden');
  if (page === 'quiz') loadQuestion();
  if (page === 'dashboard') updateDashboard();
}

function loadQuestion() {
  const q = questions[current];
  document.getElementById('question').innerText = q.text;
  const optionsDiv = document.getElementById('options');
  optionsDiv.innerHTML = "";
  q.options.forEach((opt, i) => {
    const btn = document.createElement('button');
    btn.innerText = opt;
    btn.onclick = () => checkAnswer(i);
    optionsDiv.appendChild(btn);
  });
}

function checkAnswer(i) {
  const q = questions[current];
  if (i === q.correct) {
    score++;
    document.getElementById('result').innerText = "✅ Benar!";
  } else {
    wrong++;
    document.getElementById('result').innerText = "❌ Salah. " + q.explanation;
  }
}

function nextQuestion() {
  current++;
  if (current < questions.length) {
    loadQuestion();
    document.getElementById('result').innerText = "";
  } else {
    document.getElementById('result').innerText = "Latihan selesai!";
  }
}

function updateDashboard() {
  document.getElementById('total').innerText = current;
  document.getElementById('score').innerText = score;

  const ctx = document.getElementById('scoreChart').getContext('2d');
  if (chart) chart.destroy();

  chart = new Chart(ctx, {
    type: 'bar',
    data: {
      labels: ['Benar', 'Salah'],
      datasets: [{
        label: 'Hasil Latihan',
        data: [score, wrong],
        backgroundColor: ['#4CAF50', '#F44336']
      }]
    },
    options: {
      responsive: true,
      plugins: { legend: { display: false } }
    }
  });
}


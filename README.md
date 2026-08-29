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

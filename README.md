<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>STOK GUDANG PEKANBARU</title>
  <link rel="icon" href="https://upload.wikimedia.org/wikipedia/en/3/33/Shell_logo.svg">
  <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/papaparse@5.3.2/papaparse.min.js"></script>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Inter', sans-serif;
      margin: 0;
      background-color: #fff;
      color: #222;
    }
    header {
      background: linear-gradient(90deg, #ffcc00 0%, #ff0000 100%);
      color: white;
      padding: 1rem 2rem;
      text-align: center;
      font-weight: 700;
      font-size: 1.8rem;
      letter-spacing: 0.5px;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 10px;
    }
    header img {
      height: 50px;
    }
    main {
      padding: 1rem 2rem;
    }
    table {
      border-collapse: collapse;
      width: 100%;
      margin-top: 1rem;
    }
    th, td {
      border: 1px solid #ddd;
      padding: 8px;
      text-align: left;
    }
    th {
      background-color: #ffcc00;
      color: #222;
      font-weight: 600;
    }
    tr:nth-child(even) {
      background-color: #f9f9f9;
    }
    .controls {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 1rem;
      flex-wrap: wrap;
      gap: 0.5rem;
    }
    input[type="text"] {
      padding: 0.5rem;
      border: 1px solid #ccc;
      border-radius: 6px;
      width: 200px;
    }
    button {
      background-color: #ff0000;
      color: white;
      border: none;
      padding: 0.6rem 1rem;
      border-radius: 6px;
      cursor: pointer;
      font-weight: 600;
    }
    button:hover {
      background-color: #cc0000;
    }
    footer {
      text-align: center;
      color: #777;
      padding: 1rem;
      font-size: 0.9rem;
    }
  </style>
</head>
<body>
  <header>
    <img src="https://upload.wikimedia.org/wikipedia/en/3/33/Shell_logo.svg" alt="Shell Logo" />
    STOK GUDANG PEKANBARU
  </header>

  <main>
    <div class="controls">
      <input type="text" id="searchInput" placeholder="Cari barang..." />
      <div>
        <button onclick="refreshData()">🔄 Refresh Data</button>
      </div>
    </div>

    <div id="tableContainer">Memuat data...</div>
  </main>

  <footer>
    © 2025 Gudang Pekanbaru - Data otomatis terupdate dari Google Sheets
  </footer>

  <script>
    const API_URL = 'https://script.google.com/macros/s/AKfycbwGlRyA2HeXdTu6Z4Hf5imLfScOttwDO8qNmhYoiO1EsY8OP1Zm3SL4goZdk-w9Ly4reQ/exec';
    let allData = [];

    async function fetchData() {
      try {
        document.getElementById('tableContainer').innerHTML = '⏳ Memuat data terbaru...';
        const response = await axios.get(`${API_URL}?t=${Date.now()}`);
        allData = response.data;
        renderTable(allData);
      } catch (error) {
        document.getElementById('tableContainer').innerHTML = '⚠️ Gagal memuat data.';
        console.error('Error fetching data:', error);
      }
    }

    function renderTable(data) {
      if (!data || data.length === 0) {
        document.getElementById('tableContainer').innerHTML = 'Tidak ada data ditemukan.';
        return;
      }

      const headers = Object.keys(data[0]);
      let html = '<table><thead><tr>' + headers.map(h => `<th>${h}</th>`).join('') + '</tr></thead><tbody>';
      data.forEach(row => {
        html += '<tr>' + headers.map(h => `<td>${row[h] || ''}</td>`).join('') + '</tr>';
      });
      html += '</tbody></table>';
      document.getElementById('tableContainer').innerHTML = html;
    }

    document.getElementById('searchInput').addEventListener('input', e => {
      const term = e.target.value.toLowerCase();
      const filtered = allData.filter(row => Object.values(row).some(v => String(v).toLowerCase().includes(term)));
      renderTable(filtered);
    });

    function refreshData() {
      fetchData();
    }

    // Auto refresh setiap 60 detik
    setInterval(fetchData, 60000);

    fetchData();
  </script>
</body>
</html>

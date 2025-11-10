<!doctype html>
<html lang="id">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>STOK GUDANG PEKANBARU</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
  <style>
    :root{
      --bg:#f7f8fb; /* light */
      --card:#ffffff;
      --text:#0b1720;
      --muted:#6b7280;
      --accent:#e41e26; /* shell red */
      --accent-2:#ffd200; /* shell yellow */
      --glass:rgba(11,23,32,0.03);
      --radius:12px;
      --shadow: 0 6px 18px rgba(11,23,32,0.08);
    }
    html,body{height:100%;margin:0;font-family:Inter,system-ui,-apple-system,"Segoe UI",Roboto,"Helvetica Neue",Arial;color:var(--text);background:var(--bg)}
    .wrap{max-width:1180px;margin:28px auto;padding:20px}
    header{display:flex;align-items:center;justify-content:space-between;gap:16px}
    .brand{display:flex;align-items:center;gap:12px}
    .logo{width:56px;height:56px;border-radius:10px;display:flex;align-items:center;justify-content:center;background:linear-gradient(180deg,var(--accent),#b71b20);box-shadow:var(--shadow)}
    .logo img{width:36px;height:36px}
    h1{margin:0;font-size:18px;font-weight:700}
    .sub{color:var(--muted);font-size:13px}

    .controls{display:flex;gap:10px;align-items:center}
    .search{padding:10px 12px;border-radius:10px;border:1px solid rgba(11,23,32,0.06);background:#fff;min-width:260px}
    .btn{padding:10px 14px;border-radius:10px;border:none;cursor:pointer;font-weight:600}
    .btn.primary{background:linear-gradient(90deg,var(--accent),#c31b23);color:white;box-shadow:0 8px 24px rgba(228,30,38,0.12)}
    .btn.ghost{background:transparent;border:1px solid rgba(11,23,32,0.06)}

    main{margin-top:18px}
    .panel{background:var(--card);border-radius:var(--radius);padding:14px;border:1px solid rgba(11,23,32,0.04);box-shadow:var(--shadow)}

    .toolbar{display:flex;align-items:center;justify-content:space-between;gap:12px;margin-bottom:12px}
    .stats{display:flex;gap:12px;align-items:center}
    .stat{background:linear-gradient(180deg,#fff,#fbfbfd);padding:10px 14px;border-radius:10px;border:1px solid rgba(11,23,32,0.03);min-width:120px}
    .stat .num{font-weight:700;font-size:18px}
    .viewToggle{display:flex;gap:8px}

    table{width:100%;border-collapse:collapse}
    thead th{background:linear-gradient(180deg,#fff,#fafafb);padding:12px;text-align:left;font-size:13px;border-bottom:1px solid rgba(11,23,32,0.05)}
    tbody td{padding:12px;border-bottom:1px solid rgba(11,23,32,0.03);vertical-align:middle}
    tbody tr:nth-child(even){background:rgba(11,23,32,0.012)}

    .cards{display:grid;grid-template-columns:repeat(auto-fill,minmax(260px,1fr));gap:12px}
    .card{background:linear-gradient(180deg,#fff,#fbfbfd);border-radius:12px;padding:12px;border:1px solid rgba(11,23,32,0.04)}
    .card .title{font-weight:700}
    .tags{display:flex;gap:8px;margin-top:8px}
    .tag{background:var(--glass);padding:6px 8px;border-radius:999px;font-size:12px;color:var(--muted);border:1px solid rgba(11,23,32,0.03)}

    footer{margin-top:12px;color:var(--muted);font-size:13px}
    @media (max-width:900px){.controls{flex-wrap:wrap}.search{min-width:140px;width:100%}}
  </style>
</head>
<body>
  <div class="wrap">
    <header>
      <div class="brand">
        <div class="logo" aria-hidden="true">
          <!-- simple shell-ish mark SVG -->
          <svg width="36" height="36" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M2 12c0 5.523 4.477 10 10 10s10-4.477 10-10H2z" fill="#FFD200"/>
            <path d="M6 12c0 3.314 2.686 6 6 6s6-2.686 6-6H6z" fill="#E41E26"/>
            <path d="M8.5 12c0 2.209 1.791 4 4 4s4-1.791 4-4H8.5z" fill="#fff" opacity="0.06"/>
          </svg>
        </div>
        <div>
          <h1>STOK GUDANG PEKANBARU</h1>
          <div class="sub">Sumber: Google Sheets — sheet: <strong>XLS SC - Balance</strong></div>
        </div>
      </div>

      <div class="controls">
        <input id="q" class="search" placeholder="Cari SKU atau Nama Barang..." />
        <div class="viewToggle">
          <button id="toggleView" class="btn ghost">Kartu</button>
          <button id="refresh" class="btn ghost">Refresh</button>
          <button id="download" class="btn primary">Download CSV</button>
        </div>
      </div>
    </header>

    <main>
      <div class="panel">
        <div class="toolbar">
          <div class="stats">
            <div class="stat">
              <div class="small">Total SKU</div>
              <div class="num" id="totalSku">—</div>
            </div>
            <div class="stat">
              <div class="small">Total Stok</div>
              <div class="num" id="totalStock">—</div>
            </div>
          </div>
          <div class="small" id="status">Memuat data...</div>
        </div>

        <div id="tableWrap">
          <table id="stokTable">
            <thead>
              <tr>
                <th>No</th>
                <th>SKU</th>
                <th>Nama Barang</th>
                <th>Category</th>
                <th>Pack</th>
                <th style="text-align:right">Balance</th>
                <th>Remarks</th>
              </tr>
            </thead>
            <tbody></tbody>
          </table>
        </div>

        <div id="cardsWrap" style="display:none;margin-top:12px">
          <div id="cards" class="cards"></div>
        </div>
      </div>

      <footer>Website ini otomatis menarik data dari Google Sheets. Pastikan sheet dapat diakses publik.</footer>
    </main>
  </div>

  <script>
    // CONFIG
    const SPREADSHEET_ID = '11qMnSGSs1SgiqsWsBtx62aNE8sx_98ZSOmR3t1lztn0';
    const SHEET_NAME = 'XLS SC - Balance';
    const AUTO_REFRESH_MS = 60_000;

    // Helper: parse gviz
    function gvizToJson(text){
      const m = text.match(/google\.visualization\.Query\.setResponse\((.*)\);/s);
      if(!m) throw new Error('Format gviz unexpected');
      return JSON.parse(m[1]);
    }

    function mapRow(cols,row){
      const obj = {};
      cols.forEach((c,i)=>{
        const label = (c.label||c.id||`col_${i}`).toString().trim();
        const cell = row.c && row.c[i] ? row.c[i].v : '';
        obj[label] = cell;
      });
      return obj;
    }

    async function fetchSheet(){
      const url = `https://docs.google.com/spreadsheets/d/${SPREADSHEET_ID}/gviz/tq?tqx=out:json&sheet=${encodeURIComponent(SHEET_NAME)}`;
      const resp = await fetch(url);
      const text = await resp.text();
      const js = gvizToJson(text);
      const cols = js.table.cols;
      const rows = js.table.rows || [];
      return rows.map(r=>mapRow(cols,r));
    }

    // UI & Data
    let DATA = [];

    function normalize(s){ return ('' + (s||'')).toString().toLowerCase(); }

    function toNumber(v){ const n = parseFloat((''+v).toString().replace(/[^0-9\-\.]/g,'')); return isNaN(n)?0:n; }

    function renderTable(items){
      const tbody = document.querySelector('#stokTable tbody'); tbody.innerHTML='';
      items.forEach(it=>{
        const tr = document.createElement('tr');
        tr.innerHTML = `
          <td>${it['Nomor']||''}</td>
          <td><strong>${it['SKU']||''}</strong></td>
          <td>${it['Product Code']||it['Nama Barang']||it['Product']||''}</td>
          <td>${it['Category']||it['CATEGORY']||it['Kategori']||''}</td>
          <td>${it['Pack']||it['PACK']||''}</td>
          <td style="text-align:right"><strong>${it['Balance']||''}</strong></td>
          <td>${it['Remarks']||it['Keterangan']||''}</td>
        `;
        tbody.appendChild(tr);
      });
    }

    function renderCards(items){
      const wrap = document.getElementById('cards'); wrap.innerHTML='';
      items.forEach(it=>{
        const card = document.createElement('div'); card.className='card';
        card.innerHTML = `
          <div style="display:flex;justify-content:space-between;align-items:center">
            <div>
              <div style="font-size:13px;color:var(--muted)">SKU</div>
              <div class="title">${it['SKU']||''}</div>
            </div>
            <div style="text-align:right">
              <div style="font-size:12px;color:var(--muted)">Stok Akhir</div>
              <div style="font-size:20px;color:var(--accent)"><strong>${it['Balance']||''}</strong></div>
            </div>
          </div>
          <div style="margin-top:10px;font-weight:600">${it['Product Code']||it['Nama Barang']||''}</div>
          <div class="tags">
            <span class="tag">${it['Category']||''}</span>
            <span class="tag">${it['Pack']||''}</span>
          </div>
          <div style="margin-top:8px;font-size:13px;color:var(--muted)">Remarks: ${it['Remarks']||''}</div>
        `;
        wrap.appendChild(card);
      });
    }

    function applyFilter(){
      const q = normalize(document.getElementById('q').value);
      const filtered = DATA.filter(it=>{
        return normalize(it['SKU']).includes(q) || normalize(it['Product Code']).includes(q) || normalize(it['Product']).includes(q) || normalize(it['Category']).includes(q);
      });
      renderTable(filtered); renderCards(filtered);
      document.getElementById('totalSku').textContent = filtered.length;
      const total = filtered.reduce((s,item)=> s + toNumber(item['Balance']||item['Saldo Akhir']||0), 0);
      document.getElementById('totalStock').textContent = Intl.NumberFormat().format(total);
      document.getElementById('status').textContent = `Menampilkan ${filtered.length} item • Terakhir sinkron: ${new Date().toLocaleString()}`;
      return filtered;
    }

    document.getElementById('q').addEventListener('input', applyFilter);
    document.getElementById('toggleView').addEventListener('click', ()=>{
      const t = document.getElementById('tableWrap'); const c = document.getElementById('cardsWrap');
      if(t.style.display === 'none'){ t.style.display='block'; c.style.display='none'; document.getElementById('toggleView').textContent='Kartu'; }
      else { t.style.display='none'; c.style.display='block'; document.getElementById('toggleView').textContent='Tabel'; }
    });

    document.getElementById('refresh').addEventListener('click', loadAndShow);
    document.getElementById('download').addEventListener('click', ()=>{
      const rows = applyFilter();
      const cols = ['Nomor','SKU','Product Code','Category','Pack','Initial Stock','Accumulative IN','Accumulative OUT','Adjustment','Balance','Remarks'];
      const csv = [cols.join(',')].concat(rows.map(r=>cols.map(c=>`"${(r[c]||'').toString().replace(/"/g,'""')}"`).join(','))).join('
');
      const blob = new Blob([csv],{type:'text/csv'}); const url = URL.createObjectURL(blob);
      const a = document.createElement('a'); a.href=url; a.download='stok-gudang-pekanbaru.csv'; a.click(); URL.revokeObjectURL(url);
    });

    async function loadAndShow(){
      try{
        document.getElementById('status').textContent = 'Memuat data...';
        const rows = await fetchSheet();
        DATA = rows.map(r=>({
          'Nomor': r['Nomor'] || r['No'] || r['nomor'] || '',
          'SKU': r['SKU'] || r['Nomor Material'] || r['Material'] || r['Nomor_Material'] || '',
          'Product Code': r['Product Code'] || r['Product_Code'] || r['Nama Barang'] || r['Product'] || r['ProductName'] || '',
          'Category': r['Category'] || r['CATEGORY'] || r['Kategori'] || '',
          'Pack': r['Pack'] || r['PACK'] || r['Jenis PACK'] || '',
          'Initial Stock': r['Initial Stock'] || r['Initial_Stock'] || r['Initial'] || '',
          'Accumulative IN': r['Accumulative IN'] || r['Accumulative_IN'] || r['Masuk'] || r['In'] || '',
          'Accumulative OUT': r['Accumulative OUT'] || r['Accumulative_OUT'] || r['Keluar'] || r['Out'] || '',
          'Adjustment': r['Adjustment'] || r['Adj'] || '',
          'Balance': r['Balance'] || r['Saldo Akhir'] || r['Stok Akhir'] || '',
          'Remarks': r['Remarks'] || r['Keterangan'] || r['Notes'] || ''
        }));
        applyFilter();
      }catch(err){
        console.error(err);
        document.getElementById('status').textContent = 'Gagal memuat data — pastikan sheet dapat diakses publik dan nama sheet benar.';
      }
    }

    // init
    loadAndShow();
    setInterval(loadAndShow, AUTO_REFRESH_MS);
  </script>
</body>
</html>

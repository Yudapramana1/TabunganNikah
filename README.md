# TabunganNikah
<!doctype html>
<html lang="id">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Tabungan Nikah - Target 250.000.000</title>
  <style>
    :root{--bg:#0f172a;--card:#0b1220;--accent:#06b6d4;--muted:#94a3b8}
    *{box-sizing:border-box}
    body{font-family:Inter,system-ui,Segoe UI,Roboto,Helvetica,Arial; margin:0; min-height:100vh; background:linear-gradient(180deg,#071024 0%, #07112a 100%); color:#e6eef6; display:flex; align-items:center; justify-content:center; padding:24px}
    .wrap{width:100%;max-width:900px}
    header{display:flex;align-items:center;justify-content:space-between;margin-bottom:18px}
    h1{font-size:20px;margin:0}
    .card{background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01)); padding:20px; border-radius:12px; box-shadow:0 6px 24px rgba(2,6,23,0.6)}
    .grid{display:grid;grid-template-columns:1fr 320px;gap:18px}
    .summary{display:flex;flex-direction:column;gap:12px}
    .big{font-size:28px;font-weight:700}
    .muted{color:var(--muted);font-size:14px}
    .progress-wrap{background:#071228;border-radius:12px;padding:12px}
    .bar{background:#082035;border-radius:8px;height:18px;overflow:hidden}
    .bar > i{display:block;height:100%;background:linear-gradient(90deg,var(--accent),#7c3aed);width:0%;transition:width 600ms ease}
    .controls{display:flex;gap:8px;flex-wrap:wrap}
    button{background:transparent;border:1px solid rgba(255,255,255,0.06);padding:8px 12px;border-radius:8px;color:inherit;cursor:pointer}
    .primary{background:linear-gradient(90deg,var(--accent),#7c3aed);border:none;color:#021026;font-weight:600}
    input[type=number]{padding:8px;border-radius:8px;border:1px solid rgba(255,255,255,0.06);background:transparent;color:inherit;width:160px}
    .countdown{display:flex;gap:8px;flex-wrap:wrap}
    .cd-box{background:#021022;padding:12px;border-radius:10px;min-width:80px;text-align:center}
    .cd-num{font-weight:700;font-size:18px}
    footer{display:flex;justify-content:space-between;align-items:center;margin-top:12px}
    .small{font-size:13px;color:var(--muted)}
    .danger{background:transparent;border:1px solid rgba(255,80,80,0.12);color:#ff8b8b}
    .edit-btn,.delete-btn{font-size:11px;padding:2px 6px;margin-left:6px;border-radius:6px}
    .edit-btn{border:1px solid rgba(80,200,255,0.3);color:#50c8ff}
    .delete-btn{border:1px solid rgba(255,80,80,0.3);color:#ff8080}
    @media (max-width:860px){.grid{grid-template-columns:1fr;}.card{padding:16px}}
  </style>
</head>
<body>
  <div class="wrap">
    <header>
      <h1>Tabungan Nikah — Target: Rp 250.000.000</h1>
      <div class="small">Aplikasi berbasis web (Private). Simpanan disimpan di browser (localStorage).</div>
    </header>

    <div class="grid">
      <section class="card">
        <div class="summary">
          <div>
            <div class="muted">Target</div>
            <div class="big">Rp <span id="targetAmount">250.000.000</span></div>
          </div>

          <div class="progress-wrap">
            <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:8px">
              <div>
                <div class="muted">Terkumpul</div>
                <div class="big">Rp <span id="savedAmount">0</span></div>
              </div>
              <div style="text-align:right">
                <div class="muted">Sisa</div>
                <div id="remaining" class="big">Rp 250.000.000</div>
              </div>
            </div>

            <div class="bar"><i id="barFill"></i></div>
            <div style="display:flex;justify-content:space-between;margin-top:8px">
              <div class="muted">Progress: <span id="percent">0%</span></div>
              <div class="muted">Tanggal target: <span id="targetDate"></span></div>
            </div>
          </div>

          <div style="display:flex;flex-direction:column;gap:10px;margin-top:12px">
            <div style="display:flex;gap:8px;align-items:center">
              <input id="addAmount" type="number" placeholder="Masukkan jumlah (contoh: 150000)" min="0" />
              <button id="addBtn" class="primary">Tambah</button>
              <button id="resetBtn" class="danger">Reset Semua</button>
            </div>

            <div class="controls">
              <button data-amt="50000">+50.000</button>
              <button data-amt="100000">+100.000</button>
              <button data-amt="500000">+500.000</button>
              <button data-amt="1000000">+1.000.000</button>
              <button data-amt="5000000">+5.000.000</button>
            </div>

            <div class="muted">Riwayat (dapat diedit/hapus):</div>
            <div id="history" style="max-height:200px;overflow:auto;background:#061022;padding:10px;border-radius:8px;border:1px solid rgba(255,255,255,0.02)"></div>
          </div>
        </div>
      </section>

      <aside class="card">
        <h3 style="margin-top:0">Countdown 5 tahun dari sekarang</h3>
        <div class="muted" style="margin-bottom:8px">Hitung mundur menuju tanggal target (5 tahun sejak saat ini).</div>

    <div style="margin-bottom:12px" class="countdown">
        <div class="cd-box"><div class="cd-num" id="cdYears">0</div><div class="muted">tahun</div></div>
        <div class="cd-box"><div class="cd-num" id="cdDays">0</div><div class="muted">hari</div></div>
        <div class="cd-box"><div class="cd-num" id="cdHours">0</div><div class="muted">jam</div></div>
        <div class="cd-box"><div class="cd-num" id="cdMinutes">0</div><div class="muted">mnt</div></div>
        <div class="cd-box"><div class="cd-num" id="cdSeconds">0</div><div class="muted">dtk</div></div>
    </div>
        <div class="muted" style="margin-bottom:10px">Tanggal target: <strong id="targetDateFull"></strong></div>
        <div class="muted">Petunjuk:</div>
        <ul class="muted">
          <li>Persiapan Diri & Niat.</li>
          <li>Komunikasi dengan Pasangan.</li>
          <li>Persiapan Finansial.</li>
          <li>Restu Orang Tua.</li>
          <li>Kesiapan Mental & Emosi.</li>
          <li>Kehidupan Setelah Menikah.</li>
          <li>Ingat Tujuan Utama.</li>
        </ul>
      </aside>
    </div>

    <footer>
      <div class="small">© 2025 Lang. HTML + JS + CSS + Github.</div>
      <div class="small">Tabungan Pernikahan</div>
    </footer>
  </div>

<script>
(function(){
  const TARGET = 250000000;
  const STORAGE_KEY = 'tabungan_nikah_250j_amount';
  const STORAGE_HISTORY = 'tabungan_nikah_250j_history';

  const historyEl = document.getElementById('history');
  const savedEl = document.getElementById('savedAmount');
  const remainingEl = document.getElementById('remaining');
  const percentEl = document.getElementById('percent');
  const barFill = document.getElementById('barFill');
  const targetAmountEl = document.getElementById('targetAmount');
  const targetDateEl = document.getElementById('targetDate');
  const targetDateFullEl = document.getElementById('targetDateFull');

  const now = new Date();
  const targetDate = new Date(now.getTime());
  targetDate.setFullYear(targetDate.getFullYear() + 5);

  targetDateEl.textContent = targetDate.toLocaleDateString('id-ID');
  targetDateFullEl.textContent = targetDate.toLocaleString('id-ID');
  targetAmountEl.textContent = formatCurrency(TARGET);

  let saved = loadAmount();
  let transactionHistory = loadHistory();

  function formatCurrency(n){ return Number(n).toLocaleString('id-ID'); }

  function render(){
    savedEl.textContent = formatCurrency(saved);
    const remaining = Math.max(0, TARGET - saved);
    remainingEl.textContent = 'Rp ' + formatCurrency(remaining);
    const pct = Math.min(100, Math.round((saved / TARGET) * 10000) / 100);
    percentEl.textContent = pct + '%';
    barFill.style.width = pct + '%';
    renderHistory();
  }

  function renderHistory(){
    if(transactionHistory.length === 0){ historyEl.innerHTML = '<div class="muted">Belum ada transaksi.</div>'; return }
    historyEl.innerHTML = '';
    transactionHistory.slice().reverse().forEach((item, idx)=>{
      const div = document.createElement('div');
      div.style.padding='6px 8px';
      div.style.borderBottom='1px solid rgba(255,255,255,0.02)';
      const realIndex = transactionHistory.length-1-idx;
      div.innerHTML = `<div style="display:flex;justify-content:space-between;align-items:center">`+
        `<div><div style=\"font-size:13px\">${item.note}</div>`+
        `<div class=\"muted\" style=\"font-size:12px\">${new Date(item.when).toLocaleString('id-ID')}</div></div>`+
        `<div><strong>Rp ${formatCurrency(item.amt)}</strong>`+
        `<button class=\"edit-btn\" data-index=\"${realIndex}\">Edit</button>`+
        `<button class=\"delete-btn\" data-index=\"${realIndex}\">Hapus</button></div>`+
      `</div>`;
      historyEl.appendChild(div);
    })

    historyEl.querySelectorAll('.edit-btn').forEach(btn=>{
      btn.addEventListener('click', ()=>{
        const idx = Number(btn.dataset.index);
        const newAmt = prompt('Masukkan jumlah baru:', transactionHistory[idx].amt);
        if(newAmt && !isNaN(newAmt)){
          saved -= transactionHistory[idx].amt;
          transactionHistory[idx].amt = Number(newAmt);
          saved += transactionHistory[idx].amt;
          saveAll(); render();
        }
      });
    });

    historyEl.querySelectorAll('.delete-btn').forEach(btn=>{
      btn.addEventListener('click', ()=>{
        const idx = Number(btn.dataset.index);
        if(confirm('Hapus transaksi ini?')){
          saved -= transactionHistory[idx].amt;
          transactionHistory.splice(idx,1);
          saveAll(); render();
        }
      });
    });
  }

  function saveAll(){
    try{ localStorage.setItem(STORAGE_KEY, String(saved)); localStorage.setItem(STORAGE_HISTORY, JSON.stringify(transactionHistory)); }catch(e){}
  }
  function loadAmount(){
    try{ const v=localStorage.getItem(STORAGE_KEY); return v?Number(v):0 }catch(e){return 0}
  }
  function loadHistory(){
    try{ const h=localStorage.getItem(STORAGE_HISTORY); return h?JSON.parse(h):[] }catch(e){return []}
  }

  render();

  function addMoney(amount, note){
    amount = Number(amount);
    if(isNaN(amount) || amount<=0) return;
    saved += amount;
    transactionHistory.push({amt:amount, when: Date.now(), note});
    saveAll(); render();
  }

  document.querySelectorAll('button[data-amt]').forEach(btn=>{
    btn.addEventListener('click', ()=>{ const amt = Number(btn.dataset.amt)||0; if(amt>0) addMoney(amt, `Tambah cepat +Rp ${formatCurrency(amt)}`); });
  });
  document.getElementById('addBtn').addEventListener('click', ()=>{
    const v = Number(document.getElementById('addAmount').value);
    if(!v || v<=0){ alert('Masukkan jumlah yang valid'); return }
    addMoney(Math.floor(v), 'Tambah manual');
    document.getElementById('addAmount').value = '';
  });
  document.getElementById('resetBtn').addEventListener('click', ()=>{
    if(!confirm('Reset seluruh tabungan?')) return;
    saved=0;transactionHistory=[];saveAll();render();
  });

  // countdown
    const cdYears = document.getElementById('cdYears');
    const cdDays = document.getElementById('cdDays');
    const cdHours = document.getElementById('cdHours');
    const cdMinutes = document.getElementById('cdMinutes');
    const cdSeconds = document.getElementById('cdSeconds');
    function tickCountdown(){
        const now = new Date();
        let years = targetDate.getFullYear()-now.getFullYear();
        if(new Date(now.getFullYear()+years, now.getMonth(), now.getDate())>targetDate){ years--; }
     let temp = new Date(now.getTime()); temp.setFullYear(temp.getFullYear()+years);
        let diff = targetDate-temp;
        const days=Math.floor(diff/(1000*60*60*24));diff-=days*86400000;
        const hours=Math.floor(diff/(1000*60*60));diff-=hours*3600000;
        const minutes=Math.floor(diff/(1000*60));diff-=minutes*60000;
        const seconds=Math.floor(diff/1000);
        cdYears.textContent=years;cdDays.textContent=days;cdHours.textContent=hours;cdMinutes.textContent=minutes;cdSeconds.textContent=seconds;
    }
    tickCountdown(); setInterval(tickCountdown,1000);
})();
</script>
</body>
</html>

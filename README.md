# behavioral-biometrics-UX-UI[index.html](https://github.com/user-attachments/files/23864069/index.html)
<!doctype html>
<html lang="ar" dir="rtl">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>سِمت — نموذج البصمة السلوكية</title>

<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<style>
:root{
  --bg:#0b1220;
  --card:#0f1724;
  --muted:#98a2b3;
  --accent1:#4f46e5;
  --accent2:#06b6d4;
  --glass: rgba(255,255,255,0.03);
  --radius:14px;
}
*{box-sizing:border-box;font-family: "Tajawal", system-ui, Arial, sans-serif}
html,body{height:100%;margin:0;background:linear-gradient(180deg,#071025 0%, #081229 100%);color:#e6eef8}
.app{max-width:1100px;margin:18px auto;padding:18px}
header{display:flex;align-items:center;gap:12px}
.logo{width:64px;height:64px;border-radius:12px;display:flex;align-items:center;justify-content:center;background:linear-gradient(135deg,var(--accent1),var(--accent2));font-weight:800;font-size:20px}
h1{margin:0;font-size:20px}
.sub{color:var(--muted);font-size:13px}
.top-actions{margin-inline-start:auto;display:flex;gap:8px;align-items:center}
.btn{background:transparent;border:1px solid rgba(255,255,255,0.06);color:inherit;padding:8px 12px;border-radius:10px;cursor:pointer}
.btn.primary{background:linear-gradient(90deg,var(--accent1),var(--accent2));border:none;font-weight:700}
.card{background:var(--card);padding:18px;border-radius:var(--radius);box-shadow:0 8px 30px rgba(0,0,0,0.6);margin-top:16px}
nav{display:flex;gap:8px;margin-top:14px}
nav .tab{padding:8px 12px;border-radius:10px;background:transparent;border:1px solid rgba(255,255,255,0.02);cursor:pointer;color:var(--muted)}
nav .tab.active{background:linear-gradient(90deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));color:#fff;border:1px solid rgba(255,255,255,0.06)}
.layout{display:grid;grid-template-columns:1fr 360px;gap:16px;margin-top:16px}
@media(max-width:980px){.layout{grid-template-columns:1fr}}
.panel{margin-bottom:14px}
.stat-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:12px}
@media(max-width:760px){.stat-grid{grid-template-columns:1fr}}
.stat{padding:12px;border-radius:10px;background:var(--glass)}
.stat h4{margin:0;color:var(--muted);font-size:13px}
.stat p{margin:6px 0 0;font-size:20px;font-weight:700}
.list{margin-top:12px;display:flex;flex-direction:column;gap:8px}
.list .item{display:flex;justify-content:space-between;align-items:center;padding:12px;border-radius:10px;background:rgba(255,255,255,0.02)}
.chip{background:#081223;padding:6px 8px;border-radius:8px;color:var(--muted);font-size:13px}
.small{font-size:13px;color:var(--muted)}
.login-box{max-width:420px;margin:18px auto}
.input{width:100%;padding:12px;border-radius:10px;border:1px solid rgba(255,255,255,0.04);background:transparent;color:inherit;margin-top:8px}
label{display:block;color:var(--muted);font-size:13px;margin-top:6px}
.center{text-align:center}
aside .card{position:sticky;top:20px}
.alert-high{background:linear-gradient(90deg, rgba(239,68,68,0.12), rgba(239,68,68,0.06));border-left:4px solid rgba(239,68,68,0.9);padding:12px;border-radius:10px}
.explain{font-size:13px;color:var(--muted);margin-top:8px}
.footer{margin-top:18px;text-align:center;color:var(--muted);font-size:13px}
.modal-back{position:fixed;inset:0;display:none;align-items:center;justify-content:center;background:rgba(3,7,18,0.6);z-index:200}
.modal{background:#071428;padding:18px;border-radius:12px;max-width:640px;width:94%;box-shadow:0 12px 40px rgba(0,0,0,0.6)}
.row{display:flex;gap:12px;align-items:center}
.muted{color:var(--muted)}
.small-muted{font-size:12px;color:var(--muted)}
.pill{display:inline-block;padding:6px 10px;border-radius:999px;background:rgba(255,255,255,0.03);font-size:13px;color:var(--muted)}
.kv{display:flex;justify-content:space-between;padding:10px;border-radius:8px;background:rgba(255,255,255,0.01);margin-top:8px}
</style>
</head>
<body>
<div class="app">
<header>
  <div class="logo">سِم</div>
  <div>
    <h1>سِمت — نموذج البصمة السلوكية</h1>
    <div class="sub">Proof-of-Concept لرفع أمان الهوية الرقمية</div>
  </div>
  <div class="top-actions">
    <button class="btn" id="downloadBtn" title="حفظ المشروع">تنزيل ZIP</button>
    <button class="btn" onclick="openModal('help')"><i class="fa-solid fa-circle-info"></i> المساعدة</button>
  </div>
</header>

<nav class="card" id="mainNav">
  <div class="tab active" data-screen="login" onclick="go('login', this)">تسجيل الدخول</div>
  <div class="tab" data-screen="dashboard" onclick="go('dashboard', this)">لوحة التحكم</div>
  <div class="tab" data-screen="analysis" onclick="go('analysis', this)">تحليل السلوك</div>
  <div class="tab" data-screen="alerts" onclick="go('alerts', this)">التنبيهات</div>
  <div class="tab" data-screen="integration" onclick="go('integration', this)">تكامل & خطة</div>
</nav>

<div class="layout">
  <main>
    <section id="login" class="card screen active">
      <div style="display:flex;gap:12px;align-items:center;justify-content:space-between">
        <div>
          <h3 style="margin:0">تسجيل الدخول</h3>
          <div class="small muted">محاكاة لالتقاط البصمة السلوكية أثناء الإدخال</div>
        </div>
        <div class="pill">MVP — Prototype</div>
      </div>
      <div class="login-box">
        <label>اسم المستخدم</label>
        <input id="userInput" class="input" placeholder="مثال: nnov" />
        <label>محاكاة الكتابة (اكتب بسرعة أو ببطء)</label>
        <input id="typingInput" class="input" placeholder="ابدأ بالكتابة هنا..." />
        <div style="display:flex;gap:8px;margin-top:12px">
          <button class="btn primary" onclick="performCheck()">تحقق السلوكي</button>
          <button class="btn" onclick="simulateAttackDetailed()">Simulate Attack</button>
        </div>
        <div class="explain small-muted">ملاحظة: الخوارزمية هنا محاكاة لعرض الفكرة فقط.</div>
      </div>
    </section>

    <section id="dashboard" class="card screen" style="display:none">
      <div class="panel">
        <div class="stat-grid">
          <div class="stat">
            <h4>إجمالي محاولات اليوم</h4>
            <p id="statTotal">1,254</p>
          </div>
          <div class="stat">
            <h4>محاولات مشبوهة</h4>
            <p id="statSus">3</p>
          </div>
          <div class="stat">
            <h4>متوسط الثقة</h4>
            <p id="statConf">82%</p>
          </div>
        </div>
      </div>

      <div class="panel card">
        <div style="display:flex;justify-content:space-between;align-items:center">
          <h3 style="margin:0">مخطط مستوى الثقة خلال اليوم</h3>
          <div class="small-muted">عرض توضيحي</div>
        </div>
        <canvas id="confChart" style="max-height:260px;margin-top:12px"></canvas>
      </div>
    </section>

    <section id="analysis" class="card screen" style="display:none">
      <h3 style="margin:0">تحليل السلوك (Explainability)</h3>
      <div class="muted small" style="margin-top:8px">سبب الاشتباه والميزات التي أثرت في القرار</div>
      <div class="card" style="margin-top:12px">
        <div class="kv"><div class="muted">جلسة</div><div id="kvSession">—</div></div>
        <div class="kv"><div class="muted">نسبة الثقة</div><div id="kvScore">—</div></div>
        <div class="kv"><div class="muted">سبب الاشتباه</div><div id="kvReason">—</div></div>
        <div style="margin-top:12px" class="small-muted">عناصر نموذجية تؤثر: مدة اللمسة، متوسط المسافة بين اللمسات، سرعة التمرير، زاوية الجهاز</div>
      </div>
    </section>

    <section id="alerts" class="card screen" style="display:none">
      <h3 style="margin:0">قائمة التنبيهات</h3>
      <div class="muted small">أحدث المحاولات المشبوهة</div>
      <div class="list" id="alertsList" style="margin-top:12px"></div>
    </section>

    <section id="integration" class="card screen" style="display:none">
      <h3 style="margin:0">تكامل مع أبشر — One-pager</h3>
      <div class="muted small" style="margin-top:8px">خلاصة سريعة لتكامل النظام مع منظومة حكومية</div>
      <div class="card" style="margin-top:12px">
        <div class="kv"><div class="muted">API</div><div>POST /risk/behavioral</div></div>
        <div class="kv"><div class="muted">Payload</div><div>user_id_hash, features[], timestamp</div></div>
        <div class="kv"><div class="muted">Response</div><div>{ score:0-100, action: allow/challenge/block }</div></div>
      </div>
    </section>
  </main>

  <aside>
    <div class="card" style="margin-top:12px">
      <h4 style="margin:0">تنبيه توضيحي</h4>
      <div class="alert-high" style="margin-top:10px">
        <strong>محاكاة:</strong> عند الاشتباه نقترح إظهار تحدّي OTP أو تعطيل الجلسة مؤقتًا.
      </div>
      <div style="margin-top:12px" class="small-muted">احفظ نسخة العرض (PDF) وارفق ملف README يشرح فتح index.html</div>
    </div>
  </aside>
</div>
</div>

<script>
let alerts = [
  {id:1, text:'محاولة دخول من جهاز جديد', level:'متوسط', time:'09:15'},
  {id:2, text:'سلوك كتابة غير نمطي', level:'عالي', time:'10:42'}
];

function go(screen, el){
  document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
  if(el) el.classList.add('active');
  document.querySelectorAll('.screen').forEach(s=>s.style.display='none');
  document.getElementById(screen).style.display='block';
  if(screen==='dashboard') renderDashboard();
  if(screen==='alerts') renderAlerts();
}

function renderDashboard(){
  document.getElementById('statTotal').innerText = 1254;
  document.getElementById('statSus').innerText = alerts.length;
  document.getElementById('statConf').innerText = '82%';
  if(!window._chartInit){initChart();window._chartInit=true;}
  else updateChart();
}

function renderAlerts(){
  const el = document.getElementById('alertsList');
  el.innerHTML = alerts.map(a=>`<div class="item"><div><strong>${a.text}</strong><br><span class="small-muted">${a.time}</span></div><div style="text-align:right"><div class="pill">${a.level}</div><div style="margin-top:8px"><button class="btn" onclick="viewAlert(${a.id})">عرض</button></div></div></div>`).join('');
}

function viewAlert(id){
  const a = alerts.find(x=>x.id===id);
  if(!a) return alert('غير موجود');
  go('analysis', document.querySelector('.tab[data-screen="analysis"]'));
  document.getElementById('kvSession').innerText = 'جلسة_'+a.id;
  document.getElementById('kvScore').innerText = Math.floor(Math.random()*50+30)+'%';
  document.getElementById('kvReason').innerText = a.text;
}

function performCheck(){
  const user = document.getElementById('userInput').value || 'user01';
  const text = document.getElementById('typingInput').value || '';
  const score = Math.min(100,Math.max(30, Math.floor(text.length*2.5)));
  document.getElementById('kvSession').innerText = user;
  document.getElementById('kvScore').innerText = score+'%';
  document.getElementById('kvReason').innerText = (score<60 ? 'انحراف في نمط الكتابة' : 'مطابق للسلوك المعتاد');
  if(score<60) alerts.unshift({id:Date.now(), text:'سلوك كتابة غير نمطي', level:'عالي', time:new Date().toLocaleTimeString()});
  go('analysis', document.querySelector('.tab[data-screen="analysis"]'));
}

// Chart
function initChart(){
  const ctx = document.getElementById('confChart').getContext('2d');
  window.confChart = new Chart(ctx,{
    type:'line',
    data:{
      labels:['08','09','10','11','12','13','14','15','16','17'],
      datasets:[{label:'Confidence %',data:[80,82,78,85,70,90,88,76,84,80],borderColor:'#4f46e5',backgroundColor:'rgba(79,70,229,0.2)'}]
    },
    options:{responsive:true,plugins:{legend:{display:false}},scales:{y:{min:0,max:100}}}
  });
}

function updateChart(){
  window.confChart.data.datasets[0].data=[82,79,85,88,90,78,80,83,77,85];
  window.confChart.update();
}
</script>
</body>
</html>


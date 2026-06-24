# 
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Planejamento de Produção</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet"/>
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}

:root{
  --bg:#F7F8FA;
  --bg-card:#FFFFFF;
  --bg-surface:#F0F2F5;
  --border:#E2E6EA;
  --border-strong:#C8CDD5;
  --text:#1A1F2E;
  --text-muted:#6B7280;
  --text-dim:#9CA3AF;
  --blue:#185FA5;
  --blue-bg:#E6F1FB;
  --blue-text:#0C447C;
  --green:#3B6D11;
  --green-bg:#EAF3DE;
  --green-text:#27500A;
  --amber:#854F0B;
  --amber-bg:#FAEEDA;
  --amber-text:#633806;
  --red:#A32D2D;
  --red-bg:#FCEBEB;
  --red-text:#791F1F;
  --radius:8px;
  --radius-lg:12px;
  --shadow:0 1px 3px rgba(0,0,0,.08),0 1px 2px rgba(0,0,0,.04);
}

@media(prefers-color-scheme:dark){
  :root{
    --bg:#0F1B2D;
    --bg-card:#1A2B3C;
    --bg-surface:#1E3248;
    --border:#2A3F55;
    --border-strong:#3A5470;
    --text:#E8EDF2;
    --text-muted:#7B90A8;
    --text-dim:#4A6278;
    --blue:#60A5FA;
    --blue-bg:#0C447C;
    --blue-text:#B5D4F4;
    --green:#3DD68C;
    --green-bg:#27500A;
    --green-text:#C0DD97;
    --amber:#F5A623;
    --amber-bg:#633806;
    --amber-text:#FAC775;
    --red:#F05252;
    --red-bg:#791F1F;
    --red-text:#F7C1C1;
  }
}

body{
  font-family:'Inter',sans-serif;
  background:var(--bg);
  color:var(--text);
  min-height:100vh;
  font-size:14px;
}

/* TOPBAR */
.topbar{
  background:var(--bg-card);
  border-bottom:1px solid var(--border);
  padding:12px 24px;
  display:flex;
  align-items:center;
  gap:16px;
  flex-wrap:wrap;
  position:sticky;
  top:0;
  z-index:100;
  box-shadow:var(--shadow);
}

.brand{
  display:flex;
  align-items:center;
  gap:10px;
  margin-right:8px;
}

.brand-icon{
  width:32px;height:32px;
  background:var(--blue);
  border-radius:var(--radius);
  display:flex;align-items:center;justify-content:center;
  flex-shrink:0;
}

.brand-icon svg{display:block}

.brand-title{
  font-size:14px;font-weight:700;
  color:var(--text);
  line-height:1.2;
}
.brand-sub{font-size:11px;color:var(--text-muted);font-weight:400}

.view-tabs{
  display:flex;gap:3px;
  background:var(--bg-surface);
  border:1px solid var(--border);
  border-radius:var(--radius);
  padding:3px;
}
.vtab{
  padding:5px 14px;
  border-radius:6px;
  border:none;background:transparent;
  font-size:12px;font-weight:500;
  cursor:pointer;color:var(--text-muted);
  font-family:inherit;
  transition:all .15s;
}
.vtab.active{
  background:var(--bg-card);
  color:var(--text);
  border:1px solid var(--border);
  box-shadow:var(--shadow);
}

.nav-group{display:flex;align-items:center;gap:6px}
.nav-btn{
  width:30px;height:30px;
  background:var(--bg-card);
  border:1px solid var(--border);
  border-radius:var(--radius);
  cursor:pointer;color:var(--text-muted);
  font-size:14px;
  display:flex;align-items:center;justify-content:center;
  transition:all .15s;
  font-family:inherit;
}
.nav-btn:hover{border-color:var(--border-strong);color:var(--text)}

.period-label{
  font-size:13px;font-weight:600;
  min-width:180px;text-align:center;
  color:var(--text);
}

.btn-today{
  padding:5px 12px;
  background:var(--bg-card);
  border:1px solid var(--border);
  border-radius:var(--radius);
  font-size:12px;font-weight:500;
  cursor:pointer;color:var(--text-muted);
  font-family:inherit;
  transition:all .15s;
}
.btn-today:hover{border-color:var(--border-strong);color:var(--text)}

.btn-export{
  margin-left:auto;
  padding:6px 14px;
  background:var(--blue);
  border:none;
  border-radius:var(--radius);
  font-size:12px;font-weight:600;
  cursor:pointer;color:#fff;
  font-family:inherit;
  display:flex;align-items:center;gap:6px;
  transition:opacity .15s;
}
.btn-export:hover{opacity:.88}

/* LEGENDA */
.legend-bar{
  background:var(--bg-card);
  border-bottom:1px solid var(--border);
  padding:8px 24px;
  display:flex;align-items:center;gap:20px;
  flex-wrap:wrap;
}
.leg-item{display:flex;align-items:center;gap:6px;font-size:11px;color:var(--text-muted)}
.leg-dot{width:10px;height:10px;border-radius:3px;flex-shrink:0}
.status-planejado{background:var(--blue-bg);color:var(--blue-text)}
.status-ok{background:var(--green-bg);color:var(--green-text)}
.status-alerta{background:var(--amber-bg);color:var(--amber-text)}
.status-parado{background:var(--red-bg);color:var(--red-text)}

/* STATS */
.stats-row{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(120px,1fr));
  gap:10px;
  padding:16px 24px 0;
  max-width:1400px;
  margin:0 auto;
}
.stat-card{
  background:var(--bg-card);
  border:1px solid var(--border);
  border-radius:var(--radius-lg);
  padding:12px 16px;
}
.stat-lbl{font-size:10px;font-weight:600;color:var(--text-muted);letter-spacing:.05em;text-transform:uppercase;margin-bottom:5px}
.stat-val{font-size:22px;font-weight:800;letter-spacing:-.03em}
.stat-val.blue{color:var(--blue)}
.stat-val.green{color:var(--green)}
.stat-val.amber{color:var(--amber)}
.stat-val.red{color:var(--red)}

/* MAIN */
.main{
  padding:16px 24px 40px;
  max-width:1400px;
  margin:0 auto;
}

/* GRADE SEMANAL */
.grid-wrap{
  overflow-x:auto;
  background:var(--bg-card);
  border:1px solid var(--border);
  border-radius:var(--radius-lg);
  box-shadow:var(--shadow);
}
table{width:100%;border-collapse:collapse;min-width:720px}
thead tr{background:var(--bg-surface)}

th{
  padding:10px 10px;
  text-align:left;
  font-size:11px;font-weight:600;
  color:var(--text-muted);
  letter-spacing:.05em;text-transform:uppercase;
  border-bottom:1px solid var(--border);
  white-space:nowrap;
}
th.day-th{text-align:center;min-width:110px}

td{
  padding:6px 8px;
  border-bottom:1px solid var(--border);
  vertical-align:top;
}
tr:last-child td{border-bottom:none}

.line-cell{
  font-size:12px;font-weight:600;
  white-space:nowrap;
  padding:10px 14px;
  background:var(--bg-surface);
  border-right:1px solid var(--border);
  width:90px;
  position:sticky;left:0;
  z-index:2;
}
.line-num{font-size:10px;color:var(--text-dim);font-weight:400;margin-top:1px}

.day-cell{
  text-align:center;
  cursor:pointer;
  position:relative;
  min-width:110px;
  padding:5px 6px;
}
.cell-inner{
  border:1.5px dashed var(--border);
  border-radius:var(--radius);
  padding:7px 8px;
  min-height:58px;
  transition:all .15s;
  display:flex;flex-direction:column;align-items:center;justify-content:center;
}
.day-cell:hover .cell-inner{border-color:var(--blue);background:var(--blue-bg)}
.cell-inner.has-order{border-style:solid;border-color:transparent}
.cell-prod{font-size:11px;font-weight:600;line-height:1.3;margin-bottom:2px}
.cell-qty{font-size:10px;opacity:.8}
.cell-eff{font-size:10px;margin-top:3px;opacity:.75}
.cell-plus{font-size:20px;color:var(--text-dim);line-height:1;transition:color .15s}
.day-cell:hover .cell-plus{color:var(--blue)}

.today-th{
  position:relative;
  color:var(--blue) !important;
}
.today-th::after{
  content:'';
  position:absolute;
  bottom:0;left:0;right:0;
  height:2px;background:var(--blue);
  border-radius:2px;
}
.today-td .cell-inner{border-color:var(--border-strong)}

/* GRID MENSAL */
.month-wrap{
  background:var(--bg-card);
  border:1px solid var(--border);
  border-radius:var(--radius-lg);
  box-shadow:var(--shadow);
  overflow:hidden;
}
.month-header-row{
  display:grid;grid-template-columns:repeat(7,1fr);
  border-bottom:1px solid var(--border);
  background:var(--bg-surface);
}
.month-hdr{
  font-size:11px;font-weight:600;color:var(--text-muted);
  letter-spacing:.05em;text-transform:uppercase;
  text-align:center;padding:10px 6px;
}
.month-grid{
  display:grid;grid-template-columns:repeat(7,1fr);
}
.month-day{
  min-height:80px;
  border-right:1px solid var(--border);
  border-bottom:1px solid var(--border);
  padding:6px;
  cursor:pointer;
  transition:background .12s;
  position:relative;
}
.month-day:nth-child(7n){border-right:none}
.month-day:hover{background:var(--bg-surface)}
.month-day.other-month{opacity:.35;pointer-events:none}
.month-day.sunday{background:var(--bg-surface);opacity:.5;pointer-events:none}
.month-day.today .mday-num{
  background:var(--blue);color:#fff;
  width:22px;height:22px;border-radius:50%;
  display:flex;align-items:center;justify-content:center;
}
.mday-num{font-size:12px;font-weight:600;margin-bottom:4px;display:inline-block}
.mday-pip{
  width:100%;height:4px;
  border-radius:2px;
  margin-bottom:2px;
}
.mday-count{font-size:9px;color:var(--text-dim);margin-top:2px}

/* MODAL */
.modal-overlay{
  position:fixed;inset:0;
  background:rgba(0,0,0,.5);
  backdrop-filter:blur(3px);
  z-index:500;
  display:flex;align-items:center;justify-content:center;
  padding:20px;
  opacity:0;pointer-events:none;
  transition:opacity .2s;
}
.modal-overlay.open{opacity:1;pointer-events:all}

.modal{
  background:var(--bg-card);
  border:1px solid var(--border);
  border-radius:var(--radius-lg);
  width:100%;max-width:420px;
  box-shadow:0 20px 60px rgba(0,0,0,.2);
  transform:translateY(12px);
  transition:transform .2s;
  overflow:hidden;
}
.modal-overlay.open .modal{transform:translateY(0)}

.modal-head{
  padding:16px 20px;
  border-bottom:1px solid var(--border);
  display:flex;align-items:center;justify-content:space-between;
  background:var(--bg-surface);
}
.modal-head h3{font-size:14px;font-weight:700}
.modal-close{
  width:28px;height:28px;
  background:transparent;
  border:1px solid var(--border);
  border-radius:var(--radius);
  cursor:pointer;color:var(--text-muted);
  font-size:16px;
  display:flex;align-items:center;justify-content:center;
  font-family:inherit;
  transition:all .15s;
}
.modal-close:hover{border-color:var(--border-strong);color:var(--text)}

.modal-body{padding:20px}

.form-row{margin-bottom:14px}
.form-label{
  display:block;
  font-size:11px;font-weight:600;
  color:var(--text-muted);
  letter-spacing:.04em;text-transform:uppercase;
  margin-bottom:5px;
}
.form-input,.form-select,.form-textarea{
  width:100%;
  background:var(--bg-surface);
  border:1px solid var(--border);
  border-radius:var(--radius);
  padding:8px 10px;
  font-size:13px;
  color:var(--text);
  font-family:inherit;
  transition:border-color .15s;
}
.form-input:focus,.form-select:focus,.form-textarea:focus{
  outline:none;
  border-color:var(--blue);
}
.form-textarea{height:60px;resize:vertical}

.form-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px}

.status-chips{display:flex;gap:6px;flex-wrap:wrap;margin-top:4px}
.chip{
  padding:5px 12px;
  border-radius:20px;
  font-size:11px;font-weight:600;
  cursor:pointer;
  border:2px solid transparent;
  transition:all .15s;
  font-family:inherit;
}
.chip:hover{opacity:.8}
.chip.selected{border-color:currentColor}

.modal-foot{
  padding:12px 20px;
  border-top:1px solid var(--border);
  display:flex;align-items:center;gap:8px;
  justify-content:flex-end;
}
.btn-del{
  margin-right:auto;
  background:transparent;
  border:1px solid var(--border);
  border-radius:var(--radius);
  padding:7px 14px;
  font-size:12px;font-weight:600;
  cursor:pointer;color:var(--red);
  font-family:inherit;
  transition:all .15s;
}
.btn-del:hover{border-color:var(--red)}
.btn-cancel{
  background:transparent;
  border:1px solid var(--border);
  border-radius:var(--radius);
  padding:7px 14px;
  font-size:12px;font-weight:500;
  cursor:pointer;color:var(--text-muted);
  font-family:inherit;
  transition:all .15s;
}
.btn-cancel:hover{border-color:var(--border-strong);color:var(--text)}
.btn-save{
  background:var(--blue);
  border:none;
  border-radius:var(--radius);
  padding:7px 18px;
  font-size:12px;font-weight:700;
  cursor:pointer;color:#fff;
  font-family:inherit;
  transition:opacity .15s;
}
.btn-save:hover{opacity:.88}

/* MODAL DIA */
.day-detail-table{width:100%;border-collapse:collapse;margin-top:10px}
.day-detail-table th{font-size:10px;font-weight:600;color:var(--text-muted);text-transform:uppercase;letter-spacing:.05em;padding:7px 10px;background:var(--bg-surface);text-align:left;border-bottom:1px solid var(--border)}
.day-detail-table td{font-size:12px;padding:8px 10px;border-bottom:1px solid var(--border)}
.day-detail-table tr:last-child td{border-bottom:none}
.btn-edit-small{
  padding:3px 10px;font-size:11px;font-weight:500;
  background:transparent;border:1px solid var(--border);
  border-radius:6px;cursor:pointer;color:var(--text-muted);
  font-family:inherit;transition:all .15s;
}
.btn-edit-small:hover{border-color:var(--blue);color:var(--blue)}
.badge{padding:3px 8px;border-radius:20px;font-size:10px;font-weight:600}

@media(max-width:700px){
  .topbar{padding:10px 14px;gap:8px}
  .main{padding:12px 14px 40px}
  .stats-row{padding:12px 14px 0;grid-template-columns:repeat(2,1fr)}
  .btn-export span{display:none}
  .period-label{min-width:120px;font-size:12px}
}
</style>
</head>
<body>

<!-- TOPBAR -->
<div class="topbar">
  <div class="brand">
    <div class="brand-icon">
      <svg width="18" height="18" viewBox="0 0 18 18" fill="none">
        <rect x="2" y="2" width="6" height="6" rx="1.5" fill="white"/>
        <rect x="10" y="2" width="6" height="6" rx="1.5" fill="white" opacity=".7"/>
        <rect x="2" y="10" width="6" height="6" rx="1.5" fill="white" opacity=".7"/>
        <rect x="10" y="10" width="6" height="6" rx="1.5" fill="white" opacity=".4"/>
      </svg>
    </div>
    <div>
      <div class="brand-title">Planejamento de Produção</div>
      <div class="brand-sub">8 linhas · Seg – Sáb</div>
    </div>
  </div>

  <div class="view-tabs">
    <button class="vtab active" onclick="setView('semana',this)">Semana</button>
    <button class="vtab" onclick="setView('mes',this)">Mês</button>
  </div>

  <div class="nav-group">
    <button class="nav-btn" onclick="navigate(-1)" title="Anterior">&#8592;</button>
    <span class="period-label" id="periodLabel"></span>
    <button class="nav-btn" onclick="navigate(1)" title="Próximo">&#8594;</button>
    <button class="btn-today" onclick="goToday()">Hoje</button>
  </div>

  <button class="btn-export" onclick="exportCSV()">
    <svg width="13" height="13" viewBox="0 0 13 13" fill="none"><path d="M6.5 1v7M3.5 5.5l3 3 3-3M2 10h9" stroke="white" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/></svg>
    <span>Exportar CSV</span>
  </button>
</div>

<!-- LEGENDA -->
<div class="legend-bar">
  <div class="leg-item"><div class="leg-dot status-planejado"></div> Planejado</div>
  <div class="leg-item"><div class="leg-dot status-ok"></div> Concluído</div>
  <div class="leg-item"><div class="leg-dot status-alerta"></div> Alerta</div>
  <div class="leg-item"><div class="leg-dot status-parado"></div> Parado</div>
  <span style="margin-left:auto;font-size:11px;color:var(--text-dim)">Clique em qualquer célula para adicionar ou editar uma ordem</span>
</div>

<!-- STATS -->
<div class="stats-row" id="statsRow"></div>

<!-- VIEW AREA -->
<div class="main" id="viewArea"></div>

<!-- MODAL ORDEM -->
<div class="modal-overlay" id="modalOrdem">
  <div class="modal">
    <div class="modal-head">
      <h3 id="modalTitle">Nova ordem</h3>
      <button class="modal-close" onclick="closeModal('modalOrdem')">✕</button>
    </div>
    <div class="modal-body">
      <div class="form-row">
        <label class="form-label">Produto / Ordem</label>
        <input class="form-input" id="f_prod" placeholder="Ex: Componente A-12"/>
      </div>
      <div class="form-grid">
        <div class="form-row">
          <label class="form-label">Quantidade (un)</label>
          <input class="form-input" id="f_qty" type="number" min="0" placeholder="0"/>
        </div>
        <div class="form-row">
          <label class="form-label">Meta do turno (un)</label>
          <input class="form-input" id="f_meta" type="number" min="0" placeholder="0"/>
        </div>
      </div>
      <div class="form-grid">
        <div class="form-row">
          <label class="form-label">Eficiência (%)</label>
          <input class="form-input" id="f_eff" type="number" min="0" max="100" placeholder="0"/>
        </div>
        <div class="form-row">
          <label class="form-label">Responsável</label>
          <input class="form-input" id="f_resp" placeholder="Nome"/>
        </div>
      </div>
      <div class="form-row">
        <label class="form-label">Status</label>
        <div class="status-chips">
          <button class="chip status-planejado selected" data-status="planejado" onclick="selectStatus(this)">Planejado</button>
          <button class="chip status-ok" data-status="ok" onclick="selectStatus(this)">Concluído</button>
          <button class="chip status-alerta" data-status="alerta" onclick="selectStatus(this)">Alerta</button>
          <button class="chip status-parado" data-status="parado" onclick="selectStatus(this)">Parado</button>
        </div>
      </div>
      <div class="form-row">
        <label class="form-label">Observação</label>
        <textarea class="form-textarea" id="f_obs" placeholder="Anotações opcionais..."></textarea>
      </div>
    </div>
    <div class="modal-foot">
      <button class="btn-del" id="btnDel" style="display:none" onclick="deleteOrder()">Excluir ordem</button>
      <button class="btn-cancel" onclick="closeModal('modalOrdem')">Cancelar</button>
      <button class="btn-save" onclick="saveOrder()">Salvar ordem</button>
    </div>
  </div>
</div>

<!-- MODAL DIA (visão mensal) -->
<div class="modal-overlay" id="modalDia">
  <div class="modal" style="max-width:560px">
    <div class="modal-head">
      <h3 id="modalDiaTitle">Resumo do dia</h3>
      <button class="modal-close" onclick="closeModal('modalDia')">✕</button>
    </div>
    <div class="modal-body" id="modalDiaBody" style="padding:0;overflow-y:auto;max-height:60vh"></div>
    <div class="modal-foot">
      <button class="btn-cancel" onclick="closeModal('modalDia')">Fechar</button>
    </div>
  </div>
</div>

<script>
const LINES=['Linha 1','Linha 2','Linha 3','Linha 4','Linha 5','Linha 6','Linha 7','Linha 8'];
const DAYS_PT=['Dom','Seg','Ter','Qua','Qui','Sex','Sáb'];
const DAYS_FULL=['Domingo','Segunda','Terça','Quarta','Quinta','Sexta','Sábado'];
const MONTHS_PT=['Janeiro','Fevereiro','Março','Abril','Maio','Junho','Julho','Agosto','Setembro','Outubro','Novembro','Dezembro'];
const MONTHS_SHORT=['jan','fev','mar','abr','mai','jun','jul','ago','set','out','nov','dez'];
const STATUS_LABEL={planejado:'Planejado',ok:'Concluído',alerta:'Alerta',parado:'Parado'};

let view='semana';
let baseDate=new Date(); baseDate.setHours(0,0,0,0);
let orders={};
let currentLine='',currentDate='';

function fmtDate(d){return d.toISOString().slice(0,10)}
function parseDate(s){const[y,m,d]=s.split('-');return new Date(+y,+m-1,+d)}
function addDays(d,n){const r=new Date(d);r.setDate(r.getDate()+n);return r}
function isToday(d){const t=new Date();return fmtDate(d)===fmtDate(t)}
function orderKey(line,date){return line+'||'+date}

function getWeekStart(d){
  const dd=new Date(d);
  const day=dd.getDay();
  const diff=day===0?-6:1-day;
  dd.setDate(dd.getDate()+diff);
  return dd;
}

function setView(v,el){
  view=v;
  document.querySelectorAll('.vtab').forEach(b=>b.classList.remove('active'));
  el.classList.add('active');
  render();
}

function navigate(dir){
  if(view==='semana') baseDate=addDays(baseDate,dir*7);
  else baseDate=new Date(baseDate.getFullYear(),baseDate.getMonth()+dir,1);
  render();
}

function goToday(){baseDate=new Date();baseDate.setHours(0,0,0,0);render()}

/* ── STATS ── */
function computeStats(days){
  let total=0,planejado=0,ok=0,alerta=0,parado=0;
  days.forEach(d=>{
    LINES.forEach(l=>{
      const o=orders[orderKey(l,fmtDate(d))];
      if(!o)return;
      total++;
      if(o.status==='planejado')planejado++;
      if(o.status==='ok')ok++;
      if(o.status==='alerta')alerta++;
      if(o.status==='parado')parado++;
    });
  });
  return{total,planejado,ok,alerta,parado};
}

function renderStats(days){
  const s=computeStats(days);
  document.getElementById('statsRow').innerHTML=`
    <div class="stat-card"><div class="stat-lbl">Total de ordens</div><div class="stat-val">${s.total}</div></div>
    <div class="stat-card"><div class="stat-lbl">Planejadas</div><div class="stat-val blue">${s.planejado}</div></div>
    <div class="stat-card"><div class="stat-lbl">Concluídas</div><div class="stat-val green">${s.ok}</div></div>
    <div class="stat-card"><div class="stat-lbl">Alertas</div><div class="stat-val amber">${s.alerta}</div></div>
    <div class="stat-card"><div class="stat-lbl">Paradas</div><div class="stat-val red">${s.parado}</div></div>
  `;
}

/* ── SEMANA ── */
function renderWeek(){
  const ws=getWeekStart(baseDate);
  const days=[];
  for(let i=0;i<6;i++) days.push(addDays(ws,i));
  document.getElementById('periodLabel').textContent=
    `${days[0].getDate()} ${MONTHS_SHORT[days[0].getMonth()]} – ${days[5].getDate()} ${MONTHS_SHORT[days[5].getMonth()]} ${days[5].getFullYear()}`;
  renderStats(days);

  let html=`<div class="grid-wrap"><table><thead><tr>
    <th style="position:sticky;left:0;z-index:3;background:var(--bg-surface)">Linha</th>`;
  days.forEach((d,i)=>{
    const tod=isToday(d);
    html+=`<th class="day-th${tod?' today-th':''}">
      ${DAYS_PT[i+1]}&nbsp;
      <span style="font-size:14px;font-weight:700;color:var(--text)">${d.getDate()}</span>
      <span style="font-size:10px;color:var(--text-dim)"> ${MONTHS_SHORT[d.getMonth()]}</span>
    </th>`;
  });
  html+=`</tr></thead><tbody>`;

  LINES.forEach((line,li)=>{
    html+=`<tr><td class="line-cell">${line}<div class="line-num">L${String(li+1).padStart(2,'0')}</div></td>`;
    days.forEach((d,di)=>{
      const ds=fmtDate(d);
      const k=orderKey(line,ds);
      const o=orders[k];
      const tod=isToday(d);
      html+=`<td class="day-cell${tod?' today-td':''}" onclick="openModal('${line}','${ds}')">`;
      if(o){
        html+=`<div class="cell-inner has-order status-${o.status}">
          <div class="cell-prod">${esc(o.produto)}</div>
          <div class="cell-qty">${o.quantidade?o.quantidade+' un':''}</div>
          ${o.eficiencia?`<div class="cell-eff">${o.eficiencia}% efic.</div>`:''}
        </div>`;
      } else {
        html+=`<div class="cell-inner"><span class="cell-plus">+</span></div>`;
      }
      html+=`</td>`;
    });
    html+=`</tr>`;
  });
  html+=`</tbody></table></div>`;
  document.getElementById('viewArea').innerHTML=html;
}

/* ── MÊS ── */
function renderMonth(){
  const year=baseDate.getFullYear(),month=baseDate.getMonth();
  document.getElementById('periodLabel').textContent=`${MONTHS_PT[month]} ${year}`;
  const firstDay=new Date(year,month,1);
  const lastDay=new Date(year,month+1,0);
  const start=getWeekStart(firstDay);

  const allDays=[];
  let cur=new Date(start);
  while(cur<=addDays(lastDay,6)){allDays.push(new Date(cur));cur=addDays(cur,1)}

  const monthDays=[];
  cur=new Date(firstDay);
  while(cur<=lastDay){monthDays.push(new Date(cur));cur=addDays(cur,1)}
  renderStats(monthDays);

  let html=`<div class="month-wrap">
    <div class="month-header-row">`;
  ['Seg','Ter','Qua','Qui','Sex','Sáb','Dom'].forEach(d=>{
    html+=`<div class="month-hdr">${d}</div>`;
  });
  html+=`</div><div class="month-grid">`;

  allDays.forEach(d=>{
    const inMonth=d.getMonth()===month;
    const isSun=d.getDay()===0;
    const tod=isToday(d);
    const ds=fmtDate(d);
    const dayOrders=LINES.map(l=>orders[orderKey(l,ds)]).filter(Boolean);
    const counts={planejado:0,ok:0,alerta:0,parado:0};
    dayOrders.forEach(o=>{if(counts[o.status]!==undefined)counts[o.status]++});

    html+=`<div class="month-day${!inMonth?' other-month':''}${isSun?' sunday':''}${tod?' today':''}"
      ${inMonth&&!isSun?`onclick="openDayDetail('${ds}')"`:''}>`;
    html+=`<div class="mday-num">${d.getDate()}</div>`;
    if(counts.planejado) html+=`<div class="mday-pip status-planejado" title="${counts.planejado} planejado(s)"></div>`;
    if(counts.ok)        html+=`<div class="mday-pip status-ok" title="${counts.ok} concluído(s)"></div>`;
    if(counts.alerta)    html+=`<div class="mday-pip status-alerta" title="${counts.alerta} alerta(s)"></div>`;
    if(counts.parado)    html+=`<div class="mday-pip status-parado" title="${counts.parado} parado(s)"></div>`;
    if(dayOrders.length) html+=`<div class="mday-count">${dayOrders.length} ordem${dayOrders.length>1?'s':''}</div>`;
    html+=`</div>`;
  });
  html+=`</div></div>`;
  document.getElementById('viewArea').innerHTML=html;
}

function render(){
  if(view==='semana') renderWeek();
  else renderMonth();
}

/* ── MODAL ORDEM ── */
function openModal(line,ds){
  currentLine=line; currentDate=ds;
  const k=orderKey(line,ds);
  const o=orders[k]||{};
  const d=parseDate(ds);
  document.getElementById('modalTitle').textContent=
    `${line} · ${DAYS_FULL[d.getDay()]}, ${d.getDate()} de ${MONTHS_PT[d.getMonth()]}`;
  document.getElementById('f_prod').value=o.produto||'';
  document.getElementById('f_qty').value=o.quantidade||'';
  document.getElementById('f_meta').value=o.meta||'';
  document.getElementById('f_eff').value=o.eficiencia||'';
  document.getElementById('f_resp').value=o.responsavel||'';
  document.getElementById('f_obs').value=o.obs||'';
  document.querySelectorAll('.chip').forEach(c=>{
    c.classList.toggle('selected',c.dataset.status===(o.status||'planejado'));
  });
  document.getElementById('btnDel').style.display=o.produto?'inline-flex':'none';
  document.getElementById('modalOrdem').classList.add('open');
}

function selectStatus(el){
  document.querySelectorAll('.chip').forEach(c=>c.classList.remove('selected'));
  el.classList.add('selected');
}

function saveOrder(){
  const prod=document.getElementById('f_prod').value.trim();
  if(!prod){alert('Informe o produto ou ordem.');return;}
  const chip=document.querySelector('.chip.selected');
  const k=orderKey(currentLine,currentDate);
  orders[k]={
    produto:prod,
    quantidade:+document.getElementById('f_qty').value||0,
    meta:+document.getElementById('f_meta').value||0,
    eficiencia:+document.getElementById('f_eff').value||0,
    responsavel:document.getElementById('f_resp').value.trim(),
    status:chip?chip.dataset.status:'planejado',
    obs:document.getElementById('f_obs').value.trim()
  };
  closeModal('modalOrdem');
  render();
}

function deleteOrder(){
  if(!confirm('Excluir esta ordem?'))return;
  delete orders[orderKey(currentLine,currentDate)];
  closeModal('modalOrdem');
  render();
}

function closeModal(id){document.getElementById(id).classList.remove('open')}

/* ── MODAL DIA ── */
function openDayDetail(ds){
  const d=parseDate(ds);
  document.getElementById('modalDiaTitle').textContent=
    `${DAYS_FULL[d.getDay()]}, ${d.getDate()} de ${MONTHS_PT[d.getMonth()]}`;

  let rows='';
  LINES.forEach(l=>{
    const o=orders[orderKey(l,ds)];
    rows+=`<tr>
      <td style="font-weight:600">${l}</td>
      <td>${o?esc(o.produto):'—'}</td>
      <td style="text-align:right">${o&&o.quantidade?o.quantidade+' un':''}</td>
      <td>${o?`<span class="badge status-${o.status}">${STATUS_LABEL[o.status]}</span>`:''}</td>
      <td><button class="btn-edit-small" onclick="closeModal('modalDia');openModal('${l}','${ds}')">Editar</button></td>
    </tr>`;
  });

  document.getElementById('modalDiaBody').innerHTML=`
    <table class="day-detail-table">
      <thead><tr>
        <th>Linha</th><th>Produto</th><th style="text-align:right">Qtd</th><th>Status</th><th></th>
      </tr></thead>
      <tbody>${rows}</tbody>
    </table>`;
  document.getElementById('modalDia').classList.add('open');
}

/* ── FECHAR AO CLICAR FORA ── */
document.getElementById('modalOrdem').addEventListener('click',function(e){
  if(e.target===this)closeModal('modalOrdem');
});
document.getElementById('modalDia').addEventListener('click',function(e){
  if(e.target===this)closeModal('modalDia');
});

/* ── EXPORTAR CSV ── */
function exportCSV(){
  const rows=[['Linha','Data','Dia','Produto','Quantidade','Meta','Eficiência (%)','Status','Responsável','Observação']];
  Object.entries(orders).forEach(([k,o])=>{
    const[line,ds]=k.split('||');
    const d=parseDate(ds);
    rows.push([line,ds,DAYS_FULL[d.getDay()],o.produto,o.quantidade,o.meta,o.eficiencia,STATUS_LABEL[o.status],o.responsavel,o.obs]);
  });
  const csv=rows.map(r=>r.map(v=>`"${String(v??'').replace(/"/g,'""')}"`).join(',')).join('\n');
  const blob=new Blob(['\uFEFF'+csv],{type:'text/csv;charset=utf-8'});
  const url=URL.createObjectURL(blob);
  const a=document.createElement('a');
  a.href=url;a.download='planejamento-producao.csv';
  a.click();URL.revokeObjectURL(url);
}

/* ── DADOS DE EXEMPLO ── */
function seedData(){
  const ws=getWeekStart(new Date());
  const prods=['Comp. A-12','Parafuso M8','Suporte Lat.','Eixo C3','Embalagem K','Peça T7','Módulo X9','Válvula V2'];
  const resps=['Ana Lima','Carlos M.','Bruna S.','Pedro R.','Fernanda C.','Lucas A.','Mariana P.','Thiago N.'];
  const statuses=['planejado','ok','ok','ok','alerta','parado'];
  LINES.forEach((l,li)=>{
    for(let i=0;i<6;i++){
      if(Math.random()<0.62){
        const d=addDays(ws,i);
        const qty=Math.round(200+Math.random()*700);
        const meta=600;
        orders[orderKey(l,fmtDate(d))]={
          produto:prods[li],
          quantidade:qty,
          meta,
          eficiencia:Math.round(55+Math.random()*45),
          responsavel:resps[li],
          status:statuses[Math.floor(Math.random()*statuses.length)],
          obs:''
        };
      }
    }
  });
}

function esc(s){if(!s)return'';return s.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;')}

seedData();
render();
</script>
</body>
</html>

<!doctype html>
<html lang="es">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Herencias - Viewer & Filtros</title>

<style>
  /* === Base Dark Style tipo rgb(32,38,46) === */
  body{
    font-family: system-ui, -apple-system, Segoe UI, Roboto, Arial;
    background: rgb(32,38,46);
    color: #f0f0f0;
    margin: 18px;
  }

  h1{margin:0 0 12px;font-size:22px;font-weight:600}

  .box{
    background:#1f252d;
    border:1px solid #3a4552;
    padding:16px;
    border-radius:8px;
    margin-bottom:14px;
  }

  label{
    display:block;
    font-size:14px;
    margin:8px 0 4px;
    color:#c9d3df;
  }

  input[type="text"], input[type="number"], select, textarea{
    width:100%;
    padding:8px 10px;
    border-radius:6px;
    border:1px solid #4a5563;
    background:#0f1318;
    color:#e8eef5;
    box-sizing:border-box;
    font-size:14px;
  }

  table{
    width:100%;
    border-collapse:collapse;
    margin-top:10px;
    font-size:13px;
  }
  th,td{
    padding:6px 8px;
    border-bottom:1px solid #2a323c;
    text-align:left;
  }
  th{
    background:#13181d;
    color:#d7e1ec;
    position:sticky;
    top:0;
    cursor:pointer; /* ← Añadido solo esto */
  }

  .small{font-size:12px;color:#aebbc9}
  .controls{
    display:grid;
    gap:10px;
    grid-template-columns:repeat(auto-fit,minmax(200px,1fr));
  }
</style>
</head>

<body>

<h1>Herencias (Viewer & Filtros)</h1>

<!-- ================== IMPORTADOR ================== -->
<div class="box">
  <label>Subir CSV
    <input type="file" id="csvFile" accept=".csv,text/csv" />
  </label>

  <label>Pegar CSV
    <textarea id="pasteArea" rows="6"></textarea>
  </label>

  <button id="importBtn">Importar CSV</button>
  <button id="clearBtn">Limpiar tabla</button>
  <button id="downloadBtn">Exportar filtrados</button>
</div>

<!-- ================== FILTROS ================== -->
<div class="box">
  <h2 style="margin:0 0 12px;font-size:18px;font-weight:600">Filtros rápidos</h2>

  <div class="controls">
    <div><label>Speed ≥</label><input type="number" id="fSpeed" /></div>
    <div><label>Stamina ≥</label><input type="number" id="fStamina" /></div>
    <div><label>Power ≥</label><input type="number" id="fPower" /></div>
    <div><label>Guts ≥</label><input type="number" id="fGuts" /></div>
    <div><label>Wit ≥</label><input type="number" id="fWit" /></div>

    <div><label>Turf ≥</label><input type="number" id="fTurf" /></div>
    <div><label>Dirt ≥</label><input type="number" id="fDirt" /></div>

    <div><label>Sprint ≥</label><input type="number" id="fSprint" /></div>
    <div><label>Mile ≥</label><input type="number" id="fMile" /></div>
    <div><label>Medium ≥</label><input type="number" id="fMedium" /></div>
    <div><label>Long ≥</label><input type="number" id="fLong" /></div>

    <div><label>End ≥</label><input type="number" id="fEnd" /></div>
    <div><label>Late ≥</label><input type="number" id="fLate" /></div>
    <div><label>Pace ≥</label><input type="number" id="fPace" /></div>
    <div><label>Front ≥</label><input type="number" id="fFront" /></div>
  </div>

  <button id="applyFilters">Aplicar filtros</button>
  <button id="resetFilters">Reset</button>
</div>

<!-- ================== TABLA ================== -->
<div class="box" id="tableContainer" style="display:none">
  <h2>Resultados <span id="count" class="small"></span></h2>
  <div style="overflow:auto; max-height:55vh;">
    <table id="dataTable"><thead></thead><tbody></tbody></table>
  </div>
</div>

<script>
/* === CSV parser y utilidades (igualito) === */
function parseCSV(text, delimiter = ',') {
  const rows = [];
  let cur = '';
  let row = [];
  let inQuotes = false;
  let i = 0;
  while (i < text.length) {
    const ch = text[i];
    if (ch === '"') {
      if (inQuotes && text[i+1] === '"') { cur += '"'; i += 2; continue; }
      inQuotes = !inQuotes; i++; continue;
    }
    if (!inQuotes && (ch === delimiter || ch === '\t')) {
      row.push(cur); cur=''; i++; continue;
    }
    if (!inQuotes && (ch === '\n' || ch === '\r')) {
      if (ch === '\r' && text[i+1] === '\n') i++;
      row.push(cur); rows.push(row);
      row=[]; cur=''; i++; continue;
    }
    cur+=ch; i++;
  }
  if (cur!=='' || row.length){ row.push(cur); rows.push(row); }
  return rows;
}

function arrayToObjects(rows) {
  const headers = rows[0].map(h=>h.trim());
  const data=[];
  for (let r=1;r<rows.length;r++){
    const row=rows[r];
    if (row.length===1 && row[0]==='') continue;
    const o={}; headers.forEach((h,i)=>o[h]=row[i]?.trim()??'');
    data.push(o);
  }
  return { headers, data };
}

function isNumericColumn(values){
  for (let v of values){
    if (v===''||v===null) continue;
    if(!/^-?\d+(\.\d+)?$/.test(v)) return false;
  }
  return true;
}

function numericOrEmpty(v){
  if(v===''||v==null) return '';
  if(/^-?\d+(\.\d+)?$/.test(v)) return Number(v);
  return v;
}

let GRID={headers:[],data:[]};
let FILTERED=[];

/* === Import === */
csvFile.onchange = ev=>{
  const f=ev.target.files[0];
  if(!f) return;
  const reader=new FileReader();
  reader.onload=()=>loadCSV(reader.result);
  reader.readAsText(f);
};
importBtn.onclick=()=>{ if(pasteArea.value.trim()) loadCSV(pasteArea.value.trim()); };
clearBtn.onclick=()=>{ GRID.data=[]; FILTERED=[]; renderTable(); };

function loadCSV(txt){
  const delim = (txt.includes('\t') && !txt.includes(',')) ? '\t' : ',';
  const rows = parseCSV(txt, delim);
  const parsed = arrayToObjects(rows);
  GRID = parsed;
  GRID.headers.forEach(h=>{
    const vals = GRID.data.map(r=>r[h]);
    if(isNumericColumn(vals)){
      GRID.data.forEach(r=>r[h]=numericOrEmpty(r[h]));
    }
  });
  FILTERED = GRID.data.slice();
  renderTable();
}

/* === SORTING (lo único añadido) === */
let sortState = {}; // guarda asc/desc por columna

function sortByColumn(colName) {
  const direction = sortState[colName] === "asc" ? "desc" : "asc";
  sortState[colName] = direction;

  FILTERED.sort((a, b) => {
    const x = a[colName];
    const y = b[colName];

    const nx = Number(x);
    const ny = Number(y);

    if (!isNaN(nx) && !isNaN(ny)) {
      return direction === "asc" ? nx - ny : ny - nx;
    }
    return direction === "asc" 
      ? String(x).localeCompare(String(y))
      : String(y).localeCompare(String(x));
  });

  renderTable();
}

/* === Tabla === */
function renderTable(rows = FILTERED){
  const cont=document.getElementById('tableContainer');
  const thead=document.querySelector('#dataTable thead');
  const tbody=document.querySelector('#dataTable tbody');
  thead.innerHTML=''; tbody.innerHTML='';

  if(!GRID.headers.length){ cont.style.display='none'; return; }
  cont.style.display='block';

  const tr=document.createElement('tr');
  GRID.headers.forEach(h=>{
  const th=document.createElement('th');
  th.style.position = "relative";

  const label = document.createElement('span');
  label.textContent = h;
  label.style.marginRight = "18px"; // deja espacio al botón

  const btn = document.createElement('button');
  btn.textContent = "↕";                      /* BOTÓN DE ORDEN */
  btn.style.position = "absolute";
  btn.style.right = "4px";
  btn.style.top = "50%";
  btn.style.transform = "translateY(-50%)";
  btn.style.background = "#0f1318";
  btn.style.border = "1px solid #3a4552";
  btn.style.borderRadius = "4px";
  btn.style.color = "#d7e1ec";
  btn.style.padding = "1px 4px";
  btn.style.cursor = "pointer";
  btn.style.fontSize = "11px";

  btn.onclick = (ev) => {
    ev.stopPropagation(); // evita que haga doble click
    sortByColumn(h);
  };

  th.onclick = () => sortByColumn(h); // click completo en la cabecera
  th.appendChild(label);
  th.appendChild(btn);

  tr.appendChild(th);
});

  thead.appendChild(tr);

  rows.forEach(r=>{
    const tr=document.createElement('tr');
    GRID.headers.forEach(h=>{
      const td=document.createElement('td'); td.textContent=r[h]??''; tr.appendChild(td);
    });
    tbody.appendChild(tr);
  });

  document.getElementById('count').textContent = `(${rows.length} / ${GRID.data.length})`;
}

/* === FILTROS === */
function applyAllFilters(){
  let out = GRID.data.slice();

  const min = (id) => Number(document.getElementById(id).value||0);

  const F = {
    Speed: min("fSpeed"),
    Stamina: min("fStamina"),
    Power: min("fPower"),
    Guts: min("fGuts"),
    Wit: min("fWit"),
    Turf: min("fTurf"),
    Dirt: min("fDirt"),
    Sprint: min("fSprint"),
    Mile: min("fMile"),
    Medium: min("fMedium"),
    Long: min("fLong"),
    End: min("fEnd"),
    Late: min("fLate"),
    Pace: min("fPace"),
    Front: min("fFront"),
  };

  for (let col in F){
    if(F[col] > 0){
      out = out.filter(r => Number(r[col]||0) >= F[col]);
    }
  }

  FILTERED = out;
  renderTable();
}

applyFilters.onclick = applyAllFilters;

resetFilters.onclick = ()=>{
  [
    "fSpeed","fStamina","fPower","fGuts","fWit",
    "fTurf","fDirt","fSprint","fMile","fMedium",
    "fLong","fEnd","fLate","fPace","fFront"
  ].forEach(id=>document.getElementById(id).value='');
  FILTERED = GRID.data.slice();
  renderTable();
};

/* === Export === */
downloadBtn.onclick=()=>{
  if(!FILTERED.length) return alert("Nada para exportar.");
  const h=GRID.headers;
  const lines=[h.join(",")];
  FILTERED.forEach(r=>{
    lines.push(
      h.map(col=>{
        const v=r[col]??"";
        return String(v).includes(",") ? `"${String(v).replace(/"/g,'""')}"` : v;
      }).join(",")
    );
  });

  const blob=new Blob([lines.join("\n")],{type:"text/csv"});
  const url=URL.createObjectURL(blob);
  const a=document.createElement("a");
  a.href=url; a.download="herencias_filtradas.csv"; a.click();
  URL.revokeObjectURL(url);
};
</script>

</body>
</html>

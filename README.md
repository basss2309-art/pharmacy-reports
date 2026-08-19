# pharmacy-reports
Объединение приходных накладных 
<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Объединение приходных накладных</title>
<style>
*{margin:0;padding:0;box-sizing:border-box}
body{font-family:'Segoe UI',Tahoma,Geneva,Verdana,sans-serif;background:linear-gradient(135deg,#4e54c8 0%,#8f94fb 50%,#ff6b9d 100%);background-attachment:fixed;min-height:100vh;padding:20px}
.container{max-width:1450px;margin:0 auto;background:rgba(255,255,255,0.98);border-radius:20px;padding:25px;box-shadow:0 20px 60px rgba(0,0,0,0.25);backdrop-filter:blur(10px)}
h1{color:#2c3e50;margin-bottom:6px;font-size:24px;display:flex;align-items:center;gap:10px;font-weight:700;letter-spacing:-0.3px}
h1::before{content:"";display:inline-block;width:6px;height:28px;background:linear-gradient(180deg,#4e54c8,#ff6b9d);border-radius:3px}
.subtitle{color:#7f8c8d;margin-bottom:18px;font-size:13px;font-style:italic}
.upload-grid{display:grid;grid-template-columns:1fr 1fr;gap:18px;margin-bottom:22px}
.upload-section{background:linear-gradient(135deg,#f8f9ff 0%,#eef1ff 100%);border:2px dashed #667eea;border-radius:14px;padding:18px;text-align:center;transition:all .3s;position:relative;overflow:hidden}
.upload-section::before{content:"";position:absolute;top:-50%;left:-50%;width:200%;height:200%;background:radial-gradient(circle,rgba(102,126,234,0.05) 0%,transparent 70%);pointer-events:none}
.upload-section.p2{background:linear-gradient(135deg,#fff8f0 0%,#ffeedc 100%);border-color:#e67e22}
.upload-section.p2::before{background:radial-gradient(circle,rgba(230,126,34,0.05) 0%,transparent 70%)}
.upload-section.dragover{background:linear-gradient(135deg,#e8edff 0%,#d4dcff 100%);border-color:#4e54c8;transform:scale(1.01);box-shadow:0 8px 25px rgba(102,126,234,0.25)}
.upload-section.p2.dragover{background:linear-gradient(135deg,#fff3e0 0%,#ffe0b2 100%);border-color:#d35400;box-shadow:0 8px 25px rgba(230,126,34,0.25)}
.upload-section h3{color:#2c3e50;margin-bottom:6px;font-size:15px;font-weight:700;display:flex;align-items:center;justify-content:center;gap:8px}
.upload-section .badge{display:inline-block;padding:2px 10px;border-radius:10px;font-size:10px;font-weight:700;color:#fff;letter-spacing:0.5px;text-transform:uppercase}
.upload-section .badge.b1{background:linear-gradient(90deg,#667eea,#764ba2)}
.upload-section .badge.b2{background:linear-gradient(90deg,#e67e22,#d35400)}
.upload-section p{color:#7f8c8d;margin-bottom:10px;font-size:12px}
.upload-btn-wrapper{position:relative;overflow:hidden;display:inline-block}
.upload-btn-wrapper input[type=file]{position:absolute;left:0;top:0;opacity:0;width:100%;height:100%;cursor:pointer}
.btn{padding:8px 20px;background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);color:#fff;border:none;border-radius:8px;font-size:13px;cursor:pointer;transition:all .3s;font-weight:600;box-shadow:0 4px 12px rgba(102,126,234,0.3)}
.btn:hover{transform:translateY(-2px);box-shadow:0 6px 18px rgba(102,126,234,0.45)}
.btn:active{transform:translateY(0)}
.btn.p2{background:linear-gradient(135deg,#e67e22 0%,#d35400 100%);box-shadow:0 4px 12px rgba(230,126,34,0.3)}
.btn.p2:hover{box-shadow:0 6px 18px rgba(230,126,34,0.45)}
.btn-danger{background:linear-gradient(135deg,#ff6b6b 0%,#ee5a6f 100%);box-shadow:0 4px 12px rgba(238,90,111,0.3)}
.btn-danger:hover{box-shadow:0 6px 18px rgba(238,90,111,0.45)}
.btn-success{background:linear-gradient(135deg,#28a745 0%,#20c997 100%);box-shadow:0 4px 12px rgba(40,167,69,0.3)}
.btn-success:hover{box-shadow:0 6px 18px rgba(40,167,69,0.45)}
.btn-warning{background:linear-gradient(135deg,#ffc107 0%,#ffb300 100%);color:#333;box-shadow:0 4px 12px rgba(255,193,7,0.3)}
.btn-warning:hover{box-shadow:0 6px 18px rgba(255,193,7,0.45)}
.btn-info{background:linear-gradient(135deg,#17a2b8 0%,#138496 100%);box-shadow:0 4px 12px rgba(23,162,184,0.3)}
.btn-info:hover{box-shadow:0 6px 18px rgba(23,162,184,0.45)}
.btn-sm{padding:6px 14px;font-size:12px}
.file-list{margin-top:12px;display:flex;flex-wrap:wrap;gap:6px;justify-content:center;max-height:90px;overflow-y:auto;padding:4px}
.file-item{background:#fff;padding:4px 12px;border-radius:15px;border:1px solid #e0e0e0;display:flex;align-items:center;gap:7px;font-size:11px;box-shadow:0 2px 6px rgba(0,0,0,0.05);transition:all .2s}
.file-item:hover{transform:translateY(-1px);box-shadow:0 4px 10px rgba(0,0,0,0.1)}
.file-item .remove{color:#ff6b6b;cursor:pointer;font-weight:700;font-size:14px;transition:transform .2s}
.file-item .remove:hover{transform:scale(1.3)}
.controls{display:flex;gap:10px;flex-wrap:wrap;margin-bottom:16px;align-items:center}
.search-box{flex:1;min-width:200px;padding:9px 16px;border:2px solid #e0e0e0;border-radius:10px;font-size:13px;transition:all .3s;background:#f8f9fa}
.search-box:focus{outline:none;border-color:#667eea;background:#fff;box-shadow:0 0 0 3px rgba(102,126,234,0.15)}
.stats{color:#555;font-size:12px;padding:6px 14px;background:linear-gradient(135deg,#f8f9fa,#e9ecef);border-radius:15px;white-space:nowrap;font-weight:600;border:1px solid #e0e0e0}
.barcode-section{background:linear-gradient(135deg,#f0f4ff 0%,#e8edff 100%);border:1px solid #c8d2f5;border-radius:12px;padding:12px 16px;margin-bottom:16px;display:flex;flex-wrap:wrap;align-items:center;gap:10px;box-shadow:inset 0 1px 3px rgba(0,0,0,0.03)}
.barcode-section .label{font-weight:700;color:#2c3e50;font-size:13px}
.barcode-list{display:flex;flex-wrap:wrap;gap:5px;flex:1}
.barcode-tag{background:linear-gradient(135deg,#667eea,#764ba2);color:#fff;padding:3px 11px;border-radius:14px;font-size:11px;font-family:'Courier New',monospace;letter-spacing:.4px;box-shadow:0 2px 6px rgba(102,126,234,0.25);transition:transform .2s}
.barcode-tag:hover{transform:translateY(-1px)}
.barcode-tag.found{background:linear-gradient(135deg,#28a745,#20c997);box-shadow:0 2px 6px rgba(40,167,69,0.3)}
.barcode-tag.not-found{background:linear-gradient(135deg,#ff6b6b,#ee5a6f);box-shadow:0 2px 6px rgba(255,107,107,0.3)}
.barcode-tag.unknown{background:linear-gradient(135deg,#95a5a6,#7f8c8d);box-shadow:0 2px 6px rgba(149,165,166,0.3)}
.table-wrapper{overflow-x:auto;border-radius:12px;border:1px solid #e0e0e0;max-height:480px;overflow-y:auto;box-shadow:0 4px 15px rgba(0,0,0,0.05)}
table{width:100%;border-collapse:collapse;font-size:12px;background:#fff;table-layout:fixed}
thead{position:sticky;top:0;z-index:10}
thead th{background:linear-gradient(180deg,#667eea 0%,#5568d3 100%);color:#fff;padding:8px 12px;text-align:left;font-weight:600;border-right:1px solid rgba(255,255,255,0.15);font-size:12px;position:relative;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;user-select:none;letter-spacing:0.2px}
thead th:last-child{border-right:none}
thead th .resizer{position:absolute;right:0;top:0;width:6px;height:100%;cursor:col-resize;background:transparent;z-index:5;transition:background .2s}
thead th .resizer:hover,thead th .resizer.active{background:rgba(255,255,255,0.4)}
thead th .resizer::after{content:"";position:absolute;right:2px;top:25%;width:2px;height:50%;background:rgba(255,255,255,0.3);border-radius:1px}
thead th .resizer:hover::after{background:rgba(255,255,255,0.8)}
tbody td{padding:5px 12px;border-bottom:1px solid #f0f0f0;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;font-size:12px;transition:background .15s}
tbody tr{transition:background .15s}
tbody tr:hover{background:#f8f9ff}
tbody tr:nth-child(even){background:#fafbff}
tbody tr:nth-child(even):hover{background:#eef1ff}
tbody tr.barcode-match{background:#d4edda!important}
tbody tr.barcode-match:hover{background:#c3e6cb!important}
tbody tr.barcode-match td:first-child{box-shadow:inset 3px 0 0 #28a745}
.empty-state{text-align:center;padding:50px 20px;color:#95a5a6}
.empty-state .emoji{font-size:48px;display:block;margin-bottom:12px;filter:drop-shadow(0 4px 8px rgba(0,0,0,0.1))}
.empty-state h3{color:#555;margin-bottom:6px;font-size:16px}
.export-section{margin-top:16px;display:flex;gap:10px;justify-content:flex-end;flex-wrap:wrap}
.progress-bar{width:100%;height:5px;background:#e9ecef;border-radius:3px;margin:10px 0;overflow:hidden;display:none;box-shadow:inset 0 1px 2px rgba(0,0,0,0.05)}
.progress-bar .fill{height:100%;background:linear-gradient(90deg,#667eea,#ff6b9d,#e67e22);background-size:200% 100%;width:0%;transition:width .3s;border-radius:3px;animation:shimmer 2s linear infinite}
@keyframes shimmer{0%{background-position:200% 0}100%{background-position:-200% 0}}
.divider{height:2px;background:linear-gradient(90deg,transparent 0%,#667eea 25%,#ff6b9d 50%,#e67e22 75%,transparent 100%);margin:12px 0;border-radius:2px;opacity:0.5}
@media(max-width:768px){.upload-grid{grid-template-columns:1fr}.controls{flex-direction:column}.search-box{width:100%}table{font-size:10px}thead th,tbody td{padding:3px 6px}.export-section{flex-direction:column}.barcode-section{flex-direction:column;align-items:stretch}}
</style>
</head>
<body>
<div class="container">
<h1>Объединение приходных накладных</h1>
<p class="subtitle">Загрузите файлы из двух источников — данные объединятся в одну таблицу</p>

<div class="upload-grid">
<!-- ОКНО 1: Загрузка с Rubus -->
<div class="upload-section" id="dropZone1">
<h3>📤 Загрузка с Rubus <span class="badge b1">Rubus</span></h3>
<p>Стандартные файлы с автопоиском столбцов</p>
<div class="upload-btn-wrapper">
<button class="btn">Выбрать файлы</button>
<input type="file" id="fileInput1" multiple accept=".xlsx,.xls,.csv">
</div>
<div class="file-list" id="fileList1"></div>
</div>

<!-- ОКНО 2: Загрузка с PharmKassa -->
<div class="upload-section p2" id="dropZone2">
<h3>📥 Загрузка с PharmKassa <span class="badge b2">PharmKassa</span></h3>
<p>Склад→Филиал, Штрихкод, Срок годности, Товар, Цена, Количество, Сумма, Серия</p>
<div class="upload-btn-wrapper">
<button class="btn p2">Выбрать файлы</button>
<input type="file" id="fileInput2" multiple accept=".xlsx,.xls,.csv">
</div>
<div class="file-list" id="fileList2"></div>
</div>
</div>

<div class="barcode-section">
<span class="label">🔍 Отслеживаемые штрихкоды:</span>
<div class="barcode-list" id="barcodeList"></div>
</div>

<div class="controls">
<input type="text" class="search-box" id="searchInput" placeholder="🔍 Поиск по таблице...">
<button class="btn btn-success btn-sm" id="processBtn">🔄 Объединить</button>
<button class="btn btn-info btn-sm" id="filterBarcodeBtn">🎯 Только отслеживаемые шк</button>
<button class="btn btn-danger btn-sm" id="clearBtn">🗑️ Очистить</button>
<span class="stats" id="stats">Файлов: 0 | Записей: 0</span>
</div>

<div class="progress-bar" id="progressBar"><div class="fill" id="progressFill"></div></div>

<div class="table-wrapper">
<div id="tableContainer">
<div class="empty-state">
<span class="emoji">📊</span>
<h3>Нет данных</h3>
<p>Загрузите файлы в оба окна и нажмите "Объединить"</p>
</div>
</div>
</div>

<div class="export-section">
<button class="btn btn-warning btn-sm" id="exportExcelBtn">📥 Выгрузить приходы в Excel</button>
<button class="btn btn-info btn-sm" id="exportFoundBtn">📥 Выгрузить отслеживаемые шк в Excel</button>
</div>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/xlsx-js-style@1.2.0/dist/xlsx.bundle.js"></script>
<script>
// ===== СПИСОК ШТРИХКОДОВ =====
const TARGET_BARCODES = [
'4812317012807','4812845005456','4810621002859','4810046007675',
'4812845005678','4812845008174','4810046013119','4812845004947',
'4812317012760','4810046004605','4812845007719','4812845001328',
'4812845005135','4810621001814','4812845005692','4870203881456'
];
const FIXED_BARCODES = new Set(TARGET_BARCODES);

// ===== ПЕРЕМЕННЫЕ =====
let allFiles1=[], allFiles2=[], combinedData=[], headers=[], showOnlyBarcodes=false, barcodeStatus={};
const fileInput1=document.getElementById('fileInput1'), fileList1=document.getElementById('fileList1');
const fileInput2=document.getElementById('fileInput2'), fileList2=document.getElementById('fileList2');
const barcodeList=document.getElementById('barcodeList');
const dropZone1=document.getElementById('dropZone1'), dropZone2=document.getElementById('dropZone2');
const searchInput=document.getElementById('searchInput'), processBtn=document.getElementById('processBtn');
const clearBtn=document.getElementById('clearBtn'), filterBarcodeBtn=document.getElementById('filterBarcodeBtn');
const exportExcelBtn=document.getElementById('exportExcelBtn'), exportFoundBtn=document.getElementById('exportFoundBtn');
const tableContainer=document.getElementById('tableContainer'), stats=document.getElementById('stats');
const progressBar=document.getElementById('progressBar'), progressFill=document.getElementById('progressFill');

// ===== ИЗМЕНЕНИЕ РАЗМЕРА СТОЛБЦОВ =====
function initResizableColumns() {
const table = document.querySelector('table');
if (!table) return;
const cols = table.querySelectorAll('th');
let currentCol = null, startX = 0, startWidth = 0, resizerEl = null;

cols.forEach((col) => {
// Удаляем старый resizer если есть
const old = col.querySelector('.resizer');
if(old) old.remove();
const resizer = document.createElement('div');
resizer.className = 'resizer';
resizer.addEventListener('mousedown', (e) => {
e.stopPropagation();
currentCol = col;
resizerEl = resizer;
startX = e.clientX;
startWidth = col.offsetWidth;
resizer.classList.add('active');
document.addEventListener('mousemove', onMouseMove);
document.addEventListener('mouseup', onMouseUp);
document.body.style.cursor = 'col-resize';
document.body.style.userSelect = 'none';
e.preventDefault();
});
col.appendChild(resizer);
});

function onMouseMove(e) {
if (!currentCol) return;
const newWidth = startWidth + (e.clientX - startX);
if (newWidth > 30) {
currentCol.style.width = newWidth + 'px';
currentCol.style.minWidth = newWidth + 'px';
const colIndex = Array.from(currentCol.parentElement.children).indexOf(currentCol);
const tableEl = currentCol.closest('table');
tableEl.querySelectorAll('tbody tr').forEach(row => {
const cell = row.children[colIndex];
if (cell) {
cell.style.width = newWidth + 'px';
cell.style.minWidth = newWidth + 'px';
}
});
}
}
function onMouseUp() {
if(resizerEl) resizerEl.classList.remove('active');
currentCol = null;
resizerEl = null;
document.removeEventListener('mousemove', onMouseMove);
document.removeEventListener('mouseup', onMouseUp);
document.body.style.cursor = '';
document.body.style.userSelect = '';
}
}

// ===== УТИЛИТЫ =====
function isTargetBarcode(row){
return row.some(cell => {
if(cell === undefined || cell === null || cell === '') return false;
const str = String(cell).trim();
return TARGET_BARCODES.some(barcode => str === barcode || str.includes(barcode));
});
}
function renderBarcodeList(){
barcodeList.innerHTML=TARGET_BARCODES.map(b=>{
const s=barcodeStatus[b]||'unknown';
return `<span class="barcode-tag ${s}">${b}</span>`;
}).join('');
}
function updateStats(){
const total=combinedData.length;
let found=combinedData.filter(r=>isTargetBarcode(r)).length;
const totalFiles=allFiles1.length+allFiles2.length;
stats.textContent=`Файлов: ${totalFiles} | Записей: ${total} | Найдено: ${found}`;
}
function setProgress(p){progressBar.style.display='block';progressFill.style.width=p+'%';if(p>=100)setTimeout(()=>{progressBar.style.display='none'},500);}
function isSkipRow(row){
if(!row||!row.length)return true;
const t=row.filter(c=>c!==undefined&&c!==null&&c!=='').map(c=>String(c).toLowerCase()).join(' ');
return t.includes('приходная накладная')||t.includes('на оптовую сумму');
}
function cleanStr(v){return typeof v==='string'?v.trim().replace(/\s+/g,' '):v;}
function readFile(file){
return new Promise((res,rej)=>{
const r=new FileReader();
r.onload=e=>{try{const d=new Uint8Array(e.target.result);const wb=XLSX.read(d,{type:'array'});res(wb);}catch(err){rej(err);}};
r.onerror=rej;r.readAsArrayBuffer(file);
});
}
function normalizeHeader(v){
return String(v ?? '').toLowerCase().replace(/ё/g,'е').replace(/[^a-zа-я0-9]+/gi,' ').replace(/\s+/g,' ').trim();
}

// ===== ЗАГРУЗКА ФАЙЛОВ =====
function handleFiles1(files){
const ef=Array.from(files).filter(f=>['xlsx','xls','csv'].includes(f.name.split('.').pop().toLowerCase()));
if(!ef.length){alert('Загрузите Excel или CSV');return;}
ef.forEach(f=>{if(!allFiles1.some(x=>x.name===f.name&&x.size===f.size))allFiles1.push(f);});
updateFileList1();updateStats();
}
function handleFiles2(files){
const ef=Array.from(files).filter(f=>['xlsx','xls','csv'].includes(f.name.split('.').pop().toLowerCase()));
if(!ef.length){alert('Загрузите Excel или CSV');return;}
ef.forEach(f=>{if(!allFiles2.some(x=>x.name===f.name&&x.size===f.size))allFiles2.push(f);});
updateFileList2();updateStats();
}
function updateFileList1(){
fileList1.innerHTML=allFiles1.map((f,i)=>`
<div class="file-item">📄 ${f.name} (${(f.size/1024).toFixed(0)}KB) <span class="remove" onclick="removeFile1(${i})">✕</span></div>
`).join('');
}
function updateFileList2(){
fileList2.innerHTML=allFiles2.map((f,i)=>`
<div class="file-item">📄 ${f.name} (${(f.size/1024).toFixed(0)}KB) <span class="remove" onclick="removeFile2(${i})">✕</span></div>
`).join('');
}
function removeFile1(i){allFiles1.splice(i,1);updateFileList1();updateStats();}
function removeFile2(i){allFiles2.splice(i,1);updateFileList2();updateStats();}

// ===== ОБРАБОТКА ОКНА 1 (Rubus) =====
function findHeaderRow1(json){
let best=null,bestScore=0;
for(let i=0;i<Math.min(json.length,30);i++){
const row=json[i]||[];
const h=row.map(normalizeHeader);
let score=0;
h.forEach(x=>{
if(x.includes('штрихкод')||x.includes('штрих код')||x.includes('barcode')) score+=5;
if(x.includes('срок годности')||x.includes('срок годн')||x.includes('годен до')) score+=5;
if(x.includes('наименование')||x.includes('название товара')) score+=4;
if(x.includes('оптовая цена')||x==='опт цена'||x.includes('цена опт')) score+=3;
if(x.includes('розничная цена')||x==='розн цена'||x.includes('цена розн')) score+=3;
if(x==='кол'||x.includes('количество')) score+=2;
if(x.includes('серия')||x.includes('сертификат')) score+=2;
if(x.includes('тнвэд')||x.includes('тн вэд')) score+=2;
});
if(score>bestScore){bestScore=score;best={index:i,row};}
}
return bestScore>=5?best:null;
}
function extractBranch(json){
const firstRow = json && json.length ? (json[0] || []) : [];
const whole = firstRow.map(v => String(v ?? '').trim()).filter(Boolean).join(' ');
if (!whole) return '';
const match = whole.match(/((?:ул|пр|пер|мкр|проспект|переулок|микрорайон|бульвар|бул)\.?\s*.+)$/i);
if (match) return match[1].trim();
const cityMatch = whole.match(/(город\s+\S+\s*.+)$/i);
if (cityMatch) return cityMatch[1].trim();
return '';
}
async function processFiles1(){
const targetHeaders=['Филиал','Штрихкод','Срок годн','Наименование','Опт.цена','Розн.цена','Кол','Стоим','Стоим.опт','Серия и сертификат','В уп','Cумма НДС(опт)','ТНВЭД'];
const rules={
'Штрихкод':['штрихкод','штрих код','barcode','код товара'],
'Срок годн':['срок годности','срок годн','годен до'],
'Наименование':['наименование товара','наименование','название товара','название'],
'Опт.цена':['оптовая цена','опт цена','цена опт','оптовая'],
'Розн.цена':['розничная цена','розн цена','цена розн','розничная'],
'Кол':['количество','кол во','колво','кол'],
'Стоим.опт':['стоимость опт','стоим опт','сумма опт','сумма оптовая'],
'Стоим':['стоимость','стоим','сумма'],
'Серия и сертификат':['серия и сертификат','серия сертификат','номер серии','сертификат','серия'],
'В уп':['в уп','в упаковке','упаковка','упак','фасовка'],
'Cумма НДС(опт)':['сумма ндс опт','ндс опт','сумма ндс','ндс'],
'ТНВЭД':['код тнвэд','тнвэд','тн вэд']
};
for(const file of allFiles1){
const wb=await readFile(file);
const ws=wb.Sheets[wb.SheetNames[0]];
const json=XLSX.utils.sheet_to_json(ws,{header:1,defval:''});
const branch=extractBranch(json);
const info=findHeaderRow1(json);
if(!info){console.warn('Заголовки не найдены:',file.name);continue;}
const header=info.row;
const normalized=header.map(normalizeHeader);
const used=new Set();
const map={};
Object.keys(rules).forEach(field=>{
for(let i=0;i<normalized.length;i++){
if(!used.has(i) && rules[field].includes(normalized[i])){
map[field]=i;used.add(i);break;
}
}
});
Object.keys(rules).forEach(field=>{
if(map[field]!==undefined)return;
let best=-1,scoreBest=0;
for(let i=0;i<normalized.length;i++){
if(used.has(i)||!normalized[i])continue;
let score=0;
rules[field].forEach(key=>{if(normalized[i].includes(key))score=Math.max(score,key.length);});
if(field==='Опт.цена' && normalized[i].includes('розн'))score=0;
if(field==='Розн.цена' && normalized[i].includes('опт'))score=0;
if(field==='Стоим' && (normalized[i].includes('опт')||normalized[i].includes('ндс')))score=0;
if(field==='Стоим.опт' && !normalized[i].includes('опт'))score=0;
if(score>scoreBest){scoreBest=score;best=i;}
}
if(best>=0){map[field]=best;used.add(best);}
});
json.slice(info.index+1).forEach(row=>{
if(!row||!row.length||isSkipRow(row))return;
const values={
'Филиал':branch,
'Штрихкод': map['Штрихкод']!==undefined ? cleanStr(row[map['Штрихкод']]) : '',
'Срок годн': map['Срок годн']!==undefined ? cleanStr(row[map['Срок годн']]) : '',
'Наименование': map['Наименование']!==undefined ? cleanStr(row[map['Наименование']]) : '',
'Опт.цена': map['Опт.цена']!==undefined ? cleanStr(row[map['Опт.цена']]) : '',
'Розн.цена': map['Розн.цена']!==undefined ? cleanStr(row[map['Розн.цена']]) : '',
'Кол': map['Кол']!==undefined ? cleanStr(row[map['Кол']]) : '',
'Стоим': map['Стоим']!==undefined ? cleanStr(row[map['Стоим']]) : '',
'Стоим.опт': map['Стоим.опт']!==undefined ? cleanStr(row[map['Стоим.опт']]) : '',
'Серия и сертификат': map['Серия и сертификат']!==undefined ? cleanStr(row[map['Серия и сертификат']]) : '',
'В уп': map['В уп']!==undefined ? cleanStr(row[map['В уп']]) : '',
'Cумма НДС(опт)': map['Cумма НДС(опт)']!==undefined ? cleanStr(row[map['Cумма НДС(опт)']]) : '',
'ТНВЭД': map['ТНВЭД']!==undefined ? cleanStr(row[map['ТНВЭД']]) : ''
};
values['Штрихкод']=String(values['Штрихкод']??'').trim();
if(Object.keys(values).some(k=>k!=='Филиал' && values[k]!=='')){
combinedData.push(targetHeaders.map(h=>values[h]));
}
});
}
}

// ===== ОБРАБОТКА ОКНА 2 (PharmKassa) =====
const SOURCE_MAP = {
'склад':'Филиал','штрихкод':'Штрихкод','срок годности':'Срок годн','срокгодности':'Срок годн','годен до':'Срок годн',
'товар':'Наименование','наименование':'Наименование','название':'Наименование','названиетовара':'Наименование',
'цена':'Опт.цена','оптоваяцена':'Опт.цена',
'количество':'Кол','кол':'Кол','колво':'Кол',
'сумма':'Стоим.опт','стоимость':'Стоим.опт',
'серия':'Серия и сертификат','номерсерии':'Серия и сертификат','серияиномер':'Серия и сертификат'
};
function findHeaderRow2(json){
let best=null,bestScore=0;
for(let i=0;i<Math.min(json.length,30);i++){
const row=json[i]||[];
const h=row.map(v=>String(v??'').toLowerCase().replace(/ё/g,'е').replace(/[^a-zа-я0-9]+/gi,'').trim());
let score=0;
const keys=['склад','штрихкод','срокгодности','товар','цена','количество','сумма','серия'];
h.forEach(x=>{if(!x) return;keys.forEach(k=>{if(x.includes(k)) score+=3;});});
if(score>bestScore){bestScore=score;best={index:i,row};}
}
return bestScore>=6?best:null;
}
function buildColumnMap2(headerRow){
const normalized = headerRow.map(v=>String(v??'').toLowerCase().replace(/ё/g,'е').replace(/[^a-zа-я0-9]+/gi,'').trim());
const map = {};
const used = new Set();
normalized.forEach((cellText, idx)=>{
if(!cellText) return;
for(const key of Object.keys(SOURCE_MAP)){
if(cellText.includes(key) && !used.has(idx)){
const ourField = SOURCE_MAP[key];
if(map[ourField]===undefined){map[ourField] = idx;used.add(idx);}
break;
}
}
});
return map;
}
async function processFiles2(){
const targetHeaders=['Филиал','Штрихкод','Срок годн','Наименование','Опт.цена','Розн.цена','Кол','Стоим','Стоим.опт','Серия и сертификат','В уп','Cумма НДС(опт)','ТНВЭД'];
for(const file of allFiles2){
const wb=await readFile(file);
const ws=wb.Sheets[wb.SheetNames[0]];
const json=XLSX.utils.sheet_to_json(ws,{header:1,defval:''});
const info=findHeaderRow2(json);
if(!info){console.warn('[PharmKassa] Заголовки не найдены:',file.name);continue;}
const colMap = buildColumnMap2(info.row);
json.slice(info.index+1).forEach(row=>{
if(!row||!row.length) return;
const hasData = row.some(c=>c!==undefined&&c!==null&&c!=='');
if(!hasData) return;
const get = (field) => {
const idx = colMap[field];
if(idx===undefined) return '';
const v = row[idx];
if(v===undefined||v===null) return '';
return typeof v==='string' ? v.trim().replace(/\s+/g,' ') : v;
};
const values = {
'Филиал':get('Филиал'),'Штрихкод':String(get('Штрихкод')??'').trim(),'Срок годн':get('Срок годн'),
'Наименование':get('Наименование'),'Опт.цена':get('Опт.цена'),'Розн.цена':'—','Кол':get('Кол'),
'Стоим':'—','Стоим.опт':get('Стоим.опт'),'Серия и сертификат':get('Серия и сертификат'),
'В уп':'—','Cумма НДС(опт)':'—','ТНВЭД':'—'
};
if(!values['Штрихкод'] && !values['Наименование']) return;
combinedData.push(targetHeaders.map(h=>values[h]));
});
}
}

// ===== ОСНОВНАЯ ОБРАБОТКА =====
async function processFiles(){
if(!allFiles1.length && !allFiles2.length){alert('Загрузите файлы хотя бы в одно окно!');return;}
try{
processBtn.disabled=true;
processBtn.textContent='⏳ Обработка...';
combinedData=[];
const totalFiles=allFiles1.length+allFiles2.length;
let processed=0;

if(allFiles1.length){
await processFiles1();
processed+=allFiles1.length;
setProgress(processed/totalFiles*100);
}
if(allFiles2.length){
await processFiles2();
processed+=allFiles2.length;
setProgress(processed/totalFiles*100);
}

combinedData=combinedData.map((r,i)=>[i+1,...r]);
headers=['№','Филиал','Штрихкод','Срок годн','Наименование','Опт.цена','Розн.цена','Кол','Стоим','Стоим.опт','Серия и сертификат','В уп','Cумма НДС(опт)','ТНВЭД'];
barcodeStatus={};
combinedData.forEach(row=>{
const barcode=String(row[2]??'').trim();
if(!barcode)return;
barcodeStatus[barcode]={fixed:FIXED_BARCODES.has(barcode),exists:true};
});
renderTable(combinedData);
updateStats();
processBtn.textContent='✅ Готово!';
setTimeout(()=>{processBtn.textContent='🔄 Объединить';processBtn.disabled=false;},1500);
}catch(e){
console.error(e);
alert('Ошибка: '+e.message);
processBtn.textContent='🔄 Объединить';
processBtn.disabled=false;
}
}

// ===== ТАБЛИЦА =====
function renderTable(data){
if(!data||!data.length){
tableContainer.innerHTML=`<div class="empty-state"><span class="emoji">📊</span><h3>Нет данных</h3><p>Загрузите файлы и нажмите "Объединить"</p></div>`;
return;
}
let display=data;
if(showOnlyBarcodes)display=data.filter(r=>isTargetBarcode(r));
if(!display.length){
tableContainer.innerHTML=`<div class="empty-state"><span class="emoji">🔍</span><h3>Ничего не найдено</h3></div>`;
return;
}
let html='<table id="mainTable"><thead><tr>';
headers.forEach(h=>html+=`<th>${h||'—'}</th>`);
html+='</tr></thead><tbody>';
display.forEach(row=>{
const match=isTargetBarcode(row);
html+=`<tr${match?' class="barcode-match"':''}>`;
row.forEach(c=>{
const cellContent = c!==undefined&&c!==null&&c!=='' ? c : '—';
html+=`<td>${cellContent}</td>`;
});
html+='</tr>';
});
html+='</tbody></table>';
tableContainer.innerHTML=html;
setTimeout(initResizableColumns, 50);
}
function searchTable(){
const q=searchInput.value.toLowerCase().trim();
let data=showOnlyBarcodes?combinedData.filter(r=>isTargetBarcode(r)):combinedData;
if(!q){renderTable(combinedData);return;}
const f=data.filter(r=>r.some(c=>c!==undefined&&c!==null&&c!==''&&String(c).toLowerCase().includes(q)));
renderTable(f);
if(f.length)stats.textContent=`Найдено: ${f.length} из ${combinedData.length}`;
}
function toggleFilter(){showOnlyBarcodes=!showOnlyBarcodes;filterBarcodeBtn.textContent=showOnlyBarcodes?'📋 Все':'🎯 Только отслеживаемые шк';renderTable(combinedData);}
function clearAll(){
allFiles1=[];allFiles2=[];combinedData=[];headers=[];showOnlyBarcodes=false;
filterBarcodeBtn.textContent='🎯 Только отслеживаемые шк';
fileList1.innerHTML='';fileList2.innerHTML='';
tableContainer.innerHTML=`<div class="empty-state"><span class="emoji">📊</span><h3>Нет данных</h3><p>Загрузите файлы и нажмите "Объединить"</p></div>`;
searchInput.value='';
TARGET_BARCODES.forEach(b=>barcodeStatus[b]='unknown');
renderBarcodeList();updateStats();
}

// ===== ВЫГРУЗКА =====
function makeSheetName(s){
let name = String(s || 'Аптека').replace(/[\\\/\?\*\[\]:]/g, '_').trim();
if(!name) name = 'Аптека';
return name.slice(0, 31);
}
function parseNum(v){
if(v === null || v === undefined || v === '' || v === '—') return 0;
const n = parseFloat(String(v).replace(',', '.').replace(/\s+/g, ''));
return isNaN(n) ? 0 : n;
}
function round2(n){ return Math.round(n * 100) / 100; }
function buildWorkbook(sourceData, filenamePrefix){
if(!sourceData || !sourceData.length){ alert('Нет данных!'); return; }
const groups = {};
const groupOrder = [];
sourceData.forEach(row => {
const branch = (row[1] && String(row[1]).trim()) || 'Без филиала';
if(!groups[branch]){ groups[branch] = []; groupOrder.push(branch); }
groups[branch].push(row);
});
const wb = XLSX.utils.book_new();
const branchSums = [];
const usedNames = {};
const yellowLabel = { fill:{fgColor:{rgb:'FFFF00'}}, font:{bold:true,sz:12}, alignment:{horizontal:'right'} };
const headerStyle = { fill:{fgColor:{rgb:'667EEA'}}, font:{bold:true,color:{rgb:'FFFFFF'},sz:11}, alignment:{horizontal:'center'} };
const branchTitleStyle = { font:{bold:true,sz:14,color:{rgb:'333333'}}, alignment:{horizontal:'left'} };
const numberStyle = { numFmt:'#,##0.00', alignment:{horizontal:'right'} };
const totalNumberStyle = { fill:{fgColor:{rgb:'FFFF00'}}, font:{bold:true,sz:12}, numFmt:'#,##0.00', alignment:{horizontal:'right'} };

groupOrder.forEach(branch => {
const rows = groups[branch];
const data = [];
data.push([branch, '', '', '', '']);
data.push(['Штрихкод', 'Наименование', 'Кол-во', 'Цена закупа', 'Сумма']);
let sumTotal = 0;
rows.forEach(row => {
const barcode = row[2] ?? '';
const name = row[4] ?? '';
const qty = parseNum(row[7]);
const price = parseNum(row[5]);
const sum = round2(qty * price);
sumTotal += sum;
data.push([String(barcode), String(name), qty || '', price || '', sum || '']);
});
sumTotal = round2(sumTotal);
data.push([]);
const totalRowIdx = data.length;
data.push(['', '', '', 'Итого:', sumTotal]);
const ws = XLSX.utils.aoa_to_sheet(data);
ws['!cols'] = [{wch:18},{wch:55},{wch:10},{wch:16},{wch:16}];
ws['!merges'] = [{s:{r:0,c:0},e:{r:0,c:4}}];
if(ws['A1']) ws['A1'].s = branchTitleStyle;
for(let c=0;c<5;c++){
const addr = XLSX.utils.encode_cell({r:1,c});
if(ws[addr]) ws[addr].s = headerStyle;
}
for(let r=2;r<totalRowIdx-1;r++){
['2','3','4'].forEach(c=>{
const addr = XLSX.utils.encode_cell({r,c:parseInt(c)});
if(ws[addr] && ws[addr].v !== '' && ws[addr].v !== null){
ws[addr].s = numberStyle;ws[addr].t = 'n';
}
});
}
const totalD = XLSX.utils.encode_cell({r:totalRowIdx,c:3});
const totalE = XLSX.utils.encode_cell({r:totalRowIdx,c:4});
if(ws[totalD]) ws[totalD].s = yellowLabel;
if(ws[totalE]){ ws[totalE].s = totalNumberStyle; ws[totalE].t = 'n'; }
branchSums.push({branch, sum: sumTotal});
let baseName = makeSheetName(branch);
let finalName = baseName;
let counter = 1;
while(usedNames[finalName]){
const suffix = `_${counter}`;
finalName = baseName.slice(0, 31 - suffix.length) + suffix;
counter++;
}
usedNames[finalName] = true;
XLSX.utils.book_append_sheet(wb, ws, finalName);
});

const summaryData = [];
summaryData.push(['Общий итог по всем аптекам', '', '']);
summaryData.push(['Аптека (филиал)', 'Сумма', '']);
let grandTotal = 0;
branchSums.forEach(b => { summaryData.push([b.branch, b.sum, '']); grandTotal += b.sum; });
grandTotal = round2(grandTotal);
summaryData.push([]);
const grandIdx = summaryData.length;
summaryData.push(['', 'ИТОГО ВСЕГО:', grandTotal]);
const wsSum = XLSX.utils.aoa_to_sheet(summaryData);
wsSum['!cols'] = [{wch:45},{wch:20},{wch:10}];
wsSum['!merges'] = [{s:{r:0,c:0},e:{r:0,c:2}}];
if(wsSum['A1']) wsSum['A1'].s = {font:{bold:true,sz:16,color:{rgb:'333333'}}};
for(let c=0;c<3;c++){
const addr = XLSX.utils.encode_cell({r:1,c});
if(wsSum[addr]) wsSum[addr].s = headerStyle;
}
for(let r=2;r<grandIdx-1;r++){
const addr = XLSX.utils.encode_cell({r,c:1});
if(wsSum[addr] && wsSum[addr].v !== '' && wsSum[addr].v !== null){
wsSum[addr].s = numberStyle;wsSum[addr].t = 'n';
}
}
const gtD = XLSX.utils.encode_cell({r:grandIdx,c:1});
const gtE = XLSX.utils.encode_cell({r:grandIdx,c:2});
if(wsSum[gtD]) wsSum[gtD].s = yellowLabel;
if(wsSum[gtE]){ wsSum[gtE].s = totalNumberStyle; wsSum[gtE].t = 'n'; }
XLSX.utils.book_append_sheet(wb, wsSum, 'Общий итог');
const sn = wb.SheetNames;
const idx = sn.indexOf('Общий итог');
if(idx > 0){ sn.splice(idx, 1); sn.unshift('Общий итог'); }
return {wb, branchSums, grandTotal};
}
function saveWorkbook(wb, filename){
const out = XLSX.write(wb, {bookType:'xlsx', type:'array', cellStyles:true});
const blob = new Blob([out], {type:'application/octet-stream'});
const a = document.createElement('a');
a.href = URL.createObjectURL(blob);
a.download = `${filename}_${new Date().toISOString().split('T')[0]}.xlsx`;
document.body.appendChild(a); a.click(); document.body.removeChild(a);
}
function exportAll(){
if(!combinedData.length){ alert('Нет данных!'); return; }
const {wb} = buildWorkbook(combinedData, 'Приходные_по_аптекам');
saveWorkbook(wb, 'Приходные_по_аптекам');
}
function exportFound(){
const f = combinedData.filter(r => isTargetBarcode(r));
if(!f.length){ alert('Нет найденных штрихкодов!'); return; }
const {wb} = buildWorkbook(f, 'Найденные_штрихкоды');
saveWorkbook(wb, 'Найденные_штрихкоды');
}

// ===== СОБЫТИЯ =====
fileInput1.addEventListener('change',e=>{handleFiles1(e.target.files);fileInput1.value='';});
fileInput2.addEventListener('change',e=>{handleFiles2(e.target.files);fileInput2.value='';});
dropZone1.addEventListener('dragover',e=>{e.preventDefault();dropZone1.classList.add('dragover');});
dropZone1.addEventListener('dragleave',e=>{e.preventDefault();dropZone1.classList.remove('dragover');});
dropZone1.addEventListener('drop',e=>{e.preventDefault();dropZone1.classList.remove('dragover');handleFiles1(e.dataTransfer.files);});
dropZone2.addEventListener('dragover',e=>{e.preventDefault();dropZone2.classList.add('dragover');});
dropZone2.addEventListener('dragleave',e=>{e.preventDefault();dropZone2.classList.remove('dragover');});
dropZone2.addEventListener('drop',e=>{e.preventDefault();dropZone2.classList.remove('dragover');handleFiles2(e.dataTransfer.files);});
processBtn.addEventListener('click',processFiles);
clearBtn.addEventListener('click',clearAll);
filterBarcodeBtn.addEventListener('click',toggleFilter);
exportExcelBtn.addEventListener('click',exportAll);
exportFoundBtn.addEventListener('click',exportFound);
let st;searchInput.addEventListener('input',()=>{clearTimeout(st);st=setTimeout(searchTable,200);});

// ===== СТАРТ =====
renderBarcodeList();
updateStats();
console.log('✅ Готово! Загрузите файлы в оба окна.');
</script>
</body>
</html>

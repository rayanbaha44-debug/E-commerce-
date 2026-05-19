<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>PRO STOCK SYSTEM FULL</title>

<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:system-ui;}

body{
background:#0a0f1c;
color:white;
display:flex;
justify-content:center;
align-items:center;
height:100vh;
}

/* DASHBOARD */
#dashboard{
display:grid;
grid-template-columns:repeat(2,1fr);
gap:12px;
width:340px;
}

.card{
background:#111827;
padding:18px;
border-radius:12px;
text-align:center;
cursor:pointer;
border:1px solid #1f2937;
font-size:14px;
}

/* PAGE */
.page{display:none;width:100%;height:100vh;padding:20px;}
.page.active{display:block;}

.header{
display:flex;
justify-content:space-between;
align-items:center;
margin-bottom:12px;
}

button{
padding:10px;
border:none;
border-radius:8px;
cursor:pointer;
background:#22c55e;
color:black;
font-weight:bold;
}

.back{background:#ef4444;color:white;}

input,select{
width:100%;
padding:10px;
margin:5px 0;
border-radius:8px;
border:none;
}

table{
width:100%;
margin-top:10px;
border-collapse:collapse;
background:#111827;
border-radius:10px;
overflow:hidden;
}

td,th{
padding:10px;
text-align:center;
border-bottom:1px solid #1f2937;
}

.box{
margin-top:10px;
background:#111827;
padding:10px;
border-radius:10px;
line-height:1.7;
}

/* ALERT */
#alertBox{
position:fixed;
top:10px;
right:10px;
padding:10px 15px;
border-radius:10px;
display:none;
z-index:9999;
font-weight:bold;
color:black;
}
</style>
</head>

<body>

<!-- ALERT -->
<div id="alertBox"></div>

<!-- DASHBOARD -->
<div id="dashboard">
<div class="card" onclick="openPage('products')">📦 المنتجات</div>
<div class="card" onclick="openPage('sales')">🧾 البيع</div>
<div class="card" onclick="openPage('stock')">📊 المخزون</div>
<div class="card" onclick="openPage('low')">⚠ المنتجات الناقصة</div>
</div>

<!-- PRODUCTS -->
<div id="products" class="page">
<div class="header">
<button class="back" onclick="back()">⬅ رجوع</button>
<h2>📦 المنتجات</h2>
</div>

<input id="pName" placeholder="اسم المنتج">
<input id="pBuy" placeholder="سعر الشراء">
<input id="pSell" placeholder="سعر البيع">
<input id="pQty" placeholder="الكمية">
<button onclick="addBatch()">إضافة</button>

<table>
<tbody id="productTable"></tbody>
</table>
</div>

<!-- SALES -->
<div id="sales" class="page">
<div class="header">
<button class="back" onclick="back()">⬅ رجوع</button>
<h2>🧾 البيع</h2>
</div>

<select id="saleSelect"></select>
<input id="saleQty" type="number" value="1">
<button onclick="sell()">بيع</button>

<table>
<tbody id="salesTable"></tbody>
</table>
</div>

<!-- STOCK -->
<div id="stock" class="page">
<div class="header">
<button class="back" onclick="back()">⬅ رجوع</button>
<h2>📊 المخزون + رأس المال</h2>
</div>

<table>
<thead>
<tr>
<th>المنتج</th>
<th>الكمية</th>
<th>رأس المال</th>
<th>الربح</th>
</tr>
</thead>
<tbody id="stockTable"></tbody>
</table>

<div class="box" id="totals"></div>
</div>

<!-- LOW STOCK -->
<div id="low" class="page">
<div class="header">
<button class="back" onclick="back()">⬅ رجوع</button>
<h2>⚠ المنتجات الناقصة</h2>
</div>

<table>
<thead>
<tr>
<th>المنتج</th>
<th>الكمية</th>
<th>الحالة</th>
</tr>
</thead>
<tbody id="lowTable"></tbody>
</table>
</div>

<script>

/* DATA */
let batches = JSON.parse(localStorage.getItem("batches")||"[]");
let sales = JSON.parse(localStorage.getItem("sales")||"[]");

/* NAV */
function openPage(id){
document.getElementById("dashboard").style.display="none";
document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
document.getElementById(id).classList.add("active");
}

function back(){
document.getElementById("dashboard").style.display="grid";
document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
}

/* SAVE */
function save(){
localStorage.setItem("batches",JSON.stringify(batches));
localStorage.setItem("sales",JSON.stringify(sales));
}

/* ADD PRODUCT */
function addBatch(){

let name = pName.value.trim();
let buy = +pBuy.value;
let sell = +pSell.value;
let qty = +pQty.value;

if(!name || !buy || !sell || !qty) return;

batches.push({name,buy,sell,qty});

save();
render();
}

/* SELL */
function sell(){

let i = saleSelect.value;
let qty = +saleQty.value;

let b = batches[i];
if(!b || b.qty < qty) return;

b.qty -= qty;

sales.push({
name:b.name,
qty,
profit:(b.sell-b.buy)*qty
});

save();
render();
}

/* ALERT */
function checkAlert(){

let low = batches.filter(b=>b.qty<=3);
let danger = batches.filter(b=>b.qty<=1);

let box = document.getElementById("alertBox");

if(low.length===0){
box.style.display="none";
return;
}

if(danger.length>0){
box.style.background="#ef4444";
box.innerHTML="🔴 خطر: "+danger.map(b=>b.name).join(" | ");
}else{
box.style.background="#facc15";
box.innerHTML="🟡 نقص: "+low.map(b=>b.name).join(" | ");
}

box.style.display="block";
}

/* LOW STOCK */
function renderLow(){

let low = batches.filter(b=>b.qty<=3);

lowTable.innerHTML = low.map(b=>`
<tr>
<td>${b.name}</td>
<td>${b.qty}</td>
<td>${b.qty<=1?"🔴 خطر":"🟡 ناقص"}</td>
</tr>
`).join('');
}

/* RENDER */
function render(){

productTable.innerHTML = batches.map(b=>`
<tr>
<td>${b.name}</td>
<td>${b.qty}</td>
<td>${b.buy}</td>
<td>${b.sell}</td>
</tr>
`).join('');

stockTable.innerHTML = batches.map(b=>`
<tr>
<td>${b.name}</td>
<td>${b.qty}</td>
<td>${(b.buy*b.qty).toFixed(2)}</td>
<td>${((b.sell-b.buy)*b.qty).toFixed(2)}</td>
</tr>
`).join('');

salesTable.innerHTML = sales.map(s=>`
<tr>
<td>${s.name}</td>
<td>${s.qty}</td>
<td>${s.profit.toFixed(2)}</td>
</tr>
`).join('');

saleSelect.innerHTML = batches.map((b,i)=>`
<option value="${i}">
${b.name} | شراء:${b.buy} | بيع:${b.sell} | كمية:${b.qty}
</option>
`).join('');

let capital = batches.reduce((a,b)=>a+(b.buy*b.qty),0);
let profit = batches.reduce((a,b)=>a+((b.sell-b.buy)*b.qty),0);

totals.innerHTML = `
💰 رأس المال: ${capital.toFixed(2)} DA<br>
📈 الأرباح: ${profit.toFixed(2)} DA<br>
💼 المجموع: ${(capital+profit).toFixed(2)} DA
`;

renderLow();
checkAlert();
}

render();

</script>

</body>
</html>

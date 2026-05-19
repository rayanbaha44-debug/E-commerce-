<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>FULL STOCK & PRODUCTS SYSTEM FIX</title>

<style>
*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:system-ui;
}

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
width:360px;
}

.card{
background:#111827;
padding:18px;
border-radius:12px;
text-align:center;
cursor:pointer;
border:1px solid #1f2937;
}

/* PAGES */
.page{
display:none;
width:100%;
height:100vh;
padding:20px;
}

.page.active{
display:block;
}

/* HEADER */
.header{
display:flex;
justify-content:space-between;
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

.back{
background:#ef4444;
color:white;
}

/* INPUT FIX */
input,select{
width:100%;
padding:10px;
margin:5px 0;
border-radius:8px;
border:none;
background:#111827;
color:white;
outline:none;
}

input:focus,select:focus{
border:1px solid #22c55e;
box-shadow:0 0 8px rgba(34,197,94,0.4);
}

/* TABLE */
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

/* DELETE */
.del{
background:#ef4444;
color:white;
padding:5px 8px;
border-radius:6px;
cursor:pointer;
font-size:12px;
}
</style>
</head>

<body>

<!-- DASHBOARD -->
<div id="dashboard">
<div class="card" onclick="openPage('products')">📦 المنتجات</div>
<div class="card" onclick="openPage('sales')">🧾 البيع</div>
<div class="card" onclick="openPage('stock')">📊 المخزون</div>
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
<button onclick="addProduct()">إضافة منتج</button>

<table>
<thead>
<tr>
<th>الاسم</th>
<th>الكمية</th>
<th>شراء</th>
<th>بيع</th>
<th>حذف</th>
</tr>
</thead>
<tbody id="productTable"></tbody>
</table>
</div>

<!-- SALES -->
<div id="sales" class="page">
<div class="header">
<button class="back" onclick="back()">⬅ رجوع</button>
<h2>🧾 البيع</h2>
</div>

<input id="searchInput" placeholder="🔎 بحث منتج" oninput="search()">

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
<h2>📊 المخزون + الحسابات</h2>
</div>

<table>
<thead>
<tr>
<th>المنتج</th>
<th>الكمية</th>
<th>رأس المال</th>
<th>الربح</th>
<th>حذف</th>
</tr>
</thead>
<tbody id="stockTable"></tbody>
</table>

<div id="totals" style="margin-top:10px;background:#111827;padding:10px;border-radius:10px;"></div>
</div>

<script>

/* DATA SAFE FIX */
let batches = JSON.parse(localStorage.getItem("batches")||"[]");
let sales = JSON.parse(localStorage.getItem("sales")||"[]");

if(!Array.isArray(batches)) batches = [];
if(!Array.isArray(sales)) sales = [];

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
function addProduct(){

let name = pName.value.trim();
let buy = +pBuy.value;
let sell = +pSell.value;
let qty = +pQty.value;

if(!name || !buy || !sell || !qty) return;

batches.push({
id:Date.now(),
name,
buy,
sell,
qty
});

save();
render();
}

/* DELETE PRODUCT */
function deleteProduct(id){
batches = batches.filter(b=>b.id!==id);
save();
render();
}

/* SEARCH */
function search(){

let val = searchInput.value.toLowerCase();

let filtered = batches.filter(b=>b.name.toLowerCase().includes(val));

saleSelect.innerHTML = filtered.map(b=>`
<option value="${b.id}">
${b.name} | qty:${b.qty}
</option>
`).join('');
}

/* SELL */
function sell(){

let id = +saleSelect.value;
let qty = +saleQty.value;

let b = batches.find(x=>x.id===id);
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

/* RENDER EVERYTHING (FIXED STRONG) */
function render(){

/* PRODUCTS */
productTable.innerHTML = "";
batches.forEach(b=>{
productTable.innerHTML += `
<tr>
<td>${b.name || ""}</td>
<td>${b.qty || 0}</td>
<td>${b.buy || 0}</td>
<td>${b.sell || 0}</td>
<td><span class="del" onclick="deleteProduct(${b.id})">حذف</span></td>
</tr>
`;
});

/* STOCK */
stockTable.innerHTML = "";
batches.forEach(b=>{

let capital = (b.buy||0)*(b.qty||0);
let profit = ((b.sell||0)-(b.buy||0))*(b.qty||0);

stockTable.innerHTML += `
<tr>
<td>${b.name || ""}</td>
<td>${b.qty || 0}</td>
<td>${capital.toFixed(2)}</td>
<td>${profit.toFixed(2)}</td>
<td><span class="del" onclick="deleteProduct(${b.id})">حذف</span></td>
</tr>
`;
});

/* SALES */
salesTable.innerHTML = sales.map(s=>`
<tr>
<td>${s.name}</td>
<td>${s.qty}</td>
<td>${s.profit.toFixed(2)}</td>
</tr>
`).join('');

/* SELECT */
saleSelect.innerHTML = batches.map(b=>`
<option value="${b.id}">
${b.name} | شراء:${b.buy} | بيع:${b.sell} | qty:${b.qty}
</option>
`).join('');

/* TOTALS */
let capital = batches.reduce((a,b)=>a+(b.buy*b.qty),0);
let profit = batches.reduce((a,b)=>a+((b.sell-b.buy)*b.qty),0);

totals.innerHTML = `
💰 رأس المال: ${capital.toFixed(2)} DA<br>
📈 الأرباح: ${profit.toFixed(2)} DA<br>
💼 المجموع: ${(capital+profit).toFixed(2)} DA
`;

}

render();

</script>

</body>
</html>

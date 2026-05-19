<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>BATCH STOCK SYSTEM</title>

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

#dashboard{
display:grid;
grid-template-columns:repeat(2,1fr);
gap:15px;
width:320px;
}

.card{
background:#111827;
padding:20px;
border-radius:12px;
text-align:center;
cursor:pointer;
border:1px solid #1f2937;
}

.page{display:none;width:100%;height:100vh;padding:20px;}
.page.active{display:block;}

.header{
display:flex;
justify-content:space-between;
margin-bottom:15px;
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
margin:6px 0;
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
line-height:1.6;
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
<h2>📦 إضافة ستوك</h2>
</div>

<input id="pName" placeholder="اسم المنتج">
<input id="pBuy" placeholder="سعر الشراء">
<input id="pSell" placeholder="سعر البيع">
<input id="pQty" placeholder="الكمية">
<button onclick="addBatch()">إضافة ستوك</button>

<table>
<tbody id="productTable"></tbody>
</table>
</div>

<!-- SALES -->
<div id="sales" class="page">
<div class="header">
<button class="back" onclick="back()">⬅ رجوع</button>
<h2>🧾 البيع (اختيار ستوك)</h2>
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
<h2>📊 كل الستوكات</h2>
</div>

<table>
<thead>
<tr>
<th>المنتج</th>
<th>الكمية</th>
<th>سعر الشراء</th>
<th>سعر البيع</th>
<th>ربح/وحدة</th>
</tr>
</thead>
<tbody id="stockTable"></tbody>
</table>

<div class="box" id="totals"></div>
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

/* ADD NEW BATCH */
function addBatch(){

batches.push({
name:pName.value,
buy:+pBuy.value,
sell:+pSell.value,
qty:+pQty.value
});

save();
render();
}

/* SELL FROM SELECTED BATCH */
function sell(){

let index = saleSelect.value;
let qty = +saleQty.value;

let b = batches[index];
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

/* RENDER */
function render(){

/* STOCK TABLE */
stockTable.innerHTML = batches.map((b,i)=>`
<tr>
<td>${b.name}</td>
<td>${b.qty}</td>
<td>${b.buy}</td>
<td>${b.sell}</td>
<td>${(b.sell-b.buy).toFixed(2)}</td>
</tr>
`).join('');

/* PRODUCTS TABLE */
productTable.innerHTML = batches.map(b=>`
<tr>
<td>${b.name}</td>
<td>${b.qty}</td>
</tr>
`).join('');

/* SALES TABLE */
salesTable.innerHTML = sales.map(s=>`
<tr>
<td>${s.name}</td>
<td>${s.qty}</td>
<td>${s.profit.toFixed(2)}</td>
</tr>
`).join('');

/* SELECT BATCH */
saleSelect.innerHTML = batches.map((b,i)=>`
<option value="${i}">
${b.name} | شراء:${b.buy} | بيع:${b.sell} | كمية:${b.qty}
</option>
`).join('');

/* TOTALS */
let totalProfit = sales.reduce((a,b)=>a+b.profit,0);

totals.innerHTML = `
📈 أرباح إجمالية: ${totalProfit.toFixed(2)} DA<br>
📦 عدد الستوكات: ${batches.length}
`;
}

render();

</script>

</body>
</html>

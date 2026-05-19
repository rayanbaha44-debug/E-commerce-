<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>PRO STOCK SYSTEM</title>

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
height:100vh;
display:flex;
justify-content:center;
align-items:center;
}

/* DASHBOARD */
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

/* PAGE */
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
align-items:center;
margin-bottom:20px;
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

input{
display:block;
margin:6px 0;
padding:10px;
width:100%;
border-radius:8px;
border:none;
}

/* TABLE */
table{
width:100%;
margin-top:15px;
border-collapse:collapse;
background:#111827;
border-radius:10px;
overflow:hidden;
}

th,td{
padding:10px;
border-bottom:1px solid #1f2937;
text-align:center;
}

/* TOTAL BOX */
.totalBox{
margin-top:15px;
background:#111827;
padding:15px;
border-radius:10px;
line-height:1.8;
}
</style>
</head>

<body>

<!-- DASHBOARD -->
<div id="dashboard">
<div class="card" onclick="openPage('products')">📦 المنتجات</div>
<div class="card" onclick="openPage('sales')">🧾 البيع</div>
<div class="card" onclick="openPage('stock')">📊 المخزون</div>
<div class="card" onclick="openPage('customers')">👥 الزبائن</div>
</div>

<!-- PRODUCTS -->
<div id="products" class="page">
<div class="header">
<button class="back" onclick="back()">⬅ رجوع</button>
<h2>📦 المنتجات</h2>
</div>

<input id="pName" placeholder="اسم">
<input id="pBuy" placeholder="سعر الشراء">
<input id="pSell" placeholder="سعر البيع">
<input id="pStock" placeholder="كمية">
<button onclick="addProduct()">إضافة / تحديث ستوك</button>

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

<input id="saleName" placeholder="اسم المنتج">
<input id="saleQty" type="number" value="1">
<button onclick="sell()">بيع</button>
</div>

<!-- STOCK -->
<div id="stock" class="page">
<div class="header">
<button class="back" onclick="back()">⬅ رجوع</button>
<h2>📊 المخزون</h2>
</div>

<table>
<thead>
<tr>
<th>المنتج</th>
<th>الكمية</th>
<th>سعر شراء متوسط</th>
<th>رأس المال</th>
<th>الربح</th>
</tr>
</thead>
<tbody id="stockTable"></tbody>
</table>

<div class="totalBox" id="totals"></div>

</div>

<!-- CUSTOMERS -->
<div id="customers" class="page">
<div class="header">
<button class="back" onclick="back()">⬅ رجوع</button>
<h2>👥 الزبائن</h2>
</div>

<input id="cName" placeholder="اسم">
<input id="cPhone" placeholder="هاتف">
<button onclick="addCustomer()">إضافة</button>
</div>

<script>

let products = JSON.parse(localStorage.getItem("products")||"[]");
let customers = JSON.parse(localStorage.getItem("customers")||"[]");

/* NAV */
function openPage(id){
document.getElementById("dashboard").style.display="none";

document.querySelectorAll(".page").forEach(p=>{
p.classList.remove("active");
});

document.getElementById(id).classList.add("active");
}

function back(){
document.getElementById("dashboard").style.display="grid";
document.querySelectorAll(".page").forEach(p=>{
p.classList.remove("active");
});
}

/* SAVE */
function save(){
localStorage.setItem("products",JSON.stringify(products));
localStorage.setItem("customers",JSON.stringify(customers));
}

/* 🔥 ADD PRODUCT WITH AVERAGE PRICE */
function addProduct(){

let name = pName.value;
let buy = +pBuy.value;
let sell = +pSell.value;
let stock = +pStock.value;

let p = products.find(x=>x.name===name);

if(p){
// 🔥 حساب متوسط السعر
let totalQty = p.stock + stock;
p.buy = ((p.buy * p.stock) + (buy * stock)) / totalQty;
p.stock += stock;
p.sell = sell; // آخر سعر بيع
}else{
products.push({name,buy,sell,stock});
}

save();
render();
}

/* SELL */
function sell(){
let p = products.find(x=>x.name===saleName.value);
if(!p || p.stock < saleQty.value) return;

p.stock -= +saleQty.value;

save();
render();
}

/* RENDER */
function render(){

productTable.innerHTML = products.map(p=>`
<tr>
<td>${p.name}</td>
<td>${p.stock}</td>
<td>${p.buy.toFixed(2)}</td>
<td>${(p.buy*p.stock).toFixed(2)} DA</td>
<td>${((p.sell-p.buy)*p.stock).toFixed(2)} DA</td>
</tr>
`).join('');

/* TOTALS */
let totalCapital = products.reduce((a,b)=>a+(b.buy*b.stock),0);
let totalProfit = products.reduce((a,b)=>a+((b.sell-b.buy)*b.stock),0);
let totalAll = totalCapital + totalProfit;

stockTable.innerHTML = "";

document.getElementById("totals").innerHTML = `
💰 مجموع رأس المال: ${totalCapital.toFixed(2)} DA<br>
📈 مجموع الأرباح: ${totalProfit.toFixed(2)} DA<br>
💼 المجموع الكلي: ${totalAll.toFixed(2)} DA
`;
}

render();

</script>

</body>
</html>

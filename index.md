<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>PRO FULL STOCK SYSTEM</title>

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

.back{
background:#ef4444;
color:white;
}

/* INPUT */
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
margin-top:10px;
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

/* DELETE */
.del{
background:#ef4444;
color:white;
border:none;
padding:5px 8px;
border-radius:6px;
cursor:pointer;
}

/* BOX */
.box{
margin-top:15px;
background:#111827;
padding:15px;
border-radius:10px;
line-height:1.7;
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
<div class="card" onclick="openPage('reports')">📊 التقارير</div>
<div class="card" onclick="openPage('low')">⚠ الناقص</div>
</div>

<!-- PRODUCTS -->
<div id="products" class="page">
<div class="header">
<button class="back" onclick="back()">⬅ رجوع</button>
<h2>📦 المنتجات</h2>
</div>

<input id="pName" placeholder="اسم">
<input id="pBuy" placeholder="شراء">
<input id="pSell" placeholder="بيع">
<input id="pStock" placeholder="كمية">
<button onclick="addProduct()">إضافة</button>

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

<input id="saleSearch" placeholder="ابحث">
<input id="saleQty" type="number" value="1">
<button onclick="sell()">بيع</button>

<div id="suggest"></div>

<table>
<tbody id="salesTable"></tbody>
</table>
</div>

<!-- STOCK -->
<div id="stock" class="page">
<div class="header">
<button class="back" onclick="back()">⬅ رجوع</button>
<h2>📊 المخزون</h2>
</div>

<table>
<tbody id="stockTable"></tbody>
</table>

<div class="box" id="totals"></div>
</div>

<!-- REPORTS -->
<div id="reports" class="page">
<div class="header">
<button class="back" onclick="back()">⬅ رجوع</button>
<h2>📊 التقارير</h2>
</div>

<div class="box" id="reportBox"></div>
</div>

<!-- LOW STOCK -->
<div id="low" class="page">
<div class="header">
<button class="back" onclick="back()">⬅ رجوع</button>
<h2>⚠ المنتجات الناقصة</h2>
</div>

<table>
<tbody id="lowTable"></tbody>
</table>
</div>

<script>

/* START EMPTY */
let products = JSON.parse(localStorage.getItem("products")||"[]");
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
localStorage.setItem("products",JSON.stringify(products));
localStorage.setItem("sales",JSON.stringify(sales));
}

/* ADD PRODUCT */
function addProduct(){

let name = pName.value.trim();
let buy = +pBuy.value;
let sell = +pSell.value;
let stock = +pStock.value;

if(!name || !buy || !sell || !stock) return;

let p = products.find(x=>x.name===name);

if(p){
let total = p.stock + stock;
p.buy = ((p.buy*p.stock)+(buy*stock))/total;
p.stock += stock;
p.sell = sell;
}else{
products.push({name,buy,sell,stock});
}

save();
render();
}

/* DELETE */
function deleteProduct(name){
products = products.filter(p=>p.name!==name);
save();
render();
}

/* SEARCH */
function search(){
let val = saleSearch.value.toLowerCase();
let box = document.getElementById("suggest");

if(!val){
box.innerHTML="";
return;
}

let res = products.filter(p=>p.name.toLowerCase().startsWith(val));

box.innerHTML = res.map(p=>`
<div onclick="selectP('${p.name}')">${p.name}</div>
`).join('');
}

function selectP(name){
saleSearch.value = name;
document.getElementById("suggest").innerHTML="";
}

/* SELL */
function sell(){

let p = products.find(x=>x.name===saleSearch.value);
if(!p || p.stock < saleQty.value) return;

let qty = +saleQty.value;

p.stock -= qty;

sales.push({
name:p.name,
qty,
profit:(p.sell-p.buy)*qty,
date:new Date().toISOString().split("T")[0]
});

save();
render();
}

/* ALERT */
function checkAlert(){

let low = products.filter(p=>p.stock<=3);
let danger = products.filter(p=>p.stock<=1);

let box = document.getElementById("alertBox");

if(low.length===0){
box.style.display="none";
return;
}

if(danger.length>0){
box.style.background="#ef4444";
box.innerHTML="🔴 خطر: "+danger.map(p=>p.name).join(" | ");
}else{
box.style.background="#facc15";
box.innerHTML="🟡 نقص: "+low.map(p=>p.name).join(" | ");
}

box.style.display="block";
}

/* REPORTS */
function filterDays(days){
let now=new Date();
let limit=new Date();
limit.setDate(now.getDate()-days);

return sales.filter(s=>new Date(s.date)>=limit);
}

function calc(arr){
return {
qty:arr.reduce((a,b)=>a+b.qty,0),
profit:arr.reduce((a,b)=>a+b.profit,0)
};
}

/* RENDER */
function render(){

/* PRODUCTS */
productTable.innerHTML = products.map(p=>`
<tr>
<td>${p.name}</td>
<td>${p.stock}</td>
<td>${p.buy.toFixed(2)}</td>
<td>${((p.sell-p.buy)*p.stock).toFixed(2)}</td>
<td><button class="del" onclick="deleteProduct('${p.name}')">حذف</button></td>
</tr>
`).join('');

/* STOCK */
stockTable.innerHTML = productTable.innerHTML;

/* SALES */
salesTable.innerHTML = sales.map(s=>`
<tr>
<td>${s.name}</td>
<td>${s.qty}</td>
<td>${s.profit.toFixed(2)}</td>
<td>${s.date}</td>
</tr>
`).join('');

/* TOTALS */
let cap = products.reduce((a,b)=>a+(b.buy*b.stock),0);
let prof = products.reduce((a,b)=>a+((b.sell-b.buy)*b.stock),0);

totals.innerHTML = `
💰 رأس المال: ${cap.toFixed(2)} DA<br>
📈 الأرباح: ${prof.toFixed(2)} DA<br>
💼 المجموع: ${(cap+prof).toFixed(2)} DA
`;

/* REPORT */
let d=calc(filterDays(1));
let w=calc(filterDays(7));
let m=calc(filterDays(30));
let y=calc(filterDays(365));

reportBox.innerHTML=`
📅 يومي: ${d.profit} DA<br>
📆 أسبوعي: ${w.profit} DA<br>
🗓️ شهري: ${m.profit} DA<br>
📊 سنوي: ${y.profit} DA
`;

/* LOW STOCK */
lowTable.innerHTML = products.map(p=>`
<tr>
<td>${p.name}</td>
<td>${p.stock}</td>
<td>${p.stock<=1?"🔴 خطر":"🟡 ناقص"}</td>
</tr>
`).join('');

/* ALERT */
checkAlert();
}

render();

</script>

</body>
</html>

<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>POS SYSTEM PRO</title>

<style>
*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:system-ui;
}

body{
background:white;
color:black;
display:flex;
justify-content:center;
align-items:center;
height:100vh;
overflow:hidden;
}

#dashboard{
display:grid;
grid-template-columns:repeat(2,1fr);
gap:12px;
width:360px;
}

.card{
background:#f3f4f6;
padding:20px;
border-radius:14px;
text-align:center;
cursor:pointer;
border:1px solid #d1d5db;
font-weight:bold;
font-size:18px;
transition:.2s;
}

.card:hover{
transform:scale(1.03);
}

.page{
display:none;
width:100%;
height:100vh;
padding:20px;
overflow:auto;
}

.page.active{
display:block;
}

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

input,select{
width:100%;
padding:12px;
margin:6px 0;
border-radius:8px;
border:1px solid #ccc;
background:white;
color:black;
font-size:15px;
}

table{
width:100%;
margin-top:10px;
border-collapse:collapse;
background:white;
border-radius:10px;
overflow:hidden;
}

th,td{
padding:10px;
text-align:center;
border-bottom:1px solid #ddd;
}

.del{
background:#ef4444;
padding:5px 8px;
border-radius:6px;
font-size:12px;
color:white;
cursor:pointer;
}

.edit{
background:#3b82f6;
padding:5px 8px;
border-radius:6px;
font-size:12px;
color:white;
cursor:pointer;
}

#salesLog{
margin-top:15px;
background:#f3f4f6;
padding:10px;
border-radius:10px;
max-height:250px;
overflow:auto;
}

.saleItem{
padding:8px;
border-bottom:1px solid #ddd;
font-size:14px;
display:flex;
justify-content:space-between;
align-items:center;
gap:10px;
flex-wrap:wrap;
}

.box{
background:#f3f4f6;
padding:12px;
border-radius:12px;
margin-bottom:12px;
}
</style>
</head>

<body>

<!-- DASHBOARD -->
<div id="dashboard">
<div class="card" onclick="openPage('products')">📦 المنتجات</div>
<div class="card" onclick="openPage('sales')">🧾 البيع</div>
<div class="card" onclick="openPage('stock')">📊 المخزون</div>
<div class="card" onclick="openPage('low')">⚠ الناقص</div>
<div class="card" onclick="openPage('profits')">💰 الأرباح</div>
</div>

<!-- PRODUCTS -->
<div id="products" class="page">

<div class="header">
<button class="back" onclick="back()">⬅ رجوع</button>
<h2>📦 المنتجات</h2>
</div>

<input 
id="productSearch" 
placeholder="🔍 ابحث عن المنتج..." 
oninput="renderProducts()"
>

<input id="pName" placeholder="اسم المنتج">
<input id="pBuy" type="number" placeholder="سعر الشراء">
<input id="pSell" type="number" placeholder="سعر البيع">
<input id="pQty" type="number" placeholder="الكمية">

<button onclick="addProduct()">إضافة</button>

<table>
<thead>
<tr>
<th>الاسم</th>
<th>الكمية</th>
<th>شراء</th>
<th>بيع</th>
<th>تعديل</th>
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

<input id="saleSearch" placeholder="ابحث عن المنتج..." oninput="renderSales()">

<select id="saleStock"></select>

<input id="saleQty" type="number" value="1">

<button onclick="sell()">بيع</button>

<div id="salesLog"></div>
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
<th>رأس المال</th>
<th>الربح</th>
<th>حذف</th>
</tr>
</thead>
<tbody id="stockTable"></tbody>
</table>

<div id="totals" class="box"></div>
</div>

<!-- LOW -->
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

<!-- PROFITS -->
<div id="profits" class="page">
<div class="header">
<button class="back" onclick="back()">⬅ رجوع</button>
<h2>💰 الأرباح</h2>
</div>

<div class="box">
<h3>📊 الأرباح اليومية</h3>
<div id="dailyProfit"></div>
</div>

<div class="box">
<h3>📅 الأرباح الشهرية</h3>
<div id="monthlyProfit"></div>
</div>

<div class="box">
<h3>📆 الأرباح السنوية</h3>
<div id="yearlyProfit"></div>
</div>

<div class="box">
<h3>🗓 حساب الأرباح بين تاريخين</h3>

<input type="date" id="fromDate">
<input type="date" id="toDate">

<button onclick="calcProfitRange()">حساب</button>

<div id="rangeProfit" style="margin-top:10px;font-weight:bold;"></div>
</div>
</div>

<script>

let batches = JSON.parse(localStorage.getItem("batches") || "[]");
let sales = JSON.parse(localStorage.getItem("sales") || "[]");

if(!Array.isArray(batches)) batches=[];
if(!Array.isArray(sales)) sales=[];

function openPage(id){
document.getElementById("dashboard").style.display="none";
document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
document.getElementById(id).classList.add("active");
}

function back(){
document.getElementById("dashboard").style.display="grid";
document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
}

function save(){
localStorage.setItem("batches",JSON.stringify(batches));
localStorage.setItem("sales",JSON.stringify(sales));
}

/* ADD PRODUCT */
function addProduct(){

if(!pName.value || !pBuy.value || !pSell.value || !pQty.value) return;

batches.push({
id:Date.now(),
name:pName.value.trim(),
buy:+pBuy.value,
sell:+pSell.value,
qty:+pQty.value
});

pName.value="";
pBuy.value="";
pSell.value="";
pQty.value="";

save();
render();
}

/* EDIT PRODUCT */
function editProduct(id){

let b = batches.find(x=>x.id===id);

if(!b) return;

let newName = prompt("اسم المنتج", b.name);
if(newName===null) return;

let newBuy = prompt("سعر الشراء", b.buy);
if(newBuy===null) return;

let newSell = prompt("سعر البيع", b.sell);
if(newSell===null) return;

let newQty = prompt("الكمية", b.qty);
if(newQty===null) return;

b.name = newName;
b.buy = +newBuy;
b.sell = +newSell;
b.qty = +newQty;

save();
render();
}

/* DELETE PRODUCT */
function deleteProduct(id){

batches = batches.filter(b=>b.id!==id);

save();
render();
}

/* SELL */
function sell(){

let id = +saleStock.value;
let qty = +saleQty.value;

let b = batches.find(x=>x.id===id);

if(!b){
alert("المنتج غير موجود");
return;
}

if(qty <= 0){
alert("أدخل كمية صحيحة");
return;
}

if(b.qty < qty){
alert("الستوك غير كافي");
return;
}

b.qty = b.qty - qty;

sales.push({
name:b.name,
qty:qty,
sellPrice:b.sell,
profit:(b.sell-b.buy)*qty,
time:new Date().toISOString()
});

save();
render();
}

/* 🔥 DELETE SALE + RESTORE STOCK */
function deleteSale(index){

let s = sales[index];

if(!s) return;

/* رجوع الكمية للستوك */
let b = batches.find(x => x.name === s.name);

if(b){
b.qty += s.qty;
}

/* حذف عملية البيع */
sales.splice(index,1);

save();
render();
}

/* SMART PRODUCTS SEARCH */
function renderProducts(){

let search = productSearch.value.toLowerCase().trim();

let filtered = batches.filter(b =>
b.name.toLowerCase().includes(search)
);

productTable.innerHTML="";

filtered.forEach(b=>{

productTable.innerHTML += `
<tr>

<td>${b.name}</td>

<td>${b.qty}</td>

<td>${b.buy}</td>

<td>${b.sell}</td>

<td>
<span class="edit" onclick="editProduct(${b.id})">
تعديل
</span>
</td>

<td>
<span class="del" onclick="deleteProduct(${b.id})">
حذف
</span>
</td>

</tr>
`;

});

}

/* SALES SEARCH */
function renderSales(){

let search = saleSearch.value.toLowerCase();

let filtered = batches.filter(b=>
b.name.toLowerCase().includes(search)
);

saleStock.innerHTML = filtered.map(b=>
`<option value="${b.id}">
${b.name} | شراء: ${b.buy} | بيع: ${b.sell} | stock: ${b.qty}
</option>`
).join('');
}

/* PROFITS */
function renderProfits(){

let now = new Date();

let daily = sales.filter(s=>{
let d = new Date(s.time);
return d.toDateString() === now.toDateString();
}).reduce((a,b)=>a+b.profit,0);

let monthly = sales.filter(s=>{
let d = new Date(s.time);
return d.getMonth() === now.getMonth()
&& d.getFullYear() === now.getFullYear();
}).reduce((a,b)=>a+b.profit,0);

let yearly = sales.filter(s=>{
let d = new Date(s.time);
return d.getFullYear() === now.getFullYear();
}).reduce((a,b)=>a+b.profit,0);

dailyProfit.innerHTML = `💰 ${daily.toFixed(2)} DA`;
monthlyProfit.innerHTML = `💰 ${monthly.toFixed(2)} DA`;
yearlyProfit.innerHTML = `💰 ${yearly.toFixed(2)} DA`;
}

/* RANGE PROFITS */
function calcProfitRange(){

let from = new Date(fromDate.value || "2000-01-01");
let to = new Date(toDate.value || "2100-01-01");

to.setHours(23,59,59,999);

let total = sales.filter(s=>{
let d = new Date(s.time);
return d >= from && d <= to;
}).reduce((a,b)=>a+b.profit,0);

rangeProfit.innerHTML = `
📅 من: ${fromDate.value}<br>
📅 إلى: ${toDate.value}<br><br>
💰 الأرباح: ${total.toFixed(2)} DA
`;
}

/* RENDER */
function render(){

renderProducts();

/* STOCK */
stockTable.innerHTML="";

batches.forEach(b=>{

let capital = b.buy * b.qty;
let profit = (b.sell - b.buy) * b.qty;

stockTable.innerHTML += `
<tr>
<td>${b.name}</td>
<td>${b.qty}</td>
<td>${capital.toFixed(2)}</td>
<td>${profit.toFixed(2)}</td>
<td><span class="del" onclick="deleteProduct(${b.id})">حذف</span></td>
</tr>`;
});

/* LOW */
lowTable.innerHTML="";

batches.forEach(b=>{

if(b.qty <= 10){

let status = "";
let color = "";

if(b.qty <= 5){
status = "🔴 خطر";
color = "red";
}
else{
status = "🟡 ناقص";
color = "orange";
}

lowTable.innerHTML += `
<tr style="color:${color};font-weight:bold;">
<td>${b.name}</td>
<td>${b.qty}</td>
<td>${status}</td>
</tr>`;
}

});

/* TOTALS */
let capital = batches.reduce((a,b)=>a+(b.buy*b.qty),0);
let profit = batches.reduce((a,b)=>a+((b.sell-b.buy)*b.qty),0);

totals.innerHTML = `
💰 رأس المال: ${capital.toFixed(2)} DA<br>
📈 الأرباح: ${profit.toFixed(2)} DA<br>
💼 المجموع: ${(capital+profit).toFixed(2)} DA
`;

/* SALES LOG */
salesLog.innerHTML = sales.slice().reverse().map((s,reverseIndex)=>{

let index = sales.length - 1 - reverseIndex;

return `
<div class="saleItem">

<div>
⏰ ${new Date(s.time).toLocaleString()} |
📦 ${s.name} |
🔢 x${s.qty} |
💵 ${s.sellPrice} DA |
💰 ${s.profit} DA
</div>

<span
onclick="deleteSale(${index})"
style="
background:#ef4444;
color:white;
padding:4px 8px;
border-radius:6px;
cursor:pointer;
font-size:12px;
">
حذف
</span>

</div>
`;

}).join('');

renderSales();
renderProfits();
}

render();

</script>

</body>
</html>

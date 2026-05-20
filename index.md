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

<input id="pName" placeholder="اسم المنتج">
<input id="pBuy" type="number" placeholder="سعر الشراء">
<input id="pSell" type="number" placeholder="سعر البيع">
<input id="pQty" type="number" placeholder="الكمية">

<button onclick="addProduct()">إضافة</button>

<input id="productSearch" placeholder="🔍 ابحث عن المنتج..." oninput="renderProducts()">

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
<h2>⚠ الناقص</h2>
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

/* 🔥 FIX 1: تنظيف البيانات القديمة باش ما يخلطش الاسم مع التاريخ */
let batches = JSON.parse(localStorage.getItem("batches") || "[]").map(b=>({
id:b.id,
name:String(b.name||""),
buy:+b.buy||0,
sell:+b.sell||0,
qty:+b.qty||0
}));

let sales = JSON.parse(localStorage.getItem("sales") || "[]").map(s=>({
name:String(s.name||""),
qty:+s.qty||0,
sellPrice:+s.sellPrice||0,
profit:+s.profit||0,
time:s.time||Date.now()
}));

function save(){
localStorage.setItem("batches",JSON.stringify(batches));
localStorage.setItem("sales",JSON.stringify(sales));
}

function openPage(id){
document.getElementById("dashboard").style.display="none";
document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
document.getElementById(id).classList.add("active");
}

function back(){
document.getElementById("dashboard").style.display="grid";
document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
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

b.name = prompt("اسم المنتج", b.name) || b.name;
b.buy = +prompt("سعر الشراء", b.buy) || b.buy;
b.sell = +prompt("سعر البيع", b.sell) || b.sell;
b.qty = +prompt("الكمية", b.qty) || b.qty;

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

if(!b || b.qty < qty) return;

b.qty -= qty;

sales.push({
name:b.name,
qty:qty,
sellPrice:b.sell,
profit:(b.sell-b.buy)*qty,
time:Date.now()
});

save();
render();
}

/* PRODUCTS SEARCH */
function renderProducts(){

let search = (productSearch.value||"").toLowerCase();

productTable.innerHTML="";

batches.filter(b=>b.name.toLowerCase().includes(search))
.forEach(b=>{

productTable.innerHTML += `
<tr>
<td>${b.name}</td>
<td>${b.qty}</td>
<td>${b.buy}</td>
<td>${b.sell}</td>
<td><span class="edit" onclick="editProduct(${b.id})">تعديل</span></td>
<td><span class="del" onclick="deleteProduct(${b.id})">حذف</span></td>
</tr>
`;
});

}

/* SALES SELECT */
function renderSales(){
saleStock.innerHTML = batches.map(b=>
`<option value="${b.id}">
${b.name} | ${b.qty}
</option>`
).join('');
}

/* 🔥 FIX 2: عرض البيع بدون أي تلصاق نصوص */
salesLog.innerHTML = sales.slice().reverse().map((s,i)=>{

let d = new Date(s.time);

return `
<div class="saleItem">

<div>📦 ${String(s.name)}</div>
<div>🔢 x${s.qty}</div>
<div>💵 ${s.sellPrice} DA</div>
<div>💰 ${s.profit} DA</div>
<div>📅 ${isNaN(d) ? "--" : d.toLocaleString()}</div>

<span onclick="deleteSale(${sales.length-1-i})"
style="background:#ef4444;color:white;padding:4px 8px;border-radius:6px;cursor:pointer;">
حذف</span>

</div>
`;

}).join('');

/* DELETE SALE */
function deleteSale(i){
let s = sales[i];
if(!s) return;

let b = batches.find(x=>x.name===s.name);
if(b) b.qty += s.qty;

sales.splice(i,1);
save();
render();
}

/* MAIN */
function render(){

renderProducts();
renderSales();

stockTable.innerHTML="";
batches.forEach(b=>{
stockTable.innerHTML += `
<tr>
<td>${b.name}</td>
<td>${b.qty}</td>
<td>${b.buy*b.qty}</td>
<td>${(b.sell-b.buy)*b.qty}</td>
<td><span class="del" onclick="deleteProduct(${b.id})">حذف</span></td>
</tr>`;
});

salesLog.innerHTML = sales.slice().reverse().map((s,i)=>{

let d = new Date(s.time);

return `
<div class="saleItem">

<div>📦 ${String(s.name)}</div>
<div>🔢 x${s.qty}</div>
<div>💵 ${s.sellPrice} DA</div>
<div>💰 ${s.profit} DA</div>
<div>📅 ${isNaN(d) ? "--" : d.toLocaleString()}</div>

</div>
`;

}).join('');

}

render();

</script>

</body>
</html>

الكود هذا متنقص في ربو والو متفهمش ومتزيد والو غير لي نقولك انا دلي في قسم البيع زر خدف وتعديل وخانة بحث داكي بتاريخ والاسم خانة البحث تكون تحت زر اضافة ومتبدلي والو خلاف ومتنقصلي والو فالكود

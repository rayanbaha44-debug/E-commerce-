<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>FIXED POS SYSTEM</title>

<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:system-ui;}

body{
background:white;
color:black;
display:flex;
justify-content:center;
align-items:center;
height:100vh;
}

#dashboard{
display:grid;
grid-template-columns:repeat(2,1fr);
gap:12px;
width:360px;
}

.card{
background:#f3f4f6;
padding:18px;
border-radius:12px;
text-align:center;
cursor:pointer;
border:1px solid #d1d5db;
color:black;
}

.page{display:none;width:100%;height:100vh;padding:20px;}
.page.active{display:block;}

.header{
display:flex;
justify-content:space-between;
margin-bottom:12px;
color:black;
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
border:1px solid #ccc;
background:white;
color:black;
}

table{
width:100%;
margin-top:10px;
border-collapse:collapse;
background:white;
border-radius:10px;
overflow:hidden;
}

td,th{
padding:10px;
text-align:center;
border-bottom:1px solid #ddd;
color:black;
}

.del{
background:#ef4444;
padding:5px 8px;
border-radius:6px;
cursor:pointer;
font-size:12px;
color:white;
}

/* 🔥 SALES LOG */
#salesLog{
margin-top:15px;
background:#f3f4f6;
padding:10px;
border-radius:10px;
max-height:220px;
overflow:auto;
}

.saleItem{
padding:8px;
border-bottom:1px solid #ddd;
font-size:14px;
}
</style>
</head>

<body>

<div id="dashboard">
<div class="card" onclick="openPage('products')">📦 المنتجات</div>
<div class="card" onclick="openPage('sales')">🧾 البيع</div>
<div class="card" onclick="openPage('stock')">📊 المخزون</div>
<div class="card" onclick="openPage('low')">⚠ الناقص</div>
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
<button onclick="addProduct()">إضافة</button>

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

<input id="saleSearch" placeholder="ابحث عن المنتج..." oninput="renderSales()">

<select id="saleStock"></select>

<input id="saleQty" type="number" value="1">

<button onclick="sell()">بيع</button>

<!-- 🔥 LOG تحت البيع -->
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

<div id="totals" style="margin-top:10px;background:#f3f4f6;padding:10px;border-radius:10px;"></div>
</div>

<!-- LOW -->
<div id="low" class="page">
<div class="header">
<button class="back" onclick="back()">⬅ رجوع</button>
<h2>⚠ الناقص</h2>
</div>

<table>
<tbody id="lowTable"></tbody>
</table>
</div>

<script>

let batches = JSON.parse(localStorage.getItem("batches")||"[]");
let sales = JSON.parse(localStorage.getItem("sales")||"[]");

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

/* ADD */
function addProduct(){
batches.push({
id:Date.now(),
name:pName.value.trim(),
buy:+pBuy.value,
sell:+pSell.value,
qty:+pQty.value
});
save();
render();
}

/* DELETE */
function deleteProduct(id){
batches=batches.filter(b=>b.id!==id);
save();
render();
}

/* SELL */
function sell(){

let id=+saleStock.value;
let qty=+saleQty.value;

let b=batches.find(x=>x.id===id);
if(!b || b.qty<qty) return;

b.qty-=qty;

let profit=(b.sell-b.buy)*qty;

sales.push({
name:b.name,
qty,
sellPrice:b.sell,
profit,
time:new Date().toLocaleTimeString()
});

save();
render();
}

/* SEARCH */
function renderSales(){

let search=saleSearch.value.toLowerCase();

let filtered=batches.filter(b=>
b.name.toLowerCase().includes(search)
);

saleStock.innerHTML=filtered.map(b=>
`<option value="${b.id}">
${b.name} | شراء: ${b.buy} | بيع: ${b.sell} | stock: ${b.qty}
</option>`
).join('');
}

/* MAIN */
function render(){

productTable.innerHTML="";
batches.forEach(b=>{
productTable.innerHTML+=`
<tr>
<td>${b.name}</td>
<td>${b.qty}</td>
<td>${b.buy}</td>
<td>${b.sell}</td>
<td><span class="del" onclick="deleteProduct(${b.id})">حذف</span></td>
</tr>`;
});

stockTable.innerHTML="";
batches.forEach(b=>{
let capital=b.buy*b.qty;
let profit=(b.sell-b.buy)*b.qty;

stockTable.innerHTML+=`
<tr>
<td>${b.name}</td>
<td>${b.qty}</td>
<td>${capital.toFixed(2)}</td>
<td>${profit.toFixed(2)}</td>
<td><span class="del" onclick="deleteProduct(${b.id})">حذف</span></td>
</tr>`;
});

lowTable.innerHTML="";
batches.forEach(b=>{
if(b.qty<=3){
lowTable.innerHTML+=`
<tr>
<td>${b.name}</td>
<td>${b.qty}</td>
<td>${b.qty<=1?"🔴 خطر":"🟡 ناقص"}</td>
</tr>`;
}
});

/* TOTALS */
let capital=batches.reduce((a,b)=>a+(b.buy*b.qty),0);
let profit=batches.reduce((a,b)=>a+((b.sell-b.buy)*b.qty),0);

totals.innerHTML=`
💰 رأس المال: ${capital.toFixed(2)} DA<br>
📈 الأرباح: ${profit.toFixed(2)} DA<br>
💼 المجموع: ${(capital+profit).toFixed(2)} DA
`;

/* 🔥 SALES LOG */
salesLog.innerHTML = sales.slice().reverse().map(s=>
`<div class="saleItem">
⏰ ${s.time} | 📦 ${s.name} | 🔢 x${s.qty} | 💵 بيع: ${s.sellPrice} DA | 💰 ربح: ${s.profit} DA
</div>`
).join('');
}

render();

</script>

</body>
</html>

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

/* DASHBOARD */
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

.card:hover{transform:scale(1.03);}

/* PAGES */
.page{
display:none;
width:100%;
height:100vh;
padding:20px;
overflow:auto;
}

.page.active{display:block;}

.header{
display:flex;
justify-content:space-between;
align-items:center;
margin-bottom:15px;
}

/* BUTTONS */
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

/* INPUTS (🔴 FIX: مربعات بين الحقول) */
input,select{
width:100%;
padding:12px;
margin:8px 0;
border-radius:8px;
border:1px solid #ccc;
background:white;
color:black;
font-size:15px;
}

/* BOX FIX SEPARATION */
.inputBox{
margin-bottom:10px;
padding:8px;
border:1px solid #ddd;
border-radius:10px;
background:#fafafa;
}

/* TABLE */
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

/* ACTION BUTTONS (FIX POSITION) */
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

/* SALES LOG */
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
flex-wrap:wrap;
gap:8px;
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

<!-- 🔥 FIX: مربعات بين الإدخال -->
<div class="inputBox"><input id="pName" placeholder="اسم المنتج"></div>
<div class="inputBox"><input id="pBuy" type="number" placeholder="سعر الشراء"></div>
<div class="inputBox"><input id="pSell" type="number" placeholder="سعر البيع"></div>
<div class="inputBox"><input id="pQty" type="number" placeholder="الكمية"></div>

<button onclick="addProduct()">إضافة</button>

<input id="productSearch" placeholder="🔍 بحث..." oninput="render()">

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

<select id="saleStock"></select>
<input id="saleQty" type="number" value="1">

<button onclick="sell()">بيع</button>

<input id="saleSearch" placeholder="بحث..." oninput="render()">

<div id="salesLog"></div>
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

let batches = [];
let sales = [];

function openPage(id){
document.getElementById("dashboard").style.display="none";
document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
document.getElementById(id).classList.add("active");
}

function back(){
document.getElementById("dashboard").style.display="grid";
document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
}

/* ADD */
function addProduct(){
batches.push({
id:Date.now(),
name:pName.value,
buy:+pBuy.value,
sell:+pSell.value,
qty:+pQty.value
});
render();
}

/* EDIT */
function editProduct(id){
let b=batches.find(x=>x.id===id);
if(!b) return;

b.name=prompt("name",b.name)||b.name;
b.buy=+prompt("buy",b.buy)||b.buy;
b.sell=+prompt("sell",b.sell)||b.sell;
b.qty=+prompt("qty",b.qty)||b.qty;

render();
}

/* DELETE */
function deleteProduct(id){
batches=batches.filter(b=>b.id!==id);
render();
}

/* SELL */
function sell(){
let b=batches.find(x=>x.id==saleStock.value);
let q=+saleQty.value;
if(!b||b.qty<q) return;

b.qty-=q;

sales.push({
name:b.name,
qty:q,
sellPrice:b.sell,
profit:(b.sell-b.buy)*q,
time:Date.now()
});

render();
}

/* RENDER */
function render(){

/* PRODUCTS */
let search=(productSearch.value||"").toLowerCase();

productTable.innerHTML="";

batches.filter(b=>b.name.toLowerCase().includes(search))
.forEach(b=>{

productTable.innerHTML+=`
<tr>
<td>${b.name}</td>
<td>${b.qty}</td>
<td>${b.buy}</td>
<td>${b.sell}</td>

<td><span class="edit" onclick="editProduct(${b.id})">تعديل</span></td>
<td><span class="del" onclick="deleteProduct(${b.id})">حذف</span></td>

</tr>`;
});

/* STOCK */
stockTable.innerHTML="";
batches.forEach(b=>{
stockTable.innerHTML+=`
<tr>
<td>${b.name}</td>
<td>${b.qty}</td>
</tr>`;
});

/* LOW */
lowTable.innerHTML="";
batches.forEach(b=>{
if(b.qty<=10){
lowTable.innerHTML+=`
<tr>
<td>${b.name}</td>
<td>${b.qty}</td>
</tr>`;
}
});

/* SALES */
saleStock.innerHTML=batches.map(b=>
`<option value="${b.id}">${b.name}</option>`
).join('');

salesLog.innerHTML=sales.slice().reverse().map(s=>{
let d=new Date(s.time);

return `
<div class="saleItem">
📦 ${s.name} |
🔢 ${s.qty} |
💵 ${s.sellPrice} |
💰 ${s.profit} |
📅 ${d.toLocaleString()}
</div>
`;
}).join('');

}

render();

</script>

</body>
</html>

📊 لوحة معلومات / Dashboard
<html lang="ar" dir="rtl">

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
background:#f9fafb;
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
background:white;
padding:20px;
border-radius:14px;
text-align:center;
cursor:pointer;
border:1px solid #d1d5db;
font-weight:bold;
font-size:18px;
transition:.2s;
box-shadow:0 4px 12px rgba(0,0,0,.08);
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
box-shadow:0 2px 10px rgba(0,0,0,.05);
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
background:white;
padding:10px;
border-radius:10px;
max-height:250px;
overflow:auto;
box-shadow:0 2px 10px rgba(0,0,0,.05);
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
background:white;
padding:12px;
border-radius:12px;
margin-bottom:12px;
box-shadow:0 2px 10px rgba(0,0,0,.05);
}

</style>
</head>

<body>

<!-- DASHBOARD -->

<div id="dashboard">

<div class="card" onclick="openPage('products')">
المنتجات
</div>

<div class="card" onclick="openPage('sales')">
البيع
</div>

<div class="card" onclick="openPage('stock')">
المخزون
</div>

<div class="card" onclick="openPage('low')">
الناقص
</div>

<div class="card" onclick="openPage('profits')">
الأرباح
</div>

<div class="card" onclick="exportData()">
تصدير البيانات
</div>

</div>

<!-- PRODUCTS -->

<div id="products" class="page">

<div class="header">

<button class="back" onclick="back()">
رجوع
</button>

<h2>المنتجات</h2>

</div>

<input id="pRef" placeholder="الرفيرونس">

<input id="pName" placeholder="اسم المنتج">

<input id="pBuy" type="number" placeholder="سعر الشراء">

<input id="pSell" type="number" placeholder="سعر البيع">

<input id="pQty" type="number" placeholder="الكمية">

<button onclick="addProduct()">
إضافة
</button>

<input id="productSearch"
placeholder="ابحث عن المنتج أو الرفيرونس..."
oninput="renderProducts()">

<table>

<thead>

<tr>

<th>الرفيرونس</th>
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

<button class="back" onclick="back()">
رجوع
</button>

<h2>البيع</h2>

</div>

<div class="box">

<h3 id="cmdNumber">
Commande #1
</h3>

</div>

<input id="saleSearch"
placeholder="ابحث عن المنتج أو الرفيرونس..."
oninput="renderSales()">

<select id="saleStock"></select>

<input id="saleQty" type="number" value="1">

<button onclick="addToCommand()">
إضافة للكوموند
</button>

<div class="box">

<h3>منتجات الكوموند</h3>

<div id="currentCommand"></div>

<h3 id="commandTotal" style="margin-top:10px;">
المجموع: 0 DA
</h3>

<button style="margin-top:10px;"
onclick="confirmCommand()">

OK

</button>

</div>

<div id="salesLog"></div>

</div>

<!-- STOCK -->

<div id="stock" class="page">

<div class="header">

<button class="back" onclick="back()">
رجوع
</button>

<h2>المخزون</h2>

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

<button class="back" onclick="back()">
رجوع
</button>

<h2>المنتجات الناقصة</h2>

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

<button class="back" onclick="back()">
رجوع
</button>

<h2>الأرباح</h2>

</div>

<div class="box">

<h3>الأرباح اليومية</h3>

<div id="dailyProfit"></div>

</div>

<div class="box">

<h3>الأرباح الشهرية</h3>

<div id="monthlyProfit"></div>

</div>

<div class="box">

<h3>الأرباح السنوية</h3>

<div id="yearlyProfit"></div>

</div>

<div class="box">

<h3>حساب الأرباح بين تاريخين</h3>

<input type="date" id="fromDate">

<input type="date" id="toDate">

<button onclick="calcProfitRange()">
حساب
</button>

<div id="rangeProfit"
style="margin-top:10px;font-weight:bold;">
</div>

</div>

</div>

<script>

let batches = JSON.parse(localStorage.getItem("batches") || "[]");
let sales = JSON.parse(localStorage.getItem("sales") || "[]");

if(!Array.isArray(batches)) batches=[];
if(!Array.isArray(sales)) sales=[];

let currentCommandData = [];

let commandNumber = JSON.parse(
localStorage.getItem("commandNumber") || "1"
);

/* SAVE */

function save(){

localStorage.setItem(
"batches",
JSON.stringify(batches)
);

localStorage.setItem(
"sales",
JSON.stringify(sales)
);

}

/* OPEN PAGE */

function openPage(id){

document.getElementById("dashboard").style.display="none";

document.querySelectorAll(".page")
.forEach(p=>p.classList.remove("active"));

document.getElementById(id)
.classList.add("active");

}

/* BACK */

function back(){

document.getElementById("dashboard")
.style.display="grid";

document.querySelectorAll(".page")
.forEach(p=>p.classList.remove("active"));

}

/* ADD PRODUCT */

function addProduct(){

if(
!pRef.value ||
!pName.value ||
!pBuy.value ||
!pSell.value ||
!pQty.value
){
alert("أكمل جميع الحقول");
return;
}

if(
+pBuy.value <= 0 ||
+pSell.value <= 0 ||
+pQty.value <= 0
){
alert("القيم غير صالحة");
return;
}

batches.push({

id:Date.now(),

ref:pRef.value.trim(),

name:pName.value.trim(),

buy:+pBuy.value,

sell:+pSell.value,

qty:+pQty.value

});

pRef.value="";
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

let newRef = prompt("الرفيرونس", b.ref || "");

if(newRef===null) return;

let newName = prompt("اسم المنتج", b.name);

if(newName===null) return;

let newBuy = prompt("سعر الشراء", b.buy);

if(newBuy===null) return;

let newSell = prompt("سعر البيع", b.sell);

if(newSell===null) return;

let newQty = prompt("الكمية", b.qty);

if(newQty===null) return;

newBuy = +newBuy;
newSell = +newSell;
newQty = +newQty;

if(
newBuy <= 0 ||
newSell <= 0 ||
newQty < 0
){
alert("قيم غير صالحة");
return;
}

b.ref = newRef.trim();

b.name = newName.trim();

b.buy = newBuy;

b.sell = newSell;

b.qty = newQty;

save();

render();

}

/* DELETE PRODUCT */

function deleteProduct(id){

if(!confirm("هل أنت متأكد من حذف المنتج؟"))
return;

batches = batches.filter(b=>b.id!==id);

save();

render();

}

/* UPDATE COMMAND UI */

function updateCommandUI(){

cmdNumber.innerHTML = `Commande #${commandNumber}`;

currentCommand.innerHTML =
currentCommandData.map((item,i)=>`

<div class="saleItem">

<div>
${item.ref || ""}
|
${item.name}
|
x${item.qty}
|
${item.sell} DA
</div>

<div>

<span onclick="removeFromCommand(${i})"

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

</div>

`).join('');

let total = currentCommandData.reduce(
(a,b)=>a+(b.sell*b.qty),
0
);

commandTotal.innerHTML =
`المجموع: ${total.toFixed(2)} DA`;

}

/* ADD TO COMMAND */

function addToCommand(){

let id = +saleStock.value;

let qty = +saleQty.value;

let b = batches.find(x=>x.id===id);

if(!b) return;

if(qty <= 0){
alert("كمية غير صالحة");
return;
}

if(b.qty < qty){
alert("المخزون غير كاف");
return;
}

let existing =
currentCommandData.find(x=>x.id===id);

if(existing){

if((existing.qty + qty) > b.qty){

alert("تجاوزت المخزون");

return;

}

existing.qty += qty;

}else{

currentCommandData.push({

id:b.id,

ref:b.ref,

name:b.name,

qty:qty,

buy:b.buy,

sell:b.sell

});

}

updateCommandUI();

}

/* REMOVE ITEM */

function removeFromCommand(index){

currentCommandData.splice(index,1);

updateCommandUI();

}

/* CONFIRM COMMAND */

function confirmCommand(){

if(currentCommandData.length===0){
alert("الكوموند فارغ");
return;
}

currentCommandData.forEach(item=>{

let b = batches.find(x=>x.id===item.id);

if(b){

b.qty -= item.qty;

}

sales.push({

id:item.id,

ref:item.ref,

name:item.name,

qty:item.qty,

sellPrice:item.sell,

profit:
(item.sell-item.buy)*item.qty,

time:Date.now(),

command:commandNumber

});

});

commandNumber++;

localStorage.setItem(
"commandNumber",
commandNumber
);

currentCommandData=[];

save();

render();

updateCommandUI();

}

/* EDIT SALE */

function editSalePrice(index){

let s = sales[index];

if(!s) return;

let b = batches.find(x => x.id === s.id);

if(!b) return;

let oldQty = s.qty;

let newQty = +prompt("عدل الكمية", s.qty);

if(isNaN(newQty) || newQty <= 0)
return;

let newPrice =
+prompt("عدل سعر البيع", s.sellPrice);

if(isNaN(newPrice) || newPrice <= 0)
return;

b.qty += oldQty;

if(b.qty < newQty){

alert("المخزون غير كاف");

b.qty -= oldQty;

return;

}

b.qty -= newQty;

s.qty = newQty;

s.sellPrice = newPrice;

s.profit =
(newPrice - b.buy) * newQty;

save();

render();

}

/* DELETE SALE */

function deleteSale(index){

if(!confirm("هل تريد حذف العملية؟"))
return;

let s = sales[index];

if(!s) return;

let b = batches.find(x => x.id === s.id);

if(b){

b.qty += s.qty;

}

sales.splice(index,1);

save();

render();

}

/* PRODUCTS SEARCH */

function renderProducts(){

let search =
productSearch.value
.toLowerCase()
.trim();

let filtered = batches.filter(b=>

(b.name && b.name.toLowerCase().includes(search))

||

(b.ref && b.ref.toLowerCase().includes(search))

);

productTable.innerHTML="";

filtered.forEach(b=>{

productTable.innerHTML += `

<tr>

<td>${b.ref || ""}</td>

<td>${b.name}</td>

<td>${b.qty}</td>

<td>${b.buy}</td>

<td>${b.sell}</td>

<td>

<span class="edit"
onclick="editProduct(${b.id})">

تعديل

</span>

</td>

<td>

<span class="del"
onclick="deleteProduct(${b.id})">

حذف

</span>

</td>

</tr>

`;

});

}

/* SALES SEARCH */

function renderSales(){

let search =
saleSearch.value.toLowerCase();

let filtered = batches.filter(b=>

(b.name && b.name.toLowerCase().includes(search))

||

(b.ref && b.ref.toLowerCase().includes(search))

);

saleStock.innerHTML = filtered.map(b=>`

<option value="${b.id}">

${b.ref || "----"}
|
${b.name}
|
شراء: ${b.buy}
|
بيع: ${b.sell}
|
stock: ${b.qty}

</option>

`).join('');

}

/* PROFITS */

function renderProfits(){

let now = new Date();

let daily = sales.filter(s=>{

let d = new Date(s.time);

return d.toDateString() ===
now.toDateString();

}).reduce((a,b)=>a+b.profit,0);

let monthly = sales.filter(s=>{

let d = new Date(s.time);

return d.getMonth() === now.getMonth()
&&
d.getFullYear() === now.getFullYear();

}).reduce((a,b)=>a+b.profit,0);

let yearly = sales.filter(s=>{

let d = new Date(s.time);

return d.getFullYear() ===
now.getFullYear();

}).reduce((a,b)=>a+b.profit,0);

dailyProfit.innerHTML =
`💰 ${daily.toFixed(2)} DA`;

monthlyProfit.innerHTML =
`💰 ${monthly.toFixed(2)} DA`;

yearlyProfit.innerHTML =
`💰 ${yearly.toFixed(2)} DA`;

}

/* RANGE PROFITS */

function calcProfitRange(){

let from = new Date(
fromDate.value || "2000-01-01"
);

let to = new Date(
toDate.value || "2100-01-01"
);

to.setHours(23,59,59,999);

let total = sales.filter(s=>{

let d = new Date(s.time);

return d >= from && d <= to;

}).reduce((a,b)=>a+b.profit,0);

rangeProfit.innerHTML = `

من: ${fromDate.value}<br>

إلى: ${toDate.value}<br><br>

الأرباح:
${total.toFixed(2)} DA

`;

}

/* EXPORT DATA */

function exportData(){

let data = {

batches,

sales,

commandNumber

};

let blob = new Blob(

[JSON.stringify(data,null,2)],

{type:"application/json"}

);

let a = document.createElement("a");

a.href = URL.createObjectURL(blob);

a.download = "backup.json";

a.click();

}

/* RENDER */

function render(){

renderProducts();

/* STOCK */

stockTable.innerHTML="";

batches.forEach(b=>{

let capital = b.buy * b.qty;

let profit =
(b.sell - b.buy) * b.qty;

stockTable.innerHTML += `

<tr>

<td>
${b.ref || ""}
-
${b.name}
</td>

<td>${b.qty}</td>

<td>${capital.toFixed(2)}</td>

<td>${profit.toFixed(2)}</td>

<td>

<span class="del"
onclick="deleteProduct(${b.id})">

حذف

</span>

</td>

</tr>

`;

});

/* LOW STOCK */

lowTable.innerHTML="";

batches.forEach(b=>{

if(b.qty <= 10){

let status =
b.qty <= 5 ? "خطر" : "ناقص";

let color =
b.qty <= 5 ? "red" : "orange";

lowTable.innerHTML += `

<tr
style="
color:${color};
font-weight:bold;
">

<td>
${b.ref || ""}
-
${b.name}
</td>

<td>${b.qty}</td>

<td>${status}</td>

</tr>

`;

}

});

/* TOTALS */

let capital = batches.reduce(
(a,b)=>a+(b.buy*b.qty),
0
);

let profit = batches.reduce(
(a,b)=>a+((b.sell-b.buy)*b.qty),
0
);

totals.innerHTML = `

رأس المال:
${capital.toFixed(2)} DA
<br>

الأرباح:
${profit.toFixed(2)} DA
<br>

المجموع:
${(capital+profit).toFixed(2)} DA

`;

/* SALES LOG */

salesLog.innerHTML =
sales.slice().reverse().map((s,reverseIndex)=>{

let index =
sales.length - 1 - reverseIndex;

let date = new Date(s.time);

return `

<div class="saleItem">

<div>

Commande #${s.command || 1}
|

${date.toLocaleDateString()}
|

${date.toLocaleTimeString()}
|

${s.ref || ""}
|

${s.name}
|

x${s.qty}
|

${s.sellPrice} DA
|

${s.profit} DA

</div>

<div>

<span
onclick="editSalePrice(${index})"

style="
background:#3b82f6;
color:white;
padding:4px 8px;
border-radius:6px;
cursor:pointer;
font-size:12px;
margin-right:5px;
">

تعديل

</span>

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

</div>

`;

}).join('');

renderSales();

renderProfits();

updateCommandUI();

}

render();

</script>

</body>
</html>

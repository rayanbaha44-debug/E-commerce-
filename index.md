<!DOCTYPE html>
<html lang="ar" dir="rtl">

<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>POS SYSTEM PRO</title>

<style>

/* ================= UI SAME ================= */

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
display:block;
overflow-x:auto;
white-space:nowrap;
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

<div class="card" onclick="openPage('products')">المنتجات📦</div>
<div class="card" onclick="openPage('sales')">البيع🛒</div>
<div class="card" onclick="openPage('stock')">المخزون🏬</div>
<div class="card" onclick="openPage('low')">الناقص⚠️</div>
<div class="card" onclick="openPage('profits')">الأرباح💰</div>
<div class="card" onclick="exportData()">تصدير البيانات 💾</div>

</div>

<!-- PRODUCTS -->
<div id="products" class="page">

<div class="header">
<button class="back" onclick="back()">رجوع↩️</button>
<h2>📦المنتجات</h2>
</div>

<input id="pRef" placeholder="الرفيرونس">
<input id="pName" placeholder="اسم المنتج">
<input id="pBuy" type="number" step="0.01" placeholder="سعر الشراء (مثال: 221.77)">
<input id="pSell" type="number" step="0.01" placeholder="سعر البيع (مثال: 250.50)">
<input id="pQty" type="number" step="0.01" placeholder="الكمية">

<button onclick="addProduct()">إضافة</button>

<input type="file" id="importFile" hidden onchange="importData(event)">
<button onclick="document.getElementById('importFile').click()" style="background:#3b82f6; color:white; margin-top:5px;">استيراد البيانات 📥</button>

<input id="productSearch" placeholder="ابحث باسم المنتج أو الرفيرونس..." oninput="renderProducts()">

<table>
<thead>
<tr>
<th>الرفيرونس</th><th>الاسم</th><th>الكمية</th><th>شراء</th><th>بيع</th><th>تعديل</th><th>حذف</th>
</tr>
</thead>
<tbody id="productTable"></tbody>
</table>

</div>

<!-- SALES -->
<div id="sales" class="page">

<div class="header">
<button class="back" onclick="back()">رجوع↩️</button>
<h2>🛒البيع</h2>
</div>

<div class="box">
<h3 id="cmdNumber">Commande #1</h3>
</div>

<input id="saleSearch" placeholder="بحث باسم المنتج لتصفية القائمة..." oninput="renderSalesOptions()">

<select id="saleStock"></select>
<input id="saleQty" type="number" step="0.01" value="1">

<button onclick="addToCommand()">إضافة للكوموند</button>

<div class="box" style="margin-top:15px;">
<h3>منتجات الكوموند</h3>
<div id="currentCommand"></div>
<h3 id="commandTotal" style="margin-top:10px;">المجموع: 0 DA</h3>

<button onclick="confirmCommand()" style="width:100%; margin-top:10px;">تأكيد الطلب OK</button>
</div>

<h3>سجل مبيعات اليوم الحالي</h3>
<div id="salesLog"></div>

</div>

<!-- STOCK -->
<div id="stock" class="page">
<div class="header">
<button class="back" onclick="back()">رجوع↩️</button>
<h2>🏬المخزون</h2>
</div>

<table>
<thead>
<tr><th>المنتج</th><th>الكمية</th><th>رأس المال</th><th>القيمة المتوقعة</th><th>حذف</th></tr>
</thead>
<tbody id="stockTable"></tbody>
</table>

<div id="totals" class="box" style="margin-top:15px;"></div>
</div>

<!-- LOW -->
<div id="low" class="page">
<div class="header">
<button class="back" onclick="back()">رجوع↩️</button>
<h2>⚠️الناقص</h2>
</div>
<table>
<thead><tr><th>المنتج</th><th>الكمية المتبقية</th><th>الحالة</th></tr></thead>
<tbody id="lowTable"></tbody>
</table>
</div>

<!-- PROFITS -->
<div id="profits" class="page">
<div class="header">
<button class="back" onclick="back()">رجوع↩️</button>
<h2>💰الأرباح</h2>
</div>

<div class="box">
<h3>أرباح اليوم</h3><div id="dailyProfit">0 DA</div>
</div>

<div class="box">
<h3>أرباح الشهر</h3><div id="monthlyProfit">0 DA</div>
</div>

<div class="box">
<h3>أرباح السنة</h3><div id="yearlyProfit">0 DA</div>
</div>

</div>

<script>

/* ================= DATA ================= */

let batches = JSON.parse(localStorage.getItem("batches") || "[]");
let sales = JSON.parse(localStorage.getItem("sales") || "[]");
let commandNumber = Number(localStorage.getItem("commandNumber") || 1);
let currentCommandData = [];

/* ================= SAVE ================= */

function save(){
localStorage.setItem("batches", JSON.stringify(batches));
localStorage.setItem("sales", JSON.stringify(sales));
localStorage.setItem("commandNumber", commandNumber);
}

/* ================= NAV ================= */

function openPage(id){
document.getElementById("dashboard").style.display="none";
document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
document.getElementById(id).classList.add("active");
if(id === 'sales') renderSalesOptions();
}

function back(){
document.getElementById("dashboard").style.display="grid";
document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
}

/* ================= PRODUCT ================= */

function addProduct(){
let ref = document.getElementById('pRef').value.trim();
let name = document.getElementById('pName').value.trim();
let buy = document.getElementById('pBuy').value;
let sell = document.getElementById('pSell').value;
let qty = document.getElementById('pQty').value;

if(!ref || !name || !buy || !sell || !qty){
alert("أكمل الحقول");
return;
}

batches.push({
id: Date.now(),
ref: ref,
name: name,
buy: +buy,
sell: +sell,
qty: +qty
});

document.getElementById('pRef').value = '';
document.getElementById('pName').value = '';
document.getElementById('pBuy').value = '';
document.getElementById('pSell').value = '';
document.getElementById('pQty').value = '';

save();
render();
}

function deleteProduct(id){
if(!confirm("هل أنت متأكد من حذف هذا المنتج نهائياً؟")) return;
batches = batches.filter(x => x.id !== id);
save();
render();
}

function editProduct(id){
let b = batches.find(x => x.id === id);
if(!b) return;

let newName = prompt("تعديل اسم المنتج:", b.name);
if(newName === null) return; 
let newQty = prompt("تعديل الكمية:", b.qty);
if(newQty === null) return;
let newBuy = prompt("تعديل سعر الشراء:", b.buy);
if(newBuy === null) return;
let newSell = prompt("تعديل سعر البيع:", b.sell);
if(newSell === null) return;

b.name = newName.trim();
b.qty = +newQty;
b.buy = +newBuy;
b.sell = +newSell;

save();
render();
}

/* ================= COMMAND ================= */

function renderSalesOptions(){
let searchVal = document.getElementById('saleSearch').value.toLowerCase();
let filtered = batches.filter(b => b.name.toLowerCase().includes(searchVal) || b.ref.toLowerCase().includes(searchVal));

let saleStock = document.getElementById('saleStock');
saleStock.innerHTML = filtered.map(b => `<option value="${b.id}">${b.name} (${b.qty} قطعة) - ${b.sell.toFixed(2)} DA</option>`).join("");
}

function addToCommand(){
let saleStock = document.getElementById('saleStock');
let saleQty = document.getElementById('saleQty');
if(!saleStock.value) return;

let id = Number(saleStock.value);
let qty = +saleQty.value;

let b = batches.find(x=>x.id===id);
if(!b || qty<=0) return;

if(b.qty < qty){
alert("المخزون غير كافي");
return;
}

let ex = currentCommandData.find(x=>x.id===id);

if(ex){
if(b.qty < ex.qty + qty){
alert("تجاوز المخزون المتوفر");
return;
}
ex.qty += qty;
}else{
currentCommandData.push({...b, qty});
}

updateCommandUI();
}

/* ================= CONFIRM ================= */

function confirmCommand(){
if(currentCommandData.length===0){
alert("الكوموند فارغ!");
return;
}

currentCommandData.forEach(item=>{
let b = batches.find(x=>x.id===item.id);
if(!b) return;

b.qty = Math.max(0, (b.qty||0) - (item.qty||0));

sales.push({
id:item.id,
ref:item.ref,
name:item.name,
qty:item.qty,
buy:item.buy,
sell:item.sell,
profit:(item.sell-item.buy)*item.qty,
time:Date.now(),
command:commandNumber
});
});

commandNumber++;
currentCommandData=[];
save();
render();
renderSalesOptions();
}

function deleteSale(index){
if(!confirm("إلغاء هذه المبيعة وإرجاع السلعة للمخزون؟")) return;

let s = sales[index];
if(!s) return;

let b = batches.find(x=>x.id===s.id);
if(b){
b.qty += s.qty;
}

sales.splice(index,1);
save();
render();
}

/* ================= CART ================= */

function updateCommandUI(){
let currentCommand = document.getElementById('currentCommand');
let commandTotal = document.getElementById('commandTotal');
let cmdNumber = document.getElementById('cmdNumber');
let total=0;

currentCommand.innerHTML = currentCommandData.map((i,idx)=>{
total += i.sell*i.qty;
return `
<div style="display:flex; justify-content:space-between; margin:5px 0; background:#f3f4f6; padding:5px; border-radius:5px;">
<span>${i.name} x${i.qty}</span>
<span>${(i.sell*i.qty).toFixed(2)} DA</span>
<span onclick="removeFromCommand(${idx})" style="cursor:pointer;">❌</span>
</div>`;
}).join("");

commandTotal.innerHTML = "المجموع: " + total.toFixed(2) + " DA";
cmdNumber.innerHTML = "Commande #" + commandNumber;
}

function removeFromCommand(i){
currentCommandData.splice(i,1);
updateCommandUI();
}

/* ================= RENDER ALL ================= */

function renderProducts(){
let searchVal = document.getElementById('productSearch').value.toLowerCase();
let filtered = batches.filter(b => b.name.toLowerCase().includes(searchVal) || b.ref.toLowerCase().includes(searchVal));

document.getElementById('productTable').innerHTML = filtered.map(b=>`
<tr>
<td>${b.ref}</td>
<td>${b.name}</td>
<td>${b.qty}</td>
<td>${b.buy.toFixed(2)}</td>
<td>${b.sell.toFixed(2)}</td>
<td><button class="edit" onclick="editProduct(${b.id})">تعديل</button></td>
<td><button class="del" onclick="deleteProduct(${b.id})">حذف</button></td>
</tr>
`).join("");
}

function render(){
renderProducts();

let totalCapital = 0;
let totalValue = 0;

document.getElementById('stockTable').innerHTML = batches.map(b=>{
let capital = b.buy * b.qty;
let expectedProfit = (b.sell - b.buy) * b.qty;
totalCapital += capital;
totalValue += (b.sell * b.qty);

return `
<tr>
<td>${b.name}</td>
<td>${b.qty}</td>
<td>${capital.toFixed(2)} DA</td>
<td>${expectedProfit.toFixed(2)} DA</td>
<td><button class="del" onclick="deleteProduct(${b.id})">حذف</button></td>
</tr>`;
}).join("");

document.getElementById('totals').innerHTML = `
<p><strong>إجمالي رأس المال الحالي:</strong> ${totalCapital.toFixed(2)} DA</p>
<p><strong>القيمة الإجمالية للسلع عند البيع:</strong> ${totalValue.toFixed(2)} DA</p>
`;

document.getElementById('salesLog').innerHTML = [...sales].reverse().map((s,i)=>{
let idx = sales.length-1-i;
return `
<div class="saleItem">
<span><strong>#${s.command}</strong> - ${s.name} x${s.qty}</span>
<span>الربح: ${s.profit.toFixed(2)} DA</span>
<span onclick="deleteSale(${idx})" style="cursor:pointer;">❌</span>
</div>`;
}).join("");

let now = new Date();
let startOfDay = new Date(now.getFullYear(), now.getMonth(), now.getDate()).getTime();
let startOfMonth = new Date(now.getFullYear(), now.getMonth(), 1).getTime();
let startOfYear = new Date(now.getFullYear(), 0, 1).getTime();

let dProfit = 0, mProfit = 0, yProfit = 0;

sales.forEach(s => {
let t = s.time || Date.now();
if(t >= startOfDay) dProfit += (s.profit || 0);
if(t >= startOfMonth) mProfit += (s.profit || 0);
if(t >= startOfYear) yProfit += (s.profit || 0);
});

document.getElementById('dailyProfit').innerHTML = dProfit.toFixed(2) + " DA";
document.getElementById('monthlyProfit').innerHTML = mProfit.toFixed(2) + " DA";
document.getElementById('yearlyProfit').innerHTML = yProfit.toFixed(2) + " DA";

let lowItems = batches.filter(b => b.qty <= 5);
document.getElementById('lowTable').innerHTML = lowItems.map(b => `
<tr style="background: ${b.qty === 0 ? '#fee2e2' : '#fef3c7'}">
<td>${b.name}</td>
<td>${b.qty}</td>
<td><span style="color:${b.qty === 0 ? 'red':'orange'}; font-weight:bold;">${b.qty === 0 ? 'منتهي ❌' : 'شبه منتهي ⚠️'}</span></td>
</tr>
`).join("");
if(lowItems.length === 0){
document.getElementById('lowTable').innerHTML = `<tr><td colspan="3">لا توجد نواقص بحمد الله 🎉</td></tr>`;
}
}

/* ================= EXPORT & IMPORT ================= */

function exportData(){
let dataStr = JSON.stringify({ batches, sales, commandNumber });
let dataUri = 'data:application/json;charset=utf-8,'+ encodeURIComponent(dataStr);

let exportFileDefaultName = 'pos_backup_' + new Date().toISOString().slice(0,10) + '.json';

let linkElement = document.createElement('a');
linkElement.setAttribute('href', dataUri);
linkElement.setAttribute('download', exportFileDefaultName);
linkElement.click();
}

function importData(event) {
let reader = new FileReader();
reader.onload = function(e){
try {
let parsed = JSON.parse(e.target.result);
if(parsed.batches || parsed.sales){
batches = parsed.batches || [];
sales = parsed.sales || [];
commandNumber = parsed.commandNumber || 1;
save();
render();
alert("تم استيراد البيانات بنجاح!");
} else {
alert("ملف غير صالح.");
}
} catch(err) {
alert("حدث خطأ أثناء قراءة الملف.");
}
};
reader.readAsText(event.target.files[0]);
}

/* INITIAL RENDER */
render();

</script>

</body>
</html>

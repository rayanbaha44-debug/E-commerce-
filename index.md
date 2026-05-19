<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Odoo Mini ERP Pro</title>

<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;600;700;800&display=swap" rel="stylesheet">

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:'Cairo',sans-serif;}

body{
    background:#0a0f1c;
    color:white;
    display:flex;
    min-height:100vh;
}

/* SIDEBAR */
.sidebar{
    width:240px;
    background:#111827;
    padding:20px;
}

.logo{
    font-size:22px;
    font-weight:800;
    color:#38bdf8;
    margin-bottom:15px;
}

.menu button{
    width:100%;
    padding:12px;
    margin-bottom:10px;
    border:none;
    border-radius:10px;
    background:#1f2937;
    color:white;
    cursor:pointer;
    font-weight:700;
}

.menu button:hover{
    background:#38bdf8;
    color:black;
}

/* MAIN */
.main{
    flex:1;
    padding:20px;
}

.section{display:none;}
.active{display:block;}

/* DASH CARDS */
.cards{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(180px,1fr));
    gap:15px;
    margin-bottom:20px;
}

.card{
    background:#111827;
    padding:15px;
    border-radius:12px;
    border:1px solid #1f2937;
}

.card span{
    font-size:20px;
    font-weight:800;
    color:#38bdf8;
}

/* INPUT */
input{
    padding:10px;
    margin:5px;
    border:none;
    border-radius:8px;
    background:#111827;
    color:white;
}

button.add{
    padding:10px 12px;
    border:none;
    border-radius:8px;
    background:#38bdf8;
    cursor:pointer;
    font-weight:bold;
}

/* TABLE */
table{
    width:100%;
    border-collapse:collapse;
    background:#111827;
    margin-top:10px;
}

th,td{
    padding:10px;
    text-align:center;
    border-bottom:1px solid #1f2937;
}

th{
    background:#0f172a;
    color:#38bdf8;
}

.del{
    background:red;
    color:white;
    border:none;
    padding:5px 8px;
    border-radius:6px;
    cursor:pointer;
}

.profit{color:lime;font-weight:bold;}
.loss{color:red;font-weight:bold;}

canvas{
    background:#0f172a;
    border-radius:12px;
    padding:10px;
}
</style>
</head>

<body>

<!-- SIDEBAR -->
<div class="sidebar">

<div class="logo">ERP PRO</div>

<div class="menu">
<button onclick="show('dash')">📊 لوحة التحكم</button>
<button onclick="show('stock')">📦 المخزون</button>
<button onclick="show('audit')">📋 الجرد</button>
<button onclick="show('customers')">👥 الزبائن</button>
<button onclick="show('sales')">💰 المبيعات</button>
<button onclick="show('charts')">📈 الرسوم البيانية</button>
</div>

</div>

<!-- MAIN -->
<div class="main">

<!-- DASH -->
<div id="dash" class="section active">

<div class="cards">
<div class="card">📦 المنتجات<br><span id="tStock">0</span></div>
<div class="card">👥 الزبائن<br><span id="tCust">0</span></div>
<div class="card">💰 الربح<br><span id="tProfit">0 DA</span></div>
<div class="card">📦 قيمة الصطوك<br><span id="tValue">0 DA</span></div>
<div class="card">⚠️ نقص<br><span id="tLow">0</span></div>
</div>

</div>

<!-- STOCK -->
<div id="stock" class="section">

<h2>📦 المخزون</h2>

<input id="name" placeholder="اسم المنتج">
<input id="buy" placeholder="سعر الشراء">
<input id="sell" placeholder="سعر البيع">
<input id="qty" placeholder="الكمية">

<button class="add" onclick="addStock()">إضافة</button>

<table>
<thead>
<tr>
<th>المنتج</th>
<th>شراء</th>
<th>بيع</th>
<th>كمية</th>
<th>الربح</th>
<th></th>
</tr>
</thead>

<tbody id="stockT"></tbody>
</table>

</div>

<!-- AUDIT -->
<div id="audit" class="section">

<h2>📋 الجرد الاحترافي</h2>

<button class="add" onclick="runAudit()">🔄 تشغيل الجرد</button>

<table>
<thead>
<tr>
<th>المنتج</th>
<th>الكمية</th>
<th>قيمة المخزون</th>
<th>الحالة</th>
</tr>
</thead>

<tbody id="auditT"></tbody>
</table>

</div>

<!-- CUSTOMERS -->
<div id="customers" class="section">

<h2>👥 الزبائن</h2>

<input id="cname" placeholder="اسم الزبون">
<input id="phone" placeholder="الهاتف">

<button class="add" onclick="addCustomer()">إضافة</button>

<table>
<tbody id="custT"></tbody>
</table>

</div>

<!-- SALES -->
<div id="sales" class="section">

<h2>💰 المبيعات</h2>

<input id="sname" placeholder="المنتج">
<input id="amount" placeholder="المبلغ">

<button class="add" onclick="addSale()">إضافة</button>

<table>
<tbody id="salesT"></tbody>
</table>

</div>

<!-- CHARTS -->
<div id="charts" class="section">

<h2>📈 الرسوم البيانية</h2>

<div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(300px,1fr));gap:15px;">

<canvas id="stockChart"></canvas>
<canvas id="profitChart"></canvas>
<canvas id="salesChart"></canvas>

</div>

</div>

</div>

<script>

let stock = JSON.parse(localStorage.getItem("erp_stock")) || [];
let customers = JSON.parse(localStorage.getItem("erp_cust")) || [];
let sales = JSON.parse(localStorage.getItem("erp_sales")) || [];

let stockChart, profitChart, salesChart;

function save(){
localStorage.setItem("erp_stock",JSON.stringify(stock));
localStorage.setItem("erp_cust",JSON.stringify(customers));
localStorage.setItem("erp_sales",JSON.stringify(sales));
}

/* NAV */
function show(id){
document.querySelectorAll('.section').forEach(s=>s.classList.remove('active'));
document.getElementById(id).classList.add('active');

if(id==="charts") drawCharts();
}

/* STOCK */
function addStock(){
stock.push({
name:name.value,
buy:+buy.value,
sell:+sell.value,
qty:+qty.value
});
save(); render();
}

/* CUSTOMERS */
function addCustomer(){
customers.push({name:cname.value,phone:phone.value});
save(); render();
}

/* SALES */
function addSale(){
sales.push({name:sname.value,amount:+amount.value});
save(); render();
}

/* DELETE */
function delStock(i){stock.splice(i,1);save();render();}

/* AUDIT */
function runAudit(){

let t="";

stock.forEach(p=>{

let value=p.buy*p.qty;
let status=p.qty<=5?"⚠️ ناقص":"✔ جيد";

t+=`
<tr>
<td>${p.name}</td>
<td>${p.qty}</td>
<td>${value} DA</td>
<td>${status}</td>
</tr>
`;

});

auditT.innerHTML=t;
}

/* CHARTS */
function drawCharts(){

let names = stock.map(p=>p.name);
let qty = stock.map(p=>p.qty);
let profit = stock.map(p=>(p.sell-p.buy)*p.qty);
let cost = stock.map(p=>p.buy*p.qty);

/* STOCK PIE */
if(stockChart) stockChart.destroy();
stockChart = new Chart(document.getElementById("stockChart"),{
type:"pie",
data:{
labels:names,
datasets:[{data:qty}]
}
});

/* PROFIT LINE */
if(profitChart) profitChart.destroy();
profitChart = new Chart(document.getElementById("profitChart"),{
type:"line",
data:{
labels:names,
datasets:[
{label:"الربح",data:profit,borderColor:"green"},
{label:"رأس المال",data:cost,borderColor:"red"}
]
}
});

/* SALES BAR */
if(salesChart) salesChart.destroy();
salesChart = new Chart(document.getElementById("salesChart"),{
type:"bar",
data:{
labels:sales.map(s=>s.name),
datasets:[{label:"المبيعات",data:sales.map(s=>s.amount)}]
}
});

}

/* RENDER */
function render(){

stockT.innerHTML=stock.map((p,i)=>{
let pr=(p.sell-p.buy)*p.qty;
return`
<tr>
<td>${p.name}</td>
<td>${p.buy}</td>
<td>${p.sell}</td>
<td>${p.qty}</td>
<td class="${pr>=0?'profit':'loss'}">${pr}</td>
<td><button class="del" onclick="delStock(${i})">X</button></td>
</tr>`;
}).join("");

custT.innerHTML=customers.map((c,i)=>
`<tr><td>${c.name}</td><td>${c.phone}</td></tr>`
).join("");

salesT.innerHTML=sales.map((s,i)=>
`<tr><td>${s.name}</td><td>${s.amount}</td></tr>`
).join("");

tStock.innerText=stock.length;
tCust.innerText=customers.length;

let totalProfit = stock.reduce((a,p)=>
a+(p.sell-p.buy)*p.qty,0);

tProfit.innerText=totalProfit+" DA";

let value = stock.reduce((a,p)=>
a+p.buy*p.qty,0);

tValue.innerText=value+" DA";

tLow.innerText=stock.filter(p=>p.qty<=5).length;

}

render();

</script>

</body>
</html>

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

/* 🔥 NEW PANEL */
#statsPanel{
margin-top:15px;
background:#f3f4f6;
padding:10px;
border-radius:10px;
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

<!-- SALES PAGE -->
<div id="sales" class="page active">

<div class="header">
<button class="back" onclick="back()">⬅ رجوع</button>
<h2>🧾 البيع</h2>
</div>

<input id="saleSearch" placeholder="ابحث عن المنتج..." oninput="renderSales()">

<select id="saleStock"></select>

<input id="saleQty" type="number" value="1">

<button onclick="sell()">بيع</button>

<!-- 🔥 SALES LOG -->
<div id="salesLog"></div>

<!-- 🔥 NEW STATS -->
<div id="statsPanel">

<h3>📊 الأرباح حسب التاريخ</h3>

<input type="date" id="fromDate">
<input type="date" id="toDate">

<button onclick="calcStats()">حساب</button>

<div id="statsResult" style="margin-top:10px;"></div>

</div>

</div>

<script>

let batches = JSON.parse(localStorage.getItem("batches")||"[]");
let sales = JSON.parse(localStorage.getItem("sales")||"[]");

if(!Array.isArray(batches)) batches=[];
if(!Array.isArray(sales)) sales=[];

/* SELL */
function sell(){

let id = +saleStock.value;
let qty = +saleQty.value;

let b = batches.find(x=>x.id===id);
if(!b || b.qty<qty) return;

b.qty -= qty;

sales.push({
name:b.name,
qty,
sellPrice:b.sell,
profit:(b.sell-b.buy)*qty,
time: new Date().toISOString()
});

save();
render();
}

/* CALCULATE STATS */
function calcStats(){

let from = new Date(fromDate.value || "2000-01-01");
let to = new Date(toDate.value || "2100-01-01");

let filtered = sales.filter(s=>{
let d = new Date(s.time);
return d >= from && d <= to;
});

let total = filtered.reduce((a,b)=>a+b.profit,0);

statsResult.innerHTML = `
💰 الربح بين التاريخين:<br>
📅 من: ${fromDate.value || "بداية"}<br>
📅 إلى: ${toDate.value || "الآن"}<br><br>
📈 المجموع: ${total.toFixed(2)} DA
`;
}

/* RENDER SALES LOG */
function render(){

salesLog.innerHTML = sales.slice().reverse().map(s=>
`<div style="padding:6px;border-bottom:1px solid #ddd">
⏰ ${new Date(s.time).toLocaleString()} | 📦 ${s.name} | x${s.qty} | 💵 ${s.sellPrice} | 💰 ${s.profit}
</div>`
).join('');
}

render();

</script>

</body>
</html>

<!DOCTYPE html>
<html lang="ar" dir="rtl">

<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>POS SYSTEM PREMIUM - نظام المبيعات الاحترافي</title>

<!-- استدعاء خط Cairo والأيقونات الاحترافية -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;600;700;800&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

<style>
/* ================= PREMIUM MODERN UI/UX ================= */
:root {
    --primary: #3b82f6;
    --primary-gradient: linear-gradient(135deg, #3b82f6 0%, #1d4ed8 100%);
    --success: #10b981;
    --success-gradient: linear-gradient(135deg, #10b981 0%, #047857 100%);
    --danger: #ef4444;
    --danger-gradient: linear-gradient(135deg, #ef4444 0%, #b91c1c 100%);
    --warning: #f59e0b;
    --background: #f1f5f9;
    --surface: #ffffff;
    --text-main: #1e293b;
    --text-muted: #64748b;
    --border: #e2e8f0;
    --radius-lg: 16px;
    --radius-md: 12px;
    --shadow-sm: 0 2px 4px 0 rgba(0,0,0,0.02);
    --shadow-md: 0 10px 15px -3px rgba(0,0,0,0.05), 0 4px 6px -4px rgba(0,0,0,0.05);
    --shadow-lg: 0 20px 25px -5px rgba(0,0,0,0.08), 0 8px 10px -6px rgba(0,0,0,0.08);
}

*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Cairo', sans-serif;
}

body{
    background: radial-gradient(at 50% 0%, #f8fafc 0%, #e2e8f0 100%);
    color: var(--text-main);
    min-height: 100vh; 
    padding: 40px 20px;
    display: flex;
    justify-content: center;
    align-items: flex-start;
}

/* لوحة التحكم الرئيسية (Dashboard Grid) */
#dashboard{
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 20px;
    width: 100%;
    max-width: 950px;
    margin: 20px auto;
}

.card{
    background: var(--surface);
    padding: 35px 25px;
    border-radius: var(--radius-lg);
    text-align: center;
    cursor: pointer;
    border: 1px solid rgba(255,255,255,0.7);
    font-weight: 700;
    font-size: 18px;
    color: var(--text-main);
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    box-shadow: var(--shadow-md);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 15px;
}

.card i {
    font-size: 32px;
    background: var(--primary-gradient);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    transition: transform 0.3s ease;
}

.card:hover{
    transform: translateY(-6px);
    box-shadow: var(--shadow-lg);
    border-color: var(--primary);
}

.card:hover i {
    transform: scale(1.15);
}

/* الصفحات والحاويات الرئيسية */
.page{
    display: none;
    width: 100%;
    max-width: 1000px;
    background: rgba(255, 255, 255, 0.95);
    backdrop-filter: blur(10px);
    padding: 35px;
    border-radius: 24px;
    box-shadow: var(--shadow-lg);
    border: 1px solid rgba(255,255,255,0.8);
    animation: slideUp 0.4s cubic-bezier(0.16, 1, 0.3, 1);
}

@keyframes slideUp {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
}

.page.active{
    display: block;
}

.header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 30px;
    padding-bottom: 20px;
    border-bottom: 2px solid var(--border);
}

.header h2 {
    font-size: 26px;
    font-weight: 800;
    color: var(--text-main);
    display: flex;
    align-items: center;
    gap: 10px;
}

/* الأزرار الفاخرة */
button{
    padding: 12px 26px;
    border: none;
    border-radius: var(--radius-md);
    cursor: pointer;
    background: var(--primary-gradient);
    color: white;
    font-weight: 700;
    font-size: 15px;
    box-shadow: 0 4px 10px rgba(59, 130, 246, 0.25);
    transition: all 0.2s ease;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
}

button:hover{
    opacity: 0.95;
    transform: translateY(-1px);
    box-shadow: 0 6px 14px rgba(59, 130, 246, 0.35);
}

button:active {
    transform: translateY(1px);
}

.back{
    background: #64748b;
    box-shadow: 0 4px 10px rgba(100, 116, 139, 0.2);
}
.back:hover{ background: #475569; box-shadow: 0 6px 14px rgba(100, 116, 139, 0.3); }

/* المدخلات والقوائم المنسدلة النظيفة */
input, select{
    width: 100%;
    padding: 14px 18px;
    margin: 10px 0;
    border-radius: var(--radius-md);
    border: 1px solid var(--border);
    background: #f8fafc;
    color: var(--text-main);
    font-size: 15px;
    font-weight: 600;
    transition: all 0.25s ease;
}

input:focus, select:focus{
    outline: none;
    border-color: var(--primary);
    background: white;
    box-shadow: 0 0 0 4px rgba(59, 130, 246, 0.15);
}

/* الجداول المنظمة والحديثة */
table{
    width: 100%;
    margin-top: 25px;
    border-collapse: separate;
    border-spacing: 0;
    border-radius: var(--radius-md);
    overflow: hidden;
    border: 1px solid var(--border);
    box-shadow: var(--shadow-sm);
}

th, td{
    padding: 18px;
    text-align: center;
    border-bottom: 1px solid var(--border);
    font-size: 15px;
}

th {
    background-color: #f8fafc;
    color: var(--text-muted);
    font-weight: 700;
    font-size: 14px;
    text-transform: uppercase;
}

tr:hover td {
    background-color: #f8fafc;
}

tr:last-child td {
    border-bottom: none;
}

.del{
    background: var(--danger-gradient);
    box-shadow: 0 4px 10px rgba(239, 68, 68, 0.2);
}
.del:hover { box-shadow: 0 6px 14px rgba(239, 68, 68, 0.35); }

.edit{
    background: #f1f5f9;
    color: var(--text-main);
    border: 1px solid var(--border);
    box-shadow: none;
}
.edit:hover{ background: var(--border); }

/* الصناديق الفرعية */
.box{
    background: #f8fafc;
    padding: 24px;
    border-radius: var(--radius-lg);
    margin-bottom: 20px;
    border: 1px solid var(--border);
}

.flex-inputs {
    display: flex;
    gap: 14px;
    align-items: center;
}

#salesLog{
    margin-top: 15px;
    max-height: 280px;
    overflow-y: auto;
    padding-right: 5px;
}

.saleItem{
    padding: 14px 20px;
    background: var(--surface);
    border-radius: var(--radius-md);
    margin-bottom: 10px;
    border: 1px solid var(--border);
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 15px;
    box-shadow: var(--shadow-sm);
}

.badge-qty {
    background: #fef3c7;
    color: #d97706;
    padding: 5px 10px;
    border-radius: 8px;
    font-weight: 700;
    font-size: 13px;
}

/* كروت عرض الأرباح الكبيرة */
.profit-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    gap: 16px;
    margin-top: 20px;
}

.profit-card {
    background: var(--surface);
    padding: 25px;
    border-radius: var(--radius-lg);
    border: 1px solid var(--border);
    border-right: 5px solid var(--primary);
    box-shadow: var(--shadow-md);
}

.profit-card.success { border-right-color: var(--success); }
.profit-card.dark { border-right-color: var(--text-main); }

.profit-card p {
    color: var(--text-muted);
    font-size: 14px;
    font-weight: 700;
    margin-bottom: 5px;
}

.profit-card .amount {
    font-size: 26px;
    font-weight: 800;
}
</style>
</head>

<body>

<!-- DASHBOARD -->
<div id="dashboard">
    <div class="card" onclick="openPage('products')"><i class="fa-solid fa-box-open"></i> إدارة المنتجات</div>
    <div class="card" onclick="openPage('sales')"><i class="fa-solid fa-cash-register"></i> واجهة البيع السريعة</div>
    <div class="card" onclick="openPage('stock')"><i class="fa-solid fa-warehouse"></i> جرد المخزون الكلي</div>
    <div class="card" onclick="openPage('low')"><i class="fa-solid fa-triangle-exclamation" style="background:var(--warning); -webkit-background-clip: text;"></i> السلع الناقصة</div>
    <div class="card" onclick="openPage('profits')"><i class="fa-solid fa-chart-line" style="background:var(--success-gradient); -webkit-background-clip: text;"></i> تقارير الأرباح</div>
    <div class="card" onclick="exportData()" style="background: #fafafa;"><i class="fa-solid fa-file-export" style="background:#64748b; -webkit-background-clip: text;"></i> تصدير نسخة احتياطية</div>
</div>

<!-- PRODUCTS -->
<div id="products" class="page">
    <div class="header">
        <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع</button>
        <h2><i class="fa-solid fa-box-open" style="color:var(--primary);"></i> إدارة المنتجات والمخزن</h2>
    </div>

    <div class="box">
        <input id="pRef" placeholder="الرقم المتسلسل / الباركود (Ref)">
        <input id="pName" placeholder="اسم المنتج بالكامل">
        <div class="flex-inputs">
            <input id="pBuy" type="number" step="0.01" placeholder="سعر الشراء (DA)">
            <input id="pSell" type="number" step="0.01" placeholder="سعر البيع (DA)">
            <input id="pQty" type="number" step="0.01" placeholder="الكمية الابتدائية">
        </div>
        <button onclick="addProduct()" style="width: 100%; margin-top: 12px; background: var(--success-gradient); box-shadow: 0 4px 10px rgba(16, 185, 129, 0.2);"><i class="fa-solid fa-plus"></i> إضافة المنتج للمخزن</button>
    </div>

    <input type="file" id="importFile" hidden onchange="importData(event)">
    <button onclick="document.getElementById('importFile').click()" style="width: 100%; margin-bottom: 20px; background:#475569;"><i class="fa-solid fa-file-import"></i> استيراد بيانات من ملف خارجي (.json)</button>

    <input id="productSearch" placeholder="🔍 ابحث هنا باسم المنتج أو الرمز لتصفية الجدول الموالي..." oninput="renderProducts()">

    <table>
        <thead>
            <tr>
                <th>الباركود</th><th>اسم المنتج</th><th>الكمية</th><th>الشراء</th><th>البيع</th><th>تعديل</th><th>حذف</th>
            </tr>
        </thead>
        <tbody id="productTable"></tbody>
    </table>
</div>

<!-- SALES -->
<div id="sales" class="page">
    <div class="header">
        <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع</button>
        <h2><i class="fa-solid fa-cash-register" style="color:var(--primary);"></i> واجهة البيع السريعة</h2>
    </div>

    <div class="box" style="border: 1px dashed var(--primary); background: #f0f7ff;">
        <h4 style="color: var(--primary); margin-bottom: 8px;"><i class="fa-solid fa-pen-to-square"></i> تعديل ومراجعة كوموند سابق</h4>
        <div class="flex-inputs">
            <input id="editCmdNumInput" type="number" placeholder="أدخل رقم الكوموند القديم للبحث عنه...">
            <button onclick="loadCommandForEdit()" style="white-space: nowrap;"><i class="fa-solid fa-magnifying-glass"></i> جلب وتعديل</button>
        </div>
    </div>

    <div class="box" style="background: var(--text-main); color: white; text-align: center; border: none; box-shadow: var(--shadow-md);">
        <h3 id="cmdNumber" style="font-weight: 800; letter-spacing: 1px; font-size: 22px;">Commande #1</h3>
    </div>

    <input id="saleSearch" placeholder="🔍 ابحث هنا عن المنتج المراد بيعه حالياً..." oninput="renderSalesOptions()">

    <select id="saleStock"></select>
    <input id="saleQty" type="number" step="1" value="1" placeholder="الكمية">

    <button onclick="addToCommand()" style="width: 100%; margin-bottom: 25px; height: 50px; font-size: 16px;"><i class="fa-solid fa-cart-plus"></i> إضافة إلى السلة الحالية</button>

    <div class="box" style="background: #fff; border: 1px solid var(--border); box-shadow: var(--shadow-md);">
        <h3 style="margin-bottom: 15px; padding-bottom: 8px; border-bottom: 2px solid var(--background); font-weight:700;"><i class="fa-solid fa-basket-shopping" style="color:var(--primary)"></i> سلة التسوق الحالية</h3>
        <div id="currentCommand"></div>
        <h3 id="commandTotal" style="margin-top:20px; color: var(--success); text-align: left; font-weight:800; font-size: 22px;">المجموع: 0.00 DA</h3>
        <button onclick="confirmCommand()" style="width:100%; margin-top:15px; background: var(--success-gradient); font-size: 18px; padding: 16px; box-shadow: 0 4px 12px rgba(16, 185, 129, 0.3);"><i class="fa-solid fa-circle-check"></i> تأكيد وحفظ الطلب (OK)</button>
    </div>

    <h3 style="margin-top: 25px; color: var(--text-muted); font-weight:700;"><i class="fa-solid fa-clock-rotate-left"></i> سجل عمليات اليوم السريعة</h3>
    <div id="salesLog"></div>
</div>

<!-- STOCK -->
<div id="stock" class="page">
    <div class="header">
        <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع</button>
        <h2><i class="fa-solid fa-warehouse" style="color:var(--primary);"></i> كشف وجرد المخزن الكلي</h2>
    </div>
    <table>
        <thead>
            <tr><th>اسم المنتج</th><th>القطع المتبقية</th><th>رأس المال المستثمر</th><th>الأرباح المتوقعة</th><th>إجراء</th></tr>
        </thead>
        <tbody id="stockTable"></tbody>
    </table>
    <div id="totals" class="box" style="margin-top:25px; line-height: 2.2; background: #fff; box-shadow: var(--shadow-md);"></div>
</div>

<!-- LOW -->
<div id="low" class="page">
    <div class="header">
        <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع</button>
        <h2><i class="fa-solid fa-triangle-exclamation" style="color:var(--warning);"></i> تنبيه السلع الناقصة والمستنفذة</h2>
    </div>
    <table>
        <thead><tr><th>اسم المنتج</th><th>الكمية الحالية</th><th>حالة السلعة بالمخزن</th></tr></thead>
        <tbody id="lowTable"></tbody>
    </table>
</div>

<!-- PROFITS -->
<div id="profits" class="page">
    <div class="header">
        <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع</button>
        <h2><i class="fa-solid fa-chart-line" style="color:var(--success);"></i> التقارير المالية والأرباح الصافية</h2>
    </div>

    <!-- ميزة البحث بين تاريخين المتقدمة -->
    <div class="box" style="background: #fff; border: 1px solid var(--border); box-shadow: var(--shadow-md);">
        <h4 style="margin-bottom: 12px; color: var(--text-main); font-weight:700;"><i class="fa-solid fa-calendar-days" style="color:var(--primary)"></i> فلترة الأرباح حسب فترة زمنية مخصصة</h4>
        <div class="flex-inputs" style="flex-wrap: wrap;">
            <div style="flex: 1; min-width: 160px;">
                <label style="font-size: 13px; font-weight:700; color: var(--text-muted); display: block; margin-bottom:4px;">من تاريخ:</label>
                <input type="date" id="profitFromDate">
            </div>
            <div style="flex: 1; min-width: 160px;">
                <label style="font-size: 13px; font-weight:700; color: var(--text-muted); display: block; margin-bottom:4px;">إلى تاريخ:</label>
                <input type="date" id="profitToDate">
            </div>
            <button onclick="filterProfitsByDate()" style="height: 50px; margin-top: 24px; background: var(--primary-gradient);"><i class="fa-solid fa-filter"></i> تطبيق الفلتر</button>
            <button onclick="resetProfitFilter()" style="height: 50px; margin-top: 24px; background: #64748b; box-shadow:none;"><i class="fa-solid fa-arrow-rotate-left"></i> إلغاء</button>
        </div>
        <div id="customPeriodResultBox" style="display:none; margin-top: 20px; padding: 16px; background: #f0fdf4; border-radius: var(--radius-md); border-right: 5px solid var(--success); animation: fadeIn 0.3s ease;">
            <p style="color: var(--success); font-weight:700; font-size: 14px;">أرباح الفترة المحددة أعلاه:</p>
            <div id="customPeriodProfit" style="font-size: 26px; font-weight: 800; color: #166534;">0.00 DA</div>
        </div>
    </div>

    <div class="profit-grid">
        <div class="profit-card success">
            <p>أرباح اليوم الحالي</p>
            <div id="dailyProfit" class="amount" style="color: var(--success);">0.00 DA</div>
        </div>
        <div class="profit-card">
            <p>أرباح الشهر الحالي</p>
            <div id="monthlyProfit" class="amount" style="color: var(--primary);">0.00 DA</div>
        </div>
        <div class="profit-card dark">
            <p>أرباح السنة الإجمالية</p>
            <div id="yearlyProfit" class="amount" style="color: var(--text-main);">0.00 DA</div>
        </div>
    </div>
</div>

<script>
/* ================= SYSTEM LOGIC ================= */
let batches = JSON.parse(localStorage.getItem("batches") || "[]");
let sales = JSON.parse(localStorage.getItem("sales") || "[]");

let commandNumber = Number(localStorage.getItem("commandNumber"));
if (!commandNumber || commandNumber <= 0) {
    calculateNextCommandNumber();
}

let currentCommandData = [];

function calculateNextCommandNumber() {
    if (sales.length > 0) {
        let maxExistingCmd = sales.reduce((max, s) => s.command > max ? s.command : max, 0);
        commandNumber = maxExistingCmd + 1;
    } else {
        commandNumber = 1;
    }
}

function save(){
    localStorage.setItem("batches", JSON.stringify(batches));
    localStorage.setItem("sales", JSON.stringify(sales));
    localStorage.setItem("commandNumber", commandNumber);
}

function openPage(id){
    document.getElementById("dashboard").style.display="none";
    document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
    document.getElementById(id).classList.add("active");
    if(id === 'sales') {
        document.getElementById('saleSearch').value = ''; 
        document.getElementById('editCmdNumInput').value = ''; 
        renderSalesOptions();
    }
    window.scrollTo(0, 0);
}

function back(){
    document.getElementById("dashboard").style.display="grid";
    document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
    window.scrollTo(0, 0);
}

function addProduct(){
    let ref = document.getElementById('pRef').value.trim();
    let name = document.getElementById('pName').value.trim();
    let buy = document.getElementById('pBuy').value;
    let sell = document.getElementById('pSell').value;
    let qty = document.getElementById('pQty').value;

    if(!ref || !name || !buy || !sell || !qty){
        alert("يرجى ملء جميع الخانات المتاحة");
        return;
    }

    batches.push({ id: Date.now(), ref, name, buy: +buy, sell: +sell, qty: +qty });
    document.getElementById('pRef').value = ''; document.getElementById('pName').value = '';
    document.getElementById('pBuy').value = ''; document.getElementById('pSell').value = '';
    document.getElementById('pQty').value = '';
    save(); render();
}

function deleteProduct(id){
    if(!confirm("هل أنت متأكد من حذف السلعة نهائياً؟")) return;
    batches = batches.filter(x => x.id !== id);
    save(); render();
}

function editProduct(id){
    let b = batches.find(x => x.id === id);
    if(!b) return;
    let newName = prompt("تعديل اسم المنتج:", b.name); if(newName === null) return; 
    let newQty = prompt("تعديل الكمية الحالية:", b.qty); if(newQty === null) return;
    let newBuy = prompt("تعديل سعر الشراء:", b.buy); if(newBuy === null) return;
    let newSell = prompt("تعديل سعر البيع الجديد:", b.sell); if(newSell === null) return;

    b.name = newName.trim(); b.qty = +newQty; b.buy = +newBuy; b.sell = +newSell;
    save(); render();
}

function renderSalesOptions(){
    let searchVal = document.getElementById('saleSearch').value.toLowerCase().trim();
    let filtered = batches.filter(b => b.name.toLowerCase().includes(searchVal) || b.ref.toLowerCase().includes(searchVal));
    let saleStock = document.getElementById('saleStock');
    saleStock.innerHTML = filtered.map(b => `<option value="${b.id}">[${b.ref}] ${b.name} - المتبقي: ${b.qty} - السعر: ${b.sell.toFixed(2)} DA</option>`).join("");
}

function addToCommand(){
    let saleStock = document.getElementById('saleStock');
    let saleQty = document.getElementById('saleQty');
    if(!saleStock.value) return;

    let id = Number(saleStock.value);
    let qty = +saleQty.value;
    let b = batches.find(x=>x.id===id);
    if(!b || qty<=0) return;

    if(b.qty < qty){ alert("المخزون المتوفر غير كافي لهذه العملية"); return; }
    let ex = currentCommandData.find(x=>x.id===id);

    if(ex){
        if(b.qty < ex.qty + qty){ alert("المجموع يتجاوز الحد المتاح بالمخزن"); return; }
        ex.qty += qty;
    } else {
        currentCommandData.push({...b, qty});
    }
    updateCommandUI();
}

function editCommandItemPrice(idx) {
    let item = currentCommandData[idx]; if(!item) return;
    let newPrice = prompt(`تغيير السعر لمنتج [${item.name}]:`, item.sell);
    if(newPrice === null || newPrice.trim() === "") return;
    item.sell = +newPrice;
    updateCommandUI();
}

function loadCommandForEdit() {
    let cmdNum = Number(document.getElementById('editCmdNumInput').value);
    if (!cmdNum || cmdNum <= 0) { alert("أدخل رقم كوموند صالح من فضلك"); return; }

    let targetSales = sales.filter(x => x.command === cmdNum);
    if (targetSales.length === 0) { alert("الكوموند غير مسجل أو تم حذفه سابقاً"); return; }

    if (currentCommandData.length > 0 && !confirm("السلة تحتوي على منتجات، هل تريد استبدالها بالكوموند القديم؟")) return;

    targetSales.forEach(s => { let b = batches.find(x => x.id === s.id); if (b) b.qty += s.qty; });
    currentCommandData = targetSales.map(s => ({ id: s.id, ref: s.ref, name: s.name, buy: s.buy, sell: s.sell, qty: s.qty }));
    sales = sales.filter(x => x.command !== cmdNum);
    commandNumber = cmdNum;

    save(); render(); updateCommandUI(); renderSalesOptions();
    alert(`تمت استعادة الكوموند #${cmdNum}، عند إكمال التعديل اضغط OK لحفظه بنفس الرقم.`);
}

function confirmCommand(){
    if(currentCommandData.length===0){ alert("السلة فارغة تماماً!"); return; }

    currentCommandData.forEach(item=>{
        let b = batches.find(x=>x.id===item.id); if(!b) return;
        b.qty = Math.max(0, (b.qty||0) - (item.qty||0));
        sales.push({
            id:item.id, ref:item.ref, name:item.name, qty:item.qty, buy:item.buy, sell:item.sell,
            profit:(item.sell-item.buy)*item.qty, time:Date.now(), command:commandNumber
        });
    });

    commandNumber = commandNumber + 1;
    currentCommandData=[];
    save(); render(); renderSalesOptions();
}

function deleteSale(index){
    if(!confirm("هل تريد إلغاء هذه المبيعة وإرجاع الكمية للمخزن؟")) return;
    let s = sales[index]; if(!s) return;
    let b = batches.find(x=>x.id===s.id); if(b) b.qty += s.qty;
    
    let deletedCommandNumber = s.command;
    sales.splice(index,1);
    commandNumber = deletedCommandNumber;

    save(); render(); renderSalesOptions();
}

function updateCommandUI(){
    let currentCommand = document.getElementById('currentCommand');
    let commandTotal = document.getElementById('commandTotal');
    let cmdNumber = document.getElementById('cmdNumber');
    let total=0;

    currentCommand.innerHTML = currentCommandData.map((i,idx)=>{
        total += i.sell*i.qty;
        return `
        <div style="display:flex; justify-content:space-between; align-items:center; margin:8px 0; background:var(--background); padding:14px; border-radius:10px; border: 1px solid var(--border);">
            <span style="font-weight:700;">${i.name} <span class="badge-qty">x${i.qty}</span></span>
            <span style="color:var(--primary); font-weight:bold;">${(i.sell*i.qty).toFixed(2)} DA</span>
            <div style="display:flex; gap:6px;">
                <button class="edit" onclick="editCommandItemPrice(${idx})" style="padding:6px 12px; font-size:13px;"><i class="fa-solid fa-tag"></i> السعر</button>
                <button class="del" onclick="removeFromCommand(${idx})" style="padding:6px 12px; font-size:13px;"><i class="fa-solid fa-trash"></i></button>
            </div>
        </div>`;
    }).join("");

    commandTotal.innerHTML = "المجموع الإجمالي: " + total.toFixed(2) + " DA";
    cmdNumber.innerHTML = "Commande #" + commandNumber;
}

function removeFromCommand(i) { currentCommandData.splice(i,1); updateCommandUI(); }

function renderProducts(){
    let searchVal = document.getElementById('productSearch').value.toLowerCase();
    let filtered = batches.filter(b => b.name.toLowerCase().includes(searchVal) || b.ref.toLowerCase().includes(searchVal));

    document.getElementById('productTable').innerHTML = filtered.map(b=>`
    <tr>
        <td><code>${b.ref}</code></td>
        <td><b>${b.name}</b></td>
        <td><span class="badge-qty">${b.qty}</span></td>
        <td>${b.buy.toFixed(2)}</td>
        <td>${b.sell.toFixed(2)}</td>
        <td><button class="edit" onclick="editProduct(${b.id})"><i class="fa-solid fa-pen"></i> تـعديل</button></td>
        <td><button class="del" onclick="deleteProduct(${b.id})"><i class="fa-solid fa-trash"></i></button></td>
    </tr>`).join("");
}

function filterProfitsByDate() {
    let fromVal = document.getElementById('profitFromDate').value;
    let toVal = document.getElementById('profitToDate').value;
    
    if(!fromVal || !toVal) {
        alert("الرجاء اختيار تاريخ البداية وتاريخ النهاية أولاً!");
        return;
    }
    
    let fromTime = new Date(fromVal).setHours(0,0,0,0);
    let toTime = new Date(toVal).setHours(23,59,59,999);
    
    let filteredProfit = 0;
    sales.forEach(s => {
        let t = s.time || Date.now();
        if(t >= fromTime && t <= toTime) {
            filteredProfit += (s.profit || 0);
        }
    });
    
    document.getElementById('customPeriodResultBox').style.display = "block";
    document.getElementById('customPeriodProfit').innerHTML = filteredProfit.toFixed(2) + " DA";
}

function resetProfitFilter() {
    document.getElementById('profitFromDate').value = "";
    document.getElementById('profitToDate').value = "";
    document.getElementById('customPeriodResultBox').style.display = "none";
}

function render(){
    renderProducts();
    let totalCapital = 0, totalValue = 0;

    document.getElementById('stockTable').innerHTML = batches.map(b=>{
        let capital = b.buy * b.qty; let expectedProfit = (b.sell - b.buy) * b.qty;
        totalCapital += capital; totalValue += (b.sell * b.qty);
        return `
        <tr>
            <td><b>${b.name}</b></td>
            <td><span class="badge-qty" style="background:#e0f2fe; color:#0369a1;">${b.qty} قطعة</span></td>
            <td>${capital.toFixed(2)} DA</td>
            <td>${expectedProfit.toFixed(2)} DA</td>
            <td><button class="del" onclick="deleteProduct(${b.id})"><i class="fa-solid fa-trash"></i></button></td>
        </tr>`;
    }).join("");

    document.getElementById('totals').innerHTML = `
        <p><i class="fa-solid fa-money-bill-trend-up" style="color:var(--primary)"></i> <strong>إجمالي رأس المال في المستودع:</strong> ${totalCapital.toFixed(2)} DA</p>
        <p><i class="fa-solid fa-coins" style="color:var(--warning)"></i> <strong>القيمة الإجمالية المتوقعة عند البيع:</strong> ${totalValue.toFixed(2)} DA</p>
        <p style="color:var(--success); font-size: 17px;"><i class="fa-solid fa-circle-dollar-to-slot"></i> <strong>صافي الأرباح المنتظرة الكلية:</strong> ${(totalValue - totalCapital).toFixed(2)} DA</p>`;

    document.getElementById('salesLog').innerHTML = [...sales].reverse().map((s,i)=>{
        let idx = sales.length-1-i;
        return `
        <div class="saleItem">
            <span><b style="color:var(--primary);">#${s.command}</b> - ${s.name} <span class="badge-qty" style="background:#f1f5f9; color:var(--text-main)">x${s.qty}</span></span>
            <span>الربح الصافي: <b style="color:var(--success);">${s.profit.toFixed(2)} DA</b></span>
            <button class="del" onclick="deleteSale(${idx})" style="padding:6px 12px; font-size:12px;"><i class="fa-solid fa-rotate-left"></i> إلغاء المبيعة</button>
        </div>`;
    }).join("");

    let now = new Date(), dProfit = 0, mProfit = 0, yProfit = 0;
    let startOfDay = new Date(now.getFullYear(), now.getMonth(), now.getDate()).getTime();
    let startOfMonth = new Date(now.getFullYear(), now.getMonth(), 1).getTime();
    let startOfYear = new Date(now.getFullYear(), 0, 1).getTime();

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
    <tr style="background: ${b.qty === 0 ? '#fef2f2' : '#fffbeb'}">
        <td><b>${b.name}</b></td>
        <td><span class="badge-qty" style="background:none; color:inherit; font-size:14px;">${b.qty} قطع متبقية</span></td>
        <td><span style="color:${b.qty === 0 ? 'var(--danger)':'#d97706'}; font-weight:800;"><i class="fa-solid fa-circle-exclamation"></i> ${b.qty === 0 ? 'منتهي تماماً ❌' : 'شبه فارغ ⚠️'}</span></td>
    </tr>`).join("");
    
    if(lowItems.length === 0){
        document.getElementById('lowTable').innerHTML = `<tr><td colspan="3" style="color:var(--success); font-weight:700; padding:30px;"><i class="fa-solid fa-circle-check"></i> كل السلع متوفرة بحالة ممتازة في المستودع 🎉</td></tr>`;
    }
    document.getElementById('cmdNumber').innerHTML = "Commande #" + commandNumber;
}

function exportData(){
    let dataStr = JSON.stringify({ batches, sales, commandNumber });
    let dataUri = 'data:application/json;charset=utf-8,'+ encodeURIComponent(dataStr);
    let linkElement = document.createElement('a');
    linkElement.setAttribute('href', dataUri);
    linkElement.setAttribute('download', 'pos_premium_backup_' + new Date().toISOString().slice(0,10) + '.json');
    linkElement.click();
}

function importData(event) {
    let reader = new FileReader();
    reader.onload = function(e){
        try {
            let parsed = JSON.parse(e.target.result);
            if(parsed.batches || parsed.sales){
                batches = parsed.batches || []; sales = parsed.sales || [];
                commandNumber = parsed.commandNumber || 1;
                save(); render(); alert("تم استيراد قاعدة البيانات بنجاح تام!");
            }
        } catch(err) { alert("الملف المرفوع غير مدعوم."); }
    };
    reader.readAsText(event.target.files[0]);
}

render();
</script>
</body>
</html>

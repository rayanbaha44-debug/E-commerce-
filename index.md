<!DOCTYPE html>
<html lang="ar" dir="rtl">

<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>POS SYSTEM PREMIUM - نظام المبيعات الاحترافي</title>

<!-- استدعاء خط Cairo والأيقونات الاحترافية -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght=300;400;600;700;800&display=swap" rel="stylesheet">
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

/* لوحة التحكم الرئيسية */
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

.card:hover i { transform: scale(1.15); }

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

.page.active{ display: block; }

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

/* الأزرار */
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

button:hover{ opacity: 0.95; transform: translateY(-1px); box-shadow: 0 6px 14px rgba(59, 130, 246, 0.35); }

.back{ background: #64748b; box-shadow: 0 4px 10px rgba(100, 116, 139, 0.2); }
.back:hover{ background: #475569; }

.del{ background: var(--danger-gradient); box-shadow: 0 4px 10px rgba(239, 68, 68, 0.2); }
.del:hover { box-shadow: 0 6px 14px rgba(239, 68, 68, 0.35); }

.edit{ background: #f1f5f9; color: var(--text-main); border: 1px solid var(--border); box-shadow: none; }
.edit:hover{ background: var(--border); }

/* المدخلات والقوائم المنسدلة */
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

/* الجداول */
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

th, td{ padding: 18px; text-align: center; border-bottom: 1px solid var(--border); font-size: 15px; }
th { background-color: #f8fafc; color: var(--text-muted); font-weight: 700; }

tfoot tr td {
    padding: 20px;
    font-size: 16px;
    font-weight: 800;
    border-top: 2px solid #cbd5e1;
}

/* الصناديق الفرعية */
.box{
    background: #f8fafc;
    padding: 24px;
    border-radius: var(--radius-lg);
    margin-bottom: 20px;
    border: 1px solid var(--border);
}

.flex-inputs { display: flex; gap: 14px; align-items: center; }
#salesLog, #expensesLog{ margin-top: 15px; max-height: 250px; overflow-y: auto; }

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

.badge-qty { background: #fef3c7; color: #d97706; padding: 5px 10px; border-radius: 8px; font-weight: 700; }

/* كروت الأرباح */
.profit-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 16px; margin-top: 20px; }
.profit-card { background: var(--surface); padding: 25px; border-radius: var(--radius-lg); border: 1px solid var(--border); border-right: 5px solid var(--primary); box-shadow: var(--shadow-md); }
.profit-card.success { border-right-color: var(--success); }
.profit-card.dark { border-right-color: var(--text-main); }
.profit-card.filter { border-right-color: #a855f7; background: #faf5ff; }
.profit-card.expense-card { border-right-color: var(--danger); background: #fef2f2; }
.profit-card p { color: var(--text-muted); font-size: 14px; font-weight: 700; margin-bottom: 5px;}
.profit-card .amount { font-size: 24px; font-weight: 800; }

/* ألوان التدريج لجدول النواقص */
.stock-empty { background-color: #27272a !important; color: #ffffff !important; }
.stock-danger { background-color: #fee2e2 !important; color: #991b1b !important; }
.stock-warning { background-color: #ffedd5 !important; color: #9a3412 !important; }
.stock-notice { background-color: #e0f2fe !important; color: #075985 !important; }
</style>
</head>

<body>

<!-- DASHBOARD -->
<div id="dashboard">
    <div class="card" onclick="openPage('products')"><i class="fa-solid fa-box-open"></i> إدارة المنتجات</div>
    <div class="card" onclick="openPage('sales')"><i class="fa-solid fa-cash-register"></i> واجهة البيع السريعة</div>
    <div class="card" onclick="openPage('stock')"><i class="fa-solid fa-warehouse"></i> جرد المخزون الكلي</div>
    <div class="card" onclick="openPage('low')"><i class="fa-solid fa-triangle-exclamation" style="background:var(--warning); -webkit-background-clip: text;"></i> السلع الناقصة</div>
    <div class="card" onclick="openPage('expenses')"><i class="fa-solid fa-hand-holding-dollar" style="background:var(--danger-gradient); -webkit-background-clip: text;"></i> إدارة المصاريف 💸</div>
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
        <h3 style="margin-bottom: 12px; font-size:16px;"><i class="fa-solid fa-plus-circle"></i> إضافة منتج جديد يدوياً</h3>
        <input id="pRef" placeholder="الرقم المتسلسل / الباركود (Ref)">
        <input id="pName" placeholder="اسم المنتج بالكامل">
        <div class="flex-inputs">
            <input id="pBuy" type="number" step="0.01" placeholder="سعر الشراء (DA)">
            <input id="pSell" type="number" step="0.01" placeholder="سعر البيع (DA)">
            <input id="pQty" type="number" step="0.01" placeholder="الكمية الابتدائية">
        </div>
        <button onclick="addProduct()" style="width: 100%; margin-top: 12px; background: var(--success-gradient);"><i class="fa-solid fa-plus"></i> إضافة المنتج للمخزن</button>
    </div>
    <input id="productSearch" placeholder="🔍 ابحث بالترتيب الأبجدي المتسلسل..." oninput="renderProducts()">
    <table>
        <thead><tr><th>الباركود</th><th>اسم المنتج</th><th>الكمية</th><th>الشراء</th><th>البيع</th><th>تعديل</th><th>حذف</th></tr></thead>
        <tbody id="productTable"></tbody>
    </table>
</div>

<!-- SALES -->
<div id="sales" class="page">
    <div class="header">
        <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع</button>
        <h2><i class="fa-solid fa-cash-register" style="color:var(--primary);"></i> واجهة البيع السريعة</h2>
    </div>
    <div class="box" style="background: var(--text-main); color: white; text-align: center;">
        <h3 id="cmdNumber" style="font-weight: 800; font-size: 22px;">Commande #1</h3>
    </div>
    <input id="saleSearch" placeholder="🔍 ابحث هنا بالترتيب الأبجدي للمنتج..." oninput="renderSalesOptions()">
    <select id="saleStock"></select>
    <input id="saleQty" type="number" step="1" value="1" placeholder="الكمية">
    <button onclick="addToCommand()" style="width: 100%; margin-bottom: 25px; height: 50px;"><i class="fa-solid fa-cart-plus"></i> إضافة إلى السلة الحالية</button>
    <div class="box" style="background: #fff; border: 1px solid var(--border);">
        <h3 style="margin-bottom: 15px;"><i class="fa-solid fa-basket-shopping" style="color:var(--primary)"></i> سلة التسوق الحالية</h3>
        <div id="currentCommand"></div>
        <h3 id="commandTotal" style="margin-top:20px; color: var(--success); text-align: left; font-weight:800;">المجموع: 0.00 DA</h3>
        <button onclick="confirmCommand()" style="width:100%; margin-top:15px; background: var(--success-gradient); font-size: 18px; padding: 16px;"><i class="fa-solid fa-circle-check"></i> تأكيد وحفظ الطلب (OK)</button>
    </div>
    <h3 style="margin-top: 25px; color: var(--text-muted); font-weight:700;"><i class="fa-solid fa-clock-rotate-left"></i> سجل عمليات البيع</h3>
    <div id="salesLog"></div>
</div>

<!-- STOCK -->
<div id="stock" class="page">
    <div class="header">
        <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع</button>
        <h2><i class="fa-solid fa-warehouse" style="color:var(--primary);"></i> كشف وجرد المخزن الكلي</h2>
    </div>
    <table>
        <thead><tr><th>اسم المنتج</th><th>القطع المتبقية</th><th>رأس المال المستثمر</th><th>الأرباح المتوقعة</th><th>إجراء</th></tr></thead>
        <tbody id="stockTable"></tbody>
        <tfoot id="stockTableFoot"></tfoot>
    </table>
</div>

<!-- LOW -->
<div id="low" class="page">
    <div class="header">
        <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع</button>
        <h2><i class="fa-solid fa-triangle-exclamation" style="color:var(--warning);"></i> كشف السلع الناقصة بالتدرج</h2>
    </div>
    <table>
        <thead><tr><th>اسم المنتج</th><th>الكمية المتبقية</th><th>حالة خطورة المخزون</th></tr></thead>
        <tbody id="lowTable"></tbody>
    </table>
</div>

<!-- EXPENSES -->
<div id="expenses" class="page">
    <div class="header">
        <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع</button>
        <h2><i class="fa-solid fa-hand-holding-dollar" style="color:var(--danger);"></i> إدارة مصاريف المحل الكلية 💸</h2>
    </div>
    <div class="box">
        <h3 style="margin-bottom: 12px; font-size:16px;"><i class="fa-solid fa-file-invoice-dollar"></i> تسجيل مصروف جديد</h3>
        <input id="expTitle" placeholder="بيان / نوع المصروف (مثال: كراء المحل، فاتورة الكهرباء، سلعة تالفة...)">
        <div class="flex-inputs">
            <input id="expAmount" type="number" step="0.01" placeholder="قيمة المصروف (DA)">
            <input id="expDate" type="date">
        </div>
        <button onclick="addExpense()" style="width: 100%; margin-top: 12px; background: var(--danger-gradient);"><i class="fa-solid fa-check"></i> حفظ وقيد المصروف</button>
    </div>
    <h3 style="color: var(--text-muted); font-weight:700; margin-top:20px;"><i class="fa-solid fa-receipt"></i> سجل المصاريف المقيدة</h3>
    <div id="expensesLog"></div>
</div>

<!-- PROFITS -->
<div id="profits" class="page">
    <div class="header">
        <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع</button>
        <h2><i class="fa-solid fa-chart-line" style="color:var(--success);"></i> التقارير المالية والأرباح الصافية الحقيقية</h2>
    </div>
    <div class="box" style="background: #fff; border: 1px solid var(--border);">
        <h3 style="margin-bottom: 12px; font-size:16px; color: #a855f7;"><i class="fa-solid fa-calendar-days"></i> فرز واحتساب الأرباح بفترة زمنية مخصصة 🗓️</h3>
        <div class="flex-inputs">
            <div style="flex:1;"><label style="font-size:13px; font-weight:700; color:var(--text-muted);">من تاريخ 📅:</label><input type="date" id="filterFrom" onchange="calculateFilteredProfit()"></div>
            <div style="flex:1;"><label style="font-size:13px; font-weight:700; color:var(--text-muted);">إلى تاريخ 🏁:</label><input type="date" id="filterTo" onchange="calculateFilteredProfit()"></div>
        </div>
    </div>
    <div class="profit-grid">
        <div class="profit-card filter" style="grid-column: span 2 / span 2;">
            <p>🎯 صافي فائدة الفترة المحددة (فائدة المبيعات - المصاريف)</p>
            <div id="filteredProfit" class="amount" style="color: #a855f7;">0.00 DA 💰</div>
        </div>
        <div class="profit-card success">
            <p>💵 صافي أرباح اليوم الحالي</p>
            <div id="dailyProfit" class="amount" style="color: var(--success);">0.00 DA</div>
        </div>
        <div class="profit-card">
            <p>📈 صافي أرباح الشهر الحالي</p>
            <div id="monthlyProfit" class="amount" style="color: var(--primary);">0.00 DA</div>
        </div>
        <div class="profit-card expense-card" style="grid-column: span 2 / span 2;">
            <p>📉 إجمالي مصاريف السنة المسجلة</p>
            <div id="totalExpensesYear" class="amount" style="color: var(--danger);">0.00 DA 💸</div>
        </div>
        <div class="profit-card dark" style="grid-column: span 2 / span 2;">
            <p>👑 صافي فائدة السنة الإجمالية الحقيقية</p>
            <div id="yearlyProfit" class="amount" style="color: var(--text-main);">0.00 DA</div>
        </div>
    </div>
</div>

<script>
/* ================= SYSTEM LOGIC ================= */
let batches = JSON.parse(localStorage.getItem("batches") || "[]");
let sales = JSON.parse(localStorage.getItem("sales") || "[]");
let expenses = JSON.parse(localStorage.getItem("expenses") || "[]");
let commandNumber = Number(localStorage.getItem("commandNumber")) || 1;
let currentCommandData = [];

window.onload = function() {
    let todayStr = new Date().toISOString().split('T')[0];
    document.getElementById('filterFrom').value = todayStr;
    document.getElementById('filterTo').value = todayStr;
    document.getElementById('expDate').value = todayStr;
    render();
};

function save(){
    localStorage.setItem("batches", JSON.stringify(batches));
    localStorage.setItem("sales", JSON.stringify(sales));
    localStorage.setItem("expenses", JSON.stringify(expenses));
    localStorage.setItem("commandNumber", commandNumber);
}

function openPage(id){
    document.getElementById("dashboard").style.display="none";
    document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
    document.getElementById(id).classList.add("active");
    if(id === 'sales') { document.getElementById('saleSearch').value = ''; renderSalesOptions(); }
    window.scrollTo(0, 0);
}

function back(){ document.getElementById("dashboard").style.display="grid"; document.querySelectorAll(".page").forEach(p=>p.classList.remove("active")); }

/* دالة إنتاج نغمة الباركود الاحترافية تلقائياً دون ملفات خارجية */
function playBeepSound() {
    try {
        let audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        let oscillator = audioCtx.createOscillator();
        let gainNode = audioCtx.createGain();

        oscillator.type = 'sine';
        oscillator.frequency.setValueAtTime(1100, audioCtx.currentTime); // تردد حاد ومميز مثل قارئ الكود
        gainNode.gain.setValueAtTime(0.15, audioCtx.currentTime); // مستوى صوت متناسق ومريح للأذن

        oscillator.connect(gainNode);
        gainNode.connect(audioCtx.destination);

        oscillator.start();
        oscillator.stop(audioCtx.currentTime + 0.1); // مدة رنة قصيرة جداً وسريعة (0.1 ثانية)
    } catch (e) {
        console.log("Audio API not supported or blocked by browser user gesture.");
    }
}

function addProduct(){
    let ref = document.getElementById('pRef').value.trim();
    let name = document.getElementById('pName').value.trim();
    let buy = document.getElementById('pBuy').value;
    let sell = document.getElementById('pSell').value;
    let qty = document.getElementById('pQty').value;

    if(!ref || !name || !buy || !sell || !qty) return alert("يرجى ملء جميع الخانات");

    let existing = batches.find(b => b.ref === ref);
    if(existing) { existing.qty += +qty; } else { batches.push({ id: Date.now(), ref, name, buy: +buy, sell: +sell, qty: +qty }); }

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
    b.name = prompt("تعديل اسم المنتج:", b.name) || b.name;
    b.qty = +prompt("تعديل الكمية الحالية:", b.qty) || b.qty;
    b.buy = +prompt("تعديل سعر الشراء:", b.buy) || b.buy;
    b.sell = +prompt("تعديل سعر البيع:", b.sell) || b.sell;
    save(); render();
}

function renderSalesOptions(){
    let searchVal = document.getElementById('saleSearch').value.toLowerCase().trim();
    let filtered = batches.filter(b => b.name.toLowerCase().startsWith(searchVal) || b.ref.toLowerCase().startsWith(searchVal));
    let saleStock = document.getElementById('saleStock');
    saleStock.innerHTML = filtered.map(b => `<option value="${b.id}">[${b.ref}] ${b.name} - المتبقي: ${b.qty} - السعر: ${b.sell} DA</option>`).join("");
}

function addToCommand(){
    let saleStock = document.getElementById('saleStock');
    let saleQty = document.getElementById('saleQty');
    if(!saleStock.value) return;

    let id = Number(saleStock.value);
    let qty = +saleQty.value;
    let b = batches.find(x=>x.id===id);
    if(!b || qty<=0) return;

    if(b.qty < qty){ alert("المخزون غير كافي"); return; }
    let ex = currentCommandData.find(x=>x.id===id);

    if(ex){
        if(b.qty < ex.qty + qty){ alert("المجموع يتجاوز المتاح"); return; }
        ex.qty += qty;
    } else { currentCommandData.push({...b, qty}); }
    
    playBeepSound(); // تشغيل الصوت فور الإضافة الناجحة للسلة 🔊
    updateCommandUI();
}

function updateCommandUI(){
    let currentCommand = document.getElementById('currentCommand');
    let commandTotal = document.getElementById('commandTotal');
    let total=0;

    currentCommand.innerHTML = currentCommandData.map((i,idx)=>{
        total += i.sell*i.qty;
        return `
        <div style="display:flex; justify-content:space-between; align-items:center; margin:8px 0; background:var(--background); padding:14px; border-radius:10px;">
            <span>${i.name} <span class="badge-qty">x${i.qty}</span></span>
            <span style="color:var(--primary); font-weight:bold;">${(i.sell*i.qty).toFixed(2)} DA</span>
            <button class="del" onclick="removeFromCommand(${idx})" style="padding:6px 12px; font-size:13px;"><i class="fa-solid fa-trash"></i></button>
        </div>`;
    }).join("");

    commandTotal.innerHTML = "المجموع الإجمالي: " + total.toFixed(2) + " DA";
}

function removeFromCommand(i) { currentCommandData.splice(i,1); updateCommandUI(); }

function confirmCommand(){
    if(currentCommandData.length===0) return alert("السلة فارغة!");
    let uniqueTime = Date.now(); 

    currentCommandData.forEach((item, index)=>{
        let b = batches.find(x=>x.id===item.id); 
        if(!b) return;
        b.qty = Math.max(0, b.qty - item.qty);
        
        sales.push({
            id: item.id, 
            ref: item.ref, 
            name: item.name, 
            qty: item.qty, 
            buy: item.buy, 
            sell: item.sell,
            profit: (item.sell - item.buy) * item.qty, 
            time: uniqueTime + index, 
            command: commandNumber
        });
    });

    commandNumber++;
    currentCommandData=[];
    save(); render(); renderSalesOptions();
}

function deleteSaleByTime(saleTime){
    if(!confirm("هل تريد إلغاء وحذف هذه المبيعة؟ (سيتم إرجاع السلعة إلى المخزن تلقائياً)")) return;
    let s = sales.find(x => x.time === saleTime);
    if(!s) return;
    
    let b = batches.find(x => x.id === s.id); 
    if(b) { b.qty += s.qty; } 
    else { batches.push({ id: s.id, ref: s.ref, name: s.name, buy: s.buy, sell: s.sell, qty: s.qty }); }
    
    sales = sales.filter(x => x.time !== saleTime);
    save(); render(); renderSalesOptions();
}

function addExpense(){
    let title = document.getElementById('expTitle').value.trim();
    let amount = document.getElementById('expAmount').value;
    let dateVal = document.getElementById('expDate').value;

    if(!title || !amount || !dateVal) return alert("يرجى ملء كافة خانات المصروف");

    expenses.push({
        id: Date.now(),
        title: title,
        amount: +amount,
        date: dateVal
    });

    document.getElementById('expTitle').value = '';
    document.getElementById('expAmount').value = '';
    save(); render();
}

function deleteExpense(id){
    if(!confirm("هل تريد حذف هذا المصروف؟")) return;
    expenses = expenses.filter(x => x.id !== id);
    save(); render();
}

function calculateFilteredProfit(){
    let fromVal = document.getElementById('filterFrom').value;
    let toVal = document.getElementById('filterTo').value;
    if(!fromVal || !toVal) return;

    let startTime = new Date(fromVal + "T00:00:00").getTime();
    let endTime = new Date(toVal + "T23:59:59").getTime();
    
    let totalSalesProfit = 0;
    sales.forEach(s => {
        let t = s.time || Date.now();
        if(t >= startTime && t <= endTime) totalSalesProfit += s.profit;
    });

    let totalExp = 0;
    expenses.forEach(e => {
        let expTime = new Date(e.date + "T12:00:00").getTime();
        if(expTime >= startTime && expTime <= endTime) totalExp += e.amount;
    });

    let netProfit = totalSalesProfit - totalExp;
    document.getElementById('filteredProfit').innerHTML = netProfit.toFixed(2) + " DA 💰";
}

function renderProducts(){
    let searchVal = document.getElementById('productSearch').value.toLowerCase().trim();
    let filtered = batches.filter(b => b.name.toLowerCase().startsWith(searchVal) || b.ref.toLowerCase().startsWith(searchVal));

    document.getElementById('productTable').innerHTML = filtered.map(b=>`
    <tr>
        <td><code>${b.ref}</code></td>
        <td><b>${b.name}</b></td>
        <td><span class="badge-qty">${b.qty}</span></td>
        <td>${b.buy}</td>
        <td>${b.sell}</td>
        <td><button class="edit" onclick="editProduct(${b.id})"><i class="fa-solid fa-pen"></i></button></td>
        <td><button class="del" onclick="deleteProduct(${b.id})"><i class="fa-solid fa-trash"></i></button></td>
    </tr>`).join("");
}

function render(){
    renderProducts();
    let totalCapital = 0, totalValue = 0, totalPieces = 0;

    document.getElementById('stockTable').innerHTML = batches.map(b=>{
        let capital = b.buy * b.qty; let expectedProfit = (b.sell - b.buy) * b.qty;
        totalCapital += capital; totalValue += (b.sell * b.qty); totalPieces += b.qty;
        return `<tr><td><b>${b.name}</b></td><td><span class="badge-qty" style="background:#e0f2fe; color:#0369a1;">${b.qty} قطعة</span></td><td>${capital.toFixed(2)} DA</td><td>${expectedProfit.toFixed(2)} DA</td><td><button class="del" onclick="deleteProduct(${b.id})"><i class="fa-solid fa-trash"></i></button></td></tr>`;
    }).join("");

    document.getElementById('stockTableFoot').innerHTML = `
        <tr style="background: #f8fafc;">
            <td style="color: var(--text-main); font-weight:800; text-align:right;">📦 إجمالي المخزون المتبقي الكلي:</td>
            <td style="color: #0284c7; background: #e0f2fe; font-weight:800;">${totalPieces} قطعة 🛍️</td>
            <td style="color: #b91c1c; background: #fee2e2; font-weight:800;">${totalCapital.toFixed(2)} DA 💰</td>
            <td style="color: #047857; background: #d1fae5; font-weight:800;">${(totalValue - totalCapital).toFixed(2)} DA 💵</td>
            <td></td>
        </tr>`;

    document.getElementById('salesLog').innerHTML = [...sales].reverse().map((s)=>{
        return `<div class="saleItem"><span><b style="color:var(--primary);">#${s.command}</b> - ${s.name} <span class="badge-qty">x${s.qty}</span></span><span>الربح: <b style="color:var(--success);">${s.profit.toFixed(2)} DA</b></span><button class="del" onclick="deleteSaleByTime(${s.time})" style="padding:6px 12px; font-size:12px;"><i class="fa-solid fa-trash-can"></i> حذف وإرجاع</button></div>`;
    }).join("");

    let totalExpensesSum = 0;
    document.getElementById('expensesLog').innerHTML = [...expenses].reverse().map(e => {
        totalExpensesSum += e.amount;
        return `
        <div class="saleItem" style="border-right: 5px solid var(--danger);">
            <span>💸 <b>${e.title}</b> <small style="color:var(--text-muted); margin-right:10px;">(${e.date})</small></span>
            <span>القيمة: <b style="color:var(--danger);">${e.amount.toFixed(2)} DA</b></span>
            <button class="del" onclick="deleteExpense(${e.id})" style="padding:6px 12px; font-size:12px;"><i class="fa-solid fa-trash-can"></i> حذف</button>
        </div>`;
    }).join("");
    if(expenses.length === 0) document.getElementById('expensesLog').innerHTML = "<p style='text-align:center; padding:15px; color:var(--text-muted);'>لا توجد مصاريف مقيدة حالياً 🌟</p>";

    let now = new Date(), dProfit = 0, mProfit = 0, yProfit = 0;
    let dExp = 0, mExp = 0;

    let startOfDay = new Date(now.getFullYear(), now.getMonth(), now.getDate()).getTime();
    let startOfMonth = new Date(now.getFullYear(), now.getMonth(), 1).getTime();
    let startOfYear = new Date(now.getFullYear(), 0, 1).getTime();

    sales.forEach(s => {
        let t = s.time || Date.now();
        if(t >= startOfDay) dProfit += s.profit;
        if(t >= startOfMonth) mProfit += s.profit;
        if(t >= startOfYear) yProfit += s.profit;
    });

    expenses.forEach(e => {
        let expTime = new Date(e.date + "T12:00:00").getTime();
        if(expTime >= startOfDay) dExp += e.amount;
        if(expTime >= startOfMonth) mExp += e.amount;
    });

    document.getElementById('dailyProfit').innerHTML = (dProfit - dExp).toFixed(2) + " DA 💵";
    document.getElementById('monthlyProfit').innerHTML = (mProfit - mExp).toFixed(2) + " DA 📈";
    document.getElementById('totalExpensesYear').innerHTML = totalExpensesSum.toFixed(2) + " DA 💸";
    document.getElementById('yearlyProfit').innerHTML = (yProfit - totalExpensesSum).toFixed(2) + " DA 👑";

    calculateFilteredProfit();

    let lowItems = batches.filter(b => b.qty <= 15);
    lowItems.sort((a, b) => a.qty - b.qty);
    document.getElementById('lowTable').innerHTML = lowItems.map(b => {
        let rowClass = "", statusText = "";
        if (b.qty === 0) { rowClass = "stock-empty"; statusText = "منتهي تماماً (0 قطع) ❌"; } 
        else if (b.qty <= 5) { rowClass = "stock-danger"; statusText = "نقص حاد جداً (1-5 قطع) 🚨"; } 
        else if (b.qty <= 10) { rowClass = "stock-warning"; statusText = "نقص متوسط (6-10 قطع) ⚠️"; } 
        else if (b.qty <= 15) { rowClass = "stock-notice"; statusText = "بداية نقص (11-15 قطعة) ℹ️"; }
        return `<tr class="${rowClass}"><td><b>${b.name}</b></td><td><b>${b.qty} قطعة</b></td><td><b>${statusText}</b></td></tr>`;
    }).join("");
    
    if(lowItems.length === 0) document.getElementById('lowTable').innerHTML = `<tr><td colspan="3" style="color:var(--success); font-weight:700; padding:30px;">🎉 كل السلع متوفرة بكميات ممتازة (+15 قطعة)</td></tr>`;
    
    document.getElementById('cmdNumber').innerHTML = "Commande #" + commandNumber;
}

function exportData(){
    let dataStr = JSON.stringify({ batches, sales, expenses, commandNumber });
    let dataUri = 'data:application/json;charset=utf-8,'+ encodeURIComponent(dataStr);
    let linkElement = document.createElement('a');
    linkElement.setAttribute('href', dataUri);
    linkElement.setAttribute('download', 'pos_premium_backup.json');
    linkElement.click();
}
</script>
</body>
</html>

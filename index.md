<!DOCTYPE html>
<html lang="ar" dir="rtl">

<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>POS SYSTEM EXECUTIVE - نظام المبيعات المطور بالخطورة الديناميكية</title>

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

<style>
/* ================= ULTRA PREMIUM MODERN DARK/NEON UI ================= */
:root {
    --primary: #3b82f6;
    --primary-gradient: linear-gradient(135deg, #3b82f6 0%, #1d4ed8 100%);
    --success: #10b981;
    --success-gradient: linear-gradient(135deg, #10b981 0%, #059669 100%);
    --danger: #ef4444;
    --danger-gradient: linear-gradient(135deg, #ef4444 0%, #b91c1c 100%);
    --warning: #f59e0b;
    --warning-gradient: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);
    --purple-gradient: linear-gradient(135deg, #a855f7 0%, #7e22ce 100%);
    
    --bg-app: #090d16; 
    --bg-gradient: linear-gradient(135deg, #090d16 0%, #111827 100%);
    --surface: #1f2937; 
    --surface-card: rgba(22, 30, 49, 0.8);
    
    --text-main: #ffffff; 
    --text-muted: #9ca3af; 
    --border: rgba(255, 255, 255, 0.08);
    
    --radius-xl: 24px;
    --radius-lg: 16px;
    --radius-md: 12px;
    
    --shadow-blur: 0 10px 30px -5px rgba(0, 0, 0, 0.5);
    --shadow-hover: 0 20px 40px -10px rgba(37, 99, 235, 0.4);
}

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Cairo', sans-serif;
}

body {
    background: var(--bg-gradient);
    color: var(--text-main);
    min-height: 100vh;
    padding: 40px 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
}

/* لوحة التحكم الرئيسية (Dashboard) */
#dashboard {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
    gap: 25px;
    width: 100%;
    max-width: 1100px;
    margin: 40px auto;
}

.card {
    background: var(--surface-card);
    backdrop-filter: blur(12px);
    -webkit-backdrop-filter: blur(12px);
    padding: 35px 25px;
    border-radius: var(--radius-xl);
    text-align: center;
    cursor: pointer;
    border: 1px solid rgba(255, 255, 255, 0.05);
    font-weight: 700;
    font-size: 18px;
    color: var(--text-main);
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    box-shadow: var(--shadow-blur);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 18px;
    position: relative;
    overflow: hidden;
}

.card::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 4px;
    background: var(--primary-gradient);
    transform: scaleX(0);
    transition: transform 0.3s ease;
}

.card:hover::after { transform: scaleX(1); }

.card i {
    font-size: 40px;
    background: var(--primary-gradient);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    transition: transform 0.3s ease;
}

.card:hover {
    transform: translateY(-8px);
    box-shadow: var(--shadow-hover);
    border-color: rgba(59, 130, 246, 0.4);
    background: rgba(31, 41, 55, 0.9);
}

.card:hover i { transform: scale(1.15) rotate(3deg); }

/* الصفحات والحاويات الرئيسية */
.page {
    display: none;
    width: 100%;
    max-width: 1200px;
    background: rgba(17, 24, 39, 0.85);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    padding: 40px;
    border-radius: var(--radius-xl);
    box-shadow: 0 30px 60px -15px rgba(0, 0, 0, 0.7);
    border: 1px solid rgba(255, 255, 255, 0.1);
    animation: slideUp 0.5s cubic-bezier(0.16, 1, 0.3, 1);
}

@keyframes slideUp {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
}

.page.active { display: block; }

.header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 30px;
    padding-bottom: 25px;
    border-bottom: 1px solid var(--border);
}

.header h2 {
    font-size: 26px;
    font-weight: 800;
    color: var(--text-main);
    display: flex;
    align-items: center;
    gap: 15px;
}

/* الأزرار الاحترافية بنظام التوهج */
button {
    padding: 14px 24px;
    border: none;
    border-radius: var(--radius-md);
    cursor: pointer;
    background: var(--primary-gradient);
    color: white;
    font-weight: 700;
    font-size: 15px;
    transition: all 0.25s cubic-bezier(0.4, 0, 0.2, 1);
    display: inline-flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
    box-shadow: 0 4px 12px rgba(37, 99, 235, 0.2);
}

button:hover { opacity: 0.95; transform: translateY(-2px); box-shadow: 0 6px 20px rgba(37, 99, 235, 0.4); }
button:active { transform: translateY(0); }

.back { background: #374151; box-shadow: 0 4px 12px rgba(55, 65, 81, 0.2); }
.back:hover { background: #4b5563; box-shadow: 0 6px 20px rgba(75, 85, 99, 0.4); }

.del { background: var(--danger-gradient); box-shadow: 0 4px 12px rgba(239, 68, 68, 0.2); }
.del:hover { box-shadow: 0 6px 20px rgba(239, 68, 68, 0.4); }

.edit { background: #1f2937; color: #3b82f6; border: 1px solid rgba(59, 130, 246, 0.3); box-shadow: none; }
.edit:hover { background: #3b82f6; color: white; }

/* عناصر الإدخال والقوائم */
label {
    display: block;
    font-size: 14px;
    font-weight: 700;
    color: #9ca3af;
    margin-bottom: 8px;
}

input, select {
    width: 100%;
    padding: 14px 18px;
    border-radius: var(--radius-md);
    border: 1px solid rgba(255, 255, 255, 0.15);
    background: #111827;
    color: var(--text-main);
    font-size: 15px;
    font-weight: 600;
    transition: all 0.25s ease;
}

input:focus, select:focus {
    outline: none;
    border-color: var(--primary);
    background: #090d16;
    box-shadow: 0 0 0 4px rgba(59, 130, 246, 0.3);
}

input.input-error {
    border-color: var(--danger) !important;
    background: rgba(239, 68, 68, 0.1) !important;
    box-shadow: 0 0 0 4px rgba(239, 68, 68, 0.3) !important;
    animation: shake 0.3s ease;
}

@keyframes shake {
    0%, 100% { transform: translateX(0); }
    25% { transform: translateX(-6px); }
    75% { transform: translateX(6px); }
}

/* تقسيم واجهة البيع بالتساوي */
.sales-grid {
    display: grid;
    grid-template-columns: 1.2fr 1fr;
    gap: 30px;
    align-items: start;
}

@media (max-width: 950px) {
    .sales-grid { grid-template-columns: 1fr; }
}

.box {
    background: rgba(9, 13, 22, 0.6);
    padding: 25px;
    border-radius: var(--radius-lg);
    margin-bottom: 25px;
    border: 1px solid var(--border);
}

.flex-inputs { display: flex; gap: 15px; align-items: center; margin-bottom: 20px; }
.flex-inputs > div { flex: 1; }

/* الجداول المتطورة */
table {
    width: 100%;
    margin-top: 25px;
    border-collapse: separate;
    border-spacing: 0;
    border-radius: var(--radius-lg);
    overflow: hidden;
    border: 1px solid rgba(255, 255, 255, 0.12);
    box-shadow: 0 15px 30px rgba(0,0,0,0.5);
    table-layout: auto;
}

th, td { 
    padding: 18px 15px; 
    text-align: center; 
    font-size: 15px; 
    vertical-align: middle;
}

th { 
    background-color: #111827; 
    color: #9ca3af; 
    font-weight: 700; 
    border-bottom: 2px solid rgba(255, 255, 255, 0.15); 
}

td { 
    background-color: #1f2937; 
    border-bottom: 1px solid rgba(255, 255, 255, 0.06); 
    color: #ffffff; 
    font-weight: 600;
}

tr:hover td {
    background-color: #2563eb; 
    color: #ffffff !important;
    transition: background 0.15s ease;
}

td code {
    background: rgba(0, 0, 0, 0.4);
    padding: 6px 12px;
    border-radius: 8px;
    color: #38bdf8; 
    font-family: monospace;
    font-size: 14px;
    border: 1px solid rgba(56, 189, 248, 0.2);
    font-weight: 700;
    display: inline-block;
    max-width: 180px;
    word-break: break-all;
    white-space: normal;
    overflow-wrap: break-word;
    line-height: 1.4;
    text-align: center;
}

tr:hover td code {
    color: #ffffff;
    background: rgba(0,0,0,0.3);
    border-color: #ffffff;
}

tr:last-child td { border-bottom: none; }

.order-card {
    background: #1f2937;
    border: 1px solid var(--border);
    border-radius: var(--radius-lg);
    padding: 20px;
    margin-bottom: 20px;
    box-shadow: var(--shadow-blur);
}

.order-card-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 1px dashed var(--border);
    padding-bottom: 12px;
    margin-bottom: 12px;
}

.order-item-line {
    display: flex;
    justify-content: space-between;
    padding: 8px 0;
    font-size: 14px;
    border-bottom: 1px solid rgba(255, 255, 255, 0.02);
}

.badge-qty { background: #111827; color: #f59e0b; padding: 4px 12px; border-radius: 8px; font-weight: 800; font-size: 13px; border: 1px solid rgba(245, 158, 11, 0.3); }

/* كروت شبكة تقارير الأرباح والمخزون */
.profit-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 20px; margin-top: 25px; }
.profit-card { background: #1f2937; padding: 25px; border-radius: var(--radius-lg); border: 1px solid var(--border); border-right: 5px solid var(--primary); box-shadow: var(--shadow-blur); }
.profit-card.success { border-right-color: var(--success); }
.profit-card.dark { border-right-color: #cbd5e1; }
.profit-card.filter { border-right-color: #a855f7; background: rgba(168, 85, 247, 0.05); border-top: 1px solid rgba(168, 85, 247, 0.1); }
.profit-card.expense-card { border-right-color: var(--danger); background: rgba(239, 68, 68, 0.05); border-top: 1px solid rgba(239, 68, 68, 0.1); }
.profit-card p { color: var(--text-muted); font-size: 14px; font-weight: 700; margin-bottom: 8px;}
.profit-card .amount { font-size: 24px; font-weight: 800; }

/* شارات درجات الخطورة الثابتة للجداول والباركود */
.risk-badge {
    padding: 6px 12px;
    border-radius: 6px;
    font-weight: 800;
    font-size: 13px;
    display: inline-block;
}

.net-profit-section {
    background-color: rgba(59, 130, 246, 0.1) !important;
    border: 2px solid var(--primary);
}

.highlight-neon {
    font-weight: 900;
    color: #38bdf8;
    font-size: 1.3em;
    text-shadow: 0 0 10px rgba(56, 189, 248, 0.4);
}

::-webkit-scrollbar { width: 10px; }
::-webkit-scrollbar-track { background: #090d16; }
::-webkit-scrollbar-thumb { background: #374151; border-radius: 5px; }
::-webkit-scrollbar-thumb:hover { background: #4b5563; }
</style>
</head>

<body>

<div id="dashboard">
    <div class="card" onclick="openPage('products')"><i class="fa-solid fa-box-open"></i> إدارة المنتجات والمخزن</div>
    <div class="card" onclick="openPage('sales')"><i class="fa-solid fa-cash-register"></i> واجهة البيع السريعة</div>
    <div class="card" onclick="openPage('stock')"><i class="fa-solid fa-warehouse"></i> جرد المخزون الكلي</div>
    <div class="card" onclick="openPage('low')"><i class="fa-solid fa-triangle-exclamation" style="background:var(--warning-gradient); -webkit-background-clip: text;"></i> السلع الناقصة بالمحل</div>
    <div class="card" onclick="openPage('expenses')"><i class="fa-solid fa-hand-holding-dollar" style="background:var(--danger-gradient); -webkit-background-clip: text;"></i> إدارة المصاريف الكلية</div>
    <div class="card" onclick="openPage('profits')"><i class="fa-solid fa-chart-line" style="background:var(--success-gradient); -webkit-background-clip: text;"></i> تقارير الأرباح الصافية</div>
    
    <div class="card" onclick="exportData()" style="background: rgba(16, 185, 129, 0.02); border: 1px dashed rgba(16, 185, 129, 0.25);"><i class="fa-solid fa-file-export" style="background:var(--success-gradient); -webkit-gradient-clip: text;"></i> تصدير نسخة احتياطية</div>
    <div class="card" onclick="triggerImport()" style="background: rgba(168, 85, 247, 0.02); border: 1px dashed rgba(168, 85, 247, 0.25);"><i class="fa-solid fa-file-import" style="background:var(--purple-gradient); -webkit-background-clip: text;"></i> استيراد نسخة من الكمبيوتر</div>
</div>

<input type="file" id="importFileInput" accept=".json" style="display: none;" onchange="importData(event)">

<div id="products" class="page">
    <div class="header">
        <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع للرئيسية</button>
        <h2><i class="fa-solid fa-box-open" style="color:var(--primary);"></i> إدارة المنتجات والمخزن</h2>
    </div>
    <div class="box">
        <h3 style="margin-bottom: 20px; font-size:17px;"><i class="fa-solid fa-plus-circle"></i> إضافة منتج جديد يدوياً</h3>
        <div class="flex-inputs">
            <div><label>الباركود / Ref (يجب أن يكون فريداً):</label><input id="pRef" placeholder="أدخل أو امسح الباركود" oninput="checkRefUniqueness()"></div>
            <div><label>اسم المنتج:</label><input id="pName" placeholder="اسم المنتج بالكامل"></div>
        </div>
        <div class="flex-inputs">
            <div><label>سعر الشراء (DA):</label><input id="pBuy" type="number" step="0.01" placeholder="0.00" oninput="checkPriceValidity()"></div>
            <div><label>سعر البيع الافتراضي (DA):</label><input id="pSell" type="number" step="0.01" placeholder="0.00" oninput="checkPriceValidity()"></div>
            <div><label>الكمية الابتدائية:</label><input id="pQty" type="number" step="0.01" placeholder="0"></div>
        </div>
        <button onclick="addProduct()" style="width: 100%; margin-top: 5px; background: var(--success-gradient); height: 50px;"><i class="fa-solid fa-plus"></i> إضافة المنتج للمخزن</button>
    </div>
    <div style="margin-top: 25px; margin-bottom: 10px;">
        <label>🔍 بحث ترتيبي من الحرف الأول فصاعداً:</label>
        <input id="productSearch" placeholder="ابحث باسم المنتج أو الرقم المتسلسل..." oninput="renderProducts()">
    </div>
    <div style="overflow-x: auto;">
        <table>
            <thead><tr><th>الباركود</th><th>اسم المنتج</th><th>الكمية الحالية</th><th>الشراء (DA)</th><th>البيع الافتراضي (DA)</th><th>تعديل</th><th>حذف</th></tr></thead>
            <tbody id="productTable"></tbody>
        </table>
    </div>
</div>

<div id="sales" class="page" style="max-width: 1300px;">
    <div class="header">
        <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع للرئيسية</button>
        <h2><i class="fa-solid fa-cash-register" style="color:var(--primary);"></i> واجهة البيع السريعة والتعديل الفوري</h2>
    </div>
    
    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-bottom: 25px;">
        <div class="box" style="background: #111827; color: white; padding: 15px; margin: 0; display: flex; align-items: center; justify-content: space-around; flex-wrap: wrap; border-color: rgba(255,255,255,0.05);">
            <span style="font-weight: 700; font-size: 16px;"><i class="fa-solid fa-receipt"></i> رقم الطلب الحالي:</span>
            <input id="cmdNumberInput" type="number" min="1" style="width: 110px; text-align: center; font-size: 18px; font-weight: 800; color: #fff; background: #1f2937; padding: 8px;" oninput="updateCommandNumberManual()">
            <button class="del" onclick="resetCommandNumber()" style="padding: 10px 16px; font-size: 13px;"><i class="fa-solid fa-arrow-rotate-left"></i> تصفير</button>
        </div>
        <div class="box" style="background: rgba(59, 130, 246, 0.05); border: 1px solid rgba(59, 130, 246, 0.2); padding: 15px; margin: 0; display: flex; align-items: center; gap: 15px;">
            <input id="searchOrderNumber" type="number" placeholder="رقم طلبية سابقة لتعديلها..." style="background: #1f2937;">
            <button onclick="loadOrderToEdit()" style="background: var(--purple-gradient); white-space: nowrap; padding: 14px 20px;"><i class="fa-solid fa-edit"></i> جلب للتعديل</button>
        </div>
    </div>

    <div class="sales-grid">
        <div>
            <div class="box" style="background: rgba(17, 24, 39, 0.6);">
                <h3 style="font-size: 17px; margin-bottom: 20px; color: var(--primary);"><i class="fa-solid fa-filter"></i> اختيار المنتج وتحديد السعر</h3>
                <div style="margin-bottom: 18px;">
                    <label>فصل وتصفية المنتجات الحرفية:</label>
                    <input id="saleSearch" placeholder="اكتب الحرف الأول فالثاني أو امسح الباركود..." oninput="renderSalesOptions()">
                </div>
                <div style="margin-bottom: 18px;">
                    <label>المنتج المستهدف حالياً:</label>
                    <select id="saleStock" onchange="updateDefaultSalePriceField()"></select>
                </div>
                
                <div class="flex-inputs">
                    <div>
                        <label>الكمية المراد بيعها:</label>
                        <input id="saleQty" type="number" step="1" value="1">
                    </div>
                    <div>
                        <label style="color: var(--primary); font-weight: 800;"><i class="fa-solid fa-pen-clip"></i> سعر البيع الحالي (عدّله بحرية):</label>
                        <input id="salePriceInput" type="number" step="0.01" style="border: 2px solid var(--primary); font-size: 17px; font-weight: 700; color: #fff; background:#111827;">
                    </div>
                </div>
                <button onclick="addToCommand()" style="width: 100%; height: 52px; font-size: 16px; background: var(--primary-gradient);"><i class="fa-solid fa-cart-plus"></i> إضافة إلى السلة الحالية</button>
            </div>
            
            <h3 style="color: var(--text-main); font-weight:700; font-size: 17px; margin-bottom: 15px;"><i class="fa-solid fa-clock-rotate-left"></i> سجل الطلبيات المبيوعة السابقة</h3>
            <div id="salesLog" style="max-height: 400px; overflow-y: auto;"></div>
        </div>

        <div class="box" style="background: rgba(31, 41, 55, 0.6); border: 1px solid rgba(16, 185, 129, 0.3); position: sticky; top: 20px;">
            <h3 style="margin-bottom: 20px; border-bottom: 1px solid var(--border); padding-bottom: 12px; font-size: 17px; color: var(--success);"><i class="fa-solid fa-basket-shopping"></i> سلة التسوق الحالية</h3>
            <div id="currentCommand" style="min-height: 160px; max-height: 320px; overflow-y: auto; margin-bottom: 20px;"></div>
            
            <div style="background: rgba(16, 185, 129, 0.05); padding: 20px; border-radius: var(--radius-md); border: 1px solid rgba(16, 185, 129, 0.2); text-align: left; margin-bottom: 20px;">
                <span style="color: var(--success); font-size: 15px; font-weight: 700;">المجموع الإجمالي المستحق:</span>
                <h3 id="commandTotal" style="color: var(--success); font-size: 28px; font-weight: 900; margin-top: 5px;">0.00 DA</h3>
            </div>
            <button onclick="confirmCommand()" style="width:100%; background: var(--success-gradient); font-size: 17px; padding: 16px; box-shadow: 0 4px 15px rgba(16, 185, 129, 0.2);"><i class="fa-solid fa-circle-check"></i> تأكيد وحفظ الطلب النهائي</button>
        </div>
    </div>
</div>

<div id="stock" class="page">
    <div class="header">
        <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع للرئيسية</button>
        <h2><i class="fa-solid fa-warehouse" style="color:var(--primary);"></i> كشف وجرد المخزون الكلي</h2>
    </div>

    <div class="profit-grid" style="margin-top: 0; margin-bottom: 30px;">
        <div class="profit-card" style="border-right-color: var(--primary);">
            <p>📦 إجمالي السلع المتوفرة بالمخزن</p>
            <div id="topStockPieces" class="amount" style="color: #60a5fa;">0 قطعة</div>
        </div>
        <div class="profit-card" style="border-right-color: var(--danger);">
            <p>💰 إجمالي رأس المال المستثمر (الشراء)</p>
            <div id="topStockCapital" class="amount" style="color: #fca5a5;">0.00 DA</div>
        </div>
        <div class="profit-card success" style="border-right-color: var(--success);">
            <p>📈 صافي الأرباح المتوقعة عند البيع</p>
            <div id="topStockProfit" class="amount" style="color: var(--success);">0.00 DA</div>
        </div>
    </div>

    <div style="overflow-x: auto;">
        <table>
            <thead><tr><th>اسم المنتج</th><th>القطع المتبقية</th><th>رأس المال المستثمر</th><th>الأرباح المتوقعة</th><th>إجراء</th></tr></thead>
            <tbody id="stockTable"></tbody>
            <tfoot id="stockTableFoot"></tfoot>
        </table>
    </div>
</div>

<div id="low" class="page">
    <div class="header">
        <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع للرئيسية</button>
        <h2><i class="fa-solid fa-triangle-exclamation" style="color:var(--warning);"></i> السلع الناقصة بالمحل (مرتبة تصاعدياً بحسب درجة الخطورة 1-15)</h2>
    </div>
    <div style="overflow-x: auto;">
        <table>
            <thead>
                <tr>
                    <th>الباركود / Ref</th>
                    <th>اسم المنتج</th>
                    <th>الكمية المتبقية</th>
                    <th>سعر الشراء (DA)</th>
                    <th>مستوى درجة الخطورة</th>
                    <th>طبيعة وحالة التنبيه الفوري</th>
                </tr>
            </thead>
            <tbody id="lowTable"></tbody>
        </table>
    </div>
</div>

<div id="expenses" class="page">
    <div class="header">
        <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع للرئيسية</button>
        <h2><i class="fa-solid fa-hand-holding-dollar" style="color:var(--danger);"></i> إدارة مصاريف المحل الكلية 💸</h2>
    </div>
    <div class="box">
        <h3 style="margin-bottom: 20px; font-size:17px;"><i class="fa-solid fa-file-invoice-dollar"></i> تسجيل مصروف جديد وتدوينه</h3>
        <div style="margin-bottom: 18px;">
            <label>بيان المصروف ونوعه:</label>
            <input id="expTitle" placeholder="مثال: فاتورة الكهرباء، نقل السلعة، تالف...">
        </div>
        <div class="flex-inputs">
            <div><label>قيمة المصروف (DA):</label><input id="expAmount" type="number" step="0.01" placeholder="0.00"></div>
            <div><label>تاريخ التقييد:</label><input id="expDate" type="date"></div>
        </div>
        <button onclick="addExpense()" style="width: 100%; margin-top: 5px; background: var(--danger-gradient); height: 50px;"><i class="fa-solid fa-check"></i> حفظ وقيد المصروف بالدفتر</button>
    </div>
    <h3 style="color: var(--text-main); font-weight:700; margin-top:30px; font-size: 17px;"><i class="fa-solid fa-receipt"></i> سجل المصاريف اليومية والسنوية المقيدة</h3>
    <div id="expensesLog" style="max-height: 420px; overflow-y: auto; margin-top: 20px;"></div>
</div>

<div id="profits" class="page">
    <div class="header">
        <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع للرئيسية</button>
        <h2><i class="fa-solid fa-chart-line" style="color:var(--success);"></i> التقارير المالية والأرباح الصافية الحقيقية</h2>
    </div>
    <div class="box" style="background: rgba(17, 24, 39, 0.6);">
        <h3 style="margin-bottom: 20px; font-size:17px; color: #a855f7;"><i class="fa-solid fa-calendar-days"></i> فرز واحتساب الأرباح بفترة زمنية مخصصة 🗓️</h3>
        <div class="flex-inputs">
            <div><label>من تاريخ 📅:</label><input type="date" id="filterFrom" onchange="calculateFilteredProfit(); calculateDynamicNetSection();"></div>
            <div><label>إلى تاريخ 🏁:</label><input type="date" id="filterTo" onchange="calculateFilteredProfit(); calculateDynamicNetSection();"></div>
        </div>
    </div>
    <div class="profit-grid">
        <div class="profit-card filter" style="grid-column: span 2 / span 2;">
            <p>🎯 صافي فائدة الفترة المحددة بالفرز أعلاه (فائدة المبيعات المعدلة - المصاريف)</p>
            <div id="filteredProfit" class="amount" style="color: #c084fc;">0.00 DA 💰</div>
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
            <p>📉 إجمالي مصاريف السنة المسجلة بالكامل</p>
            <div id="totalExpensesYear" class="amount" style="color: #fca5a5;">0.00 DA 💸</div>
        </div>
        <div class="profit-card dark" style="grid-column: span 2 / span 2;">
            <p>👑 صافي فائدة السنة الإجمالية الحقيقية</p>
            <div id="yearlyProfit" class="amount" style="color: var(--text-main);">0.00 DA</div>
        </div>
    </div>

    <!-- قسم حساب الفائدة الصافية الجديد (Net Profit Section) -->
    <h3 style="color: var(--text-main); font-weight:700; margin-top:40px; font-size: 19px;"><i class="fa-solid fa-calculator" style="color: var(--primary);"></i> حساب الفائدة الصافية التلقائي الحصري (المبلغ المرجعي 14,900)</h3>
    <div style="overflow-x: auto; margin-top: 15px;">
        <table>
            <thead>
                <tr>
                    <th>البيان المالي</th>
                    <th>طريقة وآلية الحساب الرياضي</th>
                    <th>القيمة الحالية (DA)</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td><strong>المبلغ المرجعي الثابت</strong></td>
                    <td>قيمة أساسية ثابتة للنظام</td>
                    <td>14,900.00</td>
                </tr>
                <tr>
                    <td><strong>إجمالي المبيعات (المستحق)</strong></td>
                    <td>مجموع الطلبيات للفترة المحددة بالفرز أعلاه</td>
                    <td id="netSectionSales">0.00</td>
                </tr>
                <tr>
                    <td><strong>إجمالي المصاريف</strong></td>
                    <td>مجموع المصاريف المقيدة للفترة المحددة بالفرز أعلاه</td>
                    <td id="netSectionExpenses">0.00</td>
                </tr>
                <tr class="net-profit-section">
                    <td><strong>الفائدة الصافية النهائية</strong></td>
                    <td>14900 - الإجمالي المستحق - المصاريف</td>
                    <td id="netSectionFinalResult" class="highlight-neon">14,900.00</td>
                </tr>
            </tbody>
        </table>
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
    if(id === 'sales') { 
        let sSearch = document.getElementById('saleSearch');
        sSearch.value = ''; 
        renderSalesOptions(); 
        setTimeout(() => sSearch.focus(), 100);
    }
    if(id === 'low') { renderLowStockPage(); }
    if(id === 'profits') { calculateDynamicNetSection(); }
    window.scrollTo(0, 0);
}

function back(){ document.getElementById("dashboard").style.display="grid"; document.querySelectorAll(".page").forEach(p=>p.classList.remove("active")); }

function playBeepSound() {
    try {
        let audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        let oscillator = audioCtx.createOscillator();
        let gainNode = audioCtx.createGain();
        oscillator.type = 'sine';
        oscillator.frequency.setValueAtTime(1100, audioCtx.currentTime);
        gainNode.gain.setValueAtTime(0.15, audioCtx.currentTime);
        oscillator.connect(gainNode);
        gainNode.connect(audioCtx.destination);
        oscillator.start(); oscillator.stop(audioCtx.currentTime + 0.1);
    } catch (e) { console.log("Audio error"); }
}

function playErrorSound() {
    try {
        let audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        let now = audioCtx.currentTime;
        let osc = audioCtx.createOscillator();
        let gain = audioCtx.createGain();
        osc.type = 'sawtooth';
        osc.frequency.setValueAtTime(150, now);
        osc.frequency.linearRampToValueAtTime(80, now + 0.3);
        gain.gain.setValueAtTime(0.3, now);
        gain.gain.exponentialRampToValueAtTime(0.01, now + 0.3);
        osc.connect(gain);
        gain.connect(audioCtx.destination);
        osc.start(now); osc.stop(now + 0.3);
    } catch (e) { console.log("Audio error"); }
}

function playCashRegisterSound() {
    try {
        let AudioContext = window.AudioContext || window.webkitAudioContext;
        let ctx = new AudioContext();
        let now = ctx.currentTime;
        
        let osc1 = ctx.createOscillator();
        let gain1 = ctx.createGain();
        osc1.type = 'sine';
        osc1.frequency.setValueAtTime(1400, now);
        gain1.gain.setValueAtTime(0.25, now);
        gain1.gain.exponentialRampToValueAtTime(0.001, now + 0.4);
        osc1.connect(gain1); gain1.connect(ctx.destination);
        osc1.start(now); osc1.stop(now + 0.4);
        
        let osc2 = ctx.createOscillator();
        let gain2 = ctx.createGain();
        osc2.type = 'triangle';
        osc2.frequency.setValueAtTime(880, now + 0.02);
        gain2.gain.setValueAtTime(0.15, now + 0.02);
        gain2.gain.exponentialRampToValueAtTime(0.001, now + 0.3);
        osc2.connect(gain2); gain2.connect(ctx.destination);
        osc2.start(now + 0.02); osc2.stop(now + 0.3);
    } catch (e) { console.log("Cash sound error: ", e); }
}

function checkRefUniqueness() {
    let refField = document.getElementById('pRef');
    let refVal = refField.value.trim();
    if(!refVal) { refField.classList.remove('input-error'); return; }
    let isDuplicate = batches.some(b => b.ref === refVal);
    if(isDuplicate) { refField.classList.add('input-error'); } else { refField.classList.remove('input-error'); }
}

function checkPriceValidity() {
    let buyField = document.getElementById('pBuy');
    let sellField = document.getElementById('pSell');
    let buyVal = Number(buyField.value) || 0;
    let sellVal = Number(sellField.value) || 0;
    if(sellField.value !== "" && sellVal < buyVal) { sellField.classList.add('input-error'); } else { sellField.classList.remove('input-error'); }
}

function updateDefaultSalePriceField(){
    let saleStock = document.getElementById('saleStock');
    if(!saleStock.value) return;
    let b = batches.find(x => x.id === Number(saleStock.value));
    if(b) { document.getElementById('salePriceInput').value = b.sell; }
}

function updateCommandNumberManual() {
    let inputVal = document.getElementById('cmdNumberInput').value;
    if(inputVal && Number(inputVal) >= 1) {
        commandNumber = Math.floor(Number(inputVal));
        localStorage.setItem("commandNumber", commandNumber);
    }
}

function resetCommandNumber() {
    if(confirm("هل أنت متأكد من تصفير عداد الطلبيات والبدء من 1؟")) {
        commandNumber = 1; document.getElementById('cmdNumberInput').value = commandNumber; save();
    }
}

function loadOrderToEdit() {
    let orderNum = Number(document.getElementById('searchOrderNumber').value);
    if(!orderNum || orderNum < 1) return alert("يرجى إدخال رقم طلبية صحيح لجلبه.");
    let orderItems = sales.filter(x => x.command === orderNum);
    if(orderItems.length === 0) return alert("لم يتم العثور على أي طلبية تحمل الرقم #" + orderNum);
    if(currentCommandData.length > 0) {
        if(!confirm("السلة الحالية تحتوي على منتجات، هل تريد تفريغها وجلب الطلبية القديمة للتعديل؟")) return;
    }

    currentCommandData = [];
    orderItems.forEach(item => {
        currentCommandData.push({
            ref: item.ref,
            name: item.name,
            qty: item.qty,
            sellPrice: item.sellPrice,
            buyPrice: item.buyPrice
        });
    });

    commandNumber = orderNum;
    document.getElementById('cmdNumberInput').value = commandNumber;
    sales = sales.filter(x => x.command !== orderNum);
    
    renderCurrentCommand();
    renderSalesLog();
    calculateProfitPage();
    calculateDynamicNetSection();
    alert("تم جلب عناصر الطلبية رقم #" + orderNum + " بنجاح إلى السلة وجاهزة للتعديل الصارم!");
}

/* ================= دالات إدارة السلع والمنتجات ================= */
function addProduct() {
    let ref = document.getElementById('pRef').value.trim();
    let name = document.getElementById('pName').value.trim();
    let buy = Number(document.getElementById('pBuy').value) || 0;
    let sell = Number(document.getElementById('pSell').value) || 0;
    let qty = Number(document.getElementById('pQty').value) || 0;

    if (!ref || !name || qty < 0) { playErrorSound(); return alert("يرجى ملء الباركود واسم المنتج بشكل صحيح."); }
    if (batches.some(b => b.ref === ref)) { playErrorSound(); return alert("خطأ: كود الباركود هذا مكرر بالفعل لسلعة أخرى!"); }
    if (sell < buy) { playErrorSound(); if(!confirm("تنبيه: سعر البيع أقل من سعر الشراء (خسارة)، هل تريد الاستمرار على أي حال؟")) return; }

    let item = { id: Date.now(), ref, name, buy, sell, qty };
    batches.push(item);
    save();
    
    document.getElementById('pRef').value = "";
    document.getElementById('pName').value = "";
    document.getElementById('pBuy').value = "";
    document.getElementById('pSell').value = "";
    document.getElementById('pQty').value = "";
    
    render();
    playBeepSound();
}

function deleteProduct(id) {
    if(confirm("هل أنت متأكد تماماً من حذف هذا المنتج كلياً من السجلات؟")) {
        batches = batches.filter(b => b.id !== id);
        save();
        render();
    }
}

function editProductInline(id) {
    let b = batches.find(x => x.id === id);
    if(!b) return;
    let newName = prompt("تعديل اسم المنتج:", b.name);
    if(newName === null) return;
    let newQty = prompt("تعديل الكمية المتوفرة:", b.qty);
    if(newQty === null) return;
    let newBuy = prompt("تعديل سعر الشراء (DA):", b.buy);
    if(newBuy === null) return;
    let newSell = prompt("تعديل سعر البيع الافتراضي (DA):", b.sell);
    if(newSell === null) return;

    b.name = newName.trim() || b.name;
    b.qty = parseFloat(newQty) >= 0 ? parseFloat(newQty) : b.qty;
    b.buy = parseFloat(newBuy) >= 0 ? parseFloat(newBuy) : b.buy;
    b.sell = parseFloat(newSell) >= 0 ? parseFloat(newSell) : b.sell;

    save();
    render();
    playBeepSound();
}

/* ================= عمليات واجهة البيع السريع والسلة ================= */
function renderSalesOptions() {
    let searchVal = document.getElementById('saleSearch').value.toLowerCase().trim();
    let select = document.getElementById('saleStock');
    select.innerHTML = "";

    let filtered = batches;
    if(searchVal) {
        filtered = batches.filter(b => b.name.toLowerCase().includes(searchVal) || b.ref.toLowerCase().includes(searchVal));
    }

    if(filtered.length === 0) {
        let opt = document.createElement('option');
        opt.text = "لم يتم العثور على نتائج متطابقة...";
        opt.value = "";
        select.appendChild(opt);
        document.getElementById('salePriceInput').value = "";
        return;
    }

    filtered.forEach(b => {
        let opt = document.createElement('option');
        opt.value = b.id;
        opt.text = `${b.name} [الباركود: ${b.ref}] (المتاح: ${b.qty})`;
        select.appendChild(opt);
    });

    updateDefaultSalePriceField();

    if(searchVal && filtered.length === 1 && filtered[0].ref.toLowerCase() === searchVal) {
        addToCommand();
        document.getElementById('saleSearch').value = '';
        renderSalesOptions();
    }
}

function addToCommand() {
    let select = document.getElementById('saleStock');
    if(!select.value) return;
    
    let b = batches.find(x => x.id === Number(select.value));
    if(!b) return;

    let saleQty = parseFloat(document.getElementById('saleQty').value) || 0;
    let salePrice = parseFloat(document.getElementById('salePriceInput').value) || 0;

    if(saleQty <= 0) { playErrorSound(); return alert("يرجى تحديد كمية بيع صحيحة أكبر من الصفر."); }
    
    let existing = currentCommandData.find(x => x.ref === b.ref && x.sellPrice === salePrice);
    if(existing) {
        existing.qty += saleQty;
    } else {
        currentCommandData.push({
            ref: b.ref,
            name: b.name,
            qty: saleQty,
            sellPrice: salePrice,
            buyPrice: b.buy
        });
    }

    renderCurrentCommand();
    playBeepSound();
    document.getElementById('saleQty').value = "1";
}

function removeFromCurrentCommand(index) {
    currentCommandData.splice(index, 1);
    renderCurrentCommand();
    playBeepSound();
}

function renderCurrentCommand() {
    let container = document.getElementById('currentCommand');
    container.innerHTML = "";
    let total = 0;

    currentCommandData.forEach((item, index) => {
        let itemTotal = item.qty * item.sellPrice;
        total += itemTotal;

        let div = document.createElement('div');
        div.className = "order-item-line";
        div.innerHTML = `
            <div>
                <button class="del" onclick="removeFromCurrentCommand(${index})" style="padding:4px 8px; font-size:11px; margin-left:8px;"><i class="fa-solid fa-trash"></i></button>
                <span><strong>${item.name}</strong></span>
                <span class="badge-qty" style="margin-right:10px;">${item.qty} قطعة</span>
            </div>
            <div>
                <span>${item.sellPrice.toFixed(2)} × ${item.qty} = <strong>${itemTotal.toFixed(2)} DA</strong></span>
            </div>
        `;
        container.appendChild(div);
    });

    document.getElementById('commandTotal').innerText = total.toFixed(2) + " DA";
}

function confirmCommand() {
    if(currentCommandData.length === 0) { playErrorSound(); return alert("سلة التسوق فارغة تماماً! لا يمكن حفظ طلبية فارغة."); }

    let todayStr = new Date().toISOString().split('T')[0];

    currentCommandData.forEach(item => {
        let b = batches.find(x => x.ref === item.ref);
        if(b) {
            b.qty = Math.max(0, b.qty - item.qty);
        }
        
        sales.push({
            id: Date.now() + Math.random(),
            command: commandNumber,
            ref: item.ref,
            name: item.name,
            qty: item.qty,
            buyPrice: item.buyPrice,
            sellPrice: item.sellPrice,
            date: todayStr
        });
    });

    commandNumber++;
    document.getElementById('cmdNumberInput').value = commandNumber;
    
    currentCommandData = [];
    save();
    render();
    playCashRegisterSound();
    alert("تم تأكيد، ترحيل، وحفظ الطلبية المبيوعة بنجاح وتحديث كميات المخزن!");
}

/* ================= دالات إدارة وقيد المصاريف ================= */
function addExpense() {
    let title = document.getElementById('expTitle').value.trim();
    let amount = Number(document.getElementById('expAmount').value) || 0;
    let date = document.getElementById('expDate').value;

    if(!title || amount <= 0 || !date) { playErrorSound(); return alert("يرجى تدوين بيان المصروف وقيمته الحقيقية بشكل صحيح."); }

    expenses.push({ id: Date.now(), title, amount, date });
    save();
    
    document.getElementById('expTitle').value = "";
    document.getElementById('expAmount').value = "";
    
    render();
    playBeepSound();
}

function deleteExpense(id) {
    if(confirm("هل أنت متأكد من حذف قيد هذا المصروف؟")) {
        expenses = expenses.filter(x => x.id !== id);
        save();
        render();
    }
}

/* ================= حسابات وقسم الفائدة الصافية الديناميكية المطور ================= */
function calculateDynamicNetSection() {
    let fromDate = document.getElementById('filterFrom').value;
    let toDate = document.getElementById('filterTo').value;

    if (!fromDate || !toDate) return;

    let filteredSales = sales.filter(s => s.date >= fromDate && s.date <= toDate);
    let totalSalesAmt = filteredSales.reduce((sum, s) => sum + (s.qty * s.sellPrice), 0);

    let filteredExpenses = expenses.filter(e => e.date >= fromDate && e.date <= toDate);
    let totalExpensesAmt = filteredExpenses.reduce((sum, e) => sum + e.amount, 0);

    const baseAmount = 14900;
    let finalNetProfit = baseAmount - totalSalesAmt - totalExpensesAmt;

    document.getElementById('netSectionSales').innerText = totalSalesAmt.toLocaleString(undefined, {minimumFractionDigits: 2, maximumFractionDigits: 2});
    document.getElementById('netSectionExpenses').innerText = totalExpensesAmt.toLocaleString(undefined, {minimumFractionDigits: 2, maximumFractionDigits: 2});
    document.getElementById('netSectionFinalResult').innerText = finalNetProfit.toLocaleString(undefined, {minimumFractionDigits: 2, maximumFractionDigits: 2}) + " DA";
}

function calculateFilteredProfit() {
    let from = document.getElementById('filterFrom').value;
    let to = document.getElementById('filterTo').value;
    if(!from || !to) return;

    let fSales = sales.filter(s => s.date >= from && s.date <= to);
    let fExpenses = expenses.filter(e => e.date >= from && e.date <= to);

    let salesProfit = fSales.reduce((sum, s) => sum + ((s.sellPrice - s.buyPrice) * s.qty), 0);
    let totalExp = fExpenses.reduce((sum, e) => sum + e.amount, 0);

    document.getElementById('filteredProfit').innerText = (salesProfit - totalExp).toFixed(2) + " DA 💰";
}

function calculateProfitPage() {
    let todayStr = new Date().toISOString().split('T')[0];
    let thisMonthStr = todayStr.substring(0, 7);
    let thisYearStr = todayStr.substring(0, 4);

    let dSales = sales.filter(s => s.date === todayStr);
    let dExpenses = expenses.filter(e => e.date === todayStr);
    let dProfit = dSales.reduce((sum, s) => sum + ((s.sellPrice - s.buyPrice) * s.qty), 0) - dExpenses.reduce((sum, e) => sum + e.amount, 0);
    document.getElementById('dailyProfit').innerText = dProfit.toFixed(2) + " DA";

    let mSales = sales.filter(s => s.date.startsWith(thisMonthStr));
    let mExpenses = expenses.filter(e => e.date.startsWith(thisMonthStr));
    let mProfit = mSales.reduce((sum, s) => sum + ((s.sellPrice - s.buyPrice) * s.qty), 0) - mExpenses.reduce((sum, e) => sum + e.amount, 0);
    document.getElementById('monthlyProfit').innerText = mProfit.toFixed(2) + " DA";

    let yExpenses = expenses.filter(e => e.date.startsWith(thisYearStr));
    let yExpensesTotal = yExpenses.reduce((sum, e) => sum + e.amount, 0);
    document.getElementById('totalExpensesYear').innerText = yExpensesTotal.toFixed(2) + " DA 💸";

    let ySales = sales.filter(s => s.date.startsWith(thisYearStr));
    let yProfit = ySales.reduce((sum, s) => sum + ((s.sellPrice - s.buyPrice) * s.qty), 0) - yExpensesTotal;
    document.getElementById('yearlyProfit').innerText = yProfit.toFixed(2) + " DA";

    calculateFilteredProfit();
}

/* ================= دالات الـ RENDER وعرض الواجهات الجرافيكية ================= */
function renderProducts() {
    let tbody = document.getElementById('productTable');
    tbody.innerHTML = "";
    let searchVal = document.getElementById('productSearch').value.toLowerCase().trim();

    let filtered = batches;
    if(searchVal) {
        filtered = batches.filter(b => b.name.toLowerCase().includes(searchVal) || b.ref.toLowerCase().includes(searchVal));
    }

    filtered.forEach(b => {
        let tr = document.createElement('tr');
        tr.innerHTML = `
            <td><code>${b.ref}</code></td>
            <td>${b.name}</td>
            <td style="color:${b.qty <= 3 ? '#ef4444':'#10b981'}; font-weight:800;">${b.qty}</td>
            <td>${b.buy.toFixed(2)}</td>
            <td>${b.sell.toFixed(2)}</td>
            <td><button class="edit" onclick="editProductInline(${b.id})"><i class="fa-solid fa-pen"></i> تعديل</button></td>
            <td><button class="del" onclick="deleteProduct(${b.id})"><i class="fa-solid fa-trash"></i> حذف</button></td>
        `;
        tbody.appendChild(tr);
    });
}

function renderSalesLog() {
    let container = document.getElementById('salesLog');
    container.innerHTML = "";

    let groups = {};
    sales.forEach(s => {
        if(!groups[s.command]) groups[s.command] = [];
        groups[s.command].push(s);
    });

    let sortedCommands = Object.keys(groups).sort((a,b) => b - a);

    if(sortedCommands.length === 0) {
        container.innerHTML = "<p style='color:var(--text-muted); text-align:center; padding:20px;'>لا توجد طلبيات سابقة مسجلة في السجل بعد...</p>";
        return;
    }

    sortedCommands.forEach(cmdNum => {
        let items = groups[cmdNum];
        let date = items[0].date;
        let cmdTotal = items.reduce((sum, item) => sum + (item.qty * item.sellPrice), 0);

        let card = document.createElement('div');
        card.className = "order-card";
        
        let itemsHtml = items.map(i => `
            <div style="display:flex; justify-content:space-between; font-size:13px; color:var(--text-muted); margin-top:5px;">
                <span>• ${i.name} (${i.qty} قطعة)</span>
                <span>${(i.qty * i.sellPrice).toFixed(2)} DA</span>
            </div>
        `).join('');

        card.innerHTML = `
            <div class="order-card-header">
                <span style="font-weight:800; color:var(--primary);">طلب #${cmdNum}</span>
                <span style="font-size:12px; color:var(--text-muted);"><i class="fa-solid fa-calendar"></i> ${date}</span>
            </div>
            ${itemsHtml}
            <div style="display:flex; justify-content:space-between; align-items:center; margin-top:12px; border-top:1px solid rgba(255,255,255,0.05); padding-top:10px;">
                <span style="font-size:14px; font-weight:700; color:var(--success);">المجموع: ${cmdTotal.toFixed(2)} DA</span>
                <button onclick="deleteEntireOrder(${cmdNum})" class="del" style="padding:6px 12px; font-size:11px;"><i class="fa-solid fa-trash-can"></i> إلغاء الطلب</button>
            </div>
        `;
        container.appendChild(card);
    });
}

/* التعديل الجوهري المطلوب: إعادة السلع للمخزن تلقائياً عند حذف الكوموند */
function deleteEntireOrder(cmdNum) {
    if(confirm(`هل أنت متأكد من إلغاء وحذف الطلبية رقم #${cmdNum} بالكامل؟ (سيتم استرجاع جميع الكميات المبيوعة إلى المخزن تلقائياً)`)) {
        let orderItems = sales.filter(x => x.command === cmdNum);
        
        // جرد العناصر المبيوعة وإعادتها خطوة بخطوة إلى المخزن الأصلي
        orderItems.forEach(item => {
            let b = batches.find(x => x.ref === item.ref);
            if(b) {
                b.qty = b.qty + item.qty; // إضافة الكمية الملغاة مجدداً للمخزن
            }
        });

        // مسح الطلب من جدول المبيعات
        sales = sales.filter(x => x.command !== cmdNum);
        save();
        render();
        playBeepSound();
    }
}

function renderStockPage() {
    let tbody = document.getElementById('stockTable');
    let tfoot = document.getElementById('stockTableFoot');
    tbody.innerHTML = "";

    let totalPieces = 0;
    let totalCapital = 0;
    let totalExpectedProfit = 0;

    batches.forEach(b => {
        let capital = b.qty * b.buy;
        let expectedProfit = (b.sell - b.buy) * b.qty;

        totalPieces += b.qty;
        totalCapital += capital;
        totalExpectedProfit += expectedProfit;

        let tr = document.createElement('tr');
        tr.innerHTML = `
            <td><strong>${b.name}</strong></td>
            <td>${b.qty} قطعة</td>
            <td>${capital.toFixed(2)} DA</td>
            <td style="color:var(--success);">${expectedProfit.toFixed(2)} DA</td>
            <td><button class="edit" onclick="openPage('products'); document.getElementById('productSearch').value='${b.ref}'; renderProducts();" style="padding:6px 12px; font-size:12px;"><i class="fa-solid fa-eye"></i> معاينة</button></td>
        `;
        tbody.appendChild(tr);
    });

    document.getElementById('topStockPieces').innerText = totalPieces + " قطعة";
    document.getElementById('topStockCapital').innerText = totalCapital.toFixed(2) + " DA";
    document.getElementById('topStockProfit').innerText = totalExpectedProfit.toFixed(2) + " DA";

    tfoot.innerHTML = `
        <tr style="background:#111827; font-weight:bold;">
            <td>إجمالي المحل الكلي</td>
            <td>${totalPieces} قطعة</td>
            <td>${totalCapital.toFixed(2)} DA</td>
            <td style="color:var(--success);">${totalExpectedProfit.toFixed(2)} DA</td>
            <td>---</td>
        </tr>
    `;
}

function renderLowStockPage() {
    let tbody = document.getElementById('lowTable');
    tbody.innerHTML = "";

    let lowItems = batches.filter(b => b.qty <= 5);

    lowItems.forEach(item => {
        let baseRisk = Math.ceil(5 - item.qty);
        let riskLevel = Math.max(1, Math.min(15, baseRisk * 3));
        item.calculatedRisk = riskLevel;
    });

    lowItems.sort((a,b) => b.calculatedRisk - a.calculatedRisk);

    if(lowItems.length === 0) {
        tbody.innerHTML = `<tr><td colspan="6" style="text-align:center; color:var(--success); padding:30px; font-weight:bold;"><i class="fa-solid fa-check-circle"></i> المخزن ممتاز! لا توجد أي سلع ناقصة حالياً بالمحل.</td></tr>`;
        return;
    }

    lowItems.forEach(b => {
        let badgeColor = "var(--success-gradient)";
        let statusText = "آمن حالياً";
        
        if(b.calculatedRisk >= 11) { badgeColor = "var(--danger-gradient)"; statusText = "خطر شديد / تموين فوري 🚨"; }
        else if(b.calculatedRisk >= 6) { badgeColor = "var(--warning-gradient)"; statusText = "نقص متوسط / حرج"; }

        let tr = document.createElement('tr');
        tr.innerHTML = `
            <td><code>${b.ref}</code></td>
            <td><strong>${b.name}</strong></td>
            <td style="color:var(--danger); font-weight:900; font-size:16px;">${b.qty} قطعة متبقية</td>
            <td>${b.buy.toFixed(2)} DA</td>
            <td><span class="risk-badge" style="background:${badgeColor}; color:white;">المستوى ${b.calculatedRisk} / 15</span></td>
            <td style="font-weight:700;">${statusText}</td>
        `;
        tbody.appendChild(tr);
    });
}

function renderExpensesPage() {
    let container = document.getElementById('expensesLog');
    container.innerHTML = "";

    if(expenses.length === 0) {
        container.innerHTML = "<p style='color:var(--text-muted); text-align:center; padding:20px;'>سجل المصاريف فارغ ونظيف بالكامل...</p>";
        return;
    }

    let sortedExp = [...expenses].sort((a,b) => new Date(b.date) - new Date(a.date));

    let tableHtml = `
        <table>
            <thead><tr><th>بيان المصروف ونوعه</th><th>القيمة المستهلكة</th><th>تاريخ القيد</th><th>إجراء</th></tr></thead>
            <tbody>
    `;

    sortedExp.forEach(e => {
        tableHtml += `
            <tr>
                <td><strong>${e.title}</strong></td>
                <td style="color:var(--danger); font-weight:700;">${e.amount.toFixed(2)} DA</td>
                <td><i class="fa-solid fa-calendar-day"></i> ${e.date}</td>
                <td><button class="del" onclick="deleteExpense(${e.id})" style="padding:6px 12px; font-size:12px;"><i class="fa-solid fa-trash"></i> حذف</button></td>
            </tr>
        `;
    });

    tableHtml += `</tbody></table>`;
    container.innerHTML = tableHtml;
}

function render() {
    document.getElementById('cmdNumberInput').value = commandNumber;
    renderProducts();
    renderSalesOptions();
    renderCurrentCommand();
    renderSalesLog();
    renderStockPage();
    renderExpensesPage();
    calculateProfitPage();
    calculateDynamicNetSection();
}

/* ================= دالات الاستيراد والتصدير الاحتياطي (JSON) ================= */
function exportData() {
    let dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify({
        batches, sales, expenses, commandNumber
    }));
    let downloadAnchor = document.createElement('a');
    downloadAnchor.setAttribute("href", dataStr);
    downloadAnchor.setAttribute("download", `POS_SYSTEM_BACKUP_${new Date().toISOString().split('T')[0]}.json`);
    document.body.appendChild(downloadAnchor);
    downloadAnchor.click();
    downloadAnchor.remove();
}

function triggerImport() { document.getElementById('importFileInput').click(); }

function importData(event) {
    let file = event.target.files[0];
    if (!file) return;
    let reader = new FileReader();
    reader.onload = function(e) {
        try {
            let parsed = JSON.parse(e.target.result);
            if(parsed.batches || parsed.sales || parsed.expenses) {
                if(confirm("هل أنت متأكد من استيراد هذه النسخة الاحتياطية؟ سيتم دمجها مع البيانات الحالية ونقض التكرار!")) {
                    batches = parsed.batches || [];
                    sales = parsed.sales || [];
                    expenses = parsed.expenses || [];
                    commandNumber = parsed.commandNumber || 1;
                    save();
                    render();
                    alert("تم استيراد قاعدة البيانات الاحتياطية وتحديث النظام بالكامل بنجاح كلي!");
                }
            } else { alert("الملف المرفوع غير متطابق مع بنية النظام المطور."); }
        } catch (err) { alert("خطأ في قراءة ملف الـ JSON المرفوع."); }
    };
    reader.readAsText(file);
}
</script>

</body>
</html>

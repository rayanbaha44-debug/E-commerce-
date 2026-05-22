<!DOCTYPE html>
<html lang="ar" dir="rtl">

<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>POS SYSTEM EXECUTIVE - نظام المبيعات الاحترافي المطور</title>

<!-- استدعاء خط Cairo والأيقونات الاحترافية -->
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
    --success-gradient: linear-gradient(135deg, #10b981 0%, #059669; 100%);
    --danger: #ef4444;
    --danger-gradient: linear-gradient(135deg, #ef4444 0%, #b91c1c 100%);
    --warning: #f59e0b;
    --warning-gradient: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);
    --purple-gradient: linear-gradient(135deg, #a855f7 0%, #7e22ce 100%);
    
    /* ألوان الخلفية الاحترافية الفخمة */
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

/* الصناديق والعلب الفرعية */
.box {
    background: rgba(9, 13, 22, 0.6);
    padding: 25px;
    border-radius: var(--radius-lg);
    margin-bottom: 25px;
    border: 1px solid var(--border);
}

.flex-inputs { display: flex; gap: 15px; align-items: center; margin-bottom: 20px; }
.flex-inputs > div { flex: 1; }

/* ================= الجداول المتطورة فائدة التباين والوضوح ================= */
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

/* تأثير حركي لقراءة أسهل */
tr:hover td {
    background-color: #2563eb; 
    color: #ffffff !important;
    transition: background 0.15s ease;
}

/* تخصيص وحماية كود الباركود / الرفرونس عند الكتابة الطويلة جداً */
td code {
    background: rgba(0, 0, 0, 0.4);
    padding: 6px 12px;
    border-radius: 8px;
    color: #38bdf8; 
    font-family: monospace;
    font-size: 14px;
    border: 1px solid rgba(56, 189, 248, 0.2);
    font-weight: 700;
    
    /* الخصائص السحرية لمنع خروج الرفرونس الطويل */
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

/* بطاقات الطلبيات المسجلة والسلة */
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

/* كروت شبكة تقارير الأرباح والمخزون النيون */
.profit-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 20px; margin-top: 25px; }
.profit-card { background: #1f2937; padding: 25px; border-radius: var(--radius-lg); border: 1px solid var(--border); border-right: 5px solid var(--primary); box-shadow: var(--shadow-blur); }
.profit-card.success { border-right-color: var(--success); }
.profit-card.dark { border-right-color: #cbd5e1; }
.profit-card.filter { border-right-color: #a855f7; background: rgba(168, 85, 247, 0.05); border-top: 1px solid rgba(168, 85, 247, 0.1); }
.profit-card.expense-card { border-right-color: var(--danger); background: rgba(239, 68, 68, 0.05); border-top: 1px solid rgba(239, 68, 68, 0.1); }
.profit-card p { color: var(--text-muted); font-size: 14px; font-weight: 700; margin-bottom: 8px;}
.profit-card .amount { font-size: 24px; font-weight: 800; }

/* ألوان السلع الناقصة الفاقعة والمتوافقة مع الحماية من النصوص الطويلة */
.stock-empty { background-color: #ef4444 !important; color: #ffffff !important; }
.stock-danger { background-color: rgba(239, 68, 68, 0.3) !important; color: #ffffff !important; }
.stock-warning { background-color: rgba(245, 158, 11, 0.3) !important; color: #ffffff !important; }
.stock-notice { background-color: rgba(59, 130, 246, 0.3) !important; color: #ffffff !important; }

/* حماية إضافية لأكواد الباركود داخل قائمة السلع الناقصة لمنع تغيير ألوانها بشكل مشوه */
.stock-empty td code, .stock-danger td code, .stock-warning td code, .stock-notice td code {
    color: #ffffff !important;
    background: rgba(0, 0, 0, 0.25) !important;
    border-color: rgba(255, 255, 255, 0.3) !important;
}

/* تجميل شريط التمرير */
::-webkit-scrollbar { width: 10px; }
::-webkit-scrollbar-track { background: #090d16; }
::-webkit-scrollbar-thumb { background: #374151; border-radius: 5px; }
::-webkit-scrollbar-thumb:hover { background: #4b5563; }
</style>
</head>

<body>

<!-- لوحة التحكم الرئيسية - DASHBOARD -->
<div id="dashboard">
    <div class="card" onclick="openPage('products')"><i class="fa-solid fa-box-open"></i> إدارة المنتجات والمخزن</div>
    <div class="card" onclick="openPage('sales')"><i class="fa-solid fa-cash-register"></i> واجهة البيع السريعة</div>
    <div class="card" onclick="openPage('stock')"><i class="fa-solid fa-warehouse"></i> جرد المخزون الكلي</div>
    <div class="card" onclick="openPage('low')"><i class="fa-solid fa-triangle-exclamation" style="background:var(--warning-gradient); -webkit-background-clip: text;"></i> السلع الناقصة بالمحل</div>
    <div class="card" onclick="openPage('expenses')"><i class="fa-solid fa-hand-holding-dollar" style="background:var(--danger-gradient); -webkit-background-clip: text;"></i> إدارة المصاريف الكلية</div>
    <div class="card" onclick="openPage('profits')"><i class="fa-solid fa-chart-line" style="background:var(--success-gradient); -webkit-background-clip: text;"></i> تقارير الأرباح الصافية</div>
    
    <!-- أزرار النسخ الاحتياطي المحدثة (التصدير والاستيراد) -->
    <div class="card" onclick="exportData()" style="background: rgba(16, 185, 129, 0.02); border: 1px dashed rgba(16, 185, 129, 0.25);"><i class="fa-solid fa-file-export" style="background:var(--success-gradient); -webkit-background-clip: text;"></i> تصدير نسخة احتياطية</div>
    <div class="card" onclick="triggerImport()" style="background: rgba(168, 85, 247, 0.02); border: 1px dashed rgba(168, 85, 247, 0.25);"><i class="fa-solid fa-file-import" style="background:var(--purple-gradient); -webkit-background-clip: text;"></i> استيراد نسخة من الكمبيوتر</div>
</div>

<!-- حقل مخفي مخصص لرفع الملفات من الكمبيوتر -->
<input type="file" id="importFileInput" accept=".json" style="display: none;" onchange="importData(event)">

<!-- إدارة المنتجات - PRODUCTS -->
<div id="products" class="page">
    <div class="header">
        <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع للرئيسية</button>
        <h2><i class="fa-solid fa-box-open" style="color:var(--primary);"></i> إدارة المنتجات والمخزن</h2>
    </div>
    <div class="box">
        <h3 style="margin-bottom: 20px; font-size:17px;"><i class="fa-solid fa-plus-circle"></i> إضافة منتج جديد يدوياً</h3>
        <div class="flex-inputs">
            <div><label>الباركود / Ref:</label><input id="pRef" placeholder="أدخل أو امسح الباركود"></div>
            <div><label>اسم المنتج:</label><input id="pName" placeholder="اسم المنتج بالكامل"></div>
        </div>
        <div class="flex-inputs">
            <div><label>سعر الشراء (DA):</label><input id="pBuy" type="number" step="0.01" placeholder="0.00"></div>
            <div><label>سعر البيع الافتراضي (DA):</label><input id="pSell" type="number" step="0.01" placeholder="0.00"></div>
            <div><label>الكمية الابتدائية:</label><input id="pQty" type="number" step="0.01" placeholder="0"></div>
        </div>
        <button onclick="addProduct()" style="width: 100%; margin-top: 5px; background: var(--success-gradient); height: 50px;"><i class="fa-solid fa-plus"></i> إضافة المنتج للمخزن</button>
    </div>
    <div style="margin-top: 25px; margin-bottom: 10px;">
        <label>🔍 بحث سريع وسلس في المنتجات:</label>
        <input id="productSearch" placeholder="ابحث باسم المنتج أو الرقم المتسلسل..." oninput="renderProducts()">
    </div>
    <div style="overflow-x: auto;">
        <table>
            <thead><tr><th>الباركود</th><th>اسم المنتج</th><th>الكمية الحالية</th><th>الشراء (DA)</th><th>البيع الافتراضي (DA)</th><th>تعديل</th><th>حذف</th></tr></thead>
            <tbody id="productTable"></tbody>
        </table>
    </div>
</div>

<!-- واجهة البيع السريعة - SALES -->
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
                    <label>فصل وتصفية المنتجات:</label>
                    <input id="saleSearch" placeholder="اكتب اسم المنتج أو امسح الباركود للبحث..." oninput="renderSalesOptions()">
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

<!-- جرد المخزون الكلي - STOCK -->
<div id="stock" class="page">
    <div class="header">
        <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع للرئيسية</button>
        <h2><i class="fa-solid fa-warehouse" style="color:var(--primary);"></i> كشف وجرد المخزون الكلي</h2>
    </div>

    <!-- بطاقات الإحصاءات العلوية المضافة حديثاً للمخزون للرؤية السريعة فور الدخول -->
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

<!-- السلع الناقصة - LOW -->
<div id="low" class="page">
    <div class="header">
        <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع للرئيسية</button>
        <h2><i class="fa-solid fa-triangle-exclamation" style="color:var(--warning);"></i> كشف السلع الناقصة وحالة المخزون بالتدرج</h2>
    </div>
    <div style="overflow-x: auto;">
        <table>
            <thead><tr><th>الباركود / Ref</th><th>اسم المنتج</th><th>الكمية المتبقية</th><th>سعر الشراء (DA)</th><th>حالة خطورة المخزون وطبيعة التنبيه</th></tr></thead>
            <tbody id="lowTable"></tbody>
        </table>
    </div>
</div>

<!-- إدارة المصاريف - EXPENSES -->
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

<!-- تقارير الأرباح - PROFITS -->
<div id="profits" class="page">
    <div class="header">
        <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع للرئيسية</button>
        <h2><i class="fa-solid fa-chart-line" style="color:var(--success);"></i> التقارير المالية والأرباح الصافية الحقيقية</h2>
    </div>
    <div class="box" style="background: rgba(17, 24, 39, 0.6);">
        <h3 style="margin-bottom: 20px; font-size:17px; color: #a855f7;"><i class="fa-solid fa-calendar-days"></i> فرز واحتساب الأرباح بفترة زمنية مخصصة 🗓️</h3>
        <div class="flex-inputs">
            <div><label>من تاريخ 📅:</label><input type="date" id="filterFrom" onchange="calculateFilteredProfit()"></div>
            <div><label>إلى تاريخ 🏁:</label><input type="date" id="filterTo" onchange="calculateFilteredProfit()"></div>
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

// نغمة بسيطة لإضافة مادة للسلة
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

// رنين الكاسة الاحترافي الفخم عند نجاح عملية البيع
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
        osc1.connect(gain1);
        gain1.connect(ctx.destination);
        osc1.start(now);
        osc1.stop(now + 0.4);
        
        let osc2 = ctx.createOscillator();
        let gain2 = ctx.createGain();
        osc2.type = 'triangle';
        osc2.frequency.setValueAtTime(880, now + 0.02);
        gain2.gain.setValueAtTime(0.15, now + 0.02);
        gain2.gain.exponentialRampToValueAtTime(0.001, now + 0.3);
        osc2.connect(gain2);
        gain2.connect(ctx.destination);
        osc2.start(now + 0.02);
        osc2.stop(now + 0.3);

        let osc3 = ctx.createOscillator();
        let gain3 = ctx.createGain();
        osc3.type = 'sawtooth';
        osc3.frequency.setValueAtTime(300, now + 0.08);
        osc3.frequency.linearRampToValueAtTime(120, now + 0.25);
        gain3.gain.setValueAtTime(0.1, now + 0.08);
        gain3.gain.exponentialRampToValueAtTime(0.001, now + 0.3);
        osc3.connect(gain3);
        gain3.connect(ctx.destination);
        osc3.start(now + 0.08);
        osc3.stop(now + 0.3);
        
    } catch (e) { console.log("Cash sound error: ", e); }
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
    orderItems.forEach(s => {
        let b = batches.find(x => x.id === s.id);
        if(b) { b.qty += s.qty; } 
        else { batches.push({ id: s.id, ref: s.ref, name: s.name, buy: s.buy, sell: s.sell, qty: s.qty }); }
    });
    currentCommandData = orderItems.map(s => { return { id: s.id, ref: s.ref, name: s.name, buy: s.buy, sell: s.sell, qty: s.qty }; });
    sales = sales.filter(x => x.command !== orderNum);
    commandNumber = orderNum;
    document.getElementById('cmdNumberInput').value = commandNumber;
    document.getElementById('searchOrderNumber').value = '';
    save(); render(); renderSalesOptions(); updateCommandUI();
    alert("تم جلب الطلبية #" + orderNum + " بنجاح إلى السلة.");
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
    document.getElementById('pBuy').value = ''; document.getElementById('pSell').value = ''; document.getElementById('pQty').value = '';
    save(); render();
}

function deleteProduct(id){
    if(!confirm("هل أنت متأكد من حذف السلعة نهائياً؟")) return;
    batches = batches.filter(x => x.id !== id); save(); render();
}

function editProduct(id){
    let b = batches.find(x => x.id === id); if(!b) return;
    b.name = prompt("تعديل اسم المنتج:", b.name) || b.name;
    b.qty = +prompt("تعديل الكمية الحالية:", b.qty) || b.qty;
    b.buy = +prompt("تعديل سعر الشراء:", b.buy) || b.buy;
    b.sell = +prompt("تعديل سعر البيع الافتراضي:", b.sell) || b.sell;
    save(); render();
}

function renderSalesOptions(){
    let searchVal = document.getElementById('saleSearch').value.toLowerCase().trim();
    let filtered = batches.filter(b => b.name.toLowerCase().includes(searchVal) || b.ref.toLowerCase().includes(searchVal));
    let saleStock = document.getElementById('saleStock');
    saleStock.innerHTML = filtered.map(b => `<option value="${b.id}">[${b.ref}] ${b.name} - المتبقي: ${b.qty} - السعر: ${b.sell} DA</option>`).join("");
    updateDefaultSalePriceField();
}

function addToCommand(){
    let saleStock = document.getElementById('saleStock');
    let saleQty = document.getElementById('saleQty');
    let salePriceInput = document.getElementById('salePriceInput');
    if(!saleStock.value) return;
    let id = Number(saleStock.value);
    let qty = +saleQty.value;
    let customPrice = +salePriceInput.value;
    let b = batches.find(x=>x.id===id);
    if(!b || qty<=0) return;
    if(isNaN(customPrice) || customPrice < 0) { alert("يرجى إدخال سعر بيع صحيح"); return; }
    if(b.qty < qty){ alert("المخزون غير كافي"); return; }
    let ex = currentCommandData.find(x => x.id === id && x.sell === customPrice);
    if(ex){
        if(b.qty < ex.qty + qty){ alert("المجموع يتجاوز المتاح في المخزن"); return; }
        ex.qty += qty;
    } else { currentCommandData.push({...b, qty, sell: customPrice}); }
    playBeepSound(); updateCommandUI();
}

function updateCommandUI(){
    let currentCommand = document.getElementById('currentCommand');
    let commandTotal = document.getElementById('commandTotal');
    let total=0;
    currentCommand.innerHTML = currentCommandData.map((i,idx)=>{
        total += i.sell*i.qty;
        return `
        <div style="display:flex; justify-content:space-between; align-items:center; margin:8px 0; background:#111827; padding:12px 16px; border-radius:10px; border:1px solid var(--border);">
            <span><b>${i.name}</b> <span class="badge-qty">x${i.qty}</span> <small style="color:var(--text-muted);">(@ ${i.sell.toFixed(2)} DA)</small></span>
            <div style="display:flex; align-items:center; gap:12px;">
                <span style="color:var(--success); font-weight:700;">${(i.sell*i.qty).toFixed(2)} DA</span>
                <button class="del" onclick="removeFromCommand(${idx})" style="padding:6px 12px; font-size:13px;"><i class="fa-solid fa-trash"></i></button>
            </div>
        </div>`;
    }).join("");
    commandTotal.innerHTML = total.toFixed(2) + " DA";
}

function removeFromCommand(index) { 
    currentCommandData.splice(index, 1); 
    updateCommandUI(); 
}

function confirmCommand(){
    if(currentCommandData.length===0) return alert("السلة فارغة!");
    let uniqueTime = Date.now(); 
    currentCommandData.forEach((item, index)=>{
        let b = batches.find(x=>x.id===item.id); if(!b) return;
        b.qty = Math.max(0, b.qty - item.qty);
        sales.push({
            id: item.id, ref: item.ref, name: item.name, qty: item.qty, buy: item.buy, sell: item.sell, 
            profit: (item.sell - item.buy) * item.qty, time: uniqueTime + index, command: commandNumber
        });
    });
    
    playCashRegisterSound();
    
    commandNumber++; currentCommandData=[]; save(); render(); renderSalesOptions();
}

function deleteEntireOrder(orderNum){
    if(!confirm(`هل تريد إلغاء الطلبية #${orderNum} بالكامل؟`)) return;
    let orderItems = sales.filter(x => x.command === orderNum);
    orderItems.forEach(s => {
        let b = batches.find(x => x.id === s.id);
        if(b) { b.qty += s.qty; } 
        else { batches.push({ id: s.id, ref: s.ref, name: s.name, buy: s.buy, sell: s.sell, qty: s.qty }); }
    });
    sales = sales.filter(x => x.command !== orderNum); save(); render(); renderSalesOptions();
}

function addExpense(){
    let title = document.getElementById('expTitle').value.trim();
    let amount = document.getElementById('expAmount').value;
    let dateVal = document.getElementById('expDate').value;
    if(!title || !amount || !dateVal) return alert("يرجى ملء كافة خانات المصروف");
    expenses.push({ id: Date.now(), title: title, amount: +amount, date: dateVal });
    document.getElementById('expTitle').value = ''; document.getElementById('expAmount').value = '';
    save(); render();
}

function deleteExpense(id){
    if(!confirm("هل تريد حذف هذا المصروف؟")) return;
    expenses = expenses.filter(x => x.id !== id); save(); render();
}

function calculateFilteredProfit(){
    let fromVal = document.getElementById('filterFrom').value;
    let toVal = document.getElementById('filterTo').value;
    if(!fromVal || !toVal) return;
    let startTime = new Date(fromVal + "T00:00:00").getTime();
    let endTime = new Date(toVal + "T23:59:59").getTime();
    let totalSalesProfit = 0;
    sales.forEach(s => { let t = s.time || Date.now(); if(t >= startTime && t <= endTime) totalSalesProfit += s.profit; });
    let totalExp = 0;
    expenses.forEach(e => { let expTime = new Date(e.date + "T12:00:00").getTime(); if(expTime >= startTime && expTime <= endTime) totalExp += e.amount; });
    document.getElementById('filteredProfit').innerHTML = (totalSalesProfit - totalExp).toFixed(2) + " DA 💰";
}

function renderProducts(){
    let searchVal = document.getElementById('productSearch').value.toLowerCase().trim();
    let filtered = batches.filter(b => b.name.toLowerCase().includes(searchVal) || b.ref.toLowerCase().includes(searchVal));
    document.getElementById('productTable').innerHTML = filtered.map(b=>`
    <tr>
        <td><code>${b.ref}</code></td>
        <td><b>${b.name}</b></td>
        <td><span class="badge-qty" style="background:rgba(59,130,246,0.15); color:#60a5fa; border-color:transparent;">${b.qty} قطع</span></td>
        <td style="color: #fca5a5;">${b.buy.toFixed(2)}</td>
        <td style="color: #34d399; font-weight:800;">${b.sell.toFixed(2)}</td>
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
        return `<tr><td><b>${b.name}</b></td><td><span class="badge-qty" style="background:rgba(59,130,246,0.15); color:#60a5fa; border-color:transparent;">${b.qty} قطعة</span></td><td style="color:#fca5a5;">${capital.toFixed(2)} DA</td><td style="color:#34d399;">${expectedProfit.toFixed(2)} DA</td><td><button class="del" onclick="deleteProduct(${b.id})"><i class="fa-solid fa-trash"></i></button></td></tr>`;
    }).join("");

    document.getElementById('stockTableFoot').innerHTML = `
        <tr style="background: #111827;">
            <td style="color: #ffffff; font-weight:800; text-align:right;">📦 إجمالي المخزون:</td>
            <td style="color: #38bdf8; font-weight:800;">${totalPieces} قطعة</td>
            <td style="color: #f87171; font-weight:800;">${totalCapital.toFixed(2)} DA</td>
            <td style="color: #4ade80; font-weight:800;">${(totalValue - totalCapital).toFixed(2)} DA</td>
            <td></td>
        </tr>`;

    // تحديث الكروت العلوية لصفحة جرد المخزون تلقائياً
    document.getElementById('topStockPieces').innerHTML = totalPieces + " قطعة";
    document.getElementById('topStockCapital').innerHTML = totalCapital.toFixed(2) + " DA";
    document.getElementById('topStockProfit').innerHTML = (totalValue - totalCapital).toFixed(2) + " DA";

    let ordersMap = {};
    sales.forEach(s => {
        if(!ordersMap[s.command]) { ordersMap[s.command] = { items: [], totalAmount: 0, totalProfit: 0 }; }
        ordersMap[s.command].items.push(s); ordersMap[s.command].totalAmount += (s.sell * s.qty); ordersMap[s.command].totalProfit += s.profit;
    });
    let ordersKeys = Object.keys(ordersMap).sort((a,b) => b - a);
    if(ordersKeys.length === 0){
        document.getElementById('salesLog').innerHTML = "<p style='text-align:center; padding:15px; color:var(--text-muted);'>لا توجد طلبيات بعد 🌟</p>";
    } else {
        document.getElementById('salesLog').innerHTML = ordersKeys.map(cmdNum => {
            let order = ordersMap[cmdNum];
            let itemsHTML = order.items.map(item => `
                <div class="order-item-line">
                    <span>📦 ${item.name} <span class="badge-qty">x${item.qty}</span> <small style="color:var(--text-muted);">(@ ${item.sell} DA)</small></span>
                    <span style="font-weight:600; color:var(--success);">${(item.sell * item.qty).toFixed(2)} DA</span>
                </div>
            `).join("");
            return `
            <div class="order-card">
                <div class="order-card-header">
                    <span style="font-weight:800; font-size:16px; color:var(--primary);">الطلبية # ${cmdNum}</span>
                    <div style="display:flex; gap:8px;">
                        <button onclick="document.getElementById('searchOrderNumber').value=${cmdNum}; loadOrderToEdit();" style="padding:6px 12px; font-size:12px; background:var(--purple-gradient);"><i class="fa-solid fa-pen"></i> جلب</button>
                        <button class="del" onclick="deleteEntireOrder(${cmdNum})" style="padding:6px 12px; font-size:12px;"><i class="fa-solid fa-trash"></i> إلغاء</button>
                    </div>
                </div>
                <div>${itemsHTML}</div>
                <div style="display:flex; justify-content:space-between; margin-top:12px; padding-top:10px; border-top:1px solid var(--border); font-size:14px; font-weight:700;">
                    <span style="color:var(--text-muted);">الفائدة: <b style="color:var(--success);">${order.totalProfit.toFixed(2)} DA</b></span>
                    <span style="color:var(--text-main);">المجموع: <b style="color:var(--primary);">${order.totalAmount.toFixed(2)} DA</b></span>
                </div>
            </div>`;
        }).join("");
    }

    let totalExpensesSum = 0;
    document.getElementById('expensesLog').innerHTML = [...expenses].reverse().map(e => {
        totalExpensesSum += e.amount;
        return `
        <div class="order-card" style="border-right: 5px solid var(--danger); display:flex; justify-content:space-between; align-items:center;">
            <span>💸 <b>${e.title}</b> <small style="color:var(--text-muted); margin-right:8px;">(${e.date})</small></span>
            <div style="display:flex; align-items:center; gap:15px;">
                <b style="color:var(--danger);">${e.amount.toFixed(2)} DA</b>
                <button class="del" onclick="deleteExpense(${e.id})" style="padding:6px 12px; font-size:13px;"><i class="fa-solid fa-trash"></i></button>
            </div>
        </div>`;
    }).join("");
    if(expenses.length === 0) document.getElementById('expensesLog').innerHTML = "<p style='text-align:center; padding:15px; color:var(--text-muted);'>لا توجد مصاريف مقيدة 🌟</p>";

    let now = new Date(), dProfit = 0, mProfit = 0, yProfit = 0, dExp = 0, mExp = 0;
    let startOfDay = new Date(now.getFullYear(), now.getMonth(), now.getDate()).getTime();
    let startOfMonth = new Date(now.getFullYear(), now.getMonth(), 1).getTime();
    let startOfYear = new Date(now.getFullYear(), 0, 1).getTime();

    sales.forEach(s => {
        let t = s.time || Date.now();
        if(t >= startOfDay) dProfit += s.profit; if(t >= startOfMonth) mProfit += s.profit; if(t >= startOfYear) yProfit += s.profit;
    });
    expenses.forEach(e => {
        let expTime = new Date(e.date + "T12:00:00").getTime();
        if(expTime >= startOfDay) dExp += e.amount; if(expTime >= startOfMonth) mExp += e.amount;
    });

    document.getElementById('dailyProfit').innerHTML = (dProfit - dExp).toFixed(2) + " DA";
    document.getElementById('monthlyProfit').innerHTML = (mProfit - mExp).toFixed(2) + " DA";
    document.getElementById('totalExpensesYear').innerHTML = totalExpensesSum.toFixed(2) + " DA 💸";
    document.getElementById('yearlyProfit').innerHTML = (yProfit - totalExpensesSum).toFixed(2) + " DA 👑";

    calculateFilteredProfit();

    // السلع الناقصة - متجاوبة مع الرفرونس الطويل
    let lowItems = batches.filter(b => b.qty <= 15); lowItems.sort((a, b) => a.qty - b.qty);
    document.getElementById('lowTable').innerHTML = lowItems.map(b => {
        let rowClass = "", statusText = "";
        if (b.qty === 0) { rowClass = "stock-empty"; statusText = "منتهي تماماً (0 قطع) ❌"; } 
        else if (b.qty <= 5) { rowClass = "stock-danger"; statusText = "نقص حاد جداً (1-5 قطع) 🚨"; } 
        else if (b.qty <= 10) { rowClass = "stock-warning"; statusText = "نقص متوسط (6-10 قطع) ⚠️"; } 
        else if (b.qty <= 15) { rowClass = "stock-notice"; statusText = "بداية نقص (11-15 قطعة) ℹ️"; }
        return `
        <tr class="${rowClass}">
            <td><code>${b.ref}</code></td>
            <td><b style="color:white;">${b.name}</b></td>
            <td><b>${b.qty} قطعة</b></td>
            <td style="font-weight: 700;">${b.buy.toFixed(2)} DA</td>
            <td><b>${statusText}</b></td>
        </tr>`;
    }).join("");
    if(lowItems.length === 0) document.getElementById('lowTable').innerHTML = `<tr><td colspan="5" style="color:var(--success); font-weight:700; padding:20px;">🎉 كل السلع متوفرة بكميات ممتازة</td></tr>`;
    
    document.getElementById('cmdNumberInput').value = commandNumber;
}

function exportData(){
    let dataStr = JSON.stringify({ batches, sales, expenses, commandNumber });
    let dataUri = 'data:application/json;charset=utf-8,'+ encodeURIComponent(dataStr);
    let linkElement = document.createElement('a');
    linkElement.setAttribute('href', dataUri); linkElement.setAttribute('download', 'pos_premium_backup.json');
    linkElement.click();
}

/* ================= دالة فتح واستيراد النسخة الاحتياطية ================= */
function triggerImport() {
    document.getElementById('importFileInput').click();
}

function importData(event) {
    let file = event.target.files[0];
    if (!file) return;

    if (!confirm("تحذير: استيراد ملف خارجي سيقوم باستبدال كافة البيانات الحالية بالبيانات الجديدة المخزنة داخل الملف. هل تريد الاستمرار؟")) {
        event.target.value = ''; 
        return;
    }

    let reader = new FileReader();
    reader.onload = function(e) {
        try {
            let importedData = JSON.parse(e.target.result);
            
            if (importedData.hasOwnProperty('batches') && importedData.hasOwnProperty('sales') && importedData.hasOwnProperty('expenses')) {
                batches = importedData.batches || [];
                sales = importedData.sales || [];
                expenses = importedData.expenses || [];
                commandNumber = Number(importedData.commandNumber) || 1;
                
                save();
                render();
                if(document.getElementById('sales').classList.contains('active')) {
                    renderSalesOptions();
                }
                
                alert("🎉 تم استيراد واسترجاع النسخة الاحتياطية بنجاح، وتم تحديث كامل النظام!");
            } else {
                alert("الملف المرفوع غير متوافق أو لا يحتوي على الهيكلة الصحيحة لنظام الـ POS المطور.");
            }
        } catch (err) {
            alert("حدث خطأ أثناء قراءة ملف الـ JSON المرفوع، يرجى التأكد من سلامة الملف.");
            console.error(err);
        }
        event.target.value = ''; 
    };
    reader.readAsText(file);
}
</script>
</body>
</html>

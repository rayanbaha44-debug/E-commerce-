<!DOCTYPE html>
<html lang="ar" dir="rtl">

<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>POS SYSTEM EXECUTIVE - نظام المبيعات الاحترافي الفاخر</title>

<!-- استدعاء خط Cairo والأيقونات الاحترافية -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

<style>
/* ================= PREMIUM MODERN NEON UI DESIGN ================= */
:root {
    --primary: #3b82f6;
    --primary-gradient: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
    --success: #10b981;
    --success-gradient: linear-gradient(135deg, #059669 0%, #047857 100%);
    --danger: #ef4444;
    --danger-gradient: linear-gradient(135deg, #dc2626 0%, #b91c1c 100%);
    --warning: #f59e0b;
    --warning-gradient: linear-gradient(135deg, #d97706 0%, #b45309 100%);
    --purple-gradient: linear-gradient(135deg, #a855f7 0%, #7e22ce 100%);
    
    /* ألوان الخلفية الفاخرة المظلمة */
    --bg-app: #0b0f19; 
    --sidebar-bg: #111827;
    --surface-card: rgba(31, 41, 55, 0.6);
    --input-bg: #0f172a;
    
    --text-main: #ffffff; 
    --text-muted: #9ca3af; 
    --border: rgba(255, 255, 255, 0.08);
    
    --radius-xl: 20px;
    --radius-lg: 14px;
    --radius-md: 10px;
    
    --shadow-sm: 0 4px 6px -1px rgba(0, 0, 0, 0.3);
    --shadow-md: 0 10px 25px -5px rgba(0, 0, 0, 0.5);
    --shadow-glow: 0 0 20px rgba(37, 99, 235, 0.2);
}

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Cairo', sans-serif;
}

body {
    background: var(--bg-app);
    color: var(--text-main);
    min-height: 100vh;
    display: flex;
    overflow-x: hidden;
}

/* ================= الهيكل البنائي الرئيسي (Sidebar Layout) ================= */
.app-container {
    display: flex;
    width: 100%;
    min-height: 100vh;
}

/* القائمة الجانبية الثابتة */
.sidebar {
    width: 280px;
    background: var(--sidebar-bg);
    border-left: 1px solid var(--border);
    display: flex;
    flex-direction: column;
    padding: 25px 15px;
    position: fixed;
    height: 100vh;
    right: 0;
    top: 0;
    z-index: 100;
}

.sidebar-brand {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 10px 15px 25px 15px;
    border-bottom: 1px solid var(--border);
    margin-bottom: 25px;
}

.sidebar-brand i {
    font-size: 26px;
    color: var(--primary);
    text-shadow: 0 0 10px rgba(59, 130, 246, 0.5);
}

.sidebar-brand h1 {
    font-size: 19px;
    font-weight: 800;
    letter-spacing: 0.5px;
}

.sidebar-menu {
    display: flex;
    flex-direction: column;
    gap: 8px;
    flex-grow: 1;
}

.menu-item {
    display: flex;
    align-items: center;
    gap: 14px;
    padding: 14px 18px;
    color: var(--text-muted);
    text-decoration: none;
    font-weight: 600;
    font-size: 15px;
    border-radius: var(--radius-md);
    cursor: pointer;
    transition: all 0.25s ease;
}

.menu-item i {
    font-size: 18px;
    width: 24px;
    text-align: center;
}

.menu-item:hover {
    color: var(--text-main);
    background: rgba(255, 255, 255, 0.04);
}

.menu-item.active {
    color: #fff;
    background: var(--primary-gradient);
    box-shadow: var(--shadow-glow);
}

/* منطقة المحتوى الرئيسي المستجيب */
.main-content {
    margin-right: 280px;
    flex-grow: 1;
    padding: 40px;
    min-height: 100vh;
    background: radial-gradient(circle at 50% 0%, #1e293b 0%, #0b0f19 70%);
}

@media (max-width: 1024px) {
    .sidebar { width: 80px; padding: 20px 10px; }
    .sidebar-brand h1 { display: none; }
    .sidebar-brand { justify-content: center; padding-bottom: 15px; }
    .menu-item span { display: none; }
    .menu-item { justify-content: center; padding: 15px; }
    .main-content { margin-right: 80px; padding: 20px; }
}

/* ================= مكونات لوحة تحكم والصفحات ================= */
.page {
    display: none;
    animation: fadeIn 0.4s ease-out;
}

.page.active { display: block; }

@keyframes fadeIn {
    from { opacity: 0; transform: translateY(10px); }
    to { opacity: 1; transform: translateY(0); }
}

.page-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 35px;
}

.page-title {
    font-size: 26px;
    font-weight: 800;
    display: flex;
    align-items: center;
    gap: 15px;
}

/* الأزرار الراقية */
button {
    padding: 12px 22px;
    border: none;
    border-radius: var(--radius-md);
    cursor: pointer;
    font-weight: 700;
    font-size: 14px;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    transition: all 0.2s ease;
}

.btn-primary { background: var(--primary-gradient); color: #fff; box-shadow: 0 4px 14px rgba(37, 99, 235, 0.3); }
.btn-primary:hover { transform: translateY(-2px); box-shadow: 0 6px 20px rgba(37, 99, 235, 0.5); }

.btn-success { background: var(--success-gradient); color: #fff; box-shadow: 0 4px 14px rgba(16, 185, 129, 0.3); }
.btn-success:hover { transform: translateY(-2px); box-shadow: 0 6px 20px rgba(16, 185, 129, 0.5); }

.btn-danger { background: var(--danger-gradient); color: #fff; box-shadow: 0 4px 14px rgba(239, 68, 68, 0.3); }
.btn-danger:hover { transform: translateY(-2px); box-shadow: 0 6px 20px rgba(239, 68, 68, 0.5); }

.btn-secondary { background: #374151; color: #fff; }
.btn-secondary:hover { background: #4b5563; }

/* عناصر الإدخال الفاخرة */
.card-box {
    background: var(--surface-card);
    border: 1px solid var(--border);
    border-radius: var(--radius-xl);
    padding: 30px;
    margin-bottom: 30px;
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
    box-shadow: var(--shadow-md);
}

.grid-inputs {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 20px;
    margin-bottom: 20px;
}

.form-group label {
    display: block;
    font-size: 13px;
    font-weight: 700;
    color: var(--text-muted);
    margin-bottom: 8px;
}

input, select {
    width: 100%;
    padding: 13px 16px;
    border-radius: var(--radius-md);
    border: 1px solid var(--border);
    background: var(--input-bg);
    color: var(--text-main);
    font-size: 14px;
    font-weight: 600;
    transition: all 0.2s ease;
}

input:focus, select:focus {
    outline: none;
    border-color: var(--primary);
    box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.25);
}

/* مؤشر الخطأ التلقائي */
input.input-error {
    border-color: var(--danger) !important;
    background: rgba(239, 68, 68, 0.08) !important;
    box-shadow: 0 0 0 3px rgba(239, 68, 68, 0.25) !important;
    animation: shake 0.3s ease;
}

@keyframes shake {
    0%, 100% { transform: translateX(0); }
    25% { transform: translateX(-5px); }
    75% { transform: translateX(5px); }
}

/* ================= تصميم الجداول الأنيق عالي التباين ================= */
.table-container {
    overflow-x: auto;
    border-radius: var(--radius-lg);
    border: 1px solid var(--border);
    box-shadow: var(--shadow-md);
}

table {
    width: 100%;
    border-collapse: collapse;
    text-align: right;
}

th, td { padding: 16px 20px; font-size: 14px; }
th { background: #111827; color: var(--text-muted); font-weight: 700; border-bottom: 2px solid var(--border); }
td { background: rgba(17, 24, 39, 0.4); border-bottom: 1px solid var(--border); font-weight: 600; }
tr:hover td { background: rgba(255, 255, 255, 0.03); }

td code {
    background: rgba(0, 0, 0, 0.3);
    padding: 5px 10px;
    border-radius: 6px;
    color: #38bdf8;
    font-family: monospace;
    font-weight: 700;
    display: inline-block;
    max-width: 160px;
    word-break: break-all;
}

/* ال badges وبطاقات الكميات */
.badge-qty {
    background: rgba(59, 130, 246, 0.15);
    color: #60a5fa;
    padding: 4px 10px;
    border-radius: 6px;
    font-weight: 700;
    font-size: 13px;
}

/* ================= شبكة كروت البيانات الملونة النيون ================= */
.stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    gap: 25px;
    margin-bottom: 35px;
}

.stat-card {
    background: var(--surface-card);
    border: 1px solid var(--border);
    border-radius: var(--radius-xl);
    padding: 25px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    box-shadow: var(--shadow-sm);
    position: relative;
    overflow: hidden;
}

.stat-card::before {
    content: ''; position: absolute; top: 0; right: 0; width: 4px; height: 100%; background: var(--primary);
}
.stat-card.success::before { background: var(--success); }
.stat-card.danger::before { background: var(--danger); }
.stat-card.purple::before { background: #a855f7; }
.stat-card.warning::before { background: var(--warning); }

.stat-info p { color: var(--text-muted); font-size: 13px; font-weight: 700; margin-bottom: 5px; }
.stat-info h3 { font-size: 24px; font-weight: 800; }

.stat-icon {
    width: 50px; height: 50px; border-radius: var(--radius-md); display: flex; align-items: center; justify-content: center; font-size: 22px;
}
.stat-card.primary .stat-icon { background: rgba(59, 130, 246, 0.1); color: #60a5fa; }
.stat-card.success .stat-icon { background: rgba(16, 185, 129, 0.1); color: #34d399; }
.stat-card.danger .stat-icon { background: rgba(239, 68, 68, 0.1); color: #f87171; }
.stat-card.purple .stat-icon { background: rgba(168, 85, 247, 0.1); color: #c084fc; }
.stat-card.warning .stat-icon { background: rgba(245, 158, 11, 0.1); color: #fbbf24; }

/* ================= واجهة البيع السريعة المتقدمة ================= */
.sales-layout {
    display: grid;
    grid-template-columns: 1.3fr 1fr;
    gap: 30px;
    align-items: start;
}
@media (max-width: 1200px) { .sales-layout { grid-template-columns: 1fr; } }

.basket-container {
    border: 1px solid rgba(16, 185, 129, 0.25);
    background: rgba(16, 185, 129, 0.02);
    position: sticky; top: 30px;
}

.basket-items { max-height: 300px; overflow-y: auto; margin-bottom: 25px; }

.basket-row {
    display: flex; justify-content: space-between; align-items: center; padding: 12px 15px; background: rgba(0,0,0,0.2); border: 1px solid var(--border); border-radius: var(--radius-md); margin-bottom: 10px;
}

/* ستايل حالات الخطورة في السلع الناقصة لتبدو احترافية ولا تفسد المظهر */
.row-empty { border-right: 5px solid var(--danger); }
.row-danger { border-right: 5px solid rgba(239, 68, 68, 0.5); }
.row-warning { border-right: 5px solid var(--warning); }
.row-notice { border-right: 5px solid var(--primary); }

/* شريط تمرير ناعم ومخفي */
::-webkit-scrollbar { width: 6px; height: 6px; }
::-webkit-scrollbar-track { background: var(--bg-app); }
::-webkit-scrollbar-thumb { background: #374151; border-radius: 10px; }
::-webkit-scrollbar-thumb:hover { background: #4b5563; }
</style>
</head>

<body>

<div class="app-container">
    
    <!-- القائمة الجانبية الموحدة للاستغناء عن التشتت -->
    <div class="sidebar">
        <div class="sidebar-brand">
            <i class="fa-solid fa-bolt"></i>
            <h1>نظام المبيعات الذكي</h1>
        </div>
        <div class="sidebar-menu">
            <div class="menu-item active" id="menu-home" onclick="switchTab('home')"><i class="fa-solid fa-chart-pie"></i><span>لوحة التحكم الموحدة</span></div>
            <div class="menu-item" id="menu-products" onclick="switchTab('products')"><i class="fa-solid fa-box-open"></i><span>إدارة المنتجات والمخزن</span></div>
            <div class="menu-item" id="menu-sales" onclick="switchTab('sales')"><i class="fa-solid fa-cash-register"></i><span>واجهة البيع السريعة</span></div>
            <div class="menu-item" id="menu-expenses" onclick="switchTab('expenses')"><i class="fa-solid fa-hand-holding-dollar"></i><span>إدارة وتدوين المصاريف</span></div>
            <div class="menu-item" id="menu-profits" onclick="switchTab('profits')"><i class="fa-solid fa-chart-line"></i><span>التقارير المالية والأرباح</span></div>
            <div class="menu-item" id="menu-low" onclick="switchTab('low')"><i class="fa-solid fa-triangle-exclamation"></i><span>السلع الناقصة والمخاطر</span></div>
        </div>
        <div style="display:flex; flex-direction:column; gap:10px; margin-top:auto; border-top:1px solid var(--border); padding-top:15px;">
            <button class="btn-success" onclick="exportData()" style="width:100%; font-size:12px; padding:10px;"><i class="fa-solid fa-file-export"></i> تصدير نسخة</button>
            <button class="btn-primary" onclick="triggerImport()" style="width:100%; font-size:12px; padding:10px; background:var(--purple-gradient);"><i class="fa-solid fa-file-import"></i> استيراد نسخة</button>
        </div>
    </div>

    <!-- حقل رفع ملفات قاعدة البيانات المخفي -->
    <input type="file" id="importFileInput" accept=".json" style="display: none;" onchange="importData(event)">

    <!-- منطقة المحتوى الرئيسي والتطبيقات المستهدفة -->
    <div class="main-content">

        <!-- صفحة 1: لوحة التحكم الموحدة (Home Dashboard) -->
        <div id="page-home" class="page active">
            <div class="page-header">
                <h2 class="page-title"><i class="fa-solid fa-chart-pie" style="color:var(--primary);"></i> الإحصاءات العامة الحالية للنظام</h2>
            </div>
            <!-- كروت نظرة سريعة على رأس المال والمخزون الحالي والمصاريف السنوية -->
            <div class="stats-grid">
                <div class="stat-card primary">
                    <div class="stat-info"><p>📦 السلع الكلية بالمخزن</p><h3 id="homeTotalPieces">0 قطعة</h3></div>
                    <div class="stat-icon"><i class="fa-solid fa-warehouse"></i></div>
                </div>
                <div class="stat-card warning">
                    <div class="stat-info"><p>💰 إجمالي رأس المال المستثمر</p><h3 id="homeCapital">0.00 DA</h3></div>
                    <div class="stat-icon"><i class="fa-solid fa-dollar-sign"></i></div>
                </div>
                <div class="stat-card success">
                    <div class="stat-info"><p>📈 أرباح متوقعة داخل المخزن</p><h3 id="homeExpectedProfit">0.00 DA</h3></div>
                    <div class="stat-icon"><i class="fa-solid fa-arrow-trend-up"></i></div>
                </div>
                <div class="stat-card danger">
                    <div class="stat-info"><p>💸 إجمالي المصاريف العامة السنوية</p><h3 id="homeTotalExpenses">0.00 DA</h3></div>
                    <div class="stat-icon"><i class="fa-solid fa-file-invoice-dollar"></i></div>
                </div>
            </div>
            
            <div class="card-box" style="text-align: center; padding: 40px 20px;">
                <h3 style="font-size:20px; margin-bottom:10px;">👋 أهلاً بك مجدداً في نظام المبيعات المطور الخاص بك</h3>
                <p style="color:var(--text-muted); max-width:600px; margin:0 auto 25px auto;">استخدم القائمة الجانبية الأنيقة للانتقال بسلاسة بين تسجيل السلع، البيع الفوري، قيد مصاريف المحل اليومية واحتساب الفوائد الصافية بدقة متناهية وحماية ماليّة ضد خسارة رأس المال.</p>
                <button class="btn-primary" onclick="switchTab('sales')" style="padding:15px 30px; font-size:16px;"><i class="fa-solid fa-bolt"></i> فتح واجهة البيع السريعة والبدء بالعمل</button>
            </div>
        </div>

        <!-- صفحة 2: إدارة السلع والمخزن -->
        <div id="page-products" class="page">
            <div class="page-header">
                <h2 class="page-title"><i class="fa-solid fa-box-open" style="color:var(--primary);"></i> إدارة المنتجات والمخزن الكلي</h2>
            </div>
            <div class="card-box">
                <h3 style="font-size:16px; margin-bottom:20px;"><i class="fa-solid fa-plus-circle" style="color:var(--success);"></i> إضافة منتج جديد يدوياً أو بالباركود</h3>
                <div class="grid-inputs">
                    <div class="form-group"><label>الباركود / Ref (يجب أن يكون فريداً):</label><input id="pRef" placeholder="أدخل أو امسح الباركود" oninput="checkRefUniqueness()"></div>
                    <div class="form-group"><label>اسم المنتج:</label><input id="pName" placeholder="اسم السلعة بالكامل"></div>
                </div>
                <div class="grid-inputs" style="grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));">
                    <div class="form-group"><label>سعر الشراء (DA):</label><input id="pBuy" type="number" step="0.01" placeholder="0.00" oninput="checkPriceValidity()"></div>
                    <div class="form-group"><label>سعر البيع الافتراضي (DA):</label><input id="pSell" type="number" step="0.01" placeholder="0.00" oninput="checkPriceValidity()"></div>
                    <div class="form-group"><label>الكمية الابتدائية:</label><input id="pQty" type="number" step="0.01" placeholder="0"></div>
                </div>
                <button class="btn-success" onclick="addProduct()" style="width:100%; height:48px; margin-top:10px;"><i class="fa-solid fa-check"></i> إضافة المنتج وتثبيته بالمخزن</button>
            </div>

            <div style="margin-bottom: 15px;">
                <input id="productSearch" placeholder="🔍 ابحث سريعاً بالاسم أو الباركود لفلترة جدول السلع أدناه..." oninput="renderProducts()" style="padding:15px;">
            </div>
            <div class="table-container">
                <table>
                    <thead><tr><th>الباركود</th><th>اسم المنتج</th><th>الكمية المتاحة</th><th>سعر الشراء (DA)</th><th>البيع الافتراضي (DA)</th><th>تعديل</th><th>حذف</th></tr></thead>
                    <tbody id="productTable"></tbody>
                </table>
            </div>
        </div>

        <!-- صفحة 3: واجهة البيع السريعة والتعديل الفوري -->
        <div id="page-sales" class="page">
            <div class="page-header">
                <h2 class="page-title"><i class="fa-solid fa-cash-register" style="color:var(--primary);"></i> واجهة بيع السلع وإلغاء وتعديل الفواتير</h2>
            </div>
            
            <div style="display: grid; grid-template-columns: 1fr 1fr; gap:20px; margin-bottom:25px;">
                <div class="card-box" style="margin:0; padding:15px; display:flex; align-items:center; justify-content:space-around; background:#111827;">
                    <span style="font-weight:700; font-size:14px;"><i class="fa-solid fa-receipt" style="color:var(--primary);"></i> رقم الطلب الحالي:</span>
                    <input id="cmdNumberInput" type="number" min="1" style="width:100px; text-align:center; font-weight:800; padding:8px; background:var(--input-bg);" oninput="updateCommandNumberManual()">
                    <button class="btn-danger" onclick="resetCommandNumber()" style="padding:8px 14px; font-size:12px;"><i class="fa-solid fa-rotate"></i> تصفير العداد</button>
                </div>
                <div class="card-box" style="margin:0; padding:15px; display:flex; align-items:center; gap:15px;">
                    <input id="searchOrderNumber" type="number" placeholder="أدخل رقم طلبية سابقة لتعديلها..." style="background:var(--input-bg);">
                    <button class="btn-primary" onclick="loadOrderToEdit()" style="background:var(--purple-gradient); white-space:nowrap;"><i class="fa-solid fa-edit"></i> جلب السلة للتعديل</button>
                </div>
            </div>

            <div class="sales-layout">
                <div>
                    <div class="card-box">
                        <h3 style="font-size:15px; margin-bottom:20px; color:var(--primary);"><i class="fa-solid fa-filter"></i> فلترة واختيار المنتج المستهدف بالبيع</h3>
                        <div class="form-group" style="margin-bottom:15px;">
                            <label>بحث فوري سريع:</label>
                            <input id="saleSearch" placeholder="اكتب اسم السلعة أو امسح الباركود..." oninput="renderSalesOptions()">
                        </div>
                        <div class="form-group" style="margin-bottom:15px;">
                            <label>قائمة الاختيار المصفاة:</label>
                            <select id="saleStock" onchange="updateDefaultSalePriceField()"></select>
                        </div>
                        <div class="grid-inputs">
                            <div class="form-group"><label>الكمية المراد بيعها:</label><input id="saleQty" type="number" step="1" value="1"></div>
                            <div class="form-group">
                                <label style="color:var(--primary); font-weight:800;"><i class="fa-solid fa-edit"></i> تحديد سعر البيع الحالي (مرن):</label>
                                <input id="salePriceInput" type="number" step="0.01" style="border:1px solid var(--primary); font-weight:700;">
                            </div>
                        </div>
                        <button class="btn-primary" onclick="addToCommand()" style="width:100%; height:48px; font-size:15px;"><i class="fa-solid fa-cart-plus"></i> إضافة المنتج المحدد للسلة</button>
                    </div>

                    <h3 style="font-size:16px; font-weight:700; margin-bottom:15px;"><i class="fa-solid fa-clock-rotate-left"></i> سجل العمليات والفواتير السابقة المقيدة</h3>
                    <div id="salesLog" style="max-height:380px; overflow-y:auto;"></div>
                </div>

                <!-- سلة التسوق المتوضعة بثبات على اليسار -->
                <div class="card-box basket-container">
                    <h3 style="font-size:16px; margin-bottom:15px; color:var(--success); border-bottom:1px solid var(--border); padding-bottom:10px;"><i class="fa-solid fa-basket-shopping"></i> سلة التسوق الحالية</h3>
                    <div id="currentCommand" class="basket-items"></div>
                    
                    <div style="background:rgba(16, 185, 129, 0.08); padding:20px; border-radius:var(--radius-md); border:1px solid rgba(16, 185, 129, 0.15); margin-bottom:20px; text-align:left;">
                        <span style="color:var(--success); font-size:13px; font-weight:700;">المجموع الإجمالي المستحق:</span>
                        <h2 id="commandTotal" style="color:var(--success); font-size:28px; font-weight:900; margin-top:3px;">0.00 DA</h2>
                    </div>
                    <button class="btn-success" onclick="confirmCommand()" style="width:100%; padding:15px; font-size:16px;"><i class="fa-solid fa-circle-check"></i> تأكيد الفاتورة وحفظ البيع</button>
                </div>
            </div>
        </div>

        <!-- صفحة 4: إدارة وتدوين المصاريف -->
        <div id="page-expenses" class="page">
            <div class="page-header">
                <h2 class="page-title"><i class="fa-solid fa-hand-holding-dollar" style="color:var(--danger);"></i> إدارة مصاريف المحل وتقييدها</h2>
            </div>
            <div class="card-box">
                <h3 style="font-size:16px; margin-bottom:20px;"><i class="fa-solid fa-file-invoice-dollar"></i> قيد تالف، فاتورة، أجور، أو أي مصروفات عامة</h3>
                <div class="form-group" style="margin-bottom:15px;">
                    <label>بيان ونوع المصروف بالتفصيل:</label>
                    <input id="expTitle" placeholder="مثال: فاتورة الإنترنت والمحل، نقل البضاعة، تالف سلعة...">
                </div>
                <div class="grid-inputs">
                    <div class="form-group"><label>قيمة المصروف الكلي (DA):</label><input id="expAmount" type="number" step="0.01" placeholder="0.00"></div>
                    <div class="form-group"><label>تاريخ التقييد:</label><input id="expDate" type="date"></div>
                </div>
                <button class="btn-danger" onclick="addExpense()" style="width:100%; height:48px; margin-top:10px;"><i class="fa-solid fa-check"></i> حفظ وقيد المصروف بالدفتر المالي</button>
            </div>
            
            <h3 style="font-size:16px; font-weight:700; margin-bottom:15px;"><i class="fa-solid fa-receipt"></i> كشف الدفتر اليومي والشهري للمصاريف المقيّدة</h3>
            <div id="expensesLog" style="max-height:400px; overflow-y:auto;"></div>
        </div>

        <!-- صفحة 5: التقارير المالية والأرباح الصافية -->
        <div id="page-profits" class="page">
            <div class="page-header">
                <h2 class="page-title"><i class="fa-solid fa-chart-line" style="color:var(--success);"></i> التقارير والتحليلات المالية والفوائد الصافية</h2>
            </div>
            <div class="card-box" style="background:rgba(168, 85, 247, 0.02); border-color:rgba(168, 85, 247, 0.2);">
                <h3 style="font-size:16px; margin-bottom:15px; color:#c084fc;"><i class="fa-solid fa-calendar-days"></i> فرز وحساب الأرباح الصافية خلال فترة زمنية محددة</h3>
                <div class="grid-inputs">
                    <div class="form-group"><label>من تاريخ:</label><input type="date" id="filterFrom" onchange="calculateFilteredProfit()"></div>
                    <div class="form-group"><label>إلى تاريخ:</label><input type="date" id="filterTo" onchange="calculateFilteredProfit()"></div>
                </div>
            </div>

            <div class="stats-grid">
                <div class="stat-card purple" style="grid-column: span 2 / span 2;">
                    <div class="stat-info"><p>🎯 صافي ربح الفترة المحددة بالفرز الأعلى (أرباح المبيعات - المصاريف)</p><h3 id="filteredProfit" style="color:#c084fc;">0.00 DA 💰</h3></div>
                    <div class="stat-icon" style="background:rgba(168, 85, 247, 0.1); color:#c084fc;"><i class="fa-solid fa-filter"></i></div>
                </div>
                <div class="stat-card success">
                    <div class="stat-info"><p>💵 صافي فائدة اليوم الحالي الحقيقية</p><h3 id="dailyProfit" style="color:var(--success);">0.00 DA</h3></div>
                    <div class="stat-icon"><i class="fa-solid fa-calendar-day"></i></div>
                </div>
                <div class="stat-card primary">
                    <div class="stat-info"><p>📈 صافي أرباح الشهر الحالي المقيدة</p><h3 id="monthlyProfit" style="color:var(--primary);">0.00 DA</h3></div>
                    <div class="stat-icon"><i class="fa-solid fa-calendar-days"></i></div>
                </div>
                <div class="stat-card dark" style="grid-column: span 2 / span 2; border-right:5px solid #cbd5e1;">
                    <div class="stat-info"><p>👑 صافي فائدة وأرباح السنة الإجمالية الحقيقية</p><h3 id="yearlyProfit">0.00 DA</h3></div>
                    <div class="stat-icon" style="background:rgba(255,255,255,0.05); color:#fff;"><i class="fa-solid fa-crown"></i></div>
                </div>
            </div>
        </div>

        <!-- صفحة 6: السلع الناقصة وتنبيهات المخاطر المخزنية -->
        <div id="page-low" class="page">
            <div class="page-header">
                <h2 class="page-title"><i class="fa-solid fa-triangle-exclamation" style="color:var(--warning);"></i> كشف السلع الناقصة بالمحل ومستويات الخطورة</h2>
            </div>
            <div class="table-container">
                <table>
                    <thead><tr><th>الباركود / Ref</th><th>اسم المنتج</th><th>القطع المتوفرة حالياً</th><th>سعر الشراء (DA)</th><th>حالة الخطورة ونوع تنبيه المخزن</th></tr></thead>
                    <tbody id="lowTable"></tbody>
                </table>
            </div>
        </div>

    </div>
</div>

<script>
/* ================= CORE LOGIC SYSTEM ================= */
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

/* دالة التبديل السلس بين الصفحات الجانبية الشبيهة بالبرامج السحابية */
function switchTab(tabId) {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.querySelectorAll('.menu-item').forEach(m => m.classList.remove('active'));
    
    document.getElementById('page-' + tabId).classList.add('active');
    document.getElementById('menu-' + tabId).classList.add('active');
    
    if(tabId === 'sales') {
        document.getElementById('saleSearch').value = '';
        renderSalesOptions();
    }
    window.scrollTo(0, 0);
}

// أصوات التنبيه والخطأ الذكية المقيدة هندسياً لتجربة الاستخدام السلسة
function playBeepSound() {
    try {
        let audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        let osc = audioCtx.createOscillator(); let gain = audioCtx.createGain();
        osc.type = 'sine'; osc.frequency.setValueAtTime(1100, audioCtx.currentTime);
        gain.gain.setValueAtTime(0.12, audioCtx.currentTime);
        osc.connect(gain); gain.connect(audioCtx.destination);
        osc.start(); osc.stop(audioCtx.currentTime + 0.08);
    } catch(e){}
}

function playErrorSound() {
    try {
        let audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        let now = audioCtx.currentTime;
        let osc = audioCtx.createOscillator(); let gain = audioCtx.createGain();
        osc.type = 'sawtooth'; osc.frequency.setValueAtTime(140, now);
        osc.frequency.linearRampToValueAtTime(75, now + 0.28);
        gain.gain.setValueAtTime(0.25, now); gain.gain.exponentialRampToValueAtTime(0.01, now + 0.28);
        osc.connect(gain); gain.connect(audioCtx.destination);
        osc.start(now); osc.stop(now + 0.28);
    } catch(e){}
}

function playCashRegisterSound() {
    try {
        let audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        let now = audioCtx.currentTime;
        let osc1 = audioCtx.createOscillator(); let gain1 = audioCtx.createGain();
        osc1.type = 'sine'; osc1.frequency.setValueAtTime(1350, now);
        gain1.gain.setValueAtTime(0.2, now); gain1.gain.exponentialRampToValueAtTime(0.001, now + 0.35);
        osc1.connect(gain1); gain1.connect(audioCtx.destination);
        osc1.start(now); osc1.stop(now + 0.35);
    } catch(e){}
}

function checkRefUniqueness() {
    let field = document.getElementById('pRef'); let val = field.value.trim();
    if(!val) { field.classList.remove('input-error'); return; }
    if(batches.some(b => b.ref === val)) { field.classList.add('input-error'); } 
    else { field.classList.remove('input-error'); }
}

function checkPriceValidity() {
    let buy = Number(document.getElementById('pBuy').value) || 0;
    let sellField = document.getElementById('pSell'); let sell = Number(sellField.value) || 0;
    if(sellField.value !== "" && sell < buy) { sellField.classList.add('input-error'); } 
    else { sellField.classList.remove('input-error'); }
}

function updateDefaultSalePriceField(){
    let sel = document.getElementById('saleStock'); if(!sel.value) return;
    let b = batches.find(x => x.id === Number(sel.value));
    if(b) { document.getElementById('salePriceInput').value = b.sell; }
}

function updateCommandNumberManual() {
    let v = document.getElementById('cmdNumberInput').value;
    if(v && Number(v) >= 1) { commandNumber = Math.floor(Number(v)); localStorage.setItem("commandNumber", commandNumber); }
}

function resetCommandNumber() {
    if(confirm("هل تريد تصفير عداد الطلبيات والبدء من الرقم 1؟")) { commandNumber = 1; document.getElementById('cmdNumberInput').value = 1; save(); }
}

function loadOrderToEdit() {
    let num = Number(document.getElementById('searchOrderNumber').value);
    if(!num || num < 1) return alert("يرجى إدخال رقم فاتورة صحيح");
    let items = sales.filter(x => x.command === num);
    if(items.length === 0) return alert("الطلبية غير موجودة في السجلات القديمة!");
    if(currentCommandData.length > 0 && !confirm("السلة الحالية بها عناصر، هل تريد مسحها وجلب الطلبية القديمة؟")) return;
    
    items.forEach(s => {
        let b = batches.find(x => x.id === s.id);
        if(b) b.qty += s.qty;
        else batches.push({ id: s.id, ref: s.ref, name: s.name, buy: s.buy, sell: s.sell, qty: s.qty });
    });
    currentCommandData = items.map(s => ({ id: s.id, ref: s.ref, name: s.name, buy: s.buy, sell: s.sell, qty: s.qty }));
    sales = sales.filter(x => x.command !== num);
    commandNumber = num;
    document.getElementById('cmdNumberInput').value = num;
    document.getElementById('searchOrderNumber').value = '';
    save(); render(); renderSalesOptions(); updateCommandUI();
    alert("تم سحب الطلبية رقم #" + num + " بنجاح إلى السلة لإجراء التعديل.");
}

function addProduct(){
    let refF = document.getElementById('pRef'); let sellF = document.getElementById('pSell');
    let ref = refF.value.trim(); let name = document.getElementById('pName').value.trim();
    let buy = document.getElementById('pBuy').value; let sell = sellF.value; let qty = document.getElementById('pQty').value;
    
    if(!ref || !name || !buy || !sell || !qty) return alert("يرجى ملء كافة المدخلات");
    
    if(batches.some(b => b.ref === ref)) {
        playErrorSound(); refF.classList.add('input-error');
        alert("خطأ: كود الرفرونس مستعمل مسبقاً لمنتج آخر! يرجى تغييره."); return;
    }
    if(Number(sell) < Number(buy)) {
        playErrorSound(); sellF.classList.add('input-error');
        alert("خطأ مالي: لا يمكن إدخال سعر بيع أقل من سعر الشراء (حماية منع الخسارة)!"); return;
    }
    
    batches.push({ id: Date.now(), ref, name, buy: +buy, sell: +sell, qty: +qty });
    refF.value = ''; document.getElementById('pName').value = ''; document.getElementById('pBuy').value = ''; sellF.value = ''; document.getElementById('pQty').value = '';
    refF.classList.remove('input-error'); sellF.classList.remove('input-error');
    save(); render();
}

function deleteProduct(id){
    if(confirm("هل أنت متأكد من مسح هذه السلعة نهائياً من النظام؟")) { batches = batches.filter(x => x.id !== id); save(); render(); }
}

function editProduct(id) {
    let b = batches.find(x => x.id === id); if(!b) return;
    let newName = prompt("تعديل اسم المنتج:", b.name) || b.name;
    let newQty = +prompt("تعديل الكمية المتاحة:", b.qty) || b.qty;
    let newBuy = +prompt("تعديل سعر الشراء الأصلي:", b.buy) || b.buy;
    let newSell = +prompt("تعديل سعر البيع المقترح ليدخل حيز التنفيذ:", b.sell) || b.sell;
    
    if(newSell < newBuy) { playErrorSound(); alert("مرفوض: سعر البيع أقل من سعر الشراء!"); return; }
    b.name = newName; b.qty = newQty; b.buy = newBuy; b.sell = newSell;
    save(); render();
}

function renderSalesOptions(){
    let sVal = document.getElementById('saleSearch').value.toLowerCase().trim();
    let filtered = batches.filter(b => b.name.toLowerCase().includes(sVal) || b.ref.toLowerCase().includes(sVal));
    let saleStock = document.getElementById('saleStock');
    saleStock.innerHTML = filtered.map(b => `<option value="${b.id}">[${b.ref}] ${b.name} - المتاح: ${b.qty} قطعة - السعر الأصلي: ${b.sell} DA</option>`).join("");
    updateDefaultSalePriceField();
}

function addToCommand(){
    let sel = document.getElementById('saleStock'); let sQty = document.getElementById('saleQty'); let sPrice = document.getElementById('salePriceInput');
    if(!sel.value) return;
    let id = Number(sel.value); let qty = +sQty.value; let customPrice = +sPrice.value;
    let b = batches.find(x => x.id === id);
    if(!b || qty <= 0 || isNaN(customPrice)) return;
    if(b.qty < qty) return alert("المخزون المتوفر غير كافٍ لتغطية الكمية المحددة!");
    
    if(customPrice < b.buy) {
        playErrorSound(); alert("خطأ: السعر المقترح للبيع أقل من سعر الشراء الأساسي للمادة!"); return;
    }
    
    let ex = currentCommandData.find(x => x.id === id && x.sell === customPrice);
    if(ex) {
        if(b.qty < ex.qty + qty) return alert("المجموع يتجاوز المتاح بالمخزن!");
        ex.qty += qty;
    } else { currentCommandData.push({...b, qty, sell: customPrice}); }
    playBeepSound(); updateCommandUI();
}

function updateCommandUI(){
    let container = document.getElementById('currentCommand'); let totalEl = document.getElementById('commandTotal');
    let total = 0;
    container.innerHTML = currentCommandData.map((item, idx) => {
        total += item.sell * item.qty;
        return `
        <div class="basket-row">
            <span><b>${item.name}</b> <span class="badge-qty" style="margin-right:5px;">x${item.qty}</span></span>
            <div style="display:flex; align-items:center; gap:10px;">
                <span style="color:var(--success); font-weight:700;">${(item.sell * item.qty).toFixed(2)} DA</span>
                <button class="btn-danger" onclick="removeFromCommand(${idx})" style="padding:4px 8px; font-size:12px;"><i class="fa-solid fa-trash"></i></button>
            </div>
        </div>`;
    }).join("");
    totalEl.innerHTML = total.toFixed(2) + " DA";
}

function removeFromCommand(idx) { currentCommandData.splice(idx, 1); updateCommandUI(); }

function confirmCommand(){
    if(currentCommandData.length === 0) return alert("سلة التسوق فارغة تماماً!");
    let utime = Date.now();
    currentCommandData.forEach((item, index) => {
        let b = batches.find(x => x.id === item.id); if(!b) return;
        b.qty = Math.max(0, b.qty - item.qty);
        sales.push({
            id: item.id, ref: item.ref, name: item.name, qty: item.qty, buy: item.buy, sell: item.sell,
            profit: (item.sell - item.buy) * item.qty, time: utime + index, command: commandNumber
        });
    });
    playCashRegisterSound(); commandNumber++; currentCommandData = []; save(); render(); renderSalesOptions(); updateCommandUI();
}

function deleteEntireOrder(num) {
    if(!confirm(`هل تريد إلغاء وحذف الفاتورة رقم #${num} بالكامل؟`)) return;
    sales.filter(x => x.command === num).forEach(s => {
        let b = batches.find(x => x.id === s.id);
        if(b) b.qty += s.qty;
        else batches.push({ id: s.id, ref: s.ref, name: s.name, buy: s.buy, sell: s.sell, qty: s.qty });
    });
    sales = sales.filter(x => x.command !== num); save(); render(); renderSalesOptions();
}

function addExpense(){
    let title = document.getElementById('expTitle').value.trim();
    let amount = document.getElementById('expAmount').value;
    let date = document.getElementById('expDate').value;
    if(!title || !amount || !date) return alert("يرجى تعبئة كافة الحقول المقيدة");
    expenses.push({ id: Date.now(), title, amount: +amount, date });
    document.getElementById('expTitle').value = ''; document.getElementById('expAmount').value = '';
    save(); render();
}

function deleteExpense(id) {
    if(confirm("هل تريد حذف قيد هذا المصروف نهائياً؟")) { expenses = expenses.filter(x => x.id !== id); save(); render(); }
}

function calculateFilteredProfit(){
    let from = document.getElementById('filterFrom').value; let to = document.getElementById('filterTo').value;
    if(!from || !to) return;
    let st = new Date(from + "T00:00:00").getTime(); let en = new Date(to + "T23:59:59").getTime();
    let sProfit = 0; sales.forEach(s => { let t = s.time || Date.now(); if(t >= st && t <= en) sProfit += s.profit; });
    let eAmt = 0; expenses.forEach(e => { let t = new Date(e.date + "T12:00:00").getTime(); if(t >= st && t <= en) eAmt += e.amount; });
    document.getElementById('filteredProfit').innerHTML = (sProfit - eAmt).toFixed(2) + " DA 💰";
}

function renderProducts(){
    let sVal = document.getElementById('productSearch').value.toLowerCase().trim();
    let filtered = batches.filter(b => b.name.toLowerCase().includes(sVal) || b.ref.toLowerCase().includes(sVal));
    document.getElementById('productTable').innerHTML = filtered.map(b => `
    <tr>
        <td><code>${b.ref}</code></td>
        <td><b>${b.name}</b></td>
        <td><span class="badge-qty">${b.qty} قطع</span></td>
        <td style="color:#fca5a5;">${b.buy.toFixed(2)}</td>
        <td style="color:#34d399; font-weight:800;">${b.sell.toFixed(2)}</td>
        <td><button class="btn-primary" style="padding:6px 12px; background:#1f2937; color:#3b82f6; box-shadow:none;" onclick="editProduct(${b.id})"><i class="fa-solid fa-pen"></i></button></td>
        <td><button class="btn-danger" style="padding:6px 12px;" onclick="deleteProduct(${b.id})"><i class="fa-solid fa-trash"></i></button></td>
    </tr>`).join("");
}

function render(){
    renderProducts();
    let totalCapital = 0, totalValue = 0, totalPieces = 0, totalExpSum = 0;
    
    batches.forEach(b => { totalCapital += (b.buy * b.qty); totalValue += (b.sell * b.qty); totalPieces += b.qty; });
    
    // إرسال الإحصاءات العامة لبطاقات الصفحة الرئيسية الكبرى المحدثة
    document.getElementById('homeTotalPieces').innerHTML = totalPieces + " قطعة";
    document.getElementById('homeCapital').innerHTML = totalCapital.toFixed(2) + " DA";
    document.getElementById('homeExpectedProfit').innerHTML = (totalValue - totalCapital).toFixed(2) + " DA";
    
    // معالجة جدول الفواتير وعمليات المبيعات السابقة
    let ordersMap = {};
    sales.forEach(s => {
        if(!ordersMap[s.command]) ordersMap[s.command] = { items: [], totalAmount: 0, totalProfit: 0 };
        ordersMap[s.command].items.push(s); ordersMap[s.command].totalAmount += (s.sell * s.qty); ordersMap[s.command].totalProfit += s.profit;
    });
    let oKeys = Object.keys(ordersMap).sort((a,b) => b - a);
    if(oKeys.length === 0) {
        document.getElementById('salesLog').innerHTML = "<p style='text-align:center; padding:15px; color:var(--text-muted);'>لا توجد عمليات مبيعات مسجلة حالياً 🌟</p>";
    } else {
        document.getElementById('salesLog').innerHTML = oKeys.map(num => {
            let order = ordersMap[num];
            let itemsHTML = order.items.map(i => `
                <div style="display:flex; justify-content:space-between; font-size:13px; padding:6px 0; border-bottom:1px solid rgba(255,255,255,0.02);">
                    <span>📦 ${i.name} <span class="badge-qty" style="padding:2px 6px; font-size:11px;">x${i.qty}</span></span>
                    <span style="color:var(--success); font-weight:700;">${(i.sell * i.qty).toFixed(2)} DA</span>
                </div>
            `).join("");
            return `
            <div class="card-box" style="padding:15px; margin-bottom:15px; background:rgba(17,24,39,0.5);">
                <div style="display:flex; justify-content:space-between; align-items:center; border-bottom:1px dashed var(--border); padding-bottom:8px; margin-bottom:10px;">
                    <span style="font-weight:800; color:var(--primary);">الطلبية رقم # ${num}</span>
                    <div style="display:flex; gap:6px;">
                        <button class="btn-primary" style="padding:4px 8px; font-size:12px; background:var(--purple-gradient);" onclick="document.getElementById('searchOrderNumber').value=${num}; loadOrderToEdit();"><i class="fa-solid fa-edit"></i> جلب</button>
                        <button class="btn-danger" style="padding:4px 8px; font-size:12px;" onclick="deleteEntireOrder(${num})"><i class="fa-solid fa-trash"></i> إلغاء</button>
                    </div>
                </div>
                <div>${itemsHTML}</div>
                <div style="display:flex; justify-content:space-between; margin-top:10px; padding-top:8px; border-top:1px solid var(--border); font-size:13px; font-weight:700;">
                    <span style="color:var(--text-muted);">صافي الفائدة: <b style="color:var(--success);">${order.totalProfit.toFixed(2)} DA</b></span>
                    <span>المجموع: <b style="color:var(--primary);">${order.totalAmount.toFixed(2)} DA</b></span>
                </div>
            </div>`;
        }).join("");
    }

    // بناء الدفتر المالي للمصاريف
    document.getElementById('expensesLog').innerHTML = [...expenses].reverse().map(e => {
        totalExpSum += e.amount;
        return `
        <div class="card-box" style="padding:15px; margin-bottom:10px; border-right:4px solid var(--danger); display:flex; justify-content:space-between; align-items:center;">
            <span>💸 <b>${e.title}</b> <small style="color:var(--text-muted); margin-right:5px;">(${e.date})</small></span>
            <div style="display:flex; align-items:center; gap:12px;">
                <b style="color:var(--danger);">${e.amount.toFixed(2)} DA</b>
                <button class="btn-danger" style="padding:4px 8px;" onclick="deleteExpense(${e.id})"><i class="fa-solid fa-trash"></i></button>
            </div>
        </div>`;
    }).join("");
    if(expenses.length === 0) document.getElementById('expensesLog').innerHTML = "<p style='text-align:center; padding:15px; color:var(--text-muted);'>سجل دفتر المصاريف فارغ تماماً 🌟</p>";
    
    document.getElementById('homeTotalExpenses').innerHTML = totalExpSum.toFixed(2) + " DA";

    // حسابات الفترات الزمنية للفوائد الصافية الكلية
    let now = new Date(), dProfit = 0, mProfit = 0, yProfit = 0, dExp = 0, mExp = 0;
    let startOfDay = new Date(now.getFullYear(), now.getMonth(), now.getDate()).getTime();
    let startOfMonth = new Date(now.getFullYear(), now.getMonth(), 1).getTime();
    let startOfYear = new Date(now.getFullYear(), 0, 1).getTime();

    sales.forEach(s => {
        let t = s.time || Date.now();
        if(t >= startOfDay) dProfit += s.profit; if(t >= startOfMonth) mProfit += s.profit; if(t >= startOfYear) yProfit += s.profit;
    });
    expenses.forEach(e => {
        let t = new Date(e.date + "T12:00:00").getTime();
        if(t >= startOfDay) dExp += e.amount; if(t >= startOfMonth) mExp += e.amount;
    });

    document.getElementById('dailyProfit').innerHTML = (dProfit - dExp).toFixed(2) + " DA";
    document.getElementById('monthlyProfit').innerHTML = (mProfit - mExp).toFixed(2) + " DA";
    document.getElementById('yearlyProfit').innerHTML = (yProfit - totalExpSum).toFixed(2) + " DA 👑";

    calculateFilteredProfit();

    // جرد وتصفية السلع الناقصة ذات التنبيه المتدرج والمستجيب للنصوص الطويلة للباركود
    let lowItems = batches.filter(b => b.qty <= 15); lowItems.sort((a,b) => a.qty - b.qty);
    document.getElementById('lowTable').innerHTML = lowItems.map(b => {
        let rClass = "", sText = "";
        if(b.qty === 0) { rClass = "row-empty"; sText = "منتهي كلياً (0 قطع) ❌"; }
        else if(b.qty <= 5) { rClass = "row-danger"; sText = "نقص حاد جداً (1-5 قطع) 🚨"; }
        else if(b.qty <= 10) { rClass = "row-warning"; sText = "نقص متوسط (6-10 قطع) ⚠️"; }
        else if(b.qty <= 15) { rClass = "row-notice"; sText = "بداية نقص السلعة (11-15 قطعة) ℹ️"; }
        return `
        <tr class="${rClass}">
            <td><code>${b.ref}</code></td>
            <td><b>${b.name}</b></td>
            <td><span class="badge-qty" style="background:rgba(255,255,255,0.05); color:#fff;">${b.qty} قطع</span></td>
            <td>${b.buy.toFixed(2)} DA</td>
            <td><b style="font-size:13px;">${sText}</b></td>
        </tr>`;
    }).join("");
    if(lowItems.length === 0) document.getElementById('lowTable').innerHTML = `<tr><td colspan="5" style="color:var(--success); font-weight:700; text-align:center; padding:20px;">🎉 كافة المنتجات متوفرة بالمحل بكميات ممتازة جداً</td></tr>`;

    document.getElementById('cmdNumberInput').value = commandNumber;
}

function exportData(){
    let dataStr = JSON.stringify({ batches, sales, expenses, commandNumber });
    let dataUri = 'data:application/json;charset=utf-8,'+ encodeURIComponent(dataStr);
    let a = document.createElement('a'); a.setAttribute('href', dataUri); a.setAttribute('download', 'pos_premium_backup.json');
    a.click();
}

function triggerImport() { document.getElementById('importFileInput').click(); }

function importData(event) {
    let file = event.target.files[0]; if(!file) return;
    if(!confirm("تحذير مالي: استيراد ملف جديد سيقوم بمسح كافة بياناتك الحالية وتعويضها. هل ترغب بالاستمرار؟")) { event.target.value = ''; return; }
    let reader = new FileReader();
    reader.onload = function(e) {
        try {
            let res = JSON.parse(e.target.result);
            if(res.hasOwnProperty('batches') && res.hasOwnProperty('sales')) {
                batches = res.batches || []; sales = res.sales || []; expenses = res.expenses || []; commandNumber = Number(res.commandNumber) || 1;
                save(); render(); renderSalesOptions(); alert("🎉 تم استرجاع واستيراد النسخة الاحتياطية وتحديث النظام بالكامل بنجاح تام!");
            } else { alert("الملف المرفوع غير متوافق مع بنية وهيكلية نظام POS المطور الحالي."); }
        } catch(err) { alert("حدث خطأ تقني أثناء قراءة ملف الـ JSON المرفوع."); }
        event.target.value = '';
    };
    reader.readAsText(file);
}
</script>
</body>
</html>

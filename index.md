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
/* ================= ULTRA PREMIUM MODERN UI/UX ================= */
:root {
    --primary: #2563eb;
    --primary-gradient: linear-gradient(135deg, #3b82f6 0%, #1d4ed8 100%);
    --success: #059669;
    --success-gradient: linear-gradient(135deg, #10b981 0%, #047857 100%);
    --danger: #dc2626;
    --danger-gradient: linear-gradient(135deg, #ef4444 0%, #b91c1c 100%);
    --warning: #d97706;
    --warning-gradient: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);
    --purple-gradient: linear-gradient(135deg, #a855f7 0%, #7e22ce 100%);
    
    --bg-app: #f8fafc;
    --surface: #ffffff;
    --text-main: #0f172a;
    --text-muted: #475569;
    --border: #e2e8f0;
    
    --radius-xl: 20px;
    --radius-lg: 14px;
    --radius-md: 10px;
    
    --shadow-blur: 0 10px 25px -5px rgba(15, 23, 42, 0.04), 0 8px 10px -6px rgba(15, 23, 42, 0.04);
    --shadow-hover: 0 20px 30px -10px rgba(37, 99, 235, 0.15);
}

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Cairo', sans-serif;
}

body {
    background: linear-gradient(135deg, #f1f5f9 0%, #e2e8f0 100%);
    color: var(--text-main);
    min-height: 100vh;
    padding: 30px 15px;
    display: flex;
    flex-direction: column;
    align-items: center;
}

/* لوحة التحكم الرئيسية (Dashboard) */
#dashboard {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    gap: 20px;
    width: 100%;
    max-width: 1100px;
    margin: 30px auto;
}

.card {
    background: var(--surface);
    padding: 30px 20px;
    border-radius: var(--radius-xl);
    text-align: center;
    cursor: pointer;
    border: 1px solid rgba(255, 255, 255, 0.8);
    font-weight: 700;
    font-size: 17px;
    color: var(--text-main);
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    box-shadow: var(--shadow-blur);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 15px;
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
    font-size: 36px;
    background: var(--primary-gradient);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    transition: transform 0.3s ease;
}

.card:hover {
    transform: translateY(-5px);
    box-shadow: var(--shadow-hover);
    border-color: rgba(37, 99, 235, 0.2);
}

.card:hover i { transform: scale(1.1) rotate(3deg); }

/* الصفحات والحاويات الرئيسية */
.page {
    display: none;
    width: 100%;
    max-width: 1200px;
    background: rgba(255, 255, 255, 0.92);
    backdrop-filter: blur(16px);
    -webkit-backdrop-filter: blur(16px);
    padding: 35px;
    border-radius: var(--radius-xl);
    box-shadow: 0 25px 50px -12px rgba(15, 23, 42, 0.08);
    border: 1px solid rgba(255, 255, 255, 0.6);
    animation: slideUp 0.4s cubic-bezier(0.16, 1, 0.3, 1);
}

@keyframes slideUp {
    from { opacity: 0; transform: translateY(15px); }
    to { opacity: 1; transform: translateY(0); }
}

.page.active { display: block; }

.header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 25px;
    padding-bottom: 20px;
    border-bottom: 1px solid var(--border);
}

.header h2 {
    font-size: 24px;
    font-weight: 800;
    color: var(--text-main);
    display: flex;
    align-items: center;
    gap: 12px;
}

/* الأزرار الاحترافية */
button {
    padding: 12px 22px;
    border: none;
    border-radius: var(--radius-md);
    cursor: pointer;
    background: var(--primary-gradient);
    color: white;
    font-weight: 700;
    font-size: 14px;
    transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
    display: inline-flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
}

button:hover { opacity: 0.95; transform: translateY(-1px); box-shadow: 0 4px 12px rgba(37, 99, 235, 0.2); }
button:active { transform: translateY(0); }

.back { background: #64748b; }
.back:hover { background: #475569; box-shadow: 0 4px 12px rgba(100, 116, 139, 0.2); }

.del { background: var(--danger-gradient); }
.del:hover { box-shadow: 0 4px 12px rgba(220, 38, 38, 0.2); }

.edit { background: #f1f5f9; color: var(--text-main); border: 1px solid var(--border); }
.edit:hover { background: var(--border); }

/* عناصر الإدخال والقوائم */
label {
    display: block;
    font-size: 13px;
    font-weight: 700;
    color: var(--text-muted);
    margin-bottom: 6px;
}

input, select {
    width: 100%;
    padding: 12px 16px;
    border-radius: var(--radius-md);
    border: 1px solid var(--border);
    background: #f8fafc;
    color: var(--text-main);
    font-size: 14px;
    font-weight: 600;
    transition: all 0.2s ease;
}

input:focus, select:focus {
    outline: none;
    border-color: var(--primary);
    background: white;
    box-shadow: 0 0 0 4px rgba(37, 99, 235, 0.1);
}

/* تقسيم واجهة البيع بالتساوي (Layout Split) */
.sales-grid {
    display: grid;
    grid-template-columns: 1.2fr 1fr;
    gap: 25px;
    align-items: start;
}

@media (max-width: 900px) {
    .sales-grid { grid-template-columns: 1fr; }
}

/* الصناديق والعلب الفرعية */
.box {
    background: #f8fafc;
    padding: 20px;
    border-radius: var(--radius-lg);
    margin-bottom: 20px;
    border: 1px solid var(--border);
}

.flex-inputs { display: flex; gap: 12px; align-items: center; margin-bottom: 15px; }
.flex-inputs > div { flex: 1; }

/* الجداول المتطورة */
table {
    width: 100%;
    margin-top: 20px;
    border-collapse: separate;
    border-spacing: 0;
    border-radius: var(--radius-lg);
    overflow: hidden;
    border: 1px solid var(--border);
}

th, td { padding: 14px 16px; text-align: center; font-size: 14px; }
th { background-color: #f1f5f9; color: var(--text-muted); font-weight: 700; border-bottom: 1px solid var(--border); }
td { background-color: #fff; border-bottom: 1px solid #f1f5f9; }
tr:last-child td { border-bottom: none; }

/* بطاقات الطلبيات المسجلة والسلة */
.order-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius-lg);
    padding: 16px;
    margin-bottom: 15px;
    box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.05);
}

.order-card-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 1px dashed var(--border);
    padding-bottom: 10px;
    margin-bottom: 10px;
}

.order-item-line {
    display: flex;
    justify-content: space-between;
    padding: 6px 0;
    font-size: 13px;
    border-bottom: 1px solid #f8fafc;
}

.badge-qty { background: #fef3c7; color: #b45309; padding: 3px 8px; border-radius: 6px; font-weight: 700; font-size: 12px; }

/* كروت شبكة تقارير الأرباح */
.profit-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 16px; margin-top: 20px; }
.profit-card { background: var(--surface); padding: 20px; border-radius: var(--radius-lg); border: 1px solid var(--border); border-right: 4px solid var(--primary); box-shadow: var(--shadow-blur); }
.profit-card.success { border-right-color: var(--success); }
.profit-card.dark { border-right-color: var(--text-main); }
.profit-card.filter { border-right-color: #a855f7; background: #faf5ff; border-top: 1px solid #f3e8ff; }
.profit-card.expense-card { border-right-color: var(--danger); background: #fef2f2; border-top: 1px solid #fee2fee2; }
.profit-card p { color: var(--text-muted); font-size: 13px; font-weight: 700; margin-bottom: 6px;}
.profit-card .amount { font-size: 22px; font-weight: 800; }

/* ألوان السلع الناقصة بالتدرج */
.stock-empty { background-color: #0f172a !important; color: #ffffff !important; }
.stock-danger { background-color: #fee2e2 !important; color: #991b1b !important; }
.stock-warning { background-color: #ffedd5 !important; color: #9a3412 !important; }
.stock-notice { background-color: #e0f2fe !important; color: #075985 !important; }

/* تجميل شريط التمرير */
::-webkit-scrollbar { width: 8px; }
::-webkit-scrollbar-track { background: #f1f5f9; }
::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 4px; }
::-webkit-scrollbar-thumb:hover { background: #94a3b8; }
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
    <div class="card" onclick="exportData()" style="background: #f8fafc; border: 1px dashed #cbd5e1;"><i class="fa-solid fa-file-export" style="background:#64748b; -webkit-background-clip: text;"></i> تصدير نسخة احتياطية</div>
</div>

<!-- إدارة المنتجات - PRODUCTS -->
<div id="products" class="page">
    <div class="header">
        <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع للرئيسية</button>
        <h2><i class="fa-solid fa-box-open" style="color:var(--primary);"></i> إدارة المنتجات والمخزن</h2>
    </div>
    <div class="box">
        <h3 style="margin-bottom: 15px; font-size:16px;"><i class="fa-solid fa-plus-circle"></i> إضافة منتج جديد يدوياً</h3>
        <div class="flex-inputs">
            <div><label>الباركود / Ref:</label><input id="pRef" placeholder="أدخل أو امسح الباركود"></div>
            <div><label>اسم المنتج:</label><input id="pName" placeholder="اسم المنتج بالكامل"></div>
        </div>
        <div class="flex-inputs">
            <div><label>سعر الشراء (DA):</label><input id="pBuy" type="number" step="0.01" placeholder="0.00"></div>
            <div><label>سعر البيع الافتراضي (DA):</label><input id="pSell" type="number" step="0.01" placeholder="0.00"></div>
            <div><label>الكمية الابتدائية:</label><input id="pQty" type="number" step="0.01" placeholder="0"></div>
        </div>
        <button onclick="addProduct()" style="width: 100%; margin-top: 5px; background: var(--success-gradient); height: 45px;"><i class="fa-solid fa-plus"></i> إضافة المنتج للمخزن</button>
    </div>
    <div style="margin-top: 20px;">
        <label>🔍 بحث سريع وسلس في المنتجات:</label>
        <input id="productSearch" placeholder="ابحث باسم المنتج أو الرقم المتسلسل..." oninput="renderProducts()">
    </div>
    <div style="overflow-x: auto;">
        <table>
            <thead><tr><th>الباركود</th><th>اسم المنتج</th><th>الكمية الحالية</th><th>الشراء</th><th>البيع الافتراضي</th><th>تعديل</th><th>حذف</th></tr></thead>
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
    
    <!-- قسم التحكم العلوي برقم الطلب والتعديل الاسترجاعي -->
    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-bottom: 20px;">
        <div class="box" style="background: var(--text-main); color: white; padding: 15px; margin: 0; display: flex; align-items: center; justify-content: space-around; flex-wrap: wrap;">
            <span style="font-weight: 700; font-size: 15px;"><i class="fa-solid fa-receipt"></i> رقم الطلب الحالي:</span>
            <input id="cmdNumberInput" type="number" min="1" style="width: 100px; text-align: center; font-size: 18px; font-weight: 800; color: var(--text-main); background: #fff; padding: 6px;" oninput="updateCommandNumberManual()">
            <button class="del" onclick="resetCommandNumber()" style="padding: 8px 14px; font-size: 12px;"><i class="fa-solid fa-arrow-rotate-left"></i> تصفير</button>
        </div>
        <div class="box" style="background: #eff6ff; border: 1px solid #bfdbfe; padding: 15px; margin: 0; display: flex; align-items: center; gap: 10px;">
            <input id="searchOrderNumber" type="number" placeholder="رقم طلبية سابقة لتعديلها..." style="background: #fff;">
            <button onclick="loadOrderToEdit()" style="background: var(--purple-gradient); white-space: nowrap; padding: 11px 16px;"><i class="fa-solid fa-edit"></i> جلب للتعديل</button>
        </div>
    </div>

    <!-- شبكة البيع المنقسمة -->
    <div class="sales-grid">
        <!-- الجهة اليمنى: اختيار المنتج والتحكم بالسعر المعدل -->
        <div>
            <div class="box" style="background: #fff;">
                <h3 style="font-size: 16px; margin-bottom: 15px; color: var(--primary);"><i class="fa-solid fa-filter"></i> اختيار المنتج وتحديد السعر</h3>
                <div style="margin-bottom: 15px;">
                    <label>فصل وتصفية المنتجات:</label>
                    <input id="saleSearch" placeholder="اكتب اسم المنتج أو امسح الباركود للبحث..." oninput="renderSalesOptions()">
                </div>
                <div style="margin-bottom: 15px;">
                    <label>المنتج المستهدف حالياً:</label>
                    <select id="saleStock" onchange="updateDefaultSalePriceField()"></select>
                </div>
                
                <div class="flex-inputs">
                    <div>
                        <label>الكمية المراد بيعها:</label>
                        <input id="saleQty" type="number" step="1" value="1" style="background: #fff;">
                    </div>
                    <div>
                        <label style="color: var(--primary); font-weight: 800;"><i class="fa-solid fa-pen-clip"></i> سعر البيع الحالي (عدّله بحرية):</label>
                        <input id="salePriceInput" type="number" step="0.01" style="background: #fff; border: 2px solid var(--primary); font-size: 16px; font-weight: 700; color: var(--primary);">
                    </div>
                </div>
                <button onclick="addToCommand()" style="width: 100%; height: 48px; font-size: 15px; background: var(--primary-gradient);"><i class="fa-solid fa-cart-plus"></i> إضافة إلى السلة الحالية</button>
            </div>
            
            <h3 style="color: var(--text-muted); font-weight:700; font-size: 16px; margin-bottom: 12px;"><i class="fa-solid fa-clock-rotate-left"></i> سجل الطلبيات المبيوعة السابقة</h3>
            <div id="salesLog" style="max-height: 380px; overflow-y: auto;"></div>
        </div>

        <!-- الجهة اليسرى: السلة الحالية والمجموع والتأكيد -->
        <div class="box" style="background: #fff; border: 1px solid var(--primary); position: sticky; top: 10px;">
            <h3 style="margin-bottom: 15px; border-bottom: 1px solid var(--border); padding-bottom: 10px; font-size: 16px; color: var(--success);"><i class="fa-solid fa-basket-shopping"></i> سلة التسوق الحالية</h3>
            <div id="currentCommand" style="min-height: 150px; max-height: 300px; overflow-y: auto; margin-bottom: 15px;"></div>
            
            <div style="background: #f0fdf4; padding: 15px; border-radius: var(--radius-md); border: 1px solid #bbf7d0; text-align: left; margin-bottom: 15px;">
                <span style="color: #166534; font-size: 14px; font-weight: 700;">المجموع الإجمالي المستحق:</span>
                <h3 id="commandTotal" style="color: var(--success); font-size: 24px; font-weight: 900; margin-top: 2px;">0.00 DA</h3>
            </div>
            <button onclick="confirmCommand()" style="width:100%; background: var(--success-gradient); font-size: 16px; padding: 14px;"><i class="fa-solid fa-circle-check"></i> تأكيد وحفظ الطلب النهائي</button>
        </div>
    </div>
</div>

<!-- جرد المخزون الكلي - STOCK -->
<div id="stock" class="page">
    <div class="header">
        <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع للرئيسية</button>
        <h2><i class="fa-solid fa-warehouse" style="color:var(--primary);"></i> كشف وجرد المخزون الكلي</h2>
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
            <thead><tr><th>اسم المنتج</th><th>الكمية المتبقية</th><th>حالة خطورة المخزون وطبيعة التنبيه</th></tr></thead>
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
        <h3 style="margin-bottom: 15px; font-size:16px;"><i class="fa-solid fa-file-invoice-dollar"></i> تسجيل مصروف جديد وتدوينه</h3>
        <div style="margin-bottom: 15px;">
            <label>بيان المصروف ونوعه:</label>
            <input id="expTitle" placeholder="مثال: فاتورة الكهرباء، نقل السلعة، تالف...">
        </div>
        <div class="flex-inputs">
            <div><label>قيمة المصروف (DA):</label><input id="expAmount" type="number" step="0.01" placeholder="0.00"></div>
            <div><label>تاريخ التقييد:</label><input id="expDate" type="date"></div>
        </div>
        <button onclick="addExpense()" style="width: 100%; margin-top: 5px; background: var(--danger-gradient); height: 45px;"><i class="fa-solid fa-check"></i> حفظ وقيد المصروف بالدفتر</button>
    </div>
    <h3 style="color: var(--text-muted); font-weight:700; margin-top:25px; font-size: 16px;"><i class="fa-solid fa-receipt"></i> سجل المصاريف اليومية والسنوية المقيدة</h3>
    <div id="expensesLog" style="max-height: 400px; overflow-y: auto; margin-top: 15px;"></div>
</div>

<!-- تقارير الأرباح - PROFITS -->
<div id="profits" class="page">
    <div class="header">
        <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع للرئيسية</button>
        <h2><i class="fa-solid fa-chart-line" style="color:var(--success);"></i> التقارير المالية والأرباح الصافية الحقيقية</h2>
    </div>
    <div class="box" style="background: #fff;">
        <h3 style="margin-bottom: 15px; font-size:16px; color: #a855f7;"><i class="fa-solid fa-calendar-days"></i> فرز واحتساب الأرباح بفترة زمنية مخصصة 🗓️</h3>
        <div class="flex-inputs">
            <div><label>من تاريخ 📅:</label><input type="date" id="filterFrom" onchange="calculateFilteredProfit()"></div>
            <div><label>إلى تاريخ 🏁:</label><input type="date" id="filterTo" onchange="calculateFilteredProfit()"></div>
        </div>
    </div>
    <div class="profit-grid">
        <div class="profit-card filter" style="grid-column: span 2 / span 2;">
            <p>🎯 صافي فائدة الفترة المحددة بالفرز أعلاه (فائدة المبيعات المعدلة - المصاريف)</p>
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
            <p>📉 إجمالي مصاريف السنة المسجلة بالكامل</p>
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
        <div style="display:flex; justify-content:space-between; align-items:center; margin:8px 0; background:#f8fafc; padding:10px 14px; border-radius:8px; border:1px solid var(--border);">
            <span><b>${i.name}</b> <span class="badge-qty">x${i.qty}</span> <small style="color:var(--text-muted);">(@ ${i.sell.toFixed(2)} DA)</small></span>
            <div style="display:flex; align-items:center; gap:10px;">
                <span style="color:var(--primary); font-weight:700;">${(i.sell*i.qty).toFixed(2)} DA</span>
                <button class="del" onclick="removeFromCommand(${idx})" style="padding:5px 10px; font-size:12px;"><i class="fa-solid fa-trash"></i></button>
            </div>
        </div>`;
    }).join("");
    commandTotal.innerHTML = total.toFixed(2) + " DA";
}

function removeFromCommand(i) { currentCommandData.splice(i,1); updateCommandUI(); }

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
        <td><span class="badge-qty" style="background:#e0f2fe; color:#0369a1;">${b.qty} قطع</span></td>
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
        <tr style="background: #f1f5f9;">
            <td style="color: var(--text-main); font-weight:800; text-align:right;">📦 إجمالي المخزون:</td>
            <td style="color: #0284c7; font-weight:800;">${totalPieces} قطعة</td>
            <td style="color: #b91c1c; font-weight:800;">${totalCapital.toFixed(2)} DA</td>
            <td style="color: #047857; font-weight:800;">${(totalValue - totalCapital).toFixed(2)} DA</td>
            <td></td>
        </tr>`;

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
                    <span style="font-weight:600;">${(item.sell * item.qty).toFixed(2)} DA</span>
                </div>
            `).join("");
            return `
            <div class="order-card">
                <div class="order-card-header">
                    <span style="font-weight:800; font-size:15px; color:var(--primary);">الطلبية # ${cmdNum}</span>
                    <div style="display:flex; gap:6px;">
                        <button onclick="document.getElementById('searchOrderNumber').value=${cmdNum}; loadOrderToEdit();" style="padding:5px 10px; font-size:11px; background:var(--purple-gradient);"><i class="fa-solid fa-pen"></i> جلب</button>
                        <button class="del" onclick="deleteEntireOrder(${cmdNum})" style="padding:5px 10px; font-size:11px;"><i class="fa-solid fa-trash"></i> إلغاء</button>
                    </div>
                </div>
                <div>${itemsHTML}</div>
                <div style="display:flex; justify-content:space-between; margin-top:10px; padding-top:6px; border-top:1px solid var(--border); font-size:13px; font-weight:700;">
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
        <div class="order-card" style="border-right: 4px solid var(--danger); display:flex; justify-content:space-between; align-items:center;">
            <span>💸 <b>${e.title}</b> <small style="color:var(--text-muted); margin-right:8px;">(${e.date})</small></span>
            <div style="display:flex; align-items:center; gap:15px;">
                <b style="color:var(--danger);">${e.amount.toFixed(2)} DA</b>
                <button class="del" onclick="deleteExpense(${e.id})" style="padding:5px 10px; font-size:12px;"><i class="fa-solid fa-trash"></i></button>
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

    let lowItems = batches.filter(b => b.qty <= 15); lowItems.sort((a, b) => a.qty - b.qty);
    document.getElementById('lowTable').innerHTML = lowItems.map(b => {
        let rowClass = "", statusText = "";
        if (b.qty === 0) { rowClass = "stock-empty"; statusText = "منتهي تماماً (0 قطع) ❌"; } 
        else if (b.qty <= 5) { rowClass = "stock-danger"; statusText = "نقص حاد جداً (1-5 قطع) 🚨"; } 
        else if (b.qty <= 10) { rowClass = "stock-warning"; statusText = "نقص متوسط (6-10 قطع) ⚠️"; } 
        else if (b.qty <= 15) { rowClass = "stock-notice"; statusText = "بداية نقص (11-15 قطعة) ℹ️"; }
        return `<tr class="${rowClass}"><td><b>${b.name}</b></td><td><b>${b.qty} قطعة</b></td><td><b>${statusText}</b></td></tr>`;
    }).join("");
    if(lowItems.length === 0) document.getElementById('lowTable').innerHTML = `<tr><td colspan="3" style="color:var(--success); font-weight:700; padding:20px;">🎉 كل السلع متوفرة بكميات ممتازة</td></tr>`;
    
    document.getElementById('cmdNumberInput').value = commandNumber;
}

function exportData(){
    let dataStr = JSON.stringify({ batches, sales, expenses, commandNumber });
    let dataUri = 'data:application/json;charset=utf-8,'+ encodeURIComponent(dataStr);
    let linkElement = document.createElement('a');
    linkElement.setAttribute('href', dataUri); linkElement.setAttribute('download', 'pos_premium_backup.json');
    linkElement.click();
}
</script>
</body>
</html>

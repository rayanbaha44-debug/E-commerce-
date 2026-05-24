<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>POS SYSTEM EXECUTIVE</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
<style>
:root {
  --primary: #3b82f6;
  --primary-g: linear-gradient(135deg,#3b82f6,#1d4ed8);
  --success: #10b981;
  --success-g: linear-gradient(135deg,#10b981,#059669);
  --danger: #ef4444;
  --danger-g: linear-gradient(135deg,#ef4444,#b91c1c);
  --warning: #f59e0b;
  --warning-g: linear-gradient(135deg,#f59e0b,#d97706);
  --purple-g: linear-gradient(135deg,#a855f7,#7e22ce);
  --gold-g: linear-gradient(135deg,#f59e0b,#b45309);
  --bg: #090d16;
  --surface: rgba(22,30,49,0.85);
  --card: #1f2937;
  --border: rgba(255,255,255,0.08);
  --text: #ffffff;
  --muted: #9ca3af;
  --r-xl: 24px; --r-lg: 16px; --r-md: 12px;
}
*{margin:0;padding:0;box-sizing:border-box;font-family:'Cairo',sans-serif;}
body{background:linear-gradient(135deg,#090d16,#111827);color:var(--text);min-height:100vh;padding:30px 16px;display:flex;flex-direction:column;align-items:center;}

/* ===== TOAST ===== */
#toast-container{position:fixed;top:24px;left:50%;transform:translateX(-50%);z-index:9999;display:flex;flex-direction:column;gap:10px;pointer-events:none;}
.toast{padding:14px 28px;border-radius:var(--r-md);font-weight:700;font-size:15px;color:#fff;opacity:0;transform:translateY(-20px);transition:all .35s cubic-bezier(.16,1,.3,1);pointer-events:none;box-shadow:0 8px 30px rgba(0,0,0,.5);white-space:nowrap;}
.toast.show{opacity:1;transform:translateY(0);}
.toast.success{background:var(--success-g);}
.toast.error{background:var(--danger-g);}
.toast.info{background:var(--primary-g);}
.toast.warning{background:var(--warning-g);}

/* ===== DASHBOARD ===== */
#dashboard{display:grid;grid-template-columns:repeat(auto-fit,minmax(250px,1fr));gap:22px;width:100%;max-width:1100px;margin:30px auto;}
.logo-header{width:100%;max-width:1100px;text-align:center;margin-bottom:10px;}
.logo-header h1{font-size:28px;font-weight:900;background:var(--primary-g);-webkit-background-clip:text;-webkit-text-fill-color:transparent;}
.logo-header p{color:var(--muted);font-size:14px;margin-top:4px;}

.card{background:var(--surface);backdrop-filter:blur(12px);padding:32px 20px;border-radius:var(--r-xl);text-align:center;cursor:pointer;border:1px solid rgba(255,255,255,0.05);font-weight:700;font-size:17px;color:var(--text);transition:all .3s cubic-bezier(.4,0,.2,1);box-shadow:0 10px 30px -5px rgba(0,0,0,.5);display:flex;flex-direction:column;align-items:center;justify-content:center;gap:15px;position:relative;overflow:hidden;}
.card::after{content:'';position:absolute;bottom:0;left:0;width:100%;height:4px;background:var(--primary-g);transform:scaleX(0);transition:transform .3s ease;}
.card:hover::after{transform:scaleX(1);}
.card i{font-size:36px;background:var(--primary-g);-webkit-background-clip:text;-webkit-text-fill-color:transparent;transition:transform .3s ease;}
.card:hover{transform:translateY(-7px);box-shadow:0 20px 40px -10px rgba(37,99,235,.4);border-color:rgba(59,130,246,.35);background:rgba(31,41,55,.9);}
.card:hover i{transform:scale(1.15) rotate(3deg);}
.card.gold-card{border:1px dashed rgba(245,158,11,.4);background:rgba(245,158,11,.03);}
.card.gold-card i{background:var(--gold-g);-webkit-background-clip:text;}
.card.gold-card::after{background:var(--gold-g);}

/* ===== PAGE ===== */
.page{display:none;width:100%;max-width:1200px;background:rgba(17,24,39,.88);backdrop-filter:blur(20px);padding:36px 32px;border-radius:var(--r-xl);box-shadow:0 30px 60px -15px rgba(0,0,0,.7);border:1px solid rgba(255,255,255,.1);animation:slideUp .45s cubic-bezier(.16,1,.3,1);}
@keyframes slideUp{from{opacity:0;transform:translateY(18px);}to{opacity:1;transform:translateY(0);}}
.page.active{display:block;}

.header{display:flex;justify-content:space-between;align-items:center;margin-bottom:28px;padding-bottom:22px;border-bottom:1px solid var(--border);}
.header h2{font-size:22px;font-weight:800;display:flex;align-items:center;gap:12px;}

/* ===== BUTTONS ===== */
button{padding:12px 22px;border:none;border-radius:var(--r-md);cursor:pointer;background:var(--primary-g);color:#fff;font-weight:700;font-size:14px;transition:all .22s cubic-bezier(.4,0,.2,1);display:inline-flex;align-items:center;justify-content:center;gap:8px;box-shadow:0 4px 12px rgba(37,99,235,.2);}
button:hover{opacity:.93;transform:translateY(-2px);box-shadow:0 6px 20px rgba(37,99,235,.35);}
button:active{transform:translateY(0);}
.btn-back{background:#374151;box-shadow:none;}
.btn-back:hover{background:#4b5563;}
.btn-danger{background:var(--danger-g);box-shadow:0 4px 12px rgba(239,68,68,.2);}
.btn-danger:hover{box-shadow:0 6px 20px rgba(239,68,68,.35);}
.btn-edit{background:#1f2937;color:var(--primary);border:1px solid rgba(59,130,246,.3);box-shadow:none;}
.btn-edit:hover{background:var(--primary);color:#fff;}
.btn-success{background:var(--success-g);box-shadow:0 4px 12px rgba(16,185,129,.2);}
.btn-success:hover{box-shadow:0 6px 20px rgba(16,185,129,.35);}
.btn-gold{background:var(--gold-g);box-shadow:0 4px 12px rgba(245,158,11,.2);}
.btn-gold:hover{box-shadow:0 6px 20px rgba(245,158,11,.35);}

/* ===== INPUTS ===== */
label{display:block;font-size:13px;font-weight:700;color:var(--muted);margin-bottom:6px;}
input,select{width:100%;padding:13px 16px;border-radius:var(--r-md);border:1px solid rgba(255,255,255,.14);background:#111827;color:var(--text);font-size:14px;font-weight:600;transition:all .22s ease;}
input:focus,select:focus{outline:none;border-color:var(--primary);background:#090d16;box-shadow:0 0 0 3px rgba(59,130,246,.25);}
.input-error{border-color:var(--danger)!important;background:rgba(239,68,68,.08)!important;box-shadow:0 0 0 3px rgba(239,68,68,.25)!important;animation:shake .3s ease;}
@keyframes shake{0%,100%{transform:translateX(0);}25%{transform:translateX(-5px);}75%{transform:translateX(5px);}}

.box{background:rgba(9,13,22,.55);padding:22px;border-radius:var(--r-lg);margin-bottom:22px;border:1px solid var(--border);}
.flex-row{display:flex;gap:14px;flex-wrap:wrap;}
.flex-row>div{flex:1;min-width:160px;}

/* ===== SALES GRID ===== */
.sales-grid{display:grid;grid-template-columns:1.15fr 1fr;gap:26px;align-items:start;}
@media(max-width:900px){.sales-grid{grid-template-columns:1fr;}}

/* ===== TABLES ===== */
.table-wrap{overflow-x:auto;border-radius:var(--r-lg);border:1px solid rgba(255,255,255,.1);box-shadow:0 15px 30px rgba(0,0,0,.45);}
table{width:100%;border-collapse:collapse;table-layout:auto;}
th,td{padding:16px 13px;text-align:center;font-size:14px;vertical-align:middle;}
th{background:#0d1526;color:var(--muted);font-weight:700;border-bottom:2px solid rgba(255,255,255,.12);}
td{background:#1a2235;border-bottom:1px solid rgba(255,255,255,.05);color:#fff;font-weight:600;}
tr:last-child td{border-bottom:none;}
tr:hover td{background:#1e3a5f;transition:background .12s;}
td code{background:rgba(0,0,0,.4);padding:5px 10px;border-radius:7px;color:#38bdf8;font-size:13px;border:1px solid rgba(56,189,248,.2);font-weight:700;display:inline-block;max-width:170px;word-break:break-all;white-space:normal;}
tr:hover td code{color:#fff;border-color:#fff;}
tfoot tr td{background:#0d1526!important;font-weight:800;color:#fff;}

/* ===== ORDER CARDS ===== */
.order-card{background:#1a2235;border:1px solid var(--border);border-radius:var(--r-lg);padding:18px;margin-bottom:16px;}
.order-card-hd{display:flex;justify-content:space-between;align-items:center;border-bottom:1px dashed var(--border);padding-bottom:10px;margin-bottom:10px;}
.order-item-line{display:flex;justify-content:space-between;padding:6px 0;font-size:13px;border-bottom:1px solid rgba(255,255,255,.03);}
.badge-qty{background:#111827;color:var(--warning);padding:3px 10px;border-radius:7px;font-weight:800;font-size:12px;border:1px solid rgba(245,158,11,.3);}

/* ===== STAT CARDS GRID ===== */
.stat-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(210px,1fr));gap:18px;margin-bottom:24px;}
.stat-card{background:#1a2235;padding:22px;border-radius:var(--r-lg);border:1px solid var(--border);border-right:5px solid var(--primary);}
.stat-card p{color:var(--muted);font-size:13px;font-weight:700;margin-bottom:6px;}
.stat-card .amt{font-size:22px;font-weight:900;}
.span-2{grid-column:span 2/span 2;}
@media(max-width:600px){.span-2{grid-column:span 1/span 1;}}

/* ===== RISK BADGE ===== */
.risk-badge{padding:5px 11px;border-radius:6px;font-weight:800;font-size:12px;display:inline-block;color:#fff;}

/* ===== NET PROFIT SECTION (NEW) ===== */
#netprofit.page{border-top:3px solid #f59e0b;}
.net-hero{background:linear-gradient(135deg,rgba(245,158,11,.12),rgba(180,83,9,.08));border:2px solid rgba(245,158,11,.35);border-radius:var(--r-xl);padding:36px 28px;text-align:center;margin-bottom:30px;position:relative;overflow:hidden;}
.net-hero::before{content:'';position:absolute;inset:0;background:radial-gradient(ellipse at 50% 0%,rgba(245,158,11,.18),transparent 65%);pointer-events:none;}
.net-hero .label{color:var(--warning);font-weight:700;font-size:14px;letter-spacing:.08em;text-transform:uppercase;margin-bottom:10px;}
.net-hero .big-amount{font-size:52px;font-weight:900;letter-spacing:-.02em;line-height:1;}
.net-hero .formula-text{color:var(--muted);font-size:13px;margin-top:12px;font-weight:600;}
.net-hero .big-amount.positive{color:#34d399;}
.net-hero .big-amount.negative{color:#f87171;}
.net-hero .big-amount.zero{color:var(--warning);}

.net-row-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:18px;margin-bottom:28px;}
.net-row-card{background:#1a2235;border-radius:var(--r-lg);padding:22px;border:1px solid var(--border);display:flex;flex-direction:column;gap:8px;}
.net-row-card .nr-label{font-size:13px;color:var(--muted);font-weight:700;}
.net-row-card .nr-val{font-size:20px;font-weight:900;}
.net-row-card .nr-formula{font-size:11px;color:rgba(255,255,255,.3);font-weight:600;margin-top:2px;}

.base-input-row{background:rgba(245,158,11,.06);border:1px solid rgba(245,158,11,.25);border-radius:var(--r-lg);padding:20px;margin-bottom:22px;display:flex;align-items:center;gap:18px;flex-wrap:wrap;}
.base-input-row label{color:var(--warning);font-size:14px;font-weight:800;margin:0;white-space:nowrap;}
.base-input-row input{max-width:200px;background:#111827;border-color:rgba(245,158,11,.3);color:var(--warning);font-size:16px;font-weight:900;text-align:center;}
.base-input-row input:focus{border-color:var(--warning);box-shadow:0 0 0 3px rgba(245,158,11,.2);}

.formula-breakdown{background:#0d1526;border-radius:var(--r-lg);padding:20px;border:1px solid rgba(255,255,255,.07);}
.formula-breakdown h4{font-size:15px;font-weight:800;margin-bottom:16px;color:var(--muted);}
.fb-line{display:flex;justify-content:space-between;align-items:center;padding:12px 0;border-bottom:1px solid rgba(255,255,255,.05);}
.fb-line:last-child{border-bottom:none;}
.fb-line .fb-name{font-size:14px;font-weight:700;color:var(--muted);}
.fb-line .fb-op{font-size:13px;font-weight:800;padding:3px 10px;border-radius:6px;background:rgba(255,255,255,.08);}
.fb-line .fb-val{font-size:16px;font-weight:900;}
.fb-total-line{display:flex;justify-content:space-between;align-items:center;padding:16px;margin-top:12px;border-radius:var(--r-md);background:linear-gradient(135deg,rgba(245,158,11,.12),rgba(180,83,9,.08));border:2px solid rgba(245,158,11,.3);}
.fb-total-line .ft-label{font-size:16px;font-weight:800;color:var(--warning);}
.fb-total-line .ft-val{font-size:24px;font-weight:900;}

.period-filter-bar{background:rgba(59,130,246,.05);border:1px solid rgba(59,130,246,.2);border-radius:var(--r-lg);padding:18px;margin-bottom:22px;}
.period-filter-bar h4{font-size:14px;font-weight:800;color:var(--primary);margin-bottom:12px;}

::-webkit-scrollbar{width:8px;}
::-webkit-scrollbar-track{background:#090d16;}
::-webkit-scrollbar-thumb{background:#374151;border-radius:4px;}
::-webkit-scrollbar-thumb:hover{background:#4b5563;}
</style>
</head>
<body>

<div id="toast-container"></div>

<!-- ===== DASHBOARD ===== -->
<div class="logo-header">
  <h1>POS SYSTEM EXECUTIVE</h1>
  <p>نظام نقطة البيع المتكامل - الجزائر</p>
</div>
<div id="dashboard">
  <div class="card" onclick="openPage('products')">
    <i class="fa-solid fa-box-open"></i>
    إدارة المنتجات والمخزن
  </div>
  <div class="card" onclick="openPage('sales')">
    <i class="fa-solid fa-cash-register"></i>
    واجهة البيع السريعة
  </div>
  <div class="card" onclick="openPage('stock')">
    <i class="fa-solid fa-warehouse"></i>
    جرد المخزون الكلي
  </div>
  <div class="card" onclick="openPage('low')">
    <i class="fa-solid fa-triangle-exclamation" style="background:var(--warning-g);-webkit-background-clip:text;"></i>
    السلع الناقصة بالمحل
  </div>
  <div class="card" onclick="openPage('expenses')">
    <i class="fa-solid fa-hand-holding-dollar" style="background:var(--danger-g);-webkit-background-clip:text;"></i>
    إدارة المصاريف الكلية
  </div>
  <div class="card" onclick="openPage('profits')">
    <i class="fa-solid fa-chart-line" style="background:var(--success-g);-webkit-background-clip:text;"></i>
    تقارير الأرباح الصافية
  </div>
  <div class="card gold-card" onclick="openPage('netprofit')">
    <i class="fa-solid fa-coins"></i>
    الفائدة الصافية
  </div>
  <div class="card" onclick="exportData()" style="border:1px dashed rgba(16,185,129,.3);">
    <i class="fa-solid fa-file-export" style="background:var(--success-g);-webkit-background-clip:text;"></i>
    تصدير نسخة احتياطية
  </div>
  <div class="card" onclick="triggerImport()" style="border:1px dashed rgba(168,85,247,.3);">
    <i class="fa-solid fa-file-import" style="background:var(--purple-g);-webkit-background-clip:text;"></i>
    استيراد نسخة من الكمبيوتر
  </div>
</div>
<input type="file" id="importFileInput" accept=".json" style="display:none;" onchange="importData(event)">

<!-- ===== PAGE: PRODUCTS ===== -->
<div id="products" class="page">
  <div class="header">
    <button class="btn-back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع</button>
    <h2><i class="fa-solid fa-box-open" style="color:var(--primary);"></i> إدارة المنتجات والمخزن</h2>
  </div>
  <div class="box">
    <h3 style="margin-bottom:18px;font-size:16px;"><i class="fa-solid fa-plus-circle"></i> إضافة منتج جديد</h3>
    <div class="flex-row" style="margin-bottom:14px;">
      <div><label>الباركود / Ref (فريد):</label><input id="pRef" placeholder="امسح أو أدخل يدوياً" oninput="checkRefUniq()"></div>
      <div><label>اسم المنتج:</label><input id="pName" placeholder="اسم المنتج كاملاً"></div>
    </div>
    <div class="flex-row" style="margin-bottom:14px;">
      <div><label>سعر الشراء (DA):</label><input id="pBuy" type="number" step="0.01" placeholder="0.00" oninput="checkPriceValid()"></div>
      <div><label>سعر البيع الافتراضي (DA):</label><input id="pSell" type="number" step="0.01" placeholder="0.00" oninput="checkPriceValid()"></div>
      <div><label>الكمية الابتدائية:</label><input id="pQty" type="number" step="0.01" placeholder="0"></div>
    </div>
    <button class="btn-success" onclick="addProduct()" style="width:100%;height:48px;font-size:15px;">
      <i class="fa-solid fa-plus"></i> إضافة المنتج للمخزن
    </button>
  </div>
  <div style="margin-bottom:12px;">
    <label>بحث ترتيبي:</label>
    <input id="productSearch" placeholder="ابحث بالاسم أو الباركود..." oninput="renderProducts()">
  </div>
  <div class="table-wrap">
    <table>
      <thead><tr><th>الباركود</th><th>اسم المنتج</th><th>الكمية</th><th>الشراء (DA)</th><th>البيع (DA)</th><th>تعديل</th><th>حذف</th></tr></thead>
      <tbody id="productTable"></tbody>
    </table>
  </div>
</div>

<!-- ===== PAGE: SALES ===== -->
<div id="sales" class="page" style="max-width:1300px;">
  <div class="header">
    <button class="btn-back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع</button>
    <h2><i class="fa-solid fa-cash-register" style="color:var(--primary);"></i> واجهة البيع السريعة</h2>
  </div>
  <div style="display:grid;grid-template-columns:1fr 1fr;gap:16px;margin-bottom:22px;">
    <div class="box" style="margin:0;padding:14px;display:flex;align-items:center;justify-content:space-around;flex-wrap:wrap;gap:10px;background:#111827;">
      <span style="font-weight:700;font-size:15px;"><i class="fa-solid fa-receipt"></i> رقم الطلب:</span>
      <input id="cmdNumberInput" type="number" min="1" style="width:100px;text-align:center;font-size:18px;font-weight:900;background:#1a2235;padding:8px;" oninput="updateCmdNumManual()">
      <button class="btn-danger" onclick="resetCmdNum()" style="padding:9px 14px;font-size:12px;">
        <i class="fa-solid fa-arrow-rotate-left"></i> تصفير
      </button>
    </div>
    <div class="box" style="margin:0;padding:14px;display:flex;align-items:center;gap:12px;background:rgba(59,130,246,.05);border-color:rgba(59,130,246,.2);">
      <input id="searchOrderNumber" type="number" placeholder="رقم طلبية للتعديل..." style="background:#1a2235;">
      <button onclick="loadOrderToEdit()" style="background:var(--purple-g);white-space:nowrap;padding:12px 18px;font-size:13px;">
        <i class="fa-solid fa-edit"></i> جلب للتعديل
      </button>
    </div>
  </div>
  <div class="sales-grid">
    <div>
      <div class="box">
        <h3 style="font-size:16px;margin-bottom:16px;color:var(--primary);"><i class="fa-solid fa-filter"></i> اختيار المنتج وتحديد السعر</h3>
        <div style="margin-bottom:14px;">
          <label>فلترة المنتجات:</label>
          <input id="saleSearch" placeholder="اكتب اسم المنتج أو امسح الباركود..." oninput="renderSalesOptions()">
        </div>
        <div style="margin-bottom:14px;">
          <label>المنتج المستهدف:</label>
          <select id="saleStock" onchange="updateSalePrice()"></select>
        </div>
        <div class="flex-row" style="margin-bottom:14px;">
          <div><label>الكمية:</label><input id="saleQty" type="number" step="1" value="1"></div>
          <div>
            <label style="color:var(--primary);font-weight:800;"><i class="fa-solid fa-pen-clip"></i> سعر البيع (عدّله):</label>
            <input id="salePriceInput" type="number" step="0.01" style="border:2px solid var(--primary);font-size:16px;font-weight:700;">
          </div>
        </div>
        <button onclick="addToCommand()" style="width:100%;height:48px;font-size:15px;">
          <i class="fa-solid fa-cart-plus"></i> إضافة إلى السلة
        </button>
      </div>
      <h3 style="font-weight:700;font-size:16px;margin-bottom:12px;"><i class="fa-solid fa-clock-rotate-left"></i> سجل الطلبيات السابقة</h3>
      <div id="salesLog" style="max-height:380px;overflow-y:auto;"></div>
    </div>
    <div class="box" style="border:1px solid rgba(16,185,129,.3);background:rgba(17,24,39,.65);position:sticky;top:20px;">
      <h3 style="margin-bottom:16px;padding-bottom:10px;border-bottom:1px solid var(--border);font-size:16px;color:var(--success);">
        <i class="fa-solid fa-basket-shopping"></i> السلة الحالية
      </h3>
      <div id="currentCommand" style="min-height:140px;max-height:300px;overflow-y:auto;margin-bottom:18px;"></div>
      <div style="background:rgba(16,185,129,.05);padding:18px;border-radius:var(--r-md);border:1px solid rgba(16,185,129,.2);margin-bottom:18px;">
        <span style="color:var(--success);font-size:14px;font-weight:700;">المجموع الإجمالي المستحق:</span>
        <h3 id="commandTotal" style="color:var(--success);font-size:26px;font-weight:900;margin-top:4px;">0.00 DA</h3>
      </div>
      <button onclick="confirmCommand()" class="btn-success" style="width:100%;font-size:16px;padding:15px;">
        <i class="fa-solid fa-circle-check"></i> تأكيد وحفظ الطلب
      </button>
    </div>
  </div>
</div>

<!-- ===== PAGE: STOCK ===== -->
<div id="stock" class="page">
  <div class="header">
    <button class="btn-back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع</button>
    <h2><i class="fa-solid fa-warehouse" style="color:var(--primary);"></i> جرد المخزون الكلي</h2>
  </div>
  <div class="stat-grid" style="margin-bottom:24px;">
    <div class="stat-card">
      <p>اجمالي السلع بالمخزن</p>
      <div id="topStockPieces" class="amt" style="color:#60a5fa;">0 قطعة</div>
    </div>
    <div class="stat-card" style="border-right-color:var(--danger);">
      <p>رأس المال المستثمر</p>
      <div id="topStockCapital" class="amt" style="color:#fca5a5;">0.00 DA</div>
    </div>
    <div class="stat-card" style="border-right-color:var(--success);">
      <p>الأرباح المتوقعة</p>
      <div id="topStockProfit" class="amt" style="color:var(--success);">0.00 DA</div>
    </div>
  </div>
  <div class="table-wrap">
    <table>
      <thead><tr><th>اسم المنتج</th><th>الكمية</th><th>رأس المال</th><th>الربح المتوقع</th><th>إجراء</th></tr></thead>
      <tbody id="stockTable"></tbody>
      <tfoot id="stockFoot"></tfoot>
    </table>
  </div>
</div>

<!-- ===== PAGE: LOW STOCK ===== -->
<div id="low" class="page">
  <div class="header">
    <button class="btn-back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع</button>
    <h2><i class="fa-solid fa-triangle-exclamation" style="color:var(--warning);"></i> السلع الناقصة (مرتبة بدرجة الخطورة)</h2>
  </div>
  <div class="table-wrap">
    <table>
      <thead>
        <tr><th>الباركود</th><th>اسم المنتج</th><th>الكمية المتبقية</th><th>سعر الشراء (DA)</th><th>درجة الخطورة</th><th>حالة التنبيه</th></tr>
      </thead>
      <tbody id="lowTable"></tbody>
    </table>
  </div>
</div>

<!-- ===== PAGE: EXPENSES ===== -->
<div id="expenses" class="page">
  <div class="header">
    <button class="btn-back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع</button>
    <h2><i class="fa-solid fa-hand-holding-dollar" style="color:var(--danger);"></i> إدارة المصاريف الكلية</h2>
  </div>
  <div class="box">
    <h3 style="margin-bottom:16px;font-size:16px;"><i class="fa-solid fa-file-invoice-dollar"></i> تسجيل مصروف جديد</h3>
    <div style="margin-bottom:14px;"><label>بيان المصروف ونوعه:</label><input id="expTitle" placeholder="مثال: فاتورة الكهرباء، نقل، تالف..."></div>
    <div class="flex-row" style="margin-bottom:14px;">
      <div><label>القيمة (DA):</label><input id="expAmount" type="number" step="0.01" placeholder="0.00"></div>
      <div><label>التاريخ:</label><input id="expDate" type="date"></div>
    </div>
    <button class="btn-danger" onclick="addExpense()" style="width:100%;height:48px;font-size:15px;">
      <i class="fa-solid fa-check"></i> حفظ وقيد المصروف
    </button>
  </div>
  <h3 style="font-weight:700;font-size:16px;margin-bottom:12px;"><i class="fa-solid fa-receipt"></i> سجل المصاريف المقيدة</h3>
  <div id="expensesLog" style="max-height:400px;overflow-y:auto;"></div>
</div>

<!-- ===== PAGE: PROFITS ===== -->
<div id="profits" class="page">
  <div class="header">
    <button class="btn-back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع</button>
    <h2><i class="fa-solid fa-chart-line" style="color:var(--success);"></i> تقارير الأرباح الصافية</h2>
  </div>
  <div class="box" style="background:rgba(17,24,39,.6);">
    <h3 style="margin-bottom:16px;font-size:16px;color:#a855f7;"><i class="fa-solid fa-calendar-days"></i> فرز بفترة زمنية مخصصة</h3>
    <div class="flex-row">
      <div><label>من تاريخ:</label><input type="date" id="filterFrom" onchange="calcProfits()"></div>
      <div><label>الى تاريخ:</label><input type="date" id="filterTo" onchange="calcProfits()"></div>
    </div>
  </div>
  <div class="stat-grid">
    <div class="stat-card span-2" style="border-right-color:#a855f7;background:rgba(168,85,247,.05);">
      <p>صافي فائدة الفترة المحددة (مبيعات - مصاريف)</p>
      <div id="filteredProfit" class="amt" style="color:#c084fc;">0.00 DA</div>
    </div>
    <div class="stat-card" style="border-right-color:var(--success);">
      <p>صافي أرباح اليوم الحالي</p>
      <div id="dailyProfit" class="amt" style="color:var(--success);">0.00 DA</div>
    </div>
    <div class="stat-card">
      <p>صافي أرباح الشهر الحالي</p>
      <div id="monthlyProfit" class="amt" style="color:var(--primary);">0.00 DA</div>
    </div>
    <div class="stat-card span-2" style="border-right-color:var(--danger);background:rgba(239,68,68,.04);">
      <p>اجمالي مصاريف السنة</p>
      <div id="totalExpensesYear" class="amt" style="color:#fca5a5;">0.00 DA</div>
    </div>
    <div class="stat-card span-2" style="border-right-color:#cbd5e1;">
      <p>صافي فائدة السنة الحقيقية</p>
      <div id="yearlyProfit" class="amt">0.00 DA</div>
    </div>
  </div>
</div>

<!-- ===== PAGE: NET PROFIT (NEW) ===== -->
<div id="netprofit" class="page">
  <div class="header">
    <button class="btn-back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع</button>
    <h2><i class="fa-solid fa-coins" style="color:var(--warning);"></i> الفائدة الصافية</h2>
  </div>

  <!-- Base Amount Input -->
  <div class="base-input-row">
    <label><i class="fa-solid fa-lock"></i> المبلغ المرجعي (DA):</label>
    <input id="baseAmountInput" type="number" step="0.01" value="14900" oninput="calcNetProfit()">
    <span style="color:var(--muted);font-size:13px;font-weight:700;">هذا هو المبلغ الثابت للباك — يمكن تعديله متى أردت</span>
  </div>

  <!-- Period Filter -->
  <div class="period-filter-bar">
    <h4><i class="fa-solid fa-calendar-days"></i> اختر الفترة الزمنية للحساب:</h4>
    <div class="flex-row">
      <div><label>من تاريخ:</label><input type="date" id="npFilterFrom" onchange="calcNetProfit()"></div>
      <div><label>الى تاريخ:</label><input type="date" id="npFilterTo" onchange="calcNetProfit()"></div>
    </div>
  </div>

  <!-- Big Hero Result -->
  <div class="net-hero">
    <div class="label">الفائدة الصافية النهائية</div>
    <div id="netHeroBig" class="big-amount zero">14,900.00 DA</div>
    <div id="netHeroFormula" class="formula-text">14,900.00 - 0.00 (مبيعات) - 0.00 (مصاريف) = 14,900.00 DA</div>
  </div>

  <!-- Row Cards -->
  <div class="net-row-grid">
    <div class="net-row-card" style="border:1px solid rgba(245,158,11,.3);">
      <div class="nr-label">المبلغ المرجعي الثابت</div>
      <div id="npBaseDisp" class="nr-val" style="color:var(--warning);">14,900.00 DA</div>
      <div class="nr-formula">باك المحل الثابت</div>
    </div>
    <div class="net-row-card" style="border:1px solid rgba(59,130,246,.25);">
      <div class="nr-label">اجمالي المبيعات (المستحق)</div>
      <div id="npSalesDisp" class="nr-val" style="color:#60a5fa;">0.00 DA</div>
      <div class="nr-formula">مجموع كل الطلبيات بالفترة</div>
    </div>
    <div class="net-row-card" style="border:1px solid rgba(239,68,68,.25);">
      <div class="nr-label">اجمالي المصاريف</div>
      <div id="npExpDisp" class="nr-val" style="color:#fca5a5;">0.00 DA</div>
      <div class="nr-formula">مجموع المصاريف المقيدة بالفترة</div>
    </div>
  </div>

  <!-- Formula Breakdown -->
  <div class="formula-breakdown">
    <h4><i class="fa-solid fa-calculator"></i> تفصيل آلية الحساب الرياضي</h4>
    <div class="fb-line">
      <span class="fb-name">المبلغ المرجعي الثابت</span>
      <span class="fb-op" style="color:var(--warning);">قيمة أساسية</span>
      <span id="npFbBase" class="fb-val" style="color:var(--warning);">14,900.00 DA</span>
    </div>
    <div class="fb-line">
      <span class="fb-name">اجمالي المبيعات (المستحق)</span>
      <span class="fb-op" style="color:#60a5fa;">- طرح</span>
      <span id="npFbSales" class="fb-val" style="color:#60a5fa;">0.00 DA</span>
    </div>
    <div class="fb-line">
      <span class="fb-name">اجمالي المصاريف المقيدة</span>
      <span class="fb-op" style="color:#fca5a5;">- طرح</span>
      <span id="npFbExp" class="fb-val" style="color:#fca5a5;">0.00 DA</span>
    </div>
    <div class="fb-total-line">
      <span class="ft-label"><i class="fa-solid fa-equals"></i> الفائدة الصافية النهائية</span>
      <span id="npFbResult" class="ft-val" style="color:var(--warning);">14,900.00 DA</span>
    </div>
  </div>

  <!-- Live Sales List for Period -->
  <h3 style="font-weight:700;font-size:16px;margin:28px 0 14px;"><i class="fa-solid fa-list-check" style="color:var(--primary);"></i> تفصيل الطلبيات بالفترة المحددة</h3>
  <div id="npSalesList"></div>
</div>

<script>
/* ========== DATA ========== */
let batches   = JSON.parse(localStorage.getItem("batches")   || "[]");
let sales     = JSON.parse(localStorage.getItem("sales")     || "[]");
let expenses  = JSON.parse(localStorage.getItem("expenses")  || "[]");
let cmdNumber = Number(localStorage.getItem("cmdNumber"))    || 1;
let baseAmt   = Number(localStorage.getItem("baseAmt"))      || 14900;
let currentCmd = [];

/* ========== INIT ========== */
window.onload = function(){
  let today = new Date().toISOString().split('T')[0];
  document.getElementById('filterFrom').value    = today;
  document.getElementById('filterTo').value      = today;
  document.getElementById('npFilterFrom').value  = today;
  document.getElementById('npFilterTo').value    = today;
  document.getElementById('expDate').value       = today;
  document.getElementById('baseAmountInput').value = baseAmt;
  render();
};

/* ========== SAVE ========== */
function save(){
  localStorage.setItem("batches",   JSON.stringify(batches));
  localStorage.setItem("sales",     JSON.stringify(sales));
  localStorage.setItem("expenses",  JSON.stringify(expenses));
  localStorage.setItem("cmdNumber", cmdNumber);
  localStorage.setItem("baseAmt",   baseAmt);
}

/* ========== HELPERS ========== */
function esc(s){ return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;'); }
function fmt(n){ return Number(n).toLocaleString('fr-DZ',{minimumFractionDigits:2,maximumFractionDigits:2}); }

function toast(msg, type='info'){
  let c = document.getElementById('toast-container');
  let t = document.createElement('div');
  t.className = 'toast ' + type;
  t.textContent = msg;
  c.appendChild(t);
  setTimeout(() => t.classList.add('show'), 20);
  setTimeout(() => { t.classList.remove('show'); setTimeout(() => t.remove(), 400); }, 3000);
}

function playBeep(){
  try{
    let a=new(window.AudioContext||window.webkitAudioContext)();
    let o=a.createOscillator(),g=a.createGain();
    o.type='sine';o.frequency.setValueAtTime(1100,a.currentTime);
    g.gain.setValueAtTime(0.12,a.currentTime);
    o.connect(g);g.connect(a.destination);
    o.start();o.stop(a.currentTime+0.1);
  }catch(e){}
}
function playCash(){
  try{
    let a=new(window.AudioContext||window.webkitAudioContext)();
    let now=a.currentTime;
    let o=a.createOscillator(),g=a.createGain();
    o.type='sine';o.frequency.setValueAtTime(1400,now);
    g.gain.setValueAtTime(0.2,now);g.gain.exponentialRampToValueAtTime(0.001,now+0.5);
    o.connect(g);g.connect(a.destination);o.start(now);o.stop(now+0.5);
  }catch(e){}
}
function playErr(){
  try{
    let a=new(window.AudioContext||window.webkitAudioContext)();
    let now=a.currentTime;
    let o=a.createOscillator(),g=a.createGain();
    o.type='sawtooth';o.frequency.setValueAtTime(150,now);
    o.frequency.linearRampToValueAtTime(80,now+0.3);
    g.gain.setValueAtTime(0.25,now);g.gain.exponentialRampToValueAtTime(0.01,now+0.3);
    o.connect(g);g.connect(a.destination);o.start(now);o.stop(now+0.3);
  }catch(e){}
}

/* ========== NAV ========== */
function openPage(id){
  document.getElementById('dashboard').style.display = 'none';
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  if(id==='sales'){ document.getElementById('saleSearch').value=''; renderSalesOptions(); setTimeout(()=>document.getElementById('saleSearch').focus(),100); }
  if(id==='low')   renderLow();
  if(id==='stock') renderStock();
  if(id==='profits') calcProfits();
  if(id==='netprofit') calcNetProfit();
  window.scrollTo(0,0);
}
function back(){
  document.getElementById('dashboard').style.display='grid';
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
}

/* ========== PRODUCTS ========== */
function checkRefUniq(){
  let f=document.getElementById('pRef');
  let v=f.value.trim();
  if(!v){ f.classList.remove('input-error'); return; }
  batches.some(b=>b.ref===v) ? f.classList.add('input-error') : f.classList.remove('input-error');
}
function checkPriceValid(){
  let bf=document.getElementById('pBuy'), sf=document.getElementById('pSell');
  let bv=Number(bf.value)||0, sv=Number(sf.value)||0;
  (sf.value!==''&&sv<bv) ? sf.classList.add('input-error') : sf.classList.remove('input-error');
}
function addProduct(){
  let ref=document.getElementById('pRef').value.trim();
  let name=document.getElementById('pName').value.trim();
  let buy=Number(document.getElementById('pBuy').value)||0;
  let sell=Number(document.getElementById('pSell').value)||0;
  let qty=Number(document.getElementById('pQty').value)||0;
  if(!ref||!name||qty<0){ playErr(); toast("يرجى ملء جميع الحقول بشكل صحيح","error"); return; }
  if(batches.some(b=>b.ref===ref)){ playErr(); toast("الباركود مكرر! يرجى استخدام باركود فريد","error"); return; }
  if(sell<buy){ if(!confirm("سعر البيع أقل من الشراء (خسارة)، هل تريد الاستمرار؟")) return; }
  batches.push({id:Date.now(),ref,name,buy,sell,qty});
  save(); render(); playBeep();
  document.getElementById('pRef').value='';
  document.getElementById('pName').value='';
  document.getElementById('pBuy').value='';
  document.getElementById('pSell').value='';
  document.getElementById('pQty').value='';
  toast("تم إضافة المنتج بنجاح","success");
}
function deleteProduct(id){
  if(!confirm("حذف هذا المنتج نهائياً؟")) return;
  batches=batches.filter(b=>b.id!==id); save(); render();
  toast("تم حذف المنتج","info");
}
function editProduct(id){
  let b=batches.find(x=>x.id===id); if(!b) return;
  let name=prompt("اسم المنتج:",b.name); if(name===null) return;
  let qty=prompt("الكمية:",b.qty);   if(qty===null)  return;
  let buy=prompt("سعر الشراء:",b.buy); if(buy===null)  return;
  let sell=prompt("سعر البيع:",b.sell); if(sell===null) return;
  b.name=name.trim()||b.name;
  b.qty=parseFloat(qty)>=0?parseFloat(qty):b.qty;
  b.buy=parseFloat(buy)>=0?parseFloat(buy):b.buy;
  b.sell=parseFloat(sell)>=0?parseFloat(sell):b.sell;
  save(); render(); playBeep();
  toast("تم تعديل المنتج","success");
}
function renderProducts(){
  let tbody=document.getElementById('productTable');
  tbody.innerHTML='';
  let sv=(document.getElementById('productSearch').value||'').toLowerCase().trim();
  let list=sv?batches.filter(b=>b.name.toLowerCase().includes(sv)||b.ref.toLowerCase().includes(sv)):batches;
  list.forEach(b=>{
    let tr=document.createElement('tr');
    tr.innerHTML=`
      <td><code>${esc(b.ref)}</code></td>
      <td>${esc(b.name)}</td>
      <td style="color:${b.qty<=3?'#ef4444':'#10b981'};font-weight:900;">${b.qty}</td>
      <td>${fmt(b.buy)}</td>
      <td>${fmt(b.sell)}</td>
      <td><button class="btn-edit" onclick="editProduct(${b.id})"><i class="fa-solid fa-pen"></i> تعديل</button></td>
      <td><button class="btn-danger" onclick="deleteProduct(${b.id})"><i class="fa-solid fa-trash"></i> حذف</button></td>
    `;
    tbody.appendChild(tr);
  });
}

/* ========== SALES ========== */
function updateCmdNumManual(){
  let v=document.getElementById('cmdNumberInput').value;
  if(v&&Number(v)>=1){ cmdNumber=Math.floor(Number(v)); localStorage.setItem("cmdNumber",cmdNumber); }
}
function resetCmdNum(){
  if(confirm("تصفير عداد الطلبيات والبدء من 1؟")){ cmdNumber=1; document.getElementById('cmdNumberInput').value=1; save(); }
}
function updateSalePrice(){
  let sel=document.getElementById('saleStock');
  if(!sel.value) return;
  let b=batches.find(x=>x.id===Number(sel.value));
  if(b) document.getElementById('salePriceInput').value=b.sell;
}
function renderSalesOptions(){
  let sv = (document.getElementById('saleSearch').value || '').toLowerCase().trim();
  let sel = document.getElementById('saleStock');

  sel.innerHTML = '';

  let list = sv
    ? batches.filter(b => b.name.toLowerCase().includes(sv) || b.ref.toLowerCase().includes(sv))
    : batches;

  /* إذا ماكانش نتائج */
  if(!list.length){
    let o = document.createElement('option');
    o.text = 'لا توجد نتائج...';
    o.value = '';
    sel.appendChild(o);

    document.getElementById('salePriceInput').value = '';
    return;
  }

  /* عرض المنتجات */
  list.forEach(b => {
    let o = document.createElement('option');
    o.value = b.id;

  o.text = `${fmt(b.sell)} DA | ${b.name} | الكمية: ${b.qty} | REF: ${b.ref}`;

    sel.appendChild(o);
  });

  updateSalePrice();

  /* إذا بحث ورجع منتج واحد */
  if(sv && list.length === 1 && list[0].ref.toLowerCase() === sv){
    addToCommand();
    document.getElementById('saleSearch').value = '';
    renderSalesOptions();
  }
}
function addToCommand(){

  let sel=document.getElementById('saleStock');

  if(!sel.value) return;

  let b=batches.find(x=>x.id===Number(sel.value));

  if(!b) return;

  let qty=parseFloat(document.getElementById('saleQty').value)||0;

  let price=parseFloat(document.getElementById('salePriceInput').value)||0;

  /* الكمية الموجودة في السلة */
  let alreadyInCart = currentCmd
    .filter(x=>x.ref===b.ref)
    .reduce((s,x)=>s+x.qty,0);

  /* الكمية المتوفرة */
  let availableQty = b.qty - alreadyInCart;

  /* تحقق */
  if(qty<=0){

    playErr();

    toast(
      "يرجى تحديد كمية أكبر من صفر",
      "error"
    );

    return;
  }

  /* منع البيع فوق المخزون */
  if(qty > availableQty){

    playErr();

    toast(
      "المخزون غير كاف! المتوفر فقط: " + availableQty,
      "error"
    );

    return;
  }

  /* بحث إذا المنتج موجود في السلة */
  let ex=currentCmd.find(
    x=>x.ref===b.ref && x.sellPrice===price
  );

  if(ex){

    /* تحقق عند الدمج */
    if(ex.qty + qty > b.qty){

      playErr();

      toast(
        "لا يمكن تجاوز كمية المخزون",
        "error"
      );

      return;
    }

    ex.qty += qty;

  }else{

    currentCmd.push({
      ref:b.ref,
      name:b.name,
      qty,
      sellPrice:price,
      buyPrice:b.buy
    });

  }

  renderCurrentCmd();

  playBeep();

  document.getElementById('saleQty').value='1';
}
function removeFromCmd(i){ currentCmd.splice(i,1); renderCurrentCmd(); }
function renderCurrentCmd(){
  let c=document.getElementById('currentCommand');
  c.innerHTML=''; let total=0;
  currentCmd.forEach((item,i)=>{
    let sub=item.qty*item.sellPrice; total+=sub;
    let d=document.createElement('div');
    d.className='order-item-line';
    d.innerHTML=`
      <div style="display:flex;align-items:center;gap:8px;">
        <button class="btn-danger" onclick="removeFromCmd(${i})" style="padding:3px 8px;font-size:11px;"><i class="fa-solid fa-trash"></i></button>
        <strong>${esc(item.name)}</strong>
        <span class="badge-qty">${item.qty} قطعة</span>
      </div>
      <span>${fmt(item.sellPrice)} x ${item.qty} = <strong>${fmt(sub)} DA</strong></span>
    `;
    c.appendChild(d);
  });
  document.getElementById('commandTotal').innerText=fmt(total)+' DA';
}
function confirmCommand(){

  if(!currentCmd.length){

    playErr();

    toast("السلة فارغة!","error");

    return;
  }

  /* تحقق نهائي من المخزون */
  for(let item of currentCmd){

    let b=batches.find(x=>x.ref===item.ref);

    if(!b){

      playErr();

      toast(
        "المنتج غير موجود بالمخزن",
        "error"
      );

      return;
    }

    if(item.qty > b.qty){

      playErr();

      toast(
        "المخزون غير كاف للمنتج: " + b.name,
        "error"
      );

      return;
    }
  }

  let today=new Date().toISOString().split('T')[0];

  /* خصم الكميات */
  currentCmd.forEach(item=>{

    let b=batches.find(x=>x.ref===item.ref);

    b.qty -= item.qty;

    sales.push({
  id:Date.now()+Math.random(),
  command:cmdNumber,
  ref:item.ref,
  name:item.name,
  qty:item.qty,
  buyPrice:item.buyPrice,
  sellPrice:item.sellPrice,
  date:today,

  /* حفظ السعر المرجعي وقت البيع */
  baseAmount: baseAmt
});

  });

  cmdNumber++;

  document.getElementById('cmdNumberInput').value=cmdNumber;

  currentCmd=[];

  save();

  render();

  playCash();

  toast(
    "تم تأكيد وحفظ الطلبية بنجاح",
    "success"
  );
}
function loadOrderToEdit(){
  let num=Number(document.getElementById('searchOrderNumber').value);
  if(!num||num<1){ toast("يرجى إدخال رقم طلبية صحيح","error"); return; }
  let items=sales.filter(x=>x.command===num);
  if(!items.length){ toast("لا توجد طلبية بهذا الرقم: #"+num,"error"); return; }
  if(currentCmd.length>0&&!confirm("السلة الحالية تحتوي منتجات، هل تفرغها وتجلب الطلبية القديمة؟")) return;
  /* إعادة الكميات للمخزن */
  items.forEach(item=>{
    let b=batches.find(x=>x.ref===item.ref);
    if(b) b.qty+=item.qty;
  });
  currentCmd=items.map(i=>({ref:i.ref,name:i.name,qty:i.qty,sellPrice:i.sellPrice,buyPrice:i.buyPrice}));
  cmdNumber=num; document.getElementById('cmdNumberInput').value=cmdNumber;
  sales=sales.filter(x=>x.command!==num);
  save(); render();
  toast("تم جلب الطلبية #"+num+" للتعديل وأُعيدت الكميات للمخزن","info");
}
function deleteEntireOrder(num){
  if(!confirm("حذف الطلبية #"+num+" كاملاً وإعادة الكميات للمخزن؟")) return;
  let items=sales.filter(x=>x.command===num);
  items.forEach(item=>{
    let b=batches.find(x=>x.ref===item.ref);
    if(b) b.qty+=item.qty;
  });
  sales=sales.filter(x=>x.command!==num);
  save(); render(); playBeep();
  toast("تم حذف الطلبية وإعادة الكميات للمخزن","info");
}
function renderSalesLog(){
  let c=document.getElementById('salesLog');
  c.innerHTML='';
  let groups={};
  sales.forEach(s=>{ if(!groups[s.command]) groups[s.command]=[]; groups[s.command].push(s); });
  let keys=Object.keys(groups).sort((a,b)=>b-a);
  if(!keys.length){ c.innerHTML="<p style='color:var(--muted);text-align:center;padding:20px;'>لا توجد طلبيات سابقة بعد...</p>"; return; }
  keys.forEach(k=>{
    let items=groups[k];
    let date=items[0].date;
    let total=items.reduce((s,i)=>s+i.qty*i.sellPrice,0);
    let card=document.createElement('div');
    card.className='order-card';
    let rows=items.map(i=>`<div style="display:flex;justify-content:space-between;font-size:12px;color:var(--muted);margin-top:4px;"><span>- ${esc(i.name)} (${i.qty})</span><span>${fmt(i.qty*i.sellPrice)} DA</span></div>`).join('');
    card.innerHTML=`
      <div class="order-card-hd">
        <span style="font-weight:800;color:var(--primary);">طلب #${k}</span>
        <span style="font-size:12px;color:var(--muted);"><i class="fa-solid fa-calendar"></i> ${date}</span>
      </div>
      ${rows}
      <div style="display:flex;justify-content:space-between;align-items:center;margin-top:10px;padding-top:8px;border-top:1px solid rgba(255,255,255,.05);">
        <span style="font-size:14px;font-weight:700;color:var(--success);">المجموع: ${fmt(total)} DA</span>
        <button onclick="deleteEntireOrder(${k})" class="btn-danger" style="padding:5px 10px;font-size:11px;"><i class="fa-solid fa-trash-can"></i> الغاء</button>
      </div>
    `;
    c.appendChild(card);
  });
}

/* ========== STOCK ========== */
function renderStock(){
  let tbody=document.getElementById('stockTable');
  let tfoot=document.getElementById('stockFoot');
  tbody.innerHTML=''; tfoot.innerHTML='';
  let pieces=0,capital=0,profit=0;
  batches.forEach(b=>{
    let cap=b.qty*b.buy, prof=(b.sell-b.buy)*b.qty;
    pieces+=b.qty; capital+=cap; profit+=prof;
    let tr=document.createElement('tr');
    tr.innerHTML=`
      <td><strong>${esc(b.name)}</strong></td>
      <td>${b.qty}</td>
      <td>${fmt(cap)} DA</td>
      <td style="color:var(--success);">${fmt(prof)} DA</td>
      <td><button class="btn-edit" style="padding:5px 10px;font-size:12px;" onclick="openPage('products');document.getElementById('productSearch').value='${esc(b.ref)}';renderProducts();"><i class="fa-solid fa-eye"></i></button></td>
    `;
    tbody.appendChild(tr);
  });
  document.getElementById('topStockPieces').innerText=pieces+' قطعة';
  document.getElementById('topStockCapital').innerText=fmt(capital)+' DA';
  document.getElementById('topStockProfit').innerText=fmt(profit)+' DA';
  tfoot.innerHTML=`<tr><td>الاجمالي الكلي</td><td>${pieces}</td><td>${fmt(capital)} DA</td><td style="color:var(--success);">${fmt(profit)} DA</td><td>---</td></tr>`;
}

/* ========== LOW STOCK ========== */
function renderLow(){
  let tbody=document.getElementById('lowTable');
  tbody.innerHTML='';
  let list=batches.filter(b=>b.qty<=5).map(b=>{
    let risk=Math.max(1,Math.min(15,Math.ceil((5-b.qty)*3)));
    return {...b,risk};
  }).sort((a,b)=>b.risk-a.risk);
  if(!list.length){
    tbody.innerHTML=`<tr><td colspan="6" style="text-align:center;color:var(--success);padding:28px;font-weight:700;"><i class="fa-solid fa-check-circle"></i> المخزن ممتاز! لا توجد سلع ناقصة.</td></tr>`;
    return;
  }
  list.forEach(b=>{
    let bg=b.risk>=11?'var(--danger-g)':b.risk>=6?'var(--warning-g)':'var(--success-g)';
    let status=b.risk>=11?'خطر شديد / تموين فوري':b.risk>=6?'نقص حرج / انتبه':'آمن حالياً';
    let tr=document.createElement('tr');
    tr.innerHTML=`
      <td><code>${esc(b.ref)}</code></td>
      <td><strong>${esc(b.name)}</strong></td>
      <td style="color:var(--danger);font-weight:900;">${b.qty} قطعة</td>
      <td>${fmt(b.buy)} DA</td>
      <td><span class="risk-badge" style="background:${bg};">المستوى ${b.risk}/15</span></td>
      <td style="font-weight:700;">${status}</td>
    `;
    tbody.appendChild(tr);
  });
}

/* ========== EXPENSES ========== */
function addExpense(){
  let title=document.getElementById('expTitle').value.trim();
  let amount=Number(document.getElementById('expAmount').value)||0;
  let date=document.getElementById('expDate').value;
  if(!title||amount<=0||!date){ playErr(); toast("يرجى ملء جميع حقول المصروف بشكل صحيح","error"); return; }
  expenses.push({id:Date.now(),title,amount,date});
  save(); render(); playBeep();
  document.getElementById('expTitle').value='';
  document.getElementById('expAmount').value='';
  toast("تم قيد المصروف بنجاح","success");
}
function deleteExpense(id){
  if(!confirm("حذف هذا المصروف؟")) return;
  expenses=expenses.filter(x=>x.id!==id); save(); render();
  toast("تم حذف المصروف","info");
}
function renderExpenses(){
  let c=document.getElementById('expensesLog');
  if(!expenses.length){ c.innerHTML="<p style='color:var(--muted);text-align:center;padding:20px;'>سجل المصاريف فارغ.</p>"; return; }
  let sorted=[...expenses].sort((a,b)=>new Date(b.date)-new Date(a.date));
  let html=`<div class="table-wrap"><table><thead><tr><th>البيان</th><th>القيمة</th><th>التاريخ</th><th>حذف</th></tr></thead><tbody>`;
  sorted.forEach(e=>{
    html+=`<tr><td><strong>${esc(e.title)}</strong></td><td style="color:var(--danger);font-weight:700;">${fmt(e.amount)} DA</td><td>${e.date}</td><td><button class="btn-danger" onclick="deleteExpense(${e.id})" style="padding:5px 10px;font-size:12px;"><i class="fa-solid fa-trash"></i></button></td></tr>`;
  });
  html+=`</tbody></table></div>`;
  c.innerHTML=html;
}

/* ========== NET PROFIT (CLEAN MERGED VERSION) ========== */
function calcNetProfit(){

  baseAmt =
    Number(document.getElementById('baseAmountInput').value) || 14900;

  save();

  let from = document.getElementById('npFilterFrom').value;
  let to   = document.getElementById('npFilterTo').value;

  let fSales = (from && to)
    ? sales.filter(s => s.date >= from && s.date <= to)
    : sales;

  let fExp = (from && to)
    ? expenses.filter(e => e.date >= from && e.date <= to)
    : expenses;

  /* ===== تجميع الطلبيات ===== */
  let groups = {};

  fSales.forEach(s => {
    if(!groups[s.command]) groups[s.command] = [];
    groups[s.command].push(s);
  });

  let totalSales = 0;
  let totalProfit = 0;

  Object.values(groups).forEach(order => {

    let orderTotal = order.reduce((sum, item) => {
      return sum + (item.qty * item.sellPrice);
    }, 0);

    totalSales += orderTotal;

    // baseAmount لكل طلبية (ولا fallback)
    let orderBase = Number(order[0].baseAmount);
    if(!orderBase || isNaN(orderBase)){
      orderBase = baseAmt || 14900;
    }

    // الربح = المرجعي - المبيعات
    totalProfit += (orderBase - orderTotal);
  });

  let totalExp = fExp.reduce((s, x) => s + x.amount, 0);

  let result = totalProfit - totalExp;

  /* ===== HERO ===== */
  let hero = document.getElementById('netHeroBig');
  hero.innerText = fmt(result) + ' DA';

  hero.className = 'big-amount ' +
    (result > 0 ? 'positive' :
     result < 0 ? 'negative' : 'zero');

  document.getElementById('netHeroFormula').innerText =
    'مجموع الفائدة - المصاريف = ' + fmt(result) + ' DA';

  /* ===== CARDS ===== */
  document.getElementById('npBaseDisp').innerText =
    fmt(baseAmt) + ' DA';

  document.getElementById('npSalesDisp').innerText =
    fmt(totalSales) + ' DA';

  document.getElementById('npExpDisp').innerText =
    fmt(totalExp) + ' DA';

  /* ===== BREAKDOWN ===== */
  document.getElementById('npFbBase').innerText =
    'مرجعي لكل طلبية (قابل للتغيير)';

  document.getElementById('npFbSales').innerText =
    fmt(totalSales) + ' DA';

  document.getElementById('npFbExp').innerText =
    fmt(totalExp) + ' DA';

  let res = document.getElementById('npFbResult');

  res.innerText = fmt(result) + ' DA';
  res.style.color =
    result > 0 ? '#34d399' :
    result < 0 ? '#f87171' :
    'var(--warning)';

  renderNpSalesList(fSales);
}
function renderNpSalesList(fSales){
  let c=document.getElementById('npSalesList');
  if(!fSales.length){ c.innerHTML="<p style='color:var(--muted);text-align:center;padding:20px;'>لا توجد طلبيات في هذه الفترة.</p>"; return; }
  let groups={};
  fSales.forEach(s=>{ if(!groups[s.command]) groups[s.command]=[]; groups[s.command].push(s); });
  let keys=Object.keys(groups).sort((a,b)=>b-a);
  let html='';
  keys.forEach(k=>{
    let items=groups[k];
    let date=items[0].date;
    let total=items.reduce((s,i)=>s+i.qty*i.sellPrice,0);
    let rows=items.map(i=>`<div style="display:flex;justify-content:space-between;font-size:13px;color:var(--muted);margin-top:4px;"><span>- ${esc(i.name)} (${i.qty} قطعة x ${fmt(i.sellPrice)} DA)</span><span>${fmt(i.qty*i.sellPrice)} DA</span></div>`).join('');
    html+=`
      <div class="order-card" style="border:1px solid rgba(245,158,11,.2);background:rgba(245,158,11,.03);">
        <div class="order-card-hd">
          <span style="font-weight:800;color:var(--warning);">طلب #${k}</span>
          <span style="font-size:12px;color:var(--muted);">${date}</span>
        </div>
        ${rows}
        <div style="display:flex;justify-content:flex-end;margin-top:10px;padding-top:8px;border-top:1px solid rgba(255,255,255,.05);">
          <span style="font-size:15px;font-weight:800;color:var(--warning);">المستحق: ${fmt(total)} DA</span>
        </div>
      </div>
    `;
  });
  c.innerHTML=html;
}

/* ========== EXPORT / IMPORT ========== */
function exportData(){
  let data=JSON.stringify({batches,sales,expenses,cmdNumber,baseAmt},null,2);
  let a=document.createElement('a');
  a.href='data:text/json;charset=utf-8,'+encodeURIComponent(data);
  a.download='POS_Backup_'+new Date().toISOString().split('T')[0]+'.json';
  document.body.appendChild(a); a.click(); a.remove();
  toast("تم تصدير النسخة الاحتياطية بنجاح","success");
}
function triggerImport(){ document.getElementById('importFileInput').click(); }
function importData(event){
  let file=event.target.files[0]; if(!file) return;
  let reader=new FileReader();
  reader.onload=function(e){
    try{
      let p=JSON.parse(e.target.result);
      if(!p.batches&&!p.sales&&!p.expenses){ toast("ملف غير متوافق مع النظام","error"); return; }
      if(!confirm("استيراد هذه النسخة؟ سيتم استبدال البيانات الحالية.")) return;
      batches=p.batches||[]; sales=p.sales||[]; expenses=p.expenses||[];
      cmdNumber=p.cmdNumber||1; baseAmt=p.baseAmt||14900;
      document.getElementById('baseAmountInput').value=baseAmt;
      save(); render();
      toast("تم استيراد البيانات بنجاح","success");
    }catch(err){ toast("خطأ في قراءة الملف","error"); }
  };
  reader.readAsText(file);
  event.target.value='';
}

/* ========== MAIN RENDER ========== */
function render(){
  document.getElementById('cmdNumberInput').value=cmdNumber;
  renderProducts();
  renderSalesOptions();
  renderCurrentCmd();
  renderSalesLog();
  renderStock();
  renderLow();
  renderExpenses();
  calcProfits();
  calcNetProfit();
}
</script>
</body>
</html>

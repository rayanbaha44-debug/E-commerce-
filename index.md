<!DOCTYPE html>
<html lang="ar" dir="rtl">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>POS SYSTEM EXECUTIVE - نظام المبيعات الاحترافي المطور</title>

    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght=300;400;500;600;700;800;900&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        /* ================= ULTRA PREMIUM MODERN LIGHT UI ================= */
        :root {
            --primary: #2563eb;
            --primary-gradient: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
            --success: #10b981;
            --success-gradient: linear-gradient(135deg, #10b981 0%, #059669 100%);
            --danger: #ef4444;
            --danger-gradient: linear-gradient(135deg, #ef4444 0%, #b91c1c 100%);
            --warning: #f59e0b;
            --warning-gradient: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);
            --purple-gradient: linear-gradient(135deg, #a855f7 0%, #7e22ce 100%);
            
            --bg-app: #f8fafc; 
            --bg-gradient: linear-gradient(135deg, #f8fafc 0%, #e2e8f0 100%);
            --surface: #ffffff; 
            --surface-card: rgba(255, 255, 255, 0.9);
            
            --text-main: #0f172a; 
            --text-muted: #64748b; 
            --border: rgba(15, 23, 42, 0.08);
            
            --radius-xl: 20px;
            --radius-lg: 14px;
            --radius-md: 10px;
            
            --shadow-blur: 0 10px 25px -5px rgba(15, 23, 42, 0.05);
            --shadow-hover: 0 20px 35px -10px rgba(37, 99, 235, 0.15);
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
            border: 1px solid rgba(15, 23, 42, 0.05);
            font-weight: 700;
            font-size: 17px;
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
            background: #ffffff;
        }

        .card:hover i { transform: scale(1.1) rotate(2deg); }

        .page {
            display: none;
            width: 100%;
            max-width: 1200px;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            padding: 40px;
            border-radius: var(--radius-xl);
            box-shadow: 0 25px 50px -12px rgba(15, 23, 42, 0.08);
            border: 1px solid rgba(15, 23, 42, 0.05);
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
            margin-bottom: 30px;
            padding-bottom: 25px;
            border-bottom: 1px solid var(--border);
        }

        .header h2 {
            font-size: 24px;
            font-weight: 800;
            color: var(--text-main);
            display: flex;
            align-items: center;
            gap: 15px;
        }

        button {
            padding: 13px 22px;
            border: none;
            border-radius: var(--radius-md);
            cursor: pointer;
            background: var(--primary-gradient);
            color: white;
            font-weight: 700;
            font-size: 14px;
            transition: all 0.2s ease;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            box-shadow: 0 4px 12px rgba(37, 99, 235, 0.15);
        }

        button:hover { opacity: 0.95; transform: translateY(-1px); box-shadow: 0 6px 16px rgba(37, 99, 235, 0.25); }
        button:active { transform: translateY(0); }

        .back { background: #64748b; box-shadow: 0 4px 12px rgba(100, 116, 139, 0.15); }
        .back:hover { background: #475569; box-shadow: 0 6px 16px rgba(71, 85, 105, 0.25); }

        .del { background: var(--danger-gradient); box-shadow: 0 4px 12px rgba(239, 68, 68, 0.15); }
        .del:hover { box-shadow: 0 6px 16px rgba(239, 68, 68, 0.25); }

        .edit { background: #f1f5f9; color: #2563eb; border: 1px solid rgba(37, 99, 235, 0.15); box-shadow: none; }
        .edit:hover { background: #2563eb; color: white; }

        label {
            display: block;
            font-size: 13.5px;
            font-weight: 700;
            color: #475569;
            margin-bottom: 8px;
        }

        input, select {
            width: 100%;
            padding: 13px 16px;
            border-radius: var(--radius-md);
            border: 1px solid #cbd5e1;
            background: #ffffff;
            color: var(--text-main);
            font-size: 14.5px;
            font-weight: 600;
            transition: all 0.2s ease;
        }

        input:focus, select:focus {
            outline: none;
            border-color: var(--primary);
            background: #ffffff;
            box-shadow: 0 0 0 4px rgba(37, 99, 235, 0.1);
        }

        input.input-error {
            border-color: var(--danger) !important;
            background: rgba(239, 68, 68, 0.05) !important;
            box-shadow: 0 0 0 4px rgba(239, 68, 68, 0.1) !important;
            animation: shake 0.3s ease;
        }

        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-4px); }
            75% { transform: translateX(4px); }
        }

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
            background: #f8fafc;
            padding: 25px;
            border-radius: var(--radius-lg);
            margin-bottom: 25px;
            border: 1px solid #e2e8f0;
        }

        .flex-inputs { display: flex; gap: 15px; align-items: center; margin-bottom: 20px; }
        .flex-inputs > div { flex: 1; }

        table {
            width: 100%;
            margin-top: 25px;
            border-collapse: separate;
            border-spacing: 0;
            border-radius: var(--radius-lg);
            overflow: hidden;
            border: 1px solid #e2e8f0;
            box-shadow: 0 4px 15px rgba(0,0,0,0.02);
            table-layout: auto;
        }

        th, td { 
            padding: 16px 14px; 
            text-align: center; 
            font-size: 14.5px; 
            vertical-align: middle;
        }

        th { 
            background-color: #f1f5f9; 
            color: #475569; 
            font-weight: 700; 
            border-bottom: 2px solid #e2e8f0; 
        }

        td { 
            background-color: #ffffff; 
            border-bottom: 1px solid #f1f5f9; 
            color: #0f172a; 
            font-weight: 600;
        }

        tr:hover td {
            background-color: #f8fafc; 
            transition: background 0.15s ease;
        }

        td code {
            background: #f1f5f9;
            padding: 6px 12px;
            border-radius: 6px;
            color: #1e40af; 
            font-family: monospace;
            font-size: 13.5px;
            border: 1px solid #e2e8f0;
            font-weight: 700;
            display: inline-block;
            max-width: 180px;
            word-break: break-all;
            white-space: normal;
            overflow-wrap: break-word;
            line-height: 1.4;
            text-align: center;
        }

        tr:last-child td { border-bottom: none; }

        .order-card {
            background: #ffffff;
            border: 1px solid #e2e8f0;
            border-radius: var(--radius-lg);
            padding: 20px;
            margin-bottom: 20px;
            box-shadow: var(--shadow-blur);
        }

        .order-card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px dashed #e2e8f0;
            padding-bottom: 12px;
            margin-bottom: 12px;
        }

        .order-item-line {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px 5px;
            font-size: 14.5px;
            border-bottom: 1px solid #f1f5f9;
            color: #0f172a;
            font-weight: 600;
        }

        .badge-qty { background: #eff6ff; color: #1e40af; padding: 4px 12px; border-radius: 6px; font-weight: 800; font-size: 13px; border: 1px solid #bfdbfe; margin-right: 5px; }

        .profit-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 20px; margin-top: 25px; }
        .profit-card { background: #ffffff; padding: 25px; border-radius: var(--radius-lg); border: 1px solid #e2e8f0; border-right: 5px solid var(--primary); box-shadow: var(--shadow-blur); }
        .profit-card.success { border-right-color: var(--success); }
        .profit-card.dark { border-right-color: #475569; }
        .profit-card.filter { border-right-color: #a855f7; background: rgba(168, 85, 247, 0.02); }
        .profit-card.expense-card { border-right-color: var(--danger); background: rgba(239, 68, 68, 0.02); }
        .profit-card p { color: var(--text-muted); font-size: 13.5px; font-weight: 700; margin-bottom: 8px;}
        .profit-card .amount { font-size: 22px; font-weight: 800; }

        /* ستايل التنبيهات في المخزن */
        .stock-empty { background-color: #fee2e2 !important; color: #991b1b !important; }
        .stock-empty td { background-color: #fee2e2 !important; color: #991b1b !important; }
        
        .stock-danger { background-color: #fef3c7 !important; color: #92400e !important; }
        .stock-danger td { background-color: #fef3c7 !important; color: #92400e !important; }
        
        .stock-warning { background-color: #fff7ed !important; color: #92400e !important; } 
        .stock-warning td { background-color: #fff7ed !important; color: #c2410c !important; }
        
        .stock-notice { background-color: #eff6ff !important; color: #1e40af !important; }
        .stock-notice td { background-color: #eff6ff !important; color: #1e40af !important; }

        .stock-empty td code, .stock-danger td code, .stock-warning td code, .stock-notice td code {
            background: rgba(255, 255, 255, 0.6) !important;
            border-color: currentColor !important;
            color: inherit !important;
        }

        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(15, 23, 42, 0.4);
            backdrop-filter: blur(6px);
            align-items: center;
            justify-content: center;
        }
        .modal.active { display: flex; }
        .modal-content {
            background: #ffffff;
            padding: 30px;
            border-radius: var(--radius-xl);
            width: 90%;
            max-width: 550px;
            border: 1px solid #e2e8f0;
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.1);
            animation: slideUp 0.3s ease;
        }

        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: #f1f5f9; }
        ::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: #94a3b8; }
    </style>
</head>

<body>

    <div id="dashboard">
        <div class="card" onclick="openPage('products')"><i class="fa-solid fa-box-open"></i> إدارة المنتجات والمخزن</div>
        <div class="card" onclick="openPage('sales')"><i class="fa-solid fa-cash-register"></i> واجهة البيع السريعة</div>
        <div class="card" onclick="openPage('stock')"><i class="fa-solid fa-warehouse"></i> جرد المخزون الكلي</div>
        <div class="card" onclick="openPage('low')"><i class="fa-solid fa-triangle-exclamation"></i> السلع الناقصة بالمحل</div>
        <div class="card" onclick="openPage('expenses')"><i class="fa-solid fa-hand-holding-dollar"></i> إدارة المصاريف الكلية</div>
        <div class="card" onclick="openPage('profits')"><i class="fa-solid fa-chart-line"></i> تقارير الأرباح الصافية</div>
        
        <div class="card" onclick="exportData()" style="background: rgba(16, 185, 129, 0.04); border: 1px dashed rgba(16, 185, 129, 0.3);"><i class="fa-solid fa-file-export" style="background:var(--success-gradient); -webkit-background-clip: text;"></i> تصدير نسخة احتياطية (Text)</div>
        <div class="card" onclick="triggerImport()" style="background: rgba(168, 85, 247, 0.04); border: 1px dashed rgba(168, 85, 247, 0.3);"><i class="fa-solid fa-file-import" style="background:var(--purple-gradient); -webkit-background-clip: text;"></i> استيراد ملف من الكمبيوتر (أي صيغة)</div>
    </div>

    <input type="file" id="importFileInput" style="display: none;" onchange="importData(event)">

    <!-- صفحة إدارة المنتجات -->
    <div id="products" class="page">
        <div class="header">
            <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع للرئيسية</button>
            <h2><i class="fa-solid fa-box-open" style="color:var(--primary);"></i> إدارة المنتجات والمخزن</h2>
        </div>
        <div class="box">
            <h3 style="margin-bottom: 20px; font-size:16px; font-weight:800;"><i class="fa-solid fa-plus-circle"></i> إضافة منتج جديد يدوياً</h3>
            <div class="flex-inputs">
                <div><label>الباركود / Ref (يجب أن يكون فريداً):</label><input id="pRef" placeholder="أدخل أو امسح الباركود" oninput="checkRefUniqueness()"></div>
                <div><label>اسم المنتج:</label><input id="pName" placeholder="اسم المنتج بالكامل"></div>
            </div>
            <div class="flex-inputs">
                <div><label>سعر الشراء (DA):</label><input id="pBuy" type="number" step="0.01" placeholder="0.00" oninput="checkPriceValidity()"></div>
                <div><label>سعر البيع الافتراضي (DA):</label><input id="pSell" type="number" step="0.01" placeholder="0.00" oninput="checkPriceValidity()"></div>
                <div><label>الكمية الابتدائية:</label><input id="pQty" type="number" step="0.01" placeholder="0"></div>
            </div>
            <button onclick="addProduct()" style="width: 100%; margin-top: 5px; background: var(--success-gradient); height: 48px;"><i class="fa-solid fa-plus"></i> إضافة المنتج للمخزن</button>
        </div>
        <div style="margin-top: 25px; margin-bottom: 10px;">
            <label>🔍 بحث سريع وسلس في المنتجات:</label>
            <input id="productSearch" placeholder="ابحث باسم المنتج أو الرقم المتسلسل..." oninput="renderProducts()">
        </div>
        <div style="overflow-x: auto;">
            <table>
                <thead><tr><th>الباركود</th><th>اسم المنتج</th><th>الكمية الحالية</th><th>الشراء (DA)</th><th>البيع الافتراضي (DA)</th><th>تعديل شامل</th><th>حذف</th></tr></thead>
                <tbody id="productTable"></tbody>
            </table>
        </div>
    </div>

    <!-- نافذة تعديل المنتج الشاملة المنبثقة -->
    <div id="editModal" class="modal">
        <div class="modal-content">
            <h3 style="margin-bottom: 20px; display: flex; align-items: center; gap: 10px; color: var(--primary); font-weight:800;"><i class="fa-solid fa-pen-to-square"></i> نافذة التعديل الشامل للمنتج</h3>
            <input type="hidden" id="editProductId">
            <div style="margin-bottom: 12px;">
                <label>الباركود / الرفرونس (Ref):</label>
                <input id="editProductRef">
            </div>
            <div style="margin-bottom: 12px;">
                <label>اسم المنتج:</label>
                <input id="editProductName">
            </div>
            <div class="flex-inputs" style="margin-bottom: 12px;">
                <div>
                    <label>سعر الشراء (DA):</label>
                    <input id="editProductBuy" type="number" step="0.01">
                </div>
                <div>
                    <label>سعر البيع (DA):</label>
                    <input id="editProductSell" type="number" step="0.01">
                </div>
            </div>
            <div style="margin-bottom: 20px;">
                <label>الكمية الحالية في المخزن:</label>
                <input id="editProductQty" type="number" step="0.01">
            </div>
            <div style="display: flex; gap: 10px; justify-content: flex-end;">
                <button class="back" onclick="closeEditModal()">إلغاء</button>
                <button onclick="saveProductEdits()" style="background: var(--success-gradient);"><i class="fa-solid fa-floppy-disk"></i> حفظ التعديلات</button>
            </div>
        </div>
    </div>

    <!-- واجهة البيع السريعة -->
    <div id="sales" class="page" style="max-width: 1300px;">
        <div class="header">
            <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع للرئيسية</button>
            <h2><i class="fa-solid fa-cash-register" style="color:var(--primary);"></i> واجهة البيع السريعة والتعديل الفوري</h2>
        </div>
        
        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-bottom: 25px;">
            <div class="box" style="background: #ffffff; color: var(--text-main); padding: 15px; margin: 0; display: flex; align-items: center; justify-content: space-around; flex-wrap: wrap;">
                <span style="font-weight: 700; font-size: 15px;"><i class="fa-solid fa-receipt"></i> رقم الطلب الحالي:</span>
                <input id="cmdNumberInput" type="number" min="1" style="width: 110px; text-align: center; font-size: 17px; font-weight: 800; color: #0f172a; background: #f1f5f9; padding: 8px;" oninput="updateCommandNumberManual()">
                <button class="del" onclick="resetCommandNumber()" style="padding: 10px 16px; font-size: 13px;"><i class="fa-solid fa-arrow-rotate-left"></i> تصفير</button>
            </div>
            <div class="box" style="background: rgba(37, 99, 235, 0.03); border: 1px solid rgba(37, 99, 235, 0.15); padding: 15px; margin: 0; display: flex; align-items: center; gap: 15px;">
                <input id="searchOrderNumber" type="number" placeholder="رقم طلبية سابقة لتعديلها..." style="background: #ffffff;">
                <button onclick="loadOrderToEdit()" style="background: var(--purple-gradient); white-space: nowrap; padding: 13px 20px;"><i class="fa-solid fa-edit"></i> جلب للتعديل</button>
            </div>
        </div>

        <div class="sales-grid">
            <div>
                <div class="box" style="background: #ffffff;">
                    <h3 style="font-size: 16px; font-weight:800; margin-bottom: 20px; color: var(--primary);"><i class="fa-solid fa-filter"></i> اختيار المنتج وتحديد السعر</h3>
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
                            <input id="salePriceInput" type="number" step="0.01" style="border: 2px solid var(--primary); font-size: 16px; font-weight: 700; color: #0f172a; background:#ffffff;">
                        </div>
                    </div>
                    <button onclick="addToCommand()" style="width: 100%; height: 50px; font-size: 15px; background: var(--primary-gradient);"><i class="fa-solid fa-cart-plus"></i> إضافة إلى السلة الحالية</button>
                </div>
                
                <h3 style="color: var(--text-main); font-weight:800; font-size: 16px; margin-bottom: 15px;"><i class="fa-solid fa-clock-rotate-left"></i> سجل الطلبيات المبيوعة السابقة</h3>
                <div id="salesLog" style="max-height: 400px; overflow-y: auto;"></div>
            </div>

            <div class="box" style="background: #ffffff; border: 1px solid rgba(16, 185, 129, 0.4); position: sticky; top: 20px; box-shadow: var(--shadow-blur);">
                <h3 style="margin-bottom: 20px; border-bottom: 1px solid var(--border); padding-bottom: 12px; font-size: 16px; font-weight:800; color: var(--success);"><i class="fa-solid fa-basket-shopping"></i> سلة التسوق الحالية</h3>
                <div id="currentCommand" style="min-height: 160px; max-height: 320px; overflow-y: auto; margin-bottom: 20px;"></div>
                
                <div style="background: rgba(16, 185, 129, 0.04); padding: 20px; border-radius: var(--radius-md); border: 1px solid rgba(16, 185, 129, 0.15); text-align: left; margin-bottom: 20px;">
                    <span style="color: #047857; font-size: 14px; font-weight: 700;">المجموع الإجمالي المستحق:</span>
                    <h3 id="commandTotal" style="color: var(--success); font-size: 26px; font-weight: 900; margin-top: 5px;">0.00 DA</h3>
                </div>
                <button onclick="confirmCommand()" style="width:100%; background: var(--success-gradient); font-size: 16px; padding: 15px; box-shadow: 0 4px 15px rgba(16, 185, 129, 0.15);"><i class="fa-solid fa-circle-check"></i> تأكيد وحفظ الطلب النهائي</button>
            </div>
        </div>
    </div>

    <!-- صفحة كشف وجرد المخزون الكلي -->
    <div id="stock" class="page">
        <div class="header">
            <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع للرئيسية</button>
            <h2><i class="fa-solid fa-warehouse" style="color:var(--primary);"></i> كشف وجرد المخزون الكلي</h2>
        </div>

        <div class="profit-grid" style="margin-top: 0; margin-bottom: 30px;">
            <div class="profit-card" style="border-right-color: var(--primary);">
                <p>📦 إجمالي السلع المتوفرة بالمخزن</p>
                <div id="topStockPieces" class="amount" style="color: #1e40af;">0 قطعة</div>
            </div>
            <div class="profit-card" style="border-right-color: var(--danger);">
                <p>💰 إجمالي رأس المال المستثمر (الشراء)</p>
                <div id="topStockCapital" class="amount" style="color: #c2410c;">0.00 DA</div>
            </div>
            <div class="profit-card success" style="border-right-color: var(--success);">
                <p>📈 صافي الأرباح المتوقعة عند البيع</p>
                <div id="topStockProfit" class="amount" style="color: var(--success);">0.00 DA</div>
            </div>
        </div>

        <div style="overflow-x: auto;">
            <table>
                <thead><tr><th>اسم المنتج</th><th>القطع المتبقية</th><th>رأس المال المستثمر</th><th>الأرباح المتوقعة</th><th>إجراء فوري</th></tr></thead>
                <tbody id="stockTable"></tbody>
            </table>
        </div>
    </div>

    <!-- صفحة السلع الناقصة -->
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

    <!-- صفحة إدارة المصاريف -->
    <div id="expenses" class="page">
        <div class="header">
            <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع للرئيسية</button>
            <h2><i class="fa-solid fa-hand-holding-dollar" style="color:var(--danger);"></i> إدارة مصاريف المحل الكلية 💸</h2>
        </div>
        <div class="box">
            <h3 style="margin-bottom: 20px; font-size:16px; font-weight:800;"><i class="fa-solid fa-file-invoice-dollar"></i> تسجيل مصروف جديد وتدوينه</h3>
            <div style="margin-bottom: 18px;">
                <label>بيان المصروف ونوعه:</label>
                <input id="expTitle" placeholder="مثال: فاتورة الكهرباء، نقل السلعة، تالف...">
            </div>
            <div class="flex-inputs">
                <div><label>قيمة المصروف (DA):</label><input id="expAmount" type="number" step="0.01" placeholder="0.00"></div>
                <div><label>تاريخ التقييد:</label><input id="expDate" type="date"></div>
            </div>
            <button onclick="addExpense()" style="width: 100%; margin-top: 5px; background: var(--danger-gradient); height: 48px;"><i class="fa-solid fa-check"></i> حفظ وقيد المصروف بالدفتر</button>
        </div>
        <h3 style="color: var(--text-main); font-weight:800; margin-top:30px; font-size: 16px;"><i class="fa-solid fa-receipt"></i> سجل المصاريف المقيدة</h3>
        <div id="expensesLog" style="max-height: 420px; overflow-y: auto; margin-top: 20px;"></div>
    </div>

    <!-- صفحة تقارير الأرباح -->
    <div id="profits" class="page">
        <div class="header">
            <button class="back" onclick="back()"><i class="fa-solid fa-arrow-right"></i> رجوع للرئيسية</button>
            <h2><i class="fa-solid fa-chart-line" style="color:var(--success);"></i> التقارير المالية والأرباح الصافية الحقيقية</h2>
        </div>
        <div class="box" style="background: #ffffff;">
            <h3 style="margin-bottom: 20px; font-size:16px; font-weight:800; color: #7e22ce;"><i class="fa-solid fa-calendar-days"></i> فرز واحتساب الأرباح بفترة زمنية مخصصة 🗓️</h3>
            <div class="flex-inputs">
                <div><label>من تاريخ 📅:</label><input type="date" id="filterFrom" onchange="calculateFilteredProfit()"></div>
                <div><label>إلى تاريخ 🏁:</label><input type="date" id="filterTo" onchange="calculateFilteredProfit()"></div>
            </div>
        </div>
        <div class="profit-grid">
            <div class="profit-card filter" style="grid-column: span 2 / span 2;">
                <p>🎯 صافي فائدة الفترة المحددة بالفرز أعلاه (فائدة المبيعات المعدلة - المصاريف)</p>
                <div id="filteredProfit" class="amount" style="color: #7e22ce;">0.00 DA 💰</div>
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
                <div id="totalExpensesYear" class="amount" style="color: #b91c1c;">0.00 DA 💸</div>
            </div>
            <div class="profit-card dark" style="grid-column: span 2 / span 2;">
                <p>👑 صافي فائدة السنة الإجمالية الحقيقية</p>
                <div id="yearlyProfit" class="amount" style="color: var(--text-main);">0.00 DA</div>
            </div>
        </div>
    </div>

    <!-- ================= SYSTEM LOGIC ================= -->
    <script>
        let batches = JSON.parse(localStorage.getItem("batches") || "[]");
        let sales = JSON.parse(localStorage.getItem("sales") || "[]");
        let expenses = JSON.parse(localStorage.getItem("expenses") || "[]");
        
        let commandNumber = parseInt(localStorage.getItem("commandNumber"));
        if (!commandNumber || isNaN(commandNumber) || commandNumber < 1) {
            commandNumber = 1;
        }

        let currentCommandData = [];
        let editingOrderNumber = null;

        window.onload = function() {
            let todayStr = new Date().toISOString().split('T')[0];
            document.getElementById('filterFrom').value = todayStr;
            document.getElementById('filterTo').value = todayStr;
            document.getElementById('expDate').value = todayStr;
            document.getElementById('cmdNumberInput').value = commandNumber;
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
                document.getElementById('saleSearch').value = ''; 
                renderSalesOptions();
                document.getElementById('cmdNumberInput').value = commandNumber;
            }
        }

        function back(){
            document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
            document.getElementById("dashboard").style.display="grid";
            render();
        }

        function render() {
            renderProducts();
            renderSalesOptions();
            renderCurrentCommand();
            renderSalesLog();
            renderStockReport();
            renderLowStockReport();
            renderExpensesLog();
            calculateProfits();
        }

        /* ================= PRODUCTS MANAGEMENT ================= */
        function checkRefUniqueness() {
            let refInput = document.getElementById("pRef");
            let isDuplicate = batches.some(b => b.ref === refInput.value.trim());
            if (isDuplicate && refInput.value.trim() !== "") {
                refInput.classList.add("input-error");
            } else {
                refInput.classList.remove("input-error");
            }
        }

        function checkPriceValidity() {
            let buy = parseFloat(document.getElementById("pBuy").value) || 0;
            let sell = parseFloat(document.getElementById("pSell").value) || 0;
            let sellInput = document.getElementById("pSell");
            if (sell < buy && sell > 0) {
                sellInput.classList.add("input-error");
            } else {
                sellInput.classList.remove("input-error");
            }
        }

        function addProduct() {
            let ref = document.getElementById("pRef").value.trim();
            let name = document.getElementById("pName").value.trim();
            let buy = parseFloat(document.getElementById("pBuy").value) || 0;
            let sell = parseFloat(document.getElementById("pSell").value) || 0;
            let qty = parseFloat(document.getElementById("pQty").value) || 0;

            if (!ref || !name || buy <= 0 || sell <= 0) {
                alert("الرجاء ملء جميع الحقول ببيانات صحيحة.");
                return;
            }

            if (batches.some(b => b.ref === ref)) {
                alert("الباركود هذا مسجل مسبقاً لمنتج آخر! يجب أن يكون فريداً.");
                return;
            }

            batches.push({ id: Date.now().toString(), ref, name, buy, sell, qty });
            save();
            render();

            document.getElementById("pRef").value = "";
            document.getElementById("pName").value = "";
            document.getElementById("pBuy").value = "";
            document.getElementById("pSell").value = "";
            document.getElementById("pQty").value = "";
        }

        function renderProducts() {
            let search = document.getElementById("productSearch").value.toLowerCase();
            let tbody = document.getElementById("productTable");
            tbody.innerHTML = "";

            let filtered = batches.filter(b => b.name.toLowerCase().includes(search) || b.ref.toLowerCase().includes(search));

            filtered.forEach(b => {
                let tr = document.createElement("tr");
                tr.innerHTML = `
                    <td><code>${b.ref}</code></td>
                    <td>${b.name}</td>
                    <td>${b.qty}</td>
                    <td>${b.buy.toFixed(2)}</td>
                    <td>${b.sell.toFixed(2)}</td>
                    <td><button class="edit" onclick="openEditModal('${b.id}')"><i class="fa-solid fa-pen"></i> تعديل</button></td>
                    <td><button class="del" onclick="deleteProduct('${b.id}')"><i class="fa-solid fa-trash"></i></button></td>
                `;
                tbody.appendChild(tr);
            });
        }

        function deleteProduct(id) {
            if(confirm("هل أنت متأكد من حذف هذا المنتج نهائياً من المخزن؟")) {
                batches = batches.filter(b => b.id !== id);
                save();
                render();
            }
        }

        function openEditModal(id) {
            let b = batches.find(x => x.id === id);
            if(!b) return;
            document.getElementById("editProductId").value = b.id;
            document.getElementById("editProductRef").value = b.ref;
            document.getElementById("editProductName").value = b.name;
            document.getElementById("editProductBuy").value = b.buy;
            document.getElementById("editProductSell").value = b.sell;
            document.getElementById("editProductQty").value = b.qty;
            document.getElementById("editModal").classList.add("active");
        }

        function closeEditModal() {
            document.getElementById("editModal").classList.remove("active");
        }

        function saveProductEdits() {
            let id = document.getElementById("editProductId").value;
            let ref = document.getElementById("editProductRef").value.trim();
            let name = document.getElementById("editProductName").value.trim();
            let buy = parseFloat(document.getElementById("editProductBuy").value) || 0;
            let sell = parseFloat(document.getElementById("editProductSell").value) || 0;
            let qty = parseFloat(document.getElementById("editProductQty").value) || 0;

            if(!ref || !name || buy <= 0 || sell <= 0) {
                alert("الرجاء التحقق من البيانات المدخلة.");
                return;
            }

            let index = batches.findIndex(x => x.id === id);
            if(index !== -1) {
                if(batches.some((x, i) => x.ref === ref && i !== index)) {
                    alert("الباركود مستعمل مع منتج آخر!");
                    return;
                }
                batches[index] = { id, ref, name, buy, sell, qty };
                save();
                closeEditModal();
                render();
            }
        }

        /* ================= QUICK SALES INTERFACE ================= */
        function updateCommandNumberManual() {
            let val = parseInt(document.getElementById("cmdNumberInput").value);
            if (isNaN(val) || val < 1) val = 1;
            commandNumber = val;
            localStorage.setItem("commandNumber", commandNumber);
        }

        function resetCommandNumber() {
            commandNumber = 1;
            document.getElementById("cmdNumberInput").value = 1;
            localStorage.setItem("commandNumber", commandNumber);
        }

        // تم إصلاح الدالة: تدمج تصفية البحث وتحديث السعر بشكل تفاعلي مرن
        function renderSalesOptions() {
            let search = document.getElementById("saleSearch").value.toLowerCase();
            let select = document.getElementById("saleStock");
            select.innerHTML = "";

            let filtered = batches.filter(b => b.name.toLowerCase().includes(search) || b.ref.toLowerCase().includes(search));
            
            filtered.forEach(b => {
                let opt = document.createElement("option");
                opt.value = b.id;
                opt.textContent = `${b.name} [الباركود: ${b.ref}] (المخزون: ${b.qty})`;
                select.appendChild(opt);
            });

            // تحديث السعر الافتراضي فوراً بناءً على المنتج الأول المتاح في الفرز
            if(filtered.length > 0) {
                let initialProduct = batches.find(x => x.id === select.value);
                if(initialProduct) {
                    document.getElementById("salePriceInput").value = initialProduct.sell;
                }
            } else {
                document.getElementById("salePriceInput").value = "";
            }
        }

        // تم إصلاح الدالة: لتعديل السعر ديناميكياً عند اختيار منتج مختلف من القائمة يدويًا
        function updateDefaultSalePriceField() {
            let select = document.getElementById("saleStock");
            if(select && select.value) {
                let selectedProduct = batches.find(x => x.id === select.value);
                if(selectedProduct) {
                    document.getElementById("salePriceInput").value = selectedProduct.sell;
                }
            } else {
                document.getElementById("salePriceInput").value = "";
            }
        }

        function addToCommand() {
            let select = document.getElementById("saleStock");
            if(!select || !select.value) {
                alert("الرجاء اختيار منتج أولاً.");
                return;
            }

            let b = batches.find(x => x.id === select.value);
            let qty = parseFloat(document.getElementById("saleQty").value) || 1;
            let sellPrice = parseFloat(document.getElementById("salePriceInput").value) || 0;

            if(qty <= 0 || sellPrice <= 0) {
                alert("الرجاء إدخال كمية وسعر بيع صحيحين.");
                return;
            }

            if(editingOrderNumber === null && qty > b.qty) {
                alert(`الكمية المطلوبة أكبر من المخزون المتوفر الحالي (${b.qty})`);
                return;
            }

            let exist = currentCommandData.find(x => x.productId === b.id);
            if(exist) {
                exist.qty += qty;
                exist.sellPrice = sellPrice; 
            } else {
                currentCommandData.push({
                    productId: b.id,
                    name: b.name,
                    buyPrice: b.buy, 
                    sellPrice: sellPrice,
                    qty: qty
                });
            }

            renderCurrentCommand();
            document.getElementById("saleQty").value = "1";
        }

        function renderCurrentCommand() {
            let container = document.getElementById("currentCommand");
            container.innerHTML = "";
            let total = 0;

            currentCommandData.forEach((item, index) => {
                let subTotal = item.sellPrice * item.qty;
                total += subTotal;

                let div = document.createElement("div");
                div.className = "order-item-line";
                div.innerHTML = `
                    <div style="display: flex; flex-direction: column; gap: 2px;">
                        <span style="color: var(--text-main); font-weight: 700;">${item.name}</span>
                        <span style="font-size: 12px; color: var(--text-muted);">${item.sellPrice.toFixed(2)} DA للقطعة</span>
                    </div>
                    <div style="display: flex; align-items: center; gap: 10px;">
                        <span class="badge-qty">x${item.qty}</span>
                        <span style="color: var(--text-main); font-weight: 800; min-width: 90px; text-align: left;">${subTotal.toFixed(2)} DA</span>
                        <button class="del" style="padding: 5px 9px; font-size:11px; border-radius:6px;" onclick="removeFromCurrentCommand(${index})"><i class="fa-solid fa-xmark"></i></button>
                    </div>
                `;
                container.appendChild(div);
            });

            document.getElementById("commandTotal").textContent = total.toFixed(2) + " DA";
        }

        function removeFromCurrentCommand(index) {
            currentCommandData.splice(index, 1);
            renderCurrentCommand();
        }

        function confirmCommand() {
            if(currentCommandData.length === 0) {
                alert("سلة التسوق فارغة حالياً. قم بإضافة منتجات أولاً.");
                return;
            }

            let total = currentCommandData.reduce((acc, curr) => acc + (curr.sellPrice * curr.qty), 0);
            let todayStr = new Date().toISOString().split('T')[0];

            if (!commandNumber || isNaN(commandNumber)) commandNumber = 1;

            if(editingOrderNumber !== null) {
                let oldOrder = sales.find(s => s.orderNumber === editingOrderNumber);
                if(oldOrder) {
                    oldOrder.items.forEach(oldItem => {
                        let p = batches.find(x => x.id === oldItem.productId);
                        if(p) p.qty += oldItem.qty;
                    });
                }
                sales = sales.filter(s => s.orderNumber !== editingOrderNumber);
                sales.push({
                    orderNumber: editingOrderNumber,
                    date: todayStr,
                    items: [...currentCommandData],
                    total: total
                });
                alert(`تم حفظ وتحديث الفاتورة المعدلة رقم ${editingOrderNumber} بنجاح.`);
                editingOrderNumber = null;
            } else {
                sales.push({
                    orderNumber: commandNumber,
                    date: todayStr,
                    items: [...currentCommandData],
                    total: total
                });
                
                currentCommandData.forEach(item => {
                    let p = batches.find(x => x.id === item.productId);
                    if(p) p.qty -= item.qty;
                });

                commandNumber++;
            }

            document.getElementById("cmdNumberInput").value = commandNumber;
            currentCommandData = [];
            save();
            render();
        }

        function renderSalesLog() {
            let container = document.getElementById("salesLog");
            container.innerHTML = "";

            let sortedSales = [...sales].sort((a,b) => b.orderNumber - a.orderNumber);

            sortedSales.forEach(s => {
                let div = document.createElement("div");
                div.className = "order-card";
                
                let itemsHtml = s.items.map(i => `
                    <div style="font-size: 13px; display:flex; justify-content:space-between; opacity: 0.9; margin-top:4px;">
                        <span>- ${i.name} (x${i.qty})</span>
                        <span>${(i.sellPrice * i.qty).toFixed(2)} DA</span>
                    </div>
                `).join('');

                div.innerHTML = `
                    <div class="order-card-header">
                        <span style="font-weight:800; color:var(--primary);">طلب رقم #${s.orderNumber}</span>
                        <span style="font-size:12px; color:var(--text-muted);">${s.date}</span>
                    </div>
                    <div>${itemsHtml}</div>
                    <div style="margin-top:12px; padding-top:8px; border-top:1px solid #e2e8f0; display:flex; justify-content:space-between; align-items:center;">
                        <span style="font-weight:800; color:var(--success);">إجمالي: ${s.total.toFixed(2)} DA</span>
                        <button class="edit" style="padding: 6px 12px; font-size: 12px;" onclick="prepareEditOldOrder(${s.orderNumber})"><i class="fa-solid fa-pen"></i> تعديل</button>
                    </div>
                `;
                container.appendChild(div);
            });
        }

        function prepareEditOldOrder(num) {
            let s = sales.find(x => x.orderNumber === num);
            if(!s) return;
            editingOrderNumber = num;
            currentCommandData = [...s.items];
            renderCurrentCommand();
            alert(`تم جلب الطلب رقم ${num} إلى السلة. عند التأكيد سيتم استبدال البيانات والخصم التفاعلي.`);
        }

        function loadOrderToEdit() {
            let num = parseInt(document.getElementById("searchOrderNumber").value);
            if(!num) return;
            let s = sales.find(x => x.orderNumber === num);
            if(!s) {
                alert("لم يتم العثور على أي فاتورة بهذا الرقم.");
                return;
            }
            prepareEditOldOrder(num);
        }

        /* ================= INVENTORY & CAPITALS REPORT ================= */
        function renderStockReport() {
            let tbody = document.getElementById("stockTable");
            tbody.innerHTML = "";

            let totalPieces = 0;
            let totalCapital = 0;
            let totalExpectedProfit = 0;

            batches.forEach(b => {
                let capital = b.buy * b.qty;
                let expectedProfit = (b.sell - b.buy) * b.qty;

                totalPieces += b.qty;
                totalCapital += capital;
                totalExpectedProfit += expectedProfit;

                let tr = document.createElement("tr");
                tr.innerHTML = `
                    <td style="text-align: right; font-weight:700;">${b.name}</td>
                    <td><span class="badge-qty" style="color:#0f172a; background:#e2e8f0; border-color:#cbd5e1;">${b.qty}</span></td>
                    <td>${capital.toFixed(2)} DA</td>
                    <td style="color:var(--success);">${expectedProfit.toFixed(2)} DA</td>
                    <td><button class="edit" onclick="openPage('products'); openEditModal('${b.id}');">توريد / تعديل</button></td>
                `;
                tbody.appendChild(tr);
            });

            document.getElementById("topStockPieces").textContent = totalPieces + " قطعة";
            document.getElementById("topStockCapital").textContent = totalCapital.toFixed(2) + " DA";
            document.getElementById("topStockProfit").textContent = totalExpectedProfit.toFixed(2) + " DA";
        }

        /* ================= LOW STOCK & WARNINGS ================= */
        function renderLowStockReport() {
            let tbody = document.getElementById("lowTable");
            tbody.innerHTML = "";

            batches.forEach(b => {
                let statusClass = "";
                let txt = "";

                if(b.qty === 0) {
                    statusClass = "stock-empty";
                    txt = "نفد بالكامل 🛑";
                } else if(b.qty <= 5) {
                    statusClass = "stock-danger";
                    txt = "حالة حرجة جداً ⚠️";
                } else if(b.qty <= 15) {
                    statusClass = "stock-warning";
                    txt = "ناقص بالمحل 📉";
                } else if(b.qty <= 30) {
                    statusClass = "stock-notice";
                    txt = "مخزون متوسط مقارب للنفاذ";
                } else {
                    return;
                }

                let tr = document.createElement("tr");
                tr.className = statusClass;
                tr.innerHTML = `
                    <td><code>${b.ref}</code></td>
                    <td>${b.name}</td>
                    <td><strong>${b.qty}</strong></td>
                    <td>${b.buy.toFixed(2)} DA</td>
                    <td><strong>${txt}</strong></td>
                `;
                tbody.appendChild(tr);
            });
        }

        /* ================= EXPENSES MANAGEMENT ================= */
        function addExpense() {
            let title = document.getElementById("expTitle").value.trim();
            let amount = parseFloat(document.getElementById("expAmount").value) || 0;
            let date = document.getElementById("expDate").value;

            if(!title || amount <= 0 || !date) {
                alert("الرجاء إدخال بيانات صحيحة للقيد المصرفي.");
                return;
            }

            expenses.push({
                id: Date.now().toString(),
                title, amount, date
            });

            save();
            render();

            document.getElementById("expTitle").value = "";
            document.getElementById("expAmount").value = "";
        }

        function renderExpensesLog() {
            let container = document.getElementById("expensesLog");
            container.innerHTML = "";

            let sorted = [...expenses].sort((a,b) => new Date(b.date) - new Date(a.date));

            sorted.forEach(e => {
                let div = document.createElement("div");
                div.className = "order-card";
                div.style.borderRight = "5px solid var(--danger)";
                div.innerHTML = `
                    <div style="display:flex; justify-content:space-between; align-items:center;">
                        <div>
                            <h4 style="color:var(--text-main);">${e.title}</h4>
                            <span style="font-size:12px; color:var(--text-muted);">${e.date}</span>
                        </div>
                        <div style="display:flex; align-items:center; gap:15px;">
                            <span style="font-size:17px; font-weight:800; color:var(--danger);">${e.amount.toFixed(2)} DA</span>
                            <button class="del" style="padding:6px 10px;" onclick="deleteExpense('${e.id}')"><i class="fa-solid fa-trash"></i></button>
                        </div>
                    </div>
                `;
                container.appendChild(div);
            });
        }

        function deleteExpense(id) {
            if(confirm("هل أنت متأكد من حذف وإلغاء تقييد هذا المصروف؟")) {
                expenses = expenses.filter(x => x.id !== id);
                save();
                render();
            }
        }

        /* ================= FINANCIAL PROFITS REPORTS ================= */
        function calculateProfits() {
            let todayStr = new Date().toISOString().split('T')[0];
            let currentMonthStr = todayStr.substring(0, 7);

            let daily = 0;
            let monthly = 0;
            let yearlyExpenses = 0;
            let totalSalesProfitYear = 0;

            sales.forEach(s => {
                let orderProfit = 0;
                s.items.forEach(i => {
                    orderProfit += (i.sellPrice - i.buyPrice) * i.qty;
                });

                if(s.date === todayStr) daily += orderProfit;
                if(s.date.substring(0,7) === currentMonthStr) monthly += orderProfit;
                
                totalSalesProfitYear += orderProfit;
            });

            expenses.forEach(e => {
                yearlyExpenses += e.amount;
                if(e.date === todayStr) daily -= e.amount;
                if(e.date.substring(0,7) === currentMonthStr) monthly -= e.amount;
            });

            let netYearly = totalSalesProfitYear - yearlyExpenses;

            document.getElementById("dailyProfit").textContent = daily.toFixed(2) + " DA";
            document.getElementById("monthlyProfit").textContent = monthly.toFixed(2) + " DA";
            document.getElementById("totalExpensesYear").textContent = yearlyExpenses.toFixed(2) + " DA 💸";
            document.getElementById("yearlyProfit").textContent = netYearly.toFixed(2) + " DA";

            calculateFilteredProfit();
        }

        function calculateFilteredProfit() {
            let from = document.getElementById("filterFrom").value;
            let to = document.getElementById("filterTo").value;

            if(!from || !to) return;

            let dFrom = new Date(from);
            let dTo = new Date(to);

            let salesProfit = 0;
            sales.forEach(s => {
                let d = new Date(s.date);
                if(d >= dFrom && d <= dTo) {
                    s.items.forEach(i => {
                        salesProfit += (i.sellPrice - i.buyPrice) * i.qty;
                    });
                }
            });

            let filterExp = 0;
            expenses.forEach(e => {
                let d = new Date(e.date);
                if(d >= dFrom && d <= dTo) {
                    filterExp += e.amount;
                }
            });

            let finalNet = salesProfit - filterExp;
            document.getElementById("filteredProfit").textContent = finalNet.toFixed(2) + " DA 💰";
        }

        /* ================= BACKUP SYSTEM ================= */
        function exportData() {
            let backupObject = {
                batches, 
                sales, 
                expenses, 
                commandNumber
            };
            
            let dataStr = "data:text/plain;charset=utf-8," + encodeURIComponent(JSON.stringify(backupObject));
            let downloadAnchor = document.createElement('a');
            downloadAnchor.setAttribute("href", dataStr);
            downloadAnchor.setAttribute("download", `POS_DATA_BACKUP_${new Date().toISOString().split('T')[0]}.txt`);
            document.body.appendChild(downloadAnchor);
            downloadAnchor.click();
            downloadAnchor.remove();
        }

        function triggerImport() {
            document.getElementById("importFileInput").click();
        }

        function importData(event) {
            let file = event.target.files[0];
            if (!file) return;

            let reader = new FileReader();
            reader.onload = function(e) {
                try {
                    let cleanRawText = e.target.result.trim();
                    let imported = JSON.parse(cleanRawText);
                    
                    if (imported && (imported.batches || imported.sales || imported.expenses)) {
                        
                        batches = imported.batches || [];
                        sales = imported.sales || [];
                        expenses = imported.expenses || [];
                        
                        let importedNum = parseInt(imported.commandNumber);
                        commandNumber = (!importedNum || isNaN(importedNum)) ? 1 : importedNum;
                        
                        save();
                        render();
                        document.getElementById('cmdNumberInput').value = commandNumber;
                        alert("✅ تم استيراد النسخة الاحتياطية وتحديث النظام بنجاح!");
                    } else {
                        alert("❌ خطأ: الملف لا يحتوي على هيكلة برمجية صحيحةلنظام الـ POS.");
                    }
                } catch(err) {
                    alert("❌ فشل الاستيراد: محتوى الملف غير متوافق أو تالف.");
                }
            };
            reader.readAsText(file);
            event.target.value = "";
        }
    </script>
</body>
</html>

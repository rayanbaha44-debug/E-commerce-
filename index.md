<!DOCTYPE html>
<html lang="ar" dir="rtl">

<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>POS SYSTEM PRO - نظام المبيعات الاحترافي</title>

<style>
/* ================= PROFESSIONAL MODERN UI ================= */
:root {
    --primary: #2563eb;
    --primary-hover: #1d4ed8;
    --success: #10b981;
    --success-hover: #059669;
    --danger: #ef4444;
    --danger-hover: #dc2626;
    --background: #f8fafc;
    --surface: #ffffff;
    --text-main: #0f172a;
    --text-muted: #64748b;
    --border: #e2e8f0;
}

*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
}

body{
    background: var(--background);
    color: var(--text-main);
    min-height: 100vh; 
    padding: 30px 20px;
    display: flex;
    justify-content: center;
    align-items: flex-start;
}

/* لوحة التحكم الرئيسية */
#dashboard{
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 16px;
    width: 100%;
    max-width: 800px;
    margin: 40px auto;
}

.card{
    background: var(--surface);
    padding: 30px 20px;
    border-radius: 16px;
    text-align: center;
    cursor: pointer;
    border: 1px solid var(--border);
    font-weight: 600;
    font-size: 18px;
    color: var(--text-main);
    transition: all 0.25s cubic-bezier(0.4, 0, 0.2, 1);
    box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.05), 0 2px 4px -2px rgb(0 0 0 / 0.05);
}

.card:hover{
    transform: translateY(-4px);
    border-color: var(--primary);
    box-shadow: 0 10px 15px -3px rgb(37 99 235 / 0.1), 0 4px 6px -4px rgb(37 99 235 / 0.1);
    color: var(--primary);
}

/* الصفحات والتقسيمات */
.page{
    display: none;
    width: 100%;
    max-width: 900px;
    background: var(--surface);
    padding: 30px;
    border-radius: 20px;
    box-shadow: 0 10px 25px -5px rgb(0 0 0 / 0.05);
    border: 1px solid var(--border);
    animation: fadeIn 0.3s ease-in-out;
}

@keyframes fadeIn {
    from { opacity: 0; transform: translateY(10px); }
    to { opacity: 1; transform: translateY(0); }
}

.page.active{
    display: block;
}

.header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 25px;
    padding-bottom: 15px;
    border-bottom: 2px solid var(--background);
}

.header h2 {
    font-size: 24px;
    font-weight: 700;
    color: var(--text-main);
}

/* الأزرار الاحترافية */
button{
    padding: 12px 24px;
    border: none;
    border-radius: 10px;
    cursor: pointer;
    background: var(--primary);
    color: white;
    font-weight: 600;
    font-size: 15px;
    transition: background 0.2s;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
}

button:hover{
    background: var(--primary-hover);
}

.back{
    background: var(--text-muted);
}
.back:hover{
    background: #475569;
}

/* المدخلات (Inputs) القابلة للقراءة بشكل ممتاز */
input, select{
    width: 100%;
    padding: 14px 16px;
    margin: 10px 0;
    border-radius: 10px;
    border: 1px solid var(--border);
    background: var(--background);
    color: var(--text-main);
    font-size: 16px;
    transition: all 0.2s;
}

input:focus, select:focus{
    outline: none;
    border-color: var(--primary);
    background: white;
    box-shadow: 0 0 0 4px rgb(37 99 235 / 0.1);
}

/* الجداول المنظمة */
table{
    width: 100%;
    margin-top: 20px;
    border-collapse: separate;
    border-spacing: 0;
    border-radius: 12px;
    overflow: hidden;
    border: 1px solid var(--border);
}

th, td{
    padding: 16px;
    text-align: center;
    border-bottom: 1px solid var(--border);
    font-size: 15px;
}

th {
    background-color: var(--background);
    color: var(--text-muted);
    font-weight: 600;
    text-transform: uppercase;
    font-size: 14px;
}

tr:last-child td {
    border-bottom: none;
}

.del{
    background: var(--danger);
}
.del:hover{ background: var(--danger-hover); }

.edit{
    background: #f1f5f9;
    color: var(--text-main);
    border: 1px solid var(--border);
}
.edit:hover{ background: var(--border); }

/* الصناديق الجانبية والحاويات */
.box{
    background: var(--background);
    padding: 20px;
    border-radius: 12px;
    margin-bottom: 16px;
    border: 1px solid var(--border);
}

.flex-inputs {
    display: flex;
    gap: 12px;
    align-items: center;
}

#salesLog{
    margin-top: 15px;
    max-height: 250px;
    overflow-y: auto;
}

.saleItem{
    padding: 12px;
    background: var(--surface);
    border-radius: 8px;
    margin-bottom: 8px;
    border: 1px solid var(--border);
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 15px;
}

/* تمييز الأرقام الهامة */
.badge-qty {
    background: #fef3c7;
    color: #d97706;
    padding: 4px 8px;
    border-radius: 6px;
    font-weight: 600;
}
</style>
</head>

<body>

<!-- DASHBOARD -->
<div id="dashboard">
    <div class="card" onclick="openPage('products')">📦 المنتجات</div>
    <div class="card" onclick="openPage('sales')">🛒 واجهة البيع</div>
    <div class="card" onclick="openPage('stock')">🏬 جرد المخزون</div>
    <div class="card" onclick="openPage('low')">⚠️ المواد الناقصة</div>
    <div class="card" onclick="openPage('profits')">💰 تقارير الأرباح</div>
    <div class="card" onclick="exportData()" style="background: #fafafa;">💾 تصدير البيانات</div>
</div>

<!-- PRODUCTS -->
<div id="products" class="page">
    <div class="header">
        <button class="back" onclick="back()">↩️ رجوع</button>
        <h2>📦 إدارة المنتجات</h2>
    </div>

    <div class="box">
        <input id="pRef" placeholder="الرقم المتسلسل / الباركود (Ref)">
        <input id="pName" placeholder="اسم المنتج بالكامل">
        <div class="flex-inputs">
            <input id="pBuy" type="number" step="0.01" placeholder="سعر الشراء (DA)">
            <input id="pSell" type="number" step="0.01" placeholder="سعر البيع (DA)">
            <input id="pQty" type="number" step="0.01" placeholder="الكمية الابتدائية">
        </div>
        <button onclick="addProduct()" style="width: 100%; margin-top: 10px; background: var(--success);">➕ إضافة المنتج للمخزن</button>
    </div>

    <input type="file" id="importFile" hidden onchange="importData(event)">
    <button onclick="document.getElementById('importFile').click()" style="background:var(--primary); width: 100%; margin-bottom: 15px;">📥 استيراد بيانات من ملف خارجي</button>

    <input id="productSearch" placeholder="🔍 ابحث هنا باسم المنتج أو الرمز للتصفية..." oninput="renderProducts()">

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
        <button class="back" onclick="back()">↩️ رجوع</button>
        <h2>🛒 واجهة البيع السريعة</h2>
    </div>

    <div class="box" style="border: 1px dashed var(--primary); background: #eff6ff;">
        <h4 style="color: var(--primary); margin-bottom: 8px;">✏️ تعديل ومراجعة كوموند سابق</h4>
        <div class="flex-inputs">
            <input id="editCmdNumInput" type="number" placeholder="أدخل رقم الكوموند القديم...">
            <button onclick="loadCommandForEdit()" style="white-space: nowrap;">جلب وتعديل</button>
        </div>
    </div>

    <div class="box" style="background: var(--text-main); color: white; text-align: center;">
        <h3 id="cmdNumber" style="font-weight: 700; letter-spacing: 1px;">Commande #1</h3>
    </div>

    <input id="saleSearch" placeholder="🔍 ابحث هنا عن المنتج المراد بيعه..." oninput="renderSalesOptions()">

    <select id="saleStock"></select>
    <!-- خطوة الزيادة مضبوطة على 1 لتقفز مباشرة للأرقام الكاملة -->
    <input id="saleQty" type="number" step="1" value="1" placeholder="الكمية">

    <button onclick="addToCommand()" style="width: 100%; margin-bottom: 20px;">🛒 إضافة إلى السلة</button>

    <div class="box" style="background: #fff; border: 2px solid var(--border);">
        <h3 style="margin-bottom: 10px; padding-bottom: 5px; border-bottom: 1px solid var(--border);">🛒 سلة التسوق الحالية</h3>
        <div id="currentCommand"></div>
        <h3 id="commandTotal" style="margin-top:15px; color: var(--success); text-align: left;">المجموع: 0.00 DA</h3>
        <button onclick="confirmCommand()" style="width:100%; margin-top:15px; background: var(--success); font-size: 18px; padding: 16px;">✔️ تأكيد وحفظ الطلب (OK)</button>
    </div>

    <h3 style="margin-top: 20px; color: var(--text-muted)">📋 سجل عمليات اليوم</h3>
    <div id="salesLog"></div>
</div>

<!-- STOCK -->
<div id="stock" class="page">
    <div class="header">
        <button class="back" onclick="back()">↩️ رجوع</button>
        <h2>🏬 كشف وجرد المخزن</h2>
    </div>
    <table>
        <thead>
            <tr><th>اسم المنتج</th><th>القطع المتبقية</th><th>رأس المال المستثمر</th><th>الأرباح المتوقعة</th><th>إجراء</th></tr>
        </thead>
        <tbody id="stockTable"></tbody>
    </table>
    <div id="totals" class="box" style="margin-top:20px; line-height: 2; background: #f8fafc;"></div>
</div>

<!-- LOW -->
<div id="low" class="page">
    <div class="header">
        <button class="back" onclick="back()">↩️ رجوع</button>
        <h2>⚠️ تنبيه السلع الناقصة</h2>
    </div>
    <table>
        <thead><tr><th>اسم المنتج</th><th>الكمية الحالية</th><th>حالة السلعة</th></tr></thead>
        <tbody id="lowTable"></tbody>
    </table>
</div>

<!-- PROFITS -->
<div id="profits" class="page">
    <div class="header">
        <button class="back" onclick="back()">↩️ رجوع</button>
        <h2>💰 التقارير المالية والأرباح</h2>
    </div>
    <div class="box" style="border-right: 5px solid var(--success);">
        <p style="color: var(--text-muted)">أرباح اليوم الحالي</p>
        <div id="dailyProfit" style="font-size: 28px; font-weight: 800; color: var(--success);">0.00 DA</div>
    </div>
    <div class="box" style="border-right: 5px solid var(--primary);">
        <p style="color: var(--text-muted)">أرباح الشهر الحالي</p>
        <div id="monthlyProfit" style="font-size: 28px; font-weight: 800; color: var(--primary);">0.00 DA</div>
    </div>
    <div class="box" style="border-right: 5px solid var(--text-main);">
        <p style="color: var(--text-muted)">أرباح السنة الإجمالية</p>
        <div id="yearlyProfit" style="font-size: 28px; font-weight: 800; color: var(--text-main);">0.00 DA</div>
    </div>
</div>

<script>
/* ================= SYSTEM LOGIC ================= */
let batches = JSON.parse(localStorage.getItem("batches") || "[]");
let sales = JSON.parse(localStorage.getItem("sales") || "[]");

let commandNumber = Number(localStorage.getItem("commandNumber"));
if (!commandNumber) {
    if (sales.length > 0) {
        let maxExistingCmd = sales.reduce((max, s) => s.command > max ? s.command : max, 0);
        commandNumber = maxExistingCmd + 1;
    } else {
        commandNumber = 1;
    }
}
let currentCommandData = [];

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

    let maxExistingCmd = sales.reduce((max, s) => s.command > max ? s.command : max, 0);
    commandNumber = maxExistingCmd + 1;
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
        <div style="display:flex; justify-content:space-between; align-items:center; margin:8px 0; background:var(--background); padding:12px; border-radius:10px; border: 1px solid var(--border);">
            <span style="font-weight:600;">${i.name} <span class="badge-qty">x${i.qty}</span></span>
            <span style="color:var(--primary); font-weight:bold;">${(i.sell*i.qty).toFixed(2)} DA</span>
            <div style="display:flex; gap:6px;">
                <button class="edit" onclick="editCommandItemPrice(${idx})" style="padding:5px 10px; font-size:12px;">✏️ السعر</button>
                <button class="del" onclick="removeFromCommand(${idx})" style="padding:5px 10px; font-size:12px;">❌ إلغاء</button>
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
        <td><button class="edit" onclick="editProduct(${b.id})">تعديل</button></td>
        <td><button class="del" onclick="deleteProduct(${b.id})">حذف</button></td>
    </tr>`).join("");
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
            <td><span class="badge-qty">${b.qty} قطعة</span></td>
            <td>${capital.toFixed(2)} DA</td>
            <td>${expectedProfit.toFixed(2)} DA</td>
            <td><button class="del" onclick="deleteProduct(${b.id})">حذف</button></td>
        </tr>`;
    }).join("");

    document.getElementById('totals').innerHTML = `
        <p>📊 <strong>إجمالي رأس المال في المستودع:</strong> ${totalCapital.toFixed(2)} DA</p>
        <p>📈 <strong>القيمة الإجمالية المتوقعة عند البيع:</strong> ${totalValue.toFixed(2)} DA</p>
        <p style="color:var(--success)">✨ <strong>صافي الأرباح المنتظرة:</strong> ${(totalValue - totalCapital).toFixed(2)} DA</p>`;

    document.getElementById('salesLog').innerHTML = [...sales].reverse().map((s,i)=>{
        let idx = sales.length-1-i;
        return `
        <div class="saleItem">
            <span><b style="color:var(--primary);">#${s.command}</b> - ${s.name} (x${s.qty})</span>
            <span>الربح: <b style="color:var(--success);">${s.profit.toFixed(2)} DA</b></span>
            <button class="del" onclick="deleteSale(${idx})" style="padding:4px 8px; font-size:12px;">❌ حذف المبيعة</button>
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
        <td><span class="badge-qty" style="background:none; color:inherit;">${b.qty} قطع متبقية</span></td>
        <td><span style="color:${b.qty === 0 ? 'var(--danger)':'#d97706'}; font-weight:700;">${b.qty === 0 ? 'منتهي تماماً ❌' : 'شبه فارغ ⚠️'}</span></td>
    </tr>`).join("");
    
    if(lowItems.length === 0){
        document.getElementById('lowTable').innerHTML = `<tr><td colspan="3" style="color:var(--success)">كل السلع متوفرة بحالة ممتازة 🎉</td></tr>`;
    }
    document.getElementById('cmdNumber').innerHTML = "Commande #" + commandNumber;
}

function exportData(){
    let dataStr = JSON.stringify({ batches, sales, commandNumber });
    let dataUri = 'data:application/json;charset=utf-8,'+ encodeURIComponent(dataStr);
    let linkElement = document.createElement('a');
    linkElement.setAttribute('href', dataUri);
    linkElement.setAttribute('download', 'pos_backup_' + new Date().toISOString().slice(0,10) + '.json');
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

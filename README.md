<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tailoring Business App</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; margin: 0; padding: 0; background: #0b132b; color: #ffffff; }
        
        /* Navbar */
        .navbar { background: #1c2541; padding: 15px 25px; display: flex; justify-content: space-between; align-items: center; border-bottom: 2px solid #3a506b; position: relative; }
        .navbar h2 { margin: 0; font-size: 22px; color: #6fffe9; font-weight: bold; }
        
        /* Hamburger Menu */
        .menu-icon { font-size: 26px; cursor: pointer; color: #ffffff; user-select: none; }
        .dropdown-menu { display: none; position: absolute; right: 20px; top: 60px; background: #1c2541; border: 1px solid #3a506b; border-radius: 6px; box-shadow: 0 5px 15px rgba(0,0,0,0.5); z-index: 1000; width: 200px; }
        .dropdown-menu button { display: block; width: 100%; background: none; border: none; color: white; padding: 12px 15px; text-align: left; cursor: pointer; font-size: 15px; border-bottom: 1px solid #3a506b; }
        .dropdown-menu button:hover { background: #3a506b; color: #6fffe9; }

        .container { max-width: 1200px; margin: 20px auto; padding: 20px; }
        .page { display: none; }
        .page.active { display: block; }
        
        h2, h3 { color: #6fffe9; font-weight: bold; }
        
        /* Dashboard Cards */
        .dashboard { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 20px; margin-bottom: 30px; }
        .card { background: #1c2541; padding: 20px; border-radius: 10px; border-left: 6px solid #48cae4; box-shadow: 0 4px 10px rgba(0,0,0,0.3); }
        .card.profit-card { border-left-color: #2ec4b6; background: #0f2a24; }
        .card.expense-card { border-left-color: #e71d36; background: #2c1215; }
        .card p { font-size: 16px; margin: 8px 0; }
        .card span { font-weight: bold; }

        /* Forms & Inputs */
        .form-box { background: #1c2541; padding: 25px; border-radius: 10px; border: 1px solid #3a506b; max-width: 600px; margin: auto; }
        .form-group { margin-bottom: 15px; }
        label { display: block; margin-bottom: 5px; font-weight: bold; color: #caf0f8; }
        input, select { width: 100%; padding: 10px; box-sizing: border-box; background: #0b132b; border: 1px solid #3a506b; color: white; border-radius: 5px; font-size: 15px; }
        button.btn-primary { background: #2ec4b6; color: #0b132b; border: none; padding: 12px; cursor: pointer; border-radius: 5px; width: 100%; font-size: 16px; font-weight: bold; margin-top: 10px; }
        button.btn-primary:hover { background: #4uz9f6; }

        /* Tables */
        table { width: 100%; border-collapse: collapse; margin-top: 20px; background: #1c2541; border-radius: 8px; overflow: hidden; }
        th, td { border: 1px solid #3a506b; padding: 12px; text-align: left; }
        th { background: #3a506b; color: #6fffe9; }
        .whatsapp-link { color: #2ec4b6; text-decoration: none; font-weight: bold; }
        
        .badge-green { color: #2ec4b6; font-weight: bold; }
        .badge-red { color: #e71d36; font-weight: bold; }
    </style>
</head>
<body>

<!-- Navbar with Hamburger Menu -->
<div class="navbar">
    <h2>TAILORING APP</h2>
    <div class="menu-icon" onclick="toggleMenu()">☰</div>
    <div class="dropdown-menu" id="dropdownMenu">
        <button onclick="switchPage('dashboardPage')">Dashboard</button>
        <button onclick="switchPage('customerPage')">Add Customer</button>
        <button onclick="switchPage('itemPage')">Add Item</button>
        <button onclick="switchPage('employeePage')">Add Employee</button>
        <button onclick="switchPage('completedPage')">Completed Works</button>
        <button onclick="switchPage('analyticsPage')">Data Analytics</button>
    </div>
</div>

<div class="container">

    <!-- 1. DASHBOARD PAGE -->
    <div id="dashboardPage" class="page active">
        <h2>BUSINESS DASHBOARD</h2>
        <div class="dashboard">
            <div class="card profit-card">
                <h3>Total Revenue & Profit</h3>
                <p>Total Revenue: ₹<span id="totRevenue">0</span></p>
                <p>Total Profit: <span class="badge-green">₹<span id="totProfit">0</span></span></p>
            </div>
            <div class="card">
                <h3>BEBI Platform</h3>
                <p>Revenue: ₹<span id="bebiRev">0</span> | Profit: <span class="badge-green">₹<span id="bebiProf">0</span></span></p>
            </div>
            <div class="card">
                <h3>LEDI Platform</h3>
                <p>Revenue: ₹<span id="lediRev">0</span> | Profit: <span class="badge-green">₹<span id="lediProf">0</span></span></p>
            </div>
            <div class="card profit-card" style="border-left-color: #2ec4b6;">
                <h3>Ani's Account</h3>
                <p style="font-size: 24px;" class="badge-green">₹<span id="aniTotal">0</span></p>
            </div>
        </div>

        <h3>Active Ongoing Works</h3>
        <table>
            <thead>
                <tr>
                    <th>Name</th>
                    <th>WhatsApp</th>
                    <th>Platform</th>
                    <th>Delivery</th>
                    <th>Revenue</th>
                    <th>Profit</th>
                    <th>Ani's Share</th>
                    <th>Action</th>
                </tr>
            </thead>
            <tbody id="activeCustomerTable"></tbody>
        </table>
    </div>

    <!-- 2. ADD CUSTOMER PAGE -->
    <div id="customerPage" class="page">
        <div class="form-box">
            <h2>Add New Customer</h2>
            <div class="form-group"><label>Customer Name</label><input type="text" id="custName"></div>
            <div class="form-group"><label>WhatsApp Number</label><input type="text" id="custPhone" placeholder="919876543210"></div>
            <div class="form-group"><label>Platform</label><select id="platform"><option value="BEBI">BEBI</option><option value="LEDI">LEDI</option></select></div>
            <div class="form-group"><label>Delivery Date</label><input type="date" id="delDate"></div>
            <div class="form-group"><label>Total Price</label><input type="number" id="totPrice" oninput="calculatePreview()"></div>
            <div class="form-group"><label>Advance Amount</label><input type="number" id="advAmount"></div>
            <div class="form-group"><label>Total Expense</label><input type="number" id="totExpense" oninput="calculatePreview()"></div>
            <div class="form-group"><label>Stitched By (Employee)</label><select id="stitchEmp"></select></div>
            <div class="form-group"><label>Stitching Amount</label><input type="number" id="stitchAmount"></div>
            
            <div style="background: #0b132b; padding: 10px; border-radius: 5px; margin-bottom: 15px;">
                <p>Preview Profit: <span class="badge-green">₹<span id="calcProfit">0</span></span></p>
                <p>Ani's Share: <span class="badge-green">₹<span id="calcAni">0</span></span></p>
            </div>
            <button class="btn-primary" onclick="addCustomer()">Save Customer</button>
        </div>
    </div>

    <!-- 3. ADD ITEM PAGE -->
    <div id="itemPage" class="page">
        <div class="form-box">
            <h2>Add New Item (Max 5MB Image)</h2>
            <div class="form-group"><label>Item Name</label><input type="text" id="itemName"></div>
            <div class="form-group"><label>Item Price</label><input type="number" id="itemPrice"></div>
            <div class="form-group"><label>Upload Image (Max 5MB)</label><input type="file" id="itemImage" accept="image/*"></div>
            <button class="btn-primary" onclick="addItem()">Save Item</button>
        </div>
        <h3 style="margin-top:30px;">Item List</h3>
        <table>
            <thead><tr><th>Image</th><th>Item Name</th><th>Price</th><th>Action</th></tr></thead>
            <tbody id="itemTableBody"></tbody>
        </table>
    </div>

    <!-- 4. ADD EMPLOYEE PAGE -->
    <div id="employeePage" class="page">
        <div class="form-box">
            <h2>Manage Employees</h2>
            <div class="form-group"><label>Employee Name</label><input type="text" id="empName"></div>
            <button class="btn-primary" onclick="addEmployee()">Save Employee</button>
        </div>
        <h3 style="margin-top:30px;">Employee List</h3>
        <table>
            <thead><tr><th>Name</th><th>Action</th></tr></thead>
            <tbody id="employeeTableBody"></tbody>
        </table>
    </div>

    <!-- 5. COMPLETED WORKS -->
    <div id="completedPage" class="page">
        <h2>Completed Works History</h2>
        <table>
            <thead><tr><th>Name</th><th>Platform</th><th>Delivery Date</th><th>Revenue</th><th>Profit</th><th>Ani's Share</th><th>Action</th></tr></thead>
            <tbody id="completedCustomerTable"></tbody>
        </table>
    </div>

    <!-- 6. DATA ANALYTICS PAGE -->
    <div id="analyticsPage" class="page">
        <h2>Data Analytics by Date</h2>
        <div class="form-box" style="margin-bottom: 20px;">
            <div class="form-group"><label>Select Date</label><input type="date" id="filterDate" onchange="filterAnalytics()"></div>
        </div>
        <h3>Analytics Results</h3>
        <table>
            <thead><tr><th>Name</th><th>Platform</th><th>Date</th><th>Revenue</th><th>Profit</th><th>Expense</th></tr></thead>
            <tbody id="analyticsTableBody"></tbody>
        </table>
    </div>

</div>

<!-- Firebase SDKs -->
<script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
    import { getFirestore, collection, addDoc, doc, updateDoc, deleteDoc, onSnapshot } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-firestore.js";

    const firebaseConfig = {
        apiKey: "YOUR_API_KEY",
        authDomain: "YOUR_AUTH_DOMAIN",
        projectId: "YOUR_PROJECT_ID",
        storageBucket: "YOUR_STORAGE_BUCKET",
        messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
        appId: "YOUR_APP_ID"
    };

    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);

    let allCustomersCache = [];

    window.toggleMenu = function() {
        let menu = document.getElementById('dropdownMenu');
        menu.style.display = menu.style.display === 'block' ? 'none' : 'block';
    }

    window.switchPage = function(pageId) {
        document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
        document.getElementById(pageId).classList.add('active');
        document.getElementById('dropdownMenu').style.display = 'none';
    }

    window.addEmployee = async function() {
        const name = document.getElementById('empName').value;
        if(!name) return alert('Enter name!');
        await addDoc(collection(db, "employees"), { name });
        document.getElementById('empName').value = '';
        alert('Employee Saved!');
    }

    window.deleteEmployee = async function(id) {
        if(confirm('Delete?')) await deleteDoc(doc(db, "employees", id));
    }

    window.addItem = async function() {
        const name = document.getElementById('itemName').value;
        const price = document.getElementById('itemPrice').value;
        const fileInput = document.getElementById('itemImage');
        
        if(!name || !price) return alert('Fill fields!');
        
        let imageUrl = "";
        if(fileInput.files.length > 0) {
            let file = fileInput.files[0];
            if(file.size > 5 * 1024 * 1024) return alert('Image size must be less than 5MB!');
            
            // Convert to Base64 for simple storage
            const reader = new FileReader();
            reader.readAsDataURL(file);
            reader.onload = async function() {
                imageUrl = reader.result;
                await addDoc(collection(db, "items"), { name, price, imageUrl });
                alert('Item Saved!');
                document.getElementById('itemName').value = '';
                document.getElementById('itemPrice').value = '';
                document.getElementById('itemImage').value = '';
            };
            return;
        }

        await addDoc(collection(db, "items"), { name, price, imageUrl: "" });
        alert('Item Saved!');
    }

    window.deleteItem = async function(id) {
        await deleteDoc(doc(db, "items", id));
    }

    window.calculatePreview = function() {
        const price = parseFloat(document.getElementById('totPrice').value) || 0;
        const expense = parseFloat(document.getElementById('totExpense').value) || 0;
        let rawProfit = price - expense;
        let aniShare = rawProfit > 300 ? 300 : (rawProfit > 0 ? rawProfit : 0);
        let finalProfit = rawProfit > 300 ? rawProfit - 300 : 0;

        document.getElementById('calcProfit').innerText = finalProfit;
        document.getElementById('calcAni').innerText = aniShare;
    }

    window.addCustomer = async function() {
        const name = document.getElementById('custName').value;
        const phone = document.getElementById('custPhone').value;
        const platform = document.getElementById('platform').value;
        const delDate = document.getElementById('delDate').value;
        const totPrice = parseFloat(document.getElementById('totPrice').value) || 0;
        const advAmount = parseFloat(document.getElementById('advAmount').value) || 0;
        const totExpense = parseFloat(document.getElementById('totExpense').value) || 0;
        const stitchEmp = document.getElementById('stitchEmp').value;
        const stitchAmount = parseFloat(document.getElementById('stitchAmount').value) || 0;

        const rawProfit = totPrice - totExpense;
        let aniShare = rawProfit > 300 ? 300 : (rawProfit > 0 ? rawProfit : 0);
        let finalProfit = rawProfit > 300 ? rawProfit - 300 : 0;

        await addDoc(collection(db, "customers"), {
            name, phone, platform, delDate, totPrice, advAmount, totExpense, stitchEmp, stitchAmount,
            profit: finalProfit, aniAmount: aniShare, revenue: totPrice, status: 'ongoing'
        });

        alert('Customer Saved!');
    }

    window.markCompleted = async function(id) {
        await updateDoc(doc(db, "customers", id), { status: 'completed' });
    }

    window.deleteCust = async function(id) {
        if(confirm('Delete?')) await deleteDoc(doc(db, "customers", id));
    }

    window.filterAnalytics = function() {
        const selectedDate = document.getElementById('filterDate').value;
        let tbody = document.getElementById('analyticsTableBody');
        tbody.innerHTML = '';
        
        allCustomersCache.forEach(data => {
            if(!selectedDate || data.delDate === selectedDate) {
                tbody.innerHTML += `
                    <tr>
                        <td>${data.name}</td>
                        <td>${data.platform}</td>
                        <td>${data.delDate}</td>
                        <td>₹${data.revenue}</td>
                        <td class="badge-green">₹${data.profit}</td>
                        <td class="badge-red">₹${data.totExpense}</td>
                    </tr>
                `;
            }
        });
    }

    // Realtime Syncs
    onSnapshot(collection(db, "employees"), (snapshot) => {
        let select = document.getElementById('stitchEmp');
        let empTable = document.getElementById('employeeTableBody');
        select.innerHTML = ''; empTable.innerHTML = '';
        snapshot.forEach(docSnap => {
            let emp = docSnap.data();
            select.innerHTML += `<option value="${emp.name}">${emp.name}</option>`;
            empTable.innerHTML += `<tr><td>${emp.name}</td><td><button onclick="deleteEmployee('${docSnap.id}')" style="background:#e71d36; color:white; border:none; padding:5px; cursor:pointer;">Delete</button></td></tr>`;
        });
    });

    onSnapshot(collection(db, "items"), (snapshot) => {
        let itemTable = document.getElementById('itemTableBody');
        itemTable.innerHTML = '';
        snapshot.forEach(docSnap => {
            let item = docSnap.data();
            itemTable.innerHTML += `
                <tr>
                    <td>${item.imageUrl ? `<img src="${item.imageUrl}" width="50" height="50" style="border-radius:5px;">` : 'No Image'}</td>
                    <td>${item.name}</td>
                    <td>₹${item.price}</td>
                    <td><button onclick="deleteItem('${docSnap.id}')" style="background:#e71d36; color:white; border:none; padding:5px; cursor:pointer;">Delete</button></td>
                </tr>
            `;
        });
    });

    onSnapshot(collection(db, "customers"), (snapshot) => {
        let activeTable = document.getElementById('activeCustomerTable');
        let completedTable = document.getElementById('completedCustomerTable');
        activeTable.innerHTML = ''; completedTable.innerHTML = '';
        allCustomersCache = [];

        let totRev = 0, totProf = 0, aniTot = 0, bebiRev = 0, bebiProf = 0, lediRev = 0, lediProf = 0;

        snapshot.forEach(docSnap => {
            let data = docSnap.data();
            let id = docSnap.id;
            allCustomersCache.push(data);

            totRev += data.revenue || 0;
            totProf += data.profit || 0;
            aniTot += data.aniAmount || 0;

            if(data.platform === 'BEBI') { bebiRev += data.revenue || 0; bebiProf += data.profit || 0; }
            else if(data.platform === 'LEDI') { lediRev += data.revenue || 0; lediProf += data.profit || 0; }

            let waLink = data.phone ? `https://wa.me/${data.phone.replace(/[^0-9]/g, '')}` : '#';

            let row = `
                <tr>
                    <td>${data.name}</td>
                    ${data.status === 'ongoing' ? `<td><a href="${waLink}" target="_blank" class="whatsapp-link">💬 ${data.phone || ''}</a></td>` : ''}
                    <td>${data.platform}</td>
                    <td>${data.delDate || ''}</td>
                    <td>₹${data.revenue}</td>
                    <td class="badge-green">₹${data.profit}</td>
                    <td class="badge-green">₹${data.aniAmount}</td>
                    <td>
                        ${data.status === 'ongoing' ? `<button onclick="markCompleted('${id}')" style="background:#2ec4b6; border:none; padding:5px; cursor:pointer; font-weight:bold;">Complete</button>` : ''}
                        <button onclick="deleteCust('${id}')" style="background:#e71d36; color:white; border:none; padding:5px; cursor:pointer;">Delete</button>
                    </td>
                </tr>
            `;

            if(data.status === 'completed') completedTable.innerHTML += row;
            else activeTable.innerHTML += row;
        });

        document.getElementById('totRevenue').innerText = totRev;
        document.getElementById('totProfit').innerText = totProf;
        document.getElementById('aniTotal').innerText = aniTot;
        document.getElementById('bebiRev').innerText = bebiRev;
        document.getElementById('bebiProf').innerText = bebiProf;
        document.getElementById('lediRev').innerText = lediRev;
        document.getElementById('lediProf').innerText = lediProf;
        filterAnalytics();
    });
</script>

</body>
</html>

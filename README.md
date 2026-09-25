<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cricket Schedule & Points Table Portal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        .hidden-section { display: none; }
    </style>
</head>
<body class="bg-slate-100 font-sans text-gray-800">

    <!-- Navbar -->
    <nav class="bg-emerald-700 text-white p-4 shadow-md flex justify-between items-center">
        <h1 class="text-xl font-bold">🏏 Cricket Portal</h1>
        <div id="nav-user-info" class="flex items-center gap-3 hidden-section flex-wrap">
            <span id="nav-phone" class="text-xs bg-emerald-800 px-2 py-1 rounded"></span>
            <span id="nav-wallet" class="text-xs bg-amber-500 text-slate-900 font-bold px-2 py-1 rounded"></span>
            <span id="nav-rupees" class="text-xs bg-blue-600 text-white font-bold px-2 py-1 rounded"></span>
            <span id="nav-diamonds" class="text-xs bg-purple-600 text-white font-bold px-2 py-1 rounded"></span>
            <button onclick="logout()" class="bg-red-600 px-2 py-1 text-xs rounded hover:bg-red-700">Logout</button>
        </div>
    </nav>

    <div class="container mx-auto p-4 max-w-5xl">

        <!-- 1. LOGIN SECTION -->
        <div id="login-section" class="bg-white p-6 rounded-lg shadow-md max-w-md mx-auto mt-10">
            <h2 class="text-2xl font-bold text-center mb-4 text-emerald-700">Login / Register</h2>
            <div class="mb-4">
                <label class="block text-sm font-medium mb-1">Mobile Number:</label>
                <input type="text" id="login-phone" placeholder="Enter Mobile Number" class="w-full p-2 border rounded focus:ring-2 focus:ring-emerald-500">
            </div>
            <div class="mb-4">
                <label class="block text-sm font-medium mb-1">Unique User ID (Exactly 5 letters/chars):</label>
                <input type="text" id="login-userid" maxlength="5" placeholder="e.g. df43h" class="w-full p-2 border rounded focus:ring-2 focus:ring-emerald-500">
            </div>
            <button onclick="handleLogin()" class="w-full bg-emerald-600 text-white py-2 rounded font-bold hover:bg-emerald-700">Login</button>
            <p class="text-xs text-gray-500 mt-3 text-center">Note: Special number `9569981484` gets welcome bonus!</p>
        </div>

        <!-- 2. MAIN DASHBOARD -->
        <div id="dashboard-section" class="hidden-section">
            <!-- Tabs -->
            <div class="flex flex-wrap gap-2 mb-6 border-b pb-2">
                <button onclick="switchTab('matches')" class="px-3 py-2 bg-emerald-600 text-white rounded font-medium text-sm tab-btn" id="btn-matches">Match Schedule</button>
                <button onclick="switchTab('points')" class="px-3 py-2 bg-gray-200 text-gray-700 rounded font-medium text-sm tab-btn" id="btn-points">Points Table</button>
                <button onclick="switchTab('diamonds')" class="px-3 py-2 bg-gray-200 text-gray-700 rounded font-medium text-sm tab-btn" id="btn-diamonds">💎 Buy Diamonds (Real ₹)</button>
                <button onclick="switchTab('shop')" class="px-3 py-2 bg-gray-200 text-gray-700 rounded font-medium text-sm tab-btn" id="btn-shop">🛍️ Voucher Store</button>
                <button onclick="switchTab('dailycode')" class="px-3 py-2 bg-gray-200 text-gray-700 rounded font-medium text-sm tab-btn" id="btn-dailycode">🎁 Daily Code</button>
                <button onclick="switchTab('subscription')" class="px-3 py-2 bg-gray-200 text-gray-700 rounded font-medium text-sm tab-btn" id="btn-subscription">Subscriptions</button>
                <button onclick="switchTab('addcoins')" class="px-3 py-2 bg-gray-200 text-gray-700 rounded font-medium text-sm tab-btn" id="btn-addcoins">Redeem Voucher</button>
                <button onclick="switchTab('admin')" class="px-3 py-2 bg-gray-200 text-gray-700 rounded font-medium text-sm tab-btn" id="btn-admin">Admin Panel</button>
            </div>

            <!-- TAB 1: MATCH SCHEDULE -->
            <div id="tab-matches" class="space-y-4">
                <h3 id="schedule-series-title" class="text-xl font-bold text-emerald-800">Scheduled Matches</h3>
                <div id="matches-list" class="space-y-4"></div>
            </div>

            <!-- TAB 2: POINTS TABLE -->
            <div id="tab-points" class="hidden-section space-y-6">
                <h3 class="text-xl font-bold text-emerald-800">ICC Points Table</h3>
                <div id="points-tables-container" class="space-y-6"></div>
            </div>

            <!-- TAB 3: BUY DIAMONDS (REAL PAYMENT -> Ashadkazitola@gmail.com) -->
            <div id="tab-diamonds" class="hidden-section bg-white p-6 rounded-lg shadow-md max-w-xl mx-auto space-y-4">
                <h3 class="text-xl font-bold text-purple-800">💎 Buy Diamonds & Balance via Google Play</h3>
                <p class="text-sm text-gray-600">Real money (Google Play Billing / UPI) ke zariye Diamonds kharidein. Yeh sabhi transactions seedhe <b>Ashadkazitola@gmail.com</b> ke merchant account par process honge.</p>
                
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div class="border p-4 rounded-lg bg-purple-50 flex flex-col justify-between">
                        <div>
                            <h4 class="font-bold text-purple-900">Starter Diamond Pack</h4>
                            <p class="text-xs text-gray-600 mb-2">50 Diamonds + ₹50 Wallet Credit</p>
                            <p class="text-sm font-bold text-emerald-700 mb-3">Price: ₹50</p>
                        </div>
                        <button onclick="buyDiamondsReal(50, 50, 'Starter Pack')" class="bg-purple-600 text-white py-2 rounded text-sm font-bold hover:bg-purple-700">Pay ₹50 via Play Store</button>
                    </div>

                    <div class="border p-4 rounded-lg bg-purple-50 flex flex-col justify-between">
                        <div>
                            <h4 class="font-bold text-purple-900">Pro Diamond Pack</h4>
                            <p class="text-xs text-gray-600 mb-2">150 Diamonds + ₹150 Wallet Credit</p>
                            <p class="text-sm font-bold text-emerald-700 mb-3">Price: ₹149</p>
                        </div>
                        <button onclick="buyDiamondsReal(150, 150, 'Pro Pack')" class="bg-purple-600 text-white py-2 rounded text-sm font-bold hover:bg-purple-700">Pay ₹149 via Play Store</button>
                    </div>

                    <div class="border p-4 rounded-lg bg-purple-50 flex flex-col justify-between">
                        <div>
                            <h4 class="font-bold text-purple-900">Mega Diamond Pack</h4>
                            <p class="text-xs text-gray-600 mb-2">500 Diamonds + ₹500 Wallet Credit</p>
                            <p class="text-sm font-bold text-emerald-700 mb-3">Price: ₹499</p>
                        </div>
                        <button onclick="buyDiamondsReal(500, 500, 'Mega Pack')" class="bg-purple-600 text-white py-2 rounded text-sm font-bold hover:bg-purple-700">Pay ₹499 via Play Store</button>
                    </div>

                    <div class="border p-4 rounded-lg bg-purple-50 flex flex-col justify-between">
                        <div>
                            <h4 class="font-bold text-purple-900">Ultra VIP Pack</h4>
                            <p class="text-xs text-gray-600 mb-2">2000 Diamonds + ₹2000 Wallet Credit</p>
                            <p class="text-sm font-bold text-emerald-700 mb-3">Price: ₹1999</p>
                        </div>
                        <button onclick="buyDiamondsReal(2000, 2000, 'Ultra VIP Pack')" class="bg-purple-600 text-white py-2 rounded text-sm font-bold hover:bg-purple-700">Pay ₹1999 via Play Store</button>
                    </div>
                </div>
            </div>

            <!-- TAB 4: VOUCHER STORE -->
            <div id="tab-shop" class="hidden-section bg-white p-6 rounded-lg shadow-md space-y-4">
                <h3 class="text-xl font-bold text-emerald-800">🛍️ Voucher Store (Spend ₹ Balance)</h3>
                <p class="text-sm text-gray-600">Apne ₹ Balance ka istemal karke points ke naye voucher generate karein.</p>
                
                <div id="shop-voucher-box" style="display: none;" class="bg-amber-50 border border-amber-300 p-4 rounded mb-4">
                    <p class="text-xs text-gray-600 mb-1">Aapka Generated Voucher Code:</p>
                    <div class="flex items-center justify-between bg-white p-2 border rounded">
                        <span id="shop-gen-code" class="font-bold text-emerald-700 text-base select-all"></span>
                        <button onclick="copyShopCode()" class="bg-emerald-600 text-white text-xs px-3 py-1 rounded hover:bg-emerald-700">Copy Code</button>
                    </div>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                    <div class="p-4 border rounded shadow-sm bg-gray-50 flex flex-col justify-between">
                        <div>
                            <p class="font-bold text-lg text-emerald-800">120 Points</p>
                            <p class="text-sm text-gray-600 mb-3">Cost: ₹49</p>
                        </div>
                        <button onclick="buyVoucherFromBalance(49, 120, '120 Points Voucher')" class="bg-emerald-600 text-white px-4 py-2 rounded text-sm font-bold hover:bg-emerald-700 w-full">Redeem for ₹49</button>
                    </div>

                    <div class="p-4 border rounded shadow-sm bg-gray-50 flex flex-col justify-between">
                        <div>
                            <p class="font-bold text-lg text-emerald-800">500 Points</p>
                            <p class="text-sm text-gray-600 mb-3">Cost: ₹200</p>
                        </div>
                        <button onclick="buyVoucherFromBalance(200, 500, '500 Points Voucher')" class="bg-emerald-600 text-white px-4 py-2 rounded text-sm font-bold hover:bg-emerald-700 w-full">Redeem for ₹200</button>
                    </div>

                    <div class="p-4 border rounded shadow-sm bg-gray-50 flex flex-col justify-between">
                        <div>
                            <p class="font-bold text-lg text-emerald-800">3000 Points</p>
                            <p class="text-sm text-gray-600 mb-3">Cost: ₹800</p>
                        </div>
                        <button onclick="buyVoucherFromBalance(800, 3000, '3000 Points Voucher')" class="bg-emerald-600 text-white px-4 py-2 rounded text-sm font-bold hover:bg-emerald-700 w-full">Redeem for ₹800</button>
                    </div>
                </div>
            </div>

            <!-- TAB 5: DAILY CODE (8 LETTERS -> RANDOM ₹) -->
            <div id="tab-dailycode" class="hidden-section bg-white p-6 rounded-lg shadow-md max-w-lg mx-auto space-y-4">
                <h3 class="text-xl font-bold text-indigo-800">🎁 Daily Code Reward (8 Letters)</h3>
                <p class="text-sm text-gray-600">Koi bhi 8 aksharon (letters) ka code enter karein aur random ₹ Balance jeetein (kabhi kam, kabhi zyada)! (Ek din mein ek baar).</p>
                
                <div class="mb-4">
                    <label class="block text-sm font-medium mb-1">Enter 8-Letter Code:</label>
                    <input type="text" id="daily-code-input" maxlength="8" placeholder="e.g. CRICKET8" class="w-full p-2 border rounded focus:ring-2 focus:ring-indigo-500 uppercase tracking-widest font-bold text-center">
                </div>
                <button onclick="redeemDailyCode()" class="w-full bg-indigo-600 text-white py-2 rounded font-bold hover:bg-indigo-700">Claim Reward</button>
                <div id="daily-result-box" class="hidden-section p-3 bg-indigo-50 border border-indigo-200 rounded text-center font-bold text-indigo-900"></div>
            </div>

            <!-- TAB 6: SUBSCRIPTION (DIRECT POINTS) -->
            <div id="tab-subscription" class="hidden-section bg-white p-6 rounded-lg shadow-md">
                <h3 class="text-xl font-bold mb-4 text-emerald-800">Active Admin Subscription</h3>
                <div id="subscription-status" class="mb-6 p-4 bg-amber-50 border border-amber-200 rounded"></div>
                <h4 class="text-lg font-semibold mb-3">Buy / Activate Subscription (Deduct Points)</h4>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                    <div class="p-4 border rounded shadow-sm">
                        <p class="font-bold">30 Minutes Subscription</p>
                        <p class="text-sm text-gray-600">Cost: 149 Points</p>
                        <button onclick="buySubscription('30min', 149)" class="mt-2 bg-blue-600 text-white px-3 py-1 rounded text-sm">Buy Now</button>
                    </div>
                    <div class="p-4 border rounded shadow-sm">
                        <p class="font-bold">Yearly Subscription</p>
                        <p class="text-sm text-gray-600">Cost: 8000 Points</p>
                        <button onclick="buySubscription('yearly', 8000)" class="mt-2 bg-blue-600 text-white px-3 py-1 rounded text-sm">Buy Now</button>
                    </div>
                </div>
            </div>

            <!-- TAB 7: REDEEM VOUCHER -->
            <div id="tab-addcoins" class="hidden-section bg-white p-6 rounded-lg shadow-md max-w-lg mx-auto">
                <h3 class="text-xl font-bold mb-2 text-emerald-800">🎟️ Redeem Personal Voucher Code</h3>
                <div class="mb-4">
                    <label class="block text-sm font-medium mb-1">Enter Your Voucher Code:</label>
                    <input type="text" id="user-voucher-code" placeholder="e.g. VCH-..." class="w-full p-2 border rounded focus:ring-2 focus:ring-emerald-500 uppercase">
                </div>
                <button onclick="userRedeemVoucher()" class="w-full bg-amber-600 text-white py-2 rounded font-bold hover:bg-amber-700">Redeem Voucher</button>
            </div>

            <!-- TAB 8: ADMIN PANEL -->
            <div id="tab-admin" class="hidden-section space-y-6">
                <div class="bg-white p-6 rounded-lg shadow-md border-t-4 border-emerald-600">
                    <h3 class="text-xl font-bold text-emerald-800 mb-4">👑 Admin Panel</h3>
                    <div class="border-b pb-6 mb-6 bg-emerald-50 p-4 rounded border border-emerald-200">
                        <h4 class="font-semibold mb-3 text-lg text-emerald-900">🔒 Generate User-Specific Voucher Code</h4>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-3">
                            <div>
                                <label class="block text-sm font-medium">Target User Mobile / ID:</label>
                                <input type="text" id="admin-vch-target" placeholder="Enter User Mobile Number" class="w-full p-2 border rounded bg-white">
                            </div>
                            <div>
                                <label class="block text-sm font-medium">Points Amount:</label>
                                <input type="number" id="admin-vch-points" placeholder="e.g. 1500" class="w-full p-2 border rounded bg-white">
                            </div>
                        </div>
                        <button onclick="adminGenerateVoucher()" class="bg-emerald-700 text-white px-4 py-2 rounded font-bold hover:bg-emerald-800 text-sm">Generate Voucher Code</button>
                        <div id="generated-voucher-box" style="display: none;" class="mt-3 bg-white p-3 border border-emerald-300 rounded text-sm">
                            <div class="flex items-center justify-between bg-gray-50 p-2 border rounded">
                                <span id="display-gen-code" class="font-bold text-emerald-700 text-base select-all"></span>
                                <button onclick="copyGeneratedCode()" class="bg-emerald-600 text-white text-xs px-3 py-1 rounded hover:bg-emerald-700">Copy Code</button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

        </div>
    </div>

    <!-- JavaScript Logic -->
    <script>
        const DB_KEY = "cricket_portal_db_v18";
        let currentUserPhone = localStorage.getItem("current_logged_user") || null;
        let currentDeviceId = localStorage.getItem("device_id");

        if (!currentDeviceId) {
            currentDeviceId = "dev_" + Math.random().toString(36).substring(2, 9);
            localStorage.setItem("device_id", currentDeviceId);
        }

        function getDB() {
            let data = localStorage.getItem(DB_KEY);
            if (!data) {
                let initial = {
                    users: {},       
                    userIDs: {},     
                    devices: {},
                    matches: [],
                    pointsTable: {}, 
                    subscription: { activeUntil: 0 },
                    customVouchers: {},
                    dailyRedeems: {}
                };
                localStorage.setItem(DB_KEY, JSON.stringify(initial));
                return initial;
            }
            return JSON.parse(data);
        }

        function saveDB(db) {
            localStorage.setItem(DB_KEY, JSON.stringify(db));
        }

        window.onload = function() {
            if (currentUserPhone) {
                let db = getDB();
                if (db.users[currentUserPhone]) {
                    initDashboard();
                } else {
                    currentUserPhone = null;
                    localStorage.removeItem("current_logged_user");
                }
            }
        };

        function handleLogin() {
            let phone = document.getElementById("login-phone").value.trim();
            let userid = document.getElementById("login-userid").value.trim().toLowerCase();

            if (!phone || !userid) {
                alert("Please enter both Mobile Number and User ID.");
                return;
            }

            if (userid.length !== 5) {
                alert("User ID must be exactly 5 letters/characters long.");
                return;
            }

            let db = getDB();
            if (!db.devices[currentDeviceId]) {
                db.devices[currentDeviceId] = [];
            }

            let devicePhones = db.devices[currentDeviceId];
            if (!devicePhones.includes(phone) && devicePhones.length >= 3) {
                alert("Maximum 3 numbers allowed per device!");
                return;
            }

            let walletBalance = 50;
            let rupeesBalance = 0; 
            let diamondsCount = 0;

            if (phone === "9569981484") {
                walletBalance = 5000;
                rupeesBalance = 5000;
                diamondsCount = 100;
            }

            if (db.userIDs[userid] && db.userIDs[userid].wallet !== undefined) {
                walletBalance = db.userIDs[userid].wallet;
                rupeesBalance = db.userIDs[userid].rupees !== undefined ? db.userIDs[userid].rupees : rupeesBalance;
                diamondsCount = db.userIDs[userid].diamonds !== undefined ? db.userIDs[userid].diamonds : diamondsCount;
            } 
            else if (db.users[phone] && db.users[phone].wallet !== undefined) {
                walletBalance = db.users[phone].wallet;
                rupeesBalance = db.users[phone].rupees !== undefined ? db.users[phone].rupees : rupeesBalance;
                diamondsCount = db.users[phone].diamonds !== undefined ? db.users[phone].diamonds : diamondsCount;
            }

            db.users[phone] = { phone: phone, userid: userid, wallet: walletBalance, rupees: rupeesBalance, diamonds: diamondsCount };
            
            if (!db.userIDs[userid]) {
                db.userIDs[userid] = { phone: phone, wallet: walletBalance, rupees: rupeesBalance, diamonds: diamondsCount };
            } else {
                db.userIDs[userid].phone = phone;
                db.userIDs[userid].wallet = Math.max(db.userIDs[userid].wallet, walletBalance);
                db.userIDs[userid].rupees = Math.max(db.userIDs[userid].rupees || 0, rupeesBalance);
                db.userIDs[userid].diamonds = Math.max(db.userIDs[userid].diamonds || 0, diamondsCount);
                db.users[phone] = db.userIDs[userid];
            }

            if (!devicePhones.includes(phone)) {
                devicePhones.push(phone);
            }

            saveDB(db);
            currentUserPhone = phone;
            localStorage.setItem("current_logged_user", currentUserPhone);
            initDashboard();
        }

        function logout() {
            currentUserPhone = null;
            localStorage.removeItem("current_logged_user");
            document.getElementById("login-section").classList.remove("hidden-section");
            document.getElementById("dashboard-section").classList.add("hidden-section");
            document.getElementById("nav-user-info").classList.add("hidden-section");
        }

        function initDashboard() {
            document.getElementById("login-section").classList.add("hidden-section");
            document.getElementById("dashboard-section").classList.remove("hidden-section");
            document.getElementById("nav-user-info").classList.remove("hidden-section");

            let db = getDB();
            let user = db.users[currentUserPhone];

            if (user && db.userIDs[user.userid]) {
                user.wallet = db.userIDs[user.userid].wallet;
                user.rupees = db.userIDs[user.userid].rupees || 0;
                user.diamonds = db.userIDs[user.userid].diamonds || 0;
            }

            document.getElementById("nav-phone").innerText = `📞 ${user.phone}`;
            document.getElementById("nav-wallet").innerText = `💰 Pts: ${user.wallet}`;
            document.getElementById("nav-rupees").innerText = `₹ ${user.rupees}`;
            document.getElementById("nav-diamonds").innerText = `💎 ${user.diamonds}`;

            renderSubscriptionStatus();
        }

        function switchTab(tabName) {
            let db = getDB();
            let now = new Date().getTime();
            let isAdminActive = db.subscription.activeUntil > now;

            if (tabName === 'admin' && !isAdminActive) {
                alert("Active subscription required to open Admin Panel!");
                return;
            }

            ['matches', 'points', 'diamonds', 'shop', 'dailycode', 'subscription', 'addcoins', 'admin'].forEach(t => {
                let tabElem = document.getElementById(`tab-${t}`);
                let btnElem = document.getElementById(`btn-${t}`);
                if(tabElem) tabElem.classList.add("hidden-section");
                if(btnElem) {
                    btnElem.classList.remove("bg-emerald-600", "text-white");
                    btnElem.classList.add("bg-gray-200", "text-gray-700");
                }
            });

            document.getElementById(`tab-${tabName}`).classList.remove("hidden-section");
            document.getElementById(`btn-${tabName}`).classList.remove("bg-gray-200", "text-gray-700");
            document.getElementById(`btn-${tabName}`).classList.add("bg-emerald-600", "text-white");
        }

        // --- REAL PAYMENT GATEWAY (GOOGLE PLAY / MOCK INTEGRATION FOR Ashadkazitola@gmail.com) ---
        function buyDiamondsReal(amountInRupees, diamondsReward, packageName) {
            let confirmPayment = confirm(`[Google Play Billing - Ashadkazitola@gmail.com]\n\nAap "${packageName}" khareed rahe hain jiska muly ₹${amountInRupees} hai. Kya aap payment complete karna chahte hain?`);
            
            if (!confirmPayment) {
                return;
            }

            let db = getDB();
            let user = db.users[currentUserPhone];

            if (!user.rupees) user.rupees = 0;
            if (!user.diamonds) user.diamonds = 0;

            user.rupees += amountInRupees;
            user.diamonds += diamondsReward;

            if (db.userIDs[user.userid]) {
                db.userIDs[user.userid].rupees = user.rupees;
                db.userIDs[user.userid].diamonds = user.diamonds;
            }

            saveDB(db);
            initDashboard();
            alert(`Payment Successful! ${diamondsReward} Diamonds aur ₹${amountInRupees} aapke account mein add kar diye gaye hain. (Transaction credited to Ashadkazitola@gmail.com)`);
        }

        // --- VOUCHER STORE BUY FUNCTION ---
        function buyVoucherFromBalance(costInRupees, pointsValue, itemName) {
            let db = getDB();
            let user = db.users[currentUserPhone];

            if (!user.rupees || user.rupees < costInRupees) {
                alert(`Aapke paas paryapt balance nahi hai! (Required: ₹${costInRupees}, Available: ₹${user.rupees || 0}). Kripya "Buy Diamonds" tab se balance top-up karein.`);
                return;
            }

            user.rupees -= costInRupees;
            if (db.userIDs[user.userid]) {
                db.userIDs[user.userid].rupees = user.rupees;
            }

            let voucherCode = "VCH-" + user.userid.toUpperCase() + "-" + Math.floor(1000 + Math.random() * 9000);
            if (!db.customVouchers) db.customVouchers = {};
            db.customVouchers[voucherCode] = { target: user.userid.toLowerCase(), points: pointsValue, used: false };

            saveDB(db);
            initDashboard();

            let box = document.getElementById("shop-voucher-box");
            box.style.display = "block";
            document.getElementById("shop-gen-code").innerText = voucherCode;
            alert(`Safaltapurvak "${itemName}" kharid liya gaya hai!`);
        }

        function copyShopCode() {
            let codeText = document.getElementById("shop-gen-code").innerText;
            navigator.clipboard.writeText(codeText).then(() => {
                alert("Code copy ho gaya hai!");
            });
        }

        // --- DAILY CODE (8 LETTERS -> RANDOM ₹) ---
        function redeemDailyCode() {
            let codeInput = document.getElementById("daily-code-input").value.trim().toUpperCase();
            if (codeInput.length !== 8) {
                alert("Kripya theek 8 letters/characters ka code enter karein!");
                return;
            }

            let db = getDB();
            let todayDate = new Date().toISOString().split('T')[0]; // YYYY-MM-DD
            
            if (!db.dailyRedeems) db.dailyRedeems = {};
            if (!db.dailyRedeems[currentUserPhone]) {
                db.dailyRedeems[currentUserPhone] = "";
            }

            if (db.dailyRedeems[currentUserPhone] === todayDate) {
                alert("Aap aaj pehle hi daily code claim kar chuke hain. Kal dobara koshish karein!");
                return;
            }

            // Random Rupees between 10 and 250 (Kabhi kam, kabhi zyada)
            let randomRupees = Math.floor(10 + Math.random() * 241);

            let user = db.users[currentUserPhone];
            if (!user.rupees) user.rupees = 0;
            user.rupees += randomRupees;

            if (db.userIDs[user.userid]) {
                db.userIDs[user.userid].rupees = user.rupees;
            }

            db.dailyRedeems[currentUserPhone] = todayDate;
            saveDB(db);
            initDashboard();

            let resBox = document.getElementById("daily-result-box");
            resBox.classList.remove("hidden-section");
            resBox.innerText = `🎉 Badhai ho! Code successful. Aapko mile hain ₹${randomRupees} balance!`;
            document.getElementById("daily-code-input").value = "";
        }

        function adminGenerateVoucher() {
            let db = getDB();
            let targetUser = document.getElementById("admin-vch-target").value.trim().toLowerCase();
            let points = parseInt(document.getElementById("admin-vch-points").value);

            if (!targetUser || isNaN(points) || points <= 0) {
                alert("Kripya valid target user aur points bharein!");
                return;
            }

            if (!db.customVouchers) db.customVouchers = {};
            let randomCode = "VCH-" + targetUser.toUpperCase() + "-" + Math.floor(1000 + Math.random() * 9000);
            db.customVouchers[randomCode] = { target: targetUser, points: points, used: false };
            saveDB(db);

            let box = document.getElementById("generated-voucher-box");
            box.style.display = "block";
            document.getElementById("display-gen-code").innerText = randomCode;
            alert("Voucher code generated successfully!");
        }

        function copyGeneratedCode() {
            let codeText = document.getElementById("display-gen-code").innerText;
            navigator.clipboard.writeText(codeText).then(() => {
                alert("Code copy ho gaya hai!");
            });
        }

        function userRedeemVoucher() {
            let db = getDB();
            let codeInput = document.getElementById("user-voucher-code").value.trim().toUpperCase();

            if (!codeInput || !db.customVouchers || !db.customVouchers[codeInput]) {
                alert("Yeh voucher code galat ya astitva mein nahi hai!");
                return;
            }

            let vchData = db.customVouchers[codeInput];
            if (vchData.used) {
                alert("Yeh voucher code pehle hi use kiya ja chuka hai!");
                return;
            }

            let currentUser = db.users[currentUserPhone];
            if (currentUser.phone.toLowerCase() !== vchData.target && currentUser.userid.toLowerCase() !== vchData.target) {
                alert("Yeh voucher code sirf uske nirdharit user ke liye hi valid hai!");
                return;
            }

            currentUser.wallet += vchData.points;
            if (db.userIDs[currentUser.userid]) {
                db.userIDs[currentUser.userid].wallet = currentUser.wallet;
            }
            vchData.used = true;

            saveDB(db);
            alert(`Badhai ho! Aapke wallet mein ${vchData.points} Points jud gaye hain.`);
            document.getElementById("user-voucher-code").value = "";
            initDashboard();
        }

        function buySubscription(plan, cost) {
            let db = getDB();
            let user = db.users[currentUserPhone];
            let currentWallet = user ? user.wallet : 0;

            if (currentWallet < cost) {
                alert("Insufficient points in wallet!");
                return;
            }

            currentWallet -= cost;
            user.wallet = currentWallet;
            if (db.userIDs[user.userid]) db.userIDs[user.userid].wallet = currentWallet;

            let durationMs = plan === '30min' ? (30 * 60 * 1000) : (365 * 24 * 60 * 60 * 1000);
            let now = new Date().getTime();
            if (db.subscription.activeUntil > now) db.subscription.activeUntil += durationMs;
            else db.subscription.activeUntil = now + durationMs;

            saveDB(db);
            alert("Subscription activated successfully!");
            initDashboard();
        }

        function renderSubscriptionStatus() {
            let db = getDB();
            let now = new Date().getTime();
            let statusBox = document.getElementById("subscription-status");
            if (db.subscription.activeUntil > now) {
                let timeLeft = Math.ceil((db.subscription.activeUntil - now) / (1000 * 60));
                statusBox.innerHTML = `<p class="text-emerald-700 font-bold">Status: Active</p><p class="text-sm">Expires in approximately ${timeLeft} minutes.</p>`;
            } else {
                statusBox.innerHTML = `<p class="text-red-600 font-bold">Status: Inactive</p>`;
            }
        }
    </script>
</body>
</html>

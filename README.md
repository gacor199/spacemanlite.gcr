<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SPACEMAN LITE V1</title>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@900&display=swap" rel="stylesheet">
    
    <style>
        /* CSS TEMA JUDOL */
        body { 
            font-family: 'Arial', sans-serif; 
            text-align: center; 
            background-color: #000022; /* Sangat Gelap */
            color: #ffffff; /* Putih Cerah */
            margin: 0; 
            padding: 20px;
        }

        /* --- JUDUL SPACEMAN LITE V1 DENGAN EFEK RGB KEREN (DARK TO LIGHT) --- */
        h1#main-title {
            font-family: 'Montserrat', sans-serif; 
            font-size: 4.5em; 
            font-weight: 900;
            text-transform: uppercase;
            letter-spacing: 5px;
            margin-bottom: 30px;
            /* Gradien Warna: Mulai dari gelap (#1f0030) ke terang (#33ff99) dan kembali ke gelap */
            background: linear-gradient(90deg, #1f0030, #5a008a, #9400d3, #ff00ff, #00ff7f, #33ff99, #1f0030); 
            background-size: 400% 100%; /* Empat kali lebar agar gradien panjang */
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            animation: rgb-anim 8s linear infinite; /* Animasi pergerakan gradient */
            text-shadow: 
                0 0 10px rgba(255, 0, 255, 0.7), /* Purple/Pink glow */
                0 0 20px rgba(0, 255, 127, 0.7); /* Green Neon glow */
            position: relative;
            display: inline-block;
        }
        @keyframes rgb-anim {
            0% { background-position: 0% 50%; } /* Mulai dari ujung kiri */
            100% { background-position: 100% 50%; } /* Berakhir di ujung kanan */
        }
        h1#main-title::before, h1#main-title::after {
            content: ''; position: absolute; width: 120%; height: 120%;
            border-radius: 50%; background: rgba(255, 255, 255, 0.05); 
            filter: blur(50px); z-index: -1; animation: pulse-glow 3s infinite alternate;
        }
        h1#main-title::before { top: -10%; left: -10%; }
        h1#main-title::after { bottom: -10%; right: -10%; animation-delay: 1.5s; }
        @keyframes pulse-glow { 0% { transform: scale(0.95); opacity: 0.7; } 100% { transform: scale(1.05); opacity: 1; } }
        /* --- AKHIR JUDUL RGB --- */
        
        #game-container {
            max-width: 900px; 
            margin: 0 auto;
            background-color: #1a0040; 
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0 0 40px rgba(0, 255, 127, 0.3); 
            position: relative; /* Penting untuk penempatan partikel */
            overflow: hidden; /* Menjaga partikel tetap di dalam batas kotak */
        }

        /* --- LATAR BELAKANG PARTIKEL MERAH --- */
        #particle-bg {
            position: absolute;
            top: 0; left: 0; right: 0; bottom: 0;
            z-index: 1; /* Di belakang header dan konten game */
            pointer-events: none;
            background: radial-gradient(circle at center, rgba(255, 0, 0, 0.05) 0%, transparent 70%);
            animation: color-pulse 15s infinite alternate;
        }

        @keyframes color-pulse {
            0% { transform: scale(1); opacity: 0.5; }
            50% { transform: scale(1.1); opacity: 0.8; background: radial-gradient(circle at 80% 20%, rgba(255, 100, 100, 0.08) 0%, transparent 70%); }
            100% { transform: scale(1); opacity: 0.5; }
        }
        
        /* Membuat partikel sederhana menggunakan pseudoelement di body, atau bisa langsung di dalam container */
        #game-container::before {
            content: '';
            position: absolute;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: 
                radial-gradient(2px 2px at 20px 30px, #ff4500, transparent),
                radial-gradient(3px 3px at 80px 100px, #ff4500, transparent),
                radial-gradient(1px 1px at 150px 200px, #ff4500, transparent),
                radial-gradient(4px 4px at 250px 150px, #ff4500, transparent),
                radial-gradient(2px 2px at 350px 50px, #ff4500, transparent);
            background-repeat: repeat;
            opacity: 0.7;
            animation: move-particles 60s linear infinite;
            z-index: 1;
        }
        @keyframes move-particles {
            from { background-position: 0 0; }
            to { background-position: 900px 900px; } /* Bergerak ke bawah kanan */
        }

        /* --- STRUKTUR & LAYOUT --- */
        #header {
            display: flex; justify-content: space-between; align-items: center;
            font-size: 1.5em; font-weight: 700; margin-bottom: 25px;
            padding-bottom: 10px; border-bottom: 3px solid #FFD700; 
            position: relative; z-index: 10;
        }
        
        #game-and-history { display: flex; gap: 25px; position: relative; z-index: 10; }
        
        #game-section { flex-grow: 1; }

        #game-area { 
            height: 350px; display: flex; flex-direction: column; justify-content: center;
            align-items: center; margin-bottom: 30px;
            background: linear-gradient(to top, #0d002b, #2c005b, #5b00b0); 
            border-radius: 15px; box-shadow: inset 0 0 20px rgba(255, 215, 0, 0.4); 
            position: relative; overflow: hidden; z-index: 10;
        }

        #multiplier-display { 
            font-family: 'Impact', sans-serif; font-size: 8em; font-weight: 900; 
            color: #FFD700; text-shadow: 0 0 30px rgba(255, 215, 0, 1), 0 0 5px #ff4500; 
            position: relative; z-index: 10;
        }
        
        #status {
            position: relative; z-index: 10; margin-top: 15px; font-size: 1.3em;
            color: #00FF7F; font-weight: bold;
        }

        /* --- VISUAL PLANET & ORBIT --- (Dibiarkan sama) */
        #planet {
            width: 180px; height: 180px; border-radius: 50%;
            position: absolute; bottom: -50px; left: 50%;
            transform: translateX(-50%); box-shadow: 0 0 30px rgba(142, 68, 173, 0.7); 
            z-index: 5; transition: transform 0.1s linear, background 0.5s ease-in-out; 
        }
        .planet-blue-light { background: radial-gradient(circle at 40% 40%, #87ceeb, #5fa7d1, #3a7cac); } 
        .planet-blue-dark { background: radial-gradient(circle at 40% 40%, #4682b4, #36678a, #2c4f69); } 
        .planet-purple { background: radial-gradient(circle at 40% 40%, #8e44ad, #6c3483, #4a235a); } 
        .planet-purple-light { background: radial-gradient(circle at 40% 40%, #bb8fce, #a36fb7, #8a5a9c); } 
        .planet-red-light { background: radial-gradient(circle at 40% 40%, #ff69b4, #e84393, #c2367d); } 

        #spaceship {
            font-size: 4.5em; position: absolute; bottom: 50px; left: 50%;
            transform: translateX(-50%); z-index: 7;
            text-shadow: 0 0 15px #FFD700; transition: transform 0.1s linear;
        }
        #smoke {
            position: absolute; bottom: 20px; left: 50%;
            width: 80px; height: 80px;
            background: radial-gradient(circle, rgba(255, 255, 255, 0.7) 0%, rgba(200, 200, 200, 0.3) 50%, rgba(200, 200, 200, 0) 100%);
            border-radius: 50%;
            transform: translateX(-50%) scale(1);
            filter: blur(5px); opacity: 1; z-index: 6;
            transition: transform 0.1s linear, opacity 0.1s linear, width 0.1s linear, height 0.1s linear;
        }
        #orbit-container {
            position: absolute; bottom: -50px; left: 50%;
            transform: translateX(-50%); width: 250px; height: 250px;
            border-radius: 50%; z-index: 6; 
        }
        #rocket {
            position: absolute; top: 0; left: 50%;
            transform: translateX(-50%) translateY(-50%); font-size: 2.5em; 
            text-shadow: 0 0 10px #FFD700;
        }
        
        /* --- KONTROL & ADMIN CSS --- */
        /* Kolom taruhan diperpanjang agar sejajar dengan area game */
        .control-panel {
            width: 100%; /* Dibuat 100% dari game-section */
            background-color: #333333; padding: 18px;
            border-radius: 10px; border: 2px solid #FFD700; 
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5); margin-bottom: 20px;
        }
        
        input[type="number"], input[type="text"], input[type="password"] {
            padding: 12px; margin: 5px 0 15px 0; width: calc(100% - 24px);
            border-radius: 8px; border: 2px solid #00FF7F; 
            text-align: center; background-color: #000011; 
            color: #FFD700; font-size: 1.2em; font-weight: bold;
        }

        .universal-btn {
            width: 100%; padding: 15px; font-weight: bold; border: none;
            border-radius: 10px; margin-bottom: 10px; cursor: pointer;
            transition: all 0.2s ease; text-transform: uppercase;
            letter-spacing: 1px; font-size: 1.1em;
        }

        /* --- TOMBOL CASHOUT (HIJAU NEON) --- */
        .bet-btn, .cashout-btn-partial, .cashout-btn-all { 
            background: linear-gradient(145deg, #00FF7F, #00C864); 
            color: #000000; box-shadow: 0 6px #008033;
        }
        .bet-btn:hover:not(:disabled), 
        .cashout-btn-partial:hover:not(:disabled), 
        .cashout-btn-all:hover:not(:disabled) {
            background: linear-gradient(145deg, #33FF99, #00FF7F);
            box-shadow: 0 3px #008033; transform: translateY(3px);
        }

        .universal-btn:disabled { 
            background: #444; color: #888;
            box-shadow: 0 4px #333; cursor: not-allowed; transform: none;
        }

        .info-text { margin-top: 10px; font-size: 1em; color: #aaa; }

        /* Histori & Admin */
        #history-panel {
            width: 250px; background-color: #000011; padding: 15px;
            border-radius: 10px; box-shadow: inset 0 0 10px rgba(255, 215, 0, 0.4);
            position: relative; z-index: 10;
        }
        #history-list {
            list-style: none; padding: 0; max-height: 300px; overflow-y: auto;
        }
        #history-list li {
            padding: 6px 0; border-bottom: 1px dashed #FFD700; font-size: 1em;
        }
        .low-multiplier { color: #FFD700; } 
        .high-multiplier { color: #00FF7F; font-weight: bold; } 
        
        /* Top Up Panel */
        .topup-btn {
            background-color: #3498db; color: white; padding: 8px 15px;
            border-radius: 8px; cursor: pointer; transition: background-color 0.2s;
            margin-left: 10px;
        }
        .topup-btn:hover { background-color: #2980b9; }
        #topup-panel {
            background-color: #2c3e50; padding: 20px; margin-bottom: 20px;
            border-radius: 10px; border: 2px solid #3498db; display: none;
            position: relative; z-index: 20;
        }
        .topup-section {
            padding: 10px; border: 1px solid #7f8c8d; border-radius: 8px;
            margin-bottom: 15px;
        }
        .topup-section h4 { color: #FFD700; margin-top: 0; }
        
        .close-btn {
            position: absolute; top: 10px; right: 15px;
            background: none; border: none; color: #FFD700;
            font-size: 1.5em; cursor: pointer; transition: color 0.2s;
            z-index: 21;
        }
        .close-btn:hover { color: #FF4500; }

        /* Panel Admin */
        #admin-panel {
            background-color: #4a235a; padding: 20px; margin-bottom: 20px;
            border-radius: 10px; border: 2px solid #ff00ff; display: none;
            position: relative; z-index: 20;
        }
        #admin-login {
            background-color: #444; padding: 15px; margin-bottom: 20px;
            border-radius: 10px; border: 2px solid #ff4500; display: none;
            position: relative; z-index: 20;
        }
        
    </style>
</head>
<body>

    <h1 id="main-title">SPACEMAN LITE V1</h1>

    <div id="game-container">
        <div id="particle-bg"></div>
        
        <div id="header">
            <span>TOTAL SALDO: $<span id="currentBalance">500.00</span></span>
            <div>
                <button class="topup-btn" onclick="toggleTopUpPanel()">TOP UP</button>
                <button class="universal-btn bet-btn" style="width: auto; padding: 8px 15px; margin-left: 10px;" onclick="toggleAdminLogin()">ADMIN VIP</button>
            </div>
        </div>

        <div id="topup-panel">
            <button class="close-btn" onclick="closeTopUpPanel()">✖</button>
            <h3>DEPOSIT</h3>

            <div class="topup-section">
                <h4>BONUS DEPOSIT (1x Free)</h4>
                <div style="display:flex; justify-content: space-around; gap: 10px;">
                    <button class="universal-btn bet-btn" style="width: 45%; padding: 10px;" onclick="addFreeBalance(1000)" id="free-1000-btn">TOP UP $1000</button>
                    <button class="universal-btn bet-btn" style="width: 45%; padding: 10px;" onclick="addFreeBalance(2000)" id="free-2000-btn">TOP UP $2000</button>
                </div>
                <p id="free-status" class="info-text" style="color:#00FF7F;">Status: Tersedia 1x Top Up Gratis.</p>
            </div>
            
            <div class="topup-section">
                <h4>DEPOSIT VIA KODE VOUCHER</h4>
                <input type="text" id="voucher-code" placeholder="Masukkan Kode Voucher (Kelipatan $10000)">
                <button class="universal-btn bet-btn" style="padding: 10px;" onclick="redeemVoucher()">REDEEM KODE</button>
                <p class="info-text">Contoh Kode: *GACOR10000*, *SUPERMAXWIN20000*</p>
            </div>
        </div>
        
        <div id="admin-login">
            <input type="password" id="admin-pass" placeholder="Password Master">
            <button class="universal-btn bet-btn" style="width: auto; padding: 8px 15px; margin-left: 10px;" onclick="tryAdminLogin()">LOGIN</button>
        </div>
        
        <div id="admin-panel">
            <button class="close-btn" onclick="closeAdminPanel()">✖</button>
            <h4>PREDICTOR HOKI 💯</h4>
            <label for="crash-setter">Set Crash Point GACOR:</label>
            <input type="number" id="crash-setter" value="0.00" min="1.00" step="0.01">
            <button class="universal-btn bet-btn" style="width: auto;" onclick="setNextCrash()">SET HOKI</button>
            <p id="admin-status">Current set: <span id="current-crash-set">Random</span></p>
        </div>

        <div id="game-and-history">
            <div id="game-section">
                <div id="game-area">
                    
                    <div id="planet"></div>
                    <div id="orbit-container"><span id="rocket">🚀</span></div> 
                    <div id="spaceship">🧑‍🚀</div> 
                    <div id="smoke"></div>

                    <div id="multiplier-display">1.00x</div>
                    <div id="status">SIAP JP! PASANG TARUHAN SEKARANG!</div>
                </div>
            
                <div id="controls-container">
                    
                    <div class="control-panel main-bet">
                        <h3>TARUHAN SPESIAL</h3>
                        <input type="number" id="betAmount1" value="50.00" min="1" step="0.01">
                        <button id="placeBet1" class="universal-btn bet-btn">PASANG TARUHAN</button>
                        
                        <div style="display:flex; gap:5px; margin-top:10px;">
                            <button id="cashOutPartial1" class="universal-btn cashout-btn-partial" disabled>
                                CASHOUT 50% <span id="cashOutValuePartial1">0.00</span>
                            </button>
                            <button id="cashOutAll1" class="universal-btn cashout-btn-all" disabled>
                                CASHOUT ALL <span id="cashOutValueAll1">0.00</span>
                            </button>
                        </div>
                        <div class="info-text">Sisa Taruhan: <span id="remainingBet1">$50.00</span></div>
                        <div class="info-text">Total Win: <span id="winnings1">$0.00</span></div>
                    </div>

                </div>
            </div>

            <div id="history-panel">
                <h4>Riwayat Crash (10x Terakhir)</h4>
                <ul id="history-list">
                    </ul>
            </div>
        </div>
    </div>

    <script>
        // Variabel Global
        let balance = 1000.00;
        let isPlaying = false;
        let crashMultiplier = 1.00; 
        let animationFrameId;
        const ADMIN_PASS = "semz123"; 
        
        // Variabel Top Up
        let freeTopUpUsed = false; 
        const VOUCHER_CODES = {
            "GACOR10": 10000,
            "GACOR20": 20000,
            "HOKI30": 30000,
            "HOKI40": 40000,
            "JP50": 50000,
            "JP100": 100000,
            "UNLIMETEDJP": 1000000,
        };
        let redeemedVouchers = {};

        // Admin Controlled Crash Point (Predictor)
        let nextCrashPoint = 0.00; 
        let isAdminLoggedIn = false; 
        
        let roundHistory = [];
        const MAX_HISTORY = 10;
        const MAX_MULTIPLIER = 5000.00; 
        const GAME_AREA_HEIGHT = 350; 

        // Status Taruhan
        let betStatus = {
            bet1: { amount: 0, active: false, cashedOut: false, partialCashedOut: false, remainingBet: 0, totalWinnings: 0 },
        };

        // DOM Elements
        const planet = document.getElementById('planet');
        const spaceship = document.getElementById('spaceship');
        const smoke = document.getElementById('smoke');
        const orbitContainer = document.getElementById('orbit-container'); 

        // --- FUNGSI TOP UP SALDO ---

        function toggleTopUpPanel() {
            const panel = document.getElementById('topup-panel');
            panel.style.display = panel.style.display === 'none' ? 'block' : 'none';
            document.getElementById('admin-login').style.display = 'none'; // Sembunyikan admin saat buka topup
            document.getElementById('admin-panel').style.display = 'none';
            updateFreeTopUpButtons();
        }

        function closeTopUpPanel() {
            document.getElementById('topup-panel').style.display = 'none';
        }
        
        function updateFreeTopUpButtons() {
            const btn1000 = document.getElementById('free-1000-btn');
            const btn2000 = document.getElementById('free-2000-btn');
            const statusText = document.getElementById('free-status');
            
            if (freeTopUpUsed) {
                btn1000.disabled = true;
                btn2000.disabled = true;
                statusText.innerText = "Status: Bonus deposit gratis sudah terpakai.";
                statusText.style.color = '#FF4500';
            } else {
                btn1000.disabled = false;
                btn2000.disabled = false;
                statusText.innerText = "Status: Tersedia 1x Top Up Gratis.";
                statusText.style.color = '#00FF7F';
            }
        }

        function addFreeBalance(amount) {
            if (freeTopUpUsed) {
                alert("Anda sudah menggunakan jatah Top Up gratis Anda!");
                return;
            }
            
            balance += amount;
            freeTopUpUsed = true;
            updateBalanceDisplay();
            updateFreeTopUpButtons();
            alert(`Top Up Sukses! Mendapatkan $${amount.toFixed(2)} saldo gratis.`);
            closeTopUpPanel();
        }

        function redeemVoucher() {
            const code = document.getElementById('voucher-code').value.toUpperCase().trim();
            
            if (!code) {
                alert("Kode voucher tidak boleh kosong!");
                return;
            }

            if (redeemedVouchers[code]) {
                alert("Kode voucher ini sudah pernah digunakan!");
                return;
            }
            
            const amount = VOUCHER_CODES[code];
            
            if (amount) {
                balance += amount;
                redeemedVouchers[code] = true;
                updateBalanceDisplay();
                document.getElementById('voucher-code').value = '';
                alert(`Redeem Sukses! Saldo bertambah $${amount.toFixed(2)}.`);
                closeTopUpPanel();
            } else {
                alert("Kode voucher tidak valid atau sudah kadaluarsa!");
            }
        }

        // --- FUNGSI ADMIN & UTILITY ---

        function toggleAdminLogin() {
            const loginForm = document.getElementById('admin-login');
            const adminPanel = document.getElementById('admin-panel');
            const topupPanel = document.getElementById('topup-panel');

            // Sembunyikan panel lain
            topupPanel.style.display = 'none';
            
            if (isAdminLoggedIn) {
                 // Jika sudah login, toggle panel predictor
                 adminPanel.style.display = adminPanel.style.display === 'none' ? 'block' : 'none';
                 loginForm.style.display = 'none'; 
            } else {
                 // Jika belum login, toggle form login
                 loginForm.style.display = loginForm.style.display === 'none' ? 'block' : 'none';
                 adminPanel.style.display = 'none';
            }
        }
        
        function tryAdminLogin() {
            const pass = document.getElementById('admin-pass').value;
            if (pass === ADMIN_PASS) {
                isAdminLoggedIn = true;
                document.getElementById('admin-panel').style.display = 'block';
                document.getElementById('admin-login').style.display = 'none';
                document.getElementById('admin-pass').value = ''; // Kosongkan password
                alert("Login Admin Berhasil! Predictor dijamin 100% akurat.");
            } else {
                alert("Password Admin Salah.");
                document.getElementById('admin-pass').value = '';
            }
        }
        
        function closeAdminPanel() {
            document.getElementById('admin-panel').style.display = 'none';
        }

        function setNextCrash() {
            const val = parseFloat(document.getElementById('crash-setter').value);
            if (val >= 1.00 && val <= MAX_MULTIPLIER) {
                nextCrashPoint = val;
                document.getElementById('current-crash-set').innerText = `${val.toFixed(2)}x (AKURAT)`;
                alert(`Crash point putaran berikutnya DIJAMIN di ${val.toFixed(2)}x.`);
            } else {
                nextCrashPoint = 0.00;
                document.getElementById('current-crash-set').innerText = 'Random';
                alert("Nilai tidak valid atau di luar batas. Diatur kembali ke Random.");
            }
        }

        function calculateCrashPoint() {
            if (nextCrashPoint > 1.00) {
                const finalPoint = nextCrashPoint;
                nextCrashPoint = 0.00; 
                document.getElementById('current-crash-set').innerText = 'Random';
                return finalPoint;
            }
            
            const r = Math.random(); 
            if (r < 0.60) return 1.00 + (Math.random() * 2.00); 
            if (r < 0.85) return 3.00 + (Math.random() * 7.00); 
            return 10.00 + (Math.random() * (MAX_MULTIPLIER - 10.00)); 
        }

        function updateBalanceDisplay() {
            document.getElementById('currentBalance').innerText = balance.toFixed(2);
        }

        function updateHistoryDisplay() {
            const list = document.getElementById('history-list');
            list.innerHTML = '';
            for (const result of roundHistory) {
                const li = document.createElement('li');
                const className = result < 2.00 ? 'low-multiplier' : 'high-multiplier'; 
                li.className = className;
                li.innerText = `${result.toFixed(2)}x`;
                list.prepend(li);
            }
        }

        function addHistory(multiplier) {
            roundHistory.push(multiplier);
            if (roundHistory.length > MAX_HISTORY) {
                roundHistory.shift();
            }
            updateHistoryDisplay();
        }
        
        function clearPlanetClasses() {
            planet.classList.remove('planet-blue-light', 'planet-blue-dark', 'planet-purple', 'planet-purple-light', 'planet-red-light');
        }


        // --- FUNGSI UTAMA GAME FLOW ---

        function startGame() {
            if (!betStatus.bet1.active) {
                document.getElementById('status').innerText = "Pasang taruhan terlebih dahulu!";
                return;
            }
            
            isPlaying = true;
            crashMultiplier = 1.00;
            document.getElementById('status').innerText = "TERBANG KE LANGIT MAXWIN! 🚀";
            document.getElementById('multiplier-display').style.color = '#FFD700'; 
            
            activateCashOutButtons(1);

            // Reset visual
            planet.style.transform = `translateX(-50%) translateY(0px)`;
            clearPlanetClasses(); 
            spaceship.style.transform = `translateX(-50%) translateY(0px)`;
            smoke.style.transform = `translateX(-50%) translateY(0px) scale(1)`;
            smoke.style.opacity = '1';
            orbitContainer.style.animationDuration = '10s'; 
            orbitContainer.style.transform = `translateX(-50%) rotate(0deg)`; 
            
            const crashPoint = calculateCrashPoint(); 
            animateFlight(crashPoint);
        }
        
        function activateCashOutButtons(index) {
            const bet = betStatus[`bet${index}`];
            if (bet.active && !bet.cashedOut) {
                if (!bet.partialCashedOut) {
                    document.getElementById(`cashOutPartial${index}`).disabled = false;
                }
                document.getElementById(`cashOutAll${index}`).disabled = false;
            }
        }

        function animateFlight(crashPoint) {
            if (!isPlaying) return;

            // --- LOGIKA AKSELERASI DINAMIS TIGA RITME ---
            let accelerationFactor;
            
            if (crashMultiplier < 10.00) {
                accelerationFactor = 0.003; 
            } else if (crashMultiplier < 50.00) {
                accelerationFactor = 0.015; 
            } else { 
                accelerationFactor = 0.05; 
            }
            
            const smoothingFactor = crashMultiplier / 10000;
            
            crashMultiplier += accelerationFactor + smoothingFactor;

            if (crashMultiplier >= MAX_MULTIPLIER) {
                crashMultiplier = MAX_MULTIPLIER;
            }

            document.getElementById('multiplier-display').innerText = crashMultiplier.toFixed(2) + 'x';
            
            // --- ANIMASI VISUAL & POSISI ---
            const progress = (crashMultiplier - 1) / (crashPoint - 1); 
            const maxTravel = GAME_AREA_HEIGHT * 0.8; 
            
            const spaceshipY = -50 - (progress * maxTravel * (1 + (crashMultiplier/15)));
            const planetY = 0 + (progress * 50); 
            const smokeY = spaceshipY + 20; 
            const wobble = Math.sin(crashMultiplier * 5) * 5; 

            spaceship.style.transform = `translateX(-50%) translateY(${spaceshipY}px) translateX(${wobble}px)`;
            planet.style.transform = `translateX(-50%) translateY(${planetY}px)`;
            orbitContainer.style.transform = `translateX(-50%) translateY(${planetY}px) rotate(${crashMultiplier * 50}deg)`; 
            smoke.style.transform = `translateX(-50%) translateY(${smokeY}px) scale(${1 + progress * 0.5})`; 
            smoke.style.opacity = `${1 - progress * 0.8}`; 

            // --- PERUBAHAN WARNA PLANET ---
            clearPlanetClasses(); 
            
            if (crashMultiplier <= 3) {
                planet.classList.add('planet-blue-light'); 
            } else if (crashMultiplier <= 10) {
                planet.classList.add('planet-blue-dark'); 
            } else if (crashMultiplier <= 40) {
                planet.classList.add('planet-purple'); 
            } else if (crashMultiplier <= 100) {
                planet.classList.add('planet-purple-light'); 
            } else { 
                planet.classList.add('planet-red-light'); 
            }

            // Update UI Taruhan 1
            const bet = betStatus.bet1;
            if (bet.active && !bet.cashedOut) {
                const potentialWinnings = bet.remainingBet * crashMultiplier;
                const currentTotalWinnings = bet.totalWinnings + potentialWinnings;
                
                document.getElementById('winnings1').innerText = `$${currentTotalWinnings.toFixed(2)}`;
                document.getElementById('cashOutValueAll1').innerText = currentTotalWinnings.toFixed(2);
                
                if (!bet.partialCashedOut) {
                    const partialPayout = (bet.remainingBet / 2) * (1 + crashMultiplier); 
                    document.getElementById('cashOutValuePartial1').innerText = partialPayout.toFixed(2);
                }
            }

            if (crashMultiplier >= crashPoint) {
                gameOver(crashPoint);
                return;
            }

            animationFrameId = requestAnimationFrame(() => animateFlight(crashPoint));
        }


        function gameOver(finalMultiplier) {
            cancelAnimationFrame(animationFrameId);
            isPlaying = false;
            
            document.getElementById('multiplier-display').innerText = finalMultiplier.toFixed(2) + 'x';
            document.getElementById('multiplier-display').style.color = '#FF4500'; 
            
            addHistory(finalMultiplier); 

            let totalLost = 0;
            let finalMessage = `CRASH! MAXWIN GAGAL di ${finalMultiplier.toFixed(2)}x.`;
            
            const bet = betStatus.bet1;
            if (bet.active && !bet.cashedOut) {
                totalLost += bet.remainingBet;
                document.getElementById('remainingBet1').innerText = `$0.00 (LOSE)`;
                document.getElementById('winnings1').innerText = `$${bet.totalWinnings.toFixed(2)} (RUGI)`;
            }

            balance -= totalLost;
            
            document.getElementById('cashOutAll1').disabled = true;
            document.getElementById('cashOutPartial1').disabled = true;

            if (totalLost > 0) {
                finalMessage += ` | LOSS: $${totalLost.toFixed(2)}`;
            }
            document.getElementById('status').innerText = finalMessage;


            resetRound();
            updateBalanceDisplay();
        }

        // --- HANDLER TOMBOL CASHOUT ---

        function handlePartialCashOut(index) {
            const bet = betStatus[`bet${index}`];
            if (isPlaying && bet.active && !bet.cashedOut && !bet.partialCashedOut && bet.remainingBet > 0) {
                
                const betToCashOut = bet.remainingBet / 2;
                const winnings = betToCashOut * crashMultiplier;
                
                balance += betToCashOut + winnings;
                
                bet.remainingBet = bet.remainingBet / 2;

                bet.totalWinnings += winnings;

                bet.partialCashedOut = true; 

                document.getElementById(`cashOutPartial${index}`).disabled = true;
                document.getElementById(`cashOutValuePartial${index}`).innerText = "GACOR!"; 

                document.getElementById(`remainingBet${index}`).innerText = `$${bet.remainingBet.toFixed(2)} (Sisa)`; 
                document.getElementById(`winnings${index}`).innerText = `$${bet.totalWinnings.toFixed(2)}`;

                document.getElementById('status').innerText = `CAIR SETENGAH! PROFIT: $${winnings.toFixed(2)}. Sisa Bet: $${bet.remainingBet.toFixed(2)}`;
                
                updateBalanceDisplay();
            }
        }

        function handleAllCashOut(index) {
            const bet = betStatus[`bet${index}`];
            if (isPlaying && bet.active && !bet.cashedOut && bet.remainingBet > 0) {
                const winnings = bet.remainingBet * crashMultiplier;
                
                balance += bet.remainingBet + winnings;
                
                bet.cashedOut = true;
                bet.remainingBet = 0;
                bet.totalWinnings += winnings;

                document.getElementById(`cashOutAll${index}`).disabled = true;
                document.getElementById(`cashOutPartial${index}`).disabled = true;

                document.getElementById(`remainingBet${index}`).innerText = `$0.00 (CASHOUT)`;
                document.getElementById(`winnings${index}`).innerText = `$${bet.totalWinnings.toFixed(2)} (TOTAL WIN)`;
                
                document.getElementById('status').innerText = `CASHOUT SEMUA! JP BESAR: $${winnings.toFixed(2)}`;

                updateBalanceDisplay();
            }
        }

        function handlePlaceBet(index) {
            const inputId = `betAmount${index}`;
            const amount = parseFloat(document.getElementById(inputId).value);
            const bet = betStatus[`bet${index}`];

            if (isPlaying || bet.active) return; 

            if (amount < 1 || amount > balance || isNaN(amount)) {
                alert("Jumlah taruhan tidak valid atau saldo tidak cukup!");
                return;
            }
            
            bet.amount = amount;
            bet.active = true;
            bet.remainingBet = amount; 
            bet.totalWinnings = 0;
            
            balance -= amount;
            
            document.getElementById(`placeBet${index}`).disabled = true;
            document.getElementById(`remainingBet${index}`).innerText = `$${bet.remainingBet.toFixed(2)}`;
            document.getElementById(`winnings${index}`).innerText = `$0.00`;
            document.getElementById('status').innerText = `TARUHAN $${amount.toFixed(2)} DIPASANG! MENUNGGU LUNCUR!`;

            updateBalanceDisplay();

            if (!isPlaying) {
                startGame();
            }
        }

        // --- EVENT LISTENERS ---
        document.getElementById('cashOutPartial1').addEventListener('click', () => handlePartialCashOut(1));
        document.getElementById('cashOutAll1').addEventListener('click', () => handleAllCashOut(1));
        document.getElementById('placeBet1').addEventListener('click', () => handlePlaceBet(1));

        // --- RESET ---
        function resetRound() {
            betStatus.bet1 = { amount: 0, active: false, cashedOut: false, partialCashedOut: false, remainingBet: 0, totalWinnings: 0 };

            document.getElementById('placeBet1').disabled = false;
            document.getElementById('cashOutPartial1').disabled = true;
            document.getElementById('cashOutAll1').disabled = true;
            
            document.getElementById('winnings1').innerText = "$0.00";
            document.getElementById('cashOutValuePartial1').innerText = "0.00";
            document.getElementById('cashOutValueAll1').innerText = "0.00";
            
            const bet1Input = parseFloat(document.getElementById('betAmount1').value) || 0;
            document.getElementById('remainingBet1').innerText = `$${bet1Input.toFixed(2)}`;
            
            document.getElementById('multiplier-display').innerText = '1.00x';
            document.getElementById('multiplier-display').style.color = '#FFD700'; 

            // Reset posisi visual
            planet.style.transform = `translateX(-50%) translateY(0px)`;
            clearPlanetClasses(); 
            spaceship.style.transform = `translateX(-50%) translateY(0px)`;
            smoke.style.transform = `translateX(-50%) translateY(0px) scale(1)`;
            smoke.style.opacity = '1';
            
            orbitContainer.style.animationDuration = '10s'; 
            orbitContainer.style.transform = `translateX(-50%) rotate(0deg)`; 
            

            setTimeout(() => {
                 if (!isPlaying) document.getElementById('status').innerText = "SIAP JP! PASANG TARUHAN SEKARANG!";
            }, 3000);
        }

        // Inisialisasi tampilan awal
        updateBalanceDisplay();
        updateHistoryDisplay();
        clearPlanetClasses();
        planet.classList.add('planet-blue-light');
        updateFreeTopUpButtons(); 
        
        // Sembunyikan form login dan panel admin saat inisialisasi
        document.getElementById('admin-login').style.display = 'none';
        document.getElementById('admin-panel').style.display = 'none';
    </script>
</body>
</html>

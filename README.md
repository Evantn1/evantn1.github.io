<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AdWatch - Earn USDT</title>
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #8247e5 0%, #6b46c1 100%);
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 800px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            overflow: hidden;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
        }
        
        header {
            background: linear-gradient(135deg, #8247e5 0%, #6b46c1 100%);
            color: white;
            padding: 30px 20px;
            text-align: center;
        }
        
        .logo {
            font-size: 2.5em;
            font-weight: bold;
            margin-bottom: 10px;
        }
        
        .balance-card {
            background: white;
            color: #333;
            padding: 20px;
            border-radius: 15px;
            margin: 20px auto;
            max-width: 300px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }
        
        .balance-amount {
            font-size: 2.5em;
            font-weight: bold;
            color: #8247e5;
        }
        
        .nav-tabs {
            display: flex;
            background: #f8f9fa;
            border-bottom: 2px solid #8247e5;
        }
        
        .tab {
            flex: 1;
            padding: 15px;
            text-align: center;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s;
            color: #666;
        }
        
        .tab.active {
            background: #8247e5;
            color: white;
        }
        
        .tab-content {
            display: none;
            padding: 30px;
            min-height: 400px;
        }
        
        .tab-content.active {
            display: block;
        }
        
        .ad-container {
            background: #f8f9fa;
            border-radius: 15px;
            padding: 40px;
            text-align: center;
            margin: 20px 0;
        }
        
        .ad-placeholder {
            width: 100%;
            height: 250px;
            background: linear-gradient(45deg, #8247e5, #a78bfa);
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 1.5em;
            margin: 20px 0;
            position: relative;
            overflow: hidden;
        }
        
        .ad-placeholder::before {
            content: "ADVERTISEMENT";
            position: absolute;
            font-size: 1em;
            top: 10px;
            left: 10px;
            color: rgba(255,255,255,0.8);
        }
        
        .watch-button {
            background: linear-gradient(135deg, #8247e5 0%, #6b46c1 100%);
            color: white;
            border: none;
            padding: 15px 40px;
            font-size: 1.2em;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            margin: 20px 0;
            transition: transform 0.3s, box-shadow 0.3s;
            box-shadow: 0 5px 15px rgba(130, 71, 229, 0.4);
        }
        
        .watch-button:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(130, 71, 229, 0.6);
        }
        
        .watch-button:disabled {
            opacity: 0.5;
            cursor: not-allowed;
            transform: none;
        }
        
        .timer {
            font-size: 1.2em;
            color: #666;
            margin: 10px 0;
            font-weight: 600;
        }
        
        .stats {
            display: flex;
            justify-content: space-around;
            margin: 20px 0;
            padding: 15px;
            background: white;
            border-radius: 10px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
        }
        
        .stat-item {
            text-align: center;
        }
        
        .stat-value {
            font-size: 1.5em;
            font-weight: bold;
            color: #8247e5;
        }
        
        .stat-label {
            font-size: 0.9em;
            color: #666;
        }
        
        .leaderboard-item {
            display: flex;
            align-items: center;
            padding: 15px;
            margin: 10px 0;
            background: #f8f9fa;
            border-radius: 10px;
            transition: transform 0.3s;
            border-left: 4px solid #8247e5;
        }
        
        .leaderboard-item:hover {
            transform: translateX(5px);
        }
        
        .rank {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            color: white;
            margin-right: 15px;
            font-size: 1.2em;
        }
        
        .rank-1 { 
            background: linear-gradient(135deg, #ffd700 0%, #ffa500 100%);
            box-shadow: 0 4px 10px rgba(255, 165, 0, 0.3);
        }
        .rank-2 { 
            background: linear-gradient(135deg, #c0c0c0 0%, #a0a0a0 100%);
            box-shadow: 0 4px 10px rgba(160, 160, 160, 0.3);
        }
        .rank-3 { 
            background: linear-gradient(135deg, #cd7f32 0%, #a6692e 100%);
            box-shadow: 0 4px 10px rgba(205, 127, 50, 0.3);
        }
        .rank-other { 
            background: linear-gradient(135deg, #8247e5 0%, #6b46c1 100%);
            box-shadow: 0 4px 10px rgba(130, 71, 229, 0.3);
        }
        
        .user-info {
            flex: 1;
        }
        
        .username {
            font-weight: bold;
            font-size: 1.1em;
            color: #333;
        }
        
        .ads-count {
            color: #666;
            font-size: 0.9em;
        }
        
        .reward {
            font-weight: bold;
            color: #8247e5;
            font-size: 1.1em;
        }
        
        .withdrawal-form {
            max-width: 400px;
            margin: 0 auto;
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        .form-label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #333;
        }
        
        input {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 1em;
            transition: border-color 0.3s;
        }
        
        input:focus {
            border-color: #8247e5;
            outline: none;
            box-shadow: 0 0 0 3px rgba(130, 71, 229, 0.1);
        }
        
        .payment-method-info {
            background: white;
            padding: 15px;
            border-radius: 10px;
            margin: 15px 0;
            border-left: 4px solid #8247e5;
        }
        
        .polygon-badge {
            display: inline-block;
            background: linear-gradient(135deg, #8247e5 0%, #6b46c1 100%);
            color: white;
            padding: 5px 10px;
            border-radius: 20px;
            font-size: 0.9em;
            font-weight: bold;
            margin-bottom: 10px;
        }
        
        .withdraw-button {
            background: linear-gradient(135deg, #10b981 0%, #059669 100%);
            color: white;
            border: none;
            padding: 16px;
            width: 100%;
            font-size: 1.2em;
            border-radius: 8px;
            cursor: pointer;
            font-weight: bold;
            transition: transform 0.3s, box-shadow 0.3s;
            box-shadow: 0 5px 15px rgba(16, 185, 129, 0.4);
        }
        
        .withdraw-button:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(16, 185, 129, 0.6);
        }
        
        .withdraw-button:disabled {
            opacity: 0.5;
            cursor: not-allowed;
            transform: none;
        }
        
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            padding: 15px 25px;
            background: #10b981;
            color: white;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
            display: none;
            z-index: 1000;
            animation: slideIn 0.3s ease;
        }
        
        .notification.error {
            background: #ef4444;
        }
        
        .notification.warning {
            background: #f59e0b;
        }
        
        @keyframes slideIn {
            from {
                transform: translateX(100%);
                opacity: 0;
            }
            to {
                transform: translateX(0);
                opacity: 1;
            }
        }
        
        .info-box {
            background: linear-gradient(135deg, #e0e7ff 0%, #f3e8ff 100%);
            padding: 15px;
            border-radius: 10px;
            margin: 15px 0;
            border-left: 4px solid #8247e5;
        }
        
        .info-box h4 {
            margin: 0 0 10px 0;
            color: #8247e5;
        }
        
        .currency-display {
            display: inline-block;
            background: #8247e5;
            color: white;
            padding: 3px 8px;
            border-radius: 5px;
            font-weight: bold;
            margin: 0 2px;
        }
        
        .conversion-note {
            font-size: 0.85em;
            color: #666;
            text-align: center;
            margin-top: 10px;
            padding: 10px;
            background: #f8f9fa;
            border-radius: 8px;
        }
        
        .admin-notice {
            background: linear-gradient(135deg, #fef3c7 0%, #fde68a 100%);
            border-left: 4px solid #f59e0b;
            padding: 10px;
            border-radius: 8px;
            margin-top: 15px;
            font-size: 0.85em;
        }
        
        @media (max-width: 600px) {
            .container {
                margin: 10px;
                border-radius: 15px;
            }
            
            .tab-content {
                padding: 20px;
            }
            
            .ad-placeholder {
                height: 200px;
            }
            
            .stats {
                flex-direction: column;
                gap: 15px;
            }
            
            .notification {
                left: 20px;
                right: 20px;
                text-align: center;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <div class="logo">AdWatch</div>
            <p>Watch ads & Earn USDT</p>
            <div class="balance-card">
                <div>Your Balance</div>
                <div class="balance-amount">$<span id="balance">0.0000</span> USDT</div>
            </div>
        </header>
        
        <div class="nav-tabs">
            <div class="tab active" onclick="showTab('watch')">Watch Ads</div>
            <div class="tab" onclick="showTab('leaderboard')">Leaderboard</div>
            <div class="tab" onclick="showTab('withdraw')">Withdraw</div>
        </div>
        
        <!-- Watch Ads Tab -->
        <div id="watch-tab" class="tab-content active">
            <h2>Watch & Earn USDT</h2>
            <p>Watch a 15-second ad to earn <span class="currency-display">$0.0001 USDT</span></p>
            
            <div class="ad-container">
                <div class="ad-placeholder" id="adDisplay">
                    <div style="text-align: center;">
                        <div style="font-size: 2em; margin-bottom: 10px;">📺</div>
                        <div>Sponsored Content</div>
                        <div style="font-size: 0.8em; margin-top: 5px;">15 seconds</div>
                    </div>
                </div>
                
                <div class="timer" id="timer">Ready to watch ad</div>
                
                <button class="watch-button" id="watchButton" onclick="startAd()">
                    WATCH AD & EARN $0.0001 USDT
                </button>
                
                <div class="stats">
                    <div class="stat-item">
                        <div class="stat-value" id="todayCount">0</div>
                        <div class="stat-label">Today</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value" id="totalCount">0</div>
                        <div class="stat-label">Total Ads</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value" id="earnedToday">$0.0000</div>
                        <div class="stat-label">Earned Today</div>
                    </div>
                </div>
            </div>
            
            <div class="info-box">
                <h4>💡 Tips:</h4>
                <p>• Each ad earns <span class="currency-display">$0.0001 USDT</span> (15 seconds)</p>
                <p>• Watch more ads daily to earn more</p>
                <p>• Weekly leaderboard rewards top watchers</p>
            </div>
        </div>
        
        <!-- Leaderboard Tab -->
        <div id="leaderboard-tab" class="tab-content">
            <h2>Weekly Leaderboard</h2>
            <p>Top earners this week (Resets every Sunday at 00:00 UTC)</p>
            
            <div id="leaderboard-list">
                <!-- Generated dynamically -->
            </div>
            
            <div style="text-align: center; margin-top: 20px; padding: 20px; background: linear-gradient(135deg, #fef3c7 0%, #fde68a 100%); border-radius: 15px;">
                <h3 style="color: #d97706; margin-bottom: 15px;">🏆 Weekly Prizes 🏆</h3>
                <div style="display: flex; justify-content: center; gap: 20px; flex-wrap: wrap;">
                    <div style="background: white; padding: 15px; border-radius: 10px; min-width: 150px; box-shadow: 0 4px 10px rgba(0,0,0,0.1);">
                        <div style="font-size: 1.5em; color: #ffd700;">🥇 1st</div>
                        <div style="font-weight: bold; font-size: 1.2em; color: #8247e5;">$0.50 USDT</div>
                    </div>
                    <div style="background: white; padding: 15px; border-radius: 10px; min-width: 150px; box-shadow: 0 4px 10px rgba(0,0,0,0.1);">
                        <div style="font-size: 1.5em; color: #c0c0c0;">🥈 2nd</div>
                        <div style="font-weight: bold; font-size: 1.2em; color: #8247e5;">$0.30 USDT</div>
                    </div>
                    <div style="background: white; padding: 15px; border-radius: 10px; min-width: 150px; box-shadow: 0 4px 10px rgba(0,0,0,0.1);">
                        <div style="font-size: 1.5em; color: #cd7f32;">🥉 3rd</div>
                        <div style="font-weight: bold; font-size: 1.2em; color: #8247e5;">$0.10 USDT</div>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- Withdrawal Tab -->
        <div id="withdraw-tab" class="tab-content">
            <h2>Withdraw Your USDT</h2>
            <p>Minimum withdrawal: <span class="currency-display">$0.015 USDT</span></p>
            
            <div class="withdrawal-form">
                <div class="payment-method-info">
                    <div class="polygon-badge">POLYGON NETWORK</div>
                    <p><strong>Payment Method:</strong> POL (Polygon Chain Native Token)</p>
                    <p><strong>Withdrawal Currency:</strong> USDT (converted to POL)</p>
                    <p><strong>Network Fee:</strong> ~0.1 POL per transaction</p>
                </div>
                
                <div class="conversion-note">
                    💱 USDT will be converted to POL at current market rate
                </div>
                
                <div class="form-group">
                    <label class="form-label">Amount (USDT)</label>
                    <input type="number" id="withdrawAmount" min="0.015" max="100" step="0.0001" placeholder="0.015">
                    <div style="font-size: 0.85em; color: #666; margin-top: 5px;">
                        Available: $<span id="availableBalance">0.0000</span> USDT
                    </div>
                    <div style="font-size: 0.85em; color: #666; margin-top: 5px;" id="polEquivalent">
                        Equivalent: ~0 POL
                    </div>
                </div>
                
                <div class="form-group">
                    <label class="form-label">POL Polygon Address</label>
                    <input type="text" id="walletAddress" placeholder="0x742d35Cc6634C0532925a3b844Bc9e" pattern="^0x[a-fA-F0-9]{40}$">
                    <div style="font-size: 0.85em; color: #666; margin-top: 5px;">
                        Must start with "0x" and be 42 characters (Polygon address)
                    </div>
                </div>
                
                <div class="info-box">
                    <h4>⚠️ Important:</h4>
                    <p>• USDT will be converted to POL (Polygon's native token)</p>
                    <p>• Only send to Polygon (POL) addresses</p>
                    <p>• Withdrawals processed within 24 hours</p>
                    <p>• Network fees (~0.1 POL) deducted from withdrawal</p>
                </div>
                
                <div class="admin-notice">
                    ⚡ <strong>Admin Notification:</strong> All withdrawals will send a notification to the admin bot for manual processing.
                </div>
                
                <button class="withdraw-button" onclick="processWithdrawal()">
                    WITHDRAW USDT (as POL)
                </button>
            </div>
        </div>
    </div>
    
    <div class="notification" id="notification"></div>
    
    <script>
        // ============ CONFIGURATION ============
        // 🔧 CONFIGURE THESE SETTINGS:
        const BOT_TOKEN = 'YOUR_BOT_TOKEN_HERE'; // Your Telegram Bot Token from @BotFather
        const ADMIN_CHAT_ID = 'YOUR_CHAT_ID_HERE'; // Your Telegram Chat ID to receive notifications
        
        // App Constants
        const AD_DURATION = 15; // 15-second ads
        const AD_REWARD = 0.0001; // $0.0001 USDT per ad
        const MIN_WITHDRAWAL = 0.015; // $0.015 USDT minimum
        const NETWORK_FEE_POL = 0.1; // 0.1 POL network fee
        const USDT_TO_POL_RATE = 0.0012; // Example: 1 USDT = 0.0012 POL
        
        // ============ APP CODE ============
        // Initialize Telegram Web App
        let tg = window.Telegram.WebApp;
        tg.expand();
        tg.ready();
        
        // User data
        let userData = {
            balance: 0.0000,
            adsToday: 0,
            totalAds: 0,
            earnedToday: 0.0000,
            username: 'User' + Math.floor(Math.random() * 10000),
            lastAdDate: null,
            userId: null,
            firstName: '',
            lastName: ''
        };
        
        // Load data from localStorage
        function loadData() {
            const saved = localStorage.getItem('adWatchData');
            if (saved) {
                const parsed = JSON.parse(saved);
                const today = new Date().toDateString();
                
                // Reset daily stats if it's a new day
                if (parsed.lastAdDate !== today) {
                    parsed.adsToday = 0;
                    parsed.earnedToday = 0.0000;
                }
                
                userData = parsed;
            }
            updateDisplay();
        }
        
        // Save data to localStorage
        function saveData() {
            userData.lastAdDate = new Date().toDateString();
            localStorage.setItem('adWatchData', JSON.stringify(userData));
        }
        
        // Send notification to Telegram bot
        async function sendTelegramNotification(message) {
            // Only send if bot token is configured
            if (BOT_TOKEN === 'YOUR_BOT_TOKEN_HERE' || ADMIN_CHAT_ID === 'YOUR_CHAT_ID_HERE') {
                console.log('⚠️ Bot token or chat ID not configured');
                console.log('📝 Notification message:', message);
                return false;
            }
            
            try {
                const url = `https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`;
                
                const response = await fetch(url, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({
                        chat_id: ADMIN_CHAT_ID,
                        text: message,
                        parse_mode: 'HTML'
                    })
                });
                
                const data = await response.json();
                return data.ok;
            } catch (error) {
                console.error('Error sending Telegram notification:', error);
                return false;
            }
        }
        
        // Update all displayed values
        function updateDisplay() {
            document.getElementById('balance').textContent = userData.balance.toFixed(4);
            document.getElementById('todayCount').textContent = userData.adsToday;
            document.getElementById('totalCount').textContent = userData.totalAds;
            document.getElementById('earnedToday').textContent = '$' + userData.earnedToday.toFixed(4);
            document.getElementById('availableBalance').textContent = userData.balance.toFixed(4);
            
            // Update POL equivalent
            updatePolEquivalent();
            
            // Update leaderboard
            generateLeaderboard();
        }
        
        // Update POL equivalent display
        function updatePolEquivalent() {
            const amountInput = document.getElementById('withdrawAmount');
            const amount = parseFloat(amountInput.value) || 0;
            const polAmount = amount * USDT_TO_POL_RATE;
            document.getElementById('polEquivalent').textContent = 
                `Equivalent: ~${polAmount.toFixed(4)} POL (Rate: 1 USDT = ${USDT_TO_POL_RATE.toFixed(4)} POL)`;
        }
        
        // Tab navigation
        function showTab(tabName) {
            // Hide all tabs
            document.querySelectorAll('.tab-content').forEach(tab => {
                tab.classList.remove('active');
            });
            
            // Remove active class from all tab buttons
            document.querySelectorAll('.tab').forEach(tab => {
                tab.classList.remove('active');
            });
            
            // Show selected tab
            document.getElementById(tabName + '-tab').classList.add('active');
            
            // Activate clicked tab button
            event.target.classList.add('active');
            
            // Update POL equivalent when withdrawal tab is shown
            if (tabName === 'withdraw') {
                updatePolEquivalent();
            }
        }
        
        // Ad watching function
        let adTimer;
        let secondsLeft = AD_DURATION;
        
        function startAd() {
            const button = document.getElementById('watchButton');
            button.disabled = true;
            button.textContent = 'WATCHING AD...';
            
            secondsLeft = AD_DURATION;
            document.getElementById('timer').textContent = `Ad playing... ${secondsLeft}s remaining`;
            
            // Show progress bar animation
            const adDisplay = document.getElementById('adDisplay');
            adDisplay.innerHTML = `
                <div style="text-align: center; width: 100%;">
                    <div style="font-size: 2em; margin-bottom: 15px;">⏳</div>
                    <div>Watching ad...</div>
                    <div style="margin-top: 15px; background: rgba(255,255,255,0.2); border-radius: 10px; overflow: hidden;">
                        <div id="progressBar" style="height: 8px; background: white; width: 0%; transition: width 1s linear;"></div>
                    </div>
                    <div style="font-size: 0.9em; margin-top: 10px;">Earning $${AD_REWARD.toFixed(4)} USDT</div>
                </div>
            `;
            
            // Start progress bar
            let progress = 0;
            const progressBar = document.getElementById('progressBar');
            const progressInterval = setInterval(() => {
                progress += (100 / AD_DURATION); // 100% over AD_DURATION seconds
                progressBar.style.width = Math.min(progress, 100) + '%';
            }, 1000);
            
            adTimer = setInterval(() => {
                secondsLeft--;
                document.getElementById('timer').textContent = `Ad playing... ${secondsLeft}s remaining`;
                
                if (secondsLeft <= 0) {
                    clearInterval(progressInterval);
                    finishAd();
                }
            }, 1000);
        }
        
        function finishAd() {
            clearInterval(adTimer);
            
            // Add earnings
            userData.balance += AD_REWARD;
            userData.adsToday++;
            userData.totalAds++;
            userData.earnedToday += AD_REWARD;
            
            // Update display
            updateDisplay();
            saveData();
            
            // Show notification
            showNotification(`🎉 Earned $${AD_REWARD.toFixed(4)} USDT!`);
            
            // Reset ad display
            const adDisplay = document.getElementById('adDisplay');
            adDisplay.innerHTML = `
                <div style="text-align: center;">
                    <div style="font-size: 2em; margin-bottom: 10px;">✅</div>
                    <div>Ad Completed!</div>
                    <div style="font-size: 0.9em; margin-top: 10px;">+$${AD_REWARD.toFixed(4)} USDT added</div>
                </div>
            `;
            
            // Reset button after 2 seconds
            setTimeout(() => {
                const button = document.getElementById('watchButton');
                button.disabled = false;
                button.textContent = `WATCH AD & EARN $${AD_REWARD.toFixed(4)} USDT`;
                document.getElementById('timer').textContent = 'Ready to watch another ad!';
                
                // Reset ad display
                adDisplay.innerHTML = `
                    <div style="text-align: center;">
                        <div style="font-size: 2em; margin-bottom: 10px;">📺</div>
                        <div>Sponsored Content</div>
                        <div style="font-size: 0.8em; margin-top: 5px;">${AD_DURATION} seconds</div>
                    </div>
                `;
            }, 2000);
        }
        
        // Leaderboard data
        function generateLeaderboard() {
            const leaderboard = [
                { username: 'CryptoKing', ads: 245, reward: '$0.50 USDT' },
                { username: 'AdMaster', ads: 198, reward: '$0.30 USDT' },
                { username: 'EarnPro', ads: 167, reward: '$0.10 USDT' },
                { username: userData.username, ads: userData.totalAds, reward: '-' },
                { username: 'BitcoinLover', ads: 89, reward: '-' },
                { username: 'TradingGuru', ads: 76, reward: '-' },
                { username: 'CryptoNewbie', ads: 54, reward: '-' }
            ];
            
            // Sort by ads watched
            leaderboard.sort((a, b) => b.ads - a.ads);
            
            const listElement = document.getElementById('leaderboard-list');
            listElement.innerHTML = '';
            
            leaderboard.forEach((user, index) => {
                const item = document.createElement('div');
                item.className = 'leaderboard-item';
                
                const rankClass = index === 0 ? 'rank-1' : 
                                index === 1 ? 'rank-2' : 
                                index === 2 ? 'rank-3' : 'rank-other';
                
                item.innerHTML = `
                    <div class="rank ${rankClass}">${index + 1}</div>
                    <div class="user-info">
                        <div class="username">${user.username}</div>
                        <div class="ads-count">${user.ads} ads watched</div>
                    </div>
                    <div class="reward">${user.reward}</div>
                `;
                
                listElement.appendChild(item);
            });
        }
        
        // Validate Polygon address
        function isValidPolygonAddress(address) {
            return /^0x[a-fA-F0-9]{40}$/.test(address);
        }
        
        // Calculate total POL needed (USDT amount + fee)
        function calculateTotalPOLNeeded(usdtAmount) {
            const polAmount = usdtAmount * USDT_TO_POL_RATE;
            const totalPOL = polAmount + NETWORK_FEE_POL;
            return {
                usdt: usdtAmount,
                polAmount: polAmount,
                fee: NETWORK_FEE_POL,
                total: totalPOL
            };
        }
        
        // Generate withdrawal ID
        function generateWithdrawalId() {
            return 'W' + Date.now() + Math.random().toString(36).substr(2, 6).toUpperCase();
        }
        
        // Withdrawal function
        async function processWithdrawal() {
            const amount = parseFloat(document.getElementById('withdrawAmount').value);
            const wallet = document.getElementById('walletAddress').value.trim();
            
            // Validation
            if (!amount || isNaN(amount)) {
                showNotification('⚠️ Please enter a valid amount', 'warning');
                return;
            }
            
            if (amount < MIN_WITHDRAWAL) {
                showNotification(`⚠️ Minimum withdrawal is $${MIN_WITHDRAWAL.toFixed(4)} USDT`, 'warning');
                return;
            }
            
            if (amount > userData.balance) {
                showNotification('⚠️ Insufficient USDT balance', 'warning');
                return;
            }
            
            if (!wallet || !isValidPolygonAddress(wallet)) {
                showNotification('⚠️ Please enter a valid Polygon wallet address', 'warning');
                return;
            }
            
            // Calculate POL equivalent
            const polCalculation = calculateTotalPOLNeeded(amount);
            const withdrawalId = generateWithdrawalId();
            
            // Show confirmation with details
            const confirmationMessage = `
Withdraw $${amount.toFixed(4)} USDT as POL?

Details:
• USDT Amount: $${amount.toFixed(4)}
• POL Equivalent: ${polCalculation.polAmount.toFixed(4)} POL
• Network Fee: ${polCalculation.fee.toFixed(4)} POL
• Total POL: ${polCalculation.total.toFixed(4)} POL
• To Address: ${wallet.substring(0, 16)}...${wallet.substring(38)}

Conversion Rate: 1 USDT = ${USDT_TO_POL_RATE.toFixed(4)} POL

Confirm withdrawal?
            `;
            
            if (confirm(confirmationMessage)) {
                // Disable button to prevent double submission
                const withdrawBtn = document.querySelector('.withdraw-button');
                withdrawBtn.disabled = true;
                withdrawBtn.textContent = 'PROCESSING...';
                
                // Simulate processing
                showNotification('⏳ Processing withdrawal request...', 'success');
                
                // In real app, this would process actual withdrawal
                // For demo, we just simulate it
                setTimeout(async () => {
                    userData.balance -= amount;
                    saveData();
                    updateDisplay();
                    
                    // Send Telegram notification to admin
                    const telegramMessage = `
🚀 <b>NEW WITHDRAWAL REQUEST</b> 🚀

<b>Withdrawal ID:</b> <code>${withdrawalId}</code>
<b>User:</b> ${userData.username}
<b>User ID:</b> ${userData.userId || 'N/A'}
<b>Amount:</b> $${amount.toFixed(4)} USDT
<b>POL Equivalent:</b> ${polCalculation.polAmount.toFixed(4)} POL
<b>Network Fee:</b> ${polCalculation.fee.toFixed(4)} POL
<b>Total to Send:</b> ${polCalculation.total.toFixed(4)} POL
<b>Wallet Address:</b> <code>${wallet}</code>
<b>Date:</b> ${new Date().toLocaleString()}
<b>User Balance After:</b> $${userData.balance.toFixed(4)} USDT

<b>User Stats:</b>
• Total Ads: ${userData.totalAds}
• Ads Today: ${userData.adsToday}
• Total Earned: $${(userData.totalAds * AD_REWARD).toFixed(4)} USDT

<b>ACTION REQUIRED:</b>
Send ${polCalculation.total.toFixed(4)} POL to address above.
                    `;
                    
                    // Send notification to Telegram bot
                    const notificationSent = await sendTelegramNotification(telegramMessage);
                    
                    if (notificationSent) {
                        showNotification(`✅ Withdrawal request #${withdrawalId} submitted!\nAdmin has been notified.\nYou will receive ${polCalculation.polAmount.toFixed(4)} POL.\nProcessing time: 1-24 hours`);
                    } else {
                        showNotification(`✅ Withdrawal request #${withdrawalId} submitted!\nYou will receive ${polCalculation.polAmount.toFixed(4)} POL.\nProcessing time: 1-24 hours`);
                    }
                    
                    // Clear form
                    document.getElementById('withdrawAmount').value = '';
                    document.getElementById('walletAddress').value = '';
                    
                    // Re-enable button
                    withdrawBtn.disabled = false;
                    withdrawBtn.textContent = 'WITHDRAW USDT (as POL)';
                    
                    // Show transaction details (simulated)
                    setTimeout(() => {
                        const txHash = '0x' + Math.random().toString(16).substr(2, 64);
                        showNotification(`📝 Transaction sent on Polygon!\nHash: ${txHash.substr(0, 16)}...\nAmount: ${polCalculation.polAmount.toFixed(4)} POL`);
                    }, 1500);
                    
                }, 2000); // Simulate 2 second processing time
            }
        }
        
        // Notification system
        function showNotification(message, type = 'success') {
            const notification = document.getElementById('notification');
            notification.textContent = message;
            notification.className = 'notification ' + type;
            notification.style.display = 'block';
            
            setTimeout(() => {
                notification.style.display = 'none';
            }, 4000);
        }
        
        // Initialize app
        loadData();
        
        // Try to get Telegram user info
        if (tg.initDataUnsafe && tg.initDataUnsafe.user) {
            const tgUser = tg.initDataUnsafe.user;
            userData.username = tgUser.username || 
                              `${tgUser.first_name || ''} ${tgUser.last_name || ''}`.trim() || 
                              userData.username;
            userData.userId = tgUser.id;
            userData.firstName = tgUser.first_name || '';
            userData.lastName = tgUser.last_name || '';
            updateDisplay();
            
            // Send welcome notification to admin (optional)
            if (BOT_TOKEN !== 'YOUR_BOT_TOKEN_HERE' && ADMIN_CHAT_ID !== 'YOUR_CHAT_ID_HERE') {
                const welcomeMessage = `
👤 <b>New User Started App</b>

<b>User:</b> ${userData.username}
<b>User ID:</b> ${userData.userId}
<b>Name:</b> ${userData.firstName} ${userData.lastName}
<b>Date:</b> ${new Date().toLocaleString()}
                `;
                
                // Send in background, don't wait for response
                sendTelegramNotification(welcomeMessage);
            }
        }
        
        // Update POL equivalent when user types amount
        document.getElementById('withdrawAmount').addEventListener('input', updatePolEquivalent);
        
        // Update timer and reset time
        setInterval(() => {
            const now = new Date();
            const day = now.getDay();
            const hours = now.getHours();
            const minutes = now.getMinutes();
            
            // Show leaderboard reset time
            if (document.getElementById('leaderboard-tab').classList.contains('active')) {
                const daysLeft = 6 - day;
                const hoursLeft = 23 - hours;
                const minutesLeft = 59 - minutes;
                const resetTime = `Leaderboard resets in ${daysLeft}d ${hoursLeft}h ${minutesLeft}m`;
                const resetElement = document.querySelector('#leaderboard-tab p');
                if (resetElement && daysLeft >= 0) {
                    resetElement.textContent = resetTime;
                }
            }
        }, 60000); // Update every minute
    </script>
</body>
</html>

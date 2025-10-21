<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Steel Brainrot - Генератор ключей</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #0c0c0c, #1a1a2e, #16213e);
            color: white;
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 20px;
            padding: 40px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 0 50px rgba(0, 255, 136, 0.1);
        }

        header {
            text-align: center;
            margin-bottom: 40px;
        }

        h1 {
            font-size: 3em;
            background: linear-gradient(45deg, #00ff88, #00ccff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 10px;
            text-shadow: 0 0 30px rgba(0, 255, 136, 0.3);
        }

        .subtitle {
            color: #888;
            font-size: 1.2em;
        }

        .key-section {
            background: rgba(0, 0, 0, 0.3);
            border: 2px solid #00ff88;
            border-radius: 15px;
            padding: 30px;
            margin: 30px 0;
            text-align: center;
        }

        .key-display {
            font-size: 2em;
            font-weight: bold;
            letter-spacing: 3px;
            color: #00ff88;
            margin: 20px 0;
            padding: 20px;
            background: rgba(0, 255, 136, 0.1);
            border-radius: 10px;
            border: 1px solid rgba(0, 255, 136, 0.3);
            word-break: break-all;
        }

        .btn {
            background: linear-gradient(45deg, #00ff88, #00ccff);
            border: none;
            border-radius: 10px;
            color: #000;
            padding: 18px 35px;
            font-size: 1.2em;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            margin: 10px;
            box-shadow: 0 0 20px rgba(0, 255, 136, 0.3);
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 0 30px rgba(0, 255, 136, 0.5);
        }

        .btn-secondary {
            background: rgba(255, 255, 255, 0.1);
            color: #00ff88;
            border: 1px solid #00ff88;
        }

        .stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin: 40px 0;
        }

        .stat-box {
            background: rgba(255, 255, 255, 0.05);
            padding: 25px;
            border-radius: 15px;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .stat-number {
            font-size: 2.5em;
            font-weight: bold;
            color: #00ff88;
            margin-bottom: 10px;
        }

        .timer {
            font-size: 1.5em;
            color: #ff4444;
            font-weight: bold;
            margin: 20px 0;
        }

        .instructions {
            background: rgba(0, 0, 0, 0.3);
            padding: 30px;
            border-radius: 15px;
            margin: 30px 0;
            border-left: 5px solid #00ff88;
        }

        .instructions ol {
            margin-left: 20px;
            line-height: 2;
        }

        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            background: #00ff88;
            color: black;
            padding: 20px;
            border-radius: 10px;
            font-weight: bold;
            display: none;
            z-index: 1000;
            box-shadow: 0 0 20px rgba(0, 255, 136, 0.5);
        }

        footer {
            text-align: center;
            margin-top: 40px;
            color: #666;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            padding-top: 20px;
        }

        .admin-panel {
            background: rgba(255, 0, 0, 0.1);
            border: 1px solid #ff4444;
            border-radius: 10px;
            padding: 20px;
            margin-top: 30px;
        }

        .admin-input {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid #ff4444;
            border-radius: 5px;
            color: white;
        }

        @media (max-width: 768px) {
            .container {
                padding: 20px;
            }
            
            h1 {
                font-size: 2em;
            }
            
            .key-display {
                font-size: 1.5em;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>🔑 STEEL BRAINROT</h1>
            <p class="subtitle">Генератор лицензионных ключей • 24 часа доступа</p>
        </header>

        <div class="key-section">
            <h2>Ваш ключ доступа:</h2>
            <div class="key-display" id="keyDisplay">
                Нажмите "Получить ключ"
            </div>
            
            <div class="timer" id="timer">
                --:--:--
            </div>

            <div>
                <button class="btn" onclick="generateKey()">🎲 Получить ключ</button>
                <button class="btn btn-secondary" onclick="copyKey()">📋 Копировать ключ</button>
            </div>
        </div>

        <div class="stats">
            <div class="stat-box">
                <div class="stat-number" id="activeUsers">1,847</div>
                <div>Активных пользователей</div>
            </div>
            <div class="stat-box">
                <div class="stat-number" id="keysGenerated">324</div>
                <div>Ключей сегодня</div>
            </div>
            <div class="stat-box">
                <div class="stat-number">24ч</div>
                <div>Время действия ключа</div>
            </div>
        </div>

        <div class="instructions">
            <h3>📖 Инструкция по активации:</h3>
            <ol>
                <li>Нажмите "Получить ключ" для генерации нового ключа</li>
                <li>Скопируйте ключ с помощью кнопки "Копировать ключ"</li>
                <li>Запустите скрипт Steel Brainrot в Roblox</li>
                <li>Вставьте ключ в окно активации</li>
                <li>Ключ действителен 24 часа с момента генерации</li>
                <li>По истечении времени получите новый ключ</li>
            </ol>
        </div>

        <!-- Секретная админ-панель -->
        <div class="admin-panel" id="adminPanel" style="display: none;">
            <h3>🔧 Панель администратора</h3>
            <input type="password" class="admin-input" id="adminPassword" placeholder="Введите пароль администратора">
            <button class="btn" onclick="toggleAdmin()">Войти</button>
            
            <div id="adminControls" style="display: none; margin-top: 20px;">
                <button class="btn btn-secondary" onclick="resetStats()">🔄 Сбросить статистику</button>
                <button class="btn btn-secondary" onclick="viewAllKeys()">📋 Показать все ключи</button>
                <button class="btn btn-secondary" onclick="exportKeys()">💾 Экспорт ключей</button>
            </div>
        </div>

        <footer>
            <p>Steel Brainrot &copy; 2024 • Каждый ключ уникален и защищен от копирования</p>
            <p style="margin-top: 10px; font-size: 0.8em; color: #444;">
                <a href="#" onclick="toggleAdminPanel()" style="color: #666; text-decoration: none;">⚙️</a>
            </p>
        </footer>
    </div>

    <div class="notification" id="notification">
        Ключ скопирован в буфер обмена!
    </div>

    <script>
        class KeyManager {
            constructor() {
                this.storageKey = 'steelBrainrotKeys';
                this.adminPassword = 'STEEL2024';
                this.loadKeys();
            }

            loadKeys() {
                const saved = localStorage.getItem(this.storageKey);
                if (saved) {
                    this.keysData = JSON.parse(saved);
                } else {
                    this.keysData = {
                        keys: [],
                        stats: {
                            totalUsers: 1847,
                            keysToday: 324,
                            lastReset: new Date().toDateString()
                        }
                    };
                }
                
                this.checkDailyReset();
            }

            saveKeys() {
                localStorage.setItem(this.storageKey, JSON.stringify(this.keysData));
            }

            checkDailyReset() {
                const today = new Date().toDateString();
                if (this.keysData.stats.lastReset !== today) {
                    this.keysData.stats.keysToday = 0;
                    this.keysData.stats.lastReset = today;
                    this.saveKeys();
                }
            }

            generateKey() {
                const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789';
                let key;
                
                do {
                    key = '';
                    for (let i = 0; i < 19; i++) {
                        if (i === 4 || i === 9 || i === 14) {
                            key += '-';
                        } else {
                            key += chars.charAt(Math.floor(Math.random() * chars.length));
                        }
                    }
                } while (this.isKeyExists(key));

                const keyData = {
                    key: key,
                    created: new Date().toISOString(),
                    expires: new Date(Date.now() + 24 * 60 * 60 * 1000).toISOString(),
                    used: false
                };

                this.keysData.keys.unshift(keyData);
                this.keysData.stats.keysToday++;
                this.keysData.stats.totalUsers += Math.random() > 0.8 ? 1 : 0;
                
                if (this.keysData.keys.length > 50) {
                    this.keysData.keys = this.keysData.keys.slice(0, 50);
                }

                this.saveKeys();
                this.updateStats();
                return keyData;
            }

            isKeyExists(key) {
                return this.keysData.keys.some(k => k.key === key);
            }

            getActiveKey() {
                const now = new Date();
                return this.keysData.keys.find(k => new Date(k.expires) > now && !k.used);
            }

            updateStats() {
                document.getElementById('activeUsers').textContent = 
                    this.keysData.stats.totalUsers.toLocaleString();
                document.getElementById('keysGenerated').textContent = 
                    this.keysData.stats.keysToday;
            }

            startTimer(expiresAt) {
                const timerElement = document.getElementById('timer');
                const updateTimer = () => {
                    const now = new Date();
                    const expires = new Date(expiresAt);
                    const diff = expires - now;

                    if (diff <= 0) {
                        timerElement.textContent = 'Ключ истек!';
                        timerElement.style.color = '#ff4444';
                        return;
                    }

                    const hours = Math.floor(diff / (1000 * 60 * 60));
                    const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
                    const seconds = Math.floor((diff % (1000 * 60)) / 1000);

                    timerElement.textContent = 
                        `${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
                    timerElement.style.color = hours < 1 ? '#ff4444' : '#00ff88';
                };

                updateTimer();
                setInterval(updateTimer, 1000);
            }

            resetStats() {
                this.keysData.stats.keysToday = 0;
                this.keysData.stats.totalUsers = 1500;
                this.saveKeys();
                this.updateStats();
                showNotification('Статистика сброшена!');
            }

            getAllKeys() {
                return this.keysData.keys;
            }
        }

        const keyManager = new KeyManager();

        function generateKey() {
            const keyData = keyManager.generateKey();
            document.getElementById('keyDisplay').textContent = keyData.key;
            keyManager.startTimer(keyData.expires);
            showNotification('Новый ключ сгенерирован! Действует 24 часа.');
        }

        function copyKey() {
            const key = document.getElementById('keyDisplay').textContent;
            if (key !== 'Нажмите "Получить ключ"') {
                navigator.clipboard.writeText(key).then(() => {
                    showNotification('✅ Ключ скопирован в буфер обмена!');
                }).catch(() => {
                    // Fallback для старых браузеров
                    const textArea = document.createElement('textarea');
                    textArea.value = key;
                    document.body.appendChild(textArea);
                    textArea.select();
                    document.execCommand('copy');
                    document.body.removeChild(textArea);
                    showNotification('✅ Ключ скопирован!');
                });
            } else {
                showNotification('❌ Сначала получите ключ!');
            }
        }

        function showNotification(message) {
            const notification = document.getElementById('notification');
            notification.textContent = message;
            notification.style.display = 'block';
            setTimeout(() => {
                notification.style.display = 'none';
            }, 3000);
        }

        function toggleAdminPanel() {
            const adminPanel = document.getElementById('adminPanel');
            adminPanel.style.display = adminPanel.style.display === 'none' ? 'block' : 'none';
        }

        function toggleAdmin() {
            const password = document.getElementById('adminPassword').value;
            const adminControls = document.getElementById('adminControls');
            
            if (password === keyManager.adminPassword) {
                adminControls.style.display = 'block';
                showNotification('🔧 Доступ к панели администратора разрешен');
            } else {
                showNotification('❌ Неверный пароль');
            }
        }

        function resetStats() {
            keyManager.resetStats();
        }

        function viewAllKeys() {
            const keys = keyManager.getAllKeys();
            alert('Все ключи:\n' + keys.map(k => 
                `${k.key} - ${new Date(k.created).toLocaleDateString()}`
            ).join('\n'));
        }

        function exportKeys() {
            const keys = keyManager.getAllKeys();
            const data = JSON.stringify(keys, null, 2);
            const blob = new Blob([data], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'steel_brainrot_keys.json';
            a.click();
            URL.revokeObjectURL(url);
        }

        // Инициализация при загрузке
        window.onload = function() {
            keyManager.updateStats();
            const activeKey = keyManager.getActiveKey();
            if (activeKey) {
                document.getElementById('keyDisplay').textContent = activeKey.key;
                keyManager.startTimer(activeKey.expires);
            }
            
            // Автогенерация ключа при первом посещении
            if (!activeKey) {
                generateKey();
            }
        }

        // Сохранение перед закрытием
        window.addEventListener('beforeunload', function() {
            keyManager.saveKeys();
        });
    </script>
</body>
</html>

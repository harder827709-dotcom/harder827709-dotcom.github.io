# harder827709-dotcom.github.io
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no, maximum-scale=1.0, minimum-scale=1.0">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <title>2048 - 特别版</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
            user-select: none;
            -webkit-user-select: none;
        }

        body {
            background: #faf8ef;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 15px;
        }

        /* ============ 启动页面 ============ */
        .startup-page {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            width: 100%;
            max-width: 400px;
            text-align: center;
        }

        .startup-title {
            font-size: 48px;
            font-weight: 900;
            color: #776e65;
            margin-bottom: 10px;
        }

        .startup-subtitle {
            font-size: 16px;
            color: #8f7a66;
            margin-bottom: 30px;
        }

        .password-input-wrapper {
            position: relative;
            width: 100%;
            margin-bottom: 20px;
        }

        .password-input {
            width: 100%;
            padding: 15px;
            border: 3px solid #bbada0;
            border-radius: 10px;
            font-size: 18px;
            text-align: center;
            outline: none;
            transition: border-color 0.3s;
            background: white;
            color: #776e65;
        }

        .password-input:focus {
            border-color: #776e65;
        }

        .password-input.error {
            border-color: #ff3b30;
            animation: shake 0.5s;
        }

        .password-input.success {
            border-color: #34c759;
        }

        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-10px); }
            75% { transform: translateX(10px); }
        }

        .hint-text {
            font-size: 13px;
            color: #8f7a66;
            margin-bottom: 15px;
            font-style: italic;
        }

        .enter-btn {
            width: 100%;
            padding: 14px;
            background: #8f7a66;
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 18px;
            font-weight: 700;
            cursor: pointer;
            transition: background 0.2s;
        }

        .enter-btn:active {
            background: #776e65;
        }

        .enter-btn:disabled {
            background: #ccc;
            cursor: not-allowed;
        }

        /* ============ 登录页面 ============ */
        .login-page {
            display: none;
            flex-direction: column;
            align-items: center;
            width: 100%;
            max-width: 400px;
        }

        .login-title {
            font-size: 36px;
            font-weight: 900;
            color: #776e65;
            margin-bottom: 10px;
        }

        .login-subtitle {
            font-size: 14px;
            color: #8f7a66;
            margin-bottom: 25px;
            text-align: center;
            line-height: 1.6;
        }

        .username-input-wrapper {
            position: relative;
            width: 100%;
            margin-bottom: 15px;
        }

        .username-input {
            width: 100%;
            padding: 15px;
            border: 3px solid #bbada0;
            border-radius: 10px;
            font-size: 18px;
            text-align: center;
            outline: none;
            transition: border-color 0.3s;
            background: white;
            color: #776e65;
        }

        .username-input:focus {
            border-color: #776e65;
        }

        .username-input.error {
            border-color: #ff3b30;
            animation: shake 0.5s;
        }

        .username-input.success {
            border-color: #34c759;
        }

        .error-message {
            color: #ff3b30;
            font-size: 13px;
            min-height: 20px;
            margin-bottom: 10px;
            text-align: center;
        }

        .start-game-btn {
            width: 100%;
            padding: 14px;
            background: #8f7a66;
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 18px;
            font-weight: 700;
            cursor: pointer;
            transition: background 0.2s;
        }

        .start-game-btn:active {
            background: #776e65;
        }

        /* ============ 游戏页面 ============ */
        .game-page {
            display: none;
            width: 100%;
            max-width: 400px;
        }

        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            flex-wrap: wrap;
            gap: 10px;
        }

        .game-title {
            font-size: 48px;
            font-weight: 900;
            color: #776e65;
            line-height: 1;
        }

        .player-info {
            font-size: 14px;
            color: #8f7a66;
            font-weight: 600;
        }

        .scores {
            display: flex;
            gap: 8px;
        }

        .score-box {
            background: #bbada0;
            color: white;
            padding: 8px 15px;
            border-radius: 6px;
            text-align: center;
            min-width: 70px;
        }

        .score-label {
            font-size: 11px;
            text-transform: uppercase;
            letter-spacing: 1px;
            opacity: 0.8;
        }

        .score-value {
            font-size: 22px;
            font-weight: 700;
        }

        .sub-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            flex-wrap: wrap;
            gap: 10px;
        }

        .description {
            font-size: 14px;
            color: #776e65;
            line-height: 1.4;
        }

        .btn-group {
            display: flex;
            gap: 8px;
        }

        .new-game-btn, .logout-btn {
            background: #8f7a66;
            color: white;
            border: none;
            padding: 10px 16px;
            border-radius: 6px;
            font-size: 13px;
            font-weight: 700;
            cursor: pointer;
            transition: background 0.2s;
            white-space: nowrap;
        }

        .logout-btn {
            background: #cdc1b4;
            color: #776e65;
        }

        .new-game-btn:active {
            background: #9f8b77;
        }

        .logout-btn:active {
            background: #bbada0;
        }

        .game-container {
            background: #bbada0;
            border-radius: 10px;
            padding: 10px;
            position: relative;
            margin-bottom: 15px;
            touch-action: none;
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
            position: relative;
        }

        .cell {
            background: rgba(238, 228, 218, 0.35);
            border-radius: 6px;
            aspect-ratio: 1;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 28px;
            font-weight: 800;
            transition: all 0.15s ease-in-out;
            position: relative;
            z-index: 1;
        }

        .cell[data-value="2"] { background: #eee4da; color: #776e65; }
        .cell[data-value="4"] { background: #ede0c8; color: #776e65; }
        .cell[data-value="8"] { background: #f2b179; color: #f9f6f2; }
        .cell[data-value="16"] { background: #f59563; color: #f9f6f2; }
        .cell[data-value="32"] { background: #f67c5f; color: #f9f6f2; }
        .cell[data-value="64"] { background: #f65e3b; color: #f9f6f2; }
        .cell[data-value="128"] { background: #edcf72; color: #f9f6f2; font-size: 24px; }
        .cell[data-value="256"] { background: #edcc61; color: #f9f6f2; font-size: 24px; }
        .cell[data-value="512"] { background: #edc850; color: #f9f6f2; font-size: 24px; }
        .cell[data-value="1024"] { background: #edc53f; color: #f9f6f2; font-size: 20px; }
        .cell[data-value="2048"] { background: #edc22e; color: #f9f6f2; font-size: 20px; }
        .cell[data-value="4096"] { background: #3c3a32; color: #f9f6f2; font-size: 18px; }

        .cell.new-tile {
            animation: appear 0.2s ease-in-out;
        }

        .cell.merged {
            animation: pop 0.2s ease-in-out;
        }

        @keyframes appear {
            0% { transform: scale(0); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }

        @keyframes pop {
            0% { transform: scale(1); }
            50% { transform: scale(1.2); }
            100% { transform: scale(1); }
        }

        .game-over {
            display: none;
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(238, 228, 218, 0.73);
            border-radius: 10px;
            justify-content: center;
            align-items: center;
            z-index: 10;
            font-size: 40px;
            font-weight: 900;
            color: #776e65;
            flex-direction: column;
        }

        .game-over.active {
            display: flex;
        }

        .game-over .final-score {
            font-size: 20px;
            margin-top: 10px;
            font-weight: 600;
        }

        .game-over .retry-btn {
            margin-top: 20px;
            background: #8f7a66;
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 6px;
            font-size: 18px;
            font-weight: 700;
            cursor: pointer;
        }

        .win-message {
            display: none;
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(237, 194, 46, 0.5);
            border-radius: 10px;
            justify-content: center;
            align-items: center;
            z-index: 10;
            font-size: 40px;
            font-weight: 900;
            color: #f9f6f2;
            flex-direction: column;
            text-shadow: 0 2px 4px rgba(0,0,0,0.2);
        }

        .win-message.active {
            display: flex;
        }

        .win-message .retry-btn {
            margin-top: 20px;
            background: #f9f6f2;
            color: #776e65;
            border: none;
            padding: 12px 30px;
            border-radius: 6px;
            font-size: 18px;
            font-weight: 700;
            cursor: pointer;
            text-shadow: none;
        }

        .controls {
            text-align: center;
            margin-top: 15px;
            color: #776e65;
            font-size: 13px;
        }

        .controls .gesture {
            display: inline-block;
            background: #eee4da;
            padding: 4px 10px;
            border-radius: 4px;
            margin: 0 3px;
            font-weight: 600;
        }

        /* ============ 管理员后台 ============ */
        .admin-page {
            display: none;
            width: 100%;
            max-width: 500px;
        }

        .admin-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            flex-wrap: wrap;
            gap: 10px;
        }

        .admin-title {
            font-size: 28px;
            font-weight: 900;
            color: #776e65;
        }

        .back-to-game-btn {
            background: #8f7a66;
            color: white;
            border: none;
            padding: 10px 16px;
            border-radius: 6px;
            font-size: 13px;
            font-weight: 700;
            cursor: pointer;
        }

        .admin-stats {
            background: white;
            border-radius: 10px;
            padding: 15px;
            margin-bottom: 15px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        }

        .admin-stats h3 {
            color: #776e65;
            margin-bottom: 10px;
            font-size: 16px;
        }

        .admin-stats .stat-row {
            display: flex;
            justify-content: space-between;
            padding: 5px 0;
            color: #8f7a66;
            font-size: 14px;
            border-bottom: 1px solid #f5f5f7;
        }

        .admin-stats .stat-row:last-child {
            border-bottom: none;
        }

        .admin-table {
            width: 100%;
            border-collapse: collapse;
            background: white;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        }

        .admin-table th {
            background: #8f7a66;
            color: white;
            padding: 10px 8px;
            font-size: 13px;
            text-align: left;
        }

        .admin-table td {
            padding: 10px 8px;
            border-bottom: 1px solid #eee;
            font-size: 13px;
            color: #776e65;
        }

        .admin-table tr:last-child td {
            border-bottom: none;
        }

        .admin-table tr:nth-child(even) {
            background: #faf8ef;
        }

        .admin-table .highlight {
            background: #fff9e6 !important;
            font-weight: 700;
        }

        .no-data {
            text-align: center;
            padding: 30px;
            color: #8f7a66;
            font-size: 16px;
        }

        .clear-data-btn {
            margin-top: 15px;
            background: #ff3b30;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 6px;
            font-size: 14px;
            font-weight: 700;
            cursor: pointer;
            width: 100%;
        }

        .back-btn {
            background: none;
            border: none;
            color: #8f7a66;
            font-size: 14px;
            cursor: pointer;
            padding: 5px;
            text-decoration: underline;
        }
    </style>
</head>
<body>
    <!-- ============ 启动页面 ============ -->
    <div class="startup-page" id="startupPage">
        <div class="startup-title">🎮 2048</div>
        <div class="startup-subtitle">特别版</div>
        <div class="hint-text">🔑 请输入暗号进入游戏</div>
        <div class="password-input-wrapper">
            <input type="text" class="password-input" id="passwordInput" placeholder="请输入暗号..." autocomplete="off">
        </div>
        <button class="enter-btn" id="enterBtn" onclick="checkPassword()">验证暗号</button>
    </div>

    <!-- ============ 登录页面 ============ -->
    <div class="login-page" id="loginPage">
        <div class="login-title">👤 身份验证</div>
        <div class="login-subtitle">
            请输入你的角色名称
        </div>
        <div class="username-input-wrapper">
            <input type="text" class="username-input" id="usernameInput" placeholder="请输入角色名称..." autocomplete="off">
        </div>
        <div class="error-message" id="errorMessage"></div>
        <button class="start-game-btn" id="startGameBtn" onclick="validateAndStart()">开始游戏</button>
        <button class="back-btn" onclick="goBackToStartup()" style="margin-top: 15px;">← 返回上一步</button>
    </div>

    <!-- ============ 游戏页面 ============ -->
    <div class="game-page" id="gamePage">
        <div class="header">
            <div>
                <div class="game-title">2048</div>
                <div class="player-info" id="playerInfo"></div>
            </div>
            <div class="scores">
                <div class="score-box">
                    <div class="score-label">分数</div>
                    <div class="score-value" id="score">0</div>
                </div>
                <div class="score-box">
                    <div class="score-label">最高</div>
                    <div class="score-value" id="best">0</div>
                </div>
            </div>
        </div>
        
        <div class="sub-header">
            <div class="description">合并数字得到 <strong>2048</strong> 方块！</div>
            <div class="btn-group">
                <button class="new-game-btn" onclick="newGame()">新游戏</button>
                <button class="logout-btn" onclick="logout()">退出</button>
                <button class="new-game-btn" id="adminBtn" style="display:none; background:#edc53f; color:#776e65;" onclick="showAdmin()">📊 管理</button>
            </div>
        </div>

        <div class="game-container" id="gameContainer">
            <div class="grid" id="grid"></div>
            <div class="game-over" id="gameOver">
                游戏结束！
                <div class="final-score" id="finalScore"></div>
                <button class="retry-btn" onclick="newGame()">再来一局</button>
            </div>
            <div class="win-message" id="winMessage">
                🎉 你赢了！
                <button class="retry-btn" onclick="continueGame()">继续游戏</button>
            </div>
        </div>

        <div class="controls">
            💡 滑动屏幕移动：<span class="gesture">⬆️</span><span class="gesture">⬇️</span><span class="gesture">⬅️</span><span class="gesture">➡️</span>
        </div>
    </div>

    <!-- ============ 管理员后台 ============ -->
    <div class="admin-page" id="adminPage">
        <div class="admin-header">
            <div class="admin-title">📊 玩家数据管理</div>
            <button class="back-to-game-btn" onclick="hideAdmin()">← 返回游戏</button>
        </div>
        <div class="admin-stats" id="adminStats"></div>
        <div id="adminContent">
            <div class="no-data">加载中...</div>
        </div>
        <button class="clear-data-btn" onclick="clearAllData()">🗑️ 清空所有数据</button>
    </div>

    <script>
        // ============ 全局状态 ============
        let currentUser = null;
        let board = Array(4).fill().map(() => Array(4).fill(0));
        let score = 0;
        let bestScore = 0;
        let gameOver = false;
        let hasWon = false;
        let keepPlaying = false;

        // 有效用户列表（隐藏，不显示给玩家）
        const validUsers = ['延青', '山楂', '小绦', '易安', '空', '小弥', '念念', '奚殇', '云尘'];

        // 所有玩家数据存储
        function getAllPlayerData() {
            const data = localStorage.getItem('game2048_players');
            return data ? JSON.parse(data) : {};
        }

        function saveAllPlayerData(data) {
            localStorage.setItem('game2048_players', JSON.stringify(data));
        }

        function getPlayerData(username) {
            const allData = getAllPlayerData();
            return allData[username] || { bestScore: 0, gamesPlayed: 0, totalScore: 0, lastPlayed: null, maxTile: 0 };
        }

        function savePlayerData(username, data) {
            const allData = getAllPlayerData();
            allData[username] = data;
            saveAllPlayerData(allData);
        }

        // ============ 启动页面逻辑 ============
        function checkPassword() {
            const input = document.getElementById('passwordInput');
            const btn = document.getElementById('enterBtn');
            const password = input.value.trim();

            if (password === '云尘是大帅哥') {
                input.classList.add('success');
                input.classList.remove('error');
                btn.disabled = true;
                btn.textContent = '✅ 验证成功...';
                
                setTimeout(() => {
                    document.getElementById('startupPage').style.display = 'none';
                    document.getElementById('loginPage').style.display = 'flex';
                    input.classList.remove('success');
                    input.value = '';
                    btn.disabled = false;
                    btn.textContent = '验证暗号';
                }, 800);
            } else {
                input.classList.add('error');
                input.classList.remove('success');
                input.value = '';
                input.placeholder = '❌ 暗号错误，请重试';
                
                setTimeout(() => {
                    input.classList.remove('error');
                    input.placeholder = '请输入暗号...';
                }, 1500);
            }
        }

        // 回车键提交暗号
        document.getElementById('passwordInput').addEventListener('keydown', function(e) {
            if (e.key === 'Enter') {
                checkPassword();
            }
        });

        // ============ 登录页面逻辑 ============
        function validateAndStart() {
            const input = document.getElementById('usernameInput');
            const errorMsg = document.getElementById('errorMessage');
            const username = input.value.trim();

            // 检查是否为空
            if (!username) {
                input.classList.add('error');
                errorMsg.textContent = '⚠️ 请输入角色名称';
                input.placeholder = '请输入角色名称...';
                setTimeout(() => input.classList.remove('error'), 1500);
                return;
            }

            // 检查是否为有效用户
            if (!validUsers.includes(username)) {
                input.classList.add('error');
                errorMsg.textContent = '❌ 无效的角色名称，请重新输入';
                input.value = '';
                input.placeholder = '请输入有效角色名称...';
                setTimeout(() => input.classList.remove('error'), 1500);
                return;
            }

            // 验证成功
            input.classList.add('success');
            errorMsg.textContent = '✅ 身份验证成功！';
            
            setTimeout(() => {
                currentUser = username;
                document.getElementById('loginPage').style.display = 'none';
                document.getElementById('gamePage').style.display = 'block';
                
                // 加载玩家数据
                const playerData = getPlayerData(currentUser);
                bestScore = playerData.bestScore || 0;
                
                // 显示玩家信息
                document.getElementById('playerInfo').textContent = `玩家: ${currentUser}`;
                
                // 显示管理按钮（仅云尘）
                if (currentUser === '云尘') {
                    document.getElementById('adminBtn').style.display = 'inline-block';
                } else {
                    document.getElementById('adminBtn').style.display = 'none';
                }
                
                // 重置输入
                input.classList.remove('success');
                input.value = '';
                errorMsg.textContent = '';
                
                initGame();
            }, 600);
        }

        // 回车键提交用户名
        document.getElementById('usernameInput').addEventListener('keydown', function(e) {
            if (e.key === 'Enter') {
                validateAndStart();
            }
        });

        // 返回启动页面
        function goBackToStartup() {
            document.getElementById('loginPage').style.display = 'none';
            document.getElementById('startupPage').style.display = 'flex';
            document.getElementById('usernameInput').value = '';
            document.getElementById('errorMessage').textContent = '';
            document.getElementById('usernameInput').classList.remove('error', 'success');
        }

        // ============ 游戏逻辑 ============
        const gridEl = document.getElementById('grid');
        const scoreEl = document.getElementById('score');
        const bestEl = document.getElementById('best');
        const gameOverEl = document.getElementById('gameOver');
        const winMessageEl = document.getElementById('winMessage');
        const finalScoreEl = document.getElementById('finalScore');

        function initGame() {
            board = Array(4).fill().map(() => Array(4).fill(0));
            score = 0;
            gameOver = false;
            hasWon = false;
            keepPlaying = false;
            
            bestEl.textContent = bestScore;
            
            addRandomTile();
            addRandomTile();
            
            updateDisplay();
            gameOverEl.classList.remove('active');
            winMessageEl.classList.remove('active');
        }

        function newGame() {
            // 保存上局数据
            if (score > 0) {
                saveCurrentGameData();
            }
            
            initGame();
        }

        function saveCurrentGameData() {
            const playerData = getPlayerData(currentUser);
            playerData.bestScore = Math.max(playerData.bestScore || 0, score, bestScore);
            playerData.gamesPlayed = (playerData.gamesPlayed || 0) + 1;
            playerData.totalScore = (playerData.totalScore || 0) + score;
            playerData.lastPlayed = new Date().toISOString();
            
            // 记录最大方块
            let maxTile = playerData.maxTile || 0;
            for (let i = 0; i < 4; i++) {
                for (let j = 0; j < 4; j++) {
                    if (board[i][j] > maxTile) {
                        maxTile = board[i][j];
                    }
                }
            }
            playerData.maxTile = maxTile;
            
            savePlayerData(currentUser, playerData);
        }

        function continueGame() {
            keepPlaying = true;
            winMessageEl.classList.remove('active');
        }

        function addRandomTile() {
            const emptyCells = [];
            for (let i = 0; i < 4; i++) {
                for (let j = 0; j < 4; j++) {
                    if (board[i][j] === 0) {
                        emptyCells.push({ i, j });
                    }
                }
            }

            if (emptyCells.length === 0) return;

            const { i, j } = emptyCells[Math.floor(Math.random() * emptyCells.length)];
            board[i][j] = Math.random() < 0.9 ? 2 : 4;
        }

        function move(direction) {
            if (gameOver) return;
            if (hasWon && !keepPlaying) return;

            let moved = false;
            const newBoard = board.map(row => [...row]);
            let scoreGain = 0;

            if (direction === 'left') {
                for (let i = 0; i < 4; i++) {
                    const result = mergeLine(newBoard[i]);
                    newBoard[i] = result.line;
                    scoreGain += result.score;
                    if (result.line.join(',') !== board[i].join(',')) moved = true;
                }
            } else if (direction === 'right') {
                for (let i = 0; i < 4; i++) {
                    const result = mergeLine([...newBoard[i]].reverse());
                    newBoard[i] = result.line.reverse();
                    scoreGain += result.score;
                    if (newBoard[i].join(',') !== board[i].join(',')) moved = true;
                }
            } else if (direction === 'up') {
                for (let j = 0; j < 4; j++) {
                    const col = [newBoard[0][j], newBoard[1][j], newBoard[2][j], newBoard[3][j]];
                    const result = mergeLine(col);
                    for (let i = 0; i < 4; i++) {
                        if (newBoard[i][j] !== result.line[i]) moved = true;
                        newBoard[i][j] = result.line[i];
                    }
                    scoreGain += result.score;
                }
            } else if (direction === 'down') {
                for (let j = 0; j < 4; j++) {
                    const col = [newBoard[3][j], newBoard[2][j], newBoard[1][j], newBoard[0][j]];
                    const result = mergeLine(col);
                    for (let i = 0; i < 4; i++) {
                        if (newBoard[3-i][j] !== result.line[i]) moved = true;
                        newBoard[3-i][j] = result.line[i];
                    }
                    scoreGain += result.score;
                }
            }

            if (moved) {
                board = newBoard;
                score += scoreGain;
                
                if (score > bestScore) {
                    bestScore = score;
                    const playerData = getPlayerData(currentUser);
                    playerData.bestScore = bestScore;
                    savePlayerData(currentUser, playerData);
                }
                
                addRandomTile();
                updateDisplay();

                if (!hasWon && !keepPlaying) {
                    for (let i = 0; i < 4; i++) {
                        for (let j = 0; j < 4; j++) {
                            if (board[i][j] === 2048) {
                                hasWon = true;
                                winMessageEl.classList.add('active');
                            }
                        }
                    }
                }

                if (isGameOver()) {
                    gameOver = true;
                    finalScoreEl.textContent = `得分: ${score}`;
                    gameOverEl.classList.add('active');
                    
                    saveCurrentGameData();
                }
            }
        }

        function mergeLine(line) {
            let filtered = line.filter(x => x !== 0);
            let score = 0;
            let newLine = [];
            let i = 0;

            while (i < filtered.length) {
                if (i + 1 < filtered.length && filtered[i] === filtered[i + 1]) {
                    const mergedValue = filtered[i] * 2;
                    newLine.push(mergedValue);
                    score += mergedValue;
                    i += 2;
                } else {
                    newLine.push(filtered[i]);
                    i++;
                }
            }

            while (newLine.length < 4) {
                newLine.push(0);
            }

            return { line: newLine, score };
        }

        function isGameOver() {
            for (let i = 0; i < 4; i++) {
                for (let j = 0; j < 4; j++) {
                    if (board[i][j] === 0) return false;
                }
            }

            for (let i = 0; i < 4; i++) {
                for (let j = 0; j < 4; j++) {
                    if (i < 3 && board[i][j] === board[i + 1][j]) return false;
                    if (j < 3 && board[i][j] === board[i][j + 1]) return false;
                }
            }

            return true;
        }

        function updateDisplay() {
            scoreEl.textContent = score;
            bestEl.textContent = bestScore;

            gridEl.innerHTML = '';
            for (let i = 0; i < 4; i++) {
                for (let j = 0; j < 4; j++) {
                    const cell = document.createElement('div');
                    cell.className = 'cell';
                    const value = board[i][j];
                    cell.textContent = value || '';
                    cell.setAttribute('data-value', value || '0');
                    gridEl.appendChild(cell);
                }
            }
        }

        // ============ 触摸和键盘事件 ============
        let touchStartX = 0;
        let touchStartY = 0;

        document.addEventListener('DOMContentLoaded', () => {
            const gameContainer = document.getElementById('gameContainer');
            
            gameContainer.addEventListener('touchstart', (e) => {
                touchStartX = e.touches[0].clientX;
                touchStartY = e.touches[0].clientY;
                e.preventDefault();
            }, { passive: false });

            gameContainer.addEventListener('touchend', (e) => {
                if (!touchStartX || !touchStartY) return;

                const touchEndX = e.changedTouches[0].clientX;
                const touchEndY = e.changedTouches[0].clientY;

                const dx = touchEndX - touchStartX;
                const dy = touchEndY - touchStartY;
                const absDx = Math.abs(dx);
                const absDy = Math.abs(dy);

                if (Math.max(absDx, absDy) < 30) return;

                if (absDx > absDy) {
                    move(dx > 0 ? 'right' : 'left');
                } else {
                    move(dy > 0 ? 'down' : 'up');
                }

                touchStartX = 0;
                touchStartY = 0;
            });

            document.addEventListener('keydown', (e) => {
                if (document.getElementById('gamePage').style.display !== 'block') return;
                switch(e.key) {
                    case 'ArrowLeft': move('left'); e.preventDefault(); break;
                    case 'ArrowRight': move('right'); e.preventDefault(); break;
                    case 'ArrowUp': move('up'); e.preventDefault(); break;
                    case 'ArrowDown': move('down'); e.preventDefault(); break;
                }
            });
        });

        // ============ 退出登录 ============
        function logout() {
            // 保存当前数据
            if (score > 0 || bestScore > 0) {
                saveCurrentGameData();
            }
            
            document.getElementById('gamePage').style.display = 'none';
            document.getElementById('adminBtn').style.display = 'none';
            document.getElementById('loginPage').style.display = 'flex';
            document.getElementById('usernameInput').value = '';
            document.getElementById('errorMessage').textContent = '';
            document.getElementById('usernameInput').classList.remove('error', 'success');
            currentUser = null;
        }

        // ============ 管理员后台 ============
        function showAdmin() {
            document.getElementById('gamePage').style.display = 'none';
            document.getElementById('adminPage').style.display = 'block';
            renderAdminPanel();
        }

        function hideAdmin() {
            document.getElementById('adminPage').style.display = 'none';
            document.getElementById('gamePage').style.display = 'block';
        }

        function renderAdminPanel() {
            const allData = getAllPlayerData();
            const users = Object.keys(allData);
            
            // 统计数据
            let totalGames = 0;
            let totalAllScore = 0;
            let highestOverall = 0;
            let highestPlayer = '';
            
            users.forEach(user => {
                const data = allData[user];
                totalGames += (data.gamesPlayed || 0);
                totalAllScore += (data.totalScore || 0);
                if ((data.bestScore || 0) > highestOverall) {
                    highestOverall = data.bestScore || 0;
                    highestPlayer = user;
                }
            });
            
            document.getElementById('adminStats').innerHTML = `
                <h3>📈 总体统计</h3>
                <div class="stat-row"><span>总玩家数</span><span>${users.length} 人</span></div>
                <div class="stat-row"><span>总局数</span><span>${totalGames} 局</span></div>
                <div class="stat-row"><span>总分合计</span><span>${totalAllScore.toLocaleString()} 分</span></div>
                <div class="stat-row"><span>最高纪录</span><span>${highestPlayer}: ${highestOverall.toLocaleString()} 分</span></div>
            `;
            
            // 玩家列表
            if (users.length === 0) {
                document.getElementById('adminContent').innerHTML = '<div class="no-data">暂无玩家数据</div>';
                return;
            }

            let html = '<table class="admin-table">';
            html += '<thead><tr><th>玩家</th><th>最高分</th><th>最大方块</th><th>总局数</th><th>总分</th><th>最后游戏</th></tr></thead>';
            html += '<tbody>';
            
            // 按最高分排序
            users.sort((a, b) => (allData[b].bestScore || 0) - (allData[a].bestScore || 0));
            
            users.forEach(user => {
                const data = allData[user];
                const lastPlayed = data.lastPlayed ? new Date(data.lastPlayed).toLocaleString('zh-CN', {month:'short', day:'numeric', hour:'2-digit', minute:'2-digit'}) : '暂无';
                const isCurrentUser = user === currentUser;
                html += `<tr class="${isCurrentUser ? 'highlight' : ''}">
                    <td><strong>${user}</strong>${isCurrentUser ? ' 👈' : ''}</td>
                    <td>${(data.bestScore || 0).toLocaleString()}</td>
                    <td>${data.maxTile || '-'}</td>
                    <td>${data.gamesPlayed || 0}</td>
                    <td>${(data.totalScore || 0).toLocaleString()}</td>
                    <td>${lastPlayed}</td>
                </tr>`;
            });
            
            html += '</tbody></table>';
            document.getElementById('adminContent').innerHTML = html;
        }

        function clearAllData() {
            if (confirm('⚠️ 确定要清空所有玩家的游戏数据吗？\n\n此操作不可恢复！')) {
                localStorage.removeItem('game2048_players');
                renderAdminPanel();
                alert('✅ 所有数据已清空');
            }
        }
    </script>
</body>
</html>
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>下班倒计时</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'PingFang SC', 'Microsoft YaHei', sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 20px;
            color: #fff;
        }
        
        .container {
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            width: 100%;
            max-width: 450px;
            text-align: center;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        
        h1 {
            font-size: 28px;
            margin-bottom: 10px;
            text-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
        }
        
        .current-time {
            font-size: 20px;
            margin-bottom: 15px;
            padding: 10px;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 10px;
            display: inline-block;
        }
        
        .target-time {
            font-size: 18px;
            margin-bottom: 30px;
            opacity: 0.9;
        }
        
        .countdown {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-bottom: 30px;
        }
        
        .time-unit {
            display:极 flex;
            flex-direction: column;
            align-items: center;
        }
        
        .time-value {
            background: rgba(255, 255, 255, 0.2);
            border-radius: 10px;
            padding: 15px;
            min-width: 80px;
            font-size: 42px;
            font-weight: bold;
            margin-bottom: 5px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }
        
        .time-label {
            font-size: 14px;
            opacity: 0.8;
        }
        
        .message {
            font-size: 20px;
            margin-top: 20px;
            padding: 15px;
            border-radius: 12px;
            background: rgba(255, 255, 255, 0.2);
            transition: all 0.3s ease;
        }
        
        .progress-container {
            margin: 25px 0;
        }
        
        .progress-info {
            display: flex;
            justify-content: space-between;
            margin-bottom: 8px;
            font-size: 14px;
        }
        
        .progress-percentage {
            font-size: 16px;
            font-weight: bold;
            margin-top: 8px;
            text-align: center;
        }
        
        .progress-bar {
            height: 10px;
            width: 100%;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 5px;
            overflow: hidden;
        }
        
        .progress {
            height: 100%;
            background: linear-gradient(90deg, #43e97b 0%, #38f9d7 100%);
            border-radius: 5px;
            transition: width 0.5s ease;
        }
        
        .celebrate {
            font-size: 50px;
            margin-top: 20px;
            display: none;
        }
        
        .add-to-chat {
            margin-top: 20px;
            padding: 10px 20px;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .add-to-chat:hover {
            background: rgba(255, 255, 255, 0.3);
        }
        
        .settings {
            margin-top: 20px;
            padding: 15px;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 12px;
        }
        
        .settings h3 {
            margin-bottom: 10px;
        }
        
        .settings-row {
            display: flex;
            align-items: center;
            margin-bottom: 10px;
        }
        
        .settings-row label {
            width: 120px;
            text-align: right;
            margin-right: 10px;
        }
        
        .settings-row input {
            padding: 8px;
            width: 80px;
            border-radius: 4px;
            border: 1px solid rgba(255, 255, 255, 0.3);
            background: rgba(255, 255, 255, 0.1);
            color: white;
        }
        
        .settings-row button {
            padding: 8px 15px;
            background: rgba(255, 255, 255, 0.3);
            border: none;
            border-radius: 4px;
            color: white;
            cursor: pointer;
        }
        
        .deploy-instructions {
            margin-top: 30px;
            padding: 20px;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 12px;
            font-size: 16px;
            text-align: left;
        }
        
        .deploy-instructions h3 {
            margin-bottom: 10px;
            text-align: center;
        }
        
        .deploy-instructions ol {
            padding-left: 20px;
            margin-bottom: 15px;
        }
        
        .deploy-instructions li {
            margin-bottom: 8px;
        }
        
        .deploy-buttons {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-top: 15px;
        }
        
        .deploy-button {
            padding: 10px 20px;
            background: rgba(255, 255, 255, 0.3);
            border-radius: 8px;
            text-decoration: none;
            color: white;
            font-weight: bold;
            transition: all 0.3s;
        }
        
        .deploy-button:hover {
            background: rgba(255, 255, 255, 0.4);
            transform: translateY(-2px);
        }
        
        @media (max-width: 480px) {
            .container {
                padding: 20px;
            }
            
            .time-value {
                font-size: 32px;
                min-width: 60px;
                padding: 12px;
            }
            
            h1 {
                font-size: 24px;
            }
            
            .current-time {
                font-size: 18px;
            }
            
            .settings-row {
                flex-direction: column;
                align-items: flex-start;
            }
            
            .settings-row label {
                text-align: left;
                margin-bottom: 5px;
            }
            
            .deploy-buttons {
                flex-direction: column;
                gap: 10px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1 id="countdown-title">距离下午5:30还有</h1>
        
        <div class="current-time" id="current-time">当前时间：加载中...</div>
        
        <div class="target-time" id="target-time-display">目标时间：今天 17:30:00</div>
        
        <div class="countdown">
            <div class="time-unit">
                <div class="time-value" id="hours">00</div>
                <div class="time-label">小时</div>
            </div>
            <div class="time-unit">
                <div class="time-value" id="minutes">00</div>
                <div class="time-label">分钟</div>
            </div>
            <div class="time-unit">
                <div class="time-value" id="seconds">00</div>
                <div class="time-label">秒</div>
            </div>
        </div>
        
        <div class="progress-container">
            <div class="progress-info">
                <span id="progress-start-time">8:30</span>
                <span>今日工作进度</span>
                <span id="progress-end-time">17:30</span>
            </div>
            <div class="progress-bar">
                <div class="progress" id="progress"></div>
            </div>
            <div class="progress-percentage" id="progress-percentage">0%</div>
        </div>
        
        <div class="message" id="message">加油，工作即将结束！</div>
        
        <div class="celebrate" id="celebrate">🎉 🎊 🎉</div>
        
        <div class="add-to-chat" id="add-to-chat">添加到微信聊天</div>
        
        <div class="settings">
            <h3>自定义设置</h3>
            <div class="settings-row">
                <label for="target-hour">目标时间 (时):</label>
                <input type="number" id="target-hour" min="0" max="23" value="17">
            </div>
            <div class="settings-row">
                <label for="target-minute">目标时间 (分):</label>
                <input type="number" id="target-minute" min="0" max="59" value="30">
            </div>
            <div class="settings-row">
                <label for="start-hour">开始时间 (时):</label>
                <input type="number" id="start-hour" min="0" max="23" value="8">
            </div>
            <div class="settings-row">
                <label for="start-minute">开始时间 (分):</label>
                <input type="number" id="start-minute" min="0" max="59" value="30">
            </div>
            <div class="settings-row">
                <button id="save-settings">保存设置</button>
            </div>
        </div>
        
        <div class="deploy-instructions">
            <h3>部署到免费托管服务</h3>
            <ol>
                <li>将本页保存为HTML文件（右键 > 另存为）</li>
                <li>选择以下任一方式部署：</li>
            </ol>
            <div class="deploy-buttons">
                <a href="https://github.com/" class="deploy-button" target="_blank">部署到 GitHub Pages</a>
                <a href="https://app.netlify.com/" class="deploy-button" target="_blank">部署到 Netlify</a>
            </div>
        </div>
    </div>

    <script>
        // 默认设置
        let targetHour = 17;
        let targetMinute = 30;
        let startHour = 8;
        let startMinute = 30;
        
        // 从本地存储加载设置
        function loadSettings() {
            const savedSettings = localStorage.getItem('countdownSettings');
            if (savedSettings) {
                const settings = JSON.parse(savedSettings);
                targetHour = settings.targetHour;
                targetMinute = settings.targetMinute;
                startHour = settings.startHour;
                startMinute = settings.startMinute;
                
                // 更新输入框
                document.getElementById('target-hour').value = targetHour;
                document.getElementById('target-minute').value = targetMinute;
                document.getElementById('start-hour').value = startHour;
                document.getElementById('start-minute').value = startMinute;
            }
        }
        
        // 保存设置到本地存储
        function saveSettings() {
            const settings = {
                targetHour: parseInt(document.getElementById('target-hour').value),
                targetMinute: parseInt(document.getElementById('target-minute').value),
                startHour: parseInt(document.getElementById('start-hour').value),
                startMinute: parseInt(document.getElementById('start-minute').value)
            };
            
            localStorage.setItem('countdownSettings', JSON.stringify(settings));
            alert('设置已保存！');
            updateCountdown();
        }
        
        function updateCurrentTime() {
            const now = new Date();
            const hours = now.getHours().toString().padStart(2, '0');
            const minutes = now.getMinutes().toString().padStart(2, '0');
            const seconds = now.getSeconds().toString().padStart(2, '0');
            
            document.getElementById('current-time').textContent = `当前时间：${hours}:${minutes}:${seconds}`;
        }
        
        function updateCountdown() {
            const now = new Date();
            const target = new Date();
            
            // 设置目标时间
            target.setHours(targetHour, targetMinute, 0, 0);
            
            // 如果当前时间已超过目标时间，目标设为明天
            if (now > target) {
                target.setDate(target.getDate() + 1);
            }
            
            // 计算时间差（毫秒）
            const diff = target - now;
            
            // 计算小时、分钟和秒
            const hours = Math.floor(diff / (1000 * 60 * 60));
            const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
            const seconds = Math.floor((diff % (1000 * 60)) / 1000);
            
            // 更新倒计时数字
            document.getElementById('hours').textContent = hours.toString().padStart(2, '0');
            document.getElementById('minutes').textContent = minutes.toString().padStart(2, '0');
            document.getElementById('seconds').textContent = seconds.toString().padStart(2, '0');
            
            // 处理上午/下午显示
            let period = targetHour >= 12 ? '下午' : '上午';
            let displayHour = targetHour > 12 ? targetHour - 12 : targetHour;
            if (displayHour === 0) displayHour = 12; // 0点显示为12
            
            // 更新标题和目标时间显示
            document.getElementById('countdown-title').textContent = `距离${period}${displayHour}:${targetMinute.toString().padStart(2, '0')}还有`;
            document.getElementById('target-time-display').textContent = `目标时间：今天 ${targetHour.toString().padStart(2, '0')}:${targetMinute.toString().padStart(2, '0')}:00`;
            document.getElementById('progress-end-time').textContent = `${targetHour.toString().padStart(2, '0')}:${targetMinute.toString().padStart(2, '0')}`;
            document.getElementById('progress-start-time').textContent = `${startHour.toString().padStart(2, '0')}:${startMinute.toString().padStart(2, '0')}`;
            
            // 更新进度条（从设置开始时间到目标时间）
            const workStart = new Date();
            workStart.setHours(startHour, startMinute, 0, 0);
            
            let progressPercent;
            if (now < workStart) {
                progressPercent = 0; // 早于开始时间，进度0%
            } else if (now > target) {
                progressPercent = 100; // 晚于目标时间，进度100%
            } else {
                const totalWorkTime = target - workStart;
                const timePassed = now - workStart;
                progressPercent = (timePassed / totalWorkTime) * 100;
            }
            
            // 更新进度条和百分比
            document.getElementById('progress').style.width = progressPercent + '%';
            document.getElementById('progress-percentage').textContent = `${progressPercent.toFixed(1)}%`;
            
            // 更新鼓励消息
            const message = document.getElementById('message');
            const celebrate = document.getElementById('celebrate');
            
            if (diff < 0) {
                message.textContent = "时间到！享受您的闲暇时光！";
                celebrate.style.display = "block";
            } else if (hours === 0 && minutes < 30) {
                message.textContent = "快到了，再坚持一下！";
            } else if (hours === 0) {
                message.textContent = "不到一小时了，你可以的！";
            } else if (hours < 3) {
                message.textContent = "加油，工作即将结束！";
            } else if (progressPercent < 20) {
                message.textContent = "新的一天刚刚开始，保持活力！";
            } else if (progressPercent < 50) {
                message.textContent = "上午时光，高效工作的好时机！";
            } else if (progressPercent < 70) {
                message.textContent = "午后时分，保持节奏！";
            } else {
                message.textContent = "胜利在望，坚持就是胜利！";
            }
        }
        
        function updateAll() {
            updateCurrentTime();
            updateCountdown();
        }
        
        // 初始加载设置
        loadSettings();
        
        // 初始更新
        updateAll();
        
        // 每秒更新一次
        setInterval(updateAll, 1000);
        
        // 添加到微信聊天功能
        document.getElementById('add-to-chat').addEventListener('click', function() {
            alert('在微信中，点击右上角菜单，选择"添加到聊天"即可在聊天界面快速访问此倒计时工具');
        });
        
        // 保存设置按钮
        document.getElementById('save-settings').addEventListener('click', saveSettings);
    </script>
</body>
</html>

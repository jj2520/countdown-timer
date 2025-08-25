<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>倒计时工具部署指南</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'PingFang SC', 'Microsoft YaHei', sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #1a2a6c, #b21f1f, #fdbb2d);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
            color: #fff;
        }
        
        .header {
            text-align: center;
            margin: 30px 0;
            width: 100%;
            max-width: 800px;
        }
        
        h1 {
            font-size: 42px;
            margin-bottom: 20px;
            text-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
        }
        
        .subtitle {
            font-size: 22px;
            margin-bottom: 40px;
            opacity: 0.9;
        }
        
        .container {
            display: flex;
            flex-wrap: wrap;
            gap: 30px;
            justify-content: center;
            width: 100%;
            max-width: 1200px;
        }
        
        .card {
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            width: 100%;
            max-width: 550px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        
        .card-title {
            font-size: 28px;
            margin-bottom: 20px;
            text-align: center;
            color: #ffcc00;
        }
        
        .step {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 20px;
            transition: all 0.3s ease;
        }
        
        .step:hover {
            background: rgba(255, 255, 255, 0.2);
            transform: translateY(-5px);
        }
        
        .step-number {
            display: inline-block;
            width: 30px;
            height: 30px;
            background: #ff6b6b;
            border-radius: 50%;
            text-align: center;
            line-height: 30px;
            margin-right: 10px;
            font-weight: bold;
        }
        
        .step-title {
            font-size: 20px;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
        }
        
        .step-content {
            padding-left: 40px;
            font-size: 16px;
            line-height: 1.6;
        }
        
        .step-content p {
            margin-bottom: 10px;
        }
        
        .screenshot {
            width: 100%;
            border-radius: 10px;
            margin: 15px 0;
            border: 1px solid rgba(255, 255, 255, 0.3);
        }
        
        .button-container {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 30px;
        }
        
        .deploy-button {
            padding: 15px 30px;
            background: linear-gradient(45deg, #6a11cb, #2575fc);
            border-radius: 50px;
            text-decoration: none;
            color: white;
            font-weight: bold;
            font-size: 18px;
            display: flex;
            align-items: center;
            gap: 10px;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }
        
        .deploy-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
        }
        
        .github { background: linear-gradient(45deg, #24292e, #3f4448); }
        .netlify { background: linear-gradient(45deg, #00c7b7, #00d4c8); }
        
        .icon {
            font-size: 24px;
        }
        
        .countdown-preview {
            text-align: center;
            margin-top: 30px;
            padding: 20px;
            background: rgba(0, 0, 0, 0.2);
            border-radius: 15px;
        }
        
        .preview-title {
            font-size: 24px;
            margin-bottom: 15px;
            color: #ffcc00;
        }
        
        .timer {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin: 20px 0;
        }
        
        .timer-unit {
            background: rgba(255, 255, 255, 0.2);
            border-radius: 10px;
            padding: 15px;
            min-width: 80px;
        }
        
        .timer-value {
            font-size: 36px;
            font-weight: bold;
        }
        
        .timer-label {
            font-size: 14px;
            opacity: 0.8;
        }
        
        .progress-bar {
            height: 10px;
            width: 100%;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 5px;
            overflow: hidden;
            margin: 20px 0;
        }
        
        .progress {
            height: 100%;
            background: linear-gradient(90deg, #43e97b, #38f9d7);
            border-radius: 5px;
            width: 65%;
        }
        
        .footer {
            margin-top: 50px;
            text-align: center;
            font-size: 16px;
            opacity: 0.8;
        }
        
        @media (max-width: 768px) {
            .container {
                flex-direction: column;
                align-items: center;
            }
            
            .card {
                width: 100%;
            }
            
            .button-container {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <div class="header">
        <h1>倒计时工具部署指南</h1>
        <p class="subtitle">轻松部署到GitHub Pages和Netlify</p>
    </div>
    
    <div class="container">
        <!-- GitHub Pages 部署指南 -->
        <div class="card">
            <h2 class="card-title">部署到 GitHub Pages</h2>
            
            <div class="step">
                <div class="step-title">
                    <span class="step-number">1</span>
                    <h3>创建GitHub仓库</h3>
                </div>
                <div class="step-content">
                    <p>• 登录您的GitHub账户</p>
                    <p>• 点击右上角的 "+" 图标，选择 "New repository"</p>
                    <p>• 输入仓库名称（例如：countdown-timer）</p>
                    <p>• 选择 "Public"（公开）</p>
                    <p>• 勾选 "Add a README file"</p>
                    <p>• 点击 "Create repository"</p>
                    <img src="https://docs.github.com/assets/cb-11427/images/help/repository/repo-create.png" alt="创建GitHub仓库" class="screenshot">
                </div>
            </div>
            
            <div class="step">
                <div class="step-title">
                    <span class="step-number">2</span>
                    <h3>上传HTML文件</h3>
                </div>
                <div class="step-content">
                    <p>• 在仓库页面，点击 "Add file" > "Upload files"</p>
                    <p>• 将您的HTML文件拖拽到上传区域</p>
                    <p>• 添加commit信息（例如："添加倒计时工具"）</p>
                    <p>• 点击 "Commit changes"</p>
                    <img src="https://docs.github.com/assets/cb-11427/images/help/repository/upload-files-button.png" alt="上传文件" class="screenshot">
                </div>
            </div>
            
            <div class="step">
                <div class="step-title">
                    <span class="step-number">3</span>
                    <h3>启用GitHub Pages</h3>
                </div>
                <div class="step-content">
                    <p>• 在仓库页面，点击 "Settings"</p>
                    <p>• 在左侧菜单中，选择 "Pages"</p>
                    <p>• 在 "Source" 部分，选择 "Deploy from a branch"</p>
                    <p>• 在 "Branch" 下拉菜单中，选择 "main" 分支和 "/ (root)" 文件夹</p>
                    <p>• 点击 "Save"</p>
                    <p>• 等待几分钟，页面会显示您的网站URL</p>
                    <img src="https://docs.github.com/assets/cb-11427/images/help/pages/select-source.png" alt="启用GitHub Pages" class="screenshot">
                </div>
            </div>
            
            <div class="step">
                <div class="step-title">
                    <span class="step-number">4</span>
                    <h3>访问您的网站</h3>
                </div>
                <div class="step-content">
                    <p>• 您的网站URL格式为：https://&lt;username&gt;.github.io/&lt;repository-name&gt;</p>
                    <p>• 例如：https://johnsmith.github.io/countdown-timer</p>
                    <p>• 将此URL分享给他人即可访问您的倒计时工具</p>
                </div>
            </div>
        </div>
        
        <!-- Netlify 部署指南 -->
        <div class="card">
            <h2 class="card-title">部署到 Netlify</h2>
            
            <div class="step">
                <div class="step-title">
                    <span class="step-number">1</span>
                    <h3>创建Netlify账户</h3>
                </div>
                <div class="step-content">
                    <p>• 访问 <a href="https://app.netlify.com/" style="color: #00d4c8; text-decoration: none;">https://app.netlify.com</a></p>
                    <p>• 点击 "Sign up" 注册账户</p>
                    <p>• 推荐使用GitHub账户登录（更方便后续操作）</p>
                    <img src="https://www.netlify.com/img/deploy/button.svg" alt="Netlify登录" class="screenshot">
                </div>
            </div>
            
            <div class="step">
                <div class="step-title">
                    <span class="step-number">2</span>
                    <h3>部署您的网站</h3>
                </div>
                <div class="step-content">
                    <p>• 登录后，点击 "Add new site" > "Deploy manually"</p>
                    <p>• 将您的HTML文件拖拽到上传区域</p>
                    <p>• Netlify会自动部署您的网站</p>
                    <p>• 部署完成后，您会获得一个随机子域的URL</p>
                    <img src="https://www.netlify.com/img/docs/netlify-drop-example.png" alt="Netlify部署" class="screenshot">
                </div>
            </div>
            
            <div class="step">
                <div class="step-title">
                    <span class="step-number">3</span>
                    <h3>自定义域名（可选）</h3>
                </div>
                <div class="step-content">
                    <p>• 在站点设置中，点击 "Domain settings"</p>
                    <p>• 点击 "Add custom domain"</p>
                    <p>• 输入您自己的域名</p>
                    <p>• 按照说明配置DNS记录</p>
                    <img src="https://www.netlify.com/img/docs/custom-domains.png" alt="自定义域名" class="screenshot">
                </div>
            </div>
            
            <div class="step">
                <div class="step-title">
                    <span class="step-number">4</span>
                    <h3>访问您的网站</h3>
                </div>
                <div class="step-content">
                    <p>• 您的网站URL格式为：https://&lt;random-name&gt;.netlify.app</p>
                    <p>• 例如：https://amazing-timer.netlify.app</p>
                    <p>• 将此URL分享给他人即可访问您的倒计时工具</p>
                </div>
            </div>
        </div>
    </div>
    
    <div class="countdown-preview">
        <h3 class="preview-title">倒计时工具预览</h3>
        <div class="timer">
            <div class="timer-unit">
                <div class="timer-value">05</div>
                <div class="timer-label">小时</div>
            </div>
            <div class="timer-unit">
                <div class="timer-value">30</div>
                <div class="timer-label">分钟</div>
            </div>
            <div class="timer-unit">
                <div class="timer-value">15</div>
                <div class="timer-label">秒</div>
            </div>
        </div>
        <div class="progress-bar">
            <div class="progress"></div>
        </div>
        <p>今日工作进度：65%</p>
    </div>
    
    <div class="button-container">
        <a href="https://github.com/" class="deploy-button github">
            <span class="icon">🚀</span>
            部署到 GitHub Pages
        </a>
        <a href="https://app.netlify.com/" class="deploy-button netlify">
            <span class="icon">✨</span>
            部署到 Netlify
        </a>
    </div>
    
    <div class="footer">
        <p>© 2023 倒计时工具部署指南 | 免费静态网站托管服务</p>
    </div>
</body>
</html>

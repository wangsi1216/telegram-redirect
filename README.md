<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Telegram频道轮转</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script>
        // Telegram链接数组 - 替换成你自己的
        const telegramLinks = [
            "https://t.me/laiya88801",
            "https://t.me/laiya88802",
            "https://t.me/laiya88803"
        ];
        
        // 确保随机但不完全随机（避免连续点击跳转同一链接）
        function getRandomLink() {
            const lastClicked = localStorage.getItem('lastClickedLink');
            let availableLinks = telegramLinks;
            
            // 如果上次点击过，尝试避免立即重复（除非只有一个链接）
            if (lastClicked && telegramLinks.length > 1) {
                availableLinks = telegramLinks.filter(link => link !== lastClicked);
            }
            
            const randomIndex = Math.floor(Math.random() * availableLinks.length);
            const selectedLink = availableLinks[randomIndex];
            
            // 记录本次点击
            localStorage.setItem('lastClickedLink', selectedLink);
            
            return selectedLink;
        }
        
        // 立即跳转
        window.location.href = getRandomLink();
    </script>
    
    <style>
        /* 备用样式，如果跳转失败则显示 */
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 20px;
        }
        .spinner {
            border: 4px solid rgba(255,255,255,0.3);
            border-radius: 50%;
            border-top: 4px solid white;
            width: 40px;
            height: 40px;
            animation: spin 1s linear infinite;
            margin: 20px 0;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        .manual-link {
            margin-top: 30px;
            padding: 15px 30px;
            background: white;
            color: #667eea;
            border-radius: 50px;
            text-decoration: none;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
        }
        .manual-link:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(0,0,0,0.25);
        }
    </style>
</head>
<body>
    <div id="fallback" style="display: none;">
        <h1>إعادة التوجيه إلىTelegram...</h1>
        <div class="spinner"></div>
        <p>إذا لم تتم إعادة توجيه الصفحة بعد فترة طويلة، يرجى النقر على الزر أدناه:</p>
        <a href="#" id="manualRedirect" class="manual-link">القفز اليدوي</a>
        <p style="margin-top: 30px; font-size: 14px; opacity: 0.8;">
            كل نقرة على هذا الرابط ستعيد توجيهك عشوائياً إلى قناة Telegram مختلفة.
        </p>
    </div>
    
    <script>
        // إذا فشل تحميل الصفحة في غضون 3 ثوانٍ، فاعرض واجهة بديلة.
        setTimeout(() => {
            if (!window.location.href.includes('t.me')) {
                document.getElementById('fallback').style.display = 'block';
                document.getElementById('manualRedirect').href = getRandomLink();
            }
        }, 3000);
    </script>
</body>
</html>

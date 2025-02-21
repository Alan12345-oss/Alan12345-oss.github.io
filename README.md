<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>個人履歷 | Netflix 風格</title>
    <style>
        :root {
            --netflix-red: #e50914;
            --netflix-black: #141414;
            --netflix-dark-gray: #181818;
            --netflix-medium-gray: #2f2f2f;
            --netflix-light-gray: #808080;
            --netflix-white: #ffffff;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Helvetica Neue', Arial, sans-serif;
        }
        
        body {
            background-color: var(--netflix-black);
            color: var(--netflix-white);
            overflow-x: hidden;
        }
        
        /* 導航欄樣式 */
        .navbar {
            position: fixed;
            top: 0;
            width: 100%;
            padding: 20px 40px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: linear-gradient(to bottom, rgba(0,0,0,0.7) 10%, transparent);
            transition: background-color 0.3s ease;
            z-index: 1000;
        }
        
        .navbar.scrolled {
            background-color: var(--netflix-black);
        }
        
        .logo {
            color: var(--netflix-red);
            font-weight: bold;
            font-size: 28px;
            text-decoration: none;
            letter-spacing: 1px;
        }
        
        .nav-links {
            display: flex;
            list-style: none;
        }
        
        .nav-links li {
            margin-left: 25px;
        }
        
        .nav-links a {
            color: var(--netflix-white);
            text-decoration: none;
            font-size: 14px;
            transition: color 0.3s ease;
        }
        
        .nav-links a:hover {
            color: var(--netflix-light-gray);
        }
        
        /* 主橫幅區域 */
        .hero {
            height: 90vh;
            width: 100%;
            background: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.7)), 
                        url('/api/placeholder/1920/1080') no-repeat center center/cover;
            display: flex;
            flex-direction: column;
            justify-content: center;
            padding: 0 50px;
        }
        
        .hero-content {
            max-width: 640px;
            margin-top: 60px;
        }
        
        .hero-title {
            font-size: 48px;
            font-weight: bold;
            margin-bottom: 20px;
        }
        
        .hero-subtitle {
            font-size: 24px;
            margin-bottom: 20px;
            color: #ddd;
        }
        
        .hero-description {
            font-size: 18px;
            margin-bottom: 30px;
            line-height: 1.5;
        }
        
        .cta-btn {
            background-color: var(--netflix-red);
            color: white;
            border: none;
            padding: 12px 24px;
            font-size: 16px;
            font-weight: bold;
            border-radius: 4px;
            cursor: pointer;
            transition: all 0.2s ease;
        }
        
        .cta-btn:hover {
            background-color: #f40612;
            transform: scale(1.05);
        }
        
        /* 內容區塊標題 */
        .section-title {
            font-size: 22px;
            font-weight: 500;
            margin: 50px 0 15px 50px;
        }
        
        /* 滑動行列 */
        .slider-container {
            position: relative;
            padding: 0 50px;
            margin-bottom: 40px;
        }
        
        .slider-row {
            display: flex;
            overflow-x: auto;
            padding: 20px 0;
            scroll-behavior: smooth;
            scrollbar-width: none; /* Firefox */
        }
        
        .slider-row::-webkit-scrollbar {
            display: none; /* Chrome, Safari, Opera */
        }
        
        /* 卡片項目 */
        .card {
            min-width: 280px;
            height: 160px;
            margin-right: 10px;
            border-radius: 4px;
            overflow: hidden;
            position: relative;
            transition: all 0.3s ease;
            cursor: pointer;
        }
        
        .card:hover {
            transform: scale(1.08);
            z-index: 10;
        }
        
        .card img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        
        .card-overlay {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            background: linear-gradient(transparent, rgba(0,0,0,0.9));
            padding: 15px;
            opacity: 0;
            transition: opacity 0.3s ease;
        }
        
        .card:hover .card-overlay {
            opacity: 1;
        }
        
        .card-title {
            font-size: 16px;
            font-weight: bold;
            margin-bottom: 5px;
        }
        
        .card-info {
            font-size: 14px;
            color: #ddd;
        }
        
        /* 關於區塊 */
        .about-section {
            display: flex;
            padding: 60px 50px;
            background-color: var(--netflix-dark-gray);
        }
        
        .about-image {
            flex: 0 0 40%;
            max-width: 400px;
            border-radius: 4px;
            overflow: hidden;
            box-shadow: 0 10px 20px rgba(0,0,0,0.3);
        }
        
        .about-image img {
            width: 100%;
            height: auto;
            object-fit: cover;
        }
        
        .about-content {
            flex: 1;
            padding-left: 50px;
        }
        
        .about-content h2 {
            font-size: 32px;
            margin-bottom: 20px;
        }
        
        .about-content p {
            font-size: 16px;
            line-height: 1.6;
            margin-bottom: 20px;
            color: #ddd;
        }
        
        /* 技能區塊 */
        .skills-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 20px;
            padding: 0 50px 50px;
        }
        
        .skill-card {
            background-color: var(--netflix-medium-gray);
            border-radius: 4px;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            transition: transform 0.2s ease, background-color 0.2s ease;
        }
        
        .skill-card:hover {
            transform: translateY(-5px);
            background-color: #3a3a3a;
        }
        
        .skill-icon {
            font-size: 32px;
            margin-bottom: 15px;
            color: var(--netflix-red);
        }
        
        .skill-name {
            font-size: 18px;
            font-weight: 500;
        }
        
        .skill-level {
            width: 100%;
            height: 6px;
            background-color: #444;
            border-radius: 3px;
            margin-top: 15px;
            overflow: hidden;
        }
        
        .skill-progress {
            height: 100%;
            background-color: var(--netflix-red);
            border-radius: 3px;
        }
        
        /* 聯絡表單 */
        .contact-section {
            background-color: var(--netflix-dark-gray);
            padding: 60px 50px;
        }
        
        .contact-section h2 {
            text-align: center;
            font-size: 32px;
            margin-bottom: 40px;
        }
        
        .contact-form {
            max-width: 600px;
            margin: 0 auto;
        }
        
        .form-group {
            margin-bottom: 25px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-size: 16px;
        }
        
        .form-group input,
        .form-group textarea {
            width: 100%;
            padding: 12px 15px;
            background-color: #333;
            border: 1px solid #444;
            border-radius: 4px;
            color: white;
            font-size: 16px;
        }
        
        .form-group input:focus,
        .form-group textarea:focus {
            outline: none;
            border-color: var(--netflix-red);
        }
        
        .form-group textarea {
            min-height: 150px;
            resize: vertical;
        }
        
        .submit-btn {
            background-color: var(--netflix-red);
            color: white;
            border: none;
            padding: 14px 28px;
            font-size: 16px;
            font-weight: bold;
            border-radius: 4px;
            cursor: pointer;
            transition: background-color 0.2s ease;
            display: block;
            margin: 0 auto;
        }
        
        .submit-btn:hover {
            background-color: #f40612;
        }
        
        /* 頁腳 */
        .footer {
            background-color: var(--netflix-black);
            padding: 40px 50px;
            text-align: center;
        }
        
        .social-links {
            display: flex;
            justify-content: center;
            margin-bottom: 30px;
        }
        
        .social-link {
            display: inline-flex;
            justify-content: center;
            align-items: center;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background-color: var(--netflix-medium-gray);
            color: var(--netflix-white);
            margin: 0 10px;
            text-decoration: none;
            transition: all 0.2s ease;
        }
        
        .social-link:hover {
            background-color: var(--netflix-red);
            transform: translateY(-3px);
        }
        
        .copyright {
            color: var(--netflix-light-gray);
            font-size: 14px;
        }
        
        /* 響應式設計 */
        @media (max-width: 992px) {
            .about-section {
                flex-direction: column;
            }
            
            .about-image {
                max-width: 100%;
                margin-bottom: 30px;
            }
            
            .about-content {
                padding-left: 0;
            }
        }
        
        @media (max-width: 768px) {
            .navbar {
                padding: 15px 20px;
            }
            
            .hero {
                padding: 0 20px;
            }
            
            .hero-title {
                font-size: 36px;
            }
            
            .hero-subtitle {
                font-size: 20px;
            }
            
            .section-title {
                margin-left: 20px;
            }
            
            .slider-container {
                padding: 0 20px;
            }
            
            .about-section,
            .contact-section {
                padding: 40px 20px;
            }
            
            .skills-grid {
                padding: 0 20px 40px;
            }
        }
        
        @media (max-width: 576px) {
            .nav-links li {
                margin-left: 15px;
            }
            
            .hero-title {
                font-size: 28px;
            }
            
            .card {
                min-width: 220px;
                height: 130px;
            }
        }
    </style>
</head>
<body>
    <!-- 導航欄 -->
    <nav class="navbar">
        <a href="#" class="logo">Portfolio</a>
        <ul class="nav-links">
            <li><a href="#home">首頁</a></li>
            <li><a href="#projects">作品集</a></li>
            <li><a href="#about">關於我</a></li>
            <li><a href="#skills">技能</a></li>
            <li><a href="#experience">經歷</a></li>
            <li><a href="#contact">聯絡</a></li>
        </ul>
    </nav>
    
    <!-- 主橫幅區域 -->
    <section class="hero" id="home">
        <div class="hero-content">
            <h1 class="hero-title">您的名字</h1>
            <h2 class="hero-subtitle">您的專業頭銜</h2>
            <p class="hero-description">在這裡放置一段簡短的自我介紹，描述您的專業背景、核心能力和價值主張。讓訪客一眼就能了解您是誰以及您能提供什麼。</p>
            <button class="cta-btn">查看作品集</button>
        </div>
    </section>
    
    <!-- 作品集區域 -->
    <h2 class="section-title" id="projects">精選作品</h2>
    <div class="slider-container">
        <div class="slider-row">
            <div class="card">
                <img src="/api/placeholder/280/160" alt="作品一">
                <div class="card-overlay">
                    <h3 class="card-title">作品名稱一</h3>
                    <p class="card-info">簡短描述這個專案的重點和使用技術</p>
                </div>
            </div>
            <div class="card">
                <img src="/api/placeholder/280/160" alt="作品二">
                <div class="card-overlay">
                    <h3 class="card-title">作品名稱二</h3>
                    <p class="card-info">簡短描述這個專案的重點和使用技術</p>
                </div>
            </div>
            <div class="card">
                <img src="/api/placeholder/280/160" alt="作品三">
                <div class="card-overlay">
                    <h3 class="card-title">作品名稱三</h3>
                    <p class="card-info">簡短描述這個專案的重點和使用技術</p>
                </div>
            </div>
            <div class="card">
                <img src="/api/placeholder/280/160" alt="作品四">
                <div class="card-overlay">
                    <h3 class="card-title">作品名稱四</h3>
                    <p class="card-info">簡短描述這個專案的重點和使用技術</p>
                </div>
            </div>
            <div class="card">
                <img src="/api/placeholder/280/160" alt="作品五">
                <div class="card-overlay">
                    <h3 class="card-title">作品名稱五</h3>
                    <p class="card-info">簡短描述這個專案的重點和使用技術</p>
                </div>
            </div>
        </div>
    </div>
    
    <!-- 關於我區域 -->
    <section class="about-section" id="about">
        <div class="about-image">
            <img src="/api/placeholder/400/500" alt="個人照片">
        </div>
        <div class="about-content">
            <h2>關於我</h2>
            <p>在這裡撰寫一段詳細的自我介紹，包括您的教育背景、職業經歷、專業領域和個人特質。您可以分享您的職業旅程、重要成就以及您的專業理念。</p>
            <p>這部分也可以包含您的興趣愛好、個人價值觀以及您的職業目標。讓訪客更全面地了解您作為一個專業人士和個體的特質。</p>
            <p>記得保持內容真實、有吸引力且能反映您的個性。透過這段文字，讓潛在客戶或雇主理解為什麼要選擇與您合作。</p>
            <button class="cta-btn">下載履歷</button>
        </div>
    </section>
    
    <!-- 技能區域 -->
    <h2 class="section-title" id="skills">專業技能</h2>
    <div class="skills-grid">
        <div class="skill-card">
            <div class="skill-icon">🖥️</div>
            <h3 class="skill-name">網頁開發</h3>
            <div class="skill-level">
                <div class="skill-progress" style="width: 90%;"></div>
            </div>
        </div>
        <div class="skill-card">
            <div class="skill-icon">🎨</div>
            <h3 class="skill-name">UI/UX 設計</h3>
            <div class="skill-level">
                <div class="skill-progress" style="width: 85%;"></div>
            </div>
        </div>
        <div class="skill-card">
            <div class="skill-icon">📱</div>
            <h3 class="skill-name">行動應用開發</h3>
            <div class="skill-level">
                <div class="skill-progress" style="width: 80%;"></div>
            </div>
        </div>
        <div class="skill-card">
            <div class="skill-icon">📊</div>
            <h3 class="skill-name">數據分析</h3>
            <div class="skill-level">
                <div class="skill-progress" style="width: 75%;"></div>
            </div>
        </div>
        <div class="skill-card">
            <div class="skill-icon">⚙️</div>
            <h3 class="skill-name">後端開發</h3>
            <div class="skill-level">
                <div class="skill-progress" style="width: 85%;"></div>
            </div>
        </div>
        <div class="skill-card">
            <div class="skill-icon">🚀</div>
            <h3 class="skill-name">專案管理</h3>
            <div class="skill-level">
                <div class="skill-progress" style="width: 70%;"></div>
            </div>
        </div>
    </div>
    
    <!-- 經歷區域 -->
    <h2 class="section-title" id="experience">工作經歷</h2>
    <div class="slider-container">
        <div class="slider-row">
            <div class="card">
                <img src="/api/placeholder/280/160" alt="公司一">
                <div class="card-overlay">
                    <h3 class="card-title">職位名稱</h3>
                    <p class="card-info">公司名稱 | 2023 - 現在</p>
                </div>
            </div>
            <div class="card">
                <img src="/api/placeholder/280/160" alt="公司二">
                <div class="card-overlay">
                    <h3 class="card-title">職位名稱</h3>
                    <p class="card-info">公司名稱 | 2020 - 2023</p>
                </div>
            </div>
            <div class="card">
                <img src="/api/placeholder/280/160" alt="公司三">
                <div class="card-overlay">
                    <h3 class="card-title">職位名稱</h3>
                    <p class="card-info">公司名稱 | 2018 - 2020</p>
                </div>
            </div>
            <div class="card">
                <img src="/api/placeholder/280/160" alt="教育經歷">
                <div class="card-overlay">
                    <h3 class="card-title">學位名稱</h3>
                    <p class="card-info">大學名稱 | 2014 - 2018</p>
                </div>
            </div>
        </div>
    </div>
    
    <!-- 聯絡區域 -->
    <section class="contact-section" id="contact">
        <h2>與我聯繫</h2>
        <form class="contact-form">
            <div class="form-group">
                <label for="name">姓名</label>
                <input type="text" id="name" placeholder="請輸入您的姓名">
            </div>
            <div class="form-group">
                <label for="email">電子郵件</label>
                <input type="email" id="email" placeholder="請輸入您的電子郵件">
            </div>
            <div class="form-group">
                <label for="subject">主旨</label>
                <input type="text" id="subject" placeholder="請輸入訊息主旨">
            </div>
            <div class="form-group">
                <label for="message">訊息內容</label>
                <textarea id="message" placeholder="請輸入您的訊息內容"></textarea>
            </div>
            <button type="submit" class="submit-btn">發送訊息</button>
        </form>
    </section>
    
    <!-- 頁腳 -->
    <footer class="footer">
        <div class="social-links">
            <a href="#" class="social-link">FB</a>
            <a href="#" class="social-link">IG</a>
            <a href="#" class="social-link">LI</a>
            <a href="#" class="social-link">GH</a>
        </div>
        <p class="copyright">© 2025 您的名字. 保留所有權利.</p>
    </footer>
    
    <script>
        // 滾動時變更導航欄樣式
        window.addEventListener('scroll', function() {
            const navbar = document.querySelector('.navbar');
            if (window.scrollY > 50) {
                navbar.classList.add('scrolled');
            } else {
                navbar.classList.remove('scrolled');
            }
        });
        
        // 平滑滾動到錨點
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function(e) {
                e.preventDefault();
                
                const targetId = this.getAttribute('href');
                const targetElement = document.querySelector(targetId);
                
                window.scrollTo({
                    top: targetElement.offsetTop - 70,
                    behavior: 'smooth'
                });
            });
        });
        
        // CTA 按鈕滾動到作品集
        document.querySelector('.hero .cta-btn').addEventListener('click', function() {
            const projectsSection = document.getElementById('projects');
            window.scrollTo({
                top: projectsSection.offsetTop - 70,
                behavior: 'smooth'
            });
        });
    </script>
</body>
</html>
Last edited 1 minute ago



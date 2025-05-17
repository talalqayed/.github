<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>بنك الكريمي - التطبيق الرسمي</title>
    <style>
        /* الألوان الأساسية */
        :root {
            --orange: #FFA500;
            --purple: #8A2BE2;
            --dark-purple: #6A0DAD;
            --light-purple: #E6E6FA;
            --light-gray: #F5F5F5;
            --medium-gray: #DDDDDD;
            --dark-gray: #666666;
            --success: #4CAF50;
            --error: #F44336;
            --warning: #FFC107;
        }
        
        /* إعدادات عامة */
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        
        body {
            font-family: 'Simplified Arabic', Arial, sans-serif;
            background-color: #fff;
            color: #333;
            line-height: 1.6;
        }
        
        /* الهيدر */
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px;
            background-color: white;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            position: relative;
            z-index: 100;
        }
        
        .header-left, .header-right {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .notification-icon {
            position: relative;
            color: var(--purple);
            font-size: 24px;
            cursor: pointer;
        }
        
        .notification-badge {
            position: absolute;
            top: -5px;
            right: -5px;
            background-color: var(--orange);
            color: white;
            border-radius: 50%;
            width: 18px;
            height: 18px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 10px;
        }
        
        .profile-icon {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background-color: var(--orange);
            display: flex;
            justify-content: center;
            align-items: center;
            color: white;
            font-size: 20px;
            cursor: pointer;
            background-size: cover;
            background-position: center;
        }
        
        .menu-dots {
            font-size: 24px;
            color: var(--dark-purple);
            cursor: pointer;
        }
        
        .user-name {
            font-weight: bold;
            font-size: 16px;
        }
        
        /* القائمة المنسدلة */
        .dropdown-menu {
            display: none;
            position: absolute;
            top: 60px;
            left: 15px;
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.15);
            width: 280px;
            z-index: 1000;
            overflow: hidden;
        }
        
        .dropdown-menu.show {
            display: block;
        }
        
        .menu-header {
            background-color: var(--dark-purple);
            color: white;
            padding: 12px 15px;
            font-weight: bold;
            font-size: 16px;
        }
        
        .menu-item {
            padding: 12px 15px;
            border-bottom: 1px solid var(--light-gray);
            display: flex;
            justify-content: space-between;
            align-items: center;
            cursor: pointer;
            transition: background-color 0.2s;
        }
        
        .menu-item:last-child {
            border-bottom: none;
        }
        
        .menu-item:hover {
            background-color: var(--light-gray);
        }
        
        .menu-item-icon {
            color: var(--purple);
            font-size: 20px;
        }
        
        /* بطاقات الحساب */
        .cards-container {
            display: flex;
            overflow-x: auto;
            padding: 15px;
            gap: 15px;
            scroll-snap-type: x mandatory;
            -webkit-overflow-scrolling: touch;
        }
        
        .cards-container::-webkit-scrollbar {
            display: none;
        }
        
        .bank-card {
            min-width: 320px;
            height: 202px;
            background: linear-gradient(135deg, var(--dark-purple), var(--purple));
            border-radius: 15px;
            padding: 20px;
            color: white;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            scroll-snap-align: start;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
            flex-shrink: 0;
            position: relative;
            overflow: hidden;
        }
        
        .bank-card::after {
            content: '';
            position: absolute;
            top: -50%;
            right: -50%;
            width: 200px;
            height: 200px;
            background: rgba(255,255,255,0.1);
            border-radius: 50%;
        }
        
        .bank-card::before {
            content: '';
            position: absolute;
            bottom: -30%;
            left: -30%;
            width: 150px;
            height: 150px;
            background: rgba(255,255,255,0.05);
            border-radius: 50%;
        }
        
        .card-header {
            display: flex;
            justify-content: space-between;
            font-size: 14px;
            z-index: 1;
        }
        
        .card-body {
            margin: 10px 0;
            z-index: 1;
        }
        
        .card-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 14px;
            z-index: 1;
        }
        
        .account-number {
            font-size: 20px;
            font-weight: bold;
            display: flex;
            align-items: center;
            gap: 8px;
            letter-spacing: 1px;
        }
        
        .copy-icon {
            cursor: pointer;
            font-size: 16px;
            opacity: 0.8;
            transition: opacity 0.2s;
        }
        
        .copy-icon:hover {
            opacity: 1;
        }
        
        .account-type {
            color: rgba(255,255,255,0.8);
            font-size: 14px;
            margin-top: 5px;
        }
        
        .available-balance {
            color: rgba(255,255,255,0.8);
            font-size: 14px;
            margin: 8px 0;
        }
        
        .balance {
            font-size: 24px;
            font-weight: bold;
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin: 15px 0;
        }
        
        .currency {
            font-size: 18px;
            margin-left: 5px;
        }
        
        .balance-toggle {
            background: none;
            border: none;
            color: white;
            font-size: 18px;
            cursor: pointer;
            padding: 0;
            opacity: 0.8;
            transition: opacity 0.2s;
        }
        
        .balance-toggle:hover {
            opacity: 1;
        }
        
        .service-btn {
            background: rgba(255,255,255,0.2);
            padding: 8px 12px;
            border-radius: 15px;
            font-size: 13px;
            cursor: pointer;
            transition: background-color 0.2s;
        }
        
        .service-btn:hover {
            background: rgba(255,255,255,0.3);
        }
        
        .qr-icon {
            background: rgba(255,255,255,0.2);
            width: 35px;
            height: 35px;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            cursor: pointer;
            transition: background-color 0.2s;
        }
        
        .qr-icon:hover {
            background: rgba(255,255,255,0.3);
        }
        
        /* شريط البحث */
        .search-bar {
            margin: 0 15px 15px;
            padding: 12px 20px;
            background-color: var(--light-gray);
            border-radius: 25px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: box-shadow 0.2s;
        }
        
        .search-bar:active {
            box-shadow: 0 0 0 2px var(--purple);
        }
        
        .search-text {
            color: var(--dark-gray);
            font-size: 16px;
        }
        
        .search-icon {
            color: var(--purple);
            font-size: 20px;
        }
        
        /* شبكة الخدمات */
        .services-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
            padding: 15px;
            margin-bottom: 80px;
        }
        
        .service-item {
            background-color: white;
            border-radius: 12px;
            padding: 18px 10px;
            display: flex;
            flex-direction: column;
            align-items: center;
            box-shadow: 0 3px 10px rgba(0,0,0,0.08);
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .service-item:hover {
            transform: translateY(-5px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .service-icon {
            width: 55px;
            height: 55px;
            margin-bottom: 12px;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 26px;
        }
        
        .service-name {
            font-size: 14px;
            color: #333;
            font-weight: 500;
        }
        
        /* التنقل السفلي */
        .bottom-nav {
            position: fixed;
            bottom: 0;
            width: 100%;
            display: flex;
            justify-content: space-around;
            padding: 12px 0;
            background-color: white;
            border-top: 1px solid var(--medium-gray);
            z-index: 100;
        }
        
        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            color: var(--dark-gray);
            cursor: pointer;
            transition: color 0.2s;
            flex: 1;
            max-width: 100px;
        }
        
        .nav-item:hover {
            color: var(--purple);
        }
        
        .nav-icon {
            font-size: 24px;
            margin-bottom: 5px;
        }
        
        .nav-label {
            font-size: 12px;
        }
        
        .nav-item.active {
            color: var(--purple);
        }
        
        /* نوافذ الخدمات */
        .overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: white;
            z-index: 1000;
            padding: 20px;
            overflow-y: auto;
            display: none;
        }
        
        .window-header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
            align-items: center;
            padding-bottom: 10px;
            border-bottom: 1px solid var(--light-gray);
        }
        
        .window-title {
            font-weight: bold;
            font-size: 22px;
            color: var(--dark-purple);
        }
        
        .close-btn {
            font-size: 24px;
            color: var(--dark-gray);
            cursor: pointer;
            padding: 5px;
        }
        
        .close-btn:hover {
            color: var(--purple);
        }
        
        .input-group {
            margin-bottom: 18px;
        }
        
        .input-label {
            margin-bottom: 8px;
            color: var(--dark-purple);
            font-size: 15px;
            font-weight: 500;
            display: block;
        }
        
        select, input, textarea {
            width: 100%;
            padding: 14px;
            border-radius: 10px;
            border: 1px solid var(--medium-gray);
            font-family: inherit;
            font-size: 16px;
            background-color: white;
            transition: border-color 0.2s;
        }
        
        select:focus, input:focus, textarea:focus {
            border-color: var(--purple);
            outline: none;
        }
        
        .row-inputs {
            display: flex;
            gap: 12px;
            margin-bottom: 18px;
        }
        
        .row-inputs .input-group {
            flex: 1;
            margin-bottom: 0;
        }
        
        /* الأزرار */
        .btn {
            width: 100%;
            padding: 16px;
            border-radius: 10px;
            font-weight: bold;
            font-size: 16px;
            margin-top: 15px;
            cursor: pointer;
            text-align: center;
            border: none;
            transition: all 0.3s;
        }
        
        .btn:hover {
            opacity: 0.9;
            transform: translateY(-2px);
        }
        
        .btn:active {
            transform: translateY(0);
        }
        
        .btn-primary {
            background-color: var(--purple);
            color: white;
            box-shadow: 0 3px 10px rgba(138, 43, 226, 0.3);
        }
        
        .btn-secondary {
            background-color: white;
            color: var(--purple);
            border: 1px solid var(--purple);
        }
        
        .btn-orange {
            background-color: var(--orange);
            color: white;
            box-shadow: 0 3px 10px rgba(255, 165, 0, 0.3);
        }
        
        .btn-gray {
            background-color: var(--light-gray);
            color: var(--dark-gray);
        }
        
        /* نوافذ التأكيد */
        .confirmation-header {
            text-align: center;
            margin-bottom: 25px;
        }
        
        .confirmation-title {
            font-weight: bold;
            font-size: 24px;
            color: var(--dark-purple);
            margin-bottom: 15px;
        }
        
        .divider {
            height: 2px;
            background: linear-gradient(to right, transparent, var(--medium-gray), transparent);
            margin: 15px 0;
        }
        
        .detail-row {
            display: flex;
            justify-content: space-between;
            margin-bottom: 16px;
            font-size: 16px;
        }
        
        .detail-label {
            color: var(--dark-gray);
        }
        
        .detail-value {
            font-weight: 500;
            text-align: left;
            min-width: 50%;
        }
        
        .total-row {
            border-top: 1px dashed var(--medium-gray);
            margin: 20px 0;
            padding-top: 20px;
            display: flex;
            justify-content: space-between;
            font-size: 17px;
        }
        
        .total-label {
            font-weight: bold;
            color: var(--dark-purple);
        }
        
        .total-value {
            font-weight: bold;
            color: var(--purple);
        }
        
        .action-buttons {
            display: flex;
            gap: 12px;
            margin-top: 25px;
        }
        
        /* نافذة التحميل */
        .loading-spinner {
            display: none;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(255,255,255,0.9);
            z-index: 2000;
        }
        
        .spinner {
            width: 60px;
            height: 60px;
            border: 6px solid var(--light-purple);
            border-top: 6px solid var(--purple);
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin-bottom: 20px;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        .loading-text {
            font-size: 18px;
            color: var(--dark-purple);
            font-weight: 500;
        }
        
        /* رسائل الخطأ */
        .error-message {
            display: none;
            background-color: rgba(244, 67, 54, 0.1);
            color: var(--error);
            padding: 15px;
            border-radius: 10px;
            margin: 15px 0;
            text-align: center;
            font-weight: bold;
            border: 1px solid rgba(244, 67, 54, 0.3);
        }
        
        /* نافذة النجاح */
        .success-window {
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            text-align: center;
            padding: 30px 20px;
        }
        
        .success-icon {
            width: 90px;
            height: 90px;
            background-color: var(--success);
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            color: white;
            font-size: 45px;
            margin-bottom: 25px;
            box-shadow: 0 5px 15px rgba(76, 175, 80, 0.3);
        }
        
        .success-title {
            font-weight: bold;
            font-size: 24px;
            color: var(--success);
            margin-bottom: 20px;
        }
        
        .transfer-number {
            font-size: 20px;
            margin-bottom: 15px;
            font-weight: bold;
            background: var(--light-gray);
            padding: 10px 20px;
            border-radius: 8px;
            display: inline-block;
        }
        
        .copy-btn {
            background: none;
            border: none;
            color: var(--purple);
            text-decoration: underline;
            margin-bottom: 30px;
            cursor: pointer;
            font-size: 16px;
            padding: 5px;
        }
        
        /* قائمة المستفيدين */
        .beneficiaries-list {
            max-height: 350px;
            overflow-y: auto;
            margin-bottom: 20px;
            border: 1px solid var(--light-gray);
            border-radius: 10px;
        }
        
        .beneficiary-item {
            padding: 15px;
            border-bottom: 1px solid var(--light-gray);
            display: flex;
            justify-content: space-between;
            align-items: center;
            cursor: pointer;
            transition: background-color 0.2s;
        }
        
        .beneficiary-item:last-child {
            border-bottom: none;
        }
        
        .beneficiary-item:hover {
            background-color: var(--light-gray);
        }
        
        .beneficiary-info {
            display: flex;
            flex-direction: column;
        }
        
        .beneficiary-name {
            font-weight: bold;
            margin-bottom: 3px;
        }
        
        .beneficiary-account {
            color: var(--dark-gray);
            font-size: 14px;
        }
        
        .beneficiary-actions {
            display: flex;
            gap: 10px;
        }
        
        .beneficiary-action {
            color: var(--purple);
            font-size: 18px;
            cursor: pointer;
        }
        
        /* التبويبات */
        .tabs {
            display: flex;
            border-bottom: 1px solid var(--medium-gray);
            margin-bottom: 20px;
        }
        
        .tab {
            padding: 12px 20px;
            cursor: pointer;
            border-bottom: 3px solid transparent;
            transition: all 0.2s;
            font-weight: 500;
            text-align: center;
            flex: 1;
        }
        
        .tab.active {
            border-bottom: 3px solid var(--purple);
            color: var(--purple);
            font-weight: bold;
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
        
        /* إعدادات قاعدة البيانات */
        .backup-options {
            display: flex;
            flex-direction: column;
            gap: 15px;
            margin: 20px 0;
        }
        
        .backup-option {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 15px;
            border: 1px solid var(--medium-gray);
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.2s;
        }
        
        .backup-option:hover {
            background-color: var(--light-gray);
            border-color: var(--purple);
        }
        
        .backup-info {
            display: flex;
            flex-direction: column;
        }
        
        .backup-title {
            font-weight: bold;
            margin-bottom: 5px;
        }
        
        .backup-desc {
            color: var(--dark-gray);
            font-size: 14px;
        }
        
        .backup-icon {
            color: var(--purple);
            font-size: 24px;
        }
        
        /* إعدادات النوافذ */
        .window-settings-list {
            display: flex;
            flex-direction: column;
            gap: 12px;
        }
        
        .window-setting-item {
            padding: 15px;
            border: 1px solid var(--medium-gray);
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.2s;
        }
        
        .window-setting-item:hover {
            background-color: var(--light-gray);
            border-color: var(--purple);
        }
        
        /* نافذة الملف الشخصي */
        .profile-header {
            text-align: center;
            margin-bottom: 25px;
        }
        
        .profile-pic {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            background-color: var(--orange);
            margin: 0 auto 15px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 40px;
            color: white;
            background-size: cover;
            background-position: center;
            position: relative;
            overflow: hidden;
        }
        
        .profile-pic-edit {
            position: absolute;
            bottom: 0;
            width: 100%;
            background: rgba(0,0,0,0.5);
            color: white;
            padding: 5px;
            font-size: 14px;
        }
        
        .profile-name {
            font-weight: bold;
            font-size: 20px;
        }
        
        .profile-details {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }
        
        .profile-detail {
            display: flex;
            justify-content: space-between;
            padding: 12px 0;
            border-bottom: 1px solid var(--light-gray);
        }
        
        .detail-title {
            color: var(--dark-gray);
            font-weight: 500;
        }
        
        .detail-value {
            font-weight: bold;
            text-align: left;
        }
        
        /* خدمات الكريمي إكسبريس */
        .kuraimi-services {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin: 20px 0;
        }
        
        .kuraimi-service {
            background-color: white;
            border-radius: 10px;
            padding: 15px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.08);
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
            border: 1px solid var(--light-gray);
        }
        
        .kuraimi-service:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            border-color: var(--purple);
        }
        
        .kuraimi-icon {
            font-size: 30px;
            margin-bottom: 10px;
            color: var(--purple);
        }
        
        .kuraimi-title {
            font-weight: bold;
            margin-bottom: 5px;
        }
        
        .kuraimi-desc {
            color: var(--dark-gray);
            font-size: 13px;
        }
        
        /* خدمات أم فلوس */
        .amfloos-services {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin: 20px 0;
        }
        
        /* خدمات التمويل */
        .financing-services {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin: 20px 0;
        }
        
        /* خدمات القسائم */
        .voucher-services {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin: 20px 0;
        }
        
        /* خدمات البطاقة */
        .card-services {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin: 20px 0;
        }
        
        /* خدمات أخرى */
        .other-services {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin: 20px 0;
        }
        
        /* زر الرجوع */
        .back-btn {
            display: flex;
            align-items: center;
            gap: 5px;
            color: var(--purple);
            margin-bottom: 15px;
            cursor: pointer;
            font-weight: 500;
        }
        
        /* التكيف مع الشاشات الصغيرة */
        @media (max-width: 480px) {
            .services-grid {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .bank-card {
                min-width: 280px;
                height: 180px;
                padding: 15px;
            }
            
            .account-number {
                font-size: 18px;
            }
            
            .kuraimi-services, 
            .amfloos-services,
            .financing-services,
            .voucher-services,
            .card-services,
            .other-services {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <!-- الهيدر -->
    <div class="header">
        <div class="header-left">
            <div class="notification-icon">
                <span>🔔</span>
                <div class="notification-badge">1+</div>
            </div>
            <div class="menu-dots" onclick="toggleMenu()">⋮</div>
        </div>
        
        <div class="user-name">طلال قائد احمد يحيى المخلافي</div>
        
        <div class="header-right">
            <div class="profile-icon" style="background-image: url('https://via.placeholder.com/150');" onclick="openProfile()"></div>
        </div>
        
        <!-- القائمة المنسدلة -->
        <div class="dropdown-menu" id="dropdownMenu">
            <div class="menu-header">الإعدادات</div>
            <div class="menu-item" onclick="openLanguageSettings()">
                <span>اللغة</span>
                <span>العربية ›</span>
            </div>
            <div class="menu-item" onclick="openDatabaseSettings()">
                <span>قاعدة البيانات</span>
                <span>›</span>
            </div>
            <div class="menu-item" onclick="openWindowSettings()">
                <span>إعدادات بيانات النوافذ</span>
                <span>›</span>
            </div>
            <div class="menu-item" onclick="logout()">
                <span>تسجيل خروج</span>
                <span style="color: var(--orange);">🚪</span>
            </div>
        </div>
    </div>
    
    <!-- بطاقات الحساب -->
    <div class="cards-container">
        <div class="bank-card">
            <div class="card-header">
                <div>Al-Kuraimi Bank</div>
                <div>بنك الكريمي</div>
            </div>
            
            <div class="card-body">
                <div class="account-number">3012336089 <span class="copy-icon" onclick="copyToClipboard('3012336089')">📋</span></div>
                <div class="account-type">جاري</div>
                <div class="available-balance">الرصيد المتاح</div>
                <div class="balance">
                    <span class="balance-amount">10,000 <span class="currency">ر.ي</span></span>
                    <button class="balance-toggle" onclick="toggleBalance(this)">👁️</button>
                </div>
            </div>
            
            <div class="card-footer">
                <div class="service-btn" onclick="showStatement()">البيان</div>
                <div class="qr-icon" onclick="showQR('3012336089')">QR</div>
                <div class="service-btn" onclick="showAccountServices('3012336089')">خدمات</div>
            </div>
        </div>
        
        <div class="bank-card">
            <div class="card-header">
                <div>Al-Kuraimi Bank</div>
                <div>بنك الكريمي</div>
            </div>
            
            <div class="card-body">
                <div class="account-number">3020176217 <span class="copy-icon" onclick="copyToClipboard('3020176217')">📋</span></div>
                <div class="account-type">جاري</div>
                <div class="available-balance">الرصيد المتاح</div>
                <div class="balance">
                    <span class="balance-amount">500 <span class="currency">$</span></span>
                    <button class="balance-toggle" onclick="toggleBalance(this)">👁️</button>
                </div>
            </div>
            
            <div class="card-footer">
                <div class="service-btn" onclick="showStatement()">البيان</div>
                <div class="qr-icon" onclick="showQR('3020176217')">QR</div>
                <div class="service-btn" onclick="showAccountServices('3020176217')">خدمات</div>
            </div>
        </div>
        
        <div class="bank-card">
            <div class="card-header">
                <div>Al-Kuraimi Bank</div>
                <div>بنك الكريمي</div>
            </div>
            
            <div class="card-body">
                <div class="account-number">3027165892 <span class="copy-icon" onclick="copyToClipboard('3027165892')">📋</span></div>
                <div class="account-type">جاري</div>
                <div class="available-balance">الرصيد المتاح</div>
                <div class="balance">
                    <span class="balance-amount">2,000 <span class="currency">ر.س</span></span>
                    <button class="balance-toggle" onclick="toggleBalance(this)">👁️</button>
                </div>
            </div>
            
            <div class="card-footer">
                <div class="service-btn" onclick="showStatement()">البيان</div>
                <div class="qr-icon" onclick="showQR('3027165892')">QR</div>
                <div class="service-btn" onclick="showAccountServices('3027165892')">خدمات</div>
            </div>
        </div>
    </div>
    
    <!-- شريط البحث -->
    <div class="search-bar" onclick="openSearch()">
        <div class="search-text">خذني إلى...</div>
        <div class="search-icon">🔍</div>
    </div>
    
    <!-- شبكة الخدمات -->
    <div class="services-grid">
        <!-- الصف الأول -->
        <div class="service-item" onclick="openService('kuraimi-express')">
            <div class="service-icon" style="color: red; background-color: rgba(255,0,0,0.1);">K</div>
            <div class="service-name">كريمي إكسبرس</div>
        </div>
        <div class="service-item" onclick="openService('bank-services')">
            <div class="service-icon" style="color: var(--purple); background-color: rgba(138,43,226,0.1);">🏦</div>
            <div class="service-name">الخدمات البنكية</div>
        </div>
        <div class="service-item" onclick="openService('payment-services')">
            <div class="service-icon" style="color: var(--dark-purple); background-color: rgba(106,13,173,0.1);">💻</div>
            <div class="service-name">الدفع والسداد</div>
        </div>
        
        <!-- الصف الثاني -->
        <div class="service-item" onclick="openService('am-floos')">
            <div class="service-icon" style="color: gray; background-color: rgba(128,128,128,0.1);">💰</div>
            <div class="service-name">أم فلوس</div>
        </div>
        <div class="service-item" onclick="openService('financing')">
            <div class="service-icon" style="color: var(--purple); background-color: rgba(138,43,226,0.1);">⚙️</div>
            <div class="service-name">التمويل</div>
        </div>
        <div class="service-item" onclick="openService('vouchers')">
            <div class="service-icon" style="color: gray; background-color: rgba(128,128,128,0.1);">🎫</div>
            <div class="service-name">القسائم</div>
        </div>
        
        <!-- الصف الثالث -->
        <div class="service-item" onclick="openService('card-services')">
            <div class="service-icon" style="color: gray; background-color: rgba(128,128,128,0.1);">💳</div>
            <div class="service-name">البطاقة</div>
        </div>
        <div class="service-item" onclick="openService('other-services')">
            <div class="service-icon" style="color: var(--purple); background-color: rgba(138,43,226,0.1);">➕</div>
            <div class="service-name">خدمات أخرى</div>
        </div>
    </div>
    
    <!-- نوافذ الخدمات -->
    
    <!-- نافذة التحويل -->
    <div class="overlay" id="transferWindow">
        <div class="window-header">
            <div class="window-title">الإرسال إلى رقم مميز</div>
            <div class="close-btn" onclick="closeWindow('transferWindow')">×</div>
        </div>
        
        <div class="input-group">
            <div class="input-label">الحساب المراد التحويل منه</div>
            <select id="fromAccount">
                <option value="3012336089-YER">3012336089 - YER</option>
                <option value="3020176217-USD">3020176217 - USD</option>
                <option value="3027165892-SAR">3027165892 - SAR</option>
            </select>
        </div>
        
        <div class="row-inputs">
            <div class="input-group">
                <div class="input-label">اختر المنطقة</div>
                <select id="region" onchange="updateBranches()">
                    <option value="">اختر المنطقة</option>
                    <option value="sanaa">منطقة صنعاء</option>
                    <option value="hodeidah">منطقة الحديدة</option>
                    <option value="ibb">منطقة اب</option>
                    <option value="taiz">منطقة تعز</option>
                    <option value="aden">منطقة عدن</option>
                    <option value="hadramout">منطقة حضرموت</option>
                    <option value="marib">منطقة مأرب</option>
                </select>
            </div>
            <div class="input-group">
                <div class="input-label">اختر الفرع</div>
                <select id="branch" disabled>
                    <option value="">اختر الفرع</option>
                </select>
            </div>
        </div>
        
        <div class="input-group">
            <div class="input-label">اسم المستفيد</div>
            <input type="text" id="beneficiaryName" placeholder="أدخل اسم المستفيد">
        </div>
        
        <div class="input-group">
            <div class="input-label">رقم موبایل المستفيد</div>
            <input type="tel" id="beneficiaryPhone" placeholder="أدخل رقم الهاتف">
        </div>
        
        <div class="input-group">
            <div class="input-label">ادخل المبلغ</div>
            <input type="number" id="amount" placeholder="أدخل المبلغ">
        </div>
        
        <div class="input-group">
            <div class="input-label">ملاحظات (اختياري)</div>
            <textarea id="notes" rows="2" placeholder="أدخل أي ملاحظات"></textarea>
        </div>
        
        <button class="btn btn-primary" onclick="validateTransfer()">موافق</button>
    </div>
    
    <!-- نافذة الخدمات البنكية -->
    <div class="overlay" id="bankServicesWindow">
        <div class="window-header">
            <div class="window-title">الخدمات البنكية</div>
            <div class="close-btn" onclick="closeWindow('bankServicesWindow')">×</div>
        </div>
        
        <div class="tabs">
            <div class="tab active" onclick="switchTab('beneficiaries-tab', this)">قائمة المستفيدين</div>
            <div class="tab" onclick="switchTab('transfer-tab', this)">تحويل لحساب آخر</div>
        </div>
        
        <div id="beneficiaries-tab" class="tab-content active">
            <div class="beneficiaries-list">
                <div class="beneficiary-item" onclick="selectBeneficiary('3009368433', 'فواز قايد لطف فرحان الحميدي')">
                    <div class="beneficiary-info">
                        <div class="beneficiary-name">فواز قايد لطف فرحان الحميدي</div>
                        <div class="beneficiary-account">3009368433</div>
                    </div>
                    <div class="beneficiary-actions">
                        <div class="beneficiary-action" onclick="editBeneficiary(event, '3009368433')">✏️</div>
                        <div class="beneficiary-action" onclick="deleteBeneficiary(event, '3009368433')">🗑️</div>
                    </div>
                </div>
                
                <div class="beneficiary-item" onclick="selectBeneficiary('3051621343', 'اياد عبدالرزاق عبدالرحمن السابر')">
                    <div class="beneficiary-info">
                        <div class="beneficiary-name">اياد عبدالرزاق عبدالرحمن السابر</div>
                        <div class="beneficiary-account">3051621343</div>
                    </div>
                    <div class="beneficiary-actions">
                        <div class="beneficiary-action" onclick="editBeneficiary(event, '3051621343')">✏️</div>
                        <div class="beneficiary-action" onclick="deleteBeneficiary(event, '3051621343')">🗑️</div>
                    </div>
                </div>
                
                <!-- المزيد من المستفيدين -->
            </div>
            
            <button class="btn btn-primary" onclick="addBeneficiary()">إضافة مستفيد جديد</button>
        </div>
        
        <div id="transfer-tab" class="tab-content">
            <div class="input-group">
                <div class="input-label">الحساب المراد التحويل منه</div>
                <select>
                    <option>3012336089 - YER</option>
                    <option>3020176217 - USD</option>
                    <option>3027165892 - SAR</option>
                </select>
            </div>
            
            <div class="input-group">
                <div class="input-label">إلى رقم الحساب</div>
                <div style="display: flex; gap: 5px;">
                    <input type="text" placeholder="أدخل رقم الحساب">
                    <button class="btn btn-secondary" style="width: auto; padding: 0 15px;">QR</button>
                </div>
            </div>
            
            <div class="input-group">
                <div class="input-label">ادخل المبلغ</div>
                <input type="number" placeholder="أدخل المبلغ">
            </div>
            
            <button class="btn btn-primary">موافق</button>
        </div>
    </div>
    
    <!-- نافذة الكريمي إكسبريس -->
    <div class="overlay" id="kuraimiExpressWindow">
        <div class="window-header">
            <div class="window-title">خدمات الكريمي إكسبريس</div>
            <div class="close-btn" onclick="closeWindow('kuraimiExpressWindow')">×</div>
        </div>
        
        <div class="kuraimi-services">
            <div class="kuraimi-service" onclick="openTransferToNumber()">
                <div class="kuraimi-icon">📱</div>
                <div class="kuraimi-title">الإرسال إلى رقم</div>
                <div class="kuraimi-desc">تحويل أموال إلى رقم هاتف</div>
            </div>
            
            <div class="kuraimi-service" onclick="openTransferToName()">
                <div class="kuraimi-icon">👤</div>
                <div class="kuraimi-title">الإرسال إلى اسم</div>
                <div class="kuraimi-desc">تحويل أموال إلى مستفيد محدد</div>
            </div>
            
            <div class="kuraimi-service" onclick="openTransferToAccount()">
                <div class="kuraimi-icon">🏦</div>
                <div class="kuraimi-title">دفع حوالة إلى حساب</div>
                <div class="kuraimi-desc">تحويل أموال إلى حساب بنكي</div>
            </div>
            
            <div class="kuraimi-service" onclick="openCancelTransfer()">
                <div class="kuraimi-icon">❌</div>
                <div class="kuraimi-title">إلغاء حوالة</div>
                <div class="kuraimi-desc">إلغاء حوالة مرسلة</div>
            </div>
            
            <div class="kuraimi-service" onclick="openTransferStatus()">
                <div class="kuraimi-icon">🔍</div>
                <div class="kuraimi-title">حالة الحوالة</div>
                <div class="kuraimi-desc">التحقق من حالة الحوالة</div>
            </div>
        </div>
    </div>
    
    <!-- نافذة الدفع والسداد -->
    <div class="overlay" id="paymentServicesWindow">
        <div class="window-header">
            <div class="window-title">خدمات الدفع والسداد</div>
            <div class="close-btn" onclick="closeWindow('paymentServicesWindow')">×</div>
        </div>
        
        <div class="kuraimi-services">
            <div class="kuraimi-service" onclick="openActivateEShopping()">
                <div class="kuraimi-icon">🛒</div>
                <div class="kuraimi-title">تفعيل التسوق الإلكتروني</div>
                <div class="kuraimi-desc">تفعيل الخدمة للدفع عبر الإنترنت</div>
            </div>
            
            <div class="kuraimi-service" onclick="openPaymentServices()">
                <div class="kuraimi-icon">💵</div>
                <div class="kuraimi-title">خدمات السداد</div>
                <div class="kuraimi-desc">سداد الفواتير والالتزامات</div>
            </div>
            
            <div class="kuraimi-service" onclick="openPayPurchases()">
                <div class="kuraimi-icon">🛍️</div>
                <div class="kuraimi-title">دفع قيمة المشتريات</div>
                <div class="kuraimi-desc">دفع فواتير المشتريات</div>
            </div>
            
            <div class="kuraimi-service" onclick="openPaymentList()">
                <div class="kuraimi-icon">📋</div>
                <div class="kuraimi-title">قائمة حاسب</div>
                <div class="kuraimi-desc">عرض سجل المدفوعات</div>
            </div>
        </div>
    </div>
    
    <!-- نافذة أم فلوس -->
    <div class="overlay" id="amFloosWindow">
        <div class="window-header">
            <div class="window-title">خدمات أم فلوس</div>
            <div class="close-btn" onclick="closeWindow('amFloosWindow')">×</div>
        </div>
        
        <div class="kuraimi-services">
            <div class="kuraimi-service" onclick="openTransferToAmFloos()">
                <div class="kuraimi-icon">🔄</div>
                <div class="kuraimi-title">التحويل إلى حساب أم فلوس</div>
                <div class="kuraimi-desc">تحويل أموال إلى حساب أم فلوس</div>
            </div>
            
            <div class="kuraimi-service" onclick="openCashWithdrawal()">
                <div class="kuraimi-icon">💸</div>
                <div class="kuraimi-title">السحب النقدي من وكيل أم فلوس</div>
                <div class="kuraimi-desc">سحب نقدي من نقاط الخدمة</div>
            </div>
            
            <div class="kuraimi-service" onclick="openCancelWithdrawal()">
                <div class="kuraimi-icon">✖️</div>
                <div class="kuraimi-title">إلغاء عملية السحب النقدي</div>
                <div class="kuraimi-desc">إلغاء طلب سحب نقدي</div>
            </div>
        </div>
    </div>
    
    <!-- نافذة التمويل -->
    <div class="overlay" id="financingWindow">
        <div class="window-header">
            <div class="window-title">خدمات التمويل</div>
            <div class="close-btn" onclick="closeWindow('financingWindow')">×</div>
        </div>
        
        <div class="kuraimi-services">
            <div class="kuraimi-service" onclick="openInstallmentPayment()">
                <div class="kuraimi-icon">💰</div>
                <div class="kuraimi-title">سداد القسط</div>
                <div class="kuraimi-desc">سداد أقساط التمويل</div>
            </div>
            
            <div class="kuraimi-service" onclick="openInstallmentList()">
                <div class="kuraimi-icon">📑</div>
                <div class="kuraimi-title">قائمة الأقساط</div>
                <div class="kuraimi-desc">عرض سجل الأقساط</div>
            </div>
            
            <div class="kuraimi-service" onclick="openFinanceRequest()">
                <div class="kuraimi-icon">🆕</div>
                <div class="kuraimi-title">طلب تمويل</div>
                <div class="kuraimi-desc">تقديم طلب تمويل جديد</div>
            </div>
        </div>
    </div>
    
    <!-- نافذة القسائم -->
    <div class="overlay" id="vouchersWindow">
        <div class="window-header">
            <div class="window-title">خدمات القسائم</div>
            <div class="close-btn" onclick="closeWindow('vouchersWindow')">×</div>
        </div>
        
        <div class="kuraimi-services">
            <div class="kuraimi-service" onclick="openCreateVoucher()">
                <div class="kuraimi-icon">🆕</div>
                <div class="kuraimi-title">إنشاء قسيمة</div>
                <div class="kuraimi-desc">إنشاء قسيمة جديدة</div>
            </div>
            
            <div class="kuraimi-service" onclick="openRedeemVoucher()">
                <div class="kuraimi-icon">🔙</div>
                <div class="kuraimi-title">استرداد قسيمة</div>
                <div class="kuraimi-desc">استخدام القسائم المتاحة</div>
            </div>
            
            <div class="kuraimi-service" onclick="openVouchersList()">
                <div class="kuraimi-icon">📋</div>
                <div class="kuraimi-title">القسائم</div>
                <div class="kuraimi-desc">عرض القسائم المتاحة</div>
            </div>
        </div>
    </div>
    
    <!-- نافذة البطاقة -->
    <div class="overlay" id="cardServicesWindow">
        <div class="window-header">
            <div class="window-title">خدمات البطاقة</div>
            <div class="close-btn" onclick="closeWindow('cardServicesWindow')">×</div>
        </div>
        
        <div class="kuraimi-services">
            <div class="kuraimi-service" onclick="openCardServices()">
                <div class="kuraimi-icon">💳</div>
                <div class="kuraimi-title">بطاقة ايدي</div>
                <div class="kuraimi-desc">إدارة بطاقة الصراف الآلي</div>
            </div>
        </div>
    </div>
    
    <!-- نافذة خدمات أخرى -->
    <div class="overlay" id="otherServicesWindow">
        <div class="window-header">
            <div class="window-title">خدمات أخرى</div>
            <div class="close-btn" onclick="closeWindow('otherServicesWindow')">×</div>
        </div>
        
        <div class="kuraimi-services">
            <div class="kuraimi-service" onclick="openChangePassword()">
                <div class="kuraimi-icon">🔒</div>
                <div class="kuraimi-title">تغير كلمة المرور</div>
                <div class="kuraimi-desc">تحديث كلمة المرور</div>
            </div>
            
            <div class="kuraimi-service" onclick="openLocation()">
                <div class="kuraimi-icon">📍</div>
                <div class="kuraimi-title">الموقع</div>
                <div class="kuraimi-desc">عرض مواقع الفروع</div>
            </div>
            
            <div class="kuraimi-service" onclick="openWebsite()">
                <div class="kuraimi-icon">🌐</div>
                <div class="kuraimi-title">موقعنا على الإنترنت</div>
                <div class="kuraimi-desc">الذهاب إلى الموقع الرسمي</div>
            </div>
            
            <div class="kuraimi-service" onclick="openSocialMedia()">
                <div class="kuraimi-icon">📱</div>
                <div class="kuraimi-title">صفحاتنا على التواصل الاجتماعي</div>
                <div class="kuraimi-desc">روابط وسائل التواصل</div>
            </div>
            
            <div class="kuraimi-service" onclick="openAddAlert()">
                <div class="kuraimi-icon">🔔</div>
                <div class="kuraimi-title">إضافة تنبيه</div>
                <div class="kuraimi-desc">إعداد تنبيهات مخصصة</div>
            </div>
        </div>
    </div>
    
    <!-- نافذة تأكيد التحويل -->
    <div class="overlay" id="confirmationWindow">
        <div class="confirmation-header">
            <div class="confirmation-title">التأكيد</div>
            <div class="divider"></div>
        </div>
        
        <div>
            <div class="detail-row">
                <div class="detail-label">اسم المستلم</div>
                <div class="detail-value" id="confirm-name">أحمد محمد</div>
            </div>
            <div class="detail-row">
                <div class="detail-label">رقم الهاتف</div>
                <div class="detail-value" id="confirm-phone">771234567</div>
            </div>
            <div class="detail-row">
                <div class="detail-label">من حساب</div>
                <div class="detail-value" id="confirm-from">3012336089 - YER</div>
            </div>
            <div class="detail-row">
                <div class="detail-label">المبلغ المرسل</div>
                <div class="detail-value" id="confirm-amount">10,000 ر.ي</div>
            </div>
            <div class="detail-row">
                <div class="detail-label">الرسوم</div>
                <div class="detail-value" id="confirm-fees">100 ر.ي</div>
            </div>
            
            <div class="total-row">
                <div class="total-label">المبلغ الإجمالي</div>
                <div class="total-value" id="confirm-total">10,100 ر.ي</div>
            </div>
        </div>
        
        <div class="action-buttons">
            <button class="btn btn-primary" onclick="processTransfer()">متابعة</button>
            <button class="btn btn-secondary" onclick="closeWindow('confirmationWindow')">إلغاء</button>
        </div>
    </div>
    
    <!-- نافذة التحميل -->
    <div class="loading-spinner" id="loadingSpinner">
        <div class="spinner"></div>
        <div class="loading-text">جاري معالجة العملية...</div>
    </div>
    
    <!-- رسالة الخطأ -->
    <div class="error-message" id="errorMessage">
        فشلت عملية التحويل، يرجى المحاولة مرة أخرى
    </div>
    
    <!-- نافذة النجاح -->
    <div class="overlay success-window" id="successWindow">
        <div class="success-icon">✓</div>
        <div class="success-title">تمت العملية بنجاح</div>
        <div class="transfer-number">رقم الحوالة: <span id="transferNumber">583742916</span></div>
        <button class="copy-btn" onclick="copyTransferNumber()">نسخ رقم الحوالة</button>
        <button class="btn btn-primary" onclick="closeWindow('successWindow')">موافق</button>
    </div>
    
    <!-- نافذة إعدادات قاعدة البيانات -->
    <div class="overlay" id="databaseWindow">
        <div class="window-header">
            <div class="window-title">قاعدة البيانات</div>
            <div class="close-btn" onclick="closeWindow('databaseWindow')">×</div>
        </div>
        
        <div class="backup-options">
            <div class="backup-option" onclick="createBackup()">
                <div class="backup-info">
                    <div class="backup-title">إنشاء نسخة احتياطية</div>
                    <div class="backup-desc">حفظ البيانات على Google Drive</div>
                </div>
                <div class="backup-icon">📤</div>
            </div>
            
            <div class="backup-option" onclick="restoreBackup()">
                <div class="backup-info">
                    <div class="backup-title">استرداد نسخة احتياطية</div>
                    <div class="backup-desc">استعادة البيانات من Google Drive</div>
                </div>
                <div class="backup-icon">📥</div>
            </div>
        </div>
    </div>
    
    <!-- نافذة إعدادات النوافذ -->
    <div class="overlay" id="windowSettingsWindow">
        <div class="window-header">
            <div class="window-title">إعدادات بيانات النوافذ</div>
            <div class="close-btn" onclick="closeWindow('windowSettingsWindow')">×</div>
        </div>
        
        <div class="window-settings-list">
            <div class="window-setting-item" onclick="configureWindow('kuraimi-express')">
                نوافذ خدمات الكريمي إكسبريس
            </div>
            <div class="window-setting-item" onclick="configureWindow('bank-services')">
                الخدمات البنكية
            </div>
            <div class="window-setting-item" onclick="configureWindow('payment-services')">
                نوافذ خدمات الدفع والسداد
            </div>
            <div class="window-setting-item" onclick="configureWindow('am-floos')">
                نوافذ خدمات أم فلوس
            </div>
            <div class="window-setting-item" onclick="configureWindow('financing')">
                نوافذ خدمات التمويل
            </div>
            <div class="window-setting-item" onclick="configureWindow('vouchers')">
                نوافذ خدمات القسائم
            </div>
            <div class="window-setting-item" onclick="configureWindow('card-services')">
                نوافذ خدمات البطاقة
            </div>
            <div class="window-setting-item" onclick="configureWindow('other-services')">
                نوافذ خدمات أخرى
            </div>
        </div>
    </div>
    
    <!-- نافذة إعدادات اللغة -->
    <div class="overlay" id="languageWindow">
        <div class="window-header">
            <div class="window-title">إعدادات اللغة</div>
            <div class="close-btn" onclick="closeWindow('languageWindow')">×</div>
        </div>
        
        <div class="input-group">
            <div class="input-label">اختر اللغة المفضلة</div>
            <select id="languageSelect">
                <option value="ar" selected>العربية</option>
                <option value="en">English</option>
            </select>
        </div>
        
        <button class="btn btn-primary" onclick="saveLanguage()">حفظ</button>
    </div>
    
    <!-- نافذة الملف الشخصي -->
    <div class="overlay" id="profileWindow">
        <div class="window-header">
            <div class="window-title">معلومات المستخدم</div>
            <div class="close-btn" onclick="closeWindow('profileWindow')">×</div>
        </div>
        
        <div class="profile-header">
            <div class="profile-pic" style="background-image: url('https://via.placeholder.com/150');">
                <div class="profile-pic-edit">تغيير</div>
            </div>
            <div class="profile-name">طلال قائد احمد يحيى المخلافي</div>
        </div>
        
        <div class="profile-details">
            <div class="profile-detail">
                <div class="detail-title">الحساب الافتراضي</div>
                <div class="detail-value">3012336089 - YER</div>
            </div>
            
            <div class="profile-detail">
                <div class="detail-title">تاريخ الميلاد</div>
                <div class="detail-value">1982/01/01</div>
            </div>
            
            <div class="profile-detail">
                <div class="detail-title">مكان الميلاد</div>
                <div class="detail-value">إلخشبة</div>
            </div>
            
            <div class="profile-detail">
                <div class="detail-title">الجنسية</div>
                <div class="detail-value">Yemen</div>
            </div>
            
            <div class="profile-detail">
                <div class="detail-title">رقم الموبايل</div>
                <div class="detail-value">770006222</div>
            </div>
        </div>
        
        <button class="btn btn-orange" onclick="changeProfilePicture()">تغيير صورة الملف الشخصي</button>
    </div>
    
    <!-- نافذة الإرسال إلى رقم -->
    <div class="overlay" id="transferToNumberWindow">
        <div class="back-btn" onclick="backToService('kuraimiExpressWindow')">
            ‹ الرجوع
        </div>
        
        <div class="window-header">
            <div class="window-title">الإرسال إلى رقم مميز</div>
            <div class="close-btn" onclick="closeWindow('transferToNumberWindow')">×</div>
        </div>
        
        <div class="input-group">
            <div class="input-label">الحساب المراد التحويل منه</div>
            <select>
                <option>3012336089 - YER</option>
                <option>3020176217 - USD</option>
                <option>3027165892 - SAR</option>
            </select>
        </div>
        
        <div class="row-inputs">
            <div class="input-group">
                <div class="input-label">اختر المنطقة</div>
                <select>
                    <option>منطقة صنعاء</option>
                    <option>منطقة الحديدة</option>
                    <option>منطقة اب</option>
                    <option>منطقة تعز</option>
                    <option>منطقة عدن</option>
                    <option>منطقة حضرموت</option>
                    <option>منطقة مأرب</option>
                </select>
            </div>
            <div class="input-group">
                <div class="input-label">اختر الفرع</div>
                <select>
                    <option>فرع حدة</option>
                    <option>فرع الدائري</option>
                    <option>فرع عصر</option>
                    <option>فرع جولة مذبح</option>
                    <option>فرع المحويت</option>
                </select>
            </div>
        </div>
        
        <div class="input-group">
            <div class="input-label">اسم المستفيد</div>
            <input type="text" placeholder="أدخل اسم المستفيد">
        </div>
        
        <div class="input-group">
            <div class="input-label">رقم موبایل المستفيد</div>
            <input type="tel" placeholder="أدخل رقم الهاتف">
        </div>
        
        <div class="input-group">
            <div class="input-label">ادخل المبلغ</div>
            <input type="number" placeholder="أدخل المبلغ">
        </div>
        
        <button class="btn btn-primary">موافق</button>
    </div>
    
    <!-- نافذة الإرسال إلى اسم -->
    <div class="overlay" id="transferToNameWindow">
        <div class="back-btn" onclick="backToService('kuraimiExpressWindow')">
            ‹ الرجوع
        </div>
        
        <div class="window-header">
            <div class="window-title">الإرسال إلى اسم</div>
            <div class="close-btn" onclick="closeWindow('transferToNameWindow')">×</div>
        </div>
        
        <div class="input-group">
            <div class="input-label">الحساب المراد التحويل منه</div>
            <select>
                <option>3012336089 - YER</option>
                <option>3020176217 - USD</option>
                <option>3027165892 - SAR</option>
            </select>
        </div>
        
        <div class="input-group">
            <div class="input-label">اسم المستفيد</div>
            <input type="text" placeholder="أدخل اسم المستفيد">
        </div>
        
        <div class="input-group">
            <div class="input-label">رقم حساب المستفيد</div>
            <input type="text" placeholder="أدخل رقم الحساب">
        </div>
        
        <div class="input-group">
            <div class="input-label">ادخل المبلغ</div>
            <input type="number" placeholder="أدخل المبلغ">
        </div>
        
        <button class="btn btn-primary">موافق</button>
    </div>
    
    <!-- التنقل السفلي -->
    <div class="bottom-nav">
        <div class="nav-item active" onclick="navigate('home')">
            <div class="nav-icon">🏠</div>
            <div class="nav-label">الرئيسية</div>
        </div>
        <div class="nav-item" onclick="navigate('profile')">
            <div class="nav-icon">👤</div>
            <div class="nav-label">البيانات</div>
        </div>
    </div>

    <script>
        // المتغيرات العامة
        let transferAttempts = 0;
        const branches = {
            sanaa: ["فرع حدة", "فرع الدائري", "فرع عصر", "فرع جولة مذبح", "فرع المحويت", "فرع شارع الرقاص", "فرع شارع الزبيري", "فرع شارع الستين"],
            hodeidah: ["الحديدة الرئيسي", "فرع شارع زايد", "فرع الحديدة شارع جمال", "فرع الحي التجاري", "فرع ش جيزان", "فرع حجه", "فرع شفر", "فرع كيلو 4 جولة الشهداء"],
            ibb: ["اب الرئيسي", "فرع شارع العدين", "فرع شارع تعز", "فرع مفرق جبلة", "فرع السبيل", "فرع العدين", "فرع مفرق ميثم", "فرع مفرق حبيش"],
            taiz: ["تعز الرئيسي", "فرع الحوض", "فرع تعز شارع جمال", "فرع وادي القاضي", "مكتب شارع المغتربين", "مكتب البعراره", "فرع الموشكـي", "صبر الموادم"],
            aden: ["الشيخ الرئيسي", "مكتب سوق الذهب", "فرع الممدارة", "فرع المنصورة", "فرع شارع التسعين", "فرع دار سعد", "فرع جولة كالتكس", "فرع مدينة إنماء"],
            hadramout: ["فرع خور المكلا", "بويش المكلا", "مكتب المكلا فوة", "فرع المكلا الشرج", "مكتب الشحر", "فرع الغيظة", "فرع شحن", "فرع سقطرى"],
            marib: ["فرع مارب", "فرع مارب السوق", "فرع سوق بن معيلي", "فرع مأرب الجامعه", "فرع الشبواني", "فرع عتق", "فرع بيحان", "فرع عزان شبوة"]
        };
        
        // إدارة القائمة المنسدلة
        function toggleMenu() {
            const menu = document.getElementById('dropdownMenu');
            menu.classList.toggle('show');
        }
        
        // إغلاق القائمة عند النقر خارجها
        document.addEventListener('click', function(event) {
            const menu = document.getElementById('dropdownMenu');
            if (!event.target.closest('.menu-dots') && !event.target.closest('.dropdown-menu')) {
                menu.classList.remove('show');
            }
        });
        
        // إدارة النوافذ
        function openWindow(windowId) {
            document.getElementById(windowId).style.display = 'block';
        }
        
        function closeWindow(windowId) {
            document.getElementById(windowId).style.display = 'none';
        }
        
        function backToService(serviceWindowId) {
            closeWindow(event.target.closest('.overlay').id);
            openWindow(serviceWindowId);
        }
        
        function navigate(page) {
            if (page === 'home') {
                // إغلاق جميع النوافذ
                document.querySelectorAll('.overlay').forEach(window => {
                    window.style.display = 'none';
                });
                document.getElementById('dropdownMenu').classList.remove('show');
                
                // تحديث عنصر التنقل النشط
                document.querySelectorAll('.nav-item').forEach(item => {
                    item.classList.remove('active');
                });
                document.querySelector('.nav-item:nth-child(1)').classList.add('active');
            } else if (page === 'profile') {
                openWindow('profileWindow');
                
                // تحديث عنصر التنقل النشط
                document.querySelectorAll('.nav-item').forEach(item => {
                    item.classList.remove('active');
                });
                document.querySelector('.nav-item:nth-child(2)').classList.add('active');
            }
        }
        
        // إدارة التبويبات
        function switchTab(tabId, tabElement) {
            // إزالة التنشيط من جميع التبويبات
            document.querySelectorAll('.tab').forEach(tab => {
                tab.classList.remove('active');
            });
            
            // إخفاء جميع محتويات التبويبات
            document.querySelectorAll('.tab-content').forEach(content => {
                content.classList.remove('active');
            });
            
            // تنشيط التبويب المحدد
            tabElement.classList.add('active');
            document.getElementById(tabId).classList.add('active');
        }
        
        // وظائف التحويل
        function validateTransfer() {
            const name = document.getElementById('beneficiaryName').value;
            const phone = document.getElementById('beneficiaryPhone').value;
            const amount = document.getElementById('amount').value;
            const region = document.getElementById('region').value;
            const branch = document.getElementById('branch').value;
            
            if (!name || !phone || !amount || !region || !branch) {
                alert('يرجى تعبئة جميع الحقول المطلوبة');
                return;
            }
            
            // تعيين تفاصيل التأكيد
            document.getElementById('confirm-name').textContent = name;
            document.getElementById('confirm-phone').textContent = phone;
            document.getElementById('confirm-from').textContent = document.getElementById('fromAccount').value;
            
            const amountNum = parseFloat(amount);
            let fees = 0;
            
            // حساب الرسوم حسب العملة
            const currency = document.getElementById('fromAccount').value.split('-')[1];
            if (currency === 'YER') {
                fees = amountNum * 0.01; // 1% لليمني
            } else if (currency === 'USD') {
                fees = 0.005 * amountNum; // 0.5% للدولار
            } else if (currency === 'SAR') {
                fees = 0.0006 * amountNum; // 0.06% للريال السعودي
            }
            
            document.getElementById('confirm-amount').textContent = amountNum.toLocaleString() + ' ' + 
                (currency === 'YER' ? 'ر.ي' : currency === 'USD' ? '$' : 'ر.س');
            document.getElementById('confirm-fees').textContent = fees.toFixed(3) + ' ' + 
                (currency === 'YER' ? 'ر.ي' : currency === 'USD' ? '$' : 'ر.س');
            document.getElementById('confirm-total').textContent = (amountNum + fees).toLocaleString() + ' ' + 
                (currency === 'YER' ? 'ر.ي' : currency === 'USD' ? '$' : 'ر.س');
            
            closeWindow('transferWindow');
            openWindow('confirmationWindow');
        }
        
        function processTransfer() {
            // عرض مؤشر التحميل
            document.getElementById('loadingSpinner').style.display = 'flex';
            document.getElementById('errorMessage').style.display = 'none';
            
            // محاكاة تأخير المعالجة
            setTimeout(function() {
                document.getElementById('loadingSpinner').style.display = 'none';
                
                transferAttempts++;
                
                if (transferAttempts < 3) {
                    // عرض رسالة الخطأ
                    document.getElementById('errorMessage').style.display = 'block';
                    document.getElementById('errorMessage').textContent = 
                        transferAttempts === 1 ? 'فشلت عملية التحويل، يرجى المحاولة مرة أخرى' : 
                        'فشلت عملية التحويل، يرجى المحاولة مرة ثانية';
                    
                    // إبقاء نافذة التأكيد مفتوحة لإعادة المحاولة
                } else if (transferAttempts === 3) {
                    // عرض تحذير عملية مكررة
                    if (confirm('لديك عملية بنفس البيانات، هل تود تكرار العملية؟')) {
                        // إذا وافق المستخدم، إعادة المحاولة
                        transferAttempts = 0;
                        processTransfer();
                    } else {
                        closeWindow('confirmationWindow');
                        transferAttempts = 0;
                    }
                } else {
                    // النجاح في المحاولة الرابعة (لأغراض العرض)
                    transferAttempts = 0;
                    closeWindow('confirmationWindow');
                    
                    // توليد رقم حوالة عشوائي
                    const transferNum = Math.floor(100000000 + Math.random() * 900000000);
                    document.getElementById('transferNumber').textContent = transferNum;
                    
                    openWindow('successWindow');
                }
            }, 2000);
        }
        
        function copyTransferNumber() {
            const transferNum = document.getElementById('transferNumber').textContent;
            navigator.clipboard.writeText(transferNum).then(() => {
                alert('تم نسخ رقم الحوالة: ' + transferNum);
            });
        }
        
        // وظائف الخدمات البنكية
        function selectBeneficiary(account, name) {
            alert(`تم اختيار المستفيد: ${name} (${account})`);
            // في التطبيق الفعلي، سيتم ملء نموذج التحويل
        }
        
        function editBeneficiary(event, account) {
            event.stopPropagation();
            alert(`تحرير المستفيد برقم الحساب: ${account}`);
        }
        
        function deleteBeneficiary(event, account) {
            event.stopPropagation();
            if (confirm(`هل أنت متأكد من حذف المستفيد برقم الحساب ${account}؟`)) {
                alert(`تم حذف المستفيد برقم الحساب: ${account}`);
            }
        }
        
        function addBeneficiary() {
            alert('فتح نموذج إضافة مستفيد جديد');
        }
        
        // وظائف قاعدة البيانات
        function createBackup() {
            alert('جاري إنشاء نسخة احتياطية على Google Drive...');
        }
        
        function restoreBackup() {
            alert('جاري استرداد نسخة احتياطية من Google Drive...');
        }
        
        // وظائف إعدادات النوافذ
        function configureWindow(windowType) {
            alert(`فتح إعدادات نوافذ ${windowType}`);
        }
        
        // وظائف اللغة
        function saveLanguage() {
            const language = document.getElementById('languageSelect').value;
            alert(`تم حفظ إعدادات اللغة: ${language}`);
            closeWindow('languageWindow');
        }
        
        // وظائف الملف الشخصي
        function changeProfilePicture() {
            alert('فتح معرض الصور لتغيير صورة الملف الشخصي');
        }
        
        // وظائف الخدمات
        function openService(service) {
            if (service === 'bank-services') {
                openWindow('bankServicesWindow');
            } else if (service === 'kuraimi-express') {
                openWindow('kuraimiExpressWindow');
            } else if (service === 'payment-services') {
                openWindow('paymentServicesWindow');
            } else if (service === 'am-floos') {
                openWindow('amFloosWindow');
            } else if (service === 'financing') {
                openWindow('financingWindow');
            } else if (service === 'vouchers') {
                openWindow('vouchersWindow');
            } else if (service === 'card-services') {
                openWindow('cardServicesWindow');
            } else if (service === 'other-services') {
                openWindow('otherServicesWindow');
            }
        }
        
        function openTransferToNumber() {
            closeWindow('kuraimiExpressWindow');
            openWindow('transferToNumberWindow');
        }
        
        function openTransferToName() {
            closeWindow('kuraimiExpressWindow');
            openWindow('transferToNameWindow');
        }
        
        function openTransferToAccount() {
            alert('فتح خدمة دفع حوالة إلى حساب');
        }
        
        function openCancelTransfer() {
            alert('فتح خدمة إلغاء حوالة');
        }
        
        function openTransferStatus() {
            alert('فتح خدمة حالة الحوالة');
        }
        
        function openActivateEShopping() {
            alert('فتح خدمة تفعيل التسوق الإلكتروني');
        }
        
        function openPaymentServices() {
            alert('فتح خدمات السداد');
        }
        
        function openPayPurchases() {
            alert('فتح خدمة دفع قيمة المشتريات');
        }
        
        function openPaymentList() {
            alert('فتح قائمة حاسب');
        }
        
        function openTransferToAmFloos() {
            alert('فتح خدمة التحويل إلى حساب أم فلوس');
        }
        
        function openCashWithdrawal() {
            alert('فتح خدمة السحب النقدي من وكيل أم فلوس');
        }
        
        function openCancelWithdrawal() {
            alert('فتح خدمة إلغاء عملية السحب النقدي');
        }
        
        function openInstallmentPayment() {
            alert('فتح خدمة سداد القسط');
        }
        
        function openInstallmentList() {
            alert('فتح قائمة الأقساط');
        }
        
        function openFinanceRequest() {
            alert('فتح خدمة طلب تمويل');
        }
        
        function openCreateVoucher() {
            alert('فتح خدمة إنشاء قسيمة');
        }
        
        function openRedeemVoucher() {
            alert('فتح خدمة استرداد قسيمة');
        }
        
        function openVouchersList() {
            alert('فتح خدمة القسائم');
        }
        
        function openCardServices() {
            alert('فتح خدمات البطاقة');
        }
        
        function openChangePassword() {
            alert('فتح خدمة تغيير كلمة المرور');
        }
        
        function openLocation() {
            alert('فتح خدمة الموقع');
        }
        
        function openWebsite() {
            alert('فتح موقعنا على الإنترنت');
        }
        
        function openSocialMedia() {
            alert('فتح صفحاتنا على التواصل الاجتماعي');
        }
        
        function openAddAlert() {
            alert('فتح خدمة إضافة تنبيه');
        }
        
        function openSearch() {
            alert('فتح شاشة البحث');
        }
        
        // وظائف البطاقات
        function toggleBalance(button) {
            const balance = button.parentElement.querySelector('.balance-amount');
            if (balance.style.filter === 'blur(5px)') {
                balance.style.filter = 'none';
                button.textContent = '👁️';
            } else {
                balance.style.filter = 'blur(5px)';
                button.textContent = '👁️‍🗨️';
            }
        }
        
        function copyToClipboard(text) {
            navigator.clipboard.writeText(text).then(() => {
                alert('تم نسخ رقم الحساب: ' + text);
            });
        }
        
        function showQR(accountNumber) {
            alert(`عرض رمز QR للحساب: ${accountNumber}`);
        }
        
        function showStatement() {
            alert('عرض كشف الحساب');
        }
        
        function showAccountServices(accountNumber) {
            alert(`عرض خدمات الحساب: ${accountNumber}`);
        }
        
        function updateBranches() {
            const regionSelect = document.getElementById('region');
            const branchSelect = document.getElementById('branch');
            const selectedRegion = regionSelect.value;
            
            branchSelect.innerHTML = '<option value="">اختر الفرع</option>';
            
            if (selectedRegion) {
                branchSelect.disabled = false;
                branches[selectedRegion].forEach(branch => {
                    const option = document.createElement('option');
                    option.value = branch;
                    option.textContent = branch;
                    branchSelect.appendChild(option);
                });
            } else {
                branchSelect.disabled = true;
            }
        }
        
        // القوائم المنسدلة للمناطق والفروع
        document.getElementById('region').addEventListener('change', updateBranches);
        
        // إعدادات القائمة
        function openLanguageSettings() {
            openWindow('languageWindow');
        }
        
        function openDatabaseSettings() {
            openWindow('databaseWindow');
        }
        
        function openWindowSettings() {
            openWindow('windowSettingsWindow');
        }
        
        function logout() {
            if (confirm('هل أنت متأكد من تسجيل الخروج؟')) {
                alert('تم تسجيل الخروج بنجاح');
                // في التطبيق الفعلي، سيتم إعادة التوجيه إلى صفحة تسجيل الدخول
            }
        }
        
        function openProfile() {
            openWindow('profileWindow');
        }
    </script>
</body>
</html>

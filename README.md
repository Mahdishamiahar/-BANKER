# -BANKER
<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>بنر ساز حرفه‌ای</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://html2canvas.hertzen.com/dist/html2canvas.min.js"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <style>
    @font-face {
      font-family: 'Vazir';
      src: url('https://cdn.fontcdn.ir/Font/Persian/Vazir/Vazir.ttf');
    }
    * {
      font-family: 'Vazir', sans-serif;
    }
    .banner-frame {
      transition: all 0.3s ease;
      overflow: hidden;
    }
    .modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.7);
      z-index: 1000;
      align-items: center;
      justify-content: center;
    }
    .tab-content {
      display: none;
    }
    .tab-content.active {
      display: block;
    }
    .saved-banner {
      transition: all 0.3s ease;
      cursor: pointer;
    }
    .saved-banner:hover {
      transform: scale(1.05);
    }
    .frame-1 {
      border: 15px solid #3b82f6;
      border-radius: 5px;
    }
    .frame-2 {
      border: 10px dashed #f59e0b;
    }
    .frame-3 {
      border: 20px double #10b981;
    }
    .frame-4 {
      border: 5px solid #8b5cf6;
      box-shadow: 0 0 20px rgba(139, 92, 246, 0.5);
    }
    .frame-5 {
      border-top: 10px solid #ef4444;
      border-bottom: 10px solid #ef4444;
      background: linear-gradient(to right, rgba(239, 68, 68, 0.1), rgba(239, 68, 68, 0.3));
    }
    .text-effect-1 {
      text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
    }
    .text-effect-2 {
      background: linear-gradient(to right, #f97316, #f43f5e);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
    }
    .text-effect-3 {
      letter-spacing: 2px;
      font-weight: bold;
    }
    .text-effect-4 {
      text-shadow: 0 0 10px rgba(255, 255, 255, 0.8), 0 0 20px rgba(255, 255, 255, 0.5);
    }
    #bannerPreview {
      transition: all 0.3s ease;
    }
    
    /* استایل‌های بخش هوش مصنوعی */
    :root { 
      --bg-dark:#0d1117; 
      --text-light:#fff; 
      --brand:#58a6ff; 
      --success:#238636; 
      --card-dark:rgba(33,38,45,0.9);
    }
    .ai-chat-container {
      background: var(--bg-dark);
      color: var(--text-light);
      border-radius: 15px;
      overflow: hidden;
      height: 500px;
      display: flex;
      flex-direction: column;
    }
    .ai-chat-header {
      background:#161b22;
      padding:12px;
      display:flex;
      align-items:center;
      justify-content:space-between;
      border-bottom:1px solid #30363d;
      font-size:16px;
    }
    .ai-chat-window {
      flex:1;
      overflow-y:auto;
      padding:10px;
      display:flex;
      flex-direction:column;
      gap:8px;
    }
    .ai-message {
      max-width:85%;
      padding:10px 14px;
      border-radius:12px;
      line-height:1.4;
      white-space:pre-wrap;
      position:relative;
      animation:fadeIn 0.3s ease-in-out;
      word-break: break-word;
      font-size:14px;
      display:flex;
      align-items:flex-start;
      gap:5px;
    }
    .ai-user {
      background:var(--success);
      color:#fff;
      align-self:flex-end;
      border-bottom-right-radius:0;
    }
    .ai-bot {
      background:var(--card-dark);
      color:#fff;
      align-self:flex-start;
      border-bottom-left-radius:0;
    }
    .ai-msg-time {
      font-size:10px;
      opacity:0.6;
      text-align:left;
      margin-top:2px;
    }
    .ai-msg-user {
      font-weight:bold;
      font-size:12px;
    }
    .ai-input-area {
      display:flex;
      padding:8px;
      border-top:1px solid #30363d;
      background:#161b22;
      gap:5px;
      align-items:center;
    }
    .ai-user-input {
      flex:1;
      padding:10px;
      border:none;
      border-radius:8px;
      background:var(--bg-dark);
      color:var(--text-light);
      font-size:15px;
    }
    .ai-send-btn, .ai-upload-btn {
      padding:10px 12px;
      background:var(--brand);
      border:none;
      border-radius:8px;
      cursor:pointer;
      color:#fff;
      font-size:14px;
    }
    .ai-send-btn:hover, .ai-upload-btn:hover {
      background:#1f6feb;
    }
    .ai-typing {
      font-style:italic;
      opacity:0.7;
    }
    .ai-message img {
      max-width:120px;
      border-radius:50%;
      display:block;
    }
    @keyframes fadeIn { 
      from{opacity:0; transform:translateY(5px);} 
      to{opacity:1; transform:translateY(0);} 
    }
  </style>
</head>
<body class="bg-gradient-to-br from-blue-50 via-purple-50 to-pink-50 min-h-screen p-4">
  <div class="container mx-auto max-w-6xl">
    <!-- هدر -->
    <header class="bg-white rounded-2xl shadow-lg p-6 mb-6 flex flex-col md:flex-row justify-between items-center">
      <div>
        <h1 class="text-3xl font-extrabold text-blue-600"><i class="fas fa-image mr-2"></i>بنر ساز حرفه‌ای</h1>
        <p class="text-gray-600 mt-2">ساخت بنرهای زیبا و حرفه‌ای در کمتر از چند دقیقه</p>
      </div>
      <div class="flex gap-2 mt-4 md:mt-0">
        <button id="aboutBtn" class="bg-blue-100 text-blue-700 px-4 py-2 rounded-lg shadow hover:bg-blue-200">
          <i class="fas fa-info-circle mr-1"></i>درباره
        </button>
        <button id="helpBtn" class="bg-green-100 text-green-700 px-4 py-2 rounded-lg shadow hover:bg-green-200">
          <i class="fas fa-question-circle mr-1"></i>راهنما
        </button>
      </div>
    </header>

    <div class="flex flex-col lg:flex-row gap-6">
      <!-- سایدبار -->
      <div class="w-full lg:w-1/4 bg-white rounded-2xl shadow-lg p-5 h-fit">
        <div class="tabs flex flex-col gap-2">
          <button class="tab-btn py-3 px-4 text-right rounded-lg bg-blue-100 text-blue-700 font-semibold" data-tab="design">
            <i class="fas fa-paint-brush ml-2"></i>طراحی بنر
          </button>
          <button class="tab-btn py-3 px-4 text-right rounded-lg hover:bg-gray-100" data-tab="frames">
            <i class="fas fa-border-all ml-2"></i>قاب‌ها
          </button>
          <button class="tab-btn py-3 px-4 text-right rounded-lg hover:bg-gray-100" data-tab="gallery">
            <i class="fas fa-images ml-2"></i>گالری بنرها
          </button>
          <button class="tab-btn py-3 px-4 text-right rounded-lg hover:bg-gray-100" data-tab="saved">
            <i class="fas fa-save ml-2"></i>بنرهای ذخیره شده
          </button>
          <button class="tab-btn py-3 px-4 text-right rounded-lg hover:bg-gray-100" data-tab="effects">
            <i class="fas fa-magic ml-2"></i>افکت‌ها
          </button>
          <button class="tab-btn py-3 px-4 text-right rounded-lg hover:bg-gray-100" data-tab="ai">
            <i class="fas fa-robot ml-2"></i>هوش مصنوعی
          </button>
        </div>

        <div class="mt-6">
          <h3 class="font-semibold text-gray-700 mb-3">ذخیره و بارگذاری</h3>
          <button id="saveBannerBtn" class="w-full bg-green-500 text-white p-2 rounded-lg mb-2 hover:bg-green-600">
            <i class="fas fa-save ml-2"></i>ذخیره بنر
          </button>
          <button id="loadBannerBtn" class="w-full bg-blue-500 text-white p-2 rounded-lg mb-2 hover:bg-blue-600">
            <i class="fas fa-upload ml-2"></i>بارگذاری بنر
          </button>
          <button id="resetBannerBtn" class="w-full bg-red-500 text-white p-2 rounded-lg hover:bg-red-600">
            <i class="fas fa-trash-alt ml-2"></i>بازنشانی
          </button>
        </div>
      </div>

      <!-- محتوای اصلی -->
      <div class="flex-1">
        <div class="tab-content active" id="design-tab">
          <div class="bg-white rounded-2xl shadow-lg p-6 mb-6">
            <h2 class="text-xl font-bold text-gray-800 mb-4"><i class="fas fa-sliders-h ml-2"></i>تنظیمات بنر</h2>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
              <div>
                <label class="text-sm font-semibold">متن بنر</label>
                <input id="bannerText" type="text" class="mt-1 w-full p-2 border rounded-lg" placeholder="متن خود را وارد کنید" value="بنر نمونه">
              </div>
              <div>
                <label class="text-sm font-semibold">رنگ پس‌زمینه</label>
                <input id="bgColor" type="color" class="mt-1 w-full h-10 border rounded-lg" value="#2563eb">
              </div>
              <div>
                <label class="text-sm font-semibold">تصویر پس‌زمینه</label>
                <input id="bgImage" type="file" accept="image/*" class="mt-1 w-full p-2 border rounded-lg">
              </div>
              <div>
                <label class="text-sm font-semibold">رنگ متن</label>
                <input id="textColor" type="color" class="mt-1 w-full h-10 border rounded-lg" value="#ffffff">
              </div>
              <div>
                <label class="text-sm font-semibold">اندازه فونت</label>
                <div class="flex items-center mt-1">
                  <input id="fontSize" type="range" min="10" max="100" value="24" class="w-full">
                  <span id="fontSizeValue" class="mr-2 w-10 text-center">24px</span>
                </div>
              </div>
              <div>
                <label class="text-sm font-semibold">نوع فونت</label>
                <select id="fontFamily" class="mt-1 w-full p-2 border rounded-lg">
                  <option value="Vazir">وزیر</option>
                  <option value="Arial">Arial</option>
                  <option value="Tahoma">Tahoma</option>
                  <option value="Georgia">Georgia</option>
                </select>
              </div>
              <div>
                <label class="text-sm font-semibold">اضافه کردن لوگو</label>
                <input id="logoImage" type="file" accept="image/*" class="mt-1 w-full p-2 border rounded-lg">
              </div>
              <div>
                <label class="text-sm font-semibold">تراز متن</label>
                <select id="textAlign" class="mt-1 w-full p-2 border rounded-lg">
                  <option value="center">وسط</option>
                  <option value="right">راست</option>
                  <option value="left">چپ</option>
                </select>
              </div>
            </div>
          </div>
        </div>

        <div class="tab-content" id="frames-tab">
          <div class="bg-white rounded-2xl shadow-lg p-6 mb-6">
            <h2 class="text-xl font-bold text-gray-800 mb-4"><i class="fas fa-border-all ml-2"></i>انتخاب قاب</h2>
            <div class="grid grid-cols-2 md:grid-cols-3 gap-4">
              <div class="frame-option border-2 border-gray-200 p-2 rounded-lg cursor-pointer" data-frame="none">
                <div class="h-20 bg-gray-100 rounded flex items-center justify-center">بدون قاب</div>
              </div>
              <div class="frame-option border-2 border-gray-200 p-2 rounded-lg cursor-pointer" data-frame="frame-1">
                <div class="h-20 bg-gray-100 rounded frame-1 flex items-center justify-center">قاب 1</div>
              </div>
              <div class="frame-option border-2 border-gray-200 p-2 rounded-lg cursor-pointer" data-frame="frame-2">
                <div class="h-20 bg-gray-100 rounded frame-2 flex items-center justify-center">قاب 2</div>
              </div>
              <div class="frame-option border-2 border-gray-200 p-2 rounded-lg cursor-pointer" data-frame="frame-3">
                <div class="h-20 bg-gray-100 rounded frame-3 flex items-center justify-center">قاب 3</div>
              </div>
              <div class="frame-option border-2 border-gray-200 p-2 rounded-lg cursor-pointer" data-frame="frame-4">
                <div class="h-20 bg-gray-100 rounded frame-4 flex items-center justify-center">قاب 4</div>
              </div>
              <div class="frame-option border-2 border-gray-200 p-2 rounded-lg cursor-pointer" data-frame="frame-5">
                <div class="h-20 bg-gray-100 rounded frame-5 flex items-center justify-center">قاب 5</div>
              </div>
            </div>
          </div>
        </div>

        <div class="tab-content" id="effects-tab">
          <div class="bg-white rounded-2xl shadow-lg p-6 mb-6">
            <h2 class="text-xl font-bold text-gray-800 mb-4"><i class="fas fa-magic ml-2"></i>افکت‌های متنی</h2>
            <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
              <div class="effect-option border-2 border-gray-200 p-2 rounded-lg cursor-pointer" data-effect="none">
                <div class="h-16 bg-gray-100 rounded flex items-center justify-center">بدون افکت</div>
              </div>
              <div class="effect-option border-2 border-gray-200 p-2 rounded-lg cursor-pointer" data-effect="text-effect-1">
                <div class="h-16 bg-gray-100 rounded flex items-center justify-center text-effect-1">سایه دار</div>
              </div>
              <div class="effect-option border-2 border-gray-200 p-2 rounded-lg cursor-pointer" data-effect="text-effect-2">
                <div class="h-16 bg-gray-100 rounded flex items-center justify-center text-effect-2">گرادینت</div>
              </div>
              <div class="effect-option border-2 border-gray-200 p-2 rounded-lg cursor-pointer" data-effect="text-effect-3">
                <div class="h-16 bg-gray-100 rounded flex items-center justify-center text-effect-3">ضخیم</div>
              </div>
              <div class="effect-option border-2 border-gray-200 p-2 rounded-lg cursor-pointer" data-effect="text-effect-4">
                <div class="h-16 bg-gray-100 rounded flex items-center justify-center text-effect-4">نئون</div>
              </div>
            </div>
          </div>
        </div>

        <div class="tab-content" id="gallery-tab">
          <div class="bg-white rounded-2xl shadow-lg p-6 mb-6">
            <h2 class="text-xl font-bold text-gray-800 mb-4"><i class="fas fa-images ml-2"></i>گالری بنرهای آماده</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
              <div class="saved-banner bg-blue-100 p-4 rounded-lg" data-banner="banner1">
                <div class="h-32 bg-blue-500 rounded-lg flex items-center justify-center text-white text-xl font-bold">
                  بنر تبلیغاتی
                </div>
                <p class="text-center mt-2">بنر آبی ساده</p>
              </div>
              <div class="saved-banner bg-red-100 p-4 rounded-lg" data-banner="banner2">
                <div class="h-32 bg-red-500 rounded-lg flex items-center justify-center text-white text-xl font-bold">
                  تخفیف ویژه
                </div>
                <p class="text-center mt-2">بنر قرمز تخفیف</p>
              </div>
              <div class="saved-banner bg-green-100 p-4 rounded-lg" data-banner="banner3">
                <div class="h-32 bg-green-500 rounded-lg flex items-center justify-center text-white text-xl font-bold">
                  جدیدترین محصولات
                </div>
                <p class="text-center mt-2">بنر سبز محصولات</p>
              </div>
              <div class="saved-banner bg-purple-100 p-4 rounded-lg" data-banner="banner4">
                <div class="h-32 bg-purple-500 rounded-lg flex items-center justify-center text-white text-xl font-bold">
                  رویداد ویژه
                </div>
                <p class="text-center mt-2">بنر بنفش رویداد</p>
              </div>
            </div>
          </div>
        </div>

        <div class="tab-content" id="saved-tab">
          <div class="bg-white rounded-2xl shadow-lg p-6 mb-6">
            <h2 class="text-xl font-bold text-gray-800 mb-4"><i class="fas fa-save ml-2"></i>بنرهای ذخیره شده شما</h2>
            <div id="userBannersList" class="grid grid-cols-1 md:grid-cols-2 gap-4">
              <p class="text-gray-500 text-center py-4">هیچ بنری ذخیره نکرده‌اید</p>
            </div>
          </div>
        </div>

        <!-- تب هوش مصنوعی -->
        <div class="tab-content" id="ai-tab">
          <div class="bg-white rounded-2xl shadow-lg p-6 mb-6">
            <h2 class="text-xl font-bold text-gray-800 mb-4"><i class="fas fa-robot ml-2"></i>چت هوش مصنوعی</h2>
            <div class="ai-chat-container">
              <div class="ai-chat-header">
                <h3>🤖 VIPZEXNET</h3>
                <div id="ai-menuContainer">
                  <button id="ai-menuBtn" style="background:none;border:none;color:var(--brand);font-size:18px;cursor:pointer;">⋮</button>
                  <div id="ai-historyMenu" style="display:none; position:absolute; background:#161b22; border:1px solid #30363d; border-radius:6px; min-width:180px; z-index:100; max-height:250px; overflow-y:auto; font-size:14px;">
                    <button id="ai-newChat" style="width:100%; padding:6px; border:none; background:none; color:#fff; text-align:right; cursor:pointer; font-size:14px;">🆕 چت جدید</button>
                    <button id="ai-profileBtn" style="width:100%; padding:6px; border:none; background:none; color:#fff; text-align:right; cursor:pointer; font-size:14px;">👤 پروفایل</button>
                    <div id="ai-chatHistoryList"></div>
                  </div>
                </div>
              </div>

              <div id="ai-chatWindow" class="ai-chat-window"></div>

              <div class="ai-input-area">
                <button id="ai-uploadBtn" class="ai-upload-btn">📎</button>
                <input type="text" id="ai-userInput" class="ai-user-input" placeholder="پیام خود را بنویسید...">
                <button id="ai-sendBtn" class="ai-send-btn">ارسال</button>
              </div>
            </div>
          </div>
        </div>

        <!-- پیش نمایش بنر -->
        <div class="bg-white rounded-2xl shadow-lg p-6">
          <h2 class="text-xl font-bold text-gray-800 mb-4"><i class="fas fa-eye ml-2"></i>پیش نمایش بنر</h2>
          <div id="bannerPreview" class="w-full h-64 flex items-center justify-center text-center rounded-xl overflow-hidden relative" style="background-color: #2563eb; color: #ffffff; font-family: Vazir; font-size: 24px;">
            بنر نمونه
            <img id="logoPreview" class="absolute top-4 left-4 w-12 h-12 hidden" src="" alt="لوگو">
          </div>
          
          <div class="flex flex-wrap gap-2 mt-4">
            <button id="downloadBtn" class="flex-1 bg-blue-600 text-white font-bold p-3 rounded-xl shadow-lg hover:bg-blue-700 transition">
              <i class="fas fa-download ml-2"></i>دانلود بنر
            </button>
            <button id="shareBtn" class="flex-1 bg-green-600 text-white font-bold p-3 rounded-xl shadow-lg hover:bg-green-700 transition">
              <i class="fas fa-share-alt ml-2"></i>اشتراک‌گذاری
            </button>
            <button id="printBtn" class="flex-1 bg-purple-600 text-white font-bold p-3 rounded-xl shadow-lg hover:bg-purple-700 transition">
              <i class="fas fa-print ml-2"></i>چاپ بنر
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- مودال درباره -->
  <div id="aboutModal" class="modal">
    <div class="modal-content">
      <h2 class="text-xl font-bold mb-4">درباره برنامه</h2>
      <p class="text-gray-700 mb-2">ایمیل: mahdishamiahar@gmail.com</p>
      <p class="text-gray-700 mb-2">توسعه‌دهنده: مهدی شامی</p>
      <p class="text-gray-700 mb-4">شماره: 09142500486</p>
      <button id="closeAboutModal" class="w-full bg-blue-100 text-blue-800 p-2 rounded-lg hover:bg-blue-200">بستن</button>
    </div>
  </div>

  <!-- مودال راهنما -->
  <div id="helpModal" class="modal">
    <div class="modal-content">
      <h2 class="text-xl font-bold mb-4">راهنمای استفاده</h2>
      <ul class="list-disc pr-4 text-gray-700 space-y-2">
        <li>برای تغییر متن بنر، در قسمت "متن بنر" متن مورد نظر خود را وارد کنید.</li>
        <li>برای تغییر رنگ پس‌زمینه، از انتخابگر رنگ استفاده کنید.</li>
        <li>برای اضافه کردن تصویر پس‌زمینه، از دکمه "انتخاب فایل" استفاده کنید.</li>
        <li>از تب‌های مختلف برای دسترسی به قاب‌ها، افکت‌ها و گالری استفاده کنید.</li>
        <li>برای ذخیره بنر، روی دکمه "ذخیره بنر" کلیک کنید.</li>
        <li>برای دانلود بنر نهایی، روی دکمه "دانلود بنر" کلیک کنید.</li>
      </ul>
      <button id="closeHelpModal" class="w-full bg-blue-100 text-blue-800 p-2 rounded-lg mt-4 hover:bg-blue-200">بستن</button>
    </div>
  </div>

  <!-- مودال پروفایل هوش مصنوعی -->
  <div id="ai-profileModal" style="display:none; position:fixed; top:50%; left:50%; transform:translate(-50%,-50%); background:#161b22; border:1px solid #30363d; border-radius:10px; padding:15px; z-index:200; width:90%; max-width:300px; color:#fff;">
    <h3>پروفایل</h3>
    <label>نام:</label><input type="text" id="ai-profileName" style="width:100%; margin-bottom:8px; padding:6px; background:#0d1117; color:#fff; border:1px solid #30363d; border-radius:5px; font-size:14px;">
    <label>ایمیل:</label><input type="email" id="ai-profileEmail" style="width:100%; margin-bottom:8px; padding:6px; background:#0d1117; color:#fff; border:1px solid #30363d; border-radius:5px; font-size:14px;">
    <label>عکس پروفایل:</label><input type="file" id="ai-profileAvatar" accept="image/*" style="width:100%; margin-bottom:8px; font-size:14px;">
    <div style="text-align:right;">
      <button id="ai-saveProfile" style="cursor:pointer; border:none; border-radius:5px; padding:5px 10px; font-size:14px; background:var(--success); color:#fff; margin-left:5px;">ذخیره</button>
      <button id="ai-closeProfile" style="cursor:pointer; border:none; border-radius:5px; padding:5px 10px; font-size:14px; background:#30363d; color:#fff;">بستن</button>
    </div>
  </div>

  <input type="file" id="ai-fileInput" style="display:none" accept="image/*,.txt">

  <script>
    // عناصر DOM
    const bannerText = document.getElementById('bannerText');
    const bgColor = document.getElementById('bgColor');
    const bgImage = document.getElementById('bgImage');
    const textColor = document.getElementById('textColor');
    const fontSize = document.getElementById('fontSize');
    const fontSizeValue = document.getElementById('fontSizeValue');
    const fontFamily = document.getElementById('fontFamily');
    const textAlign = document.getElementById('textAlign');
    const logoImage = document.getElementById('logoImage');
    const bannerPreview = document.getElementById('bannerPreview');
    const logoPreview = document.getElementById('logoPreview');
    const downloadBtn = document.getElementById('downloadBtn');
    const saveBannerBtn = document.getElementById('saveBannerBtn');
    const loadBannerBtn = document.getElementById('loadBannerBtn');
    const resetBannerBtn = document.getElementById('resetBannerBtn');
    const shareBtn = document.getElementById('shareBtn');
    const printBtn = document.getElementById('printBtn');
    const aboutBtn = document.getElementById('aboutBtn');
    const helpBtn = document.getElementById('helpBtn');
    const aboutModal = document.getElementById('aboutModal');
    const helpModal = document.getElementById('helpModal');
    const closeAboutModal = document.getElementById('closeAboutModal');
    const closeHelpModal = document.getElementById('closeHelpModal');
    const tabBtns = document.querySelectorAll('.tab-btn');
    const tabContents = document.querySelectorAll('.tab-content');
    const frameOptions = document.querySelectorAll('.frame-option');
    const effectOptions = document.querySelectorAll('.effect-option');
    const savedBanners = document.querySelectorAll('.saved-banner');
    const userBannersList = document.getElementById('userBannersList');

    // عناصر بخش هوش مصنوعی
    const aiChatWindow = document.getElementById('ai-chatWindow');
    const aiUserInput = document.getElementById('ai-userInput');
    const aiSendBtn = document.getElementById('ai-sendBtn');
    const aiUploadBtn = document.getElementById('ai-uploadBtn');
    const aiFileInput = document.getElementById('ai-fileInput');
    const aiMenuBtn = document.getElementById('ai-menuBtn');
    const aiHistoryMenu = document.getElementById('ai-historyMenu');
    const aiNewChat = document.getElementById('ai-newChat');
    const aiProfileBtn = document.getElementById('ai-profileBtn');
    const aiChatHistoryList = document.getElementById('ai-chatHistoryList');
    const aiProfileModal = document.getElementById('ai-profileModal');
    const aiProfileName = document.getElementById('ai-profileName');
    const aiProfileEmail = document.getElementById('ai-profileEmail');
    const aiProfileAvatar = document.getElementById('ai-profileAvatar');
    const aiSaveProfile = document.getElementById('ai-saveProfile');
    const aiCloseProfile = document.getElementById('ai-closeProfile');

    // مقداردهی اولیه
    let currentFrame = 'none';
    let currentEffect = 'none';
    let userBanners = JSON.parse(localStorage.getItem('userBanners')) || [];
    let selectedModel = "openai-large";

    // نمایش اندازه فونت
    fontSizeValue.textContent = `${fontSize.value}px`;

    // به روزرسانی بنر
    function updateBanner() {
      bannerPreview.textContent = bannerText.value;
      bannerPreview.style.backgroundColor = bgColor.value;
      bannerPreview.style.color = textColor.value;
      bannerPreview.style.fontSize = `${fontSize.value}px`;
      bannerPreview.style.fontFamily = fontFamily.value;
      bannerPreview.style.textAlign = textAlign.value;
      
      // اعمال قاب انتخاب شده
      frameOptions.forEach(option => {
        bannerPreview.classList.remove(option.dataset.frame);
      });
      if (currentFrame !== 'none') {
        bannerPreview.classList.add(currentFrame);
      }
      
      // اعمال افکت انتخاب شده
      effectOptions.forEach(option => {
        bannerPreview.classList.remove(option.dataset.effect);
      });
      if (currentEffect !== 'none') {
        bannerPreview.classList.add(currentEffect);
      }
    }

    // تغییر تب‌ها
    tabBtns.forEach(btn => {
      btn.addEventListener('click', () => {
        const tabId = `${btn.dataset.tab}-tab`;
        
        // غیرفعال کردن همه تب‌ها
        tabBtns.forEach(b => b.classList.remove('bg-blue-100', 'text-blue-700'));
        tabContents.forEach(content => content.classList.remove('active'));
        
        // فعال کردن تب انتخاب شده
        btn.classList.add('bg-blue-100', 'text-blue-700');
        document.getElementById(tabId).classList.add('active');
      });
    });

    // انتخاب قاب
    frameOptions.forEach(option => {
      option.addEventListener('click', () => {
        currentFrame = option.dataset.frame;
        updateBanner();
      });
    });

    // انتخاب افکت
    effectOptions.forEach(option => {
      option.addEventListener('click', () => {
        currentEffect = option.dataset.effect;
        updateBanner();
      });
    });

    // رویدادهای ورودی
    bannerText.addEventListener('input', updateBanner);
    bgColor.addEventListener('input', updateBanner);
    textColor.addEventListener('input', updateBanner);
    fontSize.addEventListener('input', () => {
      fontSizeValue.textContent = `${fontSize.value}px`;
      updateBanner();
    });
    fontFamily.addEventListener('change', updateBanner);
    textAlign.addEventListener('change', updateBanner);

    bgImage.addEventListener('change', function () {
      const file = bgImage.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = function (e) {
          bannerPreview.style.backgroundImage = `url('${e.target.result}')`;
        };
        reader.readAsDataURL(file);
      } else {
        bannerPreview.style.backgroundImage = '';
      }
    });

    logoImage.addEventListener('change', function () {
      const file = logoImage.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = function (e) {
          logoPreview.src = e.target.result;
          logoPreview.classList.remove('hidden');
        };
        reader.readAsDataURL(file);
      } else {
        logoPreview.src = '';
        logoPreview.classList.add('hidden');
      }
    });

    // دانلود بنر
    downloadBtn.addEventListener('click', function () {
      html2canvas(bannerPreview).then(canvas => {
        const link = document.createElement('a');
        link.download = 'banner.png';
        link.href = canvas.toDataURL('image/png');
        link.click();
      });
    });

    // ذخیره بنر
    saveBannerBtn.addEventListener('click', function() {
      const bannerData = {
        text: bannerText.value,
        bgColor: bgColor.value,
        textColor: textColor.value,
        fontSize: fontSize.value,
        fontFamily: fontFamily.value,
        textAlign: textAlign.value,
        frame: currentFrame,
        effect: currentEffect,
        bgImage: bannerPreview.style.backgroundImage || '',
        logo: logoPreview.src || '',
        timestamp: new Date().toLocaleString('fa-IR')
      };
      
      userBanners.push(bannerData);
      localStorage.setItem('userBanners', JSON.stringify(userBanners));
      alert('بنر با موفقیت ذخیره شد!');
      updateUserBannersList();
    });

    // بارگذاری بنرهای ذخیره شده
    function updateUserBannersList() {
      if (userBanners.length === 0) {
        userBannersList.innerHTML = '<p class="text-gray-500 text-center py-4">هیچ بنری ذخیره نکرده‌اید</p>';
        return;
      }
      
      userBannersList.innerHTML = '';
      userBanners.forEach((banner, index) => {
        const bannerEl = document.createElement('div');
        bannerEl.className = 'saved-banner bg-gray-100 p-4 rounded-lg';
        bannerEl.innerHTML = `
          <div class="h-32 rounded-lg flex items-center justify-center text-white text-xl font-bold" style="background-color: ${banner.bgColor}; color: ${banner.textColor}; font-family: ${banner.fontFamily}; font-size: ${banner.fontSize}px; text-align: ${banner.textAlign}; background-image: ${banner.bgImage}">
            ${banner.text}
            ${banner.logo ? `<img src="${banner.logo}" class="absolute top-2 left-2 w-10 h-10">` : ''}
          </div>
          <p class="text-center mt-2">ذخیره شده در: ${banner.timestamp}</p>
          <div class="flex gap-2 mt-2">
            <button class="load-banner-btn bg-blue-500 text-white p-1 rounded flex-1" data-index="${index}">بارگذاری</button>
            <button class="delete-banner-btn bg-red-500 text-white p-1 rounded flex-1" data-index="${index}">حذف</button>
          </div>
        `;
        userBannersList.appendChild(bannerEl);
      });
      
      // اضافه کردن رویداد به دکمه‌های بارگذاری و حذف
      document.querySelectorAll('.load-banner-btn').forEach(btn => {
        btn.addEventListener('click', (e) => {
          const index = e.target.dataset.index;
          loadBanner(userBanners[index]);
        });
      });
      
      document.querySelectorAll('.delete-banner-btn').forEach(btn => {
        btn.addEventListener('click', (e) => {
          const index = e.target.dataset.index;
          userBanners.splice(index, 1);
          localStorage.setItem('userBanners', JSON.stringify(userBanners));
          updateUserBannersList();
        });
      });
    }

    // بارگذاری بنر
    function loadBanner(bannerData) {
      bannerText.value = bannerData.text;
      bgColor.value = bannerData.bgColor;
      textColor.value = bannerData.textColor;
      fontSize.value = bannerData.fontSize;
      fontSizeValue.textContent = `${bannerData.fontSize}px`;
      fontFamily.value = bannerData.fontFamily;
      textAlign.value = bannerData.textAlign;
      currentFrame = bannerData.frame;
      currentEffect = bannerData.effect;
      bannerPreview.style.backgroundImage = bannerData.bgImage;
      
      if (bannerData.logo) {
        logoPreview.src = bannerData.logo;
        logoPreview.classList.remove('hidden');
      } else {
        logoPreview.src = '';
        logoPreview.classList.add('hidden');
      }
      
      updateBanner();
      alert('بنر با موفقیت بارگذاری شد!');
    }

    // بارگذاری بنرهای آماده
    savedBanners.forEach(banner => {
      banner.addEventListener('click', () => {
        const bannerType = banner.dataset.banner;
        let bannerData = {};
        
        switch(bannerType) {
          case 'banner1':
            bannerData = {
              text: 'بنر تبلیغاتی',
              bgColor: '#3b82f6',
              textColor: '#ffffff',
              fontSize: 28,
              fontFamily: 'Vazir',
              textAlign: 'center',
              frame: 'frame-1',
              effect: 'text-effect-1'
            };
            break;
          case 'banner2':
            bannerData = {
              text: 'تخفیف ویژه',
              bgColor: '#ef4444',
              textColor: '#ffffff',
              fontSize: 32,
              fontFamily: 'Vazir',
              textAlign: 'center',
              frame: 'frame-2',
              effect: 'text-effect-3'
            };
            break;
          case 'banner3':
            bannerData = {
              text: 'جدیدترین محصولات',
              bgColor: '#10b981',
              textColor: '#ffffff',
              fontSize: 26,
              fontFamily: 'Vazir',
              textAlign: 'center',
              frame: 'frame-4',
              effect: 'text-effect-4'
            };
            break;
          case 'banner4':
            bannerData = {
              text: 'رویداد ویژه',
              bgColor: '#8b5cf6',
              textColor: '#ffffff',
              fontSize: 30,
              fontFamily: 'Vazir',
              textAlign: 'center',
              frame: 'frame-3',
              effect: 'text-effect-2'
            };
            break;
        }
        
        loadBanner(bannerData);
      });
    });

    // بازنشانی بنر
    resetBannerBtn.addEventListener('click', function() {
      if (confirm('آیا از بازنشانی بنر اطمینان دارید؟')) {
        bannerText.value = 'بنر نمونه';
        bgColor.value = '#2563eb';
        textColor.value = '#ffffff';
        fontSize.value = 24;
        fontSizeValue.textContent = '24px';
        fontFamily.value = 'Vazir';
        textAlign.value = 'center';
        bgImage.value = '';
        logoImage.value = '';
        bannerPreview.style.backgroundImage = '';
        logoPreview.src = '';
        logoPreview.classList.add('hidden');
        currentFrame = 'none';
        currentEffect = 'none';
        
        // حذف کلاس‌های قاب و افکت
        frameOptions.forEach(option => {
          bannerPreview.classList.remove(option.dataset.frame);
        });
        effectOptions.forEach(option => {
          bannerPreview.classList.remove(option.dataset.effect);
        });
        
        updateBanner();
      }
    });

    // اشتراک‌گذاری
    shareBtn.addEventListener('click', function() {
      alert('امکان اشتراک‌گذاری به زودی اضافه خواهد شد!');
    });

    // چاپ
    printBtn.addEventListener('click', function() {
      window.print();
    });

    // مودال درباره
    aboutBtn.addEventListener('click', () => aboutModal.style.display = 'flex');
    closeAboutModal.addEventListener('click', () => aboutModal.style.display = 'none');

    // مودال راهنما
    helpBtn.addEventListener('click', () => helpModal.style.display = 'flex');
    closeHelpModal.addEventListener('click', () => helpModal.style.display = 'none');

    // بستن مودال با کلیک خارج از آن
    window.addEventListener('click', (e) => {
      if (e.target === aboutModal) aboutModal.style.display = 'none';
      if (e.target === helpModal) helpModal.style.display = 'none';
      if (e.target === aiProfileModal) aiProfileModal.style.display = 'none';
    });

    // ==================== بخش هوش مصنوعی ====================

    // بارگذاری تاریخچه چت
    function loadAIChatHistory(){
      const history = JSON.parse(localStorage.getItem("aiChatHistory") || "[]");
      history.forEach(msg => addAIMessage(msg.text, msg.sender, false, msg.time, msg.name, msg.img));
    }

    // ذخیره پیام در تاریخچه
    function saveAIMessage(text, sender, time, name = null, img = null){
      const history = JSON.parse(localStorage.getItem("aiChatHistory") || "[]");
      history.push({text, sender, time, name, img});
      localStorage.setItem("aiChatHistory", JSON.stringify(history));
    }

    // افزودن پیام به چت
    function addAIMessage(text, sender, save = true, time = null, name = null, img = null, isTyping = false){
      const msgDiv = document.createElement("div");
      msgDiv.className = "ai-message " + (sender === "user" ? "ai-user" : "ai-bot");
      
      if(!time) time = new Date().toLocaleTimeString([], {hour:'2-digit', minute:'2-digit'});
      
      let profile = JSON.parse(localStorage.getItem("aiUserProfile") || "{}");
      let userDisplay = name ? `<div class="ai-msg-user">${name}</div>` : "";
      let avatarTag = sender === "user" && profile.avatar ? `<img src="${profile.avatar}" style="width:30px;height:30px;border-radius:50%;">` : "";
      let imgTag = img ? `<img src="${img}">` : "";
      
      msgDiv.innerHTML = `${avatarTag}${userDisplay}<span>${text}</span>${imgTag}<div class="ai-msg-time">${time}</div>`;
      
      if(isTyping) msgDiv.classList.add("ai-typing");
      aiChatWindow.appendChild(msgDiv);
      aiChatWindow.scrollTop = aiChatWindow.scrollHeight;
      
      if(save) saveAIMessage(text, sender, time, name, img);

      if(sender === "user"){
        msgDiv.addEventListener('dblclick', () => {
          const newText = prompt("ویرایش پیام:", text);
          if(newText){
            msgDiv.querySelector("span").textContent = newText;
            updateAIMessageInHistory(text, newText);
          }
        });
      }

      return msgDiv;
    }

    // ویرایش پیام در تاریخچه
    function updateAIMessageInHistory(oldText, newText){
      const history = JSON.parse(localStorage.getItem("aiChatHistory") || "[]");
      const msg = history.find(m => m.text === oldText && m.sender === "user");
      if(msg){ 
        msg.text = newText; 
        localStorage.setItem("aiChatHistory", JSON.stringify(history)); 
      }
    }

    // ارسال پیام به هوش مصنوعی
    async function sendAIMessage(){
      const text = aiUserInput.value.trim();
      if(!text) return;
      
      const profile = JSON.parse(localStorage.getItem("aiUserProfile") || "{}");
      addAIMessage(text, "user", true, null, profile.name);
      aiUserInput.value = "";

      const loadingMsg = addAIMessage("در حال دریافت پاسخ...", "bot", false, null, null, null, true);

      try{
        const response = await fetch(`https://api2.api-code.ir/gpt-save-v2/?model=${selectedModel}&userid=mahdi&prompt=${encodeURIComponent(text)}`);
        const data = await response.text();
        loadingMsg.remove();
        addAIMessage(data, "bot");
      }catch(err){
        loadingMsg.remove();
        addAIMessage("❌ خطا در دریافت پاسخ", "bot");
        console.error(err);
      }
    }

    // آپلود تصویر و فایل در بخش هوش مصنوعی
    aiUploadBtn.addEventListener("click", () => aiFileInput.click());
    aiFileInput.addEventListener("change", (e) => {
      const file = e.target.files[0];
      if(!file) return;
      
      const reader = new FileReader();
      reader.onload = function(){
        const profile = JSON.parse(localStorage.getItem("aiUserProfile") || "{}");
        if(file.type.startsWith("image/")){
          addAIMessage("", "user", true, null, profile.name, reader.result);
        } else if(file.type === "text/plain"){
          addAIMessage(reader.result, "user");
        }
      };
      reader.readAsDataURL(file);
    });

    // منوی سه نقطه در بخش هوش مصنوعی
    aiMenuBtn.addEventListener("click", (e) => {
      e.stopPropagation();
      aiHistoryMenu.style.display = aiHistoryMenu.style.display === "block" ? "none" : "block";
      renderAIHistoryList();
    });

    aiNewChat.addEventListener("click", () => {
      if(confirm("آیا مطمئن هستید که چت جدید شروع شود؟")){
        localStorage.removeItem("aiChatHistory");
        aiChatWindow.innerHTML = "";
        aiHistoryMenu.style.display = "none";
      }
    });

    function renderAIHistoryList(){
      const history = JSON.parse(localStorage.getItem("aiChatHistory") || "[]");
      aiChatHistoryList.innerHTML = "";
      
      history.forEach(msg => {
        const btn = document.createElement("button");
        btn.textContent = (msg.sender === "user" ? "👤 " : "🤖 ") + msg.text.slice(0, 30);
        btn.style.width = "100%";
        btn.style.padding = "6px";
        btn.style.border = "none";
        btn.style.background = "none";
        btn.style.color = "#fff";
        btn.style.textAlign = "right";
        btn.style.cursor = "pointer";
        btn.style.fontSize = "14px";
        
        btn.addEventListener("click", () => alert("پیام کامل:\n" + msg.text));
        aiChatHistoryList.appendChild(btn);
      });
    }

    // پروفایل بخش هوش مصنوعی
    aiProfileBtn.addEventListener("click", () => {
      aiProfileModal.style.display = "block";
      aiHistoryMenu.style.display = "none";
      
      const profile = JSON.parse(localStorage.getItem("aiUserProfile") || "{}");
      aiProfileName.value = profile.name || "";
      aiProfileEmail.value = profile.email || "";
    });

    aiCloseProfile.addEventListener("click", () => {
      aiProfileModal.style.display = "none";
    });

    aiSaveProfile.addEventListener("click", () => {
      const profile = {
        name: aiProfileName.value.trim(),
        email: aiProfileEmail.value.trim()
      };
      
      if(aiProfileAvatar.files[0]){
        const reader = new FileReader();
        reader.onload = function(){
          profile.avatar = reader.result;
          localStorage.setItem("aiUserProfile", JSON.stringify(profile));
          alert("پروفایل با عکس ذخیره شد ✅");
          aiProfileModal.style.display = "none";
        };
        reader.readAsDataURL(aiProfileAvatar.files[0]);
      } else {
        const oldProfile = JSON.parse(localStorage.getItem("aiUserProfile") || "{}");
        if(oldProfile.avatar) profile.avatar = oldProfile.avatar;
        localStorage.setItem("aiUserProfile", JSON.stringify(profile));
        alert("پروفایل ذخیره شد ✅");
        aiProfileModal.style.display = "none";
      }
    });

    // رویدادهای بخش هوش مصنوعی
    aiSendBtn.addEventListener("click", sendAIMessage);
    aiUserInput.addEventListener("keydown", (e) => {
      if(e.key === "Enter") sendAIMessage();
    });

    document.addEventListener("click", (e) => {
      if(!aiHistoryMenu.contains(e.target) && e.target !== aiMenuBtn) {
        aiHistoryMenu.style.display = "none";
      }
    });

    // مقداردهی اولیه
    window.addEventListener('DOMContentLoaded', () => {
      updateBanner();
      updateUserBannersList();
      loadAIChatHistory();
    });
  </script>
</body>
</html>

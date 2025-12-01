<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>溫暖陳家 2026 EUROPE TRIP</title>
    
    <!-- Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600&family=Noto+Sans+TC:wght@300;400;500;700&family=Playfair+Display:ital,wght@0,400;0,600;1,400&family=Oswald:wght@500;700&display=swap" rel="stylesheet">
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- FontAwesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <!-- SortableJS -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Sortable/1.15.0/Sortable.min.js"></script>

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'Noto Sans TC', 'sans-serif'],
                        serif: ['Playfair Display', 'serif'],
                        display: ['Oswald', 'sans-serif'],
                    },
                    colors: {
                        primary: '#1c1917', // Stone 900
                        secondary: '#57534e', // Stone 600
                        accent: '#b45309', // Amber 700
                        bg: '#fafaf9', // Stone 50
                    }
                }
            }
        }
    </script>

    <style>
        body { background-color: #f5f5f4; -webkit-tap-highlight-color: transparent; touch-action: manipulation; }
        .no-scrollbar::-webkit-scrollbar { display: none; }
        .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
        
        .tab-content { display: none; opacity: 0; transition: opacity 0.2s ease-in-out; }
        .tab-content.active { display: flex; opacity: 1; flex-direction: column; height: 100%; }

        /* Categories */
        .badge { font-size: 10px; padding: 2px 6px; border-radius: 4px; font-weight: 600; text-transform: uppercase; }
        .cat-sight { background: #e0f2fe; color: #0369a1; } 
        .cat-food { background: #ffedd5; color: #c2410c; } 
        .cat-shop { background: #fce7f3; color: #be185d; } 
        .cat-trans { background: #f3f4f6; color: #4b5563; } 
        .cat-flex { background: #dcfce7; color: #15803d; } 

        .modal-enter { animation: slideUp 0.3s cubic-bezier(0.16, 1, 0.3, 1) forwards; }
        @keyframes slideUp { from { transform: translateY(100%); } to { transform: translateY(0); } }

        /* Nav Styling */
        .nav-item.active { color: #b45309; border-bottom: 2px solid #b45309; }
        .nav-item { color: #78716c; border-bottom: 2px solid transparent; }

        /* Guide Content Styles */
        .guide-section-title { font-size: 14px; font-weight: 700; color: #b45309; margin-top: 16px; margin-bottom: 4px; text-transform: uppercase; letter-spacing: 0.5px; }
        .guide-text { font-size: 14px; line-height: 1.6; color: #44403c; }

        /* Flight Card */
        .flight-card {
            background: white; border-radius: 12px; padding: 16px; margin-bottom: 12px; border-left: 5px solid #0ea5e9;
            box-shadow: 0 2px 4px rgba(0,0,0,0.05); position: relative;
        }
        .flight-line { height: 1px; background: #e5e7eb; margin: 10px 0; border-style: dashed; border-width: 1px; }
        
        .active-tab-btn { background-color: #b45309; color: white; border-color: #b45309; transform: scale(1.05); box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1); }
        
        /* Food Card Specifics */
        .food-card { transition: all 0.2s; }
        .food-card:active { transform: scale(0.98); }

        /* Checklist Item Styling */
        .checklist-item { transition: background-color 0.2s; }
        .checklist-item:active { background-color: #f5f5f4; }
        
        /* Note Item */
        .note-item input:focus { background-color: #fff; border-color: #b45309; }
    </style>
</head>
<body class="text-stone-800 h-screen flex flex-col overflow-hidden max-w-md mx-auto shadow-2xl bg-bg font-sans relative">

    <!-- Top Bar -->
    <header class="bg-white pt-6 pb-4 px-4 z-30 flex flex-col items-center justify-center flex-shrink-0 border-b border-stone-100 shadow-sm">
        <h1 class="font-display text-3xl font-bold text-primary tracking-[0.15em] leading-none">2026 EUROPE TRIP</h1>
        <div class="flex items-center gap-2 mt-2">
            <div class="h-[1px] w-8 bg-accent"></div>
            <p class="text-xs text-accent font-medium tracking-widest uppercase">溫暖陳家自由行</p>
            <div class="h-[1px] w-8 bg-accent"></div>
        </div>
        <div class="absolute right-4 top-6">
             <button onclick="jumpToToday()" class="bg-stone-100 text-stone-500 text-[10px] px-2 py-1 rounded-md font-bold active:bg-stone-200 transition">
                TODAY
            </button>
        </div>
    </header>

    <!-- Top Navigation -->
    <nav class="bg-white border-b border-stone-200 px-1 flex justify-between items-center z-20 flex-shrink-0 overflow-x-auto no-scrollbar">
        <button onclick="switchTab('plan')" class="nav-item active flex flex-col items-center p-3 min-w-[60px] transition-colors" id="nav-plan"><i class="fas fa-map-marked-alt text-lg mb-1"></i><span class="text-[10px] font-bold">行程</span></button>
        <button onclick="switchTab('food')" class="nav-item flex flex-col items-center p-3 min-w-[60px] transition-colors" id="nav-food"><i class="fas fa-utensils text-lg mb-1"></i><span class="text-[10px] font-bold">美食</span></button>
        <button onclick="switchTab('wallet')" class="nav-item flex flex-col items-center p-3 min-w-[60px] transition-colors" id="nav-wallet"><i class="fas fa-wallet text-lg mb-1"></i><span class="text-[10px] font-bold">記帳</span></button>
        <button onclick="switchTab('lists')" class="nav-item flex flex-col items-center p-3 min-w-[60px] transition-colors" id="nav-lists"><i class="fas fa-list-check text-lg mb-1"></i><span class="text-[10px] font-bold">清單</span></button>
        <button onclick="switchTab('info')" class="nav-item flex flex-col items-center p-3 min-w-[60px] transition-colors" id="nav-info"><i class="fas fa-plane-departure text-lg mb-1"></i><span class="text-[10px] font-bold">資訊</span></button>
        <button onclick="switchTab('guide')" class="nav-item flex flex-col items-center p-3 min-w-[60px] transition-colors" id="nav-guide"><i class="fas fa-book-open text-lg mb-1"></i><span class="text-[10px] font-bold">導覽</span></button>
    </nav>

    <!-- Main Content Area -->
    <main class="flex-1 overflow-hidden relative" id="main-container">
        
        <!-- === TAB 1: PLAN (行程) === -->
        <div id="tab-plan" class="tab-content active">
            <div class="bg-white border-b border-stone-100 shadow-sm flex-shrink-0 z-10">
                <div class="flex overflow-x-auto no-scrollbar py-3 px-4 gap-2 snap-x" id="day-navigator"></div>
            </div>
            <div class="flex-1 overflow-y-auto no-scrollbar p-4 pb-24 scroll-smooth">
                <div id="itinerary-display" class="space-y-4"></div>
            </div>
        </div>

        <!-- === TAB 2: FOOD (美食) === -->
        <div id="tab-food" class="tab-content">
            <div class="bg-white border-b border-stone-100 shadow-sm flex-shrink-0 z-10">
                 <div class="flex overflow-x-auto no-scrollbar py-3 px-4 gap-2 snap-x" id="food-city-navigator"></div>
            </div>
            <div class="flex-1 overflow-y-auto no-scrollbar p-4 pb-24">
                <div id="food-list-display" class="space-y-4"></div>
                <button onclick="addFoodItem()" class="w-full py-4 border-2 border-dashed border-orange-200 rounded-xl text-orange-400 font-bold text-sm hover:bg-orange-50 transition flex items-center justify-center mt-4 mb-8">
                    <i class="fas fa-plus mr-2"></i> 新增餐廳
                </button>
            </div>
        </div>

        <!-- === TAB 3: WALLET (記帳) === -->
        <div id="tab-wallet" class="tab-content">
            <div class="flex-1 overflow-y-auto no-scrollbar p-4 pb-24 space-y-5">
                 <div class="bg-primary text-white p-6 rounded-2xl shadow-lg relative overflow-hidden">
                    <h2 class="text-xs text-stone-400 uppercase tracking-widest mb-1">Exchange Calculator</h2>
                    <div class="flex items-end gap-2 mb-4 relative z-10">
                        <input type="text" id="calc-input" placeholder="12+5*2" class="w-full bg-transparent text-3xl font-light border-b border-white/20 focus:border-accent outline-none py-1 font-mono text-white placeholder-white/20">
                        <select id="currency-select" class="bg-white/10 text-sm border-none rounded px-2 py-1 outline-none text-white h-8 mb-2">
                            <option value="34.5">€ EUR</option><option value="40.2">£ GBP</option><option value="36.8">₣ CHF</option>
                        </select>
                    </div>
                    <div class="flex justify-between items-center bg-white/10 p-3 rounded-lg relative z-10">
                        <span class="text-xs opacity-70">約合台幣 TWD</span>
                        <span id="calc-result" class="text-2xl font-bold font-mono text-accent">0</span>
                    </div>
                    <button onclick="calculate()" class="mt-3 w-full bg-accent hover:bg-amber-500 py-2 rounded-lg text-sm font-bold shadow-md text-white transition">計算</button>
                </div>
                <div class="bg-white p-5 rounded-2xl shadow-sm border border-stone-100">
                    <h3 class="font-bold text-primary mb-3 text-sm uppercase">新增消費</h3>
                    <form id="expense-form" class="space-y-3">
                        <input type="text" id="expense-item" placeholder="消費項目" class="w-full bg-stone-50 p-3 rounded-lg border border-stone-200 text-sm outline-none focus:border-accent">
                        <div class="flex space-x-2">
                            <input type="number" id="expense-amount" placeholder="金額" step="0.01" class="w-2/3 bg-stone-50 p-3 rounded-lg border border-stone-200 text-sm outline-none focus:border-accent">
                            <select id="expense-currency" class="w-1/3 bg-stone-50 p-3 rounded-lg border border-stone-200 text-sm outline-none">
                                <option value="EUR">€ EUR</option><option value="GBP">£ GBP</option><option value="CHF">₣ CHF</option>
                            </select>
                        </div>
                        <label class="flex items-center justify-center gap-2 cursor-pointer bg-stone-50 text-stone-500 py-3 rounded-lg border border-dashed border-stone-300 hover:bg-stone-100 transition text-sm relative">
                            <i class="fas fa-camera"></i> <span id="photo-label">拍照 / 上傳收據</span>
                            <input type="file" id="expense-photo" accept="image/*" class="hidden">
                        </label>
                        <div id="photo-preview-box" class="hidden relative h-24 rounded-lg bg-cover bg-center border border-stone-200">
                            <button type="button" onclick="clearPhoto()" class="absolute top-1 right-1 bg-red-500 text-white rounded-full w-5 h-5 flex items-center justify-center text-xs shadow">×</button>
                        </div>
                        <button type="submit" class="w-full bg-primary text-white py-3 rounded-lg shadow-sm text-sm font-bold active:scale-95 transition">儲存紀錄</button>
                    </form>
                </div>
                <div id="expense-list" class="space-y-3 pb-8"></div>
            </div>
        </div>

        <!-- === TAB 5: LISTS (清單) === -->
        <div id="tab-lists" class="tab-content">
            <div class="flex-1 overflow-y-auto no-scrollbar p-4 pb-24 space-y-6">
                <!-- Checklist Section -->
                <div class="bg-white p-5 rounded-2xl shadow-sm border border-stone-100">
                    <div class="flex justify-between items-center border-b border-stone-100 pb-2 mb-3">
                        <h3 class="font-serif font-bold text-primary">行前清單 Checklist</h3>
                        <span class="text-xs text-stone-400 bg-stone-50 px-2 py-1 rounded">可右滑/點擊刪除</span>
                    </div>
                    <div class="space-y-0 divide-y divide-stone-100" id="checklist-container"></div>
                    <div class="mt-4 flex space-x-2">
                        <input type="text" id="new-todo" placeholder="輸入項目後按 +" class="flex-1 bg-stone-50 px-3 py-3 rounded-xl text-sm border border-stone-200 outline-none focus:border-primary transition">
                        <button onclick="addTodo()" class="bg-primary text-white w-12 rounded-xl hover:bg-stone-700 transition flex items-center justify-center shadow-sm"><i class="fas fa-plus"></i></button>
                    </div>
                </div>

                <!-- Notes (Memo) Section -->
                <div class="bg-white p-5 rounded-2xl shadow-sm border border-stone-100 min-h-[300px] flex flex-col">
                    <div class="flex justify-between items-center border-b border-stone-100 pb-2 mb-3">
                        <h3 class="font-serif font-bold text-primary"><i class="fas fa-sticky-note mr-2 text-yellow-500"></i>備忘筆記 Notes</h3>
                    </div>
                    
                    <div id="notes-container" class="space-y-2 flex-1">
                        <!-- Dynamic Notes -->
                    </div>

                    <div class="mt-4 flex space-x-2 border-t border-stone-50 pt-3">
                        <input type="text" id="new-note-input" placeholder="新增筆記..." class="flex-1 bg-yellow-50/50 px-3 py-3 rounded-xl text-sm border border-yellow-200 outline-none focus:border-yellow-500 focus:bg-white transition text-stone-700">
                        <button onclick="addNote()" class="bg-yellow-500 text-white w-12 rounded-xl hover:bg-yellow-600 transition flex items-center justify-center shadow-sm"><i class="fas fa-plus"></i></button>
                    </div>
                </div>
            </div>
        </div>

        <!-- === TAB 6: INFO (資訊 & 航班) === -->
        <div id="tab-info" class="tab-content">
            <div class="flex-1 overflow-y-auto no-scrollbar p-4 pb-24 space-y-6">
                <!-- Flight Section -->
                <div>
                    <div class="flex justify-between items-center mb-3 px-1">
                        <h3 class="font-bold text-primary text-lg"><i class="fas fa-plane-up mr-2 text-sky-500"></i>航班資訊</h3>
                        <button onclick="addFlight()" class="text-xs bg-sky-100 text-sky-600 px-2 py-1 rounded hover:bg-sky-200">新增</button>
                    </div>
                    <div id="flight-list" class="space-y-3"></div>
                </div>

                <!-- Emergency Card (Local) -->
                <div class="bg-white p-5 rounded-2xl shadow-sm text-center border border-stone-100">
                     <h2 class="font-serif text-lg font-bold text-primary mb-4">當地緊急電話 (Local Emergency)</h2>
                     <div class="grid grid-cols-3 gap-3 mb-4">
                         <div class="bg-red-50 p-3 rounded-xl border border-red-100"><div class="text-2xl font-bold text-red-600">112</div><div class="text-[10px] text-red-400">歐盟通用</div></div>
                         <div class="bg-red-50 p-3 rounded-xl border border-red-100"><div class="text-2xl font-bold text-red-600">999</div><div class="text-[10px] text-red-400">英國緊急</div></div>
                         <div class="bg-red-50 p-3 rounded-xl border border-red-100"><div class="text-2xl font-bold text-red-600">144</div><div class="text-[10px] text-red-400">瑞士醫療</div></div>
                     </div>
                </div>

                <!-- Emergency Card (Taiwan) -->
                <div class="bg-white p-5 rounded-2xl shadow-sm border border-stone-100 mt-2">
                    <h2 class="font-serif text-lg font-bold text-primary mb-4 text-center">🇹🇼 台灣駐外緊急聯絡</h2>
                    <div class="space-y-3">
                        <div class="flex justify-between items-center border-b border-stone-50 pb-2">
                            <span class="text-sm font-bold text-stone-600">全球免付費專線</span>
                            <a href="tel:+886800085095" class="text-accent font-bold text-sm bg-orange-50 px-2 py-1 rounded">800-085-095</a>
                        </div>
                        <div class="flex justify-between items-center border-b border-stone-50 pb-2">
                            <span class="text-sm font-bold text-stone-600">🇫🇷 法國代表處</span>
                            <a href="tel:+33680074994" class="text-blue-600 font-bold text-sm bg-blue-50 px-2 py-1 rounded">+33-680-074-994</a>
                        </div>
                        <div class="flex justify-between items-center border-b border-stone-50 pb-2">
                            <span class="text-sm font-bold text-stone-600">🇬🇧 英國代表處</span>
                            <a href="tel:+447768938765" class="text-blue-600 font-bold text-sm bg-blue-50 px-2 py-1 rounded">+44-7768-938-765</a>
                        </div>
                        <div class="flex justify-between items-center border-b border-stone-50 pb-2">
                            <span class="text-sm font-bold text-stone-600">🇨🇭 瑞士代表處</span>
                            <a href="tel:+41763366516" class="text-blue-600 font-bold text-sm bg-blue-50 px-2 py-1 rounded">+41-76-336-6516</a>
                        </div>
                         <div class="flex justify-between items-center border-b border-stone-50 pb-2">
                            <span class="text-sm font-bold text-stone-600">🇧🇪 歐盟/比利時</span>
                            <a href="tel:+32475472515" class="text-blue-600 font-bold text-sm bg-blue-50 px-2 py-1 rounded">+32-475-472-515</a>
                        </div>
                        <div class="flex justify-between items-center">
                            <span class="text-sm font-bold text-stone-600">🇳🇱 荷蘭代表處</span>
                            <a href="tel:+31654948849" class="text-blue-600 font-bold text-sm bg-blue-50 px-2 py-1 rounded">+31-654-948-849</a>
                        </div>
                    </div>
                    <p class="text-[10px] text-stone-400 mt-3 text-center">*撥打方式：長按 0 出現 + 號，再輸入號碼</p>
                </div>

                <div class="bg-white p-5 rounded-2xl shadow-sm text-center border border-stone-100">
                     <h2 class="font-serif text-lg font-bold text-primary mb-4 pt-2">Weather Links</h2>
                     <div class="grid grid-cols-2 gap-3">
                         <a href="https://weather.com/zh-TW/weather/today/l/FRXX0076:1:FR" target="_blank" class="bg-blue-50 text-blue-600 p-3 rounded-xl text-sm block font-bold hover:bg-blue-100"><i class="fas fa-cloud-sun mb-1 block text-2xl"></i>巴黎 Paris</a>
                         <a href="https://weather.com/zh-TW/weather/today/l/UKXX0085:1:UK" target="_blank" class="bg-blue-50 text-blue-600 p-3 rounded-xl text-sm block font-bold hover:bg-blue-100"><i class="fas fa-cloud-rain mb-1 block text-2xl"></i>倫敦 London</a>
                         <a href="https://weather.com/zh-TW/weather/today/l/SZXX0033:1:SZ" target="_blank" class="bg-blue-50 text-blue-600 p-3 rounded-xl text-sm block font-bold hover:bg-blue-100"><i class="fas fa-snowflake mb-1 block text-2xl"></i>策馬特 Zermatt</a>
                     </div>
                </div>

                <!-- NEW SYNC SECTION -->
                <div class="bg-stone-800 p-5 rounded-2xl shadow-lg text-white">
                     <h2 class="font-bold text-lg mb-2"><i class="fas fa-sync-alt mr-2"></i>行程資料傳輸</h2>
                     <p class="text-xs text-stone-400 mb-4 leading-relaxed">此網頁為單機版。若要將您編輯好的行程傳給家人，請點選「匯出」，並將檔案傳給對方，對方再點選「匯入」即可。</p>
                     
                     <div class="flex gap-3">
                         <button onclick="exportData()" class="flex-1 bg-accent hover:bg-amber-600 text-white py-3 rounded-xl font-bold text-sm transition shadow-md flex items-center justify-center">
                             <i class="fas fa-file-export mr-2"></i> 📤 匯出行程檔
                         </button>
                         <label class="flex-1 bg-stone-600 hover:bg-stone-500 text-white py-3 rounded-xl font-bold text-sm transition shadow-md flex items-center justify-center cursor-pointer">
                             <i class="fas fa-file-import mr-2"></i> 📥 匯入行程檔
                             <input type="file" id="import-file" class="hidden" onchange="importData(this)">
                         </label>
                     </div>
                </div>
            </div>
        </div>

        <!-- === TAB 7: GUIDE (導覽 & 伴手禮) === -->
        <div id="tab-guide" class="tab-content">
            <div class="bg-white border-b border-stone-100 shadow-sm flex-shrink-0 z-10">
                <div class="flex overflow-x-auto no-scrollbar py-3 px-4 gap-2 snap-x" id="guide-country-navigator"></div>
            </div>
            <div class="flex-1 overflow-y-auto no-scrollbar p-4 pb-24">
                <div id="guide-container"></div>
            </div>
        </div>

    </main>

    <!-- DEEP GUIDE MODAL -->
    <div id="guide-modal" class="fixed inset-0 z-50 hidden">
        <div class="absolute inset-0 bg-black/80 backdrop-blur-sm" onclick="closeGuideModal()"></div>
        <div class="absolute bottom-0 left-0 right-0 top-10 bg-white rounded-t-3xl p-0 shadow-2xl modal-enter overflow-hidden flex flex-col">
            <div class="relative h-64 bg-gray-200">
                <img id="guide-modal-img" class="w-full h-full object-cover">
                <button onclick="closeGuideModal()" class="absolute top-4 right-4 w-10 h-10 bg-black/50 text-white rounded-full flex items-center justify-center backdrop-blur-md"><i class="fas fa-times"></i></button>
                <div class="absolute bottom-0 left-0 right-0 p-6 bg-gradient-to-t from-black/80 to-transparent">
                    <h2 id="guide-modal-title" class="text-3xl font-serif text-white font-bold"></h2>
                </div>
            </div>
            <div class="flex-1 overflow-y-auto p-6 bg-white">
                <div class="space-y-6">
                    <div><h4 class="guide-section-title">最佳拍攝角度</h4><p id="guide-modal-photo" class="guide-text"></p></div>
                    <div><h4 class="guide-section-title">歷史背景</h4><p id="guide-modal-history" class="guide-text"></p></div>
                    <div><h4 class="guide-section-title">建築特色</h4><p id="guide-modal-arch" class="guide-text"></p></div>
                    <div><h4 class="guide-section-title">觀賞重點</h4><p id="guide-modal-view" class="guide-text"></p></div>
                </div>
            </div>
        </div>
    </div>

    <!-- ACCOMMODATION EDIT MODAL -->
    <div id="acc-modal" class="fixed inset-0 z-50 hidden">
        <div class="absolute inset-0 bg-black/60 backdrop-blur-sm" onclick="closeAccModal()"></div>
        <div class="absolute bottom-0 left-0 right-0 bg-white rounded-t-3xl p-6 shadow-2xl modal-enter">
            <h3 class="font-bold text-lg text-primary mb-4">編輯住宿資訊</h3>
            <form id="acc-form" class="space-y-4">
                <input type="hidden" id="acc-day-idx">
                <div><label class="text-[10px] text-stone-400 font-bold">住宿名稱</label><input type="text" id="acc-name" class="w-full bg-stone-50 p-3 rounded-lg border border-stone-200 font-bold"></div>
                <div><label class="text-[10px] text-stone-400 font-bold">地圖連結 (Google Maps)</label><input type="text" id="acc-map" class="w-full bg-stone-50 p-3 rounded-lg border border-stone-200 text-xs text-blue-600"></div>
                <div><label class="text-[10px] text-stone-400 font-bold">入住資訊/訂單連結 (Check-in)</label><input type="text" id="acc-link" class="w-full bg-stone-50 p-3 rounded-lg border border-stone-200 text-xs text-blue-600"></div>
                <div class="flex gap-3 pt-2">
                    <button type="button" onclick="closeAccModal()" class="flex-1 bg-gray-100 text-gray-500 py-3 rounded-xl font-bold text-sm">取消</button>
                    <button type="button" onclick="saveAccModal()" class="flex-[2] bg-primary text-white py-3 rounded-xl font-bold text-sm">儲存</button>
                </div>
            </form>
        </div>
    </div>

    <!-- FLIGHT EDIT MODAL -->
    <div id="flight-modal" class="fixed inset-0 z-50 hidden">
        <div class="absolute inset-0 bg-black/60 backdrop-blur-sm" onclick="closeFlightModal()"></div>
        <div class="absolute bottom-0 left-0 right-0 bg-white rounded-t-3xl p-6 shadow-2xl modal-enter">
            <h3 class="font-bold text-lg text-sky-600 mb-4">編輯航班</h3>
            <form id="flight-form" class="space-y-4">
                <input type="hidden" id="flight-id">
                <div class="grid grid-cols-2 gap-3">
                    <div><label class="text-[10px] text-stone-400 font-bold">出發地</label><input type="text" id="flight-from" class="w-full bg-stone-50 p-3 rounded-lg border text-sm font-bold" placeholder="TPE"></div>
                    <div><label class="text-[10px] text-stone-400 font-bold">目的地</label><input type="text" id="flight-to" class="w-full bg-stone-50 p-3 rounded-lg border text-sm font-bold" placeholder="CDG"></div>
                </div>
                <div class="grid grid-cols-2 gap-3">
                    <div><label class="text-[10px] text-stone-400 font-bold">航班編號</label><input type="text" id="flight-num" class="w-full bg-stone-50 p-3 rounded-lg border text-sm font-bold" placeholder="BR87"></div>
                    <div><label class="text-[10px] text-stone-400 font-bold">航廈</label><input type="text" id="flight-term" class="w-full bg-stone-50 p-3 rounded-lg border text-sm font-bold" placeholder="T2"></div>
                </div>
                <div><label class="text-[10px] text-stone-400 font-bold">日期</label><input type="date" id="flight-date" class="w-full bg-stone-50 p-3 rounded-lg border text-sm"></div>
                <div><label class="text-[10px] text-stone-400 font-bold">時間</label><input type="time" id="flight-time" class="w-full bg-stone-50 p-3 rounded-lg border text-sm"></div>
                <div class="flex gap-3 pt-2">
                    <button type="button" onclick="deleteFlight()" class="flex-1 bg-red-50 text-red-500 py-3 rounded-xl font-bold text-sm">刪除</button>
                    <button type="button" onclick="saveFlight()" class="flex-[2] bg-sky-600 text-white py-3 rounded-xl font-bold text-sm">儲存</button>
                </div>
            </form>
        </div>
    </div>

    <!-- ITINERARY EDIT MODAL -->
    <div id="edit-modal" class="fixed inset-0 z-50 hidden">
        <div class="absolute inset-0 bg-black/60 backdrop-blur-sm" onclick="closeModal()"></div>
        <div class="absolute bottom-0 left-0 right-0 bg-white rounded-t-3xl p-6 shadow-2xl modal-enter max-h-[90vh] overflow-y-auto">
            <h3 class="font-bold text-lg text-primary mb-4">編輯行程</h3>
            <form id="edit-form" class="space-y-4">
                <input type="hidden" id="modal-day-idx"><input type="hidden" id="modal-item-idx">
                <div class="grid grid-cols-2 gap-3">
                    <div><label class="text-[10px] text-stone-400 uppercase font-bold">時間</label><input type="time" id="modal-time" class="w-full bg-stone-50 p-3 rounded-lg border border-stone-200"></div>
                    <div><label class="text-[10px] text-stone-400 uppercase font-bold">分類</label>
                        <select id="modal-category" class="w-full bg-stone-50 p-3 rounded-lg border border-stone-200 text-sm">
                            <option value="sight">📷 景點</option><option value="food">🍴 美食</option><option value="shop">🛍️ 購物</option><option value="trans">🚌 交通</option><option value="flex">🤸 彈性</option>
                        </select>
                    </div>
                </div>
                <div><label class="text-[10px] text-stone-400 uppercase font-bold">名稱</label><input type="text" id="modal-title" class="w-full bg-stone-50 p-3 rounded-lg border border-stone-200 font-bold"></div>
                <div><label class="text-[10px] text-stone-400 uppercase font-bold">地圖連結 (選填)</label><input type="text" id="modal-map-url" placeholder="貼上 Google Maps 短網址" class="w-full bg-stone-50 p-3 rounded-lg border border-stone-200 text-xs text-blue-600"></div>
                <div class="bg-amber-50 p-3 rounded-xl border border-amber-100">
                    <label class="text-[10px] text-amber-700 uppercase font-bold">預估花費</label>
                    <div class="flex gap-2 mt-1"><input type="number" id="modal-cost" class="w-2/3 bg-white p-2 rounded border border-amber-200"><select id="modal-currency" class="w-1/3 bg-white p-2 rounded border border-amber-200 text-sm"><option value="EUR">€</option><option value="GBP">£</option><option value="CHF">₣</option></select></div>
                </div>
                <div><label class="text-[10px] text-stone-400 uppercase font-bold">筆記</label><textarea id="modal-note" rows="2" class="w-full bg-stone-50 p-3 rounded-lg border border-stone-200 text-sm"></textarea></div>
                <div class="flex gap-3 pt-2"><button type="button" onclick="deleteCurrentItem()" class="flex-1 bg-red-50 text-red-500 py-3 rounded-xl font-bold text-sm">刪除</button><button type="button" onclick="saveModal()" class="flex-[2] bg-primary text-white py-3 rounded-xl font-bold text-sm">儲存變更</button></div>
            </form>
        </div>
    </div>

    <!-- FOOD EDIT MODAL -->
    <div id="food-modal" class="fixed inset-0 z-50 hidden">
        <div class="absolute inset-0 bg-black/60 backdrop-blur-sm" onclick="closeFoodModal()"></div>
        <div class="absolute bottom-0 left-0 right-0 bg-white rounded-t-3xl p-6 shadow-2xl modal-enter max-h-[85vh] overflow-y-auto">
            <h3 class="font-bold text-lg text-orange-600 mb-4">編輯餐廳</h3>
            <form id="food-form" class="space-y-4">
                 <input type="hidden" id="food-idx">
                 <div><label class="text-[10px] text-stone-400 uppercase font-bold">餐廳名稱</label><input type="text" id="food-name" class="w-full bg-stone-50 p-3 rounded-lg border border-stone-200 font-bold"></div>
                 <div class="grid grid-cols-2 gap-3">
                     <div><label class="text-[10px] text-stone-400 uppercase font-bold">評分 (0-5)</label><input type="number" id="food-rating" step="0.1" class="w-full bg-stone-50 p-3 rounded-lg border border-stone-200 text-sm"></div>
                     <div><label class="text-[10px] text-stone-400 uppercase font-bold">營業時間</label><input type="text" id="food-hours" class="w-full bg-stone-50 p-3 rounded-lg border border-stone-200 text-sm"></div>
                 </div>
                 <div><label class="text-[10px] text-stone-400 uppercase font-bold">推薦/備註</label><textarea id="food-note" rows="3" class="w-full bg-stone-50 p-3 rounded-lg border border-stone-200 text-sm" placeholder="【必點】..."></textarea></div>
                 <div><label class="text-[10px] text-stone-400 uppercase font-bold">地圖連結</label><input type="text" id="food-map" class="w-full bg-stone-50 p-3 rounded-lg border border-stone-200 text-xs"></div>
                 
                 <div class="flex gap-3 pt-2"><button type="button" onclick="deleteFoodItem()" class="flex-1 bg-red-50 text-red-500 py-3 rounded-xl font-bold text-sm">刪除</button><button type="button" onclick="saveFoodModal()" class="flex-[2] bg-orange-600 text-white py-3 rounded-xl font-bold text-sm">儲存</button></div>
            </form>
        </div>
    </div>

    <!-- IMAGE PREVIEW MODAL -->
    <div id="img-modal" class="fixed inset-0 z-50 hidden flex items-center justify-center bg-black/90 p-4" onclick="document.getElementById('img-modal').classList.add('hidden')">
        <img id="img-full" src="" class="max-w-full max-h-full rounded-lg shadow-2xl">
    </div>

    <script>
        // --- SOUVENIR DATA (Updated with Shops - No Images) ---
        const souvenirData = {
            "🇫🇷 法國": [
                {name: "藥妝 (理膚寶水、貝德瑪)", shop: "City Pharma (26 Rue du Four)", desc: "巴黎最便宜藥妝店，人潮眾多建議早上去。"},
                {name: "馬卡龍 (Macarons)", shop: "Pierre Hermé / Ladurée", desc: "必買 PH 的 Ispahan (玫瑰荔枝) 口味。"},
                {name: "瑪黑兄弟茶 (Mariage Frères)", shop: "瑪黑區專賣店 / 百貨公司", desc: "經典 Marco Polo 茶款，黑色罐身非常有質感。"},
                {name: "Bordier 奶油", shop: "La Grande Épicerie (樂蓬馬歇超市)", desc: "米其林餐廳御用奶油，需最後一天買並自備保冷袋。"}
            ],
            "🇬🇧 英國": [
                {name: "皇家御用茶葉", shop: "Fortnum & Mason (Piccadilly)", desc: "Royal Blend 是經典，茶罐精美適合送禮。"},
                {name: "奶油酥餅 (Shortbread)", shop: "Waitrose / M&S 超市", desc: "Walkers 是基本款，超市自有品牌 CP 值更高。"},
                {name: "Jo Malone 香水", shop: "希斯洛機場免稅店", desc: "價格約台灣專櫃 6-7 折，機場買最划算。"},
                {name: "Jellycat 玩偶", shop: "Selfridges / Hamleys", desc: "倫敦款式最齊全，巴塞羅那熊是人氣款。"}
            ],
            "🇧🇪 比利時": [
                {name: "皇家御用巧克力", shop: "Neuhaus (Galeries Royales)", desc: "夾心巧克力 (Praline) 的發明者，口感細緻。"},
                {name: "時尚巧克力", shop: "Pierre Marcolini (Sablon)", desc: "巧克力之神，包裝精緻如珠寶盒。"},
                {name: "蓮花脆餅抹醬", shop: "Carrefour / Delhaize 超市", desc: "必掃貨！比台灣便宜很多的 Speculoos 抹醬。"},
                {name: "修道院啤酒", shop: "Beer Planet / 超市", desc: "推薦 Westmalle 或 Chimay，注意托運重量。"}
            ],
            "🇨🇭 瑞士": [
                {name: "Läderach 巧克力", shop: "Bahnhofstrasse 專賣店", desc: "現切秤重巧克力 (FrischSchoggi)，口感極佳。"},
                {name: "Victorinox 瑞士刀", shop: "Flagship Store (蘇黎世/日內瓦)", desc: "旗艦店可免費刻字，實用經典紀念品。"},
                {name: "Mammut 猛瑪象", shop: "策馬特專賣店", desc: "頂級戶外品牌，瑞士款式多且有折扣。"},
                {name: "傳統牛鈴", shop: "策馬特紀念品店", desc: "充滿阿爾卑斯風情的傳統工藝品。"}
            ],
            "🇳🇱 荷蘭": [
                {name: "焦糖煎餅 (Stroopwafel)", shop: "Albert Heijn (AH) 超市", desc: "超市買大包最划算，放在熱咖啡杯口軟化後更好吃。"},
                {name: "米飛兔 (Miffy) 周邊", shop: "de Winkel van Nijntje", desc: "米飛兔的故鄉，有許多荷蘭限定花色。"},
                {name: "Tony's 巧克力", shop: "Tony's Super Store / AH超市", desc: "荷蘭國民巧克力，包裝色彩繽紛，口味特殊。"},
                {name: "高達起司 (Gouda)", shop: "Henri Willig Cheese & More", desc: "真空包裝的起司輪，適合帶回國，推薦煙燻口味。"}
            ]
        };

        // --- GUIDE & DATA (UPDATED DETAILED CONTENT) ---
        // KEYS CHANGED TO CHINESE TO MATCH TITLES
        const guideLibrary = {
            "羅浮宮": { 
                img: "https://images.unsplash.com/photo-1499856871940-a09627c6d7db?w=800", 
                photo: "1. 拿破崙庭院利用「錯位」手抓金字塔尖端。<br>2. 德農館 (Denon Wing) 二樓窗邊，可俯瞰金字塔與廣場全景。<br>3. 黎塞留通道 (Passage Richelieu) 的光影線條。", 
                history: "始建於 12 世紀，最初是菲利普二世為了防禦而建的堡壘。14 世紀查理五世將其改為王宮。1682 年路易十四遷居凡爾賽宮後，羅浮宮開始用於展示王室收藏。1793 年法國大革命期間正式改為博物館對公眾開放。", 
                arch: "古典與現代的完美碰撞：主體為文藝復興風格的古典宮殿，中庭則是美籍華裔建築師貝聿銘設計的玻璃金字塔（1989年落成），象徵著過去與未來的連接。", 
                view: "【鎮館三寶】蒙娜麗莎 (Mona Lisa)、勝利女神 (Winged Victory)、維納斯 (Venus de Milo)。<br>【必看】拿破崙加冕圖 (The Coronation of Napoleon)、自由引導人民 (Liberty Leading the People)。" 
            },
            "大笨鐘 & 西敏寺": { 
                img: "https://images.unsplash.com/photo-1529655683826-aba9b3e77383?w=800", 
                photo: "1. 從西敏橋 (Westminster Bridge) 上拍攝全景。<br>2. 在大喬治街 (Great George St) 利用紅色電話亭作為前景框住大笨鐘。", 
                history: "西敏寺自 1066 年以來就是英國君主的加冕地，也是牛頓、達爾文等偉人的長眠處。大笨鐘（正式名稱伊莉莎白塔）建於 1859 年，是舊西敏宮大火後重建的傑作，鐘重達 13.5 噸。", 
                arch: "經典的哥德復興式建築 (Gothic Revival)，由查爾斯·巴里與普金設計，強調垂直線條、尖拱與精緻的石刻細節。", 
                view: "西敏寺內的加冕椅 (Coronation Chair)、詩人角 (Poets' Corner)、無名戰士墓。聆聽大笨鐘每 15 分鐘敲響的西敏鐘聲。" 
            },
            "馬特洪峰": { 
                img: "https://images.unsplash.com/photo-1531310197839-ccf54634509e?w=800", 
                photo: "1. 利菲爾湖 (Riffelsee) 拍攝完美倒影（建議清晨無風時）。<br>2. 日出時分的「日照金山」（黃金三角）。<br>3. 策馬特小鎮 Kirchbrücke 橋上拍攝全景。", 
                history: "阿爾卑斯山最後被征服的主要山峰之一。1865 年由愛德華·威姆佩爾首次登頂，卻發生斷繩悲劇，使其充滿了神祕與傳奇色彩。", 
                arch: "地質奇蹟：獨特的四角錐體金字塔造型，四個面分別準確面向羅盤的東南西北，是非洲板塊推擠歐洲板塊形成的天然紀念碑。", 
                view: "搭乘 Gornergrat 登山火車沿途風景、Glacier Paradise 的冰宮、瑞士三角巧克力 (Toblerone) logo 的原型視角。" 
            },
            "大廣場": { 
                img: "https://images.unsplash.com/photo-1572083925727-466d3387878e?w=800", 
                photo: "1. 站在廣場中心使用廣角鏡頭環拍 360 度。<br>2. 夜晚建築亮燈後的金碧輝煌。<br>3. 附近尿尿小童 (Manneken Pis) 合影。", 
                history: "始於 12 世紀的市集，1695 年遭法軍砲火幾乎夷平，後由各行會迅速重建。法國文豪雨果曾讚嘆其為「世界上最美麗的廣場」。", 
                arch: "風格大融合：哥德式的市政廳 (Hôtel de Ville) 高聳入雲，周圍環繞著巴洛克風格的行會大樓，頂端裝飾著金色的雕像與徽章。", 
                view: "市政廳的 96 米高塔、國王之家 (Maison du Roi，現為市立博物館)、天鵝之家 (La Cygne，馬克思曾在此起草共產黨宣言)。" 
            },
            "蒙馬特": { 
                img: "https://images.unsplash.com/photo-1550340499-a6c6088e6619?w=800", 
                photo: "1. 玫瑰之家 (La Maison Rose) 的粉紅牆面。<br>2. 沉沒之屋 (Sinking House) 的錯位照。<br>3. 聖心堂前階梯俯瞰巴黎全景。", 
                history: "曾是巴黎城外的獨立村莊，19 世紀末成為梵谷、畢卡索、達利等藝術家的聚集地，充滿波希米亞風情。也是 1871 年巴黎公社的重要發源地。", 
                arch: "聖心堂 (Sacré-Cœur) 採羅馬-拜占庭風格，使用特殊的夏特威石 (Château-Landon)，遇雨會分泌方解石使外觀更潔白。", 
                view: "特爾特廣場 (Place du Tertre) 的畫家市集、愛牆 (Wall of Love)、紅磨坊 (Moulin Rouge) 外觀。" 
            },
            "凡爾賽宮": { 
                img: "https://images.unsplash.com/photo-1565030796362-e6bd2423a854?w=800", 
                photo: "1. 鏡廳 (Hall of Mirrors) 的對稱倒影。<br>2. 從宮殿二樓俯瞰幾何花園中軸線。<br>3. 阿波羅噴泉與大運河。", 
                history: "路易十四 (太陽王) 為展現絕對王權，將原本的狩獵行館改建為歐洲最豪華的宮殿。1919 年在此簽署《凡爾賽條約》結束第一次世界大戰。", 
                arch: "法國巴洛克建築的巔峰，強調宏偉、對稱與金碧輝煌。安德烈·勒諾特爾設計的法式園林更是造景藝術的經典。", 
                view: "鏡廳的 357 面鏡子、國王與王后寢宮、戰爭畫廊、廣闊的十字運河 (Grand Canal) 與小翠安農宮 (Petit Trianon)。" 
            },
            "倫敦塔": { 
                img: "https://images.unsplash.com/photo-1533035332579-2479e0a2939e?w=800", 
                photo: "1. 站在塔橋 (Tower Bridge) 上拍攝倫敦塔全景。<br>2. 叛徒之門 (Traitors' Gate) 水門視角。<br>3. 白塔前的綠地。", 
                history: "1066 年由征服者威廉建立，近千年來曾作為皇宮、軍火庫、鑄幣廠，最著名的是作為關押上層階級的監獄與刑場（如安妮·博林王后）。", 
                arch: "以白塔 (White Tower) 為核心的諾曼式軍事建築，具備同心圓防禦結構的城堡，展示了中世紀的軍事防禦智慧。", 
                view: "帝國皇冠與權杖 (Crown Jewels)、守護倫敦塔的渡鴉 (Ravens，傳說飛走則國運衰退)、穿著傳統制服的皇家衛士 (Beefeaters)。" 
            },
            "大英博物館": { 
                img: "https://images.unsplash.com/photo-1574516852494-395d909a5c8c?w=800", 
                photo: "1. 大中庭 (Great Court) 的網狀玻璃天頂與閱覽室。<br>2. 復活節島摩艾石像 (Hoa Hakananai'a)。", 
                history: "成立於 1753 年，是世界上第一個對公眾開放的國家博物館。收藏了大英帝國全盛時期從世界各地收集（或掠奪）的珍寶。", 
                arch: "希臘復興式正門，擁有巨大的愛奧尼柱。千禧年落成的大中庭是歐洲最大的有蓋廣場，由諾曼·福斯特設計。", 
                view: "埃及羅塞塔石碑 (Rosetta Stone)、帕德嫩神廟石雕 (Elgin Marbles)、埃及木乃伊館、路易斯西洋棋。" 
            },
            "梵谷博物館": { 
                img: "https://images.unsplash.com/photo-1574516852494-395d909a5c8c?w=800", 
                photo: "1. 博物館現代感的主館外觀。<br>2. 館內的「梵谷自畫像」牆面。<br>3. 特展區的黃色佈置。", 
                history: "1973 年開館，擁有世界上最豐富的梵谷作品收藏，由梵谷的侄子文森·威廉創立基金會管理。", 
                arch: "主館由風格派大師里特維爾德設計（現代主義方正風格），新館由黑川紀章設計（橢圓形幾何風格）。", 
                view: "《向日葵》、《在亞爾的臥室》、《麥田群鴉》、《吃馬鈴薯的人》、梵谷與弟弟提奧的書信。" 
            }
        };

        const defaultGuideData = {
            "🇫🇷 法國": [{title: "羅浮宮", img: guideLibrary["羅浮宮"].img, photo: guideLibrary["羅浮宮"].photo, history: guideLibrary["羅浮宮"].history, view: guideLibrary["羅浮宮"].view}, {title: "蒙馬特", img: guideLibrary["蒙馬特"].img, photo: guideLibrary["蒙馬特"].photo, history: guideLibrary["蒙馬特"].history, view: guideLibrary["蒙馬特"].view}, {title: "凡爾賽宮", img: guideLibrary["凡爾賽宮"].img, photo: guideLibrary["凡爾賽宮"].photo, history: guideLibrary["凡爾賽宮"].history, view: guideLibrary["凡爾賽宮"].view}],
            "🇬🇧 英國": [{title: "大笨鐘 & 西敏寺", img: guideLibrary["大笨鐘 & 西敏寺"].img, photo: guideLibrary["大笨鐘 & 西敏寺"].photo, history: guideLibrary["大笨鐘 & 西敏寺"].history, view: guideLibrary["大笨鐘 & 西敏寺"].view}, {title: "倫敦塔", img: guideLibrary["倫敦塔"].img, photo: guideLibrary["倫敦塔"].photo, history: guideLibrary["倫敦塔"].history, view: guideLibrary["倫敦塔"].view}, {title: "大英博物館", img: guideLibrary["大英博物館"].img, photo: guideLibrary["大英博物館"].photo, history: guideLibrary["大英博物館"].history, view: guideLibrary["大英博物館"].view}],
            "🇧🇪 比利時": [{title: "大廣場", img: guideLibrary["大廣場"].img, photo: guideLibrary["大廣場"].photo, history: guideLibrary["大廣場"].history, view: guideLibrary["大廣場"].view}],
            "🇨🇭 瑞士": [{title: "馬特洪峰", img: guideLibrary["馬特洪峰"].img, photo: guideLibrary["馬特洪峰"].photo, history: guideLibrary["馬特洪峰"].history, view: guideLibrary["馬特洪峰"].view}],
            "🇳🇱 荷蘭": [{title: "梵谷博物館", img: guideLibrary["梵谷博物館"].img, photo: guideLibrary["梵谷博物館"].photo, history: guideLibrary["梵谷博物館"].history, view: guideLibrary["梵谷博物館"].view}]
        };

        const defaultItinerary = [
            { date: "7/19", day: "五", city: "Kaohsiung", lat: 22.62, lon: 120.30, items: [{time:"18:00", category:"trans", title:"高雄小港機場報到 (KHH)", note:"準備飛往廈門 (XMN) 轉機", cost:0, currency:"TWD"}, {time:"20:00", category:"trans", title:"飛往廈門 & 轉機巴黎", note:"長途飛行，準備頸枕", cost:0, currency:"TWD"}], accommodation:{name:"機上", mapLink:"", checkInLink:""} },
            { date: "7/20", day: "六", city: "Paris", lat: 48.85, lon: 2.35, items: [{time:"14:00", category:"trans", title:"抵達巴黎", note:"入住飯店，調整時差", cost:0, currency:"EUR"}, {time:"16:00", category:"sight", title:"塞納河散步", note:"感受巴黎氣息", cost:0, currency:"EUR"}, {time:"18:00", category:"sight", title:"蒙馬特 & 聖心堂", note:"俯瞰巴黎市景", cost:0, currency:"EUR", guideKey:"Montmartre"}], accommodation:{name:"巴黎飯店", mapLink:"", checkInLink:""} },
            { date: "7/21", day: "日", city: "Paris", lat: 48.85, lon: 2.35, items: [{time:"09:00", category:"sight", title:"羅浮宮", note:"必看三寶：蒙娜麗莎、勝利女神、維納斯", cost:22, currency:"EUR", guideKey:"羅浮宮"}, {time:"13:00", category:"sight", title:"凱旋門", note:"可登頂", cost:13, currency:"EUR"}, {time:"15:00", category:"sight", title:"香榭大道", note:"逛街", cost:0, currency:"EUR"}, {time:"19:00", category:"sight", title:"艾菲爾鐵塔周邊", note:"戰神廣場野餐", cost:0, currency:"EUR"}], accommodation:{name:"巴黎飯店", mapLink:"", checkInLink:""} },
            { date: "7/22", day: "一", city: "Paris", lat: 48.85, lon: 2.35, items: [{time:"09:30", category:"sight", title:"奧賽美術館", note:"印象派大師畫作", cost:16, currency:"EUR"}, {time:"14:00", category:"shop", title:"聖日耳曼區", note:"花神咖啡館、藥妝", cost:0, currency:"EUR"}, {time:"18:00", category:"sight", title:"塞納河遊船", note:"傍晚最美", cost:15, currency:"EUR"}], accommodation:{name:"巴黎飯店", mapLink:"", checkInLink:""} },
            { date: "7/23", day: "二", city: "Versailles", lat: 48.80, lon: 2.12, items: [{time:"09:00", category:"sight", title:"凡爾賽宮", note:"需提前預約，花園很大", cost:20, currency:"EUR", guideKey:"Château de Versailles"}, {time:"15:00", category:"shop", title:"瑪黑區", note:"備案：蒙日藥妝", cost:0, currency:"EUR"}], accommodation:{name:"巴黎飯店", mapLink:"", checkInLink:""} },
            { date: "7/24", day: "三", city: "London", lat: 51.50, lon: -0.12, items: [{time:"08:00", category:"trans", title:"歐洲之星 -> 倫敦", note:"早班車", cost:0, currency:"EUR"}, {time:"14:00", category:"sight", title:"卡姆登市場", note:"Camden Market", cost:0, currency:"GBP"}, {time:"16:00", category:"sight", title:"南岸散步", note:"泰晤士河畔", cost:0, currency:"GBP"}], accommodation:{name:"倫敦飯店", mapLink:"", checkInLink:""} },
            { date: "7/25", day: "四", city: "London", lat: 51.50, lon: -0.12, items: [{time:"10:00", category:"sight", title:"大笨鐘 & 西敏寺", note:"倫敦地標", cost:27, currency:"GBP", guideKey:"大笨鐘 & 西敏寺"}, {time:"11:30", category:"sight", title:"白金漢宮衛兵交接", note:"注意時間表", cost:0, currency:"GBP"}], accommodation:{name:"倫敦飯店", mapLink:"", checkInLink:""} },
            { date: "7/26", day: "五", city: "London", lat: 51.50, lon: -0.12, items: [{time:"09:30", category:"sight", title:"倫敦塔", note:"Crown Jewels", cost:33, currency:"GBP", guideKey:"Tower of London"}, {time:"12:00", category:"sight", title:"倫敦塔橋", note:"看橋打開", cost:0, currency:"GBP"}, {time:"14:00", category:"sight", title:"聖保羅大教堂", note:"", cost:23, currency:"GBP"}], accommodation:{name:"倫敦飯店", mapLink:"", checkInLink:""} },
            { date: "7/27", day: "六", city: "London", lat: 51.50, lon: -0.12, items: [{time:"10:00", category:"sight", title:"大英博物館", note:"預留2-3小時，羅塞塔石碑", cost:0, currency:"GBP", guideKey:"British Museum"}, {time:"14:00", category:"shop", title:"Covent Garden", note:"Borough Market", cost:0, currency:"GBP"}], accommodation:{name:"倫敦飯店", mapLink:"", checkInLink:""} },
            { date: "7/28", day: "日", city: "Windsor", lat: 51.48, lon: -0.60, items: [{time:"09:00", category:"sight", title:"近郊一日遊", note:"溫莎 / 牛津 / 巨石陣 (三選一)", cost:30, currency:"GBP"}], accommodation:{name:"倫敦飯店", mapLink:"", checkInLink:""} },
            { date: "7/29", day: "一", city: "London", lat: 51.50, lon: -0.12, items: [{time:"10:00", category:"flex", title:"自由日", note:"國家美術館 / 購物", cost:0, currency:"GBP"}, {time:"19:30", category:"sight", title:"音樂劇", note:"歌劇魅影 / 悲慘世界", cost:50, currency:"GBP"}], accommodation:{name:"倫敦飯店", mapLink:"", checkInLink:""} },
            { date: "7/30", day: "二", city: "Brussels", lat: 50.85, lon: 4.35, items: [{time:"09:00", category:"trans", title:"歐洲之星 -> 布魯塞爾", note:"", cost:0, currency:"GBP"}, {time:"14:00", category:"sight", title:"大廣場 & 尿尿小童", note:"拱廊街、巧克力", cost:0, currency:"EUR", guideKey:"大廣場"}], accommodation:{name:"布魯塞爾飯店", mapLink:"", checkInLink:""} },
            { date: "7/31", day: "三", city: "Brussels", lat: 50.85, lon: 4.35, items: [{time:"10:00", category:"sight", title:"皇家公園 & 漫畫牆", note:"", cost:0, currency:"EUR"}, {time:"14:00", category:"sight", title:"原子塔 Atomium", note:"", cost:16, currency:"EUR"}, {time:"18:00", category:"food", title:"啤酒 & 薯條", note:"", cost:20, currency:"EUR"}], accommodation:{name:"布魯塞爾飯店", mapLink:"", checkInLink:""} },
            { date: "8/1", day: "四", city: "Luxembourg", lat: 49.61, lon: 6.13, items: [{time:"09:00", category:"trans", title:"盧森堡一日遊", note:"火車往返", cost:0, currency:"EUR"}, {time:"11:00", category:"sight", title:"Bock Casemates", note:"地下要塞", cost:0, currency:"EUR"}, {time:"13:00", category:"sight", title:"Corniche 觀景路", note:"歐洲最美陽台", cost:0, currency:"EUR"}], accommodation:{name:"布魯塞爾飯店", mapLink:"", checkInLink:""} },
            { date: "8/2", day: "五", city: "Bruges", lat: 51.20, lon: 3.22, items: [{time:"09:00", category:"trans", title:"布魯日一日遊", note:"火車往返", cost:15, currency:"EUR"}, {time:"11:00", category:"sight", title:"運河遊船", note:"", cost:12, currency:"EUR"}, {time:"13:00", category:"sight", title:"鐘樓", note:"", cost:14, currency:"EUR"}], accommodation:{name:"布魯塞爾飯店", mapLink:"", checkInLink:""} },
            { date: "8/3", day: "六", city: "Zermatt", lat: 46.02, lon: 7.74, items: [{time:"08:00", category:"trans", title:"布魯塞爾 -> 策馬特", note:"飛機至日內瓦 -> 火車", cost:0, currency:"EUR"}, {time:"18:00", category:"sight", title:"馬特洪峰夕陽", note:"小鎮散步", cost:0, currency:"CHF", guideKey:"馬特洪峰"}], accommodation:{name:"策馬特飯店", mapLink:"", checkInLink:""} },
            { date: "8/4", day: "日", city: "Zermatt", lat: 46.02, lon: 7.74, items: [{time:"09:00", category:"sight", title:"Gornergrat 觀景列車", note:"經典角度，利菲爾湖倒影", cost:110, currency:"CHF"}], accommodation:{name:"策馬特飯店", mapLink:"", checkInLink:""} },
            { date: "8/5", day: "一", city: "Zermatt", lat: 46.02, lon: 7.74, items: [{time:"09:00", category:"sight", title:"五湖健行 (5-Seenweg)", note:"最美健行路線", cost:0, currency:"CHF"}], accommodation:{name:"策馬特飯店", mapLink:"", checkInLink:""} },
            { date: "8/6", day: "二", city: "Zermatt", lat: 46.02, lon: 7.74, items: [{time:"09:00", category:"sight", title:"Glacier Paradise", note:"冰川天堂，冰宮", cost:100, currency:"CHF"}], accommodation:{name:"策馬特飯店", mapLink:"", checkInLink:""} },
            { date: "8/7", day: "三", city: "Zermatt", lat: 46.02, lon: 7.74, items: [{time:"10:00", category:"flex", title:"放鬆日", note:"Sunnegga / 小鎮散步", cost:0, currency:"CHF"}], accommodation:{name:"策馬特飯店", mapLink:"", checkInLink:""} },
            { date: "8/8", day: "四", city: "Brussels", lat: 50.85, lon: 4.35, items: [{time:"09:00", category:"trans", title:"策馬特 -> 布魯塞爾", note:"移動日", cost:0, currency:"EUR"}], accommodation:{name:"布魯塞爾飯店", mapLink:"", checkInLink:""} },
            { date: "8/9", day: "五", city: "Dinant", lat: 50.26, lon: 4.91, items: [{time:"10:00", category:"sight", title:"比利時小鎮遊", note:"Dinant / Mechelen / Liège", cost:10, currency:"EUR"}], accommodation:{name:"布魯塞爾飯店", mapLink:"", checkInLink:""} },
            { date: "8/10", day: "六", city: "Amsterdam", lat: 52.36, lon: 4.90, items: [{time:"09:00", category:"trans", title:"前往阿姆斯特丹", note:"途經 Utrecht (DOM Tower)", cost:20, currency:"EUR"}, {time:"18:00", category:"food", title:"運河畔晚餐", note:"", cost:30, currency:"EUR"}], accommodation:{name:"阿姆斯特丹飯店", mapLink:"", checkInLink:""} },
            { date: "8/11", day: "日", city: "Rotterdam", lat: 51.92, lon: 4.47, items: [{time:"10:00", category:"sight", title:"鹿特丹 or 海牙", note:"方塊屋 / 莫瑞泰斯美術館", cost:20, currency:"EUR"}], accommodation:{name:"阿姆斯特丹飯店", mapLink:"", checkInLink:""} },
            { date: "8/12", day: "一", city: "Amsterdam", lat: 52.36, lon: 4.90, items: [{time:"10:00", category:"trans", title:"Hilversum -> Amsterdam", note:"寄放行李", cost:0, currency:"EUR"}, {time:"13:00", category:"sight", title:"市區輕鬆遊", note:"花市 / 9 Streets / NDSM", cost:0, currency:"EUR"}], accommodation:{name:"阿姆斯特丹飯店", mapLink:"", checkInLink:""} },
            { date: "8/13", day: "二", city: "Zaanse Schans", lat: 52.47, lon: 4.82, items: [{time:"09:00", category:"sight", title:"風車村 + 羊角村", note:"木鞋 / 起司 / 遊船", cost:25, currency:"EUR"}], accommodation:{name:"阿姆斯特丹飯店", mapLink:"", checkInLink:""} },
            { date: "8/14", day: "三", city: "Amsterdam", lat: 52.36, lon: 4.90, items: [{time:"09:00", category:"sight", title:"梵谷博物館", note:"需預約", cost:20, currency:"EUR", guideKey:"梵谷博物館"}, {time:"13:00", category:"sight", title:"國家博物館", note:"", cost:20, currency:"EUR"}, {time:"18:00", category:"food", title:"Foodhallen 晚餐", note:"", cost:25, currency:"EUR"}], accommodation:{name:"阿姆斯特丹飯店", mapLink:"", checkInLink:""} },
            { date: "8/15", day: "四", city: "Taipei", lat: 25.03, lon: 121.56, items: [{time:"10:00", category:"trans", title:"整理行李 -> 機場", note:"退稅", cost:0, currency:"EUR"}, {time:"13:00", category:"trans", title:"飛回台灣", note:"平安返家", cost:0, currency:"EUR"}], accommodation:{name:"機上", mapLink:"", checkInLink:""} },
        ];

        // --- UPDATED FOOD DATA (Real Recommended Spots - VERIFIED) ---
        const defaultFood = {
            "🇫🇷 法國": [
                {
                    name: "Le Bouillon Chartier",
                    rating: 4.0,
                    hours: "11:30-00:00 (每日)",
                    note: "【必點】油封鴨腿 (Confit de canard)、蝸牛 (Escargots)。巴黎最著名的百年工人食堂，價格極親民，無法訂位需現場排隊，體驗熱鬧氛圍。",
                    map: "https://www.google.com/maps/search/?api=1&query=Bouillon+Chartier+Paris"
                },
                {
                    name: "L'As du Fallafel",
                    rating: 4.6,
                    hours: "11:00-23:00 (週五提前打烊/週六公休)",
                    note: "【必點】Fallafel Special (招牌法拉費口袋餅)。瑪黑區排隊名店，份量巨大，炸茄子與鷹嘴豆泥球非常美味。",
                    map: "https://www.google.com/maps/search/?api=1&query=L'As+du+Fallafel+Paris"
                },
                {
                    name: "Pierre Hermé",
                    rating: 4.7,
                    hours: "10:00-20:00 (依分店)",
                    note: "【必點】Ispahan (玫瑰荔枝覆盆子) 馬卡龍、可頌。甜點界的畢卡索，口感層次豐富，比Ladurée更受現代人喜愛。",
                    map: "https://www.google.com/maps/search/?api=1&query=Pierre+Herme+Paris"
                },
                {
                    name: "Angelina",
                    rating: 4.2,
                    hours: "08:00-19:00",
                    note: "【必點】L'Africain (老式熱巧克力)、Mont-Blanc (蒙布朗栗子蛋糕)。香奈兒女士的愛店，熱巧克力濃郁如醬。",
                    map: "https://www.google.com/maps/search/?api=1&query=Angelina+Paris+Rivoli"
                },
                {
                    name: "Au Pied de Cochon",
                    rating: 4.3,
                    hours: "24小時營業",
                    note: "【必點】法式洋蔥湯、招牌烤豬腳。位於Les Halles，全天候供應傳統法餐，宵夜首選。",
                    map: "https://www.google.com/maps/search/?api=1&query=Au+Pied+de+Cochon+Paris"
                }
            ],
            "🇬🇧 英國": [
                {
                    name: "Dishoom",
                    rating: 4.6,
                    hours: "08:00-23:00",
                    note: "【必點】早餐 Bacon Naan Roll，晚餐 House Black Daal、Chicken Ruby。倫敦最紅印度菜，裝潢復古，建議預約。",
                    map: "https://www.google.com/maps/search/?api=1&query=Dishoom+Covent+Garden"
                },
                {
                    name: "Flat Iron",
                    rating: 4.5,
                    hours: "12:00-23:00",
                    note: "【必點】Flat Iron Steak (£14)。高CP值平鐵牛排，隨餐附贈可愛小菜刀，餐後有免費焦糖海鹽冰淇淋。",
                    map: "https://www.google.com/maps/search/?api=1&query=Flat+Iron+Steak+London"
                },
                {
                    name: "Borough Market",
                    rating: 4.8,
                    hours: "10:00-17:00 (週一休)",
                    note: "【必點】Richard Haward 生蠔、Paella 海鮮燉飯、Bread Ahead 爆漿甜甜圈。倫敦美食心臟。",
                    map: "https://www.google.com/maps/search/?api=1&query=Borough+Market+London"
                },
                {
                    name: "Burger & Lobster",
                    rating: 4.4,
                    hours: "12:00-22:30",
                    note: "【必點】Original Roll (龍蝦堡)、整隻蒸龍蝦。遊客必吃，龍蝦肉質Q彈，薯條與沙拉也很好吃。",
                    map: "https://www.google.com/maps/search/?api=1&query=Burger+%26+Lobster+Soho"
                },
                {
                    name: "The Breakfast Club",
                    rating: 4.3,
                    hours: "08:00-16:00",
                    note: "【必點】The All American (美式早餐)、Pancakes。全天候早午餐名店，永遠在排隊。",
                    map: "https://www.google.com/maps/search/?api=1&query=The+Breakfast+Club+London"
                }
            ],
            "🇧🇪 比利時": [
                {
                    name: "Chez Léon",
                    rating: 4.1,
                    hours: "12:00-23:00",
                    note: "【必點】Formule Léon (淡菜+薯條+啤酒套餐)。布魯塞爾大廣場旁百年老店，雖然觀光但品質穩定。",
                    map: "https://www.google.com/maps/search/?api=1&query=Chez+Leon+Brussels"
                },
                {
                    name: "Maison Dandoy",
                    rating: 4.3,
                    hours: "09:30-19:00",
                    note: "【必點】布魯塞爾鬆餅 (長方形/脆)、列日鬆餅 (圓形/軟/有珍珠糖)。比利時最著名的鬆餅店。",
                    map: "https://www.google.com/maps/search/?api=1&query=Maison+Dandoy+Galeries"
                },
                {
                    name: "Fritland",
                    rating: 4.3,
                    hours: "11:00-01:00",
                    note: "【必點】招牌薯條 + Andalouse (微辣美乃滋) 醬。證券交易所旁的人氣炸物店。",
                    map: "https://www.google.com/maps/search/?api=1&query=Fritland+Brussels"
                },
                {
                    name: "Fin de Siècle",
                    rating: 4.6,
                    hours: "18:00-00:00",
                    note: "【必點】Carbonnades (啤酒燉牛肉)、Stoemp (香腸馬鈴薯泥)。份量大、氣氛好的道地酒館。",
                    map: "https://www.google.com/maps/search/?api=1&query=Fin+de+Siecle+Brussels"
                }
            ],
            "🇨🇭 瑞士": [
                {
                    name: "Whymper-Stube",
                    rating: 4.7,
                    hours: "15:00-23:00",
                    note: "【必點】Cheese Fondue (起司鍋)、Raclette。策馬特人氣第一名餐廳，氣氛溫馨，務必提前預訂。",
                    map: "https://www.google.com/maps/search/?api=1&query=Whymper-Stube+Zermatt"
                },
                {
                    name: "Schäferstube",
                    rating: 4.8,
                    hours: "18:00-23:00",
                    note: "【必點】瓦萊州黑臉羊肉料理 (Lamb)、羊排。位於 Hotel Julen 地下室，鄉村風格極佳。",
                    map: "https://www.google.com/maps/search/?api=1&query=Restaurant+Schaferstube+Zermatt"
                },
                {
                    name: "Fuchs Bakery",
                    rating: 4.5,
                    hours: "07:00-18:30",
                    note: "【必點】Matterhörnli (馬特洪峰造型巧克力)、登山麵包。策馬特最好的烘焙坊。",
                    map: "https://www.google.com/maps/search/?api=1&query=Fuchs+Bakery+Zermatt"
                },
                {
                    name: "Du Pont",
                    rating: 4.3,
                    hours: "09:00-23:00",
                    note: "【必點】Rösti (瑞士薯餅)。策馬特現存最古老的餐廳之一，價格相對親民。",
                    map: "https://www.google.com/maps/search/?api=1&query=Restaurant+Du+Pont+Zermatt"
                }
            ],
            "🇳🇱 荷蘭": [
                {
                    name: "Winkel 43",
                    rating: 4.6,
                    hours: "08:00-01:00 (週六至03:00)",
                    note: "【必點】荷蘭蘋果派 (Appeltaart) 加鮮奶油。位於北教堂旁，被譽為阿姆斯特丹最好吃的蘋果派。",
                    map: "https://www.google.com/maps/search/?api=1&query=Winkel+43+Amsterdam"
                },
                {
                    name: "The Seafood Bar",
                    rating: 4.5,
                    hours: "12:00-22:00",
                    note: "【必點】Fruits de Mer (海鮮冷盤塔)、烤綜合海鮮。食材新鮮，裝潢現代時尚，需預約。",
                    map: "https://www.google.com/maps/search/?api=1&query=The+Seafood+Bar+Spui"
                },
                {
                    name: "Manneken Pis",
                    rating: 4.2,
                    hours: "10:00-23:00",
                    note: "【必點】尿尿小童薯條。總是排長龍，推薦嘗試荷蘭特有的 Joppiesaus (咖哩洋蔥醬)。",
                    map: "https://www.google.com/maps/search/?api=1&query=Manneken+Pis+Fries+Amsterdam"
                },
                {
                    name: "FEBO",
                    rating: 4.0,
                    hours: "11:00-03:00",
                    note: "【必點】Kroket (可樂餅炸肉捲)。荷蘭著名的「自動販賣機漢堡店」，投幣即可取出熱食，體驗非常有趣。",
                    map: "https://www.google.com/maps/search/?api=1&query=FEBO+Amsterdam"
                }
            ]
        };

        const defaultChecklist = [
            // Documents
            {text:"護照 (效期6個月以上)", done:false},
            {text:"護照影本/大頭照 (備用)", done:false},
            {text:"機票 (電子檔+紙本)", done:false},
            {text:"申根保險單 (英文版)", done:false},
            {text:"訂房紀錄/行程表 (海關用)", done:false},
            // Money
            {text:"歐元/英鎊/瑞郎現金 (小面額)", done:false},
            {text:"信用卡 (開通海外提款/刷卡)", done:false},
            {text:"信用卡 PIN 碼 (4碼, 自助機台用)", done:false},
            {text:"零錢包 (歐洲硬幣多)", done:false},
            // Electronics
            {text:"網卡 / SIM 卡 / 取卡針", done:false},
            {text:"萬用轉接頭 (歐規/英規)", done:false},
            {text:"行動電源 (需放隨身行李)", done:false},
            {text:"充電線 (長線佳)", done:false},
            // Toiletries & Health
            {text:"牙刷 / 牙膏 (歐洲飯店不附)", done:false},
            {text:"室內拖鞋 (飛機/飯店用)", done:false},
            {text:"常備藥 (感冒/腸胃/止痛/暈車)", done:false},
            {text:"個人慢性病藥物", done:false},
            {text:"OK蹦 / 人工皮 (防磨腳)", done:false},
            {text:"護唇膏 / 乳液 (歐洲乾燥)", done:false},
            // Clothing & Misc
            {text:"好走的鞋 (最重要!)", done:false},
            {text:"防風保暖外套 (洋蔥式)", done:false},
            {text:"太陽眼鏡 / 帽子", done:false},
            {text:"防盜腰包 / 貼身包", done:false},
            {text:"水壺 (歐洲買水貴)", done:false},
            {text:"環保購物袋 (超市袋子收費)", done:false},
            {text:"輕便雨衣 / 摺疊傘", done:false},
            {text:"行李鎖 (TSA)", done:false}
        ];
        
        const defaultFlights = [
            {id:1, from:"高雄 KHH", to:"廈門 XMN", num:"MF864", date:"2026-07-19", time:"19:00", term:"I"},
            {id:2, from:"廈門 XMN", to:"巴黎 CDG", num:"MF825", date:"2026-07-20", time:"00:10", term:"3"},
            {id:3, from:"巴黎 CDG", to:"倫敦 LHR", num:"AF123", date:"2026-07-24", time:"08:00", term:"2E"},
            {id:4, from:"阿姆斯特丹", to:"台北 TPE", num:"CI074", date:"2026-08-15", time:"11:00", term:"1"}
        ];

        let itinerary=[], foodData={}, expenses=[], checklist=[], memo="", flights=[];
        let notes = []; // NEW: Array for structured notes
        let currentDayIdx=0, currentGuideCountry="🇫🇷 法國", currentFoodCity="🇫🇷 法國", currentPhotoBase64=null;

        document.addEventListener('DOMContentLoaded', () => {
            initStorage();
            try { renderDayTabs(); } catch(e) { console.error(e); }
            try { renderItinerary(0); } catch(e) { console.error(e); }
            try { renderGuideCountries(); renderGuideList(currentGuideCountry); } catch(e) { console.error(e); }
            try { renderFoodCities(); renderFoodList(currentFoodCity); } catch(e) { console.error(e); }
            try { renderExpenses(); } catch(e) { console.error(e); }
            try { renderChecklist(); } catch(e) { console.error(e); }
            try { renderNotes(); } catch(e) { console.error(e); } // Changed from renderMemo
            try { renderFlights(); } catch(e) { console.error(e); }
            switchTab('plan'); 
            try { jumpToToday(); } catch(e) { console.error(e); }
        });

        function initStorage() {
            // Version 41 (Bug Fix for Memo and defaultFood)
            try {
                const p = localStorage.getItem('trip_v41_plan');
                itinerary = p ? JSON.parse(p) : defaultItinerary;
                if (!Array.isArray(itinerary) || itinerary.length === 0) itinerary = defaultItinerary;
            } catch (e) { itinerary = defaultItinerary; }

            try {
                const f = localStorage.getItem('trip_v41_food');
                foodData = f ? JSON.parse(f) : defaultFood;
            } catch (e) { foodData = defaultFood; }

            try { expenses = JSON.parse(localStorage.getItem('trip_v41_expenses')) || []; } catch(e) { expenses = []; }

            try {
                const c = localStorage.getItem('trip_v41_check');
                checklist = c ? JSON.parse(c) : defaultChecklist;
                if (!Array.isArray(checklist) || checklist.length === 0) checklist = defaultChecklist;
            } catch (e) { checklist = defaultChecklist; }

            // NEW NOTES LOGIC
            try {
                const n = localStorage.getItem('trip_v41_notes');
                notes = n ? JSON.parse(n) : [];
                
                // MIGRATION: If notes are empty, check for old v37/v38/v40 memo string
                if (notes.length === 0) {
                    const oldMemo38 = localStorage.getItem('trip_v38_memo');
                    const oldMemo37 = localStorage.getItem('trip_v37_memo');
                    const oldMemo40 = localStorage.getItem('trip_v40_memo');
                    const legacyText = oldMemo40 || oldMemo38 || oldMemo37;
                    if (legacyText && legacyText.trim() !== "") {
                        notes.push({id: Date.now(), text: legacyText});
                        localStorage.setItem('trip_v41_notes', JSON.stringify(notes));
                    }
                }
            } catch (e) { notes = []; }

            try {
                const fl = localStorage.getItem('trip_v41_flights');
                flights = fl ? JSON.parse(fl) : defaultFlights;
                if (!Array.isArray(flights) || flights.length === 0) flights = defaultFlights;
            } catch (e) { flights = defaultFlights; }
        }

        // --- NEW NOTES FUNCTIONS ---
        function renderNotes() {
            const container = document.getElementById('notes-container');
            if (!container) return;
            container.innerHTML = notes.map((note, index) => `
                <div class="note-item flex gap-2 items-center bg-yellow-50 p-2 rounded-xl border border-yellow-100 group transition hover:shadow-sm">
                    <span class="text-yellow-400 text-xs font-bold w-4 text-center">${index + 1}.</span>
                    <input type="text" value="${note.text}" onchange="updateNote(${note.id}, this.value)" class="flex-1 bg-transparent text-sm text-stone-700 outline-none font-medium">
                    <button onclick="deleteNote(${note.id})" class="text-stone-300 hover:text-red-400 p-2 rounded-full active:bg-red-50 transition opacity-50 group-hover:opacity-100">
                        <i class="fas fa-trash-alt text-xs"></i>
                    </button>
                </div>
            `).join('');
        }

        function addNote() {
            const input = document.getElementById('new-note-input');
            const text = input.value.trim();
            if (!text) return;
            notes.push({ id: Date.now(), text: text });
            localStorage.setItem('trip_v41_notes', JSON.stringify(notes));
            renderNotes();
            input.value = '';
        }

        function updateNote(id, newText) {
            const noteIndex = notes.findIndex(n => n.id === id);
            if (noteIndex > -1) {
                notes[noteIndex].text = newText;
                localStorage.setItem('trip_v41_notes', JSON.stringify(notes));
            }
        }

        function deleteNote(id) {
            if(confirm('確定刪除此條筆記？')) {
                notes = notes.filter(n => n.id !== id);
                localStorage.setItem('trip_v41_notes', JSON.stringify(notes));
                renderNotes();
            }
        }

        // --- FLIGHT FUNCTIONS ---
        function renderFlights() { document.getElementById('flight-list').innerHTML = flights.map(f => `<div onclick="editFlight(${f.id})" class="flight-card cursor-pointer active:scale-[0.98] transition"><div class="flex justify-between items-center mb-2"><span class="text-xs font-bold text-gray-400">${f.date}</span><span class="text-xs font-bold text-sky-600 bg-sky-50 px-2 py-1 rounded">${f.num}</span></div><div class="flex justify-between items-center text-lg font-bold text-primary"><span>${f.from}</span><i class="fas fa-plane text-gray-300 text-sm mx-2"></i><span>${f.to}</span></div><div class="flight-line"></div><div class="flex justify-between text-xs text-gray-500"><span><i class="far fa-clock mr-1"></i>${f.time}</span><span>航廈 ${f.term}</span></div></div>`).join(''); }
        function addFlight() { document.getElementById('flight-id').value="NEW"; document.getElementById('flight-form').reset(); document.getElementById('flight-modal').classList.remove('hidden'); }
        function editFlight(id) { const f=flights.find(x=>x.id===id); document.getElementById('flight-id').value=f.id; document.getElementById('flight-from').value=f.from; document.getElementById('flight-to').value=f.to; document.getElementById('flight-num').value=f.num; document.getElementById('flight-term').value=f.term; document.getElementById('flight-date').value=f.date; document.getElementById('flight-time').value=f.time; document.getElementById('flight-modal').classList.remove('hidden'); }
        function saveFlight() { const id=document.getElementById('flight-id').value; const f={id:id==="NEW"?Date.now():parseInt(id), from:document.getElementById('flight-from').value, to:document.getElementById('flight-to').value, num:document.getElementById('flight-num').value, term:document.getElementById('flight-term').value, date:document.getElementById('flight-date').value, time:document.getElementById('flight-time').value}; if(id==="NEW")flights.push(f); else flights[flights.findIndex(x=>x.id==id)]=f; localStorage.setItem('trip_v41_flights',JSON.stringify(flights)); renderFlights(); closeFlightModal(); }
        function deleteFlight() { const id=document.getElementById('flight-id').value; if(id!=="NEW"&&confirm("刪除?")){ flights=flights.filter(x=>x.id!=id); localStorage.setItem('trip_v41_flights',JSON.stringify(flights)); renderFlights(); } closeFlightModal(); }
        function closeFlightModal() { document.getElementById('flight-modal').classList.add('hidden'); }

        // --- PLAN ---
        function renderDayTabs(){ document.getElementById('day-navigator').innerHTML = itinerary.map((d,i)=>`<button onclick="changeDay(${i})" id="day-btn-${i}" class="flex-shrink-0 px-4 py-2 rounded-xl text-xs font-bold transition-all border border-stone-100 bg-white text-stone-400"><span class="block text-[10px] uppercase mb-0.5">${d.date}</span><span class="block text-sm">${d.day}</span></button>`).join(''); changeDay(currentDayIdx); }
        function changeDay(i){ currentDayIdx=i; document.querySelectorAll('#day-navigator button').forEach((b,idx)=>b.className=idx===i?"flex-shrink-0 px-5 py-2 rounded-xl text-xs font-bold border border-primary bg-primary text-white shadow-md scale-105":"flex-shrink-0 px-4 py-2 rounded-xl text-xs font-bold border border-stone-100 bg-white text-stone-400"); renderItinerary(i); }
        function renderItinerary(i){ 
            const d=itinerary[i]; const c={}; d.items.forEach(x=>{if(x.cost>0)c[x.currency]=(c[x.currency]||0)+parseFloat(x.cost)}); const cs=Object.entries(c).map(([k,v])=>`${k} ${v}`).join('+')||"0"; const wid=`w-${i}`; fetchWeather(d.lat,d.lon,wid); 
            
            // Accommodation
            const acc = d.accommodation || {name:"", mapLink:"", checkInLink:""};
            const accHtml = `<div class="mt-8 pt-4 border-t border-stone-100 bg-white rounded-xl p-4 shadow-sm border border-indigo-50"><div class="flex justify-between items-center mb-2"><div class="text-[10px] font-bold text-indigo-400 uppercase tracking-wider"><i class="fas fa-bed mr-1"></i>住宿資訊</div><button onclick="openAccModal(${i})" class="text-xs text-indigo-400 font-bold hover:text-indigo-600"><i class="fas fa-edit mr-1"></i>編輯</button></div><div class="text-primary font-bold text-lg mb-2">${acc.name || "未設定住宿"}</div><div class="flex gap-2">${acc.mapLink ? `<a href="${acc.mapLink}" target="_blank" class="flex-1 bg-indigo-50 text-indigo-600 py-2 rounded-lg text-xs font-bold text-center hover:bg-indigo-100"><i class="fas fa-map-marker-alt mr-1"></i>地圖</a>` : ''}${acc.checkInLink ? `<a href="${acc.checkInLink}" target="_blank" class="flex-1 bg-emerald-50 text-emerald-600 py-2 rounded-lg text-xs font-bold text-center hover:bg-emerald-100"><i class="fas fa-key mr-1"></i>Check-in</a>` : ''}</div></div>`;

            // ONE-CLICK MAP BUTTON
            const mapRoute = `https://www.google.com/maps/dir/${d.items.map(it => encodeURIComponent(d.city + " " + it.title)).join("/")}`;
            const mapBtn = d.items.length > 0 ? `<a href="${mapRoute}" target="_blank" class="block w-full bg-blue-600 text-white text-center py-3 rounded-xl font-bold shadow-md mb-6 active:scale-95 transition flex items-center justify-center"><i class="fas fa-route mr-2"></i>開啟當日路線導航</a>` : '';

            document.getElementById('itinerary-display').innerHTML=`
                <div class="flex justify-between items-end mb-4"><div><h2 class="text-2xl font-serif font-bold text-primary">${d.city}</h2><div class="flex items-center gap-2 mt-1"><span class="text-xs text-stone-400">Day ${i+1}</span><div id="${wid}" class="text-xs font-bold text-sky-600 bg-sky-50 px-2 py-0.5 rounded-full">...</div></div></div><div class="text-right"><span class="text-[10px] font-bold text-stone-400 uppercase">Spend</span><div class="text-sm font-bold text-accent font-mono bg-amber-50 px-2 py-1 rounded border border-amber-100">${cs}</div></div></div>
                ${mapBtn}
                <div id="sort-${i}" class="space-y-4 ml-2 border-l-2 border-stone-200 pl-6 pb-2">${d.items.map((x,ix)=>`<div class="relative group" data-id="${ix}"><div class="absolute -left-[33px] top-0 w-4 h-4 rounded-full border-2 border-white shadow-sm cat-${x.category} z-10" style="background-color:currentColor"></div><div onclick="openEditModal(${i},${ix})" class="bg-white rounded-xl p-4 shadow-sm border border-stone-100 cursor-pointer active:scale-95 transition select-none"><div class="flex justify-between items-start mb-1"><div class="flex items-center gap-2"><span class="text-xs font-mono font-bold text-stone-400 bg-stone-50 px-1 rounded">${x.time||'--:--'}</span><span class="badge cat-${x.category}">${x.category}</span></div><div class="flex gap-2">${x.guideKey?`<button onclick="openGuideModal('${x.guideKey}',event)" class="text-xs text-stone-500 bg-stone-100 px-2 py-1 rounded"><i class="fas fa-book-open"></i></button>`:''}<a href="${x.mapUrl||`https://www.google.com/maps/search/?api=1&query=${d.city}+${x.title}`}" target="_blank" onclick="event.stopPropagation()" class="text-stone-300 hover:text-accent"><i class="fas fa-map-location-dot"></i></a></div></div><h3 class="font-bold text-primary text-lg">${x.title}</h3>${x.note?`<p class="text-xs text-stone-500 mt-1">${x.note}</p>`:''}${x.cost>0?`<div class="mt-2 inline-block bg-yellow-50 text-yellow-700 px-2 py-0.5 rounded text-[10px] font-bold border border-yellow-100">${x.currency} ${x.cost}</div>`:''}</div></div>`).join('')}</div><button onclick="addNewItem(${i})" class="w-full py-3 border-2 border-dashed border-stone-200 rounded-xl text-stone-400 font-bold text-sm mt-4">+ 新增</button>${accHtml}`; new Sortable(document.getElementById(`sort-${i}`),{animation:150,delay:200,delayOnTouchOnly:true,onEnd:function(e){const it=itinerary[i].items.splice(e.oldIndex,1)[0];itinerary[i].items.splice(e.newIndex,0,it);localStorage.setItem('trip_v41_plan',JSON.stringify(itinerary));}}); }
        async function fetchWeather(lat,lon,id){ try{if(!lat)return;const r=await fetch(`https://api.open-meteo.com/v1/forecast?latitude=${lat}&longitude=${lon}&current_weather=true`);const d=await r.json();document.getElementById(id).innerHTML=`<i class="fas fa-cloud-sun mr-1"></i>${Math.round(d.current_weather.temperature)}°C`;}catch(e){} }

        function openAccModal(i) { const acc=itinerary[i].accommodation||{name:"",mapLink:"",checkInLink:""}; document.getElementById('acc-day-idx').value=i; document.getElementById('acc-name').value=acc.name; document.getElementById('acc-map').value=acc.mapLink; document.getElementById('acc-link').value=acc.checkInLink; document.getElementById('acc-modal').classList.remove('hidden'); }
        function saveAccModal() { const i=document.getElementById('acc-day-idx').value; itinerary[i].accommodation={name:document.getElementById('acc-name').value, mapLink:document.getElementById('acc-map').value, checkInLink:document.getElementById('acc-link').value}; localStorage.setItem('trip_v41_plan',JSON.stringify(itinerary)); renderItinerary(i); closeAccModal(); }
        function closeAccModal() { document.getElementById('acc-modal').classList.add('hidden'); }

        // --- FOOD & GUIDE ---
        function renderGuideCountries(){ document.getElementById('guide-country-navigator').innerHTML=Object.keys(defaultGuideData).map(c=>`<button onclick="currentGuideCountry='${c}';renderGuideCountries();renderGuideList('${c}')" class="flex-shrink-0 px-4 py-2 rounded-full text-xs font-bold transition-all border ${c===currentGuideCountry?'active-tab-btn':'bg-white text-stone-500 border-stone-100'}">${c}</button>`).join(''); }
        function renderGuideList(c){ 
            const guides = defaultGuideData[c]||[];
            const souvenirs = souvenirData[c]||[];
            
            let html = guides.map(g => `<div class="bg-white rounded-xl overflow-hidden shadow-sm mb-4 border border-stone-100"><div class="h-40 bg-gray-200 relative"><img src="${g.img}" class="w-full h-full object-cover"><div class="absolute bottom-0 left-0 right-0 bg-gradient-to-t from-black/60 to-transparent p-3"><h3 class="font-serif font-bold text-xl text-white">${g.title}</h3></div></div><div class="p-4"><p class="text-sm text-stone-600 line-clamp-2 mb-3">${g.history}</p><button onclick="openGuideModal('${g.title}',event)" class="w-full text-xs font-bold text-accent bg-orange-50 py-2 rounded-lg hover:bg-orange-100 transition">查看詳細導覽</button></div></div>`).join('');

            if(souvenirs.length > 0){
                html += `<div class="mt-8 mb-6"><h3 class="font-serif text-xl text-primary border-b-2 border-accent pb-2 mb-4 px-2">🛍️ 推薦伴手禮 Souvenirs</h3><div class="grid grid-cols-1 gap-3">`;
                html += souvenirs.map(s => `
                    <div class="bg-white p-4 rounded-xl shadow-sm border border-stone-100 flex flex-col gap-1">
                        <div class="flex justify-between items-start">
                            <h4 class="font-bold text-base text-primary">${s.name}</h4>
                            <span class="text-[10px] font-bold text-white bg-pink-400 px-2 py-1 rounded-full">推薦: ${s.shop}</span>
                        </div>
                        <p class="text-sm text-stone-600 mt-1 leading-relaxed">${s.desc}</p>
                    </div>`).join('');
                html += `</div></div>`;
            }
            document.getElementById('guide-container').innerHTML = html;
        }
        function renderFoodCities(){ document.getElementById('food-city-navigator').innerHTML=Object.keys(foodData).map(c=>`<button onclick="currentFoodCity='${c}';renderFoodCities();renderFoodList('${c}')" class="flex-shrink-0 px-4 py-2 rounded-full text-xs font-bold transition-all border ${c===currentFoodCity?'active-tab-btn':'bg-white text-stone-500 border-stone-100'}">${c}</button>`).join(''); }
        function renderFoodList(c){ const l=foodData[c]||[]; document.getElementById('food-list-display').innerHTML=l.map((x,i)=>`<div class="bg-white rounded-xl p-4 shadow-sm border border-stone-100 group"><h3 class="font-bold text-accent text-lg mb-1">${x.name}</h3><div class="text-yellow-400 text-xs mb-1">${'⭐'.repeat(Math.round(x.rating || 4))} <span class="text-stone-400 ml-1">${x.rating || 4.0}</span></div><div class="text-xs text-stone-500 mb-2"><i class="far fa-clock mr-1"></i>${x.hours}</div><p class="text-sm text-stone-600 bg-orange-50 p-2 rounded-lg mb-3">${x.note}</p><div class="flex justify-end gap-3 border-t border-stone-50 pt-2"><button onclick="editFoodItem('${c}',${i})" class="text-xs font-bold text-stone-400">編輯</button><a href="${x.map}" target="_blank" class="text-xs font-bold text-accent bg-orange-100 px-3 py-1 rounded-full">📍 導航</a></div></div>`).join(''); }

        // --- MODALS & UTILS ---
        function switchTab(id){ document.querySelectorAll('.tab-content').forEach(e=>e.classList.remove('active')); document.getElementById(`tab-${id}`).classList.add('active'); document.querySelectorAll('.nav-item').forEach(e=>e.classList.remove('active')); document.getElementById(`nav-${id}`).classList.add('active'); }
        function jumpToToday(){ const d=new Date(); const s=`${d.getMonth()+1}/${d.getDate()}`; const idx=itinerary.findIndex(x=>x.date===s); if(idx!==-1)changeDay(idx); else changeDay(0); switchTab('plan'); }
        
        // Itinerary Edit
        function openEditModal(d,i){ const it=itinerary[d].items[i]; document.getElementById('modal-day-idx').value=d; document.getElementById('modal-item-idx').value=i; document.getElementById('modal-time').value=it.time; document.getElementById('modal-category').value=it.category; document.getElementById('modal-title').value=it.title; document.getElementById('modal-map-url').value=it.mapUrl||""; document.getElementById('modal-cost').value=it.cost; document.getElementById('modal-currency').value=it.currency; document.getElementById('modal-note').value=it.note; document.getElementById('edit-modal').classList.remove('hidden'); }
        function addNewItem(d){ document.getElementById('modal-day-idx').value=d; document.getElementById('modal-item-idx').value="NEW"; document.getElementById('edit-form').reset(); document.getElementById('edit-modal').classList.remove('hidden'); }
        function saveModal(){ const d=document.getElementById('modal-day-idx').value; const i=document.getElementById('modal-item-idx').value; const item={time:document.getElementById('modal-time').value, category:document.getElementById('modal-category').value, title:document.getElementById('modal-title').value, mapUrl:document.getElementById('modal-map-url').value, cost:document.getElementById('modal-cost').value, currency:document.getElementById('modal-currency').value, note:document.getElementById('modal-note').value}; if(i==="NEW") itinerary[d].items.push(item); else itinerary[d].items[i]=item; localStorage.setItem('trip_v41_plan',JSON.stringify(itinerary)); renderItinerary(d); closeModal(); }
        function deleteCurrentItem(){ const d=document.getElementById('modal-day-idx').value; const i=document.getElementById('modal-item-idx').value; if(i!=="NEW"&&confirm("刪除?")){ itinerary[d].items.splice(i,1); localStorage.setItem('trip_v41_plan',JSON.stringify(itinerary)); renderItinerary(d); } closeModal(); }
        function closeModal(){ document.getElementById('edit-modal').classList.add('hidden'); }

        // Food Edit
        function addFoodItem(){ document.getElementById('food-idx').value="NEW"; document.getElementById('food-form').reset(); document.getElementById('food-modal').classList.remove('hidden'); }
        function editFoodItem(c,i){ const it=foodData[c][i]; document.getElementById('food-idx').value=i; document.getElementById('food-name').value=it.name; document.getElementById('food-rating').value=it.rating || 4.5; document.getElementById('food-note').value=it.note; document.getElementById('food-hours').value=it.hours; document.getElementById('food-map').value=it.map; document.getElementById('food-modal').classList.remove('hidden'); }
        function saveFoodModal(){ const idx=document.getElementById('food-idx').value; const item={name:document.getElementById('food-name').value, rating: document.getElementById('food-rating').value, note:document.getElementById('food-note').value, hours:document.getElementById('food-hours').value, map:document.getElementById('food-map').value || `https://www.google.com/maps/search/?api=1&query=${encodeURIComponent(document.getElementById('food-name').value)}`}; if(idx==="NEW") foodData[currentFoodCity].push(item); else foodData[currentFoodCity][idx]=item; localStorage.setItem('trip_v41_food',JSON.stringify(foodData)); renderFoodList(currentFoodCity); closeFoodModal(); }
        function deleteFoodItem(){ const idx=document.getElementById('food-idx').value; if(idx!=="NEW"&&confirm("刪除?")){ foodData[currentFoodCity].splice(idx,1); localStorage.setItem('trip_v41_food',JSON.stringify(foodData)); renderFoodList(currentFoodCity); } closeFoodModal(); }
        function closeFoodModal(){ document.getElementById('food-modal').classList.add('hidden'); }

        // Wallet / Lists / Guide (Standard)
        function calculate(){ try{document.getElementById('calc-result').innerText=Math.round(eval(document.getElementById('calc-input').value)*document.getElementById('currency-select').value).toLocaleString();}catch(e){} }
        function renderChecklist(){ document.getElementById('checklist-container').innerHTML=checklist.map((c,i)=>`<label class="flex p-2 border-b"><input type="checkbox" ${c.done?'checked':''} onchange="checklist[${i}].done=this.checked;localStorage.setItem('trip_v41_check',JSON.stringify(checklist));renderChecklist()" class="mr-2"><span>${c.text}</span></label>`).join(''); }
        function addTodo(){ const v=document.getElementById('new-todo').value; if(!v)return; checklist.push({text:v, done:false}); localStorage.setItem('trip_v41_check',JSON.stringify(checklist)); renderChecklist(); document.getElementById('new-todo').value=''; }
        function toggleCheck(i) { checklist[i].done=!checklist[i].done; localStorage.setItem('trip_v41_check',JSON.stringify(checklist)); renderChecklist(); }
        function delCheck(i) { checklist.splice(i,1); localStorage.setItem('trip_v41_check',JSON.stringify(checklist)); renderChecklist(); }
        function openGuideModal(k,e){ e.stopPropagation(); const g=guideLibrary[k]; if(!g)return; document.getElementById('guide-modal-title').innerText=k; document.getElementById('guide-modal-img').src=g.img; document.getElementById('guide-modal-photo').innerHTML=g.photo; document.getElementById('guide-modal-history').innerHTML=g.history; document.getElementById('guide-modal-arch').innerHTML=g.arch; document.getElementById('guide-modal-view').innerHTML=g.view; document.getElementById('guide-modal').classList.remove('hidden'); }
        function closeGuideModal(){ document.getElementById('guide-modal').classList.add('hidden'); }
        
        // Export & Import
        function exportData() {
            const data = {
                plan: localStorage.getItem('trip_v41_plan'),
                food: localStorage.getItem('trip_v41_food'),
                expenses: localStorage.getItem('trip_v41_expenses'),
                check: localStorage.getItem('trip_v41_check'),
                notes: localStorage.getItem('trip_v41_notes'), // Export notes instead of memo
                flights: localStorage.getItem('trip_v41_flights')
            };
            const jsonStr = JSON.stringify(data);
            const blob = new Blob([jsonStr], {type: "application/json"});
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `EuropeTrip_Backup_${new Date().toISOString().slice(0,10)}.json`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
        }

        function importData(input) {
            const file = input.files[0];
            if (!file) return;
            
            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    const data = JSON.parse(e.target.result);
                    if(data.plan) localStorage.setItem('trip_v41_plan', data.plan);
                    if(data.food) localStorage.setItem('trip_v41_food', data.food);
                    if(data.expenses) localStorage.setItem('trip_v41_expenses', data.expenses);
                    if(data.check) localStorage.setItem('trip_v41_check', data.check);
                    if(data.notes) localStorage.setItem('trip_v41_notes', data.notes); // Import notes
                    if(data.flights) localStorage.setItem('trip_v41_flights', data.flights);
                    
                    alert("匯入成功！頁面將重新整理以載入最新資料。");
                    location.reload();
                } catch (err) {
                    alert("檔案格式錯誤，無法匯入。");
                }
            };
            reader.readAsText(file);
            input.value = ''; // Reset input
        }
    </script>
</body>
</html>

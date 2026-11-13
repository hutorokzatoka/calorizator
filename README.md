# calorizator
Анализатор продуктов.для комплексного контроля питания, состава тела и физической формы. Платформа объединяет в себе профессиональный анализатор продуктов/блюд и медицинский калькулятор параметров тела.
<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>BodyAnalyzer — тело, калории и база продуктов</title>
<script src="https://cdn.tailwindcss.com/3.4.17"></script>
<link rel="preconnect" href="https://fonts.googleapis.com"><link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
<script>tailwind.config={theme:{extend:{fontFamily:{sans:['Inter','system-ui','sans-serif']}}}}</script>
<style>
:root{color-scheme:light;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
html{scroll-behavior:smooth;scroll-padding-top:env(safe-area-inset-top,0px)}
body{background-color:#F4F9F6;color:#064E3B;font-family:Inter,system-ui,sans-serif}

        /* Плавные анимации и кастомный скроллбар */
        html {
            scroll-behavior: smooth;
        }
        body {
            background-color: #F4F9F6;
            color: #064E3B;
        }
        .card-shadow {
            box-shadow: 0 10px 30px -5px rgba(6, 78, 59, 0.06), 0 4px 12px -2px rgba(16, 185, 129, 0.04);
        }
        .progress-transition {
            transition: width 0.6s cubic-bezier(0.22, 1, 0.36, 1), left 0.6s cubic-bezier(0.22, 1, 0.36, 1);
        }
        /* Убираем стрелочки у input[type=number] */
        input[type=number]::-webkit-inner-spin-button, 
        input[type=number]::-webkit-outer-spin-button { 
            -webkit-appearance: none; 
            margin: 0; 
        }
        input[type=number] {
            -moz-appearance: textfield;
        }
    
.page{display:none}.page.active{display:block}
.navl{color:#065F46}.navl:hover{background:#D1FAE5}.navl.on{background:#059669;color:#fff}
</style>
</head>
<body class="min-h-screen flex flex-col antialiased selection:bg-emerald-200 selection:text-emerald-900">
<div id="toast" class="fixed bottom-5 right-5 z-50 transform translate-y-24 opacity-0 transition-all duration-300 pointer-events-none"><div class="bg-emerald-900 text-white px-5 py-3.5 rounded-2xl shadow-xl border border-emerald-700"><span id="toast-msg" class="text-sm font-medium">Сообщение</span></div></div>
<header class="sticky top-0 z-40 bg-white/90 backdrop-blur-md border-b border-emerald-100">
 <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between gap-4">
  <a href="#home" class="flex items-center gap-3"><div class="w-10 h-10 rounded-2xl bg-gradient-to-br from-emerald-500 to-teal-600 flex items-center justify-center text-white text-lg">🥗</div><div><div class="text-lg font-extrabold tracking-tight text-emerald-950 leading-none">Body<span class="text-emerald-600">Analyzer</span></div><div id="header-subtitle" class="text-xs text-emerald-700/80 font-medium mt-0.5 hidden sm:block">Тело, калории и база продуктов</div></div></a>
  <nav class="hidden md:flex items-center gap-1 bg-emerald-50/80 p-1.5 rounded-2xl border border-emerald-200/60"><a href="#home" data-nav="home" class="navl px-3.5 py-2 rounded-xl text-xs font-bold whitespace-nowrap transition-all">Главная</a><a href="#body" data-nav="body" class="navl px-3.5 py-2 rounded-xl text-xs font-bold whitespace-nowrap transition-all">Анализ тела</a><a href="#recipe" data-nav="recipe" class="navl px-3.5 py-2 rounded-xl text-xs font-bold whitespace-nowrap transition-all">Рецепты</a><a href="#diary" data-nav="diary" class="navl px-3.5 py-2 rounded-xl text-xs font-bold whitespace-nowrap transition-all">Дневник</a><a href="#catalog" data-nav="catalog" class="navl px-3.5 py-2 rounded-xl text-xs font-bold whitespace-nowrap transition-all">База продуктов</a></nav>
  <div class="flex items-center bg-emerald-50 p-1 rounded-xl border border-emerald-200/70"><button type="button" onclick="setLanguage('ru')" id="lang-ru" class="lang-btn px-3 py-1.5 rounded-lg text-xs font-semibold transition-all bg-emerald-600 text-white shadow-sm">RU</button><button type="button" onclick="setLanguage('ua')" id="lang-ua" class="lang-btn px-3 py-1.5 rounded-lg text-xs font-semibold transition-all text-emerald-800 hover:bg-emerald-100">UA</button><button type="button" onclick="setLanguage('en')" id="lang-en" class="lang-btn px-3 py-1.5 rounded-lg text-xs font-semibold transition-all text-emerald-800 hover:bg-emerald-100">EN</button></div>
 </div>
 <nav class="md:hidden flex gap-1 overflow-x-auto bg-emerald-50 border-t border-emerald-100 px-2 py-1.5"><a href="#home" data-mnav="home" class="navl px-3.5 py-2 rounded-xl text-xs font-bold whitespace-nowrap transition-all">Главная</a><a href="#body" data-mnav="body" class="navl px-3.5 py-2 rounded-xl text-xs font-bold whitespace-nowrap transition-all">Анализ тела</a><a href="#recipe" data-mnav="recipe" class="navl px-3.5 py-2 rounded-xl text-xs font-bold whitespace-nowrap transition-all">Рецепты</a><a href="#diary" data-mnav="diary" class="navl px-3.5 py-2 rounded-xl text-xs font-bold whitespace-nowrap transition-all">Дневник</a><a href="#catalog" data-mnav="catalog" class="navl px-3.5 py-2 rounded-xl text-xs font-bold whitespace-nowrap transition-all">База продуктов</a></nav>
</header>
<main class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6 sm:py-8">
<div id="page-home" class="page space-y-8">
  <div class="bg-gradient-to-r from-emerald-800 via-emerald-700 to-teal-700 rounded-3xl p-8 sm:p-12 text-white shadow-lg">
    <h2 class="text-3xl sm:text-4xl font-extrabold tracking-tight mb-3">Здоровье под контролем</h2>
    <p class="text-emerald-100/90 text-base sm:text-lg max-w-2xl leading-relaxed">Рассчитайте параметры тела, соберите рецепт с точным КБЖУ и ведите дневник питания — всё в одном месте, с большой базой продуктов и готовых блюд.</p>
    <div class="flex flex-wrap gap-3 mt-6">
      <button onclick="go('body')" class="px-5 py-3 bg-white text-emerald-900 font-bold text-sm rounded-xl cursor-pointer">Анализ тела</button>
      <button onclick="go('catalog')" class="px-5 py-3 bg-emerald-950/40 border border-emerald-300/40 text-white font-bold text-sm rounded-xl cursor-pointer">База продуктов</button>
    </div>
  </div>
  <div class="grid grid-cols-1 md:grid-cols-4 gap-5">
    <button onclick="go('body')" class="text-left bg-white rounded-3xl p-6 card-shadow border border-emerald-100/80 cursor-pointer hover:border-emerald-400"><div class="text-3xl mb-2">⚖️</div><div class="font-bold text-emerald-950">Анализатор тела</div><p class="text-xs text-emerald-700/80 mt-1">ИМТ, метаболизм, норма калорий, процент жира, вода.</p></button>
    <button onclick="go('recipe')" class="text-left bg-white rounded-3xl p-6 card-shadow border border-emerald-100/80 cursor-pointer hover:border-emerald-400"><div class="text-3xl mb-2">🥗</div><div class="font-bold text-emerald-950">Рецепты и КБЖУ</div><p class="text-xs text-emerald-700/80 mt-1">Соберите блюдо и узнайте калорийность на 100 г.</p></button>
    <button onclick="go('diary')" class="text-left bg-white rounded-3xl p-6 card-shadow border border-emerald-100/80 cursor-pointer hover:border-emerald-400"><div class="text-3xl mb-2">📅</div><div class="font-bold text-emerald-950">Дневник питания</div><p class="text-xs text-emerald-700/80 mt-1">Записывайте приемы пищи и считайте итоги дня.</p></button>
    <button onclick="go('catalog')" class="text-left bg-white rounded-3xl p-6 card-shadow border border-emerald-100/80 cursor-pointer hover:border-emerald-400"><div class="text-3xl mb-2">📚</div><div class="font-bold text-emerald-950">База: <span id="statCount">0</span></div><p class="text-xs text-emerald-700/80 mt-1">Продукты и готовые блюда, поиск и импорт.</p></button>
  </div>
</div>
<div id="page-body" class="page">
        
        <!-- Приветственный баннер -->
        <div class="mb-8 bg-gradient-to-r from-emerald-800 via-emerald-700 to-teal-700 rounded-3xl p-6 sm:p-8 text-white shadow-lg relative overflow-hidden">
            <div class="absolute right-0 top-0 -mt-10 -mr-10 w-64 h-64 rounded-full bg-emerald-500/20 blur-2xl pointer-events-none"></div>
            <div class="relative z-10 max-w-3xl">
                <span class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full bg-emerald-950/40 border border-emerald-400/30 text-emerald-200 text-xs font-semibold mb-3">
                    <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span>
                    <span data-i18n="badgeText">Научные формулы ВОЗ, Миффлина-Сан Жеора и US Navy</span>
                </span>
                <h2 data-i18n="heroTitle" class="text-2xl sm:text-3xl font-bold tracking-tight mb-2">
                    Узнайте точные показатели вашего тела
                </h2>
                <p data-i18n="heroDesc" class="text-emerald-100/90 text-sm sm:text-base leading-relaxed">
                    Рассчитайте индекс массы тела, идеальный вес по 5 методикам, базовый метаболизм, процент жира, сухую мышечную массу и индивидуальную норму КБЖУ и воды.
                </p>
            </div>
        </div>

        <!-- Сетка: Форма ввода (слева) и Результаты (справа) -->
        <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">
            
            <!-- ЛЕВАЯ КОЛОНКА: ФОРМА ВВОДА -->
            <section class="lg:col-span-5 bg-white rounded-3xl p-5 sm:p-7 card-shadow border border-emerald-100/80">
                <div class="flex flex-wrap items-center justify-between gap-2 pb-5 mb-6 border-b border-emerald-100">
                    <h3 data-i18n="formTitle" class="text-lg sm:text-xl font-bold text-emerald-950 flex items-center gap-2">
                        <svg class="w-5 h-5 text-emerald-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"></path>
                        </svg>
                        <span>Ваши параметры</span>
                    </h3>

                    <!-- Переключатель единиц измерения -->
                    <div class="flex bg-emerald-50 p-1 rounded-xl border border-emerald-200/60 text-xs font-semibold">
                        <button type="button" id="unit-metric" onclick="setUnitSystem('metric')" class="px-2.5 py-1.5 rounded-lg bg-white text-emerald-800 shadow-sm transition-all" data-i18n="unitMetric">
                            см / кг
                        </button>
                        <button type="button" id="unit-imperial" onclick="setUnitSystem('imperial')" class="px-2.5 py-1.5 rounded-lg text-emerald-700 hover:text-emerald-900 transition-all" data-i18n="unitImperial">
                            ft / lbs
                        </button>
                    </div>
                </div>

                <form id="analyzer-form" onsubmit="event.preventDefault(); calculateAll(true);" class="space-y-5">
                    
                    <!-- Выбор пола -->
                    <div>
                        <label data-i18n="labelGender" class="block text-sm font-semibold text-emerald-900 mb-2">Пол</label>
                        <div class="grid grid-cols-2 gap-3">
                            <label class="cursor-pointer">
                                <input type="radio" name="gender" value="male" checked onchange="calculateAll()" class="peer sr-only">
                                <div class="flex items-center justify-center gap-2 py-3 px-4 rounded-2xl border-2 border-emerald-100 bg-emerald-50/40 text-emerald-800 font-semibold transition-all peer-checked:border-emerald-500 peer-checked:bg-emerald-50 peer-checked:text-emerald-950 peer-checked:shadow-sm">
                                    <svg class="w-5 h-5 text-emerald-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"></path>
                                    </svg>
                                    <span data-i18n="genderMale">Мужской</span>
                                </div>
                            </label>
                            <label class="cursor-pointer">
                                <input type="radio" name="gender" value="female" onchange="calculateAll()" class="peer sr-only">
                                <div class="flex items-center justify-center gap-2 py-3 px-4 rounded-2xl border-2 border-emerald-100 bg-emerald-50/40 text-emerald-800 font-semibold transition-all peer-checked:border-emerald-500 peer-checked:bg-emerald-50 peer-checked:text-emerald-950 peer-checked:shadow-sm">
                                    <svg class="w-5 h-5 text-emerald-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197M13 7a4 4 0 11-8 0 4 4 0 018 0z"></path>
                                    </svg>
                                    <span data-i18n="genderFemale">Женский</span>
                                </div>
                            </label>
                        </div>
                    </div>

                    <!-- Возраст, Рост, Вес -->
                    <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
                        <!-- Возраст -->
                        <div>
                            <label for="age" class="block text-xs font-semibold text-emerald-900 mb-1.5">
                                <span data-i18n="labelAge">Возраст</span> (<span data-i18n="unitYears">лет</span>)
                            </label>
                            <input type="number" id="age" min="14" max="100" value="30" oninput="calculateAll()"
                                class="w-full px-3.5 py-2.5 rounded-xl border border-emerald-200 bg-emerald-50/30 text-emerald-950 font-semibold focus:outline-none focus:ring-2 focus:ring-emerald-500 focus:bg-white transition-all">
                        </div>

                        <!-- Рост (Метрический) -->
                        <div id="height-metric-box">
                            <label for="height-cm" class="block text-xs font-semibold text-emerald-900 mb-1.5">
                                <span data-i18n="labelHeight">Рост</span> (<span data-i18n="unitCm">см</span>)
                            </label>
                            <input type="number" id="height-cm" min="100" max="250" step="0.5" value="178" oninput="calculateAll()"
                                class="w-full px-3.5 py-2.5 rounded-xl border border-emerald-200 bg-emerald-50/30 text-emerald-950 font-semibold focus:outline-none focus:ring-2 focus:ring-emerald-500 focus:bg-white transition-all">
                        </div>

                        <!-- Рост (Имперский: футы и дюймы) -->
                        <div id="height-imperial-box" class="hidden">
                            <label class="block text-xs font-semibold text-emerald-900 mb-1.5">
                                <span data-i18n="labelHeight">Рост</span> (ft / in)
                            </label>
                            <div class="grid grid-cols-2 gap-1.5">
                                <input type="number" id="height-ft" min="3" max="8" value="5" oninput="calculateAll()" placeholder="ft"
                                    class="w-full px-2.5 py-2.5 rounded-xl border border-emerald-200 bg-emerald-50/30 text-emerald-950 font-semibold focus:outline-none focus:ring-2 focus:ring-emerald-500 focus:bg-white transition-all">
                                <input type="number" id="height-in" min="0" max="11" step="0.5" value="10" oninput="calculateAll()" placeholder="in"
                                    class="w-full px-2.5 py-2.5 rounded-xl border border-emerald-200 bg-emerald-50/30 text-emerald-950 font-semibold focus:outline-none focus:ring-2 focus:ring-emerald-500 focus:bg-white transition-all">
                            </div>
                        </div>

                        <!-- Вес -->
                        <div>
                            <label for="weight" class="block text-xs font-semibold text-emerald-900 mb-1.5">
                                <span data-i18n="labelWeight">Вес</span> (<span id="weight-unit-label" data-i18n="unitKg">кг</span>)
                            </label>
                            <input type="number" id="weight" min="30" max="300" step="0.1" value="76" oninput="calculateAll()"
                                class="w-full px-3.5 py-2.5 rounded-xl border border-emerald-200 bg-emerald-50/30 text-emerald-950 font-semibold focus:outline-none focus:ring-2 focus:ring-emerald-500 focus:bg-white transition-all">
                        </div>
                    </div>

                    <!-- Уровень физической активности -->
                    <div>
                        <label for="activity" data-i18n="labelActivity" class="block text-sm font-semibold text-emerald-900 mb-1.5">
                            Уровень физической активности
                        </label>
                        <select id="activity" onchange="updateActivityDesc(); calculateAll();"
                            class="w-full px-3.5 py-3 rounded-xl border border-emerald-200 bg-emerald-50/30 text-emerald-950 font-medium text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500 focus:bg-white transition-all">
                            <option value="1.2" data-i18n="act1">1.2 — Минимальный (сидячая работа)</option>
                            <option value="1.375" selected data-i18n="act2">1.375 — Легкий (тренировки 1–3 раза в неделю)</option>
                            <option value="1.55" data-i18n="act3">1.55 — Средний (тренировки 3–5 раз в неделю)</option>
                            <option value="1.725" data-i18n="act4">1.725 — Высокий (интенсивные 6–7 раз в неделю)</option>
                            <option value="1.9" data-i18n="act5">1.9 — Экстремальный (тяжелый труд / 2 тренировки в день)</option>
                        </select>
                        <p id="activity-desc" class="mt-2 text-xs text-emerald-700 bg-emerald-50/80 p-2.5 rounded-xl border border-emerald-100 leading-relaxed">
                            Легкие физические упражнения или спорт 1–3 раза в неделю, регулярные пешие прогулки.
                        </p>
                    </div>

                    <!-- Дополнительные обхваты (для % жира и соматотипа) -->
                    <div class="pt-3 border-t border-emerald-100">
                        <div class="flex items-center justify-between mb-3">
                            <div>
                                <h4 data-i18n="measurementsTitle" class="text-sm font-bold text-emerald-950">
                                    Обхваты тела (для анализа состава)
                                </h4>
                                <p data-i18n="measurementsSub" class="text-xs text-emerald-600">
                                    Необходимы для расчета % жира и типа телосложения
                                </p>
                            </div>
                            <span class="text-xs font-semibold px-2 py-0.5 rounded-md bg-emerald-100 text-emerald-800" id="circ-unit-badge">см</span>
                        </div>

                        <div class="grid grid-cols-2 gap-3.5">
                            <!-- Шея -->
                            <div>
                                <label for="neck" class="block text-xs font-semibold text-emerald-900 mb-1">
                                    <span data-i18n="labelNeck">Шея</span> (<span class="circ-unit">см</span>)
                                </label>
                                <input type="number" id="neck" min="20" max="80" step="0.5" value="38" oninput="calculateAll()"
                                    class="w-full px-3.5 py-2 rounded-xl border border-emerald-200 bg-emerald-50/30 text-emerald-950 font-semibold text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500 focus:bg-white transition-all">
                            </div>

                            <!-- Талия -->
                            <div>
                                <label for="waist" class="block text-xs font-semibold text-emerald-900 mb-1">
                                    <span data-i18n="labelWaist">Талия</span> (<span class="circ-unit">см</span>)
                                </label>
                                <input type="number" id="waist" min="40" max="200" step="0.5" value="82" oninput="calculateAll()"
                                    class="w-full px-3.5 py-2 rounded-xl border border-emerald-200 bg-emerald-50/30 text-emerald-950 font-semibold text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500 focus:bg-white transition-all">
                            </div>

                            <!-- Бедра -->
                            <div>
                                <label for="hips" class="block text-xs font-semibold text-emerald-900 mb-1">
                                    <span data-i18n="labelHips">Бедра</span> (<span class="circ-unit">см</span>)
                                </label>
                                <input type="number" id="hips" min="50" max="220" step="0.5" value="98" oninput="calculateAll()"
                                    class="w-full px-3.5 py-2 rounded-xl border border-emerald-200 bg-emerald-50/30 text-emerald-950 font-semibold text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500 focus:bg-white transition-all">
                            </div>

                            <!-- Запястье -->
                            <div>
                                <label for="wrist" class="block text-xs font-semibold text-emerald-900 mb-1">
                                    <span data-i18n="labelWrist">Запястье</span> (<span class="circ-unit">см</span>)
                                </label>
                                <input type="number" id="wrist" min="10" max="30" step="0.1" value="17.5" oninput="calculateAll()"
                                    class="w-full px-3.5 py-2 rounded-xl border border-emerald-200 bg-emerald-50/30 text-emerald-950 font-semibold text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500 focus:bg-white transition-all">
                            </div>
                        </div>
                    </div>

                    <!-- Кнопки управления -->
                    <div class="pt-3 space-y-2.5">
                        <button type="submit" class="w-full py-3.5 px-6 rounded-2xl bg-gradient-to-r from-emerald-600 to-teal-600 hover:from-emerald-500 hover:to-teal-500 text-white font-bold text-sm sm:text-base shadow-lg shadow-emerald-600/25 transition-all transform active:scale-[0.99] flex items-center justify-center gap-2">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.2" d="M9 7h6m0 10v-3m-3 3h.01M9 17h.01M9 14h.01M12 14h.01M15 11h.01M12 11h.01M9 11h.01M7 21h10a2 2 0 002-2V5a2 2 0 00-2-2H7a2 2 0 00-2 2v14a2 2 0 002 2z"></path>
                            </svg>
                            <span data-i18n="btnCalculate">Рассчитать показатели</span>
                        </button>

                        <div class="grid grid-cols-2 gap-2.5">
                            <button type="button" onclick="fillDemoData()" class="py-2.5 px-3 rounded-xl bg-emerald-50 hover:bg-emerald-100 text-emerald-800 font-semibold text-xs transition-colors border border-emerald-200/70 flex items-center justify-center gap-1.5">
                                <svg class="w-4 h-4 text-emerald-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"></path>
                                </svg>
                                <span data-i18n="btnDemo">Демо-данные</span>
                            </button>
                            <button type="button" onclick="resetForm()" class="py-2.5 px-3 rounded-xl bg-slate-50 hover:bg-slate-100 text-slate-600 font-semibold text-xs transition-colors border border-slate-200 flex items-center justify-center gap-1.5">
                                <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15"></path>
                                </svg>
                                <span data-i18n="btnReset">Сбросить</span>
                            </button>
                        </div>
                    </div>
                </form>
            </section>

            <!-- ПРАВАЯ КОЛОНКА: РЕЗУЛЬТАТЫ РАСЧЕТОВ -->
            <section class="lg:col-span-7 space-y-6" id="results-section">
                
                <!-- 1. КАРТОЧКА ИМТ (BMI) -->
                <div class="bg-white rounded-3xl p-6 sm:p-7 card-shadow border border-emerald-100/80">
                    <div class="flex flex-wrap items-start justify-between gap-4 mb-5">
                        <div>
                            <span class="text-xs font-bold uppercase tracking-wider text-emerald-600" data-i18n="bmiTag">Индекс массы тела (ВОЗ)</span>
                            <h3 class="text-xl font-bold text-emerald-950 mt-0.5" data-i18n="bmiTitle">Оценка соответствия веса и роста</h3>
                        </div>
                        <div class="text-right">
                            <div class="text-3xl sm:text-4xl font-extrabold text-emerald-900" id="res-bmi-val">24.0</div>
                            <span id="res-bmi-badge" class="inline-block mt-1 px-3 py-1 rounded-full text-xs font-bold bg-emerald-100 text-emerald-800">
                                Нормальная масса тела
                            </span>
                        </div>
                    </div>

                    <!-- Цветовая шкала ИМТ -->
                    <div class="relative pt-6 pb-2">
                        <!-- Маркер текущего ИМТ -->
                        <div id="bmi-pointer" class="absolute top-0 -ml-3 transition-all duration-500 flex flex-col items-center" style="left: 42%;">
                            <span class="text-[11px] font-bold bg-emerald-950 text-white px-2 py-0.5 rounded-md shadow">Вы</span>
                            <div class="w-0 h-0 border-l-[5px] border-l-transparent border-r-[5px] border-r-transparent border-t-[6px] border-t-emerald-950"></div>
                        </div>

                        <!-- Полоса градаций -->
                        <div class="h-3.5 w-full rounded-full overflow-hidden flex shadow-inner bg-slate-100">
                            <div class="bg-sky-400 h-full" style="width: 18%" title="< 18.5"></div>
                            <div class="bg-emerald-500 h-full" style="width: 32%" title="18.5 - 24.9"></div>
                            <div class="bg-amber-400 h-full" style="width: 25%" title="25.0 - 29.9"></div>
                            <div class="bg-rose-500 h-full" style="width: 25%" title=">= 30.0"></div>
                        </div>

                        <!-- Подписи шкалы -->
                        <div class="flex justify-between text-[11px] font-semibold text-emerald-800/70 mt-2">
                            <span>15</span>
                            <span class="text-sky-600">18.5</span>
                            <span class="text-emerald-600">25.0</span>
                            <span class="text-amber-600">30.0</span>
                            <span class="text-rose-600">40+</span>
                        </div>
                    </div>

                    <div class="mt-4 pt-4 border-t border-emerald-50 flex flex-wrap items-center justify-between gap-2 text-sm">
                        <span class="text-emerald-700" data-i18n="healthyWeightRangeLabel">Здоровый диапазон веса для вашего роста:</span>
                        <span class="font-bold text-emerald-950 bg-emerald-50 px-3 py-1 rounded-xl border border-emerald-200/60" id="res-healthy-range">
                            58.6 — 78.9 кг
                        </span>
                    </div>
                </div>

                <!-- 2. КАЛОРИИ (BMR, TDEE) И ИНТЕРАКТИВНЫЙ КАЛЬКУЛЯТОР БЖУ -->
                <div class="bg-white rounded-3xl p-6 sm:p-7 card-shadow border border-emerald-100/80">
                    <div class="mb-5">
                        <span class="text-xs font-bold uppercase tracking-wider text-emerald-600" data-i18n="energyTag">Энергетический обмен</span>
                        <h3 class="text-xl font-bold text-emerald-950 mt-0.5" data-i18n="energyTitle">Базовый метаболизм (BMR) и норма калорий</h3>
                    </div>

                    <!-- Две формулы BMR -->
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 mb-6">
                        <div class="p-4 rounded-2xl bg-emerald-50/70 border border-emerald-200/70">
                            <div class="flex items-center justify-between mb-1">
                                <span class="text-xs font-bold text-emerald-800" data-i18n="bmrMifflinName">Миффлина — Сан-Жеора</span>
                                <span class="text-[10px] font-bold uppercase px-2 py-0.5 rounded bg-emerald-600 text-white" data-i18n="goldStandard">Рекомендуемая</span>
                            </div>
                            <div class="text-2xl font-extrabold text-emerald-950">
                                <span id="res-bmr-mifflin">1738</span> <span class="text-sm font-semibold text-emerald-700" data-i18n="unitKcal">ккал/день</span>
                            </div>
                            <p class="text-xs text-emerald-700/80 mt-1" data-i18n="bmrDesc">Расход энергии в состоянии полного покоя</p>
                        </div>

                        <div class="p-4 rounded-2xl bg-slate-50/90 border border-slate-200/80">
                            <div class="flex items-center justify-between mb-1">
                                <span class="text-xs font-bold text-slate-700" data-i18n="bmrHarrisName">Харриса — Бенедикта</span>
                                <span class="text-[10px] font-semibold px-2 py-0.5 rounded bg-slate-200 text-slate-700" data-i18n="classicFormula">Классическая</span>
                            </div>
                            <div class="text-2xl font-extrabold text-slate-800">
                                <span id="res-bmr-harris">1786</span> <span class="text-sm font-semibold text-slate-600" data-i18n="unitKcal">ккал/день</span>
                            </div>
                            <p class="text-xs text-slate-500 mt-1" data-i18n="bmrHarrisSub">Пересмотренная формула Роза и Шизгала</p>
                        </div>
                    </div>

                    <!-- Выбор цели для пересчета калорий и БЖУ -->
                    <div class="mb-5">
                        <label class="block text-xs font-bold uppercase tracking-wider text-emerald-800 mb-2.5" data-i18n="goalSelectTitle">
                            Выберите вашу цель (пересчет калорий и БЖУ):
                        </label>
                        <div class="grid grid-cols-3 gap-2 sm:gap-3 bg-emerald-50 p-1.5 rounded-2xl border border-emerald-200/60">
                            <button type="button" onclick="setGoal('lose')" id="goal-lose" class="goal-btn py-2.5 px-2 rounded-xl text-xs sm:text-sm font-bold transition-all text-emerald-800 hover:bg-white/60">
                                <div data-i18n="goalLose">Похудение</div>
                                <div class="text-[11px] font-medium opacity-80">-18% ккал</div>
                            </button>
                            <button type="button" onclick="setGoal('maintain')" id="goal-maintain" class="goal-btn py-2.5 px-2 rounded-xl text-xs sm:text-sm font-bold transition-all bg-emerald-600 text-white shadow-sm">
                                <div data-i18n="goalMaintain">Поддержание</div>
                                <div class="text-[11px] font-medium opacity-90">100% TDEE</div>
                            </button>
                            <button type="button" onclick="setGoal('gain')" id="goal-gain" class="goal-btn py-2.5 px-2 rounded-xl text-xs sm:text-sm font-bold transition-all text-emerald-800 hover:bg-white/60">
                                <div data-i18n="goalGain">Набор массы</div>
                                <div class="text-[11px] font-medium opacity-80">+15% ккал</div>
                            </button>
                        </div>
                    </div>

                    <!-- Итоговая калорийность под цель и БЖУ -->
                    <div class="bg-gradient-to-br from-emerald-900 to-teal-900 rounded-2xl p-5 text-white">
                        <div class="flex flex-wrap items-center justify-between gap-4 pb-4 mb-4 border-b border-emerald-700/60">
                            <div>
                                <div class="text-xs text-emerald-300 font-semibold" id="res-goal-label">Суточная норма для поддержания веса (TDEE)</div>
                                <div class="text-3xl sm:text-4xl font-extrabold mt-0.5 text-white">
                                    <span id="res-target-kcal">2390</span> <span class="text-base font-medium text-emerald-300" data-i18n="unitKcal">ккал/день</span>
                                </div>
                            </div>
                            <div class="text-xs text-emerald-200 bg-emerald-950/60 px-3.5 py-2 rounded-xl border border-emerald-700/50 space-y-1">
                                <div><span data-i18n="tdeeMaintainShort">Поддержание:</span> <strong id="mini-maintain" class="text-white">2390</strong></div>
                                <div><span data-i18n="tdeeLoseShort">Похудение:</span> <strong id="mini-lose" class="text-emerald-300">1960</strong></div>
                                <div><span data-i18n="tdeeGainShort">Набор массы:</span> <strong id="mini-gain" class="text-amber-300">2748</strong></div>
                            </div>
                        </div>

                        <!-- Карточки БЖУ -->
                        <div class="grid grid-cols-3 gap-3">
                            <!-- Белки -->
                            <div class="bg-white/10 backdrop-blur-sm rounded-xl p-3 border border-white/10">
                                <div class="flex items-center justify-between text-xs text-emerald-200 mb-1">
                                    <span data-i18n="macroProtein">Белки</span>
                                    <span id="macro-p-pct" class="font-bold text-emerald-300">30%</span>
                                </div>
                                <div class="text-xl sm:text-2xl font-extrabold"><span id="macro-p-g">179</span> <span class="text-xs font-normal" data-i18n="unitG">г</span></div>
                                <div class="w-full bg-emerald-950 h-1.5 rounded-full mt-2 overflow-hidden">
                                    <div id="bar-p" class="bg-emerald-400 h-full rounded-full progress-transition" style="width: 30%"></div>
                                </div>
                            </div>

                            <!-- Жиры -->
                            <div class="bg-white/10 backdrop-blur-sm rounded-xl p-3 border border-white/10">
                                <div class="flex items-center justify-between text-xs text-amber-200 mb-1">
                                    <span data-i18n="macroFat">Жиры</span>
                                    <span id="macro-f-pct" class="font-bold text-amber-300">25%</span>
                                </div>
                                <div class="text-xl sm:text-2xl font-extrabold"><span id="macro-f-g">66</span> <span class="text-xs font-normal" data-i18n="unitG">г</span></div>
                                <div class="w-full bg-emerald-950 h-1.5 rounded-full mt-2 overflow-hidden">
                                    <div id="bar-f" class="bg-amber-400 h-full rounded-full progress-transition" style="width: 25%"></div>
                                </div>
                            </div>

                            <!-- Углеводы -->
                            <div class="bg-white/10 backdrop-blur-sm rounded-xl p-3 border border-white/10">
                                <div class="flex items-center justify-between text-xs text-sky-200 mb-1">
                                    <span data-i18n="macroCarb">Углеводы</span>
                                    <span id="macro-c-pct" class="font-bold text-sky-300">45%</span>
                                </div>
                                <div class="text-xl sm:text-2xl font-extrabold"><span id="macro-c-g">269</span> <span class="text-xs font-normal" data-i18n="unitG">г</span></div>
                                <div class="w-full bg-emerald-950 h-1.5 rounded-full mt-2 overflow-hidden">
                                    <div id="bar-c" class="bg-sky-400 h-full rounded-full progress-transition" style="width: 45%"></div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- 3. СОСТАВ ТЕЛА (US NAVY % ЖИРА), СОМАТОТИП И НОРМА ВОДЫ -->
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    
                    <!-- Состав тела (Процент жира US Navy) -->
                    <div class="bg-white rounded-3xl p-6 card-shadow border border-emerald-100/80 flex flex-col justify-between">
                        <div>
                            <span class="text-xs font-bold uppercase tracking-wider text-emerald-600" data-i18n="bodyCompTag">Метод ВМС США (US Navy)</span>
                            <h3 class="text-lg font-bold text-emerald-950 mt-0.5 mb-4" data-i18n="bodyCompTitle">Процент жира и мышечная масса</h3>

                            <div id="bodyfat-valid-box">
                                <div class="flex items-baseline justify-between mb-2">
                                    <div class="text-3xl font-extrabold text-emerald-900" id="res-bf-pct">16.4%</div>
                                    <span id="res-bf-cat" class="px-2.5 py-1 rounded-lg text-xs font-bold bg-emerald-100 text-emerald-800">
                                        Фитнес-форма
                                    </span>
                                </div>

                                <!-- Визуальный бар соотношения мышцы / жир -->
                                <div class="w-full h-3 rounded-full bg-amber-300 overflow-hidden flex my-3">
                                    <div id="bf-lean-bar" class="bg-emerald-500 h-full progress-transition" style="width: 83.6%"></div>
                                </div>

                                <div class="space-y-2 mt-4 text-sm">
                                    <div class="flex justify-between items-center p-2.5 rounded-xl bg-emerald-50/70">
                                        <span class="flex items-center gap-2 text-emerald-800 font-medium">
                                            <span class="w-2.5 h-2.5 rounded-full bg-emerald-500"></span>
                                            <span data-i18n="leanMassLabel">Сухая масса (LBM):</span>
                                        </span>
                                        <span class="font-bold text-emerald-950" id="res-lean-mass">63.5 кг</span>
                                    </div>
                                    <div class="flex justify-between items-center p-2.5 rounded-xl bg-amber-50/70">
                                        <span class="flex items-center gap-2 text-amber-900 font-medium">
                                            <span class="w-2.5 h-2.5 rounded-full bg-amber-400"></span>
                                            <span data-i18n="fatMassLabel">Жировая масса:</span>
                                        </span>
                                        <span class="font-bold text-amber-950" id="res-fat-mass">12.5 кг</span>
                                    </div>
                                </div>
                            </div>

                            <div id="bodyfat-invalid-box" class="hidden p-4 rounded-2xl bg-amber-50 border border-amber-200 text-xs text-amber-900 leading-relaxed" data-i18n="bfInvalidMsg">
                                Укажите корректные обхваты шеи, талии (и бедер для женщин), чтобы рассчитать точный процент жира.
                            </div>
                        </div>

                        <!-- Соотношение талия/бедра (WHR) -->
                        <div class="mt-5 pt-4 border-t border-emerald-100 flex items-center justify-between text-xs">
                            <span class="text-emerald-700 font-medium" data-i18n="whrLabel">Индекс талия/бедра (WHR):</span>
                            <span class="font-bold text-emerald-950" id="res-whr">0.84 (Норма)</span>
                        </div>
                    </div>

                    <!-- Тип телосложения (Соловьев) и Норма воды -->
                    <div class="space-y-6 flex flex-col justify-between">
                        <!-- Соматотип -->
                        <div class="bg-white rounded-3xl p-6 card-shadow border border-emerald-100/80">
                            <span class="text-xs font-bold uppercase tracking-wider text-emerald-600" data-i18n="somatotypeTag">Индекс Соловьева</span>
                            <h3 class="text-lg font-bold text-emerald-950 mt-0.5 mb-2" data-i18n="somatotypeTitle">Тип телосложения</h3>
                            
                            <div class="flex items-center justify-between bg-emerald-50/80 p-3.5 rounded-2xl border border-emerald-100">
                                <div>
                                    <div class="text-base font-extrabold text-emerald-950" id="res-somatotype">Нормостеник</div>
                                    <div class="text-xs text-emerald-700 mt-0.5" id="res-somatotype-desc">Средняя кость, пропорциональное сложение</div>
                                </div>
                                <div class="w-11 h-11 rounded-xl bg-white flex items-center justify-center text-emerald-600 font-bold text-sm shadow-sm border border-emerald-100" id="res-wrist-display">
                                    17.5
                                </div>
                            </div>
                        </div>

                        <!-- Суточная норма воды -->
                        <div class="bg-gradient-to-br from-teal-50 to-emerald-50 rounded-3xl p-6 card-shadow border border-emerald-200/70">
                            <div class="flex items-start justify-between">
                                <div>
                                    <span class="text-xs font-bold uppercase tracking-wider text-teal-700" data-i18n="waterTag">Водный баланс</span>
                                    <h3 class="text-lg font-bold text-emerald-950 mt-0.5" data-i18n="waterTitle">Суточная норма воды</h3>
                                </div>
                                <div class="w-10 h-10 rounded-2xl bg-teal-500/15 text-teal-600 flex items-center justify-center">
                                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19.428 15.428a2 2 0 00-1.022-.547l-2.387-.477a6 6 0 00-3.86.517l-.318.158a6 6 0 01-3.86.517L6.05 15.21a2 2 0 00-1.806.547M8 4h8l-1 1v5.172a2 2 0 00.586 1.414l5 5c1.26 1.26.367 3.414-1.415 3.414H4.828c-1.782 0-2.674-2.154-1.414-3.414l5-5A2 2 0 009 10.172V5L8 4z"></path>
                                    </svg>
                                </div>
                            </div>
                            <div class="mt-3 flex items-baseline gap-2">
                                <span class="text-3xl font-extrabold text-teal-900" id="res-water-liters">2.65 л</span>
                                <span class="text-sm font-semibold text-teal-700" id="res-water-ml">(2650 мл)</span>
                            </div>
                            <p class="text-xs text-teal-800/80 mt-1.5" data-i18n="waterDesc">
                                Рассчитано с учетом вашего веса и выбранного уровня физической активности.
                            </p>
                        </div>
                    </div>
                </div>

                <!-- 4. ИДЕАЛЬНЫЙ ВЕС ПО 5 ФОРМУЛАМ -->
                <div class="bg-white rounded-3xl p-6 sm:p-7 card-shadow border border-emerald-100/80">
                    <div class="flex flex-wrap items-center justify-between gap-2 mb-5">
                        <div>
                            <span class="text-xs font-bold uppercase tracking-wider text-emerald-600" data-i18n="idealTag">Медицинские стандарты</span>
                            <h3 class="text-xl font-bold text-emerald-950 mt-0.5" data-i18n="idealTitle">Идеальный вес по 5 формулам</h3>
                        </div>
                        <div class="bg-emerald-50 px-3.5 py-2 rounded-2xl border border-emerald-200/70 text-right">
                            <div class="text-[11px] font-semibold text-emerald-700" data-i18n="idealAvgLabel">Среднее значение:</div>
                            <div class="text-lg font-extrabold text-emerald-900" id="res-ideal-avg">71.4 кг</div>
                        </div>
                    </div>

                    <div class="divide-y divide-emerald-100">
                        <!-- Брока -->
                        <div class="py-3 flex items-center justify-between gap-4">
                            <div>
                                <div class="font-bold text-sm text-emerald-950" data-i18n="fBroca">Формула Брока (уточненная)</div>
                                <div class="text-xs text-emerald-600" data-i18n="fBrocaDesc">Учитывает пол, возраст и тип телосложения</div>
                            </div>
                            <div class="font-extrabold text-base text-emerald-800 shrink-0" id="res-ideal-broca">70.2 кг</div>
                        </div>

                        <!-- Лоренца -->
                        <div class="py-3 flex items-center justify-between gap-4">
                            <div>
                                <div class="font-bold text-sm text-emerald-950" data-i18n="fLorentz">Формула Лоренца</div>
                                <div class="text-xs text-emerald-600" data-i18n="fLorentzDesc">Классическая европейская формула по росту</div>
                            </div>
                            <div class="font-extrabold text-base text-emerald-800 shrink-0" id="res-ideal-lorentz">71.0 кг</div>
                        </div>

                        <!-- Девина -->
                        <div class="py-3 flex items-center justify-between gap-4">
                            <div>
                                <div class="font-bold text-sm text-emerald-950" data-i18n="fDevine">Формула Девина (Devine)</div>
                                <div class="text-xs text-emerald-600" data-i18n="fDevineDesc">Применяется в клинической медицине</div>
                            </div>
                            <div class="font-extrabold text-base text-emerald-800 shrink-0" id="res-ideal-devine">73.1 кг</div>
                        </div>

                        <!-- Робинсона -->
                        <div class="py-3 flex items-center justify-between gap-4">
                            <div>
                                <div class="font-bold text-sm text-emerald-950" data-i18n="fRobinson">Формула Робинсона (Robinson)</div>
                                <div class="text-xs text-emerald-600" data-i18n="fRobinsonDesc">Модификация формулы Девина (1983 г.)</div>
                            </div>
                            <div class="font-extrabold text-base text-emerald-800 shrink-0" id="res-ideal-robinson">71.2 кг</div>
                        </div>

                        <!-- Миллера -->
                        <div class="py-3 flex items-center justify-between gap-4">
                            <div>
                                <div class="font-bold text-sm text-emerald-950" data-i18n="fMiller">Формула Миллера (Miller)</div>
                                <div class="text-xs text-emerald-600" data-i18n="fMillerDesc">Современная статистическая модель</div>
                            </div>
                            <div class="font-extrabold text-base text-emerald-800 shrink-0" id="res-ideal-miller">71.5 кг</div>
                        </div>
                    </div>
                </div>

            </section>
        </div>
    </div>

        
        <!-- Вкладка 1: Анализатор рецептов -->
        <div id="page-recipe" class="page space-y-6">
            <div class="bg-white rounded-3xl p-5 sm:p-7 card-shadow border border-emerald-100/80">
                <div class="flex flex-wrap items-center justify-between gap-2 mb-4">
                    <h2 class="text-lg font-bold text-emerald-950">Добавить ингредиент в блюдо</h2>
                    <button class="py-2 px-3.5 bg-emerald-50 hover:bg-emerald-100 text-emerald-800 rounded-xl text-xs font-bold transition border border-emerald-200 cursor-pointer" onclick="openModal()">➕ Свой продукт / блюдо</button>
                </div>
                <div class="flex flex-col sm:flex-row gap-3 relative">
                    <div class="relative flex-1">
                        <input type="text" id="recipeInput" placeholder="Начните ввод (например: говядина, гречка, творог, борщ)..." autocomplete="off"
                            class="w-full px-4 py-3 rounded-xl border border-emerald-200 bg-emerald-50/30 text-emerald-950 font-medium text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500">
                        <div id="recipeSuggestions" class="absolute top-full left-0 right-0 bg-white border border-emerald-200 rounded-xl mt-1 max-h-60 overflow-y-auto z-50 shadow-xl hidden"></div>
                    </div>
                    <input type="text" id="recipeAmount" class="w-full sm:w-40 px-4 py-3 rounded-xl border border-emerald-200 bg-emerald-50/30 text-emerald-950 font-medium text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500" placeholder="Вес (150г, 2шт)">
                    <button id="addRecipeBtn" class="py-3 px-6 bg-emerald-600 hover:bg-emerald-500 text-white font-bold text-sm rounded-xl shadow transition cursor-pointer">Добавить</button>
                </div>
                <p class="text-xs text-emerald-700/80 mt-2">💡 Точный расчет БЖУ и калорийности на 100г готового блюда с учетом уварки/воды.</p>
            </div>

            <div class="bg-white rounded-3xl p-5 sm:p-7 card-shadow border border-emerald-100/80">
                <div class="flex items-center justify-between mb-4">
                    <h3 class="text-base font-bold text-emerald-950">Состав блюда / рецепта</h3>
                    <button onclick="clearRecipe()" class="text-rose-600 hover:text-rose-700 text-xs font-bold cursor-pointer">Очистить рецепт</button>
                </div>

                <div class="overflow-x-auto">
                    <table id="recipeTable" class="w-full text-left text-sm hidden">
                        <thead>
                            <tr class="text-emerald-700 font-semibold text-xs uppercase border-b border-emerald-100 bg-emerald-50/50">
                                <th class="p-3">Продукт</th>
                                <th class="p-3">Вес</th>
                                <th class="p-3">Ккал</th>
                                <th class="p-3">Белки</th>
                                <th class="p-3">Жиры</th>
                                <th class="p-3">Углеводы</th>
                                <th class="p-3 text-right">Действие</th>
                            </tr>
                        </thead>
                        <tbody id="recipeTableBody" class="divide-y divide-emerald-50"></tbody>
                    </table>
                </div>
                <div id="emptyRecipe" class="text-center py-12 text-emerald-700/60 text-sm">Рецепт пуст. Добавьте ингредиенты выше.</div>

                <div id="recipeSummary" class="mt-6 p-4 rounded-2xl bg-emerald-50/80 border border-emerald-200/70 flex flex-wrap justify-between items-center gap-4 hidden">
                    <div>
                        <div class="font-bold text-xs text-emerald-900 mb-1.5">Итого на 100 граммов готового блюда:</div>
                        <div class="flex flex-wrap gap-4 text-xs font-medium text-emerald-950">
                            <div>Ккал: <strong id="resCal" class="text-emerald-600 font-bold">0</strong></div>
                            <div>Белки: <strong id="resP">0 г</strong></div>
                            <div>Жиры: <strong id="resF">0 г</strong></div>
                            <div>Углеводы: <strong id="resC">0 г</strong></div>
                            <div>Общий вес: <strong id="resWeight">0 г</strong></div>
                        </div>
                    </div>
                    <input type="text" id="dishName" placeholder="Название блюда" class="px-3 py-2.5 rounded-xl border border-emerald-200 text-xs w-44 focus:outline-none focus:ring-2 focus:ring-emerald-500"><button class="py-2.5 px-5 bg-teal-600 hover:bg-teal-500 text-white font-bold text-xs rounded-xl shadow transition cursor-pointer" onclick="saveAsDish()">💾 Сохранить блюдо в базу</button>
                </div>
            </div>
        </div>

        <!-- Вкладка 2: Дневник -->
        <div id="page-diary" class="page space-y-6">
            <div class="bg-white rounded-3xl p-5 sm:p-7 card-shadow border border-emerald-100/80">
                <h2 class="text-lg font-bold text-emerald-950 mb-4">Запись приема пищи</h2>
                <div class="grid grid-cols-1 md:grid-cols-12 gap-3">
                    <div class="md:col-span-3">
                        <select id="mealTime" class="w-full px-4 py-3 rounded-xl border border-emerald-200 bg-emerald-50/30 text-emerald-950 font-medium text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500">
                            <option value="Завтрак">🌅 Завтрак</option>
                            <option value="Обед">🍲 Обед</option>
                            <option value="Ужин">🌙 Ужин</option>
                            <option value="Перекус">🍎 Перекус</option>
                        </select>
                    </div>
                    <div class="md:col-span-6 relative">
                        <input type="text" id="diaryInput" placeholder="Поиск продукта или блюда..." autocomplete="off"
                            class="w-full px-4 py-3 rounded-xl border border-emerald-200 bg-emerald-50/30 text-emerald-950 font-medium text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500">
                        <div id="diarySuggestions" class="absolute top-full left-0 right-0 bg-white border border-emerald-200 rounded-xl mt-1 max-h-60 overflow-y-auto z-50 shadow-xl hidden"></div>
                    </div>
                    <div class="md:col-span-3 flex gap-2">
                        <input type="text" id="diaryAmount" placeholder="Вес (г)" class="w-full px-4 py-3 rounded-xl border border-emerald-200 bg-emerald-50/30 text-emerald-950 font-medium text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500">
                        <button id="addDiaryBtn" class="py-3 px-5 bg-emerald-600 hover:bg-emerald-500 text-white font-bold text-sm rounded-xl shadow transition whitespace-nowrap cursor-pointer">Записать</button>
                    </div>
                </div>
            </div>

            <div class="bg-white rounded-3xl p-5 sm:p-7 card-shadow border border-emerald-100/80">
                <h3 class="text-base font-bold text-emerald-950 mb-4">Съедено за сегодня</h3>
                <div class="overflow-x-auto">
                    <table id="diaryTable" class="w-full text-left text-sm hidden">
                        <thead>
                            <tr class="text-emerald-700 font-semibold text-xs uppercase border-b border-emerald-100 bg-emerald-50/50">
                                <th class="p-3">Прием</th>
                                <th class="p-3">Продукт</th>
                                <th class="p-3">Вес</th>
                                <th class="p-3">Ккал</th>
                                <th class="p-3">Б / Ж / В</th>
                                <th class="p-3 text-right">Действие</th>
                            </tr>
                        </thead>
                        <tbody id="diaryTableBody" class="divide-y divide-emerald-50"></tbody>
                    </table>
                </div>
                <div id="emptyDiary" class="text-center py-12 text-emerald-700/60 text-sm">Дневник за сегодня пуст.</div>

                <div id="diarySummary" class="mt-6 p-4 rounded-2xl bg-emerald-50/80 border border-emerald-200/70 flex flex-wrap justify-between items-center gap-4 hidden">
                    <div class="flex flex-wrap gap-6 text-xs font-medium text-emerald-950">
                        <div>Всего Ккал: <strong id="dayCal" class="text-emerald-600 font-bold text-base">0</strong></div>
                        <div>Белки: <strong id="dayP">0 г</strong></div>
                        <div>Жиры: <strong id="dayF">0 г</strong></div>
                        <div>Углеводы: <strong id="dayC">0 г</strong></div>
                    </div>
                    <button class="py-2 px-4 bg-emerald-100 hover:bg-emerald-200 text-emerald-900 font-bold text-xs rounded-xl transition cursor-pointer" onclick="copyDiaryReport()">📋 Копировать отчет</button>
                </div>
            </div>
        </div>

        <!-- Вкладка 3: Каталог продуктов -->
        <div id="page-catalog" class="page space-y-6">
            <div class="bg-white rounded-3xl p-5 sm:p-7 card-shadow border border-emerald-100/80">
                <div class="flex flex-wrap items-center justify-between gap-3 mb-5">
                    <h2 class="text-lg font-bold text-emerald-950">Каталог продуктов и блюд</h2>
                    <input type="text" id="catalogSearch" placeholder="Поиск в базе..." 
                        class="w-full sm:w-72 px-4 py-2.5 rounded-xl border border-emerald-200 bg-emerald-50/30 text-emerald-950 text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500">
                </div>
                <div class="mb-5 p-4 rounded-2xl bg-emerald-50/70 border border-emerald-200/70">
                    <div class="text-sm font-bold text-emerald-950 mb-1">Массовый импорт продуктов</div>
                    <p class="text-xs text-emerald-800/80 mb-2">Вставьте строки в формате: название;ккал;белки;жиры;углеводы (разделитель ; или Tab — можно копировать прямо из таблиц с сайтов). Дубли пропускаются.</p>
                    <textarea id="importText" rows="4" class="w-full px-3 py-2 rounded-xl border border-emerald-200 text-xs font-mono focus:outline-none focus:ring-2 focus:ring-emerald-500" placeholder="Борщ;49;3,0;2,2;4,5"></textarea>
                    <div class="flex flex-wrap gap-2 mt-2">
                        <button onclick="importProducts()" class="px-4 py-2 bg-emerald-600 hover:bg-emerald-500 text-white font-bold text-xs rounded-xl cursor-pointer">Импортировать</button>
                        <button onclick="exportProducts()" class="px-4 py-2 bg-white hover:bg-emerald-100 text-emerald-900 font-bold text-xs rounded-xl border border-emerald-200 cursor-pointer">Выгрузить всю базу</button>
                    </div>
                </div>
                <div id="catalogCount" class="text-xs text-emerald-700 mb-2"></div>
                <div class="overflow-x-auto max-h-[600px]">
                    <table class="w-full text-left text-sm">
                        <thead class="sticky top-0 bg-emerald-50 text-emerald-800 uppercase text-xs">
                            <tr>
                                <th class="p-3">Продукт / Блюдо (на 100г)</th>
                                <th class="p-3">Ккал</th>
                                <th class="p-3">Белки</th>
                                <th class="p-3">Жиры</th>
                                <th class="p-3">Углеводы</th>
                            </tr>
                        </thead>
                        <tbody id="catalogTableBody" class="divide-y divide-emerald-50"></tbody>
                    </table>
                </div>
                <div class="text-center mt-4"><button id="catMoreBtn" onclick="catMore()" class="px-5 py-2 bg-emerald-100 hover:bg-emerald-200 text-emerald-900 font-bold text-xs rounded-xl cursor-pointer">Показать ещё</button></div>
            </div>
        </div>

    
</main>
<!-- Модальное окно своего продукта -->
    <div id="customModal" class="fixed inset-0 bg-black/50 backdrop-blur-xs hidden items-center justify-center z-50 p-4">
        <div class="bg-white rounded-3xl p-6 sm:p-8 max-w-md w-full shadow-2xl space-y-4">
            <h3 class="text-lg font-bold text-emerald-950">Добавить свой продукт</h3>
            <div>
                <label class="block text-xs font-semibold text-emerald-900 mb-1">Название продукта или блюда:</label>
                <input type="text" id="customName" placeholder="Например: Салат фирменный" class="w-full px-3.5 py-2.5 rounded-xl border border-emerald-200 text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500">
            </div>
            <div class="grid grid-cols-2 gap-3">
                <div>
                    <label class="block text-xs font-semibold text-emerald-900 mb-1">Калории (на 100г):</label>
                    <input type="number" id="customKcal" placeholder="150" class="w-full px-3.5 py-2.5 rounded-xl border border-emerald-200 text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500">
                </div>
                <div>
                    <label class="block text-xs font-semibold text-emerald-900 mb-1">Белки (г):</label>
                    <input type="number" id="customP" placeholder="10" class="w-full px-3.5 py-2.5 rounded-xl border border-emerald-200 text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500">
                </div>
                <div>
                    <label class="block text-xs font-semibold text-emerald-900 mb-1">Жиры (г):</label>
                    <input type="number" id="customF" placeholder="5" class="w-full px-3.5 py-2.5 rounded-xl border border-emerald-200 text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500">
                </div>
                <div>
                    <label class="block text-xs font-semibold text-emerald-900 mb-1">Углеводы (г):</label>
                    <input type="number" id="customC" placeholder="20" class="w-full px-3.5 py-2.5 rounded-xl border border-emerald-200 text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500">
                </div>
            </div>
            <div class="flex gap-3 justify-end pt-2">
                <button class="px-4 py-2 bg-slate-100 hover:bg-slate-200 text-slate-700 font-bold text-xs rounded-xl cursor-pointer" onclick="closeModal()">Отмена</button>
                <button class="px-5 py-2 bg-emerald-600 hover:bg-emerald-500 text-white font-bold text-xs rounded-xl cursor-pointer" onclick="saveCustomProduct()">Сохранить</button>
            </div>
        </div>
    </div>

    
<footer class="bg-white border-t border-emerald-100 mt-12 py-6"><div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-xs text-emerald-700/80 text-center">BodyAnalyzer © 2026. Результаты носят информационный характер и не заменяют консультацию врача. Данные о калорийности — справочные, усреднённые.</div></footer>
<script>

        // --- СЛОВАРЬ ПЕРЕВОДОВ (RU / UA / EN) ---
        const i18n = {
            ru: {
                headerSubtitle: "Комплексный медицинский и фитнес-анализ",
                badgeText: "Научные формулы ВОЗ, Миффлина-Сан Жеора и US Navy",
                heroTitle: "Узнайте точные показатели вашего тела",
                heroDesc: "Рассчитайте индекс массы тела, идеальный вес по 5 методикам, базовый метаболизм, процент жира, сухую мышечную массу и индивидуальную норму КБЖУ и воды.",
                formTitle: "Ваши параметры",
                unitMetric: "см / кг",
                unitImperial: "ft / lbs",
                labelGender: "Пол",
                genderMale: "Мужской",
                genderFemale: "Женский",
                labelAge: "Возраст",
                unitYears: "лет",
                labelHeight: "Рост",
                unitCm: "см",
                unitIn: "in",
                labelWeight: "Вес",
                unitKg: "кг",
                unitLbs: "lbs",
                labelActivity: "Уровень физической активности",
                act1: "1.2 — Минимальный (сидячая работа)",
                act2: "1.375 — Легкий (тренировки 1–3 раза в неделю)",
                act3: "1.55 — Средний (тренировки 3–5 раз в неделю)",
                act4: "1.725 — Высокий (интенсивные 6–7 раз в неделю)",
                act5: "1.9 — Экстремальный (тяжелый труд / 2 тренировки в день)",
                actDesc1: "Отсутствие регулярных тренировок, сидячий образ жизни, минимальная бытовая активность.",
                actDesc2: "Легкие физические упражнения или спорт 1–3 раза в неделю, регулярные пешие прогулки.",
                actDesc3: "Умеренные тренировки средней интенсивности 3–5 раз в неделю или активная работа.",
                actDesc4: "Интенсивные силовые или кардио-тренировки 6–7 раз в неделю.",
                actDesc5: "Профессиональный спорт, тренировки дважды в день или тяжелый физический труд.",
                measurementsTitle: "Обхваты тела (для анализа состава)",
                measurementsSub: "Необходимы для расчета % жира и типа телосложения",
                labelNeck: "Шея",
                labelWaist: "Талия",
                labelHips: "Бедра",
                labelWrist: "Запястье",
                btnCalculate: "Рассчитать показатели",
                btnDemo: "Демо-данные",
                btnReset: "Сбросить",
                bmiTag: "Индекс массы тела (ВОЗ)",
                bmiTitle: "Оценка соответствия веса и роста",
                youMarker: "Вы",
                healthyWeightRangeLabel: "Здоровый диапазон веса для вашего роста:",
                bmiCat1: "Выраженный дефицит массы",
                bmiCat2: "Недостаточная масса тела",
                bmiCat3: "Нормальная масса тела",
                bmiCat4: "Избыточная масса (предожирение)",
                bmiCat5: "Ожирение I степени",
                bmiCat6: "Ожирение II степени",
                bmiCat7: "Ожирение III степени",
                energyTag: "Энергетический обмен",
                energyTitle: "Базовый метаболизм (BMR) и норма калорий",
                bmrMifflinName: "Миффлина — Сан-Жеора",
                goldStandard: "Рекомендуемая",
                unitKcal: "ккал/день",
                bmrDesc: "Расход энергии в состоянии полного покоя",
                bmrHarrisName: "Харриса — Бенедикта",
                classicFormula: "Классическая",
                bmrHarrisSub: "Пересмотренная формула Роза и Шизгала",
                goalSelectTitle: "Выберите вашу цель (пересчет калорий и БЖУ):",
                goalLose: "Похудение",
                goalMaintain: "Поддержание",
                goalGain: "Набор массы",
                goalLabelLose: "Суточная норма для плавного похудения (-18%)",
                goalLabelMaintain: "Суточная норма для поддержания веса (TDEE)",
                goalLabelGain: "Суточная норма для набора мышечной массы (+15%)",
                tdeeMaintainShort: "Поддержание:",
                tdeeLoseShort: "Похудение:",
                tdeeGainShort: "Набор массы:",
                macroProtein: "Белки",
                macroFat: "Жиры",
                macroCarb: "Углеводы",
                unitG: "г",
                bodyCompTag: "Метод ВМС США (US Navy)",
                bodyCompTitle: "Процент жира и мышечная масса",
                leanMassLabel: "Сухая масса (LBM):",
                fatMassLabel: "Жировая масса:",
                bfInvalidMsg: "Укажите корректные обхваты шеи, талии (и бедер для женщин), чтобы рассчитать точный процент жира.",
                bfCatEssential: "Необходимый минимум",
                bfCatAthlete: "Атлетическая форма",
                bfCatFitness: "Фитнес-форма",
                bfCatAverage: "Средний уровень",
                bfCatObese: "Избыточный процент жира",
                whrLabel: "Индекс талия/бедра (WHR):",
                whrNorm: "Норма (низкий риск)",
                whrWarn: "Умеренный риск",
                whrHigh: "Повышенный риск",
                somatotypeTag: "Индекс Соловьева",
                somatotypeTitle: "Тип телосложения",
                somaAsthenic: "Астеник (Эктоморф)",
                somaAsthenicDesc: "Тонкая кость, быстрый метаболизм",
                somaNormo: "Нормостеник (Мезоморф)",
                somaNormoDesc: "Средняя кость, пропорциональное сложение",
                somaHyper: "Гиперстеник (Эндоморф)",
                somaHyperDesc: "Широкая кость, склонность к набору массы",
                waterTag: "Водный баланс",
                waterTitle: "Суточная норма воды",
                unitL: "л",
                unitMl: "мл",
                waterDesc: "Рассчитано с учетом вашего веса и выбранного уровня физической активности.",
                idealTag: "Медицинские стандарты",
                idealTitle: "Идеальный вес по 5 формулам",
                idealAvgLabel: "Среднее значение:",
                fBroca: "Формула Брока (уточненная)",
                fBrocaDesc: "Учитывает пол, возраст и тип телосложения",
                fLorentz: "Формула Лоренца",
                fLorentzDesc: "Классическая европейская формула по росту",
                fDevine: "Формула Девина (Devine)",
                fDevineDesc: "Применяется в клинической медицине",
                fRobinson: "Формула Робинсона (Robinson)",
                fRobinsonDesc: "Модификация формулы Девина (1983 г.)",
                fMiller: "Формула Миллера (Miller)",
                fMillerDesc: "Современная статистическая модель",
                footerDisclaimer: "Результаты носят информационный характер. Перед началом диеты или интенсивных тренировок проконсультируйтесь со специалистом.",
                toastCalculated: "Все показатели успешно пересчитаны!",
                toastDemo: "Загружены демонстрационные данные",
                toastReset: "Параметры сброшены к стандартным",
                toastInvalid: "Пожалуйста, проверьте корректность роста, веса и возраста"
            },
            ua: {
                headerSubtitle: "Комплексний медичний та фітнес-аналіз",
                badgeText: "Наукові формули ВООЗ, Міффліна-Сан Жеора та US Navy",
                heroTitle: "Дізнайтеся точні показники вашого тіла",
                heroDesc: "Розрахуйте індекс маси тіла, ідеальну вагу за 5 методиками, базовий метаболізм, відсоток жиру, суху м'язову масу та індивідуальну норму КБЖВ і води.",
                formTitle: "Ваші параметри",
                unitMetric: "см / кг",
                unitImperial: "ft / lbs",
                labelGender: "Стать",
                genderMale: "Чоловіча",
                genderFemale: "Жіноча",
                labelAge: "Вік",
                unitYears: "років",
                labelHeight: "Зріст",
                unitCm: "см",
                unitIn: "in",
                labelWeight: "Вага",
                unitKg: "кг",
                unitLbs: "lbs",
                labelActivity: "Рівень фізичної активності",
                act1: "1.2 — Мінімальний (сидяча робота)",
                act2: "1.375 — Легкий (тренування 1–3 рази на тиждень)",
                act3: "1.55 — Середній (тренування 3–5 разів на тиждень)",
                act4: "1.725 — Високий (інтенсивні 6–7 разів на тиждень)",
                act5: "1.9 — Екстремальний (важка праця / 2 тренування на день)",
                actDesc1: "Відсутність регулярних тренувань, сидячий спосіб життя, мінімальна побутова активність.",
                actDesc2: "Легкі фізичні вправи або спорт 1–3 рази на тиждень, регулярні піші прогулянки.",
                actDesc3: "Помірні тренування середньої інтенсивності 3–5 разів на тиждень або активна робота.",
                actDesc4: "Інтенсивні силові або кардіо-тренування 6–7 разів на тиждень.",
                actDesc5: "Професійний спорт, тренування двічі на день або важка фізична праця.",
                measurementsTitle: "Обхвати тіла (для аналізу складу)",
                measurementsSub: "Необхідні для розрахунку % жиру та типу статури",
                labelNeck: "Шия",
                labelWaist: "Талія",
                labelHips: "Стегна",
                labelWrist: "Зап'ястя",
                btnCalculate: "Розрахувати показники",
                btnDemo: "Демо-дані",
                btnReset: "Скинути",
                bmiTag: "Індекс маси тіла (ВООЗ)",
                bmiTitle: "Оцінка відповідності ваги та зросту",
                youMarker: "Ви",
                healthyWeightRangeLabel: "Здоровий діапазон ваги для вашого зросту:",
                bmiCat1: "Виражений дефіцит маси",
                bmiCat2: "Недостатня маса тіла",
                bmiCat3: "Нормальна маса тіла",
                bmiCat4: "Надлишкова маса (передожиріння)",
                bmiCat5: "Ожиріння I ступеня",
                bmiCat6: "Ожиріння II ступеня",
                bmiCat7: "Ожиріння III ступеня",
                energyTag: "Енергетичний обмін",
                energyTitle: "Базовий метаболізм (BMR) і норма калорій",
                bmrMifflinName: "Міффліна — Сан-Жеора",
                goldStandard: "Рекомендована",
                unitKcal: "ккал/день",
                bmrDesc: "Витрата енергії у стані повного спокою",
                bmrHarrisName: "Харріса — Бенедикта",
                classicFormula: "Класична",
                bmrHarrisSub: "Переглянута формула Роза та Шізгала",
                goalSelectTitle: "Оберіть вашу мету (перерахунок калорій і БЖВ):",
                goalLose: "Схуднення",
                goalMaintain: "Підтримка",
                goalGain: "Набір маси",
                goalLabelLose: "Добова норма для плавного схуднення (-18%)",
                goalLabelMaintain: "Добова норма для підтримки ваги (TDEE)",
                goalLabelGain: "Добова норма для набору м'язової маси (+15%)",
                tdeeMaintainShort: "Підтримка:",
                tdeeLoseShort: "Схуднення:",
                tdeeGainShort: "Набір маси:",
                macroProtein: "Білки",
                macroFat: "Жири",
                macroCarb: "Вуглеводи",
                unitG: "г",
                bodyCompTag: "Метод ВМС США (US Navy)",
                bodyCompTitle: "Відсоток жиру та м'язова маса",
                leanMassLabel: "Суха маса (LBM):",
                fatMassLabel: "Жирова маса:",
                bfInvalidMsg: "Вкажіть коректні обхвати шиї, талії (та стегон для жінок), щоб розрахувати точний відсоток жиру.",
                bfCatEssential: "Необхідний мінімум",
                bfCatAthlete: "Атлетична форма",
                bfCatFitness: "Фітнес-форма",
                bfCatAverage: "Середній рівень",
                bfCatObese: "Надлишковий відсоток жиру",
                whrLabel: "Індекс талія/стегна (WHR):",
                whrNorm: "Норма (низький ризик)",
                whrWarn: "Помірний ризик",
                whrHigh: "Підвищений ризик",
                somatotypeTag: "Індекс Соловйова",
                somatotypeTitle: "Тип статури",
                somaAsthenic: "Астенік (Ектоморф)",
                somaAsthenicDesc: "Тонка кістка, швидкий метаболізм",
                somaNormo: "Нормостенік (Мезоморф)",
                somaNormoDesc: "Середня кістка, пропорційна статура",
                somaHyper: "Гіперстенік (Ендоморф)",
                somaHyperDesc: "Широка кістка, схильність до набору маси",
                waterTag: "Водний баланс",
                waterTitle: "Добова норма води",
                unitL: "л",
                unitMl: "мл",
                waterDesc: "Розраховано з урахуванням вашої ваги та обраного рівня фізичної активності.",
                idealTag: "Медичні стандарти",
                idealTitle: "Ідеальна вага за 5 формулами",
                idealAvgLabel: "Середнє значення:",
                fBroca: "Формула Брока (уточнена)",
                fBrocaDesc: "Враховує стать, вік та тип статури",
                fLorentz: "Формула Лоренца",
                fLorentzDesc: "Класична європейська формула за зростом",
                fDevine: "Формула Девіна (Devine)",
                fDevineDesc: "Застосовується у клінічній медицині",
                fRobinson: "Формула Робінсона (Robinson)",
                fRobinsonDesc: "Модифікація формули Девіна (1983 р.)",
                fMiller: "Формула Міллера (Miller)",
                fMillerDesc: "Сучасна статистична модель",
                footerDisclaimer: "Результати мають інформаційний характер. Перед початком дієти або інтенсивних тренувань проконсультуйтеся зі спеціалістом.",
                toastCalculated: "Усі показники успішно перераховано!",
                toastDemo: "Завантажено демонстраційні дані",
                toastReset: "Параметри скинуто до стандартних",
                toastInvalid: "Будь ласка, перевірте коректність зросту, ваги та віку"
            },
            en: {
                headerSubtitle: "Comprehensive Medical & Fitness Body Analysis",
                badgeText: "WHO, Mifflin-St Jeor & US Navy Scientific Formulas",
                heroTitle: "Discover Your Exact Body Metrics",
                heroDesc: "Calculate your Body Mass Index, ideal weight across 5 formulas, basal metabolic rate, body fat percentage, lean mass, and tailored macros & water intake.",
                formTitle: "Your Parameters",
                unitMetric: "cm / kg",
                unitImperial: "ft / lbs",
                labelGender: "Gender",
                genderMale: "Male",
                genderFemale: "Female",
                labelAge: "Age",
                unitYears: "yrs",
                labelHeight: "Height",
                unitCm: "cm",
                unitIn: "in",
                labelWeight: "Weight",
                unitKg: "kg",
                unitLbs: "lbs",
                labelActivity: "Physical Activity Level",
                act1: "1.2 — Sedentary (office job, little exercise)",
                act2: "1.375 — Light (exercise 1–3 times/week)",
                act3: "1.55 — Moderate (exercise 3–5 times/week)",
                act4: "1.725 — Active (intense exercise 6–7 times/week)",
                act5: "1.9 — Very Active (physical job / 2x training)",
                actDesc1: "Little to no regular exercise, desk job, minimal daily movement.",
                actDesc2: "Light exercise or sports 1–3 days a week, regular walking.",
                actDesc3: "Moderate intensity workouts 3–5 days a week or active daily routine.",
                actDesc4: "Hard exercise or sports 6–7 days a week.",
                actDesc5: "Professional athlete, twice-a-day training, or heavy physical labor.",
                measurementsTitle: "Body Circumferences (Composition)",
                measurementsSub: "Required for Body Fat % and Somatotype calculation",
                labelNeck: "Neck",
                labelWaist: "Waist",
                labelHips: "Hips",
                labelWrist: "Wrist",
                btnCalculate: "Calculate Metrics",
                btnDemo: "Demo Data",
                btnReset: "Reset",
                bmiTag: "Body Mass Index (WHO)",
                bmiTitle: "Weight-to-Height Assessment",
                youMarker: "You",
                healthyWeightRangeLabel: "Healthy weight range for your height:",
                bmiCat1: "Severe Thinness",
                bmiCat2: "Underweight",
                bmiCat3: "Normal Weight",
                bmiCat4: "Overweight (Pre-obese)",
                bmiCat5: "Obesity Class I",
                bmiCat6: "Obesity Class II",
                bmiCat7: "Obesity Class III",
                energyTag: "Energy Expenditure",
                energyTitle: "Basal Metabolic Rate (BMR) & Calories",
                bmrMifflinName: "Mifflin — St Jeor",
                goldStandard: "Recommended",
                unitKcal: "kcal/day",
                bmrDesc: "Calories burned at complete rest",
                bmrHarrisName: "Harris — Benedict",
                classicFormula: "Classic",
                bmrHarrisSub: "Revised equation by Roza & Shizgal",
                goalSelectTitle: "Select your goal (updates calories & macros):",
                goalLose: "Weight Loss",
                goalMaintain: "Maintain",
                goalGain: "Muscle Gain",
                goalLabelLose: "Daily calorie target for steady fat loss (-18%)",
                goalLabelMaintain: "Daily calorie target for maintenance (TDEE)",
                goalLabelGain: "Daily calorie target for muscle gain (+15%)",
                tdeeMaintainShort: "Maintain:",
                tdeeLoseShort: "Fat Loss:",
                tdeeGainShort: "Muscle Gain:",
                macroProtein: "Protein",
                macroFat: "Fats",
                macroCarb: "Carbs",
                unitG: "g",
                bodyCompTag: "US Navy Method",
                bodyCompTitle: "Body Fat % & Lean Mass",
                leanMassLabel: "Lean Body Mass (LBM):",
                fatMassLabel: "Fat Mass:",
                bfInvalidMsg: "Please enter valid neck, waist (and hip for females) measurements to calculate body fat percentage.",
                bfCatEssential: "Essential Fat",
                bfCatAthlete: "Athletes",
                bfCatFitness: "Fitness",
                bfCatAverage: "Acceptable / Average",
                bfCatObese: "Excess Body Fat",
                whrLabel: "Waist-to-Hip Ratio (WHR):",
                whrNorm: "Normal (Low Risk)",
                whrWarn: "Moderate Risk",
                whrHigh: "High Risk",
                somatotypeTag: "Soloviev Index",
                somatotypeTitle: "Body Frame / Somatotype",
                somaAsthenic: "Ectomorph (Asthenic)",
                somaAsthenicDesc: "Small bone structure, fast metabolism",
                somaNormo: "Mesomorph (Normosthenic)",
                somaNormoDesc: "Medium bone structure, balanced build",
                somaHyper: "Endomorph (Hypersthenic)",
                somaHyperDesc: "Large bone structure, higher mass retention",
                waterTag: "Hydration Balance",
                waterTitle: "Daily Water Intake",
                unitL: "L",
                unitMl: "ml",
                waterDesc: "Calculated based on your body weight and physical activity level.",
                idealTag: "Medical Standards",
                idealTitle: "Ideal Weight by 5 Formulas",
                idealAvgLabel: "Average Value:",
                fBroca: "Broca Formula (Adjusted)",
                fBrocaDesc: "Accounts for gender, age, and body frame",
                fLorentz: "Lorentz Formula",
                fLorentzDesc: "Classic European height-based equation",
                fDevine: "Devine Formula",
                fDevineDesc: "Widely used in clinical medicine",
                fRobinson: "Robinson Formula",
                fRobinsonDesc: "Modification of Devine formula (1983)",
                fMiller: "Miller Formula",
                fMillerDesc: "Modern statistical regression model",
                footerDisclaimer: "Results are for informational purposes only. Consult a healthcare professional before starting any diet or intense training program.",
                toastCalculated: "All metrics successfully calculated!",
                toastDemo: "Demo profile data loaded",
                toastReset: "Parameters reset to defaults",
                toastInvalid: "Please verify height, weight, and age values"
            }
        };

        // --- СОСТОЯНИЕ ПРИЛОЖЕНИЯ ---
        let state = {
            lang: 'ru',
            unitSystem: 'metric', // 'metric' | 'imperial'
            goal: 'maintain' // 'lose' | 'maintain' | 'gain'
        };

        // Показать всплывающее уведомление
        let toastTimeout;
        function showToast(keyOrText) {
            const toast = document.getElementById('toast');
            const msgEl = document.getElementById('toast-msg');
            msgEl.textContent = i18n[state.lang][keyOrText] || keyOrText;
            
            toast.classList.remove('translate-y-24', 'opacity-0');
            clearTimeout(toastTimeout);
            toastTimeout = setTimeout(() => {
                toast.classList.add('translate-y-24', 'opacity-0');
            }, 2800);
        }

        // Переключение языка
        function setLanguage(lang) {
            state.lang = lang;
            document.documentElement.lang = lang;

            // Обновляем активную кнопку языка
            document.querySelectorAll('.lang-btn').forEach(btn => {
                btn.classList.remove('bg-emerald-600', 'text-white', 'shadow-sm');
                btn.classList.add('text-emerald-800', 'hover:bg-emerald-100');
            });
            const activeBtn = document.getElementById(`lang-${lang}`);
            activeBtn.classList.remove('text-emerald-800', 'hover:bg-emerald-100');
            activeBtn.classList.add('bg-emerald-600', 'text-white', 'shadow-sm');

            // Обновляем все текстовые узлы с data-i18n
            const dict = i18n[lang];
            if (window.calSetLang) window.calSetLang(lang);
            document.querySelectorAll('[data-i18n]').forEach(el => {
                const key = el.getAttribute('data-i18n');
                if (dict[key]) {
                    el.textContent = dict[key];
                }
            });

            // Обновляем единицы измерения в подписях и пересчитываем
            updateUnitLabels();
            updateActivityDesc();
            calculateAll(false);
        }

        // Обновление подписей единиц измерения
        function updateUnitLabels() {
            const dict = i18n[state.lang];
            const isMetric = state.unitSystem === 'metric';

            document.getElementById('weight-unit-label').textContent = isMetric ? dict.unitKg : dict.unitLbs;
            const circUnit = isMetric ? dict.unitCm : dict.unitIn;
            document.getElementById('circ-unit-badge').textContent = circUnit;
            document.querySelectorAll('.circ-unit').forEach(el => el.textContent = circUnit);
        }

        // Переключение системы единиц (Метрическая <-> Имперская) с конвертацией текущих значений
        function setUnitSystem(system) {
            if (state.unitSystem === system) return;

            const weightEl = document.getElementById('weight');
            const neckEl = document.getElementById('neck');
            const waistEl = document.getElementById('waist');
            const hipsEl = document.getElementById('hips');
            const wristEl = document.getElementById('wrist');

            if (system === 'imperial') {
                // Конвертируем см/кг -> ft/in/lbs
                const cm = parseFloat(document.getElementById('height-cm').value) || 178;
                const totalInches = cm / 2.54;
                const ft = Math.floor(totalInches / 12);
                const inches = Math.round((totalInches % 12) * 10) / 10;
                document.getElementById('height-ft').value = ft;
                document.getElementById('height-in').value = inches;

                weightEl.value = (parseFloat(weightEl.value) * 2.20462).toFixed(1);
                neckEl.value = (parseFloat(neckEl.value) / 2.54).toFixed(1);
                waistEl.value = (parseFloat(waistEl.value) / 2.54).toFixed(1);
                hipsEl.value = (parseFloat(hipsEl.value) / 2.54).toFixed(1);
                wristEl.value = (parseFloat(wristEl.value) / 2.54).toFixed(1);

                document.getElementById('height-metric-box').classList.add('hidden');
                document.getElementById('height-imperial-box').classList.remove('hidden');

                document.getElementById('unit-imperial').classList.add('bg-white', 'text-emerald-800', 'shadow-sm');
                document.getElementById('unit-imperial').classList.remove('text-emerald-700');
                document.getElementById('unit-metric').classList.remove('bg-white', 'text-emerald-800', 'shadow-sm');
                document.getElementById('unit-metric').classList.add('text-emerald-700');
            } else {
                // Конвертируем ft/in/lbs -> см/кг
                const ft = parseFloat(document.getElementById('height-ft').value) || 5;
                const inches = parseFloat(document.getElementById('height-in').value) || 10;
                const cm = ((ft * 12) + inches) * 2.54;
                document.getElementById('height-cm').value = Math.round(cm * 10) / 10;

                weightEl.value = (parseFloat(weightEl.value) / 2.20462).toFixed(1);
                neckEl.value = (parseFloat(neckEl.value) * 2.54).toFixed(1);
                waistEl.value = (parseFloat(waistEl.value) * 2.54).toFixed(1);
                hipsEl.value = (parseFloat(hipsEl.value) * 2.54).toFixed(1);
                wristEl.value = (parseFloat(wristEl.value) * 2.54).toFixed(1);

                document.getElementById('height-imperial-box').classList.add('hidden');
                document.getElementById('height-metric-box').classList.remove('hidden');

                document.getElementById('unit-metric').classList.add('bg-white', 'text-emerald-800', 'shadow-sm');
                document.getElementById('unit-metric').classList.remove('text-emerald-700');
                document.getElementById('unit-imperial').classList.remove('bg-white', 'text-emerald-800', 'shadow-sm');
                document.getElementById('unit-imperial').classList.add('text-emerald-700');
            }

            state.unitSystem = system;
            updateUnitLabels();
            calculateAll(false);
        }

        // Обновление описания уровня активности
        function updateActivityDesc() {
            const val = document.getElementById('activity').value;
            const dict = i18n[state.lang];
            const map = {
                '1.2': dict.actDesc1,
                '1.375': dict.actDesc2,
                '1.55': dict.actDesc3,
                '1.725': dict.actDesc4,
                '1.9': dict.actDesc5
            };
            document.getElementById('activity-desc').textContent = map[val] || dict.actDesc2;
        }

        // Выбор цели (Похудение / Поддержание / Набор)
        function setGoal(goal) {
            state.goal = goal;
            document.querySelectorAll('.goal-btn').forEach(btn => {
                btn.classList.remove('bg-emerald-600', 'text-white', 'shadow-sm');
                btn.classList.add('text-emerald-800', 'hover:bg-white/60');
            });
            const active = document.getElementById(`goal-${goal}`);
            active.classList.remove('text-emerald-800', 'hover:bg-white/60');
            active.classList.add('bg-emerald-600', 'text-white', 'shadow-sm');

            calculateAll(false);
        }

        // Форматирование веса в выбранную пользователем систему (кг или lbs)
        function formatWeight(kgVal) {
            const dict = i18n[state.lang];
            if (state.unitSystem === 'metric') {
                return `${kgVal.toFixed(1)} ${dict.unitKg}`;
            } else {
                return `${(kgVal * 2.20462).toFixed(1)} ${dict.unitLbs}`;
            }
        }

        // --- ГЛАВНАЯ ФУНКЦИЯ НАУЧНЫХ РАСЧЕТОВ ---
        function calculateAll(notify = false) {
            const dict = i18n[state.lang];
            const gender = document.querySelector('input[name="gender"]:checked').value;
            const age = parseFloat(document.getElementById('age').value);
            const activity = parseFloat(document.getElementById('activity').value);

            // Приводим все входные данные к метрической системе (см и кг) для формул
            let heightCm, weightKg, neckCm, waistCm, hipsCm, wristCm;

            if (state.unitSystem === 'metric') {
                heightCm = parseFloat(document.getElementById('height-cm').value);
                weightKg = parseFloat(document.getElementById('weight').value);
                neckCm = parseFloat(document.getElementById('neck').value);
                waistCm = parseFloat(document.getElementById('waist').value);
                hipsCm = parseFloat(document.getElementById('hips').value);
                wristCm = parseFloat(document.getElementById('wrist').value);
            } else {
                const ft = parseFloat(document.getElementById('height-ft').value) || 0;
                const inches = parseFloat(document.getElementById('height-in').value) || 0;
                heightCm = ((ft * 12) + inches) * 2.54;
                weightKg = parseFloat(document.getElementById('weight').value) / 2.20462;
                neckCm = parseFloat(document.getElementById('neck').value) * 2.54;
                waistCm = parseFloat(document.getElementById('waist').value) * 2.54;
                hipsCm = parseFloat(document.getElementById('hips').value) * 2.54;
                wristCm = parseFloat(document.getElementById('wrist').value) * 2.54;
            }

            // Базовая валидация
            if (!heightCm || heightCm < 90 || !weightKg || weightKg < 25 || !age || age < 10) {
                if (notify) showToast('toastInvalid');
                return;
            }

            const heightM = heightCm / 100;
            const heightInches = heightCm / 2.54;
            const inchesOver5Feet = Math.max(0, heightInches - 60);

            // 1. ИНДЕКС МАССЫ ТЕЛА (ИМТ / BMI)
            const bmi = weightKg / (heightM * heightM);
            document.getElementById('res-bmi-val').textContent = bmi.toFixed(1);

            let bmiCatText = '';
            let bmiBadgeClass = '';
            if (bmi < 16.0) {
                bmiCatText = dict.bmiCat1;
                bmiBadgeClass = 'bg-sky-100 text-sky-800';
            } else if (bmi < 18.5) {
                bmiCatText = dict.bmiCat2;
                bmiBadgeClass = 'bg-sky-100 text-sky-800';
            } else if (bmi < 25.0) {
                bmiCatText = dict.bmiCat3;
                bmiBadgeClass = 'bg-emerald-100 text-emerald-800';
            } else if (bmi < 30.0) {
                bmiCatText = dict.bmiCat4;
                bmiBadgeClass = 'bg-amber-100 text-amber-800';
            } else if (bmi < 35.0) {
                bmiCatText = dict.bmiCat5;
                bmiBadgeClass = 'bg-orange-100 text-orange-800';
            } else if (bmi < 40.0) {
                bmiCatText = dict.bmiCat6;
                bmiBadgeClass = 'bg-rose-100 text-rose-800';
            } else {
                bmiCatText = dict.bmiCat7;
                bmiBadgeClass = 'bg-rose-200 text-rose-900';
            }

            const badgeEl = document.getElementById('res-bmi-badge');
            badgeEl.textContent = bmiCatText;
            badgeEl.className = `inline-block mt-1 px-3 py-1 rounded-full text-xs font-bold ${bmiBadgeClass}`;

            // Позиция указателя на шкале ИМТ (диапазон 15..40)
            const clampedBmi = Math.min(40, Math.max(15, bmi));
            const bmiPercent = ((clampedBmi - 15) / (40 - 15)) * 100;
            document.getElementById('bmi-pointer').style.left = `${bmiPercent}%`;

            // Здоровый диапазон веса (ИМТ 18.5 - 24.9)
            const minHealthyKg = 18.5 * heightM * heightM;
            const maxHealthyKg = 24.9 * heightM * heightM;
            document.getElementById('res-healthy-range').textContent = 
                `${formatWeight(minHealthyKg).replace(/ [a-zа-яії]+$/i, '')} — ${formatWeight(maxHealthyKg)}`;

            // 2. ТИП ТЕЛОСЛОЖЕНИЯ (СОЛОВЬЕВ)
            let somaCoeff = 1.0; // Для уточненного Брока (0.9 астеник, 1.0 нормостеник, 1.1 гиперстеник)
            let somaName = dict.somaNormo;
            let somaDesc = dict.somaNormoDesc;

            if (wristCm > 0) {
                if (gender === 'male') {
                    if (wristCm < 18) { somaName = dict.somaAsthenic; somaDesc = dict.somaAsthenicDesc; somaCoeff = 0.9; }
                    else if (wristCm > 20) { somaName = dict.somaHyper; somaDesc = dict.somaHyperDesc; somaCoeff = 1.1; }
                } else {
                    if (wristCm < 15) { somaName = dict.somaAsthenic; somaDesc = dict.somaAsthenicDesc; somaCoeff = 0.9; }
                    else if (wristCm > 17) { somaName = dict.somaHyper; somaDesc = dict.somaHyperDesc; somaCoeff = 1.1; }
                }
            }
            document.getElementById('res-somatotype').textContent = somaName;
            document.getElementById('res-somatotype-desc').textContent = somaDesc;
            document.getElementById('res-wrist-display').textContent = state.unitSystem === 'metric' 
                ? `${wristCm.toFixed(1)}` 
                : `${(wristCm / 2.54).toFixed(1)}"`;

            // 3. ИДЕАЛЬНЫЙ ВЕС ПО 5 ФОРМУЛАМ
            // 3.1 Уточненная формула Брока (с учетом возраста и типа телосложения)
            let brocaBase = age < 40 ? (heightCm - 110) : (heightCm - 100);
            const idealBroca = brocaBase * somaCoeff;

            // 3.2 Формула Лоренца
            const idealLorentz = gender === 'male'
                ? (heightCm - 100) - ((heightCm - 150) / 4)
                : (heightCm - 100) - ((heightCm - 150) / 2);

            // 3.3 Формула Девина (Devine, 1974)
            const idealDevine = gender === 'male'
                ? 50.0 + 2.3 * inchesOver5Feet
                : 45.5 + 2.3 * inchesOver5Feet;

            // 3.4 Формула Робинсона (Robinson, 1983)
            const idealRobinson = gender === 'male'
                ? 52.0 + 1.9 * inchesOver5Feet
                : 49.0 + 1.7 * inchesOver5Feet;

            // 3.5 Формула Миллера (Miller, 1983)
            const idealMiller = gender === 'male'
                ? 56.2 + 1.41 * inchesOver5Feet
                : 53.1 + 1.36 * inchesOver5Feet;

            const idealAvg = (idealBroca + idealLorentz + idealDevine + idealRobinson + idealMiller) / 5;

            document.getElementById('res-ideal-broca').textContent = formatWeight(idealBroca);
            document.getElementById('res-ideal-lorentz').textContent = formatWeight(idealLorentz);
            document.getElementById('res-ideal-devine').textContent = formatWeight(idealDevine);
            document.getElementById('res-ideal-robinson').textContent = formatWeight(idealRobinson);
            document.getElementById('res-ideal-miller').textContent = formatWeight(idealMiller);
            document.getElementById('res-ideal-avg').textContent = formatWeight(idealAvg);

            // 4. БАЗОВЫЙ МЕТАБОЛИЗМ (BMR) И СУТОЧНАЯ НОРМА КАЛОРИЙ (TDEE)
            // Миффлин — Сан-Жеор
            const bmrMifflin = gender === 'male'
                ? (10 * weightKg) + (6.25 * heightCm) - (5 * age) + 5
                : (10 * weightKg) + (6.25 * heightCm) - (5 * age) - 161;

            // Пересмотренный Харрис — Бенедикт
            const bmrHarris = gender === 'male'
                ? 88.362 + (13.397 * weightKg) + (4.799 * heightCm) - (5.677 * age)
                : 447.593 + (9.247 * weightKg) + (3.098 * heightCm) - (4.330 * age);

            document.getElementById('res-bmr-mifflin').textContent = Math.round(bmrMifflin);
            document.getElementById('res-bmr-harris').textContent = Math.round(bmrHarris);

            const tdeeMaintain = Math.round(bmrMifflin * activity);
            const tdeeLose = Math.round(tdeeMaintain * 0.82); // -18%
            const tdeeGain = Math.round(tdeeMaintain * 1.15); // +15%

            document.getElementById('mini-maintain').textContent = tdeeMaintain;
            document.getElementById('mini-lose').textContent = tdeeLose;
            document.getElementById('mini-gain').textContent = tdeeGain;

            // Расчет БЖУ под выбранную цель
            let targetKcal, pPct, fPct, cPct, goalLabelText;
            if (state.goal === 'lose') {
                targetKcal = tdeeLose;
                pPct = 35; fPct = 25; cPct = 40; // Повышенный белок на дефиците
                goalLabelText = dict.goalLabelLose;
            } else if (state.goal === 'gain') {
                targetKcal = tdeeGain;
                pPct = 25; fPct = 25; cPct = 50; // Больше углеводов для энергии и роста
                goalLabelText = dict.goalLabelGain;
            } else {
                targetKcal = tdeeMaintain;
                pPct = 30; fPct = 25; cPct = 45; // Сбалансированный рацион
                goalLabelText = dict.goalLabelMaintain;
            }

            const proteinGrams = Math.round((targetKcal * (pPct / 100)) / 4);
            const fatGrams = Math.round((targetKcal * (fPct / 100)) / 9);
            const carbGrams = Math.round((targetKcal * (cPct / 100)) / 4);

            document.getElementById('res-goal-label').textContent = goalLabelText;
            document.getElementById('res-target-kcal').textContent = targetKcal;

            document.getElementById('macro-p-pct').textContent = `${pPct}%`;
            document.getElementById('macro-f-pct').textContent = `${fPct}%`;
            document.getElementById('macro-c-pct').textContent = `${cPct}%`;

            document.getElementById('macro-p-g').textContent = proteinGrams;
            document.getElementById('macro-f-g').textContent = fatGrams;
            document.getElementById('macro-c-g').textContent = carbGrams;

            document.getElementById('bar-p').style.width = `${pPct}%`;
            document.getElementById('bar-f').style.width = `${fPct}%`;
            document.getElementById('bar-c').style.width = `${cPct}%`;

            // 5. ПРОЦЕНТ ЖИРА (МЕТОД ВМС США / US NAVY METHOD)
            let bodyFatPct = null;
            if (gender === 'male' && waistCm > neckCm && heightCm > 0) {
                bodyFatPct = 495 / (1.0324 - 0.19077 * Math.log10(waistCm - neckCm) + 0.15456 * Math.log10(heightCm)) - 450;
            } else if (gender === 'female' && (waistCm + hipsCm) > neckCm && heightCm > 0) {
                bodyFatPct = 495 / (1.29579 - 0.35004 * Math.log10(waistCm + hipsCm - neckCm) + 0.22100 * Math.log10(heightCm)) - 450;
            }

            const validBox = document.getElementById('bodyfat-valid-box');
            const invalidBox = document.getElementById('bodyfat-invalid-box');

            if (bodyFatPct !== null && isFinite(bodyFatPct) && bodyFatPct >= 2 && bodyFatPct <= 65) {
                validBox.classList.remove('hidden');
                invalidBox.classList.add('hidden');

                document.getElementById('res-bf-pct').textContent = `${bodyFatPct.toFixed(1)}%`;

                // Категория процента жира
                let bfCat = '';
                if (gender === 'male') {
                    if (bodyFatPct < 6) bfCat = dict.bfCatEssential;
                    else if (bodyFatPct < 14) bfCat = dict.bfCatAthlete;
                    else if (bodyFatPct < 18) bfCat = dict.bfCatFitness;
                    else if (bodyFatPct < 25) bfCat = dict.bfCatAverage;
                    else bfCat = dict.bfCatObese;
                } else {
                    if (bodyFatPct < 14) bfCat = dict.bfCatEssential;
                    else if (bodyFatPct < 21) bfCat = dict.bfCatAthlete;
                    else if (bodyFatPct < 25) bfCat = dict.bfCatFitness;
                    else if (bodyFatPct < 32) bfCat = dict.bfCatAverage;
                    else bfCat = dict.bfCatObese;
                }
                document.getElementById('res-bf-cat').textContent = bfCat;

                const fatMassKg = weightKg * (bodyFatPct / 100);
                const leanMassKg = weightKg - fatMassKg;

                document.getElementById('res-lean-mass').textContent = formatWeight(leanMassKg);
                document.getElementById('res-fat-mass').textContent = formatWeight(fatMassKg);
                document.getElementById('bf-lean-bar').style.width = `${Math.max(10, 100 - bodyFatPct)}%`;
            } else {
                validBox.classList.add('hidden');
                invalidBox.classList.remove('hidden');
            }

            // Соотношение талия / бедра (WHR)
            if (waistCm > 0 && hipsCm > 0) {
                const whr = waistCm / hipsCm;
                let whrStatus = dict.whrNorm;
                if (gender === 'male') {
                    if (whr >= 1.0) whrStatus = dict.whrHigh;
                    else if (whr >= 0.9) whrStatus = dict.whrWarn;
                } else {
                    if (whr >= 0.85) whrStatus = dict.whrHigh;
                    else if (whr >= 0.80) whrStatus = dict.whrWarn;
                }
                document.getElementById('res-whr').textContent = `${whr.toFixed(2)} (${whrStatus})`;
            }

            // 6. СУТОЧНАЯ НОРМА ВОДЫ
            // База 30-35 мл на 1 кг веса + поправка на активность
            const actBonus = (activity - 1.2) * 650;
            const waterMl = Math.round((weightKg * 32) + actBonus);
            const waterLiters = (waterMl / 1000).toFixed(2);
            document.getElementById('res-water-liters').textContent = `${waterLiters} ${dict.unitL}`;
            document.getElementById('res-water-ml').textContent = `(${waterMl} ${dict.unitMl})`;

            if (notify) {
                showToast('toastCalculated');
            }
        }

        // Заполнение демонстрационными данными (женский фитнес-профиль)
        function fillDemoData() {
            if (state.unitSystem !== 'metric') {
                setUnitSystem('metric');
            }
            document.querySelector('input[name="gender"][value="female"]').checked = true;
            document.getElementById('age').value = 27;
            document.getElementById('height-cm').value = 168;
            document.getElementById('weight').value = 61;
            document.getElementById('activity').value = '1.55';
            document.getElementById('neck').value = 33;
            document.getElementById('waist').value = 67;
            document.getElementById('hips').value = 95;
            document.getElementById('wrist').value = 15.5;

            updateActivityDesc();
            calculateAll(false);
            showToast('toastDemo');
        }

        // Сброс формы
        function resetForm() {
            if (state.unitSystem !== 'metric') {
                setUnitSystem('metric');
            }
            document.querySelector('input[name="gender"][value="male"]').checked = true;
            document.getElementById('age').value = 30;
            document.getElementById('height-cm').value = 178;
            document.getElementById('weight').value = 76;
            document.getElementById('activity').value = '1.375';
            document.getElementById('neck').value = 38;
            document.getElementById('waist').value = 82;
            document.getElementById('hips').value = 98;
            document.getElementById('wrist').value = 17.5;

            setGoal('maintain');
            updateActivityDesc();
            calculateAll(false);
            showToast('toastReset');
        }

        // Инициализация при загрузке страницы
        window.onload = function() {
            setLanguage('ru');
            calculateAll(false);
        };
    
</script>
<script>
(function(){
 function safeLS(k){ try { return JSON.parse(localStorage.getItem(k)) || []; } catch(e){ return []; } }

        let state = { lang: 'ru' };

        // ПОЛНАЯ РЕАЛЬНАЯ БАЗА ИЗ КЛАССИЧЕСКИХ СПРАВОЧНИКОВ И КАЛОРИЗАТОРА
        let foodDatabase = [
            // Мясо и птица
            { name: "Говядина отварная", kcal: 175, p: 25.0, f: 8.0, c: 0.0 },
            { name: "Говядина тушеная", kcal: 232, p: 18.9, f: 16.8, c: 0.0 },
            { name: "Телятина отварная", kcal: 131, p: 23.9, f: 3.3, c: 0.0 },
            { name: "Свинина нежирная (мясная)", kcal: 242, p: 16.4, f: 19.4, c: 0.0 },
            { name: "Свинина жирная", kcal: 389, p: 11.7, f: 37.3, c: 0.0 },
            { name: "Свинина отбивная на косточке", kcal: 267, p: 17.5, f: 21.6, c: 0.0 },
            { name: "Баранина отварная", kcal: 206, p: 20.6, f: 13.0, c: 0.0 },
            { name: "Куриная грудка отварная", kcal: 137, p: 29.8, f: 1.8, c: 0.5 },
            { name: "Куриная грудка запеченная", kcal: 145, p: 30.2, f: 2.2, c: 0.0 },
            { name: "Куриный окорочок без кожи", kcal: 158, p: 21.5, f: 7.8, c: 0.0 },
            { name: "Куриное крыло запеченное", kcal: 210, p: 18.0, f: 15.0, c: 0.0 },
            { name: "Индейка филе запеченное", kcal: 135, p: 28.0, f: 2.0, c: 0.0 },
            { name: "Утка жареная", kcal: 342, p: 17.5, f: 30.1, c: 0.0 },
            { name: "Гусь запеченный", kcal: 389, p: 16.2, f: 35.5, c: 0.0 },
            { name: "Крольчатина тушеная", kcal: 156, p: 22.0, f: 7.5, c: 0.0 },
            { name: "Сало свиное соленое", kcal: 815, p: 1.4, f: 90.0, c: 0.0 },
            { name: "Бекон жареный", kcal: 541, p: 37.0, f: 43.0, c: 1.4 },

            // Субпродукты
            { name: "Говяжья печень отварная", kcal: 128, p: 20.2, f: 4.7, c: 1.5 },
            { name: "Куриная печень тушеная", kcal: 167, p: 23.3, f: 7.6, c: 1.2 },
            { name: "Говяжий язык отварной", kcal: 231, p: 15.9, f: 18.1, c: 0.0 },
            { name: "Сердце говяжье отварное", kcal: 96, p: 18.0, f: 2.8, c: 0.5 },

            // Колбасы и деликатесы
            { name: "Колбаса Докторская (вареная)", kcal: 257, p: 12.8, f: 22.2, c: 1.5 },
            { name: "Колбаса Сервелат", kcal: 412, p: 24.1, f: 34.8, c: 0.0 },
            { name: "Колбаса Салями сырокопченая", kcal: 568, p: 12.0, f: 57.0, c: 1.5 },
            { name: "Сосиски Молочные", kcal: 266, p: 11.0, f: 24.0, c: 1.5 },
            { name: "Сардельки свиные", kcal: 332, p: 10.1, f: 32.0, c: 1.9 },
            { name: "Ветчина свиная", kcal: 279, p: 15.6, f: 23.8, c: 1.2 },

            // Яйца
            { name: "Яйцо куриное (1 шт)", kcal: 86, p: 7.0, f: 6.3, c: 0.4, defaultGram: 55 },
            { name: "Яйцо куриное вареное вкрутую", kcal: 155, p: 12.8, f: 11.6, c: 0.7 },
            { name: "Яичный желток", kcal: 352, p: 16.0, f: 31.0, c: 1.0 },
            { name: "Яичный белок", kcal: 45, p: 11.1, f: 0.2, c: 0.7 },
            { name: "Перепелиное яйцо (1 шт)", kcal: 17, p: 1.2, f: 1.2, c: 0.1, defaultGram: 12 },

            // Рыба и морепродукты
            { name: "Лосось (семга) слабосоленый", kcal: 202, p: 20.0, f: 13.0, c: 0.0 },
            { name: "Горбуша запеченная", kcal: 166, p: 21.0, f: 8.9, c: 0.0 },
            { name: "Оселедець солоний", kcal: 216, p: 17.7, f: 15.6, c: 0.0 },
            { name: "Скумбрия запечена", kcal: 205, p: 19.0, f: 14.5, c: 0.0 },
            { name: "Минтай отварной", kcal: 79, p: 17.6, f: 0.9, c: 0.0 },
            { name: "Хек отварной", kcal: 86, p: 16.6, f: 2.2, c: 0.0 },
            { name: "Треска отварная", kcal: 78, p: 17.5, f: 0.5, c: 0.0 },
            { name: "Судак отварной", kcal: 97, p: 21.0, f: 1.1, c: 0.0 },
            { name: "Щука отварная", kcal: 98, p: 20.0, f: 1.9, c: 0.0 },
            { name: "Карп запеченный", kcal: 124, p: 18.0, f: 5.5, c: 0.0 },
            { name: "Креветки отварные", kcal: 95, p: 18.9, f: 2.2, c: 0.5 },
            { name: "Кальмары отварные", kcal: 122, p: 22.6, f: 2.9, c: 0.8 },
            { name: "Крабовые палочки", kcal: 73, p: 6.0, f: 1.5, c: 9.5 },
            { name: "Икра красная лососевая", kcal: 249, p: 31.6, f: 13.8, c: 0.0 },
            { name: "Икра черная осетровая", kcal: 203, p: 28.3, f: 9.7, c: 0.0 },
            { name: "Печень трески консервированная", kcal: 613, p: 4.2, f: 65.7, c: 1.2 },
            { name: "Шпроты в масле", kcal: 363, p: 17.0, f: 32.4, c: 0.0 },

            // Молочные продукты и сыры
            { name: "Молоко 3.2%", kcal: 58, p: 2.8, f: 3.2, c: 4.6 },
            { name: "Молоко 2.5%", kcal: 52, p: 2.8, f: 2.5, c: 4.7 },
            { name: "Молоко 1%", kcal: 42, p: 2.8, f: 1.0, c: 4.7 },
            { name: "Сливки 10%", kcal: 118, p: 3.0, f: 10.0, c: 4.0 },
            { name: "Сливки 20%", kcal: 206, p: 2.8, f: 20.0, c: 3.6 },
            { name: "Кефир 2.5%", kcal: 53, p: 2.8, f: 2.5, c: 4.0 },
            { name: "Кефир 1%", kcal: 41, p: 2.8, f: 1.0, c: 4.0 },
            { name: "Ряжанка 2.5%", kcal: 57, p: 2.9, f: 2.5, c: 4.2 },
            { name: "Йогурт натуральный 3.2%", kcal: 67, p: 4.5, f: 3.2, c: 5.2 },
            { name: "Творог 9% (домашний)", kcal: 159, p: 16.5, f: 9.0, c: 2.0 },
            { name: "Творог 5%", kcal: 121, p: 17.0, f: 5.0, c: 1.8 },
            { name: "Творог 0% (обезжиренный)", kcal: 86, p: 18.0, f: 0.2, c: 1.8 },
            { name: "Сметана 20% (базарная)", kcal: 210, p: 2.5, f: 20.0, c: 3.2 },
            { name: "Сметана 15%", kcal: 160, p: 2.6, f: 15.0, c: 3.0 },
            { name: "Сметана 10%", kcal: 115, p: 3.0, f: 10.0, c: 3.6 },
            { name: "Масло сливочное 82.5%", kcal: 748, p: 0.5, f: 82.5, c: 0.8 },
            { name: "Масло крестьянское 72.5%", kcal: 661, p: 0.8, f: 72.5, c: 1.4 },
            { name: "Сир Российский твердый", kcal: 360, p: 24.0, f: 29.0, c: 0.0 },
            { name: "Сир Голландский", kcal: 352, p: 26.0, f: 26.8, c: 0.0 },
            { name: "Сир Пармезан", kcal: 431, p: 38.0, f: 32.0, c: 0.0 },
            { name: "Сир Моцарелла", kcal: 280, p: 18.0, f: 22.0, c: 1.0 },
            { name: "Сир Сулугуни", kcal: 290, p: 20.5, f: 22.0, c: 0.0 },
            { name: "Бринза", kcal: 260, p: 18.0, f: 20.0, c: 1.5 },
            { name: "Сир плаленый Дружба", kcal: 226, p: 13.5, f: 19.0, c: 2.0 },

            // Крупы и зерновые
            { name: "Гречневая каша отварная", kcal: 103, p: 3.6, f: 0.7, c: 20.3 },
            { name: "Гречневая крупа (ядрица сухая)", kcal: 343, p: 12.6, f: 3.3, c: 62.1 },
            { name: "Рисовая каша отварная на воде", kcal: 78, p: 1.5, f: 0.2, c: 17.0 },
            { name: "Рис белый шлифованный сухой", kcal: 344, p: 6.7, f: 0.7, c: 78.9 },
            { name: "Рис бурый (коричневый) сухой", kcal: 367, p: 7.4, f: 1.8, c: 72.9 },
            { name: "Овсяная каша на воді", kcal: 88, p: 3.0, f: 1.7, c: 15.0 },
            { name: "Овсяные хлопья (сухие)", kcal: 366, p: 11.9, f: 7.2, c: 69.3 },
            { name: "Манная каша на молоке", kcal: 98, p: 3.2, f: 2.7, c: 15.2 },
            { name: "Пшенная каша отварная", kcal: 90, p: 3.0, f: 1.7, c: 16.5 },
            { name: "Перлова каша відварна", kcal: 109, p: 3.1, f: 0.4, c: 22.5 },
            { name: "Перловая крупа сухая", kcal: 320, p: 9.3, f: 1.1, c: 73.7 },
            { name: "Плетневая каша (ячневая)", kcal: 76, p: 2.3, f: 0.4, c: 16.0 },
            { name: "Кукурузная каша отварная", kcal: 78, p: 2.1, f: 1.2, c: 15.0 },
            { name: "Булгур отварной", kcal: 83, p: 3.1, f: 0.4, c: 17.5 },
            { name: "Кускус отварной", kcal: 112, p: 3.8, f: 0.2, c: 23.2 },
            { name: "Макароны отварные (из пшеницы)", kcal: 112, p: 3.8, f: 0.4, c: 23.2 },
            { name: "Макароны сухие высший сорт", kcal: 337, p: 10.4, f: 1.1, c: 69.7 },

            // Хлеб и выпечка
            { name: "Хлеб ржаной (украинский)", kcal: 210, p: 6.8, f: 1.2, c: 42.0 },
            { name: "Хлеб пшеничный из муки 1/с", kcal: 262, p: 8.1, f: 1.6, c: 50.4 },
            { name: "Батон белый", kcal: 265, p: 8.1, f: 3.2, c: 48.8 },
            { name: "Лаваш армянский", kcal: 275, p: 8.0, f: 1.0, c: 56.0 },
            { name: "Хлебцы ржаные (цельнозерновые)", kcal: 289, p: 11.2, f: 2.2, c: 57.5 },

            // Овощи и зелень
            { name: "Картофель отварной в мундире", kcal: 78, p: 2.0, f: 0.4, c: 16.6 },
            { name: "Картофельное пюре", kcal: 106, p: 2.4, f: 3.2, c: 16.5 },
            { name: "Картофель жареный", kcal: 192, p: 2.8, f: 9.6, c: 23.4 },
            { name: "Картофель фри", kcal: 312, p: 3.4, f: 15.0, c: 41.0 },
            { name: "Огурцы свежие", kcal: 15, p: 0.8, f: 0.1, c: 2.8 },
            { name: "Помидоры свежие", kcal: 18, p: 0.9, f: 0.2, c: 3.9 },
            { name: "Капуста белокочанная свежая", kcal: 27, p: 1.8, f: 0.1, c: 4.7 },
            { name: "Капуста квашеная", kcal: 19, p: 1.8, f: 0.1, c: 3.0 },
            { name: "Капуста цветная отварная", kcal: 30, p: 2.5, f: 0.3, c: 5.4 },
            { name: "Брокколи отварная", kcal: 35, p: 3.0, f: 0.4, c: 6.6 },
            { name: "Морковь свежая", kcal: 33, p: 1.3, f: 0.1, c: 6.9 },
            { name: "Свекла отварная", kcal: 49, p: 1.8, f: 0.1, c: 10.8 },
            { name: "Лук репчатый", kcal: 41, p: 1.4, f: 0.0, c: 8.2 },
            { name: "Чеснок", kcal: 143, p: 6.5, f: 0.5, c: 29.9 },
            { name: "Перец болгарский свежий", kcal: 27, p: 1.3, f: 0.1, c: 5.3 },
            { name: "Баклажаны запеченные", kcal: 50, p: 1.2, f: 2.0, c: 6.0 },
            { name: "Кабачки тушеные", kcal: 45, p: 1.0, f: 2.5, c: 4.5 },
            { name: "Тыква запеченная", kcal: 28, p: 1.0, f: 0.1, c: 6.5 },
            { name: "Редис", kcal: 20, p: 1.2, f: 0.1, c: 3.4 },
            { name: "Зеленый горошек свежий", kcal: 73, p: 5.0, f: 0.2, c: 13.3 },
            { name: "Кукуруза консервированная", kcal: 119, p: 3.9, f: 2.2, c: 22.5 },
            { name: "Фасоль белая отварная", kcal: 123, p: 7.8, f: 0.5, c: 21.5 },
            { name: "Чечевица отварная", kcal: 116, p: 9.0, f: 0.4, c: 20.0 },
            { name: "Нут отварной", kcal: 164, p: 8.9, f: 2.6, c: 27.4 },
            { name: "Шпинат свежий", kcal: 22, p: 2.9, f: 0.3, c: 2.0 },
            { name: "Петрушка, укроп (зелень)", kcal: 36, p: 3.0, f: 0.5, c: 6.3 },

            // Грибы
            { name: "Шампиньоны свежие", kcal: 27, p: 4.3, f: 1.0, c: 0.1 },
            { name: "Белые грибы свежие", kcal: 34, p: 3.7, f: 1.7, c: 1.1 },
            { name: "Вешенки свежие", kcal: 38, p: 3.3, f: 0.4, c: 5.5 },

            // Фрукты и ягоды
            { name: "Яблоко свежее", kcal: 47, p: 0.4, f: 0.4, c: 9.8, defaultGram: 150 },
            { name: "Груша свежая", kcal: 42, p: 0.4, f: 0.3, c: 10.3, defaultGram: 150 },
            { name: "Банан", kcal: 89, p: 1.5, f: 0.2, c: 21.8, defaultGram: 120 },
            { name: "Апельсин", kcal: 43, p: 0.9, f: 0.2, c: 8.1, defaultGram: 150 },
            { name: "Мандарин", kcal: 38, p: 0.8, f: 0.2, c: 7.5, defaultGram: 100 },
            { name: "Грейпфрут", kcal: 35, p: 0.7, f: 0.2, c: 6.5, defaultGram: 250 },
            { name: "Лимон", kcal: 33, p: 0.9, f: 0.1, c: 3.0 },
            { name: "Ківі", kcal: 48, p: 1.0, f: 0.6, c: 9.0 },
            { name: "Персик", kcal: 46, p: 0.9, f: 0.1, c: 11.3 },
            { name: "Абрикос", kcal: 44, p: 0.9, f: 0.1, c: 10.8 },
            { name: "Слива", kcal: 49, p: 0.8, f: 0.3, c: 9.6 },
            { name: "Вишня", kcal: 52, p: 0.8, f: 0.4, c: 11.3 },
            { name: "Черешня", kcal: 50, p: 1.1, f: 0.4, c: 10.6 },
            { name: "Полуниця (клубника)", kcal: 36, p: 0.8, f: 0.4, c: 7.5 },
            { name: "Малина", kcal: 52, p: 0.8, f: 0.5, c: 8.3 },
            { name: "Чорниця (черника)", kcal: 44, p: 1.1, f: 0.4, c: 7.6 },
            { name: "Смородина чорна", kcal: 44, p: 1.0, f: 0.4, c: 7.3 },
            { name: "Арбуз", kcal: 27, p: 0.6, f: 0.1, c: 5.8 },
            { name: "Диня", kcal: 35, p: 0.6, f: 0.3, c: 7.4 },
            { name: "Ананас", kcal: 49, p: 0.4, f: 0.1, c: 11.5 },
            { name: "Хурма", kcal: 67, p: 0.5, f: 0.4, c: 15.3 },
            { name: "Виноград", kcal: 65, p: 0.6, f: 0.2, c: 15.4 },
            { name: "Изюм", kcal: 299, p: 3.1, f: 0.5, c: 71.2 },
            { name: "Курага", kcal: 232, p: 5.2, f: 0.3, c: 51.0 },
            { name: "Чорнослив", kcal: 231, p: 2.3, f: 0.7, c: 57.5 },

            // Орехи и семечки
            { name: "Грецькі горіхи", kcal: 654, p: 16.2, f: 60.8, c: 11.1 },
            { name: "Мигдаль", kcal: 609, p: 18.6, f: 53.7, c: 13.0 },
            { name: "Фундук", kcal: 628, p: 16.1, f: 60.9, c: 9.9 },
            { name: "Кешью", kcal: 643, p: 18.5, f: 48.5, c: 22.5 },
            { name: "Арахис жареный", kcal: 626, p: 26.3, f: 45.2, c: 9.9 },
            { name: "Семена подсолнечника очищенные", kcal: 578, p: 20.7, f: 52.9, c: 5.0 },
            { name: "Семена чиа", kcal: 512, p: 16.5, f: 30.7, c: 42.1 },

            // Супы и готовые блюда
            { name: "Борщ украинский с мясом и сметаной", kcal: 78, p: 4.8, f: 4.2, c: 5.5 },
            { name: "Суп курячий с лапшой", kcal: 52, p: 4.1, f: 2.1, c: 4.6 },
            { name: "Солянка сборная мясная", kcal: 98, p: 6.5, f: 7.0, c: 3.5 },
            { name: "Щи из свежей капусты", kcal: 45, p: 2.5, f: 2.2, c: 4.0 },
            { name: "Суп-пюре грибной", kcal: 72, p: 2.2, f: 4.5, c: 6.0 },
            { name: "Вареники с картофелем", kcal: 175, p: 4.2, f: 4.0, c: 30.0 },
            { name: "Вареники с вишней", kcal: 162, p: 3.5, f: 1.5, c: 33.0 },
            { name: "Вареники с творогом", kcal: 195, p: 9.0, f: 5.0, c: 28.0 },
            { name: "Пельмени домашние отварные", kcal: 250, p: 12.0, f: 12.0, c: 24.0 },
            { name: "Голубцы с мясом и рисом", kcal: 135, p: 6.5, f: 7.5, c: 10.5 },
            { name: "Деруны со сметаной", kcal: 220, p: 3.5, f: 12.0, c: 24.0 },
            { name: "Сырники классические домашние", kcal: 230, p: 14.0, f: 11.0, c: 18.0 },
            { name: "Блинчики с мясом", kcal: 230, p: 9.5, f: 10.0, c: 25.0 },
            { name: "Плов с свининой/говядиной", kcal: 195, p: 7.5, f: 9.0, c: 20.0 },
            { name: "Отечественный салат Оливье", kcal: 198, p: 4.5, f: 15.2, c: 7.8 },
            { name: "Салат Винегрет", kcal: 125, p: 1.4, f: 9.0, c: 9.5 },
            { name: "Салат Греческий", kcal: 115, p: 3.5, f: 9.8, c: 4.2 },

            // Масла, соусы, специи и сладости
            { name: "Масло подсолнечное", kcal: 899, p: 0.0, f: 99.9, c: 0.0 },
            { name: "Масло оливковое", kcal: 898, p: 0.0, f: 99.8, c: 0.0 },
            { name: "Майонез 67%", kcal: 624, p: 3.3, f: 67.0, c: 2.4 },
            { name: "Кетчуп", kcal: 93, p: 1.8, f: 0.1, c: 22.4 },
            { name: "Соус Соевый", kcal: 53, p: 8.1, f: 0.0, c: 4.9 },
            { name: "Мед пчелиный", kcal: 320, p: 0.8, f: 0.0, c: 80.3 },
            { name: "Сахар белый песок", kcal: 398, p: 0.0, f: 0.0, c: 99.8 },
            { name: "Шоколад черный (темный)", kcal: 539, p: 6.5, f: 35.4, c: 48.2 },
            { name: "Шоколад молочный", kcal: 550, p: 6.9, f: 35.7, c: 52.4 },
            { name: "Зефир классический", kcal: 304, p: 0.8, f: 0.0, c: 78.5 },
            { name: "Мороженое Пломбир", kcal: 227, p: 3.5, f: 15.0, c: 20.0 },

            // Напитки
            { name: "Чай черный без сахара", kcal: 1, p: 0.0, f: 0.0, c: 0.2 },
            { name: "Кофе черный без сахара", kcal: 2, p: 0.2, f: 0.0, c: 0.3 },
            { name: "Какао на молоке", kcal: 95, p: 3.8, f: 3.5, c: 12.0 },
            { name: "Сок апельсиновый свежевыжатый", kcal: 45, p: 0.7, f: 0.2, c: 10.4 },
            { name: "Квас хлебный", kcal: 27, p: 0.2, f: 0.0, c: 5.2 },
            { name: "Пиво светлое 4.5%", kcal: 43, p: 0.5, f: 0.0, c: 3.6 },
            { name: "Вино сухое красное", kcal: 68, p: 0.2, f: 0.0, c: 0.6 },
            { name: "Водка 40%", kcal: 235, p: 0.0, f: 0.0, c: 0.1 }
        ];


        const EXTRA_DB = `
Борщ с мясом|49|3.0|2.2|4.5
Борщ постный|35|1.1|1.4|4.9
Щи из свежей капусты|31|1.8|1.8|2.4
Щи кислые со сметаной|37|1.5|2.0|3.1
Суп гороховый|66|4.4|1.4|9.4
Суп куриный с лапшой|45|3.3|1.5|4.7
Суп картофельный с мясом|55|3.1|2.2|6.0
Суп грибной|40|1.6|2.0|4.0
Солянка мясная сборная|69|5.4|4.6|1.6
Рассольник|42|1.8|1.8|4.9
Харчо|75|4.2|4.0|5.6
Уха из судака|46|8.0|1.0|1.2
Окрошка на квасе|47|1.8|2.6|4.4
Борщ украинский с пампушками|78|2.8|3.1|9.5
Суп-пюре тыквенный|52|1.2|2.5|6.3
Свекольник холодный|36|1.4|1.6|4.2
Пельмени отварные|275|11.9|12.4|29.0
Вареники с картофелем|155|4.4|2.7|28.7
Вареники с творогом|189|9.1|4.4|28.0
Голубцы с мясом и рисом|105|6.0|5.2|8.4
Котлеты куриные паровые|135|18.0|5.4|3.6
Котлеты мясные жареные|220|13.5|15.0|8.0
Тефтели в томатном соусе|135|8.5|8.6|6.2
Бефстроганов|165|13.5|10.5|3.8
Плов с говядиной|165|6.0|6.8|20.6
Плов с курицей|155|7.2|5.8|19.8
Жаркое по-домашнему|135|8.1|6.8|10.4
Гуляш говяжий|145|12.0|9.0|3.2
Макароны по-флотски|188|9.5|8.0|20.0
Печень по-строгановски|130|13.4|6.2|5.5
Курица тушеная в сметане|175|17.4|11.0|2.0
Зразы картофельные с мясом|165|6.5|7.2|18.0
Рыба жареная в кляре|215|15.5|12.5|10.0
Рыба запеченная под сыром|160|17.5|8.5|3.5
Минтай тушеный с овощами|85|12.0|2.5|3.5
Яичница из двух яиц|243|13.6|20.0|0.8
Омлет с молоком|184|9.6|15.0|2.1
Сырники жареные|220|15.0|11.0|14.0
Блины на молоке|233|6.1|12.3|26.0
Оладьи на кефире|235|6.5|9.5|31.0
Драники картофельные|185|4.3|9.2|22.0
Шашлык из свинины|290|19.0|23.0|0.0
Шашлык из курицы|190|22.0|11.0|0.5
Люля-кебаб|240|16.0|18.0|2.5
Хинкали|215|10.5|9.0|23.0
Манты|205|9.8|9.5|20.0
Чебуреки|290|11.0|15.0|26.0
Шаурма куриная|215|11.0|10.0|20.0
Пицца Маргарита|250|10.5|9.8|31.0
Пицца Пепперони|285|12.0|13.5|28.0
Бургер с говядиной|265|13.0|13.0|23.0
Хот-дог|250|10.4|14.3|20.4
Суши с лососем|145|6.0|2.5|24.0
Роллы Филадельфия|185|7.0|8.0|21.0
Роллы Калифорния|175|5.5|6.0|25.0
Паста Карбонара|220|8.5|10.5|23.0
Паста Болоньезе|165|8.0|6.0|20.0
Лазанья|135|7.5|6.5|12.5
Картофель отварной|82|2.0|0.4|16.7
Картофель жареный|192|2.8|9.5|23.4
Картофельное пюре на молоке|90|2.1|3.3|13.7
Картофель фри|312|3.8|15.0|41.0
Картофель запеченный|95|2.4|0.4|20.0
Гречка отварная|110|4.2|1.1|21.3
Рис отварной|116|2.2|0.5|24.9
Рис бурый отварной|110|2.6|0.9|23.0
Макароны отварные|112|3.5|0.4|23.2
Перловка отварная|109|3.1|0.4|22.2
Овсянка на воде|88|3.0|1.7|15.0
Овсянка на молоке|102|3.2|4.1|14.2
Манная каша на молоке|98|3.0|3.2|15.3
Пшенная каша на воде|90|3.0|0.7|17.0
Кускус отварной|112|3.8|0.2|23.2
Булгур отварной|83|3.1|0.2|18.6
Киноа отварная|120|4.4|1.9|21.3
Чечевица отварная|116|9.0|0.4|20.1
Фасоль отварная|123|7.8|0.5|21.5
Нут отварной|164|8.9|2.6|27.4
Салат Оливье|198|5.0|15.0|10.0
Салат Цезарь с курицей|165|9.5|11.0|6.5
Салат Греческий|104|2.8|9.0|4.0
Сельдь под шубой|193|4.5|13.5|13.0
Винегрет|76|1.5|4.5|8.0
Салат из свежих овощей с маслом|55|1.1|4.0|3.7
Салат из капусты с морковью|75|1.4|5.0|7.0
Крабовый салат|135|4.5|9.5|8.0
Мимоза салат|200|8.0|15.0|8.0
Салат с тунцом и яйцом|155|11.0|10.0|4.5
Хлеб белый пшеничный|242|8.1|1.0|48.8
Хлеб ржаной|214|6.6|1.2|42.0
Хлеб бородинский|208|6.9|1.3|40.9
Хлеб цельнозерновой|235|9.0|2.5|43.0
Батон нарезной|264|7.5|2.9|50.9
Лаваш тонкий|236|7.9|1.0|47.6
Сухари пшеничные|331|11.2|1.4|72.4
Хлебцы цельнозерновые|295|11.0|2.5|58.0
Круассан|406|8.2|21.0|45.8
Булочка с маком|330|8.3|7.5|58.0
Пирожок с капустой жареный|230|5.5|10.5|29.0
Пирожок с мясом жареный|285|9.5|16.0|26.0
Пирожок с яблоком печеный|240|4.5|8.0|38.0
Печенье овсяное|437|6.5|14.5|71.0
Печенье песочное|458|6.5|23.0|63.0
Пряники|364|4.8|2.8|77.0
Вафли|425|3.2|19.8|57.0
Торт Наполеон|420|5.5|25.0|42.0
Торт Медовик|380|5.0|16.0|53.0
Эклер заварной|330|6.5|20.0|31.0
Пончик|380|6.0|19.0|47.0
Кекс столичный|380|7.0|14.0|59.0
Сушки|330|10.7|1.3|71.0
Крекер|440|10.0|16.0|66.0
Молоко 2.5%|52|2.8|2.5|4.7
Молоко 3.2%|58|2.9|3.2|4.7
Молоко обезжиренное|31|3.0|0.1|4.8
Молоко козье|68|3.0|4.2|4.5
Кефир 1%|40|3.0|1.0|4.0
Кефир 2.5%|53|2.9|2.5|4.0
Ряженка 4%|67|2.9|4.0|4.2
Простокваша|58|2.9|3.2|4.1
Йогурт натуральный 2%|60|4.3|2.0|6.0
Йогурт фруктовый|95|3.5|2.5|14.0
Греческий йогурт 2%|73|8.0|2.0|5.0
Сметана 15%|162|2.6|15.0|3.0
Сметана 20%|206|2.8|20.0|3.2
Сливки 10%|118|3.0|10.0|4.0
Сливки 20%|205|2.8|20.0|3.7
Творог 0%|71|16.5|0.1|1.3
Творог 5%|121|17.2|5.0|1.8
Творог 9%|159|16.7|9.0|2.0
Творог 18%|232|14.0|18.0|2.8
Творожная масса сладкая|345|7.1|23.0|27.0
Сырок глазированный|407|8.5|26.5|32.0
Сыр Российский|364|23.4|29.5|0.3
Сыр Голландский|352|26.0|26.8|0.0
Сыр Гауда|356|25.0|27.4|2.2
Сыр Моцарелла|280|22.0|22.0|2.2
Сыр Пармезан|392|33.0|28.0|0.0
Сыр Брынза|260|17.9|20.1|0.0
Сыр Фета|264|14.2|21.3|4.1
Сыр плавленый|285|16.0|23.0|8.0
Сыр Чеддер|402|25.0|33.0|1.3
Сыр Маскарпоне|435|4.8|42.0|4.8
Сыр Рикотта|174|11.3|13.0|3.0
Масло сливочное 82.5%|748|0.5|82.5|0.8
Масло топленое|892|0.3|99.0|0.0
Мороженое эскимо|270|3.5|17.0|25.0
Мороженое фруктовый лед|110|0.0|0.0|28.0
Яйцо куриное вареное|160|12.8|11.6|0.8
Яйцо перепелиное|168|11.9|13.1|0.6
Лосось запеченный|206|22.0|13.0|0.0
Лосось слабосоленый|202|20.8|13.6|0.0
Форель запеченная|168|21.0|9.0|0.0
Сельдь соленая|217|17.0|16.0|0.0
Скумбрия запеченная|223|21.0|15.0|0.0
Скумбрия горячего копчения|221|23.0|14.0|0.0
Треска отварная|78|17.7|0.7|0.0
Минтай отварной|72|15.9|0.9|0.0
Хек отварной|86|16.6|2.2|0.0
Карп запеченный|135|18.0|6.3|0.0
Судак отварной|84|18.4|1.1|0.0
Тунец консервированный в собственном соку|96|21.0|1.0|0.0
Шпроты в масле|363|17.4|32.4|0.4
Сардины в масле|230|24.0|15.0|0.0
Креветки отварные|95|20.0|1.5|0.0
Кальмар отварной|110|18.0|2.8|2.0
Мидии отварные|77|11.5|2.0|3.3
Икра красная зернистая|252|24.6|17.9|4.0
Крабовые палочки|94|5.0|1.0|15.0
Морская капуста|49|0.9|0.2|10.0
Картофель сырой|77|2.0|0.4|16.3
Морковь сырая|32|1.3|0.1|6.9
Свекла сырая|43|1.5|0.1|8.8
Капуста белокочанная|27|1.8|0.1|4.7
Капуста цветная|30|2.5|0.3|4.2
Брокколи|34|2.8|0.4|6.6
Капуста брюссельская|43|4.8|0.3|5.9
Огурец свежий|15|0.8|0.1|2.8
Помидор свежий|20|1.1|0.2|3.7
Перец болгарский сладкий|27|1.3|0.0|5.3
Баклажан|24|1.2|0.1|4.5
Кабачок|24|0.6|0.3|4.6
Тыква|28|1.3|0.3|7.7
Лук репчатый|47|1.4|0.0|10.4
Лук зеленый|19|1.3|0.0|3.5
Чеснок|143|6.5|0.5|29.9
Редис|20|1.2|0.1|3.4
Шпинат|23|2.9|0.3|2.0
Салат листовой|12|1.5|0.2|1.3
Сельдерей стебель|13|0.9|0.1|2.1
Спаржа|21|1.9|0.1|3.9
Кукуруза вареная|123|4.1|2.3|22.5
Кукуруза консервированная|119|2.2|0.4|26.0
Горошек зеленый консервированный|55|3.6|0.1|9.3
Грибы шампиньоны|27|4.3|1.0|0.1
Грибы вешенки|38|3.3|0.4|6.1
Грибы белые отварные|34|3.7|1.7|1.1
Огурцы соленые|11|0.8|0.1|1.7
Капуста квашеная|23|1.8|0.1|4.4
Оливки зеленые|125|1.4|12.7|1.3
Маслины черные|166|2.2|16.0|3.0
Имбирь корень|80|1.8|0.8|17.8
Авокадо|160|2.0|14.7|1.8
Яблоко|47|0.4|0.4|9.8
Груша|42|0.4|0.3|9.5
Банан|96|1.5|0.2|21.8
Апельсин|43|0.9|0.2|8.1
Мандарин|38|0.8|0.2|7.5
Лимон|34|0.9|0.1|3.0
Грейпфрут|35|0.7|0.2|6.5
Виноград|65|0.6|0.2|16.8
Персик|45|0.9|0.1|9.5
Абрикос|44|0.9|0.1|9.0
Слива|43|0.8|0.2|9.6
Вишня|52|0.8|0.2|10.3
Черешня|52|1.2|0.4|10.6
Клубника|41|0.8|0.4|7.5
Малина|46|0.8|0.5|8.3
Черника|44|1.1|0.6|7.6
Смородина черная|44|1.0|0.4|7.3
Арбуз|27|0.6|0.1|5.8
Дыня|33|0.6|0.3|7.4
Киви|49|1.0|0.6|10.3
Ананас|49|0.4|0.2|11.8
Манго|67|0.5|0.3|11.5
Гранат|52|0.9|0.0|11.2
Хурма|67|0.5|0.0|15.3
Инжир свежий|49|0.7|0.2|13.7
Курага|232|5.2|0.3|51.0
Изюм|264|2.9|0.6|66.0
Чернослив|231|2.3|0.7|57.5
Финики сушеные|292|2.5|0.5|69.2
Инжир сушеный|257|3.1|0.8|57.9
Грецкий орех|654|15.2|65.2|7.0
Миндаль|609|18.6|53.7|13.0
Фундук|628|15.0|61.2|9.4
Кешью|600|18.5|48.5|22.5
Арахис|551|26.3|45.2|9.9
Фисташки|556|20.0|50.0|7.0
Семена подсолнечника|572|20.7|52.9|3.4
Семена тыквы|556|24.5|45.8|4.7
Семена чиа|486|16.5|30.7|42.1
Семена льна|534|18.3|42.2|1.6
Кунжут|565|19.4|48.7|12.2
Арахисовая паста|588|25.0|50.0|20.0
Масло подсолнечное|899|0.0|99.9|0.0
Масло оливковое|898|0.0|99.8|0.0
Масло кокосовое|892|0.0|99.9|0.0
Майонез провансаль|627|0.3|67.0|2.6
Майонез легкий|260|0.8|25.0|8.0
Кетчуп томатный|93|1.8|1.0|22.2
Соус соевый|53|8.1|0.6|4.9
Горчица|143|9.9|12.7|5.3
Томатная паста|92|5.0|1.0|16.7
Сахар|399|0.0|0.0|99.8
Мед|329|0.8|0.0|81.5
Варенье|271|0.3|0.2|70.9
Джем|265|0.4|0.1|68.0
Сгущенное молоко|320|7.2|8.5|56.0
Шоколад горький 70%|540|6.2|35.4|48.2
Шоколад белый|539|5.9|30.9|59.0
Шоколадная паста|539|6.3|30.9|57.5
Конфеты шоколадные|520|4.0|28.0|60.0
Мармелад|321|0.4|0.1|79.9
Халва подсолнечная|516|11.6|29.7|54.0
Карамель леденцовая|539|0.0|0.1|97.0
Пастила|310|0.5|0.0|80.4
Гречка (крупа)|313|12.6|3.3|62.1
Рис белый (крупа)|344|6.7|0.7|78.9
Овсяные хлопья Геркулес|352|12.3|6.1|61.8
Пшено (крупа)|348|11.5|3.3|69.3
Манка (крупа)|328|10.3|1.0|67.4
Перловка (крупа)|320|9.3|1.1|66.9
Кукурузная крупа|325|8.3|1.2|75.0
Чечевица сухая|310|24.0|1.5|48.0
Горох сухой|298|20.5|2.0|49.5
Фасоль сухая|309|21.0|2.0|47.0
Мука пшеничная в/с|334|10.3|1.1|68.9
Мука ржаная|298|8.9|1.7|61.8
Макароны сухие|344|10.4|1.1|69.7
Лапша яичная|338|11.0|3.0|66.0
Крахмал картофельный|313|0.1|0.0|78.3
Мюсли|352|11.0|7.0|65.0
Кукурузные хлопья|360|7.0|1.0|82.0
Говядина (сырая)|187|18.9|12.4|0.0
Свинина (сырая)|259|16.0|21.6|0.0
Курица (сырая тушка)|190|16.0|14.0|0.0
Куриная грудка (сырая)|113|23.6|1.9|0.4
Куриное бедро (сырое)|185|16.0|13.0|0.0
Индейка (сырое филе)|84|19.2|0.7|0.0
Фарш говяжий|254|17.2|20.0|0.0
Фарш свиной|263|16.0|21.0|0.0
Фарш куриный|143|17.4|8.1|0.0
Сосиски молочные|266|11.0|24.0|0.0
Сардельки свиные|332|10.1|31.6|1.9
Ветчина|279|22.6|20.9|0.0
Буженина|510|7.4|52.6|0.0
Корейка копченая|467|10.5|47.0|0.0
Колбаса вареная Любительская|301|12.2|28.0|0.0
Колбаса копченая Краковская|466|16.2|44.6|0.0
Тушенка говяжья консервированная|220|16.8|16.1|0.0
Паштет печеночный|222|13.0|17.0|3.0
Вода минеральная|0|0.0|0.0|0.0
Сок яблочный|46|0.5|0.4|9.8
Сок томатный|18|1.1|0.2|3.8
Сок виноградный|54|0.3|0.0|14.0
Сок мультифрукт|48|0.5|0.1|11.0
Компот из сухофруктов|60|0.8|0.0|14.2
Кисель ягодный|53|0.2|0.0|13.4
Кока-кола|42|0.0|0.0|10.6
Пепси|41|0.0|0.0|10.4
Лимонад|26|0.0|0.0|6.4
Энергетический напиток|45|0.0|0.0|11.0
Чай зеленый без сахара|1|0.0|0.0|0.0
Чай с сахаром (1 ч.л.)|20|0.0|0.0|5.0
Кофе с молоком и сахаром|58|1.0|1.5|9.0
Капучино|45|2.5|2.3|3.7
Латте|56|3.0|2.7|5.0
Какао на воде|40|1.5|1.5|6.0
Пиво темное|48|0.5|0.0|5.0
Шампанское полусладкое|88|0.2|0.0|5.0
Вино белое сухое|66|0.1|0.0|0.6
Коньяк|239|0.0|0.0|0.1
Виски|250|0.0|0.0|0.1
Ром|220|0.0|0.0|0.0
`;
        (function(){
            const have = new Set(foodDatabase.map(p => p.name.toLowerCase()));
            EXTRA_DB.trim().split('\n').forEach(l => {
                const [name,k,p,f,c] = l.split('|');
                if (!name || have.has(name.toLowerCase())) return;
                have.add(name.toLowerCase());
                foodDatabase.push({ name, kcal:+k, p:+p, f:+f, c:+c });
            });
        })();
        let customProducts = safeLS('cal_pro_custom');
        let savedDishes = safeLS('cal_pro_dishes');
        function getAllProducts() { return [...customProducts, ...foodDatabase, ...savedDishes]; }

        let recipeItems = [];
        let diaryItems = safeLS('cal_pro_diary');

        let toastTimer;
        function showToast(text) {
            const toast = document.getElementById('toast');
            document.getElementById('toast-msg').textContent = text;
            toast.classList.remove('translate-y-24', 'opacity-0');
            clearTimeout(toastTimer);
            toastTimer = setTimeout(() => toast.classList.add('translate-y-24', 'opacity-0'), 2500);
        }

        window.calSetLang = function(lang){ state.lang = lang; renderCatalog(document.getElementById("catalogSearch").value); };

        function setupAutocomplete(inputEl, suggestionsEl, onSelect) {
            inputEl.addEventListener('input', () => {
                const query = inputEl.value.toLowerCase().trim();
                if (!query) { suggestionsEl.style.display = 'none'; return; }
                const matches = getAllProducts().filter(i => i.name.toLowerCase().includes(query)).slice(0, 12);
                if (matches.length === 0) { suggestionsEl.style.display = 'none'; return; }

                suggestionsEl.innerHTML = matches.map(i => `
                    <div class="p-3 text-xs hover:bg-emerald-50 cursor-pointer flex justify-between border-b border-emerald-50" data-name="${i.name}">
                        <strong>${i.name}</strong>
                        <span class="text-emerald-600">${Math.round(i.kcal)} ккал/100г</span>
                    </div>
                `).join('');
                suggestionsEl.style.display = 'block';

                suggestionsEl.querySelectorAll('div[data-name]').forEach(el => {
                    el.addEventListener('click', () => {
                        const name = el.getAttribute('data-name');
                        inputEl.value = name;
                        suggestionsEl.style.display = 'none';
                        onSelect(getAllProducts().find(p => p.name === name));
                    });
                });
            });
            document.addEventListener('click', e => {
                if (!inputEl.contains(e.target) && !suggestionsEl.contains(e.target)) suggestionsEl.style.display = 'none';
            });
        }

        function parseAmount(str) {
            str = str.toLowerCase().trim();
            let num = parseFloat(str) || 100;
            if (str.includes('шт')) return num * 55;
            if (str.includes('ст.л')) return num * 15;
            if (str.includes('ч.л')) return num * 5;
            if (str.includes('кг')) return num * 1000;
            return num;
        }

        // Рецепты
        const recipeInput = document.getElementById('recipeInput');
        const recipeAmount = document.getElementById('recipeAmount');
        let currentRecipeProd = null;
        setupAutocomplete(recipeInput, document.getElementById('recipeSuggestions'), (prod) => {
            currentRecipeProd = prod;
            recipeAmount.value = prod.defaultGram ? prod.defaultGram + 'г' : '100г';
            recipeAmount.focus();
        });

        document.getElementById('addRecipeBtn').addEventListener('click', () => {
            const name = recipeInput.value.trim();
            const amtStr = recipeAmount.value.trim() || '100г';
            if (!name) return;
            let prod = getAllProducts().find(p => p.name.toLowerCase() === name.toLowerCase()) || currentRecipeProd;
            if (!prod) prod = { name: name, kcal: 150, p: 5, f: 5, c: 20 };
            let grams = parseAmount(amtStr);

            recipeItems.push({
                id: Date.now() + Math.random(),
                name: prod.name, grams,
                kcal: prod.kcal * grams / 100,
                p: prod.p * grams / 100,
                f: prod.f * grams / 100,
                c: prod.c * grams / 100
            });
            recipeInput.value = ''; recipeAmount.value = ''; currentRecipeProd = null;
            renderRecipe();
        });

        function renderRecipe() {
            const table = document.getElementById('recipeTable');
            const tbody = document.getElementById('recipeTableBody');
            const empty = document.getElementById('emptyRecipe');
            const summary = document.getElementById('recipeSummary');

            if (recipeItems.length === 0) {
                table.classList.add('hidden'); summary.classList.add('hidden'); empty.classList.remove('hidden'); return;
            }
            empty.classList.add('hidden'); table.classList.remove('hidden'); summary.classList.remove('hidden');

            tbody.innerHTML = recipeItems.map(i => `
                <tr>
                    <td class="p-3 font-semibold">${i.name}</td>
                    <td class="p-3">${i.grams} г</td>
                    <td class="p-3 font-bold text-emerald-600">${Math.round(i.kcal)}</td>
                    <td class="p-3">${i.p.toFixed(1)} г</td>
                    <td class="p-3">${i.f.toFixed(1)} г</td>
                    <td class="p-3">${i.c.toFixed(1)} г</td>
                    <td class="p-3 text-right"><button class="text-rose-600 font-bold text-xs cursor-pointer" onclick="removeRecipeItem('${i.id}')">✕</button></td>
                </tr>
            `).join('');

            const totW = recipeItems.reduce((s, i) => s + i.grams, 0);
            const totK = recipeItems.reduce((s, i) => s + i.kcal, 0);
            const totP = recipeItems.reduce((s, i) => s + i.p, 0);
            const totF = recipeItems.reduce((s, i) => s + i.f, 0);
            const totC = recipeItems.reduce((s, i) => s + i.c, 0);

            document.getElementById('resWeight').textContent = totW + ' г';
            if (totW > 0) {
                document.getElementById('resCal').textContent = Math.round(totK * 100 / totW);
                document.getElementById('resP').textContent = (totP * 100 / totW).toFixed(1) + ' г';
                document.getElementById('resF').textContent = (totF * 100 / totW).toFixed(1) + ' г';
                document.getElementById('resC').textContent = (totC * 100 / totW).toFixed(1) + ' г';
            }
        }

        window.removeRecipeItem = (id) => { recipeItems = recipeItems.filter(i => i.id != id); renderRecipe(); };
        function clearRecipe() { recipeItems = []; renderRecipe(); }

        function saveAsDish() {
            if (recipeItems.length === 0) return;
            const dishName = (document.getElementById("dishName").value || "Мой рецепт").trim().replace(/[<>"&]/g,"");
            if (!dishName) return;
            const totW = recipeItems.reduce((s, i) => s + i.grams, 0);
            const totK = recipeItems.reduce((s, i) => s + i.kcal, 0);
            const totP = recipeItems.reduce((s, i) => s + i.p, 0);
            const totF = recipeItems.reduce((s, i) => s + i.f, 0);
            const totC = recipeItems.reduce((s, i) => s + i.c, 0);

            savedDishes.push({
                name: dishName,
                kcal: Math.round(totK * 100 / totW),
                p: +(totP * 100 / totW).toFixed(1),
                f: +(totF * 100 / totW).toFixed(1),
                c: +(totC * 100 / totW).toFixed(1)
            });
            try { localStorage.setItem('cal_pro_dishes', JSON.stringify(savedDishes)); } catch (e) {};
            showToast('Блюдо успешно сохранено в базу!');
            renderCatalog();
        }

        // Дневник
        const diaryInput = document.getElementById('diaryInput');
        const diaryAmount = document.getElementById('diaryAmount');
        let currentDiaryProd = null;
        setupAutocomplete(diaryInput, document.getElementById('diarySuggestions'), (prod) => {
            currentDiaryProd = prod;
            diaryAmount.value = prod.defaultGram ? prod.defaultGram + 'г' : '100г';
            diaryAmount.focus();
        });

        document.getElementById('addDiaryBtn').addEventListener('click', () => {
            const meal = document.getElementById('mealTime').value;
            const name = diaryInput.value.trim();
            const amtStr = diaryAmount.value.trim() || '100г';
            if (!name) return;
            let prod = getAllProducts().find(p => p.name.toLowerCase() === name.toLowerCase()) || currentDiaryProd;
            if (!prod) prod = { name: name, kcal: 150, p: 5, f: 5, c: 20 };
            let grams = parseAmount(amtStr);

            diaryItems.push({
                id: Date.now() + Math.random(),
                meal, name: prod.name, grams,
                kcal: Math.round(prod.kcal * grams / 100),
                p: +(prod.p * grams / 100).toFixed(1),
                f: +(prod.f * grams / 100).toFixed(1),
                c: +(prod.c * grams / 100).toFixed(1)
            });
            try { localStorage.setItem('cal_pro_diary', JSON.stringify(diaryItems)); } catch (e) {};
            diaryInput.value = ''; diaryAmount.value = ''; currentDiaryProd = null;
            renderDiary();
        });

        function renderDiary() {
            const table = document.getElementById('diaryTable');
            const tbody = document.getElementById('diaryTableBody');
            const empty = document.getElementById('emptyDiary');
            const summary = document.getElementById('diarySummary');

            if (diaryItems.length === 0) {
                table.classList.add('hidden'); summary.classList.add('hidden'); empty.classList.remove('hidden'); return;
            }
            empty.classList.add('hidden'); table.classList.remove('hidden'); summary.classList.remove('hidden');

            tbody.innerHTML = diaryItems.map(i => `
                <tr>
                    <td class="p-3 font-bold text-emerald-800">${i.meal}</td>
                    <td class="p-3">${i.name}</td>
                    <td class="p-3">${i.grams} г</td>
                    <td class="p-3 font-bold text-emerald-600">${i.kcal}</td>
                    <td class="p-3 text-xs">Б:${i.p} Ж:${i.f} В:${i.c}</td>
                    <td class="p-3 text-right"><button class="text-rose-600 font-bold cursor-pointer" onclick="removeDiaryItem('${i.id}')">✕</button></td>
                </tr>
            `).join('');

            document.getElementById('dayCal').textContent = diaryItems.reduce((s, i) => s + i.kcal, 0);
            document.getElementById('dayP').textContent = diaryItems.reduce((s, i) => s + i.p, 0).toFixed(1) + ' г';
            document.getElementById('dayF').textContent = diaryItems.reduce((s, i) => s + i.f, 0).toFixed(1) + ' г';
            document.getElementById('dayC').textContent = diaryItems.reduce((s, i) => s + i.c, 0).toFixed(1) + ' г';
        }

        window.removeDiaryItem = (id) => {
            diaryItems = diaryItems.filter(i => i.id != id);
            try { localStorage.setItem('cal_pro_diary', JSON.stringify(diaryItems)); } catch (e) {};
            renderDiary();
        };

        function copyDiaryReport() {
            let text = "📅 Отчет питания за сегодня:\n";
            diaryItems.forEach(i => { text += `[${i.meal}] ${i.name} (${i.grams}г) — ${i.kcal} ккал\n`; });
            text += `\n🔥 Итого: ${document.getElementById('dayCal').textContent} ккал`;
            navigator.clipboard.writeText(text);
            showToast('Отчет скопирован в буфер обмена!');
        }

        // Модальное окно своего продукта
        function openModal() { document.getElementById('customModal').classList.remove('hidden'); document.getElementById('customModal').classList.add('flex'); }
        function closeModal() { document.getElementById('customModal').classList.add('hidden'); document.getElementById('customModal').classList.remove('flex'); }

        function saveCustomProduct() {
            const name = document.getElementById('customName').value.trim();
            const kcal = parseFloat(document.getElementById('customKcal').value) || 0;
            const p = parseFloat(document.getElementById('customP').value) || 0;
            const f = parseFloat(document.getElementById('customF').value) || 0;
            const c = parseFloat(document.getElementById('customC').value) || 0;
            if (!name) return;

            customProducts.push({ name, kcal, p, f, c });
            try { localStorage.setItem('cal_pro_custom', JSON.stringify(customProducts)); } catch (e) {};
            closeModal();
            showToast('Продукт успешно добавлен в базу!');
            renderCatalog();
        }

        
        let catLimit = 150;
        function renderCatalog(filter = '') {
            const q = filter.toLowerCase().trim();
            const all = getAllProducts();
            const filtered = q ? all.filter(i => i.name.toLowerCase().includes(q)) : all;
            const shown = filtered.slice(0, catLimit);
            document.getElementById('catalogTableBody').innerHTML = shown.map(i => `
                <tr class="hover:bg-emerald-50/50">
                    <td class="p-3 font-semibold">${i.name}</td>
                    <td class="p-3 font-bold text-emerald-600">${Math.round(i.kcal)}</td>
                    <td class="p-3">${Number(i.p).toFixed(1)} г</td>
                    <td class="p-3">${Number(i.f).toFixed(1)} г</td>
                    <td class="p-3">${Number(i.c).toFixed(1)} г</td>
                </tr>`).join('');
            document.getElementById('catalogCount').textContent = 'Показано ' + shown.length + ' из ' + filtered.length + ' (всего в базе: ' + all.length + ')';
            document.getElementById('catMoreBtn').style.display = filtered.length > shown.length ? 'inline-block' : 'none';
            const sc = document.getElementById('statCount'); if (sc) sc.textContent = all.length;
        }
        function catMore() { catLimit += 300; renderCatalog(document.getElementById('catalogSearch').value); }
        document.getElementById('catalogSearch').addEventListener('input', e => { catLimit = 150; renderCatalog(e.target.value); });

        function importProducts() {
            const txt = document.getElementById('importText').value;
            const have = new Set(getAllProducts().map(p => p.name.toLowerCase()));
            let added = 0, skipped = 0;
            txt.split(/\r?\n/).forEach(line => {
                const parts = line.split(/[;\t|]/).map(s => s.trim());
                if (parts.length < 5) { if (line.trim()) skipped++; return; }
                const name = parts[0].replace(/[<>"&]/g, '');
                const n = parts.slice(1, 5).map(s => parseFloat(s.replace(',', '.')));
                if (!name || n.some(isNaN)) { skipped++; return; }
                if (have.has(name.toLowerCase())) { skipped++; return; }
                have.add(name.toLowerCase());
                customProducts.push({ name, kcal: n[0], p: n[1], f: n[2], c: n[3] });
                added++;
            });
            try { try { localStorage.setItem('cal_pro_custom', JSON.stringify(customProducts)); } catch (e) {}; } catch (e) {}
            document.getElementById('importText').value = '';
            showToast('Добавлено: ' + added + ', пропущено: ' + skipped);
            renderCatalog(document.getElementById('catalogSearch').value);
        }
        function exportProducts() {
            const text = getAllProducts().map(p => [p.name, p.kcal, p.p, p.f, p.c].join(';')).join('\n');
            document.getElementById('importText').value = text;
            showToast('База выгружена в поле ниже — скопируйте её');
        }

        
 renderCatalog(); renderRecipe(); renderDiary();
 Object.assign(window,{openModal,closeModal,saveCustomProduct,clearRecipe,saveAsDish,copyDiaryReport,importProducts,exportProducts,catMore});
})();
</script>
<script>
function go(p){ location.hash = p; }
function route(){
  let p=(location.hash||'#home').slice(1); if(!document.getElementById('page-'+p)) p='home';
  document.querySelectorAll('.page').forEach(e=>e.classList.toggle('active',e.id==='page-'+p));
  document.querySelectorAll('.navl').forEach(a=>a.classList.toggle('on',(a.dataset.nav||a.dataset.mnav)===p));
  window.scrollTo(0,0);
}
window.addEventListener('hashchange',route); route();
</script>
</body>
</html>


<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>جدول المذاكرة التفاعلي ✨</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        .checkmark {
            display: none;
        }
        .checked .checkmark {
            display: block;
        }
    </style>
</head>
<body class="min-h-screen bg-gradient-to-br from-pink-50 via-purple-50 to-pink-100 p-4 md:p-8">
    <div class="max-w-5xl mx-auto">
        <div class="text-center mb-8">
            <h1 class="text-4xl md:text-5xl font-bold text-transparent bg-clip-text bg-gradient-to-r from-pink-500 to-purple-600 mb-2">
                ✨ جدول المذاكرة ✨
            </h1>
            <p class="text-pink-600 text-lg">مقاطع إيهاب + بنك كمي</p>
        </div>

        <div id="weeksContainer" class="space-y-6"></div>

        <div class="mt-8 bg-gradient-to-r from-pink-400 to-purple-500 rounded-2xl p-6 text-white text-center shadow-xl">
            <p class="text-2xl font-bold mb-2">💪 استمري وبتوصلين لهدفك!</p>
            <p class="text-lg">كل يوم خطوة للأمام 🌟</p>
        </div>
    </div>

    <script>
        const weeks = [
            {
                title: "الأسبوع الأول",
                days: [
                    { date: "الأحد 12 يناير", clips: 2, bank: 1 },
                    { date: "الاثنين 13 يناير", clips: 2, bank: 1 },
                    { date: "الثلاثاء 14 يناير", clips: 2, bank: 1 },
                    { date: "الأربعاء 15 يناير", clips: 2, bank: 1 },
                    { date: "الخميس 16 يناير", clips: 3, bank: 2 },
                    { date: "الجمعة 17 يناير", clips: 3, bank: 2 },
                    { date: "السبت 18 يناير", clips: 2, bank: 2 }
                ]
            },
            {
                title: "الأسبوع الثاني",
                days: [
                    { date: "الأحد 19 يناير", clips: 2, bank: 1 },
                    { date: "الاثنين 20 يناير", clips: 2, bank: 1 },
                    { date: "الثلاثاء 21 يناير", clips: 2, bank: 1 },
                    { date: "الأربعاء 22 يناير", clips: 2, bank: 1 },
                    { date: "الخميس 23 يناير", clips: 3, bank: 2 },
                    { date: "الجمعة 24 يناير", clips: 3, bank: 2 },
                    { date: "السبت 25 يناير", clips: 2, bank: 2 }
                ]
            },
            {
                title: "الأسبوع الثالث",
                days: [
                    { date: "الأحد 26 يناير", clips: 2, bank: 1 },
                    { date: "الاثنين 27 يناير", clips: 2, bank: 1 },
                    { date: "الثلاثاء 28 يناير", clips: 2, bank: 1 },
                    { date: "الأربعاء 29 يناير", clips: 2, bank: 1 },
                    { date: "الخميس 30 يناير", clips: 3, bank: 2 },
                    { date: "الجمعة 31 يناير", clips: 3, bank: 2 },
                    { date: "السبت 1 فبراير", clips: 2, bank: 2 }
                ]
            },
            {
                title: "الأسبوع الرابع",
                days: [
                    { date: "الأحد 2 فبراير", clips: 2, bank: 1 },
                    { date: "الاثنين 3 فبراير", clips: 2, bank: 1 },
                    { date: "الثلاثاء 4 فبراير", clips: 2, bank: 1 },
                    { date: "الأربعاء 5 فبراير", clips: 2, bank: 1 },
                    { date: "الخميس 6 فبراير", clips: 3, bank: 2 },
                    { date: "الجمعة 7 فبراير", clips: 3, bank: 2 },
                    { date: "السبت 8 فبراير", clips: 2, bank: 2 }
                ]
            },
            {
                title: "الأيام الأخيرة",
                days: [
                    { date: "الأحد 9 فبراير", clips: 2, bank: 0, note: "مراجعة فقط" },
                    { date: "الاثنين 10 فبراير", clips: 2, bank: 0 },
                    { date: "الثلاثاء 11 فبراير", clips: 2, bank: 0 },
                    { date: "الأربعاء 12 فبراير", clips: 1, bank: 0, note: "مراجعة خفيفة" }
                ]
            }
        ];

        // Load saved progress
        let checkedItems = {};
        const savedData = localStorage.getItem('studyProgress');
        if (savedData) {
            checkedItems = JSON.parse(savedData);
        }

        // Save progress
        function saveProgress() {
            localStorage.setItem('studyProgress', JSON.stringify(checkedItems));
        }

        // Toggle checkbox
        function toggleCheck(key, element) {
            checkedItems[key] = !checkedItems[key];
            if (checkedItems[key]) {
                element.classList.add('checked');
                element.classList.add('bg-pink-500', 'border-pink-500');
                element.classList.remove('border-pink-300');
            } else {
                element.classList.remove('checked');
                element.classList.remove('bg-pink-500', 'border-pink-500');
                element.classList.add('border-pink-300');
            }
            saveProgress();
        }

        // Create checkbox
        function createCheckbox(key, label) {
            const isChecked = checkedItems[key];
            const checkboxHtml = `
                <div class="flex items-center gap-2">
                    <button 
                        onclick="toggleCheck('${key}', this)"
                        class="w-6 h-6 rounded-md border-2 flex items-center justify-center transition-all ${
                            isChecked 
                                ? 'bg-pink-500 border-pink-500 checked' 
                                : 'border-pink-300 hover:border-pink-400'
                        }"
                    >
                        <svg class="w-4 h-4 text-white checkmark" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M5 13l4 4L19 7"></path>
                        </svg>
                    </button>
                    <span class="${label.includes('مقطع') ? 'text-pink-700' : 'text-purple-700'}">
                        ${label}
                    </span>
                </div>
            `;
            return checkboxHtml;
        }

        // Render weeks
        const container = document.getElementById('weeksContainer');
        weeks.forEach((week, weekIndex) => {
            const weekDiv = document.createElement('div');
            weekDiv.className = 'bg-white/80 backdrop-blur-sm rounded-2xl shadow-lg p-6 border-2 border-pink-200';
            
            let daysHtml = '';
            week.days.forEach((day, dayIndex) => {
                const key = `${weekIndex}-${dayIndex}`;
                const clipsKey = `${key}-clips`;
                const bankKey = `${key}-bank`;
                
                const noteHtml = day.note ? `<span class="text-pink-500 text-sm italic">(${day.note})</span>` : '';
                const bankHtml = day.bank > 0 ? createCheckbox(bankKey, `${day.bank} بنك`) : '';
                
                daysHtml += `
                    <div class="bg-gradient-to-r from-pink-50 to-purple-50 rounded-xl p-4 border border-pink-200">
                        <div class="flex items-center justify-between gap-4 flex-wrap">
                            <div class="font-semibold text-purple-700 min-w-[160px]">
                                ${day.date}
                            </div>
                            <div class="flex items-center gap-6 flex-1 flex-wrap">
                                ${createCheckbox(clipsKey, `${day.clips} مقطع`)}
                                ${bankHtml}
                                ${noteHtml}
                            </div>
                        </div>
                    </div>
                `;
            });
            
            weekDiv.innerHTML = `
                <h2 class="text-2xl font-bold text-pink-600 mb-4 flex items-center gap-2">
                    <span class="text-3xl">🌸</span>
                    ${week.title}
                </h2>
                <div class="space-y-3">
                    ${daysHtml}
                </div>
            `;
            
            container.appendChild(weekDiv);
        });
    </script>
</body>
</html>

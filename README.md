<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>معلومات الجهاز</title>
    <!-- تحميل Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* استخدام خط Inter */
        body {
            font-family: 'Inter', sans-serif;
        }
        /* دعم خطوط جوجل لـ Inter (اختياري إذا لم يكن الخط متوفراً) */
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');
    </style>
</head>
<body class="bg-gray-100 min-h-screen flex items-center justify-center p-4">

    <div class="w-full max-w-2xl bg-white rounded-lg shadow-lg p-6 md:p-8">
        <h1 class="text-2xl md:text-3xl font-bold text-center text-gray-800 mb-6">
            معلومات جهازك
        </h1>
        
        <div class="space-y-4">
            <!-- سيتم ملء هذه العناصر باستخدام JavaScript -->
            <div id="info-container" class="space-y-3">
                <p class="text-center text-gray-500">جاري تحميل المعلومات...</p>
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const infoContainer = document.getElementById('info-container');
            infoContainer.innerHTML = ''; // مسح رسالة التحميل

            // دالة لإنشاء وعرض كل معلومة
            const addInfoEntry = (key, value) => {
                const entry = document.createElement('div');
                entry.className = "flex justify-between items-center p-3 bg-gray-50 rounded-lg border border-gray-200";
                
                const keySpan = document.createElement('span');
                keySpan.className = "font-semibold text-gray-700";
                keySpan.textContent = key;
                
                const valueSpan = document.createElement('span');
                valueSpan.className = "text-gray-600 text-left break-all";
                valueSpan.textContent = value || 'غير متاح';
                
                entry.appendChild(keySpan);
                entry.appendChild(valueSpan);
                infoContainer.appendChild(entry);
            };

            // 1. User Agent (معلومات المتصفح والنظام)
            addInfoEntry('المتصفح والنظام (User Agent)', navigator.userAgent);
            
            // 2. دقة الشاشة
            addInfoEntry('دقة الشاشة', `${screen.width} x ${screen.height} بكسل`);
            
            // 3. الدقة المتاحة
            addInfoEntry('الشاشة المتاحة', `${screen.availWidth} x ${screen.availHeight} بكسل`);

            // 4. عمق الألوان
            addInfoEntry('عمق الألوان', `${screen.colorDepth}-bit`);
            
            // 5. لغة المتصفح
            addInfoEntry('لغة المتصفح', navigator.language);
            
            // 6. المنصة (النظام)
            addInfoEntry('المنصة (Platform)', navigator.platform);
            
            // 7. الكوكيز مفعلة
            addInfoEntry('الكوكيز (Cookies)', navigator.cookieEnabled ? 'مفعلة' : 'معطلة');
            
            // 8. حالة الاتصال
            addInfoEntry('متصل بالإنترنت', navigator.onLine ? 'نعم' : 'لا');

            // 9. عدد أنوية المعالج
            addInfoEntry('أنوية المعالج (Threads)', navigator.hardwareConcurrency);
            
            // 10. الذاكرة (RAM) - تقريبي
            addInfoEntry('الذاكرة (RAM) - تقريبي', `${navigator.deviceMemory || 'غير متاح'} GB`);

            // 11. معلومات البطارية (تتطلب موافقة)
            if (navigator.getBattery) {
                navigator.getBattery().then(battery => {
                    const level = `${(battery.level * 100).toFixed(0)}%`;
                    const charging = battery.charging ? ' (جاري الشحن)' : '';
                    addInfoEntry('البطارية', `${level}${charging}`);
                }).catch(e => {
                    addInfoEntry('البطارية', 'غير متاح (أو مرفوض)');
                });
            } else {
                addInfoEntry('البطارية', 'غير مدعوم');
            }

            // 12. بيانات الرابط (Query Parameters)
            const urlParams = new URLSearchParams(window.location.search);
            const chatId = urlParams.get('chatId');
            if (chatId) {
                addInfoEntry('معرف الدردشة (chatId)', chatId);
            }

        });
    </script>

</body>
</html>

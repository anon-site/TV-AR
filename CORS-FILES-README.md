# دليل ملفات حل CORS 📚

تم إنشاء عدة ملفات لحل مشكلة CORS مع روابط SHLS. إليك شرح كل ملف:

---

## 📖 ملفات التوثيق

### 1. `CORS-FIX-QUICK.md` (4.7 KB)
**دليل سريع - ابدأ من هنا!**

- ✅ حل سريع في 5 دقائق
- ✅ خطوات واضحة ومباشرة
- ✅ مثالي للمبتدئين
- ✅ يستخدم CloudFlare Worker (مجاني)

**استخدمه إذا:** تريد حل سريع بدون تفاصيل كثيرة.

---

### 2. `CORS-SOLUTION.md` (9.9 KB)
**دليل شامل ومفصل**

- 📚 شرح كامل للمشكلة
- 📚 4 حلول مختلفة (CloudFlare, PHP, Netlify, Proxies)
- 📚 أمثلة كود متقدمة
- 📚 FAQ وتشخيص المشاكل

**استخدمه إذا:** تريد فهم عميق أو حلول بديلة.

---

### 3. `WARP.md` (محدّث)
**توثيق المشروع الكامل**

تم إضافة قسم **CORS Issues** يشرح:
- المشكلة بشكل مختصر
- الحل الموصى به
- روابط للملفات الأخرى

**استخدمه:** كمرجع عام للمشروع وWarp AI.

---

## 💻 ملفات الكود

### 4. `cloudflare-worker.js` (3.1 KB)
**CloudFlare Worker - الحل الموصى به**

**ماذا يفعل؟**
- يعمل كـ Proxy بين موقعك والسيرفر SHLS
- يضيف CORS headers اللازمة
- يسمح فقط بـ `edgenextcdn.net` (أمان)

**كيف تستخدمه؟**
1. اذهب إلى https://dash.cloudflare.com/
2. Workers & Pages → Create Worker
3. انسخ المحتوى والصقه
4. Deploy
5. استخدم الرابط في `script.js`

**مميزات:**
- ✅ مجاني 100,000 طلب/يوم
- ✅ سريع جداً (CDN عالمي)
- ✅ موثوق
- ✅ بدون سيرفر خاص

---

### 5. `cors-proxy.php` (2.7 KB)
**PHP Proxy - بديل إذا كان لديك سيرفر**

**ماذا يفعل؟**
- نفس عمل CloudFlare Worker لكن على سيرفر PHP
- يستخدم cURL لجلب البيانات
- يضيف CORS headers

**متطلبات:**
- سيرفر يدعم PHP 7.0+
- cURL مفعّل

**كيف تستخدمه؟**
1. ارفع الملف على سيرفرك
2. استخدم: `https://yourdomain.com/cors-proxy.php?url=STREAM_URL`

**مميزات:**
- ✅ تحكم كامل
- ✅ بدون حدود على الطلبات
- ✅ خصوصية أفضل

**عيوب:**
- ❌ يحتاج سيرفر خاص
- ❌ أبطأ من CloudFlare Worker

---

### 6. `sw.js` (محدّث)
**Service Worker - تم تحسينه**

تم إضافة دعم CORS لـ SHLS streams مباشرة في Service Worker.

**ملاحظة:** هذا الحل **لا يعمل 100%** لأن المتصفح يمنع CORS قبل وصول الطلب للـ Service Worker. استخدم CloudFlare Worker بدلاً منه.

---

## 📊 مقارنة الحلول

| الحل | التكلفة | السرعة | الموثوقية | سهولة الإعداد |
|------|---------|--------|-----------|---------------|
| **CloudFlare Worker** ⭐ | مجاني | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **PHP Proxy** | $3-5/شهر | ⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ |
| **Netlify Function** | مجاني | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Public Proxies** ⚠️ | مجاني | ⭐⭐ | ⭐ | ⭐⭐⭐⭐⭐ |

**الموصى به:** ⭐ **CloudFlare Worker**

---

## 🚀 خطوات التطبيق السريع

### للمبتدئين (5 دقائق)

1. **اقرأ:** `CORS-FIX-QUICK.md`
2. **أنشئ:** CloudFlare Worker من `cloudflare-worker.js`
3. **عدّل:** `script.js` حسب التعليمات
4. **اختبر:** في Console
5. **Deploy:** على GitHub

### للمتقدمين

1. **اقرأ:** `CORS-SOLUTION.md`
2. **اختر:** الحل المناسب لك
3. **طبّق:** حسب التعليمات التفصيلية
4. **اختبر:** بشكل شامل
5. **Deploy:** مع مراقبة الأداء

---

## 🔍 اختبار الحلول

### اختبار CloudFlare Worker

```powershell
# في PowerShell
curl "https://YOUR-WORKER.workers.dev/?url=https://shls-live-enc.edgenextcdn.net/out/v1/f6d718e841f8442f8374de47f18c93a7/index_1.m3u8"
```

يجب أن يرجع محتوى M3U8:
```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:6
...
```

### اختبار PHP Proxy

```powershell
# في PowerShell
curl "https://yourdomain.com/cors-proxy.php?url=https://shls-live-enc.edgenextcdn.net/out/v1/f6d718e841f8442f8374de47f18c93a7/index_1.m3u8"
```

### اختبار في المتصفح

افتح Console (F12):
```javascript
fetch('https://YOUR-WORKER.workers.dev/?url=https://shls-live-enc.edgenextcdn.net/out/v1/f6d718e841f8442f8374de47f18c93a7/index_1.m3u8')
  .then(r => r.text())
  .then(data => console.log('✅ نجح!', data.substring(0, 200)))
  .catch(e => console.error('❌ فشل:', e));
```

---

## ❓ الأسئلة الشائعة

### لماذا CloudFlare Worker أفضل من PHP؟

1. **مجاني تماماً** (100K طلب/يوم)
2. **أسرع بكثير** (CDN عالمي في 200+ مدينة)
3. **أكثر موثوقية** (99.99% uptime)
4. **بدون سيرفر** (لا يحتاج استضافة)
5. **سهل الإعداد** (5 دقائق)

### متى أستخدم PHP Proxy؟

- لديك سيرفر خاص
- تريد تحكم كامل
- لديك احتياجات خاصة (logging, caching, etc.)
- تريد خصوصية أفضل

### هل يمكن استخدام Service Worker؟

**لا** - Service Worker لا يحل مشكلة CORS لأن المتصفح يمنع الطلب قبل وصوله للـ Service Worker.

---

## 🎯 الملخص النهائي

```
📁 الملفات المنشأة:
├── CORS-FIX-QUICK.md      → ابدأ من هنا (5 دقائق)
├── CORS-SOLUTION.md       → دليل شامل (للمتقدمين)
├── cloudflare-worker.js   → انسخه على CloudFlare
├── cors-proxy.php         → ارفعه على سيرفر PHP
└── WARP.md               → محدّث بقسم CORS

🎖️ الحل الموصى به:
CloudFlare Worker (مجاني، سريع، موثوق)

⏱️ الوقت المتوقع:
5 دقائق للإعداد الكامل

💰 التكلفة:
$0 (مجاني 100%)

✅ النتيجة:
روابط SHLS تعمل على GitHub Pages كما تعمل على localhost!
```

---

## 📞 الدعم

إذا واجهت مشكلة:
1. تحقق من خطوات التثبيت في `CORS-FIX-QUICK.md`
2. اقرأ FAQ في `CORS-SOLUTION.md`
3. تحقق من Console في المتصفح (F12)
4. تأكد من Deploy الـ Worker بنجاح

**نصيحة:** ابدأ بالحل السريع، وإذا احتجت تفاصيل أكثر، راجع الدليل الشامل.

---

**🎉 بالتوفيق! الآن روابط SHLS ستعمل على GitHub Pages بدون مشاكل!**

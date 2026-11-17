---
category: general
date: 2026-06-04
description: استخراج SVG من HTML وتصدير ملف SVG مع خيارات حفظ مخصصة للـ SVG، مع الحفاظ
  على CSS الخارجي دون تعديل. اتبع هذا الدليل خطوة بخطوة.
draft: false
keywords:
- extract svg from html
- export svg file
- svg save options
- svg external css
- inline svg markup
language: ar
og_description: استخراج SVG من HTML بسرعة. يوضح هذا الدرس كيفية تصدير ملف SVG باستخدام
  خيارات حفظ SVG مع الحفاظ على CSS الخارجي.
og_title: استخراج SVG من HTML – دليل تصدير ملف SVG
schemas:
- author: Aspose
  dateModified: '2026-06-04'
  description: Extract SVG from HTML and export SVG file with custom SVG save options,
    keeping external CSS intact. Follow this step‑by‑step tutorial.
  headline: Extract SVG from HTML – Full Guide to Export SVG File
  type: TechArticle
tags:
- SVG
- HTML
- Export
- Scripting
title: استخراج SVG من HTML – دليل كامل لتصدير ملف SVG
url: /ar/python/general/extract-svg-from-html-full-guide-to-export-svg-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج SVG من HTML – دليل كامل لتصدير ملف SVG

هل احتجت يومًا إلى **extract svg from html** لكن لم تكن متأكدًا أي استدعاءات API تمنحك ملفًا نظيفًا ومستقلاً؟ لست وحدك. في العديد من مشاريع أتمتة الويب، يكون الـ SVG مدمجًا داخل صفحة، واستخراجه مع الحفاظ على الأنماط الأصلية يُعد أمرًا محيرًا.  

في هذا الدليل سنرشدك إلى حل كامل لا يقتصر فقط على **extracts the SVG** بل يوضح لك أيضًا كيفية **export svg file** باستخدام **svg save options** الدقيقة، مع ضمان بقاء **svg external css** خارجيًا و**inline svg markup** دون تعديل.

## ما ستتعلمه

- كيفية تحميل مستند HTML من القرص.
- كيفية تحديد العنصر `<svg>` الأول (أو أي عنصر تحتاجه).
- كيفية إنشاء `SVGDocument` من **inline svg markup**.
- أي **svg save options** تُعطّل تضمين CSS بحيث تبقى الأنماط في ملفات خارجية.
- الخطوات الدقيقة لـ **export svg file** إلى المجلد الذي ترغب به.
- نصائح للتعامل مع SVGs متعددة، الحفاظ على المعرفات (IDs)، وحل المشكلات الشائعة.

لا توجد تبعيات ثقيلة، فقط كائنات البرمجة المدمجة التي تحصل عليها مع Adobe InDesign (أو أي بيئة توفر `HTMLDocument` و `SVGDocument` و `SVGSaveOptions`). افتح محرر نصوص، انسخ الشيفرة، وستكون جاهزًا.

![Extract SVG from HTML workflow](extract-svg-workflow.png){alt="استخراج SVG من تدفق عمل HTML"}

## المتطلبات المسبقة

- Adobe InDesign (أو مضيف ExtendScript متوافق) الإصدار 2022 أو أحدث.
- إلمام أساسي بصياغة JavaScript/ExtendScript.
- ملف HTML يحتوي على عنصر `<svg>` واحد على الأقل تريد استخراجها.

إذا استوفيت هذه المتطلبات الثلاثة، يمكنك تخطي قسم “الإعداد” والانتقال مباشرة إلى الشيفرة.

---

## استخراج SVG من HTML – الخطوة 1: تحميل مستند HTML

أولاً وقبل كل شيء: تحتاج إلى مرجع للصفحة HTML التي تحتوي على SVG. يأخذ مُنشئ `HTMLDocument` مسار الملف ويقوم بتحليل العلامات لك.

```javascript
// Step 1: Load the HTML document
var htmlPath = File("YOUR_DIRECTORY/page.html"); // adjust the path
var htmlDoc = new HTMLDocument(htmlPath);
```

> **لماذا هذا مهم:** تحميل المستند يمنحك نموذج كائن شبيه بـ DOM، بحيث يمكنك الاستعلام عن العناصر كما تفعل في المتصفح. بدون ذلك، ستضطر إلى استخدام عمليات بحث نصية هشة.

---

## استخراج SVG من HTML – الخطوة 2: تحديد العنصر `<svg>` الأول

الآن بعد أن أصبح الـ DOM جاهزًا، لنلتقط أول عقدة SVG. إذا كنت تحتاج إلى عقدة مختلفة، فقط غيّر الفهرس أو استخدم محددًا أكثر تحديدًا.

```javascript
// Step 2: Locate the first <svg> element
var svgElements = htmlDoc.getElementsByTagName("svg");
if (svgElements.length === 0) {
    throw new Error("No <svg> elements found in the HTML file.");
}
var svgElement = svgElements[0]; // you could loop through all if needed
```

> **نصيحة احترافية:** `svgElements` مجموعة تشبه المصفوفة، لذا يمكنك التكرار عليها لـ **export multiple svg files** في مرحلة لاحقة.

---

## العلامة المضمنة لـ SVG – الخطوة 3: إنشاء SVGDocument

خاصية `outerHTML` تُعيد العلامة الكاملة للعنصر `<svg>`، بما في ذلك أي سمات مضمنة. تمرير تلك السلسلة إلى `SVGDocument` يمنحك كائن SVG كامل يمكنك التلاعب به أو حفظه.

```javascript
// Step 3: Create an SVGDocument from the extracted markup
var svgMarkup = svgElement.outerHTML; // this is the inline svg markup
var svgDoc = new SVGDocument(svgMarkup);
```

> **لماذا نستخدم `outerHTML`:** إنها تلتقط العنصر *وأطفاله*، مع الحفاظ على التدرجات، الفلاتر، وأي كتل `<style>` مدمجة قد تكون جزءًا من **inline svg markup**.

---

## خيارات حفظ SVG – الخطوة 4: تكوين إعدادات التصدير

بشكل افتراضي، يدمج InDesign CSS مباشرةً داخل SVG، مما قد يزيد حجم الملف ويعطل خطوط أنابيب الأنماط الخارجية. للحفاظ على ورقة الأنماط منفصلة، قم بتبديل علامة `embedCSS`.

```javascript
// Step 4: Configure SVG save options (disable CSS embedding)
var svgOptions = new SVGSaveOptions();
svgOptions.embedCSS = false;      // ensures svg external css stays external
svgOptions.embedImages = false;   // optional: keep images as links
svgOptions.fontType = SVGFontType.OUTLINE; // optional: outline fonts
```

> **ماذا يعني “svg external css”:** عندما تكون `embedCSS` مساوية لـ `false`، تُحذف أي وسوم `<style>`، ويشير SVG إلى ملف CSS منفصل (إن وجد). هذا مثالي لتدفقات العمل التي تعتمد على ورقة أنماط مشتركة عبر العديد من أصول SVG.

---

## تصدير ملف SVG – الخطوة 5: حفظ SVG المستخرج

أخيرًا، اكتب الـ SVG إلى القرص. طريقة `save` تحترم الخيارات التي حددناها أعلاه، وتنتج ملفًا نظيفًا جاهزًا للويب أو للمعالجة الإضافية.

```javascript
// Step 5: Save the extracted SVG to a separate file
var outputPath = File("YOUR_DIRECTORY/extracted.svg");
svgDoc.save(outputPath, svgOptions);
```

**النتيجة المتوقعة:** يظهر ملف باسم `extracted.svg` في `YOUR_DIRECTORY`. افتحه في المتصفح – يجب أن ترى الرسمة معروضة تمامًا كما ظهرت في HTML الأصلي، لكن الآن يتم تحميل جميع CSS من مصادر خارجية.

---

## التعامل مع SVGs متعددة (اختياري)

إذا كانت صفحة HTML الخاصة بك تحتوي على عدة SVGs، غلف منطق التحديد‑والحفظ داخل حلقة:

```javascript
for (var i = 0; i < svgElements.length; i++) {
    var element = svgElements[i];
    var doc = new SVGDocument(element.outerHTML);
    var outFile = File("YOUR_DIRECTORY/svg_" + i + ".svg");
    doc.save(outFile, svgOptions);
}
```

هذه التعديلة الصغيرة تسمح لك بـ **export svg file** على نطاق واسع دون الحاجة لإعادة كتابة أي شفرة.

---

## المشكلات الشائعة وكيفية تجنبها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| SVG يظهر فارغًا في المتصفح | تم تضمين CSS ثم تم إزالته، مما فقد قواعد الأنماط | تأكد من أن `svgOptions.embedCSS = false` فقط عندما تكون لديك ورقة أنماط خارجية جاهزة. |
| النص يبدو متعرجًا | لم يتم تحويل الخطوط إلى خطوط محددة (outline) | اضبط `svgOptions.fontType = SVGFontType.OUTLINE`. |
| الصور مفقودة | `embedImages` مُعطى true لكن الصور خارجية | غيّر `svgOptions.embedImages = false` واحتفظ بملفات الصور بجانب SVG. |
| تتعارض المعرفات (IDs) عند دمج SVGs متعددة | كل SVG احتفظ بالمعرفات الأصلية | قم بمعالجة لاحقة باستخدام سكريبت إعادة تسمية بسيط أو استخدم خيار “unique IDs” في InDesign إذا كان متاحًا. |

---

## السكريبت الكامل – جاهز للنسخ واللصق

فيما يلي السكريبت بالكامل، جاهز للإدراج في نافذة ExtendScript Toolkit وتشغيله. استبدل `YOUR_DIRECTORY` بالمجلد الذي يحتوي على ملف HTML الخاص بك.



## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [حفظ مستند SVG في Aspose.HTML للـ Java](/html/english/java/saving-html-documents/save-svg-document/)
- [كيفية تحويل SVG إلى XPS باستخدام Aspose.HTML للـ Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)
- [إنشاء PDF من SVG باستخدام Aspose.HTML للـ Java](/html/hindi/java/conversion-html-to-other-formats/convert-svg-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
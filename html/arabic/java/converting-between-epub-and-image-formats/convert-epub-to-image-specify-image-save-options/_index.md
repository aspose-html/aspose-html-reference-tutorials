---
date: 2025-12-25
description: تعلم كيفية تحويل ملفات EPUB إلى صور باستخدام Aspose.HTML للغة Java وتعيين
  حجم صفحة مخصص. يغطي هذا الدليل خطوة بخطوة المتطلبات المسبقة، واستيراد الحزم، وعملية
  التحويل.
linktitle: Specifying Image Save Options for EPUB to Image Conversion
second_title: Java HTML Processing with Aspose.HTML
title: تحويل EPUB إلى صورة باستخدام Aspose.HTML للـ Java – تعيين حجم صفحة مخصص
url: /ar/java/converting-between-epub-and-image-formats/convert-epub-to-image-specify-image-save-options/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل EPUB إلى صورة باستخدام Aspose.HTML for Java – تعيين حجم صفحة مخصص

## إجابات سريعة
- **ماذا يعني “تعيين حجم صفحة مخصص”?** يتيح لك تحديد العرض والارتفاع لكل صفحة صورة ناتجة.  
- **هل يمكنني تغيير لون خلفية الصورة؟** نعم، يمكنك تحديد أي لون باستخدام `ImageSaveOptions`.  
- **ما الصيغ المدعومة؟** JPEG، PNG، GIF، وأكثر عبر `ImageFormat`.  
- **هل أحتاج إلى ترخيص؟** نسخة تجريبية مجانية تكفي للاختبار؛ الترخيص التجاري مطلوب للإنتاج.  
- **ما نسخة Java المطلوبة؟** Java 1.7 أو أحدث مدعومة بالكامل.

## ما هو “تعيين حجم صفحة مخصص” في تحويل EPUB إلى صورة؟
تعيين حجم صفحة مخصص يعني أنك تتحكم في أبعاد الصورة المُعالجة (مثال: 3000 × 1000 بكسل). هذا مفيد عندما تحتاج إلى لقطات شاشة عالية الدقة للكتب الإلكترونية أو عندما تريد أن يتطابق الناتج مع تخطيط معين.

## لماذا تعيين حجم صفحة مخصص وتغيير لون خلفية الصورة؟
أحجام الصفحات المخصصة تمنحك مرونة لاستهداف شاشات مختلفة—شاشات الهواتف المحمولة، ملفات PDF جاهزة للطباعة، أو صور مصغرة للويب. تغيير لون الخلفية يساعدك على مطابقة العلامة التجارية أو تحسين قابلية القراءة للصور التي تحتوي على عناصر شفافة.

## المتطلبات المسبقة

قبل أن نبدأ رحلتنا في **تحويل epub إلى صورة**, تأكد من وجود ما يلي:

1. **بيئة Java** – مجموعة تطوير Java مثبتة على جهازك. إذا لم يكن لديك Java بعد, يمكنك تنزيله من [هنا](https://www.java.com).
2. **Aspose.HTML for Java** – مكتبة Aspose.HTML for Java. احصل على أحدث إصدار من [صفحة Aspose.HTML for Java](https://releases.aspose.com/html/java/).

## استيراد الحزم

للعمل مع Aspose.HTML for Java, استورد المساحات الاسمية المطلوبة:

```java
// Import the required Aspose.HTML for Java packages
import com.aspose.html.saving.ImageSaveOptions;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.drawing.Page;
import com.aspose.html.drawing.Size;
import com.aspose.html.drawing.Length;
import com.aspose.html.drawing.Color;
import com.aspose.html.converters.Converter;
import java.io.FileInputStream;
```

## دليل خطوة بخطوة

### الخطوة 1: فتح ملف EPUB موجود للقراءة

```java
try (FileInputStream fileInputStream = new FileInputStream("input.epub")) {
```

هنا نقوم بفتح ملف EPUB المصدر. استبدل `"input.epub"` بالمسار إلى ملف الكتاب الإلكتروني الخاص بك.

### الخطوة 2: تهيئة ImageSaveOptions بالإعدادات المخصصة (تعيين حجم صفحة مخصص وتغيير لون خلفية الصورة)

```java
ImageSaveOptions options = new ImageSaveOptions(ImageFormat.Jpeg);
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
Size size = new Size(
    Length.fromPixels(3000),
    Length.fromPixels(1000)
);
anyPage.setSize(size);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

في هذا الجزء نقوم **بتعيين حجم صفحة مخصص** إلى 3000 × 1000 بكسل ونغير الخلفية إلى AliceBlue. يمكنك تعديل `size` أو `Color` لتناسب مشروعك (مثال: `Color.getWhite()` لخلفية بيضاء بسيطة).

### الخطوة 3: تحويل EPUB إلى صورة

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    "output.jpg"
);
```

هذا السطر ينفذ التحويل الفعلي. ملف الإخراج (`"output.jpg"`) سيحتوي على الصورة المعالجة بالأبعاد والخلفية التي حددتها. يمكنك أيضًا تغيير امتداد الملف إلى `.png` إذا كنت تفضل **java convert epub png**.

### الخطوة 4: إغلاق الموارد (مُعالجة تلقائيًا)

تعليمات `try‑with‑resources` تغلق تلقائيًا `FileInputStream`, مما يضمن عدم ترك مقبض ملف مفتوح.

## حالات الاستخدام الشائعة
- **إنشاء صور مصغرة** لمكتبات الكتب الإلكترونية.  
- **إنشاء لقطات شاشة عالية الدقة** للتوثيق أو التسويق.  
- **معالجة دفعات** لمجموعات كبيرة من ملفات EPUB إلى موارد PNG/JPEG للمعارض على الويب.

## نصائح وأفضل الممارسات
- **نصيحة احترافية:** استخدم `Length.fromInches()` أو `Length.fromCentimeters()` إذا كنت تفضل الوحدات الفيزيائية على البكسل.  
- **نصيحة أداء:** للـ EPUB الكبيرة, فكر في زيادة حجم ذاكرة JVM (`-Xmx2g`) لتجنب ضغط الذاكرة.  
- **معالجة الأخطاء:** غلف استدعاء التحويل داخل كتلة `try‑catch` لالتقاط `IOException` أو `AsposeException`.

## الأسئلة المتكررة

**س: هل يمكنني تحويل ملفات EPUB إلى صيغ صور أخرى؟**  
ج: نعم, يمكنك تحديد صيغ مثل PNG أو GIF عن طريق تغيير `ImageFormat.Jpeg` إلى `ImageFormat.Png` أو `ImageFormat.Gif`.

**س: هل يدعم Aspose.HTML for Java صيغة EPUB3؟**  
ج: بالتأكيد. المكتبة تدعم بالكامل EPUB3, مما يتيح لك العمل بأحدث معايير الكتب الإلكترونية.

**س: كيف يمكنني معالجة الأخطاء أثناء عملية التحويل؟**  
ج: نفّذ كتل `try‑catch` حول كود التحويل لالتقاط وتسجيل الاستثناءات, مما يضمن بقاء تطبيقك قويًا.

**س: هل يمكنني تخصيص حجم الصورة وجودتها؟**  
ج: نعم, عدّل كائن `Size` للأبعاد واستخدم `options.setQuality(int)` للتحكم في جودة ضغط JPEG.

**س: هل Aspose.HTML for Java متوافق مع جميع إصدارات Java؟**  
ج: المكتبة تعمل مع Java 1.7 وما بعده, وتغطي مجموعة واسعة من بيئات التطوير.

---

**آخر تحديث:** 2025-12-25  
**تم الاختبار مع:** Aspose.HTML for Java 24.10  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
---
date: 2026-03-13
description: تعلم كيفية تحويل ملفات EPUB إلى صور باستخدام Aspose.HTML للغة Java، وضبط
  حجم الصفحة المخصص، وتغيير لون خلفية الصورة للحصول على أفضل النتائج.
linktitle: Specifying Image Save Options for EPUB to Image Conversion
second_title: Java HTML Processing with Aspose.HTML
title: تحويل EPUB إلى صورة باستخدام Aspose.HTML للغة Java – تعيين حجم صفحة مخصص
url: /ar/java/converting-between-epub-and-image-formats/convert-epub-to-image-specify-image-save-options/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل EPUB إلى صورة باستخدام Aspose.HTML للـ Java – تعيين حجم صفحة مخصص

في عالم تطوير الويب المتطور باستمرار، يعتبر Aspose.HTML للـ Java أداة قوية، وسنركز اليوم على **كيفية تعيين حجم صفحة مخصص** عند تحويل EPUB إلى صورة. سواء كنت تبني مكتبة رقمية، أو تولد صورًا مصغرة، أو تنشئ لقطات شاشة عالية الدقة، فإن إتقان هذا الإعداد يتيح لك **تحويل EPUB إلى صورة** تتطابق مع متطلبات التخطيط الدقيقة الخاصة بك.

## إجابات سريعة
- **ماذا يعني “تعيين حجم صفحة مخصص”؟** يسمح لك بتحديد عرض وارتفاع كل صفحة صورة ناتجة.  
- **هل يمكنني تغيير لون خلفية الصورة؟** نعم، يمكنك تحديد أي لون باستخدام `ImageSaveOptions`.  
- **ما الصيغ المدعومة؟** JPEG، PNG، GIF، وأكثر عبر `ImageFormat`.  
- **هل أحتاج إلى ترخيص؟** الإصدار التجريبي المجاني يعمل للاختبار؛ يتطلب الترخيص التجاري للإنتاج.  
- **ما نسخة Java المطلوبة؟** Java 1.7 أو أحدث مدعومة بالكامل.

## ما هو “تعيين حجم صفحة مخصص” في تحويل EPUB إلى صورة؟
تعيين حجم صفحة مخصص يعني أنك تتحكم في أبعاد الصورة المرسومة (مثلاً 3000 × 1000 بكسل). هذا مفيد عندما تحتاج إلى لقطات شاشة عالية الدقة للكتب الإلكترونية أو عندما تريد أن يتطابق الناتج مع تخطيط محدد.

## لماذا تعيين حجم صفحة مخصص وتغيير لون خلفية الصورة؟
تمنحك أحجام الصفحات المخصصة مرونة لأهداف عرض مختلفة—شاشات الهواتف المحمولة، ملفات PDF جاهزة للطباعة، أو صور مصغرة للويب. يساعد تغيير لون الخلفية في مطابقة العلامة التجارية أو تحسين قابلية القراءة للصور التي تحتوي على عناصر شفافة.

## المتطلبات المسبقة

قبل أن نبدأ رحلتنا في **تحويل epub إلى صورة**، تأكد من أن لديك ما يلي:

1. **بيئة Java** – مجموعة تطوير Java مثبتة على جهازك. إذا لم يكن لديك Java بعد، يمكنك تنزيله من [هنا](https://www.java.com).
2. **Aspose.HTML للـ Java** – مكتبة Aspose.HTML للـ Java. احصل على أحدث إصدار من [صفحة Aspose.HTML للـ Java](https://releases.aspose.com/html/java/).

## استيراد الحزم

للعمل مع Aspose.HTML للـ Java، استورد المساحات الاسمية المطلوبة:

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

هنا نفتح ملف EPUB المصدر. استبدل `"input.epub"` بالمسار إلى ملف الكتاب الإلكتروني الخاص بك.

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

في هذا الجزء نـ **نحدد حجم صفحة مخصص** إلى 3000 × 1000 بكسل ونغير الخلفية إلى AliceBlue. لا تتردد في تعديل `size` أو `Color` لتناسب مشروعك (مثلاً، `Color.getWhite()` لخلفية بيضاء صافية).

### الخطوة 3: تحويل EPUB إلى صورة

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    "output.jpg"
);
```

هذا السطر ينفذ التحويل الفعلي. ملف الإخراج (`"output.jpg"`) سيحتوي على الصورة المرسومة بالأبعاد والخلفية التي حددتها. يمكنك أيضًا تغيير امتداد الملف إلى `.png` إذا كنت تفضل **java convert epub png**. المكتبة تدعم كل من **صيغة الصورة JPEG** و **صيغة الصورة PNG**، مما يمنحك مرونة في المعالجة اللاحقة.

### الخطوة 4: إغلاق الموارد (مُعالجة تلقائيًا)

تعليمات `try‑with‑resources` تغلق تلقائيًا `FileInputStream`، مما يضمن عدم ترك مقبض ملفات مفتوح.

## حالات الاستخدام الشائعة
- **إنشاء صور مصغرة** لمكتبات الكتب الإلكترونية.  
- **إنشاء لقطات شاشة عالية الدقة** للتوثيق أو التسويق.  
- **معالجة دفعة** لمجموعات كبيرة من ملفات EPUB إلى موارد PNG/JPEG للمعارض على الويب.  
- **أتمتة استخراج الصور** لأدوات الوصول التي تحتاج إلى معاينات بصرية للكتب الإلكترونية.  

## نصائح وأفضل الممارسات
- **نصيحة احترافية:** استخدم `Length.fromInches()` أو `Length.fromCentimeters()` إذا كنت تفضل الوحدات الفيزيائية على البكسل.  
- **نصيحة الأداء:** بالنسبة لملفات EPUB الكبيرة، فكر في زيادة حجم الذاكرة المخصصة للـ JVM (`-Xmx2g`) لتجنب ضغط الذاكرة.  
- **معالجة الأخطاء:** غلف استدعاء التحويل داخل كتلة `try‑catch` لالتقاط `IOException` أو `AsposeException`.  
- **ضبط الجودة:** عدل `options.setQuality(90)` لضبط ضغط JPEG بدقة دون فقد ملحوظ.  

## المشكلات الشائعة والحلول
- **أخطاء نفاد الذاكرة:** زيادة حجم الذاكرة أو معالجة EPUB على أجزاء أصغر عن طريق رسم الصفحات الفردية.  
- **خلفية فارغة:** تأكد من تعيين لون خلفية؛ قد تظهر الخلفيات الشفافة باللون الأسود في بعض المشاهدين.  
- **أبعاد صورة غير متوقعة:** تحقق من أن كائن `Size` يعكس القيم البكسلية الدقيقة التي تحتاجها؛ تذكر أن إعدادات DPI لا تؤثر على حجم البكسل.  
- **ميزات EPUB غير مدعومة:** Aspose.HTML يتعامل مع EPUB3 بالكامل، لكن قد تحتاج الخطوط المخصصة إلى تضمين أو الإشارة إليها بشكل صحيح.  

## الأسئلة المتكررة

**س: هل يمكنني تحويل ملفات EPUB إلى صيغ صور أخرى؟**  
ج: نعم، يمكنك تحديد صيغ مثل PNG أو GIF عن طريق تغيير `ImageFormat.Jpeg` إلى `ImageFormat.Png` أو `ImageFormat.Gif`.

**س: هل يدعم Aspose.HTML للـ Java EPUB3؟**  
ج: بالتأكيد. المكتبة تدعم EPUB3 بالكامل، مما يتيح لك العمل مع أحدث معايير الكتب الإلكترونية.

**س: كيف يمكنني معالجة الأخطاء أثناء عملية التحويل؟**  
ج: نفّذ كتل `try‑catch` حول كود التحويل لالتقاط وتسجيل الاستثناءات، مما يضمن بقاء تطبيقك قويًا.

**س: هل يمكنني تخصيص حجم الصورة وجودتها؟**  
ج: نعم، عدل كائن `Size` للأبعاد واستخدم `options.setQuality(int)` للتحكم في جودة ضغط JPEG.

**س: هل Aspose.HTML للـ Java متوافق مع جميع إصدارات Java؟**  
ج: المكتبة تعمل مع Java 1.7 وما بعده، مما يغطي مجموعة واسعة من بيئات التطوير.  

## الخلاصة

باتباعك هذا الدليل، أصبحت الآن تعرف كيفية **تحويل EPUB إلى صورة** مع **تعيين حجم صفحة مخصص** و**تغيير لون خلفية الصورة** باستخدام Aspose.HTML للـ Java. تتيح لك هذه الإمكانيات إنتاج صور ذات حجم مثالي ومُعلمة بالعلامة التجارية لأي سير عمل لاحق—سواء كان معرضًا للصور المصغرة، أو كتيبًا تسويقيًا، أو خدمة معاينة كتب إلكترونية مؤتمتة. لا تتردد في تجربة أبعاد وألوان وصيغ إخراج مختلفة لتتناسب مع احتياجاتك الخاصة.

---

**آخر تحديث:** 2026-03-13  
**تم الاختبار مع:** Aspose.HTML for Java 24.10  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
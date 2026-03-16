---
date: 2025-12-30
description: 'تعلم كيفية تعيين حجم صفحة مخصص واستخدام خيارات حفظ الصورة لتحويل EPUB
  إلى صورة باستخدام Aspose.HTML للغة Java. #JavaDevelopment #WebDevelopment #DocumentConversion'
linktitle: Specifying Image Save Options for EPUB to Image Conversion
second_title: Java HTML Processing with Aspose.HTML
title: حجم صفحة مخصص – تحديد خيارات حفظ الصورة لتحويل EPUB إلى صورة
url: /ar/java/converting-epub-to-pdf/convert-epub-to-image-specify-image-save-options/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحديد خيارات حفظ الصورة لتحويل EPUB إلى صورة

في عالم تطوير الويب ومعالجة المستندات، يبرز Aspose.HTML for Java كأداة قوية. **تعيين حجم صفحة مخصص** يمنحك تحكمًا دقيقًا في أبعاد الصورة الناتجة، وهو مفيد بشكل خاص عندما تحتاج إلى مطابقة متطلبات تخطيط معينة. في هذا الدليل الشامل، سنستعرض كيفية تكوين خيارات حفظ الصورة—بما في ذلك حجم الصفحة المخصص ولون الخلفية—لتحويل ملف EPUB إلى تنسيق صورة.

## إجابات سريعة
- **ماذا يؤثر “حجم الصفحة المخصص”؟** يحدد عرض وارتفاع الصورة المولدة بالبكسل.  
- **إلى أي تنسيق يمكنني تحويل EPUB؟** أي تنسيق صورة يدعمه `ImageSaveOptions`، مثل JPEG أو PNG أو BMP.  
- **كيف أضبط لون الخلفية؟** استخدم `options.setBackgroundColor(Color.getAliceBlue())` (أو أي `Color` آخر).  
- **هل أحتاج إلى ترخيص للتطوير؟** النسخة التجريبية المجانية تكفي للتقييم؛ الترخيص التجاري مطلوب للإنتاج.  
- **ما نسخة Java المطلوبة؟** Java 8 أو أعلى مع مكتبة Aspose.HTML for Java.

## ما هو حجم الصفحة المخصص؟
**حجم الصفحة المخصص** يحدد الأبعاد الدقيقة بالبكسل للصفحة التي يتم عرضها قبل حفظها كصورة. من خلال تحديد حجم مخصص، تتجنب الأبعاد الافتراضية ويمكنك تعديل الناتج ليتناسب مع مكونات الواجهة، مواصفات الطباعة، أو أي متطلبات أخرى لاحقة.

## لماذا نستخدم خيارات حفظ الصورة؟
`ImageSaveOptions` يتيح لك ضبط عملية التحويل بدقة: اختيار تنسيق الصورة، تعيين حجم صفحة مخصص، تطبيق لون خلفية، والتحكم في معلمات العرض الأخرى. هذه المرونة تضمن أن الصورة الناتجة تلبي التوقعات البصرية والتقنية.

## المتطلبات المسبقة

قبل الغوص في الكود، تأكد من وجود ما يلي:

1. **بيئة تطوير Java** – JDK 8 أو أحدث مثبتة.  
2. **Aspose.HTML for Java** – حمّل المكتبة من الموقع الرسمي [هنا](https://releases.aspose.com/html/java/).  
3. **محرر كود** – IntelliJ IDEA، Eclipse، VS Code، أو أي بيئة تطوير تفضّلها.  
4. **معرفة أساسية بـ Java** – إلمام بصياغة Java وإعداد المشروع.  
5. **حماس** – جاهز لاستكشاف حجم الصفحة المخصص وخيارات حفظ الصورة الأخرى.

الآن بعد أن أصبحت جاهزًا، لننتقل إلى التنفيذ.

## استيراد الحزم

أولاً، استورد الفئات المطلوبة للعرض والتحويل.

### الخطوة 1: استيراد فئات Aspose.HTML

```java
import com.aspose.html.saving.ImageSaveOptions;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.drawing.Page;
import com.aspose.html.drawing.Size;
import com.aspose.html.drawing.Length;
import com.aspose.html.drawing.Color;
import com.aspose.html.converters.Converter;
```

تمنحك هذه الاستيرادات الوصول إلى `ImageSaveOptions`، كائنات تخطيط الصفحة، وأداة `Converter`.

## تحليل المثال: تحويل EPUB إلى صورة

فيما يلي شرح خطوة بخطوة لتحويل ملف EPUB مع تطبيق **حجم صفحة مخصص** ولون خلفية.

### الخطوة 2: فتح ملف EPUB

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
```

يقوم `FileInputStream` بقراءة ملف EPUB المصدر. استبدل `"input.epub"` بالمسار إلى ملفك الخاص.

### الخطوة 3: تهيئة ImageSaveOptions بحجم صفحة مخصص

```java
ImageSaveOptions options = new ImageSaveOptions(ImageFormat.Jpeg);
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
Size size = new Size(Length.fromPixels(3000), Length.fromPixels(1000));
anyPage.setSize(size);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

- **حجم الصفحة المخصص**: يتم إنشاء `Size` بعرض 3000 بكسل وارتفاع 1000 بكسل. عدّل هذه القيم لتتناسب مع احتياجات التخطيط لديك.  
- **لون الخلفية**: `Color.getAliceBlue()` يضبط خلفية زرقاء فاتحة؛ يمكنك اختيار أي `Color` تفضله.

### الخطوة 4: تحويل EPUB إلى صورة

```java
Converter.convertEPUB(fileInputStream, options, Resources.output("output.jpg"));
```

تقوم طريقة `convertEPUB` بإجراء التحويل باستخدام `options` المكوّنة. يتم حفظ النتيجة كـ `output.jpg`.

> **نصيحة احترافية:** إذا كنت تحتاج إخراج PNG، أنشئ `ImageSaveOptions` باستخدام `ImageFormat.Png` بدلاً من `ImageFormat.Jpeg`.

تهانينا! لقد نجحت في تحويل ملف EPUB إلى صورة مع التحكم في أبعاد الصفحة ولون الخلفية.

## المشكلات الشائعة والحلول

| المشكلة | السبب | الحل |
|-------|--------|-----|
| الصورة الناتجة مقطوعة | حجم الصفحة المخصص أصغر من المحتوى | زيادة العرض/الارتفاع في `Size` أو استخدام `options.setFitToPage(true)`. |
| الخلفية تظهر باللون الأسود | لم يتم تعيين اللون أو تنسيق غير مدعوم | تأكد من استدعاء `options.setBackgroundColor(...)` قبل التحويل. |
| فشل التحويل بـ `NullPointerException` | ملف `Resources.input` مفقود | تحقق من المسار وتأكد من وجود ملف EPUB. |

## الأسئلة المتكررة (FAQs)

### 1. أين يمكنني العثور على وثائق Aspose.HTML for Java؟

يمكنك الوصول إلى الوثائق [هنا](https://reference.aspose.com/html/java/). توفر معلومات شاملة وأمثلة لمساعدتك على البدء.

### 2. هل هناك نسخة تجريبية مجانية من Aspose.HTML for Java؟

نعم، يمكنك تنزيل نسخة تجريبية مجانية [هنا](https://releases.aspose.com/). تتيح لك استكشاف قدرات المكتبة قبل الشراء.

### 3. كيف يمكنني الحصول على ترخيص مؤقت لـ Aspose.HTML for Java؟

إذا كنت بحاجة إلى ترخيص مؤقت، يمكنك الحصول عليه [هنا](https://purchase.aspose.com/temporary-license/).

### 4. هل يمكن لـ Aspose.HTML for Java معالجة تحويلات مستندات أخرى؟

نعم، يدعم Aspose.HTML for Java تحويلات متعددة، بما في ذلك HTML → PDF، HTML → صورة، وأكثر.

### 5. هل Aspose.HTML for Java مناسب للمبتدئين والمطورين ذوي الخبرة؟

بالطبع! يمكن للمبتدئين البدء بأمثلة بسيطة، بينما يمكن للمستخدمين المتقدمين الاستفادة من كامل API لإنشاء تدفقات عمل معقدة.

**أسئلة وإجابات إضافية**

**س: هل يمكنني تحويل صفحات EPUB متعددة إلى صور منفصلة؟**  
ج: نعم. استخدم `options.setPageSetup(pageSetup)` مع حلقة تمر على كل فهرس صفحة، واستدعِ `Converter.convertEPUB` لكل صفحة.

**س: كيف أغيّر جودة الصورة لإخراج JPEG؟**  
ج: عيّن `options.setQuality(90)` (القيمة من 0‑100) قبل تنفيذ التحويل.

**س: هل تدعم المكتبة خلفيات شفافة؟**  
ج: لإخراج PNG، يمكنك استخدام `options.setBackgroundColor(Color.getTransparent())`.

## الخلاصة

يوفر Aspose.HTML for Java تحكمًا دقيقًا في تحويل EPUB إلى صورة. من خلال تكوين **حجم صفحة مخصص**، لون الخلفية، وغيرها من إعدادات `ImageSaveOptions`، يمكنك إنتاج صور تتطابق تمامًا مع المتطلبات البصرية لمشروعك. لا تتردد في تجربة صيغ وأحجام صفحات مختلفة، واستكشاف قدرات Aspose.HTML for Java الأوسع في تطبيقاتك.

هل لديك أسئلة أو تحتاج إلى مساعدة؟ تواصل مع مجتمع [Aspose.HTML](https://forum.aspose.com/) للحصول على الدعم.

---

**آخر تحديث:** 2025-12-30  
**تم الاختبار مع:** Aspose.HTML for Java 24.12  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
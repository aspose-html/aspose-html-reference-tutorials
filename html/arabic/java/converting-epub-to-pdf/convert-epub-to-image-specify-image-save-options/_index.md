---
date: 2026-03-24
description: 'تعلم كيفية تعيين لون خلفية الصورة، حجم الصفحة المخصص، وتحويل EPUB إلى
  صورة باستخدام Aspose.HTML للغة Java. #JavaDevelopment #WebDevelopment #DocumentConversion'
linktitle: Specifying Image Save Options for EPUB to Image Conversion
second_title: Java HTML Processing with Aspose.HTML
title: تعيين لون خلفية الصورة لتحويل EPUB إلى صورة
url: /ar/java/converting-epub-to-pdf/convert-epub-to-image-specify-image-save-options/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعيين لون خلفية الصورة لتحويل EPUB إلى صورة

في سير عمل الويب والوثائق الحديثة، **Aspose.HTML for Java** يمنحك القدرة على تحويل الكتب الإلكترونية مثل EPUB إلى صور نقطية مع التحكم الكامل في المخرجات البصرية. باستخدام خيار **set image background color** مع **custom page size**، يمكنك إنتاج صور تتطابق تمامًا مع مكونات واجهة المستخدم، تخطيطات الطباعة، أو أي متطلبات معالجة لاحقة. في هذا الدليل سنستعرض العملية بالكامل—من المتطلبات المسبقة إلى التحويل النهائي—حتى تتمكن من **convert EPUB to image** بثقة.

## إجابات سريعة
- **ماذا يؤثر “custom page size”؟** يحدد عرض وارتفاع الصورة المولدة بالبكسل.  
- **إلى أي صيغة يمكنني تحويل EPUB؟** أي صيغة صورة يدعمها `ImageSaveOptions`، مثل JPEG أو PNG أو BMP.  
- **كيف أضع لون خلفية للصورة؟** استخدم `options.setBackgroundColor(Color.getAliceBlue())` (أو أي `Color` آخر).  
- **هل أحتاج رخصة للتطوير؟** النسخة التجريبية مجانية للتقييم؛ الرخصة التجارية مطلوبة للإنتاج.  
- **ما نسخة Java المطلوبة؟** Java 8 أو أعلى مع مكتبة Aspose.HTML for Java.

## ما هو “set image background color”؟
تحديد لون خلفية الصورة يخبر محرك العرض أي لون يملأ القماش قبل رسم محتوى الصفحة. يكون هذا مفيدًا خاصةً عندما يحتوي EPUB الأصلي على عناصر شفافة أو عندما تريد خلفية موحدة لجميع الصفحات.

## كيف أضع لون خلفية للصورة وحجم صفحة مخصص في Java؟
فيما يلي خطوات يجب اتباعها. كل خطوة تتضمن شرحًا مختصرًا يليه المقتطف البرمجي الدقيق الذي ستستخدمه (الكود يبقى كما هو من الدرس الأصلي).

### المتطلبات المسبقة
قبل البدء، تأكد من وجود:

1. **بيئة تطوير Java** – JDK 8 أو أحدث مثبتة.  
2. **Aspose.HTML for Java** – حمّل المكتبة من الموقع الرسمي [here](https://releases.aspose.com/html/java/).  
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

هذه الاستيرادات تمنحك الوصول إلى `ImageSaveOptions`، كائنات تخطيط الصفحة، وأداة `Converter`.

## تحليل المثال: تحويل EPUB إلى صورة

فيما يلي شرح خطوة‑بخطوة **كيفية تحويل EPUB** مع تطبيق **custom page size** وخيار **set image background color**.

### الخطوة 2: فتح ملف EPUB

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
```

`FileInputStream` يقرأ ملف EPUB المصدر. استبدل `"input.epub"` بالمسار إلى ملفك الخاص.

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

- **حجم صفحة مخصص**: يتم إنشاء `Size` بعرض 3000 بكسل وارتفاع 1000 بكسل. عدّل هذه القيم لتناسب احتياجات تخطيطك.  
- **تعيين لون خلفية الصورة**: `Color.getAliceBlue()` يملأ القماش بخلفية زرقاء فاتحة؛ يمكنك استبداله بأي `Color` تفضله، مثل `Color.getTransparent()` للشفافية في PNG.  

### الخطوة 4: تحويل EPUB إلى صورة

```java
Converter.convertEPUB(fileInputStream, options, Resources.output("output.jpg"));
```

طريقة `convertEPUB` تقوم بالتحويل باستخدام `options` المُكوَّنة. النتيجة تُحفظ كـ `output.jpg`.

> **نصيحة محترف:** إذا كنت تحتاج **epub to png conversion**، أنشئ `ImageSaveOptions` باستخدام `ImageFormat.Png` بدلاً من `ImageFormat.Jpeg`.

تهانينا! لقد نجحت في **convert epub to image** مع التحكم في أبعاد الصفحة ولون الخلفية.

## كيفية تعيين حجم الصفحة (custom page size java) – نظرة أعمق
إذا كنت تحتاج حجم صفحة مختلف لكل EPUB، يمكنك حساب الأبعاد ديناميكيًا بناءً على CSS أو البيانات الوصفية للمحتوى. يمكن إعادة استخدام كائن `PageSetup` عبر تحويلات متعددة؛ فقط عدّل `Size` قبل كل استدعاء لـ `Converter.convertEPUB`.

## المشكلات الشائعة والحلول

| المشكلة | السبب | الحل |
|-------|--------|-----|
| الصورة الناتجة مقصوصة | حجم الصفحة المخصص أصغر من المحتوى | زيادة العرض/الارتفاع في `Size` أو تفعيل `options.setFitToPage(true)`. |
| الخلفية تظهر باللون الأسود | لم يتم تعيين اللون أو الصيغة غير مدعومة | تأكد من استدعاء `options.setBackgroundColor(...)` قبل التحويل. |
| فشل التحويل بـ `NullPointerException` | ملف `Resources.input` مفقود | تحقق من المسار وتأكد من وجود ملف EPUB. |

## الأسئلة المتكررة (FAQs)

### 1. أين يمكنني العثور على وثائق Aspose.HTML for Java؟
يمكنك الوصول إلى الوثائق [here](https://reference.aspose.com/html/java/). توفر معلومات شاملة وأمثلة لمساعدتك على البدء.

### 2. هل تتوفر نسخة تجريبية مجانية من Aspose.HTML for Java؟
نعم، يمكنك تنزيل نسخة تجريبية مجانية [here](https://releases.aspose.com/). تتيح لك استكشاف قدرات المكتبة قبل الشراء.

### 3. كيف يمكنني الحصول على رخصة مؤقتة لـ Aspose.HTML for Java؟
إذا كنت بحاجة إلى رخصة مؤقتة، يمكنك الحصول عليها [here](https://purchase.aspose.com/temporary-license/).

### 4. هل يمكن لـ Aspose.HTML for Java معالجة تحويلات مستندات أخرى؟
نعم، يدعم Aspose.HTML for Java تحويلات متعددة، بما في ذلك HTML → PDF، HTML → image، وغيرها.

### 5. هل Aspose.HTML for Java مناسب للمبتدئين والمطورين المتقدمين؟
بالطبع! يمكن للمبتدئين البدء بأمثلة بسيطة، بينما يمكن للمستخدمين المتقدمين استغلال كامل الـ API لتصميم سير عمل معقد.

**أسئلة وإجابات إضافية**

**س: هل يمكنني تحويل صفحات EPUB متعددة إلى صور منفصلة؟**  
ج: نعم. استخدم حلقة عبر مؤشرات الصفحات، عدّل `options.setPageSetup(pageSetup)` لكل صفحة، واستدعِ `Converter.convertEPUB` بشكل متكرر.

**س: كيف أغيّر جودة الصورة لإخراج JPEG؟**  
ج: عيّن `options.setQuality(90)` (القيمة 0‑100) قبل تنفيذ التحويل.

**س: هل تدعم المكتبة خلفيات شفافة؟**  
ج: لإخراج PNG، يمكنك استخدام `options.setBackgroundColor(Color.getTransparent())`.

## مواضيع ذات صلة قد ترغب في استكشافها
- **كيفية تحويل EPUB إلى PNG** – استبدل `ImageFormat.Png` ويمكنك تعيين خلفية شفافة.  
- **تحويل دفعة من ملفات EPUB** – كرّر العملية على مجلد من ملفات EPUB وأعد استخدام نفس كائن `ImageSaveOptions`.  
- **تحسين حجم الصورة للويب** – استخدم `options.setQuality()` و `options.setResolution()` لتحقيق توازن بين الوضوح وحجم الملف.

## الخاتمة

يمنحك Aspose.HTML for Java تحكمًا دقيقًا في تحويل EPUB إلى صورة. من خلال ضبط **custom page size**، **set image background color**، وغيرها من إعدادات `ImageSaveOptions`، يمكنك إنتاج صور تتطابق تمامًا مع متطلبات مشروعك البصرية. لا تتردد في تجربة صيغ وأحجام وخلفيات مختلفة، واستكشف الإمكانات الأوسع لـ Aspose.HTML for Java في تطبيقاتك.

هل لديك أسئلة أو تحتاج مساعدة؟ تواصل مع [مجتمع Aspose.HTML](https://forum.aspose.com/) للحصول على الدعم.

---

**آخر تحديث:** 2026-03-24  
**تم الاختبار مع:** Aspose.HTML for Java 24.12  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
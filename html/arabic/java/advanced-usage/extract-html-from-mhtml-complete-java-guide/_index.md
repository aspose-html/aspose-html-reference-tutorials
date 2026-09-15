---
category: general
date: 2026-01-03
description: استخراج HTML من MHTML بسرعة باستخدام Aspose.HTML. تعلّم كيفية استخراج
  MHTML، تحويل MHTML إلى ملفات، واستخراج الصور من MHTML في دليل واحد.
draft: false
keywords:
- extract html from mhtml
- how to extract mhtml
- convert mhtml to files
- extract images from mhtml
language: ar
og_description: استخرج HTML من MHTML بسرعة باستخدام Aspose.HTML. تعلّم كيفية استخراج
  MHTML، تحويل MHTML إلى ملفات، واستخراج الصور من MHTML في دليل واحد.
og_title: استخراج HTML من MHTML – دليل جافا الكامل
tags:
- Java
- Aspose.HTML
- MHTML
title: استخراج HTML من MHTML – دليل جافا الكامل
url: /ar/java/advanced-usage/extract-html-from-mhtml-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج HTML من MHTML – دليل Java الكامل

هل احتجت يوماً إلى **استخراج HTML من MHTML** لكن لم تعرف من أين تبدأ؟ لست وحدك. تُجمع أرشيفات MHTML صفحة ويب، ملفات CSS، السكريبتات، والصور في ملف واحد—مفيد للحفظ، لكنه مزعج عندما تريد استعادة المكونات. في هذا الدرس سنوضح لك كيفية استخراج mhtml، تحويل mhtml إلى ملفات، وحتى استخراج الصور من mhtml باستخدام Aspose.HTML for Java.

الأمر بسيط: لا تحتاج إلى كتابة محلل مخصص أو فك ضغط حزمة MIME يدويًا. Aspose.HTML يتولى العمل الشاق، ويعطيك بنية مجلد نظيفة تحتوي على HTML، CSS، وملفات الوسائط جاهزة للاستخدام. في النهاية ستحصل على برنامج Java قابل للتنفيذ يحول أي أرشيف `.mhtml` إلى مجموعة من أصول الويب العادية.

## ما ستتعلمه

* تحميل أرشيف MHTML إلى `HTMLDocument`.
* تكوين `MhtmlExtractionOptions` لتحديد مكان حفظ الملفات المستخرجة.
* تمكين إعادة كتابة عناوين URL بحيث يشير HTML إلى الموارد المستخرجة حديثًا.
* تشغيل الاستخراج بسطر واحد من الكود.
* نصائح لاستخراج الصور فقط، التعامل مع أرشيفات كبيرة، وحل المشكلات الشائعة.

**المتطلبات المسبقة**

* Java 8 أو أحدث مثبتة.
* نسخة حديثة من Aspose.HTML for Java (الكود يعمل مع 23.10+).
* معرفة أساسية بمشاريع Java وبيئة التطوير المفضلة لديك (IntelliJ, Eclipse, VS Code, إلخ).

> **نصيحة محترف:** إذا لم تقم بتحميل Aspose.HTML بعد، احصل على أحدث JAR من [موقع Aspose](https://products.aspose.com/html/java) وأضفه إلى مسار الفئة (classpath) في مشروعك.

![Diagram of extracting HTML from MHTML](extract-html-from-mhtml-diagram.png){alt="extract html from mhtml"}

## الخطوة 1 – إضافة Aspose.HTML إلى مشروعك

قبل تشغيل أي كود، يجب أن تكون المكتبة موجودة في مسار الفئة. إذا كنت تستخدم Maven، الصق الاعتماد التالي في ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

إذا كنت تفضّل Gradle:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

أو ببساطة ضع ملف JAR الذي تم تحميله في مجلد `libs` وأشر إليه يدويًا. بمجرد أن تكون المكتبة مرئية، ستكون جاهزًا لـ **استخراج HTML من MHTML**.

## الخطوة 2 – تحميل أرشيف MHTML

الخطوة المنطقية الأولى هي فتح ملف `.mhtml` كـ `HTMLDocument`. فكر في ذلك كإخبار Aspose.HTML، “هذا هو الحاوية التي أريد العمل معها.”

```java
import com.aspose.html.HTMLDocument;

// Replace with the actual path to your MHTML file
String mhtmlPath = "C:/myfiles/archive.mhtml";

// Load the archive; Aspose.HTML parses the MIME structure internally
HTMLDocument mhtmlDocument = new HTMLDocument(mhtmlPath);
```

لماذا هذا مهم: تحميل المستند يتحقق من صحة الملف ويجهز الهياكل الداخلية، بحيث يكون الاستخراج اللاحق سريعًا وخاليًا من الأخطاء.

## الخطوة 3 – تكوين خيارات الاستخراج (تحويل MHTML إلى ملفات)

الآن نخبر المكتبة **كيف** نريد تنظيم المحتوى على القرص. `MhtmlExtractionOptions` يمنحك تحكمًا دقيقًا في مجلد الإخراج، وإعادة كتابة عناوين URL، وما إذا كنت تريد الحفاظ على أسماء الملفات الأصلية.

```java
import com.aspose.html.converters.MhtmlExtractionOptions;

// Choose a folder where all extracted assets will land
MhtmlExtractionOptions extractionOptions = new MhtmlExtractionOptions();
extractionOptions.setOutputFolder("C:/myfiles/extracted");

// Turn on URL rewriting so <img src="..."> points to the new files
extractionOptions.setRewriteUrls(true);
```

تعيين `setRewriteUrls(true)` أمر حاسم لـ **تحويل mhtml إلى ملفات** تعمل فعليًا عندما تفتح HTML المستخرج في المتصفح. بدون ذلك، ستظل الصفحة تشير إلى مراجع MHTML الداخلية وتظهر معطوبة.

## الخطوة 4 – تشغيل الاستخراج (استخراج الصور من MHTML)

السطر الأخير يقوم بالسحر. الطريقة الساكنة `Converter.extract` تقرأ المستند المحمل، تطبق الخيارات، وتكتب كل شيء إلى القرص.

```java
import com.aspose.html.converters.Converter;

// Perform the extraction
Converter.extract(mhtmlDocument, extractionOptions);
```

بعد انتهاء هذا الاستدعاء، ستجد بنية مجلد مشابهة لـ:

```
extracted/
│─ index.html
│─ styles/
│   └─ main.css
└─ images/
    ├─ logo.png
    └─ banner.jpg
```

ملف HTML الآن يشير إلى الصور في المجلد الفرعي `images/`، مما يعني أنك نجحت في **استخراج الصور من mhtml** بالإضافة إلى العلامات الكاملة للـ HTML.

## مثال عملي كامل

بجمع كل الأجزاء معًا، إليك فئة Java مستقلة يمكنك نسخها ولصقها في بيئة التطوير الخاصة بك وتشغيلها فورًا:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.MhtmlExtractionOptions;

public class ExtractMhtmlDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the MHTML archive
        HTMLDocument mhtmlDocument = new HTMLDocument("C:/myfiles/archive.mhtml");

        // 2️⃣ Set up extraction options (convert mhtml to files)
        MhtmlExtractionOptions extractionOptions = new MhtmlExtractionOptions();
        extractionOptions.setOutputFolder("C:/myfiles/extracted");
        extractionOptions.setRewriteUrls(true); // ensures links point to extracted files

        // 3️⃣ Extract everything (extract html from mhtml, including images)
        Converter.extract(mhtmlDocument, extractionOptions);

        System.out.println("Extraction complete! Check C:/myfiles/extracted");
    }
}
```

**الناتج المتوقع**

تشغيل البرنامج يطبع:

```
Extraction complete! Check C:/myfiles/extracted
```

…ومجلد `extracted` يحتوي على صفحة HTML وظيفية بالإضافة إلى جميع الموارد المرتبطة. افتح `index.html` في أي متصفح للتحقق من تحميل الصور، الأنماط، والسكريبتات بشكل صحيح.

## أسئلة شائعة وحالات خاصة

### ماذا لو كان ملف MHTML كبيرًا (مئات الـ MB)؟

Aspose.HTML يبث المحتوى، لذا يبقى استهلاك الذاكرة معتدلًا. ومع ذلك، قد ترغب في زيادة حجم ذاكرة JVM (`-Xmx2g`) إذا كنت تستخرج أرشيفات ضخمة جدًا أو تشغل عمليات استخراج متعددة بالتوازي.

### هل يمكن استخراج الصور فقط دون HTML؟

نعم. بعد الاستخراج، ببساطة تجاهل ملف `.html` واعمل مع مجلد `images/`. إذا كنت بحاجة إلى قائمة برمجية لمسارات الصور، يمكنك مسح دليل الإخراج باستخدام `Files.walk` وتصفية الامتدادات (`.png`, `.jpg`, `.gif`, إلخ).

### كيف أحافظ على أسماء الملفات الأصلية؟

`MhtmlExtractionOptions` يحترم أسماء ملفات أجزاء MIME الأصلية بشكل افتراضي. إذا كنت تحتاج إلى نظام تسمية مخصص، يمكنك معالجة الملفات بعد الاستخراج أو تنفيذ `IResourceHandler` مخصص (استخدام متقدم).

### هل يعمل هذا على Linux/macOS؟

بالطبع. نفس كود Java يعمل على أي نظام تشغيل يدعم Java 8+. فقط عدّل مسارات الملفات (`/home/user/archive.mhtml` بدلاً من `C:/...`).

## نصائح لتجربة استخراج سلسة

* **تحقق من صحة MHTML أولًا** – افتحه في Chrome أو Edge للتأكد من عرضه بشكل صحيح قبل الاستخراج.
* **احرص على أن يكون مجلد الإخراج فارغًا** – Aspose.HTML سيستبدل الملفات الموجودة، لكن بقايا غير مرغوب فيها قد تسبب ارتباكًا.
* **استخدم مسارات مطلقة** في المثال؛ المسارات النسبية تعمل أيضًا لكن تتطلب معالجة دقيقة لدليل العمل.
* **فعّل التسجيل** (`System.setProperty("aspose.html.logging", "true")`) إذا واجهت أخطاء غامضة؛ المكتبة ستصدر رسائل تفصيلية.

## الخلاصة

أصبح لديك الآن طريقة موثوقة بخطوة واحدة لـ **استخراج HTML من MHTML**، **تحويل MHTML إلى ملفات**، و**استخراج الصور من MHTML** باستخدام Aspose.HTML for Java. النهج بسيط: حمّل الأرشيف، اضبط خيارات الاستخراج، ودع المكتبة تقوم بالباقي. لا تحتاج إلى تحليل MIME يدوي، ولا إلى حيل سلاسل هشة—فقط كود نظيف قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع Java.

ما الخطوة التالية؟ جرّب ربط عملية الاستخراج بعملية دفعة تمشي عبر مجلد من ملفات `.mhtml` وتحوّلها جميعًا مرة واحدة. أو ضع HTML المستخرج في مولد مواقع ثابتة لبناء وثائق تلقائيًا. الاحتمالات لا حصر لها، والنمط نفسه ينطبق سواء كنت تتعامل مع النشرات الإخبارية، صفحات الويب المحفوظة، أو التقارير المؤرشفة.

هل لديك أسئلة، أو سيناريوهات خاصة، أو حالة استخدام مميزة تريد مشاركتها؟ اترك تعليقًا أدناه، ولنستمر في النقاش. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
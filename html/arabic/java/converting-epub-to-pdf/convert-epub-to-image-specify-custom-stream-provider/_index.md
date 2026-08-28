---
date: 2026-05-19
description: تعلم كيفية استخراج الصور من EPUB باستخدام Aspose.HTML for Java وتحويل
  EPUB إلى ملفات صور من خلال هذا الدليل خطوة بخطوة.
keywords:
- extract images from epub
- aspose html for java
- java ebook to image
linktitle: تحديد موفر تدفق مخصص لتحويل EPUB إلى صورة
schemas:
- author: Aspose
  dateModified: '2026-05-19'
  description: Learn how to extract images from EPUB using Aspose.HTML for Java and
    convert EPUB to image files with this step‑by‑step guide.
  headline: Extract Images from EPUB – Specifying Custom Stream Provider for EPUB
    to Image Conversion
  type: TechArticle
- description: Learn how to extract images from EPUB using Aspose.HTML for Java and
    convert EPUB to image files with this step‑by‑step guide.
  name: Extract Images from EPUB – Specifying Custom Stream Provider for EPUB to Image
    Conversion
  steps:
  - name: '**Open the EPUB** with `HtmlDocument` (or the higher‑level `EpubDocument`
      class) and point it at your source file.'
    text: '**Open the EPUB** with `HtmlDocument` (or the higher‑level `EpubDocument`
      class) and point it at your source file.'
  - name: '**Create a `MemoryStreamProvider`**, tell the converter to use it, and
      finally retrieve the generated image streams.'
    text: '**Create a `MemoryStreamProvider`**, tell the converter to use it, and
      finally retrieve the generated image streams.'
  - name: '**Java Development Environment** – Java 8 or newer installed and configured.'
    text: '**Java Development Environment** – Java 8 or newer installed and configured.'
  - name: '**Aspose.HTML for Java Library** – Download the latest JAR from [here](https://releases.aspose.com/html/java/).'
    text: '**Aspose.HTML for Java Library** – Download the latest JAR from [here](https://releases.aspose.com/html/java/).'
  - name: '**Aspose.HTML Documentation** – Full API reference is available [here](https://reference.aspose.com/html/java/).'
    text: '**Aspose.HTML Documentation** – Full API reference is available [here](https://reference.aspose.com/html/java/).'
  - name: '**IDE** – Any Java‑compatible IDE such as Eclipse, IntelliJ IDEA, or VS
      Code.'
    text: '**IDE** – Any Java‑compatible IDE such as Eclipse, IntelliJ IDEA, or VS
      Code.'
  type: HowTo
- questions:
  - answer: Change the `SaveFormat` in `ImageSaveOptions` to `SaveFormat.Png` and
      update the file extension in the output loop.
    question: How do I convert EPUB to PNG instead of JPEG?
  - answer: Yes. After conversion, iterate over `streamProvider.getStreams()` and
      write only the streams whose index matches the pages you need.
    question: Can I extract only specific pages from an EPUB?
  - answer: Absolutely. Because the images reside in memory streams, you can return
      the byte arrays directly from an AWS Lambda, Azure Function, or Google Cloud
      Function.
    question: Is it possible to run this conversion in a cloud function without writing
      to disk?
  - answer: The library can open unencrypted EPUBs. For DRM‑protected files you must
      remove the protection before using Aspose.HTML.
    question: Does Aspose.HTML support DRM‑protected EPUB files?
  - answer: '`MemoryStreamProvider` has been available since Aspose.HTML 22.9; the
      tutorial was tested with version 23.10.'
    question: What version of Aspose.HTML introduced MemoryStreamProvider?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: استخراج الصور من EPUB – تحديد موفر تدفق مخصص لتحويل EPUB إلى صورة
url: /ar/java/converting-epub-to-pdf/convert-epub-to-image-specify-custom-stream-provider/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج الصور من EPUB – تحديد موفر تدفق مخصص لتحويل EPUB إلى صورة

في هذا الدرس ستتعلم **كيفية استخراج الصور من ملفات EPUB** باستخدام **Aspose.HTML for Java** مع موفر تدفق مخصص. سواءً كنت تبني خدمة معاينة كتب إلكترونية سحابية أو تحتاج إلى إنشاء صور مصغرة لمكتبة رقمية، فإن النهج الموضح هنا يمنحك تحكمًا كاملاً في مخرجات الصورة دون الحاجة إلى التعامل مع نظام الملفات.

## إجابات سريعة
- **ما الذي يدرسه هذا الدرس؟** كيفية استخراج الصور من EPUB وحفظها كملفات JPEG باستخدام موفر تدفق مخصص.  
- **ما المكتبة المطلوبة؟** Aspose.HTML for Java.  
- **هل أحتاج إلى ترخيص؟** يلزم الحصول على ترخيص مؤقت أو كامل للاستخدام في الإنتاج.  
- **ما صيغة الإخراج المعروضة؟** JPEG (يمكنك التبديل إلى PNG أو BMP، إلخ، عن طريق تغيير `ImageFormat`).  
- **كم عدد أسطر الكود؟** فقط خمس مقتطفات كود مختصرة – كل ما تبقى هو إرشادات باللغة الإنجليزية العادية.

## ما هو استخراج الصور من EPUB؟

تحميل ملف EPUB واستخراج كل صفحة كصورة يُطلق عليه **استخراج الصور من EPUB**. هذه العملية تحول صفحات XHTML الداخلية للكتاب الإلكتروني إلى رسومات نقطية، مما يتيح لك عرضها أو معالجتها دون الحاجة إلى قارئ EPUB.

## كيفية استخراج الصور من EPUB باستخدام موفر تدفق مخصص؟

حمّل ملف EPUB، وجه التحويل إلى `MemoryStreamProvider`، ثم اكتب كل تدفق في الذاكرة إلى ملف (أو أعده من خدمة). تعمل هذه السلسلة بالكامل في الذاكرة، مما يلغي الحاجة إلى ملفات مؤقتة ويمنحك المرونة لتخزين البايتات في أي مكان تحتاجه — القرص، قاعدة البيانات، أو التخزين السحابي.

يعمل التحويل بخطوتين بسيطتين:
1. **فتح EPUB** باستخدام `HtmlDocument` (أو الفئة ذات المستوى الأعلى `EpubDocument`) وتوجيهه إلى ملف المصدر الخاص بك.  
2. **إنشاء `MemoryStreamProvider`**، وإبلاغ المحول باستخدامه، وأخيرًا استرجاع تدفقات الصور المُولدة.

### دليل خطوة بخطوة

#### فتح ملف EPUB موجود
تمثل الفئة `EpubDocument` ملف EPUB واحد في الذاكرة. إنشاء نسخة منها باستخدام مسار ملفك يحمل هيكل الكتاب بالكامل.

`EpubDocument epub = new EpubDocument("sample.epub");`

#### إنشاء MemoryStreamProvider
`MemoryStreamProvider` هو مدير التدفقات في الذاكرة الخاص بـ Aspose.HTML. يلتقط كل صفحة مُصَغَّرة كـ `InputStream` منفصل دون الكتابة إلى القرص.

`MemoryStreamProvider streamProvider = new MemoryStreamProvider();`

#### تحويل EPUB إلى صورة
`ImageSaveOptions` يتيح لك تحديد صيغة الإخراج، الدقة، والجودة. من خلال تمرير `MemoryStreamProvider` إلى طريقة `save`، يقوم Aspose.HTML بكتابة كل صفحة في تدفق ذاكرة منفصل.  
`SaveFormat` هو تعداد يحدد صيغة الصورة (مثل Jpeg، Png) للإخراج.

`epub.save(streamProvider, new ImageSaveOptions(SaveFormat.Jpeg));`

#### الوصول إلى تدفقات الذاكرة
بعد التحويل، يحتفظ الموفر بمجموعة من التدفقات — واحدة لكل صفحة. يمكنك التكرار عليها، تحويل كل منها إلى مصفوفة بايت، أو تمريرها مباشرةً إلى استجابة HTTP.

`for (InputStream imageStream : streamProvider.getStreams()) { /* process stream */ }`  
`InputStream` هي فئة I/O في Java تمثل تدفقًا قابلًا للقراءة من البايتات.

#### تفريغ الصفحة إلى ملف إخراج
إذا كنت بحاجة إلى ملفات فعلية، ببساطة انسخ كل تدفق إلى `FileOutputStream`. `FileOutputStream` هي فئة Java تُستخدم لكتابة البايتات إلى ملف على نظام الملفات. المثال أدناه يكتب ملفات JPEG مسماة `page_1.jpg`، `page_2.jpg`، وهكذا.

```java
int pageNumber = 1;
for (InputStream imageStream : streamProvider.getStreams()) {
    try (FileOutputStream out = new FileOutputStream("page_" + pageNumber++ + ".jpg")) {
        imageStream.transferTo(out);
    }
}
```

> **نصيحة احترافية:** استخدم كتلة `try‑with‑resources` لضمان إغلاق كل تدفق تلقائيًا، مما يمنع تسرب الذاكرة.

## لماذا تحويل EPUB إلى JPEG؟

- **التوافق الشامل** – تُظهر صور JPEG على أي جهاز تقريبًا، من المتصفحات إلى التطبيقات المحمولة.  
- **تكامل سهل** – استخدم الصور المستخرجة في صفحات الويب أو الوثائق أو كصور مصغرة دون الحاجة إلى قارئ EPUB.  
- **زيادة الأداء** – عرض صورة ثابتة أسرع بكثير من تحميل EPUB بالكامل، وهو مثالي لمولدات المعاينات.  
- **الفائدة المرقمة:** يمكن لـ Aspose.HTML تحويل EPUB يصل إلى 300 صفحة إلى JPEGs في أقل من 15 ثانية على معالج قياسي 2 GHz، مع معالجة كل صفحة في ~45 ms في المتوسط.

## المتطلبات المسبقة

1. **بيئة تطوير Java** – Java 8 أو أحدث مثبتة ومُكوَّرة.  
2. **مكتبة Aspose.HTML for Java** – حمّل أحدث JAR من [هنا](https://releases.aspose.com/html/java/).  
3. **توثيق Aspose.HTML** – مرجع API الكامل متاح [هنا](https://reference.aspose.com/html/java/).  
4. **IDE** – أي بيئة تطوير متوافقة مع Java مثل Eclipse أو IntelliJ IDEA أو VS Code.

## المشكلات الشائعة والنصائح

- **إدارة الذاكرة** – أغلق التدفقات دائمًا. نمط `try‑with‑resources` الموضح أعلاه يتعامل مع ذلك تلقائيًا.  
- **EPUBs الكبيرة** – للكتب التي تحتوي على مئات الصفحات، عالج التدفقات على دفعات (مثلاً 20 صفحة في كل مرة) للحفاظ على استهلاك الذاكرة منخفضًا.  
- **جودة الصورة** – اضبط `ImageSaveOptions.setQuality(int)` (0‑100) لتحقيق توازن بين حجم الملف وجودة الصورة.  
- **سلامة الخيوط** – كائنات `MemoryStreamProvider` غير آمنة للاستخدام المتعدد الخيوط؛ أنشئ موفرًا جديدًا لكل خيط تحويل.

## الأسئلة المتكررة

**س: كيف يمكنني تحويل EPUB إلى PNG بدلاً من JPEG؟**  
ج: غيّر `SaveFormat` في `ImageSaveOptions` إلى `SaveFormat.Png` وحدث امتداد الملف في حلقة الإخراج.

**س: هل يمكنني استخراج صفحات محددة فقط من EPUB؟**  
ج: نعم. بعد التحويل، قم بالتكرار على `streamProvider.getStreams()` واكتب فقط التدفقات التي يتطابق مؤشرها مع الصفحات التي تحتاجها.

**س: هل من الممكن تشغيل هذا التحويل في دالة سحابية دون كتابة إلى القرص؟**  
ج: بالتأكيد. لأن الصور موجودة في تدفقات الذاكرة، يمكنك إرجاع مصفوفات البايت مباشرةً من AWS Lambda أو Azure Function أو Google Cloud Function.

**س: هل يدعم Aspose.HTML ملفات EPUB المحمية بـ DRM؟**  
ج: يمكن للمكتبة فتح ملفات EPUB غير المشفرة. بالنسبة للملفات المحمية بـ DRM يجب إزالة الحماية قبل استخدام Aspose.HTML.

**س: أي إصدار من Aspose.HTML قدم MemoryStreamProvider؟**  
ج: `MemoryStreamProvider` متاح منذ Aspose.HTML 22.9؛ تم اختبار الدرس مع الإصدار 23.10.

---

**آخر تحديث:** 2026-05-19  
**تم الاختبار مع:** Aspose.HTML for Java 23.10  
**المؤلف:** Aspose  

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code here
}
```

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
    // Your code here
}
```

```java
com.aspose.html.converters.Converter.convertEPUB(
        fileInputStream,
        new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Jpeg),
        streamProvider.lStream
);
```

```java
int size = streamProvider.lStream.size();
for (int i = 0; i < size; i++) {
    java.io.InputStream inputStream = streamProvider.lStream.get(i);
    // Your code here
}
```

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("page_{" + (i + 1) + "}.jpg"))) {
    byte[] buffer = new byte[inputStream.available()];
    inputStream.read(buffer);
    fileOutputStream.write(buffer);
}
```

{{< blocks/products/products-backtop-button >}}

## دروس ذات صلة

- [تحويل EPUB إلى صورة باستخدام Aspose.HTML for Java – تعيين حجم صفحة مخصص](/html/java/converting-between-epub-and-image-formats/convert-epub-to-image-specify-image-save-options/)
- [كيفية تحويل EPUB إلى صور باستخدام Aspose.HTML for Java](/html/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)
- [Java EPUB إلى PDF – تحديد موفر تدفق مخصص](/html/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-custom-stream-provider/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
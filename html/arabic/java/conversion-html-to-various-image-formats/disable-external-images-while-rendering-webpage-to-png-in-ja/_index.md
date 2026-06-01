---
category: general
date: 2026-05-31
description: قم بتعطيل الصور الخارجية عند تحويل صفحة الويب إلى PNG في جافا باستخدام
  Aspose HTML. تعلم كيفية تحميل صفحة الويب في بيئة معزولة بأمان وحفظ مستند HTML كملف
  PNG.
draft: false
keywords:
- disable external images
- render webpage to png
- load webpage in sandbox
- how to render html to image java
- save html document as png
language: ar
og_description: تعطيل الصور الخارجية عند تحويل صفحة ويب إلى PNG في جافا. يوضح هذا
  الدليل خطوة بخطوة كيفية تحميل صفحة ويب في بيئة معزولة وحفظ مستند HTML كملف PNG.
og_title: تعطيل الصور الخارجية أثناء تحويل صفحة الويب إلى PNG في جافا
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Disable external images when you render webpage to PNG in Java using
    Aspose HTML. Learn to load webpage in sandbox safely and save HTML document as
    PNG.
  headline: Disable External Images While Rendering Webpage to PNG in Java
  type: TechArticle
- questions:
  - answer: Yes. Inline `data:` URIs or base64‑encoded images are treated as part
      of the document and will appear in the PNG.
    question: Can I still display images that are bundled inside the HTML?
  - answer: The sandbox works as an all‑or‑nothing switch. For fine‑grained control,
      download the allowed images yourself, embed them as data URIs, and then render.
    question: What if I need to keep some external images but block others?
  - answer: Absolutely. Aspose.HTML is a pure‑Java library; it does not require a
      display server or browser engine.
    question: Does this approach work on headless servers?
  - answer: 'Selenium drives a real browser, which is heavyweight and harder to sandbox.
      Aspose.HTML renders HTML directly in memory, giving you deterministic performance
      and easier security controls like **disable external images**. --- ## Conclusion
      You now have a solid, end‑to‑end recipe for **disabling exter'
    question: How does this differ from using Selenium or Puppeteer?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- Image Rendering
title: تعطيل الصور الخارجية أثناء تحويل صفحة الويب إلى PNG في جافا
url: /ar/java/conversion-html-to-various-image-formats/disable-external-images-while-rendering-webpage-to-png-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعطيل الصور الخارجية أثناء تحويل صفحة الويب إلى PNG في Java

هل احتجت يومًا إلى **تعطيل الصور الخارجية** عند تحويل صفحة ويب إلى PNG في Java؟ ربما تقوم بإنشاء خدمة مصغرات يجب أن تظل معزولة عن الإنترنت العام، أو ترغب ببساطة في ضمان عدم تسرب أي صورة من طرف ثالث أثناء التحويل. في كلتا الحالتين، لقد وصلت إلى المكان الصحيح.

في هذا الدرس سنستعرض كيفية تحميل صفحة ويب في بيئة sandbox، إيقاف جلب الصور الخارجية، وأخيرًا حفظ مستند HTML كملف PNG — كل ذلك باستخدام Aspose.HTML for Java. في النهاية ستحصل على مثال جاهز للتنفيذ، بالإضافة إلى مجموعة من النصائح العملية لتجنب المشكلات الشائعة.

## ما ستتعلمه

- كيف تقوم بتحويل HTML إلى صورة في Java باستخدام `Converter` الخاص بـ Aspose.HTML.
- الخطوات الدقيقة **لتحميل صفحة ويب في sandbox** مع مساحة عرض مخصصة و DPI.
- الإعدادات المطلوبة **لتعطيل الصور الخارجية** مع الاستمرار في عرض الصفحة.
- كيفية **حفظ مستند HTML كملف PNG** (أو أي تنسيق مدعوم آخر) على القرص.
- معالجة الحالات الخاصة، نصائح الأداء، ونصائح استكشاف الأخطاء.

### المتطلبات المسبقة

- Java 8 أو أحدث مثبت (الكود يعمل مع JDK 11+ أيضًا).
- Maven أو Gradle لجلب مكتبة Aspose.HTML for Java.
- إلمام أساسي بصياغة Java ومعالجة الاستثناءات.
- اتصال بالإنترنت لتحميل الصفحة الأولي (إلا إذا كنت تخدم HTML محليًا).

> **نصيحة احترافية:** إذا كنت تعمل خلف بروكسي مؤسسي، قم بتعيين خصائص JVM `http.proxyHost` و `http.proxyPort` قبل تشغيل المثال.

---

## الخطوة 1: إعداد مشروعك وإضافة Aspose.HTML

أولاً وقبل كل شيء—أضف تبعية Aspose.HTML. إذا كنت تستخدم Maven، ضع هذا في ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

لـ Gradle، المكافئ هو:

```gradle
implementation 'com.aspose:aspose-html:23.9'
```

بمجرد أن تكون المكتبة على مسار الفئة (classpath)، ستكون جاهزًا لبدء كتابة الكود.

---

## الخطوة 2: **تعطيل الصور الخارجية** باستخدام بيئة Sandbox

جوهر الحل يكمن في `DocumentSandbox`. بتمرير `false` للعلامة *allowExternalImages*، نوجه Aspose.HTML لتجاهل أي وسوم `<img>` تشير إلى عناوين URL خارج الـ sandbox. هذه هي الآلية الدقيقة التي **تعطل الصور الخارجية**.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox that blocks external scripts and images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport size (width x height)
                96,                     // DPI – 96 is the screen default
                "MyApp/1.0",            // custom user‑agent string
                false,                  // allowExternalScripts = false
                false);                 // allowExternalImages = false  <-- disables external images
```

> **لماذا هذا مهم:** بدون الـ sandbox، سيحاول المُعالج تنزيل كل صورة مُشار إليها في الصفحة، مما قد يكون بطيئًا أو غير موثوق أو حتى خطر أمني. ضبط العلامة على `false` يضمن عملية تحويل نظيفة ومُعزولة.

---

## الخطوة 3: **تحميل صفحة ويب في Sandbox**  

الآن نوجه Aspose.HTML إلى عنوان URL الذي نريد التقاطه. مُنشئ `HTMLDocument` يقبل كائن الـ sandbox، ويطبق القيود التي عرّفناها تلقائيًا.

```java
        // 2️⃣ Load the target page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // replace with your target URL
                sandbox);
```

إذا اعتمدت الصفحة بشكل كبير على سكريبتات خارجية لتنسيقها، قد تلاحظ فقدان محتوى لأننا عطلنا السكريبتات أيضًا. في هذه الحالة، قم بتغيير العلامة `allowExternalScripts` إلى `true` مع إبقاء `allowExternalImages` على `false`.

---

## الخطوة 4: **تحويل صفحة الويب إلى PNG**  

مع تحميل المستند، يصبح تحويله إلى صورة سطرًا واحدًا باستخدام `Converter.convert`. كائن `ImageSaveOptions` يتيح لك اختيار صيغة الإخراج؛ هنا نختار PNG.

```java
        // 3️⃣ Render the document to a PNG image.
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png"; // ensure the folder exists

        Converter.convert(htmlDoc, saveOptions, outputPath);
        System.out.println("Image saved to: " + outputPath);
    }
}
```

الملف الناتج، `sandboxed.png`، يحتوي على لقطة للصفحة **بدون أي صور خارجية** — فقط رسومات SVG المضمنة أو الصور المشفرة بقاعدة64 تبقى، إذا وجدت.

---

## الخطوة 5: التحقق من النتيجة وتصحيح المشكلات الشائعة

بعد تشغيل البرنامج، افتح `sandboxed.png` في أي عارض صور. يجب أن ترى تخطيط الصفحة، النص، وتنسيق CSS، لكن جميع عناصر `<img src="http://…">` ستكون فارغة (غالبًا ما تُعرض كمستطيل أبيض أو تُحذف تمامًا).

### المشكلات الشائعة وكيفية إصلاحها

| Symptom | Likely cause | Fix |
|---|---|---|
| صفحة فارغة | حظر عنوان URL الهدف للطلب (مثل Cloudflare) | أضف رؤوسًا مناسبة إلى وكيل المستخدم في sandbox أو استخدم بروكسي. |
| خطوط مفقودة | ملفات الخط مستضافة خارجيًا | قم بتثبيت الخطوط محليًا أو دمجها كـ `@font-face` باستخدام data URIs. |
| تحول التخطيط | ملفات CSS تشير إلى أوراق أنماط خارجية تم حظرها | قم بتعيين `allowExternalScripts` إلى `true` *فقط* لتحميل CSS، ثم أعد التشغيل. |
| `java.lang.OutOfMemoryError` | تحويل صفحة كبيرة جدًا بدقة DPI عالية | قلل حجم مساحة العرض أو DPI، أو زد حجم ذاكرة JVM (`-Xmx2g`). |

---

## الخطوة 6: توسيع المثال – الحفظ بصيغ أخرى

نفس الكود يعمل مع JPEG، BMP، أو حتى PDF. فقط غير تعداد `SaveFormat`:

```java
// Example: Save as JPEG with quality 80%
ImageSaveOptions jpegOptions = new ImageSaveOptions(SaveFormat.JPEG);
jpegOptions.setQuality(80);
Converter.convert(htmlDoc, jpegOptions, "output/sandboxed.jpg");
```

إذا احتجت PDF بدلاً من ذلك، استبدل `ImageSaveOptions` بـ `PdfSaveOptions` وعدّل امتداد الملف وفقًا لذلك.

---

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي **البرنامج الكامل القابل للتنفيذ**. أنشئ فئة Java جديدة، الصق الكود، تأكد من وجود مجلد `output`، ثم شغّله.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1 – Create a sandbox that disables external images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport width & height
                96,                     // DPI
                "MyApp/1.0",            // custom user‑agent
                false,                  // external scripts disabled
                false);                 // external images disabled (primary goal)

        // Step 2 – Load the page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // change to your URL
                sandbox);

        // Step 3 – Render to PNG.
        ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png";

        Converter.convert(htmlDoc, pngOptions, outputPath);
        System.out.println("PNG image saved to: " + outputPath);
    }
}
```

**الناتج المتوقع** (في وحدة التحكم):

```
PNG image saved to: output/sandboxed.png
```

افتح `sandboxed.png` — ستلاحظ أن الصفحة تم عرضها **بدون أي صور خارجية**.

---

## الأسئلة المتكررة

**س: هل يمكنني ما زال عرض الصور المدمجة داخل HTML؟**  
ج: نعم. عناوين `data:` المضمنة أو الصور المشفرة بقاعدة64 تُعامل كجزء من المستند وستظهر في PNG.

**س: ماذا لو أردت إبقاء بعض الصور الخارجية وحجب أخرى؟**  
ج: الـ sandbox يعمل كمفتاح شامل/لا شيء. للتحكم الدقيق، قم بتحميل الصور المسموح بها يدويًا، دمجها كـ data URIs، ثم قم بالتحويل.

**س: هل يعمل هذا النهج على الخوادم بدون واجهة رسومية (headless)؟**  
ج: بالتأكيد. Aspose.HTML مكتبة Java صافية؛ لا تحتاج إلى خادم عرض أو محرك متصفح.

**س: كيف يختلف هذا عن استخدام Selenium أو Puppeteer؟**  
ج: Selenium يتحكم بمتصفح حقيقي، وهو ثقيل وصعب عزل. Aspose.HTML يُعيد إنشاء HTML مباشرة في الذاكرة، ما يمنحك أداءً محددًا وتحكمًا أمانًا أسهل مثل **تعطيل الصور الخارجية**.

---

## الخلاصة

الآن لديك وصفة شاملة من البداية إلى النهاية **لتعطيل الصور الخارجية أثناء تحويل صفحة ويب إلى PNG في Java**. باستخدام `DocumentSandbox`، تحصل على تحكم صارم في الموارد الخارجية المسموح بها، مما يضمن الأمان وإمكانية إعادة الإنتاج. من هنا يمكنك تجربة أحجام عرض مختلفة، إعدادات DPI، أو صيغ إخراج أخرى — كل تعديل يفتح بابًا جديدًا لإنشاء مصغرات، معاينات، أو لقطات أرشيفية.

هل أنت مستعد للتحدي التالي؟ جرّب تحويل مجموعة من عناوين URL بشكل متوازي، أو دمج هذه المنطق في خدمة microservice مبنية على Spring Boot تُعيد PNG عند الطلب. السماء هي الحد عندما تجمع بين مرونة Aspose.HTML وأدوات التزامن في Java.

برمجة سعيدة، ولا تنس مشاركة قصص نجاحك في التعليقات!

## ماذا يجب أن تتعلم بعد ذلك؟

- [كيفية استخدام Aspose لتحويل HTML إلى PNG – دليل خطوة بخطوة](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [كيفية تحويل HTML إلى PNG باستخدام Aspose – دليل كامل](/html/english/net/rendering-html-documents/how-to-render-html-to-png-with-aspose-complete-guide/)
- [كيفية تعديل CSS - تحرير CSS خارجي متقدم باستخدام Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
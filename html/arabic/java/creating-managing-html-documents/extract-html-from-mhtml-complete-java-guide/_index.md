---
category: general
date: 2026-04-19
description: استخراج HTML من MHTML بسرعة باستخدام Java. تعلم كيفية تحويل MHTML إلى
  HTML، استخراج محتوى البريد الإلكتروني، كتابة السلسلة إلى ملف، ومعالجة تحويل MHT.
draft: false
keywords:
- extract html from mhtml
- convert mhtml to html
- extract email body
- write string to file
- convert mht to html
language: ar
og_description: استخراج HTML من MHTML في جافا. يوضح هذا الدليل كيفية تحويل MHTML إلى
  HTML، استخراج محتوى البريد الإلكتروني، وكتابة السلسلة إلى ملف.
og_title: استخراج HTML من MHTML – جافا خطوة بخطوة
tags:
- Java
- Aspose.HTML
- Email Processing
title: استخراج HTML من MHTML – دليل جافا الكامل
url: /ar/java/creating-managing-html-documents/extract-html-from-mhtml-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج HTML من MHTML – دليل Java كامل

هل احتجت يوماً إلى **استخراج HTML من MHTML** لكن لم تكن متأكدًا من أين تبدأ؟ ربما استلمت بريدًا مؤرّخًا (`.mht`) وتريد الحصول على النص النظيف للمعاينة على الويب، أو أنك تبني سكريبت ترحيل يحول الأرشيفات القديمة إلى صفحات HTML حديثة. في كلتا الحالتين، المشكلة هي نفسها: لديك أرشيف ويب بملف واحد وتحتاج إلى الحصول على شفرة HTML الخام منه.

الخبر السار؟ ببضع أسطر من Java ومكتبة Aspose.HTML يمكنك **تحويل MHTML إلى HTML**، استخراج جسم البريد، وحتى كتابة تلك السلسلة إلى ملف—كل ذلك دون مغادرة بيئة التطوير المتكاملة (IDE). في هذا الدرس سنستعرض العملية بالكامل، نشرح لماذا كل خطوة مهمة، ونظهر لك كيفية التعامل مع الحالات الشائعة مثل الموارد المفقودة أو الترميزات غير UTF‑8.

> **ملخص سريع:** بنهاية هذا الدليل ستتمكن من **استخراج جسم البريد الإلكتروني**، **تحويل MHTML إلى HTML**، و**كتابة السلسلة إلى ملف** باستخدام مقتطف نظيف قابل لإعادة الاستخدام يعمل مع أي ملف `.mht` أو `.mhtml` تطرحه عليه.

---

## ما ستحتاجه

قبل أن نبدأ، تأكد من وجود التالي:

- **Java 17+** (الكود يستخدم نمط try‑with‑resources المتاح منذ Java 7، لكن Java 17 هو الإصدار طويل الدعم الحالي).
- **Aspose.HTML for Java** ملفات JAR على مسار الفئة (classpath). يمكنك الحصول عليها من [موقع Aspose](https://products.aspose.com/html/java/) أو عبر Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

- ملف عينة **`.mht` أو `.mhtml`** تريد معالجته. في المثال سنسميه `email.mht` ونضعه في `YOUR_DIRECTORY`.

هذا كل شيء—لا أطر إضافية، لا محللات ثقيلة. مجرد Java عادي ومكتبة موثقة جيدًا.

## الخطوة 1 – فتح ملف MHTML كتيار (Stream)

أول ما نفعله هو فتح البريد المؤرّخ كـ `InputStream`. استخدام التيار يحافظ على استهلاك الذاكرة منخفضًا، خاصةً للملفات الكبيرة `.mht` التي قد تحتوي على صور أو CSS مدمجة.

```java
// Step 1: Open the MHTML file as a stream
try (InputStream mhtmlStream = new FileInputStream("YOUR_DIRECTORY/email.mht")) {
    // Subsequent steps go inside this block
}
```

**لماذا التيار؟**  
التيار يسمح لـ `MhtmlDocument` بقراءة البيانات أثناء التنفيذ، مما يعني أنك لن تواجه `OutOfMemoryError` حتى لو كان الأرشيف عدة ميغابايت. كما يمنحك المرونة لقراءة البيانات من مصادر أخرى لاحقًا (مثل `ByteArrayInputStream` من قاعدة بيانات).

## الخطوة 2 – تحميل مستند MHTML من التيار

الآن نمرر التيار إلى فئة `MhtmlDocument` الخاصة بـ Aspose. هذه الفئة تحلل الأرشيف المشفر بـ MIME وتبني تمثيلًا شبيهًا بـ DOM للـ HTML المدمج.

```java
// Step 2: Load the MHTML document from the stream
MhtmlDocument mhtmlDoc = new MhtmlDocument(mhtmlStream);
```

**ما يحدث في الخلفية:**  
Aspose يستخرج كل جزء MIME (HTML، صور، CSS) ويعيد تجميعها داخليًا. لهذا يمكنك لاحقًا طلب الجزء HTML فقط دون القلق بشأن الموارد المدمجة.

## الخطوة 3 – استرجاع محتوى HTML الرئيسي

بعد تحميل المستند، استخراج الـ HTML الخام يصبح سطرًا واحدًا. طريقة `getHtmlContent()` تُعيد النص كـ `String`، مع الحفاظ على العلامات الأصلية.

```java
// Step 3: Retrieve the main HTML content as a string
String htmlContent = mhtmlDoc.getHtmlContent();
```

**ما ستحصل عليه:**  
`htmlContent` يحتوي على صفحة HTML كاملة—بما في ذلك وسمي `<head>` و `<body>`—تمامًا كما ظهرت عندما تم حفظ البريد. إذا كنت تحتاج فقط للجزء الظاهر، يمكنك لاحقًا تحليله باستخدام Jsoup وإزالة `<head>`.

## الخطوة 4 – كتابة HTML المستخرج إلى ملف منفصل

حفظ السلسلة إلى القرص أمر بسيط باستخدام واجهة `java.nio.file`. هذه الخطوة توضح نمط **كتابة السلسلة إلى ملف** الذي يعمل على أي منصة.

```java
// Step 4: Save the extracted HTML to a separate file
Files.writeString(Path.of("YOUR_DIRECTORY/email_body.html"), htmlContent);
```

**نصيحة:**  
إذا كنت تحتاج إلى مجموعة أحرف محددة، استخدم `Files.writeString(Path, CharSequence, Charset)`. الافتراضي هو UTF‑8، وهو مناسب لمعظم رسائل البريد الحديثة.

## الخطوة 5 – تأكيد عملية الاستخراج

استخدام `System.out.println` سريعًا يتيح لك التحقق من أن كل شيء تم دون استثناءات. في بيئة الإنتاج ستستبدل ذلك بتسجيل مناسب.

```java
// Step 5: Indicate successful extraction
System.out.println("HTML extracted.");
```

عند تشغيل البرنامج، يجب أن ترى `HTML extracted.` في وحدة التحكم، وسيظهر الملف `email_body.html` في `YOUR_DIRECTORY`.

## مثال كامل جاهز للتنفيذ

لنجمع كل ما سبق، إليك الفئة Java الكاملة المستقلة. يمكنك نسخها ولصقها في IDE ثم الضغط على **Run**.

```java
import com.aspose.html.MhtmlDocument;
import java.io.FileInputStream;
import java.io.InputStream;
import java.nio.file.Files;
import java.nio.file.Path;

public class MhtmlToHtmlConverter {

    public static void main(String[] args) {
        // Adjust the path to point to your .mht/.mhtml file
        String sourcePath = "YOUR_DIRECTORY/email.mht";
        String targetPath = "YOUR_DIRECTORY/email_body.html";

        // Try-with-resources ensures the stream is closed automatically
        try (InputStream mhtmlStream = new FileInputStream(sourcePath)) {

            // Load the MHTML document
            MhtmlDocument mhtmlDoc = new MhtmlDocument(mhtmlStream);

            // Extract the HTML content
            String htmlContent = mhtmlDoc.getHtmlContent();

            // Write the HTML string to a new file
            Files.writeString(Path.of(targetPath), htmlContent);

            // Simple confirmation output
            System.out.println("HTML extracted to " + targetPath);
        } catch (Exception e) {
            // In real code you might want to log this instead of printing
            System.err.println("Failed to extract HTML: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### النتيجة المتوقعة

تشغيل البرنامج يطبع شيئًا مثل:

```
HTML extracted to YOUR_DIRECTORY/email_body.html
```

وسيحتوي `email_body.html` على الشيفرة HTML الكاملة للبريد الأصلي. افتحه في متصفح—سترى نفس العرض البصري للرسالة المؤرخة (باستثناء أي موارد خارجية لم تُضمّن).

## التعامل مع الحالات الشائعة

### 1. الموارد المدمجة المفقودة

أحيانًا يشير ملف MHTML إلى صور خارجية لم تُحفظ داخل الأرشيف. في هذه الحالة لا يزال `getHtmlContent()` يُعيد وسم `<img src="...">`، لكن الروابط ستشير إلى الموقع الأصلي على الويب. إذا كنت تحتاج إلى ملف HTML مكتمل ذاتيًا، يمكنك:

- استخدام `MhtmlDocument.save(Path, SaveFormat.HTML)` للسماح لـ Aspose باستخراج جميع الموارد إلى مجلد.
- أو معالجة الـ HTML لاحقًا بمكتبة مثل **Jsoup** لاستبدال الروابط البعيدة ببيانات URI مشفرة بصيغة base64.

### 2. الترميزات غير UTF‑8

إذا تم حفظ بريدك بترميز مختلف (مثل `windows-1252`)، قد تحتوي السلسلة المسترجعة على أحرف غير صحيحة. يمكنك فرض مجموعة أحرف معينة عند الكتابة:

```java
Files.writeString(
    Path.of(targetPath),
    htmlContent,
    StandardCharsets.ISO_8859_1
);
```

### 3. الملفات الكبيرة

للأرشيفات التي تتجاوز بضع مئات من الميغابايت، فكر في بث مخرجات HTML مباشرة إلى `BufferedWriter` بدلاً من تحميل السلسلة بالكامل في الذاكرة. كما توفر Aspose طريقة **`save`** التي تكتب مباشرة إلى ملف، متجاوزةً الـ `String` الوسيط.

## نصائح احترافية وأفضل الممارسات

- **أعد استخدام كائن `MhtmlDocument`** إذا كنت بحاجة لاستخراج أجزاء متعددة (مثل CSS أو الصور). فهو يحلل الأرشيف مرة واحدة فقط.
- **تحقق من صحة المخرجات** باستخدام مدقق HTML (مدقق W3C أو `jsoup.isValid()`) إذا كنت ستدخل الـ HTML في نظام آخر.
- **سجل الأحداث بدلاً من الطباعة** في بيئة الإنتاج. استبدل `System.out.println` بإطار تسجيل مثل SLF4J لتسجيل الطوابع الزمنية ومستويات الخطورة.
- **تحكم في إصدارات الاعتمادات**. تصدر Aspose تحديثات متكررة؛ احرص على تثبيت الإصدار في `pom.xml` لتجنب تغييرات مفاجئة قد تكسر الكود.

## الخلاصة

لقد استعرضنا حلًا عمليًا من البداية إلى النهاية **لاستخراج HTML من MHTML** باستخدام Java. بفتح الأرشيف كتيار، تحميله عبر Aspose.HTML، استخراج سلسلة الـ HTML، و**كتابة السلسلة إلى ملف**، أصبح لديك الآن طريقة موثوقة **لتحويل MHTML إلى HTML**، **استخراج جسم البريد**، وحتى **تحويل MHT إلى HTML** للمعالجة اللاحقة.

لا تتردد في تعديل المقتطف: استبدل `FileInputStream` بـ `ByteArrayInputStream` إذا كانت الأرشيفات مخزنة في قاعدة بيانات، أو دمج الكود في مهمة دفعة أكبر تعالج عشرات الرسائل في آن واحد. الفكرة الأساسية تبقى نفسها—دع مكتبة متخصصة تتولى الجزء الصعب، ثم تعامل مع النص العادي كما تحتاج.

**الخطوات التالية** التي قد تستكشفها:

- استخدم Jsoup **لتنظيف الـ HTML المستخرج** (إزالة بكسلات التتبع، CSS مضمن، إلخ).
- أتمتة **التحويل الجماعي** عبر حلقة تمر على دليل يحتوي على ملفات `.mht`.
- دمج ذلك مع **Apache POI** لتضمين الـ HTML المنظف في مستندات Word أو PDF.

هل لديك أسئلة حول حالة معينة أو تريد مشاركة كيفية توسيع السكريبت؟ اترك تعليقًا أدناه—برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
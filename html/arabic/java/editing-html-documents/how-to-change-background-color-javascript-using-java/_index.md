---
category: general
date: 2026-09-29
description: تغيير لون الخلفية باستخدام جافاسكريبت في ملف HTML عبر جافا. تعلم كيفية
  تحميل HTML في جافا، تشغيل جافاسكريبت داخل HTML، وتعديل HTML باستخدام جافا لتغيير
  خلفية الصفحة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change background color javascript
- load html in java
- run js in html
- modify html with java
- set page background
language: ar
lastmod: 2026-09-29
og_description: تغيير لون الخلفية باستخدام جافا سكريبت في صفحة HTML باستخدام Java.
  يوضح لك هذا الدرس كيفية تحميل HTML في Java، تشغيل JavaScript في HTML، وتعيين خلفية
  الصفحة برمجيًا.
og_image_alt: Screenshot of Java code that changes the page background color
og_title: تغيير لون الخلفية باستخدام جافاسكريبت وجافا – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Change background color javascript in an HTML file using Java. Learn
    to load html in java, run js in html, and modify html with java for a new page
    background.
  headline: How to change background color javascript using Java
  type: TechArticle
tags:
- Java
- HTMLUnit
- JavaScript
- HTML manipulation
title: كيفية تغيير لون الخلفية باستخدام جافا سكريبت وجافا
url: /ar/java/editing-html-documents/how-to-change-background-color-javascript-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تغيير لون الخلفية باستخدام JavaScript في Java

إذا كنت بحاجة إلى **تغيير لون الخلفية باستخدام JavaScript** في ملف HTML موجود، يمكنك القيام بذلك بالكامل من خلال Java دون فتح متصفح. يوضح لك هذا الدليل كيفية **تحميل HTML في Java**، وتنفيذ مقتطف صغير من JavaScript، ثم **تعديل HTML باستخدام Java** بحيث يتم تحديث خلفية الصفحة.

يعمل الحل مع مكتبة **HTMLUnit** مفتوحة المصدر، التي توفر متصفحًا بدون واجهة يمكنه تقييم JavaScript بنفس دقة المتصفح الحقيقي. بحلول نهاية هذا الدليل ستحصل على طريقة قابلة لإعادة الاستخدام **تضبط خلفية الصفحة** إلى أي لون تختاره.

## المتطلبات المسبقة

| ما تحتاجه | لماذا يهم |
|-----------|-----------|
| Java 8 أو أحدث | HTMLUnit تتطلب على الأقل Java 8. |
| أداة بناء Maven أو Gradle | لسحب تبعية HTMLUnit تلقائيًا. |
| ملف HTML تريد تحريره (مثال: `input.html`) | المستند المصدر الذي سيتم تحميله وتعديله. |

أضف HTMLUnit إلى مشروعك:

*Maven*  

```xml
<dependency>
    <groupId>net.sourceforge.htmlunit</groupId>
    <artifactId>htmlunit</artifactId>
    <version>2.71.0</version>
</dependency>
```

*Gradle*  

```gradle
implementation 'net.sourceforge.htmlunit:htmlunit:2.71.0'
```

> **نصيحة احترافية:** استخدم أحدث نسخة مستقرة من HTMLUnit للحصول على أكثر محرك JavaScript دقة.

## تغيير لون الخلفية باستخدام JavaScript – تحميل HTML في Java

الخطوة الأولى هي تحميل مستند HTML إلى كائن `HTMLPage`. هذا يمنحك واجهة برمجة تطبيقات شبيهة بـ DOM وسياق تنفيذ JavaScript.

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;

public class BackgroundColorChanger {

    /**
     * Loads an HTML file from the given path.
     *
     * @param htmlPath absolute or relative path to the source HTML file
     * @return HtmlPage representing the loaded document
     * @throws IOException if the file cannot be read
     */
    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        // WebClient acts as a headless browser; disabling CSS speeds up loading.
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);

        // Convert the file path to a URL that HTMLUnit can understand.
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }
}
```

*لماذا هذا مهم*: `WebClient` ينشئ بيئة معزولة حيث يمكن تشغيل JavaScript، لذا يمكنك **تشغيل js في html** بنفس الطريقة التي يعمل بها متصفح المستخدم.

## تشغيل js في html لتعيين خلفية الصفحة

بمجرد تحميل الصفحة، يمكنك تقييم أي تعبير JavaScript. المقتطف أدناه يغيّر نمط `backgroundColor` للعنصر `<body>`.

```java
/**
 * Executes JavaScript that changes the page background color.
 *
 * @param page   the HtmlPage loaded earlier
 * @param color  any valid CSS color string, e.g., "lightblue" or "#ffcc00"
 */
private static void changeBackground(HtmlPage page, String color) {
    // The eval method runs JavaScript in the page's context.
    String script = "document.body.style.backgroundColor = '" + color + "';";
    page.getEnclosingWindow().getScriptableObject().eval(script);
}
```

*شرح*:
- `document.body.style.backgroundColor` هو الخاصية القياسية في DOM لخلفية الصفحة.
- من خلال استدعاء `eval`، نحن **نشغل js في html** دون الحاجة إلى نافذة متصفح حقيقية.
- الطريقة قابلة لإعادة الاستخدام لأي لون، وتلبي متطلب **تعيين خلفية الصفحة**.

## تعديل html باستخدام java وحفظ النتيجة

بعد تشغيل السكريبت، يعكس الـ DOM النمط الجديد. يمكنك الآن كتابة الـ HTML المحدث إلى القرص.

```java
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Saves the modified HTML content to a new file.
 *
 * @param page          the HtmlPage that has been altered
 * @param outputPath    destination file path
 * @throws IOException  if writing fails
 */
private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
    // page.asXml() returns the current HTML markup, including the changed style.
    String updatedHtml = page.asXml();
    Files.write(Paths.get(outputPath), updatedHtml.getBytes());
}
```

جمع كل شيء معًا يمنحك برنامجًا واحدًا قابلاً للتنفيذ:

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;

public class BackgroundColorChanger {

    public static void main(String[] args) {
        // Adjust these paths for your environment.
        String inputFile = "YOUR_DIRECTORY/input.html";
        String outputFile = "YOUR_DIRECTORY/js_modified.html";
        String newColor = "lightblue"; // Change to any CSS color you need.

        try {
            HtmlPage page = loadHtml(inputFile);
            changeBackground(page, newColor);
            saveModifiedHtml(page, outputFile);
            System.out.println("Background color changed to '" + newColor + "' and saved to " + outputFile);
        } catch (IOException e) {
            System.err.println("Error processing HTML file: " + e.getMessage());
        }
    }

    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }

    private static void changeBackground(HtmlPage page, String color) {
        String script = "document.body.style.backgroundColor = '" + color + "';";
        page.getEnclosingWindow().getScriptableObject().eval(script);
    }

    private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
        String updatedHtml = page.asXml();
        Files.write(Paths.get(outputPath), updatedHtml.getBytes());
    }
}
```

### المخرجات المتوقعة

تشغيل البرنامج يطبع:

```
Background color changed to 'lightblue' and saved to YOUR_DIRECTORY/js_modified.html
```

فتح `js_modified.html` في أي متصفح يظهر الصفحة بخلفية زرقاء فاتحة، مما يؤكد أن عملية **تغيير لون الخلفية باستخدام JavaScript** نجحت.

## الاختلافات الشائعة وحالات الحافة

| الحالة | كيفية التعامل |
|--------|----------------|
| **تنسيقات ألوان مختلفة** | مرّر أي قيمة متوافقة مع CSS (`"red"`, `"#ff0000"`, `"rgb(255,0,0)"`). |
| **غياب وسم `<body>`** | سيفشل السكريبت بصمت؛ يمكنك أولاً التأكد من وجود `<body>` باستخدام `page.getFirstByXPath("//body")`. |
| **ملفات HTML الكبيرة** | عطّل CSS (`setCssEnabled(false)`) وفعل فقط ميزات JavaScript التي تحتاجها لتقليل استهلاك الذاكرة. |
| **تشغيل سكريبتات متعددة** | استدعِ `changeBackground` بشكل متكرر أو أنشئ طريقة مساعدة تقبل قائمة من أوامر JavaScript. |

## الخلاصة

أنت الآن تعرف كيف **تغيير لون الخلفية باستخدام JavaScript** عن طريق تحميل ملف HTML في Java، **تشغيل js في html**، و**تعديل html باستخدام java** لت **تعيين خلفية الصفحة** إلى أي لون تختاره. المثال الكامل أعلاه يعمل مع أحدث مكتبة HTMLUnit ويمكن دمجه في خطوط أتمتة أكبر، مثل معالجة تقارير HTML على دفعات أو إعداد قوالب البريد الإلكتروني.

**الخطوات التالية**
- استكشف عمليات تعديل DOM الأخرى (مثل إدراج عناصر، إزالة سكريبتات).
- اجمع هذه الطريقة مع أداة توليد PDF لإنشاء ملفات PDF للصفحات ذات الأنماط.
- جرّب استخدام محرك headless مختلف مثل Selenium WebDriver إذا كنت بحاجة إلى محاكاة كاملة للمتصفح.

برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [احصل على النمط المحسوب Java – استخراج لون الخلفية من HTML](/html/english/java/css-html-form-editing/get-computed-style-java-extract-background-color-from-html/)
- [كيفية تحميل HTML، ضبط DPI للجهاز وقراءة لون الخلفية](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [إنشاء HTML من JavaScript في Java – دليل خطوة بخطوة كامل](/html/english/java/creating-managing-html-documents/generate-html-from-javascript-in-java-complete-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
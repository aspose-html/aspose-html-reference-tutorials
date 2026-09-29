---
category: general
date: 2026-09-29
description: تعلم كيفية اختيار العناصر حسب الفئة، وقراءة HTML من ملف، وإيجاد الروابط
  الخارجية في جافا. يغطي هذا الدليل خطوة بخطوة تكرار NodeList بكفاءة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- select elements by class
- read html from file
- find external links
- iterate nodelist java
- use queryselectorall java
language: ar
lastmod: 2026-09-29
og_description: حدد العناصر حسب الفئة في Java، اقرأ HTML من ملف، وابحث عن الروابط
  الخارجية باستخدام querySelectorAll. اتبع المثال الكامل لتكرار NodeList.
og_image_alt: Screenshot showing Java code that selects elements by class from an
  HTML file
og_title: اختر العناصر حسب الفئة في جافا – دليل كامل مع querySelectorAll
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to select elements by class, read HTML from file, and find
    external links in Java. This step‑by‑step guide covers iterating a NodeList efficiently.
  headline: How to select elements by class in Java using querySelectorAll
  type: TechArticle
- questions:
  - answer: Yes. `Jsoup.parse` treats the input as a fragment and automatically adds
      missing root elements, allowing selectors to work on the fragment’s body.
    question: Does this work with HTML fragments that lack a `<html>` root?
  - answer: The standard Java DOM API (`org.w3c.dom`) does not include `querySelectorAll`.
      Libraries such as **HTMLUnit** or **jodd-lagarto** provide similar methods.
      The pattern shown here—load, select with CSS, iterate—remains the same.
    question: Can I use `querySelectorAll` without jsoup?
  - answer: 'After obtaining each `Element`, you can call `link.attr("href", "newUrl")`
      and then write the document back to disk with `Files.writeString`. ## Conclusion
      You now know how to **select elements by class**, **read HTML from file**, **find
      external links**, and **iterate a NodeList in Java** using `qu'
    question: What if I need to modify the links instead of just printing them?
  type: FAQPage
tags:
- Java
- HTML parsing
- DOM manipulation
title: كيفية اختيار العناصر حسب الفئة في جافا باستخدام querySelectorAll
url: /ar/java/creating-managing-html-documents/how-to-select-elements-by-class-in-java-using-queryselectora/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية اختيار العناصر حسب الفئة في Java باستخدام querySelectorAll

إذا كنت بحاجة إلى **select elements by class** أثناء معالجة ملف HTML في Java، فإن هذا الدليل يوضح لك بالضبط كيفية القيام بذلك. ستتعلم كيفية قراءة HTML من ملف، واستخدام `querySelectorAll` للعثور على الروابط الخارجية، وتكرار `NodeList` الناتج بأمان.

التعامل مع HTML في Java غالبًا ما يبدو ثقيلًا، لكن المكتبات الحديثة توفر لك واجهة برمجة تطبيقات مختصرة تعتمد على محددات CSS. المثال أدناه يستخدم **jsoup** (الإصدار 1.17.2) لأنه ينفذ محددات على نمط `querySelectorAll` ويعيد مجموعة `Elements` تتصرف مثل `NodeList`. يمكنك تعديل نفس المنطق لتطبيقات DOM أخرى إذا لزم الأمر.

## المتطلبات المسبقة

* JDK 17 أو أحدث مثبت.
* Maven أو Gradle لإدارة الاعتمادات.
* إلمام أساسي بـ Java streams ونموذج DOM.

Add jsoup to your project:

```xml
<!-- Maven -->
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

```gradle
// Gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

## الخطوة 1: قراءة HTML من ملف

المهمة الأولى هي تحميل مستند HTML من القرص. `Jsoup.parse(Path, Charset)` يقرأ الملف ويبني شجرة DOM يمكنك الاستعلام عنها.

```java
import java.nio.file.Paths;
import java.nio.charset.StandardCharsets;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class HtmlLoader {
    /**
     * Loads an HTML file and returns a Jsoup Document.
     *
     * @param filePath absolute or relative path to the HTML file
     * @return parsed Document ready for DOM queries
     * @throws IOException if the file cannot be read
     */
    public static Document load(String filePath) throws IOException {
        return Jsoup.parse(Paths.get(filePath).toFile(),
                           StandardCharsets.UTF_8.name(),
                           "");
    }
}
```

*لماذا هذا مهم*: تحميل الملف مرة واحدة يجنب عمليات I/O المتكررة أثناء تكرار العناصر لاحقًا. كائن `Document` يحتفظ بـ DOM الكامل، مما يتيح استعلامات محددات سريعة.

## الخطوة 2: استخدام `querySelectorAll` لاختيار العناصر حسب الفئة

الآن بعد أن أصبح المستند في الذاكرة، يمكنك **select elements by class** باستخدام محدد CSS. المحدد `"a.external"` يطابق وسوم `<a>` التي تحمل الفئة `external`—وهو بالضبط ما تحتاجه **للعثور على الروابط الخارجية**.

```java
import org.jsoup.select.Elements;
import org.jsoup.nodes.Element;

/**
 * Returns all anchor elements with the CSS class "external".
 *
 * @param doc the parsed HTML document
 * @return a collection of matching Elements
 */
public static Elements findExternalLinks(Document doc) {
    // querySelectorAll is simulated by the select() method in Jsoup
    return doc.select("a.external");
}
```

*لماذا هذا مهم*: استخدام محدد الفئة هو تعبيري وفعال. المكتبة تترجم المحدد إلى تجوال محسّن، لذا لا تحتاج إلى كتابة حلقات يدوية على كل عقدة.

## الخطوة 3: تكرار NodeList (Elements) في Java

`Elements` تنفذ `Iterable<Element>`، مما يعني أنه يمكنك استخدام حلقة `for‑e​ach` القياسية **iterate NodeList Java**. الحلقة أدناه تطبع سمة `href` لكل رابط.

```java
/**
 * Prints the href attribute of every external link.
 *
 * @param externalLinks collection returned by findExternalLinks()
 */
public static void printExternalLinks(Elements externalLinks) {
    for (Element link : externalLinks) {
        System.out.println("External link: " + link.attr("href"));
    }
}
```

*لماذا هذا مهم*: التكرار المباشر يحافظ على قابلية قراءة الكود ويتجنب عبء تحويل المجموعة إلى stream عندما تحتاج فقط إلى إخراج بسيط.

## مثال كامل يعمل

جمع الخطوات الثلاث معًا ينتج برنامجًا مستقلًا يمكنك تشغيله من سطر الأوامر.

```java
import java.io.IOException;
import org.jsoup.nodes.Document;
import org.jsoup.select.Elements;

public class ExternalLinkExtractor {

    public static void main(String[] args) {
        // Validate input
        if (args.length != 1) {
            System.err.println("Usage: java ExternalLinkExtractor <input.html>");
            System.exit(1);
        }

        String inputPath = args[0];

        try {
            // Step 1: read HTML from file
            Document doc = HtmlLoader.load(inputPath);

            // Step 2: select elements by class (find external links)
            Elements externalLinks = findExternalLinks(doc);

            // Step 3: iterate NodeList Java and print hrefs
            printExternalLinks(externalLinks);
        } catch (IOException e) {
            System.err.println("Error reading file: " + e.getMessage());
        }
    }

    // Reuse methods from previous sections
    private static Elements findExternalLinks(Document doc) {
        return doc.select("a.external");
    }

    private static void printExternalLinks(Elements externalLinks) {
        for (org.jsoup.nodes.Element link : externalLinks) {
            System.out.println("External link: " + link.attr("href"));
        }
    }
}
```

### النتيجة المتوقعة

بافتراض أن `input.html` يحتوي على:

```html
<a class="external" href="https://example.com">Example</a>
<a class="internal" href="/about">About</a>
<a class="external" href="https://openai.com">OpenAI</a>
```

تشغيل البرنامج يطبع:

```
External link: https://example.com
External link: https://openai.com
```

## نصائح احترافية ومخاطر شائعة

* **Encoding matters** – دائمًا اقرأ الملف بـ UTF‑8 (أو مجموعة الأحرف التي تتطابق مع المصدر). الترميز غير الصحيح قد يفسد الأحرف في قيم السمات.
* **Multiple classes** – إذا كان للعنصر عدة فئات (مثال: `class="btn external"`)، فإن المحدد `"a.external"` لا يزال يطابق لأنه في CSS يتم فحص وجود الرمز، وليس السلسلة الكاملة.
* **Performance tip** – إذا كنت بحاجة فقط إلى سمة `href`، يمكنك طلبها مباشرة باستخدام `doc.select("a.external[href]").eachAttr("href")`. هذا يتجنب إنشاء كائنات `Element` كاملة لكل تطابق.
* **Null safety** – `link.attr("href")` تُعيد سلسلة فارغة إذا كانت السمة مفقودة، لذا لا تحتاج إلى فحص null قبل الطباعة.

## الأسئلة المتكررة

**س: هل يعمل هذا مع مقاطع HTML التي تفتقد جذر `<html>`؟**  
ج: نعم. `Jsoup.parse` يتعامل مع الإدخال كقطعة ويضيف تلقائيًا العناصر الجذرية المفقودة، مما يسمح للمحددات بالعمل على جسم القطعة.

**س: هل يمكنني استخدام `querySelectorAll` بدون jsoup؟**  
ج: واجهة برمجة تطبيقات DOM القياسية في Java (`org.w3c.dom`) لا تتضمن `querySelectorAll`. مكتبات مثل **HTMLUnit** أو **jodd-lagarto** توفر طرقًا مشابهة. النمط المعروض هنا—التحميل، الاختيار باستخدام CSS، التكرار—يبقى هو نفسه.

**س: ماذا لو احتجت لتعديل الروابط بدلاً من مجرد طباعتها؟**  
ج: بعد الحصول على كل `Element`، يمكنك استدعاء `link.attr("href", "newUrl")` ثم كتابة المستند مرة أخرى إلى القرص باستخدام `Files.writeString`.

## الخلاصة

أنت الآن تعرف كيف **select elements by class**، **read HTML from file**، **find external links**، و **iterate a NodeList in Java** باستخدام محددات على نمط `querySelectorAll`. المثال الكامل يوضح سير عمل نظيف وجاهز للإنتاج يمكنك دمجه في خطوط تجريف أو تحويل أكبر.

بعد ذلك، استكشف المواضيع ذات الصلة مثل **parsing dynamic content with HTMLUnit**، **writing modified HTML back to disk**، أو **using Java streams to collect link URLs into a list**. كل من هذه يبني على التقنية الأساسية لاختيار العناصر حسب الفئة التي تم توضيحها هنا. Happy coding!

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to query HTML in Java – Select elements, filter by attribute, and get text](/html/english/java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/)
- [Iterate NodeList Java – Read HTML & Get Image src](/html/english/java/creating-managing-html-documents/iterate-nodelist-java-read-html-get-image-src/)
- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-10-28
description: تعلم كيفية فتح الروابط في علامة تبويب جديدة عن طريق تحليل HTML في جافا،
  والعثور على الروابط الخارجية وإضافة `target="_blank"`.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- open links new tab
- find external links
- add target blank
- parse html in java
- save modified html
language: ar
lastmod: 2026-10-28
og_description: 'فتح الروابط في علامة تبويب جديدة باستخدام جافا: تحليل HTML، العثور
  على الروابط الخارجية، إضافة target="_blank"، وحفظ HTML المعدل.'
og_image_alt: Screenshot of Java code that parses HTML and updates external links
  to open in a new tab
og_title: فتح الروابط في علامة تبويب جديدة باستخدام جافا – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to open links in a new tab by parsing HTML in Java, finding
    external links and adding target blank.
  headline: How to open links in a new tab with Java
  type: TechArticle
tags:
- Java
- HTML parsing
- jsoup
- web automation
title: كيفية فتح الروابط في علامة تبويب جديدة باستخدام جافا
url: /ar/java/editing-html-documents/how-to-open-links-in-a-new-tab-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية فتح الروابط في علامة تبويب جديدة باستخدام Java

إذا كنت بحاجة إلى **فتح الروابط في علامة تبويب جديدة** من ملف HTML ثابت، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك. ستتعلم **تحليل HTML في Java**، **العثور على الروابط الخارجية**، **إضافة target blank**، و**حفظ HTML المعدل** دون مغادرة بيئة التطوير المتكاملة الخاصة بك.

فتح الروابط الخارجية في علامة تبويب جديدة للمتصفح يحسن تجربة المستخدم ويُبقي الزوار على الصفحة الأصلية. الحل أدناه يعمل مع أي مستند HTML، ويتطلب فقط مكتبة jsoup الشهيرة، ويعمل على Java 8 أو أحدث.

## المتطلبات المسبقة

* تم تثبيت JDK 8 +
* أداة بناء (Maven أو Gradle) لجلب تبعية **jsoup**
* ملف HTML يحتوي على وسوم الربط مع الفئة `external`

لا تحتاج إلى خادم ويب أو أطر إضافية—jsoup يتعامل مع كل شيء محليًا.

## الخطوة 1: إعداد jsoup في مشروعك

أضف jsoup كاعتماد. إذا كنت تستخدم Maven، ضع هذا في `pom.xml`:

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

لـ Gradle، أضف السطر التالي إلى `build.gradle`:

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

هذه الإحداثيات تجلب أحدث إصدار مستقر (اعتبارًا من أكتوبر 2026). بعد المزامنة، يمكنك استيراد فئات `org.jsoup` في ملفات مصدر Java الخاصة بك.

## الخطوة 2: تحليل مستند HTML

تحليل الملف هو الخطوة الأولى نحو **فتح الروابط في علامة تبويب جديدة**. طريقة `Jsoup.parse` تقرأ الملف إلى بنية شبيهة بـ DOM قابلة للتعديل.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // Load the HTML document from disk
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");
        
        // Continue with link processing...
    }
}
```

*لماذا هذا مهم*: `Document` يمنحك محددات بنمط CSS، مما يجعل من السهل تحديد العناصر التي تحتاجها.

## الخطوة 3: العثور على الروابط الخارجية

الآن حدد كل عنصر `<a>` يحمل الفئة `external`. هذا يطابق متطلب **العثور على الروابط الخارجية**.

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

// Inside main after parsing:
Elements externalLinks = doc.select("a.external");
```

`Elements` هي مجموعة من العقد المتطابقة. إذا أعاد المحدد مجموعة فارغة، فإن HTML الخاص بك إما يفتقر إلى الفئة أو يستخدم تسمية مختلفة—قم بتعديل المحدد وفقًا لذلك.

## الخطوة 4: إضافة `target="_blank"` إلى كل رابط

لكل عقدة يتم إرجاعها بواسطة **العثور على الروابط الخارجية**، اضبط سمة `target` إلى `_blank`. هذا يحقق خطوة **إضافة target blank** ويضمن أن المتصفحات تفتح الرابط في علامة تبويب جديدة.

```java
for (Element link : externalLinks) {
    link.attr("target", "_blank");
}
```

طريقة `attr` تستبدل أي قيمة `target` موجودة، مما يضمن سلوكًا متسقًا عبر جميع الروابط الخارجية.

## الخطوة 5: حفظ HTML المعدل

بعد تحديث DOM، اكتب التغييرات مرة أخرى إلى ملف. هذا يكمل جزء **حفظ HTML المعدل** من الدرس.

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

// Still inside main:
Path output = Path.of("YOUR_DIRECTORY/updated.html");
Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
System.out.println("Updated file written to " + output);
```

`doc.outerHtml()` تسلسل المستند بالكامل، مع الحفاظ على المسافات والتنسيق كما قام jsoup بتحليله أصلاً.

## مثال عملي كامل

جمع جميع الخطوات معًا ينتج برنامجًا مستقلًا يمكنك نسخه، لصقه، وتشغيله.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

/**
 * Updates all external links so they open in a new tab.
 */
public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // 1️⃣ Parse the HTML file
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");

        // 2️⃣ Find external links (a.external)
        Elements externalLinks = doc.select("a.external");

        // 3️⃣ Add target="_blank" to each link
        for (Element link : externalLinks) {
            link.attr("target", "_blank");
        }

        // 4️⃣ Save the modified HTML
        Path output = Path.of("YOUR_DIRECTORY/updated.html");
        Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
        System.out.println("Updated file written to " + output);
    }
}
```

### النتيجة المتوقعة

افترض أن `sample.html` يحتوي على:

```html
<a href="https://example.com" class="external">Example</a>
<a href="/internal/page.html">Internal</a>
```

بعد تشغيل البرنامج، سيحتوي `updated.html` على:

```html
<a href="https://example.com" class="external" target="_blank">Example</a>
<a href="/internal/page.html">Internal</a>
```

فقط الرابط الخارجي حصل على سمة `target="_blank"`، مما يعني أن المتصفحات ستفتحها الآن في علامة تبويب جديدة.

## نصائح احترافية ومشكلات شائعة

* **نصيحة احترافية:** إذا كنت بحاجة إلى اعتبار الروابط التي تبدأ بـ `http://` أو `https://` كروابط خارجية حتى بدون فئة CSS، قم بتوسيع المحدد: `doc.select("a[href^=http]")`.
* **حالة حدية:** بعض الصفحات تحدد بالفعل `target="_self"`؛ استدعاء `attr` يستبدله، مما يضمن سلوكًا متسقًا.
* **الأداء:** بالنسبة لملفات HTML الكبيرة جدًا، فكر في التحليل المتدفق (`Jsoup.parse(File, String, String, Parser.htmlParser())`) لتقليل استهلاك الذاكرة.
* **الاختبار:** تحقق من النتيجة بفتح `updated.html` في المتصفح وفحص الرابط باستخدام أدوات المطور—ابحث عن سمة `target`.

## الخلاصة

أصبح لديك الآن حل كامل وقابل للتنفيذ لـ **فتح الروابط في علامة تبويب جديدة** باستخدام Java. يغطي الدرس كيفية **تحليل html في java**، **العثور على الروابط الخارجية**، **إضافة target blank**، و**حفظ html المعدل**، كل ذلك باستخدام مكتبة jsoup الخفيفة.

من هنا يمكنك:

* توسيع المحدد للتعامل مع أنماط روابط أخرى (مثل `rel="external"`).  
* دمج هذه المنطق مع خطوة بناء تعالج جميع ملفات HTML في المشروع.  
* دمج الكود في خط أنابيب إدارة محتوى أكبر.

لا تتردد في تجربة محددات أو صيغ إخراج مختلفة، ومشاركة نتائجك مع المجتمع!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [كيفية استخدام CSS في Java – تحميل HTML، عد الروابط وتقييم XPath](/html/english/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/)
- [كيفية تحليل HTML في Java – استخراج النص من مقالات HTML](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [إنشاء عنصر HTML جديد باستخدام Java – دليل Aspose.HTML الكامل](/html/english/java/editing-html-documents/create-new-html-element-with-java-full-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
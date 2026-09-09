---
category: general
date: 2026-01-01
description: تعلم كيفية استعلام HTML باستخدام Java، وكيفية اختيار CSS، واستخراج العناصر
  من HTML مع أمثلة عملية وحساب عدد العقد.
draft: false
keywords:
- how to query html
- how to select css
- extract elements from html
- select multiple css classes
- how to count nodes
language: ar
og_description: أتقن كيفية استعلام HTML في جافا، وتعلم كيفية اختيار CSS، واستخراج
  العناصر من HTML، وعدّ العقد باستخدام أمثلة حقيقية للكود.
og_title: كيفية استعلام HTML في جافا – دليل كامل
tags:
- Java
- HTML parsing
- Aspose.HTML
title: كيفية استعلام HTML في جافا – دليل كامل
url: /ar/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية الاستعلام عن HTML في جافا – دليل كامل

هل تساءلت يومًا **كيف تستعلم عن HTML** من برنامج جافا دون أن تشد شعر رأسك؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى استخراج البيانات من كتالوج ثابت أو جمع صفحة بسيطة، وتبدو الحيل التقليدية للـ DOM غير مريحة.  

الأخبار السارة؟ ببضع أسطر من الشيفرة يمكنك تحميل ملف HTML، تشغيل استعلامات XPath أو CSS، وحتى عدّ العقد التي تهمك—كل ذلك في تدفق واحد منظم. في هذا الدليل سنستعرض **كيفية الاستعلام عن HTML**، **كيفية اختيار CSS**، وسنظهر لك كيف **استخراج العناصر من HTML**، **اختيار عدة فئات CSS**، و**كيفية عدّ العقد** باستخدام Aspose.HTML for Java.

## ما ستتعلمه

- تحميل مستند HTML من القرص أو من عنوان URL.  
- استخدام XPath للعثور على العناصر التي تطابق شروطًا معقدة.  
- تطبيق محددات CSS، بما في ذلك استعلامات الفئات المتعددة.  
- عدّ النتائج برمجيًا.  
- نصائح، فخاخ، وتنوعات للسيناريوهات الواقعية.

*المتطلبات المسبقة*: Java 8+، Maven أو Gradle، ونسخة من مكتبة Aspose.HTML for Java (الإصدار التجريبي المجاني يكفي للتجربة).

---

![مثال على كيفية الاستعلام عن HTML](https://example.com/images/query-html.png "لقطة شاشة تُظهر كيفية الاستعلام عن HTML باستخدام جافا")

## كيفية الاستعلام عن HTML – تحميل المستند

قبل أن تتمكن من طرح أي أسئلة، تحتاج إلى كائن مستند لتستجوبه. فئة `HTMLDocument` في Aspose.HTML تقوم بالعمل الشاق.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.Element;
import java.util.List;

public class QueryDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document you want to query
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/catalog.html");
```

> **لماذا هذا مهم** – تحميل الملف ينشئ شجرة DOM في الذاكرة. من هناك يمكنك تشغيل استعلامات XPath وCSS دون القلق بشأن تأخر الشبكة أو العلامات غير الصالحة. إذا لم يُعثر على الملف، تُطلق Aspose استثناء واضح `FileNotFoundException`، مما يجعل عملية التصحيح سهلة.

### نصيحة احترافية
إذا كنت تجلب HTML من موقع بعيد، ما عليك سوى تمرير سلسلة URL إلى `HTMLDocument`—ستقوم Aspose بجلبه وتحليله لك.

## كيفية اختيار CSS – باستخدام محددات CSS

بمجرد أن يصبح DOM جاهزًا، اختيار العقد باستخدام CSS يصبح بسيطًا كالسطر الواحد. دعنا نأخذ كل عنصر يحمل إما الفئة `featured` أو `highlight`.

```java
        // Step 2: Locate elements marked as featured or highlighted using a CSS selector
        List<Element> featuredElements = document.selectCss(".featured, .highlight");

        // Step 3: Output the number of elements found by the CSS selector
        System.out.println("Featured elements: " + featuredElements.size());
```

> **شرح** – المحدد `.featured, .highlight` يخبر المحرك بإرجاع *أي* عنصر يحتوي على سمة `class` فيها `featured` **أو** `highlight`. هذه هي الطريقة القياسية **لاختيار عدة فئات CSS** في استعلام واحد.

### حالة حافة
إذا كان العنصر يحتوي على كلا الفئتين (مثال: `<div class="featured highlight">`)، سيظهر **مرة واحدة** في قائمة النتائج، مما يمنع العد المزدوج.

## استخراج العناصر من HTML – دمج XPath وCSS

يتألق XPath عندما تحتاج إلى منطق علاقاتي، مثل "كل عقد `<book>` حيث السعر يتجاوز 30". إليك المقتطف الدقيق من المثال الأصلي:

```java
        // Step 4: Find all <book> elements with a price greater than 30 using XPath
        List<Element> expensiveBooks = document.selectXPath("//book[price>30]");

        // Step 5: Output the number of books that match the XPath query
        System.out.println("Expensive books count: " + expensiveBooks.size());
```

> **لماذا XPath؟** – يمكن لـ XPath تقييم المقارنات العددية (`price>30`) مباشرة، وهو ما لا يستطيع CSS فعله. كما يسمح لك بالتنقل بين العلاقات الأب/ابن دون كتابة شيفرة إضافية.

### تنويع
إذا كنت بحاجة لجلب *عناوين* تلك الكتب المكلفة، يمكنك ربط استعلام ثانٍ:

```java
        List<Element> titles = expensiveBooks.get(0).selectXPath("./title");
        System.out.println("First expensive book title: " + titles.get(0).getTextContent());
```

## اختيار عدة فئات CSS – حيل المتحدد المتقدم

أحيانًا تريد استهداف عناصر **في الوقت نفسه** لديها عدة فئات، مثل `class="product featured"`. صيغة CSS لهذا هي محدد متسلسل بدون فواصل.

```java
        // Example: select <div> elements that are both .product and .featured
        List<Element> productFeatured = document.selectCss("div.product.featured");
        System.out.println("Product‑featured divs: " + productFeatured.size());
```

> **نقطة أساسية** – لا توجد مساحة بين أسماء الفئات؛ وجود مساحة يعني “سليل”. هذا النمط أساسي عندما **تختار عدة فئات CSS** تعمل معًا لتنسيق مكوّن ما.

## كيفية عدّ العقد – الحصول على إجماليات دقيقة

عدّ العقد غالبًا ما يكون الخطوة الأخيرة في خط أنابيب استخراج البيانات. لقد رأيت بالفعل `list.size()` يُستخدم بعد كل استعلام، لكن دعنا نغلفه في مساعد قابل لإعادة الاستخدام.

```java
    /**
     * Returns the count of elements that match the given CSS selector.
     */
    private static int countByCss(HTMLDocument doc, String selector) {
        return doc.selectCss(selector).size();
    }

    /**
     * Returns the count of elements that match the given XPath expression.
     */
    private static int countByXPath(HTMLDocument doc, String xpath) {
        return doc.selectXPath(xpath).size();
    }

    public static void main(String[] args) throws Exception {
        HTMLDocument doc = new HTMLDocument("YOUR_DIRECTORY/catalog.html");

        System.out.println("Expensive books: " + countByXPath(doc, "//book[price>30]"));
        System.out.println("Featured items: " + countByCss(doc, ".featured, .highlight"));
        System.out.println("Product‑featured divs: " + countByCss(doc, "div.product.featured"));
    }
```

> **لماذا نغلفه؟** – تجميع منطق العد يجعل شيفرتك أسهل للاختبار ويقلل التكرار. كما يوضح **كيفية عدّ العقد** للقراء المستقبليين.

### فخاخ شائعة
- **المسافات في سمات الفئة** – `"featured "` (مسافة نهائية) لا تزال تتطابق مع `.featured` لأن المحدد يزيل المسافات الزائدة.  
- **حساسية الحالة** – أسماء فئات HTML حساسة لحالة الأحرف في وضع XML؛ تأكد من أن HTML المصدر يستخدم حالة موحدة.

## مثال عملي كامل

نجمع كل شيء معًا، إليك برنامجًا مستقلًا يمكنك نسخه ولصقه في بيئتك التطويرية:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.Element;
import java.util.List;

public class QueryDemo {

    private static int countByCss(HTMLDocument doc, String selector) {
        return doc.selectCss(selector).size();
    }

    private static int countByXPath(HTMLDocument doc, String xpath) {
        return doc.selectXPath(xpath).size();
    }

    public static void main(String[] args) throws Exception {
        // Load the HTML file (adjust the path as needed)
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/catalog.html");

        // XPath: books priced over 30
        int expensiveBooks = countByXPath(document, "//book[price>30]");
        System.out.println("Expensive books count: " + expensiveBooks);

        // CSS: featured or highlighted elements
        int featured = countByCss(document, ".featured, .highlight");
        System.out.println("Featured elements: " + featured);

        // CSS: elements that are both .product and .featured
        int productFeatured = countByCss(document, "div.product.featured");
        System.out.println("Product‑featured divs: " + productFeatured);
    }
}
```

**الناتج المتوقع** (مع افتراض وجود `catalog.html` نموذجي):

```
Expensive books count: 4
Featured elements: 7
Product‑featured divs: 2
```

إذا كان ملفك يحتوي على عدد أقل من العقد المتطابقة، ستتعدل الأرقام وفقًا لذلك—بدون مفاجآت.

---

## الخلاصة

غطّينا **كيفية الاستعلام عن HTML** باستخدام Aspose.HTML for Java، وأظهرنا **كيفية اختيار CSS**، وشرحنا **استخراج العناصر من HTML**، وتناولنا **اختيار عدة فئات CSS**، وبيّنّا **كيفية عدّ العقد** بشكل موثوق.  

النقطة الأساسية؟ تحميل المستند مرة واحدة ثم إعادة استخدام نفس كائن `HTMLDocument` يتيح لك دمج استعلامات XPath وCSS دون عقبات أداء.  

هل أنت مستعد للخطوة التالية؟ جرّب ربط المحددات لسحب قيم السمات (`@href`, `@src`) أو تصدير مجموعة النتائج إلى JSON للمعالجة اللاحقة. يمكنك أيضًا استكشاف معالجة الصفحات المتعددة إذا كان HTML المصدر يمتد عبر عدة صفحات.

هل لديك محدد صعب أو حالة حافة لا تستطيع حلها؟ اترك تعليقًا أدناه، ولنحلّها معًا. استمتع بالاستعلام!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-03-04
description: كيفية تمييز HTML بالبحث عن نص داخل HTML وتغليف كل تطابق بعلامة <mark>.
  دليل Java خطوة بخطوة لاستبدال النص بعناصر <mark>.
draft: false
keywords:
- how to highlight html
- search text in html
- highlight word in html
- highlight occurrences of word
- replace text with mark
language: ar
og_description: كيفية تمييز HTML عن طريق البحث عن نص في HTML وتغليف التطابقات بعلامة
  <mark>. مثال كامل بلغة Java لاستبدال النص بوسم <mark>.
og_title: كيفية تمييز HTML – البحث عن النص واستبداله بـ <mark>
tags:
- Aspose.HTML
- Java
- Text Processing
title: كيفية تمييز HTML – البحث عن النص واستبداله بـ <mark>
url: /ar/java/editing-html-documents/how-to-highlight-html-search-text-replace-with-mark/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمييز HTML – البحث عن النص واستبداله بـ `<mark>`

هل تساءلت يومًا **كيف تميّز HTML** عندما تظهر كلمة معينة عدة مرات؟ ربما تقوم ببناء موقع توثيق، أو محرك مدونة، أو فقط تحتاج إلى إبراز اسم علامة تجارية في صفحة ثابتة. الخبر السار؟ الأمر بسيط جدًا بمجرد أن تعرف كيفية البحث عن النص في HTML وتغليف النتائج بعنصر `<mark>`.

في هذا الدرس سنستعرض حلًا كاملاً بلغة Java يقوم بتحميل ملف HTML، يبحث عن كلمة مستهدفة، يستبدل كل ظهور لها بعلامة `<mark>`، وأخيرًا يحفظ النسخة المميّزة. بنهاية الدرس ستتمكن من **تمييز كلمة في HTML**، **تمييز تكرارات كلمة**، وحتى **استبدال النص بـ mark** دون الإخلال بالعلامات المحيطة.

> **ما ستحتاجه**  
> • Java 17 أو أحدث (الكود يعمل مع الإصدارات السابقة أيضًا)  
> • مكتبة Aspose.HTML for Java (نسخة تجريبية مجانية أو نسخة مرخصة)  
> • ملف HTML بسيط تريد معالجته  

إذا كان لديك هذه المتطلبات، لنبدأ.

![لقطة شاشة تُظهر مخرجات HTML المميّزة – كيفية تمييز html](/images/highlight-html-example.png "مثال على كيفية تمييز html")

## الخطوة 1 – تحميل مستند HTML (كيفية تمييز HTML)

أولاً نحتاج إلى جلب الملف المصدر إلى الذاكرة. فئة `Document` في Aspose.HTML تقوم بكل العمل الشاق، حيث تقوم بتحليل العلامات إلى بنية شبيهة بـ DOM يمكننا الاستعلام عنها.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.util.List;

public class HighlightAspose {
    public static void main(String[] args) throws Exception {

        // Load the original HTML file
        Document document = new Document("YOUR_DIRECTORY/article.html");
```

**لماذا هذا مهم:** تحميل المستند يزودنا بنموذج كائن نظيف، مما يسمح لنا بالتلاعب بعقد النص بأمان دون القلق من كسر العلامات أو السمات. كما أنه يطبع الفراغات، مما يجعل خطوة **search text in html** اللاحقة أكثر موثوقية.

## الخطوة 2 – البحث عن النص في HTML للكلمة المستهدفة

الآن بعد أن أصبح المستند جاهزًا، سنبحث عن كل ظهور للكلمة التي نريد إبرازها. تُعيد طريقة `searchText` قائمة من كائنات `TextMatch`، كل منها يصف موقع التطابق داخل الـ DOM.

```java
        // Define what we want to highlight
        String searchTerm = "Aspose";

        // Find all matches – this is the core of "search text in html"
        List<TextMatch> matches = document.searchText(searchTerm);
```

**نصيحة احترافية:** البحث حساس لحالة الأحرف بشكل افتراضي. إذا كنت بحاجة إلى بحث غير حساس لحالة الأحرف، حوّل كل من نص المستند و`searchTerm` إلى نفس الحالة قبل استدعاء `searchText`، أو استخدم نهجًا يعتمد على التعبيرات النمطية المتوفرة في المكتبة.

## الخطوة 3 – استبدال النص بـ `<mark>` (تمييز كلمة في HTML)

لكل تطابق سنعيد بناء نص العقدة المحتوية، مع إدخال عنصر `<mark>` حول الكلمة بالضبط. هذا يضمن أننا نؤثر فقط على النص المستهدف ونترك باقي HTML دون تعديل.

```java
        // Iterate over each match and wrap it with <mark>
        for (TextMatch match : matches) {
            Node parentNode = match.getNode();

            // Preserve text before and after the match
            String textBefore = parentNode.getTextContent()
                                          .substring(0, match.getStartOffset());
            String textAfter  = parentNode.getTextContent()
                                          .substring(match.getEndOffset());

            // Build the highlighted fragment
            String highlightedFragment = textBefore
                    + "<mark>" + match.getText() + "</mark>"
                    + textAfter;

            // Replace the node's content with the new fragment
            parentNode.setTextContent(highlightedFragment);
        }
```

**شرح:**  
- `getStartOffset`/`getEndOffset` يعطينا المواضع الدقيقة للأحرف المتطابقة داخل العقدة الأصلية.  
- عن طريق تقطيع النص الأصلي (`textBefore` و `textAfter`) نحافظ على كل ما تبقى كما هو.  
- تغليف التطابق بـ `<mark>` هو الطريقة القياسية لـ **replace text with mark** والحصول على تمييز المتصفح الأصلي دون الحاجة إلى CSS إضافي.

### حالات خاصة ونصائح

- **تعدد التطابقات في نفس العقدة:** الحلقة تعالج كل `TextMatch` بالتتابع. لأننا نستبدل محتوى العقدة بالكامل في كل مرة، فإن المواضع اللاحقة تتغير. تُعيد Aspose.HTML التطابقات بترتيب المستند، لذا يعمل الاستبدال البسيط في معظم الحالات. إذا صادفت تطابقات متداخلة، فكر في جمع جميع التطابقات أولًا، ثم إعادة بناء العقدة مرة واحدة.  
- **العناصر التي لا يمكنها احتواء HTML خام:** إذا كانت العقدة الأصلية `<script>` أو `<style>`، فإن إدخال `<mark>` سيكسر الصفحة. يمكنك تخطي تلك العقد بالتحقق من `parentNode.getNodeName()` قبل الاستبدال.

## الخطوة 4 – حفظ المستند المميّز (تمييز تكرارات كلمة)

بعد إتمام جميع الاستبدالات، نقوم بحفظ الـ DOM المعدل إلى القرص. سيحتوي ملف الإخراج على العلامات الأصلية بالإضافة إلى علامات `<mark>` الجديدة، مما يؤدي إلى **highlighting occurrences of word** “Aspose” بفعالية.

```java
        // Write the modified HTML back to a new file
        document.save("YOUR_DIRECTORY/highlighted.html");
    }
}
```

افتح `highlighted.html` في أي متصفح، وسترى كل كلمة “Aspose” محاطة بخلفية صفراء (النمط الافتراضي لـ `<mark>`). إذا رغبت في مظهر مخصص، أضف قاعدة CSS صغيرة:

```html
<style>
    mark { background-color: #fffa8b; color: #000; }
</style>
```

## أسئلة شائعة (Search Text in HTML – FAQs)

**س: ماذا لو ظهرت الكلمة داخل قيمة سمة؟**  
ج: `searchText` يبحث فقط في محتوى نص العقدة، وليس في سلاسل السمات. لتمييز قيم السمات تحتاج إلى iterating عبر العناصر وفحص السمات يدويًا.

**س: هل يمكنني تمييز عدة كلمات مختلفة في تمريرة واحدة؟**  
ج: بالتأكيد. أنشئ قائمة بالمصطلحات، وكرر العملية لكل منها، مع تطبيق نفس منطق الاستبدال. احرص فقط على التعامل مع التطابقات المتداخلة بحذر.

**س: هل يعمل هذا مع علامات HTML5‑only مثل `<section>` أو `<article>`؟**  
ج: نعم. Aspose.HTML يدعم بالكامل عناصر HTML5 الحديثة، لذا فإن traversing الـ DOM يعمل بغض النظر عن نوع العلامة.

## مثال كامل يعمل (جميع الخطوات مجمعة)

فيما يلي البرنامج الكامل بلغة Java جاهز للتنفيذ يوضح سير العمل بالكامل—من تحميل الملف إلى حفظ النتيجة المميّزة.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.util.List;

public class HighlightAspose {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document
        Document document = new Document("YOUR_DIRECTORY/article.html");

        // Step 2: Search for the word "Aspose"
        String searchTerm = "Aspose";
        List<TextMatch> matches = document.searchText(searchTerm);

        // Step 3: Wrap each found occurrence with a <mark> element
        for (TextMatch match : matches) {
            Node parentNode = match.getNode();
            String textBefore = parentNode.getTextContent()
                                          .substring(0, match.getStartOffset());
            String textAfter  = parentNode.getTextContent()
                                          .substring(match.getEndOffset());

            // Build the highlighted HTML fragment
            String highlightedFragment = textBefore
                    + "<mark>" + match.getText() + "</mark>"
                    + textAfter;
            parentNode.setTextContent(highlightedFragment);
        }

        // Step 4: Save the highlighted document
        document.save("YOUR_DIRECTORY/highlighted.html");
    }
}
```

**الناتج المتوقع:** افتح `highlighted.html` وسترى كل ظهور لكلمة “Aspose” مميّزًا. لا يتم تعديل أي جزء آخر من الصفحة، ويبقى الملف مستند HTML صالح.

## الخلاصة

لقد غطينا **كيفية تمييز HTML** عبر **searching text in HTML** برمجيًا، وتغليف كل تطابق بعلامة `<mark>`، ثم حفظ التغييرات. يتيح لك هذا النهج **تمييز كلمة في HTML**، **تمييز تكرارات كلمة**، و**استبدال النص بـ mark** دون كتابة كود هش لمعالجة السلاسل.

ما الخطوات التالية؟ جرّب توسيع السكريبت لت:

- قبول كلمة البحث كمعامل سطر أوامر.  
- توليد ملف CSS يحدد لون تمييز مخصص.  
- معالجة مجلد كامل من ملفات HTML دفعة واحدة.  

ستساعدك هذه التغييرات على تعميق فهمك لكل من Aspose.HTML API وأنماط معالجة النص العامة.

إذا واجهت أي صعوبات أو كان لديك أفكار لتحسينات إضافية، اترك تعليقًا أدناه. تمييز سعيد!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
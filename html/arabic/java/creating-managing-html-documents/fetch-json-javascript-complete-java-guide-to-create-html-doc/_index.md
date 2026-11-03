---
category: general
date: 2026-05-25
description: تعلم كيفية جلب JSON باستخدام JavaScript وعرض JSON في HTML في صفحة تم
  إنشاؤها بواسطة Java. دليل خطوة بخطوة لإنشاء عنصر body وعرض البيانات المسترجعة.
draft: false
keywords:
- fetch json javascript
- display json html
- display fetched data
- create body element
- create html document java
language: ar
og_description: جلب JSON باستخدام JavaScript بسهولة. يوضح هذا الدرس كيفية إنشاء مستند
  HTML باستخدام Java، إضافة عنصر body، وعرض البيانات المستلمة في HTML.
og_title: جلب JSON جافاسكريبت – دليل جافا لتوليد HTML
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Learn how to fetch json javascript and display json html in a Java‑generated
    page. Step‑by‑step guide to create body element and show fetched data.
  headline: fetch json javascript – Complete Java Guide to Create HTML Document
  type: TechArticle
- description: Learn how to fetch json javascript and display json html in a Java‑generated
    page. Step‑by‑step guide to create body element and show fetched data.
  name: fetch json javascript – Complete Java Guide to Create HTML Document
  steps:
  - name: Why This Works
    text: '- **`fetch`** is the modern, promise‑based API for HTTP requests in browsers.
      It replaces the older `XMLHttpRequest`. - The response is parsed as JSON with
      `r.json()`. - We create a `<pre>` element so the JSON appears nicely formatted
      (thanks to `JSON.stringify` with indentation). - Finally, we **di'
  - name: 1. Network Errors
    text: 'Even with the `.catch` we added, a failed request leaves the page empty.
      You might want a fallback UI:'
  - name: 2. Asynchronous Loading
    text: 'Our example runs the script as soon as the document is closed, which is
      fine for a demo. In production you might defer execution until `DOMContentLoaded`:'
  - name: 3. Styling the Output
    text: 'If you want the JSON to look prettier, add a quick CSS rule:'
  - name: 4. Multiple Requests
    text: Want to pull several endpoints? Wrap the fetch logic in a function and call
      it multiple times, or use `Promise.all` to run them in parallel.
  - name: Expected Result
    text: Open `scripted.html` and you should see a neatly formatted JSON block, exactly
      as shown earlier. The page itself contains no other content—just the **display
      json html** we programmed.
  type: HowTo
tags:
- Java
- Aspose.HTML
- JSON
- Web Scraping
title: جلب JSON جافاسكريبت – الدليل الكامل لجافا لإنشاء مستند HTML
url: /ar/java/creating-managing-html-documents/fetch-json-javascript-complete-java-guide-to-create-html-doc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# fetch json javascript – دليل Java الكامل لإنشاء مستند HTML

هل تساءلت يومًا كيف **fetch json javascript** من API عام وتضمين النتيجة مباشرةً في ملف HTML ثابت يتم إنشاؤه بواسطة Java؟ لست الوحيد الذي يحاول حل هذه المشكلة. في العديد من المشاريع—فكر في لوحات التحكم السريعة أو مولدات التقارير الآلية—تحتاج إلى سحب بيانات JSON و **display json html** دون تشغيل خادم ويب كامل.

هذا هو ما سنحله الآن. بنهاية هذا الدليل ستعرف كيف **create html document java**، وتضيف **create body element**، وتدرج `<script>` يقوم بـ **fetch json javascript**، وأخيرًا **display fetched data** داخل كتلة `<pre>` منسقة بشكل جميل. لا أسرار، مجرد مثال عملي يمكنك نسخه‑ولصقه.

## ما يغطيه هذا البرنامج التعليمي

- المتطلبات المسبقة: Java 8+، Maven، ومكتبة Aspose.HTML for Java.
- إنشاء مستند HTML خطوة بخطوة من الصفر.
- إضافة عنصر body وسكريبت يقوم بطلب `fetch`.
- حفظ الملف الناتج والتحقق من ظهور JSON في المتصفح.
- تعديلات اختيارية: معالجة الأخطاء، التنفيذ غير المتزامن مقابل المتزامن، ونصائح التنسيق.

إذا حاولت يومًا توليد HTML في الوقت الفعلي وانتهى بك الأمر بصفحة فارغة، سيوفر لك هذا الدليل ساعات من الجهد. لنبدأ.

---

## الخطوة 1: إعداد مشروعك واستيراد Aspose.HTML

قبل أن نتمكن من **create html document java**، نحتاج إلى مكتبة Aspose.HTML على مسار الفئة. أسهل طريقة هي استخدام Maven:

```xml
<!-- pom.xml snippet -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-html</artifactId>
        <version>23.10</version> <!-- Check for the latest version -->
    </dependency>
</dependencies>
```

> **نصيحة احترافية:** إذا لم تكن تستخدم Maven، قم بتحميل ملف JAR من موقع Aspose وأضفه إلى مسار بناء IDE الخاص بك.

بعد حل الاعتماد، يمكنك البدء في كتابة الشيفرة. افتح محرّكك المفضّل—IntelliJ IDEA، Eclipse، أو حتى VS Code—وأنشئ فئة Java جديدة تسمى `JsExecution`.

## الخطوة 2: **create html document java** – تهيئة مستند فارغ

أول شيء نقوم به هو إنشاء كائن `HTMLDocument` فارغ. فكر في ذلك كقماش جديد، تمامًا مثل فتح ملف Notepad جديد.

```java
import com.aspose.html.dom.*;
import com.aspose.html.services.*;

public class JsExecution {
    public static void main(String[] args) throws Exception {
        // Step 2: Create a new empty HTML document
        HTMLDocument doc = new HTMLDocument();
```

لماذا لا نكتب سلسلة HTML مباشرة؟ لأن واجهة برمجة تطبيقات DOM توفر لنا طرقًا آمنة من حيث النوع للتعامل مع العناصر، مما يضمن عدم إنتاج ترميز غير صالح عن طريق الخطأ.

## الخطوة 3: **create body element** – إضافة وسم `<body>`

المستند بدون `<body>` يكون غير مرئي تقريبًا في المتصفح. لنضيف واحدًا:

```java
        // Step 3: Add a <body> element to the document
        Element body = doc.createElement("body");
        doc.appendChild(body);
```

لاحظ أننا نستخدم `createElement` بدلاً من HTML الخام. هذا يضمن أن العنصر ينتمي إلى نفس المستند ويتجنب مشاكل النطاق التي قد تواجهها الأساليب القائمة على السلاسل النصية.

## الخطوة 4: **fetch json javascript** – إدراج `<script>` يجلب البيانات

الآن يأتي الجزء الشهي: مقطع JavaScript الذي **fetch json javascript** و **display fetched data**. سندمج السكريبت مباشرةً في DOM.

```java
        // Step 4: Insert a <script> element that fetches JSON data and displays it
        Element script = doc.createElement("script");
        script.setAttribute("type", "text/javascript");
        script.appendChild(doc.createTextNode(
                "fetch('https://jsonplaceholder.typicode.com/todos/1')\n" +
                "  .then(r => r.json())\n" +
                "  .then(data => {\n" +
                "    const pre = document.createElement('pre');\n" +
                "    pre.textContent = JSON.stringify(data, null, 2);\n" +
                "    document.body.appendChild(pre);\n" +
                "  })\n" +
                "  .catch(err => console.error('Fetch error:', err));"));
        body.appendChild(script);
```

### لماذا يعمل هذا

- **`fetch`** هو واجهة برمجة التطبيقات الحديثة القائمة على الوعود لإجراء طلبات HTTP في المتصفحات. يحل محل `XMLHttpRequest` القديم.
- يتم تحليل الاستجابة كـ JSON باستخدام `r.json()`.
- ننشئ عنصر `<pre>` حتى يظهر JSON منسقًا بشكل جميل (بفضل `JSON.stringify` مع مسافة بادئة).
- أخيرًا، نـ **display json html** عن طريق إلحاق `<pre>` إلى `document.body`.
- جملة `.catch` هي شبكة أمان: إذا فشل الاتصال الشبكي، ستظهر رسالة خطأ في وحدة التحكم بدلاً من توقف صامت.

## الخطوة 5: تشغيل السكريبت وحفظ الملف

تتعامل Aspose.HTML مع المستند كمتصفح افتراضي. لضمان تشغيل السكريبت (حتى وإن لم نحتاج النتيجة فورًا)، نغلق تدفق المستند، مما يجبر التنفيذ.

```java
        // Step 5: Trigger script execution (synchronous for demonstration)
        doc.getWindow().getDocument().close();

        // Step 6: Save the generated HTML file
        doc.save("scripted.html");
        System.out.println("HTML with fetched data saved as scripted.html");
    }
}
```

عند فتح `scripted.html` في أي متصفح حديث، سترى كتلة منسقة بشكل جميل تحتوي على شيء مثل:

```json
{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}
```

هذا هو الجزء المتعلق بـ **display fetched data** عمليًا.

## الخطوة 6: تشغيل البرنامج والتحقق من النتيجة

قم بالترجمة والتنفيذ:

```bash
mvn compile exec:java -Dexec.mainClass=JsExecution
```

يجب أن ترى رسالة في وحدة التحكم تؤكد إنشاء الملف. افتح `scripted.html` باستخدام Chrome أو Firefox أو Edge. إذا سارت الأمور بشكل صحيح، سيظهر JSON داخل كتلة `<pre>` مباشرةً تحت الـ body.

> **ملاحظة:** قد تمنع بعض إعدادات الأمان (مثل فتح ملف عبر `file://`) طلب `fetch` بسبب CORS. إذا واجهت صفحة فارغة، جرّب خدمة الملف عبر خادم HTTP محلي بسيط:

```bash
python -m http.server 8080
# Then navigate to http://localhost:8080/scripted.html
```

## معالجة الحالات الطرفية والمشكلات الشائعة

### 1. أخطاء الشبكة

حتى مع جملة `.catch` التي أضفناها، يترك الطلب الفاشل الصفحة فارغة. قد ترغب في واجهة احتياطية:

```javascript
.catch(err => {
    const msg = document.createElement('p');
    msg.textContent = 'Unable to load data. Please try again later.';
    document.body.appendChild(msg);
    console.error(err);
});
```

### 2. التحميل غير المتزامن

مثالنا ينفّذ السكريبت بمجرد إغلاق المستند، وهذا مناسب للعرض. في بيئة الإنتاج قد تفضّل تأخير التنفيذ حتى يحدث `DOMContentLoaded`:

```javascript
document.addEventListener('DOMContentLoaded', () => {
    // fetch logic here
});
```

### 3. تنسيق المخرجات

إذا أردت أن يبدو JSON أكثر جاذبية، أضف قاعدة CSS سريعة:

```java
Element style = doc.createElement("style");
style.appendChild(doc.createTextNode(
    "pre { background:#f4f4f4; padding:10px; border-radius:4px; font-family:monospace; }"));
head.appendChild(style);
```

لا تنس إنشاء عنصر `<head>` أولًا إذا لم تقم بذلك بعد.

### 4. طلبات متعددة

هل تريد سحب عدة نقاط نهاية؟ غلف منطق `fetch` داخل دالة واستدعها عدة مرات، أو استخدم `Promise.all` لتشغيلها بالتوازي.

## مثال كامل يعمل (جميع الخطوات مجمعة)

فيما يلي الملف المصدر الكامل الجاهز للتنفيذ. انسخه إلى `src/main/java/JsExecution.java` ونفّذه كما هو موضح سابقًا.

```java
import com.aspose.html.dom.*;
import com.aspose.html.services.*;

public class JsExecution {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new empty HTML document
        HTMLDocument doc = new HTMLDocument();

        // 2️⃣ Add a <head> (optional but useful for CSS)
        Element head = doc.createElement("head");
        doc.appendChild(head);

        // 3️⃣ Insert simple CSS to make the JSON look nice
        Element style = doc.createElement("style");
        style.appendChild(doc.createTextNode(
                "pre { background:#f9f9f9; padding:12px; border:1px solid #ddd; " +
                "border-radius:4px; font-family:monospace; overflow:auto; }"));
        head.appendChild(style);

        // 4️⃣ Add a <body> element – the place where we’ll inject data
        Element body = doc.createElement("body");
        doc.appendChild(body);

        // 5️⃣ <script> that **fetch json javascript** and **display fetched data**
        Element script = doc.createElement("script");
        script.setAttribute("type", "text/javascript");
        script.appendChild(doc.createTextNode(
                "fetch('https://jsonplaceholder.typicode.com/todos/1')\n" +
                "  .then(r => r.json())\n" +
                "  .then(data => {\n" +
                "    const pre = document.createElement('pre');\n" +
                "    pre.textContent = JSON.stringify(data, null, 2);\n" +
                "    document.body.appendChild(pre);\n" +
                "  })\n" +
                "  .catch(err => {\n" +
                "    const p = document.createElement('p');\n" +
                "    p.textContent = 'Failed to load data.';\n" +
                "    document.body.appendChild(p);\n" +
                "    console.error(err);\n" +
                "  });"));
        body.appendChild(script);

        // 6️⃣ Force execution and save the file
        doc.getWindow().getDocument().close();
        doc.save("scripted.html");
        System.out.println("HTML with fetched data saved as scripted.html");
    }
}
```

### النتيجة المتوقعة

افتح `scripted.html` ويجب أن ترى كتلة JSON منسقة بشكل جميل، تمامًا كما ظهر سابقًا. لا يحتوي الصفحة على أي محتوى آخر—فقط **display json html** الذي برمجناه.

## الخاتمة

لقد استعرضنا الآن سير عمل كامل لـ **fetch json javascript** باستخدام Java النقي وAspose.HTML. بدءًا من صفحة فارغة، **create html document java**، **create body element**، أدخلنا سكريبت يجلب البيانات من API عام، وأخيرًا **display fetched data** بتنسيق قابل للقراءة. النهج خفيف الوزن، لا يتطلب محرك قوالب خارجي، ويمكن توسيعه لتوليد تقارير، لوحات تحكم، أو حتى مواقع ثابتة.

ما الخطوة التالية؟ جرّب استبدال نقطة النهاية بخدمة REST الخاصة بك، أضف ترقيم الصفحات، أو أنشئ عدة صفحات في تشغيل واحد. يمكنك أيضًا استكشاف مكتبات التصيير على الجانب الخادم إذا احتجت إلى تخطيطات أكثر تعقيدًا.

هل لديك أسئلة حول معالجة الأخطاء أو التنسيق؟

## دروس ذات صلة

- [Create HTML Documents Asynchronously in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-html-documents-async/)
- [Create HTML Documents from String in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-html-documents-from-string/)
- [Create HTML File Java & Set Up Network Service (Aspose.HTML)](/html/english/java/configuring-environment/setup-network-service/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
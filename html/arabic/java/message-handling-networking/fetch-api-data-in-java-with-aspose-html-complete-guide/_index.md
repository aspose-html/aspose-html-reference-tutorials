---
category: general
date: 2026-05-28
description: جلب بيانات API في Java باستخدام Aspose.HTML – تعلم كيفية تنفيذ جافاسكريبت
  غير المتزامن، تشغيل سكريبت غير متزامن، وتعيين سمة DOM من JSON المسترجع.
draft: false
keywords:
- fetch api data
- execute async javascript
- run async script
- set dom attribute
- how to run async
language: ar
og_description: جلب بيانات API في جافا باستخدام Aspose.HTML. يوضح هذا الدرس كيفية
  تنفيذ جافاسكريبت غير المتزامن، تشغيل سكريبت غير متزامن، وتعيين سمة DOM من نتائج
  API.
og_title: جلب بيانات API في جافا – دليل Aspose.HTML خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: fetch api data in Java using Aspose.HTML – learn how to execute async
    javascript, run async script, and set dom attribute from fetched JSON.
  headline: fetch api data in Java with Aspose.HTML - Complete Guide
  type: TechArticle
- description: fetch api data in Java using Aspose.HTML – learn how to execute async
    javascript, run async script, and set dom attribute from fetched JSON.
  name: fetch api data in Java with Aspose.HTML - Complete Guide
  steps:
  - name: Expected Output
    text: '``` GitHub stars: 84327 ```'
  - name: What if the fetch call fails?
    text: 'The script will throw a JavaScript exception, which propagates to `ScriptEngine.evaluate`.
      You can catch it in Java:'
  - name: Can I fetch from a private API that requires authentication?
    text: 'Sure—just add the appropriate headers in the script:'
  - name: Does this work on older Java versions?
    text: Aspose.HTML ships with its own JavaScript engine, so you don’t need Nashorn
      or GraalVM. However, the `try‑with‑resources` syntax requires Java 7+. For Java
      6 you’d have to close the document manually.
  type: HowTo
tags:
- Java
- Aspose.HTML
- Async JavaScript
title: جلب بيانات API في جافا باستخدام Aspose.HTML - دليل كامل
url: /ar/java/message-handling-networking/fetch-api-data-in-java-with-aspose-html-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# جلب بيانات API في Java باستخدام Aspose.HTML – دليل كامل

هل تساءلت يومًا كيف **fetch api data** في Java دون مغادرة بيئة التطوير المتكاملة الخاصة بك؟ لست وحدك. يواجه العديد من المطورين جدارًا عندما يحتاجون إلى استدعاء خدمة عن بُعد من صفحة HTML تم عرضها بواسطة Aspose.HTML ثم سحب النتيجة مرة أخرى إلى Java.  

في هذا الدرس سنستعرض مثالًا عمليًا يقوم **executes async javascript**، ويشغّل **async script**، وأخيرًا **sets a DOM attribute** بالقيمة التي تم جلبها. في النهاية ستعرف بالضبط *how to run async* بشكل آمن وكيفية استرجاع البيانات التي تحتاجها.

## ما ستبنيه

سننشئ تطبيقًا صغيرًا على سطر الأوامر في Java يقوم بـ:

1. يحمّل ملف HTML يحتوي على دالة async.  
2. ينفّذ سكريبت يستخدم **fetch API** لاستدعاء نقطة النهاية العامة لـ GitHub.  
3. ينتظر حتى يتم حل الـ promise (حتى 10 ثوانٍ).  
4. يخزن عدد النجوم في سمة مخصصة `data-stars` على عنصر `<body>`.  
5. يقرأ تلك السمة مرة أخرى في Java ويطبعها.

لا توجد مكتبات عميل HTTP خارجية، ولا كود خيوط إضافي—فقط Aspose.HTML يتولى العمل.

## المتطلبات المسبقة

- **Java 17** أو أحدث (الكود يُترجم مع الإصدارات السابقة، لكن 17 هو LTS الحالي).  
- مكتبة **Aspose.HTML for Java** (الإصدار 23.9 أو أحدث).  
- ملف HTML بسيط (`async-page.html`) موجود في مكان ما على القرص الخاص بك.  
- اتصال بالإنترنت (استدعاء fetch يتوجه إلى `https://api.github.com`).  

إذا كان لديك مشروع Maven بالفعل، أضف تبعية Aspose.HTML:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

الآن، دعنا نغوص في الشيفرة.

## الخطوة 1: إعداد صفحة HTML

أولاً، أنشئ ملف HTML بسيط سيستضيف دالة async. لا تحتاج إلى أي تنسيق معقد—فقط وسم `<body>`.

```html
<!-- async-page.html -->
<!DOCTYPE html>
<html>
<head>
    <title>Async Demo</title>
</head>
<body>
    <!-- The script we’ll inject later will populate this attribute -->
</body>
</html>
```

احفظ هذا الملف في مكان يمكن الوصول إليه، مثلاً `C:/temp/async-page.html`. سيُستخدم المسار في شيفرة Java.

![مثال على جلب بيانات API](https://example.com/fetch-api-data.png "مثال على جلب بيانات API")

*نص بديل الصورة: مثال على جلب بيانات API يظهر مخرجات وحدة التحكم لعدد نجوم GitHub.*

## الخطوة 2: تحميل مستند HTML في Java

مع جاهزية ملف HTML، نفتحها باستخدام `HTMLDocument` من Aspose.HTML. يضمن كتلة `try‑with‑resources` التخلص السليم من المستند.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsExample {
    public static void main(String[] args) throws Exception {

        // Load the HTML page that contains an async function
        try (HTMLDocument doc = new HTMLDocument("C:/temp/async-page.html")) {
            // The rest of the steps go here...
        }
    }
}
```

لماذا نستخدم `HTMLDocument`؟ فهو يوفّر لنا DOM كامل الميزات، ومحرك JavaScript مدمج، وطريقة مريحة للتفاعل مع الصفحة من Java—كل ذلك دون تشغيل متصفح.

## الخطوة 3: كتابة السكريبت غير المتزامن

الآن نصنع مقطع JavaScript يقوم **fetches API data**، ينتظر الـ promise، ثم **sets a DOM attribute**. لاحظ استخدام `async/await`—نفس النمط الذي تكتبه في المتصفح.

```java
String script =
    "async function run() {" +
    "  const data = await fetch('https://api.github.com').then(r => r.json());" +
    "  document.body.setAttribute('data-stars', data.stargazers_count);" +
    "}" +
    "run();";
```

بعض النقاط التي يجب الإشارة إليها:

- الدالة `run` مُعلنة كـ `async`، لذا يمكننا `await` استدعاء `fetch`.  
- بعد تحليل JSON، نخزن `data.stargazers_count` في سمة مخصصة `data-stars`.  
- أخيرًا نستدعي `run()` فورًا.  

هذا السكريبت الصغير يقوم بكل ما نحتاجه لـ **run async script** والتقاط النتيجة.

## الخطوة 4: تنفيذ السكريبت والانتظار

يمكن لـ `ScriptEngine` من Aspose.HTML تقييم JavaScript مع مهلة زمنية. بتمرير `10000` نخبر المحرك بالانتظار حتى **10 ثوانٍ** لإكمال العملية غير المتزامنة.

```java
// Execute the script and wait (up to 10 seconds) for the async operation to finish
ScriptEngine engine = doc.getScriptEngine();
engine.evaluate(script, 10000);   // timeout in milliseconds
```

إذا استغرق الطلب وقتًا أطول من المهلة، يُطرح استثناء `ScriptException`—وهو مثالي للتعامل مع ظروف الشبكة غير المستقرة. في بيئة الإنتاج قد تغلف ذلك بـ try‑catch وتعيد المحاولة حسب الحاجة.

## الخطوة 5: استرجاع السمة من Java

بعد إكمال السكريبت، تصبح سمة `data-stars` الآن جزءًا من DOM. استرجعها إلى Java باستدعاء بسيط:

```java
// Retrieve the value set by the script from the document
String stars = doc.getBody().getAttribute("data-stars");
System.out.println("GitHub stars: " + stars);
```

يطبع هذا السطر شيئًا مثل `GitHub stars: 12345`. يتغيّر الرقم الفعلي يوميًا، لكن النمط يبقى نفسه.

## مثال كامل يعمل

بدمج جميع الأجزاء معًا، إليك البرنامج الكامل الجاهز للتنفيذ:

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML page that contains an async function
        try (HTMLDocument doc = new HTMLDocument("C:/temp/async-page.html")) {

            // Step 2: Define a script that calls the async function and stores the result in a DOM attribute
            String script =
                "async function run() {" +
                "  const data = await fetch('https://api.github.com').then(r => r.json());" +
                "  document.body.setAttribute('data-stars', data.stargazers_count);" +
                "}" +
                "run();";

            // Step 3: Execute the script and wait (up to 10 seconds) for the async operation to finish
            ScriptEngine engine = doc.getScriptEngine();
            engine.evaluate(script, 10000);

            // Step 4: Retrieve the value set by the script from the document
            String stars = doc.getBody().getAttribute("data-stars");
            System.out.println("GitHub stars: " + stars);
        }
    }
}
```

### النتيجة المتوقعة

```
GitHub stars: 84327
```

(سيتفاوت رقمك؛ الجزء المهم هو أن القيمة هي **string** تمثل عدد النجوم.)

## أسئلة شائعة وحالات خاصة

### ماذا لو فشل استدعاء fetch؟

سيرمي السكريبت استثناء JavaScript، والذي ينتقل إلى `ScriptEngine.evaluate`. يمكنك التقاطه في Java:

```java
try {
    engine.evaluate(script, 10000);
} catch (ScriptException e) {
    System.err.println("Failed to fetch data: " + e.getMessage());
}
```

### هل يمكنني جلب بيانات من API خاص يتطلب المصادقة؟

بالطبع—فقط أضف الرؤوس المناسبة في السكريبت:

```javascript
await fetch('https://api.example.com/secure', {
    headers: { 'Authorization': 'Bearer YOUR_TOKEN' }
}).then(r => r.json());
```

تذكر إبقاء الأسرار خارج نظام التحكم بالمصادر.

### هل يعمل هذا على إصدارات Java القديمة؟

تأتي Aspose.HTML بمحرك JavaScript الخاص بها، لذا لا تحتاج إلى Nashorn أو GraalVM. ومع ذلك، يتطلب بناء `try‑with‑resources` Java 7+. بالنسبة لـ Java 6 سيتعين عليك إغلاق المستند يدويًا.

## نصائح احترافية

- **Reuse the ScriptEngine**: إذا كنت بحاجة لتشغيل العديد من السكريبتات غير المتزامنة، احتفظ بنسخة واحدة من المحرك حية—يقلل ذلك من الحمل.  
- **Increase the timeout** للـ APIs الأبطأ، لكن لا تضبطه إلى `Integer.MAX_VALUE`؛ ما زلت تريد شبكة أمان.  
- **Validate the attribute** قبل استخدامها. قد تكون سمة DOM `null` إذا لم يُنفّذ السكريبت أبدًا.  
- **Log the raw JSON** أثناء التطوير؛ يساعد ذلك عندما يتغيّر شكل الـ API.

## الخطوات التالية

الآن بعد أن عرفت كيفية **fetch api data**، يمكنك توسيع النمط:

- **Parse more complex JSON** وإدخال سمات متعددة.  
- **Create tables** داخل صفحة HTML بناءً على البيانات المستخرجة.  
- **Combine with Aspose.PDF** لإنشاء PDF يحتوي على نتائج API مباشرة.  

كل من هذه يبني على نفس الأفكار الأساسية: **execute async javascript**، **run async script**، و **set dom attribute** من النتيجة. لا تتردد في التجربة—هناك الكثير من القوة المخفية في محرك السكريبت الخاص بـ Aspose.HTML.

*برمجة سعيدة! إذا واجهت أي مشاكل، اترك تعليقًا أدناه وسنقوم بحلها معًا.*

## دروس ذات صلة

- [كيفية تشغيل JavaScript في Java – دليل كامل](/html/english/java/advanced-usage/how-to-run-javascript-in-java-complete-guide/)
- [إضافة عنصر إلى الـ Body باستخدام Aspose.HTML for Java ومراقب تعديل DOM](/html/english/java/advanced-usage/dom-mutation-observer-observing-node-additions/)
- [كيفية ضبط مهلة – إدارة مهلة الشبكة في Aspose.HTML for Java](/html/english/java/message-handling-networking/network-timeout/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
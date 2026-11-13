---
category: general
date: 2026-10-09
description: تعلم كيفية استدعاء Java من JavaScript باستخدام Aspose.HTML، تشغيل JavaScript
  غير المتزامن، وجلب JSON في Java مع مثال كامل ونصائح عملية.
keywords:
- how to call java from javascript
- async fetch api java
- asynchronous javascript fetch example
- call java method from javascript
lastmod: 2026-10-09
og_description: تعلم كيفية استدعاء Java من JavaScript باستخدام Aspose.HTML، تشغيل
  JavaScript غير المتزامن مع fetch API، ومعالجة ردود JSON في Java. مثال كامل ونصائح
  لاستكشاف الأخطاء وإصلاحها.
og_image_alt: Diagram showing Java invoking JavaScript, async fetch returning JSON,
  and Java callback handling
og_title: كيفية استدعاء Java من JavaScript باستخدام fetch غير المتزامن ومحرك JS
schemas:
- author: Aspose
  dateModified: '2026-10-09'
  description: Learn how to call Java from JavaScript using Aspose.HTML, run async
    JavaScript, and fetch JSON in Java with a complete example and practical tips.
  headline: ''
  type: TechArticle
- description: Learn how to call Java from JavaScript using Aspose.HTML, run async
    JavaScript, and fetch JSON in Java with a complete example and practical tips.
  name: ''
  steps:
  - name: The **asynchronous fetch API** successfully retrieved data.
    text: The **asynchronous fetch API** successfully retrieved data.
  - name: The JSON was serialized and handed over to Java.
    text: The JSON was serialized and handed over to Java.
  - name: Our **execute javascript engine** call completed without deadlocks.
    text: Our **execute javascript engine** call completed without deadlocks.
  type: HowTo
- questions:
  - answer: Yes. Any engine that supports host objects (e.g., Nashorn, GraalVM) can
      work, but Aspose.HTML provides a full browser‑like environment with built‑in
      `fetch`.
    question: Can I use this approach with other JavaScript engines?
  - answer: Serialize the object to JSON on the Java side and let JavaScript parse
      it, or expose multiple simple methods on the host object to pass individual
      fields.
    question: What if I need to return a complex Java object instead of a string?
  - answer: Aspose.HTML follows the WHATWG Fetch Standard, handling redirects, CORS,
      and streaming exactly as modern browsers do.
    question: Is the `fetch` implementation fully standards‑compliant?
  - answer: No. The `execute` call returns immediately; the internal engine processes
      the promise asynchronously. The main thread stays alive until the script finishes
      or you shut down the engine.
    question: Does this block the Java thread while waiting for the network?
  - answer: Use the `JavaScriptEngine.setDebugMode(true)` method to output console
      messages to the Java logger.
    question: How can I debug the JavaScript code inside the engine?
  type: FAQPage
tags:
- java
- javascript
- aspose.html
- async programming
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استدعاء Java من JavaScript باستخدام fetch غير المتزامن ومحرك JS

في هذا البرنامج التعليمي ستكتشف **كيفية استدعاء Java من JavaScript** باستخدام Aspose.HTML، تشغيل JavaScript غير المتزامن باستخدام **fetch API** الحديثة، واسترجاع بيانات JSON مرة أخرى إلى Java. المثال يعمل بالكامل داخل مستند HTML مدعوم بـ Java—بدون خادم ويب خارجي أو مكتبات إضافية. في النهاية ستحصل على مقتطف جاهز للتنفيذ يوضح جسرًا نظيفًا بين Java و JavaScript، مثالي للتصيير من جانب الخادم أو سيناريوهات البرمجة المخصصة.

## إجابات سريعة
- **ما الذي يدرسه هذا البرنامج التعليمي؟** استدعاء Java من JavaScript، استخدام fetch غير المتزامن، ومعالجة ردود JSON في Java.  
- **ما المكتبة المطلوبة؟** Aspose.HTML for Java (الإصدار 23.7 أو أحدث).  
- **هل أحتاج إلى خادم ويب؟** لا، كل شيء يعمل محليًا داخل عملية Java.  
- **هل يتم دعم fetch API؟** نعم، Aspose.HTML يطبق معيار WHATWG Fetch.  
- **هل يمكنني إعادة استخدام كائن المضيف؟** بالتأكيد—قم بإنشاء أي طريقة Java عامة تحتاجها.

## كيفية استدعاء Java من JavaScript باستخدام Aspose.HTML؟

حمّل مستند HTML الخاص بك، عرّف كائن مضيف Java، اكتب دالة `async` تستخدم `fetch`، ونفّذ السكريبت. المحرك يحل الـ promise، يستدعي رد Java، ويعيد نتيجة JSON—all without blocking the main thread. يتيح لك هذا النهج إبقاء جانب Java مستجيب بينما يقوم كود JavaScript بعمليات I/O الشبكية، ويعمل بنفس طريقة المتصفح.

## ما هو async fetch API في Java؟

async fetch API هو طريقة متوافقة مع المتصفحات تُعيد `Promise`. باستخدام `await` يمكنك كتابة كود غير متزامن يقرأ ككود متزامن، مما يحسن القابلية للقراءة ومعالجة الأخطاء. في Aspose.HTML تنفيذ fetch يتبع المواصفات الكاملة لـ WHATWG، لذا تحصل على دعم لإعادة التوجيه، CORS، استجابات البث، وتوزيع الأخطاء بشكل صحيح، تمامًا كما في المتصفحات الحديثة.

## لماذا نستخدم محرك JavaScript الخاص بـ Aspose.HTML؟

Aspose.HTML يدعم **أكثر من 60** تنسيقًا للإدخال والإخراج ويمكنه معالجة مستندات تصل إلى **500 ميغابايت** دون تحميل الملف بالكامل في الذاكرة. محرك `JavaScriptEngine` المدمج يتبع معيار WHATWG Fetch بالكامل، مما يمنحك معالجة شبكة موثوقة، وإعادة توجيه، ودعم CORS مباشرةً.

## المتطلبات المسبقة
- Java 17 (أو Java 11) مثبتة ومُكوّنة على جهازك.  
- Aspose.HTML for Java 23.7 (أو أحدث إصدار) على مسار الـ classpath.  
- اتصال إنترنت لنقطة النهاية JSON التجريبية.  
- فهم أساسي لطرق Java ووعود JavaScript.

## الخطوة 1 – إنشاء مستند HTML فارغ والحصول على محرك JavaScript الخاص به

فئة `Document` تمثّل مستند HTML في الذاكرة وتوفر محرك JavaScript معزول.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsTutorial {
    public static void main(String[] args) throws Exception {
        // Create an empty HTML document
        Document document = new Document();

        // Obtain the JavaScript engine associated with the document's window
        JavaScriptEngine jsEngine = document.getWindow().getJavaScriptEngine();
```

**لماذا هذا مهم:** كائن `Document` يحاكي نافذة المتصفح، و`JavaScriptEngine` الخاص به يتيح لك تشغيل السكريبتات كما لو كانت في المتصفح. هذا هو الأساس لـ **كيفية استدعاء Java من JavaScript**—المحرك يعمل كجسر.

## الخطوة 2 – تسجيل كائن مضيف بحيث يمكن لـ JavaScript استدعاء Java مرة أخرى

كائن المضيف `JavaCallback` يعرّف طريقة واحدة `onResult` تقوم بطباعة حمولة JSON المستلمة من JavaScript.

```java
        // Register a Java host object that the script can invoke
        jsEngine.addHostObject("javaCallback", new Object() {
            // This method will be called from JavaScript with the fetched JSON string
            public void onResult(String data) {
                System.out.println("Fetched data: " + data);
            }
        });
```

**شرح:**  
- `addHostObject` يربط الاسم `javaCallback` بالكائن Java المجهول.  
- داخل JavaScript ستستدعي `javaCallback.onResult(...)`.  
- هذه هي الآلية الأساسية لـ **call java from javascript**—السكريبت يصل إلى عالم Java، وJava تتفاعل.

> **نصيحة احترافية:** اجعل طرق كائن المضيف `public` وأعد أنواعًا بسيطة (String, int, boolean) لتجنب عبء التسلسل.

## الخطوة 3 – كتابة دالة JavaScript غير متزامنة باستخدام async fetch API

دالة `fetchJson` توضح `async/await` مع API fetch القياسي.

```java
        // Asynchronous script that fetches JSON and passes it to the Java host object
        String asyncScript =
            "async function fetchData() {" +
            "  const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
            "  const json = await response.json();" +
            "  javaCallback.onResult(JSON.stringify(json));" +
            "}" +
            "fetchData();";
```

**لماذا نختار `fetch` بدلاً من XHR القديم:**  
- `fetch` يُعيد `Promise`، مما يجعل الكود أنظف.  
- يعمل بشكل أصلي مع `await`، لذا يتدفق الكود من الأعلى إلى الأسفل—مثالي لـ **مثال fetch غير متزامن في JavaScript**.  
- الـ API مستقبلي؛ معظم المتصفحات والمحركات (بما فيها Aspose) تدعمه مباشرةً.

## الخطوة 4 – تنفيذ السكريبت داخل محرك JavaScript الخاص بالمستند

تشغيل السكريبت يُفعّل حلقة الأحداث، يحل طلب الشبكة، ويستدعي Java مرة أخرى.

```java
        // Execute the async script
        jsEngine.execute(asyncScript);
    }
}
```

عند تشغيل الفئة `AsyncJsTutorial`، يجب أن ترى شيئًا مشابهًا لـ:

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

هذا الإخراج يؤكد ثلاثة أمور:

1. **async fetch API** نجح في استرجاع البيانات.  
2. تم تسلسل JSON وتسليمه إلى Java.  
3. استدعاء **execute javascript engine** انتهى دون حدوث deadlocks.

## الخطوة 5 – معالجة الأخطاء وحالات الحافة (تحسينات اختيارية)

الكود في العالم الحقيقي نادرًا ما يعمل بشكل مثالي في كل مرة. إليك بعض المشكلات الشائعة وكيفية الحماية منها.

### 5.1 فشل الشبكة

إذا كان الخادم البعيد غير متاح، `fetch` يرمي استثناء. غلف الاستدعاء بكتلة `try/catch`:

```java
String asyncScript =
    "async function fetchData() {" +
    "  try {" +
    "    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
    "    if (!response.ok) throw new Error('Network response was not ok');" +
    "    const json = await response.json();" +
    "    javaCallback.onResult(JSON.stringify(json));" +
    "  } catch (e) {" +
    "    javaCallback.onResult('Error: ' + e.message);" +
    "  }" +
    "}" +
    "fetchData();";
```

الآن يتلقى جانب Java رسالة خطأ بدلاً من التعليق.

### 5.2 مهلات الوقت

محرك Aspose لا يوفّر مهلة أصلية لـ `fetch`، لكن يمكنك تنفيذ واحدة في JavaScript:

```javascript
const controller = new AbortController();
setTimeout(() => controller.abort(), 5000); // 5‑second timeout
const response = await fetch(url, { signal: controller.signal });
```

### 5.3 استدعاءات متعددة

إذا كنت بحاجة لجلب عدة موارد، ببساطة استخدم حلقة أو `map` على مصفوفة من العناوين. يمكن توسيع كائن المضيف لقبول معرف، مما يتيح لك ربط الردود.

## مثال عملي كامل

فيما يلي ملف المصدر الكامل يمكنك نسخه‑ولصقه في IDE الخاص بك. لا توجد تبعيات مخفية، فقط ملف JAR الخاص بـ Aspose.HTML على classpath.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an empty HTML document and obtain its JavaScript engine
        Document document = new Document();
        JavaScriptEngine jsEngine = document.getWindow().getJavaScriptEngine();

        // Step 2: Register a host object that JavaScript can call back into Java
        jsEngine.addHostObject("javaCallback", new Object() {
            public void onResult(String data) {
                System.out.println("Fetched data: " + data);
            }
        });

        // Step 3: Write an async function that uses the asynchronous fetch API
        String asyncScript =
            "async function fetchData() {" +
            "  try {" +
            "    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
            "    if (!response.ok) throw new Error('Network error');" +
            "    const json = await response.json();" +
            "    javaCallback.onResult(JSON.stringify(json));" +
            "  } catch (e) {" +
            "    javaCallback.onResult('Error: ' + e.message);" +
            "  }" +
            "}" +
            "fetchData();";

        // Step 4: Execute the script inside the document's JavaScript engine
        jsEngine.execute(asyncScript);
    }
}
```

**الإخراج المتوقع في وحدة التحكم**

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

إذا رأيت سطر خطأ يبدأ بـ `Error:` فهذا يعني حدوث مشكلة—غالبًا ما تكون انقطاعًا في الشبكة.

## نظرة بصرية

![مخطط يوضح كيفية استدعاء Java لـ JavaScript واستلام نتائج fetch غير المتزامن – call java from javascript](/images/java-js-async.png)

*الصورة توضح التدفق: Java → JavaScriptEngine → async fetch → JavaCallback.*

## الأسئلة المتكررة

**Q:** هل يمكنني استخدام هذا النهج مع محركات JavaScript أخرى؟  
**A:** نعم. أي محرك يدعم كائنات المضيف (مثل Nashorn، GraalVM) يمكنه العمل، لكن Aspose.HTML يوفر بيئة شبيهة بالمتصفح مع `fetch` مدمج.

**Q:** ماذا لو احتجت لإرجاع كائن Java معقد بدلاً من سلسلة نصية؟  
**A:** قم بتحويل الكائن إلى JSON على جانب Java ودع JavaScript يحلله، أو عرّف عدة طرق بسيطة على كائن المضيف لتمرير الحقول الفردية.

**Q:** هل تنفيذ `fetch` متوافق تمامًا مع المعايير؟  
**A:** Aspose.HTML يتبع معيار WHATWG Fetch، ويتعامل مع إعادة التوجيه، CORS، والبث تمامًا كما تفعل المتصفحات الحديثة.

**Q:** هل يحجب هذا الخيط (thread) في Java أثناء انتظار الشبكة؟  
**A:** لا. استدعاء `execute` يُعيد فورًا؛ المحرك الداخلي يعالج الـ promise بشكل غير متزامن. يبقى الخيط الرئيسي نشطًا حتى ينتهي السكريبت أو تقوم بإغلاق المحرك.

**Q:** كيف يمكنني تصحيح كود JavaScript داخل المحرك؟  
**A:** استخدم الطريقة `JavaScriptEngine.setDebugMode(true)` لتوجيه رسائل وحدة التحكم إلى سجل Java.

## الخلاصة

استعرضنا سيناريو عملي يتيح لك **استدعاء Java من JavaScript**، **تشغيل JavaScript غير المتزامن**، و**جلب JSON في Java** باستخدام **async fetch API**. من خلال إنشاء كائن مضيف، كتابة دالة `async` مرتبة، وتنفيذها عبر محرك JavaScript الخاص بـ Aspose.HTML، تحصل على جسر نظيف غير محجوز بين البيئتين.

لا تتردد في تغيير عنوان نقطة النهاية، إضافة المزيد من ردود النداء، أو تشغيل عدة سكريبتات متوازية. خطوات مستقبلية قد تستكشفها:

- تنفيذ سكريبتات متعددة بشكل متزامن باستخدام مثيلات منفصلة من `JavaScriptEngine`.  
- استخدام نمط async fetch لمعالجة مجموعات بيانات كبيرة بالتوازي.  
- دمج هذا الجسر في مُصنّع HTML من جانب الخادم يجلب بيانات حية قبل التصيير.

برمجة سعيدة!

---

**آخر تحديث:** 2026-10-09  
**تم الاختبار مع:** Aspose.HTML for Java 23.7  
**المؤلف:** Aspose

## دروس ذات صلة

- [استدعاء Java من Javascript وإضافة كائن مضيف وتشغيل Javascript](/html/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/)
- [كيفية تشغيل Javascript في Java دليل كامل](/html/java/advanced-usage/how-to-run-javascript-in-java-complete-guide/)
- [تمكين تنفيذ السكريبت في Java دليل Aspose Html كامل](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-03-04
description: استدعِ جافا من جافا سكريبت باستخدام Aspose.HTML، وشغّل جافا سكريبت غير
  المتزامن، واحصل على JSON في جافا باستخدام مثال بسيط. تعلّم كيفية تنفيذ محرك جافا
  سكريبت بكفاءة.
draft: false
keywords:
- call java from javascript
- run async javascript
- fetch json in java
- asynchronous fetch api
- execute javascript engine
language: ar
og_description: استدعِ جافا من جافاسكريبت باستخدام Aspose.HTML، شغّل جافاسكريبت غير
  المتزامن، واحصل على JSON في جافا. يتضمن الكود الكامل، الشروحات، والنصائح.
og_title: استدعاء Java من JavaScript – دليل خطوة بخطوة لجلب البيانات غير المتزامن
tags:
- Java
- JavaScript
- Aspose.HTML
- Async Programming
title: استدعاء جافا من جافاسكريبت – دليل شامل للـ Fetch غير المتزامن وتنفيذ محرك جافاسكريبت
url: /ar/java/advanced-usage/call-java-from-javascript-complete-guide-to-async-fetch-js-e/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استدعاء Java من JavaScript – دليل كامل مع واجهة برمجة التطبيقات fetch غير المتزامنة

هل تساءلت يومًا كيف **تستدعي Java من JavaScript** دون مغادرة تطبيق Java الخاص بك؟ ربما تقوم بإنشاء مُعالج HTML من جانب الخادم، أو تحتاج إلى إظهار بعض منطق Java إلى سكريبت يعمل داخل مستند. الخبر السار هو أن Aspose.HTML يجعل هذا سهلًا جدًا. في هذا الدليل سنوضح لك ليس فقط كيفية *تشغيل JavaScript غير المتزامن* داخل مستند مدعوم بـ Java، بل أيضًا كيفية **جلب JSON في Java** باستخدام **واجهة برمجة التطبيقات fetch غير المتزامنة** وأخيرًا كيفية **تنفيذ مكالمات محرك JavaScript** بأمان.

باختصار، ستحصل على مثال كامل قابل للتنفيذ يجلب حمولة JSON من نقطة نهاية عامة، يسلّمها إلى كائن مضيف Java، ويطبع النتيجة على وحدة التحكم. لا خوادم ويب خارجية، لا مكتبات إضافية—فقط Java صافية و Aspose.HTML.

## ما ستتعلمه

- كيفية إنشاء مستند HTML فارغ باستخدام Aspose.HTML.
- كيفية الحصول على **محرك JavaScript** وتنفيذه من Java.
- كيفية تسجيل كائن مضيف Java يمكن للـ JavaScript استدعاؤه.
- كيفية كتابة دالة **JavaScript غير متزامنة** تستخدم **واجهة برمجة التطبيقات fetch غير المتزامنة**.
- كيفية معالجة البيانات المستلمة في Java باستخدام رد نداء نظيف.
- المخرجات المتوقعة ونصائح استكشاف الأخطاء.

### المتطلبات المسبقة

- Java 17 أو أحدث (الكود يُترجم أيضًا مع JDK 11).
- Aspose.HTML for Java 23.7 (أو أحدث نسخة متاحة وقت الكتابة).
- إلمام أساسي بـ Java ووعود JavaScript.
- اتصال بالإنترنت لطلب `jsonplaceholder` التجريبي.

إذا كان أي من ذلك غير مألوف لك، لا تقلق—كل خطوة مشروحة بلغة بسيطة، وسترى بالضبط لماذا نفعل ما نفعل.

---

## الخطوة 1 – إنشاء مستند HTML فارغ والحصول على محرك JavaScript الخاص به

أول شيء نحتاجه هو مستند فارغ يمنحنا بيئة JavaScript معزولة. فئة `Document` في Aspose.HTML تقوم بذلك تمامًا.

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

**لماذا هذا مهم:** كائن `Document` يحاكي نافذة المتصفح، و`JavaScriptEngine` الخاص به يتيح لنا تشغيل السكريبتات كما يفعل المتصفح. هذا هو الأساس لـ **call java from javascript**—المحرك يعمل كجسر.

---

## الخطوة 2 – تسجيل كائن مضيف حتى يتمكن JavaScript من الاستدعاء إلى Java

يتيح لك Aspose.HTML كشف أي كائن Java للعالم السكريبت. سننشئ فئة مجهولة ذات طريقة `onResult` واحدة تقوم ببساطة بطباعة أي JSON نتلقاه.

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
- داخل JavaScript سنستدعي `javaCallback.onResult(...)`.  
- هذا هو جوهر **call java from javascript**—السكريبت يصل إلى عالم Java، وJava تتفاعل.

> **نصيحة احترافية:** اجعل طرق كائن المضيف `public` وبسيطة؛ الكائنات المعقدة قد تسبب مشاكل في التسلسل.

---

## الخطوة 3 – كتابة دالة JavaScript غير متزامنة باستخدام واجهة برمجة التطبيقات fetch غير المتزامنة

الآن يأتي الجزء الممتع: سكريبت صغير يجلب JSON من نقطة نهاية عن بُعد. سنستخدم `async/await`، وهو الأسلوب الحديث لـ **run async JavaScript**.

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
- يعمل بشكل أصلي مع `await`، لذا يتبع التدفق من الأعلى إلى الأسفل—مثالي لعروض **asynchronous fetch api**.  
- الواجهة مستقبلية؛ معظم المتصفحات والمحركات (بما فيها Aspose) تدعمها مباشرة.

---

## الخطوة 4 – تنفيذ السكريبت داخل محرك JavaScript الخاص بالمستند

أخيرًا، نسلم السكريبت إلى المحرك. سيُنشئ المحرك حلقة أحداث صغيرة، يحل وعد `fetch`، ثم يستدعي Java عند الانتهاء.

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

هذا الإخراج يؤكد ثلاث نقاط:

1. **asynchronous fetch API** نجح في جلب البيانات.  
2. تم تسلسل JSON وتسليمه إلى Java.  
3. مكالمة **execute javascript engine** اكتملت دون أي deadlock.

---

## الخطوة 5 – معالجة الأخطاء وحالات الحافة (تحسينات اختيارية)

الكود في العالم الحقيقي نادرًا ما يعمل بشكل مثالي في كل مرة. إليك بعض المشكلات الشائعة وكيفية الحماية منها.

### 5.1 فشل الشبكة

إذا كان الخادم البعيد غير متاح، سيُطلق `fetch` استثناء. غلف الاستدعاء بكتلة `try/catch`:

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

الآن سيتلقى جانب Java رسالة خطأ بدلاً من التوقف.

### 5.2 مهلات الوقت

محرك Aspose لا يوفر مهلة أصلية لـ `fetch`، لكن يمكنك تنفيذ واحدة في JavaScript:

```javascript
const controller = new AbortController();
setTimeout(() => controller.abort(), 5000); // 5‑second timeout
const response = await fetch(url, { signal: controller.signal });
```

### 5.3 استدعاءات متعددة

إذا كنت بحاجة لجلب عدة موارد، ما عليك سوى التكرار أو الخريطة على مصفوفة من الروابط. يمكن توسيع كائن المضيف لقبول معرف، مما يتيح لك ربط الردود.

---

## مثال عملي كامل

فيما يلي **ملف المصدر الكامل** يمكنك نسخه ولصقه في بيئة التطوير الخاصة بك. لا توجد تبعيات مخفية، فقط ملف JAR الخاص بـ Aspose.HTML على مسار الـ classpath.

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

**الإخراج المتوقع على وحدة التحكم**

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

إذا رأيت سطر خطأ يبدأ بـ `Error:` فهذا يعني حدوث مشكلة—غالبًا ما تكون اضطرابًا في الشبكة.

---

## نظرة بصرية عامة

![مخطط يوضح كيف يستدعي JavaScript من Java ويتلقى نتائج fetch غير المتزامنة – call java from javascript](/images/java-js-async.png)

*الصورة تُظهر التدفق: Java → JavaScriptEngine → async fetch → JavaCallback.*

---

## الأسئلة المتكررة

**هل يمكنني استخدام هذا النهج مع محركات JavaScript أخرى؟**  
نعم، أي محرك يتيح آلية كائن مضيف (مثل Nashorn أو GraalVM) يمكنه العمل، لكن Aspose.HTML يمنحك بيئة شبيهة بالمتصفح مع `fetch` مدمج.

**ماذا لو أردت إرجاع كائن Java معقد بدلاً من سلسلة نصية؟**  
يمكنك تسلسل الكائن إلى JSON على جانب Java والسماح للـ JavaScript بتحليله، أو كشف عدة طرق على كائن المضيف لاستقبال حقول منفصلة.

**هل تنفيذ `fetch` متوافق تمامًا مع المعايير؟**  
Aspose.HTML يطبق معيار WHATWG Fetch، لذا ستحصل على معالجة صحيحة لإعادة التوجيه، CORS، والبث.

**هل يحجب هذا خيط Java أثناء انتظار الشبكة؟**  
لا. مكالمة `execute` تُعيد فورًا، والمحرك الداخلي يعالج الوعد بشكل غير متزامن. ومع ذلك، سيبقى الخيط الرئيسي نشطًا حتى ينتهي السكريبت أو تقوم بإغلاق المحرك صراحةً.

---

## الخلاصة

لقد استعرضنا سيناريو عملي يتيح لك **call java from javascript**، **run async JavaScript**، و**fetch JSON in Java** باستخدام **asynchronous fetch API**. من خلال إنشاء كائن مضيف، كتابة دالة `async` مرتبة، وتنفيذها عبر **محرك JavaScript** في Aspose.HTML، تحصل على جسر نظيف غير محجوز بين البيئتين.

جرّبه، عدّل الرابط، أو أضف المزيد من ردود النداء—الخيال هو الحد. الخطوات التالية قد تشمل:

- **Executing JavaScript engine** مع عدة سكريبتات متزامنة.  
- استخدام **run async javascript** لمعالجة مجموعات بيانات كبيرة بالتوازي.  
- دمج هذا النمط في خدمة ويب تُنشئ HTML ديناميكيًا عند الطلب.

لا تتردد في التجربة، وإذا واجهت أي عائق أرسل تعليقًا. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
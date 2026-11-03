---
category: general
date: 2026-10-14
description: استدعاء java من javascript باستخدام Aspose.HTML. تعلّم كيفية إضافة كائن
  مضيف، تنفيذ javascript في java، وتسجيل الخرج من javascript في دليل مختصر.
keywords:
- call java from javascript
- execute javascript in java
- run javascript in java
- java host object
- aspose.html scripting
lastmod: 2026-10-14
og_description: استدعاء java من javascript باستخدام Aspose.HTML. يوضح هذا الدليل كيفية
  إضافة كائن مضيف، تنفيذ javascript في java، وتسجيل الخرج من javascript، كل ذلك في
  بضع أسطر من الشيفرة.
og_image_alt: Screenshot of Java console output showing javascript logging via Aspose.HTML
  host object
og_title: استدعاء java من javascript – إضافة كائن مضيف وتشغيل javascript في java
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Call java from javascript using Aspose.HTML. Learn how to add a host
    object, execute javascript in java, and log from javascript in a concise tutorial.
  headline: Call java from javascript – add host object and run javascript in java
  type: TechArticle
- questions:
  - answer: Yes. Aspose.HTML is a pure‑Java library, so it runs on any JVM, including
      Android’s ART runtime.
    question: Does this work on Android?
  - answer: You can expose POJOs with getters and setters; the engine maps them to
      JavaScript objects automatically. Collections such as `java.util.List` or arrays
      are also convertible.
    question: What if I need to pass complex objects?
  - answer: If the script throws a JavaScript error, `eval` propagates a `ScriptException`.
      Wrap the call in a try‑catch block to log or recover.
    question: How does error handling work?
  - answer: Absolutely. The same `HTMLDocument` retains its global scope, so you can
      call `eval` repeatedly. Just manage variable names to avoid clashes.
    question: Can I run multiple scripts sequentially?
  - answer: Treat any external script as untrusted input. Validate parameters and
      consider sandboxing by exposing only the minimal required methods.
    question: Is the host object safe for untrusted scripts?
  type: FAQPage
tags:
- java
- javascript
- aspose.html
- scripting
- host object
title: استدعاء java من javascript – إضافة كائن مضيف وتشغيل javascript في java
url: /ar/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استدعاء جافا من جافاسكريبت – إضافة كائن مضيف وتشغيل جافاسكريبت في جافا

هل احتجت إلى **call java from javascript** داخل تطبيق جافا؟ ربما تقوم ببناء محرك تقارير HTML ديناميكي أو تريد ببساطة كشف مسجل جافا إلى سكريبت تتحكم فيه. في هذا الدرس ستتعرف بالضبط على كيفية إضافة كائن مضيف، تشغيل JavaScript في جافا، وحتى **log from JavaScript** إلى الـ JVM — كل ذلك باستخدام Aspose.HTML.

سنستعرض مثالًا كاملاً قابلًا للتنفيذ ينشئ مستند HTML فارغ، يحقن فئة جافا `Logger` ككائن مضيف، ينفذ سكريبت صغير، ويطبع النتيجة إلى وحدة التحكم. لا حاجة لمتصفح ويب خارجي، ولا سحر غامض — مجرد شفرة جافا عادية يمكنك نسخها ولصقها وتشغيلها اليوم.

## إجابات سريعة
- **كيف يمكنني إضافة كائن مضيف؟** سجل نسخة جافا باستخدام `document.getWindow().addHostObject("name", object)`.  
- **هل يمكنني تنفيذ JavaScript في جافا؟** نعم—استخدم `document.getWindow().eval(yourScript)`.  
- **هل يمكن تسجيل من JavaScript؟** بالتأكيد؛ يمكن للكائن المضيف كشف أي طريقة `void log(String)` .  
- **ما الإصدار المطلوب من Aspose.HTML؟** الإصدار 23.10 أو أحدث يدعم واجهة برمجة التطبيقات الكاملة للكائن المضيف.  
- **هل أحتاج إلى متصفح ويب؟** لا—توفر Aspose.HTML محركًا مدمجًا، لذا كل شيء يعمل بدون واجهة.

## ما هو استدعاء جافا من جافاسكريبت؟
**Call java from javascript** هي التقنية التي تكشف كائنات جافا لبيئة تشغيل JavaScript بحيث يمكن للسكريبتات استدعاء طرق جافا مباشرة. تُنشئ Aspose.HTML محرك JavaScript خفيف داخل عملية جافا، مما يتيح تواصلًا ثنائي الاتجاه بسلاسة دون متصفحات خارجية.

## لماذا نستخدم Aspose.HTML لتنفيذ جافاسكريبت في جافا؟
تدعم Aspose.HTML **أكثر من 50 تنسيقًا للإدخال والإخراج** ويمكنها تقييم JavaScript في بيئة HTML5 متوافقة بالكامل. تعالج السكريبتات بمتوسط حتى 200 مللي ثانية للشفرة البسيطة ذات السطر الواحد، وتقوم بذلك دون تحميل مجموعة كاملة من المتصفح، مما يقلل استهلاك الذاكرة بنسبة تصل إلى 80 % مقارنةً بالنهج القائم على Selenium.

## المتطلبات المسبقة
- Java 17 (أو أي JDK حديث) مثبت ومُكوَّن.  
- مكتبة Aspose.HTML for Java (الإصدار 23.10 أو أحدث). يمكنك الحصول عليها من Maven Central أو موقع Aspose.  
- IDE بسيط أو محرر نصوص؛ يعمل المثال من سطر الأوامر أيضًا.

> **نصيحة احترافية:** إذا كنت تستخدم Maven، أضف الاعتماد التالي إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

أو، لـ Gradle:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

الآن بعد أن رتبنا الأساسيات، دعنا نغوص في الحل خطوة بخطوة.

## كيفية إضافة كائن مضيف وتشغيل جافاسكريبت في جافا؟
`addHostObject` يسجل كائن جافا كمتغير عالمي في سياق JavaScript. حمّل `HTMLDocument` الخاص بك، سجّل مسجل جافا تحت الاسم `"javaLogger"` باستخدام `addHostObject`، ثم قيم سكريبت قصير يستدعي `javaLogger.log`. يتطلب التدفق الكامل ثلاث نداءات فقط لواجهة برمجة التطبيقات ويعمل في أي بيئة تشغيل Java 17.

### الخطوة 1: إنشاء مشروع جافا بسيط
أولاً، أنشئ فئة جافا جديدة تسمى `JsHostObjectDemo`. ستحتوي الفئة على طريقة `main` وتعريف كائن المضيف. الحفاظ على كل شيء في ملف واحد يجعل الدرس مستقلًا وسهل النسخ.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Demonstrates how to call Java from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    // -----------------------------------------------------------------
    // Step 1.1 – Define a simple Java class that will be callable from JS
    // -----------------------------------------------------------------
    public static class Logger {
        /**
         * This method will be invoked from JavaScript.
         *
         * @param message Text to print.
         */
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1.2 – Create an empty HTMLDocument – it gives us a scripting engine
        // -----------------------------------------------------------------
        HTMLDocument document = new HTMLDocument();

        // -----------------------------------------------------------------
        // Step 1.3 – Add the Java Logger instance as a host object named "javaLogger"
        // -----------------------------------------------------------------
        document.getWindow().addHostObject("javaLogger", new Logger());

        // -----------------------------------------------------------------
        // Step 1.4 – Prepare JavaScript code that uses the host object
        // -----------------------------------------------------------------
        String script = "javaLogger.log('Hello from JavaScript!');";

        // -----------------------------------------------------------------
        // Step 1.5 – Execute the script; the Java Logger handles the call
        // -----------------------------------------------------------------
        document.getWindow().eval(script);
    }
}
```

### لماذا `HTMLDocument`؟
`HTMLDocument` يمثل مستند HTML في الذاكرة ويوفر محرك JavaScript. تُنشئ فئة `HTMLDocument` بيئة سكريبت متوافقة مع HTML‑5 بالكامل. رغم أننا لا نحمل أي علامة، فإن كائن `window` للمستند يمنحنا الوصول إلى محرك JavaScript، حيث يحدث سحر **run javascript in java**. بالإضافة إلى ذلك يمكنك تعديل DOM، تحميل الموارد، أو تقييم السكريبتات دون الحاجة إلى متصفح.

## كيفية إضافة كائن المضيف – “javaLogger”؟
`Logger` هي فئة جافا بسيطة تحتوي على طريقة `log(String)` التي تكتب الرسائل إلى وحدة التحكم. سجّل نسخة `Logger` تحت الاسم `"javaLogger"` بحيث يمكن لأي سكريبت يتم تقييمه في هذا المستند استدعاء `javaLogger.log(...)`. هذا هو جوهر متطلبات **add host object** ويجعل المسجل متاحًا كمتغير عالمي لكود JavaScript.

### المشكلات الشائعة
- **تصادم الأسماء** – إذا كان لديك بالفعل متغير عالمي يسمى `javaLogger` في سكريبتك، سيُستبدل كائن المضيف. اختر اسمًا فريدًا.  
- **سلامة الخيوط** – كائن المضيف مشترك عبر تنفيذ السكريبتات على نفس المستند. إذا كنت تخطط لتشغيل سكريبتات متزامنة، اجعل فئة المضيف آمنة للخيوط (مثلاً، استخدم `synchronized` أو بدائل `java.util.concurrent`).  

## كيفية كتابة وتنفيذ جافاسكريبت في جافا؟
`eval` ينفّذ سلسلة JavaScript في محرك سكريبت المستند ويعيد أي نتيجة. قدم سكريبتًا صغيرًا إلى `eval`. يقوم المحرك بحل `javaLogger` من النطاق العالمي ويستدعي طريقة `log` مع السلسلة المقدمة. يمكنك أيضًا إرجاع القيم، معالجة الاستثناءات، وربط تقييمات متعددة لتفاعلات أكثر تعقيدًا.

### النتيجة المتوقعة

```
[JS] Hello from JavaScript!
```

## كيفية توسيع المضيف – أكثر من مجرد تسجيل؟
كائن المضيف هو أي نسخة جافا مكشوفة لـ JavaScript عبر `addHostObject`. اكشف عن وظائف إضافية بإضافة طرق إلى فئة `Logger` أو بإنشاء فئة مضيف جديدة. أدناه مثال سريع يعيد قيمة إلى JavaScript أيضًا. يمكن لكائن المضيف كشف أنواع معقدة، إجراء I/O، أو التفاعل مع خدمات أخرى. بإرجاع قيمة، يمكن للسكريبت استلام بيانات مرة أخرى، مما يتيح تواصلًا ثنائي الاتجاه بين جافا وجافاسكريبت.

```java
public static class Utils {
    public int add(int a, int b) {
        return a + b;
    }
}

// Register it
document.getWindow().addHostObject("javaUtils", new Utils());

// JavaScript side
String script2 = "var result = javaUtils.add(3, 4); javaLogger.log('3+4=' + result);";
document.getWindow().eval(script2);
```

الآن تُظهر وحدة التحكم:

```
[JS] 3+4=7
```

## كيفية تنظيف الموارد بعد تشغيل السكريبتات؟
`dispose` يحرّر الموارد الأصلية التي يحتفظ بها كائن `HTMLDocument`. عندما تنتهي من بيئة السكريبت، قم بتفريغ `HTMLDocument` لتحرير الموارد الأصلية. عدم استدعاء `dispose()` قد يؤدي إلى تسرب الذاكرة، خاصةً عند إنشاء مستندات كثيرة في حلقات أو خدمات طويلة التشغيل. احرص دائمًا على تغليف الاستخدام بكتلة try‑with‑resources أو تأكد من استدعاء `document.dispose()` في جملة finally.

```java
document.dispose(); // Important for long‑running applications
```

## مثال كامل يعمل
فيما يلي ملف المصدر الكامل الذي يمكنك تجميعه وتشغيله فورًا. احفظه باسم `JsHostObjectDemo.java`، تأكد من أن ملف JAR الخاص بـ Aspose.HTML موجود في مسار الفئات الخاص بك، ثم نفّذ `java JsHostObjectDemo`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Complete demo showing how to call Java from JavaScript, add host object,
 * run JavaScript in Java, and log from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    /** Simple logger that will be called from JavaScript. */
    public static class Logger {
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    /** Utility class exposing arithmetic to JavaScript. */
    public static class Utils {
        public int add(int a, int b) {
            return a + b;
        }
    }

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create the HTMLDocument – this spins up the JavaScript engine.
        HTMLDocument document = new HTMLDocument();

        // 2️⃣ Register host objects.
        document.getWindow().addHostObject("javaLogger", new Logger());
        document.getWindow().addHostObject("javaUtils", new Utils());

        // 3️⃣ JavaScript that logs a message and performs a calculation.
        String script = ""
                + "javaLogger.log('Hello from JavaScript!');"
                + "var sum = javaUtils.add(5, 12);"
                + "javaLogger.log('5 + 12 = ' + sum);";

        // 4️⃣ Execute the script.
        document.getWindow().eval(script);

        // 5️⃣ Clean up.
        document.dispose();
    }
}
```

تشغيل هذا البرنامج ينتج:

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

## الأسئلة المتكررة

**س: هل يعمل هذا على Android؟**  
ج: نعم. Aspose.HTML هي مكتبة جافا صافية، لذا تعمل على أي JVM، بما في ذلك بيئة تشغيل ART على Android.

**س: ماذا لو احتجت لتمرير كائنات معقدة؟**  
ج: يمكنك كشف POJOs مع getters و setters؛ يقوم المحرك بتحويلها إلى كائنات JavaScript تلقائيًا. المجموعات مثل `java.util.List` أو المصفوفات قابلة للتحويل أيضًا.

**س: كيف يعمل التعامل مع الأخطاء؟**  
ج: إذا رمى السكريبت خطأ JavaScript، فإن `eval` يمرر `ScriptException`. غلف الاستدعاء بكتلة try‑catch لتسجيل الخطأ أو الاسترداد.

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

**س: هل يمكنني تشغيل عدة سكريبتات متتالية؟**  
ج: بالتأكيد. يحتفظ نفس `HTMLDocument` بنطاقه العالمي، لذا يمكنك استدعاء `eval` بشكل متكرر. فقط احرص على إدارة أسماء المتغيرات لتجنب التعارضات.

**س: هل كائن المضيف آمن للسكريبتات غير الموثوقة؟**  
ج: عالج أي سكريبت خارجي كمدخل غير موثوق. تحقق من صحة المعلمات وفكّر في العزل (sandbox) عبر كشف الحد الأدنى فقط من الطرق المطلوبة.

## أفضل الممارسات والنصائح
- **سمِّ كائنات المضيف بوضوح** — `javaLogger`، `javaUtils`، إلخ — لتجنب الالتباس.  
- **اجعل طرق المضيف صغيرة وخالية من الآثار الجانبية** قدر الإمكان؛ فهذا يسهل عملية تصحيح الأخطاء.  
- **قم بتفريغ المستند** فور الانتهاء؛ فهو يحرّر الذاكرة الأصلية التي يخصصها Aspose.HTML.  
- **تحقق من صحة المدخلات** من JavaScript، خاصةً إذا كانت السكريبتات من مصادر غير موثوقة. عالجها كأي بيانات خارجية.

## الخلاصة
أصبح لديك الآن مثال شامل من البداية إلى النهاية حول كيفية **call java from javascript** عبر **إضافة كائن مضيف**، **تشغيل جافاسكريبت في جافا**، و**تسجيل من جافاسكريبت** باستخدام Aspose.HTML. هذا النمط قوي: يمكن كشف أي خدمة جافا للسكريبتات، مما يحول تطبيق جافا الخاص بك إلى منصة سكريبت خفيفة.

بعد ذلك، قد تستكشف:
- حقن صفحة HTML كاملة وتعديل DOM من جافاسكريبت.  
- استخدام كائن المضيف لتدفق البيانات إلى جانب جافا (مثلاً، تسلسل JSON).  
- التكامل مع محركات سكريبت أخرى مثل Nashorn أو GraalVM لدعم لغات أوسع.

جرّبه، عدّل فئات `Logger` أو `Utils`، وشاهد إلى أي مدى يمكنك دفع مفهوم **javascript host object** في مشاريعك الخاصة.

---

**آخر تحديث:** 2026-10-14  
**تم الاختبار مع:** Aspose.HTML for Java 23.10  
**المؤلف:** Aspose  

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

```javascript
javaLogger.log('Hello from JavaScript!');
```

## دروس ذات صلة
- [تمكين تنفيذ السكريبت في جافا – دليل Aspose HTML الكامل](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)
- [تنفيذ جافاسكريبت في جافا – دليل كامل لتشغيل Js من](/html/java/advanced-usage/execute-javascript-in-java-complete-guide-to-running-js-from/)
- [كيفية عزل جافاسكريبت – دليل Aspose HTML الكامل](/html/java/advanced-usage/how-to-sandbox-javascript-complete-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
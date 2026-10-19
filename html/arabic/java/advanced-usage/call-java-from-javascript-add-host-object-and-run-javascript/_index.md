---
category: general
date: 2026-03-14
description: تعلم كيفية استدعاء Java من JavaScript باستخدام Aspose.HTML. يوضح هذا
  الدليل كيفية إضافة كائن مضيف، تشغيل JavaScript في Java، وتسجيل السجلات من JavaScript.
draft: false
keywords:
- call java from javascript
- add host object
- run javascript in java
- javascript host object
- log from javascript
language: ar
og_description: استدعِ Java من JavaScript باستخدام Aspose.HTML. أضف كائن المضيف، وشغّل
  JavaScript في Java، وسجّل من JavaScript في دليل واحد.
og_title: استدعاء جافا من جافاسكريبت – دليل كامل مع كائن المضيف
tags:
- Java
- JavaScript
- Aspose.HTML
- Scripting
title: استدعاء جافا من جافاسكريبت – إضافة كائن مضيف وتشغيل جافاسكريبت في جافا
url: /ar/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استدعاء Java من JavaScript – إضافة كائن مضيف وتشغيل JavaScript في Java

هل احتجت يومًا إلى **استدعاء Java من JavaScript** داخل تطبيق Java؟ ربما تقوم بإنشاء محرك تقارير HTML ديناميكي أو تريد ببساطة إتاحة مسجل Java لسكريبت تتحكم فيه. في هذا الدرس ستتعرف بالضبط على كيفية إضافة كائن مضيف، تشغيل JavaScript في Java، وحتى **تسجيل من JavaScript** إلى JVM — كل ذلك باستخدام Aspose.HTML.

سنستعرض مثالًا كاملاً قابلاً للتنفيذ ينشئ مستند HTML فارغ، يحقن فئة Java `Logger` ككائن مضيف، ينفذ سكريبت صغير، ويطبع النتيجة على وحدة التحكم. لا تحتاج إلى متصفح ويب خارجي، ولا سحر غامض — مجرد كود Java عادي يمكنك نسخه‑ولصقه وتشغيله اليوم.

## المتطلبات المسبقة

- Java 17 (أو أي JDK حديث) مثبت ومُعد.
- مكتبة Aspose.HTML for Java (الإصدار 23.10 أو أحدث). يمكنك الحصول عليها من Maven Central أو موقع Aspose.
- بيئة تطوير بسيطة أو محرر نصوص؛ المثال يعمل أيضًا من سطر الأوامر.

> **نصيحة احترافية:** إذا كنت تستخدم Maven، أضف الاعتماد التالي إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

أو، إذا كنت تستخدم Gradle:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

الآن بعد أن رتبنا الأساسيات، دعنا نغوص في الحل خطوة بخطوة.

## الخطوة 1: إنشاء مشروع Java بسيط

أولاً، أنشئ فئة Java جديدة تُسمى `JsHostObjectDemo`. ستحتوي هذه الفئة على طريقة `main` وتعريف كائن المضيف. إبقاء كل شيء في ملف واحد يجعل الدرس مستقلًا وسهل النسخ.

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

### لماذا نستخدم `HTMLDocument`؟

فئة `HTMLDocument` في Aspose.HTML تُنشئ بيئة سكريبت متوافقة مع HTML‑5 بالكامل. رغم أننا لا نحمل أي علامة HTML، فإن كائن `window` الخاص بالمستند يمنحنا الوصول إلى محرك JavaScript، وهو المكان الذي يحدث فيه سحر **تشغيل JavaScript في Java**.

## الخطوة 2: إضافة كائن المضيف – “javaLogger”

السطر

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

يقوم بالعمل الأساسي لمتطلب **إضافة كائن مضيف**. من خلال تسجيل نسخة `Logger` تحت الاسم `"javaLogger"`، يمكن لأي سكريبت يُقيم في هذا المستند استدعاء `javaLogger.log(...)`. هذا هو جوهر مفهوم **كائن مضيف JavaScript**: جسر يسمح لـ JavaScript بالوصول إلى JVM.

### مشاكل شائعة

- **تصادم الأسماء** – إذا كان لديك بالفعل متغيّر عالمي يُدعى `javaLogger` في السكريبت، سيتم استبدال كائن المضيف. اختر اسمًا فريدًا.
- **سلامة الخيوط** – كائن المضيف مشترك بين تنفيذات السكريبت على نفس المستند. إذا كنت تخطط لتشغيل سكريبتات متزامنة، اجعل فئة المضيف آمنة للخيوط (مثلاً باستخدام `synchronized` أو أدوات `java.util.concurrent`).

## الخطوة 3: كتابة وتنفيذ JavaScript

السكريبت الذي نمرره إلى `eval` صغير عمدًا:

```javascript
javaLogger.log('Hello from JavaScript!');
```

عند تشغيل `document.getWindow().eval(script)`، يبحث المحرك عن `javaLogger` في النطاق العالمي، يجد كائن Java الذي أضفناه، ويستدعي طريقة `log` مع السلسلة الممرَّرة.

### النتيجة المتوقعة

تشغيل طريقة `main` يطبع السطر التالي على وحدة التحكم:

```
[JS] Hello from JavaScript!
```

هذا السطر الصغير يثبت أننا نجحنا في **استدعاء java من javascript**، وأن **التسجيل من javascript** يظهر تمامًا حيث تظهر رسالة `System.out` العادية في Java.

## الخطوة 4: توسيع كائن المضيف – أكثر من مجرد تسجيل

إذا احتجت إلى إتاحة وظائف إضافية (مثل الوصول إلى الملفات، استعلامات قاعدة البيانات)، ما عليك سوى إضافة المزيد من الطرق إلى فئة `Logger` — أو إنشاء فئة مضيف جديدة تمامًا. إليك مثالًا سريعًا يُعيد قيمة أيضًا:

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

هذا يوضح مرونة نمط **كائن مضيف JavaScript**: يمكنك إتاحة أي API من Java تحتاجه، طالما أن أنواع البيانات قابلة للتحويل بين Java وJavaScript (أنواع بدائية، سلاسل، مصفوفات، إلخ).

## الخطوة 5: تنظيف الموارد

عند الانتهاء من بيئة السكريبت، قم بتحرير `HTMLDocument` لتحرير الموارد الأصلية:

```java
document.dispose(); // Important for long‑running applications
```

تجاهل تحرير الموارد قد يؤدي إلى تسرب الذاكرة، خاصة إذا قمت بإنشاء مستندات متعددة داخل حلقة.

## مثال كامل يعمل

فيما يلي ملف المصدر الكامل الذي يمكنك تجميعه وتشغيله فورًا. احفظه باسم `JsHostObjectDemo.java`، تأكد من وجود ملف JAR الخاص بـ Aspose.HTML في مسار الـ classpath، ثم نفّذ `java JsHostObjectDemo`.

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

هذا هو سير عمل **استدعاء java من javascript** بالكامل في بضع أسطر فقط.

## الأسئلة المتكررة

### هل يعمل هذا على Android؟

Aspose.HTML مكتبة Java صافية، لذا تعمل على أي JVM، بما في ذلك Dalvik/ART في Android. ما عليك سوى تضمين ملف الـ JAR وستحصل على نفس قدرات كائن المضيف.

### ماذا لو احتجت لتمرير كائنات معقدة؟

يمكنك إتاحة POJOs (كائنات Java بسيطة) التي تحتوي على حقول، getters، وsetters. سيقوم المحرك بتحويلها إلى كائنات JavaScript تلقائيًا. بالنسبة للمجموعات، استخدم `java.util.List` أو المصفوفات — كلاهما قابل للتحويل.

### كيف يعمل التعامل مع الأخطاء؟

إذا ألقى السكريبت خطأ JavaScript، فإن `eval` سيُعيد استثناء `ScriptException`. غلف الاستدعاء بكتلة try‑catch لتسجيل الخطأ أو الاسترداد:

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

### هل يمكن تشغيل عدة سكريبتات بالتتابع؟

بالتأكيد. نسخة `HTMLDocument` نفسها تحتفظ بالنطاق العالمي، لذا يمكنك استدعاء `eval` مرارًا وتكرارًا. فقط احرص على تجنب تصادم أسماء المتغيّرات بين السكريبتات.

## أفضل الممارسات والنصائح

- **سمِّ كائنات المضيف بوضوح** — `javaLogger`، `javaUtils`، إلخ — لتجنب الالتباس.
- **اجعل طرق المضيف صغيرة وخالية من الآثار الجانبية** قدر الإمكان؛ فهذا يسهل عملية التصحيح.
- **حرّر المستند** فور الانتهاء؛ فهو يفرغ الذاكرة الأصلية التي يخصصها Aspose.HTML.
- **تحقق من صحة المدخلات** الواردة من JavaScript، خاصة إذا كانت السكريبتات من مصادر غير موثوقة. عالجها كأي بيانات خارجية.

## الخلاصة

أصبح لديك الآن مثال شامل من البداية إلى النهاية حول كيفية **استدعاء java من javascript** عبر **إضافة كائن مضيف**، **تشغيل JavaScript في Java**، و**تسجيل من JavaScript** باستخدام Aspose.HTML. النمط قوي: يمكن إتاحة أي خدمة Java للسكريبتات، مما يحول تطبيقك إلى منصة سكريبت خفيفة الوزن.

بعد ذلك، قد ترغب في استكشاف:

- حقن صفحة HTML كاملة والتلاعب بـ DOM من خلال JavaScript.
- استخدام كائن المضيف لبث البيانات مرة أخرى إلى جانب Java (مثل تسلسل JSON).
- التكامل مع محركات سكريبت أخرى مثل Nashorn أو GraalVM لدعم لغات أوسع.

جرّبه، عدّل فئات `Logger` أو `Utils`، وشاهد إلى أي مدى يمكنك دفع مفهوم **كائن مضيف JavaScript** في مشاريعك الخاصة.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
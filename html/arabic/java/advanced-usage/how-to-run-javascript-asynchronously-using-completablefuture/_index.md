---
category: general
date: 2026-02-16
description: تعلم كيفية تشغيل JavaScript في Java باستخدام CompletableFuture، وتأخير
  JS، وتقييم الكود غير المتزامن. دليل كامل خطوة بخطوة لتقييم JavaScript غير المتزامن.
draft: false
keywords:
- how to run javascript
- how to use completablefuture
- how to delay js
- how to evaluate async
- evaluate javascript asynchronously
language: ar
og_description: اتقن كيفية تشغيل JavaScript من Java، وتأخير تنفيذ JS، وتقييم الكود
  غير المتزامن باستخدام CompletableFuture في هذا الدرس الشامل.
og_title: كيفية تشغيل جافا سكريبت بشكل غير متزامن باستخدام CompletableFuture
tags:
- javascript
- java
- asynchronous
- completablefuture
title: كيفية تشغيل جافا سكريبت بشكل غير متزامن باستخدام CompletableFuture
url: /ar/java/advanced-usage/how-to-run-javascript-asynchronously-using-completablefuture/
---

.

Proceed.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تشغيل JavaScript بشكل غير متزامن باستخدام CompletableFuture

هل تساءلت يومًا **كيفية تشغيل JavaScript** داخل تطبيق Java دون حجب الخيط الرئيسي؟ ربما تحتاج إلى استدعاء سكريبت صغير يجلب بيانات، لكنك لا تريد أن يتجمد واجهة المستخدم. الخبر السار هو أن مكتبات Java الحديثة تتيح لك تقييم JavaScript **بشكل غير متزامن**، ويمكنك حتى إدخال تأخيرات كما تفعل في المتصفح. في هذا الدليل سنعرض مثالًا كاملاً قابلاً للتنفيذ يستخدم `ScriptEngine` من Aspose HTML مع `CompletableFuture` لتوضيح **كيفية تشغيل JavaScript** والحصول على النتيجة في Java.

سنغطي أيضًا **كيفية استخدام CompletableFuture**، **كيفية تأخير JS**، و**كيفية تقييم الكود غير المتزامن** حتى تتمكن من **تقييم JavaScript بشكل غير متزامن** في أي مشروع Java. بنهاية الدليل ستحصل على قالب جاهز يمكنك نسخه‑ولصقه، وتعديله، وإدراجه في أنظمة أكبر.

---

## ما ستتعلمه

- إعداد `ScriptEngine` في Java يمكنه تنفيذ JavaScript الحديث (ES2022).
- كتابة دالة `async` تتضمن تأخيرًا (`كيفية تأخير js`).
- استدعاء `evaluateAsync` والحصول على `CompletableFuture` (`كيفية استخدام completablefuture`).
- استرجاع النتيجة بمجرد أن يُحلّ الوعد في JavaScript (`كيفية تقييم async`).
- نصائح للتعامل مع الأخطاء، وإدارة الخيوط، وتوسيع النمط.

لا تحتاج إلى أدوات بناء خارجية بخلاف ملف JAR الخاص بـ Aspose HTML for Java، والذي يمكنك وضعه في مسار الـ classpath. لنبدأ.

---

## الخطوة 1: كيفية تشغيل JavaScript – تهيئة محرك البرمجة النصية

أولًا وقبل كل شيء. توفر مكتبة Aspose HTML فئة `ScriptEngine` التي يمكنها تنفيذ شفرة JavaScript. فكر فيها كأنها محرك Chromium صغير يعمل داخل JVM الخاص بك.

```java
import com.aspose.html.scripting.*;
import java.util.concurrent.CompletableFuture;

public class JsAsyncDemo {
    public static void main(String[] args) throws Exception {

        // Create a scripting engine that can run JavaScript
        ScriptEngine scriptEngine = new ScriptEngine();
```

> **لماذا هذا مهم:** بإنشاء كائن `ScriptEngine` نحصل على بيئة معزولة حيث يعمل JavaScript الحديث (بما في ذلك `async/await`) مباشرةً دون الحاجة لتشغيل عملية Node خارجية.

---

## الخطوة 2: كيفية تأخير JS – كتابة دالة Async مع مؤقت قائم على Promise

`setTimeout` في JavaScript هو الطريقة الكلاسيكية لإيقاف التنفيذ مؤقتًا. في الشيفرة الحديثة نغلفه داخل `Promise` حتى نتمكن من `await`ه. هذا هو ما سنفعله في سلسلة النص البرمجي.

```java
        // ES2022 async function that resolves after a short delay
        String asyncScript = """
            async function fetchMessage() {
                const delay = ms => new Promise(r => setTimeout(r, ms));
                await delay(500); // 500 ms pause
                return "Hello from async JS!";
            }
            fetchMessage(); // Return the promise to Java
            """;
```

> **كيفية تأخير js:** الدالة المساعدة `delay` تُنشئ وعدًا يُستكمل بعد `ms` ملي ثانية. عبر `await`ه، تتوقف الدالة دون حجب خيط Java.

---

## الخطوة 3: كيفية تقييم Async – تشغيل النص البرمجي والحصول على CompletableFuture

بدلاً من طريقة `evaluate` المتزامنة، نستدعي `evaluateAsync`. تُعيد فورًا كائن `CompletableFuture<Object>` سيُستكمل عندما يُحلّ وعد JavaScript.

```java
        // Evaluate the script asynchronously – a CompletableFuture is returned
        CompletableFuture<Object> resultFuture = scriptEngine.evaluateAsync(asyncScript);
```

> **كيفية تقييم async:** `evaluateAsync` يربط حلقة أحداث JavaScript مع `CompletableFuture` في Java. هذا هو جوهر **تقييم JavaScript بشكل غير متزامن**.

---

## الخطوة 4: كيفية استخدام CompletableFuture – إرفاق رد نداء وحجب الخيط للعرض التجريبي

الآن نُرفق رد نداء باستخدام `thenAccept` لطباعة النتيجة، ونحجب الخيط الرئيسي لفترة كافية لإنهاء العرض التجريبي.

```java
        // When the promise resolves, print the JavaScript result
        resultFuture.thenAccept(result ->
                System.out.println("JS result: " + result));

        // Block the main thread long enough for the demo to finish
        resultFuture.get(); // throws checked exceptions, handled by main's throws clause
    }
}
```

> **لماذا نستدعي `get()`:** في تطبيق حقيقي ربما تستمر في المعالجة في مكان آخر. هنا نحجب الخيط لجعل المثال مكتملًا ذاتيًا.

---

## نظرة بصرية عامة

![Diagram showing how to run JavaScript asynchronously with CompletableFuture](https://example.com/diagram.png "How to Run JavaScript – Async Flow")

*النص البديل:* **مخطط يوضح كيفية تشغيل JavaScript بشكل غير متزامن باستخدام CompletableFuture** – تُظهر الصورة التدفق من Java إلى محرك النصوص، التأخير غير المتزامن، وإكمال الـ CompletableFuture.

---

## الأخطاء الشائعة وأفضل الممارسات (كيفية تقييم Async بأمان)

| مشكلة | ما يحدث | الحل |
|-------|----------|------|
| نسيان إرجاع الوعد | `evaluateAsync` يُستكمل فورًا بـ `undefined` | تأكد من أن السطر الأخير في النص هو الوعد (`fetchMessage();`) |
| استخدام `Thread.sleep` الحاجز في JS | يحجب حلقة أحداث المحرك، يُفقد الفائدة من الـ async | استخدم نمط وعد `delay` كما هو موضح |
| تجاهل الاستثناءات | الـ Future يُستكمل استثنائيًا، ولا تُرى الأخطاء | أرفق `.exceptionally(e -> { e.printStackTrace(); return null; })` |
| عدم إغلاق المحرك | تسرب موارد في التطبيقات طويلة التشغيل | استدعِ `scriptEngine.dispose()` عند الانتهاء |

---

## توسيع النمط (كيفية استخدام CompletableFuture في المشاريع الحقيقية)

يمكنك ربط عدة استدعاءات JavaScript غير متزامنة، دمجها مع Futures أخرى، أو تشغيلها على `Executor` مخصص. إليك مخطط سريع:

```java
ExecutorService jsPool = Executors.newFixedThreadPool(4);
CompletableFuture<Object> future = scriptEngine.evaluateAsync(asyncScript, jsPool)
    .thenApply(result -> {
        // Post‑process the JS string result
        return ((String) result).toUpperCase();
    })
    .exceptionally(ex -> {
        System.err.println("JS error: " + ex);
        return "fallback";
    });
```

> **كيفية استخدام CompletableFuture:** بتمرير `Executor` تتحكم في مجموعة الخيوط، مما يحافظ على استجابة الواجهة ويتجنب استنزاف الخيوط.

---

## النتيجة المتوقعة

شغِّل الفئة `JsAsyncDemo` وستظهر لك النتيجة التالية:

```
JS result: Hello from async JS!
```

التأخير لمدة 500 ms غير مرئي في وحدة التحكم، لكن يمكنك إضافة طوابع زمنية للتحقق من وجوده إذا رغبت.

---

## ملخص – كيفية تشغيل JavaScript مع CompletableFuture

بدأنا بـ **كيفية تشغيل JavaScript** داخل Java، كتبنا دالة `async` تُظهر **كيفية تأخير js**، نفذناها عبر `evaluateAsync` (**كيفية تقييم async**)، واستقبلنا النتيجة باستخدام **كيفية استخدام completablefuture**. يوضح هذا التدفق الكامل **تقييم JavaScript بشكل غير متزامن** بنمط نظيف وقابل لإعادة الاستخدام.

---

## ما التالي؟

- **الدمج مع عملاء HTTP:** جلب بيانات من نقطة نهاية REST داخل الـ JS غير المتزامن وإرجاعها إلى Java.
- **استخدام نصوص متعددة:** ربط عدة استدعاءات `evaluateAsync` لإنشاء خطوط معالجة معقدة.
- **تبديل المحركات:** يعمل نفس النمط مع Nashorn أو GraalVM أو أي بيئة تشغيل JavaScript أخرى—فقط استبدل `ScriptEngine`.

لا تتردد في تجربة تأخيرات أطول، أو نصوص تُطلق استثناءات، أو حتى وحدات WebAssembly. السماء هي الحد عندما تجمع بين أدوات التزامن في Java وJavaScript الحديث.

---

### هل لديك أسئلة؟

إذا كان هناك ما غير واضح—ربما تتساءل عن كيفية التعامل مع وعد مرفوض أو كيفية تمرير متغيرات من Java إلى النص—اترك تعليقًا أدناه. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
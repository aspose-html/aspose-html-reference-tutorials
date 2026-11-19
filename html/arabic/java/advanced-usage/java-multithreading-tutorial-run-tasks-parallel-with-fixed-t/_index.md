---
category: general
date: 2026-04-05
description: دروس تعدد الخيوط في جافا تُظهر كيفية تشغيل المهام بشكل متوازي باستخدام
  مجموعة خيوط ثابتة في جافا وإغلاق ExecutorService بأمان.
draft: false
keywords:
- java multithreading tutorial
- fixed thread pool java
- shutdown executorservice
- print thread name
- run tasks parallel
language: ar
og_description: دليل جافا للبرمجة المتعددة الخيوط يشرح لك كيفية تشغيل المهام بشكل
  متوازي، وإنشاء مجموعة خيوط ثابتة في جافا، وطباعة اسم الخيط، وإغلاق خدمة التنفيذ
  (ExecutorService) بشكل نظيف.
og_title: دليل تعدد الخيوط في جافا – التنفيذ المتوازي باستخدام مجموعة خيوط ثابتة
tags:
- Java
- Concurrency
- ExecutorService
title: 'دروس تعدد الخيوط في جافا: تشغيل المهام بالتوازي مع مجموعة خيوط ثابتة'
url: /ar/java/advanced-usage/java-multithreading-tutorial-run-tasks-parallel-with-fixed-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java multithreading tutorial – Parallel Execution Made Simple

هل تساءلت يومًا كيف **تشغيل المهام بشكل متوازي** في Java دون الغرق في إدارة الخيوط منخفضة المستوى؟ في هذا **java multithreading tutorial** سنرشدك خطوة بخطوة إلى ذلك: استخدام **fixed thread pool java**، طباعة اسم كل خيط، وإغلاق **shutdown executorservice** بشكل نظيف عندما ينتهي العمل.  

إذا كتبت يومًا حلقة تُعْقِل على إدخال/إخراج الشبكة أو تحتاج إلى استخراج عدة صفحات ويب في آنٍ واحد، فإن النمط الذي نغطيه أدناه سيوفر لك الوقت والصداع.  

سنغطي كل ما تحتاجه—بدون مستندات خارجية، مجرد كود Java نقي يمكنك نسخه‑ولصقه، تشغيله، ورؤية النتائج. في النهاية ستفهم لماذا يُعَدّ fixed thread pool غالبًا الخيار المثالي للتوازي المحدود، وكيفية إيقافه بأمان، وكيفية جعل سجلاتك أكثر قابلية للقراءة بطباعة اسم الخيط.  

> **Prerequisites**: Java 8+ (حزمة `java.util.concurrent` مستقرة منذ سنوات)، بيئة تطوير متكاملة أو سطر أوامر بسيط `javac`/`java`، وفهم أساسي للبرمجة الكائنية OOP. لا توجد مكتبات إضافية مطلوبة بخلاف ملف jar الخاص بـ Aspose HTML for Java الذي لديك بالفعل.

---

![مخطط درس تعدد الخيوط في Java يُظهر مجموعة خيوط تُغذّي المهام](https://example.com/images/java-multithreading-tutorial.png "مخطط درس تعدد الخيوط في Java يُظهر مجموعة خيوط تُغذّي المهام")

## java multithreading tutorial – Set Up a Fixed Thread Pool

**fixed thread pool** يحدّ عدد الخيوط التي تعمل في وقت واحد، مما يمنع تطبيقك من إنشاء الكثير من خيوط نظام التشغيل وإستهلاك الموارد. هنا ننشئ مجموعة بأربعة عمال:

```java
import java.util.concurrent.*;

public class ParallelProcessingTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);
```

*لماذا أربعة؟* يتطابق مع عدد عناوين URL التي سنجلبها، لكن يمكنك ضبط هذا العدد بناءً على عدد نوى المعالج، شدة الإدخال/الإخراج، أو حدود الذاكرة. مصنع `Executors` يحميك من مُنشئ `Thread` منخفض المستوى ويعطيك مرجعًا نظيفًا إلى `ExecutorService` ستقوم لاحقًا **shutdown executorservice** له.

## Prepare URLs and Define Parallel Tasks

بعد ذلك، نُدرج الصفحات التي نريد معالجتها. في برنامج استخراج حقيقي ربما تقرأ هذه القيم من ملف أو قاعدة بيانات، لكن المصفوفة الثابتة تجعل المثال مكتفٍ ذاتيًا:

```java
        // Step 2: List the web pages to process
        String[] pageUrls = {
            "https://example.com/a.html",
            "https://example.com/b.html",
            "https://example.com/c.html",
            "https://example.com/d.html"
        };
```

الآن يأتي جزء **run tasks parallel**. لكل عنوان URL نُرسل دالة لامبدا تقوم بتحميل المستند وطباعة عنوانه. لاحظ استخدام `Thread.currentThread().getName()` – هذه هي حيلة **print thread name** التي تجعل تصحيح الأخطاء أسهل بكثير:

```java
        // Step 3: Submit a task for each URL that loads the document and prints its title
        for (String url : pageUrls) {
            executor.submit(() -> {
                try (HTMLDocument doc = new HTMLDocument(url)) {
                    String title = doc.getTitle();
                    // Print the thread name alongside the title
                    System.out.println(Thread.currentThread().getName() + " – " + title);
                } catch (Exception e) {
                    System.err.println(Thread.currentThread().getName() + " failed: " + e.getMessage());
                }
            });
        }
```

> **Pro tip**: تغليف `HTMLDocument` داخل كتلة try‑with‑resources يضمن إغلاق الدفق الأساسي، حتى إذا فشل تحميل الصفحة.

## Gracefully Shutdown the ExecutorService

ترك مجموعة خيوط نشطة بعد انتهاء عملها يمكن أن يُبقي JVM معطلة. الطريقة الصحيحة هي **shutdown executorservice**، ثم الانتظار حتى الانتهاء:

```java
        // Step 4: Shut down the pool and wait for all tasks to finish
        executor.shutdown();                         // No new tasks will be accepted
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            // Force shutdown if tasks exceed the timeout
            executor.shutdownNow();
        }
    }
}
```

*لماذا المهلة؟* تحميك من مهمة شائنة لا تعود أبداً (مثلاً، مكالمة شبكة تتعطل). إذا لم تنتهِ المجموعة خلال دقيقة واحدة نستدعي `shutdownNow()` لمقاطعة أي خيوط متبقية.

### Expected Output

تشغيل البرنامج يطبع شيئًا مشابهًا لـ:

```
pool-1-thread-1 – Example A
pool-1-thread-3 – Example C
pool-1-thread-2 – Example B
pool-1-thread-4 – Example D
```

قد يختلف الترتيب الفعلي—فالمهام متوازية حقًا. ما يبقى ثابتًا هو بادئة **print thread name**، التي تخبرك بالضبط أي عامل عالج كل عنوان URL.

---

## Common Variations & Edge Cases

| الحالة | ما الذي يجب تغييره | السبب |
|-----------|----------------|--------|
| **مزيد من عناوين URL مقارنةً بعدد الخيوط** | حافظ على نفس حجم المجموعة؛ سيتم وضع المهام الزائدة في قائمة الانتظار تلقائيًا. | مجموعة الخيوط الثابتة تتعامل مع الضغط العكسي (back‑pressure) نيابةً عنك. |
| **عمل يستهلك المعالج** | عيّن حجم المجموعة إلى `Runtime.getRuntime().availableProcessors()` بدلًا من قيمة ثابتة 4. | يحقق أقصى استفادة من المعالج دون تحميل زائد. |
| **الحاجة لإلغاء مهمة معينة** | احتفظ بمرجع `Future<?>` من `executor.submit()` واستدعِ `future.cancel(true)`. | يمنحك تحكمًا دقيقًا في الوظائف الفردية. |
| **معالجة ملفات كبيرة** | زد حجم المجموعة بشكل معتدل *أو* انتقل إلى `newCachedThreadPool()` إذا توقعت فترات نشاط متقطعة. | المجموعات المؤقتة (cached) تنشئ خيوطًا حسب الحاجة، لكن احذر النمو غير المحدود. |

---

## Conclusion

أصبحت الآن تمتلك **java multithreading tutorial** قويًا يُظهر كيف **run tasks parallel** باستخدام **fixed thread pool java**، **print thread name** لتسجيل واضح، و**shutdown executorservice** بشكل نظيف. الكود الكامل القابل للتنفيذ موجود في صف واحد، لذا يمكنك إدراجه في أي مشروع والبدء في توسيع عملك المعتمد على الإدخال/الإخراج فورًا.

ما الخطوة التالية؟ جرّب استبدال `HTMLDocument` بعميل HTTP الخاص بك، جرب أحجام مجموعات مختلفة، أو دمج `CompletionService` لجمع النتائج عند انتهائها. يمكنك أيضًا استكشاف `java.util.concurrent.Flow` لتدفقات رد فعل إذا احتجت إلى معالجة الضغط العكسي (back‑pressure) بما يتجاوز قائمة الانتظار البسيطة.

برمجة سعيدة، وتذكر: مع استراتيجية مجموعة الخيوط المناسبة، يصبح التزامن *قطعة من الكعك*، لا مصدرًا للأخطاء. إذا كان لديك أسئلة، لا تتردد في ترك تعليق—أنا دائمًا مستعد للدردشة حول تزامن Java!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
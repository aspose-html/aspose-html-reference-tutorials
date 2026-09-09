---
category: general
date: 2026-02-10
description: تعلم كيفية استخدام مجموعة خيوط ثابتة في جافا لحساب الصور في ملفات HTML،
  وتشغيل المهام بشكل متزامن في جافا، وإغلاق خدمة التنفيذ بشكل صحيح.
draft: false
keywords:
- java fixed thread pool
- how to count images
- shutdown executor service
- java parallel file processing
- run tasks concurrently java
language: ar
og_description: إتقان استخدام مجموعة الخيوط الثابتة في جافا لحساب الصور، ومعالجة الملفات
  بشكل متوازي، وإغلاق خدمة التنفيذ بأمان.
og_title: 'مجموعة مؤشرات ثابتة في جافا: عدّ الصور في ملفات موازية'
tags:
- Java
- Concurrency
- Aspose.HTML
title: 'مجموعة الخيوط الثابتة في Java: عدّ الصور في الملفات المتوازية'
url: /ar/java/data-handling-stream-management/java-fixed-thread-pool-count-images-in-parallel-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java fixed thread pool – دليل عدّ الصور المتوازي

هل تساءلت يومًا كيف يمكنك **java fixed thread pool** عبر عشرات ملفات HTML والحصول على عدد سريع للصور؟ ربما نظرت إلى دليل من الصفحات، وفكرت “أحتاج إلى معرفة عدد وسوم `<img>` في كل ملف”، ثم أدركت أن حلقة أحادية الخيط ستستغرق إلى الأبد.  

الخبر السار هو أنك لست بحاجة إلى كتابة مدير خيوط مخصص أو التعامل مع كائنات `Thread` منخفضة المستوى. في هذا الدليل سنوضح لك بالضبط **how to count images** باستخدام *java fixed thread pool*، وتشغيل المهام **run tasks concurrently java**، وإغلاق **shutdown executor service** بأناقة عندما يكتمل العمل.  

سنغطي كل شيء من إعداد التجمع، تحضير قائمة الملفات، تقديم المهام المتوازية، التعامل مع الحالات الحدية، إلى التحقق من المخرجات. في النهاية ستحصل على برنامج جاهز للتنفيذ يوضح **java parallel file processing** بطريقة نظيفة وقابلة للصيانة.  

## Prerequisites

قبل أن نبدأ، تأكد من توفر ما يلي:

- Java 17 أو أحدث (الكود يستخدم كلمة المفتاح `var` للتبسيط، لكن يمكنك الرجوع إلى نسخة أقدم إذا لزم الأمر).
- Aspose.HTML for Java في مسار الـ classpath – يمكنك الحصول عليه من Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

- مجموعة من ملفات HTML التي ترغب في تحليلها (الدليل يفترض أنها موجودة في `YOUR_DIRECTORY/`).
- بيئة تطوير أو أداة بناء تشعر بالراحة معها – IntelliJ IDEA، VS Code، أو مجرد `javac` يكفي.

هذا كل شيء. لا خوادم إضافية، لا Docker، مجرد Java عادي ومكتبة طرف ثالث صغيرة.

## Step 1: Create a java fixed thread pool

*java fixed thread pool* يمنحك مجموعة محدودة من خيوط العمل التي تعيد استخدامها لكل مهمة يتم تقديمها. هذا يمنع الحمل الزائد الناتج عن إنشاء خيوط جديدة باستمرار ويحد من مستوى التوازي، وهو أمر حاسم عندما تقرأ ملفات من القرص.

```java
import java.util.concurrent.*;

public class ParallelImageCounter {
    // A pool of 4 threads – adjust based on your CPU cores and I/O profile
    private static final ExecutorService executor = Executors.newFixedThreadPool(4);
}
```

**لماذا 4؟** إذا كان لديك لابتوب رباعي النواة، فإن أربعة خيوط تبقي كل نواة مشغولة دون زيادة الحمل. على خادم يحتوي على نوى أكثر يمكنك زيادة العدد، لكن تذكر أن كل خيط سيفتح مقبض ملف، لذا قد يؤدي العدد الكبير إلى استنفاد حدود نظام التشغيل.

## Step 2: List the HTML files you want to analyse

الخطوة التالية في **java parallel file processing** هي ببساطة بناء مصفوفة (أو `List`) من مسارات الملفات. في مشروع حقيقي قد تقوم بتصفح دليل بصورة متكررة، تصفية حسب الامتداد، أو قراءة المسارات من قاعدة بيانات. إليك النهج المبسط:

```java
String[] htmlFiles = {
    "YOUR_DIRECTORY/a.html",
    "YOUR_DIRECTORY/b.html",
    "YOUR_DIRECTORY/c.html",
    "YOUR_DIRECTORY/d.html"
};
```

إذا كنت بحاجة إلى التعامل مع مجموعة ديناميكية، استبدل المصفوفة الثابتة بشيء مثل:

```java
Path dir = Paths.get("YOUR_DIRECTORY");
String[] htmlFiles = Files.list(dir)
                         .filter(p -> p.toString().endsWith(".html"))
                         .map(Path::toString)
                         .toArray(String[]::new);
```

هذا المقتطف يوضح **java parallel file processing** لأي عدد من الملفات دون الحاجة لتغيير باقي الكود.

## Step 3: Submit tasks to **run tasks concurrently java**

الآن يأتي قلب الدليل – سنقوم بـ **run tasks concurrently java** عن طريق تقديم لامبدا لكل ملف. كل مهمة تقوم بتحميل مستند HTML باستخدام Aspose.HTML، تستعلم عن جميع عناصر `<img>`، وتطبع العدد.

```java
import com.aspose.html.HTMLDocument;

public static void main(String[] args) throws InterruptedException {
    for (String filePath : htmlFiles) {
        executor.submit(() -> {
            // Load the document – Aspose.HTML does the heavy lifting
            HTMLDocument document = new HTMLDocument(filePath);
            // querySelectorAll returns a NodeList; its length is the image count
            int imageCount = document.querySelectorAll("img").length;
            System.out.println(filePath + " contains " + imageCount + " images.");
        });
    }

    // Step 4 is next – gracefully shut down the pool
    shutdownAndAwaitTermination();
}
```

**لماذا نستخدم لامبدا؟** لأنها تجعل الكود مختصرًا وتجنب إنشاء فئة `Runnable` منفصلة. اللامبدا تلتقط `filePath` تلقائيًا، لذا كل مهمة تعمل على ملفها الخاص.

### How to **count images** efficiently

Aspose.HTML يحلل الملف مرة واحدة، يبني شجرة DOM، ثم `querySelectorAll("img")` يعمل في O(n) حيث *n* هو عدد العقد. بالنسبة لمعظم صفحات HTML هذا لا يُحدث فرقًا ملحوظًا. إذا كنت تحتاج إلى نهج أسرع يعتمد على التدفق فقط (مثلاً للملفات بحجم جيجابايت)، يمكنك التحول إلى محلل SAX، لكن ذلك سيُفقدنا البساطة التي نسعى إليها.

## Step 4: Properly **shutdown executor service**

لا تنسَ أبدًا إغلاق التجمع، وإلا سيستمر الـ JVM في العمل إلى الأبد. النمط أدناه هو الطريقة الموصى بها لـ **shutdown executor service** مع انتظار انتهاء جميع المهام:

```java
private static void shutdownAndAwaitTermination() {
    executor.shutdown(); // Disable new tasks from being submitted
    try {
        // Wait a while for existing tasks to terminate
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            executor.shutdownNow(); // Cancel currently executing tasks
            // Wait a second for tasks to respond to being cancelled
            if (!executor.awaitTermination(30, TimeUnit.SECONDS))
                System.err.println("Pool did not terminate");
        }
    } catch (InterruptedException ie) {
        // (Re-)Cancel if current thread also interrupted
        executor.shutdownNow();
        // Preserve interrupt status
        Thread.currentThread().interrupt();
    }
}
```

**ماذا لو علقت مهمة؟** استدعاء `shutdownNow()` يحاول مقاطعة الخيوط العاملة. إذا كان منطق عدّ الصور يحترم المقاطعة (وAspose.HTML لا يحجز على I/O)، سيتوقف التجمع بنظافة. هذا النمط هو المعيار الذهبي لأي استخدام **java fixed thread pool**.

## Step 5: Verify the output

شغّل البرنامج من داخل IDE أو عبر سطر الأوامر:

```bash
javac -cp "path/to/aspose-html.jar" ParallelImageCounter.java
java -cp ".:path/to/aspose-html.jar" ParallelImageCounter
```

المخرجات النموذجية تكون كالتالي:

```
YOUR_DIRECTORY/a.html contains 5 images.
YOUR_DIRECTORY/b.html contains 0 images.
YOUR_DIRECTORY/c.html contains 12 images.
YOUR_DIRECTORY/d.html contains 3 images.
```

إذا رأيت العدّات مطبوعة بترتيب عشوائي، فهذا متوقع – الخيوط تنتهي في أوقات مختلفة. المهم أن كل ملف تم احتسابه وأن البرنامج يخرج بنظافة بعد عملية الإغلاق.

## Full Working Example (Copy‑Paste Ready)

```java
import com.aspose.html.HTMLDocument;
import java.util.concurrent.*;

public class ParallelImageCounter {
    // 1️⃣ Fixed thread pool – change size based on your hardware
    private static final ExecutorService executor = Executors.newFixedThreadPool(4);

    public static void main(String[] args) throws InterruptedException {
        // 2️⃣ List of HTML files – replace with your own directory
        String[] htmlFiles = {
            "YOUR_DIRECTORY/a.html",
            "YOUR_DIRECTORY/b.html",
            "YOUR_DIRECTORY/c.html",
            "YOUR_DIRECTORY/d.html"
        };

        // 3️⃣ Submit a counting task for each file
        for (String filePath : htmlFiles) {
            executor.submit(() -> {
                HTMLDocument document = new HTMLDocument(filePath);
                int imageCount = document.querySelectorAll("img").length;
                System.out.println(filePath + " contains " + imageCount + " images.");
            });
        }

        // 4️⃣ Gracefully shut down the pool
        shutdownAndAwaitTermination();
    }

    // 5️⃣ Helper method to cleanly stop the executor
    private static void shutdownAndAwaitTermination() {
        executor.shutdown(); // Disable new tasks
        try {
            if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
                executor.shutdownNow(); // Cancel currently executing tasks
                if (!executor.awaitTermination(30, TimeUnit.SECONDS))
                    System.err.println("Pool did not terminate");
            }
        } catch (InterruptedException ie) {
            executor.shutdownNow();
            Thread.currentThread().interrupt();
        }
    }
}
```

### Expected Result

تشغيل المقتطف يطبع مسار كل ملف متبوعًا بعدد وسوم `<img>` الموجودة فيه، ثم يخرج الـ JVM. لا خيوط متبقية، لا تسريبات ذاكرة.

## Common Pitfalls & Pro Tips

- **Pitfall:** استخدام `newCachedThreadPool()` بدلاً من *fixed* pool. ذلك يُنشئ خيوطًا غير محدودة، مما قد يستنفد مقابض الملفات عند دفعات كبيرة. التزم بـ `newFixedThreadPool`.
- **Pro tip:** إذا كانت ملفات HTML ضخمة، فكر في زيادة حجم الـ heap (`-Xmx2g`) أو التحول إلى محلل تدفق. بالنسبة لمعظم صفحات التسويق، الـ heap الافتراضي يكفي.
- **Pitfall:** نسيان استدعاء `shutdown()` – سيظل تطبيقك معلقًا بعد طباعة النتائج. طريقة `shutdownAndAwaitTermination` أعلاه تتعامل مع ذلك بمرونة.
- **Pro tip:** سجّل وقت بدء وانتهاء كل مهمة إذا كنت بحاجة إلى مقاييس الأداء. `System.nanoTime()` قبل وبعد إنشاء `HTMLDocument` يخبرك بمدة التحليل.
- **Pitfall:** تثبيت عدد الخيوط يدويًا. استخدم `Runtime.getRuntime().availableProcessors()` لاختيار قيمة افتراضية معقولة:

```java
int cores = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(cores);
```

## Related Topics You Might Explore Next

- **run tasks concurrently java** مع `CompletableFuture` لإنشاء خطوط معالجة أكثر تعبيرًا.
- حفظ عدد الصور في قاعدة بيانات لتقارير التحليل.
- استخدام **java parallel file processing** مع API `java.nio.file.Files.walk` مع الـ streams.
- تنفيذ `ThreadFactory` مخصص لإعطاء الخيوط أسماء ذات معنى (يساعد في عملية التصحيح).

## Conclusion

لقد استعرضنا مثالًا كاملًا ومستقلاً يوضح كيف يمكن الاستفادة من **java fixed thread pool** لـ **how to count images** عبر ملفات HTML متعددة، مع إظهار الطريقة الصحيحة لـ **shutdown executor service**. النمط قابل للتوسع بسهولة – استبدل مصفوفة الملفات بقائمة ديناميكية، زد حجم التجمع، وستحصل على حل قوي لأي عبء عمل **java parallel file processing**.  

جرّبه، عدّل عدد الخيوط، وربما أضف تصدير CSV للنتائج. السماء هي الحد عندما تجمع بين أساسيات التزامن الصلبة ومكتبة مفيدة مثل Aspose.HTML. Happy coding!  

![java fixed thread pool diagram](image.png){alt="مخطط java fixed thread pool"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
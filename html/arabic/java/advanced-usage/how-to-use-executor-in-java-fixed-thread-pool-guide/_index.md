---
category: general
date: 2026-05-28
description: كيفية استخدام الـ Executor في جافا مع مجموعة خيوط ثابتة، استخراج النص
  من HTML وتسريع المعالجة – مثال كامل على مجموعة خيوط جافا.
draft: false
keywords:
- how to use executor
- fixed thread pool java
- extract text from html
- java thread pool example
- create fixed thread pool
language: ar
og_description: كيفية استخدام الـ Executor في جافا مع مجموعة خيوط ثابتة. تعلّم مثالًا
  كاملاً لمجموعة خيوط جافا يَستخرج النص من ملفات HTML بكفاءة.
og_title: كيفية استخدام Executor في Java – دليل مجموعة الخيوط الثابتة
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: how to use executor in Java with a fixed thread pool, extract text
    from HTML and speed up processing – a complete java thread pool example.
  headline: How to Use Executor in Java – Fixed Thread Pool Guide
  type: TechArticle
tags:
- Java
- Concurrency
- HTML Parsing
title: كيفية استخدام Executor في جافا – دليل مجموعة الخيوط الثابتة
url: /ar/java/advanced-usage/how-to-use-executor-in-java-fixed-thread-pool-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام Executor في Java – دليل مجموعة الخيوط الثابتة

هل تساءلت يومًا **كيف تستخدم executor** لتشغيل العديد من المهام في آن واحد دون استنزاف الذاكرة؟ لست وحدك. في العديد من التطبيقات الواقعية ستحتاج إلى استكشاف مجلد من ملفات HTML، استخراج نص الـ body، والقيام بذلك بسرعة—وهو بالضبط السيناريو الذي يحله هذا الدرس.

سنستعرض تنفيذ **fixed thread pool java** يقتطف النص من HTML، يطبع عدد الأحرف لكل ملف، ويغلق نفسه بشكل نظيف. في النهاية ستحصل على **java thread pool example** مستقل يمكنك إدراجه في أي مشروع، بالإضافة إلى بعض النصائح لتخصيص حجم المجموعة ومعالجة الحالات الخاصة.

> **ما ستحتاجه**  
> * Java 17 (أو أي JDK حديث)  
> * مكتبة صغيرة لتحليل HTML – سنستخدم *jsoup* لأنها مجربة ولا تحتاج إعدادات.  
> * مجموعة من ملفات *.html* التجريبية في دليل تختاره.

---

## كيفية استخدام Executor مع مجموعة خيوط ثابتة

قلب أي برنامج Java يعتمد على التزامن هو `ExecutorService`. بإنشاء **fixed thread pool** نخبر JVM بالحفاظ على عدد محدد من خيوط العاملين حية، مما يمنع تكلفة إنشاء الخيوط ويحد من استهلاك الموارد.

```java
// Step 1: Build a fixed‑size thread pool (4 workers in this case)
ExecutorService executor = Executors.newFixedThreadPool(4);
```

*لماذا هذا مهم:*  
إذا قمت بإنشاء `Thread` جديد لكل ملف HTML، سيتعين على نظام التشغيل جدولة عشرات الخيوط على حاسوب محمول عادي، مما يؤدي إلى تبادل سياق مفرط. مجموعة ثابتة تعيد استخدام نفس الخيوط الأربعة، مما يمنحك استخدامًا متوقعًا للمعالج.

---

## تعريف ملفات HTML التي سيتم معالجتها – Fixed Thread Pool Java

بعد ذلك نُدرج الملفات التي نريد إدخالها في المجموعة. في تطبيق حقيقي ربما تتجول في شجرة الدلائل؛ هنا نبقي الأمور بسيطة.

```java
// Step 2: List the HTML documents you want to parse
List<String> htmlFilePaths = List.of(
        "YOUR_DIRECTORY/a.html",
        "YOUR_DIRECTORY/b.html",
        "YOUR_DIRECTORY/c.html",
        "YOUR_DIRECTORY/d.html"
);
```

*نصيحة:* `List.of` تُعيد قائمة غير قابلة للتغيير، وهي آمنة للمشاركة بين الخيوط دون الحاجة إلى مزامنة إضافية.

---

## إرسال مهمة منفصلة لكل ملف HTML

الآن نمرر كل مسار إلى الـ executor. الدالة المجهولة (lambda) التي نُرسلها ستعمل **بالتوازي** على أحد الخيوط الأربعة العاملة.

```java
// Step 3: Dispatch a parsing job for every file
for (String htmlFilePath : htmlFilePaths) {
    executor.submit(() -> {
        // Each lambda runs on a thread from the pool
        try {
            // Step 4: Open the document, extract its text, and display the length
            String text = extractBodyText(htmlFilePath);
            System.out.println(htmlFilePath + " → " + text.length() + " chars");
        } catch (IOException e) {
            System.err.println("Failed to read " + htmlFilePath);
            e.printStackTrace();
        }
    });
}
```

**السبب في تغليف المنطق داخل طريقة** (`extractBodyText`) سيتضح في القسم التالي—ذلك يبقي الـ lambda منظمًا ويسمح لنا بإعادة استخدام كود الاستخراج في أماكن أخرى.

---

## استخراج النص من HTML – المنطق الأساسي

إليك الدالة المساعدة القابلة لإعادة الاستخدام التي **تستخرج النص من html** باستخدام Jsoup. تفتح الملف، تحلل DOM، وتعيد نص الـ body النقي.

```java
/**
 * Reads an HTML file and returns the plain text inside the <body>.
 *
 * @param path absolute or relative path to the .html file
 * @return body text without tags
 * @throws IOException if the file cannot be read
 */
private static String extractBodyText(String path) throws IOException {
    // Jsoup parses the file into a Document object.
    org.jsoup.nodes.Document doc = org.jsoup.Jsoup.parse(new java.io.File(path), "UTF-8");
    // getBody() gives us the <body> element; text() strips all tags.
    return doc.body().text();
}
```

*لماذا Jsoup؟* إنها خفيفة الوزن، تتعامل مع العلامات غير الصحيحة بأريحية، ولا تحتاج إلى محرك متصفح كامل. الطريقة تُطلق استثناء `IOException` حتى يقرر المستدعي كيفية التسجيل أو الاسترداد—مثالي لسيناريو مجموعة الخيوط حيث لا تريد أن يتسبب ملف واحد سيء في إيقاف الـ executor بالكامل.

---

## إغلاق الـ Executor بأمان – إنشاء مجموعة خيوط ثابتة

بعد أن أرسلنا جميع الوظائف، يجب أن نخبر المجموعة بالتوقف عن قبول أعمال جديدة وإنهاء ما هو مُدخل بالفعل في القائمة.

```java
// Step 5: Initiate an orderly shutdown once all tasks are queued
executor.shutdown();
try {
    // Wait up to 30 seconds for all tasks to finish
    if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
        System.err.println("Timed out waiting for tasks; forcing shutdown.");
        executor.shutdownNow();
    }
} catch (InterruptedException ie) {
    // Preserve interrupt status and force shutdown
    Thread.currentThread().interrupt();
    executor.shutdownNow();
}
```

*شرح:* `shutdown()` يمنع الإرسال الجديد، بينما `awaitTermination` ينتظر حتى تنتهي جميع وظائف التحليل (أو ينتهي المهلة). إذا علقت عملية ما، فإن `shutdownNow()` يحاول إلغاء المهام الجارية. هذا النمط هو الطريقة الموصى بها لإنشاء **fixed thread pool** بأمان.

---

## مثال كامل قابل للتنفيذ

بدمج كل شيء معًا، إليك ملف واحد يمكنك تجميعه وتشغيله. يتضمن الاستيرادات الضرورية، طريقة `main`، والدالة المساعدة الموضحة أعلاه.

```java
import java.io.IOException;
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

/**
 * Demonstrates how to use executor with a fixed thread pool to
 * extract text from multiple HTML files concurrently.
 */
public class HtmlThreadPoolDemo {

    public static void main(String[] args) {
        // 1️⃣ Build a fixed‑size pool (adjust the size for your hardware)
        ExecutorService executor = Executors.newFixedThreadPool(4);

        // 2️⃣ Define the files we want to process
        List<String> htmlFilePaths = List.of(
                "YOUR_DIRECTORY/a.html",
                "YOUR_DIRECTORY/b.html",
                "YOUR_DIRECTORY/c.html",
                "YOUR_DIRECTORY/d.html"
        );

        // 3️⃣ Submit a parsing task for each file
        for (String htmlFilePath : htmlFilePaths) {
            executor.submit(() -> {
                try {
                    String text = extractBodyText(htmlFilePath);
                    System.out.println(htmlFilePath + " → " + text.length() + " chars");
                } catch (IOException e) {
                    System.err.println("Error processing " + htmlFilePath);
                    e.printStackTrace();
                }
            });
        }

        // 5️⃣ Shut down the pool cleanly
        executor.shutdown();
        try {
            if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
                System.err.println("Tasks took too long; forcing shutdown.");
                executor.shutdownNow();
            }
        } catch (InterruptedException ie) {
            Thread.currentThread().interrupt();
            executor.shutdownNow();
        }
    }

    /**
     * Reads an HTML file and returns the plain text inside the <body>.
     *
     * @param path path to the .html file
     * @return body text without markup
     * @throws IOException if file cannot be read
     */
    private static String extractBodyText(String path) throws IOException {
        Document doc = Jsoup.parse(new java.io.File(path), "UTF-8");
        return doc.body().text();
    }
}
```

**الناتج المتوقع** (بافتراض أن كل ملف يحتوي تقريبًا على 1 200 حرف من نص الـ body):

```
YOUR_DIRECTORY/a.html → 1234 chars
YOUR_DIRECTORY/b.html → 1198 chars
YOUR_DIRECTORY/c.html → 1305 chars
YOUR_DIRECTORY/d.html → 1120 chars
```

إذا كان أي ملف مفقودًا أو غير صالح، ستظهر لك تتبع الأخطاء في `stderr`، لكن المهام الأخرى ستستمر دون تأثر—وهذا بالضبط ما يجب أن يفعله **java thread pool example** المتقن.

---

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|----------|--------|
| *ماذا لو كان لدي أكثر من أربعة ملفات؟* | ستضع المجموعة المهام الزائدة في قائمة الانتظار وتنفذها بمجرد أن يصبح أحد الخيوط فارغًا. لا حاجة إلى كود إضافي. |
| *هل يجب أن أستخدم `newCachedThreadPool` بدلاً من ذلك؟* | `newCachedThreadPool` ينشئ خيوطًا عند الطلب ويمكن أن ينمو بلا حدود، وهو أمر محفوف بالمخاطر للوظائف الثقيلة على I/O. **fixed thread pool** يمنحك استخدامًا متوقعًا للذاكرة والمعالج. |
| *كيف أغيّر حجم المجموعة بناءً على عدد نوى المعالج؟* | `int cores = Runtime.getRuntime().availableProcessors(); ExecutorService exec = Executors.newFixedThreadPool(cores);` هو نمط شائع. |
| *ماذا لو فشل التحليل لملف واحد؟* | `catch (IOException e)` داخل الـ lambda يعزل الفشل، يسجله، ويسمح لبقية المجموعة بالاستمرار في العمل. |
| *هل يمكنني إرجاع النص المستخرج إلى المستدعي؟* | نعم—استخدم `Future<String>` بدلاً من `submit(Runnable)`. سيبدو الكود هكذا `Future<String> f = executor.submit(() -> extractBodyText(path));` ثم لاحقًا `String result = f.get();`. |

---

## الخلاصة

غطينا **كيف تستخدم executor** لإنشاء **fixed thread pool java** يعالج مجموعة من ملفات HTML بالتوازي، يستخرج نص الـ body، ويُظهر عدد الأحرف. يُظهر **java thread pool example** الكامل إدارة موارد صحيحة، معالجة أخطاء، وطريقة استخراج قابلة لإعادة الاستخدام.

ما الخطوة التالية؟ جرّب استبدال تنفيذ `extractBodyText` بمستخرج أكثر تعقيدًا، جرب حجم مجموعة أكبر، أو أدخل النتائج إلى قاعدة بيانات. يمكنك أيضًا استكشاف `CompletionService` لاستلام النتائج فور جاهزيتها، وهو مفيد عندما تختلف أحجام الملفات بشكل كبير.

لا تتردد في تعديل مسار الدليل، إضافة ملفات أخرى، أو دمج هذا المقتطف في إطار عمل زحف أكبر. النمط الأساسي—إنشاء مجموعة، إرسال مهام مستقلة، وإغلاقها بأمان—يبقى هو نفسه مهما تعقّبت عبء العمل.

برمجة سعيدة، ولتظل خيوطك حية دائمًا (حتى تقوم بإغلاقها، بالطبع)!

## دروس ذات صلة

- [Fixed thread pool java – Parallel HTML Cleaning with ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Use Aspose.HTML for Java - Mastering HTML5 Canvas Rendering](/html/english/java/html5-canvas-rendering/html5-canvas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
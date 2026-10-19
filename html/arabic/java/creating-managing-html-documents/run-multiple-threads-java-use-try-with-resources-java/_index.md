---
category: general
date: 2026-04-09
description: تشغيل عدة خيوط في جافا بكفاءة باستخدام try‑with‑resources في جافا. تعلم
  كيفية تحميل مستند HTML في جافا بأمان وتجنب مشكلات التزامن في جافا.
draft: false
keywords:
- run multiple threads java
- use try with resources java
- load html document java
- avoid concurrency issues java
language: ar
og_description: تشغيل عدة خيوط جافا باستخدام try‑with‑resources جافا. يوضح هذا الدرس
  كيفية تحميل مستند HTML جافا بأمان مع تجنب مشاكل التزامن جافا.
og_title: تشغيل عدة خيوط في جافا – دليل try-with-resources
tags:
- java
- multithreading
- html-parsing
title: تشغيل خيوط متعددة في جافا – استخدام try with resources في جافا
url: /ar/java/creating-managing-html-documents/run-multiple-threads-java-use-try-with-resources-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تشغيل عدة خيوط في جافا – استخدم try‑with‑resources في جافا

هل تساءلت يوماً كيف **تشغيل عدة خيوط جافا** دون أن تتعارض مع بعضها البعض؟ لست وحدك—معظم المطورين يواجهون نفس المشكلة عندما يحاولون مشاركة كائن قابل للتغيير عبر الخيوط. الخبر السار؟ هناك طريقة حديثة ونظيفة للقيام بذلك، وتبدأ بعبارة `try‑with‑resources`.

في هذا الدليل سنستعرض مثالاً كاملاً جاهزاً للنسخ واللصق **يحمّل مستند HTML جافا**، يُنشئ عدة خيوط، ويضمن أن كل خيط يعمل على نسخة خاصة به من المستند. في النهاية ستتعرف أيضاً على كيفية **تجنّب مشاكل التزامن جافا** لتظل تطبيقاتك مستقرة تحت الحمل.

> **ما ستحصل عليه:** برنامج جافا قابل للتنفيذ، شروحات خطوة بخطوة، نصائح للمشاريع الواقعية، واختبار سريع يمكنك تشغيله الآن.

---

![رسم توضيحي لتشغيل عدة خيوط في جافا](run-multiple-threads-java.png "مخطط يوضح عدة خيوط كل منها يحمل نسخة منفصلة من HTMLDocument instance")

## المتطلبات المسبقة

- Java 17 أو أحدث (صيغة `try‑with‑resources` تعمل بنفس الطريقة منذ Java 7، لكننا سنستخدم ميزات اللغة الحديثة لتقليل الكود).  
- فئة مساعدة صغيرة لتحليل HTML تُدعى `HTMLDocument`. إذا لم تكن لديك، يمكنك إنشاء نسخة تجريبية كما هو موضح لاحقاً.  
- معرفة أساسية بالخيوط (`java.lang.Thread`) وواجهة `Runnable`.

إذا كان أي من هذه غير مألوف لك، لا تقلق—سيتم إعادة شرح كل مفهوم في الخطوات التالية.

---

## الخطوة 1: تحميل مستند HTML جافا باستخدام مرجع مشترك

أول شيء نحتاجه هو مرجع *مشترك* يشير إلى الملف الذي نريد تحليله. فكر فيه كخريطة: الـ URL هو نفسه لكل خيط، لكن كائن المستند الفعلي سيُنشأ لكل خيط لاحقاً.

```java
// Step 1: Load the source HTML document (shared reference for its URL)
HTMLDocument sharedDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");
```

### لماذا مرجع مشترك؟

إذا حاولت إعطاء كل خيط نفس نسخة `HTMLDocument`، فستقوم جميعها بالقراءة والكتابة إلى نفس المخازن الداخلية. هذا وصفة كلاسيكية لحدوث حالات سباق—بالضبط النوع من **مشاكل التزامن جافا** التي نحاول تجنّبها. من خلال مشاركة الـ *URL* فقط، يمكن لكل خيط فتح تدفقه الخاص بأمان لاحقاً.

> **نصيحة احترافية:** احفظ الـ URL في متغيّر `final` إذا لم تكن تنوي تغييره أبداً. سيعامل المترجم ذلك كقيمة ثابتة، مما يقلل من احتمال تعديل غير مقصود.

---

## الخطوة 2: إنشاء مهمة آمنة للخيط باستخدام try‑with‑resources جافا

الآن نحدد ما يفعله كل خيط فعلياً. الفكرة هي تغليف إنشاء `HTMLDocument` لكل خيط داخل كتلة `try‑with‑resources`. هذا يضمن إغلاق المستند تلقائياً، حتى لو ارتفعت استثناءات.

```java
// Step 2: Define a task that creates its own document instance per thread
Runnable task = () -> {
    // Each thread works with its own copy to avoid concurrency issues
    try (HTMLDocument threadDoc = new HTMLDocument(sharedDoc.getUrl())) {
        // Perform thread‑specific operations on threadDoc here
        System.out.println("Thread " + Thread.currentThread().getName()
                + " loaded: " + threadDoc.getTitle());
    } catch (Exception e) {
        System.err.println("Error in thread " + Thread.currentThread().getName()
                + ": " + e.getMessage());
    }
};
```

### كيف يساعد `try‑with‑resources`

فئة `HTMLDocument` تُنفّذ `java.lang.AutoCloseable`. عندما تنتهي كتلة `try`، تستدعي JVM تلقائياً `threadDoc.close()`. هذا أكثر أماناً بكثير من استخدام عبارة `finally` يدوية ويزيل خطر نسيان تحرير الموارد الأصلية—وهو ما قد يؤدي بسهولة إلى تسرب الذاكرة في التطبيقات متعددة الخيوط طويلة التشغيل.

---

## الخطوة 3: تشغيل الخيوط وتجنّب مشاكل التزامن جافا

مع جاهزية المهمة، يمكننا إنشاء عدد الخيوط التي نريدها. للتوضيح، سنبدأ بخيطين، لكن لا شيء يمنعك من تشغيل مجموعة خيوط (ThreadPool) تضم عشرات العمال.

```java
// Step 3: Launch multiple threads that execute the same task
Thread t1 = new Thread(task, "Worker‑1");
Thread t2 = new Thread(task, "Worker‑2");

// Start the threads
t1.start();
t2.start();

// Optional: wait for them to finish (join) if you need deterministic ordering
t1.join();
t2.join();
```

### لماذا لا نستخدم `ExecutorService`؟

في الكود الإنتاجي ربما **ستستخدم** `ExecutorService` لإدارة مجموعة من العمال. مثال الـ `Thread` البسيط يبقي الدرس مركزاً على الفكرة الأساسية—إنشاء مستند منفصل لكل خيط مع استخدام `try‑with‑resources`. لا تتردد في استبدال استدعاءات `Thread` بـ `FixedThreadPool` إذا كان ذلك يتماشى مع بنية مشروعك.

---

## مثال كامل قابل للتنفيذ

بدمج كل ما سبق، إليك برنامج مستقل يمكنك وضعه في ملف اسمه `MultiThreadHtmlDemo.java`. يتضمن نسخة تجريبية بسيطة من `HTMLDocument` لتتمكن من تجميعه وتشغيله فوراً.

```java
// MultiThreadHtmlDemo.java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;

// --- Minimal stub for demonstration purposes ---
class HTMLDocument implements AutoCloseable {
    private final String url;
    private String content;

    public HTMLDocument(String url) throws IOException {
        this.url = url;
        // Simulate loading the file (replace with real parser in production)
        this.content = Files.readString(Path.of(url));
    }

    public String getUrl() {
        return url;
    }

    public String getTitle() {
        // Very naive title extraction – just for demo
        int start = content.indexOf("<title>");
        int end = content.indexOf("</title>");
        if (start != -1 && end != -1 && end > start) {
            return content.substring(start + 7, end).trim();
        }
        return "Untitled";
    }

    @Override
    public void close() {
        // In a real library you’d release native buffers here
        content = null;
        System.out.println("Closed document for URL: " + url);
    }
}

// --- Main class that runs multiple threads java ---
public class MultiThreadHtmlDemo {
    public static void main(String[] args) throws InterruptedException, IOException {
        // Step 1: Load the source HTML document (shared reference for its URL)
        HTMLDocument sharedDoc = new HTMLDocument("sample.html");

        // Step 2: Define a task that creates its own document instance per thread
        Runnable task = () -> {
            try (HTMLDocument threadDoc = new HTMLDocument(sharedDoc.getUrl())) {
                System.out.println("Thread " + Thread.currentThread().getName()
                        + " loaded title: " + threadDoc.getTitle());
            } catch (Exception e) {
                System.err.println("Error in thread " + Thread.currentThread().getName()
                        + ": " + e.getMessage());
            }
        };

        // Step 3: Launch multiple threads that execute the same task
        Thread t1 = new Thread(task, "Worker‑1");
        Thread t2 = new Thread(task, "Worker‑2");

        t1.start();
        t2.start();

        // Wait for both threads to finish
        t1.join();
        t2.join();

        System.out.println("All threads completed.");
    }
}
```

#### النتيجة المتوقعة (بافتراض أن `sample.html` يحتوي على `<title>Hello World</title>`)

```
Thread Worker-1 loaded title: Hello World
Closed document for URL: sample.html
Thread Worker-2 loaded title: Hello World
Closed document for URL: sample.html
All threads completed.
```

لاحظ كيف يطبع كل خيط عنوانه *المحمَّل* ثم تُستدعى طريقة `close()` تلقائياً—تماماً ما يَعِد به `try‑with‑resources`.

---

## أسئلة شائعة ومعالجة الحالات الخاصة

**ماذا لو لم يُعثر على الملف؟**  
المُنشئ يرمي `IOException`. في المثال نلتقط الاستثناء داخل الـ `Runnable` ونسجل خطأ، لذا فإن فقدان الملف لن يتسبب في تعطل التطبيق بالكامل.

**هل يمكنني إعادة استخدام نفس نسخة `HTMLDocument` عبر الخيوط؟**  
فقط إذا تم توثيق الفئة صراحةً بأنها آمنة للخيوط. معظم المحللات تحتفظ بحالة قابلة للتغيير (مثل شجرات DOM)، لذا مشاركة نسخة واحدة عادةً ما تؤدي إلى **مشاكل التزامن جافا**. النمط الموضح هنا—نسخة واحدة لكل خيط—هو الأكثر أماناً كإعداد افتراضي.

**هل أحتاج إلى مزامنة أي شيء؟**  
لا. لأن كل خيط يعمل على نسخة خاصة به من `HTMLDocument`، لا يوجد حالة مشتركة قابلة للتغيير تحتاج إلى حماية. العنصر المشترك الوحيد هو سلسلة الـ URL، وهي غير قابلة للتغيير.

**كيف سيبدو هذا مع `ExecutorService`؟**  

```java
ExecutorService executor = Executors.newFixedThreadPool(4);
for (int i = 0; i < 4; i++) {
    executor.submit(task);
}
executor.shutdown();
executor.awaitTermination(1, TimeUnit.MINUTES);
```

المنطق الأساسي يبقى هو نفسه؛ الفِرْق فقط يدير دورات حياة الخيوط نيابةً عنك.

---

## نصائح احترافية للبرمجة المتعددة الخيوط على مستوى الإنتاج

1. **حدّ عدد الخيوط** – إنشاء عشرات كائنات `Thread` خام قد يثقل كاهل نظام التشغيل. استخدم مجموعة خيوط محدودة بدلاً من ذلك.  
2. **فضّل الإعدادات غير القابلة للتغيير** – احتفظ بـ URLs، مسارات الملفات، وإعدادات المحلل غير قابلة للتغيير حتى لا تُغيّرها عن غير قصد من قبل عامل.  
3. **راقب استهلاك الموارد** – حتى مع `try‑with‑resources`، فتح العديد من الملفات في آنٍ واحد قد يستنفد مقابض الملفات. قلل عدد المهام المتزامنة إذا وصلت إلى حدود.  
4. **إغلاق سلس** – احرص دائماً على إغلاق الـ executor أو الانضمام إلى الخيوط حتى يتمكن JVM من الإنهاء بنظافة.

---

## الخلاصة

أصبح لديك الآن نمط ثابت وجاهز للنسخ واللصق حول كيفية **تشغيل عدة خيوط جافا** مع الاستخدام الآمن لـ **try‑with‑resources جافا**، **تحميل مستند HTML جافا**، و**تجنّب مشاكل التزامن جافا**. الفكرة الأساسية بسيطة: أعط كل خيط نسخة خاصة به من المستند، دع بنية `try‑with‑resources` تتولى عملية التنظيف، واحفظ البيانات المشتركة غير قابلة للتغيير.

من هنا يمكنك استكشاف:

- توسيع النمط باستخدام `ExecutorService` وطابور عمل.  
- التحويل إلى محلل HTML حقيقي مثل *jsoup* (الذي يُنفّذ أيضاً `Closeable`).  
- إضافة معالجة أخطاء أكثر تعقيداً أو منطق إعادة المحاولة للعمليات غير المستقرة.

جرّبه، عدّل عدد العمال، وشاهد مخرجات وحدة التحكم تبقى مرتبة—no

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
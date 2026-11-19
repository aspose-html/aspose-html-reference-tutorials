---
category: general
date: 2026-04-05
description: जावा मल्टीथ्रेडिंग ट्यूटोरियल जो दिखाता है कि फिक्स्ड थ्रेड पूल जावा
  का उपयोग करके टास्क को समानांतर कैसे चलाएँ और एक्सीक्यूटरसर्विस को सुरक्षित रूप
  से शटडाउन करें।
draft: false
keywords:
- java multithreading tutorial
- fixed thread pool java
- shutdown executorservice
- print thread name
- run tasks parallel
language: hi
og_description: जावा मल्टीथ्रेडिंग ट्यूटोरियल जो आपको समानांतर कार्य चलाने, जावा में
  एक फिक्स्ड थ्रेड पूल बनाने, थ्रेड का नाम प्रिंट करने और एक्सीक्यूटरसर्विस को साफ़-सुथरे
  ढंग से बंद करने के माध्यम से मार्गदर्शन करता है।
og_title: जावा मल्टीथ्रेडिंग ट्यूटोरियल – फिक्स्ड थ्रेड पूल के साथ समानांतर निष्पादन
tags:
- Java
- Concurrency
- ExecutorService
title: 'जावा मल्टीथ्रेडिंग ट्यूटोरियल: फिक्स्ड थ्रेड पूल के साथ टास्क को समानांतर
  चलाएँ'
url: /hi/java/advanced-usage/java-multithreading-tutorial-run-tasks-parallel-with-fixed-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java multithreading tutorial – Parallel Execution Made Simple

क्या आपने कभी सोचा है कि **run tasks parallel** को Java में कैसे किया जाए बिना लो‑लेवल थ्रेड मैनेजमेंट में डूबे? इस **java multithreading tutorial** में हम आपको ठीक वही दिखाएंगे: **fixed thread pool java** का उपयोग, प्रत्येक थ्रेड का नाम प्रिंट करना, और काम खत्म होने पर **shutdown executorservice** को साफ़‑सुथरा तरीके से बंद करना।  

यदि आपने कभी ऐसा लूप लिखा है जो नेटवर्क I/O पर ब्लॉक करता है या आपको एक साथ कई वेब पेज स्क्रैप करने हैं, तो नीचे दिया गया पैटर्न आपका समय और सिरदर्द दोनों बचाएगा।  

हम वह सब कवर करेंगे जिसकी आपको ज़रूरत है—कोई बाहरी दस्तावेज़ नहीं, सिर्फ शुद्ध Java कोड जिसे आप कॉपी‑पेस्ट, रन और परिणाम देख सकते हैं। अंत तक आप समझ जाएंगे कि क्यों एक **fixed thread pool** अक्सर सीमित समानांतरता के लिए सबसे अच्छा विकल्प होता है, इसे सुरक्षित रूप से कैसे समाप्त करें, और थ्रेड का नाम प्रिंट करके अपने लॉग को कैसे अधिक पठनीय बनाएं।  

> **Prerequisites**: Java 8+ ( `java.util.concurrent` पैकेज कई सालों से स्थिर है), एक IDE या साधारण `javac`/`java` कमांड लाइन, और OOP की बुनियादी समझ। Aspose HTML for Java jar के अलावा कोई अतिरिक्त लाइब्रेरी आवश्यक नहीं है।

---

![java multithreading tutorial diagram showing a thread pool feeding tasks](https://example.com/images/java-multithreading-tutorial.png "java multithreading tutorial diagram")

## java multithreading tutorial – Set Up a Fixed Thread Pool

एक **fixed thread pool** एक साथ चलने वाले थ्रेड्स की संख्या को सीमित करता है, जिससे आपका एप्लिकेशन बहुत अधिक OS थ्रेड्स नहीं बनाता और संसाधनों की समाप्ति नहीं होती। यहाँ हम चार वर्कर्स के साथ एक पूल बनाते हैं:

```java
import java.util.concurrent.*;

public class ParallelProcessingTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Why four?* यह उन URLs की संख्या से मेल खाता है जिन्हें हम फ़ेच करेंगे, लेकिन आप इस संख्या को CPU कोर, I/O तीव्रता, या मेमोरी सीमाओं के आधार पर समायोजित कर सकते हैं। `Executors` फ़ैक्टरी आपको लो‑लेवल `Thread` कंस्ट्रक्टर से बचाती है और आपको एक साफ़ `ExecutorService` रेफ़रेंस देती है जिसे आप बाद में **shutdown executorservice** करेंगे।

## Prepare URLs and Define Parallel Tasks

अब हम उन पेजों की सूची बनाते हैं जिन्हें हम प्रोसेस करना चाहते हैं। वास्तविक स्क्रैपर में आप इन्हें फ़ाइल या डेटाबेस से पढ़ेंगे, लेकिन एक स्थिर एरे उदाहरण को स्वयं‑समाहित रखता है:

```java
        // Step 2: List the web pages to process
        String[] pageUrls = {
            "https://example.com/a.html",
            "https://example.com/b.html",
            "https://example.com/c.html",
            "https://example.com/d.html"
        };
```

अब आता है **run tasks parallel** भाग। प्रत्येक URL के लिए हम एक लैम्ब्डा सबमिट करते हैं जो डॉक्यूमेंट लोड करता है और उसका टाइटल प्रिंट करता है। ध्यान दें `Thread.currentThread().getName()` का उपयोग – यह हमारा **print thread name** ट्रिक है जो डिबगिंग को बहुत आसान बनाता है:

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

> **Pro tip**: `HTMLDocument` को `try‑with‑resources` ब्लॉक में लपेटने से यह सुनिश्चित होता है कि अंतर्निहित स्ट्रीम बंद हो जाए, भले ही पेज लोड न हो।

## Gracefully Shutdown the ExecutorService

काम खत्म होने के बाद थ्रेड पूल को जीवित छोड़ देना आपके JVM को लटकाए रख सकता है। सही तरीका है **shutdown executorservice** करना, फिर टर्मिनेशन की प्रतीक्षा करना:

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

*Why the timeout?* यह आपको एक रॉग टास्क से बचाता है जो कभी रिटर्न नहीं करता (जैसे, एक नेटवर्क कॉल जो हैंग हो जाता है)। यदि पूल एक मिनट में समाप्त नहीं होता तो हम `shutdownNow()` को कॉल करके बचे हुए थ्रेड्स को इंटरप्ट कर देते हैं।

### Expected Output

प्रोग्राम चलाने पर कुछ इस तरह का आउटपुट मिलेगा:

```
pool-1-thread-1 – Example A
pool-1-thread-3 – Example C
pool-1-thread-2 – Example B
pool-1-thread-4 – Example D
```

सटीक क्रम बदल सकता है—क्योंकि टास्क वास्तव में समानांतर हैं। जो स्थिर रहता है वह है **print thread name** प्रीफ़िक्स, जो आपको बताता है कि कौन सा वर्कर प्रत्येक URL को संभाल रहा है।

---

## Common Variations & Edge Cases

| Situation | What to Change | Reason |
|-----------|----------------|--------|
| **More URLs than threads** | Keep the same pool size; extra tasks will queue automatically. | The fixed pool handles back‑pressure for you. |
| **CPU‑bound work** | Set the pool size to `Runtime.getRuntime().availableProcessors()` instead of a hard‑coded 4. | Maximizes CPU utilization without oversubscribing. |
| **Need to cancel a specific task** | Keep a `Future<?>` reference from `executor.submit()` and call `future.cancel(true)`. | Gives fine‑grained control over individual jobs. |
| **Processing large files** | Increase the pool size modestly *or* switch to `newCachedThreadPool()` if you expect bursts. | Cached pools create threads on demand, but beware of unbounded growth. |

---

## Conclusion

आपके पास अब एक ठोस **java multithreading tutorial** है जो दिखाता है कैसे **run tasks parallel** को **fixed thread pool java** के साथ किया जाए, स्पष्ट लॉगिंग के लिए **print thread name** का उपयोग करें, और **shutdown executorservice** को साफ़‑सुथरा तरीके से बंद करें। पूरा, चलाने योग्य कोड एक ही क्लास में है, इसलिए आप इसे किसी भी प्रोजेक्ट में डाल सकते हैं और तुरंत अपने I/O‑bound काम को स्केल करना शुरू कर सकते हैं।

अगला कदम? `HTMLDocument` को अपने स्वयं के HTTP क्लाइंट से बदलें, विभिन्न पूल साइज के साथ प्रयोग करें, या `CompletionService` को इंटीग्रेट करके परिणामों को उनके समाप्त होने के क्रम में एकत्र करें। यदि आपको बैक‑प्रेशर हैंडलिंग की ज़रूरत है तो `java.util.concurrent.Flow` को भी देख सकते हैं।

Happy coding, and remember: with the right thread‑pool strategy, concurrency becomes a *piece of cake*, not a source of bugs. If you have questions, feel free to drop a comment—I'm always up for a chat about Java concurrency!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
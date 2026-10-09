---
category: general
date: 2026-02-10
description: जावा फिक्स्ड थ्रेड पूल का उपयोग करके HTML फ़ाइलों में छवियों की गिनती
  करना, जावा में कार्यों को समानांतर चलाना, और एक्ज़ीक्यूटर सर्विस को सही तरीके से
  बंद करना सीखें।
draft: false
keywords:
- java fixed thread pool
- how to count images
- shutdown executor service
- java parallel file processing
- run tasks concurrently java
language: hi
og_description: जावा फिक्स्ड थ्रेड पूल के उपयोग में निपुण बनें, छवियों की गिनती करें,
  फ़ाइलों को समानांतर रूप से प्रोसेस करें, और एक्ज़ीक्यूटर सर्विस को सुरक्षित रूप
  से बंद करें।
og_title: 'जावा फिक्स्ड थ्रेड पूल: समानांतर फ़ाइलों में छवियों की गिनती'
tags:
- Java
- Concurrency
- Aspose.HTML
title: 'जावा फिक्स्ड थ्रेड पूल: समानांतर फ़ाइलों में छवियों की गिनती'
url: /hi/java/data-handling-stream-management/java-fixed-thread-pool-count-images-in-parallel-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java fixed thread pool – समानांतर इमेज काउंटिंग ट्यूटोरियल

क्या आपने कभी सोचा है कि **java fixed thread pool** का उपयोग करके दर्जनों HTML फ़ाइलों को कैसे प्रोसेस करें और जल्दी से इमेज काउंट प्राप्त करें? शायद आप फ़ाइलों की एक डायरेक्टरी को देखते‑देखते थक गए हों और सोच रहे हों “मुझे हर फ़ाइल में कितने `<img>` टैग हैं पता करना है”, और फिर महसूस किया हो कि सिंगल‑थ्रेडेड लूप में बहुत समय लगेगा।  

अच्छी खबर यह है कि आपको कोई कस्टम थ्रेड मैनेजर लिखने या लो‑लेवल `Thread` ऑब्जेक्ट्स से जूझने की ज़रूरत नहीं है। इस गाइड में हम आपको दिखाएंगे कि **इमेज कैसे काउंट करें** *java fixed thread pool* का उपयोग करके, टास्क्स को समानांतर रूप से चलाएँ और काम खत्म होने पर **shutdown executor service** को ग्रेसफ़ुली कैसे बंद करें।  

हम पूल सेटअप करने से लेकर फ़ाइल लिस्ट तैयार करने, समानांतर टास्क सबमिट करने, एज केस हैंडल करने, और आउटपुट वेरिफ़ाई करने तक सब कुछ कवर करेंगे। अंत तक आपके पास एक तैयार‑टू‑रन प्रोग्राम होगा जो **java parallel file processing** को साफ़, मेंटेनेबल तरीके से दर्शाता है।  

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

- Java 17 या नया (कोड में संक्षिप्तता के लिए `var` कीवर्ड इस्तेमाल किया गया है, लेकिन जरूरत पड़े तो आप डाउनग्रेड भी कर सकते हैं)।
- Aspose.HTML for Java आपके क्लासपाथ में – इसे आप Maven Central से प्राप्त कर सकते हैं:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

- कुछ HTML फ़ाइलें जिन्हें आप एनालाइज़ करना चाहते हैं (ट्यूटोरियल मानता है कि वे `YOUR_DIRECTORY/` में हैं)।
- एक IDE या बिल्ड टूल जिससे आप सहज हों – IntelliJ IDEA, VS Code, या साधारण `javac` भी ठीक रहेगा।

बस इतना ही। कोई अतिरिक्त सर्वर, कोई Docker नहीं, सिर्फ़ साधारण Java और एक छोटा थर्ड‑पार्टी लाइब्रेरी।

## Step 1: Create a java fixed thread pool

एक *java fixed thread pool* आपको वर्कर थ्रेड्स का एक सीमित सेट देता है जो प्रत्येक सबमिट किए गए टास्क के लिए खुद को री‑यूज़ करता है। यह लगातार नए थ्रेड्स बनाने के ओवरहेड को रोकता है और कंकरेन्सी लेवल को सीमित रखता है, जो डिस्क से फ़ाइलें पढ़ते समय बहुत महत्वपूर्ण है।

```java
import java.util.concurrent.*;

public class ParallelImageCounter {
    // A pool of 4 threads – adjust based on your CPU cores and I/O profile
    private static final ExecutorService executor = Executors.newFixedThreadPool(4);
}
```

**क्यों 4?** अगर आपके पास क्वाड‑कोर लैपटॉप है, तो चार थ्रेड्स प्रत्येक कोर को व्यस्त रखेंगे बिना ओवर‑सब्सक्राइब किए। सर्वर पर अधिक कोर होने पर आप संख्या बढ़ा सकते हैं, लेकिन याद रखें कि प्रत्येक थ्रेड एक फ़ाइल हैंडल खोलता है, इसलिए बहुत अधिक थ्रेड्स OS लिमिट्स को ख़त्म कर सकते हैं।

## Step 2: List the HTML files you want to analyse

अगला चरण **java parallel file processing** का है – बस फ़ाइल पाथ्स की एक एरे (या `List`) बनाना। वास्तविक प्रोजेक्ट में आप डायरेक्टरी को रीकर्सिवली वॉक कर सकते हैं, एक्सटेंशन के आधार पर फ़िल्टर कर सकते हैं, या डेटाबेस से पाथ्स पढ़ सकते हैं। यहाँ सबसे सीधा तरीका दिया गया है:

```java
String[] htmlFiles = {
    "YOUR_DIRECTORY/a.html",
    "YOUR_DIRECTORY/b.html",
    "YOUR_DIRECTORY/c.html",
    "YOUR_DIRECTORY/d.html"
};
```

अगर आपको डायनामिक सेट को हैंडल करना है, तो स्थिर एरे को इस तरह बदलें:

```java
Path dir = Paths.get("YOUR_DIRECTORY");
String[] htmlFiles = Files.list(dir)
                         .filter(p -> p.toString().endsWith(".html"))
                         .map(Path::toString)
                         .toArray(String[]::new);
```

यह स्निपेट किसी भी संख्या की फ़ाइलों के लिए **java parallel file processing** को दिखाता है बिना बाकी कोड को बदले।

## Step 3: Submit tasks to **run tasks concurrently java**

अब ट्यूटोरियल का मुख्य भाग आता है – हम **run tasks concurrently java** करेंगे प्रत्येक फ़ाइल के लिए एक लैम्ब्डा सबमिट करके। प्रत्येक टास्क Aspose.HTML से HTML डॉक्यूमेंट लोड करता है, सभी `<img>` एलिमेंट्स को क्वेरी करता है, और काउंट प्रिंट करता है।

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

**लैम्ब्डा क्यों इस्तेमाल करें?** यह कोड को संक्षिप्त रखता है और अलग `Runnable` क्लास बनाने की ज़रूरत नहीं पड़ती। लैम्ब्डा `filePath` को ऑटोमैटिकली कैप्चर करता है, इसलिए प्रत्येक टास्क अपना फ़ाइल प्रोसेस करता है।

### How to **count images** efficiently

Aspose.HTML फ़ाइल को एक बार पार्स करता है, DOM बनाता है, और फिर `querySelectorAll("img")` O(n) में चलता है जहाँ *n* नोड्स की संख्या है। अधिकांश HTML पेजों के लिए यह नगण्य है। अगर आपको बहुत बड़े (गिगाबाइट‑साइज़) फ़ाइलों के लिए तेज़, स्ट्रीम‑ओनली अप्रोच चाहिए (जैसे SAX पार्सर), तो आप वह विकल्प चुन सकते हैं, लेकिन इससे हम जिस सरलता को चाहते हैं वह कम हो जाएगी।

## Step 4: Properly **shutdown executor service**

पूल को कभी न भूलें बंद करना, नहीं तो आपका JVM हमेशा चलता रहेगा। नीचे दिया गया पैटर्न **shutdown executor service** को अनुशंसित तरीके से करता है जबकि सभी टास्क्स के खत्म होने का इंतज़ार करता है:

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

**अगर कोई टास्क हैंग हो जाए तो?** `shutdownNow()` कॉल चल रहे थ्रेड्स को इंटरप्ट करने की कोशिश करता है। अगर आपका इमेज‑काउंटिंग लॉजिक इंटरप्शन को सम्मानित करता है (Aspose.HTML I/O पर ब्लॉक नहीं करता), तो पूल साफ़‑सुथरे ढंग से टर्मिनेट हो जाएगा। यह पैटर्न किसी भी **java fixed thread pool** उपयोग के लिए गोल्ड स्टैंडर्ड है।

## Step 5: Verify the output

प्रोग्राम को अपने IDE से या कमांड लाइन से चलाएँ:

```bash
javac -cp "path/to/aspose-html.jar" ParallelImageCounter.java
java -cp ".:path/to/aspose-html.jar" ParallelImageCounter
```

आमतौर पर आउटपुट इस प्रकार दिखता है:

```
YOUR_DIRECTORY/a.html contains 5 images.
YOUR_DIRECTORY/b.html contains 0 images.
YOUR_DIRECTORY/c.html contains 12 images.
YOUR_DIRECTORY/d.html contains 3 images.
```

अगर आप काउंट्स किसी भी क्रम में प्रिंट होते देखते हैं, तो यह सामान्य है – थ्रेड्स अलग‑अलग समय पर फिनिश होते हैं। महत्वपूर्ण बात यह है कि हर फ़ाइल का काउंट दिख रहा है और शटडाउन सीक्वेंस के बाद प्रोग्राम साफ़‑सुथरा एक्सिट हो रहा है।

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

स्निपेट चलाने पर प्रत्येक फ़ाइल पाथ के बाद उसके `<img>` टैग्स की संख्या प्रिंट होगी, फिर JVM एक्सिट हो जाएगा। कोई लिंगरिंग थ्रेड नहीं, कोई मेमोरी लीक्स नहीं।

## Common Pitfalls & Pro Tips

- **Pitfall:** `newCachedThreadPool()` का उपयोग करना बजाय *fixed* पूल के। यह अनबाउंडेड थ्रेड्स बनाता है, जो बड़ी बैच में फ़ाइल डिस्क्रिप्टर खत्म कर सकता है। `newFixedThreadPool` ही इस्तेमाल करें।
- **Pro tip:** अगर आपकी HTML फ़ाइलें बड़ी हैं, तो हीप साइज बढ़ाएँ (`-Xmx2g`) या स्ट्रीमिंग पार्सर पर स्विच करें। अधिकांश मार्केटिंग पेजों के लिए डिफ़ॉल्ट हीप पर्याप्त है।
- **Pitfall:** `shutdown()` को कॉल करना भूल जाना – परिणाम प्रिंट होने के बाद आपका ऐप हैंग कर जाएगा। ऊपर दिया गया `shutdownAndAwaitTermination` मेथड इसे मजबूती से हैंडल करता है।
- **Pro tip:** अगर आपको परफ़ॉर्मेंस मेट्रिक्स चाहिए तो प्रत्येक टास्क के शुरू और अंत का टाइम लॉग करें। `HTMLDocument` कंस्ट्रक्शन से पहले और बाद में `System.nanoTime()` इस्तेमाल करने से आपको पार्सिंग टाइम मिल जाएगा।
- **Pitfall:** थ्रेड काउंट को हार्ड‑कोड करना। डिफ़ॉल्ट वैल्यू के लिए `Runtime.getRuntime().availableProcessors()` का उपयोग करें:

```java
int cores = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(cores);
```

## Related Topics You Might Explore Next

- **run tasks concurrently java** के साथ `CompletableFuture` का उपयोग करके अधिक एक्सप्रेसिव पाइपलाइन बनाएँ।
- इमेज काउंट्स को डेटाबेस में स्टोर करके एनालिटिक्स डैशबोर्ड बनाना।
- `java.nio.file.Files.walk` API को स्ट्रीम्स के साथ मिलाकर **java parallel file processing** करना।
- कस्टम `ThreadFactory` इम्प्लीमेंट करके थ्रेड्स को अर्थपूर्ण नाम देना (डिबगिंग में मददगार)।

## Conclusion

हमने अभी एक पूर्ण, सेल्फ‑कंटेन्ड उदाहरण के माध्यम से दिखाया कि कैसे **java fixed thread pool** का उपयोग करके कई HTML फ़ाइलों में **how to count images** किया जा सकता है, साथ ही सही तरीके से **shutdown executor service** भी किया गया। यह पैटर्न आसानी से स्केल करता है—फ़ाइल एरे को डायनामिक लिस्ट से बदलें, पूल साइज बढ़ाएँ, और आपके पास किसी भी **java parallel file processing** वर्कलोड के लिए एक मजबूत समाधान है।  

इसे चलाएँ, थ्रेड काउंट को ट्यून करें, और शायद परिणामों को CSV में एक्सपोर्ट करें। जब आप एक ठोस कन्करेंसी फाउंडेशन को Aspose.HTML जैसी लाइब्रेरी के साथ जोड़ते हैं, तो संभावनाएँ अनंत होती हैं। Happy coding!  

![java fixed thread pool diagram](image.png){alt="java fixed thread pool diagram"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
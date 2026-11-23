---
category: general
date: 2026-05-28
description: जावा में फिक्स्ड थ्रेड पूल के साथ एक्ज़ीक्यूटर का उपयोग कैसे करें, HTML
  से टेक्स्ट निकालें और प्रोसेसिंग को तेज़ करें – एक पूर्ण जावा थ्रेड पूल उदाहरण।
draft: false
keywords:
- how to use executor
- fixed thread pool java
- extract text from html
- java thread pool example
- create fixed thread pool
language: hi
og_description: जावा में फिक्स्ड थ्रेड पूल के साथ एक्सीक्यूटर का उपयोग कैसे करें।
  एक पूर्ण जावा थ्रेड पूल उदाहरण सीखें जो HTML फ़ाइलों से टेक्स्ट को कुशलतापूर्वक
  निकालता है।
og_title: जावा में एक्सीक्यूटर का उपयोग कैसे करें – फिक्स्ड थ्रेड पूल गाइड
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
title: जावा में एक्सीक्यूटर का उपयोग कैसे करें – फिक्स्ड थ्रेड पूल गाइड
url: /hi/java/advanced-usage/how-to-use-executor-in-java-fixed-thread-pool-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा में Executor का उपयोग कैसे करें – फिक्स्ड थ्रेड पूल गाइड

क्या आपने कभी सोचा है कि **how to use executor** को कई कार्य एक साथ चलाने के लिए बिना मेमोरी को भरते हुए कैसे उपयोग किया जाए? आप अकेले नहीं हैं। कई वास्तविक‑दुनिया के ऐप्स में आपको HTML फ़ाइलों के एक फ़ोल्डर को क्रॉल करना होगा, बॉडी टेक्स्ट निकालना होगा, और इसे तेज़ी से करना होगा—बिल्कुल वही स्थिति जिसे यह ट्यूटोरियल हल करता है।

हम एक **fixed thread pool java** इम्प्लीमेंटेशन के माध्यम से चलेंगे जो HTML से टेक्स्ट निकालता है, प्रत्येक फ़ाइल की कैरेक्टर काउंट प्रिंट करता है, और साफ़ तौर पर शटडाउन करता है। अंत तक आपके पास एक स्व-निहित **java thread pool example** होगा जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं, साथ ही पूल आकार को कस्टमाइज़ करने और एज केस को हैंडल करने के कुछ टिप्स भी।

> **आपको क्या चाहिए**  
> * Java 17 (या कोई भी नवीनतम JDK)  
> * एक छोटी HTML‑पार्सिंग लाइब्रेरी – हम *jsoup* का उपयोग करेंगे क्योंकि यह battle‑tested और zero‑config है।  
> * आपकी पसंद की डायरेक्टरी में कुछ नमूना *.html* फ़ाइलें।  

---

## Fixed Thread Pool के साथ Executor का उपयोग कैसे करें

किसी भी concurrency‑heavy जावा प्रोग्राम का दिल `ExecutorService` है। एक **fixed thread pool** बनाकर हम JVM को ठीक N वर्कर थ्रेड्स जीवित रखने के लिए कहते हैं, जिससे थ्रेड‑क्रिएशन ओवरहेड रोका जाता है और संसाधन उपयोग सीमित रहता है।

```java
// Step 1: Build a fixed‑size thread pool (4 workers in this case)
ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Why this matters:*  
यदि आप प्रत्येक HTML फ़ाइल के लिए एक नया `Thread` लॉन्च करते हैं, तो OS को एक मध्यम लैपटॉप पर दर्जनों थ्रेड्स को शेड्यूल करना पड़ेगा, जिससे context‑switch थ्रैशिंग होगी। एक फिक्स्ड पूल वही चार थ्रेड्स को पुन: उपयोग करता है, जिससे आपको पूर्वानुमेय CPU उपयोग मिलता है।

---

## HTML फ़ाइलों को प्रोसेस करने के लिए परिभाषित करें – Fixed Thread Pool Java

अब हम उन फ़ाइलों की सूची बनाते हैं जिन्हें हम पूल में फीड करना चाहते हैं। वास्तविक ऐप में आप संभवतः एक डायरेक्टरी ट्री वॉक करेंगे; यहाँ हम इसे सरल रखते हैं।

```java
// Step 2: List the HTML documents you want to parse
List<String> htmlFilePaths = List.of(
        "YOUR_DIRECTORY/a.html",
        "YOUR_DIRECTORY/b.html",
        "YOUR_DIRECTORY/c.html",
        "YOUR_DIRECTORY/d.html"
);
```

*Tip:* `List.of` एक immutable सूची लौटाता है, जिसे अतिरिक्त सिंक्रोनाइज़ेशन के बिना थ्रेड्स के बीच साझा करना सुरक्षित है।

---

## प्रत्येक HTML फ़ाइल के लिए एक अलग टास्क सबमिट करें

अब हम प्रत्येक पाथ को executor को देते हैं। वह लैम्ब्डा जिसे हम सबमिट करेंगे **in parallel** चार वर्कर थ्रेड्स में से किसी एक पर चलेगा।

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

**Why we wrap the logic in a method** (`extractBodyText`) अगले सेक्शन में स्पष्ट हो जाएगा—यह लैम्ब्डा को साफ़ रखता है और हमें एक्सट्रैक्शन कोड को कहीं और पुन: उपयोग करने देता है।

---

## HTML से टेक्स्ट निकालें – कोर लॉजिक

यहाँ पुन: उपयोगी हेल्पर है जो वास्तव में Jsoup का उपयोग करके **extracts text from html** करता है। यह फ़ाइल खोलता है, DOM को पार्स करता है, और साधारण बॉडी टेक्स्ट लौटाता है।

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

*Why Jsoup?* यह हल्का है, खराब मार्कअप को सहजता से संभालता है, और पूर्ण ब्राउज़र इंजन की आवश्यकता नहीं होती। यह मेथड `IOException` थ्रो करता है ताकि कॉलर तय कर सके कि कैसे लॉग या रिकवर किया जाए—एक थ्रेड‑पूल परिदृश्य के लिए परफेक्ट जहाँ आप नहीं चाहते कि एक बुरी फ़ाइल पूरे executor को समाप्त कर दे।

---

## Executor को ग्रेसफुली शटडाउन करें – Create Fixed Thread Pool

सभी जॉब सबमिट करने के बाद, हमें पूल को नई कार्य स्वीकार न करने और पहले से कतार में मौजूद कार्यों को समाप्त करने के लिए कहना चाहिए।

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

*Explanation:* `shutdown()` नई सबमिशन को रोकता है, जबकि `awaitTermination` तब तक ब्लॉक करता है जब तक सभी पार्सिंग जॉब समाप्त नहीं हो जाते (या टाइमआउट समाप्त हो जाता है)। यदि कुछ हँग हो जाता है, तो `shutdownNow()` चल रहे टास्क को कैंसल करने की कोशिश करता है। यह पैटर्न **create fixed thread pool** को सुरक्षित रूप से करने का अनुशंसित तरीका है।

---

## पूरा, रन करने योग्य उदाहरण

सब कुछ एक साथ जोड़ते हुए, यहाँ एक सिंगल फ़ाइल है जिसे आप कंपाइल और रन कर सकते हैं। इसमें आवश्यक इम्पोर्ट्स, `main` मेथड, और ऊपर वर्णित हेल्पर शामिल है।

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

**Expected output** (मान लेते हैं कि प्रत्येक फ़ाइल में लगभग 1 200 कैरेक्टर बॉडी टेक्स्ट है):

```
YOUR_DIRECTORY/a.html → 1234 chars
YOUR_DIRECTORY/b.html → 1198 chars
YOUR_DIRECTORY/c.html → 1305 chars
YOUR_DIRECTORY/d.html → 1120 chars
```

यदि कोई फ़ाइल गायब या खराब है, तो आपको `stderr` पर एक स्टैक ट्रेस प्रिंट होते हुए दिखेगा, लेकिन अन्य टास्क बिना प्रभावित हुए जारी रहेंगे—बिल्कुल वही जो एक well‑behaved **java thread pool example** को करना चाहिए।

---

## सामान्य प्रश्न और एज केस

| Question | Answer |
|----------|--------|
| *यदि मेरे पास चार से अधिक फ़ाइलें हों तो क्या होगा?* | पूल अतिरिक्त टास्क को कतार में रखेगा और जैसे ही कोई थ्रेड फ्री होगा, उन्हें चलाएगा। अतिरिक्त कोड की आवश्यकता नहीं। |
| *क्या मुझे `newCachedThreadPool` का उपयोग करना चाहिए?* | `newCachedThreadPool` मांग पर थ्रेड बनाता है और अनिश्चित रूप से बढ़ सकता है, जो I/O‑heavy जॉब्स के लिए जोखिमभरा है। एक **fixed thread pool** आपको पूर्वानुमेय मेमोरी और CPU उपयोग देता है। |
| *CPU कोर के आधार पर पूल आकार कैसे बदलें?* | `int cores = Runtime.getRuntime().availableProcessors(); ExecutorService exec = Executors.newFixedThreadPool(cores);` एक सामान्य पैटर्न है। |
| *यदि एक फ़ाइल के लिए पार्सिंग फेल हो जाए तो क्या होगा?* | `catch (IOException e)` लैम्ब्डा के अंदर फेल्योर को अलग करता है, उसे लॉग करता है, और पूल के बाकी हिस्से को काम करते रहने देता है। |
| *क्या मैं निकाले गए टेक्स्ट को कॉलर को रिटर्न कर सकता हूँ?* | हां—`submit(Runnable)` की बजाय `Future<String>` का उपयोग करें। कोड इस प्रकार दिखेगा `Future<String> f = executor.submit(() -> extractBodyText(path));` और बाद में `String result = f.get();`। |

---

## निष्कर्ष

हमने **how to use executor** को कवर किया है ताकि **fixed thread pool java** को स्पिन अप किया जा सके जो HTML फ़ाइलों के संग्रह को समानांतर में प्रोसेस करता है, उनका बॉडी टेक्स्ट निकालता है, और कैरेक्टर काउंट रिपोर्ट करता है। पूरा **java thread pool example** उचित रिसोर्स मैनेजमेंट, एरर हैंडलिंग, और एक पुन: उपयोगी एक्सट्रैक्शन मेथड दर्शाता है।

अगले कदम? `extractBodyText` इम्प्लीमेंटेशन को अधिक परिष्कृत स्क्रैपर से बदलने की कोशिश करें, बड़े पूल आकार के साथ प्रयोग करें, या परिणामों को डेटाबेस में फीड करें। आप `CompletionService` को भी एक्सप्लोर कर सकते हैं ताकि परिणाम तुरंत उपलब्ध होते ही प्राप्त हो सकें, जो फ़ाइल आकार के बड़े अंतर होने पर उपयोगी है।

डायरेक्टरी पाथ को बदलने, अधिक फ़ाइलें जोड़ने, या इस स्निपेट को बड़े क्रॉलिंग फ्रेमवर्क में इंटीग्रेट करने में संकोच न करें। मूल पैटर्न—पूल बनाना, स्वतंत्र टास्क सबमिट करना, और ग्रेसफुली शटडाउन—वही रहता है, चाहे आपका वर्कलोड कितना भी जटिल हो।

हैप्पी कोडिंग, और आपके थ्रेड्स हमेशा जीवित रहें (जब तक आप उन्हें शटडाउन नहीं करते, बेशक)!

## संबंधित ट्यूटोरियल्स

- [Fixed thread pool java – ExecutorService के साथ समानांतर HTML क्लीनिंग](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [जावा में HTML क्वेरी कैसे करें – पूर्ण ट्यूटोरियल](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [जावा के लिए Aspose.HTML का उपयोग कैसे करें - HTML5 कैनवास रेंडरिंग में महारत](/html/english/java/html5-canvas-rendering/html5-canvas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
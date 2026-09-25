---
category: general
date: 2026-02-16
description: जानें कि CompletableFuture के साथ जावा में जावास्क्रिप्ट कैसे चलाएँ,
  JS को विलंबित करें, और असिंक्रोनस कोड का मूल्यांकन करें। असिंक्रोनस जावास्क्रिप्ट
  मूल्यांकन के लिए पूर्ण चरण‑दर‑चरण गाइड।
draft: false
keywords:
- how to run javascript
- how to use completablefuture
- how to delay js
- how to evaluate async
- evaluate javascript asynchronously
language: hi
og_description: इस संपूर्ण ट्यूटोरियल में जावा से जावास्क्रिप्ट चलाना, जावास्क्रिप्ट
  को विलंबित करना, और CompletableFuture के साथ असिंक्रोनस कोड का मूल्यांकन करना सीखें।
og_title: CompletableFuture का उपयोग करके जावास्क्रिप्ट को असिंक्रोनस रूप से कैसे
  चलाएँ
tags:
- javascript
- java
- asynchronous
- completablefuture
title: CompletableFuture का उपयोग करके जावास्क्रिप्ट को असिंक्रोनस रूप से कैसे चलाएँ
url: /hi/java/advanced-usage/how-to-run-javascript-asynchronously-using-completablefuture/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# CompletableFuture का उपयोग करके JavaScript को असिंक्रोनस रूप से चलाने का तरीका

क्या आपने कभी सोचा है **how to run JavaScript** को Java एप्लिकेशन के भीतर मुख्य थ्रेड को ब्लॉक किए बिना चलाया जाए? शायद आपको एक छोटा स्क्रिप्ट चलाना है जो डेटा फ़ेच करता है, लेकिन आप नहीं चाहते कि आपका UI फ्रीज़ हो जाए। अच्छी खबर यह है कि आधुनिक Java लाइब्रेरीज़ आपको JavaScript को **asynchronously** मूल्यांकित करने की सुविधा देती हैं, और आप ब्राउज़र की तरह देरी भी जोड़ सकते हैं। इस गाइड में हम एक पूर्ण, चलाने योग्य उदाहरण दिखाएंगे जो Aspose HTML के `ScriptEngine` को `CompletableFuture` के साथ उपयोग करता है ताकि **how to run javascript** किया जा सके और परिणाम Java में वापस मिल सके।

हम यह भी कवर करेंगे **how to use CompletableFuture**, **how to delay JS**, और **how to evaluate async** कोड को कैसे मूल्यांकित किया जाए ताकि आप किसी भी Java प्रोजेक्ट में **evaluate JavaScript asynchronously** कर सकें। अंत तक आपके पास एक ठोस टेम्प्लेट होगा जिसे आप कॉपी‑पेस्ट, संशोधित और बड़े सिस्टम में एम्बेड कर सकते हैं।

---

## आप क्या सीखेंगे

- एक Java `ScriptEngine` सेट अप करना जो आधुनिक ES2022 JavaScript को चलाता है।
- एक `async` फ़ंक्शन लिखना जिसमें देरी (`how to delay js`) शामिल हो।
- `evaluateAsync` को कॉल करना और एक `CompletableFuture` प्राप्त करना (`how to use completablefuture`)।
- JavaScript प्रॉमिस के रिजॉल्व होने पर परिणाम प्राप्त करना (`how to evaluate async`)।
- त्रुटि संभालना, थ्रेड प्रबंधन, और पैटर्न को विस्तारित करने के टिप्स।

Aspose HTML for Java JAR के अलावा कोई बाहरी बिल्ड टूल आवश्यक नहीं है, जिसे आप अपने क्लासपाथ में डाल सकते हैं। चलिए शुरू करते हैं।

---

## चरण 1: How to Run JavaScript – स्क्रिप्टिंग इंजन को इनिशियलाइज़ करें

सबसे पहले। Aspose HTML लाइब्रेरी एक `ScriptEngine` क्लास प्रदान करती है जो JavaScript कोड को निष्पादित कर सकती है। इसे अपने JVM के भीतर चलने वाले एक छोटे Chromium इंजन के रूप में सोचें।

```java
import com.aspose.html.scripting.*;
import java.util.concurrent.CompletableFuture;

public class JsAsyncDemo {
    public static void main(String[] args) throws Exception {

        // Create a scripting engine that can run JavaScript
        ScriptEngine scriptEngine = new ScriptEngine();
```

> **Why this matters:** `ScriptEngine` को इंस्टैंशिएट करके हमें एक सैंडबॉक्स्ड वातावरण मिलता है जहाँ आधुनिक JavaScript (जिसमें `async/await` भी शामिल है) बॉक्स से बाहर काम करता है। बाहरी Node प्रोसेस को स्पिन‑अप करने की जरूरत नहीं।

---

## चरण 2: How to Delay JS – प्रॉमिस‑आधारित टाइमर के साथ एक Async फ़ंक्शन लिखें

JavaScript का `setTimeout` निष्पादन को रोकने का क्लासिक तरीका है। आधुनिक कोड में हम इसे `Promise` में रैप करते हैं ताकि हम `await` कर सकें। यही हम स्क्रिप्ट स्ट्रिंग में करेंगे।

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

> **How to delay js:** `delay` हेल्पर एक प्रॉमिस बनाता है जो `ms` मिलीसेकंड के बाद सॉल्व हो जाता है। इसे `await` करके, फ़ंक्शन Java थ्रेड को ब्लॉक किए बिना रुकता है।

---

## चरण 3: How to Evaluate Async – स्क्रिप्ट चलाएँ और एक CompletableFuture प्राप्त करें

सिंक्रोनस `evaluate` मेथड की बजाय, हम `evaluateAsync` को कॉल करते हैं। यह तुरंत एक `CompletableFuture<Object>` लौटाता है जो JavaScript प्रॉमिस के रिजॉल्व होने पर पूरा हो जाएगा।

```java
        // Evaluate the script asynchronously – a CompletableFuture is returned
        CompletableFuture<Object> resultFuture = scriptEngine.evaluateAsync(asyncScript);
```

> **How to evaluate async:** `evaluateAsync` JavaScript इवेंट लूप को Java के `CompletableFuture` के साथ जोड़ता है। यह **evaluate javascript asynchronously** का मुख्य हिस्सा है।

---

## चरण 4: How to Use CompletableFuture – कॉलबैक जोड़ें और डेमो के लिए ब्लॉक करें

अब हम `thenAccept` के साथ एक कॉलबैक जोड़ते हैं ताकि परिणाम प्रिंट हो, और डेमो समाप्त होने तक मुख्य थ्रेड को थोड़ा ब्लॉक करते हैं।

```java
        // When the promise resolves, print the JavaScript result
        resultFuture.thenAccept(result ->
                System.out.println("JS result: " + result));

        // Block the main thread long enough for the demo to finish
        resultFuture.get(); // throws checked exceptions, handled by main's throws clause
    }
}
```

> **Why we call `get()`:** वास्तविक एप्लिकेशन में आप संभवतः कहीं और प्रोसेसिंग जारी रखेंगे। यहाँ हम उदाहरण को स्व-निहित रखने के लिए ब्लॉक करते हैं।

---

## विज़ुअल ओवरव्यू

![Diagram showing how to run JavaScript asynchronously with CompletableFuture](https://example.com/diagram.png "How to Run JavaScript – Async Flow")

*Alt text:* **Diagram showing how to run JavaScript asynchronously with CompletableFuture** – छवि Java से स्क्रिप्ट इंजन, असिंक्रोनस देरी, और CompletableFuture पूर्णता तक के प्रवाह को दर्शाती है।

---

## सामान्य त्रुटियाँ एवं सर्वोत्तम प्रथाएँ (How to Evaluate Async Safely)

| Pitfall | What Happens | Fix |
|---------|--------------|-----|
| प्रॉमिस को रिटर्न करना भूल जाना | `evaluateAsync` तुरंत `undefined` के साथ रिजॉल्व हो जाता है | सुनिश्चित करें कि स्क्रिप्ट की अंतिम पंक्ति प्रॉमिस है (`fetchMessage();`) |
| JS में ब्लॉकिंग `Thread.sleep` का उपयोग | इंजन के इवेंट लूप को ब्लॉक करता है, असिंक्रोनस को नष्ट करता है | `delay` प्रॉमिस पैटर्न का उपयोग करें (जैसा दिखाया गया) |
| एक्सेप्शन को अनदेखा करना | Future एक्सेप्शनली पूरा होता है, लेकिन आप इसे नहीं देखते | `.exceptionally(e -> { e.printStackTrace(); return null; })` जोड़ें |
| इंजन को शटडाउन न करना | लंबे‑चलने वाले ऐप्स में रिसोर्स लीक्स | समाप्त होने पर `scriptEngine.dispose()` कॉल करें |

---

## पैटर्न का विस्तार (How to Use CompletableFuture in Real Projects)

आप कई असिंक्रोनस JavaScript कॉल्स को चेन कर सकते हैं, उन्हें अन्य फ्यूचर्स के साथ मिलाकर उपयोग कर सकते हैं, या कस्टम `Executor` पर चला सकते हैं। यहाँ एक त्वरित स्केच है:

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

> **How to use CompletableFuture:** एक `Executor` पास करके आप थ्रेड पूल को नियंत्रित करते हैं, UI को रिस्पॉन्सिव रखते हैं और थ्रेड‑स्टार्वेशन से बचते हैं।

---

## अपेक्षित आउटपुट

`JsAsyncDemo` क्लास चलाएँ और आपको यह दिखना चाहिए:

```
JS result: Hello from async JS!
```

500 ms की pause कंसोल में दिखाई नहीं देती, लेकिन आप टाइमस्टैम्प जोड़कर देरी की पुष्टि कर सकते हैं यदि चाहें।

---

## सारांश – CompletableFuture के साथ JavaScript चलाना

हमने **how to run javascript** को Java के भीतर शुरू किया, एक `async` फ़ंक्शन लिखा जो **how to delay js** करता है, इसे `evaluateAsync` (**how to evaluate async**) के साथ चलाया, और परिणाम को **how to use completablefuture** से कैप्चर किया। पूरा फ्लो **evaluate javascript asynchronously** को एक साफ़, पुन: उपयोग योग्य पैटर्न में दर्शाता है।

---

## आगे क्या?

- **HTTP क्लाइंट्स के साथ इंटीग्रेट करें:** असिंक्रोनस JS के भीतर REST एन्डपॉइंट से डेटा फ़ेच करें और उसे Java को रिटर्न करें।
- **एकाधिक स्क्रिप्ट्स का उपयोग करें:** जटिल पाइपलाइन के लिए कई `evaluateAsync` कॉल्स को चेन करें।
- **इंजिन बदलें:** वही पैटर्न Nashorn, GraalVM, या अन्य JavaScript रनटाइम्स के साथ काम करता है—सिर्फ `ScriptEngine` को बदलें।

बड़े डिले, एरर‑थ्रोइंग स्क्रिप्ट्स, या यहाँ तक कि WebAssembly मॉड्यूल्स के साथ प्रयोग करने में संकोच न करें। जब आप Java की concurrency primitives को आधुनिक JavaScript के साथ मिलाते हैं तो संभावनाएँ असीमित हैं।

---

### कोई प्रश्न?

यदि कुछ स्पष्ट नहीं है—शायद आप यह जानना चाहते हैं कि रिजेक्टेड प्रॉमिस को कैसे हैंडल करें या Java से स्क्रिप्ट में वेरिएबल्स कैसे पास करें—तो नीचे कमेंट करें। Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-04-03
description: Aspose.HTML Java में सैंडबॉक्स का उपयोग करके यूज़र एजेंट सेट करना, आकार
  निर्धारित करना और तुरंत व्यूपोर्ट आकार प्राप्त करना सीखें। पूर्ण कोड, व्याख्याएँ
  और टिप्स शामिल हैं।
draft: false
keywords:
- how to use sandbox
- set user agent
- get viewport size
- how to set size
- how to get viewport
language: hi
og_description: Aspose.HTML Java में सैंडबॉक्स का उपयोग करके यूज़र एजेंट सेट करना,
  आकार निर्धारित करना और तुरंत व्यूपोर्ट आकार प्राप्त करना सीखें। कोड और सर्वोत्तम
  प्रथाओं के साथ पूर्ण गाइड।
og_title: Sandbox का उपयोग कैसे करें – यूज़र एजेंट सेट करें और व्यूपोर्ट आकार प्राप्त
  करें
tags:
- AsposeHTML
- Java
- Sandbox
title: सैंडबॉक्स का उपयोग कैसे करें – यूज़र एजेंट सेट करें और व्यूपोर्ट आकार प्राप्त
  करें
url: /hi/java/configuring-environment/how-to-use-sandbox-set-user-agent-get-viewport-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use Sandbox – Set User Agent & Get Viewport Size

क्या आपने कभी सोचा है **sandbox का उपयोग कैसे करें** जब Aspose.HTML for Java के साथ HTML रेंडर किया जाता है? शायद आप एक विशिष्ट स्क्रीन आकार का सिमुलेशन करने या यूज़र‑एजेंट स्ट्रिंग को स्पूफ़ करने की कोशिश में फँसे हैं ताकि पेज मोबाइल ब्राउज़र से विज़िट किया गया जैसा व्यवहार करे।  

अच्छी खबर यह है कि sandbox API आपको ठीक वही करने देती है, और आप पेज लोड होने के बाद गणना किया गया viewport आकार भी प्राप्त कर सकते हैं। इस ट्यूटोरियल में हम sandbox बनाना, आकार सेट करना, कस्टम यूज़र एजेंट सेट करना, रिमोट पेज लोड करना, और अंत में viewport आयाम पढ़ना देखेंगे। अंत तक आप जानेंगे **आकार कैसे सेट करें**, **viewport कैसे प्राप्त करें**, और ये कदम विश्वसनीय हेडलेस रेंडरिंग के लिए क्यों महत्वपूर्ण हैं।

> **त्वरित लाभ:** आप कुछ ही सेकंड में एक runnable Java क्लास प्राप्त करेंगे जो `Viewport: 1280×800` जैसा कुछ प्रिंट करेगा।

---

## What You’ll Need

- **Aspose.HTML for Java** संस्करण 24.6 या नया (हमारा उपयोग किया गया API 24.5 में पेश किया गया था)।  
- एक Java 17+ डेवलपमेंट किट (कोई भी हालिया JDK चलेगा)।  
- एक IDE या साधारण टेक्स्ट एडिटर—कोई विशेष प्लगइन आवश्यक नहीं।  
- इंटरनेट एक्सेस यदि आप `https://example.com` जैसे बाहरी URL को लोड करना चाहते हैं।

बस इतना ही। Maven/Gradle की कोई जादूगरी अनिवार्य नहीं है; आप चाहें तो JAR फ़ाइलों को मैन्युअल रूप से क्लासपाथ में डाल सकते हैं।  

---

## How to Use Sandbox – Overview

sandbox रेंडरिंग इंजन को होस्ट OS से अलग करता है, जिससे आप एक वर्चुअल स्क्रीन (चौड़ाई, ऊँचाई, DPI) और एक कस्टम **user agent** स्ट्रिंग परिभाषित कर सकते हैं। इसे एक छोटा ब्राउज़र विंडो समझें जो पूरी तरह मेमोरी में रहता है। जब आप बाद में `HTMLDocument` से उसका डिफ़ॉल्ट व्यू पूछते हैं, तो इंजन sandbox सेटिंग्स के आधार पर गणना किया गया **viewport size** रिपोर्ट करता है।  

नीचे एक उच्च‑स्तरीय प्रवाह दिया गया है:

1. **Create** एक `DocumentSandbox` और चौड़ाई, ऊँचाई, DPI, तथा user‑agent को कॉन्फ़िगर करें।  
2. **Load** उस sandbox के अंदर एक `HTMLDocument`।  
3. **Query** दस्तावेज़ के डिफ़ॉल्ट व्यू से viewport आकार।  

आइए प्रत्येक चरण में गहराई से देखें।

---

## Step 1: Create a Sandbox and Set Size

सबसे पहले, हम एक sandbox बनाते हैं और उसे बताते हैं कि वर्चुअल स्क्रीन कितनी बड़ी होनी चाहिए। यही वह जगह है जहाँ आप **headless render के लिए आकार कैसे सेट करें** का उत्तर देते हैं।

```java
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.drawing.Size2D;

/* Step 1 – instantiate the sandbox */
DocumentSandbox sandbox = new DocumentSandbox();

/* Set the virtual screen width & height (in pixels) */
sandbox.setScreenWidth(1280);   // width in pixels
sandbox.setScreenHeight(800);   // height in pixels

/* DPI influences CSS pixel calculations – 96 is the CSS default */
sandbox.setDeviceDpi(96);

/* Optional: give the sandbox a friendly name for debugging */
sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");
```

> **Pro tip:** यदि आप एक रिस्पॉन्सिव लेआउट का परीक्षण कर रहे हैं, तो `360` जैसी संकरी चौड़ाई का उपयोग करके फोन का सिमुलेशन करें, या `1920` जैसी विस्तृत चौड़ाई का उपयोग करके डेस्कटॉप का सिमुलेशन करें। sandbox आपके द्वारा सेट किए गए DPI का सम्मान करता है, इसलिए उच्च‑घनत्व स्क्रीन (उदाहरण – 144 DPI) `device-pixel-ratio` का उपयोग करने वाले media‑queries को प्रभावित करेगा।

---

## Step 2: Set User Agent for the Sandbox

कस्टम **user agent** की ज़रूरत क्यों? कुछ साइटें रिपोर्ट किए गए ब्राउज़र के आधार पर अलग मार्कअप या स्क्रिप्ट्स देती हैं। `setUserAgent` को कॉल करके आप पेज को यह सोचने पर मजबूर कर सकते हैं कि वह Chrome, Firefox, या मोबाइल डिवाइस से विज़िट किया गया है।

```java
/* Step 2 – customize the user‑agent string */
sandbox.setUserAgent("Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                     "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                     "Version/15.0 Mobile/15E148 Safari/604.1");
```

अब पेज यह सोचेगा कि वह iPhone पर रेंडर हो रहा है। यदि आपको **user agent को डिफ़ॉल्ट पर सेट** करना है, तो बस पहले की “AsposeHTML/24.6 …” स्ट्रिंग को पुनः उपयोग करें।

---

## Step 3: Load an HTML Document Inside the Sandbox

sandbox तैयार होने के बाद, हम कोई भी URL या स्थानीय HTML फ़ाइल लोड कर सकते हैं। `HTMLDocument` कंस्ट्रक्टर दूसरा आर्ग्युमेंट के रूप में sandbox लेता है, जिससे दोनों बंधित हो जाते हैं।

```java
import com.aspose.html.HTMLDocument;

/* Step 3 – load the page using the configured sandbox */
try (HTMLDocument doc = new HTMLDocument("https://example.com", sandbox)) {
    // The document is now rendered inside the sandbox environment.
    // Any JavaScript or CSS will see the size and user‑agent we defined.
```

`try‑with‑resources` ब्लॉक यह सुनिश्चित करता है कि दस्तावेज़ सही ढंग से नष्ट हो जाए, जिससे Aspose.HTML द्वारा अंतर्निहित रूप से आवंटित नेटिव रिसोर्सेज़ मुक्त हो जाते हैं।

---

## Step 4: Get Viewport Size from the Document

यह वह क्षण है जिसका आप इंतज़ार कर रहे थे: **viewport size** प्राप्त करना जो रेंडरिंग इंजन ने गणना किया है। यह उत्तर देता है **पेज लेआउट होने के बाद viewport कैसे प्राप्त करें**।

```java
    /* Step 4 – fetch the viewport dimensions */
    Size2D viewport = doc.getDefaultView().getScreenSize();
    System.out.println("Viewport: " + viewport.getWidth() + "×" + viewport.getHeight());
}
```

जब आप प्रोग्राम चलाएंगे, तो आपको कुछ इस तरह दिखना चाहिए:

```
Viewport: 1280×800
```

यदि आपने Step 1 में sandbox के आयाम बदल दिए हैं, तो प्रिंट किए गए नंबर उन नई मानों को दर्शाएंगे—स्वचालित परीक्षणों के लिए बिल्कुल सही जो रिस्पॉन्सिव ब्रेकपॉइंट्स की पुष्टि करते हैं।

---

## Full Working Example

नीचे पूरी, तैयार‑चलाने‑योग्य क्लास दी गई है जो सभी भागों को एक साथ जोड़ती है। इसे `SandboxExample.java` नाम की फ़ाइल में कॉपी‑पेस्ट करें, Aspose.HTML JARs को क्लासपाथ में जोड़ें, और `java SandboxExample` चलाएँ।

```java
import com.aspose.html.*;
import com.aspose.html.drawing.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox with a custom screen size and DPI
        DocumentSandbox sandbox = new DocumentSandbox();
        sandbox.setScreenWidth(1280);          // width in pixels
        sandbox.setScreenHeight(800);          // height in pixels
        sandbox.setDeviceDpi(96);              // screen DPI
        sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");

        // Step 2: (Optional) Override the user agent if you need a mobile profile
        sandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
            "Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 3: Load the HTML document inside the configured sandbox
        try (HTMLDocument htmlDocument = new HTMLDocument("https://example.com", sandbox)) {

            // Step 4: Retrieve and display the computed viewport size
            Size2D viewportSize = htmlDocument.getDefaultView().getScreenSize();
            System.out.println("Viewport: " + viewportSize.getWidth() + "×" + viewportSize.getHeight());
        }
    }
}
```

**अपेक्षित आउटपुट** (ऊपर दिए गए sandbox सेटिंग्स मानते हुए):

```
Viewport: 1280×800
```

यदि आप sandbox में अलग चौड़ाई/ऊँचाई सेट करते हैं, तो आउटपुट उसी अनुसार बदल जाएगा—बिल्कुल वही जो आपको रिस्पॉन्सिव डिज़ाइनों के परीक्षण के लिए चाहिए।

---

## Edge Cases & Common Questions

### What if the page uses `window.innerWidth` instead of CSS media queries?

sandbox का वर्चुअल स्क्रीन आकार CSS लेआउट और JavaScript के `window.innerWidth/innerHeight` दोनों को प्रभावित करता है। इसलिए **JavaScript द्वारा viewport कैसे प्राप्त करें** वही नंबर देगा जो आप Java कंसोल में देखते हैं।

### Can I run multiple sandboxes in parallel?

हाँ। प्रत्येक `DocumentSandbox` इंस्टेंस स्वतंत्र है, इसलिए आप एक थ्रेड पूल बना सकते हैं, प्रत्येक थ्रेड को अलग‑अलग आयामों वाला अपना sandbox दे सकते हैं, और साथ‑साथ दर्जनों पेज रेंडर कर सकते हैं। बस JARs को थ्रेड‑सेफ़ रखें (वे थ्रेड‑सेफ़ हैं)।

### Does the DPI setting affect image scaling?

बिल्कुल। उच्च DPI एक CSS पिक्सेल को अधिक डिवाइस पिक्सेल से मैप करता है, जिससे हाई‑रिज़ॉल्यूशन इमेजेज़ अधिक शार्प दिखती हैं। यदि आप retina‑स्टाइल एसेट्स का परीक्षण कर रहे हैं, तो `sandbox.setDeviceDpi(144)` आज़माएँ।

### How do I handle HTTPS certificates that are self

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
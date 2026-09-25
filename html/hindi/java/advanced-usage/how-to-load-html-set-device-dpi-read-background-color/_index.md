---
category: general
date: 2026-02-16
description: जावा में HTML कैसे लोड करें, डिवाइस DPI सेट करें, वर्चुअल स्क्रीन आकार
  निर्धारित करें, और किसी भी तत्व का गणना किया गया बैकग्राउंड रंग पढ़ें।
draft: false
keywords:
- how to load html
- read background color
- set device dpi
- set virtual screen size
- get computed background color
language: hi
og_description: जावा में HTML लोड करना, डिवाइस DPI सेट करना, वर्चुअल स्क्रीन आकार
  निर्धारित करना, और किसी भी तत्व का गणना किया गया बैकग्राउंड रंग पढ़ना।
og_title: HTML कैसे लोड करें, डिवाइस DPI सेट करें और बैकग्राउंड रंग पढ़ें
tags:
- Aspose.HTML
- Java
title: HTML कैसे लोड करें, डिवाइस DPI सेट करें और बैकग्राउंड रंग पढ़ें
url: /hi/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML कैसे लोड करें, डिवाइस DPI सेट करें और बैकग्राउंड रंग पढ़ें

क्या आपने कभी सोचा है कि Java एप्लिकेशन में **HTML कैसे लोड करें** और फिर पेज की स्टाइल्स की जाँच करें? आप अकेले नहीं हैं—डेवलपर्स अक्सर वेब पेज को ऑफ‑स्क्रीन रेंडर करना, अंतिम CSS मान प्राप्त करना, और उन्हें PDF रूपांतरण, स्क्रीनशॉट या यहाँ तक कि ऑटोमेटेड टेस्ट्स के लिए उपयोग करना चाहते हैं।  

इस गाइड में हम ठीक वही करेंगे: हम एक HTML फ़ाइल लोड करेंगे, **डिवाइस DPI सेट करेंगे**, एक **वर्चुअल स्क्रीन साइज** परिभाषित करेंगे, और अंत में `<body>` एलिमेंट से **बैकग्राउंड रंग पढ़ेंगे**। अंत तक आपके पास एक पूरी तरह चलने वाला स्निपेट होगा जो **गणना किया गया बैकग्राउंड रंग** प्रिंट करेगा—कोई रहस्य नहीं, सिर्फ साधारण Java।

## आपको क्या चाहिए

* Java 17 या नया (कोड किसी भी हालिया JDK के साथ काम करता है)।  
* Aspose.HTML for Java 23.9 या बाद का संस्करण—Aspose साइट से JAR डाउनलोड करें या Maven के माध्यम से जोड़ें।  
* एक साधारण HTML फ़ाइल (जैसे `responsive.html`) जिसमें CSS में बैकग्राउंड रंग परिभाषित हो।

बस इतना ही—कोई अतिरिक्त फ्रेमवर्क नहीं, कोई ब्राउज़र ड्राइवर नहीं। तैयार हैं? चलिए शुरू करते हैं।

![HTML कैसे लोड करें और गणना की गई स्टाइल्स निकालें का चित्र](/images/load-html-diagram.png){alt="HTML कैसे लोड करें"}

## चरण 1: HTML कैसे लोड करें और रेंडरिंग विकल्प कॉन्फ़िगर करें

सबसे पहले आपको एक `HtmlLoadOptions` ऑब्जेक्ट बनाना होगा। यह ऑब्जेक्ट Aspose.HTML को बताता है कि **HTML कैसे लोड करें**—जिसमें वर्चुअल स्क्रीन डाइमेंशन और वह DPI शामिल है जिसे आप अनुकरण करना चाहते हैं।

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create load options and define the virtual screen size and DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        // setVirtualScreenSize – width × height in CSS pixels
        loadOptions.setScreenSize(new Size(1280, 800));
        // setDeviceDpi – typical desktop DPI (96 is the default for most monitors)
        loadOptions.setDeviceDpi(96);
```

**यह क्यों महत्वपूर्ण है:**  
वर्चुअल स्क्रीन साइज सेट करने से यह सुनिश्चित होता है कि `@media (max-width: 600px)` जैसे मीडिया क्वेरीज़ वास्तविक मॉनिटर पर रेंडर होने जैसा व्यवहार करें। DPI यह निर्धारित करता है कि CSS `px` यूनिट्स को फिजिकल पिक्सेल्स में कैसे मैप किया जाए—जो बाद में इमेज या PDF जनरेट करते समय अत्यंत आवश्यक है।

## चरण 2: कॉन्फ़िगर किए गए विकल्पों का उपयोग करके HTML फ़ाइल लोड करें

अब हम वास्तव में फ़ाइल लोड करते हैं। ध्यान दें कि हम वही `loadOptions` पास कर रहे हैं जिसे हमने अभी कॉन्फ़िगर किया था।

```java
        // 2️⃣ Load the HTML file with the options we just set.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);
```

यदि फ़ाइल नहीं मिलती है, तो Aspose एक स्पष्ट `FileNotFoundException` फेंकेगा। प्रोडक्शन में आप इसे try‑catch में लपेटकर डिफ़ॉल्ट HTML स्ट्रिंग पर फॉल्बैक करना चाहेंगे।

## चरण 3: वर्चुअल स्क्रीन साइज और डिवाइस DPI सेट करें (स्पष्ट रूप से)

भले ही हमने ऊपर `setScreenSize` और `setDeviceDpi` को कॉल किया हो, यह उल्लेखनीय है कि **set virtual screen size** और **set device dpi** को रेंडरिंग से पहले कभी भी समायोजित किया जा सकता है। उदाहरण के लिए, आप हाई‑रेज़ोल्यूशन स्क्रीनशॉट्स के लिए DPI बढ़ा सकते हैं:

```java
        // 3️⃣ Adjust DPI for a high‑resolution render (optional).
        loadOptions.setDeviceDpi(300);   // 300 DPI is common for print‑ready images
        // 4️⃣ Change screen size for a mobile layout test.
        loadOptions.setScreenSize(new Size(375, 667)); // iPhone X viewport
```

यदि आप पहली लोड के बाद इन सेटिंग्स को बदलते हैं तो दस्तावेज़ को पुनः लोड करना याद रखें—Aspose `Document` बन जाने के बाद इन्हें अपरिवर्तनीय मानता है।

## चरण 4: बैकग्राउंड रंग पढ़ें और गणना किया गया बैकग्राउंड रंग प्राप्त करें

डॉक्यूमेंट मेमोरी में होने पर आप किसी भी एलिमेंट की गणना की गई स्टाइल क्वेरी कर सकते हैं। यहाँ हम `<body>` टैग पर ध्यान केंद्रित कर रहे हैं, लेकिन यही तरीका `<div>`, `<p>` या यहाँ तक कि pseudo‑elements के लिए भी काम करता है।

```java
        // 5️⃣ Retrieve the <body> element.
        Element bodyElement = document.getBody();

        // 6️⃣ Output the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

**आप क्या देखेंगे:** यदि `responsive.html` में `body { background: #ff5722; }` है, तो कंसोल कुछ इस तरह प्रिंट करेगा:

```
Computed background color: rgba(255,87,34,1)
```

यह **गणना किया गया बैकग्राउंड रंग** परिणाम है—Aspose सभी CSS कैस्केड नियम, मीडिया क्वेरीज़, और यहाँ तक कि `!important` डिक्लेरेशन्स को हल करके अंतिम मान लौटाता है।

## पूर्ण कार्यशील उदाहरण

सभी को एक साथ मिलाकर, यहाँ पूरा, कॉपी‑पेस्ट‑रेडी प्रोग्राम है:

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create load options – virtual screen size + DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        loadOptions.setScreenSize(new Size(1280, 800)); // set virtual screen size
        loadOptions.setDeviceDpi(96);                  // set device DPI (default desktop)

        // Optional: tweak for high‑resolution or mobile rendering.
        // loadOptions.setDeviceDpi(300);
        // loadOptions.setScreenSize(new Size(375, 667));

        // Step 2: Load the HTML document with the options.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);

        // Step 3: Grab the <body> element.
        Element bodyElement = document.getBody();

        // Step 4: Print the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

### अपेक्षित आउटपुट

```
Computed background color: rgba(255,255,255,1)
```

*(सटीक RGBA मान आपके HTML फ़ाइल में मौजूद CSS पर निर्भर करेंगे।)*

## सामान्य समस्याएँ और प्रो टिप्स

* **DPI सेटिंग गायब?** Aspose डिफ़ॉल्ट रूप से 96 DPI उपयोग करता है, जिससे हाई‑रेज़ोल्यूशन स्क्रीनशॉट्स धुंधले हो सकते हैं। यदि आपको स्पष्ट आउटपुट चाहिए तो हमेशा इसे स्पष्ट रूप से सेट करें।

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
date: 2025-12-05
description: Aspose.HTML का उपयोग करके जावा में HTML पेज के मार्जिन सेट करना सीखें,
  और अपने दस्तावेज़ों में पृष्ठ संख्या और शीर्षक जोड़ें।
linktitle: CSS Extensions - Adding Title and Page Number
second_title: Java HTML Processing with Aspose.HTML
title: Aspose.HTML के साथ जावा में HTML पेज मार्जिन कैसे सेट करें
url: /hi/java/advanced-usage/css-extensions-adding-title-page-number/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML पेज मार्जिन Java के साथ Aspose.HTML का उपयोग करके कैसे सेट करें

इस ट्यूटोरियल में आप Aspose.HTML for Java का उपयोग करके **HTML पेज मार्जिन Java‑स्टाइल** कैसे सेट करें, यह जानेंगे। हम कस्टम पेज मार्जिन बनाना, पेज नंबर डालना, और दस्तावेज़ शीर्षक जोड़ना—इन सभी को स्पष्ट, चरण‑दर‑चरण कोड के साथ दिखाएंगे जिसे आप अपने प्रोजेक्ट में कॉपी कर सकते हैं।

## त्वरित उत्तर
- **कौनसी लाइब्रेरी चाहिए?** Aspose.HTML for Java  
- **क्या मैं मार्जिन प्रोग्रामेटिकली नियंत्रित कर सकता हूँ?** हाँ, यूज़र‑स्टाइल शीट में CSS `@page` नियम के माध्यम से  
- **कौनसे आउटपुट फॉर्मेट मार्जिन को सपोर्ट करते हैं?** XPS, PDF, और अन्य रास्टर फॉर्मेट  
- **क्या प्रोडक्शन के लिए लाइसेंस चाहिए?** गैर‑ट्रायल उपयोग के लिए एक वैध Aspose.HTML लाइसेंस आवश्यक है  
- **क्या यह Java 11+ के साथ संगत है?** बिल्कुल – लाइब्रेरी आधुनिक Java संस्करणों के साथ काम करती है  

## “HTML पेज मार्जिन Java सेट करना” क्या है?
Java में HTML पेज मार्जिन सेट करना का अर्थ है रेंडरिंग इंजन (जो Aspose.HTML द्वारा प्रदान किया गया है) को कॉन्फ़िगर करना ताकि दस्तावेज़ को XPS या PDF जैसे प्रिंटेबल फॉर्मेट में बदलने से पहले CSS पेज‑बॉक्स प्रॉपर्टीज़ लागू हों। एक कस्टम `@page` नियम परिभाषित करके आप प्रिंटेबल एरिया, पेज नंबर, और हेडर/फ़ूटर कंटेंट को नियंत्रित कर सकते हैं।

## मार्जिन नियंत्रण के लिए Aspose.HTML क्यों उपयोग करें?
- **सटीक लेआउट** – CSS `@page` आपको मार्जिन, हेडर, और फ़ूटर पर पिक्सेल‑परफेक्ट नियंत्रण देता है।  
- **क्रॉस‑फ़ॉर्मेट स्थिरता** – वही मार्जिन परिभाषाएँ XPS, PDF, और इमेज आउटपुट के लिए काम करती हैं।  
- **ब्राउज़र निर्भरता नहीं** – रेंडरिंग सर्वर‑साइड होती है, इसलिए आपको हेडलेस ब्राउज़र की आवश्यकता नहीं है।  

## पूर्वापेक्षाएँ

शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ मौजूद हैं:

1. **Java विकास पर्यावरण** – JDK 11 या बाद का स्थापित हो।  
2. **Aspose.HTML for Java** – लाइब्रेरी को [यहाँ](https://releases.aspose.com/html/java/) से डाउनलोड और इंस्टॉल करें।  

## पैकेज इम्पोर्ट करें

शुरू करने के लिए, आवश्यक Aspose.HTML क्लासेस को इम्पोर्ट करें:

```java
// Import Aspose.HTML packages
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

## HTML पेज मार्जिन Java सेट करने का चरण‑दर‑चरण गाइड

### चरण 1: कॉन्फ़िगरेशन इनिशियलाइज़ करें और कस्टम पेज मार्जिन परिभाषित करें

```java
// Initialize configuration object and set up the page-margins for the document
Configuration configuration = new Configuration();
try {
    // Get the User Agent service
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Set the style of custom margins and create marks on it
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

इस ब्लॉक में हम एक `Configuration` ऑब्जेक्ट बनाते हैं, `IUserAgentService` प्राप्त करते हैं, और एक CSS `@page` नियम इंजेक्ट करते हैं जो मार्जिन, नीचे‑दाएँ पेज काउंटर, और ऊपर‑केन्द्र में दस्तावेज़ शीर्षक को परिभाषित करता है।

### चरण 2: HTML दस्तावेज़ बनाएं

```java
// Initialize an HTML document
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

यहाँ हम एक सरल “Hello World” स्निपेट के साथ `HTMLDocument` का इंस्टैंस बनाते हैं। चरण 1 की वही कॉन्फ़िगरेशन लागू की गई है, इसलिए दस्तावेज़ रेंडर होने पर कस्टम मार्जिन मान्य होते हैं।

### चरण 3: XPS फ़ाइल (या कोई भी समर्थित आउटपुट) में रेंडर करें

```java
// Initialize an output device
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    // Send the document to the output device
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

यह चरण एक `XpsDevice` बनाता है जो रेंडर किए गए पेजों को `output.xps` में लिखता है। आपने पहले परिभाषित किए हुए मार्जिन, पेज नंबर, और शीर्षक अंतिम फ़ाइल में दिखेंगे।

## सामान्य समस्याएँ और सुझाव

- **मार्जिन अपरिवर्तित दिख रहे हैं** – सुनिश्चित करें कि `@page` नियम अन्य स्टाइलशीट्स द्वारा ओवरराइड नहीं हो रहा है। `setUserStyleSheet` कॉल इसे सबसे उच्च प्राथमिकता देता है।  
- **पेज नंबर “NaN” दिखा रहे हैं** – जांचें कि आप Aspose.HTML संस्करण 23.10 या उससे नया उपयोग कर रहे हैं; पुराने संस्करणों में `currentPageNumber()` फ़ंक्शन नहीं होता।  
- **आउटपुट फ़ाइल खाली है** – पुष्टि करें कि `Resources.output` पाथ सही ढंग से हल हो रहा है और आपके पास लिखने की अनुमति है।  

## अक्सर पूछे जाने वाले प्रश्न

### प्रश्न 1: Aspose.HTML for Java क्या है?

**A:** Aspose.HTML for Java एक Java लाइब्रेरी है जो Java एप्लिकेशन्स में HTML दस्तावेज़ों के साथ काम करने के लिए शक्तिशाली टूल्स प्रदान करती है, जिसमें रूपांतरण, रेंडरिंग, और मैनिपुलेशन शामिल हैं।

### प्रश्न 2: क्या मैं पेज मार्जिन को और कस्टमाइज़ कर सकता हूँ?

**A:** हाँ, बस `setUserStyleSheet` के अंदर CSS को संपादित करें। आप किसी भी `margin-*` मान को बदल सकते हैं या अतिरिक्त `@top-*` / `@bottom-*` बॉक्स जोड़ सकते हैं।

### प्रश्न 3: मैं HTML दस्तावेज़ में अधिक सामग्री कैसे जोड़ सकता हूँ?

**A:** `new HTMLDocument("<div>Hello World!!!</div>", …)` में स्ट्रिंग को अपने स्वयं के HTML मार्कअप से बदलें, या `HTMLDocument(String url, …)` कंस्ट्रक्टर का उपयोग करके बाहरी फ़ाइल लोड करें।

### प्रश्न 4: क्या Aspose.HTML for Java अन्य दस्तावेज़ फॉर्मेट्स के साथ संगत है?

**A:** बिल्कुल। वही `HTMLDocument` को आउटपुट डिवाइस बदलकर PDF, XPS, इमेज, या यहाँ तक कि EPUB में भी रेंडर किया जा सकता है (जैसे `PdfDevice`, `PngDevice`)।

### प्रश्न 5: Aspose.HTML for Java उपयोग करने के लिए क्या मुझे लाइसेंस चाहिए?

**A:** हाँ, प्रोडक्शन उपयोग के लिए लाइसेंस आवश्यक है। आप एक ट्रायल प्राप्त कर सकते हैं या लाइसेंस खरीद सकते हैं [यहाँ](https://purchase.aspose.com/buy) या [यहाँ](https://releases.aspose.com/) से।

### प्रश्न 6: विषम और सम पृष्ठों के लिए अलग मार्जिन कैसे सेट करें?

**A:** अपने स्टाइल शीट में `@page :left` और `@page :right` प्स्यूडो‑क्लासेज़ का उपयोग करके बाएँ‑हाथ (सम) और दाएँ‑हाथ (विषम) पृष्ठों के लिए अलग-अलग मार्जिन परिभाषित करें।

### प्रश्न 7: क्या मैं रेंडर किए गए दस्तावेज़ में कस्टम फ़ॉन्ट एम्बेड कर सकता हूँ?

**A:** हाँ। यूज़र स्टाइल शीट में `@font-face` नियम जोड़ें और अपने HTML कंटेंट में फ़ॉन्ट्स का संदर्भ दें।

## निष्कर्ष

अब आप Aspose.HTML का उपयोग करके **HTML पेज मार्जिन Java सेट करना** में निपुण हो गए हैं, और आप पेज नंबर और शीर्षक जोड़ना जानते हैं जिससे आपके दस्तावेज़ पेशेवर दिखें। अतिरिक्त `@page` बॉक्स, कस्टम फ़ॉन्ट्स, या विभिन्न आउटपुट फॉर्मेट्स के साथ प्रयोग करने में संकोच न करें ताकि आपके प्रोजेक्ट की आवश्यकताओं को पूरा किया जा सके।

यदि आपको कोई चुनौती आती है, तो आधिकारिक [Aspose.HTML for Java दस्तावेज़ीकरण](https://reference.aspose.com/html/java/) और [Aspose सपोर्ट फ़ोरम](https://forum.aspose.com/) मदद के लिए उत्कृष्ट स्थान हैं।

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2025-12-05  
**Tested With:** Aspose.HTML for Java 23.12  
**Author:** Aspose  

---
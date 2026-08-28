---
date: 2026-03-18
description: Aspose.HTML for Java का उपयोग करके HTML को XPS में कैसे बदलें और XPS
  पेज आकार को कैसे समायोजित करें, सीखें। आउटपुट आयामों को आसानी से नियंत्रित करें।
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Aspose.HTML for Java के साथ HTML को XPS में बदलें और XPS पेज आकार समायोजित
  करें
url: /hi/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML को XPS में बदलें और Aspose.HTML for Java के साथ XPS पेज आकार समायोजित करें

इस ट्यूटोरियल में आप **HTML को XPS में कैसे बदलें** और Aspose.HTML for Java का उपयोग करके उत्पन्न पेज आकार को बारीकी से समायोजित करना सीखेंगे। चाहे आप प्रिंटेबल रिपोर्ट, इनवॉइस, या अभिलेखीय दस्तावेज़ बना रहे हों, XPS आयामों को नियंत्रित करने से आउटपुट बिल्कुल वही दिखेगा जैसा आप चाहते हैं। हम हर चरण को विस्तार से बताएँगे—पर्यावरण सेटअप से लेकर अंतिम XPS फ़ाइल को रेंडर करने तक—ताकि आप इस क्षमता को तुरंत अपने Java एप्लिकेशन में एकीकृत कर सकें।

## त्वरित उत्तर
- **HTML को XPS में बदलने** का क्या मतलब है? यह एक HTML दस्तावेज़ को XPS फ़ाइल में रेंडर करता है, लेआउट और स्टाइलिंग को संरक्षित रखते हुए।  
- **क्या मुझे लाइसेंस चाहिए?** विकास के लिए एक मुफ्त ट्रायल काम करता है; उत्पादन के लिए एक व्यावसायिक लाइसेंस आवश्यक है।  
- **कौन सा Java संस्करण समर्थित है?** Java 8 या उससे ऊपर (JDK 11+ की सिफारिश)।  
- **क्या मैं पेज आकार बदल सकता हूँ?** हाँ – Aspose.HTML आपको रेंडरिंग से पहले कस्टम आयाम निर्दिष्ट करने देता है।  
- **परिवर्तन में कितना समय लगता है?** सामान्य पृष्ठों के लिए आमतौर पर एक सेकंड से कम, बड़े दस्तावेज़ों में अधिक समय लग सकता है।

## HTML को XPS में बदलना क्या है?
HTML को XPS में बदलना का अर्थ है वेब‑उन्मुख मार्कअप फ़ाइल को लेकर एक XPS (XML Paper Specification) दस्तावेज़ बनाना—एक स्थिर‑लेआउट, प्रिंट‑तैयार फ़ॉर्मेट जो PDF के समान है। यह तब उपयोगी होता है जब आपको उच्च‑गुणवत्ता, डिवाइस‑स्वतंत्र दस्तावेज़ों की आवश्यकता होती है, जो Java एप्लिकेशन से अभिलेख या प्रिंटिंग के लिए उपयुक्त हों।

## XPS पेज आकार को समायोजित क्यों करें?
पेज आकार को समायोजित करने से आपको अंतिम दस्तावेज़ के भौतिक आयामों (जैसे A4, Letter, कस्टम लेबल) पर नियंत्रण मिलता है। यह अनचाहे स्केलिंग को रोकता है, सुनिश्चित करता है कि सामग्री पूरी तरह फिट हो, और अनावश्यक सफ़ेद स्थान को हटाकर फ़ाइल आकार को कम कर सकता है।

## पूर्वापेक्षाएँ

शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ मौजूद हैं:

1. **Java विकास वातावरण** – आपके सिस्टम पर Java Development Kit (JDK) स्थापित होना चाहिए।  
2. **Aspose.HTML for Java लाइब्रेरी** – Aspose.HTML for Java लाइब्रेरी को डाउनलोड करके अपने प्रोजेक्ट में शामिल करें। आप लाइब्रेरी [here](https://releases.aspose.com/html/java/) पर पा सकते हैं।  
3. **इनपुट HTML फ़ाइल** – एक HTML फ़ाइल तैयार करें जिसे आप रेंडर करना चाहते हैं और XPS पेज आकार समायोजित करना चाहते हैं। इस ट्यूटोरियल के लिए आप अपनी स्वयं की HTML फ़ाइल का उपयोग कर सकते हैं।

## पैकेज आयात करें

सबसे पहले, उन क्लासों को आयात करें जिनकी आपको आवश्यकता होगी। ये पैकेज दस्तावेज़ हैंडलिंग, रेंडरिंग, और पेज‑सेटअप सुविधाओं तक पहुंच प्रदान करते हैं।

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## चरण‑दर‑चरण गाइड

नीचे एक संक्षिप्त, क्रमांकित walkthrough दिया गया है जो मूल चरणों को प्रतिबिंबित करता है और स्पष्टता के लिए अतिरिक्त संदर्भ जोड़ता है।

### चरण 1: इनपुट फ़ाइल नाम सेट करें

`FileInputStream` का उपयोग करके स्रोत HTML फ़ाइल पढ़ें। यह स्ट्रीम कच्चे HTML को Aspose.HTML इंजन में भेजती है।

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

### चरण 2: HTML दस्तावेज़ बनाएं और स्टाइल सेट करें

`HTMLDocument` इंस्टेंस बनाएं जो उस सामग्री का प्रतिनिधित्व करता है जिसे आप रेंडर करेंगे। इस उदाहरण में हम एक छोटा CSS ब्लॉक भी सम्मिलित करते हैं ताकि स्टाइलिंग का प्रदर्शन हो—इसे अपनी स्वयं की मार्कअप से बदलने में संकोच न करें।

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n" +
               "\n";

// ...
```

### चरण 3: XPS रेंडरिंग विकल्प बनाएं

`XpsRenderingOptions` को इंस्टैंशिएट करें ताकि सभी सेटिंग्स को रखा जा सके जो HTML से XPS में परिवर्तन को प्रभावित करती हैं।

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

### चरण 4: पेज आकार समायोजित करें  

**XPS पेज आकार कैसे सेट करें** – एक कस्टम पेज आकार (बिंदुओं में चौड़ाई × ऊँचाई) निर्धारित करें और रेंडरर को बताएं कि क्या इसे स्वचालित रूप से सबसे चौड़े पेज तक विस्तारित करना चाहिए। `adjustToWidestPage` को `false` सेट करने से आप द्वारा निर्दिष्ट सटीक आयाम संरक्षित रहते हैं।

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

### चरण 5: आउटपुट रेंडर करें

अंत में, कॉन्फ़िगर किए गए विकल्पों के साथ एक `XpsDevice` बनाएं और HTML दस्तावेज़ को रेंडर करें। परिणामस्वरूप एक पूरी तरह से निर्मित XPS फ़ाइल प्राप्त होगी जिसमें आपने सेट किए हुए कस्टम पेज आयाम होंगे।

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## सामान्य समस्याएँ और समाधान

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **खाली XPS आउटपुट** | इनपुट स्ट्रीम बंद नहीं की गई या HTMLDocument गलत फ़ाइल की ओर इशारा कर रहा है। | `FileInputStream` को सही तरीके से try‑with‑resources ब्लॉक में रैप किया गया है और फ़ाइल पाथ सही है, यह सुनिश्चित करें। |
| **पेज आकार लागू नहीं हुआ** | `adjustToWidestPage` को `true` ही रहने दिया गया। | Step 4 में दिखाए अनुसार `pageSetup.setAdjustToWidestPage(false);` सेट करें। |
| **असमर्थित CSS** | Aspose.HTML केवल CSS का एक उपसमुच्चय समर्थन करता है। | बेसिक लेआउट, फ़ॉन्ट और रंगों का उपयोग करें; उन्नत सिलेक्टर्स या CSS Grid से बचें। |
| **LicenseException** | उत्पादन में वैध लाइसेंस के बिना चलाना। | रेंडरिंग से पहले अपना अस्थायी या खरीदा हुआ लाइसेंस लागू करें (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## अक्सर पूछे जाने वाले प्रश्न

**Q: Aspose.HTML for Java क्या है?**  
A: Aspose.HTML for Java एक Java लाइब्रेरी है जो डेवलपर्स को HTML दस्तावेज़ों को विभिन्न फ़ॉर्मेट्स, जैसे XPS, PDF, और इमेजेज़ में बदलने और हेरफेर करने की अनुमति देती है।

**Q: मैं Aspose.HTML for Java कहाँ डाउनलोड कर सकता हूँ?**  
A: आप Aspose.HTML for Java लाइब्रेरी को [this link](https://releases.aspose.com/html/java/) से डाउनलोड कर सकते हैं।

**Q: क्या Aspose.HTML for Java के लिए मुफ्त ट्रायल उपलब्ध है?**  
A: हाँ, आप Aspose.HTML for Java का मुफ्त ट्रायल [here](https://releases.aspose.com/) से प्राप्त कर सकते हैं।

**Q: मैं Aspose.HTML for Java के लिए अस्थायी लाइसेंस कैसे प्राप्त करूँ?**  
A: Aspose.HTML for Java के लिए अस्थायी लाइसेंस पाने हेतु [this page](https://purchase.aspose.com/temporary-license/) पर जाएँ।

**Q: क्या मैं Aspose.HTML for Java के लिए समर्थन प्राप्त कर सकता हूँ?**  
A: हाँ, आप Aspose समुदाय से मदद और समर्थन [Aspose Forum](https://forum.aspose.com/) पर ले सकते हैं।

**Q: क्या मैं हेडलेस सर्वर पर HTML को XPS में बदल सकता हूँ?**  
A: बिल्कुल। Aspose.HTML GUI‑रहित वातावरण में भी काम करता है; बस यह सुनिश्चित करें कि Java रनटाइम सही तरीके से कॉन्फ़िगर किया गया हो।

**Q: क्या लाइब्रेरी कस्टम पेज मार्जिन का समर्थन करती है?**  
A: हाँ। `PageSetup` को रेंडरिंग विकल्पों में असाइन करने से पहले `PageSetup.setMarginTop()`, `setMarginBottom()` आदि का उपयोग करें।

## निष्कर्ष

हमने **HTML को XPS में बदलने** और Aspose.HTML for Java के साथ पेज आकार समायोजित करने की पूरी प्रक्रिया को समझा। इन चरणों का पालन करके आप प्रिंट‑तैयार XPS दस्तावेज़ बना सकते हैं जो आपके सटीक लेआउट आवश्यकताओं से मेल खाते हैं। विभिन्न पेज आयाम, स्टाइल, या यहाँ तक कि हेडर और फुटर जोड़ने के साथ प्रयोग करने में संकोच न करें ताकि आपके प्रोजेक्ट की जरूरतों को पूरा किया जा सके।

यदि आपके पास कोई प्रश्न हैं या अतिरिक्त सहायता चाहिए, तो [Aspose.HTML for Java दस्तावेज़ीकरण](https://reference.aspose.com/html/java/) देखें या [Aspose Forum](https://forum.aspose.com/) पर बातचीत में शामिल हों।

---

**Last Updated:** 2026-03-18  
**Tested With:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
---
date: 2025-11-29
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

इस ट्यूटोरियल में आप **HTML को XPS में कैसे बदलें** और उत्पन्न पेज आकार को कैसे फाइन‑ट्यून करें, यह सीखेंगे। चाहे आप प्रिंटेबल रिपोर्ट, इनवॉइस, या आर्काइव दस्तावेज़ बना रहे हों, XPS आयामों को नियंत्रित करने से आउटपुट बिल्कुल वही दिखेगा जैसा आप चाहते हैं। हम हर कदम—पर्यावरण सेटअप से लेकर अंतिम XPS फ़ाइल रेंडर करने तक—परिचित कराएंगे, ताकि आप इस क्षमता को तुरंत अपने Java एप्लिकेशन में एकीकृत कर सकें।

## त्वरित उत्तर
- **“convert HTML to XPS” का क्या अर्थ है?** यह एक HTML दस्तावेज़ को XPS फ़ाइल में रेंडर करता है, लेआउट और स्टाइलिंग को संरक्षित रखते हुए।  
- **क्या मुझे लाइसेंस चाहिए?** विकास के लिए मुफ्त ट्रायल काम करता है; उत्पादन के लिए व्यावसायिक लाइसेंस आवश्यक है।  
- **कौन सा Java संस्करण समर्थित है?** Java 8 या उससे ऊपर (JDK 11+ की सिफारिश)।  
- **क्या मैं पेज आकार बदल सकता हूँ?** हाँ – Aspose.HTML आपको रेंडरिंग से पहले कस्टम आयाम निर्दिष्ट करने देता है।  
- **परिवर्तन में कितना समय लगता है?** सामान्य पेजों के लिए आमतौर पर एक सेकंड से कम; बड़े दस्तावेज़ों में अधिक समय लग सकता है।

## HTML को XPS में बदलना क्या है?
HTML को XPS में बदलना का मतलब है वेब‑उन्मुख मार्कअप फ़ाइल को XPS (XML Paper Specification) दस्तावेज़ में परिवर्तित करना—एक फिक्स्ड‑लेआउट, प्रिंट‑रेडी फ़ॉर्मेट जो PDF के समान है। यह तब उपयोगी होता है जब आपको उच्च‑फ़िडेलिटी, डिवाइस‑इंडिपेंडेंट दस्तावेज़ों की आवश्यकता होती है, जैसे कि आर्काइविंग या Java एप्लिकेशन से प्रिंटिंग।

## XPS पेज आकार क्यों समायोजित करें?
पेज आकार समायोजित करने से आप अंतिम दस्तावेज़ के भौतिक आयामों (जैसे A4, Letter, कस्टम लेबल) पर नियंत्रण पा सकते हैं। यह अनचाहे स्केलिंग को रोकता है, सामग्री को पूरी तरह फिट करता है, और अनावश्यक व्हाइट स्पेस को हटाकर फ़ाइल आकार घटा सकता है।

## आवश्यकताएँ

शुरू करने से पहले सुनिश्चित करें कि आपके पास निम्नलिखित आवश्यकताएँ उपलब्ध हों:

1. **Java विकास पर्यावरण** – आपके सिस्टम पर Java Development Kit (JDK) स्थापित हो।  
2. **Aspose.HTML for Java लाइब्रेरी** – Aspose.HTML for Java लाइब्रेरी डाउनलोड करके अपने प्रोजेक्ट में शामिल करें। आप लाइब्रेरी [यहाँ](https://releases.aspose.com/html/java/) पा सकते हैं।  
3. **इनपुट HTML फ़ाइल** – वह HTML फ़ाइल तैयार रखें जिसे आप रेंडर करना और XPS पेज आकार समायोजित करना चाहते हैं। इस ट्यूटोरियल के लिए आप अपनी स्वयं की HTML फ़ाइल उपयोग कर सकते हैं।

## पैकेज आयात करें

सबसे पहले, उन क्लासेस को आयात करें जिनकी आपको आवश्यकता होगी। ये पैकेज आपको दस्तावेज़ हैंडलिंग, रेंडरिंग, और पेज‑सेटअप सुविधाओं तक पहुँच प्रदान करते हैं।

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## चरण 1: इनपुट फ़ाइल नाम सेट करें

`FileInputStream` का उपयोग करके स्रोत HTML फ़ाइल पढ़ें। यह स्ट्रीम कच्चे HTML को Aspose.HTML इंजन में फीड करता है।

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

## चरण 2: HTML दस्तावेज़ बनाएं और स्टाइल सेट करें

`HTMLDocument` इंस्टेंस बनाएं जो उस सामग्री का प्रतिनिधित्व करता है जिसे आप रेंडर करेंगे। इस उदाहरण में हम एक छोटा CSS ब्लॉक इंजेक्ट करते हैं ताकि स्टाइलिंग दिखा सकें—आप इसे अपनी मार्कअप से बदल सकते हैं।

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

## चरण 3: XPS रेंडरिंग विकल्प बनाएं

`XpsRenderingOptions` को इंस्टैंशिएट करें ताकि सभी सेटिंग्स रखी जा सकें जो HTML से XPS में परिवर्तन को प्रभावित करती हैं।

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

## चरण 4: पेज आकार समायोजित करें

कस्टम पेज आकार (चौड़ाई × ऊँचाई पॉइंट्स में) निर्धारित करें और रेंडरर को बताएं कि क्या उसे सबसे चौड़े पेज पर स्वचालित रूप से विस्तार करना चाहिए। `adjustToWidestPage` को `false` सेट करने से आप द्वारा निर्दिष्ट सटीक आयाम संरक्षित रहते हैं।

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

## चरण 5: आउटपुट रेंडर करें

अंत में, कॉन्फ़िगर किए गए विकल्पों के साथ `XpsDevice` बनाएं और HTML दस्तावेज़ को रेंडर करें। परिणामस्वरूप एक पूर्ण‑निर्मित XPS फ़ाइल प्राप्त होगी जिसमें आपने सेट किया हुआ कस्टम पेज आकार होगा।

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## सामान्य समस्याएँ और समाधान

| समस्या | कारण | समाधान |
|-------|------|--------|
| **खाली XPS आउटपुट** | इनपुट स्ट्रीम बंद नहीं हुई या HTMLDocument गलत फ़ाइल की ओर इशारा कर रहा है। | सुनिश्चित करें कि `FileInputStream` को सही तरीके से `try‑with‑resources` ब्लॉक में रैप किया गया है और फ़ाइल पाथ सटीक है। |
| **पेज आकार लागू नहीं हो रहा** | `adjustToWidestPage` को `true` रखा गया है। | चरण 4 में दिखाए अनुसार `pageSetup.setAdjustToWidestPage(false);` सेट करें। |
| **असमर्थित CSS** | Aspose.HTML CSS का केवल एक उपसमुच्चय समर्थन करता है। | बुनियादी लेआउट, फ़ॉन्ट और रंगों तक सीमित रहें; उन्नत सिलेक्टर्स या CSS Grid से बचें। |
| **LicenseException** | उत्पादन में वैध लाइसेंस के बिना चल रहा है। | रेंडरिंग से पहले अपना अस्थायी या खरीदा हुआ लाइसेंस लागू करें (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`)। |

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: Aspose.HTML for Java क्या है?**  
उत्तर: Aspose.HTML for Java एक Java लाइब्रेरी है जो डेवलपर्स को HTML दस्तावेज़ों को विभिन्न फ़ॉर्मेट, जैसे XPS, PDF, और इमेजेज़ में बदलने की अनुमति देती है।

**प्रश्न: मैं Aspose.HTML for Java कहाँ डाउनलोड कर सकता हूँ?**  
उत्तर: आप Aspose.HTML for Java लाइब्रेरी [इस लिंक](https://releases.aspose.com/html/java/) से डाउनलोड कर सकते हैं।

**प्रश्न: क्या Aspose.HTML for Java के लिए मुफ्त ट्रायल उपलब्ध है?**  
उत्तर: हाँ, आप Aspose.HTML for Java का मुफ्त ट्रायल [यहाँ](https://releases.aspose.com/) से प्राप्त कर सकते हैं।

**प्रश्न: मैं Aspose.HTML for Java के लिए अस्थायी लाइसेंस कैसे प्राप्त करूँ?**  
उत्तर: Aspose.HTML for Java के लिए अस्थायी लाइसेंस पाने हेतु [इस पेज](https://purchase.aspose.com/temporary-license/) पर जाएँ।

**प्रश्न: क्या मैं Aspose.HTML for Java के लिए सपोर्ट प्राप्त कर सकता हूँ?**  
उत्तर: हाँ, आप Aspose समुदाय से मदद ले सकते हैं, जैसे कि [Aspose फ़ोरम](https://forum.aspose.com/) पर।

**प्रश्न: क्या मैं हेडलेस सर्वर पर HTML को XPS में बदल सकता हूँ?**  
उत्तर: बिल्कुल। Aspose.HTML GUI‑रहित वातावरण में काम करता है; बस सुनिश्चित करें कि Java रनटाइम सही तरीके से कॉन्फ़िगर हो।

**प्रश्न: क्या लाइब्रेरी कस्टम पेज मार्जिन समर्थन करती है?**  
उत्तर: हाँ। `PageSetup.setMarginTop()`, `setMarginBottom()` आदि का उपयोग करके रेंडरिंग विकल्पों में `PageSetup` असाइन करने से पहले मार्जिन सेट करें।

## निष्कर्ष

हमने **HTML को XPS में बदलने** और Aspose.HTML for Java के साथ पेज आकार समायोजित करने की पूरी प्रक्रिया को कवर किया। इन चरणों का पालन करके आप प्रिंट‑रेडी XPS दस्तावेज़ बना सकते हैं जो आपके सटीक लेआउट आवश्यकताओं को पूरा करता है। विभिन्न पेज आयाम, स्टाइल्स, या यहाँ तक कि हेडर‑फ़ूटर जोड़ने के साथ प्रयोग करने में संकोच न करें।

यदि आपके कोई प्रश्न हैं या अतिरिक्त सहायता चाहिए, तो [Aspose.HTML for Java दस्तावेज़ीकरण](https://reference.aspose.com/html/java/) देखें या [Aspose फ़ोरम](https://forum.aspose.com/) पर चर्चा में शामिल हों।

---

**अंतिम अपडेट:** 2025-11-29  
**परीक्षित संस्करण:** Aspose.HTML for Java 24.11 (लेखन समय पर नवीनतम)  
**लेखक:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
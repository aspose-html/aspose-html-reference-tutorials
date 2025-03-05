---
title: Java के लिए Aspose.HTML के साथ XPS पृष्ठ आकार समायोजित करें
linktitle: XPS पृष्ठ आकार समायोजित करना
second_title: Aspose.HTML के साथ जावा HTML प्रसंस्करण
description: Java के लिए Aspose.HTML के साथ XPS पृष्ठ आकार को समायोजित करना सीखें। अपने XPS दस्तावेज़ों के आउटपुट आयामों को आसानी से नियंत्रित करें।
type: docs
weight: 16
url: /hi/java/advanced-usage/adjust-xps-page-size/
---

इस ट्यूटोरियल में, हम आपको जावा के लिए Aspose.HTML का उपयोग करके XPS पेज आकार को समायोजित करने की प्रक्रिया के माध्यम से मार्गदर्शन करेंगे। यह शक्तिशाली लाइब्रेरी आपको HTML दस्तावेज़ों में हेरफेर करने और उन्हें XPS सहित विभिन्न प्रारूपों में प्रस्तुत करने की अनुमति देती है। जब आपको अपने XPS दस्तावेज़ के आउटपुट आयामों को नियंत्रित करने की आवश्यकता होती है, तो पृष्ठ आकार को समायोजित करना आवश्यक होता है।

## आवश्यक शर्तें

शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ मौजूद हैं:

1. जावा डेवलपमेंट एनवायरनमेंट: सुनिश्चित करें कि आपके सिस्टम पर जावा डेवलपमेंट किट (JDK) स्थापित है।

2.  Aspose.HTML for Java लाइब्रेरी: आपको अपने Java प्रोजेक्ट में Aspose.HTML for Java लाइब्रेरी को डाउनलोड करके शामिल करना होगा। आप लाइब्रेरी पा सकते हैं[यहाँ](https://releases.aspose.com/html/java/).

3. इनपुट HTML फ़ाइल: एक HTML फ़ाइल तैयार करें जिसे आप रेंडर करना चाहते हैं और उसके लिए XPS पेज का आकार समायोजित करें। आप इस ट्यूटोरियल के लिए अपनी खुद की HTML फ़ाइल का उपयोग कर सकते हैं।

## पैकेज आयात करें

सबसे पहले, आपको Java के लिए Aspose.HTML के साथ काम करने के लिए आवश्यक पैकेज आयात करने होंगे। अपने Java क्लास की शुरुआत में इन पैकेज को शामिल करें:

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## चरण 1: इनपुट फ़ाइल नाम सेट करें

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

 इस चरण में, हम आपकी HTML इनपुट फ़ाइल को एक का उपयोग करके पढ़ते हैं`FileInputStream`.

## चरण 2: HTML दस्तावेज़ बनाएं और शैलियाँ सेट करें

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
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n";

// ...
```

 इस चरण में एक बनाना शामिल है`HTMLDocument` और इसमें शैलियाँ जोड़ना।

## चरण 3: XPS रेंडरिंग विकल्प बनाएँ

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

यहां, हम रेंडरिंग प्रक्रिया को कॉन्फ़िगर करने के लिए XPS रेंडरिंग विकल्प बनाते हैं।

## चरण 4: पृष्ठ का आकार समायोजित करें

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

इस चरण में पृष्ठ का आकार निर्धारित करना तथा यह निर्दिष्ट करना शामिल है कि इसे सबसे चौड़े पृष्ठ पर समायोजित किया जाए या नहीं।

## चरण 5: आउटपुट प्रस्तुत करें

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

अंतिम चरण में, हम कॉन्फ़िगर किए गए विकल्पों का उपयोग करके XPS आउटपुट प्रस्तुत करते हैं।

## निष्कर्ष

इस ट्यूटोरियल में, हमने आपको दिखाया है कि जावा के लिए Aspose.HTML का उपयोग करके XPS पेज आकार को कैसे समायोजित किया जाए। आप अपने XPS दस्तावेज़ों के आउटपुट आयामों को नियंत्रित कर सकते हैं, यह सुनिश्चित करते हुए कि वे आपकी विशिष्ट आवश्यकताओं को पूरा करते हैं। दिए गए कोड और चरणों के साथ, आप अपने जावा अनुप्रयोगों में इस सुविधा को आसानी से लागू कर सकते हैं।

 यदि आपके कोई प्रश्न हों या आपको और सहायता की आवश्यकता हो, तो कृपया निःसंकोच यहां जाएं[जावा के लिए Aspose.HTML दस्तावेज़](https://reference.aspose.com/html/java/) या मदद के लिए पूछें[एस्पोज फोरम](https://forum.aspose.com/).

## अक्सर पूछे जाने वाले प्रश्न

### प्रश्न 1: Java के लिए Aspose.HTML क्या है?

A1: Aspose.HTML for Java एक जावा लाइब्रेरी है जो डेवलपर्स को HTML दस्तावेज़ों को विभिन्न प्रारूपों, जैसे XPS, PDF और छवियों में बदलने और परिवर्तित करने की अनुमति देती है।

### प्रश्न 2: मैं Java के लिए Aspose.HTML कहां से डाउनलोड कर सकता हूं?

 A2: आप Aspose.HTML for Java लाइब्रेरी को यहां से डाउनलोड कर सकते हैं[इस लिंक](https://releases.aspose.com/html/java/).

### प्रश्न 3: क्या Java के लिए Aspose.HTML का निःशुल्क परीक्षण उपलब्ध है?

 A3: हाँ, आप Java के लिए Aspose.HTML का निःशुल्क परीक्षण प्राप्त कर सकते हैं[यहाँ](https://releases.aspose.com/).

### प्रश्न 4: मैं Java के लिए Aspose.HTML हेतु अस्थायी लाइसेंस कैसे प्राप्त कर सकता हूं?

 A4: Java के लिए Aspose.HTML हेतु अस्थायी लाइसेंस प्राप्त करने के लिए, यहां जाएं[यह पृष्ठ](https://purchase.aspose.com/temporary-license/).

### प्रश्न 5: क्या मुझे Java के लिए Aspose.HTML का समर्थन मिल सकता है?

 A5: हाँ, आप Aspose समुदाय से सहायता और समर्थन ले सकते हैं[एस्पोज फोरम](https://forum.aspose.com/).
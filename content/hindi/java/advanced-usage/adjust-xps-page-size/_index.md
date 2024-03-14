---
title: जावा के लिए Aspose.HTML के साथ XPS पृष्ठ आकार समायोजित करें
linktitle: एक्सपीएस पृष्ठ का आकार समायोजित करना
second_title: Aspose.HTML के साथ जावा HTML प्रोसेसिंग
description: जावा के लिए Aspose.HTML के साथ XPS पृष्ठ आकार को समायोजित करना सीखें। अपने XPS दस्तावेज़ों के आउटपुट आयामों को आसानी से नियंत्रित करें।
type: docs
weight: 16
url: /hi/java/advanced-usage/adjust-xps-page-size/
---

इस ट्यूटोरियल में, हम जावा के लिए Aspose.HTML का उपयोग करके XPS पेज आकार को समायोजित करने की प्रक्रिया में आपका मार्गदर्शन करेंगे। यह शक्तिशाली लाइब्रेरी आपको HTML दस्तावेज़ों में हेरफेर करने और उन्हें XPS सहित विभिन्न स्वरूपों में प्रस्तुत करने की अनुमति देती है। जब आपको अपने XPS दस्तावेज़ के आउटपुट आयामों को नियंत्रित करने की आवश्यकता हो तो पृष्ठ आकार को समायोजित करना आवश्यक है।

## आवश्यक शर्तें

शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित आवश्यक शर्तें हैं:

1. जावा विकास पर्यावरण: सुनिश्चित करें कि आपके सिस्टम पर जावा डेवलपमेंट किट (जेडीके) स्थापित है।

2.  जावा लाइब्रेरी के लिए Aspose.HTML: आपको अपने जावा प्रोजेक्ट में जावा लाइब्रेरी के लिए Aspose.HTML को डाउनलोड और शामिल करना होगा। आप पुस्तकालय पा सकते हैं[यहाँ](https://releases.aspose.com/html/java/).

3. इनपुट HTML फ़ाइल: एक HTML फ़ाइल तैयार करें जिसे आप प्रस्तुत करना चाहते हैं और XPS पृष्ठ आकार को समायोजित करना चाहते हैं। आप इस ट्यूटोरियल के लिए अपनी स्वयं की HTML फ़ाइल का उपयोग कर सकते हैं।

## पैकेज आयात करें

सबसे पहले, आपको Java के लिए Aspose.HTML के साथ काम करने के लिए आवश्यक पैकेज आयात करने होंगे। अपने जावा क्लास की शुरुआत में इन पैकेजों को शामिल करें:

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

 इस चरण में, हम आपकी HTML इनपुट फ़ाइल को a का उपयोग करके पढ़ते हैं`FileInputStream`.

## चरण 2: एक HTML दस्तावेज़ बनाएं और शैलियाँ सेट करें

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

 इस चरण में एक बनाना शामिल है`HTMLDocument` और इसमें शैलियाँ जोड़ रहा हूँ।

## चरण 3: एक्सपीएस रेंडरिंग विकल्प बनाएं

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

इस चरण में पृष्ठ का आकार सेट करना और यह निर्दिष्ट करना शामिल है कि इसे सबसे चौड़े पृष्ठ पर समायोजित किया जाए या नहीं।

## चरण 5: आउटपुट प्रस्तुत करें

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

अंतिम चरण में, हम कॉन्फ़िगर विकल्पों का उपयोग करके XPS आउटपुट प्रस्तुत करते हैं।

## निष्कर्ष

इस ट्यूटोरियल में, हमने आपको दिखाया है कि जावा के लिए Aspose.HTML का उपयोग करके XPS पेज का आकार कैसे समायोजित करें। आप अपने XPS दस्तावेज़ों के आउटपुट आयामों को नियंत्रित कर सकते हैं, यह सुनिश्चित करते हुए कि वे आपकी विशिष्ट आवश्यकताओं को पूरा करते हैं। दिए गए कोड और चरणों के साथ, आप इस सुविधा को अपने जावा अनुप्रयोगों में आसानी से लागू कर सकते हैं।

 यदि आपके कोई प्रश्न हैं या अतिरिक्त सहायता की आवश्यकता है, तो बेझिझक यहाँ जाएँ[जावा दस्तावेज़ीकरण के लिए Aspose.HTML](https://reference.aspose.com/html/java/) या पर मदद मांगें[एस्पोज़ फोरम](https://forum.aspose.com/).

## अक्सर पूछे जाने वाले प्रश्न

### Q1: जावा के लिए Aspose.HTML क्या है?

A1: जावा के लिए Aspose.HTML एक जावा लाइब्रेरी है जो डेवलपर्स को HTML दस्तावेज़ों में हेरफेर करने और उन्हें XPS, PDF और छवियों जैसे विभिन्न प्रारूपों में परिवर्तित करने की अनुमति देती है।

### Q2: मैं जावा के लिए Aspose.HTML कहां से डाउनलोड कर सकता हूं?

 A2: आप जावा लाइब्रेरी के लिए Aspose.HTML डाउनलोड कर सकते हैं[इस लिंक](https://releases.aspose.com/html/java/).

### Q3: क्या जावा के लिए Aspose.HTML का निःशुल्क परीक्षण उपलब्ध है?

 उ3: हाँ, आप जावा के लिए Aspose.HTML का निःशुल्क परीक्षण प्राप्त कर सकते हैं[यहाँ](https://releases.aspose.com/).

### Q4: मैं जावा के लिए Aspose.HTML के लिए अस्थायी लाइसेंस कैसे प्राप्त कर सकता हूं?

 A4: जावा के लिए Aspose.HTML का अस्थायी लाइसेंस प्राप्त करने के लिए, यहां जाएं[यह पृष्ठ](https://purchase.aspose.com/temporary-license/).

### Q5: क्या मुझे जावा के लिए Aspose.HTML का समर्थन मिल सकता है?

 A5: हां, आप Aspose समुदाय से सहायता और समर्थन मांग सकते हैं[एस्पोज़ फोरम](https://forum.aspose.com/).
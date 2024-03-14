---
title: जावा के लिए Aspose.HTML के साथ पीडीएफ पेज का आकार समायोजित करें
linktitle: पीडीएफ पेज का आकार समायोजित करना
second_title: Aspose.HTML के साथ जावा HTML प्रोसेसिंग
description: जानें कि जावा के लिए Aspose.HTML के साथ पीडीएफ पेज का आकार कैसे समायोजित करें। HTML से आसानी से उच्च-गुणवत्ता वाली PDF बनाएँ। पृष्ठ आयामों को प्रभावी ढंग से नियंत्रित करें.
type: docs
weight: 15
url: /hi/java/advanced-usage/adjust-pdf-page-size/
---

आज के डिजिटल युग में, HTML सामग्री से उच्च गुणवत्ता वाली पीडीएफ़ बनाने की आवश्यकता बढ़ रही है। जावा के लिए Aspose.HTML एक शक्तिशाली जावा लाइब्रेरी है जो आपको HTML दस्तावेज़ों को आसानी से पीडीएफ प्रारूप में परिवर्तित करने की अनुमति देती है। इस ट्यूटोरियल में, हम जावा के लिए Aspose.HTML का उपयोग करके HTML को पीडीएफ में परिवर्तित करते समय पृष्ठ आकार को समायोजित करने पर ध्यान केंद्रित करेंगे।

## आवश्यक शर्तें

शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित आवश्यक शर्तें हैं:

- जावा विकास पर्यावरण: सुनिश्चित करें कि आपके सिस्टम पर जावा डेवलपमेंट किट (जेडीके) स्थापित है।
-  जावा के लिए Aspose.HTML: आपको वेबसाइट से Java के लिए Aspose.HTML को डाउनलोड और इंस्टॉल करना होगा[यहाँ](https://releases.aspose.com/html/java/).
- HTML दस्तावेज़: आपके पास रूपांतरण के लिए एक HTML दस्तावेज़ तैयार होना चाहिए। यदि नहीं, तो एक बनाएं या मौजूदा HTML फ़ाइल का उपयोग करें।

## पैकेज आयात करें

आरंभ करने के लिए, आपको जावा के लिए Aspose.HTML के साथ काम करने के लिए आवश्यक पैकेज आयात करने की आवश्यकता है। निम्नलिखित कोड स्निपेट दर्शाता है कि यह कैसे करना है:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

अब जब आपके पास आवश्यक शर्तें मौजूद हैं और आपने आवश्यक पैकेज आयात कर लिए हैं, तो आइए पीडीएफ पेज आकार को समायोजित करने की प्रक्रिया को कई चरणों में विभाजित करें:

## चरण 1: HTML सामग्री पढ़ना

सबसे पहले, आपको उस HTML सामग्री को पढ़ना होगा जिसे आप पीडीएफ में कनवर्ट करना चाहते हैं। इस उदाहरण में, हम "FirstFile.html" नामक फ़ाइल से HTML पढ़ेंगे।

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## चरण 2: HTML सामग्री लिखना

इसके बाद, आप HTML सामग्री को "FirstFileOut.html" नामक फ़ाइल में लिखेंगे।

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // यहां कस्टम HTML शैलियाँ या सामग्री जोड़ें
    String style = "<style>\n" +
                   ".st\n" +
                   "{\n" +
                   "color:\n" +
                   "green;\n" +
                   "}\n" +
                   "</style >\n" +
                   "<div id = id1 > Aspose.Html rendering Text in Black Color</div >\n" +
                   "<div id = id2 class='' st '' > Aspose.Html rendering Text in Green Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: blue;' > Aspose.Html rendering Text in Blue Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: red;' ><font face = 'Arial' > Aspose.Html rendering Text in Red\n" +
                   "Color</font ></div >\n";
    fileOutputStream.write(style.getBytes(java.nio.charset.StandardCharsets.UTF_8));
}
```

## चरण 3: HTML को पीडीएफ में प्रस्तुत करना

अब, आप HTML सामग्री को एक पीडीएफ फ़ाइल में प्रस्तुत करेंगे। हम दो परिदृश्यों को कवर करेंगे: एक जहां पृष्ठ का आकार सामग्री की चौड़ाई के अनुसार समायोजित नहीं किया जाता है, और दूसरा जहां इसे समायोजित किया जाता है।

### पृष्ठ का आकार समायोजित नहीं किया गया

इस परिदृश्य में, पृष्ठ का आकार एक निश्चित चौड़ाई और ऊंचाई पर सेट किया गया है, जो इन आयामों से अधिक होने पर सामग्री को क्रॉप कर सकता है।

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// HTML फ़ाइल से HTMLDocument इंस्टेंस बनाएं
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// पीडीएफ रेंडरिंग विकल्प सेट करें
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//आउटपुट प्रस्तुत करें
pdf_renderer.render(device, html_document);
```

### पृष्ठ का आकार सामग्री की चौड़ाई के अनुसार समायोजित किया गया

इस परिदृश्य में, पृष्ठ का आकार सामग्री की चौड़ाई के अनुसार समायोजित किया जाता है।

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//आउटपुट प्रस्तुत करें
pdf_renderer.render(device, html_document);
```

## निष्कर्ष

इस ट्यूटोरियल में, हमने यह पता लगाया है कि जावा के लिए Aspose.HTML का उपयोग करके HTML को पीडीएफ में परिवर्तित करते समय पीडीएफ पेज का आकार कैसे समायोजित किया जाए। आपने आवश्यक शर्तें सीख ली हैं, आवश्यक पैकेज आयात कर लिए हैं और इस कार्य को प्राप्त करने के लिए चरण-दर-चरण मार्गदर्शिका का पालन किया है। जावा के लिए Aspose.HTML के साथ, आप आसानी से अपने जेनरेट किए गए पीडीएफ के पृष्ठ आकार को नियंत्रित कर सकते हैं, यह सुनिश्चित करते हुए कि आपकी सामग्री इच्छित रूप में प्रदर्शित की गई है।

 अपनी विशिष्ट आवश्यकताओं को पूरा करने के लिए विभिन्न पृष्ठ आकारों और सेटिंग्स के साथ प्रयोग करने में संकोच न करें। यदि आपको कोई समस्या आती है या आपके कोई और प्रश्न हैं, तो सहायता लेने में संकोच न करें[जावा दस्तावेज़ीकरण के लिए Aspose.HTML](https://reference.aspose.com/html/java/) या[Aspose समर्थन मंच](https://forum.aspose.com/).

## अक्सर पूछे जाने वाले प्रश्न

### Q1: जावा के लिए Aspose.HTML क्या है?

A1: जावा के लिए Aspose.HTML एक जावा लाइब्रेरी है जो आपको HTML दस्तावेज़ों के साथ काम करने, हेरफेर करने, परिवर्तित करने और उन्हें पीडीएफ सहित विभिन्न प्रारूपों में प्रस्तुत करने की अनुमति देती है।

### Q2: जावा के लिए Aspose.HTML के साथ HTML को पीडीएफ में परिवर्तित करते समय मैं पीडीएफ पेज का आकार कैसे समायोजित कर सकता हूं?

 A2: आप इसका उपयोग करके पीडीएफ पेज का आकार समायोजित कर सकते हैं`PageSetup` क्लास और सेटिंग`AdjustToWidestPage` संपत्ति को`true` या `झूठा, आपकी आवश्यकताओं पर निर्भर करता है।

### Q3: क्या मैं HTML सामग्री को पीडीएफ में बदलने से पहले उसकी शैली को अनुकूलित कर सकता हूँ?

उ3: हाँ, आप अपनी HTML सामग्री को पीडीएफ में बदलने से पहले उसमें सीएसएस और HTML तत्व जोड़कर स्टाइल को अनुकूलित कर सकते हैं, जैसा कि ट्यूटोरियल में दिखाया गया है।

### Q4: मैं जावा के लिए Aspose.HTML के लिए दस्तावेज़ कहां पा सकता हूं?

 A4: आप दस्तावेज़ का संदर्भ ले सकते हैं[यहाँ](https://reference.aspose.com/html/java/) व्यापक जानकारी और उदाहरणों के लिए।

### Q5: क्या Java के लिए Aspose.HTML का निःशुल्क परीक्षण उपलब्ध है?

 A5: हां, आप जावा के लिए Aspose.HTML के निःशुल्क परीक्षण तक पहुंच सकते हैं[इस लिंक](https://releases.aspose.com/).
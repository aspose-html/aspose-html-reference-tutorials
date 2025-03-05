---
title: Java के लिए Aspose.HTML के साथ PDF पृष्ठ का आकार समायोजित करें
linktitle: पीडीएफ पृष्ठ का आकार समायोजित करना
second_title: Aspose.HTML के साथ जावा HTML प्रसंस्करण
description: Java के लिए Aspose.HTML के साथ PDF पेज का आकार समायोजित करना सीखें। HTML से आसानी से उच्च-गुणवत्ता वाली PDF बनाएँ। पेज के आयामों को प्रभावी ढंग से नियंत्रित करें।
type: docs
weight: 15
url: /hi/java/advanced-usage/adjust-pdf-page-size/
---

आज के डिजिटल युग में, HTML सामग्री से उच्च-गुणवत्ता वाली PDF बनाने की आवश्यकता बढ़ रही है। Aspose.HTML for Java एक शक्तिशाली Java लाइब्रेरी है जो आपको HTML दस्तावेज़ों को आसानी से PDF प्रारूप में बदलने की अनुमति देती है। इस ट्यूटोरियल में, हम Aspose.HTML for Java का उपयोग करके HTML को PDF में परिवर्तित करते समय पृष्ठ के आकार को समायोजित करने पर ध्यान केंद्रित करेंगे।

## आवश्यक शर्तें

आरंभ करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ मौजूद हैं:

- जावा डेवलपमेंट एनवायरनमेंट: सुनिश्चित करें कि आपके सिस्टम पर जावा डेवलपमेंट किट (JDK) स्थापित है।
-  Aspose.HTML for Java: आपको वेबसाइट से Aspose.HTML for Java डाउनलोड और इंस्टॉल करना होगा[यहाँ](https://releases.aspose.com/html/java/).
- HTML दस्तावेज़: आपके पास रूपांतरण के लिए एक HTML दस्तावेज़ तैयार होना चाहिए। यदि नहीं, तो एक बनाएं या किसी मौजूदा HTML फ़ाइल का उपयोग करें।

## पैकेज आयात करें

आरंभ करने के लिए, आपको Aspose.HTML for Java के साथ काम करने के लिए आवश्यक पैकेज आयात करने होंगे। निम्न कोड स्निपेट यह दर्शाता है कि यह कैसे करना है:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

अब जब आपके पास आवश्यक शर्तें हैं और आपने आवश्यक पैकेज आयात कर लिए हैं, तो आइए पीडीएफ पृष्ठ आकार को समायोजित करने की प्रक्रिया को कई चरणों में विभाजित करें:

## चरण 1: HTML सामग्री पढ़ना

सबसे पहले, आपको उस HTML सामग्री को पढ़ना होगा जिसे आप PDF में बदलना चाहते हैं। इस उदाहरण में, हम "FirstFile.html" नामक फ़ाइल से HTML पढ़ेंगे।

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

## चरण 3: HTML को PDF में बदलना

अब, आप HTML सामग्री को PDF फ़ाइल में प्रस्तुत करेंगे। हम दो परिदृश्यों को कवर करेंगे: एक जहाँ पृष्ठ का आकार सामग्री की चौड़ाई के अनुसार समायोजित नहीं किया गया है, और दूसरा जहाँ इसे समायोजित किया गया है।

### पृष्ठ आकार समायोजित नहीं किया गया

इस परिदृश्य में, पृष्ठ का आकार एक निश्चित चौड़ाई और ऊंचाई पर सेट किया जाता है, जो इन आयामों से अधिक होने पर सामग्री को काट सकता है।

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// HTML फ़ाइल से HTMLDocument इंस्टेंस बनाएँ
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// PDF रेंडरिंग विकल्प सेट करें
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

### पृष्ठ आकार को सामग्री की चौड़ाई के अनुसार समायोजित किया गया

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

इस ट्यूटोरियल में, हमने यह पता लगाया है कि Aspose.HTML for Java का उपयोग करके HTML को PDF में परिवर्तित करते समय PDF पृष्ठ आकार को कैसे समायोजित किया जाए। आपने आवश्यक शर्तें सीख ली हैं, आवश्यक पैकेज आयात कर लिए हैं, और इस कार्य को पूरा करने के लिए चरण-दर-चरण मार्गदर्शिका का पालन किया है। Aspose.HTML for Java के साथ, आप अपने द्वारा बनाए गए PDF के पृष्ठ आकार को आसानी से नियंत्रित कर सकते हैं, यह सुनिश्चित करते हुए कि आपकी सामग्री इच्छित रूप से प्रदर्शित हो।

 अपनी विशिष्ट आवश्यकताओं को पूरा करने के लिए अलग-अलग पेज साइज़ और सेटिंग के साथ प्रयोग करने के लिए स्वतंत्र महसूस करें। यदि आपको कोई समस्या आती है या आपके पास और प्रश्न हैं, तो सहायता लेने में संकोच न करें[जावा के लिए Aspose.HTML दस्तावेज़](https://reference.aspose.com/html/java/) या[Aspose समर्थन मंच](https://forum.aspose.com/).

## अक्सर पूछे जाने वाले प्रश्न

### प्रश्न 1: Java के लिए Aspose.HTML क्या है?

A1: Aspose.HTML for Java एक जावा लाइब्रेरी है जो आपको HTML दस्तावेज़ों के साथ काम करने, उन्हें हेरफेर करने, परिवर्तित करने और उन्हें PDF सहित विभिन्न प्रारूपों में प्रस्तुत करने की अनुमति देती है।

### प्रश्न 2: मैं Java के लिए Aspose.HTML के साथ HTML को PDF में परिवर्तित करते समय PDF पृष्ठ का आकार कैसे समायोजित कर सकता हूँ?

 A2: आप PDF पृष्ठ का आकार समायोजित कर सकते हैं`PageSetup` वर्ग और सेटिंग`AdjustToWidestPage` संपत्ति को`true` या `झूठ, आपकी आवश्यकताओं पर निर्भर करता है।

### प्रश्न 3: क्या मैं HTML सामग्री को PDF में परिवर्तित करने से पहले उसकी स्टाइलिंग को अनुकूलित कर सकता हूँ?

A3: हां, आप अपनी HTML सामग्री को PDF में परिवर्तित करने से पहले उसमें CSS और HTML तत्व जोड़कर स्टाइलिंग को अनुकूलित कर सकते हैं, जैसा कि ट्यूटोरियल में दिखाया गया है।

### प्रश्न 4: मैं Java के लिए Aspose.HTML का दस्तावेज़ कहां पा सकता हूं?

 A4: आप दस्तावेज़ देख सकते हैं[यहाँ](https://reference.aspose.com/html/java/) विस्तृत जानकारी और उदाहरण के लिए.

### प्रश्न 5: क्या Java के लिए Aspose.HTML का निःशुल्क परीक्षण उपलब्ध है?

 A5: हाँ, आप Java के लिए Aspose.HTML का निःशुल्क परीक्षण प्राप्त कर सकते हैं[इस लिंक](https://releases.aspose.com/).
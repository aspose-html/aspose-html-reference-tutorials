---
category: general
date: 2026-03-26
description: Aspose.HTML for Java का उपयोग करके HTML से कस्टम आकार का PDF बनाएं। कुछ
  ही चरणों में HTML को PDF में बदलना और PDF पेज साइज सेट करना सीखें।
draft: false
keywords:
- create pdf custom size
- convert html to pdf
- change pdf page size
- generate pdf from html
- set pdf page size
language: hi
og_description: Aspose के साथ HTML से कस्टम आकार का PDF बनाएं। यह गाइड आपको दिखाता
  है कि HTML को PDF में कैसे बदलें, PDF पेज का आकार कैसे बदलें, और PDF पेज का आकार
  आसानी से सेट करें।
og_title: PDF कस्टम साइज बनाएं – HTML को PDF में बदलने के लिए त्वरित गाइड
tags:
- aspose
- java
- pdf
- html
title: PDF कस्टम आकार बनाएं – Aspose के साथ HTML को PDF में बदलें
url: /hi/java/conversion-html-to-other-formats/create-pdf-custom-size-convert-html-to-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF कस्टम साइज बनाएं – Aspose के साथ HTML को PDF में बदलें

क्या आपको कभी HTML फ़ाइल से **PDF कस्टम साइज** बनाने की ज़रूरत पड़ी है? इस ट्यूटोरियल में हम आपको दिखाएंगे कि कैसे **HTML को PDF** में बदलें और Aspose.HTML for Java का उपयोग करके PDF पेज साइज सेट करें।  

यदि आप इनवॉइस, रिपोर्ट या ई‑बुक बना रहे हैं, तो सटीक पेज डाइमेंशन होना बहुत महत्वपूर्ण है—अन्यथा आपका लेआउट ऑफ‑सेंटर दिखेगा या कट जाएगा।  

हम हर कदम को विस्तार से बताएँगे, स्रोत HTML को लोड करने से लेकर मार्जिन समायोजित करने तक, और अंत में तैयार‑उपयोग PDF देंगे। कोई अस्पष्ट संदर्भ नहीं, सिर्फ एक पूर्ण, चलाने योग्य उदाहरण जिसे आप आज ही कॉपी‑पेस्ट कर सकते हैं।

## आपको क्या चाहिए

- **Java 17** (या कोई भी नया JDK)।  
- **Aspose.HTML for Java** JARs – आप नवीनतम संस्करण Maven रिपॉजिटरी या Aspose वेबसाइट से प्राप्त कर सकते हैं।  
- एक साधारण `input.html` फ़ाइल जिसे आप नियंत्रित फ़ोल्डर में रखें।  
- आपकी पसंद का IDE या टेक्स्ट एडिटर; मैं आमतौर पर IntelliJ IDEA में कोड करता हूँ, लेकिन Eclipse भी ठीक काम करता है।

इन पूर्वापेक्षाओं को रखने से आप बीच में “class not found” त्रुटियों का सामना नहीं करेंगे।  

अब, चलिए शुरू करते हैं।

![PDF कस्टम साइज बनाने का उदाहरण](/images/create-pdf-custom-size.png "स्क्रीनशॉट जिसमें कस्टम पेज साइज और मार्जिन के साथ जनरेट किया गया PDF दिखाया गया है – create pdf custom size")

## PDF कस्टम साइज बनाना – मुख्य चरण

नीचे वह पूरा Java प्रोग्राम है जो आपको मिलेगा। इसे `ConvertHtmlToPdfCustomPage.java` नामक फ़ाइल में कॉपी करने में संकोच न करें और Aspose डिपेंडेंसीज़ को प्रोजेक्ट में जोड़ने के बाद इसे चलाएँ।

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.PdfConversionOptions;
import com.aspose.html.saving.PageSize;
import com.aspose.html.saving.Margin;

public class ConvertHtmlToPdfCustomPage {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the source HTML document
        HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/input.html");

        // Step 2: Set up PDF conversion options
        PdfConversionOptions pdfOptions = new PdfConversionOptions();
        pdfOptions.setPageSize(PageSize.A4); // Choose page size (A4, Letter, etc.)
        pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Portrait); // Portrait or Landscape
        pdfOptions.setMargins(new Margin(20, 20, 20, 20)); // Margins: left, top, right, bottom (points)

        // Step 3: Convert the HTML document to a PDF file with the custom settings
        Converter.convertHTML(htmlDoc, "YOUR_DIRECTORY/custom_page.pdf", pdfOptions);

        // Step 4: Inform the user that the PDF has been created
        System.out.println("PDF generated with custom page size and margins.");
    }
}
```

### चरण 1 – HTML को PDF में बदलें: दस्तावेज़ लोड करना

पहला काम हम **HTML लोड** करना है जिसे हम PDF में बदलना चाहते हैं।  
`HTMLDocument` फ़ाइल को पढ़ता है, रिलेटिव लिंक को हल करता है, और एक DOM बनाता है जिसे Aspose रेंडर कर सकता है।  

> **यह क्यों महत्वपूर्ण है:** यदि HTML में CSS या इमेजेज़ का रेफ़रेंस है, तो Aspose उन्हें फ़ाइल पाथ के सापेक्ष फ़ेच करेगा। एक एब्सॉल्यूट पाथ (`YOUR_DIRECTORY/input.html`) उपयोग करने से “file not found” जैसी आश्चर्यजनक त्रुटियों से बचा जा सकता है।

### चरण 2 – PDF पेज साइज बदलें: विकल्प कॉन्फ़िगर करना

यहाँ हम एक `PdfConversionOptions` ऑब्जेक्ट बनाते हैं।  
- `setPageSize(PageSize.A4)` Aspose को मानक A4 डाइमेंशन (210 × 297 mm) उपयोग करने के लिए बताता है।  
- `setPageOrientation(...)` पेज को लैंडस्केप में बदलता है यदि आपको आवश्यकता हो।  
- `setMargins(new Margin(20, 20, 20, 20))` हर पक्ष पर 20‑पॉइंट मार्जिन देता है।  

आप `PageSize.A4` को `PageSize.LETTER` से बदल सकते हैं या यहाँ तक कि **कस्टम साइज** के लिए `SizeF` ऑब्जेक्ट पास कर सकते हैं, उदाहरण के लिए:

```java
pdfOptions.setPageSize(new SizeF(500, 800)); // width, height in points
```

> **प्रो टिप:** एक पॉइंट 1/72 इंच के बराबर होता है। यदि आप मिलीमीटर में सोचते हैं, तो पॉइंट पाने के लिए 2.83465 से गुणा करें।

### चरण 3 – HTML से PDF जनरेट करें: कन्वर्ज़न चलाना

`Converter.convertHTML` मुख्य कार्य करता है। यह लोड किए गए `HTMLDocument`, आउटपुट पाथ, और हमने अभी कॉन्फ़िगर किए गए विकल्पों को लेता है।  

यदि आप सामग्री के आधार पर **PDF पेज साइज** को डायनामिक रूप से सेट करना चाहते हैं, तो आप इस चरण से पहले आवश्यक डाइमेंशन की गणना कर सकते हैं और `pdfOptions` को उसी अनुसार समायोजित कर सकते हैं।

### चरण 4 – परिणाम सत्यापित करें

`System.out.println` लाइन वैकल्पिक है, लेकिन यह कंसोल से प्रोग्राम चलाने पर त्वरित फीडबैक देती है। निष्पादन के बाद, `custom_page.pdf` खोलें – आपको एक A4 पोर्ट्रेट PDF दिखना चाहिए जिसमें समान 20‑पॉइंट मार्जिन हो, बिल्कुल जैसा हमने निर्दिष्ट किया था।

## HTML को PDF में बदलें – सामान्य विविधताएँ

### फ़ाइल पाथ के बजाय स्ट्रीम का उपयोग

कभी-कभी आपके पास वास्तविक फ़ाइल नहीं होती; शायद HTML डेटाबेस या API से आती है। ऐसे में स्ट्रिंग को `ByteArrayInputStream` में रैप करें:

```java
String htmlContent = "<html><body><h1>Hello, PDF!</h1></body></html>";
HTMLDocument htmlDoc = new HTMLDocument(
        new ByteArrayInputStream(htmlContent.getBytes(StandardCharsets.UTF_8)),
        "http://example.com/");
```

दूसरा आर्ग्यूमेंट रिलेटिव रिसोर्सेज़ को हल करने के लिए बेस URL है।

### पेज ओरिएंटेशन बदलना

यदि आपका रिपोर्ट चौड़ा है, तो लैंडस्केप में स्विच करें:

```java
pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Landscape);
```

### मार्जिन का फाइन‑ट्यूनिंग

मार्जिन फ्लोटिंग‑पॉइंट वैल्यू स्वीकार करता है, इसलिए आप 0.5 pt सेट कर सकते हैं एक बहुत पतली बॉर्डर के लिए:

```java
pdfOptions.setMargins(new Margin(5.5, 10.2, 5.5, 10.2));
```

### बड़े HTML फ़ाइलों को संभालना

बड़े दस्तावेज़ों के लिए, **मेमोरी‑एफ़िशिएंट स्ट्रीमिंग** सक्षम करने पर विचार करें:

```java
pdfOptions.setUseMemoryCache(true);
```

यह Aspose को मध्यवर्ती डेटा को अस्थायी फ़ाइलों में लिखने को कहता है, बजाय सभी डेटा RAM में रखने के।

## PDF पेज साइज सेट करना – किनारे के केस और संभावित समस्याएँ

- **Missing Fonts:** यदि आपका HTML सर्वर पर स्थापित नहीं किए गए कस्टम फ़ॉन्ट का उपयोग करता है, तो PDF डिफ़ॉल्ट फ़ॉन्ट पर फ़ॉल बैक हो जाएगा। फ़ॉन्ट को एम्बेड करने के लिए `pdfOptions.getFontEmbeddingMode().setEmbeddingMode(EmbeddingMode.Always);` का उपयोग करें।  
- **Image Scaling:** हाई‑रेज़ोल्यूशन इमेजेज़ PDF को बड़ा बना सकते हैं। गुणवत्ता बनाए रखते हुए डाउनस्केल करने के लिए `pdfOptions.setImageResolution(150);` उपयोग करें।  
- **CSS Compatibility:** सभी CSS प्रॉपर्टीज़ पूरी तरह सपोर्टेड नहीं हैं। मानक लेआउट तकनीकों का उपयोग करें (flexbox काम करता है, लेकिन grid में कुछ गड़बड़ियां हो सकती हैं)।  
- **Path Permissions:** सुनिश्चित करें कि प्रोसेस को `YOUR_DIRECTORY` में लिखने की अनुमति है। अन्यथा, `IOException` फेंका जाएगा।

## अपेक्षित आउटपुट

प्रोग्राम चलाने से एक PDF बनता है जो इस तरह दिखता है (संकल्पनात्मक चित्र):

```
+---------------------------------------------------+
|                     Header                        |
|                                                   |
|   (HTML rendered content goes here)               |
|                                                   |
|                     Footer                        |
+---------------------------------------------------+
```

- पेज साइज: **A4** (210 × 297 mm)।  
- ओरिएंटेशन: **Portrait**।  
- मार्जिन: प्रत्येक पक्ष पर **20 pt**।  

फ़ाइल को किसी भी PDF व्यूअर (Adobe Reader, Chrome, आदि) से खोलें ताकि पुष्टि हो सके।

## समापन

अब आप जानते हैं कि Aspose.HTML for Java का उपयोग करके HTML स्रोत से **PDF कस्टम साइज** कैसे बनाते हैं। ट्यूटोरियल ने पूरी पाइपलाइन को कवर किया: **HTML को PDF में बदलना**, **PDF पेज साइज बदलना**, **PDF पेज साइज सेट करना**, और **HTML से PDF जनरेट करना** कस्टम मार्जिन के साथ।  

बिना झिझक प्रयोग करें—`PageSize.LETTER` को लीगल साइज से बदलें, मार्जिन को समायोजित करें, या अपने फ़ॉन्ट एम्बेड करें। आगे आप **वॉटरमार्क जोड़ना**, **PDF एन्क्रिप्ट करना**, या **एकाधिक HTML फ़ाइलों को बैच‑प्रोसेस करना** का अन्वेषण कर सकते हैं। ये सभी विषय वही मूल अवधारणाओं पर आधारित हैं जो हमने अभी कवर किए।  

क्या आपके पास किसी विशेष किनारे के केस के बारे में प्रश्न है? नीचे टिप्पणी छोड़ें, मैं आपकी समस्या हल करने में मदद करूंगा। कोडिंग का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
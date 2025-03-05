---
title: EPUB से PDF में PDF सहेजने के विकल्प निर्दिष्ट करना
linktitle: EPUB से PDF में PDF सहेजने के विकल्प निर्दिष्ट करना
second_title: Aspose.HTML के साथ जावा HTML प्रसंस्करण
description: Aspose.HTML, एक शक्तिशाली HTML मैनिपुलेशन लाइब्रेरी का उपयोग करके जावा में EPUB को PDF में परिवर्तित करना सीखें।
type: docs
weight: 12
url: /hi/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
---

## परिचय

Aspose.HTML for Java HTML और EPUB दस्तावेज़ों के साथ काम करने के लिए एक शक्तिशाली उपकरण है। इस चरण-दर-चरण मार्गदर्शिका में, हम आपको Aspose.HTML for Java का उपयोग करके EPUB फ़ाइल को PDF में बदलने की प्रक्रिया से परिचित कराएँगे। चाहे आप एक अनुभवी डेवलपर हों या अभी शुरुआत कर रहे हों, यह ट्यूटोरियल आपको इस कार्य को कुशलतापूर्वक करने के लिए आवश्यक ज्ञान और कौशल प्रदान करेगा।

## आवश्यक शर्तें

आरंभ करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ मौजूद हैं:

- जावा विकास वातावरण: आपके सिस्टम पर जावा विकास वातावरण स्थापित होना चाहिए।

-  Aspose.HTML for Java: Aspose.HTML for Java लाइब्रेरी डाउनलोड करें और इंस्टॉल करें। आप लाइब्रेरी और संबंधित दस्तावेज़ यहाँ पा सकते हैं[वेबसाइट](https://releases.aspose.com/html/java/).

- EPUB फ़ाइल: आपको एक EPUB फ़ाइल की आवश्यकता होगी जिसे आप PDF में बदलना चाहते हैं।

अब, आइए Java के लिए Aspose.HTML का उपयोग करके EPUB को PDF में परिवर्तित करने के लिए चरण-दर-चरण मार्गदर्शिका में गोता लगाएँ।

## चरण 1: EPUB फ़ाइल खोलें

 शुरू करने के लिए, पढ़ने के लिए एक मौजूदा EPUB फ़ाइल खोलें। आप एक का उपयोग कर सकते हैं`FileInputStream` इसे प्राप्त करने के लिए। इस चरण के लिए कोड यहां दिया गया है:

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // अगले चरणों के लिए आपका कोड यहां जाएगा।
}
```

## चरण 2: पीडीएफ सेव विकल्प निर्धारित करें

 इसका एक उदाहरण बनाएं`PdfSaveOptions` कस्टम पेज आकार और पृष्ठभूमि रंग के साथ। आप अपनी आवश्यकताओं के अनुसार पेज सेटअप कॉन्फ़िगर कर सकते हैं। यहाँ बताया गया है कि आप इसे कैसे कर सकते हैं:

```java
com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
anyPage.setSize(new com.aspose.html.drawing.Size(
    com.aspose.html.drawing.Length.fromPixels(3000),
    com.aspose.html.drawing.Length.fromPixels(1000))
);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
```

## चरण 3: EPUB को PDF में बदलें

 अब, कॉल करें`ConvertEPUB` EPUB फ़ाइल को PDF में बदलने की विधि। इनपुट स्ट्रीम, PDF सेव विकल्प और आउटपुट स्थान निर्दिष्ट करें। यह इस प्रकार किया जाता है:

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

बधाई हो! आपने Aspose.HTML for Java का उपयोग करके EPUB फ़ाइल को PDF में सफलतापूर्वक परिवर्तित कर लिया है। अब आप निर्दिष्ट आउटपुट स्थान पर परिवर्तित PDF फ़ाइल तक पहुँच सकते हैं।

## संपूर्ण स्रोत कोड
```java
Specifying PDF Save Options for EPUB to PDF
        // पढ़ने के लिए मौजूदा EPUB फ़ाइल खोलें.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // कस्टम पृष्ठ-आकार और पृष्ठभूमि-रंग के साथ PdfSaveOptions का एक उदाहरण बनाएं।
            com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
            com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
            com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
            anyPage.setSize(new com.aspose.html.drawing.Size(
                    com.aspose.html.drawing.Length.fromPixels(3000),
                    com.aspose.html.drawing.Length.fromPixels(1000))
            );
            pageSetup.setAnyPage(anyPage);
            options.setPageSetup(pageSetup);
            options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
            // EPUB को PDF में बदलने के लिए ConvertEPUB विधि को कॉल करें।
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```


## निष्कर्ष

इस ट्यूटोरियल में, हमने सीखा है कि EPUB फ़ाइलों को PDF फ़ॉर्मेट में बदलने के लिए Java के लिए Aspose.HTML का उपयोग कैसे करें। यह बहुमुखी लाइब्रेरी डेवलपर्स को दस्तावेज़ हेरफेर के लिए शक्तिशाली उपकरण प्रदान करती है। इस गाइड में बताए गए चरणों का पालन करके, आप अपने Java अनुप्रयोगों में EPUB से PDF रूपांतरण को सहजता से एकीकृत कर सकते हैं।

## अक्सर पूछे जाने वाले प्रश्न (एफएक्यू)

### क्या Aspose.HTML for Java एक निःशुल्क लाइब्रेरी है?
 Aspose.HTML for Java एक व्यावसायिक लाइब्रेरी है, लेकिन आप उनके यहां से निःशुल्क परीक्षण संस्करण प्राप्त कर सकते हैं[वेबसाइट](https://releases.aspose.com/).

### रूपांतरण के लिए कौन से EPUB प्रारूप समर्थित हैं?
Java के लिए Aspose.HTML विभिन्न EPUB प्रारूपों के रूपांतरण का समर्थन करता है, जो अधिकांश EPUB दस्तावेज़ों के साथ संगतता सुनिश्चित करता है।

### क्या मैं पीडीएफ आउटपुट को और अधिक अनुकूलित कर सकता हूं?
 हां, आप पृष्ठ सेटअप, पृष्ठभूमि रंग और अन्य सेटिंग्स को समायोजित करके पीडीएफ आउटपुट को अनुकूलित कर सकते हैं।`PdfSaveOptions`.

### क्या Java के लिए Aspose.HTML के परीक्षण संस्करण की कोई सीमाएँ हैं?
परीक्षण संस्करण में कुछ सीमाएँ हो सकती हैं, इसलिए विवरण के लिए दस्तावेज़ की जाँच करना अनुशंसित है।

### मैं Java के लिए Aspose.HTML का समर्थन कहां से प्राप्त कर सकता हूं?
आप अपने प्रश्नों के उत्तर पा सकते हैं और सहायता प्राप्त कर सकते हैं[Aspose.HTML फ़ोरम](https://forum.aspose.com/).

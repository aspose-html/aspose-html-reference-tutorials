---
date: 2026-05-30
description: जावा में Aspose.HTML के साथ EPUB को PDF में परिवर्तित करना सीखें, साथ
  ही कस्टम PDF पृष्ठ आकार और अन्य PDF सेव विकल्प सेट करते हुए।
keywords:
- custom pdf page size
- convert epub to pdf
- change pdf background color
- specify pdf page dimensions
- aspose.html java
linktitle: EPUB से PDF के लिए PDF सेव विकल्प निर्दिष्ट करना
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  headline: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  type: TechArticle
- description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  name: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  steps:
  - name: Open the EPUB File
    text: First, create a `FileInputStream` that points to your source `.epub`. Keeping
      the stream open until the conversion finishes prevents “blank page” errors.
  - name: Define PDF Save Options
    text: '`PdfSaveOptions` is Aspose.HTML''s configuration class that controls PDF
      output settings such as page size, background color, and margins. `Length.fromPixels`
      converts screen pixels to PDF points (1 point = 1/72 inch), allowing you to
      specify dimensions in familiar pixel units.'
  - name: Convert EPUB to PDF
    text: With the input stream and custom options ready, invoke the converter. The
      output PDF will be saved to the location you specify, preserving the exact page
      dimensions you defined. `PdfSaveOptions.setEnableParallelProcessing` is a method
      that enables parallel processing of pages during PDF conversion.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a commercial library, but you can obtain a free
      trial version from their [website](https://releases.aspose.com/).
    question: Is Aspose.HTML for Java a free library?
  - answer: Aspose.HTML for Java supports EPUB 2.0, EPUB 3.0, and EPUB 3.1, handling
      re‑flowable and fixed‑layout books with full CSS support.
    question: What EPUB formats are supported for conversion?
  - answer: Yes, you can customize the PDF output by adjusting the page setup, background
      color, compression level, and other settings in the `PdfSaveOptions`.
    question: Can I customize the PDF output further?
  - answer: The trial version may add a watermark to the first few pages and limits
      the maximum file size to 10 MB; purchase a license to remove these restrictions.
    question: Are there any limitations to the trial version of Aspose.HTML for Java?
  - answer: You can find answers to your questions and seek support on the [Aspose.HTML
      forum](https://forum.aspose.com/).
    question: Where can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: कस्टम PDF पृष्ठ आकार - EPUB से PDF के लिए PDF सेव विकल्प निर्दिष्ट करना
url: /hi/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# कस्टम PDF पेज आकार: EPUB से PDF के लिए PDF सेव विकल्प निर्दिष्ट करना

## परिचय

Aspose.HTML for Java EPUB को PDF में बदलना आसान बनाता है और आपको आउटपुट पर पूर्ण नियंत्रण देता है, जिसमें **कस्टम PDF पेज आकार** सेट करना शामिल है। इस चरण‑दर‑चरण गाइड में हम सब कुछ कवर करेंगे—पर्यावरण तैयार करने से लेकर `PdfSaveOptions` को इस तरह ट्यून करने तक कि उत्पन्न PDF आपके द्वारा आवश्यक सटीक पेज आयामों से मेल खाए। चाहे आप एक प्रकाशन पाइपलाइन, ई‑लर्निंग प्लेटफ़ॉर्म बना रहे हों, या सिर्फ दस्तावेज़ रूपांतरण को स्वचालित करना चाहते हों, यहाँ दी गई तकनीकें आपके लिए उपयोगी होंगी।

## त्वरित उत्तर
- **इस ट्यूटोरियल का मुख्य उद्देश्य क्या है?** एक EPUB फ़ाइल को PDF में बदलना जबकि कस्टम PDF पेज आकार लागू किया जाए।  
- **कौनसी लाइब्रेरी उपयोग की गई है?** Aspose.HTML for Java।  
- **क्या मुझे लाइसेंस की आवश्यकता है?** एक मुफ्त ट्रायल उपलब्ध है; उत्पादन के लिए एक व्यावसायिक लाइसेंस आवश्यक है।  
- **क्या मैं बैकग्राउंड रंग बदल सकता हूँ?** हाँ, `PdfSaveOptions` का उपयोग करके।  
- **क्या Java 8+ समर्थित है?** बिल्कुल—कोई भी आधुनिक Java रनटाइम काम करता है।

## कस्टम PDF पेज आकार क्या है?

कस्टम PDF पेज आकार आपको आउटपुट PDF के प्रत्येक पेज की सटीक चौड़ाई और ऊँचाई निर्धारित करने की अनुमति देता है, बजाय A4 या लेटर जैसे मानक आकारों पर निर्भर रहने के। आप आयामों को पॉइंट्स (1 पॉइंट = 1/72 इंच) में सेट कर सकते हैं या पिक्सेल से परिवर्तित कर सकते हैं, जिससे आपको अंतिम लेआउट पर पिक्सेल‑परफेक्ट नियंत्रण मिलता है। यह ई‑बुक्स, फ़्लायर्स, या किसी भी डिज़ाइन के लिए आदर्श है जिसे पूर्वनिर्धारित फ़ॉर्मेट से मेल खाना आवश्यक है, बिना मैन्युअल पोस्ट‑प्रोसेसिंग के।

## EPUB से PDF रूपांतरण के लिए Aspose.HTML का उपयोग क्यों करें?

Aspose.HTML दो लाइनों के कोड में EPUB को PDF में बदल देता है, जबकि जटिल लेआउट, एम्बेडेड फ़ॉन्ट्स, और हाई‑रेज़ोल्यूशन इमेजेज को संरक्षित रखता है। यह **50+ इनपुट और आउटपुट फ़ॉर्मेट** का समर्थन करता है, **2,000 पेज** तक के PDF को बिना पूरी फ़ाइल को मेमोरी में लोड किए रेंडर कर सकता है, और Windows, Linux, और macOS पर समान परिणाम देता है। लाइब्रेरी ग्रैन्यूलर PDF‑सेव विकल्प भी प्रदान करती है, जिससे आप पेज आकार, बैकग्राउंड रंग, मार्जिन, और कॉम्प्रेशन सेटिंग्स को Java से ही ट्यून कर सकते हैं।

## पूर्वापेक्षाएँ
- **Java विकास वातावरण:** JDK 8 या बाद का स्थापित और कॉन्फ़िगर किया हुआ।  
- **Aspose.HTML for Java:** नवीनतम JAR [वेबसाइट](https://releases.aspose.com/html/java/) से डाउनलोड करें।  
- **EPUB फ़ाइल:** वह `.epub` दस्तावेज़ जिसे आप बदलना चाहते हैं।  

अब जब सब तैयार है, चलिए वास्तविक रूपांतरण चरणों में डुबकी लगाते हैं।

## कस्टम पेज आकार के साथ EPUB को PDF में कैसे बदलें?

`FileInputStream` एक Java क्लास है जो फ़ाइल से कच्चे बाइट्स पढ़ती है।  
`PdfSaveOptions` Aspose.HTML की वह क्लास है जो PDF आउटपुट सेटिंग्स जैसे पेज आकार और बैकग्राउंड रंग को कॉन्फ़िगर करती है।  
`FileInputStream` से अपना EPUB लोड करें, `PdfSaveOptions` को सटीक पेज आयाम निर्दिष्ट करने के लिए कॉन्फ़िगर करें, और कनवर्टर को कॉल करें। नीचे दिया गया तीन‑चरणीय वर्कफ़्लो सामान्य ई‑बुक आकारों के लिए एक मिनट से कम समय में रूपांतरण करता है, और न्यूनतम कोड परिवर्तन के साथ बड़े संग्रहों के लिए स्केलेबल है।

### चरण 1: EPUB फ़ाइल खोलें

पहले, एक `FileInputStream` बनाएँ जो आपके स्रोत `.epub` की ओर इशारा करे। रूपांतरण समाप्त होने तक स्ट्रीम को खुला रखें ताकि “ब्लैंक पेज” त्रुटियों से बचा जा सके।

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

### चरण 2: PDF सेव विकल्प निर्धारित करें

`PdfSaveOptions` Aspose.HTML की कॉन्फ़िगरेशन क्लास है जो PDF आउटपुट सेटिंग्स जैसे पेज आकार, बैकग्राउंड रंग, और मार्जिन को नियंत्रित करती है।  
`Length.fromPixels` स्क्रीन पिक्सेल को PDF पॉइंट्स में बदलता है (1 पॉइंट = 1/72 इंच), जिससे आप परिचित पिक्सेल इकाइयों में आयाम निर्दिष्ट कर सकते हैं।

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

#### प्रो टिप:
- **Pixels vs. Points:** `Length.fromPixels` स्क्रीन पिक्सेल को PDF पॉइंट्स में बदलता है (1 पॉइंट = 1/72 इंच). उन मानों को चुनें जो आपके अंतिम प्रिंट आकार को दर्शाते हों।

### चरण 3: EPUB को PDF में बदलें

इनपुट स्ट्रीम और कस्टम विकल्प तैयार होने पर, कनवर्टर को कॉल करें। आउटपुट PDF उस स्थान पर सहेजा जाएगा जिसे आप निर्दिष्ट करेंगे, और यह आपके द्वारा परिभाषित सटीक पेज आयामों को संरक्षित रखेगा।

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

`PdfSaveOptions.setEnableParallelProcessing` एक मेथड है जो PDF रूपांतरण के दौरान पेजों की समानांतर प्रोसेसिंग को सक्षम करता है।

## पूरा स्रोत कोड

पूरा, चलाने योग्य उदाहरण ऊपर के तीन चरणों को एक ही Java क्लास में जोड़ता है। प्लेसहोल्डर पाथ को अपने फ़ाइल लोकेशन से बदलें।

```java
Specifying PDF Save Options for EPUB to PDF
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of the PdfSaveOptions with a custom page-size and a background-color.
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
            // Call the ConvertEPUB method to convert the EPUB to PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```

## सामान्य समस्याएँ और समाधान

| समस्या | कारण | समाधान |
|-------|-------|-----|
| **PDF पेज खाली हैं** | रूपांतरण से पहले इनपुट स्ट्रीम बंद हो गई | `try‑with‑resources` ब्लॉक को `convertEPUB` के बाद तक खुला रखें। |
| **गलत पेज आयाम** | ऐसे पिक्सेल उपयोग करना जो वांछित प्रिंट आकार से मेल नहीं खाते | इच्छित इंच को पॉइंट्स में बदलें (`1 inch = 72 points`) और फिर `Length.fromPixels` का उपयोग करके पिक्सेल में बदलें। |
| **फ़ॉन्ट गायब हैं** | फ़ॉन्ट EPUB में एम्बेड नहीं हैं | सुनिश्चित करें कि फ़ॉन्ट EPUB के अंदर पैकेज किए गए हैं या होस्ट मशीन पर इंस्टॉल किए गए हैं। |
| **बड़ी पुस्तकों पर प्रदर्शन धीमा होना** | हर पेज को क्रमिक रूप से रेंडर करना | `PdfSaveOptions.setEnableParallelProcessing(true)` के माध्यम से मल्टी‑थ्रेडेड रेंडरिंग सक्षम करें ताकि 500+ पेज वाले EPUBs की तेज़ प्रोसेसिंग हो सके। |

## अक्सर पूछे जाने वाले प्रश्न (FAQs)

**Q: क्या Aspose.HTML for Java एक मुफ्त लाइब्रेरी है?**  
A: Aspose.HTML for Java एक व्यावसायिक लाइब्रेरी है, लेकिन आप उनके [वेबसाइट](https://releases.aspose.com/) से मुफ्त ट्रायल संस्करण प्राप्त कर सकते हैं।

**Q: रूपांतरण के लिए कौनसे EPUB फ़ॉर्मेट समर्थित हैं?**  
A: Aspose.HTML for Java EPUB 2.0, EPUB 3.0, और EPUB 3.1 का समर्थन करता है, री‑फ़्लोएबल और फिक्स्ड‑लेआउट बुक्स को पूर्ण CSS समर्थन के साथ संभालता है।

**Q: क्या मैं PDF आउटपुट को और अधिक कस्टमाइज़ कर सकता हूँ?**  
A: हाँ, आप `PdfSaveOptions` में पेज सेटअप, बैकग्राउंड रंग, कॉम्प्रेशन लेवल, और अन्य सेटिंग्स को समायोजित करके PDF आउटपुट को कस्टमाइज़ कर सकते हैं।

**Q: Aspose.HTML for Java के ट्रायल संस्करण में कोई सीमाएँ हैं?**  
A: ट्रायल संस्करण पहले कुछ पेजों पर वॉटरमार्क जोड़ सकता है और अधिकतम फ़ाइल आकार को 10 MB तक सीमित कर सकता है; इन प्रतिबंधों को हटाने के लिए लाइसेंस खरीदें।

**Q: Aspose.HTML for Java के लिए समर्थन कहाँ प्राप्त कर सकता हूँ?**  
A: आप अपने प्रश्नों के उत्तर और समर्थन [Aspose.HTML फ़ोरम](https://forum.aspose.com/) पर पा सकते हैं।

---

**अंतिम अपडेट:** 2026-05-30  
**परीक्षित संस्करण:** Aspose.HTML for Java 24.11 (लेखन समय पर नवीनतम)  
**लेखक:** Aspose

## संबंधित ट्यूटोरियल

- [Aspose.HTML for Java के साथ PDF पेज आकार समायोजित करें](/html/java/advanced-usage/adjust-pdf-page-size/)
- [Java के साथ EPUB को PDF में कैसे बदलें – Aspose.HTML का उपयोग करके](/html/java/conversion-epub-to-image-and-pdf/convert-epub-to-pdf/)
- [Aspose.HTML for Java के साथ EPUB को PDF और इमेजेज में बदलें](/html/java/conversion-epub-to-image-and-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
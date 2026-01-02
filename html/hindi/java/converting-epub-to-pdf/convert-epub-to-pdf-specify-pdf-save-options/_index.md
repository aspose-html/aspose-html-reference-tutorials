---
date: 2026-01-02
description: Aspose.HTML का उपयोग करके जावा में EPUB को PDF में कैसे बदलें, साथ ही
  कस्टम PDF पेज आकार और अन्य PDF सहेजने के विकल्प सेट करें।
linktitle: Specifying PDF Save Options for EPUB to PDF
second_title: Java HTML Processing with Aspose.HTML
title: 'कस्टम PDF पेज आकार: EPUB से PDF के लिए PDF सहेजने के विकल्प निर्दिष्ट करना'
url: /hi/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# कस्टम PDF पेज साइज: EPUB से PDF के लिए PDF सेव ऑप्शन निर्दिष्ट करना

## परिचय

Aspose.HTML for Java EPUB को PDF में **कनवर्ट** करना आसान बनाता है और आपको आउटपुट पर पूर्ण नियंत्रण देता है, जिसमें **कस्टम PDF पेज साइज** सेट करना भी शामिल है। इस चरण‑दर‑चरण गाइड में हम सब कुछ कवर करेंगे—पर्यावरण तैयार करने से लेकर `PdfSaveOptions` को इस तरह ट्यून करने तक कि उत्पन्न PDF बिल्कुल वही पेज डाइमेंशन रखे जो आपको चाहिए। चाहे आप एक पब्लिशिंग पाइपलाइन, ई‑लर्निंग प्लेटफ़ॉर्म बना रहे हों, या सिर्फ़ दस्तावेज़ कनवर्ज़न को ऑटोमेट करना चाहते हों, यहाँ दी गई तकनीकें आपके लिए उपयोगी होंगी।

## त्वरित उत्तर
- **इस ट्यूटोरियल का मुख्य उद्देश्य क्या है?** एक EPUB फ़ाइल को PDF में कनवर्ट करना और कस्टम PDF पेज साइज लागू करना।  
- **कौन सी लाइब्रेरी उपयोग की गई है?** Aspose.HTML for Java।  
- **क्या लाइसेंस की आवश्यकता है?** एक फ्री ट्रायल उपलब्ध है; प्रोडक्शन के लिए कमर्शियल लाइसेंस आवश्यक है।  
- **क्या बैकग्राउंड रंग बदला जा सकता है?** हाँ, `PdfSaveOptions` का उपयोग करके।  
- **क्या Java 8+ समर्थित है?** बिल्कुल—कोई भी आधुनिक Java रनटाइम काम करता है।

## कस्टम PDF पेज साइज क्या है?

कस्टम PDF पेज साइज आपको आउटपुट PDF के प्रत्येक पेज की सटीक चौड़ाई और ऊँचाई परिभाषित करने की अनुमति देता है, बजाय इसके कि आप A4 या लेटर जैसे मानक साइज पर निर्भर रहें। यह विशेष रूप से ई‑बुक, फ़्लायर, या किसी भी स्थिति में उपयोगी है जहाँ विज़ुअल लेआउट को एक विशिष्ट डिज़ाइन से मिलाना आवश्यक हो।

## EPUB से PDF कनवर्ज़न के लिए Aspose.HTML क्यों उपयोग करें?

- **उच्च फिडेलिटी:** जटिल लेआउट, फ़ॉन्ट और इमेज को संरक्षित करता है।  
- **सूक्ष्म नियंत्रण:** `PdfSaveOptions` के माध्यम से पेज साइज, बैकग्राउंड, मार्जिन आदि को समायोजित करें।  
- **क्रॉस‑प्लेटफ़ॉर्म:** वही Java कोड Windows, Linux और macOS पर काम करता है।  
- **परफ़ॉर्मेंस:** तेज़ कनवर्ज़न के लिए ऑप्टिमाइज़्ड रेंडरिंग इंजन।

## पूर्वापेक्षाएँ

शुरू करने से पहले सुनिश्चित करें कि आपके पास हैं:

- **जावा डेवलपमेंट एनवायरनमेंट:** JDK 8 या बाद का संस्करण इंस्टॉल और कॉन्फ़िगर किया हुआ।  
- **Aspose.HTML for Java:** नवीनतम JAR [वेबसाइट](https://releases.aspose.com/html/java/) से डाउनलोड करें।  
- **EPUB फ़ाइल:** वह `.epub` दस्तावेज़ जिसे आप कनवर्ट करना चाहते हैं।  

अब जब सब तैयार है, चलिए वास्तविक कनवर्ज़न स्टेप्स में डुबकी लगाते हैं।

## चरण 1: EPUB फ़ाइल खोलें

सबसे पहले, हमें `FileInputStream` का उपयोग करके EPUB फ़ाइल खोलनी होगी। यह स्ट्रीम बाद में कनवर्टर को पास की जाएगी।

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

## चरण 2: PDF सेव ऑप्शन परिभाषित करें

यहीं पर हम **कस्टम PDF पेज साइज** और वैकल्पिक बैकग्राउंड रंग सेट करते हैं। पिक्सेल मानों को अपनी इच्छित डाइमेंशन के अनुसार समायोजित करें।

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

### प्रो टिप:
- **पिक्सेल बनाम पॉइंट्स:** `Length.fromPixels` स्क्रीन पिक्सेल को PDF पॉइंट्स में बदलता है (1 पॉइंट = 1/72 इंच)। ऐसे मान चुनें जो अंतिम प्रिंट साइज को दर्शाते हों।

## चरण 3: EPUB को PDF में कनवर्ट करें

इनपुट स्ट्रीम और कस्टम ऑप्शन तैयार होने के बाद, कनवर्टर को कॉल करें। आउटपुट PDF वह स्थान पर सेव होगा जिसे आप निर्दिष्ट करेंगे।

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

## पूर्ण स्रोत कोड

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
| **PDF पेज खाली हैं** | कनवर्ज़न से पहले इनपुट स्ट्रीम बंद हो गई | `try‑with‑resources` ब्लॉक को `convertEPUB` के बाद तक खुला रखें। |
| **पेज डाइमेंशन गलत हैं** | पिक्सेल मान इच्छित प्रिंट साइज से मेल नहीं खाते | इंच को पॉइंट्स (`1 inch = 72 points`) में बदलें और फिर `Length.fromPixels` से पिक्सेल में परिवर्तित करें। |
| **फ़ॉन्ट गायब हैं** | EPUB में फ़ॉन्ट एम्बेड नहीं हैं | सुनिश्चित करें कि फ़ॉन्ट EPUB के अंदर पैकेज्ड हों या होस्ट मशीन पर इंस्टॉल हों। |

## अक्सर पूछे जाने वाले प्रश्न (FAQs)

### क्या Aspose.HTML for Java एक मुफ्त लाइब्रेरी है?
Aspose.HTML for Java एक कमर्शियल लाइब्रेरी है, लेकिन आप उनकी [वेबसाइट](https://releases.aspose.com/) से फ्री ट्रायल संस्करण प्राप्त कर सकते हैं।

### कौन‑से EPUB फ़ॉर्मेट्स का समर्थन किया जाता है?
Aspose.HTML for Java विभिन्न EPUBॉर्मेट्स के कनवर्ज़न को सपोर्ट करता है, जिससे अधिकांश EPUB दस्तावेज़ संगत होते हैं।

### क्या मैं PDF आउटपुट को और अधिक कस्टमाइज़ कर सकता हूँ?
हाँ, आप `PdfSaveOptions` में पेज सेटअप, बैकग्राउंड रंग और अन्य सेटिंग्स को समायोजित करके PDF आउटपुट को और अधिक कस्टमाइज़ कर सकते हैं।

### Aspose.HTML for Java के ट्रायल संस्करण में कोई सीमाएँ हैं?
ट्रायल संस्करण में कुछ सीमाएँ हो सकती हैं; विस्तृत जानकारी के लिए दस्तावेज़ीकरण देखें।

### Aspose.HTML for Java के लिए सपोर्ट कहाँ मिल सकता है?
आप अपने प्रश्नों के उत्तर और सपोर्ट [Aspose.HTML फोरम](https://forum.aspose.com/) पर पा सकते हैं।

---

**अंतिम अपडेट:** 2026-01-02  
**टेस्टेड विथ:** Aspose.HTML for Java 24.11 (लेखन समय पर नवीनतम)  
**लेखक:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
---
date: 2025-12-01
description: Aspose.HTML for Java का उपयोग करके PDF पेज आकार को समायोजित करना, HTML
  को PDF के रूप में रेंडर करना और HTML से PDF बनाना सीखें। पेज के आयामों को आसानी
  से नियंत्रित करें।
linktitle: Adjusting PDF Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Aspose.HTML for Java के साथ PDF पृष्ठ आकार समायोजित करें
url: /hi/java/advanced-usage/adjust-pdf-page-size/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML for Java के साथ PDF पेज आकार समायोजित करें

HTML से PDF बनाना रिपोर्ट, इनवॉइस और ई‑बुक्स के लिए आम आवश्यकता है। जब आप **PDF पेज आकार समायोजित** करते हैं तो आप सुनिश्चित करते हैं कि अंतिम दस्तावेज़ आपके HTML लेआउट से मेल खाता हो। इस ट्यूटोरियल में आप सीखेंगे कि HTML को PDF के रूप में कैसे रेंडर करें, कस्टम आयाम कैसे सेट करें, और पेज को सबसे चौड़े कंटेंट के अनुसार स्वचालित रूप से विस्तारित करने को कैसे नियंत्रित करें। हम Aspose.HTML for Java का उपयोग करके एक पूर्ण, हैंड‑ऑन उदाहरण के माध्यम से चलेंगे।

## त्वरित उत्तर
- **“PDF पेज आकार समायोजित” का क्या अर्थ है?** यह आपको प्रत्येक PDF पेज की चौड़ाई और ऊँचाई निर्धारित करने या रेंडरर को सबसे चौड़े एलिमेंट के अनुसार स्वचालित रूप से फिट करने देता है।  
- **कौन सी लाइब्रेरी उपयोग की जाती है?** Aspose.HTML for Java (नवीनतम संस्करण)।  
- **क्या लाइसेंस की जरूरत है?** विकास के लिए फ्री ट्रायल चलती है; उत्पादन के लिए वाणिज्यिक लाइसेंस आवश्यक है।  
- **क्या आयाम प्रोग्रामेटिकली बदल सकते हैं?** हाँ – `PageSetup` और `AdjustToWidestPage` प्रॉपर्टी का उपयोग करें।  
- **क्या यह Java 8+ के साथ संगत है?** बिल्कुल – API किसी भी JDK 8 या उससे ऊपर के साथ काम करती है।

## “PDF पेज आकार समायोजित” क्या है?
PDF पेज आकार समायोजित करना मतलब HTML रेंडरर द्वारा निर्मित प्रत्येक पेज के आयामों को कॉन्फ़िगर करना। आप स्थिर आकार (जैसे A4, Letter) सेट कर सकते हैं या कंटेंट के आधार पर रेंडरर को इष्टतम चौड़ाई गणना करने दे सकते हैं। इससे लेआउट, पेजिनेशन और विज़ुअल फ़िडेलिटी पर सटीक नियंत्रण मिलता है।

## HTML को PDF में बदलते समय PDF पेज आकार क्यों समायोजित करें?
- **डिज़ाइन इरादा बनाए रखें:** कंटेंट कट या स्ट्रेच होने से बचें।  
- **प्रिंटिंग के लिए अनुकूलित करें:** डाउनस्ट्रीम प्रक्रियाओं के लिए आवश्यक कागज़ आकार से मेल रखें।  
- **पढ़ने में आसानी:** अत्यधिक व्हाइट स्पेस या भीड़भाड़ वाले टेक्स्ट से बचें।  
- **डायनामिक दस्तावेज़:** मैन्युअल गणना के बिना चौड़ी टेबल या इमेज़ को स्वचालित रूप से फिट करें।

## पूर्वापेक्षाएँ
शुरू करने से पहले सुनिश्चित करें कि आपके पास ये हों:

- **Java Development Kit (JDK) 8 या उससे ऊपर** आपके मशीन पर इंस्टॉल हो।  
- **Aspose.HTML for Java** – नवीनतम JAR [आधिकारिक रिलीज़ पेज](https://releases.aspose.com/html/java/) से डाउनलोड करें।  
- **एक HTML फ़ाइल** जिसे आप कन्वर्ट करना चाहते हैं (उदाहरण में हम `FirstFile.html` का उपयोग करेंगे)।  

## पैकेज इम्पोर्ट करें
सबसे पहले, उन क्लासेज़ को इम्पोर्ट करें जिनकी हमें आवश्यकता होगी। नीचे दिया गया कोड ब्लॉक मूल ट्यूटोरियल जैसा ही है।

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

## चरण 1: HTML कंटेंट पढ़ें
हम `FileInputStream` का उपयोग करके स्रोत HTML फ़ाइल पढ़ते हैं। यह चरण बाद में मैनिपुलेशन के लिए कच्चा मार्कअप तैयार करता है।

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## चरण 2: HTML लिखें (और वैकल्पिक रूप से समृद्ध करें)
यहाँ हम मूल HTML को नई फ़ाइल में कॉपी करते हैं और कुछ इनलाइन स्टाइल्स इंजेक्ट करते हैं ताकि दिखाया जा सके कि स्टाइलिंग PDF आउटपुट को कैसे प्रभावित करती है। आप नमूना CSS को अपनी पसंद के अनुसार बदल सकते हैं।

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Add custom HTML styles or content here
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

## चरण 3: HTML को PDF में रेंडर करें – दो परिदृश्य
अब हम देखेंगे कि **HTML से PDF जनरेट** करने के दो अलग‑अलग पेज‑साइज़ रणनीतियों का उपयोग कैसे किया जाता है।

### 3.1 पेज आकार कंटेंट की चौड़ाई के अनुसार समायोजित नहीं किया गया
इस केस में हम पेज आयाम (100 × 100 पॉइंट) को फिक्स कर देते हैं। यदि कोई एलिमेंट इन सीमाओं से अधिक हो जाता है, तो वह क्लिप हो जाएगा।

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Create an HTMLDocument instance from the HTML file
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Set PDF rendering options
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

### 3.2 पेज आकार कंटेंट की चौड़ाई के अनुसार समायोजित किया गया
यहाँ हम `AdjustToWidestPage` को सक्षम करते हैं, जिससे रेंडरर स्वचालित रूप से पेज की चौड़ाई को सबसे चौड़े एलिमेंट के अनुसार विस्तारित कर देता है जबकि ऊँचाई फिक्स रहती है।

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

## कोड में PDF आयाम कैसे सेट करें (PDF पेज आकार कैसे बदलें)
`PageSetup` ऑब्जेक्ट मुख्य है:

- `setAnyPage(Page page)`: बेस चौड़ाई × ऊँचाई निर्धारित करता है।  
- `setAdjustToWidestPage(boolean)`: स्वचालित विस्तारण को टॉगल करता है।  

इन दो प्रॉपर्टीज़ को समायोजित करके आप **किसी भी परिदृश्य** के लिए PDF आयाम सेट कर सकते हैं, चाहे वह स्थिर A4 पेज हो या डायनामिक चौड़ाई जो आपके HTML लेआउट का अनुसरण करे।

## सामान्य समस्याएँ और टिप्स
| समस्या | क्यों होता है | समाधान |
|-------|----------------|-----|
| कंटेंट कट जाता है | फिक्स्ड साइज बहुत छोटा है | `Size` मान बढ़ाएँ या `AdjustToWidestPage` सक्षम करें। |
| टेक्स्ट धुंधला दिखता है | डिफ़ॉल्ट रेंडरिंग DPI कम है | `PdfRenderingOptions.setResolution(int dpi)` से क्वालिटी बढ़ाएँ। |
| स्टाइल्स गायब हैं | एक्सटर्नल CSS लोड नहीं हुआ | CSS को इनलाइन एम्बेड करें या `HTMLDocument.setBaseUrl()` से स्टाइलशीट फ़ोल्डर पॉइंट करें। |
| बड़े HTML फ़ाइलों से OutOfMemoryError | रेंडरर पूरे दस्तावेज़ को मेमोरी में लोड करता है | दस्तावेज़ को चंक्स में प्रोसेस करें या JVM हीप बढ़ाएँ (`-Xmx`)। |

## अक्सर पूछे जाने वाले प्रश्न

**Q: Aspose.HTML for Java क्या है?**  
A: यह एक Java लाइब्रेरी है जो आपको HTML दस्तावेज़ बनाने, संपादित करने और रेंडर करने देती है, जिसमें PDF, PNG और अन्य फ़ॉर्मेट में कन्वर्ज़न शामिल है।

**Q: Aspose.HTML for Java के साथ HTML को PDF में कन्वर्ट करते समय PDF पेज आकार कैसे समायोजित करूँ?**  
A: `PageSetup` क्लास का उपयोग करें और `AdjustToWidestPage` को `true` (ऑटो‑साइज़) या `false` (फिक्स्ड साइज) सेट करें। फिर `new Page(new Size(width, height))` के माध्यम से इच्छित `Size` असाइन करें।

**Q: क्या मैं PDF में कन्वर्ट करने से पहले HTML कंटेंट की स्टाइलिंग कस्टमाइज़ कर सकता हूँ?**  
A: हाँ – आप CSS इंजेक्ट कर सकते हैं, DOM बदल सकते हैं, या एक्सटर्नल स्टाइल शीट्स उपयोग कर सकते हैं। ट्यूटोरियल में इनलाइन CSS इंजेक्शन दिखाया गया है।

**Q: Aspose.HTML for Java की डॉक्यूमेंटेशन कहाँ मिल सकती है?**  
A: विस्तृत डॉक्यूमेंटेशन [यहाँ](https://reference.aspose.com/html/java/) उपलब्ध है।

**Q: क्या Aspose.HTML for Java के लिए फ्री ट्रायल उपलब्ध है?**  
A: बिल्कुल – ट्रायल [रिलीज़ पेज](https://releases.aspose.com/html/java/) से डाउनलोड करें।

## निष्कर्ष
अब आप जानते हैं कि **PDF पेज आकार कैसे समायोजित करें**, **HTML को PDF के रूप में रेंडर करें**, और **Aspose.HTML for Java का उपयोग करके कस्टम PDF आयाम सेट करें**। विभिन्न पेज साइज, DPI सेटिंग्स और CSS ट्यूनिंग के साथ प्रयोग करें ताकि आपके विशिष्ट उपयोग केस के लिए आउटपुट परफेक्ट हो। यदि आप किसी चुनौती का सामना करते हैं, तो आधिकारिक डॉक्यूमेंटेशन या Aspose सपोर्ट फ़ोरम देखें।

---

**अंतिम अपडेट:** 2025-12-01  
**टेस्टेड विथ:** Aspose.HTML for Java 24.12 (नवीनतम)  
**लेखक:** Aspose  
**संबंधित संसाधन:** [API रेफ़रेंस](https://reference.aspose.com/html/java/) | [फ्री ट्रायल डाउनलोड करें](https://releases.aspose.com/html/java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
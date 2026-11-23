---
category: general
date: 2026-06-19
description: एक सरल जावा उदाहरण का उपयोग करके HTML से PDF कैसे बनाएं, सीखें। यह HTML
  से PDF ट्यूटोरियल आपको दिखाता है कि OpenHTMLtoPDF के साथ HTML फ़ाइल को PDF में कैसे
  परिवर्तित करें।
draft: false
keywords:
- html to pdf tutorial
- generate pdf from html
- convert html file pdf
- create pdf from html
- convert webpage to pdf
language: hi
og_description: HTML से PDF ट्यूटोरियल आपको दिखाता है कि जावा का उपयोग करके HTML से
  PDF कैसे बनाएं। HTML फ़ाइल को जल्दी PDF में बदलने के लिए चरणों का पालन करें।
og_title: 'HTML से PDF ट्यूटोरियल: जावा रूपांतरण गाइड'
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  headline: 'html to pdf tutorial: Convert HTML to PDF in Java'
  type: TechArticle
- description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  name: 'html to pdf tutorial: Convert HTML to PDF in Java'
  steps:
  - name: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
    text: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
  - name: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
    text: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
  - name: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
    text: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
  type: HowTo
tags:
- Java
- PDF
- HTML conversion
title: 'HTML से PDF ट्यूटोरियल: जावा में HTML को PDF में बदलें'
url: /hi/java/conversion-html-to-other-formats/html-to-pdf-tutorial-convert-html-to-pdf-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# html to pdf tutorial – Java के साथ HTML पेज को PDF में बदलें

क्या आपने कभी सोचा है कि बिना IDE छोड़े एक स्थिर HTML पेज को एक सुंदर PDF दस्तावेज़ में कैसे बदला जाए? आप अकेले नहीं हैं। इस **html to pdf tutorial** में हम एक पूर्ण, तैयार‑चलाने योग्य Java उदाहरण के माध्यम से चलेंगे जो कुछ ही मिनटों में **generate pdf from html** करता है।

हम वह सब कवर करेंगे जो आपको चाहिए—प्रोजेक्ट सेटअप, सही लाइब्रेरी जोड़ना, रूपांतरण कोड लिखना, और यहाँ तक कि लाइव वेबपेज को PDF में बदलने के लिए एक त्वरित टिप। अंत तक आप अपने मशीन पर **convert html file pdf** कर सकेंगे, और आप समझेंगे कि किसी भी भविष्य के प्रोजेक्ट के लिए **create pdf from html** कैसे किया जाता है।

## आपको क्या चाहिए

- Java 17 या नया (कोड किसी भी हालिया JDK के साथ काम करता है)
- Maven या Gradle (हम Maven स्निपेट दिखाएंगे)
- एक छोटा HTML फ़ाइल जिसे आप PDF में बदलना चाहते हैं (हम इसे तुरंत बनाएँगे)
- एक IDE या साधारण टेक्स्ट एडिटर—आपकी पसंद

बस इतना ही। कोई भारी सर्वर नहीं, कोई पेड SDK नहीं, सिर्फ शुद्ध Java और एक मुफ्त ओपन‑सोर्स लाइब्रेरी।

## चरण 1: html to pdf tutorial – Maven प्रोजेक्ट सेटअप करें

सबसे पहले। एक नया Maven प्रोजेक्ट बनाएं (या मौजूदा में जोड़ें)। आपको वास्तव में केवल एक ही निर्भरता चाहिए **OpenHTMLtoPDF**, जो HTML और CSS को PDF में रेंडर करने का काम करती है।

```xml
<!-- pom.xml snippet -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>html-to-pdf-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- OpenHTMLtoPDF core -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-pdfbox</artifactId>
            <version>1.0.10</version>
        </dependency>
        <!-- Optional: support for SVG, if your HTML uses it -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-svg-support</artifactId>
            <version>1.0.10</version>
        </dependency>
    </dependencies>
</project>
```

> **Pro tip:** यदि आप Gradle का उपयोग कर रहे हैं, तो वही निर्भरताएँ `build.gradle` में `implementation` के तहत जोड़ी जा सकती हैं।  

यह चरण क्यों महत्वपूर्ण है: लाइब्रेरी के बिना JVM को नहीं पता कि HTML टैग को PDF ड्रॉइंग कमांड में कैसे बदलना है। OpenHTMLtoPDF हल्का, सक्रिय रूप से रखरखाव किया गया, और CSS‑2.1 के साथ काम करता है, इसलिए आपकी स्टाइलिंग बनी रहती है।

## चरण 2: generate pdf from html – एक नमूना HTML फ़ाइल तैयार करें

आइए हमारे Java स्रोत के बगल में एक छोटा `input.html` बनाते हैं। यह उदाहरण को स्व-निहित रखता है और **create pdf from html** वर्कफ़्लो को दर्शाता है।

```html
<!-- src/main/resources/input.html -->
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Sample Report</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; }
        h1 { color: #2E86C1; }
        p { line-height: 1.5; }
    </style>
</head>
<body>
    <h1>Monthly Sales Report</h1>
    <p>This PDF was generated directly from an HTML file using Java.</p>
    <p>All you need is a few lines of code.</p>
</body>
</html>
```

आप सामग्री को कुछ भी से बदल सकते हैं—टेबल, चित्र, यहाँ तक कि JavaScript (हालांकि रेंडरर स्क्रिप्ट को अनदेखा करता है)। महत्वपूर्ण बात यह है कि फ़ाइल क्लासपाथ पर मौजूद हो ताकि कन्वर्टर उसे ढूँढ सके।

## चरण 3: convert html file pdf – रूपांतरण यूटिलिटी लिखें

अब **html to pdf tutorial** का मुख्य भाग: एक छोटा `HtmlToPdfConverter` क्लास जो HTML पढ़ता है और PDF लिखता है। नीचे दिया गया कोड एक पूर्ण, चलाने योग्य उदाहरण है; इसे `src/main/java/com/example/HtmlToPdfConverter.java` में कॉपी‑पेस्ट करें।

```java
package com.example;

import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardCopyOption;

/**
 * Simple utility that converts an HTML file to PDF.
 * It demonstrates the "convert html file pdf" use‑case.
 */
public class HtmlToPdfConverter {

    /**
     * Converts the given HTML file to a PDF file.
     *
     * @param htmlPath path to the source HTML file (can be absolute or classpath)
     * @param pdfPath  destination path for the generated PDF
     * @throws IOException if reading or writing fails
     */
    public static void convert(String htmlPath, String pdfPath) throws IOException {
        // Resolve the HTML file – support both absolute paths and classpath resources
        InputStream htmlStream = Files.exists(Path.of(htmlPath))
                ? Files.newInputStream(Path.of(htmlPath))
                : HtmlToPdfConverter.class.getResourceAsStream(htmlPath);

        if (htmlStream == null) {
            throw new FileNotFoundException("HTML source not found: " + htmlPath);
        }

        // Ensure the output directory exists
        Path pdfFile = Path.of(pdfPath);
        Files.createDirectories(pdfFile.getParent());

        try (OutputStream os = Files.newOutputStream(pdfFile);
             InputStream is = htmlStream) {

            // Builder does the heavy lifting – it parses HTML + CSS and writes PDF bytes
            new PdfRendererBuilder()
                    .withHtmlContent(new String(is.readAllBytes()), null) // base URI null = no external resources
                    .toStream(os)
                    .run();
        }
    }

    // Demo entry point – feel free to run this class directly
    public static void main(String[] args) {
        // Step 1: Specify the input HTML file location
        String htmlPath = "src/main/resources/input.html";

        // Step 2: Specify the desired output PDF file location
        String pdfPath = "target/output.pdf";

        // Step 3: Convert the HTML document to PDF using default conversion settings
        try {
            convert(htmlPath, pdfPath);
            System.out.println("✅ PDF successfully created at " + pdfPath);
        } catch (Exception e) {
            System.err.println("❌ Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### यह कोड क्यों काम करता है

1. **Resource flexibility** – यह मेथड पहले जांचता है कि दिया गया पथ वास्तविक फ़ाइल की ओर इशारा करता है या नहीं; यदि नहीं, तो यह क्लासपाथ रिसोर्स पर वापस जाता है। इसका मतलब है कि आप बाद में एक URL स्ट्रिंग देकर **convert webpage to pdf** कर सकते हैं (सिर्फ `withHtmlContent` कॉल को `withUri` से बदलें)।

2. **Automatic directory creation** – `Files.createDirectories` सुनिश्चित करता है कि `target/` फ़ोल्डर मौजूद है, इसलिए आपको “No such file or directory” त्रुटि नहीं मिलेगी।

3. **Single‑line conversion** – `PdfRendererBuilder` आंतरिक रूप से CSS, फ़ॉन्ट और पेज लेआउट को संभालता है। PDF पेज को मैन्युअली प्रबंधित करने की आवश्यकता नहीं; लाइब्रेरी आपके लिए यह करती है, जिससे उदाहरण छोटा और **convert html file pdf** अवधारणा पर केंद्रित रहता है।

## चरण 4: create pdf from html – प्रोग्राम चलाएँ और सत्यापित करें

प्रोजेक्ट रूट में एक टर्मिनल खोलें और चलाएँ:

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HtmlToPdfConverter
```

यदि सब कुछ सही ढंग से सेट है तो आप देखेंगे:

```
✅ PDF successfully created at target/output.pdf
```

`target/output.pdf` को किसी भी PDF व्यूअर से खोलें। आपको स्टाइल किया हुआ “Monthly Sales Report” हेडर, पैराग्राफ टेक्स्ट, और वही मार्जिन दिखने चाहिए जो आपने HTML `<style>` ब्लॉक में परिभाषित किए थे।

> **यदि आपको स्टाइलिंग नहीं दिख रही है तो क्या करें?**  
> सुनिश्चित करें कि CSS इनलाइन है या HTML के समान फ़ोल्डर में स्थित है। OpenHTMLtoPDF रिलेटिव URL को उस बेस URI के आधार पर हल करता है जिसे आप `withHtmlContent` को पास करते हैं। ऊपर के स्निपेट में हमने `null` पास किया था, जो सरल इनलाइन CSS के लिए काम करता है। बाहरी स्टाइलशीट्स के लिए, दूसरा आर्ग्युमेंट के रूप में डायरेक्टरी पाथ दें।

## चरण 5: convert webpage to pdf – रिमोट URLs को संभालना (वैकल्पिक)

कभी-कभी आपको इंटरनेट से सीधे **convert webpage to pdf** करने की जरूरत पड़ती है—जैसे ऑनलाइन रसीद को आर्काइव करना। लाइब्रेरी `withUri` के माध्यम से इसे सपोर्ट करती है। यहाँ एक त्वरित अनुकूलन है:

```java
public static void convertUrl(String url, String pdfPath) throws IOException {
    Path pdfFile = Path.of(pdfPath);
    Files.createDirectories(pdfFile.getParent());

    try (OutputStream os = Files.newOutputStream(pdfFile)) {
        new PdfRendererBuilder()
                .withUri(url)          // Load HTML from the web
                .toStream(os)
                .run();
    }
}
```

इसे इस तरह कॉल करें:



## अब आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण-दर-चरण व्याख्याएँ शामिल हैं ताकि आप अतिरिक्त API फीचर्स में निपुण हो सकें और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण कर सकें।

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Convert HTML to PDF Java – Configuring Environment in Aspose.HTML](/html/english/java/configuring-environment/)
- [Convert HTML to PDF in Java – Step‑by‑Step Guide with Page Size Settings](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
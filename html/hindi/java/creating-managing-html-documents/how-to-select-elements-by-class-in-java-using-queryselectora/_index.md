---
category: general
date: 2026-09-29
description: जावा में क्लास द्वारा तत्वों का चयन करना, फ़ाइल से HTML पढ़ना, और बाहरी
  लिंक ढूँढ़ना सीखें। यह चरण‑दर‑चरण गाइड NodeList को कुशलतापूर्वक इटररेट करने को कवर
  करता है।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- select elements by class
- read html from file
- find external links
- iterate nodelist java
- use queryselectorall java
language: hi
lastmod: 2026-09-29
og_description: Java में क्लास द्वारा तत्वों का चयन करें, फ़ाइल से HTML पढ़ें, और
  querySelectorAll का उपयोग करके बाहरी लिंक खोजें। NodeList को इटररेट करने के लिए
  पूर्ण उदाहरण का पालन करें।
og_image_alt: Screenshot showing Java code that selects elements by class from an
  HTML file
og_title: जावा में क्लास द्वारा तत्व चुनें – querySelectorAll के साथ पूर्ण गाइड
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to select elements by class, read HTML from file, and find
    external links in Java. This step‑by‑step guide covers iterating a NodeList efficiently.
  headline: How to select elements by class in Java using querySelectorAll
  type: TechArticle
- questions:
  - answer: Yes. `Jsoup.parse` treats the input as a fragment and automatically adds
      missing root elements, allowing selectors to work on the fragment’s body.
    question: Does this work with HTML fragments that lack a `<html>` root?
  - answer: The standard Java DOM API (`org.w3c.dom`) does not include `querySelectorAll`.
      Libraries such as **HTMLUnit** or **jodd-lagarto** provide similar methods.
      The pattern shown here—load, select with CSS, iterate—remains the same.
    question: Can I use `querySelectorAll` without jsoup?
  - answer: 'After obtaining each `Element`, you can call `link.attr("href", "newUrl")`
      and then write the document back to disk with `Files.writeString`. ## Conclusion
      You now know how to **select elements by class**, **read HTML from file**, **find
      external links**, and **iterate a NodeList in Java** using `qu'
    question: What if I need to modify the links instead of just printing them?
  type: FAQPage
tags:
- Java
- HTML parsing
- DOM manipulation
title: जावा में querySelectorAll का उपयोग करके क्लास द्वारा तत्वों का चयन कैसे करें
url: /hi/java/creating-managing-html-documents/how-to-select-elements-by-class-in-java-using-queryselectora/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java में querySelectorAll का उपयोग करके क्लास द्वारा एलिमेंट्स का चयन कैसे करें

यदि आपको Java में HTML फ़ाइल को प्रोसेस करते समय **क्लास द्वारा एलिमेंट्स का चयन** करने की आवश्यकता है, तो यह गाइड आपको ठीक-ठीक बताता है कि इसे कैसे करें। आप फ़ाइल से HTML पढ़ना, `querySelectorAll` का उपयोग करके बाहरी लिंक ढूँढना, और प्राप्त `NodeList` को सुरक्षित रूप से इटरेट करना सीखेंगे।

Java में HTML के साथ काम करना अक्सर भारी महसूस होता है, लेकिन आधुनिक लाइब्रेरीज़ आपको एक संक्षिप्त, CSS‑सेलेक्टर‑आधारित API देती हैं। नीचे दिया गया उदाहरण **jsoup** (संस्करण 1.17.2) का उपयोग करता है क्योंकि यह `querySelectorAll`‑शैली के सेलेक्टर लागू करता है और एक `Elements` कलेक्शन लौटाता है जो `NodeList` की तरह व्यवहार करता है। आप आवश्यकता पड़ने पर इसी लॉजिक को अन्य DOM इम्प्लीमेंटेशन में भी अनुकूलित कर सकते हैं।

## आवश्यकताएँ

* JDK 17 या नया स्थापित हो।
* निर्भरता प्रबंधन के लिए Maven या Gradle।
* Java streams और DOM मॉडल की बुनियादी समझ।

अपने प्रोजेक्ट में jsoup जोड़ें:

```xml
<!-- Maven -->
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

```gradle
// Gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

## चरण 1: फ़ाइल से HTML पढ़ें

पहला कार्य डिस्क से HTML दस्तावेज़ लोड करना है। `Jsoup.parse(Path, Charset)` फ़ाइल को पढ़ता है और एक DOM ट्री बनाता है जिसे आप क्वेरी कर सकते हैं।

```java
import java.nio.file.Paths;
import java.nio.charset.StandardCharsets;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class HtmlLoader {
    /**
     * Loads an HTML file and returns a Jsoup Document.
     *
     * @param filePath absolute or relative path to the HTML file
     * @return parsed Document ready for DOM queries
     * @throws IOException if the file cannot be read
     */
    public static Document load(String filePath) throws IOException {
        return Jsoup.parse(Paths.get(filePath).toFile(),
                           StandardCharsets.UTF_8.name(),
                           "");
    }
}
```

*क्यों यह महत्वपूर्ण है*: फ़ाइल को एक बार लोड करने से बाद में एलिमेंट्स पर इटरेट करते समय बार‑बार I/O से बचा जा सकता है। `Document` ऑब्जेक्ट पूर्ण DOM रखता है, जिससे तेज़ सेलेक्टर क्वेरी संभव होती है।

## चरण 2: `querySelectorAll` का उपयोग करके क्लास द्वारा एलिमेंट्स का चयन करें

अब जब दस्तावेज़ मेमोरी में है, आप CSS सेलेक्टर का उपयोग करके **क्लास द्वारा एलिमेंट्स का चयन** कर सकते हैं। सेलेक्टर `"a.external"` उन `<a>` टैग्स से मेल खाता है जिनमें `external` क्लास है—बिल्कुल वही जो आपको **बाहरी लिंक खोजने** के लिए चाहिए।

```java
import org.jsoup.select.Elements;
import org.jsoup.nodes.Element;

/**
 * Returns all anchor elements with the CSS class "external".
 *
 * @param doc the parsed HTML document
 * @return a collection of matching Elements
 */
public static Elements findExternalLinks(Document doc) {
    // querySelectorAll is simulated by the select() method in Jsoup
    return doc.select("a.external");
}
```

*क्यों यह महत्वपूर्ण है*: क्लास सेलेक्टर का उपयोग अभिव्यक्तिपूर्ण और प्रदर्शन‑उपयुक्त दोनों है। लाइब्रेरी सेलेक्टर को एक अनुकूलित ट्रैवर्सल में बदल देती है, इसलिए आपको हर नोड पर मैन्युअल लूप लिखने की जरूरत नहीं है।

## चरण 3: Java में NodeList (Elements) को इटरेट करें

`Elements` `Iterable<Element>` को इम्प्लीमेंट करता है, जिसका अर्थ है कि आप एक सामान्य `for‑each` लूप का उपयोग करके **NodeList Java** ऑब्जेक्ट्स को **इटरेट** कर सकते हैं। नीचे दिया गया लूप प्रत्येक लिंक के `href` एट्रिब्यूट को प्रिंट करता है।

```java
/**
 * Prints the href attribute of every external link.
 *
 * @param externalLinks collection returned by findExternalLinks()
 */
public static void printExternalLinks(Elements externalLinks) {
    for (Element link : externalLinks) {
        System.out.println("External link: " + link.attr("href"));
    }
}
```

*क्यों यह महत्वपूर्ण है*: सीधा इटरेशन कोड को पढ़ने योग्य बनाता है और जब आपको केवल साधारण आउटपुट चाहिए तो कलेक्शन को स्ट्रीम में बदलने के ओवरहेड से बचाता है।

## पूर्ण कार्यशील उदाहरण

तीन चरणों को मिलाकर एक स्व-निहित प्रोग्राम बनता है जिसे आप कमांड लाइन से चला सकते हैं।

```java
import java.io.IOException;
import org.jsoup.nodes.Document;
import org.jsoup.select.Elements;

public class ExternalLinkExtractor {

    public static void main(String[] args) {
        // Validate input
        if (args.length != 1) {
            System.err.println("Usage: java ExternalLinkExtractor <input.html>");
            System.exit(1);
        }

        String inputPath = args[0];

        try {
            // Step 1: read HTML from file
            Document doc = HtmlLoader.load(inputPath);

            // Step 2: select elements by class (find external links)
            Elements externalLinks = findExternalLinks(doc);

            // Step 3: iterate NodeList Java and print hrefs
            printExternalLinks(externalLinks);
        } catch (IOException e) {
            System.err.println("Error reading file: " + e.getMessage());
        }
    }

    // Reuse methods from previous sections
    private static Elements findExternalLinks(Document doc) {
        return doc.select("a.external");
    }

    private static void printExternalLinks(Elements externalLinks) {
        for (org.jsoup.nodes.Element link : externalLinks) {
            System.out.println("External link: " + link.attr("href"));
        }
    }
}
```

### अपेक्षित आउटपुट

मान लीजिए `input.html` में यह है:

```html
<a class="external" href="https://example.com">Example</a>
<a class="internal" href="/about">About</a>
<a class="external" href="https://openai.com">OpenAI</a>
```

प्रोग्राम चलाने पर यह प्रिंट करता है:

```
External link: https://example.com
External link: https://openai.com
```

## प्रो टिप्स और सामान्य pitfalls

* **Encoding matters** – फ़ाइल को हमेशा UTF‑8 (या आपके स्रोत के अनुरूप charset) से पढ़ें। गलत एन्कोडिंग एट्रिब्यूट मानों में अक्षरों को भ्रष्ट कर सकती है।
* **Multiple classes** – यदि किसी एलिमेंट में कई क्लासेज़ हैं (जैसे `class="btn external"`), तो सेलेक्टर `"a.external"` फिर भी मेल खाता है क्योंकि CSS क्लास सेलेक्टर टोकन की उपस्थिति को जाँचता है, न कि पूरी स्ट्रिंग को।
* **Performance tip** – यदि आपको केवल `href` एट्रिब्यूट चाहिए, तो आप इसे सीधे `doc.select("a.external[href]").eachAttr("href")` से प्राप्त कर सकते हैं। इससे प्रत्येक मैच के लिए पूर्ण `Element` ऑब्जेक्ट बनाने से बचा जा सकता है।
* **Null safety** – `link.attr("href")` यदि एट्रिब्यूट मौजूद नहीं है तो खाली स्ट्रिंग लौटाता है, इसलिए प्रिंट करने से पहले आपको null चेक करने की आवश्यकता नहीं है।

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या यह उन HTML फ्रैगमेंट्स के साथ काम करता है जिनमें `<html>` रूट नहीं है?**  
A: हाँ। `Jsoup.parse` इनपुट को एक फ्रैगमेंट मानता है और स्वचालित रूप से गायब रूट एलिमेंट्स जोड़ देता है, जिससे सेलेक्टर्स फ्रैगमेंट के बॉडी पर काम कर सकते हैं।

**Q: क्या मैं `querySelectorAll` को jsoup के बिना उपयोग कर सकता हूँ?**  
A: मानक Java DOM API (`org.w3c.dom`) में `querySelectorAll` नहीं है। **HTMLUnit** या **jodd-lagarto** जैसी लाइब्रेरीज़ समान मेथड प्रदान करती हैं। यहाँ दिखाया गया पैटर्न—लोड, CSS से चयन, इटरेट—वही रहता है।

**Q: यदि मुझे लिंक को केवल प्रिंट करने के बजाय संशोधित करना हो तो क्या करें?**  
A: प्रत्येक `Element` प्राप्त करने के बाद, आप `link.attr("href", "newUrl")` कॉल कर सकते हैं और फिर `Files.writeString` से दस्तावेज़ को डिस्क पर वापस लिख सकते हैं।

## निष्कर्ष

अब आप जानते हैं कि **क्लास द्वारा एलिमेंट्स का चयन** कैसे करें, **फ़ाइल से HTML पढ़ें**, **बाहरी लिंक खोजें**, और `querySelectorAll`‑शैली के सेलेक्टर्स का उपयोग करके **Java में NodeList को इटरेट** करें। पूरा उदाहरण एक साफ़, प्रोडक्शन‑रेडी वर्कफ़्लो दर्शाता है जिसे आप बड़े स्क्रैपिंग या ट्रांसफ़ॉर्मेशन पाइपलाइन में एम्बेड कर सकते हैं।

अगला, **HTMLUnit के साथ डायनामिक कंटेंट पार्सिंग**, **संशोधित HTML को डिस्क पर वापस लिखना**, या **Java streams का उपयोग करके लिंक URLs को लिस्ट में इकट्ठा करना** जैसे संबंधित विषयों का अन्वेषण करें। इन सभी में यहाँ दर्शाए गए क्लास‑आधारित चयन की मूल तकनीक का उपयोग होता है। हैप्पी कोडिंग!

## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन निकट-संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में निपुण बनने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर करने में मदद करेंगे।

- [Java में HTML क्वेरी कैसे करें – एलिमेंट्स का चयन, एट्रिब्यूट द्वारा फ़िल्टर, और टेक्स्ट प्राप्त करें](/html/english/java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/)
- [NodeList Java को इटरेट करें – HTML पढ़ें और इमेज src प्राप्त करें](/html/english/java/creating-managing-html-documents/iterate-nodelist-java-read-html-get-image-src/)
- [Aspose.HTML for Java में फ़ाइल से HTML दस्तावेज़ लोड करें](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
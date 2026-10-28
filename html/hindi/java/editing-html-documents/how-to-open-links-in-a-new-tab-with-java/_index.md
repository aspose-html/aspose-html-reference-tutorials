---
category: general
date: 2026-10-28
description: जावा में HTML को पार्स करके, बाहरी लिंक ढूँढकर और target="_blank" जोड़कर
  लिंक को नई टैब में कैसे खोलें, सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- open links new tab
- find external links
- add target blank
- parse html in java
- save modified html
language: hi
lastmod: 2026-10-28
og_description: 'जावा का उपयोग करके लिंक को नए टैब में खोलें: HTML पार्स करें, बाहरी
  लिंक खोजें, target="_blank" जोड़ें, और संशोधित HTML सहेजें।'
og_image_alt: Screenshot of Java code that parses HTML and updates external links
  to open in a new tab
og_title: जावा के साथ लिंक को नए टैब में खोलें – चरण‑दर‑चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to open links in a new tab by parsing HTML in Java, finding
    external links and adding target blank.
  headline: How to open links in a new tab with Java
  type: TechArticle
tags:
- Java
- HTML parsing
- jsoup
- web automation
title: जावा के साथ लिंक को नई टैब में कैसे खोलें
url: /hi/java/editing-html-documents/how-to-open-links-in-a-new-tab-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java के साथ लिंक को नए टैब में कैसे खोलें

यदि आपको स्थैतिक HTML फ़ाइल से **लिंक को नए टैब में खोलने** की आवश्यकता है, तो यह गाइड आपको ठीक-ठीक बताता है कि कैसे करना है। आप सीखेंगे **Java में HTML पार्स करना**, **बाहरी लिंक ढूँढ़ना**, **target blank जोड़ना**, और **संशोधित HTML सहेजना** बिना अपने IDE को छोड़े।

बाहरी लिंक को नए ब्राउज़र टैब में खोलने से उपयोगकर्ता अनुभव बेहतर होता है और आगंतुक मूल पृष्ठ पर ही रहते हैं। नीचे दिया गया समाधान किसी भी HTML दस्तावेज़ के साथ काम करता है, केवल लोकप्रिय jsoup लाइब्रेरी की आवश्यकता होती है, और Java 8 या उससे नए संस्करण पर चलता है।

## आवश्यकताएँ

* JDK 8 + स्थापित हो  
* एक बिल्ड टूल (Maven या Gradle) जो **jsoup** निर्भरता को लाए  
* `external` क्लास वाले एंकर टैग वाली एक HTML फ़ाइल

आपको वेब सर्वर या अतिरिक्त फ्रेमवर्क की आवश्यकता नहीं है—jsoup सब कुछ स्थानीय रूप से संभालता है।

## चरण 1: अपने प्रोजेक्ट में jsoup सेट करें

jsoup को एक निर्भरता के रूप में जोड़ें। यदि आप Maven उपयोग करते हैं, तो इसे `pom.xml` में रखें:

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

Gradle के लिए, `build.gradle` में निम्न पंक्ति जोड़ें:

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

ये कोऑर्डिनेट्स नवीनतम स्थिर रिलीज़ (अक्टूबर 2026 तक) को लाते हैं। सिंक करने के बाद, आप अपने Java स्रोत फ़ाइलों में `org.jsoup` क्लासेस को इम्पोर्ट कर सकते हैं।

## चरण 2: HTML दस्तावेज़ को पार्स करें

फ़ाइल को पार्स करना **लिंक को नए टैब में खोलने** की पहली कदम है। `Jsoup.parse` मेथड फ़ाइल को एक परिवर्तनीय DOM‑जैसी संरचना में पढ़ता है।

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // Load the HTML document from disk
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");
        
        // Continue with link processing...
    }
}
```

*यह क्यों महत्वपूर्ण है*: `Document` आपको CSS‑स्टाइल सेलेक्टर देता है, जिससे आवश्यक तत्वों को ढूँढ़ना बहुत आसान हो जाता है।

## चरण 3: बाहरी लिंक खोजें

अब प्रत्येक `<a>` एलिमेंट को खोजें जिसमें `external` क्लास हो। यह **बाहरी लिंक खोजें** की आवश्यकता को पूरा करता है।

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

// Inside main after parsing:
Elements externalLinks = doc.select("a.external");
```

`Elements` मिलते-जुलते नोड्स का एक संग्रह है। यदि सेलेक्टर खाली सेट लौटाता है, तो आपके HTML में क्लास नहीं है या अलग नामकरण परंपरा उपयोग की गई है—सेलेक्टर को उसी अनुसार समायोजित करें।

## चरण 4: प्रत्येक लिंक में `target="_blank"` जोड़ें

प्रत्येक नोड के लिए जो **बाहरी लिंक खोजें** द्वारा लौटाया गया है, `target` एट्रिब्यूट को `_blank` सेट करें। यह **target blank जोड़ें** चरण को पूरा करता है और सुनिश्चित करता है कि ब्राउज़र लिंक को नए टैब में खोलें।

```java
for (Element link : externalLinks) {
    link.attr("target", "_blank");
}
```

`attr` मेथड किसी भी मौजूदा `target` मान को ओवरराइट कर देता है, जिससे सभी बाहरी एंकर पर सुसंगत व्यवहार सुनिश्चित होता है।

## चरण 5: संशोधित HTML सहेजें

DOM को अपडेट करने के बाद, परिवर्तन को फ़ाइल में वापस लिखें। यह ट्यूटोरियल के **संशोधित HTML सहेजें** भाग को पूरा करता है।

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

// Still inside main:
Path output = Path.of("YOUR_DIRECTORY/updated.html");
Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
System.out.println("Updated file written to " + output);
```

`doc.outerHtml()` पूरे दस्तावेज़ को सीरियलाइज़ करता है, इंडेंटेशन और फ़ॉर्मेटिंग को वैसे ही रखता है जैसा jsoup ने मूल रूप से पार्स किया था।

## पूर्ण कार्यशील उदाहरण

सभी चरणों को मिलाकर एक स्वयं‑समाहित प्रोग्राम बनता है जिसे आप कॉपी, पेस्ट और चला सकते हैं।

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

/**
 * Updates all external links so they open in a new tab.
 */
public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // 1️⃣ Parse the HTML file
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");

        // 2️⃣ Find external links (a.external)
        Elements externalLinks = doc.select("a.external");

        // 3️⃣ Add target="_blank" to each link
        for (Element link : externalLinks) {
            link.attr("target", "_blank");
        }

        // 4️⃣ Save the modified HTML
        Path output = Path.of("YOUR_DIRECTORY/updated.html");
        Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
        System.out.println("Updated file written to " + output);
    }
}
```

### अपेक्षित आउटपुट

मान लीजिए `sample.html` में यह है:

```html
<a href="https://example.com" class="external">Example</a>
<a href="/internal/page.html">Internal</a>
```

प्रोग्राम चलाने के बाद, `updated.html` में यह होगा:

```html
<a href="https://example.com" class="external" target="_blank">Example</a>
<a href="/internal/page.html">Internal</a>
```

केवल बाहरी लिंक को `target="_blank"` एट्रिब्यूट मिला है, जिसका अर्थ है कि ब्राउज़र अब इसे नए टैब में खोलेगा।

## प्रो टिप्स और सामान्य कठिनाइयाँ

* **प्रो टिप:** यदि आपको लिंक जो `http://` या `https://` से शुरू होते हैं, को CSS क्लास के बिना भी बाहरी मानना है, तो सेलेक्टर को विस्तारित करें: `doc.select("a[href^=http]")`।  
* **एज केस:** कुछ पृष्ठ पहले से ही `target="_self"` निर्दिष्ट करते हैं; `attr` कॉल इसे ओवरराइट कर देता है, जिससे सुसंगत व्यवहार सुनिश्चित होता है।  
* **परफॉर्मेंस:** बहुत बड़े HTML फ़ाइलों के लिए, मेमोरी उपयोग कम करने हेतु स्ट्रीमिंग पार्सिंग पर विचार करें (`Jsoup.parse(File, String, String, Parser.htmlParser())`)।  
* **टेस्टिंग:** परिणाम की पुष्टि `updated.html` को ब्राउज़र में खोलकर और डेवलपर टूल्स से लिंक का निरीक्षण करके करें—`target` एट्रिब्यूट देखें।

## निष्कर्ष

अब आपके पास Java का उपयोग करके **लिंक को नए टैब में खोलने** का एक पूर्ण, चलाने योग्य समाधान है। ट्यूटोरियल ने बताया कि कैसे **java में html पार्स करें**, **बाहरी लिंक खोजें**, **target blank जोड़ें**, और **संशोधित html सहेजें**, सभी हल्की jsoup लाइब्रेरी के साथ।

अब आप कर सकते हैं:

* सेलेक्टर को अन्य लिंक पैटर्न (जैसे `rel="external"`) को संभालने के लिए विस्तारित करें।  
* इस लॉजिक को एक बिल्ड स्टेप के साथ मिलाएँ जो प्रोजेक्ट में सभी HTML फ़ाइलों को प्रोसेस करे।  
* कोड को एक बड़े कंटेंट‑मैनेजमेंट पाइपलाइन में इंटीग्रेट करें।

विभिन्न सेलेक्टर या आउटपुट फ़ॉर्मेट के साथ प्रयोग करने में संकोच न करें, और अपने परिणाम समुदाय के साथ साझा करें!

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में निपुण बनने और अपने प्रोजेक्ट में वैकल्पिक कार्यान्वयन दृष्टिकोणों की खोज करने में मदद करती हैं।

- [Java में CSS का उपयोग कैसे करें – HTML लोड करें, लिंक गिनें और XPath मूल्यांकन करें](/html/english/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/)
- [Java में HTML पार्स कैसे करें – HTML लेखों से टेक्स्ट निकालें](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Java के साथ नया HTML एलिमेंट बनाएं – पूर्ण Aspose.HTML गाइड](/html/english/java/editing-html-documents/create-new-html-element-with-java-full-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
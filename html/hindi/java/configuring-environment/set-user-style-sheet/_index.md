---
date: 2025-12-05
description: Aspose.HTML for Java में एक कस्टम यूज़र स्टाइलशीट सेट करके HTML से PDF
  बनाना सीखें, और यूज़र एजेंट सर्विस के साथ आसानी से HTML को PDF में बदलें।
language: hi
linktitle: Set User Style Sheet in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: HTML से PDF बनाएं – Aspose.HTML for Java में उपयोगकर्ता शैली पत्रक सेट करें
url: /java/configuring-environment/set-user-style-sheet/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML से PDF बनाएं – Aspose.HTML for Java में यूज़र स्टाइल शीट सेट करें

## परिचय
इस ट्यूटोरियल में आप सीखेंगे कि कैसे Aspose.HTML for Java का उपयोग करके **HTML से PDF बनाएं** और साथ ही एक कस्टम यूज़र स्टाइलशीट लागू करें।  
क्या आपने कभी अपने HTML दस्तावेज़ों की रूप‑रंग को अपनी अनोखी शैली से बदलने की इच्छा महसूस की है? कल्पना कीजिए आप एक वेबपेज बना रहे हैं और आपको हेडिंग्स को किसी विशिष्ट रंग से उभारना है या पैराग्राफ़ को सभी डिवाइसों पर समान दिखाना है। यहीं पर *यूज़र स्टाइलशीट* और **User Agent Service** काम आती है। हम हर कदम को विस्तार से देखेंगे—एक साधारण HTML फ़ाइल लिखने से लेकर यूज़र एजेंट को कॉन्फ़िगर करने तक, और अंत में **HTML को PDF में बदलने** तक—ताकि आप तुरंत परिणाम देख सकें।

## त्वरित उत्तर
- **“HTML से PDF बनाना” का क्या अर्थ है?** इसका मतलब है HTML दस्तावेज़ (CSS, इमेज, फ़ॉन्ट आदि सहित) को रेंडर करके उसका विज़ुअल आउटपुट PDF फ़ाइल के रूप में सहेजना।  
- **कौन सा Aspose घटक आवश्यक है?** Aspose.HTML for Java लाइब्रेरी में रूपांतरण इंजन और User Agent Service दोनों शामिल हैं।  
- **क्या परीक्षण के लिए लाइसेंस चाहिए?** विकास के लिए फ्री ट्रायल काम करता है; उत्पादन के लिए वाणिज्यिक लाइसेंस आवश्यक है।  
- **क्या मैं बाहरी CSS फ़ाइल उपयोग कर सकता हूँ?** हाँ – आप सामान्य ब्राउज़र की तरह बाहरी स्टाइलशीट लिंक कर सकते हैं।  
- **रूपांतरण में कितना समय लगता है?** इस गाइड में दिखाए गए सरल दस्तावेज़ के लिए रूपांतरण एक सेकंड से कम में पूरा हो जाता है।

## आवश्यकताएँ
इस कोड को चलाने से पहले सुनिश्चित करें कि आपके पास निम्नलिखित हैं:

1. **Aspose.HTML for Java** – नवीनतम JAR को [Aspose releases page](https://releases.aspose.com/html/java/) से डाउनलोड करें।  
2. **Java Development Kit (JDK) 8+** – सुनिश्चित करें कि `java -version` कमांड 8 या उससे ऊपर दिखाता है।  
3. **IDE** – IntelliJ IDEA, Eclipse, या NetBeans में से कोई भी काम करेगा।  
4. **बुनियादी HTML/CSS ज्ञान** – उपयोगी है लेकिन अनिवार्य नहीं।

## पैकेज आयात करें
शुरुआत करने के लिए आवश्यक Java क्लासेज़ को आयात करें। इस उदाहरण के लिए आपको केवल `java.io.IOException` को स्पष्ट रूप से आयात करना है; Aspose क्लासेज़ को बाद में पूरी‑योग्य नामों से संदर्भित किया जाएगा।

```java
import java.io.IOException;
```

## चरण 1: एक साधारण HTML दस्तावेज़ बनाएं
पहले, हम एक न्यूनतम HTML फ़ाइल (`document.html`) लिखेंगे जो हमारे PDF रूपांतरण का स्रोत होगी।

```java
String code = "<h1>User Agent Service</h1>\r\n" +
        "<p>The User Agent Service allows you to specify a custom user stylesheet, a primary character set for the document, language, and fonts settings.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **प्रो टिप:** HTML फ़ाइल को अपने Java स्रोत फ़ाइलों के समान डायरेक्टरी में रखें ताकि पाथ‑संबंधी समस्याएँ न आएँ।

## चरण 2: Aspose.HTML कॉन्फ़िगरेशन सेट करें
एक `Configuration` ऑब्जेक्ट बनाएं। यह ऑब्जेक्ट सभी सेवाओं (जिसमें User Agent Service भी शामिल है) के लिए कंटेनर के रूप में कार्य करता है जिसे आप बाद में उपयोग करेंगे।

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## चरण 3: User Agent Service तक पहुँचें  
**User Agent Service** आपको कस्टम स्टाइलशीट इंजेक्ट करने, डिफ़ॉल्ट कैरेक्टर सेट सेट करने, और अन्य रेंडरिंग विकल्पों को नियंत्रित करने की सुविधा देता है।

```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

## चरण 4: यूज़र स्टाइलशीट परिभाषित करें और लागू करें  
अब हम CSS नियम प्रदान करेंगे जो HTML को रेंडर करते समय लागू होंगे। यहाँ हम **User Agent Service** का उपयोग करके स्टाइलशीट सेट करेंगे।

```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; font-size:2em; }\r\n" +
        "p { background-color:GhostWhite; color:SlateGrey; font-size:1.2em; }\r\n");
```

> **यह क्यों महत्वपूर्ण है:** यूज़र‑एजेंट स्तर पर स्टाइलशीट लागू करने से यह सुनिश्चित होता है कि शैली मूल HTML में CSS फ़ाइल का उल्लेख न होने पर भी लागू रहे।

## चरण 5: कस्टम कॉन्फ़िगरेशन के साथ HTML दस्तावेज़ लोड करें  
फ़ाइल पाथ और `Configuration` इंस्टेंस दोनों को `HTMLDocument` कंस्ट्रक्टर में पास करें। इससे यूज़र स्टाइलशीट दस्तावेज़ से बंध जाएगी।

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
```

## चरण 6: HTML को PDF में बदलें  
दस्तावेज़ पूरी तरह स्टाइल हो जाने के बाद, स्थैतिक `convertHTML` मेथड को कॉल करके **HTML को PDF में बदलें**। `PdfSaveOptions` ऑब्जेक्ट आपको आउटपुट (जैसे पेज साइज, कम्प्रेशन) को फाइन‑ट्यून करने की अनुमति देता है।

```java
com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.PdfSaveOptions(),
        "user-agent-stylesheet_out.pdf"
);
```

> **परिणाम:** `user-agent-stylesheet_out.pdf` में हेडिंग ब्राउन रंग में और पैराग्राफ़ GhostWhite बैकग्राउंड के साथ दिखेगा, बिल्कुल वही जैसा स्टाइलशीट में परिभाषित किया गया है।

## चरण 7: संसाधनों को साफ़ करें  
नेटीव मेमोरी को मुक्त करने के लिए हमेशा Aspose ऑब्जेक्ट्स को डिस्पोज़ करें।

```java
if (document != null) {
    document.dispose();
}
if (configuration != null) {
    configuration.dispose();
}
```

## सामान्य समस्याएँ और समाधान
| समस्या | कारण | समाधान |
|-------|-------|-----|
| **खाली PDF आउटपुट** | स्टाइलशीट लागू नहीं हुई या दस्तावेज़ कॉन्फ़िगरेशन के साथ लोड नहीं हुआ। | सुनिश्चित करें कि `configuration` को `HTMLDocument` में पास किया गया है और `setUserStyleSheet` को लोड करने से पहले कॉल किया गया है। |
| **Unsupported CSS property warning** | Aspose.HTML कुछ उन्नत CSS फीचर्स को सपोर्ट नहीं करता। | केवल Aspose.HTML दस्तावेज़ में सूचीबद्ध CSS प्रॉपर्टीज़ का उपयोग करें या सरल स्टाइल्स पर वापस जाएँ। |
| **FileNotFoundException** | `document.html` का पाथ गलत है। | पूर्ण (absolute) पाथ उपयोग करें या HTML फ़ाइल को प्रोजेक्ट रूट में रखें। |

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: क्या मैं विभिन्न HTML तत्वों के लिए अलग‑अलग स्टाइल लागू कर सकता हूँ?**  
उत्तर: बिल्कुल! आप यूज़र स्टाइलशीट में जितनी चाहें CSS नियम जोड़ सकते हैं।

**प्रश्न: यदि मुझे स्टाइलशीट को डायनामिक रूप से बदलना हो तो क्या करें?**  
उत्तर: नया `HTMLDocument` बनाने से पहले `setUserStyleSheet` को फिर से कॉल करें; नई स्टाइल्स अगले रूपांतरण में लागू होंगी।

**प्रश्न: क्या Aspose.HTML for Java के साथ बाहरी CSS फ़ाइलें उपयोग की जा सकती हैं?**  
उत्तर: हाँ – आप HTML में बाहरी स्टाइलशीट लिंक कर सकते हैं या उसकी सामग्री लोड करके `setUserStyleSheet` को पास कर सकते हैं।

**प्रश्न: Aspose.HTML असमर्थित CSS प्रॉपर्टीज़ को कैसे संभालता है?**  
उत्तर: असमर्थित प्रॉपर्टीज़ को नजरअंदाज़ किया जाता है, जिससे बाकी स्टाइलशीट बिना त्रुटि के रेंडर होती है।

**प्रश्न: क्या मैं HTML को PDF के अलावा अन्य फॉर्मेट में भी बदल सकता हूँ?**  
उत्तर: हाँ, Aspose.HTML XPS, TIFF, PNG, JPEG आदि फॉर्मेट में रूपांतरण का समर्थन करता है, उचित `SaveOptions` क्लास का उपयोग करके।

## निष्कर्ष
आपने अब देखा कि कैसे Aspose.HTML for Java के साथ कस्टम यूज़र स्टाइलशीट सेट करके **HTML से PDF बनाएं**। यह वर्कफ़्लो आपको उत्पन्न PDF की दृश्य उपस्थिति पर पूर्ण नियंत्रण देता है, जिससे यह स्वचालित रिपोर्ट जनरेशन, इनवॉइस निर्माण, या किसी भी ऐसे परिदृश्य में आदर्श बन जाता है जहाँ स्थिर स्टाइलिंग आवश्यक है। अधिक जटिल CSS, बाहरी फ़ॉन्ट या अतिरिक्त रूपांतरण फ़ॉर्मेट के साथ प्रयोग करने के लिए स्वतंत्र महसूस करें और इस बुनियाद को आगे विस्तारित करें।

---

**अंतिम अपडेट:** 2025-12-05  
**परीक्षण किया गया:** Aspose.HTML for Java 24.11 (लेखन के समय नवीनतम)  
**लेखक:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
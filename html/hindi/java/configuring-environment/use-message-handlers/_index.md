---
date: 2026-02-10
description: Aspose का उपयोग करके टूटे हुए लिंक को संभालना, HTML को PNG में बदलना
  और Aspose.HTML for Java के साथ Java में HTML दस्तावेज़ लोड करना सीखें।
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Aspose.HTML संदेश हैंडलर्स के साथ जावा में HTML को PNG में बदलें
url: /hi/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML मेसेज हैंडलर्स के साथ Java में HTML को PNG में बदलें

## परिचय
इस ट्यूटोरियल में आप **HTML को PNG में कैसे बदलें** और अनुपलब्ध संसाधनों को सुगमता से संभालें, यह Aspose.HTML for Java का उपयोग करके सीखेंगे। हम एक छोटा HTML पेज बनाएँगे जो एक गैर‑मौजूद इमेज की ओर संकेत करता है, **कस्टम मेसेज हैंडलर** को **नेटवर्क अनुरोधों को इंटरसेप्ट** करने के लिए सेट करेंगे, **नेटवर्क सर्विस** को कॉन्फ़िगर करेंगे, दस्तावेज़ लोड करेंगे, और अंत में **HTML से इमेज रूपांतरण** करेंगे। अंत तक आपके पास **broken links java** को संभालने और उच्च‑गुणवत्ता वाले PNG आउटपुट के लिए एक ठोस पैटर्न होगा—रिपोर्ट, थंबनेल, या ईमेल प्रीव्यू के लिए एकदम उपयुक्त।

## त्वरित उत्तर
- **मेसेज हैंडलर क्या करता है?** यह नेटवर्क ऑपरेशन्स (जैसे इमेज अनुरोध) को इंटरसेप्ट करता है और आपको 404 जैसे स्टेटस कोड पर प्रतिक्रिया देने की अनुमति देता है।  
- **क्या Aspose.HTML HTML को PNG में बदल सकता है?** हाँ—`Converter.convertHTML` एक ही कॉल में रूपांतरण करता है।  
- **क्या इस उदाहरण के लिए लाइसेंस चाहिए?** एक अस्थायी लाइसेंस मूल्यांकन सीमाओं को हटाता है; उत्पादन उपयोग के लिए स्थायी लाइसेंस आवश्यक है।  
- **कौन सा Java संस्करण काम करता है?** कोई भी JDK 8+ (उदाहरण JDK 11 पर चलता है)।  
- **क्या मैं नेटवर्क सर्विस को कॉन्फ़िगर कर सकता हूँ?** बिल्कुल—`configuration.getService(INetworkService.class)` का उपयोग करके अपने हैंडलर को जोड़ें।

## पूर्वापेक्षाएँ
शुरू करने से पहले सुनिश्चित करें कि आपके पास निम्नलिखित तैयार हैं:

1. **Java Development Kit (JDK)** – इसे [Oracle वेबसाइट](https://www.oracle.com/java/technologies/javase-downloads.html) से डाउनलोड करें।  
2. **Aspose.HTML for Java** – लाइब्रेरी को [Aspose रिलीज़ पेज](https://releases.aspose.com/html/java/) से प्राप्त करें।  
3. **IDE** – IntelliJ IDEA, Eclipse, या NetBeans पर्याप्त हैं।  
4. **बेसिक Java ज्ञान** – आपको क्लासेज, try‑with‑resources, और एक्सेप्शन हैंडलिंग की समझ होनी चाहिए।  
5. **अस्थायी लाइसेंस** – यदि आप ट्रायल पर हैं, तो वाटरमार्क से बचने के लिए एक [अस्थायी लाइसेंस](https://purchase.aspose.com/temporary-license/) प्राप्त करें।

## पैकेज इम्पोर्ट करें
सबसे पहले, फ़ाइल हैंडलिंग के लिए आवश्यक Java I/O क्लास को इम्पोर्ट करें। बाकी Aspose क्लासेज़ को बाद में पूर्ण‑नाम से संदर्भित किया जाएगा, जिससे इम्पोर्ट सूची साफ़ रहती है।

```java
import java.io.IOException;
```

## चरण 1: HTML कोड तैयार करें
हम एक न्यूनतम HTML स्निपेट बनाते हैं जो जानबूझकर एक गायब इमेज को रेफ़र करता है। इससे जब इंजन संसाधन लाने की कोशिश करेगा, हमारा हैंडलर ट्रिगर हो जाएगा।

```java
String code = "<img src='missing.jpg'>";
```

## चरण 2: HTML कोड को फ़ाइल में लिखें
अब हम स्निपेट को *document.html* में सहेजते हैं। try‑with‑resources ब्लॉक का उपयोग `FileWriter` को सही ढंग से बंद करने को सुनिश्चित करता है।

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## चरण 3: कस्टम मेसेज हैंडलर लिखें
अब हम एक **कस्टम मेसेज हैंडलर** बनाते हैं जो प्रत्येक नेटवर्क अनुरोध की HTTP स्थिति जाँचता है। यदि प्रतिक्रिया `200` नहीं है, तो हम एक मित्रवत चेतावनी लॉग करते हैं। अंत में `invoke(context);` कॉल को देखें—यह अनुरोध को श्रृंखला में अगले हैंडलर को फ़ॉरवर्ड करता है, जिससे पुनरावृत्ति नहीं होती।

```java
com.aspose.html.net.MessageHandler handler = new com.aspose.html.net.MessageHandler() {
    @Override
    public void invoke(com.aspose.html.net.INetworkOperationContext context) {
        if (context.getResponse().getStatusCode() != 200) {
            System.out.println(String.format("File '%s' Not Found", context.getRequest().getRequestUri().toString()));
        }
        invoke(context);
    }
};
```

## चरण 4: नेटवर्क सर्विस को कॉन्फ़िगर करें
Aspose.HTML को हमारे हैंडलर से अवगत कराने के लिए, हम `Configuration` इंस्टेंस से **नेटवर्क सर्विस** प्राप्त करते हैं और हैंडलर को उसकी कलेक्शन में जोड़ते हैं। यही वह कदम है जहाँ हम **नेटवर्क सर्विस** को कस्टम व्यवहार के लिए **कॉन्फ़िगर** करते हैं।

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## चरण 5: HTML दस्तावेज़ लोड करें
कॉन्फ़िगरेशन तैयार होने के बाद, हम *document.html* लोड करते हैं। इंजन अब हमारे नेटवर्क सर्विस का उपयोग करता है, इसलिए गायब इमेज अनुरोध हमारे द्वारा अभी जोड़े गए हैंडलर द्वारा इंटरसेप्ट हो जाता है।

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
try {
    // Additional operations will go here
} finally {
    if (document != null) {
        document.dispose();
    }
}
```

## चरण 6: HTML को PNG में बदलें
यह **html to image conversion** प्रक्रिया का मुख्य भाग है। `Converter.convertHTML` मेथड लोड किए गए `HTMLDocument`, वैकल्पिक `ImageSaveOptions` (जहाँ आप DPI या क्वालिटी समायोजित कर सकते हैं), और आउटपुट फ़ाइल नाम लेता है।

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## चरण 7: संसाधनों को साफ़ करें
अच्छी Java प्रैक्टिस यह है कि सभी नेटिव संसाधनों को रिलीज़ किया जाए। `finally` ब्लॉक सुनिश्चित करता है कि `Configuration` को डिस्पोज़ किया जाए, भले ही कोई एक्सेप्शन उभरे।

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## मेसेज हैंडलर्स क्यों उपयोग करें?
मेसेज हैंडलर्स आपको **प्रत्येक नेटवर्क अनुरोध** पर **सूक्ष्म नियंत्रण** देते हैं—चाहे वह इमेज, CSS, JavaScript, या फ़ॉन्ट फ़ाइल हो। लाइब्रेरी को चुपचाप फेल होने देने के बजाय, आप गायब एसेट्स को लॉग कर सकते हैं, फ़ॉलबैक कंटेंट प्रदान कर सकते हैं, या यहाँ तक कि अनुरोध को री‑ट्राई भी कर सकते हैं। यह आपके HTML प्रोसेसिंग पाइपलाइन को **मज़बूत**, **प्रोडक्शन‑रेडी**, और डिबग करने में आसान बनाता है।

## सामान्य समस्याएँ और समाधान
- **हैंडलर पुनरावृत्ति** – अनंत लूप से बचने के लिए `invoke(context);` केवल एक बार कॉल करें।  
- **लाइसेंस अनुपलब्ध** – वैध लाइसेंस के बिना आउटपुट PNG में वाटरमार्क रहेगा।  
- **गलत फ़ाइल पाथ** – `document.html` लोड करते समय पूर्ण पाथ उपयोग करें या कार्य निर्देशिका सही सेट करें।  
- **असमर्थित संसाधन प्रकार** – सुनिश्चित करें कि आप जिस संसाधन को इंटरसेप्ट करना चाहते हैं (इमेज, CSS आदि) वास्तव में HTML इंजन द्वारा अनुरोधित है।

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: क्या मैं कई मेसेज हैंडलर्स को चेन कर सकता हूँ?**  
उत्तर: हाँ, आप `network.getMessageHandlers()` कलेक्शन में कई हैंडलर्स जोड़ सकते हैं; वे जोड़े गए क्रम में निष्पादित होंगे।

**प्रश्न: क्या हैंडलर CSS या स्क्रिप्ट संसाधनों के लिए भी काम करता है?**  
उत्तर: बिल्कुल—HTML इंजन द्वारा किया गया कोई भी नेटवर्क अनुरोध (इमेज, CSS, JS, फ़ॉन्ट) हैंडलर से गुजरता है।

**प्रश्न: मैं HTTP अनुरोध को भेजे जाने से पहले कैसे बदलूँ?**  
उत्तर: `invoke(context)` कॉल करने से पहले `context.getRequest()` को संशोधित करने वाला हैंडलर इम्प्लीमेंट करें।

**प्रश्न: क्या विशिष्ट URLs के लिए चेतावनी को दबाया जा सकता है?**  
उत्तर: हैंडलर के भीतर `context.getRequest().getRequestUri()` की जाँच करके शर्तीय रूप से लॉग को स्किप करें।

**प्रश्न: इन API के लिए Aspose.HTML का कौन सा संस्करण आवश्यक है?**  
उत्तर: कोड Aspose.HTML for Java 22.10 और बाद के संस्करणों के साथ काम करता है।

## निष्कर्ष
अब आपके पास **HTML को PNG में बदलने** और **कस्टम मेसेज हैंडलर** के साथ **नेटवर्क अनुरोधों को इंटरसेप्ट** करने तथा **broken links java** को संभालने का एक पूर्ण, अंत‑से‑अंत उदाहरण है। नेटवर्क सर्विस को कॉन्फ़िगर करके, दस्तावेज़ लोड करके, और कन्वर्टर को कॉल करके, आप किसी भी Java एप्लिकेशन में विश्वसनीय रूप से PNG थंबनेल या पूर्ण‑पृष्ठ स्क्रीनशॉट जनरेट कर सकते हैं।

---

**अंतिम अपडेट:** 2026-02-10  
**टेस्टेड विथ:** Aspose.HTML for Java 24.11  
**लेखक:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
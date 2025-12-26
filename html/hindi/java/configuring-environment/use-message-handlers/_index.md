---
date: 2025-12-10
description: Aspose का उपयोग करके टूटे हुए लिंक को संभालना, HTML को PNG में बदलना
  और Aspose.HTML for Java के साथ Java में HTML दस्तावेज़ लोड करना सीखें।
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: जावा में Aspose.HTML संदेश हैंडलर्स का उपयोग कैसे करें
url: /hi/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use Aspose.HTML Message Handlers in Java

## Introduction
इस ट्यूटोरियल में, **how to use aspose** को HTML में लापता संसाधनों को संभालने के लिए चरण‑बद्ध तरीके से दिखाया गया है। हम एक साधारण HTML दस्तावेज़ बनाएँगे जिसमें एक लापता इमेज का संदर्भ होगा, एक कस्टम मैसेज हैंडलर संलग्न करेंगे, और यह दिखाएँगे कि **load html document java** को कैसे लोड किया जाए जबकि टूटे हुए लिंक को सुगमता से संभाला जाए। अंत तक, आप देखेंगे कि Aspose.HTML का उपयोग करके **convert html to png** कैसे किया जाता है, जिससे आपको Java में HTML‑से‑इमेज रूपांतरण की पूरी तस्वीर मिल जाएगी।

## Quick Answers
- **Message handler का मुख्य उद्देश्य क्या है?** नेटवर्क ऑपरेशन्स को इंटरसेप्ट करना और लापता संसाधनों जैसे स्टेटस कोड पर प्रतिक्रिया देना।  
- **क्या Aspose.HTML HTML को PNG में बदल सकता है?** हाँ, `Converter.convertHTML` का उपयोग करके आप HTML को इमेज में बदल सकते हैं।  
- **क्या इस उदाहरण के लिए लाइसेंस की आवश्यकता है?** एक टेम्पररी लाइसेंस मूल्यांकन सीमाओं को हटाता है; उत्पादन के लिए एक स्थायी लाइसेंस आवश्यक है।  
- **कौन सा Java संस्करण समर्थित है?** कोई भी JDK 8+ (ट्यूटोरियल JDK 11 का उपयोग करता है)।  
- **क्या कई टूटे हुए लिंक को संभालना संभव है?** बिल्कुल – आप विभिन्न परिदृश्यों को प्रबंधित करने के लिए कई हैंडलर को चेन कर सकते हैं।

## Prerequisites
स्टेप‑बाय‑स्टेप गाइड शुरू करने से पहले, सुनिश्चित करें कि आपके पास सभी आवश्यक चीज़ें हैं:
1. Java Development Kit (JDK): सुनिश्चित करें कि आपके सिस्टम पर JDK स्थापित है। आप इसे [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html) से डाउनलोड कर सकते हैं।  
2. Aspose.HTML for Java: आपको Aspose.HTML for Java स्थापित होना चाहिए। आप इसे [Aspose releases page](https://releases.aspose.com/html/java/) से डाउनलोड कर सकते हैं।  
3. IDE: अपने पसंदीदा Java Integrated Development Environment (IDE) जैसे IntelliJ IDEA, Eclipse, या NetBeans का उपयोग करें।  
4. Basic Knowledge of Java: Java प्रोग्रामिंग की बुनियादी समझ इस ट्यूटोरियल को प्रभावी रूप से फॉलो करने के लिए आवश्यक है।  
5. Temporary License: यदि आप Aspose.HTML का ट्रायल संस्करण उपयोग कर रहे हैं, तो विकास के दौरान किसी भी सीमा से बचने के लिए एक [temporary license](https://purchase.aspose.com/temporary-license/) प्राप्त करने पर विचार करें।

## Import Packages
शुरू करने से पहले, सुनिश्चित करें कि आवश्यक पैकेज आपके Java प्रोजेक्ट में इम्पोर्ट किए गए हैं। नीचे आवश्यक इम्पोर्ट्स दिए गए हैं:
```java
import java.io.IOException;
```
ये इम्पोर्ट्स आपको नेटवर्क ऑपरेशन्स को संभालने, HTML दस्तावेज़ बनाने, और HTML‑to‑PNG रूपांतरण करने के लिए आवश्यक क्लास और मेथड्स तक पहुंच प्रदान करेंगे।

## Step 1: Prepare the HTML Code
सबसे पहले हमें एक साधारण HTML स्निपेट चाहिए जो एक इमेज फ़ाइल को संदर्भित करता हो। हम जानबूझकर एक ऐसी इमेज का संदर्भ देंगे जो मौजूद नहीं है, ताकि त्रुटि हैंडलिंग मैकेनिज़्म ट्रिगर हो सके।
```java
String code = "<img src='missing.jpg'>";
```
यह कोड एक `<img>` टैग बनाता है जो `missing.jpg` की ओर इशारा करता है। क्योंकि इमेज मौजूद नहीं है, नेटवर्क सर्विस एक गैर‑200 स्टेटस कोड लौटाएगी, जिसे हमारा कस्टम हैंडलर पकड़ लेगा।

## Step 2: Write the HTML Code to a File
अब हमें HTML स्निपेट को स्थायी रूप से सहेजना होगा ताकि Aspose.HTML इसे दस्तावेज़ के रूप में लोड कर सके।
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```
`FileWriter` का उपयोग करके हम HTML को **document.html** में सहेजते हैं। यह फ़ाइल बाद में **load html document java** चरण के लिए स्रोत बन जाती है।

## Step 3: Create a Custom Message Handler
अब हम एक कस्टम मैसेज हैंडलर बनाएँगे जो तब प्रतिक्रिया देगा जब इमेज नहीं मिल पाए। हैंडलर HTTP स्टेटस कोड जांचता है और एक मित्रवत संदेश प्रिंट करता है।
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
`invoke` मेथड `context.getResponse().getStatusCode()` की जाँच करता है। यदि यह **200** नहीं है, तो हम स्पष्ट रूप से चेतावनी देते हैं कि फ़ाइल लापता है। अंतिम `invoke(context);` कॉल अगले हैंडलर को नियंत्रण पास कर देती है।

## Step 4: Configure the Network Service
Aspose.HTML को हमारे हैंडलर के बारे में बताने के लिए, हम इसे `Configuration` क्लास के माध्यम से नेटवर्क सर्विस में रजिस्टर करते हैं।
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```
यहाँ हम एक `Configuration` इंस्टेंस बनाते हैं, `INetworkService` प्राप्त करते हैं, और हमारे कस्टम हैंडलर को उसकी कलेक्शन में जोड़ते हैं। इससे सुनिश्चित होता है कि किसी भी नेटवर्क अनुरोध, जैसे इमेज लोड करना, के दौरान हैंडलर चलाया जाएगा।

## Step 5: Load the HTML Document
कॉन्फ़िगरेशन तैयार होने के बाद, हम पहले बनाए गए HTML फ़ाइल को लोड कर सकते हैं। यह चरण **load html document java** को दर्शाता है जबकि लापता इमेज हमारे हैंडलर को ट्रिगर करती है।
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
`HTMLDocument` कंस्ट्रक्टर फ़ाइल पाथ और कस्टम `configuration` दोनों प्राप्त करता है। जब दस्तावेज़ `<img>` टैग को पार्स करता है, नेटवर्क सर्विस `missing.jpg` को फ़ेच करने की कोशिश करती है, 404 प्राप्त करती है, और हमारा हैंडलर चेतावनी प्रिंट करता है।

## Step 6: Convert HTML to PNG
Aspose.HTML की व्यापक क्षमताओं को दिखाने के लिए, हम लोड किए गए दस्तावेज़ को PNG इमेज में बदलेंगे। यह एक क्लासिक **convert html to png** परिदृश्य है।
```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```
`Converter.convertHTML` `HTMLDocument`, वैकल्पिक `ImageSaveOptions` (जहाँ आप DPI, क्वालिटी आदि सेट कर सकते हैं), और आउटपुट फ़ाइलनाम लेता है। परिणामस्वरूप रेंडर किए गए HTML की एक रास्टर इमेज बनती है।

## Step 7: Clean Up Resources
किसी भी Java एप्लिकेशन में उचित संसाधन प्रबंधन आवश्यक है। हम मेमोरी लीक से बचने के लिए `Configuration` और `HTMLDocument` दोनों को डिस्पोज़ करते हैं।
```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```
क्लीन‑अप को `finally` ब्लॉक में रखकर यह सुनिश्चित किया जाता है कि पहले कोई एक्सेप्शन आए भी या न आए, क्लीन‑अप हमेशा निष्पादित हो।

## Why Use Message Handlers?
मैसेज हैंडलर आपको **handle broken links java** जैसे नेटवर्क ऑपरेशन्स पर सूक्ष्म नियंत्रण देते हैं। लाइब्रेरी को चुपचाप फेल होने देने के बजाय, आप लॉग कर सकते हैं, री‑ट्राई कर सकते हैं, संसाधनों को बदल सकते हैं, या फॉलबैक कंटेंट प्रदान कर सकते हैं—जिससे आपका HTML प्रोसेसिंग मजबूत और प्रोडक्शन‑रेडी बन जाता है।

## Common Issues and Solutions
- **Handler recursion** – अनंत लूप से बचने के लिए `invoke(context);` को केवल एक बार कॉल करें।  
- **Missing license** – वैध लाइसेंस के बिना, रूपांतरण में वॉटरमार्क वाली इमेज बन सकती है।  
- **File path errors** – `document.html` लोड करते समय पूर्ण पाथ उपयोग करें या कार्य निर्देशिका को सही ढंग से सेट करें।

## Frequently Asked Questions

**Q: क्या मैं कई मैसेज हैंडलर चेन कर सकता हूँ?**  
A: हाँ, आप `network.getMessageHandlers()` कलेक्शन में कई हैंडलर जोड़ सकते हैं; वे जोड़े जाने के क्रम में निष्पादित होंगे।

**Q: क्या हैंडलर CSS या स्क्रिप्ट संसाधनों के लिए भी काम करता है?**  
A: बिल्कुल—HTML इंजन द्वारा किए गए किसी भी नेटवर्क अनुरोध (इमेज, CSS, JS, फ़ॉन्ट) हैंडलर के माध्यम से पास होते हैं।

**Q: मैं HTTP अनुरोध को भेजे जाने से पहले कैसे बदलूँ?**  
A: `invoke(context)` कॉल करने से पहले `context.getRequest()` को संशोधित करने वाला हैंडलर इम्प्लीमेंट करें।

**Q: क्या विशिष्ट URLs के लिए चेतावनी को दबाना संभव है?**  
A: हैंडलर के अंदर `context.getRequest().getRequestUri()` की जाँच करके शर्तीय रूप से लॉग को स्किप कर सकते हैं।

**Q: इन APIs के लिए Aspose.HTML का कौन सा संस्करण आवश्यक है?**  
A: कोड Aspose.HTML for Java 22.10 और बाद के संस्करणों के साथ काम करता है।

## Conclusion
और इस प्रकार—Java में **how to use aspose** मैसेज हैंडलर पर एक व्यापक गाइड तैयार हो गया। हमने HTML फ़ाइल बनाना, **handle broken links java** के लिए कस्टम हैंडलर जोड़ना, दस्तावेज़ लोड करना, और **convert html to png** करना कवर किया। इस पैटर्न के साथ आप लापता संसाधनों को आत्मविश्वास से प्रबंधित कर सकते हैं, कस्टम नीतियों को लागू कर सकते हैं, और किसी भी Java एप्लिकेशन में Aspose.HTML की नेटवर्किंग क्षमताओं को विस्तारित कर सकते हैं।

---

**Last Updated:** 2025-12-10  
**Tested With:** Aspose.HTML for Java 24.11  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
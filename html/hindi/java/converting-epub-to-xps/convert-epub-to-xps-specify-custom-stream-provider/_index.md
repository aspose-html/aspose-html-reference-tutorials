---
date: 2026-01-07
description: Aspose.HTML for Java का उपयोग करके EPUB को XPS में आसानी से बदलें। सहज
  रूपांतरण प्रक्रिया के लिए इस चरण‑दर‑चरण गाइड का पालन करें।
linktitle: How to Convert EPUB to XPS with a Custom Stream Provider
second_title: Java HTML Processing with Aspose.HTML
title: कस्टम स्ट्रीम प्रोवाइडर के साथ EPUB को XPS में कैसे बदलें
url: /hi/java/converting-epub-to-xps/convert-epub-to-xps-specify-custom-stream-provider/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# कस्टम स्ट्रीम प्रोवाइडर के साथ EPUB को XPS में परिवर्तित करें

आज की डिजिटल प्रकाशन दुनिया में, **convert EPUB to XPS** एक सामान्य आवश्यकता है—चाहे आपको प्रिंटिंग, अभिलेखीयकरण, या Windows डिवाइसों के बीच साझा करने के लिए एक फिक्स्ड‑लेआउट प्रतिनिधित्व चाहिए। Aspose.HTML for Java इस रूपांतरण को सरल बनाता है, और एक कस्टम मेमोरी स्ट्रीम प्रोवाइडर का उपयोग करके आप पूरी प्रक्रिया को मेमोरी में रख सकते हैं, जो क्लाउड‑आधारित या उच्च‑प्रदर्शन परिदृश्यों के लिए उपयुक्त है। नीचे आपको शुरू करने के लिए सभी आवश्यक चीज़ें मिलेंगी, पूर्वापेक्षाओं से लेकर एक पूर्ण, चलाने योग्य उदाहरण तक।

## त्वरित उत्तर
- **परिवर्तन क्या उत्पन्न करता है?** एक XPS दस्तावेज़ जो लेआउट और फ़ॉन्ट को संरक्षित रखता है।  
- **क्या मुझे लाइसेंस की आवश्यकता है?** एक मुफ्त ट्रायल परीक्षण के लिए काम करता है; उत्पादन के लिए एक वाणिज्यिक लाइसेंस आवश्यक है।  
- **क्या मैं इसे कंटेनर में चला सकता हूँ?** हाँ—यदि आप सब कुछ मेमोरी में रखते हैं तो फ़ाइल सिस्टम में लिखने की आवश्यकता नहीं है।  
- **कौन सा Java संस्करण समर्थित है?** Java 8 या उससे ऊपर।  
- **क्या कस्टम स्ट्रीम प्रोवाइडर अनिवार्य है?** नहीं, लेकिन यह आपको मेमोरी उपयोग और आउटपुट हैंडलिंग पर पूर्ण नियंत्रण देता है।

## “convert EPUB to XPS” क्या है?
EPUB फ़ाइल को XPS में परिवर्तित करने से एक रीफ़्लोएबल ई‑बुक फ़ॉर्मेट को एक फिक्स्ड‑लेआउट, डिवाइस‑स्वतंत्र दस्तावेज़ में बदल दिया जाता है। XPS (XML Paper Specification) माइक्रोसॉफ्ट का PDF के समकक्ष है, उन परिदृश्यों के लिए आदर्श जहाँ आपको एक सटीक दृश्य प्रतिनिधित्व चाहिए जो प्लेटफ़ॉर्म के बीच नहीं बदलता।

## कस्टम स्ट्रीम प्रोवाइडर का उपयोग क्यों करें?
एक कस्टम `MemoryStreamProvider` आपको रूपांतरण परिणाम को डिस्क पर अस्थायी फ़ाइल लिखने के बजाय RAM में रखने देता है। यह दृष्टिकोण:
- I/O ओवरहेड को कम करता है।
- सर्वर‑लेस या माइक्रो‑सर्विस आर्किटेक्चर में प्रदर्शन को बेहतर बनाता है।
- आपको परिणाम को सीधे क्लाइंट, क्लाउड स्टोरेज, या किसी अन्य API में स्ट्रीम करने की लचीलापन देता है।

## पूर्वापेक्षाएँ
सफलतापूर्वक **convert EPUB to XPS** करने के लिए, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ मौजूद हैं:

### 1. Aspose.HTML for Java लाइब्रेरी  
आपके Java पर्यावरण में Aspose.HTML for Java लाइब्रेरी स्थापित और कॉन्फ़िगर होनी चाहिए। यदि आपने अभी तक नहीं किया है, तो आप लाइब्रेरी को [download link](https://releases.aspose.com/html/java/) से डाउनलोड कर सकते हैं।

### 2. इनपुट EPUB फ़ाइल  
आपको एक मौजूदा EPUB फ़ाइल चाहिए जिसे आप XPS में परिवर्तित करना चाहते हैं। सुनिश्चित करें कि आपके पास यह फ़ाइल रूपांतरण प्रक्रिया के लिए तैयार है।

अब जब आपके पास सभी पूर्वापेक्षाएँ हैं, चलिए चरण‑दर‑चरण रूपांतरण को देखते हैं।

## पैकेज आयात करें
शुरू करने से पहले, Aspose.HTML for Java की कार्यक्षमताओं का उपयोग करने के लिए आवश्यक पैकेज आयात करना सुनिश्चित करें।

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.XpsSaveOptions;
import com.aspose.html.saving.MemoryStreamProvider;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.InputStream;
```

## EPUB फ़ाइल खोलें
पहले, आपको पढ़ने के लिए मौजूदा EPUB फ़ाइल खोलनी होगी। इस चरण में, हम EPUB फ़ाइल तक पहुँचने के लिए `FileInputStream` का उपयोग करते हैं।

```java
try (FileInputStream fileInputStream = new FileInputStream("path/to/your/input.epub")) {
    // Your code for Step 1
}
```

## MemoryStreamProvider बनाएं
अगला, `MemoryStreamProvider` का एक इंस्टेंस बनाएं। यह ऑब्जेक्ट रूपांतरण आउटपुट को मेमोरी में रखेगा।

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
    // Your code for Step 2
}
```

## EPUB को XPS में परिवर्तित करें
अब, `Converter.convertEPUB` मेथड का उपयोग करके EPUB फ़ाइल को XPS में परिवर्तित करें। `MemoryStreamProvider` गंतव्य स्ट्रीम प्रदान करता है।

```java
Converter.convertEPUB(
    fileInputStream,
    new XpsSaveOptions(),
    streamProvider.getStream().findFirst().get()
);
```

## परिणामी डेटा प्राप्त करें
रूपांतरण पूर्ण होने के बाद, XPS डेटा वाले मेमोरी स्ट्रीम को प्राप्त करें।

```java
InputStream inputStream = streamProvider.getStream().findFirst().get();
```

## आउटपुट सहेजें (वैकल्पिक)
यदि आपको एक भौतिक फ़ाइल चाहिए—शायद डिबगिंग या ऑफ़लाइन निरीक्षण के लिए—तो मेमोरी स्ट्रीम को डिस्क पर लिखें। अधिकांश उत्पादन परिदृश्यों में आप इस चरण को छोड़ सकते हैं और डेटा को सीधे क्लाइंट में स्ट्रीम कर सकते हैं।

```java
try (FileOutputStream fileOutputStream = new FileOutputStream("path/to/your/output.xps")) {
    byte[] buffer = new byte[inputStream.available()];
    inputStream.read(buffer);
    fileOutputStream.write(buffer);
}
```

## पूर्ण स्रोत कोड
नीचे पूर्ण, चलाने‑के‑लिए‑तैयार उदाहरण है जो सभी भागों को एक साथ जोड़ता है। इसे अपनी परियोजना में कॉपी, पेस्ट और अनुकूलित करने में संकोच न करें।

```java
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of MemoryStreamProvider
            try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
                // Convert EPUB to XPS by using the MemoryStreamProvider
                com.aspose.html.converters.Converter.convertEPUB(
                        fileInputStream,
                        new com.aspose.html.saving.XpsSaveOptions(),
                        streamProvider.lStream
                );
                // Get access to the memory stream that contains the resulted data
                java.io.InputStream inputStream = streamProvider.lStream.stream().findFirst().get();
                // Flush the result data to the output file
                try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("output.xps"))) {
                    byte[] buffer = new byte[inputStream.available()];
                    inputStream.read(buffer);
                    fileOutputStream.write(buffer);
                }
            }
        }
```

## सामान्य समस्याएँ और समाधान
| समस्या | क्यों होता है | समाधान |
|-------|----------------|-----|
| **`java.lang.OutOfMemoryError`** | बड़े EPUB फ़ाइलें पूरी तरह मेमोरी में रखने पर डिफ़ॉल्ट हीप आकार से अधिक हो सकती हैं। | JVM हीप (`-Xmx`) बढ़ाएँ या संभव हो तो EPUB को हिस्सों में प्रोसेस करें। |
| XPS में फ़ॉन्ट गायब | EPUB में एम्बेड नहीं किए गए फ़ॉन्ट रूपांतरण मशीन पर उपलब्ध नहीं होते। | सुनिश्चित करें कि आवश्यक फ़ॉन्ट सर्वर पर स्थापित हों या उन्हें EPUB में एम्बेड करें। |
| `MemoryStreamProvider` से `UnsupportedOperationException` | पुराने Aspose.HTML संस्करण का उपयोग करना। | नवीनतम Aspose.HTML for Java रिलीज़ में अपडेट करें। |

## अक्सर पूछे जाने वाले प्रश्न

### 1. EPUB क्या है?
EPUB, जिसका पूरा नाम Electronic Publication है, ई‑बुक्स के लिए व्यापक रूप से उपयोग किया जाने वाला फ़ाइल फ़ॉर्मेट है। इसे विभिन्न उपकरणों, जैसे ई‑रीडर, टैबलेट और स्मार्टफ़ोन पर आसानी से पढ़ने योग्य बनाने के लिए डिज़ाइन किया गया है।

### 2. XPS क्या है?
XPS का अर्थ XML Paper Specification है, माइक्रोसॉफ्ट द्वारा बनाया गया एक दस्तावेज़ फ़ॉर्मेट। इसका उपयोग दस्तावेज़ों को समान रूप और लेआउट के साथ साझा करने और अभिलेखीय करने के लिए किया जाता है।

### 3. Aspose.HTML for Java का उपयोग क्यों करें?
Aspose.HTML for Java एक शक्तिशाली लाइब्रेरी है जो दस्तावेज़ हेरफेर, रूपांतरण और रेंडरिंग कार्यों को सरल बनाती है। यह विभिन्न दस्तावेज़ फ़ॉर्मेट्स के लिए व्यापक सुविधाएँ और समर्थन प्रदान करती है, जिससे यह डेवलपर्स के लिए एक मूल्यवान उपकरण बन जाता है।

### 4. क्या मैं Aspose.HTML for Java का उपयोग करके अन्य दस्तावेज़ फ़ॉर्मेट्स को परिवर्तित कर सकता हूँ?
हाँ, Aspose.HTML for Java विभिन्न दस्तावेज़ फ़ॉर्मेट्स के रूपांतरण का समर्थन करता है, जिसमें HTML, EPUB, XPS और अधिक शामिल हैं। यह दस्तावेज़ प्रबंधन के लिए एक बहुमुखी उपकरण है।

### 5. अतिरिक्त संसाधन और समर्थन कहाँ मिल सकते हैं?
दस्तावेज़ीकरण और समर्थन के लिए, [Aspose.HTML for Java documentation](https://reference.aspose.com/html/java/) और [support forum](https://forum.aspose.com/) पर जाएँ।

---

**अंतिम अपडेट:** 2026-01-07  
**परीक्षित संस्करण:** Aspose.HTML for Java 24.12 (latest at time of writing)  
**लेखक:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
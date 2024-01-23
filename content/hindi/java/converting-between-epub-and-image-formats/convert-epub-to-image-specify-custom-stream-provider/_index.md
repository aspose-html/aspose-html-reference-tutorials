---
title: जावा के लिए Aspose.HTML के साथ EPUB को छवियों में बदलें
linktitle: EPUB से छवि रूपांतरण के लिए कस्टम स्ट्रीम प्रदाता निर्दिष्ट करना
second_title: Aspose.HTML के साथ जावा HTML प्रोसेसिंग
description: जावा के लिए Aspose.HTML के साथ EPUB को छवियों में परिवर्तित करने का तरीका जानें। निर्बाध रूपांतरण के लिए चरण-दर-चरण मार्गदर्शिका।
type: docs
weight: 15
url: /hi/java/converting-between-epub-and-image-formats/convert-epub-to-image-specify-custom-stream-provider/
---
यदि आप जावा में EPUB फ़ाइलों को छवियों में परिवर्तित करना चाहते हैं, तो Java के लिए Aspose.HTML एक शक्तिशाली उपकरण है जो प्रक्रिया को सुव्यवस्थित कर सकता है। इस चरण-दर-चरण मार्गदर्शिका में, हम आपको इंस्टॉलेशन से लेकर आपकी EPUB फ़ाइलों को छवि फ़ाइलों में परिवर्तित करने तक की पूरी प्रक्रिया के बारे में बताएंगे। हम आपको आवश्यक शर्तें भी प्रदान करेंगे और आवश्यक पैकेज पेश करेंगे।

## आवश्यक शर्तें

इससे पहले कि आप रूपांतरण शुरू करें, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ मौजूद हैं:

- जावा डेवलपमेंट किट (जेडीके): आपके सिस्टम पर जावा एसई डेवलपमेंट किट (जेडीके) स्थापित होना चाहिए। आप इसे यहां से डाउनलोड कर सकते हैं[यहाँ](https://www.oracle.com/java/technologies/javase-downloads.html).

-  जावा के लिए Aspose.HTML: जावा लाइब्रेरी के लिए आपके पास Aspose.HTML होना आवश्यक है। यदि आपने पहले से नहीं किया है, तो आप इसे प्राप्त कर सकते हैं[यहाँ](https://releases.aspose.com/html/java/).

- EPUB फ़ाइल: वह EPUB फ़ाइल तैयार करें जिसे आप छवियों में कनवर्ट करना चाहते हैं।

## पैकेज आयात करें

अपने जावा प्रोजेक्ट में, आपको जावा के लिए Aspose.HTML से आवश्यक पैकेज आयात करने की आवश्यकता होगी। इन्हें अपने कोड में शामिल करना सुनिश्चित करें।

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.ImageSaveOptions;
import com.aspose.html.rendering.image.ImageFormat;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.InputStream;
```

## चरण-दर-चरण मार्गदर्शिका

आइए जावा के लिए Aspose.HTML का उपयोग करके EPUB फ़ाइल को छवियों में परिवर्तित करने की प्रक्रिया को कई चरणों में विभाजित करें:

### चरण 1: EPUB फ़ाइल खोलें

 आप इसका उपयोग करके पढ़ने के लिए मौजूदा EPUB फ़ाइल खोलकर शुरुआत करेंगे`FileInputStream`.

```java
try (FileInputStream fileInputStream = new FileInputStream("input.epub")) {
```

### चरण 2: एक मेमोरी स्ट्रीम प्रदाता बनाएं

 इसके बाद, का एक उदाहरण बनाएं`MemoryStreamProvider` रूपांतरण को सुविधाजनक बनाने के लिए.

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
```

### चरण 3: EPUB को छवि में बदलें

 अब, EPUB फ़ाइल का छवियों में वास्तविक रूपांतरण करने का समय आ गया है। उपयोग`Converter.convertEPUB` इस उद्देश्य के लिए आउटपुट स्वरूप को JPEG के रूप में निर्दिष्ट करने की विधि।

```java
Converter.convertEPUB(
    fileInputStream,
    new ImageSaveOptions(ImageFormat.Jpeg),
    streamProvider.getStream()
);
```

### चरण 4: परिणामी डेटा तक पहुंचें

रूपांतरण के बाद, आप परिणामी छवि डेटा वाली मेमोरी स्ट्रीम तक पहुंच सकते हैं। छवियों को संसाधित करने के लिए इन धाराओं के माध्यम से लूप करें।

```java
int size = streamProvider.getStream().size();
for (int i = 0; i < size; i++) {
    InputStream inputStream = streamProvider.getStream().get(i);

    // पृष्ठ को आउटपुट फ़ाइल में फ़्लश करें
    try (FileOutputStream fileOutputStream = new FileOutputStream("page_" + (i + 1) + ".jpg")) {
        byte[] buffer = new byte[inputStream.available()];
        inputStream.read(buffer);
        fileOutputStream.write(buffer);
    }
}
```

और बस! आपने जावा के लिए Aspose.HTML का उपयोग करके एक EPUB फ़ाइल को छवियों में सफलतापूर्वक परिवर्तित कर लिया है।

## निष्कर्ष

जावा के लिए Aspose.HTML EPUB फ़ाइलों को छवियों में परिवर्तित करने की प्रक्रिया को सरल बनाता है। इस गाइड में बताए गए चरणों के साथ, आप इस कार्य को जल्दी और प्रभावी ढंग से पूरा कर सकते हैं। निर्बाध रूपांतरण प्रक्रिया सुनिश्चित करने के लिए आवश्यक शर्तें पूरी करना और आवश्यक पैकेज आयात करना याद रखें।

## अक्सर पूछे जाने वाले प्रश्न

### Q1: क्या मैं जावा के लिए Aspose.HTML का निःशुल्क उपयोग कर सकता हूँ?

 A1: जावा के लिए Aspose.HTML एक व्यावसायिक लाइब्रेरी है, लेकिन आप इसकी विशेषताओं का पता लगा सकते हैं[मुफ्त परीक्षण](https://releases.aspose.com/html/java).

### Q2: क्या जावा के लिए Aspose.HTML के लिए कोई दस्तावेज़ उपलब्ध है?

 उ2: हाँ, आप व्यापक दस्तावेज़ पा सकते हैं[यहाँ](https://reference.aspose.com/html/java/).

### Q3: मैं जावा के लिए Aspose.HTML के लिए अस्थायी लाइसेंस कैसे प्राप्त कर सकता हूं?

 A3: आप अस्थायी लाइसेंस प्राप्त कर सकते हैं[यहाँ](https://purchase.aspose.com/temporary-license/).

### Q4: मुझे जावा के लिए Aspose.HTML के लिए समर्थन कहां मिल सकता है?

 A4: समर्थन और सामुदायिक चर्चा के लिए, पर जाएँ[Aspose मंचों](https://forum.aspose.com/).

### Q5: क्या मैं EPUB फ़ाइलों को अन्य छवि प्रारूपों में परिवर्तित कर सकता हूँ?

 A5: हाँ, आप आउटपुट स्वरूप को समायोजित करके अनुकूलित कर सकते हैं`ImageSaveOptions` . को बदलें`ImageFormat` अपने इच्छित प्रारूप में, जैसे पीएनजी या जीआईएफ।
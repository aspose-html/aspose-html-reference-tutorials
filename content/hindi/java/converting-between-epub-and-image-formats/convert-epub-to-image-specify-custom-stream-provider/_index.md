---
title: Java के लिए Aspose.HTML के साथ EPUB को छवियों में बदलें
linktitle: EPUB से छवि रूपांतरण के लिए कस्टम स्ट्रीम प्रदाता निर्दिष्ट करना
second_title: Aspose.HTML के साथ जावा HTML प्रसंस्करण
description: जानें कि Java के लिए Aspose.HTML के साथ EPUB को छवियों में कैसे परिवर्तित किया जाए। सहज रूपांतरण के लिए चरण-दर-चरण मार्गदर्शिका।
type: docs
weight: 15
url: /hi/java/converting-between-epub-and-image-formats/convert-epub-to-image-specify-custom-stream-provider/
---
यदि आप जावा में EPUB फ़ाइलों को छवियों में बदलना चाहते हैं, तो Aspose.HTML for Java एक शक्तिशाली उपकरण है जो इस प्रक्रिया को सरल बना सकता है। इस चरण-दर-चरण मार्गदर्शिका में, हम आपको इंस्टॉलेशन से लेकर आपकी EPUB फ़ाइलों को छवि फ़ाइलों में बदलने तक की पूरी प्रक्रिया से अवगत कराएँगे। हम आपको आवश्यक शर्तें भी प्रदान करेंगे और आवश्यक पैकेज पेश करेंगे।

## आवश्यक शर्तें

रूपांतरण आरंभ करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ मौजूद हैं:

- जावा डेवलपमेंट किट (JDK): आपके सिस्टम पर जावा SE डेवलपमेंट किट (JDK) इंस्टॉल होना चाहिए। आप इसे यहाँ से डाउनलोड कर सकते हैं[यहाँ](https://www.oracle.com/java/technologies/javase-downloads.html).

-  Aspose.HTML for Java: आपके पास Aspose.HTML for Java लाइब्रेरी होनी चाहिए। अगर आपके पास पहले से नहीं है, तो आप इसे प्राप्त कर सकते हैं[यहाँ](https://releases.aspose.com/html/java/).

- EPUB फ़ाइल: वह EPUB फ़ाइल तैयार करें जिसे आप छवियों में बदलना चाहते हैं।

## पैकेज आयात करें

अपने जावा प्रोजेक्ट में, आपको Aspose.HTML for Java से ज़रूरी पैकेज आयात करने होंगे। इन्हें अपने कोड में शामिल करना न भूलें।

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.ImageSaveOptions;
import com.aspose.html.rendering.image.ImageFormat;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.InputStream;
```

## चरण-दर-चरण मार्गदर्शिका

आइए Aspose.HTML for Java का उपयोग करके EPUB फ़ाइल को छवियों में परिवर्तित करने की प्रक्रिया को कई चरणों में विभाजित करें:

### चरण 1: EPUB फ़ाइल खोलें

 आप पढ़ने के लिए एक मौजूदा EPUB फ़ाइल खोलकर शुरुआत करेंगे`FileInputStream`.

```java
try (FileInputStream fileInputStream = new FileInputStream("input.epub")) {
```

### चरण 2: मेमोरी स्ट्रीम प्रदाता बनाएँ

 इसके बाद, इसका एक उदाहरण बनाएं`MemoryStreamProvider` रूपांतरण को सुविधाजनक बनाने के लिए.

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
```

### चरण 3: EPUB को छवि में बदलें

 अब, EPUB फ़ाइल को छवियों में वास्तविक रूप से परिवर्तित करने का समय आ गया है।`Converter.convertEPUB` इस प्रयोजन के लिए विधि का उपयोग किया गया है, जिसमें आउटपुट प्रारूप को JPEG के रूप में निर्दिष्ट किया गया है।

```java
Converter.convertEPUB(
    fileInputStream,
    new ImageSaveOptions(ImageFormat.Jpeg),
    streamProvider.getStream()
);
```

### चरण 4: परिणामी डेटा तक पहुंचें

रूपांतरण के बाद, आप परिणामी छवि डेटा वाली मेमोरी स्ट्रीम तक पहुँच सकते हैं। छवियों को संसाधित करने के लिए इन स्ट्रीम के माध्यम से लूप करें।

```java
int size = streamProvider.getStream().size();
for (int i = 0; i < size; i++) {
    InputStream inputStream = streamProvider.getStream().get(i);

    // पृष्ठ को आउटपुट फ़ाइल में फ्लश करें
    try (FileOutputStream fileOutputStream = new FileOutputStream("page_" + (i + 1) + ".jpg")) {
        byte[] buffer = new byte[inputStream.available()];
        inputStream.read(buffer);
        fileOutputStream.write(buffer);
    }
}
```

और बस! आपने Java के लिए Aspose.HTML का उपयोग करके EPUB फ़ाइल को सफलतापूर्वक छवियों में परिवर्तित कर लिया है।

## निष्कर्ष

Aspose.HTML for Java EPUB फ़ाइलों को छवियों में बदलने की प्रक्रिया को सरल बनाता है। इस गाइड में बताए गए चरणों के साथ, आप इस कार्य को तेज़ी से और प्रभावी ढंग से कर सकते हैं। एक सहज रूपांतरण प्रक्रिया सुनिश्चित करने के लिए आवश्यक शर्तों को पूरा करना और आवश्यक पैकेज आयात करना याद रखें।

## अक्सर पूछे जाने वाले प्रश्न

### प्रश्न 1: क्या मैं Java के लिए Aspose.HTML का निःशुल्क उपयोग कर सकता हूँ?

 A1: Aspose.HTML for Java एक व्यावसायिक लाइब्रेरी है, लेकिन आप इसकी विशेषताओं का पता लगा सकते हैं[मुफ्त परीक्षण](https://releases.aspose.com/html/java).

### प्रश्न 2: क्या Java के लिए Aspose.HTML हेतु कोई दस्तावेज़ उपलब्ध है?

 A2: हाँ, आप व्यापक दस्तावेज पा सकते हैं[यहाँ](https://reference.aspose.com/html/java/).

### प्रश्न 3: मैं Java के लिए Aspose.HTML हेतु अस्थायी लाइसेंस कैसे प्राप्त कर सकता हूं?

 A3: आप अस्थायी लाइसेंस प्राप्त कर सकते हैं[यहाँ](https://purchase.aspose.com/temporary-license/).

### प्रश्न 4: मुझे Java के लिए Aspose.HTML का समर्थन कहां मिल सकता है?

 A4: समर्थन और सामुदायिक चर्चा के लिए, यहां जाएं[Aspose फ़ोरम](https://forum.aspose.com/).

### प्रश्न 5: क्या मैं EPUB फ़ाइलों को अन्य छवि प्रारूपों में परिवर्तित कर सकता हूँ?

 A5: हाँ, आप आउटपुट प्रारूप को समायोजित करके अनुकूलित कर सकते हैं`ImageSaveOptions` । को बदलें`ImageFormat` अपने इच्छित प्रारूप में, जैसे PNG या GIF.
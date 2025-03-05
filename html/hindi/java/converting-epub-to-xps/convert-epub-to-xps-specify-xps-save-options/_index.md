---
title: EPUB से XPS में रूपांतरण के लिए XPS सेव विकल्प निर्दिष्ट करना
linktitle: EPUB से XPS में रूपांतरण के लिए XPS सेव विकल्प निर्दिष्ट करना
second_title: Aspose.HTML के साथ जावा HTML प्रसंस्करण
description: इस चरण-दर-चरण ट्यूटोरियल में जानें कि EPUB से XPS के लिए XPS सेव विकल्प निर्दिष्ट करने के लिए Aspose.HTML for Java का उपयोग कैसे करें। EPUB फ़ाइलों को सहजता से कनवर्ट करें।
type: docs
weight: 12
url: /hi/java/converting-epub-to-xps/convert-epub-to-xps-specify-xps-save-options/
---
वेब डेवलपमेंट की दुनिया में, EPUB फ़ाइलों को XPS फ़ॉर्मेट में बदलने की क्षमता एक मूल्यवान उपकरण है। Aspose.HTML for Java एक शक्तिशाली लाइब्रेरी है जो इस रूपांतरण को आसानी से करने की क्षमता प्रदान करती है। इस व्यापक ट्यूटोरियल में, हम आपको Aspose.HTML for Java का उपयोग करके EPUB से XPS के लिए XPS सेव विकल्पों को निर्दिष्ट करने की प्रक्रिया के माध्यम से मार्गदर्शन करेंगे।

## आवश्यक शर्तें

इससे पहले कि हम ट्यूटोरियल में आगे बढ़ें, कुछ पूर्व-आवश्यकताएं हैं जो आपके पास होनी चाहिए:

1. जावा डेवलपमेंट एनवायरनमेंट: सुनिश्चित करें कि आपके सिस्टम पर जावा डेवलपमेंट किट (JDK) स्थापित है।

2.  Aspose.HTML for Java लाइब्रेरी: Aspose.HTML for Java को डाउनलोड करें और इंस्टॉल करें[लिंक को डाउनलोड करें](https://releases.aspose.com/html/java/).

3. EPUB फ़ाइल: आपको एक EPUB फ़ाइल की आवश्यकता होगी जिसे आप XPS में परिवर्तित करना चाहते हैं।

अब जबकि हमने अपनी पूर्व-आवश्यकताएं निर्धारित कर ली हैं, तो आइए EPUB से XPS के लिए XPS सेव विकल्प निर्दिष्ट करने के लिए आवश्यक चरणों पर आगे बढ़ें।

## पैकेज आयात करें

सबसे पहले, आपको Java के लिए Aspose.HTML के साथ काम करने के लिए आवश्यक पैकेज आयात करने की आवश्यकता है। आप अपनी Java फ़ाइल की शुरुआत में निम्न कोड जोड़कर ऐसा कर सकते हैं:

```java
import java.io.FileInputStream;
import com.aspose.html.saving.XpsSaveOptions;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.drawing.Page;
import com.aspose.html.drawing.Size;
import com.aspose.html.drawing.Length;
import com.aspose.html.drawing.Color;
import com.aspose.html.converters.Converter;
import com.aspose.html.system.io.resources.Resources;
```

## EPUB फ़ाइल खोलें

पढ़ने के लिए किसी मौजूदा EPUB फ़ाइल को खोलकर शुरुआत करें। आप निम्न कोड स्निपेट का उपयोग कर सकते हैं:

```java
try (FileInputStream fileInputStream = new FileInputStream(Resources.input("input.epub"))) {
    //EPUB फ़ाइल प्रबंधन के लिए आपका कोड यहां है।
}
```

## XPS सेव विकल्प बनाएं

इसके बाद, कस्टम पेज आकार और पृष्ठभूमि रंग के साथ XpsSaveOptions का एक इंस्टेंस बनाएँ। यह PageSetup और विकल्पों को कॉन्फ़िगर करके किया जाता है। यहाँ बताया गया है कि आप इसे कैसे प्राप्त कर सकते हैं:

```java
XpsSaveOptions options = new XpsSaveOptions();
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
anyPage.setSize(new Size(Length.fromPixels(3000), Length.fromPixels(1000)));
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

## EPUB को XPS में बदलें

 अंत में, आपको कॉल करना होगा`convertEPUB` EPUB से XPS रूपांतरण करने की विधि। इसके लिए कोड यहाँ दिया गया है:

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.xps")
);
```

इन चरणों का पालन करके, अब आप आसानी से Aspose.HTML for Java का उपयोग करके EPUB से XPS रूपांतरण के लिए XPS सेव विकल्प निर्दिष्ट कर सकते हैं। इस ट्यूटोरियल ने आपको एक व्यापक गाइड प्रदान की है, और इन चरणों का पालन करके, आप EPUB फ़ाइलों के साथ सहजता से काम कर सकते हैं और उन्हें XPS प्रारूप में बदल सकते हैं।

## निष्कर्ष

इस ट्यूटोरियल में, हमने आपको Aspose.HTML for Java का उपयोग करके EPUB से XPS रूपांतरण के लिए XPS सेव विकल्पों को निर्दिष्ट करने की प्रक्रिया के बारे में बताया है। सही पूर्वापेक्षाओं और चरण-दर-चरण मार्गदर्शिका के साथ, आप अपने वेब डेवलपमेंट प्रोजेक्ट के लिए इस लाइब्रेरी की शक्ति का कुशलतापूर्वक उपयोग कर सकते हैं।

## पूछे जाने वाले प्रश्न

### 1. Java के लिए Aspose.HTML क्या है?
Aspose.HTML for Java HTML और EPUB फ़ाइलों के साथ काम करने के लिए एक शक्तिशाली लाइब्रेरी है, जो डेवलपर्स को विभिन्न प्रारूपों में रूपांतरण सहित विभिन्न कार्य करने की अनुमति देता है।

### 2. क्या मैं अपनी व्यावसायिक परियोजनाओं में Java के लिए Aspose.HTML का उपयोग कर सकता हूँ?
 हां, आप व्यावसायिक परियोजनाओं में जावा के लिए Aspose.HTML का उपयोग कर सकते हैं। लाइसेंसिंग विवरण के लिए, आप यहां जा सकते हैं[खरीद पृष्ठ](https://purchase.aspose.com/buy).

### 3. क्या Java के लिए Aspose.HTML का निःशुल्क परीक्षण उपलब्ध है?
 हां, आप निःशुल्क परीक्षण के साथ लाइब्रेरी का अन्वेषण कर सकते हैं। इसे यहां से डाउनलोड करें[यहाँ](https://releases.aspose.com/).

### 4. मैं Aspose.HTML for Java के बारे में सहायता कहां से प्राप्त कर सकता हूं या प्रश्न कहां पूछ सकता हूं?
 आप समर्थन और चर्चा के लिए Aspose फ़ोरम पर जा सकते हैं[https://forum.aspose.com/](https://forum.aspose.com/).

### 5. Java के लिए Aspose.HTML की सिस्टम आवश्यकताएँ क्या हैं?
Aspose.HTML for Java के लिए जावा डेवलपमेंट किट (JDK) और एक संगत ऑपरेटिंग सिस्टम की आवश्यकता होती है। सुनिश्चित करें कि आप इस ट्यूटोरियल में बताई गई पूर्व-आवश्यकताओं को पूरा करते हैं।
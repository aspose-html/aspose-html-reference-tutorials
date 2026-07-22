---
date: 2026-03-29
description: Aspose.HTML for Java का उपयोग करके XPS सहेजने के विकल्प निर्दिष्ट करना,
  EPUB को XPS में बदलना और लाइसेंसिंग को संभालना सीखें।
linktitle: Specifying XPS Save Options for EPUB to XPS
second_title: Java HTML Processing with Aspose.HTML
title: EPUB से XPS के लिए Aspose HTML सहेजने विकल्पों का उपयोग कैसे करें
url: /hi/java/converting-epub-to-xps/convert-epub-to-xps-specify-xps-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose HTML Save Options को EPUB से XPS में उपयोग करने का तरीका

इस गाइड में हम दिखाएंगे **कैसे Aspose** HTML Save Options का उपयोग करके EPUB दस्तावेज़ को XPS में बदलें, साथ ही पृष्ठ आयाम, पृष्ठभूमि रंग, और लाइसेंसिंग विचारों पर पूर्ण नियंत्रण रखें। चाहे आप बैच‑प्रोसेसिंग पाइपलाइन बना रहे हों या एक‑बार की रूपांतरण टूल, ये चरण तेज़ और भरोसेमंद परिणाम प्राप्त करने में मदद करेंगे।

## त्वरित उत्तर
- **Aspose HTML Save Options क्या करता है?** यह XPS जैसे फ़ॉर्मेट में सहेजते समय पृष्ठ आकार, पृष्ठभूमि रंग और अन्य रेंडरिंग सेटिंग्स को अनुकूलित करने की अनुमति देता है।  
- **कौनसी लाइब्रेरी आवश्यक है?** Aspose.HTML for Java (नवीनतम संस्करण)।  
- **क्या मुझे लाइसेंस चाहिए?** मूल्यांकन के लिए एक मुफ्त ट्रायल काम करता है; उत्पादन के लिए एक व्यावसायिक लाइसेंस आवश्यक है।  
- **क्या मैं पृष्ठ आयाम बदल सकता हूँ?** हाँ – आप `PageSetup` के माध्यम से कोई भी चौड़ाई और ऊँचाई सेट कर सकते हैं।  
- **क्या रूपांतरण तेज़ है?** सामान्य EPUB फ़ाइलों के लिए रूपांतरण आधुनिक JVM पर कुछ सेकंड में पूरा हो जाता है।

## इस संदर्भ में “how to use aspose” क्या है?
वाक्यांश **how to use Aspose** Aspose.HTML लाइब्रेरी का उपयोग करके वेब‑आधारित दस्तावेज़ों को हेरफेर और रूपांतरित करने के व्यावहारिक चरणों को दर्शाता है। इस ट्यूटोरियल में हम **aspose html save options** पर ध्यान केंद्रित करते हैं, जो आपको **EPUB को XPS में बदलते** समय आउटपुट को सूक्ष्म‑समायोजित करने की सुविधा देता है।

## EPUB को XPS में बदलने के लिए Java के लिए Aspose.HTML क्यों उपयोग करें?
- **उच्च सटीकता** – जटिल लेआउट, फ़ॉन्ट और वेक्टर ग्राफ़िक्स को संरक्षित करता है।  
- **प्रोग्रामेटिक नियंत्रण** – Java एप्लिकेशन के भीतर बैच रूपांतरण को स्वचालित करें।  
- **कोई बाहरी निर्भरताएँ नहीं** – शुद्ध Java लाइब्रेरी, कोई नेटिव कंपोनेंट नहीं।  
- **अनुकूलित आउटपुट** – सहेजने के विकल्पों की बदौलत आप XPS को अपनी विशिष्ट आवश्यकताओं के अनुसार तैयार कर सकते हैं, जैसे **पृष्ठ आयाम निर्दिष्ट करना** या कस्टम पृष्ठभूमि सेट करना।  

## पूर्वापेक्षाएँ

कोड में जाने से पहले सुनिश्चित करें कि आपके पास निम्नलिखित हों:

1. **Java विकास पर्यावरण** – JDK 8 या उससे ऊपर स्थापित हो।  
2. **Aspose.HTML for Java लाइब्रेरी** – इसे [download link](https://releases.aspose.com/html/java/) से डाउनलोड करें।  
3. **EPUB फ़ाइल** – वह स्रोत EPUB जिसे आप **EPUB को XPS में बदलना** चाहते हैं।  

इन सबको तैयार रखने से आप बिना रुकावट के चरणों का पालन कर पाएँगे।

## पैकेज आयात करें

सबसे पहले, आवश्यक क्लासेस को आयात करें। इन इम्पोर्ट्स को अपने Java स्रोत फ़ाइल के शीर्ष पर रखें:

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

इन इम्पोर्ट्स से आपको रूपांतरण इंजन और **Aspose HTML Save Options** तक पहुँच मिलती है, जो सूक्ष्म‑समायोजन के लिए आवश्यक हैं।

## EPUB फ़ाइल खोलें

अब वह EPUB खोलें जिसे आप बदलना चाहते हैं। `Resources.input` हेल्पर डेमो रिसोर्स फ़ोल्डर से फ़ाइल लोड करता है:

```java
try (FileInputStream fileInputStream = new FileInputStream(Resources.input("input.epub"))) {
    // Your code for the EPUB file handling goes here.
}
```

एक try‑with‑resources ब्लॉक का उपयोग करने से स्ट्रीम स्वचालित रूप से बंद हो जाता है।

## XPS सहेजने के विकल्प बनाएं (पृष्ठ आकार और पृष्ठभूमि कॉन्फ़िगर करें)

अब हम `XpsSaveOptions` का एक इंस्टेंस बनाते हैं और उसे अनुकूलित करते हैं। यही वह जगह है जहाँ **save options** वास्तव में चमकते हैं:

```java
XpsSaveOptions options = new XpsSaveOptions();
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
anyPage.setSize(new Size(Length.fromPixels(3000), Length.fromPixels(1000)));
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

- **पृष्ठ आकार** – इस उदाहरण में 3000 × 1000 पिक्सेल सेट किया गया है; इसे अपने लक्ष्य कागज़ के आकार के अनुसार समायोजित करें या `Length.fromInches` का उपयोग करके इंच में **पृष्ठ आयाम निर्दिष्ट** करें।  
- **पृष्ठभूमि रंग** – `AliceBlue` दिखाता है कि कैनवास पृष्ठभूमि कैसे बदली जा सकती है; आप कोई भी `Color` चुन सकते हैं।  

ये सेटिंग्स **aspose html save options** का हिस्सा हैं, जो अंतिम XPS दस्तावेज़ को प्रभावित करती हैं।

## EPUB को XPS में बदलें

अंत में, स्ट्रीम, कॉन्फ़िगर किए गए विकल्प और आउटपुट पथ के साथ कनवर्टर को कॉल करें:

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.xps")
);
```

जब यह लाइन चलती है, Aspose.HTML EPUB को पढ़ता है, आपके द्वारा परिभाषित पृष्ठ सेटअप और पृष्ठभूमि रंग लागू करता है, और एक पूर्णतः मानक XPS फ़ाइल लिखता है।

## सामान्य समस्याएँ और सुझाव

- **गलत पृष्ठ आयाम** – सुनिश्चित करें कि आयाम पिक्सेल में व्यक्त किए गए हैं (या `Length.fromInches` का उपयोग करें)।  
- **फ़ॉन्ट नहीं मिल रहे** – आवश्यक फ़ॉन्ट को EPUB में एम्बेड करें या JVM होस्ट पर इंस्टॉल करें ताकि फ़ॉलबैक न हो।  
- **बड़ी फ़ाइलें** – बहुत बड़े EPUB के लिए JVM हीप (`-Xmx`) बढ़ाएँ ताकि `OutOfMemoryError` से बचा जा सके।  
- **Aspose HTML लाइसेंसिंग** – रूपांतरण से पहले एक वैध लाइसेंस लोड करें; अन्यथा ट्रायल वॉटरमार्क दिखाई देगा।

## निष्कर्ष

**Aspose HTML Save Options** का उपयोग करके आप EPUB को XPS में रेंडर करने पर सटीक नियंत्रण प्राप्त करते हैं। ऊपर दिए गए चरण दिखाते हैं कि **EPUB को कैसे बदलें**, **पृष्ठ आयाम सेट करें**, पृष्ठभूमि बदलें, और केवल कुछ Java पंक्तियों से रूपांतरण करें। इस पैटर्न को अपने बैच प्रोसेसिंग पाइपलाइन में एकीकृत करके प्रकाशन कार्यों को कुशलतापूर्वक स्वचालित करें।

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: Aspose.HTML for Java क्या है?**  
उत्तर: यह एक Java लाइब्रेरी है जो डेवलपर्स को ब्राउज़र की आवश्यकता के बिना HTML, EPUB और अन्य वेब‑आधारित दस्तावेज़ों को बनाना, संपादित करना, रेंडर करना और रूपांतरित करना सक्षम करती है।

**प्रश्न: क्या मैं इसे व्यावसायिक प्रोजेक्ट में उपयोग कर सकता हूँ?**  
उत्तर: हाँ। उत्पादन उपयोग के लिए आपको एक वैध लाइसेंस चाहिए। आप इसे [purchase page](https://purchase.aspose.com/buy) पर खरीद सकते हैं।

**प्रश्न: क्या कोई मुफ्त ट्रायल उपलब्ध है?**  
उत्तर: बिल्कुल। आप [here](https://releases.aspose.com/) से ट्रायल संस्करण डाउनलोड कर सकते हैं।

**प्रश्न: मुझे समर्थन कहाँ मिल सकता है?**  
उत्तर: Aspose फ़ोरम पर समुदाय समर्थन और आधिकारिक सहायता उपलब्ध है: [https://forum.aspose.com/](https://forum.aspose.com/)।

**प्रश्न: सिस्टम आवश्यकताएँ क्या हैं?**  
उत्तर: Java Development Kit (JDK) 8+ और Aspose रनटाइम द्वारा समर्थित ऑपरेटिंग सिस्टम। सुनिश्चित करें कि आपका पर्यावरण पहले बताए गए पूर्वापेक्षाओं को पूरा करता है।

---

**Last Updated:** 2026-03-29  
**Tested With:** Aspose.HTML for Java 24.12  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
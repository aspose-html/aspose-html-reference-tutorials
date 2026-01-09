---
date: 2026-01-09
description: Aspose.HTML for Java का उपयोग करके XPS सहेजने के विकल्प निर्दिष्ट करना
  और EPUB को XPS में कुशलतापूर्वक परिवर्तित करना सीखें।
linktitle: Specifying XPS Save Options for EPUB to XPS
second_title: Java HTML Processing with Aspose.HTML
title: EPUB से XPS रूपांतरण के लिए Aspose HTML सहेजने विकल्प निर्दिष्ट करना
url: /hi/java/converting-epub-to-xps/convert-epub-to-xps-specify-xps-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# EPUB को XPS में परिवर्तित करने के लिए Aspose HTML Save Options निर्दिष्ट करना

EPUB दस्तावेज़ को XPS में बदलना प्रकाशन वर्कफ़्लो का एक उपयोगी हिस्सा हो सकता है, और **Aspose HTML Save Options** आपको आउटपुट पर सूक्ष्म नियंत्रण प्रदान करते हैं। इस ट्यूटोरियल में हम Aspose.HTML for Java के साथ इन सेव विकल्पों को कॉन्फ़िगर करने के सटीक चरणों को देखेंगे और एक उच्च‑गुणवत्ता वाला XPS फ़ाइल बनाएँगे।

## Quick Answers
- **Aspose HTML Save Options क्या करता है?** यह XPS जैसे फ़ॉर्मेट में सहेजते समय पेज साइज, बैकग्राउंड कलर और अन्य रेंडरिंग सेटिंग्स को कस्टमाइज़ करने की सुविधा देता है।  
- **कौन सी लाइब्रेरी आवश्यक है?** Aspose.HTML for Java (नवीनतम संस्करण)।  
- **क्या लाइसेंस चाहिए?** मूल्यांकन के लिए फ्री ट्रायल काम करता है; प्रोडक्शन के लिए व्यावसायिक लाइसेंस आवश्यक है।  
- **क्या मैं पेज डाइमेंशन बदल सकता हूँ?** हाँ – आप `PageSetup` के माध्यम से कोई भी चौड़ाई और ऊँचाई सेट कर सकते हैं।  
- **क्या रूपांतरण तेज़ है?** सामान्य EPUB फ़ाइलों के लिए रूपांतरण आधुनिक JVM पर कुछ सेकंड में पूरा हो जाता है।

## What Are Aspose HTML Save Options?
Aspose HTML Save Options प्रॉपर्टीज़ का एक सेट है जो यह नियंत्रित करता है कि HTML, EPUB या अन्य वेब‑आधारित दस्तावेज़ कैसे रेंडर और लक्ष्य फ़ॉर्मेट (जैसे XPS, PDF, या इमेज फ़ाइलें) में सहेजे जाएँ। ये पेज लेआउट, बैकग्राउंड कलर, मार्जिन आदि को परिभाषित करने की अनुमति देते हैं, जिससे उत्पन्न फ़ाइल आपके डिज़ाइन आवश्यकताओं से मेल खाती है।

## Why Use Aspose.HTML for Java to Convert EPUB to XPS?
- **उच्च फ़िडेलिटी** – जटिल लेआउट, फ़ॉन्ट और वेक्टर ग्राफ़िक्स को संरक्षित करता है।  
- **प्रोग्रामेटिक कंट्रोल** – जावा एप्लिकेशन के भीतर बैच रूपांतरण को स्वचालित करें।  
- **कोई बाहरी निर्भरताएँ नहीं** – शुद्ध जावा लाइब्रेरी, कोई नेटिव कंपोनेंट नहीं।  
- **कस्टमाइज़ेबल आउटपुट** – सेव विकल्पों की मदद से आप XPS को अपनी सटीक जरूरतों के अनुसार तैयार कर सकते हैं।

## Prerequisites

कोड में जाने से पहले सुनिश्चित करें कि आपके पास निम्नलिखित उपलब्ध हैं:

1. **जावा डेवलपमेंट एनवायरनमेंट** – JDK 8 या उससे ऊपर स्थापित हो।  
2. **Aspose.HTML for Java लाइब्रेरी** – इसे [download link](https://releases.aspose.com/html/java/) से डाउनलोड करें।  
3. **EPUB फ़ाइल** – वह स्रोत EPUB जिसे आप कनवर्ट करना चाहते हैं।  

इन सबको तैयार रखने से आप बिना रुकावट के चरणों का पालन कर पाएँगे।

## Import Packages

सबसे पहले आवश्यक क्लासेज़ को इम्पोर्ट करें। ये इम्पोर्ट्स आपके जावा स्रोत फ़ाइल के शीर्ष पर रखें:

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

इन इम्पोर्ट्स से आपको कन्वर्ज़न इंजन और **Aspose HTML Save Options** तक पहुँच मिलती है, जो फाइन‑ट्यूनिंग के लिए आवश्यक हैं।

## Open the EPUB File

अब वह EPUB खोलें जिसे आप कनवर्ट करना चाहते हैं। `Resources.input` हेल्पर डेमो रिसोर्स फ़ोल्डर से फ़ाइल लोड करता है:

```java
try (FileInputStream fileInputStream = new FileInputStream(Resources.input("input.epub"))) {
    // Your code for the EPUB file handling goes here.
}
```

`try‑with‑resources` ब्लॉक का उपयोग करने से स्ट्रीम स्वतः बंद हो जाती है।

## Create XPS Save Options (Configure Page Size & Background)

अब हम `XpsSaveOptions` का एक इंस्टेंस बनाते हैं और उसे कस्टमाइज़ करते हैं। यहाँ ही **save options** की असली शक्ति दिखती है:

```java
XpsSaveOptions options = new XpsSaveOptions();
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
anyPage.setSize(new Size(Length.fromPixels(3000), Length.fromPixels(1000)));
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

- **पेज साइज** – इस उदाहरण में 3000 × 1000 पिक्सेल सेट किया गया है; इसे अपने लक्ष्य पेपर साइज के अनुसार समायोजित करें।  
- **बैकग्राउंड कलर** – `AliceBlue` दिखाता है कि कैसे कैनवास बैकग्राउंड बदल सकते हैं; आप कोई भी `Color` चुन सकते हैं।  

ये सेटिंग्स **Aspose HTML Save Options** का हिस्सा हैं जो अंतिम XPS दस्तावेज़ को प्रभावित करती हैं।

## Convert EPUB to XPS

अंत में, कन्वर्टर को स्ट्रीम, कॉन्फ़िगर किए गए विकल्प और आउटपुट पाथ के साथ कॉल करें:

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.xps")
);
```

जब यह लाइन चलती है, Aspose.HTML EPUB को पढ़ता है, आपने जो पेज सेटअप और बैकग्राउंड कलर निर्धारित किया है उसे लागू करता है, और एक पूर्णतः मानक XPS फ़ाइल लिखता है।

## Common Issues & Tips

- **गलत पेज डाइमेंशन** – सुनिश्चित करें कि डाइमेंशन पिक्सेल में व्यक्त किए गए हैं (या `Length.fromInches` का उपयोग करें)।  
- **फ़ॉन्ट नहीं मिल रहा** – आवश्यक फ़ॉन्ट को EPUB में एम्बेड करें या JVM होस्ट पर इंस्टॉल करें ताकि फ़ॉलबैक न हो।  
- **बड़ी फ़ाइलें** – बहुत बड़े EPUB के लिए JVM हीप (`-Xmx`) बढ़ाएँ ताकि `OutOfMemoryError` से बचा जा सके।  

## Conclusion

**Aspose HTML Save Options** का उपयोग करके आप EPUB को XPS में रेंडर करने पर सटीक नियंत्रण प्राप्त करते हैं। ऊपर दिए गए चरण दिखाते हैं कि पेज साइज, बैकग्राउंड कलर कैसे सेट करें और केवल कुछ जावा लाइनों से रूपांतरण कैसे करें। इस पैटर्न को अपने बैच प्रोसेसिंग पाइपलाइन में एकीकृत करके प्रकाशन कार्यों को कुशलता से ऑटोमेट करें।

## Frequently Asked Questions

**Q: Aspose.HTML for Java क्या है?**  
A: यह एक जावा लाइब्रेरी है जो डेवलपर्स को ब्राउज़र की आवश्यकता के बिना HTML, EPUB और अन्य वेब‑आधारित दस्तावेज़ बनाने, संपादित करने, रेंडर करने और कनवर्ट करने की सुविधा देती है।

**Q: क्या मैं इसे व्यावसायिक प्रोजेक्ट में उपयोग कर सकता हूँ?**  
A: हाँ। प्रोडक्शन उपयोग के लिए आपको वैध लाइसेंस चाहिए। आप इसे [purchase page](https://purchase.aspose.com/buy) से खरीद सकते हैं।

**Q: क्या फ्री ट्रायल उपलब्ध है?**  
A: बिल्कुल। ट्रायल संस्करण को [here](https://releases.aspose.com/) से डाउनलोड करें।

**Q: सपोर्ट कहाँ मिल सकता है?**  
A: कम्युनिटी सपोर्ट और आधिकारिक सहायता Aspose फ़ोरम पर उपलब्ध है: [https://forum.aspose.com/](https://forum.aspose.com/)।

**Q: सिस्टम आवश्यकताएँ क्या हैं?**  
A: Java Development Kit (JDK) 8+ और वह ऑपरेटिंग सिस्टम जो Aspose रनटाइम द्वारा समर्थित हो। सुनिश्चित करें कि आपका वातावरण पहले उल्लेखित प्रीक्विज़िट्स को पूरा करता है।

---

**Last Updated:** 2026-01-09  
**Tested With:** Aspose.HTML for Java 24.12  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
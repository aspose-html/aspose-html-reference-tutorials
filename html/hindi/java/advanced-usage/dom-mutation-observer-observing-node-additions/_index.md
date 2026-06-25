---
date: 2026-03-18
description: Aspose.HTML के Mutation Observer का उपयोग करके जावा में बॉडी में तत्व
  जोड़ना और DOM परिवर्तनों की निगरानी करना सीखें। इसमें जावा में HTML दस्तावेज़ बनाने
  और Mutation Observer को डिस्कनेक्ट करने के चरण शामिल हैं।
linktitle: Append Element to Body - Observing Node Additions
second_title: Java HTML Processing with Aspose.HTML
title: Aspose.HTML for Java का उपयोग करके DOM म्यूटेशन ऑब्ज़र्वर के साथ बॉडी में तत्व
  जोड़ें
url: /hi/java/advanced-usage/dom-mutation-observer-observing-node-additions/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML for Java के साथ DOM Mutation Observer का उपयोग करके बॉडी में एलिमेंट जोड़ें

यदि आप एक Java डेवलपर हैं जिन्हें DOM में होने वाले प्रत्येक परिवर्तन पर नज़र रखते हुए **append element to body** करने की आवश्यकता है, तो आप सही जगह पर आए हैं। Aspose.HTML for Java **create HTML document Java** ऑब्जेक्ट बनाना, एक Mutation Observer संलग्न करना, और नोड्स के जोड़ने, हटाने या बदलने पर तुरंत प्रतिक्रिया देना आसान बनाता है। इस चरण‑दर‑चरण ट्यूटोरियल में हम पूरी प्रक्रिया को समझेंगे—डॉक्यूमेंट सेटअप से लेकर **disconnect mutation observer** तक—ताकि आप अपने Java एप्लिकेशन में DOM परिवर्तन को आत्मविश्वास से मॉनिटर कर सकें।

## त्वरित उत्तर
- **What does a Mutation Observer do?** यह DOM ट्री को देखता है और आपको नोड जोड़ने, हटाने या एट्रिब्यूट परिवर्तन की सूचना देता है।  
- **Which library provides this in Java?** Aspose.HTML for Java में पूर्ण‑विशेषताओं वाला Mutation Observer API शामिल है।  
- **Do I need a license for production?** हाँ, व्यावसायिक उपयोग के लिए एक वैध Aspose.HTML लाइसेंस आवश्यक है।  
- **Can I observe changes to text nodes?** बिल्कुल—ऑब्ज़र्वर कॉन्फ़िगरेशन में `characterData` को `true` सेट करें।  
- **How do I stop the observer?** मॉनिटरिंग समाप्त होने पर `observer.disconnect()` कॉल करें।

## Aspose.HTML के संदर्भ में “append element to body” क्या है?
`<body>` टैग में एक एलिमेंट जोड़ना मतलब प्रोग्रामेटिक रूप से एक नया नोड (जैसे `<p>` या `<div>`) दस्तावेज़ के मुख्य कंटेंट एरिया में जोड़ना। जब इसे Mutation Observer के साथ मिलाया जाता है, तो आप उस जोड़ को तुरंत पहचान सकते हैं और कस्टम लॉजिक ट्रिगर कर सकते हैं—डायनामिक HTML जेनरेशन, टेस्टिंग, या सर्वर‑साइड रेंडरिंग परिदृश्यों के लिए आदर्श।

## Java में Mutation Observer क्यों उपयोग करें?
- **Real‑time monitoring:** जैसे ही DOM में बदलाव होते हैं, तुरंत प्रतिक्रिया दें।  
- **Cleaner code:** मैन्युअल पोलिंग या जटिल इवेंट हैंडलिंग की आवश्यकता नहीं।  
- **Cross‑platform consistency:** चाहे आप ब्राउज़र में या सर्वर पर HTML रेंडर करें, यह समान रूप से काम करता है।  
- **Performance:** ऑब्ज़र्वर कुशल होते हैं और असिंक्रोनस रूप से चलते हैं, जिससे आपका मुख्य थ्रेड मुक्त रहता है।

## पूर्वापेक्षाएँ
1. **Java Development Kit (JDK)** – 8 या उससे ऊपर।  
2. **Aspose.HTML for Java** – आधिकारिक साइट से नवीनतम संस्करण डाउनलोड करें।  
3. **IDE** – IntelliJ IDEA, Eclipse, या कोई भी Java‑संगत एडिटर।  

आप Aspose.HTML for Java डाउनलोड पेज से प्राप्त कर सकते हैं [here](https://releases.aspose.com/html/java/)।

## पैकेज इम्पोर्ट करें
पहले, उन क्लासेज़ को इम्पोर्ट करें जिनकी आपको आवश्यकता होगी। यह एक खाली HTML डॉक्यूमेंट भी बनाता है जिसे हम बाद में भरेंगे।

```java
// Import necessary packages
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.mutations.MutationObserver;
import com.aspose.html.dom.mutations.MutationCallback;
import com.aspose.html.dom.mutations.MutationRecord;
import com.aspose.html.dom.mutations.MutationObserverInit;
import com.aspose.html.dom.Element;
import com.aspose.html.dom.Text;
import com.aspose.html.generic.IGenericList;

// Create an empty HTML document
HTMLDocument document = new HTMLDocument();
```

## चरण 1: Mutation Observer इंस्टेंस बनाएं (mutation observer java)
एक **Mutation Observer** को एक कॉलबैक चाहिए जो प्रत्येक म्यूटेशन पर बुलाया जाएगा। हमारे कॉलबैक में हम प्रत्येक जोड़े गए नोड के लिए एक संदेश प्रिंट करते हैं।

```java
MutationObserver observer = new MutationObserver(new MutationCallback() {
    @Override
    public void invoke(IGenericList<MutationRecord> mutations, MutationObserver mutationObserver) {
        mutations.forEach(mutationRecord -> {
            mutationRecord.getAddedNodes().forEach(node -> {
                synchronized (this) {
                    System.out.println("The '" + node + "' node was added to the document.");
                    notifyAll();
                }
            });
        });
    }
});
```

## चरण 2: ऑब्ज़र्वर कॉन्फ़िगर करें (monitor dom changes java)
हम ऑब्ज़र्वर को बताते हैं कि **क्या** देखना है—चाइल्ड लिस्ट परिवर्तन, सबट्री मॉडिफिकेशन, और कैरेक्टर डेटा अपडेट।

```java
MutationObserverInit config = new MutationObserverInit();
config.setChildList(true);
config.setSubtree(true);
config.setCharacterData(true);

// Pass in the target node to observe with the specified configuration
observer.observe(document.getBody(), config);
```

## चरण 3: बॉडी में एलिमेंट जोड़ें और ऑब्ज़र्वर ट्रिगर करें
अब हम वास्तव में **append element to body** करते हैं। एक `<p>` एलिमेंट को टेक्स्ट नोड के साथ जोड़ने से वह ऑब्ज़र्वर ट्रिगर होगा जिसे हमने पहले सेट किया था।

```java
// Create a paragraph element and append it to the document body
Element p = document.createElement("p");
document.getBody().appendChild(p);

// Create a text and append it to the paragraph
Text text = document.createTextNode("Hello World");
p.appendChild(text);
```

## चरण 4: ऑब्ज़र्वेशन के लिए प्रतीक्षा करें (asynchronous handling)
म्यूटेशन असिंक्रोनस रूप से रिपोर्ट होते हैं, इसलिए हम थोड़ी देर रुकते हैं ताकि ऑब्ज़र्वर को परिवर्तन प्रोसेस करने का समय मिल सके।

```java
// Since mutations are working in async mode, wait for a few seconds
synchronized (this) {
    wait(5000);
}
```

## चरण 5: ऑब्ज़र्वर डिस्कनेक्ट करें (disconnect mutation observer)
जब आप मॉनिटरिंग समाप्त कर लें, तो हमेशा **disconnect mutation observer** करके संसाधनों को मुक्त करें।

```java
// Stop observing
observer.disconnect();
```

## बॉडी में पैराग्राफ कैसे जोड़ें
कई वास्तविक परिदृश्यों में आप एक पैराग्राफ डालना चाहेंगे जिसमें डायनामिक कंटेंट हो, जैसे उपयोगकर्ता‑जनित टेक्स्ट या सर्वर‑साइड संदेश। `<p>` एलिमेंट बनाकर, उसे `<body>` में जोड़कर, और फिर एक टेक्स्ट नोड जोड़कर आप यही हासिल कर सकते हैं। यह तरीका Mutation Observer के साथ सहजता से काम करता है, इसलिए जोड़ तुरंत लॉग हो जाता है।

## Java में DOM परिवर्तन कैसे मॉनिटर करें
हमने जो ऑब्ज़र्वर कॉन्फ़िगरेशन उपयोग किया (`childList`, `subtree`, `characterData`) अधिकांश सामान्य परिवर्तन प्रकारों को कवर करता है। यदि आपको एट्रिब्यूट मॉडिफिकेशन भी ट्रैक करने की जरूरत है, तो बस `config.setAttributes(true)` सक्षम करें। ऑब्ज़र्वर बैकग्राउंड थ्रेड पर चलता है, इसलिए आपका मुख्य एप्लिकेशन फ्लो बिना बाधा के रहता है जबकि आप विस्तृत म्यूटेशन रिकॉर्ड प्राप्त करते हैं।

## सामान्य समस्याएँ और सुझाव
- **Never forget to disconnect** – ऑब्ज़र्वर को चलाते रहने से मेमोरी लीक्स हो सकते हैं।  
- **Thread safety:** कॉलबैक बैकग्राउंड थ्रेड पर चलता है; यदि आप साझा डेटा को संशोधित करते हैं तो उचित सिंक्रोनाइज़ेशन उपयोग करें।  
- **Observe the right node:** `document.getBody()` को ऑब्ज़र्व करने से अधिकांश UI परिवर्तन पकड़ते हैं, लेकिन आप अधिक सूक्ष्म मॉनिटरिंग के लिए किसी भी एलिमेंट को टारगेट कर सकते हैं।  
- **Pro tip:** यदि आपको एट्रिब्यूट परिवर्तन भी देखना है तो `config.setAttributes(true)` उपयोग करें।

## अक्सर पूछे जाने वाले प्रश्न

**Q: What is a DOM Mutation Observer?**  
A: यह एक API है जो DOM ट्री को नोड जोड़ने, हटाने या एट्रिब्यूट अपडेट जैसे परिवर्तनों के लिए देखता है, और इन इवेंट्स को कॉलबैक के माध्यम से प्रदान करता है।

**Q: Can I use Aspose.HTML for Java in commercial projects?**  
A: हाँ, एक वैध Aspose.HTML लाइसेंस के साथ। खरीद विवरण [here](https://purchase.aspose.com/buy) पर उपलब्ध हैं।

**Q: Is there a free trial for Aspose.HTML for Java?**  
A: बिल्कुल—ट्रायल डाउनलोड करने के लिए [release page](https://releases.aspose.com/) देखें।

**Q: How do I monitor character data changes?**  
A: ऑब्ज़र्वर कॉन्फ़िगरेशन में `config.setCharacterData(true)` सेट करें, जैसा कि चरण 2 में दिखाया गया है।

**Q: What should I do after finishing the observation?**  
A: `observer.disconnect()` (चरण 5) कॉल करें और यदि आपने `HTMLDocument` बनाया है तो `document.dispose()` से उसे डिस्पोज़ करें ताकि नेटिव रिसोर्सेज़ मुक्त हो सकें।

## निष्कर्ष
आपने अब सीख लिया है कि कैसे **append element to body**, **mutation observer java** सेटअप करें, और Aspose.HTML for Java का उपयोग करके **monitor DOM changes java** करें। इन चरणों का पालन करके आप अपने सर्वर‑साइड Java एप्लिकेशन में किसी भी DOM म्यूटेशन को विश्वसनीय रूप से पहचान और प्रतिक्रिया दे सकते हैं। विभिन्न नोड प्रकारों, एट्रिब्यूट ऑब्ज़र्वेशन, या यहाँ तक कि कई ऑब्ज़र्वर के साथ प्रयोग करने में संकोच न करें ताकि अधिक जटिल परिदृश्यों को संभाला जा सके।

यदि आपको कोई समस्या आती है, तो समुदाय [Aspose.HTML forum](https://forum.aspose.com/) में मदद के लिए तैयार है। अधिक विस्तृत API विवरण के लिए आधिकारिक [Aspose.HTML for Java documentation](https://reference.aspose.com/html/java/) देखें।

---

**अंतिम अपडेट:** 2026-03-18  
**परीक्षित संस्करण:** Aspose.HTML for Java 24.11  
**लेखक:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-02-22
description: Aspose.HTML सैंडबॉक्स के साथ जावा में डिवाइस पिक्सेल रेशियो सेट करें।
  कस्टम यूज़र एजेंट सेट करना, जावा में पेज टाइटल प्राप्त करना, और एक ट्यूटोरियल में
  HTML को PNG में बदलना सीखें।
draft: false
keywords:
- set device pixel ratio
- set custom user agent
- save html as image
- convert html to png
- get page title java
language: hi
og_description: Aspose.HTML सैंडबॉक्स का उपयोग करके जावा में डिवाइस पिक्सेल रेशियो
  सेट करें। यह ट्यूटोरियल दिखाता है कि कैसे कस्टम यूज़र एजेंट सेट करें, जावा में पेज
  शीर्षक प्राप्त करें, और HTML को PNG में बदलें।
og_title: जावा में डिवाइस पिक्सेल अनुपात सेट करें – पूर्ण गाइड
tags:
- Aspose.HTML
- Java
- Web Rendering
title: जावा में डिवाइस पिक्सेल अनुपात सेट करें – पूर्ण मार्गदर्शिका
url: /hi/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा में डिवाइस पिक्सेल रेशियो सेट करें – पूर्ण गाइड

क्या आपने कभी सोचा है कि जावा से वेब पेज रेंडर करते समय **set device pixel ratio** कैसे सेट किया जाए? आप अकेले नहीं हैं। कई डेवलपर्स को हाई‑DPI मोबाइल स्क्रीन का अनुकरण करना पड़ता है ताकि स्क्रीनशॉट साफ़ दिखें, विशेषकर जब वे बाद में रिपोर्ट या मार्केटिंग एसेट्स के लिए **save html as image** करते हैं। इस ट्यूटोरियल में हम एक व्यावहारिक उदाहरण के माध्यम से इसे दिखाएंगे—और साथ ही आपको **set custom user agent**, **get page title java**, और Aspose.HTML का उपयोग करके **convert html to png** कैसे करना है, भी बताएँगे।

हम सैंडबॉक्स API का संक्षिप्त परिचय देंगे, फिर प्रत्येक कॉन्फ़िगरेशन चरण में गहराई से जाएंगे, और अंत में एक PNG फ़ाइल बनाएँगे जो वास्तविक iPhone डिस्प्ले को प्रतिबिंबित करे। अंत तक, आपके पास एक पुन: उपयोग योग्य स्निपेट होगा जिसे आप किसी भी जावा प्रोजेक्ट में डाल सकते हैं। कोई बाहरी टूल आवश्यक नहीं, केवल साधारण जावा और Aspose.HTML 7.x (या नया)।

---

## आवश्यकताएँ

- Java 17 या बाद का (कोड पहले के संस्करणों में भी कम्पाइल हो सकता है लेकिन 17 की सलाह दी जाती है)।
- Aspose.HTML for Java लाइब्रेरी (आधिकारिक Aspose साइट से डाउनलोड करें; Maven कोऑर्डिनेट्स: `com.aspose:aspose-html:23.10`)।
- आपका पसंदीदा IDE या टेक्स्ट एडिटर (IntelliJ IDEA, VS Code, Eclipse… सभी काम करेंगे)।
- डेमो URL (`https://example.com/responsive.html`) के लिए इंटरनेट एक्सेस, या इसे किसी सार्वजनिक HTML पेज से बदलें जो आपका हो।

> **Pro tip:** यदि आप प्रॉक्सी के पीछे हैं, तो कोड चलाने से पहले JVM की `http.proxyHost` और `http.proxyPort` सिस्टम प्रॉपर्टीज़ को कॉन्फ़िगर करें।

---

## चरण 1: डिवाइस पिक्सेल रेशियो और अन्य सैंडबॉक्स विकल्प सेट करें

पहले हमें एक **SandboxOptions** इंस्टेंस चाहिए जहाँ हम वर्चुअल स्क्रीन साइज और *डिवाइस पिक्सेल रेशियो* (DPR) को परिभाषित करते हैं। DPR वह फ़ैक्टर है जो ब्राउज़र को बताता है कि एक CSS पिक्सेल के लिए कितने फिजिकल पिक्सेल होते हैं। Retina iPhone पर DPR आमतौर पर **2.0** होता है, इसलिए हम वही मान उपयोग करेंगे।

```java
// Step 1: Create and configure SandboxOptions
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS width of an iPhone X
sandboxOptions.setScreenHeight(667);         // CSS height
sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
```

> **Why this matters:** सही DPR सेट न करने पर रेंडर की गई इमेज धुंधली या बहुत बड़ी दिखेगी क्योंकि रास्टराइज़र 1:1 पिक्सेल मैपिंग मान लेता है।

---

## चरण 2: कस्टम यूज़र एजेंट सेट करें

वेबसाइट्स अक्सर **User‑Agent** हेडर के आधार पर अलग‑अलग मार्कअप सर्व करती हैं। यह सुनिश्चित करने के लिए कि हमारा पेज वास्तविक iPhone की तरह व्यवहार करे, हम एक कस्टम स्ट्रिंग इंजेक्ट करते हैं जो iOS पर Safari की नकल करती है।

```java
// Step 2: Define a mobile‑specific user agent
String iphoneUA = "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                  "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                  "Version/14.0 Mobile/15E148 Safari/604.1";

sandboxOptions.setUserAgent(iphoneUA);   // <-- set custom user agent
```

> **Edge case:** कुछ साइटें `Accept-Language` हेडर भी जांचती हैं। यदि आपको अनुवाद गायब दिखें, तो `sandboxOptions.setAcceptLanguage("en-US,en;q=0.9");` जोड़ें।

---

## चरण 3: सैंडबॉक्स के अंदर पेज लोड करें और शीर्षक प्राप्त करें

अब हम उन विकल्पों के साथ सैंडबॉक्स को स्पिन अप करते हैं जो हमने अभी परिभाषित किए हैं। **Sandbox** ऑब्जेक्ट रेंडरिंग प्रक्रिया को अलग करता है, जिससे हमारा DPR और यूज़र‑एजेंट सेटिंग्स मान्य होते हैं।

```java
// Step 3: Create the sandbox and load the HTML document
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
HTMLDocument htmlDoc = new HTMLDocument(
        "https://example.com/responsive.html", mobileSandbox);
```

पेज लोड होने के बाद, शीर्षक प्राप्त करना इतना सरल है जितना `getTitle()` को कॉल करना। यह **get page title java** आवश्यकता को पूरा करता है।

```java
// Step 3b: Print the page title to the console
System.out.println("Title: " + htmlDoc.getTitle());   // <-- get page title java
```

**अपेक्षित कंसोल आउटपुट**

```
Title: Responsive Demo – Mobile View
```

यदि शीर्षक खाली है, तो URL को दोबारा जांचें या सुनिश्चित करें कि पेज CORS नीतियों द्वारा ब्लॉक नहीं है।

---

## चरण 4: HTML को PNG में बदलें और HTML को इमेज के रूप में सहेजें

Aspose.HTML आपको DOM को सीधे इमेज फ़ाइल में रेंडर करने देता है। क्योंकि हमने पहले ही DPR को 2.0 सेट किया है, परिणामी PNG में दो गुना पिक्सेल डेंसिटी होगी, जिससे एक स्पष्ट स्क्रीनशॉट मिलेगा।

```java
// Step 4: Render and save as PNG (convert html to png)
htmlDoc.save("mobile_view.png");   // <-- save html as image
```

`save` मेथड स्वचालित रूप से फ़ाइल एक्सटेंशन का पता लगाता है और उपयुक्त रेंडरर चुनता है। यदि आपको अलग फ़ॉर्मेट चाहिए (JPEG, BMP), तो बस फ़ाइल नाम बदल दें।

> **What if you need a specific image size?**  
> `ImageSaveOptions` का उपयोग करके चौड़ाई, ऊँचाई और बैकग्राउंड कलर नियंत्रित करें:

```java
ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
pngOptions.setWidth(750);   // 375 CSS px * DPR 2
pngOptions.setHeight(1334);
htmlDoc.save("mobile_view_custom.png", pngOptions);
```

---

## पूर्ण कार्यशील उदाहरण

नीचे वह पूरा, तैयार‑चलाने‑योग्य प्रोग्राम है जो सभी चरणों को जोड़ता है। इसे `SandboxDemo.java` फ़ाइल में कॉपी‑पेस्ट करें, Aspose.HTML डिपेंडेंसी जोड़ें, और `java SandboxDemo` चलाएँ।

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.rendering.image.ImageSaveOptions;
import com.aspose.html.rendering.image.SaveFormat;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Configure sandbox – set device pixel ratio, screen size, and user agent
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS width (iPhone)
        sandboxOptions.setScreenHeight(667);         // CSS height
        sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
        sandboxOptions.setUserAgent(
                "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                "Version/14.0 Mobile/15E148 Safari/604.1");   // <-- set custom user agent

        // 2️⃣ Create sandbox instance
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // 3️⃣ Load the target page inside the sandboxed environment
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com/responsive.html", mobileSandbox);

        // 4️⃣ Retrieve and print the page title (get page title java)
        System.out.println("Title: " + htmlDoc.getTitle());

        // 5️⃣ Render the page – convert html to png and save html as image
        // Simple save (auto‑detect PNG)
        htmlDoc.save("mobile_view.png");   // <-- save html as image

        // 6️⃣ Optional: custom size rendering
        ImageSaveOptions opts = new ImageSaveOptions(SaveFormat.PNG);
        opts.setWidth(750);   // 375 * DPR 2
        opts.setHeight(1334);
        htmlDoc.save("mobile_view_custom.png", opts); // another convert html to png example
    }
}
```

प्रोग्राम चलाने पर दो PNG फ़ाइलें बनती हैं:

| फ़ाइल | विवरण |
|------|-------------|
| `mobile_view.png` | कॉन्फ़िगर किए गए DPR का उपयोग करके डिफ़ॉल्ट रेंडरिंग। |
| `mobile_view_custom.png` | स्पष्ट चौड़ाई/ऊँचाई के साथ रेंडरिंग (स्थिर‑साइज़ एसेट्स के लिए उपयोगी)। |

आप किसी भी इमेज व्यूअर में इन फ़ाइलों को खोलकर हाई‑रेज़ोल्यूशन आउटपुट की पुष्टि कर सकते हैं।

---

## सामान्य प्रश्न और किनारे के मामले

| प्रश्न | उत्तर |
|----------|--------|
| **यदि पेज में जावास्क्रिप्ट है जो लोड होने के बाद DOM को संशोधित करता है तो क्या होगा?** | Aspose.HTML डिफ़ॉल्ट रूप से स्क्रिप्ट्स को एक्सीक्यूट करता है। यदि आपको स्क्रिप्ट एक्सीक्यूशन से पहले स्थिर स्नैपशॉट चाहिए, तो `sandboxOptions.setEnableJavaScript(false)` सेट करें। |
| **क्या मैं ऐसे पेज को रेंडर कर सकता हूँ जिसे ऑथेंटिकेशन की आवश्यकता है?** | हाँ। `sandboxOptions.setCredentials(new NetworkCredential("user","pass"))` का उपयोग करें या `sandboxOptions.getCookies().add(...)` के माध्यम से कुकीज़ इंजेक्ट करें। |
| **क्या DPR 2.0 तक सीमित है?** | नहीं। आप कोई भी पॉज़िटिव डबल सेट कर सकते हैं (उदाहरण: अल्ट्रा‑हाई‑DPI डिवाइस के लिए 3.0)। बस याद रखें कि बड़ा DPR बड़े इमेज फ़ाइलों का कारण बनता है। |
| **बड़ी एसेट्स (इमेज, फ़ॉन्ट) वाली पेजेज को कैसे हैंडल करें?** | `sandboxOptions.setMemoryLimit(512 * 1024 * 1024)` (बाइट्स) के साथ सैंडबॉक्स की मेमोरी लिमिट बढ़ाएँ। इससे भारी पेजेज पर आउट‑ऑफ़‑मेमोरी त्रुटियों से बचा जा सकता है। |
| **क्या मुझे सैंडबॉक्स को मैन्युअली बंद करना चाहिए?** | `Sandbox` `AutoCloseable` को इम्प्लीमेंट करता है। स्वचालित क्लीन‑अप के लिए इसे try‑with‑resources ब्लॉक में रैप करें। |

---

## निष्कर्ष

हमने दिखाया कि कैसे **set device pixel ratio** को जावा सैंडबॉक्स में सेट किया जाए, **set custom user agent**, **get page title java**, और **convert html to png** (प्रभावी रूप से **save html as image**) को Aspose.HTML का उपयोग करके किया जाए। पूरा उदाहरण एक व्यावहारिक वर्कफ़्लो दर्शाता है जिसे आप स्वचालित स्क्रीनशॉट जनरेशन, विज़ुअल रेग्रेसन टेस्टिंग, या किसी भी स्थिति में जहाँ वेब पेज का पिक्सेल‑परफेक्ट प्रतिनिधित्व आवश्यक हो, के लिए अनुकूलित कर सकते हैं।

बिना हिचकिचाहट प्रयोग करें—DPR को 3.0 करें, यूज़र‑एजेंट को Android स्ट्रिंग से बदलें, या URL को स्थानीय HTML फ़ाइल की ओर इंगित करें। वही पैटर्न PDFs, SVGs, या मल्टी‑पेज रेंडरिंग के लिए भी काम करता है।

यदि आपको यह गाइड उपयोगी लगा, तो **PDF generation with Aspose.HTML**, **headless Chrome alternatives**, या **batch rendering of multiple URLs** जैसे संबंधित विषयों को एक्सप्लोर करें। हैप्पी कोडिंग, और आपके स्क्रीनशॉट हमेशा तेज़‑धार हों!

![जावा सैंडबॉक्स में डिवाइस पिक्सेल रेशियो सेट करें](image.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
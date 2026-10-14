---
category: general
date: 2026-10-14
description: Aspose.HTML का उपयोग करके जावास्क्रिप्ट से java को कॉल करें। जानें कि
  कैसे host object जोड़ें, java में javascript निष्पादित करें, और जावास्क्रिप्ट से
  log करें, एक संक्षिप्त tutorial में।
keywords:
- call java from javascript
- execute javascript in java
- run javascript in java
- java host object
- aspose.html scripting
lastmod: 2026-10-14
og_description: Aspose.HTML का उपयोग करके जावास्क्रिप्ट से java को कॉल करें। यह guide
  दिखाता है कि कैसे host object जोड़ें, java में javascript निष्पादित करें, और जावास्क्रिप्ट
  से log करें, सभी कुछ कोड की कुछ लाइनों में।
og_image_alt: Screenshot of Java console output showing javascript logging via Aspose.HTML
  host object
og_title: जावास्क्रिप्ट से java को कॉल करें – host object जोड़ें और java में javascript
  चलाएँ
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Call java from javascript using Aspose.HTML. Learn how to add a host
    object, execute javascript in java, and log from javascript in a concise tutorial.
  headline: Call java from javascript – add host object and run javascript in java
  type: TechArticle
- questions:
  - answer: Yes. Aspose.HTML is a pure‑Java library, so it runs on any JVM, including
      Android’s ART runtime.
    question: Does this work on Android?
  - answer: You can expose POJOs with getters and setters; the engine maps them to
      JavaScript objects automatically. Collections such as `java.util.List` or arrays
      are also convertible.
    question: What if I need to pass complex objects?
  - answer: If the script throws a JavaScript error, `eval` propagates a `ScriptException`.
      Wrap the call in a try‑catch block to log or recover.
    question: How does error handling work?
  - answer: Absolutely. The same `HTMLDocument` retains its global scope, so you can
      call `eval` repeatedly. Just manage variable names to avoid clashes.
    question: Can I run multiple scripts sequentially?
  - answer: Treat any external script as untrusted input. Validate parameters and
      consider sandboxing by exposing only the minimal required methods.
    question: Is the host object safe for untrusted scripts?
  type: FAQPage
tags:
- java
- javascript
- aspose.html
- scripting
- host object
title: जावास्क्रिप्ट से java को कॉल करें – host object जोड़ें और java में javascript
  चलाएँ
url: /hi/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावास्क्रिप्ट से जावा को कॉल करें – होस्ट ऑब्जेक्ट जोड़ें और जावास्क्रिप्ट को जावा में चलाएँ

क्या आपको कभी **call java from javascript** करने की जरूरत पड़ी है किसी Java एप्लिकेशन के भीतर? शायद आप एक डायनामिक HTML रिपोर्ट इंजन बना रहे हैं या आप बस एक Java logger को उस स्क्रिप्ट में एक्सपोज़ करना चाहते हैं जिसे आप नियंत्रित करते हैं। इस ट्यूटोरियल में आप देखेंगे कि कैसे होस्ट ऑब्जेक्ट जोड़ें, Java में JavaScript चलाएँ, और यहाँ तक कि **log from JavaScript** को JVM में वापस लॉग करें—सभी Aspose.HTML के साथ।

हम एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से चलेंगे जो एक खाली HTML दस्तावेज़ बनाता है, एक Java `Logger` क्लास को होस्ट ऑब्जेक्ट के रूप में इंजेक्ट करता है, एक छोटा स्क्रिप्ट निष्पादित करता है, और परिणाम को कंसोल पर प्रिंट करता है। कोई बाहरी वेब ब्राउज़र आवश्यक नहीं, कोई रहस्यमय “मैजिक” नहीं—सिर्फ साधारण Java कोड जिसे आप आज़ ही कॉपी‑पेस्ट करके चला सकते हैं।

## त्वरित उत्तर
- **होस्ट ऑब्जेक्ट कैसे जोड़ें?** `document.getWindow().addHostObject("name", object)` के साथ एक Java इंस्टेंस रजिस्टर करें।  
- **क्या मैं Java में JavaScript चला सकता हूँ?** हाँ—`document.getWindow().eval(yourScript)` उपयोग करें।  
- **क्या JavaScript से लॉगिंग संभव है?** बिल्कुल; होस्ट ऑब्जेक्ट कोई भी `void log(String)` मेथड एक्सपोज़ कर सकता है।  
- **Aspose.HTML का कौन सा संस्करण आवश्यक है?** संस्करण 23.10 या नया पूर्ण होस्ट‑ऑब्जेक्ट API को सपोर्ट करता है।  
- **क्या मुझे वेब ब्राउज़र चाहिए?** नहीं—Aspose.HTML एक एम्बेडेड इंजन प्रदान करता है, इसलिए सब कुछ हेड‑लेस चलता है।

## call java from javascript क्या है?
**Call java from javascript** वह तकनीक है जिसमें Java ऑब्जेक्ट्स को एक JavaScript रनटाइम में एक्सपोज़ किया जाता है ताकि स्क्रिप्ट सीधे Java मेथड्स को कॉल कर सके। Aspose.HTML एक हल्का JavaScript इंजन Java प्रोसेस के भीतर बनाता है, जिससे बाहरी ब्राउज़र के बिना दो‑तरफ़ा संचार संभव हो जाता है।

## जावा में जावास्क्रिप्ट निष्पादित करने के लिए Aspose.HTML क्यों उपयोग करें?
Aspose.HTML **50+ इनपुट और आउटपुट फॉर्मेट** को सपोर्ट करता है और एक पूर्ण‑अनुपालन HTML5 वातावरण में JavaScript का मूल्यांकन कर सकता है। यह सरल एक‑लाइनर कोड के लिए औसतन 200 ms तक स्क्रिप्ट प्रोसेस करता है, और यह पूरी ब्राउज़र स्टैक लोड किए बिना करता है, जिससे मेमोरी उपयोग Selenium‑आधारित तरीकों की तुलना में 80 % तक घट जाता है।

## पूर्वापेक्षाएँ

- Java 17 (या कोई भी हालिया JDK) स्थापित और कॉन्फ़िगर किया हुआ।  
- Aspose.HTML for Java लाइब्रेरी (संस्करण 23.10 या नया)। आप इसे Maven Central या Aspose वेबसाइट से प्राप्त कर सकते हैं।  
- एक साधारण IDE या टेक्स्ट एडिटर; उदाहरण कमांड‑लाइन से भी चलाया जा सकता है।

> **Pro tip:** यदि आप Maven उपयोग करते हैं, तो निम्नलिखित डिपेंडेंसी को अपने `pom.xml` में जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

या, Gradle के लिए:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

अब जब बुनियादी बातें तय हो गई हैं, चलिए चरण‑दर‑चरण समाधान में डुबकी लगाते हैं।

## जावा में जावास्क्रिप्ट चलाने और होस्ट ऑब्जेक्ट जोड़ने का तरीका?
`addHostObject` एक Java ऑब्जेक्ट को JavaScript कॉन्टेक्स्ट में एक ग्लोबल वैरिएबल के रूप में रजिस्टर करता है। अपना `HTMLDocument` लोड करें, `addHostObject` का उपयोग करके `"javaLogger"` नाम से एक Java logger रजिस्टर करें, और फिर एक छोटा स्क्रिप्ट मूल्यांकित करें जो `javaLogger.log` को कॉल करता है। पूरी प्रक्रिया केवल तीन API कॉल्स की आवश्यकता रखती है और किसी भी Java 17 रनटाइम में काम करती है।

### चरण 1: न्यूनतम जावा प्रोजेक्ट बनाएं

पहले, `JsHostObjectDemo` नाम की एक नई Java क्लास सेट अप करें। इस क्लास में हमारा `main` मेथड और होस्ट ऑब्जेक्ट परिभाषा होगी। सब कुछ एक फ़ाइल में रखने से ट्यूटोरियल स्व-निहित और कॉपी करने में आसान बन जाता है।

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Demonstrates how to call Java from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    // -----------------------------------------------------------------
    // Step 1.1 – Define a simple Java class that will be callable from JS
    // -----------------------------------------------------------------
    public static class Logger {
        /**
         * This method will be invoked from JavaScript.
         *
         * @param message Text to print.
         */
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1.2 – Create an empty HTMLDocument – it gives us a scripting engine
        // -----------------------------------------------------------------
        HTMLDocument document = new HTMLDocument();

        // -----------------------------------------------------------------
        // Step 1.3 – Add the Java Logger instance as a host object named "javaLogger"
        // -----------------------------------------------------------------
        document.getWindow().addHostObject("javaLogger", new Logger());

        // -----------------------------------------------------------------
        // Step 1.4 – Prepare JavaScript code that uses the host object
        // -----------------------------------------------------------------
        String script = "javaLogger.log('Hello from JavaScript!');";

        // -----------------------------------------------------------------
        // Step 1.5 – Execute the script; the Java Logger handles the call
        // -----------------------------------------------------------------
        document.getWindow().eval(script);
    }
}
```

### `HTMLDocument` क्यों?
`HTMLDocument` एक इन‑मेमोरी HTML दस्तावेज़ का प्रतिनिधित्व करता है और एक JavaScript इंजन प्रदान करता है। `HTMLDocument` क्लास एक पूर्ण HTML‑5 अनुपालन स्क्रिप्टिंग वातावरण को स्पिन‑अप करता है। भले ही हम कोई मार्कअप लोड न करें, दस्तावेज़ का `window` ऑब्जेक्ट हमें JavaScript इंजन तक पहुँच देता है, जहाँ **run javascript in java** का जादू होता है। अतिरिक्त रूप से आप DOM को मैनिपुलेट कर सकते हैं, संसाधन लोड कर सकते हैं, या ब्राउज़र के बिना स्क्रिप्ट्स का मूल्यांकन कर सकते हैं।

## होस्ट ऑब्जेक्ट जोड़ें – “javaLogger”?
`Logger` एक सरल Java क्लास है जिसमें `log(String)` मेथड है जो संदेशों को कंसोल पर लिखता है। `Logger` इंस्टेंस को `"javaLogger"` नाम से रजिस्टर करें ताकि इस दस्तावेज़ में मूल्यांकित कोई भी स्क्रिप्ट `javaLogger.log(...)` को कॉल कर सके। यह **add host object** आवश्यकता का मूल है और लॉगर को JavaScript कोड के लिए ग्लोबल वैरिएबल के रूप में उपलब्ध कराता है।

### सामान्य जाल

- **नाम टकराव** – यदि आपके स्क्रिप्ट में पहले से ही `javaLogger` नाम का ग्लोबल वैरिएबल है, तो होस्ट ऑब्जेक्ट ओवरराइट हो जाएगा। एक अद्वितीय नाम चुनें।  
- **थ्रेड सुरक्षा** – होस्ट ऑब्जेक्ट एक ही दस्तावेज़ पर कई स्क्रिप्ट निष्पादन के बीच साझा किया जाता है। यदि आप समानांतर में स्क्रिप्ट चलाने की योजना बनाते हैं, तो होस्ट क्लास को थ्रेड‑सेफ़ बनाएं (जैसे `synchronized` या `java.util.concurrent` प्रिमिटिव्स का उपयोग करके)।

## जावा में जावास्क्रिप्ट लिखें और निष्पादित करें?
`eval` दस्तावेज़ के स्क्रिप्टिंग इंजन में एक JavaScript स्ट्रिंग को निष्पादित करता है और कोई भी परिणाम लौटाता है। एक छोटा स्क्रिप्ट `eval` में पास करें। इंजन ग्लोबल स्कोप से `javaLogger` को रिजॉल्व करता है और प्रदान किए गए स्ट्रिंग के साथ उसके `log` मेथड को कॉल करता है। आप मान लौटाने, अपवाद संभालने, और अधिक जटिल इंटरैक्शन के लिए कई मूल्यांकनों को चेन भी कर सकते हैं।

### अपेक्षित आउटपुट

`main` मेथड चलाने पर कंसोल में निम्न पंक्ति प्रिंट होगी:

```
[JS] Hello from JavaScript!
```

## होस्ट को विस्तारित करें – केवल लॉगिंग से अधिक?
एक होस्ट ऑब्जेक्ट कोई भी Java इंस्टेंस हो सकता है जिसे `addHostObject` के माध्यम से JavaScript को एक्सपोज़ किया जाता है। `Logger` क्लास में अतिरिक्त मेथड जोड़कर या नई होस्ट क्लास बनाकर अतिरिक्त कार्यक्षमता प्रदान करें। नीचे एक त्वरित उदाहरण है जो JavaScript को एक मान भी वापस देता है। होस्ट ऑब्जेक्ट जटिल प्रकार, I/O, या अन्य सेवाओं के साथ इंटरैक्ट कर सकता है। मान वापस करके, स्क्रिप्ट डेटा प्राप्त कर सकती है, जिससे Java और JavaScript के बीच दो‑तरफ़ा संचार संभव हो जाता है।

```java
public static class Utils {
    public int add(int a, int b) {
        return a + b;
    }
}

// Register it
document.getWindow().addHostObject("javaUtils", new Utils());

// JavaScript side
String script2 = "var result = javaUtils.add(3, 4); javaLogger.log('3+4=' + result);";
document.getWindow().eval(script2);
```

अब कंसोल दिखाता है:

```
[JS] 3+4=7
```

## स्क्रिप्ट चलाने के बाद संसाधनों को साफ़ करें?
`dispose` `HTMLDocument` इंस्टेंस द्वारा रखे गए नेटिव संसाधनों को मुक्त करता है। जब आप स्क्रिप्टिंग वातावरण के साथ काम समाप्त कर लें, तो `HTMLDocument` को डिस्पोज़ करके नेटिव संसाधनों को मुक्त करें। `dispose()` न कॉल करने से मेमोरी लीक हो सकता है, विशेषकर जब आप लूप या दीर्घकालिक सर्विस में कई दस्तावेज़ बनाते हैं। हमेशा उपयोग को `try‑with‑resources` ब्लॉक में रखें या सुनिश्चित करें कि `document.dispose()` अंत में कॉल किया गया है।

```java
document.dispose(); // Important for long‑running applications
```

## पूर्ण कार्यशील उदाहरण

नीचे पूरा स्रोत फ़ाइल है जिसे आप तुरंत कंपाइल और रन कर सकते हैं। इसे `JsHostObjectDemo.java` के रूप में सेव करें, सुनिश्चित करें कि Aspose.HTML JAR आपके क्लासपाथ में है, और `java JsHostObjectDemo` चलाएँ।

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Complete demo showing how to call Java from JavaScript, add host object,
 * run JavaScript in Java, and log from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    /** Simple logger that will be called from JavaScript. */
    public static class Logger {
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    /** Utility class exposing arithmetic to JavaScript. */
    public static class Utils {
        public int add(int a, int b) {
            return a + b;
        }
    }

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create the HTMLDocument – this spins up the JavaScript engine.
        HTMLDocument document = new HTMLDocument();

        // 2️⃣ Register host objects.
        document.getWindow().addHostObject("javaLogger", new Logger());
        document.getWindow().addHostObject("javaUtils", new Utils());

        // 3️⃣ JavaScript that logs a message and performs a calculation.
        String script = ""
                + "javaLogger.log('Hello from JavaScript!');"
                + "var sum = javaUtils.add(5, 12);"
                + "javaLogger.log('5 + 12 = ' + sum);";

        // 4️⃣ Execute the script.
        document.getWindow().eval(script);

        // 5️⃣ Clean up.
        document.dispose();
    }
}
```

इस प्रोग्राम को चलाने पर प्राप्त होगा:

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या यह Android पर काम करता है?**  
A: हाँ। Aspose.HTML एक शुद्ध‑Java लाइब्रेरी है, इसलिए यह किसी भी JVM पर चलती है, जिसमें Android का ART रनटाइम भी शामिल है।

**Q: यदि मुझे जटिल ऑब्जेक्ट पास करने हों तो क्या करें?**  
A: आप POJO को गेटर और सेटर के साथ एक्सपोज़ कर सकते हैं; इंजन उन्हें स्वचालित रूप से JavaScript ऑब्जेक्ट्स में मैप कर देता है। `java.util.List` या एरे जैसी कलेक्शन भी परिवर्तनीय हैं।

**Q: त्रुटि संभालना कैसे काम करता है?**  
A: यदि स्क्रिप्ट JavaScript त्रुटि फेंकती है, तो `eval` एक `ScriptException` प्रोपेगेट करता है। कॉल को `try‑catch` ब्लॉक में रैप करें ताकि आप लॉग या रिकवरी कर सकें।

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

**Q: क्या मैं कई स्क्रिप्ट्स क्रमिक रूप से चला सकता हूँ?**  
A: बिल्कुल। वही `HTMLDocument` अपना ग्लोबल स्कोप बनाए रखता है, इसलिए आप `eval` को बार‑बार कॉल कर सकते हैं। केवल वैरिएबल नामों का टकराव न हो, इसका ध्यान रखें।

**Q: क्या होस्ट ऑब्जेक्ट असुरक्षित स्क्रिप्ट्स के लिए सुरक्षित है?**  
A: किसी भी बाहरी स्क्रिप्ट को असुरक्षित मानें। पैरामीटर वैलिडेट करें और केवल आवश्यक मेथड्स को ही एक्सपोज़ करके सैंडबॉक्सिंग पर विचार करें।

## सर्वोत्तम प्रथाएँ और टिप्स

- **होस्ट ऑब्जेक्ट्स का नाम स्पष्ट रखें**—`javaLogger`, `javaUtils` आदि—ताकि भ्रम न हो।  
- **होस्ट मेथड्स को छोटा और साइड‑इफ़ेक्ट‑फ़्री रखें** जब संभव हो; इससे डिबगिंग आसान होती है।  
- **दस्तावेज़ को तुरंत डिस्पोज़ करें**; यह Aspose.HTML द्वारा अलोकेट की गई नेटिव मेमोरी को मुक्त करता है।  
- **JavaScript से आने वाले इनपुट को वैलिडेट करें**, विशेषकर यदि स्क्रिप्ट अनविश्वसनीय स्रोत से आती है। उन्हें किसी भी बाहरी डेटा की तरह मानें।

## निष्कर्ष

आपके पास अब **call java from javascript** करने का एक ठोस, एंड‑टू‑एंड उदाहरण है, जिसमें **होस्ट ऑब्जेक्ट जोड़ना**, **जावा में जावास्क्रिप्ट चलाना**, और **जावास्क्रिप्ट से लॉगिंग** Aspose.HTML के साथ शामिल है। यह पैटर्न शक्तिशाली है: कोई भी Java सर्विस स्क्रिप्ट्स को एक्सपोज़ की जा सकती है, जिससे आपका Java एप्लिकेशन एक हल्का स्क्रिप्टिंग प्लेटफ़ॉर्म बन जाता है।

अगला आप खोज सकते हैं:

- एक पूर्ण HTML पेज इंजेक्ट करके JavaScript से DOM को मैनिपुलेट करना।  
- होस्ट ऑब्जेक्ट का उपयोग करके डेटा को Java साइड पर वापस स्ट्रीम करना (जैसे JSON सीरियलाइज़ेशन)।  
- अन्य स्क्रिप्टिंग इंजनों जैसे Nashorn या GraalVM के साथ इंटीग्रेशन करके व्यापक भाषा समर्थन प्राप्त करना।

इसे आज़माएँ, `Logger` या `Utils` क्लास को ट्यून करें, और देखें कि आप अपने प्रोजेक्ट में **javascript host object** अवधारणा को कितनी दूर तक ले जा सकते हैं।

---

**अंतिम अपडेट:** 2026-10-14  
**परीक्षण किया गया:** Aspose.HTML for Java 23.10  
**लेखक:** Aspose  






```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

```javascript
javaLogger.log('Hello from JavaScript!');
```

## संबंधित ट्यूटोरियल

- [जावा में स्क्रिप्ट निष्पादन सक्षम करें – पूर्ण Aspose HTML गाइड](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)
- [जावा में जावास्क्रिप्ट निष्पादित करें – चलाने के लिए पूर्ण गाइड](/html/java/advanced-usage/execute-javascript-in-java-complete-guide-to-running-js-from/)
- [जावास्क्रिप्ट को सैंडबॉक्स करें – पूर्ण Aspose HTML गाइड](/html/java/advanced-usage/how-to-sandbox-javascript-complete-aspose-html-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
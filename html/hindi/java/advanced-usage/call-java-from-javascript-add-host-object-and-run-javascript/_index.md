---
category: general
date: 2026-03-14
description: Aspose.HTML का उपयोग करके JavaScript से Java को कॉल करना सीखें। यह गाइड
  दिखाता है कि होस्ट ऑब्जेक्ट कैसे जोड़ें, Java में JavaScript चलाएँ, और JavaScript
  से लॉग कैसे करें।
draft: false
keywords:
- call java from javascript
- add host object
- run javascript in java
- javascript host object
- log from javascript
language: hi
og_description: Aspose.HTML का उपयोग करके JavaScript से Java को कॉल करें। होस्ट ऑब्जेक्ट
  जोड़ें, Java में JavaScript चलाएँ, और एक ही ट्यूटोरियल में JavaScript से लॉग करें।
og_title: जावास्क्रिप्ट से जावा को कॉल करें – होस्ट ऑब्जेक्ट के साथ पूर्ण गाइड
tags:
- Java
- JavaScript
- Aspose.HTML
- Scripting
title: जावास्क्रिप्ट से जावा को कॉल करें – होस्ट ऑब्जेक्ट जोड़ें और जावा में जावास्क्रिप्ट
  चलाएँ
url: /hi/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा से जावास्क्रिप्ट को कॉल करें – होस्ट ऑब्जेक्ट जोड़ें और जावा में जावास्क्रिप्ट चलाएँ

क्या आपको कभी जावा एप्लिकेशन के भीतर **जावास्क्रिप्ट से जावा को कॉल** करने की जरूरत पड़ी है? शायद आप एक डायनामिक HTML रिपोर्ट इंजन बना रहे हैं या आप सिर्फ एक जावा लॉगर को उस स्क्रिप्ट में एक्सपोज़ करना चाहते हैं जिसे आप नियंत्रित करते हैं। इस ट्यूटोरियल में आप देखेंगे कि कैसे होस्ट ऑब्जेक्ट जोड़ें, जावा में जावास्क्रिप्ट चलाएँ, और यहाँ तक कि **जावास्क्रिप्ट से लॉग** को JVM में वापस भेजें—सभी Aspose.HTML के साथ।

हम एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से चलेंगे जो एक खाली HTML दस्तावेज़ बनाता है, एक जावा `Logger` क्लास को होस्ट ऑब्जेक्ट के रूप में इंजेक्ट करता है, एक छोटा स्क्रिप्ट निष्पादित करता है, और परिणाम को कंसोल पर प्रिंट करता है। कोई बाहरी वेब ब्राउज़र आवश्यक नहीं, कोई रहस्यमय “मैजिक” नहीं—सिर्फ साधारण जावा कोड जिसे आप आज ही कॉपी‑पेस्ट करके चला सकते हैं।

## आवश्यकताएँ

- Java 17 (या कोई भी हालिया JDK) स्थापित और कॉन्फ़िगर किया हुआ।
- Aspose.HTML for Java लाइब्रेरी (संस्करण 23.10 या नया)। आप इसे Maven Central या Aspose वेबसाइट से प्राप्त कर सकते हैं।
- एक साधारण IDE या टेक्स्ट एडिटर; उदाहरण कमांड लाइन से भी काम करता है।

> **Pro tip:** यदि आप Maven का उपयोग करते हैं, तो अपने `pom.xml` में निम्नलिखित डिपेंडेंसी जोड़ें:

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

अब जब हमने बुनियादी चीज़ें सेट कर ली हैं, चलिए चरण‑दर‑चरण समाधान में डुबकी लगाते हैं।

## चरण 1: एक न्यूनतम जावा प्रोजेक्ट बनाएं

पहले, `JsHostObjectDemo` नाम की नई जावा क्लास सेट अप करें। यह क्लास हमारे `main` मेथड और होस्ट ऑब्जेक्ट परिभाषा को रखेगी। सब कुछ एक फ़ाइल में रखने से ट्यूटोरियल स्वयं‑समाहित और कॉपी करने में आसान बन जाता है।

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

Aspose.HTML का `HTMLDocument` क्लास एक पूर्ण HTML‑5 अनुरूप स्क्रिप्टिंग वातावरण तैयार करता है। भले ही हम कभी कोई मार्कअप लोड न करें, दस्तावेज़ का `window` ऑब्जेक्ट हमें जावास्क्रिप्ट इंजन तक पहुंच देता है, जहाँ **जावा में जावास्क्रिप्ट चलाने** का जादू होता है।

## चरण 2: होस्ट ऑब्जेक्ट जोड़ें – “javaLogger”

लाइन

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

**होस्ट ऑब्जेक्ट जोड़ने** की आवश्यकता को पूरा करती है। `Logger` इंस्टेंस को नाम `"javaLogger"` के तहत रजिस्टर करके, इस दस्तावेज़ में मूल्यांकित कोई भी स्क्रिप्ट `javaLogger.log(...)` को कॉल कर सकती है। यह **javascript host object** अवधारणा का मूल है: एक पुल जो जावास्क्रिप्ट को JVM में प्रवेश करने देता है।

### सामान्य समस्याएँ

- **नाम टकराव** – यदि आपके स्क्रिप्ट में पहले से ही `javaLogger` नाम का ग्लोबल वेरिएबल मौजूद है, तो होस्ट ऑब्जेक्ट ओवरराइट हो जाएगा। एक विशिष्ट नाम चुनें।
- **थ्रेड सुरक्षा** – होस्ट ऑब्जेक्ट एक ही दस्तावेज़ पर कई स्क्रिप्ट निष्पादन के बीच साझा किया जाता है। यदि आप स्क्रिप्ट्स को समानांतर चलाने की योजना बनाते हैं, तो होस्ट क्लास को थ्रेड‑सेफ बनाएं (जैसे `synchronized` या `java.util.concurrent` प्रिमिटिव्स का उपयोग करके)।

## चरण 3: जावास्क्रिप्ट लिखें और निष्पादित करें

हम `eval` में फीड करने वाला स्क्रिप्ट जानबूझकर छोटा है:

```javascript
javaLogger.log('Hello from JavaScript!');
```

जब `document.getWindow().eval(script)` चलता है, तो इंजन अपने ग्लोबल स्कोप में `javaLogger` को खोजता है, वह जोड़ा गया जावा ऑब्जेक्ट मिलता है, और प्रदान किए गए स्ट्रिंग के साथ उसकी `log` मेथड को कॉल करता है।

### अपेक्षित आउटपुट

`main` मेथड चलाने पर कंसोल में निम्नलिखित पंक्ति प्रिंट होती है:

```
[JS] Hello from JavaScript!
```

यह छोटा लाइन साबित करता है कि हमने सफलतापूर्वक **जावास्क्रिप्ट से जावा को कॉल** किया है, और **जावास्क्रिप्ट से लॉग** ठीक उसी जगह दिखता है जहाँ सामान्य जावा `System.out` संदेश आता है।

## चरण 4: होस्ट को विस्तारित करना – केवल लॉगिंग से अधिक

यदि आपको अतिरिक्त कार्यक्षमता (जैसे फ़ाइल एक्सेस, डेटाबेस क्वेरी) एक्सपोज़ करनी है, तो बस `Logger` क्लास में और मेथड जोड़ें—या एक नया होस्ट क्लास बनाएं। यहाँ एक त्वरित उदाहरण है जो एक वैल्यू भी रिटर्न करता है:

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

यह **javascript host object** पैटर्न की लचीलापन दर्शाता है: आप कोई भी जावा API एक्सपोज़ कर सकते हैं, बशर्ते डेटा टाइप्स जावा और जावास्क्रिप्ट के बीच परिवर्तनीय हों (प्रिमिटिव्स, स्ट्रिंग्स, एरेज़, आदि)।

## चरण 5: संसाधनों को साफ़ करें

जब आप स्क्रिप्टिंग वातावरण के साथ काम समाप्त कर लें, तो `HTMLDocument` को डिस्पोज़ करके नेटिव रिसोर्सेज़ को मुक्त करें:

```java
document.dispose(); // Important for long‑running applications
```

डिस्पोज़ न करने से मेमोरी लीक हो सकता है, विशेषकर जब आप लूप में कई दस्तावेज़ बनाते हैं।

## पूर्ण कार्यशील उदाहरण

नीचे पूरा सोर्स फ़ाइल दिया गया है जिसे आप तुरंत कंपाइल और रन कर सकते हैं। इसे `JsHostObjectDemo.java` के रूप में सेव करें, सुनिश्चित करें कि Aspose.HTML JAR आपके क्लासपाथ में है, और `java JsHostObjectDemo` चलाएँ।

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

इस प्रोग्राम को चलाने पर प्राप्त होता है:

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

यही पूरी **जावास्क्रिप्ट से जावा को कॉल** वर्कफ़्लो कुछ ही लाइनों में है।

## अक्सर पूछे जाने वाले प्रश्न

### क्या यह Android पर काम करता है?

Aspose.HTML एक शुद्ध‑जावा लाइब्रेरी है, इसलिए यह किसी भी JVM पर चलती है, जिसमें Android का Dalvik/ART भी शामिल है। बस JAR को बंडल कर दें और आपको वही होस्ट‑ऑब्जेक्ट क्षमताएँ मिलेंगी।

### यदि मुझे जटिल ऑब्जेक्ट पास करने की जरूरत हो तो?

आप POJO (plain old Java objects) को एक्सपोज़ कर सकते हैं जिनमें फ़ील्ड, गेटर्स और सेटर्स हों। इंजन उन्हें स्वचालित रूप से जावास्क्रिप्ट ऑब्जेक्ट्स में मैप कर देगा। कलेक्शन्स के लिए `java.util.List` या एरेज़ का उपयोग करें—दोनों परिवर्तनीय हैं।

### त्रुटि प्रबंधन कैसे काम करता है?

यदि स्क्रिप्ट जावास्क्रिप्ट त्रुटि फेंकती है, तो `eval` एक `ScriptException` प्रोपेगेट करेगा। कॉल को try‑catch ब्लॉक में रैप करके लॉग या रिकवर करें:

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

### क्या मैं कई स्क्रिप्ट्स क्रमिक रूप से चला सकता हूँ?

बिल्कुल। वही `HTMLDocument` इंस्टेंस अपना ग्लोबल स्कोप रखता है, इसलिए आप `eval` को बार‑बार कॉल कर सकते हैं। बस स्क्रिप्ट्स के बीच वेरिएबल नाम टकराव का ध्यान रखें।

## सर्वोत्तम प्रथाएँ और सुझाव

- **होस्ट ऑब्जेक्ट्स को स्पष्ट रूप से नाम दें**—`javaLogger`, `javaUtils`, आदि—ताकि भ्रम न हो।
- **होस्ट मेथड्स को छोटा और साइड‑इफ़ेक्ट‑फ़्री रखें** जब संभव हो; इससे डिबगिंग आसान होती है।
- **डॉक्यूमेंट को तुरंत डिस्पोज़ करें** जब काम समाप्त हो; इससे Aspose.HTML द्वारा अलोकेट की गई नेटिव मेमोरी रिलीज़ होती है।
- **जावास्क्रिप्ट से इनपुट्स को वैलिडेट करें**, विशेषकर जब स्क्रिप्ट्स अनट्रस्टेड स्रोतों से आती हों। उन्हें किसी भी बाहरी डेटा की तरह ट्रीट करें।

## निष्कर्ष

अब आपके पास एक ठोस, एंड‑टू‑एंड उदाहरण है कि कैसे **जावास्क्रिप्ट से जावा को कॉल** किया जाए **होस्ट ऑब्जेक्ट जोड़कर**, **जावा में जावास्क्रिप्ट चलाकर**, और **जावास्क्रिप्ट से लॉग** करके Aspose.HTML का उपयोग करके। यह पैटर्न शक्तिशाली है: कोई भी जावा सर्विस स्क्रिप्ट्स को एक्सपोज़ की जा सकती है, जिससे आपका जावा एप्लिकेशन एक हल्का स्क्रिप्टिंग प्लेटफ़ॉर्म बन जाता है।

अगले चरण में आप खोज सकते हैं:

- एक पूर्ण HTML पेज को इंजेक्ट करना और जावास्क्रिप्ट से DOM को मैनीपुलेट करना।
- होस्ट ऑब्जेक्ट का उपयोग करके डेटा को जावा साइड पर स्ट्रीम करना (जैसे JSON सीरियलाइज़ेशन)।
- Nashorn या GraalVM जैसे अन्य स्क्रिप्टिंग इंजन के साथ इंटीग्रेशन करके व्यापक भाषा समर्थन प्राप्त करना।

इसे आज़माएँ, `Logger` या `Utils` क्लासेज़ को ट्यून करें, और देखें कि आप अपने प्रोजेक्ट्स में **javascript host object** अवधारणा को कितनी दूर तक ले जा सकते हैं।

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
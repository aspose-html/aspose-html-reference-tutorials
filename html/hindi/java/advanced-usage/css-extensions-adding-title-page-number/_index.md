---
title: Aspose.HTML के साथ HTML पेज मार्जिन को अनुकूलित करें
linktitle: CSS एक्सटेंशन - शीर्षक और पृष्ठ संख्या जोड़ना
second_title: Aspose.HTML के साथ जावा HTML प्रसंस्करण
description: Java के लिए Aspose.HTML का उपयोग करके HTML दस्तावेज़ों में पृष्ठ मार्जिन को अनुकूलित करना, पृष्ठ संख्या और शीर्षक जोड़ना सीखें।
type: docs
weight: 10
url: /hi/java/advanced-usage/css-extensions-adding-title-page-number/
---
Aspose.HTML for Java, Java अनुप्रयोगों में HTML दस्तावेज़ों को संसाधित करने के लिए एक शक्तिशाली लाइब्रेरी है। इस ट्यूटोरियल में, हम यह पता लगाएंगे कि Aspose.HTML for Java का उपयोग करके कस्टम पेज मार्जिन कैसे बनाएं और अपने HTML दस्तावेज़ों में पेज नंबर और शीर्षक कैसे जोड़ें। यह चरण-दर-चरण मार्गदर्शिका प्रक्रिया को प्रबंधनीय चरणों में विभाजित करेगी ताकि आप इन सुविधाओं को अपने HTML दस्तावेज़ों में आसानी से एकीकृत कर सकें।

## आवश्यक शर्तें

शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ मौजूद हैं:

1. जावा विकास वातावरण: सुनिश्चित करें कि आपके कंप्यूटर पर जावा विकास वातावरण स्थापित है।

2.  Aspose.HTML for Java: Aspose.HTML for Java लाइब्रेरी को यहां से डाउनलोड और इंस्टॉल करें[यहाँ](https://releases.aspose.com/html/java/).

## पैकेज आयात करें

आरंभ करने के लिए, आपको Aspose.HTML for Java से आवश्यक पैकेज आयात करने होंगे। अपने Java कोड में निम्नलिखित आयात कथन जोड़ें:

```java
// Aspose.HTML पैकेज आयात करें
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

अब, आइए कस्टम पेज मार्जिन, पेज नंबर और शीर्षक जोड़ने की प्रक्रिया को प्रबंधनीय चरणों में विभाजित करें:

## चरण 1: कॉन्फ़िगरेशन और पेज मार्जिन आरंभ करें

```java
// कॉन्फ़िगरेशन ऑब्जेक्ट को आरंभ करें और दस्तावेज़ के लिए पृष्ठ-मार्जिन सेट करें
Configuration configuration = new Configuration();
try {
    // उपयोगकर्ता एजेंट सेवा प्राप्त करें
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // कस्टम मार्जिन की शैली सेट करें और उस पर निशान बनाएं
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

इस चरण में, हम कॉन्फ़िगरेशन ऑब्जेक्ट को आरंभीकृत करते हैं और पेज काउंटर और पेज शीर्षक की स्थिति सहित कस्टम पेज मार्जिन सेट करते हैं।

## चरण 2: HTML दस्तावेज़ आरंभ करें

```java
// HTML दस्तावेज़ आरंभ करें
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

यहां, हम एक नमूना सामग्री (इस मामले में, एक "हैलो वर्ल्ड" संदेश) के साथ एक HTML दस्तावेज़ बनाते हैं और चरण 1 से कॉन्फ़िगरेशन लागू करते हैं।

## चरण 3: आउटपुट डिवाइस को आरंभ करें और दस्तावेज़ को रेंडर करें

```java
// आउटपुट डिवाइस आरंभ करें
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    //दस्तावेज़ को आउटपुट डिवाइस पर भेजें
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

इस चरण में, हम आउटपुट डिवाइस सेट करते हैं और HTML दस्तावेज़ को रेंडर करते हैं। दस्तावेज़ को प्रोसेस किया जाएगा और निर्दिष्ट पेज मार्जिन, पेज नंबर और शीर्षक के साथ XPS फ़ाइल के रूप में सहेजा जाएगा।

## निष्कर्ष

बधाई हो! आपने सफलतापूर्वक सीख लिया है कि Aspose.HTML for Java का उपयोग करके कस्टम पेज मार्जिन कैसे बनाएं और अपने HTML दस्तावेज़ों में पेज नंबर और शीर्षक कैसे जोड़ें। यह अनुकूलन आपको अधिक पेशेवर और दिखने में आकर्षक दस्तावेज़ बनाने की अनुमति देता है।

 यदि आपके कोई प्रश्न हों या आपको कोई समस्या हो तो कृपया हमसे संपर्क करें[जावा के लिए Aspose.HTML दस्तावेज़](https://reference.aspose.com/html/java/) या सहायता मांगें[Aspose समर्थन मंच](https://forum.aspose.com/).

## अक्सर पूछे जाने वाले प्रश्न

### प्रश्न 1: Java के लिए Aspose.HTML क्या है?

A1: Aspose.HTML for Java एक Java लाइब्रेरी है जो Java अनुप्रयोगों में HTML दस्तावेज़ों के साथ काम करने के लिए शक्तिशाली उपकरण प्रदान करती है।

### प्रश्न 2: क्या मैं पृष्ठ मार्जिन को और अधिक अनुकूलित कर सकता हूँ?

उत्तर 2: हां, आप अपनी आवश्यकताओं के अनुसार पृष्ठ मार्जिन को अनुकूलित करने के लिए चरण 1 में CSS शैलियों को संशोधित कर सकते हैं।

### प्रश्न 3: मैं HTML दस्तावेज़ में अधिक सामग्री कैसे जोड़ सकता हूँ?

A3: आप नमूना सामग्री को अपनी सामग्री से प्रतिस्थापित करके चरण 2 में HTML सामग्री को संशोधित कर सकते हैं।

### प्रश्न 4: क्या Aspose.HTML for Java अन्य दस्तावेज़ प्रारूपों के साथ संगत है?

A4: हां, Java के लिए Aspose.HTML का उपयोग HTML दस्तावेज़ों को PDF, XPS और छवियों सहित विभिन्न प्रारूपों में परिवर्तित करने के लिए किया जा सकता है।

### प्रश्न 5: क्या मुझे Java के लिए Aspose.HTML का उपयोग करने के लिए लाइसेंस की आवश्यकता है?

 A5: हाँ, आप लाइसेंस या निःशुल्क परीक्षण प्राप्त कर सकते हैं[यहाँ](https://purchase.aspose.com/buy) या[यहाँ](https://releases.aspose.com/).
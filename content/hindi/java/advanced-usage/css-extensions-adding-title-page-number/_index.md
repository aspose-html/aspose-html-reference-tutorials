---
title: Aspose.HTML के साथ HTML पेज मार्जिन को कस्टमाइज़ करें
linktitle: सीएसएस एक्सटेंशन - शीर्षक और पृष्ठ संख्या जोड़ना
second_title: Aspose.HTML के साथ जावा HTML प्रोसेसिंग
description: जावा के लिए Aspose.HTML का उपयोग करके पेज मार्जिन को कस्टमाइज़ करना, HTML दस्तावेज़ों में पेज नंबर और शीर्षक जोड़ना सीखें।
type: docs
weight: 10
url: /hi/java/advanced-usage/css-extensions-adding-title-page-number/
---
जावा के लिए Aspose.HTML जावा अनुप्रयोगों में HTML दस्तावेज़ों को संसाधित करने के लिए एक शक्तिशाली लाइब्रेरी है। इस ट्यूटोरियल में, हम जावा के लिए Aspose.HTML का उपयोग करके कस्टम पेज मार्जिन कैसे बनाएं और अपने HTML दस्तावेज़ों में पेज नंबर और शीर्षक कैसे जोड़ें, इसका पता लगाएंगे। यह चरण-दर-चरण मार्गदर्शिका इन सुविधाओं को आपके HTML दस्तावेज़ों में आसानी से एकीकृत करने में मदद करने के लिए प्रक्रिया को प्रबंधनीय चरणों में विभाजित करेगी।

## आवश्यक शर्तें

शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित आवश्यक शर्तें हैं:

1. जावा विकास वातावरण: सुनिश्चित करें कि आपके कंप्यूटर पर जावा विकास वातावरण स्थापित है।

2.  जावा के लिए Aspose.HTML: जावा लाइब्रेरी के लिए Aspose.HTML को डाउनलोड और इंस्टॉल करें[यहाँ](https://releases.aspose.com/html/java/).

## पैकेज आयात करें

आरंभ करने के लिए, आपको जावा के लिए Aspose.HTML से आवश्यक पैकेज आयात करने होंगे। अपने जावा कोड में निम्नलिखित आयात विवरण जोड़ें:

```java
// Aspose.HTML पैकेज आयात करें
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

अब, आइए कस्टम पेज मार्जिन, पेज नंबर और शीर्षक जोड़ने की प्रक्रिया को प्रबंधनीय चरणों में विभाजित करें:

## चरण 1: कॉन्फ़िगरेशन और पेज मार्जिन प्रारंभ करें

```java
// कॉन्फ़िगरेशन ऑब्जेक्ट को प्रारंभ करें और दस्तावेज़ के लिए पेज-मार्जिन सेट करें
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

इस चरण में, हम कॉन्फ़िगरेशन ऑब्जेक्ट को आरंभ करते हैं और पेज काउंटर और पेज शीर्षक की स्थिति सहित कस्टम पेज मार्जिन सेट करते हैं।

## चरण 2: एक HTML दस्तावेज़ प्रारंभ करें

```java
// एक HTML दस्तावेज़ आरंभ करें
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

यहां, हम नमूना सामग्री के साथ एक HTML दस्तावेज़ बनाते हैं (इस मामले में, एक "हैलो वर्ल्ड" संदेश) और चरण 1 से कॉन्फ़िगरेशन लागू करते हैं।

## चरण 3: एक आउटपुट डिवाइस प्रारंभ करें और दस्तावेज़ प्रस्तुत करें

```java
// एक आउटपुट डिवाइस को इनिशियलाइज़ करें
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

इस चरण में, हम एक आउटपुट डिवाइस स्थापित करते हैं और HTML दस्तावेज़ प्रस्तुत करते हैं। दस्तावेज़ को निर्दिष्ट पृष्ठ मार्जिन, पृष्ठ संख्या और शीर्षक के साथ एक XPS फ़ाइल के रूप में संसाधित और सहेजा जाएगा।

## निष्कर्ष

बधाई हो! आपने जावा के लिए Aspose.HTML का उपयोग करके कस्टम पेज मार्जिन बनाना और अपने HTML दस्तावेज़ों में पेज नंबर और शीर्षक जोड़ना सफलतापूर्वक सीख लिया है। यह अनुकूलन आपको अधिक पेशेवर और देखने में आकर्षक दस्तावेज़ बनाने की अनुमति देता है।

 यदि आपके कोई प्रश्न हैं या किसी समस्या का सामना करना पड़ता है, तो बेझिझक यहाँ जाएँ[जावा दस्तावेज़ीकरण के लिए Aspose.HTML](https://reference.aspose.com/html/java/) या पर सहायता मांगें[Aspose समर्थन मंच](https://forum.aspose.com/).

## अक्सर पूछे जाने वाले प्रश्न

### Q1: जावा के लिए Aspose.HTML क्या है?

A1: जावा के लिए Aspose.HTML एक जावा लाइब्रेरी है जो जावा अनुप्रयोगों में HTML दस्तावेज़ों के साथ काम करने के लिए शक्तिशाली उपकरण प्रदान करती है।

### Q2: क्या मैं पेज मार्जिन को और अधिक अनुकूलित कर सकता हूँ?

उ2: हां, आप अपनी आवश्यकताओं के अनुसार पेज मार्जिन को अनुकूलित करने के लिए चरण 1 में सीएसएस शैलियों को संशोधित कर सकते हैं।

### Q3: मैं HTML दस्तावेज़ में और अधिक सामग्री कैसे जोड़ सकता हूँ?

उ3: आप नमूना सामग्री को अपनी सामग्री से प्रतिस्थापित करके चरण 2 में HTML सामग्री को संशोधित कर सकते हैं।

### Q4: क्या जावा के लिए Aspose.HTML अन्य दस्तावेज़ प्रारूपों के साथ संगत है?

उ4: हाँ, जावा के लिए Aspose.HTML का उपयोग HTML दस्तावेज़ों को पीडीएफ, एक्सपीएस और छवियों सहित विभिन्न प्रारूपों में परिवर्तित करने के लिए किया जा सकता है।

### Q5: क्या मुझे जावा के लिए Aspose.HTML का उपयोग करने के लिए लाइसेंस की आवश्यकता है?

 A5: हां, आप यहां से लाइसेंस या निःशुल्क परीक्षण प्राप्त कर सकते हैं[यहाँ](https://purchase.aspose.com/buy) या[यहाँ](https://releases.aspose.com/).
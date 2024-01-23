---
title: Aspose.HTML के साथ .NET में पर्यावरण कॉन्फ़िगरेशन
linktitle: .NET में पर्यावरण कॉन्फ़िगरेशन
second_title: Aspose.HTML .NET HTML हेरफेर एपीआई
description: स्क्रिप्ट प्रबंधन, कस्टम शैलियों, जावास्क्रिप्ट निष्पादन नियंत्रण, और अधिक जैसे कार्यों के लिए Aspose.HTML का उपयोग करके .NET में HTML दस्तावेज़ों के साथ काम करना सीखें। यह व्यापक ट्यूटोरियल आपको आरंभ करने के लिए चरण-दर-चरण उदाहरण और अक्सर पूछे जाने वाले प्रश्न प्रदान करता है।
type: docs
weight: 10
url: /hi/net/advanced-features/environment-configuration/
---

आज की डिजिटल दुनिया में, HTML दस्तावेज़ बनाना और उनमें हेरफेर करना कई डेवलपर्स के लिए एक मौलिक कार्य है। चाहे आप एक वेब एप्लिकेशन बना रहे हों या HTML को पीडीएफ या छवियों जैसे अन्य प्रारूपों में परिवर्तित करने की आवश्यकता हो, .NET के लिए Aspose.HTML आपके टूलकिट में एक शक्तिशाली उपकरण है। इस ट्यूटोरियल में, हम .NET के लिए Aspose.HTML के विभिन्न पहलुओं का पता लगाएंगे, जिसमें पूर्वापेक्षाएँ, नेमस्पेस आयात करना और विस्तृत स्पष्टीकरण के साथ चरण-दर-चरण उदाहरण शामिल हैं।

## आवश्यक शर्तें

इससे पहले कि हम .NET के लिए Aspose.HTML का उपयोग करें, आपको यह सुनिश्चित करना होगा कि आपके पास निम्नलिखित पूर्वापेक्षाएँ हैं:

1. विजुअल स्टूडियो: सुनिश्चित करें कि आपकी डेवलपमेंट मशीन पर विजुअल स्टूडियो स्थापित है। .NET के लिए Aspose.HTML को विज़ुअल स्टूडियो के साथ सहजता से काम करने के लिए डिज़ाइन किया गया है।

2.  .NET के लिए Aspose.HTML: आप वेबसाइट से .NET लाइब्रेरी के लिए Aspose.HTML डाउनलोड कर सकते हैं। डाउनलोड पृष्ठ तक पहुँचने के लिए निम्नलिखित लिंक का उपयोग करें:[.NET के लिए Aspose.HTML डाउनलोड करें](https://releases.aspose.com/html/net/).

3. इंस्टालेशन और लाइसेंस: लाइब्रेरी डाउनलोड करने के बाद, दस्तावेज़ में दिए गए इंस्टालेशन निर्देशों का पालन करें। कुछ उन्नत सुविधाओं का उपयोग करने के लिए आपको वैध लाइसेंस की भी आवश्यकता हो सकती है। आप Aspose वेबसाइट से लाइसेंस प्राप्त कर सकते हैं:[Aspose.HTML लाइसेंस खरीदें](https://purchase.aspose.com/buy).

4.  निःशुल्क परीक्षण: यदि आप लाइसेंस खरीदने से पहले Aspose.HTML को आज़माना चाहते हैं, तो आप इस लिंक से निःशुल्क परीक्षण संस्करण प्राप्त कर सकते हैं:[Aspose.HTML निःशुल्क परीक्षण](https://releases.aspose.com/).

अब जब आपके पास आवश्यक शर्तें हैं, तो आइए अगले अनुभाग पर आगे बढ़ें जहां हम आवश्यक नामस्थान आयात करेंगे।

## नामस्थान आयात करें

.NET के लिए Aspose.HTML के साथ प्रभावी ढंग से काम करने के लिए, आपको अपने प्रोजेक्ट में उपयुक्त नामस्थान आयात करने की आवश्यकता होगी। नीचे, हम उन नामस्थानों को सूचीबद्ध करेंगे जिनकी आपको उन उदाहरणों के लिए आवश्यकता होगी जिन्हें हम कवर करेंगे:

```csharp
using Aspose.Html;
using Aspose.Html.Configuration;
using Aspose.Html.Sandbox;
using Aspose.Html.Services;
using Aspose.Html.Saving;
using System;
using System.IO;
```

आयातित इन नामस्थानों के साथ, आप .NET के लिए Aspose.HTML द्वारा प्रदान की गई कार्यक्षमता तक पहुंच सकते हैं।

## स्क्रिप्ट निष्पादन अक्षम करें

आइए HTML दस्तावेज़ के भीतर स्क्रिप्ट निष्पादन को अक्षम करने और इसे पीडीएफ में परिवर्तित करने के एक बुनियादी उदाहरण से शुरुआत करें। इन चरणों का पालन करें:

1. एक HTML कोड स्निपेट बनाएं और इसे "document.html" नामक फ़ाइल में सहेजें।

```csharp
var code = "<span>Hello World!!</span> " +
           "<script>document.write('Have a nice day!');</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. 'स्क्रिप्ट' को एक अविश्वसनीय संसाधन के रूप में चिह्नित करते हुए, Aspose.HTML कॉन्फ़िगरेशन को प्रारंभ करें।

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    configuration.Security |= Aspose.Html.Sandbox.Scripts;
    
    // निर्दिष्ट कॉन्फ़िगरेशन के साथ एक HTML दस्तावेज़ प्रारंभ करें
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // HTML को पीडीएफ में बदलें
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

इस उदाहरण में, हमने HTML दस्तावेज़ के भीतर स्क्रिप्ट के निष्पादन को रोक दिया है, इसे पीडीएफ में परिवर्तित करते समय सुरक्षा सुनिश्चित की है। अब, चलिए अगले उदाहरण पर चलते हैं।

## उपयोगकर्ता स्टाइलशीट निर्दिष्ट करें

कभी-कभी, आप HTML दस्तावेज़ के तत्वों पर कस्टम शैलियाँ लागू करना चाह सकते हैं। यहां बताया गया है कि आप .NET के लिए Aspose.HTML का उपयोग करके इसे कैसे कर सकते हैं:

1. एक HTML कोड स्निपेट बनाएं और इसे "document.html" नामक फ़ाइल में सहेजें।

```csharp
var code = @"<span>Hello World!!!</span>";
System.IO.File.WriteAllText("document.html", code);
```

2.  के लिए एक कस्टम रंग सेट करें`<span>` उपयोगकर्ता स्टाइलशीट का उपयोग कर तत्व।

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var userAgent = configuration.GetService<Aspose.Html.Services.IUserAgentService>();
    userAgent.UserStyleSheet = "span { color: green; }";
    
    // निर्दिष्ट कॉन्फ़िगरेशन के साथ एक HTML दस्तावेज़ प्रारंभ करें
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // HTML को पीडीएफ में बदलें
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

 इस उदाहरण में, हमने एक कस्टम शैली लागू की है`<span>`तत्व, इसके टेक्स्ट का रंग हरा पर सेट कर रहा है। .NET के लिए Aspose.HTML आपको शैलियों में आसानी से हेरफेर करने की अनुमति देता है।

## जावास्क्रिप्ट निष्पादन समयबाह्य

संभावित रूप से समय लेने वाले जावास्क्रिप्ट कोड से निपटते समय, अनिश्चितकालीन निष्पादन को रोकने के लिए टाइमआउट सेट करना आवश्यक है। यहां बताया गया है कि आप यह कैसे कर सकते हैं:

1. एक अंतहीन लूप के साथ एक HTML कोड स्निपेट बनाएं और इसे "document.html" नामक फ़ाइल में सहेजें।

```csharp
var code = @"<script>while(true){}</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. जावास्क्रिप्ट निष्पादन टाइमआउट को 10 सेकंड पर सेट करें।

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var runtime = configuration.GetService<Aspose.Html.Services.IRuntimeService>();
    runtime.JavaScriptTimeout = TimeSpan.FromSeconds(10);
    
    // निर्दिष्ट कॉन्फ़िगरेशन के साथ एक HTML दस्तावेज़ प्रारंभ करें
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // सभी स्क्रिप्ट समाप्त/रद्द होने तक प्रतीक्षा करें और HTML को PNG में परिवर्तित करें
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

इस उदाहरण में, हमने जावास्क्रिप्ट निष्पादन समय को 10 सेकंड तक सीमित कर दिया है, यह सुनिश्चित करते हुए कि स्क्रिप्ट अनिश्चित काल तक नहीं चलती है, जो संभावित रूप से प्रदर्शन संबंधी समस्याएं पैदा कर सकती है।

## कस्टम संदेश हैंडलर

कभी-कभी, HTML दस्तावेज़ लोड करते समय आपको त्रुटि संदेशों या अनुपलब्ध संसाधनों को संभालने की आवश्यकता हो सकती है। कस्टम संदेश हैंडलर कैसे बनाएं इसका एक उदाहरण यहां दिया गया है:

1. गुम छवि फ़ाइल संदर्भ के साथ एक HTML कोड स्निपेट बनाएं और इसे "document.html" नामक फ़ाइल में सहेजें।

```csharp
var code = @"<img src='missing.jpg'>";
System.IO.File.WriteAllText("document.html", code);
```

2. विफल अनुरोधों को लॉग करने के लिए नेटवर्क सेवा में एक त्रुटि संदेश हैंडलर जोड़ें।

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var network = configuration.GetService<Aspose.Html.Services.INetworkService>();
    network.MessageHandlers.Add(new LogMessageHandler());
    
    // निर्दिष्ट कॉन्फ़िगरेशन के साथ एक HTML दस्तावेज़ प्रारंभ करें
    // दस्तावेज़ लोड करने के दौरान, एप्लिकेशन छवि लोड करने का प्रयास करेगा, और हम कंसोल में इस ऑपरेशन का परिणाम देखेंगे।
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // HTML को PNG में कनवर्ट करें
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

इस उदाहरण में, हमने एक कस्टम संदेश हैंडलर जोड़ा है (`LogMessageHandler`) विफल अनुरोधों के बारे में जानकारी लॉग करने के लिए। यह डिबगिंग और लापता संसाधनों को शानदार तरीके से संभालने के लिए विशेष रूप से उपयोगी हो सकता है।

## निष्कर्ष

.NET के लिए Aspose.HTML एक बहुमुखी लाइब्रेरी है जो डेवलपर्स को HTML दस्तावेज़ों के साथ कुशलतापूर्वक काम करने में सक्षम बनाती है। इस ट्यूटोरियल में, हमने आवश्यक अवधारणाओं को कवर किया है और स्क्रिप्ट प्रबंधन, स्टाइलशीट अनुकूलन, जावास्क्रिप्ट निष्पादन नियंत्रण और कस्टम संदेश हैंडलिंग सहित सामान्य कार्यों के लिए चरण-दर-चरण उदाहरण प्रदान किए हैं।

इस ट्यूटोरियल में बताए गए चरणों का पालन करके, आप आत्मविश्वास के साथ अपने .NET अनुप्रयोगों में HTML दस्तावेज़ बनाने, हेरफेर करने और परिवर्तित करने के लिए .NET के लिए Aspose.HTML की शक्ति का उपयोग कर सकते हैं।

## अक्सर पूछे जाने वाले प्रश्न

### Q1: क्या मैं लाइसेंस खरीदे बिना .NET के लिए Aspose.HTML का उपयोग कर सकता हूँ?

A1: हाँ, आप नि:शुल्क परीक्षण संस्करण के साथ .NET के लिए Aspose.HTML आज़मा सकते हैं, लेकिन कुछ उन्नत सुविधाओं के लिए वैध लाइसेंस की आवश्यकता हो सकती है।

### Q2: मैं .NET के लिए Aspose.HTML का लाइसेंस कैसे प्राप्त कर सकता हूं?

 A2: आप Aspose वेबसाइट से लाइसेंस खरीद सकते हैं:[Aspose.HTML लाइसेंस खरीदें](https://purchase.aspose.com/buy).

### Q3: .NET के लिए Aspose.HTML का उपयोग करके मैं HTML दस्तावेज़ों को किन प्रारूपों में परिवर्तित कर सकता हूँ?

A3: .NET के लिए Aspose.HTML पीडीएफ, छवियों और अन्य सहित विभिन्न प्रारूपों में रूपांतरण का समर्थन करता है।

### Q4: क्या .NET के लिए Aspose.HTML के लिए कोई समुदाय या सहायता मंच है?

 A4: हाँ, आप Aspose मंचों पर सहायता और समर्थन पा सकते हैं:[Aspose.HTML सहायता फ़ोरम](https://forum.aspose.com/).

### Q5: क्या .NET के लिए Aspose.HTML दस्तावेज़ीकरण और ट्यूटोरियल प्रदान करता है?

 A5: हां, आप यहां दस्तावेज़ तक पहुंच सकते हैं:[.NET दस्तावेज़ीकरण के लिए Aspose.HTML](https://reference.aspose.com/html/net/).
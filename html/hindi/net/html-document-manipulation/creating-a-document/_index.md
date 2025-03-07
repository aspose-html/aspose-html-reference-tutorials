---
title: Aspose.HTML के साथ .NET में दस्तावेज़ बनाना
linktitle: .NET में दस्तावेज़ बनाना
second_title: Aspose.HTML .NET HTML हेरफेर एपीआई
description: .NET के लिए Aspose.HTML की शक्ति का लाभ उठाएँ। HTML और SVG दस्तावेज़ों को आसानी से बनाना, उनमें हेरफेर करना और उन्हें अनुकूलित करना सीखें। चरण-दर-चरण उदाहरण और अक्सर पूछे जाने वाले प्रश्न देखें।
weight: 14
url: /hi/net/html-document-manipulation/creating-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML के साथ .NET में दस्तावेज़ बनाना


वेब डेवलपमेंट की लगातार विकसित होती दुनिया में, वक्र से आगे रहना आवश्यक है। .NET के लिए Aspose.HTML डेवलपर्स को HTML दस्तावेज़ों के साथ काम करने के लिए एक मजबूत टूलकिट प्रदान करता है। चाहे आप स्क्रैच से शुरू कर रहे हों, किसी फ़ाइल से लोड कर रहे हों, URL से खींच रहे हों, या SVG दस्तावेज़ों को संभाल रहे हों, यह लाइब्रेरी आपको आवश्यक बहुमुखी प्रतिभा प्रदान करती है।

इस चरण-दर-चरण मार्गदर्शिका में, हम .NET के लिए Aspose.HTML का उपयोग करने के मूल सिद्धांतों पर चर्चा करेंगे, यह सुनिश्चित करते हुए कि आप अपने वेब डेवलपमेंट प्रोजेक्ट में इस शक्तिशाली टूल का उपयोग करने के लिए अच्छी तरह से सुसज्जित हैं। विवरण में जाने से पहले, आइए अपनी यात्रा शुरू करने के लिए आवश्यक शर्तों और आवश्यक नामस्थानों पर चर्चा करें।

## आवश्यक शर्तें

इस ट्यूटोरियल का सफलतापूर्वक पालन करने और .NET के लिए Aspose.HTML की शक्ति का उपयोग करने के लिए, आपको निम्नलिखित पूर्वापेक्षाएँ चाहिए:

- एक Windows मशीन जिसमें .NET Framework या .NET Core स्थापित हो।
- विजुअल स्टूडियो जैसा एक कोड संपादक.
- C# प्रोग्रामिंग का बुनियादी ज्ञान.

अब जब आपने अपनी पूर्व-आवश्यकताएं तय कर ली हैं, तो चलिए शुरू करते हैं।

## नामस्थान आयात करना

.NET के लिए Aspose.HTML का उपयोग शुरू करने से पहले, आपको आवश्यक नामस्थान आयात करने की आवश्यकता है। इन नामस्थानों में वे क्लास और विधियाँ होती हैं जो HTML दस्तावेज़ों के साथ काम करने के लिए महत्वपूर्ण हैं। नीचे उन नामस्थानों की सूची दी गई है जिन्हें आपको आयात करना चाहिए:

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

इन नामस्थानों को आयात करने के बाद, अब आप चरण-दर-चरण उदाहरणों में उतरने के लिए तैयार हैं।

## स्क्रैच से HTML दस्तावेज़ बनाना

### चरण 1: एक खाली HTML दस्तावेज़ को आरंभ करें

```csharp
// एक रिक्त HTML दस्तावेज़ आरंभ करें.
using (var document = new Aspose.Html.HTMLDocument())
{
    // एक टेक्स्ट तत्व बनाएं और उसे दस्तावेज़ में जोड़ें
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // दस्तावेज़ को डिस्क पर सहेजें.
    document.Save("document.html");
}
```

इस उदाहरण में, हम एक खाली HTML दस्तावेज़ बनाकर और उसमें "Hello World!" टेक्स्ट जोड़कर शुरू करते हैं। फिर हम दस्तावेज़ को एक फ़ाइल में सहेजते हैं।

## किसी फ़ाइल से HTML दस्तावेज़ बनाना

### चरण 1: 'document.html' फ़ाइल तैयार करें

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### चरण 2: 'document.html' फ़ाइल से लोड करें

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // दस्तावेज़ की सामग्री को आउटपुट स्ट्रीम में लिखें.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

यहाँ, हम "Hello World!" सामग्री वाली एक फ़ाइल तैयार करते हैं और फिर उसे HTML दस्तावेज़ के रूप में लोड करते हैं। हम दस्तावेज़ की सामग्री को कंसोल पर प्रिंट करते हैं।

## URL से HTML दस्तावेज़ बनाना

### चरण 1: वेब पेज से दस्तावेज़ लोड करें

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    // दस्तावेज़ की सामग्री को आउटपुट स्ट्रीम में लिखें.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

इस उदाहरण में, हम एक HTML दस्तावेज़ को सीधे वेब पेज से लोड करते हैं और उसकी सामग्री प्रदर्शित करते हैं।

## एक स्ट्रिंग से HTML दस्तावेज़ बनाना

### चरण 1: HTML कोड तैयार करें

```csharp
var html_code = "<p>Hello World!</p>";
```

### चरण 2: स्ट्रिंग वेरिएबल से दस्तावेज़ आरंभ करें

```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // दस्तावेज़ को डिस्क पर सहेजें.
    document.Save("document.html");
}
```

यहां, हम एक स्ट्रिंग वेरिएबल से एक HTML दस्तावेज़ बनाते हैं और इसे एक फ़ाइल में सहेजते हैं।

## मेमोरीस्ट्रीम से HTML दस्तावेज़ बनाना

### चरण 1: मेमोरी स्ट्रीम ऑब्जेक्ट बनाएँ

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    // मेमोरी ऑब्जेक्ट में HTML कोड लिखें
    sw.Write("<p>Hello World!</p>");
    // स्थिति को आरंभ में सेट करें
    sw.Flush();
    mem.Seek(0, System.IO.SeekOrigin.Begin);
    // मेमोरी स्ट्रीम से दस्तावेज़ आरंभ करें
    using (var document = new Aspose.Html.HTMLDocument(mem, "."))
    {
        // दस्तावेज़ को डिस्क पर सहेजें.
        document.Save("document.html");
    }
}
```

इस उदाहरण में, हम मेमोरी स्ट्रीम से एक HTML दस्तावेज़ बनाते हैं और उसे एक फ़ाइल में सहेजते हैं।

## SVG दस्तावेज़ों के साथ कार्य करना

### चरण 1: SVG दस्तावेज़ को स्ट्रिंग से आरंभ करें

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "."))
{
    // दस्तावेज़ की सामग्री को आउटपुट स्ट्रीम में लिखें.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

यहां, हम एक स्ट्रिंग से एक SVG दस्तावेज़ बनाते हैं और प्रदर्शित करते हैं।

## HTML दस्तावेज़ को एसिंक्रोनस रूप से लोड करना

### चरण 1: HTML दस्तावेज़ का उदाहरण बनाएँ

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### चरण 2: 'रेडीस्टेटचेंज' इवेंट की सदस्यता लें

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    // 'रेडीस्टेट' संपत्ति का मान जांचें.
    if (document.ReadyState == "complete")
    {
        Console.WriteLine(document.DocumentElement.OuterHTML);
        Console.WriteLine("Loading is completed. Press any key to continue...");
    }
};
```

### चरण 3: निर्दिष्ट Uri पर एसिंक्रोनस रूप से नेविगेट करें

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

इस उदाहरण में, हम एक HTML दस्तावेज़ को एसिंक्रोनस रूप से लोड करते हैं और लोडिंग पूर्ण होने पर सामग्री प्रदर्शित करने के लिए 'ReadyStateChange' इवेंट को संभालते हैं।

## 'ऑनलोड' इवेंट को संभालना

### चरण 1: HTML दस्तावेज़ का उदाहरण बनाएँ

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### चरण 2: 'ऑनलोड' इवेंट की सदस्यता लें

```csharp
document.OnLoad += (sender, @event) =>
{
    Console.WriteLine(document.DocumentElement.OuterHTML);
    Console.WriteLine("Loading is completed. Press any key to continue...");
};
```

### चरण 3: निर्दिष्ट Uri पर एसिंक्रोनस रूप से नेविगेट करें

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

यह उदाहरण एक HTML दस्तावेज़ को एसिंक्रोनस रूप से लोड करने और पूरा होने पर सामग्री प्रदर्शित करने के लिए 'OnLoad' इवेंट को संभालने का प्रदर्शन करता है।

## निष्कर्ष के तौर पर

वेब डेवलपमेंट की गतिशील दुनिया में, आपके पास सही उपकरण होना बहुत ज़रूरी है। Aspose.HTML for .NET आपको HTML और SVG दस्तावेज़ों को कुशलतापूर्वक बनाने, हेरफेर करने और संसाधित करने के साधनों से लैस करता है। इस व्यापक गाइड ने आपको ज़रूरी चीज़ों से परिचित कराया है, यह सुनिश्चित करते हुए कि आप अपनी परियोजनाओं में Aspose.HTML for .NET की शक्ति का उपयोग कर सकते हैं।

## अक्सर पूछे जाने वाले प्रश्न

### प्रश्न 1: .NET के लिए Aspose.HTML क्या है?

A1: Aspose.HTML for .NET एक शक्तिशाली .NET लाइब्रेरी है जो डेवलपर्स को HTML और SVG दस्तावेज़ों के साथ काम करने में सक्षम बनाती है। यह स्क्रैच से दस्तावेज़ बनाने से लेकर मौजूदा HTML और SVG फ़ाइलों को पार्स करने और हेरफेर करने तक की कई सुविधाएँ प्रदान करता है।

### प्रश्न 2: क्या मैं .NET कोर के साथ .NET के लिए Aspose.HTML का उपयोग कर सकता हूं?

A2: हां, .NET के लिए Aspose.HTML .NET फ्रेमवर्क और .NET कोर दोनों के साथ संगत है, जो इसे आधुनिक .NET अनुप्रयोगों के लिए एक बहुमुखी विकल्प बनाता है।

### प्रश्न 3: क्या .NET के लिए Aspose.HTML वेब स्क्रैपिंग और पार्सिंग के लिए उपयुक्त है?

A3: बिल्कुल! .NET के लिए Aspose.HTML वेब स्क्रैपिंग और पार्सिंग कार्यों के लिए एक बेहतरीन विकल्प है, इसकी वजह है URL और स्ट्रिंग से HTML दस्तावेज़ लोड करने की क्षमता। आप डेटा निकाल सकते हैं, विश्लेषण कर सकते हैं और बहुत कुछ कर सकते हैं।

### प्रश्न 4: मैं .NET के लिए Aspose.HTML हेतु समर्थन कैसे प्राप्त कर सकता हूँ?

 A4: यदि आपको .NET के लिए Aspose.HTML का उपयोग करते समय कोई समस्या आती है या आपके कोई प्रश्न हैं, तो आप यहां जा सकते हैं[एस्पोज फोरम](https://forum.aspose.com/) समुदाय और Aspose विशेषज्ञों से समर्थन और सहायता के लिए।

### उत्तर 5: मैं विस्तृत दस्तावेज और डाउनलोड विकल्प कहां पा सकता हूं?

उत्तर5: विस्तृत दस्तावेज़ीकरण और डाउनलोड विकल्पों तक पहुंच के लिए, आप निम्नलिखित लिंक देख सकते हैं:

- [प्रलेखन](https://reference.aspose.com/html/net/)
- [डाउनलोड करना](https://releases.aspose.com/html/net/)
- [खरीदना](https://purchase.aspose.com/buy)
- [मुफ्त परीक्षण](https://releases.aspose.com/)
- [अस्थायी लाइसेंस](https://purchase.aspose.com/temporary-license/)
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

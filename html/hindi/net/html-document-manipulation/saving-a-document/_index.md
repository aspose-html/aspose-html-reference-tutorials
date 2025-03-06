---
title: Aspose.HTML के साथ .NET में दस्तावेज़ सहेजना
linktitle: .NET में दस्तावेज़ सहेजना
second_title: Aspose.HTML .NET HTML हेरफेर एपीआई
description: हमारे चरण-दर-चरण गाइड के साथ .NET के लिए Aspose.HTML की शक्ति अनलॉक करें। HTML और SVG दस्तावेज़ बनाना, उनमें बदलाव करना और उन्हें परिवर्तित करना सीखें
weight: 16
url: /hi/net/html-document-manipulation/saving-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML के साथ .NET में दस्तावेज़ सहेजना


आज के डिजिटल युग में, HTML और SVG दस्तावेज़ बनाना और उनमें हेरफेर करना कई सॉफ़्टवेयर डेवलपर्स और व्यवसायों के लिए आवश्यक है। .NET के लिए Aspose.HTML एक शक्तिशाली लाइब्रेरी है जो इन कार्यों को सरल बनाती है, HTML, SVG और बहुत कुछ के साथ काम करने के लिए विभिन्न कार्यक्षमताएँ प्रदान करती है। इस व्यापक गाइड में, हम .NET के लिए Aspose.HTML की अनिवार्यताओं में गोता लगाएँगे, प्रत्येक उदाहरण को आसानी से पालन किए जाने वाले चरणों में विभाजित करेंगे। चाहे आप एक अनुभवी डेवलपर हों या अभी शुरुआत कर रहे हों, आपको Aspose.HTML की क्षमताओं का दोहन करने के लिए यह गाइड अमूल्य लगेगी।

## आवश्यक शर्तें

इससे पहले कि हम इस यात्रा पर निकलें, आइए सुनिश्चित करें कि आपके पास वह सब कुछ है जो आपको चाहिए:

- विकास वातावरण: सुनिश्चित करें कि आपके कंप्यूटर पर Visual Studio या कोई अन्य .NET विकास वातावरण स्थापित है।

- .NET के लिए Aspose.HTML: आपको .NET के लिए Aspose.HTML लाइब्रेरी प्राप्त करनी होगी। आप इसे यहाँ से डाउनलोड कर सकते हैं[यहाँ](https://releases.aspose.com/html/net/).

- C# का ज्ञान: C# प्रोग्रामिंग भाषा से परिचित होना लाभदायक है, लेकिन अनिवार्य नहीं है। यह गाइड शुरुआती लोगों के लिए अनुकूल बनाया गया है।

## नामस्थान आयात करें

.NET के लिए Aspose.HTML का उपयोग शुरू करने के लिए, आपको अपने प्रोजेक्ट में आवश्यक नेमस्पेस आयात करने होंगे। अपने C# कोड में, निम्न नेमस्पेस शामिल करें:

### चरण 1: Aspose.HTML नामस्थान आयात करें
```csharp
using Aspose.Html;
```

यह नामस्थान आपको विभिन्न HTML और SVG हेरफेर क्षमताओं तक पहुंच प्रदान करेगा।

## HTML से फ़ाइल

### चरण 1: एक खाली HTML दस्तावेज़ को आरंभ करें
```csharp
// एक रिक्त HTML दस्तावेज़ आरंभ करें.
using (var document = new Aspose.Html.HTMLDocument())
{
    // एक टेक्स्ट तत्व बनाएं और उसे दस्तावेज़ में जोड़ें
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // HTML को डिस्क पर फ़ाइल में सहेजें.
    document.Save("document.html");
}
```

इस उदाहरण में, हम एक HTML दस्तावेज़ बनाते हैं और उसमें एक सरल "Hello World!" टेक्स्ट जोड़ते हैं। फिर हम HTML को डिस्क पर एक फ़ाइल में सहेजते हैं।

## लिंक की गई फ़ाइल के बिना HTML

### चरण 1: एक सरल HTML फ़ाइल तैयार करें
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

यहां, हम एक अन्य फ़ाइल के लिए एंकर लिंक के साथ एक मूल HTML फ़ाइल बनाते हैं।

### चरण 2: 'document.html' को मेमोरी में लोड करें
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // सहेजें विकल्प इंस्टेंस बनाएँ
    var options = new Aspose.Html.Saving.HTMLSaveOptions();
    //लिंक की गई HTML फ़ाइलों को काटने के लिए अधिकतम हैंडलिंग गहराई को 0 पर सेट करें।
    options.ResourceHandlingOptions.MaxHandlingDepth = 0;
    // दस्तावेज़ सहेजें
    document.Save(@".\html-to-file-example\document.html", options);
}
```

इस उदाहरण में, हम एक HTML दस्तावेज़ को मेमोरी में लोड करते हैं, लिंक की गई फ़ाइलों को काटने के लिए अधिकतम हैंडलिंग गहराई सेट करते हैं, और दस्तावेज़ को सहेजते हैं। 

## HTML से MHTML

### चरण 1: एक सरल HTML फ़ाइल तैयार करें
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

उदाहरण 2 की तरह, हम एक अन्य फ़ाइल के लिए एंकर लिंक के साथ एक मूल HTML फ़ाइल बनाते हैं।

### चरण 2: 'document.html' को मेमोरी में लोड करें और MHTML के रूप में सेव करें
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // दस्तावेज़ को MHTML के रूप में सहेजें
    document.Save(@".\html-to-file-example\document.mht", Aspose.Html.Saving.HTMLSaveFormat.MHTML);
}
```

यहां, हम HTML दस्तावेज़ को मेमोरी में लोड करते हैं और इसे MHTML प्रारूप में सेव करते हैं।

## HTML से मार्कडाउन

### चरण 1: HTML कोड तैयार करें
```csharp
var html_code = "<H2>Hello World!</H2>";
```

 इस चरण में, हम एक HTML कोड स्निपेट परिभाषित करते हैं जिसमें`<H2>` तत्व।

### चरण 2: HTML कोड से दस्तावेज़ आरंभ करें और मार्कडाउन के रूप में सहेजें
```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // दस्तावेज़ को मार्कडाउन फ़ाइल के रूप में सहेजें.
    document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
}
```

हम कोड स्निपेट से एक HTML दस्तावेज़ बनाते हैं और उसे मार्कडाउन फ़ाइल के रूप में सहेजते हैं।

## SVG से फ़ाइल

### चरण 1: SVG कोड तैयार करें
```csharp
var code = @"
    <svg xmlns='http://www.w3.org/2000/svg' ऊंचाई='80' चौड़ाई='300'>
        <g fill='none'>
            <path stroke='red' d='M5 20 l215 0' />
            <path stroke='black' d='M5 40 l215 0' />
            <path stroke='blue' d='M5 60 l215 0' />
        </g>
    </svg>";
```

यहां, हम एक SVG कोड बनाते हैं जो एक सरल, रंगीन ग्राफ़िक बनाता है।

### चरण 2: कोड से SVG दस्तावेज़ आरंभ करें और डिस्क पर सहेजें
```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument(code, "."))
{
    // SVG फ़ाइल को डिस्क पर सहेजें
    document.Save("document.svg");
}
```

इस चरण में, हम कोड से एक SVG दस्तावेज़ बनाते हैं और उसे SVG फ़ाइल के रूप में सहेजते हैं।

## निष्कर्ष

.NET के लिए Aspose.HTML एक बहुमुखी लाइब्रेरी है जो आपके .NET अनुप्रयोगों में HTML और SVG दस्तावेज़ हैंडलिंग को सरल बनाती है। इस गाइड में, हमने पाँच आवश्यक उदाहरणों को शामिल किया है, प्रत्येक को चरण-दर-चरण निर्देशों में विभाजित किया है। चाहे आप दस्तावेज़ बना रहे हों, हेरफेर कर रहे हों या परिवर्तित कर रहे हों, Aspose.HTML आपके लिए है। इन चरणों का पालन करके, आप इस शक्तिशाली उपकरण में महारत हासिल करने के अपने रास्ते पर हैं।

## अक्सर पूछे जाने वाले प्रश्न

### प्रश्न 1: .NET के लिए Aspose.HTML क्या है?

A1: Aspose.HTML for .NET एक .NET लाइब्रेरी है जो HTML और SVG दस्तावेज़ों के साथ काम करने के लिए निर्माण, हेरफेर और रूपांतरण सहित सुविधाओं की एक विस्तृत श्रृंखला प्रदान करती है।

### प्रश्न 2: मैं .NET के लिए Aspose.HTML कहां से डाउनलोड कर सकता हूं?

 A2: आप .NET के लिए Aspose.HTML को यहां से डाउनलोड कर सकते हैं[यहाँ](https://releases.aspose.com/html/net/).

### प्रश्न 3: क्या Aspose.HTML for .NET शुरुआती लोगों के लिए उपयुक्त है?

A3: हाँ, .NET के लिए Aspose.HTML का उपयोग शुरुआती और अनुभवी डेवलपर्स दोनों द्वारा किया जा सकता है। इस गाइड में दिए गए उदाहरण शुरुआती लोगों के अनुकूल होने के लिए डिज़ाइन किए गए हैं।

### प्रश्न 4: क्या मैं .NET के लिए Aspose.HTML का उपयोग करके HTML को अन्य प्रारूपों में परिवर्तित कर सकता हूं?

A4: हां, .NET के लिए Aspose.HTML MHTML और Markdown सहित विभिन्न प्रारूपों में रूपांतरण का समर्थन करता है, जैसा कि उदाहरणों में दिखाया गया है।

### प्रश्न 5: मुझे .NET के लिए Aspose.HTML का समर्थन कहां मिल सकता है?

 A5: आप Aspose.HTML समुदाय फ़ोरम में सहायता और अपने प्रश्नों के उत्तर पा सकते हैं[यहाँ](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

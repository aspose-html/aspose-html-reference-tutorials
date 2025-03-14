---
title: Aspose.HTML के साथ .NET में HTML को PNG के रूप में प्रस्तुत करें
linktitle: .NET में HTML को PNG के रूप में प्रस्तुत करें
second_title: Aspose.HTML .NET HTML हेरफेर एपीआई
description: .NET के लिए Aspose.HTML के साथ काम करना सीखें। HTML में हेरफेर करें, विभिन्न प्रारूपों में कनवर्ट करें, और बहुत कुछ। इस व्यापक ट्यूटोरियल में गोता लगाएँ!
weight: 10
url: /hi/net/rendering-html-documents/render-html-as-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML के साथ .NET में HTML को PNG के रूप में प्रस्तुत करें


इस ट्यूटोरियल में, हम .NET के लिए Aspose.HTML की दुनिया में गहराई से जाएंगे, जो HTML दस्तावेज़ों के साथ प्रोग्रामेटिक रूप से काम करने के लिए एक शक्तिशाली उपकरण है। चाहे आप एक अनुभवी डेवलपर हों या .NET प्रोग्रामिंग की दुनिया में अपनी यात्रा शुरू कर रहे हों, यह ट्यूटोरियल आपको Aspose.HTML की अनिवार्यताओं के माध्यम से मार्गदर्शन करेगा, नामस्थानों को आयात करने से लेकर व्यावहारिक उदाहरणों को तोड़ने तक।

## परिचय

.NET के लिए Aspose.HTML एक बहुमुखी लाइब्रेरी है जो डेवलपर्स को HTML दस्तावेज़ों को आसानी से हेरफेर करने में सक्षम बनाती है। चाहे आपको HTML को अन्य प्रारूपों में बदलना हो, HTML दस्तावेज़ों से डेटा निकालना हो या गतिशील HTML सामग्री बनानी हो, Aspose.HTML आपके लिए है। इस ट्यूटोरियल में, हम इसकी क्षमताओं को चरण दर चरण देखेंगे।

## आवश्यक शर्तें

इससे पहले कि हम कोड उदाहरणों में उतरें, आपको कुछ पूर्वावश्यकताओं की आवश्यकता होगी:

1. विज़ुअल स्टूडियो: सुनिश्चित करें कि आपके पास विज़ुअल स्टूडियो स्थापित है, क्योंकि हम .NET कोड लिखेंगे।

2.  .NET के लिए Aspose.HTML: .NET के लिए Aspose.HTML लाइब्रेरी को यहां से डाउनलोड और इंस्टॉल करें[इस लिंक](https://releases.aspose.com/html/net/) आप निशुल्क परीक्षण या लाइसेंस खरीदने के बीच चयन कर सकते हैं[यहाँ](https://purchase.aspose.com/buy).

3. .NET फ्रेमवर्क या .NET कोर: सुनिश्चित करें कि आपके प्रोजेक्ट की आवश्यकताओं के आधार पर, आपके विकास मशीन पर .NET फ्रेमवर्क या .NET कोर स्थापित है।

4. कोड संपादक: आप विजुअल स्टूडियो या अपनी पसंद के किसी अन्य कोड संपादक का उपयोग कर सकते हैं।

## नामस्थान आयात करना

.NET के लिए Aspose.HTML के साथ आरंभ करने के लिए, हमें सबसे पहले आवश्यक नामस्थान आयात करने की आवश्यकता है। Visual Studio में अपना प्रोजेक्ट खोलें, एक नया C# क्लास बनाएँ, और निम्नलिखित नामस्थान आयात करें:

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;
```

ये नामस्थान HTML दस्तावेजों के साथ प्रोग्रामेटिक रूप से काम करने के लिए आवश्यक विभिन्न वर्गों और विधियों तक पहुंच प्रदान करते हैं।

## HTML को PNG के रूप में प्रस्तुत करें उदाहरण

आइए आपके द्वारा दिए गए कोड उदाहरण पर करीब से नज़र डालें और इसे कई चरणों में विभाजित करें:

```csharp
// Aspose.HTML के साथ .NET में HTML को PNG के रूप में प्रस्तुत करें
string dataDir = "Your Data Directory";

// चरण 1: एक HTML दस्तावेज़ ऑब्जेक्ट बनाएँ
using (var document = new Aspose.Html.HTMLDocument("<style>p { color: green; }</style><p>my first paragraph</p>", @"c:\work\"))
{
    // चरण 2: HTML रेंडरर बनाएं
    using (HtmlRenderer renderer = new HtmlRenderer())
    using (ImageDevice device = new ImageDevice(dataDir + @"document_out.png"))
    {
        // चरण 3: HTML दस्तावेज़ को PNG में प्रस्तुत करें
        renderer.Render(device, document);
    }
}
```

### चरण 1: HTML दस्तावेज़ ऑब्जेक्ट बनाएँ

 इस चरण में, हम एक बनाते हैं`HTMLDocument` ऑब्जेक्ट, जो एक HTML दस्तावेज़ का प्रतिनिधित्व करता है। आप HTML सामग्री को कंस्ट्रक्टर को स्ट्रिंग के रूप में पास कर सकते हैं, और आप सापेक्ष पथों को हल करने के लिए आधार पथ भी निर्दिष्ट कर सकते हैं।

### चरण 2: HTML रेंडरर बनाएं

 यहाँ, हम एक बनाते हैं`HtmlRenderer` ऑब्जेक्ट. यह HTML सामग्री को प्रस्तुत करने के लिए जिम्मेदार मुख्य घटक है. 

### चरण 3: HTML दस्तावेज़ को PNG में प्रस्तुत करें

 अंत में, हम HTML दस्तावेज़ को PNG छवि में प्रस्तुत करते हैं`HtmlRenderer` और एक`ImageDevice` परिणामी PNG छवि निर्दिष्ट स्थान पर सहेजी जाएगी।`dataDir`.

## निष्कर्ष

इस ट्यूटोरियल में, हमने आपको .NET के लिए Aspose.HTML से परिचित कराया है और उदाहरण कोड का विश्लेषण प्रदान किया है। यह सिर्फ़ शुरुआत है कि आप इस शक्तिशाली लाइब्रेरी के साथ क्या हासिल कर सकते हैं। आप इसके विस्तृत दस्तावेज़ देख सकते हैं[यहाँ](https://reference.aspose.com/html/net/) और अतिरिक्त संसाधनों और सहायता तक पहुँच प्राप्त करें[Aspose फ़ोरम](https://forum.aspose.com/).

यदि आपके पास कोई प्रश्न है या .NET के लिए Aspose.HTML के बारे में सहायता की आवश्यकता है, तो कृपया Aspose समुदाय से संपर्क करें या आगे के मार्गदर्शन के लिए दस्तावेज़ देखें।

## अक्सर पूछे जाने वाले प्रश्न (एफएक्यू)

### .NET के लिए Aspose.HTML क्या है?
   .NET के लिए Aspose.HTML एक लाइब्रेरी है जो डेवलपर्स को .NET अनुप्रयोगों में HTML दस्तावेज़ों को प्रोग्रामेटिक रूप से बदलने और परिवर्तित करने की अनुमति देती है।

### मैं .NET के लिए Aspose.HTML हेतु अस्थायी लाइसेंस कैसे प्राप्त कर सकता हूं?
    आप .NET के लिए Aspose.HTML हेतु अस्थायी लाइसेंस प्राप्त कर सकते हैं[यहाँ](https://purchase.aspose.com/temporary-license/).

### क्या मैं .NET के लिए Aspose.HTML का उपयोग करके HTML को अन्य प्रारूपों में परिवर्तित कर सकता हूं?
   हां, .NET के लिए Aspose.HTML HTML को PDF, XPS और छवियों जैसे प्रारूपों में परिवर्तित करने के लिए विभिन्न कन्वर्टर्स प्रदान करता है।

### क्या .NET के लिए Aspose.HTML का निःशुल्क परीक्षण उपलब्ध है?
    हां, आप .NET के लिए Aspose.HTML का निःशुल्क परीक्षण डाउनलोड कर सकते हैं[यहाँ](https://releases.aspose.com/).

### मैं और अधिक ट्यूटोरियल और दस्तावेज़ कहां पा सकता हूं?
   आप इस पर व्यापक दस्तावेज और ट्यूटोरियल देख सकते हैं[.NET के लिए Aspose.HTML दस्तावेज़न पृष्ठ](https://reference.aspose.com/html/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---
title: Aspose.HTML के साथ .NET में EPUB को XPS में बदलें
linktitle: .NET में EPUB को XPS में बदलें
second_title: Aspose.HTML .NET HTML हेरफेर एपीआई
description: .NET के लिए Aspose.HTML का उपयोग करके .NET में EPUB को XPS में परिवर्तित करने का तरीका जानें। सहज रूपांतरणों के लिए हमारी चरण-दर-चरण मार्गदर्शिका का पालन करें।
type: docs
weight: 13
url: /hi/net/html-extensions-and-conversions/convert-epub-to-xps/
---

क्या आप अपने .NET अनुप्रयोगों में EPUB फ़ाइलों को XPS प्रारूप में परिवर्तित करने का एक सहज तरीका ढूंढ रहे हैं? .NET के लिए Aspose.HTML इसे सहजता से प्राप्त करने के लिए एक शक्तिशाली समाधान प्रदान करता है। इस चरण-दर-चरण मार्गदर्शिका में, हम आपको Aspose.HTML का उपयोग करके EPUB को XPS में परिवर्तित करने की प्रक्रिया के बारे में बताएंगे। आएँ शुरू करें!

## आवश्यक शर्तें

इससे पहले कि आप EPUB से XPS रूपांतरण प्रक्रिया में उतरें, आपको यह सुनिश्चित करना होगा कि आपके पास निम्नलिखित शर्तें हैं:

### 1. .NET लाइब्रेरी के लिए Aspose.HTML

 सुनिश्चित करें कि आपके प्रोजेक्ट में .NET लाइब्रेरी के लिए Aspose.HTML स्थापित है। यदि आपने ऐसा नहीं किया है, तो आप इसे यहां से प्राप्त कर सकते हैं[.NET डाउनलोड पेज के लिए Aspose.HTML](https://releases.aspose.com/html/net/).

### 2. इनपुट EPUB फ़ाइल

आपको एक EPUB फ़ाइल की आवश्यकता होगी जिसे आप XPS में कनवर्ट करना चाहते हैं। सुनिश्चित करें कि आपके पास रूपांतरण के लिए एक EPUB फ़ाइल उपलब्ध है।

### 3. .NET विकास पर्यावरण

यह मार्गदर्शिका मानती है कि आपकी मशीन पर एक कार्यशील .NET विकास वातावरण स्थापित है।

## नेमस्पेस आयात करें

आरंभ करने के लिए, आपको Aspose.HTML के लिए आवश्यक नामस्थान आयात करना चाहिए:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## EPUB को XPS में कनवर्ट करें

आइए EPUB फ़ाइल को XPS प्रारूप में परिवर्तित करने की प्रक्रिया को कई चरणों में विभाजित करें।

### चरण 1.1: EPUB फ़ाइल खोलें

सबसे पहले, फ़ाइलस्ट्रीम का उपयोग करके पढ़ने के लिए मौजूदा EPUB फ़ाइल खोलें:

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // रूपांतरण प्रक्रिया जारी रखें
}
```

### चरण 1.2: XpsSaveOptions बनाएं

XpsSaveOptions का एक उदाहरण बनाएं। XPS आउटपुट को कॉन्फ़िगर करने के लिए यह चरण महत्वपूर्ण है:

```csharp
var options = new XpsSaveOptions();
```

### चरण 1.3: EPUB को XPS में बदलें

अब, EPUB को XPS में बदलने के लिए ConvertEPUB विधि को कॉल करें:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## कस्टम XPS विकल्प निर्दिष्ट करें

आप पृष्ठ आकार और पृष्ठभूमि रंग जैसे कस्टम विकल्प निर्दिष्ट करके XPS आउटपुट को और अधिक अनुकूलित कर सकते हैं।

### चरण 2.1: कस्टम पृष्ठ आकार और पृष्ठभूमि रंग

कस्टम पेज आकार और पृष्ठभूमि रंग के साथ XpsSaveOptions का एक उदाहरण बनाएं:

```csharp
var options = new XpsSaveOptions()
{
    PageSetup =
    {
        AnyPage = new Page()
        {
            Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
        }
    },
    BackgroundColor = System.Drawing.Color.AliceBlue,
};
```

### चरण 2.2: कस्टम विकल्पों के साथ EPUB को XPS में बदलें

अब, कस्टम विकल्पों के साथ EPUB को XPS में बदलने के लिए ConvertEPUB विधि को कॉल करें:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## कस्टम स्ट्रीम प्रदाता का उपयोग करें

इस चरण में, हम एक कस्टम स्ट्रीम प्रदाता का उपयोग करके EPUB को XPS में परिवर्तित करेंगे, जिससे आप परिणामी डेटा में हेरफेर कर सकेंगे।

### चरण 3.1: एक मेमोरीस्ट्रीमप्रोवाइडर बनाएं

MemoryStreamProvider का एक उदाहरण बनाएं:

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    // रूपांतरण प्रक्रिया जारी रखें
}
```

### चरण 3.2: स्ट्रीम प्रदाता के साथ EPUB को XPS में बदलें

MemoryStreamProvider का उपयोग करके EPUB को XPS में बदलें:

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### चरण 3.3: परिणाम तक पहुंचें और सहेजें

परिवर्तित डेटा वाली मेमोरी स्ट्रीम को पुनः प्राप्त करें और इसे आउटपुट फ़ाइल में सहेजें:

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

### क्लास मेमोरीस्ट्रीमप्रोवाइडर सोर्स कोड

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // दस्तावेज़ रेंडरिंग के दौरान बनाई गई मेमोरीस्ट्रीम ऑब्जेक्ट की सूची
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // इस विधि को तब कॉल किया जाता है जब केवल एक आउटपुट स्ट्रीम की आवश्यकता होती है, उदाहरण के लिए एक्सपीएस, पीडीएफ या टीआईएफएफ प्रारूपों के लिए।
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // इस विधि को तब कहा जाता है जब एकाधिक आउटपुट स्ट्रीम के निर्माण की आवश्यकता होती है। उदाहरण के लिए छवि फ़ाइलों (जेपीजी, पीएनजी, आदि) की सूची में HTML प्रस्तुत करने के दौरान
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // यहां आप डेटा से भरी स्ट्रीम को रिलीज़ कर सकते हैं और, उदाहरण के लिए, इसे हार्ड-ड्राइव पर फ्लश कर सकते हैं
            }
            public void Dispose()
            {
                // संसाधन जारी करना
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
बधाई हो! आपने .NET के लिए Aspose.HTML का उपयोग करके EPUB फ़ाइल को XPS प्रारूप में सफलतापूर्वक परिवर्तित कर लिया है।

## निष्कर्ष

इस व्यापक ट्यूटोरियल में, हमने पता लगाया कि विभिन्न अनुकूलन विकल्पों के साथ EPUB फ़ाइलों को XPS प्रारूप में परिवर्तित करने के लिए .NET के लिए Aspose.HTML का लाभ कैसे उठाया जाए। चाहे आप एक अनुभवी डेवलपर हों या अभी शुरुआत कर रहे हों, Aspose.HTML प्रक्रिया को सरल बनाता है, जिससे आप EPUB से XPS रूपांतरणों को आसानी से संभाल सकते हैं।

 क्या आपके कोई प्रश्न हैं या कोई समस्या आई है? इसकी जाँच पड़ताल करो[Aspose.HTML दस्तावेज़ीकरण](https://reference.aspose.com/html/net/) अधिक जानकारी के लिए या सहायता लेने के लिए[Aspose.HTML सामुदायिक मंच](https://forum.aspose.com/).

## अक्सर पूछे जाने वाले प्रश्नों

### .NET के लिए Aspose.HTML क्या है?
.NET के लिए Aspose.HTML एक शक्तिशाली लाइब्रेरी है जो डेवलपर्स को .NET अनुप्रयोगों में HTML, EPUB और XPS दस्तावेज़ों के साथ काम करने में सक्षम बनाती है।

### मैं .NET के लिए Aspose.HTML कहाँ से डाउनलोड कर सकता हूँ?
 आप .NET के लिए Aspose.HTML डाउनलोड कर सकते हैं[डाउनलोड पेज](https://releases.aspose.com/html/net/).

### क्या .NET के लिए Aspose.HTML का निःशुल्क परीक्षण उपलब्ध है?
 हाँ, आप नि:शुल्क परीक्षण प्राप्त कर सकते हैं[यहाँ](https://releases.aspose.com/).

### मैं .NET के लिए Aspose.HTML के लिए अस्थायी लाइसेंस कैसे प्राप्त कर सकता हूं?
 अस्थायी लाइसेंस प्राप्त करने के लिए, पर जाएँ[अस्थायी लाइसेंस पृष्ठ](https://purchase.aspose.com/temporary-license/).

### मुझे .NET के लिए Aspose.HTML के लिए और अधिक ट्यूटोरियल और दस्तावेज़ कहां मिल सकते हैं?
 ट्यूटोरियल की एक विस्तृत श्रृंखला और विस्तृत दस्तावेज़ीकरण का अन्वेषण करें[Aspose.HTML दस्तावेज़ीकरण](https://reference.aspose.com/html/net/) पृष्ठ।
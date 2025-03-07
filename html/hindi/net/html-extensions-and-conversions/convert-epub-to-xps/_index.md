---
title: Aspose.HTML के साथ .NET में EPUB को XPS में बदलें
linktitle: .NET में EPUB को XPS में बदलें
second_title: Aspose.HTML .NET HTML हेरफेर एपीआई
description: .NET के लिए Aspose.HTML का उपयोग करके .NET में EPUB को XPS में कैसे बदलें, यह जानें। सरल रूपांतरण के लिए हमारे चरण-दर-चरण मार्गदर्शिका का पालन करें।
weight: 13
url: /hi/net/html-extensions-and-conversions/convert-epub-to-xps/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML के साथ .NET में EPUB को XPS में बदलें


क्या आप अपने .NET एप्लीकेशन में EPUB फ़ाइलों को XPS फ़ॉर्मेट में बदलने का सहज तरीका खोज रहे हैं? .NET के लिए Aspose.HTML इसे आसानी से प्राप्त करने के लिए एक शक्तिशाली समाधान प्रदान करता है। इस चरण-दर-चरण मार्गदर्शिका में, हम आपको Aspose.HTML का उपयोग करके EPUB को XPS में बदलने की प्रक्रिया से अवगत कराएँगे। चलिए शुरू करते हैं!

## आवश्यक शर्तें

EPUB से XPS रूपांतरण प्रक्रिया में उतरने से पहले, आपको यह सुनिश्चित करना होगा कि आपके पास निम्नलिखित पूर्वापेक्षाएँ मौजूद हैं:

### 1. .NET लाइब्रेरी के लिए Aspose.HTML

 सुनिश्चित करें कि आपके प्रोजेक्ट में Aspose.HTML for .NET लाइब्रेरी स्थापित है। यदि आपने ऐसा नहीं किया है, तो आप इसे यहाँ से प्राप्त कर सकते हैं।[.NET के लिए Aspose.HTML डाउनलोड पृष्ठ](https://releases.aspose.com/html/net/).

### 2. EPUB फ़ाइल इनपुट करें

आपको एक EPUB फ़ाइल की आवश्यकता होगी जिसे आप XPS में बदलना चाहते हैं। सुनिश्चित करें कि आपके पास रूपांतरण के लिए एक EPUB फ़ाइल उपलब्ध है।

### 3. .NET विकास वातावरण

यह मार्गदर्शिका मानती है कि आपके मशीन पर एक कार्यशील .NET विकास वातावरण स्थापित है।

## नामस्थान आयात करें

आरंभ करने के लिए, आपको Aspose.HTML के लिए आवश्यक नामस्थान आयात करना चाहिए:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## EPUB को XPS में बदलें

आइए EPUB फ़ाइल को XPS प्रारूप में परिवर्तित करने की प्रक्रिया को कई चरणों में विभाजित करें।

### चरण 1.1: EPUB फ़ाइल खोलें

सबसे पहले, FileStream का उपयोग करके पढ़ने के लिए मौजूदा EPUB फ़ाइल खोलें:

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // रूपांतरण प्रक्रिया जारी रखें
}
```

### चरण 1.2: XpsSaveOptions बनाएँ

XpsSaveOptions का एक इंस्टेंस बनाएँ। XPS आउटपुट को कॉन्फ़िगर करने के लिए यह चरण महत्वपूर्ण है:

```csharp
var options = new XpsSaveOptions();
```

### चरण 1.3: EPUB को XPS में बदलें

अब, EPUB को XPS में बदलने के लिए ConvertEPUB विधि का उपयोग करें:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## कस्टम XPS विकल्प निर्दिष्ट करें

आप पृष्ठ आकार और पृष्ठभूमि रंग जैसे कस्टम विकल्प निर्दिष्ट करके XPS आउटपुट को और अधिक अनुकूलित कर सकते हैं।

### चरण 2.1: कस्टम पेज आकार और पृष्ठभूमि रंग

कस्टम पृष्ठ आकार और पृष्ठभूमि रंग के साथ XpsSaveOptions का एक उदाहरण बनाएं:

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

### चरण 3.1: मेमोरीस्ट्रीमप्रदाता बनाएँ

MemoryStreamProvider का एक उदाहरण बनाएँ:

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

### चरण 3.3: परिणाम तक पहुंचें और उसे सेव करें

परिवर्तित डेटा युक्त मेमोरी स्ट्रीम को पुनः प्राप्त करें और उसे आउटपुट फ़ाइल में सहेजें:

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

### क्लास मेमोरीस्ट्रीमप्रोवाइडर स्रोत कोड

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // दस्तावेज़ रेंडरिंग के दौरान बनाए गए मेमोरीस्ट्रीम ऑब्जेक्ट्स की सूची
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // इस विधि को तब बुलाया जाता है जब केवल एक आउटपुट स्ट्रीम की आवश्यकता होती है, उदाहरण के लिए XPS, PDF या TIFF प्रारूपों के लिए।
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // इस विधि को तब बुलाया जाता है जब कई आउटपुट स्ट्रीम बनाने की आवश्यकता होती है। उदाहरण के लिए, HTML को इमेज फ़ाइलों (JPG, PNG, आदि) की सूची में रेंडर करने के दौरान।
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

इस व्यापक ट्यूटोरियल में, हमने विभिन्न अनुकूलन विकल्पों के साथ EPUB फ़ाइलों को XPS प्रारूप में बदलने के लिए .NET के लिए Aspose.HTML का लाभ उठाने का तरीका खोजा। चाहे आप एक अनुभवी डेवलपर हों या अभी शुरुआत कर रहे हों, Aspose.HTML प्रक्रिया को सरल बनाता है, जिससे आप आसानी से EPUB से XPS रूपांतरणों को संभाल सकते हैं।

 क्या आपके कोई प्रश्न हैं या आपको कोई समस्या आई है?[Aspose.HTML दस्तावेज़ीकरण](https://reference.aspose.com/html/net/) अधिक जानकारी के लिए या सहायता प्राप्त करें[Aspose.HTML सामुदायिक मंच](https://forum.aspose.com/).

## अक्सर पूछे जाने वाले प्रश्नों

### .NET के लिए Aspose.HTML क्या है?
.NET के लिए Aspose.HTML एक शक्तिशाली लाइब्रेरी है जो डेवलपर्स को .NET अनुप्रयोगों में HTML, EPUB और XPS दस्तावेज़ों के साथ काम करने में सक्षम बनाती है।

### मैं .NET के लिए Aspose.HTML कहां से डाउनलोड कर सकता हूं?
 आप .NET के लिए Aspose.HTML को यहाँ से डाउनलोड कर सकते हैं।[डाउनलोड पृष्ठ](https://releases.aspose.com/html/net/).

### क्या .NET के लिए Aspose.HTML का निःशुल्क परीक्षण उपलब्ध है?
 हां, आप यहां से निःशुल्क परीक्षण प्राप्त कर सकते हैं[यहाँ](https://releases.aspose.com/).

### मैं .NET के लिए Aspose.HTML हेतु अस्थायी लाइसेंस कैसे प्राप्त कर सकता हूं?
 अस्थायी लाइसेंस प्राप्त करने के लिए, यहां जाएं[अस्थायी लाइसेंस पृष्ठ](https://purchase.aspose.com/temporary-license/).

### मैं .NET के लिए Aspose.HTML के लिए अधिक ट्यूटोरियल और दस्तावेज़ कहां पा सकता हूं?
 ट्यूटोरियल और विस्तृत दस्तावेज़ीकरण की एक विस्तृत श्रृंखला का अन्वेषण करें[Aspose.HTML दस्तावेज़ीकरण](https://reference.aspose.com/html/net/) पृष्ठ.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

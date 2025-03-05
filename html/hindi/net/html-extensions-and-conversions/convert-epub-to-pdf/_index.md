---
title: Aspose.HTML के साथ .NET में EPUB को PDF में बदलें
linktitle: .NET में EPUB को PDF में बदलें
second_title: Aspose.HTML .NET HTML हेरफेर एपीआई
description: जानें कि .NET के लिए Aspose.HTML का उपयोग करके EPUB को PDF में कैसे बदलें। यह चरण-दर-चरण मार्गदर्शिका सहज दस्तावेज़ रूपांतरण के लिए अनुकूलन विकल्प, FAQ और बहुत कुछ शामिल करती है।
type: docs
weight: 12
url: /hi/net/html-extensions-and-conversions/convert-epub-to-pdf/
---

इस ट्यूटोरियल में, हम EPUB फ़ाइलों को PDF में बदलने के लिए .NET के लिए Aspose.HTML का उपयोग करने का तरीका जानेंगे। Aspose.HTML एक शक्तिशाली .NET लाइब्रेरी है जो HTML और EPUB दस्तावेज़ों के साथ काम करने के लिए विभिन्न कार्यक्षमताएँ प्रदान करती है। हम पूर्वापेक्षाएँ कवर करेंगे, आवश्यक नामस्थान आयात करेंगे, और प्रत्येक चरण को विस्तार से समझाते हुए कई उदाहरणों को तोड़ेंगे।

## आवश्यक शर्तें

आरंभ करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ मौजूद हैं:

1. .NET के लिए Aspose.HTML: सुनिश्चित करें कि आपके .NET प्रोजेक्ट में .NET के लिए Aspose.HTML इंस्टॉल है। आप इसे यहाँ से डाउनलोड कर सकते हैं[यहाँ](https://releases.aspose.com/html/net/).

2. आपकी डेटा निर्देशिका: आपको एक डेटा निर्देशिका की आवश्यकता होगी जहां आपकी EPUB फ़ाइलें संग्रहीत हों।

अब, आइए .NET के लिए Aspose.HTML का उपयोग करके EPUB को PDF में परिवर्तित करने की चरण-दर-चरण प्रक्रिया पर नजर डालें।

## EPUB को PDF में बदलें

### चरण 1: अपना प्रोजेक्ट आरंभ करें

सुनिश्चित करें कि आपके पास .NET प्रोजेक्ट सेटअप है, और .NET के लिए Aspose.HTML स्थापित है।

### चरण 2: आवश्यक नामस्थान आयात करें

अपनी C# कोड फ़ाइल में, आवश्यक नामस्थान आयात करें:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
```

### चरण 3: EPUB फ़ाइल खोलें

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // अगले कदम के लिए आगे बढ़ें...
}
```

-  प्रतिस्थापित करें`"Your Data Directory"` वास्तविक निर्देशिका के साथ जहां आपकी EPUB फ़ाइल स्थित है।
- यह कोड EPUB फ़ाइल को पढ़ने के लिए खोलता है।

### चरण 4: पीडीएफ विकल्प सेट करें और रूपांतरण करें

```csharp
var options = new PdfSaveOptions();
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  इसका एक उदाहरण बनाएं`PdfSaveOptions` पीडीएफ रूपांतरण सेटिंग्स निर्दिष्ट करने के लिए.
-  उपयोग`Converter.ConvertEPUB` दिए गए विकल्पों के साथ EPUB को PDF में परिवर्तित करने की विधि।
- परिणामी पीडीएफ को "output.pdf" के रूप में सहेजें।

## पीडीएफ सेव विकल्प निर्दिष्ट करें

### चरण 1: अपना प्रोजेक्ट आरंभ करें

सुनिश्चित करें कि आपके पास .NET प्रोजेक्ट सेटअप है और .NET के लिए Aspose.HTML इंस्टॉल है।

### चरण 2: आवश्यक नामस्थान आयात करें

अपने C# कोड में आवश्यक नामस्थान आयात करें:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
```

### चरण 3: EPUB फ़ाइल खोलें

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // अगले कदम के लिए आगे बढ़ें...
}
```

-  प्रतिस्थापित करें`"Your Data Directory"` अपनी EPUB फ़ाइल की वास्तविक निर्देशिका के साथ.
- पढ़ने के लिए EPUB फ़ाइल खोलें.

### चरण 4: PDF विकल्प अनुकूलित करें

```csharp
var options = new PdfSaveOptions()
{
    PageSetup = { AnyPage = new Page() { Size = Size.FromPixels(3000, 1000) } },
    BackgroundColor = System.Drawing.Color.AliceBlue
};
```

-  इसका एक उदाहरण बनाएं`PdfSaveOptions` और अपनी आवश्यकताओं के अनुसार इसे अनुकूलित करें।
- इस उदाहरण में, हमने पृष्ठ का आकार 3000 पिक्सेल चौड़ाई और 1000 पिक्सेल ऊंचाई पर सेट किया है, तथा पृष्ठभूमि का रंग ऐलिस ब्लू पर सेट किया है।

### चरण 5: रूपांतरण करें

```csharp
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  उपयोग`Converter.ConvertEPUB` कस्टम विकल्पों के साथ EPUB को PDF में परिवर्तित करने की विधि।
- परिणामी पीडीएफ को "output.pdf" के रूप में सहेजें।

## कस्टम स्ट्रीम प्रदाता का उपयोग करें

### चरण 1: अपना प्रोजेक्ट आरंभ करें

.NET प्रोजेक्ट सेट अप करें और .NET के लिए Aspose.HTML इंस्टॉल करें।

### चरण 2: आवश्यक नामस्थान आयात करें

अपने C# कोड में, आवश्यक नामस्थान आयात करें:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
```

### चरण 3: EPUB फ़ाइल खोलें

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // अगले कदम के लिए आगे बढ़ें...
}
```

-  प्रतिस्थापित करें`"Your Data Directory"` अपनी EPUB फ़ाइल की वास्तविक निर्देशिका के साथ.
- पढ़ने के लिए EPUB फ़ाइल खोलें.

### चरण 4: कस्टम स्ट्रीम प्रदाता का उपयोग करें

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    Converter.ConvertEPUB(stream, new PdfSaveOptions(), streamProvider);

    // अगले कदम के लिए आगे बढ़ें...
}
```

-  एक बनाने के`MemoryStreamProvider` रूपांतरण परिणाम को मेमोरी स्ट्रीम के रूप में प्रबंधित करने के लिए.
-  उपयोग`Converter.ConvertEPUB` कस्टम स्ट्रीम प्रदाता के साथ विधि।

### चरण 5: परिणाम सहेजें

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.pdf"))
{
    memory.CopyTo(fs);
}
```

- परिवर्तित डेटा युक्त मेमोरी स्ट्रीम तक पहुँचें.
- स्ट्रीम की स्थिति को आरंभ में सेट करें.
- एक आउटपुट पीडीएफ फाइल बनाएं और मेमोरी स्ट्रीम से सामग्री को उसमें कॉपी करें।

### क्लास MemoryStreamProvider स्रोत कोड. 

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
अब, आपने सीखा है कि विभिन्न विकल्पों और अनुकूलन संभावनाओं के साथ .NET के लिए Aspose.HTML का उपयोग करके EPUB फ़ाइलों को PDF में कैसे परिवर्तित किया जाए। Aspose.HTML प्रक्रिया को सरल बनाता है, आपके दस्तावेज़ रूपांतरण पर लचीलापन और नियंत्रण प्रदान करता है।

## निष्कर्ष

.NET के लिए Aspose.HTML EPUB फ़ाइलों को PDF में बदलने के लिए एक बहुमुखी उपकरण है, जो परिणामी PDF दस्तावेज़ को आपकी ज़रूरतों के हिसाब से तैयार करने के लिए अनुकूलन विकल्प प्रदान करता है। चाहे आपको सरल रूपांतरण या उन्नत अनुकूलन की आवश्यकता हो, Aspose.HTML आपके लिए है।

 यदि आपने अभी तक ऐसा नहीं किया है, तो आप .NET के लिए Aspose.HTML को यहां से डाउनलोड कर सकते हैं।[वेबसाइट](https://releases.aspose.com/html/net/) और आज ही अपने .NET अनुप्रयोगों में इसका उपयोग शुरू करें।

---

## पूछे जाने वाले प्रश्न

### क्या .NET के लिए Aspose.HTML का उपयोग निःशुल्क है?
    .NET के लिए Aspose.HTML एक वाणिज्यिक उत्पाद है, लेकिन एक निःशुल्क परीक्षण उपलब्ध है[यहाँ](https://releases.aspose.com/).

### क्या मैं परिवर्तित पीडीएफ के स्वरूप को अनुकूलित कर सकता हूं?
   हां, आप पृष्ठ आकार और पृष्ठभूमि रंग जैसे विकल्पों को समायोजित करके पीडीएफ स्वरूप को अनुकूलित कर सकते हैं, जैसा कि उदाहरण 2 में दिखाया गया है।

### मैं .NET के लिए Aspose.HTML का समर्थन कैसे प्राप्त कर सकता हूं?
    आप यहां पर सहायता और संसाधन पा सकते हैं[Aspose.HTML फ़ोरम](https://forum.aspose.com/).

### क्या ऐसे अन्य प्रारूप हैं जिन्हें मैं .NET के लिए Aspose.HTML के साथ परिवर्तित कर सकता हूं?
   हां, .NET के लिए Aspose.HTML HTML, EPUB, और अधिक सहित विभिन्न दस्तावेज़ स्वरूपों का समर्थन करता है।

### क्या Aspose.HTML for ..NET बड़े पैमाने पर दस्तावेज़ रूपांतरण के लिए उपयुक्त है?
   .NET के लिए Aspose.HTML को बड़े पैमाने पर दस्तावेज़ रूपांतरणों को कुशलतापूर्वक संभालने के लिए डिज़ाइन किया गया है, जो इसे अनुप्रयोगों की एक विस्तृत श्रृंखला के लिए उपयुक्त बनाता है।


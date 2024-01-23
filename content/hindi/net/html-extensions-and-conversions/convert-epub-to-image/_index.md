---
title: Aspose.HTML के साथ .NET में EPUB को इमेज में बदलें
linktitle: .NET में EPUB को इमेज में बदलें
second_title: Aspose.HTML .NET HTML हेरफेर एपीआई
description: .NET के लिए Aspose.HTML का उपयोग करके EPUB को छवियों में परिवर्तित करने का तरीका जानें। कोड उदाहरणों और अनुकूलन योग्य विकल्पों के साथ चरण-दर-चरण ट्यूटोरियल।
type: docs
weight: 11
url: /hi/net/html-extensions-and-conversions/convert-epub-to-image/
---

आज के डिजिटल युग में, विभिन्न दस्तावेज़ प्रारूपों में हेरफेर करने और परिवर्तित करने की क्षमता एक मूल्यवान कौशल है। .NET के लिए Aspose.HTML एक शक्तिशाली उपकरण है जो डेवलपर्स को HTML और EPUB दस्तावेज़ों के साथ सहजता से काम करने की अनुमति देता है। इस ट्यूटोरियल में, हम .NET के लिए Aspose.HTML की दुनिया में गहराई से उतरेंगे और EPUB दस्तावेज़ों को विभिन्न छवि प्रारूपों में परिवर्तित करने की प्रक्रिया में आपका मार्गदर्शन करेंगे। हम प्रत्येक उदाहरण को अनेक चरणों में तोड़ेंगे और प्रत्येक चरण की व्याख्या करेंगे।

## आवश्यक शर्तें

इससे पहले कि हम .NET के लिए Aspose.HTML की दुनिया में उतरें, आपको यह सुनिश्चित कर लेना चाहिए कि आपके पास निम्नलिखित शर्तें मौजूद हैं:

1. विजुअल स्टूडियो: सुनिश्चित करें कि आपके सिस्टम पर विजुअल स्टूडियो स्थापित है। आप इसे वेबसाइट से डाउनलोड कर सकते हैं.

2.  .NET के लिए Aspose.HTML: आप Aspose वेबसाइट से लाइब्रेरी प्राप्त कर सकते हैं[यहाँ](https://releases.aspose.com/html/net/).

3. आपकी डेटा निर्देशिका: एक निर्देशिका तैयार करें जहां आप अपनी EPUB फ़ाइलें संग्रहीत करते हैं और जहां आउटपुट छवियां सहेजी जाएंगी।

4. C# का बुनियादी ज्ञान: इस ट्यूटोरियल में दिए गए कोड उदाहरणों को समझने और लागू करने के लिए C# प्रोग्रामिंग से परिचित होना आवश्यक है।

## आवश्यक नामस्थान आयात करना

इससे पहले कि हम .NET के लिए Aspose.HTML के साथ काम करना शुरू करें, आपको अपने C# कोड में आवश्यक नेमस्पेस आयात करना होगा। ये नामस्थान .NET सुविधाओं के लिए Aspose.HTML तक पहुंच प्रदान करते हैं।

```csharp
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using Aspose.Html.Rendering.Image;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
using System.IO;
using System.Drawing;
using System.Collections.Generic;
```

अब जबकि हमारे पास पूर्वापेक्षाएँ और नामस्थान मौजूद हैं, आइए चरण-दर-चरण उदाहरणों पर आगे बढ़ें।

## EPUB को JPEG में परिवर्तित करना

```csharp
    string dataDir = "Your Data Directory";
    // पढ़ने के लिए मौजूदा EPUB फ़ाइल खोलें।
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        // EPUB फ़ाइल को छवि में बदलने के लिए ConvertEPUB विधि को कॉल करें।
        Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), "output.jpg");
    }
```
### कदम

1. dataDir वैरिएबल में अपनी EPUB फ़ाइल का पथ प्रदान करें।
2. फ़ाइलस्ट्रीम का उपयोग करके पढ़ने के लिए EPUB फ़ाइल खोलें।
3. ConvertEPUB विधि को कॉल करें, EPUB स्ट्रीम को पास करते हुए, आउटपुट फॉर्मेट (JPEG) और आउटपुट फ़ाइल नाम ("आउटपुट.jpg") को निर्दिष्ट करने वाला एक ImageSaveOptions।
5. EPUB फ़ाइल को JPEG छवि में परिवर्तित किया जाता है।

इस उदाहरण में, हम एक EPUB फ़ाइल खोलते हैं, उसकी सामग्री पढ़ते हैं, और उसे JPEG छवि प्रारूप में परिवर्तित करते हैं। आउटपुट छवि "आउटपुट.jpg" के रूप में सहेजी गई है।

## EPUB को PNG में परिवर्तित करना

आप समान कोड संरचनाओं का उपयोग करके आसानी से EPUB फ़ाइलों को PNG, BMP, GIF और TIFF जैसे विभिन्न छवि प्रारूपों में परिवर्तित कर सकते हैं। यहां पीएनजी में कनवर्ट करने का एक उदाहरण दिया गया है:

```csharp

    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Png);
        Converter.ConvertEPUB(stream, options, "output.png");
    }

```
### कदम
1. फ़ाइलस्ट्रीम का उपयोग करके पढ़ने के लिए EPUB फ़ाइल खोलें।
2. वांछित आउटपुट प्रारूप (इस मामले में, पीएनजी) के साथ एक ImageSaveOptions ऑब्जेक्ट को प्रारंभ करें।
3. EPUB स्ट्रीम, इमेज सेव विकल्प और आउटपुट फ़ाइल नाम को पास करते हुए ConvertEPUB विधि को कॉल करें।
4. EPUB फ़ाइल को निर्दिष्ट छवि प्रारूप में परिवर्तित किया जाता है।

## छवि सहेजें विकल्प निर्दिष्ट करें

आप पृष्ठ आकार और पृष्ठभूमि रंग जैसे विकल्पों को निर्दिष्ट करके छवि आउटपुट को अनुकूलित कर सकते हैं। यहाँ एक उदाहरण है:

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Jpeg)
        {
            PageSetup =
            {
                AnyPage = new Page()
                {
                    Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
                }
            },
            BackgroundColor = Color.AliceBlue,
        };
        Converter.ConvertEPUB(stream, options, "output.jpg");
    }
```
### कदम

1.  अपनी EPUB फ़ाइल का पथ प्रदान करें`dataDir` चर।
2.  का उपयोग करके पढ़ने के लिए EPUB फ़ाइल खोलें`FileStream`.
3.  एक बनाएं`ImageSaveOptions` ऑब्जेक्ट बनाएं और वांछित आउटपुट स्वरूप (जेपीईजी) निर्दिष्ट करें।
4. यदि आवश्यक हो तो पृष्ठ का आकार और पृष्ठभूमि का रंग अनुकूलित करें।
5.  बुलाएं`ConvertEPUB`विधि, EPUB स्ट्रीम पास करना, छवि सहेजने के विकल्प और आउटपुट फ़ाइल नाम।
6. EPUB फ़ाइल निर्दिष्ट विकल्पों के साथ एक छवि में परिवर्तित हो जाती है।

## एक कस्टम स्ट्रीम प्रदाता निर्दिष्ट करें

यदि आपको आउटपुट स्ट्रीम में हेरफेर करने की आवश्यकता है, तो आप एक कस्टम स्ट्रीम प्रदाता का उपयोग कर सकते हैं। यहाँ एक उदाहरण है:

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        using (var streamProvider = new MemoryStreamProvider())
        {
            Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), streamProvider);
            
            for (int i = 0; i < streamProvider.Streams.Count; i++)
            {
                var memory = streamProvider.Streams[i];
                memory.Seek(0, SeekOrigin.Begin);
                
                using (FileStream fs = File.Create($"page_{i + 1}.jpg"))
                {
                    memory.CopyTo(fs);
                }
            }
        }
    }

```
मेमोरीस्ट्रीमप्रोवाइडर क्लास सोर्स कोड।

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

### कदम
1.  अपनी EPUB फ़ाइल का पथ प्रदान करें`dataDir` चर।
2.  का उपयोग करके पढ़ने के लिए EPUB फ़ाइल खोलें`FileStream`.
3.  एक बनाने के`MemoryStreamProvider` कस्टम आउटपुट स्ट्रीम को संभालने के लिए।
4.  बुलाएं`ConvertEPUB` विधि, EPUB स्ट्रीम, इमेज सेव विकल्प (JPEG), और कस्टम स्ट्रीम प्रदाता को पास करना।
5. कस्टम प्रदाता में मेमोरी स्ट्रीम के माध्यम से पुनरावृति करें, उन्हें अलग-अलग फ़ाइलों में सहेजें।
6. यह उदाहरण आपको आवश्यकतानुसार एकाधिक आउटपुट स्ट्रीम में हेरफेर करने और सहेजने की अनुमति देता है।

## निष्कर्ष

.NET के लिए Aspose.HTML एक बहुमुखी लाइब्रेरी है जो EPUB और HTML दस्तावेज़ों के साथ काम करना सरल बनाती है। EPUB दस्तावेज़ों को विभिन्न छवि प्रारूपों और अनुकूलन योग्य विकल्पों में परिवर्तित करने की क्षमता के साथ, यह डेवलपर्स के लिए अनुप्रयोगों की एक विस्तृत श्रृंखला प्रदान करता है।

---

## अक्सर पूछे जाने वाले प्रश्नों

### 1. मैं .NET के लिए Aspose.HTML कहां से डाउनलोड कर सकता हूं?

 आप रिलीज़ पेज से .NET के लिए Aspose.HTML डाउनलोड कर सकते हैं[यहाँ](https://releases.aspose.com/html/net/).

### 2. मैं .NET के लिए Aspose.HTML के लिए अस्थायी लाइसेंस कैसे प्राप्त कर सकता हूं?

 अस्थायी लाइसेंस प्राप्त करने के लिए, अस्थायी लाइसेंस पृष्ठ पर जाएँ[यहाँ](https://purchase.aspose.com/temporary-license/).

### 3. मुझे .NET के लिए Aspose.HTML के लिए अतिरिक्त समर्थन कहां मिल सकता है?

 किसी भी प्रश्न या समस्या के लिए, आप सहायता मंच पर एस्पोज़ समुदाय से सहायता मांग सकते हैं[यहाँ](https://forum.aspose.com/).

### 4. क्या मैं ईपीयूबी दस्तावेजों को पीडीएफ या एक्सपीएस जैसे अन्य प्रारूपों में परिवर्तित कर सकता हूं?

हां, आप EPUB दस्तावेज़ों को पीडीएफ और एक्सपीएस सहित विभिन्न प्रारूपों में परिवर्तित करने के लिए .NET के लिए Aspose.HTML का उपयोग कर सकते हैं।

### 5. क्या .NET के लिए Aspose.HTML छोटे और बड़े पैमाने की दोनों परियोजनाओं के लिए उपयुक्त है?

बिल्कुल! .NET के लिए Aspose.HTML को स्केलेबल बनाने के लिए डिज़ाइन किया गया है, जो इसे सभी आकारों की परियोजनाओं के लिए एक बढ़िया विकल्प बनाता है।

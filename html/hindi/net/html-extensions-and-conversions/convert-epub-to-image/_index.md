---
title: Aspose.HTML के साथ .NET में EPUB को छवि में बदलें
linktitle: .NET में EPUB को इमेज में बदलें
second_title: Aspose.HTML .NET HTML हेरफेर एपीआई
description: .NET के लिए Aspose.HTML का उपयोग करके EPUB को छवियों में परिवर्तित करना सीखें। कोड उदाहरणों और अनुकूलन योग्य विकल्पों के साथ चरण-दर-चरण ट्यूटोरियल।
weight: 11
url: /hi/net/html-extensions-and-conversions/convert-epub-to-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML के साथ .NET में EPUB को छवि में बदलें


आज के डिजिटल युग में, विभिन्न दस्तावेज़ प्रारूपों में हेरफेर करने और उन्हें परिवर्तित करने की क्षमता एक मूल्यवान कौशल है। .NET के लिए Aspose.HTML एक शक्तिशाली उपकरण है जो डेवलपर्स को HTML और EPUB दस्तावेज़ों के साथ आसानी से काम करने की अनुमति देता है। इस ट्यूटोरियल में, हम .NET के लिए Aspose.HTML की दुनिया में उतरेंगे और आपको EPUB दस्तावेज़ों को विभिन्न छवि प्रारूपों में परिवर्तित करने की प्रक्रिया के माध्यम से मार्गदर्शन करेंगे। हम प्रत्येक उदाहरण को कई चरणों में विभाजित करेंगे, और हर चरण को समझाएंगे।

## आवश्यक शर्तें

इससे पहले कि हम .NET के लिए Aspose.HTML की दुनिया में गोता लगाएँ, आपको यह सुनिश्चित करना चाहिए कि आपके पास निम्नलिखित पूर्वापेक्षाएँ मौजूद हैं:

1. विज़ुअल स्टूडियो: सुनिश्चित करें कि आपके सिस्टम पर विज़ुअल स्टूडियो इंस्टॉल है। आप इसे वेबसाइट से डाउनलोड कर सकते हैं।

2.  .NET के लिए Aspose.HTML: आप Aspose वेबसाइट से लाइब्रेरी प्राप्त कर सकते हैं[यहाँ](https://releases.aspose.com/html/net/).

3. आपकी डेटा निर्देशिका: एक निर्देशिका तैयार करें जहां आप अपनी EPUB फ़ाइलें संग्रहीत करते हैं और जहां आउटपुट छवियां सहेजी जाएंगी।

4. C# का मूलभूत ज्ञान: इस ट्यूटोरियल में दिए गए कोड उदाहरणों को समझने और कार्यान्वित करने के लिए C# प्रोग्रामिंग से परिचित होना आवश्यक है।

## आवश्यक नामस्थान आयात करना

इससे पहले कि हम .NET के लिए Aspose.HTML के साथ काम करना शुरू करें, आपको अपने C# कोड में आवश्यक नेमस्पेस आयात करने की आवश्यकता है। ये नेमस्पेस .NET के लिए Aspose.HTML सुविधाओं तक पहुँच प्रदान करते हैं।

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

अब जब हमारे पास पूर्वापेक्षाएँ और नामस्थान मौजूद हैं, तो चलिए चरण-दर-चरण उदाहरणों पर चलते हैं।

## EPUB को JPEG में परिवर्तित करना

```csharp
    string dataDir = "Your Data Directory";
    // पढ़ने के लिए मौजूदा EPUB फ़ाइल खोलें.
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        // EPUB फ़ाइल को छवि में परिवर्तित करने के लिए ConvertEPUB विधि को कॉल करें।
        Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), "output.jpg");
    }
```
### कदम

1. dataDir वेरिएबल में अपनी EPUB फ़ाइल का पथ प्रदान करें.
2. फ़ाइलस्ट्रीम का उपयोग करके पढ़ने के लिए EPUB फ़ाइल खोलें।
3. EPUB स्ट्रीम, आउटपुट प्रारूप (JPEG) निर्दिष्ट करने वाला ImageSaveOptions, तथा आउटपुट फ़ाइल नाम ("output.jpg") पास करते हुए ConvertEPUB विधि को कॉल करें।
5. EPUB फ़ाइल को JPEG छवि में परिवर्तित कर दिया जाता है।

इस उदाहरण में, हम एक EPUB फ़ाइल खोलते हैं, उसकी सामग्री पढ़ते हैं, और उसे JPEG छवि प्रारूप में परिवर्तित करते हैं। आउटपुट छवि "output.jpg" के रूप में सहेजी जाती है।

## EPUB को PNG में परिवर्तित करना

आप समान कोड संरचनाओं का उपयोग करके EPUB फ़ाइलों को PNG, BMP, GIF और TIFF जैसे विभिन्न छवि प्रारूपों में आसानी से परिवर्तित कर सकते हैं। PNG में परिवर्तित करने के लिए यहाँ एक उदाहरण दिया गया है:

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
2. वांछित आउटपुट प्रारूप (इस मामले में, PNG) के साथ ImageSaveOptions ऑब्जेक्ट को आरंभ करें।
3. EPUB स्ट्रीम, छवि सहेजने के विकल्प, और आउटपुट फ़ाइल नाम पास करते हुए ConvertEPUB विधि को कॉल करें।
4. EPUB फ़ाइल को निर्दिष्ट छवि प्रारूप में परिवर्तित किया जाता है।

## छवि सहेजने के विकल्प निर्दिष्ट करें

आप पेज आकार और पृष्ठभूमि रंग जैसे विकल्प निर्दिष्ट करके छवि आउटपुट को कस्टमाइज़ कर सकते हैं। यहाँ एक उदाहरण दिया गया है:

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
2.  पढ़ने के लिए EPUB फ़ाइल खोलें`FileStream`.
3.  एक बनाएं`ImageSaveOptions` ऑब्जेक्ट चुनें और वांछित आउटपुट प्रारूप (JPEG) निर्दिष्ट करें।
4. यदि आवश्यक हो तो पृष्ठ का आकार और पृष्ठभूमि का रंग अनुकूलित करें।
5.  कॉल करें`ConvertEPUB`विधि, EPUB स्ट्रीम, छवि सहेजने के विकल्प, और आउटपुट फ़ाइल नाम को पास करना।
6. EPUB फ़ाइल को निर्दिष्ट विकल्पों के साथ छवि में परिवर्तित किया जाता है।

## कस्टम स्ट्रीम प्रदाता निर्दिष्ट करें

यदि आपको आउटपुट स्ट्रीम में बदलाव करने की आवश्यकता है, तो आप कस्टम स्ट्रीम प्रदाता का उपयोग कर सकते हैं। यहाँ एक उदाहरण दिया गया है:

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
मेमोरीस्ट्रीमप्रदाता क्लास स्रोत कोड.

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

### कदम
1.  अपनी EPUB फ़ाइल का पथ प्रदान करें`dataDir` चर।
2.  पढ़ने के लिए EPUB फ़ाइल खोलें`FileStream`.
3.  एक बनाने के`MemoryStreamProvider` कस्टम आउटपुट स्ट्रीम को संभालने के लिए.
4.  कॉल करें`ConvertEPUB` विधि, EPUB स्ट्रीम, छवि सहेजें विकल्प (JPEG), और कस्टम स्ट्रीम प्रदाता को पास करना।
5. कस्टम प्रदाता में मेमोरी स्ट्रीम के माध्यम से पुनरावृति करें, उन्हें अलग-अलग फ़ाइलों में सहेजें।
6. यह उदाहरण आपको आवश्यकतानुसार एकाधिक आउटपुट स्ट्रीमों में परिवर्तन करने और उन्हें सहेजने की अनुमति देता है।

## निष्कर्ष

Aspose.HTML for .NET एक बहुमुखी लाइब्रेरी है जो EPUB और HTML दस्तावेज़ों के साथ काम करना आसान बनाती है। EPUB दस्तावेज़ों को विभिन्न छवि प्रारूपों और अनुकूलन योग्य विकल्पों में बदलने की क्षमता के साथ, यह डेवलपर्स के लिए अनुप्रयोगों की एक विस्तृत श्रृंखला प्रदान करता है।

---

## अक्सर पूछे जाने वाले प्रश्नों

### 1. मैं .NET के लिए Aspose.HTML कहां से डाउनलोड कर सकता हूं?

 आप रिलीज़ पेज से .NET के लिए Aspose.HTML डाउनलोड कर सकते हैं[यहाँ](https://releases.aspose.com/html/net/).

### 2. मैं .NET के लिए Aspose.HTML हेतु अस्थायी लाइसेंस कैसे प्राप्त कर सकता हूं?

 अस्थायी लाइसेंस प्राप्त करने के लिए, अस्थायी लाइसेंस पृष्ठ पर जाएँ[यहाँ](https://purchase.aspose.com/temporary-license/).

### 3. मुझे .NET के लिए Aspose.HTML हेतु अतिरिक्त समर्थन कहां मिल सकता है?

 किसी भी प्रश्न या समस्या के लिए, आप सहायता फ़ोरम पर Aspose समुदाय से सहायता ले सकते हैं[यहाँ](https://forum.aspose.com/).

### 4. क्या मैं EPUB दस्तावेज़ों को PDF या XPS जैसे अन्य प्रारूपों में परिवर्तित कर सकता हूँ?

हां, आप EPUB दस्तावेजों को PDF और XPS सहित विभिन्न प्रारूपों में परिवर्तित करने के लिए Aspose.HTML for .NET का उपयोग कर सकते हैं।

### 5. क्या Aspose.HTML for .NET छोटे और बड़े पैमाने की परियोजनाओं दोनों के लिए उपयुक्त है?

बिल्कुल! .NET के लिए Aspose.HTML को स्केलेबल बनाया गया है, जो इसे सभी आकारों की परियोजनाओं के लिए एक बढ़िया विकल्प बनाता है।

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

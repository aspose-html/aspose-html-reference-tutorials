---
category: general
date: 2026-04-06
description: C# में एंटीएलियासिंग को सक्षम करना, इमेज की चौड़ाई और ऊँचाई सेट करना,
  और दस्तावेज़ को PNG के रूप में सहेजना सीखें – दस्तावेज़ को इमेज में निर्यात करने
  के लिए एक त्वरित गाइड।
draft: false
keywords:
- how to enable antialiasing
- save document as png
- set image width
- set image height
- export document to image
language: hi
og_description: जब आप किसी दस्तावेज़ को छवि के रूप में निर्यात करते हैं तो एंटी‑एलियासिंग
  कैसे सक्षम करें। यह गाइड आपको दिखाता है कि छवि की चौड़ाई कैसे सेट करें, छवि की ऊँचाई
  कैसे सेट करें, और दस्तावेज़ को PNG के रूप में कैसे सहेजें।
og_title: एंटीएलियासिंग को कैसे सक्षम करें – दस्तावेज़ को इमेज में निर्यात करें
tags:
- C#
- ImageRendering
- Antialiasing
title: एंटीएलियासिंग कैसे सक्षम करें – C# के साथ दस्तावेज़ को इमेज में निर्यात करें
url: /hi/net/generate-jpg-and-png-images/how-to-enable-antialiasing-export-document-to-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# एंटीएलियासिंग को कैसे सक्षम करें – C# में दस्तावेज़ को इमेज में निर्यात करें

क्या आपने कभी सोचा है **एंटीएलियासिंग को कैसे सक्षम करें** जब आप एक दस्तावेज़ को चित्र में बदल रहे हों? शायद आपने एक त्वरित `Save` कॉल आज़माई और परिणाम खुरदुरा दिखा, विशेष रूप से तिरछी लाइनों पर। अच्छी खबर यह है कि आपको ग्राफ़िक्स जादूगर की जरूरत नहीं है—सिर्फ कुछ पंक्तियों का C# कोड और सही विकल्पों की आवश्यकता है।

इस ट्यूटोरियल में हम इमेज की चौड़ाई सेट करने, इमेज की ऊँचाई सेट करने, और अंत में **save document as PNG** करने की प्रक्रिया को देखेंगे ताकि आप **export document to image** कर सकें स्मूथ किनारों के साथ। अंत तक आपके पास एक तैयार‑चलाने‑योग्य स्निपेट होगा जो एंटीएलियासिंग चालू होने पर एक स्पष्ट 800 × 600 PNG उत्पन्न करता है।

## पूर्वापेक्षाएँ

- .NET 6.0 या बाद का संस्करण (कोड .NET Framework 4.7+ पर भी काम करता है)  
- एक रेंडरिंग लाइब्रेरी का रेफ़रेंस जो `ImageRenderingOptions` को सपोर्ट करती है (जैसे, Aspose.Words, Syncfusion, या कोई भी API जो समान प्रॉपर्टीज़ प्रदान करता है)  
- C# सिंटैक्स की बुनियादी समझ  

कोई भारी सेटअप नहीं—सिर्फ NuGet पैकेज जोड़ें और आप तैयार हैं।

## चरण 1: रेंडरिंग लाइब्रेरी स्थापित करें

सबसे पहले, पैकेज को अपने प्रोजेक्ट में जोड़ें। यदि आप Aspose.Words का उपयोग कर रहे हैं, तो चलाएँ:

```bash
dotnet add package Aspose.Words
```

> **Pro tip:** लाइब्रेरी का संस्करण अद्यतित रखें; नवीनतम रिलीज़ (अप्रैल 2026 तक) एंटीएलियासिंग के लिए प्रदर्शन सुधार जोड़ता है।

## चरण 2: Document ऑब्जेक्ट बनाएं

उस दस्तावेज़ को लोड या बनाएं जिसे आप रेंडर करना चाहते हैं। यहाँ एक न्यूनतम उदाहरण है जो एक पृष्ठ का दस्तावेज़ एक साधारण पैराग्राफ के साथ बनाता है:

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Create a new blank document
Document doc = new Document();

// Add a paragraph with some text
Paragraph para = new Paragraph(doc);
Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
para.AppendChild(run);
doc.FirstSection.Body.AppendChild(para);
```

`Document` क्लास प्रवेश बिंदु है; आप जो कुछ भी रेंडर करते हैं वह इससे आता है। वास्तविक प्रोजेक्ट्स में आप संभवतः एक मौजूदा .docx लोड करेंगे:

```csharp
// Document doc = new Document("input.docx");
```

## चरण 3: रेंडरिंग विकल्प निर्धारित करें (चौड़ाई, ऊँचाई, एंटीएलियासिंग)

अब हम मुख्य प्रश्न का उत्तर देते हैं: **how to enable antialiasing**। `ImageRenderingOptions` ऑब्जेक्ट आपको स्मूथिंग टॉगल करने और आयाम नियंत्रित करने की सुविधा देता है।

```csharp
// Step 3: Define rendering options (size and antialiasing)
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Set the desired output size
    Width = 800,               // set image width
    Height = 600,              // set image height

    // Turn on antialiasing for smoother edges
    UseAntialiasing = true
};
```

टिप्पणियों पर ध्यान दें: वे स्पष्ट रूप से **set image width**, **set image height**, और **UseAntialiasing** का उल्लेख करती हैं—तीन नियंत्रण जो एक पॉलिश्ड PNG चाहते समय सबसे अधिक महत्वपूर्ण होते हैं।

### एंटीएलियासिंग क्यों महत्वपूर्ण है

एंटीएलियासिंग के बिना, तिरछी रेखाएँ और वक्र सीढ़ी‑जैसे दिखते हैं क्योंकि रेंडरर प्रत्येक पिक्सेल को या तो ऑन या ऑफ मानता है। इसे सक्षम करने से किनारे के पिक्सेल मिश्रित हो जाते हैं, जिससे एक दृश्य नरमी उत्पन्न होती है जो फोटो एडिटर में देखी जाने वाली प्रभाव की नकल करती है। इसका नुकसान यह है कि प्रोसेसिंग समय में थोड़ा वृद्धि होती है, लेकिन अधिकांश UI‑उन्मुख निर्यातों के लिए यह नगण्य है।

## चरण 4: दस्तावेज़ को PNG के रूप में सहेजें (Export Document to Image)

विकल्प तैयार होने के बाद, हम अंत में **save document as PNG** करते हैं। `Save` मेथड फ़ाइल पाथ और हमने अभी कॉन्फ़िगर किए गए विकल्प लेता है।

```csharp
// Step 4: Render the document to a PNG file using the configured options
doc.Save("output.png", imageOptions);
```

बस इतना ही—आपका दस्तावेज़ अब एंटीएलियासिंग लागू किए हुए 800 × 600 PNG है। यदि आप `output.png` खोलते हैं तो आपको साफ़ टेक्स्ट, स्मूथ लाइन्स, और कोई खुरदुरा आर्टिफैक्ट नहीं दिखेगा।

### परिणाम की पुष्टि

आप किसी भी इमेज व्यूअर में फ़ाइल को जल्दी से जांच सकते हैं। देखें:

- सही आयाम (800 × 600)  
- टेक्स्ट या किसी भी आकार पर कोई दिखाई देने वाला सीढ़ी‑जैसा किनारा नहीं  
- यदि आपके दस्तावेज़ में बैकग्राउंड रंग नहीं है तो पारदर्शी पृष्ठभूमि (अधिकांश लाइब्रेरी डिफ़ॉल्ट रूप से सफ़ेद होती हैं)

यदि इमेज खुरदुरा दिखता है, तो दोबारा जाँचें कि `UseAntialiasing = true` कहीं और ओवरराइड नहीं हो रहा है।

## चरण 5: किनारे के मामलों और विविधताएँ

### आउटपुट फ़ॉर्मेट बदलना

क्या आप PNG के बजाय JPEG चाहते हैं? बस फ़ाइल एक्सटेंशन बदलें और वैकल्पिक रूप से संपीड़न को समायोजित करें:

```csharp
imageOptions.JpegQuality = 90; // only works for JPEG output
doc.Save("output.jpg", imageOptions);
```

### एकाधिक पृष्ठों का निर्यात

जब स्रोत दस्तावेज़ में कई पृष्ठ होते हैं, तो रेंडरर डिफ़ॉल्ट रूप से प्रत्येक पृष्ठ के लिए अलग इमेज फ़ाइल बनाता है। आप पृष्ठों के माध्यम से लूप कर सकते हैं:

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string fileName = $"page_{i + 1}.png";
    doc.Save(fileName, imageOptions);
}
```

### स्ट्रीम में सहेजना (जैसे, HTTP प्रतिक्रिया)

यदि आप एक वेब API बना रहे हैं, तो आप PNG को सीधे रिटर्न करना चाह सकते हैं:

```csharp
using (MemoryStream ms = new MemoryStream())
{
    doc.Save(ms, imageOptions);
    ms.Position = 0;
    // Return ms as FileResult in ASP.NET Core
}
```

## पूरा कार्यशील उदाहरण

नीचे वह पूर्ण, कॉपी‑पेस्ट‑तैयार प्रोग्राम है जो चर्चा किए गए सभी चरणों को सम्मिलित करता है:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;

class Program
{
    static void Main()
    {
        // 1️⃣ Create or load a document
        Document doc = new Document();
        Paragraph para = new Paragraph(doc);
        Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
        para.AppendChild(run);
        doc.FirstSection.Body.AppendChild(para);

        // 2️⃣ Define rendering options (size and antialiasing)
        ImageRenderingOptions imageOptions = new ImageRenderingOptions
        {
            Width = 800,               // set image width
            Height = 600,              // set image height
            UseAntialiasing = true     // how to enable antialiasing
        };

        // 3️⃣ Export document to image (save document as PNG)
        doc.Save("output.png", imageOptions);

        Console.WriteLine("Image saved as output.png with antialiasing enabled.");
    }
}
```

इस प्रोग्राम को चलाने से `output.png` निष्पादन योग्य फ़ोल्डर में बनता है। इसे खोलें, और आपको एक स्मूथ, 800 × 600 PNG दिखाई देगा—वही जो हमने हासिल करने के लिए निर्धारित किया था।

## आम प्रश्न और समस्या निवारण

- **यदि इमेज धुंधली दिखती है तो क्या करें?**  
  धुंधलापन तब हो सकता है जब आप छोटे स्रोत पृष्ठ को अपस्केल करते हैं। स्रोत पृष्ठ का आकार लक्ष्य आयामों के करीब रखें, या DPI को `imageOptions.Resolution` के माध्यम से बढ़ाएँ (उदाहरण के लिए, `Resolution = 300`)।

- **क्या यह .NET Framework पर काम करता है?**  
  हां। वही API क्लासिक फ्रेमवर्क में भी मौजूद है; बस उपयुक्त DLL को रेफ़रेंस करें।

- **क्या मैं बैकग्राउंड रंग नियंत्रित कर सकता हूँ?**  
  बिल्कुल। सहेजने से पहले `imageOptions.BackgroundColor = System.Drawing.Color.Transparent;` सेट करें।

- **क्या एंटीएलियासिंग हार्डवेयर‑त्वरित है?**  
  अधिकांश लाइब्रेरी सॉफ़्टवेयर एंटीएलियासिंग करती हैं। यदि आपको GPU त्वरण चाहिए, तो ऐसे रेंडरिंग इंजन की तलाश करें जो स्पष्ट रूप से इसे सपोर्ट करता हो।

## निष्कर्ष

हमने **how to enable antialiasing** को कवर किया है जब आप **export document to image** करते हैं, **set image width** और **set image height** की प्रक्रिया देखी है, और आपको **save document as PNG** के सटीक चरण दिखाए हैं। ऊपर दिया गया स्निपेट उत्पादन के लिए तैयार है, और अब आप इसे JPEG, मल्टी‑पेज PDFs, या यहाँ तक कि इमेज को सीधे क्लाइंट को स्ट्रीम करने के लिए अनुकूलित कर सकते हैं।

अगले चरण में आप वॉटरमार्क जोड़ने, प्रिंट‑क्वालिटी आउटपुट के लिए DPI समायोजित करने, या इस लॉजिक को ASP.NET Core एंडपॉइंट में एकीकृत करने का अन्वेषण कर सकते हैं। वही सिद्धांत लागू होते हैं—फ़ाइल पाथ को प्रतिक्रिया स्ट्रीम से बदल दें।

कोडिंग का आनंद लें, और उन स्पष्ट, एंटीएलियास्ड इमेजेज़ का मज़ा लें! 

![Rendered PNG with antialiasing enabled](output.png "Rendered PNG with antialiasing enabled")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
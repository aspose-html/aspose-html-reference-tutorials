---
category: general
date: 2025-12-29
description: C# में HTML दस्तावेज़ बनाएं और फ़ॉन्ट फ़ैमिली, फ़ॉन्ट आकार सेट करना सीखें,
  फिर Aspose.HTML का उपयोग करके HTML को PDF के रूप में सहेजें या HTML को PDF में परिवर्तित
  करें।
draft: false
keywords:
- create html document
- set font family
- set font size
- save html as pdf
- convert html to pdf
language: hi
og_description: C# में HTML दस्तावेज़ बनाएं और तुरंत देखें कि फ़ॉन्ट फ़ैमिली और फ़ॉन्ट
  आकार कैसे सेट करें, फिर HTML को PDF के रूप में सहेजें या Aspose.HTML के साथ HTML
  को PDF में परिवर्तित करें।
og_title: HTML दस्तावेज़ बनाएं – स्टाइल किया गया टेक्स्ट और PDF निर्यात
tags:
- aspnet
- csharp
- pdf-generation
title: स्टाइल किए गए टेक्स्ट के साथ HTML दस्तावेज़ बनाएं और PDF में निर्यात करें –
  पूर्ण गाइड
url: /hi/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# स्टाइल्ड टेक्स्ट के साथ HTML दस्तावेज़ बनाएं और PDF में निर्यात करें

क्या आपको कभी **create HTML document** तुरंत बनाकर उसे PDF में बदलने की ज़रूरत पड़ी है बिना अपने C# कोड से बाहर निकले? शायद आप एक रिपोर्टिंग इंजन, एक इनवॉइस जेनरेटर बना रहे हैं, या उपयोगकर्ताओं के लिए सिर्फ एक त्वरित‑देख पूर्वावलोकन बना रहे हैं। अच्छी खबर यह है कि आप इसे कुछ ही लाइनों में Aspose.HTML का उपयोग करके कर सकते हैं, और आपको फ़ॉन्ट फ़ैमिली, फ़ॉन्ट साइज, और यहाँ तक कि बोल्ड‑इटैलिक स्टाइलिंग पर पूरी नियंत्रण मिलेगा।

इस ट्यूटोरियल में हम पूरी प्रक्रिया को समझेंगे—इन‑मेमोरी HTML दस्तावेज़ को बनाकर उसे PDF फ़ाइल के रूप में सहेजने तक। अंत तक आप बिल्कुल जान जाएंगे कि **set font family**, **set font size**, और **save HTML as PDF** (जिसे **convert HTML to PDF** भी कहा जाता है) कैसे किया जाता है, एक साफ़, प्रोडक्शन‑रेडी कोड सैंपल के साथ।

## आपको क्या चाहिए

- .NET 6+ (API .NET Core और .NET Framework दोनों के साथ काम करता है)  
- Aspose.HTML for .NET NuGet पैकेज (`Aspose.Html`) – `dotnet add package Aspose.Html` के माध्यम से इंस्टॉल करें  
- डिस्क पर एक फ़ोल्डर जहाँ जेनरेट किया गया PDF लिखा जा सके  

![create html document illustration](/images/create-html-document.png){alt="create html document example"}

## चरण 1: HTML दस्तावेज़ बनाएं

सबसे पहले, हमें एक खाली HTML दस्तावेज़ ऑब्जेक्ट चाहिए। इसे एक नई कैनवास की तरह समझें जहाँ आप बाद में अपना स्टाइल्ड पैराग्राफ पेंट करेंगे।

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

// Step 1 – initialize a new HTML document in memory
HTMLDocument htmlDocument = new HTMLDocument();

// Grab a reference to the <body> element for later use
HTMLBodyElement body = htmlDocument.Body;
```

**Why this matters:** `HTMLDocument` आपको एक DOM‑जैसी संरचना देता है जिसे आप प्रोग्रामेटिकली मैनिपुलेट कर सकते हैं। अंत तक रॉ स्ट्रिंग्स या फ़ाइल I/O को छूने की ज़रूरत नहीं है।

## चरण 2: एक पैराग्राफ जोड़ें और फ़ॉन्ट फ़ैमिली एवं फ़ॉन्ट साइज सेट करें

अब हम एक `<p>` एलिमेंट बनाएंगे, कुछ टेक्स्ट डालेंगे, और स्पष्ट रूप से फ़ॉन्ट फ़ैमिली और साइज को परिभाषित करेंगे। यहाँ **set font family** और **set font size** कीवर्ड्स काम आते हैं।

```csharp
// Step 2 – create a <p> element with some sample text
HtmlElement paragraph = htmlDocument.CreateElement("p");
paragraph.InnerHtml = "Bold & Italic text";

// Define the base font style
paragraph.Style.FontFamily = "Arial";   // set font family
paragraph.Style.FontSize = "18px";      // set font size

// Attach the paragraph to the document body
body.AppendChild(paragraph);
```

**Pro tip:** यदि आपको वेब‑सेफ़ फॉलबैक चाहिए, तो आप कॉमा‑सेपरेटेड लिस्ट जैसे `"Arial, Helvetica, sans-serif"` दे सकते हैं; ब्राउज़र (या Aspose) पहला उपलब्ध फ़ॉन्ट चुन लेगा।

## चरण 3: WebFontStyle फ़्लैग्स के साथ बोल्ड और इटैलिक स्टाइल लागू करें

Aspose.HTML एक उपयोगी enum `WebFontStyle` प्रदान करता है जो आपको स्टाइल्स को बिटवाइज़ OR के साथ मिलाने देता है। चलिए टेक्स्ट को दोनों बोल्ड **और** इटैलिक बनाते हैं।

```csharp
// Step 3 – apply bold and italic using WebFontStyle flags
paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

**What’s happening under the hood?** `FontStyle` प्रॉपर्टी CSS `font-weight` और `font-style` डिक्लेरेशन्स में बदलती है। फ़्लैग्स को OR‑करने से हम दो अलग-अलग CSS लाइनों को लिखने से बचते हैं।

## चरण 4: HTML को PDF में बदलें (Save HTML as PDF)

अंतिम चरण वास्तविक रूपांतरण है। `Save` को एक बार कॉल करने से, Aspose.HTML DOM को रेंडर करता है और डिस्क पर एक PDF फ़ाइल लिखता है। यह **save html as pdf** और **convert html to pdf** दोनों आवश्यकताओं को पूरा करता है।

```csharp
// Step 4 – save the HTML document as a PDF file
string outputPath = @"C:\Temp\styled.pdf";
htmlDocument.Save(outputPath, new PDFSaveOptions());

// Optional: open the PDF automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Expected result:** `styled.pdf` खोलें और आपको एक पैराग्राफ दिखेगा जिसमें “Bold & Italic text” 18‑px Arial में, बोल्ड और इटैलिक रेंडर किया हुआ होगा। PDF का आकार मानक A4 पेज से मेल खाता है, और टेक्स्ट सिलेक्टेबल है—वेक्टर रेंडरिंग की वजह से।

## पूर्ण कार्यशील उदाहरण

सब कुछ मिलाकर, यहाँ पूरा, चलाने के लिए तैयार प्रोग्राम है:

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new HTML document
        HTMLDocument htmlDocument = new HTMLDocument();
        HTMLBodyElement body = htmlDocument.Body;

        // 2️⃣ Add a styled paragraph
        HtmlElement paragraph = htmlDocument.CreateElement("p");
        paragraph.InnerHtml = "Bold & Italic text";

        // Set font family and size
        paragraph.Style.FontFamily = "Arial";
        paragraph.Style.FontSize = "18px";

        // 3️⃣ Apply bold + italic
        paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // Append to body
        body.AppendChild(paragraph);

        // 4️⃣ Save as PDF (convert HTML to PDF)
        string outputFile = @"C:\Temp\styled.pdf";
        htmlDocument.Save(outputFile, new PDFSaveOptions());

        Console.WriteLine($"PDF generated at: {outputFile}");
    }
}
```

### कोड चलाना

1. Aspose.HTML NuGet पैकेज इंस्टॉल करें:  
   ```bash
   dotnet add package Aspose.Html
   ```
2. `C:\Temp\styled.pdf` को उस फ़ोल्डर से बदलें जहाँ आपके पास लिखने की अनुमति है।  
3. बिल्ड और रन करें: `dotnet run`।  

आपको कंसोल में फ़ाइल लोकेशन की पुष्टि करने वाला संदेश दिखेगा, और PDF में स्टाइल्ड पैराग्राफ होगा।

## सामान्य प्रश्न और किनारे के मामलों

- **What if I need a custom web font?**  
  पैराग्राफ बनाने से पहले `HTMLFontFaceRule` के साथ फ़ॉन्ट लोड करें या रिमोट `@font-face` CSS फ़ाइल का रेफ़रेंस दें।

- **Can I add images before converting?**  
  बिल्कुल। `HTMLImageElement img = (HTMLImageElement)htmlDocument.CreateElement("img");` का उपयोग करें और `img.Source` को स्थानीय पाथ या डेटा URI पर सेट करें।

- **What about multi‑page PDFs?**  
  अधिक एलिमेंट्स (टेबल्स, डिव्स, आदि) जोड़ें और जब कंटेंट पेज की ऊँचाई से अधिक हो जाएगा तो Aspose.HTML स्वचालित रूप से पेजिनेट करेगा।

- **Is there a way to control PDF metadata?**  
  एक `PdfSaveOptions` इंस्टेंस पास करें और `Author`, `Title`, या `PdfAConformanceLevel` जैसी प्रॉपर्टीज़ सेट करें।

## पुनरावलोकन

हमने बताया कि C# में **create HTML document** कैसे किया जाता है, **set font family**, **set font size**, बोल्ड‑इटैलिक स्टाइल कैसे लागू किए जाते हैं, और अंत में **save HTML as PDF**—अर्थात **convert HTML to PDF** Aspose.HTML के साथ। यह स्निपेट इतना छोटा है कि किसी भी .NET प्रोजेक्ट में डाला जा सके, फिर भी इतना पूरा है कि अधिक जटिल रिपोर्टिंग परिदृश्यों के लिए एक ठोस आधार बन सके।

## अगले कदम

- CSS क्लासेज़ के साथ प्रयोग करें ताकि स्टाइलिंग पुन: उपयोगी हो सके।  
- एकाधिक पैराग्राफ, टेबल्स, और इमेज़ को मिलाकर अधिक समृद्ध PDFs बनाएं।  
- यदि आपको अभिलेखीय‑ग्रेड दस्तावेज़ चाहिए तो PDF/A अनुपालन का अन्वेषण करें।  

फ़ॉन्ट, साइज, या रंगों को बदलने में संकोच न करें—प्रोग्रामेटिक रूप से आप जो भी जनरेट कर सकते हैं उसकी कोई सीमा नहीं है। कोडिंग का आनंद लें, और आपके PDFs हमेशा वैसा ही रेंडर हों जैसा आप कल्पना करते हैं!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
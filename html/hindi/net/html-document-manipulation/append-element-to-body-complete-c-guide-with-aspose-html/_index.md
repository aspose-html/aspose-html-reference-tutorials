---
category: general
date: 2026-02-11
description: Aspose.HTML का उपयोग करके C# में तत्व को बॉडी में जोड़ें। पैराग्राफ एलिमेंट
  बनाना सीखें, फ़ॉन्ट वेट को बोल्ड सेट करें, फ़ॉन्ट फ़ैमिली को एरियल सेट करें, और
  CSS फ़ॉन्ट साइज को परिभाषित करें—सभी एक ही ट्यूटोरियल में।
draft: false
keywords:
- append element to body
- create paragraph element
- set font weight bold
- set font family arial
- define css font size
language: hi
og_description: Aspose.HTML का उपयोग करके बॉडी में तत्व जोड़ें। यह ट्यूटोरियल दिखाता
  है कि पैराग्राफ तत्व कैसे बनाएं, फ़ॉन्ट वेट को बोल्ड सेट करें, फ़ॉन्ट फ़ैमिली को
  एरियल सेट करें, और CSS फ़ॉन्ट साइज को परिभाषित करें।
og_title: बॉडी में तत्व जोड़ें – पूर्ण C# गाइड
tags:
- Aspose.HTML
- C#
- DOM manipulation
title: बॉडी में तत्व जोड़ें – Aspose.HTML के साथ पूर्ण C# गाइड
url: /hi/net/html-document-manipulation/append-element-to-body-complete-c-guide-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# बॉडी में एलिमेंट जोड़ें – Aspose.HTML के साथ पूर्ण C# गाइड

क्या आपको C# से किसी HTML दस्तावेज़ की **बॉडी में एलिमेंट जोड़ने** की ज़रूरत पड़ी है और आप सोचते रहे कि उदाहरण हमेशा अधूरे क्यों दिखते हैं? आप अकेले नहीं हैं। कई त्वरित‑स्टार्ट स्निपेट्स में आप देखेंगे कि एक पैराग्राफ़ जोड़ा गया है, लेकिन स्टाइलिंग विवरण—जैसे टेक्स्ट को **फ़ॉन्ट वेट बोल्ड सेट करना** या **फ़ॉन्ट फ़ैमिली Arial सेट करना**—छोड़ दिया जाता है।  

इस ट्यूटोरियल में हम एक वास्तविक परिदृश्य को देखेंगे: `<p>` टैग बनाना, उसकी स्टाइल परिभाषित करना (जिसमें **CSS फ़ॉन्ट साइज परिभाषित करना** शामिल है), और अंत में Aspose.HTML के साथ **बॉडी में एलिमेंट जोड़ना**। अंत तक आपके पास एक पूरी‑तरह से कार्यात्मक HTML फ़ाइल होगी जिसे आप किसी भी वेब पेज में डाल सकते हैं, और आप प्रत्येक कोड लाइन के पीछे का कारण समझ पाएँगे।

## आप क्या सीखेंगे

- प्रोग्रामेटिक रूप से **पैराग्राफ़ एलिमेंट बनाना**।
- `WebFontStyle` enum का उपयोग करके **फ़ॉन्ट वेट बोल्ड सेट करना** और **फ़ॉन्ट फ़ैमिली Arial सेट करना** के सटीक चरण।
- सटीक टाइपोग्राफी के लिए पॉइंट्स में **CSS फ़ॉन्ट साइज परिभाषित करना**।
- मैन्युअल स्ट्रिंग कंकैटनेशन के बिना **बॉडी में एलिमेंट जोड़ने** का सबसे साफ़ तरीका।
- टिप्स, एज‑केस, और एक पूर्ण रूप से चलने वाला उदाहरण जिसे आप कॉपी‑पेस्ट कर सकते हैं।

Aspose.HTML के अलावा कोई बाहरी लाइब्रेरी आवश्यक नहीं है, और कोड .NET 6+ (या .NET Framework 4.7.2) के साथ काम करता है। चलिए शुरू करते हैं।

---

## Step 1 – Aspose.HTML इंस्टॉल करें और प्रोजेक्ट सेट अप करें

सबसे पहले, सुनिश्चित करें कि आपके पास Aspose.HTML NuGet पैकेज है:

```bash
dotnet add package Aspose.HTML
```

> प्रो टिप: नवीनतम स्थिर संस्करण (इस लेखन के समय, **23.9.0**) का उपयोग करें ताकि बग फ़िक्स और नई CSS सुविधाओं का लाभ मिल सके।

एक नया कंसोल ऐप बनाएं (या मौजूदा प्रोजेक्ट में इंटीग्रेट करें) और निम्नलिखित `using` निर्देश जोड़ें:

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
```

ये नेमस्पेसेस आपको `HTMLDocument`, `CSSStyleDeclaration`, और `WebFontStyle` enum तक पहुंच प्रदान करते हैं, जिसकी हमें बाद में आवश्यकता होगी।

---

## Step 2 – CSS स्टाइल परिभाषित करें: फ़ॉन्ट फ़ैमिली, साइज, वेट, और इटैलिक

क्यों एक स्टाइल ऑब्जेक्ट परिभाषित करें बजाय एक कच्ची `style` एट्रिब्यूट स्ट्रिंग लिखने के? क्योंकि `CSSStyleDeclaration` प्रॉपर्टी नामों को वैलिडेट करता है, यूनिट कन्वर्ज़न संभालता है, और भविष्य में बदलाव को आसान बनाता है।

```csharp
// Step 2: Build a CSS style block
var paragraphStyle = new CSSStyleDeclaration();

// Set the font family to Arial – this satisfies the “set font family arial” requirement
paragraphStyle.FontFamily = "Arial";

// Define the font size in points; “define css font size” is clearer than using pixels for print‑like output
paragraphStyle.FontSize = new CSSLength(14, CSSLengthUnit.Point);

// Make the text bold – fulfills “set font weight bold”
paragraphStyle.FontWeight = WebFontStyle.Bold;

// Optional: add italic for visual flair
paragraphStyle.FontStyle = WebFontStyle.Italic;
```

> **पॉइंट्स क्यों?** पॉइंट्स डिवाइस‑इंडिपेंडेंट होते हैं, जिससे स्क्रीन और प्रिंट दोनों पर समान दृश्य आकार मिलता है। यदि आपको रिस्पॉन्सिव डिज़ाइन चाहिए, तो `CSSLengthUnit.Point` को `CSSLengthUnit.Px` या `%` से बदल दें।

---

## Step 3 – नया HTML दस्तावेज़ बनाएं

Aspose.HTML आपको एक साफ़, DOM‑जैसा API देता है जो ब्राउज़र की तरह काम करता है। `HTMLDocument` को आप JavaScript के `document` ऑब्जेक्ट की तरह सोच सकते हैं।

```csharp
// Step 3: Initialize an empty HTML document
var htmlDoc = new HTMLDocument();
```

इस चरण पर दस्तावेज़ में न्यूनतम `<html><head></head><body></body></html>` संरचना मौजूद है, जो आगे की मैनिपुलेशन के लिए तैयार है।

---

## Step 4 – पैराग्राफ़ एलिमेंट बनाएं और स्टाइल लागू करें

अब हम वास्तव में **पैराग्राफ़ एलिमेंट बनाते** हैं। `CreateElement` मेथड एक `IHTMLElement` लौटाता है जिसे हम एट्रिब्यूट्स और इंटीर कंटेंट से समृद्ध कर सकते हैं।

```csharp
// Step 4: Build the <p> element
var paragraph = htmlDoc.CreateElement("p");

// Apply the previously built CSS style; CssText converts the declaration to a valid style string
paragraph.SetAttribute("style", paragraphStyle.CssText);

// Insert the visible text
paragraph.InnerHTML = "Styled with WebFontStyle – bold, italic, Arial, 14pt.";
```

यदि आप `paragraphStyle.CssText` को देखें तो आपको कुछ इस तरह मिलेगा:

```
font-family: Arial; font-size: 14pt; font-weight: bold; font-style: italic;
```

यह स्ट्रिंग बिल्कुल वही है जिसे ब्राउज़र इंटरप्रेट करेगा, लेकिन हमने मैन्युअल कंकैटनेशन से बचा।

---

## Step 5 – बॉडी में एलिमेंट जोड़ें

यह वह क्षण है जिसका आप इंतज़ार कर रहे थे: **बॉडी में एलिमेंट जोड़ना**। यह एक ही लाइन पूरे काम को संभालती है, `<p>` को दस्तावेज़ के `<body>` नोड में डालती है।

```csharp
// Step 5: Append the styled paragraph to the document body
htmlDoc.Body.AppendChild(paragraph);
```

> **एज केस अलर्ट:** यदि आप `AppendChild` को ऐसे नोड पर कॉल करते हैं जिसमें पहले से वही एलिमेंट मौजूद है, तो एलिमेंट को स्थानांतरित किया जाएगा—डुप्लिकेट नहीं। यह लूप में अनजाने में दोहराए गए पैराग्राफ़ को रोकता है।

---

## Step 6 – दस्तावेज़ सहेजें और आउटपुट सत्यापित करें

अंत में, HTML को डिस्क पर लिखें ताकि आप इसे किसी भी ब्राउज़र में खोल सकें:

```csharp
// Step 6: Persist the HTML file
string outputPath = Path.Combine(Environment.CurrentDirectory, "StyledParagraph.html");
htmlDoc.Save(outputPath);

// Optional: launch the file automatically (works on Windows)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo(outputPath) { UseShellExecute = true });
```

### अपेक्षित परिणाम

**StyledParagraph.html** खोलने पर एक ही लाइन का टेक्स्ट दिखना चाहिए:

> *Styled with WebFontStyle – bold, italic, Arial, 14pt.*

टेक्स्ट **बोल्ड**, **इटैलिक**, **Arial** में रेंडर होगा, और आकार **14 pt** होगा। यदि आप स्रोत को देखें तो आपको यह मिलेगा:

```html
<!DOCTYPE html>
<html>
<head></head>
<body>
  <p style="font-family: Arial; font-size: 14pt; font-weight: bold; font-style: italic;">
    Styled with WebFontStyle – bold, italic, Arial, 14pt.
  </p>
</body>
</html>
```

यह एक साफ़, मानकों‑अनुरूप दस्तावेज़ है जो पूरी तरह से C# से बनाया गया है।

---

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

नीचे पूरा प्रोग्राम है जिसे आप `Program.cs` में डाल सकते हैं। अन्य कोई फ़ाइल आवश्यक नहीं है।

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Define CSS style (font family, size, weight, style)
        var paragraphStyle = new CSSStyleDeclaration
        {
            FontFamily = "Arial",                                   // set font family arial
            FontSize = new CSSLength(14, CSSLengthUnit.Point),      // define css font size
            FontWeight = WebFontStyle.Bold,                         // set font weight bold
            FontStyle = WebFontStyle.Italic                         // optional italic for demo
        };

        // 2️⃣ Create an empty HTML document
        var htmlDoc = new HTMLDocument();

        // 3️⃣ Build a <p> element and attach the style
        var paragraph = htmlDoc.CreateElement("p");
        paragraph.SetAttribute("style", paragraphStyle.CssText);
        paragraph.InnerHTML = "Styled with WebFontStyle – bold, italic, Arial, 14pt.";

        // 4️⃣ Append element to body
        htmlDoc.Body.AppendChild(paragraph);

        // 5️⃣ Save the file
        string output = Path.Combine(Environment.CurrentDirectory, "StyledParagraph.html");
        htmlDoc.Save(output);
        Console.WriteLine($"HTML saved to: {output}");

        // Open automatically (Windows only)
        System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo(output) { UseShellExecute = true });
    }
}
```

`dotnet run` चलाएँ और आपके पास एक तैयार‑उपयोग HTML फ़ाइल होगी।

---

## सामान्य प्रश्न एवं एज केस

### यदि मुझे कई पैराग्राफ़ जोड़ने हों तो क्या करें?

सिर्फ **Step 4** और **Step 5** को लूप के अंदर दोहराएँ। याद रखें कि प्रत्येक `CreateElement("p")` कॉल एक नया नोड लौटाता है, इसलिए आप अनजाने में वही एलिमेंट दोबारा उपयोग नहीं करेंगे।

```csharp
for (int i = 1; i <= 3; i++)
{
    var p = htmlDoc.CreateElement("p");
    p.SetAttribute("style", paragraphStyle.CssText);
    p.InnerHTML = $"Paragraph {i}";
    htmlDoc.Body.AppendChild(p);
}
```

### क्या मैं इनलाइन स्टाइल के बजाय बाहरी CSS फ़ाइलें उपयोग कर सकता हूँ?

बिल्कुल। इनलाइन `style` एट्रिब्यूट को क्लास नाम से बदलें और एक `<style>` ब्लॉक या बाहरी स्टाइलशीट लिंक जोड़ें। यहाँ इनलाइन तरीका स्पष्टता के लिए दिखाया गया है और यह सुनिश्चित करता है कि आप **बॉडी में एलिमेंट जोड़ते** समय स्टाइल एलिमेंट के साथ ही रह जाए।

### HTML5‑स्पेसिफिक एट्रिब्यूट्स (जैसे `data-*`) के बारे में क्या?

`SetAttribute` किसी भी एट्रिब्यूट नाम के साथ काम करता है, इसलिए आप कर सकते हैं:

```csharp
paragraph.SetAttribute("data-id", "12345");
```

यह एट्रिब्यूट अंतिम मार्कअप में संरक्षित रहेगा।

### क्या यह .NET Core पर Linux में काम करता है?

हां। Aspose.HTML क्रॉस‑प्लेटफ़ॉर्म है; केवल यह सुनिश्चित करें कि नेटिव डिपेंडेंसीज़ स्थापित हों (`libgdiplus` कुछ डिस्ट्रिब्यूशन्स में) यदि आप बाद में दस्तावेज़ को इमेज में रेंडर करने की योजना बनाते हैं।

---

## निष्कर्ष

अब आपके पास एक ठोस, एंड‑टू‑एंड उदाहरण है जो Aspose.HTML का उपयोग करके C# में **बॉडी में एलिमेंट जोड़ता** है। हमने बताया कि कैसे **पैराग्राफ़ एलिमेंट बनाएं**, **फ़ॉन्ट वेट बोल्ड सेट करें**, **फ़ॉन्ट फ़ैमिली Arial सेट करें**, और **CSS फ़ॉन्ट साइज परिभाषित करें**—सभी चरणों के पीछे के कारणों के साथ।  

बिना झिझक प्रयोग करें: फ़ॉन्ट फ़ैमिली बदलें, साइज यूनिट बदलें, या `color` या `text-shadow` जैसी अतिरिक्त CSS प्रॉपर्टीज़ जोड़ें। यही पैटर्न अन्य HTML एलिमेंट्स (टेबल्स, इमेजेज, SVGs) पर भी लागू होता है, इसलिए आप इस बुनियाद को पूरी‑फ़ीचर डॉक्यूमेंट जेनरेटर में विस्तारित कर सकते हैं।

### अगले कदम

- **Aspose.HTML रेंडरिंग** का उपयोग करके HTML को PDF या PNG में बदलें।
- डायनामिक बिहेवियर के लिए **बाहरी JavaScript इंजेक्ट** करना सीखें।
- सर्वर‑साइड HTML जनरेशन के लिए **Razor टेम्प्लेट्स** के साथ इस एप्रोच को मिलाएँ।

क्या आपने कोई ट्विस्ट आज़माया? कमेंट्स में शेयर करें, और कोडिंग का आनंद लें!  

<img src="append-element-to-body.png" alt="append element to body example" width="600">

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
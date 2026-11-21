---
category: general
date: 2026-11-20
description: C# ग्राफिक्स में एंटीएलीअसिंग को सक्षम करने और प्रोग्रामेटिक रूप से फ़ॉन्ट
  आकार तथा फ़ॉन्ट शैली सेट करने के लिए ImageRenderingOptions का उपयोग करते हुए एक
  पूर्ण, चलाने योग्य उदाहरण।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable antialiasing
- set font size
- set font style programmatically
- C# graphics rendering
- ImageRenderingOptions example
language: hi
lastmod: 2026-11-20
og_description: C# ग्राफ़िक्स में एंटीएलीअसिंग कैसे सक्षम करें, फ़ॉन्ट आकार सेट करें,
  और ImageRenderingOptions का उपयोग करके प्रोग्रामेटिकली फ़ॉन्ट शैली सेट करें – पूर्ण
  कोड और व्याख्या।
og_image_alt: Screenshot of antialiased text with custom font size and style generated
  by C# code showing how to enable antialiasing
og_title: C# में प्रोग्रामेटिकली एंटीएलियासिंग को सक्षम करने और फ़ॉन्ट का आकार एवं
  शैली सेट करने का तरीका
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: How to enable antialiasing in C# graphics and set font size, set font
    style programmatically with a complete, runnable example using ImageRenderingOptions.
  headline: How to enable antialiasing and set font size and style programmatically
    in C#
  type: TechArticle
tags:
- C#
- graphics
- antialiasing
- fonts
title: C# में प्रोग्रामेटिकली एंटीएलियासिंग को सक्षम करने और फ़ॉन्ट का आकार व शैली
  सेट करने का तरीका
url: /hi/net/canvas-and-image-manipulation/how-to-enable-antialiasing-and-set-font-size-and-style-progr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में एंटीएलियासिंग को सक्षम करने और फ़ॉन्ट आकार व शैली को प्रोग्रामेटिकली सेट करने का तरीका

C# ग्राफ़िक्स में एंटीएलियासिंग को सक्षम करना एक सामान्य आवश्यकता है जब आपको आकारों या टेक्स्ट पर स्मूद किनारे चाहिए। यह ट्यूटोरियल आपको **ImageRenderingOptions** क्लास का उपयोग करके एंटीएलियासिंग को सक्षम करने, फ़ॉन्ट आकार सेट करने, और फ़ॉन्ट शैली को प्रोग्रामेटिकली सेट करने का तरीका दिखाता है। गाइड के अंत तक आपके पास एक स्व-निहित कंसोल एप्लिकेशन होगा जो एक इमेज फ़ाइल में स्पष्ट, स्टाइल्ड टेक्स्ट रेंडर करता है।

आप सीखेंगे कि रेंडरिंग पाइपलाइन को कैसे कॉन्फ़िगर करें, सही फ़ॉन्ट फ़ैमिली चुनें, फ़ॉन्ट आकार को समायोजित करें, और कोड से बाहर निकले बिना बोल्ड या इटैलिक शैली लागू करें। एकमात्र पूर्वापेक्षा एक हालिया .NET SDK और Aspose.Imaging NuGet पैकेज है, जिसे उदाहरण स्वचालित रूप से इंस्टॉल करता है।

## Prerequisites

- .NET 6.0 SDK या बाद का संस्करण (डाउनलोड: https://dotnet.microsoft.com/)
- Visual Studio 2022 या कोई भी एडिटर जो .NET प्रोजेक्ट्स को सपोर्ट करता हो
- **Aspose.Imaging** NuGet पैकेज (`ImageRenderingOptions` प्रदान करने वाली लाइब्रेरी)

आप पैकेज को निम्न कमांड से जोड़ सकते हैं:

```bash
dotnet add package Aspose.Imaging
```

## ImageRenderingOptions के साथ एंटीएलियासिंग कैसे सक्षम करें

`ImageRenderingOptions` वह केंद्रीय ऑब्जेक्ट है जो नियंत्रित करता है कि Aspose.Imaging ग्राफ़िक्स कैसे ड्रॉ करता है। इसका `UseAntialiasing` प्रॉपर्टी सेट करने से रास्टराइज़र किनारों को स्मूद करता है, जिससे एंटीएलियासिंग बंद होने पर दिखाई देने वाला खुरदुरा “सीढ़ी” प्रभाव समाप्त हो जाता है।

```csharp
// Step 1: Create a new ImageRenderingOptions instance
ImageRenderingOptions renderingOptions = new ImageRenderingOptions();

// Step 2: Enable antialiasing for smoother graphics
renderingOptions.UseAntialiasing = true;
```

एंटीएलियासिंग को सक्षम करना उच्च‑गुणवत्ता वाले UI एलिमेंट्स, चार्ट रेंडरिंग, और किसी भी स्थिति में आवश्यक है जहाँ विज़ुअल फ़िडेलिटी मायने रखती है।

## फ़ॉन्ट आकार को प्रोग्रामेटिकली सेट करें

फ़ॉन्ट आकार निर्धारित करता है कि अंतिम बिटमैप में ग्लिफ़ कितने बड़े दिखेंगे। आप इसे इच्छित पॉइंट साइज के साथ `Font` ऑब्जेक्ट बनाकर बदल सकते हैं। नीचे दिया गया उदाहरण आकार को **24 pt** सेट करता है, जो पढ़ने योग्य हेडिंग्स के लिए सामान्य साइज है।

```csharp
// Step 3: Choose a font family and size
Font font = new Font("Arial", 24); // 24‑point Arial
```

आप `24` को किसी भी पूर्णांक या फ़्लोटिंग‑पॉइंट वैल्यू से बदल सकते हैं ताकि आपके लेआउट की आवश्यकताएँ पूरी हों। यदि आपको पिक्सेल‑आधारित साइजिंग चाहिए तो `Font` क्लास `GraphicsUnit` पैरामीटर भी स्वीकार करता है।

## फ़ॉन्ट शैली को प्रोग्रामेटिकली सेट करें

बोल्ड, इटैलिक, या अंडरलाइन शैली लागू करना सिर्फ `Font` बनाते समय `WebFontStyle` फ़्लैग पास करने का मामला है। `WebFontStyle` एनीम कई शैलियों को बिटवाइज़ OR ऑपरेशन से जोड़ता है।

```csharp
// Step 4: Apply bold and italic styles
font = new Font("Arial", 24, WebFontStyle.Bold | WebFontStyle.Italic);
```

यदि आपको केवल एक ही शैली चाहिए, तो `WebFontStyle.Bold`, `WebFontStyle.Italic`, या `WebFontStyle.Underline` का उपयोग करें। यह तरीका आपको **फ़ॉन्ट शैली को प्रोग्रामेटिकली सेट** करने देता है बिना अलग‑अलग फ़ॉन्ट फ़ाइलों को हार्ड‑कोड किए।

## पूर्ण चलाने योग्य उदाहरण

नीचे एक पूर्ण कंसोल एप्लिकेशन है जो सब कुछ एक साथ जोड़ता है:

```csharp
using System;
using Aspose.Imaging;
using Aspose.Imaging.Brushes;
using Aspose.Imaging.ImageOptions;
using Aspose.Imaging.Sources;
using Aspose.Imaging.FileFormats.Png;
using Aspose.Imaging.Graphics;
using Aspose.Imaging.Fonts;
using Aspose.Imaging.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Create rendering options and enable antialiasing
        ImageRenderingOptions renderingOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            // Enable hinting for sharper text on low‑resolution images
            TextOptions = new TextOptions { UseHinting = true }
        };

        // 2️⃣ Define the font (size + style)
        Font font = new Font("Arial", 24, WebFontStyle.Bold | WebFontStyle.Italic);

        // 3️⃣ Prepare a bitmap with a white background
        int width = 800;
        int height = 200;
        using (var bitmap = new RasterImage(width, height, PixelFormat.Format24bppRgb))
        {
            bitmap.SaveOptions = new PngOptions { ColorType = PngColorType.Truecolor };
            bitmap.Fill(new SolidBrush(Color.White));

            // 4️⃣ Create a graphics object that respects our rendering options
            using (Graphics graphics = new Graphics(bitmap, renderingOptions))
            {
                // Position the text in the center of the image
                PointF location = new PointF(50, 80);
                graphics.DrawString("Antialiased Bold Italic Text", font, new SolidBrush(Color.Black), location);
            }

            // 5️⃣ Save the result
            string outputPath = "antialiased_text.png";
            bitmap.Save(outputPath);
            Console.WriteLine($"Image saved to {outputPath}");
        }
    }
}
```

### प्रत्येक सेक्शन की व्याख्या

| सेक्शन | क्यों महत्वपूर्ण है |
|---------|----------------|
| **Rendering options** | `UseAntialiasing` को ऑन करने से वेक्टर आकारों और टेक्स्ट दोनों के लिए स्मूद किनारे सुनिश्चित होते हैं। |
| **TextOptions.UseHinting** | हिन्टिंग कम‑रिज़ॉल्यूशन आउटपुट पर ग्लिफ़ आउटलाइन को समायोजित करके पठनीयता बढ़ाता है। |
| **Font construction** | `Font` कंस्ट्रक्टर **फ़ॉन्ट आकार सेट** और **फ़ॉन्ट शैली को प्रोग्रामेटिकली सेट** दोनों को एक ही कॉल में जोड़ता है। |
| **Graphics object** | `renderingOptions` को `Graphics` में पास करने से हर ड्रॉइंग ऑपरेशन एंटीएलियासिंग और हिन्टिंग का सम्मान करता है। |
| **DrawString** | यह मेथड कॉन्फ़िगर किए गए फ़ॉन्ट के साथ टेक्स्ट रेंडर करता है, जिससे अंतिम एंटीएलियास्ड आउटपुट बनता है। |
| **Saving** | PNG फ़ॉर्मेट अतिरिक्त कम्प्रेशन आर्टिफैक्ट्स के बिना सटीक पिक्सेल डेटा को संरक्षित करता है। |

#### अपेक्षित आउटपुट

प्रोग्राम चलाने पर **antialiased_text.png** बनता है जो इस प्रकार दिखता है:

![Antialiased text example](https://example.com/antialiased_text.png "Antialiased text with custom font size and style – how to enable antialiasing")

यह इमेज 24 pt पर स्मूद किनारों के साथ स्पष्ट, बोल्ड‑इटैलिक Arial टेक्स्ट दिखाती है, जिससे यह पुष्टि होती है कि **एंटीएलियासिंग को कैसे सक्षम करें** इच्छित रूप से काम किया।

## सामान्य विविधताएँ और किनारे के मामले

- **विभिन्न फ़ॉन्ट फ़ैमिली** – `"Arial"` को किसी भी इंस्टॉल्ड फ़ॉन्ट नाम (जैसे `"Times New Roman"`) से बदलें। यदि फ़ॉन्ट उपलब्ध नहीं है, तो Aspose.Imaging `FontNotFoundException` फेंकेगा।
- **फ़ॉन्ट आकार बदलना** – `Font` कंस्ट्रक्टर के दूसरे आर्ग्यूमेंट को किसी भी फ़्लोटिंग‑पॉइंट वैल्यू पर सेट करें। बड़े मान पठनीयता बढ़ाते हैं लेकिन बड़े बिटमैप की आवश्यकता हो सकती है।
- **एकाधिक शैलियाँ** – `WebFontStyle.Underline` को `Bold` और `Italic` के साथ `|` ऑपरेटर से जोड़ें: `WebFontStyle.Bold | WebFontStyle.Underline`।
- **हाई‑DPI रेंडरिंग** – रेटिना‑स्टाइल आउटपुट के लिए बिटमैप डाइमेंशन बढ़ाएँ (जैसे, 1600 × 400) जबकि वही फ़ॉन्ट आकार रखें; एंटीएलियासिंग फिर भी स्मूद परिणाम देगा।
- **एंटीएलियासिंग को डिसेबल करना** – `renderingOptions.UseAntialiasing = false;` सेट करके विज़ुअल अंतर देखें। टेक्स्ट खुरदुरा दिखेगा, जो डिबगिंग या परफ़ॉर्मेंस टेस्टिंग में उपयोगी है।

## प्रो टिप्स

- **`Font` ऑब्जेक्ट को कैश करें** यदि आप लूप में कई स्ट्रिंग्स ड्रॉ कर रहे हैं; प्रत्येक इटरेशन में नया `Font` बनाना ओवरहेड जोड़ता है।
- **`TextOptions.UseHinting` को एंटीएलियासिंग के साथ उपयोग करें** ताकि लो‑रिज़ॉल्यूशन इमेजेज़ पर शार्पनेस और स्मूदनेस के बीच सर्वश्रेष्ठ संतुलन मिले।
- **आउटपुट फ़ाइल को वैलिडेट करें** किसी ऐसे इमेज व्यूअर से खोलें जो पिक्सेल‑लेवल डिटेल दिखाता हो (जैसे Photoshop या GIMP)। इससे आप पुष्टि कर सकते हैं कि एंटीएलियासिंग वास्तव में प्रभावी हुआ है।

## निष्कर्ष

अब आप जानते हैं कि C# ग्राफ़िक्स में **एंटीएलियासिंग को कैसे सक्षम करें**, **फ़ॉन्ट आकार कैसे सेट करें**, और `ImageRenderingOptions` का उपयोग करके **फ़ॉन्ट शैली को प्रोग्रामेटिकली कैसे सेट करें**। पूरा उदाहरण एक व्यावहारिक वर्कफ़्लो दर्शाता है जिसे आप अपने प्रोजेक्ट्स में कॉपी कर सकते हैं, चाहे आप चार्ट जेनरेट कर रहे हों, UI थंबनेल बना रहे हों, या वेब सर्विसेज़ के लिए डायनामिक ग्राफ़िक्स बना रहे हों।

आगे आप **फ़ॉन्ट रंग को प्रोग्रामेटिकली सेट करना**, **ग्रेडिएंट फ़िल्स जोड़ना**, या **वेक्टर शैप्स को समान एंटीएलियासिंग सेटिंग्स के साथ रेंडर करना** एक्सप्लोर कर सकते हैं। ये सभी टॉपिक यहाँ कवर किए गए बुनियादी सिद्धांतों पर आधारित हैं, इसलिए आप पूरी तरह से कोड से हाई‑क्वालिटी ग्राफ़िक्स बनाने के लिए तैयार हैं। Happy rendering!

## What Should You Learn Next?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक रिसोर्स में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [How to Enable Antialiasing When Rendering HTML to PNG in C#](/html/english/net/rendering-html-documents/how-to-enable-antialiasing-when-rendering-html-to-png-in-c/)
- [How to enable antialiasing for HTML image rendering in C#](/html/english/net/rendering-html-documents/how-to-enable-antialiasing-for-html-image-rendering-in-c/)
- [How to Enable Antialiasing in Aspose HTML to PDF Conversion (C#)](/html/english/net/html-extensions-and-conversions/how-to-enable-antialiasing-in-aspose-html-to-pdf-conversion/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-08-15
description: C# में कस्टम रिसोर्स हैंडलर बनाकर इमेज और CSS जैसी HTML रिसोर्सेज़ को
  मैनेज करें। HTMLLoadOptions, मेमोरी स्ट्रीम्स और HTMLDocument लोडिंग सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom resource handler
- C# resource handler
- HTMLLoadOptions
- HTMLDocument loading
- memory stream for resources
language: hi
lastmod: 2026-08-15
og_description: C# में कस्टम रिसोर्स हैंडलर बनाकर HTML संसाधनों के स्ट्रीमिंग को नियंत्रित
  करें। यह ट्यूटोरियल HTMLLoadOptions सेटअप, मेमोरी स्ट्रीम हैंडलिंग, और कस्टम लॉजिक
  के साथ HTMLDocument लोड करने को दर्शाता है।
og_image_alt: Screenshot of C# code defining a custom resource handler class for HTML
  loading
og_title: C# में कस्टम रिसोर्स हैंडलर बनाएं – HTML रिसोर्स प्रबंधन के लिए पूर्ण गाइड
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  headline: Create custom resource handler in C# for HTML loading
  type: TechArticle
- description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  name: Create custom resource handler in C# for HTML loading
  steps:
  - name: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
    text: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
  - name: Configure `HTMLLoadOptions` to use the handler.
    text: Configure `HTMLLoadOptions` to use the handler.
  - name: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
    text: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
  - name: (Optional) Store received resources to disk for verification.
    text: (Optional) Store received resources to disk for verification.
  type: HowTo
tags:
- C#
- HTML
- resource handling
title: HTML लोडिंग के लिए C# में कस्टम रिसोर्स हैंडलर बनाएं
url: /hi/net/working-with-html-documents/create-custom-resource-handler-in-c-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML लोडिंग के लिए C# में कस्टम रिसोर्स हैंडलर बनाएं

यदि आपको **कस्टम रिसोर्स हैंडलर** HTML फ़ाइलों के लिए बनाना है, तो यह गाइड आपको ठीक‑ठीक दिखाएगा। आप सीखेंगे कि कैसे HTML दस्तावेज़ लोड करते समय इमेज, CSS और अन्य एसेट्स को इंटरसेप्ट किया जाए, `HTMLLoadOptions` और मेमोरी‑आधारित स्ट्रीम का उपयोग करके।

यह ट्यूटोरियल पुन: उपयोग योग्य हैंडलर को लागू करने, लोड विकल्पों को कॉन्फ़िगर करने और यह सत्यापित करने के लिए आवश्यक सभी चीज़ें कवर करता है कि रिसोर्स सही ढंग से कैप्चर हो रहे हैं। बाहरी दस्तावेज़ की आवश्यकता नहीं—केवल नीचे दिया गया कोड और व्याख्याएँ।

## Prerequisites

- .NET 6.0 या बाद का संस्करण
- C# की बुनियादी समझ
- वह HTML प्रोसेसिंग लाइब्रेरी जिसका रेफ़रेंस `HTMLDocument`, `HtmlLoadOptions`, और `ResourceHandler` प्रदान करता है (उदाहरण के लिए, GroupDocs.Viewer for .NET)

## समाधान का Overview

हम करेंगे:

1. **कस्टम रिसोर्स हैंडलर** को `ResourceHandler` को सबक्लास करके बनाना।
2. `HTMLLoadOptions` को हैंडलर उपयोग करने के लिए कॉन्फ़िगर करना।
3. `HTMLDocument` के साथ HTML फ़ाइल लोड करना, जबकि हैंडलर प्रत्येक रिसोर्स के लिए स्ट्रीम प्रदान करता है।
4. (वैकल्पिक) प्राप्त रिसोर्स को डिस्क पर स्टोर करके सत्यापन करना।

प्रत्येक चरण में पूरा स्रोत कोड और उसके पीछे की तर्कशक्ति दी गई है।

## Step 1: Define the custom resource handler class

कस्टम हैंडलर बनाने का मतलब है `HandleResource` को ओवरराइड करना ताकि लाइब्रेरी रिसोर्स बाइट्स को आपके नियंत्रित स्ट्रीम में लिख सके। `MemoryStream` का उपयोग डेटा को मेमोरी में रखता है, जो टेस्टिंग या आगे की प्रोसेसिंग के लिए आदर्श है।

```csharp
using System;
using System.IO;
using GroupDocs.Viewer.Handler;   // Adjust namespace to match your library

namespace HtmlResourceDemo
{
    /// <summary>
    /// Provides a memory stream for each HTML resource (images, CSS, etc.).
    /// </summary>
    public class MyHandler : ResourceHandler
    {
        /// <summary>
        /// Called by the viewer for every external resource referenced in the HTML.
        /// </summary>
        /// <param name="info">Information about the resource (name, MIME type, etc.).</param>
        /// <returns>A writable stream that receives the resource data.</returns>
        public override Stream HandleResource(ResourceInfo info)
        {
            // A fresh MemoryStream ensures the viewer can write the resource bytes.
            // You could replace this with a FileStream to save directly to disk.
            return new MemoryStream();
        }
    }
}
```

**Why this matters:**  
`HandleResource` को ओवरराइड करने से आपको रिसोर्स डेटा कहां जाएगा, इस पर पूरी नियंत्रण मिलती है। यदि बाद में आपको इमेज को कैश करना, CSS ट्रांसफ़ॉर्म करना या रिसोर्स उपयोग को लॉग करना हो, तो आप `MemoryStream` को किसी भी कस्टम स्ट्रीम इम्प्लीमेंटेशन से बदल सकते हैं।

## Step 2: Configure `HTMLLoadOptions` to use the handler

`HTMLLoadOptions` आपको हैंडलर को लोडिंग पाइपलाइन में प्लग करने की सुविधा देता है। `ResourceHandler` प्रॉपर्टी सेट करने से व्यूअर हर बाहरी एसेट के लिए `MyHandler` को कॉल करेगा।

```csharp
using GroupDocs.Viewer.Options;   // Namespace for HtmlLoadOptions

// ...

var loadOptions = new HtmlLoadOptions
{
    // Attach the custom handler defined in Step 1
    ResourceHandler = new MyHandler()
};
```

**Why this matters:**  
`ResourceHandler` को असाइन नहीं किया गया तो व्यूअर रिसोर्स को अपनी डिफ़ॉल्ट लोकेशन (अक्सर एक टेम्प फ़ोल्डर) में लिखेगा। अपना हैंडलर निर्दिष्ट करके आप **कस्टम रिसोर्स हैंडलर** व्यवहार बनाते हैं जो आपके एप्लिकेशन की स्टोरेज स्ट्रैटेजी के अनुरूप हो।

## Step 3: Load the HTML document with the configured options

अब HTML फ़ाइल लोड करें। व्यूअर प्रत्येक रिसोर्स के लिए `MyHandler.HandleResource` को कॉल करेगा।

```csharp
using GroupDocs.Viewer;           // Namespace for HTMLDocument

// Path to the source HTML file
string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// Load the document using the custom load options
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);
```

इस बिंदु पर HTML कंटेंट पार्स हो चुका है, और सभी बाहरी रिसोर्स `MyHandler` द्वारा प्रदान किए गए मेमोरी बफ़र्स में स्ट्रीम हो गए हैं।

## Step 4 (optional): Access the captured resources

यदि आपको रिसोर्स को जांचना या स्थायी रूप से सहेजना है, तो आप `MyHandler` को इस तरह बदल सकते हैं कि प्रत्येक `MemoryStream` को रिसोर्स नाम के आधार पर एक डिक्शनरी में स्टोर किया जाए।

```csharp
public class MyHandler : ResourceHandler
{
    // Stores streams for later retrieval
    public Dictionary<string, MemoryStream> Resources { get; } = new();

    public override Stream HandleResource(ResourceInfo info)
    {
        var stream = new MemoryStream();
        Resources[info.Name] = stream;
        return stream;
    }
}
```

लोडिंग के बाद, आप `handler.Resources` पर इटरेट करके प्रत्येक को डिस्क पर लिख सकते हैं:

```csharp
var handler = new MyHandler();
var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);

// Save each captured resource
foreach (var kvp in handler.Resources)
{
    string fileName = Path.Combine("output_resources", kvp.Key);
    File.WriteAllBytes(fileName, kvp.Value.ToArray());
    Console.WriteLine($"Saved resource: {fileName}");
}
```

**Why this matters:**  
रिसोर्स को स्टोर करने से इमेज ऑप्टिमाइज़ेशन, CSS मिनिफिकेशन या आर्काइविंग जैसी पोस्ट‑प्रोसेसिंग संभव होती है। यह यह भी स्पष्ट करता है कि **create custom resource handler** लॉजिक इच्छित रूप से काम कर रहा है।

## Step 5: Clean up

`HTMLDocument` और सभी स्ट्रीम को डिस्पोज़ करना न भूलें ताकि अनमैनेज्ड रिसोर्स मुक्त हो सकें।

```csharp
doc.Dispose();                     // Releases internal buffers
foreach (var stream in handler.Resources.Values)
{
    stream.Dispose();              // Flushes and releases memory
}
```

## Full runnable example

नीचे एक स्व-समाहित प्रोग्राम है जो क्लास डिफ़िनिशन से लेकर रिसोर्स एक्सट्रैक्शन तक सभी चरणों को दर्शाता है।

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Viewer;
using GroupDocs.Viewer.Handler;
using GroupDocs.Viewer.Options;

namespace HtmlResourceDemo
{
    public class MyHandler : ResourceHandler
    {
        public Dictionary<string, MemoryStream> Resources { get; } = new();

        public override Stream HandleResource(ResourceInfo info)
        {
            var stream = new MemoryStream();
            Resources[info.Name] = stream;
            return stream;
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare paths
            string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");
            string outputDir = Path.Combine("output_resources");
            Directory.CreateDirectory(outputDir);

            // 2️⃣ Create handler and load options
            var handler = new MyHandler();
            var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };

            // 3️⃣ Load the HTML document
            using (HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions))
            {
                // Document is now loaded; resources are in handler.Resources
            }

            // 4️⃣ Persist captured resources
            foreach (var kvp in handler.Resources)
            {
                string filePath = Path.Combine(outputDir, kvp.Key);
                File.WriteAllBytes(filePath, kvp.Value.ToArray());
                Console.WriteLine($"Saved: {filePath}");
            }

            // 5️⃣ Clean up streams
            foreach (var stream in handler.Resources.Values)
                stream.Dispose();

            Console.WriteLine("All resources processed.");
        }
    }
}
```

**Expected output**

```
Saved: output_resources/logo.png
Saved: output_resources/styles.css
Saved: output_resources/banner.jpg
All resources processed.
```

कंसोल प्रत्येक रिसोर्स को सूचीबद्ध करेगा जो व्यूअर आपके कस्टम हैंडलर के माध्यम से स्ट्रीम किया, यह पुष्टि करते हुए कि **create custom resource handler** वर्कफ़्लो सफल रहा।

## Common questions and edge cases

| Question | Answer |
|----------|--------|
| *यदि कोई रिसोर्स बड़ा है (जैसे हाई‑रेज़ोल्यूशन इमेज)?* | `MemoryStream` के बजाय एक `FileStream` उपयोग करें जो टेम्प फ़ोल्डर की ओर इशारा करता हो। इससे मेमोरी की अत्यधिक खपत रोकी जा सकती है। |
| *क्या मैं रिसोर्स को प्रकार के आधार पर फ़िल्टर कर सकता हूँ?* | `HandleResource` के अंदर `info.MimeType` या `info.Extension` जांचें और अनचाहे प्रकारों के लिए `null` रिटर्न करें। `null` रिटर्न करने से व्यूअर उस रिसोर्स को स्किप कर देगा। |
| *क्या थ्रेड‑सेफ़्टी आवश्यक है?* | यदि एक ही हैंडलर इंस्टेंस को कई समवर्ती लोड्स में उपयोग किया जाता है, तो `Resources` डिक्शनरी को लॉक से सुरक्षित करें या एक concurrent collection उपयोग करें। |
| *मैं रिलेटिव URLs को कैसे सपोर्ट करूँ?* | `ResourceInfo` में मूल URL मौजूद होता है; आप इसे HTML फ़ाइल के बेस पाथ के साथ मिलाकर रिलेटिव रेफ़रेंसेज़ को रिज़ॉल्व कर सकते हैं और फिर स्टोर कर सकते हैं। |

## Conclusion

अब आप जानते हैं कि **create custom resource handler** को C# में HTML लोडिंग के लिए कैसे बनाया जाए, `HTMLLoadOptions` को कैसे कॉन्फ़िगर किया जाए, स्ट्रीम किए गए एसेट्स को कैसे कैप्चर किया जाए, और जिम्मेदारी से क्लीन‑अप कैसे किया जाए। यह पैटर्न आपको रिसोर्स मैनेजमेंट पर पूर्ण नियंत्रण देता है, जिससे ऑन‑द‑फ़्लाई इमेज प्रोसेसिंग, CSS री‑राइटिंग या सुरक्षित स्टोरेज जैसे परिदृश्य संभव होते हैं।

अगला कदम, **HTMLDocument लोडिंग** को विभिन्न रेंडरिंग विकल्पों के साथ एक्सप्लोर करें, या हैंडलर को **C# resource handler** इम्प्लीमेंटेशन में विस्तारित करें जो सीधे क्लाउड स्टोरेज में लिखता हो। अपने प्रोजेक्ट की विशिष्ट रिसोर्स वर्कफ़्लो के अनुसार `HandleResource` मेथड को प्रयोग करके अनुकूलित करें।

## What Should You Learn Next?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच को एक्सप्लोर कर सकें।

- [Create HTML from String in C# – Custom Resource Handler Guide](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Custom Resource Handler in C# – Convert HTML to ZIP Tutorial](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
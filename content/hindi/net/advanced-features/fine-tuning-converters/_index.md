---
title: Aspose.HTML के साथ .NET में फाइन-ट्यूनिंग कन्वर्टर्स
linktitle: .NET में फ़ाइन-ट्यूनिंग कन्वर्टर्स
second_title: Aspose.HTML .NET HTML हेरफेर एपीआई
description: .NET के लिए Aspose.HTML के साथ HTML को PDF, XPS और छवियों में परिवर्तित करना सीखें। कोड उदाहरणों और अक्सर पूछे जाने वाले प्रश्नों के साथ चरण-दर-चरण ट्यूटोरियल।
type: docs
weight: 16
url: /hi/net/advanced-features/fine-tuning-converters/
---

## परिचय

.NET के लिए Aspose.HTML एक शक्तिशाली लाइब्रेरी है जो डेवलपर्स को विभिन्न स्वरूपों में HTML दस्तावेज़ों में हेरफेर करने और परिवर्तित करने की अनुमति देती है। चाहे आपको HTML को PDF, XPS, या छवियों में परिवर्तित करने की आवश्यकता हो, या अन्य HTML-संबंधित कार्य करने की आवश्यकता हो, Aspose.HTML आपको काम पूरा करने में मदद करने के लिए उपकरणों का एक मजबूत सेट प्रदान करता है।

इस ट्यूटोरियल में, हम .NET के लिए Aspose.HTML की कुछ आवश्यक विशेषताओं का पता लगाएंगे और प्रत्येक उदाहरण के लिए चरण-दर-चरण स्पष्टीकरण प्रदान करेंगे। इस ट्यूटोरियल के अंत तक, आपको अपने .NET अनुप्रयोगों में .NET के लिए Aspose.HTML का उपयोग करने की ठोस समझ हो जाएगी।

## आवश्यक शर्तें

इससे पहले कि हम उदाहरणों पर गौर करें, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ मौजूद हैं:

-  .NET के लिए Aspose.HTML: आपके पास .NET लाइब्रेरी के लिए Aspose.HTML स्थापित होना चाहिए। आप इसे यहां से डाउनलोड कर सकते हैं[लिंक को डाउनलोड करें](https://releases.aspose.com/html/net/).

- अस्थायी लाइसेंस (वैकल्पिक): यदि आपके पास वैध लाइसेंस नहीं है, तो आप अस्थायी लाइसेंस प्राप्त कर सकते हैं[यहाँ](https://purchase.aspose.com/temporary-license/).

अब, आइए .NET के लिए Aspose.HTML के साथ कुछ सामान्य उपयोग के मामलों का पता लगाएं।

## नामस्थान आयात करें

अपने C# कोड में, आवश्यक नामस्थान आयात करके प्रारंभ करें:

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Pdf;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Xps;
using Aspose.Html.Rendering.Pdf.Encryption;
using Aspose.Html.Drawing;
```

## HTML को पीडीएफ में बदलें

### चरण 1: HTML कोड तैयार करें

```csharp
var code = @"<span>Hello World!!</span>";
```

### चरण 2: HTML दस्तावेज़ प्रारंभ करें

```csharp
using (var document = new HTMLDocument(code, "."))
```

### चरण 3: पीडीएफ डिवाइस बनाएं और आउटपुट फ़ाइल निर्दिष्ट करें

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### चरण 4: HTML को पीडीएफ में प्रस्तुत करें

```csharp
document.RenderTo(device);
```

यह उदाहरण एक HTML स्निपेट को एक पीडीएफ दस्तावेज़ में परिवर्तित करता है। आप आवश्यकतानुसार HTML कोड और आउटपुट फ़ाइल को कस्टमाइज़ कर सकते हैं।

## कस्टम पृष्ठ आकार सेट करें

### चरण 1: HTML कोड तैयार करें

```csharp
var code = @"<span>Hello World!!</span>";
```

### चरण 2: HTML दस्तावेज़ प्रारंभ करें

```csharp
using (var document = new HTMLDocument(code, "."))
```

### चरण 3: पीडीएफ रेंडरिंग विकल्प बनाएं

```csharp
var options = new PdfRenderingOptions()
{
    PageSetup =
    {
        AnyPage = new Page(
            new Size(
                Length.FromInches(5),
                Length.FromInches(2)))
    }
};
```

### चरण 4: पीडीएफ डिवाइस बनाएं और विकल्प और आउटपुट फ़ाइल निर्दिष्ट करें

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### चरण 5: HTML को पीडीएफ में प्रस्तुत करें

```csharp
document.RenderTo(device);
```

यह उदाहरण दर्शाता है कि परिणामी पीडीएफ दस्तावेज़ के लिए कस्टम पेज आकार कैसे सेट किया जाए।

## संकल्प समायोजित करें

### चरण 1: HTML कोड तैयार करें और फ़ाइल में सहेजें

```csharp
var code = @"
    <style>
    p
    { 
        background: blue; 
    }
    @media(min-resolution: 300dpi)
    {
        p 
        { 
            /* high-resolution screen color */
            background: green
        }
    }
    </style>
    <p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### चरण 2: HTML दस्तावेज़ प्रारंभ करें

```csharp
using (var document = new HTMLDocument("document.html"))
```

### चरण 3: कम-रिज़ॉल्यूशन के लिए पीडीएफ रेंडरिंग विकल्प बनाएं

```csharp
var options = new PdfRenderingOptions()
{
    HorizontalResolution = 50,
    VerticalResolution = 50
};
```

### चरण 4: पीडीएफ डिवाइस बनाएं और कम-रिज़ॉल्यूशन के लिए विकल्प और आउटपुट फ़ाइल निर्दिष्ट करें

```csharp
using (var device = new PdfDevice(options, "output_resolution_50.pdf"))
```

### चरण 5: कम-रिज़ॉल्यूशन के लिए HTML को पीडीएफ में प्रस्तुत करें

```csharp
document.RenderTo(device);
```

### चरण 6: उच्च-रिज़ॉल्यूशन के लिए पीडीएफ रेंडरिंग विकल्प बनाएं

```csharp
options = new PdfRenderingOptions()
{
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

### चरण 7: पीडीएफ डिवाइस बनाएं और उच्च-रिज़ॉल्यूशन के लिए विकल्प और आउटपुट फ़ाइल निर्दिष्ट करें

```csharp
using (var device = new PdfDevice(options, "output_resolution_300.pdf"))
```

### चरण 8: उच्च-रिज़ॉल्यूशन के लिए HTML को पीडीएफ में प्रस्तुत करें

```csharp
document.RenderTo(device);
```

यह उदाहरण दिखाता है कि निम्न और उच्च-रिज़ॉल्यूशन दोनों स्क्रीन पर विचार करते हुए HTML को पीडीएफ में प्रस्तुत करते समय रिज़ॉल्यूशन को कैसे समायोजित किया जाए।

## पृष्ठभूमि रंग निर्दिष्ट करें

### चरण 1: HTML कोड तैयार करें और फ़ाइल में सहेजें

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### चरण 2: HTML दस्तावेज़ प्रारंभ करें

```csharp
using (var document = new HTMLDocument("document.html"))
```

### चरण 3: पृष्ठभूमि रंग के साथ पीडीएफ रेंडरिंग विकल्प आरंभ करें

```csharp
var options = new PdfRenderingOptions()
{
    BackgroundColor = System.Drawing.Color.Cyan
};
```

### चरण 4: पीडीएफ डिवाइस बनाएं और विकल्प और आउटपुट फ़ाइल निर्दिष्ट करें

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### चरण 5: HTML को पीडीएफ में प्रस्तुत करें

```csharp
document.RenderTo(device);
```

यह उदाहरण दर्शाता है कि HTML को पीडीएफ में परिवर्तित करते समय पृष्ठभूमि का रंग कैसे निर्दिष्ट किया जाए।

## बाएँ और दाएँ पृष्ठ आकार सेट करें

### चरण 1: HTML कोड तैयार करें

```csharp
var code = @"<style>div { page-break-after: always; }</style>
    <div>First Page</div>
    <div>Second Page</div>
    <div>Third Page</div>
    <div>Fourth Page</div>";
```

### चरण 2: HTML दस्तावेज़ प्रारंभ करें

```csharp
using (var document = new HTMLDocument(code, "."))
```

### चरण 3: बाएँ और दाएँ पृष्ठ आकार के साथ पीडीएफ रेंडरिंग विकल्प बनाएँ

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.SetLeftRightPage(
    new Page(new Size(400, 200)),
    new Page(new Size(400, 100))
);
```

### चरण 4: पीडीएफ डिवाइस बनाएं और विकल्प और आउटपुट फ़ाइल निर्दिष्ट करें

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### चरण 5: HTML को पीडीएफ में प्रस्तुत करें

```csharp
document.RenderTo(device);
```

यह उदाहरण दिखाता है कि HTML को पीडीएफ में परिवर्तित करते समय बाएं और दाएं पृष्ठों के लिए अलग-अलग पृष्ठ आकार कैसे सेट करें।

## पृष्ठ आकार को सामग्री के अनुसार समायोजित करें

### चरण 1: HTML कोड तैयार करें

```csharp
var code = @"<style>
    div { page-break-after: always; }
</style>
<div style='border: 1px solid red; width: 400px'>First Page</div>
<div style='border: 1px solid red; width: 600px'>Second Page</div>";
```

### चरण 2: HTML दस्तावेज़ प्रारंभ करें

```csharp
using (var document = new HTMLDocument(code, "."))
```

### चरण 3: पीडीएफ रेंडरिंग विकल्प बनाएं

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.AnyPage = new Page(new Size(500, 200));
options.PageSetup.AdjustToWidestPage = true;
```

### चरण 4: पीडीएफ डिवाइस बनाएं और विकल्प और आउटपुट फ़ाइल निर्दिष्ट करें

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### चरण 5: HTML को पीडीएफ में प्रस्तुत करें

```csharp
document.RenderTo(device);
```

यह उदाहरण दर्शाता है कि HTML को पीडीएफ में परिवर्तित करते समय पृष्ठ आकार को व्यापक सामग्री में कैसे समायोजित किया जाए।

## पीडीएफ अनुमतियाँ निर्दिष्ट करें

### चरण 1: HTML कोड तैयार करें

```csharp
var code = @"<div>Hello World!!</div>";
```

### चरण 2: HTML दस्तावेज़ प्रारंभ करें

```csharp
using (var document = new HTMLDocument(code, "."))
```

### चरण 3: अनुमतियों के साथ पीडीएफ रेंडरिंग विकल्प बनाएं

```csharp
var options = new PdfRenderingOptions();
options.Encryption = new PdfEncryptionInfo(
    "user_pwd",
    "owner_pwd",
    PdfPermissions.PrintDocument,
    PdfEncryptionAlgorithm.RC4_128
);
```

### चरण 4: पीडीएफ डिवाइस बनाएं और विकल्प और आउटपुट फ़ाइल निर्दिष्ट करें

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### चरण 5: HTML को पीडीएफ में प्रस्तुत करें

```csharp
document.RenderTo(device);
```

यह उदाहरण दर्शाता है कि HTML को संरक्षित पीडीएफ में परिवर्तित करते समय अनुमतियाँ और एन्क्रिप्शन कैसे निर्दिष्ट किया जाए।

## छवि-विशिष्ट विकल्प निर्दिष्ट करें

### चरण 1: HTML कोड तैयार करें

```csharp
var code = @"<div>Hello World!!</div>";
```

### चरण 2: HTML दस्तावेज़ प्रारंभ करें

```csharp
using (var document = new HTMLDocument(code, "."))
```

### चरण 3: छवि रेंडरिंग विकल्प बनाएं

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### चरण 4: छवि डिवाइस बनाएं और विकल्प और आउटपुट फ़ाइल निर्दिष्ट करें

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### चरण 5: HTML को छवि में प्रस्तुत करें

```csharp
document.RenderTo(device);
```

यह उदाहरण दर्शाता है कि प्रारूप, रिज़ॉल्यूशन और स्मूथिंग मोड जैसे विशिष्ट रेंडरिंग विकल्पों के साथ HTML को एक छवि में कैसे परिवर्तित किया जाए।

## एक्सपीएस रेंडरिंग विकल्प निर्दिष्ट करें

### चरण 1: HTML कोड तैयार करें

```csharp
var code = @"<span>Hello World!!</span>";
```

### चरण 2: HTML दस्तावेज़ प्रारंभ करें

```csharp
using (var document = new HTMLDocument(code, "."))
```

### चरण 3: पृष्ठ आकार के साथ XPS रेंडरिंग विकल्प बनाएं

```csharp
var options = new XpsRenderingOptions();
options.PageSetup.AnyPage = new Page(
    new Size(
        Length.FromInches(5),
        Length.FromInches(2)
    )
);
```

### चरण 4: एक्सपीएस डिवाइस बनाएं और विकल्प और आउटपुट फ़ाइल निर्दिष्ट करें

```csharp
using (var device = new XpsDevice(options, "output.xps"))
```

### चरण 5: HTML को XPS में प्रस्तुत करें

```csharp
document.RenderTo(device);
```

यह उदाहरण दिखाता है कि कस्टम पेज आकार और रेंडरिंग विकल्पों के साथ HTML को XPS में कैसे परिवर्तित किया जाए।

## एकाधिक HTML दस्तावेज़ों को पीडीएफ में संयोजित करें

### चरण 1: एकाधिक दस्तावेज़ों के लिए HTML कोड तैयार करें

```csharp
var code1 = @"<br><span style='color: green'>Hello World!!</span>";
var code2 = @"<br><span style='color: blue'>Hello World!!</span>";
var code3 = @"<br><span style='color: red'>Hello World!!</span>";
```

### चरण 2: मर्ज करने के लिए HTML दस्तावेज़ बनाएं

```csharp
using (var document1 = new HTMLDocument(code1, "."))
using (var document2 = new HTMLDocument(code2, "."))
using (var document3 = new HTMLDocument(code3, "."))
```

### चरण 3: HTML रेंडरर को आरंभ करें

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### चरण 4: मर्ज किए गए आउटपुट के लिए पीडीएफ डिवाइस बनाएं

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### चरण 5: HTML दस्तावेज़ों को पीडीएफ में मर्ज करें

```csharp
renderer.Render(device, document1, document2, document3);
```

यह उदाहरण दर्शाता है कि .NET के लिए Aspose.HTML का उपयोग करके एकाधिक HTML दस्तावेज़ों को एक एकल PDF फ़ाइल में कैसे संयोजित किया जाए।

## रेंडरिंग टाइमआउट सेट करें

### चरण 1: जावास्क्रिप्ट के साथ HTML कोड तैयार करें

```csharp
var code = @"
    <script>
        var count = 0;
        setInterval(function()
        {
            var element = document.createElement('div');
            var message = (++count) + '. ' + 'Hello World!!';
            var text = document.createTextNode(message);
            element.appendChild(text);
            document.body.appendChild(element);
        }, 1000);
    </script>";
```

### चरण 2: HTML दस्तावेज़ प्रारंभ करें

```csharp
using (var document = new HTMLDocument(code, "."))
```

### चरण 3: HTML रेंडरर को आरंभ करें

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### चरण 4: पीडीएफ डिवाइस बनाएं और रेंडरिंग टाइमआउट सेट करें

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### चरण 5: टाइमआउट के साथ HTML को पीडीएफ में प्रस्तुत करें

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

यह उदाहरण दर्शाता है कि HTML को पीडीएफ में परिवर्तित करते समय रेंडरिंग टाइमआउट कैसे सेट किया जाए, जो गतिशील सामग्री या लंबे समय तक चलने वाली स्क्रिप्ट से निपटने के दौरान उपयोगी हो सकता है।

## निष्कर्ष

.NET के लिए Aspose.HTML एक बहुमुखी लाइब्रेरी है जो डेवलपर्स को HTML दस्तावेज़ों के साथ कुशलतापूर्वक काम करने में सक्षम बनाती है। इस ट्यूटोरियल में, हमने बुनियादी HTML से लेकर पीडीएफ रूपांतरणों से लेकर कस्टम पेज आकार, रिज़ॉल्यूशन और अनुमतियों जैसी अधिक उन्नत सुविधाओं तक विभिन्न उदाहरणों को कवर किया है। इन उदाहरणों का पालन करके, आप अपने .NET अनुप्रयोगों में .NET के लिए Aspose.HTML की पूरी क्षमता का उपयोग कर सकते हैं।

 यदि आपके कोई प्रश्न हैं या अतिरिक्त सहायता की आवश्यकता है, तो यहां आने में संकोच न करें[Aspose.HTML फोरम](https://forum.aspose.com/) समर्थन और मार्गदर्शन के लिए.

## अक्सर पूछे जाने वाले प्रश्न

### Q1. .NET के लिए Aspose.HTML क्या है?
   
A1: .NET के लिए Aspose.HTML एक .NET लाइब्रेरी है जो डेवलपर्स को HTML दस्तावेज़ों को प्रोग्रामेटिक रूप से हेरफेर करने और परिवर्तित करने में सक्षम बनाती है। यह HTML सामग्री के साथ काम करने के लिए सुविधाओं की एक विस्तृत श्रृंखला प्रदान करता है, जिसमें HTML से पीडीएफ, एक्सपीएस और छवि रूपांतरण के साथ-साथ उन्नत रेंडरिंग विकल्प भी शामिल हैं।

### Q2. मैं .NET के लिए Aspose.HTML कहाँ से डाउनलोड कर सकता हूँ?

 A2: आप .NET के लिए Aspose.HTML डाउनलोड कर सकते हैं[लिंक को डाउनलोड करें](https://releases.aspose.com/html/net/).

### Q3. क्या मुझे .NET के लिए Aspose.HTML का उपयोग करने के लिए लाइसेंस की आवश्यकता है?

A3: जबकि आप बिना लाइसेंस के .NET के लिए Aspose.HTML का उपयोग कर सकते हैं, सभी सुविधाओं को अनलॉक करने और किसी भी वॉटरमार्क या सीमाओं को हटाने के लिए उत्पादन उपयोग के लिए लाइसेंस प्राप्त करने की अनुशंसा की जाती है।

### Q4. मैं .NET के लिए Aspose.HTML से उत्पन्न अपनी पीडीएफ फाइलों को कैसे सुरक्षित रख सकता हूं?

A4: .NET के लिए Aspose.HTML का उपयोग करके HTML को PDF में रेंडर करते समय आप PDF अनुमतियाँ और एन्क्रिप्शन सेटिंग्स निर्दिष्ट कर सकते हैं। यह आपको यह नियंत्रित करने की अनुमति देता है कि परिणामी पीडीएफ फाइलों तक कौन पहुंच सकता है और उन्हें संशोधित कर सकता है।

### Q5. क्या मैं HTML को XPS या छवियों जैसे अन्य प्रारूपों में परिवर्तित कर सकता हूँ?

A5: हां, .NET के लिए Aspose.HTML HTML को पीडीएफ, एक्सपीएस और छवियों (उदाहरण के लिए, जेपीईजी) सहित विभिन्न प्रारूपों में परिवर्तित करने का समर्थन करता है। आप अपनी विशिष्ट आवश्यकताओं को पूरा करने के लिए रूपांतरण सेटिंग्स को अनुकूलित कर सकते हैं।
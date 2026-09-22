---
category: general
date: 2026-02-11
description: إضافة عنصر إلى الـ body باستخدام Aspose.HTML في C#. تعلّم كيفية إنشاء
  عنصر فقرة، ضبط وزن الخط إلى عريض، تعيين عائلة الخط إلى Arial، وتحديد حجم الخط عبر
  CSS — كل ذلك في درس واحد.
draft: false
keywords:
- append element to body
- create paragraph element
- set font weight bold
- set font family arial
- define css font size
language: ar
og_description: إضافة عنصر إلى الجسم باستخدام Aspose.HTML. يوضح هذا الدرس كيفية إنشاء
  عنصر فقرة، وتعيين وزن الخط إلى غامق، وتحديد عائلة الخط إلى Arial، وتعريف حجم الخط
  في CSS.
og_title: إضافة عنصر إلى الـ Body – دليل C# الكامل
tags:
- Aspose.HTML
- C#
- DOM manipulation
title: إضافة عنصر إلى الـ Body – دليل C# الكامل مع Aspose.HTML
url: /ar/net/html-document-manipulation/append-element-to-body-complete-c-guide-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إلحاق عنصر إلى الجسم – دليل C# كامل مع Aspose.HTML

هل احتجت يومًا إلى **append element to body** في مستند HTML من C# وتساءلت لماذا تبدو الأمثلة دائمًا غير مكتملة؟ لست وحدك. في العديد من مقتطفات البدء السريع سترى فقرة تُضاف، لكن تفاصيل التنسيق—مثل جعل النص **set font weight bold** أو استخدام **set font family arial**—تُترك.

في هذا الدرس سنستعرض سيناريو واقعي: إنشاء وسم `<p>`، تعريف نمطه (بما في ذلك **define css font size**)، وأخيرًا **append element to body** باستخدام Aspose.HTML. في النهاية ستحصل على ملف HTML يعمل بالكامل يمكنك إدراجه في أي صفحة ويب، وستفهم السبب وراء كل سطر من الشيفرة.

## ما ستتعلمه

- كيفية **create paragraph element** برمجيًا.
- الخطوات الدقيقة لـ **set font weight bold** و **set font family arial** باستخدام تعداد `WebFontStyle`.
- كيفية **define css font size** بالنقاط للحصول على طباعة دقيقة.
- أنظف طريقة لـ **append element to body** دون دمج سلاسل يدوي.
- نصائح، حالات حافة، ومثال كامل قابل للتنفيذ يمكنك نسخه ولصقه.

لا تحتاج إلى مكتبات خارجية غير Aspose.HTML، وتعمل الشيفرة مع .NET 6+ (أو .NET Framework 4.7.2). لنبدأ.

---

## الخطوة 1 – تثبيت Aspose.HTML وإعداد المشروع

أولًا، تأكد من أنك تمتلك حزمة NuGet الخاصة بـ Aspose.HTML:

```bash
dotnet add package Aspose.HTML
```

> نصيحة احترافية: استخدم أحدث نسخة مستقرة (في وقت كتابة هذا الدليل، **23.9.0**) للاستفادة من إصلاحات الأخطاء والميزات الجديدة في CSS.

أنشئ تطبيقًا جديدًا من نوع console (أو أدمجه في مشروع موجود) وأضف توجيهات `using` التالية:

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
```

هذه المساحات الاسمية تمنحك الوصول إلى `HTMLDocument` و `CSSStyleDeclaration` وتعداد `WebFontStyle` الذي سنحتاجه لاحقًا.

## الخطوة 2 – تعريف نمط CSS: عائلة الخط، الحجم، الوزن، والمائل

لماذا نعرّف كائن نمط بدلاً من كتابة سلسلة سمة `style` مباشرة؟ لأن `CSSStyleDeclaration` يتحقق من صحة أسماء الخصائص، يتعامل مع تحويل الوحدات، ويجعل التغييرات المستقبلية سهلة.

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

> **لماذا النقاط؟** النقاط غير معتمدة على الجهاز، مما يضمن نفس الحجم البصري على الشاشة وعند الطباعة. إذا كنت بحاجة إلى تصميم متجاوب، استبدل `CSSLengthUnit.Point` بـ `CSSLengthUnit.Px` أو `%`.

## الخطوة 3 – إنشاء مستند HTML جديد

يوفر لك Aspose.HTML واجهة برمجة تطبيقات نظيفة تشبه DOM، مشابهة لما تحصل عليه من `document` في JavaScript.

```csharp
// Step 3: Initialize an empty HTML document
var htmlDoc = new HTMLDocument();
```

في هذه المرحلة يحتوي المستند على بنية `<html><head></head><body></body></html>` الحد الأدنى، جاهزة للتعديل.

## الخطوة 4 – إنشاء عنصر الفقرة وتطبيق النمط

الآن نقوم فعليًا **create paragraph element**. تُعيد طريقة `CreateElement` كائنًا من نوع `IHTMLElement` يمكننا إثرائه بالسمات والمحتوى الداخلي.

```csharp
// Step 4: Build the <p> element
var paragraph = htmlDoc.CreateElement("p");

// Apply the previously built CSS style; CssText converts the declaration to a valid style string
paragraph.SetAttribute("style", paragraphStyle.CssText);

// Insert the visible text
paragraph.InnerHTML = "Styled with WebFontStyle – bold, italic, Arial, 14pt.";
```

إذا فحصت `paragraphStyle.CssText`، سترى شيئًا مثل:

```
font-family: Arial; font-size: 14pt; font-weight: bold; font-style: italic;
```

هذه السلسلة هي بالضبط ما سيفسره المتصفح، لكننا تجنبنا الجمع اليدوي.

## الخطوة 5 – إلحاق عنصر إلى الجسم

هذه هي اللحظة التي انتظرتها: **append element to body**. هذا السطر الواحد يقوم بالعمل الشاق، بإدراج `<p>` في عقدة `<body>` الخاصة بالمستند.

```csharp
// Step 5: Append the styled paragraph to the document body
htmlDoc.Body.AppendChild(paragraph);
```

> **تنبيه حالة حافة:** إذا استدعيت `AppendChild` على عقدة تحتوي بالفعل على العنصر، سيتم نقل العنصر—not duplicated. هذا يمنع تكرار الفقرات عن طريق الخطأ عند التكرار.

## الخطوة 6 – حفظ المستند والتحقق من النتيجة

أخيرًا، احفظ ملف HTML على القرص حتى تتمكن من فتحه في أي متصفح:

```csharp
// Step 6: Persist the HTML file
string outputPath = Path.Combine(Environment.CurrentDirectory, "StyledParagraph.html");
htmlDoc.Save(outputPath);

// Optional: launch the file automatically (works on Windows)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo(outputPath) { UseShellExecute = true });
```

### النتيجة المتوقعة

فتح **StyledParagraph.html** يجب أن يعرض سطرًا واحدًا من النص:

> *Styled with WebFontStyle – bold, italic, Arial, 14pt.*

النص سيكون **bold**، **italic**، معروضًا بخط **Arial**، وحجمه **14 pt**. إذا فحصت المصدر، سترى:

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

هذا مستند نظيف ومتوافق مع المعايير تم إنشاؤه بالكامل من C#.

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي البرنامج الكامل الذي يمكنك وضعه في `Program.cs`. لا تحتاج إلى ملفات أخرى.

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

شغّل `dotnet run` وستحصل على ملف HTML جاهز للاستخدام.

## أسئلة شائعة وحالات حافة

### ماذا لو احتجت لإضافة فقرات متعددة؟

ما عليك سوى تكرار **Step 4** و **Step 5** داخل حلقة. تذكر أن كل استدعاء لـ `CreateElement("p")` يُعيد عقدة جديدة، لذا لن تعيد استخدام نفس العنصر عن طريق الخطأ.

```csharp
for (int i = 1; i <= 3; i++)
{
    var p = htmlDoc.CreateElement("p");
    p.SetAttribute("style", paragraphStyle.CssText);
    p.InnerHTML = $"Paragraph {i}";
    htmlDoc.Body.AppendChild(p);
}
```

### هل يمكنني استخدام ملفات CSS خارجية بدلاً من الأنماط المضمنة؟

بالطبع. استبدل سمة `style` المضمنة باسم فئة وأضف كتلة `<style>` أو رابطًا إلى ورقة أنماط خارجية. تم عرض النهج المضمن هنا للوضوح ولأن ذلك يضمن أن النمط ينتقل مع العنصر عندما تقوم بـ **append element to body**.

### ماذا عن السمات الخاصة بـ HTML5 (مثل `data-*`)؟

`SetAttribute` يعمل مع أي اسم سمة، لذا يمكنك القيام بـ:

```csharp
paragraph.SetAttribute("data-id", "12345");
```

ستُحفظ السمة في العلامة النهائية.

### هل يعمل هذا على .NET Core على لينكس؟

نعم. Aspose.HTML متعدد المنصات؛ فقط تأكد من تثبيت الاعتمادات الأصلية (`libgdiplus` على بعض التوزيعات) إذا كنت تخطط لتحويل المستند إلى صورة لاحقًا.

## الخلاصة

الآن لديك مثال شامل من البداية إلى النهاية يوضح **append element to body** باستخدام Aspose.HTML في C#. لقد غطينا كيفية **create paragraph element**، **set font weight bold**، **set font family arial**، و **define css font size**—كل ذلك مع توضيحات واضحة لأهمية كل خطوة.

لا تتردد في التجربة: استبدل عائلة الخط، غير وحدة الحجم، أو أضف خصائص CSS أخرى مثل `color` أو `text-shadow`. النمط نفسه يعمل مع عناصر HTML أخرى (جداول، صور، SVGs)، لذا يمكنك توسيع هذا الأساس إلى مولدات مستندات متكاملة.

### الخطوات التالية

- استكشف **Aspose.HTML rendering** لتحويل HTML إلى PDF أو PNG.
- تعلم كيفية **inject external JavaScript** للسلوك الديناميكي.
- اجمع هذا النهج مع **Razor templates** لتوليد HTML من جانب الخادم.

هل جربت تعديلًا؟ شاركه في التعليقات، وبرمجة سعيدة!  

<img src="append-element-to-body.png" alt="append element to body example" width="600">

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-09-10
description: تعلم كيفية استخدام HtmlSaveOptions في C# للتحكم في أنماط الخطوط على الويب
  وحفظ ملفات HTML باستخدام Aspose.HTML. يتضمن مثالًا كاملاً للكود ونصائح عملية.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use htmlsaveoptions
- Aspose HTML library
- WebFontStyle flags
- HTMLDocument conversion
- C# save HTML
- Aspose.Html SaveOptions
language: ar
lastmod: 2026-09-10
og_description: كيفية استخدام HtmlSaveOptions في C# لتمكين أنماط الخطوط الغامقة والمائلة
  عند حفظ HTML باستخدام Aspose.HTML. تابع المثال الكامل ونصائح الممارسات الأفضل.
og_image_alt: Screenshot showing how to use HtmlSaveOptions to save an HTML file in
  C#
og_title: كيفية استخدام HtmlSaveOptions في C# مع Aspose.HTML – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: Learn how to use HtmlSaveOptions in C# to control web‑font styles and
    save HTML files with Aspose.HTML. Full code example and practical tips included.
  headline: How to use HtmlSaveOptions in C# with Aspose.HTML
  type: TechArticle
- description: Learn how to use HtmlSaveOptions in C# to control web‑font styles and
    save HTML files with Aspose.HTML. Full code example and practical tips included.
  name: How to use HtmlSaveOptions in C# with Aspose.HTML
  steps:
  - name: Why configure WebFontStyle?
    text: 'When you export an HTML document, Aspose.HTML can embed web fonts that
      match the original styling. By setting `WebFontStyle`, you tell the exporter
      which font variants to include. This reduces the final file size when you only
      need specific styles and guarantees that the rendered output matches the '
  - name: 5.1 Controlling CSS embedding
    text: 'You can decide whether to embed CSS inline, keep external links, or embed
      everything:'
  - name: 5.2 Saving to a specific encoding
    text: '```csharp saveOptions.Encoding = Encoding.UTF8; ```'
  - name: 5.3 Handling large documents
    text: 'For very large HTML files, consider streaming the output to avoid high
      memory consumption:'
  - name: 5.4 Error handling best practice
    text: 'Wrap the entire workflow in a try‑catch block and log the exception details.
      This ensures that any I/O or parsing errors are captured:'
  - name: Expected console output
    text: '``` HTML saved successfully to ''YOUR_DIRECTORY/output.html''. ```'
  type: HowTo
tags:
- Aspose.HTML
- C#
- HTML processing
title: كيفية استخدام HtmlSaveOptions في C# مع Aspose.HTML
url: /ar/net/working-with-html-documents/how-to-use-htmlsaveoptions-in-c-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام HtmlSaveOptions في C# مع Aspose.HTML

إذا كنت بحاجة إلى التحكم في طريقة حفظ Aspose.HTML لمستند HTML، فإن **تعلم كيفية استخدام HtmlSaveOptions أمر أساسي**. يوضح لك هذا الدليل خطوة بخطوة كيفية استخدام HtmlSaveOptions لتمكين أنماط خطوط الويب الغامقة والمائلة أثناء حفظ المستند.

توفر مكتبة Aspose HTML واجهة برمجة تطبيقات غنية لتحميل ومعالجة وتصدير محتوى HTML. بنهاية هذا الدليل ستكون قادرًا على:

* تحميل ملف HTML موجود إلى كائن `HTMLDocument`.
* تهيئة `HtmlSaveOptions` لتطبيق علامات `WebFontStyle` المحددة.
* حفظ المستند المعدل إلى موقع جديد أو إلى تدفق.
* توسيع الحل لتشمل أنماط خطوط أخرى، CSS مخصص، ومعالجة الأخطاء.

## المتطلبات المسبقة

قبل البدء، تأكد من وجود ما يلي:

* .NET 6.0 أو أحدث مثبت.
* رخصة صالحة لـ **Aspose.HTML for .NET** (الإصدار التجريبي المجاني يكفي لهذا المثال).
* Visual Studio 2022 (أو أي بيئة تطوير C#) لتجميع وتشغيل الكود.

لا توجد حزم NuGet إضافية مطلوبة بخلاف `Aspose.HTML`.

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

أنشئ مشروع **Console App** جديد وأضف حزمة NuGet الخاصة بـ Aspose.HTML:

```bash
dotnet add package Aspose.HTML
```

بعد ذلك، في أعلى ملف `Program.cs`، استورد المساحات الاسمية المطلوبة:

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
```

تُظهر هذه المساحات الاسمية الأنواع `HTMLDocument` و `HtmlSaveOptions` و `WebFontStyle` التي ستستخدمها طوال الدليل.

## الخطوة 2: تحميل مستند HTML المصدر

العملية الأولى هي قراءة ملف HTML الذي تريد معالجته. استبدل `"YOUR_DIRECTORY/input.html"` بالمسار الفعلي لملفك.

```csharp
// Load the source HTML document from disk
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

`HTMLDocument` يقوم بتحليل العلامات، يبني شجرة DOM، ويجعلها جاهزة للمعالجة. إذا لم يكن الملف موجودًا، سيتم إلقاء استثناء، لذا قد ترغب في وضع هذا الاستدعاء داخل كتلة try‑catch في الكود الإنتاجي.

## الخطوة 3: إنشاء وتكوين HtmlSaveOptions

`HtmlSaveOptions` يتيح لك ضبط عملية الحفظ بدقة. لتمكين أنماط خطوط الويب الغامقة والمائلة، اجمع علامات `WebFontStyle` المقابلة باستخدام عامل OR البتّي (`|`).

```csharp
// Create a new HtmlSaveOptions instance
HtmlSaveOptions saveOptions = new HtmlSaveOptions();

// Enable bold and italic web‑font styles (equivalent to the old FontStyle flags)
saveOptions.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

### لماذا تهيئة WebFontStyle؟

عند تصدير مستند HTML، يمكن لـ Aspose.HTML تضمين خطوط الويب التي تتطابق مع النمط الأصلي. من خلال ضبط `WebFontStyle`، تخبر المصدّر أي متغيّرات للخط يجب تضمينها. هذا يقلل من حجم الملف النهائي عندما تحتاج فقط إلى أنماط محددة ويضمن أن المخرجات المعروضة تتطابق مع المصدر.

#### التغيّرات الشائعة

| النمط المطلوب | علامة `WebFontStyle` المقابلة |
|---------------|-----------------------------------|
| عادي (Regular) | `WebFontStyle.Regular` |
| غامق | `WebFontStyle.Bold` |
| مائل | `WebFontStyle.Italic` |
| غامق + مائل | `WebFontStyle.Bold | WebFontStyle.Italic` |
| جميع المتغيّرات | `WebFontStyle.All` |

يمكنك دمج أي مجموعة تناسب حالتك.

## الخطوة 4: حفظ المستند باستخدام الخيارات المكوّنة

الآن احفظ المستند إلى ملف جديد. طريقة `Save` تقبل مسار الهدف وكائن `HtmlSaveOptions` الذي أعددته.

```csharp
// Save the processed HTML using the configured options
document.Save("YOUR_DIRECTORY/output.html", saveOptions);
```

إذا كنت بحاجة للكتابة إلى تدفق ذاكرة (مثلاً لإرسال الملف عبر HTTP)، استخدم النسخة التي تقبل كائن `Stream`:

```csharp
using (var stream = new MemoryStream())
{
    document.Save(stream, saveOptions);
    // Reset the position to read the content later
    stream.Position = 0;
    // Example: return the stream from a Web API endpoint
}
```

## الخطوة 5: التحقق من النتيجة

افتح `output.html` في متصفح أو افحص الملف باستخدام محرر نصوص. يجب أن ترى أن كتلة `<style>` الآن تحتوي على قواعد `@font-face` لكل من المتغيّرات الغامقة والمائلة لأي خطوط ويب مشار إليها في المستند الأصلي.

**مقتطف النتيجة المتوقعة:**

```html
<link rel="stylesheet" href="fonts/Roboto-Bold.woff2" type="font/woff2">
<link rel="stylesheet" href="fonts/Roboto-Italic.woff2" type="font/woff2">
```

إذا كان HTML الأصلي يشير إلى عائلة خطوط لا تحتوي سوى على وزن عادي، سيقوم Aspose.HTML بتضمين ذلك الملف فقط، مع احترام إعداد `WebFontStyle`.

## متقدم: استخدام HtmlSaveOptions مع ميزات إضافية

### 5.1 التحكم في تضمين CSS

يمكنك تحديد ما إذا كنت تريد تضمين CSS داخل المستند، أو الحفاظ على الروابط الخارجية، أو تضمين كل شيء:

```csharp
saveOptions.CssSavingMode = CssSavingMode.EmbedAllCss;
```

### 5.2 الحفظ بترميز محدد

```csharp
saveOptions.Encoding = Encoding.UTF8;
```

### 5.3 معالجة المستندات الكبيرة

بالنسبة لملفات HTML الكبيرة جدًا، فكر في بث الناتج لتجنب استهلاك الذاكرة العالي:

```csharp
using (FileStream fs = new FileStream("large_output.html", FileMode.Create, FileAccess.Write))
{
    document.Save(fs, saveOptions);
}
```

### 5.4 أفضل ممارسات معالجة الأخطاء

ضع سير العمل بالكامل داخل كتلة try‑catch وسجّل تفاصيل الاستثناء. يضمن ذلك التقاط أي أخطاء في الإدخال/الإخراج أو التحليل:

```csharp
try
{
    // Load, configure, and save as shown earlier
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error processing HTML: {ex.Message}");
}
```

## نصيحة احترافية: إعادة استخدام HtmlSaveOptions عبر عمليات حفظ متعددة

إذا كنت بحاجة لحفظ عدة مستندات بنفس إعداد نمط الخط، أنشئ كائن `HtmlSaveOptions` واحد وأعد استخدامه. يقلل ذلك من عبء تخصيص الكائنات ويضمن مخرجات متسقة.

```csharp
HtmlSaveOptions sharedOptions = new HtmlSaveOptions
{
    WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic,
    CssSavingMode = CssSavingMode.EmbedAllCss
};

foreach (var file in Directory.GetFiles("input_folder", "*.html"))
{
    HTMLDocument doc = new HTMLDocument(file);
    string outputPath = Path.Combine("output_folder", Path.GetFileName(file));
    doc.Save(outputPath, sharedOptions);
}
```

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يدمج جميع الخطوات التي تم مناقشتها. انسخه إلى `Program.cs` وشغّله بعد تعديل مسارات الملفات.

```csharp
using System;
using System.IO;
using System.Text;
using Aspose.Html;
using Aspose.Html.Drawing;

class Program
{
    static void Main()
    {
        // Define input and output paths
        string inputPath = "YOUR_DIRECTORY/input.html";
        string outputPath = "YOUR_DIRECTORY/output.html";

        try
        {
            // Step 1: Load the source HTML document
            HTMLDocument document = new HTMLDocument(inputPath);

            // Step 2: Create HtmlSaveOptions and enable bold + italic web‑font styles
            HtmlSaveOptions saveOptions = new HtmlSaveOptions
            {
                WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic,
                // Optional: embed all CSS and use UTF‑8 encoding
                CssSavingMode = CssSavingMode.EmbedAllCss,
                Encoding = Encoding.UTF8
            };

            // Step 3: Save the document with the configured options
            document.Save(outputPath, saveOptions);

            Console.WriteLine($"HTML saved successfully to '{outputPath}'.");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

### مخرجات وحدة التحكم المتوقعة

```
HTML saved successfully to 'YOUR_DIRECTORY/output.html'.
```

افتح `output.html` المُنشأ لتأكيد وجود أنماط خطوط الويب الغامقة والمائلة.

## الخلاصة

أنت الآن تعرف **كيفية استخدام HtmlSaveOptions** للتحكم في تضمين خطوط الويب، ومعالجة CSS، والترميز عند حفظ HTML باستخدام مكتبة Aspose HTML في C#. من خلال ضبط علامات `WebFontStyle` يمكنك تخصيص المخرجات لتشمل فقط المتغيّرات الخطية التي تحتاجها، مما يحسن الأداء ويقلل حجم الملف.

من هنا يمكنك استكشاف خصائص أخرى في `HtmlSaveOptions` مثل `ImageSavingMode` و `JavaScriptSavingMode`، أو دمج خيارات متعددة لإنشاء خطوط تحويل معقدة. جرّب الحفظ إلى تدفقات لتطبيقات الويب، أو دمج سير العمل في نظام توليد مستندات أكبر.

---

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية حفظ HTML باستخدام Aspose.Html – دليل C# كامل](/html/english/net/working-with-html-documents/how-to-save-html-with-aspose-html-complete-c-guide/)
- [كيفية استخدام Aspose لتحويل HTML إلى PNG في C#](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-in-c/)
- [كيفية استخدام Aspose لتحويل HTML إلى PNG – دليل خطوة بخطوة](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
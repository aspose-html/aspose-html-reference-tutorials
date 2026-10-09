---
category: general
date: 2026-10-09
description: إنشاء مثيل ImagerenderingOptions لتمكين مضاد التعرجات وتحسين جودة عرض
  الرسومات في تطبيقات .NET.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create imagerenderingoptions instance
- ImageRenderingOptions
- antialiasing
- SmoothingMode
- graphics rendering
language: ar
lastmod: 2026-10-09
og_description: إنشاء كائن imagerenderingoptions لتمكين مضاد التعرجات وتحقيق عرض رسومات
  أكثر سلاسة في .NET. اتبع الدليل خطوة بخطوة.
og_image_alt: Screenshot showing smooth edges after enabling antialiasing with ImageRenderingOptions
og_title: إنشاء كائن ImageRenderingOptions – تحسين جودة الرسومات في .NET
schemas:
- author: Aspose
  dateModified: '2026-10-09'
  description: Create imagerenderingoptions instance to enable antialiasing and improve
    graphics rendering quality in .NET applications.
  headline: Create imagerenderingoptions instance for high‑quality graphics rendering
  type: TechArticle
- description: Create imagerenderingoptions instance to enable antialiasing and improve
    graphics rendering quality in .NET applications.
  name: Create imagerenderingoptions instance for high‑quality graphics rendering
  steps:
  - name: '**Forgetting to pass the options** – Rendering methods that accept `ImageRenderingOptions`
      will ignore antialiasing if you call the overload without the options parameter.
      Always use the three‑parameter `GetThumbnail` or equivalent method.'
    text: '**Forgetting to pass the options** – Rendering methods that accept `ImageRenderingOptions`
      will ignore antialiasing if you call the overload without the options parameter.
      Always use the three‑parameter `GetThumbnail` or equivalent method.'
  - name: '**Mixing SmoothingMode with ImageRenderingOptions** – Setting `Graphics.SmoothingMode`
      has no effect on Aspose.Slides rendering. Rely solely on `UseAntialiasing`.'
    text: '**Mixing SmoothingMode with ImageRenderingOptions** – Setting `Graphics.SmoothingMode`
      has no effect on Aspose.Slides rendering. Rely solely on `UseAntialiasing`.'
  - name: '**Using an outdated library version** – `ImageRenderingOptions` was introduced
      in Aspose.Slides 20.5. Ensure your NuGet package is up‑to‑date; otherwise the
      class may be missing or lack the `UseAntialiasing` property.'
    text: '**Using an outdated library version** – `ImageRenderingOptions` was introduced
      in Aspose.Slides 20.5. Ensure your NuGet package is up‑to‑date; otherwise the
      class may be missing or lack the `UseAntialiasing` property.'
  type: HowTo
tags:
- .NET
- C#
- rendering
title: إنشاء كائن imagerenderingoptions لتصوير الرسومات بجودة عالية
url: /ar/net/canvas-and-image-manipulation/create-imagerenderingoptions-instance-for-high-quality-graph/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مثيل ImageRenderingOptions لتص rendering رسومات عالية الجودة

إذا كنت بحاجة إلى **إنشاء مثيل ImageRenderingOptions** لإنتاج رسومات أكثر سلاسة، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك. من خلال تكوين خاصية **antialiasing** تُزيل الحواف المتعرجة وتحصل على مخرجات بمستوى احترافي دون الحاجة إلى مكتبات إضافية.

سوف تتعلم كيفية إنشاء كائن `ImageRenderingOptions`، تفعيل **antialiasing**، وربط الخيارات بمحرك العرض مثل Aspose.Slides أو System.Drawing. يفترض هذا الدليل أنك على دراية بأساسيات صياغة C# ولديك بيئة تطوير .NET جاهزة.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الـ API متاح في .NET Standard 2.0+)
- إشارة إلى التجميع الذي يحتوي على `ImageRenderingOptions` (مثل `Aspose.Slides.NET`)
- بيئة تطوير متكاملة مثل Visual Studio 2022 أو VS Code مع امتداد C#
- فهم أساسي لسلاسل معالجة الرسومات

## الخطوة 1: إنشاء مثيل ImageRenderingOptions

العملية الأولى هي تخصيص كائن `ImageRenderingOptions` جديد. يعمل هذا الكائن كحاوية لجميع العلامات المتعلقة بالعرض.

```csharp
using Aspose.Slides;          // Replace with the appropriate namespace
using Aspose.Slides.Export;   // Needed for ImageRenderingOptions

// Step 1: Create the ImageRenderingOptions instance
ImageRenderingOptions imgOptions = new ImageRenderingOptions();
```

إنشاء المثيل يمنحك التحكم الكامل في طريقة تحويل الرسومات المتجهة إلى نقطية. يمكنك لاحقًا تمكين أو تعطيل ميزات محددة مثل **antialiasing**، وضعية عرض النص، أو ضغط الصورة.

## الخطوة 2: تفعيل antialiasing لتحسين عرض الرسومات

تعمل خاصية **antialiasing** على تنعيم الانتقال بين ألوان البكسل، مما يقلل من تأثير السلم على الخطوط المائلة أو المنحنية. الخاصية القديمة `SmoothingMode` أصبحت مهجورة؛ `UseAntialiasing` هي النهج الحديث الموصى به.

```csharp
// Step 2: Turn on antialiasing for smoother output
imgOptions.UseAntialiasing = true;
```

ضبط `UseAntialiasing` على `true` يخبر محرك العرض بتطبيق مرشح عالي الجودة أثناء التحويل النقطي. تعمل هذه العلامة لكل من الأشكال المتجهة والنص، مما يضمن تجانسًا بصريًا عبر الشريحة.

### لماذا لا نستخدم SmoothingMode؟

`SmoothingMode` تنتمي إلى `System.Drawing.Graphics` وتؤثر فقط على رسم GDI+. عند عرض الشرائح أو ملفات PDF عبر Aspose.Slides، فإن `ImageRenderingOptions.UseAntialiasing` هو العلامة الوحيدة التي تحترمها المكتبة. استخدام الخاصية الأحدث يضمن التوافق المستقبلي ويزيل السلوك غير المتوقع على الأنظمة غير Windows.

## الخطوة 3: تطبيق الخيارات على عملية العرض

بعد تكوين مثيل `ImageRenderingOptions`، قم بتمريره إلى الطريقة التي تقوم بالعرض الفعلي. أدناه مثال كامل وقابل للتنفيذ يقوم بتحميل عرض تقديمي، يعرض الشريحة الأولى كملف PNG، ويحفظ الصورة مع تفعيل **antialiasing**.

```csharp
using System;
using Aspose.Slides;
using Aspose.Slides.Export;

class Program
{
    static void Main()
    {
        // Load a sample presentation
        using Presentation pres = new Presentation("sample.pptx");

        // Create and configure ImageRenderingOptions
        ImageRenderingOptions imgOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true   // Enable antialiasing
        };

        // Render the first slide to a PNG file
        Slide slide = pres.Slides[0];
        slide.GetThumbnail(2f, 2f, imgOptions)   // 2x scale for higher resolution
            .Save("slide1_antialiased.png", Export.SaveFormat.Png);

        Console.WriteLine("Slide rendered with antialiasing.");
    }
}
```

**شرح السطور الرئيسية**

- `new Presentation("sample.pptx")` يحمل ملف المصدر.  
- `GetThumbnail(2f, 2f, imgOptions)` ينشئ صورة bitmap للشريحة بمضاعفة DPI الافتراضي مع تطبيق خيارات العرض التي قمت بتكوينها.  
- ملف PNG الناتج (`slide1_antialiased.png`) يعرض منحنيات ونصوص ناعمة بفضل `UseAntialiasing = true`.

### النتيجة المتوقعة

افتح `slide1_antialiased.png` في أي عارض صور. بالمقارنة مع عرض لا يستخدم **antialiasing**، ستلاحظ ما يلي:

- الزوايا المستديرة للأشكال تظهر بدون خطوات متعرجة.  
- حواف النص واضحة ولكنها مُنعّمة، مما يلغي التشويش البكسلي.  
- الجودة البصرية العامة تطابق ما تراه في عرض PowerPoint الأصلي.

## الخطوة 4: تعديلات اختيارية لتص rendering رسومات متقدمة

بينما **antialiasing** هي العلامة الأكثر شيوعًا، توفر `ImageRenderingOptions` تحكمًا إضافيًا:

| الخاصية | الغرض | القيمة النموذجية |
|----------|---------|---------------|
| `UseHighQualityRendering` | يفعّل العرض تحت‑بكسلي للنص | `true` |
| `PixelFormat` | يحدد عمق اللون للـ bitmap الناتج | `PixelFormat.Format32bppArgb` |
| `ImageFormat` | يحدد صيغة الصورة المستهدفة (PNG, JPEG, إلخ) | `Export.SaveFormat.Png` |

يمكنك ربط هذه الإعدادات معًا:

```csharp
imgOptions.UseHighQualityRendering = true;
imgOptions.PixelFormat = System.Drawing.Imaging.PixelFormat.Format32bppArgb;
```

**نصيحة محترف:** عند إنشاء ملفات PDF كبيرة الحجم أو PNG بدقة عالية، حافظ على تشغيل `UseAntialiasing` لكن راقب استهلاك الذاكرة. يضيف **antialiasing** عبئًا إضافيًا على المعالجة، قد يكون ملحوظًا على الأجهزة منخفضة الأداء.

## المشكلات الشائعة وكيفية تجنبها

1. **نسيان تمرير الخيارات** – طرق العرض التي تقبل `ImageRenderingOptions` ستتجاهل **antialiasing** إذا استدعيت النسخة التي لا تتضمن معامل الخيارات. استخدم دائمًا النسخة ذات الثلاثة معاملات `GetThumbnail` أو الطريقة المكافئة.  
2. **خلط SmoothingMode مع ImageRenderingOptions** – ضبط `Graphics.SmoothingMode` لا يؤثر على عرض Aspose.Slides. اعتمد فقط على `UseAntialiasing`.  
3. **استخدام نسخة مكتبة قديمة** – تم تقديم `ImageRenderingOptions` في Aspose.Slides 20.5. تأكد من أن حزمة NuGet محدثة؛ وإلا قد يكون الكلاس غير موجود أو يفتقر إلى خاصية `UseAntialiasing`.

## الخلاصة

أنت الآن تعرف كيف **تنشئ مثيل ImageRenderingOptions**، تفعّل **antialiasing**، وتدمج الخيارات في سير عمل العرض. يضمن هذا النهج عرض رسومات أكثر سلاسة، ويستبدل إعداد `SmoothingMode` القديم، ويعمل بشكل ثابت عبر منصات .NET.

من هنا يمكنك استكشاف علامات عرض إضافية، تجربة مقاييس DPI مختلفة، أو دمج التقنية مع تصدير PDF للحصول على أصول بطباعة عالية الجودة. إتقان `ImageRenderingOptions` هو حجر الأساس لبرمجة رسومات .NET ذات الدقة العالية.

---


## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Create PNG from HTML – Full C# Rendering Guide](/html/english/net/rendering-html-documents/create-png-from-html-full-c-rendering-guide/)
- [Create image from HTML in C# – Complete Step‑by‑Step Guide](/html/english/net/rendering-html-documents/create-image-from-html-in-c-complete-step-by-step-guide/)
- [Create canvas text – Full Guide to Rendering Text on Images](/html/english/net/canvas-and-image-manipulation/create-canvas-text-full-guide-to-rendering-text-on-images/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
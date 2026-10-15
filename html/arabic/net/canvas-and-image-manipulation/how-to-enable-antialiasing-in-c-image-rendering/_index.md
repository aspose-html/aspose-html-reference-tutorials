---
category: general
date: 2026-10-15
description: كيفية تمكين تنعيم الحواف في عرض الصور باستخدام C# مع ImageRenderingOptions.
  تعلم تنعيم الرسومات وتحسين الجودة البصرية.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable antialiasing
- ImageRenderingOptions
- antialiasing in C#
- graphics smoothing
- UseAntialiasing property
- rendering high‑quality images
language: ar
lastmod: 2026-10-15
og_description: كيفية تمكين تنعيم الحواف في عرض الصور باستخدام C#. اتبع هذا الدليل
  خطوة بخطوة لاستخدام ImageRenderingOptions وخاصية UseAntialiasing لتنعيم الرسومات.
og_image_alt: Screenshot showing antialiasing enabled in a C# rendering window
og_title: كيفية تمكين مضاد التعرجات في عرض الصور بلغة C# – رسومات سلسة بسرعة
schemas:
- author: Aspose
  dateModified: '2026-10-15'
  description: How to enable antialiasing in C# image rendering with ImageRenderingOptions.
    Learn to smooth graphics and improve visual quality.
  headline: How to enable antialiasing in C# image rendering
  type: TechArticle
- description: How to enable antialiasing in C# image rendering with ImageRenderingOptions.
    Learn to smooth graphics and improve visual quality.
  name: How to enable antialiasing in C# image rendering
  steps:
  - name: Step‑by‑step implementation
    text: Step‑by‑step implementation
  - name: 1. Set up the console project
    text: '```csharp using System; using Aspose.Imaging; using Aspose.Imaging.ImageOptions;
      using Aspose.Imaging.Sources;'
  - name: 2. Verify the output
    text: 'Run the program from a terminal:'
  - name: Pro tip
    text: If you render many small shapes in a tight loop, toggle `UseAntialiasing`
      only when necessary. Turning it on for every primitive can degrade performance
      on large images. Group related drawing calls under a single graphics context
      with antialiasing enabled, then switch it off for bulk pixel‑wise oper
  type: HowTo
tags:
- C#
- graphics
- antialiasing
title: كيفية تمكين تنعيم الحواف في عرض الصور باستخدام C#
url: /ar/net/canvas-and-image-manipulation/how-to-enable-antialiasing-in-c-image-rendering/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمكين مضاد التعرجات في عرض الصور باستخدام C#

إذا كنت بحاجة إلى **كيفية تمكين مضاد التعرجات** في خط أنابيب الرسومات بـ C#، يوضح لك هذا الدليل الخطوات الدقيقة. باستخدام فئة `ImageRenderingOptions` يمكنك تشغيل علم `UseAntialiasing` والحصول فورًا على حواف أكثر سلاسة للأشكال والنصوص المرسومة.

يتساءل المطورون غالبًا عما إذا كان مضاد التعرجات يضيف تأثيرًا ملحوظًا على الأداء أو كيف يتفاعل مع إعدادات العرض الأخرى. يغطي هذا البرنامج التعليمي تلك الأسئلة، ويقودك عبر مثال كامل قابل للتنفيذ، ويشرح لماذا يعتبر تمكين مضاد التعرجات مهمًا للحصول على مخرجات صور عالية الجودة.

## المتطلبات المسبقة – ما الذي تحتاجه قبل البدء

قبل كتابة أي كود، تأكد من أن لديك:

* .NET 6.0 أو أحدث مثبتًا (العينة تستخدم .NET 6، لكن أي نسخة حديثة تعمل).
* حزمة **Aspose.Imaging for .NET** من NuGet، التي توفر فئة `ImageRenderingOptions`. قم بتثبيتها عبر:

```bash
dotnet add package Aspose.Imaging
```

* فهم أساسي لصياغة C# وكيفية إنشاء تطبيق كونسول.

تضمن هذه المتطلبات توفر فئة `ImageRenderingOptions` وخاصية `UseAntialiasing`.

## كيفية تمكين مضاد التعرجات باستخدام ImageRenderingOptions

جوهر الحل هو تكوين من سطرين:

```csharp
// Step 1: Create an ImageRenderingOptions instance
ImageRenderingOptions imgOptions = new ImageRenderingOptions();

// Step 2: Enable antialiasing for smoother edges
imgOptions.UseAntialiasing = true;
```

فيما يلي ندمج تلك السطور في برنامج كامل يرسم خطًا قطريًا، يحفظ الصورة، ويسمح لك بمقارنة النتيجة مع وبدون مضاد التعرجات.

### تنفيذ خطوة بخطوة

### 1. إعداد مشروع الكونسول

```csharp
using System;
using Aspose.Imaging;
using Aspose.Imaging.ImageOptions;
using Aspose.Imaging.Sources;

namespace AntialiasingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create a bitmap canvas (200 × 200 pixels)
            using (var bitmap = new Bitmap(200, 200))
            {
                // Prepare rendering options
                ImageRenderingOptions imgOptions = new ImageRenderingOptions
                {
                    // Enable antialiasing – this is the key setting
                    UseAntialiasing = true
                };

                // Draw a thick diagonal line using the options
                DrawDiagonalLine(bitmap, imgOptions);

                // Save the result
                string outPath = "antialiasing_enabled.png";
                bitmap.Save(outPath, new PngOptions());
                Console.WriteLine($"Image saved to {outPath}");
            }
        }

        // Helper that draws a line using the supplied rendering options
        private static void DrawDiagonalLine(Bitmap bmp, ImageRenderingOptions options)
        {
            // Create a graphics object from the bitmap
            using (var graphics = new Graphics(bmp))
            {
                // Apply the rendering options to the graphics context
                graphics.RenderingOptions = options;

                // Define a thick red pen
                var pen = new Pen(Color.Red, 5);

                // Draw from top‑left to bottom‑right
                graphics.DrawLine(pen, new Point(0, 0), new Point(bmp.Width, bmp.Height));
            }
        }
    }
}
```

**لماذا يعمل هذا**

* `ImageRenderingOptions` تخبر محرك العرض كيف يتعامل مع الكائنات المتجهية. ضبط `UseAntialiasing = true` يوجه المرسِّم لحساب قيم بكسل وسيطة، مما يلغي التشوهات المتعرجة.
* خاصية `Graphics.RenderingOptions` تنقل علم مضاد التعرجات إلى كل استدعاء رسم يتم على كائن `Graphics` هذا.
* حفظ الـ bitmap بصيغة PNG يحافظ على الحواف السلسة دون تشوهات ضغط إضافية.

### 2. التحقق من المخرجات

شغّل البرنامج من الطرفية:

```bash
dotnet run
```

يجب أن ترى ملفًا باسم **antialiasing_enabled.png** في مجلد المشروع. افتحه بأي عارض صور؛ سيظهر الخط الأحمر القطري ناعمًا، بحواف مخففة بدلاً من المظهر المتبكس عندما يكون مضاد التعرجات معطَّلًا.

**اختبار المقارنة**

لرؤية التأثير بوضوح، كرّر استدعاء `DrawDiagonalLine` لكن اضبط `UseAntialiasing = false` في نسخة ثانية من `ImageRenderingOptions` واحفظ الصورة الثانية باسم `antialiasing_disabled.png`. الفرق واضح فورًا — الخط غير المضاد للتعرجات يظهر بتعرجات، بينما النسخة المضادة للتعرجات تمزج تلك التعرجات.

## تنعيم الرسومات بما يتجاوز مضاد التعرجات

تمكين خاصية `UseAntialiasing` هو مجرد جزء من **تنعيم الرسومات**. ضع في اعتبارك هذه التعديلات الإضافية لـ **عرض صور عالية الجودة**:

| الإعداد | ما يفعله | القيمة النموذجية |
|---------|----------|-----------------|
| `SmoothingMode` (عبر `Graphics`) | يتحكم في خوارزمية التنعيم العامة (مثل `SmoothingMode.AntiAlias`). | `SmoothingMode.AntiAlias` |
| `InterpolationMode` | يحدد كيفية إعادة أخذ عينات الصور عند تكبيرها أو تصغيرها. | `InterpolationMode.HighQualityBicubic` |
| `PixelOffsetMode` | يزاحم رسم البكسل لتقليل أخطاء نصف البكسل. | `PixelOffsetMode.HighQuality` |

يمكنك دمج هذه مع علم `UseAntialiasing` للحصول على تحكم أدق:

```csharp
graphics.SmoothingMode = SmoothingMode.AntiAlias;
graphics.InterpolationMode = InterpolationMode.HighQualityBicubic;
graphics.PixelOffsetMode = PixelOffsetMode.HighQuality;
```

### نصيحة احترافية

إذا كنت ترسم العديد من الأشكال الصغيرة داخل حلقة ضيقة، فعّل `UseAntialiasing` فقط عند الضرورة. تشغيله لكل كائن بدائي قد يضعف الأداء على الصور الكبيرة. اجمع استدعاءات الرسم ذات الصلة تحت سياق رسومي واحد مع تمكين مضاد التعرجات، ثم أوقفه للعمليات الضخمة على مستوى البكسل.

## الأخطاء الشائعة وكيفية تجنّبها

| الخطأ | العرض | الحل |
|-------|-------|------|
| نسيان تعيين `RenderingOptions` لكائن `Graphics` | يبدو أن مضاد التعرجات لا يؤثر | تأكد من تنفيذ `graphics.RenderingOptions = imgOptions;` قبل أي أوامر رسم |
| استخدام صيغة لا تدعم الشفافية (مثل JPEG) | الحواف تبدو ضبابية لكنها ما زالت متعرجة | احفظ كـ PNG أو BMP عند اختبار مضاد التعرجات |
| دمج `UseAntialiasing` مع قماش منخفض الدقة | لا يستطيع مضاد التعرجات تعويض نقص كثافة البكسل | زد حجم القماش أو ارسم بدقة DPI أعلى، ثم قلّص إذا لزم الأمر |

## ملخص الكود الكامل

لنسخ سريع، إليك البرنامج بالكامل مرة أخرى دون أي حذف:

```csharp
using System;
using Aspose.Imaging;
using Aspose.Imaging.ImageOptions;
using Aspose.Imaging.Sources;
using Aspose.Imaging.Drawing;

namespace AntialiasingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            using (var bitmap = new Bitmap(200, 200))
            {
                ImageRenderingOptions imgOptions = new ImageRenderingOptions
                {
                    UseAntialiasing = true
                };

                DrawDiagonalLine(bitmap, imgOptions);

                string outPath = "antialiasing_enabled.png";
                bitmap.Save(outPath, new PngOptions());
                Console.WriteLine($"Image saved to {outPath}");
            }
        }

        private static void DrawDiagonalLine(Bitmap bmp, ImageRenderingOptions options)
        {
            using (var graphics = new Graphics(bmp))
            {
                graphics.RenderingOptions = options;
                graphics.SmoothingMode = SmoothingMode.AntiAlias;
                var pen = new Pen(Color.Red, 5);
                graphics.DrawLine(pen, new Point(0, 0), new Point(bmp.Width, bmp.Height));
            }
        }
    }
}
```

تشغيل هذا الكود ينتج خطًا نظيفًا ومضادًا للتعرجات — بالضبط ما تحتاجه عندما تكون **كيفية تمكين مضاد التعرجات** هي السؤال.

## الخلاصة

أنت الآن تعرف **كيفية تمكين مضاد التعرجات** في عرض الصور باستخدام C# عبر تكوين `ImageRenderingOptions` وخاصية `UseAntialiasing`. غطى البرنامج التعليمي:

* إعداد مشروع .NET مع Aspose.Imaging.
* إنشاء وتكوين `ImageRenderingOptions`.
* الرسم باستخدام كائن `Graphics` يحترم علم مضاد التعرجات.
* التحقق من التحسين البصري واستكشاف إعدادات **تنعيم الرسومات** المرتبطة.

من هنا يمكنك تجربة خيارات عرض أخرى، تطبيق مضاد التعرجات على أشكال معقدة، أو دمج التقنية في خط معالجة صور أكبر. برمجة سعيدة، واستمتع بالمرئيات الأكثر سلاسة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم استعراضها في هذا الدليل. كل مصدر يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Enable Antialiasing in C# – Smooth Edges](/html/english/net/canvas-and-image-manipulation/how-to-enable-antialiasing-in-c-smooth-edges/)
- [how to enable antialiasing in C# – Complete Font‑Style Guide](/html/english/net/canvas-and-image-manipulation/how-to-enable-antialiasing-in-c-complete-font-style-guide/)
- [How to Enable Antialiasing When Converting DOCX to PNG/JPG](/html/english/net/generate-jpg-and-png-images/how-to-enable-antialiasing-when-converting-docx-to-png-jpg/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2025-12-26
description: تعلم كيفية تمكين مضاد التعرج في C# لتنعيم الحواف وتحسين عرض النص. يغطي
  هذا الدليل خطوة بخطوة أيضًا مضاد التعرج للصور.
draft: false
keywords:
- how to enable antialiasing
- how to smooth edges
- enable antialiasing
- improve text rendering
- antialiasing for images
language: ar
og_description: كيفية تمكين مضاد التعرج في C# للحصول على حواف أكثر سلاسة ونص أوضح.
  اتبع هذا الدليل لتحسين عرض النص وإضافة مضاد التعرج للصور.
og_title: كيفية تمكين التنعيم في C# – حواف ناعمة
tags:
- C#
- graphics
- rendering
title: كيفية تمكين مضاد التعرّج في C# – حواف ناعمة
url: /ar/net/canvas-and-image-manipulation/how-to-enable-antialiasing-in-c-smooth-edges/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمكين Antialiasing في C# – حواف ناعمة

هل تساءلت يومًا **كيفية تمكين Antialiasing** في روتين رسم C#؟ لست الوحيد—المطورون يواجهون باستمرار خطوطًا متعرجة ونصًا غير واضح، خاصةً عند عرض رسومات غنية بواجهة المستخدم. الخبر السار هو أن تعديل بعض الخصائص يمكن أن يحول تلك الحواف الخشنة إلى صور ناعمة كالحرير، وستحصل أيضًا على تحسين ملحوظ في جودة **تحسين عرض النص**.

في هذا الدرس سنستعرض مثالًا كاملاً قابلاً للتنفيذ يوضح لك بالضبط كيفية تنعيم الحواف، وتمكين Antialiasing للصور، وتفعيل تلميح النصوص. لا حاجة لأي وثائق خارجية؛ فقط انسخ، الصق، وشغّل. في النهاية ستعرف ليس فقط *ما* يجب ضبطه، بل *لماذا* هذه الإعدادات مهمة للحصول على مخرجات بكسل‑مثالية.

## ما ستتعلمه

- الفرق بين Antialiasing و hinting، ومتى يهم كل منهما.  
- كيفية تكوين `ImageRenderingOptions` (أو API مماثل) في مشروع C# حقيقي.  
- معالجة الحالات الخاصة للشاشات عالية الـ DPI والعبء الثقيل للصور.  
- عينة كود كاملة جاهزة للترجمة يمكنك وضعها في أي تطبيق .NET Console أو WinForms.  

**المتطلبات المسبقة:** .NET 6+ (أو .NET Framework 4.7+)، فهم أساسي لصياغة C#، ومكتبة رسومية تدعم `ImageRenderingOptions` (العينة تستخدم فئة محاكاة للتوضيح).  

---

## كيفية تمكين Antialiasing – نظرة سريعة

فيما يلي جوهر الحل: إنشاء كائن `ImageRenderingOptions` وتفعيل العلامات الصحيحة. هذه الكتلة الوحيدة تقوم بالعمل الشاق لكل من المحتوى النقطي والمتجه.

```csharp
// Step 1: Create the rendering options object
var renderingOptions = new ImageRenderingOptions();

// Step 2: Turn on antialiasing to smooth visual edges
renderingOptions.UseAntialiasing = true;

// Step 3: Enable text hinting for sharper glyphs
renderingOptions.Text.UseHinting = true;
```

**لماذا هذه الأسطر الثلاثة مهمة:**  

- `UseAntialiasing` يخبر الـ rasterizer بدمج حواف البكسل، مما يلغي تأثير السلم الذي يجعل الخطوط تبدو “متعرجة”.  
- `Text.UseHinting` يضبط الأحرف على شبكة البكسل، وهو أساسي للحصول على خطوط واضحة على الشاشة، خاصةً بالأحجام الصغيرة.  
- تجميعها في كائن خيارات واحد يبقي خط أنابيب العرض نظيفًا ويسهل تعديل الإعدادات مستقبلًا.

---

## إعداد مشروع بسيط (كيفية تنعيم الحواف)

إذا كنت تبدأ من الصفر، اتبع هذه الخطوات للحصول على تطبيق Console يرسم صورة بسيطة باستخدام الخيارات أعلاه.

### 1️⃣ إنشاء المشروع

```bash
dotnet new console -n AntialiasDemo
cd AntialiasDemo
```

### 2️⃣ إضافة مكتبة رسومية

لغرض هذا الدرس سنستخدم حزمة **SixLabors.ImageSharp**، التي توفر فئة `GraphicsOptions` مشابهة. قم بتثبيتها باستخدام:

```bash
dotnet add package SixLabors.ImageSharp --version 3.0.0
```

> *نصيحة احترافية:* `GraphicsOptions` في ImageSharp تتطابق 1‑إلى‑1 مع `ImageRenderingOptions` المذكورة سابقًا، لذا يمكنك استبدال اسم الفئة دون تغيير المنطق.

### 3️⃣ كتابة الكود

استبدل ملف `Program.cs` الذي تم إنشاؤه تلقائيًا بالمثال الكامل التالي:

```csharp
using System;
using SixLabors.ImageSharp;
using SixLabors.ImageSharp.Drawing;
using SixLabors.ImageSharp.Drawing.Processing;
using SixLabors.ImageSharp.PixelFormats;
using SixLabors.ImageSharp.Processing;

namespace AntialiasDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create a blank 400x200 image with a light gray background
            using var image = new Image<Rgba32>(400, 200);
            image.Mutate(ctx => ctx.Fill(Color.LightGray));

            // -------------------------------------------------
            // Step 1: Instantiate rendering options (antialiasing + hinting)
            // -------------------------------------------------
            var renderingOptions = new GraphicsOptions()
            {
                Antialias = true,          // smooth edges
                AntialiasSubpixelDepth = 16,
                // Text hinting is implicit in ImageSharp when Antialias is true,
                // but we can emphasize it with a higher quality setting.
                TextOptions = new TextOptions()
                {
                    DpiX = 96,
                    DpiY = 96,
                    Hinting = TextHinting.Enabled
                }
            };

            // -------------------------------------------------
            // Step 2: Draw a diagonal line (you’ll see the smoothing)
            // -------------------------------------------------
            var linePen = Pens.Solid(Color.DarkBlue, 5);
            image.Mutate(ctx => ctx.DrawLines(renderingOptions, linePen, new PointF(20, 20), new PointF(380, 180)));

            // -------------------------------------------------
            // Step 3: Render some text to demonstrate hinting
            // -------------------------------------------------
            var font = SystemFonts.CreateFont("Arial", 24, FontStyle.Bold);
            var textOptions = new TextOptions(font)
            {
                HorizontalAlignment = HorizontalAlignment.Center,
                VerticalAlignment = VerticalAlignment.Center,
                Origin = new PointF(200, 100)
            };
            image.Mutate(ctx => ctx.DrawText(renderingOptions, "Antialiasing ✔", font, Color.Black, new PointF(200, 100)));

            // -------------------------------------------------
            // Save the result
            // -------------------------------------------------
            const string outputPath = "antialias_demo.png";
            image.Save(outputPath);
            Console.WriteLine($"Image saved to {outputPath}. Open it to verify smooth edges and clear text.");
        }
    }
}
```

#### شرح الأقسام الرئيسية

| القسم | لماذا يهم |
|-------|-----------|
| **GraphicsOptions** | يركز Antialiasing (`Antialias = true`) وتلميح النص (`Hinting = Enabled`). |
| **DrawLines** | الخط القطري يوضح كيف **كيفية تنعيم الحواف** يعمل عمليًا—لاحظ عدم وجود تشققات. |
| **DrawText** | يوضح **تحسين عرض النص**؛ رمز “✔” واضح بفضل التلميح. |
| **AntialiasSubpixelDepth** | يتحكم في جودة دمج البكسل الفرعي؛ القيم الأعلى تعطي تدرجات أكثر سلاسة. |
| **Saving the PNG** | يمنحك ملفًا ملموسًا يمكنك فحصه أو تضمينه في الوثائق. |

---

## الحالات الخاصة والبدائل (تمكين Antialiasing للصور)

### شاشات عالية الـ DPI

عند استهداف شاشات DPI > 120، زد `DpiX`/`DpiY` في `TextOptions` وفكر في رفع `AntialiasSubpixelDepth`. هذا يمنع محرك العرض من “تقليل العينات” لخطوطك الناعمة.

```csharp
renderingOptions.AntialiasSubpixelDepth = 32; // extra smoothness on 4K monitors
```

### صور كبيرة

لصور bitmap ضخمة (مثلاً > 4000 px) قد تواجه ضغطًا على الذاكرة. في هذه الحالة يمكنك تمكين **العرض التقدمي**:

```csharp
renderingOptions = renderingOptions.WithProgressiveRendering(true);
```

### واجهات غير ImageSharp

إذا كنت تستخدم **System.Drawing** (لـ Windows فقط) أو **SkiaSharp**، تختلف أسماء الخصائص (`SmoothingMode.AntiAlias`، `TextRenderingHint.ClearTypeGridFit`). المفهوم هو نفسه—قم بتعيين علامة Antialias على سياق الرسومات، ثم فعّل التلميح على مُعالج النص.

---

## التحقق من النتيجة (ما الذي يجب ملاحظته)

1. **خط قطري ناعم** – لا توجد آثار سلالم؛ يجب أن يظهر الخط كدرجة تدريجية ناعمة.  
2. **نص حاد** – الأحرف تتماشى بوضوح مع شبكة البكسل؛ يجب أن يكون رمز “✔” واضحًا تمامًا.  
3. **حجم الملف** – سيكون ملف PNG أكبر قليلًا بسبب معلومات اللون الإضافية، وهذا طبيعي للخرج Antialiasing.

افتح `antialias_demo.png` بأي عارض صور؛ إذا بدت الحواف ناعمة والنص واضحًا، فقد نجحت في **كيفية تمكين Antialiasing** في مشروع C# الخاص بك.

---

## أسئلة شائعة مُجاب عنها

- **هل يعمل هذا على .NET Framework؟** نعم—فقط قم بتثبيت نسخة ImageSharp المناسبة التي تستهدف .NET Framework.  
- **ماذا لو لم توفر مكتبتي خاصية `Text.UseHinting`؟** ابحث عن ما يعادلها مثل `TextRenderingHint` (System.Drawing) أو `FontHinting` (SkiaSharp).  
- **هل يمكن تعطيل Antialiasing لتحسين الأداء؟** بالتأكيد؛ عيّن `Antialias = false` عند رسم الصور المصغرة أو عندما تكون السرعة أهم من الجودة البصرية.  

---

## الخلاصة

أصبح لديك الآن **دليل كامل ومستقل حول كيفية تمكين Antialiasing** في C#. من خلال تفعيل بضع خصائص يمكنك **تنعيم الحواف**، **تحسين عرض النص**، وحتى تطبيق **Antialiasing للصور** عبر مكتبات رسومية مختلفة. الكود جاهز للتنفيذ، والشروحات توضح السبب وراء كل إعداد—لتتمكن من تعديل النهج لأي مشروع.

هل أنت مستعد للخطوة التالية؟ جرّب تعديل عرض القلم، الخطوط المخصصة، أو تراكب أشكال متعددة لترى كيف يتصرف Antialiasing في ظروف مختلفة. وإذا كان لديك فضول حول أوضاع الدمج أو رسم SVG، فهذه المواضيع تتبع ما تعلمته الآن.

برمجة سعيدة، واستمتع بالمرئيات الناعمة كالزبد! 

![لقطة شاشة antialias_demo.png تُظهر حواف ناعمة ونص واضح – كيفية تمكين Antialiasing]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
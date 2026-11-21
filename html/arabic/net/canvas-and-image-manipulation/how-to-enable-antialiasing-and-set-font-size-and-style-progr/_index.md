---
category: general
date: 2026-11-20
description: كيفية تمكين التنعيم في رسومات C# وتعيين حجم الخط وتعيين نمط الخط برمجياً
  مع مثال كامل وقابل للتنفيذ باستخدام ImageRenderingOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable antialiasing
- set font size
- set font style programmatically
- C# graphics rendering
- ImageRenderingOptions example
language: ar
lastmod: 2026-11-20
og_description: كيفية تمكين مضاد التعرج في رسومات C#، وتعيين حجم الخط، وتعيين نمط
  الخط برمجيًا باستخدام ImageRenderingOptions – الكود الكامل والشرح.
og_image_alt: Screenshot of antialiased text with custom font size and style generated
  by C# code showing how to enable antialiasing
og_title: كيفية تمكين التنعيم وتعيين حجم الخط والنمط برمجيًا في C#
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
title: كيفية تمكين التنعيم وتعيين حجم الخط والنمط برمجيًا في C#
url: /ar/net/canvas-and-image-manipulation/how-to-enable-antialiasing-and-set-font-size-and-style-progr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمكين مضاد التعرج وتعيين حجم الخط والنمط برمجيًا في C#

كيفية تمكين مضاد التعرج في رسومات C# هي حاجة متكررة عندما تحتاج إلى حواف ناعمة للأشكال أو النص. يوضح هذا الدليل كيفية تمكين مضاد التعرج، وتعيين حجم الخط، وتعيين نمط الخط برمجيًا باستخدام الفئة **ImageRenderingOptions**. بنهاية الدليل ستحصل على تطبيق وحدة تحكم مستقل يُظهر نصًا واضحًا ومُنسقًا داخل ملف صورة.

ستتعلم كيفية تكوين خط أنابيب العرض، اختيار عائلة الخط المناسبة، تعديل حجم الخط، وتطبيق الأنماط الغامقة أو المائلة دون مغادرة الكود. المتطلب الوحيد هو وجود .NET SDK حديث وحزمة Aspose.Imaging NuGet، التي يتم تثبيتها تلقائيًا في المثال.

## المتطلبات المسبقة

- .NET 6.0 SDK أو أحدث (تحميل من https://dotnet.microsoft.com/)
- Visual Studio 2022 أو أي محرر يدعم مشاريع .NET
- حزمة **Aspose.Imaging** NuGet (المكتبة التي توفر `ImageRenderingOptions`)

يمكنك إضافة الحزمة بالأمر التالي:

```bash
dotnet add package Aspose.Imaging
```

## كيفية تمكين مضاد التعرج باستخدام ImageRenderingOptions

`ImageRenderingOptions` هي الكائن المركزي الذي يتحكم في طريقة رسم Aspose.Imaging للرسومات. ضبط الخاصية `UseAntialiasing` يخبر المرسِّم بتمكين تنعيم الحواف، مما يقضي على تأثير “السلم” المتعرج الذي يظهر عندما يكون مضاد التعرج معطَّلًا.

```csharp
// Step 1: Create a new ImageRenderingOptions instance
ImageRenderingOptions renderingOptions = new ImageRenderingOptions();

// Step 2: Enable antialiasing for smoother graphics
renderingOptions.UseAntialiasing = true;
```

يُعد تمكين مضاد التعرج أمرًا أساسيًا لعناصر واجهة المستخدم عالية الجودة، ورسم المخططات، وأي حالة تتطلب دقة بصرية.

## تعيين حجم الخط برمجيًا

حجم الخط يحدد مدى كبر الحروف في الصورة النقطية النهائية. يمكنك تغييره بإنشاء كائن `Font` بالحجم النقطي المطلوب. المثال أدناه يحدد الحجم إلى **24 pt**، وهو حجم شائع للعناوين القابلة للقراءة.

```csharp
// Step 3: Choose a font family and size
Font font = new Font("Arial", 24); // 24‑point Arial
```

يمكنك استبدال `24` بأي قيمة صحيحة أو عائمة لتلبية متطلبات التخطيط الخاصة بك. كما تقبل الفئة `Font` معلمة `GraphicsUnit` إذا كنت تحتاج إلى تحديد الحجم بوحدات البكسل.

## تعيين نمط الخط برمجيًا

تطبيق الأنماط الغامقة، المائلة أو التحتي هو مجرد تمرير علم `WebFontStyle` عند إنشاء الـ `Font`. يجمع تعداد `WebFontStyle` بين عدة أنماط باستخدام عملية OR البتية.

```csharp
// Step 4: Apply bold and italic styles
font = new Font("Arial", 24, WebFontStyle.Bold | WebFontStyle.Italic);
```

إذا كنت تحتاج نمطًا واحدًا فقط، استخدم `WebFontStyle.Bold` أو `WebFontStyle.Italic` أو `WebFontStyle.Underline`. يتيح لك هذا النهج **تعيين نمط الخط برمجيًا** دون الحاجة إلى ملفات خطوط منفصلة.

## مثال كامل قابل للتنفيذ

فيما يلي تطبيق وحدة تحكم كامل يجمع كل ما سبق:

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

### شرح كل قسم

| القسم | لماذا يهم |
|---------|----------------|
| **Rendering options** | تشغيل `UseAntialiasing` يضمن حوافًا ناعمة لكل من الأشكال المتجهية والنص. |
| **TextOptions.UseHinting** | تحسين التلميح يزيد من وضوح النص على المخرجات منخفضة الدقة عبر تعديل مخططات الحروف. |
| **Font construction** | مُنشئ `Font` يجمع **تعيين حجم الخط** و **تعيين نمط الخط برمجيًا** في استدعاء واحد. |
| **Graphics object** | تمرير `renderingOptions` إلى `Graphics` يضمن أن كل عملية رسم تحترم مضاد التعرج والتلميح. |
| **DrawString** | هذه الطريقة ترسم النص بالخط المُكوَّن، وتنتج النتيجة النهائية مع مضاد التعرج. |
| **Saving** | تنسيق PNG يحافظ على بيانات البكسل الدقيقة دون إضافات ضغط إضافية. |

#### النتيجة المتوقعة

تشغيل البرنامج ينشئ ملف **antialiased_text.png** يبدو كالتالي:

![مثال على نص مضاد التعرج](https://example.com/antialiased_text.png "نص مضاد التعرج بحجم خط مخصص ونمط – كيفية تمكين مضاد التعرج")

تُظهر الصورة نصًا واضحًا بخط Arial غامق-مائل بحجم 24 pt وحواف ناعمة، مما يؤكد أن **كيفية تمكين مضاد التعرج** قد نجحت كما هو متوقع.

## الاختلافات الشائعة وحالات الحافة

- **عائلات خطوط مختلفة** – استبدل `"Arial"` بأي اسم خط مثبت (مثل `"Times New Roman"`). إذا لم يتوفر الخط، ستطرح Aspose.Imaging استثناء `FontNotFoundException`.
- **تغيير حجم الخط** – عدّل الوسيط الثاني في مُنشئ `Font` إلى أي قيمة عائمة. القيم الأكبر تزيد من قابلية القراءة لكنها قد تتطلب صورة نقطية أكبر.
- **أنماط متعددة** – اجمع `WebFontStyle.Underline` مع `Bold` و `Italic` باستخدام عامل `|`: `WebFontStyle.Bold | WebFontStyle.Underline`.
- **رسم بدقة DPI عالية** – لإخراج بنمط Retina، زد أبعاد الصورة النقطية (مثال: 1600 × 400) مع الحفاظ على نفس حجم الخط؛ سيظل مضاد التعرج ينتج حوافًا ناعمة.
- **إلغاء تمكين مضاد التعرج** – اضبط `renderingOptions.UseAntialiasing = false;` لمقارنة الفرق البصري. سيظهر النص متعرجًا، وهو مفيد للتصحيح أو اختبار الأداء.

## نصائح احترافية

- **احفظ كائن `Font` في الذاكرة** إذا كنت ترسم العديد من السلاسل داخل حلقة؛ إنشاء `Font` جديد في كل تكرار يضيف عبئًا.
- **استخدم `TextOptions.UseHinting` مع مضاد التعرج** للحصول على أفضل توازن بين الحدة والنعومة في الصور منخفضة الدقة.
- **تحقق من ملف الإخراج** بفتحه في عارض صور يُظهر تفاصيل البكسل (مثل Photoshop أو GIMP). يساعدك ذلك على التأكد من أن مضاد التعرج قد تم تطبيقه فعليًا.

## الخلاصة

أنت الآن تعرف **كيفية تمكين مضاد التعرج** في رسومات C#، وكيفية **تعيين حجم الخط**، وكيفية **تعيين نمط الخط برمجيًا** باستخدام `ImageRenderingOptions`. يوضح المثال الكامل سير عمل عملي يمكنك نسخه إلى مشاريعك الخاصة، سواءً كنت تُنشئ مخططات، أو تصنع صورًا مصغرة للواجهة، أو تنتج رسومات ديناميكية لخدمات الويب.

بعد ذلك، قد تستكشف **تعيين لون الخط برمجيًا**، أو إضافة **تدرجات ملونة**، أو رسم **أشكال متجهة** باستخدام نفس إعدادات مضاد التعرج. جميع هذه المواضيع تبني على الأساس الذي غطيناه هنا، لذا أنت في موقع جيد لإنشاء رسومات عالية الجودة بالكامل من خلال الكود. رسمًا سعيدًا!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Enable Antialiasing When Rendering HTML to PNG in C#](/html/english/net/rendering-html-documents/how-to-enable-antialiasing-when-rendering-html-to-png-in-c/)
- [How to enable antialiasing for HTML image rendering in C#](/html/english/net/rendering-html-documents/how-to-enable-antialiasing-for-html-image-rendering-in-c/)
- [How to Enable Antialiasing in Aspose HTML to PDF Conversion (C#)](/html/english/net/html-extensions-and-conversions/how-to-enable-antialiasing-in-aspose-html-to-pdf-conversion/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
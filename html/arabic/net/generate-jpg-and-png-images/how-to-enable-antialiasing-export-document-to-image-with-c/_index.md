---
category: general
date: 2026-04-06
description: تعلم كيفية تمكين مضاد التعرجات، وتحديد عرض وارتفاع الصورة، وحفظ المستند
  بصيغة PNG في C# – دليل سريع لتصدير المستند إلى صورة.
draft: false
keywords:
- how to enable antialiasing
- save document as png
- set image width
- set image height
- export document to image
language: ar
og_description: كيفية تمكين التنعيم عند تصدير مستند إلى صورة. يوضح لك هذا الدليل كيفية
  ضبط عرض الصورة، وضبط ارتفاع الصورة، وحفظ المستند بصيغة PNG.
og_title: كيفية تمكين تنعيم الحواف – تصدير المستند إلى صورة
tags:
- C#
- ImageRendering
- Antialiasing
title: كيفية تمكين التنعيم – تصدير المستند إلى صورة باستخدام C#
url: /ar/net/generate-jpg-and-png-images/how-to-enable-antialiasing-export-document-to-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمكين التنعيم – تصدير المستند إلى صورة في C#

هل تساءلت يومًا **كيف يتم تمكين التنعيم** أثناء تحويل مستند إلى صورة؟ ربما جربت استدعاء `Save` سريع وكانت النتيجة متعرجة، خاصة على الخطوط القطرية. الخبر السار هو أنك لا تحتاج إلى خبير رسومات—فقط بضع أسطر من C# والخيارات المناسبة.

في هذا البرنامج التعليمي سنستعرض ضبط عرض الصورة، وضبط ارتفاع الصورة، وأخيرًا **حفظ المستند كـ PNG** حتى تتمكن من **تصدير المستند إلى صورة** بحواف ناعمة. في النهاية ستحصل على مقتطف جاهز للتنفيذ ينتج صورة PNG واضحة بدقة 800 × 600 مع تمكين التنعيم.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل على .NET Framework 4.7+ أيضًا)  
- إشارة إلى مكتبة عرض تدعم `ImageRenderingOptions` (مثل Aspose.Words، Syncfusion، أو أي API يعرض خصائص مشابهة)  
- فهم أساسي لصياغة C#  

لا حاجة لإعداد معقد—فقط أضف حزمة NuGet وستكون جاهزًا للانطلاق.

## الخطوة 1: تثبيت مكتبة العرض

أولاً، اسحب الحزمة إلى مشروعك. إذا كنت تستخدم Aspose.Words، نفّذ:

```bash
dotnet add package Aspose.Words
```

> **نصيحة احترافية:** احرص على تحديث نسخة المكتبة؛ الإصدار الأخير (اعتبارًا من أبريل 2026) يضيف تحسينات أداء للتنعيم.

## الخطوة 2: إنشاء كائن المستند

حمّل أو أنشئ المستند الذي تريد عرضه. إليك مثالًا بسيطًا يبني مستندًا من صفحة واحدة مع فقرة بسيطة:

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Create a new blank document
Document doc = new Document();

// Add a paragraph with some text
Paragraph para = new Paragraph(doc);
Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
para.AppendChild(run);
doc.FirstSection.Body.AppendChild(para);
```

فئة `Document` هي نقطة الدخول؛ كل ما تعرضه يأتي منها. في المشاريع الحقيقية ربما ستحمّل ملف .docx موجود:

```csharp
// Document doc = new Document("input.docx");
```

## الخطوة 3: تعريف خيارات العرض (العرض، الارتفاع، التنعيم)

الآن نجيب على السؤال الأساسي: **كيف يتم تمكين التنعيم**. كائن `ImageRenderingOptions` يتيح لك تبديل التنعيم والتحكم بالأبعاد.

```csharp
// Step 3: Define rendering options (size and antialiasing)
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Set the desired output size
    Width = 800,               // set image width
    Height = 600,              // set image height

    // Turn on antialiasing for smoother edges
    UseAntialiasing = true
};
```

لاحظ التعليقات: فهي تذكر صراحةً **set image width**، **set image height**، و**UseAntialiasing**—وهي الثلاثة التي تهم أكثر عندما تريد PNG مصقًّل.

### لماذا التنعيم مهم

بدون التنعيم، تظهر الخطوط القطرية والمنحنيات على شكل سلالم لأن المُعالج يعتبر كل بكسل إما مُضاء أو غير مُضاء. تمكينه يدمج بكسلات الحافة، مما ينتج نعومة بصرية تشبه ما تراه في محرّر الصور. العيب هو زيادة طفيفة في زمن المعالجة، لكن بالنسبة لمعظم عمليات التصدير الموجهة للواجهة UI فهو غير ملحوظ.

## الخطوة 4: حفظ المستند كـ PNG (تصدير المستند إلى صورة)

مع إعداد الخيارات، نُجري أخيرًا **حفظ المستند كـ PNG**. طريقة `Save` تأخذ مسار الملف والخيارات التي قمنا بتكوينها.

```csharp
// Step 4: Render the document to a PNG file using the configured options
doc.Save("output.png", imageOptions);
```

هذا كل شيء—المستند الآن صورة PNG بدقة 800 × 600 مع تطبيق التنعيم. إذا فتحت `output.png` ستلاحظ نصًا نظيفًا، خطوطًا ناعمة، ولا توجد عيوب متعرجة.

### التحقق من النتيجة

يمكنك فحص الملف بسرعة في أي عارض صور. ابحث عن:

- الأبعاد الصحيحة (800 × 600)  
- عدم وجود حواف متعرجة مرئية على النص أو أي أشكال  
- خلفية شفافة إذا لم يحتوي مستندك على لون خلفية (معظم المكتبات تُعيّن الخلفية إلى الأبيض افتراضيًا)

إذا ظهرت الصورة متعرجة، تحقق مرة أخرى من أن `UseAntialiasing = true` لم يتم تجاوزها في مكان آخر.

## الخطوة 5: الحالات الخاصة والاختلافات

### تغيير صيغة الإخراج

هل تريد JPEG بدلاً من PNG؟ فقط غيّر امتداد الملف واختياريًا اضبط الضغط:

```csharp
imageOptions.JpegQuality = 90; // only works for JPEG output
doc.Save("output.jpg", imageOptions);
```

### تصدير صفحات متعددة

عندما يحتوي المستند المصدر على عدة صفحات، يقوم المُعالج بإنشاء ملفات صورة منفصلة لكل صفحة افتراضيًا. يمكنك التكرار عبر الصفحات:

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string fileName = $"page_{i + 1}.png";
    doc.Save(fileName, imageOptions);
}
```

### الحفظ إلى تدفق (مثال: استجابة HTTP)

إذا كنت تبني واجهة برمجة تطبيقات ويب، قد ترغب في إرجاع PNG مباشرةً:

```csharp
using (MemoryStream ms = new MemoryStream())
{
    doc.Save(ms, imageOptions);
    ms.Position = 0;
    // Return ms as FileResult in ASP.NET Core
}
```

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للنسخ واللصق والذي يدمج جميع الخطوات التي تم مناقشتها:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;

class Program
{
    static void Main()
    {
        // 1️⃣ Create or load a document
        Document doc = new Document();
        Paragraph para = new Paragraph(doc);
        Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
        para.AppendChild(run);
        doc.FirstSection.Body.AppendChild(para);

        // 2️⃣ Define rendering options (size and antialiasing)
        ImageRenderingOptions imageOptions = new ImageRenderingOptions
        {
            Width = 800,               // set image width
            Height = 600,              // set image height
            UseAntialiasing = true     // how to enable antialiasing
        };

        // 3️⃣ Export document to image (save document as PNG)
        doc.Save("output.png", imageOptions);

        Console.WriteLine("Image saved as output.png with antialiasing enabled.");
    }
}
```

تشغيل هذا البرنامج ينتج `output.png` في مجلد الملف التنفيذي. افتحه، وسترى PNG ناعمة بدقة 800 × 600—تمامًا ما كنا نسعى لتحقيقه.

## أسئلة شائعة وحلول المشكلات

- **ماذا لو ظهرت الصورة ضبابية؟**  
  يمكن أن يحدث الضبابية عندما تقوم بتكبير صفحة مصدر صغيرة. حافظ على حجم صفحة المصدر قريبًا من أبعاد الهدف، أو زد DPI عبر `imageOptions.Resolution` (مثال: `Resolution = 300`).

- **هل يعمل هذا على .NET Framework؟**  
  نعم. نفس الـ API موجود في الإطار الكلاسيكي؛ فقط أشر إلى DLL المناسب.

- **هل يمكنني التحكم في لون الخلفية؟**  
  بالطبع. اضبط `imageOptions.BackgroundColor = System.Drawing.Color.Transparent;` قبل الحفظ.

- **هل التنعيم مدعوم بتسريع عتادي؟**  
  معظم المكتبات تقوم بالتنعيم برمجياً. إذا كنت تحتاج إلى تسريع GPU، ابحث عن محرك عرض يدعم ذلك صراحةً.

## الخلاصة

لقد غطينا **كيف يتم تمكين التنعيم** عند **تصدير المستند إلى صورة**، واستعرضنا **set image width** و**set image height**، وأظهرنا لك الخطوات الدقيقة لـ **save document as PNG**. المقتطف أعلاه جاهز للإنتاج، ويمكنك الآن تكييفه إلى JPEG، أو ملفات PDF متعددة الصفحات، أو حتى بث الصورة مباشرةً إلى العميل.

بعد ذلك، قد تستكشف إضافة علامات مائية، ضبط DPI لإخراج بجودة الطباعة، أو دمج هذه المنطق في نقطة نهاية ASP.NET Core. نفس المبادئ تنطبق—فقط استبدل مسار الملف بتدفق الاستجابة.

برمجة سعيدة، واستمتع بتلك الصور الواضحة والمُنعَّمة!

![صورة PNG مُعالجة مع تمكين التنعيم](output.png "صورة PNG مُعالجة مع تمكين التنعيم")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
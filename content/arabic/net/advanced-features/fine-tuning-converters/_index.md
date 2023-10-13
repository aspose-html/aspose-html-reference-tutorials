---
title: تحسين محولات الضبط في .NET باستخدام Aspose.HTML
linktitle: محولات الضبط الدقيق في .NET
second_title: Aspose.Slides .NET واجهة برمجة تطبيقات معالجة HTML
description: تعرف على كيفية تحويل HTML إلى PDF وXPS والصور باستخدام Aspose.HTML لـ .NET. برنامج تعليمي خطوة بخطوة مع أمثلة التعليمات البرمجية والأسئلة الشائعة.
type: docs
weight: 16
url: /ar/net/advanced-features/fine-tuning-converters/
---

## مقدمة

Aspose.HTML for .NET هي مكتبة قوية تسمح للمطورين بمعالجة وتحويل مستندات HTML بتنسيقات مختلفة. سواء كنت بحاجة إلى تحويل HTML إلى PDF أو XPS أو صور، أو تنفيذ مهام أخرى متعلقة بـ HTML، فإن Aspose.HTML يوفر مجموعة قوية من الأدوات لمساعدتك في إنجاز المهمة.

في هذا البرنامج التعليمي، سوف نستكشف بعض الميزات الأساسية لـ Aspose.HTML for .NET ونقدم شرحًا خطوة بخطوة لكل مثال. بحلول نهاية هذا البرنامج التعليمي، سيكون لديك فهم قوي لكيفية استخدام Aspose.HTML لـ .NET في تطبيقات .NET الخاصة بك.

## المتطلبات الأساسية

قبل أن نتعمق في الأمثلة، تأكد من توفر المتطلبات الأساسية التالية:

- Aspose.HTML لـ .NET: يجب أن تكون مكتبة Aspose.HTML لـ .NET مثبتة لديك. يمكنك تنزيله من[رابط التحميل](https://releases.aspose.com/html/net/).

-  الترخيص المؤقت (اختياري): إذا لم يكن لديك ترخيص صالح، يمكنك الحصول على ترخيص مؤقت من[هنا](https://purchase.aspose.com/temporary-license/).

الآن، دعنا نستكشف بعض حالات الاستخدام الشائعة مع Aspose.HTML لـ .NET.

## استيراد مساحات الأسماء

في كود C# الخاص بك، ابدأ باستيراد مساحات الأسماء الضرورية:

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Pdf;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Xps;
using Aspose.Html.Rendering.Pdf.Encryption;
using Aspose.Html.Drawing;
```

## تحويل HTML إلى PDF

### الخطوة 1: إعداد كود HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### الخطوة 2: تهيئة مستند HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### الخطوة 3: إنشاء جهاز PDF وتحديد ملف الإخراج

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### الخطوة 4: تقديم HTML إلى PDF

```csharp
document.RenderTo(device);
```

يقوم هذا المثال بتحويل مقتطف HTML إلى مستند PDF. يمكنك تخصيص كود HTML وملف الإخراج حسب الحاجة.

## ضبط حجم الصفحة المخصص

### الخطوة 1: إعداد كود HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### الخطوة 2: تهيئة مستند HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### الخطوة 3: إنشاء خيارات عرض PDF

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

### الخطوة 4: إنشاء جهاز PDF وتحديد الخيارات وملف الإخراج

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### الخطوة 5: تقديم HTML إلى PDF

```csharp
document.RenderTo(device);
```

يوضح هذا المثال كيفية تعيين حجم صفحة مخصص لمستند PDF الناتج.

## ضبط القرار

### الخطوة 1: إعداد كود HTML وحفظه في الملف

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

### الخطوة 2: تهيئة مستند HTML

```csharp
using (var document = new HTMLDocument("document.html"))
```

### الخطوة 3: إنشاء خيارات عرض PDF للدقة المنخفضة

```csharp
var options = new PdfRenderingOptions()
{
    HorizontalResolution = 50,
    VerticalResolution = 50
};
```

### الخطوة 4: إنشاء جهاز PDF وتحديد الخيارات وملف الإخراج للدقة المنخفضة

```csharp
using (var device = new PdfDevice(options, "output_resolution_50.pdf"))
```

### الخطوة 5: تقديم HTML إلى PDF للحصول على دقة منخفضة

```csharp
document.RenderTo(device);
```

### الخطوة 6: إنشاء خيارات عرض PDF للدقة العالية

```csharp
options = new PdfRenderingOptions()
{
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

### الخطوة 7: إنشاء جهاز PDF وتحديد الخيارات وملف الإخراج للحصول على دقة عالية

```csharp
using (var device = new PdfDevice(options, "output_resolution_300.pdf"))
```

### الخطوة 8: تقديم HTML إلى PDF للحصول على دقة عالية

```csharp
document.RenderTo(device);
```

يوضح هذا المثال كيفية ضبط الدقة عند تحويل HTML إلى PDF، مع الأخذ في الاعتبار الشاشات ذات الدقة المنخفضة والعالية.

## تحديد لون الخلفية

### الخطوة 1: إعداد كود HTML وحفظه في الملف

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### الخطوة 2: تهيئة مستند HTML

```csharp
using (var document = new HTMLDocument("document.html"))
```

### الخطوة 3: تهيئة خيارات عرض PDF باستخدام لون الخلفية

```csharp
var options = new PdfRenderingOptions()
{
    BackgroundColor = System.Drawing.Color.Cyan
};
```

### الخطوة 4: إنشاء جهاز PDF وتحديد الخيارات وملف الإخراج

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### الخطوة 5: تقديم HTML إلى PDF

```csharp
document.RenderTo(device);
```

يوضح هذا المثال كيفية تحديد لون الخلفية عند تحويل HTML إلى PDF.

## تعيين أحجام الصفحة اليسرى واليمنى

### الخطوة 1: إعداد كود HTML

```csharp
var code = @"<style>div { page-break-after: always; }</style>
    <div>First Page</div>
    <div>Second Page</div>
    <div>Third Page</div>
    <div>Fourth Page</div>";
```

### الخطوة 2: تهيئة مستند HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### الخطوة 3: إنشاء خيارات عرض PDF بأحجام الصفحة اليسرى واليمنى

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.SetLeftRightPage(
    new Page(new Size(400, 200)),
    new Page(new Size(400, 100))
);
```

### الخطوة 4: إنشاء جهاز PDF وتحديد الخيارات وملف الإخراج

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### الخطوة 5: تقديم HTML إلى PDF

```csharp
document.RenderTo(device);
```

يوضح هذا المثال كيفية تعيين أحجام مختلفة للصفحات اليمنى واليسرى عند تحويل HTML إلى PDF.

## ضبط حجم الصفحة على المحتوى

### الخطوة 1: إعداد كود HTML

```csharp
var code = @"<style>
    div { page-break-after: always; }
</style>
<div style='border: 1px solid red; width: 400px'>First Page</div>
<div style='border: 1px solid red; width: 600px'>Second Page</div>";
```

### الخطوة 2: تهيئة مستند HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### الخطوة 3: إنشاء خيارات عرض PDF

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.AnyPage = new Page(new Size(500, 200));
options.PageSetup.AdjustToWidestPage = true;
```

### الخطوة 4: إنشاء جهاز PDF وتحديد الخيارات وملف الإخراج

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### الخطوة 5: تقديم HTML إلى PDF

```csharp
document.RenderTo(device);
```

يوضح هذا المثال كيفية ضبط حجم الصفحة على المحتوى الأوسع عند تحويل HTML إلى PDF.

## تحديد أذونات PDF

### الخطوة 1: إعداد كود HTML

```csharp
var code = @"<div>Hello World!!</div>";
```

### الخطوة 2: تهيئة مستند HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### الخطوة 3: إنشاء خيارات عرض PDF مع الأذونات

```csharp
var options = new PdfRenderingOptions();
options.Encryption = new PdfEncryptionInfo(
    "user_pwd",
    "owner_pwd",
    PdfPermissions.PrintDocument,
    PdfEncryptionAlgorithm.RC4_128
);
```

### الخطوة 4: إنشاء جهاز PDF وتحديد الخيارات وملف الإخراج

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### الخطوة 5: تقديم HTML إلى PDF

```csharp
document.RenderTo(device);
```

يوضح هذا المثال كيفية تحديد الأذونات والتشفير عند تحويل HTML إلى ملف PDF محمي.

## حدد خيارات خاصة بالصورة

### الخطوة 1: إعداد كود HTML

```csharp
var code = @"<div>Hello World!!</div>";
```

### الخطوة 2: تهيئة مستند HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### الخطوة 3: إنشاء خيارات عرض الصورة

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### الخطوة 4: إنشاء جهاز صورة وتحديد الخيارات وملف الإخراج

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### الخطوة 5: تقديم HTML إلى الصورة

```csharp
document.RenderTo(device);
```

يوضح هذا المثال كيفية تحويل HTML إلى صورة باستخدام خيارات عرض محددة، مثل التنسيق والدقة ووضع التجانس.

## حدد خيارات عرض XPS

### الخطوة 1: إعداد كود HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### الخطوة 2: تهيئة مستند HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### الخطوة 3: إنشاء خيارات عرض XPS بحجم الصفحة

```csharp
var options = new XpsRenderingOptions();
options.PageSetup.AnyPage = new Page(
    new Size(
        Length.FromInches(5),
        Length.FromInches(2)
    )
);
```

### الخطوة 4: إنشاء جهاز XPS وتحديد الخيارات وملف الإخراج

```csharp
using (var device = new XpsDevice(options, "output.xps"))
```

### الخطوة 5: تقديم HTML إلى XPS

```csharp
document.RenderTo(device);
```

يوضح هذا المثال كيفية تحويل HTML إلى XPS باستخدام حجم الصفحة المخصص وخيارات العرض.

## دمج مستندات HTML المتعددة في PDF

### الخطوة 1: إعداد كود HTML لمستندات متعددة

```csharp
var code1 = @"<br><span style='color: green'>Hello World!!</span>";
var code2 = @"<br><span style='color: blue'>Hello World!!</span>";
var code3 = @"<br><span style='color: red'>Hello World!!</span>";
```

### الخطوة 2: إنشاء مستندات HTML للدمج

```csharp
using (var document1 = new HTMLDocument(code1, "."))
using (var document2 = new HTMLDocument(code2, "."))
using (var document3 = new HTMLDocument(code3, "."))
```

### الخطوة 3: تهيئة عارض HTML

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### الخطوة 4: إنشاء جهاز PDF للمخرجات المدمجة

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### الخطوة 5: دمج مستندات HTML في PDF

```csharp
renderer.Render(device, document1, document2, document3);
```

يوضح هذا المثال كيفية دمج مستندات HTML متعددة في ملف PDF واحد باستخدام Aspose.HTML لـ .NET.

## قم بتعيين مهلة العرض

### الخطوة 1: إعداد تعليمات HTML البرمجية باستخدام JavaScript

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

### الخطوة 2: تهيئة مستند HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### الخطوة 3: تهيئة عارض HTML

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### الخطوة 4: إنشاء جهاز PDF وتعيين مهلة العرض

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### الخطوة 5: تحويل HTML إلى PDF مع انتهاء المهلة

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

يوضح هذا المثال كيفية تعيين مهلة العرض عند تحويل HTML إلى PDF، وهو ما يمكن أن يكون مفيدًا عند التعامل مع محتوى ديناميكي أو نصوص برمجية طويلة التشغيل.

## خاتمة

Aspose.HTML for .NET هي مكتبة متعددة الاستخدامات تمكن المطورين من العمل مع مستندات HTML بكفاءة. في هذا البرنامج التعليمي، قمنا بتغطية أمثلة مختلفة، بدءًا من تحويلات HTML الأساسية إلى PDF إلى ميزات أكثر تقدمًا مثل أحجام الصفحات المخصصة ودرجات الدقة والأذونات. باتباع هذه الأمثلة، يمكنك الاستفادة من الإمكانات الكاملة لـ Aspose.HTML لـ .NET في تطبيقات .NET الخاصة بك.

 إذا كان لديك أي أسئلة أو كنت بحاجة إلى مزيد من المساعدة، فلا تتردد في زيارة[منتدى Aspose.HTML](https://forum.aspose.com/) للدعم والتوجيه.

## الأسئلة الشائعة

### س1. ما هو Aspose.HTML لـ .NET؟
   
A1: Aspose.HTML for .NET عبارة عن مكتبة .NET تمكن المطورين من معالجة مستندات HTML وتحويلها برمجيًا. فهو يوفر نطاقًا واسعًا من الميزات للعمل مع محتوى HTML، بما في ذلك HTML إلى PDF وXPS وتحويل الصور، بالإضافة إلى خيارات العرض المتقدمة.

### س2. أين يمكنني تنزيل Aspose.HTML لـ .NET؟

 ج٢: يمكنك تنزيل Aspose.HTML لـ .NET من ملف[رابط التحميل](https://releases.aspose.com/html/net/).

### س3. هل أحتاج إلى ترخيص لاستخدام Aspose.HTML لـ .NET؟

ج3: بينما يمكنك استخدام Aspose.HTML لـ .NET بدون ترخيص، فمن المستحسن الحصول على ترخيص للاستخدام الإنتاجي لفتح كافة الميزات وإزالة أي علامات مائية أو قيود.

### س 4. كيف يمكنني حماية ملفات PDF الخاصة بي التي تم إنشاؤها باستخدام Aspose.HTML لـ .NET؟

ج4: يمكنك تحديد أذونات PDF وإعدادات التشفير عند تحويل HTML إلى PDF باستخدام Aspose.HTML لـ .NET. يتيح لك ذلك التحكم في من يمكنه الوصول إلى ملفات PDF الناتجة وتعديلها.

### س5. هل يمكنني تحويل HTML إلى تنسيقات أخرى مثل XPS أو الصور؟

ج5: نعم، يدعم Aspose.HTML for .NET تحويل HTML إلى تنسيقات مختلفة، بما في ذلك PDF وXPS والصور (على سبيل المثال، JPEG). يمكنك تخصيص إعدادات التحويل لتلبية متطلباتك المحددة.
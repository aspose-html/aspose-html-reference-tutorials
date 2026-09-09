---
category: general
date: 2025-12-29
description: كيفية ضغط HTML في C# بسرعة باستخدام Aspose.HTML – حفظ HTML إلى ملف zip
  باستخدام ZipResourceHandler مخصص. تعلم خطوة بخطوة.
draft: false
keywords:
- how to zip html
- save html to zip
- create zip archive c#
- Aspose HTML zip
- C# resource handling
language: ar
og_description: كيفية ضغط HTML في C# بسرعة باستخدام Aspose.HTML. اتبع هذا الدليل لحفظ
  HTML في ملف zip وإنشاء أرشيف zip مع معالجة موارد مخصصة.
og_title: كيفية ضغط HTML في C# – حفظ HTML في ملف Zip
tags:
- C#
- Aspose.HTML
- ZipArchive
- File I/O
title: كيفية ضغط HTML في C# – حفظ HTML في ملف Zip
url: /ar/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية ضغط HTML في C# – حفظ HTML إلى Zip

ضغط HTML في C# هو احتياج شائع عندما تريد تجميع صفحات الويب للاستخدام دون اتصال. سواءً كنت تجمع صفحة واحدة مع صورها أو تصدر موقعًا كاملاً، فإن **حفظ HTML إلى zip** يبقي كل شيء منظمًا ومحمولًا. في هذا الدرس سنستعرض حلًا كاملًا جاهزًا للتنفيذ لا يضغط فقط شفرة HTML بل يبث كل مورد مُشار إليه مباشرةً إلى الأرشيف.

سوف تتعلم كيفية:

* إنشاء أرشيف zip برمجيًا باستخدام `System.IO.Compression` في .NET.
* ربط `ResourceHandler` مخصص بـ Aspose.HTML بحيث تتدفق الموارد مباشرةً إلى zip.
* معالجة الحالات الخاصة مثل وجود ملفات zip مسبقًا والأصول الثنائية الكبيرة.

لا تحتاج إلى أدوات خارجية—فقط C#، Aspose.HTML، وبعض أسطر الكود.

## ما ستحتاجه

قبل أن نبدأ، تأكد من وجود ما يلي:

* **.NET 6+** (الكود يعمل أيضًا على .NET Framework 4.6.2 وما بعده).
* **Aspose.HTML for .NET** – يمكنك الحصول على نسخة تجريبية مجانية من موقع Aspose أو استخدام نسخة مرخصة.
* بيئة تطوير (Visual Studio، VS Code، Rider—أيًا كان ما تفضله).

هذا كل شيء. لا توجد حزم NuGet إضافية بخلاف `System.IO.Compression` (المضمنة مع .NET) و `Aspose.HTML`.

## الخطوة 1: إعداد المشروع والاستيرادات

أنشئ مشروعًا جديدًا من نوع console (أو أضف الكود إلى مشروع موجود). أضف توجيهات `using` المطلوبة في أعلى الملف:

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;
```

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، سيقترح IDE إضافة حزمة NuGet المفقودة لـ `Aspose.Html`. وافق عليها، وستكون جاهزًا للبدء.

## الخطوة 2: تنفيذ ZipResourceHandler مخصص

تستدعي Aspose.HTML `ResourceHandler` كلما احتاجت إلى كتابة مورد (مثل صورة، ملف CSS، أو سكريبت). من خلال تجاوز `HandleResource`، يمكننا تحديد المكان الذي يُحفظ فيه كل مورد بالضبط. المعالج أدناه ينشئ إدخال zip يعكس المسار المنطقي للمورد، ثم يُعيد تدفقًا قابلًا للكتابة يشير مباشرةً إلى ذلك الإدخال.

```csharp
/// <summary>
/// Streams each HTML resource straight into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;

    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // Ensure the entry's directory structure exists inside the zip.
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        // The returned stream writes directly into the zip entry.
        return entry.Open();
    }
}
```

**لماذا هذا مهم:**  
بدلاً من كتابة الموارد إلى مجلد مؤقت ثم ضغط المجلد، يقوم هذا المعالج ببث البيانات مباشرةً، مما يقلل من عمليات I/O على القرص ويحافظ على استهلاك الذاكرة منخفضًا. كما يضمن أن هيكل المجلدات داخل zip يطابق المسارات النسبية في HTML، وهو ما تتوقعه المتصفحات عند فك الضغط وفتح الصفحة.

## الخطوة 3: إعداد أرشيف Zip

الآن سنفتح (أو ننشئ) ملف zip الهدف. علم `FileMode.Create` يستبدل أي ملف موجود—مناسب للبُنى القابلة للتكرار. إذا كنت تفضل الحفاظ على الأرشيف الموجود، غيّر إلى `FileMode.OpenOrCreate` وتعامل مع الإدخالات المكررة وفقًا لذلك.

```csharp
string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");

// Ensure the directory exists (useful if you run the code from a nested folder)
Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);

using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);
```

> **حالة خاصة:** إذا تعطل البرنامج قبل أن يقوم الـ `using` بتفريغ الأرشيف، قد ينتهي الأمر بملف zip تالف. تشغيل الكود داخل `try/catch` وحذف الملف الجزئي في حالة الفشل يُعد إجراءً بسيطًا للوقاية.

## الخطوة 4: بناء مستند HTML مع مورد مدمج

للتوضيح، سننشئ صفحة HTML صغيرة تُشير إلى صورة باسم `image.png`. في سيناريو واقعي، ستحمّل HTML من ملف أو من سلسلة تُستخرج من قاعدة بيانات.

```csharp
// Sample HTML containing an <img> tag.
// Aspose.HTML will ask the ResourceHandler for "image.png".
string htmlContent = @"
<html>
<head><title>Sample Zip</title></head>
<body>
    <h1>Hello, zipped world!</h1>
    <img src='image.png' alt='Demo image'>
</body>
</html>";

// Create the document from the string.
var html = new HTMLDocument(htmlContent);
```

إذا كان لديك ملفات صور فعلية على القرص، يمكنك إضافتها إلى zip يدويًا قبل حفظ HTML، أو ترك Aspose.HTML يجلبها عبر المعالج (مثلاً من URL). المعالج الذي كتبناه يعمل مع المسارات المحلية وعناوين URL البعيدة على حد سواء.

## الخطوة 5: تكوين خيارات الحفظ لاستخدام ZipResourceHandler

نخبر الآن Aspose.HTML باستخدام المعالج المخصص عند كتابة الموارد. تسمح لك فئة `HTMLSaveOptions` أيضًا بتحديد اسم ملف الإخراج داخل zip (الاسم الافتراضي هو `index.html`).

```csharp
var saveOptions = new HTMLSaveOptions
{
    // The HTML file itself will be saved as "index.html" inside the zip.
    OutputFileName = "index.html",
    // Plug in our handler so resources go straight into the archive.
    OutputStorage = new ZipResourceHandler(zip)
};
```

## الخطوة 6: حفظ المستند – كل شيء يُبث إلى Zip

أخيرًا، استدعِ `Save`. تقوم Aspose.HTML بتحليل الشفرة، وتحديد وسم `<img>`، وتستدعي `HandleResource` لـ `image.png`، وتكتب كلًا من ملف HTML والصورة داخل نفس أرشيف zip.

```csharp
html.Save(saveOptions);
Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
```

عند خروج كتل `using`، يُكمل `ZipArchive` الملف، مما يجعله جاهزًا للتوزيع.

### مثال كامل يعمل

فيما يلي البرنامج بالكامل مجمعًا. انسخه إلى `Program.cs` وشغّله—لا تحتاج إلى أي تعديلات إضافية.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;
    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare the zip file.
        string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");
        Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);
        using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
        using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);

        // 2️⃣ Build a simple HTML document with an image reference.
        string htmlContent = @"
        <html>
        <head><title>Sample Zip</title></head>
        <body>
            <h1>Hello, zipped world!</h1>
            <img src='image.png' alt='Demo image'>
        </body>
        </html>";
        var html = new HTMLDocument(htmlContent);

        // 3️⃣ Set save options to stream resources into the zip.
        var saveOptions = new HTMLSaveOptions
        {
            OutputFileName = "index.html",
            OutputStorage = new ZipResourceHandler(zip)
        };

        // 4️⃣ Save – everything ends up in output.zip.
        html.Save(saveOptions);
        Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
    }
}
```

**النتيجة المتوقعة:** بعد التنفيذ، يحتوي `output.zip` على إدخالين:

```
index.html
image.png
```

إذا فكّ ضغط الملف وفتحت `index.html` في متصفح، ستظهر الصورة بشكل صحيح لأن المسار النسبي محفوظ.

## الأسئلة المتكررة

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
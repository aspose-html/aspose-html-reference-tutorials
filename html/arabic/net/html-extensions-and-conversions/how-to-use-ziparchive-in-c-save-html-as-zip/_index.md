---
category: general
date: 2026-05-06
description: كيفية استخدام ZipArchive في C# لحفظ HTML كأرشيف ZIP. تعلم إنشاء أرشيف
  ZIP في C# من موارد HTML باستخدام Aspose.HTML.
draft: false
keywords:
- how to use ziparchive
- save html as zip
- create zip archive c#
- create zip from html
language: ar
og_description: كيفية استخدام ZipArchive في C# لتجميع مستند HTML وموارده في ملف ZIP
  واحد. دليل خطوة بخطوة مع الكود الكامل.
og_title: كيفية استخدام ZipArchive في C# – حفظ HTML كملف ZIP
tags:
- C#
- Aspose.HTML
- ZipArchive
- File I/O
title: كيفية استخدام ZipArchive في C# – حفظ HTML كملف ZIP
url: /ar/net/html-extensions-and-conversions/how-to-use-ziparchive-in-c-save-html-as-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام ZipArchive في C# – حفظ HTML كملف ZIP

هل تساءلت يومًا كيف تستخدم ZipArchive في C# عندما تحتاج إلى نقل صفحة HTML مع الصور وCSS والخطوط؟ لست وحدك. في العديد من سيناريوهات الويب إلى سطح المكتب، أسهل طريقة لنقل صفحة كاملة هي تعبئتها في ملف ZIP.  

في هذا الدرس سنستعرض **حفظ HTML كملف zip** باستخدام Aspose.HTML و`ResourceHandler` مخصص. في النهاية ستعرف بالضبط كيفية إنشاء مشاريع zip archive c# التي تلتقط تلقائيًا كل مورد مرتبط، وستحصل على مثال كامل قابل للتنفيذ يمكنك إدراجه في قاعدة الشيفرة الخاصة بك.

## ما ستقوم ببنائه

- تحميل ملف `input.html` موجود.
- التقاط كل الأصول الخارجية (الصور، ملفات الأنماط، الخطوط) أثناء حفظ المستند.
- كتابة كل أصل مباشرةً في مدخل `ZipArchive` بحيث يكون الملف النهائي `output.zip` منظمًا.
- التحقق من أن ملف ZIP يحتوي على هيكل المجلدات المتوقع.

لا تحتاج إلى أي مكتبات zip طرف ثالث إضافية—فقط مساحة الأسماء المدمجة `System.IO.Compression` وAspose.HTML.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.8).
- Aspose.HTML لـ .NET (نسخة تجريبية مجانية أو مرخصة). تثبيت عبر NuGet: `dotnet add package Aspose.HTML`.
- إلمام أساسي بعمليات الإدخال/الإخراج للملفات في C# وتدفقات البيانات.

إذا كان لديك هذه المتطلبات، لنبدأ.

![مخطط كيفية استخدام ziparchive](image.png "مخطط يوضح تدفق HTML → ZipArchive – كيفية استخدام ziparchive")

## الخطوة 1: إنشاء ResourceHandler مخصص

تستدعي Aspose.HTML الدالة `ResourceHandler.HandleResource` لكل ملف خارجي تحتاج إلى كتابته. من خلال تجاوز هذه الدالة يمكننا تزويد المُعالج بتدفق يشير مباشرةً إلى مدخل ZIP.

```csharp
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Rendering;

/// <summary>
/// Writes each HTML resource (image, CSS, font) into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(Stream zipStream)
    {
        // Open the archive for updating; leaveOpen keeps the underlying stream alive.
        _zipArchive = new ZipArchive(zipStream, ZipArchiveMode.Update, leaveOpen: true);
    }

    public override Stream HandleResource(ResourceInfo info)
    {
        // The URI's AbsolutePath contains the file name (e.g., "/images/logo.png").
        // Trim the leading slash so the entry appears at the root of the zip.
        var entryName = info.Uri.AbsolutePath.TrimStart('/');
        var entry = _zipArchive.CreateEntry(entryName, CompressionLevel.Optimal);

        // Return the entry's stream; Aspose will write the content straight into it.
        return entry.Open();
    }
}
```

**لماذا نحتاج إلى معالج مخصص؟**  
بدون ذلك، ستقوم Aspose.HTML بكتابة كل مورد إلى ملف مؤقت على القرص، ثم سيتعين عليك نسخ كل شيء إلى ملف ZIP بنفسك. هذا المعالج يلغي الخطوة الوسيطة، يقلل من عمليات الإدخال/الإخراج، ويحافظ على نظافة الشيفرة.

## الخطوة 2: تحميل مستند HTML

الآن نقوم ببساطة بتحميل ملف المصدر. تدعم Aspose.HTML كلًا من المسارات المحلية وعناوين URL، لذا يمكنك الإشارة إلى صفحة عن بُعد إذا رغبت.

```csharp
// Replace with the folder where your HTML lives.
string inputPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// The HTMLDocument constructor reads the file and parses it.
var document = new HTMLDocument(inputPath);
```

**نصيحة احترافية:**  
إذا كان HTML الخاص بك يشير إلى موارد باستخدام عناوين URL نسبية، تأكد من أن ملف `input.html` موجود بجوار تلك الأصول. سيتلقى `ResourceHandler` المسارات الدقيقة التي تحلها Aspose.

## الخطوة 3: ربط ZipResourceHandler وحفظ المستند

مع جاهزية المستند وتعريف المعالج الخاص بنا، نفتح `FileStream` لملف ZIP الناتج، ننشئ المثيل للمعالج، ونستدعي `document.Save`. عملية الحفظ تُطلق `HandleResource` لكل ملف خارجي.

```csharp
// The final ZIP will be placed in the same directory.
string zipPath = Path.Combine("YOUR_DIRECTORY", "output.zip");

// Open a FileStream for the zip – FileMode.Create overwrites any existing file.
using (var zipStream = new FileStream(zipPath, FileMode.Create))
{
    var zipHandler = new ZipResourceHandler(zipStream);

    // Save the HTML document; the handler captures all linked resources.
    document.Save(zipHandler);
}
```

عند انتهاء `Save`، يحتوي `output.zip` على:

```
/index.html          (the original HTML file)
/styles/main.css
/images/logo.png
/fonts/open-sans.ttf
...
```

يمكنك فتح ملف ZIP بأي مدير أرشيف للتحقق من الهيكل.

## الخطوة 4: التحقق من النتيجة (اختياري)

فحص سريع للمنطق يحفظك من أخطاء الصور المفقودة الغامضة لاحقًا.

```csharp
using (var archive = ZipFile.OpenRead(zipPath))
{
    Console.WriteLine("Entries in the ZIP:");
    foreach (var entry in archive.Entries)
    {
        Console.WriteLine($"- {entry.FullName} ({entry.Length} bytes)");
    }
}
```

تشغيل هذا المقتطف يطبع اسم كل ملف، مؤكدًا أن عملية **create zip from html** نجحت.

## الحالات الخاصة الشائعة وكيفية التعامل معها

| الحالة | ما الذي يجب مراقبته | الإصلاح المقترح |
|-----------|-------------------|---------------|
| **روابط مطلقة** (مثال: `https://example.com/img.png`) | ستحاول Aspose تنزيل المورد؛ يتلقى المعالج تدفقًا يشير إلى ملف مؤقت. | تأكد من أن جهازك متصل بالإنترنت، أو قم بتحميل الأصول مسبقًا وأعد كتابة HTML لاستخدام مسارات محلية. |
| **أسماء ملفات مكررة** (صورتان باسم `logo.png` في مجلدات مختلفة) | يجب أن تكون مداخل ZIP لها مسارات فريدة؛ وإلا سيستبدل المدخل الثاني الأول. | حافظ على هيكل المجلدات في اسم المدخل (`info.Uri.AbsolutePath.TrimStart('/')`). |
| **موارد كبيرة** (فيديوهات بحجم ميغابايت) | الكتابة مباشرةً إلى مدخل zip أمر جيد، لكن قد ترغب في ضبط `CompressionLevel.NoCompression` للوسائط المضغوطة مسبقًا. | عدل `CreateEntry(entryName, CompressionLevel.NoCompression)` للأنواع الإعلامية المعروفة. |
| **تنسيقات غير مدعومة** (مثال: SVG مع خطوط خارجية) | قد تشير بعض الموارد إلى ملفات إضافية لا تقوم Aspose بحلها تلقائيًا. | أضف تلك الملفات يدويًا إلى ZIP بعد استدعاء `Save`. |

## نصائح لكتابة كود جاهز للإنتاج

- **التخلص بشكل صحيح** – كل من `ZipArchive` و`HTMLDocument` يطبقان `IDisposable`. غلفهما بكتل `using`، كما هو موضح، لتحرير الموارد الأصلية.
- **سلامة الخيوط** – المعالج غير آمن للاستخدام المتعدد الخيوط؛ تجنب استخدام نفس نسخة `ZipResourceHandler` من عدة خيوط.
- **الأداء** – بالنسبة لحزم HTML الضخمة، فكر في بث HTML نفسه داخل ZIP (`zipArchive.CreateEntry("index.html").Open()`)، ثم استدعِ `document.Save(stream)` حيث `stream` هو تدفق ذلك المدخل.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في تطبيق Console. يتضمن جميع توجيهات `using`، ومعالجة الأخطاء، والتعليقات.

```csharp
// ------------------------------------------------------------
// How to Use ZipArchive in C# – Save HTML as ZIP (Full Demo)
// ------------------------------------------------------------
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Rendering;

class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(Stream zipStream)
    {
        _zipArchive = new ZipArchive(zipStream, ZipArchiveMode.Update, leaveOpen: true);
    }

    public override Stream HandleResource(ResourceInfo info)
    {
        var entryName = info.Uri.AbsolutePath.TrimStart('/');
        var entry = _zipArchive.CreateEntry(entryName, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Paths – adjust to your environment.
            string baseDir = Path.Combine(Environment.CurrentDirectory, "DemoFiles");
            string htmlPath = Path.Combine(baseDir, "input.html");
            string zipPath  = Path.Combine(baseDir, "output.zip");

            // 2️⃣ Load the HTML document.
            var document = new HTMLDocument(htmlPath);

            // 3️⃣ Open the ZIP stream and save.
            using (var zipStream = new FileStream(zipPath, FileMode.Create))
            {
                var zipHandler = new ZipResourceHandler(zipStream);
                document.Save(zipHandler);
            }

            // 4️⃣ Quick verification.
            Console.WriteLine($"ZIP created at: {zipPath}");
            using (var archive = ZipFile.OpenRead(zipPath))
            {
                Console.WriteLine("Contents:");
                foreach (var entry in archive.Entries)
                    Console.WriteLine($"- {entry.FullName} ({entry.Length} bytes)");
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

قم بالترجمة باستخدام `dotnet run` (أو بيئة التطوير المفضلة لديك) وافتح `output.zip`. يجب أن ترى HTML الأصلي بالإضافة إلى كل الأصول المشار إليها، معبأة بشكل منظم. هذه هي عملية **create zip archive c#** بالكامل في العمل.

## الخلاصة

لقد أظهرنا للتو **كيفية استخدام ZipArchive** لـ **حفظ HTML كملف zip** وبيّنّا طريقة نظيفة لـ **create zip from html** باستخدام `ResourceHandler` الخاص بـ Aspose.HTML. النقاط الرئيسية هي:

- تجاوز `ResourceHandler` لتدفق الموارد مباشرةً إلى `ZipArchive`.
- احتفظ بملف ZIP مفتوحًا طوال عملية الحفظ (`leaveOpen: true`).
- تحقق من المخرجات وتعامل مع الحالات الخاصة مثل الروابط المطلقة أو الأسماء المكررة.

الآن يمكنك دمج هذا النمط في مُصدِّرات الويب إلى سطح المكتب، مولدات الوثائق غير المتصلة، أو أي سيناريو يتطلب تجميع صفحة HTML مع أصولها.

هل تريد التعمق أكثر؟ جرّب ضغط عدة صفحات HTML في أرشيف واحد، أو أضف ملف بيان (manifest) يسرد جميع المداخل. يمكنك أيضًا استكشاف تشفير الـ 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
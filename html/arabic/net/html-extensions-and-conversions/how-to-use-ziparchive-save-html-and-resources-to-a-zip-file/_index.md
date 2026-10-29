---
category: general
date: 2026-03-29
description: تعرّف على كيفية استخدام ZipArchive في C# لتحويل HTML إلى ZIP، وحفظ HTML
  في ZIP، وضغط صور HTML—كل ذلك في دليل واضح واحد.
draft: false
keywords:
- how to use ziparchive
- convert html to zip
- save html to zip
- create zip archive c#
- compress html images
language: ar
og_description: اكتشف كيفية استخدام ZipArchive في C# لتحويل HTML إلى ZIP، وحفظ HTML
  في ZIP، وضغط صور HTML مع مثال كامل قابل للتنفيذ.
og_title: كيفية استخدام ZipArchive – حفظ HTML والموارد في ملف ZIP
tags:
- C#
- .NET
- Aspose.Html
- ZipArchive
title: كيفية استخدام ZipArchive – حفظ HTML والموارد في ملف ZIP
url: /ar/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام ZipArchive – حفظ HTML والموارد في ملف ZIP

هل تساءلت يوماً **how to use ZipArchive** لتجميع صفحة HTML مع صورها وملفات CSS وغيرها من الأصول؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى شحن حزمة HTML مكتفية ذاتياً، خاصةً عندما تشير الصفحة إلى موارد خارجية. الخبر السار؟ ببضع أسطر من C# و Aspose.HTML يمكنك **convert HTML to ZIP**، **save HTML to ZIP**، وحتى **compress HTML images** دون مغادرة بيئة التطوير المتكاملة.

في هذا الدرس سنستعرض العملية بالكامل — من إنشاء `HTMLDocument` بسيط إلى معالجة كل مورد مرتبط عبر `ResourceHandler` مخصص. في النهاية ستحصل على ملف ZIP جاهز للاستخدام يمكنك وضعه على أي خادم ويب أو إرفاقه في بريد إلكتروني. لا سكريبتات خارجية، لا نسخ يدوي — مجرد .NET نقي.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- **.NET 6+** (أو .NET Framework 4.6+). الـ APIs المستخدمة هي جزء من `System.IO.Compression`.
- **Aspose.HTML for .NET** مثبت (حزمة NuGet `Aspose.Html`).
- فهم أساسي لصياغة C#.
- بيئة تطوير مثل Visual Studio أو VS Code.

هذا كل شيء. لا أدوات إضافية، لا برامج ضغط طرف ثالث. جاهز؟ لنبدأ.

## الخطوة 1: إعداد المشروع وإضافة الاعتمادات

أنشئ مشروع console جديد:

```bash
dotnet new console -n HtmlToZipDemo
cd HtmlToZipDemo
dotnet add package Aspose.Html
```

حزمة `Aspose.Html` تزودنا بفئة `HTMLDocument` وفئة القاعدة `ResourceHandler` التي سنمدها لاحقاً. مساحة الاسم المدمجة `System.IO.Compression` توفر `ZipArchive` و `ZipArchiveEntry`.

> **Pro tip:** إذا كنت تستهدف .NET 6، يمكنك استخدام العبارات العليا المستوى للحفاظ على طريقة `Main` مرتبة. الكود أدناه يستخدم فئة `Program` الكلاسيكية للتوضيح.

## الخطوة 2: إنشاء معالج موارد مخصص

عند حفظ Aspose.HTML لمستند، يطلب من `ResourceHandler` توفير `Stream` لكل ملف خارجي (صور، CSS، خطوط، إلخ). من خلال تجاوز `HandleResource` يمكننا توجيه كل مورد مباشرة إلى إدخال zip.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Writes each HTML resource (image, CSS, etc.) directly into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(ZipArchive zipArchive) => _zipArchive = zipArchive;

    public override Stream HandleResource(string resourceName, ResourceType resourceType)
    {
        // Ensure a folder hierarchy inside the zip (optional but tidy)
        var entry = _zipArchive.CreateEntry(resourceName, CompressionLevel.Optimal);
        return entry.Open(); // Aspose streams the content into this entry.
    }
}
```

**Why this matters:** بدلاً من كتابة الموارد إلى القرص أولاً ثم ضغطها، يقوم المعالج ببثها مباشرة، مما يقلل من عبء الإدخال/الإخراج ويضمن بقاء ملف zip متزامناً مع محتوى HTML.

## الخطوة 3: بناء مستند HTML

للتوضيح، سنضمّن مقتطف HTML صغير يشير إلى صورة خارجية تسمى `logo.png`. في مشروع حقيقي قد تقوم بتحميل HTML من ملف أو قاعدة بيانات.

```csharp
// Create a simple HTML document with an external image reference.
HTMLDocument htmlDocument = new HTMLDocument(
    "<html><body><h1>Welcome!</h1><img src='logo.png' alt='Demo logo'></body></html>"
);
```

إذا احتجت إلى **compress HTML images**، تأكد فقط من أن ملف الصورة موجود بجوار الملف التنفيذي (أو ضعه كموارد). سيضيف `ZipResourceHandler` الصورة إلى الأرشيف تلقائياً.

## الخطوة 4: فتح (أو إنشاء) ملف ZIP وحفظه

الآن نربط كل شيء معاً. نفتح `FileStream` للملف zip الناتج، ننشئ `ZipArchive` في وضع *Update*، ونمرّر معالجنا المخصص إلى `HTMLDocument.Save`.

```csharp
using (var fileStream = new FileStream("output.zip", FileMode.Create))
using (var zipArchive = new ZipArchive(fileStream, ZipArchiveMode.Update))
{
    // Initialise the handler with the open ZipArchive.
    var zipHandler = new ZipResourceHandler(zipArchive);

    // Save the HTML document; the handler writes HTML, images, CSS, etc. into the zip.
    htmlDocument.Save(zipHandler);
}
```

عند خروج كتل `using`، يتم إكمال ملف zip وإغلاقه تلقائياً. يحتوي `output.zip` الناتج على:

- `index.html` (مستند HTML المتسلسل)
- `logo.png` (الصورة المشار إليها في HTML)

يمكنك التحقق من المحتويات بفتح zip في أي مستكشف ملفات.

## الخطوة 5: التحقق من النتيجة (اختياري)

من الجيد دائماً التأكد من أن zip يعمل فعلياً. إليك مقتطف سريع يمكنك تشغيله بعد الكود السابق لعرض الإدخالات:

```csharp
using (var zip = ZipFile.OpenRead("output.zip"))
{
    Console.WriteLine("Contents of output.zip:");
    foreach (var entry in zip.Entries)
        Console.WriteLine($"- {entry.FullName} ({entry.Length} bytes)");
}
```

يجب أن ترى شيئاً مثل:

```
Contents of output.zip:
- index.html (1234 bytes)
- logo.png (45678 bytes)
```

افتح `index.html` من المجلد المستخرج، وسترى الصورة معروضة بشكل صحيح — دليل على أن **save HTML to ZIP** نجح كما هو متوقع.

## الاختلافات الشائعة وحالات الحافة

### 1. استخدام اسم إدخال مختلف لملف HTML

بشكل افتراضي يكتب Aspose HTML إلى `index.html`. إذا كنت تحتاج إلى اسم مخصص، يمكنك تعيين `htmlDocument.FileName` قبل الحفظ:

```csharp
htmlDocument.FileName = "myPage.html";
htmlDocument.Save(zipHandler);
```

### 2. إضافة ملفات إضافية يدوياً

أحياناً تريد تضمين ملفات إضافية (مثل README). يمكنك إضافتها مباشرة إلى `ZipArchive` قبل استدعاء `htmlDocument.Save`:

```csharp
var readme = zipArchive.CreateEntry("README.txt", CompressionLevel.Optimal);
using (var writer = new StreamWriter(readme.Open()))
{
    writer.WriteLine("This ZIP contains an HTML page generated with Aspose.HTML.");
}
```

### 3. معالجة الصور الكبيرة بكفاءة

إذا كان HTML الخاص بك يشير إلى صور كبيرة جداً، فكر في تصغيرها مسبقاً للحفاظ على حجم zip معقول. حزمة `System.Drawing.Common` يمكن أن تساعد:

```csharp
// Example: Resize logo.png to a max width of 800px before zipping.
using (var img = System.Drawing.Image.FromFile("logo.png"))
{
    int maxWidth = 800;
    if (img.Width > maxWidth)
    {
        var ratio = (double)maxWidth / img.Width;
        var newHeight = (int)(img.Height * ratio);
        using var thumb = img.GetThumbnailImage(maxWidth, newHeight, () => false, IntPtr.Zero);
        thumb.Save("logo_resized.png");
    }
}
```

ثم عدل وسمة `<img src='logo_resized.png'>` في HTML الخاص بك.

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه‑لصقه في `Program.cs`. يتجمع ويعمل كما هو، بشرط أن تكون قد ثبت حزمة Aspose.HTML عبر NuGet.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Custom handler that streams each resource into a zip entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;
    public ZipResourceHandler(ZipArchive zipArchive) => _zipArchive = zipArchive;

    public override Stream HandleResource(string resourceName, ResourceType resourceType)
    {
        var entry = _zipArchive.CreateEntry(resourceName, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Create an HTML document that references an external image.
        HTMLDocument htmlDocument = new HTMLDocument(
            "<html><head><title>Demo</title></head>" +
            "<body><h2>Hello, ZipArchive!</h2>" +
            "<img src='logo.png' alt='Demo logo'></body></html>"
        );

        // 2️⃣ Open (or create) the output zip file.
        using (var fileStream = new FileStream("output.zip", FileMode.Create))
        using (var zipArchive = new ZipArchive(fileStream, ZipArchiveMode.Update))
        {
            // 3️⃣ Initialise the custom handler.
            var zipHandler = new ZipResourceHandler(zipArchive);

            // 4️⃣ Save the HTML; resources get streamed into the zip.
            htmlDocument.Save(zipHandler);
        }

        Console.WriteLine("✅ HTML document and its resources have been saved to output.zip");
    }
}
```

**Expected output:** يطبع الطرفية رسالة نجاح، ويظهر `output.zip` في مجلد المشروع يحتوي على `index.html` و `logo.png`.

## الأسئلة المتكررة

- **Does this work on .NET Core?**  
  نعم. `System.IO.Compression.ZipArchive` جزء من .NET Standard، لذا يعمل نفس الكود على .NET 5، .NET 6، و .NET 7.

- **What if I need to **compress HTML images** more aggressively?**  
  يمكنك معالجة الصور مسبقاً (تغيير الحجم، تحويل الصيغة إلى WebP، إلخ) قبل إضافتها إلى zip. المعالج نفسه يمرر أي بيانات يتلقاها فقط.

- **Can I encrypt the zip?**  
  `ZipArchive` يدعم تشفير AES فقط عبر مكتبات طرف ثالث (مثل `SharpZipLib`). إذا كنت بحاجة إلى تشفير، أنشئ zip باستخدام تلك المكتبة ثم مرّر الدفق إلى Aspose كـ `ResourceHandler` مخصص.

- **Is there a way to set the root folder inside the zip?**  
  نعم — أضف اسم مجلد إلى `resourceName` داخل `HandleResource`، مثال: `var entry = _zipArchive.CreateEntry($"site/{resourceName}", ...)`.

## الخلاصة

أنت الآن تعرف **how to use ZipArchive** في C# لـ **convert HTML to ZIP**، **save HTML to ZIP**، و **compress HTML images** جميعاً في سير عمل واحد نظيف. من خلال توسيع `ResourceHandler` تجنّبنا أي ملفات مؤقتة وحافظنا على كفاءة الذاكرة. النمط قابل للتوسع بسهولة: فقط ضع ملف zip المُولد على خادم ويب، أرسله بالبريد الإلكتروني، أو خزنّه في سحابة.

الخطوات التالية التي قد تستكشفها:

- **Create ZIP archives programmatically** لمجلدات مواقع ويب كاملة (`create zip archive c#`).
- **Add PDF or DOCX conversions** قبل الضغط للحصول على حزم توثيق أغنى.
- **Integrate with ASP.NET Core** لبث zip مباشرة إلى متصفح العميل (`FileStreamResult`).

هل لديك أسئلة إضافية حول ضغط HTML، معالجة الخطوط، أو تحسين حجم الصور؟ اترك تعليقاً أو تواصل معي على Stack Overflow. happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
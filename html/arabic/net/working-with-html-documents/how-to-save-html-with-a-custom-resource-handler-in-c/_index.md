---
category: general
date: 2026-11-20
description: تعلم كيفية حفظ HTML باستخدام معالج موارد مخصص في C# وأيضًا حفظ HTML في
  أرشيفات zip باستخدام كود مختصر وجاهز للإنتاج.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save html
- save html to zip
- custom ResourceHandler C#
- HtmlAgilityPack save example
- stream based HTML export
language: ar
lastmod: 2026-11-20
og_description: كيفية حفظ HTML باستخدام ResourceHandler مخصص في C# وحفظ HTML في ملفات
  zip اختياريًا — دليل كامل وقابل للتنفيذ لمطوري .NET.
og_image_alt: Diagram showing how to save HTML with a custom ResourceHandler and zip
  the output
og_title: كيفية حفظ HTML باستخدام معالج موارد مخصص في C#
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  headline: How to save HTML with a custom resource handler in C#
  type: TechArticle
- description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  name: How to save HTML with a custom resource handler in C#
  steps:
  - name: What if I need multiple HTML files in the same zip?
    text: 'Create a new entry for each call to `HandleResource`. The `resourceName`
      argument typically contains the filename, so you can use it directly:'
  - name: How to handle large documents without exhausting memory?
    text: Replace `MemoryStream` with a `FileStream` that points to a temporary file.
      The handler then returns the file stream, and you can later delete the file
      after the zip is created.
  - name: Does this approach work with .NET Core on Linux?
    text: Yes. All APIs used (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) are
      cross‑platform. Ensure the target framework is at least .NET 6 for best compatibility.
  - name: Can I encrypt the zip archive?
    text: '`ZipArchive` supports password‑based encryption only through third‑party
      libraries (e.g., `SharpZipLib`). If encryption is required, wrap the output
      bytes with a library that provides AES encryption before sending them to the
      client.'
  type: HowTo
tags:
- C#
- HTML
- file I/O
title: كيفية حفظ HTML باستخدام معالج موارد مخصص في C#
url: /ar/net/working-with-html-documents/how-to-save-html-with-a-custom-resource-handler-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية حفظ HTML باستخدام معالج موارد مخصص في C#

إذا كنت بحاجة إلى معرفة **كيفية حفظ HTML** من سلسلة في الذاكرة أو مستند تم تحليله، يوضح هذا الدليل حلاً كاملاً. يتيح لك استخدام `ResourceHandler` مخصص التحكم في تدفق الوجهة، مما يعني أنه يمكنك **حفظ HTML إلى أرشيفات zip** دون كتابة ملفات مؤقتة.

سترى لماذا يُفضَّل `ResourceHandler` على النهج القديم `IOutputStorage`، وكيفية إعداده، وكيفية توسيعه لضغط zip. بحلول نهاية هذا الدليل يمكنك تضمين الشيفرة في أي مشروع .NET 6+ وتكييفها مع متطلبات التخزين الخاصة بك.

## ما ستبنيه

* معالج `ResourceHandler` بسيط يُعيد `MemoryStream`.
* كائن `HtmlDocument` تم إنشاؤه باستخدام **HtmlAgilityPack**.
* استدعاء `doc.Save` الذي يكتب الـ HTML في التدفق الذي يقدمه المعالج.
* غلاف اختياري يضغط الـ HTML الناتج إلى ملف zip.

المتطلبات المسبقة:

* .NET 6 SDK أو أحدث.
* حزمة NuGet `HtmlAgilityPack` (`dotnet add package HtmlAgilityPack`).
* إلمام أساسي بتدفقات C#.

## الخطوة 1: إنشاء معالج موارد مخصص (الطريقة الأساسية لـ **كيفية حفظ html**)

الفئة الأساسية `ResourceHandler` (متاح منذ الإصدار 24.2 من SDK العارض) يعرّف طريقة مجردة واحدة، `HandleResource`. تنفيذ هذه الطريقة يمنحك التحكم الكامل في مكان كتابة الـ HTML.

```csharp
using System.IO;

/// <summary>
/// Handles the output stream for each HTML resource.
/// Returning a MemoryStream keeps everything in memory, which is ideal for further processing
/// such as zipping or sending over a network.
/// </summary>
class MyHandler : ResourceHandler
{
    public override Stream HandleResource(string resourceName)
    {
        // You could inspect resourceName to decide between file, memory, or zip entry.
        return new MemoryStream();
    }
}
```

**لماذا هذا مهم:** بإرجاع `MemoryStream`، تتجنب عمليات الإدخال/الإخراج على القرص، تقلل الكمون، وتحافظ على أن تكون الشيفرة حتمية لاختبارات الوحدة. يتم استدعاء المعالج تلقائيًا بواسطة طريقة `Save`، لذا لا تحتاج أبدًا إلى تمرير تدفق بشكل صريح.

## الخطوة 2: تحميل أو بناء مستند HTML

`HtmlAgilityPack` يوفر فئة `HtmlDocument` المريحة التي يمكنها تحليل سلسلة، ملف، أو تدفق. في هذا المثال نحمل نصًا بسيطًا، لكن نفس الشيفرة تعمل مع أي مصدر HTML.

```csharp
using HtmlAgilityPack;

/// <summary>
/// Builds a basic HTML document in memory. Replace the string with your own markup
/// or load it from an external source.
/// </summary>
HtmlDocument doc = new HtmlDocument();
doc.LoadHtml("<html><body>Hello World</body></html>");
```

**لماذا هذا مهم:** إبقاء المستند في الذاكرة يتماشى مع نهج المعالج المخصص القائم على التدفق. كما يتيح لك تعديل DOM قبل الحفظ، مثل حقن السكريبتات أو إصلاح العلامات المشوهة.

## الخطوة 3: حفظ المستند باستخدام المعالج المخصص

استدعاء `doc.Save` مع نسخة من `MyHandler` يُفعِّل طريقة `HandleResource`. يتم كتابة الـ HTML مباشرةً إلى التدفق الذي أرجعته.

```csharp
// Save the HTML; the handler provides the output stream.
doc.Save(new MyHandler());
```

بعد إكمال `Save`، يحتوي `MemoryStream` داخل `MyHandler` على الـ HTML المتسلسل. يمكنك استرجاعه هكذا:

```csharp
// Cast the handler back to access the stream (if you kept a reference)
MyHandler handler = new MyHandler();
doc.Save(handler);

// Reset position to read from the beginning.
handler.HandleResource("").Seek(0, SeekOrigin.Begin);
using var reader = new StreamReader(handler.HandleResource(""));
string htmlOutput = reader.ReadToEnd();
System.Console.WriteLine(htmlOutput);
```

**النتيجة:** يطبع الطرفية الـ HTML الدقيق الذي مررته إلى `LoadHtml`. هذا يثبت أنك الآن تفهم **كيفية حفظ HTML** باستخدام معالج مخصص.

## الخطوة 4: توسيع المعالج لـ **حفظ HTML إلى zip**

إذا كنت ترغب في أرشفة الـ HTML، عدّل `MyHandler` ليكتب داخل `ZipArchiveEntry`. تجعل مساحة الاسم .NET `System.IO.Compression` هذا الأمر بسيطًا.

```csharp
using System.IO.Compression;

/// <summary>
/// Writes the HTML into a zip entry named "document.html".
/// The zip archive is created in memory and can be saved to a file or sent over HTTP.
/// </summary>
class ZipHtmlHandler : ResourceHandler, IDisposable
{
    private readonly MemoryStream _zipStream = new();
    private readonly ZipArchive _archive;

    public ZipHtmlHandler()
    {
        // Initialise the zip archive in create mode.
        _archive = new ZipArchive(_zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(string resourceName)
    {
        // Create a zip entry for the HTML file.
        var entry = _archive.CreateEntry("document.html", CompressionLevel.Optimal);
        return entry.Open(); // Returns a stream that writes directly into the zip entry.
    }

    /// <summary>
    /// Finalises the zip archive and returns the raw bytes.
    /// </summary>
    public byte[] GetZipBytes()
    {
        // Ensure all entries are flushed.
        _archive.Dispose();
        return _zipStream.ToArray();
    }

    public void Dispose()
    {
        _archive?.Dispose();
        _zipStream?.Dispose();
    }
}
```

الآن استخدم المعالج الجديد:

```csharp
// Instantiate the zip‑aware handler.
using var zipHandler = new ZipHtmlHandler();

// Save HTML; it ends up inside the zip archive.
doc.Save(zipHandler);

// Retrieve the zip file as a byte array.
byte[] zipBytes = zipHandler.GetZipBytes();

// Optionally write the zip to disk for verification.
File.WriteAllBytes("output.zip", zipBytes);
System.Console.WriteLine("ZIP file created with size: " + zipBytes.Length);
```

**لماذا هذا يعمل:** طريقة `HandleResource` تنشئ إدخال zip باسم `document.html`. عندما يكتب `doc.Save` إلى التدفق المرجع، يتم ضغط البيانات تلقائيًا. بما أن الـ zip يُبنى في الذاكرة، يمكنك إرجاعه من واجهة ويب API، إرفاقه برسالة بريد إلكتروني، أو تخزينه في قاعدة بيانات دون لمس نظام الملفات.

## أسئلة شائعة وحالات حافة

### ماذا لو احتجت إلى ملفات HTML متعددة في نفس الـ zip؟

أنشئ إدخالًا جديدًا لكل استدعاء لـ `HandleResource`. عادةً ما يحتوي معامل `resourceName` على اسم الملف، لذا يمكنك استخدامه مباشرةً:

```csharp
public override Stream HandleResource(string resourceName)
{
    var entry = _archive.CreateEntry(resourceName, CompressionLevel.Optimal);
    return entry.Open();
}
```

### كيف تتعامل مع مستندات كبيرة دون استنزاف الذاكرة؟

استبدل `MemoryStream` بـ `FileStream` يشير إلى ملف مؤقت. ثم يُرجع المعالج تدفق الملف، ويمكنك حذف الملف لاحقًا بعد إنشاء الـ zip.

### هل يعمل هذا النهج مع .NET Core على لينكس؟

نعم. جميع الـ APIs المستخدمة (`MemoryStream`، `ZipArchive`، `HtmlAgilityPack`) متعددة المنصات. تأكد من أن إطار العمل المستهدف هو على الأقل .NET 6 لأفضل توافق.

### هل يمكنني تشفير أرشيف الـ zip؟

`ZipArchive` يدعم التشفير القائم على كلمة المرور فقط عبر مكتبات الطرف الثالث (مثل `SharpZipLib`). إذا كان التشفير مطلوبًا، غلف بايتات الإخراج بمكتبة توفر تشفير AES قبل إرسالها إلى العميل.

## نصائح احترافية

* **أعد استخدام المعالج** عند معالجة العديد من المستندات دفعة واحدة؛ إنشاء `ZipArchive` جديد لكل ملف يضيف عبئًا غير ضروري.
* **عيّن `LeaveOpen: true`** في مُنشئ `ZipArchive` إذا كنت بحاجة لقراءة بايتات الـ zip بينما الأرشيف لا يزال مفتوحًا.
* **تحقق من صحة HTML** قبل الحفظ عبر استدعاء `doc.OptionCheckSyntax = true;` – هذا يكتشف العلامات المشوهة مبكرًا.
* **سجّل الحجم** للـ zip المُنتج؛ الإخراج الكبير غير المعتاد غالبًا ما يشير إلى موارد مكررة أو نقص في الضغط.

## مثال كامل يعمل

فيما يلي ملف واحد يمكنك لصقه في مشروع وحدة تحكم (`dotnet new console`) وتشغيله. يوضح كلًا من حفظ HTML العادي وضغطه إلى zip.



## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة تعمل مع شرح خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية حفظ HTML في C# باستخدام معالج موارد مخصص](/html/english/net/working-with-html-documents/how-to-save-html-in-c-with-custom-resource-handler/)
- [كيفية استخدام ZipArchive – حفظ HTML والموارد إلى ملف ZIP](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [حفظ HTML كملف zip باستخدام معالج موارد مخصص – دليل خطوة بخطوة](/html/english/net/html-extensions-and-conversions/save-html-as-zip-with-a-custom-resource-handler-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
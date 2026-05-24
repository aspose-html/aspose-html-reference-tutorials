---
category: general
date: 2026-02-22
description: يتيح لك معالج الموارد المخصص التقاط مخرجات HTML. تعلّم كيفية تحميل مستند
  HTML، واستخدام Aspose HTML للحفظ، وحفظ HTML إلى تدفق باستخدام مثال بسيط بلغة C#.
draft: false
keywords:
- custom resource handler
- load html document
- aspose html save
- save html to stream
- capture html output
language: ar
og_description: تعلم كيف يلتقط معالج الموارد المخصص مخرجات HTML، ويحمل مستند HTML،
  ويحفظ HTML إلى تدفق باستخدام Aspose HTML في C#.
og_title: معالج الموارد المخصص في Aspose HTML – دليل حفظ إلى الدفق
tags:
- aspose-html
- csharp
- streaming
- resource-handler
title: معالج الموارد المخصص في Aspose HTML – دليل حفظ إلى تدفق
url: /ar/net/advanced-features/custom-resource-handler-in-aspose-html-save-to-stream-guide/
---

.

Now produce final content with Arabic translation.

Make sure to keep markdown formatting exactly.

Let's craft Arabic translations.

Be careful with punctuation and line breaks.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# معالج الموارد المخصص – التقاط مخرجات HTML باستخدام Aspose HTML

هل احتجت يوماً إلى **معالج موارد مخصص** لاعتراض كل ملف تكتبه Aspose HTML أثناء التحويل؟ ربما أردت توجيه HTML أو الصور أو CSS مباشرة إلى الذاكرة بدلاً من القرص. هذا سيناريو شائع جداً عندما تقوم بإنشاء خدمة ويب يجب أن تظل بلا حالة أو عندما تريد ببساطة **حفظ HTML إلى تدفق** للمعالجة لاحقاً.

في هذا الدرس سنستعرض مثالاً كاملاً جاهزاً للتنفيذ يوضح كيفية **تحميل مستند HTML**، إرفاق **معالج موارد مخصص**، واستخدام **Aspose HTML save** لالتقاط كل جزء من المخرجات في `MemoryStream`. في النهاية ستفهم ليس فقط “ما هو” بل “لماذا” وراء كل سطر، وستحصل على نمط قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع C#.

> **لماذا يهم؟**  
> يتيح لك التقاط مخرجات HTML في الذاكرة تجنّب عمليات الإدخال/الإخراج على نظام الملفات، تقليل زمن الاستجابة في وظائف السحابة، ومنحك تحكمًا كاملاً في التسمية أو الضغط أو حتى التحويلات الفورية.

---

## ما ستحتاجه

- **.NET 6** أو أحدث (الكود يعمل أيضاً على .NET Framework 4.7+).  
- حزمة NuGet **Aspose.HTML for .NET** (`Aspose.Html`).  
- ملف HTML بسيط (`input.html`) موجود في مجلد يمكنك الإشارة إليه.  
- أي بيئة تطوير تفضلها—Visual Studio، Rider، أو VS Code مع ملحقات C#.

لا يلزم أي إعداد إضافي؛ الـ API يقوم بكل الأعمال الثقيلة.

---

## الخطوة 1 – إنشاء معالج موارد مخصص

جوهر هذه التقنية هو إنشاء فئة فرعية من `Aspose.Html.Rendering.ResourceHandler`. عبر تجاوز `HandleResource` تقرر **أين** يذهب كل تدفق مورد. في حالتنا نعيد `MemoryStream` جديد لكل طلب، مما يعني أن كل CSS أو صورة أو جزء فرعي من HTML يبقى فقط في الذاكرة.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;

/// <summary>
/// Custom handler that writes every resource to a new MemoryStream.
/// </summary>
class MemoryStreamHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // The ResourceInfo gives you the original URL and MIME type.
        // You could inspect it here to decide whether to skip certain files.
        // For this tutorial we just allocate a fresh stream.
        return new MemoryStream();
    }
}
```

**نصيحة احترافية:** إذا كنت بحاجة إلى تتبع التدفقات (مثلاً لكتابتها لاحقاً في أرشيف ZIP)، احفظها في `Dictionary<string, MemoryStream>` مع مفتاح `resourceInfo.Uri`.

---

## الخطوة 2 – تحميل مستند HTML

قبل أن تتمكن من حفظ أي شيء، يجب **تحميل مستند HTML** إلى كائن `HTMLDocument`. يمكن لـ Aspose HTML القراءة من مسار ملف، URL، أو حتى من سلسلة نصية. هنا نستخدم ملفًا محليًا للتبسيط.

```csharp
// Adjust the path to point at your real HTML file.
string htmlPath = Path.Combine(Environment.CurrentDirectory, "input.html");

// Load the source HTML document.
HTMLDocument htmlDocument = new HTMLDocument(htmlPath);
```

إذا كان ملف HTML الخاص بك يشير إلى موارد خارجية (صور، خطوط، إلخ) تأكد من صحة الـ base URI؛ وإلا لن يتمكن المعالج من العثور عليها.

---

## الخطوة 3 – إنشاء مثيل للمعالج المخصص

الآن نقوم بإنشاء مثيل للمعالج الذي عرّفناه سابقًا. لا شيء معقد—فقط `new` بسيط. سيتم تمرير هذا الكائن إلى طريقة `Save` في الخطوة التالية.

```csharp
// Step 3: Instantiate the custom handler.
MemoryStreamHandler resourceHandler = new MemoryStreamHandler();
```

نظرًا لأن المعالج يعيش فقط في الذاكرة، لا تحتاج للقلق بشأن أذونات الملفات أو تنظيفها على القرص.

---

## الخطوة 4 – حفظ المستند باستخدام Aspose HTML Save

عملية **Aspose HTML save** تقبل `ResourceHandler`. أثناء تجول المحرك عبر الـ DOM وحل كل مورد مرتبط، يتم استدعاء `HandleResource`. تنفيذنا يعيد `MemoryStream`، لذا كل جزء ينتهي به المطاف في الذاكرة.

```csharp
// Step 4: Save the document.
// The handler's HandleResource method will be invoked for each output stream.
htmlDocument.Save(resourceHandler);
```

في هذه المرحلة يكون التحويل مكتملًا، لكن التدفقات لا تزال في الذاكرة. يمكنك الآن قراءتها، كتابتها إلى قاعدة بيانات، أو إرجاعها في استجابة API.

---

## الخطوة 5 – استرجاع والتحقق من التدفقات الملتقطة

نظرًا لأننا أعدنا `MemoryStream` جديد في كل مرة، نحتاج إلى طريقة للاحتفاظ بالمراجع. أدناه امتداد سريع للمعالج السابق يخزن كل تدفق في قاموس لتتمكن من فحصها بعد عملية الحفظ.

```csharp
class TrackingMemoryStreamHandler : ResourceHandler
{
    public Dictionary<string, MemoryStream> Streams { get; } = new();

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var ms = new MemoryStream();
        Streams[resourceInfo.Uri] = ms;   // Remember the stream by its URI.
        return ms;
    }
}

// Usage:
var trackingHandler = new TrackingMemoryStreamHandler();
htmlDocument.Save(trackingHandler);

// Example: write the main HTML output to console (as text)
if (trackingHandler.Streams.TryGetValue(htmlPath, out var mainStream))
{
    mainStream.Position = 0; // rewind
    using var reader = new StreamReader(mainStream);
    string html = reader.ReadToEnd();
    Console.WriteLine("=== Rendered HTML ===");
    Console.WriteLine(html);
}
```

تشغيل هذا الكود سيطبع الـ HTML النهائي الذي أنشأه Aspose، مؤكدًا أن **capture html output** يعمل كما هو متوقع.

---

## الحالات الخاصة والأسئلة الشائعة

### 1. ماذا لو كان المستند كبيرًا؟

يمكن أن يزداد استهلاك الذاكرة بسرعة. بالنسبة للملفات الكبيرة أو HTML يحتوي على الكثير من الصور عالية الدقة، فكر في البث مباشرة إلى `FileStream` أو **تدفق شبكة مؤقت** بدلاً من `MemoryStream`. يمكن للمعالج اتخاذ القرار بناءً على `resourceInfo.MimeType`.

### 2. هل يجب إغلاق (dispose) التدفقات؟

نعم. بعد الانتهاء من المعالجة، استدعِ `Dispose()` على كل `MemoryStream` (أو دع كتلة `using` تتولى ذلك). في مثال التتبع يمكننا إضافة:

```csharp
foreach (var ms in trackingHandler.Streams.Values)
    ms.Dispose();
```

### 3. هل يمكنني إعادة تسمية الموارد قبل الحفظ؟

بالطبع. داخل `HandleResource` لديك إمكانية الوصول إلى `resourceInfo.Uri`. يمكنك تعديلها، إضافة بادئة، أو حتى تخطي ملفات معينة بإرجاع `null`.

```csharp
if (resourceInfo.MimeType.StartsWith("image/"))
    return null; // Skip images completely.
```

### 4. هل هذا النهج آمن للمتعدد الخيوط؟

يجب **عدم** مشاركة مثيل واحد من المعالج بين عمليات `Save` المتزامنة. أنشئ معالجًا جديدًا لكل تحويل، أو احمِ القاموس الداخلي بقفل إذا اضطررت لإعادة استخدامه.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك لصقه في تطبيق Console. يوضح كل شيء—من تحميل ملف HTML إلى طباعة المخرجات الملتقطة.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering;

class TrackingMemoryStreamHandler : ResourceHandler
{
    public Dictionary<string, MemoryStream> Streams { get; } = new();

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var ms = new MemoryStream();
        Streams[resourceInfo.Uri] = ms;
        return ms;
    }
}

class SaveToStreamTutorial
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the HTML document you want to render.
        // -------------------------------------------------
        string htmlPath = Path.Combine(Environment.CurrentDirectory, "input.html");
        if (!File.Exists(htmlPath))
        {
            Console.WriteLine($"Cannot find {htmlPath}");
            return;
        }

        HTMLDocument htmlDocument = new HTMLDocument(htmlPath);

        // -------------------------------------------------
        // Step 2: Create the custom handler that captures streams.
        // -------------------------------------------------
        var handler = new TrackingMemoryStreamHandler();

        // -------------------------------------------------
        // Step 3: Save the document – Aspose will invoke our handler.
        // -------------------------------------------------
        htmlDocument.Save(handler);

        // -------------------------------------------------
        // Step 4: Retrieve the main HTML output and display it.
        // -------------------------------------------------
        if (handler.Streams.TryGetValue(htmlPath, out var mainStream))
        {
            mainStream.Position = 0; // rewind to start
            using var reader = new StreamReader(mainStream);
            string renderedHtml = reader.ReadToEnd();
            Console.WriteLine("=== Rendered HTML Output ===");
            Console.WriteLine(renderedHtml);
        }
        else
        {
            Console.WriteLine("Main HTML stream not found.");
        }

        // -------------------------------------------------
        // Step 5: Clean up.
        // -------------------------------------------------
        foreach (var ms in handler.Streams.Values)
            ms.Dispose();

        Console.WriteLine("All streams disposed. Done.");
    }
}
```

**المخرجات المتوقعة:** يطبع الـ Console الـ HTML المُصوَّر بالكامل (بما في ذلك أي CSS مضمن قد يولده Aspose) متبوعًا بتأكيد أن جميع التدفقات قد تم إغلاقها.

---

## الخلاصة

لقد تعلمت الآن كيفية تنفيذ **معالج موارد مخصص** في Aspose HTML، **تحميل مستند HTML**، و**حفظ HTML إلى تدفق** مع **التقاط مخرجات HTML** لمعالجة إضافية. النمط خفيف الوزن، واعٍ للمتعدد الخيوط، وقابل للتوسيع بالكامل—يمكنك استبدال `MemoryStream` بملف، أو مقبس شبكة، أو واجهة تخزين سحابية ببضع أسطر من الكود.

بعد ذلك، قد ترغب في استكشاف:

- **الحفظ إلى أرشيف ZIP** (مثالي لتجميع HTML، CSS، والصور).  
- **تطبيق التحويلات** (مثل تصغير CSS أثناء التنفيذ).  
- **البث مباشرة إلى استجابة HTTP** في ASP.NET Core للتنزيل الفوري.

جرّب ذلك وسترى مدى قوة **معالج الموارد المخصص** المخصَّص في السيناريوهات الواقعية. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
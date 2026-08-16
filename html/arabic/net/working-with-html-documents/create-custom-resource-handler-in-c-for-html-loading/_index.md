---
category: general
date: 2026-08-15
description: إنشاء معالج موارد مخصص بلغة C# لإدارة موارد HTML مثل الصور وCSS. تعلّم
  HTMLLoadOptions، تدفقات الذاكرة، وتحميل HTMLDocument.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom resource handler
- C# resource handler
- HTMLLoadOptions
- HTMLDocument loading
- memory stream for resources
language: ar
lastmod: 2026-08-15
og_description: إنشاء معالج موارد مخصص في C# للتحكم في طريقة تدفق موارد HTML. يوضح
  هذا الدرس إعداد HTMLLoadOptions، ومعالجة تدفق الذاكرة، وتحميل HTMLDocument بمنطق
  مخصص.
og_image_alt: Screenshot of C# code defining a custom resource handler class for HTML
  loading
og_title: إنشاء معالج موارد مخصص في C# – دليل كامل لإدارة موارد HTML
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  headline: Create custom resource handler in C# for HTML loading
  type: TechArticle
- description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  name: Create custom resource handler in C# for HTML loading
  steps:
  - name: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
    text: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
  - name: Configure `HTMLLoadOptions` to use the handler.
    text: Configure `HTMLLoadOptions` to use the handler.
  - name: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
    text: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
  - name: (Optional) Store received resources to disk for verification.
    text: (Optional) Store received resources to disk for verification.
  type: HowTo
tags:
- C#
- HTML
- resource handling
title: إنشاء معالج موارد مخصص في C# لتحميل HTML
url: /ar/net/working-with-html-documents/create-custom-resource-handler-in-c-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء معالج موارد مخصص في C# لتحميل HTML

إذا كنت بحاجة إلى **إنشاء معالج موارد مخصص** لملفات HTML، فإن هذا الدليل يوضح لك الطريقة بالضبط. ستتعلم كيفية اعتراض الصور، CSS، وغيرها من الأصول أثناء تحميل مستند HTML، باستخدام `HTMLLoadOptions` وتدفق قائم على الذاكرة.

يغطي الدرس كل ما يلزم لتنفيذ معالج قابل لإعادة الاستخدام، وتكوين خيارات التحميل، والتحقق من أن الموارد قد تم التقاطها بشكل صحيح. لا تحتاج إلى وثائق خارجية—فقط الشيفرة أدناه والشروحات.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث
- إلمام أساسي بـ C#
- مرجع لمكتبة معالجة HTML التي توفر `HTMLDocument`، `HtmlLoadOptions`، و `ResourceHandler` (مثل GroupDocs.Viewer for .NET)

## نظرة عامة على الحل

سنقوم بـ:

1. **إنشاء معالج موارد مخصص** عن طريق وراثة `ResourceHandler`.
2. تكوين `HTMLLoadOptions` لاستخدام المعالج.
3. تحميل ملف HTML باستخدام `HTMLDocument` بينما يوفر المعالج تدفقًا لكل مورد.
4. (اختياري) حفظ الموارد المستلمة على القرص للتحقق منها.

كل خطوة تتضمن الشيفرة الكاملة والسبب وراءها.

## الخطوة 1: تعريف فئة معالج الموارد المخصص

إنشاء معالج مخصص يعني تجاوز `HandleResource` حتى تتمكن المكتبة من كتابة بايتات المورد إلى تدفق تتحكم فيه. استخدام `MemoryStream` يبقي البيانات في الذاكرة، وهو مثالي للاختبار أو المعالجة اللاحقة.

```csharp
using System;
using System.IO;
using GroupDocs.Viewer.Handler;   // Adjust namespace to match your library

namespace HtmlResourceDemo
{
    /// <summary>
    /// Provides a memory stream for each HTML resource (images, CSS, etc.).
    /// </summary>
    public class MyHandler : ResourceHandler
    {
        /// <summary>
        /// Called by the viewer for every external resource referenced in the HTML.
        /// </summary>
        /// <param name="info">Information about the resource (name, MIME type, etc.).</param>
        /// <returns>A writable stream that receives the resource data.</returns>
        public override Stream HandleResource(ResourceInfo info)
        {
            // A fresh MemoryStream ensures the viewer can write the resource bytes.
            // You could replace this with a FileStream to save directly to disk.
            return new MemoryStream();
        }
    }
}
```

**لماذا هذا مهم:**  
تجاوز `HandleResource` يمنحك التحكم الكامل في مكان توجيه بيانات الموارد. إذا احتجت لاحقًا إلى تخزين الصور مؤقتًا، أو تحويل CSS، أو تسجيل استخدام الموارد، يمكنك استبدال `MemoryStream` بأي تنفيذ تدفق مخصص.

## الخطوة 2: تكوين `HTMLLoadOptions` لاستخدام المعالج

`HTMLLoadOptions` يتيح لك ربط المعالج بسلسلة تحميل المستند. ضبط خاصية `ResourceHandler` يخبر العارض باستدعاء `MyHandler` لكل أصل خارجي.

```csharp
using GroupDocs.Viewer.Options;   // Namespace for HtmlLoadOptions

// ...

var loadOptions = new HtmlLoadOptions
{
    // Attach the custom handler defined in Step 1
    ResourceHandler = new MyHandler()
};
```

**لماذا هذا مهم:**  
بدون تعيين `ResourceHandler`، سيكتب العارض الموارد إلى موقعه الافتراضي (غالبًا مجلد مؤقت). بتحديد معالجك الخاص، **تنشئ معالج موارد مخصص** يتماشى مع استراتيجية التخزين في تطبيقك.

## الخطوة 3: تحميل مستند HTML باستخدام الخيارات المكوَّنة

الآن قم بتحميل ملف HTML. سيستدعي العارض `MyHandler.HandleResource` لكل مورد يصادفه.

```csharp
using GroupDocs.Viewer;           // Namespace for HTMLDocument

// Path to the source HTML file
string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// Load the document using the custom load options
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);
```

في هذه المرحلة يتم تحليل محتوى HTML، وتُدفّق جميع الموارد الخارجية إلى مخازن الذاكرة التي يوفرها `MyHandler`.

## الخطوة 4 (اختياري): الوصول إلى الموارد الملتقطة

إذا كنت بحاجة إلى فحص أو حفظ الموارد، يمكنك تعديل `MyHandler` لتخزين كل `MemoryStream` في قاموس مفتاحه اسم المورد.

```csharp
public class MyHandler : ResourceHandler
{
    // Stores streams for later retrieval
    public Dictionary<string, MemoryStream> Resources { get; } = new();

    public override Stream HandleResource(ResourceInfo info)
    {
        var stream = new MemoryStream();
        Resources[info.Name] = stream;
        return stream;
    }
}
```

بعد التحميل، يمكنك التجول عبر `handler.Resources` وكتابة كل منها إلى القرص:

```csharp
var handler = new MyHandler();
var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);

// Save each captured resource
foreach (var kvp in handler.Resources)
{
    string fileName = Path.Combine("output_resources", kvp.Key);
    File.WriteAllBytes(fileName, kvp.Value.ToArray());
    Console.WriteLine($"Saved resource: {fileName}");
}
```

**لماذا هذا مهم:**  
تخزين الموارد يتيح المعالجة اللاحقة مثل تحسين الصور، تصغير CSS، أو الأرشفة. كما يوفر تحققًا ملموسًا من أن منطق **إنشاء معالج موارد مخصص** يعمل كما هو متوقع.

## الخطوة 5: التنظيف

يجب التخلص من كل من `HTMLDocument` وأي تدفقات لتفريغ الموارد غير المُدارة.

```csharp
doc.Dispose();                     // Releases internal buffers
foreach (var stream in handler.Resources.Values)
{
    stream.Dispose();              // Flushes and releases memory
}
```

## مثال كامل قابل للتنفيذ

فيما يلي برنامج مكتمل يوضح جميع الخطوات من تعريف الفئة إلى استخراج الموارد.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Viewer;
using GroupDocs.Viewer.Handler;
using GroupDocs.Viewer.Options;

namespace HtmlResourceDemo
{
    public class MyHandler : ResourceHandler
    {
        public Dictionary<string, MemoryStream> Resources { get; } = new();

        public override Stream HandleResource(ResourceInfo info)
        {
            var stream = new MemoryStream();
            Resources[info.Name] = stream;
            return stream;
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare paths
            string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");
            string outputDir = Path.Combine("output_resources");
            Directory.CreateDirectory(outputDir);

            // 2️⃣ Create handler and load options
            var handler = new MyHandler();
            var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };

            // 3️⃣ Load the HTML document
            using (HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions))
            {
                // Document is now loaded; resources are in handler.Resources
            }

            // 4️⃣ Persist captured resources
            foreach (var kvp in handler.Resources)
            {
                string filePath = Path.Combine(outputDir, kvp.Key);
                File.WriteAllBytes(filePath, kvp.Value.ToArray());
                Console.WriteLine($"Saved: {filePath}");
            }

            // 5️⃣ Clean up streams
            foreach (var stream in handler.Resources.Values)
                stream.Dispose();

            Console.WriteLine("All resources processed.");
        }
    }
}
```

**الناتج المتوقع**

```
Saved: output_resources/logo.png
Saved: output_resources/styles.css
Saved: output_resources/banner.jpg
All resources processed.
```

تسرد وحدة التحكم كل مورد قام العارض بتدفقه عبر معالجك المخصص، مؤكدًا أن سير عمل **إنشاء معالج موارد مخصص** قد نجح.

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|----------|--------|
| *ماذا لو كان المورد كبيرًا (مثل صورة عالية الدقة)؟* | استبدل `MemoryStream` بـ `FileStream` يشير إلى مجلد مؤقت. هذا يمنع استهلاك الذاكرة بشكل مفرط. |
| *هل يمكنني تصفية الموارد حسب النوع؟* | داخل `HandleResource`، افحص `info.MimeType` أو `info.Extension` وأعد `null` للأنواع غير المرغوبة. إرجاع `null` يخبر العارض بتخطي المورد. |
| *هل يلزم ضمان أمان الخيوط (thread safety)؟* | إذا تم استخدام نفس نسخة المعالج عبر عمليات تحميل متزامنة متعددة، احمِ قاموس `Resources` باستخدام قفل أو استخدم مجموعة متزامنة. |
| *كيف أدعم عناوين URL النسبية؟* | يحتوي `ResourceInfo` على عنوان URL الأصلي؛ يمكنك دمجه مع المسار الأساسي لملف HTML لحل الإشارات النسبية قبل التخزين. |

## الخلاصة

أصبحت الآن تعرف كيف **تنشئ معالج موارد مخصص** في C# لتحميل HTML، وتُكوّن `HTMLLoadOptions`، وتلتقط الأصول المتدفقة، وتُنظف الموارد بشكل مسؤول. يتيح لك هذا النمط التحكم الكامل في إدارة الموارد، مما يفتح أمامك سيناريوهات مثل معالجة الصور أثناء التشغيل، إعادة كتابة CSS، أو التخزين الآمن.

بعد ذلك، استكشف المواضيع ذات الصلة مثل **تحميل HTMLDocument** بخيارات عرض مختلفة، أو وسّع المعالج إلى تنفيذات **معالج موارد C#** التي تكتب مباشرة إلى التخزين السحابي. جرّب طريقة `HandleResource` لتتناسب مع سير عمل الموارد الخاص بمشروعك.

## ماذا يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تُكمل التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [Create HTML from String in C# – Custom Resource Handler Guide](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Custom Resource Handler in C# – Convert HTML to ZIP Tutorial](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
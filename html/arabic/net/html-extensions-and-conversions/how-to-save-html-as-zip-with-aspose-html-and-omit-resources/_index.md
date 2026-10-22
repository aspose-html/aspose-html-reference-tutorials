---
category: general
date: 2026-10-21
description: تعلم كيفية حفظ HTML كملف ZIP باستخدام Aspose.HTML، وتحويل HTML إلى ZIP،
  وإزالة الموارد للحصول على حزمة نظيفة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save html as zip
- convert html to zip
- how to omit resources
- how to strip resources
- create html zip
language: ar
lastmod: 2026-10-21
og_description: احفظ ملفات HTML كملف ZIP باستخدام Aspose.HTML، وتعلم كيفية تحويل HTML
  إلى ZIP وإزالة الموارد لإنشاء أرشيف خفيف الوزن.
og_image_alt: Screenshot showing the save html as zip process with resources omitted
og_title: حفظ HTML كملف ZIP باستخدام Aspose.HTML – حذف الموارد في خطوة واحدة
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to save HTML as ZIP using Aspose.HTML, convert HTML to ZIP,
    and strip resources for a clean package.
  headline: How to save HTML as ZIP with Aspose.HTML and omit resources
  type: TechArticle
tags:
- Aspose.HTML
- C#
- ZIP archive
- HTML conversion
- Resource handling
title: كيفية حفظ HTML كملف ZIP باستخدام Aspose.HTML وتجاهل الموارد
url: /ar/net/html-extensions-and-conversions/how-to-save-html-as-zip-with-aspose-html-and-omit-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية حفظ HTML كملف ZIP باستخدام Aspose.HTML وتجاهل الموارد

إذا كنت بحاجة إلى **حفظ HTML كملف ZIP** مع إزالة الملفات الخارجية، فإن هذا الدليل يوضح حلاً كاملاً وجاهزًا للتنفيذ. في نهاية البرنامج التعليمي ستكون قادرًا على **تحويل HTML إلى ZIP**، والتحكم في الموارد التي يتم الاحتفاظ بها، وإنتاج أرشيف نظيف يحتوي فقط على العلامات الأساسية.

العديد من سيناريوهات أتمتة الويب تتطلب حزم صفحة للاستخدام دون اتصال، أو كمرفق بريد إلكتروني، أو للتخزين الأرشيفي. تضمين الصور أو الخطوط أو السكريبتات غالبًا ما يزيد حجم الأرشيف دون ضرورة. الخطوات أدناه توضح **كيفية تجاهل الموارد** و**كيفية حذف الموارد** من الناتج، بحيث يبقى ملف ZIP الناتج خفيفًا.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من أن لديك:

- .NET 6.0 أو أحدث مثبت  
- رخصة Aspose.HTML لـ .NET (أو نسخة تجريبية مجانية)  
- بيئة تطوير C# أساسية (Visual Studio أو VS Code أو Rider)  

لا توجد حزم NuGet إضافية مطلوبة بخلاف `Aspose.Html`.

## الخطوة 1: إنشاء معالج موارد مخصص

جوهر **كيفية تجاهل الموارد** يكمن في فئة فرعية من `ResourceHandler`. تقوم Aspose.HTML باستدعاء هذا المعالج لكل أصل خارجي (صور، CSS، سكريبتات). بإرجاع تدفق فارغ، تقوم فعليًا بإخبار المحول بتخطي الأصل.

```csharp
using System.IO;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Prevents external resources from being written to the output package.
/// </summary>
class CustomResourceHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info)
    {
        // Returning an empty MemoryStream strips the resource from the ZIP.
        return new MemoryStream();
    }
}
```

**لماذا هذا مهم:** السلوك الافتراضي ينسخ كل ملف مرتبط إلى ملف ZIP، مما قد يضاعف أو يثلث حجم الملف. تجاوز `HandleResource` يمنحك تحكمًا دقيقًا دون تعديل الـ HTML الأصلي.

## الخطوة 2: تحميل مستند HTML

قم بتحميل الملف المصدر باستخدام `HTMLDocument`. يقبل المُنشئ مسار ملف، أو عنوان URL، أو تدفق. في هذا المثال نقرأ ملفًا محليًا اسمه `input.html`.

```csharp
// Load the source HTML file from the local file system.
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

إذا كان الـ HTML موجودًا في الذاكرة أو يأتي من طلب ويب، يمكنك تمرير `MemoryStream` أو سلسلة URL بدلاً من ذلك. تعمل الـ API بنفس الطريقة.

## الخطوة 3: تكوين خيارات الحفظ

أنشئ كائنًا من `HtmlSaveOptions` وعيّن المعالج المخصص الذي تم إنشاؤه في الخطوة 1. هذا يخبر Aspose.HTML باستخدام المعالج كلما صادف موردًا.

```csharp
// Prepare save options and attach the custom resource handler.
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // The ResourceHandler property is what enables resource stripping.
    ResourceHandler = new CustomResourceHandler()
};
```

يمكنك أيضًا تعديل خيارات أخرى هنا، مثل `CompressImages = false` إذا كنت تريد الاحتفاظ ببيانات الصور ولكن لا تزال تتجاهل الأصول الأخرى. المثال يحتفظ بإعدادات الضغط الافتراضية.

## الخطوة 4: حفظ المستند كأرشيف ZIP

أخيرًا، استدعِ `Save` مع مسار الهدف والخيارات المكوَّنة. سيكون الملف الناتج ملف `.zip` يحتوي على `index.html` (أو اسم الملف الأصلي) و**بدون موارد خارجية**.

```csharp
// Save the HTML document as a ZIP file. The archive will contain only the HTML markup.
document.Save("YOUR_DIRECTORY/output.zip", saveOptions);
```

### النتيجة المتوقعة

- `output.zip` → يحتوي على ملف `index.html` واحد.  
- جميع الصور، ملفات CSS، وإشارات JavaScript تم حذفها، لأن المعالج المخصص أرجع تدفقًا فارغًا لكل منها.

يمكنك التحقق من الأرشيف بفتحه بأي عارض ZIP. ستظل صفحة HTML تشير إلى عناوين URL الأصلية، لكن تلك الملفات غير موجودة في الأرشيف، مما يحافظ على حزمة خفيفة.

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه، لصقه، وتشغيله. استبدل `YOUR_DIRECTORY` بمسار مجلد فعلي على جهازك.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Converters;

class Program
{
    static void Main()
    {
        // Step 1: Define a custom resource handler to control how external resources are saved.
        class CustomResourceHandler : ResourceHandler
        {
            public override Stream HandleResource(ResourceInfo info)
            {
                // Returning an empty stream strips the resource from the ZIP output.
                return new MemoryStream();
            }
        }

        // Step 2: Load an HTML document from a file.
        string inputPath = "YOUR_DIRECTORY/input.html";
        HTMLDocument document = new HTMLDocument(inputPath);

        // Step 3: Create HTML save options and assign the custom handler.
        HtmlSaveOptions saveOptions = new HtmlSaveOptions
        {
            ResourceHandler = new CustomResourceHandler()
        };

        // Step 4: Save the document as a ZIP archive containing the HTML and (now omitted) resources.
        string outputPath = "YOUR_DIRECTORY/output.zip";
        document.Save(outputPath, saveOptions);

        Console.WriteLine($"HTML has been saved as ZIP at: {outputPath}");
    }
}
```

تشغيل هذا البرنامج ينتج ملف ZIP الموضح سابقًا. يمكنك الآن توزيع صفحة HTML دون تجميع الأصول غير الضرورية.

## تنوعات شائعة وحالات حدية

| السيناريو | التعديل |
|----------|------------|
| **الاحتفاظ بالصور وحذف CSS/JS** | في `CustomResourceHandler`، افحص `info.MimeType`. أرجع `MemoryStream` فقط لـ `text/css` و `application/javascript`. |
| **الحفاظ على الخطوط الخارجية** | أرجع التدفق الأصلي لأنواع MIME `font/woff2`، وإلا أرجع تدفقًا فارغًا. |
| **إنشاء ZIP باسم إدخال مخصص** | استخدم overload `Save(string path, SaveOptions options, string entryName)` في `HtmlSaveOptions` لتحديد اسم ملف جذري مختلف. |
| **تحويل ملفات HTML متعددة إلى ملف ZIP واحد** | قم بالتكرار على كل ملف، أنشئ `HTMLDocument` منفصل، وأضف كل منها إلى نفس `ZipArchive` يدويًا باستخدام `System.IO.Compression`. |

## نصائح احترافية

- **تحقق من النتيجة**: بعد الحفظ، افتح ملف ZIP وحمّل `index.html` في المتصفح. ستظهر الموارد المفقودة كروابط مكسورة، مما يؤكد أن المعالج عمل.  
- **الأداء**: إرجاع `MemoryStream` فارغ تكلفة قليلة، ولكن إذا كان لديك آلاف الأصول، فكر في تخزين القرار مؤقتًا (مثل `HashSet<string>` لأنواع MIME التي يجب تخطيها).  
- **الترخيص**: النسخة التجريبية المجانية من Aspose.HTML تضيف تعليق علامة مائية داخل الـ HTML. استخدم نسخة مرخصة لإزالتها في بيئة الإنتاج.

## الخلاصة

أنت الآن تعرف كيف **تحفظ HTML كملف ZIP**، **تحول HTML إلى ZIP**، و**تحذف الموارد** باستخدام Aspose.HTML لـ .NET. من خلال تنفيذ `ResourceHandler` مخصص، يمكنك تجاهل الملفات غير المرغوب فيها والحفاظ على الأرشيف خفيفًا. جرب منطق المعالج لتحتفظ فقط بالموارد التي تحتاجها حقًا، ودمج هذا النمط في خطوط أتمتة أكبر.

---

**الخطوات التالية**

- استكشف ميزات أخرى في `HtmlSaveOptions` مثل `EmbedImages` لتضمين الصور مباشرةً في الـ HTML.  
- اجمع هذا النهج مع `Aspose.PDF` لتحويل نفس الـ HTML إلى PDF بعد إنشاء الـ ZIP.  
- انظر إلى سيناريوهات الخادم حيث تقوم بإنشاء الـ ZIP عند الطلب وتدفقه إلى العميل دون كتابة إلى القرص.  

برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة من التعليمات البرمجية مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية استخدام ZipArchive – حفظ HTML والموارد إلى ملف ZIP](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [كيفية حفظ HTML في C# – معالجات موارد مخصصة & ZIP](/html/english/net/working-with-html-documents/how-to-save-html-in-c-custom-resource-handlers-zip/)
- [كيفية حفظ HTML كملف ZIP في C# – دليل Aspose.HTML الكامل](/html/english/net/html-extensions-and-conversions/how-to-save-html-as-zip-in-c-complete-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
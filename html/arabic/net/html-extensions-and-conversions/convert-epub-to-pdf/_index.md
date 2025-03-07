---
title: تحويل EPUB إلى PDF في .NET باستخدام Aspose.HTML
linktitle: تحويل EPUB إلى PDF في .NET
second_title: Aspose.HTML .NET HTML manipulation API
description: تعرف على كيفية تحويل EPUB إلى PDF باستخدام Aspose.HTML لـ .NET. يغطي هذا الدليل خطوة بخطوة خيارات التخصيص والأسئلة الشائعة والمزيد لتحويل المستندات بسلاسة.
weight: 12
url: /ar/net/html-extensions-and-conversions/convert-epub-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل EPUB إلى PDF في .NET باستخدام Aspose.HTML


في هذا البرنامج التعليمي، سنستكشف كيفية استخدام Aspose.HTML for .NET لتحويل ملفات EPUB إلى PDF. Aspose.HTML هي مكتبة .NET قوية توفر وظائف متنوعة للعمل مع مستندات HTML وEPUB. سنغطي المتطلبات الأساسية، ونستورد المساحات الأساسية الضرورية، ونتناول أمثلة متعددة، ونشرح كل خطوة بالتفصيل.

## المتطلبات الأساسية

قبل أن تبدأ، تأكد من توفر المتطلبات الأساسية التالية:

1. Aspose.HTML for .NET: تأكد من تثبيت Aspose.HTML for .NET في مشروع .NET الخاص بك. يمكنك تنزيله من[هنا](https://releases.aspose.com/html/net/).

2. دليل البيانات الخاص بك: سوف تحتاج إلى دليل بيانات يتم تخزين ملفات EPUB الخاصة بك فيه.

الآن، دعنا ننتقل إلى عملية تحويل EPUB إلى PDF خطوة بخطوة باستخدام Aspose.HTML لـ .NET.

## تحويل EPUB إلى PDF

### الخطوة 1: قم ببدء مشروعك

تأكد من إعداد مشروع .NET لديك، وتثبيت Aspose.HTML لـ .NET.

### الخطوة 2: استيراد المساحات المطلوبة

في ملف الكود C# الخاص بك، قم باستيراد المساحات الأساسية الضرورية:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
```

### الخطوة 3: افتح ملف EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // انتقل إلى الخطوة التالية...
}
```

-  يستبدل`"Your Data Directory"` مع الدليل الفعلي الذي يوجد به ملف EPUB الخاص بك.
- يفتح هذا الكود ملف EPUB للقراءة.

### الخطوة 4: تعيين خيارات PDF وإجراء التحويل

```csharp
var options = new PdfSaveOptions();
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  إنشاء مثيل لـ`PdfSaveOptions` لتحديد إعدادات تحويل PDF.
-  استخدم`Converter.ConvertEPUB` طريقة تحويل EPUB إلى PDF باستخدام الخيارات الموضحة.
- احفظ ملف PDF الناتج باسم "output.pdf".

## تحديد خيارات حفظ PDF

### الخطوة 1: قم ببدء مشروعك

تأكد من إعداد مشروع .NET وتثبيت Aspose.HTML لـ .NET.

### الخطوة 2: استيراد المساحات المطلوبة

استيراد المساحات الأسماء الضرورية في الكود C# الخاص بك:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
```

### الخطوة 3: افتح ملف EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // انتقل إلى الخطوة التالية...
}
```

-  يستبدل`"Your Data Directory"` مع الدليل الفعلي لملف EPUB الخاص بك.
- افتح ملف EPUB للقراءة.

### الخطوة 4: تخصيص خيارات PDF

```csharp
var options = new PdfSaveOptions()
{
    PageSetup = { AnyPage = new Page() { Size = Size.FromPixels(3000, 1000) } },
    BackgroundColor = System.Drawing.Color.AliceBlue
};
```

-  إنشاء مثيل لـ`PdfSaveOptions` وتخصيصها حسب متطلباتك.
- في هذا المثال، قمنا بتعيين حجم الصفحة إلى 3000 بكسل عرضًا و1000 بكسل ارتفاعًا، ولون الخلفية إلى Alice Blue.

### الخطوة 5: تنفيذ التحويل

```csharp
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  استخدم`Converter.ConvertEPUB` طريقة تحويل EPUB إلى PDF باستخدام الخيارات المخصصة.
- احفظ ملف PDF الناتج باسم "output.pdf".

## استخدم موفر البث المخصص

### الخطوة 1: قم ببدء مشروعك

قم بإعداد مشروع .NET وتثبيت Aspose.HTML لـ .NET.

### الخطوة 2: استيراد المساحات المطلوبة

في الكود C# الخاص بك، قم باستيراد المساحات الأساسية الضرورية:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
```

### الخطوة 3: افتح ملف EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // انتقل إلى الخطوة التالية...
}
```

-  يستبدل`"Your Data Directory"` مع الدليل الفعلي لملف EPUB الخاص بك.
- افتح ملف EPUB للقراءة.

### الخطوة 4: استخدام موفر بث مخصص

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    Converter.ConvertEPUB(stream, new PdfSaveOptions(), streamProvider);

    // انتقل إلى الخطوة التالية...
}
```

-  إنشاء`MemoryStreamProvider` لإدارة نتيجة التحويل كتدفق للذاكرة.
-  استخدم`Converter.ConvertEPUB` الطريقة مع موفر البث المخصص.

### الخطوة 5: احفظ النتيجة

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.pdf"))
{
    memory.CopyTo(fs);
}
```

- الوصول إلى مجرى الذاكرة الذي يحتوي على البيانات المحولة.
- ضبط موضع البث إلى البداية.
- قم بإنشاء ملف PDF إخراجي ثم انسخ المحتوى من مجرى الذاكرة إليه.

### كود المصدر للفئة MemoryStreamProvider. 

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // قائمة كائنات MemoryStream التي تم إنشاؤها أثناء عرض المستند
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // يتم استدعاء هذه الطريقة عندما تكون هناك حاجة إلى تيار إخراج واحد فقط، على سبيل المثال بالنسبة لتنسيقات XPS أو PDF أو TIFF.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // يتم استدعاء هذه الطريقة عندما يكون إنشاء تدفقات إخراج متعددة مطلوبًا. على سبيل المثال أثناء عرض HTML لقائمة ملفات الصور (JPG وPNG وما إلى ذلك)
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // هنا يمكنك تحرير التدفق المليء بالبيانات، على سبيل المثال، وتفريغه على القرص الصلب
            }
            public void Dispose()
            {
                // تحرير الموارد
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
الآن، تعلمت كيفية تحويل ملفات EPUB إلى PDF باستخدام Aspose.HTML for .NET مع خيارات متنوعة وإمكانيات التخصيص. يبسط Aspose.HTML العملية، ويوفر المرونة والتحكم في تحويل المستندات.

## خاتمة

Aspose.HTML for .NET هي أداة متعددة الاستخدامات لتحويل ملفات EPUB إلى PDF، وتوفر خيارات التخصيص لتكييف مستند PDF الناتج مع احتياجاتك. سواء كنت بحاجة إلى تحويلات بسيطة أو تخصيص متقدم، فإن Aspose.HTML يوفر لك ما تحتاجه.

 إذا لم تقم بذلك بالفعل، فيمكنك تنزيل Aspose.HTML لـ .NET من[موقع إلكتروني](https://releases.aspose.com/html/net/) وابدأ في استخدامه في تطبيقات .NET الخاصة بك اليوم.

---

## الأسئلة الشائعة

### هل استخدام Aspose.HTML لـ .NET مجاني؟
    Aspose.HTML for .NET هو منتج تجاري، ولكن تتوفر نسخة تجريبية مجانية[هنا](https://releases.aspose.com/).

### هل يمكنني تخصيص مظهر ملف PDF المُحوّل؟
   نعم، يمكنك تخصيص مظهر ملف PDF عن طريق ضبط الخيارات مثل حجم الصفحة ولون الخلفية، كما هو موضح في المثال 2.

### كيف يمكنني الحصول على الدعم لـ Aspose.HTML لـ .NET؟
    يمكنك العثور على الدعم والموارد على[منتدى Aspose.HTML](https://forum.aspose.com/).

### هل هناك تنسيقات أخرى يمكنني تحويلها باستخدام Aspose.HTML لـ .NET؟
   نعم، يدعم Aspose.HTML for .NET تنسيقات المستندات المختلفة، بما في ذلك HTML، وEPUB، والمزيد.

### هل Aspose.HTML for ..NET مناسب لتحويل المستندات على نطاق واسع؟
   تم تصميم Aspose.HTML for .NET للتعامل بكفاءة مع تحويلات المستندات واسعة النطاق، مما يجعله مناسبًا لمجموعة واسعة من التطبيقات.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

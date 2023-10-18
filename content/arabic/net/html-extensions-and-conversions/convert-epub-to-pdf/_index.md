---
title: قم بتحويل EPUB إلى PDF بتنسيق .NET باستخدام Aspose.HTML
linktitle: تحويل EPUB إلى PDF في .NET
second_title: Aspose.HTML .NET واجهة برمجة تطبيقات معالجة HTML
description: تعرف على كيفية تحويل EPUB إلى PDF باستخدام Aspose.HTML لـ .NET. يغطي هذا الدليل خطوة بخطوة خيارات التخصيص والأسئلة الشائعة والمزيد لتحويل المستندات بسلاسة.
type: docs
weight: 12
url: /ar/net/html-extensions-and-conversions/convert-epub-to-pdf/
---

في هذا البرنامج التعليمي، سوف نستكشف كيفية استخدام Aspose.HTML لـ .NET لتحويل ملفات EPUB إلى PDF. Aspose.HTML هي مكتبة .NET قوية توفر وظائف متنوعة للعمل مع مستندات HTML وEPUB. سنقوم بتغطية المتطلبات الأساسية، واستيراد مساحات الأسماء الضرورية، وتقسيم الأمثلة المتعددة، وشرح كل خطوة بالتفصيل.

## المتطلبات الأساسية

قبل البدء، تأكد من توفر المتطلبات الأساسية التالية:

1. Aspose.HTML for .NET: تأكد من تثبيت Aspose.HTML for .NET في مشروع .NET الخاص بك. يمكنك تنزيله من[هنا](https://releases.aspose.com/html/net/).

2. دليل البيانات الخاص بك: ستحتاج إلى دليل بيانات حيث يتم تخزين ملفات EPUB الخاصة بك.

الآن، دعنا نتعمق في عملية تحويل EPUB إلى PDF خطوة بخطوة باستخدام Aspose.HTML لـ .NET.

## تحويل EPUB إلى PDF

### الخطوة 1: تهيئة مشروعك

تأكد من إعداد مشروع .NET، ومن تثبيت Aspose.HTML لـ .NET.

### الخطوة 2: استيراد مساحات الأسماء المطلوبة

في ملف كود C# الخاص بك، قم باستيراد مساحات الأسماء الضرورية:

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
- يفتح هذا الرمز ملف EPUB للقراءة.

### الخطوة 4: ضبط خيارات PDF وإجراء التحويل

```csharp
var options = new PdfSaveOptions();
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  إنشاء مثيل ل`PdfSaveOptions` لتحديد إعدادات تحويل PDF.
-  استخدم ال`Converter.ConvertEPUB` طريقة لتحويل EPUB إلى PDF مع الخيارات المحددة.
- احفظ ملف PDF الناتج باسم "output.pdf".

## حدد خيارات حفظ PDF

### الخطوة 1: تهيئة مشروعك

تأكد من إعداد مشروع .NET وتثبيت Aspose.HTML لـ .NET.

### الخطوة 2: استيراد مساحات الأسماء المطلوبة

قم باستيراد مساحات الأسماء الضرورية في كود C# الخاص بك:

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

-  إنشاء مثيل ل`PdfSaveOptions` وتخصيصه وفقا لمتطلباتك.
- في هذا المثال، قمنا بتعيين حجم الصفحة على 3000 بكسل عرضًا و1000 بكسل ارتفاعًا، ولون الخلفية إلى Alice Blue.

### الخطوة 5: إجراء التحويل

```csharp
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  استخدم ال`Converter.ConvertEPUB` طريقة لتحويل EPUB إلى PDF مع الخيارات المخصصة.
- احفظ ملف PDF الناتج باسم "output.pdf".

## استخدم موفر الدفق المخصص

### الخطوة 1: تهيئة مشروعك

قم بإعداد مشروع .NET وقم بتثبيت Aspose.HTML لـ .NET.

### الخطوة 2: استيراد مساحات الأسماء المطلوبة

في كود C# الخاص بك، قم باستيراد مساحات الأسماء الضرورية:

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

### الخطوة 4: استخدم موفر دفق مخصص

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    Converter.ConvertEPUB(stream, new PdfSaveOptions(), streamProvider);

    // انتقل إلى الخطوة التالية...
}
```

-  إنشاء`MemoryStreamProvider` لإدارة نتيجة التحويل كدفق الذاكرة.
-  استخدم ال`Converter.ConvertEPUB` الطريقة مع موفر الدفق المخصص.

### الخطوة 5: حفظ النتيجة

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.pdf"))
{
    memory.CopyTo(fs);
}
```

- الوصول إلى دفق الذاكرة الذي يحتوي على البيانات المحولة.
- اضبط موضع الدفق على البداية.
- قم بإنشاء ملف PDF للإخراج وانسخ المحتوى من دفق الذاكرة إليه.

### كود مصدر فئة MemoryStreamProvider. 

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // قائمة كائنات MemoryStream التي تم إنشاؤها أثناء عرض المستند
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // يتم استدعاء هذه الطريقة عند الحاجة إلى دفق إخراج واحد فقط، على سبيل المثال لتنسيقات XPS أو PDF أو TIFF.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // يتم استدعاء هذه الطريقة عند الحاجة إلى إنشاء تدفقات إخراج متعددة. على سبيل المثال، أثناء عرض HTML لقائمة ملفات الصور (JPG، PNG، وما إلى ذلك)
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // هنا يمكنك تحرير الدفق المليء بالبيانات، على سبيل المثال، دفعه إلى القرص الصلب
            }
            public void Dispose()
            {
                // الافراج عن الموارد
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
لقد تعلمت الآن كيفية تحويل ملفات EPUB إلى PDF باستخدام Aspose.HTML لـ .NET مع العديد من الخيارات وإمكانيات التخصيص. يعمل Aspose.HTML على تبسيط العملية، مما يوفر المرونة والتحكم في تحويل المستند.

## خاتمة

Aspose.HTML for .NET هي أداة متعددة الاستخدامات لتحويل ملفات EPUB إلى PDF، مما يوفر خيارات التخصيص لتخصيص مستند PDF الناتج وفقًا لاحتياجاتك. سواء كنت تحتاج إلى تحويلات بسيطة أو تخصيص متقدم، فإن Aspose.HTML يلبي احتياجاتك.

 إذا لم تكن قد قمت بذلك بالفعل، فيمكنك تنزيل Aspose.HTML لـ .NET من[موقع إلكتروني](https://releases.aspose.com/html/net/) وابدأ في استخدامه في تطبيقات .NET الخاصة بك اليوم.

---

## الأسئلة الشائعة

### هل Aspose.HTML for .NET مجاني للاستخدام؟
    يعد Aspose.HTML for .NET منتجًا تجاريًا، ولكن تتوفر نسخة تجريبية مجانية منه[هنا](https://releases.aspose.com/).

### هل يمكنني تخصيص مظهر ملف PDF المحول؟
   نعم، يمكنك تخصيص مظهر PDF عن طريق ضبط خيارات مثل حجم الصفحة ولون الخلفية، كما هو موضح في المثال 2.

### كيف يمكنني الحصول على دعم لـ Aspose.HTML لـ .NET؟
    يمكنك العثور على الدعم والموارد على[منتدى Aspose.HTML](https://forum.aspose.com/).

### هل هناك تنسيقات أخرى يمكنني تحويلها باستخدام Aspose.HTML لـ .NET؟
   نعم، يدعم Aspose.HTML for .NET تنسيقات المستندات المختلفة، بما في ذلك HTML وEPUB والمزيد.

### هل Aspose.HTML for ..NET مناسب لتحويل المستندات على نطاق واسع؟
   تم تصميم Aspose.HTML for .NET للتعامل مع تحويلات المستندات واسعة النطاق بكفاءة، مما يجعله مناسبًا لمجموعة واسعة من التطبيقات.


---
title: تحويل EPUB إلى XPS في .NET باستخدام Aspose.HTML
linktitle: تحويل EPUB إلى XPS في .NET
second_title: Aspose.Slides .NET واجهة برمجة تطبيقات معالجة HTML
description: تعرف على كيفية تحويل EPUB إلى XPS في .NET باستخدام Aspose.HTML لـ .NET. اتبع دليلنا خطوة بخطوة لإجراء تحويلات سهلة.
type: docs
weight: 13
url: /ar/net/html-extensions-and-conversions/convert-epub-to-xps/
---

هل تبحث عن طريقة سلسة لتحويل ملفات EPUB إلى تنسيق XPS في تطبيقات .NET الخاصة بك؟ يوفر Aspose.HTML for .NET حلاً قويًا لتحقيق ذلك دون عناء. في هذا الدليل المفصّل خطوة بخطوة، سنرشدك خلال عملية تحويل EPUB إلى XPS باستخدام Aspose.HTML. هيا بنا نبدأ!

## المتطلبات الأساسية

قبل أن تتعمق في عملية تحويل EPUB إلى XPS، ستحتاج إلى التأكد من توفر المتطلبات الأساسية التالية:

### 1. Aspose.HTML لمكتبة .NET

 تأكد من تثبيت مكتبة Aspose.HTML for .NET في مشروعك. إذا لم تقم بذلك، يمكنك الحصول عليه من[صفحة تنزيل Aspose.HTML لـ .NET](https://releases.aspose.com/html/net/).

### 2. إدخال ملف EPUB

ستحتاج إلى ملف EPUB الذي تريد تحويله إلى XPS. تأكد من أن لديك ملف EPUB متاح للتحويل.

### 3. بيئة تطوير .NET

يفترض هذا الدليل أن لديك بيئة تطوير .NET عاملة تم إعدادها على جهازك.

## استيراد مساحة الاسم

للبدء، يجب عليك استيراد مساحة الاسم اللازمة لـ Aspose.HTML:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## تحويل EPUB إلى XPS

دعنا نقسم عملية تحويل ملف EPUB إلى تنسيق XPS إلى خطوات متعددة.

### الخطوة 1.1: افتح ملف EPUB

أولاً، افتح ملف EPUB الموجود للقراءة باستخدام FileStream:

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // تابع عملية التحويل
}
```

### الخطوة 1.2: إنشاء XpsSaveOptions

إنشاء مثيل XpsSaveOptions. تعتبر هذه الخطوة ضرورية لتكوين مخرجات XPS:

```csharp
var options = new XpsSaveOptions();
```

### الخطوة 1.3: تحويل EPUB إلى XPS

الآن، لنستدعي طريقة ConvertEPUB لتحويل EPUB إلى XPS:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## حدد خيارات XPS المخصصة

يمكنك تخصيص مخرجات XPS بشكل أكبر عن طريق تحديد خيارات مخصصة مثل حجم الصفحة ولون الخلفية.

### الخطوة 2.1: حجم الصفحة المخصص ولون الخلفية

قم بإنشاء مثيل لـ XpsSaveOptions بحجم صفحة مخصص ولون خلفية:

```csharp
var options = new XpsSaveOptions()
{
    PageSetup =
    {
        AnyPage = new Page()
        {
            Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
        }
    },
    BackgroundColor = System.Drawing.Color.AliceBlue,
};
```

### الخطوة 2.2: تحويل EPUB إلى XPS باستخدام الخيارات المخصصة

الآن، اتصل بالطريقة ConvertEPUB لتحويل EPUB إلى XPS باستخدام الخيارات المخصصة:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## استخدم موفر الدفق المخصص

في هذه الخطوة، سنقوم بتحويل EPUB إلى XPS باستخدام موفر تدفق مخصص، مما يسمح لك بمعالجة البيانات الناتجة.

### الخطوة 3.1: إنشاء MemoryStreamProvider

إنشاء مثيل لـ MemoryStreamProvider:

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    // تابع عملية التحويل
}
```

### الخطوة 3.2: تحويل EPUB إلى XPS باستخدام موفر البث

تحويل EPUB إلى XPS باستخدام MemoryStreamProvider:

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### الخطوة 3.3: الوصول إلى النتيجة وحفظها

استرجع دفق الذاكرة الذي يحتوي على البيانات المحولة واحفظه في ملف إخراج:

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

### كود مصدر فئة MemoryStreamProvider

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
تهانينا! لقد نجحت في تحويل ملف EPUB إلى تنسيق XPS باستخدام Aspose.HTML لـ .NET.

## خاتمة

في هذا البرنامج التعليمي الشامل، اكتشفنا كيفية الاستفادة من Aspose.HTML for .NET لتحويل ملفات EPUB إلى تنسيق XPS مع خيارات التخصيص المتنوعة. سواء كنت مطورًا متمرسًا أو بدأت للتو، يعمل Aspose.HTML على تبسيط العملية، مما يسمح لك بالتعامل مع تحويلات EPUB إلى XPS بسهولة.

 هل لديك أي أسئلة أو واجهت مشاكل؟ تفحص ال[وثائق Aspose.HTML](https://reference.aspose.com/html/net/) لمزيد من الأفكار أو طلب المساعدة من[منتدى مجتمع Aspose.HTML](https://forum.aspose.com/).

## أسئلة مكررة

### ما هو Aspose.HTML لـ .NET؟
Aspose.HTML for .NET هي مكتبة قوية تمكن المطورين من العمل مع مستندات HTML وEPUB وXPS في تطبيقات .NET.

### أين يمكنني تنزيل Aspose.HTML لـ .NET؟
 يمكنك تنزيل Aspose.HTML لـ .NET من[صفحة التحميل](https://releases.aspose.com/html/net/).

### هل هناك نسخة تجريبية مجانية متاحة لـ Aspose.HTML لـ .NET؟
 نعم، يمكنك الحصول على نسخة تجريبية مجانية من[هنا](https://releases.aspose.com/).

### كيف يمكنني الحصول على ترخيص مؤقت لـ Aspose.HTML لـ .NET؟
 للحصول على ترخيص مؤقت، قم بزيارة[صفحة الترخيص المؤقتة](https://purchase.aspose.com/temporary-license/).

### أين يمكنني العثور على المزيد من البرامج التعليمية والوثائق الخاصة بـ Aspose.HTML لـ .NET؟
استكشف مجموعة واسعة من البرامج التعليمية والوثائق التفصيلية حول[وثائق Aspose.HTML](https://reference.aspose.com/html/net/) صفحة.
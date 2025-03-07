---
title: تحويل EPUB إلى XPS في .NET باستخدام Aspose.HTML
linktitle: تحويل EPUB إلى XPS في .NET
second_title: Aspose.HTML .NET HTML manipulation API
description: تعرف على كيفية تحويل EPUB إلى XPS في .NET باستخدام Aspose.HTML لـ .NET. اتبع دليلنا خطوة بخطوة لإجراء تحويلات سهلة.
weight: 13
url: /ar/net/html-extensions-and-conversions/convert-epub-to-xps/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل EPUB إلى XPS في .NET باستخدام Aspose.HTML


هل تبحث عن طريقة سلسة لتحويل ملفات EPUB إلى تنسيق XPS في تطبيقات .NET الخاصة بك؟ يوفر Aspose.HTML for .NET حلاً قويًا لتحقيق ذلك دون عناء. في هذا الدليل التفصيلي، سنرشدك خلال عملية تحويل EPUB إلى تنسيق XPS باستخدام Aspose.HTML. لنبدأ!

## المتطلبات الأساسية

قبل أن تغوص في عملية تحويل EPUB إلى XPS، ستحتاج إلى التأكد من توفر المتطلبات الأساسية التالية:

### 1. Aspose.HTML لمكتبة .NET

 تأكد من تثبيت مكتبة Aspose.HTML for .NET في مشروعك. إذا لم تقم بذلك، فيمكنك الحصول عليها من[صفحة تنزيل Aspose.HTML لـ .NET](https://releases.aspose.com/html/net/).

### 2. إدخال ملف EPUB

ستحتاج إلى ملف EPUB الذي تريد تحويله إلى XPS. تأكد من توفر ملف EPUB للتحويل.

### 3. بيئة تطوير .NET

يفترض هذا الدليل أن لديك بيئة تطوير .NET عاملة تم إعدادها على جهازك.

## استيراد مساحة الاسم

للبدء، يجب عليك استيراد مساحة الأسماء اللازمة لـ Aspose.HTML:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## تحويل EPUB إلى XPS

دعونا نقوم بتقسيم عملية تحويل ملف EPUB إلى تنسيق XPS إلى خطوات متعددة.

### الخطوة 1.1: افتح ملف EPUB

أولاً، افتح ملف EPUB الموجود للقراءة باستخدام FileStream:

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // متابعة عملية التحويل
}
```

### الخطوة 1.2: إنشاء XpsSaveOptions

قم بإنشاء مثيل لـ XpsSaveOptions. هذه الخطوة مهمة لتكوين إخراج XPS:

```csharp
var options = new XpsSaveOptions();
```

### الخطوة 1.3: تحويل EPUB إلى XPS

الآن، دعنا نستدعي طريقة ConvertEPUB لتحويل EPUB إلى XPS:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## تحديد خيارات XPS المخصصة

بإمكانك تخصيص إخراج XPS بشكل أكبر عن طريق تحديد خيارات مخصصة مثل حجم الصفحة ولون الخلفية.

### الخطوة 2.1: حجم الصفحة المخصص ولون الخلفية

إنشاء مثيل لـ XpsSaveOptions بحجم صفحة مخصص ولون خلفية:

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

### الخطوة 2.2: تحويل EPUB إلى XPS باستخدام خيارات مخصصة

الآن، قم باستدعاء طريقة ConvertEPUB لتحويل EPUB إلى XPS باستخدام الخيارات المخصصة:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## استخدم موفر البث المخصص

في هذه الخطوة، سنقوم بتحويل EPUB إلى XPS باستخدام موفر تدفق مخصص، مما يسمح لك بالتعامل مع البيانات الناتجة.

### الخطوة 3.1: إنشاء MemoryStreamProvider

إنشاء مثيل لـ MemoryStreamProvider:

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    // متابعة عملية التحويل
}
```

### الخطوة 3.2: تحويل EPUB إلى XPS باستخدام Stream Provider

تحويل EPUB إلى XPS باستخدام MemoryStreamProvider:

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### الخطوة 3.3: الوصول إلى النتيجة وحفظها

استرداد مجرى الذاكرة الذي يحتوي على البيانات المحولة وحفظه في ملف إخراج:

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
مبروك! لقد نجحت في تحويل ملف EPUB إلى تنسيق XPS باستخدام Aspose.HTML لـ .NET.

## خاتمة

في هذا البرنامج التعليمي الشامل، استكشفنا كيفية الاستفادة من Aspose.HTML for .NET لتحويل ملفات EPUB إلى تنسيق XPS باستخدام خيارات تخصيص متنوعة. سواء كنت مطورًا متمرسًا أو مبتدئًا، فإن Aspose.HTML يبسط العملية، مما يسمح لك بالتعامل مع تحويلات EPUB إلى XPS بسهولة.

 هل لديك أي أسئلة أو واجهت أي مشكلات؟ تحقق من[توثيق Aspose.HTML](https://reference.aspose.com/html/net/) لمزيد من المعلومات أو طلب المساعدة من[منتدى مجتمع Aspose.HTML](https://forum.aspose.com/).

## الأسئلة الشائعة

### ما هو Aspose.HTML لـ .NET؟
Aspose.HTML for .NET هي مكتبة قوية تتيح للمطورين العمل مع مستندات HTML وEPUB وXPS في تطبيقات .NET.

### أين يمكنني تنزيل Aspose.HTML لـ .NET؟
 يمكنك تنزيل Aspose.HTML لـ .NET من[صفحة التحميل](https://releases.aspose.com/html/net/).

### هل هناك نسخة تجريبية مجانية متاحة لـ Aspose.HTML لـ .NET؟
 نعم، يمكنك الحصول على نسخة تجريبية مجانية من[هنا](https://releases.aspose.com/).

### كيف يمكنني الحصول على ترخيص مؤقت لـ Aspose.HTML لـ .NET؟
 للحصول على رخصة مؤقتة قم بزيارة[صفحة الترخيص المؤقت](https://purchase.aspose.com/temporary-license/).

### أين يمكنني العثور على المزيد من الدروس والوثائق الخاصة بـ Aspose.HTML لـ .NET؟
 استكشف مجموعة واسعة من البرامج التعليمية والوثائق التفصيلية حول[توثيق Aspose.HTML](https://reference.aspose.com/html/net/) صفحة.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

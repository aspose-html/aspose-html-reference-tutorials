---
title: تحويل EPUB إلى صورة في .NET باستخدام Aspose.HTML
linktitle: تحويل EPUB إلى صورة في .NET
second_title: Aspose.HTML .NET HTML manipulation API
description: تعرف على كيفية تحويل EPUB إلى صور باستخدام Aspose.HTML لـ .NET. برنامج تعليمي خطوة بخطوة مع أمثلة التعليمات البرمجية والخيارات القابلة للتخصيص.
type: docs
weight: 11
url: /ar/net/html-extensions-and-conversions/convert-epub-to-image/
---

في العصر الرقمي الحالي، تعد القدرة على التعامل مع تنسيقات المستندات المختلفة وتحويلها مهارة قيمة. يعد Aspose.HTML for .NET أداة قوية تتيح للمطورين العمل مع مستندات HTML وEPUB دون عناء. في هذا البرنامج التعليمي، سنتعمق في عالم Aspose.HTML for .NET وسنرشدك خلال عملية تحويل مستندات EPUB إلى تنسيقات صور مختلفة. سنقوم بتقسيم كل مثال إلى خطوات متعددة، مع شرح كل خطوة على طول الطريق.

## المتطلبات الأساسية

قبل أن نتعمق في عالم Aspose.HTML لـ .NET، يجب عليك التأكد من توفر المتطلبات الأساسية التالية:

1. Visual Studio: تأكد من تثبيت Visual Studio على نظامك. يمكنك تنزيله من موقع الويب.

2.  Aspose.HTML لـ .NET: يمكنك الحصول على المكتبة من موقع Aspose على الويب[هنا](https://releases.aspose.com/html/net/).

3. دليل البيانات الخاص بك: قم بإعداد دليل لتخزين ملفات EPUB الخاصة بك وحيث سيتم حفظ الصور الناتجة.

4. المعرفة الأساسية بلغة C#: تعتبر المعرفة ببرمجة C# ضرورية لفهم وتنفيذ أمثلة التعليمات البرمجية المقدمة في هذا البرنامج التعليمي.

## استيراد المساحات الاسمية الضرورية

قبل أن نبدأ العمل مع Aspose.HTML for .NET، يتعين عليك استيراد المساحات المطلوبة إلى كود C# الخاص بك. توفر هذه المساحات إمكانية الوصول إلى ميزات Aspose.HTML for .NET.

```csharp
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using Aspose.Html.Rendering.Image;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
using System.IO;
using System.Drawing;
using System.Collections.Generic;
```

الآن بعد أن أصبح لدينا المتطلبات الأساسية ومساحات الأسماء في مكانها، دعنا ننتقل إلى الأمثلة خطوة بخطوة.

## تحويل EPUB إلى JPEG

```csharp
    string dataDir = "Your Data Directory";
    // افتح ملف EPUB الموجود للقراءة.
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        // اتصل بطريقة ConvertEPUB لتحويل ملف EPUB إلى صورة.
        Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), "output.jpg");
    }
```
### خطوات

1. قم بتوفير المسار إلى ملف EPUB الخاص بك في المتغير dataDir.
2. افتح ملف EPUB للقراءة باستخدام FileStream.
3. قم باستدعاء طريقة ConvertEPUB، ومرر دفق EPUB، وImageSaveOptions التي تحدد تنسيق الإخراج (JPEG)، واسم ملف الإخراج ("output.jpg").
5. يتم تحويل ملف EPUB إلى صورة JPEG.

في هذا المثال، نفتح ملف EPUB ونقرأ محتواه ونحوله إلى تنسيق صورة JPEG. يتم حفظ الصورة الناتجة بتنسيق "output.jpg".

## تحويل EPUB إلى PNG

يمكنك بسهولة تحويل ملفات EPUB إلى تنسيقات صور مختلفة مثل PNG وBMP وGIF وTIFF باستخدام هياكل أكواد مماثلة. فيما يلي مثال للتحويل إلى PNG:

```csharp

    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Png);
        Converter.ConvertEPUB(stream, options, "output.png");
    }

```
### خطوات
1. افتح ملف EPUB للقراءة باستخدام FileStream.
2. قم بتهيئة كائن ImageSaveOptions باستخدام تنسيق الإخراج المطلوب (في هذه الحالة، PNG).
3. قم باستدعاء طريقة ConvertEPUB، ومرر دفق EPUB، وخيارات حفظ الصورة، واسم ملف الإخراج.
4. يتم تحويل ملف EPUB إلى تنسيق الصورة المحدد.

## تحديد خيارات حفظ الصورة

يمكنك تخصيص إخراج الصورة من خلال تحديد خيارات مثل حجم الصفحة ولون الخلفية. فيما يلي مثال:

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Jpeg)
        {
            PageSetup =
            {
                AnyPage = new Page()
                {
                    Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
                }
            },
            BackgroundColor = Color.AliceBlue,
        };
        Converter.ConvertEPUB(stream, options, "output.jpg");
    }
```
### خطوات

1.  قم بتوفير المسار إلى ملف EPUB الخاص بك في`dataDir` عامل.
2.  افتح ملف EPUB للقراءة باستخدام`FileStream`.
3.  إنشاء`ImageSaveOptions` الكائن وتحديد تنسيق الإخراج المطلوب (JPEG).
4. تخصيص حجم الصفحة ولون الخلفية، إذا لزم الأمر.
5.  اتصل بـ`ConvertEPUB`الطريقة، تمرير دفق EPUB، وخيارات حفظ الصورة، واسم ملف الإخراج.
6. يتم تحويل ملف EPUB إلى صورة باستخدام الخيارات المحددة.

## تحديد موفر دفق مخصص

إذا كنت بحاجة إلى معالجة تدفق الإخراج، فيمكنك استخدام موفر تدفق مخصص. فيما يلي مثال:

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        using (var streamProvider = new MemoryStreamProvider())
        {
            Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), streamProvider);
            
            for (int i = 0; i < streamProvider.Streams.Count; i++)
            {
                var memory = streamProvider.Streams[i];
                memory.Seek(0, SeekOrigin.Begin);
                
                using (FileStream fs = File.Create($"page_{i + 1}.jpg"))
                {
                    memory.CopyTo(fs);
                }
            }
        }
    }

```
كود المصدر لفئة MemoryStreamProvider.

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

### خطوات
1.  قم بتوفير المسار إلى ملف EPUB الخاص بك في`dataDir` عامل.
2.  افتح ملف EPUB للقراءة باستخدام`FileStream`.
3.  إنشاء`MemoryStreamProvider` للتعامل مع تدفقات الإخراج المخصصة.
4.  اتصل بـ`ConvertEPUB` الطريقة، تمرير دفق EPUB، وخيارات حفظ الصورة (JPEG)، ومزود الدفق المخصص.
5. قم بالتكرار خلال تدفقات الذاكرة في الموفر المخصص، ثم احفظها في ملفات فردية.
6. يسمح لك هذا المثال بالتعامل مع تدفقات إخراج متعددة وحفظها حسب الحاجة.

## خاتمة

Aspose.HTML for .NET هي مكتبة متعددة الاستخدامات تبسط العمل مع مستندات EPUB وHTML. بفضل القدرة على تحويل مستندات EPUB إلى تنسيقات صور مختلفة وخيارات قابلة للتخصيص، تقدم مجموعة واسعة من التطبيقات للمطورين.

---

## الأسئلة الشائعة

### 1. أين يمكنني تنزيل Aspose.HTML لـ .NET؟

 يمكنك تنزيل Aspose.HTML لـ .NET من صفحة الإصدارات[هنا](https://releases.aspose.com/html/net/).

### 2. كيف يمكنني الحصول على ترخيص مؤقت لـ Aspose.HTML لـ .NET؟

 للحصول على رخصة مؤقتة قم بزيارة صفحة الرخصة المؤقتة[هنا](https://purchase.aspose.com/temporary-license/).

### 3. أين يمكنني العثور على دعم إضافي لـ Aspose.HTML لـ .NET؟

 لأي أسئلة أو مشكلات، يمكنك طلب المساعدة من مجتمع Aspose في منتدى الدعم[هنا](https://forum.aspose.com/).

### 4. هل يمكنني تحويل مستندات EPUB إلى تنسيقات أخرى مثل PDF أو XPS؟

نعم، يمكنك استخدام Aspose.HTML لـ .NET لتحويل مستندات EPUB إلى تنسيقات مختلفة، بما في ذلك PDF وXPS.

### 5. هل Aspose.HTML لـ .NET مناسب للمشاريع الصغيرة والكبيرة؟

بالتأكيد! تم تصميم Aspose.HTML for .NET ليكون قابلاً للتطوير، مما يجعله خيارًا رائعًا للمشاريع من جميع الأحجام.

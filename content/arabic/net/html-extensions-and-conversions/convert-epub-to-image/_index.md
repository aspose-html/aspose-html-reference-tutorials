---
title: قم بتحويل EPUB إلى صورة في .NET باستخدام Aspose.HTML
linktitle: تحويل EPUB إلى صورة في .NET
second_title: Aspose.HTML .NET واجهة برمجة تطبيقات معالجة HTML
description: تعرف على كيفية تحويل EPUB إلى صور باستخدام Aspose.HTML لـ .NET. برنامج تعليمي خطوة بخطوة مع أمثلة التعليمات البرمجية والخيارات القابلة للتخصيص.
type: docs
weight: 11
url: /ar/net/html-extensions-and-conversions/convert-epub-to-image/
---

في العصر الرقمي الحالي، تعد القدرة على التعامل مع تنسيقات المستندات المختلفة وتحويلها مهارة قيمة. Aspose.HTML for .NET هي أداة قوية تسمح للمطورين بالعمل مع مستندات HTML وEPUB دون عناء. في هذا البرنامج التعليمي، سوف نتعمق في عالم Aspose.HTML لـ .NET ونرشدك خلال عملية تحويل مستندات EPUB إلى تنسيقات صور متنوعة. سنقوم بتقسيم كل مثال إلى خطوات متعددة، مع شرح كل خطوة على طول الطريق.

## المتطلبات الأساسية

قبل أن نتعمق في عالم Aspose.HTML لـ .NET، يجب عليك التأكد من توفر المتطلبات الأساسية التالية:

1. Visual Studio: تأكد من تثبيت Visual Studio على نظامك. يمكنك تنزيله من الموقع.

2.  Aspose.HTML for .NET: يمكنك الحصول على المكتبة من موقع Aspose[هنا](https://releases.aspose.com/html/net/).

3. دليل البيانات الخاص بك: قم بإعداد دليل حيث تقوم بتخزين ملفات EPUB الخاصة بك وحيث سيتم حفظ الصور الناتجة.

4. المعرفة الأساسية بـ C#: يعد الإلمام ببرمجة C# أمرًا ضروريًا لفهم أمثلة التعليمات البرمجية المتوفرة في هذا البرنامج التعليمي وتنفيذها.

## استيراد مساحات الأسماء الضرورية

قبل أن نبدأ العمل مع Aspose.HTML for .NET، تحتاج إلى استيراد مساحات الأسماء المطلوبة إلى كود C# الخاص بك. توفر مساحات الأسماء هذه إمكانية الوصول إلى ميزات Aspose.HTML لـ .NET.

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

الآن بعد أن أصبح لدينا المتطلبات الأساسية ومساحات الأسماء، فلننتقل إلى الأمثلة خطوة بخطوة.

## تحويل EPUB إلى JPEG

```csharp
    string dataDir = "Your Data Directory";
    // افتح ملف EPUB موجود للقراءة.
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        // قم باستدعاء طريقة ConvertEPUB لتحويل ملف EPUB إلى صورة.
        Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), "output.jpg");
    }
```
### خطوات

1. قم بتوفير المسار إلى ملف EPUB الخاص بك في متغير dataDir.
2. افتح ملف EPUB للقراءة باستخدام FileStream.
3. قم باستدعاء الأسلوب ConvertEPUB، وتمرير تدفق EPUB، وImageSaveOptions الذي يحدد تنسيق الإخراج (JPEG)، واسم ملف الإخراج ("output.jpg").
5. يتم تحويل ملف EPUB إلى صورة JPEG.

في هذا المثال، نقوم بفتح ملف EPUB، وقراءة محتواه، وتحويله إلى تنسيق صورة JPEG. يتم حفظ الصورة الناتجة باسم "output.jpg."

## تحويل EPUB إلى PNG

يمكنك بسهولة تحويل ملفات EPUB إلى تنسيقات صور متنوعة مثل PNG وBMP وGIF وTIFF باستخدام هياكل تعليمات برمجية مماثلة. فيما يلي مثال للتحويل إلى PNG:

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
2. قم بتهيئة كائن ImageSaveOptions بتنسيق الإخراج المطلوب (في هذه الحالة، PNG).
3. قم باستدعاء طريقة ConvertEPUB، وتمرير دفق EPUB، وخيارات حفظ الصورة، واسم ملف الإخراج.
4. يتم تحويل ملف EPUB إلى تنسيق الصورة المحدد.

## حدد خيارات حفظ الصورة

يمكنك تخصيص إخراج الصورة عن طريق تحديد خيارات مثل حجم الصفحة ولون الخلفية. هنا مثال:

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

1.  قم بتوفير المسار إلى ملف EPUB الخاص بك في ملف`dataDir` عامل.
2.  افتح ملف EPUB للقراءة باستخدام ملف`FileStream`.
3.  يخترع`ImageSaveOptions` الكائن وحدد تنسيق الإخراج المطلوب (JPEG).
4. قم بتخصيص حجم الصفحة ولون الخلفية، إذا لزم الأمر.
5.  اتصل ب`ConvertEPUB`الطريقة، وتمرير دفق EPUB، وخيارات حفظ الصورة، واسم ملف الإخراج.
6. يتم تحويل ملف EPUB إلى صورة بالخيارات المحددة.

## حدد موفر دفق مخصص

إذا كنت بحاجة إلى معالجة دفق الإخراج، فيمكنك استخدام موفر دفق مخصص. هنا مثال:

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
رمز مصدر فئة MemoryStreamProvider.

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

### خطوات
1.  قم بتوفير المسار إلى ملف EPUB الخاص بك في ملف`dataDir` عامل.
2.  افتح ملف EPUB للقراءة باستخدام ملف`FileStream`.
3.  إنشاء`MemoryStreamProvider` للتعامل مع تدفقات الإخراج المخصصة.
4.  اتصل ب`ConvertEPUB` الطريقة، وتمرير دفق EPUB، وخيارات حفظ الصورة (JPEG)، وموفر الدفق المخصص.
5. قم بالتكرار عبر تدفقات الذاكرة في الموفر المخصص، وحفظها في ملفات فردية.
6. يتيح لك هذا المثال معالجة تدفقات الإخراج المتعددة وحفظها حسب الحاجة.

## خاتمة

Aspose.HTML for .NET هي مكتبة متعددة الاستخدامات تعمل على تبسيط العمل مع مستندات EPUB وHTML. ومع القدرة على تحويل مستندات EPUB إلى تنسيقات صور متنوعة وخيارات قابلة للتخصيص، فإنه يوفر نطاقًا واسعًا من التطبيقات للمطورين.

---

## أسئلة مكررة

### 1. أين يمكنني تنزيل Aspose.HTML لـ .NET؟

 يمكنك تنزيل Aspose.HTML for .NET من صفحة الإصدارات[هنا](https://releases.aspose.com/html/net/).

### 2. كيف يمكنني الحصول على ترخيص مؤقت لـ Aspose.HTML لـ .NET؟

 للحصول على ترخيص مؤقت قم بزيارة صفحة الترخيص المؤقت[هنا](https://purchase.aspose.com/temporary-license/).

### 3. أين يمكنني العثور على دعم إضافي لـ Aspose.HTML لـ .NET؟

 إذا كانت لديك أي أسئلة أو مشكلات، يمكنك طلب المساعدة من مجتمع Aspose في منتدى الدعم[هنا](https://forum.aspose.com/).

### 4. هل يمكنني تحويل مستندات EPUB إلى تنسيقات أخرى مثل PDF أو XPS؟

نعم، يمكنك استخدام Aspose.HTML for .NET لتحويل مستندات EPUB إلى تنسيقات مختلفة، بما في ذلك PDF وXPS.

### 5. هل Aspose.HTML for .NET مناسب لكل من المشاريع الصغيرة والكبيرة الحجم؟

قطعاً! تم تصميم Aspose.HTML for .NET ليكون قابلاً للتطوير، مما يجعله خيارًا رائعًا للمشروعات بجميع أحجامها.

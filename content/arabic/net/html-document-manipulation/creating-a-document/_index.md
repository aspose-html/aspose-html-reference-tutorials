---
title: إنشاء مستند في .NET باستخدام Aspose.HTML
linktitle: إنشاء مستند في .NET
second_title: Aspose.HTML .NET HTML manipulation API
description: أطلق العنان لقوة Aspose.HTML لـ .NET. تعلم كيفية إنشاء مستندات HTML وSVG ومعالجتها وتحسينها بسهولة. استكشف الأمثلة والأسئلة الشائعة خطوة بخطوة.
type: docs
weight: 14
url: /ar/net/html-document-manipulation/creating-a-document/
---

في عالم تطوير الويب المتطور باستمرار، يعد البقاء في المقدمة أمرًا ضروريًا. توفر Aspose.HTML for .NET للمطورين مجموعة أدوات قوية للعمل مع مستندات HTML. سواء كنت تبدأ من الصفر، أو تقوم بالتحميل من ملف، أو تسحب من عنوان URL، أو تتعامل مع مستندات SVG، فإن هذه المكتبة توفر التنوع الذي تحتاجه.

في هذا الدليل التفصيلي، سنتعمق في أساسيات استخدام Aspose.HTML لـ .NET، مما يضمن لك التجهيز الجيد لاستخدام هذه الأداة القوية في مشاريع تطوير الويب الخاصة بك. قبل أن نتعمق في التفاصيل، دعنا نستعرض المتطلبات الأساسية ومساحات الأسماء الضرورية لبدء رحلتك.

## المتطلبات الأساسية

لمتابعة هذا البرنامج التعليمي بنجاح والاستفادة من قوة Aspose.HTML لـ .NET، ستحتاج إلى المتطلبات الأساسية التالية:

- جهاز كمبيوتر يعمل بنظام Windows مع تثبيت .NET Framework أو .NET Core.
- محرر أكواد مثل Visual Studio.
- المعرفة الأساسية لبرمجة C#.

الآن بعد أن أصبحت المتطلبات الأساسية جاهزة، فلنبدأ.

## استيراد المساحات الاسمية

قبل أن تبدأ في استخدام Aspose.HTML لـ .NET، تحتاج إلى استيراد المساحات الأساسية اللازمة. تحتوي هذه المساحات الأساسية على فئات وطرق ضرورية للعمل مع مستندات HTML. فيما يلي قائمة بالمساحات الأساسية التي يجب عليك استيرادها:

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

بعد استيراد هذه المساحات الأساسية، أصبحت الآن جاهزًا للانتقال إلى الأمثلة خطوة بخطوة.

## إنشاء مستند HTML من الصفر

### الخطوة 1: تهيئة مستند HTML فارغ

```csharp
// تهيئة مستند HTML فارغ.
using (var document = new Aspose.Html.HTMLDocument())
{
    // إنشاء عنصر نص وإضافته إلى المستند
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // حفظ المستند على القرص.
    document.Save("document.html");
}
```

في هذا المثال، نبدأ بإنشاء مستند HTML فارغ وإضافة نص "Hello World!" إليه. ثم نحفظ المستند في ملف.

## إنشاء مستند HTML من ملف

### الخطوة 1: إعداد ملف "document.html"

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### الخطوة 2: التحميل من ملف "document.html"

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // اكتب محتوى المستند في مجرى الإخراج.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

هنا، نقوم بإعداد ملف يحتوي على محتوى "Hello World!" ثم نقوم بتحميله كمستند HTML. نقوم بطباعة محتوى المستند على وحدة التحكم.

## إنشاء مستند HTML من عنوان URL

### الخطوة 1: تحميل مستند من صفحة الويب

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    // اكتب محتوى المستند في مجرى الإخراج.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

في هذا المثال، نقوم بتحميل مستند HTML مباشرة من صفحة الويب وعرض محتواه.

## إنشاء مستند HTML من سلسلة

### الخطوة 1: إعداد كود HTML

```csharp
var html_code = "<p>Hello World!</p>";
```

### الخطوة 2: تهيئة المستند من متغير السلسلة

```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // حفظ المستند على القرص.
    document.Save("document.html");
}
```

هنا، نقوم بإنشاء مستند HTML من متغير سلسلة وحفظه في ملف.

## إنشاء مستند HTML من MemoryStream

### الخطوة 1: إنشاء كائن تدفق الذاكرة

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    // اكتب كود HTML في كائن الذاكرة
    sw.Write("<p>Hello World!</p>");
    // ضبط الموضع إلى البداية
    sw.Flush();
    mem.Seek(0, System.IO.SeekOrigin.Begin);
    // تهيئة المستند من مجرى الذاكرة
    using (var document = new Aspose.Html.HTMLDocument(mem, "."))
    {
        // حفظ المستند على القرص.
        document.Save("document.html");
    }
}
```

في هذا المثال، نقوم بإنشاء مستند HTML من مجرى ذاكرة وحفظه في ملف.

## العمل مع مستندات SVG

### الخطوة 1: تهيئة مستند SVG من سلسلة

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "."))
{
    // اكتب محتوى المستند في مجرى الإخراج.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

هنا، نقوم بإنشاء وعرض مستند SVG من سلسلة.

## تحميل مستند HTML بشكل غير متزامن

### الخطوة 1: إنشاء مثيل لمستند HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### الخطوة 2: الاشتراك في الحدث 'ReadyStateChange'

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    // تحقق من قيمة الخاصية 'ReadyState'.
    if (document.ReadyState == "complete")
    {
        Console.WriteLine(document.DocumentElement.OuterHTML);
        Console.WriteLine("Loading is completed. Press any key to continue...");
    }
};
```

### الخطوة 3: التنقل بشكل غير متزامن في عنوان Uri المحدد

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

في هذا المثال، نقوم بتحميل مستند HTML بشكل غير متزامن ونقوم بمعالجة الحدث 'ReadyStateChange' لعرض المحتوى عند اكتمال التحميل.

## التعامل مع حدث "OnLoad"

### الخطوة 1: إنشاء مثيل لمستند HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### الخطوة 2: الاشتراك في حدث "OnLoad"

```csharp
document.OnLoad += (sender, @event) =>
{
    Console.WriteLine(document.DocumentElement.OuterHTML);
    Console.WriteLine("Loading is completed. Press any key to continue...");
};
```

### الخطوة 3: التنقل بشكل غير متزامن في عنوان Uri المحدد

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

يوضح هذا المثال تحميل مستند HTML بشكل غير متزامن ومعالجة الحدث "OnLoad" لعرض المحتوى عند الانتهاء.

## ختاماً

في عالم تطوير الويب الديناميكي، يعد امتلاك الأدوات المناسبة أمرًا بالغ الأهمية. يزودك Aspose.HTML for .NET بالوسائل اللازمة لإنشاء مستندات HTML وSVG ومعالجتها ومعالجتها بكفاءة. لقد شرح لك هذا الدليل الشامل الأساسيات، مما يضمن لك إمكانية الاستفادة من قوة Aspose.HTML for .NET في مشاريعك.

## الأسئلة الشائعة

### س1: ما هو Aspose.HTML لـ .NET؟

A1: Aspose.HTML for .NET هي مكتبة .NET قوية تتيح للمطورين العمل مع مستندات HTML وSVG. وهي توفر مجموعة واسعة من الميزات، بدءًا من إنشاء المستندات من البداية وحتى تحليل ملفات HTML وSVG الموجودة ومعالجتها.

### س2: هل يمكنني استخدام Aspose.HTML لـ .NET مع .NET Core؟

ج2: نعم، يعد Aspose.HTML for .NET متوافقًا مع كل من .NET Framework و.NET Core، مما يجعله خيارًا متعدد الاستخدامات لتطبيقات .NET الحديثة.

### س3: هل Aspose.HTML for .NET مناسب لكشط الويب وتحليله؟

ج3: بالتأكيد! يعد Aspose.HTML for .NET خيارًا ممتازًا لمهام كشط وتحليل الويب، وذلك بفضل قدرته على تحميل مستندات HTML من عناوين URL والسلاسل. يمكنك استخراج البيانات وإجراء التحليلات والمزيد.

### س4: كيف يمكنني الوصول إلى الدعم لـ Aspose.HTML لـ .NET؟

 ج4: إذا واجهت أي مشكلات أو كانت لديك أسئلة أثناء استخدام Aspose.HTML لـ .NET، فيمكنك زيارة[منتدى اسبوس](https://forum.aspose.com/) للحصول على الدعم والمساعدة من المجتمع وخبراء Aspose.

### ج5: أين يمكنني العثور على الوثائق التفصيلية وخيارات التنزيل؟

ج5: للحصول على توثيق شامل والوصول إلى خيارات التنزيل، يمكنك الرجوع إلى الروابط التالية:

- [التوثيق](https://reference.aspose.com/html/net/)
- [تحميل](https://releases.aspose.com/html/net/)
- [يشتري](https://purchase.aspose.com/buy)
- [نسخة تجريبية مجانية](https://releases.aspose.com/)
- [رخصة مؤقتة](https://purchase.aspose.com/temporary-license/)
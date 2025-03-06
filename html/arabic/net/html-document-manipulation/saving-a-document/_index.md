---
title: حفظ مستند في .NET باستخدام Aspose.HTML
linktitle: حفظ مستند في .NET
second_title: Aspose.HTML .NET HTML manipulation API
description: اكتشف قوة Aspose.HTML لـ .NET من خلال دليلنا خطوة بخطوة. تعلم كيفية إنشاء مستندات HTML وSVG ومعالجتها وتحويلها
weight: 16
url: /ar/net/html-document-manipulation/saving-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# حفظ مستند في .NET باستخدام Aspose.HTML


في العصر الرقمي الحالي، يعد إنشاء ومعالجة مستندات HTML وSVG أمرًا ضروريًا للعديد من مطوري البرامج والشركات. Aspose.HTML for .NET هي مكتبة قوية تبسط هذه المهام، وتقدم وظائف متنوعة للعمل مع HTML وSVG والمزيد. في هذا الدليل الشامل، سنتعمق في أساسيات Aspose.HTML for .NET، ونقسم كل مثال إلى خطوات سهلة المتابعة. سواء كنت مطورًا متمرسًا أو بدأت للتو، فستجد هذا الدليل لا يقدر بثمن للاستفادة من إمكانيات Aspose.HTML.

## المتطلبات الأساسية

قبل أن نبدأ هذه الرحلة، دعونا نتأكد من أن لديك كل ما تحتاجه:

- بيئة التطوير: تأكد من تثبيت Visual Studio أو أي بيئة تطوير .NET أخرى على جهاز الكمبيوتر لديك.

- Aspose.HTML for .NET: تحتاج إلى الحصول على مكتبة Aspose.HTML for .NET. يمكنك تنزيلها من[هنا](https://releases.aspose.com/html/net/).

- معرفة لغة البرمجة C#: إن معرفة لغة البرمجة C# مفيدة ولكنها ليست إلزامية. تم تصميم هذا الدليل ليكون مناسبًا للمبتدئين.

## استيراد مساحة الاسم

للبدء في استخدام Aspose.HTML لـ .NET، ستحتاج إلى استيراد المساحات الاسمية اللازمة إلى مشروعك. في كود C# الخاص بك، قم بتضمين المساحة الاسمية التالية:

### الخطوة 1: استيراد مساحة اسم Aspose.HTML
```csharp
using Aspose.Html;
```

ستتيح لك هذه المساحة الاسمية الوصول إلى إمكانيات معالجة HTML وSVG المختلفة.

## HTML إلى ملف

### الخطوة 1: تهيئة مستند HTML فارغ
```csharp
// تهيئة مستند HTML فارغ.
using (var document = new Aspose.Html.HTMLDocument())
{
    // إنشاء عنصر نص وإضافته إلى المستند
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // احفظ HTML في الملف الموجود على القرص.
    document.Save("document.html");
}
```

في هذا المثال، نقوم بإنشاء مستند HTML وإضافة نص بسيط إليه وهو "Hello World!". ثم نقوم بحفظ النص HTML في ملف على القرص.

## HTML بدون ملف مرتبط

### الخطوة 1: إعداد ملف HTML بسيط
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

هنا، نقوم بإنشاء ملف HTML أساسي يحتوي على رابط لملف آخر.

### الخطوة 2: تحميل 'document.html' في الذاكرة
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // إنشاء مثيل لخيارات الحفظ
    var options = new Aspose.Html.Saving.HTMLSaveOptions();
    //قم بتعيين الحد الأقصى لعمق المعالجة إلى 0 لقطع ملفات HTML المرتبطة.
    options.ResourceHandlingOptions.MaxHandlingDepth = 0;
    // حفظ المستند
    document.Save(@".\html-to-file-example\document.html", options);
}
```

في هذا المثال، نقوم بتحميل مستند HTML إلى الذاكرة، وتعيين أقصى عمق معالجة لقطع الملفات المرتبطة، وحفظ المستند. 

## HTML إلى MHTML

### الخطوة 1: إعداد ملف HTML بسيط
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

تمامًا كما هو الحال في المثال 2، نقوم بإنشاء ملف HTML أساسي يحتوي على رابط أساسي لملف آخر.

### الخطوة 2: تحميل 'document.html' في الذاكرة وحفظه بتنسيق MHTML
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // حفظ المستند بصيغة MHTML
    document.Save(@".\html-to-file-example\document.mht", Aspose.Html.Saving.HTMLSaveFormat.MHTML);
}
```

هنا، نقوم بتحميل مستند HTML إلى الذاكرة وحفظه بتنسيق MHTML.

## HTML إلى Markdown

### الخطوة 1: إعداد كود HTML
```csharp
var html_code = "<H2>Hello World!</H2>";
```

 في هذه الخطوة، نقوم بتعريف مقتطف من كود HTML يحتوي على`<H2>` عنصر.

### الخطوة 2: تهيئة المستند من كود HTML وحفظه بتنسيق Markdown
```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // احفظ المستند كملف Markdown.
    document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
}
```

نقوم بإنشاء مستند HTML من مقتطف الكود ونحفظه كملف Markdown.

## SVG إلى ملف

### الخطوة 1: إعداد كود SVG
```csharp
var code = @"
    <svg xmlns='http://www.w3.org/2000/svg' الارتفاع='80' العرض='300'>
        <g fill='none'>
            <path stroke='red' d='M5 20 l215 0' />
            <path stroke='black' d='M5 40 l215 0' />
            <path stroke='blue' d='M5 60 l215 0' />
        </g>
    </svg>";
```

هنا، نقوم بإنشاء كود SVG يرسم رسمًا بيانيًا بسيطًا وملونًا.

### الخطوة 2: تهيئة مستند SVG من الكود وحفظه على القرص
```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument(code, "."))
{
    // حفظ ملف SVG على القرص
    document.Save("document.svg");
}
```

في هذه الخطوة، نقوم بإنشاء مستند SVG من الكود وحفظه كملف SVG.

## خاتمة

Aspose.HTML for .NET هي مكتبة متعددة الاستخدامات تعمل على تبسيط التعامل مع مستندات HTML وSVG في تطبيقات .NET. في هذا الدليل، قمنا بتغطية خمسة أمثلة أساسية، وقمنا بتقسيم كل منها إلى تعليمات خطوة بخطوة. سواء كنت تقوم بإنشاء مستندات أو معالجتها أو تحويلها، فإن Aspose.HTML يغطيك. باتباع هذه الخطوات، ستكون على الطريق الصحيح لإتقان هذه الأداة القوية.

## الأسئلة الشائعة

### س1: ما هو Aspose.HTML لـ .NET؟

A1: Aspose.HTML for .NET هي مكتبة .NET توفر مجموعة واسعة من الميزات للعمل مع مستندات HTML وSVG، بما في ذلك الإنشاء والمعالجة والتحويل.

### س2: أين يمكنني تنزيل Aspose.HTML لـ .NET؟

 A2: يمكنك تنزيل Aspose.HTML لـ .NET من[هنا](https://releases.aspose.com/html/net/).

### س3: هل Aspose.HTML لـ .NET مناسب للمبتدئين؟

ج3: نعم، يمكن للمبتدئين والمطورين ذوي الخبرة استخدام Aspose.HTML for .NET. تم تصميم الأمثلة في هذا الدليل لتكون سهلة الاستخدام للمبتدئين.

### س4: هل يمكنني تحويل HTML إلى تنسيقات أخرى باستخدام Aspose.HTML لـ .NET؟

ج4: نعم، يدعم Aspose.HTML لـ .NET التحويل إلى تنسيقات مختلفة، بما في ذلك MHTML وMarkdown، كما هو موضح في الأمثلة.

### س5: أين يمكنني الحصول على الدعم لـ Aspose.HTML لـ .NET؟

 ج5: يمكنك العثور على الدعم والإجابات على أسئلتك في منتدى مجتمع Aspose.HTML[هنا](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

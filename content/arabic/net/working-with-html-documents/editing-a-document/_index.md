---
title: تحرير مستند في .NET باستخدام Aspose.HTML
linktitle: تحرير مستند في .NET
second_title: Aspose.HTML .NET واجهة برمجة تطبيقات معالجة HTML
description: تعرف على كيفية العمل مع مستندات HTML في .NET باستخدام Aspose.HTML. يغطي هذا البرنامج التعليمي الشامل إنشاء المستندات ومعالجتها وتصميمها. نبدأ الآن!
type: docs
weight: 12
url: /ar/net/working-with-html-documents/editing-a-document/
---

مرحبًا بك في برنامجنا التعليمي حول استخدام Aspose.HTML for .NET، وهي أداة قوية للتعامل مع مستندات HTML في تطبيقات .NET الخاصة بك. في هذا البرنامج التعليمي، سنرشدك عبر الخطوات الأساسية للعمل مع مستندات HTML باستخدام Aspose.HTML. سواء كنت مطورًا متمرسًا أو بدأت للتو في تطوير .NET، سيساعدك هذا الدليل على الاستفادة من الإمكانات الكاملة لـ Aspose.HTML لمشروعاتك.

## المتطلبات الأساسية

قبل أن نتعمق في أمثلة التعليمات البرمجية، تأكد من توفر المتطلبات الأساسية التالية:

1. Visual Studio: ستحتاج إلى تثبيت Visual Studio على جهازك لمتابعة الأمثلة.

2.  Aspose.HTML لـ .NET: يجب أن يكون لديك Aspose.HTML لمكتبة .NET مثبتة. يمكنك تنزيله من[هنا](https://releases.aspose.com/html/net/).

3. الفهم الأساسي لـ C#: الإلمام ببرمجة C# سيكون مفيدًا، ولكن حتى لو كنت جديدًا في C#، فلا يزال بإمكانك المتابعة والتعلم.

## استيراد مساحات الأسماء الضرورية

لبدء استخدام Aspose.HTML لـ .NET، تحتاج إلى استيراد مساحات الأسماء المطلوبة. وإليك كيف يمكنك القيام بذلك:

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.Dom.Css;
```

الآن بعد أن انتهيت من تغطية المتطلبات الأساسية، دعنا نقسم كل مثال إلى خطوات متعددة ونشرح كل خطوة بالتفصيل.

## المثال 1: إنشاء وتحرير مستند HTML

```csharp
static void EditDocumentTree()
{
    using (var document = new Aspose.Html.HTMLDocument())
    {
        var body = document.Body;
        // إنشاء عنصر الفقرة
        var p = (Aspose.Html.HTMLParagraphElement)document.CreateElement("p");
        // تعيين سمة مخصصة
        p.SetAttribute("id", "my-paragraph");
        // إنشاء عقدة نصية
        var text = document.CreateTextNode("my first paragraph");
        // إرفاق النص بالفقرة
        p.AppendChild(text);
        // إرفاق فقرة بنص الوثيقة
        body.AppendChild(p);
    }
}
```

### توضيح:

1.  نبدأ بإنشاء مستند HTML جديد باستخدام`Aspose.Html.HTMLDocument()`.

2. نصل إلى عنصر نص الوثيقة.

3. بعد ذلك، نقوم بإنشاء عنصر فقرة HTML (`<p>` ) استخدام`document.CreateElement("p")`.

4.  قمنا بتعيين سمة مخصصة`id` لعنصر الفقرة

5.  يتم إنشاء عقدة نصية باستخدام`document.CreateTextNode("my first paragraph")`.

6.  نعلق عقدة النص على عنصر الفقرة باستخدام`p.AppendChild(text)`.

7. وأخيرا، نعلق الفقرة على متن الوثيقة.

يوضح هذا المثال كيفية إنشاء بنية مستند HTML ومعالجتها.

## المثال 2: إزالة عنصر من مستند HTML

```csharp
static void EditDocumentTreeWithAppendRemoveChild()
{
    using (var document = new Aspose.Html.HTMLDocument("<p>paragraph</p><div>some element to remove</div>", "about:blank"))
    {
        var body = document.Body;
        // احصل على عنصر "div".
        var div = (Aspose.Html.HTMLDivElement)body.GetElementsByTagName("div").First();
        // قم بإزالة العنصر الذي تم العثور عليه
        body.RemoveChild(div);
    }
}
```

### توضيح:

1.  نقوم بإنشاء وثيقة HTML مع العناصر الموجودة، بما في ذلك`<p>` و أ`<div>`.

2. نصل إلى عنصر نص الوثيقة.

3.  استخدام`body.GetElementsByTagName("div").First()` ، نستعيد الأول`<div>` عنصر في الوثيقة

4.  نقوم بإزالة المحدد`<div>` عنصر من نص الوثيقة باستخدام`body.RemoveChild(div)`.

يوضح هذا المثال كيفية التعامل مع العناصر وإزالتها من مستند HTML موجود.

## المثال 3: تحرير محتوى HTML

```csharp
static void EditHtml()
{
    using (var document = new Aspose.Html.HTMLDocument())
    {
        // الحصول على عنصر الجسم
        var body = document.Body;
        // ضبط محتوى عنصر الجسم
        body.InnerHTML = "<p>paragraph</p>";
        // الانتقال إلى الطفل الأول
        var node = body.FirstChild;
        System.Console.WriteLine(node.LocalName);
    }
}
```

### توضيح:

1. نقوم بإنشاء مستند HTML جديد.

2. نصل إلى عنصر نص الوثيقة.

3.  استخدام`body.InnerHTML` ، قمنا بتعيين محتوى HTML للنص على`<p>paragraph</p>`.

4.  نقوم باسترجاع العنصر الطفل الأول من الجسم باستخدام`body.FirstChild`.

5. نقوم بطباعة الاسم المحلي للعنصر الفرعي الأول إلى وحدة التحكم.

يوضح هذا المثال كيفية تعيين واسترداد محتوى HTML لعنصر داخل مستند HTML.

## المثال 4: تحرير أنماط العناصر

```csharp
static void EditElementStyle()
{
    using (var document = new Aspose.Html.HTMLDocument("<style>p { color: red; }</style><p>my first paragraph</p>", "about:blank"))
    {
        // الحصول على العنصر للتفتيش
        var element = document.GetElementsByTagName("p")[0];
        // احصل على كائن عرض CSS
        var view = (Aspose.Html.Dom.Css.IViewCSS)document.Context.Window;
        // احصل على النمط المحسوب للعنصر
        var declaration = view.GetComputedStyle(element);
        // احصل على قيمة خاصية "اللون".
        System.Console.WriteLine(declaration.Color); // رغب (255، 0، 0)
    }
}
```

### توضيح:

1.  نقوم بإنشاء مستند HTML باستخدام CSS مضمن يحدد لونه`<p>` العناصر إلى اللون الأحمر.

2.  نقوم باسترجاع`<p>` العنصر باستخدام`document.GetElementsByTagName("p")[0]`.

3.  نحن نصل إلى كائن عرض CSS ونحصل على النمط المحسوب لـ`<p>` عنصر.

4. نقوم باسترجاع وطباعة قيمة خاصية "اللون"، والتي تم ضبطها على اللون الأحمر في CSS.

يوضح هذا المثال كيفية فحص ومعالجة أنماط CSS لعناصر HTML.

## المثال 5: تغيير نمط العنصر باستخدام السمات

```csharp
static void EditElementStyleUsingAttribute()
{
    using (var document = new Aspose.Html.HTMLDocument("<style>p { color: red; }</style><p>my first paragraph</p>", "about:blank"))
    {
        // احصل على العنصر لتحريره
        var element = (Aspose.Html.HTMLElement)document.GetElementsByTagName("p")[0];
        // احصل على كائن عرض CSS
        var view = (Aspose.Html.Dom.Css.IViewCSS)document.Context.Window;
        // احصل على النمط المحسوب للعنصر
        var declaration = view.GetComputedStyle(element);
        // تعيين اللون الأخضر
        element.Style.Color = "green";
        // احصل على قيمة خاصية "اللون".
        System.Console.WriteLine(declaration.Color); // رغب (0، 128، 0)
    }
}
```

### توضيح:

1.  نقوم بإنشاء مستند HTML باستخدام CSS مضمن يحدد لونه`<p>` العناصر إلى اللون الأحمر.

2.  نقوم باسترجاع`<p>` العنصر باستخدام`document.GetElementsByTagName("p")[0]`.

3.  نحن نصل إلى كائن عرض CSS ونحصل على النمط المحسوب لـ`<p>` العنصر قبل أي تغييرات.

4.  نقوم بتغيير لون`<p>` عنصر إلى اللون الأخضر باستخدام`element.Style.Color = "green"`.

5. نقوم باسترجاع وطباعة القيمة المحدثة لـ "اللون"

 الملكية التي أصبحت الآن خضراء.

يوضح هذا المثال كيفية تعديل نمط عنصر HTML مباشرةً باستخدام السمات.

## خاتمة

في هذا البرنامج التعليمي، قمنا بتغطية أساسيات استخدام Aspose.HTML لـ .NET لإنشاء مستندات HTML ومعالجتها وتصميمها داخل تطبيقات .NET الخاصة بك. لقد استكشفنا أمثلة مختلفة، بدءًا من إنشاء مستند HTML وحتى تحرير بنيته وأنماطه. باستخدام هذه المهارات، يمكنك التعامل مع مستندات HTML بفعالية في مشاريع .NET الخاصة بك.

 إذا كان لديك أي أسئلة أو كنت بحاجة إلى مزيد من المساعدة، فلا تتردد في زيارة[Aspose.HTML لوثائق .NET](https://reference.aspose.com/html/net/) أو طلب المساعدة على[منتدى Aspose](https://forum.aspose.com/).

---

## الأسئلة المتداولة (الأسئلة الشائعة)

### ما هو Aspose.HTML لـ .NET؟
Aspose.HTML for .NET هي مكتبة قوية للعمل مع مستندات HTML في تطبيقات .NET.

### أين يمكنني تنزيل Aspose.HTML لـ .NET؟
 يمكنك تنزيل Aspose.HTML لـ .NET من[هنا](https://releases.aspose.com/html/net/).

### هل هناك نسخة تجريبية مجانية متاحة؟
 نعم، يمكنك الحصول على نسخة تجريبية مجانية من Aspose.HTML من[هنا](https://releases.aspose.com/).

### كيف يمكنني شراء ترخيص؟
 لشراء ترخيص، قم بزيارة[هذا الرابط](https://purchase.aspose.com/buy).

### هل أحتاج إلى خبرة سابقة في استخدام HTML لاستخدام Aspose.HTML لـ .NET؟
على الرغم من أن المعرفة بـ HTML مفيدة، إلا أنه يمكنك استخدام Aspose.HTML لـ .NET حتى لو لم تكن خبيرًا في HTML.


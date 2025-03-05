---
title: تحرير مستند في .NET باستخدام Aspose.HTML
linktitle: تحرير مستند في .NET
second_title: Aspose.HTML .NET HTML manipulation API
description: تعرف على كيفية التعامل مع مستندات HTML في .NET باستخدام Aspose.HTML. يغطي هذا البرنامج التعليمي الشامل إنشاء المستندات ومعالجتها وتصميمها. ابدأ الآن!
type: docs
weight: 12
url: /ar/net/working-with-html-documents/editing-a-document/
---

مرحبًا بك في البرنامج التعليمي الخاص بنا حول استخدام Aspose.HTML لـ .NET، وهي أداة قوية للتعامل مع مستندات HTML في تطبيقات .NET الخاصة بك. في هذا البرنامج التعليمي، سنأخذك خلال الخطوات الأساسية للعمل مع مستندات HTML باستخدام Aspose.HTML. سواء كنت مطورًا متمرسًا أو بدأت للتو في تطوير .NET، سيساعدك هذا الدليل على الاستفادة الكاملة من إمكانات Aspose.HTML في مشاريعك.

## المتطلبات الأساسية

قبل أن نتعمق في أمثلة التعليمات البرمجية، تأكد من توفر المتطلبات الأساسية التالية:

1. Visual Studio: ستحتاج إلى تثبيت Visual Studio على جهازك لمتابعة الأمثلة.

2.  Aspose.HTML for .NET: يجب أن يكون لديك مكتبة Aspose.HTML for .NET مثبتة. يمكنك تنزيلها من[هنا](https://releases.aspose.com/html/net/).

3. فهم أساسي لـ C#: سيكون من المفيد التعرف على برمجة C#، ولكن حتى إذا كنت جديدًا على C#، فلا يزال بإمكانك المتابعة والتعلم.

## استيراد المساحات الاسمية الضرورية

للبدء في استخدام Aspose.HTML لـ .NET، تحتاج إلى استيراد المساحات المطلوبة. إليك كيفية القيام بذلك:

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.Dom.Css;
```

الآن بعد أن قمت بتغطية المتطلبات الأساسية، دعنا نقسم كل مثال إلى خطوات متعددة ونشرح كل خطوة بالتفصيل.

## المثال 1: إنشاء مستند HTML وتحريره

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
        // إرفاق فقرة بنص المستند
        body.AppendChild(p);
    }
}
```

### توضيح:

1.  نبدأ بإنشاء مستند HTML جديد باستخدام`Aspose.Html.HTMLDocument()`.

2. نقوم بالوصول إلى عنصر نص المستند.

3. بعد ذلك، نقوم بإنشاء عنصر فقرة HTML (`<p>` ) استخدام`document.CreateElement("p")`.

4.  لقد قمنا بتعيين سمة مخصصة`id` لعنصر الفقرة.

5.  يتم إنشاء عقدة نصية باستخدام`document.CreateTextNode("my first paragraph")`.

6.  نقوم بربط عقدة النص بعنصر الفقرة باستخدام`p.AppendChild(text)`.

7. وأخيرًا، نقوم بربط الفقرة بجسم المستند.

يوضح هذا المثال كيفية إنشاء هيكل مستند HTML والتلاعب به.

## المثال 2: إزالة عنصر من مستند HTML

```csharp
static void EditDocumentTreeWithAppendRemoveChild()
{
    using (var document = new Aspose.Html.HTMLDocument("<p>paragraph</p><div>some element to remove</div>", "about:blank"))
    {
        var body = document.Body;
        // الحصول على عنصر "div"
        var div = (Aspose.Html.HTMLDivElement)body.GetElementsByTagName("div").First();
        // إزالة العنصر الموجود
        body.RemoveChild(div);
    }
}
```

### توضيح:

1.  نقوم بإنشاء مستند HTML بالعناصر الموجودة، بما في ذلك`<p>` و أ`<div>`.

2. نقوم بالوصول إلى عنصر نص المستند.

3.  استخدام`body.GetElementsByTagName("div").First()` ، نستعيد الأول`<div>` عنصر في الوثيقة.

4.  نقوم بإزالة المحدد`<div>` عنصر من نص المستند باستخدام`body.RemoveChild(div)`.

يوضح هذا المثال كيفية التعامل مع العناصر وإزالتها من مستند HTML موجود.

## المثال 3: تحرير محتوى HTML

```csharp
static void EditHtml()
{
    using (var document = new Aspose.Html.HTMLDocument())
    {
        // الحصول على عنصر الجسم
        var body = document.Body;
        // تعيين محتوى عنصر الجسم
        body.InnerHTML = "<p>paragraph</p>";
        // انتقل إلى الطفل الأول
        var node = body.FirstChild;
        System.Console.WriteLine(node.LocalName);
    }
}
```

### توضيح:

1. نقوم بإنشاء مستند HTML جديد.

2. نقوم بالوصول إلى عنصر نص المستند.

3.  استخدام`body.InnerHTML` ، قمنا بتعيين محتوى HTML للجسم إلى`<p>paragraph</p>`.

4.  نحن نستعيد أول عنصر طفل في الجسم باستخدام`body.FirstChild`.

5. نقوم بطباعة الاسم المحلي للعنصر الفرعي الأول في وحدة التحكم.

يوضح هذا المثال كيفية تعيين واسترجاع محتوى HTML لعنصر داخل مستند HTML.

## المثال 4: تحرير أنماط العناصر

```csharp
static void EditElementStyle()
{
    using (var document = new Aspose.Html.HTMLDocument("<style>p { color: red; }</style><p>my first paragraph</p>", "about:blank"))
    {
        // احصل على العنصر للتفتيش
        var element = document.GetElementsByTagName("p")[0];
        // الحصول على كائن عرض CSS
        var view = (Aspose.Html.Dom.Css.IViewCSS)document.Context.Window;
        // احصل على النمط المحسوب للعنصر
        var declaration = view.GetComputedStyle(element);
        // الحصول على قيمة خاصية "اللون"
        System.Console.WriteLine(declaration.Color); // اللون الأحمر والأخضر والأزرق(255، 0، 0)
    }
}
```

### توضيح:

1.  نقوم بإنشاء مستند HTML باستخدام CSS مضمن يحدد لون`<p>` العناصر باللون الأحمر.

2.  نحن نستعيد`<p>` عنصر باستخدام`document.GetElementsByTagName("p")[0]`.

3.  نقوم بالوصول إلى كائن عرض CSS والحصول على النمط المحسوب لـ`<p>` عنصر.

4. نقوم باسترجاع وطباعة قيمة خاصية "اللون" والتي تم تعيينها على اللون الأحمر في CSS.

يوضح هذا المثال كيفية فحص أنماط CSS لعناصر HTML ومعالجتها.

## المثال 5: تغيير نمط العنصر باستخدام السمات

```csharp
static void EditElementStyleUsingAttribute()
{
    using (var document = new Aspose.Html.HTMLDocument("<style>p { color: red; }</style><p>my first paragraph</p>", "about:blank"))
    {
        // احصل على العنصر لتحريره
        var element = (Aspose.Html.HTMLElement)document.GetElementsByTagName("p")[0];
        // الحصول على كائن عرض CSS
        var view = (Aspose.Html.Dom.Css.IViewCSS)document.Context.Window;
        // احصل على النمط المحسوب للعنصر
        var declaration = view.GetComputedStyle(element);
        // تعيين اللون الأخضر
        element.Style.Color = "green";
        // الحصول على قيمة خاصية "اللون"
        System.Console.WriteLine(declaration.Color); // اللون الأحمر والأخضر والأزرق(0، 128، 0)
    }
}
```

### توضيح:

1.  نقوم بإنشاء مستند HTML باستخدام CSS مضمن يحدد لون`<p>` العناصر باللون الأحمر.

2.  نحن نستعيد`<p>` عنصر باستخدام`document.GetElementsByTagName("p")[0]`.

3.  نقوم بالوصول إلى كائن عرض CSS والحصول على النمط المحسوب لـ`<p>` العنصر قبل أي تغييرات.

4.  نحن نغير لون`<p>` العنصر إلى اللون الأخضر باستخدام`element.Style.Color = "green"`.

5. نقوم باسترجاع وطباعة القيمة المحدثة لـ "اللون"

 الممتلكات التي أصبحت الآن خضراء.

يوضح هذا المثال كيفية تعديل نمط عنصر HTML بشكل مباشر باستخدام السمات.

## خاتمة

في هذا البرنامج التعليمي، قمنا بتغطية أساسيات استخدام Aspose.HTML لـ .NET لإنشاء مستندات HTML ومعالجتها وتصميمها داخل تطبيقات .NET الخاصة بك. لقد استكشفنا أمثلة مختلفة، من إنشاء مستند HTML إلى تحرير بنيته وأنماطه. باستخدام هذه المهارات، يمكنك التعامل مع مستندات HTML بفعالية في مشاريع .NET الخاصة بك.

 إذا كان لديك أي أسئلة أو تحتاج إلى مزيد من المساعدة، فلا تتردد في زيارة[توثيق Aspose.HTML لـ .NET](https://reference.aspose.com/html/net/) أو اطلب المساعدة على[منتدى اسبوس](https://forum.aspose.com/).

---

## الأسئلة الشائعة

### ما هو Aspose.HTML لـ .NET؟
Aspose.HTML for .NET هي مكتبة قوية للعمل مع مستندات HTML في تطبيقات .NET.

### أين يمكنني تنزيل Aspose.HTML لـ .NET؟
 يمكنك تنزيل Aspose.HTML لـ .NET من[هنا](https://releases.aspose.com/html/net/).

### هل هناك نسخة تجريبية مجانية متاحة؟
 نعم، يمكنك الحصول على نسخة تجريبية مجانية من Aspose.HTML من[هنا](https://releases.aspose.com/).

### كيف يمكنني شراء ترخيص؟
 لشراء الترخيص، قم بزيارة[هذا الرابط](https://purchase.aspose.com/buy).

### هل أحتاج إلى خبرة سابقة مع HTML لاستخدام Aspose.HTML لـ .NET؟
على الرغم من أن معرفة HTML مفيدة، إلا أنه يمكنك استخدام Aspose.HTML لـ .NET حتى إذا لم تكن خبيرًا في HTML.


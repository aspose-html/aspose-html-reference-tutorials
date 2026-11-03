---
category: general
date: 2026-03-02
description: تعلم كيفية تمكين التنعيم وكيفية تطبيق الخط العريض برمجياً أثناء استخدام
  التلميحات وتعيين أنماط خطوط متعددة في خطوة واحدة.
draft: false
keywords:
- how to enable antialiasing
- how to apply bold
- how to use hinting
- set font style programmatically
- set multiple font styles
language: ar
og_description: اكتشف كيفية تمكين التنعيم، وتطبيق الخط العريض، واستخدام التلميحات
  أثناء ضبط أنماط خطوط متعددة برمجياً في C#.
og_title: كيفية تمكين التنعيم في C# – دليل شامل لأنماط الخط
tags:
- C#
- graphics
- text rendering
title: كيفية تمكين التنعيم في C# – دليل كامل لأنماط الخط
url: /ar/net/canvas-and-image-manipulation/how-to-enable-antialiasing-in-c-complete-font-style-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمكين مضاد التعرج في C# – دليل كامل لأنماط الخط

هل تساءلت يومًا **كيفية تمكين مضاد التعرج** عند رسم النص في تطبيق .NET؟ لست وحدك. يواجه معظم المطورين مشكلة عندما يبدو واجهة المستخدم متعرجة على شاشات عالية الدقة DPI، وغالبًا ما يكون الحل مخفيًا خلف بعض تبديلات الخصائص. في هذا الدرس سنستعرض الخطوات الدقيقة لتفعيل مضاد التعرج، **كيفية تطبيق الخط العريض**، وحتى **كيفية استخدام التلميح** لجعل الشاشات منخفضة الدقة تبدو حادة. في النهاية ستتمكن من **تعيين نمط الخط برمجيًا** ودمج **أنماط خطوط متعددة** دون عناء.

سنغطي كل ما تحتاجه: المساحات الاسمية المطلوبة، مثال كامل قابل للتنفيذ، لماذا كل علم مهم، وبعض المشكلات التي قد تواجهها. لا مستندات خارجية، فقط دليل مستقل يمكنك نسخه ولصقه في Visual Studio ورؤية النتائج فورًا.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (واجهات برمجة التطبيقات المستخدمة هي جزء من `System.Drawing.Common` ومكتبة مساعدة صغيرة)
- معرفة أساسية بـ C# (أنت تعرف ما هي `class` و `enum`)
- بيئة تطوير متكاملة أو محرر نصوص (Visual Studio، VS Code، Rider—أيًا كان)

إذا كان لديك ذلك، لننطلق.

---

## كيفية تمكين مضاد التعرج في عرض النصوص بـ C#

جوهر النص السلس هو الخاصية `TextRenderingHint` على كائن `Graphics`. ضبطها إلى `ClearTypeGridFit` أو `AntiAlias` يخبر المُعالج بدمج حواف البكسل، مما يلغي تأثير السلم المتعرج.

```csharp
using System;
using System.Drawing;
using System.Drawing.Text;   // for TextRenderingHint
using System.Windows.Forms; // for a quick demo form

public class AntialiasDemo : Form
{
    protected override void OnPaint(PaintEventArgs e)
    {
        base.OnPaint(e);

        // Step 3: Enable antialiasing for smoother glyph edges
        e.Graphics.TextRenderingHint = TextRenderingHint.AntiAlias;
        // You could also use ClearTypeGridFit for LCD screens:
        // e.Graphics.TextRenderingHint = TextRenderingHint.ClearTypeGridFit;

        // Draw sample text so you can see the effect
        e.Graphics.DrawString(
            "Antialiased Text",
            new Font("Segoe UI", 24, FontStyle.Regular),
            Brushes.Black,
            new PointF(20, 20));
    }

    [STAThread]
    public static void Main()
    {
        Application.Run(new AntialiasDemo());
    }
}
```

**لماذا هذا يعمل:** `TextRenderingHint.AntiAlias` يجبر محرك GDI+ على دمج حواف الحروف مع الخلفية، مما ينتج مظهرًا أكثر سلاسة. على أجهزة Windows الحديثة يكون هذا عادةً الإعداد الافتراضي، لكن العديد من سيناريوهات الرسم المخصصة تعيد تعيين التلميح إلى `SystemDefault`، لذا نضبطه صراحة.

> **نصيحة احترافية:** إذا كنت تستهدف شاشات عالية DPI، اجمع بين `AntiAlias` و `Graphics.ScaleTransform` للحفاظ على وضوح النص بعد التحجيم.

### النتيجة المتوقعة

عند تشغيل البرنامج، يفتح نافذة تعرض “Antialiased Text” مُرسمًا دون حواف متعرجة. قارن ذلك مع نفس السلسلة المرسومة بدون ضبط `TextRenderingHint`—الفرق واضح.

---

## كيفية تطبيق الأنماط العريضة والمائلة للخط برمجيًا

تطبيق الخط العريض (أو أي نمط) ليس مجرد ضبط قيمة منطقية؛ تحتاج إلى دمج العلامات من تعداد `FontStyle`. المقتطف البرمجي الذي رأيته سابقًا يستخدم تعدادًا مخصصًا `WebFontStyle`، لكن المبدأ هو نفسه مع `FontStyle`.

```csharp
// Step 1: Create a CSS‑style container (simulated with FontStyle)
FontStyle combinedStyle = FontStyle.Bold | FontStyle.Italic;

// Step 2: Apply bold and italic font styles using the enum
Font styledFont = new Font("Segoe UI", 28, combinedStyle);
```

في سيناريو واقعي قد تخزن النمط في كائن إعدادات وتطبقه لاحقًا:

```csharp
public class TextOptions
{
    public FontStyle FontStyle { get; set; } = FontStyle.Regular;
    public bool UseAntialiasing { get; set; } = false;
    public bool UseHinting { get; set; } = false;
}
```

ثم استخدمه عند الرسم:

```csharp
var options = new TextOptions
{
    FontStyle = FontStyle.Bold | FontStyle.Italic,
    UseAntialiasing = true,
    UseHinting = true
};

Font font = new Font("Segoe UI", 24, options.FontStyle);
if (options.UseAntialiasing)
    e.Graphics.TextRenderingHint = TextRenderingHint.AntiAlias;
if (options.UseHinting)
    e.Graphics.TextRenderingHint = TextRenderingHint.SingleBitPerPixelGridFit;

// Draw with the configured font
e.Graphics.DrawString("Bold & Italic", font, Brushes.DarkBlue, new PointF(20, 80));
```

**لماذا دمج العلامات؟** `FontStyle` هو تعداد حقل بت، يعني أن كل نمط (Bold, Italic, Underline, Strikeout) يشغل بتًا مميزًا. استخدام عملية OR البتية (`|`) يتيح لك تجميعها دون استبدال الاختيارات السابقة.

## كيفية استخدام التلميح للشاشات منخفضة الدقة

التلميح يدفع حدود الحروف لتتماشى مع شبكة البكسل، وهو أمر أساسي عندما لا تستطيع الشاشة عرض تفاصيل تحت البكسل. في GDI+، يتم التحكم في التلميح عبر `TextRenderingHint.SingleBitPerPixelGridFit` أو `ClearTypeGridFit`.

```csharp
// Step 4: Turn on hinting to improve text rendering on low‑resolution displays
if (options.UseHinting)
{
    // SingleBitPerPixelGridFit works well on older LCD panels
    e.Graphics.TextRenderingHint = TextRenderingHint.SingleBitPerPixelGridFit;
}
```

### متى تستخدم التلميح

- **شاشات منخفضة DPI** (مثال: شاشات كلاسيكية 96 dpi)
- **خطوط bitmap** حيث كل بكسل مهم
- **تطبيقات حساسة للأداء** حيث يكون مضاد التعرج الكامل ثقيلًا

إذا قمت بتمكين كل من مضاد التعرج *و* التلميح، سيعطي المُعالج الأولوية للتلميح أولًا، ثم يطبق التنعيم. الترتيب مهم؛ اضبط التلميح **بعد** مضاد التعرج إذا أردت أن يؤثر التلميح على الحروف التي تم تنعيمها بالفعل.

## تعيين أنماط خطوط متعددة مرة واحدة – مثال عملي

بجمع كل شيء معًا، إليك عرضًا مختصرًا يوضح:

1. **يفعل مضاد التعرج** (`how to enable antialiasing`)
2. **يطبق العريض والمائل** (`how to apply bold`)
3. **يشغل التلميح** (`how to use hinting`)
4. **يحدد أنماط خطوط متعددة** (`set multiple font styles`)

```csharp
using System;
using System.Drawing;
using System.Drawing.Text;
using System.Windows.Forms;

public class FullStyleDemo : Form
{
    private readonly TextOptions _options = new()
    {
        FontStyle = FontStyle.Bold | FontStyle.Italic,
        UseAntialiasing = true,
        UseHinting = true
    };

    protected override void OnPaint(PaintEventArgs e)
    {
        base.OnPaint(e);

        // Apply antialiasing if requested
        if (_options.UseAntialiasing)
            e.Graphics.TextRenderingHint = TextRenderingHint.AntiAlias;

        // Apply hinting after antialiasing
        if (_options.UseHinting)
            e.Graphics.TextRenderingHint = TextRenderingHint.SingleBitPerPixelGridFit;

        // Build the font with multiple styles
        using Font font = new Font("Segoe UI", 30, _options.FontStyle);

        // Render the text
        e.Graphics.DrawString(
            "Bold + Italic + Hinted",
            font,
            Brushes.DarkGreen,
            new PointF(20, 20));
    }

    [STAThread]
    public static void Main()
    {
        Application.Run(new FullStyleDemo());
    }
}
```

#### ما يجب أن تراه

نافذة تعرض **Bold + Italic + Hinted** باللون الأخضر الداكن، مع حواف ناعمة بفضل مضاد التعرج ومحاذاة واضحة بفضل التلميح. إذا علقت أي علامة، سيظهر النص إما متعرجًا (بدون مضاد التعرج) أو غير محاذٍ قليلًا (بدون التلميح).

---

## أسئلة شائعة وحالات حافة

| السؤال | الجواب |
|----------|--------|
| *ماذا لو كانت منصة الهدف لا تدعم `System.Drawing.Common`؟* | على Windows مع .NET 6+ لا يزال بإمكانك استخدام GDI+. بالنسبة للرسومات عبر المنصات، فكر في SkiaSharp – فهو يقدم خيارات مضاد تعرج وتلميح مماثلة عبر `SKPaint.IsAntialias`. |
| *هل يمكنني دمج `Underline` مع `Bold` و `Italic`؟* | بالطبع. `FontStyle.Bold | FontStyle.Italic | FontStyle.Underline` يعمل بنفس الطريقة. |
| *هل يؤثر تمكين مضاد التعرج على الأداء؟* | قليلًا، خاصةً على القماشيات الكبيرة. إذا كنت ترسم آلاف السلاسل في كل إطار، قم بقياس الأداء لكل إعداد واتخذ القرار. |
| *ماذا لو لم تكن عائلة الخط تحتوي على وزن عريض؟* | سيقوم GDI+ بتوليد نمط عريض اصطناعيًا، قد يبدو أثقل من النسخة العريضة الحقيقية. اختر خطًا يضم وزنًا عريضًا أصليًا للحصول على أفضل جودة بصرية. |
| *هل هناك طريقة لتبديل هذه الإعدادات أثناء التشغيل؟* | نعم—فقط قم بتحديث كائن `TextOptions` واستدعِ `Invalidate()` على التحكم لإجبار إعادة الرسم. |

## توضيح بالصورة

![لقطة شاشة توضح كيفية تمكين مضاد التعرج في كود C# والنص السلس الناتج](/images/antialias-demo.png)

*نص بديل:* **how to enable antialiasing** – الصورة توضح الكود والناتج السلس.

## ملخص وخطوات قادمة

لقد غطينا **كيفية تمكين مضاد التعرج** في سياق رسومات C#، **كيفية تطبيق الخط العريض** وأنماط أخرى برمجيًا، **كيفية استخدام التلميح** للشاشات منخفضة الدقة، وأخيرًا **كيفية تعيين أنماط خطوط متعددة** في سطر واحد من الكود. المثال الكامل يجمع بين المفاهيم الأربعة، ويقدم لك حلًا جاهزًا للتنفيذ.

ما التالي؟ قد ترغب في:

- استكشاف **SkiaSharp** أو **DirectWrite** للحصول على خطوط أنابيب عرض نصية أكثر غنى.
- تجربة **تحميل الخطوط ديناميكيًا** (`PrivateFontCollection`) لتجميع خطوط مخصصة.
- إضافة **واجهة مستخدم قابلة للتحكم** (مربعات اختيار لمضاد التعرج/التلميح) لرؤية التأثير في الوقت الحقيقي.

لا تتردد في تعديل فئة `TextOptions`، تغيير الخطوط، أو دمج هذه المنطق في تطبيق WPF أو WinUI. المبادئ تبقى نفسها: اضبط الـ

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
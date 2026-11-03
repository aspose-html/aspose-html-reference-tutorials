---
category: general
date: 2026-04-23
description: تطبيق نمط الخط برمجيًا وتعلم كيفية إزالة الخط السفلي من النص، وتغيير
  نمط النص، وتعيين النص الغامق برمجيًا في دليل مختصر.
draft: false
keywords:
- apply font style
- remove underline from text
- change text style
- text formatting tutorial
- set bold text programmatically
language: ar
og_description: تطبيق نمط الخط برمجياً واكتشاف كيفية إزالة الخط السفلي من النص، وتغيير
  نمط النص، وتعيين النص الغامق برمجياً في دليل قصير عملي.
og_title: تطبيق نمط الخط برمجياً – دليل C# سريع
tags:
- csharp
- ui
- text-formatting
- programming
title: تطبيق نمط الخط برمجيًا – دليل C# السريع
url: /ar/net/html-document-manipulation/apply-font-style-programmatically-quick-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تطبيق نمط الخط برمجيًا – دليل سريع بلغة C#

هل احتجت يومًا إلى **تطبيق نمط الخط** على عنصر واجهة المستخدم لكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك—معظم المطورين يواجهون هذه المشكلة عندما يبدأون بالتحكم الديناميكي في تنسيق النص. الخبر السار؟ خلال دقائق قليلة ستعرف بالضبط كيف تغير مظهر تسمية، وتزيل الخط السفلي من النص، وتضبط النص الغامق برمجيًا دون الحاجة للبحث في وثائق لا نهائية.

في هذا **الدليل لتنسيق النص** سنستعرض مثالًا كاملًا قابلًا للتنفيذ، نشرح "السبب" وراء كل سطر، ونضيف نصائح عملية يمكنك نسخها‑لصقها في أي مشروع WinForms أو WPF. لا حشو، فقط ما ينجز المهمة.

---

## ما ستتعلمه

- كيف **تطبق نمط الخط** باستخدام فئة مساعدة صغيرة.  
- الخطوات الدقيقة **لإزالة الخط السفلي من النص** مع الحفاظ على الأنماط الأخرى.  
- طرق **تغيير نمط النص** (غامق، مائل، تحته خط) في الوقت الحقيقي.  
- مقتطف كامل جاهز للنسخ **يضبط النص الغامق برمجيًا**.  
- الأخطاء الشائعة وتعامل مع الحالات الحدية حتى لا تُفاجأ لاحقًا.

**المتطلبات المسبقة:** .NET 6+ (أو أي نسخة حديثة من .NET Framework)، معرفة أساسية بـ C#، وبيئة تطوير من اختيارك (Visual Studio، Rider، أو VS Code). هذا كل ما تحتاجه—لا حزم NuGet إضافية مطلوبة.

---

## الخطوة 1 – تطبيق نمط الخط على التحكم الخاص بك

جوهر أي عملية **تطبيق نمط الخط** هو تعداد `FontStyle` مع كائن `Font`. لجعل الكود منظمًا سنغلف منطق التعداد داخل فئة صغيرة تسمى `WebFontStyle`. هذه الفئة تعكس الخصائص التي رأيتها في المقتطف الأصلي (`Bold`, `Italic`, `Underline`) وتُنشئ قيمة `FontStyle` يمكنك تمريرها إلى `Font`.

```csharp
using System;
using System.Drawing;

/// <summary>
/// Simple helper that mimics the original WebFontStyle API.
/// It lets you toggle Bold, Italic, and Underline flags and
/// converts the result into a System.Drawing.FontStyle value.
/// </summary>
public class WebFontStyle
{
    public bool Bold { get; set; } = false;
    public bool Italic { get; set; } = false;
    public bool Underline { get; set; } = false;

    /// <summary>
    /// Returns a FontStyle that combines the selected flags.
    /// </summary>
    public FontStyle ToFontStyle()
    {
        FontStyle style = FontStyle.Regular;
        if (Bold)      style |= FontStyle.Bold;
        if (Italic)    style |= FontStyle.Italic;
        if (Underline) style |= FontStyle.Underline;
        return style;
    }

    /// <summary>
    /// Creates a new Font based on an existing one but with the
    /// updated style. Handy for UI controls that already have a font.
    /// </summary>
    public Font ToFont(Font baseFont)
    {
        return new Font(baseFont, ToFontStyle());
    }
}
```

**لماذا هذا مهم:**  
من خلال عزل منطق بناء العلامات، تتجنب نشر عمليات bitwise `|` في كل مكان في كود الواجهة. يصبح الكود أسهل للقراءة، وأسهل للاختبار،—والأهم—يجعل نية **تطبيق نمط الخط** واضحة تمامًا.

---

## الخطوة 2 – إزالة الخط السفلي من النص (مع الحفاظ على الأنماط الأخرى)

افترض أنك ورثت تسمية مُحددة بالفعل بخط سفلي، لكن التصميم يتطلب نصًا غامقًا عاديًا. لا تريد فقدان الغامق أثناء إزالة الخط السفلي. هنا تتألق فئة `WebFontStyle`.

```csharp
// Assume we already have a Label named lblSample.
var fontStyle = new WebFontStyle
{
    Bold = true,          // Keep bold on.
    Italic = false,      // No italic needed.
    Underline = false    // This line **removes underline**.
};

// Apply the new Font to the label.
lblSample.Font = fontStyle.ToFont(lblSample.Font);
```

**النقطة الأساسية:** ضبط `Underline = false` صراحةً يخبر المساعد *باستبعاد* علامة الخط السفلي. إذا حذفت السطر تمامًا، سيستمر الخط السفلي السابق، وهذا مصدر شائع للأخطاء عندما يقتصر المطورون على تبديل خاصية `Bold` فقط.

---

## الخطوة 3 – تغيير نمط النص: غامق، مائل، وأكثر

قد تتساءل، “ماذا لو أردت تبديل المائل أيضًا؟” نفس الكائن يعمل لأي تركيبة. أدناه مصفوفة سريعة يمكنك الرجوع إليها أثناء البرمجة.

| النمط المطلوب | `Bold` | `Italic` | `Underline` |
|---------------|--------|----------|-------------|
| **غامق فقط** | true   | false    | false       |
| *مائل فقط* | false  | true     | false       |
| **غامق + مائل** | true   | true     | false       |
| **غامق + تحته خط** | true   | false    | true        |

ما عليك سوى ضبط الخصائص التي تحتاجها واستدعاء `ToFont`. المساعد يقوم بالعمل الشاق نيابةً عنك، لتتمكن من التركيز على منطق الواجهة.

---

## مثال كامل – ضبط النص الغامق برمجيًا

فيما يلي مثال **كامل وقابل للتنفيذ على WinForms** يوضح كل ما تناولناه. الصقه في مشروع WinForms جديد من نوع console‑style واضغط **F5**.

```csharp
using System;
using System.Drawing;
using System.Windows.Forms;

namespace FontStyleDemo
{
    static class Program
    {
        [STAThread]
        static void Main()
        {
            ApplicationConfiguration.Initialize(); // .NET 6+ boilerplate
            Application.Run(new DemoForm());
        }
    }

    public class DemoForm : Form
    {
        private readonly Label _sampleLabel;

        public DemoForm()
        {
            Text = "Apply Font Style Demo";
            Size = new Size(400, 200);
            StartPosition = FormStartPosition.CenterScreen;

            _sampleLabel = new Label
            {
                Text = "Hello, world!",
                AutoSize = true,
                Location = new Point(20, 30)
            };
            Controls.Add(_sampleLabel);

            // STEP: instantiate WebFontStyle and configure it
            var fontStyle = new WebFontStyle
            {
                Bold = true,          // set bold text programmatically
                Italic = false,      // no italic
                Underline = false    // remove underline from text
            };

            // Apply the new style to the label
            _sampleLabel.Font = fontStyle.ToFont(_sampleLabel.Font);
        }
    }

    // ---- WebFontStyle class from Step 1 (included for completeness) ----
    public class WebFontStyle
    {
        public bool Bold { get; set; } = false;
        public bool Italic { get; set; } = false;
        public bool Underline { get; set; } = false;

        public FontStyle ToFontStyle()
        {
            FontStyle style = FontStyle.Regular;
            if (Bold)      style |= FontStyle.Bold;
            if (Italic)    style |= FontStyle.Italic;
            if (Underline) style |= FontStyle.Underline;
            return style;
        }

        public Font ToFont(Font baseFont)
        {
            return new Font(baseFont, ToFontStyle());
        }
    }
}
```

### النتيجة المتوقعة

عند تشغيل البرنامج، تظهر نافذة تحتوي على النص **“Hello, world!”** معروضًا **غامقًا**، **ليس مائلًا**، و**بدون أي خط سفلي**. هذا التأكيد البصري يُظهر أن منطق **تطبيق نمط الخط** عمل بشكل مثالي.

---

## نصائح احترافية وحالات حدية

- **التحديثات الديناميكية:** إذا احتجت لتغيير النمط بعد إظهار النموذج (مثلاً استجابةً لمربع اختيار)، ما عليك سوى إنشاء كائن `WebFontStyle` جديد أو تعديل خصائصه وإعادة تعيين `lbl.Font`. ستُحدَّث الواجهة فورًا.  
- **اعتبارات DPI العالية:** عند استبدال كائن `Font`، يقوم Windows تلقائيًا بتكييفه بناءً على DPI الحالي. لا تحتاج إلى كود إضافي إلا إذا كنت تتعامل مع التحجيم يدويًا.  
- **المكافئ في WPF:** في WPF ستربط `FontWeight`، `FontStyle`، و`TextDecorations` بدلاً من استبدال كائن `Font`. نفس الفكرة المنطقية تُطبق—احتفظ بمنطق النمط خارج طبقة العرض.  
- **تجنب تسرب الذاكرة:** إعادة تعيين `Label.Font` يُنشئ كائن `Font` جديد. قم بتحرير الكائن القديم إذا كنت تبدل الأنماط بشكل متكرر: `var oldFont = lbl.Font; lbl.Font = newFont; oldFont.Dispose();`

---

## الخلاصة

أنت الآن تعرف كيف **تطبق نمط الخط** على أي عنصر .NET، **تزيل الخط السفلي من النص**، و**تغير نمط النص** في الوقت الحقيقي—كل ذلك مع الحفاظ على نظافة وإعادة استخدام الكود. المساعد الصغير `WebFontStyle` يحول مجموعة من العلامات البوليانية إلى مكوّن ثابت وقابل للاختبار، والمثال الكامل يثبت أنك تستطيع **ضبط النص الغامق برمجيًا** في بضع أسطر فقط.

ما الخطوة التالية؟ جرّب دمج هذا النهج مع إعدادات يُحددها المستخدم، أو استكشف علامات `FontStyle` أخرى مثل `Strikeout`. يمكنك حتى إنشاء لوحة تحكم صغيرة تسمح للمستخدمين غير التقنيين باختيار الغامق أو المائل أو الخط السفلي أثناء التشغيل—دون الحاجة لإعادة التجميع.

إذا وجدت هذا **الدليل لتنسيق النص** مفيدًا، لا تتردد في ترك تعليق أو مشاركة تنويعاتك الخاصة. برمجة سعيدة، ولتظهر واجهاتك دائمًا كما تريد! 

---

![لقطة شاشة تُظهر كيفية تطبيق نمط الخط على تسمية في C#](https://example.com/images/apply-font-style.png

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
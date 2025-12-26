---
category: general
date: 2025-12-26
description: كيفية دمج الخطوط في C# باستخدام عوامل البت – تعلم تعيين نمط الخط برمجيًا
  وتطبيق أنماط خطوط متعددة بكفاءة.
draft: false
keywords:
- how to combine fonts
- set font style programmatically
- how to set font
- combine font styles
- apply multiple font styles
language: ar
og_description: كيفية دمج الخطوط في C# بسرعة. يوضح لك هذا الدليل كيفية تعيين نمط الخط
  برمجياً وتطبيق أنماط خطوط متعددة مع أمثلة واضحة.
og_title: كيفية دمج الخطوط في C# – دليل برمجي كامل
tags:
- C#
- graphics
- typography
title: كيفية دمج الخطوط برمجيًا في C# – دليل خطوة بخطوة
url: /ar/net/advanced-features/how-to-combine-fonts-programmatically-in-c-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية دمج الخطوط برمجياً في C#

هل تساءلت يومًا **كيفية دمج الخطوط** في سطر واحد من كود C#؟ ربما تقوم ببناء محرر ويب، أو مولد PDF، أو واجهة مستخدم لعبة، وتحتاج إلى نص يكون **غامقًا** *و* *مائلًا* في نفس الوقت. الخبر السار هو أنك لست بحاجة إلى كتابة عشرات الاستدعاءات المنفصلة—فقط حيلة بسيطة باستخدام العمليات البتية وستكون جاهزًا.

في هذا الدرس سنستعرض **كيفية ضبط نمط الخط** برمجياً، نستكشف عامل `|` (OR البتية) لدمج أعلام `WebFontStyle`، ونوضح لك كيفية **تطبيق أنماط خطوط متعددة** دون التعقيد في التحميل الزائد. بنهاية الدرس ستحصل على مثال كامل قابل للتنفيذ يمكنك إدراجه في أي مشروع .NET.

> **ملخص سريع:** استخدم `WebFontStyle.Bold | WebFontStyle.Italic` (أو أي تركيبة) وعيّن النتيجة إلى `GraphicContext.FontStyle`. هذا كل ما تحتاجه **لدمج أنماط الخطوط**.

---

## ما ستحتاجه

قبل أن نبدأ، تأكد من وجود ما يلي:

* .NET 6.0 أو أحدث (واجهة برمجة التطبيقات التي نستخدمها جزء من مكتبة رسومات افتراضية، لكن النمط يعمل مع أي تعداد `Flags`).
* بيئة تطوير—Visual Studio أو Rider أو VS Code تكفي.
* إلمام أساسي بتعدادات C# وعوامل البت.

لا توجد حزم NuGet إضافية مطلوبة للمثال الأساسي؛ سنستخدم فئة `GraphicContext` بسيطة لتبقى الأمور مكتفية ذاتيًا.

---

## كيفية دمج الخطوط في C# – الفكرة الأساسية

جوهر **كيفية دمج الخطوط** يكمن في أن `WebFontStyle` مُعلَّم بصفة `[Flags]`. هذا يخبر CLR أن كل قيمة من التعداد تمثل بتًا واحدًا، ويمكنك دمجها بأمان باستخدام عامل OR البتية (`|`). النتيجة هي عدد صحيح واحد حيث كل بت يمثل نمطًا مختارًا.

```csharp
// Define the enum – each value occupies a distinct bit.
[Flags]
public enum WebFontStyle
{
    Regular = 0,
    Bold    = 1 << 0,   // 0001
    Italic  = 1 << 1,   // 0010
    Underline = 1 << 2 // 0100
    // Add more styles as needed
}
```

عند كتابة `WebFontStyle.Bold | WebFontStyle.Italic`، ينتج المترجم قيمة تمثيلها الثنائي هو `0011`. ثم تقوم فئة `GraphicContext` بقراءة تلك البتات وتعرض النص وفقًا لها.

---

## تنفيذ خطوة بخطوة

فيما يلي **برنامج كامل قابل للتنفيذ** يوضح سير العمل بالكامل—من إنشاء سياق رسومي إلى **ضبط نمط الخط برمجياً** وأخيرًا **تطبيق أنماط خطوط متعددة** على قطعة نص.

### 1️⃣ إنشاء سياق رسومي بسيط

أولًا، نحتاج إلى سطح للرسم عليه. في مشروع حقيقي قد تستخدم شيء مثل `System.Drawing.Graphics` أو لوحة قماش من طرف ثالث، لكن للتوضيح سنُعرّف فئة بسيطة كبديل.

```csharp
using System;

public class GraphicContext
{
    // The FontStyle property accepts a combination of WebFontStyle flags.
    public WebFontStyle FontStyle { get; set; } = WebFontStyle.Regular;

    // Simulated draw method – in a real app this would render to screen or PDF.
    public void DrawString(string text)
    {
        Console.WriteLine($"Drawing text: \"{text}\" with style: {FontStyle}");
        // Here you would normally pass FontStyle to the underlying rendering engine.
    }
}
```

### 2️⃣ دمج الأنماط المطلوبة

الآن نقوم فعليًا **بدمج أنماط الخط**. هذا هو الجزء الذي يجيب مباشرة على سؤال “كيفية دمج الخطوط”.

```csharp
// Combine Bold and Italic using the bitwise OR operator.
WebFontStyle combinedStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

يمكنك إضافة أعلام أخرى إذا احتجت إلى تسطير، شطب، أو أي نمط مخصص يدعمه مكتبتك:

```csharp
WebFontStyle fancyStyle = WebFontStyle.Bold | WebFontStyle.Italic | WebFontStyle.Underline;
```

### 3️⃣ تطبيق النمط المدمج على السياق

أخيرًا، عيّن القيمة المدمجة إلى `GraphicContext` وارسم شيئًا ما.

```csharp
GraphicContext graphicContext = new GraphicContext();

// Apply the combined style.
graphicContext.FontStyle = combinedStyle;

// Render a sample string.
graphicContext.DrawString("Hello, combined fonts!");
```

### 4️⃣ البرنامج الكامل

نجمع كل ما سبق في ملف مصدر واحد يمكنك نسخه، لصقه، وتشغيله:

```csharp
using System;

[Flags]
public enum WebFontStyle
{
    Regular   = 0,
    Bold      = 1 << 0,   // 0001
    Italic    = 1 << 1,   // 0010
    Underline = 1 << 2    // 0100
    // Extend with more styles as needed.
}

public class GraphicContext
{
    public WebFontStyle FontStyle { get; set; } = WebFontStyle.Regular;

    public void DrawString(string text)
    {
        // In a real graphics library you would pass FontStyle to the renderer.
        Console.WriteLine($"Drawing text: \"{text}\" with style: {FontStyle}");
    }
}

class Program
{
    static void Main()
    {
        // Step 1: Obtain a graphic context.
        GraphicContext graphicContext = new GraphicContext();

        // Step 2: Combine the desired font styles using the bitwise OR operator.
        // This creates a single value that represents both Bold and Italic.
        WebFontStyle combinedStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // Step 3: Apply the combined style to the graphic context.
        graphicContext.FontStyle = combinedStyle;

        // Step 4: Draw something to verify the result.
        graphicContext.DrawString("Hello, combined fonts!");

        // Bonus: Show how to add underline as well.
        WebFontStyle fancy = WebFontStyle.Bold | WebFontStyle.Italic | WebFontStyle.Underline;
        graphicContext.FontStyle = fancy;
        graphicContext.DrawString("Now with underline!");
    }
}
```

**الإخراج المتوقع**

```
Drawing text: "Hello, combined fonts!" with style: Bold, Italic
Drawing text: "Now with underline!" with style: Bold, Italic, Underline
```

إذا شغلت هذا في وحدة تحكم، ستظهر السطران اللذان يؤكدان أن الأنماط تم دمجها بشكل صحيح. في واجهة مستخدم حقيقية سترى نصًا غامقًا مائلًا (ويمكن أن يكون مسطرًا) معروضًا على الشاشة.

---

## أسئلة شائعة وحالات خاصة

### ماذا لو احتجت إلى **إزالة** نمط لاحقًا؟

يمكنك استخدام عامل AND البتية مع المكمل (`& ~`) لإلغاء علم معين:

```csharp
// Remove Italic while keeping Bold.
graphicContext.FontStyle &= ~WebFontStyle.Italic;
```

### هل يعمل هذا مع **عائلات خطوط مخصصة**؟

بالتأكيد. نهج الاعلام يختص فقط بـ *النمط* (غامق، مائل، إلخ). عائلة الخط الفعلية (مثل `"Arial"` أو `"Open Sans"`) تُحدد عادةً عبر خاصية منفصلة مثل `FontFamily`. ادمجهما حسب الحاجة.

### هل صفة `Flags` ضرورية؟

نعم. بدون `[Flags]` سيظل التعداد يُترجم، لكن تمثيل السلسلة (`ToString()`) لن يكون واضحًا، وقد يصعب قراءة التركيبات البتية. معظم مكتبات الرسومات التي تُعرِّف تعدادًا للأنماط تُعلِّمها بالفعل بـ `[Flags]`.

### هل يمكنني استخدام هذا النمط مع **WPF** أو **WinForms**؟

كلا الإطارين يقدمان تعدادًا مشابهًا للعلامات (`FontStyle` في WinForms، `FontWeight`/`FontStyle` في WPF). المبدأ هو نفسه: دمج قيم التعداد باستخدام `|`. مثال على WinForms:

```csharp
myLabel.Font = new Font(myLabel.Font, FontStyle.Bold | FontStyle.Italic);
```

---

## نصائح احترافية لضبط نمط الخط برمجياً

* **تحقق قبل التطبيق** – بعض محركات العرض ترفض تركيبات غير مدعومة (مثل `Bold | Italic` على خط لا يوفر وزنًا غامقًا). تحقق من `CanApplyStyle` إذا وفرت الواجهة هذه الدالة.
* **خزن الأنماط المدمجة** – إذا كنت ترسم آلاف السلاسل، احسب قيمة التعداد المدمجة مرة واحدة وأعد استخدامها.
* **تذكر الثقافة** – بعض اللغات لها قواعد طباعية خاصة؛ اختبر النتيجة البصرية دائمًا في اللغة المستهدفة.
* **ملاحظة الأداء** – عمليات البت تقريبًا مجانية؛ عنق الزجاجة عادةً يكون في عملية العرض نفسها، وليس في دمج الأنماط.

---

## ملخص بصري

![مخطط يوضح كيف يدمج OR البتية أعلام نمط الخط](/images/combine-fonts-diagram.png "مثال على دمج الخطوط")

*النص البديل:* *مخطط مثال دمج الخطوط يوضح عملية OR البتية بين علمي Bold و Italic.*

---

## الخلاصة

غطّينا **كيفية دمج الخطوط** في C# من الصفر: تعريف تعداد `[Flags]`، دمج الأنماط باستخدام عامل `|`، و**ضبط نمط الخط برمجياً** على سياق رسومي. يثبت المثال الكامل أنك تستطيع **تطبيق أنماط خطوط متعددة** ببضع أسطر فقط، وتضمن النصائح الإضافية تجنب المشكلات الشائعة.

الآن بعد أن عرفت الحيلة، جرب إضافة تسطير، شطب، أو حتى أعلام مخصصة للظل أو النقش. النمط قابل للتوسيع بسهولة، ما يسمح لك بالحفاظ على شفرة واجهة المستخدم نظيفة ومعبرة.

إذا وجدت هذا الدليل مفيدًا، شاركه مع زملائك أو ضع نجمة على المستودع الذي تحتفظ فيه بأدوات الرسومات الخاصة بك. برمجة سعيدة، ولتظهر نصوصك دائمًا كما تتخيل! 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
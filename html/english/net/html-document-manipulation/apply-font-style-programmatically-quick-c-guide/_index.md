---
category: general
date: 2026-04-23
description: Apply font style programmatically and learn how to remove underline from
  text, change text style, and set bold text programmatically in a concise tutorial.
draft: false
keywords:
- apply font style
- remove underline from text
- change text style
- text formatting tutorial
- set bold text programmatically
language: en
og_description: Apply font style programmatically and discover how to remove underline
  from text, change text style, and set bold text programmatically in a short, practical
  tutorial.
og_title: Apply Font Style Programmatically – Quick C# Guide
tags:
- csharp
- ui
- text-formatting
- programming
title: Apply Font Style Programmatically – Quick C# Guide
url: /net/html-document-manipulation/apply-font-style-programmatically-quick-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Apply Font Style Programmatically – Quick C# Guide

Ever needed to **apply font style** to a UI element but weren’t sure where to start? You’re not the only one—most developers hit that snag when they first dabble with dynamic text formatting. The good news? In just a few minutes you’ll know exactly how to change a label’s appearance, remove underline from text, and set bold text programmatically without hunting through endless docs.

In this **text formatting tutorial** we’ll walk through a complete, runnable example, explain the “why” behind each line, and sprinkle in practical tips you can copy‑paste into any WinForms or WPF project. No fluff, just the stuff that gets the job done.

---

## What You’ll Learn

- How to **apply font style** using a tiny helper class.  
- The precise steps to **remove underline from text** while keeping other styles intact.  
- Ways to **change text style** (bold, italic, underline) on the fly.  
- A full, copy‑ready snippet that **sets bold text programmatically**.  
- Common pitfalls and edge‑case handling so you don’t get surprised later.

**Prerequisites:** .NET 6+ (or any recent .NET Framework), basic C# knowledge, and an IDE of your choice (Visual Studio, Rider, or VS Code). That’s it—no extra NuGet packages required.

---

## Step 1 – Apply Font Style to Your Control

The core of any **apply font style** operation is a `FontStyle` enum combined with a `Font` object. To keep the code tidy we’ll wrap the enum logic inside a small `WebFontStyle` class. This class mirrors the properties you saw in the original snippet (`Bold`, `Italic`, `Underline`) and builds a `FontStyle` value you can hand to `Font`.

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

**Why this matters:**  
By isolating the flag‑building logic, you avoid sprinkling bitwise `|` operations throughout your UI code. It’s easier to read, easier to test, and—most importantly—makes the **apply font style** intent crystal clear.

---

## Step 2 – Remove Underline from Text (and Keep Other Styles Intact)

Suppose you’ve inherited a label that’s already underlined, but the design calls for plain bold text. You don’t want to lose the boldness while stripping the underline. Here’s where the `WebFontStyle` class shines.

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

**Key point:** Setting `Underline = false` explicitly tells the helper to *exclude* the underline flag. If you omitted the line altogether the previous underline would persist, which is a common source of bugs when developers only toggle the `Bold` property.

---

## Step 3 – Change Text Style: Bold, Italic, and More

You might wonder, “What if I need to toggle italic as well?” The same object works for any combination. Below is a quick matrix you can reference while coding.

| Desired Style | `Bold` | `Italic` | `Underline` |
|---------------|--------|----------|-------------|
| **Bold only** | true   | false    | false       |
| *Italic only* | false  | true     | false       |
| **Bold + Italic** | true   | true     | false       |
| **Bold + Underline** | true   | false    | true        |

Just set the properties you need and call `ToFont`. The helper does the heavy lifting for you, so you can focus on the UI logic.

---

## Full Example – Set Bold Text Programmatically

Below is a **complete, runnable WinForms** example that demonstrates everything we’ve covered. Paste it into a new console‑style WinForms project and hit **F5**.

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

### Expected Result

When you run the program, a window appears with the text **“Hello, world!”** rendered **bold**, **not italic**, and **without any underline**. That visual confirmation tells you the **apply font style** logic worked perfectly.

---

## Pro Tips & Edge Cases

- **Dynamic updates:** If you need to change the style after the form is shown (e.g., in response to a checkbox), just recreate the `WebFontStyle` instance or modify its properties and reassign `lbl.Font`. The UI updates instantly.
- **High‑DPI considerations:** When you replace a `Font` object, Windows automatically scales it based on the current DPI. No extra code needed unless you’re manually handling scaling.
- **WPF equivalent:** In WPF you’d bind `FontWeight`, `FontStyle`, and `TextDecorations` instead of swapping a `Font` object. The same logical separation applies—keep style logic out of the view layer.
- **Avoiding memory leaks:** Reassigning `Label.Font` creates a new `Font` object. Dispose of the old one if you’re swapping styles frequently: `var oldFont = lbl.Font; lbl.Font = newFont; oldFont.Dispose();`

---

## Conclusion

You now know how to **apply font style** to any .NET control, **remove underline from text**, and **change text style** on the fly—all while keeping your code clean and reusable. The tiny `WebFontStyle` helper turns a handful of boolean flags into a solid, testable component, and the full example proves you can **set bold text programmatically** in just a few lines.

What’s next? Try combining this approach with user‑driven settings, or experiment with other `FontStyle` flags like `Strikeout`. You could even expose a tiny UI panel that lets non‑technical users pick bold, italic, or underline at runtime—no recompilation required.

If you found this **text formatting tutorial** helpful, feel free to drop a comment or share your own variations. Happy coding, and may your UI always look exactly the way you intended! 

---

![Screenshot showing how to apply font style to a label in C#](https://example.com/images/apply-font-style.png

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
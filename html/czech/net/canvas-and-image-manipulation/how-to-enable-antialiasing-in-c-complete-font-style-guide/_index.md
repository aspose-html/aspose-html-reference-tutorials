---
category: general
date: 2026-03-02
description: Naučte se, jak povolit antialiasing a jak programově nastavit tučné písmo
  při použití hintingu a nastavení několika stylů písma najednou.
draft: false
keywords:
- how to enable antialiasing
- how to apply bold
- how to use hinting
- set font style programmatically
- set multiple font styles
language: cs
og_description: Objevte, jak povolit antialiasing, použít tučné písmo a využít hintingu
  při programovém nastavení více stylů písma v C#.
og_title: Jak povolit antialiasing v C# – Kompletní průvodce stylováním písma
tags:
- C#
- graphics
- text rendering
title: Jak povolit antialiasing v C# – Kompletní průvodce stylováním písma
url: /cs/net/canvas-and-image-manipulation/how-to-enable-antialiasing-in-c-complete-font-style-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak povolit antialiasing v C# – Kompletní průvodce stylů písma

Už jste se někdy zamýšleli **jak povolit antialiasing** při kreslení textu v .NET aplikaci? Nejste v tom sami. Většina vývojářů narazí na problém, když jejich UI vypadá zubatě na obrazovkách s vysokým DPI a oprava je často skryta za několika přepínači vlastností. V tomto tutoriálu vás provedeme přesnými kroky, jak zapnout antialiasing, **jak použít tučný styl**, a dokonce **jak použít hinting**, aby i nízké rozlišení displejů vypadaly ostře. Na konci budete schopni **nastavit styl písma programově** a kombinovat **více stylů písma** bez potíží.

Pokryjeme vše, co potřebujete: požadované jmenné prostory, kompletní spustitelný příklad, proč je každá vlajka důležitá a několik úskalí, na která můžete narazit. Žádná externí dokumentace, jen samostatný průvodce, který můžete zkopírovat a vložit do Visual Studia a okamžitě vidět výsledek.

## Požadavky

- .NET 6.0 nebo novější (používaná API jsou součástí `System.Drawing.Common` a malé pomocné knihovny)
- Základní znalost C# (víte, co je `class` a `enum`)
- IDE nebo textový editor (Visual Studio, VS Code, Rider — každý bude stačit)

Pokud to máte, pojďme na to.

---

## Jak povolit antialiasing při vykreslování textu v C#

Základ hladkého textu je vlastnost `TextRenderingHint` na objektu `Graphics`. Nastavením na `ClearTypeGridFit` nebo `AntiAlias` řeknete vykreslovači, aby prolnul okraje pixelů, čímž odstraní schodovitý efekt.

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

**Proč to funguje:** `TextRenderingHint.AntiAlias` nutí engine GDI+ prolnout okraje glyfu s pozadím, čímž vzniká hladší vzhled. Na moderních Windows počítačích je to obvykle výchozí nastavení, ale mnoho scénářů vlastního kreslení přepíná nápovědu na `SystemDefault`, proto ji nastavujeme explicitně.

> **Tip:** Pokud cílíte na monitory s vysokým DPI, kombinujte `AntiAlias` s `Graphics.ScaleTransform`, aby text zůstal ostrý po škálování.

### Očekávaný výsledek

Když spustíte program, otevře se okno zobrazující „Antialiasovaný text“ vykreslený bez zubatých okrajů. Porovnejte to se stejným řetězcem vykresleným bez nastavení `TextRenderingHint` — rozdíl je patrný.

---

## Jak programově použít tučný a kurzívní styl písma

Aplikace tučného (nebo jakéhokoli stylu) není jen nastavení booleanu; musíte kombinovat příznaky z výčtu `FontStyle`. Kódový úryvek, který jste viděli dříve, používá vlastní výčet `WebFontStyle`, ale princip je stejný jako u `FontStyle`.

```csharp
// Step 1: Create a CSS‑style container (simulated with FontStyle)
FontStyle combinedStyle = FontStyle.Bold | FontStyle.Italic;

// Step 2: Apply bold and italic font styles using the enum
Font styledFont = new Font("Segoe UI", 28, combinedStyle);
```

V reálném scénáři můžete styl uložit do konfiguračního objektu a použít jej později:

```csharp
public class TextOptions
{
    public FontStyle FontStyle { get; set; } = FontStyle.Regular;
    public bool UseAntialiasing { get; set; } = false;
    public bool UseHinting { get; set; } = false;
}
```

Pak jej použijte při kreslení:

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

**Proč kombinovat příznaky?** `FontStyle` je výčet typu bit‑field, což znamená, že každý styl (Bold, Italic, Underline, Strikeout) zabírá samostatný bit. Použití bitového OR (`|`) vám umožní je skládat bez přepsání předchozích voleb.

---

## Jak použít hinting pro nízké rozlišení displejů

Hinting posouvá obrysy glyfů tak, aby se zarovnaly s pixlovou mřížkou, což je nezbytné, když obrazovka nedokáže vykreslit subpixelové detaily. V GDI+ se hinting řídí pomocí `TextRenderingHint.SingleBitPerPixelGridFit` nebo `ClearTypeGridFit`.

```csharp
// Step 4: Turn on hinting to improve text rendering on low‑resolution displays
if (options.UseHinting)
{
    // SingleBitPerPixelGridFit works well on older LCD panels
    e.Graphics.TextRenderingHint = TextRenderingHint.SingleBitPerPixelGridFit;
}
```

### Kdy použít hinting

- **Monitory s nízkým DPI** (např. klasické 96 dpi displeje)
- **Bitmapové fonty**, kde záleží na každém pixelu
- **Aplikace citlivé na výkon**, kde je plný antialiasing příliš náročný

Pokud povolíte jak antialiasing *tak* hinting, vykreslovač upřednostní nejprve hinting a pak aplikuje vyhlazování. Pořadí je důležité; nastavte hinting **po** antialiasingu, pokud chcete, aby hinting působil na již vyhlazených glyfech.

---

## Nastavení více stylů písma najednou – Praktický příklad

Spojením všeho dohromady zde máte kompaktní demo, které:

1. **Povolí antialiasing** (`how to enable antialiasing`)
2. **Aplikuje tučný a kurzívní styl** (`how to apply bold`)
3. **Zapne hinting** (`how to use hinting`)
4. **Nastaví více stylů písma** (`set multiple font styles`)

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

#### Co byste měli vidět

Okno zobrazující **Bold + Italic + Hinted** v tmavě zelené barvě, s hladkými okraji díky antialiasingu a ostrým zarovnáním díky hintingu. Pokud některou vlajku zakomentujete, text bude buď zubatý (bez antialiasingu) nebo mírně nesprávně zarovnaný (bez hintingu).

---

## Často kladené otázky a okrajové případy

| Question | Answer |
|----------|--------|
| *Co když cílová platforma nepodporuje `System.Drawing.Common`?* | Na Windows s .NET 6+ můžete stále používat GDI+. Pro multiplatformní grafiku zvažte SkiaSharp — nabízí podobné možnosti antialiasingu a hintingu přes `SKPaint.IsAntialias`. |
| *Mohu kombinovat `Underline` s `Bold` a `Italic`?* | Ano. `FontStyle.Bold | FontStyle.Italic | FontStyle.Underline` funguje stejným způsobem. |
| *Ovlivňuje povolení antialiasingu výkon?* | Mírně, zejména na velkých plátnech. Pokud kreslíte tisíce řetězců za snímek, otestujte oba nastavení a rozhodněte se. |
| *Co když rodina fontů nemá tučnou váhu?* | GDI+ vytvoří syntetický tučný styl, který může vypadat těžší než skutečná tučná varianta. Vyberte font, který obsahuje nativní tučnou váhu pro nejlepší vizuální kvalitu. |
| *Existuje způsob, jak tato nastavení přepínat za běhu?* | Ano — stačí aktualizovat objekt `TextOptions` a zavolat `Invalidate()` na ovládacím prvku, aby se vynutilo překreslení. |

## Ilustrace obrázku

![Screenshot showing how to enable antialiasing in C# code and the resulting smooth text](/images/antialias-demo.png)

*Alt text:* **jak povolit antialiasing** — obrázek ukazuje kód a hladký výstup.

## Shrnutí a další kroky

Probrali jsme **jak povolit antialiasing** v kontextu grafiky C#, **jak použít tučný** a další styly programově, **jak použít hinting** pro displeje s nízkým rozlišením a nakonec **jak nastavit více stylů písma** v jedné řádce kódu. Kompletní příklad spojuje všechny čtyři koncepty a poskytuje připravené řešení.

Co dál? Můžete chtít:

- Prozkoumat **SkiaSharp** nebo **DirectWrite** pro ještě bohatší renderovací pipeline textu.
- Experimentovat s **dynamickým načítáním fontů** (`PrivateFontCollection`) pro balení vlastních typů písma.
- Přidat **uživatelsky řízené UI** (checkboxy pro antialiasing/hinting), abyste viděli dopad v reálném čase.

Klidně upravte třídu `TextOptions`, vyměňte fonty nebo integrujte tuto logiku do WPF nebo WinUI aplikace. Principy zůstávají stejné: set the

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
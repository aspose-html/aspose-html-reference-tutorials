---
category: general
date: 2026-06-25
description: Naučte se, jak v .NET povolit ClearType a zapnout režim vyhlazování pro
  ostřejší text a hladší grafiku. Postupujte podle tohoto krok‑za‑krokem průvodce
  s kompletním kódem.
draft: false
keywords:
- how to enable clear type
- enable smoothing mode
language: cs
og_description: Objevte, jak v .NET povolit ClearType a zapnout režim vyhlazování
  pro ostrou a hladkou grafiku pomocí kompletního spustitelného příkladu.
og_title: Jak povolit ClearType – povolit režim vyhlazování v .NET
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Learn how to enable Clear Type in .NET and enable smoothing mode for
    sharper text and smoother graphics. Follow this step‑by‑step guide with full code.
  headline: How to Enable Clear Type – Enable Smoothing Mode in .NET
  type: TechArticle
- description: Learn how to enable Clear Type in .NET and enable smoothing mode for
    sharper text and smoother graphics. Follow this step‑by‑step guide with full code.
  name: How to Enable Clear Type – Enable Smoothing Mode in .NET
  steps:
  - name: 1. Running on Non‑Windows Platforms
    text: 'Clear Type is a Windows‑only technology. If your app runs on macOS or Linux
      via .NET Core, the `ClearTypeGridFit` hint will silently fall back to a generic
      anti‑alias mode. To avoid confusion, you can guard the setting:'
  - name: 2. High‑DPI Scaling
    text: 'When the OS scales UI elements (e.g., 150% DPI), Clear Type can still look
      great, but you must ensure your form is DPI‑aware. In your project file add:'
  - name: 3. Performance Considerations
    text: Applying anti‑aliasing on a per‑frame basis (e.g., in a game loop) can be
      expensive. In such cases, pre‑render static elements to a bitmap with smoothing
      enabled, then blit the bitmap without re‑applying the settings each frame.
  - name: 4. Text Contrast
    text: Clear Type works best with dark text on a light background (or vice versa).
      If you’re drawing white text on a dark background, consider switching to `TextRenderingHint.ClearTypeGridFit`
      as shown, but also test readability; sometimes `TextRenderingHint.AntiAlias`
      gives a better visual on very dark su
  type: HowTo
tags:
- .NET graphics
- text rendering
- antialiasing
title: Jak povolit ClearType – povolit režim vyhlazování v .NET
url: /cs/net/advanced-features/how-to-enable-clear-type-enable-smoothing-mode-in-net/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak povolit Clear Type – povolit režim vyhlazování v .NET

Už jste se někdy zamysleli **jak povolit clear type** pro vaše .NET UI a získat text ostrý jako břitva? Nejste sami. Mnoho vývojářů narazí na problém, když štítky v aplikaci vypadají rozmazaně na obrazovkách s vysokým DPI, a oprava je překvapivě jednoduchá. V tomto tutoriálu projdeme přesné kroky, jak povolit clear type **a** povolit režim vyhlazování, aby vaše grafika získala vyleštěný vzhled.

Probereme vše, co potřebujete—od požadovaných jmenných prostorů až po konečný vizuální výsledek—takže na konci budete mít připravený úryvek k základnímu vložení, který můžete vložit do jakéhokoli projektu WinForms nebo WPF. Žádné odbočky, jen přímé a výstižné vedení.

## Požadavky

- .NET 6+ (API, které používáme, jsou součástí `System.Drawing.Common`, který je součástí .NET 6 a novějších)
- Počítač s Windows (ClearType je technologie renderování textu specifická pro Windows)
- Základní znalost C# a Visual Studio nebo vašeho oblíbeného IDE

Pokud vám něco chybí, stáhněte si nejnovější .NET SDK z webu Microsoftu—rychle a bez problémů.

## Co ve skutečnosti znamená “Clear Type” a “Smoothing Mode”

Clear Type je technika subpixelového renderování od Microsoftu, která způsobuje, že text vypadá hladší tím, že využívá fyzické uspořádání pixelů LCD. Představte si to jako chytrý způsob, jak oklamat oko, aby vidělo více detailů, než obrazovka skutečně dokáže zobrazit.

Režim vyhlazování se naopak stará o grafiku, která není textová—čáry, tvary a hrany. Povolení `SmoothingMode.AntiAlias` říká GDI+, aby smíchalo pixely na okrajích, čímž snižuje zubaté artefakty. Když oba spojíte, získáte UI, které působí *profesionálně* a *čitelně* i na monitorech s nízkým rozlišením.

## Krok 1 – Přidejte požadované jmenné prostory

First thing’s first: you need to bring the right types into scope. In a typical WinForms form file you’d start with:

```csharp
using System.Drawing;
using System.Drawing.Drawing2D;
using System.Drawing.Text;
```

Tyto tři jmenné prostory vám poskytují přístup k `ImageRenderingOptions`, `SmoothingMode` a `TextRenderingHint`. Pokud některý zapomenete, kompilátor si stěžuje a budete se ptát, proč se kód nedaří zkompilovat.

## Krok 2 – Vytvořte instanci `ImageRenderingOptions`

Nyní, když jsou importy na místě, vytvořme objekt, který bude uchovávat naše nastavení renderování. Tento objekt je nenáročný a může být znovu použit v několika voláních kreslení.

```csharp
// Step 2: Create rendering options for image processing
ImageRenderingOptions renderingOptions = new ImageRenderingOptions();
```

Proč objekt `ImageRenderingOptions`? Protože spojuje vše, co potřebujete—vyhlazování, tipy pro text a dokonce i posun pixelů—takže nemusíte nastavovat každou vlastnost na objektu Graphics jednotlivě. Udržuje kód přehledný a usnadňuje budoucí úpravy.

## Krok 3 – Povolit režim vyhlazování pro anti‑aliasované hrany

Zde **povolíme režim vyhlazování**. Bez něj bude každá nakreslená čára vypadat jako soubor malých schodů.

```csharp
// Step 3: Enable anti‑aliasing for smoother edges
renderingOptions.SmoothingMode = SmoothingMode.AntiAlias;
```

Nastavení `SmoothingMode.AntiAlias` říká GDI+, aby smíchalo barvy na hraně tvarů, čímž vznikne měkký přechod napodobující přirozené křivky. Pokud někdy potřebujete výkon nad vizuální kvalitou, můžete přepnout na `SmoothingMode.HighSpeed`, ale pro UI práci je anti‑aliasing obvykle stojí za drobný dopad na CPU.

## Krok 4 – Řekněte rendereru, aby použil Clear Type

Nyní konečně odpovídáme na hlavní otázku: **jak povolit clear type**. Vlastnost, kterou musíme nastavit, je `TextRenderingHint`.

```csharp
// Step 4: Set text rendering hint for clearer text
renderingOptions.TextRenderingHint = TextRenderingHint.ClearTypeGridFit;
```

`ClearTypeGridFit` je optimální volba pro většinu scénářů—zarovnává Clear Type s mřížkou pixelů zařízení, čímž odstraňuje rozmazané hrany, které se mohou objevit, když je text kreslen mimo mřížku. Pokud cílíte na starší hardware, můžete experimentovat s `TextRenderingHint.AntiAliasGridFit`, ale Clear Type obecně poskytuje nejlepší čitelnost na moderních LCD panelech.

## Krok 5 – Použijte nastavení při kreslení

Vytvoření nastavení je jen polovina boje; musíte je skutečně aplikovat na objekt `Graphics`. Níže je minimální přepsání WinForms `OnPaint`, které ukazuje celý proces.

```csharp
protected override void OnPaint(PaintEventArgs e)
{
    base.OnPaint(e);

    // Grab the Graphics context
    Graphics g = e.Graphics;

    // Apply our rendering options
    g.SmoothingMode = renderingOptions.SmoothingMode;
    g.TextRenderingHint = renderingOptions.TextRenderingHint;

    // Draw a sample string
    using (Font font = new Font("Segoe UI", 24, FontStyle.Regular))
    {
        g.DrawString("Clear Type + Smoothing", font, Brushes.Black, new PointF(10, 20));
    }

    // Draw a diagonal line to showcase anti‑aliasing
    using (Pen pen = new Pen(Color.Blue, 2))
    {
        g.DrawLine(pen, new Point(10, 80), new Point(300, 200));
    }
}
```

Všimněte si, že hodnoty `renderingOptions` přenášíme do objektu `Graphics` před jakýmkoli kreslením. To zaručuje, že každý následující volání kreslení respektuje jak Clear Type, tak anti‑aliasing. Příklad vykresluje text a čáru; text by měl být ostrý a čára hladká—žádné zubaté hrany.

## Očekávaný výstup

Když spustíte formulář, měli byste vidět:

- Fráze **“Clear Type + Smoothing”** vykreslená s břitko ostrými znaky, zejména patrná na LCD monitorech.
- Modrá úhlopříčná čára, která vypadá měkce po okrajích místo zubatého schodiště.

Pokud to porovnáte s verzí, kde je `SmoothingMode` ponechán na výchozím (`None`) a `TextRenderingHint` je `SystemDefault`, rozdíly jsou výrazné—rozmazaný text a drsné čáry oproti vyleštěnému výsledku výše.

## Okrajové případy a časté úskalí

### 1. Běh na ne‑Windows platformách

Clear Type je Windows‑only technologie. Pokud vaše aplikace běží na macOS nebo Linuxu přes .NET Core, nápověda `ClearTypeGridFit` tiše přejde na obecný anti‑alias režim. Aby nedošlo ke zmatení, můžete nastavení ošetřit:

```csharp
if (RuntimeInformation.IsOSPlatform(OSPlatform.Windows))
{
    renderingOptions.TextRenderingHint = TextRenderingHint.ClearTypeGridFit;
}
```

### 2. Škálování při vysokém DPI

Když OS škáluje UI prvky (např. 150 % DPI), Clear Type může stále vypadat skvěle, ale musíte zajistit, že je váš formulář DPI‑aware. Ve vašem souboru projektu přidejte:

```xml
<PropertyGroup>
  <EnableWindowsFormsHighDpi>True</EnableWindowsFormsHighDpi>
</PropertyGroup>
```

### 3. Úvahy o výkonu

Aplikace anti‑aliasingu na každém snímku (např. ve smyčce hry) může být nákladná. V takových případech předrenderujte statické prvky do bitmapy s povoleným vyhlazováním a poté bitmapu zobrazte bez opětovného nastavení parametrů v každém snímku.

### 4. Kontrast textu

Clear Type funguje nejlépe s tmavým textem na světlém pozadí (nebo naopak). Pokud kreslíte bílý text na tmavém pozadí, zvažte přepnutí na `TextRenderingHint.ClearTypeGridFit`, jak je ukázáno, ale také otestujte čitelnost; někdy `TextRenderingHint.AntiAlias` poskytne lepší vzhled na velmi tmavých plochách.

## Pro tipy – Vytěžené maximum z Clear Type

- **Používejte písma kompatibilní s ClearType**: Segoe UI, Calibri a Verdana jsou navrženy s ohledem na sub‑pixelové renderování.
- **Vyhněte se sub‑pixelovému umístění**: Zarovnejte text na celo‑pixelové souřadnice (`new PointF(10, 20)` funguje; `new PointF(10.3f, 20.7f)` může způsobit rozmazání).
- **Kombinujte s `PixelOffsetMode.Half`**: Toto posune kreslicí operace o půl pixelu, což často vede k ostřejším čarám při zapnutém anti‑aliasingu.

```csharp
g.PixelOffsetMode = PixelOffsetMode.Half;
```

- **Testujte na více monitorech**: Různé panely (IPS vs. TN) renderují Clear Type mírně odlišně; rychlá vizuální kontrola ušetří pozdější problémy.

## Kompletní funkční příklad

Níže je samostatný úryvek projektu WinForms, který můžete vložit do nové třídy formuláře. Obsahuje všechny části, o kterých jsme mluvili, od using direktiv po metodu `OnPaint`.



Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak povolit antialiasing v C# – Hladké hrany](/html/english/net/canvas-and-image-manipulation/how-to-enable-antialiasing-in-c-smooth-edges/)
- [Jak povolit antialiasing při konverzi DOCX na PNG/JPG](/html/english/net/generate-jpg-and-png-images/how-to-enable-antialiasing-when-converting-docx-to-png-jpg/)
- [Jak renderovat HTML jako PNG – Kompletní C# průvodce](/html/english/net/rendering-html-documents/how-to-render-html-as-png-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
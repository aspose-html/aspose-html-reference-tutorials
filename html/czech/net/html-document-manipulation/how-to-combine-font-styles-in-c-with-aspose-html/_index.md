---
category: general
date: 2026-10-15
description: Kombinujte styly písma v C# nastavením rodiny písma a velikosti pomocí
  konstruktoru Aspose.HTML Font. Naučte se rychle vytvářet tučný kurzívní text.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- combine font styles
- set font family
- set font size c#
- c# font constructor
- create bold italic text
language: cs
lastmod: 2026-10-15
og_description: Kombinujte styly písma v C# pomocí konstruktoru Aspose.HTML Font.
  Tento tutoriál ukazuje, jak nastavit rodinu písma, nastavit velikost písma v C#
  a vytvořit tučný kurzívní text.
og_image_alt: Screenshot of C# code that combines font styles with Aspose.HTML
og_title: Kombinujte styly písma v C# – rychlý průvodce s Aspose.HTML
schemas:
- author: Aspose
  dateModified: '2026-10-15'
  description: Combine font styles in C# by setting font family and size using the
    Aspose.HTML Font constructor. Learn to create bold italic text quickly.
  headline: How to combine font styles in C# with Aspose.HTML
  type: TechArticle
- description: Combine font styles in C# by setting font family and size using the
    Aspose.HTML Font constructor. Learn to create bold italic text quickly.
  name: How to combine font styles in C# with Aspose.HTML
  steps:
  - name: Explanation
    text: '- `"Arial"` – **set font family** to Arial, a widely supported sans‑serif
      typeface. - `12` – **set font size c#** to 12 points, which is a comfortable
      default for body text. - `WebFontStyle.Bold | WebFontStyle.Italic` – this expression
      **combines font styles**. The `|` operator merges the `Bold` and'
  - name: Why this works
    text: '- `paragraph.Style.FontFamily` uses the **set font family** value from
      the `Font` instance. - `paragraph.Style.FontSize` uses the **set font size c#**
      you defined. - The explicit `FontWeight` and `FontStyle` assignments mirror
      the **combine font styles** flags, ensuring the rendered output matches t'
  - name: Pro tip on performance
    text: 'Creating many `Font` objects inside a tight loop can degrade performance.
      Cache commonly used fonts in a dictionary and reuse them:'
  type: HowTo
tags:
- C#
- Aspose.HTML
- Font styling
title: Jak kombinovat styly písma v C# s Aspose.HTML
url: /cs/net/html-document-manipulation/how-to-combine-font-styles-in-c-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak kombinovat styly písma v C# s Aspose.HTML

Pokud potřebujete **kombinovat styly písma** v aplikaci C#, tento návod vám ukáže stručný způsob, jak to provést pomocí Aspose.HTML. Naučíte se, jak nastavit rodinu písma, **nastavit velikost písma c#** a použít **c# font constructor** k vytvoření tučného kurzívního textu během několika řádků kódu.

Vývojáři se často ptají, zda musí vytvářet samostatné objekty `Font` pro každý styl, nebo zda jeden konstruktor může zvládnout více atributů. Odpověď je, že styly můžete kombinovat přímo při vytváření písma. Tento tutoriál vás provede celým procesem, od importu správného jmenného prostoru až po vykreslení stylovaného textu v HTML dokumentu.

## Požadavky

Než začnete, ujistěte se, že máte:

- Aspose.HTML pro .NET nainstalováno (NuGet balíček `Aspose.HTML` verze 23.9 nebo novější).
- .NET 6.0+ nebo .NET Framework 4.7.2+.
- Základní znalost syntaxe C# a objektově orientovaného programování.
- Nejsou vyžadovány žádné další knihovny třetích stran.

## Krok 1: Importujte namespace pro kreslení

První věc, kterou musíte udělat, je **importovat jmenný prostor Aspose.Html.Drawing**, abyste měli přístup ke třídě `Font` a souvisejícím kreslicím utilitám.

```csharp
using Aspose.Html.Drawing;
```

> **Proč?** Třída `Font` se nachází v `Aspose.Html.Drawing`. Import tohoto jmenného prostoru zpřístupní typ bez nutnosti pokaždé ho plně kvalifikovat, což udržuje váš kód čistý a čitelný.

## Krok 2: Použijte konstruktor písma v C# k nastavení rodiny, velikosti a kombinaci stylů

**c# font constructor** přijímá tři parametry: název rodiny písma, velikost v bodech a bitovou kombinaci příznaků `WebFontStyle`. Použitím bitového OR operátoru (`|`) můžete **kombinovat styly písma** jako tučný a kurzíva.

```csharp
// Create a Font instance that is both bold and italic
var font = new Font("Arial", 12, WebFontStyle.Bold | WebFontStyle.Italic);
```

### Vysvětlení

- `"Arial"` – **nastavte rodinu písma** na Arial, široce podporované písmo bez patky.
- `12` – **nastavte velikost písma c#** na 12 bodů, což je pohodlná výchozí hodnota pro tělo textu.
- `WebFontStyle.Bold | WebFontStyle.Italic` – tento výraz **kombinuje styly písma**. Operátor `|` sloučí příznaky `Bold` a `Italic` do jedné hodnoty, což konstruktoru umožní vytvořit písmo, které je současně tučné *i* kurzívní.

> **Tip:** Pokud potřebujete přidat podtržení nebo přeškrtnutí, zahrňte `WebFontStyle.Underline` nebo `WebFontStyle.Strikethrough` do stejného výrazu.

## Krok 3: Použijte písmo na HTML prvek

Nyní, když máte objekt `Font`, můžete jej použít na libovolný HTML prvek, který podporuje stylování. Níže vytvoříme jednoduchý HTML dokument, přidáme odstavec a přiřadíme kombinovaný styl.

```csharp
using Aspose.Html;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;

// Create a new HTML document
var document = new HTMLDocument();

// Add a paragraph element
var paragraph = document.CreateElement("p");
paragraph.InnerHtml = "This text is bold and italic using combined font styles.";
document.Body.AppendChild(paragraph);

// Apply the Font object to the paragraph's style
paragraph.Style.FontFamily = font.Family;
paragraph.Style.FontSize = $"{font.Size}pt";
paragraph.Style.FontWeight = "bold";
paragraph.Style.FontStyle = "italic";

// Render the document to an image (optional verification step)
using (var renderer = new ImageRenderer())
{
    renderer.Render(document, "output.png");
}
```

### Proč to funguje

- `paragraph.Style.FontFamily` používá **nastavenou rodinu písma** z instance `Font`.
- `paragraph.Style.FontSize` používá **nastavenou velikost písma c#**, kterou jste definovali.
- Explicitní přiřazení `FontWeight` a `FontStyle` odráží příznaky **kombinovat styly písma**, což zajišťuje, že vykreslený výstup odpovídá zamýšlenému tučně‑kurzívnímu vzhledu.

> **Hraniční případ:** Pokud cílová rodina písma nepodporuje kurzívu nebo tučné varianty, prohlížeč může styl simulovat, což může ovlivnit vizuální věrnost. Vždy testujte se skutečným písmem, které plánujete distribuovat.

## Krok 4: Ověřte výsledek

Spusťte program a otevřete `output.png`. Měli byste vidět větu vykreslenou v Arial, 12 pt, s aplikovaným tučným i kurzívním stylem. To potvrzuje, že **c# font constructor** správně kombinoval styly.

Pokud raději chcete zobrazit HTML přímo, můžete krok vykreslování přeskočit a dokument uložit:

```csharp
document.Save("styled.html");
```

Otevřete `styled.html` v libovolném moderním prohlížeči a uvidíte stejný stylovaný odstavec.

## Běžné varianty a tipy

| Cíl | Ukázka kódu | Poznámky |
|------|--------------|-------|
| **Pouze tučné** | `new Font("Arial", 12, WebFontStyle.Bold)` | Použijte jediný příznak, pokud nepotřebujete kurzívu. |
| **Tučné, kurzíva, podtržení** | `new Font("Arial", 12, WebFontStyle.Bold \| WebFontStyle.Italic \| WebFontStyle.Underline)` | Kombinujte libovolný počet stylů. |
| **Dynamická velikost** | `var size = 14; var font = new Font("Times New Roman", size, WebFontStyle.Italic);` | Velikost můžete vypočítat za běhu. |
| **Vlastní rodina písma** | `new Font("MyCustomFont", 10, WebFontStyle.Bold)` | Ujistěte se, že vlastní písmo je dostupné vykreslovacímu enginu (např. pomocí `@font-face`). |

### Tip pro výkon

Vytváření mnoha objektů `Font` uvnitř úzké smyčky může snížit výkon. Uložte často používaná písma do slovníku a znovu je použijte:

```csharp
var fontCache = new Dictionary<string, Font>();
string key = "Arial_12_BoldItalic";

if (!fontCache.TryGetValue(key, out var cachedFont))
{
    cachedFont = new Font("Arial", 12, WebFontStyle.Bold | WebFontStyle.Italic);
    fontCache[key] = cachedFont;
}
```

## Úplný spustitelný příklad

Níže je samostatný program, který můžete zkopírovat, vložit a spustit. Ukazuje celý tok od importu jmenného prostoru až po vykreslení stylovaného textu.

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Rendering.Image;

class Program
{
    static void Main()
    {
        // Step 1: Import Aspose.Html.Drawing (already done via using statements)

        // Step 2: Create a Font that combines bold and italic
        var font = new Font("Arial", 12, WebFontStyle.Bold | WebFontStyle.Italic);

        // Step 3: Build a simple HTML document
        var document = new HTMLDocument();
        var paragraph = document.CreateElement("p");
        paragraph.InnerHtml = "This text is bold and italic using combined font styles.";
        document.Body.AppendChild(paragraph);

        // Apply font settings
        paragraph.Style.FontFamily = font.Family;
        paragraph.Style.FontSize = $"{font.Size}pt";
        paragraph.Style.FontWeight = "bold";
        paragraph.Style.FontStyle = "italic";

        // Optional: Render to PNG for visual verification
        using (var renderer = new ImageRenderer())
        {
            renderer.Render(document, "output.png");
        }

        // Save HTML for manual inspection
        document.Save("styled.html");

        Console.WriteLine("Styled document generated: styled.html and output.png");
    }
}
```

### Očekávaný výstup

- `styled.html` zobrazuje odstavec s Arial 12 pt, tučný a kurzívní.
- `output.png` obsahuje obrázek stejného stylovaného odstavce.

## Závěr

Nyní víte, jak **kombinovat styly písma** v C# pomocí Aspose.HTML **c# font constructor**. Použitím **nastavit rodinu písma**, **nastavit velikost písma c#** a předáním bitového OR příznaků `WebFontStyle` můžete **vytvořit tučný kurzívní text** (nebo jakoukoli jinou kombinaci) s minimálním množstvím kódu. Použijte stejný vzor i pro jiné prvky, cachujte písma pro výkon a rozšiřte přístup o podtržení nebo přeškrtnutí podle potřeby.

Chcete-li pokračovat, zkuste:

- Použít `WebFontStyle.Underline` k **nastavení podtržení písma**.
- Načíst vlastní webová písma pomocí `@font-face` a aplikovat je stejným konstruktorem.
- Renderovat PDF místo obrázků výměnou `ImageRenderer` za `PdfRenderer`.

Šťastné programování a užívejte si flexibilitu stylování textu programově v C#!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, která vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Vytvořit HTML dokument C# – tučný kurzívní text s vlastním písmem](/html/english/net/html-document-manipulation/create-html-document-c-bold-italic-text-with-custom-font/)
- [Vytvořit HTML dokument C# – renderovat do PNG s tučným kurzívním písmem](/html/english/net/rendering-html-documents/create-html-document-c-render-to-png-with-bold-italic-font/)
- [Uložit HTML jako PDF v C# – Kompletní průvodce s písmy](/html/indonesian/net/html-extensions-and-conversions/save-html-as-pdf-in-c-complete-guide-with-fonts/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
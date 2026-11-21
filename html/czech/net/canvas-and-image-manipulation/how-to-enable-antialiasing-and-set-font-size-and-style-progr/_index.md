---
category: general
date: 2026-11-20
description: Jak povolit antialiasing v grafice C# a nastavit velikost písma, nastavit
  styl písma programově s kompletním, spustitelným příkladem pomocí ImageRenderingOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable antialiasing
- set font size
- set font style programmatically
- C# graphics rendering
- ImageRenderingOptions example
language: cs
lastmod: 2026-11-20
og_description: Jak povolit antialiasing v grafice C#, nastavit velikost písma a styl
  písma programově pomocí ImageRenderingOptions – kompletní kód a vysvětlení.
og_image_alt: Screenshot of antialiased text with custom font size and style generated
  by C# code showing how to enable antialiasing
og_title: Jak programově povolit vyhlazování a nastavit velikost a styl písma v C#
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: How to enable antialiasing in C# graphics and set font size, set font
    style programmatically with a complete, runnable example using ImageRenderingOptions.
  headline: How to enable antialiasing and set font size and style programmatically
    in C#
  type: TechArticle
tags:
- C#
- graphics
- antialiasing
- fonts
title: Jak programově povolit vyhlazování a nastavit velikost a styl písma v C#
url: /cs/net/canvas-and-image-manipulation/how-to-enable-antialiasing-and-set-font-size-and-style-progr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak programově povolit antialiasing a nastavit velikost a styl písma v C#

Povolení antialiasingu v grafice C# je častý požadavek, když potřebujete hladké hrany tvarů nebo textu. Tento tutoriál vám ukáže, jak povolit antialiasing, nastavit velikost písma a nastavit styl písma programově pomocí třídy **ImageRenderingOptions**. Na konci průvodce budete mít samostatnou konzolovou aplikaci, která vykreslí ostrý, stylovaný text do souboru obrázku.

Naučíte se, jak nakonfigurovat renderovací pipeline, vybrat správnou rodinu písma, upravit velikost písma a aplikovat tučné nebo kurzívní styly, aniž byste opustili svůj kód. Jedinou podmínkou je aktuální .NET SDK a NuGet balíček Aspose.Imaging, který příklad nainstaluje automaticky.

## Požadavky

- .NET 6.0 SDK nebo novější (stáhněte z https://dotnet.microsoft.com/)
- Visual Studio 2022 nebo jakýkoli editor, který podporuje .NET projekty
- **Aspose.Imaging** NuGet balíček (knihovna, která poskytuje `ImageRenderingOptions`)

Můžete přidat balíček pomocí následujícího příkazu:

```bash
dotnet add package Aspose.Imaging
```

## Jak povolit antialiasing pomocí ImageRenderingOptions

`ImageRenderingOptions` je centrální objekt, který řídí, jak Aspose.Imaging vykresluje grafiku. Nastavením jeho vlastnosti `UseAntialiasing` řeknete rasterizéru, aby vyhladil hrany, což eliminuje zubatý „schodišťový“ efekt, který se objeví, když je antialiasing vypnutý.

```csharp
// Step 1: Create a new ImageRenderingOptions instance
ImageRenderingOptions renderingOptions = new ImageRenderingOptions();

// Step 2: Enable antialiasing for smoother graphics
renderingOptions.UseAntialiasing = true;
```

Povolení antialiasingu je nezbytné pro vysoce kvalitní UI prvky, vykreslování grafů a jakoukoli situaci, kde záleží na vizuální věrnosti.

## Nastavení velikosti písma programově

Velikost písma určuje, jak velké glify budou v konečném bitmapu. Můžete ji změnit vytvořením objektu `Font` s požadovanou velikostí v bodech. Níže uvedený příklad nastavuje velikost na **24 pt**, což je běžná velikost pro čitelné nadpisy.

```csharp
// Step 3: Choose a font family and size
Font font = new Font("Arial", 24); // 24‑point Arial
```

Můžete nahradit `24` libovolným celým nebo desetinným číslem, aby vyhovovalo vašim požadavkům na rozvržení. Třída `Font` také přijímá parametr `GraphicsUnit`, pokud potřebujete velikost založenou na pixelech.

## Nastavení stylu písma programově

Aplikace tučného, kurzívního nebo podtrženého stylu spočívá v předání příznaku `WebFontStyle` při vytváření objektu `Font`. Výčtový typ `WebFontStyle` kombinuje více stylů pomocí bitové operace OR.

```csharp
// Step 4: Apply bold and italic styles
font = new Font("Arial", 24, WebFontStyle.Bold | WebFontStyle.Italic);
```

Pokud potřebujete jen jeden styl, použijte `WebFontStyle.Bold`, `WebFontStyle.Italic` nebo `WebFontStyle.Underline`. Tento přístup vám umožní **nastavit styl písma programově** bez pevného kódování samostatných souborů písma.

## Kompletní spustitelný příklad

Níže je kompletní konzolová aplikace, která spojuje všechny části dohromady:

```csharp
using System;
using Aspose.Imaging;
using Aspose.Imaging.Brushes;
using Aspose.Imaging.ImageOptions;
using Aspose.Imaging.Sources;
using Aspose.Imaging.FileFormats.Png;
using Aspose.Imaging.Graphics;
using Aspose.Imaging.Fonts;
using Aspose.Imaging.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Create rendering options and enable antialiasing
        ImageRenderingOptions renderingOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            // Enable hinting for sharper text on low‑resolution images
            TextOptions = new TextOptions { UseHinting = true }
        };

        // 2️⃣ Define the font (size + style)
        Font font = new Font("Arial", 24, WebFontStyle.Bold | WebFontStyle.Italic);

        // 3️⃣ Prepare a bitmap with a white background
        int width = 800;
        int height = 200;
        using (var bitmap = new RasterImage(width, height, PixelFormat.Format24bppRgb))
        {
            bitmap.SaveOptions = new PngOptions { ColorType = PngColorType.Truecolor };
            bitmap.Fill(new SolidBrush(Color.White));

            // 4️⃣ Create a graphics object that respects our rendering options
            using (Graphics graphics = new Graphics(bitmap, renderingOptions))
            {
                // Position the text in the center of the image
                PointF location = new PointF(50, 80);
                graphics.DrawString("Antialiased Bold Italic Text", font, new SolidBrush(Color.Black), location);
            }

            // 5️⃣ Save the result
            string outputPath = "antialiased_text.png";
            bitmap.Save(outputPath);
            Console.WriteLine($"Image saved to {outputPath}");
        }
    }
}
```

### Vysvětlení jednotlivých částí

| Sekce | Proč je důležité |
|---------|----------------|
| **Rendering options** | Zapnutí `UseAntialiasing` zaručuje hladké hrany jak pro vektorové tvary, tak pro text. |
| **TextOptions.UseHinting** | Hinting zlepšuje čitelnost při nízkém rozlišení úpravou obrysů glifů. |
| **Font construction** | Konstruktor `Font` kombinuje **nastavení velikosti písma** a **nastavení stylu písma programově** v jediném volání. |
| **Graphics object** | Předání `renderingOptions` do `Graphics` zajišťuje, že každá kreslicí operace respektuje antialiasing a hinting. |
| **DrawString** | Tato metoda vykresluje text s nastaveným písmem a vytváří finální antialiasovaný výstup. |
| **Saving** | Formát PNG zachovává přesná data pixelů bez dalších artefaktů komprese. |

#### Očekávaný výstup

Spuštěním programu se vytvoří **antialiased_text.png**, který vypadá takto:

![Příklad antialiasovaného textu](https://example.com/antialiased_text.png "Antialiasovaný text s vlastním nastavením velikosti a stylu – jak povolit antialiasing")

Obrázek ukazuje ostrý, tučně‑kurzívní text Arial vykreslený ve velikosti 24 pt s hladkými hranami, což potvrzuje, že **jak povolit antialiasing** fungovalo podle očekávání.

## Běžné varianty a okrajové případy

- **Různé rodiny písem** – Nahraďte `"Arial"` libovolným nainstalovaným názvem písma (např. `"Times New Roman"`). Pokud písmo není k dispozici, Aspose.Imaging vyhodí `FontNotFoundException`.
- **Změna velikosti písma** – Upravte druhý argument konstruktoru `Font` na libovolnou desetinnou hodnotu. Větší hodnoty zvyšují čitelnost, ale mohou vyžadovat větší bitmapu.
- **Více stylů** – Kombinujte `WebFontStyle.Underline` s `Bold` a `Italic` pomocí operátoru `|`: `WebFontStyle.Bold | WebFontStyle.Underline`.
- **Vysoké DPI vykreslování** – Pro výstup ve stylu retina zvětšete rozměry bitmapy (např. 1600 × 400) při zachování stejné velikosti písma; antialiasing stále poskytne hladké výsledky.
- **Vypnutí antialiasingu** – Nastavte `renderingOptions.UseAntialiasing = false;` pro porovnání vizuálního rozdílu. Text bude zubatý, což je užitečné pro ladění nebo testování výkonu.

## Profesionální tipy

- **Ukládejte objekt `Font` do cache** pokud v cyklu kreslíte mnoho řetězců; vytvoření nového `Font` v každé iteraci přidává režii.
- **Používejte `TextOptions.UseHinting` spolu s antialiasingem** pro nejlepší kompromis mezi ostrostí a hladkostí na nízkých rozlišeních obrázků.
- **Ověřte výstupní soubor** otevřením v prohlížeči obrázků, který zobrazuje detail na úrovni pixelů (např. Photoshop nebo GIMP). To vám pomůže potvrdit, že antialiasing skutečně působil.

## Závěr

Nyní víte, **jak povolit antialiasing** v grafice C#, jak **nastavit velikost písma** a jak **nastavit styl písma programově** pomocí `ImageRenderingOptions`. Kompletní příklad ukazuje praktický workflow, který můžete zkopírovat do svých projektů, ať už generujete grafy, vytváříte miniatury UI nebo produkujete dynamickou grafiku pro webové služby.

Dále můžete zkoumat **nastavení barvy písma programově**, přidat **gradientové výplně** nebo vykreslovat **vektorové tvary** se stejnými nastaveními antialiasingu. Všechny tyto témata staví na základech zde popsaných, takže jste dobře připraveni vytvářet vysoce kvalitní grafiku kompletně z kódu. Šťastné renderování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak povolit antialiasing při renderování HTML do PNG v C#](/html/english/net/rendering-html-documents/how-to-enable-antialiasing-when-rendering-html-to-png-in-c/)
- [Jak povolit antialiasing pro renderování HTML obrázků v C#](/html/english/net/rendering-html-documents/how-to-enable-antialiasing-for-html-image-rendering-in-c/)
- [Jak povolit antialiasing v konverzi Aspose HTML do PDF (C#)](/html/english/net/html-extensions-and-conversions/how-to-enable-antialiasing-in-aspose-html-to-pdf-conversion/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
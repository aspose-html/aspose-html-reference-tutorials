---
category: general
date: 2026-05-28
description: Naučte se, jak vytvořit vlastní manipulátor zdrojů v C# pro vykreslení
  webové stránky do obrázku, zachycení snímku obrazovky webové stránky a uložení HTML
  jako PNG s kompletním kódem.
draft: false
keywords:
- custom resource handler
- render webpage to image
- capture webpage screenshot
- render html to png
- save webpage as png
language: cs
og_description: Vytvořte vlastní handler zdrojů v C# a renderujte webovou stránku
  do obrázku. Pořiďte snímek obrazovky, renderujte HTML do PNG a uložte výsledek s
  kompletním příkladem.
og_title: Vlastní obslužná rutina zdrojů v C# – Vykreslení webové stránky do obrázku
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to create a custom resource handler in C# to render webpage
    to image, capture webpage screenshot and save HTML as PNG with complete code.
  headline: Custom Resource Handler in C# – Render Webpage to Image
  type: TechArticle
- description: Learn how to create a custom resource handler in C# to render webpage
    to image, capture webpage screenshot and save HTML as PNG with complete code.
  name: Custom Resource Handler in C# – Render Webpage to Image
  steps:
  - name: Expected Output
    text: Running the full program should produce a PNG that looks like a faithful
      snapshot of `https://example.com`. Open it in any image viewer, and you’ll see
      the page rendered at the default viewport size (usually 1024 × 768 px). All
      linked images and styles are stored alongside, ready for reuse.
  - name: What if the target page uses relative URLs?
    text: Our handler already strips the leading slash (`info.Path.TrimStart('/')`)
      and combines it with the output folder, so relative paths resolve correctly.
      If you encounter a URL that starts with `//` (protocol‑relative), the renderer
      normalizes it before calling `HandleResource`.
  - name: How do I change the output dimensions?
    text: 'Pass a `Size` object to `RenderPage` overload:'
  - name: Can I render multiple pages in one run?
    text: Absolutely. Just loop over a list of URLs and call `RenderPage` each time.
      The same `MyResourceHandler` instance will keep populating the `output` folder,
      keeping everything tidy.
  - name: What about authentication‑protected sites?
    text: If the page requires cookies or HTTP headers, configure an `HttpClient`
      and assign it to the renderer’s `HttpClient` property (if your library exposes
      it). This keeps the **render html to png** flow seamless for internal dashboards.
  type: HowTo
tags:
- C#
- ImageRenderer
- WebAutomation
title: Vlastní handler zdrojů v C# – Vykreslení webové stránky do obrázku
url: /cs/net/generate-jpg-and-png-images/custom-resource-handler-in-c-render-webpage-to-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vlastní manipulátor zdrojů v C# – Vykreslení webové stránky do obrázku

Už jste se někdy zamýšleli, jak pomocí **custom resource handler** získat dokonalý snímek obrazovky libovolného webu? Nejste v tom sami. Zachycení snímku webové stránky programově může připomínat honbu za pohyblivým cílem, zejména když potřebujete, aby obrázky a fonty byly uloženy přesně tam, kde je chcete.

V tomto návodu vás provedeme tvorbou **custom resource handler** v C#, nastavením možností vykreslování a nakonec použitím ImageRenderer k **render webpage to image**. Na konci budete vědět, jak **capture webpage screenshot**, **render html to png** a **save webpage as png** bez toho, abyste si trhali vlasy.

## Co budete potřebovat

- .NET 6.0 nebo novější (API, které používáme, cílí na .NET Standard 2.0, takže funguje jakékoli moderní runtime)
- NuGet balíček, který poskytuje `ImageRenderer`, `ImageRenderingOptions` a související typy (např. *Aspose.HTML* nebo podobná knihovna)
- Základní znalost C# – nic exotického, jen pár `using` direktiv a metoda `Main`
- Výstupní složka, kam může renderer ukládat soubory (klidně ji vytvořte ručně nebo nechte kód, aby ji vytvořil)

A to je vše. Žádné extra služby, žádné headless prohlížeče, jen čistý .NET kód.

![Custom resource handler saving rendered resources](https://example.com/assets/custom-resource-handler.png "custom resource handler")

## Krok 1: Vytvořte **Custom Resource Handler**

Prvním, co potřebujete, je třída dědící z `ResourceHandler`. Zde se děje kouzlo: každý obrázek, CSS soubor nebo font, který renderer požaduje, je směrován přes váš handler, a vy rozhodujete, kam jej uložit.

```csharp
using System.IO;
using Aspose.Html.Rendering.Image;   // Adjust the namespace to your library

// Step 1: Create a custom resource handler to store rendered resources
class MyResourceHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info)
    {
        // Build a safe file path inside the output directory
        string filePath = Path.Combine("output", info.Path.TrimStart('/'));

        // Ensure the directory hierarchy exists
        Directory.CreateDirectory(Path.GetDirectoryName(filePath)!);

        // Return a writable stream that the renderer will fill
        return File.OpenWrite(filePath);
    }
}
```

**Proč je to důležité:** Bez handleru může renderer uchovávat zdroje v paměti nebo je úplně zahazovat. Poskytnutím `Stream` získáte plnou kontrolu nad tím, kam se každý asset uloží – ideální pro pozdější opětovné použití nebo ladění.

## Krok 2: Nastavte možnosti vykreslování obrázku

Nyní, když máme místo pro assety, řekněme rendereru, jak má finální obrázek vypadat. Antialiasing vyhlazuje hrany, hinting zlepšuje čitelnost textu a výběr fontu zajišťuje, že výstup odpovídá vašemu designu.

```csharp
using Aspose.Html.Drawing;          // For ImageRenderingOptions, TextOptions, Font, etc.

// Step 2: Set up image rendering options (antialiasing, text hinting, font)
var imageOptions = new ImageRenderingOptions
{
    UseAntialiasing = true,
    TextOptions = new TextOptions { UseHinting = true },
    Font = new Font("Times New Roman", 14, WebFontStyle.Bold)
};
```

**Proč tato nastavení?** Antialiasing snižuje zubaté pixely, zejména na zakřivených částech. Hinting říká rasterizéru, aby zarovnal glyfy k pixelovým hranám, což je klíčové při **render html to png** při typických rozlišeních obrazovky. Tučný font Times New Roman je jen příklad; můžete jej nahradit libovolným web‑safe nebo vlastním fontem.

## Krok 3: Připojte handler k Image Rendereru

S nastavenými možnostmi a připraveným handlerem vytvoříme `ImageRenderer`. Přiřazením našeho `MyResourceHandler` k vlastnosti `ResourceHandler` zajistíme, že každý externí soubor skončí na disku.

```csharp
using Aspose.Html.Rendering.Image; // For ImageRenderer

// Step 3: Create the image renderer with the options and the custom handler
var renderer = new ImageRenderer(imageOptions)
{
    ResourceHandler = new MyResourceHandler()
};
```

**Pro tip:** Pokud budete potřebovat logovat každý požadavek, přepište `HandleResource` a přidejte `Console.WriteLine(info.Path)` před vrácením streamu. Tento drobný doplněk může ušetřit hodiny při řešení chybějících fontů nebo poškozených obrázků.

## Krok 4: **Render Webpage to Image** a uložte jej

Nakonec řekněte rendereru, kterou URL má zachytit a kam má PNG uložit. Níže uvedené volání provede vše potřebné: načte stránku, zpracuje CSS, načte fonty a zapíše výsledný bitmap.

```csharp
// Step 4: Render a web page to an image file
renderer.RenderPage("https://example.com", "output/page.png");
```

Když metoda skončí, v adresáři `output` najdete dvě věci:

1. `page.png` – snímek stránky (náš výsledek **capture webpage screenshot**)
2. Strukturu podadresářů odrážející zdroje stránky (CSS, obrázky, fonty) – vše uloženo díky našemu **custom resource handler**

### Očekávaný výstup

Spuštěním kompletního programu by se měl vytvořit PNG, který vypadá jako věrná kopie `https://example.com`. Otevřete jej v libovolném prohlížeči obrázků a uvidíte stránku vykreslenou ve výchozí velikosti viewportu (obvykle 1024 × 768 px). Všechny propojené obrázky a styly jsou uloženy vedle, připravené k opětovnému použití.

## Časté otázky a okrajové případy

### Co když cílová stránka používá relativní URL?

Náš handler již odstraňuje úvodní lomítko (`info.Path.TrimStart('/')`) a kombinuje jej s výstupní složkou, takže relativní cesty se řeší správně. Pokud narazíte na URL, která začíná `//` (protokol‑relativní), renderer ji normalizuje před voláním `HandleResource`.

### Jak změním rozměry výstupu?

Předávejte objekt `Size` do přetížení `RenderPage`:

```csharp
renderer.RenderPage("https://example.com", "output/page.png", new Size(1920, 1080));
```

Tímto způsobem můžete **save webpage as png** ve vysokém rozlišení pro tiskové materiály.

### Můžu vykreslit více stránek během jednoho spuštění?

Určitě. Stačí projít seznam URL a každou z nich zavolat `RenderPage`. Stejná instance `MyResourceHandler` bude nadále naplňovat složku `output`, takže vše zůstane přehledné.

### Co s weby chráněnými autentifikací?

Pokud stránka vyžaduje cookies nebo HTTP hlavičky, nakonfigurujte `HttpClient` a přiřaďte jej k vlastnosti `HttpClient` rendereru (pokud to knihovna umožňuje). To zajistí plynulý tok **render html to png** pro interní dashboardy.

## Kompletní funkční příklad

Spojením všeho dohromady získáte minimální konzolovou aplikaci, kterou můžete zkopírovat a vložit do Visual Studia:

```csharp
using System;
using System.IO;
using Aspose.Html.Drawing;
using Aspose.Html.Rendering.Image;

class MyResourceHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info)
    {
        string filePath = Path.Combine("output", info.Path.TrimStart('/'));
        Directory.CreateDirectory(Path.GetDirectoryName(filePath)!);
        return File.OpenWrite(filePath);
    }
}

class Program
{
    static void Main()
    {
        var imageOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            TextOptions = new TextOptions { UseHinting = true },
            Font = new Font("Times New Roman", 14, WebFontStyle.Bold)
        };

        var renderer = new ImageRenderer(imageOptions)
        {
            ResourceHandler = new MyResourceHandler()
        };

        // Render the page and save as PNG
        renderer.RenderPage("https://example.com", "output/page.png");

        Console.WriteLine("Done! Screenshot saved to output/page.png");
    }
}
```

Zkompilujte a spusťte (`dotnet run`), pak zkontrolujte adresář `output`. Právě jste **rendered a webpage to image**, zachytili snímek a uložili HTML jako PNG – vše díky úhlednému **custom resource handler**.

## Závěr

Vytvořili jsme **custom resource handler**, upravili možnosti vykreslování a použili `ImageRenderer` k **render webpage to image**. Výsledkem je ostrý PNG plus kompletní sada zdrojů, která vám poskytne vše potřebné k **capture webpage screenshot**, **render html to png** a **save webpage as png** pro reporty, náhledy nebo automatizované testování.

Co dál? Zkuste experimentovat s:

- Různými velikostmi viewportu pro mobilní vs. desktopové snímky
- Přidáním vodoznaků nebo překryvů po vykreslení
- Exportem do jiných formátů (JPEG, BMP) úpravou `ImageRenderingOptions`

Neváhejte zanechat komentář, pokud narazíte na problém nebo objevíte chytrý trik. Šťastné programování a ať jsou vaše snímky vždy pixel‑dokonalé!

## Související tutoriály

- [Jak uložit HTML v C# – Kompletní průvodce s použitím Custom Resource Handleru](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Vytvořit HTML ze stringu v C# – Průvodce Custom Resource Handlerem](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Jak renderovat HTML jako PNG – Kompletní C# průvodce](/html/english/net/rendering-html-documents/how-to-render-html-as-png-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
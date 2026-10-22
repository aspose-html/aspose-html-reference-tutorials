---
category: general
date: 2026-10-21
description: Naučte se, jak uložit HTML jako ZIP pomocí Aspose.HTML, převést HTML
  na ZIP a odstranit zdroje pro čistý balíček.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save html as zip
- convert html to zip
- how to omit resources
- how to strip resources
- create html zip
language: cs
lastmod: 2026-10-21
og_description: Uložte HTML jako ZIP pomocí Aspose.HTML, naučte se, jak převést HTML
  na ZIP a odstranit zdroje pro lehký archiv.
og_image_alt: Screenshot showing the save html as zip process with resources omitted
og_title: Uložte HTML jako ZIP pomocí Aspose.HTML – vynechejte zdroje v jednom kroku
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to save HTML as ZIP using Aspose.HTML, convert HTML to ZIP,
    and strip resources for a clean package.
  headline: How to save HTML as ZIP with Aspose.HTML and omit resources
  type: TechArticle
tags:
- Aspose.HTML
- C#
- ZIP archive
- HTML conversion
- Resource handling
title: Jak uložit HTML jako ZIP pomocí Aspose.HTML a vynechat zdroje
url: /cs/net/html-extensions-and-conversions/how-to-save-html-as-zip-with-aspose-html-and-omit-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak uložit HTML jako ZIP s Aspose.HTML a vynechat zdroje

Pokud potřebujete **uložit HTML jako ZIP** a zároveň odstranit externí soubory, tento návod ukazuje kompletní, připravené řešení. Na konci tutoriálu budete schopni **převést HTML na ZIP**, řídit, které zdroje jsou zachovány, a vytvořit čistý archiv, který obsahuje pouze základní značky.

Mnoho scénářů web‑automatizace vyžaduje zabalení stránky pro offline použití, e‑mailový příloha nebo archivaci. Vkládání obrázků, fontů nebo skriptů často zbytečně zvětšuje archiv. Níže uvedené kroky vysvětlují **jak vynechat zdroje** a **jak odstranit zdroje** z výstupu, aby výsledný ZIP zůstal lehký.

## Požadavky

- .NET 6.0 nebo novější nainstalovaný  
- Licence Aspose.HTML pro .NET (nebo bezplatná zkušební verze)  
- Základní vývojové prostředí C# (Visual Studio, VS Code nebo Rider)  

Kromě `Aspose.Html` nejsou vyžadovány žádné další balíčky NuGet.

## Krok 1: Vytvořte vlastní manipulátor zdrojů

Jádro **jak vynechat zdroje** spočívá v podtřídě `ResourceHandler`. Aspose.HTML volá tento manipulátor pro každý externí asset (obrázky, CSS, skripty). Vrácením prázdného streamu efektivně řeknete konvertoru, aby asset přeskočil.

```csharp
using System.IO;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Prevents external resources from being written to the output package.
/// </summary>
class CustomResourceHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info)
    {
        // Returning an empty MemoryStream strips the resource from the ZIP.
        return new MemoryStream();
    }
}
```

**Proč je to důležité:** Výchozí chování kopíruje každý odkazovaný soubor do ZIP, což může zdvojnásobit nebo ztrojnásobit velikost souboru. Přepsáním `HandleResource` získáte jemnou kontrolu bez úpravy původního HTML.

## Krok 2: Načtěte HTML dokument

Načtěte zdrojový soubor pomocí `HTMLDocument`. Konstruktor přijímá cestu k souboru, URL nebo stream. V tomto příkladu čteme lokální soubor s názvem `input.html`.

```csharp
// Load the source HTML file from the local file system.
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

Pokud je vaše HTML v paměti nebo pochází z webového požadavku, můžete místo toho předat `MemoryStream` nebo řetězec URL. API funguje stejným způsobem.

## Krok 3: Nakonfigurujte možnosti uložení

Vytvořte instanci `HtmlSaveOptions` a přiřaďte vlastní manipulátor vytvořený v Kroku 1. Tím řeknete Aspose.HTML, aby použil tento manipulátor při každém výskytu zdroje.

```csharp
// Prepare save options and attach the custom resource handler.
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // The ResourceHandler property is what enables resource stripping.
    ResourceHandler = new CustomResourceHandler()
};
```

Můžete zde také upravit další možnosti, například `CompressImages = false`, pokud chcete zachovat data obrázků, ale stále vynechat jiné assety. Příklad zachovává výchozí nastavení komprese.

## Krok 4: Uložte dokument jako ZIP archiv

Nakonec zavolejte `Save` s cílovou cestou a nakonfigurovanými možnostmi. Výstupní soubor bude `.zip`, který obsahuje `index.html` (nebo původní název souboru) a **žádné externí zdroje**.

```csharp
// Save the HTML document as a ZIP file. The archive will contain only the HTML markup.
document.Save("YOUR_DIRECTORY/output.zip", saveOptions);
```

### Očekávaný výsledek

- `output.zip` → obsahuje jediný soubor `index.html`.  
- Všechny obrázky, CSS soubory a odkazy na JavaScript jsou vynechány, protože vlastní manipulátor vrátil pro každý prázdný stream.

Archiv můžete ověřit otevřením v libovolném prohlížeči ZIP. HTML stránka bude stále odkazovat na původní URL, ale tyto soubory v archivu nebudou přítomny, což udržuje balíček minimálním.

## Kompletní, spustitelný příklad

Níže je kompletní program, který můžete zkopírovat, vložit a spustit. Nahraďte `YOUR_DIRECTORY` skutečnou cestou ke složce na vašem počítači.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Converters;

class Program
{
    static void Main()
    {
        // Step 1: Define a custom resource handler to control how external resources are saved.
        class CustomResourceHandler : ResourceHandler
        {
            public override Stream HandleResource(ResourceInfo info)
            {
                // Returning an empty stream strips the resource from the ZIP output.
                return new MemoryStream();
            }
        }

        // Step 2: Load an HTML document from a file.
        string inputPath = "YOUR_DIRECTORY/input.html";
        HTMLDocument document = new HTMLDocument(inputPath);

        // Step 3: Create HTML save options and assign the custom handler.
        HtmlSaveOptions saveOptions = new HtmlSaveOptions
        {
            ResourceHandler = new CustomResourceHandler()
        };

        // Step 4: Save the document as a ZIP archive containing the HTML and (now omitted) resources.
        string outputPath = "YOUR_DIRECTORY/output.zip";
        document.Save(outputPath, saveOptions);

        Console.WriteLine($"HTML has been saved as ZIP at: {outputPath}");
    }
}
```

Spuštěním tohoto programu se vytvoří ZIP soubor popsaný výše. Nyní můžete distribuovat HTML stránku bez balení zbytečných assetů.

## Běžné varianty a okrajové případy

| Scénář | Úprava |
|----------|------------|
| **Ponechat obrázky, ale odstranit CSS/JS** | V `CustomResourceHandler` zkontrolujte `info.MimeType`. Vraťte `MemoryStream` pouze pro `text/css` a `application/javascript`. |
| **Zachovat externí fonty** | Vraťte původní stream pro MIME typy `font/woff2`, jinak vraťte prázdný stream. |
| **Vytvořit ZIP s vlastním názvem položky** | Použijte přetížení `HtmlSaveOptions` `Save(string path, SaveOptions options, string entryName)`, abyste určili jiný kořenový název souboru. |
| **Převést více HTML souborů do jednoho ZIP** | Procházejte každý soubor, vytvořte samostatný `HTMLDocument` a přidejte jej do stejného `ZipArchive` ručně pomocí `System.IO.Compression`. |

Tyto varianty ilustrují **jak selektivně odstranit zdroje**, což vám dává plnou kontrolu nad konečnou velikostí archivu.

## Profesionální tipy

- **Ověřte výsledek**: Po uložení otevřete ZIP a načtěte `index.html` v prohlížeči. Chybějící zdroje se zobrazí jako nefunkční odkazy, což potvrzuje, že manipulátor fungoval.  
- **Výkon**: Vrácení prázdného `MemoryStream` je levné, ale pokud máte tisíce assetů, zvažte cachování rozhodnutí (např. `HashSet<string>` MIME typů k vynechání).  
- **Licencování**: Bezplatná zkušební verze Aspose.HTML přidává vodotiskový komentář do HTML. Nasazení licencované verze jej odstraní pro produkční použití.  

## Závěr

Nyní víte, jak **uložit HTML jako ZIP**, **převést HTML na ZIP** a **odstranit zdroje** pomocí Aspose.HTML pro .NET. Implementací vlastního `ResourceHandler` můžete vynechat nechtěné soubory a udržet archiv lehký. Experimentujte s logikou manipulátoru, abyste zachovali jen zdroje, které skutečně potřebujete, a začleňte tento vzor do větších automatizačních pipeline.

---

**Další kroky**

- Prozkoumejte další funkce `HtmlSaveOptions`, například `EmbedImages`, které vloží obrázky přímo do HTML.  
- Kombinujte tento přístup s `Aspose.PDF` pro převod stejného HTML do PDF po vytvoření ZIP.  
- Podívejte se na scénáře na straně serveru, kde generujete ZIP na vyžádání a streamujete jej klientovi bez zápisu na disk.  

Příjemné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, která vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy ve vašich projektech.

- [Jak použít ZipArchive – Uložit HTML a zdroje do ZIP souboru](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [Jak uložit HTML v C# – Vlastní manipulátory zdrojů a ZIP](/html/english/net/working-with-html-documents/how-to-save-html-in-c-custom-resource-handlers-zip/)
- [Jak uložit HTML jako ZIP v C# – Kompletní průvodce Aspose.HTML](/html/english/net/html-extensions-and-conversions/how-to-save-html-as-zip-in-c-complete-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
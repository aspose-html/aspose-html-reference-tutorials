---
category: general
date: 2026-02-13
description: Naučte se, jak v C# vytvořit vlastní manipulátor zdrojů pro převod HTML
  do ZIP archivu, vytváření ZIPu v paměti pomocí Aspose.HTML – krok za krokem průvodce.
draft: false
keywords:
- custom resource handler
- convert html zip archive
- create zip from memory
- Aspose HTML
- in‑memory streaming
- C# zip compression
language: cs
og_description: Objevte kompletní řešení v C# pro použití vlastního manipulátoru zdrojů
  k převodu HTML do ZIP archivu přímo v paměti.
og_title: Vlastní obsluha zdrojů – převod HTML do ZIP z paměti
tags:
- C#
- Aspose.HTML
- ZipArchive
- MemoryStream
title: Vlastní manipulátor zdrojů v C# – Převod HTML do ZIP archivu z paměti
url: /cs/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-archive-fro/
---

Storage", "document.Save", etc. Keep them.

Now craft final markdown.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vlastní manipulátor zdrojů – Převod HTML do ZIP archivu z paměti

Už jste někdy potřebovali **custom resource handler**, který zachytí každý obrázek, CSS soubor nebo skript, který HTML stránka načítá, a pak vše zabalí do ZIPu, aniž byste se dotkli disku? Nejste v tom sami. V mnoha scénářích web‑automatizace nebo šablonování e‑mailů chcete celou stránku zabalit do jediného přenosného balíčku a raději vše uchováte v RAM pro rychlost a bezpečnost.

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který vám ukáže, jak **convert HTML zip archive** pomocí **custom resource handler** a poté **create zip from memory** s .NET `System.IO.Compression`. Na konci budete mít samostatnou metodu, kterou můžete vložit do libovolného C# projektu používajícího Aspose.HTML.

## Co budete potřebovat

- .NET 6+ (or .NET Framework 4.7.2+)  
- Aspose.HTML for .NET (NuGet package `Aspose.HTML`)  
- Základní znalost streamů a třídy `ZipArchive`  

Žádné externí nástroje, žádné dočasné soubory, jen čisté zpracování v paměti.

## Krok 1: Definujte vlastní manipulátor zdrojů

Jádrem řešení je třída, která dědí z `Aspose.Html.ResourceHandler`. Její úkolem je poskytnout čerstvý `Stream` pro každý externí zdroj, který HTML engine požaduje. Vrácením nového `MemoryStream` pokaždé udržujeme data oddělená a připravená k pozdějšímu zabalení.

```csharp
using System.IO;
using Aspose.Html;

// Step 1 – Custom handler that stores resources in memory
class MemoryResourceHandler : ResourceHandler
{
    // The framework calls this method for every external resource (images, CSS, etc.)
    public override Stream HandleResource(Resource resource)
    {
        // We give the engine an empty stream; later we’ll fill it with the actual bytes.
        // Using MemoryStream means everything stays in RAM.
        return new MemoryStream();
    }
}
```

**Proč je to důležité:**  
Pokud necháte Aspose.HTML zapisovat zdroje na disk, budete muset později uklízet. Manipulátor v paměti eliminuje I/O režii a činí kód bezpečným pro sandboxované prostředí (např. Azure Functions).

## Krok 2: Načtěte svůj HTML dokument

Dále nasměrujte Aspose.HTML na HTML soubor, který chcete zabalit. Dokument může být na disku, URL nebo i surový řetězec. Zde použijeme cestu k souboru pro jednoduchost.

```csharp
using Aspose.Html;

// Step 2 – Load the source HTML
HtmlDocument document = new HtmlDocument("YOUR_DIRECTORY/input.html");
```

> **Tip:** Pokud váš HTML odkazuje na relativní zdroje, ujistěte se, že `input.html` se nachází ve stejné složce jako tyto soubory, jinak je handler nebude schopen najít.

## Krok 3: Připojte handler a uložte do MemoryStream

Nyní vytvoříme instanci handleru a řekneme Aspose.HTML, aby jej použil přes `HtmlSaveOptions.OutputStorage`. Výsledné HTML (včetně přepsaných URL zdrojů) skončí v `MemoryStream`.

```csharp
using Aspose.Html.Saving;
using System.IO;

// Step 3 – Prepare the handler and an in‑memory buffer for the final HTML
var resourceHandler = new MemoryResourceHandler();

using (MemoryStream htmlMemoryStream = new MemoryStream())
{
    document.Save(htmlMemoryStream, new HtmlSaveOptions
    {
        OutputStorage = resourceHandler // redirects all resources to the handler
    });

    // At this point htmlMemoryStream contains the full HTML file,
    // while each external resource resides in the streams returned by the handler.
```

**Co se děje pod kapotou?**  
Když se spustí `document.Save`, Aspose.HTML požádá `MemoryResourceHandler` o stream pro každý zdroj. Protože jsme vrátili prázdné `MemoryStream`y, engine zapisuje surová data přímo do paměti. Žádné dočasné soubory nejsou vytvořeny.

## Krok 4: Sestavte ZIP archiv kompletně v paměti

Nyní přichází zábavná část: vytvoříme `ZipArchive`, který žije uvnitř dalšího `MemoryStream`. To nám umožní **create zip from memory** aniž bychom se kdy dotkli souborového systému.

```csharp
    // Step 4 – Build the ZIP archive in memory
    using (MemoryStream zipMemoryStream = new MemoryStream())
    using (var zipArchive = new ZipArchive(zipMemoryStream, ZipArchiveMode.Create, leaveOpen: true))
    {
        // 4a – Add the main HTML file
        var htmlEntry = zipArchive.CreateEntry("index.html");
        using (var entryStream = htmlEntry.Open())
        {
            // Reset the position of the HTML stream before copying
            htmlMemoryStream.Position = 0;
            htmlMemoryStream.CopyTo(entryStream);
        }

        // 4b – Add each resource that the handler captured
        // The handler stored each resource in a fresh MemoryStream, which we can enumerate.
        // For demonstration, assume we kept a list of those streams (you could store them in a dictionary).
        // Example placeholder – replace with your actual collection:
        // foreach (var kvp in capturedResources)
        // {
        //     var resourceEntry = zipArchive.CreateEntry(kvp.Key); // kvp.Key = relative path
        //     using var entry = resourceEntry.Open();
        //     kvp.Value.Position = 0;
        //     kvp.Value.CopyTo(entry);
        // }

        // When we’re done, flush everything
        zipArchive.Dispose(); // optional because of using, but makes intent clear
    }

    // At this stage zipMemoryStream holds the complete ZIP file.
    // You can return it, write it to a response stream, or save it to disk if you wish.
}
```

> **Poznámka:** Zakomentovaná část ukazuje, jak můžete shromažďovat streamy uvnitř `MemoryResourceHandler`. V produkčním scénáři byste uložili každý `MemoryStream` do slovníku klíčovaného původní URL zdroje a pak zde iterovali pro přidání do archivu.

**Proč uchovávat ZIP v paměti?**  
Uložení archivu v `MemoryStream` usnadní jeho přímé odeslání HTTP klientovi (`FileResult` v ASP.NET Core) nebo nahrání do cloudového úložiště bez mezilehlého souboru.

## Krok 5: (Volitelné) Uložte ZIP na disk

Pokud stále potřebujete fyzický soubor – třeba pro ladění – stačí zapsat `zipMemoryStream` na disk:

```csharp
// Optional: write the in‑memory ZIP to a file for inspection
File.WriteAllBytes("YOUR_DIRECTORY/output.zip", zipMemoryStream.ToArray());
```

## Kompletní funkční příklad

Spojením všeho dohromady zde máte jednorázový, připravený k zkopírování program, který **converts HTML to a ZIP archive** kompletně v paměti.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class MemoryResourceHandler : ResourceHandler
{
    // Capture each resource in a dictionary for later retrieval
    public static readonly System.Collections.Generic.Dictionary<string, MemoryStream> Captured = new();

    public override Stream HandleResource(Resource resource)
    {
        var ms = new MemoryStream();
        // Store the stream using the resource's absolute URL as the key
        Captured[resource.Uri.AbsoluteUri] = ms;
        return ms;
    }
}

class Program
{
    static void Main()
    {
        // Load the HTML file
        HtmlDocument doc = new HtmlDocument("YOUR_DIRECTORY/input.html");

        // Attach the custom handler
        var handler = new MemoryResourceHandler();

        // Save HTML + resources to memory
        using var htmlStream = new MemoryStream();
        doc.Save(htmlStream, new HtmlSaveOptions { OutputStorage = handler });

        // Create the ZIP archive in memory
        using var zipStream = new MemoryStream();
        using (var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, true))
        {
            // Add the HTML file
            var htmlEntry = zip.CreateEntry("index.html");
            using (var entry = htmlEntry.Open())
            {
                htmlStream.Position = 0;
                htmlStream.CopyTo(entry);
            }

            // Add each captured resource
            foreach (var kvp in MemoryResourceHandler.Captured)
            {
                // Derive a sane relative path from the URL
                var uri = new Uri(kvp.Key);
                var relativePath = uri.AbsolutePath.TrimStart('/');
                var resEntry = zip.CreateEntry(relativePath);
                using var entry = resEntry.Open();
                kvp.Value.Position = 0;
                kvp.Value.CopyTo(entry);
            }
        }

        // The ZIP is ready – write it out or return it from a web API
        File.WriteAllBytes("YOUR_DIRECTORY/output.zip", zipStream.ToArray());

        Console.WriteLine("HTML successfully packaged into output.zip");
    }
}
```

### Očekávaný výsledek

Spuštěním programu se vytvoří `output.zip` obsahující:

- `index.html` – přepsané HTML, které odkazuje na zabalené zdroje.  
- Všechny obrázky, CSS a JavaScript soubory, na které původní stránka odkazovala, uloženy s jejich původními relativními cestami.

Otevřete `index.html` z ZIPu v libovolném prohlížeči a uvidíte, že stránka se vykreslí přesně tak, jako když byla na souborovém systému.

## Často kladené otázky a okrajové případy

| Otázka | Odpověď |
|----------|--------|
| **Co když je zdroj obrovský (např. video)?** | Protože vše žije v paměti, velmi velké soubory mohou způsobit `OutOfMemoryException`. V takovém případě streamujte přímo do dočasného souboru nebo omezte velikost, kterou akceptujete. |
| **Musím řešit duplicitní URL zdrojů?** | Slovník v handleru přepíše duplikáty. Pokud chcete zachovat jen jednu kopii, zkontrolujte `Captured.ContainsKey` před přidáním. |
| **Mohu to použít v ASP.NET Core controlleru?** | Určitě. Vraťte `File(zipStream.ToArray(), "application/zip", "page.zip")` z akční metody. |
| **Co s HTTPS zdroji?** | Aspose.HTML je stáhne automaticky, pokud runtime důvěřuje SSL certifikátu. Pro samopodepsané certifikáty nastavte `ServicePointManager.ServerCertificateValidationCallback`. |
| **Je vlastní handler thread‑safe?** | Příklad používá statický slovník, který *není* thread‑safe. Zabalte přístupy do zámku nebo použijte `ConcurrentDictionary`, pokud plánujete zpracovávat mnoho dokumentů současně. |

## Pro tipy pro produkční použití

- **Znovu použijte handler** pouze pro jeden dokument; vytvořte novou instanci pro každou žádost, aby nedocházelo k prolínání mezi uživateli.  
- **Okamžitě uvolňujte streamy**. I když `using` bloky řeší většinu případů, streamy uložené ve slovníku by měly být uvolněny po vytvoření ZIPu.  
- **Validujte HTML** před zpracováním, aby se zachytily špatně formátované značky, které by mohly způsobit, že handler požaduje neočekávané zdroje.  
- **Komprimujte agresivně** nastavením `ZipArchiveEntry.CompressionLevel = CompressionLevel.Optimal`, pokud záleží na velikosti souboru.  

## Závěr

Probrali jsme vše, co potřebujete k **custom resource handler** průchodu HTML stránkou, zachycení každého propojeného assetu a **create zip from memory** bez jakéhokoli doteku disku. Tento vzor je dostatečně flexibilní pro scénáře web‑servisů, background úloh nebo dokonce desktopových utilit, které potřebují distribuovat samostatný HTML balíček.

Vyzkoušejte to – zaměňte `YOUR_DIRECTORY/input.html` za libovolnou stránku, upravte handler tak, aby ukládal zdroje do `ConcurrentDictionary`, a budete mít robustní, v‑paměti HTML‑to‑ZIP pipeline připravenou pro produkci.

---

*Připravený posunout se dál?* Dále prozkoumejte, jak **convert HTML to PDF** pomocí Aspose.HTML, nebo experimentujte s šifrováním ZIP pro zvýšenou bezpečnost. Možnosti jsou neomezené, když ovládáte streaming v paměti v C#. Šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
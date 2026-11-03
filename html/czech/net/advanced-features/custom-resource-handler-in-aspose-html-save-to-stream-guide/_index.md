---
category: general
date: 2026-02-22
description: Vlastní handler zdrojů vám umožňuje zachytit výstup HTML. Naučte se,
  jak načíst HTML dokument, použít Aspose HTML save a uložit HTML do streamu pomocí
  jednoduchého příkladu v C#.
draft: false
keywords:
- custom resource handler
- load html document
- aspose html save
- save html to stream
- capture html output
language: cs
og_description: Zjistěte, jak vlastní obsluha zdrojů zachytává výstup HTML, načítá
  HTML dokument a ukládá HTML do proudu pomocí Aspose HTML v C#.
og_title: Vlastní manipulátor zdrojů v Aspose HTML – Průvodce ukládáním do proudu
tags:
- aspose-html
- csharp
- streaming
- resource-handler
title: Vlastní obsluha zdrojů v Aspose HTML – Průvodce ukládáním do proudu
url: /cs/net/advanced-features/custom-resource-handler-in-aspose-html-save-to-stream-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vlastní obsluha zdrojů – Zachycení výstupu HTML pomocí Aspose HTML

Už jste někdy potřebovali **custom resource handler**, který zachytí každý soubor, který Aspose HTML během konverze zapíše? Možná jste chtěli přenést HTML, obrázky nebo CSS přímo do paměti místo na disk. To je velmi častý scénář, když budujete webovou službu, která musí zůstat beze stavu, nebo když jednoduše chcete **save HTML to stream** pro pozdější zpracování.

V tomto tutoriálu projdeme kompletním, připraveným příkladem, který ukazuje, jak **load HTML document**, připojit **custom resource handler** a použít **Aspose HTML save** k zachycení každého výstupního kusu v `MemoryStream`. Na konci pochopíte nejen „co“, ale i „proč“ za každým řádkem a získáte znovupoužitelný vzor, který můžete vložit do libovolného projektu C#.

> **Proč na tom záleží?**  
> Zachycení výstupu HTML v paměti vám umožní vyhnout se I/O souborového systému, snižuje latenci ve cloudových funkcích a dává vám plnou kontrolu nad pojmenováním, kompresí nebo dokonce transformacemi za běhu.

## Co budete potřebovat

- **.NET 6** nebo novější (kód také funguje na .NET Framework 4.7+).  
- **Aspose.HTML for .NET** NuGet balíček (`Aspose.Html`).  
- Jednoduchý HTML soubor (`input.html`) umístěný ve složce, na kterou můžete odkazovat.  
- Jakékoli IDE, které chcete—Visual Studio, Rider nebo VS Code s rozšířeními C#.

Žádná další konfigurace není vyžadována; API udělá veškerou těžkou práci.

## Krok 1 – Vytvořte vlastní obsluhu zdrojů

Jádrem této techniky je podtřída `Aspose.Html.Rendering.ResourceHandler`. Přepsáním `HandleResource` určíte **kde** každý stream zdroje půjde. V našem případě vracíme nový `MemoryStream` pro každý požadavek, což znamená, že každý CSS, obrázek nebo pod‑HTML fragment existuje pouze v RAM.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;

/// <summary>
/// Custom handler that writes every resource to a new MemoryStream.
/// </summary>
class MemoryStreamHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // The ResourceInfo gives you the original URL and MIME type.
        // You could inspect it here to decide whether to skip certain files.
        // For this tutorial we just allocate a fresh stream.
        return new MemoryStream();
    }
}
```

**Pro tip:** Pokud potřebujete sledovat streamy (např. pro pozdější zápis do ZIP archivu), uložte je do `Dictionary<string, MemoryStream>` indexovaného pomocí `resourceInfo.Uri`.

## Krok 2 – Načtěte HTML dokument

Než můžete něco uložit, musíte **load HTML document** do instance `HTMLDocument`. Aspose HTML může číst z cesty k souboru, URL nebo dokonce ze řetězce. Zde používáme lokální soubor pro jednoduchost.

```csharp
// Adjust the path to point at your real HTML file.
string htmlPath = Path.Combine(Environment.CurrentDirectory, "input.html");

// Load the source HTML document.
HTMLDocument htmlDocument = new HTMLDocument(htmlPath);
```

Pokud váš HTML odkazuje na externí zdroje (obrázky, fonty atd.), ujistěte se, že základní URI je správné; jinak obsluha nebude schopna je najít.

## Krok 3 – Vytvořte instanci vlastní obsluhy

Nyní vytvoříme instanci obsluhy, kterou jsme definovali dříve. Nic zvláštního—jen obyčejné `new`. Tento objekt bude předán metodě `Save` v dalším kroku.

```csharp
// Step 3: Instantiate the custom handler.
MemoryStreamHandler resourceHandler = new MemoryStreamHandler();
```

Protože obsluha existuje pouze v paměti, nemusíte se starat o oprávnění k souborům nebo úklid na disku.

## Krok 4 – Uložte dokument pomocí Aspose HTML Save

Operace **Aspose HTML save** přijímá `ResourceHandler`. Jak motor prochází DOM a řeší každý propojený zdroj, volá `HandleResource`. Naše implementace vrací `MemoryStream`, takže každý kus končí v RAM.

```csharp
// Step 4: Save the document.
// The handler's HandleResource method will be invoked for each output stream.
htmlDocument.Save(resourceHandler);
```

V tomto okamžiku je konverze dokončena, ale streamy jsou stále v paměti. Nyní je můžete číst, zapsat do databáze nebo vrátit v odpovědi API.

## Krok 5 – Získejte a ověřte zachycené streamy

Protože jsme při každém volání vrátili nový `MemoryStream`, potřebujeme způsob, jak uchovat reference. Níže je rychlé rozšíření předchozí obsluhy, které ukládá každý stream do slovníku, abyste je mohli po uložení prozkoumat.

```csharp
class TrackingMemoryStreamHandler : ResourceHandler
{
    public Dictionary<string, MemoryStream> Streams { get; } = new();

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var ms = new MemoryStream();
        Streams[resourceInfo.Uri] = ms;   // Remember the stream by its URI.
        return ms;
    }
}

// Usage:
var trackingHandler = new TrackingMemoryStreamHandler();
htmlDocument.Save(trackingHandler);

// Example: write the main HTML output to console (as text)
if (trackingHandler.Streams.TryGetValue(htmlPath, out var mainStream))
{
    mainStream.Position = 0; // rewind
    using var reader = new StreamReader(mainStream);
    string html = reader.ReadToEnd();
    Console.WriteLine("=== Rendered HTML ===");
    Console.WriteLine(html);
}
```

Spuštěním tohoto kódu se vytiskne finální HTML, které Aspose vygenerovalo, což potvrzuje, že **capture html output** funguje podle očekávání.

## Okrajové případy a časté otázky

### 1. Co když je dokument obrovský?

Spotřeba paměti může rychle růst. Pro velké PDF nebo HTML s mnoha vysoce rozlišenými obrázky zvažte streamování přímo do `FileStream` nebo **buffered network stream** místo `MemoryStream`. Obsluha může rozhodnout na základě `resourceInfo.MimeType`.

### 2. Musím streamy uvolnit (dispose)?

Ano. Po dokončení zpracování zavolejte `Dispose()` na každém `MemoryStream` (nebo nechte, aby to udělal `using` blok). V příkladu se sledováním bychom mohli přidat:

```csharp
foreach (var ms in trackingHandler.Streams.Values)
    ms.Dispose();
```

### 3. Můžu před uložením přejmenovat zdroje?

Určitě. V `HandleResource` máte přístup k `resourceInfo.Uri`. Můžete jej přepsat, přidat prefix nebo dokonce některé soubory přeskočit tím, že vrátíte `null`.

```csharp
if (resourceInfo.MimeType.StartsWith("image/"))
    return null; // Skip images completely.
```

### 4. Je tento přístup thread‑safe?

Jedna instance obsluhy by **neměla** být sdílena mezi souběžnými voláními `Save`. Vytvořte novou obsluhu pro každou konverzi, nebo pokud ji musíte znovu použít, chraňte interní slovník zámkem.

## Kompletní funkční příklad

Níže je kompletní program, který můžete vložit do konzolové aplikace. Ukazuje vše—od načtení HTML souboru po vytištění zachyceného výstupu.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering;

class TrackingMemoryStreamHandler : ResourceHandler
{
    public Dictionary<string, MemoryStream> Streams { get; } = new();

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var ms = new MemoryStream();
        Streams[resourceInfo.Uri] = ms;
        return ms;
    }
}

class SaveToStreamTutorial
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the HTML document you want to render.
        // -------------------------------------------------
        string htmlPath = Path.Combine(Environment.CurrentDirectory, "input.html");
        if (!File.Exists(htmlPath))
        {
            Console.WriteLine($"Cannot find {htmlPath}");
            return;
        }

        HTMLDocument htmlDocument = new HTMLDocument(htmlPath);

        // -------------------------------------------------
        // Step 2: Create the custom handler that captures streams.
        // -------------------------------------------------
        var handler = new TrackingMemoryStreamHandler();

        // -------------------------------------------------
        // Step 3: Save the document – Aspose will invoke our handler.
        // -------------------------------------------------
        htmlDocument.Save(handler);

        // -------------------------------------------------
        // Step 4: Retrieve the main HTML output and display it.
        // -------------------------------------------------
        if (handler.Streams.TryGetValue(htmlPath, out var mainStream))
        {
            mainStream.Position = 0; // rewind to start
            using var reader = new StreamReader(mainStream);
            string renderedHtml = reader.ReadToEnd();
            Console.WriteLine("=== Rendered HTML Output ===");
            Console.WriteLine(renderedHtml);
        }
        else
        {
            Console.WriteLine("Main HTML stream not found.");
        }

        // -------------------------------------------------
        // Step 5: Clean up.
        // -------------------------------------------------
        foreach (var ms in handler.Streams.Values)
            ms.Dispose();

        Console.WriteLine("All streams disposed. Done.");
    }
}
```

**Očekávaný výstup:** Konzole vytiskne plně vykreslené HTML (včetně jakéhokoli inline CSS, které Aspose mohl vygenerovat) a poté potvrzení, že všechny streamy byly uvolněny.

## Závěr

Právě jste se naučili, jak implementovat **custom resource handler** v Aspose HTML, **load an HTML document** a **save HTML to stream**, přičemž **capturing the HTML output** pro další zpracování. Tento vzor je lehký, thread‑aware a plně rozšiřitelný—můžete vyměnit `MemoryStream` za soubor, síťový socket nebo cloudové úložiště API pomocí několika řádků kódu.

Dále můžete zkusit:

- **Saving to a ZIP archive** (perfektní pro balení HTML, CSS a obrázků).  
- **Applying transformations** (např. minifikace CSS za běhu).  
- **Streaming directly to an HTTP response** v ASP.NET Core pro okamžité stažení.

Vyzkoušejte je a uvidíte, jak mocný může být přizpůsobený **custom resource handler** v reálných scénářích. Šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
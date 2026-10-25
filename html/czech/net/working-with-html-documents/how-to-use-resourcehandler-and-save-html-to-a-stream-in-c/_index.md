---
category: general
date: 2026-10-25
description: Jak použít ResourceHandler k řízení načítání zdrojů a jak uložit HTML
  do proudu pomocí Aspose.HTML v C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use resourcehandler
- how to save html to stream
- Aspose.HTML ResourceHandler
- HTML to MemoryStream C#
- custom resource handling C#
language: cs
lastmod: 2026-10-25
og_description: Jak použít ResourceHandler k řízení načítání zdrojů a jak uložit HTML
  do proudu pomocí Aspose.HTML pro .NET.
og_image_alt: Screenshot of C# code using ResourceHandler to save HTML to a memory
  stream
og_title: Jak použít ResourceHandler a uložit HTML do proudu v C#
schemas:
- author: Aspose
  dateModified: '2026-10-25'
  description: How to use ResourceHandler to control resource loading and how to save
    HTML to a stream using Aspose.HTML in C#.
  headline: How to use ResourceHandler and save HTML to a stream in C#
  type: TechArticle
- description: How to use ResourceHandler to control resource loading and how to save
    HTML to a stream using Aspose.HTML in C#.
  name: How to use ResourceHandler and save HTML to a stream in C#
  steps:
  - name: Expected output
    text: 'Running the code above prints:'
  - name: 1. Embedding real resources
    text: 'If you need to embed an image, modify `MyHandler` to return a stream that
      contains the image bytes:'
  - name: 2. Handling large documents
    text: For very large HTML files, consider using `BufferedStream` or writing directly
      to a file‑based `FileStream` if memory becomes a bottleneck. The pattern for
      **how to save HTML to a stream** stays the same; only the stream type changes.
  - name: 3. Thread safety
    text: '`ResourceHandler` instances are **not** guaranteed to be thread‑safe. If
      you plan to reuse a handler across parallel conversions, either:'
  - name: 4. Disposing resources
    text: Both `HTMLDocument` and any streams you create implement `IDisposable`.
      Wrapping them in `using` blocks, as shown in Step 4, guarantees clean release
      of unmanaged resources.
  - name: What’s next?
    text: '* **Embed real images or CSS** by extending `MyHandler` (see the “Embedding
      real resources” section). * **Convert the stream to PDF** with `HtmlConverter.ConvertHtml`
      if you need a printable version. * **Stream the result directly from a Web API**
      using `FileStreamResult` or `MemoryStream` in ASP.NE'
  type: HowTo
tags:
- Aspose.HTML
- C#
- Stream handling
title: Jak použít ResourceHandler a uložit HTML do proudu v C#
url: /cs/net/working-with-html-documents/how-to-use-resourcehandler-and-save-html-to-a-stream-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak použít ResourceHandler a uložit HTML do streamu v C#

Pokud potřebujete **jak použít ResourceHandler** při renderování HTML pomocí Aspose.HTML, tento průvodce vám ukáže kompletní, připravené řešení. Také se naučíte **jak uložit HTML do streamu**, abyste mohli výstup přenést bez zásahu do souborového systému.

Práce s HTML v paměti je běžná, když generujete e‑maily, API odpovědi nebo PDF za běhu. Na konci tohoto tutoriálu budete mít samostatný C# program, který vytvoří `HTMLDocument`, poskytne vlastní `ResourceHandler` a zapíše výsledek do `MemoryStream`.

## Požadavky

* .NET 6.0 nebo novější (kód také funguje s .NET Core 3.1 a .NET Framework 4.7+)
* Balíček **Aspose.HTML for .NET** NuGet  
  ```bash
  dotnet add package Aspose.HTML
  ```
* Základní pochopení C# async/await (volitelné, ale užitečné)

## Co tutoriál pokrývá

* Jak **jak použít ResourceHandler** k zachycení požadavků na obrázky, CSS nebo skripty
* Jak nakonfigurovat `HtmlSaveOptions` s vlastním handlerem
* Jak **jak uložit HTML do streamu** pomocí `MemoryStream`
* Řešení okrajových případů, jako jsou chybějící zdroje a uvolnění streamu
* Tipy pro rozšíření handleru k vložení skutečných zdrojů později

## Krok 1: Vytvořit jednoduchý HTML dokument ze řetězce

Prvním krokem je vytvořit instanci `HTMLDocument` z neformátovaného HTML. Tento objekt představuje strom DOM, který Aspose.HTML vykreslí.

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using System.IO;

// Simple HTML markup – you can replace this with any valid HTML string.
string htmlContent = "<html><body>Hello World</body></html>";

// The HTMLDocument constructor parses the string into a DOM.
HTMLDocument document = new HTMLDocument(htmlContent);
```

> **Proč je to důležité:** Vytvoření dokumentu ze řetězce udržuje celý workflow v paměti, což je nezbytné, když později **jak uložit HTML do streamu** bez zásahu na disk.

## Krok 2: Implementovat vlastní ResourceHandler

`ResourceHandler` je háček, který Aspose.HTML používá, kdykoli potřebuje externí zdroj (obrázky, CSS, fonty atd.). Přepsáním `HandleResource` určíte, jaký stream se vrátí pro každý požadavek.

```csharp
// Define a handler that supplies an empty stream for every resource request.
class MyHandler : ResourceHandler
{
    public override Stream HandleResource(Resource resource)
    {
        // Returning an empty MemoryStream effectively disables external resources.
        // You could return a real image stream here if you need to embed assets.
        return new MemoryStream();
    }
}

// Instantiate the handler so it can be attached to the save options.
MyHandler customHandler = new MyHandler();
```

> **Proč byste to mohli potřebovat:** Při generování HTML pro e‑mail nebo API odpovědi často nechcete externí volání. Poskytnutí prázdných streamů zabraňuje chybám 404 a zrychluje renderování. Toto ukazuje **jak použít ResourceHandler** pro výstup „bez zdrojů“.

## Krok 3: Nakonfigurovat HtmlSaveOptions pro použití vlastního handleru

`HtmlSaveOptions` vám umožňuje řídit proces ukládání. Přiřaďte vlastnost `ResourceHandler` k vaší vlastní implementaci.

```csharp
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // Attach the handler so every resource request goes through MyHandler.
    ResourceHandler = customHandler
};
```

> **Tip:** Pokud později potřebujete vložit CSS nebo obrázky, nahraďte `MyHandler` verzí, která vrací odpovídající streamy na základě `resource.Uri`.

## Krok 4: Uložit dokument do MemoryStream

Nyní máte vše připravené k **jak uložit HTML do streamu**. Použití `MemoryStream` udržuje výstup v RAM, což usnadňuje odeslání přes HTTP, uložení do databáze nebo předání jiné API.

```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    // The Save method writes the HTML (and any referenced resources) into the stream.
    document.Save(outputStream, saveOptions);

    // Reset the position so callers can read from the beginning.
    outputStream.Position = 0;

    // Example: Convert the stream to a string for debugging.
    using (StreamReader reader = new StreamReader(outputStream))
    {
        string resultHtml = reader.ReadToEnd();
        System.Console.WriteLine(resultHtml);
    }

    // At this point, outputStream can be returned from a web API, attached to an email,
    // or passed to another component without ever touching the file system.
}
```

### Očekávaný výstup

Running the code above prints:

```html
<html><head></head><body>Hello World</body></html>
```

Protože vlastní handler vrací prázdné streamy, žádné externí `<link>` ani `<img>` tagy nejsou vyřešeny a HTML zůstává čisté.

## Běžné varianty a okrajové případy

### 1. Vkládání skutečných zdrojů

If you need to embed an image, modify `MyHandler` to return a stream that contains the image bytes:

```csharp
public override Stream HandleResource(Resource resource)
{
    if (resource.Uri.EndsWith(".png"))
    {
        // Load the PNG from embedded resources or a database.
        byte[] imageBytes = File.ReadAllBytes("logo.png");
        return new MemoryStream(imageBytes);
    }
    return new MemoryStream(); // Fallback for other resources.
}
```

### 2. Práce s velkými dokumenty

U velmi velkých HTML souborů zvažte použití `BufferedStream` nebo přímý zápis do souborového `FileStream`, pokud se paměť stane úzkým hrdlem. Vzor pro **jak uložit HTML do streamu** zůstává stejný; mění se pouze typ streamu.

### 3. Bezpečnost vláken

`ResourceHandler` instances are **not** guaranteed to be thread‑safe. If you plan to reuse a handler across parallel conversions, either:

* Vytvořte nový handler pro každou konverzi, nebo
* Chraňte sdílený stav uvnitř `HandleResource` pomocí zámků.

### 4. Uvolňování zdrojů

Jak `HTMLDocument`, tak všechny streamy, které vytvoříte, implementují `IDisposable`. Zabalení do `using` bloků, jak je ukázáno v Kroku 4, zajišťuje čisté uvolnění neřízených zdrojů.

## Pro tip: Opětovné použití stejného MemoryStream

If you need to concatenate multiple HTML outputs into a single stream, reset the position before each `Save` call:

```csharp
outputStream.Position = 0; // Clear previous content
document.Save(outputStream, saveOptions);
```

Alternativně vytvořte nový `MemoryStream` pro každou konverzi, aby nedošlo k nechtěnému smíchání dat.

## Kompletní funkční příklad

Níže je kompletní program, který můžete zkopírovat a vložit do konzolové aplikace. Kompiluje s .NET 6.0 a Aspose.HTML 23.9 (nebo novějším).

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using System;
using System.IO;

namespace ResourceHandlerDemo
{
    // Custom handler that supplies empty streams for any requested resource.
    class MyHandler : ResourceHandler
    {
        public override Stream HandleResource(Resource resource)
        {
            // Return an empty stream to suppress external resources.
            return new MemoryStream();
        }
    }

    class Program
    {
        static void Main()
        {
            // Step 1: Create the HTML document.
            string htmlContent = "<html><body>Hello World</body></html>";
            HTMLDocument document = new HTMLDocument(htmlContent);

            // Step 2: Attach the custom ResourceHandler.
            MyHandler customHandler = new MyHandler();

            // Step 3: Configure save options.
            HtmlSaveOptions saveOptions = new HtmlSaveOptions
            {
                ResourceHandler = customHandler
            };

            // Step 4: Save to a MemoryStream.
            using (MemoryStream outputStream = new MemoryStream())
            {
                document.Save(outputStream, saveOptions);
                outputStream.Position = 0;

                // Display the generated HTML for verification.
                using (StreamReader reader = new StreamReader(outputStream))
                {
                    string resultHtml = reader.ReadToEnd();
                    Console.WriteLine("Generated HTML:");
                    Console.WriteLine(resultHtml);
                }
            }
        }
    }
}
```

Spusťte program a uvidíte vygenerované HTML vytištěné do konzole, což potvrzuje, že **jak použít ResourceHandler** a **jak uložit HTML do streamu** spolu bez problémů fungují.

## Závěr

Tento tutoriál ukázal **jak použít ResourceHandler** k řízení načítání externích zdrojů a přesné kroky **jak uložit HTML do streamu** pomocí Aspose.HTML v C#. Nyní máte znovupoužitelný vzor pro generování HTML v paměti, což je ideální pro webová API, šablony e‑mailů a pipeline pro konverzi do PDF.

### Co dál?

* **Vložit skutečné obrázky nebo CSS** rozšířením `MyHandler` (viz sekce „Vkládání skutečných zdrojů“).
* **Převést stream do PDF** pomocí `HtmlConverter.ConvertHtml`, pokud potřebujete tisknutelnou verzi.
* **Streamovat výsledek přímo z Web API** pomocí `FileStreamResult` nebo `MemoryStream` v ASP.NET

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s krok‑za‑krokem vysvětlením, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Save HTML in C# with Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-with-custom-resource-handler/)
- [how to use handler in Aspose.HTML – Load HTML, Save as ZIP](/html/english/net/html-extensions-and-conversions/how-to-use-handler-in-aspose-html-load-html-save-as-zip/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
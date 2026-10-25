---
category: general
date: 2026-10-25
description: Hur man använder ResourceHandler för att kontrollera resurshämtning och
  hur man sparar HTML till en ström med Aspose.HTML i C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use resourcehandler
- how to save html to stream
- Aspose.HTML ResourceHandler
- HTML to MemoryStream C#
- custom resource handling C#
language: sv
lastmod: 2026-10-25
og_description: Hur man använder ResourceHandler för att kontrollera resursladdning
  och hur man sparar HTML till en ström med Aspose.HTML för .NET.
og_image_alt: Screenshot of C# code using ResourceHandler to save HTML to a memory
  stream
og_title: Hur man använder ResourceHandler och sparar HTML till en ström i C#
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
title: Hur man använder ResourceHandler och sparar HTML till en ström i C#
url: /sv/net/working-with-html-documents/how-to-use-resourcehandler-and-save-html-to-a-stream-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder ResourceHandler och sparar HTML till en ström i C#

Om du behöver **how to use ResourceHandler** när du renderar HTML med Aspose.HTML, visar den här guiden en komplett, färdig‑att‑köra lösning. Du kommer också att lära dig **how to save HTML to a stream** så att du kan överföra resultatet utan att röra filsystemet.

Att arbeta med HTML i minnet är vanligt när du genererar e‑post, API‑svar eller PDF‑filer i farten. I slutet av den här handledningen kommer du att ha ett självständigt C#‑program som skapar ett `HTMLDocument`, tillhandahåller en anpassad `ResourceHandler` och skriver resultatet till en `MemoryStream`.

## Förutsättningar

Innan du börjar, se till att du har:

* .NET 6.0 eller senare (koden fungerar också med .NET Core 3.1 och .NET Framework 4.7+)
* **Aspose.HTML for .NET** NuGet‑paketet  
  ```bash
  dotnet add package Aspose.HTML
  ```
* En grundläggande förståelse för C# async/await (valfritt men hjälpsamt)

## Vad handledningen täcker

* Hur man **how to use ResourceHandler** för att avlyssna bild-, CSS- eller skriptförfrågningar
* Hur man konfigurerar `HtmlSaveOptions` med en anpassad hanterare
* Hur man **how to save HTML to a stream** med `MemoryStream`
* Hantering av kantfall såsom saknade resurser och strömutsläpp
* Tips för att utöka hanteraren för att bädda in riktiga resurser senare

## Steg 1: Skapa ett enkelt HTML‑dokument från en sträng

Det första steget är att instansiera ett `HTMLDocument` från rå HTML. Detta objekt representerar DOM‑trädet som Aspose.HTML kommer att rendera.

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

> **Varför detta är viktigt:** Att skapa dokumentet från en sträng håller hela arbetsflödet i minnet, vilket är avgörande när du senare **how to save HTML to a stream** utan att röra hårddisken.

## Steg 2: Implementera en anpassad ResourceHandler

`ResourceHandler` är den krok som Aspose.HTML använder när den behöver en extern resurs (bilder, CSS, teckensnitt osv.). Genom att åsidosätta `HandleResource` bestämmer du vilken ström som ska returneras för varje begäran.

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

> **Varför du kan behöva detta:** När du genererar HTML för e‑post eller API‑svar vill du ofta undvika externa anrop. Att tillhandahålla tomma strömmar förhindrar 404‑fel och snabbar upp renderingen. Detta demonstrerar **how to use ResourceHandler** för en “resursfri” utskrift.

## Steg 3: Konfigurera HtmlSaveOptions för att använda den anpassade hanteraren

`HtmlSaveOptions` låter dig styra sparprocessen. Tilldela `ResourceHandler`‑egenskapen till din anpassade implementation.

```csharp
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // Attach the handler so every resource request goes through MyHandler.
    ResourceHandler = customHandler
};
```

> **Tips:** Om du senare behöver bädda in CSS eller bilder, ersätt `MyHandler` med en version som returnerar lämpliga strömmar baserat på `resource.Uri`.

## Steg 4: Spara dokumentet till en MemoryStream

Nu har du allt redo för att **how to save HTML to a stream**. Att använda en `MemoryStream` håller utdata i RAM, vilket gör det enkelt att skicka över HTTP, lagra i en databas eller skicka vidare till ett annat API.

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

### Förväntad output

Att köra koden ovan skriver ut:

```html
<html><head></head><body>Hello World</body></html>
```

Eftersom den anpassade hanteraren returnerar tomma strömmar, löses inga externa `<link>`‑ eller `<img>`‑taggar upp, och HTML‑koden förblir ren.

## Vanliga variationer och kantfall

### 1. Bädda in riktiga resurser

Om du behöver bädda in en bild, ändra `MyHandler` så att den returnerar en ström som innehåller bildens byte:

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

### 2. Hantera stora dokument

För mycket stora HTML‑filer, överväg att använda `BufferedStream` eller skriva direkt till en fil‑baserad `FileStream` om minnet blir en flaskhals. Mönstret för **how to save HTML to a stream** förblir detsamma; endast strömtypen ändras.

### 3. Trådsäkerhet

`ResourceHandler`‑instanser är **inte** garanterade att vara trådsäkra. Om du planerar att återanvända en hanterare över parallella konverteringar, antingen:

* Skapa en ny hanterare per konvertering, eller
* Skydda delat tillstånd inuti `HandleResource` med lås.

### 4. Frigöra resurser

Både `HTMLDocument` och alla strömmar du skapar implementerar `IDisposable`. Att omsluta dem i `using`‑block, som visas i Steg 4, garanterar en ren frigöring av ohanterade resurser.

## Pro‑tips: Återanvända samma MemoryStream

Om du behöver sammanfoga flera HTML‑utdata till en enda ström, återställ positionen före varje `Save`‑anrop:

```csharp
outputStream.Position = 0; // Clear previous content
document.Save(outputStream, saveOptions);
```

Alternativt, skapa en ny `MemoryStream` för varje konvertering för att undvika oavsiktlig datamischning.

## Fullt fungerande exempel

Nedan är det kompletta programmet som du kan kopiera‑och‑klistra in i en konsolapplikation. Det kompileras med .NET 6.0 och Aspose.HTML 23.9 (eller senare).

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

Kör programmet så ser du den genererade HTML‑koden skrivas ut i konsolen, vilket bekräftar att **how to use ResourceHandler** och **how to save HTML to a stream** fungerar tillsammans sömlöst.

## Slutsats

Denna handledning demonstrerade **how to use ResourceHandler** för att kontrollera laddning av externa resurser och de exakta stegen **how to save HTML to a stream** med Aspose.HTML i C#. Du har nu ett återanvändbart mönster för HTML‑generering i minnet, vilket är idealiskt för webb‑API:er, e‑postmallar och PDF‑konverteringspipelines.

### Vad blir nästa?

* **Bädda in riktiga bilder eller CSS** genom att utöka `MyHandler` (se avsnittet “Embedding real resources”).
* **Konvertera strömmen till PDF** med `HtmlConverter.ConvertHtml` om du behöver en utskrivbar version.
* **Strömma resultatet direkt från ett Web‑API** med `FileStreamResult` eller `MemoryStream` i ASP.NET

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man sparar HTML i C# – Komplett guide med en anpassad resurshanterare](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Hur man sparar HTML i C# med anpassad resurshanterare](/html/english/net/working-with-html-documents/how-to-save-html-in-c-with-custom-resource-handler/)
- [hur man använder hanterare i Aspose.HTML – Ladda HTML, spara som ZIP](/html/english/net/html-extensions-and-conversions/how-to-use-handler-in-aspose-html-load-html-save-as-zip/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-08-15
description: Skapa en anpassad resurs‑hanterare i C# för att hantera HTML‑resurser
  som bilder och CSS. Lär dig HTMLLoadOptions, minnesströmmar och laddning av HTMLDocument.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom resource handler
- C# resource handler
- HTMLLoadOptions
- HTMLDocument loading
- memory stream for resources
language: sv
lastmod: 2026-08-15
og_description: Skapa en anpassad resurs‑hanterare i C# för att kontrollera hur HTML‑resurser
  strömmas. Denna handledning visar hur man konfigurerar HTMLLoadOptions, hanterar
  minnesström och laddar HTMLDocument med anpassad logik.
og_image_alt: Screenshot of C# code defining a custom resource handler class for HTML
  loading
og_title: Skapa anpassad resurs‑hanterare i C# – fullständig guide för HTML‑resurshantering
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  headline: Create custom resource handler in C# for HTML loading
  type: TechArticle
- description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  name: Create custom resource handler in C# for HTML loading
  steps:
  - name: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
    text: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
  - name: Configure `HTMLLoadOptions` to use the handler.
    text: Configure `HTMLLoadOptions` to use the handler.
  - name: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
    text: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
  - name: (Optional) Store received resources to disk for verification.
    text: (Optional) Store received resources to disk for verification.
  type: HowTo
tags:
- C#
- HTML
- resource handling
title: Skapa anpassad resurs‑hanterare i C# för HTML‑laddning
url: /sv/net/working-with-html-documents/create-custom-resource-handler-in-c-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa anpassad resurs‑hanterare i C# för HTML‑laddning

Om du behöver **create custom resource handler** för HTML‑filer, visar den här guiden exakt hur. Du kommer att lära dig att avlyssna bilder, CSS och andra resurser när du laddar ett HTML‑dokument, med hjälp av `HTMLLoadOptions` och en minnes‑baserad ström.

Handledningen täcker allt som krävs för att implementera en återanvändbar hanterare, konfigurera laddningsalternativ och verifiera att resurser fångas korrekt. Ingen extern dokumentation behövs—bara koden nedan och förklaringarna.

## Förutsättningar

- .NET 6.0 eller senare
- Grundläggande kunskap om C#
- En referens till HTML‑bearbetningsbiblioteket som tillhandahåller `HTMLDocument`, `HtmlLoadOptions` och `ResourceHandler` (t.ex. GroupDocs.Viewer för .NET)

## Översikt av lösningen

Vi kommer att:

1. **Create a custom resource handler** genom att subklassa `ResourceHandler`.
2. Konfigurera `HTMLLoadOptions` för att använda hanteraren.
3. Ladda en HTML‑fil med `HTMLDocument` medan hanteraren tillhandahåller en ström för varje resurs.
4. (Valfritt) Spara mottagna resurser till disk för verifiering.

Varje steg innehåller full källkod och resonemanget bakom.

## Steg 1: Definiera den anpassade resurs‑hanterarklassen

Att skapa en anpassad hanterare innebär att åsidosätta `HandleResource` så att biblioteket kan skriva resurs‑byte till en ström du kontrollerar. Att använda en `MemoryStream` håller data i minnet, vilket är idealiskt för testning eller vidare bearbetning.

```csharp
using System;
using System.IO;
using GroupDocs.Viewer.Handler;   // Adjust namespace to match your library

namespace HtmlResourceDemo
{
    /// <summary>
    /// Provides a memory stream for each HTML resource (images, CSS, etc.).
    /// </summary>
    public class MyHandler : ResourceHandler
    {
        /// <summary>
        /// Called by the viewer for every external resource referenced in the HTML.
        /// </summary>
        /// <param name="info">Information about the resource (name, MIME type, etc.).</param>
        /// <returns>A writable stream that receives the resource data.</returns>
        public override Stream HandleResource(ResourceInfo info)
        {
            // A fresh MemoryStream ensures the viewer can write the resource bytes.
            // You could replace this with a FileStream to save directly to disk.
            return new MemoryStream();
        }
    }
}
```

**Varför detta är viktigt:**  
Att åsidosätta `HandleResource` ger dig full kontroll över var resursdata placeras. Om du senare behöver cacha bilder, transformera CSS eller logga resursanvändning, kan du ersätta `MemoryStream` med någon anpassad ström‑implementation.

## Steg 2: Konfigurera `HTMLLoadOptions` för att använda hanteraren

`HTMLLoadOptions` låter dig ansluta hanteraren till laddnings‑pipeline. Genom att sätta egenskapen `ResourceHandler` instrueras visaren att anropa `MyHandler` för varje extern tillgång.

```csharp
using GroupDocs.Viewer.Options;   // Namespace for HtmlLoadOptions

// ...

var loadOptions = new HtmlLoadOptions
{
    // Attach the custom handler defined in Step 1
    ResourceHandler = new MyHandler()
};
```

**Varför detta är viktigt:**  
Utan att tilldela `ResourceHandler` skulle visaren skriva resurser till sin standardplats (ofta en temporär mapp). Genom att specificera din egen hanterare, **create custom resource handler**‑beteendet som matchar din applikations lagringsstrategi.

## Steg 3: Ladda HTML‑dokumentet med de konfigurerade alternativen

Ladda nu HTML‑filen. Visaren kommer att anropa `MyHandler.HandleResource` för varje resurs den stöter på.

```csharp
using GroupDocs.Viewer;           // Namespace for HTMLDocument

// Path to the source HTML file
string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// Load the document using the custom load options
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);
```

Vid detta tillfälle har HTML‑innehållet parsats och alla externa resurser har strömmas in i minnesbuffertarna som tillhandahålls av `MyHandler`.

## Steg 4 (valfritt): Åtkomst till de fångade resurserna

Om du behöver inspektera eller lagra resurserna kan du modifiera `MyHandler` för att spara varje `MemoryStream` i en dictionary nycklad med resursnamnet.

```csharp
public class MyHandler : ResourceHandler
{
    // Stores streams for later retrieval
    public Dictionary<string, MemoryStream> Resources { get; } = new();

    public override Stream HandleResource(ResourceInfo info)
    {
        var stream = new MemoryStream();
        Resources[info.Name] = stream;
        return stream;
    }
}
```

Efter laddning kan du iterera över `handler.Resources` och skriva varje till disk:

```csharp
var handler = new MyHandler();
var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);

// Save each captured resource
foreach (var kvp in handler.Resources)
{
    string fileName = Path.Combine("output_resources", kvp.Key);
    File.WriteAllBytes(fileName, kvp.Value.ToArray());
    Console.WriteLine($"Saved resource: {fileName}");
}
```

**Varför detta är viktigt:**  
Att lagra resurser möjliggör efterbehandling såsom bildoptimering, CSS‑minifiering eller arkivering. Det ger också en påtaglig verifiering att **create custom resource handler**‑logiken fungerar som avsett.

## Steg 5: Rensa upp

Både `HTMLDocument` och alla strömmar bör avyttras för att frigöra ohanterade resurser.

```csharp
doc.Dispose();                     // Releases internal buffers
foreach (var stream in handler.Resources.Values)
{
    stream.Dispose();              // Flushes and releases memory
}
```

## Fullt körbart exempel

Nedan är ett fristående program som demonstrerar alla steg från klassdefinition till resursutvinning.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Viewer;
using GroupDocs.Viewer.Handler;
using GroupDocs.Viewer.Options;

namespace HtmlResourceDemo
{
    public class MyHandler : ResourceHandler
    {
        public Dictionary<string, MemoryStream> Resources { get; } = new();

        public override Stream HandleResource(ResourceInfo info)
        {
            var stream = new MemoryStream();
            Resources[info.Name] = stream;
            return stream;
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare paths
            string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");
            string outputDir = Path.Combine("output_resources");
            Directory.CreateDirectory(outputDir);

            // 2️⃣ Create handler and load options
            var handler = new MyHandler();
            var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };

            // 3️⃣ Load the HTML document
            using (HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions))
            {
                // Document is now loaded; resources are in handler.Resources
            }

            // 4️⃣ Persist captured resources
            foreach (var kvp in handler.Resources)
            {
                string filePath = Path.Combine(outputDir, kvp.Key);
                File.WriteAllBytes(filePath, kvp.Value.ToArray());
                Console.WriteLine($"Saved: {filePath}");
            }

            // 5️⃣ Clean up streams
            foreach (var stream in handler.Resources.Values)
                stream.Dispose();

            Console.WriteLine("All resources processed.");
        }
    }
}
```

**Förväntad output**

```
Saved: output_resources/logo.png
Saved: output_resources/styles.css
Saved: output_resources/banner.jpg
All resources processed.
```

Konsolen listar varje resurs som visaren strömmade genom din anpassade hanterare, vilket bekräftar att **create custom resource handler**‑arbetsflödet lyckades.

## Vanliga frågor och kantfall

| Question | Answer |
|----------|--------|
| *Vad händer om en resurs är stor (t.ex. högupplöst bild)?* | Ersätt `MemoryStream` med en `FileStream` som pekar på en temporär mapp. Detta förhindrar överdriven minnesanvändning. |
| *Kan jag filtrera resurser efter typ?* | Inuti `HandleResource`, inspektera `info.MimeType` eller `info.Extension` och returnera `null` för oönskade typer. Att returnera `null` instruerar visaren att hoppa över resursen. |
| *Krävs trådsäkerhet?* | Om samma hanterarinstans används över flera samtidiga laddningar, skydda `Resources`‑dictionaryn med en låsning eller använd en trådsäker samling. |
| *Hur stödjer jag relativa URL:er?* | `ResourceInfo` innehåller den ursprungliga URL:en; du kan kombinera den med basvägen för HTML‑filen för att lösa relativa referenser innan lagring. |

## Slutsats

Du vet nu hur du **create custom resource handler** i C# för HTML‑laddning, konfigurerar `HTMLLoadOptions`, fångar strömmade tillgångar och rensar upp på ett ansvarsfullt sätt. Detta mönster ger dig full kontroll över resurshantering, vilket möjliggör scenarier som bildbehandling i farten, CSS‑omskrivning eller säker lagring.

Nästa steg, utforska relaterade ämnen som **HTMLDocument loading** med olika renderingsalternativ, eller utöka hanteraren till **C# resource handler**‑implementationer som skriver direkt till molnlagring. Experimentera med hanterarens `HandleResource`‑metod för att anpassa den till ditt projekts specifika resursarbetsflöde.

## Vad bör du lära dig härnäst?

Följande handledningar täcker nära besläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Skapa HTML från sträng i C# – Guide för anpassad resurs‑hanterare](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Anpassad resurs‑hanterare i C# – Konvertera HTML till ZIP‑handledning](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [Hur man sparar HTML i C# – Komplett guide med en anpassad resurs‑hanterare](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
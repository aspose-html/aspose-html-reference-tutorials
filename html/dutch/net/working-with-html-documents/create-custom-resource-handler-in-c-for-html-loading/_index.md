---
category: general
date: 2026-08-15
description: Maak een aangepaste resourcehandler in C# om HTML‑resources zoals afbeeldingen
  en CSS te beheren. Leer HTMLLoadOptions, geheugenstromen en het laden van HTMLDocument.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom resource handler
- C# resource handler
- HTMLLoadOptions
- HTMLDocument loading
- memory stream for resources
language: nl
lastmod: 2026-08-15
og_description: Maak een aangepaste resourcehandler in C# om te bepalen hoe HTML‑resources
  worden gestreamd. Deze tutorial toont de configuratie van HTMLLoadOptions, het omgaan
  met geheugenstreams en het laden van HTMLDocument met aangepaste logica.
og_image_alt: Screenshot of C# code defining a custom resource handler class for HTML
  loading
og_title: Maak een aangepaste resourcehandler in C# – volledige gids voor HTML‑resourcebeheer
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
title: Maak een aangepaste resourcehandler in C# voor het laden van HTML
url: /nl/net/working-with-html-documents/create-custom-resource-handler-in-c-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak aangepaste resourcehandler in C# voor HTML laden

Als je **create custom resource handler** voor HTML‑bestanden moet maken, laat deze gids je precies zien hoe. Je leert afbeeldingen, CSS en andere assets te onderscheppen tijdens het laden van een HTML‑document, met behulp van `HTMLLoadOptions` en een geheugen‑gebaseerde stream.

De tutorial behandelt alles wat nodig is om een herbruikbare handler te implementeren, laadopties te configureren en te verifiëren dat resources correct worden vastgelegd. Er is geen externe documentatie nodig—alleen de onderstaande code en de uitleg.

## Vereisten

- .NET 6.0 of later
- Basiskennis van C#
- Een referentie naar de HTML‑verwerkingsbibliotheek die `HTMLDocument`, `HtmlLoadOptions` en `ResourceHandler` levert (bijv. GroupDocs.Viewer voor .NET)

## Overzicht van de oplossing

We zullen:

1. **Create a custom resource handler** door `ResourceHandler` te subklassen.
2. Configure `HTMLLoadOptions` om de handler te gebruiken.
3. Laad een HTML‑bestand met `HTMLDocument` terwijl de handler een stream levert voor elke resource.
4. (Optioneel) Sla ontvangen resources op schijf voor verificatie.

Elke stap bevat volledige broncode en de reden erachter.

## Stap 1: Definieer de custom resource handler‑klasse

Een custom handler maken betekent dat je `HandleResource` overschrijft zodat de bibliotheek resource‑bytes naar een door jou beheerde stream kan schrijven. Het gebruik van een `MemoryStream` houdt de gegevens in het geheugen, wat ideaal is voor testen of verdere verwerking.

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

**Waarom dit belangrijk is:**  
Het overschrijven van `HandleResource` geeft je volledige controle over waar resource‑data naartoe gaat. Als je later afbeeldingen wilt cachen, CSS wilt transformeren of resource‑gebruik wilt loggen, kun je de `MemoryStream` vervangen door een willekeurige custom stream‑implementatie.

## Stap 2: Configure `HTMLLoadOptions` om de handler te gebruiken

`HTMLLoadOptions` stelt je in staat de handler in de laad‑pipeline te koppelen. Het instellen van de eigenschap `ResourceHandler` vertelt de viewer om `MyHandler` aan te roepen voor elk extern asset.

```csharp
using GroupDocs.Viewer.Options;   // Namespace for HtmlLoadOptions

// ...

var loadOptions = new HtmlLoadOptions
{
    // Attach the custom handler defined in Step 1
    ResourceHandler = new MyHandler()
};
```

**Waarom dit belangrijk is:**  
Zonder het toewijzen van `ResourceHandler` zou de viewer resources naar de standaardlocatie schrijven (meestal een tijdelijke map). Door je eigen handler op te geven, creëer je **custom resource handler**‑gedrag dat aansluit bij de opslagstrategie van je applicatie.

## Stap 3: Laad het HTML‑document met de geconfigureerde opties

Laad nu het HTML‑bestand. De viewer zal `MyHandler.HandleResource` aanroepen voor elke resource die het tegenkomt.

```csharp
using GroupDocs.Viewer;           // Namespace for HTMLDocument

// Path to the source HTML file
string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// Load the document using the custom load options
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);
```

Op dit punt is de HTML‑inhoud geparseerd en zijn alle externe resources gestreamd naar de geheugen‑buffers die door `MyHandler` worden geleverd.

## Stap 4 (optioneel): Toegang tot de vastgelegde resources

Als je de resources wilt inspecteren of bewaren, kun je `MyHandler` aanpassen om elke `MemoryStream` op te slaan in een dictionary met de resource‑naam als sleutel.

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

Na het laden kun je itereren over `handler.Resources` en elk naar schijf schrijven:

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

**Waarom dit belangrijk is:**  
Het opslaan van resources maakt post‑processing mogelijk, zoals beeldoptimalisatie, CSS‑minimalisatie of archivering. Het biedt ook een tastbare verificatie dat de **create custom resource handler**‑logica werkt zoals bedoeld.

## Stap 5: Opruimen

Zowel `HTMLDocument` als eventuele streams moeten worden disposed om niet‑geheugengebonden resources vrij te geven.

```csharp
doc.Dispose();                     // Releases internal buffers
foreach (var stream in handler.Resources.Values)
{
    stream.Dispose();              // Flushes and releases memory
}
```

## Volledig uitvoerbaar voorbeeld

Hieronder staat een zelfstandige programma‑voorbeeld dat alle stappen van klasse‑definitie tot resource‑extractie demonstreert.

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

**Verwachte output**

```
Saved: output_resources/logo.png
Saved: output_resources/styles.css
Saved: output_resources/banner.jpg
All resources processed.
```

De console geeft elke resource weer die de viewer via jouw custom handler heeft gestreamd, wat bevestigt dat de **create custom resource handler**‑workflow geslaagd is.

## Veelgestelde vragen en randgevallen

| Vraag | Antwoord |
|----------|--------|
| *Wat als een resource groot is (bijv. een hoge‑resolutie afbeelding)?* | Vervang `MemoryStream` door een `FileStream` die naar een tijdelijke map wijst. Dit voorkomt overmatig geheugenverbruik. |
| *Kan ik resources filteren op type?* | Binnen `HandleResource` inspecteer je `info.MimeType` of `info.Extension` en retourneer je `null` voor ongewenste types. Het retourneren van `null` vertelt de viewer de resource over te slaan. |
| *Is thread‑veiligheid vereist?* | Als dezelfde handler‑instantie wordt gebruikt bij meerdere gelijktijdige loads, bescherm dan de `Resources`‑dictionary met een lock of gebruik een thread‑veilige collectie. |
| *Hoe ondersteun ik relatieve URL's?* | `ResourceInfo` bevat de originele URL; je kunt deze combineren met het basispad van het HTML‑bestand om relatieve verwijzingen op te lossen voordat je ze opslaat. |

## Conclusie

Je weet nu hoe je **create custom resource handler** in C# voor HTML‑laden kunt maken, `HTMLLoadOptions` kunt configureren, gestreamde assets kunt vastleggen en verantwoord kunt opruimen. Dit patroon geeft je volledige controle over resource‑beheer, waardoor scenario's zoals on‑the‑fly beeldverwerking, CSS‑herwerking of veilige opslag mogelijk zijn.

Vervolgens kun je gerelateerde onderwerpen verkennen, zoals **HTMLDocument loading** met verschillende renderopties, of de handler uitbreiden naar **C# resource handler**‑implementaties die direct naar cloud‑opslag schrijven. Experimenteer met de `HandleResource`‑methode van de handler om deze aan te passen aan de specifieke resource‑workflow van je project.

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [HTML maken vanuit string in C# – Custom Resource Handler gids](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Custom Resource Handler in C# – HTML naar ZIP converteren tutorial](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [Hoe HTML opslaan in C# – Complete gids met een Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
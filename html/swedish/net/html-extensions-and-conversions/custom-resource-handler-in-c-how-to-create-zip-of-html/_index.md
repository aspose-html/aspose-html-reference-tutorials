---
category: general
date: 2026-07-21
description: Anpassad resurs‑hanterare i C# låter dig enkelt exportera HTML till ZIP—lär
  dig hur du skapar HTML‑ZIP‑arkiv med Aspose.HTML och hur du skapar zip‑filer programatiskt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom resource handler
- how to create zip
- create html zip
- export html to zip
- save html zip
language: sv
lastmod: 2026-07-21
og_description: Anpassad resurs‑hanterare i C# gör export av HTML till ZIP enkelt.
  Följ den här steg‑för‑steg‑guiden för att skapa HTML‑ZIP‑filer med Aspose.HTML.
og_image_alt: Diagram showing custom resource handler flow for exporting HTML to a
  ZIP archive
og_title: Anpassad resurs‑hanterare i C# – Exportera HTML till ZIP på några minuter
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Custom resource handler in C# lets you export HTML to ZIP easily—learn
    how to create HTML ZIP archives with Aspose.HTML and how to create zip files programmatically.
  headline: Custom Resource Handler in C# – How to Create ZIP of HTML
  type: TechArticle
- description: Custom resource handler in C# lets you export HTML to ZIP easily—learn
    how to create HTML ZIP archives with Aspose.HTML and how to create zip files programmatically.
  name: Custom Resource Handler in C# – How to Create ZIP of HTML
  steps:
  - name: '**Forgot to set `SaveFormat.Zip`** – Aspose.HTML defaults to a folder output.
      Always set `saveOptions.SaveFormat = SaveFormat.Zip;`.'
    text: '**Forgot to set `SaveFormat.Zip`** – Aspose.HTML defaults to a folder output.
      Always set `saveOptions.SaveFormat = SaveFormat.Zip;`.'
  - name: '**Output directory doesn’t exist** – `doc.Save` won’t create the parent
      folder. Use `Directory.CreateDirectory(Path.GetDirectoryName(outputPath));`
      beforehand.'
    text: '**Output directory doesn’t exist** – `doc.Save` won’t create the parent
      folder. Use `Directory.CreateDirectory(Path.GetDirectoryName(outputPath));`
      beforehand.'
  - name: '**Handler returns a closed stream** – The stream must be writable and open;
      otherwise the ZIP will be corrupted.'
    text: '**Handler returns a closed stream** – The stream must be writable and open;
      otherwise the ZIP will be corrupted.'
  - name: '**Large documents exhaust memory** – For massive sites, consider streaming
      directly to a file stream inside the handler instead of `MemoryStream`.'
    text: '**Large documents exhaust memory** – For massive sites, consider streaming
      directly to a file stream inside the handler instead of `MemoryStream`.'
  type: HowTo
tags:
- Aspose.HTML
- C#
- ZIP
- HTML export
title: Anpassad resurshanterare i C# – Hur man skapar ZIP av HTML
url: /sv/net/html-extensions-and-conversions/custom-resource-handler-in-c-how-to-create-zip-of-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Anpassad resurs‑hanterare i C# – Hur man skapar ZIP av HTML

Har du någonsin undrat hur man skapar en **custom resource handler** som förvandlar ett HTML‑dokument till en prydlig ZIP‑fil? Du är inte ensam. Många utvecklare stöter på problem när de måste paketera en HTML‑sida tillsammans med dess CSS, bilder och skript för offline‑användning. Den goda nyheten? Med Aspose.HTML kan du göra det på bara några rader C#‑kod – och du får full kontroll över var varje resurs hamnar.

I den här handledningen går vi igenom hela processen för **export html to zip** med en **custom resource handler**. När du är klar har du en återanvändbar komponent som inte bara **save html zip**‑filer utan också låter dig finjustera lagringsstrategin (minne, filsystem, moln, du bestämmer). Låt oss dyka ner.

## Vad du kommer att lära dig

- Varför en **custom resource handler** är det föredragna sättet att hantera HTML‑resurser under export.  
- Hur man implementerar hanteraren för att skriva varje resurs till en minnesström.  
- De exakta stegen för att **create html zip**‑arkiv med Aspose.HTML:s `HtmlSaveOptions`.  
- Tips för att hantera stora tillgångar, felsöka vanliga fallgropar och utöka lösningen för molnlagring.  

> **Förutsättningar** – Du behöver .NET 6+ (eller .NET Framework 4.7.2+), Visual Studio 2022 (eller någon IDE du föredrar), och en aktiv Aspose.HTML‑licens. Om du ännu inte har en licens fungerar gratisprovet utmärkt för lärande.

---

## Steg 1: Implementera en anpassad resurs‑hanterare

Kärnan i lösningen är en klass som ärver från `Aspose.Html.Storage.ResourceHandler`. Denna **custom resource handler** bestämmer **hur varje resurs** (HTML‑markup, CSS‑filer, bilder osv.) lagras när dokumentet sparas.

```csharp
using System.IO;
using Aspose.Html.Storage;

/// <summary>
/// Writes every requested resource to a fresh memory stream.
/// This makes the save operation entirely in‑memory, perfect for ZIP creation.
/// </summary>
class MyHandler : ResourceHandler
{
    /// <summary>
    /// Called by Aspose.HTML for each resource that needs to be persisted.
    /// </summary>
    /// <param name="resource">Metadata about the resource (name, mime‑type, …).</param>
    /// <returns>A writable stream where the resource will be written.</returns>
    public override Stream HandleResource(Resource resource)
    {
        // For a ZIP archive we just return a new MemoryStream.
        // Aspose.HTML will write the resource bytes into it.
        return new MemoryStream();
    }
}
```

**Varför detta är viktigt:**  
Om du hoppar över hanteraren och förlitar dig på standardfilsystemlagring kommer Aspose.HTML att sprida filer över din disk, vilket gör städning till en mardröm. Genom att leda allt genom en **custom resource handler** håller du hela processen prydlig och kan senare bestämma om du vill spara ZIP‑filen på disk, ladda upp den till Azure Blob Storage eller till och med returnera den direkt från ett webb‑API.

## Steg 2: Bygg HTML‑dokumentet

Nästa steg är att skapa HTML‑koden du vill zippa. För demonstration använder vi en enkel sträng, men du kan läsa in från en fil, en StringBuilder eller till och med generera den dynamiskt.

```csharp
using Aspose.Html;

// Create an in‑memory HTML document from a raw string.
HTMLDocument doc = new HTMLDocument(
    "<html><head><style>h1{color:#0066CC;}</style></head>" +
    "<body><h1>Hello, World!</h1><p>This page is packaged inside a ZIP.</p></body></html>"
);
```

> **Proffstips:** Om din sida refererar till extern CSS eller bilder, se till att dessa filer är tillgängliga för `HTMLDocument` (t.ex. genom att använda `doc.Open` med en bas‑URL). **custom resource handler** kommer att fånga dem automatiskt när du sparar.

## Steg 3: Konfigurera sparalternativ för att exportera HTML till ZIP

Nu instruerar vi Aspose.HTML att använda vår **custom resource handler** och att producera ett ZIP‑arkiv istället för en lös mapp.

```csharp
using Aspose.Html.Rendering;
using Aspose.Html.Storage;

// Set up save options – the key is OutputStorage.
HtmlSaveOptions saveOptions = new HtmlSaveOptions();
saveOptions.OutputStorage = new MyHandler();   // <-- our custom handler
saveOptions.SaveFormat = SaveFormat.Zip;       // Explicitly request ZIP output
```

**Vad som händer under huven?**  
När `doc.Save` körs, strömmar Aspose.HTML varje resurs (HTML‑fil, CSS, bilder) in i den `MemoryStream` som returneras av `MyHandler`. När alla strömmar är fyllda komprimerar biblioteket dem till ett enda ZIP‑paket.

## Steg 4: Spara HTML‑ZIP‑filen

Till sist sparar du den minnes‑ZIP‑filen till disk (eller någon annan destination). Följande rad skriver arkivet till en mapp du anger.

```csharp
// Choose an output directory that already exists.
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.zip");

// The Save method will pull the data from our handler and write the ZIP.
doc.Save(outputPath, saveOptions);

Console.WriteLine($"✅ HTML ZIP created at: {outputPath}");
```

**Förväntat resultat:**  
Efter att programmet har körts ser du `output.zip` i din projektkatalog. Öppna den så hittar du:

- `index.html` – markupen vi definierade.  
- `style.css` – den inbäddade stilen extraherad som en separat fil (om någon).  
- Alla refererade bilder eller teckensnitt (inga i detta lilla exempel).

## Förstå den anpassade resurs‑hanterarens interna funktion

| Situation | Vad hanteraren gör | Varför det är bra |
|-----------|--------------------|-------------------|
| **Stora bilder** | Returnerar en ny `MemoryStream` för varje bild, vilket undviker filsystem‑I/O. | Håller minnesanvändningen förutsägbar; du kan senare byta strömmen mot en moln‑uppladdningsström. |
| **Misslyckad resursladdning** | Om en resurs inte kan hämtas kastar Aspose.HTML ett undantag innan `HandleResource` anropas. | Du kan fånga undantaget vid `doc.Save` och logga den saknade tillgången. |
| **Anpassad namngivning** | Åsidosätt `Resource.Name` i `HandleResource` för att byta namn på filer innan de läggs i ZIP‑filen. | Användbart när du behöver SEO‑vänliga filnamn eller vill ta bort frågesträngar. |

Om du behöver lagra resurser på Azure Blob Storage istället för i minnet, ersätt helt enkelt raden `return new MemoryStream();` med kod som returnerar en ström som stöds av moln‑SDK:n.

## Vanliga fallgropar & hur man undviker dem

1. **Glömt att sätta `SaveFormat.Zip`** – Aspose.HTML använder som standard en mapputmatning. Sätt alltid `saveOptions.SaveFormat = SaveFormat.Zip;`.
2. **Utdatamappen finns inte** – `doc.Save` skapar inte föräldramappen. Använd `Directory.CreateDirectory(Path.GetDirectoryName(outputPath));` i förväg.
3. **Hanteraren returnerar en stängd ström** – Strömmen måste vara skrivbar och öppen; annars blir ZIP‑filen korrupt.
4. **Stora dokument tömmer minnet** – För enorma webbplatser, överväg att strömma direkt till en filström i hanteraren istället för `MemoryStream`.

## Utöka lösningen: Från minne till moln

Anta att du vill **save html zip** direkt till en AWS S3‑bucket. Ersätt hanteraren med något liknande:

```csharp
class S3Handler : ResourceHandler
{
    private readonly AmazonS3Client _client;
    private readonly string _bucket;
    private readonly string _keyPrefix;

    public S3Handler(AmazonS3Client client, string bucket, string keyPrefix = "")
    {
        _client = client;
        _bucket = bucket;
        _keyPrefix = keyPrefix;
    }

    public override Stream HandleResource(Resource resource)
    {
        // Create a stream that uploads directly to S3.
        var request = new PutObjectRequest
        {
            BucketName = _bucket,
            Key = $"{_keyPrefix}/{resource.Name}",
            InputStream = new MemoryStream()
        };
        _client.PutObjectAsync(request).Wait();
        return request.InputStream;
    }
}
```

Nu kommer samma `doc.Save`‑anrop att skicka varje fil direkt till S3, och den slutgiltiga ZIP‑filen kan sättas ihop senare med AWS SDK:s multipart‑uppladdning. Detta visar **flexibiliteten** hos en **custom resource handler** — du styr lagringsmekanismen från början till slut.

## Fullt fungerande exempel (kopiera‑klistra klart)

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering;
using Aspose.Html.Storage;

class MyHandler : ResourceHandler
{
    public override Stream HandleResource(Resource resource)
    {
        // All resources go into a fresh memory stream.
        return new MemoryStream();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Build the HTML document.
        HTMLDocument doc = new HTMLDocument(
            "<html><head><style>h1{color:#0066CC;}</style></head>" +
            "<body><h1>Hello, World!</h1><p>This page is packaged inside a ZIP.</p></body></html>"
        );

        // 2️⃣ Prepare save options with our custom handler.
        HtmlSaveOptions saveOptions = new HtmlSaveOptions
        {
            OutputStorage = new MyHandler(),
            SaveFormat = SaveFormat.Zip
        };

        // 3️⃣ Define the output path (ensure the folder exists).
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.zip");
        Directory.CreateDirectory(Path.GetDirectoryName(outputPath));

        // 4️⃣ Save – the ZIP will contain index.html and any linked resources.
        doc.Save(outputPath, saveOptions);

        Console.WriteLine($"✅ HTML ZIP created at: {outputPath}");
    }
}
```

Kör programmet (`dotnet run`), så ser du ✅‑bekräftelsen. Öppna `output.zip` med någon arkivhanterare — du hittar en fullt funktionell HTML‑sida klar för offline‑användning.

## Visuell översikt

![Diagram som visar flödet för anpassad resurs‑hanterare vid export av HTML till ett ZIP‑arkiv](image.png)

*Alt text: Diagram som visar flödet för anpassad resurs‑hanterare vid export av HTML till ett ZIP‑arkiv*

## Slutsats

Vi har precis gått igenom allt du behöver för att **custom resource handler** din väg till en **create html zip**‑lösning i C#. Genom att implementera en liten subklass av `ResourceHandler`, konfigurera `HtmlSaveOptions` och anropa

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man sparar HTML i C# – Komplett guide med en anpassad resurs‑hanterare](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Skapa HTML från sträng i C# – Guide för anpassad resurs‑hanterare](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Hur man zippar HTML i C# – Spara HTML till ZIP](/html/english/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
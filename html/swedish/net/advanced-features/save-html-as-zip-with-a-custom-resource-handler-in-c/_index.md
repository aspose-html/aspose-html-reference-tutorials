---
category: general
date: 2026-08-19
description: Spara HTML som ZIP i C# med Aspose.HTML och en anpassad resurs‑hanterare.
  Följ den här steg‑för‑steg‑guiden för att bädda in resurser och skapa ett portabelt
  arkiv.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save HTML as ZIP
- custom resource handler
- Aspose.HTML C#
- HTML archive generation
- resource streaming C#
language: sv
lastmod: 2026-08-19
og_description: Spara HTML som ZIP i C# med Aspose.HTML och en anpassad resurs‑hanterare.
  Denna handledning visar hela koden, förklarar varför varje steg är viktigt och tar
  upp vanliga fallgropar.
og_image_alt: Screenshot of C# code that saves an HTML document as a ZIP archive
og_title: Spara HTML som ZIP med en anpassad resurshanterare i C# – komplett guide
schemas:
- author: Aspose
  dateModified: '2026-08-19'
  description: Save HTML as ZIP in C# using Aspose.HTML and a custom resource handler.
    Follow this step‑by‑step guide to embed resources and generate a portable archive.
  headline: Save HTML as ZIP with a custom resource handler in C#
  type: TechArticle
- description: Save HTML as ZIP in C# using Aspose.HTML and a custom resource handler.
    Follow this step‑by‑step guide to embed resources and generate a portable archive.
  name: Save HTML as ZIP with a custom resource handler in C#
  steps:
  - name: Saving to a specific folder inside the ZIP
    text: 'If you want all resources to reside under a subfolder (e.g., `assets/`),
      modify the handler to prepend the folder name to each file name:'
  - name: Streaming directly to a network location
    text: 'When the ZIP must be sent over HTTP without touching the local file system,
      use a `MemoryStream` for the final archive:'
  - name: Handling large resources
    text: 'Large images or videos can exhaust memory if you keep everything in `MemoryStream`.
      Switch to a file‑based stream inside the handler:'
  - name: Preserving original URLs
    text: 'Aspose.HTML rewrites the `src`/`href` attributes to point to the new locations
      inside the ZIP. If you need to keep the original URLs for later processing,
      capture them before saving:'
  type: HowTo
tags:
- C#
- Aspose.HTML
- ZIP archive
- resource handling
title: Spara HTML som ZIP med en anpassad resurshanterare i C#
url: /sv/net/advanced-features/save-html-as-zip-with-a-custom-resource-handler-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Spara HTML som ZIP med en anpassad resurshanterare i C#

Om du behöver **spara HTML som ZIP** samtidigt som du styr hur länkade resurser lagras, ger den här guiden en komplett lösning. Du kommer att lära dig hur du skapar en anpassad resurshanterare, konfigurerar Aspose.HTML‑s spara‑alternativ och genererar ett portabelt ZIP‑arkiv som innehåller HTML‑filen och dess tillgångar.

Att bädda in resurser på rätt sätt är viktigt när du vill leverera en självständig webbsida, arkivera en rapport för efterlevnad eller cachea en ögonblicksbild för offline‑användning. Stegen nedan fungerar med Aspose.HTML 23.10 eller senare och kräver bara en .NET‑utvecklingsmiljö.

## Vad du kommer att bygga

När du är klar med den här tutorialen har du:

* En C#‑klass som implementerar `ResourceHandler` och returnerar en ström för varje resurs.
* Kod som läser in en befintlig HTML‑fil från disk.
* Konfiguration av `HTMLSaveOptions` för att använda den anpassade hanteraren.
* Ett anrop till `HTMLDocument.Save` som producerar `output.zip`, ett ZIP‑arkiv som innehåller HTML‑dokumentet och alla refererade resurser.

## Förutsättningar

* .NET 6.0 SDK eller senare (exemplet fungerar även på .NET Framework 4.7.2).
* Visual Studio 2022 eller någon IDE som stödjer C#‑projekt.
* Aspose.HTML för .NET NuGet‑paket (`Aspose.Html`).
* En HTML‑fil (`example.html`) med minst en extern resurs (bild, CSS, skript) så att du kan se hanteraren i aktion.

## Steg 1: Skapa en anpassad resurshanterare

Den **anpassade resurshanteraren** bestämmer var varje extern tillgång skrivs. Genom att implementera `ResourceHandler` får du full kontroll över utdata‑strömmen.

```csharp
using Aspose.Html;
using System.IO;

/// <summary>
/// Provides a stream for each resource referenced by the HTML document.
/// </summary>
class MyResourceHandler : ResourceHandler
{
    /// <summary>
    /// Returns a writable stream for the given resource.
    /// </summary>
    /// <param name="resource">Metadata about the resource being saved.</param>
    /// <returns>A stream that Aspose.HTML will write the resource to.</returns>
    public override Stream HandleResource(Resource resource)
    {
        // Create a memory stream for the resource.
        // In production you might write to a file on disk, a cloud blob, or a database.
        return new MemoryStream();
    }
}
```

**Varför detta är viktigt:**  
`HandleResource` anropas för varje extern fil (bilder, stilmallar, skript). Genom att returnera en ny `MemoryStream` låter du Aspose.HTML samla in data i minnet, vilket spar‑rutinen senare packar in i ZIP‑arkivet. Om du vill ha resurserna på disk, ersätt `new MemoryStream()` med `File.Create(Path.Combine(outputFolder, resource.FileName))`.

## Steg 2: Läs in HTML‑dokumentet

Läs in källfilen med `HTMLDocument`. Konstruktorn accepterar en filsökväg, en URL eller en ström.

```csharp
using Aspose.Html;

// Adjust the path to point to your HTML file.
string htmlPath = Path.Combine("YOUR_DIRECTORY", "example.html");

// Load the document into memory.
HTMLDocument doc = new HTMLDocument(htmlPath);
```

**Varför detta är viktigt:**  
Att läsa in dokumentet först säkerställer att Aspose.HTML parsar DOM‑trädet och upptäcker alla länkade resurser. Biblioteket skickar sedan varje upptäckt resurs till den hanterare du definierade i föregående steg.

## Steg 3: Konfigurera spar‑alternativ med den anpassade hanteraren

`HTMLSaveOptions` låter dig ange utdataformatet och resurshanteraren.

```csharp
using Aspose.Html.Saving;

// Create default save options.
HTMLSaveOptions saveOptions = new HTMLSaveOptions();

// Attach the custom resource handler.
saveOptions.ResourceHandler = new MyResourceHandler();
```

**Varför detta är viktigt:**  
Utan att tilldela `ResourceHandler` skriver Aspose.HTML resurser till en temporär mapp på disk, vilket du inte kan styra. Genom att länka din `MyResourceHandler` bestämmer du exakt hur varje resurs lagras innan ZIP‑arkivet skapas.

## Steg 4: Spara dokumentet som ett ZIP‑arkiv

Slutligen anropar du `HTMLDocument.Save` med `SaveFormat.Zip`. Metoden komprimerar HTML‑filen och alla strömmar som levererats av hanteraren.

```csharp
// Define the output ZIP path.
string zipPath = Path.Combine("YOUR_DIRECTORY", "output.zip");

// Save the document as a ZIP archive.
doc.Save(zipPath, SaveFormat.Zip, saveOptions);
```

När anropet är klart innehåller `output.zip`:

* `example.html` – den ursprungliga HTML‑filen med uppdaterade resurslänkar.
* Alla externa tillgångar (bilder, CSS, JS) lagrade som separata poster, var och en skapad av den anpassade hanteraren.

## Verifiera resultatet

Öppna det genererade ZIP‑arkivet med någon arkivvisare. Du bör se en mappstruktur liknande:

```
output.zip
│─ example.html
│─ images/
│   └─ logo.png
│─ styles/
│   └─ main.css
│─ scripts/
│   └─ app.js
```

Öppna `example.html` från den extraherade mappen i en webbläsare; sidan ska renderas exakt som originalet, vilket bekräftar att resurserna har bäddats in korrekt.

## Vanliga variationer och kantfall

### Spara till en specifik mapp i ZIP‑arkivet

Om du vill att alla resurser ska ligga under en undermapp (t.ex. `assets/`), ändra hanteraren så att den lägger till mappnamnet framför varje filnamn:

```csharp
public override Stream HandleResource(Resource resource)
{
    string folder = "assets";
    string entryName = Path.Combine(folder, resource.FileName);
    // Aspose.HTML uses the entry name when packing the ZIP.
    resource.FileName = entryName;
    return new MemoryStream();
}
```

### Strömma direkt till en nätverksplats

När ZIP‑filen måste skickas över HTTP utan att röra den lokala filsystemet, använd en `MemoryStream` för det slutgiltiga arkivet:

```csharp
using (var zipStream = new MemoryStream())
{
    doc.Save(zipStream, SaveFormat.Zip, saveOptions);
    zipStream.Position = 0; // Reset for reading.
    // Send zipStream to a web API, store in Azure Blob, etc.
}
```

### Hantera stora resurser

Stora bilder eller videor kan tömma minnet om du behåller allt i `MemoryStream`. Byt till en fil‑baserad ström i hanteraren:

```csharp
public override Stream HandleResource(Resource resource)
{
    string tempPath = Path.GetTempFileName();
    return new FileStream(tempPath, FileMode.Create, FileAccess.Write);
}
```

Efter att `doc.Save` är klar kan du radera de temporära filerna.

### Bevara ursprungliga URL:er

Aspose.HTML skriver om `src`/`href`‑attributen så att de pekar på de nya platserna i ZIP‑arkivet. Om du behöver behålla de ursprungliga URL:erna för senare bearbetning, fånga dem innan du sparar:

```csharp
foreach (var img in doc.Images)
{
    Console.WriteLine($"Original src: {img.Source}");
}
```

## Pro‑tips

* **Återanvänd hanteraren** – Skapa en enda instans av `MyResourceHandler` och återanvänd den över flera spar‑operationer för att undvika upprepade allokeringar.
* **Validera resurser** – Inuti `HandleResource` kan du inspektera `resource.MimeType` eller `resource.FileName` för att filtrera bort oönskade filer (t.ex. hoppa över analys‑skript).
* **Ställ in komprimeringsnivå** – `HTMLSaveOptions` exponerar `CompressionLevel` (0–9). Högre värden ger mindre ZIP‑filer på bekostnad av CPU‑tid.

## Fullt, körbart exempel

Nedan är det kompletta programmet som du kan kopiera in i ett nytt konsolprojekt (`dotnet new console`). Det demonstrerar varje steg från att läsa in HTML‑filen till att producera `output.zip`.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Saving;

class MyResourceHandler : ResourceHandler
{
    public override Stream HandleResource(Resource resource)
    {
        // Return a memory stream for each resource.
        // Replace with FileStream if you need disk persistence.
        return new MemoryStream();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Define paths.
        string baseDir = Path.Combine(Environment.CurrentDirectory, "YOUR_DIRECTORY");
        string htmlPath = Path.Combine(baseDir, "example.html");
        string zipPath = Path.Combine(baseDir, "output.zip");

        // 2️⃣ Load the HTML document.
        HTMLDocument doc = new HTMLDocument(htmlPath);

        // 3️⃣ Configure save options with the custom handler.
        HTMLSaveOptions saveOptions = new HTMLSaveOptions
        {
            ResourceHandler = new MyResourceHandler()
        };

        // 4️⃣ Save as a ZIP archive.
        doc.Save(zipPath, SaveFormat.Zip, saveOptions);

        Console.WriteLine($"HTML saved as ZIP at: {zipPath}");
    }
}
```

**Förväntad utdata**

```
HTML saved as ZIP at: C:\path\to\YOUR_DIRECTORY\output.zip
```

Extrahera ZIP‑filen för att verifiera strukturen som beskrivits tidigare.

## Slutsats

Du vet nu hur du **sparar HTML som ZIP** med Aspose.HTML för .NET samtidigt som du utnyttjar en **anpassad resurshanterare** för att styra var varje tillgång skrivs. Detta tillvägagångssätt ger dig full flexibilitet över resurslagring, möjliggör bearbetning i minnet och integreras enkelt med moln‑ eller lokala arbetsflöden.

Härifrån kan du:

* Utöka hanteraren för att skriva resurser till Azure Blob Storage (sekundärt nyckelord: custom resource handler).
* Kombinera ZIP‑filen med en digital signatur för säker dokumentleverans.
* Använda `HTMLSaveOptions` för att generera andra format (t.ex. MHTML) samtidigt som du hanterar resurser programatiskt.

Experimentera med olika strömtyper, komprimeringsnivåer och mappstrukturer för att passa ditt projekts krav. Lycka till med kodandet!


## Vad bör du lära dig härnäst?


Följande tutorials täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Custom Resource Handler in C# – Convert HTML to ZIP Tutorial](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [How to Render HTML – Complete Guide with Custom Resource Handler](/html/english/net/rendering-html-documents/how-to-render-html-complete-guide-with-custom-resource-handl/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
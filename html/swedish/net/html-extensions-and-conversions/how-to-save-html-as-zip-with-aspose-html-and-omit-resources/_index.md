---
category: general
date: 2026-10-21
description: Lär dig hur du sparar HTML som ZIP med Aspose.HTML, konverterar HTML
  till ZIP och tar bort resurser för ett rent paket.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save html as zip
- convert html to zip
- how to omit resources
- how to strip resources
- create html zip
language: sv
lastmod: 2026-10-21
og_description: Spara HTML som ZIP med Aspose.HTML, lär dig hur du konverterar HTML
  till ZIP och tar bort resurser för ett lättviktigt arkiv.
og_image_alt: Screenshot showing the save html as zip process with resources omitted
og_title: Spara HTML som ZIP med Aspose.HTML – utelämna resurser i ett steg
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
title: Hur man sparar HTML som ZIP med Aspose.HTML och utesluter resurser
url: /sv/net/html-extensions-and-conversions/how-to-save-html-as-zip-with-aspose-html-and-omit-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man sparar HTML som ZIP med Aspose.HTML och utesluter resurser

Om du behöver **spara HTML som ZIP** samtidigt som du tar bort externa filer, visar den här guiden en komplett, färdig‑att‑köra‑lösning. I slutet av handledningen kommer du att kunna **konvertera HTML till ZIP**, kontrollera vilka resurser som behålls och skapa ett rent arkiv som bara innehåller den grundläggande markupen.

Många web‑automatiseringsscenarier kräver att en sida paketeras för offline‑användning, e‑postbilaga eller arkiveringslagring. Att inkludera bilder, typsnitt eller skript ökar ofta arkivet onödigt mycket. Stegen nedan förklarar **hur man utesluter resurser** och **hur man tar bort resurser** från resultatet, så att den färdiga ZIP‑filen förblir lättviktig.

## Förutsättningar

- .NET 6.0 eller senare installerat  
- En Aspose.HTML för .NET-licens (eller en gratis utvärdering)  
- En grundläggande C#-utvecklingsmiljö (Visual Studio, VS Code eller Rider)  

Inga ytterligare NuGet‑paket krävs utöver `Aspose.Html`.

## Steg 1: Skapa en anpassad resurs‑hanterare

Kärnan i **hur man utesluter resurser** ligger i en subklass av `ResourceHandler`. Aspose.HTML anropar denna hanterare för varje extern tillgång (bilder, CSS, skript). Genom att returnera en tom ström talar du i praktiken om konverteraren att hoppa över tillgången.

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

**Varför detta är viktigt:** Standardbeteendet kopierar varje länkat fil till ZIP‑filen, vilket kan dubbla eller tredubbla filstorleken. Genom att åsidosätta `HandleResource` får du fin‑granulär kontroll utan att ändra den ursprungliga HTML‑koden.

## Steg 2: Läs in HTML‑dokumentet

Läs in källfilen med `HTMLDocument`. Konstruktorn accepterar en filsökväg, en URL eller en ström. I det här exemplet läser vi en lokal fil som heter `input.html`.

```csharp
// Load the source HTML file from the local file system.
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

Om din HTML finns i minnet eller kommer från en webbförfrågan kan du istället skicka en `MemoryStream` eller en URL‑sträng. API‑et fungerar på samma sätt.

## Steg 3: Konfigurera sparalternativen

Skapa en instans av `HtmlSaveOptions` och tilldela den anpassade hanteraren som skapades i Steg 1. Detta instruerar Aspose.HTML att använda hanteraren när den stöter på en resurs.

```csharp
// Prepare save options and attach the custom resource handler.
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // The ResourceHandler property is what enables resource stripping.
    ResourceHandler = new CustomResourceHandler()
};
```

Du kan också justera andra alternativ här, till exempel `CompressImages = false` om du vill behålla bilddata men ändå utesluta andra tillgångar. Exemplet behåller standardinställningarna för komprimering.

## Steg 4: Spara dokumentet som ett ZIP‑arkiv

Slutligen anropar du `Save` med mål‑sökvägen och de konfigurerade alternativen. Utdatafilen blir en `.zip` som innehåller `index.html` (eller det ursprungliga filnamnet) och **inga externa resurser**.

```csharp
// Save the HTML document as a ZIP file. The archive will contain only the HTML markup.
document.Save("YOUR_DIRECTORY/output.zip", saveOptions);
```

### Förväntat resultat

- `output.zip` → innehåller en enda `index.html`‑fil.  
- Alla bilder, CSS‑filer och JavaScript‑referenser är uteslutna, eftersom den anpassade hanteraren returnerade en tom ström för varje.  

Du kan verifiera arkivet genom att öppna det med någon ZIP‑visare. HTML‑sidan kommer fortfarande att referera till de ursprungliga URL‑erna, men dessa filer finns inte i arkivet, vilket håller paketet minimalt.

## Fullt, körbart exempel

Nedan är det kompletta programmet som du kan kopiera, klistra in och köra. Ersätt `YOUR_DIRECTORY` med en faktisk mapp‑sökväg på din maskin.

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

När du kör detta program skapas ZIP‑filen som beskrivits tidigare. Du kan nu distribuera HTML‑sidan utan att paketera onödiga tillgångar.

## Vanliga varianter och kantfall

| Scenario | Adjustment |
|----------|------------|
| **Behåll bilder men ta bort CSS/JS** | I `CustomResourceHandler`, inspektera `info.MimeType`. Returnera en `MemoryStream` endast för `text/css` och `application/javascript`. |
| **Bevara externa typsnitt** | Returnera den ursprungliga strömmen för MIME‑typerna `font/woff2`, annars returnera en tom ström. |
| **Generera en ZIP med ett anpassat postnamn** | Använd `HtmlSaveOptions`‑överladdning `Save(string path, SaveOptions options, string entryName)` för att ange ett annat rotfilnamn. |
| **Konvertera flera HTML‑filer till en enda ZIP** | Loopa över varje fil, skapa ett separat `HTMLDocument` och lägg till varje i samma `ZipArchive` manuellt med `System.IO.Compression`. |

Dessa varianter illustrerar **hur man tar bort resurser** selektivt, vilket ger dig full kontroll över den slutliga arkivstorleken.

## Pro‑tips

- **Validera resultatet**: Efter sparandet, öppna ZIP‑filen och ladda `index.html` i en webbläsare. Saknade resurser visas som brutna länkar, vilket bekräftar att hanteraren fungerade.  
- **Prestanda**: Att returnera en tom `MemoryStream` är billigt, men om du har tusentals tillgångar bör du överväga att cache‑a beslutet (t.ex. en `HashSet<string>` med MIME‑typer att hoppa över).  
- **Licensiering**: Den fria utvärderingsversionen av Aspose.HTML lägger till en vattenstämpel‑kommentar i HTML‑koden. Distribuera en licensierad version för att ta bort den i produktionsmiljö.

## Slutsats

Du vet nu hur man **sparar HTML som ZIP**, **konverterar HTML till ZIP** och **tar bort resurser** med Aspose.HTML för .NET. Genom att implementera en anpassad `ResourceHandler` kan du utesluta oönskade filer och hålla arkivet lättviktigt. Experimentera med hanterarlogiken för att behålla endast de resurser du verkligen behöver, och integrera detta mönster i större automations‑pipelines.

---

**Nästa steg**

- Utforska andra `HtmlSaveOptions`‑funktioner som `EmbedImages` för att bädda in bilder direkt i HTML.  
- Kombinera detta tillvägagångssätt med `Aspose.PDF` för att konvertera samma HTML till en PDF efter att ZIP‑filen skapats.  
- Titta på server‑sidiga scenarier där du genererar ZIP‑filen på begäran och strömmar den till en klient utan att skriva till disk.  

Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man använder ZipArchive – Spara HTML och resurser till en ZIP‑fil](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [Hur man sparar HTML i C# – Anpassade resurs‑hanterare & ZIP](/html/english/net/working-with-html-documents/how-to-save-html-in-c-custom-resource-handlers-zip/)
- [Hur man sparar HTML som ZIP i C# – Komplett Aspose.HTML‑guide](/html/english/net/html-extensions-and-conversions/how-to-save-html-as-zip-in-c-complete-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
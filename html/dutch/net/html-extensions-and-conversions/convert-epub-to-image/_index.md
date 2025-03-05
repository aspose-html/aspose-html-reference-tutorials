---
title: Converteer EPUB naar afbeelding in .NET met Aspose.HTML
linktitle: EPUB naar afbeelding converteren in .NET
second_title: Aspose.HTML .NET HTML-manipulatie-API
description: Leer hoe u EPUB naar afbeeldingen converteert met Aspose.HTML voor .NET. Stapsgewijze tutorial met codevoorbeelden en aanpasbare opties.
type: docs
weight: 11
url: /nl/net/html-extensions-and-conversions/convert-epub-to-image/
---

In het digitale tijdperk van vandaag is het vermogen om verschillende documentformaten te manipuleren en converteren een waardevolle vaardigheid. Aspose.HTML voor .NET is een krachtige tool waarmee ontwikkelaars moeiteloos met HTML- en EPUB-documenten kunnen werken. In deze tutorial duiken we in de wereld van Aspose.HTML voor .NET en begeleiden we u door het proces van het converteren van EPUB-documenten naar verschillende afbeeldingsformaten. We splitsen elk voorbeeld op in meerdere stappen en leggen elke stap uit.

## Vereisten

Voordat we in de wereld van Aspose.HTML voor .NET duiken, moet u ervoor zorgen dat u aan de volgende vereisten voldoet:

1. Visual Studio: Zorg ervoor dat Visual Studio op uw systeem is geïnstalleerd. U kunt het downloaden van de website.

2.  Aspose.HTML voor .NET: U kunt de bibliotheek verkrijgen via de Aspose-website[hier](https://releases.aspose.com/html/net/).

3. Uw gegevensmap: Maak een map aan waar u uw EPUB-bestanden opslaat en waar de uitvoerafbeeldingen worden opgeslagen.

4. Basiskennis van C#: Kennis van C#-programmering is essentieel om de codevoorbeelden in deze tutorial te begrijpen en te implementeren.

## Noodzakelijke naamruimten importeren

Voordat we beginnen met Aspose.HTML voor .NET, moet u de vereiste namespaces importeren in uw C#-code. Deze namespaces bieden toegang tot de Aspose.HTML voor .NET-functies.

```csharp
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using Aspose.Html.Rendering.Image;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
using System.IO;
using System.Drawing;
using System.Collections.Generic;
```

Nu de vereisten en naamruimten op hun plaats staan, gaan we verder met de stapsgewijze voorbeelden.

## EPUB naar JPEG converteren

```csharp
    string dataDir = "Your Data Directory";
    // Open een bestaand EPUB-bestand om te lezen.
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        // Roep de ConvertEPUB-methode aan om het EPUB-bestand naar een afbeelding te converteren.
        Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), "output.jpg");
    }
```
### Stappen

1. Geef het pad naar uw EPUB-bestand op in de variabele dataDir.
2. Open het EPUB-bestand om het te lezen met behulp van een FileStream.
3. Roep de ConvertEPUB-methode aan en geef de EPUB-stream door, een ImageSaveOptions met de uitvoerindeling (JPEG) en de naam van het uitvoerbestand ("output.jpg").
5. Het EPUB-bestand wordt geconverteerd naar een JPEG-afbeelding.

In dit voorbeeld openen we een EPUB-bestand, lezen de inhoud en converteren het naar een JPEG-afbeeldingsformaat. De uitvoerafbeelding wordt opgeslagen als "output.jpg."

## EPUB naar PNG converteren

U kunt EPUB-bestanden eenvoudig converteren naar verschillende afbeeldingsformaten zoals PNG, BMP, GIF en TIFF met behulp van vergelijkbare codestructuren. Hier is een voorbeeld voor het converteren naar PNG:

```csharp

    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Png);
        Converter.ConvertEPUB(stream, options, "output.png");
    }

```
### Stappen
1. Open het EPUB-bestand om het te lezen met behulp van een FileStream.
2. Initialiseer een ImageSaveOptions-object met de gewenste uitvoerindeling (in dit geval PNG).
3. Roep de ConvertEPUB-methode aan en geef de EPUB-stream, de opties voor het opslaan van de afbeelding en de naam van het uitvoerbestand door.
4. Het EPUB-bestand wordt geconverteerd naar het opgegeven afbeeldingsformaat.

## Geef opties voor het opslaan van afbeeldingen op

U kunt de afbeeldingsuitvoer aanpassen door opties op te geven zoals paginaformaat en achtergrondkleur. Hier is een voorbeeld:

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Jpeg)
        {
            PageSetup =
            {
                AnyPage = new Page()
                {
                    Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
                }
            },
            BackgroundColor = Color.AliceBlue,
        };
        Converter.ConvertEPUB(stream, options, "output.jpg");
    }
```
### Stappen

1.  Geef het pad naar uw EPUB-bestand op in de`dataDir` variabel.
2.  Open het EPUB-bestand om te lezen met behulp van een`FileStream`.
3.  Maak een`ImageSaveOptions` object en geef het gewenste uitvoerformaat (JPEG) op.
4. Pas indien nodig het paginaformaat en de achtergrondkleur aan.
5.  Bel de`ConvertEPUB`methode, waarbij de EPUB-stream, de opties voor het opslaan van de afbeelding en de naam van het uitvoerbestand worden doorgegeven.
6. Het EPUB-bestand wordt geconverteerd naar een afbeelding met de opgegeven opties.

## Geef een aangepaste streamprovider op

Als u de uitvoerstream moet manipuleren, kunt u een aangepaste streamprovider gebruiken. Hier is een voorbeeld:

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        using (var streamProvider = new MemoryStreamProvider())
        {
            Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), streamProvider);
            
            for (int i = 0; i < streamProvider.Streams.Count; i++)
            {
                var memory = streamProvider.Streams[i];
                memory.Seek(0, SeekOrigin.Begin);
                
                using (FileStream fs = File.Create($"page_{i + 1}.jpg"))
                {
                    memory.CopyTo(fs);
                }
            }
        }
    }

```
Broncode van de klasse MemoryStreamProvider.

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // Lijst met MemoryStream-objecten die zijn gemaakt tijdens het renderen van het document
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // Deze methode wordt aangeroepen wanneer er maar één uitvoerstroom nodig is, bijvoorbeeld voor XPS-, PDF- of TIFF-indelingen.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // Deze methode wordt aangeroepen wanneer de creatie van meerdere output streams vereist is. Bijvoorbeeld tijdens het renderen van HTML naar een lijst met afbeeldingsbestanden (JPG, PNG, etc.)
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // Hier kunt u de met data gevulde stream vrijgeven en bijvoorbeeld naar de harde schijf spoelen
            }
            public void Dispose()
            {
                // Vrijgeven van hulpbronnen
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```

### Stappen
1.  Geef het pad naar uw EPUB-bestand op in de`dataDir` variabel.
2.  Open het EPUB-bestand om te lezen met behulp van een`FileStream`.
3.  Maak een`MemoryStreamProvider` om aangepaste uitvoerstromen te verwerken.
4.  Bel de`ConvertEPUB` methode, waarbij de EPUB-stream, de opties voor het opslaan van de afbeelding (JPEG) en de aangepaste streamprovider worden doorgegeven.
5. Doorloop de geheugenstromen in de aangepaste provider en sla ze op in afzonderlijke bestanden.
6. Met dit voorbeeld kunt u indien nodig meerdere uitvoerstromen bewerken en opslaan.

## Conclusie

Aspose.HTML voor .NET is een veelzijdige bibliotheek die het werken met EPUB- en HTML-documenten vereenvoudigt. Met de mogelijkheid om EPUB-documenten te converteren naar verschillende afbeeldingsformaten en aanpasbare opties, biedt het een breed scala aan toepassingen voor ontwikkelaars.

---

## Veelgestelde vragen

### 1. Waar kan ik Aspose.HTML voor .NET downloaden?

 U kunt Aspose.HTML voor .NET downloaden van de releasepagina[hier](https://releases.aspose.com/html/net/).

### 2. Hoe kan ik een tijdelijke licentie voor Aspose.HTML voor .NET krijgen?

 Om een tijdelijke licentie te verkrijgen, gaat u naar de pagina tijdelijke licentie[hier](https://purchase.aspose.com/temporary-license/).

### 3. Waar kan ik aanvullende ondersteuning vinden voor Aspose.HTML voor .NET?

 Voor vragen of problemen kunt u hulp krijgen van de Aspose-community op het ondersteuningsforum[hier](https://forum.aspose.com/).

### 4. Kan ik EPUB-documenten converteren naar andere formaten zoals PDF of XPS?

Ja, u kunt Aspose.HTML voor .NET gebruiken om EPUB-documenten te converteren naar verschillende formaten, waaronder PDF en XPS.

### 5. Is Aspose.HTML voor .NET geschikt voor zowel kleine als grote projecten?

Absoluut! Aspose.HTML voor .NET is ontworpen om schaalbaar te zijn, waardoor het een geweldige keuze is voor projecten van alle groottes.

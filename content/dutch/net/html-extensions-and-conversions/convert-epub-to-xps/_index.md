---
title: Converteer EPUB naar XPS in .NET met Aspose.HTML
linktitle: EPUB naar XPS converteren in .NET
second_title: Aspose.HTML .NET HTML-manipulatie-API
description: Leer hoe u EPUB naar XPS converteert in .NET met Aspose.HTML voor .NET. Volg onze stapsgewijze handleiding voor moeiteloze conversies.
type: docs
weight: 13
url: /nl/net/html-extensions-and-conversions/convert-epub-to-xps/
---

Bent u op zoek naar een naadloze manier om EPUB-bestanden naar XPS-formaat te converteren in uw .NET-toepassingen? Aspose.HTML voor .NET biedt een krachtige oplossing om dit moeiteloos te bereiken. In deze stapsgewijze handleiding leiden we u door het proces van het converteren van EPUB naar XPS met behulp van Aspose.HTML. Laten we beginnen!

## Vereisten

Voordat u met de conversie van EPUB naar XPS begint, moet u ervoor zorgen dat aan de volgende vereisten is voldaan:

### 1. Aspose.HTML voor .NET-bibliotheek

 Zorg ervoor dat u de Aspose.HTML voor .NET-bibliotheek in uw project hebt geïnstalleerd. Als u dat nog niet hebt gedaan, kunt u deze verkrijgen via de[Aspose.HTML voor .NET Downloadpagina](https://releases.aspose.com/html/net/).

### 2. Invoer EPUB-bestand

U hebt een EPUB-bestand nodig dat u wilt converteren naar XPS. Zorg ervoor dat u een EPUB-bestand beschikbaar hebt voor conversie.

### 3. .NET-ontwikkelomgeving

In deze handleiding gaan we ervan uit dat u een werkende .NET-ontwikkelomgeving op uw computer hebt ingesteld.

## Naamruimte importeren

Om te beginnen moet u de benodigde naamruimte voor Aspose.HTML importeren:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## EPUB naar XPS converteren

Laten we het proces van het converteren van een EPUB-bestand naar XPS-formaat opsplitsen in meerdere stappen.

### Stap 1.1: Open het EPUB-bestand

Open eerst het bestaande EPUB-bestand om het te lezen met behulp van een FileStream:

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Ga door met het conversieproces
}
```

### Stap 1.2: XpsSaveOptions maken

Maak een instantie van XpsSaveOptions. Deze stap is cruciaal voor het configureren van de XPS-uitvoer:

```csharp
var options = new XpsSaveOptions();
```

### Stap 1.3: EPUB naar XPS converteren

Laten we nu de ConvertEPUB-methode aanroepen om EPUB naar XPS te converteren:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Aangepaste XPS-opties opgeven

U kunt de XPS-uitvoer verder aanpassen door aangepaste opties op te geven, zoals paginaformaat en achtergrondkleur.

### Stap 2.1: Aangepaste paginagrootte en achtergrondkleur

Maak een exemplaar van XpsSaveOptions met aangepaste paginagrootte en achtergrondkleur:

```csharp
var options = new XpsSaveOptions()
{
    PageSetup =
    {
        AnyPage = new Page()
        {
            Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
        }
    },
    BackgroundColor = System.Drawing.Color.AliceBlue,
};
```

### Stap 2.2: EPUB naar XPS converteren met aangepaste opties

Roep nu de ConvertEPUB-methode aan om de EPUB naar XPS te converteren met de aangepaste opties:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Gebruik aangepaste streamprovider

In deze stap converteren we EPUB naar XPS met behulp van een aangepaste streamprovider, zodat u de resulterende gegevens kunt bewerken.

### Stap 3.1: Een MemoryStreamProvider maken

Maak een instantie van MemoryStreamProvider:

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    // Ga door met het conversieproces
}
```

### Stap 3.2: EPUB naar XPS converteren met Stream Provider

Converteer EPUB naar XPS met behulp van MemoryStreamProvider:

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### Stap 3.3: Toegang tot en opslaan van resultaat

Haal de geheugenstroom op die de geconverteerde gegevens bevat en sla deze op in een uitvoerbestand:

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

### Broncode van klasse MemoryStreamProvider

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
Gefeliciteerd! U hebt met succes een EPUB-bestand geconverteerd naar XPS-formaat met behulp van Aspose.HTML voor .NET.

## Conclusie

In deze uitgebreide tutorial hebben we onderzocht hoe je Aspose.HTML voor .NET kunt gebruiken om EPUB-bestanden te converteren naar XPS-formaat met verschillende aanpassingsopties. Of je nu een doorgewinterde ontwikkelaar bent of net begint, Aspose.HTML vereenvoudigt het proces, zodat je EPUB-naar-XPS-conversies eenvoudig kunt verwerken.

 Heeft u vragen of problemen? Bekijk de[Aspose.HTML-documentatie](https://reference.aspose.com/html/net/) voor meer inzicht of zoek hulp bij de[Aspose.HTML Communityforum](https://forum.aspose.com/).

## Veelgestelde vragen

### Wat is Aspose.HTML voor .NET?
Aspose.HTML voor .NET is een krachtige bibliotheek waarmee ontwikkelaars met HTML-, EPUB- en XPS-documenten in .NET-toepassingen kunnen werken.

### Waar kan ik Aspose.HTML voor .NET downloaden?
 U kunt Aspose.HTML voor .NET downloaden van de[downloadpagina](https://releases.aspose.com/html/net/).

### Is er een gratis proefversie beschikbaar voor Aspose.HTML voor .NET?
 Ja, u kunt een gratis proefversie krijgen van[hier](https://releases.aspose.com/).

### Hoe kan ik een tijdelijke licentie voor Aspose.HTML voor .NET verkrijgen?
 Om een tijdelijke licentie te krijgen, gaat u naar de[tijdelijke licentiepagina](https://purchase.aspose.com/temporary-license/).

### Waar kan ik meer tutorials en documentatie vinden voor Aspose.HTML voor .NET?
 Ontdek een breed scala aan tutorials en gedetailleerde documentatie over de[Aspose.HTML-documentatie](https://reference.aspose.com/html/net/) pagina.
---
title: Converteer EPUB naar PDF in .NET met Aspose.HTML
linktitle: EPUB naar PDF converteren in .NET
second_title: Aspose.HTML .NET HTML-manipulatie-API
description: Leer hoe u EPUB naar PDF converteert met Aspose.HTML voor .NET. Deze stapsgewijze handleiding behandelt aanpassingsopties, veelgestelde vragen en meer voor naadloze documentconversie.
type: docs
weight: 12
url: /nl/net/html-extensions-and-conversions/convert-epub-to-pdf/
---

In deze tutorial gaan we onderzoeken hoe je Aspose.HTML voor .NET kunt gebruiken om EPUB-bestanden naar PDF te converteren. Aspose.HTML is een krachtige .NET-bibliotheek die verschillende functionaliteiten biedt voor het werken met HTML- en EPUB-documenten. We behandelen de vereisten, importeren de benodigde naamruimten en geven meerdere voorbeelden, waarbij we elke stap gedetailleerd uitleggen.

## Vereisten

Voordat u begint, moet u ervoor zorgen dat aan de volgende voorwaarden is voldaan:

1. Aspose.HTML voor .NET: Zorg ervoor dat u Aspose.HTML voor .NET in uw .NET-project hebt geïnstalleerd. U kunt het downloaden van[hier](https://releases.aspose.com/html/net/).

2. Uw gegevensmap: U hebt een gegevensmap nodig waarin uw EPUB-bestanden zijn opgeslagen.

Laten we nu eens kijken naar het stapsgewijze proces voor het converteren van EPUB naar PDF met behulp van Aspose.HTML voor .NET.

## EPUB naar PDF converteren

### Stap 1: Initialiseer uw project

Zorg ervoor dat u een .NET-project hebt ingesteld en dat Aspose.HTML voor .NET is geïnstalleerd.

### Stap 2: Importeer vereiste naamruimten

Importeer de benodigde naamruimten in uw C#-codebestand:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
```

### Stap 3: Open het EPUB-bestand

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Ga door naar de volgende stap...
}
```

-  Vervangen`"Your Data Directory"` met de werkelijke map waar uw EPUB-bestand zich bevindt.
- Met deze code wordt het EPUB-bestand geopend, zodat u het kunt lezen.

### Stap 4: PDF-opties instellen en conversie uitvoeren

```csharp
var options = new PdfSaveOptions();
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Maak een exemplaar van`PdfSaveOptions` om PDF-conversie-instellingen op te geven.
-  Gebruik de`Converter.ConvertEPUB` Methode om EPUB naar PDF te converteren met de gegeven opties.
- Sla het resulterende PDF-bestand op als "output.pdf."

## Geef PDF-opslagopties op

### Stap 1: Initialiseer uw project

Zorg ervoor dat u een .NET-project hebt ingesteld en dat Aspose.HTML voor .NET is geïnstalleerd.

### Stap 2: Importeer vereiste naamruimten

Importeer de benodigde naamruimten in uw C#-code:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
```

### Stap 3: Open het EPUB-bestand

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Ga door naar de volgende stap...
}
```

-  Vervangen`"Your Data Directory"` met de werkelijke map van uw EPUB-bestand.
- Open het EPUB-bestand om te lezen.

### Stap 4: PDF-opties aanpassen

```csharp
var options = new PdfSaveOptions()
{
    PageSetup = { AnyPage = new Page() { Size = Size.FromPixels(3000, 1000) } },
    BackgroundColor = System.Drawing.Color.AliceBlue
};
```

-  Maak een exemplaar van`PdfSaveOptions` en pas het aan uw wensen aan.
- In dit voorbeeld stellen we de paginagrootte in op 3000 pixels breed en 1000 pixels hoog, en de achtergrondkleur op Alice Blue.

### Stap 5: Conversie uitvoeren

```csharp
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Gebruik de`Converter.ConvertEPUB` Methode om EPUB naar PDF te converteren met de aangepaste opties.
- Sla het resulterende PDF-bestand op als "output.pdf."

## Gebruik aangepaste streamprovider

### Stap 1: Initialiseer uw project

Stel een .NET-project in en installeer Aspose.HTML voor .NET.

### Stap 2: Importeer vereiste naamruimten

Importeer de benodigde naamruimten in uw C#-code:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
```

### Stap 3: Open het EPUB-bestand

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Ga door naar de volgende stap...
}
```

-  Vervangen`"Your Data Directory"` met de werkelijke map van uw EPUB-bestand.
- Open het EPUB-bestand om te lezen.

### Stap 4: Gebruik een aangepaste streamprovider

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    Converter.ConvertEPUB(stream, new PdfSaveOptions(), streamProvider);

    // Ga door naar de volgende stap...
}
```

-  Maak een`MemoryStreamProvider` om het conversieresultaat te beheren als een geheugenstroom.
-  Gebruik de`Converter.ConvertEPUB` methode met de aangepaste streamprovider.

### Stap 5: Sla het resultaat op

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.pdf"))
{
    memory.CopyTo(fs);
}
```

- Krijg toegang tot de geheugenstroom met de geconverteerde gegevens.
- Stel de streampositie in op het begin.
- Maak een PDF-uitvoerbestand en kopieer de inhoud van de geheugenstroom ernaartoe.

### Broncode van klasse MemoryStreamProvider. 

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
Nu hebt u geleerd hoe u EPUB-bestanden naar PDF kunt converteren met Aspose.HTML voor .NET met verschillende opties en aanpassingsmogelijkheden. Aspose.HTML vereenvoudigt het proces en biedt flexibiliteit en controle over uw documentconversie.

## Conclusie

Aspose.HTML voor .NET is een veelzijdige tool voor het converteren van EPUB-bestanden naar PDF, met aanpassingsopties om het resulterende PDF-document aan te passen aan uw behoeften. Of u nu eenvoudige conversies of geavanceerde aanpassingen nodig hebt, Aspose.HTML heeft het voor u.

 Als u dat nog niet hebt gedaan, kunt u Aspose.HTML voor .NET downloaden van de[website](https://releases.aspose.com/html/net/) en begin het vandaag nog te gebruiken in uw .NET-toepassingen.

---

## Veelgestelde vragen

### Is Aspose.HTML voor .NET gratis te gebruiken?
    Aspose.HTML voor .NET is een commercieel product, maar er is een gratis proefversie beschikbaar[hier](https://releases.aspose.com/).

### Kan ik het uiterlijk van de geconverteerde PDF aanpassen?
   Ja, u kunt het uiterlijk van het PDF-bestand aanpassen door opties als paginaformaat en achtergrondkleur aan te passen, zoals weergegeven in voorbeeld 2.

### Hoe kan ik ondersteuning krijgen voor Aspose.HTML voor .NET?
    Ondersteuning en hulpmiddelen vindt u op de[Aspose.HTML-forum](https://forum.aspose.com/).

### Zijn er andere formaten die ik met Aspose.HTML voor .NET kan converteren?
   Ja, Aspose.HTML voor .NET ondersteunt verschillende documentformaten, waaronder HTML, EPUB en meer.

### Is Aspose.HTML voor ..NET geschikt voor grootschalige documentconversie?
   Aspose.HTML voor .NET is ontworpen om grootschalige documentconversies efficiënt af te handelen en is daardoor geschikt voor een breed scala aan toepassingen.


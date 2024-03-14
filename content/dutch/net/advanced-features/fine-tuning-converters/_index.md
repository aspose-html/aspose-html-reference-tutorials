---
title: Converters verfijnen in .NET met Aspose.HTML
linktitle: Conversieprogramma's verfijnen in .NET
second_title: Aspose.HTML .NET HTML-manipulatie-API
description: Leer hoe u HTML naar PDF, XPS en afbeeldingen converteert met Aspose.HTML voor .NET. Stapsgewijze zelfstudie met codevoorbeelden en veelgestelde vragen.
type: docs
weight: 16
url: /nl/net/advanced-features/fine-tuning-converters/
---

## Invoering

Aspose.HTML voor .NET is een krachtige bibliotheek waarmee ontwikkelaars HTML-documenten in verschillende formaten kunnen manipuleren en converteren. Of u nu HTML naar PDF, XPS of afbeeldingen moet converteren of andere HTML-gerelateerde taken moet uitvoeren, Aspose.HTML biedt een robuuste set hulpmiddelen om u te helpen de klus te klaren.

In deze zelfstudie verkennen we enkele essentiële functies van Aspose.HTML voor .NET en geven we stapsgewijze uitleg voor elk voorbeeld. Aan het einde van deze zelfstudie heeft u een goed begrip van het gebruik van Aspose.HTML voor .NET in uw .NET-toepassingen.

## Vereisten

Voordat we in de voorbeelden duiken, moet u ervoor zorgen dat u aan de volgende vereisten voldoet:

-  Aspose.HTML voor .NET: De bibliotheek Aspose.HTML voor .NET moet geïnstalleerd zijn. Je kunt het downloaden van de[download link](https://releases.aspose.com/html/net/).

- Tijdelijke licentie (optioneel): Als u niet over een geldige licentie beschikt, kunt u een tijdelijke licentie verkrijgen bij[hier](https://purchase.aspose.com/temporary-license/).

Laten we nu enkele veelvoorkomende gebruiksscenario's bekijken met Aspose.HTML voor .NET.

## Naamruimten importeren

Begin in uw C#-code met het importeren van de benodigde naamruimten:

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Pdf;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Xps;
using Aspose.Html.Rendering.Pdf.Encryption;
using Aspose.Html.Drawing;
```

## Converteer HTML naar PDF

### Stap 1: HTML-code voorbereiden

```csharp
var code = @"<span>Hello World!!</span>";
```

### Stap 2: Initialiseer het HTML-document

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Stap 3: Maak een PDF-apparaat en geef het uitvoerbestand op

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Stap 4: HTML naar PDF renderen

```csharp
document.RenderTo(device);
```

In dit voorbeeld wordt een HTML-fragment omgezet in een PDF-document. U kunt de HTML-code en het uitvoerbestand indien nodig aanpassen.

## Stel aangepast paginaformaat in

### Stap 1: HTML-code voorbereiden

```csharp
var code = @"<span>Hello World!!</span>";
```

### Stap 2: Initialiseer het HTML-document

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Stap 3: Maak PDF-weergaveopties

```csharp
var options = new PdfRenderingOptions()
{
    PageSetup =
    {
        AnyPage = new Page(
            new Size(
                Length.FromInches(5),
                Length.FromInches(2)))
    }
};
```

### Stap 4: Maak een PDF-apparaat en geef opties en uitvoerbestand op

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Stap 5: HTML naar PDF renderen

```csharp
document.RenderTo(device);
```

Dit voorbeeld laat zien hoe u een aangepast paginaformaat instelt voor het resulterende PDF-document.

## Resolutie aanpassen

### Stap 1: HTML-code voorbereiden en opslaan in bestand

```csharp
var code = @"
    <style>
    p
    { 
        background: blue; 
    }
    @media(min-resolution: 300dpi)
    {
        p 
        { 
            /* high-resolution screen color */
            background: green
        }
    }
    </style>
    <p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Stap 2: Initialiseer het HTML-document

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Stap 3: Maak PDF-weergaveopties voor lage resolutie

```csharp
var options = new PdfRenderingOptions()
{
    HorizontalResolution = 50,
    VerticalResolution = 50
};
```

### Stap 4: Maak een PDF-apparaat en geef opties en uitvoerbestand op voor lage resolutie

```csharp
using (var device = new PdfDevice(options, "output_resolution_50.pdf"))
```

### Stap 5: HTML naar PDF renderen voor lage resolutie

```csharp
document.RenderTo(device);
```

### Stap 6: Maak PDF-weergaveopties voor hoge resolutie

```csharp
options = new PdfRenderingOptions()
{
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

### Stap 7: Maak een PDF-apparaat en geef opties en uitvoerbestand op voor hoge resolutie

```csharp
using (var device = new PdfDevice(options, "output_resolution_300.pdf"))
```

### Stap 8: HTML naar PDF renderen voor hoge resolutie

```csharp
document.RenderTo(device);
```

Dit voorbeeld illustreert hoe u de resolutie kunt aanpassen bij het renderen van HTML naar PDF, waarbij zowel schermen met lage als hoge resolutie in aanmerking worden genomen.

## Achtergrondkleur opgeven

### Stap 1: HTML-code voorbereiden en opslaan in bestand

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Stap 2: Initialiseer het HTML-document

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Stap 3: Initialiseer PDF-weergaveopties met achtergrondkleur

```csharp
var options = new PdfRenderingOptions()
{
    BackgroundColor = System.Drawing.Color.Cyan
};
```

### Stap 4: Maak een PDF-apparaat en geef opties en uitvoerbestand op

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Stap 5: HTML naar PDF renderen

```csharp
document.RenderTo(device);
```

Dit voorbeeld laat zien hoe u een achtergrondkleur kunt opgeven bij het converteren van HTML naar PDF.

## Stel de linker- en rechterpaginaformaten in

### Stap 1: HTML-code voorbereiden

```csharp
var code = @"<style>div { page-break-after: always; }</style>
    <div>First Page</div>
    <div>Second Page</div>
    <div>Third Page</div>
    <div>Fourth Page</div>";
```

### Stap 2: Initialiseer het HTML-document

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Stap 3: Maak PDF-weergaveopties met linker- en rechterpaginaformaten

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.SetLeftRightPage(
    new Page(new Size(400, 200)),
    new Page(new Size(400, 100))
);
```

### Stap 4: Maak een PDF-apparaat en geef opties en uitvoerbestand op

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Stap 5: HTML naar PDF renderen

```csharp
document.RenderTo(device);
```

Dit voorbeeld laat zien hoe u verschillende paginaformaten voor de linker- en rechterpagina's kunt instellen bij het converteren van HTML naar PDF.

## Pas het paginaformaat aan de inhoud aan

### Stap 1: HTML-code voorbereiden

```csharp
var code = @"<style>
    div { page-break-after: always; }
</style>
<div style='border: 1px solid red; width: 400px'>First Page</div>
<div style='border: 1px solid red; width: 600px'>Second Page</div>";
```

### Stap 2: Initialiseer het HTML-document

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Stap 3: Maak PDF-weergaveopties

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.AnyPage = new Page(new Size(500, 200));
options.PageSetup.AdjustToWidestPage = true;
```

### Stap 4: Maak een PDF-apparaat en geef opties en uitvoerbestand op

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Stap 5: HTML naar PDF renderen

```csharp
document.RenderTo(device);
```

Dit voorbeeld laat zien hoe u het paginaformaat kunt aanpassen aan de breedste inhoud bij het converteren van HTML naar PDF.

## Geef PDF-machtigingen op

### Stap 1: HTML-code voorbereiden

```csharp
var code = @"<div>Hello World!!</div>";
```

### Stap 2: Initialiseer het HTML-document

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Stap 3: Maak PDF-weergaveopties met machtigingen

```csharp
var options = new PdfRenderingOptions();
options.Encryption = new PdfEncryptionInfo(
    "user_pwd",
    "owner_pwd",
    PdfPermissions.PrintDocument,
    PdfEncryptionAlgorithm.RC4_128
);
```

### Stap 4: Maak een PDF-apparaat en geef opties en uitvoerbestand op

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Stap 5: HTML naar PDF renderen

```csharp
document.RenderTo(device);
```

Dit voorbeeld laat zien hoe u machtigingen en codering kunt opgeven bij het converteren van HTML naar een beveiligde PDF.

## Geef afbeeldingsspecifieke opties op

### Stap 1: HTML-code voorbereiden

```csharp
var code = @"<div>Hello World!!</div>";
```

### Stap 2: Initialiseer het HTML-document

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Stap 3: Creëer opties voor beeldweergave

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### Stap 4: Maak een afbeeldingsapparaat en geef opties en uitvoerbestand op

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### Stap 5: HTML naar afbeelding renderen

```csharp
document.RenderTo(device);
```

Dit voorbeeld laat zien hoe u HTML naar een afbeelding kunt converteren met specifieke weergaveopties, zoals formaat, resolutie en afvlakkingsmodus.

## Geef XPS-weergaveopties op

### Stap 1: HTML-code voorbereiden

```csharp
var code = @"<span>Hello World!!</span>";
```

### Stap 2: Initialiseer het HTML-document

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Stap 3: Maak XPS-weergaveopties met paginaformaat

```csharp
var options = new XpsRenderingOptions();
options.PageSetup.AnyPage = new Page(
    new Size(
        Length.FromInches(5),
        Length.FromInches(2)
    )
);
```

### Stap 4: Maak een XPS-apparaat en geef opties en uitvoerbestand op

```csharp
using (var device = new XpsDevice(options, "output.xps"))
```

### Stap 5: HTML renderen naar XPS

```csharp
document.RenderTo(device);
```

Dit voorbeeld laat zien hoe u HTML naar XPS converteert met een aangepast paginaformaat en weergaveopties.

## Combineer meerdere HTML-documenten in PDF

### Stap 1: HTML-code voorbereiden voor meerdere documenten

```csharp
var code1 = @"<br><span style='color: green'>Hello World!!</span>";
var code2 = @"<br><span style='color: blue'>Hello World!!</span>";
var code3 = @"<br><span style='color: red'>Hello World!!</span>";
```

### Stap 2: Maak HTML-documenten om samen te voegen

```csharp
using (var document1 = new HTMLDocument(code1, "."))
using (var document2 = new HTMLDocument(code2, "."))
using (var document3 = new HTMLDocument(code3, "."))
```

### Stap 3: Initialiseer HTML-renderer

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Stap 4: Maak een PDF-apparaat voor samengevoegde uitvoer

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Stap 5: HTML-documenten samenvoegen tot PDF

```csharp
renderer.Render(device, document1, document2, document3);
```

Dit voorbeeld laat zien hoe u meerdere HTML-documenten combineert in één enkel PDF-bestand met behulp van Aspose.HTML voor .NET.

## Time-out voor weergave instellen

### Stap 1: HTML-code voorbereiden met JavaScript

```csharp
var code = @"
    <script>
        var count = 0;
        setInterval(function()
        {
            var element = document.createElement('div');
            var message = (++count) + '. ' + 'Hello World!!';
            var text = document.createTextNode(message);
            element.appendChild(text);
            document.body.appendChild(element);
        }, 1000);
    </script>";
```

### Stap 2: Initialiseer het HTML-document

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Stap 3: Initialiseer HTML-renderer

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Stap 4: Maak een PDF-apparaat en stel de renderingtime-out in

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Stap 5: HTML naar PDF renderen met time-out

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

Dit voorbeeld laat zien hoe u een time-out voor weergave instelt bij het converteren van HTML naar PDF, wat handig kan zijn bij het omgaan met dynamische inhoud of langlopende scripts.

## Conclusie

Aspose.HTML voor .NET is een veelzijdige bibliotheek waarmee ontwikkelaars efficiënt met HTML-documenten kunnen werken. In deze zelfstudie hebben we verschillende voorbeelden besproken, van eenvoudige HTML- naar PDF-conversies tot meer geavanceerde functies zoals aangepaste paginaformaten, resoluties en machtigingen. Door deze voorbeelden te volgen, kunt u het volledige potentieel van Aspose.HTML voor .NET benutten in uw .NET-toepassingen.

 Als u vragen heeft of verdere hulp nodig heeft, aarzel dan niet om een bezoek te brengen aan de[Aspose.HTML-forum](https://forum.aspose.com/) voor ondersteuning en begeleiding.

## Veelgestelde vragen

### Q1. Wat is Aspose.HTML voor .NET?
   
A1: Aspose.HTML voor .NET is een .NET-bibliotheek waarmee ontwikkelaars HTML-documenten programmatisch kunnen manipuleren en converteren. Het biedt een breed scala aan functies voor het werken met HTML-inhoud, waaronder HTML naar PDF, XPS en beeldconversie, evenals geavanceerde weergaveopties.

### Vraag 2. Waar kan ik Aspose.HTML voor .NET downloaden?

 A2: U kunt Aspose.HTML voor .NET downloaden van de[download link](https://releases.aspose.com/html/net/).

### Q3. Heb ik een licentie nodig om Aspose.HTML voor .NET te gebruiken?

A3: Hoewel u Aspose.HTML voor .NET zonder licentie kunt gebruiken, is het raadzaam een licentie voor productiegebruik aan te schaffen om alle functies te ontgrendelen en eventuele watermerken of beperkingen te verwijderen.

### Q4. Hoe kan ik mijn PDF-bestanden beschermen die zijn gegenereerd met Aspose.HTML voor .NET?

A4: U kunt PDF-machtigingen en coderingsinstellingen opgeven bij het renderen van HTML naar PDF met behulp van Aspose.HTML voor .NET. Hiermee kunt u bepalen wie de resulterende PDF-bestanden kan openen en wijzigen.

### Vraag 5. Kan ik HTML naar andere formaten zoals XPS of afbeeldingen converteren?

A5: Ja, Aspose.HTML voor .NET ondersteunt het converteren van HTML naar verschillende formaten, waaronder PDF, XPS en afbeeldingen (bijvoorbeeld JPEG). U kunt de conversie-instellingen aanpassen aan uw specifieke vereisten.
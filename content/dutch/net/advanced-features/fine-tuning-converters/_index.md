---
title: Fine-tuning converters in .NET met Aspose.HTML
linktitle: Converters in .NET nauwkeurig afstemmen
second_title: Aspose.HTML .NET HTML-manipulatie-API
description: Leer hoe u HTML naar PDF, XPS en afbeeldingen converteert met Aspose.HTML voor .NET. Stapsgewijze tutorial met codevoorbeelden en veelgestelde vragen.
type: docs
weight: 16
url: /nl/net/advanced-features/fine-tuning-converters/
---

## Invoering

Aspose.HTML voor .NET is een krachtige bibliotheek waarmee ontwikkelaars HTML-documenten in verschillende formaten kunnen manipuleren en converteren. Of u nu HTML naar PDF, XPS of afbeeldingen wilt converteren of andere HTML-gerelateerde taken wilt uitvoeren, Aspose.HTML biedt een robuuste set tools om u te helpen de klus te klaren.

In deze tutorial verkennen we enkele essentiële functies van Aspose.HTML voor .NET en geven we stapsgewijze uitleg voor elk voorbeeld. Aan het einde van deze tutorial hebt u een goed begrip van hoe u Aspose.HTML voor .NET in uw .NET-toepassingen kunt gebruiken.

## Vereisten

Voordat we ingaan op de voorbeelden, moet u ervoor zorgen dat u aan de volgende voorwaarden voldoet:

-  Aspose.HTML voor .NET: U moet de Aspose.HTML voor .NET-bibliotheek geïnstalleerd hebben. U kunt deze downloaden van de[downloadlink](https://releases.aspose.com/html/net/).

-  Tijdelijke licentie (optioneel): Als u geen geldige licentie hebt, kunt u een tijdelijke licentie verkrijgen bij[hier](https://purchase.aspose.com/temporary-license/).

Laten we nu eens enkele veelvoorkomende use cases met Aspose.HTML voor .NET bekijken.

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

### Stap 2: Initialiseer HTML-document

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Stap 3: PDF-apparaat maken en uitvoerbestand specificeren

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Stap 4: HTML naar PDF renderen

```csharp
document.RenderTo(device);
```

Dit voorbeeld converteert een HTML-fragment naar een PDF-document. U kunt de HTML-code en het uitvoerbestand naar wens aanpassen.

## Aangepaste paginagrootte instellen

### Stap 1: HTML-code voorbereiden

```csharp
var code = @"<span>Hello World!!</span>";
```

### Stap 2: Initialiseer HTML-document

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Stap 3: PDF-renderingopties maken

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

### Stap 4: Maak een PDF-apparaat en specificeer opties en uitvoerbestand

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

### Stap 2: Initialiseer HTML-document

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Stap 3: Maak PDF-renderingopties voor lage resolutie

```csharp
var options = new PdfRenderingOptions()
{
    HorizontalResolution = 50,
    VerticalResolution = 50
};
```

### Stap 4: Maak een PDF-apparaat en specificeer opties en uitvoerbestand voor lage resolutie

```csharp
using (var device = new PdfDevice(options, "output_resolution_50.pdf"))
```

### Stap 5: HTML naar PDF renderen voor lage resolutie

```csharp
document.RenderTo(device);
```

### Stap 6: Maak PDF-renderingopties voor hoge resolutie

```csharp
options = new PdfRenderingOptions()
{
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

### Stap 7: Maak een PDF-apparaat en specificeer opties en uitvoerbestand voor hoge resolutie

```csharp
using (var device = new PdfDevice(options, "output_resolution_300.pdf"))
```

### Stap 8: HTML naar PDF renderen voor hoge resolutie

```csharp
document.RenderTo(device);
```

Dit voorbeeld illustreert hoe u de resolutie kunt aanpassen bij het renderen van HTML naar PDF, waarbij rekening wordt gehouden met schermen met zowel een lage als een hoge resolutie.

## Achtergrondkleur opgeven

### Stap 1: HTML-code voorbereiden en opslaan in bestand

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Stap 2: Initialiseer HTML-document

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Stap 3: Initialiseer PDF-renderingopties met achtergrondkleur

```csharp
var options = new PdfRenderingOptions()
{
    BackgroundColor = System.Drawing.Color.Cyan
};
```

### Stap 4: Maak een PDF-apparaat en specificeer opties en uitvoerbestand

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Stap 5: HTML naar PDF renderen

```csharp
document.RenderTo(device);
```

Dit voorbeeld laat zien hoe u een achtergrondkleur kunt opgeven bij het converteren van HTML naar PDF.

## Stel de linker- en rechterpagina-afmetingen in

### Stap 1: HTML-code voorbereiden

```csharp
var code = @"<style>div { page-break-after: always; }</style>
    <div>First Page</div>
    <div>Second Page</div>
    <div>Third Page</div>
    <div>Fourth Page</div>";
```

### Stap 2: Initialiseer HTML-document

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Stap 3: Maak PDF-renderingopties met linker- en rechterpaginaformaten

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.SetLeftRightPage(
    new Page(new Size(400, 200)),
    new Page(new Size(400, 100))
);
```

### Stap 4: Maak een PDF-apparaat en specificeer opties en uitvoerbestand

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Stap 5: HTML naar PDF renderen

```csharp
document.RenderTo(device);
```

Dit voorbeeld laat zien hoe u verschillende paginaformaten voor de linker- en rechterpagina's kunt instellen bij het converteren van HTML naar PDF.

## Paginaformaat aanpassen aan inhoud

### Stap 1: HTML-code voorbereiden

```csharp
var code = @"<style>
    div { page-break-after: always; }
</style>
<div style='border: 1px solid red; width: 400px'>First Page</div>
<div style='border: 1px solid red; width: 600px'>Second Page</div>";
```

### Stap 2: Initialiseer HTML-document

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Stap 3: PDF-renderingopties maken

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.AnyPage = new Page(new Size(500, 200));
options.PageSetup.AdjustToWidestPage = true;
```

### Stap 4: Maak een PDF-apparaat en specificeer opties en uitvoerbestand

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Stap 5: HTML naar PDF renderen

```csharp
document.RenderTo(device);
```

Dit voorbeeld laat zien hoe u de paginagrootte kunt aanpassen aan de breedste inhoud bij het converteren van HTML naar PDF.

## PDF-machtigingen specificeren

### Stap 1: HTML-code voorbereiden

```csharp
var code = @"<div>Hello World!!</div>";
```

### Stap 2: Initialiseer HTML-document

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Stap 3: PDF-renderingopties met machtigingen maken

```csharp
var options = new PdfRenderingOptions();
options.Encryption = new PdfEncryptionInfo(
    "user_pwd",
    "owner_pwd",
    PdfPermissions.PrintDocument,
    PdfEncryptionAlgorithm.RC4_128
);
```

### Stap 4: Maak een PDF-apparaat en specificeer opties en uitvoerbestand

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Stap 5: HTML naar PDF renderen

```csharp
document.RenderTo(device);
```

Dit voorbeeld laat zien hoe u machtigingen en encryptie kunt opgeven bij het converteren van HTML naar een beveiligde PDF.

## Geef afbeeldingsspecifieke opties op

### Stap 1: HTML-code voorbereiden

```csharp
var code = @"<div>Hello World!!</div>";
```

### Stap 2: Initialiseer HTML-document

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Stap 3: Opties voor het renderen van afbeeldingen maken

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### Stap 4: Maak een afbeeldingsapparaat en specificeer opties en uitvoerbestand

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### Stap 5: HTML naar afbeelding renderen

```csharp
document.RenderTo(device);
```

Dit voorbeeld laat zien hoe u HTML naar een afbeelding kunt converteren met specifieke renderingopties, zoals opmaak, resolutie en smoothing-modus.

## XPS-renderingopties specificeren

### Stap 1: HTML-code voorbereiden

```csharp
var code = @"<span>Hello World!!</span>";
```

### Stap 2: Initialiseer HTML-document

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Stap 3: XPS-renderingopties maken met paginaformaat

```csharp
var options = new XpsRenderingOptions();
options.PageSetup.AnyPage = new Page(
    new Size(
        Length.FromInches(5),
        Length.FromInches(2)
    )
);
```

### Stap 4: XPS-apparaat maken en opties en uitvoerbestand specificeren

```csharp
using (var device = new XpsDevice(options, "output.xps"))
```

### Stap 5: HTML naar XPS renderen

```csharp
document.RenderTo(device);
```

Dit voorbeeld laat zien hoe u HTML naar XPS kunt converteren met aangepaste paginagrootte en renderingopties.

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

Dit voorbeeld laat zien hoe u meerdere HTML-documenten kunt combineren tot één PDF-bestand met behulp van Aspose.HTML voor .NET.

## Stel rendering-time-out in

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

### Stap 2: Initialiseer HTML-document

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Stap 3: Initialiseer HTML-renderer

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Stap 4: PDF-apparaat maken en rendering-time-out instellen

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Stap 5: HTML naar PDF renderen met time-out

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

Dit voorbeeld laat zien hoe u een rendering-time-out instelt bij het converteren van HTML naar PDF. Dit kan handig zijn bij dynamische inhoud of langlopende scripts.

## Conclusie

Aspose.HTML voor .NET is een veelzijdige bibliotheek waarmee ontwikkelaars efficiënt met HTML-documenten kunnen werken. In deze tutorial hebben we verschillende voorbeelden behandeld, van eenvoudige HTML- naar PDF-conversies tot geavanceerdere functies zoals aangepaste paginagroottes, resoluties en machtigingen. Door deze voorbeelden te volgen, kunt u het volledige potentieel van Aspose.HTML voor .NET in uw .NET-toepassingen benutten.

 Als u vragen heeft of verdere hulp nodig heeft, aarzel dan niet om de website te bezoeken[Aspose.HTML-forum](https://forum.aspose.com/) voor ondersteuning en begeleiding.

## Veelgestelde vragen

### Vraag 1. Wat is Aspose.HTML voor .NET?
   
A1: Aspose.HTML voor .NET is een .NET-bibliotheek waarmee ontwikkelaars HTML-documenten programmatisch kunnen manipuleren en converteren. Het biedt een breed scala aan functies voor het werken met HTML-inhoud, waaronder HTML naar PDF, XPS en afbeeldingsconversie, evenals geavanceerde renderingopties.

### V2. Waar kan ik Aspose.HTML voor .NET downloaden?

 A2: U kunt Aspose.HTML voor .NET downloaden van de[downloadlink](https://releases.aspose.com/html/net/).

### V3. Heb ik een licentie nodig om Aspose.HTML voor .NET te gebruiken?

A3: Hoewel u Aspose.HTML voor .NET zonder licentie kunt gebruiken, raden wij u aan een licentie voor productiegebruik aan te schaffen. Zo kunt u alle functies ontgrendelen en watermerken of beperkingen verwijderen.

### Vraag 4. Hoe kan ik mijn PDF-bestanden die zijn gegenereerd met Aspose.HTML voor .NET beschermen?

A4: U kunt PDF-machtigingen en encryptie-instellingen opgeven bij het renderen van HTML naar PDF met Aspose.HTML voor .NET. Hiermee kunt u bepalen wie toegang heeft tot de resulterende PDF-bestanden en deze mag wijzigen.

### V5. Kan ik HTML converteren naar andere formaten zoals XPS of afbeeldingen?

A5: Ja, Aspose.HTML voor .NET ondersteunt het converteren van HTML naar verschillende formaten, waaronder PDF, XPS en afbeeldingen (bijv. JPEG). U kunt de conversie-instellingen aanpassen aan uw specifieke vereisten.
---
title: Finjustera omvandlare i .NET med Aspose.HTML
linktitle: Finjustera omvandlare i .NET
second_title: Aspose.HTML .NET HTML manipulation API
description: Lär dig hur du konverterar HTML till PDF, XPS och bilder med Aspose.HTML för .NET. Steg-för-steg handledning med kodexempel och vanliga frågor.
type: docs
weight: 16
url: /sv/net/advanced-features/fine-tuning-converters/
---

## Introduktion

Aspose.HTML för .NET är ett kraftfullt bibliotek som låter utvecklare manipulera och konvertera HTML-dokument i olika format. Oavsett om du behöver konvertera HTML till PDF, XPS eller bilder, eller utföra andra HTML-relaterade uppgifter, tillhandahåller Aspose.HTML en robust uppsättning verktyg som hjälper dig att få jobbet gjort.

I den här handledningen kommer vi att utforska några väsentliga funktioner i Aspose.HTML för .NET och ge steg-för-steg förklaringar för varje exempel. I slutet av denna handledning kommer du att ha en gedigen förståelse för hur du använder Aspose.HTML för .NET i dina .NET-applikationer.

## Förutsättningar

Innan vi dyker in i exemplen, se till att du har följande förutsättningar på plats:

-  Aspose.HTML for .NET: Du bör ha Aspose.HTML for .NET-biblioteket installerat. Du kan ladda ner den från[nedladdningslänk](https://releases.aspose.com/html/net/).

- Tillfällig licens (valfritt): Om du inte har en giltig licens kan du få en tillfällig licens från[här](https://purchase.aspose.com/temporary-license/).

Låt oss nu utforska några vanliga användningsfall med Aspose.HTML för .NET.

## Importera namnområden

Börja med att importera de nödvändiga namnrymden i din C#-kod:

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Pdf;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Xps;
using Aspose.Html.Rendering.Pdf.Encryption;
using Aspose.Html.Drawing;
```

## Konvertera HTML till PDF

### Steg 1: Förbered HTML-kod

```csharp
var code = @"<span>Hello World!!</span>";
```

### Steg 2: Initiera HTML-dokument

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Steg 3: Skapa PDF-enhet och ange utdatafil

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Steg 4: Gör HTML till PDF

```csharp
document.RenderTo(device);
```

Det här exemplet konverterar ett HTML-utdrag till ett PDF-dokument. Du kan anpassa HTML-koden och utdatafilen efter behov.

## Ställ in anpassad sidstorlek

### Steg 1: Förbered HTML-kod

```csharp
var code = @"<span>Hello World!!</span>";
```

### Steg 2: Initiera HTML-dokument

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Steg 3: Skapa PDF-renderingsalternativ

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

### Steg 4: Skapa PDF-enhet och ange alternativ och utdatafil

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Steg 5: Gör HTML till PDF

```csharp
document.RenderTo(device);
```

Det här exemplet visar hur du ställer in en anpassad sidstorlek för det resulterande PDF-dokumentet.

## Justera upplösning

### Steg 1: Förbered HTML-kod och spara till fil

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

### Steg 2: Initiera HTML-dokument

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Steg 3: Skapa PDF-renderingsalternativ för låg upplösning

```csharp
var options = new PdfRenderingOptions()
{
    HorizontalResolution = 50,
    VerticalResolution = 50
};
```

### Steg 4: Skapa PDF-enhet och ange alternativ och utdatafil för lågupplösning

```csharp
using (var device = new PdfDevice(options, "output_resolution_50.pdf"))
```

### Steg 5: Gör HTML till PDF för lågupplösning

```csharp
document.RenderTo(device);
```

### Steg 6: Skapa PDF-renderingsalternativ för hög upplösning

```csharp
options = new PdfRenderingOptions()
{
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

### Steg 7: Skapa PDF-enhet och ange alternativ och utdatafil för hög upplösning

```csharp
using (var device = new PdfDevice(options, "output_resolution_300.pdf"))
```

### Steg 8: Återge HTML till PDF för hög upplösning

```csharp
document.RenderTo(device);
```

Det här exemplet illustrerar hur du justerar upplösningen när du renderar HTML till PDF, med tanke på både låg- och högupplösta skärmar.

## Ange bakgrundsfärg

### Steg 1: Förbered HTML-kod och spara till fil

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Steg 2: Initiera HTML-dokument

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Steg 3: Initiera PDF-renderingsalternativ med bakgrundsfärg

```csharp
var options = new PdfRenderingOptions()
{
    BackgroundColor = System.Drawing.Color.Cyan
};
```

### Steg 4: Skapa PDF-enhet och ange alternativ och utdatafil

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Steg 5: Gör HTML till PDF

```csharp
document.RenderTo(device);
```

Det här exemplet visar hur du anger en bakgrundsfärg när du konverterar HTML till PDF.

## Ställ in vänster och höger sidstorlekar

### Steg 1: Förbered HTML-kod

```csharp
var code = @"<style>div { page-break-after: always; }</style>
    <div>First Page</div>
    <div>Second Page</div>
    <div>Third Page</div>
    <div>Fourth Page</div>";
```

### Steg 2: Initiera HTML-dokument

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Steg 3: Skapa PDF-renderingsalternativ med vänster och höger sidstorlek

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.SetLeftRightPage(
    new Page(new Size(400, 200)),
    new Page(new Size(400, 100))
);
```

### Steg 4: Skapa PDF-enhet och ange alternativ och utdatafil

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Steg 5: Gör HTML till PDF

```csharp
document.RenderTo(device);
```

Det här exemplet visar hur du ställer in olika sidstorlekar för vänster och höger sida när du konverterar HTML till PDF.

## Justera sidstorlek till innehåll

### Steg 1: Förbered HTML-kod

```csharp
var code = @"<style>
    div { page-break-after: always; }
</style>
<div style='border: 1px solid red; width: 400px'>First Page</div>
<div style='border: 1px solid red; width: 600px'>Second Page</div>";
```

### Steg 2: Initiera HTML-dokument

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Steg 3: Skapa PDF-renderingsalternativ

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.AnyPage = new Page(new Size(500, 200));
options.PageSetup.AdjustToWidestPage = true;
```

### Steg 4: Skapa PDF-enhet och ange alternativ och utdatafil

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Steg 5: Gör HTML till PDF

```csharp
document.RenderTo(device);
```

Det här exemplet visar hur du justerar sidstorleken till det bredaste innehållet när du konverterar HTML till PDF.

## Ange PDF-behörigheter

### Steg 1: Förbered HTML-kod

```csharp
var code = @"<div>Hello World!!</div>";
```

### Steg 2: Initiera HTML-dokument

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Steg 3: Skapa PDF-renderingsalternativ med behörigheter

```csharp
var options = new PdfRenderingOptions();
options.Encryption = new PdfEncryptionInfo(
    "user_pwd",
    "owner_pwd",
    PdfPermissions.PrintDocument,
    PdfEncryptionAlgorithm.RC4_128
);
```

### Steg 4: Skapa PDF-enhet och ange alternativ och utdatafil

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Steg 5: Gör HTML till PDF

```csharp
document.RenderTo(device);
```

Det här exemplet visar hur man anger behörigheter och kryptering när HTML konverteras till en skyddad PDF.

## Ange bildspecifika alternativ

### Steg 1: Förbered HTML-kod

```csharp
var code = @"<div>Hello World!!</div>";
```

### Steg 2: Initiera HTML-dokument

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Steg 3: Skapa alternativ för bildrendering

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### Steg 4: Skapa bildenhet och ange alternativ och utdatafil

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### Steg 5: Återge HTML till bild

```csharp
document.RenderTo(device);
```

Det här exemplet visar hur man konverterar HTML till en bild med specifika renderingsalternativ, såsom format, upplösning och utjämningsläge.

## Ange XPS-renderingsalternativ

### Steg 1: Förbered HTML-kod

```csharp
var code = @"<span>Hello World!!</span>";
```

### Steg 2: Initiera HTML-dokument

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Steg 3: Skapa XPS-renderingsalternativ med sidstorlek

```csharp
var options = new XpsRenderingOptions();
options.PageSetup.AnyPage = new Page(
    new Size(
        Length.FromInches(5),
        Length.FromInches(2)
    )
);
```

### Steg 4: Skapa XPS-enhet och ange alternativ och utdatafil

```csharp
using (var device = new XpsDevice(options, "output.xps"))
```

### Steg 5: Rendera HTML till XPS

```csharp
document.RenderTo(device);
```

Det här exemplet visar hur du konverterar HTML till XPS med anpassad sidstorlek och renderingsalternativ.

## Kombinera flera HTML-dokument till PDF

### Steg 1: Förbered HTML-kod för flera dokument

```csharp
var code1 = @"<br><span style='color: green'>Hello World!!</span>";
var code2 = @"<br><span style='color: blue'>Hello World!!</span>";
var code3 = @"<br><span style='color: red'>Hello World!!</span>";
```

### Steg 2: Skapa HTML-dokument som ska sammanfogas

```csharp
using (var document1 = new HTMLDocument(code1, "."))
using (var document2 = new HTMLDocument(code2, "."))
using (var document3 = new HTMLDocument(code3, "."))
```

### Steg 3: Initiera HTML Renderer

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Steg 4: Skapa PDF-enhet för sammanslagen utdata

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Steg 5: Slå samman HTML-dokument till PDF

```csharp
renderer.Render(device, document1, document2, document3);
```

Det här exemplet visar hur man kombinerar flera HTML-dokument till en enda PDF-fil med Aspose.HTML för .NET.

## Ställ in renderingstidsgräns

### Steg 1: Förbered HTML-kod med JavaScript

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

### Steg 2: Initiera HTML-dokument

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Steg 3: Initiera HTML Renderer

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Steg 4: Skapa PDF-enhet och ställ in renderingstidsgräns

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Steg 5: Gör HTML till PDF med Timeout

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

Det här exemplet visar hur man ställer in en renderingstidsgräns vid konvertering av HTML till PDF, vilket kan vara användbart när man hanterar dynamiskt innehåll eller långa skript.

## Slutsats

Aspose.HTML för .NET är ett mångsidigt bibliotek som ger utvecklare möjlighet att arbeta med HTML-dokument effektivt. I den här handledningen täckte vi olika exempel, från grundläggande HTML till PDF-konverteringar till mer avancerade funktioner som anpassade sidstorlekar, upplösningar och behörigheter. Genom att följa dessa exempel kan du utnyttja den fulla potentialen hos Aspose.HTML för .NET i dina .NET-applikationer.

 Om du har några frågor eller behöver ytterligare hjälp, tveka inte att besöka[Aspose.HTML Forum](https://forum.aspose.com/) för stöd och vägledning.

## FAQ's

### Q1. Vad är Aspose.HTML för .NET?
   
S1: Aspose.HTML för .NET är ett .NET-bibliotek som gör det möjligt för utvecklare att manipulera och konvertera HTML-dokument programmatiskt. Den erbjuder ett brett utbud av funktioner för att arbeta med HTML-innehåll, inklusive HTML till PDF, XPS och bildkonvertering, samt avancerade renderingsalternativ.

### Q2. Var kan jag ladda ner Aspose.HTML för .NET?

 S2: Du kan ladda ner Aspose.HTML för .NET från[nedladdningslänk](https://releases.aspose.com/html/net/).

### Q3. Behöver jag en licens för att använda Aspose.HTML för .NET?

S3: Även om du kan använda Aspose.HTML för .NET utan licens, rekommenderas det att du skaffar en licens för produktionsanvändning för att låsa upp alla funktioner och ta bort eventuella vattenstämplar eller begränsningar.

### Q4. Hur kan jag skydda mina PDF-filer genererade med Aspose.HTML för .NET?

S4: Du kan ange PDF-behörigheter och krypteringsinställningar när du renderar HTML till PDF med Aspose.HTML för .NET. Detta låter dig kontrollera vem som kan komma åt och ändra de resulterande PDF-filerna.

### F5. Kan jag konvertera HTML till andra format som XPS eller bilder?

S5: Ja, Aspose.HTML för .NET stöder konvertering av HTML till olika format, inklusive PDF, XPS och bilder (t.ex. JPEG). Du kan anpassa konverteringsinställningarna för att uppfylla dina specifika krav.
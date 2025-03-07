---
title: Konvertera EPUB till PDF i .NET med Aspose.HTML
linktitle: Konvertera EPUB till PDF i .NET
second_title: Aspose.HTML .NET HTML manipulation API
description: Lär dig hur du konverterar EPUB till PDF med Aspose.HTML för .NET. Den här steg-för-steg-guiden täcker anpassningsalternativ, vanliga frågor och mer för sömlös dokumentkonvertering.
weight: 12
url: /sv/net/html-extensions-and-conversions/convert-epub-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konvertera EPUB till PDF i .NET med Aspose.HTML


I den här handledningen kommer vi att utforska hur man använder Aspose.HTML för .NET för att konvertera EPUB-filer till PDF. Aspose.HTML är ett kraftfullt .NET-bibliotek som tillhandahåller olika funktioner för att arbeta med HTML- och EPUB-dokument. Vi kommer att täcka förutsättningarna, importera nödvändiga namnrymder och dela upp flera exempel och förklara varje steg i detalj.

## Förutsättningar

Innan du börjar, se till att du har följande förutsättningar på plats:

1. Aspose.HTML for .NET: Se till att du har Aspose.HTML for .NET installerat i ditt .NET-projekt. Du kan ladda ner den från[här](https://releases.aspose.com/html/net/).

2. Din datakatalog: Du behöver en datakatalog där dina EPUB-filer lagras.

Låt oss nu dyka in i steg-för-steg-processen att konvertera EPUB till PDF med Aspose.HTML för .NET.

## Konvertera EPUB till PDF

### Steg 1: Initiera ditt projekt

Se till att du har ett .NET-projekt inställt och att Aspose.HTML för .NET är installerat.

### Steg 2: Importera nödvändiga namnområden

Importera de nödvändiga namnrymden i din C#-kodfil:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
```

### Steg 3: Öppna EPUB-filen

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Fortsätt till nästa steg...
}
```

-  Ersätta`"Your Data Directory"` med den faktiska katalogen där din EPUB-fil finns.
- Denna kod öppnar EPUB-filen för läsning.

### Steg 4: Ställ in PDF-alternativ och utför konvertering

```csharp
var options = new PdfSaveOptions();
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Skapa en instans av`PdfSaveOptions` för att ange PDF-konverteringsinställningar.
-  Använd`Converter.ConvertEPUB` metod för att konvertera EPUB till PDF med de givna alternativen.
- Spara den resulterande PDF-filen som "output.pdf."

## Ange PDF-sparalternativ

### Steg 1: Initiera ditt projekt

Se till att du har ett .NET-projekt inställt och Aspose.HTML för .NET installerat.

### Steg 2: Importera nödvändiga namnområden

Importera de nödvändiga namnrymden i din C#-kod:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
```

### Steg 3: Öppna EPUB-filen

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Fortsätt till nästa steg...
}
```

-  Ersätta`"Your Data Directory"` med den faktiska katalogen för din EPUB-fil.
- Öppna EPUB-filen för läsning.

### Steg 4: Anpassa PDF-alternativ

```csharp
var options = new PdfSaveOptions()
{
    PageSetup = { AnyPage = new Page() { Size = Size.FromPixels(3000, 1000) } },
    BackgroundColor = System.Drawing.Color.AliceBlue
};
```

-  Skapa en instans av`PdfSaveOptions` och anpassa den enligt dina krav.
- I det här exemplet ställer vi in sidstorleken till 3000 pixlars bredd och 1000 pixlars höjd, och bakgrundsfärgen till Alice Blue.

### Steg 5: Utför konvertering

```csharp
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Använd`Converter.ConvertEPUB` metod för att konvertera EPUB till PDF med de anpassade alternativen.
- Spara den resulterande PDF-filen som "output.pdf."

## Använd Custom Stream Provider

### Steg 1: Initiera ditt projekt

Skapa ett .NET-projekt och installera Aspose.HTML för .NET.

### Steg 2: Importera nödvändiga namnområden

Importera de nödvändiga namnrymden i din C#-kod:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
```

### Steg 3: Öppna EPUB-filen

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Fortsätt till nästa steg...
}
```

-  Ersätta`"Your Data Directory"` med den faktiska katalogen för din EPUB-fil.
- Öppna EPUB-filen för läsning.

### Steg 4: Använd en anpassad strömleverantör

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    Converter.ConvertEPUB(stream, new PdfSaveOptions(), streamProvider);

    // Fortsätt till nästa steg...
}
```

-  Skapa en`MemoryStreamProvider` för att hantera konverteringsresultatet som en minnesström.
-  Använd`Converter.ConvertEPUB` metod med den anpassade stream-leverantören.

### Steg 5: Spara resultatet

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.pdf"))
{
    memory.CopyTo(fs);
}
```

- Få tillgång till minnesströmmen som innehåller de konverterade data.
- Ställ in strömningspositionen till början.
- Skapa en utdata-PDF-fil och kopiera innehållet från minnesströmmen till den.

### Klass MemoryStreamProvider källkod. 

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // Lista över MemoryStream-objekt som skapats under dokumentrenderingen
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // Denna metod anropas när den enda utdataströmmen krävs, till exempel för XPS-, PDF- eller TIFF-format.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // Denna metod kallas när skapandet av flera utströmmar krävs. Till exempel under renderingen av HTML till lista över bildfiler (JPG, PNG, etc.)
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // Här kan du släppa strömmen fylld med data och till exempel spola den till hårddisken
            }
            public void Dispose()
            {
                // Frigör resurser
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
Nu har du lärt dig hur du konverterar EPUB-filer till PDF med Aspose.HTML för .NET med olika alternativ och anpassningsmöjligheter. Aspose.HTML förenklar processen, ger flexibilitet och kontroll över din dokumentkonvertering.

## Slutsats

Aspose.HTML för .NET är ett mångsidigt verktyg för att konvertera EPUB-filer till PDF, som erbjuder anpassningsalternativ för att skräddarsy det resulterande PDF-dokumentet efter dina behov. Oavsett om du behöver enkla omvandlingar eller avancerad anpassning, har Aspose.HTML dig täckt.

 Om du inte redan har gjort det kan du ladda ner Aspose.HTML för .NET från[webbplats](https://releases.aspose.com/html/net/) och börja använda det i dina .NET-applikationer idag.

---

## Vanliga frågor

### Är Aspose.HTML för .NET gratis att använda?
    Aspose.HTML för .NET är en kommersiell produkt, men en gratis testversion är tillgänglig[här](https://releases.aspose.com/).

### Kan jag anpassa utseendet på den konverterade PDF-filen?
   Ja, du kan anpassa PDF-utseendet genom att justera alternativ som sidstorlek och bakgrundsfärg, som visas i exempel 2.

### Hur kan jag få support för Aspose.HTML för .NET?
    Du kan hitta support och resurser på[Aspose.HTML forum](https://forum.aspose.com/).

### Finns det andra format jag kan konvertera med Aspose.HTML för .NET?
   Ja, Aspose.HTML för .NET stöder olika dokumentformat, inklusive HTML, EPUB och mer.

### Är Aspose.HTML för ..NET lämplig för storskalig dokumentkonvertering?
   Aspose.HTML för .NET är utformad för att hantera storskaliga dokumentkonverteringar effektivt, vilket gör den lämplig för ett brett spektrum av applikationer.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

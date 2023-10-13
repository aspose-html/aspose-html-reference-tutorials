---
title: Konvertera EPUB till XPS i .NET med Aspose.HTML
linktitle: Konvertera EPUB till XPS i .NET
second_title: Aspose.Slides .NET HTML manipulation API
description: Lär dig hur du konverterar EPUB till XPS i .NET med Aspose.HTML för .NET. Följ vår steg-för-steg-guide för enkla konverteringar.
type: docs
weight: 13
url: /sv/net/html-extensions-and-conversions/convert-epub-to-xps/
---

Letar du efter ett smidigt sätt att konvertera EPUB-filer till XPS-format i dina .NET-program? Aspose.HTML för .NET ger en kraftfull lösning för att uppnå detta utan ansträngning. I den här steg-för-steg-guiden går vi igenom processen att konvertera EPUB till XPS med Aspose.HTML. Låt oss börja!

## Förutsättningar

Innan du dyker in i konverteringsprocessen från EPUB till XPS måste du se till att du har följande förutsättningar:

### 1. Aspose.HTML för .NET Library

 Se till att du har Aspose.HTML för .NET-biblioteket installerat i ditt projekt. Om du inte har gjort det kan du få det från[Aspose.HTML för .NET Nedladdningssida](https://releases.aspose.com/html/net/).

### 2. Mata in EPUB-fil

Du behöver en EPUB-fil som du vill konvertera till XPS. Se till att du har en EPUB-fil tillgänglig för konvertering.

### 3. .NET utvecklingsmiljö

Den här guiden förutsätter att du har en fungerande .NET-utvecklingsmiljö inställd på din dator.

## Importera namnutrymme

Till att börja med bör du importera det nödvändiga namnutrymmet för Aspose.HTML:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## Konvertera EPUB till XPS

Låt oss dela upp processen att konvertera en EPUB-fil till XPS-format i flera steg.

### Steg 1.1: Öppna EPUB-filen

Öppna först den befintliga EPUB-filen för läsning med en FileStream:

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Fortsätt med konverteringsprocessen
}
```

### Steg 1.2: Skapa XpsSaveOptions

Skapa en instans av XpsSaveOptions. Detta steg är avgörande för att konfigurera XPS-utgången:

```csharp
var options = new XpsSaveOptions();
```

### Steg 1.3: Konvertera EPUB till XPS

Låt oss nu anropa ConvertEPUB-metoden för att konvertera EPUB till XPS:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Ange anpassade XPS-alternativ

Du kan anpassa XPS-utdata ytterligare genom att ange anpassade alternativ som sidstorlek och bakgrundsfärg.

### Steg 2.1: Anpassad sidstorlek och bakgrundsfärg

Skapa en instans av XpsSaveOptions med anpassad sidstorlek och bakgrundsfärg:

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

### Steg 2.2: Konvertera EPUB till XPS med anpassade alternativ

Anropa nu ConvertEPUB-metoden för att konvertera EPUB till XPS med de anpassade alternativen:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Använd Custom Stream Provider

I det här steget kommer vi att konvertera EPUB till XPS med en anpassad strömleverantör, så att du kan manipulera den resulterande informationen.

### Steg 3.1: Skapa en MemoryStreamProvider

Skapa en instans av MemoryStreamProvider:

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    // Fortsätt med konverteringsprocessen
}
```

### Steg 3.2: Konvertera EPUB till XPS med Stream Provider

Konvertera EPUB till XPS med MemoryStreamProvider:

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### Steg 3.3: Få åtkomst till och spara resultat

Hämta minnesströmmen som innehåller den konverterade datan och spara den i en utdatafil:

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

### Klass MemoryStreamProvider källkod

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
Grattis! Du har framgångsrikt konverterat en EPUB-fil till XPS-format med Aspose.HTML för .NET.

## Slutsats

den här omfattande handledningen undersökte vi hur man kan utnyttja Aspose.HTML för .NET för att konvertera EPUB-filer till XPS-format med olika anpassningsalternativ. Oavsett om du är en erfaren utvecklare eller precis har börjat, förenklar Aspose.HTML processen, så att du enkelt kan hantera EPUB till XPS-konverteringar.

 Har du frågor eller stött på problem? Kolla in[Aspose.HTML-dokumentation](https://reference.aspose.com/html/net/) för mer insikter eller sök hjälp från[Aspose.HTML Community Forum](https://forum.aspose.com/).

## Vanliga frågor

### Vad är Aspose.HTML för .NET?
Aspose.HTML för .NET är ett kraftfullt bibliotek som gör det möjligt för utvecklare att arbeta med HTML-, EPUB- och XPS-dokument i .NET-applikationer.

### Var kan jag ladda ner Aspose.HTML för .NET?
 Du kan ladda ner Aspose.HTML för .NET från[nedladdningssida](https://releases.aspose.com/html/net/).

### Finns det en gratis testversion tillgänglig för Aspose.HTML för .NET?
 Ja, du kan få en gratis provperiod från[här](https://releases.aspose.com/).

### Hur kan jag få en tillfällig licens för Aspose.HTML för .NET?
 För att få en tillfällig licens, besök[sida för tillfällig licens](https://purchase.aspose.com/temporary-license/).

### Var kan jag hitta fler handledningar och dokumentation för Aspose.HTML för .NET?
Utforska ett brett utbud av handledningar och detaljerad dokumentation om[Aspose.HTML-dokumentation](https://reference.aspose.com/html/net/) sida.
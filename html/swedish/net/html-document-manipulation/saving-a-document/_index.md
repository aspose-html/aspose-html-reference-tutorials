---
title: Spara ett dokument i .NET med Aspose.HTML
linktitle: Spara ett dokument i .NET
second_title: Aspose.HTML .NET HTML manipulation API
description: Lås upp kraften i Aspose.HTML för .NET med vår steg-för-steg-guide. Lär dig att skapa, manipulera och konvertera HTML- och SVG-dokument
weight: 16
url: /sv/net/html-document-manipulation/saving-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Spara ett dokument i .NET med Aspose.HTML


I dagens digitala tidsålder är det viktigt att skapa och manipulera HTML- och SVG-dokument för många mjukvaruutvecklare och företag. Aspose.HTML för .NET är ett kraftfullt bibliotek som förenklar dessa uppgifter och erbjuder olika funktioner för att arbeta med HTML, SVG och mer. I den här omfattande guiden kommer vi att dyka in i det väsentliga i Aspose.HTML för .NET, och dela upp varje exempel i lätta att följa steg. Oavsett om du är en erfaren utvecklare eller precis har börjat, kommer du att tycka att den här guiden är ovärderlig för att utnyttja funktionerna i Aspose.HTML.

## Förutsättningar

Innan vi ger oss ut på den här resan, låt oss se till att du har allt du behöver:

- Utvecklingsmiljö: Se till att du har Visual Studio eller någon annan .NET-utvecklingsmiljö installerad på din dator.

- Aspose.HTML for .NET: Du måste skaffa Aspose.HTML for .NET-biblioteket. Du kan ladda ner den från[här](https://releases.aspose.com/html/net/).

- Kunskaper i C#: Bekantskap med programmeringsspråket C# är fördelaktigt men inte obligatoriskt. Den här guiden är designad för att vara nybörjarvänlig.

## Importera namnutrymme

För att börja använda Aspose.HTML för .NET måste du importera de nödvändiga namnrymden till ditt projekt. Inkludera följande namnområde i din C#-kod:

### Steg 1: Importera Aspose.HTML-namnutrymme
```csharp
using Aspose.Html;
```

Detta namnutrymme ger dig tillgång till olika HTML- och SVG-manipuleringsfunktioner.

## HTML till fil

### Steg 1: Initiera ett tomt HTML-dokument
```csharp
// Initiera ett tomt HTML-dokument.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Skapa ett textelement och lägg till det i dokumentet
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Spara HTML till filen på disken.
    document.Save("document.html");
}
```

I det här exemplet skapar vi ett HTML-dokument och lägger till ett enkelt "Hello World!" text till den. Vi sparar sedan HTML till en fil på disken.

## HTML utan länkad fil

### Steg 1: Förbered en enkel HTML-fil
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Här skapar vi en grundläggande HTML-fil med en ankarlänk till en annan fil.

### Steg 2: Ladda 'document.html' i minnet
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Skapa instans av Spara alternativ
    var options = new Aspose.Html.Saving.HTMLSaveOptions();
    //Ställ in det maximala hanteringsdjupet till 0 för att klippa bort länkade HTML-filer.
    options.ResourceHandlingOptions.MaxHandlingDepth = 0;
    // Spara dokumentet
    document.Save(@".\html-to-file-example\document.html", options);
}
```

I det här exemplet laddar vi ett HTML-dokument i minnet, ställer in maximalt hanteringsdjup för att klippa bort länkade filer och sparar dokumentet. 

## HTML till MHTML

### Steg 1: Förbered en enkel HTML-fil
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Precis som i exempel 2 skapar vi en grundläggande HTML-fil med en ankarlänk till en annan fil.

### Steg 2: Ladda 'document.html' i minnet och spara som MHTML
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Spara dokumentet som MHTML
    document.Save(@".\html-to-file-example\document.mht", Aspose.Html.Saving.HTMLSaveFormat.MHTML);
}
```

Här laddar vi HTML-dokumentet i minnet och sparar det i MHTML-format.

## HTML till Markdown

### Steg 1: Förbered en HTML-kod
```csharp
var html_code = "<H2>Hello World!</H2>";
```

 I det här steget definierar vi ett HTML-kodavsnitt som innehåller en`<H2>` element.

### Steg 2: Initiera dokument från HTML-kod och spara som Markdown
```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Spara dokumentet som en Markdown-fil.
    document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
}
```

Vi skapar ett HTML-dokument från kodavsnittet och sparar det som en Markdown-fil.

## SVG till fil

### Steg 1: Förbered en SVG-kod
```csharp
var code = @"
    <svg xmlns='http://www.w3.org/2000/svg' height='80' width='300'>
        <g fill='none'>
            <path stroke='red' d='M5 20 l215 0' />
            <path stroke='black' d='M5 40 l215 0' />
            <path stroke='blue' d='M5 60 l215 0' />
        </g>
    </svg>";
```

Här skapar vi en SVG-kod som ritar en enkel, färgglad grafik.

### Steg 2: Initiera ett SVG-dokument från koden och spara på disk
```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument(code, "."))
{
    // Spara SVG-filen på disken
    document.Save("document.svg");
}
```

I det här steget skapar vi ett SVG-dokument från koden och sparar det som en SVG-fil.

## Slutsats

Aspose.HTML för .NET är ett mångsidigt bibliotek som förenklar HTML- och SVG-dokumenthantering i dina .NET-applikationer. I den här guiden har vi täckt fem viktiga exempel, som delar upp var och en i steg-för-steg-instruktioner. Oavsett om du skapar, manipulerar eller konverterar dokument, har Aspose.HTML dig täckt. Genom att följa dessa steg är du på god väg att bemästra detta kraftfulla verktyg.

## FAQ's

### F1: Vad är Aspose.HTML för .NET?

S1: Aspose.HTML för .NET är ett .NET-bibliotek som tillhandahåller ett brett utbud av funktioner för att arbeta med HTML- och SVG-dokument, inklusive skapande, manipulation och konvertering.

### F2: Var kan jag ladda ner Aspose.HTML för .NET?

 S2: Du kan ladda ner Aspose.HTML för .NET från[här](https://releases.aspose.com/html/net/).

### F3: Är Aspose.HTML för .NET lämplig för nybörjare?

S3: Ja, Aspose.HTML för .NET kan användas av både nybörjare och erfarna utvecklare. Exemplen i den här guiden är utformade för att vara nybörjarvänliga.

### F4: Kan jag konvertera HTML till andra format med Aspose.HTML för .NET?

S4: Ja, Aspose.HTML för .NET stöder konvertering till olika format, inklusive MHTML och Markdown, som visas i exemplen.

### F5: Var kan jag få support för Aspose.HTML för .NET?

 S5: Du kan hitta support och svar på dina frågor i Aspose.HTML-gemenskapsforumet[här](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

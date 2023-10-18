---
title: Skapa ett dokument i .NET med Aspose.HTML
linktitle: Skapa ett dokument i .NET
second_title: Aspose.HTML .NET HTML manipulation API
description: Släpp lös kraften i Aspose.HTML för .NET. Lär dig att skapa, manipulera och optimera HTML- och SVG-dokument enkelt. Utforska steg-för-steg exempel och vanliga frågor.
type: docs
weight: 14
url: /sv/net/html-document-manipulation/creating-a-document/
---

I den ständigt föränderliga världen av webbutveckling är det viktigt att ligga före kurvan. Aspose.HTML för .NET ger utvecklare en robust verktygslåda för att arbeta med HTML-dokument. Oavsett om du börjar från början, laddar från en fil, hämtar från en URL eller hanterar SVG-dokument, erbjuder detta bibliotek den mångsidighet du behöver.

den här steg-för-steg-guiden kommer vi att fördjupa oss i grunderna för att använda Aspose.HTML för .NET, för att säkerställa att du är väl rustad att använda detta kraftfulla verktyg i dina webbutvecklingsprojekt. Innan vi dyker in i detaljerna, låt oss gå igenom förutsättningarna och de nödvändiga namnområdena för att kickstarta din resa.

## Förutsättningar

För att framgångsrikt följa denna handledning och utnyttja kraften i Aspose.HTML för .NET, behöver du följande förutsättningar:

- En Windows-maskin med .NET Framework eller .NET Core installerat.
- En kodredigerare som Visual Studio.
- Grundläggande kunskaper i C#-programmering.

Nu när du har dina förutsättningar på plats, låt oss sätta igång.

## Importera namnområden

Innan du börjar använda Aspose.HTML för .NET måste du importera de nödvändiga namnrymden. Dessa namnområden innehåller klasser och metoder som är viktiga för att arbeta med HTML-dokument. Nedan finns en lista över namnområden du bör importera:

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

Med dessa namnrymder importerade är du nu redo att dyka in i steg-för-steg-exemplen.

## Skapa ett HTML-dokument från grunden

### Steg 1: Initiera ett tomt HTML-dokument

```csharp
// Initiera ett tomt HTML-dokument.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Skapa ett textelement och lägg till det i dokumentet
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Spara dokumentet på disk.
    document.Save("document.html");
}
```

I det här exemplet börjar vi med att skapa ett tomt HTML-dokument och lägga till ett "Hello World!" text till den. Vi sparar sedan dokumentet till en fil.

## Skapa ett HTML-dokument från en fil

### Steg 1: Förbered en 'document.html'-fil

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### Steg 2: Ladda från en 'document.html'-fil

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Skriv dokumentinnehållet till utdataströmmen.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Här förbereder vi en fil med "Hello World!" innehåll och sedan ladda det som ett HTML-dokument. Vi skriver ut dokumentets innehåll till konsolen.

## Skapa ett HTML-dokument från en URL

### Steg 1: Ladda ett dokument från en webbsida

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    // Skriv dokumentinnehållet till utdataströmmen.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

I det här exemplet laddar vi ett HTML-dokument direkt från en webbsida och visar dess innehåll.

## Skapa ett HTML-dokument från en sträng

### Steg 1: Förbered en HTML-kod

```csharp
var html_code = "<p>Hello World!</p>";
```

### Steg 2: Initiera dokument från strängvariabeln

```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Spara dokumentet på disk.
    document.Save("document.html");
}
```

Här skapar vi ett HTML-dokument från en strängvariabel och sparar det i en fil.

## Skapa ett HTML-dokument från en MemoryStream

### Steg 1: Skapa ett minnesströmobjekt

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    // Skriv HTML-koden i minnesobjektet
    sw.Write("<p>Hello World!</p>");
    // Ställ in positionen till början
    sw.Flush();
    mem.Seek(0, System.IO.SeekOrigin.Begin);
    // Initiera dokument från minnesströmmen
    using (var document = new Aspose.Html.HTMLDocument(mem, "."))
    {
        // Spara dokumentet på disk.
        document.Save("document.html");
    }
}
```

I det här exemplet skapar vi ett HTML-dokument från en minnesström och sparar det i en fil.

## Arbeta med SVG-dokument

### Steg 1: Initiera SVG-dokumentet från en sträng

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "."))
{
    // Skriv dokumentinnehållet till utdataströmmen.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Här skapar vi och visar ett SVG-dokument från en sträng.

## Ladda ett HTML-dokument asynkront

### Steg 1: Skapa instansen av HTML-dokument

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Steg 2: Prenumerera på 'ReadyStateChange'-evenemanget

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    //Kontrollera värdet på egenskapen "ReadyState".
    if (document.ReadyState == "complete")
    {
        Console.WriteLine(document.DocumentElement.OuterHTML);
        Console.WriteLine("Loading is completed. Press any key to continue...");
    }
};
```

### Steg 3: Navigera asynkront på den angivna Uri

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

I det här exemplet laddar vi ett HTML-dokument asynkront och hanterar händelsen 'ReadyStateChange' för att visa innehållet när laddningen är klar.

## Hantera 'OnLoad'-händelsen

### Steg 1: Skapa instansen av HTML-dokument

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Steg 2: Prenumerera på 'OnLoad'-evenemanget

```csharp
document.OnLoad += (sender, @event) =>
{
    Console.WriteLine(document.DocumentElement.OuterHTML);
    Console.WriteLine("Loading is completed. Press any key to continue...");
};
```

### Steg 3: Navigera asynkront på den angivna Uri

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

Det här exemplet visar att du laddar ett HTML-dokument asynkront och hanterar händelsen 'OnLoad' för att visa innehållet när det är klart.

## Sammanfattningsvis

I webbutvecklingens dynamiska värld är det avgörande att ha rätt verktyg till ditt förfogande. Aspose.HTML för .NET ger dig möjlighet att skapa, manipulera och bearbeta HTML- och SVG-dokument effektivt. Den här omfattande guiden har gått igenom det väsentliga och säkerställt att du kan utnyttja kraften i Aspose.HTML för .NET i dina projekt.

## FAQ's

### F1: Vad är Aspose.HTML för .NET?

S1: Aspose.HTML för .NET är ett kraftfullt .NET-bibliotek som gör det möjligt för utvecklare att arbeta med HTML- och SVG-dokument. Det ger ett brett utbud av funktioner, från att skapa dokument från början till att analysera och manipulera befintliga HTML- och SVG-filer.

### F2: Kan jag använda Aspose.HTML för .NET med .NET Core?

S2: Ja, Aspose.HTML för .NET är kompatibel med både .NET Framework och .NET Core, vilket gör det till ett mångsidigt val för moderna .NET-applikationer.

### F3: Är Aspose.HTML för .NET lämplig för webbskrapning och analys?

A3: Absolut! Aspose.HTML för .NET är ett utmärkt val för webbskrapnings- och analysuppgifter, tack vare dess förmåga att ladda HTML-dokument från webbadresser och strängar. Du kan extrahera data, utföra analyser och mer.

### F4: Hur får jag tillgång till support för Aspose.HTML för .NET?

 S4: Om du stöter på några problem eller har frågor när du använder Aspose.HTML för .NET, kan du besöka[Aspose Forum](https://forum.aspose.com/) för stöd och hjälp från samhället och Aspose-experter.

### S5: Var kan jag hitta detaljerad dokumentation och nedladdningsalternativ?

S5: För omfattande dokumentation och tillgång till nedladdningsalternativ kan du hänvisa till följande länkar:

- [Dokumentation](https://reference.aspose.com/html/net/)
- [Ladda ner](https://releases.aspose.com/html/net/)
- [köpa](https://purchase.aspose.com/buy)
- [Gratis provperiod](https://releases.aspose.com/)
- [Tillfällig licens](https://purchase.aspose.com/temporary-license/)
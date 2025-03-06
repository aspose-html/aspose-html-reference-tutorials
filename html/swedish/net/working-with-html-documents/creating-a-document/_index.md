---
title: Skapa ett HTML-dokument i .NET med Aspose.HTML
linktitle: Skapa ett HTML-dokument i .NET
second_title: Aspose.HTML .NET HTML manipulation API
description: Lär dig hur du skapar HTML-dokument i .NET med Aspose.HTML, från början eller från webbadresser. En omfattande handledning för webbutvecklare.
weight: 10
url: /sv/net/working-with-html-documents/creating-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa ett HTML-dokument i .NET med Aspose.HTML


När det gäller webbutveckling och datamanipulation är det oumbärligt att ha ett kraftfullt verktyg för att skapa, modifiera och arbeta med HTML-dokument. Aspose.HTML för .NET är ett sådant verktyg som kan förenkla dina HTML-relaterade uppgifter. I denna omfattande handledning kommer vi att utforska hur man skapar HTML-dokument med Aspose.HTML för .NET steg för steg. Innan vi dyker in i exemplen, låt oss täcka några förutsättningar.

## Förutsättningar

Innan du ger dig ut på denna resa, se till att du har följande förutsättningar på plats:

1. Visual Studio: Se till att du har Visual Studio installerat på ditt system.

2. Aspose.HTML for .NET: Ladda ner och installera Aspose.HTML for .NET-biblioteket. Du hittar nedladdningslänken[här](https://releases.aspose.com/html/net/).

3. Grundläggande kunskaper i C#: Bekanta dig med grunderna i programmeringsspråket i C#.

Nu när vi har täckta förutsättningarna, låt oss börja med att skapa HTML-dokument.

## Importera namnområden

Först måste du importera de nödvändiga namnrymden för att använda Aspose.HTML i ditt C#-projekt. Lägg till följande med hjälp av direktiv till din kodfil:

```csharp
using Aspose.Html.Dom.Svg;
using Aspose.Html;
```

## Skapa ett SVG-dokument

```csharp
static void CreateSVG()
{
    using (var document = new SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "about:blank"))
    {
        // Utför åtgärder på SVG-dokumentet här...
    }
}
```

 I det här exemplet skapar vi ett SVG-dokument genom att tillhandahålla SVG-innehållet och en bas-URL. De`SVGDocument` klass från Aspose.HTML för .NET låter dig manipulera SVG-dokument utan ansträngning.

## Skapa ett HTML-dokument från grunden

```csharp
static void FromScratch()
{
    using (var document = new HTMLDocument())
    {
        // Utför åtgärder på HTML-dokumentet här...
    }
}
```

 Det här exemplet visar hur man skapar ett HTML-dokument från början. De`HTMLDocument`klass tillhandahåller en tom arbetsyta för ditt HTML-innehåll.

## Skapa ett HTML-dokument från en lokal fil

```csharp
static void FromLocalFile()
{
    string dataDir = "Your Data Directory";
    using (var document = new HTMLDocument(dataDir + "input.html"))
    {
        // Utför åtgärder på HTML-dokumentet här...
    }
}
```

 Om du har en befintlig HTML-fil på ditt lokala system kan du ladda den med hjälp av`HTMLDocument` klass, som visas i detta exempel.

## Skapa ett HTML-dokument från en fjärradress

```csharp
static void FromRemoteURL()
{
    using (var document = new HTMLDocument("http://din.webbplats.com/"))
    {
        // Utför åtgärder på HTML-dokumentet här...
    }
}
```

Ibland kan du behöva arbeta med HTML-innehåll som finns på en fjärrserver. Det här exemplet visar hur man skapar ett HTML-dokument från en fjärr-URL.

## Skapa ett HTML-dokument från en fjärradress (alternativ)

```csharp
static void FromRemoteURL1()
{
    using (var document = new HTMLDocument(new Url("http://your.site.com/")))
    {
        // Utför åtgärder på HTML-dokumentet här...
    }
}
```

Detta alternativa tillvägagångssätt visar också hur man skapar ett HTML-dokument från en fjärr-URL med en annan konstruktor.

## Skapa ett HTML-dokument från HTML-innehåll

```csharp
static void FromHTML()
{
    using (var document = new HTMLDocument("<p>my first paragraph</p>", "."))
    {
        // Utför åtgärder på HTML-dokumentet här...
    }
}
```

Om du har HTML-innehåll i ett strängformat kan du skapa ett HTML-dokument med det, som visas i det här exemplet.

## Skapa ett HTML-dokument från en ström

```csharp
static void FromStream()
{
    using (MemoryStream mem = new MemoryStream())
    using (StreamWriter sw = new StreamWriter(mem))
    {
        sw.Write("<p>my first paragraph</p>");
        sw.Flush();
        mem.Seek(0, SeekOrigin.Begin);
        using (var document = new HTMLDocument(mem, "about:blank"))
        {
            // Utför åtgärder på HTML-dokumentet här...
        }
    }
}
```

det här exemplet visar vi hur man skapar ett HTML-dokument från data i en minnesström. Detta kan vara användbart när du har HTML-innehåll i en ström och vill manipulera det.

## Slutsats

Aspose.HTML för .NET tillhandahåller en kraftfull uppsättning verktyg för att skapa och arbeta med HTML-dokument i dina .NET-applikationer. Med exemplen i den här handledningen kan du enkelt komma igång med att skapa HTML-dokument, oavsett om det är från början, lokala filer, fjärrwebbadresser eller befintligt HTML-innehåll.

 Har du frågor eller behöver du hjälp? Besök Aspose.HTML community forum för support på[https://forum.aspose.com/](https://forum.aspose.com/).

## Vanliga frågor

### F1: Är Aspose.HTML för .NET gratis att använda?
 S1: Aspose.HTML för .NET erbjuder en gratis provperiod, men för full användning måste du köpa en licens. Du hittar mer information på[https://purchase.aspose.com/buy](https://purchase.aspose.com/buy).

### F2: Hur kan jag få en tillfällig licens för Aspose.HTML för .NET?
 S2: Om du behöver en tillfällig licens kan du få en på[https://purchase.aspose.com/temporary-license/](https://purchase.aspose.com/temporary-license/).

### F3: Var kan jag hitta dokumentation för Aspose.HTML för .NET?
S3: Dokumentationen finns på[https://reference.aspose.com/html/net/](https://reference.aspose.com/html/net/).

### F4: Finns det några andra Aspose-bibliotek för .NET-utveckling?
 S4: Ja, Aspose tillhandahåller en rad bibliotek för olika filformat och dokumentmanipuleringsuppgifter. Kolla in deras utbud på[https://products.aspose.com/](https://products.aspose.com/).

### F5: Kan jag använda Aspose.HTML för .NET i mina webbapplikationer?
S5: Ja, Aspose.HTML för .NET är kompatibel med webbapplikationer, vilket gör det till ett mångsidigt val för både stationära och webbaserade projekt.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

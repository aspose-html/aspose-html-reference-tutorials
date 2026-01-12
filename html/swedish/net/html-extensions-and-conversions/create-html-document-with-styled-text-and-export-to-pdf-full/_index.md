---
category: general
date: 2025-12-29
description: Skapa ett HTML‑dokument i C# och lär dig hur du anger teckensnittsfamilj,
  ställer in teckenstorlek och sedan sparar HTML som PDF eller konverterar HTML till
  PDF med Aspose.HTML.
draft: false
keywords:
- create html document
- set font family
- set font size
- save html as pdf
- convert html to pdf
language: sv
og_description: Skapa HTML-dokument i C# och se omedelbart hur du ställer in teckensnittsfamilj,
  ställer in teckenstorlek, och sedan sparar HTML som PDF eller konverterar HTML till
  PDF med Aspose.HTML.
og_title: Skapa HTML-dokument – Formaterad text & PDF-export
tags:
- aspnet
- csharp
- pdf-generation
title: Skapa HTML-dokument med formaterad text och exportera till PDF – Fullständig
  guide
url: /sv/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa HTML‑dokument med formaterad text och exportera till PDF

Har du någonsin behövt **skapa HTML‑dokument** i farten och omvandla det till en PDF utan att lämna din C#‑kod? Kanske bygger du en rapportmotor, en fakturagenerator eller bara en snabb förhandsgranskning för användare. Den goda nyheten är att du kan göra det på några rader med Aspose.HTML, och du får full kontroll över teckensnittsfamilj, teckenstorlek och även fet‑kursiv formatering.

I den här handledningen går vi igenom hela processen – från att skapa ett HTML‑dokument i minnet till att spara det som en PDF‑fil. När du är klar vet du exakt hur du **sätter teckensnittsfamilj**, **sätter teckenstorlek** och **sparar HTML som PDF** (dvs. **konverterar HTML till PDF**) med ett rent, produktionsklart kodexempel.

## Vad du behöver

- .NET 6+ (API:et fungerar både med .NET Core och .NET Framework)  
- Aspose.HTML för .NET NuGet‑paket (`Aspose.Html`) – installera via `dotnet add package Aspose.Html`  
- En mapp på disken där den genererade PDF‑filen kan skrivas  

Inga extra HTML‑mallar, inga externa konverterare, bara ren C#.

![create html document illustration](/images/create-html-document.png){alt="exempel på skapa html-dokument"}

## Steg 1: Skapa HTML‑dokumentet

Först behöver vi ett tomt HTML‑dokumentobjekt. Tänk på det som en ren duk där du senare målar ditt formaterade stycke.

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

// Step 1 – initialize a new HTML document in memory
HTMLDocument htmlDocument = new HTMLDocument();

// Grab a reference to the <body> element for later use
HTMLBodyElement body = htmlDocument.Body;
```

**Varför detta är viktigt:** `HTMLDocument` ger dig en DOM‑liknande struktur som du kan manipulera programatiskt. Du behöver inte röra råa strängar eller fil‑I/O förrän i slutet.

## Steg 2: Lägg till ett stycke och ange teckensnittsfamilj & teckenstorlek

Nu skapar vi ett `<p>`‑element, sätter in lite text och definierar explicit teckensnittsfamilj och storlek. Här kommer nyckelorden **set font family** och **set font size** in i bilden.

```csharp
// Step 2 – create a <p> element with some sample text
HtmlElement paragraph = htmlDocument.CreateElement("p");
paragraph.InnerHtml = "Bold & Italic text";

// Define the base font style
paragraph.Style.FontFamily = "Arial";   // set font family
paragraph.Style.FontSize = "18px";      // set font size

// Attach the paragraph to the document body
body.AppendChild(paragraph);
```

**Proffstips:** Om du behöver en webbsäker reserv kan du ange en kommaseparerad lista som `"Arial, Helvetica, sans-serif"`; webbläsaren (eller Aspose) väljer det första tillgängliga teckensnittet.

## Steg 3: Applicera fet och kursiv stil med WebFontStyle‑flaggor

Aspose.HTML erbjuder en praktisk enum `WebFontStyle` som låter dig kombinera stilar med en bitvis OR. Låt oss göra texten både fet **och** kursiv.

```csharp
// Step 3 – apply bold and italic using WebFontStyle flags
paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

**Vad händer under huven?** `FontStyle`‑egenskapen översätts till CSS‑deklarationerna `font-weight` och `font-style`. Genom att OR‑a flaggorna undviker vi att skriva två separata CSS‑rader.

## Steg 4: Konvertera HTML till PDF (Spara HTML som PDF)

Det sista steget är själva konverteringen. Med ett enda anrop till `Save` renderar Aspose.HTML DOM‑en och skriver en PDF‑fil till disk. Detta uppfyller både **save html as pdf** och **convert html to pdf**‑kraven.

```csharp
// Step 4 – save the HTML document as a PDF file
string outputPath = @"C:\Temp\styled.pdf";
htmlDocument.Save(outputPath, new PDFSaveOptions());

// Optional: open the PDF automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Förväntat resultat:** Öppna `styled.pdf` så ser du ett enda stycke med texten “Bold & Italic text” i 18‑px Arial, renderat i fet och kursiv stil. PDF‑dimensionerna motsvarar ett standard‑A4‑blad och texten är markerbar – tack vare vektorrendering.

## Fullständigt fungerande exempel

Sätter vi ihop allt får vi det kompletta, körklara programmet:

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new HTML document
        HTMLDocument htmlDocument = new HTMLDocument();
        HTMLBodyElement body = htmlDocument.Body;

        // 2️⃣ Add a styled paragraph
        HtmlElement paragraph = htmlDocument.CreateElement("p");
        paragraph.InnerHtml = "Bold & Italic text";

        // Set font family and size
        paragraph.Style.FontFamily = "Arial";
        paragraph.Style.FontSize = "18px";

        // 3️⃣ Apply bold + italic
        paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // Append to body
        body.AppendChild(paragraph);

        // 4️⃣ Save as PDF (convert HTML to PDF)
        string outputFile = @"C:\Temp\styled.pdf";
        htmlDocument.Save(outputFile, new PDFSaveOptions());

        Console.WriteLine($"PDF generated at: {outputFile}");
    }
}
```

### Så kör du koden

1. Installera Aspose.HTML NuGet‑paketet:  
   ```bash
   dotnet add package Aspose.Html
   ```
2. Ersätt `C:\Temp\styled.pdf` med en mapp där du har skrivbehörighet.  
3. Bygg och kör: `dotnet run`.  

Du bör se ett konsolmeddelande som bekräftar filens plats, och PDF‑filen kommer att innehålla det formaterade stycket.

## Vanliga frågor & kantfall

- **Vad gör jag om jag behöver ett eget web‑teckensnitt?**  
  Ladda teckensnittet med `HTMLFontFaceRule` eller referera till en fjärr‑`@font-face`‑CSS‑fil innan du skapar stycket.

- **Kan jag lägga till bilder innan konvertering?**  
  Absolut. Använd `HTMLImageElement img = (HTMLImageElement)htmlDocument.CreateElement("img");` och sätt `img.Source` till en lokal sökväg eller data‑URI.

- **Hur hanterar jag flersidiga PDF‑filer?**  
  Lägg till fler element (tabeller, div‑ar osv.) så paginerar Aspose.HTML automatiskt när innehållet överskrider sidans höjd.

- **Finns det ett sätt att styra PDF‑metadata?**  
  Skicka in en `PdfSaveOptions`‑instans och sätt egenskaper som `Author`, `Title` eller `PdfAConformanceLevel`.

## Sammanfattning

Vi har gått igenom hur du **skapar HTML‑dokument** i C#, **sätter teckensnittsfamilj**, **sätter teckenstorlek**, applicerar fet‑kursiv stil och slutligen **sparar HTML som PDF – alltså **konverterar HTML till PDF** med Aspose.HTML. Kodsnutten är kort nog att klistra in i vilket .NET‑projekt som helst, men ändå komplett nog att fungera som en stabil grund för mer avancerade rapporteringsscenarier.

## Nästa steg

- Experimentera med CSS‑klasser för återanvändbar styling.  
- Kombinera flera stycken, tabeller och bilder för att bygga rikare PDF‑dokument.  
- Utforska PDF/A‑kompatibilitet om du behöver arkiveringsklassade dokument.  

Känn dig fri att justera teckensnitt, storlek eller färger – det finns ingen gräns för vad du kan generera programmässigt. Lycka till med kodandet, och må dina PDF‑filer alltid renderas exakt som du föreställer dig!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
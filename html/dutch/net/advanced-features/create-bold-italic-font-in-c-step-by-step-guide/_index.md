---
category: general
date: 2026-08-15
description: Maak snel een vet‑cursief lettertype in C#. Leer hoe je een lettertype
  in C# maakt met vet‑ en cursief‑stijlen met behulp van de ingebouwde Font‑klasse.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create bold italic font
- create font in c#
- C# FontStyle
- text styling C#
- System.Drawing.Font
language: nl
lastmod: 2026-08-15
og_description: Maak een vet cursief lettertype in C# met een duidelijk voorbeeld.
  Deze tutorial laat zien hoe je een lettertype maakt in C# met behulp van FontStyle‑vlaggen
  en legt veelvoorkomende valkuilen uit.
og_image_alt: Screenshot of text rendered with a bold italic Arial font in a C# console
  window
og_title: Maak een vet cursief lettertype in C# – volledige programmeergids
schemas:
- author: Aspose
  dateModified: '2026-08-15'
  description: Create bold italic font in C# quickly. Learn how to create font in
    C# with bold and italic styles using the built‑in Font class.
  headline: Create bold italic font in C# – step‑by‑step guide
  type: TechArticle
- description: Create bold italic font in C# quickly. Learn how to create font in
    C# with bold and italic styles using the built‑in Font class.
  name: Create bold italic font in C# – step‑by‑step guide
  steps:
  - name: Save the code to a file named `Program.cs`.
    text: Save the code to a file named `Program.cs`.
  - name: Open a terminal in the file’s directory.
    text: Open a terminal in the file’s directory.
  - name: Execute `dotnet new console -n FontDemo` (if you need a project scaffold).
    text: Execute `dotnet new console -n FontDemo` (if you need a project scaffold).
  - name: Replace the generated `Program.cs` with the code above.
    text: Replace the generated `Program.cs` with the code above.
  - name: Run `dotnet add package System.Drawing.Common` (required for .NET Core/5+).
    text: Run `dotnet add package System.Drawing.Common` (required for .NET Core/5+).
  - name: Build and run with `dotnet run`.
    text: Build and run with `dotnet run`.
  type: HowTo
tags:
- C#
- fonts
- text styling
title: Maak een vet‑cursief lettertype in C# – stapsgewijze handleiding
url: /nl/net/advanced-features/create-bold-italic-font-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vet cursief lettertype maken in C# – stapsgewijze gids

Als je **vet cursief lettertype wilt maken** in C#, laat deze gids je precies zien hoe je dat doet. Je ziet een volledig, uitvoerbaar voorbeeld dat ook laat zien hoe je **lettertype maakt in C#** met de standaard .NET `Font`-klasse.

Werken met aangepaste lettertypen is een routineonderdeel van het bouwen van Windows desktop‑apps, het genereren van PDF’s of het renderen van HTML op de server. Aan het einde van deze tutorial kun je een lettertype instantiëren dat zowel vet als cursief is, begrijp je waarom de bitwise `|`‑operator wordt gebruikt, en kun je veelvoorkomende randgevallen afhandelen, zoals ontbrekende lettertypefamilies.

Er zijn geen externe bibliotheken nodig — alles maakt gebruik van de .NET Framework / .NET Core basis‑class‑library.

## Wat je zult leren

* Hoe je de benodigde namespaces voor lettertype‑verwerking importeert.  
* De syntaxis om `FontStyle.Bold` en `FontStyle.Italic` te combineren.  
* Hoe je verifieert dat het lettertype succesvol is aangemaakt.  
* Tips voor fallback‑afhandeling wanneer de gevraagde familie niet geïnstalleerd is.  

Er zijn geen externe bibliotheken nodig — alles maakt gebruik van de .NET Framework / .NET Core basis‑class‑library.

## Vereisten

* .NET 6.0 SDK of later (de code werkt ook op .NET Framework 4.6+).  
* Een code‑editor of IDE (Visual Studio, VS Code, Rider, enz.).  
* Basiskennis van C#‑syntaxis.  

Als je aan deze vereisten voldoet, kun je de stappen volgen zonder extra configuratie.

## Stap 1: Voeg de benodigde using‑directieven toe

De `Font`‑klasse bevindt zich in de `System.Drawing`‑namespace, die deel uitmaakt van het `System.Drawing.Common`‑NuGet‑pakket voor .NET Core/.NET 5+. Voeg de namespace toe aan de bovenkant van je bestand:

```csharp
using System;
using System.Drawing;   // Provides Font and FontStyle
```

> **Waarom deze stap belangrijk is** – Zonder de regel `using System.Drawing;` kan de compiler `Font` of `FontStyle` niet vinden, wat resulteert in een “type or namespace name could not be found”‑fout.

## Stap 2: Combineer vet en cursief stijlen met de bitwise OR‑operator

In .NET is `FontStyle` een enum gemarkeerd met het `[Flags]`‑attribuut. Dit betekent dat je meerdere waarden kunt combineren met de `|` (bitwise OR)‑operator:

```csharp
// Step 2: Create a Font that is both bold and italic
var font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
```

### Uitleg

* `\"Arial\"` – de naam van de lettertypefamilie. Als het systeem Arial niet geïnstalleerd heeft, valt de constructor terug op het standaardlettertype.  
* `12` – puntgrootte.  
* `FontStyle.Bold | FontStyle.Italic` – combineert de twee stijl‑flags. De `|`‑operator voegt de binaire representatie van elke flag samen, waardoor een enkele waarde ontstaat die “vet + cursief” vertegenwoordigt.

> **Pro tip:** Gebruik altijd de enum‑namen (`FontStyle.Bold`) in plaats van magische getallen; dit verbetert de leesbaarheid en voorkomt bugs wanneer de enum‑waarden veranderen.

## Stap 3: Verifieer het aangemaakte lettertype (optioneel maar aanbevolen)

Het afdrukken van de eigenschappen van het lettertype helpt je te bevestigen dat de stijlcombinatie geslaagd is, vooral bij het debuggen op een nieuwe machine.

```csharp
// Step 3: Output the font details to the console
Console.WriteLine($"Font family: {font.Name}");
Console.WriteLine($"Size (pt): {font.Size}");
Console.WriteLine($"Style: {font.Style}");
```

**Verwachte output**

```
Font family: Arial
Size (pt): 12
Style: Bold, Italic
```

Als de output zowel `Bold` als `Italic` vermeldt, is het lettertype correct aangemaakt.

## Stap 4: Render een voorbeeldstring (visuele bevestiging)

Wanneer je een console‑app uitvoert kun je de daadwerkelijke glyph‑styling niet zien, maar je kunt een afbeelding genereren om het resultaat te bewijzen. Het volgende fragment tekent “Hello, World!” met het vet‑cursieve lettertype en slaat het op als *sample.png*:

```csharp
// Step 4: Draw text to an image file for visual confirmation
using (var bitmap = new Bitmap(300, 100))
using (var graphics = Graphics.FromImage(bitmap))
{
    graphics.Clear(Color.White);
    var brush = Brushes.Black;
    graphics.DrawString("Hello, World!", font, brush, new PointF(10, 30));
    bitmap.Save("sample.png");
    Console.WriteLine("Image saved as sample.png");
}
```

Na het uitvoeren van het programma, open *sample.png* om de tekst te zien die is gerenderd met de vet‑cursieve stijl.

![Voorbeeldtekst gerenderd met vet cursief lettertype](sample.png)

*Afbeeldings‑alt‑tekst: Screenshot van tekst gerenderd met een vet‑cursief Arial‑lettertype in een C#‑console‑venster* – deze alt‑tekst voldoet aan de SEO‑vereiste voor afbeeldings‑alt‑tekst.

## Stap 5: Elegante fallback wanneer de lettertypefamilie niet beschikbaar is

Als de gevraagde familie (bijv. “Arial”) niet geïnstalleerd is, gooit de `Font`‑constructor een `ArgumentException`. Plaats de creatie in een `try/catch`‑blok en val terug op een bekend veilig lettertype zoals “Segoe UI”.

```csharp
Font font;
try
{
    font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
}
catch (ArgumentException)
{
    Console.WriteLine("Arial not found – falling back to Segoe UI.");
    font = new Font("Segoe UI", 12, FontStyle.Bold | FontStyle.Italic);
}
```

**Waarom dit afhandelen?** In gecontaineriseerde of headless omgevingen kan de standaardset lettertypen verschillen van een typische desktop. Het bieden van een fallback voorkomt runtime‑crashes en zorgt voor consistente styling.

## Volledig, uitvoerbaar voorbeeld

Alles samengevoegd, hier is een compleet programma dat je kunt kopiëren, plakken en uitvoeren:

```csharp
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create the font (bold + italic)
        Font font;
        try
        {
            font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
        }
        catch (ArgumentException)
        {
            Console.WriteLine("Arial not found – using Segoe UI as fallback.");
            font = new Font("Segoe UI", 12, FontStyle.Bold | FontStyle.Italic);
        }

        // Display font information
        Console.WriteLine($"Font family: {font.Name}");
        Console.WriteLine($"Size (pt): {font.Size}");
        Console.WriteLine($"Style: {font.Style}");

        // Render a sample image
        using (var bitmap = new Bitmap(300, 100))
        using (var graphics = Graphics.FromImage(bitmap))
        {
            graphics.Clear(Color.White);
            graphics.DrawString("Hello, World!", font, Brushes.Black, new PointF(10, 30));
            bitmap.Save("sample.png");
        }

        Console.WriteLine("Sample image saved as sample.png");
    }
}
```

### Hoe uit te voeren

1. Sla de code op in een bestand met de naam `Program.cs`.  
2. Open een terminal in de map van het bestand.  
3. Voer `dotnet new console -n FontDemo` uit (als je een project‑scaffold nodig hebt).  
4. Vervang de gegenereerde `Program.cs` door de bovenstaande code.  
5. Voer `dotnet add package System.Drawing.Common` uit (vereist voor .NET Core/5+).  
6. Bouw en voer uit met `dotnet run`.  

Je ziet de console‑output die de lettertype‑eigenschappen bevestigt, en `sample.png` verschijnt in de projectmap.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Valkuil | Waarom het gebeurt | Oplossing |
|---------|--------------------|-----------|
| **Ontbrekend `System.Drawing.Common`‑pakket** | .NET Core bevat `System.Drawing` niet standaard. | Voer `dotnet add package System.Drawing.Common` uit. |
| **Lettertypefamilie niet geïnstalleerd** | Headless Docker‑images missen vaak Windows‑lettertypen. | Gebruik een fallback‑lettertype of installeer de benodigde lettertypen in de container. |
| **Onjuiste gebruik van `|`** | Het gebruiken van `+` in plaats van `|` leidt tot een ongeldige combinatie. | Combineer `FontStyle`‑waarden altijd met de bitwise OR‑operator (`|`). |
| **Het `Font`‑object niet vrijgeven** | Het niet aanroepen van `Dispose` kan GDI‑bronnen lekken. | Plaats `Font` in een `using`‑blok of roep `font.Dispose()` aan nadat je klaar bent. |

## Conclusie

Je weet nu hoe je **vet cursief lettertype kunt maken** in C# en hoe je **lettertype maakt in C#** veilig en efficiënt. De tutorial behandelde het importeren van de juiste namespace, het combineren van `FontStyle`‑flags, het verifiëren van het resultaat, het renderen van een visueel voorbeeld, en het afhandelen van ontbrekende lettertypefamilies.

Vervolgens kun je verkennen:

* **Onderstreepte of doorgestreepte lettertypen maken** – voeg `FontStyle.Underline` of `FontStyle.Strikeout` toe.  
* **Aangepaste TrueType‑lettertypen gebruiken** – laad een `.ttf`‑bestand met `PrivateFontCollection`.  
* **Lettertypen toepassen in WinForms, WPF of PDF‑generatie** – hetzelfde `Font`‑object kan worden doorgegeven aan UI‑controls of externe bibliotheken.  

Voel je vrij om te experimenteren met verschillende families, groottes en stijlcombinaties. Als je problemen tegenkomt, raadpleeg dan opnieuw de tabel “Veelvoorkomende valkuilen” of bekijk de officiële [.NET‑documentatie voor System.Drawing.Font](https://learn.microsoft.com/dotnet/api/system.drawing.font). Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe je lettertypen programmatically combineert in C# – stapsgewijze gids](/html/indonesian/net/advanced-features/how-to-combine-fonts-programmatically-in-c-step-by-step-guid/)
- [HTML‑document maken met opgemaakte tekst en exporteren naar PDF – volledige gids](/html/english/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/)
- [docx naar png converteren – zip‑archief maken c# tutorial](/html/english/net/generate-jpg-and-png-images/convert-docx-to-png-create-zip-archive-c-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
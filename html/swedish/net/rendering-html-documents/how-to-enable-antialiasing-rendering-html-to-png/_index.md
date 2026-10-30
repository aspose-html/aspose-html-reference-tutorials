---
category: general
date: 2026-07-08
description: Lär dig hur du aktiverar kantutjämning när du renderar HTML till PNG
  med Aspose HTML. Denna guide täcker också hur du konverterar HTML till bild och
  sparar HTML som PNG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable antialiasing
- render html to png
- convert html to image
- save html as png
- aspose html to png
language: sv
lastmod: 2026-07-08
og_description: Hur du aktiverar kantutjämning när du renderar HTML till PNG med Aspose
  HTML. Följ den här steg‑för‑steg‑handledningen för att konvertera HTML till bild
  och spara HTML som PNG.
og_image_alt: Screenshot of HTML rendered to PNG with antialiasing enabled – how to
  enable antialiasing
og_title: Hur du aktiverar kantutjämning vid rendering av HTML till PNG – Aspose‑guide
schemas:
- author: Aspose
  dateModified: '2026-07-08'
  description: Learn how to enable antialiasing when you render HTML to PNG using
    Aspose HTML. This guide also covers convert html to image and save html as png.
  headline: How to Enable Antialiasing Rendering HTML to PNG
  type: TechArticle
- description: Learn how to enable antialiasing when you render HTML to PNG using
    Aspose HTML. This guide also covers convert html to image and save html as png.
  name: How to Enable Antialiasing Rendering HTML to PNG
  steps:
  - name: '**HTMLDocument** – works entirely in memory, so you don’t need any physical
      `.html` files. Perfect for on‑the‑fly conversions.'
    text: '**HTMLDocument** – works entirely in memory, so you don’t need any physical
      `.html` files. Perfect for on‑the‑fly conversions.'
  - name: '**WebFontStyle** – shows that you can style text before rendering; the
      bold‑italic combo is just a demo.'
    text: '**WebFontStyle** – shows that you can style text before rendering; the
      bold‑italic combo is just a demo.'
  - name: '**ImageRenderingOptions.UseAntialiasing** – this flag is the answer to
      **how to enable antialiasing**; set it to `true` and the rasterizer will smooth
      edges.'
    text: '**ImageRenderingOptions.UseAntialiasing** – this flag is the answer to
      **how to enable antialiasing**; set it to `true` and the rasterizer will smooth
      edges.'
  - name: '**TextOptions.UseHinting** – hinting improves the clarity of glyphs, especially
      at small sizes. It’s a nice companion to antialiasing.'
    text: '**TextOptions.UseHinting** – hinting improves the clarity of glyphs, especially
      at small sizes. It’s a nice companion to antialiasing.'
  - name: '**ImageSaveOptions** – bundles both rendering and text options, then tells
      Aspose to output a PNG file.'
    text: '**ImageSaveOptions** – bundles both rendering and text options, then tells
      Aspose to output a PNG file.'
  type: HowTo
tags:
- Aspose
- C#
- Image Rendering
title: Hur man aktiverar kantutjämning vid rendering av HTML till PNG
url: /sv/net/rendering-html-documents/how-to-enable-antialiasing-rendering-html-to-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man aktiverar antialiasing vid rendering av HTML till PNG

Har du någonsin undrat **how to enable antialiasing** när du omvandlar en webbsida till en skarp PNG-bild? Du är inte ensam—många utvecklare stöter på problem när resultatet ser hackigt eller suddigt ut. Den goda nyheten är att med Aspose.HTML kan du jämna ut kanterna med bara några rader kod. I den här handledningen går vi igenom de exakta stegen för att rendera HTML till PNG, konvertera HTML till bild, och slutligen **save HTML as PNG** med antialiasing aktiverat.

> **What you’ll get:** en komplett, färdig‑att‑köra C#‑exempel, en förklaring av varje alternativ, och tips för att hantera kantfall som anpassade typsnitt eller stora sidor.

## Hur man aktiverar antialiasing vid rendering av HTML till PNG

Det första du behöver förstå är **why antialiasing matters**. När renderingsmotorn ritar former eller text approximera den kurvor med pixlar. Utan antialiasing skapar dessa approximationer trappsteg‑artefakter—särskilt märkbara på diagonala linjer eller tunna typsnitt. Att aktivera antialiasing får motorn att blanda närliggande pixlar, vilket ger ett mjukare visuellt resultat.

Nedan är kärnkoden som demonstrerar **how to enable antialiasing** med Aspose.HTML:s `ImageRenderingOptions`. Vi kommer att gå igenom den steg‑för‑steg så att du kan se exakt vad varje rad gör.

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Drawing;

// Step 1: Create an in‑memory HTML document
HTMLDocument htmlDoc = new HTMLDocument("<html><body><h1>Sample</h1></body></html>");

// Step 2: Define the desired font style (bold + italic)
WebFontStyle fontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

// Step 3: Configure image rendering options – enable antialiasing for smoother graphics
ImageRenderingOptions imageOpts = new ImageRenderingOptions();
imageOpts.UseAntialiasing = true;

// Step 4: Configure text rendering options – enable hinting for clearer text
TextOptions textOpts = new TextOptions();
textOpts.UseHinting = true;

// Step 5: Combine rendering and text options into PNG save options
ImageSaveOptions pngSaveOpts = new ImageSaveOptions(SaveFormat.Png)
{
    RenderingOptions = imageOpts,
    TextOptions = textOpts
};

// Step 6: Save the HTML document as a PNG image using the configured options
htmlDoc.Save("YOUR_DIRECTORY/sample.png", pngSaveOpts);
```

### Varför varje del är viktig

1. **HTMLDocument** – fungerar helt i minnet, så du behöver inga fysiska `.html`‑filer. Perfekt för on‑the‑fly‑konverteringar.
2. **WebFontStyle** – visar att du kan formatera text innan rendering; kombinationen fet‑kursiv är bara en demo.
3. **ImageRenderingOptions.UseAntialiasing** – den här flaggan är svaret på **how to enable antialiasing**; sätt den till `true` så jämnar rasteriseraren kanterna.
4. **TextOptions.UseHinting** – hinting förbättrar tydligheten hos glyfer, särskilt i små storlekar. Det är en bra följeslagare till antialiasing.
5. **ImageSaveOptions** – samlar både renderings- och textalternativ, och instruerar sedan Aspose att skapa en PNG‑fil.

## Rendera HTML till PNG med Aspose

Nu när du vet **how to enable antialiasing**, låt oss prata om den bredare bilden av **render html to png**. Aspose.HTML abstraherar bort det tunga arbetet:

- **Automatic layout** – motorn parsar CSS, beräknar box‑modeller och placerar element precis som en webbläsare.
- **Resolution control** – du kan ange DPI via `ImageRenderingOptions.Resolution`, vilket är praktiskt för högupplösta utskrifter.
- **Background handling** – sätt `imageOpts.BackgroundColor` om du behöver en transparent eller färgad canvas.

Här är en snabb justering som lägger till en anpassad DPI:

```csharp
imageOpts.Resolution = new SizeF(300, 300); // 300 DPI for print‑quality PNG
```

> **Pro tip:** Om du konverterar en sida som innehåller externa resurser (bilder, typsnitt), se till att sätta `htmlDoc.BaseUrl` till mappen som innehåller dessa tillgångar. Annars kommer renderaren att hoppa över dem.

## Konvertera HTML till bild – avancerade alternativ

Frasen **convert html to image** innebär ofta mer än bara PNG. Aspose stödjer JPEG, BMP, TIFF och till och med GIF. Att byta format är så enkelt som att ändra `SaveFormat`‑enum:

```csharp
ImageSaveOptions jpegOpts = new ImageSaveOptions(SaveFormat.Jpeg)
{
    RenderingOptions = imageOpts,
    TextOptions = textOpts,
    Quality = 90 // JPEG quality (0‑100)
};

htmlDoc.Save("sample.jpg", jpegOpts);
```

När du behöver vektor‑vänlig output, överväg `SvgSaveOptions`. Samma renderingspipeline gäller, så du får konsekvent antialiasing över format.

### Kantfall: Mycket långa sidor

Om din HTML är längre än en vanlig skärm, kommer Aspose som standard att skapa en enda hög bild. Det kan öka minnesanvändningen kraftigt. För att mildra detta kan du dela dokumentet i flera sidor:

```csharp
var pageHeight = 1080; // pixels
var totalHeight = htmlDoc.DocumentElement.ScrollHeight;
for (int offset = 0; offset < totalHeight; offset += pageHeight)
{
    imageOpts.Viewport = new RectangleF(0, offset, htmlDoc.DocumentElement.ScrollWidth, pageHeight);
    htmlDoc.Save($"page_{offset / pageHeight}.png", pngSaveOpts);
}
```

## Spara HTML som PNG – sista steget

Vid detta tillfälle har du sett **how to enable antialiasing**, du har lärt dig att **render html to png**, och du har utforskat **convert html to image**‑alternativ. Den sista handlingen—**save html as png**—är redan demonstrerad i originalsnutten, men låt oss paketera den i en återanvändbar metod:

```csharp
public static void SaveHtmlAsPng(string html, string outputPath, bool antialias = true)
{
    // Create document
    var doc = new HTMLDocument(html);

    // Rendering options
    var imgOpts = new ImageRenderingOptions
    {
        UseAntialiasing = antialias,
        Resolution = new SizeF(96, 96) // default screen DPI
    };

    // Text options
    var txtOpts = new TextOptions { UseHinting = true };

    // Combine into save options
    var saveOpts = new ImageSaveOptions(SaveFormat.Png)
    {
        RenderingOptions = imgOpts,
        TextOptions = txtOpts
    };

    // Save
    doc.Save(outputPath, saveOpts);
}
```

Du kan nu anropa `SaveHtmlAsPng("<html>…</html>", @"C:\temp\output.png")` från var som helst i ditt projekt. `antialias`‑parametern låter dig växla den mjuka kant‑funktionen, vilket ger dig full kontroll över **how to enable antialiasing** vid körning.

## Aspose HTML till PNG – fullt fungerande exempel

Nedan är en fristående konsolapplikation som samlar allt. Kopiera‑klistra, justera `YOUR_DIRECTORY`‑platshållaren, och kör den med .NET 6 eller senare.



## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man använder Aspose för att rendera HTML till PNG – Steg‑för‑steg‑guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [Hur man renderar HTML till PNG med Aspose – Komplett guide](/html/english/net/rendering-html-documents/how-to-render-html-to-png-with-aspose-complete-guide/)
- [Rendera HTML som PNG i .NET med Aspose.HTML](/html/english/net/rendering-html-documents/render-html-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-01-14
description: hur man ställer in dpi när man konverterar en URL till PNG. Lär dig rendera
  HTML till PNG, ställa in viewport‑storlek och spara HTML som PNG med Aspose.HTML
  i Java.
draft: false
keywords:
- how to set dpi
- render html to png
- convert url to png
- set viewport size
- save html as png
language: sv
og_description: hur man ställer in dpi när man konverterar en URL till PNG. Steg‑för‑steg‑guide
  för att rendera HTML till PNG, kontrollera viewport‑storlek och spara HTML som PNG
  med Aspose.HTML.
og_title: hur man ställer in dpi – Rendera HTML till PNG med AsposeHTML
tags:
- AsposeHTML
- Java
- image rendering
title: hur man ställer in dpi – Rendera HTML till PNG med AsposeHTML
url: /sv/java/conversion-html-to-various-image-formats/how-to-set-dpi-render-html-to-png-with-asposehtml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hur man ställer in dpi – Rendera HTML till PNG med AsposeHTML

Har du någonsin undrat **hur man ställer in dpi** för en skärmbild‑liknande bild som genereras från en webbsida? Kanske behöver du en 300 DPI PNG för utskrift, eller en låg‑upplöst miniatyr för en mobilapp. I båda fallen är tricket att tala om för renderingsmotorn vilken logisk DPI du vill ha, och sedan låta den göra det tunga arbetet.  

I den här handledningen tar vi en live‑URL, renderar den till en PNG‑fil, **ställer in viewport‑storleken**, justerar DPI, och slutligen **sparar HTML som PNG**—allt med Aspose.HTML för Java. Inga externa webbläsare, inga röriga kommandoradsverktyg—bara ren Java‑kod som du kan lägga in i vilket Maven‑ eller Gradle‑projekt som helst.

> **Pro tip:** Om du bara vill ha en snabb miniatyr kan du behålla DPI på 96 DPI (standard för de flesta skärmar). För utskriftsklara resurser, höj den till 300 DPI eller högre.

![exempel på hur man ställer in dpi](https://example.com/images/how-to-set-dpi.png "exempel på hur man ställer in dpi")

## Vad du behöver

- **Java 17** (eller någon nyare JDK).  
- **Aspose.HTML for Java** 24.10 eller nyare. Du kan hämta den från Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>24.10</version>
</dependency>
```

- En internetanslutning för att hämta målsidan (exemplet använder `https://example.com/sample.html`).  
- Skrivrättigheter till utdata‑mappen.

Det är allt—ingen Selenium, ingen headless Chrome. Aspose.HTML gör renderingen i‑process, vilket betyder att du stannar inom JVM och undviker overheaden av att starta en webbläsare.

## Steg 1 – Ladda HTML‑dokumentet från en URL

Först skapar vi en `HTMLDocument`‑instans som pekar på sidan vi vill fånga. Konstruktorn laddar automatiskt ner HTML, parsar den och förbereder DOM‑en.

```java
import com.aspose.html.HTMLDocument;
import java.nio.file.Paths;

// Load the remote page
HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");
```

*Varför detta är viktigt:* Genom att ladda dokumentet direkt hoppar du över behovet av en separat HTTP‑klient. Aspose.HTML respekterar omdirigeringar, cookies och även grundläggande autentisering om du bäddar in referenser i URL‑en.

## Steg 2 – Bygg en sandbox med önskad DPI och viewport

En **sandbox** är Aspose.HTML:s sätt att efterlikna en webbläsarmiljö. Här får vi den att låtsas vara en 1280 × 720‑skärm och, avgörande, vi ställer in **device DPI**. Att ändra DPI förändrar bildens pixeldensitet utan att ändra den logiska storleken.

```java
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;

// Create a sandbox that simulates a 1280×720 screen at 96 DPI
SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
        .setViewportSize(1280, 720)          // width, height in pixels
        .setDeviceDpi(96)                    // logical DPI (change to 300 for print)
        .setUserAgent("AsposeHTML/24.10")    // optional custom user‑agent
        .build();

// Apply the sandbox to the document
htmlDoc.setSandbox(sandbox);
```

*Varför du kan vilja justera dessa värden:*  
- **Viewport‑storlek** styr hur CSS‑media‑queries (`@media (max-width: …)`) beter sig.  
- **Device DPI** påverkar den fysiska storleken på bilden när den skrivs ut. En 96 DPI‑bild ser bra ut på skärmar; en 300 DPI‑bild behåller skärpan på papper.

Om du behöver en fyrkantig miniatyr, ändra helt enkelt `setViewportSize(500, 500)` och håll DPI låg.

## Steg 3 – Välj PNG som utdataformat

Aspose.HTML stödjer flera rasterformat (PNG, JPEG, BMP, GIF). PNG är förlustfri, vilket gör den perfekt för skärmbilder där du vill ha varje pixel bevarad.

```java
import com.aspose.html.rendering.ImageSaveOptions;

// Prepare PNG save options
ImageSaveOptions pngOptions = new ImageSaveOptions();
pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);
```

Du kan också justera komprimeringsnivån (`pngOptions.setCompressionLevel(9)`) om du är orolig för filstorleken.

## Steg 4 – Rendera och spara bilden

Nu instruerar vi dokumentet att **spara** sig själv som en bild. `save`‑metoden tar en filsökväg och de tidigare konfigurerade alternativen.

```java
// Define the output path (replace with your own directory)
String outputPath = "YOUR_DIRECTORY/sandboxed.png";

// Render the document to a PNG file
htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

System.out.println("Rendering completed.");
```

När programmet är klart hittar du en PNG‑fil på `YOUR_DIRECTORY/sandboxed.png`. Öppna den—om du har ställt in DPI till 300 kommer bildmetadata att återspegla det, även om pixelmåtten fortfarande är 1280 × 720.

## Steg 5 – Verifiera DPI (valfritt men praktiskt)

Om du vill dubbelkolla att DPI verkligen har tillämpats kan du läsa PNG‑metadata med ett lättviktigt bibliotek som **metadata‑extractor**:

```java
import com.drew.imaging.ImageMetadataReader;
import com.drew.metadata.png.PngDirectory;

File pngFile = new File(outputPath);
var metadata = ImageMetadataReader.readMetadata(pngFile);
var pngDir = metadata.getFirstDirectoryOfType(PngDirectory.class);
int dpi = pngDir.getInt(PngDirectory.TAG_PIXELS_PER_UNIT_X);
System.out.println("DPI stored in PNG: " + dpi);
```

Du bör se `300` (eller vad du än har angett) skrivet till konsolen. Detta steg krävs inte för rendering, men det är en snabb kontroll, särskilt när du genererar resurser för ett utskriftsflöde.

## Vanliga frågor & kantfall

### ”Vad händer om sidan använder JavaScript för att ladda innehåll?”

Aspose.HTML kör ett **begränsat delmängd** av JavaScript. För de flesta statiska webbplatser fungerar det direkt. Om sidan starkt förlitar sig på klient‑side‑ramverk (React, Angular, Vue) kan du behöva för‑rendera sidan eller använda en headless‑browser istället. DPI‑inställningen fungerar dock på samma sätt när DOM‑en är klar.

### ”Kan jag rendera en PDF istället för PNG?”

Absolut. Byt `ImageSaveOptions` mot `PdfSaveOptions` och ändra utdata‑filändelsen till `.pdf`. DPI‑inställningen påverkar fortfarande det rasteriserade utseendet på eventuella inbäddade bilder.

### ”Vad gäller högupplösta skärmbilder för retina‑skärmar?”

Dubbel helt enkelt viewport‑dimensionerna samtidigt som du behåller DPI på 96 DPI, eller behåll viewporten och höj DPI till 192. Den resulterande PNG‑filen kommer att innehålla dubbelt så många pixlar, vilket ger den skarpa retina‑känslan.

### ”Behöver jag rensa resurser?”

`HTMLDocument` implementerar `AutoCloseable`. I en produktionsapp, omslut den i ett try‑with‑resources‑block:

```java
try (HTMLDocument doc = new HTMLDocument(url)) {
    // configure sandbox, render, etc.
}
```

Det säkerställer att inhemska resurser frigörs omedelbart.

## Fullt fungerande exempel (klar att kopiera‑klistra in)

Nedan är det kompletta, klar‑att‑köra‑programmet. Ersätt `YOUR_DIRECTORY` med en faktisk mapp på din maskin.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.ImageSaveOptions;
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;
import java.nio.file.Paths;

public class RenderHtmlToPng {
    public static void main(String[] args) {
        // 1️⃣ Load the HTML document from a URL
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");

        // 2️⃣ Create a sandbox – set viewport size and DPI
        SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
                .setViewportSize(1280, 720)   // width × height in pixels
                .setDeviceDpi(96)             // change to 300 for print‑ready PNG
                .setUserAgent("AsposeHTML/24.10")
                .build();

        htmlDoc.setSandbox(sandbox); // apply sandbox to the document

        // 3️⃣ Prepare PNG save options
        ImageSaveOptions pngOptions = new ImageSaveOptions();
        pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);

        // 4️⃣ Render and save
        String outputPath = "YOUR_DIRECTORY/sandboxed.png";
        htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

        System.out.println("Rendering completed. Check: " + outputPath);
    }
}
```

Kör klassen, så får du en PNG som respekterar **hur man ställer in dpi**‑inställningen du angav.

## Slutsats

Vi har gått igenom **hur man ställer in dpi** när du **renderar HTML till PNG**, täckt steget **set viewport size**, och visat hur du **sparar HTML som PNG** med Aspose.HTML för Java. De viktigaste slutsatserna är:

- Använd en **sandbox** för att kontrollera DPI och viewport.  
- Välj rätt **ImageSaveOptions** för förlustfri utdata.  
- Verifiera DPI‑metadata om du behöver garantera utskriftskvalitet.

Härifrån kan du experimentera med olika DPI‑värden, större viewports, eller till och med batch‑processa en lista med URL:er. Vill du konvertera en hel webbplats till PNG‑miniatyrer? Loopa bara över en array med URL:er och återanvänd samma sandbox‑konfiguration.

Lycka till med rendering, och må dina skärmbilder alltid vara pixel‑perfekta!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
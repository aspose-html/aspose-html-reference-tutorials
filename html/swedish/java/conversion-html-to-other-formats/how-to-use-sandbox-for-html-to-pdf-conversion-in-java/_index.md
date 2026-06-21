---
category: general
date: 2026-03-29
description: Hur man använder sandbox för att säkert konvertera HTML till PDF i Java
  – ställ in användaragent, skärmstorlek och DPI för perfekta resultat.
draft: false
keywords:
- how to use sandbox
- convert html to pdf
- generate pdf from html
- set user agent
- html to pdf java
language: sv
og_description: Hur man använder sandbox för att konvertera HTML till PDF i Java.
  Lär dig att ställa in användaragent, skärmstorlek och DPI för pålitlig PDF‑utmatning.
og_title: Hur man använder Sandbox – HTML‑till‑PDF‑guide för Java
tags:
- Aspose.HTML
- Java
- PDF generation
title: Hur man använder Sandbox för HTML‑till‑PDF‑konvertering i Java
url: /sv/java/conversion-html-to-other-formats/how-to-use-sandbox-for-html-to-pdf-conversion-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder Sandbox för HTML‑till‑PDF‑konvertering i Java

Har du någonsin undrat **how to use sandbox** när du omvandlar webbsidor till PDF‑filer? Du är inte ensam—många Java‑utvecklare stöter på problem när CSS @media‑regler ignorerar de dimensioner de anger, eller när en fjärrplats blockerar standard‑user‑agent. Den goda nyheten? En sandbox ger dig en kontrollerad miljö där du bestämmer skärmstorlek, DPI och till och med tidszonen, vilket säkerställer att den genererade PDF‑filen ser exakt ut som du förväntar dig.

I den här handledningen går vi igenom hela processen för **how to use sandbox** med Aspose.HTML, från att konfigurera skärmdimensioner till att ange en anpassad user‑agent, och slutligen konvertera en HTML‑fil till en PDF. I slutet kommer du kunna **convert HTML to PDF** på ett pålitligt sätt, **generate PDF from HTML** med vilka inställningar du vill, och du vet hur du **set user agent**‑strängar som vissa webbtjänster kräver. Inga externa verktyg, bara ett enda, självständigt Java‑program.

> **What you’ll get:** en färdig‑att‑köra `SandboxTutorial.java`‑fil, en förklaring av varje rad, och tips för vanliga fallgropar (som saknade teckensnitt eller tidszons‑missmatchar). Låt oss dyka ner.

---

## Förutsättningar

- **Java 17** eller nyare installerat (koden använder try‑with‑resources, som finns sedan Java 7, men vi rekommenderar den senaste LTS).
- **Aspose.HTML for Java**‑bibliotek (version 23.10 eller senare). Lägg till Maven‑beroendet eller ladda ner JAR‑filen från Aspose‑webbplatsen.
- En enkel HTML‑fil (`input.html`) som du vill omvandla till en PDF. Den kan innehålla CSS, bilder eller JavaScript—Aspose.HTML hanterar allt.
- En IDE eller en textredigerare; vi använder Visual Studio Code i skärmbilderna, men vilken Java‑IDE som helst fungerar.

> **Proffstips:** Om du använder Maven, lägg till följande i din `pom.xml`:
> ```xml
> <dependency>
>     <groupId>com.aspose</groupId>
>     <artifactId>aspose-html</artifactId>
>     <version>23.10</version>
> </dependency>
> ```

---

## Så här använder du Sandbox – Ställa in miljön

Det första du behöver veta om **how to use sandbox** är att det inte är en magisk svart låda; det är ett tunt omslag runt en separat process som respekterar de alternativ du ger den. Tänk på det som en mini‑browser som körs i en bur, och följer dina regler.

```java
// Step 1: Import required Aspose.HTML classes
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.converters.Converter;
```

> **Why these imports?** `DocumentSandbox` skapar den isolerade miljön, `SandboxOptions` låter dig justera skärmstorlek, DPI, user‑agent osv., och `Converter` gör det tunga arbetet med att omvandla HTML till PDF.

### Konfigurera skärmstorlek, DPI och tidszon

```java
// Step 2: Define sandbox configuration (screen size, DPI, user‑agent, time zone)
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(1280);               // width in pixels
sandboxOptions.setScreenHeight(720);               // height in pixels
sandboxOptions.setDevicePixelRatio(2.0);           // high‑DPI (retina) scaling
sandboxOptions.setUserAgent("AsposeHTML/1.0 (CI)"); // custom user‑agent string
sandboxOptions.setTimeZone("UTC");                // forces UTC for consistent timestamps
```

- **Screen width/height** påverkar CSS‑media‑queries som `@media (max-width: 600px)`. Om du hoppar över detta använder sandbox standardvärdet 1024 × 768, vilket kan trigga ett mobil‑layout du inte förväntade dig.
- **Device pixel ratio** påverkar hur bilder och vektorgrafik rasteriseras. Att sätta den till `2.0` ger dig skarpa, retina‑klara PDF‑filer.
- **User‑agent** är avgörande när mål‑webbplatsen levererar olika markup till olika webbläsare. Genom att **set user agent** till en sträng som efterliknar en riktig webbläsare undviker du att få en “no‑script”‑version.
- **Time zone** är viktigt för datum‑relaterad JavaScript. Att använda UTC säkerställer reproducerbara resultat över utvecklare och CI‑pipelines.

---

## Konvertera HTML till PDF i en Sandbox

Nu när sandboxen är konfigurerad, låt oss se **how to use sandbox** för att faktiskt **convert HTML to PDF**. Konverteringen måste ske *inuti* sandboxen; annars kommer CSS `@media`‑regler att läsa värden från värddatorns dimensioner, vilket förstör layouten.

```java
// Step 3: Create a sandbox instance with the configured options
try (DocumentSandbox sandbox = new DocumentSandbox(sandboxOptions)) {

    // Step 4: Run the conversion inside the sandbox so CSS @media rules use the defined dimensions
    sandbox.run(() -> {
        // Convert input.html to sandboxed.pdf using the options defined above
        Converter.convert("YOUR_DIRECTORY/input.html", "YOUR_DIRECTORY/sandboxed.pdf");
    });
}
```

> **What’s happening here?**  
> 1. `DocumentSandbox` startar en separat process med de alternativ vi definierade.  
> 2. `sandbox.run` tar emot en lambda (kodblocket) som körs *inuti* den processen.  
> 3. `Converter.convert` läser `input.html`, renderar den med sandboxens virtuella skärm och skriver `sandboxed.pdf`.

Om du kör programmet nu bör du se en `sandboxed.pdf`‑fil bredvid din käll‑HTML. Öppna den—matchar layouten vad du ser i en vanlig webbläsare på 1280 × 720? Om ja har du bemästrat **how to use sandbox** för PDF‑generering.

---

## Generera PDF från HTML med en anpassad User Agent

Ibland blockerar webbplatsen du konverterar okända webbläsare. Det är då **set user agent** kommer till sin rätt. Låt oss justera exemplet så att det efterliknar Chrome på Windows:

```java
sandboxOptions.setUserAgent(
    "Mozilla/5.0 (Windows NT 10.0; Win64; x64) " +
    "AppleWebKit/537.36 (KHTML, like Gecko) " +
    "Chrome/124.0.0.0 Safari/537.36"
);
```

Kör programmet igen och jämför PDF‑filen med den som genererades med den generiska AsposeHTML‑user‑agenten. Du kommer märka skillnader i teckensnitt, ikoner eller till och med dolda element som bara visas för Chrome. Detta demonstrerar **how to use sandbox** för att styra request‑headern, ett viktigt knep för pålitliga **html to pdf java**‑pipelines.

---

## Vanliga kantfall & hur man hanterar dem

| Situation | Varför det händer | Fix (using how to use sandbox) |
|-----------|-------------------|--------------------------------|
| Missing web fonts | Sandboxen har ingen åtkomst till OS‑teckensnittsmappen. | Lägg till `sandboxOptions.setFontFolder("/path/to/fonts")` eller bädda in teckensnitt i CSS med `@font-face`. |
| JavaScript errors | Sandboxen kör med en begränsad JavaScript‑motor. | Använd `sandboxOptions.setJavaScriptEnabled(true)` (standard) och säkerställ att du använder Aspose.HTML 23.10+ som stödjer modern JS. |
| Large images cause memory spikes | Hög DPI + stora bilder → enorma raster‑buffertar. | Reducera `DevicePixelRatio` till `1.0` eller för‑skala bilder i HTML‑koden. |
| Time‑zone‑specific content displays incorrectly | JavaScript `new Date()` använder värddatorns tidszon. | Att sätta `sandboxOptions.setTimeZone("UTC")` tvingar en konsekvent tidszon över byggprocesser. |

> **Tip:** Testa alltid med ett CI‑jobb som kör sandboxen i headless‑läge. Om jobbet misslyckas visar loggarna vilket alternativ som orsakade problemet, vilket gör felsökning enklare.

---

## Fullt fungerande exempel (Klar att kopiera och klistra in)

Nedan är den kompletta `SandboxTutorial.java`. Ersätt `YOUR_DIRECTORY` med den absoluta sökvägen till din projektmapp.

```java
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.converters.Converter;

public class SandboxTutorial {
    public static void main(String[] args) throws Exception {

        // Step 2: Define sandbox configuration (screen size, DPI, user‑agent, time zone)
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(1280);
        sandboxOptions.setScreenHeight(720);
        sandboxOptions.setDevicePixelRatio(2.0);
        sandboxOptions.setUserAgent("AsposeHTML/1.0 (CI)");
        sandboxOptions.setTimeZone("UTC");

        // OPTIONAL: Mimic Chrome if the site blocks generic agents
        // sandboxOptions.setUserAgent(
        //     "Mozilla/5.0 (Windows NT 10.0; Win64; x64) " +
        //     "AppleWebKit/537.36 (KHTML, like Gecko) " +
        //     "Chrome/124.0.0.0 Safari/537.36"
        // );

        // Step 3: Create a sandbox instance with the configured options
        try (DocumentSandbox sandbox = new DocumentSandbox(sandboxOptions)) {

            // Step 4: Run the conversion inside the sandbox so CSS @media rules use the defined dimensions
            sandbox.run(() -> {
                // Convert HTML to PDF
                Converter.convert("YOUR_DIRECTORY/input.html", "YOUR_DIRECTORY/sandboxed.pdf");
            });
        }

        System.out.println("PDF generated successfully at YOUR_DIRECTORY/sandboxed.pdf");
    }
}
```

**Expected output:** Efter att ha kört `java SandboxTutorial` kommer du se konsolmeddelandet *“PDF generated successfully at …”* och en fil med namnet `sandboxed.pdf`. Öppna den; sidan bör respektera layouten 1280 × 720, den hög‑DPI‑skalning och eventuell anpassad user‑agent‑logik du injicerade.

---

## Visuell översikt

![Diagram som illustrerar hur man använder sandbox för HTML‑till‑PDF‑konvertering](https://example.com/placeholder.png "diagram för hur man använder sandbox")

*Bilden visar flödet: Java‑kod → SandboxOptions → DocumentSandbox → Converter → PDF.*

---

## Sammanfattning – Vad vi gick igenom

- **How to use sandbox** för att isolera rendering, så att CSS‑media‑queries ser de dimensioner du anger.  
- **Convert HTML to PDF** på ett säkert sätt, utan bieffekter från värddatorns OS.  
- **Generate PDF from HTML** med en anpassad **set user agent**‑sträng för webbplatser som begränsar innehåll.  
- Hantera kantfall som saknade teckensnitt, Java

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
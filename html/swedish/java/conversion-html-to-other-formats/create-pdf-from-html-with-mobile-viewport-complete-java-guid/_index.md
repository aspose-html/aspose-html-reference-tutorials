---
category: general
date: 2026-03-18
description: Skapa PDF från HTML i Java snabbt. Lär dig hur du konverterar HTML till
  PDF, simulerar iPhone‑skärm och ställer in skärmstorlek för responsiva PDF‑filer.
draft: false
keywords:
- create pdf from html
- convert html to pdf
- simulate iphone screen
- how to set screen
- how to convert html
language: sv
og_description: Skapa PDF från HTML i Java. Den här guiden visar hur du konverterar
  HTML till PDF, simulerar en iPhone‑skärm och ställer in skärmstorlekar för perfekta
  responsiva PDF‑filer.
og_title: Skapa PDF från HTML med mobilvy – Java-handledning
tags:
- Java
- Aspose.HTML
- PDF
- Responsive Design
- Mobile Viewport
title: Skapa PDF från HTML med mobilvy – Komplett Java‑guide
url: /sv/java/conversion-html-to-other-formats/create-pdf-from-html-with-mobile-viewport-complete-java-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa PDF från HTML med mobilvy – Komplett Java‑guide

Har du någonsin behövt **create PDF from HTML** men resultatet såg ut som en skrivbordssida på en liten telefonskärm? Du är inte ensam. När du konverterar en responsiv webbplats till PDF ignorerar standard‑viewporten ofta mobil‑breakpoints, vilket lämnar dig med en trång röra.  

Den goda nyheten? Du kan **convert HTML to PDF** medan du **simulating an iPhone screen**, allt från ren Java‑kod. I den här handledningen går vi igenom varje steg—hur du ställer in skärmstorlek, hur du justerar device‑scale factor, och varför dessa inställningar är viktiga för en pixelperfekt PDF.

> **Pro tip:** Om du redan har använt Aspose.HTML för enkla konverteringar kommer du att hitta viewport‑justeringarna bara några extra rader bort.

---

## Vad du kommer att lära dig

* Hur man **create PDF from HTML** med Aspose.HTML för Java.  
* Den exakta koden för att **simulate iPhone screen** dimensioner (375 × 667 px @ 2× density).  
* Var du placerar **how to set screen**‑alternativen i konverterings‑pipeline.  
* Vanliga fallgropar när du konverterar responsiva sidor och hur du undviker dem.  
* Ett komplett, färdigt‑till‑körning Java‑exempel som du kan copy‑paste in i din IDE.

### Förutsättningar

* Java 17 eller nyare (koden kompilerar med äldre versioner, men 17 rekommenderas).  
* Aspose.HTML för Java‑biblioteket – du kan hämta den senaste JAR‑filen från [Aspose website](https://products.aspose.com/html/java).  
* En enkel HTML‑fil (`input.html`) som du vill omvandla till en PDF.  
* Grundläggande kunskap om Maven eller Gradle (vi visar ett Maven‑exempel).

---

## Steg 1 – Lägg till Aspose.HTML i ditt projekt

Först och främst behöver du biblioteket på din classpath. Om du använder Maven, lägg till detta beroende i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- Use the latest version -->
</dependency>
```

> **Why this matters:** Aspose.HTML sköter det tunga arbetet—parsing HTML, applying CSS, och rasterizing layouten. Utan det skulle du behöva skriva en fullständig webbläsarmotor själv, vilket är ett *massor* av arbete.

Om du föredrar Gradle, är motsvarigheten:

```groovy
implementation 'com.aspose:aspose-html:23.12'
```

---

## Steg 2 – Förbered Load Options och simulera en iPhone‑viewport

Nu ska vi konfigurera **how to set screen**‑parametrarna. Klassen `HtmlLoadOptions` låter dig tala om för Aspose vilken storlek och pixel‑densitet webbläsaren ska låtsas ha.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;

public class ViewportDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create load options for the HTML document
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();

        // 2️⃣ Simulate a mobile viewport (iPhone 6/7/8) – 375 × 667 pixels with retina density
        loadOptions.setScreenSize(new Size(375, 667));
        loadOptions.setDeviceScaleFactor(2.0);

        // 3️⃣ Convert the HTML file to PDF using the configured viewport
        Converter.convertDocument(
                "YOUR_DIRECTORY/input.html",          // source HTML
                "YOUR_DIRECTORY/output.pdf",          // destination PDF
                new PdfSaveOptions(),
                loadOptions);

        // 4️⃣ Notify that the conversion is complete
        System.out.println("Responsive conversion using mobile viewport.");
    }
}
```

### Varför dessa siffror?

* **375 × 667** motsvarar de logiska CSS‑pixel‑dimensionerna för en iPhone 6/7/8 i stående läge.  
* **DeviceScaleFactor = 2.0** talar om för renderaren att varje CSS‑pixel motsvarar två fysiska pixlar, vilket efterliknar Retina‑displayen.

Om du behöver en annan enhet—t.ex. en iPhone 12 Pro Max—skulle du ändra storleken till `428 × 926` och behålla scale‑faktorn på `3.0`.

---

## Steg 3 – Kör konverteringen och verifiera resultatet

Kompilera och kör klassen:

```bash
mvn compile exec:java -Dexec.mainClass=ViewportDemo
```

Efter att programmet har avslutats, öppna `output.pdf`. Du bör se:

* Alla media queries som riktar sig mot `max-width: 375px` tillämpas korrekt.  
* Bilder renderas skarpt tack vare 2× scale‑faktorn.  
* Text som respekterar den mobila font‑size‑hierarkin du definierat i CSS.

Om PDF‑filen fortfarande ser ut som en skrivbordssida, dubbelkolla att din HTML använder responsiva meta‑taggar:

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

Utan den taggen kommer även en perfekt viewport‑inställning inte att trigga den mobila stylesheeten.

---

## Steg 4 – Hantera externa resurser (bilder, typsnitt, CSS)

När du **convert HTML to PDF**, försöker Aspose.HTML hämta varje länkad resurs. Om du konverterar en sida som finns på ett lokalt filsystem fungerar absoluta URL:er (`file:///…`) bra. För fjärrresurser kan du stöta på:

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **404‑fel för bilder** | HTML‑filen pekar på en URL som kräver autentisering. | Använd `HtmlLoadOptions.setBaseUrl("file:///C:/myproject/")` för att lösa relativa sökvägar, eller bädda in bilder som Base64. |
| **Saknade webbtypsnitt** | PDF‑motorn kan inte ladda ner typsnittsfilen. | Ladda ner `.woff`/`.ttf`‑filerna lokalt och referera dem med en relativ sökväg. |
| **CSS tillämpas inte** | CSS‑filen blockeras av CORS. | Värd CSS på en server som tillåter cross‑origin‑förfrågningar, eller inlinea CSS i HTML. |

Ett snabbt sätt att testa resurshämtning är att omsluta konverteringsanropet i ett try‑catch‑block och skriva ut `Exception`‑meddelandet. Aspose.HTML ger detaljerade loggar som pekar på den exakta URL:en som misslyckades.

```java
try {
    Converter.convertDocument(...);
} catch (Exception ex) {
    System.err.println("Conversion failed: " + ex.getMessage());
}
```

---

## Steg 5 – Avancerade justeringar (valfritt)

### a) Ändra PDF‑sidstorlek

Som standard skapar Aspose.HTML en PDF‑sida som matchar viewport‑storleken. Om du föredrar A4 eller Letter, lägg till en `PdfSaveOptions`‑konfiguration:

```java
PdfSaveOptions pdfOptions = new PdfSaveOptions();
pdfOptions.setPageSize(PageSize.A4);
Converter.convertDocument("input.html", "output.pdf", pdfOptions, loadOptions);
```

### b) Lägg till en header/footer programatiskt

Du kan injicera en enkel header/footer efter konvertering med Aspose.PDF (ett separat bibliotek). Arbetsflödet är:

1. Konvertera HTML → PDF (som visat).  
2. Öppna den resulterande PDF‑filen med Aspose.PDF.  
3. Lägg till `HeaderFooter`‑objekt på varje sida.

```java
import com.aspose.pdf.*;

Document pdfDoc = new Document("output.pdf");
for (Page page : pdfDoc.getPages()) {
    page.addHeaderFooter(new HeaderFooter("Generated on " + LocalDate.now()));
}
pdfDoc.save("output-with-header.pdf");
```

### c) Batch‑konvertering

Om du har en mapp med HTML‑filer, loopa över dem:

```java
Files.list(Paths.get("html_folder"))
     .filter(p -> p.toString().endsWith(".html"))
     .forEach(p -> {
         String pdfPath = p.toString().replace(".html", ".pdf");
         Converter.convertDocument(p.toString(), pdfPath, new PdfSaveOptions(), loadOptions);
     });
```

---

## Vanliga frågor (FAQ)

**Q: Fungerar detta med JavaScript‑tunga sidor?**  
A: Aspose.HTML stödjer en delmängd av JavaScript. Enkla DOM‑manipulationer och CSS‑ändringar fungerar vanligtvis, men komplexa ramverk (React, Angular) kan behöva en förrenderad statisk HTML‑snapshot.

**Q: Vad händer om jag behöver konvertera en sida som använder `@media print`‑regler?**  
A: Biblioteket respekterar `@media print` automatiskt. Men om du också sätter en mobil‑viewport kan `print`‑stylesheeten åsidosätta vissa mobila stilar. Testa båda scenarierna.

**Q: Kan jag ange ett eget DPI för PDF‑filen?**  
A: Ja. Använd `PdfSaveOptions.setDpi(300)` före konvertering. Högre DPI ger större filer men skarpare bilder.

---

## Förväntad resultat‑skärmbild

Nedan är en illustration av den slutliga PDF‑sidan (mobil‑viewport simulerad).  
![Screenshot of PDF generated by create pdf from html demo showing iPhone‑sized layout]  

*Bildens alt‑text innehåller huvudnyckelordet för SEO.*

---

## Slutsats

Du har nu ett robust **create pdf from html**‑arbetsflöde som respekterar mobila breakpoints, simulerar en iPhone‑skärm och ger dig full kontroll över sidans dimensioner. Genom att justera `HtmlLoadOptions` kan du svara på “**how to set screen**” för vilken enhet som helst, och genom att använda `Converter.convertDocument` har du bemästrat **how to convert html** i Java.

Redo för nästa utmaning? Prova att kombinera detta tillvägagångssätt med Aspose.PDF för att lägga till vattenstämplar, slå ihop flera PDF‑filer eller skydda dokumentet med ett lösenord. Och glöm inte att experimentera med andra enheter—byt bara `Size` och `DeviceScaleFactor`‑värdena för att matcha den pixel‑densitet du behöver.

Lycka till med kodandet, och må dina PDF‑filer alltid se lika skarpa ut på papper som på en telefonskärm! 

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
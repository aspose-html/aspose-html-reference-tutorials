---
date: 2025-11-29
description: Lär dig hur du konverterar HTML till XPS och justerar XPS‑sidstorlek
  med Aspose.HTML för Java. Kontrollera utdata mått enkelt.
language: sv
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Konvertera HTML till XPS och justera XPS‑sidstorlek med Aspose.HTML för Java
url: /java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konvertera HTML till XPS och justera XPS‑sidstorlek med Aspose.HTML för Java

## Quick Answers
- **Vad betyder “convert HTML to XPS”?** Det renderar ett HTML‑dokument till en XPS‑fil och bevarar layout och stil.  
- **Behöver jag en licens?** En gratis provversion fungerar för utveckling; en kommersiell licens krävs för produktion.  
- **Vilken Java‑version stöds?** Java 8 eller högre (JDK 11+ rekommenderas).  
- **Kan jag ändra sidstorlek?** Ja – Aspose.HTML låter dig ange anpassade dimensioner innan rendering.  
- **Hur lång tid tar konverteringen?** Vanligtvis under en sekund för standardsidor; större dokument kan ta längre tid.

## What is converting HTML to XPS?
Att konvertera HTML till XPS innebär att ta en webbaserad markup‑fil och producera ett XPS‑dokument (XML Paper Specification) – ett fast layout‑, utskriftsklart format som liknar PDF. Detta är användbart när du behöver högupplösta, enhetsoberoende dokument för arkivering eller utskrift från Java‑applikationer.

## Why adjust the XPS page size?
Att justera sidstorleken ger dig kontroll över de fysiska dimensionerna på det slutgiltiga dokumentet (t.ex. A4, Letter, anpassade etiketter). Det förhindrar oönskad skalning, säkerställer att innehållet passar perfekt och kan minska filstorleken genom att eliminera onödigt vitt utrymme.

## Prerequisites

Innan vi börjar, se till att du har följande förutsättningar på plats:

1. **Java Development Environment** – Java Development Kit (JDK) installerat på ditt system.  
2. **Aspose.HTML for Java Library** – Ladda ner och inkludera Aspose.HTML for Java‑biblioteket i ditt projekt. Du kan hitta biblioteket [här](https://releases.aspose.com/html/java/).  
3. **Input HTML File** – Förbered en HTML‑fil som du vill rendera och justera XPS‑sidstorlek för. Du kan använda din egen HTML‑fil för den här handledningen.

## Import Packages

Först, importera de klasser du behöver. Dessa paket ger dig åtkomst till dokumenthantering, rendering och sidinställningsfunktioner.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Step 1: Set the Input File Name

Läs in käll‑HTML‑filen med en `FileInputStream`. Denna ström matar den råa HTML‑koden till Aspose.HTML‑motorn.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

## Step 2: Create an HTML Document and Set Styles

Skapa en `HTMLDocument`‑instans som representerar innehållet du ska rendera. I det här exemplet injicerar vi också ett litet CSS‑block för att demonstrera styling – du kan fritt ersätta det med din egen markup.

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n" +
               "\n";

// ...
```

## Step 3: Create XPS Rendering Options

Instansiera `XpsRenderingOptions` för att hålla alla inställningar som påverkar konverteringen från HTML till XPS.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

## Step 4: Adjust the Page Size

Definiera en anpassad sidstorlek (bredd × höjd i punkter) och ange för renderaren om den ska expandera automatiskt till den bredaste sidan. Att sätta `adjustToWidestPage` till `false` bevarar exakt de dimensioner du anger.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

## Step 5: Render the Output

Slutligen, skapa en `XpsDevice` med de konfigurerade alternativen och rendera HTML‑dokumentet. Resultatet blir en fullständig XPS‑fil med de anpassade sidmåtten du angav.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Common Issues and Solutions

| Problem | Varför det händer | Lösning |
|---------|-------------------|---------|
| **Blank XPS output** | Inmatningsströmmen är inte stängd eller HTMLDocument pekar på fel fil. | Se till att `FileInputStream` är korrekt inlindad i ett try‑with‑resources‑block och att filvägen är korrekt. |
| **Page size not applied** | `adjustToWidestPage` lämnades som `true`. | Sätt `pageSetup.setAdjustToWidestPage(false);` som visas i Steg 4. |
| **Unsupported CSS** | Aspose.HTML stödjer en delmängd av CSS. | Håll dig till grundläggande layout, typsnitt och färger; undvik avancerade selektorer eller CSS Grid. |
| **LicenseException** | Kör utan en giltig licens i produktion. | Applicera din temporära eller köpta licens innan rendering (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Frequently Asked Questions

**Q: What is Aspose.HTML for Java?**  
A: Aspose.HTML for Java är ett Java‑bibliotek som låter utvecklare manipulera och konvertera HTML‑dokument till olika format, såsom XPS, PDF och bilder.

**Q: Where can I download Aspose.HTML for Java?**  
A: Du kan ladda ner Aspose.HTML for Java‑biblioteket från [den här länken](https://releases.aspose.com/html/java/).

**Q: Is there a free trial available for Aspose.HTML for Java?**  
A: Ja, du kan få en gratis provversion av Aspose.HTML for Java från [här](https://releases.aspose.com/).

**Q: How can I obtain a temporary license for Aspose.HTML for Java?**  
A: För att få en temporär licens för Aspose.HTML for Java, besök [denna sida](https://purchase.aspose.com/temporary-license/).

**Q: Can I get support for Aspose.HTML for Java?**  
A: Ja, du kan söka hjälp och support från Aspose‑gemenskapen på [Aspose Forum](https://forum.aspose.com/).

**Q: Can I convert HTML to XPS on a headless server?**  
A: Absolut. Aspose.HTML fungerar i miljöer utan GUI; se bara till att Java‑runtime är korrekt konfigurerad.

**Q: Does the library support custom page margins?**  
A: Ja. Använd `PageSetup.setMarginTop()`, `setMarginBottom()`, etc., innan du tilldelar `PageSetup` till renderingsalternativen.

## Conclusion

Vi har gått igenom hela processen för **konvertera HTML till XPS** och justera sidstorleken med Aspose.HTML för Java. Genom att följa dessa steg kan du skapa utskriftsklara XPS‑dokument som matchar dina exakta layoutkrav. Känn dig fri att experimentera med olika sidmått, stilar eller till och med lägga till sidhuvuden och sidfötter för att passa ditt projekts behov.

Om du har några frågor eller behöver ytterligare hjälp, utforska [Aspose.HTML for Java-dokumentationen](https://reference.aspose.com/html/java/) eller gå med i samtalet på [Aspose Forum](https://forum.aspose.com/).

---

**Senast uppdaterad:** 2025-11-29  
**Testat med:** Aspose.HTML for Java 24.11 (senaste vid skrivtillfället)  
**Författare:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
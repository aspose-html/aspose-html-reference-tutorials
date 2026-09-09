---
date: 2026-03-18
description: Lär dig hur du konverterar HTML till XPS och justerar XPS‑sidstorlek
  med Aspose.HTML för Java. Kontrollera enkelt utskriftsdimensionerna.
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Konvertera HTML till XPS och justera XPS‑sidstorlek med Aspose.HTML för Java
url: /sv/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konvertera HTML till XPS och justera XPS‑sidstorlek med Aspose.HTML för Java

## Snabba svar
- **Vad betyder “convert HTML to XPS”?** Det renderar ett HTML‑dokument till en XPS‑fil och bevarar layout och stil.  
- **Behöver jag en licens?** En gratis provversion fungerar för utveckling; en kommersiell licens krävs för produktion.  
- **Vilken Java‑version stöds?** Java 8 eller högre (JDK 11+ rekommenderas).  
- **Kan jag ändra sidstorlek?** Ja – Aspose.HTML låter dig ange anpassade dimensioner innan rendering.  
- **Hur lång tid tar konverteringen?** Vanligtvis under en sekund för standard‑sidor; större dokument kan ta längre tid.

## Vad är konvertering av HTML till XPS?
Att konvertera HTML till XPS innebär att ta en webbaserad markup‑fil och producera ett XPS‑dokument (XML Paper Specification) – ett fast layout‑, utskriftsklart format som liknar PDF. Detta är användbart när du behöver högupplösta, enhetsoberoende dokument för arkivering eller utskrift från Java‑applikationer.

## Varför justera XPS‑sidstorleken?
Att justera sidstorleken ger dig kontroll över de fysiska dimensionerna på det slutliga dokumentet (t.ex. A4, Letter, anpassade etiketter). Det förhindrar oönskad skalning, säkerställer att innehållet passar perfekt och kan minska filstorleken genom att eliminera onödigt vitt utrymme.

## Förutsättningar

Innan vi börjar, se till att du har följande förutsättningar på plats:

1. **Java Development Environment** – Java Development Kit (JDK) installerat på ditt system.  
2. **Aspose.HTML for Java Library** – Ladda ner och inkludera Aspose.HTML for Java‑biblioteket i ditt projekt. Du kan hitta biblioteket [här](https://releases.aspose.com/html/java/).  
3. **Input HTML File** – Förbered en HTML‑fil som du vill rendera och justera XPS‑sidstorlek för. Du kan använda din egen HTML‑fil för den här handledningen.

## Importera paket

Först importerar du de klasser du behöver. Dessa paket ger dig åtkomst till dokumenthantering, rendering och sidinställningsfunktioner.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Steg‑för‑steg‑guide

Nedan följer en kortfattad, numrerad genomgång som speglar de ursprungliga stegen samtidigt som extra kontext läggs till för tydlighet.

### Steg 1: Ange indatafilens namn

Läs in käll‑HTML‑filen med en `FileInputStream`. Denna ström matar den råa HTML‑koden till Aspose.HTML‑motorn.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

### Steg 2: Skapa ett HTML‑dokument och ange stilar

Skapa en `HTMLDocument`‑instans som representerar innehållet du ska rendera. I detta exempel injicerar vi också ett litet CSS‑block för att demonstrera styling – du kan fritt ersätta det med din egen markup.

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

### Steg 3: Skapa XPS‑renderingsalternativ

Instansiera `XpsRenderingOptions` för att hålla alla inställningar som påverkar konverteringen från HTML till XPS.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

### Steg 4: Justera sidstorleken  

**Hur man anger XPS‑sidstorlek** – Definiera en anpassad sidstorlek (bredd × höjd i punkter) och tala om för renderaren om den ska expandera automatiskt till den bredaste sidan. Att sätta `adjustToWidestPage` till `false` bevarar de exakta dimensioner du anger.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

### Steg 5: Rendera utdata

Slutligen skapar du en `XpsDevice` med de konfigurerade alternativen och renderar HTML‑dokumentet. Resultatet är en fullständig XPS‑fil med de anpassade siddimensioner du angav.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Vanliga problem och lösningar

| Problem | Varför det händer | Lösning |
|---------|-------------------|--------|
| **Tom XPS‑utdata** | Inmatningsströmmen är inte stängd eller HTMLDocument pekar på fel fil. | Se till att `FileInputStream` är korrekt inlindad i ett try‑with‑resources‑block och att filvägen är korrekt. |
| **Sidstorlek tillämpas inte** | `adjustToWidestPage` är kvar på `true`. | Ange `pageSetup.setAdjustToWidestPage(false);` som visas i Steg 4. |
| **CSS stöds inte** | Aspose.HTML stödjer en delmängd av CSS. | Håll dig till grundläggande layout, typsnitt och färger; undvik avancerade selektorer eller CSS Grid. |
| **LicenseException** | Kör utan en giltig licens i produktion. | Applicera din tillfälliga eller köpta licens innan rendering (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Vanliga frågor

**Q: Vad är Aspose.HTML för Java?**  
A: Aspose.HTML för Java är ett Java‑bibliotek som låter utvecklare manipulera och konvertera HTML‑dokument till olika format, såsom XPS, PDF och bilder.

**Q: Var kan jag ladda ner Aspose.HTML för Java?**  
A: Du kan ladda ner Aspose.HTML för Java‑biblioteket från [denna länk](https://releases.aspose.com/html/java/).

**Q: Finns det en gratis provversion av Aspose.HTML för Java?**  
A: Ja, du kan få en gratis provversion av Aspose.HTML för Java från [här](https://releases.aspose.com/).

**Q: Hur får jag en tillfällig licens för Aspose.HTML för Java?**  
A: För att få en tillfällig licens för Aspose.HTML för Java, besök [denna sida](https://purchase.aspose.com/temporary-license/).

**Q: Kan jag få support för Aspose.HTML för Java?**  
A: Ja, du kan söka hjälp och support från Aspose‑communityn på [Aspose Forum](https://forum.aspose.com/).

**Q: Kan jag konvertera HTML till XPS på en huvudlös server?**  
A: Absolut. Aspose.HTML fungerar i miljöer utan GUI; se bara till att Java‑runtime är korrekt konfigurerad.

**Q: Stöder biblioteket anpassade sidmarginaler?**  
A: Ja. Använd `PageSetup.setMarginTop()`, `setMarginBottom()` osv. innan du tilldelar `PageSetup` till renderingsalternativen.

## Slutsats

Vi har gått igenom hela processen för **konvertera HTML till XPS** och justera sidstorleken med Aspose.HTML för Java. Genom att följa dessa steg kan du skapa utskriftsklara XPS‑dokument som matchar dina exakta layoutkrav. Känn dig fri att experimentera med olika sidimensioner, stilar eller till och med lägga till sidhuvuden och sidfötter för att passa ditt projekts behov.

Om du har några frågor eller behöver ytterligare hjälp, utforska [Aspose.HTML för Java‑dokumentationen](https://reference.aspose.com/html/java/) eller gå med i samtalet på [Aspose Forum](https://forum.aspose.com/).

---

**Senast uppdaterad:** 2026-03-18  
**Testad med:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Författare:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
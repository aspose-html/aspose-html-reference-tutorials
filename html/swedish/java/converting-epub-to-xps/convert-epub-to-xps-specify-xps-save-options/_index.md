---
date: 2026-01-09
description: Lär dig hur du använder Aspose.HTML för Java för att ange XPS‑sparalternativ
  och konvertera EPUB till XPS effektivt.
linktitle: Specifying XPS Save Options for EPUB to XPS
second_title: Java HTML Processing with Aspose.HTML
title: Specificering av Aspose HTML‑sparalternativ för konvertering från EPUB till
  XPS
url: /sv/java/converting-epub-to-xps/convert-epub-to-xps-specify-xps-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Specificering av Aspose HTML Save Options för EPUB till XPS

Att konvertera ett EPUB-dokument till XPS kan vara en praktisk del av ett publiceringsarbetsflöde, och **Aspose HTML Save Options** ger dig finjusterad kontroll över resultatet. I den här handledningen går vi igenom de exakta stegen som behövs för att konfigurera dessa spara‑alternativ med Aspose.HTML för Java och producera en högkvalitativ XPS‑fil.

## Snabba svar
- **Vad gör Aspose HTML Save Options?** Det låter dig anpassa sidstorlek, bakgrundsfärg och andra renderingsinställningar när du sparar till format som XPS.  
- **Vilket bibliotek krävs?** Aspose.HTML för Java (senaste versionen).  
- **Behöver jag en licens?** En gratis provversion fungerar för utvärdering; en kommersiell licens krävs för produktion.  
- **Kan jag ändra sidans dimensioner?** Ja – du kan ange valfri bredd och höjd via `PageSetup`.  
- **Är konverteringen snabb?** För vanliga EPUB‑filer slutförs konverteringen på sekunder på en modern JVM.

## Vad är Aspose HTML Save Options?
Aspose HTML Save Options är en uppsättning egenskaper som styr hur HTML, EPUB eller andra webbaserade dokument renderas och sparas till ett målformat såsom XPS, PDF eller bildfiler. De låter dig definiera sidlayout, bakgrundsfärger, marginaler och mer, vilket säkerställer att den resulterande filen matchar dina designkrav.

## Varför använda Aspose.HTML för Java för att konvertera EPUB till XPS?
- **Hög noggrannhet** – bevarar komplexa layouter, typsnitt och vektorgrafik.  
- **Programmatisk kontroll** – automatisera batchkonverteringar i Java‑applikationer.  
- **Inga externa beroenden** – rent Java‑bibliotek, inga inhemska komponenter.  
- **Anpassningsbar output** – tack vare spara‑alternativen kan du skräddarsy XPS‑filen efter dina exakta behov.

## Förutsättningar

Innan vi dyker ner i koden, se till att du har följande:

1. **Java‑utvecklingsmiljö** – JDK 8 eller högre installerad.  
2. **Aspose.HTML för Java‑bibliotek** – ladda ner det från [download link](https://releases.aspose.com/html/java/).  
3. **EPUB‑fil** – den käll‑EPUB du vill konvertera.  

Att ha dessa redo gör att du kan följa stegen utan avbrott.

## Importera paket

Först importerar du de nödvändiga klasserna. Placera importerna högst upp i din Java‑källfil:

```java
import java.io.FileInputStream;
import com.aspose.html.saving.XpsSaveOptions;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.drawing.Page;
import com.aspose.html.drawing.Size;
import com.aspose.html.drawing.Length;
import com.aspose.html.drawing.Color;
import com.aspose.html.converters.Converter;
import com.aspose.html.system.io.resources.Resources;
```

Dessa importeringar ger dig åtkomst till konverteringsmotorn och de **Aspose HTML Save Options** som behövs för finjustering.

## Öppna EPUB‑filen

Nästa steg är att öppna den EPUB du vill konvertera. Hjälpverktyget `Resources.input` laddar en fil från demo‑resursmappen:

```java
try (FileInputStream fileInputStream = new FileInputStream(Resources.input("input.epub"))) {
    // Your code for the EPUB file handling goes here.
}
```

Att använda ett try‑with‑resources‑block säkerställer att strömmen stängs automatiskt.

## Skapa XPS‑spara‑alternativ (konfigurera sidstorlek och bakgrund)

Nu skapar vi en `XpsSaveOptions`‑instans och anpassar den. Det är här **spara‑alternativen** verkligen glänser:

```java
XpsSaveOptions options = new XpsSaveOptions();
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
anyPage.setSize(new Size(Length.fromPixels(3000), Length.fromPixels(1000)));
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

- **Sidstorlek** – satt till 3000 × 1000 pixlar i detta exempel; justera för att matcha ditt mål‑pappersformat.  
- **Bakgrundsfärg** – `AliceBlue` visar hur du ändrar canvas‑bakgrunden; du kan välja vilken `Color` som helst.

Dessa inställningar är en del av **Aspose HTML Save Options** som påverkar den slutliga XPS‑dokumentet.

## Konvertera EPUB till XPS

Slutligen anropar du konverteraren med strömmen, de konfigurerade alternativen och en utdataväg:

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.xps")
);
```

När denna rad körs läser Aspose.HTML EPUB‑filen, tillämpar sidinställningarna och bakgrundsfärgen du definierat, och skriver en fullt kompatibel XPS‑fil.

## Vanliga problem & tips

- **Felaktiga siddimensioner** – se till att dimensionerna uttrycks i pixlar (eller använd `Length.fromInches`).  
- **Saknade typsnitt** – bädda in nödvändiga typsnitt i EPUB‑filen eller installera dem på JVM‑värden för att undvika fallback.  
- **Stora filer** – för mycket stora EPUB‑filer, öka JVM‑heapen (`-Xmx`) för att förhindra `OutOfMemoryError`.  

## Slutsats

Genom att utnyttja **Aspose HTML Save Options** får du exakt kontroll över hur en EPUB renderas till XPS. Stegen ovan visar hur du ställer in sidstorlek, bakgrundsfärg och utför konverteringen med bara några rader Java‑kod. Integrera detta mönster i dina batch‑processpipelines för att automatisera publiceringsuppgifter effektivt.

## Vanliga frågor

**Q: Vad är Aspose.HTML för Java?**  
A: Det är ett Java‑bibliotek som gör det möjligt för utvecklare att skapa, redigera, rendera och konvertera HTML, EPUB och andra webbaserade dokument utan att behöva en webbläsare.

**Q: Kan jag använda detta i ett kommersiellt projekt?**  
A: Ja. För produktionsbruk behöver du en giltig licens. Du kan köpa en på [purchase page](https://purchase.aspose.com/buy).

**Q: Finns det en gratis provversion tillgänglig?**  
A: Absolut. Ladda ner en provversion från [here](https://releases.aspose.com/).

**Q: Var kan jag få support?**  
A: Community‑support och officiell hjälp finns via Aspose‑forumet på [https://forum.aspose.com/](https://forum.aspose.com/).

**Q: Vad är systemkraven?**  
A: Ett Java Development Kit (JDK) 8+ och ett operativsystem som stöds av Aspose‑runtime. Säkerställ att din miljö uppfyller de tidigare nämnda förutsättningarna.

---

**Senast uppdaterad:** 2026-01-09  
**Testat med:** Aspose.HTML for Java 24.12  
**Författare:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
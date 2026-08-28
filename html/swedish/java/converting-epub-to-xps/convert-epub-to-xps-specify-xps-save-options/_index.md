---
date: 2026-03-29
description: Lär dig hur du använder Aspose.HTML för Java för att ange XPS‑sparalternativ,
  konvertera EPUB till XPS och hantera licensiering.
linktitle: Specifying XPS Save Options for EPUB to XPS
second_title: Java HTML Processing with Aspose.HTML
title: Hur du använder Aspose HTML-sparalternativ för EPUB till XPS
url: /sv/java/converting-epub-to-xps/convert-epub-to-xps-specify-xps-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder Aspose HTML Save Options för EPUB till XPS

I den här guiden visar vi **how to use Aspose** HTML Save Options för att konvertera ett EPUB-dokument till XPS med full kontroll över sidstorlek, bakgrundsfärg och licensieringsaspekter. Oavsett om du bygger en batch‑processpipeline eller ett engångsverktyg för konvertering, hjälper dessa steg dig att snabbt få pålitliga resultat.

## Snabba svar
- **Vad gör Aspose HTML Save Options?** Det låter dig anpassa sidstorlek, bakgrundsfärg och andra renderingsinställningar när du sparar till format som XPS.  
- **Vilket bibliotek krävs?** Aspose.HTML for Java (senaste versionen).  
- **Behöver jag en licens?** En gratis provversion fungerar för utvärdering; en kommersiell licens krävs för produktion.  
- **Kan jag ändra siddimensioner?** Ja – du kan ange valfri bredd och höjd via `PageSetup`.  
- **Är konverteringen snabb?** För vanliga EPUB-filer slutförs konverteringen på några sekunder på en modern JVM.

## Vad betyder “how to use aspose” i detta sammanhang?
Frasen **how to use Aspose** avser de praktiska stegen för att utnyttja Aspose.HTML-biblioteket för att manipulera och konvertera webbaserade dokument. I den här handledningen fokuserar vi på **aspose html save options** som låter dig finjustera resultatet när du **convert EPUB to XPS**.

## Varför använda Aspose.HTML för Java för att konvertera EPUB till XPS?
- **High fidelity** – bevarar komplexa layouter, teckensnitt och vektorgrafik.  
- **Programmatic control** – automatisera batchkonverteringar i Java‑applikationer.  
- **No external dependencies** – rent Java‑bibliotek, inga inhemska komponenter.  
- **Customizable output** – tack vare save‑options kan du anpassa XPS efter dina exakta behov, såsom **specify page dimensions** eller ange en anpassad bakgrund.  

## Förutsättningar

Innan vi dyker ner i koden, se till att du har följande:

1. **Java Development Environment** – JDK 8 eller högre installerat.  
2. **Aspose.HTML for Java Library** – ladda ner den från [download link](https://releases.aspose.com/html/java/).  
3. **EPUB File** – käll‑EPUB‑filen du vill **convert EPUB to XPS**.  

Att ha dessa redo gör att du kan följa stegen utan avbrott.

## Importera paket

Först, importera de nödvändiga klasserna. Placera importerna högst upp i din Java‑källfil:

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

Nästa steg, öppna den EPUB du vill konvertera. Hjälpmetoden `Resources.input` laddar en fil från demo‑resursmappen:

```java
try (FileInputStream fileInputStream = new FileInputStream(Resources.input("input.epub"))) {
    // Your code for the EPUB file handling goes here.
}
```

Genom att använda ett try‑with‑resources‑block säkerställs att strömmen stängs automatiskt.

## Skapa XPS Save Options (konfigurera sidstorlek & bakgrund)

Nu skapar vi en `XpsSaveOptions`‑instans och anpassar den. Det är här **save options** verkligen kommer till sin rätt:

```java
XpsSaveOptions options = new XpsSaveOptions();
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
anyPage.setSize(new Size(Length.fromPixels(3000), Length.fromPixels(1000)));
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

- **Page size** – satt till 3000 × 1000 pixlar i detta exempel; justera för att matcha ditt målpapper eller använd `Length.fromInches` för att **specify page dimensions** i tum.  
- **Background color** – `AliceBlue` visar hur du ändrar canvas‑bakgrunden; du kan välja vilken `Color` som helst.  

Dessa inställningar är en del av **aspose html save options** som påverkar det slutliga XPS‑dokumentet.

## Konvertera EPUB till XPS

Till sist, anropa konverteraren med strömmen, de konfigurerade alternativen och en utskrivningssökväg:

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.xps")
);
```

När den här raden körs läser Aspose.HTML EPUB‑filen, tillämpar sidinställningarna och bakgrundsfärgen du definierat, och skriver en fullt kompatibel XPS‑fil.

## Vanliga problem & tips

- **Incorrect page dimensions** – se till att dimensionerna anges i pixlar (eller använd `Length.fromInches`).  
- **Missing fonts** – bädda in nödvändiga teckensnitt i EPUB‑filen eller installera dem på JVM‑värden för att undvika fallback.  
- **Large files** – för mycket stora EPUB‑filer, öka JVM‑heapen (`-Xmx`) för att förhindra `OutOfMemoryError`.  
- **Aspose HTML licensing** – se till att en giltig licens är laddad innan konvertering; annars visas provvattenstämpeln.

## Slutsats

Genom att utnyttja **Aspose HTML Save Options** får du exakt kontroll över hur ett EPUB renderas till XPS. Stegen ovan visar hur du **how to convert EPUB**, sätter **page dimensions**, ändrar bakgrunden och utför konverteringen med bara några rader Java‑kod. Integrera detta mönster i dina batch‑processpipelines för att automatiskt hantera publiceringsuppgifter effektivt.

## Vanliga frågor

**Q: What is Aspose.HTML for Java?**  
A: Det är ett Java‑bibliotek som gör det möjligt för utvecklare att skapa, redigera, rendera och konvertera HTML, EPUB och andra webbaserade dokument utan att behöva en webbläsare.

**Q: Can I use this in a commercial project?**  
A: Ja. För produktionsbruk behöver du en giltig licens. Du kan köpa en på [purchase page](https://purchase.aspose.com/buy).

**Q: Is there a free trial available?**  
A: Absolut. Ladda ner en provversion från [here](https://releases.aspose.com/).

**Q: Where can I get support?**  
A: Community‑support och officiell hjälp finns via Aspose‑forumet på [https://forum.aspose.com/](https://forum.aspose.com/).

**Q: What are the system requirements?**  
A: Ett Java Development Kit (JDK) 8+ och ett operativsystem som stöds av Aspose‑runtime. Se till att din miljö uppfyller de tidigare listade förutsättningarna.

---

**Senast uppdaterad:** 2026-03-29  
**Testat med:** Aspose.HTML for Java 24.12  
**Författare:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
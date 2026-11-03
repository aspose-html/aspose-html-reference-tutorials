---
category: general
date: 2026-03-18
description: Rychle vytvořte PDF z HTML v Javě. Naučte se, jak převést HTML na PDF,
  simulovat obrazovku iPhone a nastavit velikost obrazovky pro responzivní PDF.
draft: false
keywords:
- create pdf from html
- convert html to pdf
- simulate iphone screen
- how to set screen
- how to convert html
language: cs
og_description: Vytvořte PDF z HTML v Javě. Tento průvodce ukazuje, jak převést HTML
  na PDF, simulovat obrazovku iPhone a nastavit rozměry obrazovky pro dokonalé responzivní
  PDF.
og_title: Vytvořte PDF z HTML s mobilním viewportem – Java tutoriál
tags:
- Java
- Aspose.HTML
- PDF
- Responsive Design
- Mobile Viewport
title: Vytvořte PDF z HTML s mobilním viewportem – Kompletní Java průvodce
url: /cs/java/conversion-html-to-other-formats/create-pdf-from-html-with-mobile-viewport-complete-java-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření PDF z HTML s mobilním viewportem – Kompletní průvodce pro Java

Už jste někdy potřebovali **vytvořit PDF z HTML**, ale výstup vypadal jako desktopová stránka na malém telefonním displeji? Nejste v tom sami. Když převádíte responzivní webovou stránku do PDF, výchozí viewport často ignoruje mobilní breakpointy, což vám zanechá stísněný nepořádek.  

Dobrá zpráva? Můžete **převést HTML do PDF** při **simulaci iPhone obrazovky**, a to jen pomocí čistého Java kódu. V tomto tutoriálu projdeme každý krok – jak nastavit velikost obrazovky, jak upravit faktor měřítka zařízení a proč jsou tato nastavení důležitá pro pixel‑dokonalé PDF.

> **Tip:** Pokud jste již použili Aspose.HTML pro jednoduché konverze, zjistíte, že úpravy viewportu jsou jen o několik řádků dál.

---

## Co se naučíte

* Jak **vytvořit PDF z HTML** pomocí Aspose.HTML pro Java.  
* Přesný kód pro **simulaci iPhone obrazovky** s rozměry (375 × 667 px @ 2× hustota).  
* Kde umístit **jak nastavit obrazovku** možnosti v konverzním pipeline.  
* Běžné úskalí při konverzi responzivních stránek a jak se jim vyhnout.  
* Kompletní, připravený Java příklad, který můžete zkopírovat a vložit do svého IDE.

### Požadavky

* Java 17 nebo novější (kód se kompiluje i se staršími verzemi, ale 17 je doporučená).  
* Knihovna Aspose.HTML pro Java – můžete stáhnout nejnovější JAR z [Aspose webu](https://products.aspose.com/html/java).  
* Jednoduchý HTML soubor (`input.html`), který chcete převést na PDF.  
* Základní znalost Maven nebo Gradle (ukážeme Maven ukázku).

---

## Krok 1 – Přidejte Aspose.HTML do svého projektu

Nejprve potřebujete knihovnu ve své classpath. Pokud používáte Maven, vložte tuto závislost do svého `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- Use the latest version -->
</dependency>
```

> **Proč je to důležité:** Aspose.HTML provádí těžkou práci – parsování HTML, aplikaci CSS a rasterizaci rozvržení. Bez ní byste museli sami psát kompletní prohlížečový engine, což je *mnoho* práce.

Pokud dáváte přednost Gradle, ekvivalent je:

```groovy
implementation 'com.aspose:aspose-html:23.12'
```

---

## Krok 2 – Připravte Load Options a simulujte iPhone viewport

Nyní nakonfigurujeme parametry **jak nastavit obrazovku**. Třída `HtmlLoadOptions` vám umožní říci Aspose, jakou velikost a hustotu pixelů má prohlížeč předstírat.

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

### Proč tyto čísla?

* **375 × 667** odpovídá logickým CSS pixelovým rozměrům iPhone 6/7/8 v režimu na výšku.  
* **DeviceScaleFactor = 2.0** říká rendereru, že každý CSS pixel odpovídá dvěma fyzickým pixelům, čímž napodobuje Retina displej.  

Pokud potřebujete jiné zařízení – například iPhone 12 Pro Max – změníte velikost na `428 × 926` a zachováte faktor měřítka na `3.0`.

---

## Krok 3 – Spusťte konverzi a ověřte výstup

Zkompilujte a spusťte třídu:

```bash
mvn compile exec:java -Dexec.mainClass=ViewportDemo
```

Po dokončení programu otevřete `output.pdf`. Měli byste vidět:

* Všechny media queries cílené na `max-width: 375px` jsou aplikovány správně.  
* Obrázky jsou vykresleny ostře díky 2× faktoru měřítka.  
* Text, který respektuje hierarchii mobilních velikostí fontů definovanou v CSS.

Pokud PDF stále vypadá jako desktopová stránka, dvojitě zkontrolujte, že vaše HTML používá responzivní meta tagy:

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

Bez tohoto tagu ani dokonalé nastavení viewportu nespustí mobilní stylesheet.

---

## Krok 4 – Zpracování externích zdrojů (Obrázky, Fonty, CSS)

Když **převádíte HTML do PDF**, Aspose.HTML se snaží načíst každý propojený zdroj. Pokud převádíte stránku, která žije v lokálním souborovém systému, absolutní URL (`file:///…`) fungují dobře. U vzdálených zdrojů můžete narazit na:

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **404 chyby u obrázků** | HTML odkazuje na URL, která vyžaduje autentizaci. | Použijte `HtmlLoadOptions.setBaseUrl("file:///C:/myproject/")` k vyřešení relativních cest, nebo vložte obrázky jako Base64. |
| **Chybějící webové fonty** | PDF engine nemůže stáhnout soubor fontu. | Stáhněte soubory `.woff`/`.ttf` lokálně a odkažte na ně relativní cestou. |
| **CSS není aplikováno** | Soubor CSS je blokován CORS. | Umístěte CSS na server, který povoluje cross‑origin požadavky, nebo vložte CSS přímo do HTML. |

Rychlý způsob, jak otestovat načítání zdrojů, je zabalit volání konverze do try‑catch bloku a vytisknout zprávu `Exception`. Aspose.HTML poskytuje podrobné logy, které ukazují přesnou URL, která selhala.

```java
try {
    Converter.convertDocument(...);
} catch (Exception ex) {
    System.err.println("Conversion failed: " + ex.getMessage());
}
```

---

## Krok 5 – Pokročilé úpravy (Volitelné)

### a) Změna velikosti PDF stránky

Ve výchozím nastavení Aspose.HTML vytváří PDF stránku, která odpovídá velikosti viewportu. Pokud dáváte přednost A4 nebo Letter, přidejte konfiguraci `PdfSaveOptions`:

```java
PdfSaveOptions pdfOptions = new PdfSaveOptions();
pdfOptions.setPageSize(PageSize.A4);
Converter.convertDocument("input.html", "output.pdf", pdfOptions, loadOptions);
```

### b) Přidání záhlaví/pati programově

Po konverzi můžete pomocí Aspose.PDF (samostatná knihovna) vložit jednoduché záhlaví/pati. Pracovní postup je:

1. Převést HTML → PDF (jak je ukázáno).  
2. Otevřít vzniklé PDF pomocí Aspose.PDF.  
3. Přidat objekty `HeaderFooter` na každou stránku.

```java
import com.aspose.pdf.*;

Document pdfDoc = new Document("output.pdf");
for (Page page : pdfDoc.getPages()) {
    page.addHeaderFooter(new HeaderFooter("Generated on " + LocalDate.now()));
}
pdfDoc.save("output-with-header.pdf");
```

### c) Hromadná konverze

Pokud máte složku s HTML soubory, projděte je v cyklu:

```java
Files.list(Paths.get("html_folder"))
     .filter(p -> p.toString().endsWith(".html"))
     .forEach(p -> {
         String pdfPath = p.toString().replace(".html", ".pdf");
         Converter.convertDocument(p.toString(), pdfPath, new PdfSaveOptions(), loadOptions);
     });
```

---

## Často kladené otázky (FAQ)

**Q: Funguje to s JavaScript‑těžkými stránkami?**  
A: Aspose.HTML podporuje podmnožinu JavaScriptu. Jednoduché manipulace s DOM a změny CSS obvykle fungují, ale složité frameworky (React, Angular) mohou vyžadovat předem vygenerovaný statický HTML snapshot.

**Q: Co když potřebuji převést stránku, která používá pravidla `@media print`?**  
A: Knihovna automaticky respektuje `@media print`. Nicméně, pokud také nastavíte mobilní viewport, stylesheet pro `print` může přepsat některé mobilní styly. Otestujte oba scénáře.

**Q: Můžu nastavit vlastní DPI pro PDF?**  
A: Ano. Použijte `PdfSaveOptions.setDpi(300)` před konverzí. Vyšší DPI vede k větším souborům, ale ostřejším obrázkům.

---

## Očekávaný výsledek – screenshot

Níže je ilustrace finální PDF stránky (simulovaný mobilní viewport).  
![Screenshot of PDF generated by create pdf from html demo showing iPhone‑sized layout]  

*Alt text obrázku obsahuje hlavní klíčové slovo pro SEO.*

---

## Závěr

Nyní máte solidní workflow **create pdf from html**, který respektuje mobilní breakpointy, simuluje iPhone obrazovku a dává vám plnou kontrolu nad rozměry stránky. Úpravou `HtmlLoadOptions` můžete odpovědět na otázku “**how to set screen**” pro jakékoli zařízení a pomocí `Converter.convertDocument` jste zvládli **how to convert html** v Javě.

Jste připraveni na další výzvu? Zkuste kombinovat tento přístup s Aspose.PDF pro přidání vodoznaků, sloučení více PDF nebo ochranu dokumentu heslem. A nezapomeňte experimentovat s dalšími zařízeními – stačí změnit hodnoty `Size` a `DeviceScaleFactor`, aby odpovídaly požadované hustotě pixelů.

Šťastné kódování a ať vaše PDF vždy vypadají stejně ostrě na papíře jako na telefonním displeji! 

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
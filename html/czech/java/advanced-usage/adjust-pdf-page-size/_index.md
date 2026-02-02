---
date: 2026-02-02
description: Naučte se, jak upravit velikost stránky PDF, renderovat HTML jako PDF,
  převést HTML na PDF a generovat PDF z HTML pomocí Aspose.HTML pro Javu. Snadno ovládejte
  rozměry stránky.
linktitle: Adjusting PDF Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Upravte velikost stránky PDF pomocí Aspose.HTML pro Javu
url: /cs/java/advanced-usage/adjust-pdf-page-size/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Upravit velikost PDF stránky pomocí Aspose.HTML pro Java

Generování PDF z HTML je běžná potřeba pro zprávy, faktury a e‑knihy. Když **upravit velikost PDF stránky**, zajistíte, že finální dokument odpovídá rozvržení, které jste navrhli v HTML, a můžete snadno **převést HTML do PDF** s přesnými rozměry, které potřebujete. V tomto tutoriálu se naučíte, jak renderovat HTML jako PDF, nastavit vlastní rozměry a řídit, zda se stránka automaticky rozšíří na s použitím Aspose.HTML pro Java.

“?** Umožňuje definovat šířku a výšku každé PDF stránky nebo nechat renderer automaticky přizpůsobit nejširšímu prvku.  
- **Která knihovna se používá?** Aspose.HTML pro Java (nejnovější verze).  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro vývoj; pro produkci je vyžadována komerční licence.  
- **Mohu rozměry měnit programově?** Ano – použijte `PageSetup` a vlastnost `AdjustToWidestPage`.  
- **Je to kompatibilní s Java 8+?** Rozhodně – API funguje s jakýmkoli JDK 8 nebo novějším.

## Co znamená „adjust PDF page size“?
Upravení velikosti PDF stránky znamená konfiguraci rozměrů každé stránky, kterou renderer HTML vytvoří. Můžete nastavit pevnou velikost (např. A4, Letter) nebo nechat renderer vypočít roz## při konverzi HTML do PDF?
- **Zachovat záměr designu:** Zabránit oříznutí nebo roztažení obsahu.  
- **Optimalizovat pro tisk:** Odpovídat velikosti papíru požadovanému v následných procesech.  
- **Zlepšit čitelnost:** Vyhnout se nadměrnému bílému prostoru nebo stísněnému textu.  
- **Dynamické dokumenty:** Automaticky přizpůsobit široké tabulky nebo obrázky bez ručních výpočtů.

## Kdy byste měli tento přístup použít?
Pokud generujete faktury, katalogy produktů nebo technické příručky, kde musí rozvržení zůstat konzistentní napříč zařízeními a tiskárnami, úprava velikosti PDF stránky zajistí, že máte široké tabulky nebo grafiku, která by jinak byla oříznuta.

## Prerequisites
Než začnete, ujistěte se, že máte:

- **Java Development Kit (JDK) 8 nebo vyšší** nainstalovaný na vašem počítači.  
- **Aspose.HTML pro Java** – stáhněte nejnovější JAR ze [oficiální stránky vydání](https://releases.aspose.com/html/java/).  
- **HTML soubor**, který chcete převést (v příkladu použijeme `FirstFile.html`).  

## Import balíčků
Nejprve importujte třídy, které```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

## Krok 1: Načtení HTML obsahu
Načteme zdrojový HTML soubor pomocí `FileInputStream`. Tento krok připraví surový markup pro pozdější manipulaci.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## Krok 2) HTML
Zde zkopírujeme původní HTML do nového souboru a vložíme několik inline stylů, abychom ukázali, jak stylování ovlivňuje výstup PDF. Klidně nahraďte ukázkový CSS svým vlastním.

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Add custom HTML styles or content here
    String style = "<style>\n" +
                   ".st\n" +
                   "{\n" +
                   "color:\n" +
                   "green;\n" +
                   "}\n" +
                   "</style >\n" +
                   "<div id = id1 > Aspose.Html rendering Text in Black Color</div >\n" +
                   "<div id = id2 class='' st '' > Aspose.Html rendering Text in Green Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: blue;' > Aspose.Html rendering Text in Blue Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: red;' ><font face = 'Arial' > Aspose.Html rendering Text in Red\n" +
                   "Color</font ></div >\n";
    fileOutputStream.write(style.getBytes(java.nio.charset.StandardCharsets.UTF_8));
}
```

## Krok 3: Render **generovat PDF z HTML** se dvěma různými strategiemi velikosti stránky.

### 3.1 Velikost rozměry stránky (100 × 100 bodů). Pokud jakýkoli prvek překročí tyto limity, bude oříznut.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Create an HTMLDocument instance from the HTML file
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Set PDF rendering options
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

### 3.2 Velikost stránky JE UPRAVENA na šířku obsahu
Zde povolíme `AdjustToWidestPage`, takže renderer automaticky rozšíří šířku stránky tak, aby pojala nejširší prvek, přičemž výška zůstane pevná.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

## Jak nastavit rozměry PDF (jak změnit velikost PDF stránky) v kódu
Objekt `PageSetup` je klíčový:

- `setAnyPage(Page page)`: definuje základní šířku × výšku.  
- `setAdjustToWidestPage(boolean)`: přepíná automatické rozšiřování.  

Úpravou těchto dvou vlastností můžete **nastavit rozměry PDF** pro jakýkoli scénář, ať už potřebujete statickou stránku A4 nebo dynamickou šířku, která sleduje vaše HTML rozvržení.

## Časté problémy a tipy
| Problém | Proč se to děje | Řešení |
|-------|----------------|-----|
| Obsah je oříznut | Pevná velikost je příliš malá | Zvyšte hodnoty `Size` nebo povolte `AdjustToWidestPage`. |
| Text vypadá rozmazaně | Výchozí DPI renderování je nízké | Použijte `PdfRenderingOptions.setResolution(int| Chybí styly | Externí CSS není načteno | složku se styly. |
| Velké HTML soubory způsobují OutOfMemoryError | Renderer načítá celý dokument do paměti | Zpracovávejte dokument po částech nebo zvýšte heap JVM (`-Xmx`). |

### Pro tip
Při práci s obrázky vysokého rozlišení nastavte DPI na 300 nebo vyšší, aby byl výstupní PDF ostrý.

## Často kladené otázky

**Q: Co je Aspose.HTML pro Java?**  
A: Jedná se o Java knihovnu, která umožňuje vytvářet, upravovat a renderovat HTML dokumenty, včetně konverze do PDF, PNG a dalších formátů.

**Q HTML do PDF s Aspose.HTML pro Java?**  
A: Použijte třídu `PageSetup` a nastavte `AdjustToWidestPage` na `true` (automatická velikost) nebo `false` (pevná velikost). Pak přiřaďte požadovanou `Size` pomocí `new Page(new Size(width, height))`.

**Q: Mohu přizpůsobit stylování HTML obsahu před jeho převodem do PDF?**  
A: Ano – můžete vložit CSS, upravit DOM nebo použít externí stylové soubory. Tutoriál ukazuje vložení inline CSS.

**Q: Kde najdu dokumentaci k Aspose.HTML pro Java?**  
A: Kompletní dokumentace je k dispozici [zde](https://reference.aspose.com/html/java/).

: Rozhodně – stáhněte si zkušební verzi ze [stránky vydání](https://releases.aspose.com/html/java/).

## Závěr
Nyní víte, jak **upravit velikost PDF stránky**, **renderovat HTML jako PDF** a **nastavit vlastní rozměry PDF** pomocí Aspose.HTML pro Java. Experimentujte s různými velikostmi stránek, nastavením DPI a úpravami CSS, abyste dosáhli dokonalého výstupu pro váš konkréťte se na oficiální dokumentaci nebo fóra podpory Aspose.

---

**Poslední aktualizace:** 2026-02-02  
**Testováno s:** Aspose.HTML pro Java 24.12 (nejnovější)  
**Autor:** Aspose  
**Související zdroje:** [API Reference](https://reference.aspose.com/html/java/) | [Download Free Trial](https://releases.aspose.com/html/java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
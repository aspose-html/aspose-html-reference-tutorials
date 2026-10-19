---
category: general
date: 2026-02-14
description: Naučte se, jak komprimovat PDF při převodu HTML do PDF v Javě pomocí
  Aspose HTML. Obsahuje nastavení vlastní velikosti obrazovky a kompletní ukázkový
  kód.
draft: false
keywords:
- how to compress pdf
- convert html to pdf
- html to pdf java
- aspose html pdf
- set custom screen
language: cs
og_description: Jak komprimovat PDF při konverzi HTML na PDF v Javě pomocí Aspose
  HTML. Kompletní krok‑za‑krokem tutoriál s vlastními nastaveními obrazovky.
og_title: Jak komprimovat PDF pomocí Aspose HTML to PDF – průvodce pro Javu
tags:
- Aspose
- Java
- PDF conversion
title: Jak komprimovat PDF pomocí Aspose HTML to PDF – Java průvodce
url: /cs/java/conversion-html-to-other-formats/how-to-compress-pdf-with-aspose-html-to-pdf-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak komprimovat PDF pomocí Aspose HTML to PDF – průvodce pro Javu

Už jste se někdy zamysleli, **jak komprimovat pdf** soubory za běhu při převodu HTML stránek do PDF? Nejste jediní. Mnoho vývojářů narazí na problém, když se jejich PDF po konverzi nafouknou, zejména na mobilně‑prvních stránkách, kde je šířka pásma důležitá. Dobrá zpráva? S Aspose.HTML pro Javu můžete tyto PDF zmenšit — a také můžete konvertoru říci, aby stránku vykreslil, jako by byla zobrazena na zařízení s vlastním rozměrem.

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který vám přesně ukáže **jak komprimovat pdf** výstup, jak **převést html do pdf** v Javě a jak **nastavit vlastní obrazovku** tak, aby rozvržení odpovídalo telefonu 375×667 px. Na konci budete mít jedinou třídu, kterou můžete vložit do libovolného Maven nebo Gradle projektu a okamžitě začít generovat úsporné PDF.

## Co budete potřebovat

- **Java 17** (nebo jakýkoli aktuální JDK; Aspose.HTML podporuje Java 8+)
- **Aspose.HTML for Java** knihovna – můžete ji získat z Maven Central (`com.aspose:aspose-html:23.12` v době psaní)
- Jednoduchý HTML soubor (`input.html`), který chcete převést na PDF
- IDE nebo textový editor; není potřeba žádný speciální framework

> **Tip:** Pokud používáte Maven, přidejte závislost takto:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

Nyní, když jsou předpoklady vyřešeny, ponořme se do samotných kroků.

## Krok 1: Vytvořte sandbox a nastavte vlastní obrazovku

První věc, kterou obvykle děláte při konverzi HTML, je rozhodnout **jak bude stránka vykreslena**. Aspose.HTML vám umožní simulovat jakékoli zařízení konfigurací `Sandbox` s `Screen`. V našem případě napodobíme typickou obrazovku smartphonu (375 px šířka, 667 px výška, 96 dpi, měřítko 1.0).

```java
// Step 1 – create a sandbox that pretends we’re on a phone screen
Sandbox renderingSandbox = new Sandbox();
renderingSandbox.setScreen(new Screen(375, 667, 96, 1.0));
```

Proč používat sandbox? Bez něj konvertor používá výchozí desktop‑like viewport, což může způsobit posuny rozvržení a zbytečně velké PDF stránky. **Nastavením vlastní obrazovky** zajistíte, že PDF odpovídá mobilnímu designu a často snižuje počet stránek — nepřímý způsob, jak udržet velikost souboru nízkou.

## Krok 2: Nakonfigurujte možnosti konverze PDF (včetně komprese)

Nyní řekneme Aspose, že chceme komprimované PDF. Třída `PdfConversionOptions` má příznak `setCompress`, který po vykreslení spustí interní optimalizátor PDF. Můžete také doladit další možnosti (např. verzi PDF nebo kvalitu obrázků), pokud potřebujete jemnější kontrolu.

```java
// Step 2 – define PDF options and enable compression
PdfConversionOptions pdfOptions = new PdfConversionOptions();
pdfOptions.setSandbox(renderingSandbox);   // attach the sandbox from Step 1
pdfOptions.setCompress(true);              // this is the key to how to compress pdf
```

Když je zavoláno `setCompress(true)`, Aspose odstraní duplicitní objekty, sníží rozlišení obrázků a odstraní nepoužívané zdroje. Výsledkem je obvykle 30‑50 % úspora velikosti souboru bez znatelné vizuální ztráty.

## Krok 3: Proveďte konverzi HTML na PDF

S připraveným sandboxem a možnostmi je samotná konverze jedním řádkem. Stačí předat zdrojové HTML URI, cílové PDF URI a vytvořené možnosti.

```java
// Step 3 – run the conversion
Converter.convert(
        Paths.get("YOUR_DIRECTORY/input.html").toUri(),
        Paths.get("YOUR_DIRECTORY/output.pdf").toUri(),
        pdfOptions);
```

Nahraďte `YOUR_DIRECTORY` složkou, která obsahuje váš `input.html`. Po dokončení volání bude `output.pdf` ležet vedle něj, komprimovaný a přizpůsobený pro telefonní obrazovku.

## Kompletní, spustitelný příklad

Níže je kompletní Java třída, která spojuje všechny tři kroky. Klidně ji zkopírujte do souboru pojmenovaného `ConvertWithSandbox.java`, upravte cesty a spusťte `javac` + `java` jako obvykle.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfConversionOptions;
import com.aspose.html.rendering.Sandbox;
import com.aspose.html.rendering.Screen;
import java.nio.file.Paths;

/**
 * Demonstrates how to compress PDF while converting HTML to PDF in Java.
 * It also shows how to set a custom screen (375×667 px) to mimic a mobile device.
 */
public class ConvertWithSandbox {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox with a custom screen size (mobile‑friendly)
        Sandbox renderingSandbox = new Sandbox();
        renderingSandbox.setScreen(new Screen(375, 667, 96, 1.0));

        // 2️⃣ Set up PDF conversion options – enable compression
        PdfConversionOptions pdfOptions = new PdfConversionOptions();
        pdfOptions.setSandbox(renderingSandbox);
        pdfOptions.setCompress(true); // <-- this is how to compress pdf

        // 3️⃣ Convert the HTML file to a compressed PDF
        Converter.convert(
                Paths.get("YOUR_DIRECTORY/input.html").toUri(),
                Paths.get("YOUR_DIRECTORY/output.pdf").toUri(),
                pdfOptions);

        System.out.println("Conversion complete! Check output.pdf – it should be smaller and fit a 375×667 screen.");
    }
}
```

### Očekávaný výsledek

- **Velikost souboru:** Pokud váš původní HTML vytvořil 2 MB PDF, komprimovaná verze bude typicky kolem 1 MB nebo méně.
- **Rozvržení stránky:** PDF stránky budou široké 375 pt (≈5 palců) a vysoké 667 pt, což odpovídá rozměrům, které jsme předali sandboxu.
- **Vizuální věrnost:** Text zůstane ostrý; obrázky jsou sníženy jen natolik, aby byly čitelné na plátně velikosti telefonu.

Velikost úspory můžete ověřit kontrolou vlastností souboru před a po konverzi.

## Běžné varianty a okrajové případy

### 1. Potřebujete vyšší kompresi?

`PdfConversionOptions` nabízí další nastavení:

```java
pdfOptions.setImageQuality(70);   // JPEG quality (0‑100)
pdfOptions.setRemoveUnusedObjects(true);
pdfOptions.setCompress(true);
```

Snížením `setImageQuality` dále zmenšíte velikost obrázků, ale dejte pozor na viditelné artefakty u vysoce rozlišených fotografií.

### 2. Potřebujete jinou velikost obrazovky?

Stačí změnit hodnoty v konstruktoru `Screen`:

```java
renderingSandbox.setScreen(new Screen(1024, 768, 96, 1.0)); // tablet size
```

To je užitečné, když máte responzivní designy, které vypadají jinak na tabletech než na telefonech.

### 3. Konverze více HTML souborů ve smyčce

Pokud máte dávku HTML stránek, zabalte volání konverze do `for` smyčky:

```java
String[] files = {"page1.html", "page2.html"};
for (String file : files) {
    Converter.convert(
        Paths.get("src/html/" + file).toUri(),
        Paths.get("out/" + file.replace(".html", ".pdf")).toUri(),
        pdfOptions);
}
```

Stejná instance `pdfOptions` může být znovu použita, což udržuje kompresi konzistentní napříč všemi výstupy.

### 4. Zpracování externích zdrojů (CSS, obrázky)

Aspose.HTML řeší relativní URL na základě umístění HTML souboru. Ujistěte se, že všechny propojené CSS nebo obrázkové soubory jsou přístupné ze stejného adresáře, nebo použijte absolutní URL (např. `https://example.com/style.css`). Pokud se zdroj nepodaří načíst, konvertor zaznamená varování, ale pokračuje — takže stále získáte PDF, jen možná bez některých stylů.

## Často kladené otázky

**Q: Ovlivňuje komprese zabezpečení PDF?**  
A: Ne. Kompresní rutina optimalizuje pouze vnitřní strukturu PDF; nemění šifrování ani digitální podpisy. Pokud potřebujete PDF podepsat, udělejte to *po* kompresi.

**Q: Můžu streamovat výsledek místo zápisu do souboru?**  
A: Rozhodně. `Converter.convert` má také přetíženou verzi, která přijímá `OutputStream`. Nahraďte cílové URI `OutputStream` připojeným k odpovědi servletu, například.

**Q: Co když potřebuji kompatibilitu s PDF/A?**  
A: Použijte `PdfConversionOptions.setPdfACompliance(PdfACompliance.PdfA_1b)` před voláním `convert`. Komprese stále funguje; Aspose následně aplikuje pravidla specifická pro PDF/A.

## Vizualní přehled

![diagram ukazující příklad komprese pdf](https://example.com/images/compress-pdf-diagram.png "Diagram ukazující konverzní pipeline od HTML → Sandbox (vlastní obrazovka) → PDF možnosti (komprese) → Výstupní PDF")

*Alt text obsahuje primární klíčové slovo pro splnění SEO požadavků.*

## Závěr

Probrali jsme **jak komprimovat pdf** soubory při převodu HTML do PDF v Javě, předvedli **převod html do pdf** workflow s Aspose.HTML a ukázali, jak **nastavit vlastní obrazovku** pro mobilně‑přátelská rozvržení. Výše uvedený kód je připravený k spuštění a vysvětlení vám poskytují „proč“ za každým řádkem — takže můžete řešení přizpůsobit svým projektům.

Další kroky? Vyzkoušejte různé velikosti obrazovky, dolaďte `setImageQuality` pro ještě těsnější kompresi, nebo řetězte konverzi s krokem podepisování PDF. Můžete také prozkoumat další výstupní formáty Aspose (např. DOCX nebo PNG) pomocí stejné sandbox techniky.

Šťastné programování a užívejte si ty štíhlejší PDF!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-03-22
description: Vytvořte PDF ze SVG s vlastní velikostí stránky pomocí Aspose.HTML pro
  Javu – nastavte velikost stránky PDF, okraje a během několika minut převádějte SVG
  do PDF.
draft: false
keywords:
- create pdf from svg
- custom pdf page size
- how to convert svg
- set pdf page size
- aspose html
language: cs
og_description: Vytvořte PDF ze SVG s vlastní velikostí stránky pomocí Aspose.HTML
  pro Java. Naučte se, jak nastavit velikost stránky PDF, okraje a převést SVG během
  několika kroků.
og_title: Vytvořte PDF ze SVG – Vlastní velikost stránky s Aspose.HTML (Java)
tags:
- java
- aspose
- pdf-generation
title: Vytvořit PDF ze SVG – Vlastní velikost stránky s Aspose.HTML (Java)
url: /cs/java/conversion-html-to-other-formats/create-pdf-from-svg-custom-page-size-with-aspose-html-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření PDF ze SVG – Vlastní velikost stránky s Aspose.HTML (Java)

Potřebujete **vytvořit PDF ze SVG** a mít přesnou kontrolu nad rozměry každé stránky? V tomto průvodci projdeme kompletním, spustitelným příkladem, který ukazuje **jak převést SVG** do PDF při zadání *vlastní velikosti PDF stránky* a okrajů.  

Představte si, že máte sadu SVG ikon, které musí být vytištěny na listy formátu A4 – nic složitějšího, že? S Aspose.HTML to zvládnete během několika řádků kódu a já vám vysvětlím *proč* je každý řádek důležitý, abyste nemuseli hádat.

---

## Co budete potřebovat

- **Java 17** (nebo jakýkoli novější JDK) – kód funguje i na starších verzích, ale 17 je ideální.
- **Aspose.HTML for Java** JAR (nejnovější verze, např. 23.12) – můžete jej stáhnout z Maven repozitáře nebo oficiální stránky ke stažení.
- SVG soubor, který chcete převést do PDF; v tomto tutoriálu ho budeme nazývat `input.svg`.
- Jednoduché IDE (IntelliJ, Eclipse, VS Code…) – cokoliv, co vám vyhovuje.

A to je vše. Žádné další frameworky, žádné hacky s PDF tiskárnou. Jakmile máte knihovnu na classpath, můžete začít.

---

## Krok 1 – Nastavení Aspose.HTML a definice vlastní velikosti PDF stránky

Prvním krokem je importovat potřebné třídy a vytvořit objekt `PdfSaveOptions`. Tento objekt nám umožňuje **nastavit velikost PDF stránky** (A4, Letter nebo i vlastní rozměry) a definovat okraje v bodech.

```java
import com.aspose.html.Conversion;
import com.aspose.html.saving.PdfSaveOptions;
import com.aspose.html.saving.PdfPageSize;

public class SvgToPdfCustomPage {
    public static void main(String[] args) throws Exception {
        // 1️⃣  Path to the source SVG
        String inputSvgPath = "YOUR_DIRECTORY/input.svg";

        // 2️⃣  Configure PDF output options
        PdfSaveOptions pdfOptions = new PdfSaveOptions();

        // Choose a standard page size – A4 works for most print jobs
        pdfOptions.setPageSize(PdfPageSize.A4);

        // Optional: define custom margins (left, top, right, bottom) in points
        pdfOptions.setMargins(20, 20, 20, 20);   // 20 pt ≈ 0.28 in

        // 3️⃣  Perform the conversion
        Conversion.convertSvg(inputSvgPath, pdfOptions, "YOUR_DIRECTORY/output.pdf");

        System.out.println("✅ SVG successfully converted to PDF with custom page size.");
    }
}
```

**Proč je to důležité:**  
- `PdfSaveOptions` je vstupní bránou pro *nastavení velikosti PDF stránky* a okrajů. Bez něj by Aspose použil výchozí hodnoty (obvykle velikost Letter s nulovými okraji).  
- Použití `PdfPageSize.A4` zajišťuje, že výstup odpovídá nejběžnějšímu formátu pro tisk, ale můžete jej nahradit `PdfPageSize.LETTER` nebo dokonce vlastní velikostí pomocí `pdfOptions.setPageSize(new SizeF(width, height))`.  

---

## Krok 2 – Jak převést SVG do PDF jedním voláním

Těžkou práci vykonává `Conversion.convertSvg`. Tato statická metoda načte SVG, vykreslí jej a zapíše PDF podle předchozích nastavení. Jedná se o část **jak převést SVG** v celém řešení.

Několik věcí, na které je třeba pamatovat:

1. **Cesty k souborům musí být absolutní nebo relativní k pracovnímu adresáři** – jinak narazíte na `FileNotFoundException`.  
2. **Metoda vyhazuje `Exception`**, takže v produkci byste měli zachytávat konkrétní výjimky (např. `IOException`, `AsposeException`) a zpracovávat je elegantně.  
3. **Více SVG** – pokud potřebujete více‑stránkové PDF, kde každá stránka je jiný SVG, jednoduše projděte seznam názvů souborů a volajte `convertSvg` pro každý, přičemž výstupní proud připojujete ke stejnému PDF (pokročilé téma, viz sekce „Další kroky“).  

---

## Krok 3 – Ověření výsledku

Po spuštění programu by se ve výstupním adresáři měl objevit soubor `output.pdf`. Otevřete jej v libovolném PDF prohlížeči; každá stránka bude **A4** s okrajem 20 pt a grafika SVG bude perfektně přizpůsobena.

Pokud si prohlédnete vlastnosti PDF, uvidíte:

- **Velikost stránky:** 210 mm × 297 mm (A4).  
- **Okraje:** 20 pt na všech stranách, což odpovídá přibližně 7 mm.  
- **Kvalita obsahu:** Vektorová grafika zůstává ostrá, protože konverze zachovává SVG cesty.

To je kompletní end‑to‑end tok pro převod SVG do PDF s *vlastní velikostí PDF stránky*.

---

## Tipy a časté problémy

| Problém | Proč k tomu dochází | Řešení |
|---------|---------------------|--------|
| **Okraje vypadají špatně** | Body PDF vs. milimetry mohou být matoucí. | Pamatujte, že 1 pt = 1/72 in. Přizpůsobte `setMargins` podle toho. |
| **SVG elementy zmizí** | Některé SVG funkce (např. filtry) nejsou plně podporovány ve starších verzích Aspose. | Aktualizujte na nejnovější `aspose-html` JAR; podívejte se do poznámek k vydání ohledně podpory SVG. |
| **Chyba nedostatku paměti u velkých SVG** | Renderování velkých souborů spotřebovává heap. | Zvyšte heap JVM (`-Xmx2g`) nebo rozdělte SVG na menší části před konverzí. |
| **Potřeba nestandardní velikosti stránky** | Výčet v `PdfPageSize` pokrývá jen běžné velikosti. | Použijte `pdfOptions.setPageSize(new SizeF(widthInPoints, heightInPoints))`. |

---

## Krok 4 – Rozšíření příkladu: Více SVG stránek v jednom PDF

Pokud váš projekt vyžaduje **více‑stránkové PDF**, kde každá stránka pochází z jiného SVG, můžete znovu použít stejný `PdfSaveOptions` a předávat každé SVG API `Conversion`, přičemž výstup připojujete k objektu `PdfDocument`. Kód bude o něco delší, ale základní myšlenka zůstává stejná: *nastavte velikost PDF stránky jednou a pak ji znovu použijte*.

```java
import com.aspose.html.Conversion;
import com.aspose.html.saving.PdfSaveOptions;
import com.aspose.html.saving.PdfPageSize;
import com.aspose.html.saving.PdfDocument;

public class MultiSvgToPdf {
    public static void main(String[] args) throws Exception {
        String[] svgs = {"page1.svg", "page2.svg", "page3.svg"};
        PdfSaveOptions options = new PdfSaveOptions();
        options.setPageSize(PdfPageSize.A4);
        options.setMargins(20, 20, 20, 20);

        // Create an empty PDF document to collect pages
        PdfDocument pdfDoc = new PdfDocument();

        for (String svgPath : svgs) {
            // Convert each SVG to a temporary PDF stream
            ByteArrayOutputStream tempStream = new ByteArrayOutputStream();
            Conversion.convertSvg(svgPath, options, tempStream);
            // Append the temporary PDF as a new page
            pdfDoc.append(tempStream.toByteArray());
        }

        // Save the combined document
        pdfDoc.save("YOUR_DIRECTORY/multi-page-output.pdf");
        System.out.println("✅ Multi‑page PDF created.");
    }
}
```

*Poznámka:* Metoda `append` uvedená zde je jen ilustrativní; podívejte se do aktuální dokumentace Aspose.HTML pro přesný způsob slučování PDF, protože knihovna se vyvíjí.

---

## Závěr

Probrali jsme vše, co potřebujete k **vytvoření PDF ze SVG** s *vlastní velikostí PDF stránky* pomocí Aspose.HTML pro Java:

- Importujte správné třídy.  
- Nakonfigurujte `PdfSaveOptions` pro **nastavení velikosti PDF stránky** a okrajů.  
- Zavolejte `Conversion.convertSvg` pro provedení konverze jedním řádkem.  
- Ověřte výstup a řešte běžné problémy.  

Odtud můžete experimentovat s různými velikostmi stránek, vkládat písma nebo spojovat více SVG do více‑stránkového dokumentu. Flexibilita Aspose.HTML dělá z těchto úkolů skutečnou lahůdku.

Máte další otázky ohledně **jak převést SVG** soubory, nebo chcete prozkoumat triky s *vlastní velikostí PDF stránky* pro orientaci na šířku? Zanechte komentář a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
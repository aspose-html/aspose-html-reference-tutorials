---
date: 2026-01-09
description: Naučte se, jak používat Aspose.HTML pro Javu k specifikaci možností uložení
  XPS a efektivně převádět EPUB na XPS.
linktitle: Specifying XPS Save Options for EPUB to XPS
second_title: Java HTML Processing with Aspose.HTML
title: Specifikace možností uložení Aspose HTML pro konverzi EPUB na XPS
url: /cs/java/converting-epub-to-xps/convert-epub-to-xps-specify-xps-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Specifikace Aspose HTML Save Options pro EPUB do XPS

Převod dokumentu EPUB do XPS může být užitečnou součástí publikačního workflow a **Aspose HTML Save Options** vám poskytují detailní kontrolu nad výstupem. V tomto tutoriálu projdeme přesné kroky potřebné k nastavení těchto možností uložení pomocí Aspose.HTML pro Java a vytvoříme vysoce kvalitní soubor XPS.

## Rychlé odpovědi
- **Co dělá Aspose HTML Save Options?** Umožňuje vám přizpůsobit velikost stránky, barvu pozadí a další nastavení renderování při ukládání do formátů jako XPS.  
- **Která knihovna je vyžadována?** Aspose.HTML pro Java (nejnovější verze).  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro hodnocení; pro produkční nasazení je vyžadována komerční licence.  
- **Mohu změnit rozměry stránky?** Ano – můžete nastavit libovolnou šířku a výšku pomocí `PageSetup`.  
- **Je převod rychlý?** U typických souborů EPUB převod dokončí během několika sekund na moderním JVM.

## Co jsou Aspose HTML Save Options?
Aspose HTML Save Options jsou sada vlastností, které řídí, jak jsou HTML, EPUB nebo jiné webové dokumenty renderovány a ukládány do cílového formátu, jako je XPS, PDF nebo soubory obrázků. Umožňují vám definovat rozvržení stránky, barvy pozadí, okraje a další, čímž zajišťují, že výsledný soubor odpovídá vašim požadavkům na design.

## Proč použít Aspose.HTML pro Java k převodu EPUB do XPS?
- **Vysoká věrnost** – zachovává složité rozvržení, písma a vektorovou grafiku.  
- **Programová kontrola** – automatizujte hromadné převody v Java aplikacích.  
- **Žádné externí závislosti** – čistá Java knihovna, bez nativních komponent.  
- **Přizpůsobitelný výstup** – díky možnostem uložení můžete XPS přizpůsobit přesně podle svých potřeb.

## Předpoklady

Než se ponoříme do kódu, ujistěte se, že máte následující:

1. **Java vývojové prostředí** – nainstalovaný JDK 8 nebo vyšší.  
2. **Knihovna Aspose.HTML pro Java** – stáhněte ji z [download link](https://releases.aspose.com/html/java/).  
3. **Soubor EPUB** – zdrojový EPUB, který chcete převést.  

Mít tyto položky připravené vám umožní postupovat krok za krokem bez přerušení.

## Import balíčků

Nejprve importujte požadované třídy. Umístěte importy na začátek vašeho Java souboru:

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

Tyto importy vám poskytují přístup k převodnímu enginu a **Aspose HTML Save Options**, které jsou potřebné pro jemné ladění.

## Otevření souboru EPUB

Dále otevřete EPUB, který chcete převést. Pomocník `Resources.input` načte soubor z adresáře demo zdrojů:

```java
try (FileInputStream fileInputStream = new FileInputStream(Resources.input("input.epub"))) {
    // Your code for the EPUB file handling goes here.
}
```

Použití bloku try‑with‑resources zajišťuje automatické uzavření proudu.

## Vytvoření XPS Save Options (nastavení velikosti stránky a pozadí)

Nyní vytvoříme instanci `XpsSaveOptions` a přizpůsobíme ji. Zde **save options** skutečně zazáří:

```java
XpsSaveOptions options = new XpsSaveOptions();
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
anyPage.setSize(new Size(Length.fromPixels(3000), Length.fromPixels(1000)));
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

- **Velikost stránky** – v tomto příkladu nastavena na 3000 × 1000 pixelů; upravte podle požadované velikosti papíru.  
- **Barva pozadí** – `AliceBlue` ukazuje, jak změnit pozadí plátna; můžete zvolit libovolnou `Color`.  

Toto nastavení je součástí **Aspose HTML Save Options**, které ovlivňují finální XPS dokument.

## Převod EPUB do XPS

Nakonec zavolejte převodník s proudem, nakonfigurovanými možnostmi a výstupní cestou:

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.xps")
);
```

Když se tento řádek spustí, Aspose.HTML načte EPUB, použije nastavení stránky a barvu pozadí, kterou jste definovali, a zapíše plně kompatibilní XPS soubor.

## Časté problémy a tipy

- **Nesprávné rozměry stránky** – ujistěte se, že rozměry jsou vyjádřeny v pixelech (nebo použijte `Length.fromInches`).  
- **Chybějící písma** – vložte požadovaná písma do EPUB nebo je nainstalujte na hostitele JVM, aby se předešlo náhradním písmům.  
- **Velké soubory** – u velmi velkých EPUB souborů zvyšte haldu JVM (`-Xmx`), aby se zabránilo `OutOfMemoryError`.  

## Závěr

Využitím **Aspose HTML Save Options** získáte přesnou kontrolu nad tím, jak je EPUB renderován do XPS. Výše uvedené kroky ukazují, jak nastavit velikost stránky, barvu pozadí a provést převod pomocí několika řádků Java kódu. Začleňte tento vzor do svých dávkových zpracovatelských pipeline, abyste efektivně automatizovali publikační úkoly.

## Často kladené otázky

**Q: Co je Aspose.HTML pro Java?**  
A: Jedná se o Java knihovnu, která umožňuje vývojářům vytvářet, upravovat, renderovat a převádět HTML, EPUB a další webové dokumenty bez potřeby prohlížeče.

**Q: Mohu to použít v komerčním projektu?**  
A: Ano. Pro produkční použití potřebujete platnou licenci. Můžete si ji zakoupit na [purchase page](https://purchase.aspose.com/buy).

**Q: Je k dispozici bezplatná zkušební verze?**  
A: Rozhodně. Stáhněte si zkušební verzi z [here](https://releases.aspose.com/).

**Q: Kde mohu získat podporu?**  
A: Komunitní podpora a oficiální asistence jsou k dispozici na fórech Aspose na adrese [https://forum.aspose.com/](https://forum.aspose.com/).

**Q: Jaké jsou systémové požadavky?**  
A: Java Development Kit (JDK) 8+ a operační systém podporovaný runtime Aspose. Ujistěte se, že vaše prostředí splňuje výše uvedené předpoklady.

---

**Poslední aktualizace:** 2026-01-09  
**Testováno s:** Aspose.HTML for Java 24.12  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
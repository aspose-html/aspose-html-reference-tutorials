---
date: 2026-03-29
description: Zjistěte, jak používat Aspose.HTML pro Javu k nastavení možností uložení
  do XPS, převodu EPUB do XPS a správě licencí.
linktitle: Specifying XPS Save Options for EPUB to XPS
second_title: Java HTML Processing with Aspose.HTML
title: Jak použít možnosti uložení Aspose HTML pro EPUB do XPS
url: /cs/java/converting-epub-to-xps/convert-epub-to-xps-specify-xps-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak použít Aspose HTML Save Options pro převod EPUB na XPS

V tomto průvodci ukážeme **jak použít Aspose** HTML Save Options k převodu dokumentu EPUB na XPS s úplnou kontrolou nad rozměry stránky, barvou pozadí a licenčními podmínkami. Ať už vytváříte dávkový zpracovatelský řetězec nebo jednorázový konverzní nástroj, tyto kroky vám pomohou rychle získat spolehlivé výsledky.

## Rychlé odpovědi
- **Co dělá Aspose HTML Save Options?** Umožňuje vám přizpůsobit velikost stránky, barvu pozadí a další nastavení vykreslování při ukládání do formátů jako XPS.  
- **Která knihovna je vyžadována?** Aspose.HTML pro Java (nejnovější verze).  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro hodnocení; pro produkci je vyžadována komerční licence.  
- **Mohu změnit rozměry stránky?** Ano – můžete nastavit libovolnou šířku a výšku pomocí `PageSetup`.  
- **Je konverze rychlá?** Pro typické soubory EPUB konverze proběhne během několika sekund na moderním JVM.

## Co znamená „jak použít aspose“ v tomto kontextu?
Fráze **jak použít Aspose** odkazuje na praktické kroky využití knihovny Aspose.HTML k manipulaci a konverzi webových dokumentů. V tomto tutoriálu se zaměřujeme na **aspose html save options**, které vám umožní jemně doladit výstup při **převodu EPUB na XPS**.

## Proč použít Aspose.HTML pro Java k převodu EPUB na XPS?
- **Vysoká věrnost** – zachovává složité rozvržení, písma a vektorovou grafiku.  
- **Programová kontrola** – automatizujte dávkové konverze v Java aplikacích.  
- **Žádné externí závislosti** – čistá Java knihovna, bez nativních komponent.  
- **Přizpůsobitelný výstup** – díky možnostem ukládání můžete upravit XPS přesně podle svých potřeb, například **specifikovat rozměry stránky** nebo nastavit vlastní pozadí.  

## Předpoklady

Než se ponoříme do kódu, ujistěte se, že máte následující:

1. **Vývojové prostředí Java** – nainstalovaný JDK 8 nebo vyšší.  
2. **Knihovna Aspose.HTML pro Java** – stáhněte ji z [odkaz ke stažení](https://releases.aspose.com/html/java/).  
3. **Soubor EPUB** – zdrojový EPUB, který chcete **převést EPUB na XPS**.  

Mít tyto připravené vám umožní sledovat kroky bez přerušení.

## Import balíčků

Nejprve importujte požadované třídy. Umístěte importy na začátek vašeho Java zdrojového souboru:

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

Tyto importy vám poskytují přístup k převodnímu enginu a **Aspose HTML Save Options** potřebným pro jemné ladění.

## Otevření souboru EPUB

Dále otevřete EPUB, který chcete převést. Pomocník `Resources.input` načte soubor z adresáře demo zdrojů:

```java
try (FileInputStream fileInputStream = new FileInputStream(Resources.input("input.epub"))) {
    // Your code for the EPUB file handling goes here.
}
```

Použití bloku try‑with‑resources zajišťuje automatické uzavření proudu.

## Vytvoření XPS Save Options (nastavení velikosti stránky a pozadí)

Nyní vytvoříme instanci `XpsSaveOptions` a přizpůsobíme ji. Zde **save options** opravdu zazáří:

```java
XpsSaveOptions options = new XpsSaveOptions();
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
anyPage.setSize(new Size(Length.fromPixels(3000), Length.fromPixels(1000)));
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

- **Velikost stránky** – v tomto příkladu nastavena na 3000 × 1000 pixelů; upravte podle cílové velikosti papíru nebo použijte `Length.fromInches` k **specifikaci rozměrů stránky** v palcích.  
- **Barva pozadí** – `AliceBlue` ukazuje, jak změnit pozadí plátna; můžete vybrat libovolnou `Color`.  

Toto nastavení je součástí **aspose html save options**, které ovlivňují finální XPS dokument.

## Převod EPUB na XPS

Nakonec zavolejte konvertor s proudem, nakonfigurovanými možnostmi a výstupní cestou:

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.xps")
);
```

Když tento řádek běží, Aspose.HTML načte EPUB, použije nastavení stránky a barvu pozadí, kterou jste definovali, a zapíše plně kompatibilní XPS soubor.

## Časté problémy a tipy

- **Nesprávné rozměry stránky** – ujistěte se, že rozměry jsou vyjádřeny v pixelech (nebo použijte `Length.fromInches`).  
- **Chybějící písma** – vložte požadovaná písma do EPUB nebo je nainstalujte na hostiteli JVM, aby nedošlo k náhradě.  
- **Velké soubory** – pro velmi velké EPUBy zvyšte haldu JVM (`-Xmx`), aby se zabránilo `OutOfMemoryError`.  
- **Licencování Aspose HTML** – ujistěte se, že máte načtenou platnou licenci před konverzí; jinak se zobrazí vodotisk z trial verze.

## Závěr

Využitím **Aspose HTML Save Options** získáte přesnou kontrolu nad tím, jak je EPUB renderován do XPS. Výše uvedené kroky vám ukazují, jak **převést EPUB**, nastavit **rozměry stránky**, změnit pozadí a provést konverzi pomocí několika řádků Java kódu. Začleňte tento vzor do vašich dávkových zpracovatelských řetězců pro efektivní automatizaci publikovacích úkolů.

## Často kladené otázky

**Q: Co je Aspose.HTML pro Java?**  
A: Jedná se o Java knihovnu, která umožňuje vývojářům vytvářet, upravovat, renderovat a konvertovat HTML, EPUB a další webové dokumenty bez potřeby prohlížeče.

**Q: Mohu to použít v komerčním projektu?**  
A: Ano. Pro produkční použití potřebujete platnou licenci. Můžete si ji zakoupit na [stránka nákupu](https://purchase.aspose.com/buy).

**Q: Je k dispozici bezplatná zkušební verze?**  
A: Rozhodně. Stáhněte si trial verzi z [zde](https://releases.aspose.com/).

**Q: Kde mohu získat podporu?**  
A: Komunitní podpora a oficiální asistence jsou k dispozici prostřednictvím fór Aspose na [https://forum.aspose.com/](https://forum.aspose.com/).

**Q: Jaké jsou systémové požadavky?**  
A: Java Development Kit (JDK) 8+ a operační systém podporovaný runtime Aspose. Ujistěte se, že vaše prostředí splňuje výše uvedené předpoklady.

---

**Last Updated:** 2026-03-29  
**Tested With:** Aspose.HTML for Java 24.12  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
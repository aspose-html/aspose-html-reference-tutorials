---
category: general
date: 2026-02-14
description: Jak nastavit DPI při konverzi SVG na PNG pomocí Javy. Exportujte PNG
  ve vysokém rozlišení, naučte se převádět SVG na PNG a použijte knihovnu pro konverzi
  obrázků v Javě.
draft: false
keywords:
- how to set dpi
- convert svg to png
- export high resolution png
- how to convert svg
- java image conversion library
language: cs
og_description: Jak nastavit DPI při konverzi SVG na PNG pomocí Javy. Tento průvodce
  vám ukáže, jak exportovat PNG ve vysokém rozlišení a použít knihovnu pro konverzi
  obrázků v Javě.
og_title: Jak nastavit DPI při převodu SVG na PNG v Javě
tags:
- java
- image-conversion
- svg
- png
title: Jak nastavit DPI při převodu SVG na PNG v Javě
url: /cs/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak nastavit DPI při převodu SVG na PNG v Javě

Už jste se někdy zamysleli **jak nastavit DPI** při převodu SVG‑to‑PNG, aby výsledek vypadal ostrý na tiskovém posteru připraveném k tisku? Nejste v tom jediní. V mnoha projektech—například marketingové letáky, UI mockupy nebo technické diagramy—je získání vysoce rozlišeného PNG z SVG nevyjednatelný.  

V tomto tutoriálu projdeme přesně kroky k **převodu SVG na PNG**, **exportu vysoce rozlišeného PNG** a, co je nejdůležitější, ke kontrole DPI pomocí knihovny Aspose.HTML for Java. Na konci budete mít znovupoužitelný úryvek kódu, který můžete vložit do jakékoli Java aplikace, ať už budujete desktopový nástroj nebo backendovou službu.

## Co budete potřebovat

- **Java 8+** (kód se kompiluje s jakýmkoli recentním JDK)
- **Aspose.HTML for Java** JARs (k dispozici na Maven Central nebo na webu Aspose)
- SVG soubor, který chcete rasterizovat  
- Špetka zvědavosti—nic víc.

Pokud vám vyhovuje Maven, stačí přidat závislost uvedenou v následující sekci; jinak si JARy stáhněte ručně a přidejte je do classpath.

## Krok 1: Přidejte knihovnu pro konverzi obrázků v Javě

Nejprve—váš projekt potřebuje **java image conversion library**, která skutečně umí číst SVG a zapisovat PNG. Aspose.HTML je solidní volba, protože zajišťuje CSS, fonty i složité vektorové funkce přímo z krabice.

**Uživatelé Maven** mohou vložit toto do svého `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- use the latest stable version -->
</dependency>
```

**Fanoušci Gradle** mohou přidat:

```gradle
implementation 'com.aspose:aspose-html:23.12'
```

Pokud dáváte přednost manuální cestě, stáhněte JAR ze stránky Aspose a umístěte jej do `libs/`, poté jej přidejte do build path vašeho IDE.

> **Pro tip:** Sledujte číslo verze; novější vydání často zlepšují práci s DPI a opravují okrajové chyby.

## Krok 2: Vytvořte možnosti konverze a nastavte požadované DPI

Nyní, když je knihovna na palubě, musíme jí říct, *jak* má výstupní PNG vypadat. Zde vstupuje hlavní klíčové slovo—**jak nastavit DPI**. Třída `ImageConversionOptions` vám dává detailní kontrolu nad horizontálním (`dpiX`) i vertikálním (`dpiY`) rozlišením.

```java
import com.aspose.html.converters.ImageConversionOptions;

// Step 2: Build the options object and set DPI
ImageConversionOptions conversionOptions = new ImageConversionOptions();
conversionOptions.setDpiX(300); // 300 DPI horizontally
conversionOptions.setDpiY(300); // 300 DPI vertically
```

Proč 300 DPI? Pro většinu tiskových workflow se 300 dots‑per‑inch považuje za „tiskovou kvalitu“. Pokud cílíte jen na web, můžete snížit na 72 nebo 96 DPI, aby soubory zůstaly menší.

> **Co když potřebuji jiné DPI pro šířku a výšku?**  
> Stačí změnit `setDpiX` a `setDpiY` nezávisle. Knihovna respektuje neuniformní hodnoty, což je užitečné pro anamorfní obrázky.

## Krok 3: Proveďte převod SVG na PNG

S připravenými možnostmi je samotná konverze jedním statickým voláním. Použijeme `java.nio.file.Paths`, aby byl kód platformově nezávislý.

```java
import com.aspose.html.converters.Converter;
import java.nio.file.Paths;

public class SvgToPng {
    public static void main(String[] args) throws Exception {
        // Paths to input SVG and output PNG
        var inputSvg  = Paths.get("YOUR_DIRECTORY/input.svg").toUri();
        var outputPng = Paths.get("YOUR_DIRECTORY/output.png").toUri();

        // Convert using the DPI settings we defined earlier
        Converter.convert(inputSvg, outputPng, conversionOptions);
    }
}
```

A to je vše—spusťte metodu `main` a najdete ostrý PNG s 300 DPI v `YOUR_DIRECTORY`. Knihovna automaticky škáluje vektorovou grafiku tak, aby odpovídala zadanému DPI, zachovává poměr stran i čitelnost textu.

## Krok 4: Ověřte výsledek (volitelné, ale doporučené)

Rychlá kontrola může ušetřit spoustu problémů později. Otevřete vygenerovaný PNG v libovolném prohlížeči, který zobrazuje DPI metadata (např. Photoshop, GIMP nebo i Windows Explorer v záložce „Details“). Měli byste vidět **300 DPI** uvedené pod horizontálním i vertikálním rozlišením.

Pokud soubor vypadá rozmazaně, zkontrolujte:

1. Originální SVG není už od začátku nízkého rozlišení (vektorové soubory jsou rozlišení‑agnostické, ale vložené rastrové obrázky uvnitř nich mohou kvalitu omezovat).  
2. Skutečně jste soubor uložili po nastavení DPI—někdy IDE kešují staré sestavení.  
3. Možnosti konverze nebyly přepsány jinde ve vašem kódu.

## Proč je DPI důležité pro export vysoce rozlišeného PNG

Možná se ptáte: „Proč vůbec řešit DPI? Není PNG jen o pixelech?“ Pravda je, že DPI je *metadata* tag, který říká následným aplikacím (zejména těm orientovaným na tisk), kolik pixelů odpovídá palci fyzického prostoru. Pokud předáte tiskárně PNG 1200 × 800 bez správného DPI, tiskárna může předpokládat výchozí (často 72 DPI) a zvětší obrázek, což vede k rozmazanému výstupu.

Správné nastavení DPI je také výkonnostní výhoda: vyhnete se nutnosti později upscale‑ovat rastrové obrázky, což může být výpočetně náročné a snižovat kvalitu.

## Okrajové případy a běžné úskalí

| Situace | Na co si dát pozor | Jak opravit |
|-----------|-------------------|------------|
| **SVG obsahuje vložené bitmapové obrázky** | Vložená bitmapa může být nízkého rozlišení, což způsobí, že finální PNG bude pixelovaný i při vysokém DPI. | Nahraďte bitmapu verzí s vyšším rozlišením nebo upravte SVG tak, aby odkazovala na externí obrázek. |
| **Velké hodnoty DPI (např. 1200 DPI)** | Spotřeba paměti prudce roste; můžete narazit na `OutOfMemoryError`. | Zvyšte velikost haldy JVM (`-Xmx2g`) nebo omezte DPI na rozumnou maximální hodnotu pro váš případ použití. |
| **Nekvadratické pixely** | Některé displeje interpretují DPI odlišně, což vede k roztaženým obrázkům. | Ujistěte se, že `setDpiX` se rovná `setDpiY`, pokud nemáte konkrétní důvod je li odlišit. |
| **Chybějící fonty** | Text v SVG může přejít na výchozí font, což změní rozvržení. | Vložte fonty do SVG nebo nainstalujte požadované fonty na běhovém stroji. |

## Rychlé shrnutí (v jedné větě)

Pro **jak nastavit DPI** při převodu SVG‑to‑PNG vytvořte objekt `ImageConversionOptions`, nastavte `dpiX`/`dpiY` a zavolejte `Converter.convert` z knihovny Aspose.HTML for Java.

## Další kroky a související témata

- **Dávkové zpracování:** Procházejte adresář se SVG soubory a aplikujte stejná nastavení DPI.  
- **Dynamické DPI:** Načtěte konfigurační soubor nebo argument příkazové řádky a nastavte DPI za běhu.  
- **Alternativní knihovny:** Pokud nemůžete použít Aspose, zvažte **Batik** (Apache) nebo **SVG Salamander**, i když mohou vyžadovat další kód pro práci s DPI.  
- **Export vysoce rozlišeného PNG** pro Android assety: kombinujte tuto techniku s Androidovými složkami `drawable‑hdpi`, `xhdpi` atd.

Klidně experimentujte—zkuste 72 DPI pro webové náhledy, 600 DPI pro velkoformátové tisky nebo i 150 DPI jako střední variantu. Kód zůstává stejný; mění se jen čísla.

---

![jak nastavit dpi](placeholder-image.png "Ilustrace nastavení DPI v pracovním postupu konverze v Javě")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
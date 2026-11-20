---
category: general
date: 2026-03-29
description: Jak vložit obrázky při převodu MHTML na PDF pomocí Aspose HTML. Zmenšete
  velikost PDF souboru a během několika minut zvládněte techniky převodu Aspose HTML
  na PDF.
draft: false
keywords:
- how to embed images
- convert mhtml to pdf
- reduce pdf file size
- aspose html to pdf
- reduce pdf size
language: cs
og_description: Jak vložit obrázky při převodu MHTML na PDF pomocí Aspose HTML. Naučte
  se snížit velikost souboru PDF a využít naplno Aspose HTML do PDF.
og_title: Jak vložit obrázky při převodu MHTML na PDF – průvodce Aspose
tags:
- Aspose
- Java
- PDF
- MHTML
title: Jak vložit obrázky při převodu MHTML na PDF – průvodce Aspose
url: /cs/java/conversion-html-to-other-formats/how-to-embed-images-when-converting-mhtml-to-pdf-aspose-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vložit obrázky při převodu MHTML na PDF – průvodce Aspose

Už jste se někdy zamýšleli **jak vložit obrázky** během převodu MHTML‑na‑PDF a zároveň udržet výsledný soubor úsporný? Nejste v tom sami. Mnoho vývojářů narazí na problém, když jejich PDF soubory narostou, protože každá zdrojová položka — písma, skripty, dokonce i drobné ikony — se vloží dovnitř. Dobrá zpráva? S Aspose.HTML pro Java můžete konvertoru říci, aby vložil **pouze obrázky**, zatímco vše ostatní zůstane jako externí odkazy. Tato jediná úprava často dramaticky zmenší velikost PDF.

V tomto tutoriálu vás provedeme převodem MHTML zprávy na PDF, zaměříme se na **jak vložit obrázky** a přidáme několik dalších tipů, jak **snížit velikost PDF souboru**. Na konci budete mít připravenou Java třídu připravenou ke spuštění, pochopíte, proč je důležité vkládat jen obrázky, a budete vědět, kam se obrátit, pokud později budete potřebovat vložit písma nebo jiné zdroje. Žádné nejasné odkazy typu „viz dokumentace“ — jen kompletní řešení připravené ke zkopírování.

## Co se naučíte

- Přesné volání API potřebné k **převodu MHTML na PDF** pomocí Aspose.HTML.
- Jak nakonfigurovat `PdfConversionOptions`, aby konvertor **vložen pouze obrázky**.
- Proč vkládání pouze obrázků pomáhá **snížit velikost PDF** a kdy můžete chtít jiné nastavení.
- Úplný, spustitelný Java příklad, který můžete vložit do jakéhokoli Maven/Gradle projektu.
- Běžné úskalí (chybějící zdroje, špatné cesty k souborům) a rychlé opravy.

### Požadavky

- Java 8 nebo novější nainstalovaná.
- Maven nebo Gradle pro správu závislostí (ukážeme Maven úryvek).
- Knihovna Aspose.HTML pro Java (můžete si stáhnout bezplatnou zkušební verzi z webu Aspose).
- Soubor MHTML, který chcete převést na PDF (v příkladu se používá `report.mhtml`).

> **Tip:** Uchovávejte svůj MHTML a výstupní PDF ve stejné složce během testování; relativní cesty udržují věci přehledné.

---

## Krok 1 – Přidejte Aspose.HTML do svého projektu

Pokud používáte Maven, vložte následující do svého `pom.xml`. Zobrazená verze je nejnovější k březnu 2026; zkontrolujte repozitář Aspose pro novější vydání.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

Pro Gradle je ekvivalent:

```groovy
implementation 'com.aspose:aspose-html:23.12'
```

Jakmile se závislost vyřeší, můžete importovat třídy, které budeme potřebovat.

## Krok 2 – Vytvořte možnosti převodu a nastavte režim vkládání

Jádro **jak vložit obrázky** spočívá v `PdfConversionOptions`. Ve výchozím nastavení Aspose vkládá *všechny* zdroje (písma, CSS, obrázky). Změníme to na `EMBED_IMAGES_ONLY`.

```java
// Step 2: Prepare conversion options – embed only images
PdfConversionOptions options = new PdfConversionOptions();
options.setResourceEmbeddingMode(ResourceEmbeddingMode.EMBED_IMAGES_ONLY);
```

Proč je to důležité? Představte si firemní zprávu, která odkazuje na firemní písmo uložené na síťovém disku. Vložení tohoto písma nafoukne PDF o stovky kilobajtů, i když si jej prohlížeč může stáhnout vzdáleně. Vložením pouze obrázků PDF zachová požadovanou vizuální věrnost a zároveň zůstane lehké.

## Krok 3 – Proveďte převod

Nyní zavoláme `Converter.convert`, předáme cestu ke zdrojovému MHTML, cestu k výstupnímu PDF a možnosti, které jsme právě nakonfigurovali.

```java
// Step 3: Convert MHTML to PDF using the options above
String sourcePath = "YOUR_DIRECTORY/report.mhtml";
String targetPath = "YOUR_DIRECTORY/report.pdf";

Converter.convert(sourcePath, targetPath, options);
```

Pokud je vše správně nastaveno, objeví se `report.pdf` vedle vašeho MHTML souboru. Otevřete jej – každá obrázek z původní zprávy by měl být přítomen, zatímco písma a CSS zůstanou externími odkazy.

## Krok 4 – Ověřte snížení velikosti PDF

Rychlá kontrola pomůže potvrdit, že jste skutečně **snížili velikost PDF**. Porovnejte velikost souboru před a po změně režimu vkládání:

```java
File before = new File("YOUR_DIRECTORY/report_full.pdf"); // generated with default settings
File after  = new File(targetPath); // our image‑only PDF

System.out.println("Full embed size: " + before.length() / 1024 + " KB");
System.out.println("Images‑only size: " + after.length() / 1024 + " KB");
```

Ve většině případů uvidíte pokles o 30‑70 % v závislosti na tom, kolik písem nebo CSS souborů bylo původně vloženo. To je značná výhra pro každého, kdo distribuuje PDF přes web nebo je ukládá do cloudového úložiště.

## Krok 5 – Kompletní, spustitelný příklad

Níže je celá Java třída, kterou můžete zkopírovat do svého IDE. Nahraďte `YOUR_DIRECTORY` skutečnou cestou ke složce, kde se nachází `report.mhtml`.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfConversionOptions;
import com.aspose.html.converters.ResourceEmbeddingMode;

import java.io.File;

public class MhtmlToPdf {
    public static void main(String[] args) throws Exception {

        // ---------- Step 1: Define source and destination ----------
        String sourcePath = "YOUR_DIRECTORY/report.mhtml";
        String targetPath = "YOUR_DIRECTORY/report.pdf";

        // ---------- Step 2: Set conversion options (embed only images) ----------
        PdfConversionOptions conversionOptions = new PdfConversionOptions();
        conversionOptions.setResourceEmbeddingMode(ResourceEmbeddingMode.EMBED_IMAGES_ONLY);

        // ---------- Step 3: Run the conversion ----------
        Converter.convert(sourcePath, targetPath, conversionOptions);
        System.out.println("Conversion complete! PDF saved to: " + targetPath);

        // ---------- Step 4: (Optional) Show size reduction ----------
        File outputPdf = new File(targetPath);
        System.out.println("Resulting PDF size: " + outputPdf.length() / 1024 + " KB");
    }
}
```

**Očekávaný výstup** (na konzoli):

```
Conversion complete! PDF saved to: YOUR_DIRECTORY/report.pdf
Resulting PDF size: 842 KB
```

Otevřete `report.pdf` v libovolném prohlížeči; měly by se zobrazit všechny původní obrázky správně. Pokud chybí některé obrázky, zkontrolujte, zda jsou URL obrázků v MHTML absolutní nebo zda jsou soubory přístupné z konverzního stroje.

## Časté otázky a řešení okrajových případů

### Co když *potřebuji* vložit písma?

Přepněte `ResourceEmbeddingMode` na `EMBED_ALL` nebo `EMBED_FONTS_ONLY`. Výčtový typ nabízí čtyři možnosti:

| Režim                     | Co se vloží |
|---------------------------|-------------|
| `EMBED_ALL`               | Obrázky, písma, CSS |
| `EMBED_IMAGES_ONLY`       | Pouze obrázky (náš výchozí) |
| `EMBED_FONTS_ONLY`        | Pouze písma |
| `EMBED_NONE`              | Nic (pouze externí odkazy) |

### Můj MHTML obsahuje externí CSS, který ovlivňuje rozvržení – bude PDF poškozený?

Protože CSS nevkládáme, konvertor jej během převodu stále stáhne. Pokud je CSS umístěn na intranetu, ke kterému konverzní server nemá přístup, může se rozvržení vrátit k výchozím hodnotám. V takových případech buď vložte CSS (`EMBED_ALL`), nebo zkopírujte stylopis lokálně a upravte MHTML, aby odkazoval na lokální soubor.

### Můžu dávkově zpracovat složku souborů MHTML?

Určitě. Zabalte logiku převodu do smyčky, která iteruje přes `File.listFiles()` a podle toho mění cílový název souboru. Jen nezapomeňte pro výkon znovu použít jedinou instanci `PdfConversionOptions`.

### Co s paměťovou náročností u obrovských dokumentů?

Aspose.HTML streamuje obsah, takže využití paměti zůstává skromné. Nicméně velmi velké obrázky mohou stále způsobovat špičky. Pokud narazíte na `OutOfMemoryError`, zvažte snížení rozlišení obrázků před jejich vložením — Aspose nabízí `ImageConversionOptions` pro tento účel, ale to je téma pro jiný tutoriál.

## Závěr

Nyní víte **jak vložit obrázky** při převodu MHTML na PDF pomocí Aspose.HTML a viděli jste, proč toto malé nastavení může **dramatically snížit velikost PDF souboru**. Kompletní Java příklad připravený ke zkopírování ukazuje celý proces – od přidání Maven závislosti až po vytištění konečné velikosti souboru.

From here you might:

- Experimentovat s `EMBED_FONTS_ONLY`, pokud vaše PDF musí být zcela samostatná.
- Automatizovat dávkové převody pro celou složku zpráv.
- Kombinovat tuto techniku s PDF optimalizačními API od Aspose pro ještě menší soubory.

Ať už budujete reportingovou službu, pipeline e‑mail‑na‑PDF, nebo jen uklízíte archivované webové stránky, řízení toho, co se vloží, je klíčovým faktorem pro výkon a náklady. Vyzkoušejte to, upravte možnosti a nechte své PDF zůstat co nejštíhlejší.

*Šťastné programování!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
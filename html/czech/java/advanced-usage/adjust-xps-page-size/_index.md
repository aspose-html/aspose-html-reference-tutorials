---
date: 2026-08-28
description: Upravit velikost stránky XPS při převodu HTML na XPS v Javě pomocí Aspose.HTML.
  Vykreslit HTML do XPS s přesnými rozměry.
keywords:
- adjust xps page size
- render html to xps
- aspose.html java
- xps conversion java
- html to xps
lastmod: 2026-08-28
linktitle: Úprava velikosti stránky XPS
og_description: Upravit velikost stránky XPS při převodu HTML na XPS v Javě pomocí
  Aspose.HTML. Naučte se vykreslovat HTML do XPS s přesnými rozměry během několika
  sekund.
og_image_alt: Tutorial showing how to adjust XPS page size during HTML to XPS conversion
  with Aspose.HTML for Java
og_title: Upravit velikost stránky XPS při převodu HTML na XPS v Javě
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Adjust XPS page size while converting HTML to XPS in Java using Aspose.HTML.
    Render HTML to XPS with precise dimensions.
  headline: Adjust XPS page size when converting HTML to XPS in Java
  type: TechArticle
- description: Adjust XPS page size while converting HTML to XPS in Java using Aspose.HTML.
    Render HTML to XPS with precise dimensions.
  name: Adjust XPS page size when converting HTML to XPS in Java
  steps:
  - name: set the input file name
    text: The `FileInputStream` class reads raw bytes from a file, providing the HTML
      source to the renderer.
  - name: create an HTML document and set styles
    text: The `HTMLDocument` class represents an in‑memory HTML DOM used by Aspose.HTML
      for rendering.
  - name: create XPS rendering options
    text: The `XpsRenderingOptions` class holds settings that control how HTML is
      rendered to XPS, such as page size and image quality.
  - name: adjust the page size
    text: '**How to set XPS page size** – Define a custom page size (width × height
      in points) and tell the renderer whether it should automatically expand to the
      widest page. Setting `adjustToWidestPage` to `false` preserves the exact dimensions
      you specify. The `PageSetup` class defines page size, margins, a'
  - name: render the output
    text: The `XpsDevice` class is the rendering target that writes the processed
      content to an XPS file.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a Java library that allows developers to manipulate
      and convert HTML documents into various formats, such as XPS, PDF, and images.
      You can download the library from [Aspose.HTML for Java download page](https://releases.aspose.com/html/java/).
    question: What is Aspose.HTML for Java?
  - answer: You can download the Aspose.HTML for Java library from [Aspose product
      releases page](https://releases.aspose.com/).
    question: Where can I download Aspose.HTML for Java?
  - answer: Yes, you can get a free trial of Aspose.HTML for Java from the [temporary
      license request page](https://purchase.aspose.com/temporary-license/).
    question: Is there a free trial available for Aspose.HTML for Java?
  - answer: To get a temporary license for Aspose.HTML for Java, visit the [temporary
      license request page](https://purchase.aspose.com/temporary-license/).
    question: How can I obtain a temporary license for Aspose.HTML for Java?
  - answer: Yes, you can seek help and support from the Aspose community on the [Aspose
      Forum](https://forum.aspose.com/).
    question: Can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
tags:
- adjust xps page size
- Aspose.HTML
- Java XPS conversion
- HTML to XPS
- document rendering
title: Upravit velikost stránky XPS při převodu HTML na XPS v Javě
url: /cs/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Upravit velikost stránky XPS při převodu HTML na XPS v Javě

V tomto tutoriálu se naučíte **jak upravit velikost stránky XPS** při převodu HTML na XPS pomocí Aspose.HTML pro Java. Ať už potřebujete tisknutelné faktury, archivní zprávy nebo štítky na míru, řízení rozměrů stránky zajišťuje, že finální XPS vypadá přesně podle představ. Provedeme vás nastavením prostředí, možnostmi vykreslování a generováním finálního XPS, abyste tuto funkci mohli přímo začlenit do svých Java aplikací.

## Rychlé odpovědi
- **Co znamená „převod HTML na XPS“?** Vykreslí HTML dokument do souboru XPS, zachovává rozvržení a stylování.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro vývoj; pro produkci je vyžadována komerční licence.  
- **Která verze Javy je podporována?** Java 8 nebo vyšší (doporučeno JDK 11+).  
- **Mohu změnit velikost stránky?** Ano – Aspose.HTML vám umožní zadat vlastní rozměry před vykreslením.  
- **Jak dlouho trvá převod?** Obvykle méně než sekunda pro standardní stránky; větší dokumenty mohou trvat déle.

## Co je převod HTML na XPS?
Převod HTML na XPS znamená převzít webově orientovaný značkovací soubor a vytvořit dokument XPS (XML Paper Specification) – formát s pevnou rozvržením, připravený k tisku, podobný PDF. To je užitečné, když potřebujete vysoce věrné, zařízení‑nezávislé dokumenty pro archivaci nebo tisk z Java aplikací.

## Proč upravit velikost stránky XPS?
Úprava velikosti stránky XPS vám dává kontrolu nad fyzickými rozměry finálního dokumentu (např. A4, Letter, vlastní štítky). Zabraňuje nechtěnému škálování, zajišťuje, že obsah přesně zapadne, a může snížit velikost souboru odstraněním zbytečného bílého prostoru.

## Jak vykreslit HTML do XPS s vlastní velikostí stránky?
Načtěte svůj HTML, nakonfigurujte `XpsRenderingOptions` s `PageSetup`, který určuje přesnou šířku a výšku, kterou potřebujete, a poté vykreslete do `XpsDevice`. Tento dvoustupňový proces vám umožní zachovat rozvržení beze změny při vynucení specifikovaných rozměrů, vše v jediném volání API.

## Předpoklady

Než začneme, ujistěte se, že máte následující předpoklady:

1. **Java vývojové prostředí** – Java Development Kit (JDK) nainstalovaný ve vašem systému.  
2. **Knihovna Aspose.HTML pro Java** – Stáhněte a zahrňte knihovnu Aspose.HTML pro Java do svého projektu. Knihovnu najdete na stránce [Aspose.HTML for Java download page](https://releases.aspose.com/html/java/).  
3. **Vstupní HTML soubor** – Připravte HTML soubor, který chcete vykreslit a upravit velikost stránky XPS. Pro tento tutoriál můžete použít svůj vlastní HTML soubor.

## Import balíčků

Třída `Page` představuje rozměry a nastavení stránky pro výstup XPS. Třída `HtmlRenderer` provádí převod z HTML na XPS.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Průvodce krok za krokem

Níže je stručný, číslovaný průchod, který odráží původní kroky a zároveň přidává další kontext pro jasnost.

### Krok 1: nastavení názvu vstupního souboru

Třída `FileInputStream` čte surová data ze souboru a poskytuje HTML zdroj vykreslovači.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

### Krok 2: vytvoření HTML dokumentu a nastavení stylů

Třída `HTMLDocument` představuje v‑paměti HTML DOM používaný Aspose.HTML pro vykreslování.

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n" +
               "\n";

// ...
```

### Krok 3: vytvoření možností vykreslování XPS

Třída `XpsRenderingOptions` obsahuje nastavení, která řídí, jak je HTML vykresleno do XPS, například velikost stránky a kvalita obrázků.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

### Krok 4: úprava velikosti stránky  

**Jak nastavit velikost stránky XPS** – Definujte vlastní velikost stránky (šířka × výška v bodech) a řekněte vykreslovači, zda má automaticky rozšířit na nejširší stránku. Nastavením `adjustToWidestPage` na `false` zachováte přesné rozměry, které zadáte.

Třída `PageSetup` definuje velikost stránky, okraje a orientaci pro výstup XPS.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

### Krok 5: vykreslení výstupu

Třída `XpsDevice` je cílové zařízení pro vykreslování, které zapisuje zpracovaný obsah do souboru XPS.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Časté problémy a řešení

| Problém | Proč se to děje | Řešení |
|-------|----------------|-----|
| **Prázdný výstup XPS** | Vstupní stream není uzavřen nebo HTMLDocument ukazuje na špatný soubor. | Zajistěte, aby `FileInputStream` byl správně zabalen v bloku try‑with‑resources a cesta k souboru byla přesná. |
| **Velikost stránky se nepoužije** | `adjustToWidestPage` zůstalo nastaveno na `true`. | Nastavte `pageSetup.setAdjustToWidestPage(false);` jak je ukázáno v Kroku 4. |
| **Nesprávná podpora CSS** | Aspose.HTML podporuje podmnožinu CSS. | Držte se základního rozvržení, fontů a barev; vyhněte se pokročilým selektorům nebo CSS Grid. |
| **LicenseException** | Spuštění bez platné licence v produkci. | Použijte dočasnou nebo zakoupenou licenci před vykreslením (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Často kladené otázky

**Q: Co je Aspose.HTML pro Java?**  
A: Aspose.HTML pro Java je knihovna pro Javu, která umožňuje vývojářům manipulovat a převádět HTML dokumenty do různých formátů, jako jsou XPS, PDF a obrázky. Knihovnu můžete stáhnout ze stránky [Aspose.HTML for Java download page](https://releases.aspose.com/html/java/).

**Q: Kde mohu stáhnout Aspose.HTML pro Java?**  
A: Knihovnu Aspose.HTML pro Java můžete stáhnout ze stránky [Aspose product releases page](https://releases.aspose.com/).

**Q: Je k dispozici bezplatná zkušební verze Aspose.HTML pro Java?**  
A: Ano, můžete získat bezplatnou zkušební verzi Aspose.HTML pro Java na stránce [temporary license request page](https://purchase.aspose.com/temporary-license/).

**Q: Jak mohu získat dočasnou licenci pro Aspose.HTML pro Java?**  
A: Pro získání dočasné licence pro Aspose.HTML pro Java navštivte stránku [temporary license request page](https://purchase.aspose.com/temporary-license/).

**Q: Mohu získat podporu pro Aspose.HTML pro Java?**  
A: Ano, můžete vyhledat pomoc a podporu v komunitě Aspose na [Aspose Forum](https://forum.aspose.com/).

**Q: Mohu převádět HTML na XPS na serveru bez grafického rozhraní?**  
A: Rozhodně. Aspose.HTML funguje v prostředích bez GUI; stačí zajistit, aby byl Java runtime správně nakonfigurován.

**Q: Podporuje knihovna vlastní okraje stránky?**  
A: Ano. Použijte `PageSetup.setMarginTop()`, `setMarginBottom()` atd. před přiřazením `PageSetup` k možnostem vykreslování.

## Závěr

Prošli jsme kompletním procesem **převodu HTML na XPS** a **úpravy velikosti stránky XPS** pomocí Aspose.HTML pro Java. Dodržením těchto kroků můžete generovat tiskové XPS dokumenty, které přesně odpovídají vašim požadavkům na rozvržení. Neváhejte experimentovat s různými rozměry stránky, styly nebo dokonce přidávat záhlaví a zápatí podle potřeb vašeho projektu.

Pokud máte jakékoli otázky nebo potřebujete další pomoc, prozkoumejte [dokumentaci Aspose.HTML pro Java](https://reference.aspose.com/html/java/) nebo se připojte k diskusi na [Aspose Forum](https://forum.aspose.com/).

---

**Last Updated:** 2026-08-28  
**Testováno s:** Aspose.HTML for Java 24.11 (nejnovější v době psaní)  
**Author:** Aspose

## Související tutoriály

- [Převod HTML na XPS pomocí Aspose.HTML pro Java](/html/java/conversion-html-to-other-formats/convert-html-to-xps/)
- [Úprava velikosti PDF stránky pomocí Aspose.HTML pro Java](/html/java/advanced-usage/adjust-pdf-page-size/)
- [Převod EPUB na XPS pomocí Aspose.HTML pro Java](/html/java/converting-epub-to-xps/convert-epub-to-xps/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
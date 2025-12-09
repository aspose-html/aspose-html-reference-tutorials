---
date: 2025-11-29
description: Naučte se, jak převést HTML na XPS a upravit velikost stránky XPS pomocí
  Aspose.HTML pro Java. Jednoduše ovládejte rozměry výstupu.
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Převod HTML na XPS a úprava velikosti stránky XPS pomocí Aspose.HTML pro Javu
url: /cs/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod HTML na XPS a úprava velikosti stránky XPS pomocí Aspose.HTML pro Java

V tomto tutoriálu se dozvíte **jak převést HTML na XPS** a jemně doladit výslednou velikost stránky pomocí Aspose.HTML pro Java. Ať už generujete tisknutelné zprávy, faktury nebo archivní dokumenty, řízení rozměrů XPS zajišťuje, že výstup vypadá přesně tak, jak očekáváte. Provedeme vás každým krokem – od nastavení prostředí po vykreslení finálního XPS souboru – abyste tuto funkci mohli okamžitě integrovat do svých Java aplikací.

## Rychlé odpovědi
- **Co znamená „převod HTML na XPS“?** Převádí HTML dokument do XPS souboru, přičemž zachovává rozvržení a stylování.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro vývoj; pro produkci je vyžadována komerční licence.  
- **Jaká verze Javy je podporována?** Java 8 nebo vyšší (doporučeno JDK 11+).  
- **Mohu změnit velikost stránky?** Ano – Aspose.HTML vám umožní před vykreslením zadat vlastní rozměry.  
- **Jak dlouho trvá převod?** Obvykle méně než sekunda pro standardní stránky; u větších dokumentů může trvat déle.

## Co je převod HTML na XPS?
Převod HTML na XPS znamená převést soubor s webovým značkováním do dokumentu XPS (XML Paper Specification) – formátu s pevnou stránkou připraveným k tisku, podobně jako PDF. To je užitečné, když potřebujete vysoce věrné, zařízení nezávislé dokumenty pro archivaci nebo tisk z Java aplikací.

## Proč upravit velikost stránky XPS?
Úprava velikosti stránky vám dává kontrolu nad fyzickými rozměry finálního dokumentu (např. A4, Letter, vlastní štítky). Zabraňuje nechtěnému škálování, zajišťuje, že obsah přesně zapadne, a může snížit velikost souboru odstraněním zbytečného bílého prostoru.

## Požadavky

Než začneme, ujistěte se, že máte následující:

1. **Java vývojové prostředí** – nainstalovaný Java Development Kit (JDK) na vašem systému.  
2. **Aspose.HTML pro Java knihovna** – stáhněte a zahrňte knihovnu Aspose.HTML pro Java do svého projektu. Knihovnu najdete [zde](https://releases.aspose.com/html/java/).  
3. **Vstupní HTML soubor** – připravte HTML soubor, který chcete převést a upravit velikost stránky XPS. Pro tento tutoriál můžete použít svůj vlastní HTML soubor.

## Import balíčků

Nejprve importujte třídy, které budete potřebovat. Tyto balíčky vám poskytují přístup k manipulaci s dokumenty, vykreslování a nastavení stránky.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Krok 1: Nastavte název vstupního souboru

Načtěte zdrojový HTML soubor pomocí `FileInputStream`. Tento stream předává surové HTML do Aspose.HTML enginu.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

## Krok 2: Vytvořte HTML dokument a nastavte styly

Vytvořte instanci `HTMLDocument`, která představuje obsah, který budete vykreslovat. V tomto příkladu také vložíme malý CSS blok pro demonstraci stylování – klidně jej nahraďte svým vlastním značkováním.

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

## Krok 3: Vytvořte možnosti vykreslování XPS

Instancujte `XpsRenderingOptions`, která obsahuje všechna nastavení ovlivňující převod z HTML na XPS.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

## Krok 4: Upravit velikost stránky

Definujte vlastní velikost stránky (šířka × výška v bodech) a řekněte rendereru, zda má automaticky rozšířit na nejširší stránku. Nastavení `adjustToWidestPage` na `false` zachová přesné rozměry, které zadáte.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

## Krok 5: Vykreslete výstup

Nakonec vytvořte `XpsDevice` s nakonfigurovanými možnostmi a vykreslete HTML dokument. Výsledkem je plně vytvořený XPS soubor s vlastními rozměry stránky, které jste nastavili.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Časté problémy a řešení

| Problém | Proč se to děje | Řešení |
|---------|----------------|--------|
| **Prázdný XPS výstup** | Vstupní stream není uzavřen nebo `HTMLDocument` ukazuje na špatný soubor. | Ujistěte se, že `FileInputStream` je správně zabalen v bloku try‑with‑resources a cesta k souboru je přesná. |
| **Velikost stránky se nepoužije** | `adjustToWidestPage` zůstalo nastaveno na `true`. | Nastavte `pageSetup.setAdjustToWidestPage(false);` jak je ukázáno v kroku 4. |
| **Nesprávná podpora CSS** | Aspose.HTML podporuje jen podmnožinu CSS. | Držte se základního rozvržení, fontů a barev; vyhněte se pokročilým selektorům nebo CSS Grid. |
| **LicenseException** | Spuštěno bez platné licence v produkci. | Aplikujte dočasnou nebo zakoupenou licenci před vykreslením (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Často kladené otázky

**Q: Co je Aspose.HTML pro Java?**  
A: Aspose.HTML pro Java je knihovna pro Javu, která umožňuje vývojářům manipulovat a převádět HTML dokumenty do různých formátů, jako jsou XPS, PDF a obrázky.

**Q: Kde si mohu stáhnout Aspose.HTML pro Java?**  
A: Knihovnu Aspose.HTML pro Java můžete stáhnout z [tohoto odkazu](https://releases.aspose.com/html/java/).

**Q: Je k dispozici bezplatná zkušební verze Aspose.HTML pro Java?**  
A: Ano, bezplatnou zkušební verzi získáte [zde](https://releases.aspose.com/).

**Q: Jak získám dočasnou licenci pro Aspose.HTML pro Java?**  
A: Pro získání dočasné licence navštivte [tuto stránku](https://purchase.aspose.com/temporary-license/).

**Q: Mohu získat podporu pro Aspose.HTML pro Java?**  
A: Ano, pomoc a podporu můžete získat v komunitě Aspose na [Aspose fóru](https://forum.aspose.com/).

**Q: Lze převést HTML na XPS na serveru bez grafického rozhraní?**  
A: Rozhodně. Aspose.HTML funguje v prostředích bez GUI; stačí mít správně nakonfigurovaný Java runtime.

**Q: Podporuje knihovna vlastní okraje stránky?**  
A: Ano. Použijte `PageSetup.setMarginTop()`, `setMarginBottom()` a podobně před přiřazením `PageSetup` k možnostem vykreslování.

## Závěr

Prošli jsme kompletním procesem **převodu HTML na XPS** a úpravy velikosti stránky pomocí Aspose.HTML pro Java. Dodržením těchto kroků můžete generovat tiskové XPS dokumenty, které přesně odpovídají vašim požadavkům na rozvržení. Nebojte se experimentovat s různými rozměry stránky, styly nebo dokonce přidávat záhlaví a zápatí podle potřeb vašeho projektu.

Pokud máte jakékoli otázky nebo potřebujete další pomoc, prozkoumejte [dokumentaci Aspose.HTML pro Java](https://reference.aspose.com/html/java/) nebo se zapojte do diskuze na [Aspose fóru](https://forum.aspose.com/).

---

**Poslední aktualizace:** 2025-11-29  
**Testováno s:** Aspose.HTML pro Java 24.11 (nejnovější v době psaní)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
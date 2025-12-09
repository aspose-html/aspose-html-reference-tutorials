---
date: 2025-12-05
description: Naučte se, jak nastavit okraje HTML stránky v Javě pomocí Aspose.HTML
  a přidat čísla stránek a nadpisy do svých dokumentů.
linktitle: CSS Extensions - Adding Title and Page Number
second_title: Java HTML Processing with Aspose.HTML
title: Jak nastavit okraje HTML stránky v Javě pomocí Aspose.HTML
url: /cs/java/advanced-usage/css-extensions-adding-title-page-number/
weight: 10
---

{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}
{{< blocks/products/pf/main-wrap-class >}}

# Jak nastavit okraje HTML stránky v Javě s Aspose.HTML

V tomto tutoriálu se dozvíte **jak nastavit okraje HTML stránky v Javě** pomocí Aspose.HTML pro Javu. Provedeme vás tvorbou vlastních okrajů stránky, vložením čísel stránek a přidáním názvu dokumentu – vše s jasným, krok‑za‑krokem kódem, který můžete zkopírovat do svého projektu.

## Rychlé odpovědi
- **Jaká knihovna je potřeba?** Aspose.HTML for Java  
- **Mohu ovládat okraje programově?** Ano, pomocí CSS `@page` v uživatelském stylovém listu  
- **Které výstupní formáty podporují okraje?** XPS, PDF a další rastrové formáty  
- **Potřebuji licenci pro produkční použití?** Platná licence Aspose.HTML je vyžadována pro ne‑zkušební použití  
- **Je to kompatibilní s Java 11+?** Naprosto – knihovna funguje s moderními verzemi Javy  

## Co znamená „nastavení okrajů HTML stránky v Javě“?
Nastavení okrajů HTML stránky v Javě znamená konfiguraci renderovacího enginu (poskytovaného Aspose.HTML) tak, aby aplikoval CSS vlastnosti stránkových boxů před tím, než je dokument převeden do tisknutelného formátu, jako je XPS nebo PDF. Definováním vlastního pravidla `@page` řídíte tiskovou oblast, čísla stránek a obsah hlavičky/patičky.

## Proč použít Aspose.HTML pro řízení okrajů?
- **Přesné rozvržení** – CSS `@page` poskytuje pixel‑dokonalou kontrolu nad okraji, hlavičkami a patičkami.  
- **Konzistence napříč formáty** – Stejné definice okrajů fungují pro XPS, PDF i výstupy obrázků.  
- **Žádná závislost na prohlížeči** – Renderování probíhá na serveru, takže nepotřebujete headless prohlížeč.  

## Předpoklady

Než začneme, ujistěte se, že máte následující předpoklady připravené:

1. **Java vývojové prostředí** – Nainstalovaný JDK 11 nebo novější.  
2. **Aspose.HTML for Java** – Stáhněte a nainstalujte knihovnu z [zde](https://releases.aspose.com/html/java/).  

## Import balíčků

Pro zahájení importujte potřebné třídy Aspose.HTML:

```java
// Import Aspose.HTML packages
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

## Jak nastavit okraje HTML stránky v Javě – krok‑za‑krokem průvodce

### Krok 1: Inicializace konfigurace a definice vlastních okrajů stránky

```java
// Initialize configuration object and set up the page-margins for the document
Configuration configuration = new Configuration();
try {
    // Get the User Agent service
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Set the style of custom margins and create marks on it
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

V tomto bloku vytvoříme objekt `Configuration`, získáme `IUserAgentService` a vložíme CSS pravidlo `@page`, které definuje okraje, čítač stránek vpravo dole a název dokumentu uprostřed nahoře.

### Krok 2: Vytvoření HTML dokumentu

```java
// Initialize an HTML document
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Zde vytvoříme `HTMLDocument` s jednoduchým úryvkem „Hello World“. Stejná konfigurace z Kroku 1 je použita, takže vlastní okraje jsou při renderování dokumentu respektovány.

### Krok 3: Renderování do XPS souboru (nebo jakéhokoli podporovaného výstupu)

```java
// Initialize an output device
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    // Send the document to the output device
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

Tento krok vytvoří `XpsDevice`, který zapisuje renderované stránky do `output.xps`. Okraje, čísla stránek a název, které jste definovali dříve, se objeví v konečném souboru.

## Časté problémy a tipy
- **Okraje se nezdají změněny** – Ujistěte se, že pravidlo `@page` není přepsáno jinými styly. Volání `setUserStyleSheet` jej vynutí s nejvyšší prioritou.  
- **Čísla stránek zobrazují „NaN“** – Ověřte, že používáte Aspose.HTML verze 23.10 nebo novější; starší verze postrádají funkci `currentPageNumber()`.  
- **Výstupní soubor je prázdný** – Zkontrolujte, že cesta `Resources.output` je správně vyřešena a máte oprávnění k zápisu.  

## Často kladené otázky

### Q1: Co je Aspose.HTML for Java?

**A:** Aspose.HTML for Java je knihovna pro Javu, která poskytuje výkonné nástroje pro práci s HTML dokumenty v Java aplikacích, včetně konverze, renderování a manipulace.

### Q2: Mohu dále přizpůsobit okraje stránky?

**A:** Ano, stačí upravit CSS uvnitř `setUserStyleSheet`. Můžete změnit libovolné hodnoty `margin-*` nebo přidat další boxy `@top-*` / `@bottom-*`.

### Q3: Jak mohu přidat více obsahu do HTML dokumentu?

**A:** Nahraďte řetězec v `new HTMLDocument("<div>Hello World!!!</div>", …)` vlastním HTML kódem, nebo načtěte externí soubor pomocí konstruktoru `HTMLDocument(String url, …)`.

### Q4: Je Aspose.HTML for Java kompatibilní s jinými formáty dokumentů?

**A:** Naprosto. Ten samý `HTMLDocument` lze renderovat do PDF, XPS, obrázků nebo dokonce EPUB výměnou výstupního zařízení (např. `PdfDevice`, `PngDevice`).

### Q5: Potřebuji licenci pro používání Aspose.HTML for Java?

**A:** Ano, licence je vyžadována pro produkční použití. Zkušební verzi nebo licenci můžete získat [zde](https://purchase.aspose.com/buy) nebo [zde](https://releases.aspose.com/).

### Q6: Jak nastavit různé okraje pro liché a sudé stránky?

**A:** Použijte pseudo‑třídy `@page :left` a `@page :right` ve vašem stylovém listu k definování odlišných okrajů pro levé (sudé) a pravé (liché) stránky.

### Q7: Mohu vložit vlastní fonty do renderovaného dokumentu?

**A:** Ano. Přidejte pravidla `@font-face` do uživatelského stylového listu a odkažte na fonty ve vašem HTML obsahu.

## Závěr

Nyní jste zvládli **jak nastavit okraje HTML stránky v Javě** pomocí Aspose.HTML a víte, jak přidat čísla stránek a název, aby vaše dokumenty vypadaly profesionálně. Nebojte se experimentovat s dalšími `@page` boxy, vlastními fonty nebo různými výstupními formáty podle potřeb vašeho projektu.

Pokud narazíte na problémy, oficiální [dokumentace Aspose.HTML for Java](https://reference.aspose.com/html/java/) a [fórum podpory Aspose](https://forum.aspose.com/) jsou výborná místa, kde získat pomoc.

{{< /blocks/products/pf/main-wrap-class >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/products-backtop-button >}}


---

**Poslední aktualizace:** 2025-12-05  
**Testováno s:** Aspose.HTML for Java 23.12  
**Autor:** Aspose  

---

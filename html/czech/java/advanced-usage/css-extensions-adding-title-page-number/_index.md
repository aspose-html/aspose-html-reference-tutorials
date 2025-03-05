---
title: Přizpůsobte okraje stránky HTML pomocí Aspose.HTML
linktitle: Rozšíření CSS - Přidání názvu a čísla stránky
second_title: Java HTML zpracování s Aspose.HTML
description: Naučte se, jak upravit okraje stránek, přidat čísla stránek a nadpisy do dokumentů HTML pomocí Aspose.HTML for Java.
type: docs
weight: 10
url: /cs/java/advanced-usage/css-extensions-adding-title-page-number/
---
Aspose.HTML for Java je výkonná knihovna pro zpracování dokumentů HTML v aplikacích Java. V tomto tutoriálu prozkoumáme, jak vytvořit vlastní okraje stránek a přidat čísla a názvy stránek do dokumentů HTML pomocí Aspose.HTML for Java. Tento podrobný průvodce rozdělí proces na zvládnutelné kroky, které vám pomohou snadno integrovat tyto funkce do vašich dokumentů HTML.

## Předpoklady

Než začneme, ujistěte se, že máte splněny následující předpoklady:

1. Vývojové prostředí Java: Ujistěte se, že máte na svém počítači nastavené vývojové prostředí Java.

2.  Aspose.HTML for Java: Stáhněte si a nainstalujte knihovnu Aspose.HTML for Java z[zde](https://releases.aspose.com/html/java/).

## Importujte balíčky

Chcete-li začít, musíte importovat potřebné balíčky z Aspose.HTML for Java. Přidejte do kódu Java následující příkazy pro import:

```java
// Importujte balíčky Aspose.HTML
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

Nyní si rozdělme proces přidávání vlastních okrajů stránek, čísel stránek a názvů do zvládnutelných kroků:

## Krok 1: Inicializujte konfiguraci a okraje stránky

```java
// Inicializujte konfigurační objekt a nastavte okraje stránky pro dokument
Configuration configuration = new Configuration();
try {
    // Získejte službu User Agent
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Nastavte styl vlastních okrajů a vytvořte na něm značky
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

V tomto kroku inicializujeme konfigurační objekt a nastavíme vlastní okraje stránky, včetně pozice počítadla stránky a názvu stránky.

## Krok 2: Inicializujte dokument HTML

```java
// Inicializujte dokument HTML
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Zde vytvoříme dokument HTML s ukázkovým obsahem (v tomto případě zpráva „Ahoj světe“) a použijeme konfiguraci z kroku 1.

## Krok 3: Inicializujte výstupní zařízení a vykreslete dokument

```java
// Inicializujte výstupní zařízení
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    //Odešlete dokument na výstupní zařízení
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

V tomto kroku nastavíme výstupní zařízení a vykreslíme HTML dokument. Dokument bude zpracován a uložen jako soubor XPS se zadanými okraji stránek, čísly stránek a názvem.

## Závěr

Gratuluji! Úspěšně jste se naučili, jak vytvářet vlastní okraje stránek a přidávat čísla a názvy stránek do dokumentů HTML pomocí Aspose.HTML for Java. Toto přizpůsobení vám umožní vytvářet profesionálnější a vizuálně přitažlivější dokumenty.

 Pokud máte nějaké dotazy nebo se potýkáte s nějakými problémy, neváhejte navštívit[Aspose.HTML pro dokumentaci Java](https://reference.aspose.com/html/java/) nebo vyhledejte pomoc na[Aspose fórum podpory](https://forum.aspose.com/).

## FAQ

### Q1: Co je Aspose.HTML pro Java?

Odpověď 1: Aspose.HTML for Java je knihovna Java, která poskytuje výkonné nástroje pro práci s dokumenty HTML v aplikacích Java.

### Q2: Mohu dále upravit okraje stránky?

Odpověď 2: Ano, styly CSS můžete upravit v kroku 1 a upravit tak okraje stránky podle svých požadavků.

### Q3: Jak mohu přidat další obsah do dokumentu HTML?

Odpověď 3: Obsah HTML v kroku 2 můžete upravit nahrazením ukázkového obsahu vlastním.

### Q4: Je Aspose.HTML for Java kompatibilní s jinými formáty dokumentů?

Odpověď 4: Ano, Aspose.HTML for Java lze použít k převodu dokumentů HTML do různých formátů, včetně PDF, XPS a obrázků.

### Q5: Potřebuji licenci pro používání Aspose.HTML pro Java?

 A5: Ano, můžete získat licenci nebo bezplatnou zkušební verzi[zde](https://purchase.aspose.com/buy) nebo[zde](https://releases.aspose.com/).
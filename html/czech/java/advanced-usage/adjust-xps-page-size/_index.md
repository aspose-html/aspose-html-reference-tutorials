---
title: Upravte velikost stránky XPS pomocí Aspose.HTML pro Java
linktitle: Úprava velikosti stránky XPS
second_title: Java HTML zpracování s Aspose.HTML
description: Naučte se, jak upravit velikost stránky XPS pomocí Aspose.HTML pro Java. Snadno ovládejte výstupní rozměry svých dokumentů XPS.
type: docs
weight: 16
url: /cs/java/advanced-usage/adjust-xps-page-size/
---

V tomto tutoriálu vás provedeme procesem úpravy velikosti stránky XPS pomocí Aspose.HTML for Java. Tato výkonná knihovna vám umožňuje manipulovat s dokumenty HTML a převádět je do různých formátů, včetně XPS. Úprava velikosti stránky je nezbytná, když potřebujete ovládat výstupní rozměry dokumentu XPS.

## Předpoklady

Než začneme, ujistěte se, že máte splněny následující předpoklady:

1. Java Development Environment: Ujistěte se, že máte v systému nainstalovanou sadu Java Development Kit (JDK).

2.  Knihovna Aspose.HTML for Java: Musíte si stáhnout a zahrnout knihovnu Aspose.HTML for Java do svého projektu Java. Knihovnu najdete[zde](https://releases.aspose.com/html/java/).

3. Vstupní soubor HTML: Připravte soubor HTML, který chcete vykreslit, a upravte velikost stránky XPS. Pro tento výukový program můžete použít svůj vlastní soubor HTML.

## Importujte balíčky

Nejprve musíte importovat potřebné balíčky pro práci s Aspose.HTML pro Java. Na začátek třídy Java zahrňte tyto balíčky:

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Krok 1: Nastavte název vstupního souboru

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

 V tomto kroku načteme váš vstupní soubor HTML pomocí a`FileInputStream`.

## Krok 2: Vytvořte dokument HTML a nastavte styly

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
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n";

// ...
```

 Tento krok zahrnuje vytvoření`HTMLDocument` a přidat k němu styly.

## Krok 3: Vytvořte možnosti vykreslování XPS

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

Zde vytváříme možnosti vykreslování XPS pro konfiguraci procesu vykreslování.

## Krok 4: Upravte velikost stránky

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

Tento krok zahrnuje nastavení velikosti stránky a určení, zda ji upravit na nejširší stránku.

## Krok 5: Vykreslení výstupu

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

V posledním kroku vykreslíme výstup XPS pomocí nakonfigurovaných možností.

## Závěr

tomto tutoriálu jsme vám ukázali, jak upravit velikost stránky XPS pomocí Aspose.HTML pro Java. Můžete ovládat výstupní rozměry svých dokumentů XPS a zajistit, aby splňovaly vaše specifické požadavky. Pomocí poskytnutého kódu a kroků můžete tuto funkci snadno implementovat do svých aplikací Java.

 Pokud máte nějaké dotazy nebo potřebujete další pomoc, neváhejte navštívit[Aspose.HTML pro dokumentaci Java](https://reference.aspose.com/html/java/) nebo požádat o pomoc na[Fórum Aspose](https://forum.aspose.com/).

## FAQ

### Q1: Co je Aspose.HTML pro Java?

Odpověď 1: Aspose.HTML for Java je knihovna Java, která umožňuje vývojářům manipulovat s dokumenty HTML a převádět je do různých formátů, jako jsou XPS, PDF a obrázky.

### Q2: Kde si mohu stáhnout Aspose.HTML pro Java?

 A2: Knihovnu Aspose.HTML for Java si můžete stáhnout z[tento odkaz](https://releases.aspose.com/html/java/).

### Q3: Je k dispozici bezplatná zkušební verze pro Aspose.HTML pro Java?

 A3: Ano, můžete získat bezplatnou zkušební verzi Aspose.HTML pro Java od[zde](https://releases.aspose.com/).

### Q4: Jak mohu získat dočasnou licenci pro Aspose.HTML pro Java?

 A4: Chcete-li získat dočasnou licenci pro Aspose.HTML pro Java, navštivte[tuto stránku](https://purchase.aspose.com/temporary-license/).

### Q5: Mohu získat podporu pro Aspose.HTML pro Java?

 A5: Ano, můžete vyhledat pomoc a podporu od komunity Aspose na[Fórum Aspose](https://forum.aspose.com/).
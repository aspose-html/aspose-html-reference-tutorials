---
title: Upravte velikost stránky PDF pomocí Aspose.HTML pro Java
linktitle: Úprava velikosti stránky PDF
second_title: Java HTML zpracování s Aspose.HTML
description: Naučte se, jak upravit velikost stránky PDF pomocí Aspose.HTML pro Java. Vytvářejte bez námahy vysoce kvalitní soubory PDF z HTML. Efektivně kontrolujte rozměry stránky.
type: docs
weight: 15
url: /cs/java/advanced-usage/adjust-pdf-page-size/
---

dnešní digitální době je potřeba generovat vysoce kvalitní soubory PDF z obsahu HTML na vzestupu. Aspose.HTML for Java je výkonná knihovna Java, která vám umožňuje bez námahy převádět dokumenty HTML do formátu PDF. V tomto tutoriálu se zaměříme na úpravu velikosti stránky při převodu HTML do PDF pomocí Aspose.HTML for Java.

## Předpoklady

Než začnete, ujistěte se, že máte splněny následující předpoklady:

- Java Development Environment: Ujistěte se, že máte v systému nainstalovanou sadu Java Development Kit (JDK).
-  Aspose.HTML for Java: Musíte si stáhnout a nainstalovat Aspose.HTML for Java z webu[zde](https://releases.aspose.com/html/java/).
- HTML dokument: Měli byste mít připravený HTML dokument ke konverzi. Pokud ne, vytvořte jej nebo použijte existující soubor HTML.

## Importujte balíčky

Chcete-li začít, musíte importovat potřebné balíčky pro práci s Aspose.HTML for Java. Následující fragment kódu ukazuje, jak to udělat:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

Nyní, když máte připravené předpoklady a importujete potřebné balíčky, rozdělíme proces úpravy velikosti stránky PDF do několika kroků:

## Krok 1: Čtení obsahu HTML

Nejprve si musíte přečíst obsah HTML, který chcete převést do PDF. V tomto příkladu budeme číst HTML ze souboru s názvem "FirstFile.html."

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## Krok 2: Psaní obsahu HTML

Dále zapíšete obsah HTML do souboru s názvem "FirstFileOut.html."

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Zde přidejte vlastní styly HTML nebo obsah
    String style = "<style>\n" +
                   ".st\n" +
                   "{\n" +
                   "color:\n" +
                   "green;\n" +
                   "}\n" +
                   "</style >\n" +
                   "<div id = id1 > Aspose.Html rendering Text in Black Color</div >\n" +
                   "<div id = id2 class='' st '' > Aspose.Html rendering Text in Green Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: blue;' > Aspose.Html rendering Text in Blue Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: red;' ><font face = 'Arial' > Aspose.Html rendering Text in Red\n" +
                   "Color</font ></div >\n";
    fileOutputStream.write(style.getBytes(java.nio.charset.StandardCharsets.UTF_8));
}
```

## Krok 3: Vykreslení HTML do PDF

Nyní vykreslíte obsah HTML do souboru PDF. Pokryjeme dva scénáře: jeden, kdy velikost stránky není přizpůsobena šířce obsahu, a druhý, kde je přizpůsobena.

### Velikost stránky neupravena

V tomto scénáři je velikost stránky nastavena na pevnou šířku a výšku, což může oříznout obsah, pokud překročí tyto rozměry.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Vytvořte instanci HTMLDocument ze souboru HTML
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Nastavte možnosti vykreslování PDF
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Vykreslete výstup
pdf_renderer.render(device, html_document);
```

### Velikost stránky přizpůsobena šířce obsahu

V tomto scénáři je velikost stránky upravena podle šířky obsahu.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Vykreslete výstup
pdf_renderer.render(device, html_document);
```

## Závěr

V tomto tutoriálu jsme prozkoumali, jak upravit velikost stránky PDF při převodu HTML do PDF pomocí Aspose.HTML for Java. Naučili jste se předpoklady, importovali jste požadované balíčky a postupovali jste podle podrobného průvodce k dosažení tohoto úkolu. S Aspose.HTML for Java můžete snadno ovládat velikost stránky generovaných PDF a zajistit, že se váš obsah zobrazí tak, jak bylo zamýšleno.

 Nebojte se experimentovat s různými velikostmi stránek a nastaveními, abyste splnili své specifické požadavky. Pokud narazíte na nějaké problémy nebo máte další otázky, neváhejte požádat o pomoc[Aspose.HTML pro dokumentaci Java](https://reference.aspose.com/html/java/) nebo[Aspose fórum podpory](https://forum.aspose.com/).

## FAQ

### Q1: Co je Aspose.HTML pro Java?

Odpověď 1: Aspose.HTML for Java je knihovna Java, která umožňuje pracovat s dokumenty HTML, manipulovat s nimi, převádět je a vykreslovat je do různých formátů, včetně PDF.

### Otázka 2: Jak mohu upravit velikost stránky PDF při převodu HTML do PDF pomocí Aspose.HTML for Java?

 A2: Velikost stránky PDF můžete upravit pomocí`PageSetup` třídy a nastavení`AdjustToWidestPage` majetek do`true` nebo `false, v závislosti na vašich požadavcích.

### Otázka 3: Mohu upravit styl obsahu HTML před jeho převedením do PDF?

Odpověď 3: Ano, styl můžete přizpůsobit přidáním prvků CSS a HTML do obsahu HTML před jeho převedením do PDF, jak je ukázáno ve výukovém programu.

### Q4: Kde najdu dokumentaci k Aspose.HTML pro Java?

 A4: Můžete nahlédnout do dokumentace[zde](https://reference.aspose.com/html/java/) pro vyčerpávající informace a příklady.

### Q5: Je k dispozici bezplatná zkušební verze pro Aspose.HTML pro Java?

 A5: Ano, máte přístup k bezplatné zkušební verzi Aspose.HTML pro Java z[tento odkaz](https://releases.aspose.com/).
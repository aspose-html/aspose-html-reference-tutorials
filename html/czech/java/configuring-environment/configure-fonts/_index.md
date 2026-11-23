---
date: 2026-04-05
description: Naučte se generovat PDF z HTML, konfigurovat písma, použít vlastní CSS,
  využít dočasnou licenci a převádět HTML do PDF v Javě s Aspose.HTML.
keywords:
- generate pdf from html
- convert html pdf java
- add custom fonts pdf
- fonts not showing pdf
linktitle: Konfigurace fontů v Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: 'Generovat PDF z HTML: Konfigurace fontů s Aspose.HTML pro Javu'
url: /cs/java/configuring-environment/configure-fonts/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nastavení fontů pro HTML‑to‑PDF v Javě s Aspose.HTML

## Úvod
V tomto tutoriálu se dozvíte, jak **generovat PDF z HTML** pomocí Aspose.HTML a nakonfigurovat fonty pro konverzi HTML‑to‑PDF v Javě. Při práci s HTML dokumenty zajišťuje nastavení správných fontů, že vygenerované PDF vypadá přesně jako původní webová stránka — zachovává barvy značky, typografii a rozvržení. Ať už vytváříte zprávy, faktury nebo jakýkoli proces generování dokumentů, správná konfigurace fontů je klíčem k profesionálně vypadajícím PDF. Projdeme celý proces, od přípravy prostředí až po konverzi HTML do PDF s vlastními fonty a CSS.

## Rychlé odpovědi
- **Jaký je hlavní cíl tohoto tutoriálu?** Nakonfigurovat fonty pro konverzi HTML‑to‑PDF v Javě pomocí Aspose.HTML.  
- **Která knihovna provádí konverzi?** Aspose.HTML pro Java (třída `Converter`).  
- **Potřebuji licenci?** Dočasná licence Aspose odstraňuje omezení hodnocení; pro produkci je vyžadována plná licence.  
- **Kam umístit vlastní fonty?** Do složky uvedené v `FontsLookupFolder`, např. adresář `fonts` vedle vašeho projektu.  
- **Mohu přizpůsobit výstup PDF?** Ano — použijte `PdfSaveOptions` k úpravě velikosti stránky, okrajů a dalších nastavení.

## Co je **generate PDF from HTML** a proč je konfigurace fontů důležitá?
Proces **generate PDF from HTML** vykresluje HTML dokument do PDF stránky. Fonty jsou klíčovou součástí vykreslování, protože ovlivňují rozvržení, řádkování a vizuální věrnost. Nastavením Aspose.HTML na vlastní složku s fonty zajistíte, že PDF použije přesně ty typy písma, které jste navrhli pro webovou stránku, čímž eliminujete náhradní fonty a zachováte konzistenci značky.

## Proč použít Aspose.HTML pro konfiguraci fontů?
- **Přesné vykreslování:** Podporuje CSS2.1 a mnoho funkcí CSS3, takže vaše HTML vypadá v PDF stejně.  
- **Cross‑platform:** Funguje na jakémkoli OS, který podporuje Java 1.8+.  
- **Flexibilita licence:** Testujte s dočasnou licencí a poté přejděte na plnou licenci pro produkci.  
- **Výkon:** Rychlá konverze i pro složité stránky.

## Předpoklady
1. **Java Development Kit (JDK) 1.8+** – kód běží na jakémkoli moderním JDK.  
2. **Aspose.HTML pro Java** – stáhněte nejnovější JAR z [Aspose website](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse nebo jakýkoli editor kompatibilní s Javou.  
4. **Základní znalost Javy** – měli byste být obeznámeni s třídami, metodami a souborovým I/O.  
5. **Licence Aspose.HTML** – [dočasná licence](https://purchase.aspose.com/temporary-license/) odstraní omezení hodnocení.

## Import Packages
First, import the core Java and Aspose.HTML classes you’ll need.  

```java
import java.io.IOException;
```

These imports give you access to file handling and the Aspose.HTML API.

## Jak přidat vlastní fonty při generování PDF
Below we’ll explain why font handling matters, how to apply custom CSS, and how to **use a temporary license** to unlock full functionality while you test the solution.

## Průvodce krok za krokem

### Krok 1: Vytvořte HTML obsah
We’ll start by generating a simple HTML file that we’ll later convert to PDF.

#### 1.1 Napište HTML kód
```java
String code = "<h1>FontsSettings property</h1>\r\n" +
    "<p>The FontsSettings property is used for configuration of fonts handling.</p>\r\n";
```

This snippet defines a header and a paragraph. Feel free to expand the HTML with more elements if you need to test additional styles.

#### 1.2 Uložte HTML do souboru
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("user-agent-fontsetting.html")) {
    fileWriter.write(code);
}
```

The `FileWriter` writes the string to `user-agent-fontsetting.html` in your project folder. After this step you’ll have a physical HTML file ready for processing.

### Krok 2: Nakonfigurujte prostředí Aspose.HTML
Now we’ll set up the Aspose.HTML `Configuration` object, which lets us control how the HTML is rendered.

#### 2.1 Vytvořte instanci Configuration
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

The `Configuration` object is the entry point for customizing rendering options such as font handling and user‑agent behavior.

#### 2.2 Přístup k User Agent Service
```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

The `IUserAgentService` manages style sheets, fonts, and other rendering details. We’ll use it to inject custom CSS and point to our font folder.

### Krok 3: Použijte vlastní styly a fonty
With the environment ready, we can now add CSS rules and tell Aspose.HTML where to find our fonts.

#### 3.1 Nastavte vlastní CSS
```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; }\r\n" +
    "p { color:grey; }\r\n");
```

This CSS colors the header brown and the paragraph grey. You can add any valid CSS rules here—Aspose.HTML supports the full CSS2.1 spec and many CSS3 features. *(This is an example of **apply custom css**.)*

#### 3.2 Odkaz na složku s vlastními fonty
```java
userAgent.getFontsSettings().setFontsLookupFolder("fonts");
```

Place any `.ttf` or `.otf` files you want to use inside a folder named `fonts` located at the root of your project. Aspose.HTML will automatically load these fonts during rendering.

> **Tip:** Pokud máte více rodin fontů, uspořádejte je do podsložek a přidejte každou nadřazenou složku do `FontsLookupFolder` pomocí seznamu odděleného středníkem.

### Krok 4: Načtěte HTML dokument s konfigurací
Now we load the HTML file we created earlier, applying the custom configuration we just built.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("user-agent-fontsetting.html", configuration);
```

The `HTMLDocument` object now represents the styled HTML ready for conversion.

### Krok 5: Převést HTML do PDF
Finally, we perform the **aspose html pdf conversion** to produce a PDF file that respects our custom fonts and styles.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.PdfSaveOptions(),
    "user-agent-fontsetting_out.pdf"
);
```

The `PdfSaveOptions` object lets you tweak output settings such as page size, compression, and metadata. For a basic conversion, the default options work perfectly.

### Krok 6: Vyčistěte zdroje
Proper disposal prevents memory leaks, especially when processing many documents in a long‑running application.

#### 6.1 Uvolněte HTMLDocument
```java
if (document != null) {
    document.dispose();
}
```

#### 6.2 Uvolněte Configuration
```java
if (configuration != null) {
    configuration.dispose();
}
```

These calls free native resources allocated by Aspose.HTML.

## Časté problémy a řešení
| Problém | Řešení |
|-------|----------|
| **Fonty se nezobrazují** | Ověřte, že složka `fonts` je správně odkazována a obsahuje platné soubory `.ttf`/`.otf`. Použijte absolutní cesty, pokud je složka mimo adresář projektu. |
| **PDF je prázdný** | Ujistěte se, že cesta k HTML souboru je správná a soubor je čitelný. Zkontrolujte, že objekt `Configuration` je předán konstruktoru `HTMLDocument`. |
| **Výjimka licence** | Použijte dočasnou nebo plnou licenci Aspose před voláním jakýchkoli Aspose API. Umístěte soubor licence do classpath a načtěte jej pomocí `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`. |
| **Neočekávané vykreslení CSS** | Aspose.HTML podporuje většinu CSS, ale ne všechny moderní funkce (např. CSS Grid). Zjednodušte styly nebo použijte podporované CSS vlastnosti. |

## Často kladené otázky

**Q: Can I use any font with Aspose.HTML for Java?**  
A: Yes, any TrueType (`.ttf`) or OpenType (`.otf`) font that your operating system supports can be used. Just place the files in the folder you set with `FontsLookupFolder`.

**Q: Do I need a license to use Aspose.HTML for Java?**  
A: While you can evaluate the library without a license, a [temporary Aspose license](https://purchase.aspose.com/temporary-license/) removes evaluation limits. For production, a full license is required.

**Q: How can I customize the PDF output?**  
A: Pass a configured `PdfSaveOptions` instance to `convertHTML`. You can set page size, margins, compression level, and more.

**Q: Is it possible to apply more complex CSS styles?**  
A: Yes, Aspose.HTML supports a wide range of CSS. Complex selectors, media queries, and pseudo‑classes work as they would in a browser, though some very new CSS3/4 features may not be fully supported.

**Q: Where can I find more examples and documentation?**  
A: Visit the official [Aspose.HTML for Java documentation page](https://reference.aspose.com/html/java/) for detailed API references and additional code samples.

**Q: How does the temporary Aspose license affect conversion?**  
A: The temporary license lifts the 10‑page limit and watermark that appear in evaluation mode, allowing you to fully test the **aspose html pdf conversion** workflow.

**Poslední aktualizace:** 2026-04-05  
**Testováno s:** Aspose.HTML pro Java 24.12 (nejnovější v době psaní)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
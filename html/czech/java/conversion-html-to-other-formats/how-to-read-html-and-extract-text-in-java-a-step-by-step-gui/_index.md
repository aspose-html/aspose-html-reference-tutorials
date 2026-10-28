---
category: general
date: 2026-10-28
description: Jak číst HTML v Javě a extrahovat text z HTML souborů. Naučte se převádět
  HTML na text pomocí Jsoup, zahrnující čtení HTML ze souboru a techniky převodu HTML
  na text v Javě.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to read html
- extract text from html
- convert html to text
- html to text java
- read html from file
language: cs
lastmod: 2026-10-28
og_description: Jak číst HTML v Javě a extrahovat text z HTML souborů. Tento tutoriál
  ukazuje kompletní řešení pro převod HTML na text pomocí Jsoup.
og_image_alt: Diagram showing how to read HTML and extract text in Java
og_title: Jak číst HTML a extrahovat text v Javě – rychlý průvodce
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  headline: How to read HTML and extract text in Java – a step‑by‑step guide
  type: TechArticle
- description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  name: How to read HTML and extract text in Java – a step‑by‑step guide
  steps:
  - name: Maven
    text: '```xml <dependency> <groupId>org.jsoup</groupId> <artifactId>jsoup</artifactId>
      <version>1.17.2</version> </dependency> ```'
  - name: Gradle
    text: '```gradle implementation ''org.jsoup:jsoup:1.17.2'' ```'
  - name: Expected output
    text: 'Assuming `input.html` contains:'
  - name: Running the program
    text: '```bash javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java java -cp .:jsoup-1.17.2.jar
      HtmlToTextDemo ```'
  type: HowTo
tags:
- Java
- HTML parsing
- Text extraction
title: Jak číst HTML a extrahovat text v Javě – průvodce krok po kroku
url: /cs/java/conversion-html-to-other-formats/how-to-read-html-and-extract-text-in-java-a-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak číst HTML a extrahovat text v Javě – krok za krokem průvodce

Pokud potřebujete **jak číst html** z lokálního souboru, tento průvodce poskytuje kompletní řešení. Naučíte se načíst HTML dokument, extrahovat čistý text a volitelně převést HTML na text s jemnou kontrolou. Na konci tutoriálu můžete spustit ukázkový kód a vidět extrahovaný text vytištěný v konzoli.

Čtení HTML souborů je běžný úkol při zpracování web‑scrapovaných dat, generování reportů nebo čištění uživatelského obsahu. Níže uvedené kroky pokrývají vše, co potřebujete, od přidání požadované knihovny až po řešení okrajových případů, jako jsou poškozené značky nebo problémy s kódováním znaků.

## Co budete potřebovat

- Java 17 nebo novější (kód se také kompiluje s dřívějšími verzemi)
- Maven nebo Gradle pro správu závislostí, nebo Jsoup JAR přidán ručně
- HTML soubor pojmenovaný `input.html` umístěný v adresáři projektu `src/main/resources` (cestu můžete později změnit)

## Nastavení knihovny Jsoup

Jsoup je lehká, dobře zdokumentovaná knihovna, která parsuje HTML do struktury podobné DOM. Gracefully zvládá poškozené HTML, což ji činí ideální pro úkoly **extrahování textu z html**.

### Maven

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

### Gradle

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

Pokud dáváte přednost ručnímu stažení, umístěte JAR do classpath a importujte `org.jsoup.*` ve svém zdrojovém souboru.

## Načtení HTML ze souboru

Prvním programovým krokem je načíst soubor do objektu `Document`. Jsoup nabízí statickou metodu `parse`, která přijímá `File` a název znakové sady.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Path to the HTML file – adjust if your file lives elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Parse the file using UTF‑8 encoding
            Document doc = Jsoup.parse(input, "UTF-8");
            // Continue with text extraction…
        } catch (IOException e) {
            System.err.println("Failed to read the HTML file: " + e.getMessage());
        }
    }
}
```

**Proč je to důležité:** `Jsoup.parse(File, String)` čte surové bajty, dekóduje je podle zadané znakové sady a vytvoří čistý DOM. Tento přístup je bezpečnější než číst soubor do řetězce sami, protože Jsoup normalizuje konce řádků a automaticky opravuje běžné chyby značkování.

## Extrahování čistého textu z HTML

Jakmile máte `Document`, získání viditelného textu je jediným voláním metody. Metoda `text()` spojí textový obsah všech elementů a odstraňuje značky, skripty a styly.

```java
// Inside the try block from the previous snippet
String plainText = doc.body().text();
System.out.println("Extracted text:");
System.out.println(plainText);
```

Volání `body()` omezuje extrakci na element `<body>`, což je typický cíl, když **čtete html ze souboru** pro analýzu obsahu. Výsledný řetězec obsahuje mezery zredukované na jediné mezery, napodobujíc, jak by text vykreslil prohlížeč.

### Očekávaný výstup

Předpokládejme, že `input.html` obsahuje:

```html
<!DOCTYPE html>
<html>
<head><title>Sample</title></head>
<body>
  <h1>Hello World</h1>
  <p>This is a <strong>demo</strong> page.</p>
</body>
</html>
```

Spuštění programu vypíše:

```
Extracted text:
Hello World This is a demo page.
```

## Převod HTML na text s dalšími možnostmi

Někdy potřebujete větší kontrolu než poskytuje `text()` – např. zachování zalomení řádků, udržení číslování seznamů nebo ignorování určitých značek. `NodeTraversor` z Jsoup v kombinaci s vlastním `NodeVisitor` vám poskytuje tuto flexibilitu.

```java
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

public class HtmlToTextDemo {

    // ... (main method unchanged)

    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();
        NodeVisitor visitor = new NodeVisitor() {
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Preserve line breaks for block elements
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }
            public void tail(Node node, int depth) {
                // No action needed on exit
            }
        };
        NodeTraversor.traverse(visitor, doc.body());
        // Collapse multiple newlines into a single one
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

Nahraďte jednoduché volání `doc.body().text()` tímto:

```java
String detailedText = convertHtmlToText(doc);
System.out.println("Detailed conversion:");
System.out.println(detailedText);
```

**Proč to funguje:** Návštěvník prochází DOM do hloubky, přidává nový řádek před každý blok‑úrovňový element (např. `<p>`, `<div>`, `<h1>`). To zachovává oddělení odstavců, což je užitečné, když **převádíte html na text** pro čitelnost nebo následné NLP pipeline.

## Časté úskalí a osvědčené postupy

| Problém | Proč k tomu dochází | Doporučené řešení |
|-------|---------------|-----------------|
| Nesprávná znaková sada | Soubory uložené v ISO‑8859‑1, ale parsované jako UTF‑8, způsobují poškozené znaky. | Detekujte znakovou sadu z meta tagu souboru (`<meta charset="...">`) nebo předávejte správný název do `Jsoup.parse`. |
| Velké soubory | Načtení velmi velkého HTML souboru do paměti může způsobit `OutOfMemoryError`. | Streamujte soubor pomocí `Jsoup.parse(File, String, String baseUri)` a zpracovávejte uzly postupně, nebo zvětšete velikost haldy JVM. |
| Nechtěný text ze skriptů/stylů | `text()` odstraňuje obsah skriptů a stylů, ale vlastní návštěvníci jej mohou neúmyslně zahrnout. | Přeskakujte uzly, jejichž název značky je `script` nebo `style`, ve `head` metodě návštěvníka. |
| Zachování bílých znaků | Slučování mezer může ztratit formátování potřebné pro konverzi do markdownu. | Použijte `Element.wholeText()` pro surové textové uzly a poté bílý prostor zpracujte ručně. |

Řešením těchto problémů zajistíte, že vaše **html to text java** řešení bude spolehlivě fungovat s různorodými vstupy.

## Kompletní spustitelný příklad

Níže je samostatný program, který demonstruje celý workflow – od nastavení závislostí po ověření výstupu. Zkopírujte kód do souboru pojmenovaného `HtmlToTextDemo.java`, umístěte soubor `input.html` vedle něj a spusťte `javac && java` podle ukázky.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Adjust the path if your HTML file is located elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Load and parse the HTML file using UTF‑8
            Document doc = Jsoup.parse(input, "UTF-8");

            // Simple extraction – suitable for most cases
            String plain = doc.body().text();
            System.out.println("=== Simple extraction ===");
            System.out.println(plain);
            System.out.println();

            // Detailed conversion – keeps line breaks for readability
            String detailed = convertHtmlToText(doc);
            System.out.println("=== Detailed conversion ===");
            System.out.println(detailed);
        } catch (IOException e) {
            System.err.println("Error reading HTML file: " + e.getMessage());
        }
    }

    /**
     * Walks the DOM and builds a text representation that preserves
     * line breaks for block‑level elements.
     *
     * @param doc the parsed HTML document
     * @return a readable plain‑text version of the HTML body
     */
    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();

        NodeVisitor visitor = new NodeVisitor() {
            @Override
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Add a newline before block elements (e.g., <p>, <div>, <h1>)
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }

            @Override
            public void tail(Node node, int depth) {
                // No operation needed when exiting a node
            }
        };

        NodeTraversor.traverse(visitor, doc.body());

        // Collapse consecutive newlines and trim leading/trailing whitespace
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

### Spuštění programu

```bash
javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java
java -cp .:jsoup-1.17.2.jar HtmlToTextDemo
```

Konzole zobrazí jak jednoduchou extrakci, tak podrobnou


## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s krok‑za‑krokem vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich vlastních projektech.

- [Jak použít XPath v Javě – Číst HTML a extrahovat text](/html/english/java/creating-managing-html-documents/how-to-use-xpath-in-java-read-html-and-extract-text/)
- [Jak parsovat HTML v Javě – Extrahovat text z HTML článků](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Extrahovat text z HTML pomocí Javy – Kompletní krok‑za‑krokem průvodce](/html/english/java/creating-managing-html-documents/extract-text-from-html-with-java-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
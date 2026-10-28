---
category: general
date: 2026-10-28
description: Hogyan olvassuk be a HTML-t Java-ban, és nyerjünk ki szöveget HTML-fájlokból.
  Tanulja meg, hogyan konvertáljon HTML-t szöveggé a Jsoup segítségével, bemutatva
  a HTML fájlból való olvasást és a HTML‑szöveg Java technikákat.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to read html
- extract text from html
- convert html to text
- html to text java
- read html from file
language: hu
lastmod: 2026-10-28
og_description: Hogyan olvassunk HTML-t Java-ban és nyerjünk ki szöveget HTML-fájlokból.
  Ez az útmutató egy teljes megoldást mutat be az HTML szöveggé konvertálására a Jsoup
  használatával.
og_image_alt: Diagram showing how to read HTML and extract text in Java
og_title: HTML olvasása és szöveg kinyerése Java-ban – gyors útmutató
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
title: HTML beolvasása és szöveg kinyerése Java-ban – lépésről lépésre útmutató
url: /hu/java/conversion-html-to-other-formats/how-to-read-html-and-extract-text-in-java-a-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan olvassunk HTML-t és nyerjünk ki szöveget Java‑ban – lépésről‑lépésre útmutató

Ha **how to read html**‑ra van szükséged egy helyi fájlból, ez az útmutató teljes megoldást nyújt. Megtanulod, hogyan tölts be egy HTML dokumentumot, nyerd ki a sima szöveget, és opcionálisan konvertáld a HTML‑t szöveggé finomhangolt vezérléssel. A tutorial végére futtathatod a példakódot, és láthatod a kinyert szöveget a konzolon.

A HTML‑fájlok olvasása gyakori feladat web‑kaparásból származó adatok feldolgozásakor, jelentések készítésekor vagy felhasználók által generált tartalom tisztításakor. Az alábbi lépések mindent lefednek, amire szükséged lehet, a szükséges könyvtár hozzáadásától a hibás markup vagy karakterkódolási problémák kezeléséig.

## Amire szükséged lesz

- Java 17 vagy újabb (a kód korábbi verziókkal is lefordítható)
- Maven vagy Gradle a függőségkezeléshez, vagy a Jsoup JAR manuális hozzáadása
- Egy `input.html` nevű HTML‑fájl, amely a projekt `src/main/resources` könyvtárában helyezkedik el (a későbbiekben módosíthatod az útvonalat)

## Állítsd be a Jsoup könyvtárat

A Jsoup egy könnyű, jól dokumentált könyvtár, amely a HTML‑t DOM‑szerű struktúrába parse‑olja. Hibás HTML‑t is elegánsan kezel, ami ideálissá teszi a **extract text from html** feladatokhoz.

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

Ha inkább manuális letöltést részesítesz előnyben, helyezd a JAR‑t az osztályútvonalra, és importáld a `org.jsoup.*`‑t a forrásfájlodba.

## HTML betöltése fájlból

Az első programozási lépés a fájl beolvasása egy `Document` objektumba. A Jsoup egy statikus `parse` metódust kínál, amely egy `File`‑t és egy karakterkódolás nevét fogadja.

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

**Miért fontos:** A `Jsoup.parse(File, String)` a nyers bájtokat olvassa be, a megadott karakterkódolás szerint dekódolja, és tiszta DOM‑ot épít. Ez a megközelítés biztonságosabb, mint a fájl saját kezű string‑be olvasása, mivel a Jsoup normalizálja a sorvégeket és automatikusan javítja a gyakori markup hibákat.

## Sima szöveg kinyerése a HTML‑ből

Miután rendelkezel egy `Document`‑ummal, a látható szöveg lekérése egyetlen metódushívás. A `text()` metódus összefűzi az összes elem szöveges tartalmát, miközben eldobja a tageket, szkripteket és stílusokat.

```java
// Inside the try block from the previous snippet
String plainText = doc.body().text();
System.out.println("Extracted text:");
System.out.println(plainText);
```

A `body()` hívás a kinyerést a `<body>` elemre korlátozza, ami a tipikus cél, amikor **read html from file**‑t végzel tartalomelemzéshez. Az eredményül kapott stringben a szóközök egyetlen szóközre csökkennek, utánozva, ahogyan egy böngésző megjelenítené a szöveget.

### Várható kimenet

Tegyük fel, hogy az `input.html` a következőt tartalmazza:

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

A program futtatása a következőt írja ki:

```
Extracted text:
Hello World This is a demo page.
```

## HTML konvertálása szöveggé további beállításokkal

Néha több vezérlésre van szükség, mint amit a `text()` biztosít – például sortörések megőrzése, listaszámozás megtartása vagy bizonyos tagek figyelmen kívül hagyása. A Jsoup `NodeTraversor`‑ja egy egyedi `NodeVisitor`‑rel együtt ezt a rugalmasságot adja.

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

Cseréld le az egyszerű `doc.body().text()` hívást a következőre:

```java
String detailedText = convertHtmlToText(doc);
System.out.println("Detailed conversion:");
System.out.println(detailedText);
```

**Miért működik:** A látogató mélységi bejárással járja be a DOM‑ot, minden blokk‑szintű elem (pl. `<p>`, `<div>`, `<h1>`) előtt új sort fűz hozzá. Ez megőrzi a bekezdések elválasztását, ami hasznos, amikor **convert html to text**‑t végzel olvashatóság vagy downstream NLP pipeline‑ok miatt.

## Gyakori buktatók és legjobb gyakorlatok

| Probléma | Miért fordul elő | Ajánlott megoldás |
|----------|------------------|-------------------|
| Rossz karakterkódolás | A fájlok ISO‑8859‑1‑ben vannak mentve, de UTF‑8‑ként kerülnek parse‑olásra, ami torz karaktereket eredményez. | Detektáld a karakterkódolást a fájl meta‑tagjéből (`<meta charset="...">`), vagy add meg a helyes nevet a `Jsoup.parse`‑nek. |
| Nagy fájlok | Nagyon nagy HTML‑fájl memóriába töltése `OutOfMemoryError`‑t okozhat. | Streameld a fájlt a `Jsoup.parse(File, String, String baseUri)`‑val, és dolgozd fel a node‑okat fokozatosan, vagy növeld a JVM heap méretét. |
| Nem kívánt script/style szöveg | A `text()` eltávolítja a script és style tartalmat, de egyedi látogatók véletlenül belefoglalhatják. | Hagyj ki minden `script` vagy `style` nevű node‑t a látogató `head` metódusában. |
| Szóközök megőrzése | A szóközök összeolvadása elveszítheti a markdown konverzióhoz szükséges formázást. | Használd az `Element.wholeText()`‑t a nyers szövegnode‑okhoz, majd manuálisan post‑processzáld a szóközöket. |

Ezeknek a kérdéseknek a kezelése biztosítja, hogy a **html to text java** megoldásod megbízhatóan működjön különféle bemenetek esetén.

## Teljes futtatható példa

Az alábbi önálló program bemutatja a teljes munkafolyamatot – a függőség beállításától a kimenet ellenőrzéséig. Másold a kódot egy `HtmlToTextDemo.java` nevű fájlba, helyezz egy `input.html` fájlt mellé, és futtasd a `javac && java` parancsot a példában.

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

### A program futtatása

```bash
javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java
java -cp .:jsoup-1.17.2.jar HtmlToTextDemo
```

A konzol megjeleníti az egyszerű kinyerést és a részleteset.

## Mit érdemes még megtanulni?

A következő tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív implementációs megközelítéseket a saját projektjeidben.

- [How to Use XPath in Java – Read HTML and Extract Text](/html/english/java/creating-managing-html-documents/how-to-use-xpath-in-java-read-html-and-extract-text/)
- [How to Parse HTML in Java – Extract Text from HTML Articles](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Extract text from HTML with Java – Complete Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/extract-text-from-html-with-java-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
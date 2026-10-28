---
category: general
date: 2026-10-28
description: Hur man läser HTML i Java och extraherar text från HTML‑filer. Lär dig
  konvertera HTML till text med Jsoup, inklusive att läsa HTML från fil och HTML‑till‑text‑tekniker
  i Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to read html
- extract text from html
- convert html to text
- html to text java
- read html from file
language: sv
lastmod: 2026-10-28
og_description: Hur man läser HTML i Java och extraherar text från HTML‑filer. Denna
  handledning visar en komplett lösning för att konvertera HTML till text med Jsoup.
og_image_alt: Diagram showing how to read HTML and extract text in Java
og_title: Hur man läser HTML och extraherar text i Java – snabbguide
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
title: Hur man läser HTML och extraherar text i Java – en steg‑för‑steg‑guide
url: /sv/java/conversion-html-to-other-formats/how-to-read-html-and-extract-text-in-java-a-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så läser du HTML och extraherar text i Java – en steg‑för‑steg‑guide

Om du behöver **hur man läser html** från en lokal fil, ger den här guiden en komplett lösning. Du kommer att lära dig att ladda ett HTML‑dokument, extrahera ren text och eventuellt konvertera HTML till text med fin‑granulär kontroll. I slutet av handledningen kan du köra exempel­koden och se den extraherade texten skrivas ut i konsolen.

Att läsa HTML‑filer är en vanlig uppgift när man bearbetar webbscrapad data, genererar rapporter eller rensar användargenererat innehåll. Stegen nedan täcker allt du behöver, från att lägga till det nödvändiga biblioteket till att hantera kantfall som felaktig markup eller teckenkodningsproblem.

## Vad du behöver

- Java 17 eller nyare (koden kompileras även med tidigare versioner)
- Maven eller Gradle för beroendehantering, eller Jsoup‑JAR‑filen tillagd manuellt
- En HTML‑fil med namnet `input.html` placerad i projektets `src/main/resources`‑katalog (du kan ändra sökvägen senare)

## Ställ in Jsoup‑biblioteket

Jsoup är ett lättviktigt, väl‑dokumenterat bibliotek som parsar HTML till en DOM‑liknande struktur. Det hanterar bruten HTML på ett smidigt sätt, vilket gör det idealiskt för **extrahera text från html**‑uppgifter.

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

Om du föredrar en manuell nedladdning, placera JAR‑filen på din klassväg och importera `org.jsoup.*` i din källkod.

## Läs HTML från en fil

Det första programatiska steget är att läsa in filen i ett `Document`‑objekt. Jsoup erbjuder en statisk `parse`‑metod som accepterar en `File` och ett teckenkodningsnamn.

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

**Varför detta är viktigt:** `Jsoup.parse(File, String)` läser de råa bytena, avkodar dem enligt den angivna teckenkodningen och bygger ett rent DOM. Detta tillvägagångssätt är säkrare än att läsa in filen till en sträng själv eftersom Jsoup normaliserar radslut och automatiskt rättar vanliga markup‑fel.

## Extrahera ren text från HTML

När du har ett `Document` är hämtning av den synliga texten ett enda metodanrop. `text()`‑metoden sammanfogar det textuella innehållet i alla element samtidigt som den ignorerar taggar, skript och stilar.

```java
// Inside the try block from the previous snippet
String plainText = doc.body().text();
System.out.println("Extracted text:");
System.out.println(plainText);
```

`body()`‑anropet begränsar extraktionen till `<body>`‑elementet, vilket är det typiska målet när du **läser html från fil** för innehållsanalys. Den resulterande strängen har blanksteg kollapsade till enkla mellanslag, vilket efterliknar hur en webbläsare skulle rendera texten.

### Förväntad output

Antag att `input.html` innehåller:

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

Att köra programmet skriver ut:

```
Extracted text:
Hello World This is a demo page.
```

## Konvertera HTML till text med ytterligare alternativ

Ibland behöver du mer kontroll än vad `text()` erbjuder—t.ex. bevara radbrytningar, behålla listnumrering eller ignorera vissa taggar. Jsoup:s `NodeTraversor` kombinerat med en anpassad `NodeVisitor` ger dig den flexibiliteten.

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

Ersätt det enkla `doc.body().text()`‑anropet med:

```java
String detailedText = convertHtmlToText(doc);
System.out.println("Detailed conversion:");
System.out.println(detailedText);
```

**Varför detta fungerar:** Besökaren traverserar DOM‑trädet djup‑först och lägger till en ny rad före varje block‑nivå‑element (t.ex. `<p>`, `<div>`, `<h1>`). Detta behåller avsnittsskiljning, vilket är användbart när du **konverterar html till text** för läsbarhet eller efterföljande NLP‑pipelines.

## Vanliga fallgropar och bästa praxis

| Problem | Varför det uppstår | Rekommenderad åtgärd |
|-------|---------------|-----------------|
| Fel teckenkodning | Filer sparade i ISO‑8859‑1 men parsade som UTF‑8 ger felaktiga tecken. | Detektera teckenkodningen från filens meta‑tagg (`<meta charset="...">`) eller skicka det korrekta namnet till `Jsoup.parse`. |
| Stora filer | Att läsa in en mycket stor HTML‑fil i minnet kan orsaka `OutOfMemoryError`. | Strömma filen med `Jsoup.parse(File, String, String baseUri)` och bearbeta noder stegvis, eller öka JVM‑heap‑storleken. |
| Oönskad script/style‑text | `text()` tar bort script‑ och style‑innehåll, men anpassade besökare kan oavsiktligt inkludera det. | Hoppa över noder vars taggnamn är `script` eller `style` i besökarens `head`‑metod. |
| Bevara blanksteg | Att kollapsa mellanslag kan förlora formatering som behövs för markdown‑konvertering. | Använd `Element.wholeText()` för råa textnoder och bearbeta sedan blanksteg manuellt. |

Att adressera dessa frågor säkerställer att din **html to text java**‑lösning fungerar pålitligt över olika indata.

## Fullt körbart exempel

Nedan är ett fristående program som demonstrerar hela arbetsflödet—från beroendeinstallation till verifiering av output. Kopiera koden till en fil med namnet `HtmlToTextDemo.java`, placera en `input.html`‑fil bredvid den och kör `javac && java` som visas.

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

### Köra programmet

```bash
javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java
java -cp .:jsoup-1.17.2.jar HtmlToTextDemo
```

Konsolen visar både den enkla extraktionen och den detaljerade

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man använder XPath i Java – Läs HTML och extrahera text](/html/english/java/creating-managing-html-documents/how-to-use-xpath-in-java-read-html-and-extract-text/)
- [Hur man parsar HTML i Java – Extrahera text från HTML‑artiklar](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Extrahera text från HTML med Java – Komplett steg‑för‑steg‑guide](/html/english/java/creating-managing-html-documents/extract-text-from-html-with-java-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
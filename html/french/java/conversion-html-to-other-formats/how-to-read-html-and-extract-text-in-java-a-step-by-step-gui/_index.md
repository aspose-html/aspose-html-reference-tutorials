---
category: general
date: 2026-10-28
description: Comment lire du HTML en Java et extraire le texte des fichiers HTML.
  Apprenez à convertir le HTML en texte avec Jsoup, en couvrant la lecture du HTML
  depuis un fichier et les techniques Java de conversion du HTML en texte.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to read html
- extract text from html
- convert html to text
- html to text java
- read html from file
language: fr
lastmod: 2026-10-28
og_description: Comment lire du HTML en Java et extraire le texte des fichiers HTML.
  Ce tutoriel montre une solution complète pour convertir le HTML en texte en utilisant
  Jsoup.
og_image_alt: Diagram showing how to read HTML and extract text in Java
og_title: Comment lire du HTML et extraire le texte en Java – guide rapide
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
title: Comment lire du HTML et extraire le texte en Java – guide étape par étape
url: /fr/java/conversion-html-to-other-formats/how-to-read-html-and-extract-text-in-java-a-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment lire du HTML et extraire du texte en Java – un guide étape par étape

Si vous avez besoin de **how to read html** depuis un fichier local, ce guide fournit une solution complète. Vous apprendrez à charger un document HTML, à extraire le texte brut, et éventuellement à convertir le HTML en texte avec un contrôle fin. À la fin du tutoriel, vous pourrez exécuter le code d'exemple et voir le texte extrait affiché dans la console.

Lire des fichiers HTML est une tâche courante lors du traitement de données récupérées sur le web, de la génération de rapports ou du nettoyage de contenu généré par les utilisateurs. Les étapes ci‑dessous couvrent tout ce dont vous avez besoin, de l'ajout de la bibliothèque requise à la gestion des cas limites tels que le balisage malformé ou les problèmes d'encodage de caractères.

## Ce dont vous avez besoin

- Java 17 ou version ultérieure (le code se compile également avec des versions antérieures)
- Maven ou Gradle pour la gestion des dépendances, ou le JAR Jsoup ajouté manuellement
- Un fichier HTML nommé `input.html` placé dans le répertoire `src/main/resources` du projet (vous pouvez modifier le chemin plus tard)

## Configurer la bibliothèque Jsoup

Jsoup est une bibliothèque légère et bien documentée qui analyse le HTML en une structure similaire à un DOM. Elle gère le HTML cassé avec grâce, ce qui la rend idéale pour les tâches de **extract text from html**.

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

Si vous préférez un téléchargement manuel, placez le JAR sur votre classpath et importez `org.jsoup.*` dans votre fichier source.

## Charger le HTML depuis un fichier

La première étape programmatique consiste à lire le fichier dans un objet `Document`. Jsoup propose une méthode statique `parse` qui accepte un `File` et le nom d’un jeu de caractères.

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

**Why this matters:** `Jsoup.parse(File, String)` lit les octets bruts, les décode selon le jeu de caractères fourni, et construit un DOM propre. Cette approche est plus sûre que de lire le fichier dans une chaîne vous‑même, car Jsoup normalise les fins de ligne et corrige automatiquement les erreurs de balisage courantes.

## Extraire le texte brut du HTML

Une fois que vous avez un `Document`, récupérer le texte visible ne nécessite qu’un appel de méthode. La méthode `text()` concatène le contenu textuel de tous les éléments tout en ignorant les balises, les scripts et les styles.

```java
// Inside the try block from the previous snippet
String plainText = doc.body().text();
System.out.println("Extracted text:");
System.out.println(plainText);
```

L’appel `body()` limite l’extraction à l’élément `<body>`, qui est la cible typique lorsque vous **read html from file** pour l’analyse de contenu. La chaîne résultante contient les espaces blancs réduits à un seul espace, imitant la façon dont un navigateur rendrait le texte.

### Résultat attendu

En supposant que `input.html` contienne :

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

L’exécution du programme affiche :

```
Extracted text:
Hello World This is a demo page.
```

## Convertir le HTML en texte avec des options supplémentaires

Parfois vous avez besoin de plus de contrôle que ce que fournit `text()` — par exemple, préserver les sauts de ligne, conserver la numérotation des listes ou ignorer certaines balises. Le `NodeTraversor` de Jsoup combiné à un `NodeVisitor` personnalisé vous offre cette flexibilité.

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

Remplacez l’appel simple `doc.body().text()` par :

```java
String detailedText = convertHtmlToText(doc);
System.out.println("Detailed conversion:");
System.out.println(detailedText);
```

**Why this works:** Le visiteur parcourt le DOM en profondeur, ajoutant un saut de ligne avant chaque élément de niveau bloc (par ex., `<p>`, `<div>`, `<h1>`). Cela maintient la séparation des paragraphes, ce qui est utile lorsque vous **convert html to text** pour la lisibilité ou les pipelines NLP en aval.

## Pièges courants et bonnes pratiques

| Issue | Why it occurs | Recommended fix |
|-------|---------------|-----------------|
| Wrong charset | Files saved in ISO‑8859‑1 but parsed as UTF‑8 produce garbled characters. | Detect the charset from the file’s meta tag (`<meta charset="...">`) or pass the correct name to `Jsoup.parse`. |
| Large files | Loading a very large HTML file into memory can cause `OutOfMemoryError`. | Stream the file with `Jsoup.parse(File, String, String baseUri)` and process nodes incrementally, or increase the JVM heap size. |
| Unwanted script/style text | `text()` removes script and style content, but custom visitors may unintentionally include it. | Skip nodes whose tag name is `script` or `style` inside the visitor’s `head` method. |
| Preserving whitespace | Collapsing spaces may lose formatting needed for markdown conversion. | Use `Element.wholeText()` for raw text nodes, then post‑process whitespace manually. |

Aborder ces points garantit que votre solution **html to text java** fonctionne de manière fiable avec des entrées diverses.

## Exemple complet exécutable

Ci‑dessous se trouve un programme autonome qui démontre l’ensemble du flux de travail — de la configuration des dépendances à la vérification du résultat. Copiez le code dans un fichier nommé `HtmlToTextDemo.java`, placez un fichier `input.html` à côté, et exécutez `javac && java` comme indiqué.

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

### Exécution du programme

```bash
javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java
java -cp .:jsoup-1.17.2.jar HtmlToTextDemo
```

La console affiche à la fois l'extraction simple et le détail

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Use XPath in Java – Read HTML and Extract Text](/html/english/java/creating-managing-html-documents/how-to-use-xpath-in-java-read-html-and-extract-text/)
- [How to Parse HTML in Java – Extract Text from HTML Articles](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Extract text from HTML with Java – Complete Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/extract-text-from-html-with-java-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
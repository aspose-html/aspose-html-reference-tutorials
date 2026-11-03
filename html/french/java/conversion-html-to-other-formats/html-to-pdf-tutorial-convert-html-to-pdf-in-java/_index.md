---
category: general
date: 2026-06-19
description: Apprenez à générer un PDF à partir de HTML en utilisant un exemple Java
  simple. Ce tutoriel HTML vers PDF vous montre comment convertir un fichier HTML
  en PDF avec OpenHTMLtoPDF.
draft: false
keywords:
- html to pdf tutorial
- generate pdf from html
- convert html file pdf
- create pdf from html
- convert webpage to pdf
language: fr
og_description: Le tutoriel html to pdf vous montre comment générer un PDF à partir
  de HTML en utilisant Java. Suivez les étapes pour convertir rapidement un fichier
  HTML en PDF.
og_title: 'Tutoriel HTML vers PDF : guide de conversion Java'
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  headline: 'html to pdf tutorial: Convert HTML to PDF in Java'
  type: TechArticle
- description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  name: 'html to pdf tutorial: Convert HTML to PDF in Java'
  steps:
  - name: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
    text: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
  - name: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
    text: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
  - name: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
    text: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
  type: HowTo
tags:
- Java
- PDF
- HTML conversion
title: 'Tutoriel HTML vers PDF : Convertir HTML en PDF en Java'
url: /fr/java/conversion-html-to-other-formats/html-to-pdf-tutorial-convert-html-to-pdf-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutoriel html vers pdf – Transformez une page HTML en PDF avec Java

Vous êtes-vous déjà demandé comment transformer une page HTML statique en un document PDF élégant sans quitter votre IDE ? Vous n'êtes pas seul. Dans ce **tutoriel html vers pdf** nous allons parcourir un exemple complet, prêt à l’emploi, en Java qui **génère un pdf à partir de html** en quelques minutes seulement.

Nous couvrirons tout ce dont vous avez besoin — configuration du projet, ajout de la bonne bibliothèque, écriture du code de conversion, et même une astuce rapide pour convertir une page web en PDF. À la fin, vous pourrez **convertir un fichier html en pdf** sur votre propre machine, et vous comprendrez comment **créer un pdf à partir de html** pour tout projet futur.

## Ce dont vous aurez besoin

- Java 17 ou plus récent (le code fonctionne avec n’importe quel JDK récent)
- Maven ou Gradle (nous montrerons l’extrait Maven)
- Un petit fichier HTML que vous souhaitez transformer en PDF (nous le créerons à la volée)
- Un IDE ou un simple éditeur de texte — à vous de choisir

C’est tout. Pas de serveurs lourds, pas de SDK payants, juste du Java pur et une bibliothèque open‑source gratuite.

## Étape 1 : tutoriel html vers pdf – Configurer un projet Maven

Première chose à faire. Créez un nouveau projet Maven (ou ajoutez‑le à un projet existant). La seule dépendance dont vous avez réellement besoin est **OpenHTMLtoPDF**, qui se charge du rendu du HTML et du CSS en PDF.

```xml
<!-- pom.xml snippet -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>html-to-pdf-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- OpenHTMLtoPDF core -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-pdfbox</artifactId>
            <version>1.0.10</version>
        </dependency>
        <!-- Optional: support for SVG, if your HTML uses it -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-svg-support</artifactId>
            <version>1.0.10</version>
        </dependency>
    </dependencies>
</project>
```

> **Astuce :** Si vous utilisez Gradle, les mêmes dépendances peuvent être ajoutées sous `implementation` dans `build.gradle`.  

Pourquoi cette étape est importante : sans la bibliothèque, la JVM ne sait pas comment traduire les balises HTML en commandes de dessin PDF. OpenHTMLtoPDF est légère, maintenue activement, et fonctionne avec CSS‑2.1, de sorte que votre style reste intact.

## Étape 2 : générer pdf à partir de html – Préparer un fichier HTML d’exemple

Créons un petit `input.html` juste à côté de notre source Java. Cela rend l’exemple autonome et montre le flux de travail **créer pdf à partir de html**.

```html
<!-- src/main/resources/input.html -->
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Sample Report</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; }
        h1 { color: #2E86C1; }
        p { line-height: 1.5; }
    </style>
</head>
<body>
    <h1>Monthly Sales Report</h1>
    <p>This PDF was generated directly from an HTML file using Java.</p>
    <p>All you need is a few lines of code.</p>
</body>
</html>
```

Vous pouvez remplacer le contenu par n’importe quoi — tables, images, même du JavaScript (bien que le moteur ignore les scripts). L’important est que le fichier se trouve sur le classpath afin que le convertisseur puisse le localiser.

## Étape 3 : convertir fichier html en pdf – Écrire l’utilitaire de conversion

Voici le cœur du **tutoriel html vers pdf** : une petite classe `HtmlToPdfConverter` qui lit le HTML et écrit un PDF. Le code ci‑dessous est un exemple complet et exécutable ; copiez‑collez‑le dans `src/main/java/com/example/HtmlToPdfConverter.java`.

```java
package com.example;

import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardCopyOption;

/**
 * Simple utility that converts an HTML file to PDF.
 * It demonstrates the "convert html file pdf" use‑case.
 */
public class HtmlToPdfConverter {

    /**
     * Converts the given HTML file to a PDF file.
     *
     * @param htmlPath path to the source HTML file (can be absolute or classpath)
     * @param pdfPath  destination path for the generated PDF
     * @throws IOException if reading or writing fails
     */
    public static void convert(String htmlPath, String pdfPath) throws IOException {
        // Resolve the HTML file – support both absolute paths and classpath resources
        InputStream htmlStream = Files.exists(Path.of(htmlPath))
                ? Files.newInputStream(Path.of(htmlPath))
                : HtmlToPdfConverter.class.getResourceAsStream(htmlPath);

        if (htmlStream == null) {
            throw new FileNotFoundException("HTML source not found: " + htmlPath);
        }

        // Ensure the output directory exists
        Path pdfFile = Path.of(pdfPath);
        Files.createDirectories(pdfFile.getParent());

        try (OutputStream os = Files.newOutputStream(pdfFile);
             InputStream is = htmlStream) {

            // Builder does the heavy lifting – it parses HTML + CSS and writes PDF bytes
            new PdfRendererBuilder()
                    .withHtmlContent(new String(is.readAllBytes()), null) // base URI null = no external resources
                    .toStream(os)
                    .run();
        }
    }

    // Demo entry point – feel free to run this class directly
    public static void main(String[] args) {
        // Step 1: Specify the input HTML file location
        String htmlPath = "src/main/resources/input.html";

        // Step 2: Specify the desired output PDF file location
        String pdfPath = "target/output.pdf";

        // Step 3: Convert the HTML document to PDF using default conversion settings
        try {
            convert(htmlPath, pdfPath);
            System.out.println("✅ PDF successfully created at " + pdfPath);
        } catch (Exception e) {
            System.err.println("❌ Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Pourquoi ce code fonctionne

1. **Flexibilité des ressources** – la méthode vérifie d’abord si le chemin fourni pointe vers un vrai fichier ; sinon, elle revient à une ressource du classpath. Cela signifie que vous pouvez **convertir une page web en pdf** plus tard en fournissant une chaîne d’URL (remplacez simplement l’appel `withHtmlContent` par `withUri`).

2. **Création automatique de répertoires** – `Files.createDirectories` garantit que le dossier `target/` existe, évitant ainsi l’erreur « No such file or directory ».

3. **Conversion en une ligne** – `PdfRendererBuilder` gère le CSS, les polices et la mise en page des pages en interne. Pas besoin de gérer manuellement les pages PDF ; la bibliothèque le fait pour vous, ce qui garde l’exemple court et centré sur le concept **convertir fichier html en pdf**.

## Étape 4 : créer pdf à partir de html – Exécuter le programme et vérifier

Ouvrez un terminal à la racine du projet et lancez :

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HtmlToPdfConverter
```

Si tout est correctement configuré, vous verrez :

```
✅ PDF successfully created at target/output.pdf
```

Ouvrez `target/output.pdf` avec n’importe quel lecteur PDF. Vous devriez voir l’en‑tête stylisé « Monthly Sales Report », le texte du paragraphe, et les mêmes marges que vous avez définies dans le bloc `<style>` du HTML.

> **Et si le style n’apparaît pas ?**  
> Assurez‑vous que le CSS est en ligne ou situé dans le même dossier que le HTML. OpenHTMLtoPDF résout les URLs relatives en fonction de l’URI de base que vous passez à `withHtmlContent`. Dans l’extrait ci‑dessus nous avons passé `null`, ce qui fonctionne pour un CSS simple en ligne. Pour des feuilles de style externes, fournissez le chemin du répertoire comme deuxième argument.

## Étape 5 : convertir page web en pdf – Gestion des URLs distantes (optionnel)

Parfois vous devez **convertir une page web en pdf** directement depuis Internet — pensez à archiver un reçu en ligne. La bibliothèque supporte cela via `withUri`. Voici une adaptation rapide :

```java
public static void convertUrl(String url, String pdfPath) throws IOException {
    Path pdfFile = Path.of(pdfPath);
    Files.createDirectories(pdfFile.getParent());

    try (OutputStream os = Files.newOutputStream(pdfFile)) {
        new PdfRendererBuilder()
                .withUri(url)          // Load HTML from the web
                .toStream(os)
                .run();
    }
}
```

Appelez‑la ainsi :



## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités d’API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment convertir HTML en PDF Java – Utilisation d'Aspose.HTML pour Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Convertir HTML en PDF Java – Configuration de l’environnement dans Aspose.HTML](/html/english/java/configuring-environment/)
- [Convertir HTML en PDF en Java – Guide étape par étape avec réglages de taille de page](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
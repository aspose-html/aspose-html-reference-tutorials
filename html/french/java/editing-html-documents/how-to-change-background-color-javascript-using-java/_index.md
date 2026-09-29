---
category: general
date: 2026-09-29
description: Modifier la couleur d'arrière-plan avec JavaScript dans un fichier HTML
  en utilisant Java. Apprenez à charger du HTML en Java, à exécuter du JS dans le
  HTML et à modifier le HTML avec Java pour un nouvel arrière‑plan de page.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change background color javascript
- load html in java
- run js in html
- modify html with java
- set page background
language: fr
lastmod: 2026-09-29
og_description: Modifier la couleur d'arrière‑plan avec JavaScript dans une page HTML
  en utilisant Java. Ce tutoriel vous montre comment charger du HTML en Java, exécuter
  du JS dans le HTML et définir l'arrière‑plan de la page de façon programmatique.
og_image_alt: Screenshot of Java code that changes the page background color
og_title: Changer la couleur d'arrière‑plan avec JavaScript et Java – guide étape
  par étape
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Change background color javascript in an HTML file using Java. Learn
    to load html in java, run js in html, and modify html with java for a new page
    background.
  headline: How to change background color javascript using Java
  type: TechArticle
tags:
- Java
- HTMLUnit
- JavaScript
- HTML manipulation
title: Comment changer la couleur d'arrière-plan en JavaScript en utilisant Java
url: /fr/java/editing-html-documents/how-to-change-background-color-javascript-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment changer la couleur d'arrière‑plan javascript avec Java

Si vous devez **changer la couleur d'arrière‑plan javascript** dans un fichier HTML existant, vous pouvez le faire entièrement depuis Java sans ouvrir de navigateur. Ce tutoriel vous montre comment **charger du html en java**, exécuter un petit extrait JavaScript, puis **modifier le html avec java** afin que l'arrière‑plan de la page soit mis à jour.  

La solution fonctionne avec la bibliothèque open‑source **HTMLUnit**, qui fournit un navigateur sans tête capable d’évaluer le JavaScript exactement comme le ferait un vrai navigateur. À la fin de ce guide, vous disposerez d’une méthode réutilisable qui **définit l'arrière‑plan de la page** à n’importe quelle couleur de votre choix.

## Prérequis

| Ce dont vous avez besoin | Pourquoi c'est important |
|--------------------------|---------------------------|
| Java 8 ou version supérieure | HTMLUnit nécessite au moins Java 8. |
| Outil de construction Maven ou Gradle | Pour récupérer automatiquement la dépendance HTMLUnit. |
| Un fichier HTML que vous souhaitez modifier (par ex., `input.html`) | Le document source qui sera chargé et modifié. |

Ajoutez HTMLUnit à votre projet :

*Maven*  

```xml
<dependency>
    <groupId>net.sourceforge.htmlunit</groupId>
    <artifactId>htmlunit</artifactId>
    <version>2.71.0</version>
</dependency>
```

*Gradle*  

```gradle
implementation 'net.sourceforge.htmlunit:htmlunit:2.71.0'
```

> **Astuce :** Utilisez la dernière version stable d'HTMLUnit pour obtenir le moteur JavaScript le plus précis.

## Changer la couleur d'arrière‑plan javascript – charger le HTML en Java

La première étape consiste à charger le document HTML dans un objet `HTMLPage`. Cela vous donne une API de type DOM ainsi qu’un contexte d’exécution JavaScript.

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;

public class BackgroundColorChanger {

    /**
     * Loads an HTML file from the given path.
     *
     * @param htmlPath absolute or relative path to the source HTML file
     * @return HtmlPage representing the loaded document
     * @throws IOException if the file cannot be read
     */
    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        // WebClient acts as a headless browser; disabling CSS speeds up loading.
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);

        // Convert the file path to a URL that HTMLUnit can understand.
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }
}
```

*Pourquoi c'est important* : `WebClient` crée un environnement sandbox où le JavaScript peut s’exécuter, vous permettant ainsi de **run js in html** exactement comme le ferait le navigateur d’un utilisateur.

## Exécuter js in html pour définir l'arrière‑plan de la page

Une fois la page chargée, vous pouvez évaluer n’importe quelle expression JavaScript. L’extrait ci‑dessous modifie la propriété `backgroundColor` du style de l’élément `<body>`.

```java
/**
 * Executes JavaScript that changes the page background color.
 *
 * @param page   the HtmlPage loaded earlier
 * @param color  any valid CSS color string, e.g., "lightblue" or "#ffcc00"
 */
private static void changeBackground(HtmlPage page, String color) {
    // The eval method runs JavaScript in the page's context.
    String script = "document.body.style.backgroundColor = '" + color + "';";
    page.getEnclosingWindow().getScriptableObject().eval(script);
}
```

*Explication* :  
- `document.body.style.backgroundColor` est la propriété DOM standard pour l’arrière‑plan de la page.  
- En appelant `eval`, nous **run js in html** sans besoin d’une vraie fenêtre de navigateur.  
- La méthode est réutilisable pour n’importe quelle couleur, répondant ainsi à l’exigence **set page background**.

## Modifier le html avec java et enregistrer le résultat

Après l’exécution du script, le DOM reflète le nouveau style. Vous pouvez maintenant écrire le HTML mis à jour sur le disque.

```java
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Saves the modified HTML content to a new file.
 *
 * @param page          the HtmlPage that has been altered
 * @param outputPath    destination file path
 * @throws IOException  if writing fails
 */
private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
    // page.asXml() returns the current HTML markup, including the changed style.
    String updatedHtml = page.asXml();
    Files.write(Paths.get(outputPath), updatedHtml.getBytes());
}
```

Assembler le tout vous donne un programme unique et exécutable :

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;

public class BackgroundColorChanger {

    public static void main(String[] args) {
        // Adjust these paths for your environment.
        String inputFile = "YOUR_DIRECTORY/input.html";
        String outputFile = "YOUR_DIRECTORY/js_modified.html";
        String newColor = "lightblue"; // Change to any CSS color you need.

        try {
            HtmlPage page = loadHtml(inputFile);
            changeBackground(page, newColor);
            saveModifiedHtml(page, outputFile);
            System.out.println("Background color changed to '" + newColor + "' and saved to " + outputFile);
        } catch (IOException e) {
            System.err.println("Error processing HTML file: " + e.getMessage());
        }
    }

    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }

    private static void changeBackground(HtmlPage page, String color) {
        String script = "document.body.style.backgroundColor = '" + color + "';";
        page.getEnclosingWindow().getScriptableObject().eval(script);
    }

    private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
        String updatedHtml = page.asXml();
        Files.write(Paths.get(outputPath), updatedHtml.getBytes());
    }
}
```

### Sortie attendue

L’exécution du programme affiche :

```
Background color changed to 'lightblue' and saved to YOUR_DIRECTORY/js_modified.html
```

Ouvrir `js_modified.html` dans n’importe quel navigateur montre la page avec un arrière‑plan bleu clair, confirmant que l’opération **change background color javascript** a réussi.

## Variations courantes et cas limites

| Situation | Comment le gérer |
|-----------|------------------|
| **Différents formats de couleur** | Passez n’importe quelle valeur compatible CSS (`"red"`, `"#ff0000"`, `"rgb(255,0,0)"`). |
| **Balise `<body>` manquante** | Le script échouera silencieusement ; vous pouvez d’abord vous assurer que `<body>` existe avec `page.getFirstByXPath("//body")`. |
| **Fichiers HTML volumineux** | Désactivez le CSS (`setCssEnabled(false)`) et activez uniquement les fonctionnalités JavaScript dont vous avez besoin pour réduire la consommation mémoire. |
| **Exécution de plusieurs scripts** | Appelez `changeBackground` à plusieurs reprises ou créez une méthode utilitaire qui accepte une liste de commandes JavaScript. |

## Conclusion

Vous savez maintenant comment **changer la couleur d'arrière‑plan javascript** en chargeant un fichier HTML avec Java, **run js in html**, et **modifier le html avec java** pour **set page background** à la couleur de votre choix. L’exemple complet ci‑dessus fonctionne avec la dernière version d’HTMLUnit et peut être intégré à des pipelines d’automatisation plus larges, comme le traitement par lots de rapports HTML ou la préparation de modèles d’e‑mail.

**Prochaines étapes**  
- Explorez d’autres manipulations du DOM (par ex., insertion d’éléments, suppression de scripts).  
- Combinez cette approche avec un moteur de rendu PDF pour générer des PDF des pages stylisées.  
- Essayez d’utiliser un autre moteur sans tête comme Selenium WebDriver si vous avez besoin d’une fidélité totale du navigateur.

Bonne programmation !

## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités d’API et explorer des approches d’implémentation alternatives dans vos projets.

- [Get Computed Style Java – Extract Background Color from HTML](/html/english/java/css-html-form-editing/get-computed-style-java-extract-background-color-from-html/)
- [How to Load HTML, Set Device DPI & Read Background Color](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Generate HTML from JavaScript in Java – Complete Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/generate-html-from-javascript-in-java-complete-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
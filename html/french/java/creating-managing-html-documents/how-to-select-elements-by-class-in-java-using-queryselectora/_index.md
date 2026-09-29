---
category: general
date: 2026-09-29
description: Apprenez à sélectionner des éléments par classe, lire du HTML depuis
  un fichier et trouver les liens externes en Java. Ce guide étape par étape couvre
  l'itération efficace d’une NodeList.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- select elements by class
- read html from file
- find external links
- iterate nodelist java
- use queryselectorall java
language: fr
lastmod: 2026-09-29
og_description: Sélectionner des éléments par classe en Java, lire le HTML depuis
  un fichier et trouver les liens externes avec querySelectorAll. Suivez l’exemple
  complet pour parcourir un NodeList.
og_image_alt: Screenshot showing Java code that selects elements by class from an
  HTML file
og_title: Sélectionner des éléments par classe en Java – guide complet avec querySelectorAll
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to select elements by class, read HTML from file, and find
    external links in Java. This step‑by‑step guide covers iterating a NodeList efficiently.
  headline: How to select elements by class in Java using querySelectorAll
  type: TechArticle
- questions:
  - answer: Yes. `Jsoup.parse` treats the input as a fragment and automatically adds
      missing root elements, allowing selectors to work on the fragment’s body.
    question: Does this work with HTML fragments that lack a `<html>` root?
  - answer: The standard Java DOM API (`org.w3c.dom`) does not include `querySelectorAll`.
      Libraries such as **HTMLUnit** or **jodd-lagarto** provide similar methods.
      The pattern shown here—load, select with CSS, iterate—remains the same.
    question: Can I use `querySelectorAll` without jsoup?
  - answer: 'After obtaining each `Element`, you can call `link.attr("href", "newUrl")`
      and then write the document back to disk with `Files.writeString`. ## Conclusion
      You now know how to **select elements by class**, **read HTML from file**, **find
      external links**, and **iterate a NodeList in Java** using `qu'
    question: What if I need to modify the links instead of just printing them?
  type: FAQPage
tags:
- Java
- HTML parsing
- DOM manipulation
title: Comment sélectionner des éléments par classe en Java avec querySelectorAll
url: /fr/java/creating-managing-html-documents/how-to-select-elements-by-class-in-java-using-queryselectora/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment sélectionner des éléments par classe en Java avec querySelectorAll

Si vous devez **sélectionner des éléments par classe** lors du traitement d'un fichier HTML en Java, ce guide vous montre exactement comment le faire. Vous apprendrez à lire le HTML depuis un fichier, à utiliser `querySelectorAll` pour trouver les liens externes, et à parcourir en toute sécurité le `NodeList` résultant.

Travailler avec du HTML en Java semble souvent lourd, mais les bibliothèques modernes vous offrent une API concise basée sur les sélecteurs CSS. L'exemple ci‑dessous utilise **jsoup** (version 1.17.2) car il implémente des sélecteurs de type `querySelectorAll` et renvoie une collection `Elements` qui se comporte comme un `NodeList`. Vous pouvez adapter la même logique à d'autres implémentations DOM si nécessaire.

## Prérequis

* JDK 17 ou version supérieure installé.
* Maven ou Gradle pour la gestion des dépendances.
* Familiarité de base avec les streams Java et le modèle DOM.

Ajoutez jsoup à votre projet :

```xml
<!-- Maven -->
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

```gradle
// Gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

## Étape 1 : Lire le HTML depuis un fichier

La première tâche consiste à charger le document HTML depuis le disque. `Jsoup.parse(Path, Charset)` lit le fichier et construit un arbre DOM que vous pouvez interroger.

```java
import java.nio.file.Paths;
import java.nio.charset.StandardCharsets;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class HtmlLoader {
    /**
     * Loads an HTML file and returns a Jsoup Document.
     *
     * @param filePath absolute or relative path to the HTML file
     * @return parsed Document ready for DOM queries
     * @throws IOException if the file cannot be read
     */
    public static Document load(String filePath) throws IOException {
        return Jsoup.parse(Paths.get(filePath).toFile(),
                           StandardCharsets.UTF_8.name(),
                           "");
    }
}
```

*Pourquoi c’est important* : charger le fichier une seule fois évite des I/O répétés pendant que vous parcourez les éléments plus tard. L’objet `Document` contient le DOM complet, ce qui permet des requêtes de sélecteur rapides.

## Étape 2 : Utiliser `querySelectorAll` pour sélectionner des éléments par classe

Maintenant que le document est en mémoire, vous pouvez **sélectionner des éléments par classe** à l’aide d’un sélecteur CSS. Le sélecteur `"a.external"` correspond aux balises `<a>` qui possèdent la classe `external` — exactement ce dont vous avez besoin pour **trouver les liens externes**.

```java
import org.jsoup.select.Elements;
import org.jsoup.nodes.Element;

/**
 * Returns all anchor elements with the CSS class "external".
 *
 * @param doc the parsed HTML document
 * @return a collection of matching Elements
 */
public static Elements findExternalLinks(Document doc) {
    // querySelectorAll is simulated by the select() method in Jsoup
    return doc.select("a.external");
}
```

*Pourquoi c’est important* : utiliser un sélecteur de classe est à la fois expressif et performant. La bibliothèque traduit le sélecteur en un parcours optimisé, vous n’avez donc pas besoin d’écrire des boucles manuelles sur chaque nœud.

## Étape 3 : Parcourir le NodeList (Elements) en Java

`Elements` implémente `Iterable<Element>`, ce qui signifie que vous pouvez utiliser une boucle `for‑each` standard pour **parcourir les objets NodeList en Java**. La boucle ci‑dessous affiche l’attribut `href` de chaque lien.

```java
/**
 * Prints the href attribute of every external link.
 *
 * @param externalLinks collection returned by findExternalLinks()
 */
public static void printExternalLinks(Elements externalLinks) {
    for (Element link : externalLinks) {
        System.out.println("External link: " + link.attr("href"));
    }
}
```

*Pourquoi c’est important* : l’itération directe rend le code lisible et évite le surcoût de conversion de la collection en stream lorsque vous avez seulement besoin d’une sortie simple.

## Exemple complet fonctionnel

En combinant les trois étapes, on obtient un programme autonome que vous pouvez exécuter depuis la ligne de commande.

```java
import java.io.IOException;
import org.jsoup.nodes.Document;
import org.jsoup.select.Elements;

public class ExternalLinkExtractor {

    public static void main(String[] args) {
        // Validate input
        if (args.length != 1) {
            System.err.println("Usage: java ExternalLinkExtractor <input.html>");
            System.exit(1);
        }

        String inputPath = args[0];

        try {
            // Step 1: read HTML from file
            Document doc = HtmlLoader.load(inputPath);

            // Step 2: select elements by class (find external links)
            Elements externalLinks = findExternalLinks(doc);

            // Step 3: iterate NodeList Java and print hrefs
            printExternalLinks(externalLinks);
        } catch (IOException e) {
            System.err.println("Error reading file: " + e.getMessage());
        }
    }

    // Reuse methods from previous sections
    private static Elements findExternalLinks(Document doc) {
        return doc.select("a.external");
    }

    private static void printExternalLinks(Elements externalLinks) {
        for (org.jsoup.nodes.Element link : externalLinks) {
            System.out.println("External link: " + link.attr("href"));
        }
    }
}
```

### Sortie attendue

En supposant que `input.html` contienne :

```html
<a class="external" href="https://example.com">Example</a>
<a class="internal" href="/about">About</a>
<a class="external" href="https://openai.com">OpenAI</a>
```

L’exécution du programme affiche :

```
External link: https://example.com
External link: https://openai.com
```

## Astuces professionnelles et pièges courants

* **L’encodage est important** – Lisez toujours le fichier avec UTF‑8 (ou le jeu de caractères qui correspond à votre source). Un encodage incorrect peut corrompre les caractères dans les valeurs d’attribut.
* **Classes multiples** – Si un élément possède plusieurs classes (par ex., `class="btn external"`), le sélecteur `"a.external"` correspond toujours car les sélecteurs de classe CSS vérifient la présence du token, pas la chaîne exacte.
* **Astuce de performance** – Si vous avez seulement besoin de l’attribut `href`, vous pouvez le demander directement avec `doc.select("a.external[href]").eachAttr("href")`. Cela évite de créer des objets `Element` complets pour chaque correspondance.
* **Sécurité contre les null** – `link.attr("href")` renvoie une chaîne vide si l’attribut est absent, vous n’avez donc pas besoin de vérifier la nullité avant d’afficher.

## Questions fréquentes

**Q : Cette méthode fonctionne‑t‑elle avec des fragments HTML qui n’ont pas de racine `<html>` ?**  
R : Oui. `Jsoup.parse` traite l’entrée comme un fragment et ajoute automatiquement les éléments racine manquants, ce qui permet aux sélecteurs de fonctionner sur le corps du fragment.

**Q : Puis‑je utiliser `querySelectorAll` sans jsoup ?**  
R : L’API DOM standard de Java (`org.w3c.dom`) ne comprend pas `querySelectorAll`. Des bibliothèques comme **HTMLUnit** ou **jodd-lagarto** offrent des méthodes similaires. Le schéma présenté ici — charger, sélectionner avec CSS, itérer — reste le même.

**Q : Et si je dois modifier les liens au lieu de simplement les afficher ?**  
R : Après avoir obtenu chaque `Element`, vous pouvez appeler `link.attr("href", "newUrl")` puis écrire le document de nouveau sur le disque avec `Files.writeString`.

## Conclusion

Vous savez maintenant comment **sélectionner des éléments par classe**, **lire le HTML depuis un fichier**, **trouver les liens externes**, et **parcourir un NodeList en Java** en utilisant des sélecteurs de type `querySelectorAll`. L’exemple complet montre un flux de travail propre et prêt pour la production que vous pouvez intégrer dans des pipelines de scraping ou de transformation plus vastes.

Ensuite, explorez des sujets connexes tels que **l’analyse de contenu dynamique avec HTMLUnit**, **l’écriture du HTML modifié sur le disque**, ou **l’utilisation des streams Java pour collecter les URL des liens dans une liste**. Chacun de ces sujets s’appuie sur la technique fondamentale de sélection basée sur les classes présentée ici. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d’API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment interroger le HTML en Java – Sélectionner des éléments, filtrer par attribut et obtenir le texte](/html/english/java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/)
- [Parcourir NodeList Java – Lire le HTML et obtenir le src des images](/html/english/java/creating-managing-html-documents/iterate-nodelist-java-read-html-get-image-src/)
- [Charger des documents HTML depuis un fichier avec Aspose.HTML pour Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
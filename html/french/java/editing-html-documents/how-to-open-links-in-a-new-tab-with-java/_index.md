---
category: general
date: 2026-10-28
description: Apprenez à ouvrir les liens dans un nouvel onglet en analysant le HTML
  en Java, à identifier les liens externes et à ajouter target='_blank'.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- open links new tab
- find external links
- add target blank
- parse html in java
- save modified html
language: fr
lastmod: 2026-10-28
og_description: 'Ouvrir les liens dans un nouvel onglet avec Java : analyser le HTML,
  trouver les liens externes, ajouter target=''_blank'' et enregistrer le HTML modifié.'
og_image_alt: Screenshot of Java code that parses HTML and updates external links
  to open in a new tab
og_title: Ouvrir les liens dans un nouvel onglet avec Java – guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to open links in a new tab by parsing HTML in Java, finding
    external links and adding target blank.
  headline: How to open links in a new tab with Java
  type: TechArticle
tags:
- Java
- HTML parsing
- jsoup
- web automation
title: Comment ouvrir des liens dans un nouvel onglet avec Java
url: /fr/java/editing-html-documents/how-to-open-links-in-a-new-tab-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment ouvrir des liens dans un nouvel onglet avec Java

Si vous devez **ouvrir des liens dans un nouvel onglet** à partir d'un fichier HTML statique, ce guide vous montre exactement comment le faire. Vous apprendrez à **analyser le HTML en Java**, **trouver les liens externes**, **ajouter target blank**, et **enregistrer le HTML modifié** sans quitter votre IDE.

Ouvrir des liens externes dans un nouvel onglet du navigateur améliore l'expérience utilisateur et garde les visiteurs sur la page d'origine. La solution ci‑dessous fonctionne avec n'importe quel document HTML, ne nécessite que la populaire bibliothèque jsoup, et s'exécute sur Java 8 ou version supérieure.

## Prérequis

* JDK 8 + installé  
* Un outil de construction (Maven ou Gradle) pour récupérer la dépendance **jsoup**  
* Un fichier HTML contenant des balises d'ancrage avec la classe `external`

Vous n'avez pas besoin d'un serveur web ou de frameworks supplémentaires—jsoup gère tout localement.

## Étape 1 : Configurer jsoup dans votre projet

Ajoutez jsoup en tant que dépendance. Si vous utilisez Maven, placez ceci dans `pom.xml` :

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

Pour Gradle, ajoutez la ligne suivante à `build.gradle` :

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

Ces coordonnées récupèrent la dernière version stable (en date d'octobre 2026). Après synchronisation, vous pouvez importer les classes `org.jsoup` dans vos fichiers source Java.

## Étape 2 : Analyser le document HTML

Analyser le fichier est la première étape pour **ouvrir des liens dans un nouvel onglet**. La méthode `Jsoup.parse` lit le fichier dans une structure mutable de type DOM.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // Load the HTML document from disk
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");
        
        // Continue with link processing...
    }
}
```

*Pourquoi c'est important* : `Document` vous fournit des sélecteurs de style CSS, ce qui rend trivial la localisation des éléments dont vous avez besoin.

## Étape 3 : Trouver les liens externes

Localisez maintenant chaque élément `<a>` qui possède la classe `external`. Cela correspond à l'exigence **find external links**.

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

// Inside main after parsing:
Elements externalLinks = doc.select("a.external");
```

`Elements` est une collection de nœuds correspondants. Si le sélecteur renvoie un ensemble vide, votre HTML ne possède peut‑être pas la classe ou utilise une convention de nommage différente—ajustez le sélecteur en conséquence.

## Étape 4 : Ajouter `target="_blank"` à chaque lien

Pour chaque nœud renvoyé par **find external links**, définissez l'attribut `target` à `_blank`. Cela satisfait l'étape **add target blank** et garantit que les navigateurs ouvrent le lien dans un nouvel onglet.

```java
for (Element link : externalLinks) {
    link.attr("target", "_blank");
}
```

La méthode `attr` écrase toute valeur `target` existante, garantissant un comportement cohérent pour toutes les ancres externes.

## Étape 5 : Enregistrer le HTML modifié

Après avoir mis à jour le DOM, écrivez les modifications dans un fichier. Cela complète la partie **save modified html** du tutoriel.

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

// Still inside main:
Path output = Path.of("YOUR_DIRECTORY/updated.html");
Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
System.out.println("Updated file written to " + output);
```

`doc.outerHtml()` sérialise l'ensemble du document, en préservant l'indentation et le formatage tels que jsoup les a initialement analysés.

## Exemple complet fonctionnel

Assembler toutes les étapes donne un programme autonome que vous pouvez copier, coller et exécuter.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

/**
 * Updates all external links so they open in a new tab.
 */
public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // 1️⃣ Parse the HTML file
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");

        // 2️⃣ Find external links (a.external)
        Elements externalLinks = doc.select("a.external");

        // 3️⃣ Add target="_blank" to each link
        for (Element link : externalLinks) {
            link.attr("target", "_blank");
        }

        // 4️⃣ Save the modified HTML
        Path output = Path.of("YOUR_DIRECTORY/updated.html");
        Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
        System.out.println("Updated file written to " + output);
    }
}
```

### Résultat attendu

Supposons que `sample.html` contienne :

```html
<a href="https://example.com" class="external">Example</a>
<a href="/internal/page.html">Internal</a>
```

Après l'exécution du programme, `updated.html` contiendra :

```html
<a href="https://example.com" class="external" target="_blank">Example</a>
<a href="/internal/page.html">Internal</a>
```

Seul le lien externe a reçu l'attribut `target="_blank"`, ce qui signifie que les navigateurs l'ouvriront désormais dans un nouvel onglet.

## Astuces professionnelles et pièges courants

* **Astuce :** Si vous devez traiter les liens commençant par `http://` ou `https://` comme externes même sans classe CSS, élargissez le sélecteur : `doc.select("a[href^=http]")`.
* **Cas particulier** : Certaines pages spécifient déjà `target="_self"` ; l'appel `attr` l'écrase, assurant un comportement cohérent.
* **Performance** : Pour des fichiers HTML très volumineux, envisagez un parsing en flux (`Jsoup.parse(File, String, String, Parser.htmlParser())`) afin de réduire l'utilisation de la mémoire.
* **Tests** : Vérifiez le résultat en ouvrant `updated.html` dans un navigateur et en inspectant le lien avec les outils de développement—recherchez l'attribut `target`.

## Conclusion

Vous disposez maintenant d'une solution complète et exécutable pour **ouvrir des liens dans un nouvel onglet** avec Java. Le tutoriel a couvert comment **parse html in java**, **find external links**, **add target blank**, et **save modified html**, le tout avec la bibliothèque légère jsoup.

À partir d'ici, vous pouvez :

* Étendre le sélecteur pour gérer d'autres modèles de liens (par ex., `rel="external"`).  
* Combiner cette logique avec une étape de construction qui traite tous les fichiers HTML d'un projet.  
* Intégrer le code dans un pipeline de gestion de contenu plus vaste.

N'hésitez pas à expérimenter avec différents sélecteurs ou formats de sortie, et à partager vos résultats avec la communauté !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment utiliser CSS en Java – Charger HTML, compter les liens & évaluer XPath](/html/english/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/)
- [Comment analyser le HTML en Java – Extraire le texte des articles HTML](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Créer un nouvel élément HTML avec Java – Guide complet Aspose.HTML](/html/english/java/editing-html-documents/create-new-html-element-with-java-full-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
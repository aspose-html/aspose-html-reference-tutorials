---
category: general
date: 2026-03-05
description: Comment interroger le HTML en Java pour lire un fichier HTML et extraire
  les images. Apprenez à lire un fichier HTML en Java, obtenir les URL d’images en
  Java et itérer sur NodeList en Java.
draft: false
keywords:
- how to query html
- read html file java
- how to extract images
- iterate over nodelist java
- get image urls java
language: fr
og_description: Comment interroger le HTML en Java et récupérer les URL d’images.
  Ce guide montre comment lire un fichier HTML en Java, localiser les images et parcourir
  le NodeList en Java.
og_title: Comment interroger le HTML en Java – Extraire les URL d'images
tags:
- html parsing
- java
- aspose-html
- xpath
- css selector
title: Comment interroger le HTML en Java – Extraire les URL d'images
url: /fr/java/creating-managing-html-documents/how-to-query-html-in-java-extract-image-urls/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment interroger le HTML en Java – Extraire les URL d'images

Vous vous êtes déjà demandé **comment interroger le HTML** en Java pour extraire chaque image d’une page ? Vous n’êtes pas le seul—les développeurs ont constamment besoin de lire des fichiers HTML, de récupérer des images, puis de faire quelque chose d’utile avec les URL. Dans ce tutoriel, nous allons parcourir un exemple pratique qui montre exactement **comment interroger le HTML**, lire un fichier HTML à la manière Java, et obtenir les URL d’images en Java.

Nous utiliserons Aspose.HTML pour Java, mais les concepts—XPath, sélecteurs CSS et itération sur un `NodeList`—s’appliquent à toute bibliothèque DOM. À la fin de ce guide, vous serez à l’aise avec **comment extraire des images**, saurez **comment itérer sur NodeList Java**, et disposerez d’un extrait de code prêt à l’emploi que vous pourrez intégrer à votre projet.

![How to query HTML in Java example](https://example.com/placeholder.png "How to query HTML in Java")

---

## Ce que vous allez apprendre

- Charger un document HTML depuis le disque (read HTML file Java)
- Localiser les balises `<img>` en utilisant à la fois XPath et les sélecteurs CSS (how to extract images)
- Boucler sur le `NodeList` résultant (iterate over NodeList Java)
- Afficher l’attribut `src` de chaque image (get image URLs Java)

Pas de services externes, pas d’outils de construction complexes—juste du Java pur et une seule dépendance Maven.

---

## Prérequis

- Java 8 ou version supérieure installé
- Maven ou Gradle pour la gestion des dépendances
- Familiarité de base avec la structure HTML
- Optionnel mais utile : un fichier HTML simple (`sample.html`) contenant quelques éléments `<figure><img …></figure>`

Si vous avez tout cela, nous pouvons commencer immédiatement.

---

## Étape 1 : Lire un fichier HTML Java – Charger le document

Première chose à faire : nous devons charger le HTML en mémoire. La classe `HTMLDocument` d’Aspose.HTML fait le travail lourd. Pensez-y comme à l’ouverture d’un livre afin de pouvoir tourner à n’importe quelle page.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.NodeList;
import com.aspose.html.dom.Element;

/**
 * Demonstrates how to query HTML in Java and extract image URLs.
 */
public class QueryExample {
    public static void main(String[] args) throws Exception {

        // ① Load the HTML document from a local file.
        // Replace "YOUR_DIRECTORY/sample.html" with the actual path.
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/sample.html");
```

**Pourquoi c’est important :** Charger le fichier vous fournit un arbre DOM que vous pouvez interroger. Si le chemin est incorrect, vous obtiendrez une `FileNotFoundException`, alors vérifiez bien l’emplacement avant d’exécuter.

---

## Étape 2 : Localiser les images avec XPath – How to Extract Images

XPath est un langage de requête puissant qui vous permet de cibler les nœuds avec une précision laser. Ici, nous demandons chaque `<img>` à l’intérieur d’un `<figure>` qui possède également un attribut `alt`.

```java
        // ② Use XPath to find <img> elements that have an "alt" attribute.
        NodeList xpathImages = document.evaluateXPath("//figure/img[@alt]");
        System.out.println("XPath found " + xpathImages.getLength() + " images.");
```

**Pourquoi XPath ?** C’est concis et fonctionne même lorsque le HTML est désordonné. L’expression `//figure/img[@alt]` se traduit par : « tout `<img>` sous un `<figure>` qui possède un attribut `alt` ». Si vous devez filtrer par d’autres attributs, il suffit d’ajuster les crochets.

---

## Étape 3 : Localiser les images avec un sélecteur CSS – Méthode alternative pour extraire les images

Parfois vous préférez la syntaxe CSS car elle reflète ce que vous écrivez dans les feuilles de style. `querySelectorAll` accepte le même sélecteur que vous utiliseriez dans un navigateur.

```java
        // ③ Same query using a CSS selector.
        NodeList cssImages = document.querySelectorAll("figure img[alt]");
        System.out.println("CSS selector found " + cssImages.getLength() + " images.");
```

**Pourquoi les deux ?** Montrer les deux vous permet de choisir l’outil avec lequel vous êtes le plus à l’aise. En pratique vous vous tiendrez à l’un d’eux, mais disposer des deux exemples rend le tutoriel plus complet.

---

## Étape 4 : Itérer sur NodeList Java – Obtenir les URL d’images Java

Maintenant que nous avons une collection, nous devons la parcourir. C’est ici que **iterate over NodeList Java** entre en jeu. Nous extrairons l’attribut `src` de chaque image et l’afficherons.

```java
        // ④ Loop through the NodeList returned by the CSS query.
        for (int i = 0; i < cssImages.getLength(); i++) {
            Element imageElement = (Element) cssImages.item(i);
            // Extract the "src" attribute – that’s the image URL.
            System.out.println("Image src: " + imageElement.getAttribute("src"));
        }
    }
}
```

**Pourquoi une boucle `for` classique ?** Le `NodeList` d’Aspose n’implémente pas `Iterable`, donc la syntaxe `for‑each` améliorée ne compilera pas. Utiliser une boucle avec indice est la méthode fiable pour **iterate over NodeList Java**.

---

## Résultat attendu

Exécuter le programme sur un HTML d’exemple tel que :

```html
<figure>
    <img src="images/pic1.jpg" alt="First picture">
</figure>
<figure>
    <img src="images/pic2.png" alt="Second picture">
</figure>
```

Produira quelque chose de similaire à :

```
XPath found 2 images.
CSS selector found 2 images.
Image src: images/pic1.jpg
Image src: images/pic2.png
```

---

## Pièges courants & Astuces pro

- **Problèmes de chemin de fichier :** Utilisez un chemin absolu ou placez `sample.html` relatif au répertoire de travail de votre projet.  
- **Attribut `alt` manquant :** Nos requêtes XPath/CSS filtrent sur `[@alt]`. Si vous avez besoin de *toutes* les images, supprimez le filtre d’attribut (`//figure/img` ou `figure img`).  
- **Performance :** Pour des documents volumineux, envisagez des analyseurs en flux, mais pour la plupart des tâches de web‑scraping l’approche DOM suffit.  
- **Problèmes d’encodage :** Aspose.HTML respecte le jeu de caractères déclaré dans le HTML. Si vous voyez des caractères illisibles, assurez‑vous que le fichier est enregistré en UTF‑8.  

---

## Étendre l’exemple

Maintenant que vous pouvez **get image URLs Java**, vous pourriez vouloir :

1. **Télécharger les images** en utilisant `java.net.URL` et `Files.copy`.  
2. **Stocker les URL dans une base de données** pour un traitement ultérieur.  
3. **Filtrer par extension de fichier** (`src.endsWith(".png")`).  

Toutes ces opérations sont des extensions simples de la boucle présentée à l’Étape 4.

---

## Conclusion

Dans ce guide, nous avons couvert **how to query HTML** en Java du début à la fin : charger le fichier, localiser les images avec XPath et les sélecteurs CSS, et **iterating over NodeList Java** pour afficher le `src` de chaque image. Vous avez maintenant une base solide pour **how to extract images**, et vous savez exactement **how to read HTML file Java** en utilisant Aspose.HTML.

N’hésitez pas à adapter le code à vos besoins de scraping—que ce soit pour extraire d’autres attributs, gérer les balises `<a>`, ou alimenter les URL dans un téléchargeur. Le schéma reste le même : charger, interroger, itérer, et agir.

Des questions ou envie de partager un cas d’utilisation intéressant ? Laissez un commentaire ci‑dessous, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-04-23
description: Comment utiliser querySelectorAll en Java pour filtrer les éléments par
  classe, lire les valeurs d’attributs et parcourir le NodeList afin d’extraire les
  données produit.
draft: false
keywords:
- how to use queryselectorall
- how to read attribute
- iterate nodelist java
- filter elements by class
- select elements css selector
language: fr
og_description: Comment utiliser querySelectorAll en Java pour filtrer les éléments
  par classe, lire les valeurs d’attributs et parcourir le NodeList afin d’extraire
  les données produit.
og_title: Comment utiliser querySelectorAll en Java – Filtrer par classe
tags:
- Java
- HTML parsing
- DOM manipulation
title: Comment utiliser querySelectorAll en Java – Filtrer par classe
url: /fr/java/creating-managing-html-documents/how-to-use-queryselectorall-in-java-filter-by-class/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser querySelectorAll en Java – Filtrer par classe

Utiliser querySelectorAll en Java est essentiel lorsque vous devez extraire des éléments spécifiques d'un document HTML. Dans ce tutoriel, nous filtrerons les éléments par classe, lirons les valeurs d'attributs et parcourrons un NodeList pour récupérer les prix des produits d'une page de catalogue.  

Vous êtes déjà resté(e) bloqué(e) devant un fichier HTML gigantesque, vous demandant comment extraire uniquement les cartes « en‑sale » sans écrire de parseur personnalisé ? C’est exactement le problème que nous allons résoudre ici—sans bibliothèques supplémentaires au‑delà d’Aspose.HTML, et avec quelques étapes simples.

Vous repartirez avec un programme complet et exécutable qui :

* **Sélectionne les éléments** en utilisant un sélecteur CSS (`select elements css selector`),
* **Filtre par classe** (`filter elements by class`),
* **Lit un attribut personnalisé** (`how to read attribute`),
* **Parcourt le NodeList résultant** (`iterate nodelist java`).

Aucune expérience préalable avec Aspose.HTML n'est requise—juste une configuration Java de base et un fichier HTML pour tester.

![how to use querySelectorAll in Java example](https://example.com/images/queryselectorall-java.png "how to use querySelectorAll in Java")

---

## Ce dont vous aurez besoin

| Exigence | Pourquoi c'est important |
|----------|--------------------------|
| **Java 17+** | Fonctionnalités modernes du langage et meilleure gestion des modules. |
| **Aspose.HTML for Java** (latest version) | Fournit la classe `Document` et le moteur de sélecteur CSS. |
| **catalog.html** (sample HTML) | La source sur laquelle nous interrogerons. |
| **IDE ou simple `javac`** | Pour compiler et exécuter la démo. |

Si vous n'avez pas encore ajouté Aspose.HTML à votre projet, déposez le JAR dans votre dossier `libs` et ajoutez‑le au classpath :

```bash
javac -cp "libs/*" CssSelectorDemo.java
java -cp ".:libs/*" CssSelectorDemo
```

---

## Étape 1 – Charger le document HTML

Avant de pouvoir interroger quoi que ce soit, vous avez besoin d'un objet `Document` qui représente le fichier HTML. Pensez‑y comme à charger une feuille de calcul avant de pouvoir lire des cellules.

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");
```

> **Pourquoi c'est important :** La classe `Document` analyse le balisage en un arbre DOM, permettant au moteur de sélecteur CSS de fonctionner. Ignorer cette étape vous laisserait avec une simple chaîne de caractères et aucune possibilité d'utiliser `querySelectorAll`.

---

## Étape 2 – Sélectionner les éléments avec un sélecteur CSS

Voici le cœur du sujet : **comment utiliser querySelectorAll**. La méthode accepte n'importe quel sélecteur CSS valide, vous pouvez donc être aussi précis—ou aussi large—que vous le souhaitez. Pour notre scénario, nous voulons les cartes produit qui :

* possèdent la classe `product-card`,
* sont également marquées avec la classe `sale`,
* et portent un attribut `data-price`.

```java
        // Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );
```

> **Explication :**  
> * `.product-card.sale` → filtre les éléments qui contiennent **les deux** classes.  
> * `[data-price]` → garantit que l'attribut existe, filtrant ainsi **les éléments par classe** **et** attribut en un seul appel.  
> * Le résultat est un `NodeList`, qui est une collection ordonnée que vous pouvez parcourir.

Si vous avez besoin de **select elements css selector** pour un autre motif, il suffit de changer la chaîne—aucune réécriture de code n'est nécessaire.

---

## Étape 3 – Parcourir le NodeList en Java

Un `NodeList` se comporte un peu comme un tableau, mais il n'implémente pas `Iterable`. C’est pourquoi nous utilisons une boucle `for` classique—parfaite pour les scénarios **iterate nodelist java**.

```java
        // Iterate over the selected elements
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
```

> **Pourquoi une boucle `for` ?**  
> Elle vous donne un accès direct à l'index, ce qui peut être pratique pour le journalisation ou le branchement conditionnel. Si vous préférez une boucle `while`, la logique reste identique—il suffit de changer la construction de la boucle.

---

## Étape 4 – Lire l'attribut `data-price`

Nous répondons enfin à **how to read attribute** à partir d'un élément. Dans l'API DOM, `getAttribute` renvoie la chaîne brute, exactement telle qu'elle apparaît dans le balisage.

```java
            // Read the price value from the data-price attribute
            String priceValue = productElement.getAttribute("data-price");
```

> **Astuce :** Si l'attribut peut être absent, `getAttribute` renvoie `null`. Vous pouvez vous en prémunir avec une simple vérification :

```java
            if (priceValue == null) {
                priceValue = "N/A"; // fallback for missing data-price
            }
```

---

## Étape 5 – Afficher les résultats

Enfin, nous imprimons chaque prix dans la console. Cela reflète un scénario réel où vous pousseriez probablement les valeurs dans une base de données ou une charge utile d'API.

```java
            // Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

### Sortie console attendue

```
Sale item price: 19.99
Sale item price: 34.50
Sale item price: 12.00
```

Si le sélecteur ne trouve aucun nœud correspondant, la boucle ne s'exécute tout simplement jamais—aucune exception n'est levée. C’est un filet de sécurité agréable pour les **edge cases** où le catalogue pourrait être vide.

---

## Exemple complet fonctionnel

En rassemblant le tout, voici le fichier complet que vous pouvez copier‑coller dans `CssSelectorDemo.java` :

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");

        // Step 2: Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );

        // Step 3 & 4: Iterate over the selected elements and read the price attribute
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
            String priceValue = productElement.getAttribute("data-price");
            if (priceValue == null) {
                priceValue = "N/A"; // fallback if attribute is missing
            }

            // Step 5: Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

Enregistrez le fichier, compilez‑le et exécutez‑le—regardez les prix défiler. 🎉

---

## Questions fréquentes & Astuces pro

| Question | Réponse |
|----------|---------|
| *Et si je dois aussi sélectionner par nom de balise ?* | Il suffit de préfixer la balise : `document.querySelectorAll("div.product-card.sale[data-price]")`. |
| *Puis‑je chaîner plusieurs filtres d'attributs ?* | Absolument. Exemple : `[data-price][data-stock]` ne gardera que les éléments qui possèdent **les deux** attributs. |
| *`querySelectorAll` est‑il sensible à la casse ?* | Oui—les sélecteurs CSS traitent les noms de classe et d'attribut comme sensibles à la casse en HTML5. |
| *Comment gérer un fichier HTML très volumineux ?* | Aspose.HTML diffuse le document, mais vous pouvez également limiter le sélecteur à un sous‑arbre (`someElement.querySelectorAll(...)`). |
| *What

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
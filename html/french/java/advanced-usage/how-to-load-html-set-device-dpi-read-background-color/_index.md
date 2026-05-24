---
category: general
date: 2026-02-16
description: Comment charger du HTML en Java, définir le DPI de l’appareil, spécifier
  une taille d’écran virtuelle et lire la couleur d’arrière‑plan calculée de n’importe
  quel élément.
draft: false
keywords:
- how to load html
- read background color
- set device dpi
- set virtual screen size
- get computed background color
language: fr
og_description: Comment charger du HTML en Java, définir le DPI de l’appareil, spécifier
  une taille d’écran virtuelle et lire la couleur d’arrière‑plan calculée de n’importe
  quel élément.
og_title: Comment charger du HTML, définir le DPI de l’appareil et lire la couleur
  d’arrière‑plan
tags:
- Aspose.HTML
- Java
title: Comment charger du HTML, définir le DPI de l’appareil et lire la couleur d’arrière-plan
url: /fr/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/
---

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment charger du HTML, définir le DPI de l'appareil et lire la couleur d'arrière‑plan

Vous vous êtes déjà demandé **comment charger du html** dans une application Java puis inspecter les styles de la page ? Vous n'êtes pas seul — les développeurs ont souvent besoin de rendre une page web hors‑écran, d’obtenir les valeurs CSS finales et de les utiliser pour la conversion en PDF, les captures d’écran ou même les tests automatisés.  

Dans ce guide, nous allons parcourir exactement cela : nous chargerons un fichier HTML, **définirons le DPI de l’appareil**, spécifierons une **taille d’écran virtuelle**, et enfin **lire la couleur d’arrière‑plan** de l’élément `<body>`. À la fin, vous disposerez d’un extrait complet et exécutable qui affiche la **couleur d’arrière‑plan calculée**—pas de mystère, juste du Java pur.

## Ce dont vous avez besoin

Avant de commencer, assurez‑vous d’avoir :

* Java 17 ou version supérieure (le code fonctionne avec n’importe quel JDK récent).  
* Aspose.HTML for Java 23.9 ou ultérieur—téléchargez le JAR depuis le site Aspose ou ajoutez‑le via Maven.  
* Un fichier HTML simple (par ex. `responsive.html`) qui définit une couleur d’arrière‑plan en CSS.

C’est tout—pas de frameworks supplémentaires, pas de pilotes de navigateur. Prêt ? C’est parti.

![Diagramme illustrant le chargement du HTML et l'extraction des styles calculés](/images/load-html-diagram.png){alt="Diagramme illustrant le chargement du HTML et l'extraction des styles calculés"}

## Étape 1 : Comment charger le HTML et configurer les options de rendu

La première chose à faire est de créer un objet `HtmlLoadOptions`. Cet objet indique à Aspose.HTML **comment charger le html**—y compris les dimensions de l’écran virtuel et le DPI que vous souhaitez émuler.

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create load options and define the virtual screen size and DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        // setVirtualScreenSize – width × height in CSS pixels
        loadOptions.setScreenSize(new Size(1280, 800));
        // setDeviceDpi – typical desktop DPI (96 is the default for most monitors)
        loadOptions.setDeviceDpi(96);
```

**Pourquoi c’est important :**  
Définir une taille d’écran virtuelle garantit que les media queries comme `@media (max-width: 600px)` se comportent comme si la page était rendue sur un vrai moniteur. Le DPI influence la façon dont les unités CSS `px` sont mappées aux pixels physiques—crucial lorsque vous générez ensuite des images ou des PDF.

## Étape 2 : Charger le fichier HTML avec les options configurées

Nous chargeons maintenant réellement le fichier. Notez que nous transmettons le même `loadOptions` que nous venons de configurer.

```java
        // 2️⃣ Load the HTML file with the options we just set.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);
```

Si le fichier n’est pas trouvé, Aspose lève une `FileNotFoundException` claire. En production, vous voudrez peut‑être entourer cela d’un try‑catch et revenir à une chaîne HTML par défaut.

## Étape 3 : Définir la taille d’écran virtuelle et le DPI de l’appareil (explicitement)

Même si nous avons déjà appelé `setScreenSize` et `setDeviceDpi` ci‑dessus, il vaut la peine de souligner que **définir la taille d’écran virtuelle** et **définir le DPI de l’appareil** peuvent être ajustés à tout moment avant le rendu. Par exemple, vous pourriez augmenter le DPI pour des captures d’écran haute résolution :

```java
        // 3️⃣ Adjust DPI for a high‑resolution render (optional).
        loadOptions.setDeviceDpi(300);   // 300 DPI is common for print‑ready images
        // 4️⃣ Change screen size for a mobile layout test.
        loadOptions.setScreenSize(new Size(375, 667)); // iPhone X viewport
```

N’oubliez pas de recharger le document si vous modifiez ces paramètres après le premier chargement—Aspose les considère comme immuables une fois le `Document` créé.

## Étape 4 : Lire la couleur d’arrière‑plan et obtenir la couleur d’arrière‑plan calculée

Avec le document en mémoire, vous pouvez interroger le style calculé de n’importe quel élément. Ici nous nous concentrons sur la balise `<body>`, mais la même approche fonctionne pour `<div>`, `<p>` ou même les pseudo‑éléments.

```java
        // 5️⃣ Retrieve the <body> element.
        Element bodyElement = document.getBody();

        // 6️⃣ Output the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

**Ce que vous verrez :** Si `responsive.html` contient `body { background: #ff5722; }`, la console affichera quelque chose comme :

```
Computed background color: rgba(255,87,34,1)
```

C’est le résultat de **get computed background color**—Aspose résout toutes les règles de cascade CSS, les media queries et même les déclarations `!important` avant de renvoyer la valeur finale.

## Exemple complet fonctionnel

En rassemblant le tout, voici le programme complet, prêt à copier‑coller :

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create load options – virtual screen size + DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        loadOptions.setScreenSize(new Size(1280, 800)); // set virtual screen size
        loadOptions.setDeviceDpi(96);                  // set device DPI (default desktop)

        // Optional: tweak for high‑resolution or mobile rendering.
        // loadOptions.setDeviceDpi(300);
        // loadOptions.setScreenSize(new Size(375, 667));

        // Step 2: Load the HTML document with the options.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);

        // Step 3: Grab the <body> element.
        Element bodyElement = document.getBody();

        // Step 4: Print the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

### Sortie attendue

```
Computed background color: rgba(255,255,255,1)
```

*(Les valeurs RGBA exactes dépendent du CSS présent dans votre fichier HTML.)*

## Pièges courants & astuces professionnelles

* **Paramètre DPI manquant ?** Aspose utilise par défaut 96 DPI, ce qui peut flouter les captures d’écran haute résolution. Définissez‑le toujours explicitement si vous avez besoin d’une sortie nette.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
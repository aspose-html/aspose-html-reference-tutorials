---
title: Ajuster la taille de la page XPS avec Aspose.HTML pour Java
linktitle: Réglage de la taille de la page XPS
second_title: Traitement HTML Java avec Aspose.HTML
description: Découvrez comment ajuster la taille des pages XPS avec Aspose.HTML pour Java. Contrôlez facilement les dimensions de sortie de vos documents XPS.
weight: 16
url: /fr/java/advanced-usage/adjust-xps-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajuster la taille de la page XPS avec Aspose.HTML pour Java


Dans ce didacticiel, nous vous guiderons tout au long du processus d'ajustement de la taille de la page XPS à l'aide d'Aspose.HTML pour Java. Cette puissante bibliothèque vous permet de manipuler des documents HTML et de les restituer dans différents formats, y compris XPS. L'ajustement de la taille de la page est essentiel lorsque vous devez contrôler les dimensions de sortie de votre document XPS.

## Prérequis

Avant de commencer, assurez-vous que les conditions préalables suivantes sont remplies :

1. Environnement de développement Java : assurez-vous que le kit de développement Java (JDK) est installé sur votre système.

2.  Bibliothèque Aspose.HTML pour Java : vous devez télécharger et inclure la bibliothèque Aspose.HTML pour Java dans votre projet Java. Vous pouvez trouver la bibliothèque[ici](https://releases.aspose.com/html/java/).

3. Fichier HTML d'entrée : préparez un fichier HTML que vous souhaitez restituer et dont vous souhaitez ajuster la taille de la page XPS. Vous pouvez utiliser votre propre fichier HTML pour ce didacticiel.

## Paquets d'importation

Tout d'abord, vous devez importer les packages nécessaires pour travailler avec Aspose.HTML pour Java. Incluez ces packages au début de votre classe Java :

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Étape 1 : définir le nom du fichier d’entrée

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

 Dans cette étape, nous lisons votre fichier d'entrée HTML à l'aide d'un`FileInputStream`.

## Étape 2 : créer un document HTML et définir des styles

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n";

// ...
```

 Cette étape consiste à créer un`HTMLDocument` et y ajouter des styles.

## Étape 3 : Créer des options de rendu XPS

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

Ici, nous créons des options de rendu XPS pour configurer le processus de rendu.

## Étape 4 : Ajuster la taille de la page

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

Cette étape consiste à définir la taille de la page et à spécifier si elle doit être ajustée à la page la plus large.

## Étape 5 : Rendre le résultat

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

Dans la dernière étape, nous rendons la sortie XPS en utilisant les options configurées.

## Conclusion

Dans ce didacticiel, nous vous avons montré comment ajuster la taille de la page XPS à l'aide d'Aspose.HTML pour Java. Vous pouvez contrôler les dimensions de sortie de vos documents XPS, en vous assurant qu'elles répondent à vos exigences spécifiques. Avec le code et les étapes fournis, vous pouvez facilement implémenter cette fonctionnalité dans vos applications Java.

 Si vous avez des questions ou avez besoin d'aide supplémentaire, n'hésitez pas à visiter le[Documentation d'Aspose.HTML pour Java](https://reference.aspose.com/html/java/) ou demandez de l'aide sur le[Forum Aspose](https://forum.aspose.com/).

## FAQ

### Q1 : Qu'est-ce qu'Aspose.HTML pour Java ?

A1 : Aspose.HTML pour Java est une bibliothèque Java qui permet aux développeurs de manipuler et de convertir des documents HTML dans divers formats, tels que XPS, PDF et images.

### Q2 : Où puis-je télécharger Aspose.HTML pour Java ?

 A2 : Vous pouvez télécharger la bibliothèque Aspose.HTML pour Java à partir de[ce lien](https://releases.aspose.com/html/java/).

### Q3 : Existe-t-il un essai gratuit disponible pour Aspose.HTML pour Java ?

 A3 : Oui, vous pouvez obtenir un essai gratuit d'Aspose.HTML pour Java à partir de[ici](https://releases.aspose.com/).

### Q4 : Comment puis-je obtenir une licence temporaire pour Aspose.HTML pour Java ?

 A4 : Pour obtenir une licence temporaire pour Aspose.HTML pour Java, visitez[cette page](https://purchase.aspose.com/temporary-license/).

### Q5 : Puis-je obtenir de l'aide pour Aspose.HTML pour Java ?

 A5 : Oui, vous pouvez demander de l'aide et du soutien à la communauté Aspose sur le[Forum Aspose](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---
title: Appliquer du CSS externe aux documents HTML dans Aspose.HTML pour Java
linktitle: Appliquer du CSS externe aux documents HTML dans Aspose.HTML pour Java
second_title: Traitement HTML Java avec Aspose.HTML
description: Découvrez comment appliquer du CSS externe à des documents HTML à l'aide d'Aspose.HTML pour Java ! Suivez ce guide étape par étape pour un tutoriel complet.
type: docs
weight: 12
url: /fr/java/editing-html-documents/apply-external-css-html-documents/
---
## Introduction
Lorsque vous travaillez avec des documents HTML, l'application de styles peut faire toute la différence en termes de présentation et d'expérience utilisateur. Si vous vous lancez dans Java et que vous souhaitez apprendre à appliquer des styles CSS externes à vos documents HTML à l'aide de la bibliothèque Aspose.HTML, vous êtes au bon endroit ! Ce guide vise à éclairer le processus étape par étape, le rendant facile même pour ceux qui sont nouveaux dans Java ou CSS.
## Prérequis
Avant de plonger dans le code, vous devez mettre en place quelques éléments :
### 1. Kit de développement Java (JDK)
 Assurez-vous que le JDK est installé sur votre machine. Vous pouvez télécharger la dernière version à partir de[Site Web Java d'Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).
### 2. Aspose.HTML pour Java
Vous devez avoir configuré Aspose.HTML pour Java. Si vous ne l'avez pas encore fait, rendez-vous sur le[Page de téléchargement d'Aspose](https://releases.aspose.com/html/java/) et prends la bibliothèque.
### 3. Un IDE ou un éditeur de texte
Choisissez un environnement de développement intégré (IDE) comme IntelliJ IDEA, Eclipse ou même un simple éditeur de texte pour écrire votre code Java.
### 4. Connaissances de base de Java
Une connaissance de la programmation Java et des bases CSS vous aidera certainement à suivre plus confortablement.
## Paquets d'importation
Une fois que vous avez tout configuré, l'étape suivante consiste à importer les packages nécessaires dans votre projet Java. Voici ce dont vous avez besoin :
```java
import com.aspose.html.HTMLDocument;
```
Ces importations vous permettront de manipuler des documents HTML et de les restituer dans différents formats, tels que PDF.

Nous allons décomposer notre tutoriel en étapes faciles à gérer. Chaque étape vous guidera tout au long du processus d'application de styles CSS externes à un document HTML à l'aide d'Aspose.HTML pour Java.
## Étape 1 : Créer un document HTML
Tout d'abord, nous devons créer notre document HTML. Nous commencerons par définir le contenu avec une structure HTML simple.
```java
String content = "<div><p>Internal CSS</p><p>An internal CSS is used to define a style for a single HTML page</p></div>";
HTMLDocument document = new HTMLDocument(content, ".");
```

 Ici, nous avons défini une structure HTML de base, comprenant un`<div>` avec deux paragraphes. Le`HTMLDocument` La classe est utilisée pour créer une représentation de document de notre contenu HTML.
## Étape 2 : Créer un élément de style
 Ensuite, nous allons créer un`style` élément pour contenir nos règles CSS.
```java
Element style = document.createElement("style");
style.setTextContent(".frame1 { margin-top:50px; margin-left:50px; padding:20px; width:360px; height:90px; background-color:#a52a2a; font-family:verdana; color:#FFF5EE;} \n" +
        ".frame2 { margin-top:-90px; margin-left:160px; text-align:center; padding:20px; width:360px; height:100px; background-color:#ADD8E6;}");
```

 En utilisant le`createElement` méthode de`HTMLDocument` , nous créons un nouveau`<style>` élément et définissez son contenu pour inclure nos définitions CSS pour deux classes :`frame1` et`frame2`Ces classes définissent les marges, le remplissage, les dimensions, les couleurs d'arrière-plan, les familles de polices et les couleurs de texte.
## Étape 3 : ajouter le style à l’en-tête du document
Maintenant que notre CSS est en place, nous devons ajouter notre élément de style à l'en-tête du document.
```java
Element head = document.getElementsByTagName("head").get_Item(0);
head.appendChild(style);
```

 Nous récupérons l'en-tête du document et ajoutons notre nouvellement créé`style` élément. Cette action intègre efficacement notre CSS dans le document HTML, lui permettant de styliser notre contenu HTML.
## Étape 4 : Appliquer des classes aux éléments HTML
Ensuite, nous appliquerons les classes CSS précédemment définies à nos éléments de paragraphe.
```java
HTMLElement paragraph = (HTMLElement) document.getElementsByTagName("p").get_Item(0);
paragraph.setClassName("frame1");
HTMLElement lastParagraph = (HTMLElement) document.getElementsByTagName("p").get_Item(document.getElementsByTagName("p").getLength() - 1);
lastParagraph.setClassName("frame2");
```

Ici, nous accédons aux premier et dernier éléments de paragraphe du document et leur attribuons les classes CSS que nous avons créées. Cette attribution garantit qu'ils adhèrent aux styles définis dans notre CSS.
## Étape 5 : définir des propriétés de style supplémentaires
Pour améliorer encore l'apparence, nous allons définir des propriétés de style supplémentaires pour nos paragraphes.
```java
paragraph.getStyle().setFontSize("250%");
paragraph.getStyle().setTextAlign("center");
lastParagraph.getStyle().setColor("#434343");
lastParagraph.getStyle().setFontSize("150%");
lastParagraph.getStyle().setFontFamily("verdana");
```

Dans cette étape, nous peaufinons nos styles. La taille de police du premier paragraphe est augmentée et centrée, tandis que la couleur, la taille de police et la famille de polices du dernier paragraphe sont définies. Ce raffinement est essentiel pour la lisibilité et l'attrait esthétique.
## Étape 6 : Enregistrer le document HTML
Une fois nos styles appliqués, il est temps d'enregistrer le document HTML.
```java
document.save("edit-internal-css.html");
```

 Ici, nous utilisons le`save` méthode de la`HTMLDocument` classe pour écrire le contenu HTML modifié dans un fichier, préservant ainsi nos styles et nos modifications.
## Étape 7 : Rendre le document au format PDF
Enfin, rendons le document au format PDF pour la sortie.
```java
PdfDevice device = new PdfDevice("edit-internal-css.pdf");
document.renderTo(device);
```

 En utilisant le`PdfDevice` classe, nous mettons en place le rendu de notre document HTML en PDF. Cette étape est essentielle lorsque vous souhaitez partager le document stylisé dans un format universellement accessible.
## Conclusion
Et voilà : appliquer du code CSS externe à des documents HTML à l'aide d'Aspose.HTML pour Java est à la fois simple et gratifiant ! Avec seulement quelques lignes de code, vous pouvez transformer du texte brut en documents visuellement attrayants et de style professionnel. Ainsi, que vous conceviez pour un usage personnel, créiez des rapports ou développiez du contenu Web, comprendre comment manipuler HTML et CSS en Java est une compétence puissante à avoir dans votre boîte à outils.
## FAQ
### Qu'est-ce qu'Aspose.HTML pour Java ?
Aspose.HTML pour Java est une bibliothèque puissante qui permet aux développeurs de travailler avec des documents HTML dans des applications Java, offrant une vaste gamme de fonctionnalités, de la manipulation HTML au rendu.
### Ai-je besoin d'une connexion Internet pour utiliser Aspose.HTML ?
Non, une fois que vous avez téléchargé les fichiers de bibliothèque nécessaires, vous pouvez utiliser Aspose.HTML hors ligne.
### Puis-je appliquer plusieurs fichiers CSS à un document HTML ?
 Oui, vous pouvez créer plusieurs`<link>` éléments et les ajouter à l'en-tête du document pour divers fichiers CSS.
### Existe-t-il une différence entre CSS interne et externe ?
Oui ! Le CSS interne est défini dans un document HTML, tandis que le CSS externe est placé dans un fichier séparé et lié au document.
### Comment puis-je obtenir de l'aide pour Aspose.HTML pour Java ?
 Vous pouvez accéder au soutien communautaire via le[Forum Aspose](https://forum.aspose.com/c/html/29) pour toute question ou problème que vous pourriez rencontrer.
---
title: Ajuster la taille de la page PDF avec Aspose.HTML pour Java
linktitle: Ajuster la taille de la page PDF
second_title: Traitement HTML Java avec Aspose.HTML
description: Découvrez comment ajuster la taille des pages PDF avec Aspose.HTML pour Java. Créez des PDF de haute qualité à partir de HTML sans effort. Contrôlez efficacement les dimensions des pages.
weight: 15
url: /fr/java/advanced-usage/adjust-pdf-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajuster la taille de la page PDF avec Aspose.HTML pour Java


À l'ère du numérique, la nécessité de générer des PDF de haute qualité à partir de contenu HTML est de plus en plus importante. Aspose.HTML pour Java est une puissante bibliothèque Java qui vous permet de convertir sans effort des documents HTML au format PDF. Dans ce didacticiel, nous nous concentrerons sur l'ajustement de la taille de la page lors de la conversion de HTML en PDF à l'aide d'Aspose.HTML pour Java.

## Prérequis

Avant de commencer, assurez-vous que les conditions préalables suivantes sont remplies :

- Environnement de développement Java : assurez-vous que le kit de développement Java (JDK) est installé sur votre système.
-  Aspose.HTML pour Java : vous devez télécharger et installer Aspose.HTML pour Java à partir du site Web[ici](https://releases.aspose.com/html/java/).
- Document HTML : vous devez disposer d'un document HTML prêt à être converti. Sinon, créez-en un ou utilisez un fichier HTML existant.

## Paquets d'importation

Pour commencer, vous devez importer les packages nécessaires pour travailler avec Aspose.HTML pour Java. L'extrait de code suivant montre comment procéder :

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

Maintenant que vous avez mis en place les conditions préalables et que vous avez importé les packages nécessaires, décomposons le processus d'ajustement de la taille de la page PDF en plusieurs étapes :

## Étape 1 : Lecture du contenu HTML

Tout d'abord, vous devez lire le contenu HTML que vous souhaitez convertir en PDF. Dans cet exemple, nous allons lire le code HTML à partir d'un fichier nommé « FirstFile.html ».

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## Étape 2 : Rédaction du contenu HTML

Ensuite, vous écrirez le contenu HTML dans un fichier nommé « FirstFileOut.html ».

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Ajoutez ici des styles ou du contenu HTML personnalisés
    String style = "<style>\n" +
                   ".st\n" +
                   "{\n" +
                   "color:\n" +
                   "green;\n" +
                   "}\n" +
                   "</style >\n" +
                   "<div id = id1 > Aspose.Html rendering Text in Black Color</div >\n" +
                   "<div id = id2 class='' st '' > Aspose.Html rendering Text in Green Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: blue;' > Aspose.Html rendering Text in Blue Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: red;' ><font face = 'Arial' > Aspose.Html rendering Text in Red\n" +
                   "Color</font ></div >\n";
    fileOutputStream.write(style.getBytes(java.nio.charset.StandardCharsets.UTF_8));
}
```

## Étape 3 : Conversion de HTML en PDF

Vous allez maintenant restituer le contenu HTML dans un fichier PDF. Nous aborderons deux scénarios : l'un où la taille de la page n'est pas ajustée à la largeur du contenu, et l'autre où elle est ajustée.

### Taille de la page non ajustée

Dans ce scénario, la taille de la page est définie sur une largeur et une hauteur fixes, ce qui peut recadrer le contenu s'il dépasse ces dimensions.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Créer une instance HTMLDocument à partir du fichier HTML
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Définir les options de rendu PDF
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Rendre le résultat
pdf_renderer.render(device, html_document);
```

### Taille de la page ajustée à la largeur du contenu

Dans ce scénario, la taille de la page est ajustée en fonction de la largeur du contenu.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Rendre le résultat
pdf_renderer.render(device, html_document);
```

## Conclusion

Dans ce didacticiel, nous avons exploré comment ajuster la taille de la page PDF lors de la conversion de HTML en PDF à l'aide d'Aspose.HTML pour Java. Vous avez appris les prérequis, importé les packages requis et suivi un guide étape par étape pour réaliser cette tâche. Avec Aspose.HTML pour Java, vous pouvez facilement contrôler la taille de la page de vos PDF générés, en vous assurant que votre contenu s'affiche comme prévu.

 N'hésitez pas à tester différentes tailles de page et différents paramètres pour répondre à vos besoins spécifiques. Si vous rencontrez des problèmes ou si vous avez d'autres questions, n'hésitez pas à demander de l'aide au[Documentation d'Aspose.HTML pour Java](https://reference.aspose.com/html/java/) ou le[Forum d'assistance Aspose](https://forum.aspose.com/).

## FAQ

### Q1 : Qu'est-ce qu'Aspose.HTML pour Java ?

A1 : Aspose.HTML pour Java est une bibliothèque Java qui vous permet de travailler avec des documents HTML, de les manipuler, de les convertir et de les restituer dans différents formats, y compris PDF.

### Q2 : Comment puis-je ajuster la taille de la page PDF lors de la conversion de HTML en PDF avec Aspose.HTML pour Java ?

 A2 : Vous pouvez ajuster la taille de la page PDF en utilisant le`PageSetup` classe et réglage de la`AdjustToWidestPage` propriété à`true` ou « faux », selon vos besoins.

### Q3 : Puis-je personnaliser le style du contenu HTML avant de le convertir en PDF ?

A3 : Oui, vous pouvez personnaliser le style en ajoutant des éléments CSS et HTML à votre contenu HTML avant de le convertir en PDF, comme démontré dans le didacticiel.

### Q4 : Où puis-je trouver la documentation d'Aspose.HTML pour Java ?

 A4 : Vous pouvez vous référer à la documentation[ici](https://reference.aspose.com/html/java/) pour des informations complètes et des exemples.

### Q5 : Existe-t-il un essai gratuit disponible pour Aspose.HTML pour Java ?

 A5 : Oui, vous pouvez accéder à un essai gratuit d'Aspose.HTML pour Java à partir de[ce lien](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

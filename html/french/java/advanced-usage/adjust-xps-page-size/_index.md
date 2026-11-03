---
date: 2026-08-28
description: Ajustez la taille de page XPS lors de la conversion de HTML en XPS en
  Java avec Aspose.HTML. Rendre le HTML en XPS avec des dimensions précises.
keywords:
- adjust xps page size
- render html to xps
- aspose.html java
- xps conversion java
- html to xps
lastmod: 2026-08-28
linktitle: Ajustement de la taille de page XPS
og_description: Ajustez la taille de page XPS lors de la conversion de HTML en XPS
  en Java avec Aspose.HTML. Apprenez à rendre le HTML en XPS avec des dimensions précises
  en quelques secondes.
og_image_alt: Tutorial showing how to adjust XPS page size during HTML to XPS conversion
  with Aspose.HTML for Java
og_title: Ajuster la taille de page XPS lors de la conversion de HTML en XPS en Java
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Adjust XPS page size while converting HTML to XPS in Java using Aspose.HTML.
    Render HTML to XPS with precise dimensions.
  headline: Adjust XPS page size when converting HTML to XPS in Java
  type: TechArticle
- description: Adjust XPS page size while converting HTML to XPS in Java using Aspose.HTML.
    Render HTML to XPS with precise dimensions.
  name: Adjust XPS page size when converting HTML to XPS in Java
  steps:
  - name: set the input file name
    text: The `FileInputStream` class reads raw bytes from a file, providing the HTML
      source to the renderer.
  - name: create an HTML document and set styles
    text: The `HTMLDocument` class represents an in‑memory HTML DOM used by Aspose.HTML
      for rendering.
  - name: create XPS rendering options
    text: The `XpsRenderingOptions` class holds settings that control how HTML is
      rendered to XPS, such as page size and image quality.
  - name: adjust the page size
    text: '**How to set XPS page size** – Define a custom page size (width × height
      in points) and tell the renderer whether it should automatically expand to the
      widest page. Setting `adjustToWidestPage` to `false` preserves the exact dimensions
      you specify. The `PageSetup` class defines page size, margins, a'
  - name: render the output
    text: The `XpsDevice` class is the rendering target that writes the processed
      content to an XPS file.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a Java library that allows developers to manipulate
      and convert HTML documents into various formats, such as XPS, PDF, and images.
      You can download the library from [Aspose.HTML for Java download page](https://releases.aspose.com/html/java/).
    question: What is Aspose.HTML for Java?
  - answer: You can download the Aspose.HTML for Java library from [Aspose product
      releases page](https://releases.aspose.com/).
    question: Where can I download Aspose.HTML for Java?
  - answer: Yes, you can get a free trial of Aspose.HTML for Java from the [temporary
      license request page](https://purchase.aspose.com/temporary-license/).
    question: Is there a free trial available for Aspose.HTML for Java?
  - answer: To get a temporary license for Aspose.HTML for Java, visit the [temporary
      license request page](https://purchase.aspose.com/temporary-license/).
    question: How can I obtain a temporary license for Aspose.HTML for Java?
  - answer: Yes, you can seek help and support from the Aspose community on the [Aspose
      Forum](https://forum.aspose.com/).
    question: Can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
tags:
- adjust xps page size
- Aspose.HTML
- Java XPS conversion
- HTML to XPS
- document rendering
title: Ajuster la taille de page XPS lors de la conversion de HTML en XPS en Java
url: /fr/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajuster la taille de la page XPS lors de la conversion de HTML en XPS en Java

Dans ce tutoriel, vous apprendrez **comment ajuster la taille de la page XPS** lors de la conversion de HTML en XPS avec Aspose.HTML for Java. Que vous ayez besoin de factures imprimables, de rapports d'archivage ou d'étiquettes de taille personnalisée, le contrôle des dimensions de la page garantit que le XPS final apparaît exactement comme prévu. Nous parcourrons la configuration de l'environnement, les options de rendu et la génération finale du XPS afin que vous puissiez intégrer cette fonctionnalité directement dans vos applications Java.

## Réponses rapides
- **Que signifie « convertir HTML en XPS » ?** Il rend un document HTML en un fichier XPS, en préservant la mise en page et le style.  
- **Ai-je besoin d'une licence ?** Un essai gratuit fonctionne pour le développement ; une licence commerciale est requise pour la production.  
- **Quelle version de Java est prise en charge ?** Java 8 ou supérieur (JDK 11+ recommandé).  
- **Puis-je modifier la taille de la page ?** Oui – Aspose.HTML vous permet de spécifier des dimensions personnalisées avant le rendu.  
- **Combien de temps prend la conversion ?** Typiquement moins d'une seconde pour les pages standard ; les documents plus volumineux peuvent prendre plus de temps.  

## Qu'est-ce que la conversion de HTML en XPS ?
Convertir HTML en XPS consiste à prendre un fichier de balisage orienté web et à produire un document XPS (XML Paper Specification) – un format à mise en page fixe, prêt à l'impression, similaire au PDF. Cela est utile lorsque vous avez besoin de documents haute fidélité, indépendants du dispositif, pour l'archivage ou l'impression depuis des applications Java.

## Pourquoi ajuster la taille de la page XPS ?
Ajuster la taille de la page XPS vous donne le contrôle sur les dimensions physiques du document final (par ex., A4, Letter, étiquettes personnalisées). Cela évite les mises à l'échelle indésirables, garantit que le contenu s'adapte parfaitement et peut réduire la taille du fichier en éliminant les espaces blancs inutiles.

## Comment rendre HTML en XPS avec une taille de page personnalisée ?
Chargez votre HTML, configurez `XpsRenderingOptions` avec un `PageSetup` qui définit la largeur et la hauteur exactes dont vous avez besoin, puis rendez vers un `XpsDevice`. Ce flux en deux étapes vous permet de conserver la mise en page intacte tout en imposant les dimensions que vous spécifiez, le tout en un seul appel d'API.

## Prérequis

Avant de commencer, assurez-vous d'avoir les prérequis suivants en place :

1. **Environnement de développement Java** – Java Development Kit (JDK) installé sur votre système.  
2. **Bibliothèque Aspose.HTML for Java** – Téléchargez et incluez la bibliothèque Aspose.HTML for Java dans votre projet. Vous pouvez trouver la bibliothèque [Page de téléchargement d'Aspose.HTML for Java](https://releases.aspose.com/html/java/).  
3. **Fichier HTML d'entrée** – Préparez un fichier HTML que vous souhaitez rendre et dont vous voulez ajuster la taille de page XPS. Vous pouvez utiliser votre propre fichier HTML pour ce tutoriel.  

## Importer les packages

La classe `Page` représente les dimensions et les paramètres de la page pour la sortie XPS. La classe `HtmlRenderer` effectue la conversion de HTML en XPS.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Guide étape par étape

Ci-dessous se trouve un guide concis, numéroté, qui reflète les étapes originales tout en ajoutant un contexte supplémentaire pour plus de clarté.

### Étape 1 : définir le nom du fichier d'entrée

La classe `FileInputStream` lit les octets bruts d'un fichier, fournissant la source HTML au moteur de rendu.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

### Étape 2 : créer un document HTML et définir les styles

La classe `HTMLDocument` représente un DOM HTML en mémoire utilisé par Aspose.HTML pour le rendu.

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
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n" +
               "\n";

// ...
```

### Étape 3 : créer les options de rendu XPS

La classe `XpsRenderingOptions` contient les paramètres qui contrôlent la façon dont le HTML est rendu en XPS, comme la taille de la page et la qualité de l'image.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

### Étape 4 : ajuster la taille de la page  

**Comment définir la taille de page XPS** – Définissez une taille de page personnalisée (largeur × hauteur en points) et indiquez au moteur de rendu s'il doit s'étendre automatiquement à la page la plus large. Définir `adjustToWidestPage` sur `false` préserve les dimensions exactes que vous spécifiez.

La classe `PageSetup` définit la taille de la page, les marges et l'orientation pour la sortie XPS.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

### Étape 5 : rendre la sortie

La classe `XpsDevice` est la cible de rendu qui écrit le contenu traité dans un fichier XPS.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Problèmes courants et solutions

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Sortie XPS vide** | Le flux d'entrée n'est pas fermé ou le HTMLDocument pointe vers le mauvais fichier. | Assurez-vous que le `FileInputStream` est correctement enveloppé dans un bloc try‑with‑resources et que le chemin du fichier est exact. |
| **Taille de page non appliquée** | `adjustToWidestPage` laissé à `true`. | Définissez `pageSetup.setAdjustToWidestPage(false);` comme indiqué à l'étape 4. |
| **CSS non pris en charge** | Aspose.HTML prend en charge un sous-ensemble de CSS. | Utilisez une mise en page, des polices et des couleurs de base ; évitez les sélecteurs avancés ou le CSS Grid. |
| **LicenseException** | Exécution sans licence valide en production. | Appliquez votre licence temporaire ou achetée avant le rendu (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Questions fréquemment posées

**Q : Qu'est-ce qu'Aspose.HTML for Java ?**  
R : Aspose.HTML for Java est une bibliothèque Java qui permet aux développeurs de manipuler et de convertir des documents HTML en divers formats, tels que XPS, PDF et images. Vous pouvez télécharger la bibliothèque depuis [Page de téléchargement d'Aspose.HTML for Java](https://releases.aspose.com/html/java/).

**Q : Où puis-je télécharger Aspose.HTML for Java ?**  
R : Vous pouvez télécharger la bibliothèque Aspose.HTML for Java depuis la [page des versions produit d'Aspose](https://releases.aspose.com/).

**Q : Existe-t-il un essai gratuit disponible pour Aspose.HTML for Java ?**  
R : Oui, vous pouvez obtenir un essai gratuit d'Aspose.HTML for Java depuis la [page de demande de licence temporaire](https://purchase.aspose.com/temporary-license/).

**Q : Comment obtenir une licence temporaire pour Aspose.HTML for Java ?**  
R : Pour obtenir une licence temporaire pour Aspose.HTML for Java, rendez-vous sur la [page de demande de licence temporaire](https://purchase.aspose.com/temporary-license/).

**Q : Puis-je obtenir du support pour Aspose.HTML for Java ?**  
R : Oui, vous pouvez demander de l'aide et du support à la communauté Aspose sur le [Forum Aspose](https://forum.aspose.com/).

**Q : Puis-je convertir HTML en XPS sur un serveur sans interface graphique ?**  
R : Absolument. Aspose.HTML fonctionne dans des environnements sans interface graphique ; assurez-vous simplement que le runtime Java est correctement configuré.

**Q : La bibliothèque prend-elle en charge les marges de page personnalisées ?**  
R : Oui. Utilisez `PageSetup.setMarginTop()`, `setMarginBottom()`, etc., avant d'assigner le `PageSetup` aux options de rendu.

## Conclusion

Nous avons parcouru le processus complet de **conversion de HTML en XPS** et **d'ajustement de la taille de la page XPS** avec Aspose.HTML for Java. En suivant ces étapes, vous pouvez générer des documents XPS prêts à l'impression qui correspondent exactement à vos exigences de mise en page. N'hésitez pas à expérimenter différentes dimensions de page, styles, ou même à ajouter des en-têtes et pieds de page pour répondre aux besoins de votre projet.

Si vous avez des questions ou avez besoin d'aide supplémentaire, consultez la [documentation Aspose.HTML for Java](https://reference.aspose.com/html/java/) ou rejoignez la conversation sur le [Forum Aspose](https://forum.aspose.com/).

---

**Dernière mise à jour :** 2026-08-28  
**Testé avec :** Aspose.HTML for Java 24.11 (dernière version au moment de la rédaction)  
**Auteur :** Aspose

## Tutoriels associés

- [Convertir HTML en XPS avec Aspose.HTML for Java](/html/java/conversion-html-to-other-formats/convert-html-to-xps/)
- [Ajuster la taille de page PDF avec Aspose.HTML for Java](/html/java/advanced-usage/adjust-pdf-page-size/)
- [Conversion d'EPUB en XPS avec Aspose.HTML for Java](/html/java/converting-epub-to-xps/convert-epub-to-xps/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
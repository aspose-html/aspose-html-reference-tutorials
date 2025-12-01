---
date: 2025-12-01
description: Apprenez à ajuster la taille des pages PDF, à rendre le HTML en PDF et
  à générer un PDF à partir du HTML en utilisant Aspose.HTML pour Java. Contrôlez
  facilement les dimensions des pages.
language: fr
linktitle: Adjusting PDF Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Ajuster la taille de la page PDF avec Aspose.HTML pour Java
url: /java/advanced-usage/adjust-pdf-page-size/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajuster la taille de la page PDF avec Aspose.HTML pour Java

Générer des PDF à partir de HTML est une exigence courante pour les rapports, factures et livres numériques. Lorsque vous **ajustez la taille de la page PDF**, vous vous assurez que le document final correspond à la mise en page que vous avez conçue en HTML. Dans ce tutoriel, vous apprendrez comment rendre du HTML en PDF, définir des dimensions personnalisées et contrôler si la page s’étend automatiquement à l’élément le plus large. Nous parcourrons un exemple complet, pratique, en utilisant Aspose.HTML pour Java.

## Réponses rapides
- **Que signifie « ajuster la taille de la page PDF » ?** Cela vous permet de définir la largeur et la hauteur de chaque page PDF ou de laisser le rendu s’ajuster automatiquement à l’élément le plus large.  
- **Quelle bibliothèque est utilisée ?** Aspose.HTML pour Java (dernière version).  
- **Ai‑je besoin d’une licence ?** Une version d’essai gratuite suffit pour le développement ; une licence commerciale est requise pour la production.  
- **Puis‑je modifier les dimensions par programme ?** Oui – utilisez `PageSetup` et la propriété `AdjustToWidestPage`.  
- **Est‑ce compatible avec Java 8+ ?** Absolument – l’API fonctionne avec tout JDK 8 ou supérieur.

## Qu’est‑ce que « ajuster la taille de la page PDF » ?
Ajuster la taille de la page PDF signifie configurer les dimensions de chaque page que le moteur de rendu HTML crée. Vous pouvez définir une taille fixe (par ex. A4, Letter) ou laisser le moteur calculer la largeur optimale en fonction du contenu. Cela vous donne un contrôle précis sur la mise en page, la pagination et la fidélité visuelle.

## Pourquoi ajuster la taille de la page PDF lors de la conversion HTML → PDF ?
- **Conserver l’intention de conception :** Empêcher le contenu d’être tronqué ou étiré.  
- **Optimiser pour l’impression :** Correspondre à la taille de papier requise par les processus en aval.  
- **Améliorer la lisibilité :** Éviter les espaces blancs excessifs ou le texte trop serré.  
- **Documents dynamiques :** Adapter automatiquement les tableaux ou images larges sans calculs manuels.

## Prérequis
Avant de commencer, assurez‑vous d’avoir :

- **Java Development Kit (JDK) 8 ou supérieur** installé sur votre machine.  
- **Aspose.HTML pour Java** – téléchargez le dernier JAR depuis la [page de version officielle](https://releases.aspose.com/html/java/).  
- **Un fichier HTML** que vous souhaitez convertir (nous utiliserons `FirstFile.html` dans l’exemple).  

## Importer les packages
Tout d’abord, importez les classes dont nous aurons besoin. Le bloc de code ci‑dessous est identique à celui du tutoriel original.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

## Étape 1 : Lire le contenu HTML
Nous lisons le fichier HTML source à l’aide d’un `FileInputStream`. Cette étape prépare le balisage brut pour une manipulation ultérieure.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## Étape 2 : Écrire (et éventuellement enrichir) le HTML
Ici nous copions le HTML original dans un nouveau fichier et injectons quelques styles en ligne pour montrer comment le style influence le rendu PDF. Remplacez librement le CSS d’exemple par le vôtre.

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Add custom HTML styles or content here
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

## Étape 3 : Rendre le HTML en PDF – Deux scénarios
Nous allons maintenant voir comment **générer un PDF à partir de HTML** avec deux stratégies de taille de page différentes.

### 3.1 Taille de page NON ajustée à la largeur du contenu
Dans ce cas nous fixons les dimensions de la page (100 × 100 points). Si un élément dépasse ces limites, il sera découpé.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Create an HTMLDocument instance from the HTML file
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Set PDF rendering options
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

### 3.2 Taille de page AJUSTÉE à la largeur du contenu
Ici nous activons `AdjustToWidestPage`, de sorte que le moteur étend automatiquement la largeur de la page pour accueillir l’élément le plus large tout en maintenant la hauteur fixe.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

## Comment définir les dimensions PDF (comment changer la taille de la page PDF) dans le code
L’objet `PageSetup` est la clé :

- `setAnyPage(Page page)` : définit la largeur × hauteur de base.  
- `setAdjustToWidestPage(boolean)` : active ou désactive l’élargissement automatique.  

En ajustant ces deux propriétés, vous pouvez **définir les dimensions PDF** pour n’importe quel scénario, que vous ayez besoin d’une page A4 statique ou d’une largeur dynamique qui suit votre mise en page HTML.

## Problèmes courants & astuces
| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| Le contenu est tronqué | La taille fixe est trop petite | Augmentez les valeurs de `Size` ou activez `AdjustToWidestPage`. |
| Le texte apparaît flou | La résolution DPI du rendu est basse par défaut | Utilisez `PdfRenderingOptions.setResolution(int dpi)` pour augmenter la qualité. |
| Les styles sont manquants | CSS externe non chargé | Intégrez le CSS en ligne ou utilisez `HTMLDocument.setBaseUrl()` pour pointer vers votre dossier de feuilles de style. |
| Les gros fichiers HTML provoquent OutOfMemoryError | Le moteur charge tout le document en mémoire | Traitez le document par morceaux ou augmentez le tas JVM (`-Xmx`). |

## Questions fréquentes

**Q : Qu’est‑ce qu’Aspose.HTML pour Java ?**  
R : C’est une bibliothèque Java qui vous permet de créer, modifier et rendre des documents HTML, y compris la conversion en PDF, PNG et autres formats.

**Q : Comment puis‑je ajuster la taille de la page PDF lors de la conversion HTML → PDF avec Aspose.HTML pour Java ?**  
R : Utilisez la classe `PageSetup` et définissez `AdjustToWidestPage` à `true` (auto‑taille) ou `false` (taille fixe). Puis attribuez la `Size` souhaitée via `new Page(new Size(width, height))`.

**Q : Puis‑je personnaliser le style du contenu HTML avant de le convertir en PDF ?**  
R : Oui – vous pouvez injecter du CSS, modifier le DOM ou utiliser des feuilles de style externes. Le tutoriel montre l’injection de CSS en ligne.

**Q : Où puis‑je trouver la documentation d’Aspose.HTML pour Java ?**  
R : La documentation complète est disponible [ici](https://reference.aspose.com/html/java/).

**Q : Existe‑t‑il une version d’essai gratuite pour Aspose.HTML pour Java ?**  
R : Absolument – téléchargez une version d’essai depuis la [page de version](https://releases.aspose.com/html/java/).

## Conclusion
Vous savez maintenant comment **ajuster la taille de la page PDF**, **rendre du HTML en PDF** et **définir des dimensions PDF personnalisées** avec Aspose.HTML pour Java. Expérimentez avec différentes tailles de page, réglages DPI et ajustements CSS pour obtenir le rendu parfait pour votre cas d’utilisation. En cas de difficulté, consultez la documentation officielle ou les forums de support Aspose.

---

**Dernière mise à jour :** 2025-12-01  
**Testé avec :** Aspose.HTML pour Java 24.12 (dernière version)  
**Auteur :** Aspose  
**Ressources associées :** [Référence API](https://reference.aspose.com/html/java/) | [Télécharger l’essai gratuit](https://releases.aspose.com/html/java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
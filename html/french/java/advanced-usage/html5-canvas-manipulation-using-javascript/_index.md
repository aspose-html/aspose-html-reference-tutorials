---
date: 2026-03-21
description: Apprenez à convertir un canvas en PDF en utilisant JavaScript et Aspose.HTML
  pour Java. Créez des graphiques dynamiques, dessinez du texte sur le canvas et exportez
  le HTML en PDF.
linktitle: Convert Canvas to PDF Using JavaScript
second_title: Java HTML Processing with Aspose.HTML
title: Convertir Canvas en PDF avec Aspose.HTML pour Java
url: /fr/java/advanced-usage/html5-canvas-manipulation-using-javascript/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir Canvas en PDF avec Aspose.HTML pour Java

Les expériences web interactives reposent souvent sur l'élément **Canvas** HTML5. En dessinant des graphiques avec JavaScript, vous pouvez créer des graphiques, des signatures ou des illustrations personnalisées directement dans le navigateur. Mais que faire si vous avez besoin d'une version imprimable et partageable de ce canvas ? Dans ce tutoriel, vous apprendrez **comment convertir canvas en PDF** en utilisant JavaScript avec **Aspose.HTML for Java**. Nous parcourrons la création d'un canvas, le dessin de texte, l'enregistrement du HTML, puis l'exportation du résultat vers un fichier PDF.

## Réponses rapides
- **Que signifie « convertir canvas en pdf » ?** Cela consiste à prendre le contenu visuel rendu sur un Canvas HTML5 et à générer un document PDF qui préserve cet aspect.  
- **Quelle bibliothèque gère la conversion ?** Aspose.HTML for Java fournit une API fiable côté serveur pour convertir du HTML (y compris Canvas) en PDF.  
- **Ai-je besoin d'un navigateur pour la conversion ?** Non. La conversion s'exécute sur le runtime Java, vous pouvez donc automatiser la génération de PDF sur un serveur ou dans un service backend.  
- **Puis-je dessiner du texte sur le canvas avant la conversion ?** Absolument – nous montrerons un exemple JavaScript simple qui écrit « Hello World » sur le canvas.  
- **Quelles sont les principales conditions préalables ?** Java JDK, bibliothèque Aspose.HTML for Java et un IDE Java (Eclipse, IntelliJ, etc.).  

## Qu’est‑ce que « convertir canvas en pdf » ?
Convertir un canvas en PDF signifie rendre le dessin basé sur les pixels provenant de l'élément `<canvas>` sous forme d'une page PDF adaptée aux vecteurs. Cela vous permet de conserver l'aspect exact du canvas tout en bénéficiant des fonctionnalités PDF telles que la pagination, le texte recherchable et le partage facile.

## Pourquoi utiliser Aspose.HTML pour Java pour cette tâche ?
- **Prise en charge complète de HTML5** – Canvas, CSS3 et JavaScript moderne s'exécutent correctement pendant la conversion.  
- **Traitement côté serveur** – Pas besoin de navigateur sans tête ; la bibliothèque gère le rendu en interne.  
- **Sortie PDF haute fidélité** – Les polices, les couleurs et la mise en page sont conservées avec précision.  
- **Multi‑plateforme** – Fonctionne sur tout système d'exploitation supportant Java.

## Prérequis
- **Java Development Kit (JDK)** – Java 8 ou supérieur.  
- **Aspose.HTML for Java** – Téléchargez depuis le site officiel [ici](https://releases.aspose.com/html/java/).  
- **IDE** – Eclipse, IntelliJ IDEA ou tout éditeur compatible Java.

Avec ces éléments en place, vous êtes prêt à commencer à créer et exporter des graphiques canvas.

## Importer les packages
Tout d'abord, importez les classes dont nous aurons besoin depuis Aspose.HTML et Java I/O.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.PdfSaveOptions;
import java.io.FileWriter;
```

## Pourquoi enregistrer le canvas en PDF ?
Enregistrer le canvas en PDF est idéal lorsque vous avez besoin d'une représentation statique, imprimable, de graphiques web dynamiques. Les PDF sont universellement lisibles, supportent le rendu haute résolution et peuvent être archivés ou envoyés par e‑mail sans perte de qualité.

## Étape 1 : Créer un élément Canvas et dessiner du texte

### 1.1 Préparer le HTML et le JavaScript (dessiner du texte sur le canvas)
Ci-dessous se trouve une chaîne Java contenant une page HTML simple avec un élément `<canvas>`. Le JavaScript intégré obtient le contexte du canvas, définit une police et dessine la phrase **« Hello World »**.

```java
String code = "<canvas id='myCanvas' width='200' height='100' style='border:1px solid #d3d3d3;'></canvas>\n" +
              "<script>\n" +
              "    var c = document.getElementById('myCanvas');\n" +
              "    var context = c.getContext('2d');\n" +
              "    context.font = '20px Arial';\n" +
              "    context.fillStyle = 'red';\n" +
              "    context.fillText('Hello World', 40, 50);\n" +
              "</script>\n";
```

### 1.2 Enregistrer le code HTML dans un fichier (conversion java html en pdf)
Nous écrivons la chaîne HTML dans `document.html`. Ce fichier sera ensuite chargé par Aspose.HTML.

```java
try (FileWriter fileWriter = new FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Initialiser un document HTML
Chargez le fichier HTML dans un objet `HTMLDocument` afin qu'Aspose.HTML puisse le traiter.

```java
HTMLDocument document = new HTMLDocument("document.html");
```

## Convertir le HTML (avec Canvas) en PDF
Enfin, utilisez la classe `Converter` pour transformer le document HTML en fichier PDF. Cette étape **enregistre le canvas en PDF** et complète le flux « convertir canvas en pdf ».

```java
try {
    Converter.convertHTML(
        document,
        new PdfSaveOptions(),
        "output.pdf"
    );
} finally {
    if (document != null) {
        document.dispose();
    }
}
```

### Résultat attendu
L'exécution du programme crée `output.pdf`. L'ouverture du PDF montre le texte rouge « Hello World » exactement comme il apparaissait sur le canvas dans la page HTML d'origine.

## Comment générer un PDF à partir d’un canvas avec Java
Le processus de conversion présenté ci‑dessus est un exemple simple de **générer pdf à partir de canvas**. Vous pouvez l'étendre en ajoutant plusieurs canvases, en les stylisant avec du CSS ou en incorporant des images. Le moteur Aspose.HTML rendra tout cela dans un seul document PDF.

## Problèmes courants et dépannage
- **Canvas non rendu dans le PDF** – Assurez‑vous d'utiliser une version récente d'Aspose.HTML qui prend pleinement en charge le Canvas HTML5.  
- **Polices manquantes** – Si la police n'est pas incorporée, le PDF peut revenir à une police par défaut. Utilisez `PdfSaveOptions` pour incorporer les polices si nécessaire.  
- **Chemins de fichiers** – Les chemins relatifs fonctionnent lorsque le processus Java s'exécute depuis le même répertoire que `document.html`. Sinon, fournissez un chemin absolu.

## Questions fréquentes

**Q : Qu’est‑ce qu’Aspose.HTML for Java ?**  
R : Aspose.HTML for Java est une bibliothèque puissante qui permet aux développeurs de créer, manipuler et convertir des documents HTML dans des applications Java, en prenant en charge les fonctionnalités HTML5 comme Canvas.

**Q : Puis‑je l’utiliser dans des projets commerciaux ?**  
R : Oui, une licence commerciale est requise pour une utilisation en production. Les détails sont disponibles sur la [page d'achat](https://purchase.aspose.com/buy).

**Q : Existe‑t‑il une version d’essai gratuite ?**  
R : Absolument. Vous pouvez télécharger une version d'essai depuis [ici](https://releases.aspose.com/).

**Q : Comment obtenir une licence temporaire pour les tests ?**  
R : Les licences temporaires sont fournies à des fins d'évaluation via le lien [ici](https://purchase.aspose.com/temporary-license/).

**Q : Où trouver une documentation détaillée ?**  
R : La référence complète de l'API est disponible [ici](https://reference.aspose.com/html/java/).

## Conclusion
Vous disposez maintenant d’une solution complète, de bout en bout, pour **convertir canvas en PDF** en utilisant JavaScript et Aspose.HTML for Java. En dessinant sur le canvas, en enregistrant le HTML et en appelant l'API de conversion, vous pouvez générer des PDF de haute qualité qui capturent tous les graphiques dynamiques que vous créez sur le web. Expérimentez avec différentes formes, couleurs et même des animations (capturées sous forme de séries d'images) pour élargir les possibilités de vos applications web soutenues par Java.

Si vous rencontrez des difficultés ou souhaitez explorer des fonctionnalités avancées, n’hésitez pas à visiter le [forum Aspose.HTML](https://forum.aspose.com/) pour obtenir le soutien de la communauté.

---

**Dernière mise à jour :** 2026-03-21  
**Testé avec :** Aspose.HTML for Java 24.11  
**Auteur :** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
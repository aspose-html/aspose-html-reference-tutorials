---
date: 2025-11-29
description: Apprenez à convertir du HTML en XPS et à ajuster la taille de la page
  XPS à l'aide d'Aspose.HTML pour Java. Contrôlez facilement les dimensions de sortie.
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Convertir HTML en XPS et ajuster la taille de la page XPS avec Aspose.HTML
  pour Java
url: /fr/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir HTML en XPS et ajuster la taille de page XPS avec Aspose.HTML pour Java

Dans ce tutoriel, vous découvrirez **comment convertir HTML en XPS** et ajuster finement la taille de page résultante à l’aide d’Aspose.HTML pour Java. Que vous génériez des rapports imprimables, des factures ou des documents d’archivage, contrôler les dimensions XPS garantit que la sortie apparaît exactement comme vous le souhaitez. Nous parcourrons chaque étape — de la configuration de l’environnement au rendu du fichier XPS final — afin que vous puissiez intégrer cette fonctionnalité dans vos applications Java dès maintenant.

## Réponses rapides
- **Que signifie « convertir HTML en XPS » ?** Cela rend un document HTML sous forme de fichier XPS, en préservant la mise en page et le style.  
- **Ai‑je besoin d’une licence ?** Une version d’essai gratuite suffit pour le développement ; une licence commerciale est requise en production.  
- **Quelle version de Java est prise en charge ?** Java 8 ou supérieur (JDK 11+ recommandé).  
- **Puis‑je changer la taille de la page ?** Oui – Aspose.HTML vous permet de spécifier des dimensions personnalisées avant le rendu.  
- **Combien de temps dure la conversion ?** Généralement moins d’une seconde pour des pages standards ; les documents plus volumineux peuvent prendre plus de temps.

## Qu’est‑ce que la conversion de HTML en XPS ?
Convertir HTML en XPS consiste à prendre un fichier de balisage orienté web et à produire un document XPS (XML Paper Specification) – un format à mise en page fixe, prêt à l’impression, similaire au PDF. Cela est utile lorsque vous avez besoin de documents haute fidélité, indépendants du dispositif, pour l’archivage ou l’impression depuis des applications Java.

## Pourquoi ajuster la taille de page XPS ?
Ajuster la taille de page vous donne le contrôle sur les dimensions physiques du document final (par ex. A4, Letter, étiquettes personnalisées). Cela évite les mises à l’échelle indésirables, assure que le contenu s’ajuste parfaitement et peut réduire la taille du fichier en éliminant les espaces blancs inutiles.

## Prérequis

Avant de commencer, assurez‑vous d’avoir les prérequis suivants :

1. **Environnement de développement Java** – Kit de développement Java (JDK) installé sur votre système.  
2. **Bibliothèque Aspose.HTML pour Java** – Téléchargez et incluez la bibliothèque Aspose.HTML pour Java dans votre projet. Vous pouvez la trouver [ici](https://releases.aspose.com/html/java/).  
3. **Fichier HTML d’entrée** – Préparez un fichier HTML que vous souhaitez rendre et dont vous voulez ajuster la taille de page XPS. Vous pouvez utiliser votre propre fichier HTML pour ce tutoriel.

## Importer les packages

Tout d’abord, importez les classes dont vous aurez besoin. Ces packages vous donnent accès à la manipulation de documents, au rendu et aux fonctionnalités de configuration de page.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Étape 1 : Définir le nom du fichier d’entrée

Lisez le fichier HTML source à l’aide d’un `FileInputStream`. Ce flux alimente le HTML brut dans le moteur Aspose.HTML.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

## Étape 2 : Créer un document HTML et définir les styles

Créez une instance `HTMLDocument` qui représente le contenu que vous allez rendre. Dans cet exemple, nous injectons également un petit bloc CSS pour illustrer le style – remplacez‑le par votre propre balisage si vous le souhaitez.

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

## Étape 3 : Créer les options de rendu XPS

Instanciez `XpsRenderingOptions` pour contenir tous les paramètres qui influencent la conversion de HTML en XPS.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

## Étape 4 : Ajuster la taille de page

Définissez une taille de page personnalisée (largeur × hauteur en points) et indiquez au moteur s’il doit s’étendre automatiquement à la page la plus large. Mettre `adjustToWidestPage` à `false` préserve exactement les dimensions que vous spécifiez.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

## Étape 5 : Rendre la sortie

Enfin, créez un `XpsDevice` avec les options configurées et rendez le document HTML. Le résultat est un fichier XPS complet avec les dimensions de page personnalisées que vous avez définies.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Problèmes courants et solutions

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Sortie XPS vide** | Le flux d’entrée n’est pas fermé ou le `HTMLDocument` pointe vers le mauvais fichier. | Assurez‑vous que le `FileInputStream` est correctement encapsulé dans un bloc try‑with‑resources et que le chemin du fichier est exact. |
| **Taille de page non appliquée** | `adjustToWidestPage` laissé à `true`. | Définissez `pageSetup.setAdjustToWidestPage(false);` comme indiqué à l’étape 4. |
| **CSS non pris en charge** | Aspose.HTML ne supporte qu’un sous‑ensemble de CSS. | Limitez‑vous aux mises en page, polices et couleurs de base ; évitez les sélecteurs avancés ou le CSS Grid. |
| **LicenseException** | Exécution sans licence valide en production. | Appliquez votre licence temporaire ou achetée avant le rendu (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Foire aux questions

**Q : Qu’est‑ce qu’Aspose.HTML pour Java ?**  
R : Aspose.HTML pour Java est une bibliothèque Java qui permet aux développeurs de manipuler et de convertir des documents HTML en divers formats, tels que XPS, PDF et images.

**Q : Où puis‑je télécharger Aspose.HTML pour Java ?**  
R : Vous pouvez télécharger la bibliothèque Aspose.HTML pour Java depuis [ce lien](https://releases.aspose.com/html/java/).

**Q : Existe‑t‑il une version d’essai gratuite pour Aspose.HTML pour Java ?**  
R : Oui, vous pouvez obtenir une version d’essai gratuite d’Aspose.HTML pour Java [ici](https://releases.aspose.com/).

**Q : Comment obtenir une licence temporaire pour Aspose.HTML pour Java ?**  
R : Pour obtenir une licence temporaire, rendez‑vous sur [cette page](https://purchase.aspose.com/temporary-license/).

**Q : Puis‑je obtenir du support pour Aspose.HTML pour Java ?**  
R : Oui, vous pouvez demander de l’aide et du support à la communauté Aspose sur le [Forum Aspose](https://forum.aspose.com/).

**Q : Puis‑je convertir HTML en XPS sur un serveur sans interface graphique ?**  
R : Absolument. Aspose.HTML fonctionne dans des environnements sans GUI ; assurez‑vous simplement que le runtime Java est correctement configuré.

**Q : La bibliothèque prend‑elle en charge les marges de page personnalisées ?**  
R : Oui. Utilisez `PageSetup.setMarginTop()`, `setMarginBottom()`, etc., avant d’assigner le `PageSetup` aux options de rendu.

## Conclusion

Nous avons parcouru le processus complet de **conversion de HTML en XPS** et d’ajustement de la taille de page avec Aspose.HTML pour Java. En suivant ces étapes, vous pouvez générer des documents XPS prêts à l’impression qui correspondent exactement à vos exigences de mise en page. N’hésitez pas à expérimenter avec différentes dimensions de page, styles, ou même à ajouter des en‑têtes et pieds de page pour répondre aux besoins de votre projet.

Si vous avez des questions ou besoin d’assistance supplémentaire, consultez la [documentation Aspose.HTML pour Java](https://reference.aspose.com/html/java/) ou rejoignez la conversation sur le [Forum Aspose](https://forum.aspose.com/).

---

**Dernière mise à jour :** 2025-11-29  
**Testé avec :** Aspose.HTML pour Java 24.11 (dernière version au moment de la rédaction)  
**Auteur :** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
---
date: 2025-12-05
description: Apprenez à définir les marges d’une page HTML en Java avec Aspose.HTML,
  et à ajouter des numéros de page et des titres à vos documents.
linktitle: CSS Extensions - Adding Title and Page Number
second_title: Java HTML Processing with Aspose.HTML
title: Comment définir les marges d’une page HTML en Java avec Aspose.HTML
url: /fr/java/advanced-usage/css-extensions-adding-title-page-number/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment définir les marges de page HTML en Java avec Aspose.HTML

Dans ce tutoriel, vous découvrirez **comment définir les marges de page HTML en Java** à l'aide d'Aspose.HTML pour Java. Nous parcourrons la création de marges de page personnalisées, l'insertion de numéros de page et l'ajout d'un titre de document — le tout avec du code clair, étape par étape, que vous pouvez copier dans votre propre projet.

## Réponses rapides
- **Quelle bibliothèque est nécessaire ?** Aspose.HTML for Java  
- **Puis-je contrôler les marges par programme ?** Oui, via une règle CSS `@page` dans la feuille de style utilisateur  
- **Quels formats de sortie prennent en charge les marges ?** XPS, PDF et d'autres formats raster  
- **Ai‑je besoin d'une licence pour la production ?** Une licence valide d'Aspose.HTML est requise pour une utilisation non‑d'essai  
- **Cette fonctionnalité est‑elle compatible avec Java 11+ ?** Absolument – la bibliothèque fonctionne avec les versions modernes de Java  

## Qu’est‑ce que « Définir les marges de page HTML en Java » ?
Définir les marges de page HTML en Java signifie configurer le moteur de rendu (fourni par Aspose.HTML) pour appliquer les propriétés CSS de boîte de page avant que le document ne soit converti en un format imprimable tel que XPS ou PDF. En définissant une règle `@page` personnalisée, vous contrôlez la zone imprimable, les numéros de page et le contenu d’en‑tête/pied de page.

## Pourquoi utiliser Aspose.HTML pour le contrôle des marges ?
- **Mise en page précise** – CSS `@page` vous offre un contrôle pixel‑par‑pixel des marges, en‑têtes et pieds de page.  
- **Cohérence multi‑format** – Les mêmes définitions de marge fonctionnent pour XPS, PDF et les sorties image.  
- **Aucune dépendance au navigateur** – Le rendu se fait côté serveur, vous n’avez donc pas besoin d’un navigateur sans tête.  

## Prérequis

Avant de commencer, assurez‑vous d’avoir les prérequis suivants :

1. **Environnement de développement Java** – JDK 11 ou version ultérieure installé.  
2. **Aspose.HTML for Java** – Téléchargez et installez la bibliothèque depuis [here](https://releases.aspose.com/html/java/).  

## Importer les packages

Pour commencer, importez les classes Aspose.HTML nécessaires :

```java
// Import Aspose.HTML packages
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

## Comment définir les marges de page HTML en Java – Guide étape par étape

### Étape 1 : Initialiser la configuration et définir les marges de page personnalisées

```java
// Initialize configuration object and set up the page-margins for the document
Configuration configuration = new Configuration();
try {
    // Get the User Agent service
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Set the style of custom margins and create marks on it
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

Dans ce bloc, nous créons un objet `Configuration`, obtenons le service `IUserAgentService` et injectons une règle CSS `@page` qui définit les marges, un compteur de page en bas à droite et un titre de document centré en haut.

### Étape 2 : Créer le document HTML

```java
// Initialize an HTML document
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Ici, nous instancions un `HTMLDocument` avec un extrait simple « Hello World ». La même configuration de l’Étape 1 est appliquée, de sorte que les marges personnalisées sont respectées lors du rendu du document.

### Étape 3 : Rendre vers un fichier XPS (ou toute sortie prise en charge)

```java
// Initialize an output device
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    // Send the document to the output device
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

Cette étape crée un `XpsDevice` qui écrit les pages rendues dans `output.xps`. Les marges, numéros de page et titre que vous avez définis précédemment apparaîtront dans le fichier final.

## Problèmes courants & astuces

- **Les marges semblent inchangées** – Assurez‑vous que la règle `@page` n’est pas écrasée par d’autres feuilles de style. L’appel `setUserStyleSheet` la force à la priorité la plus élevée.  
- **Les numéros de page affichent « NaN »** – Vérifiez que vous utilisez Aspose.HTML version 23.10 ou plus récente ; les versions antérieures ne disposent pas de la fonction `currentPageNumber()`.  
- **Le fichier de sortie est vide** – Confirmez que le chemin `Resources.output` est résolu correctement et que vous disposez des droits d’écriture.  

## Questions fréquemment posées

### Q1 : Qu’est‑ce qu’Aspose.HTML pour Java ?

**R :** Aspose.HTML pour Java est une bibliothèque Java qui fournit des outils puissants pour travailler avec des documents HTML dans les applications Java, incluant la conversion, le rendu et la manipulation.

### Q2 : Puis‑je personnaliser davantage les marges de page ?

**R :** Oui, il suffit de modifier le CSS à l’intérieur de `setUserStyleSheet`. Vous pouvez changer n’importe quelle valeur `margin-*` ou ajouter des boîtes supplémentaires `@top-*` / `@bottom-*`.

### Q3 : Comment ajouter plus de contenu au document HTML ?

**R :** Remplacez la chaîne dans `new HTMLDocument("<div>Hello World!!!</div>", …)` par votre propre balisage HTML, ou chargez un fichier externe en utilisant le constructeur `HTMLDocument(String url, …)`.

### Q4 : Aspose.HTML pour Java est‑il compatible avec d’autres formats de document ?

**R :** Absolument. Le même `HTMLDocument` peut être rendu en PDF, XPS, images, ou même EPUB en changeant le dispositif de sortie (par ex., `PdfDevice`, `PngDevice`).

### Q5 : Ai‑je besoin d’une licence pour utiliser Aspose.HTML pour Java ?

**R :** Oui, une licence est requise pour une utilisation en production. Vous pouvez obtenir une version d’essai ou acheter une licence depuis [here](https://purchase.aspose.com/buy) ou [here](https://releases.aspose.com/).

### Q6 : Comment définir des marges différentes pour les pages impaires et paires ?

**R :** Utilisez les pseudo‑classes `@page :left` et `@page :right` dans votre feuille de style pour définir des marges distinctes pour les pages de gauche (paires) et de droite (impaires).

### Q7 : Puis‑je intégrer des polices personnalisées dans le document rendu ?

**R :** Oui. Ajoutez des règles `@font-face` à la feuille de style utilisateur et faites référence aux polices dans votre contenu HTML.

## Conclusion

Vous avez maintenant maîtrisé **comment définir les marges de page HTML en Java** à l’aide d’Aspose.HTML, et vous savez comment ajouter des numéros de page et un titre pour rendre vos documents professionnels. N’hésitez pas à expérimenter avec des boîtes `@page` supplémentaires, des polices personnalisées ou différents formats de sortie pour répondre aux besoins de votre projet.

Si vous rencontrez des difficultés, la documentation officielle [Aspose.HTML for Java](https://reference.aspose.com/html/java/) et le [forum de support Aspose](https://forum.aspose.com/) sont d’excellents endroits pour obtenir de l’aide.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Dernière mise à jour :** 2025-12-05  
**Testé avec :** Aspose.HTML for Java 23.12  
**Auteur :** Aspose  

---
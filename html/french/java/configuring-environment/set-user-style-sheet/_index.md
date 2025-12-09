---
date: 2025-12-05
description: Apprenez à créer un PDF à partir de HTML en définissant une feuille de
  style utilisateur personnalisée dans Aspose.HTML pour Java, et convertissez facilement
  le HTML en PDF avec le service User Agent.
linktitle: Set User Style Sheet in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Créer un PDF à partir de HTML – Définir la feuille de style utilisateur dans
  Aspose.HTML pour Java
url: /fr/java/configuring-environment/set-user-style-sheet/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF à partir de HTML – Définir la feuille de style utilisateur dans Aspose.HTML pour Java

## Introduction
Dans ce tutoriel, vous apprendrez comment **créer un PDF à partir de HTML** en utilisant Aspose.HTML pour Java tout en appliquant une feuille de style utilisateur personnalisée.  
Vous êtes déjà arrivé à vouloir ajuster l’apparence de vos documents HTML avec votre propre style unique ? Imaginez que vous créez une page web et que vous avez besoin que les titres ressortent avec une couleur spécifique ou que les paragraphes restent cohérents sur tous les appareils. C’est là qu’interviennent une *feuille de style utilisateur* et le **User Agent Service**. Nous parcourrons chaque étape — de l’écriture d’un fichier HTML simple, à la configuration du user agent, jusqu’à la **conversion du HTML en PDF** — pour que vous puissiez voir le résultat immédiatement.

## Quick Answers
- **Que signifie « créer un PDF à partir de HTML » ?** Cela consiste à rendre un document HTML (avec CSS, images, polices, etc.) et à enregistrer le rendu visuel sous forme de fichier PDF.  
- **Quel composant Aspose est requis ?** La bibliothèque Aspose.HTML pour Java fournit le moteur de conversion et le User Agent Service.  
- **Ai‑je besoin d’une licence pour les tests ?** Une version d’essai gratuite suffit pour le développement ; une licence commerciale est requise en production.  
- **Puis‑je utiliser un fichier CSS externe ?** Oui – vous pouvez lier des feuilles de style externes comme dans un navigateur classique.  
- **Combien de temps dure la conversion ?** Pour un document simple comme celui de ce guide, la conversion s’effectue en moins d’une seconde.

## Prerequisites
Avant de plonger dans le code, assurez‑vous de disposer de :

1. **Aspose.HTML pour Java** – téléchargez le JAR le plus récent depuis la [page des releases Aspose](https://releases.aspose.com/html/java/).  
2. **Java Development Kit (JDK) 8+** – vérifiez que `java -version` renvoie 8 ou une version supérieure.  
3. **IDE** – IntelliJ IDEA, Eclipse ou NetBeans conviendront parfaitement.  
4. **Connaissances de base en HTML/CSS** – utiles mais pas obligatoires.

## Import Packages
Pour commencer, importez les classes Java essentielles. La seule importation explicite nécessaire pour cet exemple est `java.io.IOException` ; les classes Aspose sont référencées avec leurs noms pleinement qualifiés plus tard.

```java
import java.io.IOException;
```

## Step 1: Create a Simple HTML Document
Tout d’abord, nous allons écrire un fichier HTML minimal (`document.html`) qui servira de source pour la conversion en PDF.

```java
String code = "<h1>User Agent Service</h1>\r\n" +
        "<p>The User Agent Service allows you to specify a custom user stylesheet, a primary character set for the document, language, and fonts settings.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Astuce :** Conservez le fichier HTML dans le même répertoire que votre source Java afin d’éviter les problèmes de chemin.

## Step 2: Set Up Aspose.HTML Configuration
Créez un objet `Configuration`. Cet objet agit comme un conteneur pour tous les services (y compris le User Agent Service) que vous utiliserez ultérieurement.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Step 3: Access the User Agent Service  
Le **User Agent Service** vous permet d’injecter une feuille de style personnalisée, de définir le jeu de caractères par défaut et de contrôler d’autres options de rendu.

```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

## Step 4: Define and Apply the User Stylesheet  
Nous fournissons maintenant les règles CSS qui styliseront le HTML lors du rendu. C’est ici que nous **utilisons le service d’agent utilisateur** pour définir la feuille de style.

```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; font-size:2em; }\r\n" +
        "p { background-color:GhostWhite; color:SlateGrey; font-size:1.2em; }\r\n");
```

> **Pourquoi c’est important :** En appliquant une feuille de style au niveau de l’agent utilisateur, vous garantissez que les styles sont respectés même si le HTML d’origine ne fait pas référence à un fichier CSS.

## Step 5: Load the HTML Document with the Custom Configuration  
Passez à la fois le chemin du fichier et l’instance `Configuration` au constructeur `HTMLDocument`. Cela lie la feuille de style utilisateur au document.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
```

## Step 6: Convert HTML to PDF  
Une fois le document entièrement stylisé, invoquez la méthode statique `convertHTML` pour **convertir le HTML en PDF**. L’objet `PdfSaveOptions` vous permet d’ajuster finement la sortie (par ex., taille de page, compression).

```java
com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.PdfSaveOptions(),
        "user-agent-stylesheet_out.pdf"
);
```

> **Résultat :** `user-agent-stylesheet_out.pdf` contiendra le titre en brun et le paragraphe avec un arrière‑plan GhostWhite, exactement comme défini dans la feuille de style.

## Step 7: Clean Up Resources  
Libérez toujours les objets Aspose afin de libérer la mémoire native.

```java
if (document != null) {
    document.dispose();
}
if (configuration != null) {
    configuration.dispose();
}
```

## Common Issues & Solutions
| Problème | Cause | Solution |
|----------|-------|----------|
| **PDF vide** | Aucune feuille de style appliquée ou document non chargé avec la configuration. | Vérifiez que `configuration` est passé à `HTMLDocument` et que `setUserStyleSheet` est appelé avant le chargement. |
| **Avertissement de propriété CSS non prise en charge** | Aspose.HTML ne supporte pas certaines fonctionnalités CSS avancées. | Utilisez uniquement les propriétés CSS répertoriées dans la documentation Aspose.HTML ou revenez à des styles plus simples. |
| **FileNotFoundException** | Chemin incorrect vers `document.html`. | Utilisez un chemin absolu ou placez le fichier HTML à la racine du projet. |

## Frequently Asked Questions

**Q : Puis‑je appliquer des styles différents à différents éléments HTML ?**  
R : Absolument ! Vous pouvez définir autant de règles CSS que nécessaire dans la feuille de style utilisateur.

**Q : Que faire si je dois changer la feuille de style dynamiquement ?**  
R : Appelez à nouveau `setUserStyleSheet` avant de créer une nouvelle instance `HTMLDocument` ; les nouveaux styles seront appliqués lors de la prochaine conversion.

**Q : Est‑il possible d’utiliser des fichiers CSS externes avec Aspose.HTML pour Java ?**  
R : Oui – vous pouvez soit lier une feuille de style externe dans le HTML, soit charger son contenu et le transmettre à `setUserStyleSheet`.

**Q : Comment Aspose.HTML gère‑t‑il les propriétés CSS non prises en charge ?**  
R : Les propriétés non prises en charge sont ignorées, permettant au reste de la feuille de style de se rendre sans erreurs.

**Q : Puis‑je convertir le HTML vers d’autres formats que le PDF ?**  
R : Oui, Aspose.HTML prend en charge la conversion vers XPS, TIFF, PNG, JPEG, et bien d’autres en utilisant la classe `SaveOptions` appropriée.

## Conclusion
Vous avez maintenant vu comment **créer un PDF à partir de HTML** en définissant une feuille de style utilisateur personnalisée avec Aspose.HTML pour Java. Ce flux de travail vous donne un contrôle total sur l’apparence visuelle du PDF généré, ce qui le rend idéal pour la génération automatisée de rapports, la création de factures ou tout scénario où une mise en forme cohérente est cruciale. N’hésitez pas à expérimenter avec des CSS plus complexes, des polices externes ou des formats de conversion supplémentaires pour étendre cette base.

---

**Dernière mise à jour :** 2025-12-05  
**Testé avec :** Aspose.HTML pour Java 24.11 (dernière version au moment de la rédaction)  
**Auteur :** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
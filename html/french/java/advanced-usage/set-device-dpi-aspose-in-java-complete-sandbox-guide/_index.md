---
category: general
date: 2026-06-16
description: Apprenez à définir le DPI de l’appareil avec Aspose et à fixer la largeur
  et la hauteur du viewport lors du rendu HTML avec le bac à sable Aspose.HTML en
  Java. Un code étape par étape est inclus.
draft: false
keywords:
- set device dpi aspose
- set viewport width height
language: fr
og_description: Découvrez comment définir le DPI de l'appareil avec Aspose et définir
  la largeur et la hauteur du viewport en utilisant le bac à sable Aspose.HTML pour
  Java. Code complet et explication.
og_title: Définir le DPI de l'appareil Aspose en Java – Guide complet du bac à sable
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to set device dpi aspose and set viewport width height when
    rendering HTML with Aspose.HTML sandbox in Java. Step‑by‑step code included.
  headline: set device dpi aspose in Java – Complete Sandbox Guide
  type: TechArticle
- description: Learn how to set device dpi aspose and set viewport width height when
    rendering HTML with Aspose.HTML sandbox in Java. Step‑by‑step code included.
  name: set device dpi aspose in Java – Complete Sandbox Guide
  steps:
  - name: Configure sandbox options (including DPI and viewport size).
    text: Configure sandbox options (including DPI and viewport size).
  - name: Instantiate a `DocumentSandbox` with those options.
    text: Instantiate a `DocumentSandbox` with those options.
  - name: Load an external HTML page inside the sandbox.
    text: Load an external HTML page inside the sandbox.
  - name: Perform a simple DOM operation—printing the page title.
    text: Perform a simple DOM operation—printing the page title.
  type: HowTo
tags:
- Aspose.HTML
- Java
- HTML rendering
- Sandbox
title: Définir le DPI de l’appareil Aspose en Java – Guide complet du bac à sable
url: /fr/java/advanced-usage/set-device-dpi-aspose-in-java-complete-sandbox-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# définir le DPI de l'appareil aspose – Tutoriel Sandbox Java

Vous êtes-vous déjà demandé comment **définir le DPI de l'appareil aspose** lors du rendu d'une page web en Java ? Vous n'êtes pas le seul. De nombreux développeurs se heurtent à un mur lorsqu'ils ont besoin que la page rendue ressemble exactement à ce qu'elle serait sur un écran réel—surtout lorsque le DPI influence les calculs de mise en page.  

Dans ce guide, nous vous accompagnons à travers un exemple pratique qui non seulement **définit le DPI de l'appareil aspose**, mais montre également comment **définir la largeur et la hauteur du viewport** afin que la page se comporte comme dans une fenêtre de navigateur de 1280 × 800 pixels. À la fin, vous disposerez d’un extrait exécutable, d’une explication claire de chaque étape, et de conseils pour éviter les pièges courants.

## Ce que couvre ce tutoriel

Nous commencerons par présenter les prérequis, puis nous plongerons dans quatre étapes concises :

1. Configurer les options du sandbox (y compris le DPI et la taille du viewport).  
2. Instancier un `DocumentSandbox` avec ces options.  
3. Charger une page HTML externe à l’intérieur du sandbox.  
4. Effectuer une opération DOM simple — afficher le titre de la page.

Vous verrez pourquoi chaque élément est important, comment ajuster les paramètres pour différents appareils, et à quoi doit ressembler la sortie. Aucun document externe n’est nécessaire ; tout ce dont vous avez besoin se trouve ici.

## Prérequis

- Java 8 ou supérieur (la bibliothèque Aspose.HTML for Java prend en charge JDK 8+).  
- JARs Aspose.HTML for Java ajoutés au classpath de votre projet.  
- Un IDE ou un outil de construction (Maven/Gradle) pour compiler et exécuter le code.  
- Accès Internet si vous prévoyez de charger une URL en direct comme `https://example.com`.

Si ces points sont cochés, lançons‑nous.

## Étape 1 : Définir le DPI de l'appareil aspose – Configurer les options du sandbox

La première chose à faire est d’indiquer au sandbox quel « écran » vous simulez. C’est là que **définir le DPI de l'appareil aspose** entre en jeu. Le DPI (dots per inch) influence la façon dont les unités CSS `px` sont interprétées, ce qui peut modifier la taille des polices, le redimensionnement des images et les media queries.

```java
// Step 1: Create sandbox options and configure DPI and viewport.
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setDeviceDpi(96);               // set device dpi aspose
sandboxOptions.setViewportWidth(1280);         // set viewport width height
sandboxOptions.setViewportHeight(800);         // set viewport width height
```

> **Pourquoi c’est important :**  
> *L’appel `setDeviceDpi` indique à Aspose.HTML de considérer un pixel CSS comme 1/96 de pouce, reproduisant ainsi la plupart des moniteurs de bureau. Si vous omettez cela, la mise en page peut apparaître trop petite ou trop grande sur des écrans à DPI élevé.*

## Étape 2 : Créer le sandbox avec les options configurées

Une fois les options prêtes, vous avez besoin d’une instance de sandbox qui les respecte. Pensez au sandbox comme à un petit moteur de navigateur isolé qui n’interagit pas avec votre système de fichiers.

```java
// Step 2: Initialise the DocumentSandbox using the options above.
DocumentSandbox documentSandbox = new DocumentSandbox(sandboxOptions);
```

> **Astuce :**  
> Réutiliser le même `DocumentSandbox` pour plusieurs pages permet d’économiser de la mémoire, mais n’oubliez pas de réinitialiser les options si vous devez changer de DPI ou de viewport plus tard.

## Étape 3 : Charger un document HTML dans le sandbox

Avec le sandbox en place, le chargement d’une page est simple. Le constructeur de `HTMLDocument` accepte l’URL et le sandbox que vous venez de créer.

```java
// Step 3: Load a remote HTML page using the sandbox.
HTMLDocument htmlDoc = new HTMLDocument("https://example.com", documentSandbox);
```

> **Cas particulier :**  
> Si le site cible bloque les requêtes automatisées, vous pourriez obtenir une erreur 403. Dans ce cas, téléchargez le HTML localement et chargez‑le depuis un chemin de fichier, ou définissez une chaîne d’agent‑utilisateur personnalisée via `sandboxOptions`.

## Étape 4 : Effectuer des opérations DOM normales – Afficher le titre de la page

À ce stade, la page est entièrement rendue dans le sandbox, donc toute requête DOM fonctionne exactement comme dans un navigateur complet. Restons simples et récupérons le titre.

```java
// Step 4: Access the DOM – print the page title.
System.out.println("Title: " + htmlDoc.getTitle());
```

**Sortie attendue**

```
Title: Example Domain
```

Si vous obtenez autre chose, revérifiez que l’URL est accessible et que vous n’avez pas accidentellement modifié les valeurs de DPI ou de viewport.

## Pourquoi définir la largeur et la hauteur du viewport est crucial

Vous vous demandez peut‑être : « Pourquoi **définir la largeur et la hauteur du viewport** du tout ? » La réponse réside dans le design réactif. Les media queries comme `@media (max-width: 600px)` réagissent aux dimensions du viewport, pas à la taille physique de l’écran. En spécifiant `1280` × `800`, vous garantissez que la page rend le layout « desktop », même si vous exécutez le code sur un serveur sans affichage.

```java
sandboxOptions.setViewportWidth(1280);   // set viewport width height
sandboxOptions.setViewportHeight(800);   // set viewport width height
```

Modifier ces nombres vous permet de simuler des tablettes, des téléphones ou même des moniteurs ultra‑larges sans quitter votre IDE.

## Exemple complet fonctionnel

Voici la classe Java complète, prête à être exécutée, qui réunit tous les éléments. Copiez‑collez‑la dans un fichier nommé `SandboxExample.java`, ajoutez les JARs Aspose.HTML au classpath, puis lancez `javac SandboxExample.java && java SandboxExample`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.sandbox.SandboxOptions;

public class SandboxExample {
    public static void main(String[] args) {
        // Step 1: Define sandbox options – set device DPI and viewport.
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setDeviceDpi(96);               // set device dpi aspose
        sandboxOptions.setViewportWidth(1280);         // set viewport width height
        sandboxOptions.setViewportHeight(800);         // set viewport width height

        // Step 2: Create a DocumentSandbox using the defined options.
        DocumentSandbox documentSandbox = new DocumentSandbox(sandboxOptions);

        // Step 3: Load an HTML document inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com", documentSandbox);

        // Step 4: Perform normal DOM operations – print the page title.
        System.out.println("Title: " + htmlDoc.getTitle());
    }
}
```

> **Vérification rapide :**  
> Exécutez le programme. Si vous voyez `Title: Example Domain`, tout est correctement configuré. Sinon, examinez la console pour détecter les exceptions — la plupart des problèmes proviennent de JARs manquants ou de restrictions réseau.

## Pièges courants & comment les éviter

| Symptôme | Cause probable | Solution |
|---|---|---|
| `NullPointerException` sur `htmlDoc.getTitle()` | Le sandbox n’a pas chargé la page | Vérifiez l’URL, ajoutez un try‑catch autour du constructeur `HTMLDocument`, ou activez la journalisation via `sandboxOptions.setLogLevel(...)`. |
| La mise en page apparaît zoomée | DPI mal configuré | Assurez‑vous que `sandboxOptions.setDeviceDpi(96)` (ou le DPI cible). |
| Les media queries ne se déclenchent jamais | Dimensions du viewport manquantes | Vérifiez que vous avez appelé à la fois `setViewportWidth` **et** `setViewportHeight`. |
| Erreur de mémoire insuffisante sur de grandes pages | Réutilisation d’un même sandbox pour de nombreuses pages lourdes | Créez un nouveau `DocumentSandbox` par page ou appelez `documentSandbox.dispose()` après usage. |

## Extendre l’exemple

Maintenant que vous savez comment **définir le DPI de l'appareil aspose** et **définir la largeur et la hauteur du viewport**, vous pouvez aller plus loin :

- **Capturer une capture d’écran** de la page rendue avec `htmlDoc.renderToBitmap(...)`.  
- **Injecter du CSS personnalisé** avant le rendu pour tester les thèmes sombre.  
- **Exécuter du JavaScript** dans le sandbox avec `htmlDoc.getWindow().eval(...)`.  

Toutes ces actions respectent le DPI et le viewport que vous avez configurés, vous offrant un terrain de test fiable pour les mises en page réactives.

## Conclusion

Nous venons de parcourir une solution concise, de bout en bout, qui montre comment **définir le DPI de l'appareil aspose** et **définir la largeur et la hauteur du viewport** à l’aide du sandbox Aspose.HTML en Java. Vous disposez désormais d’une base solide pour rendre des pages exactement comme elles apparaîtraient sur n’importe quel appareil, le tout depuis un environnement sûr et isolé.

Prêt pour l’étape suivante ? Essayez de rendre une page qui utilise une grille CSS, ou chargez une feuille de style distante et observez comment le DPI influence le rendu des polices. Le sandbox vous donne la liberté d’expérimenter sans impacter votre système hôte.

Si vous rencontrez des difficultés, laissez un commentaire ci‑dessous ou consultez la documentation Aspose.HTML for Java—bien que tout ce dont vous avez besoin soit déjà présenté ici. Bon codage !  

![set device dpi aspose sandbox diagram](https://example.com/images/set-device-dpi-aspose.png "Diagram showing DPI and viewport configuration in Aspose.HTML sandbox")


## Que devez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos projets.

- [Create PDF from HTML using Aspose.HTML for Java – Sandbox](/html/english/java/configuring-environment/implement-sandboxing/)
- [Create PDF from HTML – Set User Style Sheet in Aspose.HTML for Java](/html/english/java/configuring-environment/set-user-style-sheet/)
- [How to Set Charset in Aspose.HTML for Java](/html/english/java/configuring-environment/set-character-set/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
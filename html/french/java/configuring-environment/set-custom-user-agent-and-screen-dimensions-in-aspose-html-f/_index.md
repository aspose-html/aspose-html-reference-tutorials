---
category: general
date: 2026-09-29
description: Définissez un agent utilisateur personnalisé dans Aspose.HTML pour Java
  et apprenez comment définir la taille d'écran virtuelle pour un rendu HTML précis.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom user agent
- set virtual screen size
- specify user agent
- set screen dimensions
- set screen width
language: fr
lastmod: 2026-09-29
og_description: Définissez un agent utilisateur personnalisé dans Aspose.HTML pour
  Java et apprenez comment définir la taille d’écran virtuelle pour un rendu HTML
  précis.
og_image_alt: Diagram showing how to set custom user agent and screen dimensions in
  a Java sandbox
og_title: Définir un agent utilisateur personnalisé et les dimensions de l'écran dans
  Aspose.HTML pour Java
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Set custom user agent in Aspose.HTML for Java and learn how to set
    virtual screen size for accurate HTML rendering.
  headline: Set custom user agent and screen dimensions in Aspose.HTML for Java
  type: TechArticle
tags:
- Aspose.HTML
- Java
- sandbox
- user agent
- screen size
title: Définir un agent utilisateur personnalisé et les dimensions de l'écran dans
  Aspose.HTML pour Java
url: /fr/java/configuring-environment/set-custom-user-agent-and-screen-dimensions-in-aspose-html-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Définir un agent utilisateur personnalisé et les dimensions d'écran dans Aspose.HTML pour Java

Si vous devez **définir un agent utilisateur personnalisé** lors du rendu HTML avec Aspose.HTML pour Java, ce guide vous montre exactement comment le faire. En configurant un sandbox, vous obtenez également la possibilité de **définir la taille d'écran virtuelle**, garantissant que la mise en page correspond à la fenêtre d'affichage d'un vrai navigateur.

Vous terminerez ce tutoriel avec un programme complet et exécutable qui **spécifie l'agent utilisateur**, **définit la largeur de l'écran** et **définit la hauteur de l'écran**. Aucun outil externe n'est requis — uniquement Aspose.HTML pour Java et un runtime Java 8+.

## Ce que vous allez apprendre

* Comment créer un `SandboxConfiguration` pour isoler le rendu.
* Comment **définir un agent utilisateur personnalisé** et pourquoi c'est important pour les pages réactives.
* Comment **définir la taille d'écran virtuelle** (largeur et hauteur) pour une mise en page précise.
* Comment charger un fichier HTML dans le sandbox et enregistrer le résultat traité.
* Pièges courants et conseils de bonnes pratiques pour le rendu en sandbox.

> **Prérequis** – Vous avez besoin d'une licence valide d'Aspose.HTML pour Java, de Java 8 ou plus récent, et d'un IDE (IntelliJ IDEA, Eclipse ou VS Code). L'exemple utilise un fichier local `input.html`, mais n'importe quelle URL accessible fonctionne.

![Diagramme du flux du sandbox](sandbox-flow.png "exemple de définition d'un agent utilisateur personnalisé en Java")

## Étape 1 : Créer une configuration sandbox (la base)

Le sandbox isole l'environnement de rendu de la JVM hôte, ce qui est essentiel lorsque vous souhaitez **définir un agent utilisateur personnalisé** ou modifier la taille de la fenêtre d'affichage.

```java
import com.aspose.html.sandbox.SandboxConfiguration;

// Create a fresh sandbox configuration object
SandboxConfiguration sandboxConfig = new SandboxConfiguration();
```

*Pourquoi cette étape ?*  
`SandboxConfiguration` contient toutes les options de rendu, y compris les **dimensions d'écran** et les chaînes **user‑agent**. En la configurant avant de charger le document, vous garantissez que le moteur HTML respecte ces paramètres dès la première requête.

## Étape 2 : Définir les dimensions d'écran pour imiter un appareil réel

Les sites réactifs lisent souvent `window.innerWidth` et `window.innerHeight`. Pour faire croire au moteur qu'il s'exécute sur un écran de 1024 × 768, vous **définissez la taille d'écran virtuelle** :

```java
// Define the virtual screen size for the sandboxed document
sandboxConfig.setScreenWidth(1024);   // set screen width
sandboxConfig.setScreenHeight(768);   // set screen height
```

*Pourquoi c'est important* – Si vous omettez **définir les dimensions d'écran**, le rendu peut utiliser une petite fenêtre d'affichage par défaut, ce qui fait que les media queries CSS choisissent la mise en page mobile. En définissant explicitement **la largeur de l'écran** et **la hauteur de l'écran**, vous contrôlez quelles règles CSS sont appliquées.

## Étape 3 : Spécifier une chaîne d'agent utilisateur personnalisée

Certaines pages web livrent un contenu différent selon l'en-tête user‑agent. Pour **spécifier l'agent utilisateur**, il suffit de le définir dans la configuration du sandbox :

```java
// Set a custom user‑agent string that will be sent during resource loading
sandboxConfig.setUserAgent("AsposeHTML/1.0");
```

*Pourquoi utiliser un agent utilisateur personnalisé ?*  
Une chaîne personnalisée peut contourner la détection de bots, déclencher des fonctionnalités réservées aux ordinateurs de bureau, ou tester le comportement d'un site pour une version de navigateur spécifique. Le moteur Aspose transmet cette valeur avec chaque requête HTTP effectuée lors du chargement des ressources externes (CSS, images, scripts).

## Étape 4 : Charger le document HTML à l'intérieur du sandbox

Maintenant que le sandbox est entièrement configuré, chargez le fichier HTML. Le constructeur qui accepte un chemin de fichier et un `SandboxConfiguration` applique automatiquement tous les paramètres que nous avons définis.

```java
import com.aspose.html.HTMLDocument;

// Load the HTML file using the previously configured sandbox
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);
```

Si vous devez charger depuis une URL distante, remplacez le chemin du fichier par la chaîne URL — Aspose.HTML respectera toujours le **agent utilisateur personnalisé défini** et les **dimensions d'écran**.

## Étape 5 : Enregistrer la sortie traitée

Après le chargement complet du document, vous pouvez l'enregistrer dans n'importe quel format supporté. Ici nous écrivons un fichier HTML sandboxé qui reflète les modifications du DOM causées par les paramètres personnalisés.

```java
// Save the processed document to the desired output location
document.save("YOUR_DIRECTORY/sandboxed_output.html");
```

Le fichier enregistré contiendra le même balisage, mais tout script qui a interrogé `navigator.userAgent` ou inspecté `window.innerWidth` verra désormais les valeurs que vous avez fournies.

## Exemple complet et exécutable

En combinant toutes les étapes, vous obtenez un programme autonome que vous pouvez copier, coller et exécuter.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.SandboxConfiguration;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox configuration to isolate the rendering environment
        SandboxConfiguration sandboxConfig = new SandboxConfiguration();

        // Step 2: Define the virtual screen size for the sandboxed document
        sandboxConfig.setScreenWidth(1024);   // set screen width
        sandboxConfig.setScreenHeight(768);   // set screen height

        // Step 3: Set a custom user‑agent string to be used during loading
        sandboxConfig.setUserAgent("AsposeHTML/1.0"); // set custom user agent

        // Step 4: Load the HTML document within the sandbox using the configuration
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);

        // Step 5: Save the processed document to the desired output location
        document.save("YOUR_DIRECTORY/sandboxed_output.html");
    }
}
```

### Résultat attendu

L'exécution du programme crée `sandboxed_output.html`. Si vous l'ouvrez dans un navigateur et inspectez `navigator.userAgent` via la console, vous verrez **AsposeHTML/1.0**. De même, `window.innerWidth` affichera **1024**, confirmant que les **dimensions d'écran définies** ont fonctionné comme prévu.

## Questions fréquentes & gestion des cas limites

| Question | Réponse |
|----------|--------|
| **Et si la page charge des ressources supplémentaires depuis un domaine différent ?** | Le sandbox transmet le **user‑agent personnalisé** avec chaque requête, mais les politiques de même origine restent appliquées. Utilisez `sandboxConfig.setAllowCrossDomain(true)` si vous devez assouplir ces restrictions. |
| **Puis-je modifier la taille de l'écran après le chargement du document ?** | Non. Les dimensions d'écran sont lues lors du premier passage de mise en page. Pour rendre avec une taille différente, créez un nouveau `SandboxConfiguration` et rechargez le document. |
| **Dois‑je appeler `document.close()` ?** | Le `HTMLDocument` implémente `AutoCloseable`. Utiliser un bloc try‑with‑resources assure un nettoyage correct, mais l'appel explicite à `close()` est optionnel dans les scripts simples. |
| **En quoi cela diffère‑t‑il de la définition d'un user‑agent dans un client HTTP ?** | Définir le user‑agent sur le sandbox affecte **toutes** les requêtes de ressources effectuées par le moteur HTML, pas seulement le téléchargement initial du HTML. Cela imite plus fidèlement un vrai navigateur. |
| **Le sandbox est‑il sûr pour du HTML non fiable ?** | Oui. Le sandbox isole l'accès au système de fichiers et limite les appels réseau selon la configuration, réduisant le risque que des scripts malveillants affectent votre JVM hôte. |

## Astuces professionnelles

* **Réutiliser les configurations** – Si vous rendez de nombreuses pages avec le même viewport, créez un seul `SandboxConfiguration` et réutilisez‑le pour éviter le surcoût de création d'objets.
* **Déboguer avec les logs** – Activez la journalisation d'Aspose.HTML (`sandboxConfig.setLogLevel(LogLevel.DEBUG)`) pour voir quelles ressources ont été récupérées avec le user‑agent personnalisé.
* **Combiner avec les media queries CSS** – En ajustant **la largeur de l'écran**, vous pouvez tester le comportement de votre design réactif sur tablettes, téléphones ou grands écrans de bureau sans ouvrir de vrai navigateur.

## Conclusion

Vous savez maintenant comment **définir un agent utilisateur personnalisé** et **définir les dimensions d'écran** lors du rendu HTML avec Aspose.HTML pour Java. En configurant un sandbox, vous isolez l'environnement, contrôlez le viewport et assurez que les ressources externes voient exactement les en‑têtes que vous spécifiez. Cette technique est essentielle pour tester les mises en page réactives, contourner les blocages de bots ou reproduire des fonctionnalités réservées aux ordinateurs de bureau dans des pipelines automatisés.

Ensuite, vous pourriez explorer **comment définir des cookies personnalisés** ou **capturer des captures d'écran rendues** en utilisant l'API de rendu d'Aspose.HTML — les deux concepts s'appuient sur le même modèle de configuration sandbox que vous venez de maîtriser.

Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Rendu haute DPI en Java – Capturer des captures d'écran de pages Web avec un agent utilisateur personnalisé](/html/english/java/conversion-html-to-various-image-formats/high-dpi-rendering-in-java-capture-webpage-screenshots-with/)
- [Comment charger du HTML, définir le DPI de l'appareil et lire la couleur d'arrière‑plan](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Créer un fichier HTML Java & configurer le service réseau (Aspose.HTML)](/html/english/java/configuring-environment/setup-network-service/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
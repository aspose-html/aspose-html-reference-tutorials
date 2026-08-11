---
category: general
date: 2026-02-11
description: Créer un document HTML en Java avec Aspose.HTML. Apprenez comment récupérer
  le JSON JavaScript, ajouter un élément script, générer du HTML à partir du JSON
  et convertir le JSON en pre.
draft: false
keywords:
- create html document
- fetch json javascript
- add script element
- generate html from json
- convert json to pre
language: fr
og_description: Créez un document HTML en Java avec Aspose.HTML. Récupérez le JSON
  JavaScript, ajoutez un élément script, générez du HTML à partir du JSON et convertissez
  le JSON en balise pre — le tout dans un seul tutoriel.
og_title: Créer un document HTML en Java – Guide complet
tags:
- Aspose.HTML
- Java
- Web Automation
title: Créer un document HTML avec Java – Récupérer le JSON et générer le contenu
url: /fr/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un document HTML – Tutoriel complet Java

Vous avez déjà eu besoin de **créer un document HTML** à la volée mais vous ne saviez pas comment y intégrer des données distantes ? Vous n'êtes pas seul. Dans de nombreux projets, vous souhaiterez récupérer du JSON avec JavaScript, injecter le résultat dans une page, puis enregistrer le balisage final sous forme de fichier statique. Ce guide vous montre exactement comment faire cela en utilisant Aspose.HTML pour Java.

Nous parcourrons chaque étape : de l’instanciation d’un document vide, à **fetch JSON JavaScript**, à **add script element**, et enfin à **generate HTML from JSON** et **convert JSON to pre**. À la fin, vous disposerez d’un fichier `fetchResult.html` prêt à l’emploi contenant les données récupérées affichées sous forme de JSON joliment formaté.

## Prérequis

- Java 17 ou plus récent (le code compile également avec JDK 11+)
- Bibliothèque Aspose.HTML for Java (disponible via Maven Central)
- Familiarité de base avec HTML et JavaScript asynchrone
- Un IDE ou la simple ligne de commande `javac`/`java`

Aucun cadre supplémentaire n’est requis—tout s’exécute localement.

## Étape 1 : Configurer le projet et importer Aspose.HTML

Tout d’abord, ajoutez la dépendance Aspose.HTML à votre `pom.xml` (ou téléchargez le JAR manuellement).

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- latest as of Feb 2026 -->
</dependency>
```

> **Astuce :** Gardez le numéro de version à jour ; les nouvelles versions corrigent des bugs et améliorent le moteur de script.

## Étape 2 : **Create HTML Document** – la toile vierge

Nous commençons par créer un `HTMLDocument` vide. Considérez-le comme une page vierge où nous déposerons plus tard notre script.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.scripting.*;

public class JsFetchExample {
    public static void main(String[] args) throws Exception {

        // Step 2: Create an empty HTML document that will host the script
        HTMLDocument htmlDoc = new HTMLDocument();
```

Pourquoi avons‑nous besoin d’un objet document ? Le `ScriptEngine` d’Aspose.HTML travaille sur un DOM, pas sur une chaîne brute. En construisant un document approprié, nous offrons au moteur un environnement réel pour exécuter notre **fetch JSON JavaScript**.

## Étape 3 : Écrire l’extrait JavaScript – **Fetch JSON JavaScript** et **Convert JSON to pre**

Le cœur du tutoriel réside dans cette chaîne multilignes. Elle effectue un `fetch` asynchrone, analyse le JSON, puis écrit un élément `<pre>` contenant les données formatées de façon lisible.

```java
        // Step 3: Define a JavaScript snippet that fetches JSON data and injects it into the page
        String fetchScript = """
            (async function() {
                const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
                const data = await response.json();
                // Convert JSON to <pre> for readable formatting
                document.body.innerHTML = '<pre>' + JSON.stringify(data, null, 2) + '</pre>';
            })();
            """;
```

Remarquez le commentaire *Convert JSON to <pre>* – c’est exactement ce que fait l’appel `JSON.stringify(..., null, 2)`. Il ajoute de l’indentation, rendant la sortie lisible par l’homme.

## Étape 4 : **Add Script Element** au document

Nous créons maintenant une balise `<script>`, y insérons notre code, puis l’ajoutons au corps (`<body>`). C’est la partie **add script element**.

```java
        // Step 4: Add the script element to the document's body
        HTMLScriptElement scriptElement = (HTMLScriptElement) htmlDoc.createElement("script");
        scriptElement.setTextContent(fetchScript);
        htmlDoc.getBody().appendChild(scriptElement);
```

Pourquoi l’attacher au corps ? Dans un vrai navigateur, le script s’exécuterait dès qu’il est analysé. En l’ajoutant au DOM, nous imitons ce comportement exact, garantissant que le fetch asynchrone s’exécute lorsque nous invoquons plus tard le moteur.

## Étape 5 : Exécuter le Script Engine – Laisser le fetch asynchrone se terminer

Aspose.HTML fournit un `ScriptEngine` capable d’exécuter le JavaScript basé sur le DOM. Nous appelons `run()` et attendons que la chaîne de promesses se résolve.

```java
        // Step 5: Run the script engine so the asynchronous fetch completes before saving
        ScriptEngine scriptEngine = new ScriptEngine(htmlDoc);
        scriptEngine.run();
```

Le moteur bloque jusqu’à ce que toutes les tâches en attente (notre fetch) soient résolues, garantissant que le HTML généré contient déjà les données.

## Étape 6 : **Generate HTML from JSON** – enregistrer le résultat

Enfin, nous enregistrons le document sur le disque. Le fichier contient maintenant le bloc `<pre>` avec la charge JSON.

```java
        // Step 6: Save the resulting HTML, which now contains the fetched data
        htmlDoc.save("YOUR_DIRECTORY/fetchResult.html");
        System.out.println("HTML with fetched data saved.");
    }
}
```

L’exécution du programme produit `fetchResult.html`. Ouvrez‑le dans n’importe quel navigateur et vous verrez quelque chose comme :

```html
<pre>{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}</pre>
```

C’est le résultat **generate HTML from JSON** que vous recherchiez.

## Exemple complet fonctionnel

Ci‑dessous se trouve le fichier source complet, prêt à être exécuté. Copiez‑le, collez‑le, ajustez le chemin de sortie, et lancez `java JsFetchExample`.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.scripting.*;

public class JsFetchExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an empty HTML document that will host the script
        HTMLDocument htmlDoc = new HTMLDocument();

        // Step 2: Define a JavaScript snippet that fetches JSON data and injects it into the page
        String fetchScript = """
            (async function() {
                const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
                const data = await response.json();
                // Convert JSON to <pre> for readable formatting
                document.body.innerHTML = '<pre>' + JSON.stringify(data, null, 2) + '</pre>';
            })();
            """;

        // Step 3: Add the script element to the document's body
        HTMLScriptElement scriptElement = (HTMLScriptElement) htmlDoc.createElement("script");
        scriptElement.setTextContent(fetchScript);
        htmlDoc.getBody().appendChild(scriptElement);

        // Step 4: Run the script engine so the asynchronous fetch completes before saving
        ScriptEngine scriptEngine = new ScriptEngine(htmlDoc);
        scriptEngine.run();

        // Step 5: Save the resulting HTML, which now contains the fetched data
        htmlDoc.save("YOUR_DIRECTORY/fetchResult.html");
        System.out.println("HTML with fetched data saved.");
    }
}
```

## Résultat attendu & vérification

1. **Console :** Vous verrez `HTML with fetched data saved.`  
2. **Fichier (`fetchResult.html`) :** L’ouvrir affiche le JSON à l’intérieur d’un bloc `<pre>`, joliment indenté.  
3. **Validation :** Si vous visualisez le source de la page, vous ne trouverez qu’un élément `<pre>`—aucune balise script supplémentaire ne reste car le moteur les a déjà exécutées.

## Questions fréquentes & cas particuliers

| Question | Réponse |
|----------|--------|
| *Et si l’API renvoie une erreur ?* | Enveloppez l’appel `fetch` dans un bloc `try…catch` et écrivez un message d’erreur dans le corps à la place du JSON. |
| *Puis‑je récupérer plusieurs ressources ?* | Oui—chaînez simplement des appels supplémentaires `await fetch(...)` ou utilisez `Promise.all`. Le `innerHTML` final peut concaténer plusieurs blocs `<pre>`. |
| *Dois‑je définir des en‑têtes CORS ?* | Comme le script s’exécute dans le sandbox d’Aspose.HTML, il respecte la politique same‑origin. Le point d’accès public JSONPlaceholder autorise déjà les requêtes cross‑origin. |
| *Comment changer le répertoire de sortie à l’exécution ?* | Passez le chemin en argument de ligne de commande (`args[0]`) et remplacez la chaîne codée en dur dans `htmlDoc.save`. |
| *Existe‑t‑il un moyen d’intégrer du CSS pour le style ?* | Absolument. Créez un élément `<style>`, définissez son `textContent` avec votre CSS, puis ajoutez‑le à `<head>` avant d’exécuter le moteur. |

## Conseils pour l’utilisation en production

- **Cachez le JSON** si le point d’accès est lent ; vous pouvez écrire la chaîne récupérée dans un fichier et la réutiliser.  
- **Sanitisez les données** avant de les injecter, surtout si la source n’est pas fiable. Utilisez `JSON.stringify` en toute sécurité ou échappez les entités HTML.  
- **Configurez le timeout du ScriptEngine** (`scriptEngine.setTimeout(5000)`) pour éviter que le processus ne reste bloqué sur des services non réactifs.  

## Résumé visuel

![exemple de création de document HTML montrant le HTML généré avec le JSON à l’intérieur d’une balise pre](fetchResult.png "Capture d’écran du document HTML généré")

*Texte alternatif :* *exemple de création de document HTML – fichier HTML généré affichant le JSON récupéré à l’intérieur d’un élément pre.*

## Conclusion

Vous savez maintenant comment **create HTML document** programmatically in Java, **fetch JSON JavaScript**, **add script element**, **generate HTML from JSON**, et **convert JSON to pre** pour obtenir une sortie lisible. L’ensemble du flux de travail s’exécute hors ligne, ne nécessite qu’Aspose.HTML, et produit un fichier statique propre que vous pouvez servir n’importe où.

Ensuite, essayez d’étendre le script pour parcourir un tableau d’objets, ajouter du style CSS, ou générer plusieurs pages en utilisant la même technique. Vous pouvez également remplacer l’URL `fetch` par votre propre API afin de transformer des données dynamiques en instantanés statiques—idéal pour le pré‑rendu SEO‑friendly.

Bon codage, et n’hésitez pas à partager vos expériences dans les commentaires !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
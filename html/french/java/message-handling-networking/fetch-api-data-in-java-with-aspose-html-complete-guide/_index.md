---
category: general
date: 2026-05-28
description: récupérer les données d’une API en Java avec Aspose.HTML – apprenez à
  exécuter du JavaScript asynchrone, à lancer un script asynchrone et à définir un
  attribut DOM à partir du JSON récupéré.
draft: false
keywords:
- fetch api data
- execute async javascript
- run async script
- set dom attribute
- how to run async
language: fr
og_description: Récupérez les données d’API en Java avec Aspose.HTML. Ce tutoriel
  montre comment exécuter du JavaScript asynchrone, lancer un script asynchrone et
  définir un attribut DOM à partir des résultats de l’API.
og_title: Récupérer les données d’une API en Java – Guide Aspose.HTML étape par étape
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: fetch api data in Java using Aspose.HTML – learn how to execute async
    javascript, run async script, and set dom attribute from fetched JSON.
  headline: fetch api data in Java with Aspose.HTML - Complete Guide
  type: TechArticle
- description: fetch api data in Java using Aspose.HTML – learn how to execute async
    javascript, run async script, and set dom attribute from fetched JSON.
  name: fetch api data in Java with Aspose.HTML - Complete Guide
  steps:
  - name: Expected Output
    text: '``` GitHub stars: 84327 ```'
  - name: What if the fetch call fails?
    text: 'The script will throw a JavaScript exception, which propagates to `ScriptEngine.evaluate`.
      You can catch it in Java:'
  - name: Can I fetch from a private API that requires authentication?
    text: 'Sure—just add the appropriate headers in the script:'
  - name: Does this work on older Java versions?
    text: Aspose.HTML ships with its own JavaScript engine, so you don’t need Nashorn
      or GraalVM. However, the `try‑with‑resources` syntax requires Java 7+. For Java
      6 you’d have to close the document manually.
  type: HowTo
tags:
- Java
- Aspose.HTML
- Async JavaScript
title: Récupérer les données d'API en Java avec Aspose.HTML - Guide complet
url: /fr/java/message-handling-networking/fetch-api-data-in-java-with-aspose-html-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# récupérer des données d'API en Java avec Aspose.HTML – Guide complet

Vous êtes‑vous déjà demandé comment **fetch api data** en Java sans quitter le confort de votre IDE ? Vous n'êtes pas seul. De nombreux développeurs se heurtent à un mur lorsqu'ils doivent appeler un service distant depuis une page HTML rendue par Aspose.HTML puis récupérer le résultat dans Java.  

Dans ce tutoriel, nous parcourrons un exemple pratique qui **executes async javascript**, exécute un **async script**, et enfin **sets a DOM attribute** avec la valeur récupérée. À la fin, vous saurez exactement *how to run async* les opérations en toute sécurité et récupérer les données dont vous avez besoin.

## Ce que vous allez créer

Nous créerons une petite application console Java qui :

1. Charge un fichier HTML contenant une fonction async.  
2. Exécute un script qui utilise le **fetch API** pour appeler le point d'accès public de GitHub.  
3. Attend que la promesse se résolve (jusqu'à 10 secondes).  
4. Stocke le nombre d'étoiles dans un attribut personnalisé `data-stars` sur l'élément `<body>`.  
5. Lit cet attribut depuis Java et l'affiche.

Aucune bibliothèque cliente HTTP externe, aucun code de thread supplémentaire—juste Aspose.HTML qui fait le travail lourd.

## Prérequis

- **Java 17** ou plus récent (le code se compile avec des versions antérieures, mais 17 est la LTS actuelle).  
- Bibliothèque **Aspose.HTML for Java** (version 23.9 ou ultérieure).  
- Un fichier HTML simple (`async-page.html`) placé quelque part sur votre disque.  
- Une connexion Internet (l'appel fetch cible `https://api.github.com`).  

Si vous avez déjà un projet Maven, ajoutez la dépendance Aspose.HTML :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

Maintenant, plongeons dans le code.

## Étape 1 : préparer la page HTML

Tout d'abord, créez un fichier HTML minimal qui hébergera la fonction async. Vous n'avez besoin d'aucun balisage sophistiqué—juste une balise `<body>`.

```html
<!-- async-page.html -->
<!DOCTYPE html>
<html>
<head>
    <title>Async Demo</title>
</head>
<body>
    <!-- The script we’ll inject later will populate this attribute -->
</body>
</html>
```

Enregistrez ce fichier à un endroit accessible, par ex., `C:/temp/async-page.html`. Le chemin sera utilisé dans le code Java.

![exemple de récupération de données d'API](https://example.com/fetch-api-data.png "exemple de récupération de données d'API")

*Texte alternatif de l'image : exemple de récupération de données d'API affichant une sortie console des étoiles GitHub.*

## Étape 2 : charger le document HTML en Java

Avec le fichier HTML prêt, nous l'ouvrons en utilisant `HTMLDocument` d'Aspose.HTML. Le bloc `try‑with‑resources` garantit que le document est correctement libéré.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsExample {
    public static void main(String[] args) throws Exception {

        // Load the HTML page that contains an async function
        try (HTMLDocument doc = new HTMLDocument("C:/temp/async-page.html")) {
            // The rest of the steps go here...
        }
    }
}
```

Pourquoi utiliser `HTMLDocument` ? Il nous fournit un DOM complet, un moteur JavaScript intégré, et un moyen pratique d'interagir avec la page depuis Java—tout cela sans lancer de navigateur.

## Étape 3 : écrire le script async

Nous créons maintenant un extrait JavaScript qui **fetches API data**, attend la promesse, puis **sets a DOM attribute**. Notez l'utilisation de `async/await`—le même modèle que vous écririez dans un navigateur.

```java
String script =
    "async function run() {" +
    "  const data = await fetch('https://api.github.com').then(r => r.json());" +
    "  document.body.setAttribute('data-stars', data.stargazers_count);" +
    "}" +
    "run();";
```

Quelques points à souligner :

- La fonction `run` est déclarée `async`, donc nous pouvons `await` l'appel `fetch`.  
- Après le parsing du JSON, nous stockons `data.stargazers_count` dans un attribut personnalisé `data-stars`.  
- Enfin, nous invoquons `run()` immédiatement.  

Ce petit script fait tout ce dont nous avons besoin pour **run async script** et capturer le résultat.

## Étape 4 : exécuter le script et attendre

Le `ScriptEngine` d'Aspose.HTML peut évaluer du JavaScript avec un délai d'attente. En passant `10000`, nous indiquons au moteur d'attendre jusqu'à **10 secondes** pour que l'opération async se termine.

```java
// Execute the script and wait (up to 10 seconds) for the async operation to finish
ScriptEngine engine = doc.getScriptEngine();
engine.evaluate(script, 10000);   // timeout in milliseconds
```

Si la requête prend plus de temps que le délai d'attente, une `ScriptException` est levée—parfait pour gérer des conditions réseau instables. En production, vous envelopperiez probablement cela dans un try‑catch et réessayeriez si nécessaire.

## Étape 5 : récupérer l'attribut depuis Java

Après l'exécution du script, l'attribut `data-stars` fait maintenant partie du DOM. Récupérez-le dans Java avec un appel simple :

```java
// Retrieve the value set by the script from the document
String stars = doc.getBody().getAttribute("data-stars");
System.out.println("GitHub stars: " + stars);
```

Cette ligne affiche quelque chose comme `GitHub stars: 12345`. Le nombre exact change quotidiennement, mais le modèle reste le même.

## Exemple complet fonctionnel

En assemblant toutes les pièces, voici le programme complet, prêt à être exécuté :

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML page that contains an async function
        try (HTMLDocument doc = new HTMLDocument("C:/temp/async-page.html")) {

            // Step 2: Define a script that calls the async function and stores the result in a DOM attribute
            String script =
                "async function run() {" +
                "  const data = await fetch('https://api.github.com').then(r => r.json());" +
                "  document.body.setAttribute('data-stars', data.stargazers_count);" +
                "}" +
                "run();";

            // Step 3: Execute the script and wait (up to 10 seconds) for the async operation to finish
            ScriptEngine engine = doc.getScriptEngine();
            engine.evaluate(script, 10000);

            // Step 4: Retrieve the value set by the script from the document
            String stars = doc.getBody().getAttribute("data-stars");
            System.out.println("GitHub stars: " + stars);
        }
    }
}
```

### Sortie attendue

```
GitHub stars: 84327
```

(Votre nombre sera différent ; l'important est que la valeur soit une **string** représentant le nombre d'étoiles.)

## Questions fréquentes & cas limites

### Que se passe-t-il si l'appel fetch échoue ?

Le script lèvera une exception JavaScript, qui se propage à `ScriptEngine.evaluate`. Vous pouvez la capturer en Java :

```java
try {
    engine.evaluate(script, 10000);
} catch (ScriptException e) {
    System.err.println("Failed to fetch data: " + e.getMessage());
}
```

### Puis‑je récupérer depuis une API privée nécessitant une authentification ?

Bien sûr—ajoutez simplement les en‑têtes appropriés dans le script :

```javascript
await fetch('https://api.example.com/secure', {
    headers: { 'Authorization': 'Bearer YOUR_TOKEN' }
}).then(r => r.json());
```

N'oubliez pas de garder les secrets hors du contrôle de version.

### Cela fonctionne‑t‑il sur d'anciennes versions de Java ?

Aspose.HTML est livré avec son propre moteur JavaScript, vous n'avez donc pas besoin de Nashorn ou GraalVM. Cependant, la syntaxe `try‑with‑resources` nécessite Java 7+. Pour Java 6, vous devrez fermer le document manuellement.

## Astuces professionnelles

- **Reuse the ScriptEngine** : si vous devez exécuter de nombreux scripts async, conservez une seule instance du moteur active—cela crée moins de surcharge.  
- **Increase the timeout** : augmentez le délai d'attente pour les API plus lentes, mais ne le réglez pas sur `Integer.MAX_VALUE` ; vous avez toujours besoin d'un filet de sécurité.  
- **Validate the attribute** : validez l'attribut avant de l'utiliser. L'attribut DOM peut être `null` si le script ne s'est jamais exécuté.  
- **Log the raw JSON** : consignez le JSON brut pendant le développement ; cela aide lorsque l'API change de forme.

## Prochaines étapes

Maintenant que vous savez comment **fetch api data**, vous pouvez étendre le modèle :

- **Parse more complex JSON** et injecter plusieurs attributs.  
- **Create tables** dans la page HTML en fonction des données récupérées.  
- **Combine with Aspose.PDF** pour générer un PDF contenant les résultats d'API en temps réel.  

Chacune de ces étapes repose sur les mêmes idées de base : **execute async javascript**, **run async script**, et **set dom attribute** à partir du résultat. N'hésitez pas à expérimenter—beaucoup de puissance est cachée dans le moteur de script d'Aspose.HTML.

---

*Bon codage ! Si vous rencontrez des problèmes, laissez un commentaire ci‑dessous et nous résoudrons cela ensemble.*

## Tutoriels associés

- [Comment exécuter JavaScript en Java – Guide complet](/html/english/java/advanced-usage/how-to-run-javascript-in-java-complete-guide/)
- [Ajouter un élément au corps avec Aspose.HTML pour Java en utilisant un observateur de mutation DOM](/html/english/java/advanced-usage/dom-mutation-observer-observing-node-additions/)
- [Comment définir un délai d'attente – Gérer le délai d'attente réseau dans Aspose.HTML pour Java](/html/english/java/message-handling-networking/network-timeout/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
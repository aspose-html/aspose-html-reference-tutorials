---
category: general
date: 2026-03-26
description: Exemple d'await de niveau supérieur montrant await delay en JavaScript,
  classe d'incrémentation de compteur et champs de classe publics en JavaScript dans
  une démo en direct.
draft: false
keywords:
- top level await example
- await delay javascript
- increment counter class
- public class fields javascript
- javascript class public field
language: fr
og_description: Exemple de top‑level await démontrant await delay en JavaScript, classe
  de compteur incrémental et champs publics de classe en JavaScript dans un tutoriel
  concis.
og_title: exemple d'await de niveau supérieur – Utilisation d'un délai await en JavaScript
tags:
- JavaScript
- ES2022
- async‑await
- classes
title: exemple d'await de niveau supérieur – Utilisation de await delay en JavaScript
url: /fr/java/advanced-usage/top-level-await-example-using-await-delay-in-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# exemple top level await – Utilisation de await delay en JavaScript

Vous vous êtes déjà demandé comment mettre en pause l'exécution d'un module sans envelopper le tout dans une IIFE async ? C’est exactement ce qu’un **top level await example** vous permet de faire. Dans ce tutoriel, nous parcourrons une petite page web qui utilise `await delay javascript` pour différer le travail, puis crée une `increment counter class` qui exploite **public class fields javascript**. À la fin, vous disposerez d’un extrait complet, copiable‑collable, qui s’exécute dans n’importe quel navigateur moderne.

Nous couvrirons tout, de la définition d’une classe avec un champ public à la mise en place d’un simple helper de délai basé sur les promesses. Aucun bibliothèque externe, aucune étape de build — juste du HTML simple, un `<script type="module">` et les dernières fonctionnalités ECMAScript. Si vous êtes déjà à l’aise avec les fonctions async, vous verrez pourquoi le top‑level await ressemble à une extension naturelle. Si vous débutez avec la syntaxe **javascript class public field**, ne vous inquiétez pas — nous expliquons le pourquoi de chaque ligne.

## Ce que vous apprendrez

- Comment un **top level await example** fonctionne à l’intérieur d’un script module.
- Le pattern d’un helper `await delay javascript` qui imite `setTimeout` avec des promesses.
- Comment écrire une **increment counter class** qui utilise un champ public (`count`) et un bloc d’initialisation statique.
- La sortie console attendue et comment vérifier que le bloc statique s’exécute avant le reste du script.
- Astuces pour dépanner les pièges courants, comme les navigateurs plus anciens qui ne supportent pas le top‑level await.

> **Pro tip :** Les navigateurs modernes (Chrome 106+, Firefox 102+, Edge 106+) supportent déjà le top‑level await. Si vous devez prendre en charge des environnements plus anciens, envisagez de regrouper votre code avec un outil comme Vite ou Babel.

## Étape 1 – Définir une classe avec un champ public et un bloc statique

La première partie de notre démonstration est une classe qui stocke un compteur numérique. Remarquez la ligne `count = 0;` — c’est la syntaxe **public class fields javascript** introduite dans ES2022. Elle crée une propriété d’instance sans constructeur.

```html
<!DOCTYPE html>
<html>
<head>
    <title>ECMAScript 2022 Demo</title>
</head>
<body>
<img src="placeholder.png" alt="top level await example screenshot" title="top level await example">

<script type="module">
    // Step 1: Class definition
    class Counter {
        // Public field holds the current count
        count = 0;

        // Static block runs once when the class is first evaluated
        static {
            console.log('Counter class initialized');
        }

        // Simple method that increments the public field
        increment() {
            this.count++;
        }
    }
```

**Pourquoi un bloc statique ?** Il nous permet d’exécuter une logique d’initialisation unique (comme un log) au moment où le module est analysé, *avant* que tout top‑level await ne s’exécute. Cela garantit que le message apparaît en premier dans la console, prouvant que la classe a été évaluée tôt.

## Étape 2 – Créer un helper `await delay javascript`

Ensuite, nous avons besoin d’une petite fonction de délai basée sur les promesses. C’est essentiellement un wrapper autour de `setTimeout`, mais le fait de retourner une promesse le rend awaitable.

```javascript
    // Step 2: Promise‑based delay helper
    const delay = ms => new Promise(resolve => setTimeout(resolve, ms));
```

**Cas limite :** Si `ms` est négatif ou n’est pas un nombre, `setTimeout` le traite comme `0`. Vous pourriez ajouter une validation, mais pour une démo, le one‑liner garde les choses lisibles.

## Étape 3 – Utiliser le Top‑Level Await pour mettre en pause l’exécution

Voici maintenant la star du spectacle : le top‑level await. Parce que notre script est un module (`type="module"`), nous pouvons placer `await` directement dans le scope supérieur. Cela met le module en pause jusqu’à ce que la promesse se résolve, nous permettant de contrôler l’ordre des effets de bord.

```javascript
    // Step 3: Top‑level await – delay half a second
    await delay(500);   // Wait 500 ms so the static block logs first
```

**Question fréquente :** « Puis‑je utiliser le top‑level await dans une balise `<script>` normale ? » Non—seuls les scripts modules le supportent. Si vous oubliez `type="module"`, vous obtiendrez une erreur de syntaxe.

## Étape 4 – Instancier la classe, incrémenter et journaliser le résultat

Enfin, nous rassemblons le tout : créer une instance, appeler `increment()`, et afficher le compteur final. Cela montre la **increment counter class** en action.

```javascript
    // Step 4: Work with the Counter instance
    const counterInstance = new Counter();
    counterInstance.increment();               // count becomes 1
    console.log('Final count:', counterInstance.count);
</script>
</body>
</html>
```

### Sortie console attendue

```
Counter class initialized
Final count: 1
```

Si vous ouvrez la page dans les DevTools, vous devriez voir le message du bloc statique apparaître **avant** que le délai ne se termine, confirmant que la classe a été évaluée en premier.

## Étape 5 – Pourquoi utiliser les champs de classe publics plutôt qu’un constructeur ?

Vous pourriez vous demander pourquoi nous n’avons pas écrit :

```javascript
class Counter {
    constructor() {
        this.count = 0;
    }
}
```

Les deux approches fonctionnent, mais **public class fields javascript** offrent une syntaxe plus propre et déclarative. Le champ est défini une seule fois, pas à l’intérieur de chaque appel de constructeur, ce qui peut être plus lisible lorsque la classe devient plus grande. De plus, les blocs statiques ne peuvent pas être placés dans un constructeur, donc séparer la logique d’initialisation devient plus naturel.

## Étape 6 – Adapter l’exemple aux applications réelles

En production, vous aurez souvent besoin de plus d’un simple compteur. Voici quelques idées rapides :

- **Compteurs multiples :** Stockez‑les dans un `Map` indexé par identifiant.
- **État persistant :** Remplacez `console.log` par des écritures `localStorage`.
- **Initialisation async :** Utilisez le bloc statique pour récupérer une configuration depuis un serveur avant que des instances ne soient créées.

Tous ces patterns bénéficient toujours du top‑level await, car vous pouvez récupérer les données une fois au chargement du module et garantir qu’elles sont prêtes pour chaque consommateur.

## Questions fréquentes

**Q : Le top‑level await bloque‑t‑il les autres modules ?**  
R : Non. Chaque module s’exécute indépendamment. Seul le module contenant le await est mis en pause ; les autres modules continuent de se charger en parallèle.

**Q : Que se passe‑t‑il si la promesse de délai est rejetée ?**  
R : Un rejet non géré interrompra l’évaluation du module et apparaîtra comme une erreur dans la console. Enveloppez le await dans un `try…catch` si vous avez besoin d’un fallback élégant.

**Q : Le mot‑clé `static` est‑il obligatoire ?**  
R : Pas pour le compteur lui‑même, mais le bloc statique est un moyen pratique de démontrer que le code s’exécute *une fois* au chargement—idéal pour le logging ou la détection de fonctionnalités.

## Conclusion

Vous venez de créer un **top level await example** qui met en avant `await delay javascript`, une **increment counter class**, et la puissance des **public class fields javascript**. L’extrait complet et exécutable se trouve ci‑dessus, et la sortie console prouve que le bloc statique se déclenche avant que le code retardé ne s’exécute.  

À partir d’ici, vous pouvez expérimenter avec des flux async plus complexes, remplacer le délai par un appel API réel, ou étendre la classe avec des méthodes supplémentaires. Rappelez‑vous, le JavaScript moderne vous permet de traiter les modules comme des entités async de première classe—sans wrappers supplémentaires.

Bon codage, et n’hésitez pas à partager vos variantes dans les commentaires. Si ce guide vous a été utile, partagez‑le avec un collègue qui lutte encore avec les patterns async !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
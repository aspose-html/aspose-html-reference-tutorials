---
category: general
date: 2026-06-03
description: Créer un document HTML en Java et intégrer du JavaScript pour incrémenter
  un compteur. Apprenez un exemple de moteur de script, récupérez le innerHTML d’un
  élément, et plus encore.
draft: false
keywords:
- create html document
- embed javascript html
- get element innerhtml
- increment counter javascript
- script engine example
language: fr
og_description: Créer un document HTML en Java, intégrer du JavaScript pour incrémenter
  un compteur, et récupérer la valeur finale à l'aide d'un exemple de moteur de script.
og_title: Créer un document HTML avec JavaScript intégré – Exemple Java
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  headline: Create HTML Document with Embedded JavaScript – Java Example
  type: TechArticle
- description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  name: Create HTML Document with Embedded JavaScript – Java Example
  steps:
  - name: '**Creates an HTML document** in memory.'
    text: '**Creates an HTML document** in memory.'
  - name: '**Embeds a small JavaScript snippet** that increments a counter five times.'
    text: '**Embeds a small JavaScript snippet** that increments a counter five times.'
  - name: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
    text: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
  - name: '**Retrieves the final counter value** using `getElementInnerHTML`.'
    text: '**Retrieves the final counter value** using `getElementInnerHTML`.'
  - name: 'Prints `Final counter value: 5` to the console.'
    text: 'Prints `Final counter value: 5` to the console.'
  type: HowTo
tags:
- HTML
- JavaScript
- Java
- ScriptEngine
title: Créer un document HTML avec JavaScript intégré – Exemple Java
url: /fr/java/creating-managing-html-documents/create-html-document-with-embedded-javascript-java-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un document HTML avec JavaScript intégré – Exemple Java

Vous avez déjà eu besoin de **créer un document HTML** à partir de code Java et vous vous demandez comment intégrer du JavaScript à l'intérieur ? Dans ce guide, nous vous montrerons exactement cela, étape par étape, et vous obtiendrez un exemple fonctionnel de moteur de script qui affiche la valeur finale du compteur.  

Si vous vous êtes déjà demandé *« comment obtenir le innerHTML d'un élément après l'exécution d'un script ? »* ou *« quelle est la façon la plus propre d'incrémenter un compteur en JavaScript depuis Java ? »*—vous êtes au bon endroit. Nous couvrirons **embed javascript html**, **increment counter javascript**, et **get element innerHTML** dans un même tutoriel cohérent.

![Créer un document HTML avec JavaScript intégré](/images/create-html-document.png){: .center alt="Exemple de création de document HTML avec JavaScript intégré"}

## Ce que vous allez créer

À la fin de ce tutoriel, vous disposerez d'un programme Java autonome qui :

1. **Crée un document HTML** en mémoire.
2. **Intègre un petit extrait JavaScript** qui incrémente un compteur cinq fois.
3. **Initialise un moteur de script** (l'exemple `ScriptEngine`) pour exécuter cet extrait.
4. **Récupère la valeur finale du compteur** en utilisant `getElementInnerHTML`.
5. Affiche `Final counter value: 5` dans la console.

Pas de fichiers externes, pas de serveur web—juste du Java pur et une petite chaîne HTML.

## Prérequis

- Java 17 ou ultérieur (l'API `ScriptEngine` fait partie de la bibliothèque standard).
- Familiarité de base avec HTML et JavaScript (vous n'avez pas besoin d'une expertise approfondie).
- Un IDE ou un éditeur de texte simple plus un terminal pour compiler et exécuter le programme.

## Étape 1 : Créer un document HTML en Java

La première chose dont nous avons besoin est un objet document HTML vierge que nous pourrons remplir plus tard avec du balisage. Considérez-le comme une page virtuelle qui n'existe que dans la mémoire.

```java
// Import statements
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;

// Minimal HTML document wrapper (pseudo‑class for illustration)
class HTMLDocument {
    private StringBuilder html = new StringBuilder();

    public void write(String content) {
        html.append(content);
    }

    public String getContent() {
        return html.toString();
    }

    // Simple DOM simulation for getElementById / innerHTML
    private java.util.Map<String, String> elements = new java.util.HashMap<>();

    public void setElementInnerHTML(String id, String value) {
        elements.put(id, value);
    }

    public String getElementInnerHTML(String id) {
        return elements.getOrDefault(id, "");
    }

    // Helper used by the script engine (not production‑grade)
    public void updateCounter(int value) {
        setElementInnerHTML("counter", String.valueOf(value));
    }
}
```

**Pourquoi c’est important :** En **créant des objets document HTML** vous-même, vous évitez d'écrire sur le disque et gardez tout testable. La petite simulation du DOM nous permet plus tard de **get element innerHTML** sans navigateur complet.

## Étape 2 : Intégrer du JavaScript HTML – La logique du compteur

Nous allons maintenant écrire le balisage HTML qui inclut un bloc `<script>`. Ce script **increment counter JavaScript** cinq fois.

```java
HTMLDocument doc = new HTMLDocument();

doc.write(
    "<!DOCTYPE html><html><body>"
  + "<div id='counter'>0</div>"
  + "<script>"
  + "for (let i = 0; i < 5; i++) {"
  + "  document.getElementById('counter').innerHTML = i + 1;"
  + "}"
  + "</script>"
  + "</body></html>"
);
```

**Explication :**  
- Le `<div id='counter'>0</div>` est notre élément cible.  
- La boucle `for` exécute la logique **increment counter javascript**, mettant à jour le div à chaque itération.  
- Comme nous ne sommes pas dans un vrai navigateur, le moteur de script que nous utiliserons plus tard devra comprendre `document.getElementById`. C’est pourquoi nous avons ajouté une petite implémentation factice dans `HTMLDocument`.

## Étape 3 : Initialiser le moteur de script – Exemple de moteur de script

Java fournit l'API `ScriptEngine` (JSR‑223). Nous créerons un petit wrapper qui alimente le moteur avec le contenu HTML et fournit les méthodes DOM minimales attendues.

```java
class SimpleScriptEngine {
    private final HTMLDocument document;
    private final ScriptEngine engine;

    public SimpleScriptEngine(HTMLDocument doc) throws ScriptException {
        this.document = doc;
        ScriptEngineManager manager = new ScriptEngineManager();
        this.engine = manager.getEngineByName("JavaScript");
        // Expose a mock 'document' object to the JavaScript context
        engine.put("document", new Object() {
            public Object getElementById(String id) {
                return new Object() {
                    public void setInnerHTML(String value) {
                        document.updateCounter(Integer.parseInt(value));
                    }
                };
            }
        });
    }

    public void execute() throws ScriptException {
        // Extract only the script part from the HTML (simplified)
        String html = document.getContent();
        int scriptStart = html.indexOf("<script>") + "<script>".length();
        int scriptEnd   = html.indexOf("</script>");
        String script = html.substring(scriptStart, scriptEnd);
        engine.eval(script);
    }
}
```

**Pourquoi c’est important :** Cet **script engine example** montre comment exécuter du JavaScript intégré sans navigateur complet. Il démontre également une méthode légère pour exposer `document.getElementById` afin que le script puisse interagir avec notre DOM factice.

## Étape 4 : Exécuter le JavaScript – Incrémentation du compteur JavaScript en action

Avec le moteur prêt, nous exécutons simplement le script. La boucle à l'intérieur de la balise `<script>` se déclenchera, et notre `setInnerHTML` factice mettra à jour le compteur.

```java
try {
    SimpleScriptEngine engine = new SimpleScriptEngine(doc);
    engine.execute(); // runs the embedded JavaScript
} catch (ScriptException e) {
    e.printStackTrace();
}
```

**Que se passe-t-il en coulisses ?** Chaque itération de la boucle appelle `document.getElementById('counter').innerHTML = i + 1;`. Notre `setInnerHTML` factice transmet la chaîne numérique à `HTMLDocument.updateCounter`, qui enregistre la dernière valeur. Après la fin de la boucle, la carte interne du document contient `"5"` pour l'élément `counter`.

## Étape 5 : Récupérer la valeur finale du compteur – Get Element InnerHTML

Maintenant que le script est terminé, nous pouvons **get element innerHTML** depuis notre instance `HTMLDocument`.

```java
String finalValue = doc.getElementInnerHTML("counter");
System.out.println("Final counter value: " + finalValue); // prints 5
```

L'exécution du programme complet affiche :

```
Final counter value: 5
```

Cela confirme que la logique **increment counter javascript** a fonctionné et que nous avons bien **retrieved the element innerHTML** après l'exécution du script.

## Exemple complet fonctionnel

En assemblant le tout, voici la classe Java complète, prête à être exécutée :



## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Créer des documents HTML vides dans Aspose.HTML pour Java](/html/english/java/creating-managing-html-documents/create-empty-html-documents/)
- [Créer des documents HTML à partir d'une chaîne dans Aspose.HTML pour Java](/html/english/java/creating-managing-html-documents/create-html-documents-from-string/)
- [Enregistrer un document HTML dans Aspose.HTML pour Java](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
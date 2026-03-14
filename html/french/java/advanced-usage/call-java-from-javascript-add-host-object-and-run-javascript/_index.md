---
category: general
date: 2026-03-14
description: Apprenez à appeler Java depuis JavaScript en utilisant Aspose.HTML. Ce
  guide montre comment ajouter un objet hôte, exécuter du JavaScript en Java et journaliser
  depuis JavaScript.
draft: false
keywords:
- call java from javascript
- add host object
- run javascript in java
- javascript host object
- log from javascript
language: fr
og_description: Appelez du Java depuis JavaScript avec Aspose.HTML. Ajoutez un objet
  hôte, exécutez du JavaScript en Java et journalisez depuis JavaScript dans un seul
  tutoriel.
og_title: Appeler Java depuis JavaScript – Guide complet avec l'objet hôte
tags:
- Java
- JavaScript
- Aspose.HTML
- Scripting
title: Appeler Java depuis JavaScript – Ajouter un objet hôte et exécuter JavaScript
  en Java
url: /fr/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

?" Good.

Now ensure we didn't translate code block placeholders.

All code block placeholders remain unchanged.

Now produce final output with all content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Appeler Java depuis JavaScript – Ajouter un objet hôte et exécuter du JavaScript en Java

Vous avez déjà eu besoin d'**appeler Java depuis JavaScript** au sein d'une application Java ? Peut-être que vous construisez un moteur de rapports HTML dynamique ou que vous souhaitez simplement exposer un logger Java à un script que vous contrôlez. Dans ce tutoriel, vous verrez exactement comment ajouter un objet hôte, exécuter du JavaScript en Java, et même **journaliser depuis JavaScript** vers la JVM — le tout avec Aspose.HTML.

Nous parcourrons un exemple complet et exécutable qui crée un document HTML vide, injecte une classe Java `Logger` en tant qu'objet hôte, exécute un petit script et affiche le résultat dans la console. Aucun navigateur web externe requis, aucune “magie” mystique — juste du code Java simple que vous pouvez copier‑coller et exécuter dès aujourd'hui.

## Prérequis

- Java 17 (ou tout JDK récent) installé et configuré.
- Bibliothèque Aspose.HTML for Java (version 23.10 ou plus récente). Vous pouvez l’obtenir depuis Maven Central ou le site web d’Aspose.
- Un IDE simple ou un éditeur de texte ; l’exemple fonctionne également depuis la ligne de commande.

> **Conseil pro** : Si vous utilisez Maven, ajoutez la dépendance suivante à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

Ou, pour Gradle :

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

Maintenant que les bases sont en place, plongeons dans la solution étape par étape.

## Étape 1 : Créer un projet Java minimal

Tout d'abord, créez une nouvelle classe Java nommée `JsHostObjectDemo`. Cette classe contiendra notre méthode `main` ainsi que la définition de l'objet hôte. Garder tout dans un seul fichier rend le tutoriel autonome et facile à copier.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Demonstrates how to call Java from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    // -----------------------------------------------------------------
    // Step 1.1 – Define a simple Java class that will be callable from JS
    // -----------------------------------------------------------------
    public static class Logger {
        /**
         * This method will be invoked from JavaScript.
         *
         * @param message Text to print.
         */
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1.2 – Create an empty HTMLDocument – it gives us a scripting engine
        // -----------------------------------------------------------------
        HTMLDocument document = new HTMLDocument();

        // -----------------------------------------------------------------
        // Step 1.3 – Add the Java Logger instance as a host object named "javaLogger"
        // -----------------------------------------------------------------
        document.getWindow().addHostObject("javaLogger", new Logger());

        // -----------------------------------------------------------------
        // Step 1.4 – Prepare JavaScript code that uses the host object
        // -----------------------------------------------------------------
        String script = "javaLogger.log('Hello from JavaScript!');";

        // -----------------------------------------------------------------
        // Step 1.5 – Execute the script; the Java Logger handles the call
        // -----------------------------------------------------------------
        document.getWindow().eval(script);
    }
}
```

### Pourquoi un `HTMLDocument` ?

La classe `HTMLDocument` d’Aspose.HTML crée un environnement de script complet conforme à HTML‑5. Même si nous ne chargeons jamais de balisage, l’objet `window` du document nous donne accès au moteur JavaScript, c’est là que la magie de **run JavaScript in Java** se produit.

## Étape 2 : Ajouter l'objet hôte – « javaLogger »

La ligne

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

effectue le travail lourd pour la fonctionnalité **add host object**. En enregistrant l'instance `Logger` sous le nom `"javaLogger"`, tout script évalué dans ce document peut appeler `javaLogger.log(...)`. C’est le cœur du concept de **javascript host object** : un pont qui permet à JavaScript d’accéder à la JVM.

### Pièges courants

- **Collisions de noms** – Si vous avez déjà une variable globale nommée `javaLogger` dans votre script, l'objet hôte sera écrasé. Choisissez un nom unique.
- **Sécurité des threads** – L'objet hôte est partagé entre les exécutions de script sur le même document. Si vous prévoyez d’exécuter des scripts simultanément, rendez la classe hôte thread‑safe (par ex., utilisez `synchronized` ou les primitives de `java.util.concurrent`).

## Étape 3 : Écrire et exécuter du JavaScript

Le script que nous transmettons à `eval` est délibérément minuscule :

```javascript
javaLogger.log('Hello from JavaScript!');
```

Lorsque `document.getWindow().eval(script)` s’exécute, le moteur recherche `javaLogger` dans son scope global, trouve l’objet Java que nous avons ajouté et invoque sa méthode `log` avec la chaîne fournie.

### Sortie attendue

Exécuter la méthode `main` affiche la ligne suivante dans la console :

```
[JS] Hello from JavaScript!
```

Cette petite ligne prouve que nous avons réussi à **call java from javascript**, et le **log from javascript** apparaît exactement où un message Java normal `System.out` le ferait.

## Étape 4 : Étendre l'objet hôte – Plus que de la journalisation

Si vous devez exposer des fonctionnalités supplémentaires (par ex., accès aux fichiers, requêtes de base de données), ajoutez simplement d’autres méthodes à la classe `Logger` — ou créez une toute nouvelle classe hôte. Voici un exemple rapide qui renvoie également une valeur :

```java
public static class Utils {
    public int add(int a, int b) {
        return a + b;
    }
}

// Register it
document.getWindow().addHostObject("javaUtils", new Utils());

// JavaScript side
String script2 = "var result = javaUtils.add(3, 4); javaLogger.log('3+4=' + result);";
document.getWindow().eval(script2);
```

La console affiche maintenant :

```
[JS] 3+4=7
```

Cela démontre la flexibilité du modèle **javascript host object** : vous pouvez exposer n’importe quelle API Java dont vous avez besoin, tant que les types de données sont convertibles entre Java et JavaScript (primitifs, chaînes, tableaux, etc.).

## Étape 5 : Nettoyer les ressources

Lorsque vous avez terminé avec l’environnement de script, libérez le `HTMLDocument` afin de libérer les ressources natives :

```java
document.dispose(); // Important for long‑running applications
```

Ignorer la libération peut entraîner des fuites de mémoire, surtout si vous créez de nombreux documents dans une boucle.

## Exemple complet fonctionnel

Voici le fichier source complet que vous pouvez compiler et exécuter immédiatement. Enregistrez-le sous le nom `JsHostObjectDemo.java`, assurez‑vous que le JAR Aspose.HTML est dans votre classpath, et lancez `java JsHostObjectDemo`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Complete demo showing how to call Java from JavaScript, add host object,
 * run JavaScript in Java, and log from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    /** Simple logger that will be called from JavaScript. */
    public static class Logger {
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    /** Utility class exposing arithmetic to JavaScript. */
    public static class Utils {
        public int add(int a, int b) {
            return a + b;
        }
    }

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create the HTMLDocument – this spins up the JavaScript engine.
        HTMLDocument document = new HTMLDocument();

        // 2️⃣ Register host objects.
        document.getWindow().addHostObject("javaLogger", new Logger());
        document.getWindow().addHostObject("javaUtils", new Utils());

        // 3️⃣ JavaScript that logs a message and performs a calculation.
        String script = ""
                + "javaLogger.log('Hello from JavaScript!');"
                + "var sum = javaUtils.add(5, 12);"
                + "javaLogger.log('5 + 12 = ' + sum);";

        // 4️⃣ Execute the script.
        document.getWindow().eval(script);

        // 5️⃣ Clean up.
        document.dispose();
    }
}
```

L’exécution de ce programme produit :

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

C’est l’ensemble du flux **call java from javascript** en quelques lignes.

## FAQ – Questions fréquentes

### Cela fonctionne‑t‑il sur Android ?

Aspose.HTML est une bibliothèque pure Java, elle s’exécute donc sur n’importe quelle JVM, y compris Dalvik/ART d’Android. Il suffit d’inclure le JAR et vous disposerez des mêmes capacités d’objet hôte.

### Et si je dois passer des objets complexes ?

Vous pouvez exposer des POJO (plain old Java objects) contenant des champs, getters et setters. Le moteur les mappe automatiquement en objets JavaScript. Pour les collections, utilisez `java.util.List` ou des tableaux — les deux sont convertibles.

### Comment la gestion des erreurs fonctionne‑t‑elle ?

Si le script lève une erreur JavaScript, `eval` propagera une `ScriptException`. Enveloppez l’appel dans un bloc try‑catch pour journaliser ou récupérer :

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

### Puis‑je exécuter plusieurs scripts séquentiellement ?

Absolument. La même instance `HTMLDocument` conserve son scope global, vous pouvez donc appeler `eval` à plusieurs reprises. Veillez simplement aux collisions de noms de variables entre les scripts.

## Bonnes pratiques et astuces

- **Nommez clairement vos objets hôte** — `javaLogger`, `javaUtils`, etc. — pour éviter les confusions.
- **Gardez les méthodes hôte petites et sans effets de bord** lorsque c’est possible ; cela facilite le débogage.
- **Libérez le document** dès que vous avez fini ; cela libère la mémoire native allouée par Aspose.HTML.
- **Validez les entrées** provenant de JavaScript, surtout si les scripts proviennent de sources non fiables. Traitez‑les comme n’importe quelles données externes.

## Conclusion

Vous disposez maintenant d’un exemple complet, de bout en bout, montrant comment **call java from javascript** en **ajoutant un objet hôte**, **exécutant du JavaScript en Java**, et **journalisant depuis JavaScript** avec Aspose.HTML. Le modèle est puissant : n’importe quel service Java peut être exposé aux scripts, transformant votre application Java en une plateforme de script légère.

Ensuite, vous pourriez explorer :

- L’injection d’une page HTML complète et la manipulation du DOM depuis JavaScript.
- L’utilisation de l’objet hôte pour transmettre des données vers le côté Java (par ex., sérialisation JSON).
- L’intégration avec d’autres moteurs de script comme Nashorn ou GraalVM pour un support plus large de langages.

Essayez, modifiez les classes `Logger` ou `Utils`, et voyez jusqu’où vous pouvez pousser le concept de **javascript host object** dans vos propres projets

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-10-14
description: Appeler java depuis javascript avec Aspose.HTML. Apprenez comment ajouter
  un host object, exécuter javascript en java, et log depuis javascript dans un tutoriel
  concis.
keywords:
- call java from javascript
- execute javascript in java
- run javascript in java
- java host object
- aspose.html scripting
lastmod: 2026-10-14
og_description: Appeler java depuis javascript avec Aspose.HTML. Ce guide montre comment
  ajouter un host object, exécuter javascript en java, et log depuis javascript, le
  tout en quelques lignes de code.
og_image_alt: Screenshot of Java console output showing javascript logging via Aspose.HTML
  host object
og_title: Appeler java depuis javascript – ajouter un host object et exécuter javascript
  en java
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Call java from javascript using Aspose.HTML. Learn how to add a host
    object, execute javascript in java, and log from javascript in a concise tutorial.
  headline: Call java from javascript – add host object and run javascript in java
  type: TechArticle
- questions:
  - answer: Yes. Aspose.HTML is a pure‑Java library, so it runs on any JVM, including
      Android’s ART runtime.
    question: Does this work on Android?
  - answer: You can expose POJOs with getters and setters; the engine maps them to
      JavaScript objects automatically. Collections such as `java.util.List` or arrays
      are also convertible.
    question: What if I need to pass complex objects?
  - answer: If the script throws a JavaScript error, `eval` propagates a `ScriptException`.
      Wrap the call in a try‑catch block to log or recover.
    question: How does error handling work?
  - answer: Absolutely. The same `HTMLDocument` retains its global scope, so you can
      call `eval` repeatedly. Just manage variable names to avoid clashes.
    question: Can I run multiple scripts sequentially?
  - answer: Treat any external script as untrusted input. Validate parameters and
      consider sandboxing by exposing only the minimal required methods.
    question: Is the host object safe for untrusted scripts?
  type: FAQPage
tags:
- java
- javascript
- aspose.html
- scripting
- host object
title: Appeler java depuis javascript – ajouter un host object et exécuter javascript
  en java
url: /fr/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Appeler Java depuis JavaScript – ajouter un objet hôte et exécuter JavaScript en Java

Ever needed to **call java from javascript** inside a Java application? Maybe you’re building a dynamic HTML report engine or you simply want to expose a Java logger to a script you control. In this tutorial you’ll see exactly how to add a host object, run JavaScript in Java, and even **log from JavaScript** back to the JVM—all with Aspose.HTML.

We’ll walk through a complete, runnable example that creates an empty HTML document, injects a Java `Logger` class as a host object, executes a tiny script, and prints the result to the console. No external web browser required, no mystic “magic”—just plain Java code you can copy‑paste and run today.

## Réponses rapides
- **Comment ajouter un objet hôte ?** Register a Java instance with `document.getWindow().addHostObject("name", object)`.  
- **Puis‑je exécuter du JavaScript en Java ?** Yes—use `document.getWindow().eval(yourScript)`.  
- **Le journalisation depuis JavaScript est‑elle possible ?** Absolutely; the host object can expose any `void log(String)` method.  
- **Quelle version d'Aspose.HTML est requise ?** Version 23.10 or newer supports the full host‑object API.  
- **Ai‑je besoin d'un navigateur web ?** No—Aspose.HTML provides an embedded engine, so everything runs head‑less.

## Qu'est-ce que l'appel de Java depuis JavaScript ?
**Call java from javascript** is the technique of exposing Java objects to a JavaScript runtime so that scripts can invoke Java methods directly. Aspose.HTML creates a lightweight JavaScript engine inside a Java process, enabling seamless two‑way communication without external browsers.

## Pourquoi utiliser Aspose.HTML pour exécuter du JavaScript en Java ?
Aspose.HTML supports **50+ input and output formats** and can evaluate JavaScript in a fully‑compliant HTML5 environment. It processes scripts up to 200 ms on average for simple one‑liner code, and it does so without loading a full browser stack, which reduces memory usage by up to 80 % compared with Selenium‑based approaches.

## Prérequis

- Java 17 (or any recent JDK) installed and configured.  
- Aspose.HTML for Java library (version 23.10 or newer). You can obtain it from Maven Central or the Aspose website.  
- A simple IDE or text editor; the example works from the command line as well.

> **Pro tip:** If you use Maven, add the following dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

Or, for Gradle:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

Now that we’ve got the basics sorted, let’s dive into the step‑by‑step solution.

## Comment ajouter un objet hôte et exécuter du JavaScript en Java ?
`addHostObject` registers a Java object as a global variable in the JavaScript context. Load your `HTMLDocument`, register a Java logger under the name `"javaLogger"` using `addHostObject`, and then evaluate a short script that calls `javaLogger.log`. The entire flow requires only three API calls and works in any Java 17 runtime.

### Étape 1 : créer un projet Java minimal

First, set up a new Java class called `JsHostObjectDemo`. The class will house our `main` method and the host object definition. Keeping everything in one file makes the tutorial self‑contained and easy to copy.

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
`HTMLDocument` represents an in‑memory HTML document and provides a JavaScript engine. The `HTMLDocument` class spins up a full HTML‑5 compliant scripting environment. Even though we never load any markup, the document’s `window` object gives us access to the JavaScript engine, which is where the **run javascript in java** magic happens. Additionally you can manipulate the DOM, load resources, or evaluate scripts without a browser.

## Comment ajouter l'objet hôte – « javaLogger » ?
`Logger` is a simple Java class with a `log(String)` method that writes messages to the console. Register the `Logger` instance under the name `"javaLogger"` so that any script evaluated in this document can call `javaLogger.log(...)`. This is the core of the **add host object** requirement and makes the logger available as a global variable to JavaScript code.

### Pièges courants

- **Conflits de noms** – If you already have a global variable called `javaLogger` in your script, the host object will be overwritten. Choose a unique name.  
- **Sécurité des threads** – The host object is shared across script executions on the same document. If you plan to run scripts concurrently, make the host class thread‑safe (e.g., use `synchronized` or `java.util.concurrent` primitives).

## Comment écrire et exécuter du JavaScript en Java ?
`eval` executes a JavaScript string in the document's scripting engine and returns any result. Feed a tiny script into `eval`. The engine resolves `javaLogger` from the global scope and invokes its `log` method with the supplied string. You can also return values, handle exceptions, and chain multiple evaluations for more complex interactions.

### Sortie attendue

Running the `main` method prints the following line to the console:

```
[JS] Hello from JavaScript!
```

## Comment étendre l'objet hôte – plus que la simple journalisation ?
A host object is any Java instance exposed to JavaScript via `addHostObject`. Expose additional functionality by adding methods to the `Logger` class or by creating a new host class. Below is a quick example that also returns a value to JavaScript. The host object can expose complex types, perform I/O, or interact with other services. By returning a value, the script can receive data back, enabling two‑way communication between Java and JavaScript.

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

Now the console shows:

```
[JS] 3+4=7
```

## Comment nettoyer les ressources après l'exécution des scripts ?
`dispose` releases native resources held by the `HTMLDocument` instance. When you’re done with the scripting environment, dispose of the `HTMLDocument` to free native resources. Failing to call `dispose()` may lead to memory leaks, especially when creating many documents in loops or long‑running services. Always wrap the usage in a try‑with‑resources block or ensure `document.dispose()` is called in a finally clause.

```java
document.dispose(); // Important for long‑running applications
```

## Exemple complet fonctionnel

Below is the complete source file you can compile and run immediately. Save it as `JsHostObjectDemo.java`, ensure the Aspose.HTML JAR is on your classpath, and execute `java JsHostObjectDemo`.

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

Running this program yields:

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

## Questions fréquemment posées

**Q : Cela fonctionne‑t‑il sur Android ?**  
R : Oui. Aspose.HTML est une bibliothèque pure‑Java, donc elle fonctionne sur n'importe quelle JVM, y compris le runtime ART d'Android.

**Q : Et si je dois passer des objets complexes ?**  
R : Vous pouvez exposer des POJO avec getters et setters ; le moteur les mappe automatiquement aux objets JavaScript. Les collections comme `java.util.List` ou les tableaux sont également convertibles.

**Q : Comment fonctionne la gestion des erreurs ?**  
R : Si le script lève une erreur JavaScript, `eval` propage une `ScriptException`. Enveloppez l'appel dans un bloc try‑catch pour journaliser ou récupérer.

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

**Q : Puis‑je exécuter plusieurs scripts séquentiellement ?**  
R : Absolument. Le même `HTMLDocument` conserve son scope global, vous pouvez appeler `eval` à plusieurs reprises. Gérez simplement les noms de variables pour éviter les conflits.

**Q : L'objet hôte est‑il sûr pour des scripts non fiables ?**  
R : Traitez tout script externe comme une entrée non fiable. Validez les paramètres et envisagez de sandboxer en n'exposant que les méthodes strictement nécessaires.

## Bonnes pratiques et astuces

- **Nommez clairement vos objets hôte**—`javaLogger`, `javaUtils`, etc.—pour éviter la confusion.  
- **Gardez les méthodes hôte petites et sans effets de bord** quand c'est possible ; cela facilite le débogage.  
- **Libérez le document** dès que vous avez fini ; cela libère la mémoire native allouée par Aspose.HTML.  
- **Validez les entrées** provenant de JavaScript, surtout si les scripts proviennent de sources non fiables. Traitez‑les comme toute donnée externe.

## Conclusion

You now have a solid, end‑to‑end example of how to **call java from javascript** by **adding a host object**, **running javascript in java**, and **logging from javascript** using Aspose.HTML. The pattern is powerful: any Java service can be exposed to scripts, turning your Java application into a lightweight scripting platform.

Next, you might explore:

- Injecter une page HTML complète et manipuler le DOM depuis JavaScript.  
- Utiliser l'objet hôte pour renvoyer des données vers le côté Java (p. ex., sérialisation JSON).  
- Intégrer d'autres moteurs de script comme Nashorn ou GraalVM pour un support plus large des langages.

Give it a try, tweak the `Logger` or `Utils` classes, and see how far you can push the **javascript host object** concept in your own projects.

---

**Last Updated:** 2026-10-14  
**Tested With:** Aspose.HTML for Java 23.10  
**Author:** Aspose  






```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

```javascript
javaLogger.log('Hello from JavaScript!');
```

## Tutoriels associés

- [Activer l'exécution de scripts en Java Guide complet Aspose HTML](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)
- [Exécuter JavaScript en Java Guide complet pour exécuter Js depuis](/html/java/advanced-usage/execute-javascript-in-java-complete-guide-to-running-js-from/)
- [Comment sandboxer JavaScript Guide complet Aspose HTML](/html/java/advanced-usage/how-to-sandbox-javascript-complete-aspose-html-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
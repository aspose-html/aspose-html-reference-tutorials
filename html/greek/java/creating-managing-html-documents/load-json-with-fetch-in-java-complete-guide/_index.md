---
category: general
date: 2026-06-16
description: Φορτώστε JSON με fetch χρησιμοποιώντας Java. Μάθετε πώς να εκτελείτε
  JavaScript από Java, προαιρετική αλυσίδωση και να δημιουργείτε HTMLDocument σε Java
  σε ένα μόνο σεμινάριο.
draft: false
keywords:
- load json with fetch
- fetch json in javascript
- run javascript from java
- optional chaining tutorial
- create htmldocument in java
language: el
og_description: Φορτώστε JSON με fetch χρησιμοποιώντας Java. Αυτό το σεμινάριο δείχνει
  πώς να εκτελέσετε JavaScript από Java, να χρησιμοποιήσετε προαιρετική αλυσίδωση
  και να δημιουργήσετε HTMLDocument σε Java.
og_title: Φόρτωση JSON με Fetch στη Java – Οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Load JSON with fetch using Java. Learn how to run JavaScript from Java,
    optional chaining, and create HTMLDocument in Java in one tutorial.
  headline: Load JSON with Fetch in Java – Complete Guide
  type: TechArticle
- description: Load JSON with fetch using Java. Learn how to run JavaScript from Java,
    optional chaining, and create HTMLDocument in Java in one tutorial.
  name: Load JSON with Fetch in Java – Complete Guide
  steps:
  - name: Expected Output
    text: '``` Title: delectus aut autem ```'
  - name: 1. What if the target API returns a non‑JSON response?
    text: '`response.json()` will throw a `SyntaxError`. Our `try/catch` block captures
      that, logging “Fetch failed”. You can extend the catch to retry or fallback
      to a static payload.'
  - name: 2. Can I use this approach with HTTPS certificates that aren’t trusted?
    text: The built‑in `fetch` respects the JVM’s default SSL context. If you need
      to trust a self‑signed cert, set a custom `SSLContext` before creating the `HTMLDocument`.
      That’s a bit beyond this tutorial, but the principle stays the same.
  - name: 3. Does this work on Android?
    text: Unfortunately, `HTMLDocument` isn’t part of the Android SDK. For mobile,
      you’d need a different JavaScript engine (e.g., GraalVM) or a native HTTP client.
  - name: 4. How does optional chaining differ from classic null checks?
    text: 'Instead of writing:'
  type: HowTo
tags:
- Java
- JavaScript
- Fetch API
- HTMLDocument
- Scripting
title: Φόρτωση JSON με Fetch στη Java – Πλήρης Οδηγός
url: /el/java/creating-managing-html-documents/load-json-with-fetch-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Φόρτωση JSON με Fetch – Πλήρης Οδηγός Java

Σας έχει έρθει ποτέ η σκέψη πώς να **load JSON with fetch** παραμένοντας μέσα σε μια καθαρή εφαρμογή Java; Δεν είστε οι μόνοι. Πολλοί προγραμματιστές συναντούν εμπόδιο όταν πρέπει να καλέσουν ένα σύγχρονο REST endpoint αλλά δεν θέλουν να προσθέσουν μια βαριά βιβλιοθήκη HTTP client. Τα καλά νέα; Μπορείτε να αξιοποιήσετε τη δύναμη της κλάσης `HTMLDocument` που μοιάζει με πρόγραμμα περιήγησης, να δημιουργήσετε μια μηχανή JavaScript και να αφήσετε το `fetch` να κάνει τη βαριά δουλειά—όλα από τη Java.

Σε αυτόν τον οδηγό θα περάσουμε βήμα-βήμα από ένα πρακτικό παράδειγμα που **fetches JSON in JavaScript**, εκτελεί αυτό το script από τη Java, και επιπλέον παρουσιάζει optional chaining. Στο τέλος θα ξέρετε πώς να **run JavaScript from Java**, να δημιουργήσετε ένα `HTMLDocument` στη Java, και να διαχειριστείτε χάρη στην ευγένεια τα ελλιπή πεδία JSON. Χωρίς εξωτερικές εξαρτήσεις, μόνο το JDK και μια δόση δημιουργικότητας.

## What This Tutorial Covers

- Ρύθμιση ενός αντικειμένου `HTMLDocument` στη Java (`create htmldocument in java`).
- Λήψη του ενσωματωμένου `ScriptEngine` και παροχή του σύγχρονου JavaScript.
- Γραφή ενός αποσπάσματος **fetch JSON in JavaScript** που χρησιμοποιεί `async/await` και optional chaining (`optional chaining tutorial`).
- Εκτέλεση του script μέσω `engine.evaluate` (`run javascript from java`).
- Επαλήθευση του αποτελέσματος και διαχείριση περιπτώσεων όπως σφάλματα δικτύου ή ελλιπή ιδιότητες.

Θα χρειαστείτε Java 17 ή νεότερη, επειδή η επίδειξη βασίζεται στη ενσωματωμένη μηχανή συμβατή με Nashorn που έρχεται με το JDK. Αν χρησιμοποιείτε παλαιότερο JDK, προσθέστε τη σχετική βιβλιοθήκη scripting—λεπτομέρειες στην ενότητα “Prerequisites”.

---

## Prerequisites

- **JDK 17+** εγκατεστημένο και ρυθμισμένο το `JAVA_HOME`.
- Βασική εξοικείωση με τη σύνταξη της Java και το ασύγχρονο JavaScript.
- Ένα IDE ή κειμενογράφο (IntelliJ IDEA, VS Code, Eclipse—όπως προτιμάτε).

Δεν απαιτείται τρίτο HTTP client ή JSON parser· όλα ζουν μέσα στο script.

---

## Step 1: Create an HTMLDocument in Java

First things first—**create htmldocument in java**. Η κλάση `HTMLDocument` μας παρέχει ένα ελαφρύ DOM και, πιο σημαντικό, ένα ενσωματωμένο `ScriptEngine` που μπορεί να αξιολογήσει JavaScript όπως θα έκανε ένας περιηγητής.

```java
import org.w3c.dom.html.HTMLDocument;
import javax.script.ScriptEngine;

// Step 1: Instantiate an empty HTMLDocument.
HTMLDocument doc = new HTMLDocument();
```

> **Why this matters:** Το `HTMLDocument` λειτουργεί ως sandbox. Παρέχει ένα παγκόσμιο αντικείμενο `window`, το `fetch` και άλλα web APIs στα οποία το script μπορεί να προσπελάσει. Σκεφτείτε το ως ένα μικρό‑πρόγραμμα περιήγησης χωρίς UI.

---

## Step 2: Pull the JavaScript Engine from the Document

Now we need to **run JavaScript from Java**. Το έγγραφο εκθέτει ένα `ScriptEngine` που καταλαβαίνει σύγχρονα ECMAScript (συμπεριλαμβανομένου του `async/await`). Πάρτε το έτσι:

```java
// Step 2: Obtain the scripting engine linked to the document.
ScriptEngine engine = doc.getScriptEngine();
```

> **Pro tip:** Αν ποτέ αντιμετωπίσετε ένα `ScriptException` σχετικά με μη υποστηριζόμενα χαρακτηριστικά, βεβαιωθείτε ότι χρησιμοποιείτε JDK 17+. Τα παλαιότερα JDK έρχονται με μια κληρονομική μηχανή Nashorn που δεν υποστηρίζει async.

---

## Step 3: Write a Modern JavaScript Snippet (Optional Chaining Tutorial)

Here’s where the **fetch json in javascript** part shines. Θα ορίσουμε μια multi‑line string (Java 15+ `"""` text block) που θα κατεβάσει ένα δείγμα JSON payload, θα χρησιμοποιήσει `await`, και θα δείξει optional chaining (`??`) για διαχείριση ελλιπών τιμών.

```java
// Step 3: Define a modern JavaScript snippet.
String script = """
    async function loadData() {
        try {
            const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
            if (!response.ok) {
                console.error('Network error:', response.status);
                return;
            }
            const data = await response.json();
            // optional chaining tutorial – safely access title
            console.log('Title:', data.title ?? 'No title');
        } catch (err) {
            console.error('Fetch failed:', err);
        }
    }
    loadData();
    """;
```

**What’s happening?**

- Το `fetch` στέλνει ένα GET αίτημα σε ένα δημόσιο placeholder API.
- Το `await` παγώνει την εκτέλεση μέχρι να λυθεί η υπόσχεση, κρατώντας τον κώδικα καθαρό.
- Το `data.title ?? 'No title'` είναι το πρότυπο optional chaining: αν το `title` είναι `null` ή `undefined`, επιστρέφει το `'No title'`.
- Όλο το σενάριο τυλίγεται σε block `try/catch` για να εμφανίσει τυχόν σφάλματα δικτύου.

---

## Step 4: Execute the Script Inside the Document

Τέλος, παραδίδουμε το script στη μηχανή. Η μηχανή το τρέχει στο ίδιο νήμα, οπότε θα δείτε την έξοδο της κονσόλας απευθείας στη διαδικασία Java.

```java
// Step 4: Run the JavaScript within the document's scripting environment.
engine.evaluate(script);
```

Όταν τρέξετε το πρόγραμμα, θα πρέπει να δείτε κάτι σαν:

```
Title: delectus aut autem
```

Αν το API αλλάξει ή το πεδίο `title` εξαφανιστεί, η έξοδος θα μεταβεί αβίαστα σε:

```
Title: No title
```

Αυτή είναι η ομορφιά του optional chaining—κανένα `TypeError` δεν καταρρέει την εφαρμογή Java.

---

## Full Working Example

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι μια αυτόνομη κλάση Java που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο `Main.java` και να τρέξετε με `java Main.java`.

```java
import org.w3c.dom.html.HTMLDocument;
import javax.script.ScriptEngine;
import javax.script.ScriptException;

public class Main {
    public static void main(String[] args) throws ScriptException {
        // 1️⃣ Create an empty HTMLDocument.
        HTMLDocument doc = new HTMLDocument();

        // 2️⃣ Get the JavaScript engine tied to the document.
        ScriptEngine engine = doc.getScriptEngine();

        // 3️⃣ Define a script that loads JSON with fetch and uses optional chaining.
        String script = """
            async function loadData() {
                try {
                    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
                    if (!response.ok) {
                        console.error('Network error:', response.status);
                        return;
                    }
                    const data = await response.json();
                    // optional chaining tutorial – safely access title
                    console.log('Title:', data.title ?? 'No title');
                } catch (err) {
                    console.error('Fetch failed:', err);
                }
            }
            loadData();
            """;

        // 4️⃣ Execute the script.
        engine.evaluate(script);
    }
}
```

### Expected Output

```
Title: delectus aut autem
```

Αν σκόπιμα χαλάσετε το URL (π.χ., αλλάζετε `todos/1` σε `todos/9999`), θα δείτε το μήνυμα fallback ή σφάλμα δικτύου, δείχνοντας ανθεκτική διαχείριση σφαλμάτων.

---

## Common Questions & Edge Cases

### 1. What if the target API returns a non‑JSON response?

Το `response.json()` θα ρίξει ένα `SyntaxError`. Το block `try/catch` μας το καταγράφει, εμφανίζοντας “Fetch failed”. Μπορείτε να επεκτείνετε το catch για επαναπροσπάθεια ή fallback σε στατικό payload.

### 2. Can I use this approach with HTTPS certificates that aren’t trusted?

Το ενσωματωμένο `fetch` σέβεται το προεπιλεγμένο SSL context της JVM. Αν χρειάζεται να εμπιστευτείτε ένα self‑signed cert, ορίστε ένα προσαρμοσμένο `SSLContext` πριν δημιουργήσετε το `HTMLDocument`. Αυτό είναι λίγο εκτός του παρόντος tutorial, αλλά η αρχή παραμένει η ίδια.

### 3. Does this work on Android?

Δυστυχώς, το `HTMLDocument` δεν αποτελεί μέρος του Android SDK. Για κινητές συσκευές, θα χρειαστείτε διαφορετική μηχανή JavaScript (π.χ., GraalVM) ή έναν native HTTP client.

### 4. How does optional chaining differ from classic null checks?

Αντί να γράψετε:

```javascript
if (data && data.title) {
    console.log(data.title);
} else {
    console.log('No title');
}
```

μπορείτε απλώς να κάνετε `data.title ?? 'No title'`. Είναι πιο σύντομο, λιγότερο επιρρεπές σε λάθη, και διαβάζεται σαν φυσική γλώσσα—τέλειο για ένα **optional chaining tutorial**.

---

## Pro Tips & Best Practices

- **Reuse the engine:** Η δημιουργία νέου `HTMLDocument` για κάθε αίτημα μπορεί να είναι δαπανηρή. Κρατήστε μία ενιαία παρουσία ζωντανή αν κάνετε πολλές κλήσεις.
- **Thread safety:** Το `ScriptEngine` δεν είναι thread‑safe από προεπιλογή. Συγχρονίστε την πρόσβαση ή δημιουργήστε μια πισίνα μηχανών για ταυτόχρονες εργασίες.
- **Logging:** Το `console.log` του script γράφει στο `System.out`. Αν χρειάζεστε ολοκληρωμένο σύστημα logging, ανακατευθύνετε το `engine.getContext().setWriter(new PrintWriter(...))`.
- **Timeouts:** Το `fetch` σέβεται το προεπιλεγμένο timeout του browser (συνήθως κανένα). Μπορείτε να υλοποιήσετε χειροκίνητο abort χρησιμοποιώντας το API `AbortController` μέσα στο script αν απαιτείται αυστηρότερος έλεγχος.

---

## Conclusion

Δείξαμε πώς να **load JSON with fetch** από ένα πρόγραμμα Java, αξιοποιώντας μια ενσωματωμένη μηχανή JavaScript για να τρέξει σύγχρονο κώδικα `async/await`, και χρησιμοποιώντας optional chaining για καθαρότητα. Με το **creating an HTMLDocument in Java**, αποκτάτε ένα sandboxed περιβάλλον που κάνει το **running JavaScript from Java** να φαίνεται φυσικό, ενώ παραμένετε εντός καθαρής Java.

Από εδώ μπορείτε:

- Να αντικαταστήσετε το placeholder API με τη δική σας υπηρεσία (`fetch json in javascript` από ιδιωτικό endpoint).
- Να προσθέσετε πιο σύνθετη διαχείριση σφαλμάτων ή επαναπροσπάθειες.
- Να εξερευνήσετε τις δυνατότητες polyglot του GraalVM για ακόμη πιο πλούσιο scripting.

Δοκιμάστε το, τροποποιήστε το URL, ίσως προσθέστε ένα `POST`—υπάρχει ένας ολόκληρος κόσμος web‑κεντρικής Java που μπορείτε να ξεκλειδώσετε χωρίς βαριές βιβλιοθήκες.

Happy coding, and feel free to drop a comment if you hit any snags!

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Run JavaScript in Java – Complete Guide](/html/english/java/advanced-usage/how-to-run-javascript-in-java-complete-guide/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Load HTML Documents from URL in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
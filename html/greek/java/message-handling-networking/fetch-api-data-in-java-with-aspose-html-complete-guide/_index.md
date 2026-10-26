---
category: general
date: 2026-05-28
description: Ανάκτηση δεδομένων API σε Java με χρήση του Aspose.HTML – μάθετε πώς
  να εκτελείτε ασύγχρονο JavaScript, να τρέχετε ασύγχρονα σενάρια και να ορίζετε χαρακτηριστικό
  DOM από το ανακτηθέν JSON.
draft: false
keywords:
- fetch api data
- execute async javascript
- run async script
- set dom attribute
- how to run async
language: el
og_description: Ανάκτηση δεδομένων API σε Java με το Aspose.HTML. Αυτό το εκπαιδευτικό
  δείχνει πώς να εκτελέσετε ασύγχρονο JavaScript, να τρέξετε ασύγχρονο script και
  να ορίσετε χαρακτηριστικό DOM από τα αποτελέσματα του API.
og_title: Ανάκτηση δεδομένων API σε Java – Οδηγός Aspose.HTML βήμα‑προς‑βήμα
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
title: Ανάκτηση δεδομένων API σε Java με το Aspose.HTML - Πλήρης Οδηγός
url: /el/java/message-handling-networking/fetch-api-data-in-java-with-aspose-html-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# fetch api data σε Java με Aspose.HTML – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ πώς να **fetch api data** σε Java χωρίς να αφήσετε την άνεση του IDE σας; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν πρέπει να καλέσουν μια απομακρυσμένη υπηρεσία από μια σελίδα HTML που αποδίδεται από το Aspose.HTML και στη συνέχεια να φέρουν το αποτέλεσμα πίσω στη Java.  

Σε αυτό το tutorial θα περάσουμε από ένα πρακτικό παράδειγμα που **executes async javascript**, εκτελεί ένα **async script**, και τελικά **sets a DOM attribute** με την ανακτημένη τιμή. Στο τέλος θα γνωρίζετε ακριβώς *how to run async* λειτουργίες με ασφάλεια και θα ανακτήσετε τα δεδομένα που χρειάζεστε.

## Τι Θα Κατασκευάσετε

Θα δημιουργήσουμε μια μικρή εφαρμογή κονσόλας Java που:

1. Φορτώνει ένα αρχείο HTML που περιέχει μια async λειτουργία.  
2. Εκτελεί ένα script που χρησιμοποιεί το **fetch API** για να καλέσει το δημόσιο endpoint του GitHub.  
3. Περιμένει το promise να λυθεί (μέχρι 10 δευτερόλεπτα).  
4. Αποθηκεύει τον αριθμό αστεριών σε ένα προσαρμοσμένο χαρακτηριστικό `data-stars` στο στοιχείο `<body>`.  
5. Διαβάζει αυτό το χαρακτηριστικό πίσω στη Java και το εκτυπώνει.

Χωρίς εξωτερικές βιβλιοθήκες HTTP client, χωρίς επιπλέον κώδικα threading—απλώς το Aspose.HTML κάνει το σκληρό έργο.

## Προαπαιτούμενα

- **Java 17** ή νεότερη (ο κώδικας μεταγλωττίζεται με παλαιότερες εκδόσεις, αλλά η 17 είναι η τρέχουσα LTS).  
- **Aspose.HTML for Java** βιβλιοθήκη (έκδοση 23.9 ή νεότερη).  
- Ένα απλό αρχείο HTML (`async-page.html`) τοποθετημένο κάπου στο δίσκο σας.  
- Σύνδεση στο διαδίκτυο (η κλήση fetch στο `https://api.github.com`).  

Αν έχετε ήδη ένα Maven project, προσθέστε την εξάρτηση Aspose.HTML:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

Τώρα, ας βουτήξουμε στον κώδικα.

## Βήμα 1: Προετοιμασία της HTML Σελίδας

Πρώτα, δημιουργήστε ένα ελάχιστο αρχείο HTML που θα φιλοξενήσει τη async λειτουργία. Δεν χρειάζεστε καμία περίπλοκη σήμανση—απλώς μια ετικέτα `<body>`.

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

Αποθηκεύστε αυτό το αρχείο κάπου προσβάσιμο, π.χ., `C:/temp/async-page.html`. Η διαδρομή θα χρησιμοποιηθεί στον κώδικα Java.

![παράδειγμα fetch api data](https://example.com/fetch-api-data.png "παράδειγμα fetch api data")

*Κείμενο εναλλακτικού κειμένου εικόνας: παράδειγμα fetch api data που δείχνει μια έξοδο κονσόλας με τα αστέρια του GitHub.*

## Βήμα 2: Φόρτωση του HTML Εγγράφου στη Java

Με το αρχείο HTML έτοιμο, το ανοίγουμε χρησιμοποιώντας το `HTMLDocument` του Aspose.HTML. Το μπλοκ `try‑with‑resources` εγγυάται ότι το έγγραφο διαγράφεται σωστά.

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

Γιατί να χρησιμοποιήσουμε το `HTMLDocument`; Μας παρέχει ένα πλήρες DOM, μια ενσωματωμένη μηχανή JavaScript, και έναν βολικό τρόπο αλληλεπίδρασης με τη σελίδα από τη Java—όλα χωρίς να χρειάζεται να ξεκινήσουμε έναν browser.

## Βήμα 3: Γράψιμο του Async Script

Τώρα δημιουργούμε ένα απόσπασμα JavaScript που **fetches API data**, περιμένει το promise, και στη συνέχεια **sets a DOM attribute**. Παρατηρήστε τη χρήση του `async/await`—το ίδιο μοτίβο που θα γράφατε σε έναν browser.

```java
String script =
    "async function run() {" +
    "  const data = await fetch('https://api.github.com').then(r => r.json());" +
    "  document.body.setAttribute('data-stars', data.stargazers_count);" +
    "}" +
    "run();";
```

Μερικά σημεία προς επισήμανση:

- Η συνάρτηση `run` δηλώνεται `async`, ώστε να μπορούμε να `await` το κάλεσμα `fetch`.  
- Μετά την ανάλυση του JSON, αποθηκεύουμε το `data.stargazers_count` σε ένα προσαρμοσμένο χαρακτηριστικό `data-stars`.  
- Τέλος, καλούμε το `run()` αμέσως.  

Αυτό το μικρό script κάνει όλα όσα χρειάζονται για **run async script** και να καταγράψουμε το αποτέλεσμα.

## Βήμα 4: Εκτέλεση του Script και Αναμονή

Το `ScriptEngine` του Aspose.HTML μπορεί να αξιολογήσει JavaScript με χρονικό όριο. Με το πέρασμα του `10000` λέμε στη μηχανή να περιμένει έως **10 δευτερόλεπτα** για να ολοκληρωθεί η async λειτουργία.

```java
// Execute the script and wait (up to 10 seconds) for the async operation to finish
ScriptEngine engine = doc.getScriptEngine();
engine.evaluate(script, 10000);   // timeout in milliseconds
```

Αν το αίτημα διαρκέσει περισσότερο από το χρονικό όριο, ρίχνεται ένα `ScriptException`—ιδανικό για τη διαχείριση ασταθών συνθηκών δικτύου. Σε παραγωγή πιθανότατα θα το τυλίξετε σε try‑catch και θα επαναλάβετε όπως χρειάζεται.

## Βήμα 5: Ανάκτηση του Χαρακτηριστικού από τη Java

Μετά το script να ολοκληρωθεί, το χαρακτηριστικό `data-stars` είναι πλέον μέρος του DOM. Τραβήξτε το πίσω στη Java με μια απλή κλήση:

```java
// Retrieve the value set by the script from the document
String stars = doc.getBody().getAttribute("data-stars");
System.out.println("GitHub stars: " + stars);
```

Αυτή η γραμμή εκτυπώνει κάτι όπως `GitHub stars: 12345`. Ο ακριβής αριθμός αλλάζει καθημερινά, αλλά το μοτίβο παραμένει το ίδιο.

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα:

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

### Αναμενόμενη Έξοδος

```
GitHub stars: 84327
```

(Ο αριθμός σας θα διαφέρει· το σημαντικό είναι ότι η τιμή είναι ένα **string** που αντιπροσωπεύει τον αριθμό αστεριών.)

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν η κλήση fetch αποτύχει;

Το script θα ρίξει μια εξαίρεση JavaScript, η οποία διαδίδεται στο `ScriptEngine.evaluate`. Μπορείτε να την πιάσετε στη Java:

```java
try {
    engine.evaluate(script, 10000);
} catch (ScriptException e) {
    System.err.println("Failed to fetch data: " + e.getMessage());
}
```

### Μπορώ να κάνω fetch από ιδιωτικό API που απαιτεί έλεγχο ταυτότητας;

Φυσικά—απλώς προσθέστε τις κατάλληλες κεφαλίδες στο script:

```javascript
await fetch('https://api.example.com/secure', {
    headers: { 'Authorization': 'Bearer YOUR_TOKEN' }
}).then(r => r.json());
```

Θυμηθείτε να κρατάτε τα μυστικά εκτός του source control.

### Λειτουργεί αυτό σε παλαιότερες εκδόσεις Java;

Το Aspose.HTML έρχεται με τη δική του μηχανή JavaScript, οπότε δεν χρειάζεστε Nashorn ή GraalVM. Ωστόσο, η σύνταξη `try‑with‑resources` απαιτεί Java 7+. Για Java 6 θα πρέπει να κλείσετε το έγγραφο χειροκίνητα.

## Συμβουλές Επαγγελματία

- **Reuse the ScriptEngine**: Αν χρειάζεται να εκτελέσετε πολλά async scripts, διατηρήστε μια μόνο παρουσία του engine ενεργή—δημιουργεί λιγότερο φορτίο.  
- **Increase the timeout** για πιο αργά APIs, αλλά μην το ορίσετε σε `Integer.MAX_VALUE`; θέλετε ακόμη ένα ασφαλές όριο.  
- **Validate the attribute** πριν το χρησιμοποιήσετε. Το χαρακτηριστικό DOM μπορεί να είναι `null` αν το script δεν εκτελέστηκε ποτέ.  
- **Log the raw JSON** κατά την ανάπτυξη· βοηθά όταν το API αλλάζει δομή.

## Επόμενα Βήματα

Τώρα που γνωρίζετε πώς να **fetch api data**, μπορείτε να επεκτείνετε το μοτίβο:

- **Parse more complex JSON** και να ενσωματώσετε πολλαπλά χαρακτηριστικά.  
- **Create tables** μέσα στη σελίδα HTML βάσει των δεδομένων που φέρονται.  
- **Combine with Aspose.PDF** για να δημιουργήσετε ένα PDF που περιέχει ζωντανά αποτελέσματα API.  

Κάθε ένα από αυτά βασίζεται στις ίδιες βασικές ιδέες: **execute async javascript**, **run async script**, και **set dom attribute** από το αποτέλεσμα. Μη διστάσετε να πειραματιστείτε—υπάρχει πολλή δύναμη κρυμμένη στη μηχανή script του Aspose.HTML.

---

*Καλή προγραμματιστική! Αν αντιμετωπίσατε προβλήματα, αφήστε ένα σχόλιο παρακάτω και θα τα επιλύσουμε μαζί.*

## Σχετικά Tutorials

- [Πώς να Εκτελέσετε JavaScript σε Java – Πλήρης Οδηγός](/html/english/java/advanced-usage/how-to-run-javascript-in-java-complete-guide/)
- [Προσθήκη Στοιχείου στο Body με Aspose.HTML για Java χρησιμοποιώντας DOM Mutation Observer](/html/english/java/advanced-usage/dom-mutation-observer-observing-node-additions/)
- [Πώς να Ορίσετε Timeout – Διαχείριση Network Timeout στο Aspose.HTML για Java](/html/english/java/message-handling-networking/network-timeout/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
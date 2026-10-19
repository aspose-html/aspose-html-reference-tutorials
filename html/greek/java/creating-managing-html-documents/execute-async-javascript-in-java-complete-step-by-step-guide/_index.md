---
category: general
date: 2026-02-10
description: Μάθετε πώς να εκτελείτε ασύγχρονο JavaScript σε Java, να φορτώνετε αρχείο
  HTML σε Java, να διαβάζετε τοπικό JSON και να εκτελείτε fetch JavaScript — όλα με
  το Aspose.HTML.
draft: false
keywords:
- execute async javascript
- load html file java
- read local json
- run javascript fetch
language: el
og_description: Η εκτέλεση ασύγχρονης JavaScript σε Java έγινε εύκολη. Ακολουθήστε
  αυτό το σεμινάριο για να φορτώσετε αρχείο HTML σε Java, να διαβάσετε τοπικό JSON
  και να εκτελέσετε fetch JavaScript με το Aspose.HTML.
og_title: Εκτέλεση ασύγχρονης JavaScript σε Java – Πλήρης Οδηγός
tags:
- Java
- JavaScript
- Aspose.HTML
- Async Programming
title: Εκτέλεση ασύγχρονου JavaScript σε Java – Πλήρης Οδηγός Βήμα προς Βήμα
url: /el/java/creating-managing-html-documents/execute-async-javascript-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση ασύγχρονης JavaScript σε Java – Πλήρης Οδηγός Βήμα‑βήμα

Έχετε χρειαστεί ποτέ να **execute async javascript** από μια εφαρμογή Java αλλά δεν ήξερατε από πού να ξεκινήσετε; Δεν είστε μόνοι· πολλοί προγραμματιστές αντιμετωπίζουν αυτό το εμπόδιο όταν προσπαθούν να γεφυρώσουν τη διακομιστική Java με τα script της πλευράς του πελάτη. Τα καλά νέα είναι ότι με το Aspose.HTML μπορείτε να εκτελέσετε μια πλήρη κλήση `fetch`, να διαβάσετε ένα τοπικό αρχείο JSON και να λάβετε το αποτέλεσμα πίσω στον κώδικα Java—χωρίς πρόγραμμα περιήγησης.

Σε αυτό το tutorial θα δούμε πώς να φορτώνουμε ένα αρχείο HTML σε Java, να διαβάζουμε ένα τοπικό payload JSON και να χρησιμοποιούμε το μοτίβο `run javascript fetch` για να αντλήσουμε δεδομένα ασύγχρονα. Στο τέλος θα έχετε ένα εκτελέσιμο παράδειγμα που εκτυπώνει τον τίτλο του JSON στην κονσόλα, μαζί με συμβουλές για τη διαχείριση edge cases και κοινών παγίδων.

---

## Τι Θα Χρειαστείτε

- **Java 17** (ή οποιοδήποτε πρόσφατο JDK· το Aspose.HTML λειτουργεί με Java 8+)
- **Aspose.HTML for Java** JARs – μπορείτε να κατεβάσετε την πιο πρόσφατη έκδοση από το Maven Central repository ή τον επίσημο ιστότοπο Aspose.
- Ένα μικρό αρχείο **HTML** (`async.html`) που φιλοξενεί τη μηχανή script (μπορεί να είναι κενό, χρειαζόμαστε μόνο ένα έγγραφο).
- Ένα αρχείο **JSON** (`data.json`) τοποθετημένο δίπλα στο αρχείο HTML.
- Το αγαπημένο σας IDE (IntelliJ IDEA, Eclipse, VS Code…) – ό,τι σας βολεύει.

Καμία πρόσθετη βιβλιοθήκη, κανένα Node.js, κανένα headless browsers. Απλώς καθαρή Java και Aspose.HTML.

## Βήμα 1: Φόρτωση αρχείου HTML σε Java  

Πριν μπορέσουμε να εκτελέσουμε οποιοδήποτε script, χρειαζόμαστε μια παρουσία `HTMLDocument`. Σκεφτείτε το ως το “πρόγραμμα περιήγησης” που ζει μέσα στο JVM σας.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.net.URL;

/* Load the local HTML file – replace YOUR_DIRECTORY with the actual path */
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("file:///YOUR_DIRECTORY/async.html"));
```

> **Γιατί είναι σημαντικό αυτό το βήμα:**  
> Το `HTMLDocument` δημιουργεί ένα DOM, καταχωρεί ενσωματωμένα αντικείμενα (όπως `fetch`), και σας παρέχει ένα `ScriptEngine` συνδεδεμένο με αυτό το έγγραφο. Χωρίς έγγραφο, δεν υπάρχει που να εκτελεστεί η JavaScript.

## Βήμα 2: Λήψη της μηχανής JavaScript  

Aspose.HTML περιλαμβάνει μια μηχανή βασισμένη στο V8 που καταλαβαίνει το σύγχρονο ECMAScript, συμπεριλαμβανομένων των `async/await` και `fetch`. Αποκτήστε την από το έγγραφο:

```java
import com.aspose.html.scripting.ScriptEngine;

/* The engine is automatically linked to the document’s context */
ScriptEngine scriptEngine = htmlDoc.getScriptEngine();
```

> **Συμβουλή:** Αν σκοπεύετε να επαναχρησιμοποιήσετε τη μηχανή σε πολλά scripts, κρατήστε μια αναφορά αντί να δημιουργείτε νέο `HTMLDocument` κάθε φορά—αυτό εξοικονομεί μνήμη και επιταχύνει τη διαδικασία.

## Βήμα 3: Εκτέλεση κλήσης fetch με `run javascript fetch`  

Τώρα γράφουμε το πραγματικό async JavaScript. Η μέθοδος `evaluateAsync` επιστρέφει ένα αντικείμενο παρόμοιο με `java.util.concurrent.CompletableFuture` που λύνει στην τελική τιμή.

```java
/* This script fetches the JSON file, parses it, and extracts the "title" property */
Object titleResult = scriptEngine.evaluateAsync(
        "fetch('YOUR_DIRECTORY/data.json')" +
        ".then(r => r.json())" +
        ".then(d => d.title);"
);
```

> **Τι συμβαίνει στο παρασκήνιο;**  
> - `fetch` διαβάζει το τοπικό `data.json` μέσω ενός file URL.  
> - Το πρώτο `.then` μετατρέπει το ρεύμα της απόκρισης σε αντικείμενο JavaScript.  
> - Το δεύτερο `.then` εξάγει το πεδίο `title`, το οποίο στη συνέχεια μεταφέρεται πίσω στη Java ως απλό `Object`.

Αν προτιμάτε τη νεότερη σύνταξη `async/await`, μπορείτε να αντικαταστήσετε το απόσπασμα με:

```java
Object titleResult = scriptEngine.evaluateAsync(
        "(async () => {" +
        "  const r = await fetch('YOUR_DIRECTORY/data.json');" +
        "  const d = await r.json();" +
        "  return d.title;" +
        "})()"
);
```

Και οι δύο εκδόσεις λειτουργούν· επιλέξτε αυτή που διαβάζεται καλύτερα για την ομάδα σας.

## Βήμα 4: Εκτύπωση του ανακτημένου τίτλου  

Τέλος, εμφανίστε το αποτέλεσμα. Το `Object` που επιστρέφει η `evaluateAsync` είναι ήδη αποσυσκευασμένο, έτσι ένα απλό `toString()` κάνει τη δουλειά.

```java
System.out.println("Fetched title: " + titleResult);
```

**Αναμενόμενη έξοδος κονσόλας** (υπόθεση ότι το `data.json` περιέχει `{ \"title\": \"Aspose Rocks!\" }`):

```
Fetched title: Aspose Rocks!
```

Αν το αρχείο JSON λείπει ή είναι κατεστραμμένο, το Aspose.HTML ρίχνει ένα `ScriptException`. Πιάστε το για να αποφύγετε την κατάρρευση της εφαρμογής σας:

```java
try {
    Object titleResult = scriptEngine.evaluateAsync(...);
    System.out.println("Fetched title: " + titleResult);
} catch (Exception e) {
    System.err.println("Failed to fetch title: " + e.getMessage());
}
```

## Πλήρες Παράδειγμα Λειτουργίας  

Παρακάτω βρίσκεται το πλήρες πρόγραμμα, έτοιμο για αντιγραφή‑επικόλληση. Αντικαταστήστε το `YOUR_DIRECTORY` με τη απόλυτη διαδρομή του φακέλου που περιέχει τα `async.html` και `data.json`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.net.URL;
import com.aspose.html.scripting.ScriptEngine;

/**
 * Demonstrates how to execute async javascript in Java,
 * load html file java, read local json and run javascript fetch.
 */
public class JsExecution {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load the HTML document from a local file
        HTMLDocument htmlDoc = new HTMLDocument(
                new URL("file:///YOUR_DIRECTORY/async.html"));

        // 2️⃣ Obtain the JavaScript engine associated with the document
        ScriptEngine scriptEngine = htmlDoc.getScriptEngine();

        // 3️⃣ Execute an asynchronous fetch that reads the local JSON
        Object titleResult = scriptEngine.evaluateAsync(
                "fetch('YOUR_DIRECTORY/data.json')" +
                ".then(r => r.json())" +
                ".then(d => d.title);"
        );

        // 4️⃣ Output the fetched title
        System.out.println("Fetched title: " + titleResult);
    }
}
```

> **Γρήγορος έλεγχος:**  
> - Το `async.html` μπορεί να είναι ένα κενό αρχείο `<html></html>`.  
> - Το `data.json` πρέπει να είναι έγκυρο JSON και να βρίσκεται ακριβώς στη διαδρομή που υποδεικνύεται.  
> - Βεβαιωθείτε ότι τα file URLs χρησιμοποιούν μπροστιγές κάθετες (`/`) ακόμη και στα Windows· το σχήμα `file:///` διαχειρίζεται τη μετατροπή.

## Διαχείριση Συνηθισμένων Edge Cases  

| Situation | What to Watch For | Recommended Fix |
|-----------|-------------------|-----------------|
| **JSON not found** | Το `fetch` επιστρέφει απόκριση 404, οδηγώντας σε απορριπτόμενο promise. | Τυλίξτε το script σε μπλοκ `try/catch` ή ελέγξτε `response.ok` πριν το `json()`. |
| **Large JSON payload** | Μπλοκάρετε το JVM ενώ η μηχανή αναλύει ένα τεράστιο αντικείμενο. | Χρησιμοποιήστε streaming APIs (`response.body.getReader()`) μέσα στο script, ή χωρίστε το αρχείο σε μικρότερα τμήματα. |
| **Cross‑origin restrictions** | Παρόλο που διαβάζουμε τοπικό αρχείο, το Aspose επιβάλλει πολιτική same‑origin εξ ορισμού. | Ορίστε `scriptEngine.getSettings().setAllowFileAccess(true)` αν αντιμετωπίσετε σφάλματα άδειας. |
| **Multiple async calls** | Κάθε `evaluateAsync` δημιουργεί τη δική του αλυσίδα promises, που μπορεί να είναι δύσκολο να συντονιστεί. | Συνδέστε τις κλήσεις μέσα σε ένα μόνο script ή χρησιμοποιήστε `Promise.all` για να τις εκτελέσετε παράλληλα. |

## Pro Συμβουλές & Καλές Πρακτικές  

- **Cache the `ScriptEngine`** αν θα εκτελείτε πολλά scripts· αποφεύγει την επανεκκίνηση του V8 runtime κάθε φορά.  
- **Reuse the same `HTMLDocument`** όταν χρειάζεται να χειριστείτε το DOM (π.χ., ενσωμάτωση scripts σε πραγματικό χρόνο).  
- **Log the raw JavaScript** πριν την αξιολόγηση όταν κάνετε debugging· τα συντακτικά σφάλματα εμφανίζονται ως `ScriptException` με τον αριθμό της προβληματικής γραμμής.  
- **Keep your JSON tiny** για σκοπούς επίδειξης. Σε παραγωγή, σκεφτείτε τη συμπίεση του αρχείου ή την εξυπηρέτησή του μέσω HTTP ώστε το `fetch` να εκμεταλλευτεί την ενσωματωμένη caching.  
- **Version lock Aspose.HTML** στο `pom.xml` σας για να αποφύγετε απρόσμενες αλλαγές που σπάζουν:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

## Οπτική Επισκόπηση  

![execute async javascript αποτέλεσμα screenshot](https://example.com/placeholder.png "execute async javascript έξοδος κονσόλας")

*Image alt text:* **execute async javascript** έξοδος κονσόλας που εμφανίζει τον ανακτημένο τίτλο.

## Συμπέρασμα  

Μόλις δείξαμε **πώς να execute async javascript** από Java, φορτώσαμε ένα αρχείο HTML, διαβάσαμε ένα τοπικό αρχείο JSON και χρησιμοποιήσαμε το μοτίβο `run javascript fetch` για να αντλήσουμε δεδομένα πίσω στο JVM σας. Το πλήρες παράδειγμα εκτελείται σε λιγότερο από ένα δευτερόλεπτο, χρειάζεται μόνο Aspose.HTML και λειτουργεί σε οποιαδήποτε πλατφόρμα που υποστηρίζει Java.

Στη συνέχεια, μπορείτε να εξερευνήσετε:

- **Running multiple fetches** σε παράλληλο με `Promise.all`.  
- **Injecting custom Java objects** στο context του script για πιο πλούσια αλληλεπίδραση.  
- **Using `async/await`** για πιο καθαρή αναγνωσιμότητα κώδικα.  

Όλες αυτές οι επεκτάσεις περιστρέφονται γύρω από τις βασικές ιδέες της φόρτωσης HTML, της ανάγνωσης JSON και της εκτέλεσης JavaScript fetch—οπότε είστε ήδη έτοιμοι για πιο βαθιές δοκιμές.

Έχετε ερωτήσεις ή αντιμετωπίζετε πρόβλημα; Αφήστε ένα σχόλιο, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
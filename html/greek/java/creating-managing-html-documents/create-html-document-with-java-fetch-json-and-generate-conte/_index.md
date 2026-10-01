---
category: general
date: 2026-02-11
description: Δημιουργήστε έγγραφο HTML σε Java χρησιμοποιώντας το Aspose.HTML. Μάθετε
  πώς να ανακτήσετε JSON JavaScript, να προσθέσετε στοιχείο script, να δημιουργήσετε
  HTML από JSON και να μετατρέψετε το JSON σε pre.
draft: false
keywords:
- create html document
- fetch json javascript
- add script element
- generate html from json
- convert json to pre
language: el
og_description: Δημιουργήστε έγγραφο HTML σε Java με το Aspose.HTML. Ανακτήστε JSON
  JavaScript, προσθέστε στοιχείο script, δημιουργήστε HTML από JSON και μετατρέψτε
  το JSON σε pre—όλα σε ένα μόνο οδηγό.
og_title: Δημιουργία εγγράφου HTML σε Java – Πλήρης οδηγός
tags:
- Aspose.HTML
- Java
- Web Automation
title: Δημιουργία εγγράφου HTML με Java – Λήψη JSON και δημιουργία περιεχομένου
url: /el/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Εγγράφου HTML – Πλήρης Java Tutorial

Έχετε ποτέ χρειαστεί να **create HTML document** επί τόπου αλλά δεν ήσασταν σίγουροι πώς να αντλήσετε απομακρυσμένα δεδομένα σε αυτό; Δεν είστε μόνοι. Σε πολλά έργα θα θέλετε να **fetch JSON** με JavaScript, να ενσωματώσετε το αποτέλεσμα σε μια σελίδα και στη συνέχεια να αποθηκεύσετε το τελικό markup ως στατικό αρχείο. Αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε χρησιμοποιώντας το Aspose.HTML για Java.

Θα περάσουμε από κάθε βήμα: από τη δημιουργία ενός κεντρικού εγγράφου, μέχρι **fetch JSON JavaScript**, μέχρι **add script element**, και τέλος **generate HTML from JSON** και **convert JSON to pre** tags. Στο τέλος θα έχετε ένα έτοιμο προς χρήση `fetchResult.html` που περιέχει τα αντληθέντα δεδομένα εμφανισμένα ως pretty‑printed JSON.

## Προαπαιτούμενα

- Java 17 ή νεότερο (ο κώδικας μεταγλωττίζεται επίσης με JDK 11+)
- Aspose.HTML for Java library (διαθέσιμο μέσω Maven Central)
- Βασική εξοικείωση με HTML και async JavaScript
- Ένα IDE ή απλή γραμμή εντολών `javac`/`java`

Δεν απαιτούνται πρόσθετα frameworks—όλα εκτελούνται τοπικά.

## Βήμα 1: Ρύθμιση του Έργου και Εισαγωγή του Aspose.HTML

Πρώτα, προσθέστε την εξάρτηση Aspose.HTML στο `pom.xml` σας (ή κατεβάστε το JAR χειροκίνητα).

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- latest as of Feb 2026 -->
</dependency>
```

> **Pro tip:** Διατηρήστε τον αριθμό έκδοσης ενημερωμένο· οι νεότερες εκδόσεις διορθώνουν σφάλματα και βελτιώνουν τη μηχανή script.

## Βήμα 2: **Create HTML Document** – ο Κενός Καμβάς

Ξεκινάμε δημιουργώντας ένα κενό `HTMLDocument`. Σκεφτείτε το ως μια φρέσκια σελίδα όπου θα τοποθετήσουμε αργότερα το script μας.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.scripting.*;

public class JsFetchExample {
    public static void main(String[] args) throws Exception {

        // Step 2: Create an empty HTML document that will host the script
        HTMLDocument htmlDoc = new HTMLDocument();
```

Γιατί χρειαζόμαστε ένα αντικείμενο εγγράφου; Το `ScriptEngine` του Aspose.HTML λειτουργεί πάνω σε DOM, όχι σε ακατέργαστη συμβολοσειρά. Δημιουργώντας ένα σωστό έγγραφο δίνουμε στη μηχανή ένα πραγματικό περιβάλλον για την εκτέλεση του **fetch JSON JavaScript** μας.

## Βήμα 3: Γράψτε το απόσπασμα JavaScript – **Fetch JSON JavaScript** και **Convert JSON to pre**

Η καρδιά του tutorial βρίσκεται σε αυτή τη πολλαπλών γραμμών συμβολοσειρά. Εκτελεί ένα ασύγχρονο `fetch`, αναλύει το JSON και στη συνέχεια γράφει ένα στοιχείο `<pre>` με δεδομένα pretty‑printed.

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

Παρατηρήστε το σχόλιο *Convert JSON to <pre>* – ακριβώς αυτό κάνει η κλήση `JSON.stringify(..., null, 2)`. Προσθέτει εσοχές, καθιστώντας την έξοδο αναγνώσιμη από άνθρωπο.

## Βήμα 4: **Add Script Element** στο Έγγραφο

Τώρα δημιουργούμε ένα ετικέτα `<script>`, τοποθετούμε τον κώδικά μας μέσα και το συνδέουμε με το σώμα. Αυτό είναι το μέρος **add script element**.

```java
        // Step 4: Add the script element to the document's body
        HTMLScriptElement scriptElement = (HTMLScriptElement) htmlDoc.createElement("script");
        scriptElement.setTextContent(fetchScript);
        htmlDoc.getBody().appendChild(scriptElement);
```

Γιατί το συνδέουμε με το σώμα; Σε πραγματικό πρόγραμμα περιήγησης το script θα εκτελείται αμέσως μόλις αναλυθεί. Προσθέτοντάς το στο DOM μιμούμε αυτή τη συμπεριφορά, διασφαλίζοντας ότι το ασύγχρονο fetch εκτελείται όταν καλέσουμε αργότερα τη μηχανή.

## Βήμα 5: Εκτέλεση του Script Engine – Αφήστε το Async Fetch να ολοκληρωθεί

Το Aspose.HTML παρέχει ένα `ScriptEngine` που μπορεί να εκτελέσει το JavaScript βασισμένο σε DOM. Καλούμε `run()` και περιμένουμε την αλυσίδα των promises να ολοκληρωθεί.

```java
        // Step 5: Run the script engine so the asynchronous fetch completes before saving
        ScriptEngine scriptEngine = new ScriptEngine(htmlDoc);
        scriptEngine.run();
```

Η μηχανή μπλοκάρει μέχρι όλες οι εκκρεμείς εργασίες (το fetch μας) να ολοκληρωθούν, εξασφαλίζοντας ότι το παραγόμενο HTML περιέχει ήδη τα δεδομένα.

## Βήμα 6: **Generate HTML from JSON** – Αποθήκευση του Αποτελέσματος

Τέλος αποθηκεύουμε το έγγραφο στο δίσκο. Το αρχείο τώρα περιέχει το μπλοκ `<pre>` με το JSON payload.

```java
        // Step 6: Save the resulting HTML, which now contains the fetched data
        htmlDoc.save("YOUR_DIRECTORY/fetchResult.html");
        System.out.println("HTML with fetched data saved.");
    }
}
```

Η εκτέλεση του προγράμματος παράγει το `fetchResult.html`. Ανοίξτε το σε οποιοδήποτε πρόγραμμα περιήγησης και θα δείτε κάτι όπως:

```html
<pre>{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}</pre>
```

Αυτό είναι το αποτέλεσμα **generate HTML from JSON** που ζητούσατε.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση αρχείο πηγαίου κώδικα. Αντιγράψτε, επικολλήστε, προσαρμόστε τη διαδρομή εξόδου και τρέξτε `java JsFetchExample`.

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

## Αναμενόμενη Έξοδος & Επαλήθευση

1. **Console:** Θα δείτε `HTML with fetched data saved.`  
2. **File (`fetchResult.html`):** Ανοίγοντάς το εμφανίζει το JSON μέσα σε ένα μπλοκ `<pre>`, ωραία εσοχή.  
3. **Validation:** Αν δείτε τον πηγαίο κώδικα της σελίδας, θα βρείτε μόνο ένα στοιχείο `<pre>`—δεν υπάρχουν επιπλέον ετικέτες script επειδή η μηχανή τα έχει ήδη εκτελέσει.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| *Τι γίνεται αν το API επιστρέψει σφάλμα;* | Τυλίξτε την κλήση `fetch` σε ένα μπλοκ `try…catch` και γράψτε ένα μήνυμα σφάλματος στο σώμα αντί για το JSON. |
| *Μπορώ να αντλήσω πολλαπλούς πόρους;* | Ναι—απλώς αλυσίδωσε επιπλέον κλήσεις `await fetch(...)` ή χρησιμοποίησε `Promise.all`. Το τελικό `innerHTML` μπορεί να συνενώσει πολλά μπλοκ `<pre>`. |
| *Χρειάζεται να ορίσω CORS headers;* | Επειδή το script εκτελείται μέσα στην άκρη του Aspose.HTML, σέβεται την πολιτική same‑origin. Το δημόσιο endpoint JSONPlaceholder επιτρέπει ήδη cross‑origin αιτήματα. |
| *Πώς να αλλάξω τον φάκελο εξόδου σε χρόνο εκτέλεσης;* | Περνάτε τη διαδρομή ως όρισμα γραμμής εντολών (`args[0]`) και αντικαθιστάτε τη σκληρά κωδικοποιημένη συμβολοσειρά στο `htmlDoc.save`. |
| *Υπάρχει τρόπος να ενσωματώσω CSS για στυλ;* | Απόλυτα. Δημιουργήστε ένα στοιχείο `<style>`, ορίστε το `textContent` στο CSS σας, και προσθέστε το στο `<head>` πριν τρέξετε τη μηχανή. |

## Συμβουλές για Χρήση σε Παραγωγή

- **Cache the JSON** αν το endpoint είναι αργό· μπορείτε να γράψετε τη ληφθείσα συμβολοσειρά σε αρχείο και να την επαναχρησιμοποιήσετε.
- **Sanitize the data** πριν την ενσωμάτωση, ειδικά αν η πηγή δεν είναι αξιόπιστη. Χρησιμοποιήστε το `JSON.stringify` με ασφάλεια ή διαφύγετε τις οντότητες HTML.
- **Configure the ScriptEngine timeout** (`scriptEngine.setTimeout(5000)`) για να αποφύγετε το κρέμασμα σε μη ανταποκρινόμενες υπηρεσίες.

## Οπτική Σύνοψη

![παράδειγμα δημιουργίας εγγράφου html που δείχνει το παραγόμενο HTML με JSON μέσα σε ετικέτα pre](fetchResult.png "Στιγμιότυπο του παραγόμενου εγγράφου HTML")

*Alt text:* *παράδειγμα δημιουργίας εγγράφου html – αρχείο HTML που εμφανίζει το ληφθέν JSON μέσα σε στοιχείο pre.*

## Συμπέρασμα

Τώρα ξέρετε πώς να **create HTML document** προγραμματιστικά σε Java, **fetch JSON JavaScript**, **add script element**, **generate HTML from JSON**, και **convert JSON to pre** για αναγνώσιμη έξοδο. Όλη η ροή εργασίας εκτελείται εκτός σύνδεσης, απαιτεί μόνο το Aspose.HTML και παράγει ένα καθαρό στατικό αρχείο που μπορείτε να σερβίρετε οπουδήποτε.

Στη συνέχεια, δοκιμάστε να επεκτείνετε το script ώστε να επαναλαμβάνει έναν πίνακα αντικειμένων, να προσθέτει στυλ CSS ή να γράφει πολλαπλές σελίδες χρησιμοποιώντας την ίδια τεχνική. Μπορείτε επίσης να αντικαταστήσετε το URL `fetch` με το δικό σας API για να μετατρέψετε δυναμικά δεδομένα σε στατικά στιγμιότυπα—ιδανικό για SEO‑φιλική προ‑απόδοση.

Καλό προγραμματισμό, και μη διστάσετε να μοιραστείτε τα πειράματά σας στα σχόλια!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-10-09
description: Μάθετε πώς να καλέσετε Java από JavaScript χρησιμοποιώντας το Aspose.HTML,
  να εκτελέσετε async JavaScript και να ανακτήσετε JSON σε Java με ένα πλήρες παράδειγμα
  και πρακτικές συμβουλές.
keywords:
- how to call java from javascript
- async fetch api java
- asynchronous javascript fetch example
- call java method from javascript
lastmod: 2026-10-09
og_description: Μάθετε πώς να καλέσετε Java από JavaScript χρησιμοποιώντας το Aspose.HTML,
  να εκτελέσετε async JavaScript με το fetch API και να διαχειριστείτε JSON callbacks
  σε Java. Πλήρες παράδειγμα και συμβουλές αντιμετώπισης προβλημάτων.
og_image_alt: Diagram showing Java invoking JavaScript, async fetch returning JSON,
  and Java callback handling
og_title: Πώς να καλέσετε Java από JavaScript, async fetch και JS engine
schemas:
- author: Aspose
  dateModified: '2026-10-09'
  description: Learn how to call Java from JavaScript using Aspose.HTML, run async
    JavaScript, and fetch JSON in Java with a complete example and practical tips.
  headline: ''
  type: TechArticle
- description: Learn how to call Java from JavaScript using Aspose.HTML, run async
    JavaScript, and fetch JSON in Java with a complete example and practical tips.
  name: ''
  steps:
  - name: The **asynchronous fetch API** successfully retrieved data.
    text: The **asynchronous fetch API** successfully retrieved data.
  - name: The JSON was serialized and handed over to Java.
    text: The JSON was serialized and handed over to Java.
  - name: Our **execute javascript engine** call completed without deadlocks.
    text: Our **execute javascript engine** call completed without deadlocks.
  type: HowTo
- questions:
  - answer: Yes. Any engine that supports host objects (e.g., Nashorn, GraalVM) can
      work, but Aspose.HTML provides a full browser‑like environment with built‑in
      `fetch`.
    question: Can I use this approach with other JavaScript engines?
  - answer: Serialize the object to JSON on the Java side and let JavaScript parse
      it, or expose multiple simple methods on the host object to pass individual
      fields.
    question: What if I need to return a complex Java object instead of a string?
  - answer: Aspose.HTML follows the WHATWG Fetch Standard, handling redirects, CORS,
      and streaming exactly as modern browsers do.
    question: Is the `fetch` implementation fully standards‑compliant?
  - answer: No. The `execute` call returns immediately; the internal engine processes
      the promise asynchronously. The main thread stays alive until the script finishes
      or you shut down the engine.
    question: Does this block the Java thread while waiting for the network?
  - answer: Use the `JavaScriptEngine.setDebugMode(true)` method to output console
      messages to the Java logger.
    question: How can I debug the JavaScript code inside the engine?
  type: FAQPage
tags:
- java
- javascript
- aspose.html
- async programming
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να καλέσετε Java από JavaScript async fetch και μηχανή JS

Σε αυτό το tutorial θα ανακαλύψετε **πώς να καλέσετε Java από JavaScript** χρησιμοποιώντας το Aspose.HTML, να εκτελέσετε ασύγχρονο JavaScript με το σύγχρονο **fetch API**, και να ανακτήσετε δεδομένα JSON πίσω στη Java. Το παράδειγμα εκτελείται εξ ολοκλήρου μέσα σε ένα HTML έγγραφο που υποστηρίζεται από Java — δεν απαιτείται εξωτερικός web server ή επιπλέον βιβλιοθήκες. Στο τέλος θα έχετε ένα έτοιμο κομμάτι κώδικα που δείχνει μια καθαρή γέφυρα μεταξύ Java και JavaScript, ιδανική για server‑side rendering ή προσαρμοσμένα σενάρια scripting.

## Σύντομες απαντήσεις
- **Τι διδάσκει αυτό το tutorial;** Κλήση Java από JavaScript, χρήση async fetch, και διαχείριση JSON callbacks στη Java.  
- **Ποια βιβλιοθήκη απαιτείται;** Aspose.HTML for Java (version 23.7 or later).  
- **Χρειάζομαι web server;** Όχι, όλα εκτελούνται τοπικά μέσα στη διαδικασία Java.  
- **Υποστηρίζεται το fetch API;** Ναι, το Aspose.HTML υλοποιεί το WHATWG Fetch Standard.  
- **Μπορώ να επαναχρησιμοποιήσω το host object;** Απόλυτα — εκθέστε οποιαδήποτε δημόσια μέθοδο Java χρειάζεστε.

## Πώς να καλέσετε Java από JavaScript χρησιμοποιώντας το Aspose.HTML;

Φορτώστε το HTML έγγραφό σας, εκθέστε ένα Java host object, γράψτε μια `async` συνάρτηση που χρησιμοποιεί `fetch`, και εκτελέστε το script. Η μηχανή επιλύει το promise, καλεί το Java callback, και επιστρέφει το αποτέλεσμα JSON — όλα χωρίς να μπλοκάρει το κύριο νήμα. Αυτή η προσέγγιση σας επιτρέπει να διατηρείτε την πλευρά Java αντιδράσιμη ενώ ο κώδικας JavaScript εκτελεί δικτυακές I/O, και λειτουργεί με τον ίδιο τρόπο όπως σε περιβάλλον προγράμματος περιήγησης.

## Τι είναι το async fetch API στη Java;

Το ασύγχρονο fetch API είναι μια μέθοδος συμβατή με browsers που επιστρέφει ένα `Promise`. Η χρήση `await` σας επιτρέπει να γράψετε ασύγχρονο κώδικα που διαβάζεται σαν συγχρονισμένος, βελτιώνοντας την αναγνωσιμότητα και τη διαχείριση σφαλμάτων. Στο Aspose.HTML η υλοποίηση του fetch ακολουθεί την πλήρη προδιαγραφή WHATWG, ώστε να έχετε υποστήριξη για redirects, CORS, streaming responses, και σωστή διάδοση σφαλμάτων, όπως σε σύγχρονα browsers.

## Γιατί να χρησιμοποιήσετε τη μηχανή JavaScript του Aspose.HTML;

Το Aspose.HTML υποστηρίζει **60+ μορφές εισόδου και εξόδου** και μπορεί να επεξεργαστεί έγγραφα έως **500 MB** χωρίς να φορτώσει ολόκληρο το αρχείο στη μνήμη. Η ενσωματωμένη `JavaScriptEngine` ακολουθεί το πλήρες WHATWG Fetch Standard, παρέχοντάς σας αξιόπιστη διαχείριση δικτύου, redirects και CORS έτοιμη για χρήση.

## Προαπαιτούμενα
- Java 17 (ή Java 11) εγκατεστημένη και ρυθμισμένη στο σύστημά σας.  
- Aspose.HTML for Java 23.7 (ή η πιο πρόσφατη έκδοση) στο classpath.  
- Σύνδεση στο Internet για το demo JSON endpoint.  
- Βασική κατανόηση των μεθόδων Java και των promises του JavaScript.

## Βήμα 1 – Δημιουργήστε ένα κενό HTML έγγραφο και αποκτήστε τη μηχανή JavaScript του

Η κλάση `Document` αντιπροσωπεύει ένα HTML έγγραφο στη μνήμη και παρέχει μια sandboxed μηχανή JavaScript.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsTutorial {
    public static void main(String[] args) throws Exception {
        // Create an empty HTML document
        Document document = new Document();

        // Obtain the JavaScript engine associated with the document's window
        JavaScriptEngine jsEngine = document.getWindow().getJavaScriptEngine();
```

**Γιατί είναι σημαντικό:** Το αντικείμενο `Document` μιμείται ένα παράθυρο προγράμματος περιήγησης, και η `JavaScriptEngine` του σας επιτρέπει να εκτελείτε scripts ακριβώς όπως θα έκανε ένας browser. Αυτό αποτελεί τη βάση για **πώς να καλέσετε Java από JavaScript** — η μηχανή λειτουργεί ως γέφυρα.

## Βήμα 2 – Καταχωρήστε ένα host object ώστε το JavaScript να μπορεί να κάνει κλήση πίσω στη Java

Το host object `JavaCallback` εκθέτει μια μοναδική μέθοδο `onResult` που εκτυπώνει το JSON payload που λαμβάνεται από το JavaScript.

```java
        // Register a Java host object that the script can invoke
        jsEngine.addHostObject("javaCallback", new Object() {
            // This method will be called from JavaScript with the fetched JSON string
            public void onResult(String data) {
                System.out.println("Fetched data: " + data);
            }
        });
```

**Επεξήγηση:**  
- `addHostObject` συνδέει το όνομα `javaCallback` με το ανώνυμο αντικείμενο Java.  
- Μέσα στο JavaScript θα καλέσετε `javaCallback.onResult(...)`.  
- Αυτός είναι ο κύριος μηχανισμός για **call java from javascript** — το script φθάνει στη Java και η Java αντιδρά.

> **Pro tip:** Κρατήστε τις μεθόδους του host‑object `public` και επιστρέψτε απλούς τύπους (String, int, boolean) για να αποφύγετε το κόστος σειριοποίησης.

## Βήμα 3 – Γράψτε μια ασύγχρονη συνάρτηση JavaScript χρησιμοποιώντας το async fetch API

Η συνάρτηση `fetchJson` δείχνει `async/await` με το τυπικό fetch API.

```java
        // Asynchronous script that fetches JSON and passes it to the Java host object
        String asyncScript =
            "async function fetchData() {" +
            "  const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
            "  const json = await response.json();" +
            "  javaCallback.onResult(JSON.stringify(json));" +
            "}" +
            "fetchData();";
```

**Γιατί επιλέγουμε το `fetch` αντί των παλαιότερων XHR:**  
- Το `fetch` επιστρέφει ένα `Promise`, καθιστώντας τον κώδικα πιο καθαρό.  
- Λειτουργεί εγγενώς με `await`, έτσι η ροή διαβάζεται από πάνω προς τα κάτω — ιδανικό για ένα **asynchronous javascript fetch example**.  
- Το API είναι μελλοντικό· οι περισσότεροι browsers και engines (συμπεριλαμβανομένου του Aspose) το υποστηρίζουν αμέσως.

## Βήμα 4 – Εκτελέστε το script μέσα στη μηχανή JavaScript του εγγράφου

Η εκτέλεση του script ενεργοποιεί το event loop, επιλύει το αίτημα δικτύου, και καλεί πίσω τη Java.

```java
        // Execute the async script
        jsEngine.execute(asyncScript);
    }
}
```

Όταν τρέξετε την κλάση `AsyncJsTutorial`, θα δείτε κάτι όπως:

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

Αυτή η έξοδος επιβεβαιώνει τρία πράγματα:

1. Το **asynchronous fetch API** ανέκτησε επιτυχώς τα δεδομένα.  
2. Το JSON σειριοποιήθηκε και παραδόθηκε στη Java.  
3. Η κλήση **execute javascript engine** ολοκληρώθηκε χωρίς deadlocks.

## Βήμα 5 – Διαχείριση σφαλμάτων και ειδικών περιπτώσεων (προαιρετικές βελτιώσεις)

Ο κώδικας σε πραγματικό κόσμο σπάνια τρέχει τέλεια κάθε φορά. Παρακάτω μερικές κοινές παγίδες και πώς να τις αντιμετωπίσετε.

### 5.1 Αποτυχίες δικτύου

Αν ο απομακρυσμένος server είναι εκτός λειτουργίας, το `fetch` ρίχνει εξαίρεση. Τυλίξτε την κλήση σε μπλοκ `try/catch`:

```java
String asyncScript =
    "async function fetchData() {" +
    "  try {" +
    "    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
    "    if (!response.ok) throw new Error('Network response was not ok');" +
    "    const json = await response.json();" +
    "    javaCallback.onResult(JSON.stringify(json));" +
    "  } catch (e) {" +
    "    javaCallback.onResult('Error: ' + e.message);" +
    "  }" +
    "}" +
    "fetchData();";
```

Τώρα η πλευρά Java λαμβάνει μήνυμα σφάλματος αντί να κολλάει.

### 5.2 Χρονικά όρια

Η μηχανή του Aspose δεν εκθέτει εγγενές timeout για το `fetch`, αλλά μπορείτε να το υλοποιήσετε στο JavaScript:

```javascript
const controller = new AbortController();
setTimeout(() => controller.abort(), 5000); // 5‑second timeout
const response = await fetch(url, { signal: controller.signal });
```

### 5.3 Πολλαπλές κλήσεις

Αν χρειάζεται να κάνετε fetch σε πολλαπλούς πόρους, απλώς κάντε loop ή map πάνω σε έναν πίνακα URLs. Το host object μπορεί να επεκταθεί ώστε να δέχεται αναγνωριστικό, επιτρέποντας τη συσχέτιση των απαντήσεων.

## Πλήρες λειτουργικό παράδειγμα

Παρακάτω βρίσκεται το πλήρες αρχείο πηγαίου κώδικα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο IDE σας. Δεν υπάρχουν κρυφές εξαρτήσεις, μόνο το Aspose.HTML JAR στο classpath.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an empty HTML document and obtain its JavaScript engine
        Document document = new Document();
        JavaScriptEngine jsEngine = document.getWindow().getJavaScriptEngine();

        // Step 2: Register a host object that JavaScript can call back into Java
        jsEngine.addHostObject("javaCallback", new Object() {
            public void onResult(String data) {
                System.out.println("Fetched data: " + data);
            }
        });

        // Step 3: Write an async function that uses the asynchronous fetch API
        String asyncScript =
            "async function fetchData() {" +
            "  try {" +
            "    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
            "    if (!response.ok) throw new Error('Network error');" +
            "    const json = await response.json();" +
            "    javaCallback.onResult(JSON.stringify(json));" +
            "  } catch (e) {" +
            "    javaCallback.onResult('Error: ' + e.message);" +
            "  }" +
            "}" +
            "fetchData();";

        // Step 4: Execute the script inside the document's JavaScript engine
        jsEngine.execute(asyncScript);
    }
}
```

**Αναμενόμενη έξοδος στην κονσόλα**

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

Αν δείτε μια γραμμή σφάλματος που αρχίζει με `Error:` τότε κάτι πήγε στραβά — πιθανότατα ένα πρόβλημα δικτύου.

## Οπτική επισκόπηση

![Διάγραμμα που απεικονίζει πώς η Java καλεί το JavaScript και λαμβάνει αποτελέσματα async fetch – call java from javascript](/images/java-js-async.png)

*Η εικόνα δείχνει τη ροή: Java → JavaScriptEngine → async fetch → JavaCallback.*

## Συχνές ερωτήσεις

**Q: Μπορώ να χρησιμοποιήσω αυτή την προσέγγιση με άλλες μηχανές JavaScript;**  
A: Ναι. Οποιαδήποτε μηχανή υποστηρίζει host objects (π.χ., Nashorn, GraalVM) μπορεί να λειτουργήσει, αλλά το Aspose.HTML παρέχει ένα πλήρες περιβάλλον παρόμοιο με browser με ενσωματωμένο `fetch`.

**Q: Τι γίνεται αν χρειαστεί να επιστρέψω ένα πολύπλοκο αντικείμενο Java αντί για string;**  
A: Σειριοποιήστε το αντικείμενο σε JSON στη Java και αφήστε το JavaScript να το αναλύσει, ή εκθέστε πολλαπλές απλές μεθόδους στο host object για να περάσετε μεμονωμένα πεδία.

**Q: Είναι η υλοποίηση του `fetch` πλήρως συμβατή με τα πρότυπα;**  
A: Το Aspose.HTML ακολουθεί το WHATWG Fetch Standard, διαχειρίζεται redirects, CORS, και streaming ακριβώς όπως κάνουν οι σύγχρονοι browsers.

**Q: Μπλοκάρει αυτό το νήμα Java ενώ περιμένει το δίκτυο;**  
A: Όχι. Η κλήση `execute` επιστρέφει αμέσως· η εσωτερική μηχανή επεξεργάζεται το promise ασύγχρονα. Το κύριο νήμα παραμένει ενεργό μέχρι το script να ολοκληρωθεί ή μέχρι να τερματίσετε τη μηχανή.

**Q: Πώς μπορώ να εντοπίσω σφάλματα στον κώδικα JavaScript μέσα στη μηχανή;**  
A: Χρησιμοποιήστε τη μέθοδο `JavaScriptEngine.setDebugMode(true)` για να εκτυπώνονται μηνύματα console στο Java logger.

## Συμπέρασμα

Διασχίσαμε ένα πρακτικό σενάριο που σας επιτρέπει να **καλέσετε Java από JavaScript**, **να εκτελέσετε async JavaScript**, και **να κάνετε fetch JSON στη Java** χρησιμοποιώντας το **asynchronous fetch API**. Δημιουργώντας ένα host object, γράφοντας μια καθαρή `async` συνάρτηση, και εκτελώντας την με τη **JavaScript engine** του Aspose.HTML, αποκτάτε μια καθαρή, μη‑μπλοκαριστική γέφυρα μεταξύ των δύο runtime.

Αλλάξτε την URL του endpoint, προσθέστε περισσότερα callbacks, ή τρέξτε πολλά scripts παράλληλα. Επόμενα βήματα που μπορείτε να εξερευνήσετε:

- Εκτέλεση πολλαπλών scripts ταυτόχρονα με ξεχωριστές `JavaScriptEngine` instances.  
- Χρήση του async fetch pattern για επεξεργασία μεγάλων συνόλων δεδομένων παράλληλα.  
- Ενσωμάτωση αυτής της γέφυρας σε έναν server‑side HTML renderer που τραβά ζωντανά δεδομένα πριν το rendering.

Καλό προγραμματισμό!

---

**Τελευταία ενημέρωση:** 2026-10-09  
**Δοκιμή με:** Aspose.HTML for Java 23.7  
**Συγγραφέας:** Aspose

## Σχετικά tutorials

- [Κλήση Java από Javascript Προσθήκη Host Object και Εκτέλεση Javascript](/html/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/)
- [Πώς να Εκτελέσετε Javascript σε Java – Πλήρης Οδηγός](/html/java/advanced-usage/how-to-run-javascript-in-java-complete-guide/)
- [Ενεργοποίηση Εκτέλεσης Script σε Java – Πλήρης Οδηγός Aspose HTML](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
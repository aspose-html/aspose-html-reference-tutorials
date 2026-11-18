---
category: general
date: 2026-04-05
description: Πώς να ενεργοποιήσετε τη JavaScript κατά τη φόρτωση ενός αρχείου HTML
  σε Java χρησιμοποιώντας το Aspose.HTML – μάθετε πώς να φορτώνετε HTML με JavaScript,
  να εκτελείτε σενάρια και να ανακτάτε τα αποτελέσματα των σεναρίων.
draft: false
keywords:
- how to enable javascript
- load html with javascript
- how to execute javascript
- retrieve script result
- run page script java
language: el
og_description: Πώς να ενεργοποιήσετε τη JavaScript κατά τη φόρτωση HTML σε Java.
  Αυτός ο οδηγός δείχνει πώς να φορτώσετε HTML με JavaScript, να εκτελέσετε το script
  της σελίδας σε Java και να ανακτήσετε το αποτέλεσμα του script.
og_title: Πώς να ενεργοποιήσετε τη JavaScript σε Java HTMLDocument – Πλήρης οδηγός
tags:
- Aspose.HTML
- Java
- JavaScript
- HTML processing
title: Πώς να ενεργοποιήσετε τη JavaScript σε Java HTMLDocument – Οδηγός βήμα‑βήμα
url: /el/java/advanced-usage/how-to-enable-javascript-in-java-htmldocument-step-by-step-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ενεργοποιήσετε τη JavaScript σε Java HTMLDocument – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να ενεργοποιήσετε τη JavaScript** όταν φορτώνετε ένα αρχείο HTML από τη Java; Ίσως δημιουργείτε έναν γεννήτορα αναφορών, έναν web‑scraper ή μια μη‑απεικονιζόμενη μηχανή προεπισκόπησης και χρειάζεστε την λογική της σελίδας στην πλευρά του πελάτη να εκτελείται. Τα καλά νέα; Με το Aspose.HTML μπορείτε να μετατρέψετε αυτό το “ίσως” σε ένα στέρεο “ναι, λειτουργεί”.

Σε αυτό το tutorial θα περάσουμε από τη φόρτωση HTML με υποστήριξη JavaScript, την εκτέλεση ενός script που βρίσκεται στη σελίδα, και τελικά την ανάκτηση του αποτελέσματος του script πίσω στον κώδικα Java. Καθ' οδόν θα αγγίξουμε επίσης **load html with javascript**, **how to execute javascript**, και τις λεπτομέρειες του **run page script java**. Στο τέλος θα έχετε ένα αυτόνομο, εκτελέσιμο παράδειγμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Maven.

---

## Τι Θα Χρειαστείτε

- **Java 17** (ή οποιοδήποτε πρόσφατο JDK· το API είναι συμβατό προς τα πίσω)
- **Aspose.HTML for Java** 23.10 ή νεότερο – προσθέστε την εξάρτηση Maven που φαίνεται παρακάτω
- Ένα αρχείο HTML που περιέχει ένα μικρό script που ορίζει το `window.result` (θα δημιουργήσουμε ένα)
- Ένα αγαπημένο IDE (IntelliJ, Eclipse, VS Code…) – οτιδήποτε μπορεί να μεταγλωττίσει Java

Χωρίς εξωτερικά προγράμματα περιήγησης, χωρίς Selenium, μόνο καθαρή Java και Aspose.HTML.

![πώς να ενεργοποιήσετε τη JavaScript σε Java HTMLDocument](placeholder.png)

*Κείμενο εναλλακτικού: πώς να ενεργοποιήσετε τη JavaScript σε Java HTMLDocument*

## Βήμα 1 – Προσθέστε το Aspose.HTML στο Έργο σας

Πρώτα απ' όλα. Αν δεν το έχετε κάνει ήδη, προσθέστε τη βιβλιοθήκη Aspose.HTML στο Maven `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

> **Pro tip:** Η δωρεάν έκδοση αξιολόγησης λειτουργεί χωρίς κλειδί άδειας, αλλά θα δείτε ένα υδατογράφημα στο παραγόμενο αποτέλεσμα. Για παραγωγή, καταχωρήστε μια άδεια όπως περιγράφεται στα επίσημα έγγραφα.

## Βήμα 2 – Πώς να Ενεργοποιήσετε τη JavaScript Κατά τη Φόρτωση του Εγγράφου

Ο **πρωτεύων** διακόπτης βρίσκεται στο `DocumentLoadOptions`. Από προεπιλογή το Aspose.HTML απενεργοποιεί τη JavaScript για ασφάλεια, οπότε πρέπει να την ενεργοποιήσετε ρητά:

```java
// Step 2: Enable JavaScript execution while loading the document
DocumentLoadOptions loadOptions = new DocumentLoadOptions();
loadOptions.setEnableJavaScript(true);
```

Γιατί είναι σημαντικό: όταν ο parser HTML συναντά μια ετικέτα `<script>`, θα ενεργοποιήσει μια ενσωματωμένη μηχανή JavaScript (V8 στο παρασκήνιο) και θα επιτρέψει την εκτέλεση του κώδικα. Χωρίς αυτή τη σημαία το script αγνοείται, και οποιεσδήποτε μεταβλητές προσπαθήσετε να διαβάσετε αργότερα απλώς δεν θα υπάρχουν.

## Βήμα 3 – Φόρτωση HTML με Υποστήριξη JavaScript

Τώρα φορτώνουμε πραγματικά τη σελίδα. Παρατηρήστε ότι περνάμε το `loadOptions` που μόλις διαμορφώσαμε:

```java
// Step 3: Load the interactive HTML file with the configured options
try (HTMLDocument htmlDoc = new HTMLDocument(
        "YOUR_DIRECTORY/interactive.html", loadOptions)) {
    // The document is now ready for script interaction
}
```

Αν αναρωτιέστε αν η διαδρομή του αρχείου πρέπει να είναι απόλυτη, η απάντηση είναι **όχι** – μια σχετική διαδρομή λειτουργεί εφόσον μπορεί να επιλυθεί από τον τρέχοντα φάκελο εργασίας. Επίσης, το μπλοκ `try‑with‑resources` εγγυάται ότι το έγγραφο θα απορριφθεί σωστά, αποτρέποντας διαρροές μνήμης.

## Βήμα 4 – Πώς να Εκτελέσετε τη JavaScript και να Ανακτήσετε το Αποτέλεσμα του Script

Με τη σελίδα φορτωμένη, μπορείτε να καλέσετε οποιαδήποτε έκφραση JavaScript μέσω της μεθόδου `Window.eval`. Στο παράδειγμά μας το script της σελίδας ορίζει `window.result = "42"`; θα διαβάσουμε αυτήν την τιμή πίσω:

```java
// Step 4: Execute a script in the page context and retrieve the result
String scriptResult = (String) htmlDoc.getWindow().eval("window.result");

// Step 5: Display the value set by the page script
System.out.println("Result from script: " + scriptResult);
```

Γιατί να χρησιμοποιήσετε το `eval` αντί για `executeScript`; το `eval` αξιολογεί μια έκφραση και επιστρέφει το αποτέλεσμα άμεσα, κάτι που είναι τέλειο για απλούς getters. Αν χρειαστεί να εκτελέσετε μια πολυγραμμική συνάρτηση, περάστε ολόκληρο το σώμα της συνάρτησης ως συμβολοσειρά.

**Αναμενόμενο αποτέλεσμα**

```
Result from script: 42
```

Αν το script δεν εκτελεστεί ποτέ (ίσως ξεχάσατε να ενεργοποιήσετε τη JavaScript), το `scriptResult` θα είναι `null` και η κονσόλα θα εκτυπώσει `Result from script: null`. Αυτό είναι ένας χρήσιμος έλεγχος λογικής.

## Βήμα 5 – Εκτέλεση Script Σελίδας Java – Συνηθισμένα Πιθανά Σφάλματα & Ακραίες Περιπτώσεις

### 5.1 Απενεργοποίηση JavaScript κατά Λάθος

Αν δείτε `null` ή μια εξαίρεση όπως `ReferenceError: result is not defined`, ελέγξτε ξανά:

```java
loadOptions.setEnableJavaScript(true);   // must be true
```

### 5.2 Διαχείριση Ασύγχρονου Κώδικα

Η μηχανή του Aspose.HTML εκτελεί τα scripts **συγχρονισμένα** κατά τη φόρτωση του εγγράφου. Αν η σελίδα σας χρησιμοποιεί `setTimeout` ή promises, αυτά **δεν** θα εκτελεστούν εκτός αν χειροκίνητα προωθήσετε τον βρόχο γεγονότων:

```java
htmlDoc.getWindow().setTimeout(() -> {
    // your async code here
}, 0);
htmlDoc.getWindow().processEvents(); // forces pending tasks to run
```

### 5.3 Διαχείριση Διαφορετικών Τύπων Επιστροφής

`eval` επιστρέφει ένα `Object`. Κάντε cast στον κατάλληλο τύπο:

```java
Object raw = htmlDoc.getWindow().eval("window.result");
if (raw instanceof Number) {
    int number = ((Number) raw).intValue();
    // use as int
}
```

### 5.4 Θεωρήσεις Ασφαλείας

Η ενεργοποίηση της JavaScript ανοίγει την πόρτα σε ενδεχομένως επιβλαβή scripts. Αν φορτώνετε μη αξιόπιστο HTML, σκεφτείτε την απομόνωση (sandboxing):

```java
loadOptions.setJavaScriptSandboxEnabled(true);
```

Αυτό περιορίζει την πρόσβαση στο DOM και αποτρέπει αλληλεπιδράσεις με το σύστημα αρχείων.

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι το **πλήρες** πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα αρχείο με όνομα `JsExecutionDemo.java`. Αντικαταστήστε το `YOUR_DIRECTORY/interactive.html` με τη διαδρομή του δοκιμαστικού αρχείου HTML σας.

```java
import com.aspose.html.*;
import com.aspose.html.saving.*;

public class JsExecutionDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Enable JavaScript execution while loading the document
        DocumentLoadOptions loadOptions = new DocumentLoadOptions();
        loadOptions.setEnableJavaScript(true);

        // Step 2: Load the interactive HTML file with the configured options
        try (HTMLDocument htmlDoc = new HTMLDocument(
                "YOUR_DIRECTORY/interactive.html", loadOptions)) {

            // Step 3: Execute a script in the page context and retrieve the result
            String scriptResult = (String) htmlDoc.getWindow().eval("window.result");

            // Step 4: Display the value set by the page script
            System.out.println("Result from script: " + scriptResult);
        }
    }
}
```

**interactive.html**

```html
<!DOCTYPE html>
<html>
<head>
    <title>Interactive Demo</title>
    <script>
        // Simple script that sets a global variable
        window.result = "42";
    </script>
</head>
<body>
    <h1>JavaScript Test Page</h1>
</body>
</html>
```

Εκτελέστε το πρόγραμμα με `mvn compile exec:java -Dexec.mainClass=JsExecutionDemo`. Θα πρέπει να δείτε το αναμενόμενο αποτέλεσμα να εκτυπώνεται στην κονσόλα.

## Ανακεφαλαίωση – Τι Καλύψαμε

- **Πώς να ενεργοποιήσετε τη JavaScript** in Aspose.HTML via `DocumentLoadOptions`
- **Φόρτωση HTML με JavaScript** υποστήριξη χωρίς να αφήσετε το οικοσύστημα της Java
- **Πώς να εκτελέσετε τη JavaScript** (`eval`) και **να ανακτήσετε το αποτέλεσμα του script** πίσω στη Java
- Πρακτικές συμβουλές για **run page script java**, διαχείριση ασύγχρονου κώδικα, και απομόνωση

## Τι Ακολουθεί;

Τώρα που έχετε κατακτήσει τα βασικά, μπορείτε να εξερευνήσετε:

- **Manipulating the DOM** from Java (π.χ., `htmlDoc.getBody().appendChild(...)`)
- **Running multiple scripts** and reading back complex objects (JSON serialization)
- **Exporting the rendered page** to PDF or image using `htmlDoc.save("output.pdf", SaveFormat.PDF)`

Κάθε ένα από αυτά τα θέματα βασίζεται άμεσα στη βάση **load html with javascript** που δημιουργήσαμε εδώ.

### Τελευταίες Σκέψεις

Μόλις μάθατε **πώς να ενεργοποιήσετε τη JavaScript** σε ένα Java HTMLDocument, εκτελέσατε ένα script σελίδας και αντλήσατε το αποτέλεσμα πίσω στην εφαρμογή σας. Είναι ένα απλό μοτίβο που ξεκλειδώνει πολλές κρυφές λειτουργίες σε διαφορετικά στατικά αρχεία HTML. Μη διστάσετε να τροποποιήσετε το παράδειγμα, να πειραματιστείτε με διαφορετικά scripts και να ενσωματώσετε την προσέγγιση σε μεγαλύτερα έργα. Καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
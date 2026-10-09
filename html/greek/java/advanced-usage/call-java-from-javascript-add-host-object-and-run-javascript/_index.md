---
category: general
date: 2026-03-14
description: Μάθετε πώς να καλείτε Java από JavaScript χρησιμοποιώντας το Aspose.HTML.
  Αυτός ο οδηγός δείχνει πώς να προσθέσετε αντικείμενο φιλοξενίας, να εκτελέσετε JavaScript
  σε Java και να καταγράψετε από JavaScript.
draft: false
keywords:
- call java from javascript
- add host object
- run javascript in java
- javascript host object
- log from javascript
language: el
og_description: Κλήση Java από JavaScript χρησιμοποιώντας το Aspose.HTML. Προσθήκη
  αντικειμένου host, εκτέλεση JavaScript σε Java και καταγραφή από JavaScript σε ένα
  ενιαίο σεμινάριο.
og_title: Κλήση Java από JavaScript – Πλήρης Οδηγός με το Host Object
tags:
- Java
- JavaScript
- Aspose.HTML
- Scripting
title: Κλήση Java από JavaScript – Προσθήκη αντικειμένου φιλοξενίας και εκτέλεση JavaScript
  σε Java
url: /el/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Κλήση Java από JavaScript – Προσθήκη Host Object και Εκτέλεση JavaScript σε Java

Ποτέ χρειάστηκε να **call Java from JavaScript** μέσα σε μια εφαρμογή Java; Ίσως δημιουργείτε μια δυναμική μηχανή αναφορών HTML ή απλώς θέλετε να εκθέσετε έναν Java logger σε ένα script που ελέγχετε. Σε αυτό το tutorial θα δείτε ακριβώς πώς να προσθέσετε ένα host object, να εκτελέσετε JavaScript σε Java και ακόμη **log from JavaScript** πίσω στο JVM—όλα με το Aspose.HTML.

Θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που δημιουργεί ένα κενό έγγραφο HTML, ενσωματώνει μια κλάση Java `Logger` ως host object, εκτελεί ένα μικρό script και εκτυπώνει το αποτέλεσμα στην κονσόλα. Δεν απαιτείται εξωτερικό web browser, δεν υπάρχει “μαγικό”—απλός κώδικας Java που μπορείτε να αντιγράψετε‑και‑επικολλήσετε και να τρέξετε σήμερα.

## Prerequisites

- Java 17 (ή οποιοδήποτε πρόσφατο JDK) εγκατεστημένο και ρυθμισμένο.
- Βιβλιοθήκη Aspose.HTML for Java (έκδοση 23.10 ή νεότερη). Μπορείτε να την αποκτήσετε από το Maven Central ή την ιστοσελίδα της Aspose.
- Ένα απλό IDE ή επεξεργαστή κειμένου· το παράδειγμα λειτουργεί και από τη γραμμή εντολών.

> **Pro tip:** Αν χρησιμοποιείτε Maven, προσθέστε την παρακάτω εξάρτηση στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

Ή, για Gradle:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

Τώρα που έχουμε τα βασικά τακτοποιημένα, ας βουτήξουμε στη βήμα‑βήμα λύση.

## Step 1: Create a Minimal Java Project

Πρώτα, δημιουργήστε μια νέα κλάση Java με όνομα `JsHostObjectDemo`. Η κλάση θα περιέχει τη μέθοδο `main` και τον ορισμό του host object. Κρατώντας τα πάντα σε ένα αρχείο κάνει το tutorial αυτό-συνεπές και εύκολο στην αντιγραφή.

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

### Why an `HTMLDocument`?

Η κλάση `HTMLDocument` του Aspose.HTML δημιουργεί ένα πλήρες περιβάλλον scripting συμβατό με HTML‑5. Ακόμη και αν δεν φορτώνουμε κανένα markup, το αντικείμενο `window` του εγγράφου μας δίνει πρόσβαση στη μηχανή JavaScript, όπου συμβαίνει η **run JavaScript in Java** μαγεία.

## Step 2: Add the Host Object – “javaLogger”

Η γραμμή

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

εκτελεί το βαρέως έργο για την απαίτηση **add host object**. Καταχωρίζοντας το στιγμιότυπο `Logger` με το όνομα `"javaLogger"`, οποιοδήποτε script αξιολογείται σε αυτό το έγγραφο μπορεί να καλέσει `javaLogger.log(...)`. Αυτό είναι ο πυρήνας της έννοιας **javascript host object**: μια γέφυρα που επιτρέπει στο JavaScript να φτάσει στο JVM.

### Common Pitfalls

- **Naming collisions** – Αν ήδη έχετε μια παγκόσμια μεταβλητή με όνομα `javaLogger` στο script σας, το host object θα αντικατασταθεί. Επιλέξτε ένα μοναδικό όνομα.
- **Thread safety** – Το host object μοιράζεται μεταξύ των εκτελέσεων script στο ίδιο έγγραφο. Αν σκοπεύετε να τρέχετε scripts ταυτόχρονα, κάντε την κλάση host ασφαλή ως προς τα νήματα (π.χ., χρησιμοποιήστε `synchronized` ή τις primitive του `java.util.concurrent`).

## Step 3: Write and Execute JavaScript

Το script που περνάμε στο `eval` είναι σκόπιμα μικρό:

```javascript
javaLogger.log('Hello from JavaScript!');
```

Όταν εκτελείται `document.getWindow().eval(script)`, η μηχανή αναζητά το `javaLogger` στο παγκόσμιο scope, βρίσκει το Java αντικείμενο που προσθέσαμε και καλεί τη μέθοδο `log` με το δοσμένο string.

### Expected Output

Η εκτέλεση της μεθόδου `main` εκτυπώνει την ακόλουθη γραμμή στην κονσόλα:

```
[JS] Hello from JavaScript!
```

Αυτή η μικρή γραμμή αποδεικνύει ότι καταφέραμε με επιτυχία **call java from javascript**, και το **log from javascript** εμφανίζεται ακριβώς όπου θα εμφανιζόταν ένα κανονικό μήνυμα `System.out` της Java.

## Step 4: Extending the Host – More Than Just Logging

Αν χρειάζεται να εκθέσετε πρόσθετη λειτουργικότητα (π.χ., πρόσβαση σε αρχεία, ερωτήματα βάσης δεδομένων), απλώς προσθέστε περισσότερες μεθόδους στην κλάση `Logger`—ή δημιουργήστε μια ολοκαίνουργια κλάση host. Εδώ είναι ένα γρήγορο παράδειγμα που επιστρέφει επίσης μια τιμή:

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

Τώρα η κονσόλα δείχνει:

```
[JS] 3+4=7
```

Αυτό δείχνει την ευελιξία του προτύπου **javascript host object**: μπορείτε να εκθέσετε οποιοδήποτε Java API χρειάζεστε, αρκεί οι τύποι δεδομένων να είναι μετατρέψιμοι μεταξύ Java και JavaScript (πρωτότυπα, strings, arrays κ.λπ.).

## Step 5: Clean Up Resources

Όταν τελειώσετε με το περιβάλλον scripting, απελευθερώστε το `HTMLDocument` για να ελευθερώσετε τους εγγενείς πόρους:

```java
document.dispose(); // Important for long‑running applications
```

Η παράλειψη της απελευθέρωσης μπορεί να οδηγήσει σε διαρροές μνήμης, ειδικά αν δημιουργείτε πολλά έγγραφα σε βρόχο.

## Full Working Example

Παρακάτω βρίσκεται το πλήρες αρχείο πηγαίου κώδικα που μπορείτε να μεταγλωττίσετε και να τρέξετε αμέσως. Αποθηκεύστε το ως `JsHostObjectDemo.java`, βεβαιωθείτε ότι το JAR του Aspose.HTML βρίσκεται στο classpath, και εκτελέστε `java JsHostObjectDemo`.

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

Η εκτέλεση αυτού του προγράμματος αποδίδει:

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

Αυτή είναι ολόκληρη η ροή εργασίας **call java from javascript** σε λίγες μόνο γραμμές.

## Frequently Asked Questions

### Does this work on Android?

Το Aspose.HTML είναι βιβλιοθήκη καθαρά Java, επομένως λειτουργεί σε οποιοδήποτε JVM, συμπεριλαμβανομένου του Android Dalvik/ART. Απλώς συμπεριλάβετε το JAR και θα έχετε τις ίδιες δυνατότητες host‑object.

### What if I need to pass complex objects?

Μπορείτε να εκθέσετε POJOs (plain old Java objects) που περιέχουν πεδία, getters και setters. Η μηχανή θα τα χαρτογραφήσει αυτόματα σε αντικείμενα JavaScript. Για συλλογές, χρησιμοποιήστε `java.util.List` ή arrays—και τα δύο είναι μετατρέψιμα.

### How does error handling work?

Αν το script ρίξει σφάλμα JavaScript, το `eval` θα προωθήσει ένα `ScriptException`. Τυλίξτε την κλήση σε block try‑catch για να καταγράψετε ή να ανακτήσετε:

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

### Can I run multiple scripts sequentially?

Απολύτως. Η ίδια παρουσία `HTMLDocument` διατηρεί το παγκόσμιο scope, οπότε μπορείτε να καλέσετε `eval` επανειλημμένα. Απλώς προσέξτε τις συγκρούσεις ονομάτων μεταβλητών μεταξύ των scripts.

## Best Practices & Tips

- **Name your host objects clearly**—`javaLogger`, `javaUtils`, κ.λπ.—για να αποφύγετε σύγχυση.
- **Keep host methods small and side‑effect free** όποτε είναι δυνατόν· διευκολύνει τον εντοπισμό σφαλμάτων.
- **Dispose of the document** μόλις τελειώσετε· απελευθερώνει τη φυσική μνήμη που καταλαμβάνει το Aspose.HTML.
- **Validate inputs** από το JavaScript, ειδικά αν τα scripts προέρχονται από μη αξιόπιστες πηγές. Θεωρήστε τα όπως οποιαδήποτε εξωτερικά δεδομένα.

## Conclusion

Τώρα έχετε ένα στέρεο, end‑to‑end παράδειγμα για το πώς να **call java from javascript** προσθέτοντας ένα **host object**, **running JavaScript in Java**, και **logging from JavaScript** χρησιμοποιώντας το Aspose.HTML. Το πρότυπο είναι ισχυρό: οποιαδήποτε υπηρεσία Java μπορεί να εκτεθεί σε scripts, μετατρέποντας την εφαρμογή σας σε μια ελαφριά πλατφόρμα scripting.

Στη συνέχεια, μπορείτε να εξερευνήσετε:

- Ενσωμάτωση πλήρους σελίδας HTML και χειρισμό του DOM από JavaScript.
- Χρήση του host object για ροή δεδομένων πίσω στη Java (π.χ., σειριοποίηση JSON).
- Ενσωμάτωση με άλλες μηχανές scripting όπως Nashorn ή GraalVM για ευρύτερη υποστήριξη γλωσσών.

Δοκιμάστε το, τροποποιήστε τις κλάσεις `Logger` ή `Utils`, και δείτε πόσο μακριά μπορείτε να προωθήσετε την έννοια **javascript host object** στα δικά σας έργα.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
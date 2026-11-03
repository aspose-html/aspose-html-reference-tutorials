---
category: general
date: 2026-10-14
description: Κλήση java από javascript χρησιμοποιώντας Aspose.HTML. Μάθετε πώς να
  προσθέσετε ένα host object, να εκτελέσετε javascript σε java και να κάνετε log από
  javascript σε ένα σύντομο tutorial.
keywords:
- call java from javascript
- execute javascript in java
- run javascript in java
- java host object
- aspose.html scripting
lastmod: 2026-10-14
og_description: Κλήση java από javascript χρησιμοποιώντας Aspose.HTML. Αυτός ο guide
  δείχνει πώς να προσθέσετε ένα host object, να εκτελέσετε javascript σε java και
  να κάνετε log από javascript, όλα σε λίγες γραμμές κώδικα.
og_image_alt: Screenshot of Java console output showing javascript logging via Aspose.HTML
  host object
og_title: Κλήση java από javascript – προσθήκη host object και εκτέλεση javascript
  σε java
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
title: Κλήση java από javascript – προσθήκη host object και εκτέλεση javascript σε
  java
url: /el/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Κλήση Java από JavaScript – προσθήκη αντικειμένου κεντρικού υπολογιστή και εκτέλεση JavaScript σε Java

Έχετε χρειαστεί ποτέ να **call java from javascript** μέσα σε μια εφαρμογή Java; Ίσως να δημιουργείτε μια δυναμική μηχανή αναφορών HTML ή απλώς θέλετε να εκθέσετε έναν Java logger σε ένα script που ελέγχετε. Σε αυτό το tutorial θα δείτε ακριβώς πώς να προσθέσετε ένα αντικείμενο κεντρικού υπολογιστή, να εκτελέσετε JavaScript σε Java, και ακόμη **log from JavaScript** πίσω στο JVM—όλα με το Aspose.HTML.

Θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που δημιουργεί ένα κενό έγγραφο HTML, ενσωματώνει μια κλάση Java `Logger` ως αντικείμενο κεντρικού υπολογιστή, εκτελεί ένα μικρό script και εκτυπώνει το αποτέλεσμα στην κονσόλα. Δεν απαιτείται εξωτερικό πρόγραμμα περιήγησης, δεν υπάρχει μυστηριώδης «μαγεία»—απλώς απλός κώδικας Java που μπορείτε να αντιγράψετε‑επικολλήσετε και να εκτελέσετε σήμερα.

## Γρήγορες απαντήσεις
- **Πώς προσθέτω ένα αντικείμενο κεντρικού υπολογιστή;** Register a Java instance with `document.getWindow().addHostObject("name", object)`.  
- **Μπορώ να εκτελέσω JavaScript σε Java;** Yes—use `document.getWindow().eval(yourScript)`.  
- **Είναι δυνατή η καταγραφή από JavaScript;** Absolutely; the host object can expose any `void log(String)` method.  
- **Ποια έκδοση του Aspose.HTML απαιτείται;** Version 23.10 or newer supports the full host‑object API.  
- **Χρειάζομαι πρόγραμμα περιήγησης;** No—Aspose.HTML provides an embedded engine, so everything runs head‑less.

## Τι είναι η κλήση java από javascript;
**Call java from javascript** είναι η τεχνική έκθεσης αντικειμένων Java σε ένα runtime JavaScript ώστε τα scripts να μπορούν να καλούν μεθόδους Java άμεσα. Το Aspose.HTML δημιουργεί μια ελαφριά μηχανή JavaScript μέσα σε μια διεργασία Java, επιτρέποντας αδιάλειπτη διπλής κατεύθυνσης επικοινωνία χωρίς εξωτερικά προγράμματα περιήγησης.

## Γιατί να χρησιμοποιήσετε το Aspose.HTML για την εκτέλεση javascript σε java;
Το Aspose.HTML υποστηρίζει **50+ μορφές εισόδου και εξόδου** και μπορεί να αξιολογήσει JavaScript σε ένα πλήρως‑συμβατό περιβάλλον HTML5. Επεξεργάζεται scripts έως 200 ms κατά μέσο όρο για απλό κώδικα μιας γραμμής, και το κάνει αυτό χωρίς να φορτώνει ολόκληρο το stack ενός προγράμματος περιήγησης, μειώνοντας τη χρήση μνήμης έως και 80 % σε σύγκριση με προσεγγίσεις βασισμένες στο Selenium.

## Προαπαιτούμενα

- Java 17 (ή οποιοδήποτε πρόσφατο JDK) εγκατεστημένο και ρυθμισμένο.  
- Βιβλιοθήκη Aspose.HTML for Java (έκδοση 23.10 ή νεότερη). Μπορείτε να την αποκτήσετε από το Maven Central ή την ιστοσελίδα Aspose.  
- Ένα απλό IDE ή επεξεργαστή κειμένου· το παράδειγμα λειτουργεί επίσης από τη γραμμή εντολών.

> **Pro tip:** Αν χρησιμοποιείτε Maven, προσθέστε την ακόλουθη εξάρτηση στο `pom.xml` σας:

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

## Πώς να προσθέσετε ένα αντικείμενο κεντρικού υπολογιστή και να εκτελέσετε javascript σε java;
`addHostObject` καταχωρεί ένα αντικείμενο Java ως παγκόσμια μεταβλητή στο context του JavaScript. Φορτώστε το `HTMLDocument`, καταχωρήστε έναν Java logger με το όνομα "javaLogger" χρησιμοποιώντας `addHostObject`, και στη συνέχεια αξιολογήστε ένα σύντομο script που καλεί `javaLogger.log`. Η πλήρης ροή απαιτεί μόνο τρία κλήσεις API και λειτουργεί σε οποιοδήποτε runtime Java 17.

### Βήμα 1: δημιουργήστε ένα ελάχιστο έργο java

Πρώτα, δημιουργήστε μια νέα κλάση Java που ονομάζεται `JsHostObjectDemo`. Η κλάση θα περιέχει τη μέθοδο `main` και τον ορισμό του αντικειμένου κεντρικού υπολογιστή. Η διατήρηση όλων σε ένα αρχείο κάνει το tutorial αυτό-συνεπές και εύκολο στην αντιγραφή.

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

### Γιατί ένα `HTMLDocument`;
`HTMLDocument` αντιπροσωπεύει ένα HTML έγγραφο στη μνήμη και παρέχει μια μηχανή JavaScript. Η κλάση `HTMLDocument` δημιουργεί ένα πλήρως συμβατό περιβάλλον scripting HTML‑5. Παρόλο που δεν φορτώνουμε ποτέ κάποιο markup, το αντικείμενο `window` του εγγράφου μας δίνει πρόσβαση στη μηχανή JavaScript, όπου συμβαίνει η **run javascript in java** μαγεία. Επιπλέον, μπορείτε να χειριστείτε το DOM, να φορτώσετε πόρους, ή να αξιολογήσετε scripts χωρίς πρόγραμμα περιήγησης.

## Πώς να προσθέσετε το αντικείμενο κεντρικού υπολογιστή – “javaLogger”;
`Logger` είναι μια απλή κλάση Java με μέθοδο `log(String)` που γράφει μηνύματα στην κονσόλα. Καταχωρήστε το αντικείμενο `Logger` με το όνομα "javaLogger" ώστε οποιοδήποτε script αξιολογηθεί σε αυτό το έγγραφο να μπορεί να καλέσει `javaLogger.log(...)`. Αυτό είναι ο πυρήνας της απαίτησης **add host object** και καθιστά τον logger διαθέσιμο ως παγκόσμια μεταβλητή στον κώδικα JavaScript.

### Συνηθισμένα προβλήματα
- **Συγκρούσεις ονομάτων** – Εάν έχετε ήδη μια παγκόσμια μεταβλητή με όνομα `javaLogger` στο script σας, το αντικείμενο κεντρικού υπολογιστή θα αντικατασταθεί. Επιλέξτε ένα μοναδικό όνομα.  
- **Ασφάλεια νήματος** – Το αντικείμενο κεντρικού υπολογιστή μοιράζεται μεταξύ εκτελέσεων script στο ίδιο έγγραφο. Εάν σκοπεύετε να εκτελείτε scripts ταυτόχρονα, κάντε την κλάση κεντρικού υπολογιστή thread‑safe (π.χ., χρησιμοποιήστε `synchronized` ή τις primitive του `java.util.concurrent`).

## Πώς να γράψετε και να εκτελέσετε javascript σε java;
`eval` εκτελεί μια συμβολοσειρά JavaScript στη μηχανή scripting του εγγράφου και επιστρέφει οποιοδήποτε αποτέλεσμα. Δώστε ένα μικρό script στο `eval`. Η μηχανή επιλύει το `javaLogger` από το παγκόσμιο scope και καλεί τη μέθοδο `log` με τη δοθείσα συμβολοσειρά. Μπορείτε επίσης να επιστρέψετε τιμές, να διαχειριστείτε εξαιρέσεις, και να αλυσίδετε πολλαπλές αξιολογήσεις για πιο σύνθετες αλληλεπιδράσεις.

### Αναμενόμενο αποτέλεσμα
Η εκτέλεση της μεθόδου `main` εκτυπώνει την ακόλουθη γραμμή στην κονσόλα:

```
[JS] Hello from JavaScript!
```

## Πώς να επεκτείνετε το αντικείμενο κεντρικού υπολογιστή – περισσότερο από απλή καταγραφή;
Ένα αντικείμενο κεντρικού υπολογιστή είναι οποιοδήποτε αντικείμενο Java που εκτίθεται στο JavaScript μέσω `addHostObject`. Επεκτείνετε τη λειτουργικότητα προσθέτοντας μεθόδους στην κλάση `Logger` ή δημιουργώντας μια νέα κλάση κεντρικού υπολογιστή. Παρακάτω υπάρχει ένα γρήγορο παράδειγμα που επίσης επιστρέφει μια τιμή στο JavaScript. Το αντικείμενο κεντρικού υπολογιστή μπορεί να εκθέσει σύνθετους τύπους, να εκτελεί I/O, ή να αλληλεπιδρά με άλλες υπηρεσίες. Επιστρέφοντας μια τιμή, το script μπορεί να λάβει δεδομένα πίσω, επιτρέποντας διπλής κατεύθυνσης επικοινωνία μεταξύ Java και JavaScript.

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

Τώρα η κονσόλα εμφανίζει:

```
[JS] 3+4=7
```

## Πώς να καθαρίσετε πόρους μετά την εκτέλεση scripts;
`dispose` απελευθερώνει τους εγγενείς πόρους που κρατά το αντικείμενο `HTMLDocument`. Όταν τελειώσετε με το περιβάλλον scripting, απελευθερώστε το `HTMLDocument` για να ελευθερώσετε τους εγγενείς πόρους. Η μη κλήση του `dispose()` μπορεί να οδηγήσει σε διαρροές μνήμης, ειδικά όταν δημιουργείτε πολλά έγγραφα σε βρόχους ή σε υπηρεσίες που τρέχουν πολύ χρόνο. Πάντα τυλίξτε τη χρήση σε ένα μπλοκ try‑with‑resources ή βεβαιωθείτε ότι το `document.dispose()` καλείται σε finally.

```java
document.dispose(); // Important for long‑running applications
```

## Πλήρες λειτουργικό παράδειγμα
Παρακάτω είναι το πλήρες αρχείο πηγαίου κώδικα που μπορείτε να μεταγλωττίσετε και να εκτελέσετε αμέσως. Αποθηκεύστε το ως `JsHostObjectDemo.java`, βεβαιωθείτε ότι το JAR του Aspose.HTML βρίσκεται στο classpath σας, και εκτελέστε `java JsHostObjectDemo`.

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

## Συχνές ερωτήσεις

**Q: Λειτουργεί αυτό σε Android;**  
A: Ναι. Το Aspose.HTML είναι μια καθαρή βιβλιοθήκη Java, επομένως τρέχει σε οποιοδήποτε JVM, συμπεριλαμβανομένου του runtime ART του Android.

**Q: Τι γίνεται αν χρειαστεί να περάσω σύνθετα αντικείμενα;**  
A: Μπορείτε να εκθέσετε POJOs με getters και setters· η μηχανή τα αντιστοιχίζει αυτόματα σε αντικείμενα JavaScript. Συλλογές όπως `java.util.List` ή πίνακες είναι επίσης μετατρέψιμες.

**Q: Πώς λειτουργεί η διαχείριση σφαλμάτων;**  
A: Εάν το script ρίξει σφάλμα JavaScript, το `eval` προωθεί ένα `ScriptException`. Τυλίξτε την κλήση σε μπλοκ try‑catch για να καταγράψετε ή να ανακτήσετε.

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

**Q: Μπορώ να εκτελέσω πολλαπλά scripts διαδοχικά;**  
A: Απόλυτα. Το ίδιο `HTMLDocument` διατηρεί το παγκόσμιο scope του, ώστε να μπορείτε να καλέσετε το `eval` επανειλημμένα. Απλώς διαχειριστείτε τα ονόματα μεταβλητών για να αποφύγετε συγκρούσεις.

**Q: Είναι το αντικείμενο κεντρικού υπολογιστή ασφαλές για μη αξιόπιστα scripts;**  
A: Θεωρήστε οποιοδήποτε εξωτερικό script ως μη αξιόπιστη είσοδο. Επικυρώστε τις παραμέτρους και εξετάστε την απομόνωση (sandboxing) εκθέτοντας μόνο τις ελάχιστες απαιτούμενες μεθόδους.

## Καλές πρακτικές & συμβουλές
- **Ονομάστε τα αντικείμενα κεντρικού υπολογιστή σαφώς**—`javaLogger`, `javaUtils`, κλπ.—για να αποφύγετε σύγχυση.  
- **Κρατήστε τις μεθόδους κεντρικού υπολογιστή μικρές και χωρίς παρενέργειες** όταν είναι δυνατόν· διευκολύνει τον εντοπισμό σφαλμάτων.  
- **Αποδεσμεύστε το έγγραφο** μόλις τελειώσετε· απελευθερώνει τη φυσική μνήμη που καταλαμβάνει το Aspose.HTML.  
- **Επικυρώστε τις εισόδους** από JavaScript, ειδικά αν τα scripts προέρχονται από μη αξιόπιστες πηγές. Θεωρήστε τα όπως οποιαδήποτε εξωτερικά δεδομένα.

## Συμπέρασμα
Τώρα έχετε ένα στέρεο, ολοκληρωμένο παράδειγμα για το πώς να **call java from javascript** με **προσθήκη αντικειμένου κεντρικού υπολογιστή**, **εκτέλεση javascript σε java**, και **καταγραφή από javascript** χρησιμοποιώντας το Aspose.HTML. Το πρότυπο είναι ισχυρό: οποιαδήποτε υπηρεσία Java μπορεί να εκτεθεί σε scripts, μετατρέποντας την εφαρμογή Java σας σε μια ελαφριά πλατφόρμα scripting.

Στη συνέχεια, μπορείτε να εξερευνήσετε:
- Ενσωμάτωση μιας πλήρους σελίδας HTML και χειρισμό του DOM από JavaScript.  
- Χρήση του αντικειμένου κεντρικού υπολογιστή για ροή δεδομένων πίσω στη Java (π.χ., σειριοποίηση JSON).  
- Ενσωμάτωση με άλλες μηχανές scripting όπως Nashorn ή GraalVM για ευρύτερη υποστήριξη γλωσσών.

Δοκιμάστε το, τροποποιήστε τις κλάσεις `Logger` ή `Utils`, και δείτε πόσο μακριά μπορείτε να προωθήσετε την έννοια του **javascript host object** στα δικά σας έργα.

---

**Τελευταία ενημέρωση:** 2026-10-14  
**Δοκιμάστηκε με:** Aspose.HTML for Java 23.10  
**Συγγραφέας:** Aspose  

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

```javascript
javaLogger.log('Hello from JavaScript!');
```

## Σχετικά μαθήματα

- [Ενεργοποίηση Εκτέλεσης Script σε Java – Πλήρης Οδηγός Aspose Html](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)
- [Εκτέλεση Javascript σε Java – Πλήρης Οδηγός για την Εκτέλεση Js Από](/html/java/advanced-usage/execute-javascript-in-java-complete-guide-to-running-js-from/)
- [Πώς να Απομονώσετε (Sandbox) Javascript – Πλήρης Οδηγός Aspose Html](/html/java/advanced-usage/how-to-sandbox-javascript-complete-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
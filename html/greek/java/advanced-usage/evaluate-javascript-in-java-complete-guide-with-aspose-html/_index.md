---
category: general
date: 2026-04-03
description: Αξιολογήστε JavaScript σε Java χρησιμοποιώντας το Aspose.HTML – μάθετε
  πώς να εκτελείτε JavaScript από Java, να ορίζετε innerHTML και να καλείτε συναρτήσεις
  σε ένα ενιαίο σεμινάριο.
draft: false
keywords:
- evaluate javascript in java
- set innerhtml javascript
- run javascript from java
- invoke javascript function java
language: el
og_description: Μάθετε πώς να αξιολογείτε JavaScript σε Java, να ορίζετε innerHTML,
  να εκτελείτε σενάρια και να καλείτε συναρτήσεις χρησιμοποιώντας το Aspose.HTML σε
  ένα σύντομο, εκτελέσιμο παράδειγμα.
og_title: Αξιολόγηση JavaScript σε Java – Οδηγός βήμα‑προς‑βήμα
tags:
- Aspose.HTML
- Java
- JavaScript
title: Αξιολόγηση JavaScript σε Java – Πλήρης Οδηγός με το Aspose.HTML
url: /el/java/advanced-usage/evaluate-javascript-in-java-complete-guide-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αξιολόγηση JavaScript σε Java – Πλήρης Οδηγός με Aspose.HTML

Έχετε ποτέ χρειαστεί να **αξιολογήσετε JavaScript σε Java** αλλά δεν ήσασταν σίγουροι ποιο API μπορεί να γεφυρώσει το κενό; Δεν είστε μόνοι· πολλοί προγραμματιστές Java αντιμετωπίζουν αυτό το πρόβλημα όταν προσπαθούν να χειριστούν HTML ή να εκτελέσουν λογική στην πλευρά του πελάτη στον διακομιστή. Τα καλά νέα; Η Aspose.HTML σας παρέχει μια μηχανή script που σας επιτρέπει να **εκτελείτε JavaScript από Java**, να αλλάζετε το DOM και να καλείτε συναρτήσεις—όλα χωρίς πρόγραμμα περιήγησης.

Σε αυτό το tutorial θα δείτε ακριβώς πώς να **ορίσετε innerHTML JavaScript** από Java, να καλέσετε μια συνάρτηση JavaScript και να λάβετε τα αποτελέσματα πίσω στον κώδικα Java. Στο τέλος θα έχετε ένα αυτόνομο, έτοιμο για αντιγραφή‑επικόλληση παράδειγμα που λειτουργεί με την πιο πρόσφατη έκδοση της Aspose.HTML for Java (v23.12 τη στιγμή της συγγραφής). Χωρίς εξωτερικά έγγραφα, χωρίς ασαφείς αναφορές—μόνο κώδικας, εξηγήσεις και μερικές επαγγελματικές συμβουλές.

## Τι Θα Χρειαστεί

- **Java 17** (ή οποιοδήποτε πρόσφατο JDK· το API είναι συμβατό με Java‑8)
- **Aspose.HTML for Java** JARs στο classpath σας (κατεβάστε από την επίσημη ιστοσελίδα της Aspose)
- Ένα απλό IDE όπως IntelliJ IDEA ή VS Code, αλλά λειτουργεί και ένας απλός επεξεργαστής κειμένου
- Περιέργεια να πειραματιστείτε με το DOM από τη Java

Αν τα έχετε ήδη, υπέροχα—ας προχωρήσουμε κατευθείαν στη λύση.

## Βήμα 1: Δημιουργία Κενής HTML Εγγράφου – Καμβάς για Αξιολόγηση

Το πρώτο που κάνουμε είναι να δημιουργήσουμε ένα κενό `HTMLDocument`. Σκεφτείτε το ως μια φρέσκια σελίδα HTML που υπάρχει μόνο στη μνήμη· μπορείτε να προσθέσετε scripts, να τροποποιήσετε στοιχεία και να ερωτήσετε το DOM χωρίς ποτέ να γράψετε αρχείο.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class JavaScriptEvalTutorial {
    public static void main(String[] args) throws Exception {

        // Step 1 – create an in‑memory HTML document
        try (HTMLDocument document = new HTMLDocument()) {
            // All further actions happen inside this try‑with‑resources block
```

> **Γιατί είναι σημαντικό:**  
> Η Aspose.HTML απομονώνει τη μηχανή script από το κεντρικό JVM, ώστε να μην μολύνει κατά λάθος το classpath της εφαρμογής σας. Το έγγραφο σας παρέχει επίσης ένα `ScriptEngine` που σέβεται τα ίδια πρότυπα JavaScript όπως θα έκανε ένας περιηγητής.

## Βήμα 2: Προσθήκη Στοιχείου `<script>` – Ορισμός της Συνάρτησης που Θα Καλέσετε

Στη συνέχεια ενσωματώνουμε μια απλή συνάρτηση JavaScript. Σε πραγματικά έργα μπορείτε να φορτώσετε ένα εξωτερικό αρχείο ή ακόμη και να δημιουργήσετε το script δυναμικά.

```java
            // Step 2 – embed a JavaScript function into the <head>
            String functionScript = "function add(a,b){ return a+b; }";
            document.getHead()
                    .appendChild(document.createElement("script"))
                    .setTextContent(functionScript);
```

> **Συμβουλή επαγγελματία:**  
> Χρησιμοποιήστε `document.createElement("script")` αντί για την ένωση συμβολοσειρών στο HTML· εξασφαλίζει σωστή κωδικοποίηση και αποτρέπει σφάλματα τύπου XSS όταν το script περιέχει εισαγωγικά.

## Βήμα 3: Λήψη της Μηχανής Script – Η Γέφυρα μεταξύ Java & JavaScript

Η Aspose.HTML παρέχει ένα `ScriptEngine` που ακολουθεί το συμβόλαιο JSR‑223 (javax.script). Μonce το έχετε, μπορείτε να `eval` αυθαίρετο κώδικα ή να καλέσετε απευθείας ονομαστικές συναρτήσεις.

```java
            // Step 3 – obtain the JavaScript engine tied to the document
            ScriptEngine scriptEngine = document.getScriptEngine();
```

> **Τι συμβαίνει στο παρασκήνιο;**  
> Η μηχανή είναι ένας ελαφρύς ερμηνευτής βασισμένος στο V8. Σέβεται το τρέχον πλαίσιο `document`, πράγμα που σημαίνει ότι οποιαδήποτε αλλαγή DOM κάνετε μέσα στο `eval` θα επηρεάσει το ίδιο αντικείμενο `HTMLDocument`.

## Βήμα 4: Κλήση Συνάρτησης JavaScript από Java – `invokeFunction` σε Δράση

Τώρα το διασκεδαστικό μέρος: η κλήση της συνάρτησης `add` που μόλις ορίσαμε. Η μέθοδος `invokeFunction` παίρνει το όνομα της συνάρτησης ακολουθούμενο από τυχόν επιχειρήματα που θέλετε να περάσετε.

```java
            // Step 4 – call the JavaScript function directly from Java
            Object addResult = scriptEngine.invokeFunction("add", 7, 13);
            System.out.println("Result of add(7,13): " + addResult); // prints 20
```

> **Γιατί να χρησιμοποιήσετε το `invokeFunction`;**  
> Παρακάμπτει το κόστος ανάλυσης μιας πλήρους συμβολοσειράς script και σας παρέχει επιχειρήματα τύπου‑ασφαλή. Η τιμή επιστροφής μετατρέπεται αυτόματα σε Java `Object`, το οποίο μπορείτε να κάνετε cast αν χρειαστεί.

## Βήμα 5: Αξιολόγηση Αυθαίρετης Έκφρασης JavaScript – Ορισμός `innerHTML` από Java

Τέλος, επιδεικνύουμε **ορισμό innerHTML JavaScript** εκτελώντας ένα απόσπασμα που τροποποιεί το σώμα της σελίδας και επιστρέφει το κείμενο περιεχομένου.

```java
            // Step 5 – evaluate a script that changes the DOM
            Object evalResult = scriptEngine.eval(
                    "document.body.innerHTML = '<p>Hello</p>'; document.body.textContent;");
            System.out.println("Body text: " + evalResult); // prints \"Hello\"
        }
    }
}
```

> **Τι να περιμένετε:**  
> Μετά την εκτέλεση του `eval`, το `<body>` του εγγράφου στη μνήμη περιέχει τώρα `<p>Hello</p>`. Η έκφραση διαβάζει έπειτα `document.body.textContent`, το οποίο η μηχανή επιστρέφει στη Java ως συμβολοσειρά. Αυτό δείχνει τη δύναμη του **εκτέλεσης JavaScript από Java** διατηρώντας όλα τύπου‑ασφαλή.

---

![παράδειγμα αξιολόγησης javascript σε java](https://example.com/images/eval-js-in-java.png)

*Κείμενο εναλλακτικής εικόνας: παράδειγμα αξιολόγησης javascript σε java – δείχνει μια κονσόλα Java που εκτυπώνει αποτελέσματα*

## Συνηθισμένες Παραλλαγές & Ακραίες Περιπτώσεις

### Διαχείριση Ασύγχρονου Κώδικα

Αν το script σας χρησιμοποιεί `setTimeout` ή promises, θα χρειαστεί να καλέσετε `scriptEngine.eval` μέσα σε βρόχο που ελέγχει `scriptEngine.getContext().getAttribute("javax.script.pending")`. Στις περισσότερες περιπτώσεις διακομιστή, ο συγχρονισμένος κώδικας (όπως φαίνεται) είναι επαρκής.

### Μετάδοση Σύνθετων Αντικειμένων

Μπορείτε να εκθέσετε ένα αντικείμενο Java στο JavaScript μέσω `scriptEngine.put("javaObj", myObject)`. Μέσα στο script, το `javaObj` συμπεριφέρεται ως ένα κανονικό αντικείμενο Java, επιτρέποντάς σας να καλέσετε τις δημόσιες μεθόδους του.

### Διαχείριση Σφαλμάτων

Τυλίξτε το `scriptEngine.eval` σε μπλοκ try‑catch για `ScriptException`. Το μήνυμα της εξαίρεσης περιλαμβάνει τον αριθμό γραμμής και ένα stack trace JavaScript, καθιστώντας τον εντοπισμό σφαλμάτων απλό.

```java
try {
    scriptEngine.eval("invalid code");
} catch (ScriptException ex) {
    System.err.println("Script error: " + ex.getMessage());
}
```

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω βρίσκεται το πλήρες πρόγραμμα, ακριβώς όπως θα το τοποθετήσετε στο `src/main/java/JavaScriptEvalTutorial.java`.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class JavaScriptEvalTutorial {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a blank HTML document that will host the script
        try (HTMLDocument document = new HTMLDocument()) {

            // Step 2: Add a <script> element defining a simple JavaScript function
            String functionScript = "function add(a,b){ return a+b; }";
            document.getHead()
                    .appendChild(document.createElement("script"))
                    .setTextContent(functionScript);

            // Step 3: Obtain the script engine associated with the document
            ScriptEngine scriptEngine = document.getScriptEngine();

            // Step 4: Call the JavaScript function directly from Java
            Object addResult = scriptEngine.invokeFunction("add", 7, 13);
            System.out.println("Result of add(7,13): " + addResult); // prints 20

            // Step 5: Evaluate an arbitrary JavaScript expression that modifies the page
            Object evalResult = scriptEngine.eval(
                    "document.body.innerHTML = '<p>Hello</p>'; document.body.textContent;");
            System.out.println("Body text: " + evalResult); // prints "Hello"
        }
    }
}
```

**Αναμενόμενη έξοδος κονσόλας**

```
Result of add(7,13): 20
Body text: Hello
```

Αν δείτε αυτές τις δύο γραμμές, έχετε επιτυχώς **αξιολογήσει JavaScript σε Java**, **ορίσει innerHTML JavaScript**, και **καλέσει συνάρτηση JavaScript από Java**—όλα σε μία ενέργεια.

## Περίληψη & Επόμενα Βήματα

Διασχίσαμε ολόκληρο τον κύκλο ζωής της **αξιολόγησης JavaScript σε Java** με την Aspose.HTML:

1. Δημιουργήστε ένα `HTMLDocument` στη μνήμη.  
2. Ενσωματώστε μια ετικέτα `<script>` που περιέχει τη συνάρτηση που θέλετε να καλέσετε.  
3. Λάβετε το `ScriptEngine` που συνδέεται με αυτό το έγγραφο.  
4. Χρησιμοποιήστε `invokeFunction` για **να εκτελέσετε JavaScript από Java** και να λάβετε ένα αποτέλεσμα.  
5. Χρησιμοποιήστε `eval` για **να ορίσετε innerHTML JavaScript** και να ανακτήσετε δεδομένα DOM.

Από εδώ μπορείτε να εξερευνήσετε:

- **Φόρτωση εξωτερικών scripts** με `document.createElement("script").setAttribute("src", "...")`.
- **Διαχείριση CSS** μέσω `document.body.style`.
- **Εκτέλεση μεγαλύτερων βιβλιοθηκών** όπως Lodash ή Moment.js μέσα στη μηχανή.

Νιώστε ελεύθεροι να πειραματιστείτε—αντικαταστήστε τη συνάρτηση `add` με κάτι πιο σύνθετο, ή περάστε συμβολοσειρές JSON στο script και αναλύστε τις ξανά στη Java. Οι δυνατότητες είναι ανοιχτές όπως η κονσόλα ενός περιηγητή, αλλά με την ασφάλεια και την απόδοση μιας διαδικασίας Java στο διακομιστή.

Έχετε ερωτήσεις ή αντιμετωπίσατε πρόβλημα; Αφήστε ένα σχόλιο, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
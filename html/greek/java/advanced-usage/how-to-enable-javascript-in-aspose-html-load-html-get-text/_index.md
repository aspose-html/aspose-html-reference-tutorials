---
category: general
date: 2026-01-06
description: Πώς να ενεργοποιήσετε τη JavaScript στο Aspose HTML και να φορτώσετε
  HTML με JS για να λάβετε το κείμενο ενός στοιχείου. Αυτός ο οδηγός σας δείχνει πώς
  να φορτώσετε HTML JavaScript, να εξάγετε το κείμενο του στοιχείου και να διαχειριστείτε
  τις αλλαγές του DOM.
draft: false
keywords:
- how to enable javascript
- load html javascript
- get element text
- load html with js
- extract element text
language: el
og_description: Πώς να ενεργοποιήσετε τη JavaScript στο Aspose HTML, να φορτώσετε
  HTML με JS και να εξάγετε το κείμενο στοιχείου από δυναμικές σελίδες σε λίγα εύκολα
  βήματα.
og_title: Πώς να ενεργοποιήσετε τη JavaScript στο Aspose HTML – Φόρτωση HTML & Λήψη
  κειμένου
tags:
- Aspose HTML
- Java
- JavaScript sandbox
title: Πώς να ενεργοποιήσετε τη JavaScript στο Aspose HTML – Φόρτωση HTML & Λήψη κειμένου
url: /el/java/advanced-usage/how-to-enable-javascript-in-aspose-html-load-html-get-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ενεργοποιήσετε τη JavaScript στο Aspose HTML – Φόρτωση HTML & Λήψη Κειμένου

Έχετε αναρωτηθεί ποτέ **πώς να ενεργοποιήσετε τη javascript** κατά την απόδοση μιας σελίδας με Aspose HTML; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν μια σελίδα που βασίζεται σε script δεν εμφανίζει ποτέ το περιεχόμενο που αναμένουν, επειδή η μηχανή παραλείπει σιωπηλά τη JavaScript.  

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα τις ακριβείς ενέργειες για να ενεργοποιήσετε τη JavaScript, να φορτώσετε ένα αρχείο HTML που περιέχει scripts, και τελικά **να λάβετε το κείμενο του στοιχείου** από το DOM. Στο τέλος θα γνωρίζετε επίσης πώς να **φορτώνετε html javascript**, **φορτώνετε html με js**, και **εξάγετε το κείμενο του στοιχείου** χωρίς να διασπάσετε το sandbox.

> **Προαπαιτούμενα** – Java 17+, Aspose.HTML for Java (τελευταία έκδοση), και βασική κατανόηση του HTML/JavaScript. Δεν απαιτούνται εξωτερικές βιβλιοθήκες.

![Διάγραμμα που δείχνει πώς να ενεργοποιήσετε τη javascript στο Aspose HTML](/images/enable-js-diagram.png "πώς να ενεργοποιήσετε τη javascript στο Aspose HTML")

---

## Βήμα 1 – Πώς να ενεργοποιήσετε τη JavaScript στο Aspose HTML

Το πρώτο που πρέπει να κάνετε είναι να ενημερώσετε το αντικείμενο `HtmlLoadOptions` ότι η εκτέλεση script επιτρέπεται. Από προεπιλογή η μηχανή απενεργοποιεί τη JavaScript για ασφάλεια, επομένως πρέπει να την ενεργοποιήσετε ρητά.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class JsSandbox {
    public static void main(String[] args) throws Exception {

        // Step 1: Create load options and enable JavaScript execution
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        loadOptions.setEnableJavaScript(true);   // allow scripts to run
        loadOptions.setSandboxEnabled(true);     // isolate script execution
```

*Γιατί είναι σημαντικό*: Η ενεργοποίηση της JavaScript (`setEnableJavaScript(true)`) δίνει στη σελίδα τη δυνατότητα να χειριστεί το DOM. Το sandbox (`setSandboxEnabled(true)`) αποτρέπει αυτά τα scripts από το να επηρεάσουν το περιβάλλον σας, κάτι που είναι ιδιαίτερα σημαντικό όταν επεξεργάζεστε μη αξιόπιστο HTML.

---

## Βήμα 2 – Φόρτωση HTML με JavaScript

Τώρα που η JavaScript είναι ενεργοποιημένη, μπορούμε πραγματικά να φορτώσουμε μια σελίδα που περιέχει scripts. Το παρακάτω παράδειγμα υποθέτει ότι υπάρχει ένα αρχείο με όνομα `dynamic.html` σε έναν φάκελο που ελέγχετε.

```java
        // Step 2: Load the HTML page that contains JavaScript which modifies the DOM
        HtmlDocument document = new HtmlDocument("YOUR_DIRECTORY/dynamic.html", loadOptions);
```

Παρατηρήστε πώς περνάμε το ίδιο αντικείμενο `loadOptions` που διαμορφώσαμε στο προηγούμενο βήμα. Αυτό είναι το σημείο όπου το **load html javascript** γίνεται αποτελεσματικό – η μηχανή διαβάζει το αρχείο, εκτελεί τυχόν ετικέτες `<script>` και δημιουργεί το τελικό δέντρο DOM.

> **Συμβουλή** – Αν χρειάζεται να φορτώσετε HTML από μια συμβολοσειρά ή ροή, χρησιμοποιήστε την υπερφόρτωση `HtmlDocument(InputStream, HtmlLoadOptions)`. Οι ίδιες επιλογές εξακολουθούν να ελέγχουν την εκτέλεση script.

---

## Βήμα 3 – Λήψη Κειμένου Στοιχείου από το Αποδομένο DOM

Αφού εκτελεστεί το script, η σελίδα θα πρέπει να έχει δημιουργήσει ένα νέο στοιχείο (για παράδειγμα, ένα `<div id="generated">`). Τώρα μπορούμε να ερωτήσουμε το έγγραφο όπως θα κάναμε σε ένα πρόγραμμα περιήγησης.

```java
        // Step 3: After the script runs, locate the element created by the script
        Element generatedElement = document.querySelector("#generated");

        // Step 4: Output the text content of the generated element
        System.out.println("Generated text: " + generatedElement.getTextContent());
    }
}
```

Η κλήση στο `querySelector("#generated")` αποτελεί το τμήμα **get element text** της ροής εργασίας. Μόλις έχουμε το αντικείμενο `Element`, η μέθοδος `getTextContent()` επιστρέφει τη συμβολοσειρά που εισήγαγε η JavaScript.

**Αναμενόμενη έξοδος** (υποθέτοντας ότι το `dynamic.html` γράφει “Hello from JS!” στο στοιχείο):

```
Generated text: Hello from JS!
```

Αν το στοιχείο δεν βρεθεί, το `generatedElement` θα είναι `null`. Σε παραγωγικό σενάριο θα προστατεύατε τον κώδικα από αυτό:

```java
if (generatedElement != null) {
    System.out.println("Generated text: " + generatedElement.getTextContent());
} else {
    System.err.println("Element #generated not found – check your script.");
}
```

---

## Βήμα 4 – Ασφαλής Εξαγωγή Κειμένου Στοιχείου (Περιπτώσεις Άκρων)

Μερικές φορές τα scripts εκτελούνται ασύγχρονα ή εξαρτώνται από εξωτερικούς πόρους. Το Aspose HTML εκτελεί τα scripts συγχρονισμένα, αλλά μπορεί να αντιμετωπίσετε προβλήματα χρονισμού. Ένα αξιόπιστο μοτίβο είναι:

1. **Ενεργοποιήστε τη JavaScript** (όπως κάναμε).  
2. **Περιμένετε το DOM να σταθεροποιηθεί** – μπορείτε να ελέγχετε το στοιχείο με σύντομο χρονικό όριο.  
3. **Εξάγετε το κείμενο** μόλις εμφανιστεί το στοιχείο.

```java
int attempts = 0;
Element generated = null;
while (attempts < 5 && generated == null) {
    generated = document.querySelector("#generated");
    if (generated == null) Thread.sleep(200); // small pause
    attempts++;
}
if (generated != null) {
    System.out.println("Extracted text: " + generated.getTextContent());
} else {
    System.out.println("Failed to locate #generated after waiting.");
}
```

Αυτό το απόσπασμα δείχνει έναν πρακτικό τρόπο για **εξαγωγή κειμένου στοιχείου** ακόμη και όταν το script χρειάζεται λίγο χρόνο για να ολοκληρωθεί. Είναι μια μικρή προσθήκη, αλλά σας προστατεύει από μυστηριώδη αποτελέσματα `null`.

---

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα, εδώ είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα:

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class JsSandbox {
    public static void main(String[] args) throws Exception {

        // Enable JavaScript and sandbox the execution
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        loadOptions.setEnableJavaScript(true);
        loadOptions.setSandboxEnabled(true);

        // Load the HTML file that contains a script creating #generated
        HtmlDocument document = new HtmlDocument("YOUR_DIRECTORY/dynamic.html", loadOptions);

        // Optional: wait a bit for async‑like scripts
        int attempts = 0;
        Element generated = null;
        while (attempts < 5 && generated == null) {
            generated = document.querySelector("#generated");
            if (generated == null) Thread.sleep(200);
            attempts++;
        }

        // Retrieve and print the text
        if (generated != null) {
            System.out.println("Generated text: " + generated.getTextContent());
        } else {
            System.err.println("Element #generated not found – verify your JavaScript.");
        }
    }
}
```

Αποθηκεύστε το ως `JsSandbox.java`, αντικαταστήστε το `YOUR_DIRECTORY/dynamic.html` με την πραγματική διαδρομή, μεταγλωττίστε με `javac` και εκτελέστε με `java`. Θα πρέπει να δείτε το κείμενο που εισήγαγε το script.

---

## Συχνές Ερωτήσεις

**Ε: Λειτουργεί αυτό με εξωτερικά αρχεία script;**  
Α: Ναι. Εφόσον τα URLs των script είναι προσβάσιμα από το μηχάνημα που εκτελεί τον κώδικα, η μηχανή θα τα κατεβάσει και θα τα εκτελέσει. Θυμηθείτε να διατηρείτε το `setSandboxEnabled(true)` για να αποτρέψετε ανεπιθύμητες παρενέργειες.

**Ε: Τι γίνεται αν χρειαστεί να απενεργοποιήσω τη JavaScript για μια συγκεκριμένη σελίδα;**  
Α: Απλώς ορίστε `loadOptions.setEnableJavaScript(false)` πριν φορτώσετε εκείνη τη σελίδα. Αυτό είναι χρήσιμο όταν θέλετε μόνο να εξάγετε στατικό περιεχόμενο.

**Ε: Μπορώ να το τρέξω σε headless server;**  
Α: Απόλυτα. Το Aspose.HTML είναι μια καθαρή βιβλιοθήκη Java· δεν απαιτείται πρόγραμμα περιήγησης ή UI.

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να ενεργοποιήσετε τη javascript** στο Aspose HTML, πώς να **φορτώνετε html με js**, και τα ακριβή βήματα για **να λάβετε το κείμενο του στοιχείου** και **να εξάγετε το κείμενο του στοιχείου** από μια δυναμικά παραγόμενη σελίδα. Τα βασικά σημεία είναι:

* Ενεργοποιήστε τη JavaScript μέσω `HtmlLoadOptions.setEnableJavaScript(true)`.  
* Διατηρήστε το sandbox ενεργό για ασφάλεια.  
* Χρησιμοποιήστε `querySelector` (ή άλλες DOM APIs) για να εντοπίσετε στοιχεία που δημιουργήθηκαν από scripts.  
* Προαιρετικά ελέγξτε (poll) για το στοιχείο αν το script χρειάζεται λίγο χρόνο για να ολοκληρωθεί.

Από εδώ μπορείτε να πειραματιστείτε με πιο σύνθετα σενάρια—πολλαπλά scripts, διατάξεις που καθορίζονται από CSS, ή ακόμη και HTML5 APIs. Το μοτίβο παραμένει το ίδιο: ενεργοποίηση, φόρτωση, ερώτημα και εξαγωγή. Καλή προγραμματιστική δουλειά, και απολαύστε τη δύναμη της επεξεργασίας HTML με ενεργοποιημένη JavaScript!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
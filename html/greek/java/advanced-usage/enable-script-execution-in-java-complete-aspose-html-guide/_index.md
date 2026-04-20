---
category: general
date: 2026-02-13
description: Ενεργοποιήστε την εκτέλεση σεναρίων κατά τη φόρτωση ενός εγγράφου HTML
  με το Aspose.HTML. Μάθετε πώς να ορίζετε το χρονικό όριο του σεναρίου, να χρησιμοποιείτε
  το query selector Java και να λαμβάνετε το υπολογισμένο φόντο σε ένα ενιαίο σεμινάριο.
draft: false
keywords:
- enable script execution
- set script timeout
- load html document
- query selector java
- get computed background
language: el
og_description: Ενεργοποιήστε την εκτέλεση σεναρίων σε Java με το Aspose.HTML. Αυτός
  ο οδηγός δείχνει πώς να ορίσετε το χρονικό όριο σεναρίου, να φορτώσετε έγγραφο HTML,
  να χρησιμοποιήσετε το query selector Java και να λάβετε το υπολογισμένο φόντο.
og_title: Ενεργοποίηση Εκτέλεσης Σεναρίου σε Java – Εκπαιδευτικό Σεμινάριο Aspose.HTML
tags:
- Aspose.HTML
- Java
- DOM Manipulation
title: Ενεργοποίηση Εκτέλεσης Σεναρίων σε Java – Πλήρης Οδηγός Aspose.HTML
url: /el/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ενεργοποίηση Εκτέλεσης Σεναρίων σε Java – Πλήρης Οδηγός Aspose.HTML

Έχετε αναρωτηθεί ποτέ πώς να **ενεργοποιήσετε την εκτέλεση σεναρίων** όταν επεξεργάζεστε ένα αρχείο HTML σε Java; Ίσως χτίζετε έναν server‑side renderer, ή απλώς χρειάζεστε να εξάγετε τιμές που δημιουργούνται από JavaScript κατά το χρόνο εκτέλεσης. Σε αυτό το tutorial θα δείτε ακριβώς πώς να ενεργοποιήσετε την εκτέλεση σεναρίων, **να ορίσετε το χρονικό όριο σεναρίου**, και να αντλήσετε το υπολογισμένο χρώμα φόντου από ένα δυναμικό στοιχείο — όλα με το Aspose.HTML.

Θα περάσουμε από τη φόρτωση ενός εγγράφου HTML, τη ρύθμιση της μηχανής, την αναμονή για την ολοκλήρωση των σεναρίων, και τέλος τη χρήση του **query selector java** για να εντοπίσουμε το στοιχείο που μας ενδιαφέρει. Στο τέλος, θα μπορείτε να **λάβετε το υπολογισμένο φόντο** χωρίς να βγείτε από το οικοσύστημα της Java.

## Προαπαιτούμενα

- Java 17 ή νεότερη (ο κώδικας συντάσσεται και με παλαιότερες εκδόσεις, αλλά συνιστάται η 17)
- Aspose.HTML for Java 23.12 ή νεότερη – μπορείτε να κατεβάσετε το Maven artifact `com.aspose:aspose-html:23.12`
- Ένα απλό αρχείο HTML (`scripted.html`) που περιέχει ένα script που τροποποιεί ένα στοιχείο με `id="dynamicDiv"`

Δεν απαιτούνται πρόσθετα frameworks· η βιβλιοθήκη διαχειρίζεται τα πάντα εσωτερικά.

---

## Βήμα 1 – Φόρτωση Εγγράφου HTML και Ενεργοποίηση Εκτέλεσης Σεναρίου

Το πρώτο που πρέπει να κάνετε είναι **να φορτώσετε το html έγγραφο** σε ένα αντικείμενο `HtmlDocument`. Από προεπιλογή το Aspose.HTML ενεργοποιεί ήδη την εκτέλεση σεναρίων, αλλά θα το ορίσουμε ρητά ώστε η πρόθεση να είναι ξεκάθαρη.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;

public class JsAndDomTutorial {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML file that contains JavaScript
        HtmlDocument htmlDoc = new HtmlDocument("YOUR_DIRECTORY/scripted.html", new LoadOptions());

        // Explicitly enable script execution – this is the key line
        htmlDoc.getWindow().setScriptsEnabled(true);
```

> **Γιατί είναι σημαντικό:** Αν τα σενάρια είναι απενεργοποιημένα, οποιοδήποτε JavaScript που τροποποιεί το DOM θα αγνοηθεί, και δεν θα μπορείτε ποτέ να **λάβετε το υπολογισμένο φόντο** αργότερα.

---

## Βήμα 2 – Ορισμός Χρονικού Ορίου Σεναρίου για Αποφυγή Παγώματος

Η εκτέλεση μη αξιόπιστων σεναρίων μπορεί να είναι επικίνδυνη. Το Aspose.HTML σας επιτρέπει να **ορίσετε χρονικό όριο σεναρίου** ώστε η μηχανή να διακόπτει οποιοδήποτε script τρέχει περισσότερο από τα καθορισμένα χιλιοστά του δευτερολέπτου. Εδώ δίνουμε στα σενάρια έως 5 δευτερόλεπτα.

```java
        // Step 2: Allow scripts up to 5 seconds before timing out
        htmlDoc.getWindow().setTimeout(5000);
```

> **Pro tip:** 5 δευτερόλεπτα είναι γενναιόδωρα για τις περισσότερες απλές σελίδες. Για βαρύτερες βιβλιοθήκες (όπως Chart.js) ίσως χρειαστεί να αυξήσετε το όριο στα 10 000 ms. Θυμηθείτε, ένα μικρότερο όριο κάνει την υπηρεσία σας πιο ανθεκτική σε κακόβουλο κώδικα.

---

## Βήμα 3 – Δώστε Χρόνο στα Σενάρια να Ολοκληρωθούν

Η εκτέλεση JavaScript είναι ασύγχρονη. Μια σύντομη παύση επιτρέπει στη μηχανή να ολοκληρώσει τυχόν εκκρεμείς χρονομετρητές ή promises. Θα μπορούσατε να ελέγχετε το `document.readyState`, αλλά ένα απλό `Thread.sleep` αρκεί για τις περισσότερες περιπτώσεις επίδειξης.

```java
        // Step 3: Pause the thread so scripts can finish (2 seconds is usually enough)
        Thread.sleep(2000);
```

> **Τι γίνεται αν χρειάζεστε μεγαλύτερη ακρίβεια;** Αντικαταστήστε το `Thread.sleep` με έναν βρόχο που ελέγχει `htmlDoc.getReadyState() == "complete"` – έτσι περιμένετε ακριβώς όσο χρειάζεται.

---

## Βήμα 4 – Εντοπισμός του Δυναμικού Στοιχείου με Query Selector Java

Τώρα που η σελίδα έχει σταθεροποιηθεί, μπορούμε να χρησιμοποιήσουμε **query selector java** για να πάρουμε το στοιχείο του οποίου το στυλ άλλαξε από το script. Ο selector `#dynamicDiv` ταιριάζει με το `<div id="dynamicDiv">` που αναμένουμε να υπάρχει.

```java
        // Step 4: Find the element that the script modified
        Element dynamicDiv = htmlDoc.querySelector("#dynamicDiv");
        if (dynamicDiv != null) {
```

> **Κοινό λάθος:** Η παράλειψη του `#` για έναν selector ID. Το `querySelector("dynamicDiv")` θα έψαχνε για ένα `<dynamicDiv>` tag, το οποίο προφανώς δεν υπάρχει.

---

## Βήμα 5 – Ανάκτηση του Υπολογισμένου Χρώματος Φόντου

Τέλος, **παίρνουμε το υπολογισμένο φόντο** από το υπολογισμένο στυλ του στοιχείου. Αυτό αντικατοπτρίζει την τελική τιμή μετά την εφαρμογή όλων των κανόνων CSS και των αλλαγών JavaScript.

```java
            // Step 5: Read the computed background color
            String backgroundColor = dynamicDiv.getComputedStyle().getBackgroundColor();
            System.out.println("Computed background: " + backgroundColor);
        } else {
            System.out.println("Element #dynamicDiv not found.");
        }

        // Clean up resources
        htmlDoc.dispose();
    }
}
```

**Αναμενόμενο αποτέλεσμα** (υποθέτοντας ότι το script ορίζει `background-color: rgb(255, 0, 0)`):

```
Computed background: rgb(255, 0, 0)
```

Αν το script χρησιμοποιεί ένα χρωματικό όνομα όπως `red`, η υπολογισμένη τιμή θα επιστραφεί ακόμη και έτσι σε μορφή `rgb(...)`.

---

## Ακραίες Περιπτώσεις & Παραλλαγές

| Κατάσταση | Τι να Αλλάξετε | Λόγος |
|-----------|----------------|--------|
| **Πολλά σενάρια χρειάζονται περισσότερο χρόνο** | Αυξήστε το όριο (`setTimeout(10000)`) | Αποτρέψτε πρόωρη διακοπή |
| **Το HTML φορτώνεται από URL** | Χρησιμοποιήστε `new HtmlDocument("https://example.com", new LoadOptions())` | Λειτουργεί με τον ίδιο τρόπο όπως με διαδρομή αρχείου |
| **Πρέπει να περιμένετε μια συγκεκριμένη αλλαγή στο DOM** | Ελέγξτε `dynamicDiv.getComputedStyle().getBackgroundColor()` σε βρόχο με μικρή παύση | Εξασφαλίζει ότι θα καταγράψετε την τελική τιμή |
| **Τρέχετε σε κοντέινερ χωρίς UI νήμα** | Δεν απαιτούνται επιπλέον βήματα – το Aspose.HTML τρέχει headlessly | Ιδανικό για CI pipelines |

---

## Πλήρες Παράδειγμα (Έτοιμο για Αντιγραφή‑Επικόλληση)

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;

public class JsAndDomTutorial {
    public static void main(String[] args) throws Exception {

        // Load the HTML document that contains JavaScript
        HtmlDocument htmlDoc = new HtmlDocument("YOUR_DIRECTORY/scripted.html", new LoadOptions());

        // Enable script execution – crucial for dynamic content
        htmlDoc.getWindow().setScriptsEnabled(true);

        // Set a generous script timeout (5 seconds)
        htmlDoc.getWindow().setTimeout(5000);

        // Give scripts a moment to finish
        Thread.sleep(2000);

        // Use query selector java to locate the element altered by the script
        Element dynamicDiv = htmlDoc.querySelector("#dynamicDiv");
        if (dynamicDiv != null) {
            // Retrieve the computed background color after script execution
            String backgroundColor = dynamicDiv.getComputedStyle().getBackgroundColor();
            System.out.println("Computed background: " + backgroundColor);
        } else {
            System.out.println("Element #dynamicDiv not found.");
        }

        // Release native resources
        htmlDoc.dispose();
    }
}
```

Αποθηκεύστε το ως `JsAndDomTutorial.java`, αντικαταστήστε το `YOUR_DIRECTORY` με τη διαδρομή προς το αρχείο HTML σας, μεταγλωττίστε με `javac -cp aspose-html-23.12.jar JsAndDomTutorial.java`, και τρέξτε `java -cp .:aspose-html-23.12.jar JsAndDomTutorial`. Θα πρέπει να δείτε το υπολογισμένο φόντο να εκτυπώνεται στην κονσόλα.

---

## Συχνές Ερωτήσεις

**Ε: Υποστηρίζει το Aspose.HTML σύνταξη ES6;**  
Α: Ναι. Η μηχανή χρησιμοποιεί έναν σύγχρονο ερμηνευτή JavaScript που καταλαβαίνει `let`, `const`, βέλη (arrow functions) και ακόμη `async/await`. Απλώς βεβαιωθείτε ότι δίνετε αρκετό χρόνο με το `set script timeout`.

**Ε: Τι γίνεται αν η σελίδα χρησιμοποιεί εξωτερικά αρχεία script;**  
Α: Εφόσον αυτά τα αρχεία είναι προσβάσιμα (τοπική διαδρομή ή απόλυτο URL) θα ληφθούν αυτόματα. Αν εργάζεστε offline, ενσωματώστε τα scripts στο HTML ή χρησιμοποιήστε `LoadOptions.setBaseUrl()` για να δείξετε σε τοπικό φάκελο.

**Ε: Μπορώ να ανακτήσω άλλα υπολογισμένα στυλ;**  
Α: Απόλυτα. Το αντικείμενο `ComputedStyle` εκθέτει κάθε ιδιότητα CSS—`getFontSize()`, `getMarginTop()`, κ.λπ. Χρησιμοποιήστε το ίδιο μοτίβο που χρησιμοποιήσατε για να **λάβετε το υπολογισμένο φόντο**.

---

## Συμπέρασμα

Τώρα ξέρετε πώς να **ενεργοποιήσετε την εκτέλεση σεναρίων** στο Aspose.HTML για Java, **να ορίσετε χρονικό όριο σεναρίου**, **να φορτώσετε html έγγραφο**, να αξιοποιήσετε το **query selector java**, και τελικά να **λάβετε το υπολογισμένο φόντο** από ένα δυναμικά στιλιζαρισμένο στοιχείο. Αυτή η ολοκληρωμένη ροή αποτελεί μια σταθερή βάση για οποιαδήποτε εργασία server‑side rendering ή εξαγωγής δεδομένων από HTML.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να εξάγετε υπολογισμένα πλάτη, ύψη, ή ακόμη να διαβάσετε τιμές από στοιχεία canvas. Ή συνδυάστε το με μετατροπή σε PDF για στιγμιότυπο της πλήρως αποδομένης σελίδας—το Aspose.HTML το κάνει παιχνιδάκι.

Καλή προγραμματιστική, και μην ξεχνάτε να πειραματιστείτε με τα χρονικά όρια και τις παραλλαγές selector ώστε να ταιριάζουν στην περίπτωσή σας! 🚀

---

![Screenshot showing enable script execution in Aspose.HTML](/images/enable-script-execution.png "Enable script execution in Aspose.HTML example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
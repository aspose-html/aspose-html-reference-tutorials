---
category: general
date: 2026-04-11
description: Επιλέξτε div κατά κλάση χρησιμοποιώντας Java – μάθετε πώς να φορτώνετε
  HTML, να περιμένετε τη φόρτωση του HTML και να αξιολογείτε αποδοτικά το XPath σε
  Java.
draft: false
keywords:
- select div by class
- load html java
- java xpath nodeset
- wait for html load
- evaluate xpath java
language: el
og_description: Επιλογή div κατά κλάση χρησιμοποιώντας Java – μάθετε πώς να φορτώνετε
  HTML, να περιμένετε τη φόρτωση του HTML και να αξιολογείτε αποδοτικά το XPath με
  Java.
og_title: Επιλογή div κατά κλάση σε Java – Πλήρης Οδηγός XPath
tags:
- Java
- XPath
- Aspose.HTML
title: Επιλογή div κατά κλάση σε Java – Πλήρης οδηγός XPath
url: /el/java/creating-managing-html-documents/select-div-by-class-in-java-complete-xpath-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Επιλογή div κατά κλάση σε Java – Πλήρης Οδηγός XPath

Κάποτε χρειάστηκε να **επιλέξετε div κατά κλάση** σε ένα έργο Java αλλά δεν ήσασταν σίγουροι ποιο API θα σας έδινε αξιόπιστο αποτέλεσμα; Δεν είστε μόνοι. Οι περισσότεροι προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν προσπαθούν να αναλύσουν ένα αρχείο HTML, περιμένουν να φορτωθεί και στη συνέχεια εκτελούν μια έκφραση XPath που επιστρέφει ένα `NodeSet`.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα τις ακριβείς ενέργειες για **φόρτωση HTML σε Java**, διασφάλιση ότι το έγγραφο είναι πλήρως έτοιμο (ναι, *αναμονή για φόρτωση HTML*), και τέλος **αξιολόγηση XPath Java** για να εξάγουμε κάθε `<div>` του οποίου το χαρακτηριστικό `class` είναι ίσο με `"test"`. Στο τέλος θα έχετε ένα έτοιμο δείγμα κώδικα, μια σαφή εξήγηση του γιατί κάθε γραμμή είναι σημαντική, και μερικές συμβουλές για αποφυγή κοινών παγίδων.

---

## Τι Θα Δημιουργήσετε

- Φόρτωση αρχείου HTML χρησιμοποιώντας Aspose.HTML for Java.  
- Παύση της εκτέλεσης μέχρι να ολοκληρωθεί η φόρτωση του εγγράφου.  
- Εκτέλεση μιας υψηλότερης‑τάξης συνάρτησης XPath (`filter`) που επιστρέφει ένα **Java XPath NodeSet** από τα αντίστοιχα στοιχεία `<div>`.  
- Εκτύπωση του αριθμού των αντιστοιχίσεων στην κονσόλα.

Δεν απαιτούνται εξωτερικές βιβλιοθήκες εκτός από το Aspose.HTML, και ο κώδικας λειτουργεί σε Java 17 και νεότερες εκδόσεις.

---

## Προαπαιτούμενα

- Java Development Kit (JDK) 17+ εγκατεστημένο.  
- Aspose.HTML for Java JAR στο classpath σας (μπορείτε να το κατεβάσετε από το Maven Central).  
- Ένα μικρό αρχείο `data.html` που περιέχει κάποια στοιχεία `<div class="test">` – θα το δημιουργήσουμε στο επόμενο βήμα.

---

## Βήμα 1: Φόρτωση HTML σε Java με Aspose.HTML

Το πρώτο που χρειάζεστε είναι ένα έγκυρο αντικείμενο `HTMLDocument`. Το Aspose.HTML το κάνει με μία γραμμή κώδικα, αλλά πρέπει να του δείξετε το σωστό μονοπάτι αρχείου.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;

public class XPath31Demo {
    public static void main(String[] args) throws Exception {

        // 👉 Step 1: Load the HTML document from disk
        HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/data.html");
```

**Γιατί είναι σημαντικό:**  
`HTMLDocument` αναλύει το αρχείο και δημιουργεί ένα δέντρο DOM που μπορεί να ερωτηθεί από XPath αργότερα. Αν το αρχείο δεν βρεθεί, το Aspose ρίχνει `FileNotFoundException`, οπότε ελέγξτε προσεκτικά το μονοπάτι ή χρησιμοποιήστε απόλυτη διαδρομή.

---

## Βήμα 2: Αναμονή για Φόρτωση HTML Πριν την Ερώτηση

Η ανάλυση HTML μπορεί να είναι ασύγχρονη, ειδικά όταν το έγγραφο περιέχει εξωτερικούς πόρους (scripts, images κ.λπ.). Η κλήση `waitForLoad()` εγγυάται ότι το DOM είναι πλήρως χτισμένο.

```java
        // 👉 Step 2: Ensure the document is fully loaded before querying
        htmlDoc.waitForLoad();
```

**Pro tip:**  
Αν παραλείψετε το `waitForLoad()`, μπορεί να λάβετε ένα κενό `NodeSet` επειδή ο parser δεν έχει τελειώσει. Σε περιβάλλοντα headless αυτή η κλήση είναι πρακτικά δωρεάν, οπότε πάντα να την συμπεριλαμβάνετε.

---

## Βήμα 3: Αξιολόγηση XPath Java για Λήψη NodeSet

Τώρα απελευθερώνουμε τη δύναμη της συνάρτησης `filter()` του XPath 3.1. Διατρέχει όλα τα στοιχεία `<div>` και κρατά μόνο εκείνα των οποίων το `@class` είναι ίσο με `"test"`.

```java
        // 👉 Step 3: Use a higher‑order XPath function to select <div> elements with class="test"
        NodeList matchingDivs = htmlDoc.evaluate(
                "filter(//div, function($n){$n/@class='test'})",
                htmlDoc,
                XPathResultType.NODESET
        ).getNodeSet();
```

**Ανάλυση της έκφρασης:**

| Μέρος | Εξήγηση |
|------|---------|
| `//div` | Επιλέγει κάθε `<div>` στο έγγραφο. |
| `filter(..., function($n){...})` | Εφαρμόζει μια λανβά‑στυλ συνάρτηση σε κάθε κόμβο `$n`. |
| `$n/@class='test'` | Επιστρέφει `true` μόνο όταν το χαρακτηριστικό `class` είναι ίσο με `"test"`. |
| `XPathResultType.NODESET` | Ενημερώνει το Aspose ότι αναμένουμε μια συλλογή κόμβων. |

Επειδή ζητήσαμε ένα **Java XPath NodeSet**, το αποτέλεσμα επιστρέφεται ως `NodeList`, το οποίο μπορούμε να διατρέξουμε ή να ερωτήσουμε περαιτέρω.

---

## Βήμα 4: Εξαγωγή Αποτελέσματος – Επαλήθευση του Ερωτήματος

Τέλος, ας εκτυπώσουμε πόσα στοιχεία `<div class="test">` βρήκαμε.

```java
        // 👉 Step 4: Output the number of matching elements found
        System.out.println("Found " + matchingDivs.getLength() + " matching div(s).");
    }
}
```

**Αναμενόμενη έξοδος** (υποθέτοντας ότι το `data.html` περιέχει τρία ταιριαστά divs):

```
Found 3 matching div(s).
```

Αν δείτε `0`, ελέγξτε ξανά την ορθογραφία του ονόματος κλάσης, τη θέση του αρχείου HTML, και αν κάνατε κλήση στο `waitForLoad()`.

---

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι το πλήρες, έτοιμο για αντιγραφή πρόγραμμα. Αντικαταστήστε το `YOUR_DIRECTORY` με το πραγματικό φάκελο που περιέχει το `data.html`.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;

public class XPath31Demo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document
        HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/data.html");

        // Step 2: Ensure the document is fully loaded before querying
        htmlDoc.waitForLoad();

        // Step 3: Use a higher‑order XPath function to select <div> elements with class="test"
        NodeList matchingDivs = htmlDoc.evaluate(
                "filter(//div, function($n){$n/@class='test'})",
                htmlDoc,
                XPathResultType.NODESET
        ).getNodeSet();

        // Step 4: Output the number of matching elements found
        System.out.println("Found " + matchingDivs.getLength() + " matching div(s).");
    }
}
```

> **Tip:** Αν χρειαστεί να επεξεργαστείτε κάθε ταιριαστό κόμβο (π.χ., να εξάγετε το εσωτερικό κείμενο), απλώς κάντε βρόχο πάνω στο `matchingDivs`:

```java
for (int i = 0; i < matchingDivs.getLength(); i++) {
    Element div = (Element) matchingDivs.item(i);
    System.out.println(div.getTextContent());
}
```

---

## Συνηθισμένες Παραλλαγές & Ακραίες Περιπτώσεις

### Επιλογή Πολλαπλών Κλάσεων

Αν ένα `<div>` μπορεί να έχει πολλές κλάσεις (π.χ., `class="test primary"`), αλλάξτε το πρότυπο XPath ώστε να χρησιμοποιεί `contains()`:

```xpath
filter(//div, function($n){contains($n/@class, 'test')})
```

### Ανίχνευση Χωρίς Ευαισθησία σε Πεζά/Κεφαλαία

Το XPath 3.1 δεν διαθέτει ενσωματωμένο τελεστή ανίχνευσης χωρίς διάκριση πεζών‑κεφαλαίων, αλλά μπορείτε να κανονικοποιήσετε και τις δύο πλευρές:

```xpath
filter(//div, function($n){lower-case($n/@class) = 'test'})
```

### Μεγάλα Έγγραφα

Όταν αναλύετε τεράστια αρχεία HTML, σκεφτείτε τη ροή (streaming) του εγγράφου ή την αύξηση του heap της JVM (`-Xmx2g`). Η κλήση `waitForLoad()` εξακολουθεί να λειτουργεί· απλώς περιμένει περισσότερο.

---

## Pro Tips & Gotchas

- **Αποφύγετε σκληρά κωδικοποιημένα μονοπάτια.** Χρησιμοποιήστε `Paths.get("data.html").toAbsolutePath()` για φορητότητα.  
- **Ελέγξτε την έκδοση του Aspose.HTML.** Η συνάρτηση `filter()` είναι διαθέσιμη μόνο από την έκδοση 22.7 και μετά.  
- **Θυμηθείτε να κλείνετε πόρους.** `htmlDoc.dispose();` απελευθερώνει φυσική μνήμη—ιδιαίτερα σημαντικό σε υπηρεσίες μακράς διάρκειας.  
- **Debugging XPath:** Αν δεν είστε σίγουροι γιατί ένας κόμβος δεν επιλέγεται, δοκιμάστε πρώτα ένα απλό ερώτημα `//div` και εκτυπώστε το μήκος· μετά βελτιώστε το πρότυπο.

---

## Εικονογραφική Παράσταση

![Διάγραμμα παραδείγματος επιλογής div κατά κλάση](select-div-by-class.png "Διάγραμμα που δείχνει τη ροή από τη φόρτωση HTML στην αξιολόγηση XPath και την ανάκτηση των ταιριαστών divs")

*Alt text:* Διάγραμμα παραδείγματος επιλογής div κατά κλάση που απεικονίζει τη φόρτωση HTML, την αναμονή για φόρτωση HTML, την αξιολόγηση XPath Java, και την ανάκτηση ενός Java XPath NodeSet.

---

## Συμπέρασμα

Δείξαμε πώς να **επιλέξετε div κατά κλάση** σε Java χρησιμοποιώντας Aspose.HTML, εξασφαλίζοντας ότι το έγγραφο είναι πλήρως φορτωμένο, και να λάβετε ένα **Java XPath NodeSet** με μια σύντομη έκφραση `filter()`. Η προσέγγιση είναι γρήγορη, τύπου‑ασφαλής, και λειτουργεί με τις σύγχρονες δυνατότητες του XPath 3.1, καθιστώντας την μια αξιόπιστη επιλογή για οποιαδήποτε εργασία ανάλυσης HTML.

Τι θα κάνετε στη συνέχεια; Δοκιμάστε να αλλάξετε το πρότυπο για άλλα χαρακτηριστικά, πειραματιστείτε με τις συναρτήσεις `map` ή `for-each` του XPath, ή ενσωματώστε αυτό το απόσπασμα σε ένα μεγαλύτερο pipeline εξόρυξης δεδομένων web. Τώρα έχετε τα δομικά στοιχεία για **φόρτωση HTML Java**, **αναμονή για φόρτωση HTML**, και **αξιολόγηση XPath Java** σαν επαγγελματίας.

Καλή προγραμματιστική, και μη διστάσετε να αφήσετε τις ερωτήσεις σας στα σχόλια—κανένα πρόβλημα δεν είναι πολύ μικρό όταν πρόκειται για την κυριαρχία του XPath σε Java!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
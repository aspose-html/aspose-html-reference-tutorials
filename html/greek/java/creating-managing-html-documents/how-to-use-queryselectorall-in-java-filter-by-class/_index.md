---
category: general
date: 2026-04-23
description: Πώς να χρησιμοποιήσετε το querySelectorAll στην Java για να φιλτράρετε
  στοιχεία κατά κλάση, να διαβάζετε τιμές χαρακτηριστικών και να επαναλάβετε το NodeList για
  εξαγωγή δεδομένων προϊόντων.
draft: false
keywords:
- how to use queryselectorall
- how to read attribute
- iterate nodelist java
- filter elements by class
- select elements css selector
language: el
og_description: Πώς να χρησιμοποιήσετε το querySelectorAll στη Java για να φιλτράρετε
  στοιχεία κατά κλάση, να διαβάζετε τιμές χαρακτηριστικών και να επαναλάβετε το NodeList
  για εξαγωγή δεδομένων προϊόντων.
og_title: Πώς να χρησιμοποιήσετε το querySelectorAll στην Java – Φιλτράρισμα κατά
  κλάση
tags:
- Java
- HTML parsing
- DOM manipulation
title: Πώς να χρησιμοποιήσετε το querySelectorAll στη Java – Φιλτράρισμα ανά κλάση
url: /el/java/creating-managing-html-documents/how-to-use-queryselectorall-in-java-filter-by-class/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε το querySelectorAll στη Java – Φίλτρο με Κλάση

Το πώς να χρησιμοποιήσετε το querySelectorAll στη Java είναι το κλειδί όταν χρειάζεται να εξάγετε συγκεκριμένα στοιχεία από ένα έγγραφο HTML. Σε αυτό το tutorial θα φιλτράρουμε στοιχεία κατά κλάση, θα διαβάσουμε τιμές χαρακτηριστικών και θα επαναλάβουμε ένα NodeList για να εξάγουμε τις τιμές προϊόντων από μια σελίδα καταλόγου.  

Έχετε βρεθεί ποτέ μπροστά σε ένα τεράστιο αρχείο HTML, αναρωτιέται πώς να εξάγετε μόνο τις κάρτες «σε προσφορά» χωρίς να γράψετε έναν προσαρμοσμένο parser; Αυτό ακριβώς είναι το πρόβλημα που θα λύσουμε εδώ—χωρίς επιπλέον βιβλιοθήκες εκτός από το Aspose.HTML, και με λίγα απλά βήματα.

Θα αποχωρήσετε με ένα πλήρες, εκτελέσιμο πρόγραμμα που:

* **Επιλέγει στοιχεία** χρησιμοποιώντας έναν CSS selector (`select elements css selector`),
* **Φιλτράρει κατά κλάση** (`filter elements by class`),
* **Διαβάζει ένα προσαρμοσμένο χαρακτηριστικό** (`how to read attribute`),
* **Επαναλαμβάνει το προκύπτον NodeList** (`iterate nodelist java`).

Δεν απαιτείται προηγούμενη εμπειρία με το Aspose.HTML—απλώς μια βασική εγκατάσταση Java και ένα αρχείο HTML για δοκιμή.

![πώς να χρησιμοποιήσετε το querySelectorAll στη Java παράδειγμα](https://example.com/images/queryselectorall-java.png "πώς να χρησιμοποιήσετε το querySelectorAll στη Java")

---

## Τι Θα Χρειαστείτε

| Απαίτηση | Γιατί είναι σημαντικό |
|-------------|----------------|
| **Java 17+** | Σύγχρονες δυνατότητες γλώσσας και καλύτερη διαχείριση modules. |
| **Aspose.HTML for Java** (τελευταία έκδοση) | Παρέχει την κλάση `Document` και τη μηχανή CSS‑selector. |
| **catalog.html** (δείγμα HTML) | Η πηγή που θα ερωτήσουμε. |
| **IDE ή απλό `javac`** | Για να μεταγλωττίσετε και να εκτελέσετε τη demo. |

Αν δεν έχετε προσθέσει ακόμα το Aspose.HTML στο πρότζεκτ σας, τοποθετήστε το JAR στο φάκελο `libs` και προσθέστε το στο classpath:

```bash
javac -cp "libs/*" CssSelectorDemo.java
java -cp ".:libs/*" CssSelectorDemo
```

---

## Βήμα 1 – Φόρτωση του HTML Εγγράφου

Πριν μπορέσετε να κάνετε ερωτήματα, χρειάζεστε ένα αντικείμενο `Document` που να αντιπροσωπεύει το αρχείο HTML. Σκεφτείτε το σαν να φορτώνετε ένα λογιστικό φύλλο πριν διαβάσετε τα κελιά.

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");
```

> **Γιατί είναι σημαντικό:** Η κλάση `Document` αναλύει το markup σε ένα δέντρο DOM, επιτρέποντας στη μηχανή CSS‑selector να λειτουργήσει. Παραλείποντας αυτό το βήμα θα έχετε μόνο μια απλή συμβολοσειρά και κανέναν τρόπο να χρησιμοποιήσετε το `querySelectorAll`.

---

## Βήμα 2 – Επιλογή Στοιχείων με CSS Selector

Τώρα έρχεται η ουσία: **πώς να χρησιμοποιήσετε το querySelectorAll**. Η μέθοδος δέχεται οποιονδήποτε έγκυρο CSS selector, ώστε να μπορείτε να είστε τόσο ακριβείς—ή τόσο γενικοί—όσο θέλετε. Για το σενάριό μας θέλουμε κάρτες προϊόντων που:

* έχουν την κλάση `product-card`,
* είναι επίσης σημειωμένες με την κλάση `sale`,
* και διαθέτουν χαρακτηριστικό `data-price`.

```java
        // Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );
```

> **Εξήγηση:**  
> * `.product-card.sale` → φιλτράρει στοιχεία που περιέχουν **και τις δύο** κλάσεις.  
> * `[data-price]` → εξασφαλίζει ότι το χαρακτηριστικό υπάρχει, φιλτράροντας αποτελεσματικά **κατά κλάση** **και** χαρακτηριστικό σε μία κλήση.  
> * Το αποτέλεσμα είναι ένα `NodeList`, μια διατεταγμένη συλλογή που μπορείτε να επαναλάβετε.

Αν χρειαστεί ποτέ να **select elements css selector** για διαφορετικό μοτίβο, απλώς αλλάξτε τη συμβολοσειρά—χωρίς ανάγκη επαναγραφής κώδικα.

---

## Βήμα 3 – Επανάληψη του NodeList στη Java

Ένα `NodeList` συμπεριφέρεται πολύ σαν έναν πίνακα, αλλά δεν υλοποιεί το `Iterable`. Γι’ αυτό χρησιμοποιούμε έναν κλασικό βρόχο `for`—ιδανικό για σενάρια **iterate nodelist java**.

```java
        // Iterate over the selected elements
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
```

> **Γιατί βρόχος `for`;**  
> Σας δίνει άμεση πρόσβαση στο δείκτη, κάτι χρήσιμο για καταγραφές ή συνθήκες. Αν προτιμάτε βρόχο `while`, η λογική παραμένει ίδια—απλώς αλλάξτε τη δομή του βρόχου.

---

## Βήμα 4 – Ανάγνωση του Χαρακτηριστικού `data-price`

Τώρα τελικά απαντάμε στο **πώς να διαβάσετε attribute** τιμές από ένα στοιχείο. Στο API DOM, η `getAttribute` επιστρέφει τη ακατέργαστη συμβολοσειρά, ακριβώς όπως εμφανίζεται στο markup.

```java
            // Read the price value from the data-price attribute
            String priceValue = productElement.getAttribute("data-price");
```

> **Συμβουλή:** Αν το χαρακτηριστικό μπορεί να λείπει, η `getAttribute` επιστρέφει `null`. Μπορείτε να το προστατέψετε με έναν απλό έλεγχο:

```java
            if (priceValue == null) {
                priceValue = "N/A"; // fallback for missing data-price
            }
```

---

## Βήμα 5 – Εκτύπωση των Αποτελεσμάτων

Τελευταίο αλλά όχι λιγότερο σημαντικό, εκτυπώνουμε κάθε τιμή στην κονσόλα. Αυτό αντικατοπτρίζει ένα πραγματικό σενάριο όπου πιθανώς θα στέλνατε τις τιμές σε βάση δεδομένων ή σε payload API.

```java
            // Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

### Αναμενόμενη Εξαγωγή στην Κονσόλα

```
Sale item price: 19.99
Sale item price: 34.50
Sale item price: 12.00
```

Αν ο selector δεν βρει κανένα αντίστοιχο κόμβο, ο βρόχος απλώς δεν εκτελείται—δεν ρίχνεται εξαίρεση. Αυτό αποτελεί ένα ωραίο δίχτυ ασφαλείας για **edge cases** όπου ο κατάλογος μπορεί να είναι κενός.

---

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας τα παραπάνω, εδώ είναι το ολοκληρωμένο αρχείο που μπορείτε να αντιγράψετε‑επικολλήσετε στο `CssSelectorDemo.java`:

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");

        // Step 2: Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );

        // Step 3 & 4: Iterate over the selected elements and read the price attribute
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
            String priceValue = productElement.getAttribute("data-price");
            if (priceValue == null) {
                priceValue = "N/A"; // fallback if attribute is missing
            }

            // Step 5: Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

Αποθηκεύστε το αρχείο, μεταγλωττίστε και τρέξτε—παρακολουθήστε τις τιμές να εμφανίζονται. 🎉

---

## Συχνές Ερωτήσεις & Pro Tips

| Ερώτηση | Απάντηση |
|----------|--------|
| *Τι γίνεται αν χρειαστεί να επιλέξω και με όνομα ετικέτας;* | Απλώς προσθέστε την ετικέτα στην αρχή: `document.querySelectorAll("div.product-card.sale[data-price]")`. |
| *Μπορώ να συνδυάσω πολλαπλά φίλτρα χαρακτηριστικών;* | Απόλυτα. Παράδειγμα: `[data-price][data-stock]` θα κρατήσει μόνο στοιχεία που έχουν **και τα δύο** χαρακτηριστικά. |
| *Είναι το `querySelectorAll` case‑sensitive;* | Ναι—οι CSS selectors αντιμετωπίζουν τα ονόματα κλάσεων και χαρακτηριστικών ως case‑sensitive στο HTML5. |
| *Πώς διαχειρίζομαι ένα τεράστιο αρχείο HTML;* | Το Aspose.HTML κάνει streaming του εγγράφου, αλλά μπορείτε επίσης να περιορίσετε το selector σε ένα υποδέντρο (`someElement.querySelectorAll(...)`). |
| * What

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
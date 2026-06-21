---
category: general
date: 2026-04-09
description: Μάθετε πώς να μετατρέπετε HTML σε PNG χρησιμοποιώντας τη Java. Αυτό το
  σεμινάριο καλύπτει τη μετατροπή HTML σε PNG, τη συμπλήρωση πίνακα HTML με JavaScript,
  τη δημιουργία εγγράφου HTML με Java και τη δημιουργία κενής HTML με Java.
draft: false
keywords:
- convert html to png
- render html to png
- populate html table javascript
- create html document java
- create empty html java
language: el
og_description: Η μετατροπή HTML σε PNG έγινε εύκολη. Ακολουθήστε αυτόν τον οδηγό
  βήμα‑βήμα για να αποδώσετε HTML σε PNG, να γεμίσετε πίνακα HTML με JavaScript και
  να δημιουργήσετε έγγραφο HTML με Java.
og_title: Μετατροπή HTML σε PNG – Πλήρης Οδηγός Απόδοσης Java
tags:
- Java
- Aspose.HTML
- Image rendering
title: Μετατροπή HTML σε PNG – Οδηγός Java για τη δημιουργία εικόνων από πίνακες HTML
url: /el/java/conversion-html-to-various-image-formats/convert-html-to-png-java-guide-to-rendering-html-tables-as-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# μετατροπή html σε png – Οδηγός Java για απόδοση πινάκων HTML ως εικόνες

Έχετε ποτέ χρειαστεί να **convert html to png** αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν πρόβλημα όταν πρέπει να μετατρέψουν ένα δυναμικό απόσπασμα HTML—ιδιαίτερα ένα που δημιουργείται με JavaScript—σε μια στατική εικόνα. Σε αυτό το tutorial θα περάσουμε βήμα-βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που παίρνει μια μικρή σελίδα HTML, γεμίζει έναν πίνακα με JavaScript και τελικά τον αποδίδει ως αρχείο PNG χρησιμοποιώντας το Aspose.HTML for Java.

Θα αγγίξουμε επίσης σχετικά θέματα όπως **render html to png**, πώς να **populate html table javascript**, και τις λεπτομέρειες του **create html document java** σε σύγκριση με το **create empty html java**. Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Maven ή Gradle και να το εκτελέσετε αμέσως.

## Προαπαιτούμενα

- Java 17 ή νεότερη (το API λειτουργεί με Java 8+ αλλά θα χρησιμοποιήσουμε την πιο πρόσφατη LTS)
- Βιβλιοθήκη Aspose.HTML for Java (διαθέσιμη μέσω Maven Central)
- Ένα απλό IDE ή η απλή γραμμή εντολών `javac`/`java`
- Δικαίωμα εγγραφής σε φάκελο όπου θα αποθηκευτεί το PNG

Χωρίς εξωτερικά προγράμματα περιήγησης, χωρίς headless Chrome, μόνο καθαρός κώδικας Java.

## Βήμα 1: Δημιουργία κενής HTML εγγράφου (create empty html java)

Το πρώτο πράγμα που χρειαζόμαστε είναι ένα καθαρό φύλλο—ένα κενό αντικείμενο HTMLDocument που μπορούμε να χειριστούμε προγραμματιστικά. Το Aspose.HTML παρέχει την κλάση `HTMLDocument` η οποία λειτουργεί σαν μια μικρή μηχανή προγράμματος περιήγησης.

```java
import com.aspose.html.HTMLDocument;

// Step 1: Initialise an empty document
HTMLDocument htmlDoc = new HTMLDocument();
```

Γιατί να ξεκινήσουμε με ένα κενό έγγραφο; Επειδή εγγυάται ότι κανένα ανεπιθύμητο markup ή προηγούμενη κατάσταση δεν θα επηρεάσει τον πίνακα που πρόκειται να δημιουργήσουμε. Είναι το ισοδύναμο στην Java του `document.open()` σε έναν περιηγητή.

## Βήμα 2: Γράψτε μια ελάχιστη HTML σελίδα που περιέχει έναν κενό πίνακα (create html document java)

Στη συνέχεια ενσωματώνουμε ένα μικρό σκελετό HTML. Η σελίδα περιλαμβάνει έναν placeholder `<table id='data'></table>` και μερικούς κανόνες CSS για να φαίνεται ο πίνακας αποδεκτός κατά την απόδοση.

```java
htmlDoc.write(
    "<!DOCTYPE html><html><head><style>" +
    "table {border-collapse: collapse; width: 100%;}" +
    "td, th {border: 1px solid #ddd; padding: 8px;}" +
    "</style></head><body>" +
    "<table id='data'></table></body></html>"
);
```

Παρατηρήστε πώς **create html document java** τροφοδοτώντας μια ακατέργαστη συμβολοσειρά στη μέθοδο `write`. Αυτή η προσέγγιση είναι χρήσιμη όταν το HTML δημιουργείται εν κινήσει και αποφεύγει την ανάγκη για εξωτερικά αρχεία προτύπων.

## Βήμα 3: Συμπλήρωση του HTML πίνακα με JavaScript (populate html table javascript)

Τώρα έρχεται το διασκεδαστικό μέρος—η προσθήκη γραμμών στον πίνακα χρησιμοποιώντας JavaScript. Θα δημιουργήσουμε ένα σύντομο script που θα επαναλαμβάνει πέντε φορές, εισάγοντας μια γραμμή σε κάθε επανάληψη και γεμίζοντας δύο κελιά: ένα με τον αριθμό της γραμμής και ένα άλλο με “Even” ή “Odd”.

```java
String populateScript = ""
    + "const tbl = document.querySelector('#data');"
    + "for (let i = 1; i <= 5; i++) {"
    + "  const row = tbl.insertRow();"
    + "  row.insertCell().textContent = `Row ${i}`;"
    + "  row.insertCell().textContent = (i % 2 === 0) ? 'Even' : 'Odd';"
    + "}";
```

Γιατί να χρησιμοποιήσουμε JavaScript εδώ; Επειδή πολλές πραγματικές σελίδες δημιουργούν πίνακες δυναμικά—σκεφτείτε πίνακες ελέγχου, αναφορές ή πλέγματα δεδομένων στην πλευρά του πελάτη. Με το **populate html table javascript** μέσα στη μηχανή Aspose, μιμούμαστε ακριβώς αυτό που θα συνέβαινε σε έναν περιηγητή, διασφαλίζοντας ότι το παραγόμενο PNG είναι ταυτόσημο με αυτό που θα έβλεπε ο χρήστης.

## Βήμα 4: Εκτέλεση του script μέσα στην άσφαλτο του εγγράφου

Το Aspose.HTML μας παρέχει ένα αντικείμενο `Window` που συμπεριφέρεται όπως το `window` ενός περιηγητή. Η κλήση του `eval` εκτελεί το script μας σε απομονωμένο περιβάλλον, ώστε να μην γίνονται εξωτερικές κλήσεις δικτύου.

```java
htmlDoc.getWindow().eval(populateScript);
```

Ένα κοινό λάθος είναι να ξεχάσουμε να περιμένουμε το script να ολοκληρωθεί πριν από την απόδοση. Σε αυτήν την απλή περίπτωση το script εκτελείται συγχρονισμένα, οπότε μπορούμε να προχωρήσουμε αμέσως στο επόμενο βήμα. Αν ενσωματώσετε ασύγχρονο κώδικα (π.χ., `fetch`), θα πρέπει να συνδέσετε το `onload` event ή να χρησιμοποιήσετε αναμονή βασισμένη σε `Promise`.

## Βήμα 5: Διαμόρφωση επιλογών αποθήκευσης εικόνας (render html to png)

Πριν πραγματικά rasterize τη σελίδα, αποφασίζουμε το μέγεθος της εξόδου εικόνας. Η κλάση `ImageSaveOptions` μας επιτρέπει να ορίσουμε πλάτος, ύψος και μερικές παραμέτρους ποιότητας.

```java
import com.aspose.html.converters.ImageSaveOptions;

ImageSaveOptions imageOptions = new ImageSaveOptions();
imageOptions.setWidth(800);   // Desired width in pixels
imageOptions.setHeight(600);  // Desired height in pixels
```

Η επιλογή ενός λογικού μεγέθους καμβά είναι κρίσιμη για ένα καθαρό αποτέλεσμα **render html to png**. Πολύ μικρό και το κείμενο κόβεται· πολύ μεγάλο και σπαταλάται μνήμη. Το 800×600 είναι ένα ασφαλές μέσο για τους περισσότερους πίνακες.

## Βήμα 6: Μετατροπή της συμπληρωμένης HTML σελίδας σε εικόνα PNG (convert html to png)

Τέλος, καλούμε τη στατική μέθοδο `Converter.convertHTML`. Παίρνει το `HTMLDocument`, τις επιλογές αποθήκευσης και τη διαδρομή του αρχείου προορισμού.

```java
import com.aspose.html.converters.Converter;

Converter.convertHTML(htmlDoc, imageOptions, "YOUR_DIRECTORY/table.png");
```

Αντικαταστήστε το `YOUR_DIRECTORY` με μια απόλυτη ή σχετική διαδρομή που υπάρχει στο σύστημά σας. Μετά το τέλος του προγράμματος, θα βρείτε το `table.png` που εμφανίζει έναν ωραία μορφοποιημένο πίνακα με πέντε γραμμές, εναλλασσόμενες ετικέτες “Even”/“Odd”.

> **Συμβουλή:** Αν χρειάζεστε διαφανές φόντο, ενεργοποιήστε το μέσω `imageOptions.setBackgroundColor(Color.getTransparent());`.

## Πλήρες, Έτοιμο‑για‑Εκτέλεση Παράδειγμα

Παρακάτω βρίσκεται η πλήρης κλάση Java που συνδυάζει όλα. Αντιγράψτε‑και‑επικολλήστε την στο `JsDomManipulation.java`, προσαρμόστε το φάκελο εξόδου και εκτελέστε την.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.ImageSaveOptions;

public class JsDomManipulation {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an empty HTML document
        HTMLDocument htmlDoc = new HTMLDocument();

        // Step 2: Write a minimal HTML page that contains an empty table
        htmlDoc.write(
            "<!DOCTYPE html><html><head><style>" +
            "table {border-collapse: collapse; width: 100%;}" +
            "td, th {border: 1px solid #ddd; padding: 8px;}" +
            "</style></head><body>" +
            "<table id='data'></table></body></html>"
        );

        // Step 3: Define JavaScript that populates the table with rows
        String populateScript = ""
            + "const tbl = document.querySelector('#data');"
            + "for (let i = 1; i <= 5; i++) {"
            + "  const row = tbl.insertRow();"
            + "  row.insertCell().textContent = `Row ${i}`;"
            + "  row.insertCell().textContent = (i % 2 === 0) ? 'Even' : 'Odd';"
            + "}";

        // Step 4: Execute the script inside the document's sandbox
        htmlDoc.getWindow().eval(populateScript);

        // Step 5: Configure image‑save options (size of the rendered image)
        ImageSaveOptions imageOptions = new ImageSaveOptions();
        imageOptions.setWidth(800);
        imageOptions.setHeight(600);

        // Step 6: Convert the populated HTML page to a PNG image
        Converter.convertHTML(htmlDoc, imageOptions, "YOUR_DIRECTORY/table.png");
    }
}
```

### Αναμενόμενη έξοδος

Όταν ανοίξετε το `table.png`, θα πρέπει να δείτε κάτι όπως αυτό:

![παράδειγμα εξόδου μετατροπής html σε png](https://example.com/assets/table.png "convert html to png – αποδοθείς πίνακας")

Η εικόνα εμφανίζει έναν πίνακα 5 γραμμών με το μοτίβο “Row 1 – Odd” … “Row 5 – Odd”, μορφοποιημένο με λεπτά περιγράμματα και εσωτερικά περιθώρια.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **Το script εκτελείται μετά την απόδοση** | Ο ασύγχρονος κώδικας (π.χ., `setTimeout`) δεν περιμένει. | Χρησιμοποιήστε `window.onload` ή μπλοκάρετε μέχρι `document.readyState === 'complete'`. |
| **Η εικόνα είναι κενή** | Δεν υπάρχει περιεχόμενο στο παράθυρο προβολής (πλάτος/ύψος ορίσθηκαν σε 0). | Βεβαιωθείτε ότι οι διαστάσεις του `ImageSaveOptions` δεν είναι μηδενικές και ταιριάζουν με τη διάταξη της σελίδας. |
| **Οι γραμμές του πίνακα κόβονται** | Ο καμβάς είναι πολύ μικρός για το ύψος του πίνακα. | Αυξήστε το `imageOptions.setHeight` ή χρησιμοποιήστε `imageOptions.setFitToPage(true)`. |
| **Απουσία CSS** | Το ενσωματωμένο στυλ παραλείφθηκε ή το εξωτερικό CSS δεν φορτώθηκε. | Διατηρήστε όλο το απαιτούμενο CSS μέσα στην ετικέτα `<style>` επειδή οι εξωτερικοί πόροι δεν φορτώνονται εξ ορισμού. |

## Επέκταση του παραδείγματος

- **Απόδοση σε JPEG** – αντικαταστήστε το `ImageSaveOptions` με `JpegSaveOptions`.
- **Προσθήκη γραφημάτων** – ενσωματώστε ένα στοιχείο `<canvas>` και σχεδιάστε με Chart.js· η μηχανή θα rasterize το καμβά ως μέρος του PNG.
- **Επεξεργασία σε παρτίδες** – επαναλάβετε πάνω σε μια συλλογή δεδομένων, δημιουργήστε ένα νέο `HTMLDocument` κάθε φορά και αποθηκεύστε κάθε PNG με μοναδικό όνομα.

## Συμπέρασμα

Τώρα έχετε μια σταθερή, έτοιμη για παραγωγή συνταγή για **convert html to png** χρησιμοποιώντας καθαρή Java. Το tutorial κάλυψε τα πάντα από τη δημιουργία ενός κενό HTML εγγράφου, τη σύνταξη του markup, **populate html table javascript**, τη διαμόρφωση των επιλογών **render html to png**, και τέλος την εκτέλεση της μετατροπής.

Μη διστάσετε να πειραματιστείτε: δοκιμάστε μεγαλύτερους πίνακες, διαφορετικά θέματα CSS ή ακόμη και ενσωματώστε γραφικά SVG. Όταν είστε έτοιμοι, εξερευνήστε άλλες δυνατότητες του Aspose.HTML όπως η μετατροπή σε PDF ή HTML‑to‑DOCX. Καλή κωδικοποίηση, και οι στιγμιότυπές σας να είναι πάντα pixel‑perfect!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
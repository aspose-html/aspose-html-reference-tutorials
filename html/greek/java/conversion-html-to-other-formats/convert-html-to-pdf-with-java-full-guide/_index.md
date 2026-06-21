---
category: general
date: 2026-04-23
description: Μετατρέψτε HTML σε PDF χρησιμοποιώντας το Aspose.HTML σε Java. Μάθετε
  πώς να ενεργοποιήσετε το JavaScript PDF, να ορίσετε PDF υψηλής ανάλυσης, να ρυθμίσετε
  το DPI του PDF και να εφαρμόσετε ομοιόμορφα περιθώρια σελίδας.
draft: false
keywords:
- convert html to pdf
- enable javascript pdf
- high resolution pdf
- adjust pdf dpi
- uniform page margins
language: el
og_description: Μετατρέψτε HTML σε PDF σε Java με το Aspose.HTML. Αυτός ο οδηγός δείχνει
  πώς να ενεργοποιήσετε το JavaScript PDF, να δημιουργήσετε PDF υψηλής ανάλυσης, να
  ρυθμίσετε το DPI του PDF και να ορίσετε ομοιόμορφα περιθώρια σελίδας.
og_title: Μετατροπή HTML σε PDF με Java – Πλήρης Οδηγός
tags:
- Java
- Aspose.HTML
- PDF conversion
title: Μετατροπή HTML σε PDF με Java – Πλήρης Οδηγός
url: /el/java/conversion-html-to-other-formats/convert-html-to-pdf-with-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή HTML σε PDF με Java – Πλήρης Οδηγός

Χρειάζεστε **μετατροπή HTML σε PDF** με Java; Βρίσκεστε στο σωστό μέρος. Σε αυτό το tutorial θα περάσουμε από τη μετατροπή HTML σε PDF χρησιμοποιώντας τη βιβλιοθήκη Aspose.HTML, και θα καλύψουμε επίσης πώς να **ενεργοποιήσετε το JavaScript PDF**, να δημιουργήσετε ένα **PDF υψηλής ανάλυσης**, **ρυθμίσετε το DPI του PDF**, και να εφαρμόσετε **ομοιόμορφα περιθώρια σελίδας**—όλα σε ένα μόνο, εύκολο‑να‑εκτελεστεί παράδειγμα.

Φανταστείτε ότι έχετε μια δυναμική ιστοσελίδα που βασίζεται σε script στο client‑side, και θέλετε ένα εκτυπώσιμο PDF που να μοιάζει ακριβώς με την απόδοση του προγράμματος περιήγησης. Αυτό είναι ένα κοινό σενάριο για συστήματα τιμολόγησης, δημιουργούς αναφορών ή οποιοδήποτε αυτοματοποιημένο pipeline εγγράφων. Στο τέλος αυτού του οδηγού θα έχετε ένα έτοιμο‑για‑χρήση πρόγραμμα Java που κάνει ακριβώς αυτό.

## Τι Θα Χρειαστείτε

- **Java Development Kit (JDK) 8 ή νεότερο** – ο κώδικας τρέχει σε οποιοδήποτε πρόσφατο JDK.  
- **Aspose.HTML for Java** – η εξάρτηση Maven/Gradle είναι μικρή και δωρεάν για δοκιμή.  
- Ένα **text editor ή IDE** (IntelliJ IDEA, Eclipse, VS Code… ό,τι προτιμάτε).  
- Ένα **αρχείο HTML** που θέλετε να μετατρέψετε σε PDF (θα το ονομάσουμε `input.html`).  

Αυτό είναι όλο. Καμία εξωτερική υπηρεσία, κανένα επιπλέον δυαδικό αρχείο. Απλώς καθαρή Java και μία βιβλιοθήκη.

## Μετατροπή HTML σε PDF – Ρύθμιση του Περιβάλλοντος

### Βήμα 1: Προσθήκη Aspose.HTML στο Έργο σας

Αν χρησιμοποιείτε Maven, προσθέστε αυτό στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- check the latest version on Maven Central -->
</dependency>
```

Οι χρήστες Gradle μπορούν να προσθέσουν:

```gradle
implementation 'com.aspose:aspose-html:23.12'
```

Γιατί είναι σημαντικό: το Aspose.HTML κάνει το σκληρό κομμάτι—αναλύει HTML, εκτελεί JavaScript και rasterises το αποτέλεσμα σε PDF. Χωρίς αυτό θα έπρεπε να ξαναεφευρέσετε τον τροχό.

> **Pro tip:** Αν βρίσκεστε σε εταιρικό δίκτυο, βεβαιωθείτε ότι τα URLs των αποθετηρίων δεν είναι μπλοκαρισμένα· διαφορετικά η κατασκευή θα αποτύχει κατά τη λήψη.

### Βήμα 2: Ορισμός Διαδρομών Πηγής και Προορισμού

Δημιουργήστε μια κλάση Java με όνομα `ConvertHtmlToPdfWithOptions`. Μέσα στο `main`, ξεκινήστε δείχνοντας στο αρχείο HTML σας και πού θέλετε να αποθηκευτεί το PDF:

```java
// Step 2: Define source HTML and destination PDF file paths
String sourceHtmlPath = "YOUR_DIRECTORY/input.html";
String destinationPdfPath = "YOUR_DIRECTORY/output.pdf";
```

Αντικαταστήστε το `YOUR_DIRECTORY` με μια απόλυτη ή σχετική διαδρομή που η JVM μπορεί να διαβάσει/γράψει. Η χρήση απόλυτων διαδρομών εξαλείφει την έκπληξη «αρχείο δεν βρέθηκε» που μπορεί να είχατε αντιμετωπίσει νωρίτερα.

### Βήμα 3: Ενεργοποίηση JavaScript PDF και Ρύθμιση DPI

Τώρα διαμορφώνουμε τις επιλογές μετατροπής. Δύο πράγματα είναι κρίσιμα για πιστή απόδοση:

1. **Enable JavaScript** – πολλές σύγχρονες σελίδες βασίζονται σε script για τη δημιουργία στοιχείων DOM.  
2. **Set a high DPI** – μια υψηλότερη τιμή dots‑per‑inch προσφέρει πιο καθαρό κείμενο και εικόνες, ειδικά για εκτύπωση.  

```java
// Step 3: Create PDF conversion options and enable JavaScript execution
PdfConversionOptions conversionOptions = new PdfConversionOptions();
conversionOptions.setEnableJavaScript(true);   // enable javascript pdf
conversionOptions.setDpi(300);                 // adjust pdf dpi for high resolution pdf
```

Γιατί 300 DPI; Είναι το de‑facto πρότυπο για ποιότητα εκτύπωσης. Οτιδήποτε χαμηλότερο φαίνεται λίγο θολό στο χαρτί, ενώ υψηλότερες τιμές αυξάνουν το μέγεθος του αρχείου χωρίς αισθητή βελτίωση για τις περισσότερες περιπτώσεις χρήσης.

### Βήμα 4: Ορισμός Ομοιόμορφων Περιθωρίων Σελίδας

Συνεπή περιθώρια κάνουν το έγγραφο να φαίνεται επαγγελματικό και αποτρέπουν το περιεχόμενο από το να χτυπάει την άκρη της σελίδας. Το Aspose.HTML σας επιτρέπει να ορίσετε και τις τέσσερις πλευρές με μία κλήση:

```java
// Step 4: Define uniform page margins (top, right, bottom, left) in points
conversionOptions.setPageMargins(20, 20, 20, 20); // uniform page margins
```

Κάθε περιθώριο μετράται σε points (1 pt = 1/72 in). Είκοσι points ισοδυναμούν περίπου με 0,28 in, μια ωραία ισορροπία μεταξύ λευκού χώρου και χρήσιμης περιοχής.

### Βήμα 5: Εκτέλεση της Μετατροπής

Τέλος, παραδίδουμε την πηγή, τον προορισμό και τις επιλογές στην κλάση `Converter`:

```java
// Step 5: Perform the conversion using the configured options
Converter.convert(sourceHtmlPath, destinationPdfPath, conversionOptions);
```

Αν όλα είναι σωστά συνδεδεμένα, θα δείτε το `output.pdf` να εμφανίζεται στον φάκελο που καθορίσατε. Ανοίξτε το με οποιονδήποτε προβολέα PDF—Adobe Reader, Chrome ή ακόμη και τον ενσωματωμένο προεπισκόπηση του λειτουργικού σας συστήματος—και θα πρέπει να δείτε ένα καθαρό, με σταθερά περιθώρια έγγραφο που σέβεται το JavaScript της αρχικής σελίδας.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Αντιγράψτε‑και‑επικολλήστε το σε ένα αρχείο με όνομα `ConvertHtmlToPdfWithOptions.java`, προσαρμόστε τις διαδρομές αρχείων, και τρέξτε `javac` + `java` όπως συνήθως.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfConversionOptions;

/**
 * Demonstrates how to convert an HTML file to a PDF with advanced options:
 * - JavaScript execution (enable javascript pdf)
 * - High‑resolution output (high resolution pdf)
 * - Custom DPI (adjust pdf dpi)
 * - Uniform margins (uniform page margins)
 */
public class ConvertHtmlToPdfWithOptions {
    public static void main(String[] args) throws Exception {

        // Step 1: Define source HTML and destination PDF file paths
        String sourceHtmlPath = "YOUR_DIRECTORY/input.html";
        String destinationPdfPath = "YOUR_DIRECTORY/output.pdf";

        // Step 2: Create PDF conversion options and enable JavaScript execution
        PdfConversionOptions conversionOptions = new PdfConversionOptions();
        conversionOptions.setEnableJavaScript(true);    // enable javascript pdf

        // Step 3: Set high‑resolution DPI for sharper output
        conversionOptions.setDpi(300);                  // adjust pdf dpi

        // Step 4: Define uniform page margins (top, right, bottom, left) in points
        conversionOptions.setPageMargins(20, 20, 20, 20); // uniform page margins

        // Step 5: Perform the conversion using the configured options
        Converter.convert(sourceHtmlPath, destinationPdfPath, conversionOptions);

        System.out.println("Conversion complete! PDF saved to " + destinationPdfPath);
    }
}
```

**Αναμενόμενο αποτέλεσμα:**  
- Ένα αρχείο PDF με όνομα `output.pdf`.  
- Το PDF αντικατοπτρίζει τη οπτική διάταξη του `input.html`, συμπεριλαμβανομένων τυχόν αλλαγών DOM που έγιναν από το JavaScript.  
- Κείμενο και εικόνες εμφανίζονται καθαρά χάρη στη ρύθμιση 300 DPI.  
- Τα περιθώρια είναι τα ίδια και στις τέσσερις πλευρές, δίνοντας στο έγγραφο μια καθαρή, επαγγελματική εμφάνιση.

![παράδειγμα εξόδου μετατροπής html σε pdf](https://example.com/convert-html-to-pdf.png "παράδειγμα εξόδου μετατροπής html σε pdf")

*Το παραπάνω στιγμιότυπο δείχνει ένα δείγμα PDF που δημιουργήθηκε από τον κώδικα—σημειώστε τα ομοιόμορφα περιθώρια και την καθαρή απόδοση.*

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν το HTML μου αναφέρεται σε εξωτερικούς πόρους (CSS, εικόνες, γραμματοσειρές);

Το Aspose.HTML επιλύει σχετικές URLs βάσει της τοποθεσίας του αρχείου πηγής. Βεβαιωθείτε ότι το HTML και οι πόροι του βρίσκονται μαζί, ή χρησιμοποιήστε απόλυτα URLs (π.χ., `https://example.com/styles.css`). Αν βρίσκεστε πίσω από proxy, ρυθμίστε τις ρυθμίσεις proxy της Java πριν από τη μετατροπή.

### Μπορώ να μετατρέψω ένα URL αντί για τοπικό αρχείο;

Απόλυτα. Αντικαταστήστε το `sourceHtmlPath` με μια συμβολοσειρά URL, όπως `"https://example.com/report.html"`. Οι ίδιες επιλογές—JavaScript, DPI, περιθώρια—ισχύουν ακόμη.

### Τι γίνεται με την κατανάλωση μνήμης για πολύ μεγάλες σελίδες;

Η βιβλιοθήκη κάνει streaming του αποτελέσματος, αλλά η απόδοση τεράστιων σελίδων (χιλιάδες κόμβους DOM) μπορεί ακόμα να καταναλώνει RAM. Αν αντιμετωπίσετε `OutOfMemoryError`, αυξήστε το heap της JVM (`-Xmx2g`) ή χωρίστε το HTML σε μικρότερα τμήματα και συγχωνεύστε τα PDF αργότερα.

### Πώς αλλάζω το μέγεθος σελίδας (A4, Letter, κλπ);

Χρησιμοποιήστε `conversionOptions.setPageSize(PageSize.A4);` ή περάστε ένα προσαρμοσμένο αντικείμενο `SizeF`. Η προεπιλογή είναι A4, που λειτουργεί για τις περισσότερες διεθνείς περιπτώσεις χρήσης.

## Συμπέρασμα

Μόλις καλύψαμε όλα όσα χρειάζεστε για **μετατροπή HTML σε PDF** σε Java ενώ **ενεργοποιείτε το JavaScript PDF**, παράγετε ένα **PDF υψηλής ανάλυσης**, **ρυθμίζετε το DPI του PDF**, και εφαρμόζετε **ομοιόμορφα περιθώρια σελίδας**. Ο κώδικας είναι αυτόνομος, τα βήματα εξηγημένα, και τώρα έχετε μια σταθερή βάση για να ενσωματώσετε τη μετατροπή HTML‑σε‑PDF σε οποιαδήποτε εφαρμογή Java.

Τι θα κάνετε στη συνέχεια; Δοκιμάστε να αλλάξετε το DPI σε 600 για ποιότητα εκτυπωτικού καταστήματος, πειραματιστείτε με προσανατολισμό τοπίου, ή συνδέστε πολλά αρχεία HTML σε ένα ενιαίο PDF χρησιμοποιώντας την κλάση `PdfDocument` του Aspose. Η βιβλιοθήκη είναι αρκετά ευέλικτη για επεξεργασία παρτίδας, υδατογράφημα ή ακόμη και ψηφιακή υπογραφή.

Αν αντιμετωπίσετε κάποιο πρόβλημα, ελέγξτε ξανά ότι το JAR του Aspose.HTML ταιριάζει με την έκδοση του JDK σας, και βεβαιωθείτε ότι το αρχείο HTML και οι πόροι του είναι προσβάσιμοι. Καλή προγραμματιστική δουλειά, και εύχομαι τα PDF σας να αποδίδουν πάντα ακριβώς όπως τα φανταζόσασταν!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
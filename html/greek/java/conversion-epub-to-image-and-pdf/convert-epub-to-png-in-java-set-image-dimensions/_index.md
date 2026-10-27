---
category: general
date: 2026-04-09
description: Μάθετε πώς να μετατρέπετε EPUB σε PNG με Java, να ορίζετε τις διαστάσεις
  της εικόνας με στυλ Java και να εξάγετε μόνο την πρώτη σελίδα ως εξώφυλλο PNG. Περιλαμβάνεται
  γρήγορο παράδειγμα κώδικα.
draft: false
keywords:
- convert epub to png
- set image dimensions java
- convert first page png
- aspose html java
- ebook cover generation
language: el
og_description: Μετατρέψτε EPUB σε PNG με Java, ορίστε τις διαστάσεις της εικόνας
  σε Java και εξάγετε μόνο την πρώτη σελίδα ως εξώφυλλο PNG με ένα πλήρες, εκτελέσιμο
  παράδειγμα.
og_title: Μετατροπή EPUB σε PNG σε Java – Ορισμός διαστάσεων εικόνας
tags:
- Java
- Aspose.HTML
- Image Processing
title: Μετατροπή EPUB σε PNG σε Java – Ορισμός διαστάσεων εικόνας
url: /el/java/conversion-epub-to-image-and-pdf/convert-epub-to-png-in-java-set-image-dimensions/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή EPUB σε PNG σε Java – Ορισμός Διαστάσεων Εικόνας

Έχετε αναρωτηθεί ποτέ πώς να **convert EPUB to PNG** χωρίς να ενσωματώνετε μια βαριά βιβλιοθήκη γραφικών; Δεν είστε οι μόνοι. Πολλοί προγραμματιστές χρειάζονται έναν γρήγορο τρόπο για να δημιουργήσουν μια εικόνα εξώφυλλου ή μικρογραφία από ένα e‑book, αλλά συναντούν δυσκολίες όταν το API απαιτεί επιπλέον βήματα για επιλογή σελίδας και μέγεθος.  

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα από μια πλήρη λύση που όχι μόνο **convert EPUB to PNG** αλλά και σας επιτρέπει να **set image dimensions Java** style και **convert first page PNG** με λίγες μόνο γραμμές κώδικα. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση πρόγραμμα που παράγει ένα καθαρό PNG 1024 × 1440 της πρώτης σελίδας οποιουδήποτε αρχείου EPUB.

## Τι Θα Χρειαστείτε

- Java 17 ή νεότερη (ο κώδικας λειτουργεί και με παλαιότερες εκδόσεις, αλλά η 17 είναι η τρέχουσα LTS).  
- Aspose.HTML for Java library (the Maven coordinate is `com.aspose:aspose-html:23.10`).  
- Ένα αρχείο EPUB που θέλετε να μετατρέψετε σε εικόνα.  
- Οποιοδήποτε IDE ή απλή γραμμή εντολών `javac`/`java`.  

Αυτό είναι όλο—χωρίς επιπλέον εργαλεία επεξεργασίας εικόνας, χωρίς εγγενή εκτελέσιμα. Μόνο ένα μόνο JAR και λίγη Java.

## Βήμα 1: Φόρτωση του Εγγράφου EPUB  

Το πρώτο πράγμα που πρέπει να κάνουμε είναι να δώσουμε στο Aspose.HTML κάτι για να δουλέψει. Η φόρτωση ενός EPUB είναι τόσο απλή όσο το να υποδείξουμε τον κατασκευαστή `HTMLDocument` στο μονοπάτι του αρχείου.

```java
import com.aspose.html.HTMLDocument;

// ...

// Replace with the actual path to your EPUB file
String epubPath = "YOUR_DIRECTORY/input.epub";

// Load the EPUB into an HTMLDocument object
HTMLDocument epubDocument = new HTMLDocument(epubPath);
```

*Γιατί είναι σημαντικό:* `HTMLDocument` αφαιρεί τις εσωτερικές HTML, CSS και πόρους του EPUB σε ένα ενιαίο αντικείμενο που μπορεί να αποδώσει ο μετατροπέας. Αν παραλείψετε αυτό το βήμα, η βιβλιοθήκη δεν θα ξέρει τι να σχεδιάσει.

## Βήμα 2: Ορισμός Διαστάσεων Εικόνας Java  

Στη συνέχεια διαμορφώνουμε πώς θα πρέπει να φαίνεται το PNG εξόδου. Η κλάση `ImageSaveOptions` σας επιτρέπει να ελέγξετε τον αριθμό σελίδας, το πλάτος, το ύψος και μια σειρά άλλων σημάνσεων απόδοσης.

```java
import com.aspose.html.converters.ImageSaveOptions;

// ...

ImageSaveOptions imageOptions = new ImageSaveOptions();

// Render only the first page (the cover is usually page 1)
imageOptions.setPageNumber(1);

// Define the desired output size – this is where we **set image dimensions java**
imageOptions.setWidth(1024);   // pixels
imageOptions.setHeight(1440); // pixels
```

*Γιατί μπορεί να αλλάξετε αυτούς τους αριθμούς:* Διάφορες πλατφόρμες απαιτούν διαφορετικά μεγέθη μικρογραφιών. Για ένα εξώφυλλο Kindle μπορεί να χρησιμοποιήσετε 1600 × 2400, ενώ μια προεπισκόπηση ιστού μπορεί να είναι τόσο μικρή όσο 300 × 400. Προσαρμόστε το πλάτος/ύψος ώστε να ταιριάζει στην περίπτωσή σας.

## Βήμα 3: Μετατροπή Πρώτης Σελίδας σε PNG  

Τώρα έρχεται η πραγματική μετατροπή. Παραδίδουμε το `HTMLDocument`, τις επιλογές που μόλις δημιουργήσαμε, και ένα μονοπάτι προορισμού στη στατική μέθοδο `Converter.convertHTML`.

```java
import com.aspose.html.converters.Converter;

// ...

// Output file – this will be the PNG of the first page
String outputPath = "YOUR_DIRECTORY/cover.png";

// Perform the conversion
Converter.convertHTML(epubDocument, imageOptions, outputPath);
```

*Γιατί λειτουργεί:* Το Aspose.HTML αποδίδει την πρώτη σελίδα του EPUB σε ένα bitmap εκτός οθόνης, στη συνέχεια γράφει αυτό το bitmap σε αρχείο PNG χρησιμοποιώντας τις διαστάσεις που δώσατε. Η λειτουργία είναι συγχρονισμένη και ρίχνει εξαίρεση αν κάτι πάει στραβά, ώστε να μπορείτε να το τυλίξετε σε μπλοκ try‑catch για κώδικα παραγωγής.

## Βήμα 4: Επαλήθευση του Αποτελέσματος  

Μετά το τέλος του προγράμματος, θα πρέπει να δείτε ένα αρχείο `cover.png` στη θέση που καθορίσατε. Ανοίξτε το με οποιονδήποτε προβολέα εικόνας για να επιβεβαιώσετε:

- Οι διαστάσεις της εικόνας ταιριάζουν με τις τιμές που ορίσατε (1024 × 1440 στο παράδειγμά μας).  
- Το περιεχόμενο αντιστοιχεί στην πρώτη σελίδα του EPUB (συνήθως το εξώφυλλο ή τη σελίδα τίτλου).  

Αν η εικόνα φαίνεται παραμορφωμένη, ελέγξτε ξανά την αναλογία διαστάσεων που επιλέξατε· ίσως χρειαστεί να διατηρήσετε την αρχική αναλογία ορίζοντας μόνο το πλάτος **ή** το ύψος.

## Βήμα 5: Συνηθισμένα Πιθανά Προβλήματα & Pro Συμβουλές  

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|------|----------------|-----|
| **Blank image** | Το EPUB περιέχει εξωτερικές γραμματοσειρές που δεν είναι ενσωματωμένες. | Εγκαταστήστε τις λείπουν γραμματοσειρές στο σύστημα ή ενσωματώστε τις στο EPUB. |
| **Wrong page rendered** | `setPageNumber` είναι 0‑based σε ορισμένες παλαιότερες εκδόσεις. | Επαληθεύστε την έκδοση της βιβλιοθήκης· για Aspose.HTML 23.x το API είναι 1‑based όπως φαίνεται. |
| **Out‑of‑memory errors** on large pages | Η απόδοση σε πολύ υψηλές αναλύσεις καταναλώνει πολύ RAM. | Μειώστε το πλάτος/ύψος ή αυξήστε τη μνήμη heap του JVM (`-Xmx2g`). |
| **File not found** | Τα strings διαδρομής χρησιμοποιούν backslashes στα Windows χωρίς escaping. | Χρησιμοποιήστε forward slashes ή `Paths.get(...)` για να δημιουργήσετε διαδρομές ανεξάρτητες από την πλατφόρμα. |

*Pro tip:* Αν χρειάζεστε να δημιουργήσετε μικρογραφίες για κάθε σελίδα ενός EPUB, απλώς κάντε βρόχο πάνω στους αριθμούς σελίδων και αλλάξτε `imageOptions.setPageNumber(i)` μέσα στο βρόχο. Θυμηθείτε να δώσετε σε κάθε αρχείο εξόδου ένα μοναδικό όνομα, π.χ., `cover_page_1.png`, `cover_page_2.png`, κλπ.

## Πλήρες Παράδειγμα Λειτουργίας  

Παρακάτω βρίσκεται η πλήρης, έτοιμη‑για‑εκτέλεση κλάση Java. Αντιγράψτε την σε ένα αρχείο με όνομα `EpubToPng.java`, προσαρμόστε τις διαδρομές και εκτελέστε.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.ImageSaveOptions;

/**
 * Demonstrates how to convert an EPUB file to a PNG image,
 * set custom image dimensions, and export only the first page.
 */
public class EpubToPng {
    public static void main(String[] args) throws Exception {

        // --------------------------------------------------------------------
        // Step 1: Load the EPUB document
        // --------------------------------------------------------------------
        // Replace with your actual EPUB location
        HTMLDocument epubDocument = new HTMLDocument("YOUR_DIRECTORY/input.epub");

        // --------------------------------------------------------------------
        // Step 2: Configure conversion options (first page, dimensions)
        // --------------------------------------------------------------------
        ImageSaveOptions imageOptions = new ImageSaveOptions();
        imageOptions.setPageNumber(1);   // Render only the first page
        imageOptions.setWidth(1024);     // Desired width in pixels
        imageOptions.setHeight(1440);    // Desired height in pixels

        // --------------------------------------------------------------------
        // Step 3: Convert the selected page to a PNG image
        // --------------------------------------------------------------------
        // Output PNG path – this will hold the result of the conversion
        Converter.convertHTML(epubDocument, imageOptions, "YOUR_DIRECTORY/cover.png");

        System.out.println("✅ Conversion complete! Check YOUR_DIRECTORY/cover.png");
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Μετά την εκτέλεση `java EpubToPng`, η κονσόλα εκτυπώνει ένα μήνυμα επιτυχίας και θα βρείτε το `cover.png` με μέγεθος **1024 × 1440** pixels, εμφανίζοντας την πρώτη σελίδα του EPUB σας.

## Συμπέρασμα  

Τώρα έχετε μια σταθερή, αυτόνομη συνταγή για **convert EPUB to PNG** σε Java, **set image dimensions Java** σε ό,τι χρειάζεστε, και **convert first page PNG** για δημιουργία εξωφύλλου ή μικρογραφίας. Η προσέγγιση είναι ελαφριά, βασίζεται σε μία κλήση Aspose.HTML, και μπορεί να επεκταθεί για μαζική επεξεργασία πολλαπλών EPUB ή πολλαπλών σελίδων με ελάχιστες αλλαγές.

---

### Τι Ακολουθεί;

- **Batch conversion:** Τυλίξτε τη λογική σε έναν σαρωτή καταλόγου για να επεξεργαστεί αυτόματα δεκάδες αρχεία EPUB.  
- **Dynamic sizing:** Υπολογίστε το πλάτος/ύψος βάσει της αρχικής αναλογίας σελίδας για να αποφύγετε την παραμόρφωση.  
- **Alternative output formats:** Αντικαταστήστε το `ImageSaveOptions` με `PdfSaveOptions` ή `JpegSaveOptions` αν χρειάζεστε PDF ή JPEG αντί για PNG.  

Μη διστάσετε να πειραματιστείτε—αλλάξτε τις διαστάσεις, δοκιμάστε διαφορετικό αριθμό σελίδας, ή ενσωματώστε αυτό το απόσπασμα σε ένα μεγαλύτερο εργαλείο διαχείρισης e‑book. Αν αντιμετωπίσετε προβλήματα, τα docs του Aspose.HTML for Java είναι ένας καλός σύντροφος, αλλά ο παραπάνω κώδικας θα πρέπει να λειτουργεί αμέσως για τις περισσότερες περιπτώσεις.

Καλό κώδικα, και απολαύστε αυτές τις καθαρές PNG εξώφυλλες!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
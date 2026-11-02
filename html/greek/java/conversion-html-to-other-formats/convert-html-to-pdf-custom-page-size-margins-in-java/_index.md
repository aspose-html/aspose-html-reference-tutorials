---
category: general
date: 2026-04-03
description: Μετατρέψτε HTML σε PDF χρησιμοποιώντας το Aspose.HTML σε Java με προσαρμοσμένο
  μέγεθος σελίδας PDF, ορίστε τα περιθώρια PDF και το πλάτος σελίδας PDF. Μάθετε πώς
  να μετατρέπετε HTML γρήγορα.
draft: false
keywords:
- convert html to pdf
- custom pdf page size
- set pdf margins
- how to convert html
- set pdf page width
language: el
og_description: Μετατρέψτε HTML σε PDF χρησιμοποιώντας το Aspose.HTML σε Java. Αυτός
  ο οδηγός δείχνει πώς να ορίσετε προσαρμοσμένο μέγεθος σελίδας PDF, περιθώρια και
  πλάτος σελίδας για τέλεια αποτελέσματα.
og_title: Μετατροπή HTML σε PDF – Προσαρμοσμένο μέγεθος σελίδας & περιθώρια σε Java
tags:
- Java
- PDF
- Aspose.HTML
title: Μετατροπή HTML σε PDF – Προσαρμοσμένο μέγεθος σελίδας & περιθώρια σε Java
url: /el/java/conversion-html-to-other-formats/convert-html-to-pdf-custom-page-size-margins-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή HTML σε PDF – Προσαρμοσμένο Μέγεθος Σελίδας & Περιθώρια σε Java

Έχετε ποτέ χρειαστεί να **μετατρέψετε HTML σε PDF** και αναρωτηθήκατε πώς να ελέγξετε τις διαστάσεις της σελίδας; Σε αυτό το tutorial θα σας καθοδηγήσουμε βήμα‑βήμα μέσα από μια πλήρη, έτοιμη‑για‑εκτέλεση λύση που δείχνει πώς να **μετατρέψετε HTML σε PDF** με *προσαρμοσμένο μέγεθος σελίδας PDF*, πώς να **ορίσετε περιθώρια PDF**, και ακόμη πώς να **ορίσετε το πλάτος της σελίδας PDF** χρησιμοποιώντας το Aspose.HTML for Java.  

Αν δημιουργείτε τιμολόγια, αναφορές ή e‑books, αυτές οι ρυθμίσεις διάταξης είναι η διαφορά μεταξύ ενός απλού σωρού κειμένου και ενός επαγγελματικού εγγράφου που φαίνεται ακριβώς όπως το θέλετε.

## Τι Θα Μάθετε

* Πώς να δημιουργήσετε ένα απλό έργο Maven/Gradle με Aspose.HTML.  
* Γιατί η επιλογή του σωστού μεγέθους σελίδας είναι σημαντική για εκτύπωση και απόδοση στην οθόνη.  
* Ο κώδικας βήμα‑βήμα για **μετατροπή HTML σε PDF** με προσαρμογή ύψους, πλάτους και περιθωρίων.  
* Συνηθισμένα προβλήματα (όπως ελλιπείς ερωτήματα CSS media) και πώς να τα αποφύγετε.  
* Πώς να επαληθεύσετε ότι το PDF δημιουργήθηκε σωστά.

Δεν απαιτείται προηγούμενη εμπειρία με το Aspose—απλώς ένα βασικό IDE Java και η δυνατότητα εκτέλεσης μιας μεθόδου `main`.

## Απαιτήσεις

* **Java 17** (ή οποιοδήποτε πρόσφατο JDK) εγκατεστημένο στον υπολογιστή σας.  
* **Aspose.HTML for Java** βιβλιοθήκη – μπορείτε να κατεβάσετε το πιο πρόσφατο JAR από το Maven Central (`com.aspose:aspose-html:23.9` τη στιγμή της συγγραφής).  
* Ένα απλό αρχείο HTML (`input.html`) που θέλετε να μετατρέψετε σε PDF.  
* Προαιρετικά: ένας επεξεργαστής εικόνας αν θέλετε να προεπισκοπήσετε το αποτέλεσμα PDF.

> **Pro tip:** Αν χρησιμοποιείτε Maven, προσθέστε την εξάρτηση παρακάτω στο `pom.xml`. Αν προτιμάτε Gradle, οι ίδιες συντεταγμένες λειτουργούν με τη ρύθμιση `implementation`.

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

```groovy
// Gradle
implementation 'com.aspose:aspose-html:23.9'
```

## Μετατροπή HTML σε PDF – Ρύθμιση του Έργου

Πρώτα απ' όλα: δημιουργήστε μια νέα κλάση Java με όνομα `PdfConversionAdvanced`. Αυτή η κλάση θα περιέχει όλη τη λογική μετατροπής. Τα imports που χρειάζεστε αναφέρονται στην αρχή του αρχείου—μην διστάσετε να τα αντιγράψετε‑και‑επικολλήσετε απευθείας.

```java
import com.aspose.html.*;
import com.aspose.html.converters.*;
import com.aspose.html.converters.pdf.*;

public class PdfConversionAdvanced {
    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1: Point to the source HTML file you want to convert.
        // -----------------------------------------------------------------
        String inputHtmlPath = "YOUR_DIRECTORY/input.html";

        // -----------------------------------------------------------------
        // Step 2: Create PdfSaveOptions and configure custom page size.
        // -----------------------------------------------------------------
        PdfSaveOptions pdfOptions = new PdfSaveOptions();

        // A5 size in points (1 pt = 1/72 inch). Adjust as needed.
        pdfOptions.setPageWidth(420);   // set pdf page width
        pdfOptions.setPageHeight(595);  // set pdf page height

        // -----------------------------------------------------------------
        // Step 3: Define margins – 10 mm ≈ 28.35 points.
        // -----------------------------------------------------------------
        pdfOptions.setMarginTop(28.35);
        pdfOptions.setMarginBottom(28.35);
        pdfOptions.setMarginLeft(28.35);
        pdfOptions.setMarginRight(28.35);

        // -----------------------------------------------------------------
        // Step 4: Make sure the converter uses the "print" media type.
        // -----------------------------------------------------------------
        pdfOptions.setMediaType("print");

        // -----------------------------------------------------------------
        // Step 5: Perform the conversion.
        // -----------------------------------------------------------------
        String outputPdfPath = "YOUR_DIRECTORY/output.pdf";
        Converter.convert(inputHtmlPath, outputPdfPath, pdfOptions);

        // -----------------------------------------------------------------
        // Step 6: Confirm the file was created.
        // -----------------------------------------------------------------
        System.out.println("PDF created with custom layout at " + outputPdfPath);
    }
}
```

### Γιατί Αυτές οι Ρυθμίσεις Είναι Σημαντικές

* **Custom PDF page size** (`setPageWidth` / `setPageHeight`) σας επιτρέπει να στοχεύσετε A5, Letter ή οποιαδήποτε προσαρμοσμένη διάσταση χρειάζεστε. Αν το παραλείψετε, το Aspose προεπιλέγει A4, κάτι που μπορεί να σπαταλήσει χαρτί ή να «σπάσει» το σχέδιο.  
* **Set PDF margins** εξασφαλίζει ότι το περιεχόμενο δεν αγγίζει τις άκρες της σελίδας—κρίσιμο για εκτυπωτές που απαιτούν μη‑εκτυπώσιμο περιθώριο.  
* **Media type “print”** αναγκάζει τη μηχανή να εφαρμόσει οποιοδήποτε `@media print` CSS έχετε ορίσει, δίνοντάς σας ακριβή έλεγχο πάνω σε γραμματοσειρές, χρώματα και διάταξη που διαφέρουν από την προβολή στην οθόνη.

## Ορισμός Προσαρμοσμένου Μεγέθους Σελίδας PDF

Αν το προεπιλεγμένο μέγεθος A4 δεν είναι κατάλληλο για το έργο σας, μπορείτε να χρησιμοποιήσετε οποιεσδήποτε διαστάσεις θέλετε. Το παραπάνω απόσπασμα κώδικα δείχνει ήδη μια κλασική διάταξη A5, αλλά ας εξετάσουμε μερικές εναλλακτικές:

| Μέγεθος | Πλάτος (pt) | Ύψος (pt) |
|------|------------|------------|
| **Letter** | 612 | 792 |
| **Legal** | 612 | 1008 |
| **Custom 8×10 inches** | 576 | 720 |

Για να εφαρμόσετε ένα προσαρμοσμένο μέγεθος, απλώς αντικαταστήστε τις τιμές που περνιούνται στο `setPageWidth` και `setPageHeight`. Θυμηθείτε: **1 point = 1/72 ίντσα**, οπότε ένας γρήγορος πολλαπλασιασμός σας δίνει τους σωστούς αριθμούς.

> **Note:** Αν χρειάζεστε αλλαγή από πορτραίτο σε τοπίο, απλώς ανταλλάξτε τις τιμές πλάτους και ύψους.

## Ορισμός Περιθωρίων PDF για Ακριβή Διάταξη

Τα περιθώρια εκφράζονται επίσης σε points. Το παράδειγμα χρησιμοποιεί **10 mm** (≈ 28.35 pt) σε όλες τις πλευρές. Θέλετε πιο σφιχτή διάταξη; Αλλάξτε τους αριθμούς:

```java
pdfOptions.setMarginTop(14.18);    // 5 mm
pdfOptions.setMarginBottom(14.18);
pdfOptions.setMarginLeft(21.26);   // 7.5 mm
pdfOptions.setMarginRight(21.26);
```

Γιατί να ασχοληθείτε; Οι εκτυπωτές συχνά έχουν ελάχιστη εκτυπώσιμη περιοχή—ο ορισμός περιθωρίων αποτρέπει το κλάψιμο του περιεχομένου. Επίσης, ένα συνεπές περιθώριο δίνει στο PDF σας επαγγελματική εμφάνιση, ειδικά όταν δημιουργείτε συμβόλαια ή πιστοποιητικά.

## Δυναμική Προσαρμογή Πλάτους (και Ύψους) Σελίδας PDF

Μερικές φορές το HTML που λαμβάνετε περιέχει ήδη μια ένδειξη πλάτους (π.χ., ένα `<div>` με στυλ 800 px). Μπορείτε να υπολογίσετε το απαιτούμενο πλάτος PDF «on the fly»:

```java
int htmlWidthPx = 800;                     // example from HTML
double pointsPerPixel = 0.75;              // 96 DPI => 0.75 pt per pixel
pdfOptions.setPageWidth(htmlWidthPx * pointsPerPixel);
```

Αυτή η τεχνική εξασφαλίζει ότι το PDF αντικατοπτρίζει την αρχική διάταξη χωρίς παραμόρφωση. Είναι ένα χρήσιμο κόλπο όταν **πώς να μετατρέψετε HTML** που αρχικά σχεδιάστηκε για προβολή στην οθόνη.

## Εκτέλεση της Μετατροπής και Επαλήθευση του Αποτελέσματος

Αφού ρυθμίσετε τα πάντα, εκτελέστε τη μέθοδο `main`. Αν όλα είναι σωστά συνδεδεμένα, θα δείτε:

```
PDF created with custom layout at YOUR_DIRECTORY/output.pdf
```

Ανοίξτε το παραγόμενο PDF σε οποιονδήποτε προβολέα (Adobe Reader, Chrome ή την προεπισκόπηση του λειτουργικού σας συστήματος). Θα πρέπει να δείτε:

* Το ακριβές μέγεθος σελίδας που ορίσατε.  
* Ομοιόμορφα περιθώρια γύρω από το περιεχόμενο.  
* CSS που εφαρμόζεται όπως αν η σελίδα εκτυπώνεται (ευχαριστώντας το `setMediaType("print")`).

![Παράδειγμα εξόδου μετατροπής HTML σε PDF](https://example.com/convert-html-to-pdf-output.png "παράδειγμα εξόδου μετατροπής html σε pdf")

*Το κείμενο alt της εικόνας περιλαμβάνει τη βασική λέξη‑κλειδί για SEO.*

## Κοινές Ακραίες Περιπτώσεις & Πώς να τις Διαχειριστείτε

| Πρόβλημα | Σύμπτωμα | Διόρθωση |
|-------|---------|-----|
| **Λείπει CSS** | Το κείμενο φαίνεται απλό, χωρίς γραμματοσειρές ή χρώματα. | Βεβαιωθείτε ότι έχει οριστεί `pdfOptions.setMediaType("print")` και ότι το HTML σας συνδέεται με το φύλλο στυλ με απόλυτη διαδρομή ή ενσωματώνει το CSS εντός. |
| **Μεγάλες Εικόνες Κόβονται** | Οι εικόνες περικόπτονται στα όρια της σελίδας. | Αλλάξτε το μέγεθος των εικόνων στο HTML ή ορίστε `pdfOptions.setImageResolution(300)` για αύξηση DPI, έπειτα προσαρμόστε τα περιθώρια. |
| **Χαρακτήρες Unicode Δεν Απεικονίζονται** | Τα ειδικά σύμβολα εμφανίζονται ως κουτάκια. | Προσθέστε μια γραμματοσειρά που υποστηρίζει τους χαρακτήρες και αναφερθείτε σε αυτή στο CSS (`@font-face`). |
| **Καθυστέρηση Απόδοσης σε Μεγάλες Εγγραφές** | Η μετατροπή διαρκεί >30 δευτερόλεπτα. | Χρησιμοποιήστε `pdfOptions.setEnableThreading(true)` (αν υποστηρίζεται) ή χωρίστε το HTML σε μικρότερα τμήματα και συγχωνεύστε τα PDF αργότερα. |

## Πλήρες Παράδειγμα Εργασίας (Όλα Μαζί)

Ακολουθεί ολόκληρο το αρχείο που μπορείτε να ενσωματώσετε σε ένα νέο έργο. Αντικαταστήστε το `YOUR_DIRECTORY` με μια πραγματική διαδρομή φακέλου στον υπολογιστή σας.

```java
import com.aspose.html.*;
import com.aspose.html.converters.*;
import com.aspose.html.converters.pdf.*;

public class PdfConversionAdvanced {
    public static void main(String[] args) throws Exception {

        // Step 1: Source HTML location
        String inputHtmlPath = "C:/pdf-demo/input.html";

        // Step 2: Configure PDF options – custom size and margins
        PdfSaveOptions pdfOptions = new PdfSaveOptions();
        pdfOptions.setPageWidth(420);   // custom pdf page width (A5)
        pdfOptions.setPageHeight(595);  // custom pdf page height (A5)

        // Set margins – 10 mm ≈ 28.35 pt
        pdfOptions.setMarginTop(28.35);
        pdfOptions.setMarginBottom(28.35);
        pdfOptions.setMarginLeft(28.35);
        pdfOptions.setMarginRight(28.35);

        // Ensure print CSS is used
        pdfOptions.setMediaType("print");

        // Step 3: Destination PDF file
        String outputPdfPath = "C:/pdf-demo/output.pdf";

        // Step 4: Perform conversion
        Converter.convert(inputHtmlPath, outputPdfPath, pdfOptions);

        // Step 5: Confirmation
        System.out.println("PDF created with custom layout at " + outputPdfPath);
    }
}
```

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-03-26
description: Δημιουργήστε PDF προσαρμοσμένου μεγέθους από HTML χρησιμοποιώντας το
  Aspose.HTML για Java. Μάθετε πώς να μετατρέπετε HTML σε PDF και να ορίζετε το μέγεθος
  σελίδας του PDF σε λίγα μόνο βήματα.
draft: false
keywords:
- create pdf custom size
- convert html to pdf
- change pdf page size
- generate pdf from html
- set pdf page size
language: el
og_description: Δημιουργήστε προσαρμοσμένο μέγεθος PDF από HTML με το Aspose. Αυτός
  ο οδηγός σας δείχνει πώς να μετατρέψετε HTML σε PDF, να αλλάξετε το μέγεθος σελίδας
  PDF και να ορίσετε το μέγεθος σελίδας PDF εύκολα.
og_title: Δημιουργία PDF Προσαρμοσμένου Μεγέθους – Σύντομος Οδηγός για τη Μετατροπή
  HTML σε PDF
tags:
- aspose
- java
- pdf
- html
title: Δημιουργία PDF προσαρμοσμένου μεγέθους – Μετατροπή HTML σε PDF με το Aspose
url: /el/java/conversion-html-to-other-formats/create-pdf-custom-size-convert-html-to-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία PDF Προσαρμοσμένου Μεγέθους – Μετατροπή HTML σε PDF με Aspose

Σας έχει ξανασυμβεί να χρειαστείτε **να δημιουργήσετε PDF προσαρμοσμένου μεγέθους** από ένα αρχείο HTML; Σε αυτό το tutorial θα σας δείξουμε πώς να **μετατρέψετε HTML σε PDF** και να ορίσετε το μέγεθος της σελίδας PDF χρησιμοποιώντας το Aspose.HTML for Java.  

Αν δημιουργείτε τιμολόγια, αναφορές ή e‑books, η ακριβής διάσταση της σελίδας είναι σημαντική — διαφορετικά η διάταξη φαίνεται εκτός κέντρου ή αποκόπτεται.  

Θα περάσουμε από κάθε βήμα, από τη φόρτωση του πηγαίου HTML μέχρι τη ρύθμιση των περιθωρίων, και θα ολοκληρώσουμε με ένα έτοιμο PDF. Χωρίς ασαφείς αναφορές, μόνο ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να αντιγράψετε‑επικολλήσετε σήμερα.

## Τι Θα Χρειαστείτε

- **Java 17** (ή οποιοδήποτε πρόσφατο JDK).  
- **Aspose.HTML for Java** JARs – μπορείτε να πάρετε την πιο πρόσφατη έκδοση από το αποθετήριο Maven ή τον ιστότοπο Aspose.  
- Ένα απλό αρχείο `input.html` τοποθετημένο σε φάκελο που ελέγχετε.  
- Ένα IDE ή κειμενογράφο της επιλογής σας· εγώ συνήθως κωδικοποιώ στο IntelliJ IDEA, αλλά το Eclipse λειτουργεί εξίσου καλά.

Η ύπαρξη αυτών των προαπαιτήσεων σημαίνει ότι δεν θα αντιμετωπίσετε σφάλματα “class not found” στη μέση της διαδικασίας.  

Τώρα, ας βουτήξουμε.

![Δημιουργία PDF προσαρμοσμένου μεγέθους παράδειγμα](/images/create-pdf-custom-size.png "Στιγμιότυπο οθόνης που δείχνει ένα PDF που δημιουργήθηκε με προσαρμοσμένο μέγεθος σελίδας και περιθώρια – create pdf custom size")

## Δημιουργία PDF Προσαρμοσμένου Μεγέθους – Κύρια Βήματα

Παρακάτω είναι το πλήρες πρόγραμμα Java που θα προκύψει. Μπορείτε ελεύθερα να το αντιγράψετε σε ένα αρχείο με όνομα `ConvertHtmlToPdfCustomPage.java` και να το εκτελέσετε αφού προσθέσετε τις εξαρτήσεις Aspose στο έργο σας.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.PdfConversionOptions;
import com.aspose.html.saving.PageSize;
import com.aspose.html.saving.Margin;

public class ConvertHtmlToPdfCustomPage {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the source HTML document
        HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/input.html");

        // Step 2: Set up PDF conversion options
        PdfConversionOptions pdfOptions = new PdfConversionOptions();
        pdfOptions.setPageSize(PageSize.A4); // Choose page size (A4, Letter, etc.)
        pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Portrait); // Portrait or Landscape
        pdfOptions.setMargins(new Margin(20, 20, 20, 20)); // Margins: left, top, right, bottom (points)

        // Step 3: Convert the HTML document to a PDF file with the custom settings
        Converter.convertHTML(htmlDoc, "YOUR_DIRECTORY/custom_page.pdf", pdfOptions);

        // Step 4: Inform the user that the PDF has been created
        System.out.println("PDF generated with custom page size and margins.");
    }
}
```

### Βήμα 1 – Μετατροπή HTML σε PDF: Φόρτωση του Εγγράφου

Το πρώτο που κάνουμε είναι **να φορτώσουμε το HTML** που θέλουμε να μετατρέψουμε σε PDF.  
`HTMLDocument` διαβάζει το αρχείο, επιλύει σχετικούς συνδέσμους και δημιουργεί ένα DOM που μπορεί να αποδώσει το Aspose.  

> **Γιατί είναι σημαντικό:** Αν το HTML αναφέρει CSS ή εικόνες, το Aspose θα τις ανακτήσει σε σχέση με τη διαδρομή του αρχείου. Η χρήση απόλυτης διαδρομής (`YOUR_DIRECTORY/input.html`) αποτρέπει εκπλήξεις “file not found”.

### Βήμα 2 – Αλλαγή Μεγέθους Σελίδας PDF: Διαμόρφωση Επιλογών

Εδώ δημιουργούμε ένα αντικείμενο `PdfConversionOptions`.  
- `setPageSize(PageSize.A4)` λέει στο Aspose να χρησιμοποιήσει τις τυπικές διαστάσεις A4 (210 × 297 mm).  
- `setPageOrientation(...)` περιστρέφει τη σελίδα αν χρειάζεστε τοπία.  
- `setMargins(new Margin(20, 20, 20, 20))` θέτει περιθώριο 20 points σε κάθε πλευρά.

Μπορείτε να αντικαταστήσετε το `PageSize.A4` με `PageSize.LETTER` ή ακόμη και με **προσαρμοσμένο μέγεθος** περνώντας ένα αντικείμενο `SizeF`, π.χ.:

```java
pdfOptions.setPageSize(new SizeF(500, 800)); // width, height in points
```

> **Pro tip:** Ένα point ισούται με 1/72 ίντσα. Αν σκέφτεστε σε χιλιοστά, πολλαπλασιάστε με 2.83465 για να πάρετε points.

### Βήμα 3 – Δημιουργία PDF από HTML: Εκτέλεση της Μετατροπής

`Converter.convertHTML` κάνει το σκληρό κομμάτι. Παίρνει το φορτωμένο `HTMLDocument`, τη διαδρομή εξόδου και τις επιλογές που μόλις διαμορφώσαμε.  

Αν θέλετε να **ορίσετε το μέγεθος σελίδας PDF** δυναμικά βάσει του περιεχομένου, μπορείτε να υπολογίσετε τις απαιτούμενες διαστάσεις πριν από αυτό το βήμα και να προσαρμόσετε το `pdfOptions` αναλόγως.

### Βήμα 4 – Επαλήθευση του Αποτελέσματος

Η γραμμή `System.out.println` είναι προαιρετική, αλλά παρέχει γρήγορη ανάδραση όταν τρέχετε το πρόγραμμα από κονσόλα. Μετά την εκτέλεση, ανοίξτε το `custom_page.pdf` – θα πρέπει να δείτε ένα PDF A4 πορτραίτου με ομοιόμορφα περιθώρια 20 points, ακριβώς όπως ορίσαμε.

## Μετατροπή HTML σε PDF – Συνηθισμένες Παραλλαγές

### Χρήση Stream αντί για Διαδρομή Αρχείου

Μερικές φορές δεν έχετε φυσικό αρχείο· ίσως το HTML προέρχεται από βάση δεδομένων ή API. Σε αυτή την περίπτωση, τυλίξτε τη συμβολοσειρά σε ένα `ByteArrayInputStream`:

```java
String htmlContent = "<html><body><h1>Hello, PDF!</h1></body></html>";
HTMLDocument htmlDoc = new HTMLDocument(
        new ByteArrayInputStream(htmlContent.getBytes(StandardCharsets.UTF_8)),
        "http://example.com/");
```

Το δεύτερο όρισμα είναι η βασική URL για την επίλυση σχετικών πόρων.

### Αλλαγή Προσανατολισμού Σελίδας

Αν η αναφορά σας είναι πλατιά, αλλάξτε σε τοπία:

```java
pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Landscape);
```

### Λεπτομερής Ρύθμιση Περιθωρίων

Τα περιθώρια δέχονται τιμές κινητής υποδιαστολής, έτσι μπορείτε να θέσετε 0.5 pt για ένα εξαιρετικά λεπτό περιθώριο:

```java
pdfOptions.setMargins(new Margin(5.5, 10.2, 5.5, 10.2));
```

### Διαχείριση Μεγάλων Αρχείων HTML

Για τεράστια έγγραφα, σκεφτείτε να ενεργοποιήσετε **memory‑efficient streaming**:

```java
pdfOptions.setUseMemoryCache(true);
```

Αυτό λέει στο Aspose να γράφει ενδιάμεσα δεδομένα σε προσωρινά αρχεία αντί να τα κρατά όλα στη μνήμη RAM.

## Ορισμός Μεγέθους Σελίδας PDF – Ακραίες Περιπτώσεις & Πιθανά Προβλήματα

- **Missing Fonts:** Αν το HTML σας χρησιμοποιεί προσαρμοσμένη γραμματοσειρά που δεν είναι εγκατεστημένη στον server, το PDF θα επιστρέψει σε προεπιλεγμένη. Ενσωματώστε τη γραμματοσειρά με `pdfOptions.getFontEmbeddingMode().setEmbeddingMode(EmbeddingMode.Always);`.  
- **Image Scaling:** Υψηλής ανάλυσης εικόνες μπορούν να αυξήσουν το μέγεθος του PDF. Χρησιμοποιήστε `pdfOptions.setImageResolution(150);` για να μειώσετε την ανάλυση διατηρώντας την ποιότητα.  
- **CSS Compatibility:** Δεν υποστηρίζονται όλες οι ιδιότητες CSS πλήρως. Κρατήστε τα σε τυπικές τεχνικές διάταξης (το flexbox λειτουργεί, αλλά το grid μπορεί να έχει ιδιόρρυθμες συμπεριφορές).  
- **Path Permissions:** Βεβαιωθείτε ότι η διαδικασία έχει δικαιώματα εγγραφής στο `YOUR_DIRECTORY`. Διαφορετικά, θα προκληθεί `IOException`.

## Αναμενόμενο Αποτέλεσμα

Η εκτέλεση του προγράμματος παράγει ένα PDF που φαίνεται ως εξής (εννοιολογική απεικόνιση):

```
+---------------------------------------------------+
|                     Header                        |
|                                                   |
|   (HTML rendered content goes here)               |
|                                                   |
|                     Footer                        |
+---------------------------------------------------+
```

- Μέγεθος σελίδας: **A4** (210 × 297 mm).  
- Προσανατολισμός: **Portrait**.  
- Περιθώρια: **20 pt** σε κάθε πλευρά.  

Ανοίξτε το αρχείο με οποιονδήποτε προβολέα PDF (Adobe Reader, Chrome, κ.λπ.) για να το επιβεβαιώσετε.

## Συμπεράσματα

Τώρα ξέρετε πώς να **δημιουργήσετε PDF προσαρμοσμένου μεγέθους** από μια πηγή HTML χρησιμοποιώντας το Aspose.HTML for Java. Το tutorial κάλυψε ολόκληρη τη ροή: **μετατροπή HTML σε PDF**, **αλλαγή μεγέθους σελίδας PDF**, **ορισμός μεγέθους σελίδας PDF**, και **δημιουργία PDF από HTML** με προσαρμοσμένα περιθώρια.  

Μη διστάσετε να πειραματιστείτε—αντικαταστήστε το `PageSize.LETTER` με νομικό μέγεθος, τροποποιήστε τα περιθώρια ή ενσωματώστε τις δικές σας γραμματοσειρές. Στη συνέχεια, μπορείτε να εξερευνήσετε **προσθήκη υδατογραφήματος**, **κρυπτογράφηση του PDF**, ή **μαζική επεξεργασία πολλαπλών αρχείων HTML**. Όλα αυτά τα θέματα βασίζονται στις ίδιες βασικές έννοιες που καλύψαμε.  

Έχετε ερώτηση για κάποια συγκεκριμένη ακραία περίπτωση; Αφήστε ένα σχόλιο παρακάτω και θα σας βοηθήσω να το επιλύσετε. Καλό κώδικα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
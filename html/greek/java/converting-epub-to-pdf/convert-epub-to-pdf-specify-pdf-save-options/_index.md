---
date: 2026-05-30
description: Μάθετε πώς να μετατρέψετε EPUB σε PDF σε Java με Aspose.HTML ενώ ορίζετε
  ένα προσαρμοσμένο μέγεθος σελίδας PDF και άλλες επιλογές αποθήκευσης PDF.
keywords:
- custom pdf page size
- convert epub to pdf
- change pdf background color
- specify pdf page dimensions
- aspose.html java
linktitle: Καθορισμός Επιλογών Αποθήκευσης PDF για EPUB σε PDF
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  headline: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  type: TechArticle
- description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  name: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  steps:
  - name: Open the EPUB File
    text: First, create a `FileInputStream` that points to your source `.epub`. Keeping
      the stream open until the conversion finishes prevents “blank page” errors.
  - name: Define PDF Save Options
    text: '`PdfSaveOptions` is Aspose.HTML''s configuration class that controls PDF
      output settings such as page size, background color, and margins. `Length.fromPixels`
      converts screen pixels to PDF points (1 point = 1/72 inch), allowing you to
      specify dimensions in familiar pixel units.'
  - name: Convert EPUB to PDF
    text: With the input stream and custom options ready, invoke the converter. The
      output PDF will be saved to the location you specify, preserving the exact page
      dimensions you defined. `PdfSaveOptions.setEnableParallelProcessing` is a method
      that enables parallel processing of pages during PDF conversion.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a commercial library, but you can obtain a free
      trial version from their [website](https://releases.aspose.com/).
    question: Is Aspose.HTML for Java a free library?
  - answer: Aspose.HTML for Java supports EPUB 2.0, EPUB 3.0, and EPUB 3.1, handling
      re‑flowable and fixed‑layout books with full CSS support.
    question: What EPUB formats are supported for conversion?
  - answer: Yes, you can customize the PDF output by adjusting the page setup, background
      color, compression level, and other settings in the `PdfSaveOptions`.
    question: Can I customize the PDF output further?
  - answer: The trial version may add a watermark to the first few pages and limits
      the maximum file size to 10 MB; purchase a license to remove these restrictions.
    question: Are there any limitations to the trial version of Aspose.HTML for Java?
  - answer: You can find answers to your questions and seek support on the [Aspose.HTML
      forum](https://forum.aspose.com/).
    question: Where can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: Προσαρμοσμένο Μέγεθος Σελίδας PDF - Καθορισμός Επιλογών Αποθήκευσης PDF για
  EPUB σε PDF
url: /el/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσαρμοσμένο Μέγεθος Σελίδας PDF: Καθορισμός Επιλογών Αποθήκευσης PDF για EPUB σε PDF

## Εισαγωγή

Το Aspose.HTML for Java καθιστά εύκολη τη **μετατροπή EPUB σε PDF** και σας παρέχει πλήρη έλεγχο του αποτελέσματος, συμπεριλαμβανομένου του καθορισμού ενός **προσαρμοσμένου μεγέθους σελίδας PDF**. Σε αυτόν τον οδηγό βήμα‑βήμα θα καλύψουμε όλα όσα χρειάζεστε—από την προετοιμασία του περιβάλλοντος μέχρι την προσαρμογή του `PdfSaveOptions` ώστε το παραγόμενο PDF να ταιριάζει ακριβώς με τις διαστάσεις σελίδας που απαιτείτε. Είτε δημιουργείτε μια αλυσίδα δημοσίευσης, μια πλατφόρμα e‑learning, είτε απλώς χρειάζεστε αυτοματοποίηση της μετατροπής εγγράφων, οι τεχνικές εδώ θα σας φανούν χρήσιμες.

## Γρήγορες Απαντήσεις
- **Ποιος είναι ο κύριος σκοπός αυτού του οδηγού;** Μετατροπή ενός αρχείου EPUB σε PDF με εφαρμογή προσαρμοσμένου μεγέθους σελίδας PDF.  
- **Ποια βιβλιοθήκη χρησιμοποιείται;** Aspose.HTML for Java.  
- **Χρειάζομαι άδεια;** Διατίθεται δωρεάν δοκιμαστική έκδοση· απαιτείται εμπορική άδεια για παραγωγή.  
- **Μπορώ να αλλάξω το χρώμα φόντου;** Ναι, χρησιμοποιώντας το `PdfSaveOptions`.  
- **Υποστηρίζεται η Java 8+;** Απόλυτα—οποιοδήποτε σύγχρονο περιβάλλον Java λειτουργεί.

## Τι είναι ένα προσαρμοσμένο μέγεθος σελίδας PDF;

Ένα προσαρμοσμένο μέγεθος σελίδας PDF σας επιτρέπει να ορίσετε το ακριβές πλάτος και το ύψος κάθε σελίδας στο παραγόμενο PDF, αντί να βασίζεστε σε τυπικά μεγέθη όπως A4 ή Letter. Μπορείτε να ορίσετε τις διαστάσεις σε points (1 point = 1/72 inch) ή να τις μετατρέψετε από pixels, παρέχοντάς σας έλεγχο pixel‑perfect πάνω στην τελική διάταξη. Αυτό είναι ιδανικό για e‑books, φυλλάδια ή οποιοδήποτε σχέδιο που πρέπει να ταιριάζει με προκαθορισμένο φορμά χωρίς χειροκίνητη επεξεργασία.

## Γιατί να χρησιμοποιήσετε το Aspose.HTML για μετατροπή EPUB σε PDF;

Το Aspose.HTML μετατρέπει EPUB σε PDF με δύο γραμμές κώδικα διατηρώντας πολύπλοκες διατάξεις, ενσωματωμένες γραμματοσειρές και εικόνες υψηλής ανάλυσης. Υποστηρίζει **πάνω από 50 μορφές εισόδου και εξόδου**, μπορεί να αποδώσει PDF έως **2.000 σελίδες** χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη, και λειτουργεί σε Windows, Linux και macOS με τα ίδια αποτελέσματα. Η βιβλιοθήκη προσφέρει επίσης λεπτομερείς επιλογές αποθήκευσης PDF, επιτρέποντάς σας να ρυθμίσετε το μέγεθος σελίδας, το χρώμα φόντου, τα περιθώρια και τις ρυθμίσεις συμπίεσης—όλα από τη Java.

## Προαπαιτούμενα
- **Περιβάλλον Ανάπτυξης Java:** JDK 8 ή νεότερο εγκατεστημένο και διαμορφωμένο.  
- **Aspose.HTML for Java:** Κατεβάστε το τελευταίο JAR από την [ιστοσελίδα](https://releases.aspose.com/html/java/).  
- **Αρχείο EPUB:** Ένα έγγραφο `.epub` που θέλετε να μετατρέψετε.  

Τώρα που όλα είναι έτοιμα, ας βουτήξουμε στα πραγματικά βήματα μετατροπής.

## Πώς να μετατρέψετε EPUB σε PDF με προσαρμοσμένο μέγεθος σελίδας;

`FileInputStream` είναι μια κλάση της Java που διαβάζει ακατέργαστα bytes από ένα αρχείο. `PdfSaveOptions` είναι μια κλάση στο Aspose.HTML που ρυθμίζει τις ρυθμίσεις εξόδου PDF όπως το μέγεθος σελίδας και το χρώμα φόντου. Φορτώστε το EPUB σας με ένα `FileInputStream`, διαμορφώστε το `PdfSaveOptions` για να ορίσετε τις ακριβείς διαστάσεις σελίδας, και καλέστε τον μετατροπέα. Η παρακάτω διαδικασία τριών βημάτων εκτελεί τη μετατροπή σε λιγότερο από ένα λεπτό για τυπικά μεγέθη e‑book, και κλιμακώνεται σε μεγαλύτερες συλλογές με ελάχιστες αλλαγές κώδικα.

### Βήμα 1: Άνοιγμα του Αρχείου EPUB

Αρχικά, δημιουργήστε ένα `FileInputStream` που δείχνει στο πηγαίο σας `.epub`. Η διατήρηση του ρεύματος ανοιχτού μέχρι να ολοκληρωθεί η μετατροπή αποτρέπει σφάλματα «κενής σελίδας».

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

### Βήμα 2: Ορισμός Επιλογών Αποθήκευσης PDF

`PdfSaveOptions` είναι η κλάση διαμόρφωσης του Aspose.HTML που ελέγχει τις ρυθμίσεις εξόδου PDF όπως το μέγεθος σελίδας, το χρώμα φόντου και τα περιθώρια. `Length.fromPixels` μετατρέπει τα pixel της οθόνης σε PDF points (1 point = 1/72 ίντσα), επιτρέποντάς σας να ορίσετε διαστάσεις σε γνωστές μονάδες pixel.

```java
com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
anyPage.setSize(new com.aspose.html.drawing.Size(
    com.aspose.html.drawing.Length.fromPixels(3000),
    com.aspose.html.drawing.Length.fromPixels(1000))
);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
```

#### Συμβουλή:
- **Pixels vs. Points:** `Length.fromPixels` μετατρέπει τα pixel της οθόνης σε PDF points (1 point = 1/72 ίντσα). Επιλέξτε τιμές που αντανακλούν το τελικό εκτυπωμένο μέγεθος που χρειάζεστε.

### Βήμα 3: Μετατροπή EPUB σε PDF

Με το ρεύμα εισόδου και τις προσαρμοσμένες επιλογές έτοιμες, καλέστε τον μετατροπέα. Το παραγόμενο PDF θα αποθηκευτεί στην τοποθεσία που θα ορίσετε, διατηρώντας τις ακριβείς διαστάσεις σελίδας που καθορίσατε.

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

`PdfSaveOptions.setEnableParallelProcessing` είναι μια μέθοδος που ενεργοποιεί την παράλληλη επεξεργασία σελίδων κατά τη μετατροπή PDF.

## Πλήρης Πηγαίος Κώδικας

Το πλήρες, εκτελέσιμο παράδειγμα συνδυάζει τα τρία παραπάνω βήματα σε μία ενιαία κλάση Java. Αντικαταστήστε τις διαδρομές placeholder με τις δικές σας τοποθεσίες αρχείων.

```java
Specifying PDF Save Options for EPUB to PDF
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of the PdfSaveOptions with a custom page-size and a background-color.
            com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
            com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
            com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
            anyPage.setSize(new com.aspose.html.drawing.Size(
                    com.aspose.html.drawing.Length.fromPixels(3000),
                    com.aspose.html.drawing.Length.fromPixels(1000))
            );
            pageSetup.setAnyPage(anyPage);
            options.setPageSetup(pageSetup);
            options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
            // Call the ConvertEPUB method to convert the EPUB to PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```

## Συχνά Προβλήματα και Λύσεις

| Πρόβλημα | Αιτία | Διόρθωση |
|----------|-------|----------|
| **Οι σελίδες PDF είναι κενές** | Το ρεύμα εισόδου κλείνει πριν τη μετατροπή | Διατηρήστε το μπλοκ `try‑with‑resources` ανοιχτό μέχρι μετά το `convertEPUB`. |
| **Λανθασμένες διαστάσεις σελίδας** | Χρήση pixel που δεν αντιστοιχούν στο επιθυμητό μέγεθος εκτύπωσης | Μετατρέψτε τις επιθυμητές ίντσες σε points (`1 inch = 72 points`) και στη συνέχεια σε pixel χρησιμοποιώντας το `Length.fromPixels`. |
| **Απουσία γραμματοσειρών** | Οι γραμματοσειρές δεν είναι ενσωματωμένες στο EPUB | Βεβαιωθείτε ότι οι γραμματοσειρές είναι πακεταρισμένες μέσα στο EPUB ή εγκαταστήστε τις στο σύστημα. |
| **Μείωση απόδοσης σε μεγάλα βιβλία** | Απόδοση κάθε σελίδας διαδοχικά | Ενεργοποιήστε την πολυνηματική απόδοση μέσω `PdfSaveOptions.setEnableParallelProcessing(true)` για ταχύτερη επεξεργασία EPUB με πάνω από 500 σελίδες. |

## Συχνές Ερωτήσεις (FAQs)

**Ε: Είναι το Aspose.HTML for Java δωρεάν βιβλιοθήκη;**  
Α: Το Aspose.HTML for Java είναι εμπορική βιβλιοθήκη, αλλά μπορείτε να αποκτήσετε δωρεάν δοκιμαστική έκδοση από την [ιστοσελίδα](https://releases.aspose.com/).

**Ε: Ποιοι τύποι EPUB υποστηρίζονται για μετατροπή;**  
Α: Το Aspose.HTML for Java υποστηρίζει EPUB 2.0, EPUB 3.0 και EPUB 3.1, διαχειριζόμενο επαναρροή και σταθερής διάταξης βιβλία με πλήρη υποστήριξη CSS.

**Ε: Μπορώ να προσαρμόσω περαιτέρω την έξοδο PDF;**  
Α: Ναι, μπορείτε να προσαρμόσετε την έξοδο PDF ρυθμίζοντας τη διαρρύθμιση σελίδας, το χρώμα φόντου, το επίπεδο συμπίεσης και άλλες ρυθμίσεις στο `PdfSaveOptions`.

**Ε: Υπάρχουν περιορισμοί στην δοκιμαστική έκδοση του Aspose.HTML for Java;**  
Α: Η δοκιμαστική έκδοση μπορεί να προσθέσει υδατογράφημα στις πρώτες σελίδες και περιορίζει το μέγιστο μέγεθος αρχείου στα 10 MB· αγοράστε άδεια για να αφαιρέσετε αυτούς τους περιορισμούς.

**Ε: Πού μπορώ να λάβω υποστήριξη για το Aspose.HTML for Java;**  
Α: Μπορείτε να βρείτε απαντήσεις στις ερωτήσεις σας και να ζητήσετε υποστήριξη στο [φόρουμ Aspose.HTML](https://forum.aspose.com/).

---

**Τελευταία Ενημέρωση:** 2026-05-30  
**Δοκιμάστηκε Με:** Aspose.HTML for Java 24.11 (τελευταία έκδοση τη στιγμή της συγγραφής)  
**Συγγραφέας:** Aspose

## Σχετικά Μαθήματα

- [Ρύθμιση Μεγέθους Σελίδας PDF με Aspose.HTML for Java](/html/java/advanced-usage/adjust-pdf-page-size/)
- [Πώς να Μετατρέψετε EPUB σε PDF με Java – Χρησιμοποιώντας Aspose.HTML](/html/java/conversion-epub-to-image-and-pdf/convert-epub-to-pdf/)
- [Μετατροπή EPUB σε PDF και Εικόνες με Aspose.HTML for Java](/html/java/conversion-epub-to-image-and-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
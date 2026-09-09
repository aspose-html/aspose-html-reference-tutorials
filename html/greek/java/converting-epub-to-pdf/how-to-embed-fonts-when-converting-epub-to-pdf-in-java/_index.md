---
category: general
date: 2026-01-01
description: Πώς να ενσωματώσετε γραμματοσειρές κατά τη μετατροπή EPUB σε PDF σε Java.
  Μάθετε πώς να ορίσετε το μέγεθος σελίδας PDF και να χρησιμοποιήσετε το Aspose HTML
  για ομαλή μετατροπή EPUB σε PDF σε Java.
draft: false
keywords:
- how to embed fonts
- convert epub to pdf
- how to convert epub
- set pdf page size
- epub to pdf java
language: el
og_description: Πώς να ενσωματώσετε γραμματοσειρές κατά τη μετατροπή EPUB σε PDF σε
  Java. Αυτός ο οδηγός σας δείχνει βήμα‑βήμα πώς να ορίσετε το μέγεθος σελίδας PDF
  και να εκτελέσετε μια αξιόπιστη μετατροπή epub σε pdf με Java.
og_title: Πώς να ενσωματώσετε γραμματοσειρές κατά τη μετατροπή EPUB σε PDF με Java
tags:
- Java
- PDF
- EPUB
title: Πώς να ενσωματώσετε γραμματοσειρές κατά τη μετατροπή EPUB σε PDF με Java
url: /el/java/converting-epub-to-pdf/how-to-embed-fonts-when-converting-epub-to-pdf-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Ενσωματώσετε Γραμματοσειρές Κατά τη Μετατροπή EPUB σε PDF με Java

Έχετε αναρωτηθεί **πώς να ενσωματώσετε γραμματοσειρές** ώστε το μετατρεπόμενο PDF να φαίνεται ακριβώς όπως το αρχικό EPUB; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν το πρόβλημα της έλλειψης γραμματοσειρών αμέσως μετά την πρώτη προσπάθεια μετατροπής. Τα καλά νέα είναι ότι με το Aspose.HTML for Java μπορείτε να ελέγξετε την ενσωμάτωση γραμματοσειρών, το μέγεθος σελίδας και ολόκληρη τη διαδικασία μετατροπής με λίγες μόνο γραμμές κώδικα.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα τη διαδικασία **convert epub to pdf** χρησιμοποιώντας Java, θα σας δείξουμε πώς να **set pdf page size**, και θα εξηγήσουμε γιατί η ενσωμάτωση γραμματοσειρών είναι σημαντική για την πιστότητα μεταξύ πλατφορμών. Στο τέλος θα έχετε ένα έτοιμο πρόγραμμα που μετατρέπει οποιοδήποτε αρχείο EPUB σε ένα τέλεια αποδομένο PDF, με ενσωματωμένες γραμματοσειρές και το μέγεθος σελίδας που επιλέξατε.

> **Prerequisites**  
> * Java 17 ή νεότερη (το API λειτουργεί και με παλαιότερες εκδόσεις, αλλά η 17 είναι η ιδανική).  
> * Βιβλιοθήκη Aspose.HTML for Java – μπορείτε να την κατεβάσετε από το Maven Central.  
> * Ένα δείγμα αρχείου EPUB για δοκιμή.  

Αν είστε άνετοι με Maven ή Gradle, είστε έτοιμοι. Διαφορετικά, απλώς κατεβάστε το JAR και προσθέστε το στο classpath—δεν υπάρχει πρόβλημα.

---

## Πώς να Ενσωματώσετε Γραμματοσειρές στο PDF Output

Η ενσωμάτωση γραμματοσειρών εξασφαλίζει ότι το PDF εμφανίζει την ίδια τυπογραφία σε οποιαδήποτε συσκευή, ακόμη και αν ο αναγνώστης δεν έχει εγκατεστημένη την αρχική γραμματοσειρά. Το Aspose.HTML σας παρέχει ένα μόνο κουμπί για να το ενεργοποιήσετε.

```java
// Configure PDF save options
PdfSaveOptions pdfOptions = new PdfSaveOptions();
pdfOptions.setEmbedFonts(true);               // <-- This line embeds all used fonts
```

Γιατί είναι σημαντικό; Φανταστείτε ότι στέλνετε ένα PDF σε πελάτη που έχει μόνο τις προεπιλεγμένες γραμματοσειρές του συστήματος. Χωρίς ενσωμάτωση, οι τίτλοι μπορεί να επιστρέψουν σε Arial ή Times New Roman, σπάζοντας το layout σας. Με την ενσωμάτωση, κλειδώνετε το οπτικό σχέδιο, καθιστώντας το PDF πραγματικά φορητό.

> **Pro tip:** Αν γνωρίζετε τις ακριβείς γραμματοσειρές που χρησιμοποιεί το EPUB σας, μπορείτε επίσης να παρέχετε έναν προσαρμοσμένο φάκελο γραμματοσειρών μέσω `pdfOptions.setFontsFolder("path/to/fonts")`. Αυτό επιταχύνει τη μετατροπή και αποφεύγει περιττή ενσωμάτωση γραμματοσειρών.

---

## Convert EPUB to PDF in Java – Full Workflow

Παρακάτω είναι ο ελάχιστος, αλλά πλήρης, κώδικας που χρειάζεστε. Καλύπτει τρία βασικά βήματα: εντοπισμός του πηγαίου EPUB, ρύθμιση των PDF options (συμπεριλαμβανομένου του μεγέθους σελίδας) και κλήση της μετατροπής.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfSaveOptions;

public class EpubToPdfDemo {

    public static void main(String[] args) throws Exception {
        // Step 1: Point to your source EPUB file
        String epubPath = "YOUR_DIRECTORY/input.epub";

        // Step 2: Set up PDF save options (embed fonts + page size)
        PdfSaveOptions pdfOptions = new PdfSaveOptions();
        pdfOptions.setEmbedFonts(true);                         // Embed fonts for accurate rendering
        pdfOptions.setPageSize(PdfSaveOptions.PageSize.LETTER); // Set PDF page size to Letter (8.5"x11")

        // Step 3: Perform the conversion
        String outputPdf = "YOUR_DIRECTORY/output.pdf";
        Converter.convert(epubPath, outputPdf, pdfOptions);

        System.out.println("Conversion complete! PDF saved to: " + outputPdf);
    }
}
```

### Τι συμβαίνει στο παρασκήνιο;

1. **Source EPUB** – Η μεταβλητή `epubPath` λέει στο Aspose από πού να διαβάσει το EPUB container.  
2. **PDF Options** – Το `PdfSaveOptions` σας επιτρέπει να ενεργοποιήσετε την ενσωμάτωση γραμματοσειρών (`setEmbedFonts`) και να ορίσετε τις διαστάσεις της σελίδας (`setPageSize`). Το enum `PageSize.LETTER` είναι χρήσιμο για US‑letter· μπορείτε επίσης να επιλέξετε `A4`, `A5`, κ.λπ.  
3. **Conversion Call** – Η `Converter.convert` κάνει το βαριά δουλειά. Αναλύει το EPUB, αποδίδει κάθε σελίδα XHTML σε σελίδα PDF, εφαρμόζει τις επιλογές και γράφει το αποτέλεσμα.

Η μέθοδος ρίχνει μια γενική `Exception` για συντομία· σε παραγωγικό περιβάλλον θα πιάνατε συγκεκριμένες υποκλάσεις (π.χ., `IOException`, `FileNotFoundException`) και θα τις διαχειριζόσασταν με ευγένεια.

---

## Set PDF Page Size for the Result

Η επιλογή του σωστού μεγέθους σελίδας είναι περισσότερο από αισθητική· επηρεάζει την αρίθμηση σελίδων, την κλιμάκωση εικόνων και το layout εκτύπωσης. Το Aspose.HTML παρέχει ένα βολικό enum, αλλά μπορείτε επίσης να περάσετε προσαρμοσμένο μέγεθος αν τα προεπιλεγμένα δεν ταιριάζουν.

```java
// Example: Custom size – 6" x 9"
pdfOptions.setPageSize(new PdfSaveOptions.PageSize(6.0, 9.0));
```

Γιατί μπορεί να χρειαστείτε προσαρμοσμένο μέγεθος; Ίσως δημιουργείτε pocket‑sized e‑books ή ένα εκτυπώσιμο φυλλάδιο με συγκεκριμένο trim size. Το API δέχεται ίντσες (ή μπορείτε να χρησιμοποιήσετε χιλιοστά μετατρέποντας τα μόνοι σας), δίνοντάς σας πλήρη έλεγχο.

---

## Complete Working Example (Including Maven Dependency)

Αν χρησιμοποιείτε Maven, προσθέστε την ακόλουθη εξάρτηση στο `pom.xml`. Αυτό εξασφαλίζει ότι οι κλάσεις `Converter` και `PdfSaveOptions` είναι στο classpath.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

**Full source file (`EpubToPdfDemo.java`)**

```java
package com.example.epubtopdf;

import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfSaveOptions;

/**
 * Demonstrates how to embed fonts and set PDF page size while converting an EPUB file to PDF.
 * Run this class from your IDE or via `java -cp <classpath> com.example.epubtopdf.EpubToPdfDemo`.
 */
public class EpubToPdfDemo {

    public static void main(String[] args) {
        try {
            // -----------------------------------------------------------------
            // 1️⃣ Locate the EPUB file
            // -----------------------------------------------------------------
            String epubPath = "C:/Docs/input.epub";

            // -----------------------------------------------------------------
            // 2️⃣ Configure PDF options – embed fonts & choose page size
            // -----------------------------------------------------------------
            PdfSaveOptions pdfOptions = new PdfSaveOptions();
            pdfOptions.setEmbedFonts(true);                         // Embed every font used in the EPUB
            pdfOptions.setPageSize(PdfSaveOptions.PageSize.LETTER); // Letter size (8.5"x11")

            // -----------------------------------------------------------------
            // 3️⃣ Convert and save the PDF
            // -----------------------------------------------------------------
            String outputPdf = "C:/Docs/output.pdf";
            Converter.convert(epubPath, outputPdf, pdfOptions);

            System.out.println("✅ Success! PDF created at: " + outputPdf);
        } catch (Exception e) {
            System.err.println("❌ Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Expected output

Η εκτέλεση του προγράμματος εκτυπώνει μια γραμμή επιβεβαίωσης:

```
✅ Success! PDF created at: C:/Docs/output.pdf
```

Ανοίξτε το παραγόμενο PDF σε οποιονδήποτε προβολέα (Adobe Reader, Chrome, κ.λπ.) και θα δείτε:

* Όλα τα κειμενικά στοιχεία διατηρούν το αρχικό στυλ γραμματοσειράς.  
* Οι διαστάσεις σελίδας ταιριάζουν με το επιλεγμένο μέγεθος **Letter**.  
* Εικόνες, πίνακες και υπερσυνδέσεις από το EPUB διατηρούνται.

Αν ελέγξετε τις ιδιότητες του PDF (File → Properties → Fonts), θα παρατηρήσετε ότι κάθε γραμματοσειρά εμφανίζεται ως **Embedded Subset**, επιβεβαιώνοντας ότι η κλήση `setEmbedFonts(true)` έκανε τη δουλειά της.

---

## Frequently Asked Questions & Edge Cases

| Question | Answer |
|----------|--------|
| **What if my EPUB uses a custom font not installed on the server?** | Τοποθετήστε τα αρχεία `.ttf` ή `.otf` σε έναν φάκελο και κατευθύνετε το Aspose σε αυτόν με `pdfOptions.setFontsFolder("path/to/custom/fonts")`. Ο μετατροπέας θα τα φορτώσει και θα τα ενσωματώσει αυτόματα. |
| **Can I convert multiple EPUBs in one run?** | Απολύτως. Τυλίξτε τη λογική μετατροπής σε βρόχο, αλλάξτε το `epubPath` και το `outputPdf` για κάθε αρχείο. Το Aspose είναι thread‑safe, οπότε μπορείτε ακόμη και να παραλληλοποιήσετε τη δουλειά με ένα `ExecutorService`. |
| **Is there a size limit for the input EPUB?** | Δεν υπάρχει σκληρό όριο, αλλά πολύ μεγάλα EPUB (εκατοντάδες MB) θα καταναλώσουν περισσότερη μνήμη. Σκεφτείτε να αυξήσετε το heap της JVM (`-Xmx2g` ή περισσότερο) για τεράστια βιβλία. |
| **How do I disable font embedding for a smaller PDF?** | Ορίστε `pdfOptions.setEmbedFonts(false)`. Το παραγόμενο PDF θα εξαρτάται από τις εγκατεστημένες γραμματοσειρές του προβολέα, μειώνοντας το μέγεθος του αρχείου αλλά ενδεχομένως αλλάζοντας την εμφάνιση. |
| **Do I need a license for Aspose.HTML?** | Μια δωρεάν evaluation license λειτουργεί για δοκιμές, αλλά προσθέτει υδατογράφημα. Για παραγωγή, αγοράστε άδεια και καλέστε `License license = new License(); license.setLicense("path/to/license.xml");` πριν από τη μετατροπή. |

---

## Conclusion

Τώρα ξέρετε **πώς να ενσωματώσετε γραμματοσειρές** όταν **convert EPUB to PDF** με Java, πώς να **set PDF page size**, και πώς να συνδυάσετε όλα τα παραπάνω με το Aspose.HTML. Το πλήρες, εκτελέσιμο παράδειγμα παραπάνω θα πρέπει να λειτουργεί αμέσως—απλώς αντικαταστήστε τις διαδρομές placeholder με τα δικά σας αρχεία και είστε έτοιμοι.

Τι θα κάνετε μετά; Δοκιμάστε άλλα φορμάτ σελίδας όπως **A4** ή ένα προσαρμοσμένο 6×9, εξερευνήστε τις ιδιότητες `PdfSaveOptions` για συμπίεση εικόνων, ή ακόμη προσθέστε μια σελίδα εξώφυλλου προγραμματιστικά. Το ίδιο μοτίβο λειτουργεί και για άλλες πηγές (HTML, Markdown) επειδή το Aspose.HTML τα αντιμετωπίζει ομοιόμορφα.

Καλή προγραμματιστική δουλειά, και εύχομαι τα PDFs σας να φαίνονται πάντα ακριβώς όπως τα φανταστήκατε! 

![Πώς να ενσωματώσετε γραμματοσειρές στη μετατροπή PDF](https://example.com/images/embed-fonts.png "Πώς να ενσωματώσετε γραμματοσειρές στη μετατροπή PDF")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
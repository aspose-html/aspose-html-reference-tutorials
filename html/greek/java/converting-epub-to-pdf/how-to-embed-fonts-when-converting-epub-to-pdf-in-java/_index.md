---
category: general
date: 2026-04-12
description: Μάθετε πώς να ορίζετε το μέγεθος σελίδας PDF και να ενσωματώνετε γραμματοσειρές
  όταν μετατρέπετε EPUB σε PDF σε Java χρησιμοποιώντας το Aspose.HTML. Αυτός ο οδηγός
  σας καθοδηγεί μέσα από τη πλήρη διαδικασία μετατροπής Java EPUB σε PDF.
draft: false
keywords:
- set pdf page size
- embed fonts pdf
- convert epub to pdf
- java epub to pdf
- custom pdf page size
og_description: Μάθετε πώς να ορίζετε το μέγεθος σελίδας PDF και να ενσωματώνετε γραμματοσειρές
  κατά τη μετατροπή EPUB σε PDF σε Java με το Aspose.HTML.
og_title: Ορισμός μεγέθους σελίδας PDF & ενσωμάτωση γραμματοσειρών για EPUB σε PDF
  σε Java
tags:
- Java
- PDF
- EPUB
title: Ορισμός μεγέθους σελίδας PDF & ενσωμάτωση γραμματοσειρών για EPUB σε PDF σε
  Java
url: /el/java/converting-epub-to-pdf/how-to-embed-fonts-when-converting-epub-to-pdf-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ορισμός μεγέθους σελίδας PDF & Ενσωμάτωση γραμματοσειρών για EPUB σε PDF σε Java

Αν χρειάζεστε να **set PDF page size** ενώ **convert EPUB to PDF** και θέλετε να εγγυηθείτε ότι το παραγόμενο έγγραφο φαίνεται ακριβώς όπως το αρχικό, βρίσκεστε στο σωστό μέρος. Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, έτοιμο για παραγωγή παράδειγμα Java που δείχνει πώς να **embed fonts pdf**, να επιλέξετε ένα **custom pdf page size**, και να εκτελέσετε τη μετατροπή με το Aspose.HTML. Στο τέλος θα έχετε ένα πρόγραμμα έτοιμο προς εκτέλεση που παράγει ένα πιστό PDF κάθε φορά.

## Γρήγορες Απαντήσεις
- **What is the main goal?** Ορίστε το μέγεθος σελίδας PDF και ενσωματώστε γραμματοσειρές κατά τη μετατροπή EPUB σε PDF σε Java.  
- **Which library should I use?** Aspose.HTML for Java (διαθέσιμο δωρεάν δοκιμαστικό).  
- **Do I need a license for production?** Ναι – μια άδεια αφαιρεί το υδατογράφημα αξιολόγησης.  
- **Can I use a custom page size?** Απόλυτα – μπορείτε να περάσετε ακριβείς διαστάσεις ή να χρησιμοποιήσετε ενσωματωμένα enums όπως A4, LETTER, κλπ.  
- **What Java version is required?** Συνιστάται Java 17 ή νεότερη.

### Προαπαιτούμενα
- Εγκατεστημένο Java 17+.  
- Προστέθηκε το Aspose.HTML for Java στο έργο σας (Maven, Gradle ή χειροκίνητο JAR).  
- Ένα αρχείο EPUB που θέλετε να μετατρέψετε.

> Αν προτιμάτε Gradle, απλώς αντικαταστήστε το απόσπασμα Maven με το ισοδύναμο Gradle coordinates.

---

## Γιατί να ενσωματώσετε γραμματοσειρές σε PDF;

Η ενσωμάτωση γραμματοσειρών κλειδώνει το οπτικό σχέδιο του πηγαίου EPUB, έτσι ώστε το PDF να αποδίδει σωστά σε οποιαδήποτε συσκευή—ακόμη και αν ο προβολέας δεν έχει εγκατεστημένες τις αρχικές γραμματοσειρές. Χωρίς ενσωμάτωση, οι επικεφαλίδες μπορεί να επιστρέψουν σε προεπιλεγμένες γραμματοσειρές όπως Arial, διασπώντας τη διάταξη που δημιουργήσατε με κόπο.

**Pro tip:** Αν γνωρίζετε τις ακριβείς γραμματοσειρές που χρησιμοποιούνται στο EPUB, υποδείξτε στο Aspose έναν φάκελο που περιέχει αυτά τα `.ttf` ή `.otf` αρχεία με `pdfOptions.setFontsFolder("path/to/fonts")`. Αυτό επιταχύνει τη μετατροπή και μειώνει το τελικό μέγεθος αρχείου.

```java
// Configure PDF save options
PdfSaveOptions pdfOptions = new PdfSaveOptions();
pdfOptions.setEmbedFonts(true);               // <-- This line embeds all used fonts
```

---

## Πώς να μετατρέψετε EPUB σε PDF σε Java – Πλήρης Ροή Εργασίας

Παρακάτω είναι ο ελάχιστος, αλλά πλήρης, κώδικας που χρειάζεστε. Καλύπτει τρία βασικά βήματα: εντοπισμός του πηγαίου EPUB, ρύθμιση επιλογών PDF (συμπεριλαμβανομένου του **set PDF page size**), και κλήση της μετατροπής.

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

1. **Source EPUB** – Το `epubPath` λέει στο Aspose από πού να διαβάσει το δοχείο EPUB.  
2. **PDF Options** – Το `PdfSaveOptions` σας επιτρέπει να ενεργοποιήσετε/απενεργοποιήσετε την ενσωμάτωση γραμματοσειρών (`setEmbedFonts`) και να ορίσετε τις διαστάσεις της σελίδας (`setPageSize`). Το enum `PageSize.LETTER` είναι χρήσιμο για US‑letter· μπορείτε επίσης να επιλέξετε `A4`, `A5`, κλπ.  
3. **Conversion Call** – Το `Converter.convert` αναλύει το EPUB, αποδίδει κάθε σελίδα XHTML σε σελίδα PDF, εφαρμόζει τις επιλογές και γράφει το αποτέλεσμα.

Η μέθοδος ρίχνει μια γενική `Exception` για συντομία· στην παραγωγή θα πιάνατε συγκεκριμένες υποκλάσεις (π.χ., `IOException`, `FileNotFoundException`) και θα τις διαχειριζόσασταν ομαλά.

---

## Πώς να ορίσετε το μέγεθος σελίδας PDF για το αποτέλεσμα

Η επιλογή του σωστού μεγέθους σελίδας επηρεάζει την αρίθμηση, την κλιμάκωση εικόνων και τη διάταξη εκτύπωσης. Το Aspose.HTML παρέχει ένα βολικό enum, αλλά μπορείτε επίσης να περάσετε προσαρμοσμένο μέγεθος εάν τα προεπιλεγμένα δεν ταιριάζουν στις ανάγκες σας.

```java
// Example: Custom size – 6" x 9"
pdfOptions.setPageSize(new PdfSaveOptions.PageSize(6.0, 9.0));
```

**When would you need a custom size?** Μπορεί να δημιουργείτε e‑books μικρού μεγέθους, ένα εκτυπώσιμο φυλλάδιο ή μια αναφορά που ακολουθεί συγκεκριμένο μέγεθος περικοπής. Το API δέχεται ίντσες (ή μπορείτε να μετατρέψετε από χιλιοστά), δίνοντάς σας πλήρη έλεγχο.

## Πλήρες Παράδειγμα Εργασίας (Συμπεριλαμβανομένης της Εξάρτησης Maven)

Αν χρησιμοποιείτε Maven, προσθέστε την ακόλουθη εξάρτηση στο `pom.xml`. Αυτό εξασφαλίζει ότι οι κλάσεις `Converter` και `PdfSaveOptions` είναι στο classpath.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

**Πλήρες αρχείο πηγαίου κώδικα (`EpubToPdfDemo.java`)**

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

### Αναμενόμενο αποτέλεσμα

Η εκτέλεση του προγράμματος εκτυπώνει μια γραμμή επιβεβαίωσης:

```
✅ Success! PDF created at: C:/Docs/output.pdf
```

Ανοίξτε το παραγόμενο PDF σε οποιονδήποτε προβολέα (Adobe Reader, Chrome, κλπ.) και θα δείτε:

* Όλα τα κειμενικά στοιχεία διατηρούν την αρχική μορφοποίηση γραμματοσειράς.  
* Οι διαστάσεις της σελίδας ταιριάζουν με το επιλεγμένο μέγεθος **Letter** (ή οποιοδήποτε προσαρμοσμένο μέγεθος έχετε ορίσει).  
* Εικόνες, πίνακες και υπερσυνδέσεις από το EPUB διατηρούνται.

Αν εξετάσετε τις ιδιότητες του PDF (File → Properties → Fonts), θα παρατηρήσετε ότι κάθε γραμματοσειρά εμφανίζεται ως **Embedded Subset**, επιβεβαιώνοντας ότι η κλήση `setEmbedFonts(true)` έκανε τη δουλειά της.

---

## Συχνές Ερωτήσεις

**Q: Τι γίνεται αν το EPUB μου χρησιμοποιεί προσαρμοσμένη γραμματοσειρά που δεν είναι εγκατεστημένη στον διακομιστή;**  
A: Τοποθετήστε τα αρχεία `.ttf` ή `.otf` σε έναν φάκελο και υποδείξτε το στο Aspose με `pdfOptions.setFontsFolder("path/to/custom/fonts")`. Ο μετατροπέας θα φορτώσει και θα ενσωματώσει αυτές τις γραμματοσειρές αυτόματα.

**Q: Μπορώ να μετατρέψω πολλαπλά αρχεία EPUB σε μία εκτέλεση;**  
A: Ναι. Τυλίξτε τη λογική μετατροπής σε βρόχο, αλλάξτε `epubPath` και `outputPdf` για κάθε αρχείο, και προαιρετικά εκτελέστε τον βρόχο παράλληλα χρησιμοποιώντας `ExecutorService` επειδή το Aspose είναι thread‑safe.

**Q: Υπάρχει όριο μεγέθους για το εισερχόμενο EPUB;**  
A: Δεν υπάρχει σκληρό όριο, αλλά πολύ μεγάλα EPUB (εκατοντάδες MB) μπορούν να καταναλώσουν σημαντική μνήμη. Αυξήστε τη μνήμη heap της JVM (`-Xmx2g` ή περισσότερο) για τεράστια βιβλία.

**Q: Πώς απενεργοποιώ την ενσωμάτωση γραμματοσειρών για να μειώσω το μέγεθος του PDF;**  
A: Καλέστε `pdfOptions.setEmbedFonts(false)`. Το PDF θα βασίζεται στις γραμματοσειρές που είναι εγκατεστημένες στον προβολέα, μειώνοντας το μέγεθος του αρχείου αλλά ενδέχεται να αλλάξει η εμφάνιση.

**Q: Χρειάζομαι άδεια για το Aspose.HTML;**  
A: Μια δωρεάν άδεια αξιολόγησης λειτουργεί για δοκιμές αλλά προσθέτει υδατογράφημα. Για παραγωγική χρήση, αγοράστε άδεια και φορτώστε την με `License license = new License(); license.setLicense("path/to/license.xml");`.

## Συμπέρασμα

Τώρα ξέρετε **how to set PDF page size** και **embed fonts pdf** όταν **convert EPUB to PDF** σε Java χρησιμοποιώντας το Aspose.HTML. Το πλήρες, εκτελέσιμο παράδειγμα παραπάνω θα πρέπει να λειτουργεί αμέσως—απλώς αντικαταστήστε τις διαδρομές placeholder με τα δικά σας αρχεία.

Επόμενα βήματα; Δοκιμάστε διαφορετικές μορφές σελίδας όπως **A4** ή ένα προσαρμοσμένο μέγεθος 6×9, εξερευνήστε άλλες `PdfSaveOptions` (συμπίεση εικόνας, συμμόρφωση PDF/A), ή προσθέστε μια σελίδα εξώφυλλου προγραμματιστικά. Το ίδιο μοτίβο λειτουργεί για άλλες πηγές μορφές (HTML, Markdown) επειδή το Aspose.HTML τις αντιμετωπίζει ομοιόμορφα.

Καλό κώδικα, και εύχομαι τα PDF σας να φαίνονται πάντα ακριβώς όπως επιθυμείτε! 

![Πώς να ενσωματώσετε γραμματοσειρές σε μετατροπή PDF](https://example.com/images/embed-fonts.png "Πώς να ενσωματώσετε γραμματοσειρές σε μετατροπή PDF")

---

**Τελευταία ενημέρωση:** 2026-04-12  
**Δοκιμή με:** Aspose.HTML for Java 23.10  
**Συγγραφέας:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
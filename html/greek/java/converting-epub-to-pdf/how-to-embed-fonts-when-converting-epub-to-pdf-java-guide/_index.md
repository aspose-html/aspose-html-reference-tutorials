---
category: general
date: 2026-01-03
description: Πώς να ενσωματώσετε γραμματοσειρές κατά τη μετατροπή EPUB σε PDF χρησιμοποιώντας
  το Aspose HTML για Java. Μάθετε πώς να ορίζετε τα περιθώρια PDF, να μετατρέπετε
  το ebook σε PDF και να κατακτήσετε τη μετατροπή ebook.
draft: false
keywords:
- how to embed fonts
- convert epub to pdf
- how to convert epub
- convert ebook to pdf
- set pdf margins
language: el
og_description: Πώς να ενσωματώσετε γραμματοσειρές κατά τη μετατροπή EPUB σε PDF χρησιμοποιώντας
  το Aspose HTML για Java. Ακολουθήστε το βήμα‑βήμα μας οδηγό για να ορίσετε τα περιθώρια
  PDF και να μετατρέψετε το ebook σε PDF.
og_title: Πώς να ενσωματώσετε γραμματοσειρές κατά τη μετατροπή EPUB σε PDF – Οδηγός
  Java
tags:
- Java
- Aspose
- PDF
- EPUB
title: Πώς να ενσωματώσετε γραμματοσειρές κατά τη μετατροπή EPUB σε PDF – Οδηγός Java
url: /el/java/converting-epub-to-pdf/how-to-embed-fonts-when-converting-epub-to-pdf-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ενσωματώσετε γραμματοσειρές κατά τη μετατροπή EPUB σε PDF – Οδηγός Java

Έχετε αναρωτηθεί ποτέ **πώς να ενσωματώσετε γραμματοσειρές** όταν χρειάζεται να μετατρέψετε ένα αρχείο EPUB σε ένα επαγγελματικό PDF; Δεν είστε μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν πρόβλημα όταν το παραγόμενο PDF φαίνεται σαν ένα σύνολο προεπιλεγμένων γραμματοσειρών του συστήματος αντί για την όμορφη τυπογραφία του αρχικού e‑book.  

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει **πώς να ενσωματώσετε γραμματοσειρές** χρησιμοποιώντας το Aspose.HTML for Java, καλύπτοντας επίσης **convert epub to pdf**, **set pdf margins**, και άλλες χρήσιμες συμβουλές για έργα **convert ebook to pdf**.

## Τι θα μάθετε

- Τα ακριβή βήματα για **πώς να ενσωματώσετε γραμματοσειρές** στη διαδικασία μετατροπής.  
- Πώς να **convert epub to pdf** με προσαρμοσμένες ρυθμίσεις περιθωρίων.  
- Γιατί η ρύθμιση των περιθωρίων PDF (`set pdf margins`) είναι σημαντική για έγγραφα έτοιμα για εκτύπωση.  
- Κοινά προβλήματα όταν **how to convert epub** αρχεία και πώς να τα αποφύγετε.  

### Προαπαιτούμενα

- Java 17 (ή οποιαδήποτε πρόσφατη έκδοση LTS).  
- Βιβλιοθήκη Aspose.HTML for Java (έκδοση 23.9 ή νεότερη).  
- Ένα αρχείο EPUB που θέλετε να δοκιμάσετε.  
- Ένα βασικό IDE ή επεξεργαστή κειμένου—IntelliJ IDEA, Eclipse, VS Code, κ.λπ.

Δεν απαιτούνται άλλα εργαλεία τρίτων· όλα εκτελούνται σε καθαρή Java.

---

## Βήμα 1: Προσθέστε το Aspose.HTML στο έργο σας

Πρώτα, βεβαιωθείτε ότι το JAR του Aspose.HTML βρίσκεται στο classpath σας. Αν χρησιμοποιείτε Maven, προσθέστε την ακόλουθη εξάρτηση στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

> **Συμβουλή:** Αν προτιμάτε Gradle, το ισοδύναμο είναι  
> `implementation 'com.aspose:aspose-html:23.9'`.

Η διαθεσιμότητα της βιβλιοθήκης μας επιτρέπει να δημιουργήσουμε αντικείμενα `HTMLDocument`, `PdfSaveOptions` και την στατική κλάση `Converter`.

## Βήμα 2: Φορτώστε το EPUB που θέλετε να μετατρέψετε

```java
// Load the source EPUB file
HTMLDocument epubDocument = new HTMLDocument("YOUR_DIRECTORY/input.epub");
```

Ο κατασκευαστής `HTMLDocument` αναλύει αυτόματα το πακέτο EPUB, εξάγει το περιεχόμενο HTML, CSS και ενσωματωμένους πόρους. Στις περισσότερες περιπτώσεις δεν χρειάζεται να επεμβείτε στα εσωτερικά—απλώς δώστε τη διαδρομή του αρχείου.

## Βήμα 3: Διαμορφώστε τις επιλογές μετατροπής PDF (συμπεριλαμβανομένης της ενσωμάτωσης γραμματοσειρών)

Τώρα έρχεται η ουσία του **πώς να ενσωματώσετε γραμματοσειρές**. Από προεπιλογή, το Aspose.HTML ενσωματώνει τις γραμματοσειρές που βρίσκει, αλλά μπορείτε να το επιβάλετε και να ρυθμίσετε τα περιθώρια ταυτόχρονα:

```java
PdfSaveOptions pdfOptions = new PdfSaveOptions();

// 1️⃣ Ensure fonts are embedded so the PDF looks identical on any machine
pdfOptions.setEmbedFonts(true);

// 2️⃣ Set uniform margins – this is where we apply the “set pdf margins” requirement
pdfOptions.setPageMargins(20, 20, 20, 20); // left, top, right, bottom (points)

// Optional: you can also control PDF version, compliance, etc.
pdfOptions.setCompliance(PdfSaveOptions.Compliance.PDF_A_1B);
```

Γιατί να ενσωματώσετε γραμματοσειρές; Αν ο αναγνώστης δεν έχει εγκατεστημένες τις αρχικές γραμματοσειρές, το PDF θα επιστρέψει σε μια γενική γραμματοσειρά, διαταράσσοντας τη διάταξη. Η ενεργοποίηση του `setEmbedFonts(true)` εγγυάται την ακριβή εμφάνιση που σχεδιάσατε.

## Βήμα 4: Εκτελέστε τη μετατροπή

```java
// Convert and save the PDF
Converter.convert(epubDocument, "YOUR_DIRECTORY/output.pdf", pdfOptions);
```

Αυτή η μοναδική γραμμή κάνει τη βαριά δουλειά: αναλύει το EPUB, αποδίδει κάθε σελίδα, εφαρμόζει τις ρυθμίσεις περιθωρίων και γράφει ένα PDF με όλες τις γραμματοσειρές ενσωματωμένες.

## Βήμα 5: Επαληθεύστε το αποτέλεσμα

Αφού ολοκληρωθεί το πρόγραμμα, ανοίξτε το `output.pdf` σε οποιονδήποτε προβολέα PDF. Θα πρέπει να δείτε:

- Όλες οι αρχικές γραμματοσειρές ανέπαφες (χωρίς αντικατάσταση).  
- Συνεπή περιθώρια 20 σημείων γύρω από το περιεχόμενο.  
- Αλλαγές σελίδας που σέβονται τη ροή του αρχικού EPUB.

Αν υποπτεύεστε ότι μια γραμματοσειρά δεν ενσωματώθηκε, οι περισσότεροι προβολείς σας επιτρέπουν να δείτε τις ιδιότητες του εγγράφου → Fonts. Αναζητήστε τη σημαία “Embedded” δίπλα σε κάθε γραμματοσειρά.

---

## Συχνές ερωτήσεις & ειδικές περιπτώσεις

### Τι γίνεται αν το EPUB χρησιμοποιεί μια γραμματοσειρά που δεν έχει άδεια ενσωμάτωσης;

Το Aspose.HTML σέβεται τις άδειες γραμματοσειρών. Αν μια γραμματοσειρά είναι σημειωμένη ως “non‑embeddable”, η βιβλιοθήκη θα επιστρέψει σε μια παρόμοια γραμματοσειρά του συστήματος και θα καταγράψει μια προειδοποίηση. Σε τέτοιες περιπτώσεις, εξετάστε:

- Αντικατάσταση της γραμματοσειράς με μια ανοιχτού κώδικα εναλλακτική πριν τη μετατροπή.  
- Χρήση του `pdfOptions.setFallbackFont("Arial")` για να ορίσετε μια ασφαλή προεπιλογή.

### Μπορώ να ενσωματώσω μόνο ένα υποσύνολο χαρακτήρων για να μειώσω το μέγεθος του αρχείου;

Ναι. Χρησιμοποιήστε το `pdfOptions.setSubsetFonts(true)` (ενεργοποιημένο από προεπιλογή). Αυτό λέει στον μετατροπέα να ενσωματώνει μόνο τα γλύφους που χρησιμοποιούνται πραγματικά στο έγγραφο, κάτι που μπορεί να μειώσει δραματικά το PDF για μεγάλες γραμματοσειρές.

### Πώς διαχειρίζομαι γλώσσες RTL (από δεξιά προς αριστερά);

Το Aspose.HTML υποστηρίζει πλήρως τα σενάρια RTL. Απλώς βεβαιωθείτε ότι το CSS του αρχικού EPUB περιλαμβάνει `direction: rtl;`. Η διαδικασία μετατροπής θα διατηρήσει τη διάταξη, και οι ενσωματωμένες γραμματοσειρές θα περιλαμβάνουν τα απαραίτητα γλύφους.

### Τι γίνεται αν χρειάζομαι διαφορετικά περιθώρια ανά σελίδα;

`PdfSaveOptions.setPageMargins` εφαρμόζει ένα ομοιόμορφο περιθώριο σε κάθε σελίδα. Για έλεγχο ανά σελίδα, μπορείτε να δημιουργήσετε ένα αντικείμενο `PdfPage` για κάθε σελίδα μετά τη μετατροπή και να προσαρμόσετε το `MediaBox`. Αυτό είναι πιο προχωρημένο σενάριο, αλλά τα βασικά που καλύπτονται εδώ λειτουργούν για τη μεγάλη πλειονότητα των ροών εργασίας ebook‑to‑PDF.

---

## Πλήρης κώδικας (έτοιμος για εκτέλεση)

Αποθηκεύστε το παρακάτω ως `ConvertEpubToPdf.java` και αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή φακέλου όπου βρίσκεται το EPUB σας.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfSaveOptions;

/**
 * Demonstrates how to embed fonts while converting an EPUB file to PDF using Aspose.HTML for Java.
 * The example also shows how to set PDF margins.
 */
public class ConvertEpubToPdf {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the EPUB document you want to convert
        HTMLDocument epubDocument = new HTMLDocument("YOUR_DIRECTORY/input.epub");

        // Step 2: Configure PDF conversion options
        PdfSaveOptions pdfOptions = new PdfSaveOptions();

        // Ensure all fonts from the EPUB are embedded in the resulting PDF
        pdfOptions.setEmbedFonts(true);                     // <‑‑ how to embed fonts
        // Set uniform margins (left, top, right, bottom) – 20 points ≈ 0.28 inch
        pdfOptions.setPageMargins(20, 20, 20, 20);           // <‑‑ set pdf margins
        // Optional: enforce PDF/A‑1b compliance for archival purposes
        pdfOptions.setCompliance(PdfSaveOptions.Compliance.PDF_A_1B);

        // Step 3: Convert the EPUB to PDF and save the result
        Converter.convert(epubDocument, "YOUR_DIRECTORY/output.pdf", pdfOptions);

        System.out.println("Conversion complete! PDF saved to YOUR_DIRECTORY/output.pdf");
    }
}
```

Η εκτέλεση του προγράμματος εκτυπώνει μια γραμμή επιβεβαίωσης και παράγει το `output.pdf` με όλες τις γραμματοσειρές ενσωματωμένες και τα περιθώρια ορισμένα ακριβώς όπως καθορίζονται.

---

## Οπτική σύνοψη

![Διάγραμμα που απεικονίζει την ενσωμάτωση γραμματοσειρών κατά τη μετατροπή EPUB σε PDF conversion](https://example.com/diagram-embed-fonts.png "Πώς να ενσωματώσετε γραμματοσειρές")

*Η παραπάνω εικόνα δείχνει τη ροή: EPUB → HTMLDocument → PdfSaveOptions (ενσωμάτωση γραμματοσειρών + περιθώρια) → Converter → PDF.*

---

## Συμπέρασμα

Καλύψαμε **πώς να ενσωματώσετε γραμματοσειρές** όταν **convert epub to pdf** χρησιμοποιώντας το Aspose.HTML for Java, ενώ επίσης δείξαμε πώς να **set pdf margins** και να αντιμετωπίσουμε κοινές ειδικές περιπτώσεις. Ακολουθώντας τα πέντε παραπάνω βήματα, θα αποκτήσετε ένα πιστό, έτοιμο για εκτύπωση PDF που φαίνεται ακριβώς όπως το αρχικό e‑book, ανεξάρτητα από το πού ανοίγεται.

Στη συνέχεια, ίσως θέλετε να εξερευνήσετε:

- Προσθήκη σελίδας εξώφυλλου ή υδατογραφήματος (ακόμη χρησιμοποιώντας το `PdfSaveOptions`).  
- Επεξεργασία σε παρτίδες ολόκληρου φακέλου EPUB (βρόχος πάνω σε αρχεία, ίδιος κώδικας).  
- Πειραματισμός με διαφορετικές τιμές περιθωρίων για να ταιριάζουν σε συγκεκριμένα μεγέθη σελίδας (`set pdf margins` ανά στόχο εκτυπωτή).

Μη διστάσετε να τροποποιήσετε τον κώδικα, να δοκιμάσετε διαφορετικές γραμματοσειρές ή να συνδυάσετε αυτό με άλλες δυνατότητες του Aspose όπως η κρυπτογράφηση PDF. Καλή προγραμματιστική δουλειά, και εύχομαι τα PDF σας πάντα να διατηρούν την τέλεια τυπογραφία!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
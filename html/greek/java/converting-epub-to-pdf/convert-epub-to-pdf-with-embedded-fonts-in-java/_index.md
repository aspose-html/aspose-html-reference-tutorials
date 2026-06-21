---
category: general
date: 2026-04-11
description: Μετατρέψτε EPUB σε PDF και ενσωματώστε γραμματοσειρές στο PDF χρησιμοποιώντας
  το Aspose.HTML για Java. Μάθετε πώς να ενσωματώνετε γραμματοσειρές στο PDF, να ενεργοποιείτε
  την ενσωμάτωση γραμματοσειρών στο PDF και να δημιουργείτε υποσύνολα γραμματοσειρών
  στο PDF για μικρότερα αρχεία.
draft: false
keywords:
- convert epub to pdf
- embed fonts in pdf
- how to embed fonts pdf
- subset fonts in pdf
- enable font embedding pdf
language: el
og_description: Μετατρέψτε EPUB σε PDF και ενσωματώστε γραμματοσειρές στο PDF χρησιμοποιώντας
  το Aspose.HTML για Java. Αυτός ο οδηγός δείχνει πώς να ενσωματώσετε γραμματοσειρές
  στο PDF και να ενεργοποιήσετε την ενσωμάτωση γραμματοσειρών στο PDF σε λίγα μόνο
  βήματα.
og_title: Μετατροπή EPUB σε PDF με ενσωματωμένες γραμματοσειρές σε Java
tags:
- Java
- Aspose.HTML
- PDF conversion
title: Μετατροπή EPUB σε PDF με ενσωματωμένες γραμματοσειρές σε Java
url: /el/java/converting-epub-to-pdf/convert-epub-to-pdf-with-embedded-fonts-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή EPUB σε PDF με ενσωματωμένες γραμματοσειρές σε Java

Κάποτε χρειάστηκε να **μετατρέψετε EPUB σε PDF** αλλά ανησυχατε ότι το παραγόμενο αρχείο θα χάσει την όμορφη τυπογραφία του; Δεν είστε μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν το PDF επιστρέφει σε γενικές γραμματοσειρές, χαλώντας την εμπειρία ανάγνωσης.  

Τα καλά νέα; Με το Aspose.HTML for Java μπορείτε να **μετατρέψετε EPUB σε PDF** *και* να ενσωματώσετε τις αρχικές γραμματοσειρές ώστε το αποτέλεσμα να φαίνεται ακριβώς όπως η πηγή. Σε αυτό το tutorial θα δείξουμε επίσης πώς να **ενσωματώσετε γραμματοσειρές σε PDF**, να ενεργοποιήσετε την **υποσύνολο γραμματοσειρών** και να διατηρήσετε το μέγεθος του αρχείου λογικό.

Στο τέλος αυτού του οδηγού θα έχετε ένα έτοιμο‑για‑εκτέλεση πρόγραμμα Java που παίρνει ένα αρχείο EPUB, ενσωματώνει τις γραμματοσειρές του και παράγει ένα γυαλιστερό PDF. Χωρίς εξωτερικά εργαλεία, χωρίς χειροκίνητη διαχείριση γραμματοσειρών—απλώς κώδικας.

## Τι Θα Χρειαστείτε

- **Java Development Kit (JDK) 11+** – η πιο πρόσφατη σταθερή έκδοση λειτουργεί καλύτερα.  
- **Aspose.HTML for Java** βιβλιοθήκη (έκδοση 23.11 ή νεότερη).  
- Ένα αρχείο EPUB που θέλετε να μετατρέψετε (οποιοδήποτε αρχείο χωρίς DRM).  
- Ένα καλό IDE (IntelliJ IDEA, Eclipse ή ακόμη και VS Code).  

Αυτό είναι όλο. Αν ήδη έχετε έργο Maven ή Gradle, απλώς προσθέστε την εξάρτηση Aspose.HTML και είστε έτοιμοι.

![μετατροπή epub σε pdf με ενσωματωμένες γραμματοσειρές](image-placeholder.png "Εικονογράφηση της μετατροπής ενός αρχείου EPUB σε PDF με ενσωματωμένες γραμματοσειρές")

## Βήμα 1: Ρυθμίστε το Έργο σας και Προσθέστε το Aspose.HTML

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.11</version>
</dependency>
```

### Gradle

```groovy
implementation 'com.aspose:aspose-html:23.11'
```

> **Pro tip:** Αν χρησιμοποιείτε εταιρικό proxy, βεβαιωθείτε ότι τα URLs των αποθετηρίων είναι προσβάσιμα· διαφορετικά η κατασκευή θα αποτύχει σιωπηλά.

Η εγκατάσταση της βιβλιοθήκης σας δίνει πρόσβαση στα `HTMLDocument`, `PdfConversionOptions` και στην κλάση `Converter` που θα χρησιμοποιήσουμε αργότερα.

## Βήμα 2: Φορτώστε το Έγγραφο EPUB

Το πρώτο που κάνουμε είναι να δημιουργήσουμε μια παρουσία `HTMLDocument` που δείχνει στο πηγαίο EPUB. Το Aspose.HTML αντιμετωπίζει το EPUB ως μια συλλογή σελίδων HTML στο παρασκήνιο, οπότε το API είναι απλό.

```java
import com.aspose.html.*;
import com.aspose.html.converters.*;

public class EpubToPdfWithFonts {
    public static void main(String[] args) throws Exception {

        // 👉 Step 2: Load the EPUB you want to convert
        // Replace "input.epub" with the path to your file.
        HTMLDocument epubDocument = new HTMLDocument("YOUR_DIRECTORY/input.epub");

        // ... we'll add conversion options next
    }
}
```

> **Γιατί είναι σημαντικό:** Η φόρτωση του EPUB ως `HTMLDocument` διατηρεί το εσωτερικό CSS και τις αναφορές γραμματοσειρών, κάτι που είναι κρίσιμο για την επακόλουθη **ενσωμάτωση γραμματοσειρών σε PDF**.

## Βήμα 3: Διαμορφώστε τις Επιλογές Μετατροπής PDF – Ενεργοποίηση Ενσωμάτωσης Γραμματοσειρών

Το Aspose.HTML σας δίνει λεπτομερή έλεγχο της εξόδου PDF. Για να βεβαιωθούμε ότι οι γραμματοσειρές θα μεταφερθούν μαζί με το PDF, ενεργοποιούμε δύο σημαίες:

1. **`setEmbedFonts(true)`** – λέει στον μετατροπέα να ενσωματώνει κάθε γραμματοσειρά που βρίσκει.  
2. **`setSubsetFonts(true)`** – περικόπτει κάθε ενσωματωμένη γραμματοσειρά μόνο στα γλύφους που χρησιμοποιούνται πραγματικά, μειώνοντας δραστικά το μέγεθος του αρχείου.

```java
        // 👉 Step 3: Create PDF conversion options and enable font embedding
        PdfConversionOptions pdfOptions = new PdfConversionOptions();
        pdfOptions.setEmbedFonts(true);      // embed fonts in PDF
        pdfOptions.setSubsetFonts(true);     // subset fonts in PDF
```

> **Πώς λειτουργεί:** Όταν το `embedFonts` είναι true, ο μετατροπέας εξάγει τα αρχεία γραμματοσειρών που αναφέρονται στο EPUB (π.χ. .ttf ή .otf) και τα γράφει στο λεξικό γραμματοσειρών του PDF. Η ενεργοποίηση του `subsetFonts` σημαίνει ότι αποθηκεύονται μόνο οι χαρακτήρες που χρησιμοποιούνται, κάτι που είναι το κλειδί για ελαφρύ PDF.

## Βήμα 4: Εκτελέστε τη Μετατροπή

Με το έγγραφο και τις επιλογές έτοιμες, το τελικό βήμα είναι μια κλήση μίας γραμμής στο `Converter.convert`. Γράφει το PDF στην τοποθεσία που καθορίζετε.

```java
        // 👉 Step 4: Convert the EPUB to PDF using the configured options
        Converter.convert(epubDocument, pdfOptions, "YOUR_DIRECTORY/output.pdf");

        System.out.println("Conversion complete! Check YOUR_DIRECTORY/output.pdf");
    }
}
```

Τρέξτε το πρόγραμμα και θα βρείτε ένα PDF που φαίνεται ακριβώς όπως το αρχικό EPUB—γραμματοσειρές, χρώματα και διάταξη αμετάβλητα.

### Αναμενόμενο Αποτέλεσμα

- **Οπτική πιστότητα:** Το PDF αντικατοπτρίζει την τυπογραφία του EPUB.  
- **Ενσωματωμένες γραμματοσειρές:** Ανοίξτε το PDF στο Adobe Acrobat → *File > Properties > Fonts* και θα δείτε κάθε γραμματοσειρά να εμφανίζεται ως “Embedded Subset”.  
- **Λογικό μέγεθος:** Επειδή ενεργοποιήσαμε **υποσύνολο γραμματοσειρών σε PDF**, το αρχείο είναι συχνά 30‑50 % μικρότερο από μια πλήρως ενσωματωμένη έκδοση.

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Λείπουν γραμματοσειρές στο αποτέλεσμα** | Το EPUB αναφέρει γραμματοσειρές που δεν είναι ενσωματωμένες (π.χ. συστημικές γραμματοσειρές). | Βεβαιωθείτε ότι το EPUB περιλαμβάνει τα δικά του αρχεία γραμματοσειρών, ή τοποθετήστε τις λείπουσες γραμματοσειρές σε φάκελο και ορίστε `pdfOptions.setAdditionalFontsFolder("path")`. |
| **LicenseException** | Το Aspose.HTML λειτουργεί σε λειτουργία αξιολόγησης μετά από 30 ημέρες. | Αγοράστε άδεια και καλέστε `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` πριν τη μετατροπή. |
| **FileNotFoundException** | Λανθασμένο μονοπάτι για το εισερχόμενο EPUB ή το εξαγόμενο PDF. | Χρησιμοποιήστε απόλυτα μονοπάτια ή `Paths.get("").toAbsolutePath()` για εντοπισμό σφαλμάτων. |
| **Μεγάλο PDF παρά το υποσύνολο** | Τα αρχεία γραμματοσειρών είναι τεράστια ή περιέχουν πολλούς αχρησιμοποίητους γλύφους. | Ελέγξτε ότι το EPUB δεν ενσωματώνει ολόκληρες οικογένειες γραμματοσειρών που δεν χρειάζεστε· σκεφτείτε να καθαρίσετε το EPUB πρώτα. |

## Ανακεφαλαίωση Βήμα‑Βήμα (με Όλο τον Κώδικα)

```java
import com.aspose.html.*;
import com.aspose.html.converters.*;

public class EpubToPdfWithFonts {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load the EPUB document you want to convert
        HTMLDocument epubDocument = new HTMLDocument("YOUR_DIRECTORY/input.epub");

        // 2️⃣ Create PDF conversion options and enable font embedding
        PdfConversionOptions pdfOptions = new PdfConversionOptions();
        pdfOptions.setEmbedFonts(true);      // embed fonts in PDF
        pdfOptions.setSubsetFonts(true);     // subset fonts in PDF

        // 3️⃣ Convert the EPUB to PDF using the configured options
        Converter.convert(epubDocument, pdfOptions, "YOUR_DIRECTORY/output.pdf");

        System.out.println("Conversion complete! Check YOUR_DIRECTORY/output.pdf");
    }
}
```

Αντιγράψτε‑και‑επικολλήστε το παραπάνω σε ένα αρχείο με όνομα `EpubToPdfWithFonts.java`, προσαρμόστε τα μονοπάτια, μεταγλωττίστε με `javac` και τρέξτε με `java`. Η κονσόλα θα επιβεβαιώσει πότε ολοκληρωθεί η μετατροπή.

## Προχωρημένες Ρυθμίσεις (Προαιρετικά)

### Ενεργοποίηση Συμμόρφωσης PDF/A

Αν χρειάζεστε PDF αρχειοθέτησης, ορίστε το επίπεδο συμμόρφωσης:

```java
pdfOptions.setCompliance(PdfCompliance.PdfA1b);
```

### Προσθήκη Κωδικού Πρόσβασης PDF

```java
pdfOptions.setPassword("Secret123");
```

### Έλεγχος Ποιότητας Εικόνας

```java
pdfOptions.setImageCompressionQuality(80); // 0‑100, higher = better quality
```

Όλες αυτές οι επιλογές εξακολουθούν να σέβονται την **ενσωμάτωση γραμματοσειρών PDF**, ώστε οι γραμματοσειρές σας να παραμένουν ενσωματωμένες.

## Επόμενα Βήματα & Σχετικά Θέματα

- **Πώς να ενσωματώσετε γραμματοσειρές PDF** σε άλλες μορφές (π.χ. DOCX → PDF).  
- **Ενεργοποίηση ενσωμάτωσης γραμματοσειρών PDF** όταν χρησιμοποιείτε iText ή PDFBox.  
- **Υποσύνολο γραμματοσειρών σε PDF** για τεράστιες αναφορές με χιλιάδες σελίδες.  
- Εξερευνήστε τις δυνατότητες του **Aspose.HTML** όπως μετατροπή HTML → PNG ή EPUB → DOCX.  

Πειραματιστείτε με τις παραπάνω επιλογές και σύντομα θα νιώσετε άνετα με τη διαχείριση γραμματοσειρών στη δημιουργία PDF.

## Συμπέρασμα

Διασχίσαμε ένα πλήρες, εκτελέσιμο παράδειγμα που **μετατρέπει epub σε pdf** ενώ **ενσωματώνει γραμματοσειρές σε pdf**, **πώς να ενσωματώσετε γραμματοσειρές pdf**, **υποσύνολο γραμματοσειρών σε pdf**, και **ενεργοποίηση ενσωμάτωσης γραμματοσειρών pdf**—όλα με λίγες μόνο γραμμές κώδικα Java. Το βασικό συμπέρασμα; Ενεργοποιήστε `setEmbedFonts` και `setSubsetFonts` για να διατηρήσετε την τυπογραφία και να κρατήσετε λογικά τα μεγέθη των αρχείων.  

Δοκιμάστε το με τα δικά σας EPUB, προσαρμόστε τις επιλογές μετατροπής και θα έχετε μια αξιόπιστη αλυσίδα παραγωγής όμορφα αποδομένων PDF κάθε φορά. Έχετε ερωτήσεις ή ένα επίμονο EPUB που δεν συνεργάζεται; Αφήστε ένα σχόλιο παρακάτω—καλή κωδικοποίηση!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
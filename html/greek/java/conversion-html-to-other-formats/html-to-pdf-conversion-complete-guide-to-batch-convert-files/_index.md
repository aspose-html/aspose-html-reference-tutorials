---
category: general
date: 2026-03-07
description: Μάθετε τη μετατροπή HTML σε PDF και πώς να μετατρέπετε μαζικά αρχεία,
  συμπεριλαμβανομένης της μετατροπής SVG σε PNG και του καθορισμού του μεγέθους της
  εικόνας, χρησιμοποιώντας το Aspose.HTML σε Java.
draft: false
keywords:
- html to pdf conversion
- how to batch convert
- batch convert files
- svg to png conversion
- set image size
language: el
og_description: Κατακτήστε τη μετατροπή html σε pdf και μάθετε πώς να μετατρέπετε
  μαζικά αρχεία, να εκτελείτε μετατροπή svg σε png και να ορίζετε το μέγεθος εικόνας
  χρησιμοποιώντας τη βιβλιοθήκη Aspose.HTML Java.
og_title: Μετατροπή html σε pdf – Μαζική μετατροπή αρχείων με το Aspose.HTML
tags:
- Java
- Aspose.HTML
- Document Conversion
title: Μετατροπή html σε pdf – Πλήρης Οδηγός για Μαζική Μετατροπή Αρχείων με το Aspose.HTML
url: /el/java/conversion-html-to-other-formats/html-to-pdf-conversion-complete-guide-to-batch-convert-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή html σε pdf – Πλήρης Οδηγός Μαζικής Μετατροπής

Ποτέ χρειάστηκε **html to pdf conversion** για δεκάδες αρχεία και αναρωτηθήκατε αν πρέπει να εκτελείτε ξεχωριστή διαδικασία για το καθένα; Αυτό είναι ένα κοινό πρόβλημα, ειδικά όταν το ίδιο έργο απαιτεί επίσης τη μετατροπή γραφικών SVG σε εικόνες PNG ή τη μετατροπή e‑books σε έγγραφα Word. Σε αυτόν τον οδηγό θα σας δείξουμε **πώς να κάνετε batch convert** ένα μεικτό σύνολο εγγράφων με ένα μόνο, καθαρό πρόγραμμα Java.

Θα αποκτήσετε ένα έτοιμο προς εκτέλεση παράδειγμα που **batch convert files** διαφορετικών τύπων, δείχνει **svg to png conversion**, και ακόμη σας δείχνει πώς να **set image size** για τα raster αποτελέσματα. Χωρίς εξωτερικά scripts, χωρίς χειροκίνητη αντιγραφή‑επικόλληση — μόνο ένας ενιαίος κώδικας που μπορείτε να ενσωματώσετε στο πρότζεκτ σας σήμερα.

## Τι καλύπτει αυτό το tutorial

* Τα ακριβή βήματα για τη δημιουργία ενός `BatchConverter` με Aspose.HTML.  
* Προσθήκη εργασίας **html to pdf conversion**, εργασίας **svg to png conversion** (με προσαρμοσμένες διαστάσεις) και εργασίας EPUB → DOCX.  
* Εκτέλεση του batch και ερμηνεία της αναφοράς αποτελεσμάτων.  
* Συμβουλές για διαχείριση μεγάλων batches, διαχείριση σφαλμάτων και επιδόσεων.  
* Ένα πλήρες, εκτελέσιμο πρόγραμμα Java – αντιγράψτε, επικολλήστε και τρέξτε.

> **Prerequisites** – Θα χρειαστείτε Java 8+ και τη βιβλιοθήκη Aspose.HTML for Java (έκδοση 23.8 ή νεότερη). Οι χρήστες Maven μπορούν να την προσθέσουν με την τυπική εξάρτηση· οι χρήστες IDE μπορούν να προσθέσουν το JAR χειροκίνητα. Δεν απαιτούνται άλλα frameworks.

---

## Step 1: Set Up the Project and Import Aspose.HTML

Πριν βουτήξουμε στη λογική του batch, βεβαιωθείτε ότι η βιβλιοθήκη βρίσκεται στο classpath σας.

**Maven**  

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.8</version>
</dependency>
```

**Gradle**  

```gradle
implementation "com.aspose:aspose-html:23.8"
```

Αν προτιμάτε τη χειροκίνητη προσέγγιση, κατεβάστε το JAR από την ιστοσελίδα της Aspose και προσθέστε το στις βιβλιοθήκες του IDE σας.

> **Pro tip:** Κρατήστε την έκδοση της βιβλιοθήκης σε συγχρονισμό με το Java runtime σας για να αποφύγετε `NoClassDefFoundError` κατά την εκτέλεση.

---

## Step 2: Create a Batch Converter for html to pdf conversion and More

Η καρδιά της λύσης είναι η κλάση `BatchConverter`. Κρατά μια ουρά εργασιών μετατροπής που μπορείτε να εκτελέσετε με μία κλήση.

```java
import com.aspose.html.converters.*;
import java.util.*;

public class BatchConversionDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣  Initialize the batch converter – this will store every job we add.
        BatchConverter batchConverter = new BatchConverter();
```

Εδώ δημιουργήσαμε το αντικείμενο batch. Σκεφτείτε το ως μια λίστα εργασιών για τις μετατροπές σας. Η προσθήκη εργασιών αργότερα είναι τόσο απλή όσο η κλήση `addConversion`.

---

## Step 3: Add an html to pdf conversion Job (Primary Use‑Case)

Τώρα θα βάλουμε στην ουρά τη **html to pdf conversion**. Αυτό το βήμα δείχνει ακριβώς **how to batch convert** ένα αρχείο HTML μαζί με άλλες μορφές.

```java
        // 2️⃣  Queue HTML → PDF conversion.
        // Replace YOUR_DIRECTORY with the actual folder path.
        batchConverter.addConversion(
                "YOUR_DIRECTORY/input.html",          // source HTML
                "YOUR_DIRECTORY/output.pdf",          // target PDF
                new PdfConversionOptions());          // default PDF options
```

Το αντικείμενο `PdfConversionOptions` σας επιτρέπει να ρυθμίσετε στοιχεία όπως η έκδοση PDF, αλλά οι προεπιλογές λειτουργούν για τις περισσότερες περιπτώσεις. Αν χρειάζεστε κρυπτογράφηση ή συμπίεση, μπορείτε να το ρυθμίσετε εδώ.

---

## Step 4: Add an svg to png conversion Job and set image size

Στη συνέχεια, θα δείξουμε **svg to png conversion** ενώ ταυτόχρονα δείχνουμε πώς να **set image size** για το raster αποτέλεσμα. Αυτό είναι χρήσιμο όταν χρειάζεστε μικρογραφίες ή εικόνες έτοιμες για το web.

```java
        // 3️⃣  Prepare PNG options – we’ll resize the output to 800×600.
        ImageConversionOptions pngOptions = new ImageConversionOptions();
        pngOptions.setWidth(800);   // set image width
        pngOptions.setHeight(600);  // set image height

        // Queue SVG → PNG conversion with the custom size.
        batchConverter.addConversion(
                "YOUR_DIRECTORY/input.svg",
                "YOUR_DIRECTORY/output.png",
                pngOptions);
```

Καλώντας `setWidth` και `setHeight`, ορίζουμε ρητά **set image size**. Η Aspose.HTML θα διατηρήσει την αναλογία διαστάσεων του SVG αν ορίσετε μόνο μία διάσταση, αλλά παρέχοντας και τις δύο έχετε ακριβή έλεγχο.

---

## Step 5: Add an EPUB → DOCX conversion Job (Bonus)

Αν και η κύρια εστίαση είναι **html to pdf conversion**, τα περισσότερα πραγματικά έργα χρειάζονται επίσης διαχείριση e‑books. Η προσθήκη μιας εργασίας EPUB → DOCX είναι εξίσου απλή.

```java
        // 4️⃣  Queue EPUB → DOCX conversion.
        batchConverter.addConversion(
                "YOUR_DIRECTORY/input.epub",
                "YOUR_DIRECTORY/output.docx",
                new DocxConversionOptions());
```

Η κλάση `DocxConversionOptions` προσφέρει ρυθμίσεις για τη διάταξη σελίδας, αλλά οι προεπιλογές συνήθως παράγουν ένα πιστό έγγραφο Word.

---

## Step 6: Execute the Batch and Review Results

Με όλες τις εργασίες στην ουρά, εκκινούμε το batch. Η μέθοδος `execute` επιστρέφει ένα `BatchConversionResult` που περιέχει μια λίστα από αντικείμενα `ConversionJob`, το καθένα αναφέρει επιτυχία ή αποτυχία.

```java
        // 5️⃣  Run every queued conversion in one go.
        BatchConversionResult conversionResult = batchConverter.execute();

        // 6️⃣  Print a concise report – useful for CI pipelines.
        conversionResult.getJobs().forEach(job -> {
            System.out.println(job.getSource() + " → " + job.getTarget() +
                               " : " + (job.isSuccess() ? "OK" : "FAIL"));
        });
    }
}
```

Ένα παράδειγμα εξόδου στην κονσόλα μπορεί να είναι:

```
YOUR_DIRECTORY/input.html → YOUR_DIRECTORY/output.pdf : OK
YOUR_DIRECTORY/input.svg → YOUR_DIRECTORY/output.png : OK
YOUR_DIRECTORY/input.epub → YOUR_DIRECTORY/output.docx : OK
```

Αν κάποια εργασία αποτύχει, η σημαία `job.isSuccess()` θα είναι `false` και μπορείτε να ανακτήσετε την εξαίρεση μέσω `job.getException()` για πιο λεπτομερή αποσφαλμάτωση.

---

## Step 7: Run the Program and Verify the Files

Συγκεντρώστε και τρέξτε την κλάση:

```bash
javac -cp ".:aspose-html-23.8.jar" BatchConversionDemo.java
java -cp ".:aspose-html-23.8.jar" BatchConversionDemo
```

Μετά την εκτέλεση, ελέγξτε το φάκελο `YOUR_DIRECTORY`. Θα πρέπει να δείτε:

* `output.pdf` – μια πιστή απόδοση PDF του `input.html`.  
* `output.png` – ένα PNG 800×600 που προέρχεται από το `input.svg`.  
* `output.docx` – ένα έγγραφο Word που περιέχει το περιεχόμενο του EPUB.

Ανοίξτε κάθε αρχείο για να επιβεβαιώσετε ότι η μετατροπή ολοκληρώθηκε επιτυχώς και ότι οι διαστάσεις της εικόνας ταιριάζουν με τις τιμές που ορίσατε.

---

## Common Questions & Edge Cases

### What if I have 100+ files to convert?

Ο `BatchConverter` επεξεργάζεται τις εργασίες διαδοχικά από προεπιλογή. Για τεράστιες φορτώσεις μπορείτε:

1. **Split the list** σε μικρότερα batches (π.χ., 20 αρχεία το καθένα) για να αποφύγετε αιχμές μνήμης.  
2. **Run batches in parallel** χρησιμοποιώντας το `ExecutorService` της Java. Κάθε νήμα μπορεί να δημιουργήσει το δικό του `BatchConverter` – η βιβλιοθήκη είναι thread‑safe για λειτουργίες μόνο ανάγνωσης.

### How does the library handle unsupported formats?

Αν προσπαθήσετε να μετατρέψετε μια μορφή που η Aspose.HTML δεν αναγνωρίζει, η εργασία θα αποτύχει και το `job.isSuccess()` θα είναι `false`. Η εξαίρεση θα υποδείξει “Unsupported conversion type”. Προστατέψτε το ελέγχοντας τις επεκτάσεις αρχείων πριν τα προσθέσετε στο batch.

### Can I customize PDF metadata (author, title)?

Απόλυτα. Η `PdfConversionOptions` εκθέτει τη μέθοδο `setPdfDocumentOptions` όπου μπορείτε να ορίσετε το αντικείμενο `PdfDocumentInfo`. Παράδειγμα:

```java
PdfConversionOptions pdfOpts = new PdfConversionOptions();
pdfOpts.getPdfDocumentOptions().setAuthor("John Doe");
pdfOpts.getPdfDocumentOptions().setTitle("Generated Report");
batchConverter.addConversion("report.html", "report.pdf", pdfOpts);
```

### What about logging?

Η Aspose.HTML γράφει διαγνωστικά μηνύματα στην κονσόλα από προεπιλογή. Μπορείτε να τα ανακατευθύνετε ρυθμίζοντας το `java.util.logging` ή παρέχοντας μια προσαρμοσμένη υλοποίηση `ILogger`.

---

## Pro Tips for Production‑Ready Batch Conversion

| Tip | Why It Matters |
|-----|----------------|
| **Reuse a single `BatchConverter` instance** | Μειώνει το κόστος δημιουργίας αντικειμένων και διατηρεί τη χρήση μνήμης χαμηλή. |
| **Validate input files before queuing** | Αποτρέπει περιττές αποτυχίες και επιταχύνει την εκτέλεση του batch. |
| **Use absolute paths** | Αποφεύγει σύγχυση όταν αλλάζει ο τρέχων φάκελος (π.χ., σε CI server). |
| **Enable `setOverwriteExisting(true)`** in conversion options if you want to replace old outputs automatically. |
| **Monitor execution time** – wrap `batchConverter.execute()` with `System.nanoTime()` to log performance metrics. |
| **Handle exceptions per job** – the batch result gives you per‑job exceptions, making it easy to retry only the failed items. |

---

## Visual Overview

![Διάγραμμα μαζικής μετατροπής html σε pdf](https://example.com/batch-diagram.png "Διάγραμμα που δείχνει πώς η μετατροπή html σε pdf, η μετατροπή svg σε png και η μετατροπή epub σε docx γίνονται σε σειρά και επεξεργάζονται μαζί")

*Image alt text:* **Διάγραμμα μαζικής μετατροπής html σε pdf** που απεικονίζει πολλαπλούς τύπους αρχείων που επεξεργάζονται σε μία εκτέλεση.

---

## Conclusion

Τώρα έχετε ένα πλήρες, production‑ready παράδειγμα που δείχνει **html to pdf conversion**, παρουσιάζει **how to batch convert** ένα μεικτό σύνολο εγγράφων, εκτελεί **svg to png conversion** ενώ **set image size**, και ακόμη διαχειρίζεται μετατροπές EPUB → DOCX. Χρησιμοποιώντας το `BatchConverter` της Aspose.HTML, εξαλείφετε επαναλαμβανόμενο κώδικα, αποκτάτε ένα ενιαίο σημείο διαχείρισης σφαλμάτων και διατηρείτε την αλυσίδα μετατροπής σας οργανωμένη.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να προσθέσετε υδατογράφημα PDF, να συμπιέσετε το PNG output, ή να ενσωματώσετε αυτή τη δουλειά batch σε μια μικροϋπηρεσία Spring Boot. Το ίδιο pattern κλιμακώνεται — απλώς συνεχίστε να προσθέτετε εργασίες και αφήστε τη μηχανή batch να κάνει το δύσκολο.

Αν αντιμετωπίσετε δυσκολίες ή έχετε ιδέες για περαιτέρω βελτιώσεις, αφήστε ένα σχόλιο παρακάτω. Καλό coding και απολαύστε την απλότητα της μαζικής μετατροπής!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-03-29
description: Πώς να ενσωματώσετε εικόνες κατά τη μετατροπή MHTML σε PDF με το Aspose
  HTML. Μειώστε το μέγεθος του αρχείου PDF και κατακτήστε τις τεχνικές Aspose HTML
  σε PDF σε λίγα λεπτά.
draft: false
keywords:
- how to embed images
- convert mhtml to pdf
- reduce pdf file size
- aspose html to pdf
- reduce pdf size
language: el
og_description: Πώς να ενσωματώσετε εικόνες κατά τη μετατροπή MHTML σε PDF με το Aspose
  HTML. Μάθετε πώς να μειώσετε το μέγεθος του αρχείου PDF και να αξιοποιήσετε στο
  έπακρο το Aspose HTML σε PDF.
og_title: Πώς να ενσωματώσετε εικόνες κατά τη μετατροπή MHTML σε PDF – Οδηγός Aspose
tags:
- Aspose
- Java
- PDF
- MHTML
title: Πώς να ενσωματώσετε εικόνες κατά τη μετατροπή MHTML σε PDF – Οδηγός Aspose
url: /el/java/conversion-html-to-other-formats/how-to-embed-images-when-converting-mhtml-to-pdf-aspose-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ενσωματώσετε εικόνες κατά τη μετατροπή MHTML σε PDF – Οδηγός Aspose

Έχετε αναρωτηθεί **πώς να ενσωματώσετε εικόνες** κατά τη μετατροπή MHTML‑σε‑PDF και να διατηρήσετε το τελικό αρχείο ελαφρύ; Δεν είστε οι μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν πρόβλημα όταν τα PDF τους μεγαλώνουν επειδή κάθε πόρος—γραμματοσειρές, σενάρια, ακόμη και μικρά εικονίδια—ενσωματώνεται. Τα καλά νέα; Με το Aspose.HTML for Java μπορείτε να πείτε στον μετατροπέα να ενσωματώνει **μόνο τις εικόνες**, αφήνοντας τα υπόλοιπα ως εξωτερικές αναφορές. Αυτή η μικρή ρύθμιση συχνά μειώνει δραστικά το μέγεθος του PDF.

Σε αυτό το tutorial θα περάσουμε από τη μετατροπή μιας αναφοράς MHTML σε PDF, θα εστιάσουμε στο **πώς να ενσωματώσετε εικόνες**, και θα προσθέσουμε μερικές επιπλέον συμβουλές για **μείωση του μεγέθους του PDF**. Στο τέλος θα έχετε μια έτοιμη κλάση Java, θα καταλάβετε γιατί η ενσωμάτωση μόνο των εικόνων είναι σημαντική, και θα ξέρετε πού να πάτε αν αργότερα χρειαστεί να ενσωματώσετε γραμματοσειρές ή άλλους πόρους. Χωρίς ασαφείς «δείτε την τεκμηρίωση» συντομεύσεις—απλώς μια πλήρης, αντιγραφή‑επικόλληση λύση.

## Τι θα μάθετε

- Τα ακριβή API calls που χρειάζονται για **μετατροπή MHTML σε PDF** με το Aspose.HTML.  
- Πώς να διαμορφώσετε το `PdfConversionOptions` ώστε ο μετατροπέας **να ενσωματώνει μόνο εικόνες**.  
- Γιατί η ενσωμάτωση μόνο των εικόνων βοηθά **να μειωθεί το μέγεθος του PDF** και πότε μπορεί να χρειαστεί διαφορετική ρύθμιση.  
- Ένα πλήρες, εκτελέσιμο παράδειγμα Java που μπορείτε να ενσωματώσετε σε οποιοδήποτε Maven/Gradle project.  
- Συνήθεις παγίδες (ελλιπείς πόροι, λανθασμένες διαδρομές αρχείων) και γρήγορες λύσεις.

### Προαπαιτούμενα

- Java 8 ή νεότερη εγκατεστημένη.  
- Maven ή Gradle για διαχείριση εξαρτήσεων (θα δείξουμε το απόσπασμα Maven).  
- Βιβλιοθήκη Aspose.HTML for Java (μπορείτε να κατεβάσετε δωρεάν δοκιμαστική έκδοση από την ιστοσελίδα της Aspose).  
- Ένα αρχείο MHTML που θέλετε να μετατρέψετε σε PDF (το παράδειγμα χρησιμοποιεί το `report.mhtml`).

> **Pro tip:** Κρατήστε το MHTML και το παραγόμενο PDF στον ίδιο φάκελο κατά τη δοκιμή· οι σχετικές διαδρομές διατηρούν τα πράγματα οργανωμένα.

---

## Βήμα 1 – Προσθήκη Aspose.HTML στο έργο σας

Αν χρησιμοποιείτε Maven, επικολλήστε το παρακάτω στο `pom.xml`. Η έκδοση που φαίνεται είναι η πιο πρόσφατη τον Μάρτιο 2026· ελέγξτε το αποθετήριο της Aspose για νεότερες εκδόσεις.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

Για Gradle, το ισοδύναμο είναι:

```groovy
implementation 'com.aspose:aspose-html:23.12'
```

Μόλις λυθεί η εξάρτηση, είστε έτοιμοι να εισάγετε τις κλάσεις που θα χρειαστούμε.

## Βήμα 2 – Δημιουργία επιλογών μετατροπής και ορισμός του τρόπου ενσωμάτωσης

Η καρδιά του **πώς να ενσωματώσετε εικόνες** βρίσκεται στο `PdfConversionOptions`. Από προεπιλογή το Aspose ενσωματώνει *όλους* τους πόρους (γραμματοσειρές, CSS, εικόνες). Θα το αλλάξουμε σε `EMBED_IMAGES_ONLY`.

```java
// Step 2: Prepare conversion options – embed only images
PdfConversionOptions options = new PdfConversionOptions();
options.setResourceEmbeddingMode(ResourceEmbeddingMode.EMBED_IMAGES_ONLY);
```

Γιατί είναι σημαντικό; Σκεφτείτε μια εταιρική αναφορά που αναφέρεται σε μια εταιρική γραμματοσειρά αποθηκευμένη σε κοινόχρηστο δίκτυο. Η ενσωμάτωση αυτής της γραμματοσειράς αυξάνει το PDF κατά εκατοντάδες kilobytes, παρόλο που ο αναγνώστης μπορεί να την κατεβάσει απομακρυσμένα. Ενσωματώνοντας μόνο τις εικόνες, το PDF διατηρεί την οπτική πιστότητα που χρειάζεστε ενώ παραμένει ελαφρύ.

## Βήμα 3 – Εκτέλεση της μετατροπής

Τώρα καλούμε το `Converter.convert`, περνώντας τη διαδρομή του πηγαίου MHTML, τη διαδρομή του προορισμού PDF, και τις επιλογές που μόλις διαμορφώσαμε.

```java
// Step 3: Convert MHTML to PDF using the options above
String sourcePath = "YOUR_DIRECTORY/report.mhtml";
String targetPath = "YOUR_DIRECTORY/report.pdf";

Converter.convert(sourcePath, targetPath, options);
```

Αν όλα είναι σωστά ρυθμισμένα, θα δείτε ένα `report.pdf` να εμφανίζεται δίπλα στο αρχείο MHTML. Ανοίξτε το—κάθε εικόνα από την αρχική αναφορά πρέπει να είναι εκεί, ενώ οι γραμματοσειρές και το CSS παραμένουν εξωτερικές αναφορές.

## Βήμα 4 – Επαλήθευση της μείωσης του μεγέθους PDF

Μια γρήγορη επιβεβαίωση βοηθά να βεβαιωθείτε ότι **μειώσατε το μέγεθος του PDF**. Συγκρίνετε το μέγεθος του αρχείου πριν και μετά την αλλαγή του τρόπου ενσωμάτωσης:

```java
File before = new File("YOUR_DIRECTORY/report_full.pdf"); // generated with default settings
File after  = new File(targetPath); // our image‑only PDF

System.out.println("Full embed size: " + before.length() / 1024 + " KB");
System.out.println("Images‑only size: " + after.length() / 1024 + " KB");
```

Στις περισσότερες περιπτώσεις θα δείτε πτώση 30‑70 % ανάλογα με το πόσες γραμματοσειρές ή αρχεία CSS ήταν αρχικά ενσωματωμένα. Αυτό αποτελεί σημαντικό κέρδος για όποιον στέλνει PDFs μέσω διαδικτύου ή τα αποθηκεύει σε cloud.

## Βήμα 5 – Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω βρίσκεται ολόκληρη η κλάση Java που μπορείτε να αντιγράψετε στο IDE σας. Αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή όπου βρίσκεται το `report.mhtml`.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfConversionOptions;
import com.aspose.html.converters.ResourceEmbeddingMode;

import java.io.File;

public class MhtmlToPdf {
    public static void main(String[] args) throws Exception {

        // ---------- Step 1: Define source and destination ----------
        String sourcePath = "YOUR_DIRECTORY/report.mhtml";
        String targetPath = "YOUR_DIRECTORY/report.pdf";

        // ---------- Step 2: Set conversion options (embed only images) ----------
        PdfConversionOptions conversionOptions = new PdfConversionOptions();
        conversionOptions.setResourceEmbeddingMode(ResourceEmbeddingMode.EMBED_IMAGES_ONLY);

        // ---------- Step 3: Run the conversion ----------
        Converter.convert(sourcePath, targetPath, conversionOptions);
        System.out.println("Conversion complete! PDF saved to: " + targetPath);

        // ---------- Step 4: (Optional) Show size reduction ----------
        File outputPdf = new File(targetPath);
        System.out.println("Resulting PDF size: " + outputPdf.length() / 1024 + " KB");
    }
}
```

**Αναμενόμενη έξοδος** (στην κονσόλα):

```
Conversion complete! PDF saved to: YOUR_DIRECTORY/report.pdf
Resulting PDF size: 842 KB
```

Ανοίξτε το `report.pdf` σε οποιονδήποτε προβολέα· θα πρέπει να δείτε όλες τις αρχικές εικόνες να εμφανίζονται σωστά. Αν παρατηρήσετε ελλιπείς εικόνες, ελέγξτε ξανά ότι τα URLs των εικόνων στο MHTML είναι απόλυτα ή ότι τα αρχεία είναι προσβάσιμα από τη μηχανή μετατροπής.

## Συχνές ερωτήσεις & αντιμετώπιση ειδικών περιπτώσεων

### Τι γίνεται αν *πρέπει* να ενσωματώσω γραμματοσειρές;

Αλλάξτε το `ResourceEmbeddingMode` σε `EMBED_ALL` ή `EMBED_FONTS_ONLY`. Το enum προσφέρει τέσσερις επιλογές:

| Λειτουργία               | Τι ενσωματώνεται |
|--------------------------|-------------------|
| `EMBED_ALL`              | Εικόνες, γραμματοσειρές, CSS |
| `EMBED_IMAGES_ONLY`      | Μόνο εικόνες (η προεπιλογή μας) |
| `EMBED_FONTS_ONLY`       | Μόνο γραμματοσειρές |
| `EMBED_NONE`             | Τίποτα (μόνο εξωτερικές αναφορές) |

### Το MHTML μου περιέχει εξωτερικό CSS που επηρεάζει τη διάταξη—θα χαλάσει το PDF;

Αφού δεν ενσωματώνουμε CSS, ο μετατροπέας θα το κατεβάσει κατά τη μετατροπή. Αν το CSS φιλοξενείται σε εσωτερικό δίκτυο που ο διακομιστής μετατροπής δεν μπορεί να προσεγγίσει, η διάταξη μπορεί να επιστρέψει στα προεπιλεγμένα. Σε αυτές τις περιπτώσεις, είτε ενσωματώστε το CSS (`EMBED_ALL`) είτε αντιγράψτε το φύλλο στυλ τοπικά και προσαρμόστε το MHTML ώστε να δείχνει στο τοπικό αρχείο.

### Μπορώ να επεξεργαστώ παρτίδες (batch) φακέλου MHTML;

Απόλυτα. Τυλίξτε τη λογική μετατροπής σε βρόχο που διατρέχει τα `File.listFiles()` και προσαρμόστε το όνομα του αρχείου προορισμού ανάλογα. Θυμηθείτε να επαναχρησιμοποιήσετε ένα μόνο αντικείμενο `PdfConversionOptions` για καλύτερη απόδοση.

### Τι γίνεται με την κατανάλωση μνήμης για τεράστια έγγραφα;

Το Aspose.HTML κάνει streaming του περιεχομένου, οπότε η χρήση μνήμης παραμένει μέτρια. Ωστόσο, πολύ μεγάλες εικόνες μπορεί ακόμα να προκαλέσουν αυξήσεις. Αν αντιμετωπίσετε `OutOfMemoryError`, σκεφτείτε να μειώσετε την ανάλυση των εικόνων πριν την ενσωμάτωση—το Aspose προσφέρει `ImageConversionOptions` για αυτό, αλλά αυτό είναι θέμα άλλου tutorial.

---

## Συμπέρασμα

Τώρα ξέρετε **πώς να ενσωματώσετε εικόνες** κατά τη μετατροπή MHTML σε PDF με το Aspose.HTML, και έχετε δει πώς αυτή η μικρή ρύθμιση μπορεί να **μειώσει δραστικά το μέγεθος του PDF**. Το πλήρες, αντιγραφή‑επικόλληση παράδειγμα Java δείχνει όλη τη διαδικασία—from την προσθήκη της εξάρτησης Maven μέχρι την εκτύπωση του τελικού μεγέθους αρχείου.

Από εδώ μπορείτε:

- Να πειραματιστείτε με το `EMBED_FONTS_ONLY` αν τα PDFs σας πρέπει να είναι απολύτως αυτόνομα.  
- Να αυτοματοποιήσετε παρτίδες μετατροπών για ολόκληρο φάκελο αναφορών.  
- Να συνδυάσετε αυτήν την τεχνική με τα API βελτιστοποίησης PDF του Aspose για ακόμη μικρότερα αρχεία.

Είτε χτίζετε μια υπηρεσία αναφορών, μια γραμμή μετατροπής email‑σε‑PDF, είτε απλώς καθαρίζετε αρχειοθετημένες ιστοσελίδες, ο έλεγχος του τι ενσωματώνεται είναι ένας βασικός μοχλός για απόδοση και κόστος. Δοκιμάστε το, προσαρμόστε τις επιλογές, και αφήστε τα PDFs σας όσο πιο ελαφριά γίνεται.

*Καλό προγραμματισμό!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
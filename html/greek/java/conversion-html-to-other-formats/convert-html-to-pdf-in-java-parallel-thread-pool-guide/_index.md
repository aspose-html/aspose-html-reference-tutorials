---
category: general
date: 2026-05-31
description: Μετατρέψτε HTML σε PDF χρησιμοποιώντας το σταθερό thread pool της Java.
  Μάθετε πώς να μετατρέπετε πολλαπλά αρχεία HTML ταυτόχρονα με το Aspose HTML σε PDF
  και πώς να τερματίζετε σωστά το ExecutorService.
draft: false
keywords:
- convert html to pdf
- java fixed thread pool
- convert multiple html files
- shutdown executorservice java
- aspose html to pdf
language: el
og_description: Μετατρέψτε HTML σε PDF γρήγορα με τη Java. Αυτός ο οδηγός δείχνει
  πώς να μετατρέψετε πολλαπλά αρχεία HTML χρησιμοποιώντας μια σταθερή ομάδα νημάτων
  και το Aspose HTML σε PDF, καθώς και το σωστό κλείσιμο του ExecutorService.
og_title: Μετατροπή HTML σε PDF σε Java – Οδηγός Thread Pool
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Convert HTML to PDF using Java's fixed thread pool. Learn how to convert
    multiple HTML files concurrently with Aspose HTML to PDF and properly shutdown
    ExecutorService.
  headline: Convert HTML to PDF in Java – Parallel Thread Pool Guide
  type: TechArticle
- description: Convert HTML to PDF using Java's fixed thread pool. Learn how to convert
    multiple HTML files concurrently with Aspose HTML to PDF and properly shutdown
    ExecutorService.
  name: Convert HTML to PDF in Java – Parallel Thread Pool Guide
  steps:
  - name: Why a Fixed Thread Pool?
    text: A `FixedThreadPool` gives you predictable resource usage. Unlike `CachedThreadPool`,
      it won’t spawn an unbounded number of threads that could exhaust memory or CPU.
      For I/O‑bound work like file conversion, matching the pool size to the number
      of available cores *plus* a couple of extra threads usual
  - name: How Aspose Handles the Conversion
    text: '`Converter.convert` reads the source HTML, renders it internally using
      a headless browser engine, and writes a PDF file based on the supplied `PdfSaveOptions`.
      The default options produce a faithful layout, embedded fonts, and vector graphics—perfect
      for most business documents.'
  - name: TL;DR
    text: You now have a battle‑tested recipe to **convert HTML to PDF** in Java using
      a **fixed thread pool**, efficiently handling **multiple HTML files** and correctly
      **shutting down the ExecutorService**. Drop the code into your
  type: HowTo
tags:
- Java
- Concurrency
- PDF Generation
title: Μετατροπή HTML σε PDF σε Java – Οδηγός Παράλληλου Thread Pool
url: /el/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-parallel-thread-pool-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή HTML σε PDF σε Java – Οδηγός Παράλληλης Πισίνας Νημάτων  

Έχετε αναρωτηθεί ποτέ πώς να **μετατρέψετε HTML σε PDF** χωρίς να μπλοκάρετε το UI σας ή να περιμένετε κάθε αρχείο να ολοκληρωθεί ένα‑με‑ένα; Δεν είστε μόνοι. Σε πολλές επιχειρησιακές περιπτώσεις έχουμε δεκάδες αναφορές, τιμολόγια ή σελίδες μάρκετινγκ που πρέπει να γίνουν PDF ταυτόχρονα, και η σειριακή εκτέλεση δεν είναι αποδοτική.  

Σε αυτό το tutorial θα δείτε ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που **μετατρέπει πολλαπλά αρχεία HTML** παράλληλα χρησιμοποιώντας μια **σταθερή πισίνα νημάτων Java** και τη βιβλιοθήκη **Aspose HTML to PDF**. Θα καλύψουμε επίσης τον σωστό τρόπο **shutdown ExecutorService Java** ώστε η εφαρμογή σας να τερματίζει καθαρά.  

Στο τέλος του οδηγού θα έχετε ένα επαναχρησιμοποιήσιμο μοτίβο που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Java, είτε χτίζετε ένα micro‑service είτε μια επιτραπέζια εφαρμογή. Χωρίς εξωτερικά scripts, χωρίς μυστικά βήματα—απλώς καθαρός κώδικας Java που μπορείτε να μεταγλωττίσετε και να τρέξετε σήμερα.

---

## Τι Θα Χρειαστείτε  

- **JDK 11 ή νεότερο** – ο κώδικας χρησιμοποιεί το σύγχρονο API σύγχυσης, αλλά λειτουργεί σε οποιαδήποτε πρόσφατη έκδοση της Java.  
- **Aspose.HTML for Java** – εμπορική βιβλιοθήκη που παρέχει `Converter` και `PdfSaveOptions`. Μπορείτε να κατεβάσετε μια δωρεάν δοκιμή από την ιστοσελίδα της Aspose.  
- Ένα IDE ή ένας απλός επεξεργαστής κειμένου συν Maven/Gradle για τη διαχείριση της εξάρτησης.  

Αν δεν έχετε προσθέσει ποτέ ένα τρίτο‑μέρος JAR, απλώς τοποθετήστε το `aspose-html-x.x.x.jar` στον φάκελο `libs` του έργου σας και προσθέστε το στο classpath. Οι χρήστες Maven μπορούν να προσθέσουν:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- replace with the latest -->
</dependency>
```

---

## ## Μετατροπή HTML σε PDF με Σταθερή Πισίνα Νημάτων  

Παρακάτω βρίσκεται η καρδιά της λύσης. Δημιουργούμε μια **σταθερού μεγέθους πισίνα νημάτων**, δίνουμε κάθε αρχείο HTML σε έναν εργαζόμενο και αφήνουμε την Aspose να κάνει το σκληρό έργο. Το μέγεθος της πισίνας (`4` στο παράδειγμα) μπορεί να ρυθμιστεί ώστε να ταιριάζει με τους πυρήνες CPU ή το εύρος ζώνης I/O.

```java
import java.util.concurrent.*;
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.PdfSaveOptions;

/**
 * ParallelConversionDemo demonstrates how to convert HTML to PDF
 * concurrently using a Java fixed thread pool and Aspose HTML to PDF.
 */
public class ParallelConversionDemo {

    public static void main(String[] args) throws Exception {
        // Step 1: Create a fixed‑size thread pool for concurrent work
        ExecutorService executor = Executors.newFixedThreadPool(4);

        // Step 2: List the HTML files to be converted (adjust the directory)
        String[] inputFiles = {
            "YOUR_DIRECTORY/a.html",
            "YOUR_DIRECTORY/b.html",
            "YOUR_DIRECTORY/c.html",
            "YOUR_DIRECTORY/d.html"
        };

        // Step 3: Submit a conversion task for each input file
        for (String htmlPath : inputFiles) {
            executor.submit(() -> {
                try {
                    // Step 4: Prepare PDF save options (default settings are fine)
                    PdfSaveOptions pdfOptions = new PdfSaveOptions();

                    // Step 5: Convert the HTML file to PDF; each thread uses its own Converter instance
                    String pdfPath = htmlPath.replace(".html", ".pdf");
                    Converter.convert(htmlPath, pdfOptions, pdfPath);

                    System.out.println(htmlPath + " → PDF conversion completed");
                } catch (Exception e) {
                    // Step 5b: Log the error but keep the pool alive
                    System.err.println("Failed to convert " + htmlPath);
                    e.printStackTrace();
                }
            });
        }

        // Step 6: Shut down the pool and wait for all tasks to finish
        executor.shutdown();                       // graceful stop – no new tasks accepted
        boolean finished = executor.awaitTermination(5, TimeUnit.MINUTES);
        if (finished) {
            System.out.println("All conversions finished successfully.");
        } else {
            System.err.println("Timeout reached before all tasks completed.");
        }
    }
}
```

### Γιατί Σταθερή Πισίνα Νημάτων;  

Μια `FixedThreadPool` σας προσφέρει προβλέψιμη χρήση πόρων. Σε αντίθεση με την `CachedThreadPool`, δεν θα δημιουργήσει απεριόριστο αριθμό νημάτων που θα μπορούσαν να εξαντλήσουν τη μνήμη ή το CPU. Για εργασίες που εξαρτώνται από I/O όπως η μετατροπή αρχείων, η αντιστοίχιση του μεγέθους της πισίνας με τον αριθμό των διαθέσιμων πυρήνων *συν* μερικά επιπλέον νήματα συνήθως αποδίδει τη βέλτιστη απόδοση.

### Πώς η Aspose Διαχειρίζεται τη Μετατροπή  

`Converter.convert` διαβάζει το πηγαίο HTML, το αποδίδει εσωτερικά χρησιμοποιώντας μια μη‑γραφική μηχανή προγράμματος περιήγησης και γράφει ένα αρχείο PDF βάσει των παρεχόμενων `PdfSaveOptions`. Οι προεπιλεγμένες επιλογές παράγουν μια πιστή διάταξη, ενσωματωμένες γραμματοσειρές και διανυσματικά γραφικά—ιδανικό για τα περισσότερα επιχειρηματικά έγγραφα.

---

## ## Αποτελεσματική Μετατροπή Πολλαπλών Αρχείων HTML  

Αν έχετε έναν φάκελο με δεκάδες αρχεία `.html`, μπορείτε να αυτοματοποιήσετε το βήμα ανακάλυψης:

```java
import java.nio.file.*;
import java.util.stream.*;

String directory = "YOUR_DIRECTORY";
String[] inputFiles = Files.walk(Paths.get(directory))
    .filter(p -> p.toString().endsWith(".html"))
    .map(Path::toString)
    .toArray(String[]::new);
```

Αυτό το απόσπασμα διασχίζει το δέντρο καταλόγου, φιλτράρει τις επεκτάσεις `.html` και τροφοδοτεί τον προκύπτοντα πίνακα απευθείας στον βρόχο της πισίνας νημάτων που εμφανίστηκε νωρίτερα. Είναι μια μικρή τροποποίηση, αλλά μετατρέπει μια στατική λίστα σε έναν δυναμικό, έτοιμο‑για‑παραγωγή σαρωτή.

---

## ## Κατάλληλο Τερματισμό του ExecutorService σε Java  

Καλώντας `executor.shutdown()` λέτε στην πισίνα **να μην** δέχεται νέες εργασίες ενώ επιτρέπει στις ήδη‑υποβληθείσες να ολοκληρωθούν. Αν παραλείψετε αυτό το βήμα, η εφαρμογή σας μπορεί να συνεχίσει να τρέχει επ' άπειρον, ειδικά σε ένα εργαλείο γραμμής εντολών.  

Το επακόλουθο `awaitTermination` μπλοκάρει το κύριο νήμα για έως **5 λεπτά** (ρυθμιζόμενο) και επιστρέφει `true` αν όλα ολοκληρωθούν εντός του χρόνου. Αν το χρονικό όριο λήξει, μπορείτε να επιβάλετε βίαιο τερματισμό με `executor.shutdownNow()`, αλλά αυτό θα πρέπει να είναι η τελευταία λύση, επειδή μπορεί να διακόψει ενεργές μετατροπές και να αφήσει μισογράφητα PDFs.

---

## ## Διαχείριση Ακραίων Περιπτώσεων και Συνηθισμένων Παγίδων  

| Situation | What to Watch For | Recommended Fix |
|-----------|-------------------|-----------------|
| **Απουσία αρχείου HTML** | `FileNotFoundException` μέσα στην εργασία | Επαληθεύστε τις διαδρομές πριν την υποβολή ή πιάστε την εξαίρεση (όπως φαίνεται) και καταγράψτε ένα σαφές μήνυμα. |
| **Έλλειψη μνήμης σε μεγάλες σελίδες** | Η Aspose μπορεί να δεσμεύσει πολύ heap για εικόνες υψηλής ανάλυσης | Αυξήστε το heap της JVM (`-Xmx2g`) ή μειώστε την ανάλυση των εικόνων μέσω `PdfSaveOptions.setRasterImagesResolution()`. |
| **Ανησυχίες ασφαλείας νήματος** | Κοινή χρήση ενός μόνο αντικειμένου `Converter` μεταξύ νημάτων | Χρησιμοποιήστε **νέο Converter ανά εργασία** (η στατική μέθοδος `convert` κάνει ακριβώς αυτό). |
| **Μερικά PDFs μετά το χρονικό όριο** | `awaitTermination` επιστρέφει `false` | Σκεφτείτε μεγαλύτερο χρονικό όριο ή μηχανισμό επανάληψης· επίσης καθαρίστε τα ατελή αρχεία. |
| **Σημείο συμφόρησης απόδοσης στο I/O δίσκου** | Όλα τα νήματα προσβάλλουν τον ίδιο HDD | Χρησιμοποιήστε αποθήκευση SSD ή διανείμετε τους φακέλους εξόδου σε διαφορετικούς δίσκους. |

---

## ## Αναμενόμενο Αποτέλεσμα  

Όταν εκτελέσετε το πρόγραμμα (αντικαταστήστε το `YOUR_DIRECTORY` με πραγματική διαδρομή), θα πρέπει να δείτε κάτι σαν:

```
YOUR_DIRECTORY/a.html → PDF conversion completed
YOUR_DIRECTORY/b.html → PDF conversion completed
YOUR_DIRECTORY/c.html → PDF conversion completed
YOUR_DIRECTORY/d.html → PDF conversion completed
All conversions finished successfully.
```

Κάθε αρχείο `.html` θα έχει ένα αδελφό αρχείο `.pdf` στον ίδιο φάκελο. Ανοίξτε οποιοδήποτε από αυτά σε προβολή PDF για να επαληθεύσετε ότι η διάταξη ταιριάζει με το αρχικό HTML.

---

## ## Πλήρες Παράδειγμα Εργασίας (All‑in‑One)  

Αν προτιμάτε ένα μόνο αρχείο που μπορείτε να αντιγράψετε‑επικολλήσετε στο `src/main/java/ParallelConversionDemo.java`, εδώ είναι:

```java
import java.util.concurrent.*;
import java.nio.file.*;
import java.util.stream.*;
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.PdfSaveOptions;

public class ParallelConversionDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a fixed thread pool – change 4 to suit your CPU
        ExecutorService executor = Executors.newFixedThreadPool(4);

        // 2️⃣ Discover all HTML files in the target folder
        String folder = "YOUR_DIRECTORY"; // ← update this
        String[] inputFiles = Files.walk(Paths.get(folder))
                .filter(p -> p.toString().endsWith(".html"))
                .map(Path::toString)
                .toArray(String[]::new);

        // 3️⃣ Submit a conversion job for each file
        for (String htmlPath : inputFiles) {
            executor.submit(() -> {
                try {
                    PdfSaveOptions options = new PdfSaveOptions();
                    String pdfPath = htmlPath.replace(".html", ".pdf");
                    Converter.convert(htmlPath, options, pdfPath);
                    System.out.println(htmlPath + " → PDF conversion completed");
                } catch (Exception ex) {
                    System.err.println("Error converting " + htmlPath);
                    ex.printStackTrace();
                }
            });
        }

        // 4️⃣ Gracefully shut down – wait up to 5 minutes
        executor.shutdown();
        if (!executor.awaitTermination(5, TimeUnit.MINUTES)) {
            System.err.println("Timeout – forcing shutdown");
            executor.shutdownNow();
        } else {
            System.out.println("All conversions finished successfully.");
        }
    }
}
```

Μεταγλώττιση και εκτέλεση:

```bash
javac -cp "libs/*" ParallelConversionDemo.java
java -cp ".:libs/*" ParallelConversionDemo
```

Αντικαταστήστε το `libs/*` με την πραγματική διαδρομή προς τα JAR της Aspose.

---

## ## Επόμενα Βήματα και Σχετικά Θέματα  

- **Βελτιώστε την έξοδο PDF** – εξερευνήστε το `PdfSaveOptions` (συμπίεση, συμμόρφωση PDF/A, υδατογράφημα).  
- **Κλιμάκωση πέρα από ένα μόνο μηχάνημα** – συνδυάστε αυτό το μοτίβο με μια ουρά μηνυμάτων (RabbitMQ, Kafka) για διανομή εργασίας σε ένα σύμπλεγμα.  
- **Ενσωμάτωση με Spring Boot** – εκθέστε ένα REST endpoint που δέχεται φορτίο HTML και επιστρέφει ροή PDF, επαναχρησιμοποιώντας το ίδιο bean της πισίνας νημάτων.  
- **Πειραματισμός με άλλες μορφές Aspose** – η βιβλιοθήκη υποστηρίζει επίσης μετατροπές `DOCX`, `XLSX` και `SVG`, ανοίγοντας δρόμους σε πιο πλούσιες αγωγές εγγράφων.  

---

### TL;DR  

Τώρα έχετε μια δοκιμασμένη συνταγή για **μετατροπή HTML σε PDF** σε Java χρησιμοποιώντας μια **σταθερή πισίνα νημάτων**, διαχειριζόμενοι αποδοτικά **πολλαπλά αρχεία HTML** και κλείνοντας σωστά το **ExecutorService**. Ενσωματώστε τον κώδικα στο δικό σας

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

- [Πώς να Μετατρέψετε HTML σε PDF Java – Χρησιμοποιώντας Aspose.HTML για Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Μετατροπή HTML σε PDF Java – Διαμόρφωση Περιβάλλοντος στο Aspose.HTML](/html/english/java/configuring-environment/)
- [Μετατροπή HTML σε PDF σε Java – Οδηγός Βήμα‑Βήμα με Ρυθμίσεις Μεγέθους Σελίδας](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
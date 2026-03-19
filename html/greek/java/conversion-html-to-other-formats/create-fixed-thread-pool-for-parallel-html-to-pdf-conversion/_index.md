---
category: general
date: 2026-03-18
description: Δημιουργήστε σταθερό σύνολο νημάτων για γρήγορη μετατροπή HTML σε PDF.
  Μάθετε τη μαζική μετατροπή HTML σε PDF, αποθηκεύστε HTML ως PDF και μετατρέψτε πολλαπλά
  αρχεία HTML με το Aspose.HTML.
draft: false
keywords:
- create fixed thread pool
- convert html to pdf
- batch html to pdf
- save html as pdf
- convert multiple html files
language: el
og_description: Δημιουργήστε σταθερό σύνολο νημάτων για αποδοτική μετατροπή HTML σε
  PDF. Αυτός ο οδηγός σας καθοδηγεί στη μαζική μετατροπή HTML σε PDF, στην αποθήκευση
  HTML ως PDF και στη διαχείριση πολλαπλών αρχείων.
og_title: Δημιουργία Στατικού Πισίνας Νημάτων για Παράλληλη Μετατροπή HTML‑σε‑PDF
tags:
- Java
- Multithreading
- Aspose.HTML
- PDF conversion
title: Δημιουργία Σταθερής Πισίνας Νημάτων για Παράλληλη Μετατροπή HTML‑σε‑PDF σε
  Java
url: /el/java/conversion-html-to-other-formats/create-fixed-thread-pool-for-parallel-html-to-pdf-conversion/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Fixed Thread Pool για Παράλληλη Μετατροπή HTML‑σε‑PDF σε Java

Έχετε αναρωτηθεί ποτέ πώς να **δημιουργήσετε fixed thread pool** που μπορεί να **μετατρέπει HTML σε PDF** με αστραπιαία ταχύτητα; Δεν είστε οι μόνοι—οι προγραμματιστές συχνά αντιμετωπίζουν το πρόβλημα όταν ένας φάκελος αναφορών πρέπει να μετατραπεί σε PDF μέσα σε μια νύχτα.  

Το καλό νέο είναι ότι μπορείτε να δημιουργήσετε μια δεξαμενή εργαζομένων νήματος, να παραχωρήσετε κάθε αρχείο HTML στο Aspose.HTML, και να αφήσετε τη JVM να κάνει το σκληρό έργο. Σε αυτό το tutorial θα μετατρέψουμε HTML σε PDF σε παρτίδες, θα αποθηκεύσουμε HTML ως PDF, και θα σας δείξουμε πώς να **μετατρέψετε πολλαπλά αρχεία HTML** χωρίς να κατακλύσετε την CPU.

## Τι Θα Χρειαστείτε

- Java 17 ή νεότερη (ο κώδικας λειτουργεί σε οποιοδήποτε πρόσφατο JDK)  
- Aspose.HTML for Java 23.9 (ή η πιο πρόσφατη έκδοση) – περιλαμβάνει την κλάση `Converter` που θα χρησιμοποιήσουμε  
- Μερικά αρχεία `.html` που θέλετε να μετατρέψετε σε PDF  
- Το αγαπημένο σας IDE ή έναν απλό επεξεργαστή κειμένου  

Αυτό είναι όλο. Δεν απαιτούνται εξωτερικά εργαλεία κατασκευής πέρα από το JAR του Aspose.HTML στο classpath.

## Βήμα 1: Καταγράψτε τα Αρχεία HTML που Θέλετε να Επεξεργαστείτε  

Πρώτα απ’ όλα, χρειάζεστε μια συλλογή αρχείων προέλευσης. Σκεφτείτε το ως τη “λίστα αγορών” για τη δουλειά μετατροπής.

```java
// Step 1 – define the files that will be turned into PDFs
String[] htmlFileNames = {
        "YOUR_DIRECTORY/input1.html",
        "YOUR_DIRECTORY/input2.html",
        "YOUR_DIRECTORY/input3.html",
        "YOUR_DIRECTORY/input4.html"
};
```

Γιατί κρατάμε τη λίστα σε έναν πίνακα; Είναι απλό, type‑safe, και μας επιτρέπει να επαναλάβουμε με έναν καθαρό βρόχο `for‑each` αργότερα. Αν χρειαστεί ποτέ να διαβάσετε τα ονόματα από έναν φάκελο, απλώς αντικαταστήστε τον πίνακα με `Files.list(Paths.get("YOUR_DIRECTORY"))…`.

## Βήμα 2: **Δημιουργία Fixed Thread Pool** Με Μέγεθος Συμφωνικό με την CPU Σας  

Τώρα δημιουργούμε πραγματικά **fixed thread pool**. Το μέγεθος της δεξαμενής ταιριάζει με τον αριθμό των λογικών πυρήνων, κάτι που συνήθως προσφέρει την καλύτερη απόδοση χωρίς να στερεί τους πόρους του λειτουργικού συστήματος.

```java
// Step 2 – spin up a fixed thread pool based on available processors
ExecutorService executor = Executors.newFixedThreadPool(
        Runtime.getRuntime().availableProcessors());
```

*Συμβουλή:* Αν η μετατροπή σας είναι I/O‑bound (διάβασμα μεγάλων αρχείων HTML από δίσκο), μπορείτε να αυξήσετε λίγο το μέγεθος της δεξαμενής. Αλλά για CPU‑intensive rendering, η αντιστοίχηση με τον αριθμό των πυρήνων είναι η ιδανική επιλογή.

![Διάγραμμα ενός fixed thread pool που διαχειρίζεται εργασίες HTML‑σε‑PDF](/images/create-fixed-thread-pool-diagram.png "εικονογράφηση δημιουργίας fixed thread pool")

*Alt text:* διάγραμμα fixed thread pool που δείχνει παράλληλη μετατροπή αρχείων HTML σε PDF.

## Βήμα 3: Υποβάλετε μια **Εργασία Μετατροπής HTML σε PDF** για Κάθε Αρχείο  

Με τη δεξαμενή έτοιμη, παραχωρούμε κάθε διαδρομή HTML σε ένα νήμα εργασίας. Μέσα στο lambda καλούμε το `Converter.convertDocument` του Aspose.HTML, το οποίο κάνει το σκληρό έργο της απόδοσης της σελίδας και της εγγραφής ενός PDF.

```java
// Step 3 – enqueue a conversion job for every HTML file
for (String sourcePath : htmlFileNames) {
    executor.submit(() -> {
        String destinationPath = sourcePath.replace(".html", ".pdf");
        try {
            // Convert HTML to PDF using Aspose.HTML
            Converter.convertDocument(sourcePath, destinationPath, new PdfSaveOptions());
            System.out.println("Converted: " + sourcePath);
        } catch (Exception e) {
            // Wrap checked exceptions to avoid cluttering the lambda
            throw new RuntimeException(e);
        }
    });
}
```

Γιατί τυλίγουμε την εξαίρεση; Τα lambdas δεν μπορούν να ρίξουν ελεγχόμενες εξαιρέσεις χωρίς try‑catch, και η επαναρίψη ως `RuntimeException` κρατά τον κώδικα συνοπτικό ενώ εξακολουθεί να εμφανίζει αποτυχίες στην κονσόλα.

## Βήμα 4: Κλείσιμο της Δεξαμενής με Στοργή και **Μετατροπή Πολλαπλών Αρχείων HTML**  

Αφού όλες οι εργασίες έχουν προγραμματιστεί, λέμε στον εκτελεστή να σταματήσει να δέχεται νέα έργα και περιμένουμε μέχρι να ολοκληρωθεί κάθε νήμα. Αυτός είναι ο καθαρός τρόπος για **batch HTML to PDF** χωρίς να αφήνουμε κρεμασμένα νήματα.

```java
// Step 4 – stop accepting new tasks and wait for completion
executor.shutdown();
executor.awaitTermination(5, TimeUnit.MINUTES);
```

Αν λήξει το χρονικό όριο, το πρόγραμμα θα τερματιστεί με προειδοποίηση—τέλεια για CI pipelines όπου δεν θέλετε μια ασταθή διαδικασία.

## Επαλήθευση του Αποτελέσματος – **Αποθήκευση HTML ως PDF**  

Όταν το πρόγραμμα ολοκληρωθεί, θα πρέπει να δείτε μια σειρά από αρχεία `.pdf` δίπλα στα αρχικά `.html`. Ανοίξτε οποιοδήποτε από αυτά· θα παρατηρήσετε ότι η διάταξη, το CSS και οι εικόνες διατηρούνται—ακριβώς όπως θα περιμένατε όταν **αποθηκεύετε HTML ως PDF** με έναν σύγχρονο renderer.

```text
$ ls YOUR_DIRECTORY
input1.html  input1.pdf  input2.html  input2.pdf  ...
```

Αν λείπει κάποιο PDF, ελέγξτε την έξοδο της κονσόλας για το stack trace της εξαίρεσης. Συνηθισμένα προβλήματα περιλαμβάνουν:

- Έλλειψη γραμματοσειρών στον διακομιστή (το Aspose.HTML θα επιστρέψει μια προεπιλογή, αλλά η εμφάνιση μπορεί να αλλάξει)  
- Σχετικές διαδρομές εικόνων που δεν επιλύονται από τον τρέχοντα φάκελο εργασίας  
- Ανεπαρκής μνήμη για εξαιρετικά μεγάλα HTML (αυξήστε το heap της JVM με `-Xmx2g`)

## Συμβουλές & Τεχνάκια για Πραγματική Χρήση  

| Κατάσταση | Σύσταση |
|-----------|----------|
| **Τεράστια παρτίδα (1000+ αρχεία)** | Χρησιμοποιήστε μια περιορισμένη ουρά (`LinkedBlockingQueue`) και υποβάλετε εργασίες σε τμήματα για να αποφύγετε `OutOfMemoryError`. |
| **Διαφορετικοί φάκελοι εξόδου** | Υπολογίστε το `destinationPath` με `Paths.get(outputDir, filename + ".pdf")`. |
| **Προσαρμοσμένες ρυθμίσεις PDF** | Περάστε ένα ρυθμισμένο `PdfSaveOptions` (π.χ., `setCompress(true)`) αντί της προεπιλογής. |
| **Καταγραφή αντί `System.out`** | Ενσωματώστε SLF4J ή Log4j για logs επιπέδου παραγωγής. |
| **Διαχείριση σφαλμάτων** | Συλλέξτε τα αποτυχημένα αρχεία σε λίστα και ξαναπροσπαθήστε μετά το τέλος της κύριας εκτέλεσης. |

Αυτές οι προσαρμογές σας επιτρέπουν να **μετατρέψετε πολλαπλά αρχεία HTML** αξιόπιστα σε περιβάλλον παραγωγής.

## Πλήρες Παράδειγμα Εργασίας  

Παρακάτω βρίσκεται η πλήρης, έτοιμη‑για‑εκτέλεση κλάση Java. Αντιγράψτε‑και‑επικολλήστε την στο `ParallelBatch.java`, προσθέστε το JAR του Aspose.HTML στο classpath, και τρέξτε `java ParallelBatch`.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.PdfSaveOptions;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.TimeUnit;

public class ParallelBatch {
    public static void main(String[] args) throws Exception {

        // Step 1: List the HTML files to be converted
        String[] htmlFileNames = {
                "YOUR_DIRECTORY/input1.html",
                "YOUR_DIRECTORY/input2.html",
                "YOUR_DIRECTORY/input3.html",
                "YOUR_DIRECTORY/input4.html"
        };

        // Step 2: Create a fixed thread pool sized to the number of CPU cores
        ExecutorService executor = Executors.newFixedThreadPool(
                Runtime.getRuntime().availableProcessors());

        // Step 3: Submit a conversion task for each HTML file
        for (String sourcePath : htmlFileNames) {
            executor.submit(() -> {
                String destinationPath = sourcePath.replace(".html", ".pdf");
                try {
                    // Convert the HTML document to PDF using Aspose.HTML
                    Converter.convertDocument(sourcePath, destinationPath, new PdfSaveOptions());
                    System.out.println("Converted: " + sourcePath);
                } catch (Exception e) {
                    // Wrap any checked exception as an unchecked one for simplicity
                    throw new RuntimeException(e);
                }
            });
        }

        // Step 4: Shut down the pool and wait for all conversions to finish
        executor.shutdown();
        executor.awaitTermination(5, TimeUnit.MINUTES);
    }
}
```

Τρέξτε το και θα δείτε την κονσόλα να επιβεβαιώνει κάθε αρχείο:

```
Converted: YOUR_DIRECTORY/input1.html
Converted: YOUR_DIRECTORY/input2.html
...
```

## Συμπέρασμα  

Σας δείξαμε πώς να **δημιουργήσετε fixed thread pool** σε Java και να το χρησιμοποιήσετε για **παράλληλη μετατροπή HTML σε PDF**. Με το batching της εργασίας, μπορείτε αποδοτικά να **μετατρέψετε πολλαπλά αρχεία HTML**, να κρατήσετε την CPU σας ευχαριστημένη, και να καταλήξετε με ένα τακτοποιημένο σύνολο PDF έτοιμο για διανομή.  

Στη συνέχεια, μπορείτε να εξερευνήσετε πιο προχωρημένα χαρακτηριστικά του Aspose.HTML—όπως ενσωμάτωση γραμματοσειρών, προσθήκη υδατογραφιών, ή συγχώνευση των παραγόμενων PDF σε μια ενιαία αναφορά. Ή, αν σας ενδιαφέρει η κλιμάκωση, αντικαταστήστε το τοπικό thread pool με έναν κατανεμημένο εκτελεστή όπως το ForkJoinPool ή μια cloud‑based ουρά εργασιών.  

Δοκιμάστε το, προσαρμόστε το μέγεθος της δεξαμενής, και αφήστε την εφαρμογή σας να διαχειριστεί το επόμενο βουνό αναφορών HTML χωρίς να ιδρώνει. Καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
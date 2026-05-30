---
category: general
date: 2026-04-23
description: Μάθετε πώς να αποθηκεύετε HTML ως PDF γρήγορα με τη Java. Αυτός ο οδηγός
  δείχνει πώς να μετατρέπετε HTML σε PDF σε παρτίδες χρησιμοποιώντας μια σταθερή ομάδα
  νημάτων και πώς να τερματίζετε με ασφάλεια τον εκτελεστή.
draft: false
keywords:
- save html as pdf
- convert html to pdf
- batch html to pdf
- fixed thread pool java
- shut down executor
language: el
og_description: Μάθετε πώς να αποθηκεύετε HTML ως PDF γρήγορα με τη Java. Αυτός ο
  οδηγός δείχνει πώς να μετατρέπετε HTML σε PDF σε παρτίδες χρησιμοποιώντας μια σταθερή
  ομάδα νημάτων και πώς να τερματίζετε με ασφάλεια τον εκτελεστή.
og_title: Αποθήκευση HTML ως PDF – Παράλληλη Μαζική Μετατροπή με Σταθερό Πισίνα Νημάτων
  Java
tags:
- Java
- multithreading
- PDF conversion
- Aspose.HTML
title: Αποθήκευση HTML ως PDF – Παράλληλη μαζική μετατροπή με χρήση σταθερού pool
  νημάτων σε Java
url: /el/java/conversion-html-to-other-formats/save-html-as-pdf-parallel-batch-conversion-using-fixed-threa/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# αποθήκευση html ως pdf – Παράλληλη Μετατροπή σε Batch με Fixed Thread Pool Java

Κάποτε χρειάστηκε να **αποθηκεύσετε html ως pdf** και διαπιστώσατε ότι η μονονηματική προσέγγιση ήταν εξαιρετικά αργή; Δεν είστε μόνοι—οι προγραμματιστές συχνά «κολλάνται» όταν πρέπει να μετατρέψουν δεκάδες σελίδες η μία μετά την άλλη. Τα καλά νέα είναι ότι μπορείτε να **μετατρέψετε html σε pdf** παράλληλα, αφήνοντας την CPU να κάνει το σκληρό έργο ενώ εσείς πίνετε καφέ.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που **batch html to pdf** χρησιμοποιώντας το `DocumentPool` του Aspose.HTML μαζί με ένα **fixed thread pool java**. Θα δείξουμε επίσης τον σωστό τρόπο **shut down executor** ώστε να μην μένουν «αδέσποτα» νήματα. Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε Maven ή Gradle project και να ξεκινήσετε τη μετατροπή άμεσα.

---

## Τι Θα Χρειαστείτε

- **Java 17** ή νεότερη (ο κώδικας χρησιμοποιεί τη σύγχρονη σύνταξη `var` μόνο για συντομία, αλλά μπορείτε να μείνετε σε Java 8 αν προτιμάτε).  
- **Aspose.HTML for Java** 23.x (ή την πιο πρόσφατη έκδοση) στο classpath σας.  
- Μια σειρά από αρχεία HTML που θέλετε να μετατρέψετε σε PDF.  
- Ένα IDE ή έναν απλό επεξεργαστή κειμένου—δεν απαιτείται τίποτα περίπλοκο.

Καμία εξωτερική υπηρεσία, κανένα κρυφό αρχείο ρυθμίσεων—απλώς καθαρός κώδικας Java που μπορείτε να μεταγλωττίσετε και να τρέξετε σήμερα.

---

## Βήμα 1 – Αποθήκευση HTML ως PDF με Document Pool

Το πρώτο που χρειαζόμαστε είναι μια πισίνα (pool) που παρέχει ένα φρέσκο `Dom.Document` για κάθε νήμα εργασίας. Σκεφτείτε το ως μια επαναχρησιμοποιήσιμη κουζίνα όπου κάθε σεφ παίρνει ένα καθαρό τηγάνι αντί να αγοράζει καινούργιο για κάθε πιάτο.

```java
import com.aspose.html.concurrent.DocumentPool;

// Create a pool that can provide a Document instance for each worker.
DocumentPool documentPool = new DocumentPool(4); // 4 = number of concurrent threads
```

**Γιατί μια πισίνα;**  
Τα αντικείμενα `Dom.Document` είναι σχετικά βαριά· η συνεχής δημιουργία τους μπορεί να περιορίσει την απόδοση. Η πισίνα διατηρεί έναν περιορισμένο αριθμό προ‑αρχικοποιημένων στιγμιοτύπων, μειώνοντας την πίεση στο GC και επιταχύνοντας κάθε εργασία μετατροπής.

> **Συμβουλή:** Ταιριάξτε το μέγεθος της πισίνας με τον αριθμό των νημάτων στον executor. Πάρα πολλά νήματα και η πισίνα γίνεται bottleneck· πολύ λίγα και σπαταλάτε CPU cycles.

---

## Βήμα 2 – Ρύθμιση Fixed Thread Pool Java

Τώρα δημιουργούμε ένα **fixed thread pool java**. Αυτό είναι το «μυαλό» που θα εκτελεί τις εργασίες μετατροπής μας παράλληλα.

```java
import java.util.concurrent.*;

ExecutorService executor = Executors.newFixedThreadPool(4); // 4 threads = 4 parallel conversions
```

Μια σταθερή πισίνα σας δίνει προβλεψιμότητα—ακριβώς τέσσερα νήματα θα τρέχουν ταυτόχρονα, χωρίς ξαφνικές εκρήξεις νημάτων. Επίσης, κάνει πιο εύκολη τη διαχείριση πόρων αργότερα όταν **shut down executor**.

---

## Βήμα 3 – Προετοιμασία Λίστας Batch HTML προς PDF

Πριν αναθέσουμε δουλειά στα νήματα, πρέπει να τους πούμε *τι* θα μετατρέψουν. Εδώ υπάρχει ένας απλός πίνακας, αλλά μπορείτε να διαβάσετε από φάκελο, βάση δεδομένων ή ακόμη και από HTTP endpoint.

```java
String[] htmlFilePaths = {
    "YOUR_DIRECTORY/file1.html", "YOUR_DIRECTORY/file2.html",
    "YOUR_DIRECTORY/file3.html", "YOUR_DIRECTORY/file4.html"
};
```

**Ακραία περίπτωση:** Αν ο φάκελος περιέχει μη‑HTML αρχεία, η μετατροπή θα πετάξει εξαίρεση. Ένα γρήγορο φίλτρο όπως `path.endsWith(".html")` μπορεί να κρατήσει τα πράγματα καθαρά.

---

## Βήμα 4 – Υποβολή Εργασιών Μετατροπής (Convert HTML to PDF)

Για κάθε διαδρομή υποβάλλουμε ένα lambda στον executor. Μέσα στο lambda αποκτούμε ένα `Dom.Document` από την πισίνα, φορτώνουμε το HTML και το αποθηκεύουμε ως PDF.

```java
for (String htmlPath : htmlFilePaths) {
    executor.submit(() -> {
        try (Dom.Document doc = documentPool.acquire()) {
            // Load the source HTML.
            doc.load(htmlPath);

            // Derive the output PDF file name.
            String pdfPath = htmlPath.replace(".html", ".pdf");

            // Save the document as PDF.
            doc.save(pdfPath, com.aspose.html.SaveFormat.PDF);
        } catch (Exception e) {
            // In a tutorial we simply print the stack trace.
            e.printStackTrace();
        }
    });
}
```

**Γιατί χρησιμοποιούμε `try‑with‑resources`;**  
Εγγυάται ότι το `Dom.Document` επιστρέφεται στην πισίνα ακόμη και αν προκύψει εξαίρεση, αποτρέποντας διαρροές που θα μπορούσαν να «πνίξουν» επόμενες εργασίες.

**Συχνή ερώτηση:** *Τι γίνεται αν δύο νήματα προσπαθήσουν να γράψουν στο ίδιο αρχείο PDF;*  
Το σχήμα ονοματοδοσίας μας (`replace(".html", ".pdf")`) εξασφαλίζει αντιστοίχιση ένα‑προς‑ένα, οπότε οι συγκρούσεις αποφεύγονται. Αν χρειάζεστε προσαρμοσμένη στρατηγική ονοματοδοσίας, βεβαιωθείτε ότι είναι thread‑safe.

---

## Βήμα 5 – Κατάλληλο Shut Down Executor

Αφού όλες οι εργασίες έχουν τοποθετηθεί στην ουρά, λέμε στον executor να μην δέχεται νέα έργα και περιμένουμε να ολοκληρωθούν οι σε εξέλιξη μετατροπές.

```java
executor.shutdown();                     // No more tasks will be accepted
executor.awaitTermination(1, TimeUnit.MINUTES); // Wait up to 1 minute
```

Αν ξεχάσετε να **shut down executor**, η εφαρμογή σας μπορεί να «κολλήσει» κατά το κλείσιμο επειδή τα μη‑daemon νήματα παραμένουν ζωντανά. Η κλήση `awaitTermination` προσθέτει ένα δίχτυ ασφαλείας—αν οι μετατροπές διαρκούν περισσότερο από το αναμενόμενο, μπορείτε να καταγράψετε μια προειδοποίηση ή να τις ακυρώσετε.

> **Σημείωση:** Ρυθμίστε το timeout ανάλογα με το μέγεθος των αρχείων HTML. Για μεγάλα έγγραφα, μερικά λεπτά μπορεί να είναι πιο ρεαλιστικά.

---

## Προαιρετικό: Οπτική Επιβεβαίωση (Image)

![Διάγραμμα που δείχνει την παράλληλη γραμμή μετατροπής όπου τα αρχεία HTML τροφοδοτούνται σε ένα fixed thread pool και αποθηκεύονται ως PDF](/images/save-html-as-pdf-pipeline.png "save html as pdf pipeline")

*Η παραπάνω εικονογράφηση αναδεικνύει τη ροή από την είσοδο HTML στην έξοδο PDF χρησιμοποιώντας ένα thread pool.*

---

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το ολοκληρωμένο πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο `ParallelConversionDemo.java`. Συγκεντρώνεται με μία εντολή `javac` (υπόθεση ότι το JAR του Aspose.HTML βρίσκεται στο classpath).

```java
import com.aspose.html.concurrent.DocumentPool;
import com.aspose.html.Dom;
import java.util.concurrent.*;

public class ParallelConversionDemo {
    public static void main(String[] args) throws Exception {

        // Step 1 – Create a pool that can provide a Document instance for each worker.
        DocumentPool documentPool = new DocumentPool(4);

        // Step 2 – Set up a fixed‑size thread pool to run conversions in parallel.
        ExecutorService executor = Executors.newFixedThreadPool(4);

        // Step 3 – List the HTML files that will be turned into PDFs.
        String[] htmlFilePaths = {
            "YOUR_DIRECTORY/file1.html", "YOUR_DIRECTORY/file2.html",
            "YOUR_DIRECTORY/file3.html", "YOUR_DIRECTORY/file4.html"
        };

        // Step 4 – For every HTML file, submit a conversion task to the executor.
        for (String htmlPath : htmlFilePaths) {
            executor.submit(() -> {
                try (Dom.Document doc = documentPool.acquire()) {
                    // Load the source HTML.
                    doc.load(htmlPath);
                    // Derive the output PDF file name.
                    String pdfPath = htmlPath.replace(".html", ".pdf");
                    // Save the document as PDF.
                    doc.save(pdfPath, com.aspose.html.SaveFormat.PDF);
                } catch (Exception e) {
                    // In a tutorial we simply print the stack trace.
                    e.printStackTrace();
                }
            });
        }

        // Step 5 – Shut down the executor and wait for all tasks to finish.
        executor.shutdown();
        executor.awaitTermination(1, TimeUnit.MINUTES);
    }
}
```

**Αναμενόμενη έξοδος:**  
Για κάθε `fileX.html` θα βρείτε το αντίστοιχο `fileX.pdf` στον ίδιο φάκελο. Ανοίξτε οποιοδήποτε PDF με τον αγαπημένο σας προβολέα—οι σελίδες πρέπει να φαίνονται ακριβώς όπως το αρχικό HTML, συμπεριλαμβανομένου του CSS και των εικόνων.

---

## Επίλυση Προβλημάτων & Συμβουλές

| Κατάσταση | Τι να ελέγξετε | Προτεινόμενη λύση |
|-----------|----------------|-------------------|
| **`OutOfMemoryError`** | Το μέγεθος της πισίνας είναι πολύ μεγάλο για τη διαθέσιμη μνήμη heap. | Μειώστε το μέγεθος του `DocumentPool` ή αυξήστε τη σημαία JVM `-Xmx`. |
| **Απουσία εικόνων στο PDF** | Οι σχετικές διαδρομές εικόνων δεν επιλύονται. | Χρησιμοποιήστε `doc.setBaseUrl("file:///YOUR_DIRECTORY/");` πριν το `load`. |
| **Η μετατροπή «κολλάει»** | Ο executor δεν κλείνει. | Βεβαιωθείτε ότι κάθε μπλοκ `submit` επιστρέφει· ελέγξτε για άπειρους βρόχους σε προσαρμοσμένο HTML. |
| **Το PDF είναι κενό** | Το αρχείο HTML δεν βρέθηκε ή είναι κενό. | Επαληθεύστε τις διαδρομές αρχείων· προσθέστε μια γραμμή `System.out.println(htmlPath)` για debugging. |

---

## Συμπέρασμα

Μόλις μάθατε πώς να **save html as pdf** αποδοτικά, μετατρέποντας HTML σε PDF σε μορφή **batch html to pdf**, αξιοποιώντας ένα **fixed thread pool java** και καθαρίζοντας σωστά τον **shut down executor** μετά το τέλος της εργασίας. Το μοτίβο κλιμακώνεται—απλώς αυξήστε το μέγεθος της πισίνας και προσθέστε περισσότερες διαδρομές αρχείων, και η CPU σας θα παραμένει απασχολημένη χωρίς να εξαντλεί τη μνήμη.

Τι θα κάνετε στη συνέχεια; Δοκιμάστε να σαρώνετε έναν φάκελο αυτόματα (`Files.list(Paths.get("YOUR_DIRECTORY"))`) για να αυτοματοποιήσετε την ανακάλυψη, ή πειραματιστείτε με `PdfSaveOptions` για να ρυθμίσετε συμπίεση και μεταδεδομένα. Μπορείτε επίσης να ενσωματώσετε αυτή τη λογική σε ένα Spring Boot REST endpoint, μετατρέποντας την υπηρεσία σας σε API on‑demand HTML‑to‑PDF.

Αλλάξτε τον κώδικα, προσθέστε logging, ή αντικαταστήστε το Aspose.HTML με άλλη βιβλιοθήκη—η βασική ιδέα παραμένει η ίδια: αποκτήστε ένα επαναχρησιμοποιήσιμο έγγραφο, εκτελέστε μετατροπές παράλληλα και πάντα καθαρίστε τον executor. Καλή προγραμματιστική δουλειά και απολαύστε την αύξηση ταχύτητας!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
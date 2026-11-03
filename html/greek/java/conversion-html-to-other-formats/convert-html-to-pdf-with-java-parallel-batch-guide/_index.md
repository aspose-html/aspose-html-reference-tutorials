---
category: general
date: 2026-06-07
description: Μετατρέψτε HTML σε PDF χρησιμοποιώντας το ExecutorService της Java. Μάθετε
  πώς να μετατρέπετε μαζικά αρχεία HTML, να αποθηκεύετε έγγραφο HTML ως PDF και να
  τερματίζετε το ExecutorService ομαλά.
draft: false
keywords:
- convert html to pdf
- save html document as pdf
- shutdown executorservice gracefully
- batch convert html to pdf
language: el
og_description: Μετατρέψτε HTML σε PDF χρησιμοποιώντας το ExecutorService της Java.
  Διαχειριστείτε τη μαζική μετατροπή, αποθηκεύοντας το έγγραφο HTML ως PDF, και πραγματοποιήστε
  ομαλό τερματισμό του ExecutorService.
og_title: Μετατροπή HTML σε PDF με Java – Οδηγός Παράλληλης Παρτίδας
schemas:
- author: Aspose
  dateModified: '2026-06-07'
  description: Convert HTML to PDF using Java's ExecutorService. Learn how to batch
    convert HTML files, save HTML document as PDF, and shutdown ExecutorService gracefully.
  headline: Convert HTML to PDF with Java – Parallel Batch Guide
  type: TechArticle
- description: Convert HTML to PDF using Java's ExecutorService. Learn how to batch
    convert HTML files, save HTML document as PDF, and shutdown ExecutorService gracefully.
  name: Convert HTML to PDF with Java – Parallel Batch Guide
  steps:
  - name: The HTML file is read into a string.
    text: The HTML file is read into a string.
  - name: '`PdfRendererBuilder` parses the markup, applies CSS, and streams the result
      to a PDF file.'
    text: '`PdfRendererBuilder` parses the markup, applies CSS, and streams the result
      to a PDF file.'
  - name: Any `IOException` bubbles up to `convertAndSave`, where we log success or
      failure.
    text: Any `IOException` bubbles up to `convertAndSave`, where we log success or
      failure.
  type: HowTo
tags:
- Java
- Concurrency
- PDF Generation
title: Μετατροπή HTML σε PDF με Java – Οδηγός Παράλληλης Επεξεργασίας σε Παρτίδες
url: /el/java/conversion-html-to-other-formats/convert-html-to-pdf-with-java-parallel-batch-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή HTML σε PDF με Java – Οδηγός Παράλληλης Επεξεργασίας σε Batch

Κάποτε χρειάστηκε να **μετατρέψετε HTML σε PDF** αλλά νιώσατε κολλημένοι με δεκάδες αρχεία; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν δημιουργούν γεννήτριες αναφορών ή εξαγωγείς τιμολογίων. Τα καλά νέα; Με λίγες γραμμές Java και μια έξυπνη ομάδα νημάτων, μπορείτε να **μετατρέψετε HTML σε PDF σε batch** σε ελάχιστο χρόνο, **αποθηκεύοντας το έγγραφο HTML ως PDF**, και ακόμη **να τερματίσετε το ExecutorService με χάρη** όταν ολοκληρωθεί η εργασία.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα. Θα δείτε γιατί ένα fixed‑size thread pool είναι η ιδανική λύση για παράλληλη μετατροπή, πώς φαίνεται ο κώδικας μετατροπής, και τα ακριβή βήματα για καθαρό τερματισμό του executor. Στο τέλος, θα έχετε ένα αυτόνομο πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε project—χωρίς ελλείψεις, χωρίς ασαφείς «δείτε τα docs» συνδέσμους.

---

## Τι Θα Κατασκευάσετε

- Μια εφαρμογή Java console που διαβάζει μια λίστα τοπικών αρχείων HTML.  
- Κάθε αρχείο παραδίδεται σε ένα νήμα εργασίας που δημιουργεί μια έκδοση PDF.  
- Η εφαρμογή χρησιμοποιεί **ExecutorService** για να εκτελεί τις μετατροπές παράλληλα.  
- Μόλις όλες οι εργασίες προγραμματιστούν, η ομάδα **τερματίζεται με χάρη**, εξασφαλίζοντας ότι δεν μένει κανένα νήμα κρεμασμένο.

**Προαπαιτούμενα**  
- Java 17 (ή οποιοδήποτε πρόσφατο JDK).  
- Μια βιβλιοθήκη PDF που μπορεί να αποδώσει HTML, όπως **OpenHTMLtoPDF**, **iText**, ή **Flying Saucer**. Στον κώδικα θα αναφερθούμε σε μια placeholder κλάση `HTMLDocument`; αντικαταστήστε την με το API της βιβλιοθήκης σας.  
- Βασικές γνώσεις σύγχρονης Java (τίποτα περίπλοκο).

---

![Διάγραμμα που δείχνει τη batch μετατροπή αρχείων HTML σε PDF χρησιμοποιώντας ExecutorService](batch-convert-diagram.png "Μετατροπή HTML σε PDF παράλληλα με ExecutorService")

*Alt text: Διάγραμμα που απεικονίζει πώς να μετατρέψετε HTML σε PDF χρησιμοποιώντας μια ομάδα νημάτων για επεξεργασία batch.*

---

## Μετατροπή HTML σε PDF σε Παράλληλο (Batch Convert HTML to PDF)

Όταν έχετε δεκάδες—ή και χιλιάδες—αρχεία HTML, η μετατροπή τους ένα‑ένα στο κύριο νήμα γίνεται bottleneck. Ένα fixed‑size thread pool επιτρέπει στη JVM να επαναχρησιμοποιεί έναν καθορισμένο αριθμό νημάτων εργασίας, διατηρώντας υψηλή χρήση CPU χωρίς να υπερφορτώνει το σύστημα.

```java
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

/**
 * Simple demo that batch converts HTML files to PDF using a fixed thread pool.
 * Replace HTMLDocument with the actual class from your chosen PDF library.
 */
public class HtmlToPdfBatch {

    public static void main(String[] args) {
        // 1️⃣ Prepare a list of HTML files to convert
        List<String> htmlPaths = List.of(
            "src/main/resources/page1.html",
            "src/main/resources/page2.html",
            "src/main/resources/page3.html"
        );

        // 2️⃣ Create a fixed‑size thread pool – 4 workers is a good starting point
        ExecutorService pool = Executors.newFixedThreadPool(4);

        // 3️⃣ Submit a conversion task for each HTML file
        for (String htmlPath : htmlPaths) {
            pool.submit(() -> convertAndSave(htmlPath));
        }

        // 4️⃣ Shutdown ExecutorService gracefully – no new tasks, wait for running ones
        shutdownGracefully(pool);
    }

    /**
     * Core conversion logic – this is where we **save HTML document as PDF**.
     */
    private static void convertAndSave(String htmlPath) {
        try {
            // Imagine HTMLDocument is from OpenHTMLtoPDF, iText, etc.
            HTMLDocument doc = new HTMLDocument(htmlPath);
            String pdfPath = htmlPath.replace(".html", ".pdf");
            doc.save(pdfPath);
            System.out.println("✅ Converted: " + htmlPath + " → " + pdfPath);
        } catch (Exception e) {
            System.err.println("❌ Failed to convert " + htmlPath + ": " + e.getMessage());
        }
    }

    /**
     * Helper that **shutdowns ExecutorService gracefully**.
     */
    private static void shutdownGracefully(ExecutorService executor) {
        executor.shutdown(); // stop accepting new tasks
        try {
            // Wait a maximum of 60 seconds for existing tasks to finish
            if (!executor.awaitTermination(60, java.util.concurrent.TimeUnit.SECONDS)) {
                System.err.println("⚠️ Pool didn’t terminate in time – forcing shutdown");
                executor.shutdownNow(); // cancel currently executing tasks
            } else {
                System.out.println("🛑 All tasks completed – executor shut down cleanly.");
            }
        } catch (InterruptedException ie) {
            // Preserve interrupt status & force shutdown
            Thread.currentThread().interrupt();
            executor.shutdownNow();
        }
    }
}
```

### Γιατί Λειτουργεί Αυτό

- **Parallelism**: Κάθε κλήση `submit` παραδίδει τη μετατροπή σε ένα νήμα εργασίας, έτσι τέσσερα αρχεία μπορούν να επεξεργαστούν ταυτόχρονα σε μηχάνημα τετραπύρηνο.  
- **Isolation**: Η μέθοδος `convertAndSave` περιέχει όλη τη λογική που χρειάζεται για **αποθήκευση του εγγράφου HTML ως PDF**, καθιστώντας εύκολη την αντικατάσταση της υποκείμενης βιβλιοθήκης αργότερα.  
- **Graceful termination**: Καλώντας πρώτα το `shutdown()` λέμε στην ομάδα «δεν υπάρχει άλλη δουλειά, παρακαλώ ολοκληρώστε ό,τι έχετε». Ο βρόχος `awaitTermination` δίνει στα νήματα την ευκαιρία να τελειώσουν, και μόνο αν είναι επίμονα καλούμε το `shutdownNow()`. Αυτό το pattern είναι η προτεινόμενη μέθοδος για **shutdown ExecutorService gracefully**.

---

## Αποθήκευση Εγγράφου HTML ως PDF – Κύρια Λογική Μετατροπής

Η καρδιά κάθε ροής **convert HTML to PDF** είναι η βιβλιοθήκη μετατροπής. Ενώ το παράδειγμα χρησιμοποιεί ένα ψεύτικο `HTMLDocument`, εδώ είναι μια γρήγορη ματιά στο πώς θα το κάνατε με **OpenHTMLtoPDF**:

```java
import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;

public class HTMLDocument {
    private final String htmlPath;

    public HTMLDocument(String htmlPath) {
        this.htmlPath = htmlPath;
    }

    public void save(String pdfPath) throws IOException {
        try (OutputStream os = new FileOutputStream(pdfPath);
             InputStream is = new FileInputStream(htmlPath)) {

            PdfRendererBuilder builder = new PdfRendererBuilder();
            builder.withHtmlContent(new String(is.readAllBytes()), null);
            builder.toStream(os);
            builder.run();
        }
    }
}
```

**Τι συμβαίνει;**  
1. Το αρχείο HTML διαβάζεται σε μια συμβολοσειρά.  
2. Ο `PdfRendererBuilder` αναλύει το markup, εφαρμόζει CSS, και στέλνει το αποτέλεσμα σε αρχείο PDF.  
3. Οποιοδήποτε `IOException` προωθείται στην `convertAndSave`, όπου καταγράφουμε επιτυχία ή αποτυχία.

Αισθανθείτε ελεύθεροι να αντικαταστήσετε αυτό το απόσπασμα με το `HtmlConverter.convertToPdf` του iText ή το `ITextRenderer` του Flying Saucer. Ο κώδικας του thread‑pool παραμένει ακριβώς ο ίδιος, γι' αυτό τόνισα τη **save HTML document as PDF** ως ξεχωριστό ζήτημα.

---

## Τερματισμός ExecutorService με Χάρη – Καλές Πρακτικές

Ένα κοινό λάθος είναι να καλέσετε `shutdownNow()` αμέσως μετά την υποβολή των εργασιών. Αυτό διακόπτει ξαφνικά τα νήματα, αφήνοντας ενδεχομένως μισογράψιμα αρχεία PDF στο δίσκο. Το pattern που χρησιμοποιούμε—`shutdown()` → `awaitTermination()` → προαιρετικό `shutdownNow()`—εξασφαλίζει:

- **Καμία νέα εργασία** δεν γίνεται αποδεκτή μετά την προγραμματισμένη ουρά.  
- **Οι τρέχουσες εργασίες** έχουν την ευκαιρία να ολοκληρωθούν καθαρά.  
- **Τα μπλοκαρισμένα νήματα** διακόπτονται μόνο αν υπερβούν ένα λογικό όριο χρόνου (εδώ, 60 δευτερόλεπτα).  

Αν αναμένετε πολύ μεγάλα PDF ή αργή μηχανή απόδοσης, αυξήστε το timeout ή χρησιμοποιήστε `executor.invokeAll(tasks, timeout, unit)` για πιο ακριβή έλεγχο.

---

## Πλήρες Παράδειγμα Λειτουργίας (Όλα τα Τμήματα Μαζί)

Παρακάτω είναι ολόκληρο το πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε ένα αρχείο `HtmlToPdfBatch.java`. Απλώς προσθέστε την εξάρτηση OpenHTMLtoPDF (ή την προτιμώμενη βιβλιοθήκη) στο `pom.xml` ή στο Gradle build, και είστε έτοιμοι.



## Τι Θα Μάθετε Στη Σύντομη Μελλοντική Σας

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην δική σας υλοποίηση.

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Convert HTML to PDF Java – Configuring Environment in Aspose.HTML](/html/english/java/configuring-environment/)
- [Convert HTML to PDF in Java – Step‑by‑Step Guide with Page Size Settings](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-05-28
description: πώς να χρησιμοποιήσετε τον executor στη Java με σταθερό pool νημάτων,
  να εξάγετε κείμενο από HTML και να επιταχύνετε την επεξεργασία – ένα πλήρες παράδειγμα
  thread pool σε Java.
draft: false
keywords:
- how to use executor
- fixed thread pool java
- extract text from html
- java thread pool example
- create fixed thread pool
language: el
og_description: πώς να χρησιμοποιήσετε τον executor στη Java με σταθερό pool νημάτων.
  Μάθετε ένα πλήρες παράδειγμα pool νημάτων Java που εξάγει κείμενο από αρχεία HTML
  αποδοτικά.
og_title: Πώς να χρησιμοποιήσετε τον Executor στη Java – Οδηγός για Σταθερό Πισίνα
  Νημάτων
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: how to use executor in Java with a fixed thread pool, extract text
    from HTML and speed up processing – a complete java thread pool example.
  headline: How to Use Executor in Java – Fixed Thread Pool Guide
  type: TechArticle
tags:
- Java
- Concurrency
- HTML Parsing
title: Πώς να χρησιμοποιήσετε τον Executor στη Java – Οδηγός για Σταθερή Πισίνα Νημάτων
url: /el/java/advanced-usage/how-to-use-executor-in-java-fixed-thread-pool-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε τον Executor στη Java – Οδηγός Σταθερού Thread Pool

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε τον executor** για να εκτελέσετε πολλές εργασίες ταυτόχρονα χωρίς να εξαντλήσετε τη μνήμη σας; Δεν είστε μόνοι. Σε πολλές πραγματικές εφαρμογές θα χρειαστεί να σαρώσετε έναν φάκελο με αρχεία HTML, να εξάγετε το κείμενο του σώματος, και να το κάνετε γρήγορα — ακριβώς το σενάριο που λύνει αυτό το tutorial.

Θα περάσουμε βήμα‑βήμα από μια υλοποίηση **fixed thread pool java** που εξάγει κείμενο από HTML, εκτυπώνει τον αριθμό χαρακτήρων κάθε αρχείου και κλείνει ομαλά. Στο τέλος θα έχετε ένα αυτόνομο **java thread pool example** που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο, καθώς και μερικές συμβουλές για την προσαρμογή του μεγέθους της πισίνας και τη διαχείριση ειδικών περιπτώσεων.

> **Τι θα χρειαστείτε**  
> * Java 17 (ή οποιοδήποτε πρόσφατο JDK)  
> * Μια μικρή βιβλιοθήκη ανάλυσης HTML – θα χρησιμοποιήσουμε το *jsoup* επειδή είναι δοκιμασμένη και δεν απαιτεί ρυθμίσεις.  
> * Μια μικρή δόση δείγματος *.html* αρχείων σε έναν φάκελο της επιλογής σας.

---

## Πώς να Χρησιμοποιήσετε τον Executor με Σταθερό Thread Pool

Η καρδιά κάθε προγράμματος Java με έντονη ταυτόχρονη εκτέλεση είναι το `ExecutorService`. Δημιουργώντας ένα **fixed thread pool** λέμε στη JVM να διατηρεί ακριβώς N νήματα εργασίας ενεργά, κάτι που αποτρέπει το κόστος δημιουργίας νημάτων και περιορίζει τη χρήση πόρων.

```java
// Step 1: Build a fixed‑size thread pool (4 workers in this case)
ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Γιατί είναι σημαντικό:*  
Αν δημιουργούσατε ένα νέο `Thread` για κάθε αρχείο HTML, το λειτουργικό σύστημα θα έπρεπε να προγραμματίσει δεκάδες νήματα σε ένα μέτριο laptop, οδηγώντας σε υπερβολικές εναλλαγές περιεχομένου. Μια σταθερή πισίνα επαναχρησιμοποιεί τα ίδια τέσσερα νήματα, παρέχοντάς σας προβλέψιμη χρήση CPU.

---

## Ορισμός των Αρχείων HTML για Επεξεργασία – Fixed Thread Pool Java

Στη συνέχεια παραθέτουμε τα αρχεία που θέλουμε να τροφοδοτήσουμε στην πισίνα. Σε μια πραγματική εφαρμογή πιθανόν να περιηγηθείτε σε ένα δέντρο καταλόγων· εδώ το κρατάμε απλό.

```java
// Step 2: List the HTML documents you want to parse
List<String> htmlFilePaths = List.of(
        "YOUR_DIRECTORY/a.html",
        "YOUR_DIRECTORY/b.html",
        "YOUR_DIRECTORY/c.html",
        "YOUR_DIRECTORY/d.html"
);
```

*Συμβουλή:* `List.of` επιστρέφει μια αμετάβλητη λίστα, η οποία είναι ασφαλής για κοινή χρήση μεταξύ νημάτων χωρίς πρόσθετη συγχρονισμό.

## Υποβολή Ξεχωριστής Εργασίας για Κάθε Αρχείο HTML

Τώρα παραδίδουμε κάθε διαδρομή στον executor. Η lambda που υποβάλλουμε θα εκτελείται **παράλληλα** σε ένα από τα τέσσερα νήματα εργασίας.

```java
// Step 3: Dispatch a parsing job for every file
for (String htmlFilePath : htmlFilePaths) {
    executor.submit(() -> {
        // Each lambda runs on a thread from the pool
        try {
            // Step 4: Open the document, extract its text, and display the length
            String text = extractBodyText(htmlFilePath);
            System.out.println(htmlFilePath + " → " + text.length() + " chars");
        } catch (IOException e) {
            System.err.println("Failed to read " + htmlFilePath);
            e.printStackTrace();
        }
    });
}
```

**Γιατί τυλίγουμε τη λογική σε μια μέθοδο** (`extractBodyText`) θα γίνει σαφές στην επόμενη ενότητα — κρατά τη lambda καθαρή και μας επιτρέπει να επαναχρησιμοποιήσουμε τον κώδικα εξαγωγής αλλού.

## Εξαγωγή Κειμένου από HTML – Η Κεντρική Λογική

Αυτή είναι η επαναχρησιμοποιήσιμη βοηθητική μέθοδος που στην πραγματικότητα **εξάγει κείμενο από html** χρησιμοποιώντας το Jsoup. Ανοίγει το αρχείο, αναλύει το DOM και επιστρέφει το απλό κείμενο του σώματος.

```java
/**
 * Reads an HTML file and returns the plain text inside the <body>.
 *
 * @param path absolute or relative path to the .html file
 * @return body text without tags
 * @throws IOException if the file cannot be read
 */
private static String extractBodyText(String path) throws IOException {
    // Jsoup parses the file into a Document object.
    org.jsoup.nodes.Document doc = org.jsoup.Jsoup.parse(new java.io.File(path), "UTF-8");
    // getBody() gives us the <body> element; text() strips all tags.
    return doc.body().text();
}
```

*Γιατί Jsoup;* Είναι ελαφρύ, διαχειρίζεται κακοδιατυπωμένο markup με χάρη, και δεν απαιτεί πλήρες κινητήρα προγράμματος περιήγησης. Η μέθοδος ρίχνει `IOException` ώστε ο καλών να αποφασίσει πώς να το καταγράψει ή να ανακάμψει — ιδανικό για σενάριο thread‑pool όπου δεν θέλετε ένα μόνο κακό αρχείο να τερματίσει ολόκληρο τον executor.

## Καθαρό Κλείσιμο του Executor – Δημιουργία Σταθερού Thread Pool

Αφού έχουμε υποβάλει όλες τις εργασίες, πρέπει να πούμε στην πισίνα να σταματήσει να δέχεται νέα έργα και να ολοκληρώσει όσα είναι ήδη στην ουρά.

```java
// Step 5: Initiate an orderly shutdown once all tasks are queued
executor.shutdown();
try {
    // Wait up to 30 seconds for all tasks to finish
    if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
        System.err.println("Timed out waiting for tasks; forcing shutdown.");
        executor.shutdownNow();
    }
} catch (InterruptedException ie) {
    // Preserve interrupt status and force shutdown
    Thread.currentThread().interrupt();
    executor.shutdownNow();
}
```

*Εξήγηση:* `shutdown()` αποτρέπει νέες υποβολές, ενώ το `awaitTermination` μπλοκάρει μέχρι να τελειώσουν όλες οι εργασίες ανάλυσης (ή λήξει το χρονικό όριο). Αν κάτι κολλήσει, το `shutdownNow()` προσπαθεί να ακυρώσει τις τρέχουσες εργασίες. Αυτό το μοτίβο είναι ο προτεινόμενος τρόπος για **create fixed thread pool** με ασφάλεια.

## Πλήρες, Εκτελέσιμο Παράδειγμα

Συνδυάζοντας όλα, εδώ είναι ένα μοναδικό αρχείο που μπορείτε να μεταγλωττίσετε και να εκτελέσετε. Περιλαμβάνει τις απαραίτητες εισαγωγές, τη μέθοδο `main` και τη βοηθητική λειτουργία που περιγράφηκε παραπάνω.

```java
import java.io.IOException;
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

/**
 * Demonstrates how to use executor with a fixed thread pool to
 * extract text from multiple HTML files concurrently.
 */
public class HtmlThreadPoolDemo {

    public static void main(String[] args) {
        // 1️⃣ Build a fixed‑size pool (adjust the size for your hardware)
        ExecutorService executor = Executors.newFixedThreadPool(4);

        // 2️⃣ Define the files we want to process
        List<String> htmlFilePaths = List.of(
                "YOUR_DIRECTORY/a.html",
                "YOUR_DIRECTORY/b.html",
                "YOUR_DIRECTORY/c.html",
                "YOUR_DIRECTORY/d.html"
        );

        // 3️⃣ Submit a parsing task for each file
        for (String htmlFilePath : htmlFilePaths) {
            executor.submit(() -> {
                try {
                    String text = extractBodyText(htmlFilePath);
                    System.out.println(htmlFilePath + " → " + text.length() + " chars");
                } catch (IOException e) {
                    System.err.println("Error processing " + htmlFilePath);
                    e.printStackTrace();
                }
            });
        }

        // 5️⃣ Shut down the pool cleanly
        executor.shutdown();
        try {
            if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
                System.err.println("Tasks took too long; forcing shutdown.");
                executor.shutdownNow();
            }
        } catch (InterruptedException ie) {
            Thread.currentThread().interrupt();
            executor.shutdownNow();
        }
    }

    /**
     * Reads an HTML file and returns the plain text inside the <body>.
     *
     * @param path path to the .html file
     * @return body text without markup
     * @throws IOException if file cannot be read
     */
    private static String extractBodyText(String path) throws IOException {
        Document doc = Jsoup.parse(new java.io.File(path), "UTF-8");
        return doc.body().text();
    }
}
```

**Αναμενόμενη έξοδος** (υποθέτοντας ότι κάθε αρχείο περιέχει περίπου 1 200 χαρακτήρες κειμένου σώματος):

```
YOUR_DIRECTORY/a.html → 1234 chars
YOUR_DIRECTORY/b.html → 1198 chars
YOUR_DIRECTORY/c.html → 1305 chars
YOUR_DIRECTORY/d.html → 1120 chars
```

Αν κάποιο αρχείο λείπει ή είναι κακοδιατυπωμένο, θα δείτε ένα stack trace να εκτυπώνεται στο `stderr`, αλλά οι άλλες εργασίες θα συνεχίσουν αδιάσπαστες — ακριβώς αυτό που πρέπει να κάνει ένα σωστά λειτουργικό **java thread pool example**.

## Συχνές Ερωτήσεις & Ειδικές Περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| *Τι γίνεται αν έχω περισσότερα από τέσσερα αρχεία;* | Η πισίνα θα τοποθετήσει στην ουρά τις επιπλέον εργασίες και θα τις εκτελέσει μόλις ελευθερωθεί ένα νήμα. Δεν απαιτείται επιπλέον κώδικας. |
| *Θα πρέπει να χρησιμοποιήσω `newCachedThreadPool` αντί αυτού;* | `newCachedThreadPool` δημιουργεί νήματα κατ' απαίτηση και μπορεί να αυξηθεί απεριόριστα, κάτι που είναι επικίνδυνο για εργασίες βαριές σε I/O. Ένα **fixed thread pool** σας δίνει προβλέψιμη χρήση μνήμης και CPU. |
| *Πώς μπορώ να αλλάξω το μέγεθος της πισίνας βάσει των πυρήνων CPU;* | `int cores = Runtime.getRuntime().availableProcessors(); ExecutorService exec = Executors.newFixedThreadPool(cores);` είναι ένα κοινό μοτίβο. |
| *Τι γίνεται αν η ανάλυση αποτύχει για ένα αρχείο;* | Το `catch (IOException e)` μέσα στη lambda απομονώνει την αποτυχία, το καταγράφει, και αφήνει την υπόλοιπη πισίνα να συνεχίσει τη δουλειά. |
| *Μπορώ να επιστρέψω το εξαγόμενο κείμενο στον καλούντα;* | Ναι — χρησιμοποιήστε `Future<String>` αντί για `submit(Runnable)`. Ο κώδικας θα ήταν `Future<String> f = executor.submit(() -> extractBodyText(path));` και αργότερα `String result = f.get();`. |

## Συμπέρασμα

Καλύψαμε **πώς να χρησιμοποιήσετε τον executor** για να δημιουργήσετε ένα **fixed thread pool java** που επεξεργάζεται μια συλλογή αρχείων HTML παράλληλα, εξάγει το κείμενο του σώματος και αναφέρει τον αριθμό χαρακτήρων. Το πλήρες **java thread pool example** δείχνει σωστή διαχείριση πόρων, διαχείριση σφαλμάτων και μια επαναχρησιμοποιήσιμη μέθοδο εξαγωγής.

Επόμενα βήματα; Δοκιμάστε να αντικαταστήσετε την υλοποίηση `extractBodyText` με έναν πιο εξελιγμένο scraper, πειραματιστείτε με μεγαλύτερο μέγεθος πισίνας, ή τροφοδοτήστε τα αποτελέσματα σε μια βάση δεδομένων. Μπορείτε επίσης να εξερευνήσετε το `CompletionService` για να λαμβάνετε τα αποτελέσματα μόλις είναι έτοιμα, κάτι χρήσιμο όταν τα μεγέθη των αρχείων διαφέρουν πολύ.

Μη διστάσετε να τροποποιήσετε τη διαδρομή του καταλόγου, να προσθέσετε περισσότερα αρχεία ή να ενσωματώσετε αυτό το απόσπασμα σε ένα μεγαλύτερο πλαίσιο crawling. Το βασικό μοτίβο — δημιουργία πισίνας, υποβολή ανεξάρτητων εργασιών και καθαρό κλείσιμο — παραμένει το ίδιο, όποια και αν είναι η πολυπλοκότητα του φορτίου εργασίας.

Καλή προγραμματιστική, και εύχομαι τα νήματά σας να παραμένουν πάντα ενεργά (μέχρι να τα κλείσετε, φυσικά)!

## Σχετικά Μαθήματα

- [Fixed thread pool java – Παράλληλος Καθαρισμός HTML με ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [Πώς να Ερωτήσετε HTML στη Java – Πλήρες Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Πώς να Χρησιμοποιήσετε το Aspose.HTML για Java - Κατορθώνοντας τη Σχεδίαση Canvas HTML5](/html/english/java/html5-canvas-rendering/html5-canvas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
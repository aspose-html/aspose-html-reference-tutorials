---
category: general
date: 2026-04-05
description: Μάθημα Java πολυνηματισμού που δείχνει πώς να εκτελείτε εργασίες παράλληλα
  χρησιμοποιώντας μια σταθερή ομάδα νημάτων στην Java και να τερματίζετε το ExecutorService
  με ασφάλεια.
draft: false
keywords:
- java multithreading tutorial
- fixed thread pool java
- shutdown executorservice
- print thread name
- run tasks parallel
language: el
og_description: Μάθημα Java multithreading που σας καθοδηγεί στη εκτέλεση εργασιών
  παράλληλα, τη δημιουργία σταθερού pool νημάτων Java, την εκτύπωση του ονόματος του
  νήματος και τον καθαρό τερματισμό του ExecutorService.
og_title: Εκπαιδευτικό Java για πολυνηματισμό – Παράλληλη εκτέλεση με σταθερό σύνολο
  νημάτων
tags:
- Java
- Concurrency
- ExecutorService
title: 'Εκμάθηση πολυνηματισμού Java: Εκτέλεση εργασιών παράλληλα με σταθερό Thread
  Pool'
url: /el/java/advanced-usage/java-multithreading-tutorial-run-tasks-parallel-with-fixed-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java multithreading tutorial – Parallel Execution Made Simple

Έχετε αναρωτηθεί ποτέ πώς να **τρέξετε εργασίες παράλληλα** στη Java χωρίς να βυθιστείτε στη διαχείριση χαμηλού επιπέδου νήματος; Σε αυτό το **java multithreading tutorial** θα σας δείξουμε ακριβώς αυτό: χρήση **fixed thread pool java**, εκτύπωση του ονόματος κάθε νήματος, και καθαρό **shutdown executorservice** όταν ολοκληρωθεί η εργασία.  

Αν έχετε γράψει ποτέ έναν βρόχο που μπλοκάρει σε δικτυακή I/O ή χρειάζεστε να «σκάψετε» πολλές ιστοσελίδες ταυτόχρονα, το μοτίβο που καλύπτουμε παρακάτω θα σας εξοικονομήσει χρόνο και κόπο.  

Θα καλύψουμε όλα όσα χρειάζεστε — χωρίς εξωτερικά έγγραφα, μόνο καθαρός κώδικας Java που μπορείτε να αντιγράψετε‑επικολλήσετε, να τρέξετε και να δείτε τα αποτελέσματα. Στο τέλος θα καταλάβετε γιατί ένα fixed thread pool είναι συχνά η ιδανική λύση για περιορισμένο παράλληλο φόρτο, πώς να το τερματίσετε με ασφάλεια, και πώς να κάνετε τα logs πιο αναγνώσιμα εκτυπώνοντας το όνομα του νήματος.  

> **Prerequisites**: Java 8+ (το πακέτο `java.util.concurrent` είναι σταθερό εδώ και χρόνια), ένα IDE ή απλή γραμμή εντολών `javac`/`java`, και μια βασική κατανόηση του OOP. Δεν απαιτούνται πρόσθετες βιβλιοθήκες πέρα από το Aspose HTML for Java jar που ήδη έχετε.

---

![java multithreading tutorial diagram showing a thread pool feeding tasks](https://example.com/images/java-multithreading-tutorial.png "java multithreading tutorial diagram")

## java multithreading tutorial – Set Up a Fixed Thread Pool

Ένα **fixed thread pool** περιορίζει τον αριθμό των νήματων που εκτελούνται ταυτόχρονα, αποτρέποντας την εφαρμογή σας από το να δημιουργεί υπερβολικά πολλά νήματα OS και να εξαντλεί πόρους. Εδώ δημιουργούμε μια ομάδα με τέσσερις εργάτες:

```java
import java.util.concurrent.*;

public class ParallelProcessingTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Γιατί τέσσερα;* Συμφωνεί με τον αριθμό των URL που θα φέρουμε, αλλά μπορείτε να ρυθμίσετε αυτόν τον αριθμό βάσει των πυρήνων CPU, της έντασης I/O ή των περιορισμών μνήμης. Η εργοστασιακή μέθοδος `Executors` σας προστατεύει από τον χαμηλού επιπέδου κατασκευαστή `Thread` και σας δίνει μια καθαρή αναφορά `ExecutorService` που θα **shutdown executorservice** αργότερα.

## Prepare URLs and Define Parallel Tasks

Στη συνέχεια, παραθέτουμε τις σελίδες που θέλουμε να επεξεργαστούμε. Σε έναν πραγματικό scraper πιθανότατα θα διαβάζατε αυτά από αρχείο ή βάση δεδομένων, αλλά ένας στατικός πίνακας κρατά το παράδειγμα αυτό αυτόνομο:

```java
        // Step 2: List the web pages to process
        String[] pageUrls = {
            "https://example.com/a.html",
            "https://example.com/b.html",
            "https://example.com/c.html",
            "https://example.com/d.html"
        };
```

Τώρα έρχεται το μέρος **run tasks parallel**. Για κάθε URL υποβάλλουμε ένα lambda που φορτώνει το έγγραφο και εκτυπώνει τον τίτλο του. Παρατηρήστε τη χρήση του `Thread.currentThread().getName()` — αυτό είναι το **print thread name** τρικ που κάνει το debugging πολύ πιο εύκολο:

```java
        // Step 3: Submit a task for each URL that loads the document and prints its title
        for (String url : pageUrls) {
            executor.submit(() -> {
                try (HTMLDocument doc = new HTMLDocument(url)) {
                    String title = doc.getTitle();
                    // Print the thread name alongside the title
                    System.out.println(Thread.currentThread().getName() + " – " + title);
                } catch (Exception e) {
                    System.err.println(Thread.currentThread().getName() + " failed: " + e.getMessage());
                }
            });
        }
```

> **Pro tip**: Η περιτύλιξη του `HTMLDocument` σε μπλοκ `try‑with‑resources` εγγυάται ότι το υποκείμενο stream κλείνει, ακόμη και αν η σελίδα αποτύχει να φορτωθεί.

## Gracefully Shutdown the ExecutorService

Αφήνοντας μια ομάδα νήματος ζωντανή μετά το τέλος της εργασίας μπορεί να κρατήσει το JVM σας κρεμασμένο. Ο σωστός τρόπος είναι να **shutdown executorservice**, μετά να περιμένετε το τερματισμό:

```java
        // Step 4: Shut down the pool and wait for all tasks to finish
        executor.shutdown();                         // No new tasks will be accepted
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            // Force shutdown if tasks exceed the timeout
            executor.shutdownNow();
        }
    }
}
```

*Γιατί το timeout;* Προστατεύει από μια ακατάσχετη εργασία που δεν επιστρέφει ποτέ (π.χ. κλήση δικτύου που κρέμεται). Αν η ομάδα δεν ολοκληρωθεί σε ένα λεπτό, καλούμε `shutdownNow()` για να διακόψουμε τυχόν εναπομείναντα νήματα.

### Expected Output

Η εκτέλεση του προγράμματος εκτυπώνει κάτι παρόμοιο με:

```
pool-1-thread-1 – Example A
pool-1-thread-3 – Example C
pool-1-thread-2 – Example B
pool-1-thread-4 – Example D
```

Η ακριβής σειρά μπορεί να διαφέρει — αφού οι εργασίες είναι πραγματικά παράλληλες. Αυτό που παραμένει σταθερό είναι το πρόθεμα **print thread name**, που σας λέει ακριβώς ποιος εργάτης χειρίστηκε κάθε URL.

---

## Common Variations & Edge Cases

| Situation | What to Change | Reason |
|-----------|----------------|--------|
| **More URLs than threads** | Keep the same pool size; extra tasks will queue automatically. | Η fixed pool διαχειρίζεται το back‑pressure για εσάς. |
| **CPU‑bound work** | Set the pool size to `Runtime.getRuntime().availableProcessors()` instead of a hard‑coded 4. | Μεγιστοποιεί τη χρήση CPU χωρίς υπερβολική υπερφόρτωση. |
| **Need to cancel a specific task** | Keep a `Future<?>` reference from `executor.submit()` and call `future.cancel(true)`. | Παρέχει λεπτομερή έλεγχο πάνω σε μεμονωμένες εργασίες. |
| **Processing large files** | Increase the pool size modestly *or* switch to `newCachedThreadPool()` if you expect bursts. | Οι cached pools δημιουργούν νήματα κατά απαίτηση, αλλά προσέξτε την απεριόριστη ανάπτυξη. |

---

## Conclusion

Τώρα έχετε ένα στέρεο **java multithreading tutorial** που δείχνει πώς να **run tasks parallel** χρησιμοποιώντας ένα **fixed thread pool java**, **print thread name** για καθαρό logging, και **shutdown executorservice** με ασφάλεια. Ο πλήρης, εκτελέσιμος κώδικας βρίσκεται σε μία κλάση, ώστε να τον ενσωματώσετε σε οποιοδήποτε έργο και να ξεκινήσετε αμέσως την κλιμάκωση της I/O‑bound εργασίας σας.

Τι ακολουθεί; Δοκιμάστε να αντικαταστήσετε το `HTMLDocument` με τον δικό σας HTTP client, πειραματιστείτε με διαφορετικά μεγέθη ομάδας, ή ενσωματώστε ένα `CompletionService` για να συλλέγετε αποτελέσματα καθώς ολοκληρώνονται. Μπορείτε επίσης να εξερευνήσετε το `java.util.concurrent.Flow` για reactive streams αν χρειάζεστε διαχείριση back‑pressure πέρα από μια απλή ουρά.

Καλή προγραμματιστική, και θυμηθείτε: με τη σωστή στρατηγική thread‑pool, η ταυτόχρονη εκτέλεση γίνεται *κομμάτι κέικ*, όχι πηγή σφαλμάτων. Αν έχετε ερωτήσεις, αφήστε ένα σχόλιο — είμαι πάντα διαθέσιμος για συζήτηση σχετικά με τη σύγχρονη Java concurrency!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
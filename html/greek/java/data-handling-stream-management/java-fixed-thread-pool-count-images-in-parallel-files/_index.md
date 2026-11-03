---
category: general
date: 2026-02-10
description: Μάθετε πώς να χρησιμοποιείτε ένα σταθερό thread pool Java για να μετράτε
  εικόνες σε αρχεία HTML, να εκτελείτε εργασίες ταυτόχρονα σε Java και να τερματίζετε
  σωστά την υπηρεσία εκτελεστή.
draft: false
keywords:
- java fixed thread pool
- how to count images
- shutdown executor service
- java parallel file processing
- run tasks concurrently java
language: el
og_description: Κατακτήστε τη χρήση του σταθερού thread pool της Java για να μετρήσετε
  εικόνες, να επεξεργάζεστε αρχεία παράλληλα και να τερματίζετε με ασφάλεια την υπηρεσία
  εκτελεστή.
og_title: 'java fixed thread pool: Καταμέτρηση εικόνων σε παράλληλα αρχεία'
tags:
- Java
- Concurrency
- Aspose.HTML
title: 'java fixed thread pool: Καταμέτρηση εικόνων σε παράλληλα αρχεία'
url: /el/java/data-handling-stream-management/java-fixed-thread-pool-count-images-in-parallel-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java fixed thread pool – Παράλληλο Εγχειρίδιο Καταμέτρησης Εικόνων

Έχετε αναρωτηθεί ποτέ πώς να **java fixed thread pool** μέσα από δεκάδες αρχεία HTML και να πάρετε γρήγορη καταμέτρηση εικόνων; Ίσως έχετε κοιτάξει έναν κατάλογο σελίδων, σκεφτείτε “Πρέπει να ξέρω πόσες ετικέτες `<img>` έχει κάθε αρχείο”, και μετά συνειδητοποιήσετε ότι ένας βρόχος μονό-νήματος θα διαρκούσε για πάντα.  

Τα καλά νέα είναι ότι δεν χρειάζεται να γράψετε έναν προσαρμοσμένο διαχειριστή νημάτων ή να παλέψετε με low‑level `Thread` objects. Σε αυτόν τον οδηγό θα σας δείξουμε ακριβώς **how to count images** χρησιμοποιώντας ένα *java fixed thread pool*, **run tasks concurrently java**, και με χάρη **shutdown executor service** όταν ολοκληρωθεί η εργασία.  

Θα καλύψουμε τα πάντα, από τη ρύθμιση της δεξαμενής, την προετοιμασία της λίστας αρχείων, την υποβολή παράλληλων εργασιών, τη διαχείριση ειδικών περιπτώσεων, μέχρι την επαλήθευση του αποτελέσματος. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση πρόγραμμα που δείχνει **java parallel file processing** με καθαρό, συντηρήσιμο τρόπο.  

## Προαπαιτούμενα

- Java 17 ή νεότερη (ο κώδικας χρησιμοποιεί τη λέξη-κλειδί `var` για συντομία, αλλά μπορείτε να κάνετε υποβάθμιση αν χρειαστεί).
- Aspose.HTML for Java στο classpath σας – μπορείτε να το κατεβάσετε από το Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

- Μερικά αρχεία HTML που θέλετε να αναλύσετε (το tutorial υποθέτει ότι βρίσκονται στο `YOUR_DIRECTORY/`).
- Ένα IDE ή εργαλείο κατασκευής με το οποίο είστε άνετοι – IntelliJ IDEA, VS Code, ή απλώς `javac` λειτουργεί καλά.

Αυτό είναι όλο. Χωρίς επιπλέον διακομιστές, χωρίς Docker, μόνο απλή Java και μια μικρή βιβλιοθήκη τρίτου.

## Βήμα 1: Δημιουργία java fixed thread pool

Ένα *java fixed thread pool* σας παρέχει ένα περιορισμένο σύνολο εργατικών νημάτων που επαναχρησιμοποιούν τον εαυτό τους για κάθε υποβαλλόμενη εργασία. Αυτό αποτρέπει το κόστος δημιουργίας νέων νημάτων συνεχώς και περιορίζει το επίπεδο ταυτόχρονης εκτέλεσης, κάτι που είναι κρίσιμο όταν διαβάζετε αρχεία από το δίσκο.

```java
import java.util.concurrent.*;

public class ParallelImageCounter {
    // A pool of 4 threads – adjust based on your CPU cores and I/O profile
    private static final ExecutorService executor = Executors.newFixedThreadPool(4);
}
```

**Why 4?** Αν έχετε ένα quad‑core laptop, τέσσερα νήματα κρατούν κάθε πυρήνα απασχολημένο χωρίς υπερβολική κατανομή. Σε διακομιστή με περισσότερους πυρήνες μπορείτε να αυξήσετε τον αριθμό, αλλά θυμηθείτε ότι κάθε νήμα θα ανοίγει ένα file handle, οπότε πολλά μπορεί να εξαντλήσουν τα όρια του OS.

## Βήμα 2: Καταγραφή των αρχείων HTML που θέλετε να αναλύσετε

Το επόμενο κομμάτι του **java parallel file processing** είναι απλώς η δημιουργία ενός πίνακα (ή `List`) διαδρομών αρχείων. Σε ένα πραγματικό έργο μπορεί να περιηγηθείτε σε έναν φάκελο αναδρομικά, να φιλτράρετε κατά επέκταση, ή να διαβάσετε διαδρομές από μια βάση δεδομένων. Εδώ είναι η απλή προσέγγιση:

```java
String[] htmlFiles = {
    "YOUR_DIRECTORY/a.html",
    "YOUR_DIRECTORY/b.html",
    "YOUR_DIRECTORY/c.html",
    "YOUR_DIRECTORY/d.html"
};
```

Αν χρειάζεται να διαχειριστείτε ένα δυναμικό σύνολο, αντικαταστήστε τον στατικό πίνακα με κάτι όπως:

```java
Path dir = Paths.get("YOUR_DIRECTORY");
String[] htmlFiles = Files.list(dir)
                         .filter(p -> p.toString().endsWith(".html"))
                         .map(Path::toString)
                         .toArray(String[]::new);
```

Αυτό το απόσπασμα δείχνει **java parallel file processing** για οποιονδήποτε αριθμό αρχείων χωρίς να αλλάξει το υπόλοιπο του κώδικα.

## Βήμα 3: Υποβολή εργασιών στο **run tasks concurrently java**

Τώρα έρχεται η καρδιά του tutorial – θα **run tasks concurrently java** υποβάλλοντας ένα lambda για κάθε αρχείο. Κάθε εργασία φορτώνει το HTML έγγραφο με Aspose.HTML, ερωτά όλα τα στοιχεία `<img>` και εκτυπώνει την καταμέτρηση.

```java
import com.aspose.html.HTMLDocument;

public static void main(String[] args) throws InterruptedException {
    for (String filePath : htmlFiles) {
        executor.submit(() -> {
            // Load the document – Aspose.HTML does the heavy lifting
            HTMLDocument document = new HTMLDocument(filePath);
            // querySelectorAll returns a NodeList; its length is the image count
            int imageCount = document.querySelectorAll("img").length;
            System.out.println(filePath + " contains " + imageCount + " images.");
        });
    }

    // Step 4 is next – gracefully shut down the pool
    shutdownAndAwaitTermination();
}
```

**Why use a lambda?** Κρατά τον κώδικα σύντομο και αποφεύγει τη δημιουργία ξεχωριστής κλάσης `Runnable`. Το lambda συλλαμβάνει το `filePath` αυτόματα, έτσι κάθε εργασία λειτουργεί στο δικό της αρχείο.

### Πώς να **count images** αποδοτικά

Το Aspose.HTML αναλύει το αρχείο μία φορά, δημιουργεί ένα DOM, και μετά το `querySelectorAll("img")` εκτελείται σε O(n) όπου *n* είναι ο αριθμός των κόμβων. Για τις περισσότερες σελίδες HTML αυτό είναι αμελητέο. Αν χρειάζεστε μια πιο γρήγορη, μόνο streaming προσέγγιση (π.χ., για αρχεία μεγέθους gigabyte), θα μπορούσατε να μεταβείτε σε έναν SAX parser, αλλά αυτό θα θυσίαζε την απλότητα που επιδιώκουμε.

## Βήμα 4: Κατάλληλο **shutdown executor service**

Μην ξεχνάτε ποτέ να κλείσετε την δεξαμενή, αλλιώς η JVM σας θα τρέχει για πάντα. Το παρακάτω μοτίβο είναι ο συνιστώμενος τρόπος για **shutdown executor service** ενώ περιμένετε όλες οι εργασίες να ολοκληρωθούν:

```java
private static void shutdownAndAwaitTermination() {
    executor.shutdown(); // Disable new tasks from being submitted
    try {
        // Wait a while for existing tasks to terminate
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            executor.shutdownNow(); // Cancel currently executing tasks
            // Wait a second for tasks to respond to being cancelled
            if (!executor.awaitTermination(30, TimeUnit.SECONDS))
                System.err.println("Pool did not terminate");
        }
    } catch (InterruptedException ie) {
        // (Re-)Cancel if current thread also interrupted
        executor.shutdownNow();
        // Preserve interrupt status
        Thread.currentThread().interrupt();
    }
}
```

**What if a task hangs?** Η κλήση `shutdownNow()` προσπαθεί να διακόψει τα τρέχοντα νήματα. Αν η λογική καταμέτρησης εικόνων σέβεται την διακοπή (που το Aspose.HTML δεν μπλοκάρει στο I/O), η δεξαμενή θα τερματιστεί καθαρά. Αυτό το μοτίβο είναι το χρυσό πρότυπο για οποιαδήποτε χρήση **java fixed thread pool**.

## Βήμα 5: Επαλήθευση του αποτελέσματος

Εκτελέστε το πρόγραμμα από το IDE σας ή μέσω της γραμμής εντολών:

```bash
javac -cp "path/to/aspose-html.jar" ParallelImageCounter.java
java -cp ".:path/to/aspose-html.jar" ParallelImageCounter
```

Η τυπική έξοδος μοιάζει με:

```
YOUR_DIRECTORY/a.html contains 5 images.
YOUR_DIRECTORY/b.html contains 0 images.
YOUR_DIRECTORY/c.html contains 12 images.
YOUR_DIRECTORY/d.html contains 3 images.
```

Αν δείτε τις καταμετρήσεις εκτυπωμένες με οποιαδήποτε σειρά, είναι αναμενόμενο – τα νήματα ολοκληρώνουν σε διαφορετικούς χρόνους. Το σημαντικό είναι ότι κάθε αρχείο λογίζεται και το πρόγραμμα κλείνει καθαρά μετά τη σειρά τερματισμού.

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```java
import com.aspose.html.HTMLDocument;
import java.util.concurrent.*;

public class ParallelImageCounter {
    // 1️⃣ Fixed thread pool – change size based on your hardware
    private static final ExecutorService executor = Executors.newFixedThreadPool(4);

    public static void main(String[] args) throws InterruptedException {
        // 2️⃣ List of HTML files – replace with your own directory
        String[] htmlFiles = {
            "YOUR_DIRECTORY/a.html",
            "YOUR_DIRECTORY/b.html",
            "YOUR_DIRECTORY/c.html",
            "YOUR_DIRECTORY/d.html"
        };

        // 3️⃣ Submit a counting task for each file
        for (String filePath : htmlFiles) {
            executor.submit(() -> {
                HTMLDocument document = new HTMLDocument(filePath);
                int imageCount = document.querySelectorAll("img").length;
                System.out.println(filePath + " contains " + imageCount + " images.");
            });
        }

        // 4️⃣ Gracefully shut down the pool
        shutdownAndAwaitTermination();
    }

    // 5️⃣ Helper method to cleanly stop the executor
    private static void shutdownAndAwaitTermination() {
        executor.shutdown(); // Disable new tasks
        try {
            if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
                executor.shutdownNow(); // Cancel currently executing tasks
                if (!executor.awaitTermination(30, TimeUnit.SECONDS))
                    System.err.println("Pool did not terminate");
            }
        } catch (InterruptedException ie) {
            executor.shutdownNow();
            Thread.currentThread().interrupt();
        }
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Η εκτέλεση του αποσπάσματος εκτυπώνει κάθε διαδρομή αρχείου ακολουθούμενη από τον αριθμό των ετικετών `<img>` που περιέχει, μετά η JVM τερματίζει. Χωρίς παραμένοντα νήματα, χωρίς διαρροές μνήμης.

## Συνηθισμένα Πιθανά Προβλήματα & Επαγγελματικές Συμβουλές

- **Pitfall:** Χρήση του `newCachedThreadPool()` αντί για *fixed* pool. Αυτό δημιουργεί απεριόριστα νήματα, που μπορούν να εξαντλήσουν τα file descriptors σε μεγάλες παρτίδες. Μείνετε με `newFixedThreadPool`.
- **Pro tip:** Αν τα HTML αρχεία σας είναι τεράστια, σκεφτείτε να αυξήσετε το heap (`-Xmx2g`) ή να μεταβείτε σε streaming parser. Για τις περισσότερες σελίδες marketing, το προεπιλεγμένο heap είναι εντάξει.
- **Pitfall:** Ξεχάσμα κλήσης `shutdown()` – η εφαρμογή σας θα κρέμεται μετά την εκτύπωση των αποτελεσμάτων. Η μέθοδος `shutdownAndAwaitTermination` παραπάνω το διαχειρίζεται αξιόπιστα.
- **Pro tip:** Καταγράψτε την ώρα έναρξης και λήξης κάθε εργασίας αν χρειάζεστε μετρικές απόδοσης. Απλό `System.nanoTime()` πριν και μετά την κατασκευή του `HTMLDocument` σας λέει πόσο διάστημα πήρε η ανάλυση.
- **Pitfall:** Σκληρή κωδικοποίηση του αριθμού νημάτων. Χρησιμοποιήστε `Runtime.getRuntime().availableProcessors()` για να επιλέξετε ένα λογικό προεπιλεγμένο:

```java
int cores = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(cores);
```

## Σχετικά Θέματα που Μπορείτε να Εξερευνήσετε Στη Σειρά

- **run tasks concurrently java** με `CompletableFuture` για πιο εκφραστικούς αγωγούς.
- Αποθήκευση των καταμετρήσεων εικόνων σε βάση δεδομένων για πίνακες ελέγχου analytics.
- Χρήση του **java parallel file processing** με το API `java.nio.file.Files.walk` σε συνδυασμό με streams.
- Υλοποίηση ενός προσαρμοσμένου `ThreadFactory` για να δώσετε στα νήματα σημασιολογικά ονόματα (βοηθά στον εντοπισμό σφαλμάτων).

## Συμπέρασμα

Μόλις περάσαμε από ένα πλήρες, αυτόνομο παράδειγμα που δείχνει πώς ένα **java fixed thread pool** μπορεί να αξιοποιηθεί για **how to count images** σε πολλαπλά αρχεία HTML, ενώ παράλληλα δείχνει τον σωστό τρόπο για **shutdown executor service**. Το μοτίβο κλιμακώνεται καλά—αντικαταστήστε τον πίνακα αρχείων με μια δυναμική λίστα, αυξήστε το μέγεθος της δεξαμενής, και έχετε μια αξιόπιστη λύση για οποιοδήποτε φορτίο **java parallel file processing**.  

Δοκιμάστε το, ρυθμίστε τον αριθμό νημάτων, και ίσως προσθέσετε εξαγωγή CSV των αποτελεσμάτων. Ο ουρανός είναι το όριο όταν συνδυάζετε μια ισχυρή βάση ταυτόχρονης εκτέλεσης με μια χρήσιμη βιβλιοθήκη όπως το Aspose.HTML. Καλή προγραμματιστική!  

![java fixed thread pool diagram](image.png){alt="διάγραμμα java fixed thread pool"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
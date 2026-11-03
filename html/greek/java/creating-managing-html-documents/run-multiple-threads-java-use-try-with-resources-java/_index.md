---
category: general
date: 2026-04-09
description: Τρέξτε πολλαπλά νήματα Java αποδοτικά χρησιμοποιώντας try‑with‑resources
  Java. Μάθετε πώς να φορτώνετε με ασφάλεια ένα έγγραφο HTML Java και να αποφεύγετε
  προβλήματα ταυτόχρονης εκτέλεσης Java.
draft: false
keywords:
- run multiple threads java
- use try with resources java
- load html document java
- avoid concurrency issues java
language: el
og_description: εκτελέστε πολλαπλά νήματα java με try‑with‑resources java. Αυτό το
  tutorial δείχνει πώς να φορτώσετε ένα έγγραφο html java με ασφάλεια, αποφεύγοντας
  προβλήματα ταυτόχρονης πρόσβασης java.
og_title: Εκτέλεση πολλαπλών νημάτων Java – οδηγός Try With Resources
tags:
- java
- multithreading
- html-parsing
title: εκτέλεση πολλαπλών νημάτων java – χρήση try‑with‑resources java
url: /el/java/creating-managing-html-documents/run-multiple-threads-java-use-try-with-resources-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# εκτέλεση πολλαπλών νημάτων java – χρήση try‑with‑resources java

Έχετε αναρωτηθεί ποτέ πώς να **run multiple threads java** χωρίς να παρεμβαίνετε το ένα στο άλλο; Δεν είστε ο μόνος—οι περισσότεροι προγραμματιστές συναντούν το ίδιο πρόβλημα όταν προσπαθούν να μοιραστούν ένα μεταβλητό αντικείμενο μεταξύ νημάτων. Τα καλά νέα; Υπάρχει ένας καθαρός, σύγχρονος τρόπος να το κάνετε, και ξεκινά με τη δήλωση `try‑with‑resources`.

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο για αντιγραφή‑και‑επικόλληση παράδειγμα που **loads an HTML document java**, δημιουργεί αρκετά νήματα και εγγυάται ότι κάθε νήμα εργάζεται με τη δική του παρουσία του εγγράφου. Στο τέλος θα δείτε επίσης πώς να **avoid concurrency issues java** ώστε η εφαρμογή σας να παραμένει σταθερή υπό φόρτο.

> **Τι θα πάρετε:** ένα εκτελέσιμο πρόγραμμα Java, εξηγήσεις βήμα‑βήμα, συμβουλές για πραγματικά έργα και ένα γρήγορο τεστ που μπορείτε να τρέξετε αμέσως.

---

![εικονογράφηση εκτέλεσης πολλαπλών νημάτων java](run-multiple-threads-java.png "Διάγραμμα που δείχνει πολλαπλά νήματα, το καθένα κρατά ένα ξεχωριστό στιγμιότυπο HTMLDocument instance")

## Προαπαιτούμενα

- Java 17 ή νεότερη (η σύνταξη `try‑with‑resources` λειτουργεί το ίδιο μέχρι τη Java 7, αλλά θα χρησιμοποιήσουμε πρόσφατα χαρακτηριστικά της γλώσσας για συντομία).  
- Μια μικρή βοηθητική κλάση ανάλυσης HTML που ονομάζεται `HTMLDocument`. Αν δεν την έχετε, μπορείτε να τη δημιουργήσετε όπως φαίνεται παρακάτω.  
- Βασικές γνώσεις για νήματα (`java.lang.Thread`) και τη διεπαφή `Runnable`.

Αν κάποιο από αυτά σας φαίνεται άγνωστο, μην πανικοβληθείτε—κάθε έννοια θα επανεξεταστεί στα επόμενα βήματα.

---

## Βήμα 1: Φόρτωση HTML document java με κοινή αναφορά

Το πρώτο που χρειαζόμαστε είναι μια *κοινή* αναφορά που δείχνει στο αρχείο που θέλουμε να αναλύσουμε. Σκεφτείτε το ως ένα σχέδιο: το URL είναι το ίδιο για κάθε νήμα, αλλά το πραγματικό αντικείμενο εγγράφου θα δημιουργηθεί ανά νήμα αργότερα.

```java
// Step 1: Load the source HTML document (shared reference for its URL)
HTMLDocument sharedDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");
```

### Γιατί κοινή αναφορά;

Αν προσπαθήσετε να δώσετε σε κάθε νήμα την ίδια παρουσία `HTMLDocument`, όλα θα διαβάζουν και θα γράφουν στα ίδια εσωτερικά buffers. Αυτό είναι κλασική συνταγή για race conditions—ακριβώς το είδος των **concurrency issues java** που προσπαθούμε να αποφύγουμε. Κρατώντας μόνο το *URL* κοινό, κάθε νήμα μπορεί με ασφάλεια να ανοίξει το δικό του stream αργότερα.

> **Pro tip:** Αποθηκεύστε το URL σε μια μεταβλητή `final` αν δεν σκοπεύετε ποτέ να το αλλάξετε. Ο μεταγλωττιστής θα το θεωρήσει σταθερά, μειώνοντας περαιτέρω τυχαίες μεταβολές.

---

## Βήμα 2: Δημιουργία thread‑safe εργασίας χρησιμοποιώντας try with resources java

Τώρα ορίζουμε τι κάνει πραγματικά κάθε νήμα. Το κόλπο είναι να τυλίξουμε τη δημιουργία του `HTMLDocument` ανά νήμα μέσα σε ένα μπλοκ `try‑with‑resources`. Αυτό εγγυάται ότι το έγγραφο κλείνει αυτόματα, ακόμη και αν εξαπλωθεί μια εξαίρεση.

```java
// Step 2: Define a task that creates its own document instance per thread
Runnable task = () -> {
    // Each thread works with its own copy to avoid concurrency issues
    try (HTMLDocument threadDoc = new HTMLDocument(sharedDoc.getUrl())) {
        // Perform thread‑specific operations on threadDoc here
        System.out.println("Thread " + Thread.currentThread().getName()
                + " loaded: " + threadDoc.getTitle());
    } catch (Exception e) {
        System.err.println("Error in thread " + Thread.currentThread().getName()
                + ": " + e.getMessage());
    }
};
```

### Πώς βοηθά το `try‑with‑resources`

Η κλάση `HTMLDocument` υλοποιεί το `java.lang.AutoCloseable`. Όταν το μπλοκ `try` ολοκληρωθεί, η JVM καλεί αυτόματα το `threadDoc.close()`. Αυτό είναι πολύ πιο ασφαλές από μια χειροκίνητη εντολή `finally` και εξαλείφει τον κίνδυνο να ξεχάσετε να ελευθερώσετε εγγενείς πόρους—κάτι που μπορεί εύκολα να οδηγήσει σε διαρροές μνήμης σε μακροχρόνιες πολυνηματικές εφαρμογές.

---

## Βήμα 3: Εκκίνηση νημάτων και αποφυγή concurrency issues java

Με την εργασία έτοιμη, μπορούμε να δημιουργήσουμε όσα νήματα θέλουμε. Για επίδειξη, θα ξεκινήσουμε δύο, αλλά δεν υπάρχει κάτι που να σας εμποδίζει να δημιουργήσετε μια ομάδα νημάτων με δεκάδες εργαζόμενους.

```java
// Step 3: Launch multiple threads that execute the same task
Thread t1 = new Thread(task, "Worker‑1");
Thread t2 = new Thread(task, "Worker‑2");

// Start the threads
t1.start();
t2.start();

// Optional: wait for them to finish (join) if you need deterministic ordering
t1.join();
t2.join();
```

### Γιατί να μην χρησιμοποιήσουμε `ExecutorService`;

Σε κώδικα παραγωγής πιθανότατα **θα** χρησιμοποιήσετε ένα `ExecutorService` για τη διαχείριση μιας ομάδας εργατών. Το απλό παράδειγμα με `Thread` κρατά το tutorial εστιασμένο στην κεντρική ιδέα—δημιουργία ξεχωριστού εγγράφου ανά νήμα ενώ χρησιμοποιείται το `try‑with‑resources`. Μπορείτε ελεύθερα να αντικαταστήσετε τις κλήσεις `Thread` με ένα `FixedThreadPool` αν αυτό ταιριάζει στην αρχιτεκτονική του έργου σας.

---

## Πλήρες, εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα, εδώ είναι ένα αυτόνομο πρόγραμμα που μπορείτε να τοποθετήσετε σε ένα αρχείο με όνομα `MultiThreadHtmlDemo.java`. Περιλαμβάνει μια ελάχιστη υλοποίηση stub για το `HTMLDocument` ώστε να μπορείτε να το μεταγλωττίσετε και να το τρέξετε αμέσως.

```java
// MultiThreadHtmlDemo.java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;

// --- Minimal stub for demonstration purposes ---
class HTMLDocument implements AutoCloseable {
    private final String url;
    private String content;

    public HTMLDocument(String url) throws IOException {
        this.url = url;
        // Simulate loading the file (replace with real parser in production)
        this.content = Files.readString(Path.of(url));
    }

    public String getUrl() {
        return url;
    }

    public String getTitle() {
        // Very naive title extraction – just for demo
        int start = content.indexOf("<title>");
        int end = content.indexOf("</title>");
        if (start != -1 && end != -1 && end > start) {
            return content.substring(start + 7, end).trim();
        }
        return "Untitled";
    }

    @Override
    public void close() {
        // In a real library you’d release native buffers here
        content = null;
        System.out.println("Closed document for URL: " + url);
    }
}

// --- Main class that runs multiple threads java ---
public class MultiThreadHtmlDemo {
    public static void main(String[] args) throws InterruptedException, IOException {
        // Step 1: Load the source HTML document (shared reference for its URL)
        HTMLDocument sharedDoc = new HTMLDocument("sample.html");

        // Step 2: Define a task that creates its own document instance per thread
        Runnable task = () -> {
            try (HTMLDocument threadDoc = new HTMLDocument(sharedDoc.getUrl())) {
                System.out.println("Thread " + Thread.currentThread().getName()
                        + " loaded title: " + threadDoc.getTitle());
            } catch (Exception e) {
                System.err.println("Error in thread " + Thread.currentThread().getName()
                        + ": " + e.getMessage());
            }
        };

        // Step 3: Launch multiple threads that execute the same task
        Thread t1 = new Thread(task, "Worker‑1");
        Thread t2 = new Thread(task, "Worker‑2");

        t1.start();
        t2.start();

        // Wait for both threads to finish
        t1.join();
        t2.join();

        System.out.println("All threads completed.");
    }
}
```

#### Αναμενόμενη έξοδος (υποθέτοντας ότι το `sample.html` περιέχει `<title>Hello World</title>`)

```
Thread Worker-1 loaded title: Hello World
Closed document for URL: sample.html
Thread Worker-2 loaded title: Hello World
Closed document for URL: sample.html
All threads completed.
```

Παρατηρήστε πώς κάθε νήμα εκτυπώνει τον δικό του *loaded title* και στη συνέχεια η μέθοδος `close()` εκτελείται αυτόματα—ακριβώς αυτό που υπόσχεται το `try‑with‑resources`.

---

## Συχνές ερωτήσεις & διαχείριση edge‑case

**Τι γίνεται αν το αρχείο δεν βρεθεί;**  
Ο κατασκευαστής ρίχνει `IOException`. Στο παράδειγμα το πιάσαμε μέσα στο `Runnable` και καταγράψαμε το σφάλμα, ώστε ένα ελλιπές αρχείο να μην καταρρεύσει ολόκληρη η εφαρμογή.

**Μπορώ να επαναχρησιμοποιήσω την ίδια παρουσία `HTMLDocument` μεταξύ νημάτων;**  
Μόνο αν η κλάση είναι ρητά τεκμηριωμένη ως thread‑safe. Οι περισσότεροι αναλυτές διατηρούν μεταβλητή κατάσταση (π.χ., δέντρα DOM), οπότε η κοινή χρήση μιας παρουσίας συνήθως οδηγεί σε **concurrency issues java**. Το μοτίβο που παρουσιάζεται εδώ—μία παρουσία ανά νήμα—είναι η ασφαλέστερη προεπιλογή.

**Πρέπει να συγχρονίσω κάτι;**  
Όχι. Επειδή κάθε νήμα εργάζεται με τη δική του `HTMLDocument`, δεν υπάρχει κοινή μεταβλητή κατάσταση που να χρειάζεται προστασία. Το μόνο κοινό στοιχείο είναι η συμβολοσειρά URL, η οποία είναι αμετάβλητη.

**Πώς θα έμοιαζε αυτό με `ExecutorService`;**  

```java
ExecutorService executor = Executors.newFixedThreadPool(4);
for (int i = 0; i < 4; i++) {
    executor.submit(task);
}
executor.shutdown();
executor.awaitTermination(1, TimeUnit.MINUTES);
```

Η βασική λογική παραμένει ίδια· η ομάδα διαχειρίζεται μόνο τον κύκλο ζωής των νημάτων για εσάς.

---

## Pro tips για παραγωγική πολυνηματική ανάπτυξη

1. **Περιορίστε τον αριθμό νημάτων** – η δημιουργία δεκάδων ακατέργαστων αντικειμένων `Thread` μπορεί να υπερφορτώσει το OS. Χρησιμοποιήστε μια περιορισμένη ομάδα νημάτων.  
2. **Προτιμήστε αμετάβλητη διαμόρφωση** – κρατήστε URLs, διαδρομές αρχείων και ρυθμίσεις parser αμετάβλητες ώστε να μην τα μεταβάλετε τυχαία από έναν εργαζόμενο.  
3. **Παρακολουθήστε τη χρήση πόρων** – ακόμη και με `try‑with‑resources`, το άνοιγμα πολλών αρχείων ταυτόχρονα μπορεί να εξαντλήσει τους περιγραφείς αρχείων. Περιορίστε τον αριθμό των ταυτόχρονων εργασιών αν φτάσετε τα όρια.  
4. **Καθαρός τερματισμός** – πάντα τερματίζετε τον executor ή κάντε join στα νήματά σας ώστε η JVM να κλείσει ομαλά.

---

## Συμπέρασμα

Τώρα έχετε ένα στιβαρό, έτοιμο για αντιγραφή‑και‑επικόλληση μοτίβο για το πώς να **run multiple threads java** ενώ χρησιμοποιείτε με ασφάλεια το **try with resources java**, **loading html document java**, και **avoiding concurrency issues java**. Το κύριο συμπέρασμα είναι απλό: δώστε σε κάθε νήμα τη δική του παρουσία εγγράφου, αφήστε το `try‑with‑resources` να διαχειριστεί τον καθαρισμό και κρατήστε τα κοινά δεδομένα αμετάβλητα.

Από εδώ μπορείτε να εξερευνήσετε:

- Κλιμάκωση του μοτίβου με `ExecutorService` και μια ουρά εργασιών.  
- Μετάβαση σε έναν πραγματικό αναλυτή HTML όπως το *jsoup* (που επίσης υλοποιεί `Closeable`).  
- Προσθήκη πιο σύνθετης διαχείρισης σφαλμάτων ή λογικής επανάληψης για ασταθή I/O.

Δοκιμάστε το, ρυθμίστε τον αριθμό των εργατών, και παρακολουθήστε την έξοδο της κονσόλας να παραμένει τακτική—χωρίς

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
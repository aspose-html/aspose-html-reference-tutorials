---
category: general
date: 2026-06-19
description: Πώς να ξεκινήσετε νήμα στην Java με επαναχρησιμοποιήσιμο Runnable, να
  ξεκινήσετε πολλαπλά νήματα, να εκτυπώσετε το όνομα του νήματος και να αναλύσετε
  HTML με Java. Παράδειγμα βήμα‑προς‑βήμα.
draft: false
keywords:
- how to start thread
- start multiple threads
- print thread name
- parse html with java
- how to use runnable
language: el
og_description: Πώς να ξεκινήσετε νήμα στην Java χρησιμοποιώντας Runnable, να εκτελέσετε
  πολλαπλά νήματα, να εκτυπώσετε το όνομα του νήματος και να αναλύσετε HTML με Java
  σε ένα ενιαίο, εκτελέσιμο παράδειγμα.
og_title: Πώς να ξεκινήσετε νήμα στην Java – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to start thread in Java with a reusable Runnable, start multiple
    threads, print thread name, and parse HTML with Java. Step‑by‑step example.
  headline: How to start thread in Java – Complete Guide
  type: TechArticle
tags:
- java
- multithreading
- html-parsing
- runnable
title: Πώς να ξεκινήσετε ένα νήμα στη Java – Πλήρης Οδηγός
url: /el/java/creating-managing-html-documents/how-to-start-thread-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ξεκινήσετε νήμα σε Java – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να ξεκινήσετε νήμα** σε Java χωρίς να πνίγεστε σε κώδικα boilerplate; Δεν είστε μόνοι. Είτε χτίζετε έναν web crawler, έναν ενημερωτή UI, ή απλώς χρειάζεστε να εκχωρήσετε έναν βαριά υπολογισμό, η κατάκτηση της δημιουργίας νημάτων είναι μια απαραίτητη δεξιότητα για κάθε προγραμματιστή Java.

Σε αυτό το tutorial θα περάσουμε από ένα πρακτικό σενάριο: **ανάλυση HTML με Java**, εκτύπωση του ονόματος του τρέχοντος νήματος, και **έναρξη πολλαπλών νημάτων** που μοιράζονται την ίδια λογική. Στο τέλος θα γνωρίζετε **πώς να χρησιμοποιήσετε Runnable**, θα δημιουργήσετε αρκετούς εργαζόμενους, και θα δείτε το αναμενόμενο αποτέλεσμα — όλα σε ένα αυτόνομο παράδειγμα που μπορείτε να αντιγράψετε‑επικολλήσετε αμέσως.

## Τι Θα Μάθετε

- Τα ακριβή βήματα **πώς να ξεκινήσετε νήμα** χρησιμοποιώντας την κλάση `Thread` και ένα `Runnable`.
- Πώς να **ξεκινήσετε πολλαπλά νήματα** που εκτελούν την ίδια εργασία χωρίς να διπλοτυπείτε κώδικα.
- Ο πιο απλός τρόπος να **εκτυπώσετε το όνομα του νήματος** μαζί με τα αποτελέσματα επεξεργασίας.
- Μια καθαρή μέθοδος για **ανάλυση HTML με Java** χρησιμοποιώντας έναν ελαφρύ βοηθό `HTMLDocument` (ή οποιονδήποτε parser προτιμάτε).
- Γιατί το **πώς να χρησιμοποιήσετε runnable** είναι σημαντικό για επαναχρησιμοποιήσιμο, δοκιμαστικό κώδικα.

Δεν απαιτούνται εξωτερικές βιβλιοθήκες για το βασικό παράδειγμα, αλλά θα σημειώσουμε πού μπορείτε να αντικαταστήσετε με Jsoup ή άλλο parser εάν χρειάζεστε περισσότερη ισχύ.

## Βήμα 1: Ορίστε μια επαναχρησιμοποιήσιμη εργασία – **πώς να χρησιμοποιήσετε runnable**

Το πρώτο πράγμα που πρέπει να γνωρίζετε **πώς να χρησιμοποιήσετε runnable** είναι να ενσωματώσετε τη δουλειά που θέλετε να εκτελεί κάθε νήμα. Ένα `Runnable` είναι απλώς μια λειτουργική διεπαφή με μία μέθοδο `run()`, που το καθιστά ιδανικό για εκφράσεις lambda.

```java
// Define the reusable task
Runnable extractTextLength = () -> {
    // Open the HTML file inside a try‑with‑resources block
    try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
        // Get the length of the body text
        int textLength = doc.getBody().getTextContent().length();

        // Print the thread name and the length
        System.out.println(Thread.currentThread().getName() + ": " + textLength);
    } catch (Exception e) {
        e.printStackTrace();
    }
};
```

**Γιατί είναι σημαντικό:** Κρατώντας τη λογική μέσα σε ένα `Runnable`, μπορείτε να τη δώσετε σε οποιονδήποτε αριθμό αντικειμένων `Thread`, σε μια ομάδα νημάτων (thread pool), ή ακόμη και σε μια υπηρεσία εκτελεστή (executor service) αργότερα. Αυτό διατηρεί τον κώδικά σας DRY και δοκιμαστικό.

## Βήμα 2: **Πώς να ξεκινήσετε νήμα** – δημιουργήστε τον πρώτο εργαζόμενο

Τώρα που έχουμε ένα `Runnable`, η εκκίνηση ενός νήματος είναι τόσο εύκολη όσο η κλήση του κατασκευαστή `Thread`. Η ερώτηση **πώς να ξεκινήσετε νήμα** απαντάται με μία μόνο γραμμή:

```java
// Start the first thread
Thread worker1 = new Thread(extractTextLength, "Worker-1");
worker1.start();   // <-- this actually starts the new thread
```

Παρατηρήστε το δεύτερο όρισμα, `"Worker-1"`. Αυτό το όνομα θα εμφανιστεί όταν αργότερα **εκτυπώσουμε το όνομα του νήματος**, κάνοντας τον εντοπισμό σφαλμάτων πολύ λιγότερο ασαφές.

## Βήμα 3: **Έναρξη πολλαπλών νημάτων** – επαναχρησιμοποίηση του ίδιου Runnable

Θέλετε να επεξεργαστείτε πολλά αρχεία HTML ταυτόχρονα; Απλώς δημιουργήστε ένα ακόμη `Thread` με το ίδιο `Runnable`. Αυτό δείχνει **έναρξη πολλαπλών νημάτων** χωρίς να αντιγράψετε τον κώδικα της εργασίας:

```java
// Start a second thread that runs the exact same task
Thread worker2 = new Thread(extractTextLength, "Worker-2");
worker2.start();
```

Τanto `Worker-1` όσο και `Worker-2` θα εκτελέσουν το μπλοκ που ορίζεται στο `extractTextLength` ταυτόχρονα. Επειδή η εργασία είναι χωρίς κατάσταση (διαβάζει μόνο ένα αρχείο), δεν υπάρχει κατάσταση αγώνα (race condition) για να ανησυχείτε.

## Βήμα 4: **Εκτύπωση ονόματος νήματος** κατά την ανάλυση HTML

Μέσα στο `Runnable` έχουμε ήδη καλέσει το `Thread.currentThread().getName()`. Αυτός είναι ο κανονικός τρόπος για **εκτύπωση ονόματος νήματος**. Η έξοδος θα μοιάζει κάπως έτσι (υποθέτοντας ότι το σώμα του HTML περιέχει 1 234 χαρακτήρες):

```
Worker-1: 1234
Worker-2: 1234
```

Αν εκτελέσετε το πρόγραμμα σε ένα μεγαλύτερο αρχείο, κάθε γραμμή θα δείχνει το ίδιο μήκος επειδή και τα δύο νήματα διαβάζουν το ίδιο αρχείο. Αλλάξτε τη διαδρομή ή περάστε το όνομα του αρχείου ως παράμετρο για να δείτε διαφορετικά αποτελέσματα.

## Βήμα 5: Πλήρες, runnable παράδειγμα – από την εισαγωγή μέχρι την εκτέλεση

Παρακάτω βρίσκεται το πλήρες, **αυτόνομο** πρόγραμμα που μπορείτε να τοποθετήσετε σε ένα αρχείο με όνομα `HtmlThreadDemo.java`. Περιλαμβάνει ένα μικρό stub `HTMLDocument` ώστε ο κώδικας να μεταγλωττίζεται ακόμη και αν δεν έχετε πραγματικό parser. Αντικαταστήστε το stub με Jsoup ή οποιαδήποτε βιβλιοθήκη προτιμάτε για παραγωγική χρήση.

```java
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Minimal HTMLDocument helper.
 * In a real project you would use Jsoup or another robust parser.
 */
class HTMLDocument implements AutoCloseable {
    private final String content;

    private HTMLDocument(String html) {
        this.content = html;
    }

    public static HTMLDocument load(String path) throws IOException {
        String html = new String(Files.readAllBytes(Paths.get(path)));
        return new HTMLDocument(html);
    }

    public Body getBody() {
        // Very naive extraction of <body>...</body>
        int start = content.indexOf("<body");
        if (start == -1) return new Body("");
        start = content.indexOf('>', start) + 1;
        int end = content.indexOf("</body>", start);
        if (end == -1) end = content.length();
        return new Body(content.substring(start, end));
    }

    @Override
    public void close() {
        // No resources to free in this stub
    }

    /** Simple wrapper for body text */
    static class Body {
        private final String text;
        Body(String text) { this.text = text; }
        public String getTextContent() { return text; }
    }
}

public class HtmlThreadDemo {

    public static void main(String[] args) {
        // Step 1: Define a reusable task (how to use runnable)
        Runnable extractTextLength = () -> {
            try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
                int textLength = doc.getBody().getTextContent().length();
                // Step 4: Print thread name and length
                System.out.println(Thread.currentThread().getName() + ": " + textLength);
            } catch (Exception e) {
                e.printStackTrace();
            }
        };

        // Step 2 & 3: How to start thread and start multiple threads
        new Thread(extractTextLength, "Worker-1").start();
        new Thread(extractTextLength, "Worker-2").start();
    }
}
```

### Αναμενόμενη έξοδος

Υποθέτοντας ότι το `page.html` περιέχει 2 567 χαρακτήρες μέσα στην ετικέτα `<body>`, θα δείτε κάτι όπως:

```
Worker-1: 2567
Worker-2: 2567
```

Αν το αρχείο δεν μπορεί να διαβαστεί, θα εκτυπωθεί το stack trace — χάρη στο μπλοκ `catch`.

## Συνηθισμένα Παράπλοκα & Επαγγελματικές Συμβουλές

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Αρχείο δεν βρέθηκε** | Η διαδρομή `"YOUR_DIRECTORY/page.html"` είναι σχετική με το σημείο όπου εκκινείτε το JVM. | Χρησιμοποιήστε απόλυτη διαδρομή ή `Paths.get("").toAbsolutePath()` για εντοπισμό σφαλμάτων. |
| **Καταστάσεις αγώνα** | Αν το `Runnable` τροποποιεί κοινή κατάσταση, τα νήματα μπορεί να συγκρούονται. | Διατηρήστε την εργασία χωρίς κατάσταση ή συγχρονίστε την πρόσβαση σε κοινά αντικείμενα. |
| **Πάρα πολλά νήματα** | Η δημιουργία δεκάδων `Thread`s μπορεί να εξαντλήσει τους πόρους του λειτουργικού συστήματος. | Μεταβείτε σε `ExecutorService` με περιορισμένο pool αφού κατακτήσετε τα βασικά. |
| **Λανθασμένη ανάλυση HTML** | Το stub `HTMLDocument` είναι απλό· σύνθετες σελίδες αποτυγχάνουν. | Αντικαταστήστε το με Jsoup: `Document doc = Jsoup.parse(new File(path), "UTF‑8");` |

## Επέκταση του Παραδείγματος

Τώρα που ξέρετε **πώς να ξεκινήσετε νήμα**, μπορεί να θέλετε να:

- **Αναλύστε διαφορετικά αρχεία** περνώντας το όνομα αρχείου στο `Runnable` (χρησιμοποιήστε έναν constructor ή μια lambda που καταγράφει μια μεταβλητή).
- **Συλλέξτε αποτελέσματα** με ένα `ConcurrentLinkedQueue<Integer>` αντί για απλή εκτύπωση.
- **Εκμεταλλευτείτε μια ομάδα νημάτων** (`Executors.newFixedThreadPool(4)`) για καλύτερη κλιμακωσιμότητα.
- **Αντικαταστήστε τον parser** με Jsoup, HtmlUnit, ή οποιαδήποτε βιβλιοθήκη ταιριάζει στις ανάγκες του έργου σας.

Όλα αυτά τα βήματα βασίζονται ακόμα στην κεντρική ιδέα που καλύψαμε: ορίστε μια επαναχρησιμοποιήσιμη εργασία, δώστε την σε ένα ή πολλά νήματα, και παρατηρήστε ποιο νήμα εκτελεί τη δουλειά με **εκτύπωση ονόματος νήματος**.

## Συμπέρασμα

Καλύψαμε **πώς να ξεκινήσετε νήμα** σε Java, δείξαμε **πώς να χρησιμοποιήσετε runnable** για επαναχρησιμοποιήσιμη εργασία, σας δείξαμε πώς να **ξεκινήσετε πολλαπλά νήματα**, και περιγράψαμε έναν απλό τρόπο για **ανάλυση HTML με Java** ενώ **εκτυπώνετε το όνομα του νήματος** για κάθε εργαζόμενο. Το πλήρες απόσπασμα κώδικα παραπάνω είναι έτοιμο για εκτέλεση, και οι έννοιες κλιμακώνονται σε πιο σύνθετες, παραγωγικές εφαρμογές.

Νιώστε ελεύθεροι να πειραματιστείτε: αλλάξτε τη διαδρομή του αρχείου, αυξήστε τον αριθμό των εργαζομένων, ή ενσωματώστε έναν πραγματικό parser HTML. Τα θεμελιώδη παραμένουν τα ίδια, και τώρα έχετε μια ισχυρή βάση για οποιοδήποτε πολυνηματικό έργο Java.

Έχετε ερωτήσεις σχετικά με την ασφάλεια νημάτων, τις υπηρεσίες εκτελεστών ή τις βιβλιοθήκες ανάλυσης HTML; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Σταθερό thread pool java – Παράλληλος Καθαρισμός HTML με ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [Πώς να Επεξεργαστείτε HTML Χρησιμοποιώντας Aspose.HTML για Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Πώς να Μετατρέψετε HTML σε PDF Java – Χρησιμοποιώντας Aspose.HTML για Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
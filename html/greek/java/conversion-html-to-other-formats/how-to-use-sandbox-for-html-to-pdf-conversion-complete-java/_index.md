---
category: general
date: 2026-06-10
description: πώς να χρησιμοποιήσετε το sandbox στην Java για να μετατρέψετε HTML σε
  PDF. Μάθετε πώς να ορίσετε το μέγεθος του viewport, να ορίσετε προσαρμοσμένο user
  agent και να δημιουργήσετε PDF από HTML σε λίγα λεπτά.
draft: false
keywords:
- how to use sandbox
- convert html to pdf
- set viewport size
- set custom user agent
- create pdf from html
language: el
og_description: πώς να χρησιμοποιήσετε sandbox στη Java για ασφαλή μετατροπή HTML
  σε PDF. Περιλαμβάνει βήματα για ορισμό μεγέθους προβολής, ορισμό προσαρμοσμένου
  user agent και δημιουργία PDF από HTML.
og_title: πώς να χρησιμοποιήσετε το sandbox – Οδηγός μετατροπής Java HTML σε PDF
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: how to use sandbox in Java to convert HTML to PDF. Learn to set viewport
    size, set custom user agent, and create PDF from HTML in minutes.
  headline: how to use sandbox for HTML‑to‑PDF conversion – Complete Java Guide
  type: TechArticle
- description: how to use sandbox in Java to convert HTML to PDF. Learn to set viewport
    size, set custom user agent, and create PDF from HTML in minutes.
  name: how to use sandbox for HTML‑to‑PDF conversion – Complete Java Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Reason | |-------------|--------| | Java 17 or newer |
      Aspose.HTML requires at least Java 8, but Java 17 gives you the latest language
      features. | | Maven or Gradle build tool | To pull the Aspose.HTML library automatically.
      | | Basic knowledge of Java I/O | We’ll read an HTML file a'
  - name: Expected Output
    text: 'After the program finishes, you’ll find `responsive.pdf` in the `output`
      folder. Open it with any PDF viewer and you should see the exact layout of `responsive.html`
      as rendered on a 1280 × 800 virtual screen with a high‑DPI factor of 2.0. All
      images, fonts, and CSS media queries should respect the '
  - name: Why This Works
    text: '- **Isolation:** The `Sandbox` object runs the rendering engine in a confined
      process, preventing rogue scripts from affecting your main JVM. - **Consistency:**
      By fixing the viewport and DPI, you guarantee that every PDF looks the same,
      regardless of the machine that runs the code. - **Compatibilit'
  - name: Recap
    text: 'We’ve covered everything you need to **create PDF from HTML** safely with
      Aspose.HTML:'
  type: HowTo
tags:
- Java
- Aspose.HTML
- PDF Generation
title: πώς να χρησιμοποιήσετε το sandbox για τη μετατροπή HTML‑σε‑PDF – Πλήρης Οδηγός
  Java
url: /el/java/conversion-html-to-other-formats/how-to-use-sandbox-for-html-to-pdf-conversion-complete-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# πώς να χρησιμοποιήσετε sandbox για μετατροπή HTML‑σε‑PDF – Πλήρης Οδηγός Java

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε sandbox** όταν χρειάζεται να μετατρέψετε μια ιστοσελίδα σε PDF χωρίς να εκθέτετε την κύρια εφαρμογή σας σε επικίνδυνα scripts; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν προβλήματα όταν προσπαθούν να **μετατρέψουν HTML σε PDF** και ανησυχούν για κακόβουλο JavaScript ή απρόσμενες κλήσεις δικτύου.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα ένα πρακτικό παράδειγμα που δείχνει ακριβώς πώς να ρυθμίσετε ένα sandbox, **να ορίσετε το μέγεθος του viewport**, **να ορίσετε προσαρμοσμένο user agent**, και τελικά **να δημιουργήσετε PDF από HTML** χρησιμοποιώντας το Aspose.HTML για Java. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση πρόγραμμα που αποδίδει με ασφάλεια το `responsive.html` σε `responsive.pdf`.

## Τι Θα Μάθετε

- Γιατί ένα sandbox είναι ο πιο ασφαλής τρόπος για την απόδοση μη αξιόπιστου HTML.
- Πώς να ρυθμίσετε το περιβάλλον απόδοσης (viewport, DPI, user‑agent).
- Ο ακριβής κώδικας που απαιτείται για **μετατροπή HTML σε PDF** μέσα στο sandbox.
- Συμβουλές για την αντιμετώπιση κοινών προβλημάτων όπως ελλιπείς γραμματοσειρές ή αποκλεισμένοι πόροι.

### Προαπαιτούμενα

| Απαίτηση | Αιτία |
|-------------|--------|
| Java 17 ή νεότερη | Το Aspose.HTML απαιτεί τουλάχιστον Java 8, αλλά η Java 17 σας παρέχει τις πιο πρόσφατες δυνατότητες της γλώσσας. |
| Εργαλείο κατασκευής Maven ή Gradle | Για αυτόματη λήψη της βιβλιοθήκης Aspose.HTML. |
| Βασικές γνώσεις Java I/O | Θα διαβάσουμε ένα αρχείο HTML και θα γράψουμε ένα αρχείο PDF. |
| Μηχανή συνδεδεμένη στο διαδίκτυο (για την πρώτη εκτέλεση) | Το sandbox θα χρειαστεί να κατεβάσει τα JAR του Aspose.HTML αν δεν υπάρχουν ήδη στο τοπικό σας αποθετήριο. |

Αν έχετε αυτά τα στοιχεία, είστε έτοιμοι να ξεκινήσετε. Δεν απαιτούνται επιπλέον κόλπα IDE — οποιοσδήποτε επεξεργαστής που μπορεί να μεταγλωττίσει Java αρκεί.

## Βήμα 1 – Προσθήκη Εξαρτήματος Aspose.HTML

Πρώτα, ενημερώστε το σύστημα κατασκευής σας να κατεβάσει τη βιβλιοθήκη Aspose.HTML. Για Maven, προσθέστε αυτό το απόσπασμα στο `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

Αν προτιμάτε Gradle, το ισοδύναμο είναι:

```gradle
implementation 'com.aspose:aspose-html:23.12'
```

> **Pro tip:** Κλειδώστε τον αριθμό έκδοσης για να αποφύγετε απρόσμενες αλλαγές που σπάζουν τη λειτουργία αργότερα.

## Βήμα 2 – Δημιουργία Αντικειμένου Sandbox Options (ορισμός μεγέθους viewport & προσαρμοσμένου user agent)

Το sandbox σας παρέχει ένα περιβάλλον παρόμοιο με πρόγραμμα περιήγησης σε sandbox. Μπορείτε να το σκεφτείτε ως ένα headless Chrome που τρέχει μέσα στη διαδικασία Java, αλλά με αυστηρούς περιορισμούς στο τι μπορεί να κάνει.

```java
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;

// ...

// Define the rendering environment
SandboxOptions options = new SandboxOptions();
options.setViewportWidth(1280);          // set viewport size – width in pixels
options.setViewportHeight(800);          // set viewport size – height in pixels
options.setDevicePixelRatio(2.0);        // simulate high‑DPI screens (retina)
options.setUserAgent(
    "Mozilla/5.0 (Windows NT 10.0; Win64; x64) Chrome/120.0"
); // set custom user agent to mimic a modern browser
```

Παρατηρήστε πώς **ορίζουμε το μέγεθος του viewport** με δύο ξεχωριστές κλήσεις. Αυτό είναι κρίσιμο για σχεδιασμούς responsive· χωρίς αυτό η διάταξη μπορεί να καταρρεύσει σε προβολή κινητού. Η συμβολοσειρά **προσαρμοσμένου user agent** παραπλανά ορισμένες ιστοσελίδες ώστε να σερβίρουν την έκδοση για επιτραπέζιους υπολογιστές, κάτι που συχνά θέλετε όταν δημιουργείτε PDFs.

## Βήμα 3 – Αρχικοποίηση του Sandbox

Τώρα εκκινούμε το sandbox χρησιμοποιώντας ένα μπλοκ *try‑with‑resources*. Αυτό εγγυάται ότι το sandbox κλείνει αυτόματα, ακόμη και αν προκύψει εξαίρεση.

```java
try (Sandbox sandbox = new Sandbox(options)) {
    // sandbox is now ready – all rendering will happen inside this safe container
}
```

Αν είστε περίεργοι, το sandbox απομονώνει την πρόσβαση στο σύστημα αρχείων, τις κλήσεις δικτύου και την εκτέλεση JavaScript. Είναι ο προτεινόμενος τρόπος για **μετατροπή HTML σε PDF** όταν το πηγαίο HTML προέρχεται από εξωτερική ή μη αξιόπιστη πηγή.

## Βήμα 4 – Μετατροπή HTML σε PDF Μέσα στο Sandbox

Μέσα στο μπλοκ `try` καλούμε το `Conversion.convert`. Αυτή η στατική μέθοδος κάνει τη βαριά δουλειά: φορτώνει το HTML, το αποδίδει σύμφωνα με τις επιλογές που ορίσαμε και γράφει ένα αρχείο PDF.

```java
import com.aspose.html.Conversion;

// ...

Conversion.convert(
    "YOUR_DIRECTORY/responsive.html",   // input HTML path
    "YOUR_DIRECTORY/output/responsive.pdf" // output PDF path
);
```

Αντικαταστήστε το `YOUR_DIRECTORY` με την απόλυτη ή σχετική διαδρομή όπου βρίσκεται το HTML σας. Η μέθοδος θα ρίξει εξαίρεση αν το αρχείο δεν μπορεί να διαβαστεί ή το PDF δεν μπορεί να γραφτεί, οπότε ίσως θελήσετε να το τυλίξετε σε ένα υψηλότερο επίπεδο `try/catch` αν χρειάζεστε ευγενική διαχείριση σφαλμάτων.

### Αναμενόμενο Αποτέλεσμα

Μετά την ολοκλήρωση του προγράμματος, θα βρείτε το `responsive.pdf` στο φάκελο `output`. Ανοίξτε το με οποιονδήποτε προβολέα PDF και θα πρέπει να δείτε την ακριβή διάταξη του `responsive.html` όπως αποδόθηκε σε εικονική οθόνη 1280 × 800 με παράγοντα υψηλής DPI 2.0. Όλες οι εικόνες, οι γραμματοσειρές και τα CSS media queries θα πρέπει να σέβονται το **ορισμένο μέγεθος viewport** και το **προσαρμοσμένο user agent** που ορίσαμε νωρίτερα.

![πώς να χρησιμοποιήσετε sandbox – διάγραμμα παραδείγματος sandbox](https://example.com/images/sandbox-diagram.png "πώς να χρησιμοποιήσετε sandbox")

*Κείμενο εναλλακτικής εικόνας:* πώς να χρησιμοποιήσετε sandbox – διάγραμμα της ροής εργασίας sandbox

## Βήμα 5 – Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα, εδώ είναι η πλήρης, έτοιμη‑για‑εκτέλεση κλάση Java. Μη διστάσετε να αντιγράψετε‑επικολλήσετε, να προσαρμόσετε τις διαδρομές και να πατήσετε *run*.

```java
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.Conversion;

/**
 * Demonstrates how to use sandbox to safely convert HTML to PDF.
 * The example sets a custom viewport size and a custom user‑agent string.
 */
public class SandboxExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create sandbox options and define the rendering environment
        SandboxOptions options = new SandboxOptions();
        options.setViewportWidth(1280);          // width of the virtual screen
        options.setViewportHeight(800);          // height of the virtual screen
        options.setDevicePixelRatio(2.0);        // simulate high‑DPI displays
        options.setUserAgent(
            "Mozilla/5.0 (Windows NT 10.0; Win64; x64) Chrome/120.0"
        ); // set custom user agent

        // Step 2: Initialise the sandbox with the configured options
        try (Sandbox sandbox = new Sandbox(options)) {
            // Step 3: Convert the HTML file to PDF inside the sandbox context
            Conversion.convert(
                "YOUR_DIRECTORY/responsive.html",
                "YOUR_DIRECTORY/output/responsive.pdf"
            );
        } // the sandbox is automatically closed here
    }
}
```

### Γιατί Λειτουργεί Αυτό

- **Isolation:** Το αντικείμενο `Sandbox` εκτελεί τη μηχανή απόδοσης σε περιορισμένη διεργασία, αποτρέποντας ακατάλληλα scripts από το να επηρεάσουν την κύρια JVM σας.
- **Consistency:** Με το να σταθεροποιήσετε το viewport και το DPI, εξασφαλίζετε ότι κάθε PDF φαίνεται το ίδιο, ανεξάρτητα από το μηχάνημα που εκτελεί τον κώδικα.
- **Compatibility:** Ένα προσαρμοσμένο user‑agent εξασφαλίζει ότι οι ιστοσελίδες που σερβίρουν διαφορετικό markup για κινητό vs. επιτραπέζιο δεν θα σας εκπλήξουν με σπασμένη διάταξη.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| *Τι γίνεται αν το HTML μου αναφέρεται σε εξωτερικό CSS ή εικόνες;* | Το sandbox μπορεί να κατεβάσει απομακρυσμένους πόρους, αλλά ίσως θέλετε να απενεργοποιήσετε την πρόσβαση στο δίκτυο για αυστηρότερη ασφάλεια. Χρησιμοποιήστε `options.setEnableNetworkAccess(false)` εάν χρειάζεστε μόνο τοπικά στοιχεία. |
| *Το PDF μου λείπουν οι γραμματοσειρές.* | Βεβαιωθείτε ότι οι γραμματοσειρές που χρησιμοποιούνται στο HTML είναι εγκατεστημένες στο λειτουργικό σύστημα ή ενσωματώστε τις χρησιμοποιώντας CSS `@font-face`. Το Aspose.HTML θα ενσωματώσει οποιαδήποτε γραμματοσειρά μπορεί να εντοπίσει. |
| *Το παραγόμενο PDF είναι κενό.* | Ελέγξτε ξανά τη διαδρομή εισόδου και βεβαιωθείτε ότι οι διαστάσεις του viewport είναι αρκετά μεγάλες για το περιεχόμενο της σελίδας. |
| *Μπορώ να μετατρέψω πολλά αρχεία HTML σε μία εκτέλεση;* | Ναι. Απλώς κάντε βρόχο πάνω σε μια λίστα ονομάτων αρχείων και καλέστε `Conversion.convert` για κάθε επανάληψη μέσα στο ίδιο sandbox. |

## Επόμενα Βήματα

Τώρα που γνωρίζετε **πώς να χρησιμοποιήσετε sandbox** για ένα μόνο αρχείο, ίσως θέλετε να:

1. **Επεξεργασία κατά παρτίδες** ενός φακέλου αναφορών HTML — ιδανική για νυχτερινή αυτοματοποίηση.
2. **Προσθήκη υδατογραφήματος** ή μεταδεδομένων PDF χρησιμοποιώντας το Aspose.PDF μετά τη μετατροπή.
3. **Ενσωμάτωση** της μετατροπής σε ένα REST endpoint Spring Boot, εκθέτοντας ένα `POST /convert` που επιστρέφει το ρεύμα PDF.

Όλες αυτές οι επεκτάσεις εξακολουθούν να ωφελούνται από το δίχτυ ασφαλείας του sandbox, ώστε να διατηρείτε το περιβάλλον παραγωγής σας καθαρό και ασφαλές.

---

### Ανακεφαλαίωση

Συζητήσαμε όλα όσα χρειάζεστε για να **δημιουργήσετε PDF από HTML** με ασφάλεια χρησιμοποιώντας το Aspose.HTML:

- Ρυθμίστε το sandbox (συμπεριλαμβανομένου του **ορισμού μεγέθους viewport** και του **προσαρμοσμένου user agent**).
- Εκτελέστε `Conversion.convert` μέσα στο sandbox για **μετατροπή HTML σε PDF**.
- Αντιμετωπίστε κοινά προβλήματα και σκεφτείτε την κλιμάκωση της λύσης.

Δοκιμάστε το, προσαρμόστε το viewport ή το user‑agent ώστε να ταιριάζει στο κοινό-στόχο σας, και αφήστε το sandbox να κάνει τη βαριά δουλειά. Καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σειρά;

Οι παρακάτω οδηγίες καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Χρησιμοποιήσετε το Aspose.HTML για Διαμόρφωση Γραμματοσειρών για HTML‑σε‑PDF Java](/html/english/java/configuring-environment/configure-fonts/)
- [Δημιουργία PDF από HTML – Ορισμός Φύλλου Στυλ Χρήστη στο Aspose.HTML για Java](/html/english/java/configuring-environment/set-user-style-sheet/)
- [Πώς να Μετατρέψετε HTML σε PDF Java – Χρησιμοποιώντας το Aspose.HTML για Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-06-19
description: Αποκτήστε τον τίτλο της σελίδας σε Java φορτώνοντας μια ιστοσελίδα εκτός
  σύνδεσης, ορίζοντας τις διαστάσεις της οθόνης και απενεργοποιώντας εξωτερικούς πόρους.
  Μάθετε πώς να φορτώνετε τη διεύθυνση URL ενός εγγράφου HTML βήμα‑βήμα.
draft: false
keywords:
- extract page title
- set screen dimensions
- load webpage offline
- disable external resources
- load html document url
language: el
og_description: Αποκτήστε γρήγορα τον τίτλο της σελίδας σε Java. Αυτός ο οδηγός δείχνει
  πώς να φορτώσετε μια ιστοσελίδα εκτός σύνδεσης, να ορίσετε τις διαστάσεις της οθόνης
  και να απενεργοποιήσετε εξωτερικούς πόρους για αξιόπιστη επεξεργασία HTML.
og_title: Εξαγωγή Τίτλου Σελίδας σε Java – Πλήρες Μάθημα Aspose.HTML
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Extract page title in Java by loading a webpage offline, setting screen
    dimensions, and disabling external resources. Learn to load HTML document URL
    step‑by‑step.
  headline: Extract Page Title with Java – Full Guide Using Aspose.HTML
  type: TechArticle
- description: Extract page title in Java by loading a webpage offline, setting screen
    dimensions, and disabling external resources. Learn to load HTML document URL
    step‑by‑step.
  name: Extract Page Title with Java – Full Guide Using Aspose.HTML
  steps:
  - name: What if the page redirects?
    text: Aspose.HTML follows HTTP redirects by default. The final destination’s title
      will be returned. If you need to capture intermediate titles, you’d have to
      handle the `HttpResponse` manually—something rarely required for simple title
      extraction.
  - name: How do I handle non‑HTML responses (e.g., PDFs)?
    text: The `HTMLDocument.load` method throws an exception if the content type isn’t
      HTML. Wrap the call in a `try/catch` and inspect the `Content-Type` header if
      you need a fallback strategy.
  - name: Can I extract other meta tags at the same time?
    text: 'Absolutely. Once you have the `HTMLDocument` instance, you can query the
      DOM:'
  - name: Does the sandbox support JavaScript execution?
    text: Yes, but only if you enable it. By default, the sandbox runs in a “safe
      mode” where scripts are ignored. If you ever need to evaluate inline scripts
      for title generation (rare, but possible with SPA frameworks), set `setAllowExternalResources(true)`
      and optionally enable `setEnableJavaScript(true)`.
  type: HowTo
tags:
- Java
- Aspose.HTML
- Web Scraping
title: Εξαγωγή Τίτλου Σελίδας με Java – Πλήρης Οδηγός Χρήσης Aspose.HTML
url: /el/java/creating-managing-html-documents/extract-page-title-with-java-full-guide-using-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Τίτλου Σελίδας με Java – Πλήρης Οδηγός Χρήσης Aspose.HTML

Έχετε χρειαστεί ποτέ να **εξάγετε τον τίτλο της σελίδας** από έναν απομακρυσμένο ιστότοπο αλλά δεν θέλετε η εφαρμογή σας να κατεβάζει κάθε τυχαίο αρχείο CSS, script ή εικόνα; Δεν είστε μόνοι. Σε πολλές περιπτώσεις αυτοματοποίησης—σκεφτείτε ελέγχους SEO ή παρακολούθηση περιεχομένου—μας ενδιαφέρει μόνο τα μεταδεδομένα μιας σελίδας, όχι η πλήρης οπτική απόδοση.  

Αυτό το tutorial δείχνει ακριβώς πώς να **εξάγετε τον τίτλο της σελίδας** χρησιμοποιώντας Aspose.HTML για Java ενώ **φορτώνετε τη σελίδα εκτός σύνδεσης**, **ορίζετε τις διαστάσεις της οθόνης**, και **απενεργοποιείτε εξωτερικούς πόρους**. Στο τέλος, θα έχετε ένα συμπαγές, έτοιμο για παραγωγή snippet που φορτώνει οποιοδήποτε **HTML document URL** σε περιβάλλον sandbox και εκτυπώνει τον τίτλο του στην κονσόλα.

## Τι Θα Μάθετε

- Διαμορφώστε ένα sandbox Aspose.HTML για να **ορίσετε τις διαστάσεις της οθόνης** που μιμείται έναν επιτραπέζιο περιηγητή.  
- Απενεργοποιήστε τις κλήσεις δικτύου για CSS, JavaScript και εικόνες ώστε η φόρτωση να γίνεται **εκτός σύνδεσης**.  
- Χρησιμοποιήστε το `HTMLDocument.load` με ένα **load html document url** και ανακτήστε το στοιχείο `<title>`.  
- Διαχειριστείτε τους πόρους με ασφάλεια χρησιμοποιώντας try‑with‑resources και αποφύγετε διαρροές μνήμης.  

Δεν απαιτούνται εξωτερικές βιβλιοθήκες πέρα από το Aspose.HTML, και ο κώδικας λειτουργεί σε Java 8+ και οποιοδήποτε σύγχρονο JDK.

---

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

1. **Java Development Kit (JDK) 8 ή νεότερο** εγκατεστημένο.  
2. **Aspose.HTML for Java** (η τελευταία έκδοση μέχρι τον Ιούνιο 2026). Μπορείτε να το αποκτήσετε από το Maven Central:

   ```xml
   <dependency>
       <groupId>com.aspose</groupId>
       <artifactId>aspose-html</artifactId>
       <version>23.9</version>
   </dependency>
   ```

3. Ένα **βασικό IDE** (IntelliJ IDEA, Eclipse ή VS Code) ή έναν απλό επεξεργαστή κειμένου και τη γραμμή εντολών.  

Αυτό είναι όλο—χωρίς επιπλέον ρυθμίσεις, χωρίς headless browsers, μόνο το Aspose.HTML που κάνει το σκληρό έργο.

---

## Βήμα 1: Δημιουργία Sandbox και **Ορισμός Διαστάσεων Οθόνης**

Το πρώτο πράγμα που θα παρατηρήσετε στον δείγμα κώδικα είναι η διαμόρφωση του sandbox. Ένα sandbox είναι ένας ελαφρύς, εντός‑διαδικασίας εξομοιωτής περιηγητή. Από προεπιλογή προσποιείται ότι είναι μια μικρή κινητή συσκευή, κάτι που μπορεί να παραμορφώσει το DOM που λαμβάνετε. Για να κάνετε τη σελίδα να συμπεριφέρεται όπως όταν προβάλλεται σε τυπικό επιτραπέζιο περιηγητή, πρέπει να **ορίσετε τις διαστάσεις της οθόνης**.

```java
// Initialize load options
HtmlLoadOptions loadOptions = new HtmlLoadOptions();

// Emulate a 1024×768 screen – this is a common desktop resolution
loadOptions.getSandbox()
           .setScreenWidth(1024)   // set screen width
           .setScreenHeight(768); // set screen height
```

> **Γιατί είναι σημαντικό;** Πολλοί σύγχρονοι ιστότοποι παρέχουν διαφορετικά HTML τμήματα ανάλογα με το μέγεθος του viewport. Με την επιβολή πλάτους 1024 px, διασφαλίζετε ότι το markup που λαμβάνετε περιέχει το πλήρες ετικέτα `<title>` όπως θα την αποδίδει ένας κανονικός περιηγητής.

---

## Βήμα 2: **Απενεργοποίηση Εξωτερικών Πόρων** για Φόρτωση Εκτός Σύνδεσης

Όταν χρειάζεστε μόνο τον τίτλο της σελίδας, η λήψη κάθε εξωτερικού stylesheet, script ή εικόνας είναι άσκοπη. Επίσης επιβραδύνει την εφαρμογή σας και μπορεί να προκαλέσει ανεπιθύμητες παρενέργειες (π.χ., JavaScript που προσπαθεί να επικοινωνήσει με τρίτο API). Το Aspose.HTML σας επιτρέπει να **απενεργοποιήσετε εξωτερικούς πόρους** με μια μόνο γραμμή:

```java
// Prevent the sandbox from fetching CSS, JS, images, etc.
loadOptions.getSandbox().setAllowExternalResources(false);
```

> **Συμβουλή:** Αν αργότερα διαπιστώσετε ότι χρειάζεστε ενσωματωμένο CSS για σωστή εξαγωγή τίτλου (σπάνιο, αλλά δυνατό), απλώς αλλάξτε αυτή τη σημαία σε `true`.

---

## Βήμα 3: **Φόρτωση του HTML Document URL** Μέσα στο Sandbox

Τώρα που το sandbox είναι προετοιμασμένο, μπορείτε με ασφάλεια να **φορτώσετε το html document url** χωρίς να ανησυχείτε για επιπλέον δικτυακή κίνηση. Η μέθοδος `HTMLDocument.load` δέχεται το URL προορισμού και τις επιλογές που μόλις δημιουργήσαμε.

```java
String url = "https://example.com"; // replace with the page you want to inspect

try (HTMLDocument doc = HTMLDocument.load(url, loadOptions)) {
    // Extract the title once the document is fully parsed
    String title = doc.getTitle();
    System.out.println("Title: " + title);
}
```

Το μπλοκ `try‑with‑resources` εγγυάται ότι το έγγραφο διαχειρίζεται σωστά, αποτρέποντας διαρροές μνήμης—ιδιαίτερα σημαντικό όταν επεξεργάζεστε πολλές σελίδες σε μια παρτίδα.

> **Τι λαμβάνετε:** Η κονσόλα εκτυπώνει κάτι όπως `Title: Example Domain`. Αυτό είναι το αποτέλεσμα **εξαγωγής τίτλου σελίδας** που ζητούσατε.

---

## Βήμα 4: Πλήρες, Έτοιμο‑για‑Εκτέλεση Παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα, έτοιμο για αντιγραφή‑επικόλληση σε αρχείο `LoadWithSandbox.java`. Όλα τα μέρη—ρυθμίσεις sandbox, διαστάσεις οθόνης, απενεργοποίηση πόρων και εξαγωγή τίτλου—συνδυάζονται.

```java
import com.aspose.html.*;
import com.aspose.html.load.*;

public class LoadWithSandbox {
    public static void main(String[] args) throws Exception {
        // Step 1: Specify the URL of the page to load
        String url = "https://example.com";

        // Step 2: Create load options and configure a sandbox that mimics a desktop browser
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        loadOptions.getSandbox()
                   .setScreenWidth(1024)                     // emulate 1024‑pixel wide screen
                   .setScreenHeight(768)                     // emulate 768‑pixel tall screen
                   .setUserAgent("Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36");

        // Step 3: Disable external network resources (CSS, JS, images) for offline processing
        loadOptions.getSandbox().setAllowExternalResources(false);

        // Step 4: Load the HTML document using the configured sandbox and display its title
        try (HTMLDocument doc = HTMLDocument.load(url, loadOptions)) {
            System.out.println("Title: " + doc.getTitle());
        }
    }
}
```

**Αναμενόμενη έξοδος** (όταν εκτελεστεί εναντίον του `https://example.com`):

```
Title: Example Domain
```

Αν θέσετε τη μεταβλητή `url` σε οποιονδήποτε άλλο ιστότοπο, το πρόγραμμα θα εξακολουθήσει να **εξάγει τον τίτλο της σελίδας** γρήγορα επειδή όλα τα βαριά assets παραμένουν απενεργοποιημένα.

---

## Βήμα 5: Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν η σελίδα κάνει ανακατεύθυνση;

Το Aspose.HTML ακολουθεί τις ανακατευθύνσεις HTTP από προεπιλογή. Θα επιστραφεί ο τίτλος του τελικού προορισμού. Αν χρειαστεί να καταγράψετε ενδιάμεσους τίτλους, θα πρέπει να διαχειριστείτε το `HttpResponse` χειροκίνητα—κάτι σπάνια απαιτείται για απλή εξαγωγή τίτλου.

### Πώς να διαχειριστώ μη‑HTML απαντήσεις (π.χ., PDF);

Η μέθοδος `HTMLDocument.load` ρίχνει εξαίρεση αν ο τύπος περιεχομένου δεν είναι HTML. Τυλίξτε την κλήση σε `try/catch` και ελέγξτε την κεφαλίδα `Content-Type` αν χρειάζεστε στρατηγική εναλλακτικής λύσης.

### Μπορώ να εξάγω και άλλα meta tags ταυτόχρονα;

Απόλυτα. Μonce έχετε το αντικείμενο `HTMLDocument`, μπορείτε να ερωτήσετε το DOM:

```java
String description = doc.querySelector("meta[name='description']").getAttribute("content");
```

Απλώς θυμηθείτε να διατηρείτε την **απενεργοποίηση εξωτερικών πόρων** ενεργή αν σας ενδιαφέρουν μόνο τα μεταδεδομένα· διαφορετικά μπορεί να κατεβάσετε ακούσια μεγάλα assets.

### Υποστηρίζει το sandbox την εκτέλεση JavaScript;

Ναι, αλλά μόνο αν το ενεργοποιήσετε. Από προεπιλογή, το sandbox λειτουργεί σε “ασφαλή λειτουργία” όπου τα scripts αγνοούνται. Αν ποτέ χρειαστεί να αξιολογήσετε ενσωματωμένα scripts για τη δημιουργία τίτλου (σπάνιο, αλλά δυνατό με SPA frameworks), ορίστε `setAllowExternalResources(true)` και προαιρετικά ενεργοποιήστε `setEnableJavaScript(true)`.

---

## Επαγγελματικές Συμβουλές & Πιθανά Σφάλματα

- **Επαναχρησιμοποίηση του `HtmlLoadOptions`** όταν επεξεργάζεστε πολλά URLs. Η δημιουργία νέου sandbox για κάθε αίτηση προσθέτει επιπλέον φόρτο.  
- **Κρύψτε (cache) τη συμβολοσειρά user‑agent** αν κάνετε επαναλαμβανόμενα αιτήματα στο ίδιο domain· ορισμένοι ιστότοποι παρέχουν διαφορετικούς τίτλους ανάλογα με το UA.  
- **Προσοχή σε Cloudflare ή ανίχνευση bots**. Ακόμη και με απενεργοποιημένους εξωτερικούς πόρους, ο διακομιστής μπορεί να μπλοκάρει αιτήματα που λείπουν κοινές κεφαλίδες. Η προσθήκη ενός ρεαλιστικού user‑agent (όπως φαίνεται παραπάνω) συνήθως λύνει το πρόβλημα.

---

## Συμπέρασμα

Διασχίσαμε έναν πλήρη, παραγωγικό τρόπο για **εξαγωγή τίτλου σελίδας** από οποιοδήποτε URL χρησιμοποιώντας Java και Aspose.HTML. Με **ορισμό διαστάσεων οθόνης**, **απενεργοποίηση εξωτερικών πόρων**, και φόρτωση του HTML εγγράφου σε περιβάλλον sandbox, λαμβάνετε γρήγορα, αξιόπιστα αποτελέσματα χωρίς το βάρος ενός πλήρους μηχανήματος περιήγησης.  

Από εδώ μπορείτε να επεκτείνετε τη λύση—να συλλέξετε meta descriptions, Open Graph tags, ή ακόμη και να δημιουργήσετε screenshot αν αποφασίσετε αργότερα να ενεργοποιήσετε το οπτικό pipeline. Το βασικό μοτίβο παραμένει το ίδιο: διαμορφώστε το sandbox, απενεργοποιήστε ό,τι δεν χρειάζεστε, φορτώστε το URL και διαβάστε το DOM.

Έτοιμοι να το ενσωματώσετε σε έναν μεγαλύτερο crawler; Προσθέστε ένα thread pool, δώστε του μια λίστα URLs, και αποθηκεύστε κάθε τίτλο σε βάση δεδομένων. Ο ουρανός είναι το όριο.

*Καλό κώδικα, και οι τίτλοι σας πάντα να είναι ακριβείς!*

![Στιγμιότυπο οθόνης που δείχνει την έξοδο της κονσόλας κατά την εξαγωγή του τίτλου σελίδας χρησιμοποιώντας το sandbox Aspose.HTML](extract-page-title.png "εξαγωγή τίτλου σελίδας χρησιμοποιώντας το sandbox Aspose.HTML")

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικούς θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Φόρτωση Εγγράφων HTML από URL στο Aspose.HTML για Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-url/)
- [Διαχείριση Συμβάντων Φόρτωσης Εγγράφου στο Aspose.HTML για Java](/html/english/java/creating-managing-html-documents/handle-document-load-events/)
- [Δημιουργία sandbox για HTML σε Java – Οδηγός Βήμα‑Βήμα](/html/english/java/creating-managing-html-documents/create-sandbox-for-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
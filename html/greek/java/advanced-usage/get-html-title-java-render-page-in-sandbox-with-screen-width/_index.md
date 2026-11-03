---
category: general
date: 2026-03-22
description: Αποκτήστε γρήγορα τον τίτλο HTML σε Java χρησιμοποιώντας το Aspose.HTML.
  Μάθετε πώς να ορίσετε το πλάτος της οθόνης σε Java και να εξάγετε τον τίτλο της
  σελίδας σε Java με ασφάλεια σε περιβάλλον sandbox.
draft: false
keywords:
- get html title java
- extract page title java
- set screen width java
language: el
og_description: Αποκτήστε τον τίτλο HTML Java σε δευτερόλεπτα. Αυτός ο οδηγός δείχνει
  πώς να ορίσετε το πλάτος της οθόνης Java και να εξάγετε με ασφάλεια τον τίτλο της
  σελίδας Java με το Aspose.HTML.
og_title: Αποκτήστε τον τίτλο HTML Java – Οδηγός γρήγορης απόδοσης sandbox
tags:
- Java
- Aspose.HTML
- Web Scraping
title: Απόκτηση του τίτλου HTML σε Java – Απόδοση σελίδας σε sandbox με πλάτος οθόνης
url: /el/java/advanced-usage/get-html-title-java-render-page-in-sandbox-with-screen-width/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Λήψη HTML Title Java – Απόδοση Σελίδας σε Sandbox με Πλάτος Οθόνης

Έχετε ποτέ χρειαστεί να **get HTML title java** αλλά δεν ήσασταν σίγουροι πώς να αποφύγετε απρόοπτα δικτύου ή ασυνεπή απόδοση; Δεν είστε μόνοι. Σε πολλά έργα αυτοματοποίησης ο τίτλος της σελίδας είναι το πρώτο δεδομένο που ζητάτε, όμως η αξιόπιστη λήψη του μπορεί να είναι επίπονη—ιδιαίτερα όταν η σελίδα εξαρτάται από ένα συγκεκριμένο μέγεθος προβολής.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει πώς να **set screen width java** για καθοριστική διάταξη, να φορτώσετε μια απομακρυσμένη σελίδα μέσα σε sandbox, και τελικά να **extract page title java** με το Aspose.HTML. Στο τέλος θα έχετε ένα αυτόνομο απόσπασμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Java, χωρίς επιπλέον κόλπα.

## Τι Θα Χρειαστείτε

- Java 17 ή νεότερη (ο κώδικας χρησιμοποιεί try‑with‑resources, επομένως JDK 7+ είναι εντάξει).  
- Aspose.HTML for Java 23.9 (ή η πιο πρόσφατη έκδοση τη στιγμή της συγγραφής).  
- Ένα IDE ή απλή γραμμή εντολών `javac`/`java`.  
- Πρόσβαση στο Internet για την πρώτη εκτέλεση (το sandbox θα μπλοκάρει περαιτέρω κλήσεις).  

Αυτό είναι—χωρίς μαγεία Maven, χωρίς επιπλέον βιβλιοθήκες πέρα από το Aspose.HTML. Αν ήδη χρησιμοποιείτε κάποιο εργαλείο κατασκευής, απλώς προσθέστε το JAR του Aspose.HTML στο classpath.

## Βήμα 1: Set Screen Width Java για Συνεπή Απόδοση

Όταν μια σελίδα αποδίδεται, το μέγεθος του viewport του προγράμματος περιήγησης μπορεί να αλλάξει τη διάταξη DOM, τα CSS media queries ή ακόμη και το κείμενο του τίτλου (σκεφτείτε τα responsive λογότυπα). Για να εγγυηθείτε το ίδιο αποτέλεσμα κάθε φορά, δημιουργούμε ένα sandbox που προσομοιώνει την οθόνη **1024 × 768** pixel.

```java
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxBuilder;

// Build a sandbox that simulates a 1024×768 screen and disables network calls.
Sandbox renderingSandbox = new SandboxBuilder()
        .setScreenWidth(1024)          // <-- set screen width java
        .setScreenHeight(768)
        .disableNetworkAccess()        // blocks any further HTTP requests
        .build();
```

**Γιατί αυτό είναι σημαντικό:**  
Η κλήση `setScreenWidth` αναγκάζει τη μηχανή απόδοσης να αντιμετωπίζει την εικονική οθόνη ακριβώς όπως μια οθόνη πλάτους 1024 pixel. Αν αργότερα μεταβείτε σε σχεδίαση mobile‑first, απλώς αλλάξτε το πλάτος και το υπόλοιπο του κώδικα παραμένει το ίδιο.

> **Pro tip:** Αν δοκιμάζετε πολλαπλά breakpoints, δημιουργήστε ξεχωριστές sandbox instances για κάθε πλάτος. Είναι φτηνό και διατηρεί τα τεστ σας καθοριστικά.

## Βήμα 2: Φόρτωση του HTML Document Μέσα στο Sandbox

Τώρα που το sandbox είναι έτοιμο, φορτώνουμε το URL-στόχο. Ο κατασκευαστής του `HTMLDocument` δέχεται το sandbox ως δεύτερο όρισμα, διασφαλίζοντας ότι η σελίδα αποδίδεται μέσα στο ελεγχόμενο περιβάλλον που ορίσαμε.

```java
import com.aspose.html.HTMLDocument;

try (HTMLDocument htmlDoc = new HTMLDocument("https://example.com", renderingSandbox)) {
    // The document is now rendered with the 1024×768 viewport.
    // Any subsequent network request (e.g., AJAX) will be blocked.
```

**Τι συμβαίνει στο παρασκήνιο;**  
Το Aspose.HTML δημιουργεί έναν off‑screen renderer βασισμένο στο Chromium. Το sandbox απομονώνει τη διαδικασία, έτσι ακόμη και αν η σελίδα προσπαθήσει να φορτώσει εξωτερικά scripts, θα απορρίπτονται σιωπηρά—ιδανικό για crawlers με έμφαση στην ασφάλεια.

## Βήμα 3: Extract Page Title Java – Επαλήθευση του Αποτελέσματος

Με το έγγραφο φορτωμένο, η λήψη του τίτλου είναι μια γραμμή κώδικα. Αυτό είναι ο πυρήνας του **get html title java**.

```java
    // Step 3: Retrieve the page title.
    String pageTitle = htmlDoc.getTitle();
    System.out.println("Title: " + pageTitle); // Expected output: Title: Example Domain
}
```

Η εκτέλεση του προγράμματος εκτυπώνει:

```
Title: Example Domain
```

Αυτή είναι η ενότητα **extract page title java** ολοκληρωμένη. Επειδή χρησιμοποιήσαμε sandbox, ο τίτλος που βλέπετε είναι ακριβώς αυτός που θα έβλεπε ένας χρήστης με πρόγραμμα περιήγησης πλάτους 1024 px—χωρίς κρυφά JavaScript κόλπα.

## Πλήρες, Εκτελέσιμο Παράδειγμα

Παρακάτω είναι ο πλήρης κώδικας που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο `RenderWithSandbox.java`. Συγκεντρώνεται και εκτελείται ακριβώς όπως είναι, εφόσον το JAR του Aspose.HTML βρίσκεται στο classpath σας.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxBuilder;

public class RenderWithSandbox {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox that simulates a 1024×768 screen and blocks external network access.
        Sandbox renderingSandbox = new SandboxBuilder()
                .setScreenWidth(1024)          // set screen width java
                .setScreenHeight(768)
                .disableNetworkAccess()
                .build();

        // Step 2: Load the HTML document inside the sandboxed environment.
        try (HTMLDocument htmlDoc = new HTMLDocument("https://example.com", renderingSandbox)) {

            // Step 3: Work with the rendered content – here we simply print the page title.
            System.out.println("Title: " + htmlDoc.getTitle()); // get html title java
        }
    }
}
```

### Αναμενόμενη Έξοδος

```
Title: Example Domain
```

Αν το URL αλλάξει ή η σελίδα χρησιμοποιεί διαφορετικό τίτλο, η κονσόλα θα εμφανίσει τη νέα τιμή—χωρίς ανάγκη αλλαγής κώδικα.

## Συχνές Ερωτήσεις (FAQ)

### Λειτουργεί αυτό με ιστότοπους HTTPS που απαιτούν πιστοποιητικά;
Ναι. Το Aspose.HTML σέβεται το προεπιλεγμένο trust store της Java. Αν χρειάζεστε προσαρμοσμένο keystore, ρυθμίστε το πριν δημιουργήσετε το sandbox.

### Τι γίνεται αν χρειαστεί να ενεργοποιήσω πρόσβαση δικτύου για συγκεκριμένους πόρους;
Αντί για `disableNetworkAccess()`, καλέστε `allowNetworkAccess()` και στη συνέχεια χρησιμοποιήστε `addAllowedDomain("mycdn.com")` στον builder. Αυτό κρατά το sandbox σφιχτό ενώ εξακολουθεί να επιτρέπει την λήψη των απαραίτητων πόρων.

### Μπορώ να καταγράψω screenshot της αποδοθείσας σελίδας;
Απολύτως. Μετά τη φόρτωση, καλέστε `htmlDoc.renderToBitmap("output.png", 1024, 768);`. Το ίδιο `setScreenWidth` που χρησιμοποιήσατε θα καθορίσει τις διαστάσεις της εικόνας.

### Πώς διαφέρει αυτό από τη χρήση του Selenium;
Το Selenium οδηγεί ένα πραγματικό πρόγραμμα περιήγησης, το οποίο είναι βαριά και πιο δύσκολο να sandbox. Το Aspose.HTML αποδίδει off‑screen, καταναλώνει πολύ λιγότερη μνήμη και παρέχει άμεση πρόσβαση στο DOM χωρίς γέφυρα WebDriver.

## Ακραίες Περιπτώσεις & Καλές Πρακτικές

| Κατάσταση | Προτεινόμενη Προσέγγιση |
|-----------|------------------------|
| Η σελίδα χρησιμοποιεί **dynamic meta refresh** για αλλαγή του τίτλου μετά τη φόρτωση | Προσθέστε ένα σύντομο `Thread.sleep(2000)` πριν το `getTitle()` ή ακούστε το γεγονός `onload` μέσω `htmlDoc.addEventListener("load", ...)`. |
| Ο τίτλος ορίζεται μέσω **JavaScript μετά AJAX** | Διατηρήστε την πρόσβαση δικτύου ενεργοποιημένη για το συγκεκριμένο API endpoint, ή προσομοιώστε την απόκριση μέσα στο sandbox χρησιμοποιώντας `addVirtualResponse`. |
| Χρειάζεται να **επεξεργαστείτε πολλές URLs** | Επαναχρησιμοποιήστε ένα μόνο αντικείμενο `Sandbox`; δημιουργήστε νέο `HTMLDocument` μόνο ανά URL για μείωση του κόστους. |
| Ο ιστότοπος μπλοκάρει **headless browsers** | Κάντε spoof ένα κοινό user‑agent string μέσω `renderingSandbox.setUserAgent("Mozilla/5.0 …")`. |

## Σχετικά Θέματα που Μπορείτε Να Εξερευνήσετε Στη Σειρά

- **Extract page title java** από αρχεία PDF χρησιμοποιώντας Aspose.PDF.  
- **Set screen width java** για μετατροπή PDF σε εικόνα (χρησιμοποιήστε `PdfRenderOptions`).  
- Χρήση του **Aspose.HTML** για λήψη πλήρων screenshots σελίδας για visual regression testing.  

## Συμπέρασμα

Σας δείξαμε πώς να **get HTML title java** αξιόπιστα δημιουργώντας ένα sandbox που **set screen width java**, φορτώνοντας μια απομακρυσμένη σελίδα, και στη συνέχεια **extract page title java** με μια μόνο κλήση μεθόδου. Το παράδειγμα είναι πλήρες, εκτελείται αμέσως, και δείχνει γιατί ο έλεγχος του viewport είναι σημαντικός για καθοριστικά αποτελέσματα.

Δοκιμάστε το, τροποποιήστε τις διαστάσεις της οθόνης, και δείτε πώς οι τίτλοι αλλάζουν ανάμεσα στα breakpoints. Όταν νιώσετε άνετα, επεκτείνετε το μοτίβο για να εξάγετε meta descriptions, Open Graph tags, ή ακόμη και πλήρη DOM fragments. Καλή προγραμματιστική, και οι τίτλοι σας να είναι πάντα ακριβείς! 

![Get HTML title Java example output](https://example.com/images/get-html-title-java.png "Get HTML title Java – console output showing the extracted title")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
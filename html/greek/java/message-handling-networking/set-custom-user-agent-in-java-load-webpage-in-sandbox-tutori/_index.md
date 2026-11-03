---
category: general
date: 2026-04-09
description: Ορίστε προσαρμοσμένο user agent σε Java για τη φόρτωση ιστοσελίδας σε
  sandbox. Μάθετε βήμα‑βήμα πώς να ορίσετε το user agent σε Java και να προσομοιώσετε
  κινητές συσκευές.
draft: false
keywords:
- set custom user agent
- set user agent java
- load webpage in sandbox
- Aspose HTML sandbox
- Java web automation
language: el
og_description: Ορίστε προσαρμοσμένο user agent στη Java για να φορτώσετε τη σελίδα
  σε sandbox. Ακολουθήστε αυτόν τον οδηγό για να ορίσετε το user agent στη Java, να
  προσομοιώσετε συσκευές και να εξάγετε δεδομένα της σελίδας.
og_title: Ρύθμιση προσαρμοσμένου user agent στη Java – Πλήρης οδηγός Sandbox
tags:
- Aspose.HTML
- Java
- Web Scraping
title: Ορισμός προσαρμοσμένου user agent σε Java – Φόρτωση ιστοσελίδας σε sandbox
  tutorial
url: /el/java/message-handling-networking/set-custom-user-agent-in-java-load-webpage-in-sandbox-tutori/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ορισμός προσαρμοσμένου user agent σε Java – Φόρτωση ιστοσελίδας σε sandbox

Έχετε χρειαστεί ποτέ να **set custom user agent in Java** αλλά δεν ήξερες πώς να κάνεις τον στόχο να πιστεύει ότι είσαι κινητό πρόγραμμα περιήγησης; Δεν είστε ο μόνος. Πολλοί ιστότοποι σερβίρουν διαφορετικό HTML ή ακόμη και μπλοκάρουν αιτήματα εκτός εάν η κεφαλίδα *User‑Agent* φαίνεται γνωστή. Τα καλά νέα; Με το Aspose.HTML μπορείτε να **set custom user agent** μέσα σε sandbox, να φορτώσετε τη σελίδα και να εργαστείτε με το DOM ακριβώς όπως αν μια πραγματική συσκευή το είχε αποδώσει.

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει πώς να **set user agent java**, να διαμορφώσετε ένα sandbox για εξομοίωση iPhone, και στη συνέχεια να **load webpage in sandbox**. Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Java και να ξεκινήσετε το scraping ή το testing αμέσως.

## Τι θα χρειαστείτε

- Java 17 ή νεότερη (ο κώδικας χρησιμοποιεί το σύγχρονο σύστημα modules, αλλά παλαιότερα JDK λειτουργούν με μικρές προσαρμογές)  
- Aspose.HTML for Java (η πιο πρόσφατη έκδοση τη στιγμή της συγγραφής, 23.10)  
- Ένα απλό IDE ή επεξεργαστή κειμένου· δεν απαιτείται Maven/Gradle για το απόσπασμα, αλλά θα χρειαστεί το JAR στο classpath  
- Πρόσβαση στο Internet για το παράδειγμα URL (`https://example.com`)

Αυτό είναι όλο—χωρίς επιπλέον servers, χωρίς headless browsers, μόνο λίγες γραμμές καθαρού Java.

![Παράδειγμα προσαρμοσμένου user agent](https://example.com/image.png "προσαρμοσμένος user agent σε Java sandbox")

## Βήμα 1: Διαμόρφωση του sandbox – το μέρος όπου **set custom user agent**

Το sandbox είναι ένα ελαφρύ, απομονωμένο περιβάλλον που μιμείται ένα πρόγραμμα περιήγησης. Πρώτα δημιουργούμε ένα αντικείμενο `SandboxOptions` και του λέμε ποιο μέγεθος οθόνης και ποια συμβολοσειρά *User‑Agent* θέλουμε.

```java
import com.aspose.html.sandbox.SandboxOptions;

// Step 1 – define sandbox options
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);               // iPhone width in CSS pixels
sandboxOptions.setScreenHeight(667);              // iPhone height
sandboxOptions.setUserAgent(
        "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
        "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.0 Mobile/15E148 Safari/604.1");
```

**Why this matters:** Η κλήση `setUserAgent` είναι το σημείο όπου **set custom user agent**. Αν ταιριάξετε τη συμβολοσειρά ενός πραγματικού συσκευής, πείθετε τον server να σερβίρει τη mobile διάταξη, η οποία συχνά περιέχει πιο απλό markup—χρήσιμο για scraping ή UI testing.

## Βήμα 2: Εκκίνηση της παρουσίας sandbox

Τώρα που οι επιλογές είναι έτοιμες, τις παραδίδουμε στο `HtmlDocumentSandbox`. Αυτό το αντικείμενο θα επιβάλει τις ρυθμίσεις για όλα όσα εκτελούνται μέσα του.

```java
import com.aspose.html.sandbox.HtmlDocumentSandbox;

// Step 2 – create the sandbox with our options
HtmlDocumentSandbox sandbox = new HtmlDocumentSandbox(sandboxOptions);
```

**Pro tip:** Μπορείτε να επαναχρησιμοποιήσετε το ίδιο sandbox για πολλαπλές φορτώσεις σελίδων, κάτι που εξοικονομεί μνήμη σε σύγκριση με την εκκίνηση νέου προγράμματος περιήγησης κάθε φορά.

## Βήμα 3: Φόρτωση σελίδας ενώ **set user agent java** τρέχει στο παρασκήνιο

Με το sandbox ενεργό, η φόρτωση μιας σελίδας είναι τόσο απλή όσο η δημιουργία ενός `HTMLDocument`. Ο κατασκευαστής παίρνει το URL και το sandbox που μόλις δημιουργήσαμε.

```java
import com.aspose.html.HTMLDocument;

// Step 3 – load the target page inside the sandbox
HTMLDocument htmlDoc = new HTMLDocument("https://example.com", sandbox);
```

Σε αυτό το σημείο το αίτημα έχει ήδη μεταφέρει την προσαρμοσμένη κεφαλίδα *User‑Agent*. Αν ελέγξετε την κίνηση δικτύου (π.χ., με Wireshark ή proxy), θα δείτε ακριβώς τη συμβολοσειρά που ορίσαμε νωρίτερα.

## Βήμα 4: Επαλήθευση ότι η σελίδα φορτώθηκε σωστά – το αποτέλεσμα του **load webpage in sandbox**

Ας εξάγουμε τον τίτλο από το έγγραφο για να αποδείξουμε ότι όλα λειτούργησαν. Αυτό επίσης δείχνει πώς μπορείτε να αλληλεπιδράσετε με το DOM μετά το rendering της σελίδας.

```java
// Step 4 – read the title to confirm we loaded the page
System.out.println("Title (in sandbox): " + htmlDoc.getTitle());
```

**Expected output (may vary):**

```
Title (in sandbox): Example Domain
```

Αν δείτε τον τίτλο να εκτυπώνεται, το **load webpage in sandbox** πέτυχε και ο προσαρμοσμένος user agent εφαρμόστηκε.

## Πλήρες, εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα τα κομμάτια παίρνετε μια μοναδική κλάση που μπορείτε να μεταγλωττίσετε και να τρέξετε:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.HtmlDocumentSandbox;
import com.aspose.html.sandbox.SandboxOptions;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Configure the sandbox to emulate a mobile device
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);   // iPhone width in CSS pixels
        sandboxOptions.setScreenHeight(667);
        sandboxOptions.setUserAgent(
                "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 2: Create a sandbox instance with the configured options
        HtmlDocumentSandbox sandbox = new HtmlDocumentSandbox(sandboxOptions);

        // Step 3: Load the web page inside the sandboxed environment
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com", sandbox);

        // Step 4: Work with the document as if it were rendered on the simulated device
        System.out.println("Title (in sandbox): " + htmlDoc.getTitle());
    }
}
```

Μεταγλώττιση με:

```bash
javac -cp "path/to/aspose-html.jar" SandboxExample.java
java -cp ".:path/to/aspose-html.jar" SandboxExample
```

Αντικαταστήστε το `path/to/aspose-html.jar` με την πραγματική θέση του αρχείου Aspose.HTML JAR.

## Συνηθισμένες παραλλαγές και ειδικές περιπτώσεις

### Χρήση διαφορετικού προφίλ συσκευής

Αν χρειαστεί να **set custom user agent** για Android tablet, απλώς αλλάξτε τις διαστάσεις της οθόνης και τη συμβολοσειρά user‑agent:

```java
sandboxOptions.setScreenWidth(800);
sandboxOptions.setScreenHeight(1280);
sandboxOptions.setUserAgent(
        "Mozilla/5.0 (Linux; Android 12; SM-G991U) " +
        "AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.5249.91 Mobile Safari/537.36");
```

### Διαχείριση ανακατευθύνσεων

Το Aspose.HTML ακολουθεί αυτόματα τις ανακατευθύνσεις, αλλά η κεφαλίδα *User‑Agent* διατηρείται μόνο αν παραμείνετε στο ίδιο sandbox. Αν δημιουργήσετε νέο `HTMLDocument` για κάθε ανακατεύθυνση, θυμηθείτε να περάσετε το ίδιο αντικείμενο `sandbox`.

### Φόρτωση HTTPS ιστοτόπων με αυτο-υπογεγραμμένα πιστοποιητικά

Για εσωτερικό testing μπορεί να χρειαστείτε πρόσβαση σε site με αυτο‑υπογεγραμμένο cert. Μπορείτε να χαλαρώσετε την επικύρωση του πιστοποιητικού τροποποιώντας το `SandboxOptions`:

```java
sandboxOptions.setIgnoreCertificateErrors(true);
```

Χρησιμοποιήστε το μόνο σε αξιόπιστα περιβάλλοντα· διαφορετικά μειώνει την ασφάλεια.

## Συμβουλές και παγίδες

- **Pro tip:** Κρατήστε το sandbox ενεργό για batch jobs. Η δημιουργία και καταστροφή του ανά αίτημα προσθέτει overhead.
- **Watch out for:** Κάποιοι ιστότοποι ελέγχουν επιπλέον κεφαλίδες (π.χ., `Accept-Language`). Αν συνεχίσουν να σας μπλοκάρουν, προσθέστε αυτές τις κεφαλίδες μέσω `sandboxOptions.getHeaders().add("Accept-Language", "en-US")`.
- **Performance note:** Το sandbox τρέχει εντός της ίδιας διεργασίας, έτσι η χρήση μνήμης είναι μέτρια σε σύγκριση με πλήρη browsers όπως το Selenium. Ωστόσο, πολύ μεγάλες σελίδες μπορούν ακόμη να καταναλώσουν σημαντικό RAM—παρακολουθήστε το αν σκοπεύετε να φορτώσετε δεκάδες σελίδες ταυτόχρονα.

## Συμπέρασμα

Τώρα ξέρετε πώς να **set custom user agent in Java**, να διαμορφώσετε ένα sandbox, και να **load webpage in sandbox** χρησιμοποιώντας το Aspose.HTML. Ο πλήρης κώδικας παραπάνω δείχνει όλη τη ροή—from τον ορισμό του `SandboxOptions` μέχρι την εκτύπωση του τίτλου της σελίδας—ώστε να μπορείτε να το αντιγράψετε, να το επικολλήσετε και να το τρέξετε αμέσως.

Στη συνέχεια, σκεφτείτε να επεκτείνετε το παράδειγμα για εξαγωγή συγκεκριμένων στοιχείων (`htmlDoc.getElementById(...)`), λήψη screenshots (`sandbox.getScreenCapture()`), ή αλυσίδωση πολλαπλών URLs για εργασία crawling. Όλες αυτές οι εργασίες ωφελούνται από την ίδια τεχνική **set user agent java** που μόλις μάθατε.

Νιώστε ελεύθεροι να πειραματιστείτε με διαφορετικές συμβολοσειρές συσκευών, μεγέθη οθόνης ή ακόμη και προσαρμοσμένες κεφαλίδες. Όσο περισσότερο παίζετε, τόσο καλύτερα θα καταλάβετε πώς αντιδρούν οι servers σε διάφορους agents—μια κρίσιμη δεξιότητα για web automation, testing και εξαγωγή δεδομένων.

Καλή προγραμματιστική, και οι αιτήσεις σας πάντα να γίνονται δεκτές!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
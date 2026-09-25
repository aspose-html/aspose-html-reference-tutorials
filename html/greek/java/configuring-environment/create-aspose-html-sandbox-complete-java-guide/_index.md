---
category: general
date: 2026-09-03
description: Πώς να δημιουργήσετε Aspose sandbox java και να ανακτήσετε τον τίτλο
  της σελίδας java με καθαρή, απομονωμένη φόρτωση HTML. Οδηγός βήμα‑βήμα με εκτελέσιμο
  κώδικα.
draft: false
keywords:
- create aspose sandbox java
- retrieve page title java
- aspose html sandbox options
- java html sandbox example
- aspose html document title
lastmod: 2026-09-03
og_description: Μάθετε πώς να δημιουργήσετε ένα Aspose sandbox σε Java και να ανακτήσετε
  αμέσως τον τίτλο της σελίδας java. Λεπτομερή βήματα, βέλτιστες πρακτικές και πλήρης
  κώδικας παραδείγματος.
og_image_alt: Screenshot of Java code creating an Aspose HTML sandbox in Eclipse
og_title: Πώς να δημιουργήσετε Aspose sandbox java – πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-09-03'
  description: How to create Aspose sandbox java and retrieve page title java with
    a clean, isolated HTML load. Step‑by‑step guide with runnable code.
  headline: How to create Aspose sandbox java – complete guide
  type: TechArticle
- questions:
  - answer: Yes. The sandbox runs without a visible UI and can be executed on any
      server that supports Java 8+.
    question: Can I use this sandbox in a headless CI pipeline?
  - answer: Absolutely. It uses Chromium under the hood, so modern JavaScript, including
      ES6 features, runs correctly.
    question: Does the sandbox support JavaScript execution?
  - answer: The engine can render pages up to 200 MB in size, limited only by the
      host machine’s memory.
    question: How large a page can the sandbox handle?
  - answer: You can customize the `User-Agent` string in `SandboxOptions` or supply
      cookies via `HtmlLoadOptions` to mimic a regular browser.
    question: What if the target site blocks automated requests?
  - answer: Yes. After loading the document, call `document.save("snapshot.png", SaveFormat.Png);`
      to export a PNG image of the rendered page.
    question: Is there a way to capture a screenshot of the loaded page?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- Web scraping
- Sandbox
title: Πώς να δημιουργήσετε Aspose sandbox java – πλήρης οδηγός
url: /el/java/configuring-environment/create-aspose-html-sandbox-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε Aspose sandbox java – πλήρης οδηγός

Ever needed to **create Aspose HTML sandbox** but weren’t sure how to keep the loaded page isolated from your main JVM? Maybe you’re building a web‑scraper, a testing harness, or just want to experiment with remote pages without risking side‑effects. In this tutorial we’ll walk through exactly that, and we’ll also show you **how to retrieve page title java** from inside the sandbox.  

The solution is pretty straightforward: configure a `SandboxOptions` object, spin up a `Sandbox`, load an external URL with `HtmlDocument`, read the title, and finally clean everything up. By the end you’ll have a self‑contained snippet you can drop into any Java project that uses Aspose.HTML for Java 23.1 (or newer).

## Σύντομες απαντήσεις
- **What is an Aspose sandbox?** Είναι ένα απομονωμένο περιβάλλον βασισμένο σε Chromium που εκτελείται μέσα στη JVM σας χωρίς να αγγίζει το σύστημα αρχείων.  
- **Why use a sandbox for page title extraction?** Εγγυάται ότι τα εξωτερικά scripts δεν μπορούν να επηρεάσουν την κατάσταση ή τη μνήμη της εφαρμογής σας.  
- **Which Java version is required?** Java 8 ή νεότερη· η βιβλιοθήκη λειτουργεί επίσης με Java 11, 17 και μεταγενέστερες.  
- **Do I need a license?** Μια δωρεάν δοκιμαστική άδεια είναι επαρκής για ανάπτυξη· απαιτείται εμπορική άδεια για παραγωγή.  
- **How many lines of code are needed?** Λιγότερες από 30 γραμμές για τη βασική λογική, συν προαιρετικό κώδικα ρύθμισης.

## Τι είναι το create aspose sandbox java;
`Sandbox` είναι η ελαφριά, απομονωμένη μηχανή περιήγησης του Aspose.HTML που εκτελείται μέσα στη διαδικασία Java. Παρέχει ένα ασφαλές κοντέινερ όπου μπορείτε να φορτώσετε απομακρυσμένο HTML, να εκτελέσετε JavaScript και να αλληλεπιδράσετε με το DOM χωρίς να εκθέτετε το περιβάλλον υποδοχής.

## Γιατί να χρησιμοποιήσετε sandbox όταν ανακτάτε τον τίτλο της σελίδας java;
Το Aspose.HTML υποστηρίζει **50+ μορφές εισόδου και εξόδου** και μπορεί να αποδώσει έγγραφα πολλαπλών εκατοντάδων σελίδων χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη. Η χρήση sandbox προσθέτει ένα επιπλέον επίπεδο ασφαλείας, εξασφαλίζοντας ότι οποιοδήποτε κακόβουλο script στη σελίδα-στόχο δεν μπορεί να διαφύγει από το κοντέινερ. Αυτή η προσέγγιση μειώνει τον κίνδυνο διαρροών μνήμης και προστατεύει τη JVM σας από ανεπιθύμητες επιδράσεις.

## Προαπαιτούμενα
- Άδεια Aspose.HTML for Java έγκυρη (η δοκιμαστική λειτουργεί για δοκιμές).  
- Java 8 ή νεότερη εγκατεστημένη στο μηχάνημά σας.  
- Εργαλείο κατασκευής Maven ή Gradle για διαχείριση εξαρτήσεων.  

> **Pro tip:** Διατηρήστε την έκδοση της βιβλιοθήκης ευθυγραμμισμένη με τις επίσημες σημειώσεις έκδοσης του Aspose· οι νεότερες εκδόσεις περιλαμβάνουν διορθώσεις ασφαλείας που είναι κρίσιμες όταν φορτώνετε μη αξιόπιστο περιεχόμενο.

## Βήμα 1: ρυθμίστε το έργο σας

Πριν βυθιστούμε στον κώδικα, βεβαιωθείτε ότι το `pom.xml` (Maven) ή το αρχείο Gradle περιλαμβάνει την εξάρτηση Aspose.HTML:

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.1</version>
</dependency>
```

Αν χρησιμοποιείτε Gradle:

```groovy
implementation 'com.aspose:aspose-html:23.1'
```

> **Pro tip:** Διατηρήστε την έκδοση της βιβλιοθήκης σε συγχρονισμό με τις επίσημες σημειώσεις έκδοσης του Aspose· οι νεότερες εκδόσεις προσθέτουν διορθώσεις ασφαλείας που είναι ιδιαίτερα σημαντικές όταν φορτώνετε εξωτερικό περιεχόμενο.

## Πώς να διαμορφώσετε τις επιλογές sandbox; (retrieve page title java)

Το πρώτο πραγματικό βήμα στη **δημιουργία ενός Aspose HTML sandbox** είναι να αποφασίσετε πώς πρέπει να συμπεριφέρεται ο εικονικός περιηγητής. Μπορείτε να μιμηθείτε ένα desktop, μια κινητή συσκευή ή ακόμη και ένα προσαρμοσμένο μέγεθος οθόνης.  
`SandboxOptions` διαμορφώνει τη συμπεριφορά του sandbox, όπως το μέγεθος του viewport, τη συμβολοσειρά user‑agent και τις τιμές timeout. Σας επιτρέπει να ελέγξετε πώς αποδίδεται η σελίδα και ποιοι πόροι επιτρέπονται.

```java
import com.aspose.html.sandbox.SandboxOptions;

// Step 1 – configure viewport and user‑agent
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setViewportWidth(800);   // emulate an 800 px wide screen
sandboxOptions.setViewportHeight(600); // height of the virtual viewport
sandboxOptions.setUserAgent("AsposeHTML/1.0"); // custom user‑agent string
```

Γιατί είναι σημαντικό αυτό; Το μέγεθος του viewport επηρεάζει τα CSS media queries, ενώ το user‑agent μπορεί να επηρεάσει τη διαπραγμάτευση περιεχομένου από τον διακομιστή. Ορίζοντάς τα ρητά, διασφαλίζετε ότι η σελίδα από την οποία αργότερα **retrieve page title java** θα αποδοθεί ακριβώς όπως περιμένετε.

## Πώς να δημιουργήσετε το στιγμιότυπο sandbox;

Τώρα που έχουμε τις επιλογές μας, μπορούμε να δημιουργήσουμε το sandbox.  
`Sandbox` είναι το απομονωμένο στιγμιότυπο της μηχανής Chromium που εκτελείται μέσα στη JVM. Δημιουργεί ένα ασφαλές περιβάλλον όπου το HTML μπορεί να φορτωθεί και να εκτελεστεί χωρίς να αγγίζει το σύστημα αρχείων του κεντρικού υπολογιστή.

```java
import com.aspose.html.sandbox.Sandbox;

// Step 2 – create the sandbox using the options above
Sandbox sandboxInstance = new Sandbox(sandboxOptions);
```

Σκεφτείτε το `Sandbox` ως μια ελαφριά, απομονωμένη μηχανή Chromium που ζει μέσα στη διαδικασία Java. Δεν αγγίζει το σύστημα αρχείων εκτός εάν το υποδείξετε ρητά, κάτι που το καθιστά ιδανικό για ασφαλή scraping.

## Πώς να φορτώσετε μια εξωτερική σελίδα μέσα στο sandbox;

Με το sandbox έτοιμο, η φόρτωση μιας απομακρυσμένης σελίδας είναι τόσο απλή όσο η μεταβίβαση του URL και του στιγμιότυπου sandbox στο `HtmlDocument`.  
`HtmlDocument` αντιπροσωπεύει μια σελίδα HTML που φορτώνεται στο sandbox, παρέχοντας πρόσβαση στο DOM, δυνατότητες απόδοσης και εκτέλεση JavaScript.

```java
import com.aspose.html.HtmlDocument;

// Step 3 – load a remote HTML page (example.com is used for demo)
HtmlDocument htmlDoc = new HtmlDocument("https://example.com", sandboxInstance);
```

> **Edge case:** Εάν ο στόχος απαιτεί έλεγχο ταυτότητας ή ανακατευθύνσεις, μπορείτε να προ‑ρυθμίσετε χειριστές `HttpClient` και να τους περάσετε μέσω `HtmlLoadOptions`. Αυτό είναι εκτός του πλαισίου αυτού του γρήγορου οδηγού, αλλά το API το υποστηρίζει.

## Πώς να αποκτήσετε τον τίτλο της σελίδας; (retrieve page title java)

Τώρα έρχεται το μέρος που ζητήσατε: η εξαγωγή του τίτλου της σελίδας ενώ παραμένετε μέσα στο sandbox. Η κλάση `HtmlDocument` εκθέτει τη μέθοδο `getTitle()` που διαβάζει το στοιχείο `<title>`.  
`getTitle()` επιστρέφει το κείμενο του στοιχείου `<title>` της σελίδας, παρέχοντάς σας έναν απλό τρόπο να επαληθεύσετε ότι η σελίδα φορτώθηκε σωστά.

```java
// Step 4 – read and print the title
System.out.println("Title inside sandbox: " + htmlDoc.getTitle());
```

Όταν εκτελέσετε το πλήρες πρόγραμμα εναντίον του `https://example.com`, θα πρέπει να δείτε:

```
Title inside sandbox: Example Domain
```

Αυτή η γραμμή αποδεικνύει ότι δημιουργήσαμε επιτυχώς **ένα Aspose HTML sandbox**, φορτώσαμε μια απομακρυσμένη σελίδα και **ανακτήσαμε τον τίτλο της σελίδας java** χωρίς ποτέ να βγούμε από το απομονωμένο περιβάλλον.

## Πώς να καθαρίσετε τους πόρους;

Τα αντικείμενα Aspose.HTML διατηρούν εγγενείς πόρους, επομένως είναι κρίσιμο να τα απελευθερώνετε ρητά. Η παράλειψη μπορεί να οδηγήσει σε διαρροές μνήμης, ειδικά όταν επεξεργάζεστε πολλές σελίδες σε βρόχο.  
`dispose()` απελευθερώνει τους εγγενείς πόρους που κρατούν τα αντικείμενα Aspose.HTML, αποτρέποντας διαρροές μνήμης και διασφαλίζοντας ότι η JVM μπορεί να ανακτήσει τη μνήμη άμεσα.

```java
// Step 5 – release native resources
htmlDoc.dispose();
sandboxInstance.dispose();
```

> **Why dispose?** Η υποκείμενη μηχανή Chromium εκχωρεί εγγενή μνήμη και χειριστές αρχείων. Η κλήση του `dispose()` λέει στη JVM να ελευθερώσει αυτά αμέσως αντί να περιμένει τους τελικούς καθαριστές.

## Πλήρες λειτουργικό παράδειγμα

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε σε ένα αρχείο με όνομα `SandboxExample.java`. Συγκεντρώστε με `javac` και εκτελέστε με `java`. Όλα τα βήματα είναι στη σωστή σειρά και κάθε εισαγωγή είναι καταχωρημένη.

```java
import com.aspose.html.HtmlDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Configure sandbox options (viewport size and user‑agent)
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setViewportWidth(800);   // emulate an 800 px wide screen
        sandboxOptions.setViewportHeight(600);
        sandboxOptions.setUserAgent("AsposeHTML/1.0");

        // Step 2: Create the sandbox using the configured options
        Sandbox sandboxInstance = new Sandbox(sandboxOptions);

        // Step 3: Load an external HTML page inside the sandbox
        HtmlDocument htmlDoc = new HtmlDocument("https://example.com", sandboxInstance);

        // Step 4: Access and display the page title (demonstrates sandbox isolation)
        System.out.println("Title inside sandbox: " + htmlDoc.getTitle());

        // Step 5: Release resources when done
        htmlDoc.dispose();
        sandboxInstance.dispose();
    }
}
```

![Στιγμιότυπο κώδικα Java που δημιουργεί ένα Aspose HTML sandbox](/images/create-aspose-html-sandbox.png "παράδειγμα δημιουργίας aspose html sandbox")

### Αναμενόμενη έξοδος

```
Title inside sandbox: Example Domain
```

Αν αντικαταστήσετε το `https://example.com` με άλλο URL, ο εκτυπωμένος τίτλος θα αντανακλά το `<title>` tag της σελίδας—εφόσον ο ιστότοπος επιτρέπει ανώνυμη πρόσβαση.

## Πρακτικές συμβουλές & κοινά προβλήματα

- **Network timeouts:** Από προεπιλογή το sandbox χρησιμοποιεί timeout 60 δευτερολέπτων. Αν αντιμετωπίζετε πιο αργούς ιστότοπους, καλέστε `sandboxOptions.setTimeout(120_000);` πριν δημιουργήσετε το sandbox.  
- **Java security manager:** Όταν εκτελείται σε περιορισμένη JVM, βεβαιωθείτε ότι το `java.security.policy` χορηγεί `java.net.SocketPermission` για τον στόχο domain.  
- **Processing multiple pages:** Επαναχρησιμοποιήστε ένα μόνο στιγμιότυπο `Sandbox`; απλώς δημιουργήστε ένα νέο `HtmlDocument` για κάθε URL και απελευθερώστε το μετά. Αυτό μειώνει το κόστος εκκίνησης.  
- **Debugging:** Ορίστε `sandboxOptions.setDebugMode(true);` για να λάβετε αναλυτικά logs στην κονσόλα που μπορούν να σας βοηθήσουν να εντοπίσετε γιατί μια σελίδα δεν φορτώθηκε.

## Συχνές ερωτήσεις

**Q: Μπορώ να χρησιμοποιήσω αυτό το sandbox σε μια headless CI pipeline;**  
A: Ναι. Το sandbox εκτελείται χωρίς ορατό UI και μπορεί να εκτελεστεί σε οποιονδήποτε διακομιστή που υποστηρίζει Java 8+.

**Q: Υποστηρίζει το sandbox εκτέλεση JavaScript;**  
A: Απόλυτα. Χρησιμοποιεί Chromium στο παρασκήνιο, έτσι ώστε το σύγχρονο JavaScript, συμπεριλαμβανομένων των χαρακτηριστικών ES6, να εκτελείται σωστά.

**Q: Πόσο μεγάλη σελίδα μπορεί να χειριστεί το sandbox;**  
A: Η μηχανή μπορεί να αποδώσει σελίδες έως 200 MB, περιοριζόμενη μόνο από τη μνήμη του κεντρικού μηχανήματος.

**Q: Τι γίνεται αν ο στόχος μπλοκάρει αυτοματοποιημένα αιτήματα;**  
A: Μπορείτε να προσαρμόσετε τη συμβολοσειρά `User-Agent` στο `SandboxOptions` ή να παρέχετε cookies μέσω `HtmlLoadOptions` για να μιμηθείτε έναν κανονικό περιηγητή.

**Q: Υπάρχει τρόπος να καταγράψετε στιγμιότυπο της φορτωμένης σελίδας;**  
A: Ναι. Μετά τη φόρτωση του εγγράφου, καλέστε `document.save("snapshot.png", SaveFormat.Png);` για να εξάγετε μια εικόνα PNG της αποδομένης σελίδας.

**Τελευταία ενημέρωση:** 2026-09-03  
**Δοκιμή με:** Aspose.HTML for Java 23.1  
**Συγγραφέας:** Aspose

## Σχετικά μαθήματα

- [Πώς να χρησιμοποιήσετε Sandbox για Html σε Pdf Java – Οδηγός βήμα προς βήμα](/html/java/advanced-usage/how-to-use-sandbox-for-html-to-pdf-java-step-by-step-guide/)
- [Δημιουργία PDF από HTML χρησιμοποιώντας Aspose.HTML for Java – Sandbox](/html/java/configuring-environment/implement-sandboxing/)
- [Ενεργοποίηση εκτέλεσης script σε Java – Πλήρης οδηγός Aspose Html](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
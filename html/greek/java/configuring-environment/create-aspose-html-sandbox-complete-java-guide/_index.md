---
category: general
date: 2026-01-04
description: Δημιουργήστε ένα sandbox Aspose HTML σε Java και μάθετε πώς να ανακτήσετε
  τον τίτλο της σελίδας σε Java με ένα βήμα‑βήμα παράδειγμα. Συμπεριλαμβάνεται γρήγορος,
  εκτελέσιμος κώδικας.
draft: false
keywords:
- create aspose html sandbox
- retrieve page title java
- aspose html sandbox options
- java html sandbox example
- aspose html document title
language: el
og_description: Δημιουργήστε sandbox Aspose HTML σε Java και ανακτήστε άμεσα τον τίτλο
  της σελίδας Java. Ακολουθήστε αυτόν τον λεπτομερή οδηγό για μια καθαρή, απομονωμένη
  φόρτωση HTML.
og_title: Δημιουργία Aspose HTML Sandbox – Εγχειρίδιο Java
tags:
- Aspose.HTML
- Java
- Web Scraping
- Sandbox
title: Δημιουργία Aspose HTML Sandbox – Πλήρης Οδηγός Java
url: /el/java/configuring-environment/create-aspose-html-sandbox-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Aspose HTML Sandbox – Πλήρης Οδηγός Java

Έχετε ποτέ χρειαστεί να **create Aspose HTML sandbox** αλλά δεν ήσασταν σίγουροι πώς να διατηρήσετε τη φορτωμένη σελίδα απομονωμένη από το κύριο JVM σας; Ίσως να δημιουργείτε έναν web‑scraper, ένα testing harness, ή απλώς θέλετε να πειραματιστείτε με απομακρυσμένες σελίδες χωρίς να διακινδυνεύσετε ανεπιθύμητες επιδράσεις. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από αυτό, και επίσης θα σας δείξουμε **how to retrieve page title java** από μέσα στο sandbox.

Η λύση είναι αρκετά απλή: διαμορφώστε ένα αντικείμενο `SandboxOptions`, δημιουργήστε ένα `Sandbox`, φορτώστε ένα εξωτερικό URL με `HtmlDocument`, διαβάστε τον τίτλο και, τέλος, καθαρίστε τα πάντα. Στο τέλος θα έχετε ένα αυτόνομο απόσπασμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Java που χρησιμοποιεί Aspose.HTML for Java 23.1 (ή νεότερο).

## Τι Θα Μάθετε

- Πώς να **create Aspose HTML sandbox** με προσαρμοσμένες ρυθμίσεις viewport και user‑agent.  
- Τα ακριβή βήματα για **retrieve page title java** από απομακρυσμένη σελίδα ενώ παραμένετε ασφαλώς μέσα στο sandbox.  
- Κοινά προβλήματα (όπως η παράλειψη διαγραφής πόρων) και συμβουλές βέλτιστων πρακτικών που διατηρούν το αποτύπωμα μνήμης χαμηλό.  
- Ένα πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα Java που μπορείτε να αντιγράψετε‑επικολλήσετε, να μεταγλωττίσετε και να εκτελέσετε.

> **Prerequisites** – Χρειάζεστε μια έγκυρη άδεια Aspose.HTML for Java (λειτουργεί η δωρεάν δοκιμή) και εγκατεστημένο Java 8 ή νεότερο. Δεν απαιτούνται πρόσθετες βιβλιοθήκες τρίτων.

---

## Βήμα 1: Ρύθμιση του Έργου σας

Πριν βουτήξουμε στον κώδικα, βεβαιωθείτε ότι το `pom.xml` (Maven) ή το αρχείο Gradle περιλαμβάνει την εξάρτηση Aspose.HTML:

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

> **Pro tip:** Διατηρήστε την έκδοση της βιβλιοθήκης συγχρονισμένη με τις επίσημες σημειώσεις κυκλοφορίας της Aspose· οι νεότερες εκδόσεις προσθέτουν διορθώσεις ασφαλείας που είναι ιδιαίτερα σημαντικές κατά τη φόρτωση εξωτερικού περιεχομένου.

---

## Διαμόρφωση Sandbox Options (retrieve page title java)

Το πρώτο πραγματικό βήμα στην **creating an Aspose HTML sandbox** είναι να αποφασίσετε πώς θα συμπεριφέρεται ο εικονικός περιηγητής. Μπορείτε να μιμηθείτε ένα desktop, μια κινητή συσκευή ή ακόμη και ένα προσαρμοσμένο μέγεθος οθόνης.

```java
import com.aspose.html.sandbox.SandboxOptions;

// Step 1 – configure viewport and user‑agent
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setViewportWidth(800);   // emulate an 800 px wide screen
sandboxOptions.setViewportHeight(600); // height of the virtual viewport
sandboxOptions.setUserAgent("AsposeHTML/1.0"); // custom user‑agent string
```

Γιατί είναι σημαντικό αυτό; Το μέγεθος του viewport επηρεάζει τα CSS media queries, ενώ το user‑agent μπορεί να επηρεάσει τη διαπραγμάτευση περιεχομένου από την πλευρά του διακομιστή. Ορίζοντάς τα ρητά, διασφαλίζετε ότι η σελίδα από την οποία αργότερα **retrieve page title java** θα αποδοθεί ακριβώς όπως περιμένετε.

---

## Δημιουργία του Sandbox Instance

Τώρα που έχουμε τις επιλογές μας, μπορούμε να δημιουργήσουμε το sandbox.

```java
import com.aspose.html.sandbox.Sandbox;

// Step 2 – create the sandbox using the options above
Sandbox sandboxInstance = new Sandbox(sandboxOptions);
```

Σκεφτείτε το `Sandbox` ως μια ελαφριά, απομονωμένη μηχανή Chromium που ζει μέσα στη διαδικασία Java σας. Δεν αγγίζει το σύστημα αρχείων εκτός αν το υποδείξετε ρητά, κάτι που το καθιστά ιδανικό για ασφαλή scraping.

---

## Φόρτωση Εξωτερικής Σελίδας Μέσα στο Sandbox

Με το sandbox έτοιμο, η φόρτωση μιας απομακρυσμένης σελίδας είναι τόσο απλή όσο η μεταβίβαση του URL και της παρουσίας sandbox στο `HtmlDocument`.

```java
import com.aspose.html.HtmlDocument;

// Step 3 – load a remote HTML page (example.com is used for demo)
HtmlDocument htmlDoc = new HtmlDocument("https://example.com", sandboxInstance);
```

> **Edge case:** Αν ο στόχος απαιτεί έλεγχο ταυτότητας ή ανακατευθύνσεις, μπορείτε να προ‑ρυθμίσετε τους χειριστές `HttpClient` και να τους περάσετε μέσω `HtmlLoadOptions`. Αυτό υπερβαίνει το πεδίο εφαρμογής αυτού του σύντομου οδηγού, αλλά το API το υποστηρίζει.

---

## Πρόσβαση στον Τίτλο Σελίδας – retrieve page title java

Τώρα έρχεται το μέρος που ζητήσατε: εξαγωγή του τίτλου της σελίδας ενώ παραμένετε μέσα στο sandbox. Η κλάση `HtmlDocument` εκθέτει τη μέθοδο `getTitle()` που διαβάζει το στοιχείο `<title>`.

```java
// Step 4 – read and print the title
System.out.println("Title inside sandbox: " + htmlDoc.getTitle());
```

Όταν εκτελέσετε το πλήρες πρόγραμμα εναντίον του `https://example.com`, θα πρέπει να δείτε:

```
Title inside sandbox: Example Domain
```

Αυτή η γραμμή αποδεικνύει ότι δημιουργήσαμε επιτυχώς **created an Aspose HTML sandbox**, φορτώσαμε μια απομακρυσμένη σελίδα και **retrieved page title java** χωρίς ποτέ να βγούμε από το απομονωμένο περιβάλλον.

---

## Καθαρισμός Πόρων

Τα αντικείμενα Aspose.HTML διακρατούν εγγενείς πόρους, επομένως είναι κρίσιμο να τα απελευθερώνετε ρητά. Η παράλειψη μπορεί να οδηγήσει σε διαρροές μνήμης, ειδικά όταν επεξεργάζεστε πολλές σελίδες σε βρόχο.

```java
// Step 5 – release native resources
htmlDoc.dispose();
sandboxInstance.dispose();
```

> **Why dispose?** Η υποκείμενη μηχανή Chromium εκχωρεί εγγενή μνήμη και χειριστές αρχείων. Καλώντας `dispose()` λέτε στο JVM να ελευθερώσει αυτά αμέσως αντί να περιμένει τους τελικούς καθαριστές.

---

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε σε ένα αρχείο με όνομα `SandboxExample.java`. Μεταγλωττίστε το με `javac` και τρέξτε το με `java`. Όλα τα βήματα είναι στη σωστή σειρά και κάθε εισαγωγή (import) αναγράφεται.

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

### Αναμενόμενη Έξοδος

```
Title inside sandbox: Example Domain
```

Αν αντικαταστήσετε το `https://example.com` με άλλο URL, ο εκτυπωμένος τίτλος θα αντανακλά το `<title>` tag εκείνης της σελίδας — υπό την προϋπόθεση ότι ο ιστότοπος επιτρέπει ανώνυμη πρόσβαση.

---

## Πρακτικές Συμβουλές & Συνηθισμένα Πιθανά Προβλήματα

- **Network Timeouts:** Από προεπιλογή το sandbox χρησιμοποιεί χρονικό όριο 60 δευτερολέπτων. Αν αντιμετωπίζετε πιο αργούς ιστότοπους, καλέστε `sandboxOptions.setTimeout(120_000);` πριν δημιουργήσετε το sandbox.  
- **Java Security Manager:** Όταν εκτελείται μέσα σε περιορισμένο JVM, βεβαιωθείτε ότι το `java.security.policy` χορηγεί `java.net.SocketPermission` για τον στόχο domain.  
- **Multiple Pages:** Αν χρειάζεται να επεξεργαστείτε πολλά URLs, επαναχρησιμοποιήστε μια μόνο παρουσία `Sandbox`; απλώς δημιουργήστε ένα νέο `HtmlDocument` για κάθε URL και απελευθερώστε το μετά. Αυτό μειώνει το κόστος εκκίνησης.  
- **Debugging:** Ορίστε `sandboxOptions.setDebugMode(true);` για να λάβετε αναλυτικά logs στην κονσόλα που μπορούν να σας βοηθήσουν να εντοπίσετε γιατί μια σελίδα απέτυχε να φορτωθεί.

---

## Συμπέρασμα

Μόλις **created an Aspose HTML sandbox** σε Java, το διαμορφώσαμε για προβλέψιμο viewport, φορτώσαμε μια εξωτερική σελίδα και δείξαμε πώς να **retrieve page title java** με ασφαλή και αποδοτικό τρόπο. Η πλήρης ροή — από τη ρύθμιση επιλογών μέχρι τον καθαρισμό πόρων — είναι ενσωματωμένη σε ένα σύντομο, επαναχρησιμοποιήσιμο απόσπασμα.

Τώρα μπορείτε να πάρετε αυτό το υπόβαθρο και να το επεκτείνετε: να κάνετε scrape meta tags, να καταγράψετε screenshots, ή ακόμη και να εκτελέσετε JavaScript μέσα στο sandbox. Οι δυνατότητες είναι τόσο μεγάλες όσο το ίδιο το web.  

Έχετε ερωτήσεις σχετικά με τη διαχείριση ελέγχου ταυτότητας, ρυθμίσεων proxy, ή τη δημιουργία PDF από το sandbox; Αφήστε ένα σχόλιο και θα εξερευνήσουμε αυτά τα προχωρημένα σενάρια μαζί. Καλή προγραμματιστική!  

![Screenshot of Java code creating an Aspose HTML sandbox](/images/create-aspose-html-sandbox.png "create aspose html sandbox example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
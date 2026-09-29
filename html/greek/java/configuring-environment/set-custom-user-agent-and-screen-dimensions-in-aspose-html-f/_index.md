---
category: general
date: 2026-09-29
description: Ορίστε προσαρμοσμένο user agent στο Aspose.HTML για Java και μάθετε πώς
  να ορίσετε το εικονικό μέγεθος οθόνης για ακριβή απόδοση HTML.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom user agent
- set virtual screen size
- specify user agent
- set screen dimensions
- set screen width
language: el
lastmod: 2026-09-29
og_description: Καθορίστε προσαρμοσμένο user agent στο Aspose.HTML για Java και μάθετε
  πώς να ορίσετε το εικονικό μέγεθος οθόνης για ακριβή απόδοση HTML.
og_image_alt: Diagram showing how to set custom user agent and screen dimensions in
  a Java sandbox
og_title: Ορισμός προσαρμοσμένου πράκτορα χρήστη και διαστάσεων οθόνης στο Aspose.HTML
  για Java
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Set custom user agent in Aspose.HTML for Java and learn how to set
    virtual screen size for accurate HTML rendering.
  headline: Set custom user agent and screen dimensions in Aspose.HTML for Java
  type: TechArticle
tags:
- Aspose.HTML
- Java
- sandbox
- user agent
- screen size
title: Ορισμός προσαρμοσμένου user agent και διαστάσεων οθόνης στο Aspose.HTML για
  Java
url: /el/java/configuring-environment/set-custom-user-agent-and-screen-dimensions-in-aspose-html-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ορισμός προσαρμοσμένου user agent και διαστάσεων οθόνης στο Aspose.HTML για Java

Αν χρειάζεστε να **ορίσετε προσαρμοσμένο user agent** κατά την απόδοση HTML με το Aspose.HTML για Java, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε. Με τη ρύθμιση ενός sandbox αποκτάτε επίσης τη δυνατότητα να **ορίσετε εικονικό μέγεθος οθόνης**, εξασφαλίζοντας ότι η διάταξη ταιριάζει με το πραγματικό viewport ενός προγράμματος περιήγησης.

Θα ολοκληρώσετε αυτό το tutorial με ένα πλήρες, εκτελέσιμο πρόγραμμα που **καθορίζει user agent**, **ορίζει το πλάτος της οθόνης** και **ορίζει το ύψος της οθόνης**. Δεν απαιτούνται εξωτερικά εργαλεία—μόνο το Aspose.HTML για Java και ένα runtime Java 8+.

## Τι θα μάθετε

* Πώς να δημιουργήσετε ένα `SandboxConfiguration` για απομόνωση της απόδοσης.
* Πώς να **ορίσετε προσαρμοσμένο user agent** και γιατί είναι σημαντικό για τις ανταποκρινόμενες σελίδες.
* Πώς να **ορίσετε εικονικό μέγεθος οθόνης** (πλάτος και ύψος οθόνης) για ακριβή διάταξη.
* Πώς να φορτώσετε ένα αρχείο HTML στο sandbox και να αποθηκεύσετε το επεξεργασμένο αποτέλεσμα.
* Κοινά προβλήματα και συμβουλές βέλτιστων πρακτικών για απόδοση σε sandbox.

> **Προαπαιτούμενα** – Χρειάζεστε μια έγκυρη άδεια Aspose.HTML για Java, Java 8 ή νεότερη, και ένα IDE (IntelliJ IDEA, Eclipse ή VS Code). Το παράδειγμα χρησιμοποιεί ένα τοπικό αρχείο `input.html`, αλλά οποιοδήποτε προσβάσιμο URL λειτουργεί.

![Sandbox flow diagram](sandbox-flow.png "set custom user agent example in Java")

## Βήμα 1: Δημιουργία ρύθμισης sandbox (το θεμέλιο)

Το sandbox απομονώνει το περιβάλλον απόδοσης από το κεντρικό JVM, κάτι που είναι απαραίτητο όταν θέλετε να **ορίσετε προσαρμοσμένο user agent** ή να αλλάξετε το μέγεθος του viewport.

```java
import com.aspose.html.sandbox.SandboxConfiguration;

// Create a fresh sandbox configuration object
SandboxConfiguration sandboxConfig = new SandboxConfiguration();
```

*Γιατί αυτό το βήμα;*  
`SandboxConfiguration` περιέχει όλες τις επιλογές απόδοσης, συμπεριλαμβανομένων των **διαστάσεων οθόνης** και των **συμβολοσειρών user‑agent**. Με τη ρύθμισή του πριν τη φόρτωση του εγγράφου, εξασφαλίζετε ότι η μηχανή HTML θα τηρήσει αυτές τις ρυθμίσεις από το πρώτο αίτημα.

## Βήμα 2: Ορισμός διαστάσεων οθόνης για προσομοίωση πραγματικής συσκευής

Οι ανταποκρινόμενες ιστοσελίδες συχνά διαβάζουν `window.innerWidth` και `window.innerHeight`. Για να κάνετε τη μηχανή να πιστεύει ότι εκτελείται σε οθόνη 1024 × 768, **ορίζετε εικονικό μέγεθος οθόνης**:

```java
// Define the virtual screen size for the sandboxed document
sandboxConfig.setScreenWidth(1024);   // set screen width
sandboxConfig.setScreenHeight(768);   // set screen height
```

*Γιατί είναι σημαντικό* – Εάν παραλείψετε το **set screen dimensions**, ο renderer μπορεί να χρησιμοποιήσει προεπιλεγμένο μικρό viewport, προκαλώντας τα CSS media queries να επιλέξουν τη διάταξη για κινητά. Με την ρητή **set screen width** και **set screen height**, ελέγχετε ποιοι κανόνες CSS ενεργοποιούνται.

## Βήμα 3: Καθορισμός προσαρμοσμένης συμβολοσειράς user‑agent

Ορισμένες ιστοσελίδες παρέχουν διαφορετικό περιεχόμενο ανάλογα με την κεφαλίδα user‑agent. Για να **καθορίσετε user agent** απλώς το ορίζετε στη ρύθμιση του sandbox:

```java
// Set a custom user‑agent string that will be sent during resource loading
sandboxConfig.setUserAgent("AsposeHTML/1.0");
```

*Γιατί να χρησιμοποιήσετε προσαρμοσμένο user agent;*  
Μια προσαρμοσμένη συμβολοσειρά μπορεί να παρακάμψει τον εντοπισμό bot, να ενεργοποιήσει λειτουργίες μόνο για επιτραπέζιους υπολογιστές ή να δοκιμάσει πώς συμπεριφέρεται ένας ιστότοπος για συγκεκριμένη έκδοση προγράμματος περιήγησης. Η μηχανή Aspose προωθεί αυτήν την τιμή με κάθε αίτημα HTTP που γίνεται κατά τη φόρτωση εξωτερικών πόρων (CSS, εικόνες, scripts).

## Βήμα 4: Φόρτωση του εγγράφου HTML μέσα στο sandbox

Τώρα που το sandbox είναι πλήρως ρυθμισμένο, φορτώστε το αρχείο HTML. Ο κατασκευαστής που δέχεται διαδρομή αρχείου και ένα `SandboxConfiguration` εφαρμόζει αυτόματα όλες τις ρυθμίσεις που ορίσαμε.

```java
import com.aspose.html.HTMLDocument;

// Load the HTML file using the previously configured sandbox
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);
```

Αν χρειάζεται να φορτώσετε από απομακρυσμένο URL, αντικαταστήστε τη διαδρομή αρχείου με τη συμβολοσειρά URL—το Aspose.HTML θα συνεχίσει να σέβεται το **set custom user agent** και τις **screen dimensions**.

## Βήμα 5: Αποθήκευση του επεξεργασμένου αποτελέσματος

Αφού το έγγραφο ολοκληρώσει τη φόρτωση, μπορείτε να το αποθηκεύσετε σε οποιαδήποτε υποστηριζόμενη μορφή. Εδώ γράφουμε ένα HTML αρχείο sandboxed που αντικατοπτρίζει τυχόν αλλαγές DOM που προκλήθηκαν από τις προσαρμοσμένες ρυθμίσεις.

```java
// Save the processed document to the desired output location
document.save("YOUR_DIRECTORY/sandboxed_output.html");
```

Το αποθηκευμένο αρχείο θα περιέχει το ίδιο markup, αλλά οποιαδήποτε scripts που έλεγχαν το `navigator.userAgent` ή εξέταζαν το `window.innerWidth` θα δουν τώρα τις τιμές που παρείχατε.

## Πλήρες, εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα τα βήματα μαζί, έχετε ένα αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε, να επικολλήσετε και να εκτελέσετε.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.SandboxConfiguration;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox configuration to isolate the rendering environment
        SandboxConfiguration sandboxConfig = new SandboxConfiguration();

        // Step 2: Define the virtual screen size for the sandboxed document
        sandboxConfig.setScreenWidth(1024);   // set screen width
        sandboxConfig.setScreenHeight(768);   // set screen height

        // Step 3: Set a custom user‑agent string to be used during loading
        sandboxConfig.setUserAgent("AsposeHTML/1.0"); // set custom user agent

        // Step 4: Load the HTML document within the sandbox using the configuration
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);

        // Step 5: Save the processed document to the desired output location
        document.save("YOUR_DIRECTORY/sandboxed_output.html");
    }
}
```

### Αναμενόμενο αποτέλεσμα

Η εκτέλεση του προγράμματος δημιουργεί το `sandboxed_output.html`. Αν το ανοίξετε σε έναν περιηγητή και ελέγξετε το `navigator.userAgent` μέσω της κονσόλας, θα δείτε **AsposeHTML/1.0**. Ομοίως, το `window.innerWidth` θα εμφανίσει **1024**, επιβεβαιώνοντας ότι το **set screen dimensions** λειτούργησε όπως αναμενόταν.

## Συχνές ερωτήσεις & αντιμετώπιση ειδικών περιπτώσεων

| Ερώτηση | Απάντηση |
|----------|--------|
| **Τι γίνεται αν η σελίδα φορτώνει πρόσθετους πόρους από διαφορετικό domain;** | Το sandbox προωθεί το **custom user agent** με κάθε αίτημα, αλλά οι πολιτικές cross‑origin εξακολουθούν να ισχύουν. Χρησιμοποιήστε `sandboxConfig.setAllowCrossDomain(true)` εάν χρειάζεται να χαλαρώσετε αυτούς τους περιορισμούς. |
| **Μπορώ να αλλάξω το μέγεθος της οθόνης μετά τη φόρτωση του εγγράφου;** | Όχι. Οι διαστάσεις της οθόνης διαβάζονται κατά τη διάρκεια του αρχικού βήματος διάταξης. Για να αποδώσετε με διαφορετικό μέγεθος, δημιουργήστε ένα νέο `SandboxConfiguration` και φορτώστε ξανά το έγγραφο. |
| **Χρειάζεται να καλέσω `document.close()`;** | Το `HTMLDocument` υλοποιεί το `AutoCloseable`. Η χρήση ενός μπλοκ try‑with‑resources εξασφαλίζει σωστό καθαρισμό, αλλά η ρητή κλήση `close()` είναι προαιρετική σε απλά scripts. |
| **Πώς διαφέρει αυτό από τον ορισμό user‑agent σε HTTP client;** | Ο ορισμός του user‑agent στο sandbox επηρεάζει **όλες** τις αιτήσεις πόρων που κάνει η μηχανή HTML, όχι μόνο την αρχική λήψη του HTML. Αυτό προσομοιώνει πιο πιστά έναν πραγματικό περιηγητή. |
| **Είναι το sandbox ασφαλές για μη αξιόπιστο HTML;** | Ναι. Το sandbox απομονώνει την πρόσβαση στο σύστημα αρχείων και περιορίζει τις κλήσεις δικτύου σύμφωνα με τη ρύθμιση, μειώνοντας τον κίνδυνο κακόβουλων scripts να επηρεάσουν το κεντρικό JVM. |

## Συμβουλές επαγγελματιών

* **Επαναχρησιμοποίηση ρυθμίσεων** – Εάν αποδίδετε πολλές σελίδες με το ίδιο viewport, δημιουργήστε ένα μόνο `SandboxConfiguration` και επαναχρησιμοποιήστε το για να αποφύγετε το κόστος δημιουργίας αντικειμένων.
* **Ανίχνευση με logging** – Ενεργοποιήστε το logging του Aspose.HTML (`sandboxConfig.setLogLevel(LogLevel.DEBUG)`) για να δείτε ποιοι πόροι λήφθηκαν με το προσαρμοσμένο user‑agent.
* **Συνδυασμός με CSS media queries** – Ρυθμίζοντας το **set screen width** μπορείτε να δοκιμάσετε πώς η ανταποκρινόμενη σχεδίασή σας συμπεριφέρεται σε tablets, κινητά ή μεγάλα desktop χωρίς να ανοίξετε πραγματικό περιηγητή.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **ορίσετε προσαρμοσμένο user agent** και **ορίσετε διαστάσεις οθόνης** κατά την απόδοση HTML με το Aspose.HTML για Java. Με τη ρύθμιση ενός sandbox, απομονώνετε το περιβάλλον, ελέγχετε το viewport και διασφαλίζετε ότι οι εξωτερικοί πόροι βλέπουν τις ακριβείς κεφαλίδες που ορίζετε. Αυτή η τεχνική είναι απαραίτητη για τη δοκιμή ανταποκρινόμενων διατάξεων, την παράκαμψη φραγμών bot ή την αναπαραγωγή λειτουργιών μόνο για επιτραπέζιους υπολογιστές σε αυτοματοποιημένες διαδικασίες.

Στη συνέχεια, μπορείτε να εξερευνήσετε **πώς να ορίσετε προσαρμοσμένα cookies** ή **πώς να καταγράψετε screenshots της απόδοσης** χρησιμοποιώντας το API απόδοσης του Aspose.HTML—και τα δύο concepts βασίζονται στο ίδιο πρότυπο ρύθμισης sandbox που μόλις μάθατε.

Καλή προγραμματιστική!

## Τι θα πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [High DPI Rendering in Java – Capture Webpage Screenshots with Custom User Agent](/html/english/java/conversion-html-to-various-image-formats/high-dpi-rendering-in-java-capture-webpage-screenshots-with/)
- [How to Load HTML, Set Device DPI & Read Background Color](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Create HTML File Java & Set Up Network Service (Aspose.HTML)](/html/english/java/configuring-environment/setup-network-service/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
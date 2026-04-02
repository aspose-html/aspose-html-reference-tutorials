---
category: general
date: 2026-04-02
description: Μάθετε πώς να ορίζετε το DPI, το μέγεθος του viewport και το user agent
  στο Aspose.HTML Sandbox. Παράδειγμα Java βήμα‑προς‑βήμα με πλήρη κώδικα και συμβουλές.
draft: false
keywords:
- how to set dpi
- set viewport size
- set user agent
- Aspose.HTML sandbox
- Java rendering settings
language: el
og_description: Μάθετε πώς να ορίζετε DPI, μέγεθος viewport και user agent στο Aspose.HTML
  Sandbox με ένα πλήρες παράδειγμα Java.
og_title: Πώς να ορίσετε DPI στο Aspose.HTML Sandbox – Οδηγός Java
tags:
- Aspose.HTML
- Java
- Rendering
- Sandbox
title: Πώς να ορίσετε το DPI στο Aspose.HTML Sandbox – Πλήρης οδηγός Java
url: /el/java/configuring-environment/how-to-set-dpi-in-aspose-html-sandbox-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ορίσετε DPI στο Aspose.HTML Sandbox – Πλήρης Οδηγός Java

Έχετε αναρωτηθεί ποτέ **πώς να ορίσετε DPI** κατά την απόδοση μιας ιστοσελίδας με Aspose.HTML; Δεν είστε ο μόνος. Σε πολλές δοκιμαστικές καταστάσεις χρειάζεται η διάταξη να ταιριάζει με μια συγκεκριμένη πυκνότητα οθόνης — σκεφτείτε PDF έτοιμα για εκτύπωση ή στιγμιότυπα υψηλής ανάλυσης. Τα καλά νέα είναι ότι το sandbox του Aspose.HTML σας επιτρέπει να ελέγχετε το DPI, το μέγεθος του viewport και ακόμη και τη συμβολοσειρά user‑agent σε ένα κομψό πακέτο.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πρακτικό παράδειγμα Java που **ορίζει DPI**, **ορίζει μέγεθος viewport** και **ορίζει user agent** ταυτόχρονα. Στο τέλος θα έχετε ένα εκτελέσιμο πρόγραμμα, θα καταλάβετε γιατί κάθε ρύθμιση είναι σημαντική και θα είστε έτοιμοι να προσαρμόσετε το sandbox για τα δικά σας έργα.

---

## Τι Θα Χρειαστεί

- **Java 17** (ή οποιοδήποτε πρόσφατο JDK· το API είναι συμβατό με Java 8+)
- **Aspose.HTML for Java** βιβλιοθήκη (έκδοση 23.12 ή νεότερη)
- Ένα IDE ή απλός επεξεργαστής κειμένου + μεταγλώττιση από τη γραμμή εντολών
- Πρόσβαση στο διαδίκτυο για το δείγμα URL (`https://example.com`)

Δεν απαιτούνται εξωτερικά εργαλεία κατασκευής· ο κώδικας μεταγλωττίζεται με `javac` και εκτελείται με `java`. Αν προτιμάτε Maven ή Gradle, απλώς προσθέστε την εξάρτηση Aspose.HTML — τίποτα περίπλοκο.

---

## Βήμα 1: Δημιουργία Sandbox που Ορίζει το Περιβάλλον Απόδοσης

Το sandbox είναι το σημείο όπου λέτε στο Aspose.HTML τι «οθόνη» προσποιείστε ότι έχετε. Εδώ ορίζουμε ένα **viewport 1024 × 768**, ένα **DPI 96** και μια προσαρμοσμένη **συμβολοσειρά user‑agent**.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Define the sandbox – this is the core of how to set dpi, viewport, and user agent.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent
```

**Γιατί είναι σημαντικό:**  
- **DPI** επηρεάζει το πώς οι μονάδες CSS `pt` μετατρέπονται σε pixel· υψηλότερο DPI προσφέρει πιο οξεία απόδοση.  
- **Μέγεθος viewport** καθορίζει τα σημεία διακοπής (breakpoints) που θα ενεργοποιήσει το responsive CSS.  
- **User‑agent** μπορεί να προκαλέσει παραλλαγές περιεχομένου από τον διακομιστή (mobile vs desktop).

> **Pro tip:** Αν αργότερα δημιουργείτε PDF, ταιριάξτε το DPI με την επιθυμητή ανάλυση εκτύπωσης (π.χ., 300 dpi για εκτυπώσεις υψηλής ποιότητας).

---

## Βήμα 2: Φόρτωση Ιστοσελίδας Μέσα στο Sandbox

Τώρα κατευθύνουμε το sandbox σε ένα URL. Ο κατασκευαστής `HTMLDocument` δέχεται το sandbox, ώστε η μηχανή διάταξης να σέβεται τις ρυθμίσεις που ορίσαμε.

```java
        // Load the page using the sandbox we just configured.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {
```

**Τι συμβαίνει στο παρασκήνιο;**  
Το Aspose.HTML δημιουργεί ένα απομονωμένο περιβάλλον απόδοσης, παρόμοιο με έναν headless browser, αλλά χωρίς το βάρος μιας πλήρους εγκατάστασης Chromium. Αυτό κάνει τη λειτουργία γρήγορη και ελαφριά σε μνήμη — ιδανική για επεξεργασία παρτίδων.

---

## Βήμα 3: Αλληλεπίδραση με το DOM – Ανάγνωση Τίτλου Σελίδας

Για επίδειξη θα πάρουμε τον τίτλο και θα τον εκτυπώσουμε. Σε πραγματικό σενάριο θα μπορούσατε να πάρετε στιγμιότυπο, να εξάγετε σε PDF ή να κάνετε scraping δεδομένων.

```java
            // Simple DOM interaction – fetch and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());
        }
    }
}
```

**Αναμενόμενη έξοδος** (όταν το `https://example.com` είναι προσβάσιμο):

```
Title inside sandbox: Example Domain
```

Αν ο ιστότοπος επιστρέψει διαφορετικό τίτλο, θα δείτε αυτόν αντί αυτού — δεν χρειάζεται καμία άλλη αλλαγή.

---

## Βήμα 4: Επαλήθευση Ρυθμίσεων (Προαιρετικό Debug)

Μερικές φορές θέλετε να βεβαιωθείτε ότι το sandbox σέβεται πραγματικά το DPI και το viewport. Το Aspose.HTML δεν εκθέτει αυτές τις τιμές άμεσα, αλλά μπορείτε να τις υπολογίσετε μετρώντας διαστάσεις στοιχείων.

```java
        // Example: measure a known element's width in pixels.
        int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
        System.out.println("Measured width (px): " + elementWidth);
```

Αν γνωρίζετε ότι το CSS δηλώνει το στοιχείο ως `width: 200pt;`, σε **96 dpi** θα πρέπει να δείτε `200pt * (96/72) ≈ 267px`. Αλλάξτε το DPI και ξανατρέξτε για να δείτε την αλλαγή — απόδειξη ότι **πώς να ορίσετε dpi** λειτουργεί στην πράξη.

---

## Πλήρης Κώδικας Πηγής σε Ένα Μπλοκ

Αντιγράψτε‑και‑επικολλήστε το παρακάτω στο `SandboxExample.java`. Μεταγλωττίζεται ακριβώς· απλώς βεβαιωθείτε ότι το JAR του Aspose.HTML βρίσκεται στο classpath.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox that defines the rendering environment
        // (viewport size 1024×768 and 96 dpi) and a custom user‑agent string.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent

        // Step 2: Load a web page inside the sandbox so layout respects the settings.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {

            // Step 3: Interact with the DOM – here we simply read and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());

            // Optional: verify DPI effect by measuring an element (if you know its CSS size).
            // int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
            // System.out.println("Measured width (px): " + elementWidth);
        }
    }
}
```

Μεταγλώττιση και εκτέλεση:

```bash
javac -cp "aspose-html-23.12.jar" SandboxExample.java
java -cp ".:aspose-html-23.12.jar" SandboxExample
```

Θα πρέπει να δείτε τον τίτλο εκτυπωμένο, επιβεβαιώνοντας ότι το sandbox λειτουργεί με το **ορισμένο dpi**, **ορισμένο μέγεθος viewport** και **ορισμένο user agent** που παρείχατε.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι κάνω αν χρειάζομαι διαφορετικό DPI;

Απλώς αλλάξτε το δεύτερο όρισμα του `DocumentSandbox`. Για PDF έτοιμα για εκτύπωση μπορείτε να χρησιμοποιήσετε `300`:

```java
new DocumentSandbox(new Size(1024, 768), 300, "MyCustomUserAgent/1.0");
```

Υψηλότερο DPI δίνει μεγαλύτερες διαστάσεις pixel για τα ίδια CSS points, βελτιώνοντας την ποιότητα raster αλλά καταναλώνοντας περισσότερη μνήμη.

### Μπορώ να φορτώσω τοπικό αρχείο HTML αντί για URL;

Απόλυτα. Αντικαταστήστε το URL με διαδρομή αρχείου:

```java
HTMLDocument webDoc = new HTMLDocument("file:///C:/myfolder/page.html", renderingSandbox);
```

Βεβαιωθείτε ότι η διαδρομή είναι απόλυτη και χρησιμοποιεί το σχήμα `file:///`.

### Πώς αλλάζω το user‑agent μετά τη δημιουργία του sandbox;

Το sandbox είναι αμετάβλητο — μόλις το περάσετε στο `HTMLDocument`, οι ρυθμίσεις κλειδώνουν. Για διαφορετικό user‑agent, δημιουργήστε νέο `DocumentSandbox` με τη ζητούμενη συμβολοσειρά.

### Υποστηρίζει το Aspose.HTML εκτέλεση JavaScript;

Ναι, η μηχανή εκτελεί τις περισσότερες client‑side script. Αν ένα script τροποποιεί το DOM μετά τη φόρτωση, μπορείτε να περιμένετε λίγο:

```java
webDoc.waitForLoad();
```

Ή χρησιμοποιήστε λογική τύπου `setTimeout` μέσα στη σελίδα πριν ερωτήσετε στοιχεία.

---

## Οπτική Επιβεβαίωση (Εικόνα)

Παρακάτω φαίνεται ένα στιγμιότυπο της κονσόλας που δείχνει την επιτυχή εκτέλεση. Παρατηρήστε ότι ο τίτλος ταιριάζει με τη σελίδα, επιβεβαιώνοντας ότι το sandbox τήρησε τις ρυθμίσεις μας.

![Console output showing how to set dpi in Aspose.HTML Sandbox](/images/console-output.png)

*Alt text:* *Στιγμιότυπο κονσόλας που δείχνει πώς να ορίσετε dpi, να ορίσετε μέγεθος viewport και να ορίσετε user agent στο Aspose.HTML Sandbox.*

---

## Περίληψη & Επόμενα Βήματα

Καλύψαμε **πώς να ορίσετε DPI** (96 dpi στο παράδειγμα), **πώς να ορίσετε μέγεθος viewport** (1024 × 768) και **πώς να ορίσετε user agent** (προσαρμοσμένη συμβολοσειρά) χρησιμοποιώντας το API sandbox του Aspose.HTML. Το πλήρες, εκτελέσιμο πρόγραμμα Java αποδεικνύει ότι αυτές οι ρυθμίσεις δεν είναι μόνο θεωρητικές — επηρεάζουν άμεσα την απόδοση και την αλληλεπίδραση με το DOM.

Έτοιμοι για περισσότερα;

- **Εξαγωγή σε PDF:** Μετά τη φόρτωση της σελίδας, καλέστε `webDoc.save("output.pdf", SaveFormat.PDF);` για να δημιουργήσετε PDF υψηλής ανάλυσης που αντικατοπτρίζει το DPI που ορίσατε.  
- **Λήψη Στιγμιότυπου:** Χρησιμοποιήστε `webDoc.renderToBitmap("screenshot.png");` για εικόνες pixel‑perfect.  
- **Πειραματισμός με Responsive Layouts:** Αλλάξτε τις διαστάσεις του viewport για να δοκιμάσετε mobile breakpoints χωρίς πραγματική συσκευή.  

Πειραματιστείτε με διαφορετικές τιμές DPI, συνδυασμούς viewport και user‑agents για να δείτε πώς αντιδρούν οι διακομιστές και το CSS. Το sandbox είναι ένα ελαφρύ πεδίο παιχνιδιού που σας εξοικονομεί το χρόνο εκκίνησης πλήρων browsers.

---

### Συνεχίστε την Εξερεύνηση

- **Aspose.HTML Documentation** – εμβάθυνση στις επιλογές `DocumentSandbox`.  
- **Advanced CSS Media Queries** – μάθετε πώς το μέγεθος του viewport ενεργοποιεί διαφορετικά στυλ.  
- **User‑Agent Spoofing** – ανακαλύψτε πώς ορισμένοι ιστότοποι παρέχουν εναλλακτικό markup βάσει της συμβολοσειράς agent.

Έχετε ερωτήσεις ή δύσκολη περίπτωση; Αφήστε ένα σχόλιο και ας το λύσουμε μαζί. Καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
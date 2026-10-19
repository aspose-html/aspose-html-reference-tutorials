---
category: general
date: 2026-10-19
description: Ορίστε την αναλογία εικονοστοιχείου συσκευής σε Java χρησιμοποιώντας
  το sandbox Aspose.HTML. Μάθετε πώς να ορίσετε το πλάτος και το ύψος της οθόνης και
  να λάβετε τίτλο σελίδας java με ένα πλήρες, εκτελέσιμο παράδειγμα.
draft: false
keywords:
- get page title java
- device pixel ratio java
- create virtual device java
- set screen width height
lastmod: 2026-10-19
og_description: Λάβετε τίτλο σελίδας java με το sandbox Aspose.HTML. Αυτός ο οδηγός
  σας δείχνει πώς να ορίσετε το πλάτος και το ύψος της οθόνης και την αναλογία εικονοστοιχείου
  συσκευής σε Java σε λίγα εύκολα βήματα.
og_image_alt: 'Developer guide: set device pixel ratio in Java using Aspose.HTML sandbox'
og_title: Λάβετε τίτλο σελίδας java – ορισμός αναλογίας εικονοστοιχείου συσκευής σε
  Java sandbox
schemas:
- author: Aspose
  dateModified: '2026-10-19'
  description: set device pixel ratio in Java using Aspose.HTML sandbox. Learn how
    to set screen width height and get page title java with a complete, runnable example.
  headline: Get page title java – set device pixel ratio in Java sandbox tutorial
  type: TechArticle
- questions:
  - answer: Yes—create a new `SandboxOptions` with a different `setDevicePixelRatio`
      value and instantiate a fresh `Sandbox`. Re‑using the same sandbox after changing
      its options is not supported.
    question: Can I change the pixel ratio at runtime?
  - answer: Loop over a list of `SandboxOptions` (e.g., iPhone 8, Pixel 4) and run
      the same load‑and‑title logic for each.
    question: What if I need to test multiple devices?
  - answer: Aspose.HTML respects Java’s default SSL trust store. Add the cert to the
      JVM’s keystore or, for testing only, disable verification (not recommended for
      production).
    question: Does this work with HTTPS sites that have self‑signed certificates?
  - answer: The `HTMLDocument` API provides `save` methods that can export the rendered
      page to PNG or JPEG. Use `htmlDoc.save("output.png", SaveFormat.PNG);` after
      loading.
    question: How do I capture a screenshot instead of just the title?
  - answer: Each `Sandbox` instance is isolated, but you should avoid sharing a single
      instance across multiple threads without synchronization.
    question: Is the sandbox thread‑safe?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- mobile emulation
title: Λάβετε τίτλο σελίδας java – ορισμός αναλογίας εικονοστοιχείου συσκευής σε Java
  sandbox
url: /el/java/advanced-usage/set-device-pixel-ratio-in-java-mobile-sandbox-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Λάβετε τίτλο σελίδας java – ορίστε την αναλογία εικονοστοιχείων συσκευής σε sandbox Java

Έχετε χρειαστεί ποτέ να **ορίσετε την αναλογία εικονοστοιχείων συσκευής** ενώ δοκιμάζετε έναν ανταποκρινόμενο ιστότοπο σε Java; Δεν είστε ο μόνος. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν η σελίδα φαίνεται τέλεια στην επιφάνεια εργασίας αλλά σπάζει σε τηλέφωνα υψηλής ανάλυσης DPI. Τα καλά νέα; Με το sandbox του Aspose.HTML μπορείτε να προσομοιώσετε ένα iPhone X (ή οποιαδήποτε συσκευή) απευθείας από τον κώδικα Java — χωρίς πρόγραμμα περιήγησης.

Σε αυτόν τον οδηγό θα περάσουμε από το **πώς να ορίσετε το πλάτος και το ύψος της οθόνης**, να διαμορφώσουμε την **αναλογία εικονοστοιχείων συσκευής**, και τελικά το **get page title java** για να επαληθεύσουμε ότι όλα αποδόθηκαν σωστά. Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο και να αρχίσετε αμέσως τη δοκιμή των κινητών διατάξεων.

## Γρήγορες απαντήσεις
- **Πώς ορίζω την αναλογία εικονοστοιχείων συσκευής σε Java;** Χρησιμοποιήστε `SandboxOptions.setDevicePixelRatio(double)` πριν δημιουργήσετε το sandbox.  
- **Ποια μέθοδος επιστρέφει τον τίτλο της σελίδας;** Καλέστε `htmlDocument.getTitle()` στο φορτωμένο `HTMLDocument`.  
- **Μπορώ να προσομοιώσω άλλες συσκευές;** Ναι — δημιουργήστε ένα νέο `SandboxOptions` με το επιθυμητό πλάτος, ύψος και αναλογία εικονοστοιχείων.  
- **Χρειάζομαι οδηγό προγράμματος περιήγησης;** Όχι, το sandbox του Aspose.HTML είναι head‑less και εκτελείται αποκλειστικά σε Java.  
- **Ποια έκδοση του Aspose.HTML απαιτείται;** Η έκδοση 23.7 ή νεότερη υποστηρίζει όλες τις δυνατότητες προσομοίωσης κινητών.

## Τι είναι το get page title java;
`get page title java` είναι η λειτουργία ανάκτησης του στοιχείου `<title>` από ένα έγγραφο HTML χρησιμοποιώντας κώδικα Java. Σας επιτρέπει να επιβεβαιώσετε ότι μια σελίδα που φορτώθηκε σε ένα εικονικό περιβάλλον συσκευής απέδωσε τον αναμενόμενο τίτλο. Η ανάκτηση του τίτλου είναι ένα κοινό βήμα στην αυτοματοποιημένη επικύρωση για να διασφαλιστεί ότι η σωστή σελίδα φορτώθηκε μετά την εφαρμογή των παραμέτρων προσομοίωσης συσκευής.

## Γιατί να χρησιμοποιήσετε το sandbox του Aspose.HTML για προσομοίωση κινητών;
Το Aspose.HTML υποστηρίζει **30+** μορφές εισόδου και εξόδου — συμπεριλαμβανομένων HTML, CSS, SVG και PDF — και μπορεί να αποδώσει σελίδες χωρίς την εκκίνηση πλήρους προγράμματος περιήγησης. Το sandbox του επεξεργάζεται ιστότοπους με εκατοντάδες σελίδες διατηρώντας τη χρήση μνήμης κάτω από 200 MB, καθιστώντας το ιδανικό για CI pipelines.

## Προαπαιτούμενα
- Java 8 ή νεότερο (ο κώδικας μεταγλωττίζεται επίσης με JDK 11)  
- Βιβλιοθήκη Aspose.HTML for Java (έκδοση 23.7 ή νεότερη) – μπορείτε να την κατεβάσετε από το Maven Central  
- Ένα IDE ή μια απλή ρύθμιση `javac` γραμμής εντολών  
- Πρόσβαση στο Internet για το demo URL (`https://responsive.example.com`)

Καμία επιπλέον πλατφόρμα, χωρίς Selenium, μόνο καθαρή Java και Aspose.HTML.

## Πώς να ορίσετε το πλάτος και το ύψος της οθόνης και την αναλογία εικονοστοιχείων συσκευής σε Java
Η κλάση `SandboxOptions` σας επιτρέπει να καθορίσετε τις διαστάσεις οθόνης και την πυκνότητα εικονοστοιχείων της εικονικής συσκευής. Για να προσομοιώσετε μια συγκεκριμένη κινητή συσκευή, πρέπει να διαμορφώσετε το sandbox με το επιθυμητό πλάτος, ύψος και την αναλογία εικονοστοιχείων συσκευής. Δημιουργώντας ένα αντικείμενο `SandboxOptions` και ορίζοντας αυτές τις ιδιότητες, η μηχανή απόδοσης θα αντιμετωπίσει τη σελίδα σαν να εμφανίζεται σε αυτή τη συσκευή, εξασφαλίζοντας ότι τα CSS media queries και η κλιμάκωση εικόνων λειτουργούν σωστά.

Δημιουργήστε μια παρουσία `SandboxOptions`, ορίστε το πλάτος σε **375**, το ύψος σε **812**, και την αναλογία εικονοστοιχείων συσκευής σε **3.0**. Στη συνέχεια περάστε αυτές τις επιλογές σε ένα νέο `Sandbox`. Αυτό διαμορφώνει πλήρως τη εικονική συσκευή πριν φορτωθεί οποιαδήποτε σελίδα.

Η κλάση `SandboxOptions` ορίζει το μέγεθος οθόνης και την πυκνότητα εικονοστοιχείων της εικονικής συσκευής. Είναι το σημείο εισόδου για οποιοδήποτε σενάριο προσομοίωσης κινητών.

```java
// Step 1 – configure the virtual device
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixels width
sandboxOptions.setScreenHeight(812);         // CSS pixels height
sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI factor (set device pixel ratio)
```

> **Γιατί είναι σημαντικό:**  
> Η κλήση `setDevicePixelRatio` κλιμακώνει τα πάντα — από εικόνες μέχρι την απόδοση γραμματοσειράς — ώστε η σελίδα να πιστεύει ότι βρίσκεται σε πραγματικό τηλέφωνο. Αν την παραλείψετε, η διάταξη μπορεί να επιστρέψει σε CSS media queries τύπου desktop, υπονομεύοντας τον σκοπό των δοκιμών κινητών.

## Πώς να δημιουργήσετε την παρουσία sandbox
Η κλάση `Sandbox` αντιπροσωπεύει ένα περιβάλλον headless browser που αποδίδει HTML χρησιμοποιώντας τις προηγουμένως ορισμένες επιλογές. Αφού διαμορφώσετε το `SandboxOptions`, δημιουργήστε ένα `Sandbox` με αυτές τις επιλογές για να αποκτήσετε ένα απομονωμένο περιβάλλον απόδοσης. Αυτό το sandbox λειτουργεί σαν ελαφρύ πρόγραμμα περιήγησης, εφαρμόζοντας το μέγεθος οθόνης και την πυκνότητα εικονοστοιχείων που καθορίσατε, και μπορεί να επαναχρησιμοποιηθεί για πολλαπλές φορτώσεις σελίδων διατηρώντας το περιβάλλον καθαρό.

Δημιουργήστε ένα `Sandbox` με τις προηγουμένως διαμορφωμένες `SandboxOptions`. Το sandbox συμπεριφέρεται σαν ένας μικρός, headless browser που σέβεται τις διαστάσεις και την αναλογία εικονοστοιχείων που ορίσατε.

Το αντικείμενο `Sandbox` είναι η απομονωμένη μηχανή απόδοσης του Aspose.HTML που λειτουργεί χωρίς UI. Εγγυάται ότι κάθε δοκιμή εκτελείται σε καθαρό περιβάλλον.

```java
// Step 2 – spin up the sandbox with the options above
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

> **Συμβουλή:** Μπορείτε να επαναχρησιμοποιήσετε το ίδιο αντικείμενο `Sandbox` για πολλαπλές φορτώσεις σελίδων· απλώς αλλάξτε το URL και το sandbox θα διατηρήσει τα ίδια χαρακτηριστικά συσκευής.

## Πώς να φορτώσετε τη σελίδα μέσα στο sandbox
Η κλάση `HTMLDocument` αντιπροσωπεύει ένα αναλυμένο αρχείο HTML στη μνήμη, παρέχοντας πρόσβαση DOM και δυνατότητες απόδοσης. Με το sandbox έτοιμο, δημιουργήστε ένα `HTMLDocument περνώντας το URL προορισμού και την παρουσία sandbox. Αυτό φορτώνει και αποδίδει τη σελίδα χρησιμοποιώντας τις ρυθμίσεις εικονικής συσκευής, επιτρέποντάς σας να αλληλεπιδράσετε με το DOM ή να εξάγετε πληροφορίες όπως ο τίτλος.

Δημιουργήστε ένα `HTMLDocument` περνώντας το URL προορισμού και την παρουσία `Sandbox`. Αυτό αναγκάζει το έγγραφο να αποδοθεί χρησιμοποιώντας την εικονική συσκευή που ορίσατε νωρίτερα.

Η κλάση `HTMLDocument` αντιπροσωπεύει ένα αναλυμένο αρχείο HTML στη μνήμη και παρέχει μεθόδους για χειρισμό DOM και εξαγωγή μεταδεδομένων.

```java
// Step 3 – fetch the target page using the sandbox
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("https://responsive.example.com"), mobileSandbox);
```

Αν το URL είναι μη προσβάσιμο ή η σελίδα περιέχει σφάλματα, το Aspose.HTML θα ρίξει μια εξαίρεση. Για κώδικα παραγωγής θα το τυλίγατε σε `try‑catch` και θα καταγράφατε το σφάλμα, αλλά το tutorial το διατηρεί απλό.

## Πώς να επαληθεύσετε με το get page title java
Η μέθοδος `getTitle()` επιστρέφει το περιεχόμενο του στοιχείου `<title>` του HTML εγγράφου ως απλό κείμενο. Η ανάγνωση του τίτλου είναι ο πιο γρήγορος έλεγχος λογικής. Μετά τη φόρτωση της σελίδας, καλέστε `htmlDocument.getTitle()` για να ανακτήσετε το κείμενο του τίτλου. Αυτός ο απλός έλεγχος επιβεβαιώνει ότι η σελίδα αποδόθηκε σωστά υπό τις ρυθμίσεις προσομοιωμένης συσκευής και παρέχει έναν γρήγορο τρόπο επικύρωσης πλοήγησης ή αλλαγών περιεχομένου σε αυτοματοποιημένες δοκιμές.

Καλέστε `htmlDocument.getTitle()` στο φορτωμένο έγγραφο και εκτυπώστε το αποτέλεσμα. Εάν το sandbox εφάρμοσε σωστά την **αναλογία εικονοστοιχείων συσκευής**, ο τίτλος θα ταιριάζει με αυτόν που θα δείτε σε ένα πραγματικό iPhone X.

Η μέθοδος `getTitle()` επιστρέφει το περιεχόμενο του στοιχείου `<title>` ως απλό κείμενο, επιτρέποντάς σας να επικυρώσετε την απόδοση χωρίς οπτική επιθεώρηση.

```java
// Step 4 – retrieve and print the page title (get page title java)
System.out.println("Title under sandbox: " + htmlDoc.getTitle());
```

**Αναμενόμενη έξοδος (παράδειγμα):**

```
Title under sandbox: Responsive Demo – Mobile View
```

Αν δείτε τον τίτλο να εκτυπώνεται, έχετε επιτυχώς **ορίσει την αναλογία εικονοστοιχείων συσκευής**, **ορίσει το πλάτος και το ύψος της οθόνης**, και **λάβει τον τίτλο της σελίδας** χρησιμοποιώντας Java.

## Πλήρες, εκτελέσιμο παράδειγμα
Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα αρχείο με όνομα `SandboxDemo.java`. Βεβαιωθείτε ότι τα JAR του Aspose.HTML είναι στο classpath σας (`-cp` flag) πριν το μεταγλωττίσετε.

Η κλάση `SandboxDemo` ενώνει όλα τα προηγούμενα βήματα σε ένα ενιαίο, εκτελέσιμο παράδειγμα.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.net.URL;

/**
 * Demonstrates how to set device pixel ratio, set screen width height,
 * and get page title java using Aspose.HTML sandbox.
 */
public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // ---------- Step 1: Define device characteristics ----------
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS pixels width
        sandboxOptions.setScreenHeight(812);         // CSS pixels height
        sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI screen factor (set device pixel ratio)

        // ---------- Step 2: Create the sandbox ----------
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // ---------- Step 3: Load a web page inside the sandbox ----------
        HTMLDocument htmlDoc = new HTMLDocument(
                new URL("https://responsive.example.com"), mobileSandbox);

        // ---------- Step 4: Verify the document loaded correctly ----------
        System.out.println("Title under sandbox: " + htmlDoc.getTitle());
    }
}
```

Μεταγλώττιση και εκτέλεση:

```bash
javac -cp "aspose-html-23.7.jar" SandboxDemo.java
java -cp ".:aspose-html-23.7.jar" SandboxDemo
```

Θα πρέπει να δείτε τον τίτλο να εκτυπώνεται στην κονσόλα, επιβεβαιώνοντας ότι η σελίδα αποδόθηκε με την επιθυμητή **αναλογία εικονοστοιχείων συσκευής**.

## Συχνές ερωτήσεις & ειδικές περιπτώσεις
**Ε: Μπορώ να αλλάξω την αναλογία εικονοστοιχείων κατά την εκτέλεση;**  
Α: Ναι — δημιουργήστε ένα νέο `SandboxOptions` με διαφορετική τιμή `setDevicePixelRatio` και δημιουργήστε ένα νέο `Sandbox`. Η επαναχρήση του ίδιου sandbox μετά την αλλαγή των επιλογών του δεν υποστηρίζεται.

**Ε: Τι αν χρειαστεί να δοκιμάσω πολλές συσκευές;**  
Α: Επαναλάβετε πάνω σε μια λίστα `SandboxOptions` (π.χ., iPhone 8, Pixel 4) και εκτελέστε την ίδια λογική φόρτωσης‑και‑τίτλου για κάθε μία.

**Ε: Λειτουργεί αυτό με HTTPS ιστότοπους που έχουν αυτο‑υπογεγραμμένα πιστοποιητικά;**  
Α: Το Aspose.HTML σέβεται το προεπιλεγμένο SSL trust store της Java. Προσθέστε το πιστοποιητικό στο keystore του JVM ή, μόνο για δοκιμές, απενεργοποιήστε την επαλήθευση (δεν συνιστάται για παραγωγή).

**Ε: Πώς μπορώ να καταγράψω ένα στιγμιότυπο οθόνης αντί του τίτλου;**  
Α: Το API του `HTMLDocument` παρέχει μεθόδους `save` που μπορούν να εξάγουν τη σελίδα σε PNG ή JPEG. Χρησιμοποιήστε `htmlDoc.save("output.png", SaveFormat.PNG);` μετά τη φόρτωση.

**Ε: Είναι το sandbox thread‑safe;**  
Α: Κάθε παρουσία `Sandbox` είναι απομονωμένη, αλλά θα πρέπει να αποφεύγετε την κοινή χρήση μιας ενιαίας παρουσίασης μεταξύ πολλαπλών νημάτων χωρίς συγχρονισμό.

## Οπτική επισκόπηση
![Διάγραμμα που δείχνει την ορισμένη αναλογία εικονοστοιχείων σε mobile sandbox](https://example.com/images/sandbox-diagram.png "διάγραμμα αναλογίας εικονοστοιχείων")
[Διάγραμμα που δείχνει την ορισμένη αναλογία εικονοστοιχείων σε mobile sandbox](https://example.com/images/sandbox-diagram.png "διάγραμμα αναλογίας εικονοστοιχείων")

*Η παραπάνω εικονογράφηση απεικονίζει τη ροή από τη διαμόρφωση του `SandboxOptions` (συμπεριλαμβανομένων **ορισμού πλάτους και ύψους οθόνης** και **ορισμού αναλογίας εικονοστοιχείων συσκευής**) στη φόρτωση ενός URL και την εξαγωγή του τίτλου.*

## Συμπέρασμα
Τώρα γνωρίζετε **πώς να ορίσετε την αναλογία εικονοστοιχείων συσκευής** σε Java, πώς να **ορίσετε το πλάτος και το ύψος της οθόνης** για ακριβή προσομοίωση κινητών, και πώς να **get page title java** για να επιβεβαιώσετε ότι η απόδοση ολοκληρώθηκε με επιτυχία. Αυτή η σύντομη ροή εργασίας εξαλείφει την ανάγκη για βαριά προγράμματα περιήγησης κατά τη διάρκεια αυτοματοποιημένων δοκιμών UI και ενσωματώνεται άψογα σε CI pipelines.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να εξάγετε τη σελίδα ως εικόνα, ή πειραματιστείτε με την αποσφαλμάτωση CSS media‑query εναλλάσσοντας το `devicePixelRatio` μεταξύ 1.0 και 3.0. Μπορείτε επίσης να εξερευνήσετε τις δυνατότητες μετατροπής PDF του Aspose.HTML για να δημιουργήσετε μια εκτυπώσιμη έκδοση της κινητής προβολής.

Καλή προγραμματιστική, και εύχομαι οι κινητές διατάξεις σας να είναι πάντα καθαρές — ανεξάρτητα από την πυκνότητα εικονοστοιχείων!

**Τελευταία ενημέρωση:** 2026-10-19  
**Δοκιμάστηκε με:** Aspose.HTML 23.7 for Java  
**Συγγραφέας:** Aspose

## Σχετικά Μαθήματα
- [Λάβετε HTML Τίτλο Java Απόδοση Σελίδας Σε Sandbox Με Πλάτος Οθόνης](/html/java/advanced-usage/get-html-title-java-render-page-in-sandbox-with-screen-width/)
- [Δημιουργία Aspose Html Sandbox Πλήρης Οδηγός Java](/html/java/configuring-environment/create-aspose-html-sandbox-complete-java-guide/)
- [Ορισμός Αναλογίας Εικονοστοιχείων Συσκευής Σε Java Πλήρης Οδηγός](/html/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
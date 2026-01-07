---
category: general
date: 2026-01-03
description: Εκπαίδευση υψηλής ανάλυσης DPI για προγραμματιστές Java. Μάθετε πώς να
  ορίσετε έναν προσαρμοσμένο πράκτορα χρήστη, να χρησιμοποιήσετε το λόγο εικονοστοιχείων
  της συσκευής και να μετατρέψετε HTML σε εικόνα με Java για λήψη στιγμιότυπου οθόνης
  ιστοσελίδας Java.
draft: false
keywords:
- high dpi rendering
- custom user agent
- html to image java
- device pixel ratio
- webpage screenshot java
language: el
og_description: Οδηγός απόδοσης υψηλής ανάλυσης DPI που δείχνει πώς να ορίσετε έναν
  προσαρμοσμένο πράκτορα χρήστη και λόγο εικονοστοιχείων συσκευής για τη δημιουργία
  στιγμιότυπων Java HTML σε εικόνα.
og_title: Απόδοση υψηλής ανάλυσης DPI σε Java – Λήψη στιγμιότυπων οθόνης ιστοσελίδων
tags:
- Java
- Aspose.HTML
- Rendering
- Web Automation
title: Απόδοση υψηλής ανάλυσης DPI σε Java – Καταγραφή στιγμιότυπων οθόνης ιστοσελίδων
  με προσαρμοσμένο πράκτορα χρήστη
url: /el/java/conversion-html-to-various-image-formats/high-dpi-rendering-in-java-capture-webpage-screenshots-with/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Απόδοση Υψηλής Ανάλυσης DPI – Λήψη Στιγμιότυπων Ιστοσελίδων σε Java

Κάποτε χρειάστηκε **απόδοση υψηλής ανάλυσης DPI** για ένα στιγμιότυπο ιστοσελίδας αλλά δεν ήξερα πώς να προσομοιώσω μια οθόνη retina σε Java; Δεν είστε μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν πρόβλημα όταν το αποτέλεσμα φαίνεται θολό σε οθόνες υψηλής ανάλυσης, ειδικά όταν μετατρέπουν HTML σε εικόνα με Java.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει πώς να ρυθμίσετε ένα sandbox, να ορίσετε έναν **προσαρμοσμένο user agent**, να ρυθμίσετε το **device pixel ratio**, και τέλος να παραγάγετε ένα καθαρό **webpage screenshot Java**. Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Java και να αρχίσετε αμέσως να δημιουργείτε εικόνες υψηλής ποιότητας.

## Τι Θα Μάθετε

- Γιατί η **απόδοση υψηλής ανάλυσης DPI** είναι σημαντική για τις σύγχρονες οθόνες.  
- Πώς να ορίσετε έναν **προσαρμοσμένο user agent** ώστε η σελίδα να νομίζει ότι επισκέπτεται ένας πραγματικός περιηγητής.  
- Χρήση του `Sandbox` και των `SandboxOptions` του Aspose.HTML για έλεγχο του **device pixel ratio**.  
- Μετατροπή HTML σε εικόνα σε Java (το κλασικό σενάριο **html to image java**).  
- Συνηθισμένα προβλήματα και επαγγελματικές συμβουλές για αξιόπιστη δημιουργία **webpage screenshot java**.

> **Προαπαιτούμενα:** Java 8+, Maven ή Gradle, και άδεια Aspose.HTML for Java (η δωρεάν δοκιμή λειτουργεί για αυτήν την επίδειξη). Δεν απαιτούνται άλλες εξωτερικές βιβλιοθήκες.

---

## Βήμα 1: Διαμόρφωση Sandbox Options για Απόδοση Υψηλής DPI

Η καρδιά της **απόδοσης υψηλής DPI** είναι η ενημέρωση της μηχανής απόδοσης ότι η εικονική οθόνη έχει μεγαλύτερη πυκνότητα εικονοστοιχείων. Το Aspose.HTML το εκθέτει μέσω του `SandboxOptions`. Θα ορίσουμε ένα device‑pixel‑ratio 2.0, που αντιστοιχεί σε τυπικές οθόνες Retina.

```java
import com.aspose.html.rendering.Sandbox;
import com.aspose.html.rendering.SandboxOptions;

/* Step 1 – Define sandbox options: screen size, DPI, and user‑agent */
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(1280);          // logical CSS pixels
sandboxOptions.setScreenHeight(800);          // logical CSS pixels
sandboxOptions.setDevicePixelRatio(2.0);      // high‑DPI factor
sandboxOptions.setUserAgent("AsposeHTML/1.0"); // custom user agent string
```

**Γιατί είναι σημαντικό:**  
- `setScreenWidth/Height` ορίζουν το CSS viewport που θα δει η σελίδα.  
- `setDevicePixelRatio` πολλαπλασιάζει κάθε CSS pixel σε φυσικά pixels, δίνοντάς σας την οξεία εμφάνιση retina.  
- `setUserAgent` σας επιτρέπει να μεταμφιεστείτε σε σύγχρονο περιηγητή, εξασφαλίζοντας ότι οποιαδήποτε λογική διάταξης βασισμένη σε JavaScript (όπως responsive CSS media queries) λειτουργεί σωστά.

> **Συμβουλή επαγγελματία:** Αν στοχεύετε σε οθόνη 4K, αυξήστε το ratio σε `3.0` ή `4.0` και παρακολουθήστε το μέγεθος του αρχείου να μεγαλώνει ανάλογα.

---

## Βήμα 2: Δημιουργία του Sandbox Instance

Τώρα δημιουργούμε το sandbox με τις επιλογές που μόλις διαμορφώσαμε. Το sandbox απομονώνει τη διαδικασία απόδοσης, αποτρέποντας ανεπιθύμητες κλήσεις δικτύου ή εκτέλεση σεναρίων που θα μπορούσαν να επηρεάσουν το JVM σας.

```java
/* Step 2 – Build the sandbox using the prepared options */
Sandbox renderingSandbox = new Sandbox(sandboxOptions);
```

**Τι κάνει το sandbox:**  
- Παρέχει ένα ελεγχόμενο περιβάλλον (σαν headless browser) που σέβεται το viewport που ορίσαμε.  
- Εγγυάται επαναλήψιμα στιγμιότυπα ανεξάρτητα από το μηχάνημα στο οποίο τρέχετε τον κώδικα.  

---

## Βήμα 3: Φόρτωση της Στόχευσης Ιστοσελίδας (HTML to Image Java)

Με το sandbox έτοιμο, μπορούμε να φορτώσουμε οποιοδήποτε URL. Ο κατασκευαστής `HTMLDocument` δέχεται το sandbox, εξασφαλίζοντας ότι η σελίδα λαμβάνει τον **προσαρμοσμένο user agent** και το **device pixel ratio** μας.

```java
import com.aspose.html.HTMLDocument;

/* Step 3 – Load the web page inside the sandbox */
HTMLDocument htmlDoc = new HTMLDocument("https://example.com", renderingSandbox);
```

**Ακραία περίπτωση:**  
Αν ο ιστότοπος χρησιμοποιεί αυστηρές κεφαλίδες CSP ή αποκλείει άγνωστους agents, ίσως χρειαστεί να προσαρμόσετε τη συμβολοσειρά `User-Agent` ώστε να μιμείται το Chrome ή το Firefox. Για παράδειγμα:

```java
sandboxOptions.setUserAgent(
    "Mozilla/5.0 (Windows NT 10.0; Win64; x64) " +
    "AppleWebKit/537.36 (KHTML, like Gecko) " +
    "Chrome/120.0.0.0 Safari/537.36");
```

Αυτή η μικρή αλλαγή μπορεί να μετατρέψει μια αποτυχημένη φόρτωση σε μια τέλεια αποδομένη σελίδα.

---

## Βήμα 4: Απόδοση του Εγγράφου σε Εικόνα (Webpage Screenshot Java)

Το Aspose.HTML σας επιτρέπει να αποδίδετε απευθείας σε ένα `Bitmap` ή να αποθηκεύετε ως PNG/JPEG. Παρακάτω καταγράφουμε ολόκληρο το viewport και το γράφουμε σε αρχείο PNG.

```java
import com.aspose.html.rendering.ImageRenderOptions;
import com.aspose.html.rendering.ImageRenderer;
import java.io.File;

/* Step 4 – Prepare rendering options */
ImageRenderOptions renderOptions = new ImageRenderOptions();
renderOptions.setOutputFilePath("screenshot.png");
renderOptions.setImageFormat(ImageRenderOptions.ImageFormat.PNG);

/* Render the document */
ImageRenderer renderer = new ImageRenderer(htmlDoc, renderOptions);
renderer.render();
renderer.dispose(); // clean up native resources
```

**Αποτέλεσμα:**  
Το `screenshot.png` θα είναι ένα στιγμιότυπο υψηλής ανάλυσης του `https://example.com`, αποδομένο σε 2× DPI. Ανοίξτε το σε οποιαδήποτε οθόνη και θα δείτε καθαρό κείμενο και οξείς γραφικές παραστάσεις — ακριβώς αυτό που υπόσχεται η **απόδοση υψηλής DPI**.

---

## Βήμα 5: Επαλήθευση και Ρύθμιση (Προαιρετικό)

Μετά την πρώτη εκτέλεση, ίσως θελήσετε να:

- **Ρυθμίσετε τις διαστάσεις:** Αλλάξτε `setScreenWidth`/`setScreenHeight` για λήψη ολόκληρης σελίδας.  
- **Αλλάξετε μορφή:** Μεταβείτε σε JPEG για μικρότερα αρχεία (`ImageFormat.JPEG`) ή BMP για lossless.  
- **Προσθέσετε καθυστέρηση:** Κάποιες σελίδες φορτώνουν περιεχόμενο ασύγχρονα. Εισάγετε `Thread.sleep(2000);` πριν την απόδοση για να δώσετε χρόνο στα σενάρια να ολοκληρωθούν.

```java
// Example: Wait for dynamic content before rendering
Thread.sleep(2000);
renderer.render();
```

---

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται το ολοκληρωμένο, έτοιμο‑για‑εκτέλεση πρόγραμμα Java που συνδυάζει όλα τα παραπάνω. Αντιγράψτε‑και‑επικολλήστε το σε ένα αρχείο `RenderWithSandbox.java`, προσθέστε την εξάρτηση Aspose.HTML στο `pom.xml` ή `build.gradle`, και εκτελέστε.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.Sandbox;
import com.aspose.html.rendering.SandboxOptions;
import com.aspose.html.rendering.ImageRenderOptions;
import com.aspose.html.rendering.ImageRenderer;

/**
 * Demonstrates high DPI rendering, custom user agent, and HTML‑to‑image conversion.
 */
public class RenderWithSandbox {
    public static void main(String[] args) throws Exception {

        // Step 1: Define sandbox options – screen size, DPI and user‑agent string
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(1280);
        sandboxOptions.setScreenHeight(800);
        sandboxOptions.setDevicePixelRatio(2.0);   // high‑DPI rendering
        sandboxOptions.setUserAgent("AsposeHTML/1.0"); // custom user agent

        // Step 2: Create a sandbox using the configured options
        Sandbox renderingSandbox = new Sandbox(sandboxOptions);

        // Step 3: Load the web page inside the sandbox so that viewport‑dependent code
        //         (CSS media queries, JavaScript) sees the dimensions we set
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com", renderingSandbox);

        // Optional: pause for async scripts (e.g., 2 seconds)
        // Thread.sleep(2000);

        // Step 4: Set up rendering options for PNG output
        ImageRenderOptions renderOptions = new ImageRenderOptions();
        renderOptions.setOutputFilePath("screenshot.png");
        renderOptions.setImageFormat(ImageRenderOptions.ImageFormat.PNG);

        // Step 5: Render the document to an image file
        ImageRenderer renderer = new ImageRenderer(htmlDoc, renderOptions);
        renderer.render();

        // Clean up resources
        renderer.dispose();
        renderingSandbox.dispose();

        System.out.println("Screenshot saved as screenshot.png");
    }
}
```

Τρέξτε το πρόγραμμα και θα δείτε το `screenshot.png` στον φάκελο του έργου σας — καθαρό, υψηλής ανάλυσης, και έτοιμο για περαιτέρω επεξεργασία (π.χ., ενσωμάτωση σε PDF ή αποστολή μέσω email).

---

## Συχνές Ερωτήσεις (FAQ)

**Ε: Λειτουργεί αυτό με σελίδες που απαιτούν πιστοποίηση;**  
Α: Ναι. Μπορείτε να εισάγετε cookies ή HTTP headers μέσω του `NetworkSettings` του sandbox. Απλώς ορίστε `sandboxOptions.setCookies(...)` πριν φορτώσετε το έγγραφο.

**Ε: Τι κάνω αν χρειάζομαι λήψη ολόκληρης σελίδας, όχι μόνο του viewport;**  
Α: Αυξήστε το `setScreenHeight` στο scroll height της σελίδας (μπορείτε να το ερωτήσετε με JavaScript: `document.body.scrollHeight`). Στη συνέχεια αποδώστε όπως φαίνεται παραπάνω.

**Ε: Είναι απαραίτητος ο `custom user agent`;**  
Α: Πολλοί σύγχρονοι ιστότοποι σερβίρουν διαφορετικές διατάξεις βάσει του user‑agent. Η παροχή ενός που μιμείται πραγματικό περιηγητή αποτρέπει “mobile‑only” ή “no‑JS” εναλλακτικές, δίνοντάς σας την προοριζόμενη επιφάνεια εργασίας desktop.

**Ε: Πώς επηρεάζει το **device pixel ratio** το μέγεθος του αρχείου;**  
Α: Υψηλότερα ratios πολλαπλασιάζουν τον αριθμό των εικονοστοιχείων, έτσι μια εικόνα 2× DPI μπορεί να είναι περίπου τέσσερις φορές μεγαλύτερη από μια 1×. Ισορροπήστε την ποιότητα με το χώρο αποθήκευσης ανάλογα με τις ανάγκες σας.

---

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για να εκτελέσετε **απόδοση υψηλής DPI** σε Java, από τη ρύθμιση ενός **προσαρμοσμένου user agent** μέχρι την προσαρμογή του **device pixel ratio** και την τελική δημιουργία ενός καθαρού **webpage screenshot java**. Το πλήρες παράδειγμα δείχνει τη ροή εργασίας **html to image java** με το sandbox renderer του Aspose.HTML, ενώ οι επιπλέον συμβουλές σας βοηθούν να διαχειριστείτε δυναμικές σελίδες και σενάρια πιστοποίησης.

Πειραματιστείτε — αλλάξτε το URL, ρυθμίστε το DPI, ή αλλάξτε τις μορφές εξόδου. Το ίδιο μοτίβο λειτουργεί για δημιουργία μικρογραφιών, παραγωγή PDF, ή ακόμη και τροφοδοσία εικόνων σε pipelines μηχανικής μάθησης.  

Έχετε περισσότερες ερωτήσεις; Αφήστε ένα σχόλιο, και καλή προγραμματιστική!

![παράδειγμα απόδοσης υψηλής DPI](https://example.com/high-dpi-rendering.png "παράδειγμα απόδοσης υψηλής DPI")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
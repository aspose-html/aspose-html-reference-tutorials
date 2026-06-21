---
category: general
date: 2026-02-22
description: Ορίστε το λόγο εικονοστοιχείων της συσκευής (device pixel ratio) σε Java
  με το sandbox του Aspose.HTML. Μάθετε πώς να ορίσετε προσαρμοσμένο user agent, να
  λάβετε τον τίτλο της σελίδας σε Java και να μετατρέψετε HTML σε PNG σε έναν ενιαίο
  οδηγό.
draft: false
keywords:
- set device pixel ratio
- set custom user agent
- save html as image
- convert html to png
- get page title java
language: el
og_description: Ορίστε το λόγο εικονοστοιχείων της συσκευής σε Java χρησιμοποιώντας
  το sandbox του Aspose.HTML. Αυτό το σεμινάριο δείχνει πώς να ορίσετε προσαρμοσμένο
  πράκτορα χρήστη, να ανακτήσετε τον τίτλο της σελίδας σε Java και να μετατρέψετε
  HTML σε PNG.
og_title: Ορισμός Αναλογίας Pixel Συσκευής σε Java – Πλήρης Οδηγός
tags:
- Aspose.HTML
- Java
- Web Rendering
title: Ορισμός του λόγου εικονοστοιχείων συσκευής στη Java – Πλήρης οδηγός
url: /el/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ορισμός Αναλογίας Pixel Συσκευής σε Java – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ πώς να **ορίσετε την αναλογία pixel της συσκευής** κατά την απόδοση μιας ιστοσελίδας από τη Java; Δεν είστε οι μόνοι. Πολλοί προγραμματιστές χρειάζονται να προσομοιώσουν οθόνες κινητών υψηλής ανάλυσης (high‑DPI) ώστε τα στιγμιότυπα να είναι καθαρά, ειδικά όταν αργότερα **αποθηκεύουν html ως εικόνα** για αναφορές ή διαφημιστικό υλικό. Σε αυτό το tutorial θα περάσουμε από ένα πρακτικό παράδειγμα που κάνει ακριβώς αυτό—ενώ θα σας δείξουμε επίσης πώς να **ορίσετε προσαρμοσμένο user agent**, **get page title java**, και **convert html to png** χρησιμοποιώντας το Aspose.HTML.

Θα ξεκινήσουμε με μια σύντομη επισκόπηση του sandbox API, μετά θα εμβαθύνουμε σε κάθε βήμα ρύθμισης και τέλος θα δημιουργήσουμε ένα αρχείο PNG που αντικατοπτρίζει μια πραγματική οθόνη iPhone. Στο τέλος, θα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε Java project. Δεν απαιτούνται εξωτερικά εργαλεία, μόνο καθαρή Java και Aspose.HTML 7.x (ή νεότερη).

---

## Προαπαιτούμενα

- Java 17 ή νεότερη (ο κώδικας συντάσσεται και με παλαιότερες εκδόσεις, αλλά συνιστάται η 17).
- Βιβλιοθήκη Aspose.HTML for Java (κατεβάστε την από την επίσημη ιστοσελίδα της Aspose· Maven coordinates: `com.aspose:aspose-html:23.10`).
- IDE ή κειμενογράφος της επιλογής σας (IntelliJ IDEA, VS Code, Eclipse… όλα λειτουργούν).
- Πρόσβαση στο διαδίκτυο για το demo URL (`https://example.com/responsive.html`), ή αντικαταστήστε το με οποιαδήποτε δημόσια HTML σελίδα που κατέχετε.

> **Pro tip:** Αν βρίσκεστε πίσω από proxy, ρυθμίστε τις ιδιότητες συστήματος `http.proxyHost` και `http.proxyPort` του JVM πριν τρέξετε τον κώδικα.

---

## Βήμα 1: Ορισμός Αναλογίας Pixel Συσκευής και Άλλων Sandbox Options

Το πρώτο που χρειαζόμαστε είναι ένα αντικείμενο **SandboxOptions** όπου ορίζουμε το εικονικό μέγεθος οθόνης και την *αναλογία pixel συσκευής* (DPR). Σκεφτείτε το DPR ως τον παράγοντα που λέει στο πρόγραμμα περιήγησης πόσα φυσικά pixel αντιστοιχούν σε ένα CSS pixel. Σε ένα Retina iPhone το DPR είναι συνήθως **2.0**, γι' αυτό θα χρησιμοποιήσουμε αυτήν την τιμή.

```java
// Step 1: Create and configure SandboxOptions
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS width of an iPhone X
sandboxOptions.setScreenHeight(667);         // CSS height
sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
```

> **Γιατί είναι σημαντικό:** Χωρίς τον σωστό ορισμό του DPR, η παραγόμενη εικόνα θα φαίνεται θολή ή υπερμεγέθους επειδή ο rasterizer υποθέτει απεικόνιση 1:1 pixel.

---

## Βήμα 2: Ορισμός Προσαρμοσμένου User Agent

Οι ιστοσελίδες συχνά σερβίρουν διαφορετικό markup βάσει της κεφαλίδας **User‑Agent**. Για να διασφαλίσουμε ότι η σελίδα μας συμπεριφέρεται όπως σε πραγματικό iPhone, εισάγουμε μια προσαρμοσμένη συμβολοσειρά που μιμείται το Safari στο iOS.

```java
// Step 2: Define a mobile‑specific user agent
String iphoneUA = "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                  "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                  "Version/14.0 Mobile/15E148 Safari/604.1";

sandboxOptions.setUserAgent(iphoneUA);   // <-- set custom user agent
```

> **Edge case:** Κάποιες ιστοσελίδες ελέγχουν επίσης την κεφαλίδα `Accept-Language`. Αν παρατηρήσετε ελλιπείς μεταφράσεις, προσθέστε `sandboxOptions.setAcceptLanguage("en-US,en;q=0.9");`.

---

## Βήμα 3: Φόρτωση Σελίδας Μέσα στο Sandbox και Λήψη Τίτλου

Τώρα δημιουργούμε το sandbox με τις επιλογές που ορίσαμε. Το αντικείμενο **Sandbox** απομονώνει τη διαδικασία απόδοσης, εξασφαλίζοντας ότι οι ρυθμίσεις DPR και user‑agent τηρούνται.

```java
// Step 3: Create the sandbox and load the HTML document
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
HTMLDocument htmlDoc = new HTMLDocument(
        "https://example.com/responsive.html", mobileSandbox);
```

Μόλις φορτωθεί η σελίδα, η λήψη του τίτλου είναι τόσο απλή όσο η κλήση του `getTitle()`. Αυτό ικανοποιεί την απαίτηση **get page title java**.

```java
// Step 3b: Print the page title to the console
System.out.println("Title: " + htmlDoc.getTitle());   // <-- get page title java
```

**Αναμενόμενη έξοδος στην κονσόλα**

```
Title: Responsive Demo – Mobile View
```

Αν ο τίτλος είναι κενός, ελέγξτε ξανά το URL ή βεβαιωθείτε ότι η σελίδα δεν μπλοκάρεται από πολιτικές CORS.

---

## Βήμα 4: Μετατροπή HTML σε PNG και Αποθήκευση HTML ως Εικόνα

Το Aspose.HTML σας επιτρέπει να αποδώσετε το DOM απευθείας σε αρχείο εικόνας. Επειδή έχουμε ήδη ορίσει το DPR σε 2.0, το παραγόμενο PNG θα έχει διπλή πυκνότητα pixel, προσφέροντας ένα καθαρό στιγμιότυπο.

```java
// Step 4: Render and save as PNG (convert html to png)
htmlDoc.save("mobile_view.png");   // <-- save html as image
```

Η μέθοδος `save` ανιχνεύει αυτόματα την επέκταση του αρχείου και επιλέγει τον κατάλληλο renderer. Αν χρειάζεστε διαφορετική μορφή (JPEG, BMP), απλώς αλλάξτε το όνομα του αρχείου αναλόγως.

> **Τι κάνετε αν χρειάζεστε συγκεκριμένο μέγεθος εικόνας;**  
> Χρησιμοποιήστε `ImageSaveOptions` για να ελέγξετε πλάτος, ύψος και χρώμα φόντου:

```java
ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
pngOptions.setWidth(750);   // 375 CSS px * DPR 2
pngOptions.setHeight(1334);
htmlDoc.save("mobile_view_custom.png", pngOptions);
```

---

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι το ολοκληρωμένο, έτοιμο‑για‑εκτέλεση πρόγραμμα που ενώνει όλα τα βήματα. Αντιγράψτε‑και‑επικολλήστε το σε ένα αρχείο `SandboxDemo.java`, προσθέστε την εξάρτηση Aspose.HTML και τρέξτε `java SandboxDemo`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.rendering.image.ImageSaveOptions;
import com.aspose.html.rendering.image.SaveFormat;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Configure sandbox – set device pixel ratio, screen size, and user agent
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS width (iPhone)
        sandboxOptions.setScreenHeight(667);         // CSS height
        sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
        sandboxOptions.setUserAgent(
                "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                "Version/14.0 Mobile/15E148 Safari/604.1");   // <-- set custom user agent

        // 2️⃣ Create sandbox instance
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // 3️⃣ Load the target page inside the sandboxed environment
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com/responsive.html", mobileSandbox);

        // 4️⃣ Retrieve and print the page title (get page title java)
        System.out.println("Title: " + htmlDoc.getTitle());

        // 5️⃣ Render the page – convert html to png and save html as image
        // Simple save (auto‑detect PNG)
        htmlDoc.save("mobile_view.png");   // <-- save html as image

        // 6️⃣ Optional: custom size rendering
        ImageSaveOptions opts = new ImageSaveOptions(SaveFormat.PNG);
        opts.setWidth(750);   // 375 * DPR 2
        opts.setHeight(1334);
        htmlDoc.save("mobile_view_custom.png", opts); // another convert html to png example
    }
}
```

Η εκτέλεση του προγράμματος παράγει δύο αρχεία PNG:

| Αρχείο | Περιγραφή |
|--------|------------|
| `mobile_view.png` | Προεπιλεγμένη απόδοση με το ρυθμισμένο DPR. |
| `mobile_view_custom.png` | Απόδοση με ρητό πλάτος/ύψος (χρήσιμο για σταθερά assets). |

Μπορείτε να ανοίξετε οποιοδήποτε από τα αρχεία σε προβολέα εικόνων για να επαληθεύσετε την υψηλή ανάλυση.

---

## Συχνές Ερωτήσεις & Edge Cases

| Ερώτηση | Απάντηση |
|----------|----------|
| **Τι γίνεται αν η σελίδα περιέχει JavaScript που τροποποιεί το DOM μετά τη φόρτωση;** | Το Aspose.HTML εκτελεί σενάρια από προεπιλογή. Αν χρειάζεστε στατικό στιγμιότυπο πριν την εκτέλεση, ορίστε `sandboxOptions.setEnableJavaScript(false)`. |
| **Μπορώ να αποδώσω σελίδα που απαιτεί έλεγχο ταυτότητας;** | Ναι. Χρησιμοποιήστε `sandboxOptions.setCredentials(new NetworkCredential("user","pass"))` ή εισάγετε cookies μέσω `sandboxOptions.getCookies().add(...)`. |
| **Η DPR περιορίζεται στο 2.0;** | Όχι. Μπορείτε να ορίσετε οποιοδήποτε θετικό double (π.χ., 3.0 για ultra‑high‑DPI συσκευές). Θυμηθείτε ότι μεγαλύτερο DPR σημαίνει μεγαλύτερα αρχεία εικόνας. |
| **Πώς διαχειρίζομαι σελίδες με μεγάλα assets (εικόνες, γραμματοσειρές);** | Αυξήστε το όριο μνήμης του sandbox με `sandboxOptions.setMemoryLimit(512 * 1024 * 1024)` (bytes). Αυτό αποτρέπει σφάλματα out‑of‑memory σε βαρύ περιεχόμενο. |
| **Πρέπει να κλείσω το sandbox χειροκίνητα;** | Το `Sandbox` υλοποιεί το `AutoCloseable`. Τυλίξτε το σε block `try‑with‑resources` για αυτόματη εκκαθάριση. |

---

## Συμπέρασμα

Δείξαμε πώς να **ορίσετε την αναλογία pixel συσκευής** σε Java sandbox, **ορίσετε προσαρμοσμένο user agent**, **get page title java**, και **convert html to png** (δηλαδή **save html as image**) χρησιμοποιώντας το Aspose.HTML. Το πλήρες παράδειγμα παρουσιάζει μια πρακτική ροή εργασίας που μπορείτε να προσαρμόσετε για αυτόματη δημιουργία στιγμιότυπων, visual regression testing, ή οποιοδήποτε σενάριο που απαιτεί ακριβή αναπαράσταση μιας ιστοσελίδας.

Πειραματιστείτε—αλλάξτε το DPR σε 3.0, αντικαταστήστε το user‑agent με μια συμβολοσειρά Android, ή κατευθύνετε το URL σε τοπικό αρχείο HTML. Το ίδιο μοτίβο λειτουργεί για PDFs, SVGs ή ακόμη και πολυ‑σελίδες απόδοσης.

Αν βρήκατε χρήσιμο αυτόν τον οδηγό, εξερευνήστε σχετικά θέματα όπως **δημιουργία PDF με Aspose.HTML**, **εναλλακτικές λύσεις headless Chrome**, ή **μαζική απόδοση πολλαπλών URLs**. Καλό coding, και οι στιγμιότυπές σας να είναι πάντα razor‑sharp!

![ορισμός αναλογίας pixel συσκευής σε Java sandbox](image.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
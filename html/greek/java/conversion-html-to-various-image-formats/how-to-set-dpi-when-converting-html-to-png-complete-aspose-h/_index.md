---
category: general
date: 2026-06-29
description: Μάθετε πώς να ορίζετε το DPI και την ανάλυση εικόνας κατά τη μετατροπή
  HTML σε PNG με το Aspose HTML Converter. Περιλαμβάνεται παράδειγμα Java βήμα‑προς‑βήμα.
draft: false
keywords:
- how to set dpi
- convert html to png
- set image resolution
- convert html page
- aspose html converter
language: el
og_description: Πώς να ορίσετε το DPI στη μετατροπή HTML με το Aspose. Αυτός ο οδηγός
  σας δείχνει πώς να μετατρέψετε μια σελίδα HTML σε εικόνα PNG υψηλής ανάλυσης σε
  Java.
og_title: Πώς να ορίσετε DPI κατά τη μετατροπή HTML σε PNG – Εκπαίδευση Aspose HTML
schemas:
- author: Aspose
  dateModified: '2026-06-29'
  description: Learn how to set DPI and image resolution while converting HTML to
    PNG with Aspose HTML Converter. Step‑by‑step Java example included.
  headline: How to Set DPI When Converting HTML to PNG – Complete Aspose HTML Guide
  type: TechArticle
- description: Learn how to set DPI and image resolution while converting HTML to
    PNG with Aspose HTML Converter. Step‑by‑step Java example included.
  name: How to Set DPI When Converting HTML to PNG – Complete Aspose HTML Guide
  steps:
  - name: 1. Different Output Formats
    text: Aspose.HTML isn’t limited to PNG. Swap the file extension and use a matching
      options class, e.g., `JpegConversionOptions` for JPEGs. The DPI logic stays
      identical.
  - name: 2. Dynamically Determining Screen Size
    text: 'If you need the sandbox to mimic a mobile device, read the dimensions from
      a config file:'
  - name: 3. Batch Conversion
    text: Wrap the conversion call inside a loop that iterates over a directory of
      HTML files. Remember to reuse the same `Sandbox` and `ImageConversionOptions`
      objects to avoid unnecessary allocations.
  type: HowTo
tags:
- Java
- Aspose.HTML
- Image Processing
title: Πώς να ορίσετε DPI κατά τη μετατροπή HTML σε PNG – Πλήρης οδηγός Aspose HTML
url: /el/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-html-to-png-complete-aspose-h/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ορίσετε DPI κατά τη μετατροπή HTML σε PNG – Πλήρης Οδηγός Aspose HTML

Έχετε αναρωτηθεί ποτέ **πώς να ορίσετε DPI** για ένα PNG που δημιουργείτε από μια σελίδα HTML; Σε πολλές περιπτώσεις αναφοράς ή αυτοματοποίησης στιγμιότυπων, το προεπιλεγμένο 96 dpi δεν είναι απλώς αρκετά καθαρό. Τα καλά νέα είναι ότι το Aspose.HTML for Java σας δίνει πλήρη έλεγχο πάνω στην προσομοίωση οθόνης και την ανάλυση εικόνας, ώστε να μπορείτε να αυξήσετε το DPI σε 300 ή ακόμη και 600 με λίγες μόνο γραμμές κώδικα.

Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό παράδειγμα Java που **μετατρέπει μια σελίδα HTML σε PNG** ενώ ρυθμίζει ρητά **το DPI** και **την ανάλυση εικόνας**. Στο τέλος θα έχετε μια έτοιμη προς εκτέλεση κλάση, θα καταλάβετε γιατί κάθε ρύθμιση είναι σημαντική και θα ξέρετε πώς να την προσαρμόσετε για διαφορετικές περιπτώσεις χρήσης όπως εκτυπώσεις υψηλής ανάλυσης ή μικρογραφίες για το web.

> **Γρήγορη προεπισκόπηση:** Τα βασικά βήματα είναι (1) δημιουργία ενός `Sandbox` που προσομοιώνει οθόνη, (2) ορισμός του DPI, (3) διαμόρφωση του `ImageConversionOptions` με την επιθυμητή ανάλυση, και (4) κλήση του `Converter.convert`. Χωρίς εξωτερικά εργαλεία, χωρίς γραμμή εντολών — μόνο καθαρή Java.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

- **Java 17** (ή οποιοδήποτε πρόσφατο JDK) εγκατεστημένο και ρυθμισμένο στο IDE σας.
- **Aspose.HTML for Java** βιβλιοθήκη (το Maven artifact `com.aspose:aspose-html`). Μπορείτε να την κατεβάσετε από το [Aspose Maven repository](https://repo.aspose.com/repo) ή να κατεβάσετε το JAR απευθείας.
- Ένα απλό αρχείο HTML (`page.html`) που θέλετε να μετατρέψετε σε PNG. Τοποθετήστε το κάπου προσβάσιμο, π.χ. `C:/temp/page.html`.
- Βασική εξοικείωση με τη διαχείριση εξαιρέσεων της Java — τίποτα περίπλοκο.

Αν κάποιο από τα παραπάνω σας φαίνεται άγνωστο, κάντε μια παύση και εγκαταστήστε το απαιτούμενο κομμάτι. Το υπόλοιπο του οδηγού υποθέτει ότι είστε άνετοι με το άνοιγμα ενός Java project και την προσθήκη εξωτερικών JAR.

## Βήμα 1: Ρυθμίστε το Maven Project σας (ή Προσθέστε το JAR Χειροκίνητα)

Αν χρησιμοποιείτε Maven, προσθέστε την εξάρτηση στο `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>24.11</version> <!-- Check for the newest version -->
</dependency>
```

Διαφορετικά, τοποθετήστε το `aspose-html-*.jar` στον φάκελο `libs` του project και προσθέστε το στο build path. Αυτό το βήμα δεν αφορά άμεσα το **πώς να ορίσετε DPI**, αλλά χωρίς τη βιβλιοθήκη δεν μπορείτε να έχετε πρόσβαση στην κλάση `Sandbox` που καθιστά δυνατός ο έλεγχος DPI.

## Βήμα 2: Δημιουργήστε ένα Sandbox που Προσομοιώνει Πραγματική Οθόνη

Ένα *sandbox* είναι ο τρόπος του Aspose να αναπαράγει ένα περιβάλλον περιηγητή. Σκεφτείτε το ως ένα εικονικό monitor όπου καθορίζετε το πλάτος, το ύψος και, κυρίως, το **DPI**. Ακολουθεί το απόσπασμα κώδικα που δημιουργεί μια οθόνη 1024 × 768 σε 96 dpi — ένα βασικό σημείο εκκίνησης πριν αυξήσουμε την ανάλυση:

```java
// Step 2.1: Initialise the sandbox
Sandbox sandbox = new Sandbox();

// Step 2.2: Define virtual screen dimensions (pixels)
sandbox.setScreenWidth(1024);
sandbox.setScreenHeight(768);

// Step 2.3: Set the DPI – this is the key to controlling image sharpness
sandbox.setDpi(96); // Change this value to 300, 600, etc., later
```

> **Γιατί ένα sandbox;** Χωρίς αυτό, το Aspose θα επανέλθει στις ρυθμίσεις οθόνης του κεντρικού υπολογιστή, οδηγώντας σε ασυνεπή αποτελέσματα μεταξύ διαφορετικών μηχανών ανάπτυξης. Κλειδώνοντας το DPI, εξασφαλίζετε ότι κάθε μετατροπή θα φαίνεται το ίδιο, είτε τρέχει σε laptop είτε σε CI server.

## Βήμα 3: Διαμορφώστε τις Επιλογές Μετατροπής Εικόνας – Ορίστε την Ανάλυση Εικόνας

Τώρα που το sandbox είναι έτοιμο, λέμε στον μετατροπέα ποια **ανάλυση εικόνας** θέλουμε. Η κλάση `ImageConversionOptions` σας επιτρέπει να ορίσετε το DPI του εξαγόμενου PNG ανεξάρτητα από το DPI του sandbox, δίνοντάς σας δύο μοχλούς ελέγχου.

```java
// Step 3.1: Prepare conversion options
ImageConversionOptions conversionOptions = new ImageConversionOptions();

// Step 3.2: Desired output DPI – this directly influences PNG quality
conversionOptions.setResolution(300); // 300 dpi is print‑quality; increase for sharper prints

// Step 3.3: Bind the sandbox to the options so the layout engine respects our virtual screen
conversionOptions.setSandbox(sandbox);
```

**Συμβουλή:** Αν θέλετε ένα PNG 600 dpi για φυλλάδια υψηλής ποιότητας, απλώς αλλάξτε το `setResolution(300)` σε `setResolution(600)`. Λάβετε υπόψη ότι μεγαλύτερες τιμές DPI αυξάνουν την κατανάλωση μνήμης και τον χρόνο επεξεργασίας, οπότε δοκιμάστε πρώτα με μια μικρή σελίδα.

## Βήμα 4: Μετατρέψτε τη Σελίδα HTML σε PNG

Με το sandbox και τις επιλογές στη θέση τους, το πραγματικό βήμα **convert html to png** είναι μια γραμμή κώδικα:

```java
// Step 4: Perform the conversion
Converter.convert(
        "C:/temp/page.html",   // Source HTML file (convert html page)
        "C:/temp/page.png",    // Destination PNG file
        conversionOptions);    // Options that include DPI and sandbox
```

Αν όλα πάνε ομαλά, θα δείτε το μήνυμα στην κονσόλα από το επόμενο βήμα.

## Βήμα 5: Επαληθεύστε το Αποτέλεσμα και Εκτυπώστε Επιβεβαίωση

Μια γρήγορη `System.out.println` σας λέει ότι η εργασία ολοκληρώθηκε. Σε πραγματικό project ίσως θέλετε να ελέγξετε το μέγεθος του αρχείου, τις διαστάσεις ή ακόμη και να ανοίξετε το PNG προγραμματιστικά για να επικυρώσετε το DPI.

```java
System.out.println("PNG generated with sandboxed layout at 300 dpi.");
```

Η εκτέλεση της κλάσης θα πρέπει να δημιουργήσει το `page.png` στον ίδιο φάκελο με το αρχείο HTML. Ανοίξτε το σε προβολέα εικόνας που εμφανίζει DPI (π.χ. Windows Photo Viewer → Properties → Details) και βεβαιωθείτε ότι εμφανίζει **300 dpi**.

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι μια αυτόνομη κλάση Java που μπορείτε να αντιγράψετε‑επικολλήσετε στο IDE σας:

```java
import com.aspose.html.conversions.Converter;
import com.aspose.html.conversions.options.ImageConversionOptions;
import com.aspose.html.sandbox.Sandbox;

public class HtmlToPngWithSandbox {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox that simulates a 1024×768 screen with 96 dpi.
        Sandbox sandbox = new Sandbox();
        sandbox.setScreenWidth(1024);
        sandbox.setScreenHeight(768);
        sandbox.setDpi(96); // <-- This is where you learn how to set dpi

        // Step 2: Configure image conversion options – 300 dpi PNG using the sandbox.
        ImageConversionOptions conversionOptions = new ImageConversionOptions();
        conversionOptions.setResolution(300); // Set image resolution (dpi)
        conversionOptions.setSandbox(sandbox);

        // Step 3: Convert the HTML page to a PNG image using the defined options.
        Converter.convert(
                "C:/temp/page.html",   // convert html page
                "C:/temp/page.png",    // output PNG
                conversionOptions);    // includes dpi and resolution settings

        // Step 4: Indicate that the conversion has completed.
        System.out.println("PNG generated with sandboxed layout at 300 dpi.");
    }
}
```

> **Θυμηθείτε:** Η γραμμή `sandbox.setDpi(96);` είναι το τμήμα *πώς να ορίσετε dpi*. Προσαρμόστε το ώστε να ταιριάζει με την πυκνότητα οθόνης που χρειάζεστε· το `conversionOptions.setResolution(300);` ελέγχει το τελικό DPI της εικόνας.

## Διαχείριση Συνηθισμένων Προβλημάτων

| Κατάσταση | Τι να προσέξετε | Προτεινόμενη Διόρθωση |
|-----------|-------------------|---------------|
| **Out‑of‑Memory errors** όταν χρησιμοποιείτε 600 dpi | Το υψηλό DPI αυξάνει δραματικά το μέγεθος του raster (π.χ. 1024 × 768 @ 600 dpi ≈ 4 MP). | Μειώστε τις διαστάσεις της οθόνης ή κάντε streaming τη μετατροπή χρησιμοποιώντας callbacks του `ConversionProgress`. |
| **HTML uses external CSS/JS that isn’t loading** | Το sandbox λειτουργεί σε απομόνωση· οι απομακρυσμένοι πόροι πρέπει να είναι προσβάσιμοι. | Παρέχετε απόλυτες URL ή ενσωματώστε το CSS απευθείας στο HTML. |
| **Incorrect DPI in the output** | Αλλάξατε το `sandbox.setDpi` αλλά ξεχάσατε να προσαρμόσετε το `conversionOptions.setResolution`. | Βεβαιωθείτε ότι και οι δύο τιμές ευθυγραμμίζονται με το επιθυμητό αποτέλεσμα. |
| **FileNotFoundException** | Λάθος διαδρομή ή έλλειψη δικαιωμάτων αρχείου. | Χρησιμοποιήστε `Paths.get(...).toAbsolutePath()` και ελέγξτε τα δικαιώματα ανάγνωσης/εγγραφής. |

## Προχωρημένες Παραλλαγές

### 1. Διαφορετικές Μορφές Εξόδου

Το Aspose.HTML δεν περιορίζεται μόνο σε PNG. Αλλάξτε την επέκταση του αρχείου και χρησιμοποιήστε την αντίστοιχη κλάση επιλογών, π.χ. `JpegConversionOptions` για JPEG. Η λογική DPI παραμένει η ίδια.

```java
import com.aspose.html.conversions.options.JpegConversionOptions;

// ...

JpegConversionOptions jpegOpts = new JpegConversionOptions();
jpegOpts.setResolution(300);
jpegOpts.setSandbox(sandbox);

Converter.convert("page.html", "page.jpg", jpegOpts);
```

### 2. Δυναμικός Προσδιορισμός Μεγέθους Οθόνης

Αν χρειάζεται το sandbox να προσομοιώνει κινητή συσκευή, διαβάστε τις διαστάσεις από ένα αρχείο ρυθμίσεων:

```java
sandbox.setScreenWidth(Integer.parseInt(System.getProperty("screen.width", "375")));
sandbox.setScreenHeight(Integer.parseInt(System.getProperty("screen.height", "667")));
sandbox.setDpi(Integer.parseInt(System.getProperty("screen.dpi", "96")));
```

Τρέξτε με `-Dscreen.width=375 -Dscreen.height=667 -Dscreen.dpi=326` για να προσομοιώσετε μια οθόνη iPhone Retina.

### 3. Μαζική Μετατροπή

Τυλίξτε την κλήση μετατροπής μέσα σε βρόχο που διατρέχει έναν φάκελο με αρχεία HTML. Θυμηθείτε να επαναχρησιμοποιήσετε τα ίδια αντικείμενα `Sandbox` και `ImageConversionOptions` για να αποφύγετε περιττές κατανομές μνήμης.

```java
Files.list(Paths.get("C:/temp/html"))
     .filter(p -> p.toString().endsWith(".html"))
     .forEach(htmlPath -> {
         String pngPath = htmlPath.toString().replace(".html", ".png");
         Converter.convert(htmlPath.toString(), pngPath, conversionOptions);
     });
```

## Αναμενόμενο Αποτέλεσμα

Η εκτέλεση της κλάσης με τις προεπιλεγμένες ρυθμίσεις παράγει ένα αρχείο PNG περίπου **1024 × 768 pixel** σε **300 dpi**. Στους περισσότερους επεξεργαστές εικόνας οι διαστάσεις θα εμφανίζονται ως 1024 × 768, ενώ τα μεταδεδομένα DPI θα δείχνουν 300. Αν εκτυπώσετε την εικόνα με πλάτος 1 ίντσα, θα έχετε μια καθαρή γραμμή 300 pixel — ιδανική για φυλλάδια υψηλής ποιότητας.

## Οπτική Σύνοψη

![πώς να ορίσετε dpi στην μετατροπή Aspose HTML](/images/aspose-dpi-example.png "πώς να ορίσετε dpi – Παράδειγμα sandbox Aspose HTML")

*Το στιγμιότυπο δείχνει τα μεταδεδομένα DPI του παραγόμενου PNG (300 dpi).*

## Συμπέρασμα

Καλύψαμε **πώς να ορίσετε DPI** όταν **μετατρέπετε HTML σε PNG** χρησιμοποιώντας τον **Aspose HTML Converter** σε Java. Δημιουργώντας ένα sandbox, διαμορφώνοντας το `ImageConversionOptions` και καλώντας το `Converter.convert`, αποκτάτε τέλεια έλεγχο τόσο στην προσομοίωση οθόνης όσο και στην τελική ανάλυση εικόνας. Είτε παράγετε τιμολόγια εκτυπώσιμα, είτε assets web υψηλής ανάλυσης, είτε αυτόματες μικρογραφίες, το ίδιο μοτίβο ισχύει — απλώς προσαρμόστε το DPI και το μέγεθος οθόνης ώστε να ταιριάζει στις ανάγκες σας.

## Τι Θα Μάθετε Στη Σειρά Επόμενη;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας projects.

- [Πώς να χρησιμοποιήσετε το Aspose για απόδοση HTML σε PNG – Οδηγός βήμα-βήμα](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [Πώς να μετατρέψετε HTML σε JPEG χρησιμοποιώντας το Aspose.HTML for Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-jpeg/)
- [Πώς να μετατρέψετε HTML σε BMP με το Aspose.HTML for Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-bmp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
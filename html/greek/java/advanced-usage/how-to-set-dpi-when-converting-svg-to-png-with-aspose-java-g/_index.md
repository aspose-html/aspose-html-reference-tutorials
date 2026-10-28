---
category: general
date: 2026-04-23
description: Μάθετε πώς να ορίζετε το DPI για εξαιρετικά υψηλής ποιότητας μετατροπή
  SVG σε PNG στη Java χρησιμοποιώντας το Aspose. Περιλαμβάνει κώδικα βήμα‑βήμα, συμβουλές
  και διαχείριση ακραίων περιπτώσεων.
draft: false
keywords:
- how to set dpi
- convert svg to png
- svg to png java
- how to convert svg
- aspose svg to png
language: el
og_description: Μάθετε πώς να ορίζετε το DPI για τη μετατροπή SVG σε PNG χρησιμοποιώντας
  το Aspose HTML σε Java. Πλήρης κώδικας, εξηγήσεις και συμβουλές βέλτιστων πρακτικών.
og_title: Πώς να ορίσετε το DPI κατά τη μετατροπή SVG σε PNG – Java Tutorial
tags:
- Aspose
- Java
- SVG
- PNG
- Image Conversion
title: Πώς να ορίσετε DPI κατά τη μετατροπή SVG σε PNG με το Aspose – Οδηγός Java
url: /el/java/advanced-usage/how-to-set-dpi-when-converting-svg-to-png-with-aspose-java-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ορίσετε DPI κατά τη μετατροπή SVG σε PNG με το Aspose – Οδηγός Java

Έχετε αναρωτηθεί ποτέ **πώς να ορίσετε DPI** για ένα κρυστάλλινο PNG που προέρχεται από SVG; Ίσως δημιουργείτε μια διαδικασία branding και χρειάζεστε το λογότυπο στα 600 dpi για εκτύπωση, ή απλώς θέλετε η ραστερ εικόνα να φαίνεται οξεία σε οθόνες υψηλής ανάλυσης. Τα καλά νέα είναι ότι δεν χρειάζεται να μαντεύετε—το Aspose HTML for Java το κάνει εύκολο.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα **πώς να ορίσετε DPI** ενώ **μετατρέπετε SVG σε PNG** χρησιμοποιώντας τη βιβλιοθήκη Aspose. Θα λάβετε ένα πλήρες, έτοιμο‑για‑εκτέλεση δείγμα κώδικα, εξήγηση κάθε επιλογής διαμόρφωσης, και μια σειρά πρακτικών συμβουλών για πραγματικά έργα. Δεν απαιτούνται εξωτερικές αναφορές—όλα όσα χρειάζεστε είναι εδώ.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

- Java 17 (ή οποιοδήποτε πρόσφατο JDK) εγκατεστημένο.
- Maven ή Gradle για διαχείριση εξαρτήσεων (θα δείξουμε το απόσπασμα Maven).
- Ένα αρχείο SVG που θέλετε να ραστερίσετε (π.χ. `logo.svg`).
- Βασική κατανόηση της σύνταξης Java—τίποτα περίπλοκο, μόνο το συνηθισμένο `public static void main`.

Αν λείπει κάτι από τα παραπάνω, κατεβάστε το πρώτα· το υπόλοιπο του οδηγού υποθέτει ότι είναι ήδη στη θέση του.

## Εξάρτηση Maven

Προσθέστε την εξάρτηση Aspose HTML for Java στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

Οι χρήστες Gradle μπορούν να αντικαταστήσουν το απόσπασμα με την ισοδύναμη γραμμή `implementation "com.aspose:aspose-html:23.12"`.

## Βήμα 1: Δημιουργία του αντικειμένου επιλογών μετατροπής

Το πρώτο που πρέπει να κάνετε είναι να δημιουργήσετε ένα `SvgConversionOptions`. Αυτό το αντικείμενο περιέχει κάθε ρύθμιση που μπορεί να θέλετε—DPI, χρώμα φόντου, κλιμάκωση κ.λπ.

```java
// Step 1: Build conversion options for SVG → PNG
SvgConversionOptions conversionOptions = new SvgConversionOptions();
```

Γιατί είναι σημαντικό: χωρίς ρητό ορισμό DPI, το Aspose χρησιμοποιεί προεπιλογή 96 dpi, που είναι εντάξει για web αλλά μακριά από την εκτυπώσιμη ποιότητα. Δημιουργώντας το αντικείμενο επιλογών, αποκτάτε πλήρη έλεγχο της διαδικασίας ραστεροποίησης.

## Βήμα 2: Ορισμός του επιθυμητού DPI

Τώρα απαντάμε στην κεντρική ερώτηση: **πώς να ορίσετε DPI**. Η μέθοδος `setDpi(int)` δέχεται έναν ακέραιο αριθμό· τυπικές τιμές κυμαίνονται από 72 dpi (χαμηλή ανάλυση) έως 1200 dpi (υψηλή ανάλυση). Για τις περισσότερες εργασίες εκτύπωσης, 300 dpi είναι το ιδανικό σημείο· για λογότυπα που πρέπει να κλιμακώνονται, 600 dpi είναι μια ασφαλής επιλογή.

```java
// Step 2: Define the resolution (DPI) – 600 DPI for ultra‑high‑quality output
conversionOptions.setDpi(600);
```

> **Συμβουλή επαγγελματία:** τιμές DPI που δεν είναι πολλαπλάσια του 72 μπορεί μερικές φορές να παράγουν μη ακέραιες διαστάσεις pixel. Αν χρειάζεστε ακριβές μέγεθος pixel, υπολογίστε `pixel = inches * DPI` εκ των προτέρων και προσαρμόστε το `viewBox` του SVG ανάλογα.

## Βήμα 3: Διαχείριση διαφάνειας με χρώμα φόντου

Τα SVG συχνά περιέχουν διαφανείς περιοχές. Το PNG υποστηρίζει διαφάνεια, αλλά αν στο workflow εκτύπωσης απαιτείται αδιαφανές φόντο, θα θέλετε να το αντικαταστήσετε. Η μέθοδος `setBackgroundColor(String)` δέχεται οποιοδήποτε συμβολοσειρά χρώματος συμβατή με CSS.

```java
// Step 3: Replace transparent areas with white (or any color you prefer)
conversionOptions.setBackgroundColor("white");
```

Μπορείτε επίσης να χρησιμοποιήσετε `#FFFFFF`, `rgb(255,255,255)`, ή ακόμη και `transparent` αν *θέλετε* να διατηρήσετε το κανάλι άλφα.

## Βήμα 4: Εκτέλεση της μετατροπής

Με τις επιλογές διαμορφωμένες, η πραγματική μετατροπή είναι μια μόνο στατική κλήση στο `Converter.convert`. Παρέχετε τη διαδρομή εισόδου SVG, τη διαδρομή εξόδου PNG, και το αντικείμενο επιλογών.

```java
// Step 4: Convert the SVG file to a PNG using the configured options
Converter.convert(
        "YOUR_DIRECTORY/logo.svg",   // Input SVG
        "YOUR_DIRECTORY/logo.png",   // Output PNG
        conversionOptions);          // Options we just set
```

Αυτό είναι—το Aspose αναλαμβάνει την ανάλυση του SVG, την εφαρμογή της κλιμάκωσης DPI, τη συμπλήρωση του φόντου, και τη γραφή του αρχείου PNG στο δίσκο.

## Πλήρες, Εκτελέσιμο Παράδειγμα

Παρακάτω βρίσκεται η πλήρης κλάση Java που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε ένα αρχείο με όνομα `SvgToPngHighRes.java`. Αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή φακέλου στο σύστημά σας.

```java
import com.aspose.html.converters.SvgConversionOptions;
import com.aspose.html.converters.Converter;

/**
 * Demonstrates how to set DPI when converting an SVG file to a high‑resolution PNG
 * using Aspose.HTML for Java.
 *
 * Prerequisites:
 *   - Aspose.HTML for Java library (Maven dependency shown earlier)
 *   - Java 17+ runtime
 *
 * Expected result:
 *   - logo.png created at 600 DPI with a white background.
 */
public class SvgToPngHighRes {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create conversion options for SVG → PNG
        SvgConversionOptions conversionOptions = new SvgConversionOptions();

        // 2️⃣ Set the desired resolution (DPI) – 600 DPI yields ultra‑high‑quality output
        conversionOptions.setDpi(600);

        // 3️⃣ Define a background color to replace any transparency (white works for most prints)
        conversionOptions.setBackgroundColor("white");

        // 4️⃣ Convert the SVG file to a PNG using the configured options
        Converter.convert(
                "YOUR_DIRECTORY/logo.svg",   // <-- change this to your source file
                "YOUR_DIRECTORY/logo.png",   // <-- change this to your target file
                conversionOptions);

        System.out.println("Conversion complete! Check YOUR_DIRECTORY/logo.png");
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Η εκτέλεση του προγράμματος θα δημιουργήσει το `logo.png` στον ίδιο φάκελο. Ανοίξτε το αρχείο σε προβολέα εικόνας και ελέγξτε τις **ιδιότητες εικόνας**—θα πρέπει να δείτε:

- **Ανάλυση:** 600 dpi (ή όποια τιμή έχετε ορίσει)
- **Διαστάσεις:** Κλιμακωμένες σύμφωνα με το αρχικό `viewBox` του SVG πολλαπλασιασμένο με τον παράγοντα DPI
- **Φόντο:** Σταθερό λευκό (χωρίς διαφανή pixel)

Αν ανοίξετε το PNG σε εργαλείο όπως το Photoshop, τα μεταδεδομένα DPI θα είναι ορατά στο *Image → Image Size*.

## Συνηθισμένες Περιπτώσεις & Πώς να τις Διαχειριστείτε

| Κατάσταση | Σε τι πρέπει να προσέξετε | Προτεινόμενη Διόρθωση |
|-----------|---------------------------|------------------------|
| **Απουσία αρχείου SVG** | Εξαίρεση `FileNotFoundException` που ρίχνει το `Converter.convert` | Επαληθεύστε τη διαδρομή πριν τη μετατροπή χρησιμοποιώντας `Files.exists(Paths.get(...))`. |
| **Μη υποστηριζόμενα χαρακτηριστικά SVG** (π.χ. φίλτρα που δεν έχουν υλοποιηθεί) | Το Aspose μπορεί να παραλείψει αυτά τα χαρακτηριστικά σιωπηλά | Χρησιμοποιήστε `SvgConversionOptions.setEnableSvgFilters(true)` αν χρειάζεστε υποστήριξη φίλτρων (διαθέσιμο σε νεότερες εκδόσεις). |
| **Πολύ υψηλό DPI (≥1200)** | Το αρχείο εξόδου μπορεί να γίνει τεράστιο (εκατοντάδες MB) | Σκεφτείτε τη ροή (streaming) του αποτελέσματος ή μειώστε το DPI για μεγάλες εικόνες. |
| **Διατήρηση διαφάνειας** | Ορίσατε χρώμα φόντου αλλά στην πραγματικότητα θέλετε άλφα | Παραλείψτε το `setBackgroundColor` ή περάστε `"transparent"` για να κρατήσετε το αρχικό κανάλι άλφα. |
| **Μαζική μετατροπή** | Η δημιουργία νέου `SvgConversionOptions` για κάθε αρχείο είναι σπατάλη | Δημιουργήστε μία μόνο παρουσία `SvgConversionOptions` και επαναχρησιμοποιήστε την μέσα σε βρόχο. |

## Συχνές Ερωτήσεις

**Ε: Λειτουργεί αυτό και με άλλες μορφές ραστερ όπως JPEG ή BMP;**  
Α: Ναι. Απλώς αντικαταστήστε την επέκταση αρχείου εξόδου (`.png`) με `.jpg` ή `.bmp`, και το Aspose θα επιλέξει αυτόματα τον κατάλληλο κωδικοποιητή. Μπορείτε επίσης να ρυθμίσετε την ποιότητα JPEG μέσω `JpegConversionOptions`.

**Ε: Μπορώ να μετατρέψω SVG που είναι αποθηκευμένα σε byte array αντί για αρχείο;**  
Α: Απόλυτα. Χρησιμοποιήστε τις υπερφορτώσεις `Converter.convert(InputStream, OutputStream, conversionOptions)` για να δουλέψετε με ροές, κάτι που είναι χρήσιμο για web services.

**Ε: Είναι η ρύθμιση DPI το ίδιο με την κλιμάκωση της εικόνας;**  
Α: Το DPI είναι μια μετα-πληροφορία που λέει στους εκτυπωτές πόσα pixel αντιστοιχούν σε μία ίντσα. Εσωτερικά, το Aspose κλιμακώνει την ραστερ εικόνα ώστε να ταιριάζει στο DPI, οπότε το οπτικό μέγεθος αλλάζει αν δείτε το PNG σε 100 % ζουμ σε προβολέα που σέβεται το DPI.

## Συμβουλές για Κώδικα Έτοιμο για Παραγωγή

1. **Cache τις Επιλογές** – Αν μετατρέπετε δεκάδες λογότυπα με το ίδιο DPI και φόντο, δημιουργήστε το `SvgConversionOptions` μία φορά και επαναχρησιμοποιήστε το. Μειώνει το κόστος δημιουργίας αντικειμένων.
2. **Επαλήθευση Διαστάσεων Εισόδου** – Για εξαιρετικά μεγάλα SVG, υπολογίστε το αναμενόμενο μέγεθος pixel (`width * DPI/96`) και ακυρώστε αν υπερβαίνει ένα ασφαλές όριο (π.χ. 20 000 px) για να αποφύγετε `OutOfMemoryError`.
3. **Καταγραφή Μεταδεδομένων Μετατροπής** – Αποθηκεύστε το DPI, το όνομα αρχείου προέλευσης και την χρονική σήμανση σε αρχείο log· διευκολύνει τον εντοπισμό σφαλμάτων αργότερα.
4. **Ασφάλεια σε Πολυνηματικό Περιβάλλον** – Η μέθοδος `Converter.convert` είναι thread‑safe, οπότε μπορείτε να παραλληλοποιήσετε μαζικές εργασίες με ένα `ExecutorService`.

## Οπτική Σύνοψη

![how to set dpi example](image.png){: .align-center alt="παράδειγμα ορισμού dpi"}

Το παραπάνω διάγραμμα απεικονίζει τη ροή: **SVG → ορισμός DPI & φόντου → PNG**.

## Συμπέρασμα

Τώρα ξέρετε **πώς να ορίσετε DPI** όταν **μετατρέπετε SVG σε PNG** χρησιμοποιώντας το Aspose HTML for Java. Με τη διαμόρφωση του `SvgConversionOptions` ελέγχετε την ανάλυση, τη διαχείριση φόντου, και πολλά άλλα, μετατρέποντας ένα απλό αρχείο διανυσματικού σε ραστερ έτοιμο για εκτύπωση με λίγες μόνο γραμμές κώδικα.

Δοκιμάστε τα επόμενα:

- Μετατροπή ολόκληρου φακέλου SVG σε batch loop.
- Αλλαγή της μορφής εξόδου σε JPEG για assets βελτιστοποιημένα για web.
- Χρήση άλλων επιλογών μετατροπής Aspose όπως `setScaleX/Y` για προσαρμοσμένη κλιμάκωση πέρα από το DPI.

Καλό coding, και εύχομαι τα PNG σας να είναι πάντα τόσο καθαρά όσο χρειάζεστε!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
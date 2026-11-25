---
category: general
date: 2026-05-06
description: Πώς να ορίσετε DPI για μετατροπή SVG σε PNG υψηλής ανάλυσης σε Java χρησιμοποιώντας
  το Aspose.HTML. Μάθετε πώς να μετατρέψετε SVG σε PNG, να εξάγετε SVG ως PNG και
  να μετατρέψετε διανυσματικό σε ραστερ.
draft: false
keywords:
- how to set dpi
- convert svg to png
- how to convert svg
- export svg as png
- convert vector to raster
language: el
og_description: Πώς να ορίσετε το DPI για μετατροπή SVG σε PNG υψηλής ανάλυσης σε
  Java χρησιμοποιώντας το Aspose.HTML. Λάβετε κώδικα βήμα‑προς‑βήμα και επαγγελματικές
  συμβουλές.
og_title: Πώς να ορίσετε DPI κατά τη μετατροπή SVG σε PNG – Οδηγός Java
tags:
- Java
- Aspose.HTML
- Image Conversion
title: Πώς να ορίσετε DPI κατά τη μετατροπή SVG σε PNG – Οδηγός Java
url: /el/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ορίσετε DPI κατά τη μετατροπή SVG σε PNG – Οδηγός Java

Έχετε αναρωτηθεί ποτέ **πώς να ορίσετε DPI** για μια μετατροπή SVG‑σε‑PNG και να έχετε μια καθαρή, έτοιμη για εκτύπωση εικόνα; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν το εξαγόμενο PNG φαίνεται θολό επειδή το προεπιλεγμένο DPI (συνήθως 96) δεν είναι αρκετό για επαγγελματικό αποτέλεσμα.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει **πώς να ορίσετε DPI** χρησιμοποιώντας το Aspose.HTML για Java. Στο τέλος θα μπορείτε να **μετατρέψετε SVG σε PNG**, **εξάγετε SVG ως PNG**, και ακόμη **μετατρέψετε vector σε raster** με οποιοδήποτε DPI χρειάζεστε — χωρίς μυστήριο, μόνο καθαρός κώδικας.

## Τι θα μάθετε

- Τα ακριβή βήματα για τη ρύθμιση DPI πριν από τη μετατροπή.
- Γιατί το DPI είναι σημαντικό όταν **μετατρέπετε vector σε raster**.
- Πώς να **μετατρέψετε SVG σε PNG** με μία μόνο γραμμή κώδικα.
- Συμβουλές για τη διαχείριση μεγάλων SVG και την επεξεργασία σε παρτίδες.
- Ένα πλήρες, μεταγλωττιζόμενο πρόγραμμα που μπορείτε να ενσωματώσετε αμέσως στο έργο σας.

## Προαπαιτήσεις

Πριν προχωρήσουμε, βεβαιωθείτε ότι έχετε:

- Java 17 ή νεότερη (η τελευταία LTS έκδοση λειτουργεί καλύτερα).
- Maven ή Gradle για να κατεβάσετε τη βιβλιοθήκη Aspose.HTML.
- Ένα απλό αρχείο SVG που θέλετε να rasterize (π.χ. `logo.svg`).
- Ένα IDE ή κειμενογράφο — IntelliJ IDEA, VS Code, ή ακόμη και το απλό Notepad.

Δεν απαιτούνται άλλα εξωτερικά εργαλεία· η βιβλιοθήκη κάνει όλη τη βαριά δουλειά.

## Βήμα 1: Προσθήκη Aspose.HTML στο έργο σας

Πρώτα απ' όλα, χρειάζεστε το JAR του Aspose.HTML. Αν χρησιμοποιείτε Maven, προσθέστε αυτό το απόσπασμα στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

Για Gradle, είναι ως εξής:

```groovy
implementation 'com.aspose:aspose-html:23.10'
```

> **Pro tip:** Πάντα χρησιμοποιείτε την πιο πρόσφατη σταθερή έκδοση· οι νεότερες κυκλοφορίες περιλαμβάνουν διορθώσεις απόδοσης για rendering υψηλού DPI.

## Βήμα 2: Πώς να ορίσετε DPI για τη μετατροπή

Τώρα φτάνουμε στην ουσία — **πώς να ορίσετε DPI**. Το Aspose.HTML εκθέτει το `ImageConversionOptions`, όπου μπορείτε να καθορίσετε τόσο την οριζόντια (`dpiX`) όσο και την κάθετη (`dpiY`) ανάλυση. Ορίζοντας και τα δύο σε `300` παίρνετε την κλασική πυκνότητα εκτύπωσης.

```java
import com.aspose.html.converters.ImageConversionOptions;
import com.aspose.html.rendering.Converter;

public class SvgHighRes {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create conversion options
        ImageConversionOptions conversionOptions = new ImageConversionOptions();

        // 2️⃣ Set target DPI for high‑resolution output (300 dpi → crisp print quality)
        conversionOptions.setDpiX(300);
        conversionOptions.setDpiY(300);

        // 3️⃣ Convert the SVG file to a PNG using the configured options
        Converter.convertSvgToPng(
                "YOUR_DIRECTORY/logo.svg",        // source SVG
                "YOUR_DIRECTORY/logo_300dpi.png", // destination PNG
                conversionOptions);
    }
}
```

> **Γιατί 300 dpi;** Είναι το de‑facto πρότυπο για επαγγελματική εκτύπωση. Αν χρειάζεστε εικόνα για web, 72 dpi αρκεί, αλλά για φυλλάδια ή μπροσούρες θα θέλετε τουλάχιστον 300 dpi.

### Προεπισκόπηση εικόνας

![Πώς να ορίσετε DPI κατά τη μετατροπή SVG σε PNG](https://example.com/placeholder.png "Πώς να ορίσετε DPI κατά τη μετατροπή SVG σε PNG")

*Η παραπάνω εικόνα δείχνει τη διαφορά μεταξύ ενός PNG χαμηλού DPI (αριστερά) και ενός εξόδου 300 dpi (δεξιά).*

## Βήμα 3: Μετατροπή SVG σε PNG – Μία Γραμμή Κώδικα

Αν θέλετε απλώς μια γρήγορη **μετατροπή svg σε png** χωρίς να ασχοληθείτε με DPI, μπορείτε να παραλείψετε εντελώς το αντικείμενο επιλογών:

```java
Converter.convertSvgToPng("logo.svg", "logo_default.png", null);
```

Η παράμετρος `null` λέει στο Aspose.HTML να χρησιμοποιήσει το προεπιλεγμένο DPI του (συνήθως 96). Αυτό είναι χρήσιμο για μικρογραφίες ή όταν δεν σας ενδιαφέρει η ποιότητα εκτύπωσης.

## Βήμα 4: Επαλήθευση του αποτελέσματος – Εξαγωγή SVG ως PNG

Μετά το τέλος της μετατροπής, ανοίξτε το παραγόμενο PNG σε οποιονδήποτε προβολέα εικόνας. Θα πρέπει να δείτε μια raster εικόνα που ταιριάζει στις διαστάσεις του αρχικού vector, αλλά τώρα φέρει το DPI που ορίσατε. Οι περισσότεροι προβολείς εμφανίζουν το DPI στις ιδιότητες της εικόνας· στα Windows, δεξί‑κλικ → Properties → Details.

Αν χρειάζεται να επαληθεύσετε προγραμματιστικά το DPI, η `ImageIO` της Java μπορεί να το διαβάσει:

```java
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;

BufferedImage img = ImageIO.read(new File("logo_300dpi.png"));
int dpi = (int) img.getProperty("dpi");
System.out.println("Exported PNG DPI: " + dpi);
```

> **Σημείωση:** Δεν αποθηκεύουν όλα τα φορμά εικόνας μεταδεδομένα DPI· το PNG το κάνει, αλλά το JPEG μπορεί να απαιτεί επιπλέον διαχείριση.

## Ακραίες Περιπτώσεις & Παραλλαγές

### 1️⃣ Διαφορετικές τιμές DPI

Μπορεί να αναρωτιέστε, “Τι γίνεται αν χρειαστώ 600 dpi για μεγάλο πόστερ?” Απλώς αλλάξτε τους αριθμούς:

```java
conversionOptions.setDpiX(600);
conversionOptions.setDpiY(600);
```

Υψηλότερο DPI σημαίνει μεγαλύτερο μέγεθος αρχείου, οπότε προσέξτε τους περιορισμούς μνήμης όταν επεξεργάζεστε πολλά αρχεία.

### 2️⃣ Μετατροπή παρτίδας φακέλου

Όταν έχετε δεκάδες SVG, τυλίξτε τη μετατροπή σε έναν απλό βρόχο:

```java
File dir = new File("YOUR_DIRECTORY");
for (File svg : dir.listFiles((d, name) -> name.endsWith(".svg"))) {
    String pngName = svg.getName().replace(".svg", "_300dpi.png");
    Converter.convertSvgToPng(svg.getAbsolutePath(),
                              new File(dir, pngName).getAbsolutePath(),
                              conversionOptions);
}
```

Αυτό το μοτίβο **μετατρέπει vector σε raster** μαζικά, εξοικονομώντας σας ώρες χειροκίνητης εργασίας.

### 3️⃣ Διαχείριση διαφανούς φόντου

Αν το SVG σας περιέχει διαφάνεια και θέλετε λευκό φόντο, αποδώστε πρώτα σε ένα `BufferedImage`, έπειτα γεμίστε το φόντο:

```java
// Render SVG to BufferedImage with DPI
BufferedImage raster = Converter.convertSvgToImage(
        "logo.svg", conversionOptions);

// Fill background (optional)
Graphics2D g = raster.createGraphics();
g.setComposite(AlphaComposite.SrcOver);
g.setColor(Color.WHITE);
g.fillRect(0, 0, raster.getWidth(), raster.getHeight());
g.dispose();

// Write out PNG
ImageIO.write(raster, "png", new File("logo_whitebg.png"));
```

## Συχνές Ερωτήσεις

**Ε: Λειτουργεί αυτό σε Linux;**  
Α: Απόλυτα. Το Aspose.HTML είναι ανεξάρτητο από πλατφόρμα· απλώς βεβαιωθείτε ότι έχετε το κατάλληλο Java runtime.

**Ε: Τι γίνεται αν το SVG μου αναφέρεται σε εξωτερικές εικόνες;**  
Α: Βεβαιωθείτε ότι οι πόροι είναι προσβάσιμοι μέσω απόλυτων διαδρομών ή URLs· διαφορετικά ο renderer θα τους παραλείψει.

**Ε: Μπορώ να μετατρέψω SVG σε άλλες μορφές raster όπως JPEG ή BMP;**  
Α: Ναι. Χρησιμοποιήστε `Converter.convertSvgToJpeg` ή `Converter.convertSvgToBmp` με τις ίδιες `ImageConversionOptions`.

## Pro Tips για Υψηλής Ποιότητας Rasterization

- **Ταιριάξτε το DPI με το τελικό μέγεθος εξόδου.** Ένα λογότυπο 2 ίντσες που εκτυπώνεται στα 300 dpi χρειάζεται πλάτος 600 px (2 in × 300 dpi). Κλιμακώστε το SVG αναλόγως πριν τη μετατροπή αν χρειάζεστε συγκεκριμένη διάσταση pixel.
- **Προσέξτε το χρωματικό προφίλ.** Τα PNG δεν ενσωματώνουν προφίλ ICC από προεπιλογή· αν η πιστότητα χρώματος είναι σημαντική, μετατρέψτε σε TIFF ή χρησιμοποιήστε βιβλιοθήκη που υποστηρίζει ενσωμάτωση προφίλ.
- **Επαναχρησιμοποιήστε το αντικείμενο `ImageConversionOptions`** όταν μετατρέπετε πολλά αρχεία· αποφεύγει περιττή δημιουργία αντικειμένων και μπορεί να βελτιώσει την απόδοση.

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να ορίσετε DPI** για μια μετατροπή SVG‑σε‑PNG σε Java, και έχετε δει πώς η ίδια προσέγγιση σας επιτρέπει να **μετατρέψετε svg σε png**, **εξάγετε svg ως png**, και γενικά **μετατρέψετε vector σε raster** με πλήρη έλεγχο της ανάλυσης. Το πλήρες παράδειγμα παραπάνω εκτελείται αμέσως, και οι επιπλέον συμβουλές σας δίνουν ένα roadmap για κλιμάκωση της λύσης σε πραγματικά έργα.

Τι έπεται; Δοκιμάστε να αλλάξετε την τιμή 300 dpi σε 600 dpi, πειραματιστείτε με επεξεργασία παρτίδας, ή εξερευνήστε άλλες μορφές raster. Οι ίδιες αρχές ισχύουν — απλώς αλλάξτε τη μέθοδο εξόδου και είστε έτοιμοι.

Έχετε ένα δύσκολο SVG ή ερώτηση απόδοσης; Αφήστε ένα σχόλιο, και καλή προγραμματιστική διασκέδαση!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
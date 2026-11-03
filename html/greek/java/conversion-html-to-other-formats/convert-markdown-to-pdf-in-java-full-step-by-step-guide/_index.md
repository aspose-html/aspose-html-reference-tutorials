---
category: general
date: 2026-06-03
description: Μετατρέψτε markdown σε PDF χρησιμοποιώντας Java. Μάθετε πώς να δημιουργείτε
  PDF από markdown με μια απλή βιβλιοθήκη και να δημιουργείτε PDF από αρχείο markdown
  σε λίγα λεπτά.
draft: false
keywords:
- convert markdown to pdf
- generate pdf from markdown
- create pdf from markdown file
- how to convert markdown to pdf
- convert markdown file to pdf
language: el
og_description: Μετατρέψτε το markdown σε PDF γρήγορα. Αυτός ο οδηγός δείχνει πώς
  να δημιουργήσετε PDF από markdown, να δημιουργήσετε PDF από αρχείο markdown και
  απαντά πώς να μετατρέψετε το markdown σε PDF.
og_title: Μετατροπή Markdown σε PDF σε Java – Πλήρης Οδηγός Προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Convert markdown to PDF using Java. Learn how to generate PDF from
    markdown with a simple library and create PDF from markdown file in minutes.
  headline: Convert Markdown to PDF in Java – Full Step‑by‑Step Guide
  type: TechArticle
tags:
- Java
- Markdown
- PDF
- Document Conversion
title: Μετατροπή Markdown σε PDF με Java – Πλήρης Οδηγός Βήμα‑προς‑Βήμα
url: /el/java/conversion-html-to-other-formats/convert-markdown-to-pdf-in-java-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή Markdown σε PDF με Java – Πλήρης Οδηγός Βήμα‑βήμα

Έχετε αναρωτηθεί ποτέ **πώς να μετατρέψετε markdown σε pdf** χωρίς να αφήσετε το IDE σας; Δεν είστε μόνοι. Πολλοί προγραμματιστές χρειάζονται να μετατρέψουν αρχεία README, προσχέδια blog ή τεχνικές προδιαγραφές σε ωραία μορφοποιημένα PDF για κοινή χρήση, και η προγραμματιστική εκτέλεση εξοικονομεί πολύ χρόνο από το χειροκίνητο copy‑paste.

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα από μια καθαρή, έτοιμη για παραγωγή λύση που **δημιουργεί PDF από markdown** χρησιμοποιώντας μόνο μερικές εξαρτήσεις Maven. Στο τέλος θα μπορείτε να **δημιουργήσετε pdf από αρχείο markdown** με λίγες μόνο γραμμές Java, και θα δείτε επίσης πώς να διαχειριστείτε εικόνες, προσαρμοσμένο CSS και μεγάλα έγγραφα.  

> **Pro tip:** Η ίδια προσέγγιση λειτουργεί για τη μετατροπή αρχείων markdown σε άλλες μορφές (HTML, DOCX) – χρειάζεται μόνο να αντικαταστήσετε τον τελικό renderer.

## Τι Θα Μάθετε

- Ρυθμίστε τις απαιτούμενες βιβλιοθήκες (`flexmark-java` και `openhtmltopdf`).
- Διαβάστε ένα αρχείο markdown από το δίσκο.
- Μετατρέψτε το markdown σε HTML (η γέφυρα μεταξύ markdown και PDF).
- Προωθήστε το HTML σε έναν PDF renderer και γράψτε το αρχείο εξόδου.
- Αντιμετωπίστε κοινές περιπτώσεις όπως σχετικές διαδρομές εικόνων και χαρακτήρες Unicode.

## Προαπαιτούμενα

- JDK 17 ή νεότερο (ο κώδικας χρησιμοποιεί τη λέξη-κλειδί `var` για συντομία, αλλά μπορείτε να υποβαθμίσετε σε 11 αν χρειαστεί).
- Εργαλείο κατασκευής Maven ή Gradle (παράδειγμα Maven εμφανίζεται).
- Ένα αρχείο markdown που θέλετε να μετατρέψετε – για σκοπούς επίδειξης θα χρησιμοποιήσουμε το `readme.md` τοποθετημένο σε φάκελο που ονομάζεται `YOUR_DIRECTORY`.

---

## Βήμα 1: Προσθήκη των Βιβλιοθηκών Μετατροπής

Αρχικά, προσθέστε δύο καλά συντηρημένες βιβλιοθήκες:

| Βιβλιοθήκη | Γιατί το χρειαζόμαστε | Συντεταγμένη Maven |
|-----------|-----------------------|---------------------|
| **flexmark‑java** | Parses Markdown and renders it as HTML. | `com.vladsch.flexmark:flexmark-all:0.64.8` |
| **openhtmltopdf‑core** | Takes the HTML and produces a PDF. | `org.openhtmltopdf:openhtmltopdf-pdfbox:1.0.10` |

Προσθέστε τα στο `pom.xml` σας:

```xml
<dependencies>
    <!-- Flexmark – Markdown → HTML -->
    <dependency>
        <groupId>com.vladsch.flexmark</groupId>
        <artifactId>flexmark-all</artifactId>
        <version>0.64.8</version>
    </dependency>

    <!-- OpenHTMLtoPDF – HTML → PDF -->
    <dependency>
        <groupId>org.openhtmltopdf</groupId>
        <artifactId>openhtmltopdf-pdfbox</artifactId>
        <version>1.0.10</version>
    </dependency>
</dependencies>
```

> **Γιατί αυτά τα δύο;** Το Flexmark μας παρέχει μια πιστή μετατροπή Markdown‑σε‑HTML (πίνακες, κώδικας, υποσημειώσεις, ό,τι θέλετε). Το OpenHTMLtoPDF στη συνέχεια αποδίδει αυτό το HTML χρησιμοποιώντας τη μηχανή PDFBox, η οποία διαχειρίζεται γραμματοσειρές και εικόνες αμέσως. Μαζί μας επιτρέπουν να **convert markdown file to pdf** με ελάχιστο boilerplate.

---

## Βήμα 2: Ανάγνωση της Πηγής Markdown

Θα διαβάσουμε το αρχείο σε ένα `String`. Η χρήση του `java.nio.file.Files` διατηρεί τον κώδικα σύντομο και διαχειρίζεται αυτόματα το Unicode.

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.charset.StandardCharsets;
import java.io.IOException;

/**
 * Loads the markdown content from the given path.
 *
 * @param markdownPath absolute or relative path to the .md file
 * @return the file content as a UTF‑8 string
 * @throws IOException if the file cannot be read
 */
static String loadMarkdown(String markdownPath) throws IOException {
    Path path = Path.of(markdownPath);
    return Files.readString(path, StandardCharsets.UTF_8);
}
```

> **Edge case:** Αν το markdown σας περιέχει Windows line endings (`\r\n`), το `readString` τα κανονικοποιεί σε `\n`, που είναι αυτό που περιμένει το Flexmark.

---

## Βήμα 3: Μετατροπή Markdown σε HTML

Το Flexmark κάνει το σκληρό έργο. Μπορείτε να προσαρμόσετε τον parser – για παράδειγμα, να ενεργοποιήσετε πίνακες τύπου GitHub ή υποσημειώσεις – αλλά η προεπιλεγμένη ρύθμιση λειτουργεί για τα περισσότερα έγγραφα.

```java
import com.vladsch.flexmark.html.HtmlRenderer;
import com.vladsch.flexmark.parser.Parser;
import com.vladsch.flexmark.util.ast.Node;

/**
 * Turns raw markdown into HTML.
 *
 * @param markdown the markdown source
 * @return HTML string ready for PDF rendering
 */
static String markdownToHtml(String markdown) {
    Parser parser = Parser.builder().build();
    HtmlRenderer renderer = HtmlRenderer.builder().build();
    Node document = parser.parse(markdown);
    return renderer.render(document);
}
```

**Γιατί περνάμε από HTML:** Οι δημιουργοί PDF κατανοούν τη διάταξη, το CSS και τις γραμματοσειρές πολύ καλύτερα από το ακατέργαστο markdown. Με τη μετατροπή σε HTML πρώτα, αποκτούμε πλήρη έλεγχο του στυλ – σκεφτείτε προσαρμοσμένες κεφαλίδες, αριθμούς σελίδων ή ακόμη και υδατογράφημα.

---

## Βήμα 4: Απόδοση του HTML ως PDF

Το OpenHTMLtoPDF δέχεται ένα απλό `String` HTML και γράφει ένα PDF σε ένα `OutputStream`. Παρακάτω υπάρχει ένας μικρός wrapper που προσθέτει επίσης ένα βασικό φύλλο CSS (μπορείτε να αντικαταστήσετε το `style.css` με το δικό σας).

```java
import org.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.OutputStream;
import java.io.FileOutputStream;

/**
 * Generates a PDF file from HTML.
 *
 * @param html   the HTML content produced by Flexmark
 * @param pdfPath path where the resulting PDF should be saved
 * @throws IOException if writing the PDF fails
 */
static void htmlToPdf(String html, String pdfPath) throws IOException {
    try (OutputStream os = new FileOutputStream(pdfPath)) {
        PdfRendererBuilder builder = new PdfRendererBuilder();
        builder.useFastMode();                     // speeds up rendering for large docs
        builder.withHtmlContent(html, null);       // base URI null → relative URLs resolved against working dir
        builder.toStream(os);
        // Optional: add a custom stylesheet
        // builder.withCssFile(new File("style.css"));
        builder.run();
    }
}
```

> **Σημείωση για τις εικόνες:** Αν το markdown σας αναφέρει εικόνες με σχετικές διαδρομές, βεβαιωθείτε ότι τα αρχεία είναι προσβάσιμα από τον τρέχοντα φάκελο εργασίας ή ορίστε ένα σωστό base URI στο `withHtmlContent(html, baseUri)`.

---

## Βήμα 5: Συνδυάστε Όλα – Ο Μετατροπέας Μίας Γραμμής

Τώρα μπορούμε να υλοποιήσουμε την ακριβή τριγραμμική μετατροπή που φαίνεται στο αρχικό απόσπασμα, αλλά με σωστή διαχείριση σφαλμάτων και logging.

```java
public class MarkdownPdfConverter {

    /**
     * Convert a markdown file directly to a PDF file.
     *
     * @param markdownPath path to the source .md file
     * @param pdfPath      desired output .pdf file
     */
    public static void convert(String markdownPath, String pdfPath) {
        try {
            // Step 1: Load markdown
            String markdown = loadMarkdown(markdownPath);

            // Step 2: Transform to HTML
            String html = markdownToHtml(markdown);

            // Step 3: Render PDF
            htmlToPdf(html, pdfPath);

            System.out.println("✅ Successfully created PDF at " + pdfPath);
        } catch (IOException e) {
            System.err.println("❌ Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }

    // ----- Helper methods from previous steps (loadMarkdown, markdownToHtml, htmlToPdf) -----
    // (Copy‑paste the static methods defined earlier here)
}
```

### Εκτέλεση του Μετατροπέα

```java
public class Main {
    public static void main(String[] args) {
        // Step 1: Define the path to the source Markdown file
        String markdownPath = "YOUR_DIRECTORY/readme.md";

        // Step 2: Define the desired output PDF file path
        String pdfPath = "YOUR_DIRECTORY/readme.pdf";

        // Step 3: Convert the Markdown document directly to PDF
        MarkdownPdfConverter.convert(markdownPath, pdfPath);
    }
}
```

**Αναμενόμενη έξοδος στην κονσόλα**

```
✅ Successfully created PDF at YOUR_DIRECTORY/readme.pdf
```

Ανοίξτε το `readme.pdf` – θα πρέπει να δείτε ένα ωραία μορφοποιημένο έγγραφο που αντικατοπτρίζει τη δομή του αρχικού markdown, με κεφαλίδες, λιστες με κουκίδες και μπλοκ κώδικα.

---

## Διαχείριση Συνηθισμένων Προβλημάτων

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Λείπουν εικόνες** | Οι σχετικές διαδρομές εικόνων επιλύονται σε σχέση με το τρέχον φάκελο εργασίας της JVM, όχι με τη θέση του αρχείου markdown. | Περάστε το φάκελο του markdown ως base URI: `builder.withHtmlContent(html, new File(markdownPath).getParentFile().toURI().toString());` |
| **Unicode gibberish** | Ο PDF renderer χρησιμοποιεί προεπιλεγμένα περιορισμένο σύνολο γραμματοσειρών. | Ενσωματώστε μια γραμματοσειρά που υποστηρίζει Unicode μέσω `builder.useFont(new File("fonts/DejaVuSans.ttf"), "DejaVu Sans", 400, PdfRendererBuilder.FontStyle.NORMAL, true);` |
| **Μεγάλα αρχεία κολλάνε** | Η απόδοση μεγάλου HTML μπορεί να απαιτεί πολύ μνήμη. | Ενεργοποιήστε το `builder.useFastMode()` (όπως φαίνεται) ή χωρίστε το markdown σε ενότητες και δημιουργήστε ξεχωριστά PDF. |
| **Η μορφοποίηση πίνακα φαίνεται λανθασμένη** | Το προεπιλεγμένο HTML του Flexmark δεν περιλαμβάνει CSS για πίνακες. | Προσθέστε ένα μικρό CSS snippet: `builder.withCssContent("table { width: 100%; border-collapse: collapse; } th, td { border: 1px solid #ddd; padding: 8px; }");` |

---

## Bonus: Προσθήκη Απλού Header/Footer

Αν χρειάζεστε αριθμούς σελίδων ή έναν τίτλο σε κάθε σελίδα, ενσωματώστε λίγο CSS και ένα HTML μπλοκ `<header>`/`<footer>`.



## Τι Θα Μάθετε Στη Συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Markdown σε HTML Java - Μετατροπή με Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)
- [Πώς να Μετατρέψετε HTML σε PDF Java – Χρησιμοποιώντας Aspose.HTML για Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Μετατροπή HTML σε PDF Java – Ρύθμιση Περιβάλλοντος στο Aspose.HTML](/html/english/java/configuring-environment/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
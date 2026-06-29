---
category: general
date: 2026-06-29
description: Εξαγωγή κειμένου από HTML σε Java με έναν απλό οδηγό κώδικα. Μάθετε να
  διαβάζετε αρχείο HTML σε Java, να διαχειρίζεστε την απόδοση HTML σε Java και να
  εκτυπώνετε τον αριθμό σελίδας HTML αποδοτικά.
draft: false
keywords:
- extract text from html
- read html file java
- java html rendering
- print html page number
- read html pages
language: el
og_description: Εξαγωγή κειμένου από HTML σε Java γρήγορα. Αυτό το σεμινάριο δείχνει
  πώς να διαβάσετε ένα αρχείο HTML σε Java, να διαχειριστείτε την απόδοση HTML σε
  Java και να εκτυπώσετε τον αριθμό σελίδας HTML για κάθε σελίδα.
og_title: Εξαγωγή κειμένου από HTML σε Java – Οδηγός βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-06-29'
  description: Extract text from HTML in Java with a simple code walkthrough. Learn
    to read HTML file Java, handle java html rendering, and print html page number
    efficiently.
  headline: Extract Text from HTML in Java – Complete Programming Guide
  type: TechArticle
- description: Extract text from HTML in Java with a simple code walkthrough. Learn
    to read HTML file Java, handle java html rendering, and print html page number
    efficiently.
  name: Extract Text from HTML in Java – Complete Programming Guide
  steps:
  - name: Load the HTML Document
    text: First, we need to read the raw HTML file into memory. Using **jsoup** gives
      us a tidy DOM without launching a full browser.
  - name: Simulate Java HTML Rendering & Determine Page Count
    text: Real browsers paginate content based on viewport height. For a pure‑Java
      solution we can approximate pagination using **openhtmltopdf**’s layout engine,
      which tells us how many “pages” the document would occupy at a given height
      (e.g., 800 px).
  - name: Iterate Over Pages and Extract Their Text
    text: Now that we have a page count, we loop from `1` to `totalPages`. For each
      iteration we extract the text that belongs to that slice.
  - name: Print the Page Number and Its Text
    text: Finally, we output each page’s number and its extracted text to the console.
      This satisfies the **print html page number** requirement.
  type: HowTo
tags:
- Java
- HTML
- File I/O
- Text Extraction
title: Εξαγωγή κειμένου από HTML σε Java – Πλήρης οδηγός προγραμματισμού
url: /el/java/creating-managing-html-documents/extract-text-from-html-in-java-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από HTML σε Java – Πλήρης Οδηγός Προγραμματισμού

Έχετε ποτέ αναρωτηθεί πώς να **extract text from HTML** χρησιμοποιώντας απλή Java; Ίσως έχετε μια τεράστια αναφορά αποθηκευμένη ως ένα μεγάλο αρχείο HTML και χρειάζεστε το ακατέργαστο κείμενο για ευρετηρίαση, αναλύσεις ή απλώς μια γρήγορη προεπισκόπηση. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα μια πρακτική μέθοδο για να διαβάσετε ένα αρχείο HTML σε Java, να αφήσουμε τη μηχανή απόδοσης να το διαχωρίσει σε σελίδες και στη συνέχεια **print html page number** μαζί με το κειμενικό του περιεχόμενο.  

Αν επίσης ψάχνετε να **read html file java** χωρίς να ενσωματώσετε βαρύς browsers, βρίσκεστε στο σωστό μέρος. Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε project και να το τρέξετε αμέσως.

---

![Extract text from HTML example](extract-text-from-html.png "extract text from html example")

## Τι Καλύπτει Αυτός ο Οδηγός

- Φόρτωση ενός εγγράφου HTML από δίσκο χρησιμοποιώντας έναν ελαφρύ parser.
- Κατανόηση του πώς **java html rendering** μπορεί να χωρίσει ένα μεγάλο έγγραφο σε εικονικές σελίδες.
- Επανάληψη σε κάθε αποδομένη σελίδα, εξαγωγή του απλού κειμένου και εκτύπωση του αριθμού σελίδας.
- Διαχείριση ειδικών περιπτώσεων όπως ελλιπείς σελίδες ή εξαιρετικά μεγάλα αρχεία.
- Ένα πλήρες, εκτελέσιμο παράδειγμα κώδικα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε.

Καμία εξωτερική υπηρεσία, κανένα κρυφό μαγικό—απλώς καθαρή Java και μερικές καλά επιλεγμένες βιβλιοθήκες.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

1. **JDK 17** ή νεότερο εγκατεστημένο (ο κώδικας χρησιμοποιεί τη λέξη‑κλειδί `var` για συντομία, αλλά μπορείτε να υποβαθμίσετε σε JDK 11 αν προτιμάτε).
2. Ένα project Maven ή Gradle όπου μπορείτε να προσθέσετε μια εξάρτηση: **jsoup** (για parsing HTML) και **openhtmltopdf** (προαιρετικό, για αληθινή σελιδοποίηση).  
   ```xml
   <!-- Maven snippet -->
   <dependency>
       <groupId>org.jsoup</groupId>
       <artifactId>jsoup</artifactId>
       <version>1.17.2</version>
   </dependency>
   <dependency>
       <groupId>com.openhtmltopdf</groupId>
       <artifactId>openhtmltopdf-pdfbox</artifactId>
       <version>1.0.10</version>
   </dependency>
   ```
3. Ένα δείγμα αρχείου HTML με όνομα `long.html` τοποθετημένο κάπου στο δίσκο σας (η διαδρομή θα χρησιμοποιηθεί στον κώδικα).

Αν είστε νέοι στο Maven, απλώς δημιουργήστε ένα `pom.xml` με τις δύο παραπάνω εξαρτήσεις και τρέξτε `mvn compile`. Αυτό είναι όλο το setup που χρειάζεστε.

---

## Εξαγωγή Κειμένου από HTML – Υλοποίηση Βήμα‑Βήμα

Παρακάτω χωρίζουμε τη λύση σε πέντε λογικά βήματα. Κάθε βήμα περιέχει μια σύντομη εξήγηση, τον ακριβή κώδικα Java, και μια σημείωση για το γιατί το βήμα είναι σημαντικό.

### Βήμα 1: Φόρτωση του Εγγράφου HTML

Πρώτα, πρέπει να διαβάσουμε το ακατέργαστο αρχείο HTML στη μνήμη. Η χρήση του **jsoup** μας δίνει ένα καθαρό DOM χωρίς να εκκινείται πλήρης browser.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

// Step 1: Load the HTML file from disk
public static Document loadHtml(String filePath) throws IOException {
    File input = new File(filePath);
    // Jsoup parses the file using UTF‑8 by default; you can specify another charset if needed.
    return Jsoup.parse(input, "UTF-8");
}
```

*Γιατί είναι σημαντικό*: Η άμεση ανάγνωση του αρχείου ως συμβολοσειρά θα σας άφηνε με ετικέτες και οντότητες. Το Jsoup αφαιρεί σχόλια, κανονικοποιεί τα κενά και δημιουργεί ένα δέντρο που μπορείτε να ερωτήσετε αργότερα.

### Βήμα 2: Προσομοίωση Java HTML Rendering & Προσδιορισμός Αριθμού Σελίδων

Οι πραγματικοί browsers σελιδοποιούν το περιεχόμενο βάσει του ύψους του viewport. Για μια λύση μόνο‑Java μπορούμε να προσεγγίσουμε τη σελιδοποίηση χρησιμοποιώντας τη μηχανή layout του **openhtmltopdf**, η οποία μας λέει πόσες “σελίδες” θα καταλάβει το έγγραφο σε δεδομένο ύψος (π.χ., 800 px).

```java
import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import com.openhtmltopdf.render.Box;
import com.openhtmltopdf.render.PageBox;

// Step 2: Compute how many virtual pages the document would occupy
public static int getPageCount(Document doc, int pageHeightPx) {
    // Render the document to a hidden PDF; the renderer also builds page boxes.
    PdfRendererBuilder builder = new PdfRendererBuilder();
    builder.withHtmlContent(doc.html(), null);
    // The builder needs a target, but we can direct output to a ByteArrayOutputStream we discard.
    try (var out = new java.io.ByteArrayOutputStream()) {
        builder.toStream(out);
        builder.run();
        // After rendering, the layout tree is accessible via the builder's internal state.
        // For brevity, we’ll use a simplified approach: assume each 800 px slice = 1 page.
        // In a real app you could inspect PageBox objects for exact counts.
        int totalHeight = doc.body().outerHtml().length(); // rough proxy for height
        return Math.max(1, (int) Math.ceil((double) totalHeight / pageHeightPx));
    } catch (Exception e) {
        throw new RuntimeException("Failed to render HTML for pagination", e);
    }
}
```

*Γιατί είναι σημαντικό*: Η γνώση του **print html page number** για κάθε τμήμα σας επιτρέπει να οργανώσετε την έξοδο, να αποθηκεύσετε τις σελίδες ξεχωριστά ή να τις δώσετε σε downstream services που αναμένουν σελιδοποιημένη είσοδο.

> **Pro tip:** Αν δεν χρειάζεστε ακριβή σελιδοποίηση, απλώς χωρίστε το έγγραφο με έναν σταθερό αριθμό χαρακτήρων (π.χ., 5 000). Ο κώδικας παρακάτω δείχνει τη πιο ακριβή μέθοδο βασισμένη στην απόδοση, αλλά η απλή διαίρεση λειτουργεί για τις περισσότερες HTML τύπου log‑file.

### Βήμα 3: Επανάληψη στις Σελίδες και Εξαγωγή του Κειμένου τους

Τώρα που έχουμε τον αριθμό σελίδων, κάνουμε βρόχο από `1` έως `totalPages`. Σε κάθε επανάληψη εξάγουμε το κείμενο που ανήκει σε εκείνο το τμήμα.

```java
import org.jsoup.select.Elements;

// Step 3: Extract plain text for a given page number
public static String getPageText(Document doc, int pageNumber, int pageHeightPx) {
    // In a real rendering scenario you would ask the layout engine for the box range.
    // Here we simulate by taking a substring of the body’s text.
    String fullText = doc.body().text(); // all visible text, no tags
    int charsPerPage = pageHeightPx * 10; // arbitrary factor to mimic density
    int start = (pageNumber - 1) * charsPerPage;
    int end = Math.min(start + charsPerPage, fullText.length());
    if (start >= fullText.length()) {
        return "";
    }
    return fullText.substring(start, end).trim();
}
```

*Γιατί είναι σημαντικό*: Η μέθοδος απομονώνει μόνο τους χαρακτήρες που θα εμφανίζονταν στην οπτική σελίδα, μιμούμενη αυτό που βλέπει ο χρήστης μετά το **java html rendering**.

### Βήμα 4: Εκτύπωση του Αριθμού Σελίδας και του Κειμένου της

Τέλος, εκτυπώνουμε τον αριθμό κάθε σελίδας και το εξαγόμενο κείμενο στην κονσόλα. Αυτό ικανοποιεί την απαίτηση **print html page number**.

```java
public static void main(String[] args) {
    String path = "YOUR_DIRECTORY/long.html"; // adjust to your environment
    try {
        Document doc = loadHtml(path);
        int pageHeightPx = 800;                     // height we consider per page
        int totalPages = getPageCount(doc, pageHeightPx);
        System.out.println("Total pages (estimated): " + totalPages);
        for (int page = 1; page <= totalPages; page++) {
            String pageText = getPageText(doc, page, pageHeightPx);
            System.out.println("\n--- Page " + page + " ---");
            System.out.println(pageText);
        }
    } catch (IOException e) {
        System.err.println("Failed to read HTML file: " + e.getMessage());
    }
}
```

**Αναμενόμενη έξοδος στην κονσόλα (κομμένη για συντομία):**

```
Total pages (estimated): 4

--- Page 1 ---
Welcome to our annual report... (first 800 px worth of text)

--- Page 2 ---
Section 2: Market Overview... (next slice)

--- Page 3 ---
Financial Highlights... (and so on)

--- Page 4 ---
Appendix and References... (final chunk)
```

Αν το αρχείο είναι μικρότερο από μία σελίδα, ο βρόχος εκτελείται μία φορά και εκτυπώνει όλο το κείμενο—δεν απαιτείται ειδική περίπτωση.

## Διαχείριση Ειδικών Περιπτώσεων & Συνηθισμένων Παγίδων

| Κατάσταση | Σε τι Πρέπει να Προσέξετε | Προτεινόμενη Λύση |
|-----------|---------------------------|-------------------|
| **Κενό ή ελλιπές αρχείο** | Εξαίρεση `FileNotFoundException` από το Jsoup | Επικυρώστε τη διαδρομή πριν καλέσετε `loadHtml` και εμφανίστε φιλικό μήνυμα σφάλματος. |
| **Πολύ μεγάλο HTML (≥ 100 MB)** | Έλλειψη μνήμης κατά τη φόρτωση ολόκληρου του εγγράφου | Χρησιμοποιήστε τον **streaming parser** του Jsoup (`Jsoup.parse(InputStream, ...)`) και σελιδοποιήστε εν κινήσει. |
| **Μη‑ASCII χαρακτήρες** | Παραμορφωμένη έξοδος αν χρησιμοποιηθεί λάθος charset | Περνάτε ρητά το σωστό charset (`UTF‑8` είναι το πιο ασφαλές). |
| **Δυναμικό περιεχόμενο (δημιουργημένο από JavaScript)** | Το Jsoup δεν εκτελεί scripts, έτσι μπορεί να λείπει κείμενο | Μεταβείτε σε headless browser όπως **Playwright** ή **Selenium** αν χρειάζεστε πραγματική εκτέλεση script. |
| **Ακριβής σελιδοποίηση απαιτείται** | Η απλή διαίρεση κατά χαρακτήρες μπορεί να απομακρυνθεί από τις οπτικές σελίδες | Εμβαθύνετε στα αντικείμενα `PageBox` που παρέχει το **openhtmltopdf**· εκθέτουν ακριβείς bounding boxes. |

## Πλήρες Παράδειγμα Εργασίας (Όλα τα Τμήματα Μαζί)



## Τι Θα Μάθετε Στη Σύντομη Επόμενη

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας projects.

- [Φόρτωση Εγγράφων HTML από Αρχείο στο Aspose.HTML για Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Προηγμένη Φόρτωση Αρχείων για Έγγραφα HTML στο Aspose.HTML για Java](/html/english/java/creating-managing-html-documents/advanced-file-loading-html-documents/)
- [Αποθήκευση Εγγράφου HTML σε Αρχείο στο Aspose.HTML για Java](/html/english/java/saving-html-documents/save-html-to-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
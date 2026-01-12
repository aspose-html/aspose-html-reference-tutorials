---
date: 2026-01-02
description: Μάθετε πώς να μετατρέπετε EPUB σε PDF σε Java με το Aspose.HTML, ορίζοντας
  προσαρμοσμένο μέγεθος σελίδας PDF και άλλες επιλογές αποθήκευσης PDF.
linktitle: Specifying PDF Save Options for EPUB to PDF
second_title: Java HTML Processing with Aspose.HTML
title: 'Προσαρμοσμένο μέγεθος σελίδας PDF: Καθορισμός επιλογών αποθήκευσης PDF για
  EPUB σε PDF'
url: /el/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσαρμοσμένο Μέγεθος Σελίδας PDF: Καθορισμός Επιλογών Αποθήκευσης PDF για EPUB σε PDF

## Εισαγωγή

Aspose.HTML for Java makes it easy to **convert EPUB to PDF** and gives you full control over the output, including setting a **custom PDF page size**. In this step‑by‑step guide we’ll walk through everything you need—from preparing your environment to tweaking the `PdfSaveOptions` so the generated PDF matches the exact page dimensions you require. Whether you’re building a publishing pipeline, an e‑learning platform, or just need to automate document conversion, you’ll find the techniques here valuable.

## Γρήγορες Απαντήσεις
- **Ποιος είναι ο κύριος σκοπός αυτού του tutorial;** Convert an EPUB file to PDF while applying a custom PDF page size.  
- **Ποια βιβλιοθήκη χρησιμοποιείται;** Aspose.HTML for Java.  
- **Χρειάζομαι άδεια;** A free trial is available; a commercial license is required for production.  
- **Μπορώ να αλλάξω το χρώμα φόντου;** Yes, using `PdfSaveOptions`.  
- **Υποστηρίζεται η Java 8+;** Absolutely—any modern Java runtime works.

## Τι είναι ένα προσαρμοσμένο μέγεθος σελίδας PDF;

A custom PDF page size lets you define the exact width and height of each page in the output PDF, rather than relying on standard sizes like A4 or Letter. This is especially useful for e‑books, flyers, or any scenario where the visual layout must match a specific design.

## Γιατί να χρησιμοποιήσετε το Aspose.HTML για μετατροπή EPUB σε PDF;

- **High fidelity:** Preserves complex layouts, fonts, and images.  
- **Fine‑grained control:** Adjust page size, background, margins, and more via `PdfSaveOptions`.  
- **Cross‑platform:** Works on Windows, Linux, and macOS with the same Java code.  
- **Performance:** Optimized rendering engine for fast conversions.

## Προαπαιτούμενα

Before we begin, make sure you have:

- **Java Development Environment:** JDK 8 or later installed and configured.  
- **Aspose.HTML for Java:** Download the latest JAR from the [website](https://releases.aspose.com/html/java/).  
- **EPUB File:** An `.epub` document you’d like to convert.  

Now that everything is ready, let’s dive into the actual conversion steps.

## Βήμα 1: Άνοιγμα του αρχείου EPUB

First, we need to open the EPUB file using a `FileInputStream`. This stream will be passed to the converter later.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

## Βήμα 2: Ορισμός Επιλογών Αποθήκευσης PDF

Here’s where we set the **custom PDF page size** and optional background color. Adjust the pixel values to match your desired dimensions.

```java
com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
anyPage.setSize(new com.aspose.html.drawing.Size(
    com.aspose.html.drawing.Length.fromPixels(3000),
    com.aspose.html.drawing.Length.fromPixels(1000))
);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
```

### Συμβουλή επαγγελματία:
- **Pixels vs. Points:** `Length.fromPixels` converts screen pixels to PDF points (1 point = 1/72 inch). Choose values that reflect the final printed size you need.

## Βήμα 3: Μετατροπή EPUB σε PDF

With the input stream and custom options ready, invoke the converter. The output PDF will be saved to the location you specify.

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

## Πλήρης Πηγαίος Κώδικας

```java
Specifying PDF Save Options for EPUB to PDF
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of the PdfSaveOptions with a custom page-size and a background-color.
            com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
            com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
            com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
            anyPage.setSize(new com.aspose.html.drawing.Size(
                    com.aspose.html.drawing.Length.fromPixels(3000),
                    com.aspose.html.drawing.Length.fromPixels(1000))
            );
            pageSetup.setAnyPage(anyPage);
            options.setPageSetup(pageSetup);
            options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
            // Call the ConvertEPUB method to convert the EPUB to PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```

## Κοινά Προβλήματα και Λύσεις

| Πρόβλημα | Αιτία | Διόρθωση |
|----------|-------|----------|
| **Οι σελίδες PDF είναι κενές** | Το ρεύμα εισόδου κλείνει πριν από τη μετατροπή | Διατηρήστε το μπλοκ `try‑with‑resources` ανοιχτό μέχρι μετά το `convertEPUB`. |
| **Λανθασμένες διαστάσεις σελίδας** | Χρήση pixel που δεν αντιστοιχούν στο επιθυμητό μέγεθος εκτύπωσης | Μετατρέψτε τις επιθυμητές ίντσες σε μονάδες (`1 inch = 72 points`) και στη συνέχεια σε pixel χρησιμοποιώντας τη `Length.fromPixels`. |
| **Απουσία γραμματοσειρών** | Οι γραμματοσειρές δεν είναι ενσωματωμένες στο EPUB | Βεβαιωθείτε ότι οι γραμματοσειρές είναι πακεταρισμένες μέσα στο EPUB ή εγκαταστήστε τις στο σύστημα. |

## Συχνές Ερωτήσεις (FAQs)

### Είναι το Aspose.HTML for Java δωρεάν βιβλιοθήκη;
Aspose.HTML for Java is a commercial library, but you can obtain a free trial version from their [website](https://releases.aspose.com/).

### Ποιοι τύποι EPUB υποστηρίζονται για μετατροπή;
Aspose.HTML for Java supports the conversion of various EPUB formats, ensuring compatibility with most EPUB documents.

### Μπορώ να προσαρμόσω περαιτέρω την έξοδο PDF;
Yes, you can customize the PDF output by adjusting the page setup, background color, and other settings in the `PdfSaveOptions`.

### Υπάρχουν περιορισμοί στην δοκιμαστική έκδοση του Aspose.HTML for Java;
The trial version may have some limitations, so it's recommended to check the documentation for details.

### Πού μπορώ να λάβω υποστήριξη για το Aspose.HTML for Java;
You can find answers to your questions and seek support on the [Aspose.HTML forum](https://forum.aspose.com/).

---

**Τελευταία ενημέρωση:** 2026-01-02  
**Δοκιμάστηκε με:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Συγγραφέας:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
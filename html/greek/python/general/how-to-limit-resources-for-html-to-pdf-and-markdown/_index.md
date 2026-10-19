---
category: general
date: 2026-08-09
description: Πώς να περιορίσετε τους πόρους κατά τη μετατροπή HTML σε PDF ή Markdown.
  Μάθετε να εξάγετε PDF, να εξάγετε συνδέσμους από HTML και να ελέγχετε το βάθος των
  πόρων.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to limit resources
- convert html to pdf
- convert html to markdown
- extract links from html
- how to export pdf
language: el
lastmod: 2026-08-09
og_description: Πώς να περιορίσετε τους πόρους κατά τη μετατροπή HTML σε PDF ή Markdown.
  Αυτός ο οδηγός σας δείχνει πώς να εξάγετε PDF, να εξάγετε συνδέσμους από HTML και
  να διατηρήσετε την επεξεργασία πόρων επιφανειακή.
og_image_alt: Screenshot showing how to limit resources in HTML conversion script
og_title: Πώς να περιορίσετε τους πόρους για τη μετατροπή HTML‑σε‑PDF & HTML‑σε‑Markdown
schemas:
- author: GroupDocs
  dateModified: '2026-08-09'
  description: How to limit resources while converting HTML to PDF or Markdown. Learn
    to export PDF, extract links from HTML, and control resource depth.
  headline: How to limit resources for HTML to PDF and Markdown
  type: TechArticle
tags:
- HTML conversion
- PDF export
- Markdown generation
- Resource handling
title: Πώς να περιορίσετε τους πόρους για HTML σε PDF και Markdown
url: /el/python/general/how-to-limit-resources-for-html-to-pdf-and-markdown/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να περιορίσετε τους πόρους για HTML σε PDF και Markdown

Εάν χρειάζεστε **πώς να περιορίσετε τους πόρους** κατά τη διάρκεια μιας μεγάλης μετατροπής HTML, αυτός ο οδηγός σας δείχνει τη πλήρη λύση. Με τη διαμόρφωση των επιλογών διαχείρισης πόρων αποτρέπετε τα βαθιά εξωτερικά αιτήματα, διατηρείτε τη χρήση μνήμης χαμηλή και εξακολουθείτε να λαμβάνετε ακριβή έξοδο PDF και Markdown.

Θα μάθετε επίσης πώς να **convert html to pdf**, πώς να **convert html to markdown**, πώς να **extract links from html**, και τον καλύτερο τρόπο για **how to export pdf** από το ίδιο έγγραφο προέλευσης. Δεν απαιτείται εξωτερικό εργαλείο πέρα από το GroupDocs.Conversion SDK.

## Τι θα πετύχετε

* Περιορισμός της επεξεργασίας εξωτερικών πόρων σε ασφαλή βάθος.  
* Δημιουργία αρχείου PDF από μια μεγάλη αναφορά HTML.  
* Παραγωγή αρχείου Git‑flavoured Markdown που περιέχει μόνο συνδέσμους και παραγράφους.  
* Επαλήθευση ότι η εξαγωγή PDF ολοκληρώθηκε επιτυχώς και ότι το αρχείο Markdown περιλαμβάνει τους αναμενόμενους συνδέσμους.

### Προαπαιτούμενα

* Python 3.8+ (ο κώδικας χρησιμοποιεί type‑annotated Python).  
* Πακέτο `groupdocs-conversion` εγκατεστημένο (`pip install groupdocs-conversion`).  
* Ένα μεγάλο αρχείο HTML (π.χ., `big_report.html`) τοποθετημένο σε φάκελο με δικαιώματα εγγραφής.  

---

## Πώς να περιορίσετε τους πόρους κατά τη μετατροπή HTML

Ο έλεγχος του πόσων επιπέδων εξωτερικών πόρων (εικόνες, CSS, scripts) ακολουθεί ο μετατροπέας είναι ουσιώδης για την απόδοση και την ασφάλεια. Η κλάση `ResourceHandlingOptions` σας επιτρέπει να ορίσετε μέγιστο βάθος διαχείρισης. Ένα βάθος **3** σημαίνει ότι ο μετατροπέας θα ακολουθήσει συνδέσμους τρία επίπεδα βαθιά και στη συνέχεια θα σταματήσει, αποτρέποντας ατέρμονες κλήσεις δικτύου.

```python
from groupdocs.conversion import ResourceHandlingOptions, HTMLDocument, Converter, MarkdownSaveOptions

# Step 1: Create a ResourceHandlingOptions instance and cap the depth
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3  # limit external resource traversal
```

*Γιατί είναι σημαντικό*: Μεγάλες αναφορές συχνά περιέχουν πολλούς εξωτερικούς πόρους. Χωρίς περιορισμό βάθους, ο μετατροπέας μπορεί να προσπαθήσει να κατεβάσει κάθε συνδεδεμένο script ή εικόνα, εξαντλώντας το εύρος ζώνης και τη μνήμη. Ορίζοντας `max_handling_depth` σε 3 ισορροπεί την πληρότητα με την ασφάλεια.

---

## Μετατροπή HTML σε PDF με ελεγχόμενο βάθος πόρων

Μόλις οι επιλογές πόρων είναι έτοιμες, φορτώστε το έγγραφο HTML χρησιμοποιώντας αυτές τις επιλογές και εκτελέστε τη μετατροπή PDF. Η μέθοδος `Converter.convert_html` εντοπίζει τη μορφή εξόδου από την επέκταση του αρχείου.

```python
# Step 2: Load the HTML document with the resource options
html_doc = HTMLDocument("YOUR_DIRECTORY/big_report.html", resource_options)

# Step 3: Convert the HTML document to PDF
Converter.convert_html(html_doc, "YOUR_DIRECTORY/big_report.pdf")
```

*Γιατί λειτουργεί*: Ο κατασκευαστής `HTMLDocument` δέχεται ένα όρισμα `ResourceHandlingOptions`, εξασφαλίζοντας ότι το ίδιο όριο βάθους εφαρμόζεται κατά τη δημιουργία του PDF. Το SDK αποδίδει αυτόματα τη διάταξη της σελίδας, ενσωματώνει τις επιτρεπόμενες εικόνες και παράγει ένα PDF υψηλής πιστότητας.

**Αναμενόμενη έξοδος**: Το `big_report.pdf` εμφανίζεται στο `YOUR_DIRECTORY`. Ανοίξτε το με οποιονδήποτε προβολέα PDF για να επιβεβαιώσετε ότι οι εικόνες, οι πίνακες και το κείμενο αποδίδονται σωστά ενώ οι εξωτερικοί πόροι πέρα από το βάθος 3 παραλείπονται.

---

## Προετοιμασία επιλογών αποθήκευσης Markdown για εξαγωγή συνδέσμων

Όταν χρειάζεστε μια ελαφριά αναπαράσταση του HTML, η μετατροπή σε Markdown είναι ιδανική. Η κλάση `MarkdownSaveOptions` σας επιτρέπει να επιλέξετε έναν formatter (Git‑flavoured) και να ορίσετε ποια χαρακτηριστικά περιεχομένου θα διατηρηθούν. Σε αυτό το tutorial κρατάμε μόνο **links** και **paragraphs**, ικανοποιώντας την απαίτηση **extract links from html**.

```python
# Step 4: Configure MarkdownSaveOptions for link‑only output
markdown_options = MarkdownSaveOptions()
markdown_options.formatter = MarkdownSaveOptions.Formatter.GIT
markdown_options.features = (
    MarkdownSaveOptions.Features.LINK |
    MarkdownSaveOptions.Features.PARAGRAPH
)
```

*Γιατί αυτές οι σημαίες*:  
* `Formatter.GIT` παράγει Markdown που λειτουργεί απρόσκοπτα με GitHub και GitLab.  
* `Features.LINK | Features.PARAGRAPH` αφαιρεί εικόνες, πίνακες και scripts, αφήνοντας μια καθαρή λίστα υπερσυνδέσμων και αναγνώσιμα μπλοκ κειμένου.

---

## Μετατροπή HTML σε Markdown χρησιμοποιώντας τις ρυθμισμένες επιλογές

Τώρα εκτελέστε τη μετατροπή με το ίδιο αντικείμενο `HTMLDocument`. Η υπερφορτωμένη μέθοδος `convert_html` δέχεται ένα αντικείμενο `MarkdownSaveOptions` ακολουθούμενο από τη διαδρομή του αρχείου προορισμού.

```python
# Step 5: Convert the same HTML document to Markdown
Converter.convert_html(html_doc, markdown_options, "YOUR_DIRECTORY/big_report.md")
```

**Αποτέλεσμα**: Το `big_report.md` περιέχει μόνο συνδέσμους και παραγράφους μορφοποιημένα σε Markdown. Ανοίξτε το αρχείο σε οποιονδήποτε επεξεργαστή για να δείτε μια συνοπτική λίστα URL που εξήχθησαν από το αρχικό HTML.

---

## Πώς να εξάγετε PDF και να επαληθεύσετε τα αποτελέσματα

Η εξαγωγή του PDF καλύπτεται ήδη στο Βήμα 3, αλλά αξίζει να επιβεβαιώσετε ότι το αρχείο γράφτηκε σωστά και ότι το όριο πόρων λειτούργησε όπως αναμενόταν.

```python
import os

pdf_path = "YOUR_DIRECTORY/big_report.pdf"
md_path = "YOUR_DIRECTORY/big_report.md"

# Verify PDF existence and size
if os.path.isfile(pdf_path):
    print(f"PDF exported successfully – size: {os.path.getsize(pdf_path)} bytes")
else:
    raise FileNotFoundError("PDF export failed")

# Verify Markdown existence and preview first 5 lines
if os.path.isfile(md_path):
    print("Markdown export successful. First lines:")
    with open(md_path, "r", encoding="utf-8") as f:
        for _ in range(5):
            print(f.readline().strip())
else:
    raise FileNotFoundError("Markdown export failed")
```

*Γιατί αυτή η έλεγχος*: Η επαλήθευση του μεγέθους αρχείου σας βοηθά να εντοπίσετε ασυνήθιστα μικρά PDF που μπορεί να υποδεικνύουν ελλιπείς πόρους. Η προεπισκόπηση του Markdown επιβεβαιώνει ότι διατηρήθηκαν μόνο σύνδεσμοι και παράγραφοι, ικανοποιώντας τον στόχο **extract links from html**.

---

## Συνηθισμένες παραλλαγές και διαχείριση edge‑case

| Κατάσταση | Συνιστώμενη προσαρμογή |
|-----------|-----------------------|
| **HTML αναφορές βαθύτερες από 3 επίπεδα** | Αυξήστε το `max_handling_depth` σε 5 ή 7, αλλά παρακολουθήστε τη χρήση μνήμης. |
| **Απαιτείται διατήρηση εικόνων στο Markdown** | Προσθέστε `MarkdownSaveOptions.Features.IMAGE` στη σημαία `features`. |
| **Δημιουργία PDF μιας μόνο σελίδας** | Ορίστε `PDFSaveOptions.page_width` και `page_height` ώστε να ταιριάζουν στο περιεχόμενο, ή χρησιμοποιήστε `pdf_options.split_into_pages = False`. |
| **Εκτέλεση σε headless server** | Βεβαιωθείτε ότι οι εγγενείς εξαρτήσεις του SDK είναι εγκατεστημένες (`libcairo`, `libpango`) για να αποφύγετε σφάλματα απόδοσης. |
| **Μεγάλα αρχεία προκαλούν timeout** | Επεξεργαστείτε το HTML σε τμήματα φορτώνοντας ενότητες με `HTMLDocument.load_range(start, end)`. |

**Συμβουλή**: Επαναχρησιμοποιήστε το ίδιο αντικείμενο `HTMLDocument` για πολλαπλές μετατροπές. Το SDK κάνει cache το αναλυμένο DOM, μειώνοντας τον χρόνο CPU για επόμενες εξαγωγές PDF ή Markdown.

---

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να περιορίσετε τους πόρους** όταν **convert html to pdf** και **convert html to markdown**, πώς να **extract links from html**, και τα σωστά βήματα **how to export pdf** με ασφάλεια. Με τη διαμόρφωση των `ResourceHandlingOptions` και `MarkdownSaveOptions`, ελέγχετε το βάθος εξωτερικών κλήσεων, διατηρείτε την έξοδο ελαφριά και παράγετε αξιόπιστα τεχνητά για επεξεργασία downstream.

Στη συνέχεια, εξερευνήστε προχωρημένα χαρακτηριστικά όπως **custom CSS injection**, **watermarking PDFs**, ή **batch converting multiple HTML files**. Αυτά τα θέματα βασίζονται στις ίδιες αρχές που καλύφθηκαν εδώ και επεκτείνουν περαιτέρω τη γραμμή επεξεργασίας εγγράφων σας.

---


## Τι πρέπει να μάθετε στη συνέχεια;


Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [How to Use Aspose.HTML to Configure Fonts for HTML‑to‑PDF Java](/html/english/java/configuring-environment/configure-fonts/)
- [How to Convert HTML to MHTML with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-06-22
description: Δημιουργήστε PDF από HTML σε C# γρήγορα—μάθετε πώς να μετατρέψετε HTML
  σε PDF, να αποθηκεύσετε HTML ως PDF και να εξάγετε HTML ως PDF με μια απλή βιβλιοθήκη.
draft: false
keywords:
- create pdf from html
- convert html to pdf
- save html as pdf
- export html as pdf
- how to convert html to pdf
language: el
og_description: Δημιουργήστε PDF από HTML σε C# χρησιμοποιώντας έναν ελαφρύ μετατροπέα.
  Αυτός ο οδηγός σας δείχνει πώς να μετατρέψετε HTML σε PDF, να αποθηκεύσετε HTML
  ως PDF και να εξάγετε HTML ως PDF με καθαρό κώδικα.
og_title: Δημιουργία PDF από HTML σε C# – Οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create PDF from HTML in C# quickly—learn how to convert HTML to PDF,
    save HTML as PDF, and export HTML as PDF with a simple library.
  headline: Create PDF from HTML in C# – Complete Programming Guide
  type: TechArticle
- description: Create PDF from HTML in C# quickly—learn how to convert HTML to PDF,
    save HTML as PDF, and export HTML as PDF with a simple library.
  name: Create PDF from HTML in C# – Complete Programming Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 SDK or later (the code works on .NET Core and .NET Framework
      alike). - Basic familiarity with C# and the command line. - An HTML file you
      want to turn into a PDF (we’ll call it `input.html`).'
  - name: How It Works
    text: 1. **Reading the HTML** – We pull the raw HTML string from `input.html`.
      This step is crucial for the **save html as pdf** part because the converter
      works with a string, not a file handle. 2. **Creating a `PdfDocument`** – Think
      of this as the blank canvas where each page will be painted. 3. **`Pdf
  - name: Handling CSS and Images
    text: '```csharp // Load HTML with a base URL so relative paths resolve correctly.
      string baseUrl = Path.GetDirectoryName(htmlPath) ?? ""; PdfGenerator.AddPdfPages(pdf,
      htmlContent, PageSize.A4, new PdfGenerateConfig { BaseUrl = new Uri($"file:///{baseUrl}/")
      }); ```'
  - name: Large Documents & Pagination
    text: 'If your HTML creates many pages, the library automatically adds them. However,
      you might want to control page breaks manually:'
  type: HowTo
tags:
- C#
- HTML
- PDF
- Conversion
title: Δημιουργία PDF από HTML σε C# – Πλήρης Οδηγός Προγραμματισμού
url: /el/net/html-extensions-and-conversions/create-pdf-from-html-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία PDF από HTML σε C# – Πλήρης Οδηγός Προγραμματισμού

Έχετε αναρωτηθεί ποτέ πώς να **create PDF from HTML** χωρίς να παλεύετε με μια δεκάδα εργαλείων γραμμής εντολών; Δεν είστε μόνοι. Οι περισσότεροι προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν χρειάζεται να μετατρέψουν μια δυναμική ιστοσελίδα σε εκτυπώσιμη αναφορά, ένα τιμολόγιο ή ένα λήξιμο φυλλάδιο.

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα μια απλή, ολοκληρωμένη λύση που σας επιτρέπει να **convert HTML to PDF**, **save HTML as PDF**, και ακόμη **export HTML as PDF** με λίγες μόνο γραμμές C#. Στο τέλος θα έχετε μια επαναχρησιμοποιήσιμη μέθοδο που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET—χωρίς μυστικές εξαρτήσεις, χωρίς κρυφή μαγεία.

## Τι Θα Μάθετε

- Πώς να ρυθμίσετε μια ελάχιστη εφαρμογή κονσόλας C# για μετατροπή HTML‑σε‑PDF.  
- Ο ακριβής κώδικας που απαιτείται για **create PDF from HTML** χρησιμοποιώντας τη δημοφιλής βιβλιοθήκη *HtmlRenderer.PdfSharp* (ή οποιαδήποτε παρόμοια βιβλιοθήκη).  
- Γιατί μπορεί να προτιμάτε μια συγχρονισμένη κλήση αντί για ασύγχρονη, και πότε η κάθε μία έχει νόημα.  
- Συνηθισμένα προβλήματα—απουσία CSS, μεγάλες εικόνες και σχετικές διαδρομές—και πώς να τα παρακάμψετε.  
- Ένα γρήγορο τεστ που μπορείτε να εκτελέσετε για να επαληθεύσετε ότι το αποτέλεσμα ταιριάζει με τις προσδοκίες.

### Προαπαιτούμενα

- .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί τόσο σε .NET Core όσο και σε .NET Framework).  
- Βασική εξοικείωση με C# και τη γραμμή εντολών.  
- Ένα αρχείο HTML που θέλετε να μετατρέψετε σε PDF (θα το ονομάσουμε `input.html`).  

Αν τα έχετε, ας ξεκινήσουμε.

## Δημιουργία PDF από HTML – Ρύθμιση του Έργου

Πρώτα, δημιουργήστε ένα νέο έργο κονσόλας. Ανοίξτε ένα τερματικό και πληκτρολογήστε:

```bash
dotnet new console -n HtmlToPdfDemo
cd HtmlToPdfDemo
```

Στη συνέχεια, προσθέστε τη βιβλιοθήκη μετατροπής. Για αυτό το παράδειγμα θα χρησιμοποιήσουμε **HtmlRenderer.PdfSharp**, η οποία περιβάλλει το PdfSharp και διαχειρίζεται το μεγαλύτερο μέρος του HTML/CSS αυτόματα:

```bash
dotnet add package HtmlRenderer.PdfSharp --version 1.7.2
```

> **Pro tip:** Αν στοχεύετε .NET Framework, μπορείτε ακόμα να χρησιμοποιήσετε το ίδιο πακέτο NuGet· απλώς βεβαιωθείτε ότι το αρχείο έργου σας στοχεύει στη σωστή έκδοση του πλαισίου.

Τώρα έχετε όλα όσα χρειάζεστε για να **convert html to pdf**.

## Μετατροπή HTML σε PDF – Χρήση HtmlToPdfConverter

Δημιουργήστε ένα νέο αρχείο κλάσης με όνομα `PdfConverter.cs` (ή κρατήστε τα πάντα στο `Program.cs` για μια γρήγορη επίδειξη). Παρακάτω υπάρχει ένα **complete, runnable** παράδειγμα που φορτώνει ένα έγγραφο HTML, το μετατρέπει και γράφει το αποτέλεσμα στο δίσκο.

```csharp
using System;
using System.IO;
using TheArtOfDev.HtmlRenderer.PdfSharp;   // Namespace from HtmlRenderer.PdfSharp
using PdfSharp.Pdf;

namespace HtmlToPdfDemo
{
    /// <summary>
    /// Simple helper that encapsulates the HTML → PDF conversion logic.
    /// </summary>
    public static class PdfConverter
    {
        /// <summary>
        /// Converts the specified HTML file to a PDF and saves it.
        /// </summary>
        /// <param name="htmlPath">Full path to the source HTML file.</param>
        /// <param name="pdfPath">Full path where the PDF should be written.</param>
        public static void ConvertHtmlToPdf(string htmlPath, string pdfPath)
        {
            // Validate inputs early – helps you avoid vague exceptions later.
            if (!File.Exists(htmlPath))
                throw new FileNotFoundException($"HTML file not found: {htmlPath}");

            // Read the HTML content. Using UTF‑8 ensures you keep any special characters.
            string htmlContent = File.ReadAllText(htmlPath);

            // Create a new PDF document. This is the container that will hold our pages.
            using PdfDocument pdf = new PdfDocument();

            // The HtmlRender library does the heavy lifting. It parses the HTML and draws it onto a PDF page.
            PdfGenerator.AddPdfPages(pdf, htmlContent, PageSize.A4);

            // Finally, write the PDF to the destination path.
            pdf.Save(pdfPath);
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths to match your environment.
            string inputHtml = Path.Combine(Environment.CurrentDirectory, "input.html");
            string outputPdf = Path.Combine(Environment.CurrentDirectory, "output.pdf");

            try
            {
                PdfConverter.ConvertHtmlToPdf(inputHtml, outputPdf);
                Console.WriteLine($"✅ Success! PDF created at: {outputPdf}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Failed to create PDF: {ex.Message}");
            }
        }
    }
}
```

### Πώς Λειτουργεί

1. **Reading the HTML** – Ανάγουμε τη ακατέργαστη συμβολοσειρά HTML από το `input.html`. Αυτό το βήμα είναι κρίσιμο για το τμήμα **save html as pdf** επειδή ο μετατροπέας λειτουργεί με μια συμβολοσειρά, όχι με χειριστή αρχείου.  
2. **Creating a `PdfDocument`** – Σκεφτείτε το ως το κενό καμβά όπου θα ζωγραφιστεί κάθε σελίδα.  
3. `PdfGenerator.AddPdfPages` – Η καρδιά της βιβλιοθήκης· αναλύει το HTML, εφαρμόζει βασικό CSS και το αποδίδει σε μία ή περισσότερες σελίδες A4.  
4. **Saving the file** – Η κλήση `pdf.Save` γράφει το δυαδικό PDF στο δίσκο, εξάγοντας ουσιαστικά **export html as pdf**.

Εκτελέστε το πρόγραμμα:

```bash
dotnet run
```

Αν όλα είναι ρυθμισμένα σωστά, θα δείτε ένα πράσινο σημάδι ελέγχου και θα βρείτε το `output.pdf` δίπλα στο εκτελέσιμο σας.

## Αποθήκευση HTML ως PDF – Λεπτομέρειες Διαχείρισης Αρχείων

Μπορεί να αναρωτιέστε, *«Γιατί να μην ρέξουμε το PDF απευθείας σε μια απάντηση;»* Καλή ερώτηση. Σε πολλές περιπτώσεις web‑API θα ρέξετε τα bytes, αλλά για εφαρμογές desktop ή batch συχνά χρειάζεται ένα φυσικό αρχείο. Ο παραπάνω κώδικας ήδη **save html as pdf** καλώντας το `pdf.Save(pdfPath)`.

Μερικές λεπτομέρειες:

- **Overwrite protection** – Το `pdf.Save` θα αντικαταστήσει σιωπηλά ένα υπάρχον αρχείο. Αν θέλετε ασφάλεια, ελέγξτε πρώτα το `File.Exists(pdfPath)` και είτε μετονομάστε είτε ζητήστε επιβεβαίωση από τον χρήστη.  
- **Folder permissions** – Βεβαιωθείτε ότι η διεργασία έχει δικαίωμα εγγραφής στον προορισμό, ειδικά σε Linux containers όπου ο προεπιλεγμένος χρήστης μπορεί να είναι περιορισμένος.  
- **Encoding** – Το αρχείο HTML πρέπει να είναι UTF‑8· διαφορετικά μπορεί να εμφανιστούν ακατάληπτοι χαρακτήρες στο τελικό PDF.

## Εξαγωγή HTML ως PDF – Προχωρημένες Επιλογές

Το απλό παράδειγμα λειτουργεί για τις περισσότερες στατικές σελίδες, αλλά το HTML στην πραγματική ζωή συχνά περιλαμβάνει εξωτερικό CSS, εικόνες ή ακόμη και JavaScript. Δείτε πώς μπορείτε να επεκτείνετε τον μετατροπέα για να διαχειριστεί αυτές τις περιπτώσεις.

### Διαχείριση CSS και Εικόνων

```csharp
// Load HTML with a base URL so relative paths resolve correctly.
string baseUrl = Path.GetDirectoryName(htmlPath) ?? "";
PdfGenerator.AddPdfPages(pdf, htmlContent, PageSize.A4, 
    new PdfGenerateConfig
    {
        BaseUrl = new Uri($"file:///{baseUrl}/")
    });
```

- **BaseUrl** λέει στον renderer πού να ψάξει για `src="images/logo.png"` ή `href="styles/main.css"`.  
- Για απομακρυσμένα στοιχεία, μπορείτε να ορίσετε το `BaseUrl` σε μια HTTP διεύθυνση, αλλά προσέξτε την καθυστέρηση δικτύου.

### Μεγάλα Έγγραφα & Σελιδοποίηση

Αν το HTML σας δημιουργεί πολλές σελίδες, η βιβλιοθήκη τις προσθέτει αυτόματα. Ωστόσο, ίσως θέλετε να ελέγξετε τα διαχωριστικά σελίδων χειροκίνητα:

```html
<div style="page-break-after: always;"></div>
```

Σε C# μπορείτε επίσης να χωρίσετε το HTML σε ενότητες και να καλέσετε το `AddPdfPages` επανειλημμένα, δίνοντάς σας πιο ακριβή έλεγχο πάνω σε κεφαλίδες και υποσέλιδα.

## Πώς να Μετατρέψετε HTML σε PDF – Συνηθισμένα Προβλήματα

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|----------|------------------|----------|
| Απουσία γραμματοσειρών | Το PdfSharp χρησιμοποιεί μόνο τις προεπιλεγμένες γραμματοσειρές. | Ενσωματώστε γραμματοσειρές TrueType μέσω του `PdfFontResolver`. |
| Οι εικόνες δεν εμφανίζονται | Σπασμένες σχετικές διαδρομές ή μη υποστηριζόμενες μορφές. | Χρησιμοποιήστε `BaseUrl` ή ενσωματώστε τις εικόνες ως Base64. |
| Το CSS δεν εφαρμόζεται | Η βιβλιοθήκη υποστηρίζει μόνο ένα υποσύνολο του CSS. | Διατηρήστε τα στυλ απλά, ή προεπεξεργαστείτε το HTML με έναν headless browser (π.χ., Puppeteer). |
| Έλλειψη μνήμης σε τεράστιες σελίδες | Όλες οι σελίδες παραμένουν στη μνήμη μέχρι το `Save`. | Μετατρέψτε σε τμήματα ή χρησιμοποιήστε ένα streaming API αν είναι διαθέσιμο. |

## Αναμενόμενο Αποτέλεσμα

Αφού εκτελέσετε το παράδειγμα, ανοίξτε το `output.pdf` με οποιονδήποτε προβολέα PDF. Θα πρέπει να δείτε μια ακριβή απόδοση του `input.html`—τιτλοί, παράγραφοι και εικόνες (αν υπάρχουν) όλα τοποθετημένα σε σελίδες A4. Το μέγεθος του αρχείου κυμαίνεται συνήθως από 50 KB για απλό κείμενο έως μερικές εκατοντάδες kilobytes για σελίδες με πολλές εικόνες.

![create pdf from html example output](https://example.com/assets/create-pdf-from-html.png "create pdf from html example output")

*Το παραπάνω στιγμιότυπο δείχνει μια απλή σελίδα HTML που μετατράπηκε σε καθαρό PDF.*

## Σύνοψη & Επόμενα

## Τι Θα Μάθετε Στη Σειρά;

- [Δημιουργία PDF από HTML – Οδηγός Βήμα‑βήμα C#](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)
- [Μετατροπή HTML σε PDF σε .NET με Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Δημιουργία Εγγράφου HTML με Στυλιζαρισμένο Κείμενο και Εξαγωγή σε PDF – Πλήρης Οδηγός](/html/english/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
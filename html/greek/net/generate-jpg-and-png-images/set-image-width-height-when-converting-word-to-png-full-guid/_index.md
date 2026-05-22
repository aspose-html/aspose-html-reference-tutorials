---
category: general
date: 2026-05-22
description: Ορίστε το πλάτος και το ύψος της εικόνας κατά τη μετατροπή ενός εγγράφου
  Word σε PNG. Μάθετε πώς να εξάγετε το docx ως εικόνα με υψηλής ποιότητας απόδοση
  σε έναν βήμα‑βήμα οδηγό.
draft: false
keywords:
- set image width height
- convert word to png
- save docx as png
- export docx as image
- how to render word
language: el
og_description: Ορίστε το πλάτος και το ύψος της εικόνας κατά τη μετατροπή ενός εγγράφου
  Word σε PNG. Αυτό το σεμινάριο δείχνει πώς να εξάγετε το docx ως εικόνα με ρυθμίσεις
  υψηλής ποιότητας.
og_title: Ορισμός Πλάτους και Ύψους Εικόνας Κατά τη Μετατροπή Word σε PNG – Πλήρης
  Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-05-22'
  description: Set image width height while converting a Word document to PNG. Learn
    how to export docx as image with high‑quality rendering in a step‑by‑step tutorial.
  headline: Set Image Width Height When Converting Word to PNG – Full Guide
  type: TechArticle
- description: Set image width height while converting a Word document to PNG. Learn
    how to export docx as image with high‑quality rendering in a step‑by‑step tutorial.
  name: Set Image Width Height When Converting Word to PNG – Full Guide
  steps:
  - name: 1. Preserve Transparent Backgrounds
    text: 'If your Word document contains shapes with transparent backgrounds and
      you want to keep that transparency, set the `BackgroundColor` to `Color.Transparent`:'
  - name: 2. Render Only a Specific Range
    text: Sometimes you only need a paragraph or a table, not the whole page. Use
      `DocumentVisitor` to extract the node and render it separately. That’s a more
      advanced scenario, but it shows **how to render word** content at a granular
      level.
  - name: 3. Adjust DPI Dynamically
    text: 'If you need different DPI per page (e.g., high‑resolution for the cover
      page), modify `Resolution` inside the loop:'
  - name: 4. Batch Processing
    text: When converting dozens of documents, wrap the whole flow in a method and
      reuse the same `ImageRenderingOptions` instance. Re‑using the options object
      reduces allocation overhead.
  type: HowTo
tags:
- Aspose.Words
- C#
- Image Rendering
title: Ορισμός Πλάτους και Ύψους Εικόνας κατά τη Μετατροπή Word σε PNG – Πλήρης Οδηγός
url: /el/net/generate-jpg-and-png-images/set-image-width-height-when-converting-word-to-png-full-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ορισμός Πλάτους και Ύψους Εικόνας Κατά τη Μετατροπή Word σε PNG – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ πώς να **ορίσετε πλάτος ύψος εικόνας** ενώ **μετατρέπετε Word σε PNG**; Δεν είστε οι μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν η προεπιλεγμένη εξαγωγή δίνει θολή εικόνα ή λάθος διαστάσεις, και στη συνέχεια ξοδεύουν ώρες ψάχνοντας για μια λύση που λειτουργεί πραγματικά.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια καθαρή, ολοκληρωμένη λύση που δείχνει **πώς να αποδίδουμε word** έγγραφα ως εικόνες PNG, επιτρέποντάς σας να **αποθηκεύσετε docx ως PNG** με ακριβή έλεγχο πλάτους‑ύψους και υψηλής ποιότητας antialiasing. Στο τέλος θα έχετε ένα έτοιμο κομμάτι κώδικα, καλή κατανόηση των επιλογών του API, και μερικές επαγγελματικές συμβουλές για την αποφυγή κοινών παγίδων.

## Τι Θα Μάθετε

- Φόρτωση αρχείου `.docx` χρησιμοποιώντας το Aspose.Words for .NET.  
- **Ορισμός πλάτους ύψους εικόνας** με `ImageRenderingOptions`.  
- **Εξαγωγή docx ως εικόνα** (PNG) με ενεργοποιημένο antialiasing.  
- Πώς να **μετατρέψετε word σε png** για μία σελίδα ή ολόκληρο το έγγραφο.  
- Συμβουλές για διαχείριση μεγάλων εγγράφων, DPI και διαδρομές αρχείων.

Χωρίς εξωτερικά εργαλεία, χωρίς πολύπλοκες εντολές γραμμής εντολών—απλός κώδικας C# που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project.

---

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα εξής:

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|-----------------------|
| **.NET 6.0+** (ή .NET Framework 4.7.2) | Το Aspose.Words υποστηρίζει και τα δύο, αλλά τα νεότερα runtime προσφέρουν καλύτερη απόδοση. |
| **Aspose.Words for .NET** πακέτο NuGet (`Install-Package Aspose.Words`) | Παρέχει την κλάση `Document` και τη μηχανή απόδοσης. |
| Ένα **Word έγγραφο** (`.docx`) που **θέλετε να μετατρέψετε σε PNG**. | Η πηγή που θα μετατρέψετε. |
| Βασικές γνώσεις C# – θα καταλάβετε τις δηλώσεις `using` και την αρχικοποίηση αντικειμένων. | Κρατά το επίπεδο δυσκολίας χαμηλό. |

Αν λείπει το πακέτο NuGet, εκτελέστε την παρακάτω εντολή στο Package Manager Console:

```powershell
Install-Package Aspose.Words
```

Αυτό είναι όλο—μόλις **το πακέτο είναι εγκατεστημένο**, είστε έτοιμοι να ξεκινήσετε τον κώδικα.

---

## Βήμα 1: Φόρτωση του Πηγαίου Εγγράφου

Το πρώτο πράγμα που πρέπει να κάνετε είναι να **δείξετε στη βιβλιοθήκη το αρχείο Word που θέλετε να μετατρέψετε**.

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Load the .docx file from disk
Document doc = new Document(@"C:\MyFiles\input.docx");
```

**Γιατί είναι σημαντικό:** Η κλάση `Document` διαβάζει ολόκληρο το πακέτο Word στη μνήμη, δίνοντάς σας πρόσβαση σε σελίδες, στυλ και όλα τα υπόλοιπα. Αν η διαδρομή είναι λανθασμένη, θα **πάρετε ένα `FileNotFoundException`**, οπότε ελέγξτε ξανά ότι το αρχείο υπάρχει και ότι η διαδρομή χρησιμοποιεί **διαφθορά (escaped) backslashes (`\\`)** ή **ακριβή συμβολοσειρά (`@`)**.  

> **Pro tip:** Τυλίξτε την κλήση φόρτωσης **σε ένα `try/catch` block** αν **αναμένετε ότι το αρχείο μπορεί να λείπει κατά την εκτέλεση**.

---

## Βήμα 2: Διαμόρφωση Επιλογών Απόδοσης Εικόνας (Set Image Width Height)

Τώρα έρχεται **η καρδιά** του tutorial: **πώς να ορίσετε πλάτος ύψος εικόνας** ώστε το παραγόμενο PNG να μην είναι **τεντωμένο** ή **pixelated**. Η κλάση `ImageRenderingOptions` σας δίνει λεπτομερή έλεγχο διαστάσεων, DPI και εξομάλυνσης.

```csharp
// Create rendering options and explicitly set width and height
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Desired output size in pixels
    Width = 1024,          // Set image width height: 1024px wide
    Height = 768,          // Set image width height: 768px tall

    // High‑quality antialiasing works on Windows, Linux, and macOS
    UseAntialiasing = true,

    // Optional: increase DPI for sharper output (default is 96)
    Resolution = 300
};
```

**Επεξήγηση των βασικών ιδιοτήτων:**

- `Width` και `Height` – **ακριβείς** διαστάσεις σε pixel που **θέλετε**. Με το **να τις ορίσετε**, **ορίζετε πλάτος ύψος εικόνας** άμεσα, παρακάμπτοντας το προεπιλεγμένο μέγεθος σελίδας.  
- `UseAntialiasing` – Ενεργοποιεί υψηλής ποιότητας εξομάλυνση κειμένου και διανυσματικών γραφικών, κάτι κρίσιμο όταν **μετατρέπετε word σε png** και θέλετε καθαρά άκρα.  
- `Resolution` – Υψηλότερο DPI προσφέρει περισσότερη λεπτομέρεια, ειδικά για σύνθετες διατάξεις. Προσέξτε τη χρήση μνήμης· μια εικόνα 300 DPI μπορεί να είναι μεγάλη.

> **Γιατί να μην βασιστείτε στο προεπιλεγμένο μέγεθος;** Το προεπιλεγμένο χρησιμοποιεί τις φυσικές διαστάσεις της σελίδας (π.χ., A4 στα 96 DPI). Αυτό συχνά παράγει εικόνα 794 × 1123 pixel—καλό για κάποιες περιπτώσεις, αλλά όχι όταν χρειάζεστε συγκεκριμένο μικρογραφικό UI ή σταθερό προεπισκόπηση.

---

## Βήμα 3: Απόδοση και Αποθήκευση ως PNG (Export Docx as Image)

Με το έγγραφο φορτωμένο και τις επιλογές ρυθμισμένες, μπορείτε τελικά να **εξάγετε docx ως εικόνα**. Η μέθοδος `RenderToImage` κάνει το σκληρό κομμάτι.

```csharp
// Render the first page (page index 0) to a PNG file
doc.RenderToImage(@"C:\MyFiles\output.png", imageOptions);
```

Αν θέλετε να αποδώσετε **ολόκληρο το έγγραφο** (όλες τις σελίδες) σε ξεχωριστά αρχεία PNG, κάντε βρόχο πάνω στη συλλογή σελίδων:

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string outPath = $@"C:\MyFiles\page_{i + 1}.png";
    doc.RenderToImage(outPath, imageOptions, i);
}
```

**Τι συμβαίνει στο παρασκήνιο;** Ο renderer rasterizes κάθε σελίδα χρησιμοποιώντας τις διαστάσεις που δώσατε, εφαρμόζει antialiasing και γράφει ένα byte stream PNG στο δίσκο. Επειδή το PNG είναι lossless, διατηρείτε την πλήρη πιστότητα της αρχικής διάταξης του Word.

**Αναμενόμενο αποτέλεσμα:** Μια καθαρή εικόνα PNG ακριβώς 1024 × 768 pixel (ή όποιο μέγεθος έχετε ορίσει). Ανοίξτε την σε οποιονδήποτε προβολέα εικόνων και θα δείτε το περιεχόμενο του Word αποδομένο ακριβώς όπως εμφανίζεται στο αρχικό έγγραφο, αλλά τώρα ως bitmap.

---

## Προχωρημένες Συμβουλές & Παραλλαγές

### 1. Διατήρηση Διαφανών Φόντων

Αν το Word έγγραφό σας περιέχει σχήματα με διαφανές φόντο και θέλετε να το διατηρήσετε, ορίστε το `BackgroundColor` σε `Color.Transparent`:

```csharp
imageOptions.BackgroundColor = System.Drawing.Color.Transparent;
```

### 2. Απόδοση Μόνο Συγκεκριμένου Εύρους

Μερικές φορές χρειάζεστε μόνο μια παράγραφο ή έναν πίνακα, όχι ολόκληρη τη σελίδα. Χρησιμοποιήστε `DocumentVisitor` για να εξάγετε τον κόμβο και να τον αποδώσετε ξεχωριστά. Είναι πιο προχωρημένο σενάριο, αλλά δείχνει **πώς να αποδίδετε word** περιεχόμενο σε πιο λεπτομερή επίπεδο.

### 3. Δυναμική Ρύθμιση DPI

Αν χρειάζεστε διαφορετικό DPI ανά σελίδα (π.χ., υψηλή ανάλυση για την εξώφυλλο), τροποποιήστε το `Resolution` μέσα στον βρόχο:

```csharp
if (i == 0) imageOptions.Resolution = 600; // cover page
else imageOptions.Resolution = 300;
```

### 4. Επεξεργασία σε Παρτίδες

Όταν μετατρέπετε δεκάδες έγγραφα, τυλίξτε όλη τη ροή σε μια μέθοδο και επαναχρησιμοποιήστε το ίδιο αντικείμενο `ImageRenderingOptions`. Η επαναχρήση του αντικειμένου μειώνει το κόστος κατανομής μνήμης.

---

## Συχνές Παγίδες & Πώς να τις Αποφύγετε

| Συμπτωμα | Πιθανή Αιτία | Διόρθωση |
|----------|--------------|----------|
| Το PNG είναι θολό παρά το υψηλό DPI | `UseAntialiasing` είναι `false` | Ορίστε `UseAntialiasing = true`. |
| Το μέγεθος εξόδου δεν ταιριάζει με `Width`/`Height` | Δεν λήφθηκε υπόψη το DPI | Πολλαπλασιάστε το επιθυμητό μέγεθος με `Resolution / 96` ή προσαρμόστε το `Resolution`. |
| Εξαίρεση Out‑of‑memory σε μεγάλα έγγραφα | Απόδοση ολόκληρου εγγράφου στα 300 DPI | Αποδώστε μία σελίδα τη φορά, απελευθερώνοντας κάθε εικόνα μετά την αποθήκευση. |
| Το PNG εμφανίζει λευκό φόντο σε διαφανείς εικόνες | `BackgroundColor` δεν έχει οριστεί | Ορίστε `imageOptions.BackgroundColor = Color.Transparent`. |

---

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω υπάρχει ένα αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε μια εφαρμογή console. Δείχνει **convert word to png**, **save docx as png**, και φυσικά **set image width height**.

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;
using System.Drawing; // For Color

namespace WordToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document
            string inputPath = @"C:\MyFiles\input.docx";
            Document doc = new Document(inputPath);

            // 2️⃣ Configure rendering options (set image width height)
            ImageRenderingOptions options = new ImageRenderingOptions
            {
                Width = 1024,          // Desired pixel width
                Height = 768,          // Desired pixel height
                UseAntialiasing = true,
                Resolution = 300,
                BackgroundColor = Color.Transparent // Keep transparency if needed
            };

            // 3️⃣ Render the first page to PNG (export docx as image)
            string outputPath = @"C:\MyFiles\output.png";
            doc.RenderToImage(outputPath, options);

            Console.WriteLine($"✅ Document rendered successfully to {outputPath}");
            // Optional: render all pages
            //RenderAllPages(doc, options);
        }

        // Helper method for batch rendering (uncomment if needed)
        static void RenderAllPages(Document doc, ImageRenderingOptions options)
        {
            for (int i = 0; i < doc.PageCount; i++)
            {
                string pagePath = $@"C:\MyFiles\page_{i + 1}.png";
                doc.RenderToImage(pagePath, options, i);
                Console.WriteLine($"Page {i + 1} saved to {pagePath}");
            }
        }
    }
}
```

**Τρέξτε το:** Κατασκευάστε το project, τοποθετήστε ένα έγκυρο `input.docx` στη διαδρομή που καθορίσατε, και εκτελέστε. Θα πρέπει να δείτε ένα `output.png` ακριβώς **1024 × 768** pixel, αποδομένο με ομαλές άκρες.

## Σχετικά Tutorials

- [How to Enable Antialiasing When Converting DOCX to PNG/JPG](/html/english/net/generate-jpg-and-png-images/how-to-enable-antialiasing-when-converting-docx-to-png-jpg/)
- [convert docx to png – create zip archive c# tutorial](/html/english/net/generate-jpg-and-png-images/convert-docx-to-png-create-zip-archive-c-tutorial/)
- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
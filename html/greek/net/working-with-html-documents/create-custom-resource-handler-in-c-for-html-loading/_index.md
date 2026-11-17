---
category: general
date: 2026-08-15
description: Δημιουργήστε προσαρμοσμένο διαχειριστή πόρων σε C# για τη διαχείριση
  πόρων HTML όπως εικόνες και CSS. Μάθετε τις HTMLLoadOptions, τις ροές μνήμης και
  τη φόρτωση του HTMLDocument.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom resource handler
- C# resource handler
- HTMLLoadOptions
- HTMLDocument loading
- memory stream for resources
language: el
lastmod: 2026-08-15
og_description: Δημιουργήστε προσαρμοσμένο διαχειριστή πόρων σε C# για να ελέγχετε
  πώς μεταδίδονται οι πόροι HTML. Αυτό το σεμινάριο δείχνει τη ρύθμιση του HTMLLoadOptions,
  τη διαχείριση της μνήμης ροής και τη φόρτωση του HTMLDocument με προσαρμοσμένη λογική.
og_image_alt: Screenshot of C# code defining a custom resource handler class for HTML
  loading
og_title: Δημιουργία προσαρμοσμένου διαχειριστή πόρων σε C# – πλήρης οδηγός διαχείρισης
  πόρων HTML
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  headline: Create custom resource handler in C# for HTML loading
  type: TechArticle
- description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  name: Create custom resource handler in C# for HTML loading
  steps:
  - name: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
    text: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
  - name: Configure `HTMLLoadOptions` to use the handler.
    text: Configure `HTMLLoadOptions` to use the handler.
  - name: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
    text: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
  - name: (Optional) Store received resources to disk for verification.
    text: (Optional) Store received resources to disk for verification.
  type: HowTo
tags:
- C#
- HTML
- resource handling
title: Δημιουργία προσαρμοσμένου διαχειριστή πόρων σε C# για τη φόρτωση HTML
url: /el/net/working-with-html-documents/create-custom-resource-handler-in-c-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία προσαρμοσμένου διαχειριστή πόρων σε C# για φόρτωση HTML

Αν χρειάζεστε **create custom resource handler** για αρχεία HTML, αυτός ο οδηγός σας δείχνει ακριβώς πώς. Θα μάθετε πώς να παρεμβάλλετε εικόνες, CSS και άλλα στοιχεία κατά τη φόρτωση ενός εγγράφου HTML, χρησιμοποιώντας `HTMLLoadOptions` και μια ροή βασισμένη στη μνήμη.

Το tutorial καλύπτει όλα όσα απαιτούνται για την υλοποίηση ενός επαναχρησιμοποιήσιμου διαχειριστή, τη διαμόρφωση των επιλογών φόρτωσης και την επαλήθευση ότι οι πόροι καταγράφονται σωστά. Δεν χρειάζεται εξωτερική τεκμηρίωση — μόνο ο κώδικας παρακάτω και οι εξηγήσεις.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο
- Βασική εξοικείωση με C#
- Αναφορά στη βιβλιοθήκη επεξεργασίας HTML που παρέχει `HTMLDocument`, `HtmlLoadOptions` και `ResourceHandler` (π.χ., GroupDocs.Viewer for .NET)

## Επισκόπηση της λύσης

Θα:

1. **Create a custom resource handler** κληρονομώντας την κλάση `ResourceHandler`.
2. Διαμορφώσουμε το `HTMLLoadOptions` ώστε να χρησιμοποιεί τον διαχειριστή.
3. Φορτώσουμε ένα αρχείο HTML με το `HTMLDocument` ενώ ο διαχειριστής παρέχει ροή για κάθε πόρο.
4. (Προαιρετικά) Αποθηκεύσουμε τους ληφθέντες πόρους στο δίσκο για επαλήθευση.

Κάθε βήμα περιλαμβάνει πλήρη πηγαίο κώδικα και τη λογική που τον υποστηρίζει.

## Βήμα 1: Ορισμός της κλάσης προσαρμοσμένου διαχειριστή πόρων

Η δημιουργία προσαρμοσμένου διαχειριστή σημαίνει την υπερφόρτωση του `HandleResource` ώστε η βιβλιοθήκη να γράφει τα bytes του πόρου σε ροή που ελέγχετε. Η χρήση `MemoryStream` διατηρεί τα δεδομένα στη μνήμη, κάτι ιδανικό για δοκιμές ή περαιτέρω επεξεργασία.

```csharp
using System;
using System.IO;
using GroupDocs.Viewer.Handler;   // Adjust namespace to match your library

namespace HtmlResourceDemo
{
    /// <summary>
    /// Provides a memory stream for each HTML resource (images, CSS, etc.).
    /// </summary>
    public class MyHandler : ResourceHandler
    {
        /// <summary>
        /// Called by the viewer for every external resource referenced in the HTML.
        /// </summary>
        /// <param name="info">Information about the resource (name, MIME type, etc.).</param>
        /// <returns>A writable stream that receives the resource data.</returns>
        public override Stream HandleResource(ResourceInfo info)
        {
            // A fresh MemoryStream ensures the viewer can write the resource bytes.
            // You could replace this with a FileStream to save directly to disk.
            return new MemoryStream();
        }
    }
}
```

**Γιατί είναι σημαντικό:**  
Η υπερφόρτωση του `HandleResource` σας δίνει πλήρη έλεγχο στο πού πηγαίνουν τα δεδομένα του πόρου. Αν αργότερα χρειαστείτε να κάνετε cache εικόνων, να μετασχηματίσετε CSS ή να καταγράψετε τη χρήση πόρων, μπορείτε να αντικαταστήσετε το `MemoryStream` με οποιαδήποτε προσαρμοσμένη υλοποίηση ροής.

## Βήμα 2: Διαμόρφωση του `HTMLLoadOptions` για χρήση του διαχειριστή

Το `HTMLLoadOptions` σας επιτρέπει να ενσωματώσετε τον διαχειριστή στην αλυσίδα φόρτωσης. Ορίζοντας την ιδιότητα `ResourceHandler` λέτε στον προβολέα να καλέσει το `MyHandler` για κάθε εξωτερικό στοιχείο.

```csharp
using GroupDocs.Viewer.Options;   // Namespace for HtmlLoadOptions

// ...

var loadOptions = new HtmlLoadOptions
{
    // Attach the custom handler defined in Step 1
    ResourceHandler = new MyHandler()
};
```

**Γιατί είναι σημαντικό:**  
Χωρίς την ανάθεση του `ResourceHandler`, ο προβολέας θα έγραφε τους πόρους στην προεπιλεγμένη τοποθεσία του (συχνά σε προσωρινό φάκελο). Καθορίζοντας τον δικό σας διαχειριστή, **create custom resource handler** συμπεριφορά που ευθυγραμμίζεται με τη στρατηγική αποθήκευσης της εφαρμογής σας.

## Βήμα 3: Φόρτωση του εγγράφου HTML με τις διαμορφωμένες επιλογές

Τώρα φορτώνουμε το αρχείο HTML. Ο προβολέας θα καλέσει το `MyHandler.HandleResource` για κάθε πόρο που εντοπίζει.

```csharp
using GroupDocs.Viewer;           // Namespace for HTMLDocument

// Path to the source HTML file
string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// Load the document using the custom load options
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);
```

Σε αυτό το σημείο το περιεχόμενο HTML έχει αναλυθεί και όλοι οι εξωτερικοί πόροι έχουν ρέει στα buffers μνήμης που παρέχονται από το `MyHandler`.

## Βήμα 4 (προαιρετικό): Πρόσβαση στους καταγεγραμμένους πόρους

Αν χρειάζεται να ελέγξετε ή να αποθηκεύσετε τους πόρους, μπορείτε να τροποποιήσετε το `MyHandler` ώστε να αποθηκεύει κάθε `MemoryStream` σε λεξικό με κλειδί το όνομα του πόρου.

```csharp
public class MyHandler : ResourceHandler
{
    // Stores streams for later retrieval
    public Dictionary<string, MemoryStream> Resources { get; } = new();

    public override Stream HandleResource(ResourceInfo info)
    {
        var stream = new MemoryStream();
        Resources[info.Name] = stream;
        return stream;
    }
}
```

Μετά τη φόρτωση, μπορείτε να διατρέξετε το `handler.Resources` και να γράψετε το καθένα στο δίσκο:

```csharp
var handler = new MyHandler();
var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);

// Save each captured resource
foreach (var kvp in handler.Resources)
{
    string fileName = Path.Combine("output_resources", kvp.Key);
    File.WriteAllBytes(fileName, kvp.Value.ToArray());
    Console.WriteLine($"Saved resource: {fileName}");
}
```

**Γιατί είναι σημαντικό:**  
Η αποθήκευση των πόρων επιτρέπει επεξεργασία όπως βελτιστοποίηση εικόνων, ελαχιστοποίηση CSS ή αρχειοθέτηση. Παρέχει επίσης μια απτή επαλήθευση ότι η λογική **create custom resource handler** λειτουργεί όπως προβλέπεται.

## Βήμα 5: Καθαρισμός

Τanto το `HTMLDocument` όσο και οι ροές πρέπει να απελευθερώνονται για να ελευθερωθούν οι μη διαχειριζόμενοι πόροι.

```csharp
doc.Dispose();                     // Releases internal buffers
foreach (var stream in handler.Resources.Values)
{
    stream.Dispose();              // Flushes and releases memory
}
```

## Πλήρες εκτελέσιμο παράδειγμα

Παρακάτω υπάρχει ένα αυτόνομο πρόγραμμα που δείχνει όλα τα βήματα, από τον ορισμό της κλάσης μέχρι την εξαγωγή πόρων.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Viewer;
using GroupDocs.Viewer.Handler;
using GroupDocs.Viewer.Options;

namespace HtmlResourceDemo
{
    public class MyHandler : ResourceHandler
    {
        public Dictionary<string, MemoryStream> Resources { get; } = new();

        public override Stream HandleResource(ResourceInfo info)
        {
            var stream = new MemoryStream();
            Resources[info.Name] = stream;
            return stream;
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare paths
            string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");
            string outputDir = Path.Combine("output_resources");
            Directory.CreateDirectory(outputDir);

            // 2️⃣ Create handler and load options
            var handler = new MyHandler();
            var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };

            // 3️⃣ Load the HTML document
            using (HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions))
            {
                // Document is now loaded; resources are in handler.Resources
            }

            // 4️⃣ Persist captured resources
            foreach (var kvp in handler.Resources)
            {
                string filePath = Path.Combine(outputDir, kvp.Key);
                File.WriteAllBytes(filePath, kvp.Value.ToArray());
                Console.WriteLine($"Saved: {filePath}");
            }

            // 5️⃣ Clean up streams
            foreach (var stream in handler.Resources.Values)
                stream.Dispose();

            Console.WriteLine("All resources processed.");
        }
    }
}
```

**Αναμενόμενη έξοδος**

```
Saved: output_resources/logo.png
Saved: output_resources/styles.css
Saved: output_resources/banner.jpg
All resources processed.
```

Η κονσόλα εμφανίζει κάθε πόρο που ο προβολέας έστειλε μέσω του προσαρμοσμένου διαχειριστή, επιβεβαιώνοντας ότι η ροή **create custom resource handler** ολοκληρώθηκε με επιτυχία.

## Συχνές ερωτήσεις και ειδικές περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| *Τι γίνεται αν ένας πόρος είναι μεγάλος (π.χ., εικόνα υψηλής ανάλυσης);* | Αντικαταστήστε το `MemoryStream` με ένα `FileStream` που δείχνει σε έναν προσωρινό φάκελο. Αυτό αποτρέπει υπερβολική κατανάλωση μνήμης. |
| *Μπορώ να φιλτράρω πόρους ανά τύπο;* | Μέσα στο `HandleResource`, εξετάστε το `info.MimeType` ή `info.Extension` και επιστρέψτε `null` για ανεπιθύμητους τύπους. Η επιστροφή `null` λέει στον προβολέα να παραλείψει τον πόρο. |
| *Απαιτείται ασφάλεια νήματος;* | Αν η ίδια παρουσία διαχειριστή χρησιμοποιείται σε πολλαπλές ταυτόχρονες φορτώσεις, προστατέψτε το λεξικό `Resources` με κλείδωμα ή χρησιμοποιήστε μια σύγχρονη συλλογή. |
| *Πώς υποστηρίζω σχετικές διευθύνσεις URL;* | Το `ResourceInfo` περιέχει το αρχικό URL· μπορείτε να το συνδυάσετε με τη βάση του αρχείου HTML για να επιλύσετε σχετικές αναφορές πριν την αποθήκευση. |

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **create custom resource handler** σε C# για φόρτωση HTML, να διαμορφώσετε το `HTMLLoadOptions`, να καταγράψετε τα ροές πόρων και να καθαρίσετε υπεύθυνα. Αυτό το πρότυπο σας δίνει πλήρη έλεγχο στη διαχείριση πόρων, επιτρέποντας σενάρια όπως επεξεργασία εικόνων σε πραγματικό χρόνο, επαναγραφή CSS ή ασφαλή αποθήκευση.

Στη συνέχεια, εξερευνήστε συναφή θέματα όπως **HTMLDocument loading** με διαφορετικές επιλογές απόδοσης, ή επεκτείνετε τον διαχειριστή σε υλοποιήσεις **C# resource handler** που γράφουν απευθείας σε αποθήκευση cloud. Πειραματιστείτε με τη μέθοδο `HandleResource` του διαχειριστή για να ταιριάξει στη συγκεκριμένη ροή πόρων του έργου σας.

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση σας.

- [Create HTML from String in C# – Custom Resource Handler Guide](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Custom Resource Handler in C# – Convert HTML to ZIP Tutorial](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
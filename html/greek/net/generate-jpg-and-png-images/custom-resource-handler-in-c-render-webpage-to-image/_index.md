---
category: general
date: 2026-05-28
description: Μάθετε πώς να δημιουργήσετε έναν προσαρμοσμένο διαχειριστή πόρων σε C#
  για να αποδώσετε μια ιστοσελίδα σε εικόνα, να καταγράψετε στιγμιότυπο οθόνης της
  ιστοσελίδας και να αποθηκεύσετε το HTML ως PNG με πλήρη κώδικα.
draft: false
keywords:
- custom resource handler
- render webpage to image
- capture webpage screenshot
- render html to png
- save webpage as png
language: el
og_description: Δημιουργήστε έναν προσαρμοσμένο διαχειριστή πόρων σε C# και αποδώστε
  μια ιστοσελίδα σε εικόνα. Καταγράψτε ένα στιγμιότυπο οθόνης, αποδώστε HTML σε PNG
  και αποθηκεύστε το αποτέλεσμα με ένα πλήρες παράδειγμα.
og_title: Προσαρμοσμένος Διαχειριστής Πόρων σε C# – Απόδοση Ιστοσελίδας σε Εικόνα
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to create a custom resource handler in C# to render webpage
    to image, capture webpage screenshot and save HTML as PNG with complete code.
  headline: Custom Resource Handler in C# – Render Webpage to Image
  type: TechArticle
- description: Learn how to create a custom resource handler in C# to render webpage
    to image, capture webpage screenshot and save HTML as PNG with complete code.
  name: Custom Resource Handler in C# – Render Webpage to Image
  steps:
  - name: Expected Output
    text: Running the full program should produce a PNG that looks like a faithful
      snapshot of `https://example.com`. Open it in any image viewer, and you’ll see
      the page rendered at the default viewport size (usually 1024 × 768 px). All
      linked images and styles are stored alongside, ready for reuse.
  - name: What if the target page uses relative URLs?
    text: Our handler already strips the leading slash (`info.Path.TrimStart('/')`)
      and combines it with the output folder, so relative paths resolve correctly.
      If you encounter a URL that starts with `//` (protocol‑relative), the renderer
      normalizes it before calling `HandleResource`.
  - name: How do I change the output dimensions?
    text: 'Pass a `Size` object to `RenderPage` overload:'
  - name: Can I render multiple pages in one run?
    text: Absolutely. Just loop over a list of URLs and call `RenderPage` each time.
      The same `MyResourceHandler` instance will keep populating the `output` folder,
      keeping everything tidy.
  - name: What about authentication‑protected sites?
    text: If the page requires cookies or HTTP headers, configure an `HttpClient`
      and assign it to the renderer’s `HttpClient` property (if your library exposes
      it). This keeps the **render html to png** flow seamless for internal dashboards.
  type: HowTo
tags:
- C#
- ImageRenderer
- WebAutomation
title: Προσαρμοσμένος Διαχειριστής Πόρων σε C# – Απόδοση Ιστοσελίδας σε Εικόνα
url: /el/net/generate-jpg-and-png-images/custom-resource-handler-in-c-render-webpage-to-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσαρμοσμένος Διαχειριστής Πόρων σε C# – Απόδοση Ιστοσελίδας σε Εικόνα

Έχετε αναρωτηθεί ποτέ πώς να **custom resource handler** τη διαδρομή σας προς ένα τέλειο screenshot οποιασδήποτε ιστοσελίδας; Δεν είστε οι μόνοι. Η λήψη screenshot μιας ιστοσελίδας προγραμματιστικά μπορεί να μοιάζει με κυνήγι ενός κινούμενου στόχου, ειδικά όταν χρειάζεται να αποθηκεύσετε τις εικόνες και τις γραμματοσειρές ακριβώς εκεί που θέλετε.

Σε αυτόν τον οδηγό θα περάσουμε από τη δημιουργία ενός **custom resource handler** σε C#, τη ρύθμιση των επιλογών απόδοσης και, τέλος, τη χρήση του ImageRenderer για **render webpage to image**. Στο τέλος θα ξέρετε πώς να **capture webpage screenshot**, **render html to png**, και **save webpage as png** χωρίς να τσακώσετε τα μαλλιά σας.

## Τι Θα Χρειαστείτε

- .NET 6.0 ή νεότερο (το API που χρησιμοποιούμε στοχεύει στο .NET Standard 2.0, οπότε οποιοδήποτε σύγχρονο runtime λειτουργεί)
- Ένα πακέτο NuGet που παρέχει `ImageRenderer`, `ImageRenderingOptions` και σχετικούς τύπους (π.χ., *Aspose.HTML* ή μια παρόμοια βιβλιοθήκη)
- Βασικές γνώσεις C# — τίποτα εξωπραγματικό, μόνο μερικές `using` δηλώσεις και μια μέθοδο `Main`
- Ένας φάκελος εξόδου όπου ο renderer μπορεί να αποθηκεύει αρχεία (δημιουργήστε τον χειροκίνητα ή αφήστε τον κώδικα να το κάνει)

Αυτό είναι όλο. Χωρίς επιπλέον υπηρεσίες, χωρίς headless browsers, μόνο καθαρός κώδικας .NET.

![Αποθήκευση αποδοθέντων πόρων από προσαρμοσμένο διαχειριστή πόρων](https://example.com/assets/custom-resource-handler.png "προσαρμοσμένος διαχειριστής πόρων")

## Βήμα 1: Δημιουργία **Custom Resource Handler**

Το πρώτο που χρειάζεστε είναι μια κλάση που κληρονομεί από `ResourceHandler`. Εδώ συμβαίνει η μαγεία: κάθε εικόνα, αρχείο CSS ή γραμματοσειρά που ζητά ο renderer περνάει από τον διαχειριστή σας, και εσείς αποφασίζετε πού θα το γράψετε.

```csharp
using System.IO;
using Aspose.Html.Rendering.Image;   // Adjust the namespace to your library

// Step 1: Create a custom resource handler to store rendered resources
class MyResourceHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info)
    {
        // Build a safe file path inside the output directory
        string filePath = Path.Combine("output", info.Path.TrimStart('/'));

        // Ensure the directory hierarchy exists
        Directory.CreateDirectory(Path.GetDirectoryName(filePath)!);

        // Return a writable stream that the renderer will fill
        return File.OpenWrite(filePath);
    }
}
```

**Γιατί είναι σημαντικό:** Χωρίς διαχειριστή, ο renderer μπορεί να κρατήσει τους πόρους στη μνήμη ή να τους απορρίψει εντελώς. Εκθέτοντας ένα `Stream`, αποκτάτε πλήρη έλεγχο πάνω στο πού καταλήγει κάθε περιουσιακό στοιχείο — ιδανικό για μελλοντική επαναχρησιμοποίηση ή εντοπισμό σφαλμάτων.

## Βήμα 2: Ρύθμιση Επιλογών Απόδοσης Εικόνας

Τώρα που έχουμε ένα μέρος για τα assets, ας πούμε στον renderer πώς θέλουμε να φαίνεται η τελική εικόνα. Το antialiasing λειαίνει τις άκρες, το hinting βελτιώνει την ευκρίνεια του κειμένου, και η επιλογή γραμματοσειράς εξασφαλίζει ότι το αποτέλεσμα ταιριάζει με το σχέδιό σας.

```csharp
using Aspose.Html.Drawing;          // For ImageRenderingOptions, TextOptions, Font, etc.

// Step 2: Set up image rendering options (antialiasing, text hinting, font)
var imageOptions = new ImageRenderingOptions
{
    UseAntialiasing = true,
    TextOptions = new TextOptions { UseHinting = true },
    Font = new Font("Times New Roman", 14, WebFontStyle.Bold)
};
```

**Γιατί αυτές οι ρυθμίσεις;** Το antialiasing μειώνει τα σκαλισμένα pixel, ειδικά στις καμπύλες. Το hinting λέει στον rasterizer να ευθυγραμμίζει τα glyphs στα όρια των pixel, κάτι κρίσιμο όταν **render html to png** σε τυπικές αναλύσεις οθόνης. Η έντονη γραμματοσειρά Times New Roman είναι μόνο ένα παράδειγμα· αντικαταστήστε την με οποιαδήποτε web‑safe ή προσαρμοσμένη γραμματοσειρά προτιμάτε.

## Βήμα 3: Σύνδεση του Διαχειριστή με τον Image Renderer

Με τις επιλογές και τον διαχειριστή έτοιμους, δημιουργούμε τον `ImageRenderer`. Η ανάθεση του `MyResourceHandler` στην ιδιότητα `ResourceHandler` εξασφαλίζει ότι κάθε εξωτερικό αρχείο θα καταλήξει στο δίσκο.

```csharp
using Aspose.Html.Rendering.Image; // For ImageRenderer

// Step 3: Create the image renderer with the options and the custom handler
var renderer = new ImageRenderer(imageOptions)
{
    ResourceHandler = new MyResourceHandler()
};
```

**Pro tip:** Αν χρειαστεί ποτέ να καταγράφετε κάθε αίτηση, υπερκαλύψτε το `HandleResource` και προσθέστε ένα `Console.WriteLine(info.Path)` πριν επιστρέψετε το stream. Αυτή η μικρή προσθήκη μπορεί να σας εξοικονομήσει ώρες όταν αντιμετωπίζετε προβλήματα με λείπουν γραμματοσειρές ή σπασμένες εικόνες.

## Βήμα 4: **Render Webpage to Image** και Αποθήκευση

Τέλος, πείτε στον renderer ποιο URL θα καταγράψει και πού θα τοποθετηθεί το PNG. Η κλήση παρακάτω κάνει όλη τη βαριά δουλειά: φέρνει τη σελίδα, επεξεργάζεται το CSS, φορτώνει γραμματοσειρές και γράφει το παραγόμενο bitmap.

```csharp
// Step 4: Render a web page to an image file
renderer.RenderPage("https://example.com", "output/page.png");
```

Όταν η μέθοδος ολοκληρωθεί, θα βρείτε δύο πράγματα στον φάκελο `output`:

1. `page.png` – το screenshot της σελίδας (το αποτέλεσμα του **capture webpage screenshot**)
2. Μια υπο‑δομή φακέλων που αντικατοπτρίζει τους πόρους της σελίδας (CSS, εικόνες, γραμματοσειρές) – όλα αποθηκευμένα χάρη στον **custom resource handler** μας

### Αναμενόμενο Αποτέλεσμα

Η εκτέλεση του πλήρους προγράμματος θα πρέπει να παράγει ένα PNG που μοιάζει με πιστό στιγμιότυπο του `https://example.com`. Ανοίξτε το σε οποιονδήποτε προβολέα εικόνων και θα δείτε τη σελίδα αποδομένη στο προεπιλεγμένο μέγεθος viewport (συνήθως 1024 × 768 px). Όλες οι συνδεδεμένες εικόνες και τα στυλ αποθηκεύονται δίπλα, έτοιμα για επαναχρησιμοποίηση.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν η σελίδα-στόχος χρησιμοποιεί σχετικές διευθύνσεις URL;

Ο διαχειριστής μας αφαιρεί ήδη την αρχική κάθετος (`info.Path.TrimStart('/')`) και τη συνδυάζει με το φάκελο εξόδου, έτσι οι σχετικές διαδρομές επιλύονται σωστά. Αν συναντήσετε ένα URL που αρχίζει με `//` (πρωτόκολλο‑σχετικό), ο renderer το κανονικοποιεί πριν καλέσει το `HandleResource`.

### Πώς αλλάζω τις διαστάσεις εξόδου;

Περάστε ένα αντικείμενο `Size` στην υπερφόρτωση `RenderPage`:

```csharp
renderer.RenderPage("https://example.com", "output/page.png", new Size(1920, 1080));
```

Με αυτόν τον τρόπο μπορείτε να **save webpage as png** σε υψηλή ανάλυση για έτοιμα προς εκτύπωση assets.

### Μπορώ να αποδώσω πολλές σελίδες σε μία εκτέλεση;

Απόλυτα. Απλώς κάντε βρόχο πάνω σε μια λίστα URLs και καλέστε το `RenderPage` κάθε φορά. Η ίδια παρουσία του `MyResourceHandler` θα συνεχίσει να γεμίζει τον φάκελο `output`, διατηρώντας τα πάντα οργανωμένα.

### Τι γίνεται με ιστοσελίδες που απαιτούν έλεγχο ταυτότητας;

Αν η σελίδα απαιτεί cookies ή HTTP headers, διαμορφώστε ένα `HttpClient` και αναθέστε το στην ιδιότητα `HttpClient` του renderer (αν η βιβλιοθήκη σας το εκθέτει). Αυτό διατηρεί τη ροή **render html to png** αδιάσπαστη για εσωτερικά dashboards.

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας τα παραπάνω, ορίστε μια ελάχιστη εφαρμογή console που μπορείτε να αντιγράψετε‑επικολλήσετε στο Visual Studio:

```csharp
using System;
using System.IO;
using Aspose.Html.Drawing;
using Aspose.Html.Rendering.Image;

class MyResourceHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info)
    {
        string filePath = Path.Combine("output", info.Path.TrimStart('/'));
        Directory.CreateDirectory(Path.GetDirectoryName(filePath)!);
        return File.OpenWrite(filePath);
    }
}

class Program
{
    static void Main()
    {
        var imageOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            TextOptions = new TextOptions { UseHinting = true },
            Font = new Font("Times New Roman", 14, WebFontStyle.Bold)
        };

        var renderer = new ImageRenderer(imageOptions)
        {
            ResourceHandler = new MyResourceHandler()
        };

        // Render the page and save as PNG
        renderer.RenderPage("https://example.com", "output/page.png");

        Console.WriteLine("Done! Screenshot saved to output/page.png");
    }
}
```

Συγκεντρώστε και τρέξτε (`dotnet run`), μετά ελέγξτε τον φάκελο `output`. Μόλις **rendered a webpage to image**, καταγράψατε ένα screenshot και αποθηκεύσατε το HTML ως PNG — όλα χάρη σε έναν τακτοποιημένο **custom resource handler**.

## Συμπέρασμα

Δημιουργήσαμε έναν **custom resource handler**, ρυθμίσαμε τις επιλογές απόδοσης και χρησιμοποιήσαμε έναν `ImageRenderer` για **render webpage to image**. Το αποτέλεσμα είναι ένα καθαρό PNG συν ένα πλήρες σύνολο πόρων, δίνοντάς σας ό,τι χρειάζεστε για **capture webpage screenshot**, **render html to png**, και **save webpage as png** για αναφορές, μικρογραφίες ή αυτοματοποιημένες δοκιμές.

Τι ακολουθεί; Δοκιμάστε:

- Διαφορετικά μεγέθη viewport για κινητά vs. desktop screenshots
- Προσθήκη υδατογραφήματος ή επικάλυψης μετά την απόδοση
- Εξαγωγή σε άλλες μορφές (JPEG, BMP) τροποποιώντας το `ImageRenderingOptions`

Αφήστε ένα σχόλιο αν συναντήσετε πρόβλημα ή ανακαλύψετε έξυπνη βελτίωση. Καλό coding, και οι λήψεις σας να είναι πάντα pixel‑perfect!

## Σχετικά Tutorials

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Create HTML from String in C# – Custom Resource Handler Guide](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [How to Render HTML as PNG – Complete C# Guide](/html/english/net/rendering-html-documents/how-to-render-html-as-png-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
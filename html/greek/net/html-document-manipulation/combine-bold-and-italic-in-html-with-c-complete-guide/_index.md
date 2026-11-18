---
category: general
date: 2026-04-01
description: Συνδυάστε έντονη και πλάγια γραφή σε HTML χρησιμοποιώντας C#. Μάθετε
  πώς να τροποποιήσετε το στυλ γραμματοσειράς σε HTML, να αποθηκεύσετε το τροποποιημένο
  HTML και να αλλάξετε το στυλ γραμματοσειράς με C# σε λίγα εύκολα βήματα.
draft: false
keywords:
- combine bold and italic
- save modified html
- modify html font style
- change font style c#
language: el
og_description: Συνδυάστε έντονη και πλάγια γραφή σε HTML χρησιμοποιώντας C#. Αυτός
  ο οδηγός δείχνει πώς να τροποποιήσετε το στυλ γραμματοσειράς σε HTML, να αποθηκεύσετε
  το τροποποιημένο HTML και να αλλάξετε γρήγορα το στυλ γραμματοσειράς με C#.
og_title: Συνδυάστε έντονη και πλάγια γραφή σε HTML με C# – Βήμα‑προς‑βήμα
tags:
- C#
- Aspose.Html
- HTML manipulation
title: Συνδυάστε έντονη και πλάγια γραφή σε HTML με C# – Πλήρης οδηγός
url: /el/net/html-document-manipulation/combine-bold-and-italic-in-html-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Συνδυασμός έντονου και πλάγιου σε HTML με C# – Πλήρης Οδηγός

Έχετε χρειαστεί ποτέ να **συνδυάσετε έντονο και πλάγιο** σε ένα απόσπασμα HTML αλλά δεν ήξερες πώς να το κάνεις προγραμματιστικά; Δεν είστε ο μόνος—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν δημιουργούν δυναμικά email ή αναφορές. Τα καλά νέα είναι ότι με λίγες γραμμές C# και τη βιβλιοθήκη Aspose.HTML μπορείτε να εφαρμόσετε ένα συνδυασμένο στυλ γραμματοσειράς έντονο‑και‑πλάγιο σε οποιοδήποτε έγγραφο και στη συνέχεια **αποθηκεύσετε τροποποιημένο HTML** για μελλοντική χρήση.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: φόρτωση ενός μικρού αποσπάσματος HTML, **τροποποίηση στυλ γραμματοσειράς HTML**, εφαρμογή του εφέ **συνδυασμού έντονου και πλάγιου**, και τέλος **αποθήκευση του τροποποιημένου HTML** στο δίσκο. Στο τέλος θα γνωρίζετε ακριβώς πώς να **αλλάξετε το στυλ γραμματοσειράς με C#** χωρίς να σκάβετε μέσα σε ασαφή τεκμηρίωση.

## Τι Θα Χρειαστείτε

- .NET 6 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Core)  
- Aspose.HTML for .NET – μπορείτε να το αποκτήσετε από το NuGet (`Install-Package Aspose.HTML`)  
- Ένας επεξεργαστής κειμένου ή IDE (Visual Studio, VS Code, Rider—ό,τι προτιμάτε)  

Δεν υπάρχουν άλλες εξαρτήσεις. Αν έχετε ήδη ένα έργο, απλώς προσθέστε το πακέτο NuGet και είστε έτοιμοι.

![Στιγμιότυπο οθόνης που δείχνει κείμενο με έντονο και πλάγιο συνδυασμό σε πρόγραμμα περιήγησης – συνδυασμός έντονου και πλάγιου](https://example.com/combine-bold-italic.png)

*Κείμενο εναλλακτικής εικόνας: συνδυασμός έντονου και πλάγιου*

## Βήμα 1: Φόρτωση του αποσπάσματος HTML και δημιουργία εγγράφου

Πρώτα χρειάζεται ένα αντικείμενο `Aspose.Html.Document` που αντιπροσωπεύει το HTML με το οποίο θέλουμε να δουλέψουμε. Το παρακάτω απόσπασμα φορτώνει ένα μικρό τμήμα που περιέχει ετικέτες `<b>` και `<i>`.

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;

// The raw HTML we’ll transform
string htmlContent = "<html><body><b>Bold</b> <i>Italic</i></body></html>";

// Create a Document instance from the string
Document document = new Document(htmlContent);
```

**Γιατί είναι σημαντικό:**  
Η δημιουργία ενός `Document` σας παρέχει ένα πλήρες μοντέλο παρόμοιο με το DOM, ώστε να μπορείτε να χειρίζεστε τα στυλ ακριβώς όπως θα έκανε ένας περιηγητής. Επίσης προετοιμάζει το αντικείμενο για μελλοντική αποθήκευση, κάτι που είναι απαραίτητο όταν θέλετε να **αποθηκεύσετε τροποποιημένο HTML**.

## Βήμα 2: Συνδυασμός έντονου και πλάγιου στυλ γραμματοσειράς

Τώρα έρχεται η καρδιά του tutorial—εφαρμογή ενός στυλ που είναι ταυτόχρονα έντονο **και** πλάγιο. Η Aspose.HTML εκθέτει την απαρίθμηση `WebFontStyle`, και το μέλος `BoldItalic` είναι συντομογραφία για `FontStyle.Bold | FontStyle.Italic`.

```csharp
// Retrieve the default viewport style (covers the whole document)
var defaultStyle = document.DefaultViewPort.Style;

// Apply the combined bold‑and‑italic style
defaultStyle.FontStyle = WebFontStyle.BoldItalic; // same as FontStyle.Bold | FontStyle.Italic
```

**Εξήγηση:**  
`DefaultViewPort.Style` είναι ο παγκόσμιος κανόνας CSS που επηρεάζει κάθε στοιχείο εκτός αν παρακαμφθεί. Ορίζοντας το `FontStyle` σε `BoldItalic` διασφαλίζουμε ότι η **τροποποίηση στυλ γραμματοσειράς HTML** εφαρμόζεται ομοιόμορφα, εξαλείφοντας την ανάγκη να επεξεργαστούμε κάθε ετικέτα `<b>` ή `<i>` ξεχωριστά.

> *Συμβουλή:* Αν θέλετε μόνο ορισμένα στοιχεία να είναι έντονα‑και‑πλάγια, κάντε ερώτηση με `document.QuerySelectorAll("p.special")` και ορίστε το στυλ σε κάθε κόμβο αντί για το παγκόσμιο viewport.

## Βήμα 3: Επαλήθευση της αλλαγής (Προαιρετικό αλλά χρήσιμο)

Πριν γράψουμε κάτι στο δίσκο, είναι καλή ιδέα να ρίξουμε μια ματιά στο παραγόμενο markup. Μπορείτε να εκτυπώσετε το HTML στην κονσόλα ή σε παράθυρο εντοπισμού σφαλμάτων:

```csharp
// Output the transformed HTML for quick verification
string transformedHtml = document.ToString();
Console.WriteLine(transformedHtml);
```

Θα πρέπει να δείτε ένα μπλοκ `<style>` που έχει ενσωματωθεί στο `<head>` και αναγκάζει όλο το σώμα να αποδίδει με `font-weight: bold; font-style: italic;`. Αυτό επιβεβαιώνει ότι η λειτουργία **συνδυασμού έντονου και πλάγιου** ολοκληρώθηκε με επιτυχία.

## Βήμα 4: Αποθήκευση τροποποιημένου HTML

Τέλος, αποθηκεύουμε το ενημερωμένο έγγραφο. Η μέθοδος `Save` γράφει αυτόματα ένα καλά δομημένο αρχείο HTML, διατηρώντας τυχόν εξωτερικούς πόρους που μπορεί να έχετε προσθέσει.

```csharp
// Choose an output path that makes sense for your project
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.html");

// Save the document – this is the “save modified html” step
document.Save(outputPath);
Console.WriteLine($"Modified HTML saved to: {outputPath}");
```

**Τι λαμβάνετε:**  
Ένα αρχείο `output.html` που, όταν ανοίξει σε οποιονδήποτε περιηγητή, εμφανίζει το αρχικό κείμενο **και έντονα και πλάγια**. Αυτό είναι το συγκεκριμένο αποτέλεσμα της **αλλαγής στυλ γραμματοσειράς με C#** χρησιμοποιώντας Aspose.HTML.

## Βήμα 5: Συνηθισμένες παραλλαγές & ειδικές περιπτώσεις

### α) Στόχευση μόνο συγκεκριμένων στοιχείων

Αν χρειάζεστε να **τροποποιήσετε στυλ γραμματοσειράς HTML** μόνο για ένα υποσύνολο—π.χ., όλες τις παραγράφους με κλάση `highlight`—χρησιμοποιήστε έναν επιλογέα:

```csharp
var highlights = document.QuerySelectorAll("p.highlight");
foreach (var node in highlights)
{
    node.Style.FontStyle = WebFontStyle.BoldItalic;
}
```

### β) Διατήρηση των αρχικών ετικετών `<b>` / `<i>`

Μερικές φορές θέλετε να διατηρήσετε τις αρχικές ετικέτες για σημασιολογικούς λόγους αλλά να εφαρμόσετε το συνδυασμένο στυλ. Σε αυτήν την περίπτωση, προσθέστε μια κλάση CSS αντί να παρακάμψετε το παγκόσμιο στυλ:

```csharp
// Add a CSS class to the head
var style = document.CreateElement("style");
style.InnerHtml = ".bold-italic { font-weight: bold; font-style: italic; }";
document.Head.AppendChild(style);

// Apply the class to the body (or any element you like)
document.Body.ClassName = "bold-italic";
```

### γ) Αποθήκευση σε διαφορετική κωδικοποίηση

Η Aspose.HTML προεπιλογή είναι UTF‑8, αλλά μπορείτε να ορίσετε άλλη κωδικοποίηση αν το σύστημα σας την απαιτεί:

```csharp
var saveOptions = new HtmlSaveOptions()
{
    Encoding = System.Text.Encoding.ASCII // or any other Encoding
};
document.Save("output-ascii.html", saveOptions);
```

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα μαζί, εδώ είναι ένα αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε μια εφαρμογή κονσόλας:

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the HTML snippet
        string htmlContent = "<html><body><b>Bold</b> <i>Italic</i></body></html>";
        Document document = new Document(htmlContent);

        // 2️⃣ Apply combined bold‑and‑italic style
        var defaultStyle = document.DefaultViewPort.Style;
        defaultStyle.FontStyle = WebFontStyle.BoldItalic; // combine bold and italic

        // 3️⃣ (Optional) Verify by printing to console
        Console.WriteLine("Transformed HTML:");
        Console.WriteLine(document.ToString());

        // 4️⃣ Save the modified HTML
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.html");
        document.Save(outputPath);
        Console.WriteLine($"✅ Modified HTML saved to: {outputPath}");
    }
}
```

**Αναμενόμενη έξοδος:**  
Όταν ανοίξετε το `output.html` σε έναν περιηγητή, θα δείτε τις λέξεις “Bold Italic” εμφανιζόμενες **και έντονα και πλάγια**. Η κονσόλα θα εμφανίσει επίσης το παραγόμενο HTML, δείχνοντας μια ετικέτα `<style>` που επιβάλλει το συνδυασμένο στυλ.

## Συμπέρασμα

Τώρα ξέρετε πώς να **συνδυάσετε έντονο και πλάγιο** σε ένα έγγραφο HTML χρησιμοποιώντας C#. Φορτώνοντας το HTML σε ένα `Aspose.Html.Document`, ορίζοντας `WebFontStyle.BoldItalic` στο προεπιλεγμένο viewport, και στη συνέχεια **αποθηκεύοντας το τροποποιημένο HTML**, έχετε μια καθαρή, επαναλαμβανόμενη λύση για οποιαδήποτε εργασία αυτοματοποίησης. Είτε χρειάζεστε να **τροποποιήσετε στυλ γραμματοσειράς HTML** παγκοσμίως, να στοχεύσετε συγκεκριμένους κόμβους, είτε να **αλλάξετε το στυλ γραμματοσειράς με C#** για ένα πρότυπο web‑mail, οι ίδιες αρχές ισχύουν.

Τι ακολουθεί; Δοκιμάστε να πειραματιστείτε με άλλες τιμές του `WebFontStyle`—`Underline`, `StrikeThrough`, ή ακόμη και προσαρμοσμένες κλάσεις CSS—για να επεκτείνετε το εργαλείο στυλ σας. Μπορείτε επίσης να εξερευνήσετε τις δυνατότητες διαχείρισης εικόνων ή μετατροπής PDF της Aspose.HTML για να μετατρέψετε το ίδιο μορφοποιημένο έγγραφο σε PDF άμεσα.

Έχετε ερωτήσεις ή μια δύσκολη περίπτωση; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
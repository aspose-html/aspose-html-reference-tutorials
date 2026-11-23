---
category: general
date: 2026-07-05
description: 'Δημιουργήστε γρήγορα έγγραφο HTML σε C#: φορτώστε τη συμβολοσειρά HTML,
  αποκτήστε το στοιχείο κατά ID, ορίστε το στυλ γραμματοσειράς και τροποποιήστε το
  στυλ παραγράφου με ένα βήμα‑βήμα παράδειγμα.'
draft: false
keywords:
- create html document
- load html string
- get element by id
- set font style
- modify paragraph style
language: el
og_description: Δημιουργήστε έγγραφο HTML σε C# και μάθετε πώς να φορτώνετε μια συμβολοσειρά
  HTML, να λαμβάνετε στοιχείο κατά ID, να ορίζετε το στυλ γραμματοσειράς και να τροποποιείτε
  το στυλ παραγράφου σε ένα ενιαίο σεμινάριο.
og_title: Δημιουργία εγγράφου HTML σε C# – Οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: 'Create HTML document in C# quickly: load HTML string, get element
    by ID, set font style, and modify paragraph style with a step‑by‑step example.'
  headline: Create HTML Document in C# – Complete Programming Guide
  type: TechArticle
tags:
- C#
- HTML parsing
- DOM manipulation
- Styling
title: Δημιουργία εγγράφου HTML σε C# – Πλήρης οδηγός προγραμματισμού
url: /el/net/html-document-manipulation/create-html-document-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Εγγράφου HTML σε C# – Πλήρης Οδηγός Προγραμματισμού

Έχετε ποτέ χρειαστεί να **create html document** σε C# αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε μόνοι· πολλοί προγραμματιστές αντιμετωπίζουν αυτό το εμπόδιο όταν προσπαθούν για πρώτη φορά να χειριστούν HTML στην πλευρά του διακομιστή. Σε αυτόν τον οδηγό θα δούμε πώς να **load html string**, να εντοπίσουμε έναν κόμβο με **get element by id**, και στη συνέχεια να **set font style** ή να **modify paragraph style** χωρίς να ενσωματώσουμε μια βαριά μηχανή προγράμματος περιήγησης.

Στο τέλος του σεμιναρίου θα έχετε ένα έτοιμο προς εκτέλεση απόσπασμα κώδικα που δημιουργεί ένα έγγραφο HTML, ενσωματώνει περιεχόμενο και μορφοποιεί μια παράγραφο — όλα χρησιμοποιώντας καθαρό κώδικα C#. Χωρίς εξωτερικό UI, χωρίς JavaScript, μόνο καθαρή, δοκιμαστέα λογική.

## Τι Θα Μάθετε

- Πώς να δημιουργήσετε αντικείμενα **create html document** με την κλάση `HtmlDocument`.  
- Ο πιο απλός τρόπος για να **load html string** σε αυτό το έγγραφο.  
- Χρήση του **get element by id** για ασφαλή λήψη ενός μοναδικού κόμβου.  
- Εφαρμογή σημαιών **set font style** (bold, italic, underline) σε μια παράγραφο.  
- Επέκταση του παραδείγματος για **modify paragraph style** χρωμάτων, περιθωρίων κ.ά.  

**Prerequisites** – Θα πρέπει να έχετε εγκατεστημένο το .NET 6+, βασική εξοικείωση με τη C#, και το πακέτο NuGet `HtmlAgilityPack` (η de‑facto βιβλιοθήκη για ανάλυση HTML στην πλευρά του διακομιστή). Αν δεν έχετε προσθέσει ποτέ ένα πακέτο NuGet, απλώς εκτελέστε `dotnet add package HtmlAgilityPack` στο φάκελο του έργου σας.

---

## Δημιουργία Εγγράφου HTML και Φόρτωση HTML String

Το πρώτο βήμα είναι να **create html document** και να το τροφοδοτήσετε με ακατέργαστο markup. Σκεφτείτε το `HtmlDocument` ως ένα κενό καμβά· η μέθοδος `LoadHtml` ζωγραφίζει τη συμβολοσειρά σας πάνω του.

```csharp
using System;
using HtmlAgilityPack;   // NuGet: HtmlAgilityPack

class Program
{
    static void Main()
    {
        // Step 1: Instantiate a new HtmlDocument (create html document)
        var doc = new HtmlDocument();

        // Step 2: Load a simple HTML string (load html string)
        string rawHtml = @"<html><body><p id='txt'>Sample text</p></body></html>";
        doc.LoadHtml(rawHtml);
        
        // The rest of the tutorial continues below...
    }
}
```

Γιατί να χρησιμοποιήσετε το `LoadHtml` αντί για το `doc.Open`; Η μέθοδος `Open` είναι ένας παλιός wrapper που υπάρχει μόνο σε παλαιότερα forks· το `LoadHtml` είναι η σύγχρονη, thread‑safe εναλλακτική και λειτουργεί σε .NET Core και .NET Framework εξίσου.  

> **Pro tip:** Αν σκοπεύετε να φορτώσετε μεγάλα αρχεία, σκεφτείτε το `doc.Load(path)` που μεταφέρει τα δεδομένα από το δίσκο αντί να κρατά όλη τη συμβολοσειρά στη μνήμη.

---

## Λήψη Στοιχείου κατά ID

Τώρα που το έγγραφο βρίσκεται στη μνήμη, πρέπει να **get element by id**. Αυτό αντικατοπτρίζει την κλήση JavaScript `document.getElementById` που πιθανώς γνωρίζετε, αλλά συμβαίνει στον διακομιστή.

```csharp
// Step 3: Retrieve the paragraph element by its ID (get element by id)
var paragraph = doc.GetElementbyId("txt");

// Defensive check – always verify the node exists before touching it.
if (paragraph == null)
{
    Console.WriteLine("Element with ID 'txt' not found.");
    return;
}
```

Η μέθοδος `GetElementbyId` διασχίζει το δέντρο DOM μία φορά, οπότε είναι αποδοτική ακόμη και για μεγάλα έγγραφα. Αν χρειάζεται να στοχεύσετε πολλαπλά στοιχεία, το `SelectNodes("//p[@class='myClass']")` είναι η εναλλακτική XPath.

---

## Ορισμός Στυλ Γραμματοσειράς στην Παράγραφο

Με τον κόμβο στα χέρια, μπορούμε να **set font style**. Η κλάση `HtmlNode` δεν εκθέτει μια ειδική ιδιότητα `FontStyle`, αλλά μπορούμε να χειριστούμε άμεσα το χαρακτηριστικό `style`. Για το σκοπό αυτού του οδηγού, θα προσομοιώσουμε ένα enum τύπου `WebFontStyle` για να διατηρήσουμε τον κώδικα καθαρό.

```csharp
// Step 4: Define a simple flag enum for font styles
[Flags]
enum WebFontStyle
{
    None    = 0,
    Bold    = 1 << 0,
    Italic  = 1 << 1,
    Underline = 1 << 2
}

// Helper to translate flags into CSS
static string FontStyleToCss(WebFontStyle style)
{
    var parts = new System.Collections.Generic.List<string>();
    if (style.HasFlag(WebFontStyle.Bold)) parts.Add("font-weight: bold");
    if (style.HasFlag(WebFontStyle.Italic)) parts.Add("font-style: italic");
    if (style.HasFlag(WebFontStyle.Underline)) parts.Add("text-decoration: underline");
    return string.Join("; ", parts);
}

// Apply combined bold & italic style (set font style)
WebFontStyle combined = WebFontStyle.Bold | WebFontStyle.Italic;
string css = FontStyleToCss(combined);
paragraph.SetAttributeValue("style", css);
```

Τι συνέβη μόλις; Δημιουργήσαμε ένα μικρό enum, μετατρέψαμε τις επιλεγμένες σημαίες σε μια συμβολοσειρά CSS, και τοποθετήσαμε αυτή τη συμβολοσειρά στο χαρακτηριστικό `style` του στοιχείου `<p>`. Το αποτέλεσμα είναι μια παράγραφος που εμφανίζει **bold and italic** όταν το HTML τελικά εμφανιστεί.

**Why use flags?** Οι σημαίες σας επιτρέπουν να συνδυάσετε στυλ χωρίς να ενσωματώνετε πολλαπλές δηλώσεις `if`, και ταιριάζουν άψογα με το CSS όπου πολλές δηλώσεις χωρίζονται με ερωτηματικά.

---

## Τροποποίηση Στυλ Παραγράφου – Προχωρημένες Ρυθμίσεις

Η μορφοποίηση δεν σταματά στο bold ή italic. Ας **modify paragraph style** περαιτέρω προσθέτοντας χρώμα και line‑height. Αυτό δείχνει πώς μπορείτε να επεκτείνετε τη συμβολοσειρά CSS χωρίς να αντικαθιστάτε τις προηγούμενες τιμές.

```csharp
// Retrieve any existing style attribute (might be empty)
string existingStyle = paragraph.GetAttributeValue("style", "");

// Append extra rules – note the trailing semicolon for safety
string extraCss = "color: #2A7AE2; line-height: 1.6";
string combinedStyle = string.IsNullOrWhiteSpace(existingStyle)
    ? extraCss
    : $"{existingStyle}; {extraCss}";

paragraph.SetAttributeValue("style", combinedStyle);
```

Τώρα η παράγραφος θα εμφανίζεται σε ήρεμο μπλε χρώμα με άνετο διάστημα γραμμής.  

> **Watch out for:** διπλότυπες ιδιότητες CSS. Αν αργότερα ορίσετε ξανά το `font-weight`, η τελευταία εμφάνιση κερδίζει στα περισσότερα προγράμματα περιήγησης, αλλά μπορεί να δυσκολέψει τον εντοπισμό σφαλμάτων. Μια καθαρή προσέγγιση είναι να δημιουργήσετε ένα `Dictionary<string,string>` με δηλώσεις CSS και να το σειριοποιήσετε στο τέλος.

---

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα, εδώ είναι ένα **complete, runnable program** που δημιουργεί ένα έγγραφο HTML, φορτώνει μια συμβολοσειρά, ανακτά έναν κόμβο κατά ID και το μορφοποιεί.

```csharp
using System;
using HtmlAgilityPack;

[Flags]
enum WebFontStyle
{
    None      = 0,
    Bold      = 1 << 0,
    Italic    = 1 << 1,
    Underline = 1 << 2
}

class Program
{
    static void Main()
    {
        // 1️⃣ Create HTML document
        var doc = new HtmlDocument();

        // 2️⃣ Load HTML string
        string rawHtml = @"<html><body><p id='txt'>Sample text</p></body></html>";
        doc.LoadHtml(rawHtml);

        // 3️⃣ Get element by ID
        var paragraph = doc.GetElementbyId("txt");
        if (paragraph == null)
        {
            Console.WriteLine("Paragraph not found.");
            return;
        }

        // 4️⃣ Set font style (bold + italic)
        WebFontStyle styleFlags = WebFontStyle.Bold | WebFontStyle.Italic;
        string css = FontStyleToCss(styleFlags);
        paragraph.SetAttributeValue("style", css);

        // 5️⃣ Modify paragraph style – add color & line‑height
        string extraCss = "color: #2A7AE2; line-height: 1.6";
        string combinedStyle = $"{css}; {extraCss}";
        paragraph.SetAttributeValue("style", combinedStyle);

        // 6️⃣ Output the final HTML
        string finalHtml = doc.DocumentNode.OuterHtml;
        Console.WriteLine("=== Final HTML ===");
        Console.WriteLine(finalHtml);
    }

    static string FontStyleToCss(WebFontStyle style)
    {
        var parts = new System.Collections.Generic.List<string>();
        if (style.HasFlag(WebFontStyle.Bold)) parts.Add("font-weight: bold");
        if (style.HasFlag(WebFontStyle.Italic)) parts.Add("font-style: italic");
        if (style.HasFlag(WebFontStyle.Underline)) parts.Add("text-decoration: underline");
        return string.Join("; ", parts);
    }
}
```

### Αναμενόμενη Έξοδος

Η εκτέλεση του προγράμματος εκτυπώνει:

```
=== Final HTML ===
<html><body><p id="txt" style="font-weight: bold; font-style: italic; color: #2A7AE2; line-height: 1.6">Sample text</p></body></html>
```

Αν τοποθετήσετε το παραγόμενο HTML σε οποιοδήποτε πρόγραμμα περιήγησης, η παράγραφος θα διαβάζει “Sample text” σε bold‑italic μπλε με άνετο line height.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

**What if the HTML string is malformed?**  
`HtmlAgilityPack` είναι επιεικής· θα προσπαθήσει να διορθώσει τα ελλιπή κλεισίματα ετικετών. Παρόλα αυτά, πάντα να επικυρώνετε την είσοδο αν χειρίζεστε περιεχόμενο που παράγεται από χρήστες για να αποφύγετε επιθέσεις XSS.

**Can I load an entire file instead of a string?**  
Ναι—χρησιμοποιήστε `doc.Load("path/to/file.html")`. Οι ίδιες μέθοδοι DOM (`GetElementbyId`, `SetAttributeValue`) λειτουργούν αμετάβλητες.

**How do I remove a style later?**  
Ανακτήστε το τρέχον χαρακτηριστικό `style`, χωρίστε το με `;`, φιλτράρετε τον κανόνα που δεν θέλετε, και ορίστε ξανά τη καθαρισμένη συμβολοσειρά.

**Is there a way to add multiple classes?**  
Βεβαίως—`paragraph.AddClass("highlight")` (μέθοδος επέκτασης) ή χειροκίνητα να τροποποιήσετε το χαρακτηριστικό `class`:  
`paragraph.SetAttributeValue("class", "highlight anotherClass");`

---

## Συμπέρασμα

Μόλις **created html document** σε C#, **loaded html string**, χρησιμοποιήσαμε **get element by id**, και δείξαμε πώς να **set font style** και **modify paragraph style** με σύντομο, ιδιωματικό κώδικα. Η προσέγγιση λειτουργεί για οποιοδήποτε μέγεθος HTML, από μικρά αποσπάσματα μέχρι πλήρη πρότυπα, και παραμένει εντελώς στην πλευρά του διακομιστή — ιδανική για δημιουργία email, απόδοση PDF ή οποιοδήποτε αυτοματοποιημένο pipeline αναφορών.

Τι ακολουθεί; Δοκιμάστε να αντικαταστήσετε το inline CSS με ένα

## Τι Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω σεμινάρια καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Δημιουργία HTML από Σειρά σε C# – Οδηγός Προσαρμοσμένου Διαχειριστή Πόρων](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Δημιουργία Εγγράφου HTML με Στυλιζαμένο Κείμενο και Εξαγωγή σε PDF – Πλήρης Οδηγός](/html/english/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/)
- [Δημιουργία PDF από HTML – Οδηγός C# Βήμα‑Βήμα](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
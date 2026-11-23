---
category: general
date: 2026-06-04
description: Αποκτήστε κείμενο από EPUB γρήγορα και μάθετε πώς να διαβάζετε αρχεία
  EPUB, να μετατρέπετε το EPUB σε κείμενο και να εξάγετε κεφάλαια χρησιμοποιώντας
  Python.
draft: false
keywords:
- get text from epub
- convert epub to text
- how to read epub
language: el
og_description: Αποκτήστε κείμενο από EPUB με Python σε λίγα λεπτά. Αυτό το σεμινάριο
  δείχνει πώς να διαβάζετε αρχεία EPUB, να μετατρέπετε το EPUB σε κείμενο και να αντιμετωπίζετε
  κοινές περιπτώσεις άκρων.
og_title: Αποκτήστε κείμενο από EPUB με Python – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-04'
  description: Get text from EPUB quickly and learn how to read EPUB files, convert
    EPUB to text, and extract chapters using Python.
  headline: Get Text from EPUB in Python – Complete Guide
  type: TechArticle
- description: Get text from EPUB quickly and learn how to read EPUB files, convert
    EPUB to text, and extract chapters using Python.
  name: Get Text from EPUB in Python – Complete Guide
  steps:
  - name: Import Libraries and Load the EPUB
    text: '```python from pathlib import Path from ebooklib import epub from bs4 import
      BeautifulSoup'
  - name: Grab the First Chapter (First <section> Element)
    text: '```python # Find the first HTML document inside the EPUB first_item = None
      for item in book.get_items(): if item.get_type() == epub.ITEM_DOCUMENT: first_item
      = item break'
  - name: Strip Tags and Output Plain Text
    text: '```python # .get_text() removes all HTML tags and returns clean text chapter_text
      = first_chapter.get_text(separator="

      ", strip=True)'
  - name: Full Script – Ready to Run
    text: '```python #!/usr/bin/env python3 """ Get text from EPUB – extract the first
      chapter and print it as plain text. """'
  type: HowTo
- questions:
  - answer: Not directly. `.mobi` uses a different container format. Convert it to
      EPUB first (Calibre does a solid job), then apply the same script.
    question: Can I use this with a .mobi file?
  - answer: The fallback to `<body>` (shown in the code) covers that case. You can
      also look for `<div class="chapter">` if the publisher uses custom markup.
    question: What if the EPUB has no `<section>` tags?
  - answer: 'No. Alternatives include `zipfile` + manual HTML parsing, or `pypub`
      for a higher‑level API. `ebooklib` is popular because it abstracts the ZIP handling
      and gives you item types out of the box. --- ## Conclusion You now know how
      to **get text from EPUB** files using Python, whether you need just the'
    question: Is `ebooklib` the only library?
  type: FAQPage
tags:
- python
- epub
- text‑extraction
title: Λήψη κειμένου από EPUB σε Python – Πλήρης οδηγός
url: /el/python/general/get-text-from-epub-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Απόκτηση Κειμένου από EPUB με Python – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να διαβάσετε αρχεία EPUB** χωρίς να ανοίξετε έναν βαριά αναγνώστη; Ίσως χρειάζεστε το πρώτο κεφάλαιο για ανάλυση, ή απλώς θέλετε να **μετατρέψετε EPUB σε κείμενο** για γρήγορη αναζήτηση. Ό,τι και αν είναι το σενάριό σας, βρίσκεστε στο σωστό μέρος. Σε αυτό το tutorial θα σας δείξουμε πώς να **αποκτήσετε κείμενο από EPUB** χρησιμοποιώντας λίγες γραμμές Python, και θα εξηγήσουμε το «γιατί» πίσω από κάθε βήμα ώστε να μπορείτε να προσαρμόσετε τη λύση σε οποιοδήποτε βιβλίο.

Θα περάσουμε από την εγκατάσταση της κατάλληλης βιβλιοθήκης, τη φόρτωση του EPUB, την εξαγωγή του πρώτου στοιχείου `<section>` και την εκτύπωση του καθαρού κειμένου. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο script που λειτουργεί σε οποιοδήποτε EPUB τοποθετήσετε σε έναν φάκελο.

## Προαπαιτούμενα

- Python 3.8+ (ο κώδικας χρησιμοποιεί f‑strings και pathlib)
- Ένα σύγχρονο IDE ή απλώς ένα τερματικό
- Τα πακέτα `ebooklib` και `beautifulsoup4` (εγκαταστήστε τα με `pip install ebooklib beautifulsoup4`)

Δεν απαιτούνται άλλα εξωτερικά εργαλεία, και το script τρέχει σε Windows, macOS και Linux.

---

## Απόκτηση Κειμένου από EPUB – Βήμα‑βήμα

Παρακάτω είναι η βασική λογική που κάνει ακριβώς αυτό που υπόσχεται ο τίτλος: **αποκτά κείμενο από EPUB** και εκτυπώνει το πρώτο κεφάλαιο. Θα το αναλύσουμε ώστε να καταλάβετε κάθε γραμμή.

### Βήμα 1: Εισαγωγή Βιβλιοθηκών και Φόρτωση του EPUB

```python
from pathlib import Path
from ebooklib import epub
from bs4 import BeautifulSoup

# Path to the .epub file – change this to your own location
EPUB_PATH = Path("YOUR_DIRECTORY/book.epub")

# Load the EPUB container
book = epub.read_epub(EPUB_PATH)
```

*Γιατί αυτό το βήμα;*  
`ebooklib` γνωρίζει τη δομή ZIP‑βασισμένων αρχείων EPUB, ενώ `BeautifulSoup` κάνει την ανάλυση του ενσωματωμένου HTML απλή. Η χρήση του `Path` κρατά τον κώδικα ανεξάρτητο από το λειτουργικό σύστημα.

### Βήμα 2: Λήψη του Πρώτου Κεφαλαίου (Πρώτο Στοιχείο <section>)

```python
# Find the first HTML document inside the EPUB
first_item = None
for item in book.get_items():
    if item.get_type() == epub.ITEM_DOCUMENT:
        first_item = item
        break

if not first_item:
    raise ValueError("No HTML content found in the EPUB.")

# Parse the HTML with BeautifulSoup
soup = BeautifulSoup(first_item.get_content(), "html.parser")

# Retrieve the first <section> element – this usually holds a chapter
first_chapter = soup.find("section")
if not first_chapter:
    # Fallback: use the first <body> if no <section> exists
    first_chapter = soup.body
```

*Γιατί αυτό το βήμα;*  
Τα EPUB αποθηκεύουν κάθε κεφάλαιο ως αρχείο HTML. Ο βρόχος σταματά στο πρώτο έγγραφο, που συχνά είναι το εξώφυλλο ή η εισαγωγή. Στοχεύοντας το πρώτο `<section>` κατευθυνόμαστε απευθείας στο πρώτο πραγματικό κεφάλαιο, αλλά παρέχουμε και εναλλακτική λύση στο στοιχείο `<body>` για βιβλία που δεν χρησιμοποιούν sections.

### Βήμα 3: Αφαίρεση Ετικετών και Έξοδος Καθαρού Κειμένου

```python
# .get_text() removes all HTML tags and returns clean text
chapter_text = first_chapter.get_text(separator="\n", strip=True)

print(chapter_text)
```

*Γιατί αυτό το βήμα;*  
`get_text()` είναι ο πιο απλός τρόπος για **μετατροπή EPUB σε κείμενο**. Το όρισμα `separator` εξασφαλίζει ότι κάθε στοιχείο μπλοκ ξεκινά σε νέα γραμμή, κάνοντας την έξοδο πιο ευανάγνωστη.

### Πλήρες Script – Έτοιμο για Εκτέλεση

```python
#!/usr/bin/env python3
"""
Get text from EPUB – extract the first chapter and print it as plain text.
"""

from pathlib import Path
from ebooklib import epub
from bs4 import BeautifulSoup

def extract_first_chapter(epub_path: Path) -> str:
    """Return the plain‑text of the first chapter in an EPUB file."""
    book = epub.read_epub(epub_path)

    # Locate the first HTML document
    first_item = next(
        (i for i in book.get_items() if i.get_type() == epub.ITEM_DOCUMENT),
        None,
    )
    if not first_item:
        raise ValueError("The EPUB does not contain any HTML documents.")

    soup = BeautifulSoup(first_item.get_content(), "html.parser")

    # Try to find a <section>; otherwise fall back to <body>
    chapter_tag = soup.find("section") or soup.body
    if not chapter_tag:
        raise ValueError("No readable content found in the first HTML document.")

    # Clean the text
    return chapter_tag.get_text(separator="\n", strip=True)


if __name__ == "__main__":
    # Replace with the actual path to your EPUB file
    EPUB_PATH = Path("YOUR_DIRECTORY/book.epub")
    try:
        text = extract_first_chapter(EPUB_PATH)
        print(text)
    except Exception as e:
        print(f"Error: {e}")
```

Αποθηκεύστε το ως `extract_epub.py` και τρέξτε `python extract_epub.py`. Αν όλα είναι ρυθμισμένα σωστά, θα δείτε το κείμενο του πρώτου κεφαλαίου στην κονσόλα.

![Στιγμιότυπο οθόνης της εξόδου τερματικού που δείχνει το εξαγόμενο κείμενο EPUB](get-text-from-epub.png "Get text from EPUB example output")

---

## Μετατροπή EPUB σε Κείμενο – Κλιμάκωση

Το παραπάνω απόσπασμα διαχειρίζεται ένα μόνο κεφάλαιο, αλλά τα περισσότερα έργα χρειάζονται ολόκληρο το βιβλίο ως ένα μεγάλο string. Εδώ είναι μια γρήγορη επέκταση που διατρέχει **όλα** τα έγγραφα, συνενώνει το καθαρισμένο κείμενο και το γράφει σε αρχείο `.txt`.

```python
def convert_epub_to_text(epub_path: Path, output_path: Path) -> None:
    """Convert an entire EPUB into a plain‑text file."""
    book = epub.read_epub(epub_path)
    all_text = []

    for item in book.get_items():
        if item.get_type() == epub.ITEM_DOCUMENT:
            soup = BeautifulSoup(item.get_content(), "html.parser")
            # Grab everything inside <body> – safe for most EPUBs
            body = soup.body
            if body:
                all_text.append(body.get_text(separator="\n", strip=True))

    output_path.write_text("\n\n".join(all_text), encoding="utf-8")
    print(f"✅ EPUB converted – saved to {output_path}")

# Example usage
if __name__ == "__main__":
    EPUB_PATH = Path("YOUR_DIRECTORY/book.epub")
    TXT_PATH = Path("YOUR_DIRECTORY/book.txt")
    convert_epub_to_text(EPUB_PATH, TXT_PATH)
```

**Pro tip:** Κάποια EPUB περιέχουν scripts ή style tags που μπορούν να μπερδέψουν το `BeautifulSoup`. Αν παρατηρήσετε άσχετους χαρακτήρες, προσθέστε `soup = BeautifulSoup(item.get_content(), "lxml")` και εγκαταστήστε το `lxml` για πιο αυστηρό parser.

---

## Πώς να Διαβάζετε Αρχεία EPUB Αποδοτικά – Συνηθισμένα Πιθανά Σφάλματα

1. **Απρόσμενα encoding** – Τα EPUB είναι αρχεία ZIP που περιέχουν HTML σε UTF‑8. Αν εμφανιστεί `UnicodeDecodeError`, εξαναγκάστε UTF‑8 κατά την ανάγνωση: `item.get_content().decode("utf-8", errors="ignore")`.
2. **Πολλαπλές γλώσσες** – Βιβλία με ανάμικτες γλώσσες μπορεί να έχουν ξεχωριστά `<section>` tags ανά γλώσσα. Χρησιμοποιήστε `soup.find_all("section")` και φιλτράρετε με το χαρακτηριστικό `lang` αν χρειάζεται.
3. **Εικόνες και υποσημειώσεις** – Το script αφαιρεί ετικέτες, επομένως το alt‑text των εικόνων χάνεται. Αν τα χρειάζεστε, εξάγετε τα `alt` attributes των `<img>` ή τα links των υποσημειώσεων `<a>` πριν τον καθαρισμό.
4. **Μεγάλα βιβλία** – Η αποθήκευση κάθε κεφαλαίου στη μνήμη μπορεί να εξαντλήσει το RAM. Γράψτε κάθε καθαρισμένο κεφάλαιο απευθείας σε αρχείο σε λειτουργία προσθήκης (append) για να παραμείνετε ελαφροί σε μνήμη.

---

## Συχνές Ερωτήσεις – Γρήγορες Απαντήσεις

**Ε: Μπορώ να το χρησιμοποιήσω με αρχείο .mobi;**  
Α: Όχι άμεσα. Το `.mobi` χρησιμοποιεί διαφορετική μορφή container. Μετατρέψτε το πρώτα σε EPUB (το Calibre κάνει καλή δουλειά), μετά εφαρμόστε το ίδιο script.

**Ε: Τι γίνεται αν το EPUB δεν έχει ετικέτες `<section>`;**  
Α: Η εναλλακτική λύση στο `<body>` (όπως φαίνεται στον κώδικα) καλύπτει αυτήν την περίπτωση. Μπορείτε επίσης να ψάξετε για `<div class="chapter">` αν ο εκδότη χρησιμοποιεί προσαρμοσμένο markup.

**Ε: Είναι το `ebooklib` η μόνη βιβλιοθήκη;**  
Α: Όχι. Εναλλακτικές είναι το `zipfile` + χειροκίνητη ανάλυση HTML, ή το `pypub` για πιο υψηλού επιπέδου API. Το `ebooklib` είναι δημοφιλές επειδή αφαιρεί τη διαχείριση ZIP και παρέχει τύπους αντικειμένων κατευθείαν.

---

## Συμπέρασμα

Τώρα ξέρετε πώς να **αποκτήσετε κείμενο από EPUB** με Python, είτε χρειάζεστε μόνο το πρώτο κεφάλαιο είτε ολόκληρο το βιβλίο. Το tutorial κάλυψε τα βασικά βήματα για **μετατροπή EPUB σε κείμενο**, εξήγησε τη λογική πίσω από κάθε γραμμή, και ανέδειξε περιπτώσεις που μπορεί να συναντήσετε.

Στη συνέχεια, δοκιμάστε να επεκτείνετε το script ώστε να εξάγει μεταδεδομένα (τίτλος, συγγραφέας) με `book.get_metadata('DC', 'title')`, ή πειραματιστείτε με μορφές εξόδου όπως Markdown ή JSON. Οι ίδιες αρχές ισχύουν, οπότε θα νιώσετε άνετα να αντιμετωπίσετε οποιαδήποτε παρόμοια πρόκληση ανάλυσης αρχείων.

Καλή κωδικοποίηση, και αφήστε ένα σχόλιο αν αντιμετωπίσετε δυσκολίες!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κυριαρχήσετε πρόσθετα χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [Πώς να Μετατρέψετε EPUB σε PDF με Java – Χρησιμοποιώντας Aspose.HTML](/html/english/java/converting-epub-to-pdf/convert-epub-to-pdf/)
- [Μετατροπή EPUB σε Εικόνες Χρησιμοποιώντας Aspose HTML for Java](/html/english/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)
- [Μετατροπή EPUB σε PDF και Εικόνες με Aspose.HTML for Java](/html/english/java/conversion-epub-to-image-and-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
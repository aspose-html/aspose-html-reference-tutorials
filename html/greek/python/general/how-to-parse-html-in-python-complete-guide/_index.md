---
category: general
date: 2026-05-28
description: Πώς να αναλύσετε HTML σε Python γρήγορα—φορτώστε το αρχείο HTML, χρησιμοποιήστε
  CSS selector και εξάγετε τα χαρακτηριστικά href με ένα παράδειγμα XPath contains.
draft: false
keywords:
- how to parse html
- get href attribute
- load html file
- use css selector
- xpath contains example
language: el
og_description: 'Πώς να αναλύσετε HTML σε Python: μάθετε πώς να φορτώνετε ένα αρχείο
  HTML, να χρησιμοποιείτε επιλεκτές CSS και να λαμβάνετε τα χαρακτηριστικά href με
  ένα παράδειγμα XPath contains.'
og_title: Πώς να Αναλύσετε HTML σε Python – Βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  headline: How to Parse HTML in Python – Complete Guide
  type: TechArticle
- description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  name: How to Parse HTML in Python – Complete Guide
  steps:
  - name: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
    text: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
  - name: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
    text: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
  - name: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
    text: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
  - name: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
    text: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
  type: HowTo
tags:
- html parsing
- python
- web scraping
title: Πώς να Αναλύσετε HTML σε Python – Πλήρης Οδηγός
url: /el/python/general/how-to-parse-html-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Αναλύσετε HTML σε Python – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να αναλύσετε HTML** σε ένα script Python χωρίς να φορτώσετε έναν βαρύ περιηγητή; Δεν είστε μόνοι. Οι περισσότεροι από εμάς χρειάζονται απλώς να **φορτώσουμε ένα αρχείο HTML**, να εξάγουμε μερικές επικεφαλίδες, και ίσως να πάρουμε ένα ή δύο συνδέσμους λήψης. Σε αυτό το tutorial θα σας δείξω ακριβώς αυτό—χρησιμοποιώντας μια μικρή βιβλιοθήκη, έναν CSS selector, και ένα παράδειγμα XPath contains για **να λάβετε τις τιμές του χαρακτηριστικού href**.

Θα περάσουμε από όλη τη διαδικασία, από την ανάγνωση ενός τοπικού εγγράφου HTML μέχρι την εκτύπωση των δεδομένων που σας ενδιαφέρουν. Χωρίς περιττά, μόνο ένα πρακτικό, εκτελέσιμο παράδειγμα που μπορείτε να ενσωματώσετε στο δικό σας project σήμερα.

## Τι Θα Μάθετε

- Πώς να **φορτώσετε ένα αρχείο HTML** με έναν ελαφρύ parser.
- Πώς να **χρησιμοποιήσετε σύνταξη CSS selector** για να ανακτήσετε στοιχεία όπως επικεφαλίδες άρθρων.
- Πώς να δημιουργήσετε ένα **παράδειγμα XPath contains** που φιλτράρει συνδέσμους.
- Πώς να εξάγετε με ασφάλεια τις **τιμές του χαρακτηριστικού href** από τους ταιριασμένους κόμβους.
- Συμβουλές για τη διαχείριση κακής δομής markup και την επέκταση του script.

Απαιτούνται μόνο Python 3.8+ και τα πακέτα `lxml` και `cssselect`—και τα δύο εγκαθίστανται με μία μόνο εντολή `pip`.

---

## Βήμα 1: Φορτώστε το Αρχείο HTML

Πριν κάνετε οτιδήποτε άλλο, χρειάζεστε το περιεχόμενο HTML στη μνήμη. Η μονάδα `lxml.html` παρέχει έναν βολικό βοηθό `fromstring`, αλλά όταν έχετε ένα αρχείο στο δίσκο η συνάρτηση `parse` είναι ακόμη πιο καθαρή.

```python
# Step 1: Load the HTML file
from lxml import html

# Replace the path with the location of your HTML document
html_path = "YOUR_DIRECTORY/news.html"
doc = html.parse(html_path)

# The root element gives us access to CSS and XPath methods
root = doc.getroot()
```

> **Γιατί είναι σημαντικό:** Η φόρτωση του αρχείου μία φορά κρατά τη χρήση μνήμης χαμηλή και σας δίνει ένα μοναδικό αντικείμενο `root` που υποστηρίζει τόσο CSS selectors όσο και ερωτήματα XPath. Αν το αρχείο λείπει ή δεν μπορεί να διαβαστεί, το `html.parse` θα ρίξει ένα σαφές `OSError`, το οποίο μπορείτε να πιάσετε αργότερα.

### Pro tip
Αν εργάζεστε με μια συμβολοσειρά αντί για αρχείο, αντικαταστήστε το `html.parse` με `html.fromstring(your_html_string)`.

---

## Βήμα 2: Χρησιμοποιήστε CSS Selector για να Πάρτε τις Επικεφαλίδες

Οι CSS selectors είναι σύντομοι και γνωστοί σε όποιον έχει γράψει stylesheet. Ας πάρουμε κάθε `<h2>` μέσα σε ένα `<article>`—ιδανικό για επικεφαλίδες ειδήσεων.

```python
# Step 2: Find all article headlines using a CSS selector
headline_nodes = root.cssselect("article h2")

# Print each headline's text content
for node in headline_nodes:
    print(node.text_content().strip())
```

**Αναμενόμενη έξοδος** (υποθέτοντας ότι το δείγμα HTML περιέχει δύο άρθρα):

```
Breaking News: Python Takes Over the World
Local Developer Solves HTML Parsing Puzzle
```

> **Γιατί CSS;** Είναι αναγνώσιμο, γρήγορο, και λειτουργεί αμέσως με το `lxml`. Η μέθοδος `cssselect` μετατρέπει τον selector σε έκφραση XPath στο παρασκήνιο, προσφέροντας το καλύτερο και από τα δύο.

---

## Βήμα 3: Παράδειγμα XPath Contains – Βρείτε Συνδέσμους “download”

Μερικές φορές χρειάζεστε πιο λεπτομερή έλεγχο από ό,τι προσφέρει το CSS. Η συνάρτηση `contains()` του XPath ξεχωρίζει όταν θέλετε να ταιριάξετε ένα υποσυμβολοσειρά μέσα σε ένα χαρακτηριστικό, όπως όλοι οι σύνδεσμοι που οδηγούν σε λήψη.

```python
# Step 3: Find all links that contain the word "download" using XPath
download_link_nodes = root.xpath("//a[contains(@href, 'download')]")

# Extract and print the href attribute from each matching node
for node in download_link_nodes:
    href = node.get("href")
    print(href)
```

**Δείγμα εξόδου**:

```
/files/report_download.pdf
https://example.com/downloads/setup.exe
```

> **Γιατί XPath contains;** Σας επιτρέπει να φιλτράρετε απευθείας βάσει τιμών χαρακτηριστικών χωρίς επιπλέον βρόχους Python. Αυτό είναι το κλασικό **xpath contains example** που συχνά βλέπετε σε tutorials, αλλά εδώ συνδυάζεται με μια πραγματική περίπτωση χρήσης.

---

## Βήμα 4: Συσκευάστε Όλα σε Μια Επαναχρησιμοποιήσιμη Συνάρτηση

Η σκληρή κωδικοποίηση διαδρομών και εκτυπώσεων είναι αποδεκτή για γρήγορο τεστ, αλλά ο κώδικας παραγωγής προτιμά συναρτήσεις. Παρακάτω υπάρχει ένας σύντομος βοηθός που επιστρέφει τόσο τις επικεφαλίδες όσο και τους συνδέσμους λήψης.

```python
def parse_news_html(file_path):
    """
    Parse a news HTML file and return headlines plus download URLs.

    Parameters
    ----------
    file_path : str
        Path to the local HTML document.

    Returns
    -------
    dict
        {
            "headlines": list of strings,
            "download_links": list of href strings
        }
    """
    doc = html.parse(file_path)
    root = doc.getroot()

    # Headlines via CSS selector
    headlines = [
        node.text_content().strip()
        for node in root.cssselect("article h2")
    ]

    # Download links via XPath contains
    download_links = [
        node.get("href")
        for node in root.xpath("//a[contains(@href, 'download')]")
    ]

    return {"headlines": headlines, "download_links": download_links}
```

Τώρα μπορείτε να καλέσετε τη συνάρτηση και να εμφανίσετε τα αποτελέσματα όμορφα:

```python
if __name__ == "__main__":
    results = parse_news_html("YOUR_DIRECTORY/news.html")
    print("Headlines:")
    for h in results["headlines"]:
        print(f"- {h}")

    print("\nDownload Links:")
    for link in results["download_links"]:
        print(f"- {link}")
```

Η εκτέλεση του script δίνει την ίδια έξοδο όπως πριν, αλλά τώρα είναι οργανωμένη για επαναχρησιμοποίηση.

---

## Βήμα 5: Διαχείριση Edge Cases και Συνηθισμένων Παγίδων

1. **Απουσία χαρακτηριστικού `href`** – Το XPath θα επιστρέψει ακόμα τον κόμβο `<a>` ακόμα και αν λείπει το `href`. Προστατέψτε το ενάντια σε `None`:

   ```python
   href = node.get("href")
   if href:
       download_links.append(href)
   ```

2. **Σχετικές vs. απόλυτες URL** – Αν οι σύνδεσμοι σας είναι σχετικοί, ίσως θέλετε να τους επιλύσετε σε σχέση με τη βασική URL:

   ```python
   from urllib.parse import urljoin
   base_url = "https://example.com"
   absolute = urljoin(base_url, href)
   ```

3. **Κατεστραμμένο HTML** – Το `lxml` είναι ανεκτικό, αλλά εξαιρετικά κατεστραμμένο markup μπορεί να προκαλέσει `XMLSyntaxError` στο `html.parse`. Τυλίξτε την κλήση parse σε block `try/except` για να καταγράψετε και να παραλείψετε προβληματικά αρχεία.

4. **Απόδοση με μεγάλα αρχεία** – Για σελίδες πολλαπλών megabytes, σκεφτείτε τη ροή με `iterparse` αντί να φορτώνετε ολόκληρο το DOM στη μνήμη.

---

## Οπτική Επισκόπηση (προαιρετικό)

![How to parse HTML flow diagram showing load file → CSS selector → XPath contains → get href attribute](how-to-parse-html-flow.png "How to parse HTML flow diagram")

*Το κείμενο alt περιλαμβάνει τη βασική λέξη-κλειδί για να ικανοποιήσει το SEO.*

---

## Συμπέρασμα

Καλύψαμε **πώς να αναλύσετε HTML** σε Python από την αρχή μέχρι το τέλος: φόρτωση αρχείου HTML, χρήση CSS selector για εξαγωγή επικεφαλίδων άρθρων, δημιουργία παραδείγματος XPath contains για εντοπισμό συνδέσμων λήψης, και τέλος **λήψη τιμών του χαρακτηριστικού href** με ασφάλεια. Η επαναχρησιμοποιήσιμη συνάρτηση `parse_news_html` δείχνει μια καθαρή, συντηρήσιμη προσέγγιση που μπορείτε να προσαρμόσετε σε οποιοδήποτε έργο scraping.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να επεκτείνετε το script ώστε:

- Να αναλύει πίνακες με ερωτήματα XPath `//table//tr`.
- Να εξάγει χαρακτηριστικά `src` εικόνων χρησιμοποιώντας ένα ακόμη **xpath contains example**.
- Να μεταβείτε σε ασύγχρονη λήψη με `aiohttp` για ζωντανές ιστοσελίδες.

Καλή ανάλυση, και θυμηθείτε—μια φορά που θα κυριαρχήσετε αυτά τα βασικά, το υπόλοιπο του HTML scraping γίνεται παιδικό παιχνίδι. Αν συναντήσετε δυσκολίες, αφήστε ένα σχόλιο παρακάτω—ας το αντιμετωπίσουμε μαζί!

## Σχετικά Tutorials

- [Φόρτωση Εγγράφων HTML από Αρχείο στο Aspose.HTML για Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Πώς να Επεξεργαστείτε το Δέντρο Εγγράφου HTML στο Aspose.HTML για Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Πώς να Προσθέσετε CSS – Inline CSS σε Έγγραφα HTML στο Aspose.HTML για Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-05-31
description: Python का उपयोग करके HTML से SVG निकालना सीखें। यह चरण‑दर‑चरण ट्यूटोरियल
  दिखाता है कि HTML दस्तावेज़ को कैसे पढ़ें, SVG फ़ाइलें कैसे सहेजें और इनलाइन SVG
  को प्रभावी ढंग से कैसे सहेजें।
draft: false
keywords:
- how to extract svg
- read html document
- save svg files
- save inline svg
- extract svg from html
language: hi
og_description: Python का उपयोग करके HTML से SVG निकालने का तरीका। इस ट्यूटोरियल का
  पालन करके HTML दस्तावेज़ पढ़ें, SVG फ़ाइलें सहेजें और इनलाइन SVG को आसानी से संभालें।
og_title: Python के साथ HTML से SVG निकालने का तरीका – पूर्ण गाइड
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  headline: How to extract SVG from HTML with Python – Complete Guide
  type: TechArticle
- description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  name: How to extract SVG from HTML with Python – Complete Guide
  steps:
  - name: Reads an HTML file.
    text: Reads an HTML file.
  - name: Collects inline <svg> markup.
    text: Collects inline <svg> markup.
  - name: Finds external SVG references (<img> and <object> tags).
    text: Finds external SVG references (<img> and <object> tags).
  - name: Saves each SVG to a separate .svg file.
    text: Saves each SVG to a separate .svg file.
  type: HowTo
tags:
- Python
- SVG
- HTML parsing
- Aspose
title: Python के साथ HTML से SVG निकालने का तरीका – पूर्ण गाइड
url: /hi/python/general/how-to-extract-svg-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML से SVG निकालने के लिए Python – पूर्ण गाइड

क्या आपने कभी **SVG निकालने का तरीका** एक गंदे HTML पेज से बिना सिर दर्द के सोचा है? आप अकेले नहीं हैं। चाहे आप वेब‑स्क्रैपर बना रहे हों, डिज़ाइन‑पाइपलाइन, या सिर्फ आइकॉन को बैच‑एक्सपोर्ट करने की ज़रूरत हो, **SVG निकालने का तरीका** जानना एक उपयोगी ट्रिक है जो समय और सिरदर्द बचाता है।

इस ट्यूटोरियल में हम आपको बिल्कुल **SVG निकालने का तरीका** Aspose.HTML लाइब्रेरी for Python का उपयोग करके दिखाएंगे। हम HTML दस्तावेज़ पढ़ेंगे, दोनों इनलाइन `<svg>` मार्कअप **और** बाहरी SVG रेफ़रेंसेज़ को निकालेंगे, फिर **SVG फ़ाइलें** डिस्क पर **सेव** करेंगे—सब एक साफ़, पुन: उपयोग योग्य स्क्रिप्ट में। अंत तक आपके पास एक तैयार‑चलाने योग्य समाधान होगा जिसे आप अपने प्रोजेक्ट्स में अनुकूलित कर सकते हैं।

> **Pro tip:** यदि आप केवल पेज का त्वरित निरीक्षण चाहते हैं, तो `BeautifulSoup` भी काम करता है, लेकिन Aspose.HTML आपको पूर्ण DOM देता है, जिससे इनलाइन और लिंक्ड दोनों SVG को निकालना आसान हो जाता है।

## आपको क्या चाहिए

* Python 3.8+ (कोड f‑strings का उपयोग करता है, इसलिए 3.6+ न्यूनतम है)
* `pip install aspose-html` – वह व्यावसायिक लाइब्रेरी जो हमारे HTML पार्सिंग को शक्ति देती है
* एक फ़ोल्डर जिसमें `input.html` फ़ाइल हो जिसमें वह SVG हों जिन्हें आप निकालना चाहते हैं
* आउटपुट डायरेक्टरी में लिखने की अनुमति (हम इसे `YOUR_DIRECTORY` कहेंगे)

बस इतना ही—कोई अतिरिक्त बाइनरी नहीं, कोई हेडलेस ब्राउज़र नहीं। सरल, है ना?

## चरण 1: Aspose.HTML के साथ HTML दस्तावेज़ पढ़ें

सबसे पहला काम है **HTML दस्तावेज़ पढ़ना** ताकि आप उसके DOM ट्री को ट्रैवर्स कर सकें। Aspose.HTML आपको एक `HTMLDocument` ऑब्जेक्ट देता है जो ब्राउज़र के `document` की तरह व्यवहार करता है।

```python
from aspose.html import HTMLDocument

# Load the HTML file – replace YOUR_DIRECTORY with the actual path
doc = HTMLDocument("YOUR_DIRECTORY/input.html")
```

*यह क्यों महत्वपूर्ण है:* HTML को सही DOM में लोड करके आप regex‑आधारित पार्सिंग की समस्याओं से बचते हैं, और आपको `get_elements_by_tag_name` और `query_selector_all` जैसी मेथड्स मुफ्त में मिलती हैं।

## चरण 2: सभी इनलाइन <svg> तत्व इकट्ठा करें

इनलाइन SVG वे `<svg>…</svg>` ब्लॉक्स होते हैं जो सीधे HTML के भीतर होते हैं। **इनलाइन SVG को सेव** करने के लिए हमें केवल उनका बाहरी HTML चाहिए।

```python
svg_contents = []  # We'll collect both markup and file paths here

# Find every <svg> element in the document
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)   # Store the raw markup
```

ध्यान दें कि हम कच्चा मार्कअप सीधे `svg_contents` में जोड़ रहे हैं। बाद में हम तय करेंगे कि प्रत्येक एंट्री मार्कअप है या फ़ाइल पाथ।

## चरण 3: बाहरी SVG रेफ़रेंसेज़ खोजें (img और object टैग्स)

कई पेज बाहरी SVG फ़ाइलों को `<img src="icon.svg">` या `<object data="logo.svg">` के माध्यम से लिंक करते हैं। **HTML से SVG निकालने** के लिए हमें उन URLs को भी कैप्चर करना होगा।

```python
# CSS selector: img or object whose src/data ends with .svg (case‑insensitive)
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    # For <img> we read the src attribute, for <object> the data attribute
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:                                   # Guard against missing attribute
        svg_contents.append(src)
```

*एज केस अलर्ट:* यदि SVG URL रिलेटिव है, तो आपको उसे HTML फ़ाइल के बेस पाथ के साथ जोड़ना होगा। संक्षिप्तता के लिए हम मान लेते हैं कि HTML SVG फ़ाइलों के साथ ही स्थित है।

## चरण 4: प्रत्येक SVG को अलग फ़ाइल में लिखें

अब हमारे पास मार्कअप स्ट्रिंग्स और फ़ाइल पाथ्स की मिश्रित सूची है, हम इटररेट करेंगे और **SVG फ़ाइलें** सेव करेंगे। स्क्रिप्ट स्वचालित रूप से इनलाइन मार्कअप और मौजूदा फ़ाइल रेफ़रेंस के बीच अंतर करती है।

```python
import os
import shutil

for index, content in enumerate(svg_contents):
    output_path = f"YOUR_DIRECTORY/svg_{index}.svg"

    # Trim leading whitespace and check if it looks like markup
    if content.lstrip().startswith("<svg"):
        # Inline SVG – write the markup directly
        with open(output_path, "w", encoding="utf-8") as file:
            file.write(content)
        print(f"Saved inline SVG to {output_path}")
    else:
        # External reference – copy the source file's contents
        src_path = os.path.abspath(content)  # Resolve relative paths
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, output_path)
            print(f"Copied external SVG from {src_path} to {output_path}")
        else:
            print(f"⚠️  Warning: referenced SVG not found: {src_path}")
```

**आप क्या देखेंगे:** स्क्रिप्ट समाप्त होने के बाद, `YOUR_DIRECTORY` में `svg_0.svg`, `svg_1.svg`, … नाम की फ़ाइलें होंगी, प्रत्येक में या तो मूल इनलाइन मार्कअप या बाहरी SVG की कॉपी होगी।

### अपेक्षित आउटपुट

```
Saved inline SVG to YOUR_DIRECTORY/svg_0.svg
Saved inline SVG to YOUR_DIRECTORY/svg_1.svg
Copied external SVG from /path/to/logo.svg to YOUR_DIRECTORY/svg_2.svg
...
```

यदि कोई रेफ़रेंस्ड फ़ाइल गायब है, तो स्क्रिप्ट एक चेतावनी प्रिंट करती है लेकिन जारी रहती है—इसलिए एक टूटे लिंक से पूरी एक्सट्रैक्शन रुक नहीं जाएगी।

## सामान्य समस्याओं का समाधान

| समस्या | क्यों होता है | त्वरित समाधान |
|---------|----------------|-----------|
| **रिलेटिव URLs टूटते हैं** | `src` एट्रिब्यूट `"../assets/icon.svg"` हो सकता है | `os.path.join(os.path.dirname(html_path), src)` का उपयोग करके हल करें। |
| **डुप्लिकेट फ़ाइल नाम** | दो SVG जिनका नाम एक ही है, ओवरराइट हो जाते हैं | फ़ाइलनाम में कंटेंट का हैश शामिल करें (`hashlib.md5(content.encode()).hexdigest()[:8]`)। |
| **बड़े इनलाइन SVG मेमोरी स्पाइक पैदा करते हैं** | लिखने से पहले सभी मार्कअप को एक सूची में स्टोर करना | बफ़रिंग के बजाय प्रत्येक तत्व को सीधे फ़ाइल में स्ट्रीम करें। |
| **नॉन‑SVG इमेजेज़ पास हो जाती हैं** | कुछ `<img>` टैग्स `.svg?version=1` पर समाप्त होते हैं | एक्सटेंशन चेक से पहले क्वेरी स्ट्रिंग हटाएँ (`src.split('?')[0]`)। |

## पूरी स्क्रिप्ट जिसे आप कॉपी‑पेस्ट कर सकते हैं

नीचे पूरा, तैयार‑चलाने योग्य प्रोग्राम है। इसे `extract_svg.py` के रूप में सेव करें, `YOUR_DIRECTORY` को समायोजित करें, और `python extract_svg.py` चलाएँ।

```python
"""
extract_svg.py – How to extract SVG from HTML using Aspose.HTML for Python

This script:
1. Reads an HTML file.
2. Collects inline <svg> markup.
3. Finds external SVG references (<img> and <object> tags).
4. Saves each SVG to a separate .svg file.

Author: Your Name
Date: 2026-05-31
"""

import os
import shutil
from aspose.html import HTMLDocument

# ----------------------------------------------------------------------
# Configuration – change these paths to suit your environment
# ----------------------------------------------------------------------
HTML_PATH = "YOUR_DIRECTORY/input.html"          # Path to source HTML
OUTPUT_DIR = "YOUR_DIRECTORY"                    # Where SVGs will be written

# Ensure output directory exists
os.makedirs(OUTPUT_DIR, exist_ok=True)

# ----------------------------------------------------------------------
# Step 1: Load the HTML document (read html document)
# ----------------------------------------------------------------------
doc = HTMLDocument(HTML_PATH)

# ----------------------------------------------------------------------
# Step 2: Collect inline <svg> elements (save inline svg)
# ----------------------------------------------------------------------
svg_contents = []
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)

# ----------------------------------------------------------------------
# Step 3: Collect external SVG references (extract svg from html)
# ----------------------------------------------------------------------
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:
        # Resolve relative paths relative to the HTML file location
        src_path = os.path.join(os.path.dirname(HTML_PATH), src)
        svg_contents.append(src_path)

# ----------------------------------------------------------------------
# Step 4: Save each gathered SVG (save svg files)
# ----------------------------------------------------------------------
for idx, content in enumerate(svg_contents):
    out_path = os.path.join(OUTPUT_DIR, f"svg_{idx}.svg")

    # Detect inline markup vs file path
    if isinstance(content, str) and content.lstrip().startswith("<svg"):
        # Inline SVG – write directly
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(content)
        print(f"[✓] Inline SVG saved → {out_path}")
    else:
        # External file – copy its contents
        src_path = os.path.abspath(content)
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, out_path)
            print(f"[✓] External SVG copied → {out_path}")
        else:
            print(f"[⚠] Missing SVG file: {src_path}")

print("\n✅ Extraction complete. Check the", OUTPUT_DIR, "folder for your SVGs.")
```

## सारांश – SVG निकालने का संक्षिप्त तरीका

* **`HTMLDocument` के साथ HTML दस्तावेज़ पढ़ें**।
* **`get_elements_by_tag_name` द्वारा इनलाइन `<svg>` इकट्ठा करें**।
* **`.svg` पर समाप्त होने वाले CSS सिलेक्टर से बाहरी SVG खोजें**।
* **प्रत्येक भाग को सेव करें**—मार्कअप को सीधे फ़ाइल में लिखें या रेफ़रेंस्ड फ़ाइल कॉपी करें।
* **एज केस संभालें** जैसे रिलेटिव पाथ्स, डुप्लिकेट्स, और गायब फ़ाइलें।

यह ही पूरा उत्तर है **HTML पेज से SVG निकालने** का, एक ही, आसानी से संशोधित करने योग्य स्क्रिप्ट में संलग्न।

## आगे क्या?

अब जब आप **SVG निकाल सकते** हैं, तो इन आगे के विचारों पर विचार करें:

* **बैच प्रोसेसिंग:** आइकॉन लाइब्रेरी बनाने के लिए HTML फ़ाइलों की डायरेक्टरी पर लूप चलाएँ।
* **ऑप्टिमाइज़ेशन:** प्रत्येक सेव किए गए SVG को SVGO (Node.js ऑप्टिमाइज़र) से चलाएँ ताकि फ़ाइल आकार घटे।
* **कन्वर्ज़न:** `cairosvg` या `svglib` का उपयोग करके SVG को PNG में बदलें पुराने ब्राउज़रों के लिए।
* **मेटाडेटा एक्सट्रैक्शन:** प्रत्येक SVG के अंदर `<title>` या `<desc>` टैग्स को पार्स करें ताकि खोज योग्य लेबल मिलें।

इनमें से प्रत्येक विषय हमारे सेकेंडरी कीवर्ड्स—**read HTML document**, **save svg files**, **save inline svg**, **extract svg from html**—से जुड़ा है, इसलिए आपके पास खोजने के लिए भरपूर सामग्री होगी।

---

*हैप्पी हैकिंग! यदि आपको कोई समस्या आती है, तो नीचे टिप्पणी छोड़ें या GitHub पर मुझे पिंग करें। SVG की दुनिया विशाल है, लेकिन सही टूल्स के साथ, उन्हें निकालना बहुत आसान है।*

## अब आपको क्या सीखना चाहिए?

- [Aspose.HTML for Java में SVG दस्तावेज़ सहेजें](/html/english/java/saving-html-documents/save-svg-document/)
- [Aspose.HTML for Java के साथ SVG को XPS में कैसे बदलें](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)
- [Aspose.HTML के साथ .NET में SVG दस्तावेज़ को PNG फ़ॉर्मेट में रेंडर करें](/html/french/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
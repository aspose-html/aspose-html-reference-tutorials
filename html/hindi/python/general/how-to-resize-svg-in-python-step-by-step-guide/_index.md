---
category: general
date: 2026-06-16
description: Python में SVG को जल्दी से रिसाइज़ कैसे करें – Python से SVG फ़ाइल लोड
  करें, Python से SVG फ़ाइल संपादित करें, और एक छोटे स्क्रिप्ट से SVG फ़ाइलों को बैच
  में भी रिसाइज़ करें।
draft: false
keywords:
- how to resize svg
- batch resize svg files
- load svg file python
- edit svg file python
language: hi
og_description: Python में SVG का आकार कैसे बदलें? स्पष्ट, चलाने योग्य उदाहरण के साथ
  SVG फ़ाइल को Python में लोड करना, SVG फ़ाइल को Python में संपादित करना, और बैच में
  SVG फ़ाइलों का आकार बदलना सीखें।
og_title: Python में SVG का आकार कैसे बदलें – पूर्ण ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to resize SVG in Python quickly – load SVG file Python, edit SVG
    file Python, and even batch resize SVG files with a tiny script.
  headline: How to Resize SVG in Python – Step‑by‑Step Guide
  type: TechArticle
- description: How to resize SVG in Python quickly – load SVG file Python, edit SVG
    file Python, and even batch resize SVG files with a tiny script.
  name: How to Resize SVG in Python – Step‑by‑Step Guide
  steps:
  - name: '**Collects** every `.svg` file in the source folder.'
    text: '**Collects** every `.svg` file in the source folder.'
  - name: '**Loads** each file using the same routine we used for a single SVG.'
    text: '**Loads** each file using the same routine we used for a single SVG.'
  - name: '**Resizes** to the desired width while keeping the aspect ratio.'
    text: '**Resizes** to the desired width while keeping the aspect ratio.'
  - name: '**Writes** the result to a new folder, leaving originals untouched.'
    text: '**Writes** the result to a new folder, leaving originals untouched.'
  type: HowTo
tags:
- Python
- SVG
- Automation
title: Python में SVG का आकार कैसे बदलें – चरण‑दर‑चरण मार्गदर्शिका
url: /hi/python/general/how-to-resize-svg-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SVG को Python में री‑साइज़ कैसे करें – पूर्ण ट्यूटोरियल

क्या आप कभी **SVG को री‑साइज़ कैसे करें** बिना ग्राफ़िक्स एडिटर खोले, के बारे में सोचते रहे हैं? शायद आपके पास एक लोगो है जिसे वेब बैनर के लिए 200 px चौड़ा होना चाहिए, या आप मोबाइल ऐप के लिए दर्जनों आइकन तैयार कर रहे हैं। अच्छी खबर? आप यह सब Python में कर सकते हैं—नो Photoshop, नो Inkscape UI, बस कुछ लाइनों का कोड।

इस गाइड में हम Python में SVG फ़ाइल लोड करने, उसके आयाम संपादित करने, और यहाँ तक कि एक ही बार में कई SVG फ़ाइलों को स्केल करने की प्रक्रिया देखेंगे। अंत तक आप **load SVG file Python**, **edit SVG file Python**, और **batch resize SVG files** को आत्मविश्वास के साथ कर पाएँगे।

## आवश्यकताएँ

- Python 3.8+ स्थापित हो (मानक `python` कमांड काम करता है)
- `svgwrite` या `lxml` लाइब्रेरी – हम `lxml` का उपयोग करेंगे क्योंकि यह सीधे DOM एक्सेस देता है।
- एक फ़ोल्डर जिसमें वह SVGs हों जिन्हें आप री‑साइज़ करना चाहते हैं (उदाहरण के लिए `assets/icons/`)

आपको किसी GUI टूल की ज़रूरत नहीं है; सब कुछ टर्मिनल से चलता है।

---

## चरण 1: आवश्यक लाइब्रेरी स्थापित करें

पहले, PyPI से `lxml` प्राप्त करें। यह छोटा, तेज़, और हमें XML एट्रिब्यूट्स को सीधे बदलने देता है।

```bash
pip install lxml
```

> **Pro tip:** यदि आप वर्चुअल एनवायरनमेंट में काम कर रहे हैं, तो कमांड चलाने से पहले उसे सक्रिय करें। इससे आपके प्रोजेक्ट की डिपेंडेंसीज़ साफ़ रहती हैं।

## चरण 2: Python में SVG फ़ाइल लोड करें

अब हम **load SVG file Python** शैली में करेंगे—XML पढ़ेंगे, रूट `<svg>` एलिमेंट प्राप्त करेंगे, और उसकी वर्तमान साइज प्रिंट करेंगे।

```python
from lxml import etree

def load_svg(path: str) -> etree._ElementTree:
    """
    Load an SVG document and return the parsed XML tree.
    """
    parser = etree.XMLParser(remove_blank_text=True)
    tree = etree.parse(path, parser)
    return tree

# Example usage
svg_path = "assets/logo.svg"
svg_tree = load_svg(svg_path)
root = svg_tree.getroot()
print(f"Original width: {root.get('width')}, height: {root.get('height')}")
```

**Why this matters:** `lxml` हमें एक वास्तविक DOM देता है, इसलिए हम किसी भी एट्रिब्यूट को क्वेरी या बदल सकते हैं—**edit SVG file Python** कार्यों के लिए एकदम उपयुक्त।

## चरण 3: चौड़ाई (और ऊँचाई) बदलें – SVG को री‑साइज़ कैसे करें

SVG वेक्टर होते हैं, इसलिए आप या तो चौड़ाई, ऊँचाई, या दोनों सेट कर सकते हैं। यदि आप केवल चौड़ाई बदलते हैं, तो viewBox अनुपात को बनाए रखेगा, लेकिन कई टूल्स मिलते‑जुलते height एट्रिब्यूट का भी सम्मान करते हैं। यहाँ एक हेल्पर है जो मूल aspect ratio को बनाए रखते हुए री‑साइज़ करता है:

```python
def resize_svg(tree: etree._ElementTree, new_width: int) -> None:
    """
    Resize the root <svg> element to `new_width` while preserving aspect ratio.
    """
    root = tree.getroot()
    # Grab original dimensions (they may be in px, pt, or just numbers)
    orig_width = float(root.get("width").replace("px", ""))
    orig_height = float(root.get("height").replace("px", ""))

    # Compute scale factor and new height
    scale = new_width / orig_width
    new_height = round(orig_height * scale, 2)

    # Update attributes
    root.set("width", f"{new_width}px")
    root.set("height", f"{new_height}px")

    # Optional: ensure viewBox exists for better scaling in browsers
    if "viewBox" not in root.attrib:
        viewbox = f"0 0 {orig_width} {orig_height}"
        root.set("viewBox", viewbox)

# Resize to 200 px wide
resize_svg(svg_tree, 200)
```

ऊपर दिया गया फ़ंक्शन **how to resize SVG** का मूल है। यह वर्तमान साइज पढ़ता है, अनुपातिक ऊँचाई गणना करता है, और नई एट्रिब्यूट्स फ़ाइल में लिख देता है।

## चरण 4: संशोधित SVG को सहेजें

संपादन के बाद, आपको बदलावों को डिस्क पर वापस लिखना होगा। यह **edit SVG file Python** चक्र को पूरा करता है।

```python
def save_svg(tree: etree._ElementTree, destination: str) -> None:
    """
    Write the modified SVG tree to `destination`.
    """
    tree.write(
        destination,
        pretty_print=True,
        xml_declaration=True,
        encoding="UTF-8"
    )
    print(f"Saved resized SVG to {destination}")

# Save as a new file so the original stays untouched
output_path = "assets/logo_resized.svg"
save_svg(svg_tree, output_path)
```

पूरा स्क्रिप्ट चलाएँ और आपको एक नई `logo_resized.svg` दिखेगी जो बिल्कुल 200 px चौड़ी होगी।

## चरण 5: बैच में SVG फ़ाइलों को री‑साइज़ करें – पूरे फ़ोल्डर को स्केल करें

अब जब हम **load SVG file Python**, **edit SVG file Python**, और इसे सहेज सकते हैं, चलिए एक डायरेक्टरी पर लूप लगाते हैं और प्रत्येक फ़ाइल पर वही ट्रांसफ़ॉर्मेशन लागू करते हैं। यह **batch resize SVG files** का उत्तर है।

```python
import pathlib

def batch_resize(source_dir: str, target_dir: str, width: int) -> None:
    """
    Resize every .svg file in `source_dir` to `width` pixels and store
    the results in `target_dir`.
    """
    src = pathlib.Path(source_dir)
    tgt = pathlib.Path(target_dir)
    tgt.mkdir(parents=True, exist_ok=True)

    svg_files = list(src.glob("*.svg"))
    if not svg_files:
        print("No SVG files found.")
        return

    for svg_path in svg_files:
        try:
            tree = load_svg(str(svg_path))
            resize_svg(tree, width)
            out_path = tgt / svg_path.name
            save_svg(tree, str(out_path))
        except Exception as e:
            print(f"Failed on {svg_path.name}: {e}")

# Example: resize everything in 'assets/icons' to 64 px wide
batch_resize("assets/icons", "assets/icons_resized", 64)
```

### यह क्या करता है:

1. **Collects** स्रोत फ़ोल्डर में प्रत्येक `.svg` फ़ाइल को इकट्ठा करता है।
2. **Loads** प्रत्येक फ़ाइल को उसी रूटीन से लोड करता है जो हमने एकल SVG के लिए उपयोग किया था।
3. **Resizes** इच्छित चौड़ाई पर सेट करता है जबकि aspect ratio को बनाए रखता है।
4. **Writes** परिणाम को एक नए फ़ोल्डर में लिखता है, मूल फ़ाइलों को अपरिवर्तित छोड़ता है।

अब आपके पास **batch resize SVG files** के लिए एक तैयार‑उपयोग पाइपलाइन है।

## चरण 6: किनारे के मामलों और सामान्य समस्याएँ

| समस्या | क्यों होता है | समाधान |
|-------|----------------|-----|
| `width`/`height` एट्रिब्यूट्स की कमी | कुछ SVG केवल `viewBox` पर निर्भर होते हैं। | यदि एट्रिब्यूट्स अनुपस्थित हैं, तो viewBox आयामों (`viewBox="0 0 w h"`) पर फॉलबैक करें। |
| `px` के अलावा अन्य इकाइयाँ (जैसे `pt`, `%`) | स्क्रिप्ट केवल `px` हटाती है। | `replace` कॉल को विस्तारित करें या किसी भी इकाई को पकड़ने के लिए regex उपयोग करें। |
| जटिल `<symbol>` या `<use>` एलिमेंट्स | रूट को री‑साइज़ करने से नेस्टेड सिम्बॉल्स प्रभावित नहीं हो सकते। | प्रत्येक `<symbol>` टैग पर समान एट्रिब्यूट परिवर्तन लागू करें, या CSS `transform: scale()` उपयोग करें। |
| फ़ाइल नामों में Unicode या विशेष अक्षर | `pathlib` अधिकांश मामलों को संभालता है, लेकिन Windows कुछ अक्षरों पर समस्या कर सकता है। | फ़ाइलनाम UTF‑8 सुरक्षित हों, यह सुनिश्चित करें, या प्रोसेसिंग से पहले उनका नाम बदलें। |

इनको पहले से ही संबोधित करने से बाद में आश्चर्यजनक टूटे हुए आइकन से बचा जा सकता है।

## चरण 7: परिणाम की जाँच करें

एक त्वरित sanity check एक छोटे HTML स्निपेट से किया जा सकता है:

```html
<!DOCTYPE html>
<html>
<head><title>SVG Test</title></head>
<body>
  <h3>Original</h3>
  <img src="assets/logo.svg" alt="original logo">
  <h3>Resized</h3>
  <img src="assets/logo_resized.svg" alt="resized logo">
</body>
</html>
```

फ़ाइल को ब्राउज़र में खोलें—दोनों इमेज़ समान दिखनी चाहिए, लेकिन री‑साइज़्ड इमेज़ डेवलपर टूल्स में **200 px** की चौड़ाई दिखाएगी।

---

## निष्कर्ष

अब आप शुद्ध Python का उपयोग करके **how to resize SVG** करना जानते हैं, एक फ़ाइल से लेकर पूरी डायरेक्टरी तक। यह वर्कफ़्लो **load SVG file Python**, **edit SVG file Python**, और **batch resize SVG files** को कवर करता है—सिर्फ कुछ फ़ंक्शन्स के साथ।

इसे आज़माएँ: विभिन्न चौड़ाइयों को ट्राय करें, केवल ऊँचाई री‑साइज़िंग के साथ प्रयोग करें, या `argparse` का उपयोग करके कमांड‑लाइन इंटरफ़ेस जोड़ें। संभावनाएँ अनंत हैं, और स्क्रिप्ट इतनी हल्की है कि इसे बिल्ड पाइपलाइन्स, CI जॉब्स, या डेस्कटॉप यूटिलिटीज़ में एम्बेड किया जा सकता है।

ग्रेडिएंट्स, एम्बेडेड फ़ॉन्ट्स, या इसे Flask ऐप में इंटीग्रेट करने के बारे में सवाल हैं? टिप्पणी छोड़ें, और हम साथ में उन पहलुओं को देखेंगे। कोडिंग का आनंद लें!

## अब आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर करने में मदद करेंगे।

- [Aspose.HTML के साथ .NET में SVG को इमेज में बदलें](/html/hindi/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [Aspose.HTML के साथ .NET में SVG को PDF में बदलें](/html/hindi/net/canvas-and-image-manipulation/convert-svg-to-pdf/)
- [Aspose.HTML के साथ .NET में SVG दस्तावेज़ को PNG के रूप में प्रस्तुत करें](/html/hindi/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
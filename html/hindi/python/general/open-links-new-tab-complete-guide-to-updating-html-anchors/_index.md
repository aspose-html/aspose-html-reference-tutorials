---
category: general
date: 2026-07-05
description: Python का उपयोग करके लिंक को नई टैब में खोलें – सीखें कैसे target="_blank"
  जोड़ें, लिंक टार्गेट बदलें, attribute contains सेलेक्टर का उपयोग करें, और संशोधित
  HTML को आसानी से सहेजें।
draft: false
keywords:
- open links new tab
- add target blank
- change link target
- attribute contains selector
- save modified html
language: hi
og_description: लिंक को जल्दी से नए टैब में खोलें। यह ट्यूटोरियल दिखाता है कि टार्गेट
  ब्लैंक कैसे जोड़ें, लिंक टार्गेट बदलें, और पायथन के साथ संशोधित HTML को कैसे सहेजें।
og_title: लिंक को नई टैब में खोलें – चरण‑दर‑चरण HTML अपडेट गाइड
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  headline: Open Links New Tab – Complete Guide to Updating HTML Anchors
  type: TechArticle
- description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  name: Open Links New Tab – Complete Guide to Updating HTML Anchors
  steps:
  - name: Expected Result
    text: 'Suppose `links.html` originally contained:'
  - name: What if a link already has a `rel` attribute?
    text: 'Our loop overwrites it with `"noopener"`. If you need to preserve existing
      values (e.g., `"nofollow"`), concatenate instead:'
  - name: How to handle multiple domains?
    text: 'Just expand the selector list:'
  - name: Does `prettify()` change the original HTML structure?
    text: It re‑indents but doesn’t alter tag order or attribute values. If you must
      keep the exact original whitespace, replace `prettify()` with `str(soup)` as
      mentioned earlier.
  type: HowTo
tags:
- HTML manipulation
- Python
- web automation
title: लिंक को नई टैब में खोलें – HTML एंकर को अपडेट करने की पूरी गाइड
url: /hi/python/general/open-links-new-tab-complete-guide-to-updating-html-anchors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# लिंक को नई टैब में खोलें – HTML एंकर अपडेट करने के लिए पूर्ण गाइड

क्या आपको कभी स्थैतिक HTML पेज पर **लिंक को नई टैब में खोलने** की ज़रूरत पड़ी, लेकिन शुरुआत कैसे करें, समझ नहीं आया? आप अकेले नहीं हैं। कई डेवलपर्स को लेगेसी साइट्स को साफ़ करते समय या एक्सेसिबिलिटी सुधार जोड़ते समय यही समस्या आती है। इस ट्यूटोरियल में हम एक व्यावहारिक समाधान के माध्यम से चलेंगे जो **target blank जोड़ता है**, **लिंक टार्गेट बदलता है**, और सुरक्षित रूप से **संपादित html को सेव** करता है—सिर्फ कुछ पंक्तियों के Python कोड से।

हम यह भी देखेंगे कि **attribute contains selector** का उपयोग कैसे करें ताकि आप केवल उन एंकर को छुएँ जिनकी आपको वास्तव में ज़रूरत है (उदाहरण के लिए, *example.com* की ओर इशारा करने वाले सभी लिंक)। अंत तक, आपके पास एक पुन: उपयोग योग्य स्क्रिप्ट होगी जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं, चाहे वह बड़ा हो या छोटा।

## आप क्या सीखेंगे

- HTML फ़ाइल को एक manipulable डॉक्यूमेंट ऑब्जेक्ट में लोड करना।  
- उन `<a>` एलिमेंट्स को चुनना जिनके `href` एट्रिब्यूट में एक विशिष्ट सबस्ट्रिंग शामिल है।  
- **target blank जोड़ना** और सुरक्षा बढ़ाने के लिए `rel="noopener"` एट्रिब्यूट सेट करना।  
- **संपादित html को** डिस्क पर वापस सेव करना बिना फ़ॉर्मेटिंग खोए।  

कोई बाहरी निर्भरताएँ नहीं, केवल स्टैंडर्ड लाइब्रेरी और **beautifulsoup4** (एक छोटा इंस्टॉल)। यदि आप कोई अलग पार्सर उपयोग कर रहे हैं, तो अवधारणाएँ सीधे लागू होती हैं।

---

## पूर्वापेक्षाएँ

- आपके मशीन पर Python 3.8+ स्थापित हो।  
- HTML और Python की बुनियादी समझ।  
- `beautifulsoup4` पैकेज (`pip install beautifulsoup4`)।  

बस इतना ही—कोई भारी फ्रेमवर्क नहीं चाहिए।

---

## चरण 1: HTML डॉक्यूमेंट लोड करें

सबसे पहले हमें स्रोत फ़ाइल पढ़नी होगी और उसे BeautifulSoup को देना होगा। इसे एक खाली कैनवास खोलने के रूप में सोचें जहाँ आप नई एट्रिब्यूट्स जोड़ सकते हैं।

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Path to the original HTML file
html_path = Path("YOUR_DIRECTORY/links.html")

# Read the file content
with html_path.open(encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")
```

> **यह क्यों महत्वपूर्ण है:** `Path` का उपयोग कोड को OS‑अग्नॉस्टिक बनाता है, और `html.parser` बिल्ट‑इन है, इसलिए साधारण कार्यों के लिए अतिरिक्त पार्सर की ज़रूरत नहीं पड़ती।

---

## चरण 2: सही लिंक खोजने के लिए Attribute Contains Selector का उपयोग करें

हम केवल उन एंकर को छूना चाहते हैं जो *example.com* की ओर इशारा करते हैं। CSS सेलेक्टर `a[href*='example.com']` ठीक यही करता है—`*=` का मतलब “contains” है। BeautifulSoup की `select` मेथड इस सिंटैक्स को समझती है।

```python
# Find all <a> tags whose href contains 'example.com'
selector = "a[href*='example.com']"
anchor_elements = soup.select(selector)
```

> **प्रो टिप:** यदि आपको केस‑इन्सेंसिटिव मैच चाहिए, तो एक छोटा लूप इस्तेमाल करें जो `if 'example.com' in a.get('href', '').lower()` जाँचता है।

अब `anchor_elements` में वह सभी लिंक हैं जिनकी हमें ज़रूरत है, अगली ट्रांसफ़ॉर्मेशन के लिए तैयार।

---

## चरण 3: लिंक टार्गेट बदलें – Target Blank जोड़ें और लिंक को सुरक्षित बनाएं

लिंक को नई टैब में खोलना इतना सरल है जितना `target="_blank"` सेट करना। हालांकि, आधुनिक ब्राउज़र यह भी सलाह देते हैं कि `rel="noopener"` (या `noreferrer`) जोड़ें ताकि नई खुली पेज मूल विंडो को `window.opener` के माध्यम से एक्सेस न कर सके। यह छोटा सुरक्षा कदम फ़िशिंग अटैक को रोक सकता है।

```python
for anchor in anchor_elements:
    # Open in a new tab
    anchor['target'] = "_blank"          # add target blank
    # Harden security
    anchor['rel'] = "noopener"           # prevent access to the opener page
```

> **हम सीधे डिक्शनरी असाइनमेंट क्यों उपयोग करते हैं:** यह स्वचालित रूप से एट्रिब्यूट बनाता है यदि वह गायब है, और यदि मौजूद है तो उसे ओवरराइट कर देता है—**change link target** ऑपरेशन के लिए एकदम उपयुक्त।

---

## चरण 4: संशोधित HTML को डिस्क पर सेव करें

अंतिम चरण है अपडेटेड मार्कअप को नई फ़ाइल में लिखना। मूल फ़ाइल को अनछुआ रखना आपको अगर कुछ गड़बड़ हो तो वापस लौटने की सुविधा देता है।

```python
# Destination path for the updated HTML
output_path = Path("YOUR_DIRECTORY/links-updated.html")

# Write the prettified HTML (preserves indentation)
with output_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())
```

> **`prettify()` क्या करता है:** यह HTML को सुंदर इंडेंटेशन के साथ फ़ॉर्मेट करता है, जिससे सेव की गई फ़ाइल को पढ़ना और बाद में डिफ़ करना आसान हो जाता है। यदि आप मूल व्हाइटस्पेस रखना चाहते हैं, तो `prettify()` को `str(soup)` से बदल दें।

---

## पूर्ण स्क्रिप्ट – वन‑क्लिक समाधान

नीचे पूरी, तैयार‑चलाने‑योग्य स्क्रिप्ट दी गई है। इसे `update_links.py` के रूप में सेव करें और टर्मिनल से `python update_links.py` चलाएँ।

```python
#!/usr/bin/env python3
"""
Open Links New Tab – script that adds target blank,
sets rel="noopener", and saves modified html.
"""

from pathlib import Path
from bs4 import BeautifulSoup

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Load the HTML document
    # ------------------------------------------------------------------
    html_path = Path("YOUR_DIRECTORY/links.html")
    with html_path.open(encoding="utf-8") as f:
        soup = BeautifulSoup(f, "html.parser")

    # ------------------------------------------------------------------
    # 2️⃣ Select anchors with an attribute contains selector
    # ------------------------------------------------------------------
    selector = "a[href*='example.com']"
    anchors = soup.select(selector)

    # ------------------------------------------------------------------
    # 3️⃣ Change link target – add target blank & secure the link
    # ------------------------------------------------------------------
    for a in anchors:
        a['target'] = "_blank"          # add target blank
        a['rel'] = "noopener"           # prevent opener access

    # ------------------------------------------------------------------
    # 4️⃣ Save modified html to a new file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/links-updated.html")
    with output_path.open("w", encoding="utf-8") as f:
        f.write(soup.prettify())

    print(f"✅ Updated {len(anchors)} link(s) and saved to {output_path}")

if __name__ == "__main__":
    main()
```

### अपेक्षित परिणाम

मान लीजिए `links.html` में मूल रूप से यह था:

```html
<a href="https://example.com/page1">Page 1</a>
<a href="https://other.com/home">Home</a>
```

स्क्रिप्ट चलाने के बाद `links-updated.html` इस प्रकार दिखेगा:

```html
<a href="https://example.com/page1" target="_blank" rel="noopener">Page 1</a>
<a href="https://other.com/home">Home</a>
```

केवल *example.com* की लिंक को **add target blank** एट्रिब्यूट मिला, जिससे यह स्पष्ट होता है कि हमारा **attribute contains selector** ठीक वैसा ही काम किया जैसा हमने चाहा।

---

## सामान्य प्रश्न एवं किनारे के मामलों

### यदि किसी लिंक में पहले से `rel` एट्रिब्यूट है तो क्या होगा?

हमारा लूप इसे `"noopener"` से ओवरराइट कर देता है। यदि आपको मौजूदा मान (जैसे `"nofollow"`) को बरकरार रखना है, तो उन्हें जोड़ें:

```python
existing = a.get('rel', '')
a['rel'] = f"{existing} noopener".strip()
```

### कई डोमेनों को कैसे संभालें?

सेलेक्टर सूची को बस विस्तारित करें:

```python
domains = ["example.com", "sample.org"]
selector = ",".join([f"a[href*='{d}']" for d in domains])
anchors = soup.select(selector)
```

### क्या `prettify()` मूल HTML संरचना बदल देता है?

यह इंडेंटेशन बदलता है लेकिन टैग क्रम या एट्रिब्यूट मान नहीं। यदि आपको बिल्कुल वही व्हाइटस्पेस चाहिए, तो पहले बताया गया अनुसार `prettify()` को `str(soup)` से बदल दें।

---

## प्रोडक्शन‑रेडी स्क्रिप्ट के लिए प्रो टिप्स

- **ओवरराइट करने से पहले बैकअप बनाएं:** `shutil.copy` का उपयोग करके मूल फ़ाइल को सुरक्षित रखें।  
- **प्रिंट के बजाय लॉगिंग:** स्केलेबल प्रोजेक्ट्स के लिए `logging` मॉड्यूल इस्तेमाल करें।  
- **बैच प्रोसेसिंग:** `Path.rglob("*.html")` के साथ किसी डायरेक्टरी में सभी फ़ाइलों को एक ही रन में अपडेट करें।  

इन ट्यूनिंग्स से एक साधारण **open links new tab** स्क्रिप्ट एक मजबूत यूटिलिटी बन जाती है जो किसी भी वेब‑मेंटेनेंस वर्कफ़्लो में फिट बैठती है।

---

## निष्कर्ष

अब आपके पास एक ठोस, पुन: उपयोग योग्य तरीका है **open links new tab** को किसी भी स्थैतिक HTML संग्रह में लागू करने का। **attribute contains selector** का उपयोग करके आप **change link target** को ठीक वहीँ कर सकते हैं जहाँ ज़रूरत है, **add target blank** जोड़ सकते हैं, और **save modified html** को फ़ॉर्मेट खोए बिना कर सकते हैं। 

पहले एक टेस्ट पेज पर इसे आज़माएँ, फिर अपनी पूरी साइट पर स्केल करें। यदि आपको PDF, इमेज या अन्य डोमेनों के लिए सेलेक्टर बदलना है, तो केवल CSS स्ट्रिंग को एडजस्ट करें—बाकी सब वैसा ही रहेगा।

यदि कोई अजीब व्यवहार मिले तो टिप्पणी छोड़ें, या अपने प्रोजेक्ट में स्क्रिप्ट को कैसे विस्तारित किया, यह शेयर करें। Happy coding, और आपके सभी एंकर ठीक उसी जगह खुलें जहाँ आप चाहते हैं!

## आगे क्या सीखें?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर कर सकें।

- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
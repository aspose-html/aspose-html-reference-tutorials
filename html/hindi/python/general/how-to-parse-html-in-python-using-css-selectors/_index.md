---
category: general
date: 2026-10-21
description: Python में HTML को पार्स करना सीखें, HTML दस्तावेज़ लोड करें, CSS सेलेक्टर्स
  का उपयोग करें, और HTML से तेज़ी से हाइपरलिंक निकालें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to parse html
- how to use selector
- extract hyperlinks from html
- load html document python
language: hi
lastmod: 2026-10-21
og_description: CSS चयनकों का उपयोग करके Python में HTML को कैसे पार्स करें। एक HTML
  दस्तावेज़ लोड करें, लिंक चुनें, और साफ़ कोड के साथ HTML से हाइपरलिंक्स निकालें।
og_image_alt: Screenshot showing how to parse HTML in Python with CSS selectors
og_title: Python में HTML को कैसे पार्स करें – चरण-दर-चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to parse HTML in Python, load an HTML document, use CSS selectors,
    and extract hyperlinks from HTML quickly.
  headline: How to parse HTML in Python using CSS selectors
  type: TechArticle
tags:
- python
- html-parsing
- css-selectors
title: Python में CSS चयनकर्ताओं का उपयोग करके HTML को कैसे पार्स करें
url: /hi/python/general/how-to-parse-html-in-python-using-css-selectors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में CSS selectors का उपयोग करके HTML कैसे पार्स करें

यदि आपको Python स्क्रिप्ट में **how to parse html** की आवश्यकता है, तो यह गाइड आपको बिल्कुल वही दिखाएगा। आप सीखेंगे कि HTML दस्तावेज़ को कैसे लोड करें, selector सिंटैक्स का उपयोग करके तत्वों को कैसे खोजें, और HTML से hyperlinks को कैसे निकालें बिना कोई कस्टम पार्सर लिखे।

HTML को पार्स करना वेब स्क्रैपर्स, डेटा‑विश्लेषण पाइपलाइन्स, या स्वचालित परीक्षण के लिए एक सामान्य कार्य है। इस ट्यूटोरियल के अंत तक आपके पास एक पुन: उपयोग योग्य फ़ंक्शन होगा जो एक HTML दस्तावेज़ को लोड करता है, CSS selector के साथ सभी `<a>` टैग चुनता है, और URL की एक साफ़ सूची लौटाता है।

## आप को क्या चाहिए

- Python 3.8+ (कोड किसी भी हालिया संस्करण पर काम करता है)  
- The **lxml** library (`pip install lxml`) – तेज़ HTML पार्सिंग और CSS selector समर्थन प्रदान करता है  
- वह HTML फ़ाइल जिसे आप विश्लेषण करना चाहते हैं (उदाहरण के लिए `sample.html`)  

कोई अतिरिक्त टूल्स आवश्यक नहीं हैं; सब कुछ स्टैंडर्ड लाइब्रेरी और एक सिंगल थर्ड‑पार्टी पैकेज के साथ चलता है।

## चरण 1: HTML कैसे पार्स करें – दस्तावेज़ लोड करें

किसी भी HTML वर्कफ़्लो में पहला चरण फ़ाइल को मेमोरी में पढ़ना है। **lxml.html** का उपयोग करने से आपको एक ट्री ऑब्जेक्ट मिलता है जो CSS selectors को सपोर्ट करता है।

```python
# step_1_load.py
from lxml import html

def load_html(path: str) -> html.HtmlElement:
    """
    Load an HTML document from the given file path.
    Returns an lxml HtmlElement that can be queried with CSS selectors.
    """
    with open(path, "r", encoding="utf-8") as f:
        content = f.read()
    # Parse the raw HTML string into a tree
    return html.fromstring(content)

# Example usage
doc = load_html("sample.html")
print("Document loaded – ready for selector queries.")
```

**यह क्यों महत्वपूर्ण है:**  
`load_html` फ़ाइल‑पढ़ने वाले बायलरप्लेट को एब्स्ट्रैक्ट करता है और सुनिश्चित करता है कि दस्तावेज़ एक टॉलरेंट HTML parser के साथ पार्स किया गया है। यह **load html document python** करने का सबसे सुरक्षित तरीका है, बिना खराब मार्कअप की चिंता किए।

## चरण 2: selector का उपयोग कैसे करें – सभी लिंक तत्व खोजें

एक बार दस्तावेज़ लोड हो जाने पर, आप एक CSS selector का उपयोग करके प्रत्येक `<a>` टैग को खोज सकते हैं। selector `"a"` सभी एंकर तत्वों से मेल खाता है, लेकिन आप इसे और परिष्कृत कर सकते हैं (जैसे, `"a.external"` या `"nav a"`).

```python
# step_2_selector.py
def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    """
    Return a list of <a> elements using a CSS selector.
    This demonstrates how to use selector syntax with lxml.
    """
    # The CSS selector "a" selects every anchor tag
    return doc.cssselect("a")

# Example usage
links = select_links(doc)
print(f"Found {len(links)} <a> elements.")
```

**यह क्यों महत्वपूर्ण है:**  
`how to use selector` दृष्टिकोण आपको जटिल क्वेरीज़ को एक ही पढ़ने योग्य स्ट्रिंग में व्यक्त करने देता है, मैन्युअल ट्री ट्रैवर्सल से बचाता है। यह `lxml.cssselect` द्वारा समर्थित किसी भी CSS पैटर्न के साथ काम करता है।

## चरण 3: HTML से hyperlinks निकालें और प्रोसेस करें

अब जब आपके पास `<a>` तत्वों की एक सूची है, तो आप प्रत्येक से `href` एट्रिब्यूट निकाल सकते हैं। नीचे दिया गया हेल्पर भी रिलेटिव URL को बेस URL के विरुद्ध सामान्यीकृत करता है (यदि आप प्रदान करते हैं)।

```python
# step_3_extract.py
from urllib.parse import urljoin
from typing import Optional

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    """
    Return a list of href values from the given <a> elements.
    If base_url is supplied, relative URLs are resolved to absolute URLs.
    """
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            # Skip <a> tags without an href attribute
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

# Example usage
hyperlinks = extract_hyperlinks(links, base_url="https://example.com")
for url in hyperlinks:
    print(url)
```

**अपेक्षित आउटपुट** (मान लेते हैं कि `sample.html` में तीन लिंक हैं):

```
https://example.com/page1.html
https://example.com/page2.html
https://external.org/resource
```

**यह क्यों महत्वपूर्ण है:**  
`extract_hyperlinks` **extract hyperlinks from html** का मुख्य भाग है। यह गायब `href` एट्रिब्यूट को सुगमता से संभालता है, रिलेटिव लिंक को हल करता है, और एक साधारण Python सूची लौटाता है जिसे आप आगे की प्रोसेसिंग (जैसे, requests, pandas, या डेटाबेस) में उपयोग कर सकते हैं।

## पूरा अंत‑से‑अंत उदाहरण

तीन फ़ंक्शनों को मिलाकर आपको एक स्क्रिप्ट मिलती है जो फ़ाइल लोड करती है, सभी एंकर चुनती है, और प्रत्येक hyperlink को प्रिंट करती है।

```python
# parse_links.py
from lxml import html
from urllib.parse import urljoin
from typing import Optional

def load_html(path: str) -> html.HtmlElement:
    with open(path, "r", encoding="utf-8") as f:
        return html.fromstring(f.read())

def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    return doc.cssselect("a")

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

if __name__ == "__main__":
    # 1️⃣ Load the HTML document
    document = load_html("sample.html")
    # 2️⃣ Use selector to grab all <a> tags
    anchor_elements = select_links(document)
    # 3️⃣ Extract and print each hyperlink
    for url in extract_hyperlinks(anchor_elements, base_url="https://example.com"):
        print(url)
```

`python parse_links.py` चलाने से प्रत्येक hyperlink, पूरी तरह से रिजॉल्व्ड, कंसोल पर प्रिंट होता है। यह स्क्रिप्ट **how to parse html**, **how to use selector**, और **extract hyperlinks from html** को एक ही पुन: उपयोग योग्य फ्लो में दर्शाती है।

## सामान्य विविधताएँ और एज‑केस हैंडलिंग

| Situation | What to change | Reason |
|-----------|----------------|--------|
| **केवल absolute URLs चाहिए** | `extract_hyperlinks` में `base_url` आर्ग्यूमेंट को छोड़ दें | रिलेटिव URLs को जैसा है वैसा रखता है |
| **आपको लिंक टेक्स्ट भी चाहिए** | `extract_hyperlinks` से ट्यूपल `(href, link.text_content())` रिटर्न करें | आपको URL और एंकर टेक्स्ट दोनों को स्टोर करने की अनुमति देता है |
| **बड़े HTML फ़ाइलें** | `lxml.etree.iterparse` को CSS selector फ़िल्टर के साथ उपयोग करें | स्ट्रीमिंग द्वारा मेमोरी उपयोग कम करता है |
| **विभिन्न selector** | `"a"` को `"nav a[href]"` या `"div.content a.external"` से बदलें | लिंक का एक उपसमुच्चय लक्षित करता है, जटिल पेजों में **how to use selector** के लिए उपयोगी |

**Pro tip:** नेटवर्क अनुरोध करने से पहले हमेशा निकाले गए URLs को वैलिडेट करें। एक तेज़ `urlparse` चेक खराब स्ट्रिंग्स को फ़िल्टर कर सकता है और आपके स्क्रैपर को क्रैश से बचा सकता है।

## निष्कर्ष

अब आप Python में **how to parse html**, **load html document python**, तत्वों को लक्षित करने के लिए **how to use selector**, और **extract hyperlinks from html** को प्रभावी ढंग से करना जानते हैं। ऊपर दिया गया पूरा उदाहरण आपके प्रोजेक्ट में कॉपी‑पेस्ट करने के लिए तैयार है, और आप प्रत्येक फ़ंक्शन को अधिक उन्नत उपयोग मामलों जैसे पेजिनेशन, JavaScript‑जनित कंटेंट, या मल्टी‑पेज क्रॉलिंग के लिए अनुकूलित कर सकते हैं।

अगले कदम जिनका आप अन्वेषण कर सकते हैं:

- **requests‑html** या **Playwright** का उपयोग करके उन पेजों को फ़ेच करें जिन्हें JavaScript निष्पादन की आवश्यकता है।  
- निकाले गए URLs को बाद में विश्लेषण के लिए CSV या SQLite डेटाबेस में स्टोर करें।  
- नेटवर्क टाइमआउट और HTTP स्टेटस कोड के लिए एरर हैंडलिंग जोड़ें।

पार्सिंग का आनंद लें, और विभिन्न selectors के साथ प्रयोग करने में संकोच न करें ताकि Python में CSS‑आधारित HTML क्वेरीज़ की पूरी शक्ति को अनलॉक किया जा सके!

## आप को आगे क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ का अन्वेषण करने में मदद करती हैं।

- [Python में HTML रिसोर्स हैंडलिंग कैसे कॉन्फ़िगर करें और HTML दस्तावेज़ लोड करें](/html/english/python/general/how-to-configure-html-resource-handling-in-python-and-load-a/)
- [Python में HTML कैसे पार्स करें – पूर्ण गाइड](/html/english/python/general/how-to-parse-html-in-python-complete-guide/)
- [Python में HTML कैसे लोड करें – चरण‑दर‑चरण गाइड](/html/english/python/general/how-to-load-html-in-python-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
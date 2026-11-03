---
category: general
date: 2026-07-18
description: Python में HTML को जल्दी से EPUB में बदलें। Python में HTML फ़ाइल को
  लोड करना सीखें और सरल लाइब्रेरीज़ का उपयोग करके HTML को MHTML में भी बदलें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to epub
- load html file in python
- convert html to mhtml
language: hi
lastmod: 2026-07-18
og_description: Python में स्पष्ट, चलाने योग्य उदाहरण के साथ HTML को EPUB में बदलें।
  साथ ही सीखें कि Python में HTML फ़ाइल कैसे लोड करें और मिनटों में HTML को MHTML
  में कैसे बदलें।
og_image_alt: Diagram showing convert html to epub workflow
og_title: Python में HTML को EPUB में परिवर्तित करें – पूर्ण ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  headline: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  name: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Python 3.9+** – the syntax used here works on any recent version.'
    text: '**Python 3.9+** – the syntax used here works on any recent version.'
  - name: '**pip** – to install third‑party packages.'
    text: '**pip** – to install third‑party packages.'
  - name: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
    text: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
  type: HowTo
tags:
- python
- html
- epub
- mhtml
- file conversion
title: Python में HTML को EPUB में बदलें – पूर्ण चरण‑दर‑चरण गाइड
url: /hi/python/general/convert-html-to-epub-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में HTML को EPUB में बदलें – पूर्ण चरण‑दर‑चरण गाइड

क्या आपने कभी सोचा है कि **HTML को EPUB में बदलना** कितना आसान हो सकता है, बिना सिर दर्द के? आप अकेले नहीं हैं—डेवलपर्स को लगातार वेब पेजों को ऑफ़लाइन पढ़ने के लिए ई‑बुक में बदलना पड़ता है, और Python में यह करना आश्चर्यजनक रूप से सरल है। इस ट्यूटोरियल में हम Python में एक HTML फ़ाइल लोड करने, उस HTML को EPUB में बदलने, और उसी स्रोत को MHTML में बदलने की प्रक्रिया को समझेंगे, जिससे ई‑मेल‑फ़्रेंडली आर्काइव बन सके।

गाइड के अंत तक आपके पास एक तैयार‑चलाने‑योग्य स्क्रिप्ट होगी जो एक `sample.html` फ़ाइल लेती है और `sample.epub` तथा `sample.mhtml` दोनों बनाती है। कोई रहस्य नहीं, सिर्फ स्पष्ट कोड और व्याख्याएँ।

---

![Conversion pipeline diagram](https://example.com/images/convert-html-epub.png "Diagram showing convert html to epub workflow")

## आप क्या बनाएँगे

- **Python में HTML फ़ाइल लोड करना** बिल्ट‑इन `pathlib` और `io` मॉड्यूल का उपयोग करके।  
- **HTML को EPUB में बदलना** `ebooklib` लाइब्रेरी के साथ, जो आपके लिए EPUB कंटेनर फ़ॉर्मेट को संभालती है।  
- **HTML को MHTML** (जिसे MHT भी कहा जाता है) में बदलना `email` पैकेज का उपयोग करके, जिससे एक सिंगल‑फ़ाइल वेब आर्काइव बनता है जिसे ब्राउज़र सीधे खोल सकते हैं।  

हम additionally कवर करेंगे:

- आवश्यक डिपेंडेंसीज़ और उन्हें कैसे इंस्टॉल करें।  
- एरर हैंडलिंग ताकि आपका स्क्रिप्ट सुगमता से फेल हो।  
- EPUB फ़ाइल के लिए शीर्षक और लेखक जैसे मेटाडेटा को कैसे कस्टमाइज़ करें।  

तैयार हैं? चलिए शुरू करते हैं।

---

## आवश्यकताएँ

कोड लिखना शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

1. **Python 3.9+** – यहाँ उपयोग किया गया सिंटैक्स किसी भी हालिया संस्करण पर काम करता है।  
2. **pip** – थर्ड‑पार्टी पैकेज इंस्टॉल करने के लिए।  
3. एक साधारण HTML फ़ाइल, जैसे `sample.html`, जिसे आप किसी फ़ोल्डर में रख सकते हैं।  

यदि आपके पास ये सब है, तो बढ़िया—अगले सेक्शन पर जाएँ।  

> **Pro tip:** अपना HTML अच्छी तरह से फॉर्मेटेड रखें (सही `<head>` और `<body>` सेक्शन)। जबकि `ebooklib` छोटे‑छोटे मुद्दों को ठीक करने की कोशिश करेगा, एक साफ़ स्रोत बाद में सिरदर्द बचाता है।

---

## चरण 1 – आवश्यक लाइब्रेरीज़ इंस्टॉल करें

हमें दो बाहरी पैकेज चाहिए:

- **ebooklib** – EPUB जेनरेशन के लिए।  
- **beautifulsoup4** – वैकल्पिक, लेकिन HTML को क्लीन करने में मददगार।

टर्मिनल में यह कमांड चलाएँ:

```bash
pip install ebooklib beautifulsoup4
```

> **इन लाइब्रेरीज़ की जरूरत क्यों है?** `ebooklib` आपके लिए ZIP‑आधारित EPUB स्ट्रक्चर बनाता है, `META‑INF` फ़ोल्डर, `content.opf`, और `toc.ncx` को ऑटोमैटिकली हैंडल करता है। `beautifulsoup4` हमें HTML को साफ़ करने देता है, जिससे अंतिम ई‑बुक सभी रीडर्स पर सही रेंडर होती है।

---

## चरण 2 – Python में HTML फ़ाइल लोड करें

HTML फ़ाइल लोड करना सीधा है, लेकिन हम इसे एक छोटे हेल्पर फ़ंक्शन में रैप करेंगे जो बाद में प्रोसेसिंग के लिए **BeautifulSoup** ऑब्जेक्ट रिटर्न करता है।

```python
from pathlib import Path
from bs4 import BeautifulSoup

def load_html(filepath: str) -> BeautifulSoup:
    """
    Load an HTML file from disk and return a BeautifulSoup object.
    Raises FileNotFoundError if the file does not exist.
    """
    path = Path(filepath)
    if not path.is_file():
        raise FileNotFoundError(f"HTML file not found: {filepath}")

    # Read the file using UTF‑8 encoding (most common for web content)
    html_content = path.read_text(encoding="utf-8")
    # Parse with BeautifulSoup for optional cleaning later
    soup = BeautifulSoup(html_content, "html.parser")
    return soup
```

**व्याख्या:**  
- `Path` हमें OS‑इंडिपेंडेंट फ़ाइल हैंडलिंग देता है।  
- `read_text` का उपयोग करके हम मैन्युअल `open`/`close` बायलरप्लेट से बचते हैं।  
- `BeautifulSoup` ऑब्जेक्ट रिटर्न करने से हम बाद में स्क्रिप्ट, टूटे टैग हटाने, या स्टाइलशीट इन्जेक्ट करने जैसे काम कर सकते हैं, इससे पहले कि हम **HTML को EPUB में बदलें**।

---

## चरण 3 – HTML को EPUB में बदलें

अब जब हम **Python में HTML फ़ाइल लोड** कर सकते हैं, तो इसे एक साफ़ EPUB में ट्रांसफ़ॉर्म करते हैं। नीचे दिया फ़ंक्शन एक `BeautifulSoup` ऑब्जेक्ट, डेस्टिनेशन पाथ, और वैकल्पिक मेटाडेटा लेता है।

```python
import uuid
from ebooklib import epub

def html_to_epub(soup: BeautifulSoup,
                 output_path: str,
                 title: str = "Untitled Book",
                 author: str = "Anonymous") -> None:
    """
    Convert a BeautifulSoup HTML document to an EPUB file.
    """
    # Create a new EPUB book instance
    book = epub.EpubBook()

    # Set basic metadata – this is what shows up in e‑reader libraries
    book.set_identifier(str(uuid.uuid4()))
    book.set_title(title)
    book.set_language('en')
    book.add_author(author)

    # Convert the soup back to a string; we could also clean it here
    html_str = str(soup)

    # Create a chapter (EPUB requires at least one)
    chapter = epub.EpubHtml(title=title,
                            file_name='chap_01.xhtml',
                            lang='en')
    chapter.content = html_str
    book.add_item(chapter)

    # Define the spine (reading order) and table of contents
    book.toc = (epub.Link('chap_01.xhtml', title, 'intro'),)
    book.spine = ['nav', chapter]

    # Add default navigation files
    book.add_item(epub.EpubNcx())
    book.add_item(epub.EpubNav())

    # Write the final EPUB file
    epub.write_epub(output_path, book, {})

    print(f"✅ EPUB created at: {output_path}")
```

**यह क्यों काम करता है:**  
- `ebooklib.epub.EpubBook` ZIP कंटेनर और आवश्यक मैनिफेस्ट फ़ाइलों को एब्स्ट्रैक्ट करता है।  
- हम एक UUID को आइडेंटिफ़ायर के रूप में जेनरेट करते हैं ताकि कई बुक्स बनाते समय डुप्लिकेट ID न हो।  
- `spine` रीडर्स को अध्यायों का क्रम बताता है; अधिकांश साधारण HTML स्रोतों के लिए एक‑अध्याय बुक पर्याप्त है।  

**कन्वर्ज़न चलाना:**

```python
if __name__ == "__main__":
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_epub(html_doc,
                 "YOUR_DIRECTORY/sample.epub",
                 title="My Sample eBook",
                 author="Jane Developer")
```

जब आप स्क्रिप्ट चलाएँगे, तो आपको एक हरा चेक‑मार्क दिखेगा जो EPUB फ़ाइल के स्थान की पुष्टि करता है।

---

## चरण 4 – HTML को MHTML में बदलें

MHTML (या MHT) HTML और उसकी सभी रिसोर्सेज (इमेज, CSS) को एक सिंगल MIME फ़ाइल में बंडल करता है। Python का `email` पैकेज इस फ़ॉर्मेट को बाहरी डिपेंडेंसीज़ के बिना बना सकता है।

```python
import mimetypes
import base64
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from email.mime.base import MIMEBase
from email import encoders

def html_to_mhtml(soup: BeautifulSoup,
                  output_path: str,
                  base_url: str = "") -> None:
    """
    Convert a BeautifulSoup HTML document to an MHTML file.
    `base_url` is used to resolve relative resource links.
    """
    # Create the multipart/related container required for MHTML
    mhtml = MIMEMultipart('related')
    mhtml['Subject'] = 'Converted MHTML document'
    mhtml['Content-Type'] = 'multipart/related; type="text/html"'

    # Main HTML part
    html_part = MIMEText(str(soup), 'html', 'utf-8')
    html_part.add_header('Content-Location', 'file://index.html')
    mhtml.attach(html_part)

    # Optional: embed images referenced in the HTML
    for img in soup.find_all('img'):
        src = img.get('src')
        if not src:
            continue

        # Resolve absolute path if needed
        img_path = Path(base_url) / src if base_url else Path(src)
        if not img_path.is_file():
            continue  # skip missing files

        # Guess MIME type; default to octet-stream
        mime_type, _ = mimetypes.guess_type(img_path)
        mime_type = mime_type or 'application/octet-stream'

        with img_path.open('rb') as f:
            img_data = f.read()

        img_part = MIMEBase(*mime_type.split('/'))
        img_part.set_payload(img_data)
        encoders.encode_base64(img_part)
        img_part.add_header('Content-Location', f'file://{src}')
        img_part.add_header('Content-Transfer-Encoding', 'base64')
        mhtml.attach(img_part)

    # Write the MHTML file
    with open(output_path, 'wb') as out_file:
        out_file.write(mhtml.as_bytes())

    print(f"✅ MHTML created at: {output_path}")
```

**मुख्य बिंदु:**  

- `multipart/related` MIME टाइप ब्राउज़र्स को बताता है कि HTML पार्ट और उसकी रिसोर्सेज एक साथ हैं।  
- हम `<img>` टैग्स के माध्यम से इमेजेस को एम्बेड करते हैं; यदि आपको इमेज की ज़रूरत नहीं है, तो इस ब्लॉक को स्किप कर सकते हैं।  
- `Content-Location` एक `file://` URI उपयोग करता है ताकि ब्राउज़र रिसोर्सेज को इंटर्नली रिज़ॉल्व कर सके।  

**फ़ंक्शन को कॉल करना:**

```python
if __name__ == "__main__":
    # Re‑use the previously loaded soup
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_mhtml(html_doc, "YOUR_DIRECTORY/sample.mhtml", base_url="YOUR_DIRECTORY")
```

अब आपके पास `sample.epub` और `sample.mhtml` दोनों साइड‑बाय‑साइड मौजूद हैं।

---

## पूर्ण स्क्रिप्ट – सभी चरण एक फ़ाइल में

नीचे पूरी, तैयार‑चलाने‑योग्य स्क्रिप्ट है जो सब कुछ जोड़ती है। इसे `convert_html.py` के रूप में सेव करें और `YOUR_DIRECTORY` को उस पाथ से बदलें जहाँ आपका `sample.html` स्थित है।



## आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स इस गाइड में दिखाए गए तकनीकों पर आधारित हैं और आपको अतिरिक्त API फीचर्स में महारत हासिल करने तथा अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर करने में मदद करेंगे।

- [How to Convert HTML to MHTML with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [How to Convert EPUB to PDF with Java – Using Aspose.HTML](/html/english/java/converting-epub-to-pdf/convert-epub-to-pdf/)
- [How to Convert EPUB to Images with Aspose.HTML for Java](/html/english/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
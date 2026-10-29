---
category: general
date: 2026-08-06
description: Python में HTML को PDF में बदलें, एक पूर्ण उदाहरण के साथ। HTML से PDF
  उत्पन्न करना सीखें, HTML को PDF के रूप में सहेजें, और सामान्य किनारी मामलों को संभालें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to pdf
- generate pdf from html
- save html as pdf
- create pdf from html file
- how to convert html to pdf
language: hi
lastmod: 2026-08-06
og_description: Python में HTML को PDF में बदलें और दस्तावेज़ निर्माण को स्वचालित
  करें। इस गाइड का पालन करके HTML से PDF बनाएं, HTML को PDF के रूप में सहेजें, और
  आउटपुट को कस्टमाइज़ करें।
og_image_alt: Example of convert html to pdf script in Python
og_title: Python में HTML को PDF में बदलें – व्यापक ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-08-06'
  description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  headline: Convert HTML to PDF in Python – step‑by‑step guide
  type: TechArticle
- description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  name: Convert HTML to PDF in Python – step‑by‑step guide
  steps:
  - name: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
    text: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
  - name: '**Input handling** – read the HTML file or build the markup programmatically.'
    text: '**Input handling** – read the HTML file or build the markup programmatically.'
  - name: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
    text: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
  type: HowTo
tags:
- HTML to PDF
- Python
- Document conversion
title: Python में HTML को PDF में बदलें – चरण‑दर‑चरण मार्गदर्शिका
url: /hi/python/general/convert-html-to-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में HTML को PDF में परिवर्तित करें – चरण‑दर‑चरण गाइड

यदि आपको **HTML को PDF में** जल्दी बदलना है, तो यह ट्यूटोरियल Python में एक पूर्ण समाधान दिखाता है। आप देखेंगे कि HTML से PDF कैसे जनरेट करें, HTML को PDF के रूप में सहेजें, और कोड से बाहर निकले बिना रूपांतरण प्रक्रिया को नियंत्रित करें।

यह गाइड आपको विश्वसनीय लाइब्रेरी स्थापित करने, HTML दस्तावेज़ लोड करने, रूपांतरण करने और परिणाम की पुष्टि करने की पूरी प्रक्रिया से परिचित कराता है। अंत तक आप किसी भी Python प्रोजेक्ट में, चाहे स्रोत स्थैतिक पेज हो या गतिशील रूप से उत्पन्न मार्कअप, HTML फ़ाइल से PDF बना सकते हैं।

## आप क्या सीखेंगे

* HTML‑to‑PDF रूपांतरण के लिए आवश्यक `pdfkit` और `wkhtmltopdf` निर्भरताएँ स्थापित करें।  
* डिस्क या स्ट्रिंग से HTML दस्तावेज़ लोड करें।  
* कस्टम पेज साइज, मार्जिन और एन्कोडिंग विकल्पों के साथ HTML से PDF जनरेट करें।  
* एकल फ़ंक्शन कॉल का उपयोग करके HTML को PDF के रूप में सहेजें।  
* गुम एसेट्स, यूनिकोड कैरेक्टर्स, और बड़े फ़ाइलों जैसे सामान्य एज केसों को संभालें।  

**पूर्वापेक्षाएँ** – Python 3.8+ और फ़ाइल I/O की बुनियादी समझ। कोई बाहरी सेवाएँ आवश्यक नहीं हैं।

## HTML को PDF में बदलें – समग्र कार्यप्रवाह

रूपांतरण प्रक्रिया तीन तार्किक चरणों में विभाजित है:

1. **तैयारी** – कनवर्टर स्थापित करें और सुनिश्चित करें कि `wkhtmltopdf` बाइनरी पहुंच योग्य है।  
2. **इनपुट हैंडलिंग** – HTML फ़ाइल पढ़ें या प्रोग्रामेटिक रूप से मार्कअप बनाएं।  
3. **आउटपुट जेनरेशन** – कनवर्टर को कॉल करें, PDF फ़ाइल लिखें, और परिणाम की पुष्टि करें।  

प्रत्येक चरण नीचे समर्पित चरण में कवर किया गया है।

## चरण 1: आवश्यक लाइब्रेरी स्थापित करें

`pdfkit` व्यापक रूप से उपयोग किए जाने वाले `wkhtmltopdf` इंजन के चारों ओर एक हल्का Python रैपर प्रदान करता है। दोनों को `pip` से स्थापित करें और बाइनरी पाथ की जाँच करें।

```bash
# Install the Python wrapper
pip install pdfkit

# On Ubuntu/Debian install wkhtmltopdf package
sudo apt-get install wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf
```

यदि आप पोर्टेबल बाइनरी पसंद करते हैं, तो उपयुक्त रिलीज़ को [wkhtmltopdf GitHub page](https://github.com/wkhtmltopdf/wkhtmltopdf/releases) से डाउनलोड करें और उसे उस डायरेक्टरी में रखें जो आपके `PATH` में जोड़ी गई है। स्क्रिप्ट बाद में पाथ को स्वचालित रूप से जाँचती है।

## चरण 2: HTML दस्तावेज़ लोड करें

आप स्थैतिक फ़ाइल पढ़ सकते हैं, रिमोट कंटेंट फ़ेच कर सकते हैं, या ऑन‑द‑फ़्लाई HTML बना सकते हैं। नीचे का उदाहरण एक स्थानीय फ़ाइल `sample.html` को लोड करता है, जिसे आप अपनी परिभाषित डायरेक्टरी में रख सकते हैं।

```python
import pathlib
import pdfkit

# Define the directory that holds the HTML source
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")

# Resolve the full path to the HTML file
html_path = BASE_DIR / "sample.html"

# Read the file content as a UTF‑8 string
with html_path.open(encoding="utf-8") as f:
    html_content = f.read()
```

फ़ाइल को यूनिकोड स्ट्रिंग के रूप में पढ़ने से यह सुनिश्चित होता है कि “é”, “ß”, या एशियाई ग्लिफ़ जैसे अक्षर रूपांतरण के दौरान संरक्षित रहें। यह चरण तब आवश्यक है जब आप **HTML से PDF जनरेट** करते हैं जिसमें अंतर्राष्ट्रीय टेक्स्ट शामिल हो।

## चरण 3: HTML से PDF जनरेट करें

`pdfkit.from_string` HTML मार्कअप वाली स्ट्रिंग को PDF फ़ाइल में बदलता है। आप पेज साइज, मार्जिन और हेडर/फ़ूटर व्यवहार को नियंत्रित करने के लिए विकल्पों की डिक्शनरी पास कर सकते हैं।

```python
# Define the output PDF path
pdf_path = BASE_DIR / "sample.pdf"

# Conversion options – adjust as needed
options = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left": "0.75in",
    "encoding": "UTF-8",
    "enable-local-file-access": None,  # Allows loading local images/CSS
}

# Perform the conversion
pdfkit.from_string(html_content, str(pdf_path), options=options)
```

ऊपर का कॉल **sample.pdf** में संग्रहीत HTML फ़ाइल से PDF बनाता है। यदि स्रोत HTML स्थानीय CSS या इमेजेज़ को रेफ़र करता है, तो `enable‑local‑file‑access` फ़्लैग `wkhtmltopdf` को उन रिसोर्सेज़ को रिजॉल्व करने की अनुमति देता है।

### यह तरीका क्यों काम करता है

* `pdfkit` भारी काम `wkhtmltopdf` को सौंपता है, जो WebKit इंजन के साथ HTML रेंडर करता है, जिससे मूल लेआउट की उच्च सटीकता सुनिश्चित होती है।  
* ऑप्शन डिक्शनरी प्रदान करने से आप आउटपुट को HTML को बदले बिना बारीकी से ट्यून कर सकते हैं।  
* `from_string` का उपयोग करने से वर्कफ़्लो मेमोरी में रहता है, जो तब उपयोगी है जब HTML ऑन‑द‑फ़्लाई जनरेट किया जाता है।

## चरण 4: HTML को PDF के रूप में सहेजें और आउटपुट की पुष्टि करें

रूपांतरण के बाद, आप यह पुष्टि करना चाह सकते हैं कि PDF मौजूद है और पढ़ा जा सकता है। नीचे का स्निपेट फ़ाइल आकार जाँचता है और डिफ़ॉल्ट सिस्टम व्यूअर (प्लेटफ़ॉर्म‑विशिष्ट) के साथ PDF खोलता है।

```python
import os
import subprocess
import sys

# Verify that the PDF file was created
if pdf_path.is_file() and pdf_path.stat().st_size > 0:
    print(f"✅ PDF generated successfully: {pdf_path}")

    # Open the PDF for visual verification (optional)
    if sys.platform.startswith("darwin"):      # macOS
        subprocess.run(["open", str(pdf_path)])
    elif os.name == "nt":                      # Windows
        os.startfile(str(pdf_path))
    else:                                      # Linux and others
        subprocess.run(["xdg-open", str(pdf_path)])
else:
    raise FileNotFoundError("PDF generation failed – file not found or empty.")
```

स्क्रिप्ट चलाने पर एक सफलता संदेश प्रदर्शित होता है और PDF व्यूअर लॉन्च होता है ताकि आप तुरंत पुष्टि कर सकें कि लेआउट मूल HTML से मेल खाता है। यह चरण **save html as pdf** चक्र को पूरा करता है।

## चरण 5: उन्नत विकल्प – कस्टम सेटिंग्स के साथ HTML फ़ाइल से PDF बनाएं

कभी‑कभी आपके पास डिस्क पर एक वास्तविक HTML फ़ाइल होती है और आप स्वयं कंटेंट लोड करने के बजाय `pdfkit.from_file` को पसंद करते हैं। यह विधि तब उपयोगी होती है जब HTML में पहले से जटिल रिलेटिव पाथ्स शामिल हों।

```python
# Directly convert a file path to PDF
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

आप कवर पेज, टेबल ऑफ कंटेंट्स, या जावास्क्रिप्ट एक्सीक्यूशन फ़्लैग्स को `options` डिक्शनरी में जोड़कर एम्बेड कर सकते हैं। उदाहरण के लिए, कवर पेज जोड़ने के लिए:

```python
options.update({
    "cover": str(BASE_DIR / "cover.html"),
    "toc": None,  # Generates a table of contents
})
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

ये बदलाव **HTML को PDF में कैसे बदलें** के लिए अधिक परिष्कृत प्रकाशन पाइपलाइन दर्शाते हैं।

## सामान्य समस्याएँ और उनका समाधान

| समस्या | कारण | समाधान |
|-------|-------|--------|
| छवियां या CSS नहीं दिख रही हैं | `wkhtmltopdf` डिफ़ॉल्ट रूप से स्थानीय फ़ाइल एक्सेस को ब्लॉक करता है | ऑप्शन डिक्शनरी में `"enable-local-file-access": None` जोड़ें |
| Unicode अक्षर गड़बड़ हो जाते हैं | `encoding` विकल्प गायब है या फ़ाइल को गलत charset से पढ़ा गया है | हमेशा `"encoding": "UTF-8"` सेट करें और HTML फ़ाइल को UTF‑8 से पढ़ें |
| PDF खाली है | `wkhtmltopdf` बाइनरी का पाथ गलत है | पाथ स्पष्ट रूप से दें: `pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")` |
| बड़ी HTML फ़ाइलें टाइमआउट का कारण बनती हैं | डिफ़ॉल्ट टाइमआउट बहुत छोटा है | `"javascript-delay": "2000"` सेट करें या `"timeout": "60"` के साथ टाइमआउट बढ़ाएँ |

इन समस्याओं का समाधान करने से विभिन्न वातावरणों में एक विश्वसनीय **generate pdf from html** प्रक्रिया सुनिश्चित होती है।

## पूर्ण स्क्रिप्ट – एंड‑टू‑एंड उदाहरण

निम्नलिखित को `html_to_pdf.py` के रूप में सहेजें और `python html_to_pdf.py` से चलाएँ। `YOUR_DIRECTORY` को अपने प्रोजेक्ट फ़ोल्डर की ओर इंगित करने के लिए बदलें।

```python
#!/usr/bin/env python3
"""
Convert HTML to PDF in Python – complete, runnable example.
"""

import pathlib
import pdfkit
import os
import subprocess
import sys

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")          # <-- change this
HTML_FILE = BASE_DIR / "sample.html"
PDF_FILE = BASE_DIR / "sample.pdf"

# wkhtmltopdf configuration (optional – only needed if binary is not on PATH)
# config = pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")

# Conversion options – customize as required
OPTIONS = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left":


## आपको आगे क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स इस गाइड में प्रदर्शित तकनीकों पर आधारित निकटतम संबंधित विषयों को कवर करते हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में निपुण होने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [HTML को PDF में बदलने का तरीका Java – Aspose.HTML for Java का उपयोग करके](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Aspose.HTML के साथ .NET में HTML को PDF में बदलें](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [HTML को PDF में बदलने का तरीका Java - Aspose.HTML के साथ पेज मार्जिन सेट करें](/html/english/java/advanced-usage/css-extensions-adding-title-page-number/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
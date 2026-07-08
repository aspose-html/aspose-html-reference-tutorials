---
category: general
date: 2026-07-02
description: วิธีดึงไอคอนจากไฟล์ HTML ด้วย Python. เรียนรู้การอ่านไฟล์ HTML ด้วย Python,
  แยกวิเคราะห์เอกสาร HTML, และดึงแอตทริบิวต์ href เพื่อรับ URL ของ favicon.
draft: false
keywords:
- how to extract icons
- read html file python
- parse html document
- extract href attribute
- extract favicon urls
language: th
og_description: วิธีดึงไอคอนจากหน้า HTML ด้วย Python บทเรียนนี้จะแสดงวิธีอ่านไฟล์
  HTML ด้วย Python, แยกวิเคราะห์เอกสาร, และดึง URL ของ favicon ออกมา
og_title: วิธีสกัดไอคอนจาก HTML – คู่มือ Python
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: How to extract icons from an HTML file using Python. Learn to read
    HTML file python, parse HTML document, and extract href attribute to get favicon
    URLs.
  headline: How to Extract Icons from HTML with Python – Complete Guide
  type: TechArticle
- questions:
  - answer: Some sites embed icons via `<meta itemprop="image">`. Extend `is_icon_link`
      to also check for `meta` with `itemprop="image"` and pull its `content` attribute.
    question: What if the HTML uses `<meta>` tags for icons?
  - answer: Yes—just feed each URL into `requests.get(url, stream=True)` and write
      the content to a file. Remember to handle relative URLs with `urljoin`.
    question: Can I fetch the icons automatically?
  - answer: 'Absolutely. Replace the file‑reading step with `requests.get(page_url).text`
      and pass the HTML string to BeautifulSoup. Just be mindful of robots.txt and
      rate limits. --- ## Wrap‑Up We’ve covered **how to extract icons** from any
      static HTML using Python, from reading the file to printing out each f'
    question: Does this work on remote pages?
  type: FAQPage
tags:
- python
- html-parsing
- web‑scraping
- favicon
title: วิธีดึงไอคอนจาก HTML ด้วย Python – คู่มือฉบับสมบูรณ์
url: /th/python/general/how-to-extract-icons-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีดึงไอคอนจาก HTML ด้วย Python – คู่มือฉบับสมบูรณ์

เคยสงสัย **วิธีดึงไอคอน** จากเว็บเพจโดยไม่ต้องเปิดเบราว์เซอร์หรือไม่? บางทีคุณอาจกำลังสร้างแคตาล็อกไซต์, เครื่องมือการตรวจสอบ SEO, หรือแค่อยากรู้เกี่ยวกับ favicon เล็ก ๆ ที่ปรากฏในแท็บ ข่าวดีคือคุณสามารถทำได้ด้วยไม่กี่บรรทัดของ Python—ไม่ต้องใช้ Selenium, ไม่ต้องใช้ Chrome แบบ headless, เพียงไฟล์ HTML แบบข้อความธรรมดา.

ในบทแนะนำนี้เราจะเดินผ่านการอ่านไฟล์ HTML ด้วย Python, การแยกวิเคราะห์เอกสาร HTML, และสุดท้าย **การดึงแอตทริบิวต์ href** จากแท็ก `<link rel="icon">` เพื่อให้ได้ URL ของ favicon เหล่านั้น เมื่อจบคุณจะมีสคริปต์ที่นำกลับมาใช้ใหม่ได้ซึ่งทำงานกับ HTML แบบสถิตใด ๆ ที่คุณใส่เข้าไป, และคุณยังจะได้เห็นวิธีจัดการกับกรณีขอบเช่นเส้นทางแบบ relative หรือการประกาศไอคอนหลายรายการ.

## สิ่งที่คุณจะได้เรียนรู้

- โหลดไฟล์ HTML ในเครื่องด้วย Python (read html file python)  
- ใช้พาร์เซอร์ขนาดเล็กเพื่อ **parse html document** อย่างปลอดภัย  
- ค้นหาองค์ประกอบ `<link>` ที่ประกาศไอคอน  
- **Extract href attribute** ค่าและแปลงเป็น URL แบบเต็ม  
- รวบรวมและพิมพ์ **favicon URLs** ทั้งหมดที่ค้นพบ  

No external services required—just the standard library and the popular **BeautifulSoup** package.

![ภาพหน้าจอแสดงสคริปต์ Python ดึงไอคอน – วิธีดึงไอคอน](https://example.com/images/extract-icons-python.png "วิธีดึงไอคอน")

*ข้อความแทนภาพ: "วิธีดึงไอคอนโดยใช้สคริปต์ Python"*

## ข้อกำหนดเบื้องต้น

- ติดตั้ง Python 3.8+  
- ไลบรารี `beautifulsoup4` (`pip install beautifulsoup4`)  
- ไฟล์ HTML ในเครื่องที่คุณต้องการสแกน (เช่น `sample.html`)  

ถ้าคุณมีทั้งหมดแล้ว, ไปกันเลย.

## ขั้นตอนที่ 1: อ่านไฟล์ HTML ด้วย Python – โหลดเอกสาร

สิ่งแรกที่ต้องทำคือเปิดไฟล์และส่งเนื้อหาให้พาร์เซอร์. การใช้ `with open(..., "r", encoding="utf‑8")` รับประกันว่าไฟล์จะถูกปิดโดยอัตโนมัติ, และการเข้ารหัส UTF‑8 จัดการกับหน้าเว็บสมัยใหม่ส่วนใหญ่.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Step 1: Load the HTML document from disk
html_path = Path("sample.html")          # adjust the path as needed
html_content = html_path.read_text(encoding="utf-8")
```

**ทำไมสิ่งนี้ถึงสำคัญ:** การเปิดไฟล์ด้วยการเข้ารหัสที่ถูกต้องป้องกันอักขระ `�` ที่ไม่คาดคิดซึ่งอาจทำให้พาร์เซอร์พังในภายหลัง. การใช้ `Path` จากไลบรารีมาตรฐานยังทำให้โค้ดทำงานข้ามแพลตฟอร์มได้.

## ขั้นตอนที่ 2: แยกวิเคราะห์เอกสาร HTML – ค้นหาไอคอนลิงก์ทั้งหมด

ตอนนี้เราจะส่ง HTML ดิบให้กับ **BeautifulSoup**, ซึ่งจะสร้างต้นไม้ที่สามารถนำทางได้. เราจะค้นหาแท็ก `<link>` ทุกตัวที่แอตทริบิวต์ `rel` มีคำว่า `icon`. โปรดทราบว่า `rel` อาจเป็นรายการคั่นด้วยช่องว่าง (`rel="shortcut icon"`), ดังนั้นเราต้องตรวจสอบอย่างยืดหยุ่น.

```python
# Step 2: Parse the HTML and locate <link> tags that declare an icon
soup = BeautifulSoup(html_content, "html.parser")

def is_icon_link(tag):
    """Return True if a <link> tag declares an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    # BeautifulSoup may return a list or a string; handle both
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

icon_links = [tag for tag in soup.find_all(is_icon_link)]
```

**ทำไมขั้นตอนนี้ถึงสำคัญ:** การใช้ `soup.find_all("link", rel="icon")` อย่างง่ายจะพลาดรูปแบบเช่น `rel="shortcut icon"` หรือ `rel="apple-touch-icon"`. ตัวช่วย `is_icon_link` ของเราครอบคลุมกรณีเหล่านั้น, ทำให้การดึงข้อมูลมั่นคง.

## ขั้นตอนที่ 3: ดึงแอตทริบิวต์ href – ดึง URL

เมื่อได้แท็กที่เกี่ยวข้องแล้ว, เราจะดึงแอตทริบิวต์ `href` จากแต่ละแท็ก. บางหน้าอาจไม่มี `href` (หายากแต่เป็นไปได้), ดังนั้นเราตรวจสอบให้ไม่เป็น `None`. นอกจากนี้ favicon มักระบุด้วย URL แบบ relative, เราจะทำการ resolve กับ base URL ของหน้า หากคุณรู้. สำหรับไฟล์ในเครื่อง เราจะเก็บเส้นทางไว้ตามเดิม.

```python
# Step 3: Grab the href attribute from each icon link
icon_urls = []
for tag in icon_links:
    href = tag.get("href")
    if href:
        icon_urls.append(href.strip())
```

**ทำไมเราต้องลบช่องว่าง:** ผู้เขียน HTML บางครั้งอาจใส่ช่องว่างรอบ URL โดยไม่ได้ตั้งใจ, ซึ่งจะทำให้การร้องขอถัดไปล้มเหลว. การตัดช่องว่างทำให้ได้สตริงที่สะอาด.

## ขั้นตอนที่ 4: ดึง URL ของ Favicon – แสดงผลลัพธ์

สุดท้าย, เราจะพิมพ์ (หรือคืนค่า) รายการ URL ที่ค้นพบ. ในสคริปต์จริงคุณอาจเขียนลง CSV, ดาวน์โหลดไอคอน, หรือส่งต่อไปยังบริการอื่น. นี่คือลูปง่าย ๆ ที่แสดงผลบนคอนโซล.

```python
# Step 4: Display each discovered favicon URL
if not icon_urls:
    print("No icon links found in the document.")
else:
    for url in icon_urls:
        print("Favicon URL:", url)
```

### การจัดการกรณีขอบ

- **Multiple rel values:** การตรวจสอบ `is_icon_link` ของเราจะจับ `rel="shortcut icon"` และ `rel="apple-touch-icon"` อยู่แล้ว.  
- **Relative paths:** หากคุณต้องการ URL แบบเต็มในภายหลัง, ใช้ `urllib.parse.urljoin(base_url, href)`.  
- **Missing href:** การตรวจสอบ `if href:` จะข้ามแท็กที่ผิดรูป, ป้องกันข้อผิดพลาด `NoneType`.  
- **Duplicate entries:** คุณสามารถใช้ `icon_urls = list(dict.fromkeys(icon_urls))` เพื่อลบรายการซ้ำ.

---

## สคริปต์เต็ม – โซลูชันครบวงจร

รวมทุกอย่างเข้าด้วยกัน, นี่คือโปรแกรมที่สมบูรณ์พร้อมรัน. บันทึกเป็น `extract_icons.py` และตั้งค่า `html_path` ให้ชี้ไปที่ไฟล์ใดก็ได้ที่คุณต้องการ.

```python
#!/usr/bin/env python3
"""
How to extract icons from an HTML file using Python.

This script:
- Reads an HTML file (read html file python)
- Parses the HTML document (parse html document)
- Finds <link> tags with rel containing "icon"
- Extracts the href attribute (extract href attribute)
- Prints each favicon URL (extract favicon urls)
"""

from pathlib import Path
from bs4 import BeautifulSoup

def is_icon_link(tag):
    """Detect <link> tags that declare an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

def extract_favicon_urls(html_path: Path):
    """Return a list of favicon URLs found in the given HTML file."""
    html_content = html_path.read_text(encoding="utf-8")
    soup = BeautifulSoup(html_content, "html.parser")
    icon_links = [t for t in soup.find_all(is_icon_link)]

    urls = []
    for tag in icon_links:
        href = tag.get("href")
        if href:
            urls.append(href.strip())
    # Remove duplicates while preserving order
    return list(dict.fromkeys(urls))

if __name__ == "__main__":
    # Adjust the path to point to your HTML file
    html_file = Path("sample.html")
    favicon_urls = extract_favicon_urls(html_file)

    if not favicon_urls:
        print("No icon links found in the document.")
    else:
        for url in favicon_urls:
            print("Favicon URL:", url)
```

**ผลลัพธ์ที่คาดหวัง** (สมมติว่า `sample.html` มีไอคอนสองรายการ):

```
Favicon URL: /images/favicon.ico
Favicon URL: https://example.com/assets/apple-touch-icon.png
```

รันด้วย `python extract_icons.py` แล้วคุณจะเห็น URL ที่พิมพ์บนคอนโซล.

---

## คำถามที่พบบ่อย

**Q: ถ้า HTML ใช้แท็ก `<meta>` สำหรับไอคอนจะทำอย่างไร?**  
A: บางไซต์ฝังไอคอนผ่าน `<meta itemprop="image">`. ขยาย `is_icon_link` ให้ตรวจสอบ `meta` ที่มี `itemprop="image"` และดึงแอตทริบิวต์ `content` ของมัน.

**Q: ฉันสามารถดึงไอคอนโดยอัตโนมัติได้หรือไม่?**  
A: ได้—เพียงส่งแต่ละ URL ไปยัง `requests.get(url, stream=True)` แล้วเขียนเนื้อหาไปยังไฟล์. อย่าลืมจัดการ URL แบบ relative ด้วย `urljoin`.

**Q: วิธีนี้ทำงานกับหน้าเว็บระยะไกลได้หรือไม่?**  
A: แน่นอน. แทนขั้นตอนการอ่านไฟล์ด้วย `requests.get(page_url).text` แล้วส่งสตริง HTML ไปยัง BeautifulSoup. เพียงระวัง robots.txt และอัตราการร้องขอ.

## สรุป

เราได้อธิบาย **วิธีดึงไอคอน** จาก HTML แบบสถิตใด ๆ ด้วย Python, ตั้งแต่การอ่านไฟล์จนถึงการพิมพ์ URL ของ favicon แต่ละรายการ. แนวคิดหลัก—การอ่านไฟล์, การแยกวิเคราะห์เอกสาร, การค้นหาแท็กที่ต้องการ, และการดึงแอตทริบิวต์ `href`—เป็นรูปแบบที่นำกลับมาใช้ใหม่ได้ในงาน web‑scraping หลาย ๆ งาน.

ขั้นตอนต่อไป? ลองขยายสคริปต์เพื่อ:

- แปลง URL แบบ relative ให้เป็น URL เต็มโดยอิง base URL ของหน้า  
- ดาวน์โหลดไอคอนแต่ละรายการและบันทึกไว้ในเครื่อง  
- รองรับรูปแบบไอคอนเพิ่มเติม (`rel="mask-icon"` สำหรับ Safari)  

ลองทดลองได้ตามสบาย, หากเจอปัญหาใด ๆ ฝากคอมเมนต์ด้านล่าง. ขอให้สนุกกับการแยกข้อมูล!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้. แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโครงการของคุณ.

- [วิธี Query HTML ใน Java – คู่มือฉบับสมบูรณ์](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [วิธีแก้ไขโครงสร้างเอกสาร HTML ใน Aspose.HTML สำหรับ Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [บันทึกเอกสาร HTML ไปยังไฟล์ใน Aspose.HTML สำหรับ Java](/html/english/java/saving-html-documents/save-html-to-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
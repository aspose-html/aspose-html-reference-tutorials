---
category: general
date: 2026-10-21
description: เรียนรู้วิธีการแยกวิเคราะห์ HTML ด้วย Python, โหลดเอกสาร HTML, ใช้ตัวเลือก
  CSS และดึงลิงก์จาก HTML อย่างรวดเร็ว.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to parse html
- how to use selector
- extract hyperlinks from html
- load html document python
language: th
lastmod: 2026-10-21
og_description: วิธีแยกวิเคราะห์ HTML ด้วย Python โดยใช้ตัวเลือก CSS โหลดเอกสาร HTML
  เลือกลิงก์ และดึงไฮเปอร์ลิงก์จาก HTML ด้วยโค้ดที่สะอาดและชัดเจน
og_image_alt: Screenshot showing how to parse HTML in Python with CSS selectors
og_title: วิธีแยกวิเคราะห์ HTML ด้วย Python – คู่มือแบบขั้นตอนต่อขั้นตอน
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
title: วิธีแยกวิเคราะห์ HTML ด้วย Python โดยใช้ตัวเลือก CSS
url: /th/python/general/how-to-parse-html-in-python-using-css-selectors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการแยกวิเคราะห์ HTML ใน Python ด้วย CSS selectors

หากคุณต้องการ **how to parse html** ในสคริปต์ Python คู่มือนี้จะแสดงให้คุณเห็นอย่างชัดเจน คุณจะได้เรียนรู้วิธีโหลดเอกสาร HTML, วิธีใช้ไวยากรณ์ selector เพื่อค้นหาองค์ประกอบ, และวิธีดึง hyperlink จาก html โดยไม่ต้องเขียน parser เอง

การแยกวิเคราะห์ HTML เป็นงานทั่วไปสำหรับ web scrapers, data‑analysis pipelines หรือ automated testing เมื่อจบบทเรียนนี้คุณจะมีฟังก์ชันที่สามารถนำกลับมาใช้ใหม่ได้ ซึ่งโหลดเอกสาร HTML, เลือกแท็ก `<a>` ทั้งหมดด้วย CSS selector, และคืนรายการ URL ที่สะอาด

## สิ่งที่คุณต้องการ

- Python 3.8+ (โค้ดทำงานบนเวอร์ชันล่าสุดใดก็ได้)  
- ไลบรารี **lxml** (`pip install lxml`) – ให้การแยกวิเคราะห์ HTML ที่เร็วและสนับสนุน CSS selector  
- ไฟล์ HTML ที่คุณต้องการวิเคราะห์ (เช่น `sample.html`)  

ไม่ต้องใช้เครื่องมือเพิ่มเติม; ทุกอย่างทำงานด้วย standard library และแพ็กเกจ third‑party เพียงหนึ่งเดียว

## ขั้นตอนที่ 1: How to parse HTML – โหลดเอกสาร

ขั้นตอนแรกในกระบวนการทำงานกับ HTML ใด ๆ คือการอ่านไฟล์เข้าสู่หน่วยความจำ การใช้ **lxml.html** จะให้คุณได้อ็อบเจ็กต์ tree ที่รองรับ CSS selectors.

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

**ทำไมเรื่องนี้ถึงสำคัญ:**  
`load_html` แยกส่วนโค้ดอ่านไฟล์ที่ซ้ำซ้อนและรับประกันว่าเอกสารจะถูกแยกวิเคราะห์ด้วย HTML parser ที่ยืดหยุ่น นี่เป็นวิธีที่ปลอดภัยที่สุดในการ **load html document python** โดยไม่ต้องกังวลเกี่ยวกับ markup ที่ผิดรูป

## ขั้นตอนที่ 2: How to use selector – ค้นหาองค์ประกอบลิงก์ทั้งหมด

เมื่อเอกสารถูกโหลดแล้ว คุณสามารถใช้ CSS selector เพื่อค้นหาแท็ก `<a>` ทุกตัว selector `"a"` จะตรงกับองค์ประกอบ anchor ทั้งหมด แต่คุณสามารถปรับให้แคบลงได้ (เช่น `"a.external"` หรือ `"nav a"`).

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

**ทำไมเรื่องนี้ถึงสำคัญ:**  
วิธี **how to use selector** ทำให้คุณสามารถเขียน query ที่ซับซ้อนในรูปแบบสตริงเดียวที่อ่านง่าย ลดการเดินทางผ่าน tree ด้วยตนเอง มันทำงานกับ pattern CSS ใด ๆ ที่ `lxml.cssselect` รองรับ

## ขั้นตอนที่ 3: Extract hyperlinks from HTML และประมวลผล

ตอนนี้คุณมีรายการขององค์ประกอบ `<a>` แล้ว คุณสามารถดึงแอตทริบิวต์ `href` จากแต่ละอัน ตัวช่วยด้านล่างยังทำการทำให้ URL ที่เป็น relative เป็นมาตรฐานโดยอ้างอิง base URL (หากคุณระบุ).

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

**ผลลัพธ์ที่คาดหวัง** (สมมติว่า `sample.html` มีลิงก์สามลิงก์):

```
https://example.com/page1.html
https://example.com/page2.html
https://external.org/resource
```

**ทำไมเรื่องนี้ถึงสำคัญ:**  
`extract_hyperlinks` เป็นหัวใจของ **extract hyperlinks from html** มันจัดการกับแอตทริบิวต์ `href` ที่หายไปอย่างอ่อนโยน, แก้ไขลิงก์ relative, และคืนรายการ Python ธรรมดาที่คุณสามารถส่งต่อไปยังการประมวลผลต่อ (เช่น requests, pandas, หรือฐานข้อมูล)

## ตัวอย่างเต็มแบบ End‑to‑End

การรวมฟังก์ชันทั้งสามเข้าด้วยกันจะให้สคริปต์เดียวที่โหลดไฟล์, เลือก anchor ทั้งหมด, และพิมพ์แต่ละ hyperlink.

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

การรัน `python parse_links.py` จะพิมพ์ hyperlink ทุกอันที่ถูกแก้ไขเต็มที่ลงใน console สคริปต์นี้แสดงให้เห็น **how to parse html**, **how to use selector**, และ **extract hyperlinks from html** ในกระบวนการเดียวที่นำกลับมาใช้ใหม่ได้

## การปรับเปลี่ยนทั่วไปและการจัดการกรณีขอบ

| สถานการณ์ | สิ่งที่ต้องเปลี่ยน | เหตุผล |
|-----------|-------------------|--------|
| **ต้องการเฉพาะ URL แบบ absolute** | Omit the `base_url` argument in `extract_hyperlinks` | Keeps relative URLs untouched |
| **ต้องการข้อความลิงก์ด้วย** | Return a tuple `(href, link.text_content())` from `extract_hyperlinks` | Allows you to store both URL and anchor text |
| **ไฟล์ HTML ขนาดใหญ่** | Use `lxml.etree.iterparse` with a CSS selector filter | Reduces memory usage by streaming |
| **selector ที่แตกต่าง** | Replace `"a"` with `"nav a[href]"` or `"div.content a.external"` | Targets a subset of links, useful for **how to use selector** in complex pages |

**เคล็ดลับ:** ควรตรวจสอบ URL ที่ดึงมาเสมอก่อนทำการร้องขอเครือข่าย การตรวจสอบอย่างรวดเร็วด้วย `urlparse` สามารถกรองสตริงที่ผิดรูปและปกป้อง scraper ของคุณจากการพัง

## สรุป

ตอนนี้คุณรู้แล้วว่า **how to parse html** ใน Python, วิธี **load html document python**, วิธี **how to use selector** เพื่อเลือกองค์ประกอบ, และวิธี **extract hyperlinks from html** อย่างมีประสิทธิภาพ ตัวอย่างเต็มที่แสดงด้านบนพร้อมคัดลอก‑วางเข้าสู่โปรเจคของคุณ และคุณสามารถปรับแต่ละฟังก์ชันให้เหมาะกับกรณีการใช้งานขั้นสูง เช่น pagination, เนื้อหาที่สร้างโดย JavaScript, หรือการครอว์หลายหน้า

ขั้นตอนต่อไปที่คุณอาจสำรวจรวมถึง:

- ใช้ **requests‑html** หรือ **Playwright** เพื่อดึงหน้าที่ต้องการการทำงานของ JavaScript.  
- เก็บ URL ที่ดึงมาไว้ในไฟล์ CSV หรือฐานข้อมูล SQLite เพื่อการวิเคราะห์ในภายหลัง.  
- เพิ่มการจัดการข้อผิดพลาดสำหรับ timeout ของเครือข่ายและรหัสสถานะ HTTP.

ขอให้สนุกกับการแยกวิเคราะห์, และอย่าลังเลที่จะทดลองใช้ selector ต่าง ๆ เพื่อเปิดศักยภาพเต็มของการค้นหา HTML ด้วย CSS ใน Python!

## สิ่งที่คุณควรเรียนต่อไป

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานแบบอื่นในโปรเจคของคุณ.

- [วิธีกำหนดการจัดการทรัพยากร HTML ใน Python และโหลดเอกสาร HTML](/html/english/python/general/how-to-configure-html-resource-handling-in-python-and-load-a/)
- [วิธีแยกวิเคราะห์ HTML ใน Python – คู่มือฉบับสมบูรณ์](/html/english/python/general/how-to-parse-html-in-python-complete-guide/)
- [วิธีโหลด HTML ใน Python – คู่มือแบบขั้นตอนต่อขั้นตอน](/html/english/python/general/how-to-load-html-in-python-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
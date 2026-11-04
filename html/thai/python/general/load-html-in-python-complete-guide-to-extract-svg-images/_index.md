---
category: general
date: 2026-06-10
description: โหลด HTML ใน Python เพื่อดึงภาพ SVG จากหน้าเว็บของคุณ—โค้ดทีละขั้นตอน,
  เคล็ดลับ, และการจัดการกรณีขอบ
draft: false
keywords:
- load html python
- extract svg images
- extract svg from html
- search html svg
- find inline svg
language: th
og_description: โหลด HTML ใน Python และแยกรูปภาพ SVG ด้วยตัวอย่างที่ชัดเจนและสามารถรันได้
  เรียนรู้วิธีค้นหาองค์ประกอบ SVG ใน HTML และจัดการกับกรณีขอบเขต
og_title: โหลด HTML ด้วย Python – ดึงภาพ SVG อย่างมีประสิทธิภาพ
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Load HTML in Python to extract SVG images from your pages—step-by-step
    code, tips, and edge‑case handling.
  headline: Load HTML in Python – Complete Guide to Extract SVG Images
  type: TechArticle
tags:
- python
- html-parsing
- svg
title: โหลด HTML ใน Python – คู่มือครบวงจรสำหรับการดึงภาพ SVG
url: /th/python/general/load-html-in-python-complete-guide-to-extract-svg-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# โหลด HTML ด้วย Python – คู่มือเต็มสำหรับการดึงภาพ SVG

เคยต้อง **โหลด HTML ด้วย Python** เพียงเพื่อดึงกราฟิก SVG ทั้งหมดออกจากหน้าเว็บหรือไม่? คุณไม่ได้เป็นคนเดียว ไม่ว่าคุณจะสร้างเว็บ‑สคราเปอร์, สร้างรายงานสินทรัพย์, หรือแค่อยากรู้ว่าไอคอนของเว็บไซต์ใช้อะไร การ **ดึงภาพ SVG** จะช่วยคุณประหยัดเวลาในการค้นหามากมาย

ในบทแนะนำนี้เราจะพาคุณผ่านโซลูชันแบบครบวงจรที่ **โหลด HTML ด้วย Python**, จากนั้น **ค้นหา HTML SVG** elements, **หา inline SVG**, และแม้กระทั่งดึงไฟล์ SVG ภายนอกที่อ้างอิงโดยแท็ก `<img>` สุดท้ายคุณจะได้สคริปต์ที่นำกลับมาใช้ใหม่ได้, เคล็ดลับสำหรับส่วนที่ซับซ้อน, และภาพรวมของผลลัพธ์ที่ได้อย่างชัดเจน

## สิ่งที่คุณจะได้เรียนรู้

* สคริปต์ Python ที่ทำงานได้เต็มรูปแบบ ซึ่งทำการพาร์สไฟล์ HTML ภายในเครื่อง (หรือหน้าเว็บที่ดึงมา) และแสดงรายการ SVG ทั้งหมดที่พบ  
* ความเข้าใจในความแตกต่างระหว่าง **inline SVG** (`<svg>…</svg>`) กับ **external SVG** (`<img src="… .svg">`)  
* กลยุทธ์การจัดการกับ markup ที่ผิดรูป, ไฟล์ที่หายไป, และปัญหา namespace  
* ไอเดียสำหรับการต่อยอดโค้ด—บันทึก SVG, แปลงเป็น PNG, หรือบันทึกลงฐานข้อมูล

### ความพร้อมเบื้องต้น

* ติดตั้ง Python 3.8+  
* มีความคุ้นเคยพื้นฐานกับไลบรารี `requests` และ `BeautifulSoup` ของ Python (เราจะ import มาใช้ ไม่ต้องลงลึก)  
* มีไฟล์ HTML ภายในเครื่องหรือ URL ที่ต้องการสแกน  

ตอนนี้มาเริ่มกันเลย

## โหลด HTML ด้วย Python – ตั้งค่าตัวพาร์เซอร์

ขั้นตอนแรกคือ **โหลด HTML ด้วย Python** คุณสามารถอ่านไฟล์จากดิสก์หรือดึงหน้าเว็บจากระยะไกลได้ โค้ดด้านล่างเป็นตัวช่วยขนาดเล็กแต่แข็งแรงที่ทำทั้งสองอย่างได้:

```python
import os
import requests
from bs4 import BeautifulSoup

def load_html(source: str) -> BeautifulSoup:
    """
    Load HTML content from a file path or a URL and return a BeautifulSoup object.
    """
    if os.path.isfile(source):
        # Load from local file
        with open(source, "r", encoding="utf-8") as f:
            html = f.read()
    else:
        # Assume it's a URL and fetch it
        response = requests.get(source)
        response.raise_for_status()
        html = response.text

    # Use the html.parser for speed; switch to 'lxml' if you need extra robustness
    soup = BeautifulSoup(html, "html.parser")
    return soup
```

> **ทำไมเรื่องนี้ถึงสำคัญ:** การใช้ `BeautifulSoup` ช่วยให้คุณไม่ต้องจัดการกับความแปลกของการพาร์สสตริงแบบดิบ และฟังก์ชันนี้จัดการไฟล์ในเครื่องและ URL ระยะไกลได้อย่างราบรื่น อีกทั้งยังโยนข้อยกเว้นเมื่อการร้องขอเครือข่ายล้มเหลว—คุณจะรู้ทันทีเมื่อมีอะไรผิดพลาด

## ดึงภาพ SVG – ค้นหา Inline SVG Elements

เมื่อเอกสารถูกโหลดแล้ว ขั้นตอนต่อไปคือ **ค้นหา inline SVG** tag Inline SVG จะฝังอยู่ใน markup ของ HTML โดยตรง ทำให้คุณสามารถดึงมันจาก DOM ได้ทันที

```python
def collect_inline_svg(soup: BeautifulSoup) -> list:
    """
    Return a list of all inline <svg> elements as strings.
    """
    inline_svgs = []
    for svg in soup.find_all("svg"):
        # Preserve the original markup; .decode() gives us a string representation
        inline_svgs.append(str(svg))
    return inline_svgs
```

*เคล็ดลับ:* หากหน้าเว็บใช้ namespace ของ SVG (`<svg xmlns="http://www.w3.org/2000/svg">`) `BeautifulSoup` ยังสามารถหาแท็กได้ เพราะโดยปริยายมันจะละเลย namespace นี่เป็นความสะดวกเมื่อคุณแค่ **ค้นหา HTML SVG** เท่านั้น

## ค้นหา HTML SVG – จัดการกับ `<img>` ที่อ้างอิงภายนอก

หลายเว็บไซต์ไม่ได้ฝัง SVG โดยตรง แต่จะอ้างอิงไฟล์ภายนอกผ่าน `<img src="icon.svg">` เพื่อดึงไฟล์เหล่านี้ เราต้องวนลูปทุกแท็ก `<img>` ตรวจสอบค่า `src` และดูว่ามันจบด้วย `.svg` หรือไม่

```python
def collect_external_svg(soup: BeautifulSoup, base_path: str = "") -> list:
    """
    Return a list of file paths or URLs that point to external SVG images.
    If base_path is provided, it will be joined with relative URLs.
    """
    external_svgs = []
    for img in soup.find_all("img"):
        src = img.get("src")
        if src and src.lower().endswith(".svg"):
            # Resolve relative paths if a base directory or URL is given
            if base_path and not src.startswith(("http://", "https://")):
                src = os.path.join(base_path, src)
            external_svgs.append(src)
    return external_svgs
```

> **กรณีขอบเขตพิเศษ:** บางหน้าใช้ query string (`icon.svg?v=2`) หรือ fragment (`icon.svg#layer`) การตรวจสอบ `endswith(".svg")` ยังทำงานได้เพราะเราตรวจสอบส่วนท้ายของสตริงที่แปลงเป็นตัวพิมพ์เล็กทั้งหมด หากต้องการการตรวจสอบที่เข้มงวดกว่า สามารถใช้ `urllib.parse` เพื่อตัดพารามิเตอร์ออกก่อนได้

## ค้นหา Inline SVG – รายงานผลลัพธ์

ตอนนี้เรามีสองรายการ—หนึ่งสำหรับ markup ของ inline SVG อีกหนึ่งสำหรับอ้างอิงไฟล์ภายนอก—เราสามารถรวมกันและรายงานจำนวนทั้งหมดได้ โค้ดนี้เป็นการต่อยอดจาก snippet ดั้งเดิมของคุณ แต่เพิ่มบริบทเล็กน้อย

```python
def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")
```

## รวมทุกอย่างไว้ด้วยกัน – สคริปต์เต็ม

ด้านล่างเป็นโปรแกรมที่พร้อมรันทั้งหมด บันทึกเป็น `extract_svg.py` แล้วชี้ไปที่ไฟล์ HTML ภายในเครื่องหรือ URL ที่ต้องการ

```python
#!/usr/bin/env python3
import os
import sys
import requests
from bs4 import BeautifulSoup

# -------------------------------------------------
# Helper functions (see definitions above)
# -------------------------------------------------
def load_html(source: str) -> BeautifulSoup:
    if os.path.isfile(source):
        with open(source, "r", encoding="utf-8") as f:
            html = f.read()
    else:
        response = requests.get(source)
        response.raise_for_status()
        html = response.text
    return BeautifulSoup(html, "html.parser")

def collect_inline_svg(soup: BeautifulSoup) -> list:
    return [str(svg) for svg in soup.find_all("svg")]

def collect_external_svg(soup: BeautifulSoup, base_path: str = "") -> list:
    external_svgs = []
    for img in soup.find_all("img"):
        src = img.get("src")
        if src and src.lower().endswith(".svg"):
            if base_path and not src.startswith(("http://", "https://")):
                src = os.path.join(base_path, src)
            external_svgs.append(src)
    return external_svgs

def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")

# -------------------------------------------------
# Main execution
# -------------------------------------------------
if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python extract_svg.py <path-or-url-to-html>")
        sys.exit(1)

    source = sys.argv[1]
    soup = load_html(source)

    # Determine base path for relative <img> sources (only relevant for local files)
    base_dir = os.path.dirname(os.path.abspath(source)) if os.path.isfile(source) else ""

    inline_svgs = collect_inline_svg(soup)
    external_svgs = collect_external_svg(soup, base_dir)

    report_svg_counts(inline_svgs, external_svgs)

    # Optional: write inline SVGs to separate files for inspection
    for idx, svg_markup in enumerate(inline_svgs, start=1):
        out_path = f"inline_svg_{idx}.svg"
        with open(out_path, "w", encoding="utf-8") as out_file:
            out_file.write(svg_markup)
        print(f"Saved inline SVG #{idx} to {out_path}")

    # Optional: download external SVGs (uncomment if needed)
    # for url in external_svgs:
    #     try:
    #         resp = requests.get(url)
    #         resp.raise_for_status()
    #         filename = os.path.basename(url.split("?")[0])
    #         with open(filename, "wb") as f:
    #             f.write(resp.content)
    #         print(f"Downloaded {url} → {filename}")
    #     except Exception as e:
    #         print(f"Failed to download {url}: {e}")
```

### ผลลัพธ์ที่คาดหวัง

เมื่อรันสคริปต์กับไฟล์ตัวอย่าง `sample.html` อาจได้ผลลัพธ์ประมาณนี้:

```
Found 3 inline SVG element(s).
Found 2 external SVG reference(s).
Overall, 5 SVG item(s) detected.
Saved inline SVG #1 to inline_svg_1.svg
Saved inline SVG #2 to inline_svg_2.svg
Saved inline SVG #3 to inline_svg_3.svg
```

หากคุณเปิดคอมเมนต์บล็อกดาวน์โหลด, SVG ภายนอกจะถูกดึงลงมา

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโปรเจกต์ของคุณ

- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Convert SVG to Image in .NET with Aspose.HTML](/html/english/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [How to Convert SVG to XPS with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
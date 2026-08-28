---
category: general
date: 2026-06-16
description: วิธีปรับขนาด SVG ใน Python อย่างรวดเร็ว – โหลดไฟล์ SVG ด้วย Python, แก้ไขไฟล์
  SVG ด้วย Python, และแม้กระทั่งปรับขนาดไฟล์ SVG เป็นชุดด้วยสคริปต์เล็ก ๆ
draft: false
keywords:
- how to resize svg
- batch resize svg files
- load svg file python
- edit svg file python
language: th
og_description: วิธีปรับขนาด SVG ใน Python? เรียนรู้การโหลดไฟล์ SVG ด้วย Python, แก้ไขไฟล์
  SVG ด้วย Python, และปรับขนาดไฟล์ SVG เป็นชุดโดยใช้ตัวอย่างที่ชัดเจนและสามารถรันได้
og_title: วิธีปรับขนาด SVG ใน Python – คู่มือเต็ม
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
title: วิธีปรับขนาด SVG ใน Python – คู่มือขั้นตอนต่อขั้นตอน
url: /th/python/general/how-to-resize-svg-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีปรับขนาด SVG ใน Python – บทเรียนครบถ้วน

เคยสงสัย **วิธีปรับขนาด SVG** โดยไม่ต้องเปิดโปรแกรมแก้ไขกราฟิกหรือไม่? บางทีคุณอาจมีโลโก้ที่ต้องการความกว้าง 200 px สำหรับแบนเนอร์เว็บ, หรือกำลังเตรียมไอคอนหลายสิบตัวสำหรับแอปมือถือ ข่าวดีคือ? คุณทำได้ทั้งหมดใน Python—ไม่ต้อง Photoshop, ไม่ต้อง UI ของ Inkscape, แค่โค้ดไม่กี่บรรทัด

ในบทความนี้เราจะอธิบายขั้นตอนการโหลดไฟล์ SVG ใน Python, แก้ไขขนาด, และแม้กระทั่งสเกลโฟลเดอร์ของ SVG ทั้งหมดพร้อมกัน เมื่อเสร็จคุณจะสามารถ **load SVG file Python**, **edit SVG file Python**, และ **batch resize SVG files** ได้อย่างมั่นใจ

## ข้อกำหนดเบื้องต้น

- ติดตั้ง Python 3.8+ (คำสั่ง `python` ปกติใช้งานได้)
- ไลบรารี `svgwrite` หรือ `lxml` – เราจะใช้ `lxml` เพราะให้การเข้าถึง DOM โดยตรง
- โฟลเดอร์ที่มีไฟล์ SVG ที่ต้องการปรับขนาด (เช่น `assets/icons/`)

คุณไม่จำเป็นต้องใช้เครื่องมือ GUI; ทุกอย่างทำงานจากเทอร์มินัล

---

## ขั้นตอนที่ 1: ติดตั้งไลบรารีที่จำเป็น

ก่อนอื่นให้ติดตั้ง `lxml` จาก PyPI มันเล็ก, เร็ว, และทำให้เราจัดการคุณลักษณะ XML ได้โดยตรง

```bash
pip install lxml
```

> **เคล็ดลับ:** หากคุณทำงานใน virtual environment ให้เปิดใช้งานก่อนรันคำสั่ง เพื่อให้การจัดการ dependencies ของโปรเจคเป็นระเบียบ

## ขั้นตอนที่ 2: โหลดไฟล์ SVG ใน Python

ต่อไปเราจะ **load SVG file Python** – อ่าน XML, ดึงเอา element `<svg>` ราก, และพิมพ์ขนาดปัจจุบันออกมา

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

**ทำไมต้องทำเช่นนี้:** `lxml` ให้ DOM ที่แท้จริง, เราจึงสามารถ query หรือเปลี่ยนแปลง attribute ใดก็ได้—เหมาะอย่างยิ่งสำหรับงาน **edit SVG file Python**

## ขั้นตอนที่ 3: เปลี่ยนความกว้าง (และความสูง) – วิธีปรับขนาด SVG

SVG เป็นเวกเตอร์, คุณสามารถตั้งค่าความกว้าง, ความสูง, หรือทั้งสองได้ หากคุณเปลี่ยนแค่ความกว้าง viewBox จะรักษาอัตราส่วน, แต่เครื่องมือหลายตัวก็เคารพ attribute ความสูงที่ตรงกัน นี่คือฟังก์ชันช่วยที่ปรับขนาดโดยคงอัตราส่วนเดิมไว้

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

ฟังก์ชันด้านบนเป็นหัวใจของ **how to resize SVG** มันอ่านขนาดปัจจุบัน, คำนวณความสูงตามสัดส่วน, และเขียน attribute ใหม่กลับไปยังไฟล์

## ขั้นตอนที่ 4: บันทึก SVG ที่แก้ไขแล้ว

หลังจากแก้ไขแล้ว คุณต้องเขียนการเปลี่ยนแปลงกลับไปยังดิสก์ ซึ่งเป็นขั้นตอนสุดท้ายของวงจร **edit SVG file Python**

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

รันสคริปต์ทั้งหมดแล้วคุณจะได้ไฟล์ `logo_resized.svg` ที่กว้างพอดี 200 px

## ขั้นตอนที่ 5: ปรับขนาด SVG เป็นชุด – สเกลโฟลเดอร์ทั้งหมด

ตอนนี้เราสามารถ **load SVG file Python**, **edit SVG file Python**, และบันทึกได้แล้ว, มาเขียนลูปเพื่อประมวลผลโฟลเดอร์ทั้งหมดกัน นี่คือคำตอบของ **batch resize SVG files**

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

### สิ่งที่สคริปต์ทำ:

1. **รวบรวม** ไฟล์ `.svg` ทุกไฟล์ในโฟลเดอร์ต้นทาง
2. **โหลด** แต่ละไฟล์ด้วยขั้นตอนเดียวกับที่ใช้กับ SVG เดี่ยว
3. **ปรับขนาด** ให้ได้ความกว้างที่ต้องการพร้อมคงอัตราส่วน
4. **เขียน** ผลลัพธ์ไปยังโฟลเดอร์ใหม่, ไม่ทำลายไฟล์ต้นฉบับ

ตอนนี้คุณมี pipeline พร้อมใช้สำหรับ **batch resize SVG files** แล้ว

## ขั้นตอนที่ 6: กรณีขอบและข้อผิดพลาดทั่วไป

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|--------|
| ขาด attribute `width`/`height` | SVG บางไฟล์พึ่งพา `viewBox` เท่านั้น | หากไม่มี attribute ให้ใช้ขนาดจาก viewBox (`viewBox="0 0 w h"`) เป็นค่า fallback |
| หน่วยไม่ใช่ `px` (เช่น `pt`, `%`) | สคริปต์ลบเฉพาะ `px` | ขยายการเรียก `replace` หรือใช้ regex เพื่อจับหน่วยใดก็ได้ |
| มี `<symbol>` หรือ `<use>` ซับซ้อน | การปรับขนาดที่รากอาจไม่ส่งผลต่อสัญลักษณ์ย่อย | ทำการเปลี่ยน attribute เดียวกันกับแต่ละ `<symbol>` หรือใช้ CSS `transform: scale()` |
| ชื่อไฟล์มี Unicode หรืออักขระพิเศษ | `pathlib` รองรับส่วนใหญ่, แต่ Windows อาจเจอปัญหา | ตรวจสอบให้ชื่อไฟล์เป็น UTF‑8 safe, หรือเปลี่ยนชื่อก่อนประมวลผล |

การจัดการข้อเหล่านี้ล่วงหน้าจะช่วยคุณหลีกเลี่ยงไอคอนที่พังหลังจากรันสคริปต์

## ขั้นตอนที่ 7: ตรวจสอบผลลัพธ์

คุณสามารถตรวจสอบอย่างเร็วด้วย snippet HTML เล็ก ๆ นี้:

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

เปิดไฟล์ในเบราว์เซอร์—ทั้งสองภาพควรดูเหมือนกัน, แต่ไฟล์ที่ปรับขนาดจะรายงานความกว้าง **200 px** ใน developer tools

---

## สรุป

คุณได้เรียนรู้ **วิธีปรับขนาด SVG** ด้วย Python อย่างเต็มรูปแบบ ตั้งแต่ไฟล์เดี่ยวจนถึงโฟลเดอร์ทั้งหมด workflow ครอบคลุม **load SVG file Python**, **edit SVG file Python**, และ **batch resize SVG files**—ทั้งหมดด้วยฟังก์ชันไม่กี่ตัว

ลองใช้งานดู: เปลี่ยนความกว้างต่าง ๆ, ทดลองปรับขนาดเฉพาะความสูง, หรือเพิ่ม CLI ด้วย `argparse` ความเป็นไปได้ไม่มีที่สิ้นสุด, และสคริปต์เบา ๆ นี้สามารถฝังใน pipeline ของการ build, งาน CI, หรือยูทิลิตี้บนเดสก์ท็อปได้

มีคำถามเกี่ยวกับการจัดการ gradient, ฟอนต์ฝัง, หรือการรวมสคริปต์นี้กับแอป Flask? แสดงความคิดเห็น, เราจะสำรวจหัวข้อเหล่านั้นร่วมกัน. Happy coding!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโปรเจคของคุณ

- [แปลง SVG เป็นรูปภาพใน .NET ด้วย Aspose.HTML](/html/hindi/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [แปลง SVG เป็น PDF ใน .NET ด้วย Aspose.HTML](/html/hindi/net/canvas-and-image-manipulation/convert-svg-to-pdf/)
- [แสดงเอกสาร SVG เป็น PNG ใน .NET ด้วย Aspose.HTML](/html/hindi/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
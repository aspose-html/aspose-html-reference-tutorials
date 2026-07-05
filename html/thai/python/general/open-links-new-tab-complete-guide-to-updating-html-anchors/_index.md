---
category: general
date: 2026-07-05
description: เปิดลิงก์ในแท็บใหม่ด้วย Python – เรียนรู้วิธีเพิ่ม target="_blank", เปลี่ยนเป้าหมายของลิงก์,
  ใช้ตัวเลือก attribute contains selector, และบันทึก HTML ที่แก้ไขแล้วอย่างง่ายดาย.
draft: false
keywords:
- open links new tab
- add target blank
- change link target
- attribute contains selector
- save modified html
language: th
og_description: เปิดลิงก์ในแท็บใหม่อย่างรวดเร็ว บทเรียนนี้แสดงวิธีเพิ่ม target="_blank",
  เปลี่ยนเป้าหมายของลิงก์, และบันทึก HTML ที่แก้ไขด้วย Python.
og_title: เปิดลิงก์ในแท็บใหม่ – คู่มืออัปเดต HTML ทีละขั้นตอน
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
title: เปิดลิงก์ในแท็บใหม่ – คู่มือเต็มสำหรับการอัปเดตแอนเคอร์ HTML
url: /th/python/general/open-links-new-tab-complete-guide-to-updating-html-anchors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เปิดลิงก์ในแท็บใหม่ – คู่มือเต็มสำหรับการอัปเดต HTML Anchors

เคยต้องการ **เปิดลิงก์ในแท็บใหม่** บนหน้า HTML แบบสแตติกแต่ไม่แน่ใจว่าจะเริ่มอย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว นักพัฒนาหลายคนเจอปัญหานี้เมื่อต้องทำความสะอาดเว็บไซต์เก่าหรือเพิ่มการปรับแต่งการเข้าถึง ในบทเรียนนี้เราจะอธิบายวิธีแก้ปัญหาที่ใช้งานได้จริงที่ **เพิ่ม target blank**, **เปลี่ยน target ของลิงก์**, และ **บันทึก HTML ที่แก้ไข** อย่างปลอดภัย—ทั้งหมดด้วยไม่กี่บรรทัดของ Python.

เราจะอธิบายวิธีใช้ **attribute contains selector** เพื่อให้คุณแก้ไขแองเคอร์ที่คุณสนใจเท่านั้น (เช่น ลิงก์ทั้งหมดที่ชี้ไปที่ *example.com*). เมื่อจบคุณจะมีสคริปต์ที่นำกลับมาใช้ใหม่ได้ซึ่งสามารถใส่ลงในโปรเจกต์ใดก็ได้ ไม่ว่าจะใหญ่หรือเล็ก.

## สิ่งที่คุณจะได้เรียนรู้

- โหลดไฟล์ HTML เข้าไปในอ็อบเจ็กต์เอกสารที่สามารถจัดการได้.  
- เลือกองค์ประกอบ `<a>` ที่แอตทริบิวต์ `href` มีส่วนย่อยที่ระบุ.  
- **เพิ่ม target blank** และตั้งค่าแอตทริบิวต์ `rel="noopener"` เพื่อเพิ่มความปลอดภัย.  
- **บันทึก HTML ที่แก้ไข** กลับไปยังดิสก์โดยไม่สูญเสียรูปแบบ.  

ไม่มีการพึ่งพาไลบรารีภายนอกนอกจากไลบรารีมาตรฐานและ **beautifulsoup4** (ติดตั้งเล็กน้อย). หากคุณใช้พาร์เซอร์อื่นอยู่แล้ว แนวคิดเหล่านี้สามารถนำไปใช้ได้โดยตรง.

---

## ข้อกำหนดเบื้องต้น

- Python 3.8+ ติดตั้งบนเครื่องของคุณ.  
- ความคุ้นเคยพื้นฐานกับ HTML และ Python.  
- `beautifulsoup4` package (`pip install beautifulsoup4`).  

เท่านี้—ไม่ต้องใช้เฟรมเวิร์กหนัก.

---

## ขั้นตอนที่ 1: โหลดเอกสาร HTML

สิ่งแรกที่ต้องทำคืออ่านไฟล์ต้นฉบับและส่งให้ BeautifulSoup. คิดว่าเป็นการเปิดผ้าใบเปล่าที่คุณสามารถวาดแอตทริบิวต์ใหม่ได้.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Path to the original HTML file
html_path = Path("YOUR_DIRECTORY/links.html")

# Read the file content
with html_path.open(encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")
```

> **ทำไมเรื่องนี้สำคัญ:** การใช้ `Path` ทำให้โค้ดไม่ขึ้นกับระบบปฏิบัติการ, และ `html.parser` เป็นตัวในตัว, ดังนั้นคุณไม่ต้องใช้พาร์เซอร์เพิ่มเติมสำหรับงานง่าย ๆ.

---

## ขั้นตอนที่ 2: ใช้ Attribute Contains Selector เพื่อค้นหาลิงก์ที่ต้องการ

เราต้องการแก้ไขแองเคอร์ที่ชี้ไปที่ *example.com* เท่านั้น. ตัวเลือก CSS `a[href*='example.com']` ทำเช่นนั้น—`*=` หมายถึง “มีส่วนย่อย”. วิธี `select` ของ BeautifulSoup เข้าใจไวยากรณ์นี้.

```python
# Find all <a> tags whose href contains 'example.com'
selector = "a[href*='example.com']"
anchor_elements = soup.select(selector)
```

> **เคล็ดลับมือโปร:** หากต้องการจับคู่แบบไม่สนใจตัวพิมพ์, เปลี่ยนเป็นลูปเล็กที่ตรวจสอบ `if 'example.com' in a.get('href', '').lower()`.

ตอนนี้ `anchor_elements` มีลิงก์ทั้งหมดที่เราสนใจ, พร้อมสำหรับการแปลงต่อไป.

---

## ขั้นตอนที่ 3: เปลี่ยน Target ของลิงก์ – เพิ่ม Target Blank และทำให้ลิงก์ปลอดภัย

การเปิดลิงก์ในแท็บใหม่ง่ายเพียงตั้งค่า `target="_blank"`. อย่างไรก็ตาม, เบราว์เซอร์สมัยใหม่แนะนำให้เพิ่ม `rel="noopener"` (หรือ `noreferrer`) เพื่อป้องกันไม่ให้หน้าที่เปิดใหม่เข้าถึงหน้าต้นฉบับผ่าน `window.opener`. การปรับความปลอดภัยเล็ก ๆ นี้สามารถหยุดการโจมตีแบบฟิชชิ่งได้.

```python
for anchor in anchor_elements:
    # Open in a new tab
    anchor['target'] = "_blank"          # add target blank
    # Harden security
    anchor['rel'] = "noopener"           # prevent access to the opener page
```

> **ทำไมเราถึงใช้การกำหนดโดยตรงผ่านดิกชันนารี:** มันจะสร้างแอตทริบิวต์โดยอัตโนมัติหากไม่มี, และเขียนทับหากมีอยู่แล้ว—เหมาะอย่างยิ่งสำหรับการ **เปลี่ยน target ของลิงก์**.

---

## ขั้นตอนที่ 4: บันทึก HTML ที่แก้ไขกลับไปยังดิสก์

ขั้นตอนสุดท้ายคือเขียนมาร์กอัปที่อัปเดตไปยังไฟล์ใหม่. การเก็บไฟล์ต้นฉบับไว้ไม่เปลี่ยนแปลงทำให้คุณสามารถย้อนกลับได้หากเกิดปัญหา.

```python
# Destination path for the updated HTML
output_path = Path("YOUR_DIRECTORY/links-updated.html")

# Write the prettified HTML (preserves indentation)
with output_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())
```

> **`prettify()` ทำอะไร:** มันจัดรูปแบบ HTML ด้วยการเยื้องที่สวยงาม, ทำให้ไฟล์ที่บันทึกอ่านง่ายและเปรียบเทียบได้ง่ายในภายหลัง. หากคุณต้องการรักษาช่องว่างเดิม, แทนที่ `prettify()` ด้วย `str(soup)`.

---

## สคริปต์เต็ม – โซลูชันคลิกเดียว

ด้านล่างเป็นสคริปต์ที่สมบูรณ์พร้อมรัน. บันทึกเป็น `update_links.py` แล้วเรียกใช้ `python update_links.py` จากเทอร์มินัลของคุณ.

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

### ผลลัพธ์ที่คาดหวัง

สมมติว่า `links.html` มีเนื้อหาเดิมดังนี้:

```html
<a href="https://example.com/page1">Page 1</a>
<a href="https://other.com/home">Home</a>
```

หลังจากรันสคริปต์, `links-updated.html` จะมีลักษณะดังนี้:

```html
<a href="https://example.com/page1" target="_blank" rel="noopener">Page 1</a>
<a href="https://other.com/home">Home</a>
```

เฉพาะลิงก์ไปยัง *example.com* เท่านั้นที่ได้รับแอตทริบิวต์ **add target blank**, แสดงให้เห็นว่า **attribute contains selector** ของเราทำงานตามที่ต้องการ.

---

## คำถามทั่วไป & กรณีขอบ

### ถ้าลิงก์มีแอตทริบิวต์ `rel` อยู่แล้ว?

ลูปของเราจะเขียนทับด้วย "noopener". หากต้องการรักษาค่าที่มีอยู่ (เช่น "nofollow"), ให้ต่อข้อความแทน:

```python
existing = a.get('rel', '')
a['rel'] = f"{existing} noopener".strip()
```

### จะจัดการหลายโดเมนอย่างไร?

เพียงขยายรายการ selector:

```python
domains = ["example.com", "sample.org"]
selector = ",".join([f"a[href*='{d}']" for d in domains])
anchors = soup.select(selector)
```

### `prettify()` ทำให้โครงสร้าง HTML ดั้งเดิมเปลี่ยนหรือไม่?

มันทำการเยื้องใหม่แต่ไม่เปลี่ยนลำดับแท็กหรือค่าแอตทริบิวต์. หากคุณต้องรักษาช่องว่างเดิมอย่างแม่นยำ, ให้แทนที่ `prettify()` ด้วย `str(soup)` ตามที่กล่าวไว้ก่อนหน้า.

---

## เคล็ดลับระดับมืออาชีพสำหรับสคริปต์พร้อมใช้งานใน Production

- **สำรองข้อมูลก่อนเขียนทับ:** เพิ่มขั้นตอนคัดลอก (`shutil.copy`) เพื่อเก็บไฟล์ต้นฉบับให้ปลอดภัย.  
- **ใช้ logging แทนการพิมพ์:** ใช้โมดูล `logging` สำหรับโปรเจกต์ที่ขยายได้.  
- **ประมวลผลแบบชุด:** วนลูปผ่านไดเรกทอรีด้วย `Path.rglob("*.html")` เพื่ออัปเดตหลายไฟล์ในครั้งเดียว.  

การปรับแต่งเหล่านี้ทำให้สคริปต์ **open links new tab** ง่าย ๆ กลายเป็นยูทิลิตี้ที่แข็งแรงสำหรับกระบวนการบำรุงรักษาเว็บใด ๆ.

---

## สรุป

ตอนนี้คุณมีวิธีที่มั่นคงและนำกลับมาใช้ใหม่ได้เพื่อ **เปิดลิงก์ในแท็บใหม่** ในคอลเลกชัน HTML สแตติกใด ๆ. ด้วยการใช้ **attribute contains selector**, คุณสามารถ **เปลี่ยน target ของลิงก์** อย่างแม่นยำตรงที่ต้องการ, **เพิ่ม target blank**, และ **บันทึก HTML ที่แก้ไข** โดยไม่สูญเสียรูปแบบ.

ลองใช้บนหน้าเทสต์แล้วขยายไปยังทั้งเว็บไซต์ของคุณ. ต้องการปรับ selector สำหรับ PDF หรือโดเมนอื่น? เพียงปรับสตริง CSS—ส่วนอื่นทั้งหมดคงเดิม.

หากเจอข้อผิดพลาดใด ๆ อย่าลังเลที่จะคอมเมนต์, หรือแชร์วิธีที่คุณขยายสคริปต์สำหรับโปรเจกต์ของคุณเอง. โค้ดให้สนุก, และขอให้แองเคอร์ของคุณเปิดตรงที่คุณต้องการเสมอ!

## สิ่งที่คุณควรเรียนต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้. แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้ทางเลือกในโปรเจกต์ของคุณ.

- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
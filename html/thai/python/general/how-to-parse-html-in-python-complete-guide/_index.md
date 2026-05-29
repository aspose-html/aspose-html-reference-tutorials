---
category: general
date: 2026-05-28
description: วิธีการแยกวิเคราะห์ HTML ด้วย Python อย่างรวดเร็ว—โหลดไฟล์ HTML, ใช้
  CSS selector, และดึงค่าแอตทริบิวต์ href ด้วยตัวอย่าง XPath ที่ใช้ contains.
draft: false
keywords:
- how to parse html
- get href attribute
- load html file
- use css selector
- xpath contains example
language: th
og_description: 'วิธีการแยกวิเคราะห์ HTML ด้วย Python: เรียนรู้การโหลดไฟล์ HTML, ใช้ตัวเลือก
  CSS, และดึงค่าแอตทริบิวต์ href ด้วยตัวอย่าง XPath ที่ใช้ contains'
og_title: วิธีแยกวิเคราะห์ HTML ด้วย Python – ทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  headline: How to Parse HTML in Python – Complete Guide
  type: TechArticle
- description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  name: How to Parse HTML in Python – Complete Guide
  steps:
  - name: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
    text: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
  - name: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
    text: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
  - name: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
    text: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
  - name: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
    text: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
  type: HowTo
tags:
- html parsing
- python
- web scraping
title: วิธีแยกวิเคราะห์ HTML ด้วย Python – คู่มือฉบับสมบูรณ์
url: /th/python/general/how-to-parse-html-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการแยกวิเคราะห์ HTML ด้วย Python – คู่มือฉบับสมบูรณ์

เคยสงสัยไหมว่า **วิธีการแยกวิเคราะห์ HTML** ในสคริปต์ Python โดยไม่ต้องดึงเบราว์เซอร์ที่หนักหน่วง? คุณไม่ได้เป็นคนเดียว ส่วนใหญ่ของเราต้องการเพียง **โหลดไฟล์ HTML**, ดึงหัวข้อข่าวบางส่วน, และอาจดึงลิงก์ดาวน์โหลดหนึ่งสองลิงก์ ในบทแนะนำนี้ฉันจะแสดงให้คุณเห็นโดยใช้ไลบรารีขนาดเล็ก, ตัวเลือก CSS, และตัวอย่าง XPath contains เพื่อ **รับค่าแอตทริบิวต์ href** 

เราจะเดินผ่านกระบวนการทั้งหมด ตั้งแต่การอ่านเอกสาร HTML ในเครื่องไปจนถึงการพิมพ์ข้อมูลที่คุณสนใจ ไม่ฟุ่มเฟือย แค่ตัวอย่างที่ใช้งานได้จริงที่คุณสามารถนำไปใส่ในโปรเจกต์ของคุณได้ทันที

## สิ่งที่คุณจะได้เรียนรู้

- วิธี **โหลดไฟล์ HTML** ด้วยพาร์เซอร์ที่มีน้ำหนักเบา
- วิธี **ใช้ไวยากรณ์ CSS selector** เพื่อดึงองค์ประกอบเช่นหัวข้อบทความ
- วิธีสร้าง **ตัวอย่าง XPath contains** ที่กรองลิงก์
- วิธีรับค่าแอตทริบิวต์ **href** อย่างปลอดภัยจากโหนดที่ตรงกัน
- เคล็ดลับการจัดการกับมาร์กอัปที่ผิดรูปและการขยายสคริปต์

คุณต้องการเพียง Python 3.8+ และแพคเกจ `lxml` กับ `cssselect`—ทั้งสองสามารถติดตั้งได้ด้วยคำสั่ง `pip` เพียงคำสั่งเดียว

---

## ขั้นตอนที่ 1: โหลดไฟล์ HTML

ก่อนอื่นคุณต้องมีเนื้อหา HTML อยู่ในหน่วยความจำ โมดูล `lxml.html` มีตัวช่วย `fromstring` ที่สะดวก, แต่เมื่อคุณมีไฟล์บนดิสก์ฟังก์ชัน `parse` จะสะอาดกว่า

```python
# Step 1: Load the HTML file
from lxml import html

# Replace the path with the location of your HTML document
html_path = "YOUR_DIRECTORY/news.html"
doc = html.parse(html_path)

# The root element gives us access to CSS and XPath methods
root = doc.getroot()
```

> **ทำไมเรื่องนี้ถึงสำคัญ:** การโหลดไฟล์เพียงครั้งเดียวช่วยลดการใช้หน่วยความจำและให้คุณได้อ็อบเจ็กต์ `root` เดียวที่รองรับทั้ง CSS selector และ XPath query หากไฟล์หายหรือไม่สามารถอ่านได้ `html.parse` จะโยงข้อผิดพลาด `OSError` ที่ชัดเจนซึ่งคุณสามารถดักจับได้ในภายหลัง

### เคล็ดลับพิเศษ
หากคุณทำงานกับสตริงแทนไฟล์ ให้เปลี่ยน `html.parse` เป็น `html.fromstring(your_html_string)`

---

## ขั้นตอนที่ 2: ใช้ CSS Selector เพื่อดึงหัวข้อข่าว

CSS selector มีความกระชับและคุ้นเคยกับผู้ที่เคยเขียนสไตล์ชีต มาเลือกทุก `<h2>` ภายใน `<article>` — เหมาะอย่างยิ่งสำหรับหัวข้อข่าว

```python
# Step 2: Find all article headlines using a CSS selector
headline_nodes = root.cssselect("article h2")

# Print each headline's text content
for node in headline_nodes:
    print(node.text_content().strip())
```

**ผลลัพธ์ที่คาดหวัง** (สมมติว่า HTML ตัวอย่างมีสองบทความ):

```
Breaking News: Python Takes Over the World
Local Developer Solves HTML Parsing Puzzle
```

> **ทำไมต้องใช้ CSS?** มันอ่านง่าย, เร็ว, และทำงานได้ทันทีกับ `lxml` วิธี `cssselect` แปลง selector ให้เป็น XPath expression ภายใน, ทำให้คุณได้ประโยชน์จากทั้งสองโลก

---

## ขั้นตอนที่ 3: ตัวอย่าง XPath Contains – ค้นหาลิงก์ “download”

บางครั้งคุณต้องการการควบคุมที่ละเอียดกว่าที่ CSS ให้ได้ ฟังก์ชัน `contains()` ของ XPath จะมีประโยชน์เมื่อคุณต้องการจับส่วนย่อยของแอตทริบิวต์ เช่นลิงก์ทั้งหมดที่ชี้ไปยังการดาวน์โหลด

```python
# Step 3: Find all links that contain the word "download" using XPath
download_link_nodes = root.xpath("//a[contains(@href, 'download')]")

# Extract and print the href attribute from each matching node
for node in download_link_nodes:
    href = node.get("href")
    print(href)
```

**ตัวอย่างผลลัพธ์**:

```
/files/report_download.pdf
https://example.com/downloads/setup.exe
```

> **ทำไมต้องใช้ XPath contains?** มันให้คุณกรองโดยตรงบนค่าแอตทริบิวต์โดยไม่ต้องใช้ลูป Python เพิ่มเติม นี่คือตัวอย่าง **xpath contains example** คลาสสิกที่คุณมักเห็นในบทแนะนำ, แต่ที่นี่มันถูกจับคู่กับกรณีการใช้งานจริง

---

## ขั้นตอนที่ 4: รวมทุกอย่างเป็นฟังก์ชันที่นำกลับมาใช้ได้

การกำหนดพาธและพิมพ์แบบฮาร์ดโค้ดอาจพอสำหรับการทดสอบเร็ว, แต่โค้ดสำหรับการผลิตต้องการฟังก์ชัน ด้านล่างเป็นตัวช่วยขนาดกะทัดรัดที่คืนค่าหัวข้อข่าวและลิงก์ดาวน์โหลด

```python
def parse_news_html(file_path):
    """
    Parse a news HTML file and return headlines plus download URLs.

    Parameters
    ----------
    file_path : str
        Path to the local HTML document.

    Returns
    -------
    dict
        {
            "headlines": list of strings,
            "download_links": list of href strings
        }
    """
    doc = html.parse(file_path)
    root = doc.getroot()

    # Headlines via CSS selector
    headlines = [
        node.text_content().strip()
        for node in root.cssselect("article h2")
    ]

    # Download links via XPath contains
    download_links = [
        node.get("href")
        for node in root.xpath("//a[contains(@href, 'download')]")
    ]

    return {"headlines": headlines, "download_links": download_links}
```

คุณสามารถเรียกฟังก์ชันและพิมพ์ผลลัพธ์อย่างสวยงามได้แล้ว:

```python
if __name__ == "__main__":
    results = parse_news_html("YOUR_DIRECTORY/news.html")
    print("Headlines:")
    for h in results["headlines"]:
        print(f"- {h}")

    print("\nDownload Links:")
    for link in results["download_links"]:
        print(f"- {link}")
```

การรันสคริปต์จะให้ผลลัพธ์เดียวกับก่อนหน้า, แต่ตอนนี้มันถูกจัดเก็บอย่างเป็นระเบียบเพื่อการนำกลับมาใช้ใหม่

---

## ขั้นตอนที่ 5: การจัดการกรณีขอบและข้อผิดพลาดทั่วไป

1. **แอตทริบิวต์ `href` หาย** – XPath ยังจะคืนโหนด `<a>` แม้ว่า `href` จะไม่มีอยู่ ให้ตรวจสอบค่า `None`:
   
   ```python
   href = node.get("href")
   if href:
       download_links.append(href)
   ```

2. **URL แบบ relative กับ absolute** – หากลิงก์ของคุณเป็นแบบ relative, คุณอาจต้องแก้ไขให้เป็น URL สมบูรณ์โดยอ้างอิงกับ base URL:
   
   ```python
   from urllib.parse import urljoin
   base_url = "https://example.com"
   absolute = urljoin(base_url, href)
   ```

3. **HTML ที่ผิดรูป** – `lxml` ยอมรับบางส่วน, แต่มาร์กอัปที่เสียหายอย่างมากอาจทำให้ `html.parse` โยน `XMLSyntaxError` ให้ห่อการเรียก parse ด้วยบล็อก `try/except` เพื่อบันทึกและข้ามไฟล์ที่มีปัญหา

4. **ประสิทธิภาพกับไฟล์ขนาดใหญ่** – สำหรับหน้าเว็บหลายเมกะไบต์, พิจารณาใช้การสตรีมด้วย `iterparse` แทนการโหลด DOM ทั้งหมดเข้าสู่หน่วยความจำ

---

## ภาพรวมโดยภาพ (optional)

![แผนภาพการแยกวิเคราะห์ HTML แสดงขั้นตอนโหลดไฟล์ → CSS selector → XPath contains → รับแอตทริบิวต์ href](how-to-parse-html-flow.png "แผนภาพการแยกวิเคราะห์ HTML")

*ข้อความ alt รวมคีย์เวิร์ดหลักเพื่อให้สอดคล้องกับ SEO.*

---

## สรุป

เราได้ครอบคลุม **วิธีการแยกวิเคราะห์ HTML** ด้วย Python ตั้งแต่ต้นจนจบ: การโหลดไฟล์ HTML, การใช้ CSS selector เพื่อดึงหัวข้อบทความ, การสร้างตัวอย่าง XPath contains เพื่อค้นหาลิงก์ดาวน์โหลด, และสุดท้าย **การรับค่าแอตทริบิวต์ href** อย่างปลอดภัย ฟังก์ชัน `parse_news_html` ที่นำกลับมาใช้ได้แสดงแนวทางที่สะอาดและดูแลได้ซึ่งคุณสามารถปรับใช้กับงานสครัปใด ๆ

พร้อมสำหรับความท้าทายต่อไป? ลองขยายสคริปต์เพื่อ:
- แยกตารางด้วยการสอบถาม XPath `//table//tr`
- ดึงแอตทริบิวต์ `src` ของรูปภาพโดยใช้ **xpath contains example** อีกอัน
- เปลี่ยนเป็นการดึงข้อมูลแบบอะซิงโครนัสด้วย `aiohttp` สำหรับหน้าเว็บสด

ขอให้สนุกกับการแยกวิเคราะห์, และจำไว้ว่า—เมื่อคุณเชี่ยวชาญพื้นฐานเหล่านี้ การสครัป HTML ส่วนอื่นจะง่ายเหมือนเค้ก หากเจออุปสรรคใด ๆ ฝากคอมเมนต์ด้านล่าง—เรามาช่วยกันแก้ปัญหา!

## บทแนะนำที่เกี่ยวข้อง

- [โหลดเอกสาร HTML จากไฟล์ใน Aspose.HTML สำหรับ Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [วิธีแก้ไขโครงสร้างเอกสาร HTML ใน Aspose.HTML สำหรับ Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [วิธีเพิ่ม CSS – Inline CSS ไปยังเอกสาร HTML ใน Aspose.HTML สำหรับ Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
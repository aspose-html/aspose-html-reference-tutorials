---
category: general
date: 2026-06-10
description: โหลด HTML จาก URL เพื่อดึงไอคอนเว็บไซต์อย่างรวดเร็ว เรียนรู้วิธีการแยก
  favicons, ดึง URL ของ favicon เว็บไซต์, และจัดการกรณีพิเศษใน Python.
draft: false
keywords:
- load html from url
- get website icons
- how to extract favicons
- extract favicon urls
- fetch website favicon urls
language: th
og_description: โหลด HTML จาก URL เพื่อดึงไอคอน favicon และดึง URL ของ favicon ของเว็บไซต์
  คู่มือ Python ทีละขั้นตอนสำหรับนักพัฒนา.
og_title: โหลด HTML จาก URL และรับไอคอนเว็บไซต์ – คู่มือเต็ม
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Load HTML from URL to get website icons quickly. Learn how to extract
    favicons, fetch website favicon URLs, and handle edge cases in Python.
  headline: Load HTML from URL and Get Website Icons – Complete Guide
  type: TechArticle
tags:
- web scraping
- favicon extraction
- python
- html parsing
title: โหลด HTML จาก URL และรับไอคอนเว็บไซต์ – คู่มือฉบับสมบูรณ์
url: /th/python/general/load-html-from-url-and-get-website-icons-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# โหลด HTML จาก URL และดึงไอคอนเว็บไซต์ – คู่มือฉบับสมบูรณ์

เคยต้อง **โหลด HTML จาก URL** เพียงเพื่อดึงโลโก้ขนาดเล็กของเว็บไซต์หรือไม่? คุณไม่ได้เป็นคนเดียว ไม่ว่าคุณจะกำลังสร้างตัวจัดการบุ๊คมาร์ค, แดชบอร์ด SEO, หรือแค่โครงการส่วนตัว การดึงไอคอนเว็บไซต์เป็นส่วนเล็ก ๆ แต่สำคัญของปริศนา

ในบทเรียนนี้เราจะสาธิต **วิธีดึง favicons** ด้วย Python ธรรมดา—ไม่ต้องใช้ Selenium หนัก ๆ หรือเวทมนตร์ของเบราว์เซอร์ เมื่อจบคุณจะสามารถ **ดึง URL ของ favicon เว็บไซต์**, จัดการกับเส้นทางแบบ relative, และแม้กระทั่งดึงหลายไอคอนหากเว็บไซต์มีให้พร้อมแล้ว พร้อมหรือยัง? ไปดูกันเลย

## ทำไมต้องโหลด HTML จาก URL ในขั้นแรก?

การโหลด HTML ดิบของหน้าเว็บทำให้คุณเข้าถึงแท็ก `<link>` ที่เบราว์เซอร์ใช้เพื่อหา favicons ได้โดยตรง แท็กเหล่านี้มักจะมีลักษณะเช่น:

```html
<link rel="icon" href="/favicon.ico">
<link rel="apple-touch-icon" href="https://example.com/apple-touch-icon.png">
```

หากคุณสามารถดึง markup นี้ออกมาได้ คุณก็สามารถอ่านแอตทริบิวต์ `href` แล้วดาวน์โหลดรูปภาพด้วยตนเองได้เร็วกว่า การจับภาพหน้าจอ และทำงานได้กับทุกไซต์ที่ปฏิบัติตามมาตรฐาน

## ขั้นตอนที่ 1 – โหลดเอกสาร HTML จาก URL

สิ่งแรกที่เราต้องการคือวิธีดึงซอร์สของหน้าเว็บ ตัวเลือกที่นิยมที่สุดใน Python คือไลบรารี **requests** เพราะใช้งานง่าย เชื่อถือได้ และจัดการการเปลี่ยนเส้นทางโดยอัตโนมัติ

```python
import requests

def fetch_html(url: str) -> str:
    """
    Retrieve the raw HTML from the given URL.
    Raises an exception if the request fails.
    """
    response = requests.get(url, timeout=10)
    response.raise_for_status()          # Fail fast on HTTP errors
    return response.text
```

> **เคล็ดลับ:** หากคุณทำงานอยู่หลังพร็อกซีขององค์กร ให้ส่ง `proxies=` ไปยัง `requests.get` นอกจากนี้ การตั้งค่า timeout สั้น ๆ จะป้องกันสคริปต์ค้างเมื่อติดต่อกับไซต์ที่ไม่ตอบสนอง

ตอนนี้เราสามารถเรียก `fetch_html("https://example.com")` เพื่อรับสตริงที่มี markup ของหน้าได้ นี่คือแกนหลักของ **โหลด HTML จาก URL**—ส่วนที่เหลือของกระบวนการทำงานกับสตริงนี้ต่อไป

## ขั้นตอนที่ 2 – ดึงไอคอนเว็บไซต์

เมื่อเรามี HTML แล้ว ขั้นตอนต่อไปคือการค้นหาแท็ก `<link>` ทุกตัวที่แอตทริบิวต์ `rel` มีคำว่า “icon” โมดูลในตัว `html.parser` ทำได้ แต่ **BeautifulSoup** ทำให้โค้ดอ่านง่ายกว่าเยอะ

```python
from bs4 import BeautifulSoup
from urllib.parse import urljoin

def extract_icon_links(html: str, base_url: str) -> list[str]:
    """
    Parse the HTML and return a list of absolute URLs pointing to icons.
    Handles relative hrefs by joining them with the page’s base URL.
    """
    soup = BeautifulSoup(html, "html.parser")
    icons = []

    # Look for any <link> tag where rel contains "icon"
    for link in soup.find_all("link", rel=lambda r: r and "icon" in r.lower()):
        href = link.get("href")
        if href:
            # Convert relative URLs to absolute ones
            absolute_url = urljoin(base_url, href)
            icons.append(absolute_url)

    return icons
```

สังเกตว่าเราใช้ `urljoin` เพื่อแปลง `"/favicon.ico"` ให้เป็น `"https://example.com/favicon.ico"` — นี่เป็นกรณีขอบที่พบบ่อยเมื่อ **ดึงไอคอนเว็บไซต์** บางไซต์อาจให้ไอคอนหลายแบบสำหรับอุปกรณ์ต่าง ๆ ทำให้คุณอาจได้หลาย URL ไม่เป็นไร เราก็แค่เก็บไว้ทั้งหมด

## ขั้นตอนที่ 3 – ดึง URL ของ Favicon และแสดงผล

การประกอบส่วนต่าง ๆ เข้าด้วยกันทำได้ง่าย เราจะดึง HTML, รันตัวดึง, แล้วพิมพ์รายการที่ได้ สคริปต์สุดท้ายเป็นดังนี้:

```python
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin

def fetch_html(url: str) -> str:
    response = requests.get(url, timeout=10)
    response.raise_for_status()
    return response.text

def extract_icon_links(html: str, base_url: str) -> list[str]:
    soup = BeautifulSoup(html, "html.parser")
    icons = []
    for link in soup.find_all("link", rel=lambda r: r and "icon" in r.lower()):
        href = link.get("href")
        if href:
            icons.append(urljoin(base_url, href))
    return icons

def main():
    target = "https://example.com"
    html = fetch_html(target)
    icon_urls = extract_icon_links(html, target)
    print("Found icon URLs:", icon_urls)

if __name__ == "__main__":
    main()
```

### ผลลัพธ์ที่คาดหวัง

รันสคริปต์กับไซต์ที่ให้ favicon มาตรฐานอาจได้ผลลัพธ์เช่น:

```
Found icon URLs: ['https://example.com/favicon.ico']
```

หากไซต์นั้นมีไอคอนหลายแบบ (Apple touch icon, shortcut icon ฯลฯ) คุณจะเห็นรายการที่ยาวขึ้น:

```
Found icon URLs: [
    'https://example.com/favicon.ico',
    'https://example.com/apple-touch-icon.png',
    'https://example.com/favicon-32x32.png'
]
```

นี่คือเวิร์กโฟลว์ **ดึง URL ของ favicon** ทั้งหมด—กระชับ, มีการพึ่งพาน้อย, และพร้อมนำไปใช้ในโปรเจกต์ใดก็ได้

## การจัดการกับปัญหาที่พบบ่อย

| ปัญหา | ทำไมถึงเกิด | วิธีแก้เร็ว |
|-------|------------|------------|
| **Relative `href` without a `<base>` tag** | `urljoin` สมมติว่า URL ของหน้าเป็นฐาน ซึ่งทำงานได้ในหลายกรณี | หากมีแท็ก `<base href="...">` ให้อ่านค่าแรกและส่งเป็น `base_url` |
| **Missing `rel="icon"`** | บางไซต์ใช้ `rel="shortcut icon"` หรือค่าที่กำหนดเอง | ขยาย lambda: `rel=lambda r: r and ("icon" in r.lower() or "shortcut" in r.lower())` |
| **Redirects to a different domain** | Favicon อาจอยู่บน CDN | `urljoin` จะแก้ไขโดเมนใหม่อย่างถูกต้องเพราะใช้ URL ของการตอบกลับสุดท้าย (`response.url`) |
| **Broken links (404)** | HTML ชี้ไปยังไฟล์ที่ไม่มีอยู่แล้ว | หลังดึง URL แล้วให้ตรวจสอบแต่ละอันด้วย HEAD request ก่อนใช้งาน |
| **Multiple `<link>` tags with the same icon** | รายการซ้ำทำให้ลิสต์บวม | ใช้ `set(icon_urls)` เพื่อลบรายการซ้ำก่อนคืนค่า |

## ไปต่อ – ดึง URL ของ Favicon เว็บไซต์เป็นกลุ่ม

หากต้องการ **ดึง URL ของ favicon เว็บไซต์** สำหรับรายการโดเมนหลาย ๆ ตัว ให้ห่อโลจิก `main` ไว้ในลูป:

```python
domains = ["https://example.com", "https://python.org", "https://github.com"]
for site in domains:
    try:
        icons = extract_icon_links(fetch_html(site), site)
        print(site, "->", icons)
    except Exception as e:
        print(site, "error:", e)
```

รูปแบบนี้ขยายได้ง่าย และคุณสามารถเพิ่มการแคช (เช่น ด้วย `functools.lru_cache`) เพื่อหลีกเลี่ยงการร้องขอซ้ำ ๆ ไปยังไซต์เดียวกัน

## ภาพรวมเชิงภาพ

![แผนภาพการโหลด HTML จาก URL](load-html-url.png)

*Alt text: แผนภาพการโหลด HTML จาก URL แสดงขั้นตอน fetch → parse → extract.*

ภาพด้านบนสรุปกระบวนการสามขั้นตอน: **โหลด HTML จาก URL**, **ดึงไอคอนเว็บไซต์**, และ **ดึง URL ของ favicon** เป็นประโยชน์เมื่อคุณต้องอธิบายขั้นตอนให้เพื่อนร่วมทีมฟัง

## สรุป

เราได้เดินผ่านโซลูชันพร้อมใช้งานในระดับ production สำหรับวิธี **โหลด HTML จาก URL** และ **ดึงไอคอนเว็บไซต์** โดยใช้เพียงไลบรารี requests และ BeautifulSoup ของ Python การดึงแอตทริบิวต์ `href` ของแท็ก `<link rel="icon">` ทำให้คุณ **ดึง URL ของ favicon**, จัดการเส้นทางแบบ relative, และแม้กระทั่งรับหลายรูปแบบของไอคอนได้—ทั้งหมดในไม่กี่สิบบรรทัดของโค้ด

ต่อไปคุณจะทำอะไร? ลองดาวน์โหลดไอคอนไปยังโฟลเดอร์ในเครื่อง, สร้าง CSV ของการแมปโดเมน‑to‑favicon, หรือเชื่อมต่อโลจิกนี้เข้ากับ Flask API ที่ให้บริการ favicon ตามคำขอ ความเป็นไปได้สำหรับ **ดึง URL ของ favicon เว็บไซต์** ไม่มีที่สิ้นสุด และเทคนิคหลักยังคงเหมือนเดิม

มีคำถามเกี่ยวกับกรณีขอบหรืออยากแชร์เคล็ดลับเจ๋ง ๆ? แสดงความคิดเห็นด้านล่าง—ขอให้สนุกกับการล่าไอคอน!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอน‑ต่อ‑ขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโปรเจกต์ของคุณเอง

- [โหลดเอกสาร HTML จากไฟล์ใน Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [โหลดเอกสาร HTML จากสตรีมด้วย Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-stream/)
- [จัดการเหตุการณ์การโหลดเอกสารใน Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/handle-document-load-events/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
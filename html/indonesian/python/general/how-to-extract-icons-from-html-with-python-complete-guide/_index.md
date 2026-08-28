---
category: general
date: 2026-07-02
description: Cara mengekstrak ikon dari file HTML menggunakan Python. Pelajari cara
  membaca file HTML dengan Python, mengurai dokumen HTML, dan mengekstrak atribut
  href untuk mendapatkan URL favicon.
draft: false
keywords:
- how to extract icons
- read html file python
- parse html document
- extract href attribute
- extract favicon urls
language: id
og_description: Cara mengekstrak ikon dari halaman HTML menggunakan Python. Tutorial
  ini menunjukkan cara membaca file HTML dengan Python, mengurai dokumen, dan mengambil
  URL favicon.
og_title: Cara Mengekstrak Ikon dari HTML – Panduan Python
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
title: Cara Mengambil Ikon dari HTML dengan Python – Panduan Lengkap
url: /id/python/general/how-to-extract-icons-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengekstrak Ikon dari HTML dengan Python – Panduan Lengkap

Pernah bertanya‑tanya **cara mengekstrak ikon** dari sebuah halaman web tanpa membuka browser? Mungkin Anda sedang membangun katalog situs, alat audit SEO, atau hanya penasaran dengan favicon kecil yang muncul di tab. Kabar baiknya, Anda dapat melakukannya dalam beberapa baris Python—tanpa Selenium, tanpa Chrome headless, hanya file HTML teks biasa.

Dalam tutorial ini kita akan membahas cara membaca file HTML dengan Python, mengurai dokumen HTML, dan akhirnya **mengekstrak atribut href** dari tag `<link rel="icon">` untuk mendapatkan URL favicon tersebut. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat dipakai ulang untuk HTML statis apa pun, serta cara menangani kasus khusus seperti jalur relatif atau deklarasi ikon ganda.

## Apa yang Akan Anda Pelajari

- Memuat file HTML lokal dengan Python (read html file python)  
- Menggunakan parser ringan untuk **parse html document** secara aman  
- Menemukan elemen `<link>` yang mendeklarasikan sebuah ikon  
- **Extract href attribute** dan mengubahnya menjadi URL absolut  
- Mengumpulkan dan mencetak semua **favicon URLs** yang ditemukan  

Tidak memerlukan layanan eksternal—hanya pustaka standar dan paket **BeautifulSoup** yang populer.

---

![Screenshot showing Python script extracting icons – how to extract icons](https://example.com/images/extract-icons-python.png "cara mengekstrak ikon")

*Image alt text: "cara mengekstrak ikon menggunakan skrip Python"*

## Prasyarat

- Python 3.8+ terpasang  
- Pustaka `beautifulsoup4` (`pip install beautifulsoup4`)  
- File HTML lokal yang ingin Anda pindai (misalnya `sample.html`)  

Jika semua sudah siap, mari mulai.

## Langkah 1: Baca File HTML dengan Python – Muat Dokumen

Hal pertama yang harus dilakukan: membuka file dan memberi isinya ke parser. Menggunakan `with open(..., "r", encoding="utf‑8")` menjamin file tertutup secara otomatis, dan enkoding UTF‑8 menangani kebanyakan halaman modern.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Step 1: Load the HTML document from disk
html_path = Path("sample.html")          # adjust the path as needed
html_content = html_path.read_text(encoding="utf-8")
```

**Mengapa ini penting:** Membuka file dengan enkoding yang tepat mencegah karakter misterius `�` yang dapat merusak parser nanti. Menggunakan `Path` dari pustaka standar juga membuat kode dapat dijalankan lintas‑platform.

## Langkah 2: Parse Dokumen HTML – Temukan Semua Link Ikon

Sekarang kita serahkan HTML mentah ke **BeautifulSoup**, yang membangun pohon yang dapat dinavigasi. Kita akan mencari setiap tag `<link>` yang atribut `rel`‑nya mengandung kata `icon`. Perhatikan bahwa `rel` dapat berupa daftar dipisahkan spasi (`rel="shortcut icon"`), jadi kita memerlukan pemeriksaan yang fleksibel.

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

**Mengapa langkah ini krusial:** `soup.find_all("link", rel="icon")` yang naïf akan melewatkan variasi seperti `rel="shortcut icon"` atau `rel="apple-touch-icon"`. Helper `is_icon_link` kami mencakup kasus‑kasus tersebut, menjadikan ekstraksi lebih andal.

## Langkah 3: Extract href Attribute – Ambil URL‑nya

Setelah tag‑tag yang relevan terkumpul, kita tarik atribut `href` dari masing‑masing. Beberapa halaman mungkin tidak menyertakan `href` (jarang, tapi mungkin), jadi kita melindungi dari `None`. Selain itu, favicon sering ditentukan dengan URL relatif, sehingga kita akan menyelesaikannya terhadap URL dasar halaman jika Anda mengetahuinya. Untuk file lokal kita biarkan jalurnya apa adanya.

```python
# Step 3: Grab the href attribute from each icon link
icon_urls = []
for tag in icon_links:
    href = tag.get("href")
    if href:
        icon_urls.append(href.strip())
```

**Mengapa kami menghapus spasi:** Penulis HTML kadang‑kadang menambahkan spasi di sekitar URL, yang dapat merusak permintaan selanjutnya. Memangkas memastikan kita mendapatkan string bersih.

## Langkah 4: Extract Favicon URLs – Tampilkan Hasilnya

Akhirnya, kita mencetak (atau mengembalikan) daftar URL yang ditemukan. Dalam skrip dunia nyata Anda mungkin menuliskannya ke CSV, mengunduh ikon, atau mengirimnya ke layanan lain. Berikut contoh loop sederhana yang menampilkan hasil di konsol.

```python
# Step 4: Display each discovered favicon URL
if not icon_urls:
    print("No icon links found in the document.")
else:
    for url in icon_urls:
        print("Favicon URL:", url)
```

### Menangani Kasus Khusus

- **Beberapa nilai rel:** Pemeriksaan `is_icon_link` kami sudah menangkap `rel="shortcut icon"` dan `rel="apple-touch-icon"`.  
- **Jalur relatif:** Jika Anda kemudian membutuhkan URL absolut, gunakan `urllib.parse.urljoin(base_url, href)`.  
- **Href yang hilang:** Guard `if href:` melewati tag yang tidak valid, menghindari error `NoneType`.  
- **Entri duplikat:** Anda dapat `icon_urls = list(dict.fromkeys(icon_urls))` untuk menghilangkan duplikat.

---

## Skrip Lengkap – Solusi Satu‑Langkah

Menggabungkan semuanya, berikut program lengkap yang siap dijalankan. Simpan sebagai `extract_icons.py` dan arahkan `html_path` ke file mana pun yang Anda inginkan.

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

**Output yang diharapkan** (asumsi `sample.html` berisi dua ikon):

```
Favicon URL: /images/favicon.ico
Favicon URL: https://example.com/assets/apple-touch-icon.png
```

Jalankan dengan `python extract_icons.py` dan Anda akan melihat URL‑URL tercetak di konsol.

---

## Pertanyaan yang Sering Diajukan

**T: Bagaimana jika HTML menggunakan tag `<meta>` untuk ikon?**  
J: Beberapa situs menyematkan ikon lewat `<meta itemprop="image">`. Perluas `is_icon_link` untuk juga memeriksa `meta` dengan `itemprop="image"` dan ambil atribut `content`‑nya.

**T: Bisakah saya mengunduh ikon secara otomatis?**  
J: Ya—cukup beri setiap URL ke `requests.get(url, stream=True)` dan tulis kontennya ke file. Ingat untuk menangani URL relatif dengan `urljoin`.

**T: Apakah ini bekerja pada halaman remote?**  
J: Tentu. Ganti langkah membaca file dengan `requests.get(page_url).text` dan berikan string HTML ke BeautifulSoup. Hanya perhatikan robots.txt dan batasan kecepatan permintaan.

---

## Penutup

Kami telah membahas **cara mengekstrak ikon** dari HTML statis apa pun menggunakan Python, mulai dari membaca file hingga mencetak setiap URL favicon. Ide‑ide inti—membaca file, mengurai dokumen, menemukan tag yang tepat, dan mengekstrak atribut `href`—adalah pola yang dapat dipakai ulang dalam banyak tugas web‑scraping.

Langkah selanjutnya? Coba kembangkan skrip untuk:

- Menyelesaikan URL relatif terhadap URL dasar halaman  
- Mengunduh setiap ikon dan menyimpannya secara lokal  
- Mendukung format ikon tambahan (`rel="mask-icon"` untuk Safari)  

Silakan bereksperimen, dan jika menemukan kendala, tinggalkan komentar di bawah. Selamat mengurai!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang memperluas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Save HTML Document to File in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-to-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
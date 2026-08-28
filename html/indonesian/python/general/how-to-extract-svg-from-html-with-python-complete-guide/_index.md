---
category: general
date: 2026-05-31
description: Pelajari cara mengekstrak SVG dari HTML menggunakan Python. Tutorial
  langkah demi langkah ini menunjukkan cara membaca dokumen HTML, menyimpan file SVG,
  dan menyimpan SVG inline secara efisien.
draft: false
keywords:
- how to extract svg
- read html document
- save svg files
- save inline svg
- extract svg from html
language: id
og_description: Cara mengekstrak SVG dari HTML menggunakan Python. Ikuti tutorial
  ini untuk membaca dokumen HTML, menyimpan file SVG, dan menangani SVG inline dengan
  mudah.
og_title: Cara mengekstrak SVG dari HTML dengan Python – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  headline: How to extract SVG from HTML with Python – Complete Guide
  type: TechArticle
- description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  name: How to extract SVG from HTML with Python – Complete Guide
  steps:
  - name: Reads an HTML file.
    text: Reads an HTML file.
  - name: Collects inline <svg> markup.
    text: Collects inline <svg> markup.
  - name: Finds external SVG references (<img> and <object> tags).
    text: Finds external SVG references (<img> and <object> tags).
  - name: Saves each SVG to a separate .svg file.
    text: Saves each SVG to a separate .svg file.
  type: HowTo
tags:
- Python
- SVG
- HTML parsing
- Aspose
title: Cara mengekstrak SVG dari HTML dengan Python – Panduan Lengkap
url: /id/python/general/how-to-extract-svg-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengekstrak SVG dari HTML dengan Python – Panduan Lengkap

Pernah bertanya-tanya **bagaimana cara mengekstrak SVG** dari halaman HTML yang berantakan tanpa membuat rambut Anda rontok? Anda tidak sendirian. Baik Anda sedang membangun web‑scraper, pipeline desain, atau hanya perlu mengekspor ikon secara batch, mengetahui **bagaimana cara mengekstrak SVG** adalah trik berguna yang menghemat waktu dan mengurangi sakit kepala.

Di tutorial ini kami akan menunjukkan secara tepat **bagaimana cara mengekstrak SVG** menggunakan pustaka Aspose.HTML untuk Python. Kami akan membaca dokumen HTML, mengambil markup `<svg>` inline **dan** referensi SVG eksternal, lalu **menyimpan file SVG** ke disk—semua dalam skrip yang rapi dan dapat digunakan kembali. Pada akhir tutorial Anda akan memiliki solusi siap‑jalankan yang dapat Anda sesuaikan dengan proyek Anda.

> **Pro tip:** Jika Anda hanya ingin sekilas cepat halaman, `BeautifulSoup` juga dapat digunakan, tetapi Aspose.HTML memberi Anda DOM lengkap, membuat ekstraksi SVG inline dan yang terlink menjadi sangat mudah.

## Apa yang Anda Butuhkan

* Python 3.8+ (kode menggunakan f‑strings, jadi 3.6+ adalah minimum mutlak)
* `pip install aspose-html` – pustaka komersial yang mendukung parsing HTML kami
* Sebuah folder dengan file `input.html` yang berisi SVG yang ingin Anda ambil
* Izin menulis ke direktori output (kami akan menyebutnya `YOUR_DIRECTORY`)

Itu saja—tanpa binary tambahan, tanpa browser headless. Sederhana, kan?

## Langkah 1: Baca dokumen HTML dengan Aspose.HTML

Hal pertama yang harus Anda lakukan adalah **membaca dokumen HTML** sehingga Anda dapat menelusuri pohon DOM-nya. Aspose.HTML memberikan objek `HTMLDocument` yang berperilaku seperti `document` pada browser.

```python
from aspose.html import HTMLDocument

# Load the HTML file – replace YOUR_DIRECTORY with the actual path
doc = HTMLDocument("YOUR_DIRECTORY/input.html")
```

*Mengapa ini penting:* Dengan memuat HTML ke dalam DOM yang tepat, Anda menghindari jebakan parsing berbasis regex, dan Anda mendapatkan metode seperti `get_elements_by_tag_name` dan `query_selector_all` secara gratis.

## Langkah 2: Kumpulkan semua elemen <svg> inline

SVG inline adalah blok `<svg>…</svg>` yang berada tepat di dalam HTML. Untuk **menyimpan SVG inline** kita hanya membutuhkan outer HTML‑nya.

```python
svg_contents = []  # We'll collect both markup and file paths here

# Find every <svg> element in the document
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)   # Store the raw markup
```

Perhatikan bahwa kami menambahkan markup mentah langsung ke dalam `svg_contents`. Nanti kami akan memutuskan apakah setiap entri adalah markup atau jalur file.

## Langkah 3: Temukan referensi SVG eksternal (tag img dan object)

Banyak halaman menautkan file SVG eksternal melalui `<img src="icon.svg">` atau `<object data="logo.svg">`. Untuk **mengekstrak SVG dari HTML** kita juga perlu menangkap URL‑URL tersebut.

```python
# CSS selector: img or object whose src/data ends with .svg (case‑insensitive)
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    # For <img> we read the src attribute, for <object> the data attribute
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:                                   # Guard against missing attribute
        svg_contents.append(src)
```

*Peringatan kasus khusus:* Jika URL SVG bersifat relatif, Anda perlu menggabungkannya dengan jalur dasar file HTML. Untuk singkatnya, kami mengasumsikan HTML berada di samping file SVG.

## Langkah 4: Tulis setiap SVG ke file terpisah

Sekarang kami memiliki daftar campuran string markup dan jalur file, kami akan mengiterasi dan **menyimpan file SVG**. Skrip secara otomatis membedakan antara markup inline dan referensi ke file yang sudah ada.

```python
import os
import shutil

for index, content in enumerate(svg_contents):
    output_path = f"YOUR_DIRECTORY/svg_{index}.svg"

    # Trim leading whitespace and check if it looks like markup
    if content.lstrip().startswith("<svg"):
        # Inline SVG – write the markup directly
        with open(output_path, "w", encoding="utf-8") as file:
            file.write(content)
        print(f"Saved inline SVG to {output_path}")
    else:
        # External reference – copy the source file's contents
        src_path = os.path.abspath(content)  # Resolve relative paths
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, output_path)
            print(f"Copied external SVG from {src_path} to {output_path}")
        else:
            print(f"⚠️  Warning: referenced SVG not found: {src_path}")
```

**Apa yang akan Anda lihat:** Setelah skrip selesai, `YOUR_DIRECTORY` akan berisi file bernama `svg_0.svg`, `svg_1.svg`, … masing‑masing berisi markup inline asli atau salinan SVG eksternal.

### Output yang Diharapkan

```
Saved inline SVG to YOUR_DIRECTORY/svg_0.svg
Saved inline SVG to YOUR_DIRECTORY/svg_1.svg
Copied external SVG from /path/to/logo.svg to YOUR_DIRECTORY/svg_2.svg
...
```

Jika file yang direferensikan tidak ada, skrip akan mencetak peringatan tetapi tetap melanjutkan—sehingga satu tautan yang rusak tidak akan menghentikan seluruh proses ekstraksi.

## Menangani Kendala Umum

| Problem | Why it Happens | Quick Fix |
|---------|----------------|-----------|
| **URL Relatif tidak berfungsi** | Atribut `src` mungkin berupa `"../assets/icon.svg"` | Gunakan `os.path.join(os.path.dirname(html_path), src)` untuk menyelesaikannya. |
| **Nama file duplikat** | Dua SVG dengan nama yang sama akan ditimpa | Sertakan hash dari konten dalam nama file (`hashlib.md5(content.encode()).hexdigest()[:8]`). |
| **SVG inline besar menyebabkan lonjakan memori** | Menyimpan semua markup dalam list sebelum menulis | Alirkan setiap elemen langsung ke file alih‑alih menampungnya. |
| **Gambar non‑SVG lolos** | Beberapa tag `<img>` berakhir dengan `.svg?version=1` | Hapus query string sebelum memeriksa ekstensi (`src.split('?')[0]`). |

## Skrip Lengkap yang Bisa Anda Salin‑Tempel

Berikut adalah program lengkap yang siap dijalankan. Simpan sebagai `extract_svg.py`, sesuaikan `YOUR_DIRECTORY`, dan jalankan `python extract_svg.py`.

```python
"""
extract_svg.py – How to extract SVG from HTML using Aspose.HTML for Python

This script:
1. Reads an HTML file.
2. Collects inline <svg> markup.
3. Finds external SVG references (<img> and <object> tags).
4. Saves each SVG to a separate .svg file.

Author: Your Name
Date: 2026-05-31
"""

import os
import shutil
from aspose.html import HTMLDocument

# ----------------------------------------------------------------------
# Configuration – change these paths to suit your environment
# ----------------------------------------------------------------------
HTML_PATH = "YOUR_DIRECTORY/input.html"          # Path to source HTML
OUTPUT_DIR = "YOUR_DIRECTORY"                    # Where SVGs will be written

# Ensure output directory exists
os.makedirs(OUTPUT_DIR, exist_ok=True)

# ----------------------------------------------------------------------
# Step 1: Load the HTML document (read html document)
# ----------------------------------------------------------------------
doc = HTMLDocument(HTML_PATH)

# ----------------------------------------------------------------------
# Step 2: Collect inline <svg> elements (save inline svg)
# ----------------------------------------------------------------------
svg_contents = []
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)

# ----------------------------------------------------------------------
# Step 3: Collect external SVG references (extract svg from html)
# ----------------------------------------------------------------------
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:
        # Resolve relative paths relative to the HTML file location
        src_path = os.path.join(os.path.dirname(HTML_PATH), src)
        svg_contents.append(src_path)

# ----------------------------------------------------------------------
# Step 4: Save each gathered SVG (save svg files)
# ----------------------------------------------------------------------
for idx, content in enumerate(svg_contents):
    out_path = os.path.join(OUTPUT_DIR, f"svg_{idx}.svg")

    # Detect inline markup vs file path
    if isinstance(content, str) and content.lstrip().startswith("<svg"):
        # Inline SVG – write directly
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(content)
        print(f"[✓] Inline SVG saved → {out_path}")
    else:
        # External file – copy its contents
        src_path = os.path.abspath(content)
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, out_path)
            print(f"[✓] External SVG copied → {out_path}")
        else:
            print(f"[⚠] Missing SVG file: {src_path}")

print("\n✅ Extraction complete. Check the", OUTPUT_DIR, "folder for your SVGs.")
```

## Ringkasan – Cara mengekstrak SVG secara singkat

* **Baca dokumen HTML** dengan `HTMLDocument`.
* **Kumpulkan `<svg>` inline** melalui `get_elements_by_tag_name`.
* **Temukan SVG eksternal** menggunakan selector CSS yang berakhir dengan `.svg`.
* **Simpan setiap bagian**—tulis markup langsung ke file atau salin file yang direferensikan.
* **Tangani kasus khusus** seperti jalur relatif, duplikat, dan file yang hilang.

Itulah seluruh jawaban untuk **bagaimana cara mengekstrak SVG** dari halaman HTML, dibungkus dalam satu skrip yang mudah dimodifikasi.

## Apa Selanjutnya?

Sekarang Anda dapat **mengekstrak SVG** dengan andal, pertimbangkan ide‑ide lanjutan berikut:

* **Pemrosesan batch:** Loop melalui direktori file HTML untuk membangun perpustakaan ikon.
* **Optimasi:** Jalankan setiap SVG yang disimpan melalui SVGO (optimiser Node.js) untuk memperkecil ukuran file.
* **Konversi:** Gunakan `cairosvg` atau `svglib` untuk mengubah SVG menjadi PNG bagi browser lama.
* **Ekstraksi metadata:** Parse tag `<title>` atau `<desc>` di dalam setiap SVG untuk label yang dapat dicari.

Setiap topik tersebut menyentuh kata kunci sekunder kami—**read HTML document**, **save svg files**, **save inline svg**, **extract svg from html**—sehingga Anda akan menemukan banyak materi untuk dijelajahi.

*Selamat mencoba! Jika Anda menemui kendala, tinggalkan komentar di bawah atau hubungi saya di GitHub. Dunia SVG sangat luas, tetapi dengan alat yang tepat, mengekstraknya menjadi sangat mudah.*

## Apa yang Harus Anda Pelajari Selanjutnya?

- [Simpan Dokumen SVG di Aspose.HTML untuk Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Cara Mengonversi SVG ke XPS dengan Aspose.HTML untuk Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)
- [Render dokumen SVG ke format PNG di .NET dengan Aspose.HTML](/html/french/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
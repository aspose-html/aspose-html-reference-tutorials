---
category: general
date: 2026-09-23
description: Ubah teks elemen dalam file HTML menggunakan Python. Pelajari cara memuat
  file HTML, mengedit tag judul, dan memperbarui judul HTML secara efisien.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change element text
- how to change title
- edit title tag
- load html file
- update html title
language: id
lastmod: 2026-09-23
og_description: Ubah teks elemen dalam dokumen HTML menggunakan Python. Tutorial ini
  menunjukkan cara memuat file HTML, mengedit tag judul, dan memperbarui judul HTML
  hanya dengan beberapa baris kode.
og_image_alt: Screenshot showing change element text in HTML using Python code
og_title: Ubah teks elemen dalam HTML dengan Python – panduan singkat
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Change element text in an HTML file using Python. Learn how to load
    HTML file, edit title tag, and update HTML title efficiently.
  headline: Change element text in HTML with Python – step‑by‑step guide
  type: TechArticle
- description: Change element text in an HTML file using Python. Learn how to load
    HTML file, edit title tag, and update HTML title efficiently.
  name: Change element text in HTML with Python – step‑by‑step guide
  steps:
  - name: 'Edge case: Multiple `<title>` tags'
    text: 'HTML standards allow only one `<title>` element, but malformed files sometimes
      contain more. If you need to handle that situation, iterate over all matches:'
  - name: Editing other elements (e.g., `<h1>`)
    text: 'If you need to **change element text** for a heading instead of the title,
      adjust the XPath:'
  - name: Preserving existing whitespace
    text: 'When the original HTML uses indentation inside tags, `pretty_print` may
      reformat it. To keep the original formatting, omit `pretty_print`:'
  - name: Working with Unicode characters
    text: '`lxml` handles Unicode automatically. Ensure the source file is saved with
      UTF‑8 encoding; otherwise, specify the correct encoding when opening the file.'
  type: HowTo
tags:
- Python
- HTML manipulation
- Web scraping
title: Ubah teks elemen di HTML dengan Python – panduan langkah demi langkah
url: /id/python/general/change-element-text-in-html-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ubah teks elemen dalam HTML dengan Python – panduan langkah demi langkah

Jika Anda perlu **mengubah teks elemen** dalam dokumen HTML, panduan ini menunjukkan secara tepat cara melakukannya dengan Python. Baik Anda memperbaiki tag `<title>` yang usang atau memperbarui elemen lain, Anda akan belajar **memuat file HTML**, mengubah teks, dan **memperbarui judul HTML** (atau elemen apa pun) dengan aman.

Mengubah judul halaman web adalah tugas umum saat membersihkan data yang di‑scrape, menghasilkan halaman situs statis, atau mengotomatisasi pembaruan SEO. Dalam tutorial ini Anda akan:

* Memuat file HTML dari disk.
* Menemukan elemen `<title>` dan **mengedit tag judul**.
* Menyimpan dokumen yang telah dimodifikasi, secara efektif **memperbarui judul HTML**.

Semua kode yang diperlukan disertakan, dan setiap langkah menjelaskan **mengapa** operasi tersebut penting, bukan hanya **apa** yang harus diketik.

## Prerequisites

Sebelum memulai, pastikan Anda memiliki:

* Python 3.9 atau lebih baru terpasang.
* Pustaka `lxml` (`pip install lxml`).  
  `lxml` menyediakan parsing HTML yang cepat dan sesuai standar serta manipulasi elemen.
* Direktori yang berisi file HTML yang ingin Anda edit (ganti `YOUR_DIRECTORY` dengan jalur yang sebenarnya).

## Langkah 1: Memuat file HTML

Langkah pertama adalah **memuat file HTML** ke dalam pohon DOM (Document Object Model) yang dapat diproses oleh Python. Menggunakan `lxml.html` memberi Anda dukungan XPath dan penanganan elemen yang andal.

```python
from pathlib import Path
from lxml import html

# Path to the source HTML document
source_path = Path("YOUR_DIRECTORY/page.html")

# Parse the file into an HTML tree
doc = html.parse(str(source_path))
```

**Mengapa ini penting:**  
Parsing menghasilkan representasi terstruktur dari halaman, memungkinkan Anda menanyakan elemen secara langsung. Tanpa memuat file, Anda tidak dapat dengan aman **mengubah teks elemen** karena Anda akan bekerja dengan string mentah, yang rawan kesalahan.

## Langkah 2: Menemukan elemen `<title>` dan **mengubah teks elemen**

Setelah dokumen dimuat, Anda dapat **mengedit tag judul**. Ekspresi XPath `".//title"` menemukan elemen `<title>` pertama dalam hierarki dokumen.

```python
# Find the <title> element (the first occurrence)
title_elem = doc.find(".//title")

# Guard against missing <title>
if title_elem is None:
    raise ValueError("The document does not contain a <title> element.")

# Change the text inside the <title> tag
title_elem.text = "New Title"
```

**Mengapa ini penting:**  
Menetapkan nilai langsung ke `title_elem.text` **mengubah teks elemen** tanpa mengubah markup di sekitarnya. Pendekatan ini mempertahankan spasi, komentar, dan tag lain, memastikan output tetap HTML yang valid.

### Kasus tepi: Beberapa tag `<title>`

Standar HTML memperbolehkan hanya satu elemen `<title>`, tetapi file yang tidak terstruktur kadang berisi lebih dari satu. Jika Anda perlu menangani situasi tersebut, iterasikan semua kecocokan:

```python
for t in doc.findall(".//title"):
    t.text = "New Title"
```

## Langkah 3: Menyimpan dokumen yang dimodifikasi – **memperbarui judul HTML**

Setelah modifikasi, tulis kembali pohon ke disk. Menggunakan `pretty_print=True` membuat file tetap mudah dibaca.

```python
# Destination path for the updated file
output_path = Path("YOUR_DIRECTORY/updated.html")

# Write the updated HTML back to a file
doc.write(str(output_path), encoding="utf-8", pretty_print=True)
print(f"HTML saved to {output_path}")
```

**Mengapa ini penting:**  
Menyimpan menghasilkan file baru yang mencerminkan operasi **mengubah teks elemen**. Jika Anda perlu menimpa file asli, cukup gunakan jalur yang sama untuk `output_path`.

## Skrip lengkap dalam satu blok

Menggabungkan semuanya, berikut adalah skrip mandiri yang **memuat file HTML**, **mengubah teks elemen**, dan **memperbarui judul HTML**:

```python
"""Change element text in an HTML document – update the <title> tag."""

from pathlib import Path
from lxml import html

def change_title(source: str, new_title: str, destination: str) -> None:
    """Load an HTML file, edit its title, and save the result."""
    # Load the HTML document
    doc = html.parse(source)

    # Locate the <title> element
    title_elem = doc.find(".//title")
    if title_elem is None:
        raise ValueError("No <title> element found in the document.")

    # Change element text
    title_elem.text = new_title

    # Save the updated document
    doc.write(destination, encoding="utf-8", pretty_print=True)

if __name__ == "__main__":
    src = "YOUR_DIRECTORY/page.html"
    dst = "YOUR_DIRECTORY/updated.html"
    change_title(src, "New Title", dst)
    print(f"Updated title saved to {dst}")
```

Menjalankan skrip ini menghasilkan file `updated.html` yang `<title>`‑nya kini berisi **New Title**.

## Variasi umum teknik ini

### Mengedit elemen lain (mis., `<h1>`)

Jika Anda perlu **mengubah teks elemen** untuk heading alih‑alih judul, sesuaikan XPath:

```python
heading = doc.find(".//h1")
if heading is not None:
    heading.text = "Updated Heading"
```

### Mempertahankan spasi yang ada

Ketika HTML asli menggunakan indentasi di dalam tag, `pretty_print` dapat merombak formatnya. Untuk menjaga format asli, hapus `pretty_print`:

```python
doc.write(destination, encoding="utf-8")
```

### Bekerja dengan karakter Unicode

`lxml` menangani Unicode secara otomatis. Pastikan file sumber disimpan dengan encoding UTF‑8; jika tidak, tentukan encoding yang tepat saat membuka file.

## Pro tip dan jebakan

* **Pro tip:** Gunakan `doc.xpath("//title/text()")` jika Anda hanya membutuhkan konten teks tanpa memodifikasi elemen.
* **Waspadai:** File HTML yang berisi `<title>` di dalam `<svg>` atau namespace non‑HTML lainnya. Dalam kasus tersebut, perbaiki XPath untuk menargetkan bagian `<head>`: `doc.find(".//head/title")`.
* **Tip performa:** Untuk pemrosesan batch ribuan file, gunakan kembali instance parser yang sama untuk mengurangi overhead.

## Kesimpulan

Anda kini tahu cara **mengubah teks elemen** dalam dokumen HTML menggunakan Python, khususnya cara **memuat file HTML**, **mengedit tag judul**, dan **memperbarui judul HTML**. Contoh lengkap menunjukkan pendekatan berbasis pustaka yang andal dan berfungsi untuk HTML yang terstruktur baik maupun yang sedikit tidak terstruktur.

Dari sini Anda dapat:

* Menerapkan pola yang sama pada tag lain (`<h2>`, `<meta>`, dll.).
* Menggabungkan skrip ini dengan pipeline web‑scraping untuk membersihkan koleksi halaman yang besar.
* Menjelajahi API `lxml` yang lebih kaya untuk manipulasi atribut, selector CSS, dan serialisasi HTML.

Selamat coding, dan jangan ragu bereksperimen dengan elemen berbeda untuk menguasai manipulasi HTML di Python!

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Parse HTML Java – Load, Query & Count Elements](/html/english/java/creating-managing-html-documents/how-to-parse-html-java-load-query-count-elements/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
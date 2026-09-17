---
category: general
date: 2026-09-16
description: Mengurai file HTML di Python, memuat dokumen HTML dari file, dan membuat
  dokumen HTML dari string dengan kode sederhana yang siap dijalankan.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- parse html file in python
- create html document from string
- load html document from file
- read local html file python
language: id
lastmod: 2026-09-16
og_description: Mengurai file HTML di Python untuk membaca file HTML lokal dan membuat
  dokumen HTML dari string dengan cepat dan dapat diandalkan.
og_image_alt: Screenshot of Python code parsing an HTML file and creating a document
  from a string
og_title: Mengurai file HTML di Python – buat dokumen dari string
schemas:
- author: Aspose
  dateModified: '2026-09-16'
  description: Parse HTML file in Python, load HTML document from file, and create
    HTML document from string with simple, ready‑to‑run code.
  headline: Parse HTML file in Python and create document from string
  type: TechArticle
- description: Parse HTML file in Python, load HTML document from file, and create
    HTML document from string with simple, ready‑to‑run code.
  name: Parse HTML file in Python and create document from string
  steps:
  - name: '**Detect source type** – The constructor checks whether the supplied `source`
      exists on disk. If it does, we **load html document from file**; otherwise we
      treat it as a raw string, satisfying the **create html document from string**
      requirement.'
    text: '**Detect source type** – The constructor checks whether the supplied `source`
      exists on disk. If it does, we **load html document from file**; otherwise we
      treat it as a raw string, satisfying the **create html document from string**
      requirement.'
  - name: '**Read the file** – We use `Path.read_text(encoding="utf-8")` which is
      the recommended way to **read local html file python** safely.'
    text: '**Read the file** – We use `Path.read_text(encoding="utf-8")` which is
      the recommended way to **read local html file python** safely.'
  - name: '**Parse with BeautifulSoup** – The `lxml` parser is fast and tolerant of
      malformed markup.'
    text: '**Parse with BeautifulSoup** – The `lxml` parser is fast and tolerant of
      malformed markup.'
  type: HowTo
tags:
- python html parsing
- html document creation
- file handling python
title: Mengurai file HTML dengan Python dan membuat dokumen dari string
url: /id/python/general/parse-html-file-in-python-and-create-document-from-string/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengurai file HTML di Python dan membuat dokumen dari string

Jika Anda perlu **parse HTML file in Python**, panduan ini menunjukkan secara tepat cara membaca file HTML lokal, memuat dokumen HTML dari file, dan juga **create HTML document from string**. Baik Anda melakukan scraping data, menguji templat, atau menghasilkan konten dinamis, langkah‑langkah di bawah ini memberi Anda solusi lengkap yang dapat dijalankan.

Dalam tutorial ini Anda akan belajar cara:

* Membaca file HTML lokal menggunakan pustaka standar Python.
* Memuat dokumen HTML dari jalur file.
* Membuat dokumen HTML langsung dari string HTML.
* Menangani kasus tepi umum seperti file yang hilang dan masalah enkoding.

Satu‑satunya prasyarat adalah Python 3.8+ dan pustaka `beautifulsoup4`, yang akan kami instal pada langkah pertama.

## Prasyarat

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| Python 3.8 atau lebih baru | Menjamin kompatibilitas dengan type hints dan sintaks modern. |
| `beautifulsoup4` dan paket `lxml` | Menyediakan parser yang kuat yang dapat menangani HTML yang rusak dan memberikan objek yang mirip `HTMLDocument` yang nyaman. |
| File HTML contoh (`index.html`) di folder proyek Anda | Berfungsi sebagai input untuk contoh **load html document from file**. |

Install dependensi dengan pip:

```bash
pip install beautifulsoup4 lxml
```

## Mengurai file HTML di Python

Inti dari tutorial ini adalah operasi **parse html file in python**. Kami akan membungkus BeautifulSoup dalam kelas pembantu kecil bernama `HTMLDocument` sehingga API cocok dengan contoh yang Anda lihat sebelumnya.

```python
from pathlib import Path
from bs4 import BeautifulSoup
from typing import Union

class HTMLDocument:
    """
    Simple wrapper that mimics a “document” object.
    Accepts either a file path or a raw HTML string.
    """
    def __init__(self, source: Union[str, Path]):
        if Path(source).exists():
            # Load html document from file
            self._load_from_file(Path(source))
        else:
            # Assume source is a raw HTML string
            self._load_from_string(source)

    def _load_from_file(self, file_path: Path):
        try:
            # read local html file python – explicit UTF‑8 handling
            html = file_path.read_text(encoding="utf-8")
        except FileNotFoundError:
            raise FileNotFoundError(f"File not found: {file_path}")
        self.soup = BeautifulSoup(html, "lxml")

    def _load_from_string(self, html_string: str):
        self.soup = BeautifulSoup(html_string, "lxml")

    def title(self) -> str:
        """Return the content of the <title> tag, or an empty string."""
        if self.soup.title:
            return self.soup.title.string.strip()
        return ""

    def pretty(self) -> str:
        """Return a nicely formatted HTML representation."""
        return self.soup.prettify()
```

### Cara kerjanya

1. **Detect source type** – Konstruktor memeriksa apakah `source` yang diberikan ada di disk. Jika ada, kami **load html document from file**; jika tidak, kami memperlakukan sebagai string mentah, memenuhi persyaratan **create html document from string**.
2. **Read the file** – Kami menggunakan `Path.read_text(encoding="utf-8")` yang merupakan cara yang direkomendasikan untuk **read local html file python** dengan aman.
3. **Parse with BeautifulSoup** – Parser `lxml` cepat dan toleran terhadap markup yang rusak.

## Memuat dokumen HTML dari file

Sekarang kami memiliki kelas `HTMLDocument`, memuat file menjadi sangat sederhana:

```python
# Step 1: Load an HTML document from a local file
doc = HTMLDocument("YOUR_DIRECTORY/index.html")

# Verify that the file was parsed correctly
print("Document title:", doc.title())
```

**Output yang diharapkan** (asumsi `index.html` berisi `<title>My Page</title>`):

```
Document title: My Page
```

Jika file tidak ada, kelas akan mengeluarkan `FileNotFoundError` yang jelas, yang dapat Anda tangkap dalam kode produksi.

## Membuat dokumen HTML dari string

Membuat dokumen langsung dari string berguna untuk pengujian atau menghasilkan HTML secara dinamis:

```python
# Step 2: Create an HTML document directly from an HTML string
html_content = "<html><head><title>Hello</title></head><body><h1>Hello</h1></body></html>"
doc_from_string = HTMLDocument(html_content)

print("String‑based title:", doc_from_string.title())
```

**Output yang diharapkan**:

```
String-based title: Hello
```

Karena kelas `HTMLDocument` yang sama menangani kedua skenario, Anda mendapatkan API yang konsisten untuk **parse html file in python**, baik sumbernya berupa file maupun string.

## Membaca file HTML lokal Python – menangani kasus tepi

Saat berurusan dengan file dunia nyata, Anda sering menemui:

* **Missing files** – sudah ditangani oleh `FileNotFoundError`.
* **Different encodings** – Anda dapat membiarkan BeautifulSoup menebak enkoding, tetapi UTF‑8 eksplisit adalah yang paling aman.
* **Large files** – membaca seluruh file ke memori mungkin mahal; Anda dapat streaming dengan `BeautifulSoup(open(...), "lxml")` bila diperlukan.

Berikut adalah pembungkus defensif yang menambahkan perlindungan ini:

```python
def safe_load_html(path: Union[str, Path]) -> HTMLDocument:
    """
    Load an HTML file safely, handling missing files and encoding issues.
    Returns an HTMLDocument instance or raises a descriptive exception.
    """
    try:
        return HTMLDocument(path)
    except FileNotFoundError as e:
        raise RuntimeError(f"Unable to read local HTML file Python: {e}")
    except UnicodeDecodeError:
        raise RuntimeError("File encoding is not UTF-8; consider specifying the correct encoding.")
```

Anda kini dapat memanggil `safe_load_html("index.html")` dan mendapatkan objek `HTMLDocument` yang sama dengan keyakinan bahwa kesalahan dilaporkan secara jelas.

## Tips profesional dan jebakan umum

* **Avoid “just” using `open(...).read()`** – `Path.read_text` menangani ekspansi jalur dan enkoding dalam satu baris.
* **Don’t forget to close file handles** – `Path.read_text` melakukannya secara otomatis; jika Anda menggunakan `open()`, bungkuslah dalam blok `with`.
* **Prefer `lxml` over the default parser** – lebih cepat dan lebih toleran terhadap markup yang rusak, yang penting saat Anda **parse html file in python** dari web.
* **When creating from a string, ensure it’s a complete HTML document** – tag `<html>` atau `<body>` yang hilang dapat menyebabkan hasil `None` yang tidak terduga saat Anda menanyakan elemen.

## Skrip lengkap yang dapat Anda salin‑tempel

Berikut adalah skrip mandiri yang mendemonstrasikan setiap langkah yang dibahas. Simpan sebagai `html_demo.py` dan jalankan `python html_demo.py`.



## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Save HTML Document to File in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-to-file/)
- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Create HTML Document with Aspose.HTML – Step‑by‑Step Guide](/html/english/net/html-document-manipulation/create-html-document-with-aspose-html-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
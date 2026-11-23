---
category: general
date: 2026-05-31
description: Pelajari cara mengunduh ikon menggunakan Python. Kami juga akan membahas
  cara mengekstrak favicon, membaca dokumen HTML dengan Python, dan menulis file biner
  dengan Python dalam satu tutorial.
draft: false
keywords:
- how to download icons
- how to extract favicon
- write binary file python
- read html document python
- load html python
language: id
og_description: Cara mengunduh ikon menggunakan Python dijelaskan langkah demi langkah.
  Pelajari cara mengekstrak favicon, membaca dokumen HTML dengan Python, dan menulis
  file biner dengan Python.
og_title: Cara Mengunduh Ikon dengan Python – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to download icons using Python. We'll also cover how to extract
    favicon, read HTML document Python, and write binary file python in a single tutorial.
  headline: How to Download Icons with Python – Complete Guide
  type: TechArticle
tags:
- python
- web-scraping
- favicon
- file-io
title: Cara Mengunduh Ikon dengan Python – Panduan Lengkap
url: /id/python/general/how-to-download-icons-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengunduh Ikon dengan Python – Panduan Lengkap

Pernah bertanya-tanya **cara mengunduh ikon** dari sebuah situs web tanpa harus mengklik kanan satu per satu? Anda bukan satu-satunya. Baik Anda sedang membangun alat audit merek atau hanya ingin salinan lokal dari setiap favicon yang Anda temui, menguasai tugas ini menghemat waktu dan penekanan tombol.

Dalam tutorial ini kami akan membahas **cara mengunduh ikon** dari file HTML menggunakan Python murni. Kami juga akan menunjukkan **cara mengekstrak favicon**, mendemonstrasikan **read html document python**, dan menjelaskan **write binary file python** sehingga Anda mendapatkan folder .ico yang rapi siap untuk proyek apa pun.

---

## Apa yang Anda Butuhkan

- Python 3.8+ (perpustakaan standar sudah cukup)
- Salinan lokal halaman HTML yang ingin Anda pindai (atau URL yang dapat Anda ambil)
- Pemahaman dasar tentang I/O file di Python  
- Tidak memerlukan paket eksternal, tetapi `beautifulsoup4` dapat membuat proses lebih lancar jika Anda menginginkannya (opsional)

Sudah siap? Bagus—mari kita mulai.

![Contoh cara mengunduh ikon](https://example.com/placeholder.png "contoh cara mengunduh ikon")

---

## Langkah 1: Muat Dokumen HTML di Python  

Pertama-tama, kita perlu **load html python** style—membaca file ke memori sehingga kita dapat memeriksa tag `<link>`-nya. Cara termudah adalah membuka file dengan fungsi bawaan `open` dan membacanya sebagai teks.

```python
# Step 1: Load the HTML document
HTML_PATH = "YOUR_DIRECTORY/sample.html"

# Using the built‑in open() to read the file as a string
with open(HTML_PATH, "r", encoding="utf-8") as f:
    html_content = f.read()
```

*Mengapa langkah ini?*  
Membaca HTML memberi kita string mentah yang dapat diparsing. Jika Anda melewatkan ini dan mencoba bekerja dengan jalur secara langsung, parser tidak akan memiliki apa pun untuk diperiksa.

---

## Langkah 2: Parse Dokumen dan Temukan Tautan Ikon  

Sekarang kita perlu **read html document python** style. Meskipun Anda bisa menggunakan regex, parser HTML kecil menjaga keandalan. Python menyediakan `html.parser` yang dapat kita subclass untuk keperluan kita.

```python
from html.parser import HTMLParser

class IconLinkParser(HTMLParser):
    """Collects href attributes from <link rel='icon'> tags."""
    def __init__(self):
        super().__init__()
        self.icon_hrefs = []

    def handle_starttag(self, tag, attrs):
        if tag.lower() != "link":
            return
        attrs_dict = dict(attrs)
        # Look for rel="icon" (or rel="shortcut icon")
        rel = attrs_dict.get("rel", "").lower()
        if "icon" in rel:
            href = attrs_dict.get("href")
            if href:
                self.icon_hrefs.append(href)

# Instantiate and feed the HTML content
parser = IconLinkParser()
parser.feed(html_content)

# Now we have a list of all icon URLs
icon_hrefs = parser.icon_hrefs
print(f"Found {len(icon_hrefs)} icon link(s):", icon_hrefs)
```

**Penjelasan**  

- `handle_starttag` dipanggil untuk setiap tag pembuka.  
- Kami menyaring elemen `<link>` yang atribut `rel`‑nya mengandung kata *icon*. Ini mencakup baik `rel="icon"` dan `rel="shortcut icon"` yang lebih lama.  
- Nilai `href` disimpan dalam `icon_hrefs`, siap untuk langkah berikutnya.

---

## Langkah 3: Resolusi Jalur Relatif (Opsional tapi Membantu)

Jika HTML menggunakan URL relatif, kita harus mengubahnya menjadi jalur sistem file absolut. Di sinilah pengetahuan **load html python** bertemu dengan `urllib.parse`.

```python
import os
from urllib.parse import urljoin

# Base directory where the HTML file lives
BASE_DIR = os.path.dirname(os.path.abspath(HTML_PATH))

def resolve_path(href):
    # If href already looks like an absolute path, return it unchanged
    if os.path.isabs(href):
        return href
    # Otherwise, join it with the base directory
    return os.path.normpath(os.path.join(BASE_DIR, href))

resolved_icon_paths = [resolve_path(h) for h in icon_hrefs]
print("Resolved paths:", resolved_icon_paths)
```

*Mengapa repot?*  
Ketika Anda nanti **write binary file python**, Anda memerlukan jalur file yang sebenarnya. URL relatif seperti `images/favicon.ico` akan menyebabkan `FileNotFoundError`.

---

## Langkah 4: Tulis Setiap Ikon ke File Biner Lokal  

Inilah inti dari **cara mengunduh ikon**. Kami akan mengulangi jalur yang telah diresolusi, membaca setiap ikon sebagai data biner, dan menuliskannya ke file baru dalam folder `icons/` khusus.

```python
import shutil

OUTPUT_DIR = "YOUR_DIRECTORY/icons"
os.makedirs(OUTPUT_DIR, exist_ok=True)

for index, icon_path in enumerate(resolved_icon_paths):
    # Guard against missing files
    if not os.path.isfile(icon_path):
        print(f"⚠️  Icon file not found: {icon_path}")
        continue

    # Destination filename: icon_0.ico, icon_1.ico, …
    dest_path = os.path.join(OUTPUT_DIR, f"icon_{index}.ico")

    # **write binary file python** – copy the binary data
    with open(icon_path, "rb") as src_file, open(dest_path, "wb") as dst_file:
        shutil.copyfileobj(src_file, dst_file)

    print(f"✅ Saved {dest_path}")
```

**Apa yang terjadi?**  

- `os.makedirs(..., exist_ok=True)` memastikan folder output ada.  
- `shutil.copyfileobj` menyalurkan byte dari sumber ke tujuan, yang merupakan cara paling efisien memori untuk **write binary file python**.  
- Kami menamai setiap file `icon_<index>.ico` untuk menghindari benturan.

**Output yang Diharapkan**

```
Found 2 icon link(s): ['images/favicon.ico', 'icons/custom.ico']
Resolved paths: ['/path/to/YOUR_DIRECTORY/images/favicon.ico',
                '/path/to/YOUR_DIRECTORY/icons/custom.ico']
✅ Saved YOUR_DIRECTORY/icons/icon_0.ico
✅ Saved YOUR_DIRECTORY/icons/icon_1.ico
```

Setelah skrip selesai, Anda akan memiliki kumpulan file ikon yang bersih siap untuk tugas selanjutnya apa pun.

---

## Langkah 5: Bonus – Unduh Ikon Langsung dari URL Remote  

Jika HTML Anda berada di web alih-alih di disk lokal, ganti bagian pembacaan file dengan panggilan `requests` kecil. Ini mendemonstrasikan **cara mengekstrak favicon** dari halaman langsung mana pun.

```python
import requests

REMOTE_URL = "https://example.com"

# Grab the HTML
response = requests.get(REMOTE_URL)
response.raise_for_status()
html_content = response.text

# Re‑run the parser (same as before) to get icon URLs
parser = IconLinkParser()
parser.feed(html_content)
icon_hrefs = parser.icon_hrefs

# Download each icon via HTTP
for index, href in enumerate(icon_hrefs):
    # Resolve relative URLs against the page URL
    icon_url = urljoin(REMOTE_URL, href)
    r = requests.get(icon_url, stream=True)
    r.raise_for_status()
    dest_path = os.path.join(OUTPUT_DIR, f"remote_icon_{index}.ico")
    with open(dest_path, "wb") as out_file:
        shutil.copyfileobj(r.raw, out_file)
    print(f"✅ Downloaded {icon_url} → {dest_path}")
```

**Mengapa menambahkan ini?**  
Banyak proyek dunia nyata perlu meng-scrape favicon dari situs live. Potongan kode ini menunjukkan Anda dapat memperluas logika **cara mengunduh ikon** yang sama ke internet dengan hanya beberapa baris tambahan.

---

## Kesalahan Umum & Tips Pro

- **Missing `rel="icon"`** – Beberapa situs menyematkan ikon melalui tag `<meta>` atau CSS. Jika Anda membutuhkannya, perluas parser untuk mencari `<meta name="msapplication‑TileImage">` atau URL `background-image` CSS.  
- **Non‑ICO formats** – Favicon modern sering menggunakan `.png` atau `.svg`. Kode di atas bekerja untuk gambar biner apa pun; cukup sesuaikan ekstensi file di `dest_path` jika Anda ingin mempertahankan format asli.  
- **Permission errors** – Saat menulis file, pastikan skrip Anda dijalankan dengan izin menulis ke folder target. Menggunakan `os.makedirs(..., exist_ok=True)` menghindari crash “directory not found”.  
- **Large HTML files** – Untuk halaman yang sangat besar, pertimbangkan streaming file baris per baris alih-alih memuat seluruh string ke memori. `HTMLParser` bawaan dapat menangani feed inkremental.  

---

## Kesimpulan

Anda baru saja mempelajari **cara mengunduh ikon** dari dokumen HTML menggunakan Python murni. Dengan **reading html document python**, mem-parsing tag `<link rel="icon">`, menyelesaikan jalur relatif apa pun, dan akhirnya **write binary file python** untuk menyimpan setiap ikon secara lokal, Anda kini memiliki skrip yang dapat digunakan kembali yang berfungsi untuk halaman lokal maupun remote.

Langkah selanjutnya? Coba perluas parser untuk menangkap Apple touch icons (`rel="apple-touch-icon"`), atau integrasikan skrip ke dalam pipeline perayapan web yang lebih besar yang mengumpulkan favicon untuk ratusan domain. Dasar-dasar yang dibahas di sini—parsing HTML, resolusi jalur, dan penanganan file biner—adalah blok bangunan untuk banyak tugas otomasi web.

Ada pertanyaan atau ingin berbagi kasus penggunaan menarik? Tinggalkan komentar di bawah, dan selamat berburu ikon!

## Apa yang Harus Anda Pelajari Selanjutnya?

- [Cara Mengedit Pohon Dokumen HTML di Aspose.HTML untuk Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Cara Mengonversi HTML ke PDF Java – Menggunakan Aspose.HTML untuk Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Cara Mengonversi HTML ke JPEG Menggunakan Aspose.HTML untuk Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-jpeg/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
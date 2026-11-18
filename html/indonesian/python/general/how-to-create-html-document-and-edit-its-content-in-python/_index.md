---
category: general
date: 2026-08-25
description: Pelajari cara membuat dokumen HTML, memilih elemen CSS, memodifikasi
  teks HTML, dan menyimpan file HTML menggunakan skrip Python sederhana.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create html document
- select element css
- modify html text
- save html file
- how to edit html
language: id
lastmod: 2026-08-25
og_description: Buat dokumen HTML, pilih elemen CSS, ubah teks HTML, dan simpan file
  HTML dalam beberapa baris Python. Ikuti tutorial lengkap ini.
og_image_alt: Screenshot of a Python script that creates and updates an HTML file
og_title: Buat dokumen HTML dan edit isinya dengan Python – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-08-25'
  description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  headline: How to create html document and edit its content in Python
  type: TechArticle
- description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  name: How to create html document and edit its content in Python
  steps:
  - name: Full script for quick copy‑paste
    text: '```python # ------------------------------------------------- # File: edit_html.py
      # ------------------------------------------------- # Purpose: Demonstrate how
      to create html document, # select an element with CSS, modify its text, # and
      save the result to a file. # -------------------------------'
  - name: Selecting multiple elements
    text: If you need to **select element css** selectors that match several tags
      (e.g., `"div.note"`), use `doc.select("div.note")` which returns a list. Iterate
      over the list to apply changes to each element.
  - name: Preserving existing attributes
    text: 'When you replace the text, BeautifulSoup retains any attributes on the
      tag. For example:'
  - name: Handling missing elements gracefully
    text: In production scripts, you often encounter malformed HTML. Wrap the selection
      in a conditional or try‑except block, as shown in Step 4, to avoid crashes.
  - name: Writing to a specific directory
    text: 'Replace `output_path` with an absolute or relative path:'
  type: HowTo
tags:
- Python
- HTML manipulation
- CSS selectors
- File I/O
title: Cara membuat dokumen HTML dan mengedit isinya di Python
url: /id/python/general/how-to-create-html-document-and-edit-its-content-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat dokumen html dan mengedit isinya dengan Python

Jika Anda perlu **create html document** dari awal dan mengubah elemennya secara programatis, panduan ini menunjukkan cara melakukannya. Anda akan melihat skrip singkat yang dapat dijalankan yang membuat file, memilih paragraf dengan selector CSS, memperbarui teks, dan menulis hasilnya kembali ke disk.

Bekerja dengan HTML di Python umum dilakukan saat menghasilkan laporan, templat email, atau konten situs statis. Pada akhir tutorial ini Anda akan dapat **select element css**, **modify html text**, dan **save html file** tanpa meninggalkan kenyamanan IDE Anda.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* Python 3.9 atau yang lebih baru terpasang.
* Paket `beautifulsoup4` dan `lxml` (pasang dengan `pip install beautifulsoup4 lxml`).
* Izin menulis ke direktori tempat Anda berencana menyimpan file output.

Tidak ada alat tambahan yang diperlukan; pustaka standar menangani I/O file.

## Langkah 1: Instal pustaka yang diperlukan

```bash
pip install beautifulsoup4 lxml
```

`beautifulsoup4` menyediakan API yang nyaman untuk parsing dan manipulasi HTML, sementara `lxml` menyediakan parser cepat yang memahami selector CSS.

## Langkah 2: Buat dokumen HTML awal

```python
from bs4 import BeautifulSoup

# Define the initial markup as a string
initial_html = "<p>Old</p>"

# Parse the markup into a BeautifulSoup object
doc = BeautifulSoup(initial_html, "lxml")
```

Konstruktor `BeautifulSoup` membangun objek **create html document** di memori. Menggunakan parser `"lxml"` memastikan dukungan penuh untuk selector CSS.

## Langkah 3: Pilih elemen paragraf menggunakan selector CSS

```python
# Use the CSS selector "p" to locate the first <p> element
para = doc.select_one("p")
```

Metode `select_one` mengimplementasikan logika **select element css**, mengembalikan tag pertama yang cocok. Jika selector tidak menemukan apa pun, `para` akan bernilai `None`, sehingga pemeriksaan defensif disarankan dalam kode produksi.

## Langkah 4: Modifikasi konten teks paragraf

```python
if para is not None:
    # Replace the existing text with new content
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")
```

Menetapkan nilai ke `para.string` melakukan operasi **modify html text**. BeautifulSoup memperbarui pohon DOM yang mendasarinya, sehingga perubahan tercermin saat dokumen diserialisasi.

## Langkah 5: Simpan HTML yang telah diperbarui ke file

```python
output_path = "updated.html"

# Write the prettified HTML to disk
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())
print(f"HTML file saved to {output_path}")
```

Pemanggilan `open` bersama `write` mengimplementasikan fungsionalitas **save html file**. Menggunakan `prettify()` menghasilkan output yang terindentasi rapi, yang berguna saat debugging.

### Skrip lengkap untuk salin‑tempel cepat

```python
# -------------------------------------------------
# File: edit_html.py
# -------------------------------------------------
# Purpose: Demonstrate how to create html document,
#          select an element with CSS, modify its text,
#          and save the result to a file.
# -------------------------------------------------

from bs4 import BeautifulSoup

# 1️⃣ Create an HTML document with initial content
initial_html = "<p>Old</p>"
doc = BeautifulSoup(initial_html, "lxml")

# 2️⃣ Locate the paragraph element using a CSS selector
para = doc.select_one("p")

# 3️⃣ Update the text inside the paragraph
if para is not None:
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")

# 4️⃣ Save the modified document to a file
output_path = "updated.html"
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())

print(f"HTML file saved to {output_path}")
# -------------------------------------------------
```

Menjalankan `python edit_html.py` membuat `updated.html` yang berisi:

```html
<p>
 New
</p>
```

## Variasi umum dan kasus tepi

### Memilih beberapa elemen

Jika Anda perlu **select element css** yang cocok dengan beberapa tag (misalnya, `"div.note"`), gunakan `doc.select("div.note")` yang mengembalikan daftar. Iterasi daftar tersebut untuk menerapkan perubahan pada setiap elemen.

```python
for note in doc.select("div.note"):
    note.string = "Updated note"
```

### Mempertahankan atribut yang ada

Saat Anda mengganti teks, BeautifulSoup mempertahankan atribut apa pun pada tag. Contohnya:

```python
initial_html = '<p class="intro">Old</p>'
doc = BeautifulSoup(initial_html, "lxml")
para = doc.select_one("p.intro")
para.string = "New"
# Result: <p class="intro">New</p>
```

### Menangani elemen yang hilang secara elegan

Dalam skrip produksi, Anda sering menemui HTML yang tidak terstruktur dengan baik. Bungkus pemilihan dalam kondisi atau blok try‑except, seperti yang ditunjukkan pada Langkah 4, untuk menghindari crash.

### Menulis ke direktori tertentu

Ganti `output_path` dengan jalur absolut atau relatif:

```python
output_path = r"C:\Temp\updated.html"   # Windows
# or
output_path = "/home/user/updated.html"  # Linux/macOS
```

Pastikan direktori tersebut ada; jika tidak, Python akan mengeluarkan `FileNotFoundError`.

## Tips profesional

* **Performance** – Untuk file HTML besar, lebih baik gunakan `lxml.etree` secara langsung; BeautifulSoup menambahkan lapisan abstraksi tipis yang nyaman namun sedikit lebih lambat.
* **Encoding** – Selalu buka file dengan `encoding="utf-8"` untuk mempertahankan karakter non‑ASCII.
* **Testing** – Setelah modifikasi, Anda dapat memverifikasi output dengan `assert "New" in open(output_path).read()` dalam unit test.

## Kesimpulan

Anda kini tahu cara **create html document**, menggunakan kueri **select element css** untuk menemukan node, **modify html text**, dan akhirnya **save html file** dengan Python. Pola ini dapat diperluas ke transformasi yang lebih kompleks seperti pembaruan massal, perubahan atribut, atau pembuatan templat.

Selanjutnya, jelajahi topik terkait seperti **how to edit html** menggunakan ekspresi XPath, menghasilkan halaman HTML lengkap dengan Jinja2, atau mengotomatisasi pemrosesan batch banyak file. Masing‑masing topik tersebut membangun di atas langkah‑langkah inti yang ditunjukkan di sini dan memperluas toolkit Anda untuk manipulasi HTML secara programatis.


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik yang sangat terkait dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Create HTML Document with Aspose.HTML – Step‑by‑Step Guide](/html/english/net/html-document-manipulation/create-html-document-with-aspose-html-step-by-step-guide/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Save HTML Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
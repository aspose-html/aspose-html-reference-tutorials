---
category: general
date: 2026-05-31
description: Pelajari cara mendapatkan elemen berdasarkan ID, mengubah warna latar
  belakang HTML, membaca teks HTML, dan mengatur atribut HTML menggunakan Python.
  Tutorial langkah demi langkah.
draft: false
keywords:
- get element by id
- change background colour html
- how to read html text
- how to set html attribute
- manipulate html with python
language: id
og_description: Dapatkan elemen berdasarkan id, baca teks HTML, atur atribut HTML,
  dan ubah warna latar belakang HTML menggunakan Python dalam panduan tunggal yang
  mudah diikuti.
og_title: Dapatkan elemen berdasarkan id di Python – Tutorial Manipulasi HTML Lengkap
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  headline: Get element by id in Python – Complete HTML Manipulation Guide
  type: TechArticle
- description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  name: Get element by id in Python – Complete HTML Manipulation Guide
  steps:
  - name: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
    text: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
  - name: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
    text: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
  - name: '**Retrieves** the element using **get element by id**.'
    text: '**Retrieves** the element using **get element by id**.'
  - name: '**Prints** the element’s text—showing **how to read HTML text**.'
    text: '**Prints** the element’s text—showing **how to read HTML text**.'
  - name: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
    text: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
  - name: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
    text: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
  - name: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
    text: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
  type: HowTo
tags:
- python
- html
- web‑scraping
title: Dapatkan elemen berdasarkan ID di Python – Panduan Lengkap Manipulasi HTML
url: /id/python/general/get-element-by-id-in-python-complete-html-manipulation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dapatkan elemen berdasarkan id di Python – Panduan Lengkap Manipulasi HTML

Pernah perlu **mendapatkan elemen berdasarkan id** dari sebuah halaman HTML saat menulis skrip Python cepat? Anda tidak sendirian—banyak pengembang mengalami kendala yang sama ketika mulai merayapi situs atau mengutak‑atik laporan lokal. Kabar baiknya? Dengan beberapa baris kode Anda dapat membaca teks elemen, mengubah warna latar belakangnya, dan bahkan menambahkan atribut baru, semua tanpa meninggalkan editor Anda.

Dalam tutorial ini kita akan membahas contoh dunia nyata: memuat file `sample.html` lokal, mengambil elemen yang ID‑nya `main‑content`, mencetak teks dalamnya, dan akhirnya mengganti warna latar belakang menjadi abu‑abu muda. Pada akhir tutorial Anda juga akan mengetahui **cara membaca teks HTML**, **cara menetapkan atribut HTML**, dan mengapa **manipulasi HTML dengan Python** adalah keterampilan berguna dalam kotak peralatan otomatisasi apa pun.

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki:

- **Python 3.9+** (versi terbaru apa pun sudah cukup)
- Library **`lxml`** (atau **BeautifulSoup** jika Anda lebih suka) – kami akan menggunakan `lxml.html` karena menyediakan API bergaya `get_element_by_id` yang bersih.
- Sebuah file HTML kecil bernama `sample.html` yang berada di dalam folder bernama `YOUR_DIRECTORY`. Silakan salin potongan di bawah ini ke dalam file tersebut:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Demo Page</title>
</head>
<body>
    <div id="main-content">
        Hello, world! This is the original text.
    </div>
</body>
</html>
```

Itu saja—tidak ada kerangka kerja mewah, hanya Python biasa dan file HTML statis.

## Langkah 1: Instal Library yang Diperlukan

Jika Anda belum menginstal `lxml`, buka terminal dan jalankan:

```bash
pip install lxml
```

*Tip pro:* Menggunakan lingkungan virtual membuat instalasi Python global Anda tetap rapi, terutama saat Anda mengelola banyak proyek.

## Langkah 2: Muat Dokumen HTML

Sekarang kita akan membaca file ke dalam objek dokumen `lxml.html`. Anggap ini seperti mengubah teks mentah menjadi pohon yang dapat dinavigasi.

```python
from lxml import html
import pathlib

# Resolve the path to the sample file
html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")

# Parse the file into an HTML document
doc = html.parse(str(html_path)).getroot()
print("Document loaded successfully.")
```

Menjalankan kode ini akan mencetak “Document loaded successfully.” Jika file tidak dapat ditemukan, Python akan mengeluarkan `FileNotFoundError`—baik untuk ditangkap lebih awal sebelum Anda mengejar elemen yang tidak ada.

## Langkah 3: Dapatkan elemen berdasarkan id

Inilah inti permasalahannya. `lxml` menyediakan metode `get_element_by_id` yang mirip dengan API DOM yang Anda gunakan di JavaScript.

```python
# Retrieve the element with the specific ID
elem = doc.get_element_by_id("main-content")

if elem is not None:
    print("Element found!")
else:
    print("No element with that ID.")
```

Ketika elemen ada, Anda akan melihat “Element found!” tercetak di konsol. Inilah langkah **get element by id** yang menjadi dasar sebagian besar manipulasi selanjutnya.

## Langkah 4: Cara membaca teks HTML

Setelah Anda memiliki elemen, mengekstrak teks yang terlihat sangat mudah. Metode `text_content()` mengembalikan semua isi di dalamnya, tanpa tag.

```python
if elem is not None:
    # Show the element's current inner text
    inner_text = elem.text_content()
    print("Inner text:", inner_text)
```

Output yang diharapkan:

```
Inner text: Hello, world! This is the original text.
```

Anda mungkin bertanya, *bagaimana jika elemen berisi tag bersarang?* `text_content()` tetap berfungsi—ia menggabungkan semua node teks keturunan, memberi Anda string bersih yang dapat Anda log, simpan, atau berikan ke algoritma lain.

## Langkah 5: Cara menetapkan atribut HTML

Mengubah atau menambahkan atribut juga semudah itu. Metode `set` memungkinkan Anda menetapkan nama atribut apa pun yang Anda inginkan.

```python
if elem is not None:
    # Set a custom data attribute
    elem.set("data-modified", "true")
    # Verify it was added
    print("New attribute value:", elem.get("data-modified"))
```

Output:

```
New attribute value: true
```

Baris itu memperlihatkan **cara menetapkan atribut HTML** secara dinamis. Anda dapat mengganti `"data-modified"` dengan `"class"`, `"title"` atau atribut lain yang didukung elemen.

## Langkah 6: Ubah warna latar belakang HTML

Sekarang untuk penyesuaian visual. Untuk mengubah warna latar belakang, kita menyuntikkan atribut `style` yang menimpa nilai default.

```python
if elem is not None:
    # Change the background colour via a style attribute
    elem.set("style", "background:#f0f0f0")
    print("Background style applied.")
```

Setelah menjalankan skrip, `div` dalam `sample.html` akan terlihat seperti ini ketika Anda membukanya di peramban:

```html
<div id="main-content" data-modified="true" style="background:#f0f0f0">
    Hello, world! This is the original text.
</div>
```

Itulah teknik **change background colour html** yang dapat Anda pakai ulang untuk elemen apa pun—cukup ganti kode warna.

## Langkah 7: Manipulasi HTML dengan Python – Menggabungkan Semua Langkah

Berikut adalah skrip lengkap yang dapat dijalankan, menggabungkan semua langkah. Simpan sebagai `modify_html.py` dan jalankan dari direktori yang sama dengan folder `YOUR_DIRECTORY` Anda.

```python
#!/usr/bin/env python3
"""
Complete example: load an HTML file, get element by id,
read its text, set a new attribute, and change its background colour.
"""

from lxml import html
import pathlib
import sys

def main():
    # 1️⃣ Load the document
    html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")
    try:
        doc = html.parse(str(html_path)).getroot()
    except OSError as e:
        sys.exit(f"Failed to read HTML file: {e}")

    # 2️⃣ Get element by id
    elem = doc.get_element_by_id("main-content")
    if elem is None:
        sys.exit("Element with ID 'main-content' not found.")

    # 3️⃣ Read HTML text
    print("🗒️  Inner text:", elem.text_content())

    # 4️⃣ Set a new attribute
    elem.set("data-modified", "true")
    print("✅  data-modified attribute set to:", elem.get("data-modified"))

    # 5️⃣ Change background colour HTML
    elem.set("style", "background:#f0f0f0")
    print("🎨  Background colour changed to #f0f0f0")

    # 6️⃣ Write the modified HTML back to disk
    output_path = pathlib.Path("YOUR_DIRECTORY/sample_modified.html")
    output_path.write_text(html.tostring(doc, pretty_print=True, encoding="unicode"))
    print(f"💾  Modified file saved as {output_path}")

if __name__ == "__main__":
    main()
```

### Penjelasan skrip baris per baris

1. **Impor** `lxml.html` untuk parsing dan `pathlib` untuk path yang bersifat lintas‑OS.  
2. **Muat** `sample.html` dan hentikan dengan pesan jelas bila file tidak ada.  
3. **Ambil** elemen menggunakan **get element by id**.  
4. **Cetak** teks elemen—menunjukkan **cara membaca teks HTML**.  
5. **Tambahkan** atribut khusus, memperlihatkan **cara menetapkan atribut HTML**.  
6. **Ubah** warna latar belakang, memenuhi kebutuhan **change background colour html**.  
7. **Tulis** markup yang telah diperbarui ke `sample_modified.html`, sehingga Anda dapat membukanya di peramban dan melihat perubahan.

Menjalankan skrip akan menghasilkan output konsol serupa dengan:

```
🗒️  Inner text: Hello, world! This is the original text.
✅  data-modified attribute set to: true
🎨  Background colour changed to #f0f0f0
💾  Modified file saved as YOUR_DIRECTORY/sample_modified.html
```

Buka `sample_modified.html` dan Anda akan melihat latar belakang abu‑abu di belakang teks—bukti bahwa **manipulasi HTML dengan python** memang berhasil.

## Kesalahan Umum & Cara Menghindarinya

- **ID tidak ada** – Jika elemen target tidak ada, `get_element_by_id` mengembalikan `None`. Selalu periksa `None` sebelum mengakses properti; bila tidak, Anda akan mendapatkan `AttributeError`.  
- **Masalah encoding** – Saat membaca halaman non‑ASCII, berikan `encoding='utf-8'` ke `html.parse` atau pastikan file Anda disimpan dalam UTF‑8.  
- **Menimpa style yang sudah ada** – Menetapkan atribut `style` menggantikan semua style inline sebelumnya. Jika Anda perlu mempertahankan aturan yang ada, baca nilai `style` saat ini terlebih dahulu, tambahkan aturan baru, lalu tulis kembali.  
- **Izin file** – Menulis kembali ke folder yang sama dapat gagal pada sistem read‑only. Pilih jalur output yang dapat ditulisi, seperti yang kami lakukan dengan `sample_modified.html`.

## Memperluas Contoh

Setelah menguasai dasar‑dasarnya, pertimbangkan langkah selanjutnya berikut:

- **Loop melalui banyak ID** – Gunakan daftar ID dan iterasi dengan `for` untuk memproses beberapa bagian halaman sekaligus.  
- **Ganti teks konten** – Panggil `elem.text = "Teks baru"` untuk mengubah string yang terlihat.  
- **Tambahkan elemen anak** – Gunakan `

## Apa yang Harus Anda Pelajari Selanjutnya?

- [Cara Mengedit HTML Menggunakan Aspose.HTML untuk Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Cara Menanyakan HTML di Java – Tutorial Lengkap](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Cara Mengonversi HTML ke PDF Java – Menggunakan Aspose.HTML untuk Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
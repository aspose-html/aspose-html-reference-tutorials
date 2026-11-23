---
category: general
date: 2026-09-19
description: Pelajari cara mengubah judul dalam file HTML dengan Python. Panduan ini
  mencakup membaca HTML, memperbarui tag judul, dan menyimpan HTML yang telah dimodifikasi.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to change title
- update html title
- read html with python
- load html file python
- save modified html
language: id
lastmod: 2026-09-19
og_description: Cara mengubah judul dalam file HTML dengan Python. Ikuti contoh lengkap
  ini untuk membaca HTML, memperbarui tag judul, dan menyimpan dokumen yang telah
  dimodifikasi.
og_image_alt: Diagram showing how to change title in an HTML file using Python
og_title: Cara mengubah judul dalam file HTML menggunakan Python – panduan langkah
  demi langkah
schemas:
- author: Aspose
  dateModified: '2026-09-19'
  description: Learn how to change title in an HTML file with Python. This guide covers
    reading HTML, updating the title tag, and saving the modified HTML.
  headline: How to change title in an HTML file using Python
  type: TechArticle
tags:
- Python
- HTML
- Web scraping
title: Cara mengubah judul dalam file HTML menggunakan Python
url: /id/python/general/how-to-change-title-in-an-html-file-using-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengubah judul dalam file HTML menggunakan Python

Jika Anda perlu **cara mengubah judul** dalam dokumen HTML secara programatis, Python membuat pekerjaan ini menjadi mudah. Pada tutorial ini Anda akan membaca file HTML, memperbarui elemen `<title>`, dan menyimpan HTML yang telah dimodifikasi kembali ke disk—semua dengan kode yang jelas dan dapat dijalankan.

Mengubah judul halaman adalah langkah umum ketika Anda menghasilkan situs statis, menyesuaikan halaman yang di‑scrape, atau mengotomatisasi pembaruan SEO. Pada akhir panduan ini Anda akan tahu cara **memperbarui judul html**, cara **membaca html dengan python**, dan cara **menyimpan html yang dimodifikasi** dengan aman.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

- Python 3.8 atau yang lebih baru terpasang  
- Paket `beautifulsoup4` (`pip install beautifulsoup4`)  
- Sebuah file HTML yang ingin Anda edit (contoh menggunakan `index.html` dalam folder pilihan Anda)  

Tidak ada layanan eksternal yang diperlukan; semuanya berjalan secara lokal.

## Langkah 1: Muat file HTML dengan Python  

Tugas pertama adalah **memuat file html python**‑style. Menggunakan `BeautifulSoup` memberi Anda parser yang toleran terhadap markup yang tidak sempurna.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Define the directory that holds the original HTML
html_dir = Path("YOUR_DIRECTORY")
original_path = html_dir / "index.html"

# Read the file contents (this is how you **read html with python**)
with original_path.open(encoding="utf-8") as f:
    html_content = f.read()

# Parse the document
soup = BeautifulSoup(html_content, "html.parser")
```

*Mengapa langkah ini penting:*  
`BeautifulSoup` membangun representasi pohon, memungkinkan Anda menanyakan dan memodifikasi elemen tanpa harus menangani string secara manual. `html.parser` bawaan cepat dan tidak memerlukan binari tambahan.

## Langkah 2: Temukan elemen `<title>`  

Dokumen HTML biasanya berisi satu tag `<title>` di dalam `<head>`. Kami mengambil kemunculan pertama, yang memenuhi kebutuhan **memperbarui judul html**.

```python
# Find the first <title> element; BeautifulSoup returns None if missing
title_tag = soup.find("title")

if title_tag is None:
    # If the document lacks a <title>, create one inside <head>
    head_tag = soup.find("head")
    if head_tag is None:
        # As a safety net, add a <head> element at the top
        head_tag = soup.new_tag("head")
        soup.insert(0, head_tag)
    title_tag = soup.new_tag("title")
    head_tag.append(title_tag)

# Show the current title (useful for debugging)
print("Current title:", title_tag.string)
```

*Mengapa kami memeriksa `None`*:  
Beberapa fragmen HTML tidak menyertakan judul. Menambahkannya secara otomatis mencegah kesalahan di kemudian hari dan membuat skrip lebih tangguh.

## Langkah 3: Ubah teks judul  

Sekarang kami **memperbarui judul html** dengan menetapkan teks baru ke string tag tersebut. Inilah inti dari operasi **cara mengubah judul**.

```python
new_title = "New Title"

# Replace the existing title text
title_tag.string = new_title

print("Updated title:", title_tag.string)
```

Atribut `string` mewakili node teks di dalam `<title>`. Menimpanya memperbarui DOM di memori.

## Langkah 4: Simpan HTML yang telah dimodifikasi  

Akhirnya, tulis dokumen yang telah diubah ke file baru. Ini menyelesaikan langkah **menyimpan html yang dimodifikasi** dan menjaga file asli tetap tidak tersentuh.

```python
# Define the output path
modified_path = html_dir / "index_modified.html"

# Write the prettified HTML back to disk
with modified_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())

print(f"Modified HTML saved to {modified_path}")
```

`prettify()` memformat output dengan indentasi, sehingga file mudah dibaca setelah perubahan.

### Output yang diharapkan

Menjalankan skrip pada contoh `index.html` yang awalnya berisi:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Old Title</title>
</head>
<body>
    <h1>Welcome</h1>
</body>
</html>
```

akan menghasilkan output konsol serupa dengan:

```
Current title: Old Title
Updated title: New Title
Modified HTML saved to YOUR_DIRECTORY/index_modified.html
```

File `index_modified.html` yang disimpan kini akan dimulai dengan:

```html
<!DOCTYPE html>
<html>
 <head>
  <title>
   New Title
  </title>
 </head>
 <body>
  <h1>
   Welcome
  </h1>
 </body>
</html>
```

## Skrip lengkap untuk salin‑tempel cepat

Berikut adalah program lengkap yang siap dijalankan yang menggabungkan keempat langkah. Simpan sebagai `change_title.py` dan sesuaikan `YOUR_DIRECTORY` sesuai kebutuhan.

```python
# change_title.py
from pathlib import Path
from bs4 import BeautifulSoup

# ----------------------------------------------------------------------
# Configuration – change these values to match your environment
# ----------------------------------------------------------------------
html_dir = Path("YOUR_DIRECTORY")          # Folder containing index.html
original_file = html_dir / "index.html"
modified_file = html_dir / "index_modified.html"
new_title = "New Title"                    # Desired title text
# ----------------------------------------------------------------------

# 1️⃣ Load the HTML file (read html with python)
with original_file.open(encoding="utf-8") as f:
    html_content = f.read()

soup = BeautifulSoup(html_content, "html.parser")

# 2️⃣ Locate or create the <title> element
title_tag = soup.find("title")
if title_tag is None:
    head_tag = soup.find("head")
    if head_tag is None:
        head_tag = soup.new_tag("head")
        soup.insert(0, head_tag)
    title_tag = soup.new_tag("title")
    head_tag.append(title_tag)

print("Current title:", title_tag.string)

# 3️⃣ Update the title (how to change title)
title_tag.string = new_title
print("Updated title:", title_tag.string)

# 4️⃣ Save the modified HTML (save modified html)
with modified_file.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())

print(f"Modified HTML saved to {modified_file}")
```

Jalankan skrip:

```bash
python change_title.py
```

Anda akan melihat pesan konsol dan file baru `index_modified.html` dengan judul yang telah diperbarui.

## Tips tambahan dan kasus tepi

| Situasi | Apa yang harus dilakukan |
|-----------|------------|
| **Beberapa tag `<title>`** | `soup.find_all("title")` mengembalikan daftar; perbarui elemen pertama atau iterasi jika Anda perlu mengubah semuanya. |
| **Masalah enkoding** | Buka file dengan `encoding="utf-8-sig"` jika ada BOM, atau deteksi enkoding dengan `chardet`. |
| **File HTML besar** | Gunakan parser `lxml` (`BeautifulSoup(html_content, "lxml")`) untuk kinerja yang lebih baik. |
| **Mempertahankan format asli** | Jika Anda harus menjaga spasi persis, tulis `str(soup)` alih‑alih `prettify()`. |
| **Mengotomatisasi pada banyak file** | Bungkus logika dalam fungsi dan loop melalui `Path.rglob("*.html")`. |

Variasi ini menjaga logika inti **cara mengubah judul** tetap utuh sambil menyesuaikan dengan proyek dunia nyata.

## Kesimpulan

Anda kini tahu cara **cara mengubah judul** dalam dokumen HTML apa pun menggunakan Python. Tutorial ini mencakup membaca HTML, menemukan tag `<title>`, memperbarui teksnya, dan **menyimpan html yang dimodifikasi** dengan aman. Dengan skrip lengkap Anda dapat mengintegrasikan pola ini ke dalam generator situs statis, pipeline SEO, atau otomatisasi apa pun yang memerlukan perubahan judul dinamis.

Selanjutnya, jelajahi topik terkait seperti **membaca html dengan python** untuk mengekstrak meta tag, atau teknik **memuat file html python** untuk menangani markup yang rusak. Bereksperimenlah dengan pemrosesan batch untuk memperbarui judul di seluruh situs—keterampilan baru Anda menjadi dasar bagi banyak tugas otomasi web. Selamat coding!


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik yang sangat terkait dan membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [How to Save HTML with Aspose.Html – Complete C# Guide](/html/english/net/working-with-html-documents/how-to-save-html-with-aspose-html-complete-c-guide/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Render HTML to PNG – Complete Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-render-html-to-png-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
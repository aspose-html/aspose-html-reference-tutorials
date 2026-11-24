---
category: general
date: 2026-11-24
description: Simpan HTML yang telah dimodifikasi dan tambahkan tautan target blank
  di Python menggunakan Aspose.HTML. Pelajari cara mengubah target href untuk semua
  tag <a> dan membuka semua tautan di tab baru.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save modified html
- add target blank links
- change href target
- open all links newtab
language: id
lastmod: 2026-11-24
og_description: Simpan HTML yang telah dimodifikasi dan tambahkan tautan target blank
  di Python dengan Aspose.HTML. Ikuti tutorial langkah demi langkah ini untuk mengubah
  target href dan membuka semua tautan di tab baru.
og_image_alt: Screenshot of a Python script that saves modified HTML with target='_blank'
  on every link
og_title: Simpan HTML yang dimodifikasi dan tambahkan tautan target blank di Python
  – panduan lengkap
schemas:
- author: Aspose
  dateModified: '2026-11-24'
  description: Save modified HTML and add target blank links in Python using Aspose.HTML.
    Learn how to change href target for all <a> tags and open all links newtab.
  headline: Save modified HTML and add target blank links in Python
  type: TechArticle
tags:
- Aspose.HTML
- Python
- HTML manipulation
- Web automation
title: Simpan HTML yang dimodifikasi dan tambahkan tautan target blank di Python
url: /id/python/general/save-modified-html-and-add-target-blank-links-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Simpan HTML yang Dimodifikasi dan Tambahkan Tautan target blank di Python

Jika Anda perlu **menyimpan HTML yang dimodifikasi** setelah memperbarui setiap tautan, panduan ini menunjukkan cara melakukannya dengan Aspose.HTML untuk Python. Anda akan belajar cara **menambahkan tautan target blank**, mengubah target href, dan membuat semua tautan terbuka di tab baru.

Tutorial ini mencakup semua hal mulai dari memuat file HTML hingga memverifikasi bahwa perubahan telah ditulis dengan benar. Tidak ada alat eksternal yang diperlukan selain pustaka Aspose.HTML.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* Python 3.8 atau yang lebih baru terpasang  
* Lisensi aktif Aspose.HTML untuk Python (atau kunci evaluasi gratis)  
* File HTML lokal yang ingin Anda modifikasi (misalnya, `index.html`)  

Anda dapat menginstal pustaka dengan pip:

```bash
pip install aspose-html
```

## Langkah 1: Muat dokumen HTML

Langkah pertama adalah membuat instance `HTMLDocument` yang menunjuk ke file sumber Anda. Objek ini mewakili seluruh pohon DOM, memungkinkan Anda untuk menanyakan dan mengedit elemen.

```python
from aspose.html import HTMLDocument

# Load the original HTML file
doc = HTMLDocument("YOUR_DIRECTORY/index.html")
```

*Mengapa ini penting*: Memuat dokumen memberi Anda akses programatik ke setiap node, yang diperlukan untuk pembaruan massal seperti mengubah atribut `target` pada semua tag `<a>`.

## Langkah 2: Tambahkan tautan target blank ke setiap anchor

Agar setiap hyperlink terbuka di tab baru, Anda menetapkan atribut `target` menjadi `_blank`. Metode `query_selector_all` mengembalikan koleksi hidup semua elemen `<a>`, terlepas dari kedalaman penumpukan.

```python
# Update all <a> tags to open links in a new tab
for link in doc.query_selector_all("a"):
    link.set_attribute("target", "_blank")
```

**Poin penting**

* Loop ini menyentuh setiap anchor tepat satu kali, memastikan **add target blank links** diterapkan secara seragam.  
* Jika sebuah tautan sudah memiliki atribut `target`, pemanggilan ini akan menimpanya, menjamin perilaku yang konsisten.  

### Menangani nilai `target` yang sudah ada (opsional)

Jika Anda lebih suka mempertahankan target yang sudah ada dan hanya menetapkan `_blank` bila atribut belum ada, tambahkan pemeriksaan kondisional:

```python
for link in doc.query_selector_all("a"):
    if not link.has_attribute("target"):
        link.set_attribute("target", "_blank")
```

## Langkah 3: Ubah target href dan buka semua tautan di tab baru

Kadang-kadang Anda perlu menulis ulang atribut `href` itu sendiri—mungkin untuk menambahkan URL dasar atau mengonversi jalur relatif menjadi URL absolut. Teknik traversal DOM yang sama bekerja untuk perubahan `href`.

```python
base_url = "https://example.com/"

for link in doc.query_selector_all("a"):
    href = link.get_attribute("href")
    # Skip empty or already absolute URLs
    if href and not href.startswith("http"):
        new_href = base_url + href.lstrip("/")
        link.set_attribute("href", new_href)
    # Ensure the link opens in a new tab
    link.set_attribute("target", "_blank")
```

*Mengapa ini penting*: Dengan **changing href target** dan memastikan **open all links newtab**, Anda menjamin bahwa pengguna diarahkan ke lokasi yang tepat dan navigasi terjadi tanpa meninggalkan halaman saat ini.

## Langkah 4: Simpan dokumen yang dimodifikasi

Setelah semua modifikasi selesai, panggil `save` untuk menulis perubahan ke file baru. Inilah titik di mana **save modified html** sebenarnya terjadi.

```python
# Save the updated HTML to a new file
doc.save("YOUR_DIRECTORY/index_modified.html")
```

File `index_modified.html` yang dihasilkan berisi setiap tag `<a>` dengan `target="_blank"` dan nilai `href` yang telah diperbarui. Anda dapat membuka file tersebut di browser untuk memverifikasi bahwa mengklik tautan apa pun membuka tab baru.

## Langkah 5: Verifikasi hasil (opsional)

Pemeriksaan cepat membantu memastikan bahwa operasi berhasil:

```python
# Reload the saved file to verify changes
verify_doc = HTMLDocument("YOUR_DIRECTORY/index_modified.html")
for link in verify_doc.query_selector_all("a"):
    assert link.get_attribute("target") == "_blank", "Target attribute not set correctly"
print("All links have target='_blank' and the file was saved successfully.")
```

Jika pernyataan (assertion) gagal, skrip akan mengeluarkan error, menunjukkan elemen yang bermasalah.

## Tips pro: Pemrosesan batch banyak file

Ketika Anda memiliki direktori berisi banyak file HTML, bungkus logika dalam sebuah fungsi dan iterasikan setiap file:

```python
import os
from aspose.html import HTMLDocument

def process_file(input_path: str, output_path: str, base_url: str = None):
    doc = HTMLDocument(input_path)
    for link in doc.query_selector_all("a"):
        if base_url:
            href = link.get_attribute("href")
            if href and not href.startswith("http"):
                link.set_attribute("href", base_url + href.lstrip("/"))
        link.set_attribute("target", "_blank")
    doc.save(output_path)

source_dir = "YOUR_DIRECTORY"
for filename in os.listdir(source_dir):
    if filename.endswith(".html"):
        src = os.path.join(source_dir, filename)
        dst = os.path.join(source_dir, f"{os.path.splitext(filename)[0]}_modified.html")
        process_file(src, dst, base_url="https://example.com/")
```

Pola ini memperluas alur kerja **save modified html** ke sejumlah halaman apa pun sambil secara konsisten **add target blank links** dan **change href target**.

## Output yang diharapkan

Membuka `index_modified.html` di browser harus menampilkan tata letak visual yang sama seperti halaman asli, tetapi setiap hyperlink kini menyertakan:

```html
<a href="https://example.com/about.html" target="_blank">About Us</a>
```

Mengklik tautan membuka tujuan di tab browser baru, mempertahankan halaman pengguna saat ini.

## Kesalahan umum dan cara menghindarinya

| Kesalahan | Penjelasan | Solusi |
|-----------|------------|--------|
| Lisensi Aspose.HTML tidak ada | Pustaka akan melempar error lisensi saat runtime. | Dapatkan file lisensi dan setel `aspose.html.License().set_license("license_path")` sebelum memuat dokumen. |
| URL relatif yang dimulai dengan `//` | Dianggap sebagai URL relatif protokol dan mungkin tidak diubah. | Tambahkan pemeriksaan `href.startswith("//")` dan beri awalan `https:` bila diperlukan. |
| File HTML sangat besar | Memuat file besar dapat mengonsumsi memori yang signifikan. | Gunakan API streaming atau bagi file menjadi fragmen lebih kecil jika memori menjadi bottleneck. |

## Kesimpulan

Anda kini tahu cara **menyimpan HTML yang dimodifikasi** setelah menerapkan **add target blank links**, **change href target**, dan memastikan **open all links newtab** menggunakan Aspose.HTML untuk Python. Solusi lengkap memuat file HTML, memperbarui setiap elemen `<a>`, dan menulis hasilnya ke file baru, menangani kasus tepi seperti atribut `target` yang sudah ada dan URL relatif.

Selanjutnya, Anda dapat menjelajahi:

* Menggunakan selector CSS untuk menargetkan hanya tautan eksternal (`a[href^="http"]`)  
* Menyisipkan JavaScript yang menambahkan `rel="noopener"` untuk keamanan saat membuka tab baru  
* Mengonversi HTML yang dimodifikasi menjadi PDF dengan Aspose.PDF untuk Python  

Silakan sesuaikan kode dengan struktur proyek Anda sendiri dan bereksperimen dengan manipulasi DOM tambahan. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik yang berhubungan erat dan membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to save HTML as PDF with Aspose.HTML for Python](/html/english/python/general/how-to-save-html-as-pdf-with-aspose-html-for-python/)
- [How to save HTML as Markdown with Aspose.HTML for Python](/html/english/python/general/how-to-save-html-as-markdown-with-aspose-html-for-python/)
- [How to Use Aspose – Convert HTML to Markdown and Extract Links](/html/english/python/general/how-to-use-aspose-convert-html-to-markdown-and-extract-links/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
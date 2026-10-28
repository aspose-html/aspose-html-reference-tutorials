---
category: general
date: 2026-08-19
description: Buat opsi penanganan sumber daya di Python dan pelajari cara memuat dokumen
  HTML, bahkan halaman HTML yang besar, dengan Aspose.HTML.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- how to load html document
- load large html page
language: id
lastmod: 2026-08-19
og_description: Buat opsi penanganan sumber daya di Python dan lihat cara memuat dokumen
  HTML, termasuk halaman HTML besar, menggunakan Aspose.HTML.
og_image_alt: Screenshot of Python code that creates resource handling options and
  loads a large HTML page
og_title: Buat opsi penanganan sumber daya dan muat dokumen HTML – Panduan Python
schemas:
- author: Aspose
  dateModified: '2026-08-19'
  description: Create resource handling options in Python and learn how to load an
    HTML document, even a large HTML page, with Aspose.HTML.
  headline: Create resource handling options and load an HTML document in Python
  type: TechArticle
- description: Create resource handling options in Python and learn how to load an
    HTML document, even a large HTML page, with Aspose.HTML.
  name: Create resource handling options and load an HTML document in Python
  steps:
  - name: Verify that the page loaded successfully
    text: 'A quick way to confirm that the document is ready is to print the number
      of child nodes in the root element:'
  - name: 1. Missing resources
    text: 'When a linked CSS or JS file is unavailable, Aspose.HTML silently skips
      it but logs a warning. To capture these warnings, enable logging:'
  - name: 2. Circular references
    text: Even with a depth limit, circular references can cause the parser to waste
      time. If you notice unusually long load times, consider reducing `max_handling_depth`
      to `2` or `1`.
  - name: 3. Very large pages (> 10 MB)
    text: 'For extremely large pages, increase Python’s recursion limit **only if**
      you have verified that the depth is safe:'
  type: HowTo
tags:
- Aspose.HTML
- Python
- HTML processing
title: Buat opsi penanganan sumber daya dan muat dokumen HTML dengan Python
url: /id/python/general/create-resource-handling-options-and-load-an-html-document-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat opsi penanganan sumber daya dan muat dokumen HTML di Python

Jika Anda perlu **membuat opsi penanganan sumber daya** untuk impor HTML, panduan ini menunjukkan cara melakukannya secara tepat. Baik Anda menangani halaman sederhana maupun *halaman HTML besar* yang memuat banyak aset eksternal, langkah‑langkah di bawah ini memungkinkan Anda mengontrol kedalaman, menghindari referensi melingkar, dan menjaga penggunaan memori tetap dapat diprediksi.

Dalam tutorial ini Anda akan belajar **cara memuat file dokumen HTML** dengan Aspose.HTML untuk Python, mengonfigurasi kedalaman penanganan maksimum, dan memverifikasi bahwa halaman dimuat tanpa menghabiskan sumber daya. Pendekatan ini bekerja untuk sumber HTML apa pun, mulai dari file statis sederhana hingga halaman kompleks yang merujuk puluhan skrip, stylesheet, dan gambar.

## Apa yang Anda perlukan

Sebelum memulai, pastikan Anda memiliki:

- Python 3.8 atau yang lebih baru terpasang.
- Paket `aspose-html` (pasang dengan `pip install aspose-html`).
- File HTML lokal (misalnya, `big_page.html`) yang ingin Anda uji.
- Pengetahuan dasar tentang Python dan pemuatan sumber daya HTML.

Prasyarat ini memastikan kode berjalan tanpa perubahan di Windows, macOS, atau Linux.

## Langkah 1: Buat opsi penanganan sumber daya

Langkah pertama adalah **membuat opsi penanganan sumber daya**. Objek ini memberi tahu Aspose.HTML bagaimana memperlakukan sumber daya yang ditautkan (CSS, JS, gambar) saat parsing dokumen.

```python
# Step 1: Import the Aspose.HTML library
from aspose.html import *

# Step 2: Instantiate the options container
# This is where we will configure resource handling behavior.
resource_options = ResourceHandlingOptions()
```

> **Mengapa ini penting:** Tanpa opsi eksplisit, Aspose.HTML akan mengikuti setiap tautan yang ditemuinya, yang dapat menyebabkan rekursi tak terbatas pada halaman yang saling merujuk. Dengan membuat objek opsi, Anda mendapatkan kontrol yang halus atas proses impor.

## Langkah 2: Batasi kedalaman penanganan

Untuk mencegah panggilan jaringan yang tak terkendali, tetapkan kedalaman maksimum. Kedalaman `3` adalah nilai default yang aman untuk kebanyakan situs, memungkinkan halaman utama dan dua tingkat sumber daya bersarang.

```python
# Step 3: Limit the depth to three levels
resource_options.max_handling_depth = 3
```

- **Kedalaman 1** – file HTML itu sendiri.  
- **Kedalaman 2** – sumber daya yang langsung direferensikan oleh HTML (misalnya tag `<link>` atau `<script>`).  
- **Kedalaman 3** – sumber daya yang direferensikan oleh aset tingkat pertama tersebut (misalnya impor CSS di dalam stylesheet).

Menetapkan `max_handling_depth` menghentikan parser setelah tiga lompatan, yang sangat berguna ketika Anda **memuat halaman HTML besar** yang mencakup banyak pustaka pihak ketiga.

## Langkah 3: Muat dokumen HTML (cara memuat dokumen html)

Setelah opsi siap, Anda dapat **memuat dokumen HTML**. Berikan `resource_options` yang telah dikonfigurasi ke konstruktor `HTMLDocument`.

```python
# Step 4: Load the HTML document using the configured options
doc = HTMLDocument(
    "YOUR_DIRECTORY/big_page.html",
    resource_handling_options=resource_options
)
```

> **Penjelasan:** Kelas `HTMLDocument` membaca file, menyelesaikan sumber daya sesuai batas kedalaman, dan membangun DOM yang dapat Anda query atau render. Jika file tidak ada atau jalurnya salah, Aspose.HTML akan mengeluarkan `FileNotFoundError`.

### Verifikasi bahwa halaman berhasil dimuat

Cara cepat untuk memastikan dokumen siap adalah mencetak jumlah node anak pada elemen root:

```python
print(f"Root has {len(doc.root.child_nodes)} child nodes.")
```

Jika output menunjukkan hitungan bukan nol, parser berhasil. Untuk *halaman HTML besar*, Anda mungkin juga ingin memeriksa jumlah sumber daya eksternal yang sebenarnya diunduh:

```python
fetched = doc.resource_handling_options.fetched_resources
print(f"Fetched {len(fetched)} external resources (max depth = {resource_options.max_handling_depth}).")
```

## Menangani kasus tepi dan jebakan umum

### 1. Sumber daya yang hilang

Ketika file CSS atau JS yang ditautkan tidak tersedia, Aspose.HTML secara diam-diam melewatinya tetapi mencatat peringatan. Untuk menangkap peringatan ini, aktifkan logging:

```python
import logging
logging.basicConfig(level=logging.WARNING)
```

### 2. Referensi melingkar

Bahkan dengan batas kedalaman, referensi melingkar dapat membuat parser membuang waktu. Jika Anda memperhatikan waktu muat yang tidak biasa lama, pertimbangkan mengurangi `max_handling_depth` menjadi `2` atau `1`.

### 3. Halaman sangat besar (> 10 MB)

Untuk halaman yang sangat besar, tingkatkan batas rekursi Python **hanya jika** Anda telah memverifikasi bahwa kedalaman aman:

```python
import sys
sys.setrecursionlimit(2000)  # optional, use with caution
```

Namun, pendekatan yang disarankan adalah menjaga kedalaman tetap rendah dan membiarkan opsi menyaring aset yang tidak diperlukan.

## Contoh lengkap yang dapat dijalankan

Berikut adalah skrip lengkap yang dapat Anda salin‑tempel ke dalam file bernama `load_html.py`. Sesuaikan jalur file untuk menunjuk ke file HTML Anda sendiri.

```python
# load_html.py
# Demonstrates how to create resource handling options,
# limit handling depth, and load a large HTML page with Aspose.HTML.

from aspose.html import *
import logging
import sys

# Optional: show warnings about missing resources
logging.basicConfig(level=logging.WARNING)

def main():
    # 1️⃣ Create and configure resource handling options
    resource_options = ResourceHandlingOptions()
    resource_options.max_handling_depth = 3  # limit to three levels

    # 2️⃣ Load the HTML document using the options
    html_path = "YOUR_DIRECTORY/big_page.html"  # <-- replace with your file
    doc = HTMLDocument(html_path, resource_handling_options=resource_options)

    # 3️⃣ Verify the load
    print(f"Root has {len(doc.root.child_nodes)} child nodes.")
    fetched = doc.resource_handling_options.fetched_resources
    print(f"Fetched {len(fetched)} external resources (max depth = {resource_options.max_handling_depth}).")

    # Optional: increase recursion limit for huge documents (use with care)
    # sys.setrecursionlimit(2000)

if __name__ == "__main__":
    main()
```

Menjalankan skrip:

```bash
python load_html.py
```

**Output yang diharapkan** (contoh untuk halaman sedang):

```
Root has 12 child nodes.
Fetched 8 external resources (max depth = 3).
```

Untuk halaman yang benar‑benar besar, angka‑angka akan lebih tinggi, tetapi skrip tetap menghormati batas kedalaman yang Anda tetapkan.

## Praktik terbaik dan langkah selanjutnya

- **Gunakan kembali opsi:** Jika Anda memproses banyak halaman secara batch, buat satu instance `ResourceHandlingOptions` dan gunakan kembali untuk menghindari pembuatan objek yang berulang.
- **Kombinasikan dengan rendering:** Setelah memuat, Anda dapat merender DOM ke PDF, gambar, atau bahkan string HTML yang disanitasi menggunakan `HTMLRenderer` milik Aspose.HTML.
- **Jelajahi opsi lain:** `ResourceHandlingOptions` juga memungkinkan Anda mendefinisikan handler unduhan khusus, mengatur timeout, atau membuat whitelist/blacklist domain. Ini berguna ketika Anda perlu **memuat halaman HTML besar** dari sumber yang tidak terpercaya.

## Kesimpulan

Anda kini tahu cara **membuat opsi penanganan sumber daya**, mengonfigurasi kedalaman yang aman, dan **memuat dokumen HTML**—termasuk *halaman HTML besar*—dengan Aspose.HTML untuk Python. Dengan membatasi kedalaman penanganan, Anda melindungi aplikasi dari permintaan jaringan yang tak terkendali sambil tetap mengambil sumber daya penting untuk rendering yang akurat.

Silakan bereksperimen dengan nilai kedalaman yang berbeda, handler unduhan khusus, atau mengintegrasikan DOM yang dimuat ke dalam pipeline pemrosesan lanjutan seperti pembuatan PDF atau analisis konten. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Render HTML – Complete Guide with Custom Resource Handler](/html/english/net/rendering-html-documents/how-to-render-html-complete-guide-with-custom-resource-handl/)
- [Load HTML Using URL in .NET with Aspose.HTML](/html/english/net/html-document-manipulation/load-html-using-url/)
- [Load HTML Using a Remote Server in .NET with Aspose.HTML](/html/english/net/html-document-manipulation/load-html-using-remote-server/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
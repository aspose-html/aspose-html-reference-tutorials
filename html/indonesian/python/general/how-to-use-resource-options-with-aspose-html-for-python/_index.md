---
category: general
date: 2026-08-09
description: Cara menggunakan opsi penanganan sumber daya di Aspose.HTML untuk Python.
  Pelajari cara mengatur kedalaman penanganan maksimum dan memuat halaman HTML besar
  secara efisien.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use resource
- resource handling options
- max handling depth
- Aspose.HTML for Python
- HTMLDocument loading
language: id
lastmod: 2026-08-09
og_description: Cara menggunakan opsi penanganan sumber daya di Aspose.HTML untuk
  Python. Tutorial ini memandu Anda melalui konfigurasi kedalaman penanganan maksimum
  dan memuat file HTML besar dengan aman.
og_image_alt: Diagram illustrating how to use resource handling options in Aspose.HTML
  for Python
og_title: Cara menggunakan opsi sumber daya dengan Aspose.HTML untuk Python – panduan
  lengkap
schemas:
- author: Aspose
  dateModified: '2026-08-09'
  description: How to use resource handling options in Aspose.HTML for Python. Learn
    to set max handling depth and load large HTML pages efficiently.
  headline: How to use resource options with Aspose.HTML for Python
  type: TechArticle
- description: How to use resource handling options in Aspose.HTML for Python. Learn
    to set max handling depth and load large HTML pages efficiently.
  name: How to use resource options with Aspose.HTML for Python
  steps:
  - name: Import the required classes
    text: '```python from aspose.html import HTMLDocument, ResourceHandlingOptions
      ```'
  - name: Create a `ResourceHandlingOptions` object
    text: '```python # Step 2: Instantiate the options container resource_options
      = ResourceHandlingOptions() ```'
  - name: Set the maximum handling depth
    text: '```python # Step 3: Limit recursion to 5 levels of nested resources resource_options.max_handling_depth
      = 5 ```'
  - name: Load the HTML document with the configured options
    text: '```python # Step 4: Load the document using the options we just configured
      doc = HTMLDocument("YOUR_DIRECTORY/bigpage.html", resource_options) ```'
  - name: Verify that the document loaded correctly
    text: '```python # Step 5: Simple sanity check – print the document title print("Document
      title:", doc.title) ```'
  - name: Optional – handle missing resources gracefully
    text: '```python # Step 6: Attach an event handler to log missing resources def
      on_resource_not_found(sender, args): print(f"Resource not found: {args.resource_url}")'
  - name: Clean up
    text: '```python # Step 7: Release native resources when done doc.dispose() ```'
  - name: Pro tip
    text: When processing many HTML files in a batch, reuse a single `ResourceHandlingOptions`
      instance. Creating it once reduces object‑allocation overhead and guarantees
      consistent settings across all documents.
  type: HowTo
tags:
- Aspose.HTML
- Python
- HTML processing
- resource handling
title: Cara menggunakan opsi sumber daya dengan Aspose.HTML untuk Python
url: /id/python/general/how-to-use-resource-options-with-aspose-html-for-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menggunakan opsi sumber daya dengan Aspose.HTML untuk Python

Jika Anda bertanya‑tanya **bagaimana cara menggunakan opsi** penangan sumber daya dengan Aspose.HTML untuk Python, tutorial ini memberikan solusi lengkap yang siap dijalankan. Anda akan belajar cara mengonfigurasi `ResourceHandlingOptions`, membatasi kedalaman penangan maksimum, dan memuat halaman HTML besar tanpa menghabiskan memori.

Memproses halaman web yang kompleks sering menarik banyak sumber daya bersarang—stylesheet, gambar, skrip, dan iframe. Tanpa batas yang tepat, pemuat dapat melakukan rekursi tak terbatas, yang menyebabkan masalah kinerja atau crash. Pada akhir panduan ini Anda akan dapat:

* Membuat instance `ResourceHandlingOptions`.
* Menetapkan `max_handling_depth` ke nilai yang aman.
* Memuat `HTMLDocument` dengan opsi tersebut.
* Menangani kasus tepi umum seperti sumber daya yang hilang atau bersarang lebih dalam.

Tidak ada alat eksternal yang diperlukan selain pustaka Aspose.HTML untuk Python dan lingkungan Python 3 standar.

## Prasyarat

* Python 3.8 atau lebih baru terpasang.
* Paket Aspose.HTML untuk Python (`aspose-html`) terinstal (`pip install aspose-html`).
* File HTML contoh (misalnya `bigpage.html`) yang berisi sumber daya bersarang.
* Familiaritas dasar dengan sintaks Python dan pemrograman berorientasi objek.

## Cara menggunakan opsi penangan sumber daya – langkah demi langkah

Bagian‑bagian berikut memecah implementasi menjadi langkah‑langkah terpisah yang dapat digunakan kembali. Setiap langkah mencakup **mengapa** kode tersebut penting dan cuplikan kode lengkap yang dapat Anda salin ke proyek Anda.

### Langkah 1: Impor kelas yang diperlukan

```python
from aspose.html import HTMLDocument, ResourceHandlingOptions
```

**Mengapa ini penting:**  
`HTMLDocument` adalah titik masuk untuk memuat dan memanipulasi konten HTML. `ResourceHandlingOptions` memungkinkan Anda mengontrol bagaimana sumber daya eksternal diambil, di‑cache, atau diabaikan. Mengimpornya di bagian atas membuat skrip rapi dan mengikuti praktik terbaik Python.

### Langkah 2: Buat objek `ResourceHandlingOptions`

```python
# Step 2: Instantiate the options container
resource_options = ResourceHandlingOptions()
```

**Mengapa ini penting:**  
Objek opsi berfungsi sebagai kantong konfigurasi. Anda dapat menempelkannya ke konstruktor `HTMLDocument` sehingga setiap permintaan sumber daya menghormati pengaturan yang Anda definisikan.

### Langkah 3: Tetapkan kedalaman penangan maksimum

```python
# Step 3: Limit recursion to 5 levels of nested resources
resource_options.max_handling_depth = 5
```

**Mengapa ini penting:**  
`max_handling_depth` mencegah rekursi tak terbatas ketika sebuah halaman menyematkan sumber daya yang pada gilirannya menyematkan sumber daya lain. Menetapkannya ke **5** adalah nilai default yang aman untuk kebanyakan halaman dunia nyata, namun Anda dapat menyesuaikannya berdasarkan skenario Anda. Jika Anda menetapkan kedalaman ke **0**, pemuat akan melewatkan semua sumber daya eksternal, yang berguna untuk ekstraksi teks murni.

### Langkah 4: Muat dokumen HTML dengan opsi yang telah dikonfigurasi

```python
# Step 4: Load the document using the options we just configured
doc = HTMLDocument("YOUR_DIRECTORY/bigpage.html", resource_options)
```

**Mengapa ini penting:**  
Menyertakan `resource_options` ke konstruktor `HTMLDocument` memberi tahu pustaka untuk menghormati `max_handling_depth` yang Anda tetapkan. Dokumen kini sepenuhnya diparse, dan sumber daya di luar tingkat kelima diabaikan, menjaga penggunaan memori tetap dapat diprediksi.

### Langkah 5: Verifikasi bahwa dokumen berhasil dimuat

```python
# Step 5: Simple sanity check – print the document title
print("Document title:", doc.title)
```

**Mengapa ini penting:**  
Pemeriksaan cepat memastikan bahwa HTML diparse tanpa kesalahan fatal. Jika judul tercetak sebagai `None`, file mungkin tidak ada atau rusak, dan Anda harus menangani pengecualian (lihat bagian “Error handling” di bawah).

### Langkah 6: Opsional – tangani sumber daya yang hilang dengan elegan

```python
# Step 6: Attach an event handler to log missing resources
def on_resource_not_found(sender, args):
    print(f"Resource not found: {args.resource_url}")

resource_options.resource_not_found += on_resource_not_found
```

**Mengapa ini penting:**  
Aspose.HTML memicu event `resource_not_found` ketika aset yang ditautkan tidak dapat diambil. Mencatat kejadian ini membantu Anda mendiagnosis tautan rusak atau memutuskan apakah akan menyediakan fallback.

### Langkah 7: Pembersihan

```python
# Step 7: Release native resources when done
doc.dispose()
```

**Mengapa ini penting:**  
`HTMLDocument` menyimpan sumber daya yang tidak dikelola (misalnya buffer memori native). Membuang objek secara eksplisit membebaskan sumber daya tersebut dengan cepat, yang sangat penting dalam layanan yang berjalan lama atau pekerjaan batch.

## Contoh lengkap yang dapat dijalankan

Berikut adalah skrip lengkap yang menggabungkan semua langkah di atas. Ganti `"YOUR_DIRECTORY/bigpage.html"` dengan jalur aktual ke file HTML Anda.

```python
# ------------------------------------------------------------
# Complete example: how to use resource handling options
# with Aspose.HTML for Python
# ------------------------------------------------------------

from aspose.html import HTMLDocument, ResourceHandlingOptions

# 1️⃣ Create and configure the options
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 5  # stop after 5 levels

# 2️⃣ Optional: log missing resources
def on_resource_not_found(sender, args):
    print(f"[WARN] Missing resource: {args.resource_url}")

resource_options.resource_not_found += on_resource_not_found

# 3️⃣ Load the document using the configured options
doc_path = "YOUR_DIRECTORY/bigpage.html"
doc = HTMLDocument(doc_path, resource_options)

# 4️⃣ Verify load
print("Document title:", doc.title)

# 5️⃣ Perform any additional processing here
#    (e.g., extract text, manipulate DOM, render to PDF, etc.)

# 6️⃣ Clean up
doc.dispose()
```

**Output yang diharapkan (asumsi HTML memiliki tag `<title>`):**

```
Document title: Sample Big Page
```

Jika ada sumber daya yang hilang, Anda akan melihat baris peringatan seperti:

```
[WARN] Missing resource: https://example.com/missing-image.png
```

## Kasus tepi dan tip praktik terbaik

| Situasi | Penanganan yang disarankan |
|-----------|----------------------|
| **Kedalaman yang diperlukan lebih dalam dari 5** | Tingkatkan `max_handling_depth` ke level yang diperlukan, tetapi pantau penggunaan memori dengan profiler. |
| **Referensi sumber daya melingkar** | Batas kedalaman secara otomatis memotong siklus; Anda juga dapat mengatur `resource_options.enable_circular_reference_detection = True` jika versi API mendukungnya. |
| **Sumber daya biner besar (mis., gambar resolusi tinggi)** | Gunakan `resource_options.max_resource_size` untuk membatasi ukuran tiap aset yang diunduh. |
| **Timeout jaringan** | Konfigurasikan `resource_options.request_timeout` (dalam detik) untuk menghindari proses yang menggantung pada server lambat. |
| **Berjalan di lingkungan terbatas (tanpa internet)** | Atur `resource_options.enable_external_resources = False` untuk melewatkan semua pengambilan remote. |

### Pro tip

Saat memproses banyak file HTML secara batch, gunakan kembali satu instance `ResourceHandlingOptions`. Membuatnya sekali mengurangi overhead alokasi objek dan menjamin pengaturan konsisten di semua dokumen.

## Pertanyaan umum

**T: Apakah `max_handling_depth` memengaruhi sumber daya inline (mis., tag `<style>`)?**  
J: Tidak. Sumber daya inline merupakan bagian dari HTML asli dan selalu diproses. Batas kedalaman hanya berlaku untuk sumber daya eksternal yang memerlukan permintaan HTTP tambahan.

**


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik yang berhubungan erat dan membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Menyimpan HTML di C# – Panduan Lengkap Menggunakan Penangan Sumber Daya Kustom](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Cara Menambahkan Penangan dengan Aspose.HTML untuk Java](/html/english/java/message-handling-networking/custom-message-handler/)
- [Penanganan Data dan Manajemen Stream dalam Aspose.HTML untuk Java](/html/english/java/data-handling-stream-management/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
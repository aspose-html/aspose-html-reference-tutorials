---
category: general
date: 2026-06-10
description: Pelajari cara membatasi kedalaman sumber daya HTML menggunakan Aspose.HTML
  untuk Python. Tutorial langkah demi langkah ini mencakup opsi penanganan sumber
  daya, pemangkasan HTML, dan praktik terbaik.
draft: false
keywords:
- limit html resource depth
- Aspose.HTML Python
- resource handling options
- trim HTML document
- max handling depth
language: id
og_description: Batasi kedalaman sumber daya HTML di Python menggunakan Aspose.HTML.
  Ikuti panduan kami untuk mengatur kedalaman penanganan maksimum, memangkas HTML,
  dan menghindari pembengkakan sumber daya.
og_title: Batasi Kedalaman Sumber Daya HTML dengan Aspose.HTML – Tutorial Python Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Learn how to limit HTML resource depth using Aspose.HTML for Python.
    This step‑by‑step tutorial covers resource handling options, trimming HTML, and
    best practices.
  headline: Limit HTML Resource Depth with Aspose.HTML for Python – Complete Guide
  type: TechArticle
- description: Learn how to limit HTML resource depth using Aspose.HTML for Python.
    This step‑by‑step tutorial covers resource handling options, trimming HTML, and
    best practices.
  name: Limit HTML Resource Depth with Aspose.HTML for Python – Complete Guide
  steps:
  - name: Understanding `max_handling_depth`
    text: '- **Depth 0** – Only the primary HTML file is processed; all external assets
      are ignored. - **Depth 1** – The HTML file and any directly linked resources
      (like a stylesheet) are fetched. - **Depth 5** – Allows up to five layers of
      nested references, which is usually enough for most sites without pul'
  - name: Verifying the Result
    text: Open `trimmed_output.html` in a browser and inspect the network panel (F12
      → Network). You should see far fewer requests compared to the original file.
      If you still see a cascade of external calls, revisit **Step 2** and increase
      `max_handling_depth` slightly.
  - name: 1. Skipping Specific Resource Types
    text: 'Sometimes you only care about images, not scripts. You can combine `max_handling_depth`
      with a **resource filter**:'
  - name: 2. Handling Large Documents Efficiently
    text: 'For massive HTML files, enable **asynchronous loading** to keep memory
      usage low:'
  - name: 3. Logging What Gets Skipped
    text: 'If you need to audit which resources were omitted, turn on verbose logging:'
  type: HowTo
tags:
- Aspose
- Python
- HTML processing
title: Batasi Kedalaman Sumber Daya HTML dengan Aspose.HTML untuk Python – Panduan
  Lengkap
url: /id/python/general/limit-html-resource-depth-with-aspose-html-for-python-comple/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Batasi Kedalaman Sumber Daya HTML dengan Aspose.HTML untuk Python – Panduan Lengkap

Pernah bertanya-tanya bagaimana cara **membatasi kedalaman sumber daya HTML** saat mengonversi atau memproses halaman web di Python? Anda tidak sendirian. Banyak pengembang mengalami kendala ketika aset eksternal seperti gambar, skrip, atau gaya menurun jauh melampaui apa yang sebenarnya mereka butuhkan, menyebabkan proses build lebih lambat dan output yang bengkak.  

Dalam tutorial ini kami akan memandu Anda langkah demi langkah untuk mengatur **max handling depth**, menggunakan **resource handling options**, dan akhirnya **memangkas dokumen HTML** sehingga Anda hanya menyimpan apa yang penting. Pada akhir tutorial Anda akan memiliki file HTML yang bersih dan ringan, siap untuk diproses lebih lanjut atau dikonversi ke PDF.

> **Apa yang akan Anda dapatkan:** sebuah skrip yang dapat dijalankan, penjelasan mengapa setiap pengaturan penting, tips untuk kasus tepi, dan daftar periksa verifikasi cepat.

---

## Prerequisites

Sebelum kita mulai, pastikan Anda memiliki:

- Python 3.8+ terinstal (rilisan stabil terbaru paling baik).
- Lisensi Aspose.HTML untuk Python yang aktif (atau percobaan gratis).  
- Familiaritas dasar dengan impor Python dan jalur file.
- File HTML input yang ingin Anda pangkas, berada di direktori yang diketahui.

Jika ada yang belum familiar, jeda sejenak dan dapatkan paket resmi Aspose.HTML untuk Python:

```bash
pip install aspose-html
```

---

## Step 1: Import Aspose.HTML Classes and Load Your Document

Hal pertama yang perlu Anda lakukan adalah membawa kelas yang diperlukan ke dalam ruang lingkup dan mengarahkan Aspose.HTML ke file yang ingin Anda proses.

```python
from aspose.html import HTMLDocument, ResourceHandlingOptions

# Load the source HTML file – adjust the path to your environment
document = HTMLDocument("YOUR_DIRECTORY/input.html")
```

**Mengapa ini penting:** `HTMLDocument` adalah objek inti yang mewakili seluruh halaman HTML, termasuk DOM dan sumber daya yang terhubung. Memuat file lebih awal memberi Aspose.HTML kesempatan untuk menganalisis setiap tag `<link>`, `<script>`, dan `<img>` sebelum kita mulai memangkas.

> **Pro tip:** Gunakan jalur absolut saat debugging; jalur relatif kadang dapat terpecahkan secara tidak terduga pada sistem operasi yang berbeda.

---

## Step 2: Configure Resource Handling Options – Set Max Handling Depth

Sekarang kita memberi tahu Aspose.HTML seberapa dalam ia harus mengikuti sumber daya yang ditautkan. **max handling depth** menentukan berapa banyak tingkat referensi bersarang (misalnya, file CSS yang mengimpor file CSS lain) yang akan dikejar oleh perpustakaan.

```python
# Create a new ResourceHandlingOptions instance
handling_options = ResourceHandlingOptions()

# Limit the depth to 5 levels – this is the key to limiting HTML resource depth
handling_options.max_handling_depth = 5
```

### Memahami `max_handling_depth`

- **Depth 0** – Hanya file HTML utama yang diproses; semua aset eksternal diabaikan.
- **Depth 1** – File HTML dan semua sumber daya yang ditautkan secara langsung (seperti stylesheet) diambil.
- **Depth 5** – Mengizinkan hingga lima lapisan referensi bersarang, yang biasanya cukup untuk kebanyakan situs tanpa menarik skrip pihak ketiga yang tak berujung.

Sesuaikan angka ini berdasarkan kompleksitas halaman sumber Anda. Jika Anda melihat gambar yang hilang atau gaya yang rusak, naikkan kedalaman satu tingkat dan jalankan kembali.

---

## Step 3: Apply the Options to the Document

Dengan opsi yang telah dikonfigurasi, kami mengikatnya ke `HTMLDocument`. Langkah ini mengaktifkan batas kedalaman untuk operasi penyimpanan yang akan datang.

```python
# Attach the handling options to the document
document.resource_handling_options = handling_options
```

**Apa yang terjadi di balik layar?** Aspose.HTML kini tahu untuk berhenti merayapi sumber daya setelah mencapai tingkat kelima. Apa pun di luar itu diabaikan, secara efektif **membatasi kedalaman sumber daya HTML** dan menjaga output tetap rapi.

---

## Step 4: Save the Trimmed Document

Akhirnya, tulis HTML yang telah diproses kembali ke disk. Output akan berisi hanya sumber daya yang berada dalam batas kedalaman.

```python
# Save the trimmed HTML to a new file
document.save("YOUR_DIRECTORY/trimmed_output.html")
```

### Memverifikasi Hasil

Buka `trimmed_output.html` di browser dan periksa panel jaringan (F12 → Network). Anda seharusnya melihat jauh lebih sedikit permintaan dibandingkan file asli. Jika masih terlihat rangkaian panggilan eksternal, tinjau kembali **Step 2** dan tingkatkan `max_handling_depth` sedikit.

---

## Bonus: Advanced Scenarios and Edge Cases

### 1. Skipping Specific Resource Types

Kadang Anda hanya peduli pada gambar, bukan skrip. Anda dapat menggabungkan `max_handling_depth` dengan **resource filter**:

```python
from aspose.html import ResourceType

handling_options.resource_filter = lambda r: r.resource_type != ResourceType.SCRIPT
```

Lambda ini memberi tahu Aspose.HTML untuk mengabaikan semua sumber daya skrip terlepas dari kedalaman.

### 2. Handling Large Documents Efficiently

Untuk file HTML yang sangat besar, aktifkan **asynchronous loading** agar penggunaan memori tetap rendah:

```python
handling_options.is_async = True
document.resource_handling_options = handling_options
```

Mode asinkron men-stream sumber daya, yang berguna saat memproses ratusan halaman dalam pekerjaan batch.

### 3. Logging What Gets Skipped

Jika Anda perlu mengaudit sumber daya mana yang diabaikan, aktifkan logging verbos:

```python
handling_options.logging_enabled = True
handling_options.log_file_path = "YOUR_DIRECTORY/resource_log.txt"
```

Log akan mencantumkan setiap sumber daya yang dipertimbangkan Aspose.HTML dan apakah ia disimpan atau dibuang karena batas kedalaman.

---

## Full Working Example

Berikut adalah skrip lengkap yang dapat Anda salin‑tempel dan jalankan segera (cukup ganti `YOUR_DIRECTORY` dengan jalur aktual Anda).

```python
from aspose.html import HTMLDocument, ResourceHandlingOptions, ResourceType

# 1️⃣ Load the HTML document
document = HTMLDocument("YOUR_DIRECTORY/input.html")

# 2️⃣ Set up resource handling – limit depth to 5 levels
handling_options = ResourceHandlingOptions()
handling_options.max_handling_depth = 5

# Optional: skip scripts and enable logging
handling_options.resource_filter = lambda r: r.resource_type != ResourceType.SCRIPT
handling_options.logging_enabled = True
handling_options.log_file_path = "YOUR_DIRECTORY/resource_log.txt"

# 3️⃣ Apply the options
document.resource_handling_options = handling_options

# 4️⃣ Save the trimmed output
document.save("YOUR_DIRECTORY/trimmed_output.html")
```

**Output yang diharapkan:** File baru `trimmed_output.html` yang berisi markup asli ditambah hanya sumber daya eksternal yang berada dalam lima tingkat bersarang dan bukan skrip (berkat filter). File log akan mencantumkan setiap sumber daya yang dilewati.

---

## Common Pitfalls & How to Avoid Them

| Masalah | Mengapa Terjadi | Solusi |
|---------|-----------------|--------|
| Gambar hilang setelah pemangkasan | `max_handling_depth` terlalu rendah, menyebabkan impor CSS bersarang yang mengabaikan gambar. | Tingkatkan `max_handling_depth` menjadi 6 atau 7, lalu jalankan kembali. |
| Kesalahan JavaScript pada halaman yang dipangkas | Skrip tersaring secara tidak sengaja. | Hapus atau sesuaikan `resource_filter` untuk mengizinkan `ResourceType.SCRIPT`. |
| Kegagalan memori pada halaman besar | Penanganan asinkron tidak diaktifkan. | Setel `handling_options.is_async = True`. |
| File log tidak dibuat | Logging dinonaktifkan atau jalur tidak valid. | Pastikan `logging_enabled = True` dan direktori ada. |

---

## Conclusion

Kami telah membahas semua yang Anda perlukan untuk **membatasi kedalaman sumber daya HTML** menggunakan Aspose.HTML untuk Python. Dengan mengonfigurasi `ResourceHandlingOptions.max_handling_depth`, secara opsional memfilter tipe sumber daya, dan menyimpan dokumen yang dipangkas, Anda mendapatkan kontrol presisi atas berapa banyak konten eksternal yang masuk ke alur kerja HTML Anda.  

Sekarang Anda dapat mengintegrasikan skrip ini ke dalam pipeline yang lebih besar—baik Anda menghasilkan PDF, mengarsipkan halaman web, atau sekadar membersihkan markup sebelum menyajikannya ke klien.  

**Langkah selanjutnya:** bereksperimen dengan nilai kedalaman yang berbeda, coba menggabungkan batas kedalaman dengan **konversi PDF Aspose.HTML** untuk menghasilkan PDF yang ringan, atau jelajahi **resource filter** lebih jauh untuk hanya menyimpan gambar atau stylesheet. Kemungkinannya tak terbatas, dan peningkatan performa seringkali langsung terasa.

Selamat coding, dan jangan ragu meninggalkan komentar jika Anda menemui kendala!

## What Should You Learn Next?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Penanganan Pesan dan Jaringan di Aspose.HTML untuk Java](/html/english/java/message-handling-networking/)
- [Penanganan Data dan Manajemen Stream di Aspose.HTML untuk Java](/html/english/java/data-handling-stream-management/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
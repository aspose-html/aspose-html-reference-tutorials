---
category: general
date: 2026-07-02
description: Cara membatasi sumber daya saat memuat halaman HTML besar dengan Aspose.HTML
  di Python – atur kedalaman dan hindari kelebihan beban.
draft: false
keywords:
- how to limit resources
- how to set depth
- load large html page
language: id
og_description: Cara membatasi sumber daya saat memuat halaman HTML besar dengan Aspose.HTML
  di Python – pelajari cara mengatur kedalaman dan menjaga penggunaan memori tetap
  rendah.
og_title: Cara Membatasi Sumber Daya di Aspose.HTML Python
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: How to limit resources when loading a large HTML page with Aspose.HTML
    in Python – set depth and avoid overload.
  headline: How to Limit Resources in Aspose.HTML Python
  type: TechArticle
- description: How to limit resources when loading a large HTML page with Aspose.HTML
    in Python – set depth and avoid overload.
  name: How to Limit Resources in Aspose.HTML Python
  steps:
  - name: Why This Works
    text: 1. **Importing the right classes** – `ResourceHandlingOptions` holds the
      settings, while `HTMLDocument` does the heavy lifting of parsing the HTML. 2.
      **Setting `max_handling_depth`** – This is the exact answer to **how to set
      depth**. A depth of `3` means Aspose.HTML will follow links, scripts, and
  - name: Expected Output
    text: 'Running the script should print something like:'
  - name: Edge Cases & Gotchas
    text: '- **Circular references:** If a page includes itself indirectly (A → B
      → A), the depth limit prevents infinite loops. The loader will stop at the configured
      depth and log a warning. - **Dynamic scripts:** Some JavaScript injects resources
      after the initial load. `max_handling_depth` only affects sta'
  type: HowTo
- questions:
  - answer: Just bump `max_handling_depth` for that run. You can even compute it dynamically
      based on the page size.
    question: What if I need a deeper crawl for a specific page?
  - answer: Yes. After loading, `doc.resources` contains only the resources that were
      actually fetched. Anything missing simply isn’t in the collection.
    question: Can I retrieve a list of skipped resources?
  - answer: The `ResourceHandlingOptions` instance is immutable once passed to `HTMLDocument`,
      so you can safely reuse it across threads.
    question: Is the depth limit thread‑safe?
  type: FAQPage
tags:
- Aspose.HTML
- Python
- Resource Management
title: Cara Membatasi Sumber Daya di Aspose.HTML Python
url: /id/python/general/how-to-limit-resources-in-aspose-html-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Membatasi Sumber Daya di Aspose.HTML Python

Pernah bertanya-tanya **bagaimana cara membatasi sumber daya** saat memuat file HTML raksasa? Anda tidak sendirian. Ketika sebuah halaman menampung puluhan gambar, skrip, dan stylesheet, loader default dapat menghabiskan memori lebih cepat daripada anak kecil yang makan permen. Kabar baiknya? Aspose.HTML memberi Anda kontrol yang sangat detail, dan panduan ini menunjukkan **bagaimana cara membatasi sumber daya** langkah demi langkah.

Kami juga akan membahas **bagaimana cara mengatur kedalaman** untuk penanganan sumber daya dan mendemonstrasikan cara paling aman untuk **memuat halaman html besar** tanpa membuat proses Python Anda meluap. Pada akhir tutorial, Anda akan memiliki skrip siap‑jalankan yang menghormati batas kedalaman tiga level dan menjaga aplikasi Anda tetap responsif.

## Prerequisites

Sebelum kita mulai, pastikan Anda memiliki:

- Python 3.8 atau yang lebih baru (perpustakaan mendukung semua versi terbaru).
- Lisensi aktif Aspose.HTML untuk Python atau kunci evaluasi gratis.
- Paket `aspose-html` terpasang:

```bash
pip install aspose-html
```

Jika Anda menggunakan lingkungan virtual (sangat disarankan), aktifkan terlebih dahulu—tidak ada masalah.

## How to Limit Resources When Loading Large HTML Pages

Inti dari **bagaimana cara membatasi sumber daya** terletak pada kelas `ResourceHandlingOptions`. Anggaplah ini sebagai petugas lalu lintas yang memberi tahu Aspose.HTML kapan harus mengatakan “stop” pada sumber daya yang bersarang lebih jauh. Di bawah ini contoh lengkap yang dapat dijalankan yang mengikuti langkah‑langkah tepat yang Anda perlukan.

```python
# Step 1: Import the required Aspose.HTML classes
from aspose.html import ResourceHandlingOptions, HTMLDocument

# Step 2: Create a ResourceHandlingOptions instance and limit the handling depth
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # Stop after 3 levels of nested resources

# Step 3: Load the HTML document using the configured resource options
# Replace 'YOUR_DIRECTORY/big_page.html' with the actual path to your file
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)

# Optional: Verify that the document loaded without exhausting memory
print(f"Document title: {doc.title}")
print(f"Number of pages: {len(doc.pages)}")
```

### Why This Works

1. **Mengimpor kelas yang tepat** – `ResourceHandlingOptions` menyimpan pengaturan, sementara `HTMLDocument` melakukan pekerjaan berat dalam parsing HTML.
2. **Mengatur `max_handling_depth`** – Ini adalah jawaban tepat untuk **bagaimana cara mengatur kedalaman**. Kedalaman `3` berarti Aspose.HTML akan mengikuti tautan, skrip, dan gambar hanya hingga tiga level. Apa pun yang lebih dalam akan diabaikan, secara dramatis mengurangi penggunaan memori.
3. **Menyampaikan opsi ke konstruktor** – Konstruktor `HTMLDocument` menerima argumen kedua, sehingga Anda tidak perlu panggilan terpisah untuk menerapkan pengaturan. Ini bersih, ringkas, dan mengurangi kemungkinan lupa mengaktifkan batas.

### Expected Output

Menjalankan skrip seharusnya mencetak sesuatu seperti berikut:

```
Document title: Massive Report
Number of pages: 1
```

Jika file HTML berisi lebih dari tiga lapisan sumber daya yang ditautkan, aset yang lebih dalam tersebut tidak akan diambil. Tidak ada error yang dilempar; loader hanya melewatinya.

## How to Set Depth for Resource Handling

Setelah Anda melihat contoh dasar, mari jelajahi **bagaimana cara mengatur kedalaman** untuk berbagai skenario.

| Kedalaman yang Diinginkan | Kasus Penggunaan                                          | Pengaturan yang Disarankan                                 |
|---------------------------|-----------------------------------------------------------|------------------------------------------------------------|
| `1`                       | Hanya file HTML utama, abaikan semua aset eksternal       | `resource_options.max_handling_depth = 1`                 |
| `2`                       | Muat gambar dan CSS tetapi lewati skrip bersarang         | `resource_options.max_handling_depth = 2`                 |
| `3` (default)             | Pendekatan seimbang untuk kebanyakan halaman besar        | `resource_options.max_handling_depth = 3`                 |
| `0`                       | Nonaktifkan pemuatan sumber daya eksternal sepenuhnya     | `resource_options.max_handling_depth = 0`                 |

> **Tips profesional:** Mulailah dengan `3` dan turunkan nilai hanya jika Anda melihat proses masih memakan banyak RAM. Semakin rendah kedalaman, semakin sedikit panggilan jaringan yang Anda lakukan, yang juga mempercepat pemuatan.

### Edge Cases & Gotchas

- **Referensi melingkar:** Jika sebuah halaman menyertakan dirinya secara tidak langsung (A → B → A), batas kedalaman mencegah loop tak berujung. Loader akan berhenti pada kedalaman yang dikonfigurasi dan mencatat peringatan.
- **Skrip dinamis:** Beberapa JavaScript menyuntikkan sumber daya setelah pemuatan awal. `max_handling_depth` hanya memengaruhi referensi statis; untuk konten dinamis Anda perlu mengeksekusi skrip di browser tanpa kepala atau secara manual mengambil aset tambahan.
- **File yang hilang:** Ketika sumber daya pada kedalaman yang diizinkan tidak ada, Aspose.HTML secara diam-diam melewatinya. Anda dapat mengaktifkan logging melalui `aspose.html.logging` jika memerlukan visibilitas lebih.

## Load Large HTML Page Efficiently

Ketika tujuan adalah **memuat halaman html besar** tanpa membebani server Anda, gabungkan batas kedalaman dengan beberapa trik tambahan:

1. **Streaming file** – Jika halaman berada di disk, buka dengan aliran berbuffer untuk mengurangi lonjakan memori.
2. **Nonaktifkan JavaScript** – Jika Anda tidak memerlukan eksekusi skrip, matikan:

```python
from aspose.html import HtmlLoadOptions
load_options = HtmlLoadOptions()
load_options.enable_javascript = False
doc = HTMLDocument("big_page.html", resource_options, load_options)
```

3. **Gunakan folder sementara untuk sumber daya** – Arahkan Aspose.HTML ke folder sandbox sehingga aset yang diunduh tidak mencemari direktori proyek Anda.

```python
resource_options.resource_folder = "temp_resources"
```

Menggabungkan semuanya:

```python
from aspose.html import ResourceHandlingOptions, HTMLDocument, HtmlLoadOptions

# Configure depth limit
resource_opts = ResourceHandlingOptions()
resource_opts.max_handling_depth = 3
resource_opts.resource_folder = "temp_resources"

# Disable JavaScript for faster parsing
load_opts = HtmlLoadOptions()
load_opts.enable_javascript = False

# Load the massive HTML file
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_opts, load_opts)

print(f"Title: {doc.title}")
print(f"Loaded pages: {len(doc.pages)}")
```

Menjalankan skrip ini pada file HTML berukuran 200 MB dengan ratusan aset yang ditautkan biasanya selesai dalam kurang dari satu menit pada laptop standar—jauh lebih baik dibandingkan loader default yang tidak terbatas.

## Common Questions (and Their Answers)

- **Bagaimana jika saya membutuhkan perayapan lebih dalam untuk halaman tertentu?**  
  Tingkatkan saja `max_handling_depth` untuk eksekusi itu. Anda bahkan dapat menghitungnya secara dinamis berdasarkan ukuran halaman.

- **Apakah saya dapat mengambil daftar sumber daya yang dilewati?**  
  Ya. Setelah pemuatan, `doc.resources` hanya berisi sumber daya yang benar‑benar diambil. Apa pun yang hilang tidak ada dalam koleksi.

- **Apakah batas kedalaman thread‑safe?**  
  Instance `ResourceHandlingOptions` menjadi tidak dapat diubah setelah diteruskan ke `HTMLDocument`, sehingga Anda dapat menggunakannya kembali secara aman di antara thread.

## Recap

Dalam tutorial ini kami membahas **bagaimana cara membatasi sumber daya** saat menggunakan Aspose.HTML untuk Python, menjelaskan **bagaimana cara mengatur kedalaman** untuk mengontrol pemuatan aset bersarang, dan mendemonstrasikan cara paling aman untuk **memuat halaman html besar** tanpa menghabiskan memori. Dengan mengonfigurasi `ResourceHandlingOptions` dan, secara opsional, `HtmlLoadOptions`, Anda memperoleh kontrol yang tepat atas proses pemuatan, membuat aplikasi Anda lebih cepat dan lebih handal.

## What’s Next?

- [Cara Mengatur Timeout – Mengelola Timeout Jaringan di Aspose.HTML untuk Java](/html/english/java/message-handling-networking/network-timeout/)
- [Cara Mengatur Timeout di Layanan Runtime Aspose.HTML untuk Java](/html/english/java/configuring-environment/configure-runtime-service/)
- [Cara Mengatur Charset di Aspose.HTML untuk Java](/html/english/java/configuring-environment/set-character-set/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
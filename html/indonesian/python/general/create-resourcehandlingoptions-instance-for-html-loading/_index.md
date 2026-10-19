---
category: general
date: 2026-05-31
description: Buat instance ResourceHandlingOptions untuk mengontrol pemuatan sumber
  daya HTML. Pelajari cara membatasi kedalaman sumber daya dan memuat HTMLDocument
  dengan opsi khusus.
draft: false
keywords:
- create resourcehandlingoptions instance
- limit resource depth
- HTMLDocument options
- resource loading configuration
- python html parsing
language: id
og_description: Buat instance ResourceHandlingOptions untuk mengontrol pemuatan sumber
  daya HTML. Panduan ini menunjukkan cara mengatur kedalaman penanganan maksimum dan
  memuat HTMLDocument dengan opsi khusus.
og_title: Buat Instance ResourceHandlingOptions untuk Memuat HTML
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create ResourceHandlingOptions instance to control HTML resource loading.
    Learn how to limit resource depth and load an HTMLDocument with custom options.
  headline: Create ResourceHandlingOptions Instance for HTML Loading
  type: TechArticle
tags:
- Python
- HTML parsing
- Resource handling
title: Buat Instance ResourceHandlingOptions untuk Memuat HTML
url: /id/python/general/create-resourcehandlingoptions-instance-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Instance ResourceHandlingOptions untuk Memuat HTML

Pernah bertanya-tanya bagaimana **membuat instance ResourceHandlingOptions** sehingga Anda dapat mencegah halaman HTML raksasa membuat parser Anda meledak? Anda tidak sendirian—dokumen besar dengan skrip bersarang, frame, atau include dapat dengan cepat mengubah proses scraping sederhana menjadi mimpi buruk.  

Dalam tutorial ini kami akan memandu Anda langkah demi langkah untuk membuat objek `ResourceHandlingOptions`, membatasi tingkat kedalaman nesting, dan memasukkannya ke dalam `HTMLDocument`. Pada akhir tutorial Anda akan memiliki pola bersih dan dapat diulang untuk **konfigurasi pemuatan sumber daya** yang bekerja dengan file HTML berukuran apa pun.

## Apa yang Akan Anda Pelajari

- Mengapa instance `ResourceHandlingOptions` penting saat mem-parsing halaman yang sangat besar.  
- Cara **membatasi kedalaman sumber daya** untuk menghindari rekursi tak berujung.  
- Sintaks tepat untuk memuat `HTMLDocument` dengan opsi khusus Anda.  
- Contoh lengkap yang dapat dijalankan dan langsung Anda gunakan dalam proyek hari ini.  

**Prasyarat:** Python 3.8+, pustaka `htmlparser` yang menyediakan `HTMLDocument` dan `ResourceHandlingOptions`. Tidak ada dependensi lain yang diperlukan.

---

## Langkah 1: Buat Instance ResourceHandlingOptions

Hal pertama yang Anda perlukan adalah objek `ResourceHandlingOptions` baru. Anggap saja ini sebagai panel kontrol untuk setiap sumber daya eksternal yang mungkin ditemui parser—skrip, gambar, iframe, apa saja.

```python
# Step 1: Initialize the options object
options = ResourceHandlingOptions()
```

> **Mengapa ini penting:** Tanpa instance yang eksplisit, parser akan kembali ke nilai defaultnya, yang sering berarti “muat semuanya”. Untuk halaman raksasa, default tersebut dapat mengonsumsi gigabyte memori dan membuat skrip Anda terhenti.

---

## Langkah 2: Batasi Kedalaman Sumber Daya

Selanjutnya, kita memberi tahu opsi seberapa dalam kita bersedia menelusuri. Menetapkan `max_handling_depth` ke 5, misalnya, menghentikan parser setelah lima tingkat sumber daya bersarang. Sesuaikan angka tersebut dengan kebutuhan Anda.

```python
# Step 2: Cap the nesting depth (e.g., stop after 5 levels)
options.max_handling_depth = 5
```

> **Tip pro:** Jika Anda hanya tertarik pada konten tingkat atas, kedalaman 1 atau 2 biasanya sudah cukup dan mempercepat proses secara signifikan.

---

## Langkah 3: Muat Dokumen HTML dengan Opsi

Sekarang kita serahkan `options` yang telah dikonfigurasi ke `HTMLDocument`. Konstruktor menerima jalur file (atau URL) dan objek opsi, memberi Anda kontrol detail atas apa yang dimuat.

```python
# Step 3: Parse the HTML file using the configured options
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", options)
```

> **Apa yang akan Anda lihat:** Parser akan membaca `big_page.html`, tetapi setiap sumber daya yang akan menyebabkan kedalaman melebihi 5 akan diabaikan secara diam‑diam. Ini mencegah rekursi tak terkendali dan menjaga penggunaan memori tetap dapat diprediksi.

---

## Langkah 4: Verifikasi Hasil (Opsional tapi Membantu)

Kebiasaan yang baik adalah memeriksa bahwa dokumen telah dimuat sesuai harapan. Di bawah ini ada pemeriksaan cepat yang mencetak jumlah sumber daya yang berhasil ditangani.

```python
# Step 4: Quick verification
print(f"Handled resources: {len(doc.resources)}")
print(f"Document title: {doc.title}")
```

**Output yang diharapkan** (angka Anda akan berbeda tergantung file input):

```
Handled resources: 12
Document title: Example Large Page
```

Jika hitungannya jauh lebih rendah dari yang Anda perkirakan, Anda mungkin perlu meningkatkan `max_handling_depth` atau menyesuaikan properti `ResourceHandlingOptions` lainnya.

---

## Variasi Umum & Kasus Edge

| Situasi | Penyesuaian |
|-----------|------------|
| **Anda perlu mengabaikan hanya gambar** | Setel `options.ignore_images = True`. |
| **Skrip menyebabkan timeout** | Gunakan `options.max_script_execution_time = 2` (detik). |
| **Mem-parsing URL remote alih-alih file** | Berikan string URL ke `HTMLDocument` seperti memberikan jalur file. |
| **Anda menginginkan logger khusus** | Tetapkan `options.logger = my_logger` sebelum memuat. |

Penyesuaian ini semua merupakan bagian dari **toolkit opsi HTMLDocument** dan memungkinkan Anda menyetel **konfigurasi pemuatan sumber daya** tanpa menulis ulang parser Anda.

---

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut skrip mandiri yang dapat Anda jalankan sekarang. Simpan sebagai `parse_big_page.py` dan eksekusi dengan `python parse_big_page.py`.

```python
# parse_big_page.py
from htmlparser import HTMLDocument, ResourceHandlingOptions

def main():
    # 1️⃣ Create the options instance
    options = ResourceHandlingOptions()
    
    # 2️⃣ Limit how deep we go into nested resources
    options.max_handling_depth = 5
    
    # Optional: ignore images to speed things up
    # options.ignore_images = True
    
    # 3️⃣ Load the document with our custom options
    doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", options)
    
    # 4️⃣ Verify the load
    print(f"Handled resources: {len(doc.resources)}")
    print(f"Document title: {doc.title}")

if __name__ == "__main__":
    main()
```

Jalankan skrip tersebut dan Anda akan melihat jumlah sumber daya serta judul yang dicetak, mengonfirmasi bahwa Anda telah berhasil **membuat instance ResourceHandlingOptions** dan menerapkannya.

---

## Kesimpulan

Kami baru saja menunjukkan cara **membuat instance ResourceHandlingOptions**, membatasi tingkat nesting, dan memasukkannya ke dalam `HTMLDocument`. Pola ini memberikan Anda **konfigurasi pemuatan sumber daya** yang andal untuk file HTML besar apa pun, menjaga parsing HTML Python Anda tetap cepat dan ramah memori.

Siap untuk langkah berikutnya? Coba ubah batas kedalaman, aktifkan atau nonaktifkan `ignore_images`, atau integrasikan logger khusus—setiap penyesuaian akan mengajarkan Anda lebih banyak tentang **opsi HTMLDocument** dan cara mereka berinteraksi dengan pipeline data Anda.  

Jika Anda merasa panduan ini berguna, silakan bagikan, beri bintang pada repo, atau tinggalkan komentar dengan tips Anda sendiri. Selamat mem-parsing!

## Apa yang Harus Anda Pelajari Selanjutnya?

- [Create HTML from String in C# – Custom Resource Handler Guide](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Create Stream Provider in .NET with Aspose.HTML](/html/english/net/advanced-features/create-stream-provider/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
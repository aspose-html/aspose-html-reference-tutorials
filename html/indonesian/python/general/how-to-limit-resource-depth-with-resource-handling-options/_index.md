---
category: general
date: 2026-10-25
description: Pelajari cara membatasi kedalaman sumber daya dan menerapkan penanganan
  sumber daya saat menyimpan file HTML besar menggunakan Python. Ikuti panduan langkah
  demi langkah ini untuk hasil yang dapat diandalkan.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- limit resource depth
- apply resource handling
- HTML document processing
- save options Python
- resource handling options
language: id
lastmod: 2026-10-25
og_description: Batasi kedalaman sumber daya dan terapkan penanganan sumber daya saat
  menyimpan HTML dengan Python. Tutorial ini menunjukkan solusi lengkap yang dapat
  dijalankan.
og_image_alt: Screenshot illustrating limit resource depth in a Python script
og_title: Batasi kedalaman sumber daya saat menerapkan penanganan sumber daya – Panduan
  Python
schemas:
- author: GroupDocs
  dateModified: '2026-10-25'
  description: Learn how to limit resource depth and apply resource handling when
    saving large HTML files using Python. Follow this step‑by‑step guide for reliable
    results.
  headline: How to limit resource depth with resource handling options
  type: TechArticle
- description: Learn how to limit resource depth and apply resource handling when
    saving large HTML files using Python. Follow this step‑by‑step guide for reliable
    results.
  name: How to limit resource depth with resource handling options
  steps:
  - name: '**Dynamic content loaded via JavaScript** – The parser only sees static
      HTML. If your page relies on scripts that inject further resources, those will
      never be counted toward the depth limit. Consider pre‑rendering the page with
      a headless browser before applying the limit.'
    text: '**Dynamic content loaded via JavaScript** – The parser only sees static
      HTML. If your page relies on scripts that inject further resources, those will
      never be counted toward the depth limit. Consider pre‑rendering the page with
      a headless browser before applying the limit.'
  - name: '**Circular references** – Some pages include iframes that point back to
      the same page. The depth counter prevents infinite loops, but you may still
      see partially rendered sections. Adjust `max_handling_depth` or manually exclude
      problematic frames.'
    text: '**Circular references** – Some pages include iframes that point back to
      the same page. The depth counter prevents infinite loops, but you may still
      see partially rendered sections. Adjust `max_handling_depth` or manually exclude
      problematic frames.'
  - name: '**Mixed protocols (http/https)** – If resources use different schemes,
      the library may treat them as separate domains. The depth limit still applies
      across protocols, but network permissions might differ. Ensure your environment
      permits both.'
    text: '**Mixed protocols (http/https)** – If resources use different schemes,
      the library may treat them as separate domains. The depth limit still applies
      across protocols, but network permissions might differ. Ensure your environment
      permits both.'
  type: HowTo
tags:
- Python
- HTML
- File handling
title: Cara membatasi kedalaman sumber daya dengan opsi penanganan sumber daya
url: /id/python/general/how-to-limit-resource-depth-with-resource-handling-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membatasi kedalaman sumber daya dengan opsi penanganan sumber daya

Jika Anda perlu **membatasi kedalaman sumber daya** saat memproses file HTML yang sangat besar, panduan ini menunjukkan secara tepat cara melakukannya. Pada akhir tutorial Anda juga akan mengetahui cara **menerapkan penanganan sumber daya** sehingga operasi penyimpanan menghormati batas kedalaman dan menghindari pemrosesan yang tidak terkendali.

Halaman HTML besar sering menyematkan banyak sumber daya eksternal—gambar, skrip, stylesheet, dan iframe bersarang. Tanpa batas kedalaman, parser dapat mengikuti setiap tautan, secara dramatis meningkatkan penggunaan memori dan waktu pemrosesan. Teknik yang dijelaskan di sini menjaga operasi tetap cepat dan dapat diprediksi.

## Prasyarat

* Python 3.9+ terinstal.
* `groupdocs-viewer` (atau perpustakaan pemrosesan HTML serupa) tersedia melalui `pip install groupdocs-viewer`.
* File HTML contoh (`big_page.html`) berada di direktori yang diketahui.
* Izin menulis ke direktori output.

Item-item ini memastikan kode berjalan tanpa konfigurasi tambahan.

## Langkah 1: Muat dokumen HTML sumber

Langkah pertama adalah membuat instance `HTMLDocument` yang menunjuk ke file asli. Objek ini mewakili seluruh struktur HTML dan memberi Anda akses ke opsi penyimpanan nanti.

```python
# Step 1: Load the source HTML document
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html")
```

*Mengapa ini penting*: Memuat file sekali memberi perpustakaan satu titik masuk untuk semua operasi selanjutnya. Ini juga memvalidasi bahwa file ada, mengeluarkan error lebih awal jika path salah.

## Langkah 2: Buat opsi penanganan sumber daya dan batasi kedalaman pemrosesan

`ResourceHandlingOptions` memungkinkan Anda mengontrol seberapa dalam perpustakaan akan menelusuri sumber daya yang ditautkan. Menetapkan `max_handling_depth` ke angka rendah (misalnya 5) memberi tahu mesin untuk berhenti mengikuti tautan setelah lima tingkat bersarang.

```python
# Step 2: Create resource handling options and limit the processing depth
resource_opts = ResourceHandlingOptions()
resource_opts.max_handling_depth = 5  # Restricts handling to 5 levels deep
```

*Mengapa ini penting*: Dengan **membatasi kedalaman sumber daya**, Anda mencegah parser mengunduh setiap gambar, skrip, atau iframe yang mungkin direferensikan secara tidak langsung. Ini mengurangi lalu lintas jaringan dan tekanan memori, terutama untuk halaman yang menyematkan konten pihak ketiga.

## Langkah 3: Lampirkan opsi sumber daya ke opsi penyimpanan

`SaveOptions` menggabungkan semua pengaturan yang memengaruhi file output. Dengan menetapkan `resource_handling_options` kita **menerapkan penanganan sumber daya** pada operasi penyimpanan yang akan datang.

```python
# Step 3: Attach the resource options to the save options
save_opts = SaveOptions()
save_opts.resource_handling_options = resource_opts
```

*Mengapa ini penting*: Objek `save_opts` berfungsi sebagai wadah untuk berbagai flag (kompresi, format, dll.). Menambahkan `resource_handling_options` memastikan batas kedalaman dihormati selama fase penulisan.

## Langkah 4: Simpan dokumen dengan penanganan sumber daya yang dibatasi

Akhirnya, panggil `doc.save()` dengan `save_opts` yang telah dikonfigurasi. File output akan berisi hanya sumber daya yang berada dalam kedalaman yang ditentukan.

```python
# Step 4: Save the document with the limited resource handling applied
doc.save("YOUR_DIRECTORY/big_page_limited.html", save_opts)
```

**Hasil yang diharapkan**:  
File baru `big_page_limited.html` muncul di `YOUR_DIRECTORY`. Buka di browser; Anda akan melihat tata letak asli, tetapi semua sumber daya di luar lima tingkat bersarang dihilangkan. Halaman memuat lebih cepat dan mengonsumsi jauh lebih sedikit memori.

## Verifikasi HTML yang disimpan

Setelah menyimpan, sebaiknya memeriksa bahwa batas kedalaman telah dihormati.

```python
# Verify that the saved file exists and its size is reasonable
import os

output_path = "YOUR_DIRECTORY/big_page_limited.html"
if os.path.isfile(output_path):
    size_kb = os.path.getsize(output_path) / 1024
    print(f"Saved file size: {size_kb:.2f} KB")
else:
    raise FileNotFoundError("The limited HTML file was not created.")
```

Jika ukuran jauh lebih kecil daripada aslinya (yang dapat mencapai ratusan kilobyte), pengaturan **membatasi kedalaman sumber daya** berfungsi sebagaimana mestinya.

## Kesalahan umum dan cara menghindarinya

| Gejala | Penyebab | Solusi |
|--------|----------|--------|
| Tidak ada perubahan ukuran file | `max_handling_depth` dibiarkan pada default (tak terbatas) | Secara eksplisit atur `resource_opts.max_handling_depth` ke nilai < ∞ |
| Gambar hilang pada halaman | Sumber daya berada lebih dalam dari batas | Tingkatkan kedalaman atau pindahkan sumber daya penting ke tingkat yang lebih dangkal |
| `PermissionError` saat menyimpan | Direktori output bersifat read‑only | Pilih direktori yang dapat ditulisi atau sesuaikan izin OS |
| Exception tak terduga `ResourceHandlingException` | Inkompatibilitas versi perpustakaan | Upgrade ke rilis `groupdocs-viewer` terbaru (`pip install --upgrade groupdocs-viewer`) |

**Tips profesional**: Mulailah dengan kedalaman 3 untuk halaman yang sangat besar dan secara bertahap naikkan hingga kualitas visual memenuhi kebutuhan Anda.

## Kasus tepi yang mungkin Anda temui

1. **Konten dinamis yang dimuat via JavaScript** – Parser hanya melihat HTML statis. Jika halaman Anda bergantung pada skrip yang menyuntikkan sumber daya lebih lanjut, itu tidak akan pernah dihitung dalam batas kedalaman. Pertimbangkan untuk melakukan pre‑render halaman dengan browser headless sebelum menerapkan batas.  
2. **Referensi melingkar** – Beberapa halaman menyertakan iframe yang mengarah kembali ke halaman yang sama. Penghitung kedalaman mencegah loop tak terbatas, tetapi Anda mungkin masih melihat bagian yang ter‑render sebagian. Sesuaikan `max_handling_depth` atau secara manual kecualikan frame yang bermasalah.  
3. **Protokol campuran (http/https)** – Jika sumber daya menggunakan skema berbeda, perpustakaan mungkin memperlakukan mereka sebagai domain terpisah. Batas kedalaman tetap berlaku lintas protokol, tetapi izin jaringan mungkin berbeda. Pastikan lingkungan Anda mengizinkan keduanya.

## Langkah selanjutnya: penanganan sumber daya lanjutan

Sekarang Anda dapat **membatasi kedalaman sumber daya** dan **menerapkan penanganan sumber daya**, Anda mungkin ingin menjelajahi:

* **Filter khusus** – Gunakan `resource_opts.resource_filter` untuk melewatkan tipe file tertentu (mis., video besar).
* **Pengaturan kompresi** – Gabungkan `SaveOptions` dengan `compression_level` untuk lebih mengecilkan output.
* **Pemrosesan batch** – Loop melalui direktori file HTML, menerapkan batas kedalaman yang sama pada setiap file.

## Kesimpulan

Anda telah mempelajari cara **membatasi kedalaman sumber daya** dan **menerapkan penanganan sumber daya** saat menyimpan dokumen HTML besar dengan Python. Dengan mengonfigurasi `ResourceHandlingOptions` dan melampirkannya ke `SaveOptions`, Anda memperoleh kontrol halus atas berapa banyak sumber daya bersarang yang diproses, menghasilkan penyimpanan yang lebih cepat dan file output yang lebih kecil. Bereksperimenlah dengan nilai kedalaman yang berbeda dan `SaveOptions` tambahan untuk menyesuaikan perilaku dengan kebutuhan proyek Anda.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Menetapkan max_handling_depth dalam Aspose.HTML Python – Panduan Lengkap](/html/english/python/general/how-to-set-max-handling-depth-in-aspose-html-python-complete/)
- [Buat opsi penanganan sumber daya dan muat dokumen HTML dalam Python](/html/english/python/general/create-resource-handling-options-and-load-an-html-document-i/)
- [Cara Menyimpan HTML dengan Kedalaman Terkontrol – Panduan Python Langkah‑per‑Langkah](/html/english/python/general/how-to-save-html-with-controlled-depth-step-by-step-python-g/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
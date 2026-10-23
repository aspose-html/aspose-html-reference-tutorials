---
category: general
date: 2026-10-21
description: Konfigurasikan penanganan sumber daya dan muat dokumen HTML di Python
  dengan Aspose.HTML. Ikuti panduan langkah demi langkah ini untuk pemrosesan yang
  aman dan efisien.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- configure resource handling
- load html document python
- Aspose.HTML Python
- resource handling options
- HTMLDocument save options
language: id
lastmod: 2026-10-21
og_description: Konfigurasikan penanganan sumber daya dan muat dokumen HTML di Python
  dengan Aspose.HTML. Tutorial ini memandu Anda melalui pengaturan lengkap dan kode.
og_image_alt: Diagram showing configure resource handling in Aspose.HTML for Python
og_title: Konfigurasikan penanganan sumber daya saat memuat HTML di Python – panduan
  lengkap
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Configure resource handling and load an HTML document in Python with
    Aspose.HTML. Follow this step‑by‑step guide for safe, efficient processing.
  headline: Configure resource handling while loading HTML in Python
  type: TechArticle
tags:
- Python
- Aspose.HTML
- HTML processing
title: Konfigurasikan penanganan sumber daya saat memuat HTML di Python
url: /id/python/general/configure-resource-handling-while-loading-html-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konfigurasikan penanganan sumber daya saat memuat HTML di Python

Jika Anda perlu **mengonfigurasi penanganan sumber daya** untuk pipeline konversi HTML, panduan ini menunjukkan secara tepat cara melakukannya di Python menggunakan Aspose.HTML. Anda juga akan mempelajari cara paling andal untuk **memuat dokumen HTML di Python**, sehingga kode Anda berjalan aman bahkan ketika sumbernya berisi banyak sumber daya eksternal.

Memproses file HTML yang merujuk ke gambar, stylesheet, atau skrip dapat dengan cepat menjadi mahal jika perpustakaan mengikuti setiap tautan secara rekursif. Dengan mengonfigurasi penanganan sumber daya, Anda membatasi kedalaman rekursi, menghindari panggilan jaringan yang tidak perlu, dan menjaga penggunaan memori tetap dapat diprediksi. Langkah‑langkah di bawah ini mencakup alur kerja lengkap, mulai dari mengimpor kelas yang tepat hingga menyimpan file yang telah diproses.

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki:

* Python 3.8 atau yang lebih baru terpasang.
* Lisensi aktif Aspose.HTML untuk Python (atau percobaan gratis) – Anda dapat memperolehnya dari situs web Aspose.
* Paket `aspose-html` terpasang melalui `pip install aspose-html`.
* Folder yang berisi file `input.html` yang ingin Anda proses.

Persyaratan ini minimal; tutorial ini bekerja di IDE atau editor apa pun yang Anda sukai.

## Langkah 1: Impor kelas Aspose.HTML yang Anda butuhkan

Langkah pertama adalah membawa tipe yang diperlukan ke dalam skrip Anda. Mengimpor hanya kelas yang Anda gunakan menjaga namespace tetap bersih dan membuat kode lebih mudah dibaca.

```python
# Import the core Aspose.HTML classes for document handling and saving
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions
```

*`HTMLDocument`* mewakili file HTML yang telah diparsing, *`ResourceHandlingOptions`* memungkinkan Anda mengontrol bagaimana sumber daya eksternal diambil, dan *`SaveOptions`* menggabungkan pengaturan tersebut untuk operasi penyimpanan akhir.

## Langkah 2: Buat objek SaveOptions untuk menyimpan konfigurasi

`SaveOptions` adalah kontainer yang dibaca metode `save` saat menulis file output. Dengan mengonfigurasinya sebelum Anda memuat dokumen, Anda memastikan semua operasi selanjutnya menghormati batas sumber daya Anda.

```python
# Initialize SaveOptions – this will store all saving‑related settings
save_options = SaveOptions()
```

Anda dapat memperluas objek ini nanti dengan opsi tambahan seperti pengaturan konversi PDF atau penyesuaian kualitas gambar, tetapi untuk tutorial ini kami fokus pada penanganan sumber daya.

## Langkah 3: Konfigurasikan penanganan sumber daya untuk membatasi kedalaman rekursi

Halaman HTML yang sangat bersarang dapat menyebabkan parser mengikuti puluhan tautan sumber daya, yang berujung pada waktu proses yang lama atau kesalahan out‑of‑memory. Menetapkan `max_handling_depth` memberi tahu Aspose.HTML untuk berhenti setelah sejumlah level yang ditentukan.

```python
# Set up resource handling limits
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 5   # Stop after 5 levels of resource handling
save_options.resource_handling_options = resource_options
```

*Mengapa 5?* Pada kebanyakan skenario dunia nyata, kedalaman 5 menangkap halaman utama, stylesheet dan skrip langsungnya, serta sumber daya yang mereka referensikan, tanpa menyelam ke situs pihak ketiga. Sesuaikan nilai ini berdasarkan toleransi risiko proyek Anda:

* **Nilai lebih rendah (mis., 2)** – paling aman untuk sumber yang tidak dipercaya; hanya sumber daya langsung yang diambil.
* **Nilai lebih tinggi (mis., 10)** – berguna ketika Anda tahu HTML terstruktur dengan baik dan membutuhkan aset yang lebih dalam.

## Langkah 4: Muat dokumen HTML yang ingin Anda proses

Sekarang opsi penanganan sudah siap, muat file sumber. Konstruktor `HTMLDocument` membaca file dan menerapkan pengaturan penanganan sumber daya yang telah didefinisikan sebelumnya ketika Anda kemudian memanggil `save`.

```python
# Load the source HTML file – replace YOUR_DIRECTORY with your actual path
document = HTMLDocument("YOUR_DIRECTORY/input.html")
```

Jika Anda perlu **memuat dokumen HTML di Python** dari URL alih‑alih file lokal, ganti path file dengan string URL, misalnya `HTMLDocument("https://example.com/page.html")`. Batas penanganan sumber daya yang sama akan diterapkan.

## Langkah 5: Simpan dokumen yang diproses menggunakan opsi yang dikonfigurasi

Akhirnya, tulis file output. Metode `save` menghormati `SaveOptions` yang Anda berikan, memastikan hanya sumber daya yang diizinkan yang disematkan.

```python
# Save the processed HTML while applying the resource handling configuration
document.save("YOUR_DIRECTORY/output.html", save_options)
```

Setelah penyimpanan selesai, `output.html` berisi markup asli ditambah sumber daya apa pun yang diambil dalam kedalaman yang diizinkan. Sumber daya di luar batas kedalaman diabaikan, mencegah panggilan jaringan yang tidak terduga.

### Hasil yang Diharapkan

Menjalankan skrip dengan halaman HTML tipikal yang merujuk ke stylesheet, dua gambar, dan sebuah file JavaScript akan menghasilkan file output yang menyematkan stylesheet dan dua gambar (jika berada dalam lima level pertama). File JavaScript, jika berada lebih dalam dari batas, akan dikecualikan.

Anda dapat memverifikasi hasilnya dengan membuka `output.html` di peramban dan memastikan halaman ditampilkan dengan benar tanpa aset yang hilang.

## Kasus tepi dan tips praktis

| Situasi | Penyesuaian yang disarankan |
|-----------|------------------------|
| **Sumber daya eksternal diblokir oleh firewall** | Tingkatkan `max_handling_depth` hanya jika Anda juga mengonfigurasi proxy melalui `resource_options.proxy`. |
| **Anda perlu menonaktifkan sepenuhnya pengambilan sumber daya eksternal** | Setel `resource_options.enable_resource_handling = False`. Ini mematikan semua panggilan jaringan, menyisakan hanya markup asli. |
| **File CSS besar menyebabkan lonjakan memori** | Gunakan `resource_options.max_resource_size = 1024 * 1024` (1 MB) untuk membatasi ukuran masing‑masing sumber daya. |
| **Anda ingin mencatat sumber daya mana yang dilewati** | Implementasikan `ResourceHandler` kustom dengan mewarisi `ResourceHandlerBase` dan lampirkan ke `resource_options.custom_resource_handler`. |

**Pro tip:** Selalu uji dengan sampel representatif dari sumber HTML Anda sebelum diterapkan ke produksi. Periksa ukuran file yang dihasilkan dan waktu pemuatan; jika ukuran terlalu besar, turunkan `max_handling_depth` atau aktifkan batas ukuran.

## Skrip lengkap untuk salin‑tempel cepat

Berikut adalah contoh lengkap yang dapat dijalankan dan mencakup semua langkah yang dibahas. Ganti `YOUR_DIRECTORY` dengan path aktual di mesin Anda.

```python
# ------------------------------------------------------------
# Aspose.HTML – configure resource handling while loading HTML
# ------------------------------------------------------------

from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

# 1️⃣ Create SaveOptions container
save_options = SaveOptions()

# 2️⃣ Define resource handling limits
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 5          # limit recursion depth
# Optional: resource_options.max_resource_size = 2 * 1024 * 1024  # 2 MB per resource
save_options.resource_handling_options = resource_options

# 3️⃣ Load the source HTML document
document = HTMLDocument("YOUR_DIRECTORY/input.html")   # <-- load html document python

# 4️⃣ Save the document with the configured options
document.save("YOUR_DIRECTORY/output.html", save_options)

print("HTML processing complete. Output saved to output.html")
```

Menjalankan skrip ini mencetak pesan konfirmasi dan meninggalkan Anda dengan file HTML yang diproses dengan aman.

## Kesimpulan

Anda kini tahu cara **mengonfigurasi penanganan sumber daya** dan **memuat dokumen HTML di Python** secara andal menggunakan Aspose.HTML. Dengan membatasi kedalaman penanganan, Anda melindungi aplikasi dari rekursi dalam, lalu lintas jaringan yang tidak terkendali, dan tekanan memori sambil tetap mempertahankan aset penting yang diperlukan untuk rendering yang tepat.

Dari sini Anda dapat menjelajahi:

* Mengonversi HTML yang diproses ke PDF (`document.save("output.pdf", PdfSaveOptions())`).
* Menyesuaikan `ResourceHandlingOptions` lebih lanjut (pengaturan proxy, handler kustom).
* Mengintegrasikan alur kerja ini ke layanan web yang menyanitasi HTML yang diunggah pengguna sebelum ditampilkan.

Silakan bereksperimen dengan nilai kedalaman dan batas sumber daya yang berbeda untuk menemukan titik optimal bagi kasus penggunaan spesifik Anda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara menggunakan opsi sumber daya dengan Aspose.HTML untuk Python](/html/english/python/general/how-to-use-resource-options-with-aspose-html-for-python/)
- [Cara Menyimpan Dokumen HTML dengan Batas Sumber Daya – Panduan Python Lengkap](/html/english/python/general/how-to-save-html-document-with-resource-limits-complete-pyth/)
- [Cara Menetapkan max_handling_depth di Aspose.HTML Python – Panduan Lengkap](/html/english/python/general/how-to-set-max-handling-depth-in-aspose-html-python-complete/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
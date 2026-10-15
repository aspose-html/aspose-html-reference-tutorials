---
category: general
date: 2026-10-15
description: Pelajari cara membuat opsi penanganan sumber daya dan cara mengatur kedalaman
  penanganan maksimum untuk penyimpanan Markdown di Python. Ikuti panduan langkah
  demi langkah.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- how to set max handling depth
language: id
lastmod: 2026-10-15
og_description: Buat opsi penanganan sumber daya di Python untuk mengontrol pemrosesan
  sumber daya bersarang. Tutorial ini menunjukkan cara mengatur kedalaman penanganan
  maksimum untuk ekspor Markdown yang dapat diandalkan.
og_image_alt: Screenshot showing Python code to create resource handling options and
  set max handling depth
og_title: Buat opsi penanganan sumber daya – Panduan Python
schemas:
- author: Aspose
  dateModified: '2026-10-15'
  description: Learn how to create resource handling options and how to set max handling
    depth for Markdown saving in Python. Follow a step‑by‑step guide.
  headline: How to create resource handling options with Python
  type: TechArticle
tags:
- resource handling
- Markdown
- Python
- options
title: Cara membuat opsi penanganan sumber daya dengan Python
url: /id/python/general/how-to-create-resource-handling-options-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat opsi penanganan sumber daya dengan Python

Jika Anda perlu **membuat opsi penanganan sumber daya** untuk ekspor Markdown, panduan ini memberikan solusi lengkap. Anda akan melihat secara tepat **cara mengatur kedalaman penanganan maksimum** sehingga sumber daya bersarang berhenti diproses setelah tingkat yang diinginkan.

Penanganan sumber daya penting ketika Anda menghasilkan Markdown dari dokumen kompleks yang berisi gambar, file tersemat, atau aset tertaut lainnya. Rekursi yang tidak terkendali dapat menyebabkan masalah kinerja atau kesalahan kehabisan memori. Dengan mengonfigurasi kedalaman penanganan, Anda membuat proses menjadi dapat diprediksi dan efisien.

Dalam tutorial ini Anda akan:

* Inisialisasi objek `ResourceHandlingOptions`.
* Konfigurasikan kedalaman penanganan maksimum.
* Lampirkan opsi ke instance `MarkdownSaveOptions`.
* Jalankan contoh lengkap yang dapat Anda salin ke proyek Anda.

Tidak diperlukan pustaka eksternal selain SDK standar, dan kode berfungsi dengan versi terbaru paket Python per Oktober 2026.

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki:

* Python 3.9 atau lebih baru terpasang.
* SDK yang menyediakan `ResourceHandlingOptions` dan `MarkdownSaveOptions` (misalnya, `groupdocs-viewer` atau paket serupa). Instal dengan:

```bash
pip install groupdocs-viewer
```

* Pemahaman dasar tentang kelas Python dan atribut objek.

## Langkah 1: Buat opsi penanganan sumber daya

Langkah pertama adalah **membuat opsi penanganan sumber daya**. Objek ini berfungsi sebagai wadah untuk semua pengaturan yang terkait dengan sumber daya.

```python
from groupdocs.viewer import ResourceHandlingOptions, MarkdownSaveOptions

# Step 1: Instantiate the options object
resource_options = ResourceHandlingOptions()
```

`ResourceHandlingOptions` tidak menerapkan batas apa pun secara default, yang berarti viewer akan mengikuti setiap sumber daya tertaut yang ditemukannya. Menginisialisasi objek memberikan Anda kanvas bersih untuk menerapkan kontrol yang tepat.

## Langkah 2: Cara mengatur kedalaman penanganan maksimum

Sekarang Anda akan mempelajari **cara mengatur kedalaman penanganan maksimum**. Properti `max_handling_depth` menentukan jumlah tingkat bersarang yang akan diproses oleh exporter sebelum berhenti.

```python
# Step 2: Limit the handling depth to five levels
resource_options.max_handling_depth = 5
```

Mengapa membatasi kedalaman? Bayangkan sebuah dokumen Markdown yang merujuk ke file Markdown lain, yang pada gilirannya merujuk ke file ketiga, dan seterusnya. Tanpa batas kedalaman, exporter dapat melakukan rekursi tanpa akhir, mengonsumsi memori dan CPU. Menetapkan `max_handling_depth` ke `5` memberi tahu mesin untuk berhenti setelah lima sumber daya bersarang, yang merupakan nilai default aman untuk kebanyakan proyek.

### Kasus khusus: kedalaman tak terbatas

Jika Anda sengaja menginginkan rekursi tak terbatas (jarang dalam produksi), setel nilai menjadi `None`:

```python
resource_options.max_handling_depth = None  # No limit
```

Perlu diingat bahwa kedalaman tak terbatas dapat menyebabkan penurunan kinerja pada pohon dokumen yang sangat besar.

## Langkah 3: Lampirkan opsi ke MarkdownSaveOptions

Setelah mengonfigurasi penanganan sumber daya, Anda harus melampirkan opsi ke instance `MarkdownSaveOptions`. Ini memberi tahu exporter untuk menggunakan pengaturan saat menyimpan.

```python
# Step 3: Create MarkdownSaveOptions and attach the resource handling config
markdown_options = MarkdownSaveOptions()
markdown_options.resource_handling_options = resource_options
```

`MarkdownSaveOptions` mengumpulkan semua pengaturan terkait ekspor. Dengan menetapkan `resource_options` ke atribut `resource_handling_options`-nya, Anda memastikan bahwa batas kedalaman diterapkan selama konversi.

## Langkah 4: Jalankan konversi lengkap (demo opsional)

Potongan kode berikut menunjukkan konversi lengkap dari dokumen contoh ke Markdown menggunakan opsi yang baru saja Anda buat. Sesuaikan jalur file dengan lingkungan Anda.

```python
from groupdocs.viewer import Viewer

# Path to the source document (e.g., a DOCX with embedded images)
source_path = "sample.docx"
# Path where the Markdown output will be saved
output_path = "output.md"

# Initialize the viewer with the source file
viewer = Viewer(source_path)

# Perform the conversion using the configured options
viewer.save(output_path, markdown_options)

print(f"Conversion complete. Markdown saved to {output_path}")
```

**Output yang diharapkan**

```
Conversion complete. Markdown saved to output.md
```

Setelah menjalankan skrip, buka `output.md`. Anda akan melihat bahwa gambar dan sumber daya lain direferensikan hingga lima tingkat kedalaman; tautan yang lebih dalam diabaikan, mencegah rekursi yang tidak terkendali.

## Tips profesional: verifikasi kedalaman penanganan saat runtime

Jika Anda perlu memastikan bahwa batas kedalaman diterapkan, Anda dapat memeriksa Markdown yang dihasilkan untuk referensi sumber daya yang hilang atau mengaktifkan logging detail di SDK:

```python
viewer.set_logging(True)  # Enable detailed logs
```

Log akan menampilkan pesan seperti:

```
[INFO] Resource handling stopped at depth 5 for file 'nested_image.png'
```

## Pertanyaan umum

**Bagaimana jika dokumen saya memiliki kurang dari lima sumber daya bersarang?**  
Exporter akan memproses semua sumber daya yang tersedia karena batas kedalaman lebih tinggi daripada kedalaman aktual. Tidak ada sumber daya yang dipotong.

**Apakah saya dapat menetapkan batas yang berbeda untuk tipe file yang berbeda?**  
Ya. Buat objek `ResourceHandlingOptions` terpisah untuk setiap format ekspor dan tetapkan ke instance `SaveOptions` yang sesuai.

**Apakah batas kedalaman hanya memengaruhi gambar?**  
Tidak. Batas tersebut berlaku untuk *semua* sumber daya yang dapat diikuti oleh exporter, termasuk file tersemat, hyperlink, dan penyertaan Markdown bersarang.

## Kesimpulan

Anda kini tahu cara **membuat opsi penanganan sumber daya** dan **mengatur kedalaman penanganan maksimum** untuk ekspor Markdown yang andal dengan Python. Dengan membatasi rekursi, Anda melindungi aplikasi dari penggunaan memori berlebih sambil tetap mempertahankan hierarki konten yang diperlukan.

Langkah selanjutnya yang dapat Anda jelajahi:

* Sesuaikan properti `ResourceHandlingOptions` lainnya seperti `extract_images` atau `preserve_links`.
* Gabungkan penanganan sumber daya dengan konvensi penamaan khusus untuk file yang diekstrak.
* Bereksperimen dengan nilai kedalaman yang berbeda untuk menemukan titik optimal bagi kumpulan dokumen spesifik Anda.

Silakan sesuaikan potongan kode dengan alur kerja Anda dan bagikan temuan Anda kepada komunitas. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Menyimpan HTML di C# – Panduan Lengkap Menggunakan Penangan Sumber Daya Kustom](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Cara Mengompres HTML di C# – Tutorial Penangan Sumber Daya Kustom](/html/english/net/html-extensions-and-conversions/how-to-zip-html-in-c-custom-resource-handler-tutorial/)
- [Cara membuat penangan skema kustom dengan Aspose.HTML untuk Java](/html/english/java/custom-schema-message-handling/custom-schema-message-handler/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-11-27
description: Cara membatasi kedalaman selama pemrosesan HTML menggunakan Python. Ikuti
  contoh memuat dokumen HTML ini dengan opsi penanganan sumber daya.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to limit depth
- load html document
- html processing example
language: id
lastmod: 2026-11-27
og_description: Cara membatasi kedalaman saat memproses HTML di Python. Pelajari cara
  memuat dokumen HTML dan mengonfigurasi penanganan sumber daya untuk hasil yang efisien.
og_image_alt: Illustration of how to limit depth in HTML processing using Python
og_title: Cara membatasi kedalaman saat memproses HTML di Python
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: How to limit depth during HTML processing using Python. Follow this
    load html document example with resource handling options.
  headline: How to limit depth when processing HTML documents in Python
  type: TechArticle
tags:
- HTML processing
- resource handling
- Python
title: Cara membatasi kedalaman saat memproses dokumen HTML di Python
url: /id/python/general/how-to-limit-depth-when-processing-html-documents-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membatasi kedalaman saat memproses dokumen HTML dengan Python

Jika Anda perlu **cara membatasi kedalaman** saat menangani file HTML, panduan ini menunjukkan solusi lengkap yang siap dijalankan. Anda akan melihat alur kerja **memuat dokumen html** yang praktis dan contoh **pemrosesan html** yang jelas yang menunjukkan konfigurasi penanganan sumber daya.

Memproses pohon HTML yang besar dapat dengan cepat mengonsumsi memori atau CPU jika setiap elemen bersarang ditelusuri. Dengan membatasi kedalaman penanganan, Anda melindungi aplikasi dari rekursi tak terkendali dan menjaga kinerja tetap dapat diprediksi.

## Apa yang dibahas dalam tutorial ini

* Cara **memuat dokumen html** dengan pustaka yang kompatibel dengan Python.  
* Cara membuat dan melampirkan objek `ResourceHandlingOptions`.  
* Cara mengatur `max_handling_depth` untuk menghentikan pemrosesan setelah sejumlah tingkat bersarang tertentu.  
* Cara menyimpan file yang telah diubah menggunakan opsi yang telah dikonfigurasi.  

Pada akhir artikel ini Anda akan memiliki skrip yang berfungsi untuk membatasi kedalaman, menghindari penggunaan sumber daya yang berlebihan, dan menghasilkan file HTML output yang bersih.

![Cara membatasi kedalaman dalam pemrosesan HTML menggunakan Python](image.png)

## Prasyarat

| Persyaratan | Alasan |
|-------------|--------|
| Python 3.8+ | Diperlukan untuk petunjuk tipe pustaka dan sintaks modern. |
| `groupdocs-viewer` (atau paket penanganan HTML serupa) diinstal via `pip install groupdocs-viewer` | Menyediakan `HTMLDocument`, `ResourceHandlingOptions`, dan `SaveOptions`. |
| Familiaritas dasar dengan fungsi Python dan kode berorientasi objek | Memungkinkan Anda menyesuaikan contoh ke proyek Anda sendiri. |

> **Tip profesional:** Jika Anda menggunakan lingkungan virtual, aktifkan terlebih dahulu sebelum menginstal paket untuk menjaga ketergantungan tetap terisolasi.

## Langkah 1: Memuat dokumen HTML

Tindakan pertama adalah membaca file sumber ke dalam objek `HTMLDocument`. Objek ini mewakili seluruh pohon markup dan memberi Anda metode untuk manipulasi lebih lanjut.

```python
from groupdocs.viewer import HTMLDocument, ResourceHandlingOptions, SaveOptions

# Step 1 – load the source HTML document
html_doc = HTMLDocument("YOUR_DIRECTORY/input.html")
```

*Mengapa ini penting*: Memuat dokumen membuat representasi dalam memori yang dapat dijelajahi oleh pustaka. Tanpa langkah ini Anda tidak dapat menerapkan aturan penanganan sumber daya apa pun.

## Langkah 2: Membuat opsi penanganan sumber daya

`ResourceHandlingOptions` memungkinkan Anda menyesuaikan cara sumber daya eksternal (gambar, skrip, gaya) diproses. Untuk pembatasan kedalaman, properti `max_handling_depth` adalah kuncinya.

```python
# Step 2 – create a resource handling configuration
resource_options = ResourceHandlingOptions()
```

Sekarang Anda memiliki objek konfigurasi kosong yang dapat diisi dengan batasan yang diinginkan.

## Langkah 3: Membatasi kedalaman pemrosesan sumber daya bersarang

Atur `max_handling_depth` ke jumlah tingkat bersarang yang dapat Anda tangani. Pada contoh ini kami berhenti setelah tiga tingkat, yang biasanya cukup untuk halaman web tipikal sekaligus mencegah struktur bersarang dalam menghabiskan sistem.

```python
# Step 3 – limit processing depth (e.g., stop after 3 levels)
resource_options.max_handling_depth = 3
```

*Mengapa Anda harus membatasi kedalaman*: HTML yang sangat bersarang (misalnya tabel besar di dalam tabel atau pohon komponen rekursif) dapat menyebabkan overflow stack atau lonjakan memori yang besar. Batas kedalaman memberi tahu mesin untuk mengabaikan apa pun di luar level yang ditentukan, secara efektif **cara membatasi kedalaman** dalam praktik.

## Langkah 4: Menempelkan konfigurasi ke opsi penyimpanan

`SaveOptions` menggabungkan semua penyesuaian yang ingin Anda terapkan pada penulis saat mengekspor dokumen. Dengan menetapkan properti `resource_handling_options`, Anda memastikan batas kedalaman dihormati selama operasi penyimpanan.

```python
# Step 4 – prepare save options and attach the resource handling configuration
save_options = SaveOptions()
save_options.resource_handling_options = resource_options
```

Jika Anda memerlukan pengaturan tambahan (seperti encoding atau pretty‑print), dapat ditambahkan ke instance `save_options` yang sama.

## Langkah 5: Menyimpan dokumen yang telah diproses

Akhirnya, panggil metode `save` dengan jalur output dan `save_options` yang telah dikonfigurasi. Pustaka akan menelusuri pohon HTML, menghormati batas kedalaman, dan menulis markup yang dihasilkan ke file tujuan.

```python
# Step 5 – save the processed document with the configured options
html_doc.save("YOUR_DIRECTORY/output.html", save_options)
```

### Hasil yang diharapkan

* File `output.html` berisi konten asli hingga tiga tingkat bersarang.  
* Elemen yang lebih dalam dihilangkan, menghasilkan versi halaman yang ringan.  
* Tidak ada error yang muncul meskipun sumber berisi ratusan tag bersarang.

Anda dapat memverifikasi hasilnya dengan membuka `output.html` di browser atau mencetak cuplikan:

```python
with open("YOUR_DIRECTORY/output.html", "r", encoding="utf-8") as f:
    print(f.read()[:500])   # show the first 500 characters
```

## Pertanyaan umum dan kasus tepi

| Pertanyaan | Jawaban |
|------------|---------|
| **Bagaimana jika saya membutuhkan batas yang lebih dalam?** | Ubah `resource_options.max_handling_depth` ke bilangan bulat yang lebih tinggi, misalnya `5`. |
| **Apakah gambar di luar batas kedalaman akan dihapus?** | Ya. Setiap sumber yang berada di node lebih dalam dari batas akan diabaikan, termasuk gambar, skrip, dan gaya inline. |
| **Bisakah saya menonaktifkan pembatasan kedalaman sepenuhnya?** | Atur `max_handling_depth` ke `0` atau `None` (tergantung versi pustaka) untuk memproses seluruh pohon. |
| **Bagaimana ini berinteraksi dengan impor CSS?** | File CSS diperlakukan sebagai sumber; jika mereka ditautkan dari node yang lebih dalam dari batas, mereka tidak akan diambil. |
| **Apakah batas diterapkan per tipe sumber?** | Batas kedalaman bersifat global untuk seluruh pohon dokumen; tidak membedakan antara gambar, skrip, atau node lainnya. |

## Skrip lengkap yang berfungsi

Menggabungkan semua langkah menghasilkan satu skrip mandiri yang dapat Anda salin‑tempel ke file `.py` dan jalankan langsung:

```python
from groupdocs.viewer import HTMLDocument, ResourceHandlingOptions, SaveOptions

def limit_html_depth(input_path: str, output_path: str, max_depth: int = 3) -> None:
    """
    Loads an HTML file, limits the processing depth, and saves the result.

    Args:
        input_path: Path to the source HTML file.
        output_path: Destination path for the processed HTML.
        max_depth: Maximum nesting level to process (default is 3).
    """
    # Load the source document
    html_doc = HTMLDocument(input_path)

    # Configure depth limiting
    resource_options = ResourceHandlingOptions()
    resource_options.max_handling_depth = max_depth

    # Attach configuration to save options
    save_options = SaveOptions()
    save_options.resource_handling_options = resource_options

    # Save the transformed document
    html_doc.save(output_path, save_options)

if __name__ == "__main__":
    # Example usage – adjust paths as needed
    limit_html_depth(
        input_path="YOUR_DIRECTORY/input.html",
        output_path="YOUR_DIRECTORY/output.html",
        max_depth=3
    )
```

Menjalankan skrip ini menghasilkan `output.html` yang sama seperti yang dijelaskan sebelumnya. Silakan sesuaikan `max_depth` atau tambahkan fungsi dengan parameter tambahan (misalnya encoding khusus).

## Langkah selanjutnya dan topik terkait

* **Penanganan sumber daya lanjutan** – jelajahi properti `ResourceHandlingOptions` seperti


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik yang sangat terkait dan membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Mengatur max_handling_depth di Aspose.HTML Python – Panduan Lengkap](/html/english/python/general/how-to-set-max-handling-depth-in-aspose-html-python-complete/)
- [Membuat opsi penanganan sumber daya dan memuat dokumen HTML di Python](/html/english/python/general/create-resource-handling-options-and-load-an-html-document-i/)
- [Cara mengonfigurasi penanganan sumber daya HTML di Python dan memuat dokumen HTML](/html/english/python/general/how-to-configure-html-resource-handling-in-python-and-load-a/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
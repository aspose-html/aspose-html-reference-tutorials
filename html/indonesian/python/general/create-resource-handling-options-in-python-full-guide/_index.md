---
category: general
date: 2026-07-21
description: Buat opsi penanganan sumber daya di Python dan pelajari cara mengatur
  kedalaman penanganan maksimum untuk parsing HTML. Ikuti tutorial langkah demi langkah
  ini untuk manajemen sumber daya yang andal.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- how to set max handling depth
language: id
lastmod: 2026-07-21
og_description: Buat opsi penanganan sumber daya di Python dan langsung lihat cara
  mengatur kedalaman penanganan maksimum untuk memuat dokumen HTML yang aman. Kuasai
  teknik ini dalam hitungan menit.
og_image_alt: Screenshot of Python code that creates resource handling options with
  max handling depth set
og_title: Buat Opsi Penanganan Sumber Daya di Python – Panduan Lengkap Langkah demi
  Langkah
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  headline: Create Resource handling options in Python – Full Guide
  type: TechArticle
- description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  name: Create Resource handling options in Python – Full Guide
  steps:
  - name: Circular References
    text: 'Some legacy sites embed an iframe that points back to the original page,
      creating a loop. With `max_handling_depth` set, the loop is automatically broken
      after the third iteration. However, you might still see a warning in the logs.
      To silence noisy logs, adjust the logger level:'
  - name: Missing Resources
    text: 'If a nested resource fails to load (404 or network timeout), the parser
      throws an exception by default. Wrap the loading call in a `try/except` block
      to keep your application alive:'
  - name: Adjusting Depth Dynamically
    text: 'Sometimes you need different depths for different parts of your pipeline.
      Because `resource_options` is a mutable object, you can change `max_handling_depth`
      on the fly:'
  type: HowTo
tags:
- Python
- HTML parsing
- resource management
title: Buat Opsi Penanganan Sumber Daya di Python – Panduan Lengkap
url: /id/python/general/create-resource-handling-options-in-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Resource handling options di Python – Panduan Lengkap

Pernah bertanya-tanya bagaimana cara **create resource handling options** untuk halaman HTML yang sangat besar tanpa menghabiskan memori Anda? Anda tidak sendirian. Ketika Anda memberi dokumen raksasa ke parser, sumber daya bersarang seperti frame, iframe, atau CSS yang ditautkan dapat dengan cepat menjadi tidak terkendali.  

Berita baik? Anda dapat memberi tahu parser untuk berhenti setelah sejumlah level bersarang tertentu. Dalam tutorial ini kami akan menunjukkan **how to set max handling depth** dan menjaga aplikasi Anda tetap responsif. Siap? Mari kita mulai.

## Apa yang Akan Anda Pelajari

- Mengapa membatasi kedalaman bersarang penting untuk kinerja dan keamanan.  
- Kode tepat yang Anda perlukan untuk **create resource handling options** menggunakan kelas `ResourceHandlingOptions`.  
- Cara mengonfigurasi `max_handling_depth` sehingga parser berhenti setelah tiga level.  
- Tips menangani kasus tepi, seperti dokumen dengan referensi melingkar atau sumber daya yang hilang.  

Tidak diperlukan pengalaman sebelumnya dengan pustaka ini—hanya instalasi Python 3 yang berfungsi dan pemahaman dasar tentang file I/O.

## Prasyarat

- Python 3.8+ (pustaka ini bekerja pada semua versi terbaru).  
- Paket `htmlparser` yang menyediakan `HTMLDocument` dan `ResourceHandlingOptions`.  
- File HTML contoh (`big_page.html`) yang ditempatkan di folder yang dapat Anda referensikan.  

Jika Anda belum menginstal paket tersebut, jalankan:

```bash
pip install htmlparser
```

Sekarang dasar-dasarnya sudah selesai, mari kita masuk ke inti pembahasan.

## Buat Resource handling options – Langkah 1

Hal pertama yang harus dilakukan: Anda memerlukan sebuah instance dari `ResourceHandlingOptions`. Anggaplah itu sebagai kotak peralatan di mana Anda dapat mengatur batasan dan kebijakan yang harus dipatuhi parser.

```python
# Step 1: Create resource handling options and limit nesting depth
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # Stop after three levels of nested resources
```

**Mengapa ini penting:**  
Ketika parser menemukan sebuah `<iframe>` di dalam `<iframe>` lain, biasanya ia akan mengikuti rantai tersebut selamanya. Dengan membatasi kedalaman pada `3`, Anda mencegah rekursi tak terkendali yang dapat menghabiskan RAM atau menyebabkan stack overflow.  

> **Pro tip:** Jika Anda mem-parsing konten yang tidak terpercaya (mis., HTML yang diunggah pengguna), pertimbangkan untuk menurunkan kedalaman menjadi `1` atau `2` untuk mengurangi potensi serangan.

## Muat Dokumen HTML – Langkah 2

Dengan objek opsi Anda siap, berikan ke `HTMLDocument`. Konstruktor akan menghormati `max_handling_depth` yang baru saja Anda atur.

```python
# Step 2: Load the HTML document using the configured options
html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
```

**Apa yang terjadi di balik layar?**  
`HTMLDocument` membaca file, membangun pohon DOM, dan kemudian menelusuri setiap sumber daya eksternal (stylesheet, skrip, gambar). Setiap kali menemukan sumber daya bersarang, ia memeriksa `resource_options.max_handling_depth`. Jika batas tercapai, parser mencatat peringatan dan melewatkan bersarang lebih lanjut.  

Itu berarti Anda mendapatkan DOM yang sepenuhnya dapat digunakan untuk tiga lapisan pertama, dan sisanya diabaikan dengan aman.

## Verifikasi Konfigurasi – Langkah 3

Selalu merupakan ide yang baik untuk memastikan bahwa pengaturan Anda telah diterapkan. Objek `resource_options` menampilkan keadaan saat ini, sehingga Anda dapat mencetaknya atau melakukan assert dalam tes.

```python
# Step 3: Verify that the max handling depth is set correctly
assert resource_options.max_handling_depth == 3, "Depth limit not applied!"

print(f"Resource handling options configured: max depth = {resource_options.max_handling_depth}")
```

Jika assert berhasil, Anda dapat yakin bahwa parser akan mematuhi batas selama sisa proses.

## Menangani Kasus Tepi

### Referensi Melingkar

Beberapa situs warisan menyematkan iframe yang mengarah kembali ke halaman asli, menciptakan loop. Dengan `max_handling_depth` yang diatur, loop secara otomatis terputus setelah iterasi ketiga. Namun, Anda mungkin masih melihat peringatan di log. Untuk menenangkan log yang berisik, sesuaikan level logger:

```python
import logging
logging.getLogger("htmlparser").setLevel(logging.ERROR)
```

### Sumber Daya Hilang

Jika sumber daya bersarang gagal dimuat (404 atau timeout jaringan), parser secara default melemparkan exception. Bungkus pemanggilan pemuatan dalam blok `try/except` untuk menjaga aplikasi tetap berjalan:

```python
try:
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
except Exception as e:
    print(f"Failed to load a nested resource: {e}")
    # Fallback: load the document without additional resources
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html")
```

### Menyesuaikan Kedalaman Secara Dinamis

Kadang-kadang Anda memerlukan kedalaman yang berbeda untuk bagian-bagian pipeline yang berbeda. Karena `resource_options` adalah objek yang dapat diubah, Anda dapat mengubah `max_handling_depth` secara dinamis:

```python
resource_options.max_handling_depth = 5   # Temporarily allow deeper nesting
html_doc_deep = HTMLDocument("deep_page.html", resource_options)

resource_options.max_handling_depth = 2   # Tighten for a lightweight preview
html_doc_preview = HTMLDocument("preview.html", resource_options)
```

Hanya ingat untuk mengatur ulang nilai tersebut sebelum menggunakan kembali instance opsi yang sama di thread lain.

## Contoh Kerja Lengkap

Berikut adalah skrip lengkap yang dapat Anda salin‑tempel, sesuaikan jalur file, dan jalankan segera.

```python
import logging
from htmlparser import HTMLDocument, ResourceHandlingOptions

# Optional: Reduce noisy output
logging.getLogger("htmlparser").setLevel(logging.ERROR)

def load_document(path: str, max_depth: int = 3):
    """
    Load an HTML document with a controlled resource handling depth.
    Returns the HTMLDocument instance.
    """
    opts = ResourceHandlingOptions()
    opts.max_handling_depth = max_depth    # How to set max handling depth
    try:
        doc = HTMLDocument(path, opts)
        print(f"Loaded '{path}' with max depth {max_depth}.")
        return doc
    except Exception as exc:
        print(f"Error loading '{path}': {exc}")
        # Fallback to a simple load without resource handling
        return HTMLDocument(path)

if __name__ == "__main__":
    # Example 1: Standard depth
    doc1 = load_document("YOUR_DIRECTORY/big_page.html", max_depth=3)

    # Example 2: Deeper inspection for debugging
    doc2 = load_document("YOUR_DIRECTORY/complex_page.html", max_depth=5)

    # Example 3: Very shallow preview (e.g., thumbnail generation)
    doc3 = load_document("YOUR_DIRECTORY/preview_page.html", max_depth=1)
```

**Output yang diharapkan (ketika file ada dan terformat dengan baik):**

```
Loaded 'YOUR_DIRECTORY/big_page.html' with max depth 3.
Loaded 'YOUR_DIRECTORY/complex_page.html' with max depth 5.
Loaded 'YOUR_DIRECTORY/preview_page.html' with max depth 1.
```

Jika file tidak dapat dibaca, Anda akan melihat pesan error alih-alih crash.

![Buat resource handling options di Python](/images/resource-options.png){alt="Buat resource handling options di Python"}

## Ringkasan – Mengapa Pendekatan Ini Hebat

- **Safety first:** Membatasi kedalaman bersarang mencegah rekursi tak terkendali dan pembengkakan memori.  
- **Flexibility:** Anda dapat mengubah `max_handling_depth` pada runtime untuk menyesuaikan berbagai skenario.  
- **Simplicity:** Beberapa baris kode memungkinkan Anda **create resource handling options** dan langsung menerapkannya.  

Singkatnya, Anda kini memiliki pola yang kuat untuk mengendalikan seberapa dalam parser Anda mengikuti sumber daya eksternal.

## Apa Selanjutnya?

- Jelajahi kelas `ResourceHandlingOptions` lebih lanjut—ada flag untuk caching, penanganan timeout, dan penyaringan MIME‑type.  
- Gabungkan pembatasan kedalaman dengan string `UserAgent` khusus untuk menghindari pemblokiran oleh server yang agresif.  
- Jika Anda bekerja dengan I/O asynchronous, lihat varian `aiohtmlparser` yang menghormati opsi yang sama tetapi bekerja dengan `asyncio`.  

Jangan ragu untuk bereksperimen: coba atur kedalaman menjadi `0` dan lihat parser mengabaikan semua referensi eksternal. Ini adalah pintasan berguna ketika Anda hanya membutuhkan markup HTML mentah.

Ada pertanyaan atau halaman rumit yang masih membuat Anda bingung? Tinggalkan komentar di bawah, dan saya dengan senang hati akan membantu Anda menyesuaikan pengaturan. Selamat mem-parsing!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Buat HTML dari String di C# – Panduan Custom Resource Handler](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Cara Menyimpan HTML di C# – Panduan Lengkap Menggunakan Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Buat sandbox untuk HTML di Java – Panduan Langkah‑per‑Langkah](/html/english/java/creating-managing-html-documents/create-sandbox-for-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
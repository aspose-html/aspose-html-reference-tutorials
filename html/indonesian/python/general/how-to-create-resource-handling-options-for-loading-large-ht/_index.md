---
category: general
date: 2026-09-16
description: Pelajari cara membuat opsi penanganan sumber daya dan memuat dokumen
  HTML besar secara efisien dengan Aspose.HTML untuk Python. Panduan langkah demi
  langkah dengan kode lengkap.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- load large html document
- Aspose.HTML Python
- HTML resource management
- nested HTML resources
language: id
lastmod: 2026-09-16
og_description: Buat opsi penanganan sumber daya dan muat dokumen HTML besar dengan
  cepat menggunakan Aspose.HTML untuk Python. Ikuti tutorial lengkap ini untuk pemrosesan
  HTML yang andal.
og_image_alt: Python code screenshot that creates resource handling options for large
  HTML documents
og_title: Buat opsi penanganan sumber daya untuk memuat dokumen HTML besar – Panduan
  Python
schemas:
- author: Aspose
  dateModified: '2026-09-16'
  description: Learn how to create resource handling options and efficiently load
    large HTML documents with Aspose.HTML for Python. Step‑by‑step guide with full
    code.
  headline: How to create resource handling options for loading large HTML documents
    in Python
  type: TechArticle
- description: Learn how to create resource handling options and efficiently load
    large HTML documents with Aspose.HTML for Python. Step‑by‑step guide with full
    code.
  name: How to create resource handling options for loading large HTML documents in
    Python
  steps:
  - name: 'Optional: Adjust other resource‑handling flags'
    text: You can also control whether external URLs are fetched, whether CSS files
      are parsed, or whether scripts are ignored. These flags are useful when you
      only need the structural DOM and not the full rendering.
  - name: Verify the document was loaded
    text: 'A quick sanity check confirms that the document is ready for further processing:'
  - name: a) Document exceeds the configured depth
    text: 'If the HTML contains deeper nesting than `max_handling_depth`, Aspose.HTML
      stops loading further resources but still returns the partially built DOM. You
      can detect this situation by checking the `resource_options.max_handling_depth`
      after loading:'
  - name: b) Circular references
    text: 'Circular `<iframe>` inclusions can cause infinite loops if depth is not
      limited. The depth limit automatically breaks the cycle, but you may also want
      to log which URLs caused the break:'
  - name: c) Missing external files
    text: 'When `fetch_external_resources` is `True` and a linked CSS or image cannot
      be retrieved (e.g., 404), Aspose.HTML raises a `ResourceNotFoundException`.
      Wrap the loading call in a `try/except` block to handle it gracefully:'
  type: HowTo
tags:
- Aspose.HTML
- Python
- HTML processing
- Resource handling
title: Cara membuat opsi penanganan sumber daya untuk memuat dokumen HTML besar di
  Python
url: /id/python/general/how-to-create-resource-handling-options-for-loading-large-ht/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat opsi penanganan sumber daya untuk memuat dokumen HTML besar di Python

Jika Anda perlu **membuat opsi penanganan sumber daya** untuk file HTML yang sangat besar, tutorial ini menunjukkan secara tepat cara melakukannya. Memuat dokumen HTML besar dapat dengan cepat mengonsumsi memori atau mencapai batas rekursi, tetapi dengan mengonfigurasi opsi yang tepat Anda dapat menjaga proses tetap stabil dan berperforma baik.

Dalam panduan ini Anda juga akan belajar cara **memuat dokumen html besar** dengan Aspose.HTML untuk Python, cara menyesuaikan kedalaman penelusuran, dan cara menangani kasus tepi umum seperti referensi melingkar atau sumber daya yang hilang. Tidak diperlukan dokumentasi eksternal—semua yang Anda butuhkan sudah termasuk dalam contoh di bawah.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* Python 3.8 atau yang lebih baru terpasang.
* Perpustakaan Aspose.HTML untuk Python (`aspose-html`) terpasang melalui `pip install aspose-html`.
* File HTML berukuran besar (misalnya `bigpage.html`) yang berisi sumber daya bersarang seperti gambar, CSS, atau iframe.

Jika ada yang belum ada, instal dulu; langkah-langkah di bawah mengasumsikan lingkungan sudah siap.

## Langkah 1: Impor kelas Aspose.HTML yang diperlukan

Hal pertama yang harus Anda lakukan adalah mengimpor kelas yang memungkinkan Anda bekerja dengan dokumen HTML dan pengaturan penanganan sumber daya.

```python
# Step 1: Import the required Aspose.HTML classes
from aspose.html import HTMLDocument, ResourceHandlingOptions
```

`HTMLDocument` mewakili file HTML yang ingin Anda proses, sementara `ResourceHandlingOptions` memberi Anda kontrol detail tentang bagaimana sumber daya eksternal diambil dan seberapa dalam perpustakaan akan mengikuti referensi bersarang.

## Langkah 2: Buat opsi penanganan sumber daya dan batasi kedalaman penelusuran

Saat Anda **membuat opsi penanganan sumber daya**, Anda menentukan berapa tingkat sumber daya bersarang yang akan diikuti parser. Membatasi kedalaman mencegah rekursi tak terkendali pada halaman yang menyisipkan halaman lain berulang kali.

```python
# Step 2: Create resource handling options and limit nesting depth
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 5  # Stop after 5 levels of nested resources
```

*Mengapa membatasi kedalaman penelusuran?*  
Sebuah dokumen HTML besar dapat berisi banyak tag `<iframe>` atau `<object>` yang mengarah ke dokumen lain, yang pada gilirannya memuat lebih banyak sumber daya. Tanpa batas kedalaman, parser dapat mengonsumsi memori berlebih atau bahkan crash dengan `RecursionError`. Menetapkan `max_handling_depth` ke angka yang wajar (5 dalam contoh ini) menyeimbangkan kelengkapan dengan keamanan.

### Opsional: Sesuaikan flag penanganan sumber daya lainnya

Anda juga dapat mengontrol apakah URL eksternal diambil, apakah file CSS diparse, atau apakah skrip diabaikan. Flag ini berguna ketika Anda hanya membutuhkan DOM struktural dan bukan rendering penuh.

```python
resource_options.fetch_external_resources = True   # Allow HTTP/HTTPS resources
resource_options.enable_css_parsing = True        # Parse linked CSS files
resource_options.enable_script_execution = False  # Skip JavaScript for speed
```

## Langkah 3: Muat dokumen HTML besar menggunakan opsi yang dikonfigurasi

Sekarang setelah Anda **membuat opsi penanganan sumber daya**, Anda dapat dengan aman **memuat dokumen html besar** tanpa membebani sistem Anda.

```python
# Step 3: Load the HTML document using the configured options
document_path = "YOUR_DIRECTORY/bigpage.html"
document = HTMLDocument(document_path, resource_options)
```

Konstruktor menerima jalur file dan objek `resource_options` yang Anda siapkan. Aspose.HTML menghormati batas kedalaman dan flag lainnya yang Anda tetapkan, sehingga proses pemuatan selesai dengan cepat bahkan untuk halaman berukuran megabyte.

### Verifikasi dokumen telah dimuat

Pemeriksaan cepat memastikan bahwa dokumen siap untuk diproses lebih lanjut:

```python
print(f"Document title: {document.title}")
print(f"Root element: {document.root.tag_name}")
print(f"Number of child nodes: {len(document.root.child_nodes)}")
```

Output tipikal:

```
Document title: Example Large Page
Root element: html
Number of child nodes: 12
```

Jika judul kosong, file mungkin tidak memiliki tag `<title>`, tetapi DOM tetap dapat diakses.

## Langkah 4: Telusuri DOM untuk menghitung sumber daya eksternal

Seringkali Anda perlu mengetahui berapa banyak gambar, stylesheet, atau iframe yang sebenarnya dimuat. Potongan kode berikut menunjukkan cara menelusuri DOM dan mengumpulkan statistik.

```python
# Step 4: Count external resources (images, stylesheets, iframes)
resource_counts = {"img": 0, "link": 0, "iframe": 0}

def count_resources(node):
    if node.node_type == node.ELEMENT_NODE:
        tag = node.tag_name.lower()
        if tag == "img":
            resource_counts["img"] += 1
        elif tag == "link" and node.get_attribute("rel") == "stylesheet":
            resource_counts["link"] += 1
        elif tag == "iframe":
            resource_counts["iframe"] += 1

    # Recurse into child nodes
    for child in node.child_nodes:
        count_resources(child)

count_resources(document.root)

print("Resource summary:")
for kind, cnt in resource_counts.items():
    print(f"  {kind}: {cnt}")
```

**Mengapa menelusuri DOM?**  
Bahkan dengan pembatasan kedalaman, Anda mungkin ingin memvalidasi bahwa semua sumber daya yang diharapkan telah diambil. Loop ini memberi Anda gambaran jelas tentang apa yang sebenarnya dimuat parser.

## Langkah 5: Simpan dokumen yang diproses (opsional)

Jika Anda perlu menyimpan versi HTML yang telah dinormalisasi (misalnya, setelah menghapus skrip yang tidak diinginkan), Anda dapat menyimpannya kembali ke disk.

```python
# Step 5: Save the cleaned document
output_path = "YOUR_DIRECTORY/processed_bigpage.html"
document.save(output_path)
print(f"Processed document saved to {output_path}")
```

Menyimpan tidak mengubah file asli; ini membuat salinan baru yang menghormati konfigurasi penanganan sumber daya yang Anda definisikan.

## Langkah 6: Tangani kasus tepi umum

### a) Dokumen melebihi kedalaman yang dikonfigurasi

Jika HTML berisi penelusuran bersarang lebih dalam daripada `max_handling_depth`, Aspose.HTML menghentikan pemuatan sumber daya lebih lanjut tetapi tetap mengembalikan DOM yang dibangun sebagian. Anda dapat mendeteksi situasi ini dengan memeriksa `resource_options.max_handling_depth` setelah pemuatan:

```python
if document.resource_handling_options.max_handling_depth_reached:
    print("Warning: Some nested resources were not loaded due to depth limit.")
```

### b) Referensi melingkar

Inklusi `<iframe>` melingkar dapat menyebabkan loop tak terbatas jika kedalaman tidak dibatasi. Batas kedalaman secara otomatis memutus siklus, tetapi Anda mungkin juga ingin mencatat URL mana yang menyebabkan pemutusan:

```python
if document.resource_handling_options.circular_reference_detected:
    print("Circular reference detected and ignored.")
```

### c) File eksternal yang hilang

Ketika `fetch_external_resources` bernilai `True` dan CSS atau gambar yang terhubung tidak dapat diambil (misalnya, 404), Aspose.HTML akan mengeluarkan `ResourceNotFoundException`. Bungkus pemanggilan pemuatan dalam blok `try/except` untuk menanganinya secara elegan:

```python
try:
    document = HTMLDocument(document_path, resource_options)
except Exception as e:
    print(f"Failed to load resources: {e}")
    # Continue with a fallback or abort as needed
```

## Langkah 7: Praktik terbaik dan tip kinerja

* **Gunakan kembali `ResourceHandlingOptions`** – Buat satu instance dan berikan ke beberapa pemuatan `HTMLDocument` jika Anda memproses banyak file. Ini menghindari alokasi objek berulang.
* **Setel `max_handling_depth` berdasarkan penelusuran yang diharapkan** – Untuk kebanyakan halaman web, kedalaman 3‑5 sudah cukup. Tingkatkan hanya ketika Anda tahu kontennya mengandung frame yang dalam.
* **Nonaktifkan eksekusi skrip** – JavaScript jarang diperlukan untuk parsing sisi server dan dapat memperlambat pemuatan secara signifikan. Biarkan `enable_script_execution` diset ke `False` kecuali Anda memang memerlukan perubahan DOM yang dihasilkan skrip.
* **Gunakan I/O streaming untuk file sangat besar** – Aspose.HTML mendukung pemuatan dari stream; ini mengurangi tekanan memori ketika file HTML melebihi beberapa ratus megabyte.

```python
from aspose.html import FileStream

with FileStream(document_path, FileStream.READ) as stream:
    document = HTMLDocument(stream, resource_options)
```

## Kesimpulan

Anda kini tahu cara **membuat opsi penanganan sumber daya** dan secara andal **memuat dokumen html besar** dengan Aspose.HTML untuk Python. Dengan mengonfigurasi batas kedalaman, mengatur pengambilan sumber daya eksternal, dan menangani kasus tepi seperti referensi melingkar, Anda menjaga penggunaan memori tetap dapat diprediksi dan menghindari crash.

Dari dasar ini Anda dapat:

* Mengekstrak atau mengubah konten (misalnya, mengonversi ke PDF atau teks biasa).
* Melakukan analisis massal penggunaan sumber daya di seluruh situs web.
* Mengintegrasikan parsing HTML ke dalam pipeline pengujian otomatis.

Silakan bereksperimen dengan nilai `max_handling_depth` yang berbeda, mengaktifkan atau menonaktifkan parsing CSS, dan menggabungkan pendekatan ini dengan perpustakaan Aspose lainnya untuk alur kerja dokumen yang lebih kaya. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat dan membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Menyimpan HTML di C# – Panduan Lengkap Menggunakan Penangan Sumber Daya Kustom](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Buat HTML dari String di C# – Panduan Penangan Sumber Daya Kustom](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Buat Dokumen HTML dengan Aspose.HTML – Panduan Langkah‑per‑Langkah](/html/english/net/html-document-manipulation/create-html-document-with-aspose-html-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
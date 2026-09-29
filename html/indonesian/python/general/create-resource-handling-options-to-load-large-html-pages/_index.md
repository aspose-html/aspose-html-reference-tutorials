---
category: general
date: 2026-09-29
description: Buat opsi penanganan sumber daya untuk memuat file halaman HTML besar
  secara efisien sambil mengontrol kedalaman dan penggunaan memori.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- load large html page
- HTML document parsing
- limit resource depth
- memory‑efficient HTML loading
language: id
lastmod: 2026-09-29
og_description: Buat opsi penanganan sumber daya untuk memuat halaman HTML besar dengan
  cepat sambil mencegah konsumsi sumber daya yang berlebihan dan menjaga kedalaman
  parsing tetap terkendali.
og_image_alt: Screenshot showing resource handling options configuration for loading
  a large HTML page
og_title: Buat opsi penanganan sumber daya – muat halaman HTML besar secara efisien
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Create resource handling options to efficiently load large HTML page
    files while controlling depth and memory usage.
  headline: Create resource handling options to load large HTML pages
  type: TechArticle
tags:
- HTML
- resource handling
- performance
title: Buat opsi penanganan sumber daya untuk memuat halaman HTML besar
url: /id/python/general/create-resource-handling-options-to-load-large-html-pages/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat opsi penanganan sumber daya untuk memuat halaman HTML besar

Jika Anda perlu **membuat opsi penanganan sumber daya** untuk file HTML yang sangat besar, panduan ini menunjukkan secara tepat cara menyiapkannya dan kemudian **memuat konten halaman HTML besar** dengan aman. Halaman besar sering berisi skrip, gambar, atau sumber daya eksternal yang bersarang dalam‑dalam yang dapat menyebabkan parser melakukan rekursi tanpa batas. Dengan membatasi kedalaman pemuatan otomatis, Anda menjaga penggunaan memori tetap dapat diprediksi dan menghindari timeout.

Pada bagian berikut Anda akan mempelajari cara:

* mengonfigurasi sebuah instance `ResourceHandlingOptions`,
* menerapkan konfigurasi tersebut saat membuka file dengan `HTMLDocument`,
* menangani kasus tepi umum seperti file yang hilang atau sumber daya yang melebihi kedalaman.

Tutorial ini mengasumsikan Anda sudah memiliki pustaka yang menyediakan `HTMLDocument` dan `ResourceHandlingOptions` (misalnya paket *HtmlParser*) yang terpasang di lingkungan Python Anda.

## Apa yang Anda perlukan

* Python 3.9 atau lebih baru  
* `htmlparser` (atau pustaka setara yang mendefinisikan `HTMLDocument` dan `ResourceHandlingOptions`)  
* Sebuah file HTML besar yang ingin Anda proses – contoh menggunakan `big_page.html` yang ditempatkan di folder `YOUR_DIRECTORY`.

Anda dapat menginstal paket yang diperlukan dengan:

```bash
pip install htmlparser
```

## Buat opsi penanganan sumber daya

Langkah pertama adalah **membuat opsi penanganan sumber daya** yang membatasi seberapa dalam parser akan mengikuti pemuatan sumber daya otomatis (skrip, iframe, impor CSS, dll.). Menetapkan `max_handling_depth` ke angka rendah mencegah parser mengejar rantai aset eksternal yang tak berujung.

```python
# Step 1: Create resource handling options and limit automatic loading depth
from htmlparser import ResourceHandlingOptions

# Instantiate the options object
res_opts = ResourceHandlingOptions()

# Restrict the parser to three levels of automatic resource handling
# This value balances completeness with performance for most large pages
res_opts.max_handling_depth = 3
```

**Mengapa ini penting:**  
Ketika sebuah halaman menyertakan banyak sumber daya bersarang, setiap tingkat tambahan menggandakan jumlah data yang harus diambil parser. Dengan membatasi kedalaman, Anda memastikan operasi tetap berada dalam batas memori dan waktu yang dapat diterima, yang sangat penting saat Anda **memuat file halaman HTML besar** pada server dengan sumber daya terbatas.

## Memuat halaman HTML besar secara efisien

Setelah objek opsi siap, berikan ke konstruktor `HTMLDocument`. Parser akan menghormati batas kedalaman saat membaca file.

```python
# Step 2: Load the HTML document using the configured options
from htmlparser import HTMLDocument

# Provide the path to your large HTML file and the previously defined options
doc = HTMLDocument(
    "YOUR_DIRECTORY/big_page.html",
    ResourceHandlingOptions=res_opts
)

# Verify that the document was loaded
print(f"Document title: {doc.title}")
print(f"Number of top‑level nodes: {len(doc.root.children)}")
```

**Mengapa ini berhasil:**  
`HTMLDocument` menerima argumen `ResourceHandlingOptions`, memungkinkan Anda menyuntikkan pembatasan kedalaman langsung ke dalam alur parsing. Pustaka kemudian membaca file, menerapkan batas tersebut, dan membangun pohon mirip DOM yang dapat Anda kueri.

### Variasi umum

| Variasi | Kapan digunakan | Perubahan kode |
|-----------|----------------|----------------|
| **Tingkatkan kedalaman** | Halaman mengandalkan inklusi bersarang dalam (mis., iframe berlapis). | `res_opts.max_handling_depth = 5` |
| **Nonaktifkan pemuatan otomatis** | Anda hanya membutuhkan HTML statis tanpa sumber daya eksternal. | `res_opts.max_handling_depth = 0` |
| **Timeout khusus** | Latensi jaringan untuk sumber daya eksternal menjadi perhatian. | `res_opts.resource_timeout = 10  # seconds` |

## Contoh lengkap dengan penanganan error

Berikut adalah skrip lengkap yang dapat dijalankan, yang membuat opsi, memuat file, dan menangani kegagalan umum secara elegan seperti file yang tidak ada atau sumber daya yang melebihi kedalaman.

```python
# complete_example.py
import os
from htmlparser import HTMLDocument, ResourceHandlingOptions, ResourceError

def load_large_html(path: str, max_depth: int = 3) -> HTMLDocument | None:
    """Create resource handling options and load a large HTML page safely."""
    if not os.path.isfile(path):
        print(f"Error: file not found → {path}")
        return None

    # Create and configure the options
    res_opts = ResourceHandlingOptions()
    res_opts.max_handling_depth = max_depth

    try:
        # Load the document with the configured options
        doc = HTMLDocument(path, ResourceHandlingOptions=res_opts)
        return doc
    except ResourceError as e:
        # This exception is raised when the parser exceeds the depth limit
        print(f"Resource handling error: {e}")
        return None
    except Exception as e:
        # Catch‑all for unexpected issues (e.g., malformed HTML)
        print(f"Unexpected error while loading HTML: {e}")
        return None


if __name__ == "__main__":
    html_path = "YOUR_DIRECTORY/big_page.html"
    document = load_large_html(html_path, max_depth=3)

    if document:
        print("✅ Document loaded successfully")
        print(f"Title: {document.title}")
        print(f"Root children count: {len(document.root.children)}")
    else:
        print("❌ Failed to load the HTML document")
```

**Output yang diharapkan** (dengan asumsi file ada dan terformat dengan baik):

```
✅ Document loaded successfully
Title: Example Large Page
Root children count: 42
```

Jika parser menemukan sumber daya yang akan mendorong kedalaman melewati `max_handling_depth`, blok `ResourceError` akan mencetak pesan yang jelas alih‑alih membuat program crash.

## Tips pro dan penanganan kasus tepi

* **Pantau memori** – Bahkan dengan batas kedalaman, halaman yang sangat besar dapat mengalokasikan RAM yang signifikan. Gunakan modul `tracemalloc` milik Python untuk memprofil memori jika Anda berencana memproses banyak file secara batch.
* **Validasi HTML sebelum parsing** – Menjalankan validator ringan (mis., `html5lib`) dapat menangkap tag yang tidak terstruktur dengan baik yang sebaliknya akan membuat parser membuat pohon yang terlalu dalam.
* **Pemrosesan paralel** – Saat Anda perlu **memuat file halaman HTML besar** secara bersamaan, bungkus `load_large_html` dalam thread pool tetapi tetap pertahankan `max_handling_depth` rendah untuk menghindari kontensi pada sumber daya jaringan.

## Kesimpulan

Anda kini tahu cara **membuat opsi penanganan sumber daya** dan menerapkannya untuk **memuat halaman HTML besar** secara terkendali dan efisien memori. Dengan mengonfigurasi `max_handling_depth` Anda mencegah pengambilan sumber daya yang tidak terkendali, dan contoh lengkap menunjukkan penanganan error yang kuat untuk skenario dunia nyata.

Selanjutnya, pertimbangkan untuk mengeksplorasi teknik **parsing dokumen HTML** seperti kueri XPath, selector CSS, atau parser streaming yang lebih jauh mengurangi tekanan memori saat menangani file yang sangat besar. Bereksperimenlah dengan nilai kedalaman dan pengaturan timeout yang berbeda untuk menemukan titik optimal bagi beban kerja spesifik Anda. Selamat parsing!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang dapat dijalankan dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Merender HTML – Panduan Lengkap dengan Penangan Sumber Daya Kustom](/html/english/net/rendering-html-documents/how-to-render-html-complete-guide-with-custom-resource-handl/)
- [Cara Menyimpan HTML di C# – Panduan Lengkap Menggunakan Penangan Sumber Daya Kustom](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Penangan Sumber Daya Kustom di Aspose HTML – Panduan Simpan ke Stream](/html/english/net/advanced-features/custom-resource-handler-in-aspose-html-save-to-stream-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
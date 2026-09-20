---
category: general
date: 2026-09-19
description: Pelajari cara membatasi sumber daya bersarang di Aspose.HTML untuk Python
  menggunakan ResourceHandlingOptions. Kendalikan kedalaman penanganan maksimum dan
  hindari loop tak terbatas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- limit nested resources
- resource handling options
- Aspose HTML Python
- max handling depth
- nested resource handling
language: id
lastmod: 2026-09-19
og_description: Batasi sumber daya bersarang di Aspose.HTML untuk Python menggunakan
  ResourceHandlingOptions. Atur kedalaman penanganan maksimum untuk mencegah rekursi
  yang dalam dan meningkatkan kinerja.
og_image_alt: Screenshot of Python code that limits nested resources with Aspose.HTML
og_title: Cara membatasi sumber daya bersarang di Aspose.HTML untuk Python – panduan
  langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-09-19'
  description: Learn how to limit nested resources in Aspose.HTML for Python using
    ResourceHandlingOptions. Control max handling depth and avoid infinite loops.
  headline: How to limit nested resources when processing HTML with Aspose.HTML for
    Python
  type: TechArticle
- description: Learn how to limit nested resources in Aspose.HTML for Python using
    ResourceHandlingOptions. Control max handling depth and avoid infinite loops.
  name: How to limit nested resources when processing HTML with Aspose.HTML for Python
  steps:
  - name: Explanation of each step
    text: 1. **Install the package** – The `aspose-html` wheel is required. The `pip
      install` command is shown as a comment for completeness. 2. **Import classes**
      – `HtmlDocument` loads the page, `ResourceHandlingOptions` holds the limit,
      and `HtmlLoadOptions` ties the two together. 3. **Create the options o
  - name: Changing the depth limit
    text: 'You might need a deeper or shallower limit based on your environment:'
  - name: Disabling the limit completely
    text: 'Setting the property to `0` tells Aspose.HTML to **remove any depth restriction**:'
  - name: Handling circular references
    text: 'Even with a depth limit, circular references can still appear at the same
      level. Aspose.HTML detects cycles and stops loading a resource that has already
      been processed, regardless of the depth setting. However, setting a lower `max_handling_depth`
      reduces the chance of hitting a cycle in the first '
  - name: Using the limit with local files
    text: 'The same approach works for local HTML files:'
  - name: Integrating with other Aspose.HTML features
    text: 'If you also need to control **resource download timeout**, you can combine
      `ResourceHandlingOptions` with `NetworkOptions`:'
  type: HowTo
tags:
- Aspose
- Python
- HTML processing
- Resource management
title: Cara membatasi sumber daya bersarang saat memproses HTML dengan Aspose.HTML
  untuk Python
url: /id/python/general/how-to-limit-nested-resources-when-processing-html-with-aspo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membatasi sumber daya bersarang saat memproses HTML dengan Aspose.HTML untuk Python

Jika Anda perlu **membatasi sumber daya bersarang** saat merender atau mengonversi HTML, panduan ini menunjukkan langkah‑langkah tepat untuk mengonfigurasi Aspose.HTML untuk Python. Mengontrol kedalaman penanganan sumber daya mencegah rekursi tak terkendali ketika sebuah halaman menyertakan banyak lapisan CSS, JavaScript, atau referensi gambar.

Membatasi sumber daya bersarang terutama penting untuk perayap berskala besar, pipeline rendering email, atau alur kerja otomatis apa pun yang harus tetap dalam batas memori dan waktu. Pada bagian berikut Anda akan mempelajari mengapa harus menetapkan batas kedalaman, cara menggunakan kelas `ResourceHandlingOptions`, dan cara memverifikasi bahwa batas tersebut berfungsi sebagaimana mestinya.

## Mengapa Anda harus membatasi sumber daya bersarang

Dokumen HTML sering merujuk ke sumber daya lain—lembar gaya, skrip, gambar, font, atau bahkan file HTML lainnya. Setiap sumber daya tersebut dapat, pada gilirannya, merujuk ke file tambahan, membentuk pohon ketergantungan. Tanpa pengaman, pohon tersebut dapat menjadi sangat dalam secara tak terbatas:

* Sebuah halaman memuat file CSS yang mengimpor file CSS lain, yang mengimpor lagi, dan seterusnya.
* JavaScript dapat memuat skrip tambahan secara dinamis.
* Template email dapat menyematkan gambar yang merujuk ke URL eksternal yang mengarahkan ke aset lain.

Ketika kedalaman rekursi tumbuh tanpa kontrol, Anda berisiko:

* **Konsumsi memori berlebihan** – setiap sumber daya yang diambil menempati buffer.
* **Waktu pemrosesan lebih lama** – latensi jaringan berlipat ganda pada setiap level.
* **Kemungkinan loop tak berujung** – referensi sirkular dapat menyebabkan mesin tidak pernah kembali.

Menetapkan **kedalaman penanganan maksimum** memberi tahu Aspose.HTML untuk berhenti mengikuti tautan sumber daya setelah sejumlah level tertentu, memastikan kinerja yang dapat diprediksi.

## Cara membatasi sumber daya bersarang di Aspose.HTML untuk Python

Aspose.HTML menyediakan kelas `ResourceHandlingOptions`, yang berisi properti `max_handling_depth`. Dengan menetapkan nilai numerik (misalnya `3`), Anda memberi instruksi kepada mesin untuk berhenti setelah tiga level bersarang.

Berikut adalah contoh lengkap yang dapat dijalankan yang menunjukkan seluruh alur kerja:

```python
# ---------------------------------------------------------
# Step 0: Install the Aspose.HTML package (if not already)
# ---------------------------------------------------------
# pip install aspose-html

# ---------------------------------------------------------
# Step 1: Import the required classes
# ---------------------------------------------------------
from aspose.html import HtmlDocument, ResourceHandlingOptions, HtmlLoadOptions

# ---------------------------------------------------------
# Step 2: Create a ResourceHandlingOptions instance
# ---------------------------------------------------------
resource_options = ResourceHandlingOptions()
# Limit the handling depth to three levels of nested resources
resource_options.max_handling_depth = 3

# ---------------------------------------------------------
# Step 3: Attach the options to the HTML load configuration
# ---------------------------------------------------------
load_options = HtmlLoadOptions()
load_options.resource_handling_options = resource_options

# ---------------------------------------------------------
# Step 4: Load an HTML page using the configured options
# ---------------------------------------------------------
# Replace the URL with any page that has deep resource nesting
html_url = "https://example.com/deep-nested.html"
document = HtmlDocument(html_url, load_options)

# ---------------------------------------------------------
# Step 5: Verify the depth limit worked
# ---------------------------------------------------------
# The Document object exposes a collection of loaded resources.
# We'll print the total number of resources and the deepest level reached.
print(f"Total resources loaded: {len(document.resources)}")
deepest_level = max((res.depth for res in document.resources), default=0)
print(f"Deepest resource level: {deepest_level}")

# ---------------------------------------------------------
# Step 6: (Optional) Save the processed HTML to disk
# ---------------------------------------------------------
output_path = "output_limited.html"
document.save(output_path)
print(f"Processed HTML saved to {output_path}")
```

### Penjelasan setiap langkah

1. **Instal paket** – Wheel `aspose-html` diperlukan. Perintah `pip install` ditampilkan sebagai komentar untuk melengkapi.
2. **Impor kelas** – `HtmlDocument` memuat halaman, `ResourceHandlingOptions` menyimpan batas, dan `HtmlLoadOptions` menghubungkan keduanya.
3. **Buat objek opsi** – Menginstansiasi `ResourceHandlingOptions` memberi Anda wadah yang dapat diubah.
4. **Setel `max_handling_depth`** – Tetapkan `3` (atau integer lain) untuk membatasi mesin pada tiga level sumber daya bersarang. Ini adalah inti dari **membatasi sumber daya bersarang**.
5. **Lampirkan opsi ke konfigurasi pemuatan** – `HtmlLoadOptions` memungkinkan Anda mengirim `resource_options` ke loader.
6. **Muat HTML** – Konstruktor `HtmlDocument` menerima URL atau jalur file bersama `load_options`. Mesin kini menghormati batas kedalaman.
7. **Verifikasi** – Dengan mengiterasi `document.resources`, Anda dapat melihat berapa banyak sumber daya yang sebenarnya diambil dan level terdalam yang ditemui. Jika level terdalam adalah `3` atau lebih rendah, batas berhasil.
8. **Simpan** – Simpan dokumen yang telah diproses. File yang disimpan hanya berisi sumber daya hingga kedalaman yang diizinkan.

#### Output yang diharapkan

```
Total resources loaded: 12
Deepest resource level: 3
Processed HTML saved to output_limited.html
```

Angka-angka akan bervariasi tergantung pada halaman sumber, tetapi level terdalam tidak boleh melebihi `3` karena kami menetapkan `max_handling_depth = 3`.

## Variasi umum dan kasus tepi

### Mengubah batas kedalaman

Anda mungkin memerlukan batas yang lebih dalam atau lebih dangkal tergantung pada lingkungan Anda:

```python
resource_options.max_handling_depth = 1   # Only top‑level resources (e.g., images directly referenced)
resource_options.max_handling_depth = 5   # Allow deeper CSS imports but still guard against runaway recursion
```

### Menonaktifkan batas sepenuhnya

Menetapkan properti ke `0` memberi tahu Aspose.HTML untuk **menghapus semua pembatasan kedalaman**:

```python
resource_options.max_handling_depth = 0   # No limit – use with caution
```

Lakukan ini hanya ketika Anda yakin HTML sumber berperilaku baik.

### Menangani referensi sirkular

Bahkan dengan batas kedalaman, referensi sirkular masih dapat muncul pada level yang sama. Aspose.HTML mendeteksi siklus dan menghentikan pemuatan sumber daya yang sudah diproses, terlepas dari pengaturan kedalaman. Namun, menetapkan `max_handling_depth` yang lebih rendah mengurangi kemungkinan menemukan siklus sejak awal.

### Menggunakan batas dengan file lokal

Pendekatan yang sama berlaku untuk file HTML lokal:

```python
document = HtmlDocument("C:/myproject/templates/email.html", load_options)
```

Mesin memperlakukan atribut `href` atau `src` relatif dengan cara yang sama seperti URL remote, menerapkan batas kedalaman juga pada sumber daya sistem file.

### Mengintegrasikan dengan fitur Aspose.HTML lainnya

Jika Anda juga perlu mengontrol **batas waktu unduhan sumber daya**, Anda dapat menggabungkan `ResourceHandlingOptions` dengan `NetworkOptions`:

```python
from aspose.html import NetworkOptions

network_opts = NetworkOptions()
network_opts.timeout = 5000   # milliseconds
load_options.network_options = network_opts
```

Kedua opsi bersifat independen, sehingga Anda dapat menyetel kinerja dan keamanan secara bersamaan.

## Tips profesional untuk penggunaan produksi

* **Log pohon sumber daya** – Saat debugging, iterasi `document.resources` dan catat URL serta kedalaman setiap sumber daya. Ini membantu Anda memahami mengapa halaman tertentu melebihi harapan.
* **Cache sumber daya yang diambil** – Jika Anda memproses aset eksternal yang sama berulang kali, aktifkan caching untuk menghindari panggilan jaringan yang berulang.
* **Gabungkan dengan whitelist** – Jika hanya domain tertentu yang dipercaya, filter `document.resources` setelah pemuatan dan buang yang berada di luar whitelist.
* **Uji dengan halaman kasus tepi** – Buat file HTML sintetis yang mengimpor rangkaian 10 file CSS. Verifikasi bahwa batas Anda memotong rangkaian tersebut sesuai yang diharapkan.

## Kesimpulan

Anda kini mengetahui cara **membatasi sumber daya bersarang** di Aspose.HTML untuk Python dengan mengonfigurasi `ResourceHandlingOptions.max_handling_depth`. Menetapkan batas kedalaman melindungi aplikasi Anda dari penggunaan memori berlebihan, waktu pemrosesan yang lama, dan potensi loop tak berujung yang disebabkan oleh referensi sumber daya yang sangat bersarang atau sirkular.

Dari titik ini Anda dapat:

* Menyesuaikan kedalaman agar sesuai dengan anggaran kinerja Anda (`resource_handling_options.max_handling_depth`).
* Menggabungkan batas dengan batas waktu jaringan, caching, atau whitelist domain untuk pipeline yang kuat.
* Menjelajahi topik terkait seperti **resource handling options**, **max handling depth**, dan **nested resource handling** untuk lebih memperketat kontrol atas pemrosesan HTML.

Cobalah nilai kedalaman yang berbeda dan amati bagaimana jumlah sumber daya yang dimuat berubah. Saat Anda siap, integrasikan pola ini ke dalam layanan konversi atau rendering HTML yang lebih besar untuk memastikan eksekusi yang dapat diprediksi, aman, dan efisien.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Message Handling and Networking in Aspose.HTML for Java](/html/english/java/message-handling-networking/)
- [Custom Schema Filter and Message Handling in Aspose.HTML for Java](/html/english/java/custom-schema-message-handling/)
- [Data Handling and Stream Management in Aspose.HTML for Java](/html/english/java/data-handling-stream-management/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
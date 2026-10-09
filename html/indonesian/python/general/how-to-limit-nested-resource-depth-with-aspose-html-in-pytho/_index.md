---
category: general
date: 2026-10-09
description: Pelajari cara membatasi kedalaman sumber daya bersarang menggunakan Aspose.HTML
  ResourceHandlingOptions di Python. Kendalikan max_handling_depth untuk konversi
  HTML yang aman.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- limit nested resource depth
- Aspose.HTML ResourceHandlingOptions
- Python resource handling
- max_handling_depth
- nested HTML resources
language: id
lastmod: 2026-10-09
og_description: Batasi kedalaman sumber daya bersarang menggunakan Aspose.HTML ResourceHandlingOptions
  di Python. Atur max_handling_depth untuk melindungi alur kerja konversi HTML Anda.
og_image_alt: Screenshot showing limit nested resource depth setting in Python
og_title: Cara membatasi kedalaman sumber daya bersarang dengan Aspose.HTML di Python
schemas:
- author: Aspose
  dateModified: '2026-10-09'
  description: Learn to limit nested resource depth using Aspose.HTML ResourceHandlingOptions
    in Python. Control max_handling_depth for safe HTML conversion.
  headline: How to limit nested resource depth with Aspose.HTML in Python
  type: TechArticle
- description: Learn to limit nested resource depth using Aspose.HTML ResourceHandlingOptions
    in Python. Control max_handling_depth for safe HTML conversion.
  name: How to limit nested resource depth with Aspose.HTML in Python
  steps:
  - name: What the setting does
    text: '- **Depth 0** – The root HTML document is processed, but no external resources
      are fetched. - **Depth 1** – Direct resources referenced by the root (e.g.,
      `<img src="...">`, `<link href="...">`) are fetched. - **Depth 2** – Resources
      referenced by the first‑level resources (e.g., CSS files that impo'
  - name: Using the options with a converter
    text: After configuring the depth limit, pass the `resource_options` object to
      the `HtmlConverter` (or any Aspose.HTML API that accepts `ResourceHandlingOptions`).
  - name: 1. Disabling depth limiting entirely
    text: Set the property to a very high number (e.g., `sys.maxsize`) or `None` if
      you want unrestricted handling. Use this only when you trust the source HTML.
  - name: 2. Handling missing resources
    text: When the depth limit stops a resource from being fetched, Aspose.HTML logs
      a warning but continues. You can capture these warnings by attaching a custom
      logger to the converter if you need audit trails.
  - name: 3. Combining with other resource options
    text: '`ResourceHandlingOptions` also offers `allow_external_resources`, `download_timeout`,
      and `max_resource_size`. Pairing a depth limit with a size limit provides a
      robust safety net.'
  - name: 4. Testing the limit
    text: Create a test HTML hierarchy with nested `<iframe>` tags or CSS `@import`
      statements to verify that your depth limit behaves as expected before deploying
      to production.
  type: HowTo
tags:
- Aspose.HTML
- Python
- HTML conversion
- Resource handling
title: Cara membatasi kedalaman sumber daya bersarang dengan Aspose.HTML di Python
url: /id/python/general/how-to-limit-nested-resource-depth-with-aspose-html-in-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membatasi kedalaman sumber daya bersarang dengan Aspose.HTML di Python

Jika Anda perlu **membatasi kedalaman sumber daya bersarang** saat mengonversi HTML dengan Aspose.HTML, panduan ini menunjukkan secara tepat cara melakukannya di Python. Mengontrol properti `max_handling_depth` mencegah rekursi tak terkendali ketika sebuah halaman menyertakan sumber daya yang sangat bersarang seperti frame atau stylesheet yang ditautkan.

Anda juga akan mempelajari mengapa menetapkan batas kedalaman penting, melihat contoh kode lengkap, serta menemukan jebakan umum dan tip praktik terbaik. Tidak diperlukan dokumentasi eksternal—semua yang Anda butuhkan ada di sini.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

- Python 3.8 atau yang lebih baru terpasang  
- Paket `aspose.html` (`pip install aspose-html`)  
- Familiaritas dasar dengan alur kerja konversi Aspose.HTML  

Item‑item ini adalah satu‑satunya ketergantungan untuk contoh di bawah ini.

## Langkah 1: Impor kelas **ResourceHandlingOptions**

Langkah pertama adalah membawa kelas `ResourceHandlingOptions` ke dalam skrip Anda. Kelas ini mengelompokkan semua opsi yang memengaruhi cara sumber daya eksternal (gambar, CSS, skrip, dll.) diambil dan diproses selama konversi.

```python
# Step 1: Import the ResourceHandlingOptions class
from aspose.html import ResourceHandlingOptions
```

**Mengapa ini penting:**  
`ResourceHandlingOptions` memisahkan pengaturan yang berhubungan dengan sumber daya dari opsi konversi lainnya, memungkinkan Anda menyesuaikan cara penanganan sumber daya bersarang tanpa memengaruhi rendering atau format output.

## Langkah 2: Buat instance objek opsi

Instansiasi `ResourceHandlingOptions` sehingga Anda dapat memodifikasi propertinya. Instance default mengizinkan penelusuran tak terbatas, yang dapat menyebabkan masalah kinerja atau bahkan overflow stack pada halaman yang dirancang secara jahat.

```python
# Step 2: Create an instance of the options object
resource_options = ResourceHandlingOptions()
```

**Tip profesional:**  
Jika Anda berencana menggunakan batas kedalaman yang sama pada banyak konversi, simpan objek yang telah dikonfigurasi dalam variabel tingkat modul untuk menghindari pembuatan ulang setiap kali.

## Langkah 3: Atur **max_handling_depth** untuk membatasi kedalaman sumber daya bersarang

Tetapkan properti `max_handling_depth` ke jumlah maksimum tingkat bersarang yang ingin Anda izinkan. Pada contoh ini kami menghentikan setelah **3** tingkat, tetapi Anda dapat memilih bilangan bulat apa pun yang sesuai dengan skenario Anda.

```python
# Step 3: Limit the depth of nested resource handling (stop after 3 levels)
resource_options.max_handling_depth = 3
```

### Apa yang dilakukan pengaturan ini

- **Depth 0** – Dokumen HTML akar diproses, tetapi tidak ada sumber daya eksternal yang diambil.  
- **Depth 1** – Sumber daya langsung yang direferensikan oleh akar (misalnya `<img src="...">`, `<link href="...">`) diambil.  
- **Depth 2** – Sumber daya yang direferensikan oleh sumber daya tingkat pertama (misalnya file CSS yang meng‑import CSS lain) diambil.  
- **Depth 3** – Proses berhenti setelah menangani sumber daya tingkat ketiga. Referensi bersarang lebih lanjut diabaikan.

Menetapkan `max_handling_depth` melindungi aplikasi Anda dari:

| Risiko | Bagaimana batas membantu |
|------|----------------------|
| **Rekursi tak terbatas** yang disebabkan oleh referensi melingkar | Konverter berhenti setelah kedalaman yang ditentukan, memutuskan loop. |
| **Lalu lintas jaringan berlebihan** ketika sebuah halaman memuat puluhan stylesheet berantai | Hanya beberapa tingkat pertama yang diunduh, mengurangi penggunaan bandwidth. |
| **Kelebihan memori** akibat memuat pohon sumber daya yang sangat besar | Lebih sedikit objek yang dibuat, menjaga penggunaan memori tetap dapat diprediksi. |

### Menggunakan opsi dengan konverter

Setelah mengonfigurasi batas kedalaman, serahkan objek `resource_options` ke `HtmlConverter` (atau API Aspose.HTML mana pun yang menerima `ResourceHandlingOptions`).

```python
from aspose.html import HtmlConverter, SaveFormat

# Create a converter with the resource handling options
converter = HtmlConverter(resource_options)

# Convert a sample HTML file to PDF while respecting the depth limit
converter.convert("sample.html", "output.pdf", SaveFormat.PDF)

print("Conversion completed with max_handling_depth =", resource_options.max_handling_depth)
```

**Output yang diharapkan**

```
Conversion completed with max_handling_depth = 3
```

Jika HTML sumber berisi sumber daya di luar tingkat ketiga, mereka akan dihilangkan dari PDF, dan konversi tetap selesai dengan cepat.

## Kasus Tepi dan Variasi Umum

### 1. Menonaktifkan pembatasan kedalaman sepenuhnya

Setel properti ke angka yang sangat tinggi (misalnya `sys.maxsize`) atau `None` jika Anda menginginkan penanganan tanpa batas. Gunakan ini hanya ketika Anda mempercayai HTML sumber.

```python
import sys
resource_options.max_handling_depth = sys.maxsize  # effectively unlimited
```

### 2. Menangani sumber daya yang hilang

Ketika batas kedalaman menghentikan pengambilan sebuah sumber daya, Aspose.HTML mencatat peringatan tetapi tetap melanjutkan. Anda dapat menangkap peringatan ini dengan melampirkan logger khusus ke konverter jika memerlukan jejak audit.

### 3. Menggabungkan dengan opsi sumber daya lainnya

`ResourceHandlingOptions` juga menawarkan `allow_external_resources`, `download_timeout`, dan `max_resource_size`. Menggabungkan batas kedalaman dengan batas ukuran memberikan jaring pengaman yang kuat.

```python
resource_options.allow_external_resources = True
resource_options.max_resource_size = 5 * 1024 * 1024  # 5 MiB per resource
```

### 4. Menguji batas

Buat hierarki HTML uji dengan tag `<iframe>` bersarang atau pernyataan CSS `@import` untuk memverifikasi bahwa batas kedalaman Anda berfungsi sebagaimana mestinya sebelum diterapkan ke produksi.

## Tips Praktis (E‑E‑A‑T)

- **Validasi URL input** sebelum konversi untuk menghindari panggilan jaringan yang tidak perlu.  
- **Catat kedalaman aktual yang tercapai** (`converter.handling_depth_reached`) untuk pemantauan.  
- **Gunakan kembali `ResourceHandlingOptions` yang sama** pada beberapa konversi untuk menjaga konsistensi konfigurasi.  
- **Profil kinerja** saat mengubah kedalaman; batas yang lebih rendah biasanya mempercepat konversi tetapi dapat menghilangkan aset yang diperlukan.  

## Kesimpulan

Anda kini mengetahui cara **membatasi kedalaman sumber daya bersarang** saat bekerja dengan Aspose.HTML di Python dengan mengonfigurasi properti `max_handling_depth` pada `ResourceHandlingOptions`. Pengaturan tunggal ini melindungi pipeline konversi Anda dari rekursi tak terkendali, penggunaan jaringan berlebih, dan lonjakan memori sekaligus memberi Anda kontrol terperinci atas seberapa dalam pohon sumber daya diproses.

Siap menjelajah lebih jauh? Coba gabungkan batas kedalaman dengan `max_resource_size` untuk membuat alur kerja konversi HTML‑ke‑PDF yang sepenuhnya diperkuat, atau baca panduan kami tentang **penanganan sumber daya Aspose.HTML** untuk wawasan lebih dalam mengenai `allow_external_resources` dan manajemen timeout.

--- 

*Gambar yang menggambarkan pengaturan batas kedalaman (opsional):*  
![Screenshot menunjukkan pengaturan limit nested resource depth di Python](placeholder.png "limit nested resource depth")

## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Custom Resource Handler in Aspose HTML – Save to Stream Guide](/html/english/net/advanced-features/custom-resource-handler-in-aspose-html-save-to-stream-guide/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Message Handling and Networking in Aspose.HTML for Java](/html/english/java/message-handling-networking/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
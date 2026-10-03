---
category: general
date: 2026-10-02
description: Pelajari cara membuat dokumen SVG di Python, menyimpan SVG ke file, dan
  mengekspor gambar SVG dengan skrip singkat yang lengkap.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG to file
- how to generate SVG
- export SVG image
- SVG Python tutorial
language: id
lastmod: 2026-10-02
og_description: Buat dokumen SVG di Python dan ekspor gambar SVG dengan tutorial praktis
  ini. Ikuti skripnya, simpan SVG ke file, dan gunakan kembali grafik vektor secara
  instan.
og_image_alt: Screenshot of a Python script that creates an SVG document
og_title: Buat dokumen SVG di Python – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-10-02'
  description: Learn how to create SVG document in Python, save SVG to file, and export
    SVG image with a short, complete script.
  headline: How to create SVG document and export it as an image in Python
  type: TechArticle
tags:
- SVG
- Python
- graphics
title: Cara membuat dokumen SVG dan mengekspornya sebagai gambar di Python
url: /id/python/general/how-to-create-svg-document-and-export-it-as-an-image-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat dokumen SVG dan mengekspornya sebagai gambar di Python

Jika Anda perlu **membuat dokumen SVG** secara programatis, tutorial ini menunjukkan secara tepat cara melakukannya dengan Python. Anda akan melihat skrip lengkap yang membangun sebuah lingkaran sederhana, menyimpan SVG ke file, dan menghasilkan gambar SVG yang dapat diekspor dan disisipkan di mana saja.

Membuat grafik vektor skalabel dari kode menghilangkan upaya manual menggambar bentuk di editor GUI. Pada akhir panduan ini Anda dapat mengintegrasikan pembuatan SVG ke dalam pipeline visualisasi data, generator laporan otomatis, atau proyek apa pun yang memerlukan grafik tajam dan independen resolusi.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

- Python 3.8 atau lebih baru terpasang
- Library `svgwrite` (pasang dengan `pip install svgwrite`)
- Izin menulis ke direktori tempat SVG akan disimpan

Persyaratan ini menjaga contoh tetap ringan dan kompatibel dengan sebagian besar lingkungan.

## Langkah 1: Instal dan impor library SVG

Langkah pertama adalah menambahkan library pihak ketiga yang menyediakan API nyaman untuk pembuatan SVG.

```python
# Install the library (run once in your terminal)
# pip install svgwrite

import svgwrite  # Provides the SVGDocument class and element helpers
```

`svgwrite` mengabstraksi struktur XML dari file SVG, memungkinkan Anda fokus pada geometri alih-alih markup mentah.

## Langkah 2: Buat objek dokumen SVG

Sekarang Anda dapat **membuat dokumen SVG** dengan menginstansiasi `svgwrite.Drawing`. Objek ini mewakili elemen root `<svg>` dan menampung semua bentuk selanjutnya.

```python
# Step 2: Initialize the SVG document
dwg = svgwrite.Drawing(
    filename="circle.svg",     # Desired output file name
    size=("100px", "100px"),   # Width and height of the canvas
    viewBox=("0 0 100 100")    # Coordinate system for drawing
)
```

Argumen `size` menentukan dimensi piksel yang dirender, sementara `viewBox` menetapkan sistem koordinat yang cocok dengan geometri yang akan Anda definisikan nanti.

## Langkah 3: Tambahkan elemen lingkaran

Sebuah lingkaran didefinisikan oleh pusatnya (`cx`, `cy`) dan jari‑jari (`r`). Gunakan helper `circle` untuk melampirkan atribut‑atribut ini.

```python
# Step 3: Create a <circle> element
circle = dwg.circle(
    center=("50", "50"),   # cx = 50, cy = 50
    r="40",                # radius = 40
    fill="lightcoral",     # Fill color for visual clarity
    stroke="black",        # Outline color
    stroke_width="2"
)

# Append the circle to the SVG root
dwg.add(circle)
```

Lingkaran berada di tengah kanvas 100 × 100, meninggalkan margin 10 piksel di setiap sisi. Sesuaikan `fill` dan `stroke` agar sesuai dengan bahasa desain Anda.

## Langkah 4: Simpan SVG ke file

Setelah grafik selesai dirakit, Anda dapat **menyimpan SVG ke file** menggunakan metode `save`. Ini menulis XML yang terstruktur dengan baik yang dapat dipahami oleh peramban dan editor vektor.

```python
# Step 4: Persist the SVG document
dwg.save()
print("SVG file saved as circle.svg")
```

File `circle.svg` kini berada di direktori kerja saat ini. Anda dapat membukanya di peramban web, Inkscape, atau alat apa pun yang mendukung format SVG.

## Langkah 5: Verifikasi gambar SVG yang diekspor

Buka file yang disimpan di peramban untuk memastikan outputnya. Anda seharusnya melihat lingkaran terpusat dengan warna yang telah ditentukan. XML mentahnya terlihat seperti ini:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg width="100px" height="100px" viewBox="0 0 100 100"
     xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40"
          fill="lightcoral" stroke="black" stroke-width="2"/>
</svg>
```

Karena SVG berbasis vektor, Anda dapat memperbesar gambar tanpa kehilangan kualitas, menjadikannya ideal untuk desain web responsif atau cetakan resolusi tinggi.

## Tips pro: Ekspor SVG sebagai PNG atau JPEG

Jika Anda memerlukan versi raster, gabungkan file SVG dengan alat konversi seperti **CairoSVG**:

```python
# Optional: Convert SVG to PNG
# pip install cairosvg
import cairosvg

cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

Langkah ini memperlihatkan **mengekspor gambar SVG** ke format bitmap, berguna ketika sistem hilir tidak dapat merender SVG secara langsung.

## Variasi umum dan kasus tepi

| Variasi | Cara menangani |
|-----------|---------------|
| Banyak bentuk | Panggil `dwg.add()` untuk setiap elemen baru (rect, line, path). |
| Dimensi dinamis | Hitung `size` dan `viewBox` dari data sebelum membuat `Drawing`. |
| Label teks | Gunakan `dwg.text("Label", insert=("10", "20"))` dan stilkan dengan `font_size` serta `fill`. |
| Menggunakan kembali dokumen | Simpan objek `Drawing` di memori dan panggil `save()` kapanpun Anda membutuhkan file yang diperbarui. |
| File besar | Alirkan output menggunakan `dwg.tostring()` dan tulis ke objek file secara manual untuk menghindari lonjakan memori. |

Menangani skenario‑skenario ini memastikan skrip **cara menghasilkan SVG** Anda dapat diskalakan dari ikon sederhana hingga diagram kompleks.

## Rekap skrip lengkap

Berikut contoh lengkap yang dapat dijalankan dan mencakup semua langkah serta konversi opsional:

```python
# Full SVG creation script – create SVG document, save SVG to file, export SVG image
import svgwrite
import cairosvg  # Optional, only needed for PNG conversion

# Initialize the drawing (SVG document)
dwg = svgwrite.Drawing(
    filename="circle.svg",
    size=("100px", "100px"),
    viewBox=("0 0 100 100")
)

# Define a circle element
circle = dwg.circle(
    center=("50", "50"),
    r="40",
    fill="lightcoral",
    stroke="black",
    stroke_width="2"
)

# Add the circle to the document
dwg.add(circle)

# Save the SVG file
dwg.save()
print("SVG file saved as circle.svg")

# Optional: convert SVG to PNG (export SVG image)
cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

Menjalankan skrip ini menghasilkan `circle.svg` dan, jika `cairosvg` terpasang, `circle.png`. Kedua file siap disertakan dalam halaman web, laporan, atau proses lanjutan lainnya.

## Kesimpulan

Anda kini tahu cara **membuat dokumen SVG** di Python, **menyimpan SVG ke file**, dan **mengekspor gambar SVG** untuk penggunaan yang lebih luas. Contoh ini mencakup panggilan API penting, menjelaskan mengapa setiap langkah penting, serta menawarkan ekstensi untuk grafik yang lebih kompleks.

Selanjutnya, jelajahi topik **tutorial SVG Python** tambahan seperti menggambar path, menerapkan gradien, dan menganimasikan elemen. Mengintegrasikan teknik‑teknik ini akan memungkinkan Anda menghasilkan grafik vektor dinamis yang didorong data langsung dari aplikasi Python Anda. Selamat coding!


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang dapat dijalankan dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Buat dan Kelola Dokumen SVG di Aspose.HTML untuk Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [Simpan Dokumen SVG di Aspose.HTML untuk Java](/html/english/java/saving-html-documents/save-svg-document/)
- [svg to png java – Konversi SVG ke Gambar dengan Aspose.HTML untuk Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
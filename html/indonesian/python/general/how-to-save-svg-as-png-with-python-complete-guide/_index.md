---
category: general
date: 2026-09-29
description: Cara menyimpan SVG menggunakan Python dan mengekspor SVG ke PNG. Pelajari
  cara mengonversi SVG ke PNG dengan opsi yang disesuaikan dalam hitungan menit.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save svg
- convert svg to png
- save svg as png
- export svg to png
- vector svg to png
language: id
lastmod: 2026-09-29
og_description: Cara menyimpan SVG menggunakan Python dan mengekspor SVG ke PNG. Ikuti
  panduan ini untuk mengonversi SVG ke PNG dengan kontrol penuh atas opsi.
og_image_alt: Screenshot of Python code converting a vector SVG file to a PNG image
og_title: Cara menyimpan SVG sebagai PNG dengan Python – langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: How to save SVG using Python and export SVG to PNG. Learn to convert
    SVG to PNG with fine‑tuned options in minutes.
  headline: How to save SVG as PNG with Python – complete guide
  type: TechArticle
- description: How to save SVG using Python and export SVG to PNG. Learn to convert
    SVG to PNG with fine‑tuned options in minutes.
  name: How to save SVG as PNG with Python – complete guide
  steps:
  - name: Load the SVG document
    text: '```python from aspose.svg import SVGDocument'
  - name: (Optional) Create image‑save options
    text: '```python from aspose.svg import ImageSaveOptions'
  - name: Save the SVG as PNG
    text: '```python # Export the SVG to a PNG file using the options defined above
      svg_doc.save("YOUR_DIRECTORY/vector.png", options) ```'
  - name: Full script
    text: 'Putting the pieces together yields a complete, runnable program:'
  - name: Missing file or invalid path
    text: 'If `src_path` does not exist, `SVGDocument` raises a `FileNotFoundError`.
      Wrap the call in a `try/except` block to provide a friendly error message:'
  - name: Preserving aspect ratio
    text: When only one dimension (width **or** height) is set, the library automatically
      scales the other dimension to maintain the original aspect ratio. If you set
      both dimensions, the image may stretch. Choose the approach that matches your
      UI requirements.
  - name: Transparent backgrounds
    text: 'If the original SVG relies on transparency (e.g., icons), you can keep
      the PNG transparent by omitting `background_color`:'
  type: HowTo
tags:
- Python
- SVG
- Image conversion
title: Cara menyimpan SVG sebagai PNG dengan Python – panduan lengkap
url: /id/python/general/how-to-save-svg-as-png-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyimpan SVG sebagai PNG dengan Python – panduan lengkap

Jika Anda perlu **menyimpan SVG** sebagai gambar raster, tutorial ini menunjukkan solusi siap‑jalankan. Anda akan belajar cara memuat file SVG vektor, secara opsional menyesuaikan pengaturan penyimpanan gambar, dan mengekspor hasilnya ke PNG hanya dalam tiga baris kode.

Menyimpan file SVG sebagai PNG umum dilakukan ketika Anda ingin menyisipkan grafik di halaman web, membuat thumbnail, atau memasukkan gambar raster ke pipeline pembelajaran mesin. Pendekatan yang dijelaskan di sini bekerja di Windows, macOS, dan Linux tanpa ketergantungan native tambahan.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* Python 3.9 atau yang lebih baru terpasang
* Paket `aspose.svg` (Aspose SVG resmi untuk Python via .NET). Instal dengan:

```bash
pip install aspose-svg
```

* File SVG yang valid di disk (misalnya `vector.svg`)

Persyaratan ini menjaga contoh tetap mandiri dan menghindari alat eksternal seperti CairoSVG.

## Cara menyimpan SVG dengan Python

Inti proses ini terdiri dari tiga langkah: memuat, mengkonfigurasi, dan menyimpan. Bagian berikut memecah masing‑masing langkah.

### Langkah 1: Muat dokumen SVG

```python
from aspose.svg import SVGDocument

# Load the SVG file from the local filesystem
svg_doc = SVGDocument("YOUR_DIRECTORY/vector.svg")
```

`SVGDocument` mem-parsing XML SVG dan membangun representasi dalam memori. Memuat file terlebih dahulu wajib; jika tidak operasi penyimpanan tidak memiliki data sumber.

### Langkah 2: (Opsional) Buat opsi penyimpanan gambar

```python
from aspose.svg import ImageSaveOptions

# Create default options; you can tweak width, height, and background
options = ImageSaveOptions()
options.width = 800          # Desired output width in pixels
options.height = 600         # Desired output height in pixels
options.background_color = "#FFFFFF"  # Force a white background for transparent SVGs
```

`ImageSaveOptions` memungkinkan Anda menyesuaikan output PNG secara detail. Mengatur lebar dan tinggi mempertahankan rasio aspek kecuali Anda menetapkan keduanya secara eksplisit. Menetapkan warna latar belakang berguna ketika SVG asli memiliki transparansi tetapi Anda memerlukan PNG yang tidak tembus.

### Langkah 3: Simpan SVG sebagai PNG

```python
# Export the SVG to a PNG file using the options defined above
svg_doc.save("YOUR_DIRECTORY/vector.png", options)
```

Metode `save` menulis file PNG ke jalur target. Jika Anda mengabaikan argumen `options`, perpustakaan menggunakan dimensi default yang diambil dari viewBox SVG.

### Skrip lengkap

Menggabungkan semua bagian menghasilkan program lengkap yang dapat dijalankan:

```python
# -*- coding: utf-8 -*-
"""
How to save SVG as PNG with Python.
This script loads an SVG file, applies optional image‑save settings,
and exports the result to PNG.
"""

from aspose.svg import SVGDocument, ImageSaveOptions

def convert_svg_to_png(
    src_path: str,
    dst_path: str,
    width: int = 800,
    height: int = 600,
    background: str = "#FFFFFF"
) -> None:
    """Convert an SVG file to PNG with custom dimensions and background."""
    # Load the SVG document
    svg_doc = SVGDocument(src_path)

    # Prepare save options
    options = ImageSaveOptions()
    options.width = width
    options.height = height
    options.background_color = background

    # Save as PNG
    svg_doc.save(dst_path, options)


if __name__ == "__main__":
    # Example usage
    convert_svg_to_png(
        src_path="YOUR_DIRECTORY/vector.svg",
        dst_path="YOUR_DIRECTORY/vector.png",
        width=1024,
        height=768,
        background="#FFFFFF"
    )
    print("SVG successfully saved as PNG.")
```

Menjalankan skrip mencetak **“SVG berhasil disimpan sebagai PNG.”** dan membuat `vector.png` di folder yang sama.

## Mengonversi SVG ke PNG – menangani jebakan umum

### File tidak ada atau jalur tidak valid

Jika `src_path` tidak ada, `SVGDocument` akan mengeluarkan `FileNotFoundError`. Bungkus pemanggilan dalam blok `try/except` untuk memberikan pesan error yang ramah:

```python
try:
    svg_doc = SVGDocument(src_path)
except FileNotFoundError:
    raise SystemExit(f"File not found: {src_path}")
```

### Mempertahankan rasio aspek

Ketika hanya satu dimensi (lebar **atau** tinggi) yang diatur, perpustakaan secara otomatis menyesuaikan dimensi lainnya untuk mempertahankan rasio aspek asli. Jika Anda mengatur kedua dimensi, gambar dapat terdistorsi. Pilih pendekatan yang sesuai dengan kebutuhan UI Anda.

### Latar belakang transparan

Jika SVG asli mengandalkan transparansi (misalnya ikon), Anda dapat mempertahankan PNG transparan dengan menghilangkan `background_color`:

```python
options.background_color = None   # PNG will retain transparency
```

Variasi ini berguna ketika PNG akan ditumpuk di atas grafik lain.

## Mengekspor SVG ke PNG – tips kinerja

* **Gunakan kembali `ImageSaveOptions`** saat mengonversi banyak file secara batch. Membuat objek opsi baru untuk setiap file menambah overhead yang dapat diabaikan, tetapi penggunaan kembali menghindari alokasi memori berulang.
* **Pemrosesan batch**: Loop melalui direktori file SVG dan panggil `convert_svg_to_png` untuk masing‑masing. Perpustakaan memproses setiap file secara independen, sehingga Anda dapat memparalelkan loop dengan `concurrent.futures.ThreadPoolExecutor` untuk konversi lebih cepat pada mesin multi‑core.

```python
import os
from concurrent.futures import ThreadPoolExecutor

svg_folder = "YOUR_DIRECTORY"
png_folder = "YOUR_DIRECTORY/pngs"
os.makedirs(png_folder, exist_ok=True)

def batch_convert(file_name):
    src = os.path.join(svg_folder, file_name)
    dst = os.path.join(png_folder, file_name.replace('.svg', '.png'))
    convert_svg_to_png(src, dst)

with ThreadPoolExecutor(max_workers=8) as executor:
    executor.map(batch_convert, [f for f in os.listdir(svg_folder) if f.endswith('.svg')])
```

## Menyimpan SVG sebagai PNG – verifikasi

Setelah konversi, Anda dapat memverifikasi output secara programatis:

```python
from PIL import Image

with Image.open("YOUR_DIRECTORY/vector.png") as img:
    print(f"PNG size: {img.size}, mode: {img.mode}")
```

Output tipikal:

```
PNG size: (1024, 768), mode: RGBA
```

`mode` `RGBA` mengonfirmasi bahwa gambar mengandung kanal alfa (transparansi). Jika Anda menetapkan warna latar belakang, mode akan menjadi `RGB`.

## Kesimpulan

Anda kini tahu **cara menyimpan SVG** sebagai PNG menggunakan Python, **cara mengonversi SVG ke PNG**, dan **cara mengekspor SVG ke PNG** dengan dimensi khusus serta penanganan latar belakang. Skrip lengkap menunjukkan seluruh alur kerja mulai dari memuat file SVG vektor hingga menghasilkan gambar PNG raster.

Selanjutnya, jelajahi topik terkait seperti **menyimpan SVG sebagai PNG** dalam mode batch, menggunakan perpustakaan alternatif seperti **CairoSVG**, atau menghasilkan PDF multi‑halaman dari sumber SVG. Bereksperimenlah dengan berbagai pengaturan `ImageSaveOptions` untuk menyempurnakan kualitas, DPI, dan kompresi sesuai kebutuhan Anda.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [svg ke png java – Mengonversi SVG ke Gambar dengan Aspose.HTML untuk Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Menampilkan dokumen SVG sebagai PNG di .NET dengan Aspose.HTML](/html/hindi/net/rendering-html-documents/render-svg-doc-as-png/)
- [Cara Menetapkan DPI Saat Mengonversi SVG ke PNG dengan Java](/html/english/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-with-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
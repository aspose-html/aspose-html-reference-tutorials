---
category: general
date: 2026-10-25
description: Simpan SVG sebagai PNG dengan cepat menggunakan Python. Pelajari cara
  mengonversi SVG ke PNG, mengekspor SVG ke PNG, dan dapatkan kode SVG ke PNG siap
  pakai.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save svg as png
- convert svg to png
- how to convert svg
- export svg to png
- svg to png code
language: id
lastmod: 2026-10-25
og_description: simpan SVG sebagai PNG menggunakan Python. Tutorial ini menunjukkan
  cara mengonversi SVG ke PNG dengan kode yang jelas, opsi, dan tips pemecahan masalah.
og_image_alt: Diagram illustrating saving an SVG file as a PNG image with Python
og_title: Simpan SVG sebagai PNG di Python – panduan lengkap
schemas:
- author: Aspose
  dateModified: '2026-10-25'
  description: save SVG as PNG quickly with Python. Learn to convert SVG to PNG, export
    SVG to PNG, and get ready‑to‑use svg to png code.
  headline: How to save SVG as PNG in Python – step‑by‑step guide
  type: TechArticle
- description: save SVG as PNG quickly with Python. Learn to convert SVG to PNG, export
    SVG to PNG, and get ready‑to‑use svg to png code.
  name: How to save SVG as PNG in Python – step‑by‑step guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Reason | |------------|--------| | Python 3.8+ | Modern
      syntax and type hints. | | `aspose.svg` package (or any library that provides
      `SVGDocument` and `PngSaveOptions`) | Supplies the `SVGDocument` class used
      in the example. | | An SVG file you own or have permission to use | The so'
  - name: Load the SVG document
    text: '```python from aspose.svg import SVGDocument'
  - name: Convert SVG to PNG – create save options
    text: '```python from aspose.svg import PngSaveOptions'
  - name: Export SVG to PNG
    text: '```python # Destination file for the PNG image png_path = "YOUR_DIRECTORY/vector.png"
      svg_doc.save(png_path, png_options) ```'
  - name: Verify the output (optional but recommended)
    text: '```python from PIL import Image'
  type: HowTo
tags:
- SVG
- PNG
- Python
title: Cara menyimpan SVG sebagai PNG di Python – panduan langkah demi langkah
url: /id/python/general/how-to-save-svg-as-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyimpan SVG sebagai PNG di Python – panduan langkah demi langkah

Jika Anda perlu **menyimpan SVG sebagai PNG** dengan cepat, panduan ini memberikan solusi lengkap yang dapat dijalankan. Anda akan melihat cara **mengonversi SVG ke PNG**, mengatur parameter ekspor opsional, dan menjalankan skrip pada platform apa pun yang mendukung Python.  

Tutorial ini mencakup semua hal mulai dari menginstal pustaka yang diperlukan hingga memverifikasi gambar yang dihasilkan, sehingga Anda dapat menyalin‑tempel kode dan mendapatkan hasil secara langsung. Tidak diperlukan dokumentasi eksternal—cukup ikuti langkah‑langkah di bawah ini.

## Apa yang akan Anda pelajari

* Kode **svg to png** yang tepat yang Anda butuhkan untuk konversi satu baris.  
* Cara **mengekspor SVG ke PNG** dengan DPI khusus atau warna latar belakang.  
* Kesulitan umum saat mengonversi SVG kompleks dan cara menghindarinya.  
* Cara mengintegrasikan konversi ke dalam proyek Python yang lebih besar.

### Prasyarat

| Persyaratan | Alasan |
|------------|--------|
| Python 3.8+ | Sintaks modern dan petunjuk tipe. |
| `aspose.svg` package (or any library that provides `SVGDocument` and `PngSaveOptions`) | Menyediakan kelas `SVGDocument` yang digunakan dalam contoh. |
| An SVG file you own or have permission to use | Grafik vektor sumber. |

Instal pustaka dengan pip sebelum Anda memulai:

```bash
pip install aspose.svg
```

> **Pro tip:** Jika Anda lebih suka dependensi yang lebih ringan, `cairosvg` juga menyediakan `svg2png`, tetapi API yang ditampilkan di sini cocok dengan potongan kode asli dan berfungsi untuk SVG sederhana maupun kompleks.

## Cara menyimpan SVG sebagai PNG dengan Python

### Langkah 1: Muat dokumen SVG

```python
from aspose.svg import SVGDocument

# Replace the path with your actual SVG file location
svg_path = "YOUR_DIRECTORY/vector.svg"
svg_doc = SVGDocument(svg_path)
```

*Mengapa langkah ini penting* – Memuat file membuat representasi dalam memori yang dapat dimanipulasi oleh pustaka. Tanpa instance `SVGDocument` yang tepat, panggilan ekspor berikutnya akan gagal.

### Langkah 2: Konversi SVG ke PNG – buat opsi penyimpanan

```python
from aspose.svg import PngSaveOptions

# Default options work for most cases; you can customize them later
png_options = PngSaveOptions()
```

`PngSaveOptions` memungkinkan Anda mengontrol ukuran output, DPI, warna latar belakang, dan lainnya. Konfigurasi default mempertahankan dimensi SVG asli dan menghasilkan PNG lossless.

### Langkah 3: Ekspor SVG ke PNG

```python
# Destination file for the PNG image
png_path = "YOUR_DIRECTORY/vector.png"
svg_doc.save(png_path, png_options)
```

Setelah `save` selesai, `vector.png` akan berisi versi rasterisasi dari SVG asli. Konversi dilakukan sepenuhnya dalam memori, sehingga cepat bahkan untuk file besar.

### Langkah 4: Verifikasi output (opsional tetapi disarankan)

```python
from PIL import Image

with Image.open(png_path) as img:
    print(f"PNG size: {img.size} – mode: {img.mode}")
    img.show()  # Opens the image in the default viewer
```

Menjalankan cuplikan ini mencetak dimensi piksel dan membuka PNG, mengonfirmasi bahwa konversi berhasil.

## Menyesuaikan konversi (cara mengonversi SVG dengan kontrol lebih)

Jika Anda memerlukan DPI tertentu atau latar belakang solid untuk SVG transparan, sesuaikan `PngSaveOptions` sebelum memanggil `save`:

```python
png_options = PngSaveOptions()
png_options.dpi = 300                     # High‑resolution output
png_options.background_color = "#FFFFFF" # White background for transparency
```

Pengaturan ini berguna ketika PNG akan dicetak atau disematkan dalam dokumen yang tidak mendukung kanal alfa.

## Skrip lengkap – **kode svg to png** siap dijalankan

Berikut adalah program lengkap yang mencakup penanganan error dan pengaturan khusus opsional. Salin ke dalam file bernama `svg_to_png.py` dan jalankan `python svg_to_png.py`.

```python
"""
Complete script to save SVG as PNG using the Aspose.SVG library.
It demonstrates the basic flow and optional customizations.
"""

import sys
from aspose.svg import SVGDocument, PngSaveOptions
from PIL import Image

def convert_svg_to_png(
    svg_path: str,
    png_path: str,
    dpi: int = 96,
    background: str = None,
) -> None:
    """
    Loads an SVG file, applies PNG save options, and writes the PNG file.
    
    Args:
        svg_path: Path to the source SVG file.
        png_path: Desired output PNG file path.
        dpi: Dots per inch for the rasterized image (default 96).
        background: Hex color (e.g., "#FFFFFF") for the PNG background.
                     If None, the original SVG transparency is kept.
    """
    try:
        # Load SVG
        svg_doc = SVGDocument(svg_path)

        # Prepare PNG options
        png_options = PngSaveOptions()
        png_options.dpi = dpi
        if background:
            png_options.background_color = background

        # Save as PNG
        svg_doc.save(png_path, png_options)

        # Verify result
        with Image.open(png_path) as img:
            print(f"Successfully saved PNG → {png_path}")
            print(f"Image size: {img.size} (pixels), mode: {img.mode}")

    except Exception as e:
        print(f"Error during conversion: {e}", file=sys.stderr)
        sys.exit(1)


if __name__ == "__main__":
    # Example usage – replace paths as needed
    SVG_INPUT = "YOUR_DIRECTORY/vector.svg"
    PNG_OUTPUT = "YOUR_DIRECTORY/vector.png"

    convert_svg_to_png(
        svg_path=SVG_INPUT,
        png_path=PNG_OUTPUT,
        dpi=300,               # High‑resolution export
        background="#FFFFFF", # White background for transparent SVGs
    )
```

**Output yang diharapkan**

```
Successfully saved PNG → YOUR_DIRECTORY/vector.png
Image size: (800, 600) (pixels), mode: RGB
```

Dimensi gambar mencerminkan viewBox SVG atau DPI yang Anda tentukan.

## Kesulitan umum dan cara menghindarinya

| Gejala | Penyebab | Solusi |
|---------|-------|-----|
| PNG kosong atau sepenuhnya transparan | `background_color` tidak diatur untuk SVG yang mengandalkan transparansi | Atur `png_options.background_color` ke nilai hex solid. |
| Output buram | DPI dibiarkan pada default 96 untuk SVG dengan detail tinggi | Tingkatkan `png_options.dpi` menjadi 300 atau lebih tinggi. |
| Skrip crash dengan `FileNotFoundError` | Path ke file SVG salah | Gunakan path absolut atau verifikasi `os.path.exists(svg_path)`. |
| Perubahan warna pada PNG | SVG menggunakan profil ICC yang tidak didukung oleh pustaka | Rasterisasi dengan pustaka lain (mis., `cairosvg`) atau ratakan warna sebelum ekspor. |

## Langkah selanjutnya

* **Batch conversion** – Loop melalui direktori SVG dan gunakan kembali `convert_svg_to_png`.  
* **Integrasi dengan layanan web** – Ekspose fungsi sebagai endpoint Flask untuk mengonversi unggahan secara langsung.  
* **Jelajahi format lain** – `PngSaveOptions` memiliki saudara seperti `JpegSaveOptions` dan `BmpSaveOptions` untuk kebutuhan ekspor tambahan.

Dengan menguasai alur kerja **save svg as png**, Anda dapat mengotomatisasi pipeline aset, menghasilkan thumbnail untuk galeri, atau menyiapkan grafik untuk laporan PDF—semua dari satu skrip Python.

---


## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Konversi SVG ke PNG di Python – Panduan Ekspor Resolusi Tinggi](/html/english/python/general/convert-svg-to-png-in-python-high-resolution-export-guide/)
- [Konversi SVG ke PNG di Python – Panduan Langkah demi Langkah Lengkap](/html/english/python/general/convert-svg-to-png-in-python-complete-step-by-step-guide/)
- [Konversi SVG ke PNG di Python menggunakan Aspose.HTML](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
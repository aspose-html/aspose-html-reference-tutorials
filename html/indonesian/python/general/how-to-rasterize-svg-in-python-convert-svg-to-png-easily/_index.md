---
category: general
date: 2026-10-28
description: Pelajari cara merasterkan SVG di Python dan mengonversi SVG ke PNG dengan
  skrip sederhana menggunakan CairoSVG. Simpan SVG sebagai PNG dalam hitungan detik.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to rasterize svg
- convert svg to png
- save svg as png
- svg to png python
- export svg as png
language: id
lastmod: 2026-10-28
og_description: 'Cara merasterkan SVG di Python: panduan ini menunjukkan cara mengonversi
  SVG ke PNG menggunakan CairoSVG, mencakup instalasi, kode, dan pemecahan masalah.'
og_image_alt: Screenshot of Python code that rasterizes SVG to PNG
og_title: Cara merasterkan SVG di Python – panduan cepat SVG ke PNG
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to rasterize SVG in Python and convert SVG to PNG with a
    simple script using CairoSVG. Save SVG as PNG in seconds.
  headline: How to rasterize SVG in Python – convert SVG to PNG easily
  type: TechArticle
- description: Learn how to rasterize SVG in Python and convert SVG to PNG with a
    simple script using CairoSVG. Save SVG as PNG in seconds.
  name: How to rasterize SVG in Python – convert SVG to PNG easily
  steps:
  - name: Why CairoSVG?
    text: '- **Pure Python**: No need for external command‑line tools once the package
      is installed. - **SVG‑compliant**: Supports most SVG 1.1 features, including
      gradients, masks, and text. - **Flexible output**: Besides PNG, you can export
      to PDF, PS, or even raw bytes.'
  - name: Step‑by‑step breakdown
    text: 1. **Install the library** – `pip install cairosvg` pulls in the compiled
      Cairo bindings. 2. **Import the module** – `import cairosvg` gives you access
      to the `svg2png` helper. 3. **Call `svg2png`** – Pass the SVG file path (or
      a URL) and the destination PNG path. Optional `output_width`, `output_he
  - name: Edge cases you might encounter
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | **Large SVG (megapixel dimensions)** | Increase `dpi` or set explicit `output_width`/`output_height`
      to avoid memory spikes. | | **Missing fonts** | Install the required fonts on
      the system or em'
  type: HowTo
tags:
- svg
- python
- image processing
- cairosvg
title: Cara merasterkan SVG di Python – konversi SVG ke PNG dengan mudah
url: /id/python/general/how-to-rasterize-svg-in-python-convert-svg-to-png-easily/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara merasterisasi SVG di Python – konversi SVG ke PNG dengan mudah

Jika Anda perlu **cara merasterisasi svg** untuk aplikasi web, laporan, atau proses build otomatis, panduan ini memberikan solusi siap‑jalankan. Anda akan melihat cara **konversi svg ke png** dengan hanya beberapa baris Python, dan hasilnya adalah PNG tajam yang dapat Anda simpan atau layani secara langsung.

Tutorial ini mencakup semua hal mulai dari instalasi pustaka yang diperlukan hingga penanganan kasus tepi seperti file besar atau pengaturan DPI khusus. Pada akhir tutorial, Anda akan dapat **simpan svg sebagai png**, **ekspor svg sebagai png**, dan mengintegrasikan proses ini ke dalam alur kerja Python apa pun.

## Apa yang Anda perlukan

- Python 3.8+ (kode ini bekerja pada 3.9, 3.10, dan versi lebih baru)
- `pip` untuk menginstal paket
- File SVG lokal (misalnya `logo.svg`) yang ingin Anda rasterisasi
- Opsional: lingkungan virtual untuk manajemen dependensi yang bersih

> **Tip Pro:** Menggunakan lingkungan virtual (`python -m venv .venv`) memisahkan dependensi CairoSVG dari paket Python global Anda.

## Cara merasterisasi SVG di Python

Cara paling sederhana untuk **cara merasterisasi svg** adalah dengan pustaka **CairoSVG**. CairoSVG membaca XML SVG, merendernya dengan mesin grafis Cairo, dan menulis gambar raster ke PNG, PDF, atau format bitmap lainnya.

```bash
# Install CairoSVG and its binary dependencies
pip install cairosvg
```

```python
# rasterize_svg.py
import sys
from pathlib import Path
import cairosvg

def rasterize_svg(input_path: str, output_path: str,
                  width: int | None = None,
                  height: int | None = None,
                  dpi: int = 96) -> None:
    """
    Convert an SVG file to a PNG image.

    Parameters
    ----------
    input_path : str
        Path to the source SVG file.
    output_path : str
        Destination path for the PNG file.
    width : int | None
        Desired output width in pixels (maintains aspect ratio if height is None).
    height : int | None
        Desired output height in pixels (maintains aspect ratio if width is None).
    dpi : int
        Dots per inch for the rasterization. Higher DPI yields larger files but more detail.
    """
    try:
        # CairoSVG can read from a file path directly
        cairosvg.svg2png(url=Path(input_path).as_uri(),
                         write_to=output_path,
                         output_width=width,
                         output_height=height,
                         dpi=dpi)
        print(f"✅ Successfully saved PNG to {output_path}")
    except Exception as e:
        print(f"❌ Failed to rasterize {input_path}: {e}", file=sys.stderr)
        raise

if __name__ == "__main__":
    # Example usage:
    # python rasterize_svg.py ./assets/logo.svg ./output/logo.png 300 300
    if len(sys.argv) < 3:
        print("Usage: python rasterize_svg.py <input_svg> <output_png> [width] [height] [dpi]")
        sys.exit(1)

    input_svg = sys.argv[1]
    output_png = sys.argv[2]
    w = int(sys.argv[3]) if len(sys.argv) > 3 else None
    h = int(sys.argv[4]) if len(sys.argv) > 4 else None
    d = int(sys.argv[5]) if len(sys.argv) > 5 else 96

    rasterize_svg(input_svg, output_png, width=w, height=h, dpi=d)
```

### Mengapa CairoSVG?

- **Pure Python**: Tidak memerlukan alat baris perintah eksternal setelah paket diinstal.
- **SVG‑compliant**: Mendukung sebagian besar fitur SVG 1.1, termasuk gradien, masker, dan teks.
- **Flexible output**: Selain PNG, Anda dapat mengekspor ke PDF, PS, atau bahkan byte mentah.

### Langkah‑per‑langkah

1. **Instal pustaka** – `pip install cairosvg` mengunduh binding Cairo yang telah dikompilasi.  
2. **Impor modul** – `import cairosvg` memberi Anda akses ke helper `svg2png`.  
3. **Panggil `svg2png`** – Berikan path file SVG (atau URL) dan path tujuan PNG. Opsional `output_width`, `output_height`, dan `dpi` memungkinkan Anda mengontrol ukuran dan resolusi.  
4. **Tangani error** – Blok `try/except` mencetak pesan jelas jika SVG tidak valid atau direktori output tidak dapat ditulisi.

## Konversi SVG ke PNG dengan CairoSVG

Jika Anda hanya membutuhkan satu baris kode untuk konversi cepat, cuplikan berikut melakukan pekerjaan tanpa fungsi pembungkus:

```python
import cairosvg

cairosvg.svg2png(url="logo.svg", write_to="logo.png")
```

Ini adalah ilustrasi paling singkat dari **konversi svg ke png**. Ia membaca `logo.svg` dari direktori saat ini dan menulis `logo.png` di sampingnya.

## Simpan SVG sebagai PNG – verifikasi hasilnya

Setelah menjalankan skrip, Anda seharusnya melihat file PNG di path tujuan. Buka dengan penampil gambar apa pun untuk memastikan:

```bash
# Linux/macOS
xdg-open ./output/logo.png   # or open on macOS
# Windows
start ./output/logo.png
```

Jika PNG terlihat buram, tingkatkan argumen `dpi` (misalnya, `dpi=300`) untuk menghasilkan raster dengan resolusi lebih tinggi.

## Ekspor SVG sebagai PNG dalam format berbeda

CairoSVG juga dapat menghasilkan **PDF**, **PostScript**, atau **PNG bytes** mentah. Berikut contoh mengekspor ke objek `BytesIO` ketika Anda memerlukan gambar dalam memori (misalnya, untuk respons Flask):

```python
import io
import cairosvg

svg_path = "logo.svg"
png_bytes = io.BytesIO()
cairosvg.svg2png(url=Path(svg_path).as_uri(), write_to=png_bytes)
png_bytes.seek(0)  # Ready for sending over HTTP
```

### Kasus tepi yang mungkin Anda temui

| Situasi                                 | Penanganan yang disarankan |
|----------------------------------------|----------------------------|
| **SVG Besar (dimensi megapiksel)**     | Tingkatkan `dpi` atau tetapkan `output_width`/`output_height` secara eksplisit untuk menghindari lonjakan memori. |
| **Font yang hilang**                   | Instal font yang diperlukan pada sistem atau sematkan dalam SVG menggunakan tag `<style>`. |
| **Masalah transparansi**               | PNG mempertahankan alfa secara default; jika Anda memerlukan latar belakang solid, berikan `background_color="#FFFFFF"` ke `svg2png`. |
| **Pemrosesan batch**                   | Loop melalui direktori berisi SVG dan panggil `rasterize_svg` untuk setiap file. |

## Contoh kerja lengkap

Berikut adalah skrip minimal yang berdiri sendiri yang dapat Anda salin‑tempel ke file bernama `svg_to_png.py` dan jalankan segera.

```python
# svg_to_png.py
import cairosvg
from pathlib import Path

def main():
    src = Path("example.svg")
    dst = Path("example.png")
    if not src.is_file():
        raise FileNotFoundError(f"Source SVG not found: {src}")

    # Convert with default DPI (96) and keep original dimensions
    cairosvg.svg2png(url=src.as_uri(), write_to=dst)
    print(f"✅ {src.name} → {dst.name} created successfully.")

if __name__ == "__main__":
    main()
```

Menjalankan `python svg_to_png


## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang erat dengan teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑per‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [How to Rasterize SVG in Python – Complete Guide](/html/english/python/general/how-to-rasterize-svg-in-python-complete-guide/)
- [Convert SVG to PNG in Python – High‑Resolution Export Guide](/html/english/python/general/convert-svg-to-png-in-python-high-resolution-export-guide/)
- [Create SVG Document in Python – Convert SVG to PNG Guide](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
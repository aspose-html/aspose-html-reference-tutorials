---
category: general
date: 2026-06-19
description: Konversi SVG ke PNG di Python dengan cepat dan mudah. Pelajari cara menyimpan
  SVG sebagai PNG, menangani konversi SVG ke PNG, dan mengekspor SVG ke PNG dengan
  skrip sederhana.
draft: false
keywords:
- convert svg to png
- save svg as png
- svg to png conversion
- svg to png python
- export svg to png
language: id
og_description: Konversi SVG ke PNG di Python dengan tutorial praktis ini. Pelajari
  proses konversi lengkap dari SVG ke PNG dan cara mengekspor SVG ke PNG secara efisien.
og_title: Mengonversi SVG ke PNG dengan Python – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Convert SVG to PNG in Python quickly and easily. Learn how to save
    SVG as PNG, handle svg to png conversion, and export SVG to PNG with a simple
    script.
  headline: Convert SVG to PNG in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Convert SVG to PNG in Python quickly and easily. Learn how to save
    SVG as PNG, handle svg to png conversion, and export SVG to PNG with a simple
    script.
  name: Convert SVG to PNG in Python – Complete Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - Basic familiarity with pip and
      virtual environments. - An SVG file you want to transform (we’ll use `logo.svg`
      as an example).'
  - name: Why This Approach Works
    text: '- **Explicit I/O handling:** By reading the SVG as bytes, we avoid issues
      with Unicode encodings that sometimes crop up on Windows. - **Custom DPI:**
      Scaling is often required when the target PNG must match a specific pixel density
      (think print vs. screen). - **Optional background:** Some SVGs have '
  - name: Expected Result
    text: '- `output/logo.png` – a 1:1 raster of the original SVG, preserving any
      transparency. - `output/logo_highres.png` – a 300 DPI version with a white background,
      perfect for print.'
  - name: 1. **What if the SVG uses external fonts?**
    text: '`cairosvg` tries to embed referenced fonts, but it only sees files on the
      local filesystem. Copy the font files next to the SVG or embed them directly
      in the SVG with `<style>` tags. Otherwise you’ll get fallback fonts in the PNG.'
  - name: 2. **How do I keep the original aspect ratio when scaling?**
    text: Pass only `dpi` and let Cairo compute the pixel dimensions from the SVG’s
      viewBox. If you need a fixed width/height, calculate the appropriate DPI yourself
      or use the `output_width`/`output_height` arguments provided by `svg2png`.
  - name: 3. **Can I convert large SVGs without exhausting memory?**
    text: Yes. `cairosvg` streams the rasterization, but you should avoid loading
      massive SVGs into memory all at once. Process them one by one, as shown in the
      batch example.
  - name: 4. **Is the conversion thread‑safe?**
    text: The underlying Cairo library is not fully thread‑safe on all platforms.
      If you plan to run conversions in parallel, wrap calls in a multiprocessing
      pool rather than threading.
  - name: What’s Next?
    text: '- Explore **svg to png conversion** with alternative libraries like `svglib`
      + `reportlab` for PDF‑first workflows. - Combine this script with image‑optimization
      tools (e.g., `pngquant`) to shrink file size for the web. - Add a CLI wrapper
      using `argparse` or `click` so you can run `python -m conver'
  type: HowTo
tags:
- Python
- Image Processing
- SVG
title: Mengonversi SVG ke PNG dengan Python – Panduan Langkah demi Langkah Lengkap
url: /id/python/general/convert-svg-to-png-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konversi SVG ke PNG di Python – Panduan Lengkap Langkah‑per‑Langkah

Pernah membutuhkan untuk **convert SVG to PNG** tetapi tidak yakin pustaka mana yang harus dipilih? Anda tidak sendirian—banyak pengembang mengalami masalah ini ketika mencoba menyematkan grafik vektor ke aset web atau menghasilkan thumbnail secara langsung. Kabar baik? Dengan hanya beberapa baris Python Anda dapat **save SVG as PNG** dan menjaga alur pembangunan tetap lancar.

Dalam tutorial ini kami akan membahas **svg to png conversion** praktis menggunakan pustaka populer, mengulas nuansa kode **svg to png python**, dan menunjukkan cara **export SVG to PNG** dengan penanganan error yang tepat. Pada akhir tutorial Anda akan memiliki fungsi yang dapat dipakai ulang yang dapat Anda masukkan ke proyek apa pun, baik Anda membangun alat CLI maupun layanan gambar sisi‑server.

## Apa yang Akan Anda Pelajari

- Dependensi minimal yang diperlukan untuk **convert svg to png** di Python.  
- Cara memuat file SVG, mengonfigurasi opsi ekspor PNG, dan menulis gambar output.  
- Jebakan umum (latar belakang transparan, dimensi besar) dan cara menghindarinya.  
- Skrip siap‑jalankan yang dapat Anda sesuaikan untuk pemrosesan batch atau diintegrasikan ke endpoint Flask/Django.  

### Prasyarat

- Python 3.8+ terpasang di mesin Anda.  
- Familiaritas dasar dengan pip dan lingkungan virtual.  
- File SVG yang ingin Anda ubah (kami akan menggunakan `logo.svg` sebagai contoh).  

Jika Anda sudah memiliki semuanya, bagus—mari kita mulai.

## Langkah 1: Instal Pustaka yang Diperlukan

Cara paling sederhana untuk **convert SVG to PNG** di Python adalah dengan paket `cairosvg`. Paket ini membungkus pustaka grafis Cairo dan menangani rasterisasi vektor di balik layar.

```bash
pip install cairosvg
```

> **Pro tip:** Tetapkan versi (misalnya, `cairosvg==2.7.0`) di `requirements.txt` Anda untuk menghindari kerusakan tak terduga ketika rilis mayor baru muncul.

## Langkah 2: Tulis Fungsi Konversi Sederhana

Setelah pustaka tersedia, kami akan membuat pembantu kecil yang melakukan pekerjaan berat. Fungsi ini membungkus logika **svg to png python**, memudahkan penggunaan kembali.

```python
# convert_svg_to_png.py
import os
from cairosvg import svg2png

def convert_svg_to_png(
    input_path: str,
    output_path: str,
    dpi: int = 96,
    background_color: str = None,
) -> None:
    """
    Convert an SVG file to a PNG image.

    Parameters
    ----------
    input_path : str
        Path to the source SVG file.
    output_path : str
        Destination path for the generated PNG.
    dpi : int, optional
        Dots per inch for the rasterized image (default: 96).
    background_color : str, optional
        Hex color (e.g., "#FFFFFF") to use as background.
        If None, the SVG's own transparency is preserved.

    Raises
    ------
    FileNotFoundError
        If the input SVG does not exist.
    ValueError
        If the output directory cannot be created.
    """
    # Validate input file
    if not os.path.isfile(input_path):
        raise FileNotFoundError(f"SVG file not found: {input_path}")

    # Ensure output directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Read the SVG content
    with open(input_path, "rb") as svg_file:
        svg_bytes = svg_file.read()

    # Perform the conversion
    svg2png(
        bytestring=svg_bytes,
        write_to=output_path,
        dpi=dpi,
        background_color=background_color,
    )
    print(f"✅ Successfully saved PNG to {output_path}")
```

### Mengapa Pendekatan Ini Berhasil

- **Explicit I/O handling:** Dengan membaca SVG sebagai byte, kami menghindari masalah dengan enkoding Unicode yang kadang muncul di Windows.  
- **Custom DPI:** Skala sering diperlukan ketika PNG target harus cocok dengan kepadatan piksel tertentu (pikirkan cetak vs. layar).  
- **Optional background:** Beberapa SVG memiliki area transparan; memberikan warna hex memungkinkan Anda **export SVG to PNG** dengan latar belakang padat, yang berguna untuk thumbnail UI.  

## Langkah 3: Jalankan Skrip Konversi

Dengan fungsi siap, mari konversi file nyata. Letakkan `logo.svg` di folder bernama `assets/` dan jalankan skrip dari root proyek.

```python
# demo_conversion.py
from convert_svg_to_png import convert_svg_to_png

if __name__ == "__main__":
    INPUT_SVG = "assets/logo.svg"
    OUTPUT_PNG = "output/logo.png"

    # Simple call – defaults keep transparency and 96 DPI
    convert_svg_to_png(INPUT_SVG, OUTPUT_PNG)

    # Example with a white background and higher DPI for sharper output
    convert_svg_to_png(
        INPUT_SVG,
        "output/logo_highres.png",
        dpi=300,
        background_color="#FFFFFF",
    )
```

Jalankan:

```bash
python demo_conversion.py
```

Anda akan melihat output konsol yang mengonfirmasi file telah ditulis:

```
✅ Successfully saved PNG to output/logo.png
✅ Successfully saved PNG to output/logo_highres.png
```

### Hasil yang Diharapkan

- `output/logo.png` – raster 1:1 dari SVG asli, mempertahankan transparansi apa pun.  
- `output/logo_highres.png` – versi 300 DPI dengan latar belakang putih, sempurna untuk cetak.  

![contoh output convert svg ke png](example.png){alt="contoh output convert svg ke png"}

*(Tangkapan layar menunjukkan file PNG dibuka di penampil gambar, mengonfirmasi konversi berhasil.)*

## Langkah 4: Proses Batch Banyak SVG (Opsional)

Jika Anda perlu **save SVG as PNG** untuk seluruh direktori, loop singkat dapat menyelesaikannya. Potongan kode ini juga menunjukkan penanganan error yang elegan—berguna ketika beberapa SVG mungkin rusak.

```python
import glob
from pathlib import Path

def batch_convert(source_dir: str, dest_dir: str, **options):
    svg_paths = glob.glob(os.path.join(source_dir, "*.svg"))
    for svg_path in svg_paths:
        try:
            filename = Path(svg_path).stem + ".png"
            output_path = os.path.join(dest_dir, filename)
            convert_svg_to_png(svg_path, output_path, **options)
        except Exception as e:
            print(f"⚠️  Failed to convert {svg_path}: {e}")

if __name__ == "__main__":
    batch_convert(
        source_dir="assets/",
        dest_dir="output/batch/",
        dpi=150,
        background_color="#F0F0F0",
    )
```

Menjalankan ini akan mengisi `output/batch/` dengan PNG untuk setiap SVG di `assets/`. Jika sebuah file gagal, skrip mencatat error dan melanjutkan—tidak perlu menghentikan seluruh pekerjaan.

## Pertanyaan Umum & Kasus Tepi

### 1. **Bagaimana jika SVG menggunakan font eksternal?**  

`cairosvg` mencoba menyematkan font yang direferensikan, tetapi hanya melihat file di sistem berkas lokal. Salin file font di sebelah SVG atau sematkan langsung dalam SVG dengan tag `<style>`. Jika tidak, Anda akan mendapatkan font fallback di PNG.

### 2. **Bagaimana cara menjaga rasio aspek asli saat menskalakan?**  

Berikan hanya `dpi` dan biarkan Cairo menghitung dimensi piksel dari viewBox SVG. Jika Anda membutuhkan lebar/tinggi tetap, hitung DPI yang sesuai sendiri atau gunakan argumen `output_width`/`output_height` yang disediakan oleh `svg2png`.

### 3. **Bisakah saya mengonversi SVG besar tanpa menghabiskan memori?**  

Ya. `cairosvg` melakukan streaming rasterisasi, tetapi Anda harus menghindari memuat SVG besar ke memori sekaligus. Proses satu per satu, seperti yang ditunjukkan dalam contoh batch.

### 4. **Apakah konversi ini thread‑safe?**  

Pustaka Cairo di bawahnya tidak sepenuhnya thread‑safe di semua platform. Jika Anda berencana menjalankan konversi secara paralel, bungkus pemanggilan dalam pool multiprocessing bukan threading.

## Tips Kinerja

- **Cache the PNG** jika SVG jarang berubah; menghitung ulang pada setiap permintaan membuang siklus CPU.  
- **Reuse the same DPI** di seluruh pemanggilan untuk menghindari perhitungan skala berulang.  
- Untuk layanan web, pertimbangkan mengembalikan PNG sebagai aliran `BytesIO` alih-alih menulis ke disk—ini mengurangi latensi I/O.  

```python
from io import BytesIO
def convert_svg_to_png_bytes(svg_path: str, dpi: int = 96) -> BytesIO:
    with open(svg_path, "rb") as f:
        svg_bytes = f.read()
    png_bytes = BytesIO()
    svg2png(bytestring=svg_bytes, write_to=png_bytes, dpi=dpi)
    png_bytes.seek(0)
    return png_bytes
```

## Ringkasan

Kami telah membahas semua yang Anda perlukan untuk **convert SVG to PNG** menggunakan Python:

1. Instal `cairosvg`.  
2. Tulis fungsi `convert_svg_to_png` yang dapat dipakai ulang yang menangani DPI, warna latar belakang, dan pengecekan error.  
3. Jalankan skrip pada satu file atau proses batch seluruh folder.  
4. Atasi keanehan umum seperti font eksternal, preservasi rasio aspek, dan keamanan thread.  

Dengan pengetahuan ini, Anda kini dapat **save SVG as PNG** dalam pipeline otomatisasi apa pun, mengintegrasikan konversi ke API web, atau sekadar menghasilkan aset untuk sistem desain. 

### Apa Selanjutnya?

- Jelajahi **svg to png conversion** dengan pustaka alternatif seperti `svglib` + `reportlab` untuk alur kerja PDF‑first.  
- Gabungkan skrip ini dengan alat optimasi gambar (mis., `pngquant`) untuk memperkecil ukuran file bagi web.  
- Tambahkan pembungkus CLI menggunakan `argparse` atau `click` sehingga Anda dapat menjalankan `python -m convert_svg_to_png INPUT.svg OUTPUT.png` dari terminal.  

Ada pertanyaan lebih lanjut? Tinggalkan komentar di bawah, atau fork repositori dan bereksperimen dengan pengaturan ekspor yang berbeda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [svg to png java – Konversi SVG ke Gambar dengan Aspose.HTML untuk Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Render SVG Doc sebagai PNG di .NET dengan Aspose.HTML](/html/english/net/rendering-html-documents/render-svg-doc-as-png/)
- [svg a png java – Mengonversi SVG ke gambar dengan Aspose.HTML untuk Java](/html/spanish/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
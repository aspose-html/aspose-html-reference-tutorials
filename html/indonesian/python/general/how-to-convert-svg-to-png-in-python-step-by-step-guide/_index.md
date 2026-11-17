---
category: general
date: 2026-11-17
description: Konversi SVG ke PNG menggunakan Python dalam beberapa baris. Pelajari
  cara menyimpan SVG sebagai PNG dengan pengaturan konversi opsional.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert svg to png
- save svg as png
- export svg as png
- svg to raster image
- how to convert svg to png
language: id
lastmod: 2026-11-17
og_description: Konversi SVG ke PNG dalam Python dengan contoh singkat. Ikuti langkah-langkah
  untuk mengekspor SVG menjadi PNG secara efisien.
og_image_alt: Diagram illustrating convert svg to png workflow in Python
og_title: Konversi SVG ke PNG di Python – Panduan Cepat
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: convert svg to png using Python in a few lines. Learn to save SVG as
    PNG with optional conversion settings.
  headline: How to convert SVG to PNG in Python – step‑by‑step guide
  type: TechArticle
tags:
- svg
- png
- python
- image conversion
title: Cara mengonversi SVG ke PNG di Python – panduan langkah demi langkah
url: /id/python/general/how-to-convert-svg-to-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengonversi SVG ke PNG di Python – panduan langkah demi langkah

Jika Anda perlu **mengonversi svg ke png**, panduan ini menunjukkan solusi lengkap yang dapat Anda jalankan hari ini. Anda juga akan melihat cara **menyimpan svg sebagai png** dengan pengaturan opsional untuk ukuran dan warna latar belakang.

Membuat gambar raster dari file SVG vektor umum dilakukan ketika Anda menyajikan grafik ke browser, membuat thumbnail, atau menyematkan gambar dalam PDF. Tutorial ini mencakup semuanya mulai dari menginstal pustaka yang diperlukan hingga menangani kasus tepi seperti file yang hilang atau SVG yang sangat besar.

## Prasyarat

* Python 3.8 atau yang lebih baru terinstal.
* Akses ke terminal atau command prompt.
* Paket `cairosvg`, yang melakukan pekerjaan berat untuk konversi **svg to raster image**.

Anda dapat menginstal paket tersebut dengan satu perintah pip:

```bash
pip install cairosvg
```

> **Pro tip:** Gunakan lingkungan virtual untuk menjaga dependensi terisolasi dari proyek lain.

## Cara mengonversi SVG ke PNG di Python

Inti proses terdiri dari tiga tindakan: memuat SVG, secara opsional menyesuaikan parameter konversi, dan menulis file PNG. Kode di bawah ini mengimplementasikan ketiga langkah tersebut dalam fungsi yang dapat digunakan kembali.

```python
import cairosvg
from pathlib import Path

def convert_svg_to_png(svg_path: str, png_path: str) -> None:
    """
    Convert an SVG file to a PNG raster image.

    Parameters
    ----------
    svg_path : str
        Path to the source SVG file.
    png_path : str
        Destination path for the generated PNG file.
    """
    # Verify that the SVG file exists
    if not Path(svg_path).is_file():
        raise FileNotFoundError(f"SVG file not found: {svg_path}")

    # Perform the conversion using default settings
    cairosvg.svg2png(url=svg_path, write_to=png_path)

# Example usage
if __name__ == "__main__":
    svg_file = "YOUR_DIRECTORY/image.svg"
    png_file = "YOUR_DIRECTORY/image.png"
    convert_svg_to_png(svg_file, png_file)
    print(f"Converted {svg_file} to {png_file}")
```

### Mengapa ini berhasil

* `cairosvg.svg2png` membaca file SVG (`url=svg_path`) dan menulis file PNG (`write_to=png_path`).  
* Fungsi ini menghasilkan error yang jelas jika SVG sumber tidak dapat ditemukan, yang membantu Anda men-debug masalah jalur file lebih awal.  
* Menjaga logika konversi di dalam fungsi memudahkan penggunaan kembali di banyak skrip atau integrasi ke aplikasi yang lebih besar.

## Opsional: menyempurnakan konversi

Jika Anda memerlukan ukuran output tertentu atau latar belakang yang berbeda, `cairosvg.svg2png` menerima argumen tambahan. Di bawah ini adalah varian yang mengatur lebar 300 px dan latar belakang putih.

```python
def convert_svg_to_png_custom(svg_path: str, png_path: str,
                              width: int = 300,
                              background_color: str = "white") -> None:
    """
    Convert an SVG to PNG with custom dimensions and background.

    Parameters
    ----------
    width : int
        Desired width of the PNG in pixels; height scales proportionally.
    background_color : str
        Hex or named color for the PNG background.
    """
    if not Path(svg_path).is_file():
        raise FileNotFoundError(f"SVG file not found: {svg_path}")

    cairosvg.svg2png(
        url=svg_path,
        write_to=png_path,
        output_width=width,
        background_color=background_color
    )
```

Anda dapat memanggil fungsi ini dengan cara yang sama seperti versi dasar, dengan memberikan lebar atau warna apa pun yang Anda inginkan.

## Pertanyaan umum dan kasus tepi

**Bagaimana jika SVG berisi font eksternal?**  
`cairosvg` secara otomatis menyematkan font yang direferensikan, tetapi file font harus dapat diakses dari lokasi SVG. Letakkan file font di samping SVG atau gunakan URL absolut.

**Bagaimana cara menangani SVG yang sangat besar?**  
File besar dapat mengonsumsi memori yang signifikan. Anda dapat melakukan streaming konten SVG alih-alih memuatnya dari disk:

```python
with open(svg_path, "rb") as svg_stream:
    cairosvg.svg2png(file_obj=svg_stream, write_to=png_path)
```

**Bisakah saya mengonversi beberapa file sekaligus?**  
Bungkus pemanggilan konversi dalam sebuah loop dan gunakan `Path.glob("*.svg")` untuk menemukan semua SVG dalam sebuah direktori.

## Output yang Diharapkan

Menjalankan skrip contoh mencetak satu baris yang mengonfirmasi konversi:

```
Converted YOUR_DIRECTORY/image.svg to YOUR_DIRECTORY/image.png
```

File `image.png` yang dihasilkan berada di direktori yang sama dan dapat dibuka dengan penampil gambar apa pun.

## Kesimpulan

Anda sekarang tahu cara **convert svg to png** di Python, cara **save svg as png**, dan cara **export svg as png** dengan dimensi khusus. Pendekatan yang sama bekerja untuk file SVG apa pun, mengubah grafik vektor menjadi format **svg to raster image** yang cocok untuk halaman web, laporan, atau thumbnail.

Langkah selanjutnya dapat meliputi:

* Menjelajahi parameter `export svg as png` untuk kontrol DPI.
* Mengintegrasikan fungsi konversi ke endpoint Flask atau Django untuk menyediakan pembuatan gambar secara langsung.
* Menggunakan kata kunci sekunder **how to convert svg to png** untuk mencari kasus penggunaan yang lebih maju seperti pemrosesan batch atau pipeline CI/CD.

Silakan bereksperimen dengan pengaturan yang berbeda dan bagikan hasil Anda dengan komunitas!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Mengonversi SVG ke PNG di Python – Panduan Ekspor Resolusi Tinggi](/html/english/python/general/convert-svg-to-png-in-python-high-resolution-export-guide/)
- [Mengonversi SVG ke PNG di Python menggunakan Aspose.HTML](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)
- [Mengonversi SVG ke PNG di Python – Panduan Langkah demi Langkah Lengkap](/html/english/python/general/convert-svg-to-png-in-python-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
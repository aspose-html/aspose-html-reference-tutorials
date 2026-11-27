---
category: general
date: 2026-11-27
description: Buat dokumen SVG dan simpan file SVG menggunakan Python. Pelajari cara
  mengekspor vektor sebagai SVG dan menghasilkan gambar SVG dengan cepat.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG file
- export vector as SVG
- save SVG image
- how to create SVG
language: id
lastmod: 2026-11-27
og_description: Buat dokumen SVG dan simpan file SVG dengan Python. Panduan ini menunjukkan
  cara mengekspor vektor sebagai SVG dan menghasilkan gambar SVG dalam hitungan menit.
og_image_alt: Screenshot of a red circle saved as an SVG document
og_title: Buat dokumen SVG dan simpan file SVG menggunakan Python
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  headline: Create SVG document and save SVG file with Python
  type: TechArticle
- description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  name: Create SVG document and save SVG file with Python
  steps:
  - name: Expected output
    text: 'The resulting `circle.svg` contains:'
  - name: Exporting more complex vectors
    text: 'If you need to **export vector as SVG** for multi‑shape illustrations,
      simply repeat the `dwg.add()` pattern with other primitives (`rect`, `line`,
      `path`, etc.). For example:'
  - name: Handling Unicode and text
    text: "SVG supports text elements with full Unicode support. Use `dwg.text(\"Hello,
      \U0001F30D\", insert=(5, 95), fill=\"black\")` to embed multilingual labels."
  - name: Saving to a different location
    text: 'When **save SVG image** to a user‑specified folder, validate the path to
      avoid permission errors:'
  - name: Minifying the output
    text: 'For production pipelines, you might want a smaller file size. Pass `pretty=False`
      to `dwg.tostring()` and write the result manually:'
  type: HowTo
tags:
- SVG
- Python
- Vector graphics
title: Buat dokumen SVG dan simpan file SVG dengan Python
url: /id/python/general/create-svg-document-and-save-svg-file-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Dokumen SVG dan Simpan File SVG dengan Python

Jika Anda perlu **create SVG document** dari awal, panduan ini akan memandu Anda melalui seluruh proses. Anda akan melihat cara **save SVG file** ke disk, mengekspor vektor sebagai SVG, dan mendapatkan gambar SVG siap pakai hanya dalam beberapa baris kode.

Membuat grafik yang dapat diskalakan secara programatik berguna untuk laporan, ikon UI, atau situasi apa pun di mana Anda menginginkan gambar yang tidak bergantung pada resolusi. Pada akhir tutorial ini Anda akan dapat menjawab “**how to create SVG**?” untuk bentuk sederhana dan memperluas pola tersebut ke karya vektor yang kompleks.

## Apa yang Anda butuhkan

- Python 3.8 atau yang lebih baru  
- Paket `svgwrite` (dapat diinstal melalui `pip`)  
- Direktori yang dapat ditulisi untuk file output  

Tidak diperlukan editor grafis eksternal; semuanya berjalan dari baris perintah.

## Langkah 1: Instal library `svgwrite`

`svgwrite` menyediakan API yang bersih dan Pythonic untuk membangun markup SVG. Instal sekali dengan:

```bash
pip install svgwrite
```

> **Pro tip:** Gunakan lingkungan virtual (`python -m venv .venv`) untuk menjaga ketergantungan terisolasi.

## Langkah 2: Buat Dokumen SVG

Sekarang kita benar-benar **create SVG document** objek. Kelas `Drawing` mewakili elemen root `<svg>` dan menangani namespace secara otomatis.

```python
import pathlib
import svgwrite

# Define where the file will be saved
output_path = pathlib.Path("output/circle.svg")
output_path.parent.mkdir(parents=True, exist_ok=True)

# Initialize a new SVG document with a 100×100 viewport
dwg = svgwrite.Drawing(
    filename=str(output_path),
    size=("100px", "100px"),
    profile="tiny"  # tiny profile keeps the file lightweight
)
```

Instansi `Drawing` adalah titik masuk untuk semua operasi SVG berikutnya. Dengan menentukan `size` kami mengatur dimensi kanvas, yang memengaruhi cara peramban merender gambar.

## Langkah 3: Tambahkan Elemen Lingkaran Merah

Menambahkan bentuk sangat sederhana. Metode `circle` membuat elemen `<circle>`; kemudian kami menempelkannya ke root.

```python
# Create a red circle with radius 40 centered at (50, 50)
circle = dwg.circle(
    center=(50, 50),
    r=40,
    fill="red"
)

# Append the circle to the SVG root
dwg.add(circle)
```

Mengapa kami memilih lingkaran: lingkaran adalah primitif vektor yang menunjukkan skalabilitas tanpa kehilangan kualitas, menjadikan output ideal untuk menguji alur kerja **export vector as SVG**.

## Langkah 4: Simpan File SVG

Akhirnya, tulis markup ke disk. Langkah ini memenuhi persyaratan **save SVG file** dan menghasilkan file yang dapat Anda buka di peramban atau editor vektor mana pun.

```python
# Persist the SVG document to the filesystem
dwg.save()
print(f"SVG saved to {output_path.resolve()}")
```

Saat Anda menjalankan skrip, Anda akan melihat pesan konsol yang mengonfirmasi lokasi file yang dihasilkan.

### Output yang Diharapkan

File `circle.svg` yang dihasilkan berisi:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg height="100px" version="1.1" width="100px" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" fill="red"/>
</svg>
```

Membuka file di peramban menampilkan lingkaran merah yang tajam, dan karena berbasis vektor Anda dapat memperbesar tanpa batas tanpa pikselasi.

## Langkah 5: Variasi Umum dan Kasus Tepi

### Mengekspor Vektor yang Lebih Kompleks

Jika Anda perlu **export vector as SVG** untuk ilustrasi multi‑bentuk, cukup ulangi pola `dwg.add()` dengan primitif lain (`rect`, `line`, `path`, dll.). Misalnya:

```python
dwg.add(dwg.rect(insert=(10, 10), size=(30, 30), fill="blue"))
dwg.add(dwg.line(start=(0, 0), end=(100, 100), stroke="black", stroke_width=2))
```

### Menangani Unicode dan Teks

SVG mendukung elemen teks dengan dukungan Unicode penuh. Gunakan `dwg.text("Hello, 🌍", insert=(5, 95), fill="black")` untuk menyematkan label multibahasa.

### Menyimpan ke Lokasi yang Berbeda

Saat **save SVG image** ke folder yang ditentukan pengguna, validasi jalur untuk menghindari kesalahan izin:

```python
if not output_path.parent.exists():
    raise PermissionError(f"Cannot write to {output_path.parent}")
dwg.save()
```

### Memperkecil Output

Untuk pipeline produksi, Anda mungkin menginginkan ukuran file yang lebih kecil. Berikan `pretty=False` ke `dwg.tostring()` dan tulis hasilnya secara manual:

```python
minified = dwg.tostring(pretty=False)
output_path.write_text(minified)
```

## Cara Membuat SVG dengan Library Alternatif (opsional)

Meskipun `svgwrite` ringan dan murni‑Python, ekosistem lain ada:

- **cairosvg** – mengonversi PNG, PDF, atau HTML ke SVG.  
- **lxml** – memungkinkan Anda membangun markup SVG secara manual menggunakan API XML.  

Memilih library tergantung pada kompleksitas proyek Anda dan ketergantungan yang ada.

## Kesimpulan

Anda sekarang tahu cara **create SVG document**, menambahkan bentuk vektor, dan **save SVG file** menggunakan Python. Solusi lengkap ini menunjukkan langkah-langkah untuk **export vector as SVG**, menghasilkan **SVG image**, dan menjawab pertanyaan umum **how to create SVG** secara programatik.

Dari sini Anda dapat:

- Memperluas skrip dengan loop untuk menghasilkan diagram atau ikon secara otomatis.  
- Mengintegrasikan output SVG ke dalam aplikasi web atau templat email.  
- Menjelajahi animasi dengan menambahkan elemen `<animate>` menggunakan `svgwrite`.  

Bereksperimenlah dengan berbagai bentuk, warna, dan gradien untuk sepenuhnya memanfaatkan kekuatan grafik vektor yang dapat diskalakan dalam proyek Python Anda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Buat Dokumen SVG – Tambahkan Lingkaran dan Simpan sebagai SVG](/html/english/python/general/create-svg-document-add-a-circle-and-save-as-svg/)
- [Buat Dokumen SVG di Python – Panduan Mengonversi SVG ke PNG](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)
- [Muat File SVG Python – Panduan Lengkap untuk Mengekspor, Menyematkan & Mengonversi](/html/english/python/general/load-svg-file-python-complete-guide-to-export-embed-convert/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
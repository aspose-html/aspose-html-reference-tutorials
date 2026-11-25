---
category: general
date: 2026-06-16
description: Cara mengubah ukuran SVG di Python dengan cepat – memuat file SVG dengan
  Python, mengedit file SVG dengan Python, dan bahkan mengubah ukuran batch file SVG
  dengan skrip kecil.
draft: false
keywords:
- how to resize svg
- batch resize svg files
- load svg file python
- edit svg file python
language: id
og_description: Bagaimana cara mengubah ukuran SVG di Python? Pelajari cara memuat
  file SVG dengan Python, mengedit file SVG dengan Python, dan mengubah ukuran batch
  file SVG menggunakan contoh yang jelas dan dapat dijalankan.
og_title: Cara Mengubah Ukuran SVG di Python – Tutorial Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to resize SVG in Python quickly – load SVG file Python, edit SVG
    file Python, and even batch resize SVG files with a tiny script.
  headline: How to Resize SVG in Python – Step‑by‑Step Guide
  type: TechArticle
- description: How to resize SVG in Python quickly – load SVG file Python, edit SVG
    file Python, and even batch resize SVG files with a tiny script.
  name: How to Resize SVG in Python – Step‑by‑Step Guide
  steps:
  - name: '**Collects** every `.svg` file in the source folder.'
    text: '**Collects** every `.svg` file in the source folder.'
  - name: '**Loads** each file using the same routine we used for a single SVG.'
    text: '**Loads** each file using the same routine we used for a single SVG.'
  - name: '**Resizes** to the desired width while keeping the aspect ratio.'
    text: '**Resizes** to the desired width while keeping the aspect ratio.'
  - name: '**Writes** the result to a new folder, leaving originals untouched.'
    text: '**Writes** the result to a new folder, leaving originals untouched.'
  type: HowTo
tags:
- Python
- SVG
- Automation
title: Cara Mengubah Ukuran SVG di Python – Panduan Langkah-demi-Langkah
url: /id/python/general/how-to-resize-svg-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengubah Ukuran SVG di Python – Tutorial Lengkap

Pernah bertanya-tanya **bagaimana cara mengubah ukuran SVG** tanpa membuka editor grafis? Mungkin Anda memiliki logo yang harus berukuran lebar 200 px untuk spanduk web, atau Anda sedang menyiapkan puluhan ikon untuk aplikasi seluler. Kabar baiknya? Anda dapat melakukannya semua di Python—tanpa Photoshop, tanpa UI Inkscape, hanya beberapa baris kode.

Dalam panduan ini kami akan menjelaskan cara memuat file SVG di Python, mengedit dimensinya, dan bahkan menskalakan seluruh folder SVG sekaligus. Pada akhir tutorial Anda akan dapat **load SVG file Python**, **edit SVG file Python**, dan **batch resize SVG files** dengan percaya diri.

## Prasyarat

- Python 3.8+ terpasang (perintah `python` standar berfungsi)
- Library `svgwrite` atau `lxml` – kami akan menggunakan `lxml` karena memberikan akses DOM langsung.
- Sebuah folder berisi SVG yang ingin Anda ubah ukurannya (misalnya, `assets/icons/`)

Anda tidak memerlukan alat GUI apa pun; semuanya dijalankan dari terminal.

---

## Langkah 1: Instal Library yang Diperlukan

Pertama, dapatkan `lxml` dari PyPI. Library ini kecil, cepat, dan memungkinkan kita memanipulasi atribut XML secara langsung.

```bash
pip install lxml
```

> **Pro tip:** Jika Anda bekerja dalam lingkungan virtual, aktifkan terlebih dahulu sebelum menjalankan perintah. Ini menjaga ketergantungan proyek tetap rapi.

## Langkah 2: Muat File SVG di Python

Sekarang kita akan **load SVG file Python**—membaca XML, mendapatkan elemen root `<svg>`, dan mencetak ukuran saat ini.

```python
from lxml import etree

def load_svg(path: str) -> etree._ElementTree:
    """
    Load an SVG document and return the parsed XML tree.
    """
    parser = etree.XMLParser(remove_blank_text=True)
    tree = etree.parse(path, parser)
    return tree

# Example usage
svg_path = "assets/logo.svg"
svg_tree = load_svg(svg_path)
root = svg_tree.getroot()
print(f"Original width: {root.get('width')}, height: {root.get('height')}")
```

**Mengapa ini penting:** `lxml` memberi kita DOM yang sesungguhnya, sehingga kita dapat menanyakan atau mengubah atribut apa pun—sempurna untuk tugas **edit SVG file Python**.

## Langkah 3: Ubah Lebar (dan Tinggi) – Cara Mengubah Ukuran SVG

SVG bersifat vektor, jadi Anda dapat mengatur lebar, tinggi, atau keduanya. Jika Anda hanya mengubah lebar, viewBox akan mempertahankan rasio aspek, namun banyak alat juga menghormati atribut tinggi yang sesuai. Berikut helper yang mengubah ukuran sambil mempertahankan rasio aspek asli:

```python
def resize_svg(tree: etree._ElementTree, new_width: int) -> None:
    """
    Resize the root <svg> element to `new_width` while preserving aspect ratio.
    """
    root = tree.getroot()
    # Grab original dimensions (they may be in px, pt, or just numbers)
    orig_width = float(root.get("width").replace("px", ""))
    orig_height = float(root.get("height").replace("px", ""))

    # Compute scale factor and new height
    scale = new_width / orig_width
    new_height = round(orig_height * scale, 2)

    # Update attributes
    root.set("width", f"{new_width}px")
    root.set("height", f"{new_height}px")

    # Optional: ensure viewBox exists for better scaling in browsers
    if "viewBox" not in root.attrib:
        viewbox = f"0 0 {orig_width} {orig_height}"
        root.set("viewBox", viewbox)

# Resize to 200 px wide
resize_svg(svg_tree, 200)
```

Fungsi di atas adalah inti dari **how to resize SVG**. Fungsi ini membaca ukuran saat ini, menghitung tinggi proporsional, dan menulis atribut baru kembali ke file.

## Langkah 4: Simpan SVG yang Dimodifikasi

Setelah mengedit, Anda perlu menulis perubahan kembali ke disk. Ini menyelesaikan siklus **edit SVG file Python**.

```python
def save_svg(tree: etree._ElementTree, destination: str) -> None:
    """
    Write the modified SVG tree to `destination`.
    """
    tree.write(
        destination,
        pretty_print=True,
        xml_declaration=True,
        encoding="UTF-8"
    )
    print(f"Saved resized SVG to {destination}")

# Save as a new file so the original stays untouched
output_path = "assets/logo_resized.svg"
save_svg(svg_tree, output_path)
```

Jalankan seluruh skrip dan Anda akan melihat `logo_resized.svg` baru yang berukuran tepat 200 px lebar.

## Langkah 5: Batch Resize SVG Files – Skala Seluruh Folder

Sekarang karena kita dapat **load SVG file Python**, **edit SVG file Python**, dan menyimpannya, mari iterasi melalui sebuah direktori dan terapkan transformasi yang sama pada setiap file. Ini adalah jawaban untuk **batch resize SVG files**.

```python
import pathlib

def batch_resize(source_dir: str, target_dir: str, width: int) -> None:
    """
    Resize every .svg file in `source_dir` to `width` pixels and store
    the results in `target_dir`.
    """
    src = pathlib.Path(source_dir)
    tgt = pathlib.Path(target_dir)
    tgt.mkdir(parents=True, exist_ok=True)

    svg_files = list(src.glob("*.svg"))
    if not svg_files:
        print("No SVG files found.")
        return

    for svg_path in svg_files:
        try:
            tree = load_svg(str(svg_path))
            resize_svg(tree, width)
            out_path = tgt / svg_path.name
            save_svg(tree, str(out_path))
        except Exception as e:
            print(f"Failed on {svg_path.name}: {e}")

# Example: resize everything in 'assets/icons' to 64 px wide
batch_resize("assets/icons", "assets/icons_resized", 64)
```

### Apa yang dilakukan:

1. **Mengumpulkan** setiap file `.svg` di folder sumber.
2. **Muat** setiap file menggunakan rutinitas yang sama seperti pada satu SVG.
3. **Ubah ukuran** ke lebar yang diinginkan sambil mempertahankan rasio aspek.
4. **Tulis** hasilnya ke folder baru, meninggalkan file asli tidak tersentuh.

Anda kini memiliki pipeline siap pakai untuk **batch resize SVG files**.

## Langkah 6: Kasus Pinggiran & Kesalahan Umum

| Masalah | Mengapa Terjadi | Solusi |
|---------|----------------|--------|
| Atribut `width`/`height` yang hilang | Beberapa SVG hanya mengandalkan `viewBox`. | Jika atribut tidak ada, gunakan dimensi viewBox sebagai cadangan (`viewBox="0 0 w h"`). |
| Unit selain `px` (mis., `pt`, `%`) | Skrip hanya menghapus `px`. | Perluas pemanggilan `replace` atau gunakan regex untuk menangkap unit apa pun. |
| Elemen `<symbol>` atau `<use>` yang kompleks | Mengubah ukuran root mungkin tidak memengaruhi simbol yang bersarang. | Terapkan perubahan atribut yang sama pada setiap tag `<symbol>`, atau gunakan CSS `transform: scale()`. |
| Karakter Unicode atau khusus dalam nama file | `pathlib` menangani sebagian besar kasus, tetapi Windows dapat mengalami masalah dengan karakter tertentu. | Pastikan nama file aman UTF‑8, atau ubah nama sebelum diproses. |

Menangani hal ini sebelumnya akan menyelamatkan Anda dari ikon yang rusak secara tak terduga di kemudian hari.

## Langkah 7: Verifikasi Hasil

Pemeriksaan cepat dapat dilakukan dengan potongan HTML kecil:

```html
<!DOCTYPE html>
<html>
<head><title>SVG Test</title></head>
<body>
  <h3>Original</h3>
  <img src="assets/logo.svg" alt="original logo">
  <h3>Resized</h3>
  <img src="assets/logo_resized.svg" alt="resized logo">
</body>
</html>
```

Buka file di browser—kedua gambar harus terlihat identik, tetapi yang diubah ukurannya akan melaporkan lebar **200 px** di alat pengembang.

---

## Kesimpulan

Anda kini tahu **how to resize SVG** menggunakan Python murni, dari satu file hingga seluruh direktori. Alur kerja mencakup **load SVG file Python**, **edit SVG file Python**, dan **batch resize SVG files**—semua dengan hanya beberapa fungsi.

Cobalah: coba lebar yang berbeda, bereksperimen dengan mengubah ukuran hanya tinggi, atau tambahkan antarmuka baris perintah menggunakan `argparse`. Kemungkinannya tak terbatas, dan skrip ini cukup ringan untuk disematkan dalam pipeline build, pekerjaan CI, atau utilitas desktop.

Ada pertanyaan tentang penanganan gradien, font tersemat, atau mengintegrasikan ini ke dalam aplikasi Flask? Tinggalkan komentar, dan kami akan menjelajahi hal tersebut bersama. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Aspose.HTML के साथ .NET में SVG को इमेज में बदलें](/html/hindi/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [Aspose.HTML के साथ .NET में SVG को PDF में बदलें](/html/hindi/net/canvas-and-image-manipulation/convert-svg-to-pdf/)
- [Aspose.HTML के साथ .NET में SVG दस्तावेज़ को PNG के रूप में प्रस्तुत करें](/html/hindi/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
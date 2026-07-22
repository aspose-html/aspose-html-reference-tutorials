---
category: general
date: 2026-07-21
description: Cara mengedit file SVG menggunakan Python. Pelajari cara memuat SVG,
  mengubah warna isi SVG, dan menguasai manipulasi SVG dengan Python dalam hitungan
  menit.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to edit svg
- change svg fill color
- edit svg with python
- load svg python
- python svg manipulation
language: id
lastmod: 2026-07-21
og_description: Cara mengedit SVG dengan cepat menggunakan Python. Panduan ini menunjukkan
  cara memuat SVG, mengubah warna isi SVG, dan melakukan manipulasi SVG Python tingkat
  lanjut.
og_image_alt: Screenshot showing how to edit SVG fill color using Python
og_title: Cara Mengedit SVG dengan Python – Tutorial Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: How to edit SVG files using Python. Learn to load SVG, change SVG fill
    color, and master python SVG manipulation in minutes.
  headline: How to Edit SVG – Complete Python Guide for Beginners
  type: TechArticle
- description: How to edit SVG files using Python. Learn to load SVG, change SVG fill
    color, and master python SVG manipulation in minutes.
  name: How to Edit SVG – Complete Python Guide for Beginners
  steps:
  - name: Why This Works
    text: '- **`xml.etree.ElementTree`** is part of Python’s standard library, so
      you don’t need extra packages. It parses the SVG as an XML tree, giving you
      direct access to every node. - The `xpath` string includes the SVG namespace
      (`{http://www.w3.org/2000/svg}`) because SVG files are namespaced XML. Witho'
  - name: 1. Editing Multiple Paths at Once
    text: '```python def recolor_all_paths(svg_path: Path, colour: str) -> None: tree
      = ET.parse(svg_path) root = tree.getroot() for path in root.iter("{http://www.w3.org/2000/svg}path"):
      path.set("fill", colour) tree.write(svg_path.with_name(f"{svg_path.stem}_all_{colour.lstrip(''#'')}.svg"))
      ```'
  - name: 2. Preserving Existing Styles
    text: 'Sometimes an element already has a complex `style` attribute like `style="stroke:#000;fill:#fff;"`.
      Overwriting `fill` directly could discard the stroke. To keep everything tidy:'
  - name: 3. Handling SVGs with Embedded Images
    text: If your SVG contains `<image>` tags that reference external raster files,
      changing colours won’t affect them. You’ll need to edit the referenced image
      separately (e.g., with Pillow) and then re‑embed it as a data URI. That’s a
      whole topic on its own, but it’s good to be aware of the limitation.
  type: HowTo
tags:
- svg
- python
- image-processing
- xml
title: Cara Mengedit SVG – Panduan Python Lengkap untuk Pemula
url: /id/python/general/how-to-edit-svg-complete-python-guide-for-beginners/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengedit SVG – Panduan Python Lengkap untuk Pemula

Pernah bertanya‑tanya **cara mengedit SVG** tanpa membuka editor grafis? Mungkin Anda perlu mengubah warna ikon secara cepat atau menghasilkan sekumpulan logo yang disesuaikan untuk kampanye pemasaran. Kabar baiknya, semua itu—and lebih—bisa dilakukan langsung dari Python. Dalam tutorial ini kita akan memandu Anda memuat sebuah SVG, mengubah warna isinya, serta menjelajahi beberapa trik tambahan untuk manipulasi SVG dengan Python yang handal.

Anda akan menyelesaikan panduan ini dengan skrip siap‑jalankan yang mengambil file SVG apa pun, mengganti warna elemen `<path>` pertama menjadi merah terang, dan menulis hasilnya ke file baru. Tanpa GUI eksternal, hanya kode murni.

---

## Apa yang Akan Anda Pelajari

- Cara **memuat SVG** di Python menggunakan modul bawaan `xml.etree.ElementTree`.  
- Cara paling sederhana untuk **mengubah warna isi SVG** dengan satu pembaruan atribut.  
- Bagaimana memperluas pola ini untuk tugas **manipulasi SVG dengan python** yang lebih kompleks (banyak path, gradien, dll.).  
- Tip praktis dan jebakan umum agar SVG Anda tetap valid setelah diedit.

Sebelum kita mulai, pastikan Anda memiliki:

- Python 3.8+ terpasang (library standar sudah cukup).  
- Pemahaman dasar tentang sintaks XML (SVG hanyalah XML).  
- File SVG yang ingin Anda coba – misalnya `logo.svg`.

---

## Cara Mengedit SVG – Panduan Python Langkah demi Langkah

Berikut adalah skrip lengkap yang akan kita bangun secara bertahap. Silakan salin‑tempel ke file bernama `edit_svg.py` dan jalankan setelah Anda memiliki contoh SVG.

```python
#!/usr/bin/env python3
"""
How to edit SVG with Python – change fill colour of the first <path>.
"""

import xml.etree.ElementTree as ET
from pathlib import Path

def edit_svg_fill(
    input_path: Path,
    output_path: Path,
    new_fill: str = "#ff0000",
    xpath: str = ".//{http://www.w3.org/2000/svg}path"
) -> None:
    """
    Load an SVG, change the fill attribute of the first matching element,
    and save the modified SVG.
    
    Parameters
    ----------
    input_path: Path
        Path to the original SVG file.
    output_path: Path
        Path where the edited SVG will be written.
    new_fill: str
        Hex colour string (e.g., '#ff0000' for red).
    xpath: str
        XPath expression targeting the element(s) you want to edit.
    """
    # Step 1: Load the SVG document
    tree = ET.parse(input_path)
    root = tree.getroot()

    # Step 2: Find the first <path> (or any element matching xpath)
    element = root.find(xpath)
    if element is None:
        raise ValueError(f"No element found for xpath '{xpath}'.")
    
    # Step 3: Change its fill colour
    element.set("fill", new_fill)

    # Step 4: Write the modified SVG to a new file
    tree.write(output_path, encoding="utf-8", xml_declaration=True)
    print(f"✅ Saved edited SVG to {output_path}")

if __name__ == "__main__":
    # Example usage – adjust paths as needed
    src = Path("YOUR_DIRECTORY/logo.svg")
    dst = Path("YOUR_DIRECTORY/logo_modified.svg")
    edit_svg_fill(src, dst, new_fill="#ff0000")
```

### Mengapa Ini Berfungsi

- **`xml.etree.ElementTree`** merupakan bagian dari library standar Python, jadi Anda tidak memerlukan paket tambahan. Ia mem‑parse SVG sebagai pohon XML, memberi Anda akses langsung ke setiap node.  
- String `xpath` menyertakan namespace SVG (`{http://www.w3.org/2000/svg}`) karena file SVG adalah XML yang bernamespace. Tanpa itu, `find()` akan mengembalikan `None`.  
- Dengan memanggil `element.set("fill", new_fill)`, kita **mengubah warna isi SVG** secara langsung. Atribut tersebut ditulis kembali ketika kita memanggil `tree.write()`.

Jalankan skrip dan buka `logo_modified.svg` di browser – Anda akan melihat path pertama kini berwarna merah.

---

## Mengubah Warna Isi SVG – Variasi Satu Baris

Jika Anda hanya perlu **mengubah warna isi SVG** untuk elemen dengan ID yang sudah diketahui, Anda dapat memotong beberapa baris dari fungsi:

```python
import xml.etree.ElementTree as ET

tree = ET.parse("logo.svg")
root = tree.getroot()
root.find(".//{http://www.w3.org/2000/svg}path[@id='myShape']").set("fill", "#00ff00")
tree.write("logo_green.svg")
```

- XPath `[@id='myShape']` menargetkan `<path>` tertentu berdasarkan atribut `id`‑nya.  
- Pendekatan ini berguna ketika Anda memiliki template SVG dengan ID yang dapat diprediksi.

**Tip:** Selalu periksa kembali bahwa elemen tersebut memang memiliki atribut `fill`; jika tidak, atribut baru akan ditambahkan secara otomatis.

---

## Memuat SVG di Python – Hal yang Perlu Diketahui

Ketika kita membicarakan **load SVG python**, kuncinya adalah menangani namespace dengan benar. Banyak pemula lupa bahwa setiap tag SVG berada di dalam namespace `http://www.w3.org/2000/svg`, itulah mengapa sintaks kurung kurawal muncul di XPath. Berikut cheat‑sheet singkatnya:

| Tugas | Potongan Kode |
|------|--------------|
| Mem‑parse file SVG | `tree = ET.parse("file.svg")` |
| Mendapatkan elemen root | `root = tree.getroot()` |
| Menemukan semua elemen `<rect>` | `rects = root.findall(".//{http://www.w3.org/2000/svg}rect")` |
| Iterasi dan mencetak atribut | `for r in rects: print(r.attrib)` |

Jika Anda lebih suka library tingkat‑lebih‑tinggi, `svgwrite` atau `cairosvg` juga dapat **load SVG with Python**, tetapi mereka menambah dependensi. Untuk perubahan atribut sederhana, alat XML bawaan sudah lebih dari cukup.

---

## Tips Manipulasi SVG dengan Python Tingkat Lanjut

Sekarang Anda sudah menguasai dasar‑dasar **python svg manipulation**, mari jelajahi beberapa skenario yang mungkin Anda temui.

### 1. Mengedit Banyak Path Sekaligus

```python
def recolor_all_paths(svg_path: Path, colour: str) -> None:
    tree = ET.parse(svg_path)
    root = tree.getroot()
    for path in root.iter("{http://www.w3.org/2000/svg}path"):
        path.set("fill", colour)
    tree.write(svg_path.with_name(f"{svg_path.stem}_all_{colour.lstrip('#')}.svg"))
```

- `root.iter()` menelusuri seluruh pohon, sehingga setiap `<path>` mendapatkan warna baru.  
- Nama file output dihasilkan secara otomatis, memudahkan pemrosesan batch.

### 2. Mempertahankan Gaya yang Sudah Ada

Kadang sebuah elemen sudah memiliki atribut `style` kompleks seperti `style="stroke:#000;fill:#fff;"`. Menimpa `fill` secara langsung dapat menghilangkan stroke. Untuk menjaga semuanya tetap rapi:

```python
def update_fill_preserve_style(elem: ET.Element, new_fill: str) -> None:
    style = elem.get("style", "")
    # Split existing style into dict
    style_dict = dict(item.split(":") for item in style.split(";") if item)
    style_dict["fill"] = new_fill
    # Re‑join into a string
    elem.set("style", ";".join(f"{k}:{v}" for k, v in style_dict.items()))
```

Gunakan helper ini di dalam loop apa pun yang menyentuh elemen dengan CSS inline.

### 3. Menangani SVG dengan Gambar Tersemat

Jika SVG Anda berisi tag `<image>` yang merujuk ke file raster eksternal, mengubah warna tidak akan memengaruhi mereka. Anda harus mengedit gambar yang dirujuk secara terpisah (misalnya dengan Pillow) lalu menyematkannya kembali sebagai data URI. Itu topik tersendiri, tetapi penting untuk diketahui adanya keterbatasan ini.

---

## Jebakan Umum & Cara Menghindarinya

- **Ketidaksesuaian namespace** – Lupa menambahkan namespace SVG adalah penyebab paling sering `None` dikembalikan oleh `find()`. Selalu awali namespace dalam kurung kurawal.  
- **Atribut `fill` tidak ada** – Jika elemen mengandalkan kelas CSS, penetapan atribut mungkin tidak berpengaruh visual. Dalam kasus itu, tambahkan atribut `style` atau ubah stylesheet yang terhubung.  
- **Menyimpan tanpa deklarasi XML** – Beberapa browser bingung dengan SVG yang tidak memiliki baris `<?xml version="1.0"?>`. Menggunakan `tree.write(..., xml_declaration=True)` menyelesaikannya.  
- **Masalah encoding** – Gunakan UTF‑8 saat menulis kembali ke file; jika tidak, Anda dapat merusak karakter non‑ASCII di node teks.

---

## Ringkasan Contoh Skrip Lengkap

Menggabungkan semuanya, berikut skrip minimal yang memperlihatkan **cara mengedit SVG** dari awal hingga akhir:

```python
import xml.etree.ElementTree as ET
from pathlib import Path

def main():
    src = Path("example.svg")
    dst = Path("example_red.svg")
    # Load SVG
    tree = ET.parse(src)
    root = tree.getroot()
    # Change first path fill to red
    first_path = root.find(".//{http://www.w3.org/2000/svg}path")
    if first_path is not None:
        first_path.set("fill", "#ff0000")
    else:
        raise RuntimeError("No <path> element found in the SVG.")
    # Save result
    tree.write(dst, encoding="utf-8", xml_declaration=True)
    print(f"Edited SVG saved to {dst}")

if __name__ == "__main__":
    main()
```

**Output yang diharapkan** ketika Anda membuka `example_red.svg` di browser: bentuk pertama yang Anda lihat di file asli kini berwarna merah terang, sementara sisanya tetap tidak berubah.

---

## Kesimpulan

Kami telah membahas **cara mengedit SVG** menggunakan Python dari nol: memuat file, menemukan elemen, mengubah warna isinya, dan menyimpan hasilnya. Anda juga telah melihat cara memperluas pendekatan untuk recolouring batch, mempertahankan aturan gaya yang ada, serta menghindari masalah namespace yang paling umum. Dengan alat‑alat ini di kotak perkakas Anda, manipulasi SVG dengan python menjadi bagian yang mudah dari pipeline aset atau aplikasi dinamis apa pun.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikutnya membahas topik terkait yang memperluas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Mengonversi SVG ke XPS dengan Aspose.HTML untuk Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)
- [Aspose.HTML के साथ .NET में SVG को PDF में बदलें](/html/hindi/net/canvas-and-image-manipulation/convert-svg-to-pdf/)
- [Aspose.HTML के साथ .NET में SVG दस्तावेज़ को PNG के रूप में प्रस्तुत करें](/html/hindi/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
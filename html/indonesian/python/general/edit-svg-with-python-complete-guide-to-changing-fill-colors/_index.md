---
category: general
date: 2026-06-26
description: Edit SVG dengan Python secara cepat. Pelajari cara memuat dokumen SVG
  di Python, mengubah isian SVG secara programatik, dan mengatur atribut isian SVG
  hanya dalam beberapa baris.
draft: false
keywords:
- edit svg with python
- change svg fill programmatically
- load svg document python
- set svg fill attribute
language: id
og_description: Edit SVG dengan Python dengan memuat dokumen SVG, mengubah warna isi
  secara programatik, dan menyimpan hasilnya. Panduan praktis untuk pengembang.
og_title: Edit SVG dengan Python – Panduan Langkah-demi-Langkah Mengubah Warna Isi
schemas:
- author: Aspose
  dateModified: '2026-06-26'
  description: Edit SVG with Python quickly. Learn how to load SVG document python,
    change SVG fill programmatically and set SVG fill attribute in just a few lines.
  headline: Edit SVG with Python – Complete Guide to Changing Fill Colors
  type: TechArticle
tags:
- svg
- python
- graphics-manipulation
title: Edit SVG dengan Python – Panduan Lengkap untuk Mengubah Warna Isi
url: /id/python/general/edit-svg-with-python-complete-guide-to-changing-fill-colors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Edit SVG dengan Python – Panduan Lengkap Mengubah Warna Isi

Pernah perlu mengedit SVG dengan Python tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian. Baik Anda sedang menyesuaikan warna logo untuk penyegaran merek atau menghasilkan ikon secara dinamis, mempelajari cara **load SVG document python** dan memanipulasi atributnya adalah keterampilan yang berguna. Dalam tutorial ini kami akan menelusuri contoh singkat yang praktis yang menunjukkan cara **change SVG fill programmatically** dan **set SVG fill attribute** tanpa meninggalkan skrip Anda.

Kami akan membahas semuanya mulai dari parsing file, menemukan elemen `<path>` yang tepat, memperbarui warnanya, dan akhirnya menulis kembali SVG yang telah dimodifikasi ke disk. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat dipakai ulang dalam proyek apa pun, dan Anda akan memahami “mengapa” di balik setiap langkah sehingga dapat menyesuaikannya dengan struktur SVG yang lebih kompleks.

## Prerequisites

- Python 3.8+ terpasang (perpustakaan standar sudah cukup)
- File SVG dasar (kami akan menggunakan `logo.svg` sebagai contoh)
- Familiaritas dengan list dan dictionary Python (opsional tetapi membantu)

Tidak ada dependensi eksternal yang diperlukan; kami akan mengandalkan `xml.etree.ElementTree`, yang sudah termasuk dalam Python. Jika Anda lebih suka perpustakaan tingkat tinggi seperti `svgwrite`, Anda dapat menyesuaikan kode – gagasan intinya tetap sama.

## Step 1: Load the SVG Document (load svg document python)

Hal pertama yang harus Anda lakukan adalah membaca file SVG ke dalam memori. Anggaplah SVG hanyalah dokumen XML, sehingga `ElementTree` melakukan pekerjaan beratnya.

```python
import xml.etree.ElementTree as ET
from pathlib import Path

# Define the path to your original SVG
svg_path = Path("YOUR_DIRECTORY/logo.svg")

# Parse the SVG file – this gives us a tree we can walk through
tree = ET.parse(svg_path)
root = tree.getroot()
```

> **Why this matters:** Dengan memuat SVG ke dalam sebuah `ElementTree`, Anda mendapatkan akses acak ke setiap node. Itulah dasar bagi alur kerja **edit svg with python** apa pun.

### Pro tip
Jika SVG Anda menggunakan namespace (sebagian besar melakukannya), Anda perlu mendaftarkannya agar `findall` berfungsi dengan benar. Potongan kode di bawah ini menangkap namespace default secara otomatis:

```python
ns = {"svg": root.tag.split("}")[0].strip("{")}
```

## Step 2: Locate the First `<path>` Element (change svg fill programmatically)

Setelah dokumen berada di memori, kita perlu menemukan elemen yang isinya ingin diubah. Pada banyak ikon sederhana warna disimpan pada tag `<path>` pertama, tetapi Anda dapat menyesuaikan XPath untuk menargetkan elemen mana pun.

```python
# Retrieve all <path> elements – adjust the tag if you need <rect>, <circle>, etc.
paths = root.findall(".//svg:path", ns)

if not paths:
    raise ValueError("No <path> elements found in the SVG.")
    
first_path = paths[0]  # Grab the first one for this example
```

> **Why this step is crucial:** Mengakses elemen secara langsung memungkinkan Anda **set svg fill attribute** tanpa menebak posisinya dalam file. Kode ini aman – ia akan mengeluarkan error yang jelas jika tidak ada path, yang membantu Anda melakukan debug lebih awal.

## Step 3: Change Its Fill Colour (set svg fill attribute)

Mengubah warna semudah memperbarui atribut `fill` pada elemen tersebut. Warna SVG menerima format warna CSS apa pun, jadi `#ff6600` berfungsi dengan baik.

```python
new_fill = "#ff6600"  # Bright orange – pick whatever you like
first_path.set("fill", new_fill)
```

Jika elemen sudah memiliki atribut `style` yang berisi deklarasi `fill:`, Anda mungkin perlu memodifikasi string tersebut sebagai gantinya. Berikut helper singkat yang menangani kedua kasus:

```python
def set_fill(element, colour):
    if "fill" in element.attrib:
        element.set("fill", colour)
    elif "style" in element.attrib:
        # Replace any existing fill in the style string
        style = element.attrib["style"]
        new_style = ";".join(
            part if not part.strip().startswith("fill:") else f"fill:{colour}"
            for part in style.split(";")
        )
        element.set("style", new_style)
    else:
        # No fill defined – just add it
        element.set("fill", colour)

set_fill(first_path, new_fill)
```

> **Why we handle `style` too:** Beberapa editor SVG menanamkan CSS secara inline di dalam atribut `style`. Mengabaikannya akan membuat warna visual tidak berubah, sehingga tujuan **change svg fill programmatically** tidak tercapai.

## Step 4: Save the Modified SVG (edit svg with python)

Setelah mengubah atribut, langkah terakhir adalah menulis kembali pohon ke file. Anda dapat menimpa file asli atau membuat versi baru – yang terakhir lebih aman untuk kontrol versi.

```python
output_path = Path("YOUR_DIRECTORY/logo_modified.svg")
tree.write(output_path, encoding="utf-8", xml_declaration=True)

print(f"Modified SVG saved to {output_path}")
```

File yang dihasilkan akan terlihat hampir identik dengan sumbernya, kecuali `<path>` pertama kini membawa nilai `fill` yang baru.

### Expected Output

Jika Anda membuka `logo_modified.svg` di browser atau penampil SVG, bentuk yang semula berwarna hitam (atau warna apa pun) kini akan muncul dengan warna oranye terang `#ff6600`. Semua elemen lain tetap tidak berubah.

## Step 5: Wrap It Up in a Reusable Function (edit svg with python)

Agar pola ini dapat dipakai ulang di berbagai proyek, mari enkapsulasi logika dalam sebuah fungsi tunggal. Ini membuat kode DRY dan memungkinkan Anda mengubah warna isi elemen apa pun dengan memberikan ekspresi XPath.

```python
def edit_svg_fill(
    source_file: Path,
    target_file: Path,
    xpath: str,
    colour: str,
    namespace: dict = None,
) -> None:
    """
    Load an SVG, change the fill colour of the element(s) matched by `xpath`,
    and write the result to `target_file`.

    Parameters
    ----------
    source_file : Path
        Path to the original SVG.
    target_file : Path
        Path where the modified SVG will be saved.
    xpath : str
        XPath expression to locate the element(s) (e.g., ".//svg:path").
    colour : str
        New fill colour (any CSS colour format).
    namespace : dict, optional
        Namespace mapping for the SVG; auto‑detected if omitted.
    """
    tree = ET.parse(source_file)
    root = tree.getroot()
    ns = namespace or {"svg": root.tag.split("}")[0].strip("{")}
    elements = root.findall(xpath, ns)

    if not elements:
        raise ValueError(f"No elements found for XPath: {xpath}")

    for el in elements:
        set_fill(el, colour)

    tree.write(target_file, encoding="utf-8", xml_declaration=True)

# Example usage:
edit_svg_fill(
    source_file=Path("YOUR_DIRECTORY/logo.svg"),
    target_file=Path("YOUR_DIRECTORY/logo_modified.svg"),
    xpath=".//svg:path",
    colour="#ff6600",
)
```

> **Why wrap it?** Fungsi seperti ini memungkinkan Anda **load svg document python**, **set svg fill attribute**, dan **change svg fill programmatically** untuk SVG apa pun, bukan hanya path pertama. Ini juga memudahkan pembuatan pipeline otomatis (misalnya job CI yang menghasilkan aset merek) menjadi sangat sederhana.

## Common Pitfalls & Edge Cases

| Masalah | Mengapa Terjadi | Cara Memperbaiki |
|-------|----------------|-----------|
| **Kesalahan namespace** | File SVG sering mendeklarasikan namespace default, sehingga `findall` mengembalikan daftar kosong. | Ekstrak namespace dari `root.tag` seperti yang ditunjukkan, atau gunakan `ET.register_namespace('', ns_uri)`. |
| **Beberapa fill di atribut `style`** | String `style` dapat berisi beberapa properti CSS; penggantian naïf dapat merusak style lain. | Gunakan helper `set_fill` yang mem-parsing string style dan hanya mengganti bagian `fill:`. |
| **Elemen bukan `<path>`** | Beberapa ikon menggunakan `<rect>`, `<circle>`, atau `<polygon>` untuk bentuknya. | Ubah XPath (`".//svg:rect"` dll.) atau berikan selector yang lebih umum seperti `".//*"` dan filter berdasarkan atribut. |
| **Format warna tidak cocok** | Memberikan `rgb(255,102,0)` ketika file mengharapkan hex dapat menyebabkan anomali render pada browser lama. | Gunakan hex (`#ff6600`) untuk kompatibilitas maksimal, atau uji output di lingkungan target Anda. |

## Bonus: Batch‑Processing a Folder of SVGs

Jika Anda perlu mewarnai ulang seluruh kit merek, loop singkat dapat menyelesaikannya:

```python
from pathlib import Path

svg_folder = Path("YOUR_DIRECTORY/icons")
for svg_file in svg_folder.glob("*.svg"):
    out_file = svg_folder / f"{svg_file.stem}_orange.svg"
    edit_svg_fill(
        source_file=svg_file,
        target_file=out_file,
        xpath=".//svg:path",
        colour="#ff6600",
    )
    print(f"Processed {svg_file.name}")
```

Sekarang Anda memiliki satu baris kode yang **edit svg with python** pada puluhan file – sempurna untuk penyegaran merek yang cepat.

## Conclusion

Anda baru saja mempelajari cara **edit SVG with Python** dari awal hingga akhir: memuat SVG, menemukan elemen, **changing the SVG fill programmatically**, dan akhirnya **saving the modified file**. Teknik inti bergantung pada parsing pohon XML, memperbarui atribut `fill` (atau string `style`) secara aman, dan menulis kembali hasilnya. Dengan fungsi `edit_svg_fill` yang dapat dipakai ulang di kotak peralatan Anda, Anda dapat mengotomatisasi pergantian warna untuk aset SVG apa pun, mengintegrasikan proses ke dalam pipeline build, atau membuat layanan web kecil yang menyajikan ikon yang disesuaikan secara dinamis.

Apa selanjutnya? Cobalah memperluas fungsi untuk memodifikasi warna stroke, menambahkan gradien, atau bahkan menyisipkan elemen `<text>` baru. Spesifikasi SVG sangat kaya, dan perpustakaan XML Python memberi Anda kontrol penuh. Jika Anda menemui namespace yang rumit atau harus menangani SVG kompleks yang dihasilkan Illustrator, prinsip yang sama tetap berlaku – cukup sesuaikan XPath dan penanganan namespace.

Jangan ragu bereksperimen, berbagi temuan, atau mengajukan pertanyaan di kolom komentar. Selamat coding, dan nikmati dunia berwarna dari manipulasi SVG secara programatik! 

![Contoh Edit SVG dengan Python](https://example.com/placeholder-image.png "Contoh Edit SVG dengan Python")


## What Should You Learn Next?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Simpan Dokumen SVG di Aspose.HTML untuk Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Render dokumen SVG sebagai PNG di .NET dengan Aspose.HTML](/html/dutch/net/rendering-html-documents/render-svg-doc-as-png/)
- [svg ke png java – ubah SVG menjadi gambar dengan Aspose.HTML for Java](/html/hindi/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
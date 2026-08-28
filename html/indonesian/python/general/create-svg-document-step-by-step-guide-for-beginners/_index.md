---
category: general
date: 2026-07-02
description: Buat dokumen SVG dengan cepat menggunakan Python. Pelajari cara menyimpan
  file SVG, menghasilkan gambar SVG dasar, dan mengekspor SVG dari kode hanya dalam
  beberapa baris.
draft: false
keywords:
- create svg document
- save svg file
- how to generate svg
- export svg from code
- create basic svg image
language: id
og_description: Buat dokumen SVG dengan mudah. Panduan ini menunjukkan cara menghasilkan
  SVG, menyimpan file SVG, dan mengekspor SVG dari kode dengan contoh Python yang
  bersih.
og_title: Buat Dokumen SVG – Tutorial Python Cepat
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Create SVG document quickly with Python. Learn to save SVG file, generate
    a basic SVG image, and export SVG from code in just a few lines.
  headline: Create SVG Document – Step‑by‑Step Guide for Beginners
  type: TechArticle
- description: Create SVG document quickly with Python. Learn to save SVG file, generate
    a basic SVG image, and export SVG from code in just a few lines.
  name: Create SVG Document – Step‑by‑Step Guide for Beginners
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: How can I add text or other shapes?
    text: Just call `svg.create_element("text", {...})` or `svg.create_element("circle",
      {...})` and append them just like the rectangle. The same **how to generate
      SVG** logic applies.
  - name: What if I need to **export SVG from code** with a transparent background?
    text: Remove any `fill` attribute from the root `<svg>` element or set `fill="none"`
      on shapes that should be transparent. The XML stays valid; browsers will render
      the transparency automatically.
  - name: Can I **save SVG file** with pretty‑printed formatting?
    text: '`ElementTree` writes compact XML by default. For a human‑readable version,
      you can use `xml.dom.minidom` to re‑format:'
  - name: What about performance for large SVGs?
    text: When generating thousands of elements, consider building a list of `ET.Element`
      objects first and then extending the root in one go. This reduces the number
      of tree mutations and speeds up the **save SVG file** operation.
  type: HowTo
tags:
- SVG
- Python
- Graphics
- File I/O
title: Buat Dokumen SVG – Panduan Langkah-demi-Langkah untuk Pemula
url: /id/python/general/create-svg-document-step-by-step-guide-for-beginners/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Dokumen SVG – Panduan Langkah‑ demi‑Langkah untuk Pemula

Pernah bertanya-tanya bagaimana cara **create SVG document** tanpa membuka editor grafis? Anda tidak sendirian. Baik Anda membutuhkan ikon kecil untuk halaman web atau diagram dinamis yang dihasilkan secara otomatis, kemampuan untuk **create SVG document** secara programatik menghemat waktu dan menjaga semuanya terkendali versi.

Dalam tutorial ini kami akan membimbing Anda melalui contoh lengkap yang dapat dijalankan yang menunjukkan secara tepat cara **create SVG document**, **save SVG file**, dan bahkan menjawab pertanyaan yang terus muncul “**how to generate SVG**” ketika Anda mengotomatisasi grafik. Pada akhir tutorial Anda akan memiliki sebuah kotak merah di disk, dan Anda akan tahu cara **export SVG from code** untuk proyek selanjutnya.

## Apa yang Anda Butuhkan

* Python 3.9 atau lebih baru (perpustakaan standar melakukan semua pekerjaan berat)
* Editor teks atau IDE yang Anda suka—VS Code, PyCharm, atau bahkan Notepad sudah cukup
* Izin menulis ke folder tempat Anda akan **save SVG file** (kami akan menggunakan direktori `output/`)

Tidak diperlukan paket eksternal, jadi penyiapannya hanya beberapa menit.

## Langkah 1: Siapkan Fungsi Pembantu SVG (Buat Dokumen)

Pertama-tama: kita membutuhkan pembantu kecil yang membangun struktur XML di balik sebuah SVG. Anggap ini sebagai kanvas tempat kita nanti akan **create basic SVG image** elemen.

```python
import pathlib
import xml.etree.ElementTree as ET

# ----------------------------------------------------------------------
# Helper class that mimics a minimal SVG library.
# ----------------------------------------------------------------------
class SVGDocument:
    """Simple wrapper to generate an SVG document using ElementTree."""
    
    SVG_NS = "http://www.w3.org/2000/svg"
    def __init__(self, width: int = 200, height: int = 200):
        # Register the SVG namespace so the output looks clean
        ET.register_namespace("", self.SVG_NS)
        self.root = ET.Element(
            "svg",
            attrib={
                "xmlns": self.SVG_NS,
                "width": str(width),
                "height": str(height),
                "version": "1.1"
            }
        )
    
    def create_element(self, tag: str, attributes: dict) -> ET.Element:
        """Create an SVG element with the given attributes."""
        return ET.Element(tag, attrib=attributes)
    
    def append_child(self, element: ET.Element):
        """Append a child element to the root <svg> node."""
        self.root.append(element)
    
    def save(self, file_path: str):
        """Write the SVG XML to a file, creating directories as needed."""
        path = pathlib.Path(file_path)
        path.parent.mkdir(parents=True, exist_ok=True)
        tree = ET.ElementTree(self.root)
        tree.write(str(path), encoding="utf-8", xml_declaration=True)
```

**Mengapa langkah ini penting:** Kelas `SVGDocument` mengabstraksi kerumitan XML tingkat rendah. Dengan membungkusnya dalam sebuah kelas, kita menjaga sisa kode tetap bersih, yang merupakan praktik terbaik ketika Anda **export SVG from code** dalam aplikasi yang lebih besar.

## Langkah 2: Tambahkan Persegi Panjang – Inti dari Contoh **Create Basic SVG Image**

Sekarang kita memiliki objek dokumen, mari tambahkan sebuah kotak merah. Ini adalah inti dari bagian **create basic SVG image** dalam tutorial.

```python
# ----------------------------------------------------------------------
# Step 2: Build the SVG content
# ----------------------------------------------------------------------
svg = SVGDocument(width=120, height=120)   # canvas size a little larger than the square

# Define rectangle attributes: 100x100 size, red fill, positioned at (10,10)
rect_attrs = {
    "x": "10",
    "y": "10",
    "width": "100",
    "height": "100",
    "fill": "red"
}

# Create the <rect> element and attach it to the SVG root
rect_element = svg.create_element("rect", rect_attrs)
svg.append_child(rect_element)
```

**Penjelasan:**  
* Koordinat `x` dan `y` persegi panjang memberikan margin 10‑pixel sehingga tidak menempel pada tepi.  
* Menggunakan kamus untuk atribut membuat kode mudah dibaca dan mencerminkan cara Anda **save SVG file** atribut dalam format berbasis XML apa pun.  
* Jika Anda pernah perlu **how to generate SVG** bentuk selain persegi panjang, cukup ubah tag menjadi `"circle"` atau `"path"` dan sesuaikan kamus atributnya.

## Langkah 3: Simpan SVG – Akhirnya **Save SVG File** ke Disk

Kami telah membangun dokumen di memori; sekarang kami akan menuliskannya. Inilah saat di mana **create SVG document** yang abstrak menjadi file nyata yang dapat Anda buka di peramban.

```python
# ----------------------------------------------------------------------
# Step 3: Persist the SVG to the filesystem
# ----------------------------------------------------------------------
output_path = "output/square.svg"
svg.save(output_path)

print(f"✅ SVG saved! Open {output_path} in any browser to see the red square.")
```

**Apa yang akan Anda lihat:** Membuka `output/square.svg` di Chrome, Firefox, atau penampil SVG apa pun akan menampilkan sebuah kotak merah sederhana dengan batas putih tipis (latar belakang kanvas SVG). Itu bukti bahwa kami berhasil **exported SVG from code**.

## Skrip Lengkap – Solusi Satu‑File

Berikut adalah seluruh skrip, siap untuk disalin‑tempel ke `create_svg.py`. Menjalankan `python create_svg.py` akan menghasilkan file yang dijelaskan di atas.

```python
import pathlib
import xml.etree.ElementTree as ET

class SVGDocument:
    """Simple wrapper to generate an SVG document using ElementTree."""
    SVG_NS = "http://www.w3.org/2000/svg"
    def __init__(self, width: int = 200, height: int = 200):
        ET.register_namespace("", self.SVG_NS)
        self.root = ET.Element(
            "svg",
            attrib={
                "xmlns": self.SVG_NS,
                "width": str(width),
                "height": str(height),
                "version": "1.1"
            }
        )
    def create_element(self, tag: str, attributes: dict) -> ET.Element:
        return ET.Element(tag, attrib=attributes)
    def append_child(self, element: ET.Element):
        self.root.append(element)
    def save(self, file_path: str):
        path = pathlib.Path(file_path)
        path.parent.mkdir(parents=True, exist_ok=True)
        tree = ET.ElementTree(self.root)
        tree.write(str(path), encoding="utf-8", xml_declaration=True)

# -------------------- Build the SVG --------------------
svg = SVGDocument(width=120, height=120)

rect_attrs = {
    "x": "10",
    "y": "10",
    "width": "100",
    "height": "100",
    "fill": "red"
}
svg.append_child(svg.create_element("rect", rect_attrs))

# -------------------- Save the file --------------------
output_path = "output/square.svg"
svg.save(output_path)

print(f"✅ SVG saved! Open {output_path} in any browser to see the red square.")
```

### Output yang Diharapkan

Menjalankan skrip mencetak:

```
✅ SVG saved! Open output/square.svg in any browser to see the red square.
```

Dan `square.svg` yang dihasilkan terlihat seperti ini (tampilan disederhanakan):

```xml
<?xml version='1.0' encoding='utf-8'?>
<svg xmlns="http://www.w3.org/2000/svg" width="120" height="120" version="1.1">
  <rect x="10" y="10" width="100" height="100" fill="red" />
</svg>
```

Membuka file menampilkan kotak merah yang tajam—tepat seperti yang kami maksudkan dengan **create basic SVG image**.

## Memperluas Contoh – Pertanyaan Umum Terjawab

### Bagaimana saya dapat menambahkan teks atau bentuk lain?

Cukup panggil `svg.create_element("text", {...})` atau `svg.create_element("circle", {...})` dan tambahkan mereka seperti persegi panjang. Logika **how to generate SVG** yang sama berlaku.

### Bagaimana jika saya perlu **export SVG from code** dengan latar belakang transparan?

Hapus atribut `fill` apa pun dari elemen root `<svg>` atau setel `fill="none"` pada bentuk yang harus transparan. XML tetap valid; peramban akan menampilkan transparansi secara otomatis.

### Bisakah saya **save SVG file** dengan format pretty‑printed?

`ElementTree` menulis XML yang kompak secara default. Untuk versi yang dapat dibaca manusia, Anda dapat menggunakan `xml.dom.minidom` untuk memformat ulang:

```python
import xml.dom.minidom as minidom

def pretty_save(svg_doc, path):
    rough_string = ET.tostring(svg_doc.root, 'utf-8')
    reparsed = minidom.parseString(rough_string)
    with open(path, 'w', encoding='utf-8') as f:
        f.write(reparsed.toprettyxml(indent="  "))
```

Ganti `svg.save(output_path)` dengan `pretty_save(svg, output_path)`.

### Bagaimana dengan kinerja untuk SVG besar?

Saat menghasilkan ribuan elemen, pertimbangkan untuk membangun daftar objek `ET.Element` terlebih dahulu dan kemudian memperluas root sekaligus. Ini mengurangi jumlah mutasi pohon dan mempercepat operasi **save SVG file**.

## Tips Pro & Jebakan

* **Pro tip:** Selalu gunakan path absolut (atau `pathlib.Path`) saat **saving SVG file**; path relatif dapat rusak ketika skrip Anda dijalankan dari direktori kerja yang berbeda.  
* **Waspadai:** Lupa mendaftarkan namespace SVG. Tanpa `ET.register_namespace("", SVGDocument.SVG_NS)`, output akan berisi prefiks `ns0` yang berlebih dan beberapa peramban dapat menafsirkannya secara salah.  
* **Kesalahan umum:** Mencampur tipe integer dan string dalam nilai atribut. XML mengharapkan string, jadi kami mengubah semuanya dengan `str()`—kelas pembantu melakukan ini untuk Anda, tetapi jika Anda melewatinya, Anda mungkin mendapatkan `TypeError`.  

## Kesimpulan

Kami baru saja melewati contoh lengkap, end‑to‑end yang menunjukkan cara **create SVG document**, **save SVG file**, dan menjawab

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-08-06
description: Konversi HTML ke PDF dalam Python dengan contoh lengkap. Pelajari cara
  menghasilkan PDF dari HTML, menyimpan HTML sebagai PDF, dan menangani kasus tepi
  umum.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to pdf
- generate pdf from html
- save html as pdf
- create pdf from html file
- how to convert html to pdf
language: id
lastmod: 2026-08-06
og_description: Konversi HTML ke PDF dengan Python dan otomatisasi pembuatan dokumen.
  Ikuti panduan ini untuk menghasilkan PDF dari HTML, menyimpan HTML sebagai PDF,
  dan menyesuaikan output.
og_image_alt: Example of convert html to pdf script in Python
og_title: Mengonversi HTML ke PDF dengan Python – tutorial komprehensif
schemas:
- author: Aspose
  dateModified: '2026-08-06'
  description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  headline: Convert HTML to PDF in Python – step‑by‑step guide
  type: TechArticle
- description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  name: Convert HTML to PDF in Python – step‑by‑step guide
  steps:
  - name: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
    text: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
  - name: '**Input handling** – read the HTML file or build the markup programmatically.'
    text: '**Input handling** – read the HTML file or build the markup programmatically.'
  - name: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
    text: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
  type: HowTo
tags:
- HTML to PDF
- Python
- Document conversion
title: Mengonversi HTML ke PDF dengan Python – panduan langkah demi langkah
url: /id/python/general/convert-html-to-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengonversi HTML ke PDF dengan Python – panduan langkah demi langkah

Jika Anda perlu **mengonversi HTML ke PDF** dengan cepat, tutorial ini menunjukkan solusi lengkap dalam Python. Anda akan melihat cara menghasilkan PDF dari HTML, menyimpan HTML sebagai PDF, dan mengendalikan proses konversi tanpa meninggalkan kode Anda.

Panduan ini membawa Anda melalui instalasi pustaka yang handal, memuat dokumen HTML, melakukan konversi, dan memverifikasi hasilnya. Pada akhir tutorial Anda dapat membuat PDF dari file HTML dalam proyek Python apa pun, baik sumbernya berupa halaman statis maupun markup yang dihasilkan secara dinamis.

## Apa yang akan Anda pelajari

* Instal dependensi `pdfkit` dan `wkhtmltopdf` yang diperlukan untuk konversi HTML‑ke‑PDF.  
* Muat dokumen HTML dari disk atau string.  
* Hasilkan PDF dari HTML dengan ukuran halaman, margin, dan opsi encoding yang dapat disesuaikan.  
* Simpan HTML sebagai PDF menggunakan satu pemanggilan fungsi.  
* Tangani kasus tepi umum seperti aset yang hilang, karakter Unicode, dan file berukuran besar.  

**Prasyarat** – Python 3.8+ dan pemahaman dasar tentang I/O file. Tidak diperlukan layanan eksternal.

## Mengonversi HTML ke PDF – alur kerja keseluruhan

Proses konversi terdiri dari tiga fase logis:

1. **Persiapan** – instal konverter dan pastikan binary `wkhtmltopdf` dapat dijangkau.  
2. **Penanganan input** – baca file HTML atau bangun markup secara programatik.  
3. **Pembuatan output** – panggil konverter, tulis file PDF, dan konfirmasi hasil.

Setiap fase dibahas dalam langkah khusus di bawah ini.

## Langkah 1: Instal pustaka yang diperlukan

`pdfkit` menyediakan wrapper Python tipis di atas mesin `wkhtmltopdf` yang banyak digunakan. Instal keduanya dengan `pip` dan verifikasi jalur binary.

```bash
# Install the Python wrapper
pip install pdfkit

# On Ubuntu/Debian install wkhtmltopdf package
sudo apt-get install wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf
```

Jika Anda lebih suka binary yang dapat dipindahkan, unduh rilis yang sesuai dari [halaman GitHub wkhtmltopdf](https://github.com/wkhtmltopdf/wkhtmltopdf/releases) dan letakkan di direktori yang ditambahkan ke `PATH` Anda. Skrip kemudian akan memeriksa jalur secara otomatis.

## Langkah 2: Muat dokumen HTML

Anda dapat membaca file statis, mengambil konten remote, atau membangun HTML secara dinamis. Contoh di bawah memuat file lokal bernama `sample.html` yang berada di direktori yang Anda tentukan.

```python
import pathlib
import pdfkit

# Define the directory that holds the HTML source
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")

# Resolve the full path to the HTML file
html_path = BASE_DIR / "sample.html"

# Read the file content as a UTF‑8 string
with html_path.open(encoding="utf-8") as f:
    html_content = f.read()
```

Membaca file sebagai string Unicode memastikan bahwa karakter seperti “é”, “ß”, atau glyph Asia tetap terjaga selama konversi. Langkah ini penting ketika Anda **menghasilkan PDF dari HTML** yang berisi teks internasional.

## Langkah 3: Hasilkan PDF dari HTML

`pdfkit.from_string` mengonversi string yang berisi markup HTML menjadi file PDF. Anda dapat memberikan kamus opsi untuk mengendalikan ukuran halaman, margin, serta perilaku header/footer.

```python
# Define the output PDF path
pdf_path = BASE_DIR / "sample.pdf"

# Conversion options – adjust as needed
options = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left": "0.75in",
    "encoding": "UTF-8",
    "enable-local-file-access": None,  # Allows loading local images/CSS
}

# Perform the conversion
pdfkit.from_string(html_content, str(pdf_path), options=options)
```

Pemanggilan di atas **membuat PDF dari file HTML** yang disimpan di `sample.pdf`. Jika HTML sumber merujuk ke CSS atau gambar lokal, flag `enable‑local‑file-access` memungkinkan `wkhtmltopdf` menemukan sumber daya tersebut.

### Mengapa pendekatan ini berhasil

* `pdfkit` menyerahkan pekerjaan berat kepada `wkhtmltopdf`, yang merender HTML dengan mesin WebKit, menjamin kesetiaan tinggi terhadap tata letak asli.  
* Memberikan kamus opsi memungkinkan Anda menyesuaikan output secara detail tanpa mengubah HTML itu sendiri.  
* Menggunakan `from_string` menjaga alur kerja tetap dalam memori, yang berguna ketika HTML dihasilkan secara dinamis.

## Langkah 4: Simpan HTML sebagai PDF dan verifikasi output

Setelah konversi, Anda mungkin ingin memastikan bahwa PDF ada dan dapat dibaca. Potongan kode di bawah memeriksa ukuran file dan membuka PDF dengan penampil sistem default (spesifik platform).

```python
import os
import subprocess
import sys

# Verify that the PDF file was created
if pdf_path.is_file() and pdf_path.stat().st_size > 0:
    print(f"✅ PDF generated successfully: {pdf_path}")

    # Open the PDF for visual verification (optional)
    if sys.platform.startswith("darwin"):      # macOS
        subprocess.run(["open", str(pdf_path)])
    elif os.name == "nt":                      # Windows
        os.startfile(str(pdf_path))
    else:                                      # Linux and others
        subprocess.run(["xdg-open", str(pdf_path)])
else:
    raise FileNotFoundError("PDF generation failed – file not found or empty.")
```

Menjalankan skrip mencetak pesan keberhasilan dan meluncurkan penampil PDF sehingga Anda dapat langsung memastikan bahwa tata letak sesuai dengan HTML asli. Langkah ini menyelesaikan siklus **save html as pdf**.

## Langkah 5: Opsi lanjutan – buat PDF dari file HTML dengan pengaturan khusus

Kadang-kadang Anda memiliki file HTML fisik di disk dan lebih memilih `pdfkit.from_file` daripada memuat kontennya sendiri. Metode ini berguna ketika HTML sudah mencakup jalur relatif yang kompleks.

```python
# Directly convert a file path to PDF
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

Anda juga dapat menyematkan halaman sampul, daftar isi, atau flag eksekusi JavaScript dengan memperluas kamus `options`. Misalnya, untuk menambahkan halaman sampul:

```python
options.update({
    "cover": str(BASE_DIR / "cover.html"),
    "toc": None,  # Generates a table of contents
})
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

Penyesuaian ini menunjukkan **cara mengonversi HTML ke PDF** untuk alur penerbitan yang lebih canggih.

## Kesalahan umum dan cara menghindarinya

| Masalah | Penyebab | Solusi |
|-------|-------|--------|
| Gambar atau CSS tidak muncul | `wkhtmltopdf` memblokir akses file lokal secara default | Tambahkan `"enable-local-file-access": None` ke kamus opsi |
| Karakter Unicode menjadi rusak | Opsi `encoding` hilang atau membaca file dengan charset yang salah | Selalu set `"encoding": "UTF-8"` dan baca file HTML dengan UTF‑8 |
| PDF kosong | Jalur ke binary `wkhtmltopdf` tidak tepat | Berikan jalur secara eksplisit: `pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")` |
| File HTML besar menyebabkan timeout | Timeout default terlalu singkat | Set `"javascript-delay": "2000"` atau tingkatkan timeout dengan `"timeout": "60"` |

Menangani masalah-masalah ini memastikan proses **generate pdf from html** yang handal di berbagai lingkungan.

## Skrip lengkap – contoh end‑to‑end

Simpan berikut ini sebagai `html_to_pdf.py` dan jalankan dengan `python html_to_pdf.py`. Sesuaikan `YOUR_DIRECTORY` untuk mengarah ke folder proyek Anda.

```python
#!/usr/bin/env python3
"""
Convert HTML to PDF in Python – complete, runnable example.
"""

import pathlib
import pdfkit
import os
import subprocess
import sys

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")          # <-- change this
HTML_FILE = BASE_DIR / "sample.html"
PDF_FILE = BASE_DIR / "sample.pdf"

# wkhtmltopdf configuration (optional – only needed if binary is not on PATH)
# config = pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")

# Conversion options – customize as required
OPTIONS = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left":


## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Mengonversi HTML ke PDF Java – Menggunakan Aspose.HTML untuk Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Mengonversi HTML ke PDF di .NET dengan Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Cara Mengonversi HTML ke PDF Java – Mengatur Margin Halaman dengan Aspose.HTML](/html/english/java/advanced-usage/css-extensions-adding-title-page-number/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
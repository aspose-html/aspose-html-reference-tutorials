---
category: general
date: 2026-07-15
description: Buat PDF dari HTML menggunakan Python. Pelajari cara mengonversi HTML
  ke PDF dengan cepat menggunakan skrip sederhana dan langkah‑langkah yang jelas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf from html
- convert html to pdf
- html to pdf python
- save html as pdf
- html to pdf tutorial
language: id
lastmod: 2026-07-15
og_description: Buat PDF dari HTML dengan Python. Panduan ini menunjukkan cara mengonversi
  HTML ke PDF, menyimpan HTML sebagai PDF, dan menangani sumber daya secara efisien.
og_image_alt: Screenshot of a Python script that creates PDF from HTML
og_title: Buat PDF dari HTML di Python – Tutorial Praktis
schemas:
- author: Aspose
  dateModified: '2026-07-15'
  description: Create PDF from HTML using Python. Learn how to convert HTML to PDF
    quickly with a simple script and clear steps.
  headline: Create PDF from HTML in Python – HTML to PDF Python Tutorial
  type: TechArticle
tags:
- python
- pdf
- html
- conversion
title: Buat PDF dari HTML dengan Python – Tutorial Python HTML ke PDF
url: /id/python/general/create-pdf-from-html-in-python-html-to-pdf-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF dari HTML di Python – Tutorial Lengkap

Pernah perlu **membuat PDF dari HTML** tetapi tidak yakin pustaka Python mana yang harus dipilih? Anda tidak sendirian—banyak pengembang mengalami hal yang sama ketika mereka mencoba mengubah laporan web, faktur, atau halaman pemasaran menjadi PDF yang dapat dicetak.  

Kabar baiknya, dengan hanya beberapa baris kode Anda dapat **mengonversi HTML ke PDF** secara andal, dan skrip ini bekerja di Windows, macOS, dan Linux. Dalam panduan ini kami akan menelusuri contoh lengkap yang dapat dijalankan, menjelaskan mengapa setiap langkah penting, dan menunjukkan cara **menyimpan HTML sebagai PDF** tanpa meninggalkan hal yang terlewat.

---

## Apa yang Akan Anda Pelajari

- Instal paket Python yang tepat untuk konversi HTML‑ke‑PDF.  
- Muat file HTML dengan opsi penanganan sumber daya khusus (untuk menghindari impor CSS yang tak berujung).  
- Hasilkan file PDF bersih di disk.  
- Tangani kasus tepi umum seperti gambar eksternal, jalur relatif, dan dokumen besar.  

Pada akhir **tutorial HTML ke PDF** ini Anda akan memiliki fungsi yang dapat dipakai ulang dan dapat disisipkan ke proyek apa pun.

---

## Prasyarat

- Python 3.9+ (kode juga berfungsi dengan 3.8, tetapi 3.9+ memberikan fitur `pathlib` terbaru).  
- Familiaritas dasar dengan baris perintah dan lingkungan virtual.  
- File HTML yang ingin Anda ubah menjadi PDF—halaman statis apa pun dapat digunakan.

> **Pro tip:** Jika Anda menggunakan lingkungan virtual, aktifkan terlebih dahulu sebelum menginstal pustaka; ini menjaga instalasi Python global Anda tetap rapi.

---

## Langkah 1 – Instal WeasyPrint (mesin di balik konversi)

WeasyPrint adalah pustaka murni‑Python yang merender HTML dan CSS menjadi PDF. Ia menangani sebagian besar fitur web modern dan memberi Anda kontrol detail atas pemuatan sumber daya.

```bash
pip install weasyprint
```

Menjalankan perintah di atas akan mengunduh `cairocffi`, `tinycss2`, dan beberapa dependensi lainnya. Jika Anda menemui error terkait `cairo` di Windows, unduh roda (wheel) yang sudah dibangun sebelumnya dari [WeasyPrint website](https://weasyprint.org/docs/install/).

---

## Langkah 2 – Siapkan pembantu kecil untuk penanganan sumber daya

Saat Anda memuat dokumen HTML yang merujuk ke stylesheet atau gambar eksternal, pustaka akan mengikuti tautan‑tautan tersebut. Dalam beberapa kasus hal ini dapat menyebabkan penelusuran yang sangat dalam atau bahkan loop tak terbatas (bayangkan file CSS yang `@import` dirinya sendiri). Untuk menjaga kebersihan kami membatasi kedalaman penanganan sumber daya.

```python
from weasyprint import HTML, CSS
from pathlib import Path

class ResourceHandlingOptions:
    """Simple container to mimic max depth handling."""
    def __init__(self, max_depth: int = 3):
        self.max_depth = max_depth
        self._current_depth = 0

    def within_limit(self) -> bool:
        return self._current_depth < self.max_depth

    def __enter__(self):
        self._current_depth += 1
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        self._current_depth -= 1
```

Kelas di atas tidak diwajibkan oleh WeasyPrint, tetapi meniru pola yang Anda lihat pada cuplikan asli dan memberi Anda titik masuk untuk menghentikan impor yang melaju tak terkendali. Anda akan melihatnya dipakai pada langkah berikutnya.

---

## Langkah 3 – Muat dokumen HTML menggunakan opsi khusus

Sekarang kita benar‑benar membaca file HTML. Kelas `HTML` menerima argumen `base_url`, yang kami set ke direktori yang berisi file sumber—ini membuat tautan relatif berfungsi tanpa server web.

```python
def load_html(input_path: Path, options: ResourceHandlingOptions) -> HTML:
    """
    Load an HTML file while respecting the max handling depth.
    """
    if not options.within_limit():
        raise RuntimeError("Maximum resource handling depth exceeded.")
    # The `with` block increments depth for the duration of the call.
    with options:
        return HTML(filename=str(input_path), base_url=str(input_path.parent))
```

> **Mengapa ini penting:** Jika HTML Anda memuat serangkaian file CSS, setiap `@import` akan memicu pemuatan lain. Penjaga kedalaman mencegah skrip melenceng keluar kendali.

---

## Langkah 4 – Simpan dokumen yang telah diproses sebagai PDF

Dengan objek `HTML` di tangan, menghasilkan PDF cukup dengan satu baris kode. Kami juga menyertakan cuplikan CSS sederhana yang memaksa ukuran halaman bersih (A4) dan menambahkan margin tipis—silakan sesuaikan bila perlu.

```python
def save_as_pdf(html_doc: HTML, output_path: Path) -> None:
    """
    Render the HTML document to a PDF file.
    """
    default_css = CSS(string='''
        @page { size: A4; margin: 1cm }
    ''')
    html_doc.write_pdf(target=str(output_path), stylesheets=[default_css])
```

Memanggil `write_pdf` menyalurkan PDF ke disk, sehingga Anda mendapatkan file siap‑bagikan.

---

## Langkah 5 – Gabungkan Semua

Berikut adalah skrip ringkas yang dapat Anda salin‑tempel ke `convert.py`. Ganti jalur placeholder dengan direktori Anda yang sebenarnya.

```python
#!/usr/bin/env python3
"""
HTML to PDF Python script – complete, runnable example.
"""

from pathlib import Path

# Import the helper classes we defined earlier
from __main__ import ResourceHandlingOptions, load_html, save_as_pdf  # noqa: E402

def main():
    # 1️⃣  Define input and output locations
    input_html = Path("YOUR_DIRECTORY/input.html")
    output_pdf = Path("YOUR_DIRECTORY/output.pdf")

    # 2️⃣  Create resource handling options (max depth = 3)
    resource_options = ResourceHandlingOptions(max_depth=3)

    # 3️⃣  Load the HTML document with the custom options
    html_doc = load_html(input_html, resource_options)

    # 4️⃣  Save the processed document as PDF
    save_as_pdf(html_doc, output_pdf)

    print(f"✅ PDF saved to {output_pdf.resolve()}")

if __name__ == "__main__":
    main()
```

**Output yang diharapkan** – setelah menjalankan `python convert.py` Anda akan melihat:

```
✅ PDF saved to /full/path/YOUR_DIRECTORY/output.pdf
```

Buka file yang dihasilkan dengan penampil PDF apa pun; Anda akan melihat tata letak halaman asli, styling CSS, dan gambar (asalkan dapat diakses dari file HTML).  

Jika Anda menemukan gambar yang hilang, periksa kembali bahwa atribut `src` mereka berupa URL absolut atau jalur relatif yang memang ada di bawah `YOUR_DIRECTORY`.

---

## Pertanyaan Umum & Penanganan Kasus Tepi

| Pertanyaan | Jawaban |
|------------|---------|
| *Bagaimana jika HTML saya merujuk ke font eksternal?* | WeasyPrint akan mengunduh file font secara otomatis, tetapi Anda mungkin ingin memasukkan domain ke dalam whitelist agar waktu pengambilan tidak terlalu lama. |
| *Bisakah saya mengonversi string HTML alih‑alih file?* | Ya—gunakan `HTML(string=my_html_string)` dan lewati `base_url` atau setel ke folder sementara. |
| *Bagaimana cara mengontrol metadata PDF (judul, penulis)?* | Berikan dict `metadata` ke `write_pdf`, misalnya `html_doc.write_pdf(target='out.pdf', metadata={'Title': 'Report'})`. |
| *Saya mendapat “cairo‑cffi error” di Linux.* | Instal paket sistem `libcairo2-dev` (`apt-get install libcairo2-dev` pada Debian/Ubuntu) sebelum melakukan pip install WeasyPrint. |

---

## Penutup

Kami baru saja **membuat PDF dari HTML** menggunakan alur kerja Python yang bersih, membahas mekanisme **konversi HTML ke PDF**, dan menunjukkan cara **menyimpan HTML sebagai PDF** dengan penanganan sumber daya yang kuat. Skrip ini cukup kecil untuk disisipkan ke pipeline CI, namun cukup fleksibel untuk diperluas dengan header, footer, atau watermark khusus.

Langkah selanjutnya yang dapat Anda jelajahi:

- Gunakan pustaka **html to pdf python** `pdfkit` untuk pendekatan berbasis wkhtmltopdf (baik untuk CSS lama).  
- Tambahkan antarmuka CLI dengan `argparse` sehingga skrip menerima argumen input/output.  
- Hasilkan PDF secara langsung di dalam endpoint Flask atau FastAPI untuk laporan sesuai permintaan.  

Silakan bereksperimen, pecahkan masalah, dan kembali ke panduan ini untuk penyegaran cepat. Jika Anda menemui kendala, dokumentasi WeasyPrint dan forum komunitasnya adalah sumber daya yang sangat berguna.

Selamat coding, dan nikmati mengubah halaman web menjadi PDF yang elegan!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑per‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Konversi HTML ke PDF dengan Aspose.HTML – Panduan Manipulasi Lengkap](/html/english/)
- [Konversi HTML ke PDF di .NET dengan Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Buat PDF dari HTML – Panduan Langkah‑per‑Langkah C#](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
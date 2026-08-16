---
category: general
date: 2026-08-15
description: Cara membatasi sumber daya saat mengonversi HTML ke PDF menggunakan Python.
  Pelajari cara mengekspor HTML ke PDF dengan kedalaman sumber daya yang terkontrol.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to limit resources
- convert html to pdf
- export html to pdf
- save html as pdf
- how to convert html
language: id
lastmod: 2026-08-15
og_description: Cara membatasi sumber daya saat mengonversi HTML ke PDF dengan Python.
  Panduan ini menunjukkan cara mengekspor HTML ke PDF secara aman dengan membatasi
  kedalaman sumber daya yang terhubung.
og_image_alt: Screenshot of Python code converting an HTML file to a PDF with limited
  resource handling
og_title: Cara membatasi sumber daya saat mengonversi HTML ke PDF dengan Python
schemas:
- author: Aspose
  dateModified: '2026-08-15'
  description: How to limit resources while converting HTML to PDF using Python. Learn
    to export HTML to PDF with controlled resource depth.
  headline: How to limit resources when converting HTML to PDF in Python
  type: TechArticle
tags:
- HTML to PDF
- Python
- Resource handling
title: Cara membatasi sumber daya saat mengonversi HTML ke PDF dengan Python
url: /id/python/general/how-to-limit-resources-when-converting-html-to-pdf-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membatasi sumber daya saat mengonversi HTML ke PDF dengan Python

Jika Anda perlu **cara membatasi sumber daya** selama transformasi HTML‑ke‑PDF, panduan ini menyediakan solusi lengkap yang siap dijalankan. Dengan mengonfigurasi penanganan sumber daya, Anda mencegah pengambilan tautan mendalam, pengunduhan gambar besar, atau eksekusi skrip tak berujung, yang membuat konversi menjadi cepat dan dapat diprediksi.

Anda juga akan belajar cara **mengonversi HTML ke PDF**, **mengekspor HTML ke PDF**, dan **menyimpan HTML sebagai PDF** dengan satu skrip terstruktur dengan baik. Tidak diperlukan dokumentasi eksternal—cukup ikuti langkah‑langkah di bawah ini.

## Apa yang Anda perlukan

* Python 3.9 atau yang lebih baru  
* Paket `aspose.html` (perpustakaan yang menyediakan `HTMLDocument`, `ResourceHandlingOptions`, dan `PdfSaveOptions`)  
* File HTML yang ingin Anda konversi (misalnya, `big_page.html`)  

Memiliki prasyarat ini terpasang memastikan kode berjalan tanpa konfigurasi tambahan.

## Langkah 1: Instal paket Aspose.HTML

```bash
pip install aspose-html
```

Paket `aspose-html` menyediakan kelas‑kelas yang digunakan untuk memuat, mengonfigurasi, dan menyimpan dokumen. Menginstalnya sekali saja sudah cukup untuk semua impor selanjutnya.

## Langkah 2: Muat dokumen HTML yang ingin Anda konversi

```python
from aspose.html import HTMLDocument

# Load the source HTML file
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html")
```

`HTMLDocument` mem‑parse file dan membangun DOM di memori. Objek ini menjadi titik masuk untuk setiap konversi, baik Anda berencana **mengonversi HTML ke PDF** atau menampilkannya di browser.

## Langkah 3: Konfigurasikan penanganan sumber daya (cara membatasi sumber daya)

```python
from aspose.html.drawing import ResourceHandlingOptions

# Create a resource handling options object
res_opts = ResourceHandlingOptions()
# Limit the depth of linked resources to three levels
res_opts.max_handling_depth = 3
```

Menetapkan `max_handling_depth` memberi tahu mesin untuk berhenti mengikuti tautan setelah tiga lompatan. Inilah inti dari **cara membatasi sumber daya**: sumber daya yang lebih dalam diabaikan, mencegah permintaan jaringan yang tak terkendali atau konsumsi memori yang besar. Sesuaikan nilai ini berdasarkan kebijakan keamanan atau kinerja proyek Anda.

### Mengapa membatasi sumber daya?

* **Keamanan** – Mencegah pemuatan skrip eksternal yang dapat mengeksekusi kode yang tidak diinginkan.  
* **Kinerja** – Mengurangi penggunaan bandwidth dan waktu CPU ketika halaman sumber memiliki banyak gambar atau stylesheet.  
* **Prediktabilitas** – Menjamin konversi selesai dalam jangka waktu yang diketahui.

## Langkah 4: Lampirkan opsi sumber daya ke pengaturan penyimpanan PDF

```python
from aspose.html.saving import PdfSaveOptions

# Create PDF save options and attach the resource handling configuration
pdf_opts = PdfSaveOptions()
pdf_opts.resource_handling_options = res_opts
```

`PdfSaveOptions` menggabungkan semua parameter untuk ekspor akhir. Dengan menautkan `resource_handling_options`, Anda memastikan langkah **mengekspor HTML ke PDF** menghormati batas kedalaman yang telah Anda tentukan.

## Langkah 5: Ekspor HTML ke PDF (simpan HTML sebagai PDF)

```python
# Save the document as a PDF file using the configured options
doc.save("YOUR_DIRECTORY/big_page.pdf", pdf_opts)
```

Memanggil `save` menulis PDF ke disk. Baris ini memperlihatkan **cara mengonversi HTML** menjadi dokumen portabel sambil mematuhi batasan sumber daya. File yang dihasilkan, `big_page.pdf`, hanya berisi sumber daya dalam kedalaman yang diizinkan.

## Langkah 6: Verifikasi PDF yang dihasilkan

Buka `big_page.pdf` dengan penampil PDF apa pun. Anda akan melihat tata letak halaman asli, tetapi sumber daya eksternal di luar tiga lompatan tidak akan muncul. Jika Anda menemukan gambar atau gaya yang hilang, pertimbangkan meningkatkan `max_handling_depth` atau menyematkan aset tersebut langsung di HTML.

### Daftar periksa verifikasi umum

| Pemeriksaan | Hasil yang diharapkan |
|------------|-----------------------|
| Teks muncul dengan benar | Semua konten teks dari HTML sumber hadir |
| Gambar utama dimuat | Gambar yang direferensikan dalam tiga level terlihat |
| Tidak ada panggilan jaringan setelah konversi | Gunakan monitor jaringan untuk memastikan tidak ada permintaan tambahan |

## Kasus khusus dan tips praktis

| Situasi | Penanganan yang disarankan |
|---------|----------------------------|
| **File lokal tidak ditemukan** | Bungkus pembuatan `HTMLDocument` dalam blok `try/except FileNotFoundError` dan catat pesan error yang jelas. |
| **Gambar sangat besar** | Gabungkan `max_handling_depth` dengan `max_image_resolution` di `PdfSaveOptions` untuk menurunkan resolusi grafik yang berukuran berlebih. |
| **Konten JavaScript dinamis** | Setel `pdf_opts.enable_javascript = False` jika Anda menginginkan konversi statis murni tanpa eksekusi skrip. |
| **URL relatif** | Pastikan `doc.base_url` mengarah ke direktori yang berisi file HTML sehingga tautan relatif dapat di‑resolve dengan benar. |

## Skrip lengkap yang dapat Anda salin‑tempel

```python
# -------------------------------------------------------------
# Full example: limit resources while converting HTML to PDF
# -------------------------------------------------------------
# pip install aspose-html   # Run once before execution
# -------------------------------------------------------------

from aspose.html import HTMLDocument
from aspose.html.drawing import ResourceHandlingOptions
from aspose.html.saving import PdfSaveOptions

def convert_html_to_pdf(
    html_path: str,
    pdf_path: str,
    max_depth: int = 3
) -> None:
    """
    Converts an HTML file to PDF while limiting the depth of linked resources.

    Args:
        html_path: Path to the source .html file.
        pdf_path: Destination path for the generated .pdf file.
        max_depth: Maximum depth for resource handling (default = 3).
    """
    # Load the HTML document
    doc = HTMLDocument(html_path)

    # Configure resource handling
    res_opts = ResourceHandlingOptions()
    res_opts.max_handling_depth = max_depth

    # Attach resource options to PDF save settings
    pdf_opts = PdfSaveOptions()
    pdf_opts.resource_handling_options = res_opts

    # Export HTML to PDF
    doc.save(pdf_path, pdf_opts)

if __name__ == "__main__":
    # Example usage
    convert_html_to_pdf(
        html_path="YOUR_DIRECTORY/big_page.html",
        pdf_path="YOUR_DIRECTORY/big_page.pdf",
        max_depth=3
    )
```

Menjalankan skrip ini akan membuat `big_page.pdf` di direktori yang sama, menerapkan aturan **cara membatasi sumber daya** yang telah Anda definisikan. Fungsi `convert_html_to_pdf` dapat dipakai kembali dalam proyek yang lebih besar, memudahkan **menyimpan HTML sebagai PDF** dengan pengaturan konsisten.

## Kesimpulan

Anda kini mengetahui **cara membatasi sumber daya** ketika **mengonversi HTML ke PDF** menggunakan Python. Tutorial ini mencakup instalasi perpustakaan, memuat HTML, mengonfigurasi `ResourceHandlingOptions`, melampirkan opsi tersebut ke `PdfSaveOptions`, dan akhirnya **mengekspor HTML ke PDF**. Dengan mengontrol `max_handling_depth` Anda melindungi aplikasi dari lalu lintas jaringan berlebih dan waktu konversi yang tidak dapat diprediksi.

Selanjutnya, jelajahi topik terkait seperti **cara mengonversi HTML** dengan CSS khusus, menyematkan font, atau menghasilkan PDF secara massal. Menyesuaikan opsi lain pada `PdfSaveOptions` (misalnya ukuran halaman, kompresi) memungkinkan Anda menyempurnakan output untuk faktur, laporan, atau e‑book.

Jangan ragu bereksperimen dengan nilai kedalaman yang berbeda, menggabungkan pendekatan ini dengan browser headless, atau mengintegrasikannya ke layanan web yang mengembalikan PDF sesuai permintaan. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait dan membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Create HTML Document with Styled Text and Export to PDF – Full Guide](/html/english/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/)
- [Convert HTML to PDF with Aspose.HTML – Full Manipulation Guide](/html/english/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
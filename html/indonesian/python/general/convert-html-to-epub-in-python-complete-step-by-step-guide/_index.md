---
category: general
date: 2026-07-18
description: Konversi HTML ke EPUB dengan Python secara cepat. Pelajari cara memuat
  file HTML di Python dan juga mengonversi HTML ke MHTML menggunakan pustaka sederhana.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to epub
- load html file in python
- convert html to mhtml
language: id
lastmod: 2026-07-18
og_description: Konversi HTML ke EPUB dalam Python dengan contoh yang jelas dan dapat
  dijalankan. Juga pelajari cara memuat file HTML di Python dan mengonversi HTML ke
  MHTML dalam hitungan menit.
og_image_alt: Diagram showing convert html to epub workflow
og_title: Mengonversi HTML ke EPUB dengan Python – Tutorial Lengkap
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  headline: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  name: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Python 3.9+** – the syntax used here works on any recent version.'
    text: '**Python 3.9+** – the syntax used here works on any recent version.'
  - name: '**pip** – to install third‑party packages.'
    text: '**pip** – to install third‑party packages.'
  - name: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
    text: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
  type: HowTo
tags:
- python
- html
- epub
- mhtml
- file conversion
title: Mengonversi HTML ke EPUB dengan Python – Panduan Lengkap Langkah demi Langkah
url: /id/python/general/convert-html-to-epub-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengonversi HTML ke EPUB dengan Python – Panduan Lengkap Langkah‑per‑Langkah

Pernah bertanya-tanya bagaimana cara **mengonversi HTML ke EPUB** tanpa membuat rambut Anda rontok? Anda bukan satu-satunya—para pengembang terus-menerus perlu mengubah halaman web menjadi e‑book untuk dibaca secara offline, dan melakukannya dengan Python ternyata sangat mudah. Dalam tutorial ini kami akan menjelaskan cara memuat file HTML di Python, mengonversi HTML tersebut ke EPUB, dan bahkan mengubah sumber yang sama menjadi MHTML untuk arsip yang ramah email.

Pada akhir panduan, Anda akan memiliki skrip siap‑jalankan yang mengambil satu file `sample.html` dan menghasilkan baik `sample.epub` maupun `sample.mhtml`. Tidak ada misteri, hanya kode yang jelas dan penjelasan.

![Diagram alur konversi](https://example.com/images/convert-html-epub.png "Diagram yang menunjukkan alur kerja mengonversi html ke epub")

## Apa yang Akan Anda Bangun

- **Muat file HTML di Python** menggunakan modul bawaan `pathlib` dan `io`.  
- **Konversi HTML ke EPUB** dengan perpustakaan `ebooklib`, yang menangani format kontainer EPUB untuk Anda.  
- **Konversi HTML ke MHTML** (juga dikenal sebagai MHT) menggunakan paket `email`, membuat arsip web satu‑file yang dapat dibuka langsung oleh peramban.  

Kami juga akan membahas:

- Dependensi yang diperlukan dan cara menginstalnya.  
- Penanganan error sehingga skrip Anda gagal dengan elegan.  
- Cara menyesuaikan metadata seperti judul dan penulis untuk file EPUB.  

Siap? Mari kita mulai.

## Prasyarat

Sebelum kita mulai menulis kode, pastikan Anda memiliki:

1. **Python 3.9+** – sintaks yang digunakan di sini bekerja pada versi terbaru apa pun.  
2. **pip** – untuk menginstal paket pihak ketiga.  
3. File HTML sederhana, misalnya `sample.html`, yang ditempatkan di folder yang Anda kontrol.  

Jika Anda sudah memiliki semuanya, bagus—lewati ke bagian berikutnya.  

> **Pro tip:** Pastikan HTML Anda terstruktur dengan baik (bagian `<head>` dan `<body>` yang tepat). Meskipun `ebooklib` akan mencoba memperbaiki masalah kecil, sumber yang bersih menghindarkan Anda dari masalah di kemudian hari.

## Langkah 1 – Instal Perpustakaan yang Diperlukan

Kami memerlukan dua paket eksternal:

- **ebooklib** – untuk pembuatan EPUB.  
- **beautifulsoup4** – opsional, tetapi berguna untuk membersihkan HTML sebelum konversi.

Jalankan ini di terminal Anda:

```bash
pip install ebooklib beautifulsoup4
```

> **Mengapa perpustakaan ini?** `ebooklib` membangun struktur EPUB berbasis ZIP untuk Anda, menangani folder `META‑INF`, `content.opf`, dan `toc.ncx` secara otomatis. `beautifulsoup4` memungkinkan kami merapikan HTML, memastikan e‑book akhir ditampilkan dengan benar di semua pembaca.

## Langkah 2 – Muat File HTML di Python

Memuat file HTML sangat sederhana, tetapi kami akan membungkusnya dalam fungsi pembantu kecil yang mengembalikan objek **BeautifulSoup** untuk diproses nanti.

```python
from pathlib import Path
from bs4 import BeautifulSoup

def load_html(filepath: str) -> BeautifulSoup:
    """
    Load an HTML file from disk and return a BeautifulSoup object.
    Raises FileNotFoundError if the file does not exist.
    """
    path = Path(filepath)
    if not path.is_file():
        raise FileNotFoundError(f"HTML file not found: {filepath}")

    # Read the file using UTF‑8 encoding (most common for web content)
    html_content = path.read_text(encoding="utf-8")
    # Parse with BeautifulSoup for optional cleaning later
    soup = BeautifulSoup(html_content, "html.parser")
    return soup
```

**Penjelasan:**  
- `Path` memberikan penanganan file yang independen dari OS.  
- Menggunakan `read_text` menghindari boilerplate `open`/`close` manual.  
- Mengembalikan objek `BeautifulSoup` berarti kita dapat nanti menghapus skrip, memperbaiki tag yang rusak, atau menyisipkan stylesheet sebelum kita **mengonversi HTML ke EPUB**.

## Langkah 3 – Konversi HTML ke EPUB

Sekarang karena kita dapat **memuat file HTML di Python**, mari ubah menjadi EPUB yang bersih. Fungsi di bawah menerima objek `BeautifulSoup`, jalur tujuan, dan metadata opsional.

```python
import uuid
from ebooklib import epub

def html_to_epub(soup: BeautifulSoup,
                 output_path: str,
                 title: str = "Untitled Book",
                 author: str = "Anonymous") -> None:
    """
    Convert a BeautifulSoup HTML document to an EPUB file.
    """
    # Create a new EPUB book instance
    book = epub.EpubBook()

    # Set basic metadata – this is what shows up in e‑reader libraries
    book.set_identifier(str(uuid.uuid4()))
    book.set_title(title)
    book.set_language('en')
    book.add_author(author)

    # Convert the soup back to a string; we could also clean it here
    html_str = str(soup)

    # Create a chapter (EPUB requires at least one)
    chapter = epub.EpubHtml(title=title,
                            file_name='chap_01.xhtml',
                            lang='en')
    chapter.content = html_str
    book.add_item(chapter)

    # Define the spine (reading order) and table of contents
    book.toc = (epub.Link('chap_01.xhtml', title, 'intro'),)
    book.spine = ['nav', chapter]

    # Add default navigation files
    book.add_item(epub.EpubNcx())
    book.add_item(epub.EpubNav())

    # Write the final EPUB file
    epub.write_epub(output_path, book, {})

    print(f"✅ EPUB created at: {output_path}")
```

**Mengapa ini berhasil:**  
- `ebooklib.epub.EpubBook` mengabstraksi kontainer ZIP dan file manifest yang diperlukan.  
- Kami menghasilkan UUID sebagai pengidentifikasi untuk menghindari duplikasi ID jika Anda membuat banyak buku.  
- `spine` memberi tahu pembaca urutan bab; buku satu‑bab cukup untuk kebanyakan sumber HTML sederhana.

**Menjalankan konversi:**  

```python
if __name__ == "__main__":
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_epub(html_doc,
                 "YOUR_DIRECTORY/sample.epub",
                 title="My Sample eBook",
                 author="Jane Developer")
```

Saat Anda menjalankan skrip, Anda akan melihat tanda centang hijau yang mengonfirmasi lokasi file EPUB.

## Langkah 4 – Konversi HTML ke MHTML

MHTML (atau MHT) menggabungkan HTML dan semua sumber dayanya (gambar, CSS) ke dalam satu file MIME. Paket `email` Python dapat membangun format ini tanpa ketergantungan eksternal.

```python
import mimetypes
import base64
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from email.mime.base import MIMEBase
from email import encoders

def html_to_mhtml(soup: BeautifulSoup,
                  output_path: str,
                  base_url: str = "") -> None:
    """
    Convert a BeautifulSoup HTML document to an MHTML file.
    `base_url` is used to resolve relative resource links.
    """
    # Create the multipart/related container required for MHTML
    mhtml = MIMEMultipart('related')
    mhtml['Subject'] = 'Converted MHTML document'
    mhtml['Content-Type'] = 'multipart/related; type="text/html"'

    # Main HTML part
    html_part = MIMEText(str(soup), 'html', 'utf-8')
    html_part.add_header('Content-Location', 'file://index.html')
    mhtml.attach(html_part)

    # Optional: embed images referenced in the HTML
    for img in soup.find_all('img'):
        src = img.get('src')
        if not src:
            continue

        # Resolve absolute path if needed
        img_path = Path(base_url) / src if base_url else Path(src)
        if not img_path.is_file():
            continue  # skip missing files

        # Guess MIME type; default to octet-stream
        mime_type, _ = mimetypes.guess_type(img_path)
        mime_type = mime_type or 'application/octet-stream'

        with img_path.open('rb') as f:
            img_data = f.read()

        img_part = MIMEBase(*mime_type.split('/'))
        img_part.set_payload(img_data)
        encoders.encode_base64(img_part)
        img_part.add_header('Content-Location', f'file://{src}')
        img_part.add_header('Content-Transfer-Encoding', 'base64')
        mhtml.attach(img_part)

    # Write the MHTML file
    with open(output_path, 'wb') as out_file:
        out_file.write(mhtml.as_bytes())

    print(f"✅ MHTML created at: {output_path}")
```

**Poin penting:**  

- Tipe MIME `multipart/related` memberi tahu peramban bahwa bagian HTML dan sumber dayanya berada bersama.  
- Kami mengulangi tag `<img>` untuk menyematkan gambar; jika Anda tidak memerlukan gambar, Anda dapat melewatkan blok tersebut.  
- `Content-Location` menggunakan URI `file://` sehingga peramban dapat menyelesaikan sumber daya secara internal.

**Memanggil fungsi:**  

```python
if __name__ == "__main__":
    # Re‑use the previously loaded soup
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_mhtml(html_doc, "YOUR_DIRECTORY/sample.mhtml", base_url="YOUR_DIRECTORY")
```

Sekarang Anda memiliki `sample.epub` dan `sample.mhtml` berdampingan.

## Skrip Lengkap – Semua Langkah dalam Satu File

Berikut adalah skrip lengkap yang siap dijalankan yang menggabungkan semuanya. Simpan sebagai `convert_html.py` dan ganti `YOUR_DIRECTORY` dengan jalur yang berisi `sample.html` Anda.



## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑per‑langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Mengonversi HTML ke MHTML dengan Aspose.HTML untuk Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [Cara Mengonversi EPUB ke PDF dengan Java – Menggunakan Aspose.HTML](/html/english/java/converting-epub-to-pdf/convert-epub-to-pdf/)
- [Cara Mengonversi EPUB ke Gambar dengan Aspose.HTML untuk Java](/html/english/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
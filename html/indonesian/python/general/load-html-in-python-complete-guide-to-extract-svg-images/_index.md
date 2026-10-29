---
category: general
date: 2026-06-10
description: Muat HTML di Python untuk mengekstrak gambar SVG dari halaman Anda—kode
  langkah demi langkah, tips, dan penanganan kasus tepi.
draft: false
keywords:
- load html python
- extract svg images
- extract svg from html
- search html svg
- find inline svg
language: id
og_description: Muat HTML di Python dan ekstrak gambar SVG dengan contoh yang jelas
  dan dapat dijalankan. Pelajari cara mencari elemen SVG dalam HTML serta menangani
  kasus tepi.
og_title: Muat HTML di Python – Ekstrak Gambar SVG Secara Efisien
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Load HTML in Python to extract SVG images from your pages—step-by-step
    code, tips, and edge‑case handling.
  headline: Load HTML in Python – Complete Guide to Extract SVG Images
  type: TechArticle
tags:
- python
- html-parsing
- svg
title: Muat HTML di Python – Panduan Lengkap untuk Mengekstrak Gambar SVG
url: /id/python/general/load-html-in-python-complete-guide-to-extract-svg-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Memuat HTML di Python – Panduan Lengkap untuk Mengekstrak Gambar SVG

Pernah perlu **memuat HTML di Python** hanya untuk mengambil semua grafik SVG dari sebuah halaman? Anda tidak sendirian. Baik Anda sedang membangun web‑scraper, menghasilkan laporan aset, atau sekadar penasaran dengan ikon yang digunakan situs, mengetahui cara **mengekstrak gambar SVG** menghemat banyak waktu pencarian manual.

Dalam tutorial ini kami akan membahas solusi praktis end‑to‑end yang **memuat HTML di Python**, kemudian **menelusuri elemen HTML SVG**, **menemukan inline SVG**, dan bahkan mengambil file SVG eksternal yang direferensikan oleh tag `<img>`. Pada akhir tutorial Anda akan memiliki skrip yang dapat digunakan kembali, beberapa tips untuk bagian yang rumit, dan gambaran jelas tentang seperti apa outputnya.

## Apa yang Akan Anda Dapatkan

* Skrip Python yang dapat dijalankan sepenuhnya yang mem-parsing file HTML lokal (atau halaman yang di‑fetch) dan mencantumkan setiap SVG yang dapat ditemukan.  
* Pemahaman tentang perbedaan antara **inline SVG** (`<svg>…</svg>`) dan **external SVG** (`<img src="… .svg">`).  
* Strategi untuk menangani markup yang rusak, file yang hilang, dan keanehan namespace.  
* Ide untuk memperluas kode—menyimpan SVG, mengonversinya ke PNG, atau memasukkannya ke dalam basis data.

### Prasyarat

* Python 3.8+ terpasang.  
* Familiaritas dasar dengan pustaka `requests` dan `BeautifulSoup` Python (kami akan meng‑importnya, tidak perlu pendalaman).  
* File HTML lokal atau URL yang ingin Anda scan.  

Sekarang, mari kita mulai.

## Memuat HTML di Python – Menyiapkan Parser

Langkah pertama adalah **memuat HTML di Python**. Anda dapat membaca file dari disk atau mengambil halaman remote. Berikut adalah helper minimal namun kuat yang melakukan keduanya:

```python
import os
import requests
from bs4 import BeautifulSoup

def load_html(source: str) -> BeautifulSoup:
    """
    Load HTML content from a file path or a URL and return a BeautifulSoup object.
    """
    if os.path.isfile(source):
        # Load from local file
        with open(source, "r", encoding="utf-8") as f:
            html = f.read()
    else:
        # Assume it's a URL and fetch it
        response = requests.get(source)
        response.raise_for_status()
        html = response.text

    # Use the html.parser for speed; switch to 'lxml' if you need extra robustness
    soup = BeautifulSoup(html, "html.parser")
    return soup
```

> **Mengapa ini penting:** Menggunakan `BeautifulSoup` mengabstraksi keanehan parsing string mentah, dan fungsi ini menangani baik file lokal maupun URL remote dengan elegan. Ia juga melemparkan exception bila permintaan jaringan gagal—sehingga Anda langsung tahu bila ada yang tidak beres.

## Mengekstrak Gambar SVG – Menemukan Elemen Inline SVG

Setelah dokumen dimuat, langkah logis berikutnya adalah **menemukan tag inline SVG**. Inline SVG disisipkan langsung dalam markup HTML, yang berarti Anda dapat mengambilnya langsung dari DOM.

```python
def collect_inline_svg(soup: BeautifulSoup) -> list:
    """
    Return a list of all inline <svg> elements as strings.
    """
    inline_svgs = []
    for svg in soup.find_all("svg"):
        # Preserve the original markup; .decode() gives us a string representation
        inline_svgs.append(str(svg))
    return inline_svgs
```

*Tip pro:* Jika halaman menggunakan namespace SVG (`<svg xmlns="http://www.w3.org/2000/svg">`), `BeautifulSoup` tetap menemukan tag tersebut karena secara default mengabaikan namespace. Itu sangat membantu ketika Anda hanya **menelusuri HTML SVG**.

## Menelusuri HTML SVG – Menangani Referensi `<img>` Eksternal

Banyak situs tidak menyematkan SVG secara langsung; mereka mereferensikan file eksternal melalui `<img src="icon.svg">`. Untuk menangkapnya, kita perlu mengiterasi setiap tag `<img>`, memeriksa `src`‑nya, dan melihat apakah berakhiran `.svg`.

```python
def collect_external_svg(soup: BeautifulSoup, base_path: str = "") -> list:
    """
    Return a list of file paths or URLs that point to external SVG images.
    If base_path is provided, it will be joined with relative URLs.
    """
    external_svgs = []
    for img in soup.find_all("img"):
        src = img.get("src")
        if src and src.lower().endswith(".svg"):
            # Resolve relative paths if a base directory or URL is given
            if base_path and not src.startswith(("http://", "https://")):
                src = os.path.join(base_path, src)
            external_svgs.append(src)
    return external_svgs
```

> **Peringatan kasus tepi:** Beberapa halaman menggunakan query string (`icon.svg?v=2`) atau fragment (`icon.svg#layer`). Pemeriksaan `endswith(".svg")` tetap berfungsi karena kami hanya melihat bagian akhir string yang sudah di‑lower‑case. Jika Anda memerlukan validasi yang lebih ketat, pertimbangkan menggunakan `urllib.parse` untuk menghapus parameter terlebih dahulu.

## Menemukan Inline SVG – Melaporkan Hasil

Sekarang kita memiliki dua daftar—satu untuk markup inline SVG dan satu lagi untuk referensi file eksternal—kita dapat menggabungkannya dan melaporkan total jumlahnya. Ini meniru potongan kode asli yang Anda posting, namun menambahkan sedikit konteks.

```python
def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")
```

## Menggabungkan Semua – Skrip Lengkap

Berikut adalah program lengkap yang siap dijalankan. Simpan sebagai `extract_svg.py` dan arahkan ke file HTML lokal atau URL.

```python
#!/usr/bin/env python3
import os
import sys
import requests
from bs4 import BeautifulSoup

# -------------------------------------------------
# Helper functions (see definitions above)
# -------------------------------------------------
def load_html(source: str) -> BeautifulSoup:
    if os.path.isfile(source):
        with open(source, "r", encoding="utf-8") as f:
            html = f.read()
    else:
        response = requests.get(source)
        response.raise_for_status()
        html = response.text
    return BeautifulSoup(html, "html.parser")

def collect_inline_svg(soup: BeautifulSoup) -> list:
    return [str(svg) for svg in soup.find_all("svg")]

def collect_external_svg(soup: BeautifulSoup, base_path: str = "") -> list:
    external_svgs = []
    for img in soup.find_all("img"):
        src = img.get("src")
        if src and src.lower().endswith(".svg"):
            if base_path and not src.startswith(("http://", "https://")):
                src = os.path.join(base_path, src)
            external_svgs.append(src)
    return external_svgs

def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")

# -------------------------------------------------
# Main execution
# -------------------------------------------------
if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python extract_svg.py <path-or-url-to-html>")
        sys.exit(1)

    source = sys.argv[1]
    soup = load_html(source)

    # Determine base path for relative <img> sources (only relevant for local files)
    base_dir = os.path.dirname(os.path.abspath(source)) if os.path.isfile(source) else ""

    inline_svgs = collect_inline_svg(soup)
    external_svgs = collect_external_svg(soup, base_dir)

    report_svg_counts(inline_svgs, external_svgs)

    # Optional: write inline SVGs to separate files for inspection
    for idx, svg_markup in enumerate(inline_svgs, start=1):
        out_path = f"inline_svg_{idx}.svg"
        with open(out_path, "w", encoding="utf-8") as out_file:
            out_file.write(svg_markup)
        print(f"Saved inline SVG #{idx} to {out_path}")

    # Optional: download external SVGs (uncomment if needed)
    # for url in external_svgs:
    #     try:
    #         resp = requests.get(url)
    #         resp.raise_for_status()
    #         filename = os.path.basename(url.split("?")[0])
    #         with open(filename, "wb") as f:
    #             f.write(resp.content)
    #         print(f"Downloaded {url} → {filename}")
    #     except Exception as e:
    #         print(f"Failed to download {url}: {e}")
```

### Output yang Diharapkan

Menjalankan skrip terhadap contoh `sample.html` mungkin menghasilkan:

```
Found 3 inline SVG element(s).
Found 2 external SVG reference(s).
Overall, 5 SVG item(s) detected.
Saved inline SVG #1 to inline_svg_1.svg
Saved inline SVG #2 to inline_svg_2.svg
Saved inline SVG #3 to inline_svg_3.svg
```

Jika Anda mengaktifkan blok download, SVG eksternal akan diunduh.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Convert SVG to Image in .NET with Aspose.HTML](/html/english/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [How to Convert SVG to XPS with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
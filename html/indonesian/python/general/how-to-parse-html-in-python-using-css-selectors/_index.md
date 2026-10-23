---
category: general
date: 2026-10-21
description: Pelajari cara mem-parsing HTML dengan Python, memuat dokumen HTML, menggunakan
  selector CSS, dan mengekstrak tautan dari HTML dengan cepat.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to parse html
- how to use selector
- extract hyperlinks from html
- load html document python
language: id
lastmod: 2026-10-21
og_description: Cara mengurai HTML di Python menggunakan selector CSS. Muat dokumen
  HTML, pilih tautan, dan ekstrak hyperlink dari HTML dengan kode yang bersih.
og_image_alt: Screenshot showing how to parse HTML in Python with CSS selectors
og_title: Cara mengurai HTML di Python – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to parse HTML in Python, load an HTML document, use CSS selectors,
    and extract hyperlinks from HTML quickly.
  headline: How to parse HTML in Python using CSS selectors
  type: TechArticle
tags:
- python
- html-parsing
- css-selectors
title: Cara mengurai HTML di Python menggunakan selector CSS
url: /id/python/general/how-to-parse-html-in-python-using-css-selectors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mem-parsing HTML di Python menggunakan CSS selector

Jika Anda perlu **how to parse html** dalam skrip Python, panduan ini menunjukkan tepatnya itu. Anda akan belajar cara memuat dokumen HTML, cara menggunakan sintaks selector untuk menemukan elemen, dan cara mengekstrak hyperlink dari html tanpa menulis parser khusus.

Parsing HTML adalah tugas umum untuk web scraper, pipeline analisis data, atau pengujian otomatis. Pada akhir tutorial ini Anda akan memiliki fungsi yang dapat digunakan kembali yang memuat dokumen HTML, memilih semua tag `<a>` dengan CSS selector, dan mengembalikan daftar URL yang bersih.

## Apa yang Anda butuhkan

- Python 3.8+ (kode ini bekerja pada versi terbaru apa pun)  
- Pustaka **lxml** (`pip install lxml`) – menyediakan parsing HTML cepat dan dukungan CSS selector  
- File HTML yang ingin Anda analisis (mis., `sample.html`)  

Tidak ada alat tambahan yang diperlukan; semuanya berjalan dengan pustaka standar dan satu paket pihak ketiga.

## Langkah 1: Cara mem-parsing HTML – memuat dokumen

Langkah pertama dalam alur kerja HTML apa pun adalah membaca file ke memori. Menggunakan **lxml.html** memberi Anda objek pohon yang mendukung CSS selector.

```python
# step_1_load.py
from lxml import html

def load_html(path: str) -> html.HtmlElement:
    """
    Load an HTML document from the given file path.
    Returns an lxml HtmlElement that can be queried with CSS selectors.
    """
    with open(path, "r", encoding="utf-8") as f:
        content = f.read()
    # Parse the raw HTML string into a tree
    return html.fromstring(content)

# Example usage
doc = load_html("sample.html")
print("Document loaded – ready for selector queries.")
```

**Mengapa ini penting:**  
`load_html` mengabstraksi boilerplate pembacaan file dan menjamin dokumen diparse dengan parser HTML yang toleran. Ini adalah cara paling aman untuk **load html document python** tanpa khawatir tentang markup yang rusak.

## Langkah 2: Cara menggunakan selector – menemukan semua elemen tautan

Setelah dokumen dimuat, Anda dapat menggunakan CSS selector untuk menemukan setiap tag `<a>`. Selector `"a"` mencocokkan semua elemen anchor, tetapi Anda dapat memperhalusnya (mis., `"a.external"` atau `"nav a"`).

```python
# step_2_selector.py
def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    """
    Return a list of <a> elements using a CSS selector.
    This demonstrates how to use selector syntax with lxml.
    """
    # The CSS selector "a" selects every anchor tag
    return doc.cssselect("a")

# Example usage
links = select_links(doc)
print(f"Found {len(links)} <a> elements.")
```

**Mengapa ini penting:**  
Pendekatan **how to use selector** memungkinkan Anda mengekspresikan kueri kompleks dalam satu string yang mudah dibaca, menghindari traversing pohon manual. Ini bekerja untuk pola CSS apa pun yang didukung oleh `lxml.cssselect`.

## Langkah 3: Ekstrak hyperlink dari HTML dan proses mereka

Sekarang Anda memiliki daftar elemen `<a>`, Anda dapat mengambil atribut `href` dari masing‑masing. Helper di bawah ini juga menormalkan URL relatif terhadap base URL (jika Anda menyediakannya).

```python
# step_3_extract.py
from urllib.parse import urljoin
from typing import Optional

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    """
    Return a list of href values from the given <a> elements.
    If base_url is supplied, relative URLs are resolved to absolute URLs.
    """
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            # Skip <a> tags without an href attribute
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

# Example usage
hyperlinks = extract_hyperlinks(links, base_url="https://example.com")
for url in hyperlinks:
    print(url)
```

**Output yang diharapkan** (asumsi `sample.html` berisi tiga tautan):

```
https://example.com/page1.html
https://example.com/page2.html
https://external.org/resource
```

**Mengapa ini penting:**  
`extract_hyperlinks` adalah inti dari **extract hyperlinks from html**. Ia menangani atribut `href` yang hilang dengan elegan, menyelesaikan tautan relatif, dan mengembalikan daftar Python biasa yang dapat Anda berikan ke proses selanjutnya (mis., requests, pandas, atau basis data).

## Contoh lengkap end‑to‑end

Menggabungkan ketiga fungsi memberikan Anda satu skrip yang memuat file, memilih semua anchor, dan mencetak setiap hyperlink.

```python
# parse_links.py
from lxml import html
from urllib.parse import urljoin
from typing import Optional

def load_html(path: str) -> html.HtmlElement:
    with open(path, "r", encoding="utf-8") as f:
        return html.fromstring(f.read())

def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    return doc.cssselect("a")

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

if __name__ == "__main__":
    # 1️⃣ Load the HTML document
    document = load_html("sample.html")
    # 2️⃣ Use selector to grab all <a> tags
    anchor_elements = select_links(document)
    # 3️⃣ Extract and print each hyperlink
    for url in extract_hyperlinks(anchor_elements, base_url="https://example.com"):
        print(url)
```

Menjalankan `python parse_links.py` mencetak setiap hyperlink, yang sudah diselesaikan sepenuhnya, ke konsol. Skrip ini mendemonstrasikan **how to parse html**, **how to use selector**, dan **extract hyperlinks from html** dalam alur kerja yang dapat digunakan kembali.

## Variasi umum dan penanganan kasus tepi

| Situasi | Apa yang diubah | Alasan |
|-----------|----------------|--------|
| **Hanya URL absolut yang dibutuhkan** | Hapus argumen `base_url` dalam `extract_hyperlinks` | Membiarkan URL relatif tidak tersentuh |
| **Anda juga membutuhkan teks tautan** | Kembalikan tuple `(href, link.text_content())` dari `extract_hyperlinks` | Memungkinkan Anda menyimpan URL dan teks anchor |
| **File HTML besar** | Gunakan `lxml.etree.iterparse` dengan filter CSS selector | Mengurangi penggunaan memori dengan streaming |
| **Selector berbeda** | Ganti `"a"` dengan `"nav a[href]"` atau `"div.content a.external"` | Menargetkan subset tautan, berguna untuk **how to use selector** pada halaman kompleks |

**Pro tip:** Selalu validasi URL yang diekstrak sebelum melakukan permintaan jaringan. Pemeriksaan cepat dengan `urlparse` dapat menyaring string yang rusak dan melindungi scraper Anda dari crash.

## Kesimpulan

Anda kini tahu **how to parse html** di Python, cara **load html document python**, cara **how to use selector** untuk menargetkan elemen, dan cara **extract hyperlinks from html** secara efisien. Contoh lengkap di atas siap disalin‑tempel ke proyek Anda, dan Anda dapat menyesuaikan setiap fungsi untuk kasus penggunaan yang lebih maju seperti pagination, konten yang dihasilkan JavaScript, atau perayapan multi‑halaman.

Langkah selanjutnya yang dapat Anda jelajahi meliputi:

- Menggunakan **requests‑html** atau **Playwright** untuk mengambil halaman yang memerlukan eksekusi JavaScript.  
- Menyimpan URL yang diekstrak ke CSV atau basis data SQLite untuk analisis selanjutnya.  
- Menambahkan penanganan error untuk timeout jaringan dan kode status HTTP.

Selamat mem‑parse, dan silakan bereksperimen dengan selector yang berbeda untuk membuka potensi penuh kueri HTML berbasis CSS di Python!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara mengkonfigurasi penanganan sumber daya HTML di Python dan memuat dokumen HTML](/html/english/python/general/how-to-configure-html-resource-handling-in-python-and-load-a/)
- [Cara Mem-parse HTML di Python – Panduan Lengkap](/html/english/python/general/how-to-parse-html-in-python-complete-guide/)
- [Cara Memuat HTML di Python – Panduan Langkah‑per‑Langkah](/html/english/python/general/how-to-load-html-in-python-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
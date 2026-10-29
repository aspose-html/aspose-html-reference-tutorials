---
category: general
date: 2026-06-26
description: Pelajari cara mendapatkan favicon dengan memuat HTML dari URL dan mengekstrak
  href dari tag link. Kode Python langkah demi langkah untuk mendapatkan ikon situs
  web dengan cepat.
draft: false
keywords:
- how to get favicon
- load html from url
- get website icons
- extract href from link
- how to extract favicons
language: id
og_description: 'Cara cepat mendapatkan favicon: muat HTML dari URL, temukan link
  rel=''icon'', dan ekstrak href dari tag link menggunakan Python.'
og_title: Cara Mendapatkan Favicon – Tutorial Python
schemas:
- author: Aspose
  dateModified: '2026-06-26'
  description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  headline: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  type: TechArticle
- description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  name: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  steps:
  - name: What if the site uses a `<meta>` tag instead of `<link>`?
    text: Some older pages embed the icon URL in a `<meta name="msapplication‑TileImage">`.
      You can extend `find_icon_links` to also search for those meta tags and treat
      them the same way.
  - name: How do I handle relative URLs that start with `//`?
    text: '`urljoin` automatically resolves protocol‑relative URLs (`//example.com/favicon.ico`)
      based on the scheme of the base URL, so you don’t need extra logic.'
  - name: Can I retrieve multiple sizes (e.g., 32×32, 180×180) automatically?
    text: Yes—just drop the `filter_ico_urls` step. The script will return every icon
      URL it discovers, including PNGs of various dimensions. You can then sort or
      select based on the filename pattern.
  - name: Does this work on sites that block bots?
    text: 'If a site returns a 403 or requires a custom User‑Agent, tweak the `requests.get`
      call:'
  type: HowTo
tags:
- Python
- Web Scraping
- HTML Parsing
title: Cara Mendapatkan Favicon – Panduan Python Lengkap untuk Mengekstrak Ikon Situs
url: /id/python/general/how-to-get-favicon-complete-python-guide-for-extracting-site/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mendapatkan Favicon – Panduan Python Lengkap untuk Mengekstrak Ikon Situs

Pernah bertanya-tanya **how to get favicon** dari situs mana pun tanpa harus menggali sumber halaman secara manual? Anda bukan satu-satunya—pengembang, pakar SEO, dan bahkan desainer sering membutuhkan ikon kecil yang mewakili sebuah situs. Dalam tutorial ini kami akan menunjukkan cara yang bersih dan berfokus pada Python untuk memuat HTML dari sebuah URL, menemukan tag `<link rel="icon">`, dan mengambil URL ikon. Pada akhir tutorial, Anda akan tahu persis **how to get favicon** untuk domain apa pun, dan Anda akan memiliki skrip yang dapat digunakan kembali untuk proyek Anda.

Kami akan membahas semuanya mulai dari mengambil HTML hingga menangani kasus tepi seperti URL relatif dan berbagai format ikon. Tidak diperlukan layanan eksternal—hanya pustaka standar `requests` dan parser HTML ringan. Siap memulai? Mari kita selami.

## Prerequisites

- Python 3.8+ terpasang (kode juga berfungsi pada 3.10)  
- Familiaritas dasar dengan `requests` dan list comprehensions  
- Akses internet untuk situs target  

Jika Anda sudah memiliki semua ini, bagus—lanjutkan ke langkah pertama. Jika belum, instal satu-satunya dependensi yang kami perlukan:

```bash
pip install requests beautifulsoup4
```

> **Pro tip:** `beautifulsoup4` adalah parser yang telah teruji dalam pertempuran dan membuat “load html from url” menjadi sangat mudah.

## Step 1: Load HTML from URL with Python  

Hal pertama yang perlu Anda lakukan ketika mempelajari **how to get favicon** adalah mengambil sumber halaman. Inilah bagian “load html from url” dari proses tersebut.

```python
import requests
from bs4 import BeautifulSoup

def fetch_html(url: str) -> str:
    """Download the raw HTML of *url* and return it as text."""
    response = requests.get(url, timeout=10)
    response.raise_for_status()   # will raise if the request failed
    return response.text
```

Mengapa menggunakan `requests`? Karena ia menangani pengalihan, verifikasi HTTPS, dan timeout secara otomatis, yang berarti lebih sedikit kejutan ketika Anda kemudian mencoba **get website icons**.

## Step 2: Parse the Document and Find Icon Links  

Sekarang kita sudah memiliki HTML, kita perlu menemukan semua elemen `<link>` yang atribut `rel`‑nya menunjukkan sebuah ikon. Inilah inti dari **how to get favicon**.

```python
def find_icon_links(html: str) -> list[BeautifulSoup]:
    """Return a list of <link> tags that declare an icon."""
    soup = BeautifulSoup(html, "html.parser")
    # Look for rel="icon" or rel="shortcut icon"
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]
```

Perhatikan kami memeriksa baik `icon` maupun `shortcut icon` karena situs lama masih menggunakan yang terakhir. Nuansa kecil ini sering membuat orang kebingungan ketika mereka mencari “how to extract favicons.”

## Step 3: Extract href from Link Elements  

Dengan tag yang relevan di tangan, langkah logis berikutnya—**extract href from link**—sangat sederhana.

```python
from urllib.parse import urljoin

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    """Convert each <link> tag’s href into a full absolute URL."""
    urls = []
    for tag in link_tags:
        href = tag.get("href")
        if href:
            # Resolve relative URLs against the base page
            full_url = urljoin(base_url, href)
            urls.append(full_url)
    return urls
```

Menggunakan `urljoin` menjamin bahwa bahkan jika sebuah situs memberikan jalur relatif seperti `/favicon.ico`, Anda akan mendapatkan URL absolut yang tepat—kritikal untuk skrip **how to get favicon** yang dapat diandalkan.

## Step 4: Optional – Validate and Filter Icon URLs  

Kadang sebuah halaman mencantumkan banyak ikon (Apple touch icons, PNG dengan berbagai ukuran, dll.). Jika Anda hanya menginginkan file `.ico` klasik, filterlah sesuai. Langkah ini menunjukkan **how to extract favicons** dengan tipe tertentu.

```python
def filter_ico_urls(urls: list[str]) -> list[str]:
    """Keep only URLs that end with .ico (case‑insensitive)."""
    return [u for u in urls if u.lower().endswith(".ico")]
```

Silakan sesuaikan filter: ganti `".ico"` dengan `".png"` atau periksa `rel="apple-touch-icon"` jika Anda membutuhkan ikon resolusi tinggi.

## Step 5: Download the Icon Files (If You Want the Actual Image)  

Mengekstrak URL hanyalah setengah dari perjuangan; mengunduh memberi Anda file yang dapat ditampilkan atau disimpan. Berikut helper singkatnya:

```python
import os

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    """Save each icon to *folder*, creating it if necessary."""
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")
```

Menjalankan ini setelah langkah‑langkah sebelumnya akan memberi Anda salinan lokal dari setiap favicon yang ditemukan, sempurna untuk caching atau analisis offline.

## Step 6: Putting It All Together – Full Working Example  

Berikut adalah skrip lengkap yang siap dijalankan dan mendemonstrasikan **how to get favicon** dari situs apa pun. Salin‑tempel, ubah `target_url`, dan lihat hasilnya.

```python
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin
import os

def fetch_html(url: str) -> str:
    response = requests.get(url, timeout=10)
    response.raise_for_status()
    return response.text

def find_icon_links(html: str) -> list[BeautifulSoup]:
    soup = BeautifulSoup(html, "html.parser")
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    return [urljoin(base_url, tag.get("href")) for tag in link_tags if tag.get("href")]

def filter_ico_urls(urls: list[str]) -> list[str]:
    return [u for u in urls if u.lower().endswith(".ico")]

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")

def get_favicons(target_url: str) -> None:
    print(f"Fetching HTML from {target_url} …")
    html = fetch_html(target_url)

    print("Finding <link> tags that declare icons …")
    icon_tags = find_icon_links(html)

    print(f"Extracting href attributes – {len(icon_tags)} candidates found.")
    raw_urls = extract_icon_urls(target_url, icon_tags)

    # Optional filtering – keep only .ico files
    ico_urls = filter_ico_urls(raw_urls)
    print(f"Filtered to {len(ico_urls)} .ico URLs:", ico_urls)

    if ico_urls:
        download_icons(ico_urls)
    else:
        print("No .ico favicons detected; here are all discovered URLs:")
        print(raw_urls)

# Example usage – replace with any site you want to test
if __name__ == "__main__":
    target_url = "https://www.python.org"
    get_favicons(target_url)
```

**Expected output (truncated for brevity):**

```
Fetching HTML from https://www.python.org …
Finding <link> tags that declare icons …
Extracting href attributes – 3 candidates found.
Filtered to 1 .ico URLs: ['https://www.python.org/static/favicon.ico']
Saved favicons/favicon.ico
```

Jika situs hanya menyediakan PNG atau Apple touch icons, skrip akan menampilkan URL‑URL tersebut sebagai gantinya, memperlihatkan secara tepat **how to get favicon** dalam setiap skenario.

## Common Questions & Edge Cases  

### What if the site uses a `<meta>` tag instead of `<link>`?  
Beberapa halaman lama menanamkan URL ikon dalam `<meta name="msapplication‑TileImage">`. Anda dapat memperluas `find_icon_links` untuk juga mencari meta tag tersebut dan memperlakukannya dengan cara yang sama.

### How do I handle relative URLs that start with `//`?  
`urljoin` secara otomatis menyelesaikan URL relatif protokol (`//example.com/favicon.ico`) berdasarkan skema URL dasar, jadi Anda tidak memerlukan logika tambahan.

### Can I retrieve multiple sizes (e.g., 32×32, 180×180) automatically?  
Ya—cukup lewati langkah `filter_ico_urls`. Skrip akan mengembalikan setiap URL ikon yang ditemukan, termasuk PNG dengan berbagai dimensi. Anda kemudian dapat menyortir atau memilih berdasarkan pola nama file.

### Does this work on sites that block bots?  
Jika sebuah situs mengembalikan 403 atau memerlukan User‑Agent khusus, sesuaikan panggilan `requests.get`:

```python
headers = {"User-Agent": "Mozilla/5.0 (compatible; FaviconBot/1.0)"}
response = requests.get(url, headers=headers, timeout=10)
```

Perubahan kecil ini sering menyelesaikan “how to get favicon” pada domain yang lebih ketat.

## Visual Overview  

![Diagram showing the flow of how to get favicon from a website – load HTML, parse link tags, extract href, optional download](how-to-get-favicon-diagram.png "how to get favicon flow diagram")

*Teks alt gambar berisi kata kunci utama, memenuhi kebutuhan SEO untuk gambar.*

## Conclusion  

Kami telah menelusuri **how to get favicon** langkah demi langkah: memuat HTML dari sebuah URL,

## What Should You Learn Next?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Menyimpan HTML di C# – Panduan Lengkap Menggunakan Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Cara Mengedit HTML Menggunakan Aspose.HTML untuk Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Cara Mengonversi HTML ke PDF dengan Java – Menggunakan Aspose.HTML untuk Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
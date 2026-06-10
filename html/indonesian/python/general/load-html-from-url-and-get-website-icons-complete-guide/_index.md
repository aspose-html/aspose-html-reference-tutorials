---
category: general
date: 2026-06-10
description: Muat HTML dari URL untuk mendapatkan ikon situs web dengan cepat. Pelajari
  cara mengekstrak favicon, mengambil URL favicon situs web, dan menangani kasus khusus
  dalam Python.
draft: false
keywords:
- load html from url
- get website icons
- how to extract favicons
- extract favicon urls
- fetch website favicon urls
language: id
og_description: Muat HTML dari URL untuk mengekstrak favicon dan mengambil URL favicon
  situs web. Tutorial Python langkah demi langkah untuk pengembang.
og_title: Muat HTML dari URL dan Dapatkan Ikon Situs Web – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Load HTML from URL to get website icons quickly. Learn how to extract
    favicons, fetch website favicon URLs, and handle edge cases in Python.
  headline: Load HTML from URL and Get Website Icons – Complete Guide
  type: TechArticle
tags:
- web scraping
- favicon extraction
- python
- html parsing
title: Muat HTML dari URL dan Dapatkan Ikon Situs Web – Panduan Lengkap
url: /id/python/general/load-html-from-url-and-get-website-icons-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Muat HTML dari URL dan Dapatkan Ikon Situs Web – Panduan Lengkap

Pernahkah Anda perlu **load HTML from URL** hanya untuk mengambil logo kecil sebuah situs? Anda tidak sendirian. Baik Anda sedang membangun manajer bookmark, dasbor SEO, atau hanya proyek hobi pribadi, mendapatkan ikon situs web adalah bagian kecil namun penting dari puzzle.

Dalam tutorial ini kami akan menunjukkan **how to extract favicons** menggunakan Python biasa—tanpa Selenium yang berat, tanpa sihir browser. Pada akhir tutorial Anda akan dapat **fetch website favicon URLs**, menangani jalur relatif, dan bahkan mengambil beberapa ikon jika sebuah situs menyediakannya. Siap? Mari kita mulai.

## Mengapa Memuat HTML dari URL di Awal?

Memuat HTML mentah sebuah halaman memberi Anda akses langsung ke tag `<link>` yang digunakan browser untuk menemukan favicon. Tag-tag tersebut biasanya terlihat seperti:

```html
<link rel="icon" href="/favicon.ico">
<link rel="apple-touch-icon" href="https://example.com/apple-touch-icon.png">
```

Jika Anda dapat mengambil markup tersebut, Anda dapat secara program membaca atribut `href` dan mengunduh gambar sendiri. Ini lebih cepat daripada mengambil screenshot, dan berfungsi untuk situs apa pun yang mengikuti konvensi standar.

## Langkah 1 – Muat Dokumen HTML dari URL

Hal pertama yang kita butuhkan adalah cara untuk mengambil sumber halaman. Pilihan paling populer di Python adalah pustaka **requests** karena sederhana, dapat diandalkan, dan menangani pengalihan secara otomatis.

```python
import requests

def fetch_html(url: str) -> str:
    """
    Retrieve the raw HTML from the given URL.
    Raises an exception if the request fails.
    """
    response = requests.get(url, timeout=10)
    response.raise_for_status()          # Fail fast on HTTP errors
    return response.text
```

> **Pro tip:** Jika Anda bekerja di belakang proxy perusahaan, berikan `proxies=` ke `requests.get`. Selain itu, mengatur timeout singkat mencegah skrip Anda menggantung pada situs yang tidak responsif.

Sekarang kita dapat memanggil `fetch_html("https://example.com")` dan mendapatkan string yang berisi markup halaman. Ini adalah inti dari **load HTML from URL**—sisa pipeline bekerja dengan string tersebut.

## Langkah 2 – Dapatkan Ikon Situs Web

Setelah kita memiliki HTML, langkah selanjutnya adalah menemukan setiap elemen `<link>` yang atribut `rel`‑nya menyebutkan “icon”. Modul bawaan `html.parser` dapat melakukan pekerjaan ini, namun **BeautifulSoup** membuat kode jauh lebih mudah dibaca.

```python
from bs4 import BeautifulSoup
from urllib.parse import urljoin

def extract_icon_links(html: str, base_url: str) -> list[str]:
    """
    Parse the HTML and return a list of absolute URLs pointing to icons.
    Handles relative hrefs by joining them with the page’s base URL.
    """
    soup = BeautifulSoup(html, "html.parser")
    icons = []

    # Look for any <link> tag where rel contains "icon"
    for link in soup.find_all("link", rel=lambda r: r and "icon" in r.lower()):
        href = link.get("href")
        if href:
            # Convert relative URLs to absolute ones
            absolute_url = urljoin(base_url, href)
            icons.append(absolute_url)

    return icons
```

Perhatikan bagaimana kami menggunakan `urljoin` untuk mengubah `"/favicon.ico"` menjadi `"https://example.com/favicon.ico"`—itu adalah kasus tepi umum saat **get website icons**. Beberapa situs bahkan menyajikan ikon berbeda untuk perangkat yang berbeda, sehingga Anda mungkin mendapatkan beberapa URL. Tidak masalah; kami hanya mengumpulkannya semua.

## Langkah 3 – Ekstrak URL Favicon dan Tampilkan

Menggabungkan semua bagian cukup sederhana. Kami akan mengambil HTML, menjalankan ekstraktor, dan mencetak daftar hasilnya. Skrip akhir terlihat seperti ini:

```python
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin

def fetch_html(url: str) -> str:
    response = requests.get(url, timeout=10)
    response.raise_for_status()
    return response.text

def extract_icon_links(html: str, base_url: str) -> list[str]:
    soup = BeautifulSoup(html, "html.parser")
    icons = []
    for link in soup.find_all("link", rel=lambda r: r and "icon" in r.lower()):
        href = link.get("href")
        if href:
            icons.append(urljoin(base_url, href))
    return icons

def main():
    target = "https://example.com"
    html = fetch_html(target)
    icon_urls = extract_icon_links(html, target)
    print("Found icon URLs:", icon_urls)

if __name__ == "__main__":
    main()
```

### Output yang Diharapkan

Menjalankan skrip terhadap situs yang menyediakan favicon standar mungkin menghasilkan:

```
Found icon URLs: ['https://example.com/favicon.ico']
```

Jika situs menyediakan beberapa ikon (Apple touch icon, shortcut icon, dll.), Anda akan melihat daftar yang lebih panjang:

```
Found icon URLs: [
    'https://example.com/favicon.ico',
    'https://example.com/apple-touch-icon.png',
    'https://example.com/favicon-32x32.png'
]
```

Itulah seluruh alur kerja **extract favicon urls**—kompak, ringan dependensi, dan siap dimasukkan ke proyek mana pun.

## Menangani Kendala Umum

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **Relative `href` tanpa tag `<base>`** | `urljoin` mengasumsikan URL halaman sebagai basis, yang bekerja untuk kebanyakan kasus. | Jika ada tag `<base href="...">`, bacalah terlebih dahulu dan berikan sebagai `base_url`. |
| **Tidak ada `rel="icon"`** | Beberapa situs menggunakan `rel="shortcut icon"` atau nilai khusus. | Perluas lambda: `rel=lambda r: r and ("icon" in r.lower() or "shortcut" in r.lower())`. |
| **Redirects ke domain berbeda** | Favicon mungkin berada di CDN. | `urljoin` akan menyelesaikan domain baru dengan benar karena menggunakan URL permintaan akhir (`response.url`). |
| **Tautan rusak (404)** | HTML mengarah ke file yang tidak lagi ada. | Setelah mengekstrak URL, Anda dapat memverifikasi masing-masing dengan permintaan HEAD sebelum menggunakannya. |
| **Beberapa tag `<link>` dengan ikon yang sama** | Entri duplikat memperbanyak daftar. | Gunakan `set(icon_urls)` untuk menghilangkan duplikat sebelum mengembalikan. |

## Lebih Lanjut – Ambil URL Favicon Situs Web secara Massal

Jika Anda perlu **fetch website favicon URLs** untuk daftar domain, bungkus logika `main` dalam sebuah loop:

```python
domains = ["https://example.com", "https://python.org", "https://github.com"]
for site in domains:
    try:
        icons = extract_icon_links(fetch_html(site), site)
        print(site, "->", icons)
    except Exception as e:
        print(site, "error:", e)
```

Pola ini skala dengan baik, dan Anda dapat menambahkan caching (misalnya, dengan `functools.lru_cache`) untuk menghindari menabrak situs yang sama berulang kali.

## Gambaran Visual

![Diagram memuat HTML dari URL](load-html-url.png)

*Teks alternatif: Diagram memuat HTML dari URL yang menunjukkan langkah fetch → parse → extract.*

Gambar di atas merangkum proses tiga langkah: **load HTML from URL**, **get website icons**, dan **extract favicon URLs**. Ini berguna ketika Anda perlu menjelaskan alur tersebut kepada rekan tim.

## Kesimpulan

Kami telah membahas solusi lengkap yang siap produksi untuk cara **load HTML from URL** dan **get website icons** menggunakan hanya pustaka requests dan BeautifulSoup Python. Dengan mengekstrak atribut `href` dari tag `<link rel="icon">`, Anda dapat **extract favicon URLs**, menangani jalur relatif, dan bahkan mengambil beberapa format ikon—semua dalam beberapa puluh baris kode.

Apa selanjutnya? Coba unduh ikon ke folder lokal, buat CSV pemetaan domain‑ke‑favicon, atau sambungkan logika ini ke API Flask yang menyajikan favicon sesuai permintaan. Kemungkinan untuk **fetch website favicon URLs** tidak terbatas, dan teknik inti tetap sama.

Punya pertanyaan tentang kasus tepi, atau ingin berbagi trik cerdas? Tinggalkan komentar di bawah—selamat berburu ikon!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Muat Dokumen HTML dari File di Aspose.HTML untuk Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Muat Dokumen HTML dari Stream dengan Aspose.HTML untuk Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-stream/)
- [Tangani Peristiwa Muat Dokumen di Aspose.HTML untuk Java](/html/english/java/creating-managing-html-documents/handle-document-load-events/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
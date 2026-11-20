---
category: general
date: 2026-05-28
description: Cara mem-parsing HTML di Python dengan cepat—memuat file HTML, menggunakan
  selector CSS, dan mengekstrak atribut href dengan contoh XPath contains.
draft: false
keywords:
- how to parse html
- get href attribute
- load html file
- use css selector
- xpath contains example
language: id
og_description: 'Cara mengurai HTML di Python: pelajari cara memuat file HTML, menggunakan
  selector CSS, dan mendapatkan atribut href dengan contoh XPath contains.'
og_title: Cara Mengurai HTML di Python – Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  headline: How to Parse HTML in Python – Complete Guide
  type: TechArticle
- description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  name: How to Parse HTML in Python – Complete Guide
  steps:
  - name: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
    text: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
  - name: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
    text: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
  - name: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
    text: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
  - name: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
    text: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
  type: HowTo
tags:
- html parsing
- python
- web scraping
title: Cara Mengurai HTML di Python – Panduan Lengkap
url: /id/python/general/how-to-parse-html-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Parse HTML in Python – Complete Guide

Pernah bertanya‑tanya **bagaimana cara mem‑parse HTML** dalam skrip Python tanpa harus meng‑import browser yang berat? Anda tidak sendirian. Kebanyakan dari kita hanya perlu **memuat file HTML**, mengambil beberapa judul artikel, dan mungkin mengambil satu atau dua tautan unduhan. Dalam tutorial ini saya akan menunjukkan hal itu—menggunakan pustaka kecil, selector CSS, dan contoh XPath contains untuk **mengambil nilai atribut href**.

Kita akan melangkah melalui seluruh proses, mulai dari membaca dokumen HTML lokal hingga mencetak data yang Anda butuhkan. Tanpa basa‑basi, hanya contoh praktis yang dapat dijalankan dan langsung Anda gunakan dalam proyek Anda hari ini.

## What You’ll Learn

- Cara **memuat file HTML** dengan parser ringan.
- Cara **menggunakan sintaks CSS selector** untuk mengambil elemen seperti judul artikel.
- Cara membuat **contoh XPath contains** yang memfilter tautan.
- Cara **mengambil nilai atribut href** secara aman dari node yang cocok.
- Tips menangani markup yang rusak dan memperluas skrip.

Anda hanya memerlukan Python 3.8+ serta paket `lxml` dan `cssselect`—keduanya dapat di‑install dengan satu perintah `pip`.

---

## Step 1: Load the HTML File

Sebelum apa pun, Anda perlu memuat konten HTML ke dalam memori. Modul `lxml.html` menyediakan helper `fromstring` yang praktis, tetapi ketika Anda memiliki file di disk fungsi `parse` jauh lebih bersih.

```python
# Step 1: Load the HTML file
from lxml import html

# Replace the path with the location of your HTML document
html_path = "YOUR_DIRECTORY/news.html"
doc = html.parse(html_path)

# The root element gives us access to CSS and XPath methods
root = doc.getroot()
```

> **Mengapa ini penting:** Memuat file sekali saja menjaga penggunaan memori tetap rendah dan memberi Anda satu objek `root` yang mendukung baik selector CSS maupun kueri XPath. Jika file tidak ada atau tidak dapat dibaca, `html.parse` akan mengeluarkan `OSError` yang jelas, yang dapat Anda tangkap nanti.

### Pro tip
Jika Anda berurusan dengan string alih‑alih file, ganti `html.parse` dengan `html.fromstring(your_html_string)`.

---

## Step 2: Use CSS Selector to Get Headlines

Selector CSS singkat dan familiar bagi siapa saja yang pernah menulis stylesheet. Mari ambil setiap `<h2>` di dalam `<article>`—sempurna untuk judul berita.

```python
# Step 2: Find all article headlines using a CSS selector
headline_nodes = root.cssselect("article h2")

# Print each headline's text content
for node in headline_nodes:
    print(node.text_content().strip())
```

**Expected output** (asumsi HTML contoh berisi dua artikel):

```
Breaking News: Python Takes Over the World
Local Developer Solves HTML Parsing Puzzle
```

> **Mengapa CSS?** Mudah dibaca, cepat, dan langsung bekerja dengan `lxml`. Metode `cssselect` menerjemahkan selector menjadi ekspresi XPath di balik layar, memberi Anda kelebihan kedua dunia.

---

## Step 3: XPath Contains Example – Find “download” Links

Kadang‑kadang Anda memerlukan kontrol yang lebih detail daripada yang ditawarkan CSS. Fungsi `contains()` pada XPath sangat berguna ketika Anda ingin mencocokkan substring di dalam atribut, seperti semua tautan yang mengarah ke unduhan.

```python
# Step 3: Find all links that contain the word "download" using XPath
download_link_nodes = root.xpath("//a[contains(@href, 'download')]")

# Extract and print the href attribute from each matching node
for node in download_link_nodes:
    href = node.get("href")
    print(href)
```

**Sample output**:

```
/files/report_download.pdf
https://example.com/downloads/setup.exe
```

> **Mengapa XPath contains?** Ia memungkinkan Anda memfilter langsung berdasarkan nilai atribut tanpa loop Python tambahan. Ini adalah contoh **xpath contains** klasik yang sering Anda lihat di tutorial, tetapi di sini dipadukan dengan kasus penggunaan dunia nyata.

---

## Step 4: Wrap It All Into a Reusable Function

Menuliskan jalur dan `print` secara hard‑code memang cukup untuk percobaan cepat, tetapi kode produksi lebih suka fungsi. Di bawah ini helper ringkas yang mengembalikan baik judul artikel maupun tautan unduhan.

```python
def parse_news_html(file_path):
    """
    Parse a news HTML file and return headlines plus download URLs.

    Parameters
    ----------
    file_path : str
        Path to the local HTML document.

    Returns
    -------
    dict
        {
            "headlines": list of strings,
            "download_links": list of href strings
        }
    """
    doc = html.parse(file_path)
    root = doc.getroot()

    # Headlines via CSS selector
    headlines = [
        node.text_content().strip()
        for node in root.cssselect("article h2")
    ]

    # Download links via XPath contains
    download_links = [
        node.get("href")
        for node in root.xpath("//a[contains(@href, 'download')]")
    ]

    return {"headlines": headlines, "download_links": download_links}
```

Sekarang Anda dapat memanggil fungsi tersebut dan mencetak hasilnya dengan rapi:

```python
if __name__ == "__main__":
    results = parse_news_html("YOUR_DIRECTORY/news.html")
    print("Headlines:")
    for h in results["headlines"]:
        print(f"- {h}")

    print("\nDownload Links:")
    for link in results["download_links"]:
        print(f"- {link}")
```

Menjalankan skrip menghasilkan output yang sama seperti sebelumnya, tetapi kini terpaket rapi untuk penggunaan kembali.

---

## Step 5: Handling Edge Cases and Common Pitfalls

1. **Atribut `href` yang hilang** – XPath tetap mengembalikan node `<a>` meskipun `href` tidak ada. Lindungi dari `None`:

   ```python
   href = node.get("href")
   if href:
       download_links.append(href)
   ```

2. **URL relatif vs. absolut** – Jika tautan Anda relatif, Anda mungkin ingin menyelesaikannya terhadap URL dasar:

   ```python
   from urllib.parse import urljoin
   base_url = "https://example.com"
   absolute = urljoin(base_url, href)
   ```

3. **HTML yang rusak** – `lxml` toleran, tetapi markup yang sangat rusak dapat menyebabkan `html.parse` mengeluarkan `XMLSyntaxError`. Bungkus pemanggilan `parse` dalam blok `try/except` untuk mencatat dan melewati file yang bermasalah.

4. **Kinerja dengan file besar** – Untuk halaman berukuran multi‑megabyte, pertimbangkan streaming dengan `iterparse` alih‑alih memuat seluruh DOM ke memori.

---

## Visual Overview (optional)

![Diagram alur cara mem‑parse HTML yang menunjukkan memuat file → CSS selector → XPath contains → mengambil atribut href](how-to-parse-html-flow.png "Diagram alur cara mem‑parse HTML")

*Alt text mencakup kata kunci utama untuk memenuhi SEO.*

---

## Conclusion

Kami telah membahas **cara mem‑parse HTML** di Python dari awal hingga akhir: memuat file HTML, menggunakan CSS selector untuk mengambil judul artikel, membuat contoh XPath contains untuk menemukan tautan unduhan, dan akhirnya **mengambil nilai atribut href** secara aman. Fungsi `parse_news_html` yang dapat dipakai ulang menunjukkan pendekatan bersih dan dapat dipelihara yang dapat Anda adaptasi untuk tugas scraping apa pun.

Siap untuk tantangan berikutnya? Coba kembangkan skrip untuk:

- Mem‑parse tabel dengan kueri XPath `//table//tr`.
- Mengekstrak atribut `src` gambar menggunakan contoh **xpath contains** lainnya.
- Beralih ke pengambilan asinkron dengan `aiohttp` untuk halaman web langsung.

Selamat mem‑parse, dan ingat—setelah Anda menguasai dasar‑dasarnya, seluruh proses scraping HTML menjadi sangat mudah. Jika Anda menemukan kendala, tinggalkan komentar di bawah—mari kita selesaikan bersama!

## Related Tutorials

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-07-05
description: Buka tautan di tab baru menggunakan Python – pelajari cara menambahkan
  target blank, mengubah target tautan, menggunakan selector yang mengandung atribut,
  dan menyimpan HTML yang dimodifikasi dengan mudah.
draft: false
keywords:
- open links new tab
- add target blank
- change link target
- attribute contains selector
- save modified html
language: id
og_description: Buka tautan di tab baru dengan cepat. Tutorial ini menunjukkan cara
  menambahkan target blank, mengubah target tautan, dan menyimpan HTML yang dimodifikasi
  dengan Python.
og_title: Buka Tautan di Tab Baru – Panduan Pembaruan HTML Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  headline: Open Links New Tab – Complete Guide to Updating HTML Anchors
  type: TechArticle
- description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  name: Open Links New Tab – Complete Guide to Updating HTML Anchors
  steps:
  - name: Expected Result
    text: 'Suppose `links.html` originally contained:'
  - name: What if a link already has a `rel` attribute?
    text: 'Our loop overwrites it with `"noopener"`. If you need to preserve existing
      values (e.g., `"nofollow"`), concatenate instead:'
  - name: How to handle multiple domains?
    text: 'Just expand the selector list:'
  - name: Does `prettify()` change the original HTML structure?
    text: It re‑indents but doesn’t alter tag order or attribute values. If you must
      keep the exact original whitespace, replace `prettify()` with `str(soup)` as
      mentioned earlier.
  type: HowTo
tags:
- HTML manipulation
- Python
- web automation
title: Buka Tautan di Tab Baru – Panduan Lengkap Memperbarui Anchor HTML
url: /id/python/general/open-links-new-tab-complete-guide-to-updating-html-anchors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buka Tautan di Tab Baru – Panduan Lengkap untuk Memperbarui Anchor HTML

Pernahkah Anda perlu **open links new tab** pada halaman HTML statis tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian. Banyak pengembang mengalami masalah ini saat membersihkan situs warisan atau menambahkan penyesuaian aksesibilitas. Dalam tutorial ini kami akan menjelaskan solusi praktis yang **adds target blank**, **changes link target**, dan dengan aman **saves modified html**—semua dengan beberapa baris Python.

Kami juga akan membahas cara menggunakan **attribute contains selector** sehingga Anda hanya menyentuh anchor yang benar‑benar penting (misalnya, setiap tautan yang mengarah ke *example.com*). Pada akhir tutorial, Anda akan memiliki skrip yang dapat dipakai ulang dan dapat ditempatkan di proyek apa pun, besar atau kecil.

## Apa yang Akan Anda Pelajari

- Memuat file HTML ke dalam objek dokumen yang dapat dimanipulasi.  
- Memilih elemen `<a>` yang atribut `href`‑nya mengandung substring tertentu.  
- **Add target blank** dan menetapkan atribut `rel="noopener"` untuk meningkatkan keamanan.  
- **Save modified html** kembali ke disk tanpa kehilangan format.  

Tidak ada dependensi eksternal selain pustaka standar dan **beautifulsoup4** (instalasi yang sangat ringan). Jika Anda sudah menggunakan parser lain, konsep‑konsep ini dapat langsung diterapkan.

---

## Prasyarat

- Python 3.8+ terpasang di mesin Anda.  
- Familiaritas dasar dengan HTML dan Python.  
- Paket `beautifulsoup4` (`pip install beautifulsoup4`).  

Itu saja—tidak diperlukan kerangka kerja berat.

---

## Langkah 1: Muat Dokumen HTML

Pertama‑tama: kita perlu membaca file sumber dan menyerahkannya ke BeautifulSoup. Anggap ini seperti membuka kanvas kosong di mana Anda dapat menambahkan atribut baru.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Path to the original HTML file
html_path = Path("YOUR_DIRECTORY/links.html")

# Read the file content
with html_path.open(encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")
```

> **Why this matters:** Menggunakan `Path` membuat kode bersifat OS‑agnostic, dan `html.parser` sudah built‑in, jadi Anda tidak memerlukan parser tambahan untuk tugas sederhana.

---

## Langkah 2: Gunakan Attribute Contains Selector untuk Menemukan Tautan yang Tepat

Kami hanya ingin menyentuh anchor yang mengarah ke *example.com*. Selektor CSS `a[href*='example.com']` melakukan hal itu—`*=` berarti “mengandung”. Metode `select` milik BeautifulSoup memahami sintaks ini.

```python
# Find all <a> tags whose href contains 'example.com'
selector = "a[href*='example.com']"
anchor_elements = soup.select(selector)
```

> **Pro tip:** Jika Anda memerlukan pencocokan yang tidak sensitif huruf besar/kecil, beralihlah ke loop kecil yang memeriksa `if 'example.com' in a.get('href', '').lower()`.

Sekarang `anchor_elements` berisi setiap tautan yang kami pedulikan, siap untuk transformasi selanjutnya.

---

## Langkah 3: Ubah Target Tautan – Tambahkan Target Blank dan Amankan Tautan

Membuka tautan di tab baru sesederhana menetapkan `target="_blank"`. Namun, browser modern juga menyarankan menambahkan `rel="noopener"` (atau `noreferrer`) untuk mencegah halaman yang baru dibuka mengakses jendela asal melalui `window.opener`. Penyesuaian keamanan kecil ini dapat menghentikan serangan phishing.

```python
for anchor in anchor_elements:
    # Open in a new tab
    anchor['target'] = "_blank"          # add target blank
    # Harden security
    anchor['rel'] = "noopener"           # prevent access to the opener page
```

> **Why we use direct dictionary assignment:** Secara otomatis membuat atribut jika belum ada, dan menimpanya jika sudah ada—sempurna untuk operasi **change link target**.

---

## Langkah 4: Simpan HTML yang Dimodifikasi Kembali ke Disk

Langkah terakhir adalah menulis markup yang telah diperbarui ke file baru. Menjaga file asli tetap tidak tersentuh memungkinkan Anda mengembalikan perubahan jika ada yang salah.

```python
# Destination path for the updated HTML
output_path = Path("YOUR_DIRECTORY/links-updated.html")

# Write the prettified HTML (preserves indentation)
with output_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())
```

> **What `prettify()` does:** Memformat HTML dengan indentasi yang rapi, sehingga file yang disimpan lebih mudah dibaca dan dibandingkan nanti. Jika Anda lebih suka whitespace asli, ganti `prettify()` dengan `str(soup)`.

---

## Skrip Lengkap – Solusi Satu‑Klik

Berikut adalah skrip lengkap yang siap dijalankan. Simpan sebagai `update_links.py` dan jalankan `python update_links.py` dari terminal Anda.

```python
#!/usr/bin/env python3
"""
Open Links New Tab – script that adds target blank,
sets rel="noopener", and saves modified html.
"""

from pathlib import Path
from bs4 import BeautifulSoup

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Load the HTML document
    # ------------------------------------------------------------------
    html_path = Path("YOUR_DIRECTORY/links.html")
    with html_path.open(encoding="utf-8") as f:
        soup = BeautifulSoup(f, "html.parser")

    # ------------------------------------------------------------------
    # 2️⃣ Select anchors with an attribute contains selector
    # ------------------------------------------------------------------
    selector = "a[href*='example.com']"
    anchors = soup.select(selector)

    # ------------------------------------------------------------------
    # 3️⃣ Change link target – add target blank & secure the link
    # ------------------------------------------------------------------
    for a in anchors:
        a['target'] = "_blank"          # add target blank
        a['rel'] = "noopener"           # prevent opener access

    # ------------------------------------------------------------------
    # 4️⃣ Save modified html to a new file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/links-updated.html")
    with output_path.open("w", encoding="utf-8") as f:
        f.write(soup.prettify())

    print(f"✅ Updated {len(anchors)} link(s) and saved to {output_path}")

if __name__ == "__main__":
    main()
```

### Hasil yang Diharapkan

Misalkan `links.html` awalnya berisi:

```html
<a href="https://example.com/page1">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Setelah menjalankan skrip, `links-updated.html` akan terlihat seperti:

```html
<a href="https://example.com/page1" target="_blank" rel="noopener">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Hanya tautan ke *example.com* yang menerima atribut **add target blank**, menunjukkan bahwa **attribute contains selector** kami bekerja persis seperti yang diharapkan.

---

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika sebuah tautan sudah memiliki atribut `rel`?

Loop kami menimpanya dengan `"noopener"`. Jika Anda perlu mempertahankan nilai yang ada (misalnya, `"nofollow"`), gabungkan saja:

```python
existing = a.get('rel', '')
a['rel'] = f"{existing} noopener".strip()
```

### Bagaimana menangani banyak domain?

Cukup perluas daftar selector:

```python
domains = ["example.com", "sample.org"]
selector = ",".join([f"a[href*='{d}']" for d in domains])
anchors = soup.select(selector)
```

### Apakah `prettify()` mengubah struktur HTML asli?

Ia hanya meng‑indentasi ulang tetapi tidak mengubah urutan tag atau nilai atribut. Jika Anda harus mempertahankan whitespace asli secara persis, ganti `prettify()` dengan `str(soup)` seperti yang disebutkan sebelumnya.

---

## Tips Pro untuk Skrip Siap Produksi

- **Backup before overwriting:** Tambahkan langkah penyalinan (`shutil.copy`) untuk menjaga file asli tetap aman.  
- **Logging instead of print:** Gunakan modul `logging` untuk proyek yang skalabel.  
- **Batch processing:** Loop melalui direktori dengan `Path.rglob("*.html")` untuk memperbarui banyak file dalam satu kali jalan.  

Penyesuaian ini mengubah skrip **open links new tab** yang sederhana menjadi utilitas kuat untuk alur kerja pemeliharaan web apa pun.

---

## Kesimpulan

Anda kini memiliki metode yang solid dan dapat dipakai ulang untuk **open links new tab** di seluruh koleksi HTML statis. Dengan memanfaatkan **attribute contains selector**, Anda dapat **change link target** secara tepat di tempat yang diperlukan, **add target blank**, dan **save modified html** tanpa kehilangan format.

Cobalah pada halaman percobaan, lalu skalakan ke seluruh situs Anda. Perlu menyesuaikan selector untuk PDF, gambar, atau domain lain? Cukup ubah string CSS—semua hal lain tetap sama.

Silakan tinggalkan komentar jika Anda menemukan kejanggalan, atau bagikan bagaimana Anda memperluas skrip untuk proyek Anda sendiri. Selamat coding, semoga semua anchor Anda terbuka tepat di tempat yang Anda inginkan!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Mengedit HTML Menggunakan Aspose.HTML untuk Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Cara Menambahkan CSS – Inline CSS ke Dokumen HTML dalam Aspose.HTML untuk Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-06-07
description: Cara menambahkan awalan pada heading HTML menggunakan Python. Pelajari
  cara memilih beberapa heading, mengubah judul HTML, dan menyimpan HTML yang telah
  dimodifikasi secara efisien.
draft: false
keywords:
- how to add prefix
- select multiple headings
- save modified html
- change html titles
- modify html with python
language: id
og_description: Cara menambahkan awalan pada heading HTML menggunakan Python. Tutorial
  ini menunjukkan cara memilih beberapa heading, mengubah judul HTML, dan menyimpan
  HTML yang telah dimodifikasi hanya dalam beberapa baris.
og_title: Cara Menambahkan Awalan pada Heading HTML dengan Python – Panduan Cepat
schemas:
- author: Aspose
  dateModified: '2026-06-07'
  description: How to add prefix to HTML headings using Python. Learn to select multiple
    headings, change HTML titles, and save modified HTML efficiently.
  headline: How to Add Prefix to HTML Headings with Python – Step‑by‑Step Guide
  type: TechArticle
- description: How to add prefix to HTML headings using Python. Learn to select multiple
    headings, change HTML titles, and save modified HTML efficiently.
  name: How to Add Prefix to HTML Headings with Python – Step‑by‑Step Guide
  steps:
  - name: Verify the changes in a diff tool.
    text: Verify the changes in a diff tool.
  - name: Roll back instantly if something looks off.
    text: Roll back instantly if something looks off.
  - name: Keep the original untouched for audit purposes.
    text: Keep the original untouched for audit purposes.
  type: HowTo
tags:
- Python
- HTML
- Automation
- Web Scraping
title: Cara Menambahkan Awalan pada Heading HTML dengan Python – Panduan Langkah demi
  Langkah
url: /id/python/general/how-to-add-prefix-to-html-headings-with-python-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menambahkan Prefix ke Heading HTML dengan Python – Tutorial Lengkap

Menambahkan prefix ke heading HTML menggunakan Python adalah kebutuhan umum ketika Anda mengelola situs yang sering diperbarui. Dalam panduan ini kami akan membahas cara memilih banyak heading, mengubah judul HTML, dan menyimpan HTML yang telah dimodifikasi—semua tanpa meninggalkan editor Anda.  

Jika Anda pernah bertanya-tanya apakah Anda dapat mengotomatisasi badge “ditandai sebagai diperbarui” di puluhan halaman, Anda berada di tempat yang tepat. Kami juga akan menyentuh cara **modify html with python** secara skalabel, sehingga Anda tidak perlu membuka setiap file secara manual.

## Apa yang Akan Anda Capai

Pada akhir tutorial ini Anda akan dapat:

* **Memilih banyak heading** (`h1`, `h2`, `h3`) dalam satu kali proses.  
* **Menambahkan prefix khusus** (misalnya `[Updated]`) ke teks setiap heading.  
* **Menyimpan html yang dimodifikasi** kembali ke disk, mempertahankan struktur file asli.  
* Memahami trade‑off antara berbagai parser HTML Python, dan memilih yang paling cocok untuk proyek Anda.

Tanpa layanan eksternal, tanpa kerangka kerja berat—hanya Python murni dan beberapa pustaka yang terawat dengan baik.

---

## Cara Menambahkan Prefix ke Teks Heading di Python

Berikut adalah contoh minimal yang dapat dijalankan yang menunjukkan ide inti. Ia menggunakan pustaka **`lxml`** bersama **`cssselect`** untuk dukungan selector, yang meniru metode `query_selector_all` yang Anda lihat pada cuplikan asli.

```python
# -------------------------------------------------
# Step 0: Install dependencies (run once)
# -------------------------------------------------
# pip install lxml cssselect

# -------------------------------------------------
# Step 1: Load the HTML document
# -------------------------------------------------
from lxml import html

# Replace with your actual file path
input_path = "YOUR_DIRECTORY/article.html"
with open(input_path, "r", encoding="utf-8") as f:
    doc = html.fromstring(f.read())

# -------------------------------------------------
# Step 2: Select multiple headings (h1, h2, h3)
# -------------------------------------------------
# The CSS selector "h1, h2, h3" grabs all three levels.
headings = doc.cssselect("h1, h2, h3")

# -------------------------------------------------
# Step 3: Add the prefix "[Updated] " to each heading
# -------------------------------------------------
prefix = "[Updated] "
for heading in headings:
    # Preserve existing whitespace but prepend our tag
    heading.text = f"{prefix}{heading.text_content().strip()}"

# -------------------------------------------------
# Step 4: Save the modified HTML
# -------------------------------------------------
output_path = "YOUR_DIRECTORY/article_updated.html"
with open(output_path, "w", encoding="utf-8") as f:
    f.write(html.tostring(doc, pretty_print=True, encoding="unicode"))

print(f"✅ Finished! Modified file saved to {output_path}")
```

**Output yang diharapkan** (kutipan dari `article_updated.html`):

```html
<h1>[Updated] Introduction to Machine Learning</h1>
<h2>[Updated] Data Pre‑processing Steps</h2>
<h3>[Updated] Feature Engineering Techniques</h3>
```

Perhatikan bagaimana setiap heading kini dimulai dengan tag `[Updated]`—tepat seperti yang kami inginkan ketika menanyakan **how to add prefix** ke judul kami.

### Mengapa Pendekatan Ini Berhasil

* **`lxml` + `cssselect`** memberi Anda kekuatan selector CSS penuh, menjadikan langkah “select multiple headings” satu baris kode.  
* Metode `text_content()` mengekstrak teks dalam dengan aman, menghindari entitas HTML atau tag anak.  
* Menulis kembali dengan `pretty_print=True` menjaga file tetap dapat dibaca manusia, yang berguna untuk diff kontrol versi.

---

## Memilih Banyak Heading dengan CSS Selectors

Jika Anda berasal dari latar belakang JavaScript, sintaks `cssselect` akan terasa familiar. Selector `"h1, h2, h3"` adalah **daftar dipisahkan koma**, yang berarti “ambil elemen apa pun yang cocok *salah satu* dari tiga ini”.  

Anda juga dapat memperluas cakupan:

```python
# Grab every heading from h1 through h6
all_headings = doc.cssselect("h1, h2, h3, h4, h5, h6")
```

Atau mempersempitnya ke bagian tertentu:

```python
# Only headings inside the <article> tag
article_headings = doc.cssselect("article h1, article h2, article h3")
```

Penyesuaian kecil ini memungkinkan Anda **select multiple headings** dengan presisi laser, yang sangat berguna ketika Anda memiliki situs dokumentasi besar dan hanya ingin memperbarui sub‑bagian.

---

## Menyimpan File HTML yang Dimodifikasi dengan Aman

Saat Anda **save modified html**, Anda ingin menghindari kerusakan pada file asli. Pola yang ditunjukkan di atas menulis ke file baru (`article_updated.html`). Dengan cara ini Anda dapat:

1. Memverifikasi perubahan dengan alat diff.  
2. Mengembalikan secara instan jika ada yang terlihat tidak beres.  
3. Membiarkan file asli tidak tersentuh untuk keperluan audit.

Jika Anda lebih suka edit di tempat, cukup tukar jalurnya:

```python
import shutil
shutil.move(output_path, input_path)  # Overwrites the original
```

Namun ingat: **selalu backup** sebelum menimpa, terutama di server produksi.

---

## Mengubah Title HTML vs. Heading

Anda mungkin bertanya-tanya apakah “changing HTML titles” sama dengan menambahkan prefix pada heading. Dalam istilah HTML, tag `<title>` berada di dalam `<head>` dan mengontrol judul tab browser, sedangkan heading (`<h1>…<h3>`) muncul di badan halaman.

Jika Anda perlu **change html titles** juga, alur kerja `lxml` yang sama dapat diterapkan:

```python
# Change the <title> tag
title_elem = doc.find(".//title")
if title_elem is not None:
    title_elem.text = f"{prefix}{title_elem.text}"
```

Sekarang baik judul halaman maupun heading yang terlihat membawa flag `[Updated]` yang sama—sempurna untuk audit SEO di mana Anda menginginkan konsistensi antara meta‑data dan konten halaman.

---

## Pustaka Alternatif untuk modify html with python

Meskipun `lxml` cepat dan kaya fitur, Anda mungkin sudah menggunakan **BeautifulSoup** (bs4) dalam proyek Anda. Berikut logika yang sama dengan gaya yang lebih “pythonic”:

```python
from bs4 import BeautifulSoup

with open(input_path, "r", encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")

for tag in soup.select("h1, h2, h3"):
    tag.string = f"{prefix}{tag.get_text(strip=True)}"

with open(output_path, "w", encoding="utf-8") as f:
    f.write(str(soup.prettify()))
```

Kedua pustaka memungkinkan Anda **modify html with python**, jadi pilihlah yang cocok dengan stack yang sudah ada. `BeautifulSoup` unggul ketika Anda membutuhkan parsing yang toleran terhadap markup yang rusak, sementara `lxml` menawarkan kecepatan superior untuk batch besar.

---

## Pro Tips & Pitfalls Umum

* **Encoding penting** – selalu buka file dengan `encoding="utf-8"` untuk menghindari error Unicode pada karakter non‑ASCII.  
* **Hindari double‑prefixing** – jika Anda menjalankan skrip dua kali, Anda akan mendapatkan `[Updated] [Updated] …`. Cegah dengan memeriksa `heading.text.startswith(prefix)`.  
* **Pertahankan whitespace** – pemanggilan `strip()` menghapus spasi berlebih, menjaga output tetap rapi.  
* **Pemrosesan batch** – bungkus seluruh alur dalam loop `for file in pathlib.Path("YOUR_DIRECTORY").glob("*.html"):` untuk memperbarui seluruh folder dengan satu perintah.  

---

## Contoh Lengkap: Batch Update Direktori

Berikut adalah skrip ringkas yang mengiterasi setiap file `.html` dalam sebuah direktori, menambahkan prefix pada heading, memperbarui `<title>`, dan menulis file baru dengan akhiran `_updated`.

```python
import pathlib
from lxml import html

prefix = "[Updated] "
source_dir = pathlib.Path("YOUR_DIRECTORY")
output_dir = source_dir / "updated"
output_dir.mkdir(exist_ok=True)

for html_path in source_dir.glob("*.html"):
    # Load
    with open(html_path, "r", encoding="utf-8") as f:
        doc = html.fromstring(f.read())

    # Headings
    for h in doc.cssselect("h1, h2, h3"):
        if not h.text_content().startswith(prefix):
            h.text = f"{prefix}{h.text_content().strip()}"

    # Title
    title_elem = doc.find(".//title")
    if title_elem is not None and not title_elem.text.startswith(prefix):
        title_elem.text = f"{prefix}{title_elem.text}"

    # Save
    out_path = output_dir / f"{html_path.stem}_updated.html"
    with open(out_path, "w", encoding="utf-8") as f:
        f.write(html.tostring(doc, pretty_print=True, encoding="unicode"))

    print(f"✅ Processed {html_path.name} → {out_path.name}")
```

Jalankan sekali, dan setiap file HTML di `YOUR_DIRECTORY` akan mendapatkan badge `[Updated]` baru—tanpa perlu mengedit manual.

---

## Kesimpulan

Kami telah membahas **how to add prefix** ke heading HTML menggunakan Python, mendemonstrasikan cara **select multiple headings**, menunjukkan cara **save modified html** dengan aman, dan bahkan menyentuh **change html titles** untuk overhaul lengkap. Dengan memanfaatkan `lxml` atau `BeautifulSoup`, Anda kini memiliki toolbox yang solid untuk **modify html with python** dalam proyek dunia nyata.

Langkah selanjutnya? Coba tambahkan timestamp alih-alih tag statis, atau hasilkan file changelog yang mencantumkan setiap file yang Anda ubah. Anda juga dapat mengaitkan skrip ini ke pipeline CI sehingga setiap deployment otomatis


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
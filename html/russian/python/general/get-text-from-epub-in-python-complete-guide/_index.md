---
category: general
date: 2026-06-04
description: Быстро получайте текст из EPUB и узнайте, как читать файлы EPUB, конвертировать
  EPUB в текст и извлекать главы с помощью Python.
draft: false
keywords:
- get text from epub
- convert epub to text
- how to read epub
language: ru
og_description: Получите текст из EPUB с помощью Python за несколько минут. Этот учебник
  показывает, как читать файлы EPUB, конвертировать EPUB в текст и обрабатывать типичные
  граничные случаи.
og_title: Получить текст из EPUB в Python – Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-06-04'
  description: Get text from EPUB quickly and learn how to read EPUB files, convert
    EPUB to text, and extract chapters using Python.
  headline: Get Text from EPUB in Python – Complete Guide
  type: TechArticle
- description: Get text from EPUB quickly and learn how to read EPUB files, convert
    EPUB to text, and extract chapters using Python.
  name: Get Text from EPUB in Python – Complete Guide
  steps:
  - name: Import Libraries and Load the EPUB
    text: '```python from pathlib import Path from ebooklib import epub from bs4 import
      BeautifulSoup'
  - name: Grab the First Chapter (First <section> Element)
    text: '```python # Find the first HTML document inside the EPUB first_item = None
      for item in book.get_items(): if item.get_type() == epub.ITEM_DOCUMENT: first_item
      = item break'
  - name: Strip Tags and Output Plain Text
    text: '```python # .get_text() removes all HTML tags and returns clean text chapter_text
      = first_chapter.get_text(separator="

      ", strip=True)'
  - name: Full Script – Ready to Run
    text: '```python #!/usr/bin/env python3 """ Get text from EPUB – extract the first
      chapter and print it as plain text. """'
  type: HowTo
- questions:
  - answer: Not directly. `.mobi` uses a different container format. Convert it to
      EPUB first (Calibre does a solid job), then apply the same script.
    question: Can I use this with a .mobi file?
  - answer: The fallback to `<body>` (shown in the code) covers that case. You can
      also look for `<div class="chapter">` if the publisher uses custom markup.
    question: What if the EPUB has no `<section>` tags?
  - answer: 'No. Alternatives include `zipfile` + manual HTML parsing, or `pypub`
      for a higher‑level API. `ebooklib` is popular because it abstracts the ZIP handling
      and gives you item types out of the box. --- ## Conclusion You now know how
      to **get text from EPUB** files using Python, whether you need just the'
    question: Is `ebooklib` the only library?
  type: FAQPage
tags:
- python
- epub
- text‑extraction
title: Получить текст из EPUB в Python – Полное руководство
url: /ru/python/general/get-text-from-epub-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Получить текст из EPUB в Python – Полное руководство

Когда‑нибудь задумывались **как читать файлы EPUB** без громоздкого читалки? Может, вам нужно вытащить первую главу для анализа, или просто **конвертировать EPUB в текст** для быстрого поиска. Как бы то ни было, вы попали по адресу. В этом руководстве мы покажем, как **получить текст из EPUB** с помощью нескольких строк кода на Python, а также объясним, зачем нужен каждый шаг, чтобы вы могли адаптировать решение под любую книгу.

Мы пройдем процесс установки нужной библиотеки, загрузки EPUB, извлечения первого элемента `<section>` и вывода его чистого текста. К концу вы получите переиспользуемый скрипт, который работает с любым EPUB, помещённым в папку.

## Требования

- Python 3.8+ (код использует f‑строки и pathlib)
- Современная IDE или просто терминал
- Пакеты `ebooklib` и `beautifulsoup4` (устанавливаются командой `pip install ebooklib beautifulsoup4`)

Никаких дополнительных внешних инструментов не требуется, скрипт работает в Windows, macOS и Linux.

---

## Получить текст из EPUB – Пошагово

Ниже представлена основная логика, которая делает ровно то, что обещает заголовок: **получает текст из EPUB** и выводит первую главу. Мы разберём её, чтобы вы поняли каждую строку.

### Шаг 1: Импорт библиотек и загрузка EPUB

```python
from pathlib import Path
from ebooklib import epub
from bs4 import BeautifulSoup

# Path to the .epub file – change this to your own location
EPUB_PATH = Path("YOUR_DIRECTORY/book.epub")

# Load the EPUB container
book = epub.read_epub(EPUB_PATH)
```

*Зачем этот шаг?*  
`ebooklib` знает ZIP‑структуру файлов EPUB, а `BeautifulSoup` упрощает разбор встроенного HTML. Использование `Path` делает код независимым от ОС.

### Шаг 2: Получить первую главу (первый элемент <section>)

```python
# Find the first HTML document inside the EPUB
first_item = None
for item in book.get_items():
    if item.get_type() == epub.ITEM_DOCUMENT:
        first_item = item
        break

if not first_item:
    raise ValueError("No HTML content found in the EPUB.")

# Parse the HTML with BeautifulSoup
soup = BeautifulSoup(first_item.get_content(), "html.parser")

# Retrieve the first <section> element – this usually holds a chapter
first_chapter = soup.find("section")
if not first_chapter:
    # Fallback: use the first <body> if no <section> exists
    first_chapter = soup.body
```

*Зачем этот шаг?*  
В EPUB каждая глава хранится в виде HTML‑файла. Цикл останавливается на первом документе, который часто является обложкой или введением. Нацелившись на первый `<section>`, мы сразу попадаем в первую реальную главу, но также предусмотрен запасной вариант — элемент `<body>` для книг, где секций нет.

### Шаг 3: Удалить теги и вывести чистый текст

```python
# .get_text() removes all HTML tags and returns clean text
chapter_text = first_chapter.get_text(separator="\n", strip=True)

print(chapter_text)
```

*Зачем этот шаг?*  
`get_text()` — самый простой способ **конвертировать EPUB в текст**. Параметр `separator` гарантирует, что каждый блочный элемент начинается с новой строки, делая вывод читабельным.

### Полный скрипт – готов к запуску

```python
#!/usr/bin/env python3
"""
Get text from EPUB – extract the first chapter and print it as plain text.
"""

from pathlib import Path
from ebooklib import epub
from bs4 import BeautifulSoup

def extract_first_chapter(epub_path: Path) -> str:
    """Return the plain‑text of the first chapter in an EPUB file."""
    book = epub.read_epub(epub_path)

    # Locate the first HTML document
    first_item = next(
        (i for i in book.get_items() if i.get_type() == epub.ITEM_DOCUMENT),
        None,
    )
    if not first_item:
        raise ValueError("The EPUB does not contain any HTML documents.")

    soup = BeautifulSoup(first_item.get_content(), "html.parser")

    # Try to find a <section>; otherwise fall back to <body>
    chapter_tag = soup.find("section") or soup.body
    if not chapter_tag:
        raise ValueError("No readable content found in the first HTML document.")

    # Clean the text
    return chapter_tag.get_text(separator="\n", strip=True)


if __name__ == "__main__":
    # Replace with the actual path to your EPUB file
    EPUB_PATH = Path("YOUR_DIRECTORY/book.epub")
    try:
        text = extract_first_chapter(EPUB_PATH)
        print(text)
    except Exception as e:
        print(f"Error: {e}")
```

Сохраните файл как `extract_epub.py` и запустите `python extract_epub.py`. Если всё настроено правильно, вы увидите текст первой главы в консоли.

![Скриншот вывода терминала, показывающий извлечённый текст EPUB](get-text-from-epub.png "Пример вывода получения текста из EPUB")

---

## Конвертировать EPUB в текст – Масштабирование

Приведённый выше фрагмент работает с одной главой, но большинство проектов требуют весь текст книги в одной большой строке. Ниже показано быстрое расширение, которое проходит по **всем** элементам документа, объединяет их очищенный текст и записывает в файл `.txt`.

```python
def convert_epub_to_text(epub_path: Path, output_path: Path) -> None:
    """Convert an entire EPUB into a plain‑text file."""
    book = epub.read_epub(epub_path)
    all_text = []

    for item in book.get_items():
        if item.get_type() == epub.ITEM_DOCUMENT:
            soup = BeautifulSoup(item.get_content(), "html.parser")
            # Grab everything inside <body> – safe for most EPUBs
            body = soup.body
            if body:
                all_text.append(body.get_text(separator="\n", strip=True))

    output_path.write_text("\n\n".join(all_text), encoding="utf-8")
    print(f"✅ EPUB converted – saved to {output_path}")

# Example usage
if __name__ == "__main__":
    EPUB_PATH = Path("YOUR_DIRECTORY/book.epub")
    TXT_PATH = Path("YOUR_DIRECTORY/book.txt")
    convert_epub_to_text(EPUB_PATH, TXT_PATH)
```

**Совет:** Некоторые EPUB содержат скрипты или стили, которые могут сбивать `BeautifulSoup`. Если появляются лишние символы, используйте `soup = BeautifulSoup(item.get_content(), "lxml")` и установите `lxml` для более строгого парсера.

---

## Как эффективно читать файлы EPUB – Распространённые подводные камни

1. **Неожиданные кодировки** – EPUB — это ZIP‑файлы с HTML в UTF‑8. Если получаете `UnicodeDecodeError`, принудительно задайте UTF‑8 при чтении: `item.get_content().decode("utf-8", errors="ignore")`.
2. **Несколько языков** – Книги с миксом языков могут иметь отдельные теги `<section>` для каждого языка. Используйте `soup.find_all("section")` и фильтруйте по атрибуту `lang`, если нужно.
3. **Изображения и сноски** – Скрипт удаляет теги, поэтому alt‑текст изображений исчезает. Если они нужны, извлеките атрибуты `alt` у `<img>` или ссылки сносков `<a>` до очистки.
4. **Большие книги** – Сохранение каждой главы в памяти может перегрузить RAM. Записывайте каждую очищенную главу сразу в файл в режиме добавления, чтобы экономить память.

---

## FAQ – Краткие ответы на типичные вопросы

**В: Можно ли использовать это с файлом .mobi?**  
О: Не напрямую. `.mobi` использует иной контейнерный формат. Сначала конвертируйте его в EPUB (Calibre делает это хорошо), затем применяйте тот же скрипт.

**В: Что делать, если в EPUB нет тегов `<section>`?**  
О: Запасной вариант с `<body>` (показан в коде) покрывает такой случай. Можно также искать `<div class="chapter">`, если издатель использует собственную разметку.

**В: Является ли `ebooklib` единственной библиотекой?**  
О: Нет. Альтернативы включают `zipfile` + ручной разбор HTML или `pypub` для более высокого уровня API. `ebooklib` популярен, потому что абстрагирует работу с ZIP и сразу предоставляет типы элементов.

---

## Заключение

Теперь вы знаете, как **получить текст из EPUB** файлов с помощью Python, будь то только первая глава или вся книга. Руководство охватило основные шаги **конвертации EPUB в текст**, объяснило логику каждого кода и указало на возможные нюансы.  

Дальше попробуйте расширить скрипт, чтобы извлекать метаданные (название, автора) через `book.get_metadata('DC', 'title')`, или экспериментировать с форматами вывода, например Markdown или JSON. Принципы остаются теми же, так что вы сможете справиться с любой похожей задачей парсинга файлов.

Удачной разработки, и оставляйте комментарии, если столкнётесь с трудностями!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом гайде. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to Convert EPUB to PDF with Java – Using Aspose.HTML](/html/english/java/converting-epub-to-pdf/convert-epub-to-pdf/)
- [Convert EPUB to Images Using Aspose HTML for Java](/html/english/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)
- [Convert EPUB to PDF and Images with Aspose.HTML for Java](/html/english/java/conversion-epub-to-image-and-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
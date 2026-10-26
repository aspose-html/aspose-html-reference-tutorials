---
category: general
date: 2026-06-07
description: Как добавить префикс к заголовкам HTML с помощью Python. Узнайте, как
  выбрать несколько заголовков, изменить названия HTML и эффективно сохранить изменённый
  HTML.
draft: false
keywords:
- how to add prefix
- select multiple headings
- save modified html
- change html titles
- modify html with python
language: ru
og_description: Как добавить префикс к заголовкам HTML с помощью Python. В этом руководстве
  показано, как выбрать несколько заголовков, изменить названия HTML и сохранить изменённый
  HTML всего за несколько строк.
og_title: Как добавить префикс к заголовкам HTML с помощью Python – Быстрое руководство
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
title: Как добавить префикс к заголовкам HTML с помощью Python – пошаговое руководство
url: /ru/python/general/how-to-add-prefix-to-html-headings-with-python-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как добавить префикс к заголовкам HTML с помощью Python – Полный учебник

Как добавить префикс к заголовкам HTML с помощью Python — это распространённая потребность, когда вы поддерживаете сайт, который часто обновляется. В этом руководстве мы пройдёмся по выбору нескольких заголовков, изменению HTML‑заголовков и сохранению изменённого HTML — всё без выхода из редактора.  

Если вы когда‑нибудь задумывались, можно ли автоматизировать бейдж «отмечено как обновлённое» на десятках страниц, вы попали по адресу. Мы также коснёмся того, как **modify html with python** масштабируемо, чтобы вам не пришлось открывать каждый файл вручную.

## Что вы получите

* **Select multiple headings** (`h1`, `h2`, `h3`) в один проход.  
* **Add a custom prefix** (например, `[Updated]`) к тексту каждого заголовка.  
* **Save modified html** обратно на диск, сохраняя исходную структуру файлов.  
* Поймите компромиссы между различными парсерами HTML для Python и выберите тот, который подходит вашему проекту.

Никаких внешних сервисов, никаких тяжёлых фреймворков — только чистый Python и пара хорошо поддерживаемых библиотек.

---

## Как добавить префикс к тексту заголовка в Python

Ниже представлен минимальный, исполняемый пример, демонстрирующий основную идею. Он использует библиотеку **`lxml`** вместе с **`cssselect`** для поддержки селекторов, что отражает метод `query_selector_all`, который вы видели в оригинальном фрагменте.

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

**Expected output** (отрывок из `article_updated.html`):

```html
<h1>[Updated] Introduction to Machine Learning</h1>
<h2>[Updated] Data Pre‑processing Steps</h2>
<h3>[Updated] Feature Engineering Techniques</h3>
```

Обратите внимание, как каждый заголовок теперь начинается с тега `[Updated]` — именно то, что мы хотели, когда задавали вопрос **how to add prefix** к нашим заголовкам.

### Почему этот подход работает

* **`lxml` + `cssselect`** дает вам полную мощность CSS‑селекторов, делая шаг «select multiple headings» однострочным.  
* Метод `text_content()` безопасно извлекает внутренний текст, избегая HTML‑сущностей или дочерних тегов.  
* Запись с `pretty_print=True` сохраняет файл читаемым для человека, что удобно для diff‑ов в системе контроля версий.

---

## Выбор нескольких заголовков с помощью CSS‑селекторов

Если вы пришли из JavaScript‑фонда, синтаксис `cssselect` будет вам знаком. Селектор `"h1, h2, h3"` — это **comma‑separated list**, означающая «выбрать любой элемент, соответствующий *любому* из этих трёх».  

Вы также можете расширить область:

```python
# Grab every heading from h1 through h6
all_headings = doc.cssselect("h1, h2, h3, h4, h5, h6")
```

Или сузить её до конкретного раздела:

```python
# Only headings inside the <article> tag
article_headings = doc.cssselect("article h1, article h2, article h3")
```

Эти небольшие правки позволяют вам **select multiple headings** с лазерной точностью, что особенно полезно, когда у вас огромный сайт документации и нужно обновить только подпункт.

---

## Безопасное сохранение изменённых HTML‑файлов

Когда вы **save modified html**, вы хотите избежать порчи оригинального файла. Показанный выше шаблон записывает в новый файл (`article_updated.html`). Таким образом вы можете:

1. Проверить изменения в инструменте diff.  
2. Мгновенно откатить, если что‑то выглядит неверно.  
3. Сохранить оригинал нетронутым для целей аудита.

Если вы предпочитаете редактировать «на месте», просто поменяйте пути:

```python
import shutil
shutil.move(output_path, input_path)  # Overwrites the original
```

Но помните: **always back up** перед перезаписью, особенно на продакшн‑серверах.

---

## Изменение HTML‑заголовков vs. Заголовков страницы

Возможно, вы задаётесь вопросом, одинаково ли «changing HTML titles» и добавление префикса к заголовкам. В терминологии HTML тег `<title>` находится внутри `<head>` и управляет заголовком вкладки браузера, тогда как заголовки (`<h1>…<h3>`) отображаются в теле страницы.

Если вам также нужно **change html titles**, тот же рабочий процесс `lxml` подходит:

```python
# Change the <title> tag
title_elem = doc.find(".//title")
if title_elem is not None:
    title_elem.text = f"{prefix}{title_elem.text}"
```

Теперь и заголовок страницы, и видимые заголовки несут одинаковый флаг `[Updated]` — идеально для SEO‑аудитов, где требуется согласованность между метаданными и контентом на странице.

---

## Альтернативные библиотеки для modify html with python

Хотя `lxml` быстрый и функционально богатый, вы, возможно, уже используете **BeautifulSoup** (bs4) в своём проекте. Вот тот же логика в более «pythonic» стиле:

```python
from bs4 import BeautifulSoup

with open(input_path, "r", encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")

for tag in soup.select("h1, h2, h3"):
    tag.string = f"{prefix}{tag.get_text(strip=True)}"

with open(output_path, "w", encoding="utf-8") as f:
    f.write(str(soup.prettify()))
```

Обе библиотеки позволяют вам **modify html with python**, поэтому выбирайте ту, которая соответствует вашему текущему стеку. `BeautifulSoup` shines, когда нужен прощающий парсинг некорректной разметки, тогда как `lxml` предлагает превосходную скорость для больших пакетов.

---

## Pro Tips & Common Pitfalls

* **Encoding matters** – всегда открывайте файлы с `encoding="utf-8"`, чтобы избежать ошибок Unicode при работе с не‑ASCII символами.  
* **Avoid double‑prefixing** – если запустить скрипт дважды, вы получите `[Updated] [Updated] …`. Защищайтесь, проверяя `heading.text.startswith(prefix)`.  
* **Preserve whitespace** – вызов `strip()` удаляет лишние пробелы, делая вывод аккуратным.  
* **Batch processing** – оберните весь процесс в цикл `for file in pathlib.Path("YOUR_DIRECTORY").glob("*.html"):` чтобы обновить всю папку одной командой.  

---

## Полный рабочий пример: пакетное обновление каталога

Ниже представлен компактный скрипт, который перебирает каждый файл `.html` в каталоге, добавляет префикс к заголовкам, обновляет `<title>` и записывает новый файл с добавлением `_updated`.

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

Запустите его один раз, и каждый HTML‑файл в `YOUR_DIRECTORY` получит свежий бейдж `[Updated]` — без ручного редактирования.

---

## Заключение

Мы рассмотрели **how to add prefix** к заголовкам HTML с помощью Python, продемонстрировали, как **select multiple headings**, показали, как **save modified html** безопасно, и даже коснулись **change html titles** для полного обновления. Используя либо `lxml`, либо `BeautifulSoup`, у вас теперь есть надёжный набор инструментов для **modify html with python** в реальных проектах.

Следующие шаги? Попробуйте вместо статического тега добавлять временные метки, или сгенерировать файл changelog, в котором перечислены все изменённые файлы. Вы также можете подключить этот скрипт к CI‑конвейеру, чтобы каждый деплой происходил автоматически.

## Что вам стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как редактировать HTML с помощью Aspose.HTML для Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Как добавить CSS – Inline CSS в HTML‑документы с Aspose.HTML для Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [Как выполнять запросы к HTML в Java – Полный учебник](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
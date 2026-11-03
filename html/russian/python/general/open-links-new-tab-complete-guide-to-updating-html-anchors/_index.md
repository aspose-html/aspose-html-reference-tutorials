---
category: general
date: 2026-07-05
description: Открывайте ссылки в новой вкладке с помощью Python — узнайте, как добавить
  target="_blank", изменить цель ссылки, использовать селектор с атрибутом contains
  и легко сохранять изменённый HTML.
draft: false
keywords:
- open links new tab
- add target blank
- change link target
- attribute contains selector
- save modified html
language: ru
og_description: Быстро открывайте ссылки в новой вкладке. Этот урок показывает, как
  добавить target="_blank", изменить цель ссылки и сохранить изменённый HTML с помощью
  Python.
og_title: Открывать ссылки в новой вкладке – пошаговое руководство по обновлению HTML
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
title: Открывать ссылки в новой вкладке — Полное руководство по обновлению HTML‑якорей
url: /ru/python/general/open-links-new-tab-complete-guide-to-updating-html-anchors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Открытие ссылок в новой вкладке – Полное руководство по обновлению HTML‑якорей

Когда‑нибудь вам нужно было **open links new tab** на статической HTML‑странице, но вы не знали, с чего начать? Вы не одиноки. Многие разработчики сталкиваются с этой проблемой при очистке устаревших сайтов или добавлении улучшений доступности. В этом руководстве мы пройдем практическое решение, которое **adds target blank**, **changes link target**, и безопасно **saves modified html** — всё с помощью нескольких строк Python.

Мы также расскажем, как использовать **attribute contains selector**, чтобы изменять только те якоря, которые действительно важны (например, каждую ссылку, указывающую на *example.com*). К концу вы получите переиспользуемый скрипт, который можно добавить в любой проект, независимо от его размера.

## Что вы узнаете

- Загрузить HTML‑файл в объект документа, с которым можно работать.  
- Выбрать элементы `<a>`, у которых атрибут `href` содержит определённую подстроку.  
- **Add target blank** и установить атрибут `rel="noopener"` для повышения безопасности.  
- **Save modified html** обратно на диск без потери форматирования.  

Никаких внешних зависимостей, кроме стандартной библиотеки и **beautifulsoup4** (микро‑установка). Если вы уже используете другой парсер, концепции применимы напрямую.

---

## Требования

- Python 3.8+ установлен на вашем компьютере.  
- Базовое знакомство с HTML и Python.  
- `beautifulsoup4` пакет (`pip install beautifulsoup4`).  

Вот и всё — никаких тяжёлых фреймворков не требуется.

---

## Шаг 1: Загрузка HTML‑документа

Сначала нам нужно прочитать исходный файл и передать его BeautifulSoup. Представьте это как открытие чистого холста, на котором можно добавить новые атрибуты.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Path to the original HTML file
html_path = Path("YOUR_DIRECTORY/links.html")

# Read the file content
with html_path.open(encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")
```

> **Почему это важно:** Использование `Path` делает код независимым от ОС, а `html.parser` встроен, поэтому для простых задач не нужны дополнительные парсеры.

---

## Шаг 2: Использование селектора с содержанием атрибута для поиска нужных ссылок

Мы хотим изменять только те якоря, которые указывают на *example.com*. CSS‑селектор `a[href*='example.com']` делает именно это — `*=` означает «содержит». Метод `select` в BeautifulSoup понимает такой синтаксис.

```python
# Find all <a> tags whose href contains 'example.com'
selector = "a[href*='example.com']"
anchor_elements = soup.select(selector)
```

> **Совет:** Если требуется регистронезависимое совпадение, используйте небольшой цикл, проверяющий `if 'example.com' in a.get('href', '').lower()`.

Теперь `anchor_elements` содержит все ссылки, которые нам нужны, готовые к следующему преобразованию.

---

## Шаг 3: Изменение цели ссылки — добавление target blank и защита ссылки

Открытие ссылки в новой вкладке так же просто, как установить `target="_blank"`. Однако современные браузеры рекомендуют также добавить `rel="noopener"` (или `noreferrer`), чтобы предотвратить доступ открытой страницы к оригинальному окну через `window.opener`. Эта небольшая настройка безопасности может остановить фишинговые атаки.

```python
for anchor in anchor_elements:
    # Open in a new tab
    anchor['target'] = "_blank"          # add target blank
    # Harden security
    anchor['rel'] = "noopener"           # prevent access to the opener page
```

> **Почему мы используем прямое присваивание словарю:** Это автоматически создаёт атрибут, если его нет, и перезаписывает его, если он уже существует — идеально для операции **change link target**.

---

## Шаг 4: Сохранение изменённого HTML на диск

Последний шаг — записать обновлённую разметку в новый файл. Сохранение оригинала нетронутым позволяет откатиться, если что‑то пойдёт не так.

```python
# Destination path for the updated HTML
output_path = Path("YOUR_DIRECTORY/links-updated.html")

# Write the prettified HTML (preserves indentation)
with output_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())
```

> **Что делает `prettify()`:** Он форматирует HTML с хорошим отступом, делая сохранённый файл легче читаемым и сравниваемым позже. Если вы предпочитаете оригинальные пробелы, замените `prettify()` на `str(soup)`.

---

## Полный скрипт — решение в один клик

Ниже представлен полный, готовый к запуску скрипт. Сохраните его как `update_links.py` и выполните `python update_links.py` из терминала.

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

### Ожидаемый результат

Предположим, что `links.html` изначально содержал:

```html
<a href="https://example.com/page1">Page 1</a>
<a href="https://other.com/home">Home</a>
```

После выполнения скрипта `links-updated.html` будет выглядеть так:

```html
<a href="https://example.com/page1" target="_blank" rel="noopener">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Только ссылка на *example.com* получила атрибуты **add target blank**, что демонстрирует, что наш **attribute contains selector** сработал точно как задумано.

---

## Часто задаваемые вопросы и крайние случаи

### Что если у ссылки уже есть атрибут `rel`?

Наш цикл перезаписывает его значением `"noopener"`. Если нужно сохранить существующие значения (например, `"nofollow"`), объедините их вместо этого:

```python
existing = a.get('rel', '')
a['rel'] = f"{existing} noopener".strip()
```

### Как обрабатывать несколько доменов?

Просто расширьте список селекторов:

```python
domains = ["example.com", "sample.org"]
selector = ",".join([f"a[href*='{d}']" for d in domains])
anchors = soup.select(selector)
```

### Меняет ли `prettify()` оригинальную структуру HTML?

Он переотступает, но не меняет порядок тегов или значения атрибутов. Если необходимо сохранить точные оригинальные пробелы, замените `prettify()` на `str(soup)`, как упоминалось ранее.

---

## Профессиональные советы для скриптов, готовых к продакшену

- **Backup before overwriting:** Добавьте шаг копирования (`shutil.copy`), чтобы сохранить оригинальный файл в безопасности.  
- **Logging instead of print:** Используйте модуль `logging` для масштабируемых проектов.  
- **Batch processing:** Пройдитесь по директории с помощью `Path.rglob("*.html")`, чтобы обновить множество файлов за один запуск.  

Эти доработки превращают простой скрипт **open links new tab** в надёжный инструмент для любого процесса поддержки веб‑сайтов.

---

## Заключение

Теперь у вас есть надёжный, переиспользуемый метод для **open links new tab** в любой статической HTML‑коллекции. Используя **attribute contains selector**, вы можете **change link target** точно там, где это нужно, **add target blank** и **save modified html** без потери форматирования.

Попробуйте его на тестовой странице, а затем масштабируйте на весь сайт. Нужно изменить селектор для PDF‑файлов или других доменов? Просто скорректируйте строку CSS — всё остальное остаётся прежним.

Не стесняйтесь оставить комментарий, если столкнётесь с особенностями, или поделиться тем, как вы расширили скрипт для своих проектов. Приятного кодинга, и пусть все ваши якоря открываются именно там, где вы хотите!

---

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и изучить альтернативные подходы к реализации в своих проектах.

- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
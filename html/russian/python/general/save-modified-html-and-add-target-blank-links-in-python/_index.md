---
category: general
date: 2026-11-24
description: Сохраните изменённый HTML и добавьте ссылки с target="_blank" в Python
  с помощью Aspose.HTML. Узнайте, как изменить target href для всех тегов <a> и открыть
  все ссылки в новой вкладке.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save modified html
- add target blank links
- change href target
- open all links newtab
language: ru
lastmod: 2026-11-24
og_description: Сохраните изменённый HTML и добавьте ссылки с target="_blank" в Python
  с помощью Aspose.HTML. Следуйте этому пошаговому руководству, чтобы изменить target
  у href и открыть все ссылки в новой вкладке.
og_image_alt: Screenshot of a Python script that saves modified HTML with target='_blank'
  on every link
og_title: Сохранение изменённого HTML и добавление ссылок с target=_blank в Python
  — полное руководство
schemas:
- author: Aspose
  dateModified: '2026-11-24'
  description: Save modified HTML and add target blank links in Python using Aspose.HTML.
    Learn how to change href target for all <a> tags and open all links newtab.
  headline: Save modified HTML and add target blank links in Python
  type: TechArticle
tags:
- Aspose.HTML
- Python
- HTML manipulation
- Web automation
title: Сохранить изменённый HTML и добавить ссылки с target="_blank" в Python
url: /ru/python/general/save-modified-html-and-add-target-blank-links-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Сохранение изменённого HTML и добавление target=_blank ссылок в Python

Если вам нужно **save modified HTML** после обновления каждой ссылки, это руководство покажет, как сделать это с помощью Aspose.HTML for Python. Вы узнаете, как **add target blank links**, изменить цель `href` и заставить все ссылки открываться в новой вкладке.

## Предварительные требования

Перед началом убедитесь, что у вас есть:

* Python 3.8 или новее установлен  
* Действующая лицензия Aspose.HTML for Python (или бесплатный оценочный ключ)  
* Локальный HTML‑файл, который нужно изменить (например, `index.html`)  

Вы можете установить библиотеку через pip:

```bash
pip install aspose-html
```

## Шаг 1: Загрузка HTML‑документа

Первый шаг — создать экземпляр `HTMLDocument`, указывающий на ваш исходный файл. Этот объект представляет всё дерево DOM, позволяя выполнять запросы и редактировать элементы.

```python
from aspose.html import HTMLDocument

# Load the original HTML file
doc = HTMLDocument("YOUR_DIRECTORY/index.html")
```

*Почему это важно*: Загрузка документа даёт программный доступ к каждому узлу, что необходимо для массовых обновлений, таких как изменение атрибута `target` у всех тегов `<a>`.

## Шаг 2: Добавление target=_blank ссылок к каждому якорю

Чтобы каждый гиперссылка открывалась в новой вкладке, задайте атрибут `target` со значением `_blank`. Метод `query_selector_all` возвращает живую коллекцию всех элементов `<a>`, независимо от глубины вложенности.

```python
# Update all <a> tags to open links in a new tab
for link in doc.query_selector_all("a"):
    link.set_attribute("target", "_blank")
```

**Ключевые моменты**

* Цикл обрабатывает каждый якорь ровно один раз, гарантируя, что **add target blank links** применяется одинаково.  
* Если у ссылки уже есть атрибут `target`, вызов перезапишет его, обеспечивая согласованное поведение.  

### Обработка существующих значений `target` (необязательно)

Если вы хотите сохранить уже заданные `target` и установить `_blank` только там, где атрибут отсутствует, добавьте условную проверку:

```python
for link in doc.query_selector_all("a"):
    if not link.has_attribute("target"):
        link.set_attribute("target", "_blank")
```

## Шаг 3: Изменение цели href и открытие всех ссылок в новой вкладке

Иногда требуется изменить сам атрибут `href` — например, добавить базовый URL или преобразовать относительные пути в абсолютные. Та же техника обхода DOM работает и для изменений `href`.

```python
base_url = "https://example.com/"

for link in doc.query_selector_all("a"):
    href = link.get_attribute("href")
    # Skip empty or already absolute URLs
    if href and not href.startswith("http"):
        new_href = base_url + href.lstrip("/")
        link.set_attribute("href", new_href)
    # Ensure the link opens in a new tab
    link.set_attribute("target", "_blank")
```

*Почему это важно*: Путём **changing href target** и обеспечения **open all links newtab** вы гарантируете, что пользователи попадут по правильному адресу, а навигация произойдёт без покидания текущей страницы.

## Шаг 4: Сохранение изменённого документа

После завершения всех правок вызовите `save`, чтобы записать изменения в новый файл. Здесь и происходит фактическое **save modified html**.

```python
# Save the updated HTML to a new file
doc.save("YOUR_DIRECTORY/index_modified.html")
```

Полученный файл `index_modified.html` содержит каждый тег `<a>` с `target="_blank"` и обновлёнными значениями `href`. Откройте его в браузере, чтобы убедиться, что при клике ссылка открывается в новой вкладке.

## Шаг 5: Проверка результата (необязательно)

Быстрая проверка поможет убедиться, что операция прошла успешно:

```python
# Reload the saved file to verify changes
verify_doc = HTMLDocument("YOUR_DIRECTORY/index_modified.html")
for link in verify_doc.query_selector_all("a"):
    assert link.get_attribute("target") == "_blank", "Target attribute not set correctly"
print("All links have target='_blank' and the file was saved successfully.")
```

Если утверждение не выполнится, скрипт выбросит ошибку, указывая на проблемный элемент.

## Совет: пакетная обработка нескольких файлов

Когда у вас есть каталог с множеством HTML‑файлов, оберните логику в функцию и пройдитесь по каждому файлу:

```python
import os
from aspose.html import HTMLDocument

def process_file(input_path: str, output_path: str, base_url: str = None):
    doc = HTMLDocument(input_path)
    for link in doc.query_selector_all("a"):
        if base_url:
            href = link.get_attribute("href")
            if href and not href.startswith("http"):
                link.set_attribute("href", base_url + href.lstrip("/"))
        link.set_attribute("target", "_blank")
    doc.save(output_path)

source_dir = "YOUR_DIRECTORY"
for filename in os.listdir(source_dir):
    if filename.endswith(".html"):
        src = os.path.join(source_dir, filename)
        dst = os.path.join(source_dir, f"{os.path.splitext(filename)[0]}_modified.html")
        process_file(src, dst, base_url="https://example.com/")
```

Такой подход масштабирует workflow **save modified html** на любое количество страниц, последовательно применяя **add target blank links** и **change href target**.

## Ожидаемый результат

Открытие `index_modified.html` в браузере должно показать тот же визуальный макет, что и у оригинальной страницы, но каждая гиперссылка теперь содержит:

```html
<a href="https://example.com/about.html" target="_blank">About Us</a>
```

Клик по ссылке открывает её в новой вкладке браузера, сохраняя текущую страницу пользователя.

## Распространённые подводные камни и как их избежать

| Подводный камень | Описание | Решение |
|------------------|----------|----------|
| Отсутствует лицензия Aspose.HTML | Библиотека бросает ошибку лицензирования во время выполнения. | Получите файл лицензии и вызовите `aspose.html.License().set_license("license_path")` перед загрузкой документа. |
| Относительные URL, начинающиеся с `//` | Рассматриваются как протокольно‑относительные URL и могут остаться без изменений. | Добавьте проверку `href.startswith("//")` и при необходимости добавьте префикс `https:`. |
| Очень большие HTML‑файлы | Загрузка огромных файлов может потреблять значительное количество памяти. | Используйте потоковые API или разбейте файл на более мелкие фрагменты, если память становится узким местом. |

## Заключение

Теперь вы знаете, как **save modified HTML** после применения **add target blank links**, **change href target** и обеспечения **open all links newtab** с помощью Aspose.HTML for Python. Полное решение загружает HTML‑файл, обновляет каждый элемент `<a>` и записывает результат в новый файл, учитывая такие нюансы, как уже существующие атрибуты `target` и относительные URL.

Далее вы можете изучить:

* Использование CSS‑селекторов для выбора только внешних ссылок (`a[href^="http"]`)  
* Внедрение JavaScript, добавляющего `rel="noopener"` для безопасности при открытии новых вкладок  
* Преобразование изменённого HTML в PDF с помощью Aspose.PDF for Python  

Не стесняйтесь адаптировать код под структуру вашего проекта и экспериментировать с дополнительными манипуляциями DOM. Happy coding!

## Что вам стоит изучить дальше?

Следующие руководства охватывают смежные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to save HTML as PDF with Aspose.HTML for Python](/html/english/python/general/how-to-save-html-as-pdf-with-aspose-html-for-python/)
- [How to save HTML as Markdown with Aspose.HTML for Python](/html/english/python/general/how-to-save-html-as-markdown-with-aspose-html-for-python/)
- [How to Use Aspose – Convert HTML to Markdown and Extract Links](/html/english/python/general/how-to-use-aspose-convert-html-to-markdown-and-extract-links/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
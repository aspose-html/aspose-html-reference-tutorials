---
category: general
date: 2026-09-16
description: Разберите HTML‑файл в Python, загрузите HTML‑документ из файла и создайте
  HTML‑документ из строки с простым, готовым к запуску кодом.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- parse html file in python
- create html document from string
- load html document from file
- read local html file python
language: ru
lastmod: 2026-09-16
og_description: Разбор HTML‑файла в Python для чтения локальных HTML‑файлов и быстрого
  и надёжного создания HTML‑документов из строк.
og_image_alt: Screenshot of Python code parsing an HTML file and creating a document
  from a string
og_title: Разбор HTML‑файла в Python — создание документа из строки
schemas:
- author: Aspose
  dateModified: '2026-09-16'
  description: Parse HTML file in Python, load HTML document from file, and create
    HTML document from string with simple, ready‑to‑run code.
  headline: Parse HTML file in Python and create document from string
  type: TechArticle
- description: Parse HTML file in Python, load HTML document from file, and create
    HTML document from string with simple, ready‑to‑run code.
  name: Parse HTML file in Python and create document from string
  steps:
  - name: '**Detect source type** – The constructor checks whether the supplied `source`
      exists on disk. If it does, we **load html document from file**; otherwise we
      treat it as a raw string, satisfying the **create html document from string**
      requirement.'
    text: '**Detect source type** – The constructor checks whether the supplied `source`
      exists on disk. If it does, we **load html document from file**; otherwise we
      treat it as a raw string, satisfying the **create html document from string**
      requirement.'
  - name: '**Read the file** – We use `Path.read_text(encoding="utf-8")` which is
      the recommended way to **read local html file python** safely.'
    text: '**Read the file** – We use `Path.read_text(encoding="utf-8")` which is
      the recommended way to **read local html file python** safely.'
  - name: '**Parse with BeautifulSoup** – The `lxml` parser is fast and tolerant of
      malformed markup.'
    text: '**Parse with BeautifulSoup** – The `lxml` parser is fast and tolerant of
      malformed markup.'
  type: HowTo
tags:
- python html parsing
- html document creation
- file handling python
title: Разбор HTML‑файла в Python и создание документа из строки
url: /ru/python/general/parse-html-file-in-python-and-create-document-from-string/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Разбор HTML‑файла в Python и создание документа из строки

Если вам нужно **parse HTML file in Python**, это руководство показывает, как точно прочитать локальный HTML‑файл, загрузить HTML‑документ из файла и также **create HTML document from string**. Независимо от того, собираете ли вы данные, тестируете шаблоны или генерируете динамический контент, нижеуказанные шаги предоставят полное, готовое к запуску решение.

В этом уроке вы узнаете, как:

* Прочитать локальный HTML‑файл с помощью стандартных библиотек Python.
* Загрузить HTML‑документ из пути к файлу.
* Создать HTML‑документ напрямую из HTML‑строки.
* Обрабатывать типичные пограничные случаи, такие как отсутствие файлов и проблемы с кодировкой.

Единственными предварительными требованиями являются Python 3.8+ и библиотека `beautifulsoup4`, которую мы установим в первом шаге.

## Требования

| Требование | Почему это важно |
|-------------|----------------|
| Python 3.8 или новее | Гарантирует совместимость с типовыми подсказками и современным синтаксисом. |
| Пакеты `beautifulsoup4` и `lxml` | Обеспечивают надёжный парсер, способный работать с некорректным HTML и предоставляющий удобный объект, похожий на `HTMLDocument`. |
| Пример HTML‑файла (`index.html`) в папке проекта | Служит входными данными для примера **load html document from file**. |

Установите зависимости с помощью pip:

```bash
pip install beautifulsoup4 lxml
```

## Разбор HTML‑файла в Python

Основой урока является операция **parse html file in python**. Мы обернём BeautifulSoup в небольшую вспомогательную класс‑обёртку `HTMLDocument`, чтобы API соответствовал показанному ранее примеру.

```python
from pathlib import Path
from bs4 import BeautifulSoup
from typing import Union

class HTMLDocument:
    """
    Simple wrapper that mimics a “document” object.
    Accepts either a file path or a raw HTML string.
    """
    def __init__(self, source: Union[str, Path]):
        if Path(source).exists():
            # Load html document from file
            self._load_from_file(Path(source))
        else:
            # Assume source is a raw HTML string
            self._load_from_string(source)

    def _load_from_file(self, file_path: Path):
        try:
            # read local html file python – explicit UTF‑8 handling
            html = file_path.read_text(encoding="utf-8")
        except FileNotFoundError:
            raise FileNotFoundError(f"File not found: {file_path}")
        self.soup = BeautifulSoup(html, "lxml")

    def _load_from_string(self, html_string: str):
        self.soup = BeautifulSoup(html_string, "lxml")

    def title(self) -> str:
        """Return the content of the <title> tag, or an empty string."""
        if self.soup.title:
            return self.soup.title.string.strip()
        return ""

    def pretty(self) -> str:
        """Return a nicely formatted HTML representation."""
        return self.soup.prettify()
```

### Как это работает

1. **Определение типа источника** – Конструктор проверяет, существует ли указанный `source` на диске. Если существует, мы **load html document from file**; иначе рассматриваем его как обычную строку, удовлетворяя требованию **create html document from string**.
2. **Чтение файла** – Мы используем `Path.read_text(encoding="utf-8")`, что является рекомендованным способом **read local html file python** безопасно.
3. **Парсинг с BeautifulSoup** – Парсер `lxml` быстрый и tolerant к некорректной разметке.

## Загрузка HTML‑документа из файла

Теперь, когда у нас есть класс `HTMLDocument`, загрузка файла становится простой:

```python
# Step 1: Load an HTML document from a local file
doc = HTMLDocument("YOUR_DIRECTORY/index.html")

# Verify that the file was parsed correctly
print("Document title:", doc.title())
```

**Ожидаемый вывод** (при условии, что `index.html` содержит `<title>My Page</title>`):

```
Document title: My Page
```

Если файл не существует, класс бросает понятный `FileNotFoundError`, который вы можете перехватить в продакшн‑коде.

## Создание HTML‑документа из строки

Создание документа напрямую из строки полезно для тестирования или генерации HTML «на лету»:

```python
# Step 2: Create an HTML document directly from an HTML string
html_content = "<html><head><title>Hello</title></head><body><h1>Hello</h1></body></html>"
doc_from_string = HTMLDocument(html_content)

print("String‑based title:", doc_from_string.title())
```

**Ожидаемый вывод**:

```
String-based title: Hello
```

Поскольку один и тот же класс `HTMLDocument` обрабатывает оба сценария, вы получаете единый API для **parse html file in python**, независимо от того, является ли источник файлом или строкой.

## Чтение локального HTML‑файла в Python – обработка пограничных случаев

Работая с реальными файлами, вы часто сталкиваетесь с:

* **Отсутствием файлов** – уже покрыто `FileNotFoundError`.
* **Различными кодировками** – вы можете позволить BeautifulSoup угадывать кодировку, но явный UTF‑8 самый надёжный.
* **Большими файлами** – чтение всего файла в память может быть дорогостоящим; при необходимости можно использовать потоковый режим `BeautifulSoup(open(...), "lxml")`.

Вот защитная обёртка, добавляющая эти меры предосторожности:

```python
def safe_load_html(path: Union[str, Path]) -> HTMLDocument:
    """
    Load an HTML file safely, handling missing files and encoding issues.
    Returns an HTMLDocument instance or raises a descriptive exception.
    """
    try:
        return HTMLDocument(path)
    except FileNotFoundError as e:
        raise RuntimeError(f"Unable to read local HTML file Python: {e}")
    except UnicodeDecodeError:
        raise RuntimeError("File encoding is not UTF-8; consider specifying the correct encoding.")
```

Теперь вы можете вызвать `safe_load_html("index.html")` и получить тот же объект `HTMLDocument` с уверенностью, что ошибки будут сообщены ясно.

## Полезные советы и распространённые подводные камни

* **Избегайте простого `open(...).read()`** – `Path.read_text` обрабатывает расширение пути и кодировку в одной строке.
* **Не забывайте закрывать файловые дескрипторы** – `Path.read_text` делает это автоматически; если вы используете `open()`, оберните его в блок `with`.
* **Предпочитайте `lxml` вместо парсера по умолчанию** – он быстрее и более tolerant к сломанной разметке, что критично при **parse html file in python** из веба.
* **При создании из строки убедитесь, что это полноценный HTML‑документ** – отсутствие тегов `<html>` или `<body>` может привести к неожиданным `None`‑результатам при запросе элементов.

## Полный скрипт, который можно скопировать и вставить

Ниже представлен автономный скрипт, демонстрирующий каждый обсуждённый шаг. Сохраните его как `html_demo.py` и запустите `python html_demo.py`.



## Что следует изучить дальше?

Следующие уроки охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Save HTML Document to File in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-to-file/)
- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Create HTML Document with Aspose.HTML – Step‑by‑Step Guide](/html/english/net/html-document-manipulation/create-html-document-with-aspose-html-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
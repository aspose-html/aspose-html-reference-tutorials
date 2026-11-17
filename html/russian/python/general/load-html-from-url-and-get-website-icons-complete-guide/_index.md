---
category: general
date: 2026-06-10
description: Загружайте HTML по URL, чтобы быстро получать иконки сайта. Узнайте,
  как извлекать фавиконы, получать URL фавиконов сайта и обрабатывать особые случаи
  в Python.
draft: false
keywords:
- load html from url
- get website icons
- how to extract favicons
- extract favicon urls
- fetch website favicon urls
language: ru
og_description: Загружайте HTML по URL, извлекайте фавиконы и получайте URL фавиконов
  сайта. Пошаговый учебник по Python для разработчиков.
og_title: Загрузка HTML по URL и получение иконок сайта – полное руководство
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
title: Загрузка HTML по URL и получение иконок сайта – Полное руководство
url: /ru/python/general/load-html-from-url-and-get-website-icons-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Загрузка HTML из URL и получение иконок сайта – Полное руководство

Когда‑нибудь вам нужно было **load HTML from URL**, чтобы получить крошечный логотип сайта? Вы не одиноки. Независимо от того, создаёте ли вы менеджер закладок, SEO‑панель или просто личный проект‑хобби, получение иконок сайта — небольшая, но важная часть задачи.

В этом руководстве мы покажем, как **извлекать фавиконы** с помощью чистого Python — без тяжёлого Selenium и без магии браузера. К концу вы сможете **получать URL фавиконов сайта**, обрабатывать относительные пути и даже получать несколько иконок, если сайт их предоставляет. Готовы? Поехали.

## Почему загружать HTML из URL?

Загрузка сырого HTML страницы даёт прямой доступ к тегам `<link>`, которые браузеры используют для поиска фавиконов. Обычно такие теги выглядят так:

```html
<link rel="icon" href="/favicon.ico">
<link rel="apple-touch-icon" href="https://example.com/apple-touch-icon.png">
```

Если вы сможете получить эту разметку, вы сможете программно прочитать атрибут `href` и загрузить изображение самостоятельно. Это быстрее, чем скрейпить скриншоты, и работает для любого сайта, следующего стандартным конвенциям.

## Шаг 1 – Загрузка HTML‑документа из URL

Первое, что нам нужно, — способ получить исходный код страницы. Самый популярный вариант в Python — библиотека **requests**, потому что она простая, надёжная и сразу обрабатывает перенаправления.

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

> **Pro tip:** Если вы работаете за корпоративным прокси, передайте `proxies=` в `requests.get`. Также установка небольшого таймаута предотвращает зависание скрипта на недоступных сайтах.

Теперь мы можем вызвать `fetch_html("https://example.com")` и получить строку, содержащую разметку страницы. Это и есть ядро **load HTML from URL** — остальная часть конвейера работает с этой строкой.

## Шаг 2 – Получение иконок сайта

Получив HTML, следующий шаг — найти каждый элемент `<link>`, у которого атрибут `rel` содержит слово «icon». Встроенный модуль `html.parser` справится, но **BeautifulSoup** делает код гораздо более читаемым.

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

Обратите внимание, как мы используем `urljoin`, чтобы превратить `"/favicon.ico"` в `"https://example.com/favicon.ico"` — это распространённый краевой случай при **get website icons**. Некоторые сайты даже отдают разные иконки для разных устройств, поэтому вы можете получить несколько URL. Проблем нет; мы просто собираем их все.

## Шаг 3 – Извлечение URL фавиконов и их вывод

Собрать всё вместе довольно просто. Мы получим HTML, запустим извлекатель и выведем полученный список. Финальный скрипт выглядит так:

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

### Ожидаемый вывод

Запуск скрипта против сайта, предоставляющего стандартный фавикон, может дать такой результат:

```
Found icon URLs: ['https://example.com/favicon.ico']
```

Если сайт предоставляет несколько иконок (Apple touch icon, shortcut icon и т.д.), вы увидите более длинный список:

```
Found icon URLs: [
    'https://example.com/favicon.ico',
    'https://example.com/apple-touch-icon.png',
    'https://example.com/favicon-32x32.png'
]
```

Это полностью рабочий процесс **extract favicon urls** — компактный, с минимумом зависимостей и готовый к использованию в любом проекте.

## Обработка распространённых подводных камней

| Проблема | Почему происходит | Быстрое решение |
|----------|-------------------|-----------------|
| **Относительный `href` без тега `<base>`** | `urljoin` использует URL страницы как базу, что работает в большинстве случаев. | Если существует тег `<base href="...">`, сначала прочитайте его и передайте в качестве `base_url`. |
| **Отсутствует `rel="icon"`** | Некоторые сайты используют `rel="shortcut icon"` или кастомные значения. | Расширьте лямбда‑функцию: `rel=lambda r: r and ("icon" in r.lower() or "shortcut" in r.lower())`. |
| **Перенаправления на другой домен** | Фавикон может находиться на CDN. | `urljoin` корректно разрешит новый домен, потому что использует окончательный URL запроса (`response.url`). |
| **Сломанные ссылки (404)** | HTML указывает на файл, который больше не существует. | После извлечения URL можно проверить каждый запросом HEAD перед использованием. |
| **Несколько тегов `<link>` с одной и той же иконкой** | Дублирующие записи увеличивают список. | Используйте `set(icon_urls)`, чтобы удалить дубликаты перед возвратом. |

## Дальше — массовое получение URL фавиконов сайта

Если вам нужно **fetch website favicon URLs** для списка доменов, оберните основную логику в цикл:

```python
domains = ["https://example.com", "https://python.org", "https://github.com"]
for site in domains:
    try:
        icons = extract_icon_links(fetch_html(site), site)
        print(site, "->", icons)
    except Exception as e:
        print(site, "error:", e)
```

Этот шаблон хорошо масштабируется, и вы можете добавить кэширование (например, с помощью `functools.lru_cache`), чтобы не нагружать один и тот же сайт повторными запросами.

## Визуальный обзор

![Load HTML from URL diagram](load-html-url.png)

*Alt text: Диаграмма Load HTML from URL, показывающая шаги fetch → parse → extract.*

Изображение выше суммирует процесс из трёх шагов: **load HTML from URL**, **get website icons** и **extract favicon URLs**. Это удобно, когда нужно объяснить поток коллегам.

## Заключение

Мы прошли полный, готовый к продакшену процесс того, как **load HTML from URL** и **get website icons** используя только библиотеки requests и BeautifulSoup. Извлекая атрибуты `href` из тегов `<link rel="icon">`, вы можете **extract favicon URLs**, обрабатывать относительные пути и даже получать несколько форматов иконок — всё в паре десятков строк кода.

Что дальше? Попробуйте скачать иконки в локальную папку, сгенерировать CSV с сопоставлением домен‑фавикон, или внедрить эту логику в Flask‑API, который будет отдавать фавиконы по запросу. Возможности для **fetch website favicon URLs** безграничны, а базовая техника остаётся той же.

Есть вопросы о крайних случаях или хотите поделиться умным трюком? Оставьте комментарий ниже — удачной охоты за иконками!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Загрузка HTML‑документов из файла в Aspose.HTML для Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Загрузка HTML‑документов из потока в Aspose.HTML для Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-stream/)
- [Обработка событий загрузки документа в Aspose.HTML для Java](/html/english/java/creating-managing-html-documents/handle-document-load-events/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
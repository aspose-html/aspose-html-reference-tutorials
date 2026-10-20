---
category: general
date: 2026-06-26
description: Узнайте, как получить favicon, загрузив HTML по URL и извлекая href из
  тегов <link>. Пошаговый код на Python для быстрого получения иконок сайта.
draft: false
keywords:
- how to get favicon
- load html from url
- get website icons
- extract href from link
- how to extract favicons
language: ru
og_description: 'Как быстро получить favicon: загрузить HTML по URL, найти link rel=''icon''
  и извлечь href из тегов link с помощью Python.'
og_title: Как получить фавикон — учебник по Python
schemas:
- author: Aspose
  dateModified: '2026-06-26'
  description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  headline: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  type: TechArticle
- description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  name: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  steps:
  - name: What if the site uses a `<meta>` tag instead of `<link>`?
    text: Some older pages embed the icon URL in a `<meta name="msapplication‑TileImage">`.
      You can extend `find_icon_links` to also search for those meta tags and treat
      them the same way.
  - name: How do I handle relative URLs that start with `//`?
    text: '`urljoin` automatically resolves protocol‑relative URLs (`//example.com/favicon.ico`)
      based on the scheme of the base URL, so you don’t need extra logic.'
  - name: Can I retrieve multiple sizes (e.g., 32×32, 180×180) automatically?
    text: Yes—just drop the `filter_ico_urls` step. The script will return every icon
      URL it discovers, including PNGs of various dimensions. You can then sort or
      select based on the filename pattern.
  - name: Does this work on sites that block bots?
    text: 'If a site returns a 403 or requires a custom User‑Agent, tweak the `requests.get`
      call:'
  type: HowTo
tags:
- Python
- Web Scraping
- HTML Parsing
title: Как получить фавикон — Полное руководство на Python по извлечению иконок сайта
url: /ru/python/general/how-to-get-favicon-complete-python-guide-for-extracting-site/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как получить favicon – Полное руководство на Python по извлечению иконок сайта

Когда‑то задавались вопросом **как получить favicon** с любого сайта, не копаясь вручную в исходном коде? Вы не одиноки — разработчики, SEO‑специалисты и даже дизайнеры часто нуждаются в этой крошечной иконке, представляющей сайт. В этом руководстве мы покажем чистый, ориентированный на Python способ загрузить HTML по URL, найти теги `<link rel="icon">` и извлечь URL‑ы иконок. К концу вы точно будете знать **как получить favicon** для любого домена и получите переиспользуемый скрипт для своих проектов.

Мы охватим всё: от получения HTML до обработки особых случаев, таких как относительные URL‑ы и несколько форматов иконок. Никаких внешних сервисов — только стандартная библиотека `requests` и лёгкий HTML‑парсер. Готовы начать? Поехали.

## Предварительные требования

- Установлен Python 3.8+ (код также работает на 3.10)  
- Базовое знакомство с `requests` и list comprehensions  
- Доступ в Интернет к целевому сайту  

Если всё уже есть — отлично, переходите к первому шагу. Иначе установите единственную зависимость, которая нам нужна:

```bash
pip install requests beautifulsoup4
```

> **Совет:** `beautifulsoup4` — проверенный парсер, который делает «загрузить html по url» простым.

## Шаг 1: Загрузка HTML по URL с помощью Python  

Первое, что нужно сделать, изучая **как получить favicon**, — получить исходный код страницы. Это часть процесса «загрузить html по url».

```python
import requests
from bs4 import BeautifulSoup

def fetch_html(url: str) -> str:
    """Download the raw HTML of *url* and return it as text."""
    response = requests.get(url, timeout=10)
    response.raise_for_status()   # will raise if the request failed
    return response.text
```

Почему `requests`? Он автоматически обрабатывает редиректы, проверку HTTPS и тайм‑ауты, что уменьшает количество сюрпризов, когда позже будете **получать иконки сайта**.

## Шаг 2: Разбор документа и поиск ссылок на иконки  

Теперь, когда у нас есть HTML, нужно найти все элементы `<link>`, у которых атрибут `rel` указывает на иконку. Это сердце **как получить favicon**.

```python
def find_icon_links(html: str) -> list[BeautifulSoup]:
    """Return a list of <link> tags that declare an icon."""
    soup = BeautifulSoup(html, "html.parser")
    # Look for rel="icon" or rel="shortcut icon"
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]
```

Обратите внимание, что проверяем как `icon`, так и `shortcut icon`, потому что старые сайты всё ещё используют второе. Эта небольшая деталь часто сбивает людей, когда они ищут «как извлечь favicon».

## Шаг 3: Извлечение href из элементов link  

Имея нужные теги, следующий логичный шаг — **извлечь href из link** — прост.

```python
from urllib.parse import urljoin

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    """Convert each <link> tag’s href into a full absolute URL."""
    urls = []
    for tag in link_tags:
        href = tag.get("href")
        if href:
            # Resolve relative URLs against the base page
            full_url = urljoin(base_url, href)
            urls.append(full_url)
    return urls
```

Использование `urljoin` гарантирует, что даже если сайт предоставляет относительный путь вроде `/favicon.ico`, вы получите корректный абсолютный URL — критически важно для надёжного скрипта **как получить favicon**.

## Шаг 4: Необязательно — проверка и фильтрация URL‑ов иконок  

Иногда страница перечисляет множество иконок (Apple touch icons, PNG разных размеров и т.д.). Если вам нужна только классическая `.ico`‑файла, отфильтруйте её. Этот шаг показывает **как извлечь favicons** определённого типа.

```python
def filter_ico_urls(urls: list[str]) -> list[str]:
    """Keep only URLs that end with .ico (case‑insensitive)."""
    return [u for u in urls if u.lower().endswith(".ico")]
```

Можно изменить фильтр: заменить `".ico"` на `".png"` или проверять `rel="apple-touch-icon"`, если нужны иконки высокого разрешения.

## Шаг 5: Скачивание файлов иконок (если нужен сам образ)

Извлечение URL‑ов — лишь половина дела; скачивание даёт файл, который можно отобразить или сохранить. Вот небольшой помощник:

```python
import os

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    """Save each icon to *folder*, creating it if necessary."""
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")
```

Запуск этого после предыдущих шагов даст локальную копию каждой найденной favicon, что удобно для кэширования или офлайн‑анализа.

## Шаг 6: Собираем всё вместе — полностью рабочий пример  

Ниже полностью готовый к запуску скрипт, демонстрирующий **как получить favicon** с любого сайта. Скопируйте, измените `target_url` и посмотрите результат.

```python
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin
import os

def fetch_html(url: str) -> str:
    response = requests.get(url, timeout=10)
    response.raise_for_status()
    return response.text

def find_icon_links(html: str) -> list[BeautifulSoup]:
    soup = BeautifulSoup(html, "html.parser")
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    return [urljoin(base_url, tag.get("href")) for tag in link_tags if tag.get("href")]

def filter_ico_urls(urls: list[str]) -> list[str]:
    return [u for u in urls if u.lower().endswith(".ico")]

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")

def get_favicons(target_url: str) -> None:
    print(f"Fetching HTML from {target_url} …")
    html = fetch_html(target_url)

    print("Finding <link> tags that declare icons …")
    icon_tags = find_icon_links(html)

    print(f"Extracting href attributes – {len(icon_tags)} candidates found.")
    raw_urls = extract_icon_urls(target_url, icon_tags)

    # Optional filtering – keep only .ico files
    ico_urls = filter_ico_urls(raw_urls)
    print(f"Filtered to {len(ico_urls)} .ico URLs:", ico_urls)

    if ico_urls:
        download_icons(ico_urls)
    else:
        print("No .ico favicons detected; here are all discovered URLs:")
        print(raw_urls)

# Example usage – replace with any site you want to test
if __name__ == "__main__":
    target_url = "https://www.python.org"
    get_favicons(target_url)
```

**Ожидаемый вывод (усечённый для краткости):**

```
Fetching HTML from https://www.python.org …
Finding <link> tags that declare icons …
Extracting href attributes – 3 candidates found.
Filtered to 1 .ico URLs: ['https://www.python.org/static/favicon.ico']
Saved favicons/favicon.ico
```

Если сайт предоставляет только PNG или Apple touch icons, скрипт выведет их URL‑ы, показывая точно **как получить favicon** в любой ситуации.

## Часто задаваемые вопросы и особые случаи  

### Что если сайт использует тег `<meta>` вместо `<link>`?  
Некоторые старые страницы помещают URL иконки в `<meta name="msapplication‑TileImage">`. Вы можете расширить `find_icon_links`, чтобы искать такие meta‑теги и обрабатывать их аналогично.

### Как обрабатывать относительные URL, начинающиеся с `//`?  
`urljoin` автоматически разрешает протокольно‑относительные URL (`//example.com/favicon.ico`) на основе схемы базового URL, так что дополнительной логики не требуется.

### Можно ли автоматически получать несколько размеров (например, 32×32, 180×180)?  
Да — просто уберите шаг `filter_ico_urls`. Скрипт вернёт каждый найденный URL иконки, включая PNG разных размеров. Затем можно отсортировать или выбрать нужный по шаблону имени файла.

### Работает ли это на сайтах, блокирующих ботов?  
Если сайт отвечает 403 или требует пользовательский User‑Agent, измените вызов `requests.get`:

```python
headers = {"User-Agent": "Mozilla/5.0 (compatible; FaviconBot/1.0)"}
response = requests.get(url, headers=headers, timeout=10)
```

Это небольшое изменение часто решает проблему «как получить favicon» на более строгих доменах.

## Визуальный обзор  

![Диаграмма, показывающая поток получения favicon с веб‑сайта — загрузка HTML, разбор link‑тегов, извлечение href, необязательная загрузка](how-to-get-favicon-diagram.png "Диаграмма потока получения favicon")

*Текст alt изображения содержит основной ключевой запрос, удовлетворяя SEO‑требованиям для изображений.*

## Заключение  

Мы пошагово прошли процесс **как получить favicon**: загрузка HTML по URL,

## Что изучать дальше?

Следующие руководства охватывают близкие темы, опираясь на техники, продемонстрированные в этом гиде. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Как сохранить HTML в C# – Полное руководство с использованием пользовательского обработчика ресурсов](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Как редактировать HTML с помощью Aspose.HTML для Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Как конвертировать HTML в PDF на Java – используя Aspose.HTML для Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
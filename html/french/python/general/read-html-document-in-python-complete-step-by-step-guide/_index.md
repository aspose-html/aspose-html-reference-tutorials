---
category: general
date: 2026-08-09
description: Lire un document HTML en Python rapidement. Apprenez comment analyser
  un fichier HTML avec Python, récupérer du HTML depuis un site web avec Python, et
  comment charger du HTML en Python avec des exemples prêts à l’exécution.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- read html document python
- parse html file python
- how to read html file python
- how to load html in python
- fetch html from website python
language: fr
lastmod: 2026-08-09
og_description: Lire un document HTML en Python pour extraire des données, analyser
  un fichier HTML avec Python et récupérer du HTML depuis un site web avec Python.
  Ce tutoriel vous montre comment charger du HTML en Python en utilisant une petite
  classe d’assistance.
og_image_alt: Screenshot of Python code loading an HTML file and printing the page
  title
og_title: Lire un document HTML en Python – guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-08-09'
  description: Read HTML document in Python quickly. Learn how to parse html file
    python, fetch html from website python, and how to load html in python with ready‑to‑run
    examples.
  headline: Read HTML document in Python – complete step‑by‑step guide
  type: TechArticle
tags:
- Python
- HTML parsing
- Web scraping
title: Lire un document HTML en Python – guide complet étape par étape
url: /fr/python/general/read-html-document-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lire un document HTML en Python – guide complet étape par étape

Si vous devez **lire un document HTML en Python**, ce tutoriel vous montre exactement comment le faire. Que vous souhaitiez analyser un fichier HTML avec Python, récupérer du HTML depuis un site web avec Python, ou simplement charger du HTML en Python pour l’extraction de données, la solution ci‑dessous couvre chaque scénario courant.

Vous terminerez ce guide avec un helper réutilisable `HTMLDocument` qui peut charger du HTML depuis un fichier local, une URL distante ou une chaîne brute. Aucune documentation externe n’est requise — copiez simplement le code, exécutez‑le, et commencez le scraping.

## Ce que couvre ce tutoriel

* Comment lire un document HTML en Python depuis trois sources différentes.  
* Un exemple complet et exécutable incluant la gestion des erreurs et la détection de l’encodage.  
* Astuces pour analyser du HTML en toute sécurité avec **BeautifulSoup** et pour gérer les échecs réseau.  
* Extensions telles que l’extraction du titre de la page, la recherche d’éléments, et la personnalisation du parseur.

**Prérequis**  
* Python 3.8 ou plus récent.  
* Packages `requests` et `beautifulsoup4` (`pip install requests beautifulsoup4`).  

Passons maintenant à l'implémentation.

## Comment lire un document HTML en Python

Below is the core class. It decides whether the supplied argument is a file path, a URL, or a plain HTML string, then creates a `BeautifulSoup` object you can query.

```python
# html_document.py
import pathlib
import requests
from bs4 import BeautifulSoup
from urllib.parse import urlparse

class HTMLDocument:
    """
    Helper to load and parse HTML from a file, a URL, or a raw string.
    The instance attribute `soup` holds a BeautifulSoup object ready for querying.
    """

    def __init__(self, source: str):
        """
        Detect the source type and load the HTML accordingly.
        :param source: file path, URL, or raw HTML string.
        """
        self.source = source
        self.html = self._load_source(source)
        # Use the built‑in html.parser for speed; switch to "lxml" if needed.
        self.soup = BeautifulSoup(self.html, "html.parser")

    def _load_source(self, src: str) -> str:
        """Return raw HTML text from the given source."""
        # 1️⃣ Is it a local file?
        if pathlib.Path(src).is_file():
            return self._load_file(src)

        # 2️⃣ Is it a well‑formed URL?
        parsed = urlparse(src)
        if parsed.scheme in ("http", "https"):
            return self._load_url(src)

        # 3️⃣ Otherwise treat it as a literal HTML string.
        return src

    def _load_file(self, path: str) -> str:
        """Read an HTML file from disk, handling common encodings."""
        try:
            with open(path, "r", encoding="utf-8") as f:
                return f.read()
        except UnicodeDecodeError:
            # Fallback to latin‑1 if UTF‑8 fails.
            with open(path, "r", encoding="latin-1") as f:
                return f.read()

    def _load_url(self, url: str) -> str:
        """Fetch HTML from a remote website, raising for HTTP errors."""
        try:
            response = requests.get(url, timeout=10)
            response.raise_for_status()
            # requests guesses the correct encoding; force utf‑8 if unsure.
            response.encoding = response.apparent_encoding or "utf-8"
            return response.text
        except requests.RequestException as exc:
            raise RuntimeError(f"Failed to fetch {url}: {exc}") from exc

    # -----------------------------------------------------------------
    # Convenience helpers ------------------------------------------------
    # -----------------------------------------------------------------
    def title(self) -> str | None:
        """Return the <title> text if present."""
        if self.soup.title:
            return self.soup.title.string.strip()
        return None

    def find(self, *args, **kwargs):
        """Proxy to BeautifulSoup.find – useful for quick queries."""
        return self.soup.find(*args, **kwargs)

    def find_all(self, *args, **kwargs):
        """Proxy to BeautifulSoup.find_all."""
        return self.soup.find_all(*args, **kwargs)
```

**Pourquoi cette classe ?**  
* Elle abstrait le problème *how to read html file python* en un seul objet réutilisable.  
* Elle centralise la gestion des erreurs (problèmes d’encodage de fichier, délais d’attente réseau) afin que votre code de scraping reste propre.  
* En exposant `soup`, vous pouvez exploiter toute la puissance de **BeautifulSoup** sans réécrire de code boilerplate.

### Exemple d'utilisation

```python
# example.py
from html_document import HTMLDocument

# 1️⃣ Load an HTML document from a local file
doc_from_file = HTMLDocument("samples/index.html")
print("File title:", doc_from_file.title())

# 2️⃣ Load an HTML document directly from a web URL
doc_from_url = HTMLDocument("https://example.com")
print("URL title:", doc_from_url.title())

# 3️⃣ Load an HTML document from an HTML string
html_content = "<html><body><h1>Hello, world!</h1></body></html>"
doc_from_string = HTMLDocument(html_content)
print("String title:", doc_from_string.title())   # None – no <title> tag
```

**Sortie attendue**

```
File title: Sample Index Page
URL title: Example Domain
String title: None
```

Le script montre les trois façons de **charger du HTML en Python** et affiche le titre de la page lorsqu'il est disponible.

## Analyser un fichier HTML en Python

Une fois que vous avez `doc_from_file.soup`, vous pouvez interroger n’importe quel élément. Voici une illustration rapide de l’extraction de tous les hyperliens :

```python
# Extract all <a> tags and their href attributes
links = doc_from_file.find_all("a")
for link in links:
    href = link.get("href")
    text = link.get_text(strip=True)
    print(f"Link text: {text} → {href}")
```

**Pourquoi analyser un fichier HTML en Python ?**  
L’analyse vous permet de transformer un balisage non structuré en données structurées que vous pouvez stocker, analyser ou transmettre à d’autres systèmes. L’API de BeautifulSoup rend cela simple, et le wrapper `HTMLDocument` garantit que vous partez toujours d’un objet soup propre.

## Charger du HTML depuis une URL en Python

Récupérer une page distante est souvent la première étape d’un pipeline de web‑scraping. Le helper effectue automatiquement :

* Définit un délai d’attente (10 secondes) pour éviter que les scripts ne restent bloqués.  
* Lève une exception claire si le statut HTTP n’est pas 200.  
* Détecte le bon encodage des caractères.

Si vous devez personnaliser la requête (en‑têtes, authentification, proxys), modifiez la méthode `_load_url` :

```python
def _load_url(self, url: str) -> str:
    headers = {"User-Agent": "MyScraper/1.0 (+https://mydomain.com)"}
    response = requests.get(url, headers=headers, timeout=10)
    response.raise_for_status()
    response.encoding = response.apparent_encoding or "utf-8"
    return response.text
```

**Comment récupérer du HTML depuis un site web en Python** efficacement ?  
* Utilisez un `User-Agent` réaliste.  
* Respectez le `robots.txt` et limitez le taux de vos requêtes.  
* Mettez en cache les réponses localement si vous revisitez souvent la même page.

## Créer un HTMLDocument à partir d'une chaîne

Parfois vous avez déjà du balisage brut — peut‑être généré par un moteur de templates ou reçu d’une API. Passer directement la chaîne évite des I/O inutiles :

```python
html_snippet = """
<div class="product">
    <h2>Widget</h2>
    <p class="price">$19.99</p>
</div>
"""
doc = HTMLDocument(html_snippet)
price = doc.find("p", class_="price").get_text(strip=True)
print("Extracted price:", price)   # → Extracted price: $19.99
```

**Quand utiliser ce modèle ?**  
* Tester les parseurs en unité sans toucher au réseau.  
* Analyser le corps d’e‑mails ou les réponses d’API qui contiennent du HTML.  

## Pièges courants et bonnes pratiques

| Problème | Pourquoi c’est important | Solution recommandée |
|----------|--------------------------|----------------------|
| **Encodage incorrect** | Des caractères illisibles apparaissent lorsque le fichier n’est pas en UTF‑8. | Utilisez une solution de secours (`latin-1`) ou laissez `requests` deviner l’encodage (`apparent_encoding`). |
| **`<title>` manquant** | `doc.title()` renvoie `None`, ce qui peut provoquer une `AttributeError` si vous supposez une chaîne. | Vérifiez toujours que la valeur n’est pas `None` avant de l’utiliser. |
| **Délais d’attente réseau** | Les scripts peuvent rester bloqués indéfiniment sur des serveurs lents. | Définissez un délai d’attente (`requests.get(..., timeout=10)`) et capturez `requests.RequestException`. |
| **Contenu dynamique** | Le HTML généré par JavaScript ne sera pas présent dans la réponse brute. | Utilisez un navigateur sans tête comme Selenium ou Playwright pour le rendu. |
| **Pages volumineuses** | Analyser un HTML très volumineux peut consommer beaucoup de mémoire. | Diffusez la réponse (`requests.get(..., stream=True)`) et analysez de façon incrémentielle si possible. |

## Exemple complet fonctionnel

Enregistrez les deux fichiers (`html_document.py` et `example.py`) dans le même répertoire, installez les dépendances, et exécutez :

```bash
pip install requests beautifulsoup4
python example.py
```

Vous devriez voir les titres affichés, suivis de toute donnée supplémentaire que vous interrogez. Le code fonctionne sous Windows, macOS et Linux avec n’importe quel interpréteur Python récent.

## Conclusion

Vous savez maintenant **comment lire un document HTML en Python** en utilisant une classe compacte `HTMLDocument` qui prend en charge la lecture depuis des fichiers, des URL et des chaînes brutes.

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications étape par étape pour vous aider à maîtriser d’autres fonctionnalités d’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Charger des documents HTML depuis un fichier avec Aspose.HTML pour Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Comment modifier l’arbre d’un document HTML avec Aspose.HTML pour Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Enregistrer un document HTML dans un fichier avec Aspose.HTML pour Java](/html/english/java/saving-html-documents/save-html-to-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
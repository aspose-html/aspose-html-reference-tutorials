---
category: general
date: 2026-06-26
description: Apprenez à récupérer le favicon en chargeant le HTML depuis une URL et
  en extrayant le href des balises <link>. Code Python étape par étape pour obtenir
  rapidement les icônes de sites web.
draft: false
keywords:
- how to get favicon
- load html from url
- get website icons
- extract href from link
- how to extract favicons
language: fr
og_description: 'Comment obtenir rapidement le favicon : charger le HTML depuis l’URL,
  trouver la balise <link rel=''icon''>, et extraire le href des balises <link> en
  utilisant Python.'
og_title: Comment obtenir un favicon – Tutoriel Python
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
title: Comment obtenir le favicon – Guide complet Python pour extraire les icônes
  de site
url: /fr/python/general/how-to-get-favicon-complete-python-guide-for-extracting-site/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment obtenir le favicon – Guide complet Python pour extraire les icônes de site

Vous vous êtes déjà demandé **how to get favicon** sur n'importe quel site sans fouiller manuellement le code source de la page ? Vous n'êtes pas le seul—les développeurs, les experts SEO et même les designers ont souvent besoin de la petite icône qui représente un site. Dans ce tutoriel, nous vous montrerons une méthode propre, centrée sur Python, pour charger le HTML depuis une URL, localiser les balises `<link rel="icon">` et extraire les URL des icônes. À la fin, vous saurez exactement **how to get favicon** pour n'importe quel domaine, et vous disposerez d'un script réutilisable prêt pour vos projets.

Nous couvrirons tout, depuis la récupération du HTML jusqu'à la prise en compte des cas particuliers comme les URL relatives et les multiples formats d'icônes. Aucun service externe requis—seulement la bibliothèque standard `requests` et un analyseur HTML léger. Prêt à commencer ? Plongeons‑y.

## Prérequis

- Python 3.8+ installé (le code fonctionne également avec 3.10)  
- Familiarité de base avec `requests` et les compréhensions de listes  
- Accès Internet au site cible  

Si vous avez déjà tout cela, super—passez à la première étape. Sinon, installez la seule dépendance dont nous avons besoin :

```bash
pip install requests beautifulsoup4
```

> **Conseil pro :** `beautifulsoup4` est un analyseur éprouvé qui rend le “load html from url” un jeu d'enfant.

## Étape 1 : Charger le HTML depuis une URL avec Python  

La première chose à faire lorsque vous apprenez **how to get favicon** est de récupérer le source de la page. C’est la partie “load html from url” du processus.

```python
import requests
from bs4 import BeautifulSoup

def fetch_html(url: str) -> str:
    """Download the raw HTML of *url* and return it as text."""
    response = requests.get(url, timeout=10)
    response.raise_for_status()   # will raise if the request failed
    return response.text
```

Pourquoi utiliser `requests` ? Il gère les redirections, la vérification HTTPS et les délais d’attente automatiquement, ce qui signifie moins de surprises lorsque vous essayez plus tard de **get website icons**.

## Étape 2 : Analyser le document et trouver les liens d'icônes  

Maintenant que nous avons le HTML, nous devons localiser tous les éléments `<link>` dont l’attribut `rel` indique une icône. C’est le cœur de **how to get favicon**.

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

Notez que nous vérifions à la fois `icon` et `shortcut icon` car les sites plus anciens utilisent encore ce dernier. Cette petite nuance perturbe souvent les gens lorsqu’ils recherchent “how to extract favicons”.

## Étape 3 : Extraire le href des éléments link  

Avec les balises pertinentes en main, l’étape logique suivante—**extract href from link**—est simple.

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

Utiliser `urljoin` garantit que même si un site fournit un chemin relatif comme `/favicon.ico`, vous obtiendrez une URL absolue correcte—crucial pour un script fiable de **how to get favicon**.

## Étape 4 : Optionnel – Valider et filtrer les URL d'icônes  

Parfois une page répertorie de nombreuses icônes (Apple touch icons, PNG de tailles diverses, etc.). Si vous ne vous intéressez qu’au fichier `.ico` classique, filtrez en conséquence. Cette étape montre **how to extract favicons** d’un type spécifique.

```python
def filter_ico_urls(urls: list[str]) -> list[str]:
    """Keep only URLs that end with .ico (case‑insensitive)."""
    return [u for u in urls if u.lower().endswith(".ico")]
```

N’hésitez pas à ajuster le filtre : remplacez `".ico"` par `".png"` ou vérifiez `rel="apple-touch-icon"` si vous avez besoin d’icônes haute résolution.

## Étape 5 : Télécharger les fichiers d'icônes (si vous voulez l'image réelle)  

Extraire les URL, c’est déjà la moitié du travail ; le téléchargement vous fournit un fichier que vous pouvez afficher ou stocker. Voici un petit utilitaire :

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

Exécuter cela après les étapes précédentes vous donne une copie locale de chaque favicon découvert, parfaite pour la mise en cache ou l’analyse hors ligne.

## Étape 6 : Assembler le tout – Exemple complet fonctionnel  

Voici le script complet, prêt à être exécuté, qui démontre **how to get favicon** depuis n’importe quel site. Copiez‑collez, modifiez le `target_url`, et observez le résultat.

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

**Sortie attendue (troncature pour la brièveté) :**

```
Fetching HTML from https://www.python.org …
Finding <link> tags that declare icons …
Extracting href attributes – 3 candidates found.
Filtered to 1 .ico URLs: ['https://www.python.org/static/favicon.ico']
Saved favicons/favicon.ico
```

Si le site ne fournit que des PNG ou des Apple touch icons, le script listera ces URL à la place, vous montrant exactement **how to get favicon** dans chaque scénario.

## Questions fréquentes & cas limites  

### Que faire si le site utilise une balise `<meta>` au lieu de `<link>` ?  
Certaines pages plus anciennes intègrent l’URL de l’icône dans une balise `<meta name="msapplication‑TileImage">`. Vous pouvez étendre `find_icon_links` pour rechercher également ces balises meta et les traiter de la même façon.

### Comment gérer les URL relatives qui commencent par `//` ?  
`urljoin` résout automatiquement les URL relatives au protocole (`//example.com/favicon.ico`) en fonction du schéma de l’URL de base, vous n’avez donc pas besoin de logique supplémentaire.

### Puis‑je récupérer plusieurs tailles (p. ex., 32×32, 180×180) automatiquement ?  
Oui—supprimez simplement l’étape `filter_ico_urls`. Le script renverra chaque URL d’icône qu’il découvre, y compris les PNG de différentes dimensions. Vous pourrez ensuite trier ou sélectionner selon le motif du nom de fichier.

### Cela fonctionne‑t‑il sur les sites qui bloquent les bots ?  
Si un site renvoie un 403 ou nécessite un User‑Agent personnalisé, ajustez l’appel `requests.get` :

```python
headers = {"User-Agent": "Mozilla/5.0 (compatible; FaviconBot/1.0)"}
response = requests.get(url, headers=headers, timeout=10)
```

Ce petit changement résout souvent le problème “how to get favicon” sur les domaines plus stricts.

## Vue d'ensemble visuelle  

![Diagramme montrant le flux de how to get favicon depuis un site web – charger le HTML, analyser les balises link, extraire le href, téléchargement optionnel](how-to-get-favicon-diagram.png "how to get favicon flow diagram")

*Le texte alternatif de l’image contient le mot‑clé principal, satisfaisant le SEO pour les images.*

## Conclusion  

Nous avons parcouru **how to get favicon** étape par étape : charger le HTML depuis une URL,

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
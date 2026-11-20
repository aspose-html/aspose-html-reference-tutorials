---
category: general
date: 2026-06-10
description: Chargez le HTML depuis une URL pour obtenir rapidement les icônes d’un
  site web. Apprenez à extraire les favicons, récupérer les URL des favicons d’un
  site et gérer les cas particuliers en Python.
draft: false
keywords:
- load html from url
- get website icons
- how to extract favicons
- extract favicon urls
- fetch website favicon urls
language: fr
og_description: Chargez le HTML depuis une URL pour extraire les favicons et récupérer
  les URL des favicons du site. Un tutoriel Python étape par étape pour les développeurs.
og_title: Charger le HTML depuis une URL et récupérer les icônes du site – Guide complet
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
title: Charger le HTML depuis une URL et récupérer les icônes du site – Guide complet
url: /fr/python/general/load-html-from-url-and-get-website-icons-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Charger le HTML depuis une URL et récupérer les icônes d’un site – Guide complet

Vous avez déjà eu besoin de **charger le HTML depuis une URL** juste pour récupérer le petit logo d’un site ? Vous n’êtes pas seul. Que vous construisiez un gestionnaire de favoris, un tableau de bord SEO, ou simplement un projet personnel, récupérer les icônes d’un site est une petite mais essentielle pièce du puzzle.

Dans ce tutoriel, nous vous montrerons **comment extraire les favicons** en utilisant du Python pur—pas de Selenium lourd, pas de magie de navigateur. À la fin, vous serez capable de **récupérer les URLs des favicons d’un site**, de gérer les chemins relatifs, et même de récupérer plusieurs icônes si un site en fournit. Prêt ? Plongeons‑y.

## Pourquoi charger le HTML depuis une URL en premier lieu ?

Charger le HTML brut d’une page vous donne un accès direct aux balises `<link>` que les navigateurs utilisent pour localiser les favicons. Ces balises ressemblent généralement à :

```html
<link rel="icon" href="/favicon.ico">
<link rel="apple-touch-icon" href="https://example.com/apple-touch-icon.png">
```

Si vous pouvez extraire ce balisage, vous pouvez lire programmétiquement l’attribut `href` et télécharger l’image vous‑même. C’est plus rapide que de scraper des captures d’écran, et cela fonctionne pour tout site qui suit les conventions standard.

## Étape 1 – Charger le document HTML depuis une URL

La première chose dont nous avons besoin est une méthode pour récupérer le source de la page. Le choix le plus populaire en Python est la bibliothèque **requests** car elle est simple, fiable, et gère les redirections automatiquement.

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

> **Astuce :** Si vous travaillez derrière un proxy d’entreprise, passez `proxies=` à `requests.get`. De plus, définir un timeout court empêche votre script de rester bloqué sur des sites morts.

Nous pouvons maintenant appeler `fetch_html("https://example.com")` et obtenir une chaîne contenant le balisage de la page. C’est le cœur du **chargement du HTML depuis une URL**—le reste du pipeline travaille avec cette chaîne.

## Étape 2 – Récupérer les icônes du site

Une fois que nous avons le HTML, l’étape suivante consiste à localiser chaque élément `<link>` dont l’attribut `rel` mentionne « icon ». Le module intégré `html.parser` peut faire le travail, mais **BeautifulSoup** rend le code beaucoup plus lisible.

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

Remarquez comment nous utilisons `urljoin` pour transformer `"/favicon.ico"` en `"https://example.com/favicon.ico"`—c’est un cas limite courant lors de la **récupération des icônes du site**. Certains sites servent même différentes icônes pour différents appareils, vous pourriez donc vous retrouver avec une poignée d’URLs. Aucun problème ; nous les collectons simplement toutes.

## Étape 3 – Extraire les URLs des favicons et les afficher

Assembler les pièces est simple. Nous récupérerons le HTML, exécuterons l’extracteur, et afficherons la liste résultante. Le script final ressemble à ceci :

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

### Sortie attendue

Exécuter le script sur un site qui fournit un favicon standard peut vous donner :

```
Found icon URLs: ['https://example.com/favicon.ico']
```

Si le site fournit plusieurs icônes (Apple touch icon, shortcut icon, etc.), vous verrez une liste plus longue :

```
Found icon URLs: [
    'https://example.com/favicon.ico',
    'https://example.com/apple-touch-icon.png',
    'https://example.com/favicon-32x32.png'
]
```

C’est l’ensemble du flux de travail **extract favicon urls**—compact, léger en dépendances, et prêt à être intégré dans n’importe quel projet.

## Gérer les problèmes courants

| Problème | Pourquoi cela se produit | Solution rapide |
|----------|--------------------------|-----------------|
| **Relative `href` sans balise `<base>`** | `urljoin` suppose l’URL de la page comme base, ce qui fonctionne dans la plupart des cas. | Si une balise `<base href="...">` existe, lisez‑la d’abord et passez‑la comme `base_url`. |
| **Missing `rel="icon"`** | Certains sites utilisent `rel="shortcut icon"` ou des valeurs personnalisées. | Étendez la lambda : `rel=lambda r: r and ("icon" in r.lower() or "shortcut" in r.lower())`. |
| **Redirects to a different domain** | Le favicon peut être hébergé sur un CDN. | `urljoin` résoudra correctement le nouveau domaine car il utilise l’URL finale de la requête (`response.url`). |
| **Broken links (404)** | Le HTML pointe vers un fichier qui n’existe plus. | Après avoir extrait les URLs, vous pouvez vérifier chacune avec une requête HEAD avant de les utiliser. |
| **Multiple `<link>` tags with the same icon** | Les entrées dupliquées gonflent la liste. | Utilisez `set(icon_urls)` pour dédupliquer avant de retourner. |

## Aller plus loin – Récupérer les URLs des favicons de sites en masse

Si vous devez **récupérer les URLs des favicons de sites** pour une liste de domaines, encapsulez la logique `main` dans une boucle :

```python
domains = ["https://example.com", "https://python.org", "https://github.com"]
for site in domains:
    try:
        icons = extract_icon_links(fetch_html(site), site)
        print(site, "->", icons)
    except Exception as e:
        print(site, "error:", e)
```

## Vue d’ensemble visuelle

![Diagramme du chargement du HTML depuis une URL montrant les étapes fetch → parse → extract](load-html-url.png)

L’image ci‑dessus condense le processus en trois étapes : **load HTML from URL**, **get website icons**, et **extract favicon URLs**. C’est pratique lorsque vous devez expliquer le flux à un collègue.

## Conclusion

Nous avons parcouru une solution complète, prête pour la production, pour **load HTML from URL** et **get website icons** en utilisant uniquement les bibliothèques requests et BeautifulSoup de Python. En extrayant les attributs `href` des balises `<link rel="icon">`, vous pouvez **extract favicon URLs**, gérer les chemins relatifs, et même récupérer plusieurs formats d’icônes—le tout en quelques dizaines de lignes de code.

Et après ? Essayez de télécharger les icônes dans un dossier local, générez un CSV de correspondances domaine‑à‑favicon, ou intégrez cette logique dans une API Flask qui sert les favicons à la demande. Les possibilités pour **fetch website favicon URLs** sont infinies, et la technique de base reste la même.

Des questions sur les cas limites, ou envie de partager une astuce ingénieuse ? Laissez un commentaire ci‑dessous—bonne chasse aux icônes !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Load HTML Documents from Stream with Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-stream/)
- [Handle Document Load Events in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/handle-document-load-events/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
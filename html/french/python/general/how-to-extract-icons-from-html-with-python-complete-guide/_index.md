---
category: general
date: 2026-07-02
description: Comment extraire les icônes d’un fichier HTML avec Python. Apprenez à
  lire un fichier HTML en Python, à analyser le document HTML et à extraire l’attribut
  href pour obtenir les URL des favicons.
draft: false
keywords:
- how to extract icons
- read html file python
- parse html document
- extract href attribute
- extract favicon urls
language: fr
og_description: Comment extraire les icônes d’une page HTML avec Python. Ce tutoriel
  vous montre comment lire un fichier HTML avec Python, analyser le document et extraire
  les URL des favicons.
og_title: Comment extraire des icônes du HTML – Guide Python
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: How to extract icons from an HTML file using Python. Learn to read
    HTML file python, parse HTML document, and extract href attribute to get favicon
    URLs.
  headline: How to Extract Icons from HTML with Python – Complete Guide
  type: TechArticle
- questions:
  - answer: Some sites embed icons via `<meta itemprop="image">`. Extend `is_icon_link`
      to also check for `meta` with `itemprop="image"` and pull its `content` attribute.
    question: What if the HTML uses `<meta>` tags for icons?
  - answer: Yes—just feed each URL into `requests.get(url, stream=True)` and write
      the content to a file. Remember to handle relative URLs with `urljoin`.
    question: Can I fetch the icons automatically?
  - answer: 'Absolutely. Replace the file‑reading step with `requests.get(page_url).text`
      and pass the HTML string to BeautifulSoup. Just be mindful of robots.txt and
      rate limits. --- ## Wrap‑Up We’ve covered **how to extract icons** from any
      static HTML using Python, from reading the file to printing out each f'
    question: Does this work on remote pages?
  type: FAQPage
tags:
- python
- html-parsing
- web‑scraping
- favicon
title: Comment extraire des icônes d'HTML avec Python – Guide complet
url: /fr/python/general/how-to-extract-icons-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment extraire des icônes d'un HTML avec Python – Guide complet

Vous vous êtes déjà demandé **comment extraire des icônes** d’une page web sans ouvrir de navigateur ? Peut-être que vous créez un catalogue de sites, un outil d’audit SEO, ou que vous êtes simplement curieux des petites favicons qui apparaissent dans les onglets. La bonne nouvelle, c’est que vous pouvez le faire en quelques lignes de Python—sans Selenium, sans Chrome sans tête, juste un fichier HTML en texte brut.

Dans ce tutoriel, nous allons parcourir la lecture d’un fichier HTML avec Python, l’analyse du document HTML, et enfin **extraire l’attribut href** des balises `<link rel="icon">` pour obtenir les URL de ces favicons. À la fin, vous disposerez d’un extrait réutilisable qui fonctionne sur n’importe quel HTML statique que vous lui soumettez, et vous verrez également comment gérer les cas particuliers comme les chemins relatifs ou les déclarations d’icônes multiples.

## Ce que vous allez apprendre

- Charger un fichier HTML local avec Python (lire un fichier html python)  
- Utiliser un analyseur léger pour **analyser le document html** en toute sécurité  
- Localiser les éléments `<link>` qui déclarent une icône  
- **Extraire les valeurs de l’attribut href** et les transformer en URL absolues  
- Collecter et afficher toutes les **URL de favicons** découvertes  

Aucun service externe requis—seulement la bibliothèque standard et le populaire package **BeautifulSoup**.

---

![Capture d’écran montrant le script Python extrayant des icônes – comment extraire des icônes](https://example.com/images/extract-icons-python.png "comment extraire des icônes")

*Texte alternatif de l’image : « comment extraire des icônes à l’aide d’un script Python »*

## Prérequis

- Python 3.8+ installé  
- Bibliothèque `beautifulsoup4` (`pip install beautifulsoup4`)  
- Un fichier HTML local que vous souhaitez analyser (par ex., `sample.html`)  

Si vous avez déjà tout cela, passons à l’action.

## Étape 1 : Lire le fichier HTML avec Python – Charger le document

Première chose à faire : nous devons ouvrir le fichier et fournir son contenu à un analyseur. Utiliser `with open(..., "r", encoding="utf‑8")` garantit que le fichier est fermé automatiquement, et le codage UTF‑8 gère la plupart des pages modernes.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Step 1: Load the HTML document from disk
html_path = Path("sample.html")          # adjust the path as needed
html_content = html_path.read_text(encoding="utf-8")
```

**Pourquoi c’est important :** Ouvrir le fichier avec le bon encodage évite les caractères mystérieux `�` qui pourraient casser l’analyseur plus tard. Utiliser `Path` de la bibliothèque standard rend également le code multiplateforme.

## Étape 2 : Analyser le document HTML – Trouver tous les liens d’icônes

Nous transmettons maintenant le HTML brut à **BeautifulSoup**, qui construit un arbre navigable. Nous rechercherons chaque balise `<link>` dont l’attribut `rel` contient le mot `icon`. Notez que `rel` peut être une liste séparée par des espaces (`rel="shortcut icon"`), donc nous avons besoin d’une vérification flexible.

```python
# Step 2: Parse the HTML and locate <link> tags that declare an icon
soup = BeautifulSoup(html_content, "html.parser")

def is_icon_link(tag):
    """Return True if a <link> tag declares an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    # BeautifulSoup may return a list or a string; handle both
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

icon_links = [tag for tag in soup.find_all(is_icon_link)]
```

**Pourquoi cette étape est cruciale :** Un `soup.find_all("link", rel="icon")` naïf manquerait des variantes comme `rel="shortcut icon"` ou `rel="apple-touch-icon"`. Notre fonction d’aide `is_icon_link` couvre ces cas, rendant l’extraction robuste.

## Étape 3 : Extraire l’attribut href – Récupérer les URL

Avec les balises pertinentes collectées, nous extrayons maintenant l’attribut `href` de chacune. Certaines pages peuvent omettre `href` (rare, mais possible), donc nous nous protégeons contre `None`. De plus, les favicons sont souvent spécifiés avec des URL relatives, nous les résoudrons donc par rapport à l’URL de base de la page si vous la connaissez. Pour un fichier local, nous garderons simplement le chemin tel quel.

```python
# Step 3: Grab the href attribute from each icon link
icon_urls = []
for tag in icon_links:
    href = tag.get("href")
    if href:
        icon_urls.append(href.strip())
```

**Pourquoi nous supprimons les espaces :** Les auteurs HTML ajoutent parfois accidentellement des espaces autour des URL, ce qui casserait une requête ultérieure. Le découpage assure d’obtenir des chaînes propres.

## Étape 4 : Extraire les URL de favicons – Afficher les résultats

Enfin, nous affichons (ou retournons) la liste des URL découvertes. Dans un script réel, vous pourriez les écrire dans un CSV, télécharger les icônes, ou les transmettre à un autre service. Voici une boucle simple qui montre le résultat dans la console.

```python
# Step 4: Display each discovered favicon URL
if not icon_urls:
    print("No icon links found in the document.")
else:
    for url in icon_urls:
        print("Favicon URL:", url)
```

### Gestion des cas particuliers

- **Valeurs `rel` multiples :** Notre vérification `is_icon_link` capture déjà `rel="shortcut icon"` et `rel="apple-touch-icon"`.  
- **Chemins relatifs :** Si vous avez besoin plus tard d’URL absolues, utilisez `urllib.parse.urljoin(base_url, href)`.  
- **`href` manquant :** La protection `if href:` ignore les balises mal formées, évitant les erreurs `NoneType`.  
- **Entrées dupliquées :** Vous pouvez `icon_urls = list(dict.fromkeys(icon_urls))` pour dédupliquer.

---

## Script complet – Solution tout‑en‑un

En rassemblant le tout, voici le programme complet, prêt à être exécuté. Enregistrez‑le sous le nom `extract_icons.py` et pointez `html_path` vers n’importe quel fichier que vous souhaitez.

```python
#!/usr/bin/env python3
"""
How to extract icons from an HTML file using Python.

This script:
- Reads an HTML file (read html file python)
- Parses the HTML document (parse html document)
- Finds <link> tags with rel containing "icon"
- Extracts the href attribute (extract href attribute)
- Prints each favicon URL (extract favicon urls)
"""

from pathlib import Path
from bs4 import BeautifulSoup

def is_icon_link(tag):
    """Detect <link> tags that declare an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

def extract_favicon_urls(html_path: Path):
    """Return a list of favicon URLs found in the given HTML file."""
    html_content = html_path.read_text(encoding="utf-8")
    soup = BeautifulSoup(html_content, "html.parser")
    icon_links = [t for t in soup.find_all(is_icon_link)]

    urls = []
    for tag in icon_links:
        href = tag.get("href")
        if href:
            urls.append(href.strip())
    # Remove duplicates while preserving order
    return list(dict.fromkeys(urls))

if __name__ == "__main__":
    # Adjust the path to point to your HTML file
    html_file = Path("sample.html")
    favicon_urls = extract_favicon_urls(html_file)

    if not favicon_urls:
        print("No icon links found in the document.")
    else:
        for url in favicon_urls:
            print("Favicon URL:", url)
```

**Sortie attendue** (en supposant que `sample.html` contienne deux icônes) :

```
Favicon URL: /images/favicon.ico
Favicon URL: https://example.com/assets/apple-touch-icon.png
```

Exécutez‑le avec `python extract_icons.py` et vous verrez les URL affichées dans la console.

---

## Questions fréquentes

**Q : Et si le HTML utilise des balises `<meta>` pour les icônes ?**  
R : Certains sites intègrent des icônes via `<meta itemprop="image">`. Étendez `is_icon_link` pour vérifier également les `meta` avec `itemprop="image"` et extraire leur attribut `content`.

**Q : Puis‑je récupérer les icônes automatiquement ?**  
R : Oui—il suffit d’alimenter chaque URL dans `requests.get(url, stream=True)` et d’écrire le contenu dans un fichier. N’oubliez pas de gérer les URL relatives avec `urljoin`.

**Q : Cela fonctionne‑t‑il sur des pages distantes ?**  
R : Absolument. Remplacez l’étape de lecture du fichier par `requests.get(page_url).text` et passez la chaîne HTML à BeautifulSoup. Soyez simplement attentif au robots.txt et aux limites de taux.

---

## Conclusion

Nous avons couvert **comment extraire des icônes** de n’importe quel HTML statique avec Python, depuis la lecture du fichier jusqu’à l’affichage de chaque URL de favicon. Les idées principales—lecture du fichier, analyse du document, localisation des balises appropriées, et extraction de l’attribut `href`—sont des modèles réutilisables que vous rencontrerez dans de nombreuses tâches de web‑scraping.

Prochaines étapes ? Essayez d’étendre le script pour :

- Résoudre les URL relatives par rapport à l’URL de base de la page  
- Télécharger chaque icône et l’enregistrer localement  
- Prendre en charge des formats d’icônes supplémentaires (`rel="mask-icon"` pour Safari)

N’hésitez pas à expérimenter, et si vous rencontrez des particularités, laissez un commentaire ci‑dessous. Bon parsing !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d’API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment interroger le HTML en Java – Tutoriel complet](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Comment modifier l’arbre du document HTML dans Aspose.HTML pour Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Enregistrer le document HTML dans un fichier avec Aspose.HTML pour Java](/html/english/java/saving-html-documents/save-html-to-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
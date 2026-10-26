---
category: general
date: 2026-06-07
description: Comment ajouter un préfixe aux titres HTML avec Python. Apprenez à sélectionner
  plusieurs titres, à modifier les titres HTML et à enregistrer le HTML modifié efficacement.
draft: false
keywords:
- how to add prefix
- select multiple headings
- save modified html
- change html titles
- modify html with python
language: fr
og_description: Comment ajouter un préfixe aux titres HTML avec Python. Ce tutoriel
  montre comment sélectionner plusieurs titres, modifier les titres HTML et enregistrer
  le HTML modifié en quelques lignes seulement.
og_title: Comment ajouter un préfixe aux titres HTML avec Python – Guide rapide
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
title: Comment ajouter un préfixe aux titres HTML avec Python – Guide étape par étape
url: /fr/python/general/how-to-add-prefix-to-html-headings-with-python-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment ajouter un préfixe aux titres HTML avec Python – Tutoriel complet

Ajouter un préfixe aux titres HTML avec Python est un besoin fréquent lorsque vous maintenez un site qui reçoit des mises à jour régulières. Dans ce guide, nous parcourrons la sélection de plusieurs titres, la modification des titres HTML et l’enregistrement du HTML modifié — le tout sans quitter votre éditeur.  

Si vous vous êtes déjà demandé s’il était possible d’automatiser le badge « marqué comme mis à jour » sur des dizaines de pages, vous êtes au bon endroit. Nous aborderons également comment **modify html with python** de manière évolutive, afin que vous n'ayez pas à ouvrir chaque fichier manuellement.

## Ce que vous allez accomplir

* **Sélectionner plusieurs titres** (`h1`, `h2`, `h3`) en une seule passe.  
* **Ajouter un préfixe personnalisé** (par ex., `[Updated]`) à chaque texte de titre.  
* **Enregistrer le html modifié** sur le disque, en préservant la structure de fichiers d'origine.  
* Comprendre les compromis entre les différents analyseurs HTML Python, et choisir celui qui convient à votre projet.

Pas de services externes, pas de frameworks lourds — juste du pur Python et quelques bibliothèques bien maintenues.

---

## Comment ajouter un préfixe au texte des titres avec Python

Voici un exemple minimal et exécutable qui illustre l’idée principale. Il utilise la bibliothèque **`lxml`** ainsi que **`cssselect`** pour la prise en charge des sélecteurs, ce qui reproduit la méthode `query_selector_all` que vous avez vue dans l’extrait original.

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

**Sortie attendue** (extrait de `article_updated.html`) :

```html
<h1>[Updated] Introduction to Machine Learning</h1>
<h2>[Updated] Data Pre‑processing Steps</h2>
<h3>[Updated] Feature Engineering Techniques</h3>
```

Remarquez comment chaque titre commence maintenant par le tag `[Updated]` — exactement ce que nous voulions lorsque nous avons demandé **how to add prefix** à nos titres.

### Pourquoi cette approche fonctionne

* **`lxml` + `cssselect`** vous offre la puissance complète des sélecteurs CSS, rendant l’étape « select multiple headings » en une seule ligne.  
* La méthode `text_content()` extrait en toute sécurité le texte interne, évitant les entités HTML ou les balises enfants.  
* Écrire de nouveau avec `pretty_print=True` garde le fichier lisible par l'homme, ce qui est pratique pour les diff de contrôle de version.

## Sélectionner plusieurs titres avec des sélecteurs CSS

Si vous venez d’un contexte JavaScript, la syntaxe `cssselect` vous semblera familière. Le sélecteur `"h1, h2, h3"` est une **liste séparée par des virgules**, signifiant « prendre tout élément qui correspond *à l’un* de ces trois ».  

Vous pouvez également élargir la portée :

```python
# Grab every heading from h1 through h6
all_headings = doc.cssselect("h1, h2, h3, h4, h5, h6")
```

Ou la restreindre à une section spécifique :

```python
# Only headings inside the <article> tag
article_headings = doc.cssselect("article h1, article h2, article h3")
```

Ces petits ajustements vous permettent de **select multiple headings** avec une précision laser, ce qui est particulièrement utile lorsque vous avez un site de documentation massif et que vous ne souhaitez mettre à jour qu’une sous-section.

## Enregistrer les fichiers HTML modifiés en toute sécurité

Lorsque vous **save modified html**, vous devez éviter de corrompre le fichier original. Le modèle présenté ci‑dessus écrit dans un nouveau fichier (`article_updated.html`). Ainsi vous pouvez :

1. Vérifier les changements dans un outil de diff.  
2. Revenir immédiatement en arrière si quelque chose semble incorrect.  
3. Conserver l'original intact à des fins d’audit.

Si vous préférez une modification en place, il suffit d’échanger les chemins :

```python
import shutil
shutil.move(output_path, input_path)  # Overwrites the original
```

Mais souvenez‑vous : **always back up** avant d’écraser, surtout sur les serveurs de production.

## Modifier les titres HTML vs. les titres de page

Vous vous demandez peut‑être si « changing HTML titles » est identique à préfixer les titres. En terminologie HTML, la balise `<title>` se trouve dans `<head>` et contrôle le titre de l’onglet du navigateur, tandis que les titres (`<h1>…<h3>`) apparaissent dans le corps de la page.

Si vous devez également **change html titles**, le même flux de travail `lxml` s’applique :

```python
# Change the <title> tag
title_elem = doc.find(".//title")
if title_elem is not None:
    title_elem.text = f"{prefix}{title_elem.text}"
```

Désormais, le titre de la page et les titres visibles portent le même indicateur `[Updated]` — parfait pour les audits SEO où vous souhaitez une cohérence entre les métadonnées et le contenu de la page.

## Bibliothèques alternatives pour modify html with python

Bien que `lxml` soit rapide et riche en fonctionnalités, vous utilisez peut‑être déjà **BeautifulSoup** (bs4) dans votre projet. Voici la même logique dans un style plus « pythonic » :

```python
from bs4 import BeautifulSoup

with open(input_path, "r", encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")

for tag in soup.select("h1, h2, h3"):
    tag.string = f"{prefix}{tag.get_text(strip=True)}"

with open(output_path, "w", encoding="utf-8") as f:
    f.write(str(soup.prettify()))
```

Les deux bibliothèques vous permettent de **modify html with python**, choisissez donc celle qui correspond à votre pile existante. `BeautifulSoup` excelle lorsque vous avez besoin d’une analyse tolérante du balisage malformé, tandis que `lxml` offre une vitesse supérieure pour les gros lots.

## Astuces pro & pièges courants

* **L'encodage est important** – ouvrez toujours les fichiers avec `encoding="utf-8"` pour éviter les erreurs Unicode sur les caractères non‑ASCII.  
* **Avoid double‑prefixing** – si vous exécutez le script deux fois, vous obtiendrez `[Updated] [Updated] …`. Protégez‑vous en vérifiant `heading.text.startswith(prefix)`.  
* **Preserve whitespace** – l’appel `strip()` supprime les espaces superflus, gardant la sortie propre.  
* **Batch processing** – encapsulez le flux complet dans une boucle `for file in pathlib.Path("YOUR_DIRECTORY").glob("*.html"):` pour mettre à jour un dossier entier avec une seule commande.  

## Exemple complet fonctionnel : mise à jour en lot d'un répertoire

Voici un script compact qui parcourt chaque fichier `.html` d’un répertoire, préfixe les titres, met à jour le `<title>`, et écrit un nouveau fichier avec le suffixe `_updated`.

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

Exécutez‑le une fois, et chaque fichier HTML dans `YOUR_DIRECTORY` reçoit un nouveau badge `[Updated]` — aucune édition manuelle requise.

## Conclusion

Nous avons couvert **how to add prefix** aux titres HTML avec Python, démontré comment **select multiple headings**, montré comment **save modified html** en toute sécurité, et même abordé **change html titles** pour une refonte complète. En exploitant `lxml` ou `BeautifulSoup`, vous disposez désormais d’une boîte à outils solide pour **modify html with python** dans des projets réels.

Prochaines étapes ? Essayez d’ajouter des horodatages au lieu d’une balise statique, ou générez un fichier de journal des modifications listant chaque fichier que vous avez touché. Vous pourriez également intégrer ce script dans un pipeline CI afin que chaque déploiement le fasse automatiquement

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment modifier le HTML avec Aspose.HTML pour Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Comment ajouter du CSS – CSS en ligne aux documents HTML dans Aspose.HTML pour Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [Comment interroger le HTML en Java – Tutoriel complet](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
category: general
date: 2026-07-05
description: Ouvrir les liens dans un nouvel onglet avec Python – apprenez comment
  ajouter target="_blank", modifier la cible du lien, utiliser le sélecteur d’attribut
  contenant, et enregistrer le HTML modifié sans effort.
draft: false
keywords:
- open links new tab
- add target blank
- change link target
- attribute contains selector
- save modified html
language: fr
og_description: Ouvrez rapidement les liens dans un nouvel onglet. Ce tutoriel montre
  comment ajouter target="_blank", modifier la cible d’un lien et enregistrer le HTML
  modifié avec Python.
og_title: Ouvrir les liens dans un nouvel onglet – Guide de mise à jour HTML étape
  par étape
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
title: Ouvrir les liens dans un nouvel onglet – Guide complet pour mettre à jour les
  ancres HTML
url: /fr/python/general/open-links-new-tab-complete-guide-to-updating-html-anchors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ouvrir les liens dans un nouvel onglet – Guide complet pour mettre à jour les ancres HTML

Vous avez déjà eu besoin d'**ouvrir les liens dans un nouvel onglet** sur une page HTML statique mais vous ne saviez pas par où commencer ? Vous n'êtes pas seul. De nombreux développeurs rencontrent ce problème lorsqu'ils nettoient des sites hérités ou ajoutent des améliorations d'accessibilité. Dans ce tutoriel, nous allons parcourir une solution pratique qui **adds target blank**, **changes link target**, et **saves modified html** en toute sécurité — le tout avec quelques lignes de Python.

Nous couvrirons également comment utiliser un **attribute contains selector** afin de ne toucher que les ancres qui vous intéressent réellement (par exemple, chaque lien pointant vers *example.com*). À la fin, vous disposerez d'un script réutilisable que vous pourrez intégrer à n'importe quel projet, quel que soit sa taille.

## Ce que vous allez apprendre

- Charger un fichier HTML dans un objet document manipulable.  
- Sélectionner les éléments `<a>` dont l'attribut `href` contient une sous‑chaîne spécifique.  
- **Add target blank** et définir l'attribut `rel="noopener"` pour améliorer la sécurité.  
- **Save modified html** sur le disque sans perdre le formatage.  

Aucune dépendance externe au-delà de la bibliothèque standard et de **beautifulsoup4** (une petite installation). Si vous utilisez déjà un autre analyseur, les concepts se traduisent directement.

---

## Prérequis

- Python 3.8+ installé sur votre machine.  
- Familiarité de base avec HTML et Python.  
- `beautifulsoup4` package (`pip install beautifulsoup4`).  

C’est tout — aucun framework lourd requis.

---

## Étape 1 : Charger le document HTML

Première chose à faire : nous devons lire le fichier source et le transmettre à BeautifulSoup. Considérez cela comme l'ouverture d'une toile vierge où vous pouvez ajouter de nouveaux attributs.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Path to the original HTML file
html_path = Path("YOUR_DIRECTORY/links.html")

# Read the file content
with html_path.open(encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")
```

> **Pourquoi c'est important :** L'utilisation de `Path` rend le code indépendant du système d'exploitation, et `html.parser` est intégré, vous n'avez donc pas besoin de parseurs supplémentaires pour des tâches simples.

---

## Étape 2 : Utiliser un **attribute contains selector** pour trouver les bons liens

Nous ne voulons toucher que les ancres qui pointent vers *example.com*. Le sélecteur CSS `a[href*='example.com']` fait exactement cela — `*=` signifie « contient ». La méthode `select` de BeautifulSoup comprend cette syntaxe.

```python
# Find all <a> tags whose href contains 'example.com'
selector = "a[href*='example.com']"
anchor_elements = soup.select(selector)
```

> **Astuce :** Si vous avez besoin d'une correspondance insensible à la casse, passez à une petite boucle qui vérifie `if 'example.com' in a.get('href', '').lower()`.

Maintenant, `anchor_elements` contient chaque lien qui nous intéresse, prêt pour la transformation suivante.

---

## Étape 3 : Modifier la cible du lien – Ajouter target blank et sécuriser le lien

Ouvrir un lien dans un nouvel onglet est aussi simple que de définir `target="_blank"`. Cependant, les navigateurs modernes recommandent également d'ajouter `rel="noopener"` (ou `noreferrer`) pour empêcher la page nouvellement ouverte d'accéder à la fenêtre d'origine via `window.opener`. Cette petite amélioration de sécurité peut empêcher les attaques de phishing.

```python
for anchor in anchor_elements:
    # Open in a new tab
    anchor['target'] = "_blank"          # add target blank
    # Harden security
    anchor['rel'] = "noopener"           # prevent access to the opener page
```

> **Pourquoi nous utilisons une assignation directe de dictionnaire :** Cela crée automatiquement l'attribut s'il manque, et le remplace s'il existe déjà — parfait pour une opération de **change link target**.

---

## Étape 4 : Enregistrer le HTML modifié sur le disque

L'étape finale consiste à écrire le balisage mis à jour dans un nouveau fichier. Conserver l'original intact vous permet de revenir en arrière si quelque chose ne fonctionne pas.

```python
# Destination path for the updated HTML
output_path = Path("YOUR_DIRECTORY/links-updated.html")

# Write the prettified HTML (preserves indentation)
with output_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())
```

> **Ce que fait `prettify()` :** Il formate le HTML avec une belle indentation, rendant le fichier enregistré plus facile à lire et à comparer plus tard. Si vous préférez les espaces d'origine, remplacez `prettify()` par `str(soup)`.

---

## Script complet – Solution en un clic

Ci-dessous le script complet, prêt à être exécuté. Enregistrez‑le sous le nom `update_links.py` et lancez `python update_links.py` depuis votre terminal.

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

### Résultat attendu

Supposons que `links.html` contenait initialement :

```html
<a href="https://example.com/page1">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Après l'exécution du script, `links-updated.html` ressemblera à :

```html
<a href="https://example.com/page1" target="_blank" rel="noopener">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Seul le lien vers *example.com* a reçu les attributs **add target blank**, démontrant que notre **attribute contains selector** a fonctionné exactement comme prévu.

---

## Questions fréquentes & cas particuliers

### Que faire si un lien possède déjà un attribut `rel` ?

Notre boucle le remplace par `"noopener"`. Si vous devez conserver les valeurs existantes (par ex., `"nofollow"`), concaténez plutôt :

```python
existing = a.get('rel', '')
a['rel'] = f"{existing} noopener".strip()
```

### Comment gérer plusieurs domaines ?

Il suffit d'étendre la liste des sélecteurs :

```python
domains = ["example.com", "sample.org"]
selector = ",".join([f"a[href*='{d}']" for d in domains])
anchors = soup.select(selector)
```

### `prettify()` modifie-t-il la structure HTML originale ?

Il ré‑indente mais ne modifie pas l'ordre des balises ni les valeurs des attributs. Si vous devez conserver exactement les espaces d'origine, remplacez `prettify()` par `str(soup)` comme indiqué précédemment.

---

## Astuces pro pour des scripts prêts pour la production

- **Sauvegarde avant d'écraser :** Ajoutez une étape de copie (`shutil.copy`) pour garder le fichier original en sécurité.  
- **Journalisation au lieu de print :** Utilisez le module `logging` pour les projets évolutifs.  
- **Traitement par lots :** Parcourez un répertoire avec `Path.rglob("*.html")` pour mettre à jour de nombreux fichiers en une seule exécution.  

Ces ajustements transforment un simple script **open links new tab** en un utilitaire robuste pour tout flux de travail de maintenance web.

---

## Conclusion

Vous disposez maintenant d'une méthode solide et réutilisable pour **open links new tab** sur n'importe quelle collection de HTML statique. En exploitant un **attribute contains selector**, vous pouvez **change link target** précisément là où vous en avez besoin, **add target blank**, et **save modified html** sans perdre le formatage.

Testez-le sur une page d'essai, puis déployez-le sur l'ensemble de votre site. Besoin d'ajuster le sélecteur pour les PDF ou d'autres domaines ? Modifiez simplement la chaîne CSS — le reste reste identique.

N'hésitez pas à laisser un commentaire si vous rencontrez des problèmes, ou à partager comment vous avez étendu le script pour vos propres projets. Bon codage, et que toutes vos ancres s'ouvrent exactement où vous le souhaitez !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment modifier le HTML avec Aspose.HTML pour Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Comment ajouter du CSS – CSS en ligne aux documents HTML dans Aspose.HTML pour Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
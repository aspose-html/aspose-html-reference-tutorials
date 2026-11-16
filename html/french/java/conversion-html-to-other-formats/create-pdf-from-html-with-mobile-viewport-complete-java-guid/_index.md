---
category: general
date: 2026-03-18
description: Créez un PDF à partir de HTML en Java rapidement. Apprenez comment convertir
  HTML en PDF, simuler l’écran d’iPhone et définir la taille d’écran pour des PDF
  réactifs.
draft: false
keywords:
- create pdf from html
- convert html to pdf
- simulate iphone screen
- how to set screen
- how to convert html
language: fr
og_description: Créer un PDF à partir de HTML en Java. Ce guide montre comment convertir
  du HTML en PDF, simuler un écran d’iPhone et définir les dimensions de l’écran pour
  des PDF réactifs parfaits.
og_title: Créer un PDF à partir de HTML avec la viewport mobile – Tutoriel Java
tags:
- Java
- Aspose.HTML
- PDF
- Responsive Design
- Mobile Viewport
title: Créer un PDF à partir de HTML avec la viewport mobile – Guide complet Java
url: /fr/java/conversion-html-to-other-formats/create-pdf-from-html-with-mobile-viewport-complete-java-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF à partir de HTML avec un viewport mobile – Guide complet Java

Vous avez déjà eu besoin de **create PDF from HTML** mais la sortie ressemblait à une page de bureau sur un tout petit écran de téléphone ? Vous n'êtes pas le seul. Lorsque vous convertissez un site Web réactif en PDF, le viewport par défaut ignore souvent les points d'arrêt mobiles, vous laissant avec un résultat encombré.  

Bonne nouvelle ? Vous pouvez **convert HTML to PDF** tout en **simulating an iPhone screen**, entièrement depuis du code Java simple. Dans ce tutoriel, nous passerons en revue chaque étape — comment définir la taille de l'écran, comment ajuster le facteur d'échelle du dispositif, et pourquoi ces paramètres sont importants pour un PDF pixel‑perfect.

> **Astuce :** Si vous avez déjà utilisé Aspose.HTML pour des conversions simples, vous constaterez que les ajustements du viewport ne sont qu'à quelques lignes supplémentaires.

---

## Ce que vous apprendrez

* Comment **create PDF from HTML** en utilisant Aspose.HTML pour Java.  
* Le code exact pour **simulate iPhone screen** dimensions (375 × 667 px @ 2× density).  
* Où placer les options **how to set screen** dans le pipeline de conversion.  
* Pièges courants lors de la conversion de pages réactives et comment les éviter.  
* Un exemple Java complet, prêt à exécuter, que vous pouvez copier‑coller dans votre IDE.

### Prérequis

* Java 17 ou plus récent (le code se compile avec des versions antérieures, mais 17 est recommandé).  
* Bibliothèque Aspose.HTML for Java – vous pouvez récupérer le dernier JAR depuis le [site Aspose](https://products.aspose.com/html/java).  
* Un fichier HTML simple (`input.html`) que vous souhaitez convertir en PDF.  
* Familiarité de base avec Maven ou Gradle (nous montrerons un extrait Maven).

---

## Étape 1 – Ajouter Aspose.HTML à votre projet

Tout d'abord, vous avez besoin de la bibliothèque dans votre classpath. Si vous utilisez Maven, ajoutez cette dépendance dans votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- Use the latest version -->
</dependency>
```

> **Pourquoi c'est important :** Aspose.HTML gère le travail lourd — analyse du HTML, application du CSS et rasterisation de la mise en page. Sans elle, vous devriez écrire un moteur de navigateur complet vous-même, ce qui représente *beaucoup* de travail.

Si vous préférez Gradle, l'équivalent est :

```groovy
implementation 'com.aspose:aspose-html:23.12'
```

---

## Étape 2 – Préparer les options de chargement et simuler un viewport iPhone

Nous allons maintenant configurer les paramètres **how to set screen**. La classe `HtmlLoadOptions` vous permet d'indiquer à Aspose la taille et la densité de pixels que le navigateur doit simuler.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;

public class ViewportDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create load options for the HTML document
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();

        // 2️⃣ Simulate a mobile viewport (iPhone 6/7/8) – 375 × 667 pixels with retina density
        loadOptions.setScreenSize(new Size(375, 667));
        loadOptions.setDeviceScaleFactor(2.0);

        // 3️⃣ Convert the HTML file to PDF using the configured viewport
        Converter.convertDocument(
                "YOUR_DIRECTORY/input.html",          // source HTML
                "YOUR_DIRECTORY/output.pdf",          // destination PDF
                new PdfSaveOptions(),
                loadOptions);

        // 4️⃣ Notify that the conversion is complete
        System.out.println("Responsive conversion using mobile viewport.");
    }
}
```

### Pourquoi ces chiffres ?

* **375 × 667** correspond aux dimensions logiques en pixels CSS d'un iPhone 6/7/8 en mode portrait.  
* **DeviceScaleFactor = 2.0** indique au moteur de rendu que chaque pixel CSS correspond à deux pixels physiques, imitant l'affichage Retina.  

Si vous avez besoin d'un autre appareil — par exemple un iPhone 12 Pro Max — vous changeriez la taille à `428 × 926` et conserveriez le facteur d'échelle à `3.0`.

---

## Étape 3 – Exécuter la conversion et vérifier le résultat

Compilez et exécutez la classe :

```bash
mvn compile exec:java -Dexec.mainClass=ViewportDemo
```

Après que le programme se termine, ouvrez `output.pdf`. Vous devriez voir :

* Toutes les requêtes média ciblant `max-width: 375px` appliquées correctement.  
* Images rendues nettement grâce au facteur d'échelle 2×.  
* Texte qui respecte la hiérarchie des tailles de police mobiles que vous avez définie dans le CSS.

Si le PDF ressemble encore à une page de bureau, vérifiez que votre HTML utilise les balises meta réactives :

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

Sans cette balise, même un réglage de viewport parfait ne déclenchera pas la feuille de style mobile.

---

## Étape 4 – Gestion des ressources externes (Images, Polices, CSS)

Lorsque vous **convert HTML to PDF**, Aspose.HTML tente de récupérer chaque ressource liée. Si vous convertissez une page qui se trouve sur le système de fichiers local, les URL absolues (`file:///…`) fonctionnent correctement. Pour les ressources distantes, vous pourriez rencontrer :

| Problème | Pourquoi cela se produit | Solution |
|-------|----------------|-----|
| **404 errors for images** | Le HTML pointe vers une URL qui nécessite une authentification. | Utilisez `HtmlLoadOptions.setBaseUrl("file:///C:/myproject/")` pour résoudre les chemins relatifs, ou intégrez les images en Base64. |
| **Missing web fonts** | Le moteur PDF ne peut pas télécharger le fichier de police. | Téléchargez les fichiers `.woff`/`.ttf` localement et référencez‑les avec un chemin relatif. |
| **CSS not applied** | Le fichier CSS est bloqué par CORS. | Hébergez le CSS sur un serveur qui autorise les requêtes cross‑origin, ou intégrez le CSS directement dans le HTML. |

Une façon rapide de tester le chargement des ressources est d’envelopper l’appel de conversion dans un bloc try‑catch et d’imprimer le message de `Exception`. Aspose.HTML fournit des journaux détaillés qui indiquent l'URL exacte qui a échoué.

```java
try {
    Converter.convertDocument(...);
} catch (Exception ex) {
    System.err.println("Conversion failed: " + ex.getMessage());
}
```

---

## Étape 5 – Ajustements avancés (Optionnel)

### a) Modifier la taille de la page PDF

Par défaut, Aspose.HTML crée une page PDF qui correspond à la taille du viewport. Si vous préférez A4 ou Letter, ajoutez une configuration `PdfSaveOptions` :

```java
PdfSaveOptions pdfOptions = new PdfSaveOptions();
pdfOptions.setPageSize(PageSize.A4);
Converter.convertDocument("input.html", "output.pdf", pdfOptions, loadOptions);
```

### b) Ajouter un en‑tête/pied de page programmatiquement

Vous pouvez injecter un en‑tête/pied de page simple après la conversion en utilisant Aspose.PDF (une bibliothèque séparée). Le flux de travail est :

1. Convertir HTML → PDF (comme montré).  
2. Ouvrir le PDF résultant avec Aspose.PDF.  
3. Ajouter des objets `HeaderFooter` à chaque page.

```java
import com.aspose.pdf.*;

Document pdfDoc = new Document("output.pdf");
for (Page page : pdfDoc.getPages()) {
    page.addHeaderFooter(new HeaderFooter("Generated on " + LocalDate.now()));
}
pdfDoc.save("output-with-header.pdf");
```

### c) Conversion par lot

Si vous avez un dossier de fichiers HTML, bouclez dessus :

```java
Files.list(Paths.get("html_folder"))
     .filter(p -> p.toString().endsWith(".html"))
     .forEach(p -> {
         String pdfPath = p.toString().replace(".html", ".pdf");
         Converter.convertDocument(p.toString(), pdfPath, new PdfSaveOptions(), loadOptions);
     });
```

---

## Questions fréquemment posées (FAQ)

**Q : Cette méthode fonctionne‑t‑elle avec des pages très lourdes en JavaScript ?**  
R : Aspose.HTML prend en charge un sous‑ensemble de JavaScript. Les manipulations DOM simples et les changements CSS fonctionnent généralement, mais les frameworks complexes (React, Angular) peuvent nécessiter un instantané HTML statique pré‑rendu.

**Q : Et si je dois convertir une page qui utilise des règles `@media print` ?**  
R : La bibliothèque respecte automatiquement `@media print`. Cependant, si vous définissez également un viewport mobile, la feuille de style `print` peut remplacer certains styles mobiles. Testez les deux scénarios.

**Q : Puis‑je définir un DPI personnalisé pour le PDF ?**  
R : Oui. Utilisez `PdfSaveOptions.setDpi(300)` avant la conversion. Un DPI plus élevé produit des fichiers plus volumineux mais des images plus nettes.

---

## Capture d'écran du résultat attendu

Ci‑dessous se trouve une illustration de la page PDF finale (viewport mobile simulé).  
![Screenshot of PDF generated by create pdf from html demo showing iPhone‑sized layout]  

*Le texte alternatif de l'image inclut le mot‑clé principal pour le SEO.*

---

## Conclusion

Vous disposez maintenant d'un flux de travail solide, **create pdf from html**, qui respecte les points d'arrêt mobiles, simule un écran iPhone, et vous donne un contrôle total sur les dimensions de la page. En ajustant `HtmlLoadOptions`, vous pouvez répondre à “**how to set screen**” pour n'importe quel appareil, et en utilisant `Converter.convertDocument`, vous avez maîtrisé **how to convert html** en Java.

Prêt pour le prochain défi ? Essayez de combiner cette approche avec Aspose.PDF pour ajouter des filigranes, fusionner plusieurs PDFs, ou protéger le document avec un mot de passe. Et n'oubliez pas d'expérimenter avec d'autres appareils — il suffit de changer les valeurs `Size` et `DeviceScaleFactor` pour correspondre à la densité de pixels dont vous avez besoin.

Bon codage, et que vos PDFs restent toujours aussi nets sur papier qu'ils le sont sur l'écran d'un téléphone ! 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
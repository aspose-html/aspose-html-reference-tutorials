---
category: general
date: 2026-10-09
description: Lernen Sie, die verschachtelte Ressourcentiefe mit Aspose.HTML ResourceHandlingOptions
  in Python zu begrenzen. Steuern Sie max_handling_depth für eine sichere HTML-Konvertierung.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- limit nested resource depth
- Aspose.HTML ResourceHandlingOptions
- Python resource handling
- max_handling_depth
- nested HTML resources
language: de
lastmod: 2026-10-09
og_description: Begrenzen Sie die Tiefe verschachtelter Ressourcen mit Aspose.HTML ResourceHandlingOptions
  in Python. Setzen Sie max_handling_depth, um Ihren HTML‑Konvertierungs‑Workflow
  zu schützen.
og_image_alt: Screenshot showing limit nested resource depth setting in Python
og_title: Wie man die Tiefe verschachtelter Ressourcen mit Aspose.HTML in Python begrenzt
schemas:
- author: Aspose
  dateModified: '2026-10-09'
  description: Learn to limit nested resource depth using Aspose.HTML ResourceHandlingOptions
    in Python. Control max_handling_depth for safe HTML conversion.
  headline: How to limit nested resource depth with Aspose.HTML in Python
  type: TechArticle
- description: Learn to limit nested resource depth using Aspose.HTML ResourceHandlingOptions
    in Python. Control max_handling_depth for safe HTML conversion.
  name: How to limit nested resource depth with Aspose.HTML in Python
  steps:
  - name: What the setting does
    text: '- **Depth 0** – The root HTML document is processed, but no external resources
      are fetched. - **Depth 1** – Direct resources referenced by the root (e.g.,
      `<img src="...">`, `<link href="...">`) are fetched. - **Depth 2** – Resources
      referenced by the first‑level resources (e.g., CSS files that impo'
  - name: Using the options with a converter
    text: After configuring the depth limit, pass the `resource_options` object to
      the `HtmlConverter` (or any Aspose.HTML API that accepts `ResourceHandlingOptions`).
  - name: 1. Disabling depth limiting entirely
    text: Set the property to a very high number (e.g., `sys.maxsize`) or `None` if
      you want unrestricted handling. Use this only when you trust the source HTML.
  - name: 2. Handling missing resources
    text: When the depth limit stops a resource from being fetched, Aspose.HTML logs
      a warning but continues. You can capture these warnings by attaching a custom
      logger to the converter if you need audit trails.
  - name: 3. Combining with other resource options
    text: '`ResourceHandlingOptions` also offers `allow_external_resources`, `download_timeout`,
      and `max_resource_size`. Pairing a depth limit with a size limit provides a
      robust safety net.'
  - name: 4. Testing the limit
    text: Create a test HTML hierarchy with nested `<iframe>` tags or CSS `@import`
      statements to verify that your depth limit behaves as expected before deploying
      to production.
  type: HowTo
tags:
- Aspose.HTML
- Python
- HTML conversion
- Resource handling
title: Wie man die Tiefe verschachtelter Ressourcen mit Aspose.HTML in Python begrenzt
url: /de/python/general/how-to-limit-nested-resource-depth-with-aspose-html-in-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man die verschachtelte Ressourcentiefe mit Aspose.HTML in Python begrenzt

Wenn Sie die **verschachtelte Ressourcentiefe** beim Konvertieren von HTML mit Aspose.HTML begrenzen müssen, zeigt Ihnen dieser Leitfaden genau, wie Sie dies in Python tun können. Das Steuern der Eigenschaft `max_handling_depth` verhindert unkontrollierte Rekursion, wenn eine Seite tief verschachtelte Ressourcen wie Frames oder verknüpfte Stylesheets enthält.

Sie erfahren außerdem, warum das Festlegen einer Tiefenbegrenzung wichtig ist, sehen das vollständige Code‑Beispiel und entdecken häufige Fallstricke sowie bewährte Tipps. Keine externe Dokumentation ist erforderlich – alles, was Sie benötigen, finden Sie hier.

## Voraussetzungen

- Python 3.8 oder neuer installiert  
- Das `aspose.html`‑Paket (`pip install aspose-html`)  
- Grundlegende Vertrautheit mit dem Konvertierungs‑Workflow von Aspose.HTML  

Diese Punkte sind die einzigen Abhängigkeiten für die nachfolgenden Beispiele.

## Schritt 1: Importieren der **ResourceHandlingOptions**‑Klasse

Der erste Schritt besteht darin, die Klasse `ResourceHandlingOptions` in Ihr Skript zu importieren. Diese Klasse fasst alle Optionen zusammen, die beeinflussen, wie externe Ressourcen (Bilder, CSS, Skripte usw.) während der Konvertierung abgerufen und verarbeitet werden.

```python
# Step 1: Import the ResourceHandlingOptions class
from aspose.html import ResourceHandlingOptions
```

**Warum das wichtig ist:**  
`ResourceHandlingOptions` isoliert ressourcenbezogene Einstellungen von anderen Konvertierungsoptionen, sodass Sie die Handhabung verschachtelter Ressourcen fein abstimmen können, ohne das Rendering oder das Ausgabeformat zu beeinflussen.

## Schritt 2: Erstellen einer Instanz des Options‑Objekts

Instanziieren Sie `ResourceHandlingOptions`, damit Sie dessen Eigenschaften ändern können. Die Standardinstanz erlaubt unbegrenztes Verschachteln, was zu Leistungsproblemen oder sogar Stack‑Overflows bei böswillig gestalteten Seiten führen kann.

```python
# Step 2: Create an instance of the options object
resource_options = ResourceHandlingOptions()
```

**Profi‑Tipp:**  
Wenn Sie dieselbe Tiefenbegrenzung für viele Konvertierungen wiederverwenden möchten, speichern Sie das konfigurierte Objekt in einer Modul‑Variablen, um es nicht jedes Mal neu zu erstellen.

## Schritt 3: Setzen von **max_handling_depth**, um die verschachtelte Ressourcentiefe zu begrenzen

Weisen Sie der Eigenschaft `max_handling_depth` die maximale Anzahl verschachtelter Ebenen zu, die Sie zulassen möchten. In diesem Beispiel stoppen wir nach **3** Ebenen, Sie können jedoch jede passende Ganzzahl wählen.

```python
# Step 3: Limit the depth of nested resource handling (stop after 3 levels)
resource_options.max_handling_depth = 3
```

### Was die Einstellung bewirkt

- **Depth 0** – Das Root‑HTML‑Dokument wird verarbeitet, aber es werden keine externen Ressourcen abgerufen.  
- **Depth 1** – Direkt vom Root referenzierte Ressourcen (z. B. `<img src="...">`, `<link href="...">`) werden abgerufen.  
- **Depth 2** – Ressourcen, die von den Ressourcen der ersten Ebene referenziert werden (z. B. CSS‑Dateien, die andere CSS importieren), werden abgerufen.  
- **Depth 3** – Der Vorgang stoppt nach der Verarbeitung von Ressourcen der dritten Ebene. Weitere verschachtelte Verweise werden ignoriert.

Das Setzen von `max_handling_depth` schützt Ihre Anwendung vor:

| Risiko | Wie die Begrenzung hilft |
|--------|--------------------------|
| **Unendliche Rekursion** verursacht durch zirkuläre Verweise | Der Konverter stoppt nach der definierten Tiefe und bricht die Schleife ab. |
| **Exzessiver Netzwerkverkehr** wenn eine Seite Dutzende verketteter Stylesheets lädt | Nur die ersten wenigen Ebenen werden heruntergeladen, wodurch die Bandbreite reduziert wird. |
| **Speicherüberlauf** durch Laden riesiger Ressourcenbäume | Weniger Objekte werden erstellt, wodurch die Speichernutzung vorhersehbar bleibt. |

### Verwendung der Optionen mit einem Konverter

Nachdem Sie die Tiefenbegrenzung konfiguriert haben, übergeben Sie das Objekt `resource_options` an den `HtmlConverter` (oder jede Aspose.HTML‑API, die `ResourceHandlingOptions` akzeptiert).

```python
from aspose.html import HtmlConverter, SaveFormat

# Create a converter with the resource handling options
converter = HtmlConverter(resource_options)

# Convert a sample HTML file to PDF while respecting the depth limit
converter.convert("sample.html", "output.pdf", SaveFormat.PDF)

print("Conversion completed with max_handling_depth =", resource_options.max_handling_depth)
```

**Erwartete Ausgabe**

```
Conversion completed with max_handling_depth = 3
```

Wenn das Quell‑HTML Ressourcen jenseits der dritten Ebene enthält, werden diese im PDF weggelassen, und die Konvertierung wird dennoch schnell abgeschlossen.

## Randfälle und gängige Variationen

### 1. Tiefenbegrenzung vollständig deaktivieren

Setzen Sie die Eigenschaft auf eine sehr hohe Zahl (z. B. `sys.maxsize`) oder `None`, wenn Sie eine uneingeschränkte Handhabung wünschen. Verwenden Sie dies nur, wenn Sie dem Quell‑HTML vertrauen.

```python
import sys
resource_options.max_handling_depth = sys.maxsize  # effectively unlimited
```

### 2. Umgang mit fehlenden Ressourcen

Wenn die Tiefenbegrenzung das Abrufen einer Ressource verhindert, protokolliert Aspose.HTML eine Warnung, fährt jedoch fort. Sie können diese Warnungen erfassen, indem Sie dem Konverter einen benutzerdefinierten Logger hinzufügen, falls Sie Prüfpfade benötigen.

### 3. Kombination mit anderen Ressourcenoptionen

`ResourceHandlingOptions` bietet außerdem `allow_external_resources`, `download_timeout` und `max_resource_size`. Die Kombination einer Tiefenbegrenzung mit einer Größenbegrenzung bietet ein robustes Sicherheitsnetz.

```python
resource_options.allow_external_resources = True
resource_options.max_resource_size = 5 * 1024 * 1024  # 5 MiB per resource
```

### 4. Testen der Begrenzung

Erstellen Sie eine Test‑HTML‑Hierarchie mit verschachtelten `<iframe>`‑Tags oder CSS‑`@import`‑Anweisungen, um zu überprüfen, ob Ihre Tiefenbegrenzung wie erwartet funktioniert, bevor Sie sie in die Produktion überführen.

## Praktische Tipps (E‑E‑A‑T)

- **Validieren Sie Eingabe‑URLs** vor der Konvertierung, um unnötige Netzwerkaufrufe zu vermeiden.  
- **Protokollieren Sie die tatsächlich erreichte Tiefe** (`converter.handling_depth_reached`) zur Überwachung.  
- **Verwenden Sie dieselben `ResourceHandlingOptions`** über mehrere Konvertierungen hinweg, um die Konfiguration konsistent zu halten.  
- **Profilieren Sie die Leistung** beim Ändern der Tiefe; eine niedrigere Begrenzung beschleunigt in der Regel die Konvertierung, kann jedoch benötigte Assets weglassen.  

## Fazit

Sie wissen jetzt, wie Sie die **verschachtelte Ressourcentiefe** bei der Arbeit mit Aspose.HTML in Python begrenzen können, indem Sie die Eigenschaft `max_handling_depth` von `ResourceHandlingOptions` konfigurieren. Diese einzelne Einstellung schützt Ihre Konvertierungspipeline vor unkontrollierter Rekursion, übermäßigem Netzwerkverkehr und Speicherspitzen, während Sie eine feinkörnige Kontrolle darüber erhalten, wie tief Ressourcenbäume verarbeitet werden.

Bereit, mehr zu entdecken? Versuchen Sie, die Tiefenbegrenzung mit `max_resource_size` zu kombinieren, um einen vollständig gehärteten HTML‑zu‑PDF‑Konvertierungs‑Workflow zu erstellen, oder lesen Sie unseren Leitfaden zur **Aspose.HTML‑Ressourcenverwaltung** für tiefere Einblicke in `allow_external_resources` und das Timeout‑Management.

--- 

*Bild, das die Einstellung zur Begrenzung der verschachtelten Ressourcentiefe (optional) veranschaulicht:*  
![Screenshot, der die Einstellung zur Begrenzung der verschachtelten Ressourcentiefe in Python zeigt](placeholder.png "Begrenzung der verschachtelten Ressourcentiefe")

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu beherrschen und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Benutzerdefinierter Ressourcen‑Handler in Aspose HTML – Leitfaden zum Speichern in einen Stream](/html/english/net/advanced-features/custom-resource-handler-in-aspose-html-save-to-stream-guide/)
- [Wie man HTML in C# speichert – Vollständiger Leitfaden mit benutzerdefiniertem Ressourcen‑Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Nachrichten‑Handling und Netzwerk in Aspose.HTML für Java](/html/english/java/message-handling-networking/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
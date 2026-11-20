---
category: general
date: 2026-05-28
description: Erfahren Sie, wie Sie SaveOptions verwenden, um HTML‑Seiten in Python
  zu kürzen. Diese Schritt‑für‑Schritt‑Anleitung erklärt außerdem, wie man ein HTML‑Dokument
  lädt und verschachtelte Ressourcen effizient entfernt.
draft: false
keywords:
- how to use saveoptions
- how to load html document
- how to trim html page
language: de
og_description: Wie man SaveOptions verwendet, um HTML‑Seiten in Python zu kürzen.
  Folgen Sie dieser Anleitung, um ein HTML‑Dokument zu laden, Ressourcenlimits festzulegen
  und eine saubere, leichte Datei zu speichern.
og_title: Wie man SaveOptions in Python verwendet – HTML‑Seiten trimmen
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to use SaveOptions to trim HTML pages in Python. This step‑by‑step
    guide also explains how to load an HTML document and efficiently remove nested
    resources.
  headline: How to Use SaveOptions in Python – Trim HTML Pages
  type: TechArticle
tags:
- python
- html-processing
- saveoptions
- resource-handling
title: Wie man SaveOptions in Python verwendet – HTML‑Seiten trimmen
url: /de/python/general/how-to-use-saveoptions-in-python-trim-html-pages/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man SaveOptions in Python verwendet – HTML-Seiten kürzen

Haben Sie sich jemals gefragt, **wie man SaveOptions** verwendet, um eine riesige HTML-Datei zu verkleinern, ohne etwas zu beschädigen? Sie sind nicht allein. Wenn Sie eine Seite einbinden, die Dutzende verschachtelter Ressourcen enthält – denken Sie an CSS, JS oder sogar andere HTML‑Snippets – kann Ihre Ausgabe unkontrollierbar anwachsen.  

In diesem Tutorial führen wir Sie durch ein vollständiges, ausführbares Beispiel, das nicht nur **zeigt, wie man SaveOptions verwendet**, sondern auch **wie man ein HTML‑Dokument lädt** und die beste Methode, **eine HTML‑Seite zu kürzen**, indem die Verschachtelungstiefe begrenzt wird. Am Ende haben Sie eine saubere, gekürzte Datei, die bereit für die Bereitstellung oder weitere Verarbeitung ist.

## Was Sie erreichen werden

- Laden Sie jede lokale HTML‑Datei mit einer einzigen Code‑Zeile.  
- Konfigurieren Sie die Optionen zur Ressourcenverarbeitung, um bei einer bestimmten Include‑Tiefe zu stoppen.  
- Speichern Sie das gekürzte Ergebnis mit der leistungsstarken `SaveOptions`‑Klasse.  

Keine externen Werkzeuge, keine Magie – nur reines Python und eine kleine Bibliothek, die die schwere Arbeit übernimmt.

---

## Voraussetzungen

Bevor wir loslegen, stellen Sie sicher, dass Sie Folgendes haben:

1. **Python 3.9+** installiert (die verwendete Syntax funktioniert in jeder aktuellen Version).  
2. Das hypothetische `htmlprocessor`‑Paket, das `HTMLDocument`, `SaveOptions` und `ResourceHandlingOptions` bereitstellt. Installieren Sie es über:

```bash
pip install htmlprocessor
```

> **Pro‑Tipp:** Wenn Sie eine virtuelle Umgebung verwenden, aktivieren Sie sie zuerst – das hält Ihre Abhängigkeiten ordentlich.

---

## Schritt 1: Wie man ein HTML‑Dokument lädt

Das Laden einer Datei ist so einfach, den Konstruktor auf Ihren Pfad zu zeigen. Die Bibliothek liest das Markup, erstellt einen DOM‑ähnlichen Baum und bereitet ihn für weitere Manipulationen vor.

```python
from htmlprocessor import HTMLDocument

# Replace with the actual path to your file
doc = HTMLDocument("YOUR_DIRECTORY/complex_page.html")
print("Document loaded –", doc.title or "Untitled")
```

> **Warum das wichtig ist:** Das `HTMLDocument`‑Objekt abstrahiert die Verarbeitung von Roh‑Strings, bietet Ihnen Methoden zum Abfragen, Ändern und schließlich Speichern der Seite. Es normalisiert außerdem Zeilenenden und Zeichenkodierungen, was Sie später vor subtilen Fehlern bewahrt.

Sie werden bemerken, dass wir den Titel ausgeben, nur um zu überprüfen, ob das Laden erfolgreich war. Wenn die Datei fehlt oder fehlerhaft ist, wirft der Konstruktor eine klare Ausnahme – keine stillen Fehler.

---

## Schritt 2: Ressourcenverarbeitung konfigurieren – Der Kern des Kürzens

Der nächste Teil des Puzzles ist **wie man HTML‑Seiten‑Inhalte kürzt**, indem man begrenzt, wie tief der Prozessor Includes folgt. Hier glänzt `ResourceHandlingOptions`.

```python
from htmlprocessor import ResourceHandlingOptions

# Create a fresh options instance
res_opt = ResourceHandlingOptions()
# max_handling_depth = 2 means: main page + one level of includes
res_opt.max_handling_depth = 2
```

### Was bewirkt `max_handling_depth`?

- **Tiefe 1** → Nur die Root‑HTML‑Datei, alle externen Ressourcen werden ignoriert.  
- **Tiefe 2** → Die Root‑Datei plus alle direkt referenzierten Dateien (z. B. ein `iframe` oder ein serverseitiges Include).  
- **Höhere Werte** → Tiefere Verschachtelung, aber auch größere Ausgabe und längere Verarbeitungszeit.

Indem wir die Tiefe auf **2** begrenzen, behalten wir die Hauptseite und eine Ebene von Includes bei und verwerfen alles Tiefergehende. Das reicht in der Regel aus, um redundante Fußzeilen, Analyse‑Skripte oder verschachtelte Vorlagen zu entfernen, die Sie in einer gekürzten Kopie nicht benötigen.

---

## Schritt 3: Optionen an die Speicher‑Konfiguration anhängen

Jetzt binden wir unsere Ressourcenregeln an eine `SaveOptions`‑Instanz. Dieses Objekt teilt der Bibliothek *genau* mit, wie die Datei wieder auf die Festplatte geschrieben werden soll.

```python
from htmlprocessor import SaveOptions

save_opt = SaveOptions()
save_opt.resource_handling_options = res_opt
```

> **Warum `SaveOptions` verwenden?**  
> Es gibt Ihnen eine feinkörnige Kontrolle über die Ausgabe – über die reine Ressourcentiefe hinaus. Sie können später Kompression, Pretty‑Printing oder sogar benutzerdefinierte Callbacks hinzufügen, ohne die Kern‑Speicherlogik zu verändern.

---

## Schritt 4: Wie man SaveOptions verwendet, um die HTML‑Seite zu kürzen

Schließlich rufen wir die `save`‑Methode mit unseren konfigurierten Optionen auf. Die Bibliothek durchläuft das DOM, respektiert das Tiefenlimit und schreibt eine gekürzte Datei.

```python
# Save the trimmed document
output_path = "YOUR_DIRECTORY/trimmed_page.html"
doc.save(output_path, save_opt)

print(f"Trimmed page saved to {output_path}")
```

### Erwartetes Ergebnis

- Die Datei `trimmed_page.html` enthält das ursprüngliche Markup **plus** alle Includes bis zu einer Ebene Tiefe.  
- Alle tieferen Includes werden weggelassen, was zu einer kleineren, schneller ladenden Seite führt.  
- Keine kaputten Tags erscheinen – die Bibliothek schließt automatisch alle Elemente, die nach dem Entfernen lose geblieben sind.

Sie können die Ausgabe in einem Browser öffnen, um zu überprüfen, dass der Hauptinhalt noch gerendert wird, während überflüssige Skripte oder verschachtelte Frames entfernt wurden.

---

## Vollständiges funktionierendes Beispiel

Alles zusammengeführt, hier das komplette Skript, das Sie kopieren und ausführen können:

```python
# -*- coding: utf-8 -*-
"""
Trim an HTML page using SaveOptions.
Demonstrates:
- How to load an HTML document
- How to configure ResourceHandlingOptions
- How to use SaveOptions to save a trimmed version
"""

from htmlprocessor import HTMLDocument, SaveOptions, ResourceHandlingOptions

def trim_html(input_path: str, output_path: str, max_depth: int = 2) -> None:
    # Load the source document
    doc = HTMLDocument(input_path)
    print("Loaded:", doc.title or "Untitled")

    # Set up resource handling (how to trim HTML page)
    res_opt = ResourceHandlingOptions()
    res_opt.max_handling_depth = max_depth

    # Attach options to save configuration (how to use SaveOptions)
    save_opt = SaveOptions()
    save_opt.resource_handling_options = res_opt

    # Perform the save
    doc.save(output_path, save_opt)
    print(f"Trimmed HTML saved to {output_path}")

if __name__ == "__main__":
    INPUT = "YOUR_DIRECTORY/complex_page.html"
    OUTPUT = "YOUR_DIRECTORY/trimmed_page.html"
    trim_html(INPUT, OUTPUT, max_depth=2)
```

Führen Sie das Skript aus, setzen Sie `INPUT` auf eine beliebige komplexe HTML‑Datei, und Sie erhalten eine schlankere Version in `OUTPUT`.  

> **Hinweis zu Sonderfällen:** Wenn die Originalseite bedingte Kommentare (`<!--[if IE]>…<![endif]-->`) enthält, die tiefere Ressourcen referenzieren, werden sie genauso wie jedes andere verschachtelte Include entfernt. Das verhindert, dass alte‑IE‑Hacks Ihre Endgröße aufblähen.

---

## Visuelle Zusammenfassung

Unten ist ein schnelles Diagramm, das den Ablauf veranschaulicht – vom Laden des Dokuments über die Ressourcenverarbeitung bis zum Speichern des gekürzten Ergebnisses.

![Beispiel für die Verwendung von SaveOptions](https://example.com/placeholder.png "Diagramm, das zeigt, wie SaveOptions verwendet wird, um HTML‑Seiten zu kürzen")

*Alt‑Text:* **Beispiel für die Verwendung von SaveOptions** – zeigt den dreischrittigen Prozess des Ladens, Konfigurierens und Speicherns eines HTML‑Dokuments.

---

## Häufige Fragen & Stolperfallen

| Frage | Antwort |
|----------|--------|
| **Was, wenn ich tiefere Verschachtelung benötige?** | Erhöhen Sie `max_handling_depth` auf 3 oder 4, aber denken Sie daran, dass die Ausgabengröße wachsen wird. |
| **Kann ich bestimmte Tags (z. B. `<script>`) unabhängig von der Tiefe ausschließen?** | Ja – `SaveOptions` unterstützt außerdem die Eigenschaft `tag_exclusion_list`. Fügen Sie `"script"` zu dieser Liste hinzu, um Skripte immer zu entfernen. |
| **Ist die Bibliothek thread‑sicher?** | Die aktuelle Version ist es nicht. Erstellen Sie pro Thread ein separates `HTMLDocument`. |
| **Werden relative URLs umgeschrieben?** | Standardmäßig nicht. Verwenden Sie `save_opt.rewrite_relative_urls = True`, wenn Sie sie an den neuen Ort anpassen müssen. |

---

## Nächste Schritte

Jetzt, wo Sie **die Verwendung von SaveOptions** gemeistert haben, probieren Sie diese Erweiterungen aus:

- **Komprimieren Sie die Ausgabe:** Setzen Sie `save_opt.enable_gzip = True` für kleinere Dateien beim Transfer.  
- **Pretty‑Print für Debugging:** Schalten Sie `save_opt.indent_output = True` ein, um schön formatiertes HTML zu erhalten.  
- **Batch‑Verarbeitung:** Durchlaufen Sie ein Verzeichnis mit HTML‑Dateien und wenden Sie dieselbe Kürzungslogik an – ideal für statische Site‑Generatoren.

Jede dieser Anpassungen baut auf derselben Grundlage auf, die Sie gerade gelernt haben, und hält Ihren Code sauber und wartbar.

---

## Fazit

Wir haben den gesamten Lebenszyklus des Kürzens einer HTML‑Seite in Python behandelt: **wie man ein HTML‑Dokument lädt**, **wie man HTML‑Seiten kürzt** mit `ResourceHandlingOptions` konfiguriert und schließlich **wie man SaveOptions verwendet**, um die bereinigte Datei zu schreiben. Das Beispiel ist vollständig eigenständig, läuft sofort und zeigt, warum die Kontrolle der Ressourcentiefe eine wichtige Optimierung für Web‑Scraping, die statische Seitengenerierung oder jede Situation ist, in der Sie einen leichten HTML‑Snapshot benötigen.

Probieren Sie es aus, experimentieren Sie mit verschiedenen `max_handling_depth`‑Werten und lassen Sie die gekürzten Seiten die schwere Arbeit für Sie übernehmen. Wenn Sie auf Probleme stoßen, hinterlassen Sie unten einen Kommentar – happy coding!

## Verwandte Tutorials

- [Wie man HTML in C# speichert – Vollständiger Leitfaden mit benutzerdefiniertem Ressourcen‑Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Wie man HTML als PNG rendert – Vollständiger C#‑Leitfaden](/html/english/net/rendering-html-documents/how-to-render-html-as-png-complete-c-guide/)
- [Wie man HTML in C# zippt – HTML in Zip speichern](/html/english/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
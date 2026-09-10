---
date: 2026-02-10
description: Erfahren Sie, wie Sie Aspose verwenden, um defekte Links in Java zu behandeln,
  HTML in PNG zu konvertieren und ein HTML‑Dokument in Java mit Aspose.HTML für Java
  zu laden.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: HTML mit Aspose.HTML Message Handlers in Java in PNG konvertieren
url: /de/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML in PNG konvertieren mit Aspose.HTML Message Handlers in Java

## Einführung
In diesem Tutorial erfahren Sie **wie man HTML in PNG** konvertiert und dabei fehlende Ressourcen elegant behandelt, mithilfe von Aspose.HTML für Java. Wir gehen Schritt für Schritt durch das Erstellen einer kleinen HTML‑Seite, die auf ein nicht vorhandenes Bild verweist, das Einbinden eines **benutzerdefinierten Message Handlers**, um **Netzwerkanfragen abzufangen**, das Konfigurieren des **Network Service**, das Laden des Dokuments und schließlich die Durchführung der **HTML‑zu‑Bild‑Konvertierung**. Am Ende haben Sie ein solides Muster sowohl für **handle broken links java** als auch für hochwertige PNG‑Ausgaben – ideal für Berichte, Thumbnails oder E‑Mail‑Vorschauen.

## Schnelle Antworten
- **Was macht ein Message Handler?** Er fängt Netzwerkoperationen (wie Bildanfragen) ab und ermöglicht es Ihnen, auf Statuscodes wie 404 zu reagieren.  
- **Kann Aspose.HTML HTML in PNG konvertieren?** Ja – `Converter.convertHTML` führt die Konvertierung in einem einzigen Aufruf aus.  
- **Benötige ich eine Lizenz für dieses Beispiel?** Eine temporäre Lizenz entfernt Evaluationsbeschränkungen; für den Produktionseinsatz ist eine permanente Lizenz erforderlich.  
- **Welche Java‑Version funktioniert?** Jede JDK 8+ (das Beispiel läuft auf JDK 11).  
- **Kann ich den Network Service konfigurieren?** Absolut – verwenden Sie `configuration.getService(INetworkService.class)`, um Ihren Handler hinzuzufügen.

## Voraussetzungen
Bevor wir beginnen, stellen Sie sicher, dass Sie Folgendes bereit haben:

1. **Java Development Kit (JDK)** – herunterladen von der [Oracle-Website](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java** – die Bibliothek beziehen Sie von der [Aspose Releases‑Seite](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse oder NetBeans funktionieren.  
4. **Grundlegende Java‑Kenntnisse** – Sie sollten mit Klassen, try‑with‑resources und Ausnahmebehandlung vertraut sein.  
5. **Temporäre Lizenz** – wenn Sie eine Testversion verwenden, holen Sie sich eine [temporäre Lizenz](https://purchase.aspose.com/temporary-license/), um Wasserzeichen zu vermeiden.

## Pakete importieren
Zuerst importieren wir die Java‑I/O‑Klasse, die wir für die Dateiverarbeitung benötigen. Die restlichen Aspose‑Klassen werden später mit vollqualifizierten Namen referenziert, wodurch die Importliste übersichtlich bleibt.

```java
import java.io.IOException;
```

## Schritt 1: HTML‑Code vorbereiten
Wir erstellen ein minimales HTML‑Snippet, das absichtlich auf ein fehlendes Bild verweist. Dies löst unseren Handler aus, wenn die Engine versucht, die Ressource abzurufen.

```java
String code = "<img src='missing.jpg'>";
```

## Schritt 2: HTML‑Code in eine Datei schreiben
Als Nächstes speichern wir das Snippet in *document.html*. Die Verwendung eines try‑with‑resources‑Blocks stellt sicher, dass der `FileWriter` ordnungsgemäß geschlossen wird.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Schritt 3: Einen benutzerdefinierten Message Handler schreiben
Jetzt erstellen wir einen **benutzerdefinierten Message Handler**, der den HTTP‑Status jeder Netzwerkanfrage prüft. Wenn die Antwort nicht `200` ist, protokollieren wir eine freundliche Warnung. Beachten Sie den Aufruf von `invoke(context);` am Ende – dieser leitet die Anfrage an den nächsten Handler in der Kette weiter und verhindert Rekursion.

```java
com.aspose.html.net.MessageHandler handler = new com.aspose.html.net.MessageHandler() {
    @Override
    public void invoke(com.aspose.html.net.INetworkOperationContext context) {
        if (context.getResponse().getStatusCode() != 200) {
            System.out.println(String.format("File '%s' Not Found", context.getRequest().getRequestUri().toString()));
        }
        invoke(context);
    }
};
```

## Schritt 4: Netzwerk‑Service konfigurieren
Damit Aspose.HTML unseren Handler kennt, holen wir den **Network Service** aus einer `Configuration`‑Instanz und fügen den Handler zu seiner Sammlung hinzu. Dies ist der Schritt, in dem wir den **Network Service** für benutzerdefiniertes Verhalten **konfigurieren**.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Schritt 5: HTML‑Dokument laden
Mit der fertigen Konfiguration laden wir *document.html*. Die Engine verwendet nun unseren Network Service, sodass die Anfrage nach dem fehlenden Bild vom gerade hinzugefügten Handler abgefangen wird.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
try {
    // Additional operations will go here
} finally {
    if (document != null) {
        document.dispose();
    }
}
```

## Schritt 6: HTML in PNG konvertieren
Hier ist das Kernstück des **HTML‑zu‑Bild‑Konvertierungs**‑Prozesses. Die Methode `Converter.convertHTML` nimmt das geladene `HTMLDocument`, optionale `ImageSaveOptions` (mit denen Sie DPI oder Qualität anpassen können) und den Ausgabedateinamen.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## Schritt 7: Ressourcen bereinigen
Gute Java‑Praxis verlangt, dass wir alle nativen Ressourcen freigeben. Der `finally`‑Block stellt sicher, dass die `Configuration` selbst bei einer Ausnahme freigegeben wird.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Warum Message Handler verwenden?
Message Handler geben Ihnen **feinkörnige Kontrolle** über jede Netzwerkanfrage – egal ob Bild, CSS, JavaScript oder Schriftdatei. Anstatt die Bibliothek stillschweigend fehlschlagen zu lassen, können Sie fehlende Assets protokollieren, Fallback‑Inhalte bereitstellen oder die Anfrage sogar erneut versuchen. Das macht Ihre HTML‑Verarbeitungspipeline **robust**, **produktionsreif** und leichter zu debuggen.

## Häufige Probleme und Lösungen
- **Handler‑Rekursion** – Rufen Sie `invoke(context);` nur einmal auf, um Endlosschleifen zu vermeiden.  
- **Fehlende Lizenz** – Ohne gültige Lizenz enthält das ausgegebene PNG ein Wasserzeichen.  
- **Falsche Dateipfade** – Verwenden Sie absolute Pfade oder setzen Sie das Arbeitsverzeichnis korrekt, wenn Sie `document.html` laden.  
- **Nicht unterstützte Ressourcentypen** – Stellen Sie sicher, dass die Ressource, die Sie abfangen möchten (Bild, CSS usw.), tatsächlich von der HTML‑Engine angefordert wird.

## Häufig gestellte Fragen

**Q: Kann ich mehrere Message Handler verketten?**  
A: Ja, Sie können mehrere Handler zur `network.getMessageHandlers()`‑Sammlung hinzufügen; sie werden in der Reihenfolge ihrer Hinzufügung ausgeführt.

**Q: Funktioniert der Handler auch für CSS‑ oder Skript‑Ressourcen?**  
A: Absolut – jede Netzwerkanfrage, die von der HTML‑Engine gestellt wird (Bilder, CSS, JS, Schriften), läuft über den Handler.

**Q: Wie ändere ich die HTTP‑Anfrage, bevor sie gesendet wird?**  
A: Implementieren Sie einen Handler, der `context.getRequest()` modifiziert, bevor `invoke(context)` aufgerufen wird.

**Q: Gibt es eine Möglichkeit, die Warnung für bestimmte URLs zu unterdrücken?**  
A: Untersuchen Sie im Handler `context.getRequest().getRequestUri()` und überspringen Sie das Protokoll bedingt.

**Q: Welche Version von Aspose.HTML wird für diese APIs benötigt?**  
A: Der Code funktioniert mit Aspose.HTML für Java 22.10 und später.

## Fazit
Sie haben nun ein vollständiges End‑zu‑Ende‑Beispiel, **wie man HTML in PNG** konvertiert, während ein **benutzerdefinierter Message Handler** **Netzwerkanfragen abfängt** und **handle broken links java** behandelt. Durch das Konfigurieren des Network Service, das Laden des Dokuments und das Aufrufen des Converters können Sie zuverlässig PNG‑Thumbnails oder Vollseiten‑Screenshots in jeder Java‑Anwendung erzeugen.

---

**Zuletzt aktualisiert:** 2026-02-10  
**Getestet mit:** Aspose.HTML for Java 24.11  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
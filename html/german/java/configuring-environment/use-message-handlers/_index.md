---
date: 2026-05-04
description: Erfahren Sie, wie Sie HTML-zu-PNG-Konvertierung durchführen, Netzwerk‑Anfragen
  in Java abfangen und defekte Links in Java behandeln, indem Sie Aspose.HTML für
  Java verwenden.
keywords:
- html to png conversion
- intercept network requests java
- html to image conversion
- load html document java
- handle broken links java
linktitle: Verwenden von Nachrichten‑Handlern in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: HTML-zu-PNG-Konvertierung mit Aspose.HTML-Nachrichten-Handlern in Java
url: /de/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML-zu-PNG-Konvertierung mit Aspose.HTML Message Handlers in Java

## Einführung in die HTML-zu-PNG-Konvertierung
In diesem Tutorial erfahren Sie **wie man HTML in PNG konvertiert**, während fehlende Ressourcen elegant mit Aspose.HTML für Java behandelt werden. Wir führen Sie durch das Erstellen einer kleinen HTML-Seite, die auf ein nicht vorhandenes Bild verweist, das Einbinden eines **benutzerdefinierten Message Handlers**, um **Netzwerkanfragen abzufangen**, das Konfigurieren des **Netzwerkdienstes**, das Laden des Dokuments und schließlich die Durchführung der **HTML‑zu‑Bild-Konvertierung**. Am Ende haben Sie ein solides Muster sowohl für **handle broken links java** als auch für hochwertige PNG‑Ausgaben – perfekt für Berichte, Thumbnails oder E‑Mail‑Vorschauen.

## Schnelle Antworten
- **Was macht ein Message Handler?** Er fängt Netzwerkoperationen (wie Bildanfragen) ab und ermöglicht es Ihnen, auf Statuscodes wie 404 zu reagieren.  
- **Kann Aspose.HTML HTML in PNG konvertieren?** Ja—`Converter.convertHTML` führt die Konvertierung in einem einzigen Aufruf aus.  
- **Benötige ich eine Lizenz für dieses Beispiel?** Eine temporäre Lizenz entfernt Evaluationsbeschränkungen; für den Produktionseinsatz ist eine permanente Lizenz erforderlich.  
- **Welche Java-Version funktioniert?** Jede JDK 8+ (das Beispiel läuft auf JDK 11).  
- **Kann ich den Netzwerkdienst konfigurieren?** Absolut—verwenden Sie `configuration.getService(INetworkService.class)`, um Ihren Handler hinzuzufügen.

## Was ist HTML-zu-PNG-Konvertierung?
Die HTML‑zu‑PNG-Konvertierung rendert eine Webseite (oder einen HTML‑Abschnitt) in ein Rasterbild. Dies ist nützlich, wenn Sie statische Vorschauen dynamischer Inhalte benötigen, Thumbnails für E‑Mail‑Newsletter erzeugen oder Webseiten als Bilder archivieren.

## Warum Message Handlers zum Abfangen von Netzwerk-Anfragen in Java verwenden?
Message Handlers geben Ihnen **feinkörnige Kontrolle** über jede Netzwerkanfrage – sei es ein Bild, CSS, JavaScript oder eine Schriftdatei. Durch das Abfangen dieser Anfragen können Sie **fehlende Ressourcen protokollieren**, Fallback‑Inhalte bereitstellen oder sogar fehlgeschlagene Downloads erneut versuchen, wodurch Ihre HTML‑Verarbeitungspipeline **robust** und **produktionsreif** wird.

## Voraussetzungen
Bevor wir beginnen, stellen Sie sicher, dass Sie Folgendes bereit haben:

1. **Java Development Kit (JDK)** – herunterladen von der [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java** – die Bibliothek von der [Aspose releases page](https://releases.aspose.com/html/java/) beziehen.  
3. **IDE** – IntelliJ IDEA, Eclipse oder NetBeans funktionieren einwandfrei.  
4. **Grundlegende Java‑Kenntnisse** – Sie sollten mit Klassen, try‑with‑resources und Ausnahmebehandlung vertraut sein.  
5. **Temporäre Lizenz** – wenn Sie eine Testversion nutzen, holen Sie sich eine [temporary license](https://purchase.aspose.com/temporary-license/), um Wasserzeichen zu vermeiden.

## Pakete importieren
Zuerst importieren wir die Java‑I/O‑Klasse, die wir für die Dateiverarbeitung benötigen. Die übrigen Aspose‑Klassen werden später mit vollqualifizierten Namen referenziert, wodurch die Import‑Liste übersichtlich bleibt.

```java
import java.io.IOException;
```

## Schritt 1: HTML-Code vorbereiten
Wir erstellen ein minimales HTML‑Snippet, das absichtlich ein fehlendes Bild referenziert. Dies löst unseren Handler aus, wenn die Engine versucht, die Ressource abzurufen.

```java
String code = "<img src='missing.jpg'>";
```

## Schritt 2: HTML-Code in eine Datei schreiben
Als Nächstes speichern wir das Snippet in *document.html*. Durch die Verwendung eines try‑with‑resources‑Blocks wird sichergestellt, dass der `FileWriter` ordnungsgemäß geschlossen wird.

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

## Schritt 4: Netzwerkdienst konfigurieren
Damit Aspose.HTML unseren Handler kennt, holen wir den **Network Service** aus einer `Configuration`‑Instanz und fügen den Handler zu seiner Sammlung hinzu. Dies ist der Schritt, in dem wir den **Network Service** für benutzerdefiniertes Verhalten **konfigurieren**.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Schritt 5: HTML-Dokument laden
Mit der fertigen Konfiguration laden wir *document.html*. Die Engine nutzt nun unseren Network Service, sodass die Anfrage nach dem fehlenden Bild vom gerade hinzugefügten Handler abgefangen wird.

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
Gute Java‑Praxis verlangt, dass wir alle nativen Ressourcen freigeben. Der `finally`‑Block stellt sicher, dass die `Configuration` freigegeben wird, selbst wenn eine Ausnahme auftritt.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Häufige Probleme und Lösungen
- **Handler recursion** – Rufen Sie `invoke(context);` nur einmal auf, um Endlosschleifen zu vermeiden.  
- **Missing license** – Ohne eine gültige Lizenz enthält das ausgegebene PNG ein Wasserzeichen.  
- **Incorrect file paths** – Verwenden Sie absolute Pfade oder setzen Sie das Arbeitsverzeichnis korrekt, wenn Sie `document.html` laden.  
- **Unsupported resource types** – Stellen Sie sicher, dass die Ressource, die Sie abfangen möchten (Bild, CSS usw.), tatsächlich von der HTML‑Engine angefordert wird.

## Häufig gestellte Fragen

**Q: Kann ich mehrere Message Handlers verketten?**  
A: Ja, Sie können mehrere Handler zur `network.getMessageHandlers()`‑Sammlung hinzufügen; sie werden in der Reihenfolge ihrer Hinzufügung ausgeführt.

**Q: Funktioniert der Handler auch für CSS‑ oder Skript‑Ressourcen?**  
A: Absolut—jede Netzwerkanfrage, die von der HTML‑Engine gestellt wird (Bilder, CSS, JS, Schriften), läuft über den Handler.

**Q: Wie ändere ich die HTTP‑Anfrage, bevor sie gesendet wird?**  
A: Implementieren Sie einen Handler, der `context.getRequest()` modifiziert, bevor `invoke(context)` aufgerufen wird.

**Q: Gibt es eine Möglichkeit, die Warnung für bestimmte URLs zu unterdrücken?**  
A: Im Handler können Sie `context.getRequest().getRequestUri()` prüfen und das Protokoll bedingt überspringen.

**Q: Welche Version von Aspose.HTML wird für diese APIs benötigt?**  
A: Der Code funktioniert mit Aspose.HTML für Java 22.10 und später.

**Zuletzt aktualisiert:** 2026-05-04  
**Getestet mit:** Aspose.HTML for Java 24.11  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
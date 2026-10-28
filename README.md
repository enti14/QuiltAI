# QuiltAI

Ein ruhiger, persönlicher KI-Workspace für GitHub Pages. Ohne Installation, Build-Schritt oder eigenen Server. Oberfläche auf Deutsch, responsiv für Desktop und Smartphone.

## Auf GitHub Pages starten

1. ZIP entpacken und den gesamten Inhalt in ein GitHub-Repository hochladen. `index.html` muss direkt im Stammverzeichnis liegen, nicht in einem weiteren Unterordner.
2. GitHub Pages für dieses Repository aktivieren und den Branch mit den Dateien sowie das Stammverzeichnis `/` als Quelle auswählen.
3. Die bereitgestellte Pages-Adresse öffnen.
4. Unter **Einstellungen** deinen Anbieter, API-Key und ein für deinen Account verfügbares Modell eintragen. Speichern und chatten.

Keine Zugangsdaten in das Repository schreiben. Jeder Besucher verwendet seinen eigenen API-Key.

## Enthalten

- Streaming-Chats mit Abbrechen, mehreren Unterhaltungen und lokalem Verlauf
- Google Gemini, OpenAI, Anthropic Claude, OpenRouter, api.airforce und eigene kompatible APIs
- Getrennte API-Schlüssel und Einstellungen pro Anbieter, schneller Anbieterwechsel im Chat
- Modelllisten direkt vom jeweiligen Anbieter laden oder Modell-IDs manuell eintragen
- Frei einstellbare Modell-IDs und Systemanweisungen
- Code Canvas mit HTML-, CSS- und JavaScript-Editor, isolierter Live-Vorschau und Website-Download
- Textdatei-Anhänge bis 250 KB (Inhalt wird mit der nächsten Nachricht an den KI-Anbieter gesendet)
- Kopieren von Nachrichten und Export als Markdown
- Lokaler Rechner, Text-Analyse und JSON-Formatierung
- Eigene GET-API-Plugins mit JSON-Antworten und dem Platzhalter `{query}`
- Übernahme von Tool-Ergebnissen als Entwurf in den Chat
- Tastatur: Enter sendet, Shift+Enter fügt eine neue Zeile ein; Strg/Cmd+K startet einen neuen Chat

## Anbieter einrichten

| Anbieter | Voreingestellte Basis-URL | Format |
| --- | --- | --- |
| Google Gemini | `https://generativelanguage.googleapis.com/v1beta` | Gemini `streamGenerateContent` |
| OpenAI | `https://api.openai.com/v1` | Chat Completions |
| Anthropic Claude | `https://api.anthropic.com/v1` | Messages API |
| OpenRouter | `https://openrouter.ai/api/v1` | Chat Completions |
| api.airforce | `https://api.airforce/v1` | Chat Completions |

1. Einstellungen öffnen und den Anbieter wählen.
2. Den API-Key **dieses Anbieters** eintragen.
3. Bei Bedarf „Modelle vom Anbieter laden“ wählen. Falls der Anbieter die Liste nicht freigibt, Modell-IDs manuell mit Komma trennen.
4. Speichern. Der Anbieter lässt sich anschließend direkt neben der Modellwahl im Chat wechseln.

Schlüssel, Modelllisten und Basis-URLs werden getrennt pro Anbieter verwaltet. Im Einstellungsdialog können mehrere Anbieter nacheinander konfiguriert und zusammen gespeichert werden. Schließen ohne Speichern verwirft die Änderungen. Der Systemprompt gilt gemeinsam für alle Anbieter. Bei Anbieterwechseln wird der Verlauf der aktuellen Unterhaltung bei der nächsten Anfrage auch an den neuen Anbieter gesendet.

Die vorbelegten Modelle sind Beispiele, keine Garantie für aktuellen Accountzugang. Nutze die Modellliste oder trage ein verfügbares Textmodell ein. Nicht jedes aufgelistete Modell unterstützt Text-Chat. Keine API-Nutzung ist in dieser ZIP enthalten.

Google verwendet `x-goog-api-key` und sein natives Nachrichtenformat, Anthropic `x-api-key`, `anthropic-version` und die native Messages API. Für persönlichen direkten Browserzugriff wird bei Anthropic der dafür vorgesehene Header gesetzt. OpenAI, OpenRouter und api.airforce nutzen Bearer-Authentifizierung. An die Basis-URL wird automatisch der passende Endpunkt angehängt; den vollständigen Chat-Endpunkt daher nicht als Basis eintragen.

Die Anbieter müssen Anfragen von deiner Pages-Adresse über CORS erlauben. QuiltAI kann serverseitige Blockaden, regionale Zugangsbeschränkungen oder fehlende Modellberechtigungen nicht aufheben. Dafür kann eine von dir kontrollierte passende HTTPS-Proxy-URL eingetragen werden. Bei einer abweichenden Basis-URL erhält deren Betreiber den jeweiligen API-Key. Eine statische Website kann keinen gemeinsamen geheimen Serverschlüssel sicher hinterlegen.

## Websites im Code Canvas erstellen

1. Anbieter und Modell einrichten.
2. Im Chat **„Website“** aktivieren oder **Code Canvas** öffnen.
3. Zum Beispiel schreiben: „Erstelle eine elegante Portfolio-Website für eine Fotografin mit Galerie, Kontaktbereich und dunklem Design.“
4. Nach einer vollständig abgeschlossenen Antwort übernimmt QuiltAI HTML, CSS und JavaScript in den Canvas. Unvollständige oder abgebrochene Antworten überschreiben den Canvas nicht.
5. Ergebnis in der Live-Vorschau ansehen. Mit dem Handy-Symbol lässt sich eine schmale Vorschau wählen.
6. Über den Chat Änderungen anfordern oder den Code direkt in den drei Tabs bearbeiten. Manuelle Änderungen aktualisieren die Vorschau nach kurzer Pause.
7. **„Website als HTML“** lädt eine eigenständige `index.html` mit eingebettetem CSS und JavaScript herunter. Diese kann wiederum auf GitHub Pages veröffentlicht werden.

Mit **„Beispiel“** lässt sich der Canvas auch ohne API-Key ausprobieren. Der Canvas wird pro Unterhaltung lokal gespeichert; ohne Unterhaltung gibt es einen lokalen Entwurf. Der aktuelle Canvas wird bei Anfragen im Website-Modus als Kontext an den gewählten KI-Anbieter gesendet.

Der Canvas unterstützt statisches HTML, CSS und JavaScript. React/JSX, npm, Backend-Prozesse und Build-Schritte werden nicht ausgeführt. Die Vorschau läuft in einem Sandbox-iframe ohne Zugriff auf QuiltAI-Schlüssel, Chats oder Browserspeicher der Hauptseite. Eine zusätzliche Content Security Policy sperrt externe Ressourcen und Netzwerkaufrufe; verwende Inline-SVG, CSS und lokale Interaktionen. Die heruntergeladene Website enthält diese zusätzliche Vorschau-Sperre nicht. Öffne heruntergeladenen Code nur, wenn du ihm vertraust.

## Tools und Plugins

Die eingebauten Tools werden manuell geöffnet und laufen im Browser. Plugins sind eigene JSON-GET-Endpunkte, keine LibreChat-, Open WebUI- oder MCP-Server-Plugins. Beispiel: `https://deine-domain.de/suche?q={query}`. Die URL wird erst bei Ausführung angefragt; QuiltAI zeigt vorher eine Bestätigung an. Der QuiltAI-API-Key wird dabei nicht mitgesendet. Plugin-Ergebnisse können in den Chat übernommen werden. Es gibt keine automatischen Modell-Tool-Aufrufe, keine eingebaute Websuche und keine Ausführung von beliebigem Plugin-Code.

## Daten und Sicherheit

Chats und Plugin-Konfiguration werden lokal im Browser gespeichert. Der API-Key bleibt standardmäßig nur bis zum Schließen bzw. Neuladen der Seite im Arbeitsspeicher. Optional kann er **unverschlüsselt** im lokalen Browserspeicher gespeichert werden. Das eignet sich nur für vertrauenswürdige persönliche Geräte. Unter Einstellungen lassen sich alle QuiltAI-Daten löschen.

Nachrichten, Systemanweisungen und angehängte Texte gehen direkt an die konfigurierte API. Die Oberfläche hat keinen eigenen Server, Login oder Cloud-Sync. Wer dasselbe Browserprofil nutzt, kann die dort gespeicherten Chats lesen. Google Fonts lädt die Schriftarten; ohne Netzwerk werden Systemschriften verwendet. KI-Antworten und Plugin-Daten werden als Text dargestellt, nicht als ausführbares HTML.

## Dateien

- `index.html`: Oberfläche
- `style.css`: Layout, Farben und mobile Ansicht
- `app.js`: Oberfläche, lokale Daten, Werkzeuge und Canvas-Verwaltung
- `providers.js`: Anfrage- und Streaming-Adapter für die Anbieter
- `canvas.js`: Code-Erkennung und Website-Zusammenbau
- `.nojekyll`: statische Bereitstellung ohne Jekyll

Alle Asset-Pfade sind relativ, damit die Website auch unter `https://name.github.io/repository/` funktioniert. Ein moderner Browser ist erforderlich.

## Prüfung

JavaScript-Syntax und Rechnerlogik geprüft. Automatisierte Prüfungen für Provider-Routing, getrennte Authentifizierungsheader, native Nachrichtenformate, über mehrere Datenblöcke verteiltes Streaming einschließlich Unicode, JSON-Antworten, Fehlerfälle und Canvas-Zusammenbau bestanden. Canvas-Website und JavaScript-Interaktion sowie Google-/Anthropic-Auswahl im Browser geprüft. Echte Anbieteraufrufe wurden mangels API-Keys nicht getestet.

## API-Dokumentation

- [OpenAI Chat Streaming](https://developers.openai.com/api/reference/resources/chat/subresources/completions/streaming-events)
- [Google Gemini Generate Content](https://ai.google.dev/api/generate-content)
- [Anthropic API](https://platform.claude.com/docs/en/api/overview)
- [OpenRouter API](https://openrouter.ai/docs/api_reference/overview)
- [api.airforce](https://api.airforce/)

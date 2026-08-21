# Kamera-Messhilfe

Einseitige Web-App, die aus dem Kamerabild eines Smartphones eine Längenmessung macht.
Nach einer Kalibrierung an einem Objekt bekannter Größe misst sie Strecken, Umfänge und
Flächen in cm bzw. mm und kann das Ergebnis als Foto mit eingezeichneter Messung sichern.

Die App besteht aus einer einzigen `index.html` ohne Build-Schritt und ohne externe
Abhängigkeiten und lässt sich als statische Datei ausliefern.

## Bedienung

1. **Kamera starten** – Rückkamera anfordern und Berechtigung erteilen.
2. **Kalibrierung** – zwei Punkte an den Enden eines Objekts bekannter Länge antippen.
   Anschließend die tatsächliche Länge eingeben; für gängige Referenzen
   (Bankkarte, 1-€- und 2-€-Münze, A4-Blatt) stehen Voreinstellungen bereit.
   Der Maßstab wird im Browser gespeichert und steht beim nächsten Aufruf wieder zur Verfügung.
   Alternativ **EC-Karte**: eine Schablone im ID-1-Format (85,60 × 53,98 mm) einblenden,
   deckungsgleich über die reale Karte legen, am Griff in der Größe anpassen und
   **Auf Karte kalibrieren** drücken. Ist bereits ein Maßstab bekannt, erscheint die
   Schablone von vornherein in ihrer echten Größe und taugt so als Gegenprobe.
3. **Messen** – nacheinander Punkte auf dem Bild antippen. Jedes Segment und die Gesamtlänge
   werden unter dem Bild angezeigt.
4. **Umfang** – schließt den Punktzug ab drei Punkten zu einem Polygon und ergänzt
   Umfang und Fläche.
5. **Lineal** – blendet ein bewegliches, frei drehbares Lineal mit echter cm-Skala ein.
6. **Foto aufnehmen** friert das Bild ein (Punkte lassen sich weiter setzen),
   **Foto speichern** sichert es mit allen Messlinien und Beschriftungen.

Mit **Punkt zurück** wird der zuletzt gesetzte Punkt entfernt, **Zurücksetzen** leert die
Messung, behält aber Kamera und Kalibrierung.

## Genauigkeit

Die Messung rechnet einen einzelnen Maßstab vom Bild auf die Wirklichkeit hoch und ist
deshalb eine Näherung. Sie gilt nur

- in derselben Ebene, in der das Referenzobjekt lag,
- bei unverändertem Abstand zwischen Kamera und Objekt,
- bei möglichst senkrechter Sicht auf diese Ebene.

Schrägsicht, ein anderer Abstand oder eine gewölbte Oberfläche verfälschen das Ergebnis.
Die App ersetzt kein Messgerät. Verändert sich der Kameraabstand, muss neu kalibriert werden.

## Betrieb

Der Kamerazugriff über `getUserMedia` setzt einen sicheren Kontext voraus: Die Seite muss
über **HTTPS** ausgeliefert werden (`http://localhost` gilt zum Entwickeln ebenfalls).
Über GitHub Pages ist das automatisch erfüllt.

Lokal testen:

```sh
python3 -m http.server 8000
# danach http://localhost:8000 öffnen
```

## Unterstützte Browser

Aktuelles Safari auf iOS sowie aktuelles Chrome, Edge und Firefox. Vorausgesetzt werden
Pointer Events, `ResizeObserver` und `getUserMedia`. Das Sichern des Fotos nutzt die
Web-Share-API, sofern vorhanden – auf dem iPhone landet das Bild damit direkt in „Fotos“ –,
sonst wird die Datei heruntergeladen.

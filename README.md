# ImageHandlerSystem 0.0.0
## Beschreibung
Softwaresystem zur einfachen, zentralen und nachhaltigen Verwaltung von Projektdaten
## Softwareentwickler
Hubert Fuchs
## Subsysteme
- Windows-App, Azure-App, Android-App, iOS-App, Web-App
## Problembeschreibung
Erfassung von Bildern und Texten auf einem mobilen Gerät, 
die Gruppenzuordnung der erfassten Informationen anhand einer Projektordnerstruktur 
und das Teilen dieser Daten mit internen und externen Mitarbeitern. 
Daten | Operationen
--- | ---
Ordnerstruktur | anlegen(manuell durch internen Mitarbeiter)
Barcode | generieren(Ordnerpfad -> Barcode)
Dokument | generieren(Barcode -> Dokument zum Drucken)
Foto | aufnehmen(Kamera), löschen(nur im Offline-Modus), anzeigen(nur im Online-Modus)
Text | erfassen, ändern(nur im Offline-Modus), löschen(nur im Offline-Modus), anzeigen(nur im Online-Modus)
## Problemspezifikation
### Windows/Azure-App: Projekt-Ordnerstruktur -> QR-Barcodes/PDF-Dokumente
- | JSON | OneDrive/Intranet | OneDrive/Intranet | -
--- | --- | --- | --- | ---
Eingabe: | Zuordnungsgruppen | Wurzelverzeichnis von allen Projekten | Ordnerstruktur von einem Projekt | Protokoll-Datei
Vorbedingung: | deserialisierbar | Lesezugriff | muss definiert sein; Lese- und Schreibzugriff | lesbar
Ausgabe: | Zuordnungsgruppen | - | QR-Code(s) in PDF(s) | Protokoll-Datei
Nachbedingung: | nicht leer; deserialisierbar | - | Anzahl vollständig; ausdruckbar | lesbar
### Android/iOS-App: Zuordnungsgruppen, QR-Barcode(s), Kamera-Foto(s) -> Bild- und Text-Datei(en)
- | - | - | - | -
--- | --- | --- | --- | ---
Eingabe: | Zuordnungsgruppen | QR-Barcode | Kamera-Foto | -
Vorbedingung: | deserialisierbar | lesbar | lesbar; als byte-array | -
Ausgabe: | anzeigen in UI | als Zuordnungsgruppe speichern | als BLOB speichern | Protokoll-Datei
Nachbedingung: | vollständig, richtig und lesbar | Bild hat richtige Zuordnungsgruppe | gültiges Format | lesbar
### Windows/Azure-App: Bild- und Text-Dateien -> Projekt-Ordnerstruktur
- | - | JSON | -
--- | --- | --- | ---
Eingabe: | Bilder als BLOB | Zuordnungsgruppen | Protokoll-Datei
Vorbedingung: | gültiges Format | deserialisierbar | lesbar
Ausgabe: | Bilddateien | - | Protokoll-Datei
Nachbedingung: | Bilddateien im richtigen Ordner vom Projekt | - | lesbar
### Web-App: Bild(er) und Text(e) als BLOB -> Anzeige für interne und externe Mitarbeiter
- | - | - | -
--- | --- | --- | ---
Eingabe: | --- | --- | ---
Vorbedingung: | --- | --- | ---
Ausgabe: | --- | --- | ---
Nachbedingung: | --- | --- | ---
## Sonstiges
### Offene Punkte
- Hat jeder Projektleiter bei TRI einen eigenen OneDrive-Account oder habt ihr ein Sammel-Account auf dem jeder mit seinem Win-PC Zugriff hat? Nutzt man aktuell OneDrive für irgendwas anderes?
### Anforderungen
- ANF01: Barcode und Dokument soll auf einem Desktop-PC generiert werden.
- ANF02: Anhand einer bereits existierenden Ordnerstruktur sollen Barcodes mit Zuordnungsgruppen generiert werden.
- ANF03: Ein Dokument soll ein Barcode enthalten und druckbar sein.
- ANF04: Der Barcode mit Zuordnungsgruppe soll auf dem mobilen Gerät scannbar sein.
- ANF05: Die Zuordnungsgruppe soll gescannt und automatisch eingestellt oder manuell ausgewählt werden.
- ANF06: Foto und Text soll auf einem mobilen Gerät erfasst werden.
- ANF07: Auf dem mobilen Gerät soll immer Offline und Online Speicherung möglich sein.
- ANF08: Im Offline-Modus sollen alle Daten dauerhaft lokal gespeichert werden.
- ANF09: Im Online-Modus sollen alle Daten dauerhaft in der Cloud gespeichert werden.
- ANF10: Bild- und Text-Daten auf dem mobilen Gerät sollen nach erfolgreicher Cloud-Übertragung gelöscht werden.
- ANF11: Interne und externe Mitarbeiter sollen Bild- und Text-Daten online lesen können.
### Version 0.1.0
- Eine Windows Desktop App die den Wurzelpfad zur lokalen Ordnerstruktur erfasst und entsprechend PDF-Dokumente mit QR-Codes erstellt.
- Eine Android Mobile App die im Offline-Modus eine Zuordnungsgruppe auswählbar oder einen QR-Code scannbar macht und dann über die Kamera ein Bilder erfasst und lokal speichert.
- Eine Azure Web App die mit Dummy-Beispieldaten eine mögliche Ansicht der Projektbilder für interne und externe Mitarbeiter zeigt. 
### Version 1.0.0
- Ein Softwaresystem das alle Anforderungen berücksichtigt und den vollständigen Workflow abbildet.

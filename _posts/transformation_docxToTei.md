---
layout: default
---

---

title: "Transformation einer .docx Datei in eine TEI P5-XML Datei"
author: Julia Dolhoff
editor: Till Grallert
date: 2017-10-19

---

[Zurück zur Startseite](./)

# Transformation einer .docx Datei in eine TEI P5-XML Datei

**Die Ergebnisse der Transformationen sind zu finden unter:**

`/Praktikanten OIB/DH-Praktikum/Transformation_Dateien/`

## Mit Oxygen XML Editor:

**Versuch 1** mit einer **deutschprachigen Datei** Digitale\_Edition.docx.

Zu finden im Verzeichnis: `/Praktikanten OIB/DH-Praktikum/Digitale_Edition.docx`


Das Dokument beinhaltet zu lange Zeilen, daher gibt Oxygen folgende Warnung aus:
> Dieses Dokument enthält lange Zeilen, welche die Performance des Text-Editors beeinträchtigen können.Die längste Zeile enthält 49.409 Zeichen.
> Diese Warnung wird nur für Dokumente angezeigt, die Zeilen mit mehr als 15.000 Zeichen enthalten (siehe die öffnen/speichern Seite im Editor -> in den Einstellungen).
> 
> Wenn Sie fortfahren, wird die Unterstützung für 'Line wrap' eingeschaltet und einige Editor-Eigenschaften werden ausgeschaltet.

Oxygen arbeitet generell sehr langsam, jedoch kann man den Speicher erhöhen um die Gewindigkeit zu steigern. Siehe dazu die Anleitungen für Windows, OS X und Linux: <https://www.oxygenxml.com/doc/versions/19.0/ug-editor/topics/set-parameters-for-application-launchers.html>.

In Transformations-Szenarien DOCX TEI P5 wählen und Szenario anwenden.

- TEI-Header erstellt
- Alle Überschriften wurden erfasst (xml:id)
- Stile der Schrift wurden erfasst (bold; italic)
- Fußnoten wurden erfasst (note)
- Links wurden erfasst (ref target=)
- Listen wurden erfasst (item)
- Abstufungen im Text wurden erfasst (rend="First Paragraph"; type="unordered")
- Keine Links


Fehler:

- Zeile 412: "## Benötigte technische Grundsätze" -> vermutlich bereits bei der Überführung des Markdown-Dokuments in Word entstanden
- Zeile 495: "[^siehe dazu: IDE]:"

--> Bei der Transformation mit einer .odt Datei werden Überschriften mit \<div> und <head> ausgezeichnet.

**Versuch 2** mit einer **arabischsprachigen Datei** `test\_arabic.docx`


Dabei wurden lediglich die erste Seiten aus der Datei `Gotha orient. A 114 - Arabic final.docx` in eine Test-Datei Kopiert und anschließend in Oxygen geöffent.

Oxygen arbeitet erneut sehr langsam um die Datei zu öffnen, das Konvertieren geht dafür sehr schnell.


**Versuch 3** mit der kompletten **arabischsprachigen Datei** `Gotha orient. A 114 - Arabic final.docx.`

Zu finden in dem Verzeichnis:
`OIB/DH-Praktikum/Gotha orient. A 114 - Arabic final.docx`

Zu große Datenmenge, Oxygen arbeitet sehr langsam.

**Anmerkungen:**

- Keine Sprachinfos (In Word-Datei vorhanden?!)


## Mit Pandoc:

Pandoc ist ein Kommandozeilenbasiertes Programm und besitzt kein Interface.
Die Installation ist sehr einfach.

Der Befehl für die Konvertierung lautet:
`pandoc \<filename> -f docx -t tei -o \<output_filename.xml>`

Dabei wird das Dokument sehr schnell in TEI simple konvertiert. Es handelt sich dabei um den Standard der einfachen Textverarbeitung. Das vorliegende arabische Dokument weist wenige Formatierungen auf, wodurch der Einsatz von TEI Simple durchaus erwähnt werden sollte.

**Anmerkungen:**

- Überschriften werden nicht erfasst (nur als \<p>)

## Mit OxGarage:

[TEI - OxGarage](http://www.tei-c.org/oxgarage/#) ist ein Web- und RESTful- Service mithilfe dessen Dokumente in andere Formate transformiert werden können. Z.B. von TEI zu Word (.docx) oder umgekehrt.

Für weitere Informationen siehe: <http://www.tei-c.org/Tools/>.

**Anmerkungen:**

- Konvertierung geht sehr schnell, Datei kann direkt heruntergeladen werden.
- Keine rechtlichen Probleme, da OxGarage die Dokumente nicht speichert.


## Mit Tustep:

DOCX -> RTF -> TUSTEP Ersetze -> XML-TEI (-> RTF Export -> DOCX)

Word-Dokument in LibreOffice als RTF abspeichern und anschließend in Tustep öffnen.

**Anmerkungen:**

- Tustep erkennt das Dokument nicht wenn Dateiname länger als 10 Zeichen

# Ergebnis:

### Oxygen

- Metadaten aus der Word-Datei
- Schema Validation nicht verlinkt
- Source-desc muss mit Inhalt gefüllt werden (ist noch nicht da)
- listChange könnte ausführlicher sein (steht nicht drin was gemacht wurde)
- Attributwerte beinhalten Leerzeichen
- Fußnoten in ordnung
- Tabellen: nicht jeder Text ist in \<p>
- stylesheet \<output indent ="no"> muss auf yes gestellt werden damit Text eingerückt wird (stylesheet auf github)

### OxGarage

- Gleich wie Oxygen


### Pandoc

- Wurzelknoten fehlt
- Für wellformed und valid: -s dranhängen (standalone)
-> Der Befehl für die Konvertierung lautet:
`pandoc \<filename> -f docx -t tei -o \<output_filename.xml -s>`
- TEI Schema fehlt
- Datei selber keine valide TEI (Title-Statement, publication leer)
- Schaut sich Struktur an (fügt \<div> hinzu wenn nötig)
- Keine Informationen über Stile
- footnode nicht eindeutig

### Tustep
- Tagnamen nicht Sprachabhängig


# Was wir brauchen:

- Leerzeichen ersetzen aus Attributwerten (z.B. Bindestrich oder camelCase)
- Gliedernde Struktur in \<div> (dort wo heading ist)
- Flacher Input muss in verschachtelte Output-Struktur überführt werden
- Verschachtelungs-Level hängt an Überschriften in Word (z.B. \<rend="heading 4">)
- Inline CSS vom Text trennen (soll im TEI-header landen)
- Überschriften- und Inhaltszeilen in Tabellen festlegen
- Es wurde versucht die Elemente grafisch nachzubauen mithilfe von Tabellen (haben z.B. nur eine Spalte)
- Gedrehte Wörter vorhanden -> Transformation versucht sie mithilfe von CSS darzustellen -> ERROR


## Anforderung an Word

- Stile wie bspw. Überschriften, Seitenumbruch

[Zurück zur Startseite](./)
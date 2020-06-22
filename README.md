# Besucherzähler Universtitätsbibliothek Magdeburg
Stand: 18.05.2020<br />
Bearbeiter: Veit Köppen<br />
Beschreibung und Datenschutz

## Executive Summary
Aufgrund der Coronakrise wird der Zutritt in der UB Magdeburg nur einer definierten Anzahl an Nutzern zur gleichen Zeit ermöglicht. Hierzu werden das Betreten und Verlassen registriert. Außerdem soll im Falle eines mit Covid-19 erkrankten Nutzers die Möglichkeit gegeben sein, alle Personen, die sich zum gleichen Zeitraum in der UB aufgehalten haben, darüber zu informieren.
Aus diesen Anforderungen wurde ein Stand-Alone-Tool entwickelt, dass sowohl die aktuell im Haus aufhaltende Nutzerzahl erfasst wie auch die zeitstempelbasierte Protokollierung durchführt.

## Aufbau Programm
Anforderungen: Rechner inkl. Barcodescanner zur kontaktlosen Bibliotheksnutzernummer-Erfassung.

Prozess:
 1.	Nutzer tritt ein, scannt selbstständig seinen Nutzerausweis ein
 2.	In der Anwendung wird der Barcode angezeigt
 3.	Bediener (Anwender) (z.B. Mitarbeiter Sicherheitsdienst oder der Bibliothek) klickt auf "Rein"
 4.	Zeitstempel und Barcode werden in einer CSV-Datei gespeichert (Eingangsvermerk)
 5.	Nach Nutzung verlässt der Nutzer die UB, scannt dabei erneut seinen Nutzerausweis ein
 6.	In der Anwendung wird der Barcode angezeigt
 7.	Anwender klickt auf "Raus"
 8.	Zeitstempel und Barcode werden in einer CSV-Datei gespeichert (Ausgangsvermerk)

## Konfigurationsparameter
Für die initiale Konfiguration wird die Datei **config.ini** im Ausführungsverzeichnis des Programms genutzt. Zur Konfiguration existieren die folgenden Parameter:
 -	**max_user**: Ganzzahlwert für den Grenzwert maximal gleichzeitig anwesender Besucher
 -	**threshold_yellow**: Gleitkommawert für den prozentualen Schwellwert der gelben Ampel
 -	**barcode_regex**: Zeichenkette für den regulären Ausdruck des Barcode-Formats (keinen 	Wert setzen lässt alle Barcodes zu)
 -	**fade_timeout**: Ganzzahlwert für die Anzahl der Millisekunden bis zum Ausblenden von 	Informationen (standardmäßig bei 10000 für 10 Sekunden)
 -	**path**: Zeichenkette für den Pfad der Ausgabedatei relativ zum Ausführungsverzeichnis des 	Programms
 -	**header**: Zeichenkette für die Kopfspalte der Ausgabedatei
 -	**sep**: Zeichen für das Spalten-Trennzeichen der Ausgabedatei
	
Befindet sich eine Datei ous100_barcodes.csv im Ausführungsverzeichnis des Programms, so werden darin enthaltene Barcodes, dem definierten regulären Ausdruck entsprechend, in den Cache des Programms geladen und mit eingescannten Barcodes vergleichen und geprüft, ob diese bereits (an-)gemeldet sind (in der Liste enthalten) oder nicht. Sind neue Barcodes nicht in der Liste enthalten, erscheint eine Information: "Achtung: Nutzer muss sich an der Ausleihtheke melden." Fehlt diese Datei, wird keine entsprechende Prüfung vorgenommen und daher auch keine Warnung über nicht angemeldete Nutzer ausgegeben.

## Datenhandling
Die erfassten Daten werden tageweise in einer Datei archiviert und für vier Wochen aufbewahrt. Anschließend werden die Nutzernummern gelöscht und somit der potentielle Personenbezug vernichtet. 

## Vorgehen zur Identifikation im Covid-19-Nutzer-Fall
Die Mitteilung über die betroffene Person zur Identifikation der Bibliotheksmitgliedschaft (Nutzernummer) erfolgt an die UB-Leitung und den Datenschutzkoordinator der UB. 
 1.	Die Identifikation der Mitgliedschaftsnummer erfolgt im LBS4-System der UB manuell.
 2.	Bei vorliegender Mitgliedschaft, werden die archivierten Dateien auf diese Nummer geprüft (Suche in CSV-Datei). 
 3.	Bei positivem Auftreten, werden alle Nutzernummern identifiziert, die sich im gleichen Zeitraum in der UB aufgehalten haben.
 4.	Im LBS4-System werden anhand der Nutzernummern, die Personen und ihre Kontaktdaten ermittelt und an die anfordernde Stelle in Form einer Excelliste (ggfs. verschlüsselt oder per Datenträger) weitergeleitet.

## Ansprechpartner
**Eckhard Blume**<br />
Leitender Bibliotheksdirektor UB Magdeburg<br />
E-Mail: eckhard.blume@ovgu.de<br />
Telefon: +49-391-67-58566

**Dr. Veit Köppen**<br />
Abteilungsleiter IT-Anwendungen & Datenschutzkoordinator UB Magdeburg<br />
E-Mail: veit.koeppen@ovgu.de<br />
Telefon: +49-391-67-58840

**Dr. Sascha Bosse**<br />
Bibliothekssystemverwalter<br />
E-Mail: sascha.bosse@ovgu.de<br />
Telefon: +49-391-67-52555

**Christian Schulz**<br />
IT-Anwendungsbetreuer<br />
E-Mail: christian.schulz@ovgu.de<br />
Telefon: +49-391-67-57414

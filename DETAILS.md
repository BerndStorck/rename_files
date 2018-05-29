# repsign 1.0.0

Beschreibt die Aufgabe des Shell-Skripts repsign, weist auf Probleme hin, die dieser Aufgabe verbunden sind und erklärt den gewählten Lösungsansatz.

## Wahl der Programmiersprache

Sehr wahrscheinlich wäre eine Lösung durch eine maschinennahe Sprache wie C effektiver. Da ich mich jedoch derzeit vor allem mit Bash-Programmierung auseinandersetzen möchte, habe ich das kleine Programme ausschließlich mit den Standardmitteln und üblichen Programmen der bash umgesetzt.

## Aufgabe des Shell-Scripts

Das Script sollte ein bestimmtes Zeichen aus Dateinamen löschen und dabei die Dateinamen weitestgehend erhalten.

Ich habe das Programm jedoch so geschrieben, dass es ein bestimmtes Zeichen in Dateinamen ersetzt, anstatt es zu löschen. Warum ich diesen Ansatz gewählt habe, beschreibt der Absatz "Probleme der Programmaufgabe".

## Probleme der Programmaufgabe

### Lesbarkeit von Dateinamen

Nach meiner Erfahrung sind Dateinamen, die etwa vormals Umlaute enthielten, und aus denen diese Umlaute gelöscht wurden nicht leicht zu lesen. Ersetzt man die Umlaute hingegen durch ein neutrales Zeichen, dann fällt es ungleich leichter, die frühere Bezeichnung zu erkennen. Dies spricht dafür, unerwünschte Zeichen nicht zu löschen, sondern zu ersetzen.

###Die Unmöglichkeit eines leeren Dateinamens

Würde man ein unerwünschtes Zeichen aus einer großen Anzahl von Dateien jedesmal Löschen, wenn es in einem Dateinamen vorkommt, dann riskiert man den unsinnigen Versuch, eine Datei auf einen leeren Dateinamen umzubenennen. Dies würde genau dann eintreten, wenn ein Dateiname nur aus dem zu löschenden Zeichen zusammengesetzt ist. 

Obwohl das Umbenennungskommando `mv` eine solche Umbenennung gar nicht durchführen würde, unterbindet repsign dieses Problem auf zwei Arten:

1. repsign löscht standardmäßig kein Zeichen aus den Dateinamen, sondern ersetzt es vorzugsweise durch ein anderes Zeichen. 
2. repsign gibt den Befehl zum Umbenennen einer Datei nur, wenn der berechnete neue Dateiname nicht leer ist. Obwohl man sogar den Aufruf `repsign "<ein_Zeichen>" ""` benutzen kann, um ein Zeichen doch zu löschen und nicht zu ersetzen, versucht repsign an `mv` nie die unsinnige Aufforderung weiterzugeben, eine Datei auf einen leeren Namen umzubenennen.

## Feedback erwünscht

Obwohl ich das kleine Programm getestet habe und es voraussichtlich problemlos seine Aufgabe erfüllt, muss ich zugeben, dass ich es in seiner jetzigen Form für unelegant halte. Ich bin neugierig, ob jemand eine andere sinnvollere oder geschicktere Vorgehensweise vorschlägt und bitte, um konstruktives Feedback,. Sowohl für andere Lösungen mit einem Bash-Script als auch mit anderen Programmiersprachen würde ich gerne sehen.


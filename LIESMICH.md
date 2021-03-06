# repsign 1.2.2

Obwohl ich dieses Shell-Script getestet habe und es meiner Ansicht nach einigermaßen solide arbeitet, rate ich dazu, von den zu manipulierenden Dateien, sofern sie wichtig und unersetzlich sind, Sicherungskopien zu erstellen, bevor man sie umbenennt. 

Dieses Dokument beschreibt  zuerst, wie man das Programm aufruft, und erläutert weiter unten warum ich das Programm so konzipiert habe, wie es ist.

**Alle meine Skripte habe ich mit der unbedingten Absicht geschrieben, deutschsprachigen Anwendern den Zugang zu Linux so weit als möglich zu erleichtern.** Deshalb haben alle meine Skripte eine deutschsprachige Hilfeseite, die unabhängig von der Systemsprache durch die Option `--hilf` angezeigt werden kann, **für repsign** also durch:

```bash
repsign --hilf
```

## Inhalt

1. Aufrufvarianten

   1.1. Erläuterung der Aufrufvarianten

2. Aufgabenbeschreibung

   2.1. Wahl der Programmiersprache

   2.2. Aufgabe des Shell-Skripts

   2.3. Probleme der Programmaufgabe

   ​	2.3.1 Lesbarkeit von Programmnamen

   ​	2.3.2. Die Unmöglichkeit eines leeren Dateinamens

## 1. Aufrufvarianten

1. `repsign`
2. `repsign <ein_Zeichen>`
3. `repsign <eine_Zeichenfolge> <eine_andere_Zeichenfolge>`
4. `repsign <ein_Pfad> <eine_Zeichenfolge> <eine_andere_Zeichenfolge>`
5. `repsign --hilf`

### 1.1. Erläuterungen zu den Aufrufvarianten

1. Das Programm ersetzt standardmäßig in den Namen aller Dateien des aktuellen Verzeichnisses alle Fragezeichen durch einen Unterstrich.

2. Wird repsign mit genau einem einzigem Parameter aufgerufen, mit der Angabe eines Zeichens, dann ersetzt repsign dieses Zeichen durch einen Unterstrich.

3. Mit zwei Parametern kann man bestimmen, welche Zeichenfolge durch welche andere Zeichenfolge ersetzt wird.

   Auch wenn dies nicht üblich ist, ist es möglich, dass ein Dateiname ein Fragezeichen "?" oder einen Asterisk "*" enthält. repsign kann auch diese Zeichen in Dateinamen ersetzen. Die folgenden beiden Programmaufrufe geben Beispiele für diese Ersetzungsmöglichkeit:

   * `repsign '?' _`  würde jedes Fragezeichen im Dateinamen durch einen Unterstrich ersetzen.
   * `repsign '*' -` würde jeden Asterisk im Dateinamen durch ein Minuszeichen ersetzen.

4. Bei drei Aufrufparametern bedeutet der erste das Verzeichnis, in dem Dateinamen verändert werden sollen, der zweite, welche Zeichenfolge ersetzt werden soll, und der dritte, welche andere Zeichenfolge stattdessen eingefügt werden soll. Solch ein Aufruf kann beispielsweise so aussehen:

   `repsign /home/rudolf/downloads "ü" "ue"`

   Dieses Beispiel zeigt, dass repsign die Pfadangabe ohne abschließenden Slash erwartet, und demonstriert zudem, dass repsign ein Zeichen auch durch mehrere ersetzen kann.

## 2. Aufgabenbeschreibung

Beschreibt die Aufgabe des Shell-Skripts repsign, weist auf Probleme hin, die dieser Aufgabe verbunden sind und erklärt den gewählten Lösungsansatz.

### 2.1. Wahl der Programmiersprache

Sehr wahrscheinlich wäre eine Lösung durch eine maschinennahe Sprache wie C effektiver. Da ich mich jedoch derzeit vor allem mit Bash-Programmierung auseinandersetzen möchte, habe ich das kleine Programme ausschließlich mit den Standardmitteln und üblichen Programmen der bash umgesetzt

### 2.2. Aufgabe des Shell-Scripts

Das Script sollte ein bestimmtes Zeichen aus Dateinamen löschen und dabei die Dateinamen weitestgehend erhalten.

Ich habe das Programm jedoch so geschrieben, dass es ein bestimmtes Zeichen in Dateinamen ersetzt, anstatt es zu löschen. Warum ich diesen Ansatz gewählt habe, beschreibt der Absatz "Probleme der Programmaufgabe".

### 2.3. Probleme der Programmaufgabe

#### 2.3.1. Lesbarkeit von Dateinamen

Nach meiner Erfahrung sind Dateinamen, die etwa vormals Umlaute enthielten, und aus denen diese Umlaute gelöscht wurden nicht leicht zu lesen. Ersetzt man die Umlaute hingegen durch ein neutrales Zeichen, dann fällt es ungleich leichter, die frühere Bezeichnung zu erkennen. Dies spricht dafür, unerwünschte Zeichen nicht zu löschen, sondern zu ersetzen.

#### 2.3.2. Die Unmöglichkeit eines leeren Dateinamens

Würde man ein unerwünschtes Zeichen aus einer großen Anzahl von Dateien jedesmal Löschen, wenn es in einem Dateinamen vorkommt, dann riskiert man den unsinnigen Versuch, eine Datei auf einen leeren Dateinamen umzubenennen. Dies würde genau dann eintreten, wenn ein Dateiname nur aus dem zu löschenden Zeichen zusammengesetzt ist. 

Obwohl das Umbenennungskommando `mv` eine solche Umbenennung gar nicht durchführen würde, unterbindet repsign dieses Problem auf zwei Arten:

1. repsign löscht standardmäßig kein Zeichen aus den Dateinamen, sondern ersetzt es vorzugsweise durch ein anderes Zeichen. 
2. repsign gibt den Befehl zum Umbenennen einer Datei nur, wenn der berechnete neue Dateiname nicht leer ist. Obwohl man sogar den Aufruf `repsign "<ein_Zeichen>" ""` benutzen kann, um ein Zeichen doch zu löschen und nicht zu ersetzen, versucht repsign an `mv` nie die unsinnige Aufforderung weiterzugeben, eine Datei auf einen leeren Namen umzubenennen.

## Feedback erwünscht

Obwohl ich das kleine Programm getestet habe und es voraussichtlich problemlos seine Aufgabe erfüllt, muss ich zugeben, dass ich es in seiner jetzigen Form für unelegant halte. Ich bin neugierig, ob jemand eine andere sinnvollere oder geschicktere Vorgehensweise vorschlägt und bitte, um konstruktives Feedback. Andere Lösungen sowohl mit einem Bash-Script als auch mit anderen Programmiersprachen würde ich gerne sehen.


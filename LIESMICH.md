# repsign 2.0.0

Dieses Dokument beschreibt  zuerst, wie man das Programm aufruft, und erläutert weiter unten warum ich das Programm so konzipiert habe, wie es ist.

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

### 1.1.1. Standardaufrufe

1. `repsign`
2. `repsign <ein_Zeichen>`|`<eine_Zeichenfolge>`
3. `repsign <eine_Zeichenfolge> <eine_andere_Zeichenfolge>`
4. `repsign <ein_Pfad> <eine_Zeichenfolge> <eine_andere_Zeichenfolge>`
5. `repsign --hilf`

**Alle meine Skripte habe ich mit der Absicht geschrieben, deutschsprachigen Anwendern den Zugang zu Linux so weit als möglich zu erleichtern.** Deshalb haben alle meine Skripte eine deutschsprachige Hilfeseite, die unabhängig von der Systemsprache durch die Option `--hilf` angezeigt werden kann, **für repsign** also durch:

```bash
repsign --hilf
```
### 1.1.2. Nur bestimmte Dateien ändern

6. `repsign <Zeichenfolge> <andere_Zeichenfolge> -f <DATEI> [<DATEI>] …`

6. Wenn der dritte Parameter die Option "-f" ist, werden die darauf folgenden
    Parameter als eine Liste von Dateien aufgefasst, auf welche die
    Namensänderungen beschränkt werden sollen.

### 1.1.3. Übersetzungsmodus

7. `repsign -t|--tr|--translate <eine_Zeichenfolge> <eine_andere_Zeichenfolge>`
8. `repsign <ein_Pfad> -t|--tr|--translate <eine_Zeichenfolge> <eine_andere_Zeichenfolge>`

### 1.1.4. Aufrufvarianten zur Dateisuche

9. `repsign -l|--list|--find`
10. `repsign --find=abnorm|--find=strange`
11. `repsign --find='Zeichenkette'`

### 1.2. Erläuterungen zu den Aufrufvarianten

1. Das Programm ersetzt standardmäßig in den Namen aller Dateien des aktuellen Verzeichnisses alle Leerzeichen durch einen Unterstrich.

2. Wird repsign mit genau einem einzigem Parameter aufgerufen, mit der Angabe eines Zeichens, dann ersetzt repsign dieses Zeichen durch einen Unterstrich.

3. Mit zwei Parametern kann man bestimmen, welche Zeichenfolge durch welche andere Zeichenfolge ersetzt wird.

   Auch wenn dies nicht üblich ist, ist es möglich, dass ein Dateiname ein Fragezeichen "?" oder einen Stern "*" enthält. repsign kann auch diese Zeichen in Dateinamen ersetzen. Die folgenden beiden Programmaufrufe geben Beispiele für diese Ersetzungsmöglichkeit:

   * `repsign '?' _`  würde jedes Fragezeichen im Dateinamen durch einen Unterstrich ersetzen.
   * `repsign '*' -` würde jeden Stern im Dateinamen durch ein Minuszeichen ersetzen.

4. Bei drei Aufrufparametern bedeutet der erste das Verzeichnis, in dem Dateinamen verändert werden sollen, der zweite, welche Zeichenfolge ersetzt werden soll, und der dritte, welche andere Zeichenfolge stattdessen eingefügt werden soll. Solch ein Aufruf kann beispielsweise so aussehen:

   `repsign /home/rudolf/downloads "ü" "ue"`

   Dieses Beispiel zeigt, dass repsign die Pfadangabe ohne abschließenden Schrägstrich erwartet, und demonstriert zudem, dass repsign ein Zeichen auch durch mehrere ersetzen kann.
   
5. Der Aufruf der Hilfe-Seite.

6. Wenn der dritte Parameter die Option "-f" ist, werden die darauf folgenden Parameter als eine Liste von Dateien aufgefasst, auf welche die Namensänderungen beschränkt werden sollen.

7. Ist der erste von insgesamt drei Parameter die Option  `-t`, `--tr` oder `--translate` dann wird jedes Zeichen aus dem zweiten Parameter durch das entsprechende Zeichen aus dem dritten Parameter ersetzt.

   Wenn `<Zeichenmenge_2>` nicht leer und kürzer als `<Zeichenmenge_1>`
       ist, werden alle überzähligen Zeichen am Ende von `<Zeichenmenge_1>`,
       für die es keine Entsprechung in `<Zeichenmenge_2>` gibt, durch das
       letzte Zeichen in `<Zeichenmenge_2>` ersetzt.

8. Bei vier Aufrufparametern bedeutet der erste das Verzeichnis, in dem Dateinamen verändert werden sollen, der zweite muss die Option `-t`, `--tr` oder `--translate` sein. Das Programm wird dann jedes Zeichen aus dem dritten Parameter durch das entsprechende Zeichen des vierten Parameters ersetzen.

9. Ein Aufruf nur mit der Option `-l`, `--list` oder `--find` sucht im aktuellen Verzeichnis und allen seinen Unterverzeichnissen nach Dateien, die ein Leerzeichen enthalten.

10. Der Aufruf `repsign --list=abnorm` sucht im aktuellen Verzeichnis und allen seinen Unterverzeichnissen nach Dateien, deren Name ein unübliches Zeichen enthält.

11. Der Aufruf `repsign --list='<Zeichenkette>'` sucht im aktuellen Verzeichnis und allen seinen Unterverzeichnissen nach Dateien, deren Name die `<Zeichenkette>` enthält.

## 2. Aufgabenbeschreibung

Beschreibt die Aufgabe des Shell-Skripts repsign, weist auf Probleme hin, die dieser Aufgabe verbunden sind und erklärt den gewählten Lösungsansatz.

### 2.1. Wahl der Programmiersprache

Sehr wahrscheinlich wäre eine Lösung durch eine maschinennahe Sprache wie C effektiver. Da ich mich jedoch derzeit vor allem mit Bash-Programmierung auseinandersetzen möchte, habe ich das kleine Programme ausschließlich mit den Standardmitteln und üblichen Programmen der Bash umgesetzt

### 2.2. Aufgabe des Shell-Scripts

Ich habe die erste Version dieses Programms geschrieben, weil ich eine größere Anzahl von Dateien mit einem Fragezeichen im Dateinamen besaß. Das Script sollte deshalb ein bestimmtes Zeichen aus Dateinamen entfernen und dabei die Dateinamen weitestgehend erhalten. Ich das Programm daher so angelegt, dass es das zu entfernende Zeichen in Dateinamen durch einen Unterstrich ersetzt. Warum ich diesen Ansatz gewählt habe, beschreibt der Absatz "Probleme der Programmaufgabe".

### 2.3. Probleme der Programmaufgabe

#### 2.3.1. Lesbarkeit von Dateinamen

Nach meiner Erfahrung sind Dateinamen, die etwa vormals Umlaute enthielten, und aus denen diese Umlaute gelöscht wurden nicht leicht zu lesen. Ersetzt man die Umlaute hingegen durch ein neutrales Zeichen, dann fällt es ungleich leichter, die frühere Bezeichnung zu erkennen. Dies spricht dafür, unerwünschte Zeichen nicht zu löschen, sondern zu ersetzen.

#### 2.3.2. Die Unmöglichkeit eines leeren Dateinamens

Würde man ein unerwünschtes Zeichen aus einer großen Anzahl von Dateien jedes Mal Löschen, wenn es in einem Dateinamen vorkommt, dann riskiert man den unsinnigen Versuch, eine Datei auf einen leeren Dateinamen umzubenennen. Dies würde genau dann eintreten, wenn ein Dateiname nur aus dem zu löschenden Zeichen zusammengesetzt ist. 

Obwohl das Umbenennungskommando `mv` keine Datei auf einen leeren Namen umbenennt, unterbindet repsign diese Situation auf zwei Arten:

1. repsign löscht standardmäßig kein Zeichen aus den Dateinamen, sondern ersetzt es vorzugsweise durch ein anderes Zeichen. 
2. repsign gibt den Befehl zum Umbenennen einer Datei nur, wenn der berechnete neue Dateiname nicht leer ist. Obwohl man sogar den Aufruf `repsign "<ein_Zeichen>" ""` benutzen kann, um ein Zeichen doch zu löschen und nicht zu ersetzen, gibt repsign an  `mv` nie die unsinnige Aufforderung weiter, eine Datei auf einen leeren Namen umzubenennen.

## Feedback erwünscht

Ich bin neugierig, ob jemand eine andere sinnvollere oder geschicktere Vorgehensweise vorschlägt. Andere Lösungen sowohl mit einem Bash-Script als auch mit anderen Programmiersprachen würde ich gerne sehen.

## Rechtliche Hinweise

Obwohl ich dieses Shell-Script getestet habe und es meiner Ansicht nach einigermaßen solide arbeitet, rate ich dazu, von den zu manipulierenden Dateien, sofern sie wichtig und unersetzlich sind, Sicherungskopien zu erstellen, bevor man sie umbenennt. 


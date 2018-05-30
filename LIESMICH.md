# repsign 1.1.1

Obwohl ich dieses Shell-Script getestet habe und es meiner Ansicht nach einigermaßen solide arbeitet, rate ich dazu, von den zu manipulierenden Dateien, sofern sie wichtig und unersetzlich sind, Sicherungskopien zu erstellen, bevor man sie umbenennt. 

Eine genauere Beschreibung der Aufgabe und der Probleme dieses kleinen Shell-Scripts liegt unter dem Dateinamen "DETAILS.md" vor.

## Aufrufvarianten

1. `repsign`
2. `repsign <ein_Zeichen>`
3. `repsign <eine_Zeichenfolge> <eine_andere_Zeichenfolge>`
4. `repsign <ein_Pfad> <eine_Zeichenfolge> <eine_andere_Zeichenfolge>`
5. `repsign -h|--help`

###Erläuterungen zu den Aufrufvarianten

1. Das Programm ersetzt standardmäßig in den Namen aller Dateien des aktuellen Verzeichnisses alle Fragezeichen durch einen Unterstrich.

2. Wird repsign mit genau einem einzigem Parameter aufgerufen, mit der Angabe eines Zeichens, dann ersetzt repsign dieses Zeichen durch einen Unterstrich.

3. Mit zwei Parametern kann man bestimmen, welche Zeichenfolge durch welche andere Zeichenfolge ersetzt wird.

4. Bei drei Aufrufparametern bedeutet der erste das Verzeichnis, in dem Dateinamen verändert werden sollen, der zweite, welche Zeichenfolge ersetzt werden soll, und der dritte, welche andere Zeichenfolge stattdessen eingefügt werden soll. Solch ein Aufruf kann beispielsweise so aussehen:
  
   `repsign /home/rudolf/downloads "ü" "ue"`

   Dieses Beispiel zeigt, dass repsign die Pfadangabe ohne abschließenden Slash erwartet, und demonstriert zudem, dass repsign ein Zeichen auch durch mehrere ersetzen kann.
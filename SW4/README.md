# Protokollierung

## Inhaltsverszeichnis
- [Was sind Logfiles](#einführung)
    - [Ereignislog](#ereignislogs)
- [Steuerung der Logfiles](#steuerung-der-logfiles)
    - [Änderung vom Ablageort der Logfiles](#änderung-vom-ablageort-der-logfiles)
    - [Konfigurationsmöglichkeiten der Logfiles](#konfigurationsmöglichkeiten-der-logfiles)

## Was sind Logfiles
Logfiles sind Dateien, welche Programme benutzten, damit sie Automatisch Informationen in die Datei schreiben können. Logfiles werden hauptsächlich aus dem Grund geschriben, dass Programme automatisch Informationen in diese Dateien reinschreiben können. Mit diesen Logfiles hat man praktisch ein Buch von allen Schritten, welche ein Programm getätigt hat. Mit Logfiles kann man ganz einfach und simpel nachfassen, wo genau Probleme entstanden sind. 

### Ereignislogs
Ein Ereignislog ist einfach eine Art an Log, ander alle Ergeignise, wie Fehlermeldungen, dokumentiert werden. Das Ereignisprotokoll wird immer verwendet um die Historie einer Aktivität einzusehen. 

## Steuerung der Logfiles

### Änderung vom Ablageort der Logfiles
Um den Ablageort von Logfiles in Ubuntu zu ändern, musst du die folgenden Schritte ausführen:
- Den Befehl ```sudo nano /etc/rsyslog.conf``` ausführen.
- Jetzt kann man nach der Zeile suchen, inder die Logfilelocation gespeichert wird. Diese Zeile fängt meistens mit $FileCreateMode und $DirCreateMode an. 
- Ändere den Pfad auf den gewünschten Speicherort für die Logfiles. 

- Änderungen speichern

- Jetzt sollte man den Dienst mit dem Command neu starten. ````sudo service rsyslog restart````.

### Konfigurationsmöglichkeiten der Logfiles
Es gibt mehrere Wege Logfiles zu konfigurieren. Um zum Beispiel **das Format** ändern, muss man das beim jeweiligen Dienst selber machen. 
Für die Ausgabe muss man ebenfalls im jeweiligem Dienst das einstellen. 
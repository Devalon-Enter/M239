# Installation des Webservers

## Inhaltsverszeichnis
- [Vorbereitung](#vorbereitung)
- [Installation](#installation)
- [Konfiguration](#konfiguration)

## Vorbereitung
Folgende Vorbereitungen wurde getroffen, um den Webserver zu installieren.
1. Eine Virtuelle Maschiene mit Ubuntu LTS 22.04 wurde aufgesetzt
2. Der Command ```sudo apt update && sudo apt upgrade -y``` wurde ausgeführt, um alle Pakete zu aktualisieren


## Installation
Die eigentliche Installation von Apache war recht simpel. Wir mussten dazu nur den Command ```sudo apt install apache2 -y``` in einem Terminal ausführen und schon wurde Apache auf unserem System installiert. <br>
Diese Installation sollte dann das Verzeichniss ```/var/www/html/``` erstellen. Dort wird dann schlussendlich die Website gehostet. Das ist das Standard Verzeichniss von Apache auf Ubuntu. Wenn wir jetzt dort eine index.html Datei reinspeichern, wird diese Datei im Browser unter ```http://localhost/``` angezeigt werden. Falls es probleme macht, kann man versuchen den Dienst mit ```sudo service apache (re)start``` zu starten. 

### Testen der installation
Dazu haben wir eine simple index.html Datei in das Verzeichniss ```/var/www/html/``` gelegt und einfach den Browser gestartet.<br>
Der Code zu der index.html Datei sah so aus:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Unsere Testseite</title>
</head>
<body>
    <header>
        <h1>Das ist unsere Website</h1>
    </header>
    <main>
        <p>Hier Testen wir, ob unser Webserver funktioniert</p>
    </main>
    <footer style="display:fixed; bottom:0; left: 0; width:100%; height:20vh; background-color:lightgray;">
        <p>Dies ist der Footer der Website</p>
    </footer>
</body>
</html>
```
Nachdem der Inhalt in der Datei war, musste ich nur noch den Command ```firefox localhost``` im Terminal eingeben und es hat mir schon den Broswer mit der Website geöffnet.

## Konfiguration 
Damit der Webserver Optimal funktioniert, mussten wir ihn minimal konfigurieren. <br>
Zuerst, wollten wir ein wenig routing hinzufügen. Darum haben wir die hosts Datei in unsererm Linux Client verändert. <br>
Die Hosts Datei liegt auf Ubuntu unter dem Pfad ```/etc/hosts```. 
Dass heisst, dass wir ganz einfach eine neue Domain hinzufügen konnten. 
Die Hosts Datei sah dann im Anschluss so aus:
```
127.0.0.1	localhost
127.0.1.1	ubuntu
127.0.0.1	watery-water.ch

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```
Wenn wir jetzt auf der Viruellen Maschiene die Website <b>[watery-water.ch](http://watery-water.ch/)</b> besuchen, wird sich jetzt unsere Website öffnen.

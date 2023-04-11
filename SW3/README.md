# Ein CMS Installieren

## Inhaltsverszeichnis
- [Einführung](#einführung)
- [Auswahl](#unsere-auswahl)
- [Installation](#installation)
- [Konfiguration](#konfiguration)
- [Testing](#testing)

## Einführung
Die Aufgabe ist es ein CMS zu installieren und zu konfigurieren. 
Folgendes Zitat beschreibt ziemlich gut. 
> Ein Content-Management-System (CMS) ist eine Softwareanwendung, die es Benutzern ermöglicht, digitale Inhalte zu erstellen, zu bearbeiten, gemeinsam zu editieren, zu veröffentlichen und zu speichern. Content-Management-Systeme werden typischerweise für Enterprise Content Management (ECM) und Web Content Management (WCM) eingesetzt.

-- Ein Zitat von der Seite [computerweekly.com](https://www.computerweekly.com/de/definition/Content-Management-System-CMS). <br>
Weiter unten sehen Sie, für welches CMS wir uns entschieden haben. 



## Unsere Auswahl
Wir haben uns für eines der bekantesten CMS's der Welt entschieden. Unser CMS wird von schätzungsweise **42% aller Websites** benutzt. Wir werden das CMS [WordPress](https://wordpress.com/de/) benutzten. WordPress ist sehr bekannt und wird von fast jedem Webhoster unterstützt. 


## Installation
Die Installation an sich war relativ simpel. Für die Installation haben wir [folgende Anleitung](https://www.digitalocean.com/community/tutorials/install-wordpress-on-ubuntu) befolgt.<br>
Zuerst mussten wir php installieren. Dies haben wir mit dem Command ```sudo apt install php php-mysql -y``` gemacht. <br>
Jetzt war es an der Zeit eine Datenbank aufzusetzen. Dazu mussten wir zuerst den mysql client installieren. Dies haben wir mit folgenden Command gemacht: ```sudo apt install mariadb-server mariadb-client -y```. <br> 
Jetzt konnte ich mich ganz einfach in die Konsole von MySQL einloggen. Für MySQL habe ich kein Passwort gesetzt. Nun war die Aufgabe eine Datenbank für die neue Website zu erstellen. <br>
Nun konnte ich eine ganze Reihe an befehlen ausführen, um die Datenbank und den Benutzer dazu zu erstellen: 
```sql
CREATE DATABASE waterywater;
CREATE USER 'wateryAdmin'@'localhost' IDENTIFIED BY 'password';
GRANT ALL ON waterywater.* TO 'wateryAdmin'@'localhost' IDENTIFIED BY 'password';
```
Nachdem dies gemacht ist, können wir WordPress vom Internet herunterladen. Und in die richtigen Ordner kopieren. 
```
cd /tmp && wget https://wordpress.org/latest.tar.gz
tar -xvf latest.tar.gz
sudo cp -R wordpress/* /var/www/html/
sudo chown -R www-data:www-data /var/www/html/
```

## Konfiguration
Für die Konfiguration konnte ich ganz einfach mit folgenden Command in die CMS Interface gelangen: ```firefox watery-water.ch```. <br>
Hier konnte ich ganz einfach folgende Eigenschaften einstellen:
- Websiten Sprache
- Datenbank Informationen
- Titel der Website
- Benutzer
- Email Adresse

Folgend sind die Benutzerdaten, welche wir gewählt haben:
- Benutzer: wateryWpAdmin
- Passwort: password
- Email: danie.greil@edu.tbz.ch

Nachdem alles Installiert und konfiguriert wurde, habe ich noch das WordPress Plugin [WooCommerce](https://woocommerce.com/) installiert. Dies habe ich gemacht, damit es sich mehr wie ein Shop anfühlt. 


## Testing
Zum überprüfen, ob PHP installiert ist, konnten wir folgenden Command ausführen: ```php --version```. An folgenden Output, konnten wir sehen, dass die Installation erfolgreich war.
```
PHP 8.1.2-1ubuntu2.11 (cli) (built: Feb 22 2023 22:56:18) (NTS)
Copyright (c) The PHP Group
Zend Engine v4.1.2, Copyright (c) Zend Technologies
    with Zend OPcache v8.1.2-1ubuntu2.11, Copyright (c), by Zend Technologies
```
Nachdem alles aufgesetzt wurde, kann man die Website öffnen. Das ist in unsererm Fall [localhost](http://localhost/) oder ganz einfach auch [watery-water.ch](https://watery-water.ch/).

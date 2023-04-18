# Zertifikate verwalten

## Inhaltsverszeichnis
- [Self Signed Certificate](#self-signed-certificate)
- [Installieren von HTTPS](#installieren-von-https-auf-einem-webserver)
- [Umleitung HTTPS](#umleitung-http-auf-https)

## Self Signed Certificate
Wie die Website [entrust.com](https://www.entrust.com/resources/faq/what-is-a-self-signed-certificate#:~:text=A%20self%2Dsigned%20TLS%2FSSL,for%20public%20applications%20and%20websites.) beschreibt, sind Self Signed Certificates nicht von offiziellen CA ausgestellt worden. <br>
```A self-signed TLS/SSL certificate is not signed by a publicly trusted certificate authority (CA) but instead by the developer or company that is responsible for the website; as they are not signed by a publicly trusted CA, they are usually considered unsafe for public applications and websites.```
<br>
Hier werde ich beschreiben, wie genau wir ein Self Signed Certifikat auf unserem Server installiert und evtl. auch konfiguriert haben.
<br>
Für diese Aufgabe habe ich die Anleitung von [Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-apache-in-ubuntu-22-04) befolgt. 
<br>
Der erste Schritt war es das sognannte ```mod_ssl``` Modul auf Apache zu aktivieren. Dies haben wir folgendermassen gemacht:
```
sudo a2enmod ssl
sudo systemctl restart apache2
```
Wenn das gemacht ist, können wir jetzt anfangen das Certifikat zu erstellen. Dies machen mit mit folgenden Command: 
```
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache-selfsigned.key -out /etc/ssl/certs/apache-selfsigned.crt
```
Nachdem dieser Command ausgeführt wurde, muss man jetzt einfache Informationen über die Eigene Firma angeben. 


## Installieren von HTTPS auf einem Webserver
Jetzt haben wir den Self Signed Certificate Schlüssel. Jetzt können wir Ihn in den Webserver einbauen.<br>
Dies machen wir, indem wir zuerst eine neue Konfigurationsdatei für apache2 erstellen. Diese Datei sollte sich unter dem Pfad ```/etc/apache2/sites-available/watery-water.ch.conf``` befinden. <br>
Diese Datei sollte dann folgenden Inhalt haben:
```
<VirtualHost *:443>
   ServerName watery-water.ch
   DocumentRoot /var/www/html

   SSLEngine on
   SSLCertificateFile /etc/ssl/certs/apache-selfsigned.crt
   SSLCertificateKeyFile /etc/ssl/private/apache-selfsigned.key
</VirtualHost>
```
Diese Konfiguration können wir mit dem Befehl ```sudo a2ensite watery-water.ch.conf``` und ```sudo apache2ctl configtest``` aktivieren und testen. 
<br>
Falls alles richtig gemacht wurde, können wir jetzt den Server neustarten. ```sudo systemctl reload apache2```. 

## Umleitung HTTP auf HTTPS
Dies war relativ simpel, da wir nur auf die vorher erstellte Konfigurationsdatei gehen mussten, und ein Paar neue Zeilen hinzufügen mussten. Jetzt sieht die ganze Datei folgendermassen aus:
```
<VirtualHost *:80>
	ServerName watery-water.ch
	Redirect / https://watery-water.ch/
</VirtualHost>

<VirtualHost *:443>
   ServerName watery-water.ch
   DocumentRoot /var/www/html

   SSLEngine on
   SSLCertificateFile /etc/ssl/certs/apache-selfsigned.crt
   SSLCertificateKeyFile /etc/ssl/private/apache-selfsigned.key
</VirtualHost>
```

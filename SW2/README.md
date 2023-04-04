# MailServer installieren

## Inhaltsverszeichnis
- [Auswahl](#auswahl)
- [Installation](#installation)
    - [dovecot](#dovecot-installation)
    - [postfix](#postfix-installation)
- [Konfiguration](#konfiguration)
    - [dovecot](#dovecot-config)
    - [postfix](#postfix-config)

## Auswahl
Für den Mailserver haben wir uns für [postfix](https://ubuntu.com/server/docs/mail-postfix) und für [dovecot](https://ubuntu.com/server/docs/mail-dovecot) entschieden.
Dies ist, weil postfix und dovecot die beliebtesten Alternativen für Mail sind. 

## Installation 
Für die Installation habe ich mich entschieden zuerst dovecot zu installieren, weil es in der Dokumentation höcher ist als postfix. <br>

### dovecot installation
Um dovecot zu installieren brauche es nur folgenden Command: ```sudo apt install dovecot-imapd dovecot-pop3d -y```. <br>

### postfix installation
Die Installation ans sich war ebenfalls sehr simpel: ```sudo apt install postfix -y```. 
Nachdem der Command ausgeführt wurde, wurden wir zu einer GUI weitergeführt, bei welcher wir Elemente wie Mailtyp und so weiter auswählen konnten.
Hier sind die Daten, welche wir gewählt haben:
- Mail-typ: Internet site
- Mail Name: watery-water.com

## Konfiguration
### dovecot-config
Nachdem dovecot installiert war, musste ich es noch konfigurieren. 
Die Konfigurationsdatei von dovecot ist unter ```/etc/dovecot/dovecot.conf``` zu finden. Die konnte ich öffnen und im Anschluss richtig konfigurieren.
### postfix-config
Um postfix zu konfigurieren, braucht man zuerst den Command ```sudo dpkg-reconfigure postfix```. 
Hier haben wir dann wieder folgende Daten benutzt:
- Mail-typ: Internet site
- Mail Name: watery-water.com
- Mail Empfänger: info@watery-water.ch
Sonst habe ich alle Werte auf default gelassen. <br>
Jetzt mussten wir nur noch den Service neustarten. Dies macht man mit dem Command ```sudo systemctl restart postfix.service```

## Testen
Das Testen des Mailservers war relativ simpel. <br>
Um dovecot zu testen, haben wir den command ```telnet localhost pop3``` eingegeben. Das ergebnis war folgendes:
```
daniel@ubuntu:~$ telnet localhost pop3
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
+OK Dovecot (Ubuntu) ready.
```
Hier können wir sehen, dass dovecot funktioniert und bereit ist. 
<br>
Jetzt können wir austesten, ob ebenfalls das postfix funktioniert.<br>
Dazu geben wir den command ```telnet watery-water.ch 25``` in die Konsole ein. 
Wir bekommen, folgenden Output zurück:
```
telnet watery-water.ch 25
Trying 127.0.0.1...
Connected to watery-water.ch.
Escape character is '^]'.
220 ubuntu.localdomain ESMTP Postfix (Ubuntu)
EHLO watery-water.ch
250-ubuntu.localdomain
250-PIPELINING
250-SIZE 10240000
250-VRFY
250-ETRN
250-STARTTLS
250-ENHANCEDSTATUSCODES
250-8BITMIME
250-DSN
250-SMTPUTF8
250 CHUNKING
```
An den Statuscode 250 können wir erkennen, dass es funktioniert. 
# Testing

## Inhaltsverszeichnis
- [Was sind Tests](#was-sind-tests)
- [Funktionstests](#funktionstests)
- [Sicherheitstests](#sicherheitstests)
- [Lasttests](#lasttests)

## Was sind Tests?
Der Begriff "Test" kann mehrere Bedeutungen haben. In diesem Fall aber, sind Tests zum Testen ob unser Webserver richtig funktioniert. Solche Tests können automatisiert oder manuell gemacht werden. In diesem Kapitel werden die Meisten tests manuell auf unserem Webserver durchgeführt. 
Websites -Tests dienen dazu, mögliche Fehler und Schwächen auf der Website zu identifizieren und zu beheben, bevor die Website für Benutzer zugänglich ist. Dies kann dazu beitragen, das Risiko von Systemfehlern oder Sicherheitsverstößen zu minimieren.

## Funktionstests
Testen ob die Website Funktioniert.

### Website erreichbar
Ziel des Tests: <br>
Hier wird getestet, ob der Webserver erreichbar ist. Es soll geschaut werden, ob ein Normaler benutzer die Website erreichen und navigieren kann.
| Beschreibung  | Erwartetes Ergebnis | Aktion        | Auswertung    |
| ------------- | ------------------- | ------------- | ------------- |
| Website Normal | Website ist normal über den Browser erreichbar | Eingabe von "watery-water.ch" in den Broswer  | Test Erfolreich. Website etwas langsam |
| Website übers Terminal öffnen | Website kann über das Terminal geöffnet werden | Eingabe von "firefox watery-water.ch" im Terminal | Test Erfolgreich |

### Website ist navigierbar?
Ziel des Tests: <br>
Hier soll geschaut werden, ob der Benutzer die Website auch Ohne Probleme benutzen kann. Der Benutzer sollte z. B. nicht auf ausgelaufene Links treffen können.
| Beschreibung  | Erwartetes Ergebnis | Aktion        | Auswertung    |
| ------------- | ------------------- | ------------- | ------------- |
| Alle Links werden ausprobiert  | Der Benutzer sollte nicht auf alte Links antreffen | Es wird auf jeden Link auf der Website geklickt | Test Knapp bestanden. Es gibt 1 oder 2 Links, welche nicht funktionieren |
| Prüfen auf Rechtschreibfehler | Die Website ist fehlerfrei geschrieben | Die Website wird navigiert und auf Rechtschreibfehler geprüft | Test nicht aufgeführt  |
| Website ist strukturiert und übersichtlich | Website ist einfach zu bedienen | Website wird benutzt | Test Erfolgreich. Die Website ist einfach zu benutzen und man kann sich schnell zurecht finden |

## Sicherheitstests
Testet die Sicherheit von der Website.

### SSL-Zertifikat funktioniert
Ziel des Tests: <br>
Hier schauen wir ob, das SSL Zertifikat funktioniert. Dies ist wichtig, damit unsere Kunden mehr Vertrauen in unsere Website haben und dass Ihre Daten sicher übertragen werden.
| Beschreibung  | Erwartetes Ergebnis | Aktion        | Auswertung    |
| ------------- | ------------------- | ------------- | ------------- |
| HTTPS Funktioniert | Der Webserver ist auf HTTPS erreichbar | Eingabe von "https://watery-water.ch" in den Broswer | Test Erfolreich. HTTPS ist auf dem Webserver aktiviert |
| HTTPS Weiterleitung | Bei der Eingabe von der Normalen Domain wird auf HTTPS umgeleitet | Eingabe von "watery-water.ch" in den Broswer | Test Erfolreich. Website wird Standartmässig auf HTTPS umgeleitet |

### Vulnerability Scan
Ziel des Tests: <br>
Das Ziel ist es die Sicherheit der Website und des Webservers zu überprüfen. Hiermit werden wir mit einem Tool die Sicherheit scannen. 
| Beschreibung  | Erwartetes Ergebnis | Aktion        | Auswertung    |
| ------------- | ------------------- | ------------- | ------------- |
| Port scanner. Website wird durch einen Port Scanner gescannt | Es gibt keine offenen Ports | Portscan durch das Terminal mit einem Tool wie nmap | Test nicht ausgeführt  |
| Website HTML Code wird hochgeladen und auf Viren gescannt | Website wird gescannt und keine Viren werden gefunden | Website Code wurde auf [Virustotal](https://www.virustotal.com/gui/home/upload) hochgeladen und gescannt | Test Erfolgreich. Keine Viren gefunden |
| Keine Sensible Information is für die Öffentlichkeit zugänglich | Keine Information über Passwörter, Emails... einfach zu recherchieren. | Die Website wird nach diesen Infos durchsucht | Test erfolgreich. Auf der Website finden sich keine sensiblen Daten.

### Authentifizierung
Ziel des Tests: <br>
Hier wird geschaut, ob die Authentifizierung von der Website funktioniert. So wissen wir immer wer auf welche Ressourcen Zugriff hat.
| Beschreibung  | Erwartetes Ergebnis | Aktion        | Auswertung    |
| ------------- | ------------------- | ------------- | ------------- |
| Admin Login  | Der Administrator kann sich ohne Probleme Einloggen | Es wird die Seite watery-water.ch/wp-admin geöffnet und die Logindaten werden eingegeben | Test Erfolgreich. Der Administrator konnte sich anmelden |
| Versuchter Admin Login. Es werden falsche Anmeldedaten eingegeben | Das versuchte Login wird Fehlschlagen | Identisch wie bein vorherigen test, mit der Ausnahme, dass Fehlerhafte Login daten eingegeben werden | Test Erfolgreich. Benutzer kann sich nicht mit fehlerhaften anmeldedaten anmelden |
| Fiktive anmeldedaten werden eingegeben | Fehler. Man sollte sich nicht anmelden können | Fitive Username und Passwort werden eingegeben | Test Erfolgreich. Man kann sich nicht anmelden

## Lasttests
Testet, ob der Webserver stark genug ist. 

### Apache JMeter
Apache JMeter ist ein Open-Source-Lasttest-Tool, das in Java geschrieben wurde und zur Überprüfung der Leistung von Webanwendungen verwendet werden kann. <br>
Ziel des Tests: <br><br>
Überprüfen wie viel der Server aushalten kann und ob der Server dem Standhalten kann.
| Beschreibung  | Erwartetes Ergebnis | Aktion        | Auswertung    |
| ------------- | ------------------- | ------------- | ------------- |
| Lasttest |  |  |  |
| Umfangtest |  |  |  |

### Apache Bench
Apache Bench ist ein weiteres Open-Source-Lasttest-Tool, das auf Apache HTTP-Server basiert und in der Lage ist, eine hohe Anzahl von gleichzeitigen Anfragen an den Webserver zu senden. <br><br>
Ziel des Tests: <br>
Überprüfen ob der Server die Anzahl an Anfragen unterstützen kann.
| Beschreibung  | Erwartetes Ergebnis | Aktion        | Auswertung    |
| ------------- | ------------------- | ------------- | ------------- |
| Lasttest |  |  |  |
| Erreichbarkeitstest |  |  |  |


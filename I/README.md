# Know-How & Begriffe
Eine Sammlung an Wissen, die Wir laut Vorgaben beantwortet haben. Verschiedene Fragen zum Thema Webservices und Webhosting, werden hier beantwortet.
## Inhaltsverszeichnis
- [Multi-Hosting](#multihosting-mit-einem-webserver)
- [DNS](#dns)
- [Server Informationen](#server-informationen)
- [Proxy](#proxy)
- [DMZ](#dmz)

## Multihosting mit einem Webserver
Mit einem Webserver, wird es uns möglich, eine Webseite zu hosten. So weit so gut. Aber wie sieht es denn aus, wenn wir nicht sehr viel Budget oder gar Hardware zur Verfügung haben und aber umbedingt eine weitere Webseite hosten müssen. Nun, vielleicht, gibt es dazu ja eine einfache Lösung.

### Virtuelle Hosts
Die antwort auf die oben gestellte Frage, lautet, Virtuelle Hosts. Nun, was ist den Viruelles Hosting. Nun stellen wir uns am besten diese Situation vor:

Wir führen ein Unternehmen, welches ihren Web-Service mit einer anderen Plattform expandieren möchte. Nun aber, haben wir nicht das Budget um uns einen neuen Server anzuschaffen, womit wir die neue Website hosten können. Die Lösung ist Virtuelles Hosting. Es erlaubt uns,  **weitere Webseiten, welche aber unter einer anderen Domain läuft, auf dem ein und dem selben Server laufen zu lassen**. So wie unsere bereits vorhandene Webseite.

Als Bildliche darstellung:
![alt text](https://www.cloudpanel.io/astatic/assets/images/article/2021/56/5c18eac9e9a50ec8fa336009d9db67f2.svg "Ein Apache Server hostet mehrere Webseiten")

Das was man hier sieht, sollte ein Beispiel dafür sein, wie das ganze aussieht. Wir haben hier einen Apache Webserver (Blau) und neben dran befinden sich mehrere Webseiten (Grün) welche vom Server gehostet werden. All diese Webseiten, müssen aber unter einer anderen Domain laufen.

## DNS
DNS oder auch ausgeschrieben Domain Name System ist eines der wichtigsten Netwerk infrastrukturen, die es im Bereich Networking gibt. Es besteht aus vielen verschiedenen Teilen, die es ermöglichen, dass wir uns täglich im Internet so bewegen könnnen, so wie wir wollen.
 

 DNS ist im Grunde genommen wie ein Baum aufgebaut. Bestehend aus vielen Zonen und Zonendateien. Diese sind Strukturiert, wie ein Baum. Der von den Subdomains ausgeht, bis hin zu den Top-Level-Domains. Hier eine grafik zur demonstration:

 ![alt text](https://www.dotcom-monitor.com/blog/wp-content/uploads/sites/3/2013/02/DNS-Monitoring-Domain-Name-Space-768x612.jpg "Der Aufbau eines DNS in verschiedenen Zonen und konfiguriert durch verschiedene Zonendateien")

### Namensauflösung
DNS ist generell dafür zuständig, dass unsere eingetippten URL's oder auch im technischen Fachbereich genannt, FQDN ausgeschrieben Fully Qualified Domain Name, erfolgreich dahin führen, wo wir auch hin wollen.

Nehmen wir uns doch einmal ein Beispiel für einen FQDN:

```Text
www.example.com.
```

Dies hier wäre ein Beispiel für eine FQDN sehen wir uns nun diese Stück für Stück an. Damit wir nachher wissen, wie DNS eine Namensauflösung durchführt.

#### Root-Label
Als erstes, haben wir hier den ``.`` nach dem ``.com`` dieser Punkt wird ***Root-Label oder auch einfach Root*** genannt. Der Grund warum wir diesen Punkt nicht in einer URL sehen, wenn wir sie einfach normal eintippen ist im Grunde einfach nur deswegen, da die Browser diese mittlerweile einfach von selbst hinten dran hängen und wir als User diese nicht eintippen müssen.
 
#### TDL oder Top-Level-Domain
Als nächstes, schauen wir uns die ***Top-Level-Domain*** an. diese sehen wir als ``.com`` oder wie wir es hier in der Schweiz am besten kennen als ``.ch``. Es wird darum Top-Level Domain genannt, weil es dafür zuständig ist, die Request des Clients an den richtigen TLD-Server zu schicken, welcher dann im Umkehrschluss dafür zuständig ist, den rest der FQDN korrekt aufzulösen.

#### Second-Level-Domain
Nun kommen wir zum Namensgebenden Teil einer Webseite. Die Second-Level-Domain oder SLD ist in der FQDN dieser Teil: ``.example``.
Sie sind im Grunde genommen lediglich dazu da, den Zweck oder Namen einer Webseite zu bestimmen.

#### Subdomains
Nun nach der Second-Level-Domain, können beliebig viele Subdomains folgen. Meistens, benutzt man sie zur logischen und oder physischen Trennung von Diensten innerhalb eines Unternehmens. Meistens aber verwenden Webserver jedoch die Standardkonvention ``www``. Hingegen andere Dienste, wie zum Beispiel Mailserver könnten hier ``imap./smtp./pop3./mail.`` verwenden.

### Zonen
Neben der Aufteilung in Labels und Levels, wird DNS in weitere Zonen aufgeteilt, welche aber grösstenteils, nur dem administrativen Zweck dienen sollten und in den Zonendateien definiert werden. ***Beziehe hier auf die Abbildung oben***.
 

 Eine Zone startet in der Regel immer zu unterst in einer Domäne und breitet sich dann progressiv zur Spitze, der Top-Level-Domain, aus.

#### Zonendateien
Eine Zonendatei, ist eine Textdatei, welche aus einer Liste von verschiedenen **R**esource **R**ecords besteht und jeweils einem Namens Server gegeben wird. Dadurch wird dieser dann konfiguriert.

Hier ein Beispiel für eine Zonendatei:

![alt text](https://lh4.googleusercontent.com/ge9ntTn5kQQte_2w0L6TD3JMP6p1hnfETfQjxiXOihjvw8UGmB-ebLziH1sLcmcAsulhocAel_zkNpsQPWTfK_GCT7SzDNbrB74MfjNWVzZzRAPKSGU63fHTNTYLcAukAyX3QJrZ "Ein Beispiel für eine Zonendatei")

Diese zuvor schon erwähnte Liste, besteht aus Resource Records oder auch kurz RR-Typen. Ich werde hier kurz auflisten, welche es gibt und was denn diese RR-Typen überhaupt machen. Fangen wir an.

* A
* AAAA
* CNAME
* MX
* TXT
* NS
* SOA
* SRV
* PTR

Diese 9 RR-Typen gibt es und werden in diesen Zonendateien gebraucht um verschiedene Dinge zu konfigurieren und zu erreichen. Als ein kleines Beispiel: Wenn wir in einer Zonendatei einen A-Record antreffen, dann beinhaltet dieser immer die IPv4 Adersse des Webservers, welcher auf diese Domain, ``www.example.com``, lautet.
 

 Als ein weiteres Beispiel, können wir den MX-Record nehmen. Dieser hält fest, wie SMTP über welchen Mail-Server routen muss.
 
## Server Informationen
Text

## Proxy
Text

## DMZ
Text
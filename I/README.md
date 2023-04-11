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
### Windows
Wenn wir die Informationen eines Mailservers herausbekommen wollen, dann können wir dies mit einem sehr einfachen Befehl herausfinden. Auf Windows funktioniert dies so.

```
nslookup -type=mx tbz.ch
```

Als ein kleines Beispiel. Das ergebnis würde dann so aussehen:

```
Server:  STBZDC12.tbz.local
Address:  10.62.99.8

Nicht autorisierende Antwort:
tbz.ch  MX preference = 10, mail exchanger = tbz-ch.mail.protection.outlook.com

tbz-ch.mail.protection.outlook.com      internet address = 104.47.11.10
tbz-ch.mail.protection.outlook.com      internet address = 104.47.11.74
```
 
### Linux

Wenn wir dies jedoch auf Linux ausführen wollen, dann müssen wir hier den ``dig`` befehl verwenden. Dieser funktioniert so:

```
dig mx tbz.ch
```

Das Ergebnis dieser Query sieht dann wie folgt aus:

```
; <<>> DiG 9.18.12-0ubuntu0.22.04.1-Ubuntu <<>> mx tbz.ch
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 63693
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 3

 

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;tbz.ch.                IN    MX

 

;; ANSWER SECTION:
tbz.ch.            5    IN    MX    10 tbz-ch.mail.protection.outlook.com.

 

;; ADDITIONAL SECTION:
tbz-ch.mail.protection.outlook.com. 5 IN A    104.47.11.10
tbz-ch.mail.protection.outlook.com. 5 IN A    104.47.11.202

 

;; Query time: 63 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Tue Apr 04 11:35:53 CEST 2023
;; MSG SIZE  rcvd: 117
```

Wie wir hier sehen können, bei beiden Versionen, gibt es uns in der jeweiligen Antwortsektionen, den namen des zuständigen Mailservers für die Domäne ``tbz.ch`` zurück.

## Proxy
Es ist eine möglichkeit immerhin einwenig Kontrolle über den eigenen Datenfluss zu bekommen. Ein Proxy ist dazu da, den direkten Datenaustausch zwischen Client und Server zu unterbinden bzw. den Austausch zu überbrücken. Bei einem Proxy handelt es sich um ein physisches Gerät (meist ein Server ganz selten ein Personal Computer) dieser Agiert meist innerhalb eines Netzwerks.

Grafische Darstellung eines Proxy:
![alt text](https://upload.wikimedia.org/wikipedia/commons/thumb/f/fb/Schematic_Proxy_Server.svg/2880px-Schematic_Proxy_Server.svg.png "Darstellung eines Proxy im Netzwerk")

Hier können wir erkennen, dass der Proxy (Orange) zwischen den beiden anderen Geräten (Weiss) steht und so die Verbindung nicht direkt zum Empfänger führt.

Bei Proxy wird zwischen zwei hauptsächlich gebräuchlichen Typen unterschieden. Dabei gibt es das sogenannte **Forward-Proxy** und das gegenstück zum Forward-Proxy, das **Reverse-Proxy**. Wir werden beide Typen so gut es geht untersuchen und erklären.

### Forward-Proxy

Ein Forward-Proxy ist die normale Art und Weise, wie ein Proxy verwendet wird. Dabei steht ein Proxy Server in einem Privaten Netzwerk und verwaltet den Datatraffic. Was passiert denn da genau? <br>

Nun wenn ein Client aus dem eigenen Netz eine Anfrage an eine Webseite macht, dann geht diese Anfrage, nicht wie sonst direkt an den Webserver dieser Webseite aber stattdessen an unseren Proxy. Dieser Proxy muss vom Client wirklich direkt angesprochen werden, sonst wird die Anfrage so wie normalerweise direkt an den Webserver mit der IP-Adresse unseres Clients als absender. <br>
Nun aber, ist es uns möglich diese Anfrage über unseren Proxy zu leiten. Dieser nimmt dann diese Anfrage und schickt sie mit seiner eigenen IP-Adresse an den Webserver. Dieser Webserver, kann den Originalen Absender nicht erkennen. Für ihn ist der Absender dieser Anfrage immernoch unser Proxy.

Auf genau dem selben Weg, geht auch die Anfrage wieder zurück. Zuerst, geht sie an den Proxy, der wiederum die IP-Adresse auf unser Netzwerk wechselt und die Antwort an unseren Client schickt.

### Reverse-Proxy

Das Gegenteil eines Forward-Proxy und eine Art und Weise, wie sie normalerweise nur Unternehmen wirklich gebrauchen, den Reverse-Proxy.

Hier grafisch dargestellt, das Schema eines Reverse-Proxy:

![alt text](https://www.psychz.net/content/proxy/reverse.jpg "Darstellung eines Reverse-Proxy Schemas")

Ein Reverse-Proxy, funktioniert, wie der Name schon sagt, umgekehrt. Heisst, wenn unser Client nun eine Anfrage an einen Webserver in einem externen Netz macht, dann geht diese Anfrage nicht wie normalerweise direkt auf den Webserver, sondern sie geht auf den Proxy dieses Webservers. Wir selbst haben in unserem Netz keinen Proxy konfiguriert auf den wir zugreifen. Lediglich der Webserver verwendet einen Proxy, der in das Externe Firmennetz hineingeht. Und nicht wie beim normalen Proxy nach draussen ins Internet.

## Proxy Vor- und Nachteile

Mit Proxy ist es möglich vor allem die Sicherheit zu erhöhen und ein gewisses Mass an anonymität gewinnen. Ausserdem ist es möglich, über diese Proxy Geräte noch weitere Dinge zu verwalten, wie zum Beispiel die Bandbreite, die Verfügbarkeit und verschiedene weiter Sicherheitseinstellungen.

Jedoch sei gesagt, dass Proxy hauptsächlich dann funktioniert, wenn man Browser anfragen macht. Dabei wird nicht der gesamte Datenverkehr eines Clients geschützt. Falls man einen Schutz für sämtlichen Datenverkehr haben möchte, dann sollte man sich VPN zurechtlegen.

## DMZ

Ein DMZ oder auch ausgeschrieben **D**e**m**ilitarisiere **Z**one wird sehr oft dann gebraucht, wenn man dienste wie Webserver, Mailserver usw in einem Netz am laufen hat. Eine DMZ ist eine Zone in einem Privaten Netzwerk, welches vom Intranet getrennt ist.

Hier eine grafische Darstellung eines DMZ Netzwerks:

![alt text](https://upload.wikimedia.org/wikipedia/commons/7/78/Demilitarized_Zone_Diagram.png "Darstellung eines DMZ")

Hier können wir sehen, dass unser Netzwerk (Gelb) getrennt ist. In zwei Zonen. Die eine Zone, wo unsere Clients usw. stehen, wird **Intranet oder LAN** genannt. Die andere Zone, ist unser DMZ Zone und alles, was ausserhalb der Firewall ist, wird **WAN oder Internet** genannt. DMZ dient dem Zweck, den Traffic, welcher über unsere Firewall geht, in die DMZ einzulassen und den Kontakt zwischen dem LAN und der DMZ zu verhindern. Das DMZ kann nur auf das WAN zugreifen, jedoch **nie** mit dem LAN in Kontakt treten.

Dies erhöht die Sicherheit des eigenen Netzwerkes Drastisch.
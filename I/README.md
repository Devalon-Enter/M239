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
Als nächstes, schauen wir uns die ***Top-Level-Domain*** an. diese sehen wir als ``.com`` oder wie wir es hier in der Schweiz am besten kennen als ``.ch``. Es wird darum Top-Level Domain genannt
## Server Informationen
Text

## Proxy
Text

## DMZ
Text
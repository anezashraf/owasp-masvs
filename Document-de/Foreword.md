
![OWASP LOGO](images/OWASP_logo.png)

# Mobile Application Security Verification Standard - Release 1.1

14.07.2018

## Vorwort von Bernhard Mueller, OWASP Mobile Project

Technologierevolutionen können sehr schnell gehen. Noch vor 10 Jahren waren Smartphones klobige Geräte mit kleinen Tastaturen - teure Spielgeräte für technikverliebte Geschäftsleute. Heute sind Smartphones ein wesentlicher Bestandteil unseres Lebens. Wir hängen inzwischen von ihnen ab und nutzen sie zur Information, Navigation und Kommunikation. Sie sind allgegenwärtig - in der Geschäftswelt und im privaten Umfeld. 

Jede neue Technologie bringt neue Sicherheitsrisiken mit sich. Eine der größten Herausforderungen für alle die im Sicherheitsumfeld arbeiten, ist Schritt zu halten mit der fortlaufenden Weiterentwicklung. Das blaue Team (Verteidigerseite) liegt dabei immer einige Schritte hinter dem roten Team (Angreiferseite) zurück. Viele unterlagen deshalb zu Beginn dem Trugschluss, altbekannte Vorgehensweisen direkt auf das mobile Umfeld anzuwenden im Sinne von: "Smartphones sind im Prinzip nur kleine PCs und mobile Apps sind wie klassische Software - folglich gelten die gleichen Sicherheitsanforderungen". Jedoch funktioniert das so nicht. 
Mobile Betriebssysteme unterscheiden sich von Desktop-Betriebssystemen und mobile Apps sich von Webanwendungen. Zum Beispiel macht die klassische Methode Virenprüfungen auf Basis von Signaturen durchzuführen in modernen mobilen Betriebssystemumgebungen keinen Sinn. Es ist nicht nur inkompatibel zur Art und Weise wie mobile Apps verteilt werden sondern darüber hinaus aufgrund des Betriebssystemdesigns (Sandbox-Isolation) von Apps technisch überhaupt nicht umsetzbar. Bei gewöhnlichen 08/15-Apps sind zudem eine Reihe von Schwachstellen wie Buffer overflows und XSS weniger relevant als in Webanwendungen und Desktopanwendungen. (Ausnahmen möglich)
Über die Zeit hat sich das gewandelt und die Securitybranche hat nun eine bessere Vorstellung für die mobile Bedrohungslage entwickelt. 

Der Datenschutz steht im Mittelpunkt mobiler Sicherheit. Apps speichern persönliche Informationen, Fotos, Aufnahmen, Notizen, Kontodaten, Geschäftsdaten, Standortdaten und viele mehr. Sie dienen uns als tägliche Helfer um uns mit Daten- und Kommunikationsdiensten zu verbinden, die jede einzelne der Nachrichten, die wir mit anderen austauschen, verarbeiten. Übernimm die Kontrolle über ein Smartphone und Du erhälst ungefilterten Zugriff auf das Leben der betreffenden Person. Wenn man sich vorstellt, dass Mobilgeräte durchaus verloren gehen oder gestohlen werden können und sich mobile Schadsoftware im Aufwärtstrend befindet wird der hohe Bedarf an Datenschutz nochmals mehr deutlich. Ein Sicherheitsstandard für mobile Apps muss deshalb klar im Fokus haben, wie mobile Apps mit sensiblen Daten umgehen, sie verarbeiten und speichern. 

Moderne mobile Betriebssysteme wie iOS und Android bieten gute APIs für sichere Datenspeicherung und Kommunikation - Diese müssen allerdings auch implementiert und dabei korrekt genutzt werden um effektiv zu sein. Datenspeicherung, Interprozesskommunikation, korrekte Nutzung kryptographischer APIs und sichere Netzwerkkommunikation sind nur ein paar der Aspekte die eine sorgfältige Betrachtung erfordern.

Eine wichtige Frage die man sich stellen muss, ist, wie weit und wie umfangreich Schutzmaßnahmen umzusetzen sind und wo die Grenze liegt. Zum Beispiel würden die meisten zustimmen, dass eine mobile App das Serverzertifikat bei einem TLS-Handshake prüfen muss. Was ist jedoch mit SSL-Zertifikat-Pinning ? Führt es direkt zu einer Schwachstelle, es nicht umzusetzen? Sollte dies eine Anforderung sein, wenn eine App sensible Daten verarbeitet oder ist es eventuell sogar contra-produktiv? Müssen wir Daten in einer SQLite-Datenbank verschlüsseln, wenn doch das Betriebssystem bereits ein Sandbox-Konzept mitbringt? Was für die eine App angemessen ist, kann für eine andere App unrealistisch sein. Der MASVS ist ein Versuch, diese Anforderungen zu standardisieren und Prüf-Level einzuführen die zu unterschiedlichen Bedrohungszenarien passen. 

Darüber hinaus hat das Erscheinen von Root-Malware und Remote-Administrations-Tools gezeigt, dass mobile Betriebssysteme selbst ausnutzbare Schwachstellen haben. Um Client-seitige Manipulation zu verhindern und den Schutz sensibler Daten zu erhöhen, kommen vermehrt zusätzliche Container-basierte Isolations-Technologien zum Einsatz. An dieser Stelle wird es kompliziert. Es gibt Hardware-basierte Sicherheitsmechanismen und Betriebssystemseitige Container-Lösungen wie Android for Work und Samsung Knox aber nicht durchgängig für alle Geräte. Als Notlösung sind Software-basierte Schutzmechanismen möglich jedoch existieren leider keine Standards sowie Testprozesse zu deren Prüfung.

Als Folge davon existieren zahlreiche mobile Sicherheitstestberichte bei denen die Tester fehlende Obfuskierung oder fehlende Root-Erkennung in einer Android-App als "Sicherheitslücke" werten. Auf der anderen Seite werden Maßnahmen wie Verschlüsselung von Zeichenketten, Erkennung von Debuggern oder Kontrollfluss-Obfuskierung nicht als verpflichtend erachtet. Letztlich ergibt dieses "schwarz-weiss Denken" keinen Sinn, denn Resilienz ist keine binäre Eigenschaft sondern hängt davon ab gegen welche konkreten Client-seitigen Bedrohungen man sich schützen möchte. Software-Schutzmaßnahmen zur Erhöhung der Resilienz bringen gewissen Nutzen jedoch können sie definitiv umgangen werden und dürfen deshalb niemals als Ersatz für Sicherheitsmaßnahmen dienen.

Das übergeordnete Ziel des MASVS ist es mit dem MASVS-L1 ein solides Basis-Sicherheitsniveau, mit dem MASVS-L2 ein erhöhtes Sicherheitsniveau sowie kontextbezogen weitere Defense-in-Depth-Maßnahmen gegen Client-seitige Bedrohungen (MASVS-R) für mobile App-Sicherheit anzubieten.


Folgendes soll mit dem MASVS erreicht werden:

- Bereitstellen von Sicherheitsanforderungen für Softwarearchitekten und Entwickler um sichere mobile Applikationen zu entwickeln;
- Definition eines Branchenstandards gegen den mobile Apps in Sicherheits-Reviews getestet werden können;
- Schärfung und Klarstellung der Rolle von Schutzmechanismen in der mobilen Sicherheit und Definition von Anforderungen um deren Effektivität zu prüfen;
- Aussprechen von individuellen Empfehlungen zur Anwendung von mobilen Sicherheitsmechanismen für verschiedene Anwendungsfälle.  

Wir sind uns bewußt dass ein 100%-iger Konsens innerhalb der Sicherheitsbranche unmöglich zu erreichen ist. Nichtsdestotrotz hoffen wir dass der MASVS eine nützliche Hilfestellung für alle Phasen mobiler Softwareentwicklung und Tests darstellt. Als offener Standard soll der MASVS sich über die Zeit weiterentwickeln und wir begrüßen jede Unterstützung und Vorschläge.   

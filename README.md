- [Autor und Version](autoren)
- [Einführung](einfuehrung)
 - [Hardware und Software](hardsoft)
 - [Installationsanleitung](installation)
 - [Qualitätskontrolle](qualitaet)
 - [Error-Handling](error)
 - [Quellen](quellen)
 - [Lizenz](lizenz)

# W15-Kubernetes
Mit diesem Projekt an der TBZ, versuche ich einen Kubernetes Cluster mit microk8s aufsetzten und eine Anleitung für nachfolgende Generationen an Schüler:innen zuschreiben. 

<a name="anker-zur-autoren"></a>
## 1. Autoren, Versionierung des Dokumentes
Autor: Janis Müller

Version: V.1.0 (Versioning habe ich nicht gemacht, da dies von GitHub erledigt wird)

<a name="anker-zur-einfuerung"></a>
## 2. Einfuehrung 
   - Kubernetes ist eine Anwendung zum bereitstellen, skalieren und verwalten von Containerumgebungen. Die einfachere Version von Kubernetes ist microk8s ("microkeight"). Mit Microk8s kann man für Raspberry Pis ein Cluster-System aufbauen.
   - Für dieses Projekt habe ich ca. 12 Lektionen zur Verfügung. In diesen Lektionen, muss ich das System aufsetzten, das gearbeitete Dokumentieren und zum schluss noch die Fehler finden welche ich bei der Installation gemacht habe. 
   - Für mich könnte ich Stolpersteine bei Konfiguration der Raspberrypis haben, denn da wir einen teil in der Schule machen können und den Rest Zuhause muss ich die Konfiguration entweder an einem Morgen durcharbeiten oder das System fest an einem Ort installieren.

<a name="anker-zur-hardsoft"></a>
## 3. Benoetigte Hard- und Software
  - Hardware
   	- Raspberry Pi 4 
   	- Raspberry Pi 3B 
   	- merere MicroSD Karten mit varierenden Grössen (2x 2GB; 1x 16GB; 2x 32GB; 1x 64GB). Diese Speicher Karten kann ich je nach nutzen und Zweck auswählen. Brauche ich viel Speicherplatz? Brauche ich eine Schnellere Karte um die Leistung des Pi's auszunutzen? Wie gross ist die Gefahr eines Bottleneck bei einer langsameren Karte?
![Ohne Titel](https://user-images.githubusercontent.com/63262820/138827765-5e85efd1-cb2e-4e70-8007-9993d56b79f7.png)

  - Die Hardware wird in Zwei Kategorienen eingeteilt den sogenannten nodes.
	- Masternode: Die Masternode ist das Rückgrad des Systemes. Auf dieser node wird ein Ubuntu 20.4 Server image laufen um die vorüge eines Server image ohne GUI zu nutzen. 
	- Leafnode: Diese Nodes werden an die Masternode angehängt und wird ebenfalls mit einem Ubuntu server image bestückt.
  - Diese images werden entweder mit dem Balena Etcher oder dem Raspberri Pi imager auf die Micro SD Karten geladen.

> "!Wichtig! Die OS müssen 64 Bit Architektur sein sonst funktioniert microk8s nicht. Denn es wurde für 64-Bit geschrieben."

<img src="https://user-images.githubusercontent.com/63262820/140657271-eecc7525-d8aa-4d7f-af51-0df5cc6f019d.JPG" width="500">

<a name="anker-zur-installation"></a>
## 4. Installationsanleitung (Didaktisch reduzierte Anleitung. Lernende sollen eine eigene Lösungswege realisieren)
   - Anweisungen verstaendlich und nachvollziehbar
   - Keine fertigen Loesungsschritte aufzeigen
   - Hilfestellung (Tipps, Quellen...

1. Zu begin der installation, sollt man die apt Datenbanken der RPI's aktualisisieren. Das braucht einen guten Moment Zeit.

2. Anschliessend beginnt der Installations Prozess des Kubernetes Cluster bzw. von microk8s(oder micro kubernetes). Für diesen Installations Schritt werden wir ein "snap" command nutzen.

> sudo snap install microk8s --classic --channel=1.22

Amd. Autor: channels sind die verschiedenen Versionen eines Programmes welches man herunterladen kann. zb. 1.20/stable ; 1.20/candidate ; 1.20/beta ; usw.

<img width="1142" alt="image" src="https://user-images.githubusercontent.com/63262820/140815252-76206b3d-41f8-4d1d-ade1-0a09fc20b5fb.png">

3. Die Installation von microk8s benötigt Admin berechtigungen für die entsprechendenen User. Für diesen Schritt benutzen wir usermod (wird ähnlich angewendet wie chmod) und chown. 

- Fügt den momentane User zur Gruppe "microk8s"
> sudo usermod -a -G microk8s $USER

- Ordner berechitigung ändern
> sudo chown -f -R $USER ~/.kube

- Neu einloggen in de Session
> su - $USER

Falls man dies nicht macht, dann endet mann so(Bild aus): 

4. Anschliessend muss man nur den Service starten.

> sudo microk8s.start

![image](https://user-images.githubusercontent.com/63262820/140830352-a62a4cdf-75a0-4a4a-a224-109f1ddbfa38.png)

Nun ist der micro kuberntes Service gestarted und man kann schon Pods starten und benutzen wie zb nginx. Der nächste schritt ist die Verlinkung der Leafnodes mit der Masternode. 

5. Nun müssen wir die Token generieren um die Nodes zu verbinden.

> sudo microk8s.add-node

<img width="570" alt="image" src="https://user-images.githubusercontent.com/63262820/140828626-78a010d1-9305-464c-aaae-c1b0e97a18d9.png">

6. Füge den Token, welchen du auf der Master note erstellt hast bei der Leaf node ein um diese zu verbinden. 

> microk8s.join <master_ip>:<port>/<token>

<img width="570" alt="image" src="https://user-images.githubusercontent.com/63262820/140828575-7ca92c00-b125-4a13-9949-0b02095e62ea.png">

7. Nach abschluss kann man auf dem Master überprüfen, dass die Node eingebunden wurde. 

<img width="522" alt="image" src="https://user-images.githubusercontent.com/63262820/140829776-c323ef1e-4e2c-472a-82a9-fc351ca2d55f.png">

<a name="anker-zur-qualitaet"></a>
## 5. Qualitaetskontrolle (Pruefen der Funktionalitaet mit Ablauf von Kommandos und entsprechenden Outputs)

https://user-images.githubusercontent.com/63262820/140835284-4f6c321b-e5f1-40df-8810-5136d5f19967.mov
		
<a name="anker-zur-error"></a>
## 6. Error-Handling 

1. Erster error welcher auftauchte war, dass der Host 2 (Leaf )konnte keine verbindung zum Host 1(Master) aufnehmen konnte. Als Fehlermeldung bekahm ich  "Connection failed. (500)".

Als gegenmasnahme habe ich geprüft ob ich im Verlauf der Intallation irgendwo die IP gesetzt habe. Zusätzlich habe ich die berechtigungen geprüft.

2. Kurz vor der Abgabe hatten wir einen Teilweisen Stromausfall zuhause bei welchem aufgrund der kurzen leasing dauer der IP. Sich diese für den Master und Leaf gewechselt hatten. So kam ich auch auf die Idee, dass die IP fest eingetragen wurde.

3. Um diese fehler zu eliminieren, habe ich am Abend vor der Abgabe, alles gelöscht und neu erstellt. So wurden alle fehler aus dem Stromausfall und den Testläufen gelöscht und es hat auch viel besser funktioniert wie ich gedacht hätte.

<a name="anker-zur-quellen"></a>
## 7. Quellen

1. https://microk8s.io
2. https://ubuntu.com/tutorials/how-to-kubernetes-cluster-on-raspberry-pi#5-master-node-and-leaf-nodes
3. https://kubernetes.io
4. https://microk8s.io/docs?_ga=2.106751627.928535389.1636302169-1211845305.1635230076

> Alle Bilder welche nicht deklariert wurden sind eigen Produkte(Screenshots, Fotographien, ...)

<a name="anker-zur-lizenz"></a>
## 8. OpenSource Lizenz
****
<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons Lizenzvertrag" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/Text" property="dct:title" rel="dct:type">W15-Kubernetes</span> von <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/Ga1i130/W15-Kubernetes/" property="cc:attributionName" rel="cc:attributionURL">Ga1i130</a> ist lizenziert unter einer <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Namensnennung 4.0 International Lizenz</a>.

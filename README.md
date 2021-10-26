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

Version: V.1.0

<a name="anker-zur-einfuerung"></a>
## 2. Einfuehrung 
   - Kubernetes ist eine Anwendung zum bereitstellen, skalieren und verwalten von Containerumgebungen. Zusammen mit dem Programm microk8s, kann man für Raspberry Pis ein Cluster-System aufbauen.
   - Für dieses Projekt habe ich ca. 12 Lektionen zur Verfügung. In diesen Lektionen, muss ich das System aufsetzten, das gearbeitete Dokumentieren und zum schluss noch die Fehler finden welche ich bei der Installation gemacht habe. 
   - Für mich könnte ich Stolpersteine bei Konfiguration der Raspberrypis haben, denn da wir einen teil in der Schule machen können und den Rest Zuhause muss ich die Konfiguration entweder an einem Morgen durcharbeiten oder das System fest an einem Ort installieren.

<a name="anker-zur-hardsoft"></a>
## 3. Benoetigte Hard- und Software
  - Hardware
   	- Raspberry Pi 4 
   	- Raspberry Pi 3B 
   	- merere MicroSD Karten mit varierenden Grössen (2x 2GB; 1x 16GB; 2x 32GB; 1x 64GB). Diese Speicher Karten kann ich je nach nutzen und Zweck auswählen. Brauche ich viel Speicherplatz? Brauche ich eine Schnellere Karte um die Leistung des Pi's auszunutzen? Wie gross ist die Gefahr eines Bottlenek bei einer langsameren Karte?
![Ohne Titel](https://user-images.githubusercontent.com/63262820/138827765-5e85efd1-cb2e-4e70-8007-9993d56b79f7.png)

  - Die Hardware wird in Zwei Kategorienen eingeteilt den sogenannten nodes.
	- Masternode: Die Masternode ist das Rückgrad des Systemes. Auf dieser node wird ein Ubuntu LST Server image laufen um die vorüge eines Server image ohne GUI zu nutzen. 
	- Leafnode: Diese Nodes werden an die Masternode angehängt und werden mit einem Ubuntu Desktop image bestückt.
  - Diese images werden entweder mit dem Balena Etcher oder dem Raspberri Pi imager auf die Micro SD Karten geladen.

<a name="anker-zur-installation"></a>
## 4. Installationsanleitung (Didaktisch reduzierte Anleitung. Lernende sollen eine eigene Lösungswege realisieren)
   - Anweisungen verstaendlich und nachvollziehbar
   - Keine fertigen Loesungsschritte aufzeigen
   - Hilfestellung (Tipps, Quellen...


<a name="anker-zur-qualitaet"></a>
## 5. Qualitaetskontrolle (Pruefen der Funktionalitaet mit Ablauf von Kommandos und entsprechenden Outputs)

<a name="anker-zur-error"></a>
## 6. Error-Handling 

<a name="anker-zur-quellen"></a>
## 7. Quellen

1. https://microk8s.io
2. https://ubuntu.com/tutorials/how-to-kubernetes-cluster-on-raspberry-pi#5-master-node-and-leaf-nodes
3. https://kubernetes.io
4. 

<a name="anker-zur-lizenz"></a>
## 8. OpenSource Lizenz
****
<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons Lizenzvertrag" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/Text" property="dct:title" rel="dct:type">W15-Kubernetes</span> von <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/Ga1i130/W15-Kubernetes/" property="cc:attributionName" rel="cc:attributionURL">Ga1i130</a> ist lizenziert unter einer <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Namensnennung 4.0 International Lizenz</a>.

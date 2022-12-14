# Prüfungsvorbereitung:

## Kapitel 5 Fragen
**1. Beschreiben Sie den Ablauf der Weiterleitung von IP-Paketen innerhalb eines Routers ("Forwarding"). Gehen Sie dabei auf die Begriffe "Routing-Tabelle", ARP wie auch Default-Gateway ein.**

**2. Was wird unter einem Autonomen System verstanden und wieso wurden Autonome Systeme eingeführt?**
- Abstraktionsschicht zur Skalierung des gesamten IP-Modells.
- Abstraktion von z.B. großen ISP-Netzen/Datacentern
- genaue Struktur innerhalb der abstrahierten Netze unklar, dadurch vereinfachung des Routings

**3. Beschreiben Sie den Gesamtprozess zur Beantragung eines AS wie auch eines providerunabhängigen IP-Ranges.**
- IANA ist die passende Organisation dazu
- diese ist unterteilt in verschiedene Regionale Vertreter
- dort melden und Adressranges usw. beantragen

**4. Was ist der Kernunterschied zwischen Distanzvektorroutingprotokollen und Link-State-Routingprotokollen? Welche Nachteile weisen Distanzverktorroutingprotokolle auf?**
- Bellmann-Ford-Algorithmus als Beispiel für Distanzvektorberechnung
- Distanzvektorroutingprotokolle: Verteilung von Informationen: über folgende Nachbarn erreiche ich für folgende Kosten dieses Ziel!
- Link-State-Funktionsweise: regelmäßiges versenden von Link-State-Advertisements mit Informationen über den Sendenden Router im Netzwerk 
- Vorteil LS: Graph Struktur ableitbar, weil ich weiß, welche Router in welchen Netzen sind usw. 
- Mithilfe Netzstruktur kann ich Routing Optimieren

**5. Wie arbeitet OSPF grundlegend? Gehen Sie dabei auf die Adjazenzbildung wie auch die Verteilung von Link State Advertisements ein.**
- Ausgangspunkt: 
 1. Hello-Pakete an alle Teilnehmer im lokalen Netz versendet
 2. wenn anderer OSPF Nachbar erkannt wird (OSPF Daemon läuft) werden mit Nachbarn Link-State-Advertisements ausgetauscht: (Informationen mit welchen der jeweilige OSPF Nachbar verbunden ist --> jeder OSPF Router weiß dann an welche Netze seine Nachbarn angebunden sind und wie er sie erreicht)
 3. In Areas gegliedert, in einer Area alle Informationen vorhanden, also innerhalb einer Area wissen alle OSPF Router alle Routen/Netze von den Nachbarn
 4. Areaübergreifend dann immer nur Minimale Informationen vorhanden, bsp. weiß ein OSPF Teilnehmer welche mit einer anderen Area verbunden ist dann nur, dass über diese Verbindung die Netze A,B,C erreichbar sind, allerdings nicht welche OSPF Router dort vorhanden sind und deren Struktur

**6. Wozu wurden Areas bei OSPF eingeführt? Welchen Zweck erfüllen sie?**
- Skalierung/Abstraktion
- tauschen von Summary-LSAs (LSAs mit weniger Informationen) zwischen Areas

**7. Wofür wird das Border Gateway Protocol (BGP) eingesetzt? Welche grundlegenden Konfigurationsinformationen müssen für die Konfiguration eines BGP-Routers vorliegen?**
- sorgt für die durchleitung von Daten über Autonome Systeme
- BGP aktualisierung und füllt die lokalen Routing Tabellen von BGP-Routern
- BGP sendet Update Nachrichten an alle angebundenen Teilnehmer
- enthalten darin:
  - ORIGIN: Herkunft der Pfadinformationen: IGP/EGP/INCOMPLETE
  - AS_PATH: bisherigen Pfad von Autonomen Systemen (Angabe der AS-Nummer), den das Update durchlaufen hat
  - NEXT_HOP: IP-Adresse des Routers, der als nächster Router auf dem im Update enthaltenen Pfad verwendet werden sollte

## Kapitel 6 Fragen
**1. Beschreiben Sie die Auflösung von Namen im DNS und gehen Sie dabei auf die Architektur des DNS ein. Gehen Sie dabei auch auf die Begriffe "Zone" und "autoritativer Nameserver" ein.**
- DNS ist ein hierarchisch organisierter Verzeichnisdienst zur Verwaltung von
Informationen über Domänen (vor allem IP-Adressinformationen)
- Domänen-Namensraum ist in **Zonen** untergliedert, die verschiedenen
Nameservern innerhalb der Serverhierarchie zugeteilt werden
- Namensauflösung erfolgt durch Delegation oder Weiterleitung; als Fallback
werden Root-Server in die Auflösung einbezogen
- **autoritativer Nameserver**: Ein autoritativer Nameserver ist verantwortlich für Verwaltung einer Zone (z.B. für Ressource Einträge).

**2. Welche Informationen werden im DNS pro Resource Record gespeichert?**
- Domäne (Root-Level, Top-Level, Second-Level usw.)
- dhge.de. (könnte beispielsweise in einer Zone enthalten sein, für welche ein autoritativer NS die Ressource Einträge Verwaltet)

**3. Nennen und beschreiben Sie vier verschiedene Resource Records.**
- A-Record
  - enthält IPv4 Adresse eines Domainnamen
- NS-Record
  - Nameserver Adressen für weitere Abfrage
- CNAME-Records
  - enthält Alias für einen Domainnamen
- MX-Record
  - enthält Informationen zum Mail-Server einer Domain

**4. Begründen Sie, wieso die Synchronisation von Uhren in Rechnernetzen und Verteilten Systemen eine besondere Herausforderung bildet.**

**5. Wie arbeitet NTP grundlegend?**

**6. Beschreiben Sie den Ablauf, der bei DHCP vorliegt, um automatisch auf ein Interface eine IP-Adresse zuzuweisen.**
- Server, welcher den verfügbaren IP-Adressraum/Subnetz verwaltet und Clients automatisiert die notwendigen IP-Konfiguration mitteilt: IP-Adresse, Default-Gateway

# Prüfungsvorbereitung/Informationen

- ISO/OSI-Referenzmodell // TCP-IP-Modell beherrschen:
  - Schichten beschreiben, welche Funktionen hat welche Schicht
  - Transportschicht: Ende zu Ende Kommunikation
  - Vermittlungsschicht: weltweite Weiterleitung von Daten
  - usw.

- Leitungs-/Paketvermittelte Kommunikation
  - Vor-/Nachteile:
    - Leitungsvermittelt: festgelegte Bandbreite vorhanden (Garantie möglich)
    - Nachteil Leitungsvermittelt: Skalierbarkeit nur schwer, für jede Verbindung MUSS eine seperate Leitung vorhanden sein 
    - Vorteil Paketvermittelt: viele Daten über eine Leitung, effizientere Nutzung der Leitung
    - Nachteil Paketvermittelt: Überlastung der Leitung möglich

- Port-basiert/Tag-basierte VLANs
  - Port an einem Switch wird mit einem bestimmten VLAN konfiguriert, jeder Host der an den Port angeschlossen wird, bekommt das VLAN X zugewiesen (1 VLAN pro Port)
  - im weitern Verlauf wird dann zwischen den Switchen auf TAG-Basiert gewechselt (Port zur Verbindung der Switches muss als Tag-basiert konfiguriert sein, so dass der VLAN Tag ergänz wird und der Empfänger das VLAN wieder zuordnen kann)

- Spanning-Tree-Protokoll
  - niedrigste MAC-Adresse + administrativ vorgegebener Wert wird Root-Bridge
  - beim Anschalten --> Phase 1: alle Teilnehmer senden BPDUs, um ihre eigene Priorität zu verteilen, außerdem gleichen alle Teilnehmer die Emfpangenen Prioritäten mit ihrer eigenen ab, so dass irgendwann genau ein Teilnehmer die höchste Prioriät feststellt
  - Phase 2: STP etabliert innerhalb des Netzes einen Spannbaum durch Blockieren von Ports, die Zyklen erzeugen würden

- IPv4: 
  - Schwächen von IPv4:
    - Effizienzprobleme (Header)
    - keine Automatische Adresskonfiguration (DHCP nötig)
    - zu wenige Adressen
  - Vergleich zu IPv6 darstellen
  - Wie wird ein IP-Paket weitergeleitet/verarbeitet?
  - Fragmentierung, wieso? 
    - weil ansonsten MTU überschritten werden würde
 - Subnetze
   - 192.168.2.0/24 ... 4 Netze die Maximal groß sind?
     - 2 Bit zusätzlich wegen 4 Netzen (00/01/10/11)
     - 192.168.2.0/26
     - 192.168.2.64/26
     - 192.168.2.128/26
     - 192.168.2.192/26

- TCP/UDP
  - Spektrum von Aufgaben: wahr/falsch
    - wenn falsch, korrigieren
    - Vorbereitung: Eigenschaften der Protokolle verinnerlichen:
      - TCP Reihenfolgegarantie - UDP nicht
      - TCP Congestion Control - UDP nicht
      - TCP langsamer - UDP schneller
      - usw.
  - Herausforderung TCP: Man weiß als Sender nicht wie viele Bytes auf den Kanal gesendet werden können. (wie viel Last drauf ist)
    - dynamischer Flaschenhals beim Senden--> Congestion Control Algorithmus
    - versuchen so gut zu erraten, wie die Bedingungen auf dem Pfad sind --> Anhand von 2 Bedingungen: Paketverlust, Pufferstatistiken
  - Nachteile von TCP: 3-Wege-Handshake, ...

- OSPF
  - Open Shortest Path First, wichtigstes Link-State-Ad. Protokoll
  - Ermittlung von Nachbarn mittels bestimmten Paketen
  - erkunden einer Netzwerk-Topologie
  - Ablauf: 
    - Hello-Pakete innerhalb der Area versendet
    - dann Adjanzenzen ausgebildet, wenn Hello, Dead und Area Paramter gleich sind
    - dann Link-State-Advertisements ausgetauscht/ untereinander weitergeleitet: An welchen Schnittstellen bin ich mit welchen Netzen verbunden, so dass jeder Router weiß, welcher Router mit welchen Netzen verbunden ist --> Ausbildung eines Graphen/Topologie
    - kürzeste Pfade mit Dijkstra-Algorithmus ermitteln

- DNS
  - Was ist ein Ressource-Record, Informationen für eine Zone?
  - Was gibt es dort für Einträge?
  - Was ist eine Zone, autoritativer Nameserver, Root-Nameserver?
  - Was ist ein Resolver, Komponente des Betriebssystems um eine einen Nameserver anzusteuern?
  - Wie werden URLs aufgelöst?
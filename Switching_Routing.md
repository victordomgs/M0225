# Switching & Routing

## 1. Fonaments de maquinari i interconnexió

Per entendre com configurar una xarxa, primer cal conèixer els "maons" que la formen. Els dispositius d'interconnexió són els elements clau que permeten que les dades viatgin d'un punt a un altre.

## L'encaminador (router)

L'encaminador és el dispositiu més important de la XAL. La seva missió principal és interconnectar diferents xarxes i permetre la comunicació entre elles.

- **Funcionament:** Treballa fins a la **Capa 3(Xarxa)** del model OSI.
- **Adreçament:** Té assignada una adreça IP i utilitza ports per connectar cada xarxa individual.
- **Decisió de ruta:** Quan rep un paquet, comprova l'adreça de destinació i el transmet pel camí més adient. 

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/M0225/blob/main/images/Image18.png" width="650" height="auto"/>
  </div>

### Arquitectura interna

Un encaminador funciona, en essència, com un ordinador especialitzat i comparteix gairebé tots els seus components.

- **CPU:** Processa les instruccions del sistema i gestiona l'encaminament.
- **RAM (Memòria volàtil):** Emmagatzema la taula d'encaminament i la configuració que s'està executant en el moment (`running-config`).
- **Memòria Flash:** On es desa el sistema operatiu (IOS o Firmware).
- **NVRAM:** Memòria no volàtil on es guarda la configuració d'arrencada (`startup-config`).
- **ROM:** Conté el programari de diagnòstic i les instruccions d'arrencada bàsiques.

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/M0225/blob/main/images/Image19.png" width="600" height="auto"/>
  </div>

### Interfícies i connexions físiques

A la part posterior dels dispositius trobem els punts de connexió amb el món exterior.

- **Ports LAN (Fast Ethernet/Gigabit):** Per a la connexió de dispositius dins de la xarxa local.
- **Ports WAN (Internet):** Per connectar el router cap a una xarxa externa o el mòdem de l'ISP.
- **Ports Sèrie (Serial):** Utilitzats per a connexions punt a punt entre routers de llarga distància; requereixen configurar el `clock rate` en el costat DCE.
- **Port de Consola:** Port especial (normalment de color blau) per a la configuració inicial del dispositiu mitjançant un ordinador i un cable de consola.

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/M0225/blob/main/images/Image20.png" width="600" height="auto"/>
  </div>

## El Commutador (Switch)

Mentre que l'encaminador connecta xarxes entre si, el commutador és el dispositiu encarregat d'interconnectar equips dins d'una mateixa Xarxa d'Àrea Local (XAL). La seva funció principal és gestionar el trànsit de dades de manera eficient i segura a la Capa 2 (Enllaç) del model OSI.

### Com funciona un Switch?

A diferència d'un concentrador (hub), que envia la informació a tots els ports, el switch és "intel·ligent":

- **Aprenentatge d'adreces MAC:** El switch llegeix l'adreça física (MAC) de cada trama que rep i aprèn a quin port està connectat cada dispositiu.
- **Taula de commutació:** Emmagatzema aquestes adreces en una taula interna per saber exactament on enviar cada dada.
- **Forwarding (Reenviament):** Quan arriba un paquet, el switch decideix per quin port l'ha de treure basant-se en la seva taula, evitant saturar la resta de la xarxa.
- **Eliminació de col·lisions:** Cada port del switch és un domini de col·lisió independent, la qual cosa redueix dràsticament la congestió del trànsit.

#### Seguretat i Bucles

Evitació de loops: El switch utilitza protocols (com l'STP) per evitar que les trames facin voltes infinites en la xarxa (cicles o bucles), cosa que podria tombar tota la comunicació.

### Segmentació Avançada: Les VLANs

Un dels grans avantatges dels switches moderns (com el Cisco 2960 de la pràctica) és la capacitat de crear VLANs (Virtual LANs):

- **Definició:** Una VLAN permet dividir una xarxa física en múltiples xarxes lògiques independents.
- **Domini de difusió:** Sense VLANs, tots els ports pertanyen al mateix domini de difusió (broadcast); amb VLANs, creem múltiples dominis per millorar el rendiment i la seguretat.
- **Utilitat:** Quan hi ha molts hosts en una xarxa, augmenten les trames de difusió. Les VLANs serveixen per limitar aquest trànsit i que no afecti equips que no el necessiten.

#### Connexió entre Switches: Trunking

Quan tenim VLANs repartides en més d'un switch, utilitzem ports de tipus Trunk (Troncal):

- Aquests ports permeten que la informació de diverses VLANs viatgi per un sol cable físic entre switches.

<br>

## 2. Lògica de l'Encaminament (Routing)

L'encaminament és el procés de seleccionar camins en una xarxa per enviar paquets de dades cap a la seva destinació final. Per fer-ho, els routers no treballen a cegues; utilitzen estructures de dades i regles lògiques.

### La Taula d'Encaminament

És el "mapa" intern del router. Cada vegada que arriba un paquet, el router consulta aquesta taula per saber per quina interfície ha de sortir.

- **Destinació:** La xarxa a la qual es vol arribar.
- **Mètrica:** El "cost" d'arribar a aquesta xarxa (quantes passes o quin temps triga).
- **Pròxima salt (Next Hop):** L'adreça IP del següent router en el camí.

```
Ideafix# show ip route
Codes: C - connected, S - static, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       ...
Gateway of last resort is not set

      192.168.1.0/24 is directly connected, FastEthernet0/0
R     192.168.3.0/24 [120/1] via 192.168.2.253, 00:00:10, Serial0/0
C     192.168.2.0/24 is directly connected, Serial0/0
```

### Tipus d'Encaminament: Com s'omple la taula?

Segons la pràctica, hi ha dues maneres principals de gestionar com un router coneix les rutes:

#### A. Encaminament Estàtic

L'administrador de la xarxa configura manualment cada ruta en la taula.

- **Avantatges:** Segur i no consumeix recursos (CPU/Ample de banda).
- **Inconvenients:** Si un cable es talla o un router cau, la xarxa no sap buscar un camí alternatiu sola; l'administrador l'ha de canviar a mà.
- **Ús:** Ideal per a xarxes molt petites o rutes per defecte cap a Internet.

#### B. Encaminament Dinàmic

Els routers utilitzen protocols per parlar entre ells i intercanviar informació sobre les xarxes que coneixen.

- **Avantatges:** Són flexibles i s'adapten sols a les fallades de la xarxa.
- **Inconvenients:** Consumeixen una mica de processament i ample de banda per enviar les actualitzacions.

### Protocols d'Encaminament Interior (IGP)

Els apunts i la pràctica es centren en dos protocols clau:

#### 1. RIP (Routing Information Protocol)

- **Lògica:** Es basa en el Vector-Distància.
- **Com funciona:** Només li importa la quantitat de salts (routers) que hi ha fins al destí. El camí amb menys salts és el que tria.
- **Límit:** Té un màxim de 15 salts; a partir d'aquí, considera la xarxa com a inabastable.

#### 2. OSPF (Open Shortest Path First)

- **Lògica:** Es basa en l'Estat de l'Enllaç.
- **Com funciona:** Utilitza un algorisme anomenat SPF (Shortest Path First). No només mira els salts, sinó l'ample de banda (la velocitat).
- **Exemple:** OSPF podria triar un camí de 3 salts si és fibra òptica en lloc d'un camí de 2 salts si és una connexió lenta de coure.

## 3. Segmentació de Xarxes: VLANs

En una xarxa local tradicional, tots els dispositius connectats a un mateix commutador (switch) pertanyen al mateix **domini de difusió**. Això significa que si un ordinador envia un paquet de broadcast, tots els altres equips de la xarxa el rebran i l'hauran de processar, fet que pot provocar congestió.

### Conceptes de Domini de Difusió i VLAN

Una VLAN (Virtual Local Area Network) és una divisió lògica de la xarxa local que crea múltiples dominis de difusió dins d'un mateix entorn físic.

- **Sense VLANs:** Un commutador considera que totes les seves interfícies pertanyen al mateix domini. L'augment d'ordinadors en una XAL provoca un increment massiu de trames de difusió que saturen la xarxa.
- **Amb VLANs:** Es segmenta la xarxa de manera que les trames de difusió només arriben als dispositius que pertanyen a la mateixa xarxa virtual. Això millora el rendiment global i la seguretat, ja que aïlla el trànsit entre departaments o tipus d'usuaris.

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/M0225/blob/main/images/Image21.png" width="600" height="auto"/>
  </div>


### Trunking: Interconnexió entre switches

Quan les VLANs s'han d'estendre a través de diversos commutadors, s'utilitza una configuració especial anomenada Trunking.

- **Enllaç Troncal (Trunk):** És un enllaç punt a punt que connecta dos dispositius de xarxa (com dos switches) i que és capaç de transportar el trànsit de múltiples VLANs simultàniament a través d'un sol cable físic.
- **Etiquetatge:** Perquè el switch receptor sàpiga a quina VLAN pertany cada trama, s'utilitzen protocols d'etiquetatge (com l'estàndard IEEE 802.1Q).
- **Utilitat:** Permet que un usuari de la "VLAN 1" a la planta 1 es comuniqui amb un altre usuari de la "VLAN 1" a la planta 2, sense que aquest trànsit es barregi amb el d'altres xarxes virtuals.

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/M0225/blob/main/images/Image22.gif" width="450" height="auto"/>
  </div>

#### El Router Linksys WRT-54GL

- El router Linksys té un switch intern de 5 ports.
- **VLAN de port d'Internet:** El port WAN (Internet) està físicament en el mateix switch però configurat en una **VLAN diferent** per aïllar la xarxa externa de la interna.

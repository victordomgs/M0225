# Dynamic Host Configuration Protocol (DHCP)

El **Protocol de Configuració Dinàmica d'Host** (DHCP, de l'anglès Dynamic Host Configuration Protocol) és un protocol de gestió de xarxa utilitzat en xarxes de **Protocol d'Internet** (IP) per assignar automàticament adreces IP i altres paràmetres de comunicació als dispositius connectats a la xarxa mitjançant una arquitectura **client-servidor**.

Aquesta tecnologia elimina la necessitat de configurar manualment i individualment cada dispositiu de xarxa. Consta de dos components: un servidor DHCP instal·lat centralment i instàncies de client de la pila de protocols en cada ordinador o dispositiu. Quan es connecta a la xarxa, i periòdicament a partir de llavors, un client sol·licita un conjunt de paràmetres al servidor mitjançant el DHCP.

### Implementació i abast

El DHCP es pot implementar en xarxes de diverses mides:

- **Xarxes residencials** (domèstiques).
- **Xarxes de campus** de gran escala.
- **Xarxes regionals d'ISP** (proveïdors de serveis d'Internet).

Molts encaminadors (**routers**) i passarel·les residencials tenen capacitat de servidor DHCP. La majoria dels routers domèstics reben una adreça IP única dins de la xarxa de l'ISP, mentre que, dins d'una xarxa local, el servidor DHCP assigna una adreça IP local a cada dispositiu.

### Versions del Protocol

Els serveis DHCP existeixen tant per a xarxes que funcionen amb el Protocol d'Internet versió 4 (IPv4) com per a la versió 6 (IPv6). La versió del protocol per a IPv6 s'anomena comunament DHCPv6.

---

## Funcionament i assignació d'adreces

El **Protocol d'Internet (IP)** defineix com es comuniquen els dispositius dins i a través de les xarxes locals a Internet. Un servidor DHCP pot gestionar la configuració IP dels dispositius de la seva xarxa local, per exemple, assignant-los adreces IP de manera automàtica i dinàmica.

El DHCP funciona basant-se en el model client-servidor. Quan un ordinador o un altre dispositiu es connecta a una xarxa, el programari client DHCP envia una consulta de difusió (broadcast) sol·licitant la informació necessària. Qualsevol servidor DHCP de la xarxa pot atendre la petició.

El servidor DHCP gestiona un grup (pool) d'adreces IP i informació sobre els paràmetres de configuració del client, com ara:

- **Pasarel·la predeterminada** (default gateway).
- **Nom de domini**.
- **Servidors de noms** (DNS) i **servidors horaris**.

En rebre una sol·licitud DHCP, el servidor pot respondre amb informació específica per a cada client (segons hagi configurat prèviament un administrador) o amb una adreça específica i qualsevol altra informació vàlida per a tota la xarxa i pel període de temps en què l'assignació (**concessió** o lease) sigui vigent. Un client DHCP sol demanar aquesta informació immediatament després d'arrencar, i periòdicament abans que la informació caduqui. Quan un client renova una assignació, inicialment sol·licita els mateixos valors, però el servidor pot assignar una adreça nova segons les polítiques establertes.

En xarxes grans que consten de múltiples enllaços, un sol servidor DHCP pot donar servei a tota la xarxa amb l'ajuda d'**agents de relleu DHCP** (relay agents) situats en els encaminadors d'interconnexió. Aquests agents retransmeten els missatges entre els clients i els servidors DHCP situats en diferents subxarxes.

### Mètodes d'assignació d'adreces IP

Depenent de la implementació, el servidor DHCP pot utilitzar tres mètodes per assignar adreces:

1. **Assignació dinàmica:** Un administrador de xarxa reserva un rang d'adreces IP per al DHCP. Cada client de la xarxa local (LAN) està configurat per sol·licitar una adreça durant la inicialització de la xarxa. El procés utilitza el concepte de concessió amb un període de temps controlable, permetent al servidor recuperar i reassignar les adreces IP que no es renovin.

2. **Assignació automàtica:** El servidor DHCP assigna permanentment una adreça IP d'un rang definit. És similar a la dinàmica, però el servidor manté una taula de les assignacions passades per intentar assignar al client la mateixa adreça que tenia anteriorment.

3. **Assignació manual:** També anomenada DHCP estàtic, assignació d'adreça fixa, reserva o vinculació d'adreça MAC/IP. L'administrador mapeja un identificador únic (l'ID de client o l'adreça MAC) de cada dispositiu a una adreça IP específica.

---

## El Model de Servei i el Procés DORA

El DHCP utilitza un model de servei **sense connexió** basat en el **Protocol de Datagrames d'Usuari** (UDP). Per a les seves operacions, s'implementa amb dos números de port UDP que són els mateixos que s'utilitzaven en el protocol d'arrencada (BOOTP):

- El **servidor** escolta al port UDP **67**.
- El **client** escolta al port UDP **68**.

Les operacions del DHCP es divideixen en quatre fases: descobriment del servidor, oferta de concessió d'IP, sol·licitud de concessió d'IP i reconeixement de la concessió d'IP. Aquestes etapes s'abreugen sovint com a DORA (Discovery, Offer, Request, Acknowledgement).

### Funcionament de l'Operació

L'operació del DHCP comença quan els clients envien una sol·licitud per **difusió** (*broadcast*). Si el client i el servidor es troben en dominis de difusió diferents, es pot utilitzar un **ajudant DHCP** o un **agent de relleu DHCP**.

Els clients que sol·liciten la **renovació** d'una concessió existent es poden comunicar directament mitjançant **unicast** UDP, ja que en aquest punt el client ja té una adreça IP establerta.

A més, existeix un **indicador de difusió** (*BROADCAST flag*), que és 1 bit en un camp d'indicadors de 2 bytes (on la resta de bits estan reservats i establerts a 0). El client pot utilitzar aquest bit per indicar de quina manera pot rebre el missatge `DHCPOFFER`:

- `0x8000` per a difusió (*broadcast*).
- `0x0000` per a unidifusió (*unicast*).

Normalment, el `DHCPOFFER` s'envia mitjançant unicast. Per a aquells equips (*hosts*) que no poden acceptar paquets unicast abans de tenir configurades les adreces IP, aquest indicador es pot utilitzar per solucionar el problema.

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/M0225/blob/main/images/Image13.png" width="450" height="auto"/>
  </div>

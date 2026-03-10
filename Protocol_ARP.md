# Address Resolution Protocol (ARP)

En xarxes de computació, el **protocol de resolució d'adreces** (**ARP**, de l'anglès Address Resolution Protocol) és un protocol de comunicacions de la **capa d'enllaç de dades**. És el responsable de trobar l'adreça de maquinari (**Ethernet MAC**) 
que correspon a una determinada **adreça IP**.

## Com funciona el procés?

1. **ARP Request:** S'envia una trama a l'adreça de difusió de la xarxa (broadcast, MAC = `FF:FF:FF:FF:FF:FF`) que conté l'adreça IP per la qual es pregunta.
2. **ARP Reply:** S'espera que aquesta màquina (o una altra) respongui amb l'adreça Ethernet que li correspon.
3. **Taula cau:** Cada màquina manté una memòria cau (cache) amb les adreces traduïdes per reduir el retard i la càrrega de la xarxa.

L'objectiu de l'ARP, explicat de manera senzilla, és permetre que un dispositiu connectat a una **xarxa LAN** obtingui l'adreça MAC d'un altre dispositiu de la mateixa xarxa del qual ja coneix l'adreça IP. Això permet que l'adreça d'Internet 
sigui independent de l'adreça física de la targeta de xarxa.

<br>

## Taules ARP

er exemplificar-ho: per localitzar el senyor "XY" entre 150 persones, es pregunta pel seu nom a tothom i el senyor "XY" ha de respondre.

Quan a l'equip A li arriba un missatge amb una adreça IP d'origen i no té aquesta adreça a la memòria cau de la seva taula ARP, enviarà una trama ARP a l'adreça de difusió (broadcast, física = `FF:FF:FF:FF:FF:FF`), amb la IP de la qual vol conèixer l'adreça física. Llavors, l'equip l'adreça IP del qual coincideixi amb la pregunta respondrà a A enviant-li la seva adreça física. En aquest moment, A ja pot afegir l'entrada d'aquesta IP a la seva taula ARP.

Les entrades de la taula s'esborren periòdicament, ja que les adreces físiques de la xarxa poden canviar (per exemple, si s'espatlla una targeta de xarxa i cal substituir-la, o si un usuari canvia la seva adreça IP).

<br>

## Reverse ARP (RARP)

El **RARP** és un protocol per obtenir l'adreça IP pertanyent a un maquinari electrònic determinat, utilitzat majoritàriament en xarxes Ethernet (definit a la RFC 903).

- **Estat actual:** El RARP ja no es fa servir; va ser reemplaçat pel BOOTP i, més tard, pel DHCP.
- **Funcionament:** Utilitza el mateix mecanisme que l'ARP, però la resposta és l'adreça de protocol de l'estació d'origen, no la de l'estació de destí.
- **Requisit:** Totes les adreces MAC han d'estar configurades en un servidor central.
- **Disponibilitat:** A part d'Ethernet, està disponible en xarxes FDDI i Token Ring.

<br>

## Inverse ARP (InARP)

La funció de l'**InARP** és traduir les adreces de la **capa d'enllaç de dades** (capa 2) a adreces de la **capa de xarxa** (capa 3).

- **Eficiència:** És més efectiu que enviar missatges ARP en cada circuit virtual i més flexible que una configuració estàtica.
- **Diferència clau:** No envia sol·licituds perquè ja coneix l'adreça de l'estació de destí.
- **Freqüència:** S'executa cada 60 segons per defecte en circuits virtuals actius.
- **Implementació:** S'utilitza el mateix format de paquet que l'ARP, però amb un codi d'operació diferent.

<br>

## ARP Proxy

La tècnica **ARP Proxy** consisteix en el fet que un amfitrió (host), generalment un encaminador (router), respon a peticions ARP destinades a un host que es troba fora de la xarxa local. En "fingir" la seva identitat, l'encaminador es fa responsable d'encaminar el paquet cap al seu destí real.

### Usos i avantatges

- Permet que equips d'una subxarxa arribin a xarxes remotes sense haver de configurar l'encaminament o la porta d'enllaç predeterminada (default gateway).
- És útil en implementacions antigues d'IPv4 o quan un host té una màscara de xarxa mal configurada i creu que el destí és local quan no ho és.
- Avantatge principal: Es pot afegir a un sol encaminador sense distorsionar les taules d'altres equips de la xarxa.

### Desavantatges

- **Trànsit:** Augmenta la quantitat de trànsit ARP en el segment.
- **Escalabilitat:** Requereix taules ARP molt grans per gestionar les assignacions.
- **Seguretat:** La xarxa queda exposada al spoofing (un host pot suplantar-ne un altre per interceptar paquets).

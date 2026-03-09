# Domain Name System (DNS)

El **sistema de noms de domini** (Domain Name System o **DNS**, per les seves sigles en anglès) és un sistema de nomenclatura jeràrquic descentralitzat per a dispositius connectats a **xarxes IP**, com Internet o una xarxa privada. Aquest sistema associa informació variada amb noms de domini assignats a cadascun dels participants.

La seva funció més important és la **resolució de noms**: «traduir» noms intel·ligibles per a les persones en identificadors binaris associats amb els equips connectats a la xarxa, amb el propòsit de poder localitzar i adreçar aquests equips mundialment.

### Funcionament i usos principals

El servidor DNS utilitza una base de **dades distribuïda i jeràrquica** que emmagatzema informació associada a noms de domini. Tot i que el DNS és capaç d'associar diferents tipus d'informació a cada nom, els usos més comuns són:

- Assignació de noms de domini a adreces IP.
- Localització dels servidors de correu electrònic de cada domini.

L'assignació de noms a adreces IP és, certament, la funció més coneguda. Per exemple, si l'adreça IP del lloc de Google és `216.58.210.163`, la majoria de la gent arriba a aquest equip especificant `www.google.com` i no l'adreça IP.

### Avantatges del sistema

A més de ser més fàcil de recordar, el nom és més fiable:

1. **Flexibilitat:** L'adreça numèrica podria canviar per moltes raons sense que calgui canviar el nom del lloc web.
2. **Optimització (CDN):** En el cas que una pàgina web utilitzi una xarxa de distribució de continguts (Content Delivery Network o **CDN**), el DNS permet que l'usuari rebi l'adreça IP del servidor més proper segons la seva localització geogràfica.

<br>

## Interacció de l'usuari i el procés de consulta

Els usuaris generalment no es comuniquen directament amb el servidor DNS: la resolució de noms es fa de forma transparent mitjançant les **aplicacions del client** (per exemple, navegadors, clients de correu i altres aplicacions que fan servir Internet).

En realitzar una petició que requereix una cerca de DNS, aquesta s'envia al servidor DNS local del **sistema operatiu**. Abans d'establir qualsevol comunicació, el sistema operatiu comprova si la resposta es troba a la **memòria cau** (cache). En cas que no hi sigui, la petició s'enviarà a un o més servidors DNS:

- L'usuari pot utilitzar els servidors propis del seu **ISP** (proveïdor d'Internet).
- Pot fer servir un **servei gratuït** de resolució de dominis.
- Pot contractar un **servei avançat de pagament**, habitualment escollits per empreses per la seva rapidesa i seguretat.

La majoria d'usuaris domèstics utilitzen el servidor proporcionat pel seu proveïdor, tret d'aquells que personalitzen els seus equips o encaminadors (routers) per a servidors públics determinats. La configuració d'aquests servidors pot ser **manual o automàtica** mitjançant el protocol **DHCP** (IP dinàmica). En altres casos, els administradors de xarxa tenen configurats els seus propis servidors DNS.

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/M0225/blob/main/images/Image16.png" width="750" height="auto"/>
  </div>

En qualsevol cas, els servidors DNS que reben la petició busquen primer si disposen de la resposta a la seva memòria cau. Si és així, serveixen la resposta; en cas contrari, iniciarien la **cerca de manera recursiva**. Una vegada trobada la resposta, el servidor DNS desarà el resultat a la seva memòria cau per a usos futurs i retornarà el resultat al client.

Respecte als protocols de xarxa, el DNS funciona de la següent manera:

| Protocol | Ús principal | Raó |
| :--- | :--- | :--- |
| **UDP** | Peticions i respostes estàndard entre client i servidor. | És molt més ràpid per a operacions lleugeres. |
| **TCP** | Respostes superiors a 512 bytes (ex. DNSSEC) o transferències de zona. | Ofereix més fiabilitat en l'intercanvi de dades grans o entre servidors. |

<br>

## L'espai de noms de domini

L'espai de noms de domini té una estructura arborescent. Les fulles i els nodes de l'arbre s'utilitzen com a etiquetes dels mitjans. Un nom de domini complet d'un objecte consisteix en la concatenació de totes les etiquetes d'un camí.

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/M0225/blob/main/images/Image17.png" width="650" height="auto"/>
  </div>

Les etiquetes són cadenes alfanumèriques (amb l'ús del guionet «-» com a únic símbol permès), han de tenir almenys un caràcter i un màxim de 63 caràcters de longitud, i han de començar amb una lletra (mai amb un guionet).

- **Format:** Les etiquetes individuals estan separades per punts.
- **FQDN:** Un nom de domini correctament format (**FQDN**, per les seves sigles en anglès) acaba amb un punt, per exemple: `www.exemple.com` (tot i que aquest últim punt normalment s'omet per ser purament formal).
- **Longitud:** Un nom de domini ha d'incloure tots els punts i té una longitud màxima de 255 caràcters.
- **Jerarquia:** Es llegeix sempre de dreta a esquerra. El punt de l'extrem dret separa l'etiqueta arrel de la jerarquia. Aquest primer nivell es coneix com a domini de nivell superior (**TLD**, per les seves sigles en anglès).

Els objectes d'un domini DNS (com el nom d'un equip) es registren en un fitxer de zona, ubicat en un o més servidors de noms.

### Tipus de servidors DNS

Segons la seva funció, els servidors es classifiquen en:

| Tipus de Servidor | Funció Principal | Característiques |
| :--- | :--- | :--- |
| **Primaris (Mestres)** | Emmagatzematge original | Guarden les dades d'un espai de noms en els seus propis fitxers de zona. Són l'autoritat principal. |
| **Secundaris (Esclaus)** | Replicació i suport | Obtenen les dades dels servidors primaris mitjançant una **transferència de zona**. Milloren la disponibilitat. |
| **Locals (Caché)** | Agilització de consultes | No tenen la base de dades original. Consulten a altres servidors i guarden la resposta per a futures peticions. |

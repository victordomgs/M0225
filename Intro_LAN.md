# Introducció a les LAN i interconnexió d'equips

<br>

## Exemple 1 — Connexió directa entre dos ordinadors (mateixa xarxa)

Anem a entendre la comunicació bàsica entre dos equips dins **la mateixa xarxa** i verificar que aquesta connexió funciona.

#### Lògica de xarxa al darrere

- Dues màquines en la **mateixa xarxa** (mateixa IP de xarxa i màscara) es poden comunicar **sense router**.
- No cal afegir una **porta d'enllaç (gateway)** perquè no sortim de la xarxa local.
- Per connexions PC↔PC, fem servir **cable creuat (Copper Cross-Over)**.

A continuació podem veure una configuració que ens permetria connectar aquests dos ordinadors. 

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/M0225/blob/main/images/Image1.png" width="650" height="auto"/>
  </div>

Recordeu que: 

- ```192.168.100.10 (PC0)``` i ```192.168.100.11 (PC1)```: és **l’adreça única** de cada ordinador dins la xarxa. Serveix per identificar-los i permetre la comunicació entre ells.
- ```255.255.255.0```: indica **quina part de la IP identifica la xarxa i quina part identifica l’equip (host).**

En definitiva, els **primers 3 octets** (```192.168.100```) identifiquen la xarxa. L’**últim octet** (el ```.10```, ```.11```, etc.) identifica **cada dispositiu dins d’aquesta xarxa.**

Per tant, la xarxa és ```192.168.100.0``` i les adreces vàlides per als equips van de ```192.168.100.1``` fins a ```192.168.100.254```.

- ```192.168.100.0``` és l’**adreça de xarxa** (no es pot assignar).
- ```192.168.100.255``` és l’**adreça de difusió (broadcast)**.

<br>

## Exemple 2 — Dos ordinadors connectats a un Hub

Anem a entendre com funciona un hub i veure que permet la comunicació dins la mateixa xarxa, però **reprodueix tot el trànsit** a tots els ports.

#### Lògica de xarxa al darrere

- El hub és un dispositiu de **nivell físic (nivell 1 OSI)**: simplement **replica els senyals** que rep per un port a tots els altres.
- Tots els equips connectats al hub **comparteixen el mateix domini de col·lisió**.
- Si les IP pertanyen a la mateixa xarxa, poden comunicar-se sense problemes.

A continuació podem veure una configuració que ens permetria connectar aquests dos ordinadors a través d'un hub.

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/M0225/blob/main/images/Image2.png" width="650" height="auto"/>
  </div>

Fixeu-vos que necessitarem seguir la mateixa lògica de l'exemple 1. **Les IPs han d'estar en la mateixa xarxa**. En aquest cas, la diferencia es que necessitarem dos **cables directes (Copper Straight-Through)** per connectar cada PC al hub.

**Diferencia amb switch:** el hub no aprèn adreces MAC, envia tot a tothom. 

Si afegim un tercer PC veurem que quan un envia un ping, tots reben còpia del paquet en Simulation Mode. Això no és eficient en xarxes grans ja que genera col·lisions i trànsit innecessari.

<br>

## Exemple 3 — Dos ordinadors connectats a un Switch

Anem a entendre com el switch optimitza la comunicació dins la mateixa xarxa local, evitant el trànsit innecessari que generava el hub.

#### Lògica de xarxa al darrere

- El switch treballa al **nivell 2 (enllaç de dades)** del model OSI.
- Aprèn les **adreces MAC** dels dispositius connectats i associa cada MAC a un port concret.
- Quan un rep un paquet, només el reenvia pel port del destí, no a tots.
- Això redueix col·lisions i millora el rendiment de la xarxa.

Fixeu-vos que necessitarem seguir la mateixa lògica de l'exemple 1 i l'exemple 2. **Les IPs han d'estar en la mateixa xarxa**. En aquest cas, necessitarem dos **cables directes (Copper Straight-Through)** per connectar cada PC al switch.

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/M0225/blob/main/images/Image3.png" width="650" height="auto"/>
  </div>

En Simulation Mode, veuràs que el switch primer envia el paquet a tots els ports, però després “aprèn” la MAC de cada PC i només reenviarà pels ports corresponents.

<br>

## Exemple 4 — Connexió amb Router (dues xarxes diferents)

Anem a entendre la funció del router com a dispositiu que permet la comunicació **entre xarxes diferents** a través de les seves interfícies.

#### Lògica de xarxa al darrere

- Cada interfície del router pertany a una **xarxa diferent**.
- Els ordinadors d’una xarxa utilitzen el router com a **porta d’enllaç (gateway)** per accedir a altres xarxes.
- Quan un paquet ha de sortir de la xarxa local, s’envia a la **default gateway**, i el router decideix per on encaminà-lo.

En aquest cas, necessitarem dos **cables directes (Copper Straight-Through)** per connectar cada PC al switch.

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/M0225/blob/main/images/Image4.png" width="650" height="auto"/>
  </div>

- El PC4 el connectem a través de la interfície Fa0/0, li afegim la IP 192.168.2.10 i la porta d'enllaç 192.168.2.1. Com que la submàscara és 255.255.255.0. Aquesta màquina es troba a la xarxa 192.168.2.
- El PC5 el connectem a través de la interfície Fa0/1, li afegim la IP 192.168.1.15 i la porta d'enllaç 192.168.1.1. Com que la submàscara és 255.255.255.0. Aquesta màquina es troba a la xarxa 192.168.1.

Molt important, desprès configurem la IP de cada interfície corresponent del router amb la porta d'enllaç definida en cada una de les xarxes. D'aquesta manera cada PC pertany a una d’aquestes xarxes i utilitza la IP del router dins la seva xarxa com a **porta d’enllaç**.

<br>

## Exemple 5 — Connexió entre dos Routers

Anem a entendre com dos routers poden connectar diferents xarxes i permetre la comunicació entre ordinadors de subxarxes separades mitjançant **rutes estàtiques**.

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/M0225/blob/main/images/Image5.png" width="650" height="auto"/>
  </div>

#### Lògica de xarxa al darrere

- Cada router connecta **dues xarxes diferents**: una local (LAN) i una de connexió entre routers (WAN).
- Perquè les dades arribin a la destinació correcta, cada router ha de saber **què hi ha a l’altra banda**.
- Aquesta informació s’afegeix amb **rutes estàtiques** que indiquen: “Per arribar a la xarxa X, envia els paquets a través de la IP Y”.

Anem a veure en detall la xarxa. Teni una connexió creada entre dos routers: 
- **Router4 (interfície cap a Router 5):** IP 10.2.2.1
- **Router5 (interfície cap a Router 4):** IP 10.2.2.2
- **Màscara:** 255.0.0.0 (indica que la xarxa és 10.0.0.0)

Això significa que **Router4** i **Router5** estan en la mateixa xarxa 10.0.0.0/8 i poden comunicar-se directament.

A part d'això, tenim creade dos xarxes: **LAN6** i **LAN7**. En aquest cas la connexió es realitza de la mateixa manera que a l'exemple 4. 

<br>

## Refresquem que és una submàscara de xarxa

Una **submàscara** (o subnet mask) serveix per **dividir una adreça IP** en dues parts:

```[ part de xarxa ] [ part d’host ]```

- La **part de xarxa** identifica la xarxa a la qual pertany el dispositiu.
- La **part d'host** identifica el dispositiu concret dins d'aquella xarxa.

#### Exemple bàsic

Suposem que tenim la IP: 

```192.168.1.14  amb la submàscara 255.255.255.0```

Recordem que la transformació en binari seria:

- **Adreça IP:** 192.168.1.14 → 11000000.10101000.00000001.00001110
- **Submàscara:** 255.255.255.0 → 11111111.11111111.11111111.00000000

La submàscara té **24 bits posats a 1**, o sigui ```/24```.

Això vol dir: 
- Els **24 primers bits** són la part de **xarxa** → ```192.168.1```
- Els **8 últims bits** són la part de **host** → ```14```

Quan dos ordinadors poden comunicar-se **sense passar per un router** vol dir que **pertanyen a la mateixa xarxa**. És a dir, tenen la mateixa part de xarxa segons la submàscara. 

#### Com sap un ordinador si l'altre és de la seva xarxa?

Quan un ordinador vol enviar un paquet: 

1. Fa una **operació AND** entre la seva IP i la seva submàscara.
2. Fa el mateix amb la IP de destinació i la seva pròpia submàscara.
3. Si el resultat és **el mateix**, l'altre està a la mateixa xarxa → envia directament.
4. Si és **diferent**, envia el paquet al **gateway (router)**.

Per exemple, si el PC IP: 192.168.1.10 / 255.255.255.0 vol parlar amb 192.168.2.50:

```
192.168.1.10  AND 255.255.255.0 = 192.168.1.0 / 192.168.2.50  AND 255.255.255.0 = 192.168.2.0
````

Com que no són iguals → PC1 sap que ha d’enviar el paquet al router.

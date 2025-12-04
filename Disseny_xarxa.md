# Disseny de xarxa

Aquesta xarxa simula un edifici amb tres plantes i un CPD central. La infraestructura està organitzada de manera que cada planta disposa de la seva pròpia VLAN i el CPD té una VLAN específica per als servidors.
La comunicació entre VLANs es realitza mitjançant un **router-on-a-stick**.

Recordem, que com s'ha determinat aquests dies enrere a la pràctica, els components que farem servir són els següents:

#### Equipament per planta (0, 1 i 2):

- 1 switch d'accés (2960).
- Diferents PCs.
- 1 impressora.
- 1 access point.

#### CPD:

- 1 switch central (2960).
- Servidor de domini de Windows.
- Servidor de correu.
- Servidor web.
- Servidor de fitxers.

#### Accés a Internet:

- Router WAN.
- Enllaç al router intern de l'edifici.

<br>

## Esquema de connexió física

| Element                        | Connectat a                         |
| ------------------------------ | ----------------------------------- |
| Router Intern (G0/0)           | Switch Central (Trunk)              |
| Switch Central (access ports)  | Switch Planta 0, Planta 1, Planta 2 |
| Servidors del CPD              | Switch Central                      |
| PCs de cada planta             | Switch de la planta                 |
| AP i Impressora de cada planta | Switch de la planta                 |

<br>

## Esquema de VLANs

| VLAN | Nom          | Ubicació | Ús                              |
| ---- | ------------ | -------- | ------------------------------- |
| 10   | VLAN_Planta0 | Planta 0 | PCs i impressora                |
| 20   | VLAN_Planta1 | Planta 1 | PCs i impressora                |
| 30   | VLAN_Planta2 | Planta 2 | PCs i impressora                |
| 40   | VLAN_Serveis | CPD      | Servidors DNS, Web, DHCP, Files |
| 99   | VLAN_Gestio  | Switches | Administració                   |

<br>

## Esquema d'adreçament IP

| VLAN | Subxarxa        | Gateway (subinterface router) |
| ---- | --------------- | ----------------------------- |
| 10   | 192.168.10.0/24 | 192.168.10.1                  |
| 20   | 192.168.20.0/24 | 192.168.20.1                  |
| 30   | 192.168.30.0/24 | 192.168.30.1                  |
| 40   | 192.168.40.0/24 | 192.168.40.1                  |
| 99   | 192.168.99.0/24 | 192.168.99.1                  |

Les adreces de servidors recomanades són: 

| Servei                                       | IP Recomanada     | Motiu                              |
| -------------------------------------------- | ----------------- | ---------------------------------- |
| **Controlador de domini Windows (AD + DNS)** | **192.168.40.10** | Primer servidor crític de la xarxa |
| **Servidor de correu**                       | **192.168.40.20** | Segon servei principal             |
| **Servidor web**                             | **192.168.40.30** | Servei públic intern               |
| **Servidor de fitxers**                      | **192.168.40.40** | Servei d’emmagatzematge            |

<br>

## Configurem desde terminal la nostra xarxa

#### 1. Anem a configurar el Switch Central (2960)

Primer de tot, crearem les VLANs pertinents desde el CLI: 

```pgsql
enable
configure terminal

vlan 10
name Planta0

vlan 20
name Planta1

vlan 30
name Planta2

vlan 40
name Serveis

vlan 99
name Gestio
```

Seguidament, configurarem *trunk* cap al router. Assumint que el port és Fa0/1:

```kotlin
interface fa0/1
switchport mode trunk
switchport trunk allowed vlan 10,20,30,40,99
```

> [!NOTE]  
> Un **trunk** és un tipus d’enllaç entre dispositius de xarxa (normalment entre switches, o entre un switch i un router) que  permet transportar **diverses VLANs alhora per un mateix cable**. En lloc de tenir un cable per a cada VLAN, el trunk encapsula els marcs Ethernet afegint-hi una etiqueta (tag 802.1Q) que indica a quina VLAN pertany cada trama. Així, múltiples xarxes virtuals poden circular per un sol enllaç físic de manera separada i segura. 

Ara, configurem *trunk* cap als switches de planta. Assumint que els ports són Fa0/2, Fa0/3 i Fa0/4: 

```go
interface range fa0/2 - 4
switchport mode trunk
switchport trunk allowed vlan 10,20,30,40,99
```

Finalment, assignem VLAN 40 als ports servidors:

```pgsql
interface range fa0/10 - 13
switchport mode access
switchport access vlan 40
```

#### 2. Configurem el router-on-a-stick

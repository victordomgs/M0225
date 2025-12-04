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

## Configuració dels switches


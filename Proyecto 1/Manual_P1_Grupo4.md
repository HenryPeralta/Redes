Universidad San Carlos de Guatemala <br>
Facultad de Ingeniería <br>
Escuela de Ciencias y Sistemas <br>
Redes de computadoras 1 sección Q <br>
Ing. Allan Alberto Morataya Gómez <br>
Aux. Jorge David Ambrosio Ventura <br>
<br>
<br>
### <center>Manual de configuración proyecto 1 </center>
<br>
<br>
  

| Nombre | Carnet |
|--|--|
| Pablo José Oliva Bonilla | 201700898 |
| Henry Gabriel Peralta Martinez | 201712289 |
| Josseline Suseth Godinez Garcia | 201503841|
| Aybson Diddiere Mercado Grijalva | 201700312|
  

# Manual de configuración

### Herramientas necesarias
- 4 PC/Laptop con sistema operativo libre.
### Software
- GNS3 instalados en los hosts fisicos.
- OpenVPN.
- Cloud Platform.
- VMware

### Topología 1
![enter image description here](https://i.ibb.co/jL1HM4g/Whats-App-Image-2022-08-28-at-11-47-16-PM.jpg)

### Topología 2
![enter image description here](https://i.ibb.co/mCCtg6W/Whats-App-Image-2022-08-28-at-11-47-16-PM-1.jpg)

### Topología 3
![enter image description here](https://i.ibb.co/7Cwf4YR/Whats-App-Image-2022-08-28-at-11-47-16-PM-2.jpg)

### Requerimiento para ejecutar el archivo GNS3
Para correr el archivo gns3 sin ningun problema se necesita lo siguiente:

 - Que cada compañero tenga una topología.
 - Estar conectados a una vpn y comprobar que todos pueden hacerse ping.
 - configurar la nube de gns3 con los puertos correctos para conectarlos con los demás compañeros, configurar los tunels UDP  y configurar los switches a troncal o acceso dependiendo la topología.
 - Tener las maquinas virtuales y configurarlas cambiando su ip, mascara de red y gateway, y conectarlas a la topología.
 - Crear las VLANS con su dirección de red dependiendo de su zona.
 - Configurar los modos cliente y transparente.

### Maquina Virtual
![enter image description here](https://i.ibb.co/yWGwqdW/maquina-virtual.png)

### Comandos utilizados 
#### CREAR EN SW4
conf t <br>
hostname ESW4 <br>
vlan 10 <br>
name RRH <br>
vlan 20 <br>
name INFORMATICA <br>
vlan 30 <br>
name CONTABILIDAD <br>
vlan 40 <br>
name VENTAS <br>

#### CONFIGURAR MODO SERVER EN SW4

conf t <br>
vtp version 2 <br>
vtp mode server <br>
vtp domain GRUPO4 <br>
vtp password grupo4 <br>

#### CONFIGURAR MODO CLIENTE EN SW1 - SW3, SW5 - SW 10

conf t <br>
vtp mode client <br>
vtp domain GRUPO4 <br>
vtp password grupo4 <br>

#### CONFIGURAR MODO TRANSPARENTE EN SW11 

conf t <br>
vtp mode transparent <br>
vtp domain GRUPO4 <br>
vtp password grupo4 <br>

### CONFIGURAR BRIDGE ROOT STP EL SW4 

conf t <br>
spanning-tree vlan 1 root primary <br>
spanning-tree vlan 10 root primary <br>
spanning-tree vlan 20 root primary <br>
spanning-tree vlan 30 root primary <br>
spanning-tree vlan 40 root primary <br>


description HACIA_ESW9 <br>
switchport trunk encapsulation dot1q <br>
switchport mode trunk <br>
switchport trunk allowed vlan 1,10,20,30,40,1002-1005 <br>

#### MODO ACCESO
Conf t <br>
Int f#/# <br>
Switchport mode Access <br>
Switchport Access vlan # <br>
Do wri <br>
End <br>

#### MODO TRONCAL
Conf t <br>
Int f#/# <br>
Switchport mode trunk <br>
Switchport trunk allowed vlan 1,#,#,1002-1005 <br>
Do wri <br>
End <br>

#### CONFIGURACION VTP
Conf t <br>
Vtp domain nombredeldominio <br>
Vtp password contraseñadeldominio <br>
Vtp mode server|client|transparent <br>
Do wri <br>
End <br>

#### PORT CHANNEL
Conf t <br>
Interfaces range f#/#-# <br>
Channel-group # mode on <br>
Do wri <br>
End <br>

#### CONFIGURACION VLAN
Conf t <br>
Vlan numerodevlan <br>
Name nombredevlan <br>
Do wri <br>
End <br>

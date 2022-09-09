Universidad San Carlos de Guatemala 
Facultad de Ingeniería 
Escuela de Ciencias y Sistemas
Redes de computadoras 1 sección Q
Ing. Allan Alberto Morataya Gómez
Aux. Jorge David Ambrosio Ventura
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
conf t 
hostname ESW4
vlan 10 
name RRH
vlan 20
name INFORMATICA
vlan 30
name CONTABILIDAD
vlan 40
name VENTAS

#### CONFIGURAR MODO SERVER EN SW4

conf t 
vtp version 2
vtp mode server
vtp domain GRUPO4
vtp password grupo4

#### CONFIGURAR MODO CLIENTE EN SW1 - SW3, SW5 - SW 10

conf t
vtp mode client
vtp domain GRUPO4
vtp password grupo4

#### CONFIGURAR MODO TRANSPARENTE EN SW11 
conf t 
vtp mode transparent
vtp domain GRUPO4
vtp password grupo4

### CONFIGURAR BRIDGE ROOT STP EL SW4 

conf t
spanning-tree vlan 1 root primary
spanning-tree vlan 10 root primary 
spanning-tree vlan 20 root primary 
spanning-tree vlan 30 root primary 
spanning-tree vlan 40 root primary


description HACIA_ESW9
switchport trunk encapsulation dot1q 
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005

#### MODO ACCESO
Conf t
Int f#/#
Switchport mode Access
Switchport Access vlan #
Do wri
End

#### MODO TRONCAL
Conf t
Int f#/#
Switchport mode trunk
Switchport trunk allowed vlan 1,#,#,1002-1005
Do wri
End

#### CONFIGURACION VTP
Conf t
Vtp domain nombredeldominio
Vtp password contraseñadeldominio
Vtp mode server|client|transparent
Do wri
End

#### PORT CHANNEL
Conf t
Interfaces range f#/#-#
Channel-group # mode on
Do wri
End

#### CONFIGURACION VLAN
Conf t
Vlan numerodevlan
Name nombredevlan
Do wri
End

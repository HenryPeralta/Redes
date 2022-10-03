Universidad San Carlos de Guatemala <br>
Facultad de Ingeniería <br>
Escuela de Ciencias y Sistemas <br>
Redes de computadoras 1 sección Q <br>
Ing. Allan Alberto Morataya Gómez <br>
Aux. Jorge David Ambrosio Ventura <br>
<br>
<br>
### <center>Manual Técnico practica 2 </center>
<br>
<br>
  

| Nombre | Carnet |
|--|--|
| Henry Gabriel Peralta Martinez | 201712289 |
  

# Manual de configuración
### Como realizar las rutas estáticas
![enter image description here](https://i.ibb.co/q98HvrS/Topologia.png)

Para realizar las rutas estáticas se conectaron las vpcs con los switches y se configuraron sus direcciones ip, luego se cambió la conexión del switch al router a modo troncal para que pueda recibir todas las vlans, luego se configuraron los routers con conexión serial y se configuro la conexión entre el switch y router y luego se configuro la conexión entre los routers.
### Comandos
### Para las vpcs

 - Ip 192.168.131.2 255.255.255.0 192.168.131.1
### Para los routers
 - conf terminal
 - interface fastEthernet 0/0
 - no shutdown
 - exit
 - interface fastEthernet 0/0.10
 - encapsulation dot1Q 10
 - ip address 192.168.131.1 255.255.255.0
 - exit
 - do wri
 - exit
 - conf terminal
 - interface s0/0
 - ip address 172.131.0.2 255.255.0.0
 - no shutdown
 - exit
 - exit
 - wr
 - configure terminal
 - ip route 192.168.132.0 255.255.255.0 172.131.0.3
 - end
 - ping 192.168.132.1
### Tablas de ruteo para cada router
X = Numero de grupo + Último número de carnet = 4 + 9 = 13
![enter image description here](https://i.ibb.co/c6PmD8b/tab1.png)

![enter image description here](https://i.ibb.co/wsShCXz/tab2.png)

### Capturas de paquetes
![enter image description here](https://i.ibb.co/RjkRt60/pc1apc3-4.png)
![enter image description here](https://i.ibb.co/kqYr9FD/pc1apc5-6.png)
![enter image description here](https://i.ibb.co/ctthHkD/pc2apc3-4.png)
![enter image description here](https://i.ibb.co/VYmQm0Y/pc2apc5-6.png)
![enter image description here](https://i.ibb.co/k2D9C9S/pc3apc1-2.png)
![enter image description here](https://i.ibb.co/Q6v6zTy/pc3apc5-6.png)
![enter image description here](https://i.ibb.co/NLVF1MC/pc4apc1-2.png)
![enter image description here](https://i.ibb.co/xLsC9qd/pc4apc5-6.png)
![enter image description here](https://i.ibb.co/z7gwkDc/pc5apc1-2.png)
![enter image description here](https://i.ibb.co/hYmG160/pc5apc3-4.png)
![enter image description here](https://i.ibb.co/SKqDSVH/pc6apc1-2.png)
![enter image description here](https://i.ibb.co/RPH8TNT/pc6apc2-3.png)

# **Manual** 
---
### Proyecto 2
### Universidad de San Carlos de Guatemala
### Facultad de Ingeniería 
### Laboratorio Redes de Computadoras 1 N
### Primer Semestre 2021
### Grupo 12


| Estudiante | Carné | 
| ------ | ------ |
| Marco Antonio Xocop Roquel | 201122934 |
| Maynor Octavio Piló Tuy | 201531166 |
| Cristian Estuardo Herrera Poncio | 201603198 |
| Edgar Humberto Borrayo Bartolón | 201503702 |

## Configuración de Topologia
Uno de los primeros pasos a realizar será el cargar la Imagen del swith a utilizar en el Emulador GNS3.
Para lo cual deberá realizarse los siguientes pasos

#### Paso 1
Primero debe descargarse la imagen de Ethernetswith o Switch de capa 3 que se encuentra en el siguiente enlace:
```
https://drive.google.com/file/d/10810USuKu7M6s-_u6cIxek-6czPIt7XH/view?usp=sharing
```

#### Paso 2
Luego abrimos el emulador GNS3 y en el menú "Editar" ubicado en la parte superior izquierda buscamos la opcion "Preferencias".

![elementos](/Proyecto1/img/conf_top_1.JPG)

#### Paso 3
Se abrira la ventana de Preferencias, acá buscaremos del lado izquierdo de la ventana el menú "Dynamips" u daremos click en el sub-menu "IOS routers".

Acá apareceran los Routes o Switchs capa 3 que se tengan configurados.
![elementos](/Proyecto1/img/conf_top_2.JPG)

#### Paso 4
Como siguiente paso buscaremos el botón "Nuevo" o "New" y daremos click cn el boton para agregar un nuevo Router.

![elementos](/Proyecto1/img/conf_top_3.JPG)

#### Paso 5
Se abrira una ventana, en la cual pedira que escoja la ruta de la Imagen que desea cargar. Para ello presionara el botón "Browse...".

Esto le abrira una ventana en la cual podrá buscar la imagen en su computadora y seleccionarla.
![elementos](/Proyecto1/img/conf_top_4.JPG)

Al seleccionar la imagen se cargara la ruta en la pantalla y tendrá que presionar el boton "Siguiente" o "Next".

![elementos](/Proyecto1/img/conf_top_5.JPG)

#### Paso 6
Luego se abrirar una pantalla en la cual le pedirá que ingrese en el campo "Name" o "Nombre" el nombre del Switch que esta cargando (esto queda a su discrecion).
Adicional la pantalla le solicita que seleccione la Plataforma del Router que desea cargar, para este proyecto se utilizo la Plataforma "c3600".
Posterio debé ingresar el chasis de la plataforma, el cual para este ejemplo se seleccionó "3640".

Como punto Importante, recuerde seleccionar la opción "This is an EtherSwitch router".
Por último presione "Siguiente" en la parte inferior derecha de la pantalla.

![elementos](/Proyecto1/img/conf_top_6.JPG)

#### Paso 7
Último paso, acá debera comprobar que el router se encuentra configurado en su simulador, en la parte izquierda deberá aparecerle el logo del nuevo dispositivo.

![elementos](/Proyecto1/img/conf_top_8.JPG)


## Topologia 1


### Red WAN (Interconexión de centro de datos y oficina central)

| Router | IP | Mask | VLAN | SALTO | Mask |
| ------ |------ |------ |------ | ------ | ------ |
| Router_2 | 10.12.0.5 | 255.255.192.0 | 10.12.64.5 | 192.168.124.0 | 255.255.255.0 |
| Router_3 | 10.12.0.6 | 255.255.192.0 | 10.12.64.6 | 192.168.125.0 | 255.255.255.0 |
| Router_4 | 10.12.0.7 | 255.255.192.0 | 10.12.128.6 | 192.168.124.0 | 255.255.255.0 |
| Router_5 | 10.12.0.5 | 255.255.192.0 | 10.12.128.5 | 192.168.125.0 | 255.255.255.0 |


### Comandos 
R2
Se configura la interface 0 la cual será la red interna de comunicacion.
```
configure terminal 

interface f0/0 
ip address 10.12.0.5 255.255.192.0
duplex full 
speed 100 
shutdown 
no shutdown
exit

```

Se configura la interface 1 la cual será la sub red y protocolo GLBP.
```
interface f0/1 
ip address 10.12.64.5 255.255.192.0
duplex full 
speed 100 
shutdown
no shutdown 
glbp 1 ip 10.12.64.7
glbp 1 priority 120 
glbp 1 preempt 
glbp 1 load-balancing host-dependent 
exit 
```

Se configuran los saltos para la comunicacion entre subredes.
```
ip route 192.168.124.0 255.255.255.0 10.12.64.7
ip route 192.168.125.0 255.255.255.0 10.12.0.5 
```

Se guardan las configuraciones
```
exit 
write memory 
```
![elementos](/Proyecto2/img/topo1_1.JPG)

R3
Se configura la interface 0 la cual será la red interna de comunicacion.
```
configure terminal 

interface f0/0 
ip address 10.12.0.6 255.255.192.0
duplex full 
speed 100 
shutdown 
no shutdown
exit
```

Se configura la interface 1 la cual será la sub red y protocolo GLBP.
```
interface f0/1 
ip address 10.12.64.6 255.255.192.0
duplex full 
speed 100 
shutdown
no shutdown 
glbp 1 ip 10.12.64.7
glbp 1 priority 100 
glbp 1 preempt 
glbp 1 load-balancing host-dependent 
exit 
```

Se configuran los saltos para la comunicacion entre subredes.
```
ip route 192.168.124.0 255.255.255.0 10.12.64.7
ip route 192.168.125.0 255.255.255.0 10.12.0.6 
```

Se guardan las configuraciones
```
exit 
write memory 
```
![elementos](/Proyecto2/img/topo1_2.JPG)


R4
Se configura la interface 0 la cual será la red interna de comunicacion.
```
configure terminal 

interface f0/0 
ip address 10.12.0.7 255.255.192.0
duplex full 
speed 100 
shutdown 
no shutdown
exit
```

Se configura la interface 1 la cual será la sub red y protocolo GLBP.
```
interface f0/1 
ip address 10.12.128.6 255.255.192.0
duplex full 
speed 100 
shutdown
no shutdown 
standby 1 ip 10.12.128.7
standby 1 priority 100 
standby 1 preempt 
exit 
```

Se configuran los saltos para la comunicacion entre subredes.
```
ip route 192.168.124.0 255.255.255.0 10.12.0.7
ip route 192.168.125.0 255.255.255.0 10.12.128.7 
```

Se guardan las configuraciones
```
exit 
write memory 
```
![elementos](/Proyecto2/img/topo1_3.JPG)


R5
Se configura la interface 0 la cual será la red interna de comunicacion.
```
configure terminal 

interface f0/0 
ip address 10.12.0.5 255.255.192.0
duplex full 
speed 100 
shutdown 
no shutdown
exit
```

Se configura la interface 1 la cual será la sub red y protocolo GLBP.
```
interface f0/1 
ip address 10.12.128.5 255.255.192.0
duplex full 
speed 100 
shutdown
no shutdown 
standby 1 ip 10.12.128.7
standby 1 priority 120 
standby 1 preempt 
exit 
```

Se configuran los saltos para la comunicacion entre subredes.
```
ip route 192.168.124.0 255.255.255.0 10.12.0.5
ip route 192.168.125.0 255.255.255.0 10.12.128.7 
```

Se guardan las configuraciones
```
exit 
write memory 
```
![elementos](/Proyecto2/img/topo1_4.JPG)

### Diseño de Topologia 1
---
![elementos](/Proyecto2/img/topo1_final.JPG)

## Topologia 2
---
### Diseño de la Topologia 2  
---
![elementos](/Proyecto2/img/t2_t.png)
---
### Diseño de la Topologia 3
---
![elementos](/Proyecto2/img/p8.png)

### Tabla del resultado del subnetting
####  Ip base 
```
192.168.124.0/24
```

| VLAN | Salto | Network |  Mask           | P.Asignable     | U.Asignable     |Broadcast        | Host totales |Cantidad de hosts |
| ---- | ----- | ------- | --------------- | --------------- | --------------- | --------------- | ------------ | ---------------- |
| 10   |  224  | D       | 255.255.255.224 | 192.168.124.193 | 192.168.124.222 | 192.168.124.223 |  32          | 30               |
| 20   |  240  | D       | 255.255.255.240 | 192.168.124.225 | 192.168.124.238 | 192.168.124.239 |  16          | 14               |
| 30   |  128  | D       | 255.255.255.128 | 192.168.124.1   | 192.168.124.126 | 192.168.124.127 |  128         | 126              |
| 40   |  192  | D       | 255.255.255.192 | 192.168.124.129 | 192.168.124.190 | 192.168.124.191 |  64          | 62               |

### Configuracion de VPC´S
---

| NO  | Nombre      | VLAN | Dirección de red| Mascara         | Gateway         |
| --- | ----------- | ---- | --------------- | --------------- | --------------- |
| 1   | RRHH        | 10   | 192.168.124.193 | 255.255.255.224 | 192.168.124.222 |
| 2   | CONTA       | 20   | 192.168.124.225 | 255.255.255.240 | 192.168.124.238 |
| 3   | VENTAS      | 30   | 192.168.124.1   | 255.255.255.128 | 192.168.124.126 |
| 4   | INFORMATICA | 40   | 192.168.124.129 | 255.255.255.192 | 192.168.124.190 |

####  VPC ventas
```
ip 192.168.124.1 255.255.255.128 192.168.124.126
save
```
####  VPC Contabilidad 
```
ip 192.168.124.225 255.255.255.240 192.168.124.238
save
```
####  VPC Recursos Humanos
```
ip 192.168.124.193 255.255.255.224 192.168.124.222
save
```
####  VPC Informatica
```
ip 192.168.124.129 255.255.255.192 192.168.124.190
save
```
### Configuracion de Switchs
---
#### Configuracion Switch 1
---
![elementos](/Proyecto2/img/t2_sw1.png)
#### Configuracion Switch 2
---
![elementos](/Proyecto2/img/t2_sw2.png)

### Configuracion de ESW1T2
---
#### Creación de VLAN´s
```
conf t
VLAN 10
name RHUMANOS
VLAN 20
name CONTABILIDAD
VLAN 30
name VENTAS
VLAN 40
name INFORMATICA
exit
exit

write
```
#### Configuracion Modo Trunk
```
conf t
int f1/0
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

int f1/1
switchport mode trunk
switchport trunk allowed vlan 1,20,30,1002-1005
exit

int f1/2
switchport mode trunk
switchport trunk allowed vlan 1,10,40,1002-1005
exit
exit

write
```
### Configuracion de Router 1
---
#### Configuración de interfaces
```
conf t 
int f0/0.10 
encapsulation dot1Q 10
ip address 192.168.124.222 255.255.255.224
no shutdown 
exit

int f0/0.20 
encapsulation dot1Q 20
ip address 192.168.124.238 255.255.255.240	
no shutdown 
exit

int f0/0.30 
encapsulation dot1Q 30
ip address 192.168.124.126 255.255.255.128	
no shutdown 
exit

int f0/0.40 
encapsulation dot1Q 40
ip address 192.168.124.190 255.255.255.192	
no shutdown 
exit

int f2/0
ip addres
end 
```
#### Configuración de ruteo estatico
```
conf t 
route ip destino mascara ip_de_comunicaicon
route ip destino mascara ip_de_comunicaicon
route ip destino mascara ip_de_comunicaicon
route ip destino mascara ip_de_comunicaicon
route ip destino mascara ip_de_comunicaicon
route ip destino mascara ip_de_comunicaicon
end
```

## Topologia 3

### Dirección de red
192.168.125.0/24

### Mascara de red
255	255	255	0

### Cantidad de subredes
4

### subredes
| Nombre |  VLAN |
| --- | --- |
| RHUMANOS  |  10 |
| CONTABILIDAD  | 20 |
| VENTAS  |  30 |
| INFORMATICA  | 40  |


### Subnetting

### IP Base
```
192.168.125.0
```

| Nombre |  VLAN | Salto  | Network  | Mask  |  P.Asignable | U.Asignable |  Broadcast | Host totales | Cantidad de hosts |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| RHUMANOS  |  10 | 64  | 192.168.125.0/26  | 255.255.255.192  | 192.168.125.192   | 192.168.125.62  |  	192.168.125.63 | 62 |  1 |
| CONTABILIDAD  | 20 | 64  | 192.168.125.64/26  | 255.255.255.192  | 192.168.125.65   | 192.168.125.62  | 192.168.125.127  | 62 |  1 |
| VENTAS  |  30 |  64 | 192.168.125.128/26  | 255.255.255.192  | 192.168.125.65   | 192.168.125.190 |  192.168.125.191 | 62 |  1 |
| INFORMATICA  | 40  | 64  | 192.168.125.192/26  | 255.255.255.192  | 192.168.125.193  | 192.168.125.190  | 192.168.125.191 | 62 |  1 |


### Configurando VPC's
| No. | Nombre | VLAN | Dirección de red | Mascara | Gateway |
| --- | --- | --- | --- | --- | --- |
| 1 | RRHH_S | 10  | 192.168.125.10 | 255.255.255.192 | 192.168.125.62 |
| 2 | CONTA_S | 20  | 192.168.125.75 | 255.255.255.192 | 192.168.125.126 |
| 3 | VENTAS_S | 30 | 192.168.125.139 | 255.255.255.192 | 192.168.125.190 |
| 4 | INFORMATICA_S | 40 | 192.168.125.198 | 255.255.255.192 | 192.168.125.254 |
 
### Comandos
### RHUMANOS
```
ip 192.168.125.10 255.255.255.192 192.168.125.62
sh ip
save
```
![elementos](/Proyecto2/img/p1.png)
### CONTABILIDAD

```
ip 192.168.125.75 255.255.255.192 192.168.125.126
sh ip
save
```
![elementos](/Proyecto2/img/p2.png)


### VENTAS

```
ip 192.168.125.139 255.255.255.192 192.168.125.190
sh ip
save
```
![elementos](/Proyecto2/img/p3.png)

### INFORMATICA

```
ip 192.168.125.198 255.255.255.192 192.168.125.254
sh ip
save
```
![elementos](/Proyecto2/img/p4.png)

### Configuracion de ESW2
Creación de VLAN´s
``` 
conf t
vlan 10
name RHUMANOS
vlan 20
name CONTABILIDAD
vlan 30
name VENTAS
vlan 40
name INFORMATICA
exit
exit
```
![elementos](/Proyecto2/img/p5.png)

Configuracion Modo Trunk
```
conf t
int f1/3
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005

int f1/4
switchport mode access
switchport access vlan 10

int f1/0
switchport mode access
switchport access vlan 20

int f1/1
switchport mode access
switchport access vlan 30

int f1/2
switchport mode access
switchport access vlan 40


exit
exit
write
```
![elementos](/Proyecto2/img/p6.png)

### Configuración Router 6
Configuración de interfaces
```
conf t
int f0/0.10
encapsulation dot1Q 10
ip address 192.168.125.62 255.255.255.192
no shutdown
exit
int f0/0.20
encapsulation dot1Q 20
ip address 192.168.125.126 255.255.255.192
no shutdown
exit
int f0/0.30
encapsulation dot1Q 30
ip address 192.168.125.190 255.255.255.192
no shutdown
exit
int f0/0.40
encapsulation dot1Q 40
ip address 192.168.125.254 255.255.255.192
no shutdown
exit

int f0/1
ip address 10.2.0.18 255.255.255.252
no shutdown
exit

int f3/0
ip address 10.2.0.22 255.255.255.252
no shutdown
exit

```
![elementos](/Proyecto2/img/p7.png)

### encender interfaces
```
conf t
int f0/0
no shutdown
exit
exit
sh ip int br
```

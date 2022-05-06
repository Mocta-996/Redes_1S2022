# **Manual** 
---
### Proyecto 1 
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
![elementos](/img/topo1_1.png)

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
![elementos](/Proyecto2/img/topo1_2.png)


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
![elementos](/Proyecto2/img/topo1_3.png)


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
![elementos](/Proyecto2/img/topo1_4.png)

### Diseño de Topologia 1
---
![elementos](/Proyecto2/img/topo1_final.png)

## Topologia 2
---

## Topologia 3
---


## Ping a maquinas

### Ping de topologia 1 a otras maquinas en topologia 2 y 3
```
ping 192.168.123.20
```
![elementos](/Proyecto1/img/Conta2.PNG)
```
ping 192.168.122.20
```
![elementos](/Proyecto1/img/Informatica1.PNG)
```
ping 192.168.121.20
```
![elementos](/Proyecto1/img/RRHH1.PNG)
```
ping 192.168.121.30
```
![elementos](/Proyecto1/img/RRHH2.PNG)
```
ping 192.168.124.20
```
![elementos](/Proyecto1/img/Ventas1.PNG)
```
ping 192.168.124.20
```
![elementos](/Proyecto1/img/Ventas_1.PNG)

## Red Física 
--- 
### Conexión físia entre cuatro máquinas
Computadoras conectadas a una  VPN formando una pequeña red donde
estas tienen conexión y acceso a propiedades de red tradicionales como archivos compartidos por
defecto.

```
Máquina 1  \\10.8.0.3\Compartir
```
![elementos](/Proyecto1/img/red_fisica1.png)

```
Máquina 2 \\10.8.0.4\Ejemplo4
```
![elementos](/Proyecto1/img/red_fisica3.png)

```
Máquina 3 \\10.8.0.5\redes1_carpeta_compartida
```
![elementos](/Proyecto1/img/red_fisica4.png)

```
Máquina 4 \\10.8.0.2\redes1_carpeta_compartida
```
![elementos](/Proyecto1/img/red_fisica2.png)

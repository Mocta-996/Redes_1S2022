# **Manual** 
---
### Tarea 3 
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


### Detalles de VLAN

| VLAN | #VLAN | Dirección de red | Gateway |
| -------| -------| -------|  -------|
| RRHH | 10 | 192.168.121.0/24 | 192.168.121.1 |
| Informatica | 20 | 192.168.122.0/24 | 192.168.122.1 |
| Contabilidad | 30 | 192.168.123.0/24 | 192.168.123.1 |
| Ventas | 40 | 192.168.124.0/24 | 192.168.124.1 |

## Topologia 1


### Distribución de direcciones IP correspondientes a cada departamento de la empresa

| VPCS | IP | Mascara de subred | Gateway | Comando |
| ------ |------ |------ |------ | ------ |
| RRHH_1 | 192.168.121.10 | 255.255.255.0 | 192.168.121.1 | ip 192.168.121.10 255.255.255.0 192.168.121.1 |
| Conta_1 | 192.168.123.10 | 255.255.255.0 | 192.168.123.1 | ip 192.168.123.10 255.255.255.0 192.168.123.1 |
| RRHH_2 | 192.168.121.20 | 255.255.255.0 | 192.168.121.1 | ip 192.168.121.20 255.255.255.0 192.168.121.1 |
| Conta_2 | 192.168.123.20 | 255.255.255.0 | 192.168.123.1 | ip 192.168.123.20 255.255.255.0 192.168.123.1 |
| Ventas_1 | 192.168.124.10 | 255.255.255.0 | 192.168.124.1 | ip 192.168.124.10 255.255.255.0 192.168.124.1 |
| Informatica_1 | 192.168.122.10 | 255.255.255.0 | 192.168.112.1 | ip 192.168.122.10 255.255.255.0 192.168.112.1 |


### Comandos 
RHHH_1
```
ip 192.168.121.10 255.255.255.0 192.168.121.1
sh ip
save
```
![elementos](/Proyecto1/img/2.png)

Conta_1
```
ip 192.168.123.10 255.255.255.0 192.168.123.1
sh ip
save
```
![elementos](/Proyecto1/img/3.png)


RRHH_2
```
ip 192.168.121.20 255.255.255.0 192.168.121.1
sh ip
save
```
![elementos](/Proyecto1/img/4.png)


Conta_2
```
ip 192.168.123.20 255.255.255.0 192.168.123.1
sh ip
save
```
![elementos](/Proyecto1/img/5.png)


Ventas_1
```
ip 192.168.124.10 255.255.255.0 192.168.124.1
sh ip
save
```
![elementos](/Proyecto1/img/6.png)


Informatica_1
```
ip 192.168.122.10 255.255.255.0 192.168.122.1
sh ip
save
```
![elementos](/Proyecto1/img/1.png)


### ESW1
```
conf t
vtp domain GRUPO12
vtp password grupo12
vtp mode client
exit
sh vtp st
```
![elementos](/Proyecto1/img/24.png)


Configurando modo truncal
```
conf t
int f1/1
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

int f1/3
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

int f1/4
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

exit
write
sh int tr
```
![elementos](/Proyecto1/img/25.png)


### ESW2
```
conf t
vtp domain GRUPO12
vtp password grupo12
vtp mode client
exit
sh vtp st
```
![elementos](/Proyecto1/img/18.png)


Configurando modo truncal
```
conf t
int f1/3
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit
int f1/5
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit
exit
write
sh int tr
```
![elementos](/Proyecto1/img/19.png)

Configurando modo acceso
```
conf t
int f1/4
switchport mode access
switchport access vlan 10
exit
int f1/0
switchport mode access
switchport access vlan 30
exit
int f1/1
switchport mode access
switchport access vlan 10
exit
exit
sh vlan-sw
```
![elementos](/Proyecto1/img/20.png)

### ESW3

```
conf t
vtp domain GRUPO12
vtp password grupo12
vtp mode client
exit
sh vtp st
```
![elementos](/Proyecto1/img/21.png)

Configurando modo truncal
```
conf t
int f1/4
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit
int f1/5
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit
exit
write
sh int tr
```
![elementos](/Proyecto1/img/22.png)

Configurando modo acceso
```
conf t
int f1/0
switchport mode access
switchport access vlan 30
exit

int f1/2
switchport mode access
switchport access vlan 40
exit

int f1/1
switchport mode access
switchport access vlan 20
exit
exit
sh vlan-sw
```
![elementos](/Proyecto1/img/23.png)

## Topologia 2
--
![elementos](/Proyecto1/img/top2.png)
--

| VPCS | IP | Mascara de subred | Gateway | Comando |
| ------ |------ |------ |------ | ------ |
| Informatica_2 | 192.168.122.20 | 255.255.255.0 | 192.168.112.1 | ip 192.168.122.20 255.255.255.0 192.168.112.2 |

## Comandos
### Informatica_1
```
ip 192.168.122.20 255.255.255.0 192.168.122.1
sh ip
save
```
### Server ESW4
#### Configurando vlans 10,20,30,40
```
conf t
vlan 10
name RRHH
exit
vlan 20
name Informatica
exit
vlan 30
name Contabilidad
exit
vlan 40
name Ventas
exit
do sh vlan-sw
exit
```
![elementos](/Proyecto1/img/8.png)

### Configuración de VTP (ESW4)
Configurando ESW4 en modo servidor VTP

```
conf t
vtp domain GRUPO12
vtp password grupo12
vtp mode server
vtp version 2
exit
sh vtp st
```
![elementos](/Proyecto1/img/9.png)

### Configuración en modo truncal (ESW4)
```
conf t
int f1/0
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit
int f1/1
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit
int f1/2
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit
do sh int tr
exit
write
```
![elementos](/Proyecto1/img/10.png)

### Configuración en modo cliente (ESW5, ESW6, ESW7)
ESW5
```
conf t
vtp domain GRUPO12
vtp password grupo12
vtp mode client
exit
sh vtp st
```
![elementos](/Proyecto1/img/11.png)


Configuración modo troncal
```
conf t
int f1/0
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit
int f1/1
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit
exit
write
sh int tr
```
![elementos](/Proyecto1/img/12.png)

ESW6
```
conf t
vtp domain GRUPO12
vtp password grupo12
vtp mode client
exit
sh vtp st
```
![elementos](/Proyecto1/img/13.png)


Configuración modo troncal
```
conf t
int f1/0
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit
int f1/1
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit
int f1/2
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit
int f1/3
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit
exit
write
sh int tr
```
![elementos](/Proyecto1/img/14.png)

ESW7
```
conf t
vtp domain GRUPO12
vtp password grupo12
vtp mode client
exit
sh vtp st
```
![elementos](/Proyecto1/img/15.png)

Configuración modo troncal
```
conf t
int f1/0
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit
int f1/1
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit
int f1/3
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit
exit
write
sh int tr
```
![elementos](/Proyecto1/img/16.png)

Configuración modo acceso
```
conf t
int f1/2
switchport mode access
switchport access vlan 20
exit
exit
sh vlan-sw
```
![elementos](/Proyecto1/img/17.png)

## Topologia 3


| VPCS | IP | Mascara de subred | Gateway | Comando |
| ------ |------ |------ |------ | ------ |
| Server_Conta | 192.168.123.30 | 255.255.255.0 | 192.168.123.1 | ip 192.168.123.30 255.255.255.0 192.168.123.1 |
| Server_Informatica | 192.168.122.30 | 255.255.255.0 | 192.168.122.1 | ip 192.168.122.30 255.255.255.0 192.168.122.1 |
| Server_RRHH | 192.168.121.30 | 255.255.255.0 | 192.168.121.1 | ip 192.168.121.30 255.255.255.0 192.168.121.1 |
| Server_Ventas | 192.168.124.20 | 255.255.255.0 | 192.168.124.1 | ip 192.168.124.20 255.255.255.0 192.168.124.1 |

## Comandos
Server_Conta
```
ip 192.168.123.30 255.255.255.0 192.168.123.1 
sh ip
save
```

Server_informatica
```
ip 192.168.122.30 255.255.255.0 192.168.122.1
sh ip
save
```


Server_RRHH
```
ip 192.168.121.30 255.255.255.0 192.168.121.1
sh ip
save
```

Server_Ventas
```
ip 192.168.124.20 255.255.255.0 192.168.124.1
sh ip
save
```
## Configuración cliente
### ESW8
```
conf t
vtp domain GRUPO12
vtp password grupo12
vtp mode client
exit
sh vtp st
```
![elementos](/Proyecto1/img/26.png)


Configuración modo troncal
```
conf t
int f1/1
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

int f1/2
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

exit
write
sh int tr
```
![elementos](/Proyecto1/img/27.png)


Configuración modo acceso
```
conf t
int f1/0
switchport mode access
switchport access vlan 40
exit
exit
sh vlan-sw
```
![elementos](/Proyecto1/img/28.png)

### ESW9
```
conf t
vtp domain GRUPO12
vtp password grupo12
vtp mode client
exit
sh vtp st
```
![elementos](/Proyecto1/img/29.png)


Configuración modo troncal
```
conf t
int f1/0
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

int f1/1
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

int f1/2
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

exit
write
sh int tr
```
![elementos](/Proyecto1/img/30.png)

Configuración modo acceso
```
conf t
int f1/3
switchport mode access
switchport access vlan 30
exit
exit
sh vlan-sw
```
![elementos](/Proyecto1/img/31.png)

### ESW10
```
conf t
vtp domain GRUPO12
vtp password grupo12
vtp mode client
exit
sh vtp st
```
![elementos](/Proyecto1/img/32.png)


Configuración modo troncal
```
conf t
int f1/0
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

int f1/2
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

exit
write
sh int tr
```
![elementos](/Proyecto1/img/33.png)

Configuración modo acceso
```
conf t
int f1/1
switchport mode access
switchport access vlan 10
exit
exit
sh vlan-sw
```
![elementos](/Proyecto1/img/34.png)

### ESW11
```
conf t
vtp domain GRUPO12
vtp password grupo12
vtp mode transparent
exit
sh vtp st
```
![elementos](/Proyecto1/img/35.png)


Configuración modo troncal
```
conf t
int f1/1
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

int f1/2
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

exit
write
sh int tr
```
![elementos](/Proyecto1/img/36.png)

Configuración modo acceso
```
conf t
int f1/0
switchport mode access
switchport access vlan 20
exit
exit
sh vlan-sw
```
![elementos](/Proyecto1/img/37.png)

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


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
Conta_1
```
ip 192.168.123.10 255.255.255.0 192.168.123.1
sh ip
save
```
RRHH_2
```
ip 192.168.121.20 255.255.255.0 192.168.121.1
sh ip
save
```
Conta_2
```
ip 192.168.123.20 255.255.255.0 192.168.123.1
sh ip
save
```
Ventas_1
```
ip 192.168.124.10 255.255.255.0 192.168.124.1
sh ip
save
```
Informatica_1
```
ip 192.168.122.10 255.255.255.0 192.168.122.1
sh ip
save
```

### ESW1
```
conf t
vtp domain GRUPO12
vtp password grupo12
vtp mode client
exit
sh vtp st
```
<24.png>

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
<25.png>
### ESW2
```
conf t
vtp domain GRUPO12
vtp password grupo12
vtp mode client
exit
sh vtp st
```
<18.png>

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
<19.png>

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
<20.png>

### ESW3

```
conf t
vtp domain GRUPO12
vtp password grupo12
vtp mode client
exit
sh vtp st
```
<21.png>

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
<22.png>

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
<23.png>

## Topologia 2


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
<8.png>

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
<9.png>

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
<10.png>

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
<11.png>


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
<12.png>

ESW6
```
conf t
vtp domain GRUPO12
vtp password grupo12
vtp mode client
exit
sh vtp st
```
<13.png>


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
<14.png>

ESW7
```
conf t
vtp domain GRUPO12
vtp password grupo12
vtp mode client
exit
sh vtp st
```
<15.png>

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
<16.png>

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
<17.png>

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
<26.png>


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
<27.png>


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
<28.png>

### ESW9
```
conf t
vtp domain GRUPO12
vtp password grupo12
vtp mode client
exit
sh vtp st
```
<29.png>


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
<30.png>

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
<31.png>

### ESW10
```
conf t
vtp domain GRUPO12
vtp password grupo12
vtp mode client
exit
sh vtp st
```
<32.png>


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
<33.png>

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
<34.png>

### ESW11
```
conf t
vtp domain GRUPO12
vtp password grupo12
vtp mode transparent
exit
sh vtp st
```
<35.png>


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
<36.png>

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
<37.png>
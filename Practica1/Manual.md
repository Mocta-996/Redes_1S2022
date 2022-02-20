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

---
## Configuración inicial
---
Se creará un Proyecto en GNS3, se agregara los siguientes elementos

- 2 cloud
- 1 Switch
- 1 VPcs

![elementos](/Practica1/img/m1.png)


---
## Configuración de las VPCs (Marco)
---
Se insertara una VPC y luego se le dara clic derecho en "start", despues abrir su consola con clic derecho y elegir "console" tal como se ve en la imagen

![Consola](/Practica1/img/m2.png)

En este caso usaremos la siguiente configuración para el equipo

la mascara de subred:
```
255.255.255.0
```
y el gaterway
```
192.168.112.1 
```
la dirección de IP
```
192.168.112.10
```
Comando completo
```
ip 192.168.112.10 255.255.255.0 192.168.112.1
```
   
Asi se vera en la consola ya ejecutada 

![Consola](/Practica1/img/m3.png)



---
## Configuración de las nubes
---
Para configurar la nube "Cloud" seleccionaremos con clic derecho configure

![Consola](/Practica1/img/m4.png)

Iremos a la pestaña "UDP tunnels"
Ahi colocaremos la siguiente configuración para la nube "Cristian"
```
Local port: 30100
Remote host: 10.8.0.3
Remote port: 20100
```

Iremos a la pestaña "UDP tunnels"
Ahi colocaremos la siguiente configuración para la nube "Maynor"
```
Local port: 30100
Remote host: 10.8.0.4
Remote port: 20100
```

- Donde local port será un puerto que elegimos
- Remote host es la dirección Ip de la otra VPC que queremos alcanzar
- Remote port será al puerto que nos conectaremos

Debemos dar clic en "Add" para guardar la configuración y luego dar clic en "OK" para realizar la configuración para la nube "Cristian"

![Consola](/Practica1/img/m5.png)

Debemos dar clic en "Add" para guardar la configuración y luego dar clic en "OK" para realizar la configuración para la nube "Maynor"

![Consola](/Practica1/img/m5.png)


Depues se realizaran las conexiones entre los distintos componentes, es muy importante que al conectar el switch se conecte al puerto UDP tunnel1 o el nombre que se le haya asignado al configurarse la nube.

![Conección](/Practica1/img/m6.png)

---
## Pings entre los hosts
---
Se realizara la conexion con la maquina de la nube de "Cristian"
```
ping 192.168.112.20
```
En la imagen se puede notar que si existe una conexión constante y estable.

![Conección](/Practica1/img/m7.png)


Se realizara la conexion con la maquina de la nube de "Maynor"
```
ping 192.168.112.30
```
En la imagen se puede notar que si existe una conexión constante y estable.

![Conección](/Practica1/img/m7.png)

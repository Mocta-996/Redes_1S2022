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
- VPN con Google Cloud (con los firewall configurados)

![elementos](/Practica1/img/m1.PNG)


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
## Configuración de las nubes (Marco)
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
Local port: 30500
Remote host: 10.8.0.4
Remote port: 20500
```

- Donde local port será un puerto que elegimos
- Remote host es la dirección Ip de la otra VPC que queremos alcanzar
- Remote port será al puerto que nos conectaremos

Debemos dar clic en "Add" para guardar la configuración y luego dar clic en "OK" para realizar la configuración para la nube "Cristian"

![Consola](/Practica1/img/m5.PNG)

Debemos dar clic en "Add" para guardar la configuración y luego dar clic en "OK" para realizar la configuración para la nube "Maynor"

![Consola](/Practica1/img/m9.PNG)


Depues se realizaran las conexiones entre los distintos componentes, es muy importante que al conectar el switch se conecte al puerto UDP tunnel1 o el nombre que se le haya asignado al configurarse la nube.

![Conección](/Practica1/img/m6.PNG)

---
## Pings entre los hosts (Marco)
---
Se realizara la conexion con la maquina de la nube de "Cristian"
```
ping 192.168.112.20
```
En la imagen se puede notar que si existe una conexión constante y estable.

![Conección](/Practica1/img/m7.PNG)


Se realizara la conexion con la maquina de la nube de "Maynor"
```
ping 192.168.112.30
```
En la imagen se puede notar que si existe una conexión constante.

![Conección](/Practica1/img/m8.PNG)


---
## Configuración de las VPCs (Maynor Octavio Piló Tuy)
---
Se inserta una VPC, se inicia y luego se realiza la siguiente configuración. 

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
192.168.112.30
```
Comando completo
```
ip 192.168.112.30 255.255.255.0 192.168.112.1
```
Ejecución de los datos ingresados.   

![Consola](https://github.com/Mocta-996/Redes_1S2022/blob/e3405bd4dc86782737338862fab7ce31c3668887/Practica1/img/mimg1.png)

---
## Configuración de las nubes (Maynor )
---
Se realizaron las siguientes configuraciones para las nubes, dicha configuracion se realizaron en la pestaña 
a "UDP tunnels", y se guardan los cambios. 
Configuración para la nube  "Cristian" 
```
Local port: 20600
Remote host: 10.8.0.3
Remote port: 30600
```
Configuración para la nube "Marco"
```
Local port: 20500
Remote host: 10.8.0.2
Remote port: 30500
```

- Donde local port será un puerto que elegimos
- Remote host es la dirección Ip de la otra VPC que queremos alcanzar
- Remote port será al puerto que nos conectaremos

Configuración para la nube  "Cristian" 

![Consola](https://github.com/Mocta-996/Redes_1S2022/blob/e3405bd4dc86782737338862fab7ce31c3668887/Practica1/img/mimg2.png)

Configuración para la nube "Marco"

![Consola](https://github.com/Mocta-996/Redes_1S2022/blob/e3405bd4dc86782737338862fab7ce31c3668887/Practica1/img/mimg3.png)


Depues se realizaran las conexiones entre los distintos componentes.

![Conección](https://github.com/Mocta-996/Redes_1S2022/blob/e3405bd4dc86782737338862fab7ce31c3668887/Practica1/img/mimg4.png)

---
## Pings entre los hosts (Maynor)
---
Conexion con la maquina de la nube de "Cristian"
```
ping 192.168.112.20
```
![Conección](https://github.com/Mocta-996/Redes_1S2022/blob/e3405bd4dc86782737338862fab7ce31c3668887/Practica1/img/ping1.png)

Se realizara la conexion con la maquina de la nube de "Marco"
```
ping 192.168.112.10
```

![Conección](https://github.com/Mocta-996/Redes_1S2022/blob/e3405bd4dc86782737338862fab7ce31c3668887/Practica1/img/ping2.png)


---
## Configuración de las VPCs (Cristian)
---
Se inserta una VPC, se inicia y luego se realiza la siguiente configuración. 

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
192.168.112.20
```
Comando completo
```
ip 192.168.112.20 255.255.255.0 192.168.112.1
```
Ejecución de los datos ingresados.   

![Consola](/Practica1/img/ch1.png)

---
## Configuración de las nubes (Cristian )
---
Se realizaron las siguientes configuraciones para las nubes, dicha configuracion se realizaron en la pestaña 
a "UDP tunnels", y se guardan los cambios. 
Configuración para la nube  "Maynor" 
```
Local port: 30600
Remote host: 10.8.0.4
Remote port: 20600
```
Configuración para la nube "Marco"
```
Local port: 20100
Remote host: 10.8.0.2
Remote port: 30100
```

- Donde local port será un puerto que elegimos
- Remote host es la dirección Ip de la otra VPC que queremos alcanzar
- Remote port será al puerto que nos conectaremos

Configuración para la nube  "Maynor" 

![Consola](https://github.com/Mocta-996/Redes_1S2022/blob/cef2701ab9185921cbd876527eb089007d2b20ea/Practica1/img/ch2.png)

Configuración para la nube "Marco"

![Consola](/Practica1/img/ch3.png)


Depues se realizaran las conexiones entre los distintos componentes.

![Conección](/Practica1/img/ch4.png)

---
## Pings entre los hosts (Cristian)
---
Conexion con la maquina de la nube de "Maynor"
```
ping 192.168.112.30
```
![Conección](/Practica1/img/ch5.png)

Se realizara la conexion con la maquina de la nube de "Marco"
```
ping 192.168.112.10
```

![Conección](/Practica1/img/ch6.png)


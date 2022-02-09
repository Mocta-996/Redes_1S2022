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
## Creación y configuración de la instancia en Google cloud
---
#### Paso 1.
Se crea un nuevo proyecto, con el nombre de Redes1Tarea3G12:
![creacion](https://github.com/Mocta-996/Redes_1S2022/blob/20fb555279237ef81500727ff105fa47ff1554bf/Tarea3/img/sc1.png)
#### Paso 2.
Se habilita una nueva maquina virtual Compute Engine API:
![creacion](https://github.com/Mocta-996/Redes_1S2022/blob/20fb555279237ef81500727ff105fa47ff1554bf/Tarea3/img/sc2.png)
#### Paso 3.
Se Crea una nueva instancia y se configura de la siguiente manera:
![creacion](https://github.com/Mocta-996/Redes_1S2022/blob/20fb555279237ef81500727ff105fa47ff1554bf/Tarea3/img/sc5.png)
Se selecciona el sistema operativo, en este caso es Ubuntu 18.04 LTS
![creacion](https://github.com/Mocta-996/Redes_1S2022/blob/20fb555279237ef81500727ff105fa47ff1554bf/Tarea3/img/sc5.png)
Se conceden los permisos  al tráfico HTTP/HTTPS
![creacion](https://github.com/Mocta-996/Redes_1S2022/blob/20fb555279237ef81500727ff105fa47ff1554bf/Tarea3/img/sc7.png)
y con esto se crea una instancia con las siguientes características:
![creacion](https://github.com/Mocta-996/Redes_1S2022/blob/20fb555279237ef81500727ff105fa47ff1554bf/Tarea3/img/sc9.png)
#### Paso 4.
Se agregan reglas de firewall con las siguientes configuraciones:
Regla con dirección del tráfico de entrada y uno con dirección del tráfico de salida:
![creacion](https://github.com/Mocta-996/Redes_1S2022/blob/20fb555279237ef81500727ff105fa47ff1554bf/Tarea3/img/sc14.png)

---
## Integrantes del grupo IAM
---
Para agregar a propietaros del proyecto, se realizaron los siguientes pasos:
#### Paso 1.
Se selecciona la opción de IAM y administración y luego se selecciona la opcion de agregar, donde se ingresa el correo de los participantes.
![integrantes](https://github.com/Mocta-996/Redes_1S2022/blob/20fb555279237ef81500727ff105fa47ff1554bf/Tarea3/img/sc15.png)
![creacion](https://github.com/Mocta-996/Redes_1S2022/blob/20fb555279237ef81500727ff105fa47ff1554bf/Tarea3/img/sc16.png)
Integrantes del grupo 12
![creacion](https://github.com/Mocta-996/Redes_1S2022/blob/20fb555279237ef81500727ff105fa47ff1554bf/Tarea3/img/sc30.png)

---
## Configuración de la red privada
---
Se ejecuta la opcion SSH de la instancia  y se ejecutan los siguientes comandos:
#### Paso 1.
Comandos a ejecutar:
- sudo apt-get update
- sudo apt-get upgrade
![red](https://github.com/Mocta-996/Redes_1S2022/blob/20fb555279237ef81500727ff105fa47ff1554bf/Tarea3/img/sc18.png)
- sudo wget https://cubaelectronica.com/OpenVPN/openvpn-install.sh
- sudo bash openvpn-install.sh
![red](https://github.com/Mocta-996/Redes_1S2022/blob/20fb555279237ef81500727ff105fa47ff1554bf/Tarea3/img/sc19.png)
#### Paso 2.
Se deja la Ip address por default: 
![red](https://github.com/Mocta-996/Redes_1S2022/blob/20fb555279237ef81500727ff105fa47ff1554bf/Tarea3/img/sc20.png)
Así tambien la ip publica:
![red](https://github.com/Mocta-996/Redes_1S2022/blob/20fb555279237ef81500727ff105fa47ff1554bf/Tarea3/img/sc21.png) 
Se selecciona  la opción 1 (UDP), el puerto 1194  de escucha del programa OpenVPN  y el DNS a utilizar es el de Google (3).
![red](https://github.com/Mocta-996/Redes_1S2022/blob/20fb555279237ef81500727ff105fa47ff1554bf/Tarea3/img/sc22.png) 
Finalmente se genera el archivo .ovpn, agrengando un nombre.
![red](https://github.com/Mocta-996/Redes_1S2022/blob/20fb555279237ef81500727ff105fa47ff1554bf/Tarea3/img/sc23.png) 

---
## Configuración del Software de OpenVPN 
---
Se utiliza la herramienta OpenVPN para la instalación del cliente local.
#### Paso 1.
Se descarga el archivo generado mediante SSH
![integrantes](https://github.com/Mocta-996/Redes_1S2022/blob/20fb555279237ef81500727ff105fa47ff1554bf/Tarea3/img/sc24.png)
#### Paso 2.
Se instala y se abre la aplicaición OpenVPN y luego se carga el archivo descargado, en este caso es el archivo maynor.opvn y se conecta. 
![integrantes](https://github.com/Mocta-996/Redes_1S2022/blob/20fb555279237ef81500727ff105fa47ff1554bf/Tarea3/img/sc26.png)
y con esto se conecta al servicio VPN
![integrantes](https://github.com/Mocta-996/Redes_1S2022/blob/20fb555279237ef81500727ff105fa47ff1554bf/Tarea3/img/sc27.png) 

---
## Pruebas de conexión 
---
- PC1 Maynor Octavio Piló Tuy
Configuración del protocolo IP:
![integrantes](https://github.com/Mocta-996/Redes_1S2022/blob/20fb555279237ef81500727ff105fa47ff1554bf/Tarea3/img/sc28.png) 
Pruebas de conexión PING:
![integrantes](https://github.com/Mocta-996/Redes_1S2022/blob/20fb555279237ef81500727ff105fa47ff1554bf/Tarea3/img/sc29.png) 






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
![creacion](https://github.com/Mocta-996/Redes_1S2022/blob/20fb555279237ef81500727ff105fa47ff1554bf/Tarea3/img/sc1.png width="50")
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





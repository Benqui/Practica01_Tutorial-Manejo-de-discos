# Tutorial: Manejo de discos
### Creado por:
* Benjamin Hoyos Herrera 
* Angel Yedid Nacif Mena
* Carlos Abraham Martines Zamora
* Genaro Gonzales Lozada  
Practica 01 de la materia de Sistemas Operativos 2  
Este es un tutoria para poder manejar 


## 1.Que es hda, sda y vda?
### hda es...
Es la unidad maestra en el controlador IDE principal, linux toma el primer disco duro como un disco duro completo 
### sda es...
El (Small computer sistem interface disk) sda es para dispositivos de almacenamiento tales como discos duros mecanicos, memorias ssd, usbs, etc; que soportan comandos SCSI, la conexion es manejada por el subsistema SCSI que tiene el kernel
### vda es...
Es la particion virtualizada de una maquina virtual, el rendimiento es mejor  ya que el hipervisor no tiene que emular ninguna interfaz de hardware

## 2.Como montar y desmontar un usb en el sistema por teminal?
Hay dos formas en las cuales puedes montar una memoria USB, la primera es sin tener permisos de lectura y escritura y la otra es con los permisos, lo unico que va   a cambiar es la linea de comando al momento de montar la memoria USB:

1. Conectar la memoria USB y abrir una terminal    
2. Crear una carpeta donde montar la memoria USB con el comando ```mkdir nombre_del_archivo``` y dentro de esa carpeta creamos otra carpeta donde haremos el montaje    
3. En terminal escribir: ```lsblk``` para ver una lista de particiones e identificar que particion es tu usb    
4. Una vez identificado tienes que escribir ```sudo blkid``` para saber el sistema de archivo que maneja en este ejemplo *sda2* tiene un tipo de sistema *vfat*    
5. Aqui vamos a hacer el montaje de la USB:
    - Para el montaje sin permisos de lectura y escritura el comando es el siguiente ```sudo mount -t "tipo sistema de archivo" /dev/sd# ./Direccion donde lo vas a montar```    
    - Para el montaje con permisos de lectura y escritura es asi ```sudo mount -t "tipo sistema de archivo" -o rw,umask=0 /dev/sd# ./Direccion donde lo vas a montar```    
6. Para desmontar un USB el comando es el siguiente ```sudo umount /dev/sd#```    


## 3.Como enlistar la informacion de los dispositivos de bloque conectados aunque no esten conectados?
Existen 3 comandos con las cuales se puede realizar un listado de dispositivos de bloques esten montados o no lo esten:
1. Usando el comando ```lsblk```, con este comando se va a mostrar un el listado de dispositivos de bloques dentro de toda la informacion que muestra lo mas importante son los puntos de montajes donde estan los dispositivos 
2. Usando el comando ```sudo blkid```, con este comando la informacion que se muestra es informacion especifica de los dispositivos como el sistema de archivos que utuliza
3. Usando el comando ```sudo fdisk -l```, con este comando muestra cosas como el tipo de etiqueta de disco, el indetidicador y las particiones que tiene con el espacio que ocupan, basicamente muestra las tablas de particiones de los discos

## 4.Como mostrar la tabla de particiones del disco donde esta instalado el sistema operativo en terminal?
Para esto usamoes el comando ```sudo fdisk -l``` sirve para ver las particiones de los dispositivos de bloques, para ver de manera especifica tienes que agregar como argumento a parte la direccion en este caso de donde esta instalado, esto se puede sabes con las instrucciones que vimos en el punto anterior, el comando que usas entonces es ```sudo fdisk -l /dev/direccion donde esta instalado el sistema operativo```    
[inserte imagen aqui]    
Aqui podemos ver que particion es el boot, donde esta instalado tu sistema operativo, etc.    

## 5.Como conectar una memoria USB y mostrar su tabla de particiones en terminal?
Seguimos los pasos para montar una memoria usb del paso 2, para despues una vez montada la USB tienes que hacer lo que hicimos en el paso 4 pero ahora con el bloque de dispositivo que tiene asignada la memoria USB    
[inserte imagen aca]    


## 6.Como borrar todas las particiones de un USB en terminal?
* Para esto vamos a usar el comando ```sudo fdisk /dev/sd#```    
* Se vera que ahora es diferente como se ve la teminal, ahora se ve asi    
* Esta es la lista de comandos que podemos desplegar con la leta "m"   
* Lo que vamos a hacer es borrar las particiones que tenemos, que en este caso tenemos 3 particiones a borrar
* Como muestra la lista de comandos para borrar tenemos que usar el comando "d" y sale lo siguiente:
* Te va a dar a escoger que particion quieres eliminar una vez seleccionado puedes comprobar que se elimino usando el comando "p"
* Una vez eliminadas todas las particiones usas el comando "w" para salir y guardar los cambios
* *OJO* cabe destacar que solo tienes que tener la USB *conectada* pero *NO MONTADA* por que sino te va a marcar error al querer guardar los cambios a las tablas de las particiones

## 7.Como crear en el USB tres particiones fisicsa y una extendida en terminal?

## 8.Como crear una particion dentre ode la particion extendida del USB en terminal?

## 9.Como borrar las particiones para que solo exista una particion que abasque toda la usb por la interfaz grafica?

## 10.Como copiar una archivo .iso de distribucion live de linux a una USB por medio del comando "dd"?
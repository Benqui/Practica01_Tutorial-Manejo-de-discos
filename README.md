# Tutorial: Manejo de discos
### Creado por:
* Benjamin Hoyos Herrera 
* Angel Yedid Nacif Mena
* Carlos Abraham Martines Zamora
* Genaro Gonzales Lozada  
Practica 01 de la materia de Sistemas Operativos 2  


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
![Parte 5](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part1_5.jpg)
3. En terminal escribir: ```lsblk``` para ver una lista de particiones e identificar que particion es tu usb    
![Parte 3](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part1_3.jpg)
4. Una vez identificado tienes que escribir ```sudo blkid``` para saber el sistema de archivo que maneja en este ejemplo *sda2* tiene un tipo de sistema *vfat*    
![Parte 4](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part1_4.jpg)
5. Aqui vamos a hacer el montaje de la USB:
    - Para el montaje sin permisos de lectura y escritura el comando es el siguiente ```sudo mount -t "tipo sistema de archivo" /dev/sd# ./Direccion donde lo vas a montar```    
    ![Parte 7](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part1_7.jpg)    
    ![Parte 8](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part1_8.jpg)    
    - Para el montaje con permisos de lectura y escritura es asi ```sudo mount -t "tipo sistema de archivo" -o rw,umask=0 /dev/sd# ./Direccion donde lo vas a montar```    
    ![Parte 10](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part1_10.jpg)    
    ![Parte 11](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part1_11.jpg)    
6. Para desmontar un USB el comando es el siguiente ```sudo umount /dev/sd#```    
![Parte 9](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part1_9.jpg)


## 3.Como enlistar la informacion de los dispositivos de bloque conectados aunque no esten conectados?
Existen 3 comandos con las cuales se puede realizar un listado de dispositivos de bloques esten montados o no lo esten:
1. Usando el comando ```lsblk```, con este comando se va a mostrar un el listado de dispositivos de bloques dentro de toda la informacion que muestra lo mas importante son los puntos de montajes donde estan los dispositivos    
![Parte 1](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part2_1.png)
2. Usando el comando ```sudo blkid```, con este comando la informacion que se muestra es informacion especifica de los dispositivos como el sistema de archivos que utuliza
![Parte 2](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part2_2.jpg)
3. Usando el comando ```sudo fdisk -l```, con este comando muestra cosas como el tipo de etiqueta de disco, el indetidicador y las particiones que tiene con el espacio que ocupan, basicamente muestra las tablas de particiones de los discos
![Parte 3](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part2_3.jpg)

## 4.Como mostrar la tabla de particiones del disco donde esta instalado el sistema operativo en terminal?
Para esto usamos el comando ```sudo fdisk -l``` sirve para ver las particiones de los dispositivos de bloques, para ver de manera especifica tienes que agregar como argumento a parte la direccion en este caso de donde esta instalado, esto se puede sabes con las instrucciones que vimos en el punto anterior, el comando que usas entonces es ```sudo fdisk -l /dev/direccion donde esta instalado el sistema operativo```    
![Parte 1](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part3_1.jpg)    
Aqui podemos ver que particion es el boot, donde esta instalado tu sistema operativo, etc.    

## 5.Como conectar una memoria USB y mostrar su tabla de particiones en terminal?
Seguimos los pasos para montar una memoria usb del paso 2, para despues una vez montada la USB tienes que hacer lo que hicimos en el paso 4 pero ahora con el bloque de dispositivo que tiene asignada la memoria USB    
![Parte 4](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part4_1.jpg)    


## 6.Como borrar todas las particiones de un USB en terminal?
* Para esto vamos a usar el comando ```sudo fdisk /dev/sd#```    
* Se vera que ahora es diferente como se ve la teminal, ahora se ve asi    
![Parte 1](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part5_1.jpg)    
* Esta es la lista de comandos que podemos desplegar con la leta ```m```   
![Parte 2](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part5_2.jpg)    
* Lo que vamos a hacer es borrar las particiones que tenemos, que en este caso tenemos 3 particiones a borrar
![Parte 3](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part5_3.jpg)    
* Como muestra la lista de comandos para borrar tenemos que usar el comando ```d``` y sale lo siguiente:
![Parte 4](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part5_4.jpg)    
* Te va a dar a escoger que particion quieres eliminar una vez seleccionado puedes comprobar que se elimino usando el comando ```p```
![Parte 5](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part5_5.jpg)    
* Una vez eliminadas todas las particiones usas el comando ```w``` para salir y guardar los cambios
![Parte 8](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part5_8.jpg)    
* *OJO* cabe destacar que solo tienes que tener la USB *conectada* pero *NO MONTADA* por que sino te va a marcar error al querer guardar los cambios a las tablas de las particiones
![Parte 9](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part5_9.jpg)    

## 7.Como crear en el USB tres particiones fisicsa y una extendida en terminal?
* Empezamos con el comando ```sudo fdisk /dev/sd#```
![Parte 1](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/part6_1.jpg)    
* Ahora para crear particiones fisicas necesitamos oprimir la tecla ```n``` para crear una nueva particion selecccionamos el numero de la particion que vamos a crear en este caso el __1__, para el __First Sector__ damos ```Enter```, para __Last Sector__ tenemos que dar la capacidad de memoria
![Parte 2](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part6_2.jpg)     
    - Para comprobar que si se creo la particion imprimimos la lista con la letra ```p```    
    ![Parte 3](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/part6_3.jpg)     
* Creamos 2 particiones mas     
![Parte 4](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/part6_4.jpg)     
* Ahora para crear una particion extendida seleccionamos ```n``` y ahora escogemos la opcion ```e``` que es la opcion extendida y damos enter ya que solo nos queda una particion damos ```Enter``` __First Sector__ damos ```Enter```, para __Last Sector__ igual damos ```Enter``` para dejar de default lo que queda de la memoria de la USB     
![Parte 5](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/part6_5.jpg)     
* Damos ```w``` para salir y guardar las particiones
![Parte 8](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part5_8.jpg)     
* Ahora ya tenemos las 3 particiones fisicas y la extendida

## 8.Como crear una particion dentro de la particion extendida del USB en terminal?
* Una vez ya creadas las particiones del punto anterior, volveremos a usar el comando ```sudo fdisk /dev/sd#``` y *crearemos una nueva particion*
![Parte 1](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part7_1.jpg)     
* Antes de continuar quiero explicar que una vez creada la particion __Extendida__ las siguientes particiones que crees seran __particiones logicas__ creadas en la particion extendida
![Parte 2](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part7_2.jpg)     
* El proceso es casi igual al proceso del punto anterior solo que ahora no te pide el tipo de particion sera (primaria o extendida) solo te pedira el __First Sector__ al cual le vamos a dar ```enter``` y el __Last Sector__ aqui pondras la memoria que le vas a asignar. Podemos ver que se creo la particion con el comando ```p```
![Parte 3](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part7_3.jpg)     
* Puedes repetir el proceso dependiendo si te queda espacio en la memoria extendida
![Parte 4](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part7_4.jpg)     
* *OJO* si borras la particion extrendida *Se borraran las particiones logicas que hayas creado*, las puedes recuperar si sale si y no guardas los cambios

## 9.Como borrar las particiones para que solo exista una particion que abarque toda la usb por la interfaz grafica disks?
* Como estamos usando ubuntu, tenemos un programa llamado __disks__ que es para crear, borrar, eliminar y cambiar el tamaño de las particiones
![Parte 1](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part8_1.jpg)     
* Lo vamos a buscar en el menu de programas y damos ```enter``` 
![Parte 2](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part8_2.jpg)     
* Ya en la terminal buscamos nuestra memoria USB y empezaremos con la eliminación de las particiones que hemos creado para solo tener solo una particion
![Parte 3](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part8_3.jpg)     
* Vamos a empezar eliminando la particion extendida que por ende va a borrar las particiones lógicas que hemos creado, para esto damos click sobre la __particion numero 4__ y damos click al boton de __menos__
![Parte 4](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part8_4.jpg)     
* Saldra una ventana que nos dira si estamos seguros de eliminar la particion y esperamos a que se elimine
![Parte 5](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part8_5.jpg)     
* Ahora haremos lo mismo con las particions __2__ y __3__ 
* Una vez que tenemos solo una particion y mucho espacio libre 
![Parte 6](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part8_6.jpg)     
* Vamos a seleccionar la particion numero 1 y damos click al boton de los engranes (configuracion) y seleccionamos __resize__
![Parte 7](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part8_7.jpg)     
![Parte 8](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part8_8.jpg)     
* Saldra una ventana que nos dira cuanta memoria queremos agregarle y le damos a abarcar todo el espacio libre
![Parte 9](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part8_10.jpg)     
![Parte 10](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part8_10.jpg)     
![Parte 11](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part8_11.jpg)     

## 10.Como copiar una archivo .iso de distribucion live de linux a una USB por medio del comando "dd"?
* Primero necesitamos descargar una iso, en este caso usamos la iso de Ubuntu que se guardo en la carpeta de descargas.
![Parte 2](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part9_2.jpg)     
* Una vez descargada conectamos la usb y realizamos el siguiente comando en la terminal escribirmos ```sudo dd if=/[Direccions del iso] of=/[Nombre de la particion] satatus progress```     
![Parte 1](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part9_1.jpg)     
![Parte 3](https://github.com/Benqui/Practica01_Tutorial-Manejo-de-discos/blob/main/media/Part9_3.jpg)     



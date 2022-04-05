# Ejercicio 1 - trabajo con imágenes

## Servidor web

**Arranca un contenedor que ejecute una instancia de la imagen php:7.4-apache , que se llame web y que sea accesible desde un navegador en el puerto 8000.** 

**Colocar en el directorio raíz del servicio web ( /var/www/html ) de dicho contenedor un fichero llamado index.html con el siguiente contenido: Deberás sustituir XXXXXXXXXXX por tu nombre y tus apellidos.** 

**Colocar en ese mismo directorio raíz un archivo llamado mes.php que muestre el nombre del mes actual. Ver la salida del script en el navegador Borrar el contenedor**



```


```



-Descargo la imagen oficial

```
docker pull php:7.4-apache
```

![image-20220331100831718](Ejercicio%201%20-%20trabajo%20con%20im%C3%A1genes.assets/image-20220331100831718.png)



-Creo el contenedor a partir de esa imagen

```
 docker run -d --name web -p 8000:80 php:7.4-apache
```

![image-20220331101105850](Ejercicio%201%20-%20trabajo%20con%20im%C3%A1genes.assets/image-20220331101105850.png)



-Compruebo que esta activo

```
docker ps
```

![image-20220331101134737](Ejercicio%201%20-%20trabajo%20con%20im%C3%A1genes.assets/image-20220331101134737.png)

-Creo y coloco en el directorio raiz el index con el h1 

```
docker exec web bash -c 'echo "<h1>Hola soy Yesmina Perez </h1>" > /var/www/html/index.html'
```

-Compruebo que se ha cambiado el mensaje

![image-20220331101758495](Ejercicio%201%20-%20trabajo%20con%20im%C3%A1genes.assets/image-20220331101758495.png)



-Coloco en el mismo directorio el archivo del mes 

```
docker exec web bash -c 'echo "<?php echo date('F'); ?>"  > /var/www/html/mes.php'
```

![image-20220331112148014](Ejercicio%201%20-%20trabajo%20con%20im%C3%A1genes.assets/image-20220331112148014.png)



Me da error por no meter mes en una variable pero al meterlo me da error  de sintaxis el "=" con este codigo

```
 docker exec web bash -c 'echo "<?php $mes = date('F'); echo $mes; ?>"  > /var/www/html/mes.php'

```

-Borrar el contenedor

Primero lo detengo

```
docker stop web
```

![image-20220331112640212](Ejercicio%201%20-%20trabajo%20con%20im%C3%A1genes.assets/image-20220331112640212.png)



Luego ya lo puedo borrar

```
docker rm web
```

Y listo todos los contenedores a ver si esta

```
docker ps -a
```

![image-20220331112817073](Ejercicio%201%20-%20trabajo%20con%20im%C3%A1genes.assets/image-20220331112817073.png)



-Peso del contenedor sin nada

![image-20220331115759684](Ejercicio%201%20-%20trabajo%20con%20im%C3%A1genes.assets/image-20220331115759684.png)



-Peso despues de crear los dos archivos.

![image-20220331120023886](Ejercicio%201%20-%20trabajo%20con%20im%C3%A1genes.assets/image-20220331120023886.png)





## Servidor de base de datos

**Arrancar un contenedor que se llame bbdd y que ejecute una instancia de la imagen mariadb Antes de arrancarlo, visita la página en Docker Hub** 

**Establece las variables de entorno necesarias para que: La contraseña de root sea root .**

 **Crear una base de datos automáticamente al arrancar que se llame prueba .** 

**Crear el usuario invitado con la contraseña invitado .**

-Descargo la imagen

```
docker pull mariadb
```

-Creo el contenedor con las variables que se me piden( "-e" para asignar las variables de entorno)

```
docker run -d --name bbdd -e MARIADB_ROOT_PASSWORD=root -e MARIADB_USER=invitado -e MARIADB_PASSWORD=invitado -e MARIADB_DATABASE=prueba -d mariadb
docker run -d --name bbdd \
-e MYSQL_DATABASE=prueba \
-e MYSQL_USER=invitado \
-e MYSQL_PASSWORD=invitado \
-e MYSQL_ROOT_PASSWORD=root \
mariadb

```

![image-20220331124247863](Ejercicio%201%20-%20trabajo%20con%20im%C3%A1genes.assets/image-20220331124247863.png)



-compruebo que esta creado

![image-20220331124407040](Ejercicio%201%20-%20trabajo%20con%20im%C3%A1genes.assets/image-20220331124407040.png)



-Me conecto al contenedor con el usuario invitado

```

docker exec -it bbdd mysql -u invitado -p 

```

![image-20220401110136516](Ejercicio%201%20-%20trabajo%20con%20im%C3%A1genes.assets/image-20220401110136516.png)



-Compruebo que la base de datos prueba esta.

```
show databases;
```

![image-20220401110247991](Ejercicio%201%20-%20trabajo%20con%20im%C3%A1genes.assets/image-20220401110247991.png)



-Compruebo que no se puede borrar la imagen



```
docker rmi mariadb
```

![image-20220401110547243](Ejercicio%201%20-%20trabajo%20con%20im%C3%A1genes.assets/image-20220401110547243.png)



-Pantallazo de mis imagenes

![image-20220401110643839](Ejercicio%201%20-%20trabajo%20con%20im%C3%A1genes.assets/image-20220401110643839.png)



-Elimino el contenedor utilizado, primero lo paro y luego ya se podria borrar y por ultimo listo todos

```
docker stop bbdd
docker rm bbdd
docker ps -a
```

![image-20220401110913091](Ejercicio%201%20-%20trabajo%20con%20im%C3%A1genes.assets/image-20220401110913091.png)


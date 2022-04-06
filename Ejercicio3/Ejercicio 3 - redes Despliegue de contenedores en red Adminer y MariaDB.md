# Ejercicio 3 - redes Despliegue de contenedores en red: Adminer y MariaDB

## 1. Crea una red bridge redbd

```
docker network create redbd
```

![image-20220405121515363](C:/Users/yesmi/AppData/Roaming/Typora/typora-user-images/image-20220405121515363.png)

## 

## 2.Crea un contenedor con una imagen de mariaDB que estará en la red redbd .

##  Este contenedor se ejecutará en segundo plano, y será accesible a través del puerto 3306. (Es necesario definir la contraseña del usuario root y un volumen de datos persistente)

```
docker run --name contenedor1 -v /home/daw/datadir:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root -e MARIADB_DATABASE=prueba -d --network redbd -p 3306:3306 mariadb

```



![image-20220405131627512](C:/Users/yesmi/AppData/Roaming/Typora/typora-user-images/image-20220405131627512.png)

## 3. Crea un contenedor con Adminer que se pueda conectar al contenedor de la BD

```
docker pull adminer
```

![image-20220405125721062](C:/Users/yesmi/AppData/Roaming/Typora/typora-user-images/image-20220405125721062.png)

```
docker run -d --name contenedor2 --link contenedor1:mariadb --network redbd -p 8080:8080 adminer

```

![image-20220406100815284](Ejercicio%203%20-%20redes%20Despliegue%20de%20contenedores%20en%20red%20Adminer%20y%20MariaDB.assets/image-20220406100815284.png)

-compruebo que los dos contenedores estan ok

![image-20220406100850068](Ejercicio%203%20-%20redes%20Despliegue%20de%20contenedores%20en%20red%20Adminer%20y%20MariaDB.assets/image-20220406100850068.png)

## 4. Comprueba que el contenedor Adminer puede conectar con el contenedor mysql abriendo un navegador web y accediendo a la URL: http://localhost:8080





![image-20220405133345886](C:/Users/yesmi/AppData/Roaming/Typora/typora-user-images/image-20220405133345886.png)

![image-20220405133435941](C:/Users/yesmi/AppData/Roaming/Typora/typora-user-images/image-20220405133435941.png)

### Pantallazo donde se vea la creación de una BD con la interfaz web Adminer

![image-20220406101600143](Ejercicio%203%20-%20redes%20Despliegue%20de%20contenedores%20en%20red%20Adminer%20y%20MariaDB.assets/image-20220406101600143.png)

### Pantallazo donde se entre a la consola del servidor web en modo texto y se compruebe que se ha creado la BD

```
docker exec -it contenedor1 bash -c 'mysql -u root -p'

```

![image-20220406102545602](Ejercicio%203%20-%20redes%20Despliegue%20de%20contenedores%20en%20red%20Adminer%20y%20MariaDB.assets/image-20220406102545602.png)

![image-20220406102726114](Ejercicio%203%20-%20redes%20Despliegue%20de%20contenedores%20en%20red%20Adminer%20y%20MariaDB.assets/image-20220406102726114.png)

### Borrar los contenedores, la red, y los volúmenes utilizados

-Paramos y borramos los contenedores

![image-20220406103551326](Ejercicio%203%20-%20redes%20Despliegue%20de%20contenedores%20en%20red%20Adminer%20y%20MariaDB.assets/image-20220406103551326.png)

-Ahora ya podriamos borrar la red

```
docker network rm redbd
```

![image-20220406103730652](Ejercicio%203%20-%20redes%20Despliegue%20de%20contenedores%20en%20red%20Adminer%20y%20MariaDB.assets/image-20220406103730652.png)

-Y por ultimo busco y limpio todos los volumenes creados ( con lo del alamcenamiento persistente )y porque me confundi varias veces al crear los contenedores .

```
docker volume ls
```

![image-20220406104220817](Ejercicio%203%20-%20redes%20Despliegue%20de%20contenedores%20en%20red%20Adminer%20y%20MariaDB.assets/image-20220406104220817.png)

```
docker volume prune
```

![image-20220406104400446](Ejercicio%203%20-%20redes%20Despliegue%20de%20contenedores%20en%20red%20Adminer%20y%20MariaDB.assets/image-20220406104400446.png)

-compruebo que se hayan borrado

![image-20220406104611983](Ejercicio%203%20-%20redes%20Despliegue%20de%20contenedores%20en%20red%20Adminer%20y%20MariaDB.assets/image-20220406104611983-16492347786941.png)


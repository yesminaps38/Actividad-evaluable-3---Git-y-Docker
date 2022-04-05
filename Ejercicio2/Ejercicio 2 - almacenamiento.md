# Ejercicio 2 - almacenamiento

## Bind mount para compartir datos

### 1. Crea una carpeta llamada saludo y dentro de ella crea un fichero llamado index.html con el siguiente contenido (Deberás sustituir ese XXXXX por tu nombre.HOLA SOY XXXXXX)



-Creo la carpeta

```
mkdir saludo
```

-Entro en ella

```
cd saludo
```

-Creo y escribo el saludo

```
echo "<h1>Hola soy yesmina<h1>" > index.html
```

## 2. Una vez hecho esto arrancar dos contenedores basados en la imagen php:7.4-apache que hagan un bind mount de la carpeta saludo en la carpeta /var/www/html del contenedor. Uno de ellos vamos a acceder con el puerto 8181 y el otro con el 8282. Y su nombres serán c1 y c2 .

-Creo los dos contenedores

```
docker run -d --name c1 --mount
type=bind,src=/home/daw/saludo,dst=/var/www/html/ -p
8181:80 php:7.4-apache

```



```
docker run -d --name c2 --mount
type=bind,src=/home/daw/saludo,dst=/var/www/html/ -p
8282:80 php:7.4-apache
```

![image-20220401120437052](C:/Users/yesmi/AppData/Roaming/Typora/typora-user-images/image-20220401120437052.png)

y accedo a los puertos para ver si funcionan

![image-20220401120717060](C:/Users/yesmi/AppData/Roaming/Typora/typora-user-images/image-20220401120717060.png)

![image-20220401120804546](C:/Users/yesmi/AppData/Roaming/Typora/typora-user-images/image-20220401120804546.png)

## 4. Comprueba que puedes seguir accediendo a los contenedores, sin necesidad de reiniciarlos.

-Abro otra ventana en el terminal y me conecto al contenedor

```
docker exec -it c1 bash
```

![image-20220401121453279](C:/Users/yesmi/AppData/Roaming/Typora/typora-user-images/image-20220401121453279.png)

-desde alli modifico el index

```
echo "<h1>Hola de nuevo<h1>" > index.html
```

-y compruebo que se ha cambiado en el navegador

![image-20220401122454662](C:/Users/yesmi/AppData/Roaming/Typora/typora-user-images/image-20220401122454662.png)

Repito los mismos pasos con el otro contenedor y veo que se cambia

![image-20220401122736536](C:/Users/yesmi/AppData/Roaming/Typora/typora-user-images/image-20220401122736536.png)

![image-20220401122827529](C:/Users/yesmi/AppData/Roaming/Typora/typora-user-images/image-20220401122827529.png)

### \5. Borra los contenedores utilizados.

```
docker stop c1
docker stop c2
docker rm c1
docker rm c2

```

![image-20220401123055527](C:/Users/yesmi/AppData/Roaming/Typora/typora-user-images/image-20220401123055527.png)

![image-20220401123019599](C:/Users/yesmi/AppData/Roaming/Typora/typora-user-images/image-20220401123019599.png)


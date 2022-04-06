# Ejercicio 4 - imagen con Dockerfile

Crear una imagen con un servidor web que sirva un sitio web Basar la imagen en nginx o apache Desplegar una plantilla, o un proyecto tuyo, que tenga, al menos, un index.html y una carpeta para estilos, imágenes, etc.



-creo la carpeta con mi html como se pide y creo el fichero dockerfile

![image-20220406120311809](C:/Users/yesmi/AppData/Roaming/Typora/typora-user-images/image-20220406120311809.png)

```
gedit Dockerfile
```

y escribo lo siguiente dentro del fichero

```
FROM nginx
ADD public_html /usr/share/nginx/html
EXPOSE 80
```

![image-20220406115542352](C:/Users/yesmi/AppData/Roaming/Typora/typora-user-images/image-20220406115542352.png)

-Ahora ya puedo construir mi imagen



```
docker build -t hbs71754/ejemplo1:v1 .

```

![image-20220406121033041](C:/Users/yesmi/AppData/Roaming/Typora/typora-user-images/image-20220406121033041.png)

Comprobamos que se ha creado la imagen

```
docker images
```

![image-20220406121137688](C:/Users/yesmi/AppData/Roaming/Typora/typora-user-images/image-20220406121137688.png)

-Creamos el contenedor

```
 docker run -d -p 80:80 --name ejemplo1 hbs71754/ejemplo1:v1
```

![image-20220406121310693](C:/Users/yesmi/AppData/Roaming/Typora/typora-user-images/image-20220406121310693.png)

y ahora compuebo que funciona desde el navegador

![image-20220406121533492](C:/Users/yesmi/AppData/Roaming/Typora/typora-user-images/image-20220406121533492.png)

-Por ultimo lo subo a mi cuenta de dockerhub

```
docker login
```

![image-20220406122003637](C:/Users/yesmi/AppData/Roaming/Typora/typora-user-images/image-20220406122003637.png)

-necesitamos que nuestra imagen se llame **nombre_de_usuario/nombre_del_repositorio:etiqueta**.

```
docker tag hbs71754/ejemplo1:v1 ejemplo1

```

```
docker push hbs71754/ejemplo1:v1
```

![image-20220406122947720](C:/Users/yesmi/AppData/Roaming/Typora/typora-user-images/image-20220406122947720.png)

-Ahora compruebo que se ha subido a mi dockerhub

![image-20220406123032248](C:/Users/yesmi/AppData/Roaming/Typora/typora-user-images/image-20220406123032248.png)


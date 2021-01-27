# NGINX
## Índice

1. [Introducción](#int)
2. [Comparativa con Apache](#com)
3. [Esquema de red](#esq)
4. [Instalación](#ins)
5. [Casos prácticos](#cas)
6. [Referencias](#ref)

<a name="int"></a>
## 1.- Introducción

En este proyecto vamos a crear un servidor web usando NGINX, estudiando el proceso de creación instalación y realizaremos una comparativa con Apache.

<a name="com"></a>
## 2.- Comparativa con Apache

NGINX y Apache son servidor web muy populares usados para ofrecer páginas web a nuestros clientes. Ambos son usados en mas de 500 grandes empresas de todo el mundo.

### Apache

  - Apache fue lanzado al mercado en 1995
  - Apache esta integrado en muchas de las distribuciones mas populares de Linux, como Red Hat o CentOS.
  - Apache usa .htaccess para su configuración. Hay muchos tutoriales de como trabajar con dicho fichero. Permite configurar cosas como redireccionamiento, máxima capacidad de subida de ficheros, limites de memoria, cookies, etc.
  - Cada directorio de Apache tiene su propio archivo de configuración .htaccess.
  - Una de las grandes características de Apache es la facilidad para trabajar con modulos. Con un par de comandos podemos activar y desactivar modulos sin tener que acceder a ningun archivo de configuración.

### Nginx

  - NGINX fue lanzado al mercado en 2004.
  - El mercado de NGINX ha crecido de forma estable durante años.
  - NGINX no tiene configuraciones a nivel de directorio, a diferencia de Apache, lo cual ayuda enormemente en el rendimiento.

<a name="esq"></a>
## 3.- Esquema de red

Para esta tarea, tendremos un servidor virtual con dos tarjeta de red. Una en modo adaptador puente y otra en red interna. Acto seguido, iniciamos la máquina y seguimos el siguiente procedimiento:

1.- Detenemos el servicio de NetworkManager
```
$ systemctl stop NetworkManager
```
2.- Deshabilidad el servicio de NetworkManager
```
$ systemctl disable NetworkManager
```
3.- Accedemos a /etc/network/interfaces y editamos el fichero para configurar nuestros dos adaptadores de forma estática, debería de quedar de una forma similar:

![/img/4.png](/img/4.png)

4.- Reiniciamos el servicio networking:
```
$ systemctl restart networking
```

5.- Si nos hemos tenido ningun problema, con el comando "ip a" veremos el resultado de la configuración:

![/img/5.png](/img/5.png)

<a name="ins"></a>
## 4.- Instalación



<a name="cas"></a>
## 5.- Casos prácticos

### Versión usada de Nginx
La versión que vamos a usar en estre proyecto de Nginx es la 1.14.2.

### Servicio asociado

En este apartado vamos a ver como trabajar con el servicio de Nginx:

- Reiniciar Nginx
```
$ systemctl restart nginx
```
- Habilitar Nginx
```
$ systemctl enable nginx
```
- Deshabilitar Nginx
```
$ systemctl disable nginx
```
- Iniciar Nginx
```
$ systemctl start nginx
```
- Parar Nginx
```
$ systemctl stop nginx
```
### Ficheros de configuración
Aquí vamos a ver los ficheros y rutas mas importantes a la hora de configurar Nginx:

- La ruta principal de Nginx es /etc/nginx/
- La ruta de los sitios web esta en /var/www/html/
- El fichero de configuración principal de Nginx se encuentra en /etc/nginx/nginx.conf. En este fichero podremos ajustar cosas como directivas del trafico de red, puertos de escucha o rutas de ficheros.
- En la carpeta sites-available tenemos los sitios web disponibles.
- En la carpeta sites-enabled tenemos los sitios web activados.
- En la carpeta modules-available tenemos todos los modulos disponibles.
- En la carpeta modules-enabled tenemos todos los modulos acivados.

### Editar la página web por defecto
Vamos a modificar la página web que se nos crea por defecto al instalar nginx:

1.- Accedemos al directorio de lo sitios web, veremos que tenemos un documento .html.
```
cd /var/www/html
```
2.- Lo editamos
```
nano index.nginx-debian.html
```
3.- Veremos algo similar: 

![/img/1.png](/img/1.png)

4.- Procedemos a editar el fichero a nuestro gusto, en mi caso solo lo modificaré ligeramente:

![/img/2.png](/img/2.png)

5.- Recargamos la página de Nginx y veremos que se han aplicado los cambios:

![/img/3.png](/img/3.png)

<a name="ref"></a>
## 6.- Referencias
- [www.digitalocean.com](https://www.digitalocean.com/)
- [www.linode.com](https://www.linode.com/docs/guides/how-to-configure-nginx/)

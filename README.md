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

El proceso para instalar Nginx es muy sencillo, sigamos los siguientes comandos para ello:

1.- Actualizamos los repositorios:
```
$ apt update
```
2.- Instalamos Nginx
```
$ apt install nginx
```
3.- Comprobamos el estado del servicio Nginx:
```
$ systemctl status nginx
```

<a name="cas"></a>
## 5.- Casos prácticos

### Versión usada de Nginx

Con este comando podemos saber la versión que estamos usado de Nginx:
```
nginx -v
```
Como podemos ver, la versión de Nginx actual es la 1.14.2.
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

### Virtual Hosting

Vamos a proceder a crear dos sitios web y a acceder a ellos usando nombres. Sigamos los siguientes pasos para ello:

1.- Creamos los directorio dentro de /var/www/html
```
$ sudo mkdir /var/www/html/web1.org
$ sudo mkdir /var/www/html/web2.org
```
2.- Le damos los siguientes permisos:
```
$ chown -R www-data:www-data web1.org
$ chown -R www-data:www-data web2.org
```
3.- Creamos un archivo index.html en ambas carpetas y escribimos un código similar a este:
```
<!DOCTYPE html>
<html>
<head>
<title>Bienvenidos a Nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Bienvenidos a Nginx!</h1>
<p>Antonio J. Holguin.</p>
<p><em>Esta es la web 1</em></p>
</body>
</html>
```
4.- Vamos a crear nuestros nuevos servidores virtuales, para ello accedemos a /etc/nginx/sites-available y copiamos el fichero "default" con el nombre "web1.conf" y "web2.conf". Acto seguido abrimos el nuevo fichero y lo editamos de la siguiente forma:
```
server {
        listen 80;
        listen [::]:80;

        server_name www.web1.org;

        root /var/www/web1.org;
        index index.html;

        location / {
                try_files $uri $uri/ =404;
        }

        access_log /var/log/nginx/web1.org-access.log;
        error_log /var/log/nginx/web1.org-error.log;
}
```
5.- Copiamos los archivos a sites-enabled:
```
$ sudo ln -s /etc/nginx/sites-available/web1.conf /etc/nginx/sites-enabled/
$ sudo ln -s /etc/nginx/sites-available/web2.conf /etc/nginx/sites-enabled/
```
6.- Reiniciamos el servicio Nginx:
```
$ sudo systemctl restart nginx
```
7.- Si todo ha ido bien, si escribimos www.web1.org o www.web2.org en nuestro buscador nos apareceran nuestras páginas web:

![/img/7.png](/img/7.png)

### Autorización



### SSL/TLS



<a name="ref"></a>
## 6.- Referencias
- [www.digitalocean.com](https://www.digitalocean.com/)
- [www.linode.com](https://www.linode.com/docs/guides/how-to-configure-nginx/)
- [www.chachocool.com](https://chachocool.com/como-instalar-nginx-en-debian-10-buster/#Como_configurar_Nginx_en_Debian_10)

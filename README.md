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



<a name="ref"></a>
## 6.- Referencias
- [DigitalOcean.com](https://www.digitalocean.com/)
- [How to install dnsmasq on Debian 10](https://www.server-world.info/en/note?os=Debian_10&p=dnsmasq&f=1)

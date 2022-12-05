# Instalaciion de Nagios y Apache2, En ubuntu server (Maquina virtual)

---


Instalacion de apache2 en una maquina virtual como servidor **Ubuntu Server**


**1. Actualizar sistema (Pre-instalacion)**


```bash

# Actualizacion del sistema
sudo apt update && sudo apt upgrade 

# Si queremos hacer una actualizacion mas larga pero mejor en ciertas ocaciones realizamos lo siguiente
sudo apt full-upgrade && sudo reboot

```


**2. Instalacion de dependencias (Preparando area)**


```bash
# Tener en cuenta que puede que algunos archivos ya se hayan actualizado, (en mi caso me funcionaron estas dependencias)

sudo apt install build-essential libgd-dev openssl libssl-dev unzip apache2 php gcc libdbi-perl libdbd-mysql-perl

```


**3. Instalacion de Nagios**


```bash
# Creamos una carpeta dedicada

> mkdir nagios && cd nagios

ping www.google.com # Combṕrobacion de internet

> wget wget https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.4.6.tar.gz -O nagioscore.tar.gz

> ls

nagioscore.tar.gz


# Para este punto quedara extraer el archivo

> tar xvzf nagioscore.tar.gz

# Nos habra creado una carpeta de nagios, ingresar en ella 

> cd nagios-4.4.6

```

**4. make**

```bash

# Llegamos a la parte final, esta me creo un dolor de cabeza pero espero ayudarte!


# Importante hacer este proceso como superusuario (sudo) y en la carpeta creada anteriormente de nagios

> sudo ./configure --with-https-conf=/etc/apache2/sites-enabled

> sudo make all

> sudo make install

> sudo make install-init

> sudo make install-commandmode

> sudo make install-config


# Antes de ingresar el ultimo paso realizaremos algo antes para que no te pase lo de a mi (quedarse barado por una hora)


# -----------ERROR--------------

> sudo make install-webconf

/usr/bin/install -c -m 644 sample-config/httpd.conf /etc/httpd/conf.d/nagios.conf
/usr/bin/install: cannot create regular file ‘/etc/httpd/conf.d/nagios.conf’: No such file or directory
Makefile:296: recipe for target 'install-webconf' failed
make: *** [install-webconf] Error 1


# ----------RESOLVERLO------------


> sudo /usr/bin/install -c -m 644 sample-config/httpd.conf /etc/apache2/sites-enabled/nagios.conf

# El ultimo fichero tambien se puede llamar "0000-default.conf"

> sudo ./configure --with-https-conf=/etc/apache2/sites-enabled

> sudo make install-webconf

```


**Listo!** Para verificar si hicimos todo bien, usamos 


```bash
> curl localhost
# curl 127.0.0.1
```


Si nos regresa algo, todo esta excelente 


<br>


![imagen2](./Captura%20de%20pantalla_2022-12-05_00-12-06.png)


##### Como extra

Si desde otra maquina (local)
ingresamos la ip LAN nos aparecera la pagina de apache en ubuntu en un navegador web!



# ShellInBrowser

Para exponer la terminal en un navegador usamos ShellInABox.

ShellInABox es un emulador de terminal web basado en ajax para cualquier navegador que soporte Javascript y CSS sin necesidad de disponer de ningún plugin adicional.

Al instalar certificados SSL/TTL, ShellInABox cifrará todas las comunicaciones cliente-servidor y también hará más difícil la labor de detección de los firewalls/NIDS más “inteligentes”.

```bash
sudo apt-get install openssl shellinabox
```

Por defecto, el servidor web shellinbox escuchará en el puerto 4200/TCP. Para modificarlo simplemente lo cambiaremos en el fichero de configuración

```bash
#En la ruta /etc/default/shellinabox

# shellinabox se inicia automaticamente
SHELLINABOX_DAEMON_START=1

# Puerto TCP que shellinabox estará escuchando
SHELLINABOX_PORT=443 # <- Modificamos el puerto

# Parámetros del sistema por defecto que pueden ser cambiados, pero no es necesario de modificar para que funcione
# SHELLINABOX_DATADIR=/var/lib/shellinabox
# SHELLINABOX_USER=shellinabox
# SHELLINABOX_GROUP=shellinabox


# Beeps deshabilitados por múltiples reportes de crasheos en Firefox Linux/x86_64
SHELLINABOX_ARGS="--no-beep"

```

Durante la instalación, si no encuentra un certificado adecuado, shellinabox intenta crear uno nuevo autofirmado (certificate.pem) mediante openssl. En ese caso el certificado creado se ubica en /var/lib/shellinabox.

Seguramente haya que darle permisos al certificado.
En mi caso le doy todos los permisos por comodidad.

```bash
sudo chmod 7777 certificate.pem
```

Debemos de asegurarnos que el servicio de ssh está activado y procedemos a activar el de shellinabox: 
``` bash
sudo service ssh.service status
sudo service shellinabox start
```

Para comprobar que se haya arrancado con éxito utilizamos:
```bash
sudo service shellinabox status
```

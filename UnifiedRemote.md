## Cómo configurar Unified Remote en Ubuntu 13.10

### Instalación y puesta en marcha del servidor

Descargar del blog de Unified Remote lo siguiente:
* servidor para Linux, en su versión para [32-bits](http://www.unifiedremote.com/download/server-3dp4-0-linux-32) o [64-bits](http://www.unifiedremote.com/download/server-3dp4-0-linux-64)
* [el paquete de remotes](https://github.com/unifiedremote/sandbox/archive/master.zip)

Una vez hecho esto, descomprimir el servidor y dentro de él descomprimir los remotes dentro de una carpeta llamada _remotes_. Para iniciar el servidor, ejecutar desde una consola:
  
	./engine

Por default, esto nos va a iniciar el servidor y una GUI Web para acceder a la configuración. Por defecto, este se encuentra accesible en [http://localhost:9510/manage/gui](http://localhost:9510/manage/gui).

Desde este momento ya se puede acceder a la aplicación desde el móvil y empezar a manejar tu computadora! Pero todavía hay un problema: ambos dispositivos deben estar conectados a la misma red Wi-Fi

### Cómo utilizar el Unified Remote "sin Wi-Fi"

En principio la app Android tiene soporte para Bluetooth, aunque no logré hacerlo funcionar por ese canal (vale la aclaración: las conexiones por Bluetooth vienen desactivadas por defecto, pero pueden ser activadas desde la GUI... igualmente tampoco me funcionó tras habilitarlo).

Se me ocurrió entonces probar configurando un hotspot desde mi notebook y conectarme a esa red desde Android y finalmente eso funcionó. Primero probé con la funcionalidad nativa para hacerlo pero mi Android no me encontraba la red. Luego de Googlear un rato encontré [esta guía](http://www.webupd8.org/2013/06/how-to-set-up-wireless-hotspot-access.html) con la que finalmente pude hacerlo andar.

Básicamente lo que hice fue instalar una aplicación llamada **AP-Hotspot** que levanta un hotspot con la configuración que nosotros especifiquemos y luego conectarme desde mi teléfono móvil. A modo de resumen, estos son los comandos para operar la aplicación:

```bash
# Instalación
sudo add-apt-repository ppa:nilarimogard/webupd8
sudo apt-get update
sudo apt-get install ap-hotspot

# Levantar el hotspot. La primera vez nos pedirá que le especifiquemos el SSID y password deseados
sudo ap-hotspot start

# Detener el hotspot
sudo ap-hotspot stop
```

**Importante:** para poder iniciar el servicio hay que previamente desconectarse de la red Wi-Fi en la que estemos. Si en cambio estamos conectados por cable, el software compartirá también internet con aquellos que se conecten a nuestra red.		
		
### Alias utiles

```bash
alias hotspot='sudo ap-hotspot start'
alias hotspot-stop='sudo ap-hotspot stop'

# Previamente hacer un symlink uf-remote que apunte al engine
alias unified-remote='hotspot && uf-remote' 
```

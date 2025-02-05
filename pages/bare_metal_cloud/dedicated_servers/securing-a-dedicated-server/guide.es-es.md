---
title: "Proteger un servidor dedicado"
excerpt: "Esta guía explica cómo aplicar medidas de seguridad básicas para proteger su servidor dedicado de ataques y accesos no autorizados"
updated: 2024-02-20
---

> [!primary]
> Esta traducción ha sido generada de forma automática por nuestro partner SYSTRAN. En algunos casos puede contener términos imprecisos, como en las etiquetas de los botones o los detalles técnicos. En caso de duda, le recomendamos que consulte la versión inglesa o francesa de la guía. Si quiere ayudarnos a mejorar esta traducción, por favor, utilice el botón «Contribuir» de esta página.
> 

## Objetivo

Los servidores dedicados no incluyen de forma nativa ningún protocolo de seguridad. Por lo tanto, usted deberá implementar las medidas necesarias para proteger su servidor dedicado. OVHcloud no podrá ser considerado responsable de los fallos de seguridad de la máquina.

**Esta guía ofrece algunos consejos para proteger un servidor basado en GNU/Linux.**

> [!warning]
>OVHcloud le ofrece los servicios que usted es responsable de configurar y gestionar. Usted es responsable de su buen funcionamiento.
>
>Si necesita ayuda, póngase en contacto con un proveedor de servicios especializado o debata el problema con nuestra comunidad de usuarios en https://community.ovh.com/en/. OVHcloud no puede ofrecerle soporte técnico.
>

## Requisitos

- Tener un [servidor dedicado de OVHcloud](/links/bare-metal/bare-metal).
- Tener acceso de administrador (sudo) al servidor por SSH.

## Procedimiento

> [!primary]
>
> Tenga en cuenta que se trata de una guía general basada en un sistema operativo Ubuntu Server. Tenga en cuenta que algunos comandos deben adaptarse a la distribución que utilice y que algunos consejos le invitan a utilizar herramientas de terceros. Si necesita ayuda, consulte la documentación oficial de estas aplicaciones.
>
> Si se trata de su primera configuración de un servidor dedicado de OVHcloud, consulte nuestra guía [Primeros pasos con un servidor dedicado](/pages/bare_metal_cloud/dedicated_servers/getting-started-with-dedicated-server).
>

Los siguientes ejemplos implican que está conectado como [usuario con permisos muy exigentes](/pages/bare_metal_cloud/dedicated_servers/changing_root_password_linux_ds).

### Actualizar el sistema operativo

Los desarrolladores de distribuciones y sistemas operativos ofrecen actualizaciones frecuentes de los paquetes, en muchas ocasiones por motivos de seguridad.<br>
Garantizar que su distribución o sistema operativo estén actualizados es un aspecto fundamental para proteger su servidor dedicado.

Esta actualización consta de dos etapas.

- Actualización de la lista de paquetes:

```bash
sudo apt update
```

- Actualización de los paquetes propiamente dichos:

```bash
sudo apt upgrade
```

Esta operación debe realizarse regularmente para mantener un sistema actualizado.

### Cambiar el puerto de escucha por defecto SSH

Una de las primeras acciones que deberá realizar en su servidor es configurar el puerto de escucha del servicio SSH. Por defecto, este se define en el **puerto 22**, por lo que los intentos de hackeo del servidor por parte de robots se dirigirán prioritariamente a este puerto.
La modificación de este parámetro, en beneficio de un puerto diferente, es una medida sencilla para reforzar la protección de su servidor contra los ataques automatizados.

Para ello, edite el archivo de configuración del servicio con el editor de texto que desee (`nano` se utiliza en este ejemplo):

```bash
sudo nano /etc/ssh/sshd_config
```

Encontrará las siguientes líneas o equivalentes:

```console
#Port 22
#AddressFamily any
#ListenAddress 0.0.0.0
```

Sustituya el número **22** por el número de puerto que desee.<br>
**Recuerde que no debe indicar un número de puerto que ya esté en uso en su sistema**.
Para mayor seguridad, utilice un número entre 49152 y 65535.<br>
Guarde y cierre el archivo de configuración.

Si la línea está "comentada" (es decir, precedida de un "#") como en el ejemplo anterior, asegúrese de eliminar el "#" antes de guardar el archivo para que se tenga en cuenta el cambio. Ejemplo:

```console
Port 49152
#AddressFamily any
#ListenAddress 0.0.0.0
```

Reinicie el servicio:

```bash
sudo systemctl restart sshd
```

Esto debería ser suficiente para aplicar los cambios. En caso contrario, reinicie el servidor (`sudo reboot`).

**Para Ubuntu 23.04 y versiones posteriores**

Para las últimas versiones de Ubuntu, la configuración SSH se gestiona ahora en el archivo `ssh.socket`.

Para actualizar el puerto SSH, edite la línea `Listenstream` en el archivo de configuración con un editor de texto de su elección (`nano` utilizado en este ejemplo):

```bash
sudo nano /lib/systemd/system/ssh.socket
```

```console
[Socket]
ListenStream=49152
Accept=no
```

Guarde los cambios y ejecute los siguientes comandos:

```bash
sudo systemctl daemon-reload
```

```bash
sudo systemctl restart ssh.service
```

Si ha activado el cortafuegos del sistema operativo, asegúrese de autorizar el nuevo puerto en las reglas del cortafuegos.

Recuerde que deberá indicar el nuevo puerto en cada solicitud de [conexión SSH al servidor](/pages/bare_metal_cloud/dedicated_servers/ssh_introduction):

```bash
ssh username@IPv4_server -p NewPortNumber
```

Ejemplo:

```bash
ssh ubuntu@203.0.113.100 -p 49152
```

> [!warning]
>
> Tenga en cuenta que la modificación del puerto por defecto de SSH o de cualquier otro protocolo conlleva un riesgo. Algunos servicios no pueden configurarse para ser utilizados con puertos no estándar y, por lo tanto, no funcionarán si modifica el puerto por defecto.
>

### Crear un usuario con permisos restringidos

Por lo general, las tareas que no requieran privilegios root deben realizarse a través de un usuario estándar. Para más información, consulte [esta guía](/pages/bare_metal_cloud/dedicated_servers/changing_root_password_linux_ds).

### Configurar el firewall interno (iptables)

Las distribuciones GNU/Linux habituales se entregan con un servicio de cortafuegos llamado iptables. Por defecto, este servicio no tiene ninguna regla activa. Puede comprobarlo introduciendo el siguiente comando:

```bash
iptables -L
```

Para más información sobre iptables, consulte nuestra [guía dedicada](/pages/bare_metal_cloud/dedicated_servers/firewall-Linux-iptable).

Le recomendamos que cree y adapte las reglas de firewall en función de su uso. Para más información sobre las diversas operaciones posibles, consulte la documentación oficial de la distribución utilizada.

### Instalar Fail2ban

Fail2ban es una aplicación de prevención contra intrusiones que actúa bloqueando las direcciones IP desde las que robots o atacantes intentan penetrar en el sistema.<br>
Es recomendable, y en algunos casos incluso indispensable, proteger su servidor de los ataques de tipo *Brute Force* o *Denial of Service*.

Para instalar el paquete de software, utilice el siguiente comando:

```bash
sudo apt install fail2ban
```

Puede personalizar los archivos de configuración Fail2ban para proteger los servicios expuestos a la internet pública contra los intentos de conexión repetidos.

Como recomienda Fail2ban, cree un archivo de configuración local de sus servicios copiando el archivo "jail.conf":

```bash
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```

Abra el archivo con un editor de texto:

```bash
sudo nano /etc/fail2ban/jail.local
```

Lea la información arriba del archivo, incluyendo los comentarios en `[DEFAULT]`.

La configuración `[DEFAULT]` es global, por lo que se aplicará a todos los servicios que se hayan definido para activarla (`enabled`) en este archivo. 

Es importante saber que los parámetros globales sólo se tendrán en cuenta si no hay valores diferentes definidos en las secciones servicios (`JAILS`) del archivo.

Consideremos estas líneas en `[DEFAULT]`:

```console
bantime = 10m
maxretry = 5
enabled = false
```

Esto significa que una dirección IP desde la que un host intenta conectarse se bloqueará durante diez minutos después del quinto intento de apertura de sesión fallido.<br>
Además, todos los parámetros especificados por `[DEFAULT]` y en las siguientes secciones permanecen desactivados a menos que se añada la línea `enabled = true` para un servicio (listado debajo `# JAILS`).

Por ejemplo de uso, el hecho de tener las siguientes líneas en la sección `[sshd]` activará restricciones únicamente para el servicio OpenSSH:

```console
[sshd]
enabled = true
port = ssh
filter = sshd
maxretry = 3
findtime = 5m
bantime  = 30m
```

En este ejemplo, si un intento de conexión SSH falla tres veces en cinco minutos, el período de prohibición de las IP será de 30 minutos.

Si lo ha cambiado, puede sustituir "ssh" por el número de puerto real.

El mejor enfoque es activar Fail2ban únicamente para los servicios que realmente se ejecutan en el servidor. Cada parámetro personalizado añadido en `# JAILS` tendrá preferencia sobre los valores predeterminados.

Una vez realizados los cambios, guarde el archivo y cierre el editor.

Reinicie el servicio para asegurarse de que se ejecuta con las personalizaciones aplicadas:

```bash
sudo service fail2ban restart
```

Fail2ban dispone de múltiples parámetros y filtros de personalización, así como de opciones predefinidas, por ejemplo, cuando desea añadir una capa de protección a un servidor web Nginx.

Para más información y recomendaciones sobre Fail2ban, consulte [la documentación oficial](https://www.fail2ban.org/wiki/index.php/Main_Page){.external} de esta herramienta.

### Configuración del firewall de red de OVHcloud 

Las soluciones de OVHcloud incluyen la posibilidad de activar un firewall de red en el punto de entrada de la infraestructura. Una configuración correcta de este cortafuegos permite bloquear las conexiones incluso antes de que lleguen al servidor.

Para activarlo, consulte la guía [Configurar el firewall de red](/pages/bare_metal_cloud/dedicated_servers/firewall_network).

### Guardar copia de seguridad del sistema y los datos

La noción de seguridad va más allá de proteger un sistema frente a posibles ataques. La protección de los datos es un aspecto fundamental. Por eso, OVHcloud ofrece un espacio de backup de 500 GB gratis con su servidor dedicado. Puede activar este espacio de backup en su área de cliente y acceder a él a través de los siguientes protocolos:

- FTP
- FTPS
- NFS
- CIFS

Para replicar sus datos y transferirlos a su espacio de backup, necesitará una solución de backup externa.

Para más información sobre este espacio de backup, consulte nuestra guía [Backup Storage](/pages/bare_metal_cloud/dedicated_servers/services_backup_storage){.external}.

## Más información

[Configurar el firewall de Windows](/pages/bare_metal_cloud/dedicated_servers/activate-port-firewall-soft-win)

[Network Firewall](/pages/bare_metal_cloud/dedicated_servers/firewall_network)

Si necesita formación o asistencia técnica para implantar nuestras soluciones, póngase en contacto con su representante de ventas o haga clic en [este enlace](/links/professional-services) para obtener un presupuesto y solicitar un análisis personalizado de su proyecto a nuestros expertos del equipo de Servicios Profesionales.

Interactúe con nuestra comunidad de usuarios en <https://community.ovh.com/en/>.
# INSTALACIÓN Y CONFIGURACIÓN

### CONFIGURACIÓN SERVIDOR DNS

*desactivar network-manager*

Para empezar instalaremos el paquete necesario y se instala con el siguiente comando:

``apt update``

``apt install dnsmasq``

Lo iniciamos:

``systemctl enable dnsmasq``

``systemctl start dnsmasq``

Tendremos dos tarjetas de red una adaptador puente y otra red interna, cuya configuración sera la siguiente: 

![adaptadores](https://github.com/estebancr1993/dnsmask/blob/main/img/adaptadores.JPG)

``systemctl restart networking``

Para configurar dnsmasq, necesita editar **``/etc/dnsmasq.conf``**. El archivo contiene extensos comentarios que explican sus opciones. Para todas las opciones disponibles, consulte [dnsmasq(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dnsmasq.8).

*Sugerencia: para verificar la sintaxis de los archivos de configuración, ejecute:*  ``dnsmasq --test``

Antes de tocar cualquien fichero de configuración hacer una copia: ``cp /etc/dnsmasq.conf /etc/dnsmasq.conf.ORIGINAL``

Añadir al fichero estas lineas: ``echo -e "strict-order \ninterface=enp0s8 \naddress=/esteban.es/192.168.3.1 \nlisten-address=192.168.3.1 \nlisten-address=127.0.0.1" >> /etc/dnsmasq.conf``

**strict-order** para que asi el servidor lea la configuración que aparece en el resolv.conf y de esta manera en el caso que nuestro dnsmasq no pueda resolver la petición, se encargara a preguntar a la maquina que tengamos en ese fichero indicada, **interfaces** indica que interfaz permite recibir peticiones, **address** la ip de los nombres de servicios que ofrece y **listen-addres** es para que este equipo escuche otros equipos en la red.

Modificar /etc/hosts

![hosts](https://github.com/estebancr1993/dnsmask/blob/main/img/hosts.JPG)

Modificar /etc/resolv.conf

![resolv](https://github.com/estebancr1993/dnsmask/blob/main/img/resolv.JPG)

Reiniciar DNSmask ``systemctl restart dnsmasq``

### CONFIGURACIÓN CLIENTE

En el cliente configuramos la IP y le indicamos el DNS que acabamos de configurar.

![cliente1](https://github.com/estebancr1993/dnsmask/blob/main/img/cliente1.JPG)

![cliente1DNS](https://github.com/estebancr1993/dnsmask/blob/main/img/cliente1DNS.JPG)

---

[ATRAS](https://github.com/estebancr1993/dnsmask/blob/main/README.md)

---
title: "Práctica: Creación y configuración de un escenario router-nat"
---

## Descripción

![router](img/router.png)

Queremos automatizar la creación de la siguiente infraestructura usando Vagrant, el esquema que queremos desarrollar, que vemos en la imagen, tiene las siguientes características:

Es escenario tiene dos máquinas:

* `router`, que está conectada a una red NAT con DHCP con el direccionamiento `192.168.200.0/24` y a una red privada (muy aislada). La interfaz de red en la red privada se configura con la IP `10.0.0.1`.
* `cliente`: Esta máquina está conectada a la misma red privada que la máquina anterior, en este caso su direccionamiento es `10.0.0.2`.


Queremos configurar el escenario con ansible, para que cumpla lo siguiente:

* La máquina cliente debe tener acceso a internet. Para ello debe salir por `eth1` y la máquina `router` debe estar configurada para enrutar las peticiones de cliente. Del mismo modo, `eth0` sólo se utiliza para acceder con `vagrant ssh`. Debes pensar qué configuración debe tener la máquina cliente: puerta de enlace, configuración dns,...

La receta ansible debe tener al menos 3 roles:

* `common`: Estas tareas se deben ejecutar en los dos nodos. La única tarea es actualizar los paquetes.
* `router`: Todas las tareas necesarias para configurar `router` cómo router-nat y que salga a internet por `eth1`. Las configuraciones deben ser permanentes.
* `cliente`: Todas las tareas necesarias para que el cliente salga a internet por `eth1`.

## Mejoras

1. La máquina `router` no está conectada a una red privada de tipo NAT, sino a una red pública.
2. Una vez terminado el ejercicio, modificar la configuración de vagrant para añadir otro cliente a la red interna. Volver a ejecutar la receta para configurar este nuevo cliente.
3. Modificar la configuración de vagrant y de ansible,para añadir un nuevo cliente a una nueva red interna muy aislada (con direccionamiento `10.1.0.0/24`) que estará conectada también a la máquina `router`. Realiza los cambios oportunos para que este nuevo cliente tenga acceso a internet de la misma manera que el los clientes anteriores.
4. Crea un nuevo rol en la receta ansible para instalar y configurar un servidor web en el `cliente`. Realiza los cambios necesarios para que el router haga DNAT y tengamos acceso al servidor web del cliente.

{% capture notice-text %}
## Entrega

1. Indica las mejoras que has realizado. 
2. Documenta en redmine los pasos fundamentales para realizar la práctica, con las pruebas de funcionamiento necesarias, para demostrar los pasos que estás dando.
3. Entrega la URL del repositorio git donde has alojado todos los ficheros.
4. Entrega una captura de pantalla accediendo por ssh a las dos máquinas (**sin utilizar `vagrant ssh`, es decir sin hacer conexiones a `eth0`**). Puedes usar las claves privadas generadas para cada una de las máquinas, o puedes generar nuevas claves que introduces en las máquinas. Usa la opción `-A`  de ssh para acceder al `cliente`.
{% endcapture %}<div class="notice--info">{{ notice-text | markdownify }}</div>



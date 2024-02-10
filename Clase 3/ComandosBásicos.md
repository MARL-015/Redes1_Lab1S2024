# LABORATORIO REDES DE COMPUTADORAS 1 - 1S2024

## **COMANDOS BÁSICOS PARA CONFIGURACIONES 📚**


**Guía de comandos básicos para uso en distintos dispositivos**

- Para ingresar al modo EXEC privilegiado 

    ```
    enable
    ```

- Para ingresar al modo Modo de Configuración Global 

    ```
    configure terminal ó conf t
    ```

- Para mostrar la configuración actual del dispositivo

    ```
    show run ó sh run
    ```

- Para salir de algún modo de configuración 
    ```
    exit
    ```
 
- Para desactivar la búsqueda de nombres de dominio (DNS) cuando se ingresan comandos que no son reconocidos como comandos del dispositivo.
    ```
    no ip domain-lookup
    ```

- En dispositivos de red como routers y switches, para guardar la configuración actual de forma permanente para que la configuración sea persistente después de reiniciar el dispositivo, se utilizan los siguientes comandos:

    ```
    write memory
    wr o do wr (modo configuración global)
    copy running-config startup-config
    ```

- Para establecer una contraseña en el modo EXEC privilegiado, se puede usar el siguiente comando:
    ```
    enable secret <contraseña-enable>
    ```
 - Para visualizar el protocolo ARP desde una pc
    ```
    arp -a
    ```
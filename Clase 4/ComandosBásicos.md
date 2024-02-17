# LABORATORIO REDES DE COMPUTADORAS 1 - 1S2024

## **COMANDOS PARA CONFIGURAR VLAN 📚**


**Guía de comandos utilizados en la configuración de packet tracer**

- **Para configurar VLANs en un Switch** 

    ```
    enable
    configure terminal
    hostname SW1
    ```

- creando y definiendo las vlans

    ```
    vlan 10
    name CONTABILIDAD
    vlan 20
    name ADMINISTRACION
    vlan 99
    name NATIVA
    exit
    ```

- configurando el modo troncal

    ```
    interface f0/24
    switchport mode trunk
    ```

- cambiando la vlan nativa 
    ```
    switchport trunk native vlan 99
    ```
 
- restringiendo las vlan que se pasarán en modo troncal
    ```
    switchport trunk allowed vlan 10,20,99,1002-1005
    ```

- configurando el modo acceso

    ```
    interface f0/1
    switchport mode access
    switchport access vlan 10

    interface f0/2
    switchport mode access
    switchport access vlan 20
    ```

- guardando la configuracion
    ```
    do write
    end
    ```

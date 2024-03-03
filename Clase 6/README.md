# Configuración de STP y VTP

## Topología a realizar

[![Topologia6.png](https://i.postimg.cc/13x0xxTF/Topologia6.png)](https://postimg.cc/nCk97WnV)

Teniendo la topologia nos damos cuenta que el Switch 1 no podria ser el puerto raiz porque ya tiene un puerto bloqueado (lo muestra el color naranja).

Al correr en un switch el comando sh spanning-tree nos muestra mensajes como: 
Root ID, la prioridad que por defecto en un switch cisco es 32769, el puente, las direcciones mac y puertos designados (conectados).

En el switch que tiene por defecto el root bridge nos muestre el mensaje.

[![Bridge.png](https://i.postimg.cc/85FmvL08/Bridge.png)](https://postimg.cc/TL6bM5xQ)

## Comandos Utilizados

<ol>
<li>SWITCH ROOT </li>
Configurar el switch como Server y Root.

### Server
    conf t 
    vtp domain redes1
    vtp password redes1
    vtp version 2 
    vtp mode server


### Configurar VLANS
    conft t

    vlan 10
    name RRHH
    exit 

    vlan 20
    name Informatica
    exit 

    vlan 30
    name Contabilidad
    exit 

    vlan 40
    name Ventas
    exit 


<li>Configuración de los puertos en modo trunk y envio de las VLANs.</li>

### en switch root 
    int f0/1
    switchport mode trunk
    switchport trunk allowed vlan 1,10,20,30,40,1002-1005

    int f0/2
    switchport mode trunk
    switchport trunk allowed vlan 1,10,20,30,40,1002-1005


<li>Se configuran las VLAN para que pertenezcan al Root Bridge.</li>

### vlan root
    conf t
    spanning-tree vlan 1 root primary
    spanning-tree vlan 10 root primary
    spanning-tree vlan 20 root primary
    spanning-tree vlan 30 root primary
    spanning-tree vlan 40 root primary


<li>Comandos para verificar las configuraciones</li>

### Verificar spanning tree
    sh spanning-tree brief

### Verificar vlans 
    show vlan

### Verificar VTP 
    sh vtp status

<li>Configuración de los switches que estarán en modo cliente</li>

### Server
    conf t 
    vtp domain redes1
    vtp password redes1
    vtp version 2 
    vtp mode client


<li>Configuración de los puertos en modo trunk y envio de las VLANs.</li>

### en switch root 
    int f0/1
    switchport mode trunk
    switchport trunk allowed vlan 1,10,20,30,40,1002-1005

    int f0/2
    switchport mode trunk
    switchport trunk allowed vlan 1,10,20,30,40,1002-1005

<li>Configuración de los puertos en modo access para dispositivos finales</li>

### SWITCH 1 
    int f0/10
    switchport mode access
    switchport access vlan 40

### SWITCH 0 
    int f0/10
    switchport mode access
    switchport access vlan 20

    int f0/11
    switchport mode access
    switchport access vlan 10

    int f0/12
    switchport mode access
    switchport access vlan 30


### SWITCH 2
    int f0/10
    switchport mode access
    switchport access vlan 30
    

<li>Para STP, Si damos un sh run nos damos cuenta que un switch por defecto ya trae configurado el modo pvst.</li>

[![pvst.png](https://i.postimg.cc/KYTHSSm3/pvst.png)](https://postimg.cc/6790nP2B)

También tenemos la mejora que seria el RSTP - que simplemente tiene un procesamiento mas rapido.

<li>Para poder configurar los dispositivos haciendo uso de este protocolo se necesitan ejecutar algunos comandos:</li>

### SWITCH 2
    conf t
    spanning-tree mode rapid-pvst

[![rstp.png](https://i.postimg.cc/bwynfQ8x/rstp.png)](https://postimg.cc/GHftkT4t)

</ol>

En caso se tenga comunicación entre VLANs se debe aplicar ACL para bloquear los puertos o el paso de una vlan hacia otra.

<li>Access Control List (ACL), o lista de control de acceso, es un conjunto de reglas que se utiliza para filtrar el tráfico en una red. Una ACL permite o niega el paso de paquetes de datos basándose en ciertos criterios, como direcciones IP, protocolos y números de puerto.</li>

### No permitir las VLAN
    access-list 101 deny ip 192.168.10.0 0.0.0.255 192.168.20.0 0.0.0.255
    access-list 101 deny ip 192.168.10.0 0.0.0.255 192.168.30.0 0.0.0.255
    access-list 101 deny ip 192.168.10.0 0.0.0.255 192.168.40.0 0.0.0.255

### VERIFICAR LAS ACCESS-LIST CREADAS
    sh access-list



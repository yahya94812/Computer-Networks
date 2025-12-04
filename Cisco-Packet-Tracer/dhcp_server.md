* dhcp_server is usually built in routers
* in the lan the dhcp server is enable in the following way:
    * assign ip address, subnet mask to the router interface
    * run the following commands in router cli:
    ```
    #Configure DHCP Pool
    ip dhcp pool LAN_POOL
    network 192.168.1.0 255.255.255.0
    default-router 192.168.1.1
    dns-server 8.8.8.8
    exit
    ```
    * go to each device and set the ip configuration to dhcp
    * after few seconds the devices will get ip address from the dhcp server(it will be visible)

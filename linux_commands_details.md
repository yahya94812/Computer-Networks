# 🔍 **Detailed Explanation of `ip a` Output**

`ip a` (short for `ip address`) shows **all network interfaces** on your system and all IP-related information about them.

Below is a breakdown of each interface in your output and what every line means.

* * *

# **1. Interface: `lo` (Loopback)**

```
1: lo: <LOOPBACK,UP,LOWER_UP> ...
```

### **Meaning**

* **lo** is the loopback interface (your computer talking to itself).
    
* **UP** → interface is enabled.
    
* **LOWER_UP** → link layer is functioning internally.
    

### **Addresses**

* `inet 127.0.0.1/8` → standard IPv4 loopback.
    
* `inet6 ::1/128` → IPv6 loopback.
    

Used for local applications to communicate (e.g., `localhost`).

* * *

# **2. Interface: `enp0s25` (Ethernet / Wired)**

```
2: enp0s25: <NO-CARRIER,BROADCAST,MULTICAST,UP> state DOWN
```

### **Meaning**

* **Ethernet interface**, but:
    
    * **NO-CARRIER** → cable unplugged, or no physical connection.
        
    * **state DOWN** → not operational.
        

### **Address**

* Only MAC address shown: `54:ee:75:51:fc:0d`
    
* **No IP address** because the cable is not connected.
    

* * *

# **3. Interface: `wlp4s0` (Wi-Fi)**

```
3: wlp4s0: <BROADCAST,MULTICAST,UP,LOWER_UP> state UP
```

### **Meaning**

* **Your active Wi-Fi interface**.
    
* **UP** → interface enabled.
    
* **LOWER_UP** → hardware link OK.
    
* Connected to a WiFi network.
    

### **MAC (WiFi hardware address)**

`5c:e0:c5:04:f2:bd`

### **IPv4 address**

```
inet 10.156.40.180/24
```

* Assigned via **DHCP**, because it says **dynamic**.
    
* `/24` → subnet mask `255.255.255.0`.
    
* Valid for **3360 seconds** (lease time).

* brd 10.156.40.255 refers to the broadcast address of your IPv4 network
* A broadcast address is a special IP address used to send a packet to all devices within the same subnet simultaneously.
    

### **IPv6 addresses**

You have **three IPv6 addresses**:

1. **Temporary IPv6** (privacy address) (Rotates for privacyUsed for outgoing connections (web browsing))
    
2. **Dynamic global IPv6** (More stable Used for incoming connections (if firewall allows)Your device identity on IPv6 )
    
3. **Link-local IPv6** (starts with `fe80:` — valid only inside local network)
    

IPv6 addresses rotate for privacy, hence multiple entries.

* * *

# **4. Interface: `docker0` (Docker Virtual Bridge)**

```
4: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> state DOWN
```

### **Meaning**

* Virtual interface created by Docker for container networking.
    
* **NO-CARRIER** and **DOWN** → no containers currently using it.
    

### **IP address**

```
inet 172.17.0.1/16
```

* Default Docker bridge IP (acts like a virtual router for containers).
    

* * *

# 🔑 **Summary of What the Output Tells You**

| Interface | Purpose | Status | IPv4 | IPv6 |
| --- | --- | --- | --- | --- |
| **lo** | Loopback | UP | 127.0.0.1 | ::1 |
| **enp0s25** | Wired LAN | DOWN | — | — |
| **wlp4s0** | Wi-Fi | UP | 10.156.40.180 | Several |
| **docker0** | Docker network | DOWN | 172.17.0.1 | — |

* * *

# ⭐ In essence:

Your **Wi-Fi (wlp4s0)** is the only active network interface with a working IP address. Ethernet cable is unplugged, Docker network exists but is unused, and loopback is standard.

* * *

# 🔍 **Detailed Explanation of `ip r` Output**
Your output:

```
default via 10.156.40.166 dev wlp4s0 proto dhcp src 10.156.40.180 metric 600
10.156.40.0/24 dev wlp4s0 proto kernel scope link src 10.156.40.180 metric 600
172.17.0.0/16 dev docker0 proto kernel scope link src 172.17.0.1 linkdown
```

Let's break it down:

* * *

# 1️⃣ **Default route (gateway to the internet)**

```
default via 10.156.40.166 dev wlp4s0 proto dhcp src 10.156.40.180 metric 600
```

### Meaning:

* **default** → any traffic that doesn’t match other routes (e.g., websites)
    
* **via 10.156.40.166** → this is your **gateway router IP**
    
* **dev wlp4s0** → use the **Wi-Fi interface**
    
* **src 10.156.40.180** → your Wi-Fi IPv4 address
    
* **metric 600** → route priority (lower = preferred)
    
* **proto dhcp** → obtained via DHCP
    

👉 This is how your system knows how to reach the internet.

* * *

# 2️⃣ **Local network route (your Wi-Fi LAN)**

```
10.156.40.0/24 dev wlp4s0 proto kernel scope link src 10.156.40.180 metric 600
```

### Meaning:

* **10.156.40.0/24** → the entire local subnet
    
* **dev wlp4s0** → reachable via Wi-Fi
    
* **scope link** → only reachable within your local network (LAN)
    
* **src 10.156.40.180** → your IP on this network
    

👉 This is how you reach devices locally (printers, other PCs, router).

* * *

# 3️⃣ **Docker network route**

```
172.17.0.0/16 dev docker0 proto kernel scope link src 172.17.0.1 linkdown
```

### Meaning:

* **172.17.0.0/16** → default Docker bridge network
    
* **dev docker0** → use the Docker virtual interface
    
* **src 172.17.0.1** → Docker gateway IP (host side)
    
* **linkdown** → currently no containers using it
    

👉 Used for communication between Docker containers and your host.
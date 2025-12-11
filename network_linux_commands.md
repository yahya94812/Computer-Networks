# The 3 most important Linux network commands

When working with Linux networking, there are many commands available. However, three commands stand out as the most essential for everyday tasks:
| Task                      | Use this command | Why                                             |
| ------------------------- | ---------------- | ----------------------------------------------- |
| Manage IPs, routes, links | **`ip`**         | Replaces 10+ old tools                          |
| Check sockets & ports     | **`ss`**         | Replaces `netstat`                              |
| Manage NetworkManager     | **`nmcli`**      | For desktops/server setups using NetworkManager |

# 🚀 **Ubuntu Linux Networking Commands — Explained (Intermediate)**

* * *

# **1. Interface & IP Management (`ip`)**

## **1.1 `ip a` — Show all IP addresses**

**What it does:**  
Lists all network interfaces and their IPv4/IPv6 addresses.

**Usage:**

```bash
ip a
```

**Example output meaning:**

* `eth0`: interface name
    
* `state UP`: interface is active
    
* `inet 192.168.1.20/24`: IPv4 address
    
* `inet6 fe80::...`: IPv6 link-local address
    

* * *

## **1.2 `ip link` — Show or modify interfaces**

**What it does:**  
Shows interface status and properties.

**Usage:**

```bash
ip link
```

**Example output meaning:**

* `UP` → interface is enabled
    
* `MTU 1500` → packet size limit
    
* `ether aa:bb:cc:dd:ee:ff` → MAC Address
    

* * *

## **1.3 Add an IP address**

```bash
sudo ip addr add 192.168.1.50/24 dev eth0
```

**Meaning:**  
Assigns IP `192.168.1.50` with subnet mask `/24` to `eth0`.

* * *

## **1.4 Remove an IP address**

```bash
sudo ip addr del 192.168.1.50/24 dev eth0
```

**Meaning:**  
Deletes the previously added IP.

* * *

## **1.5 Enable/Disable an interface**

Enable:

```bash
sudo ip link set eth0 up
```

Disable:

```bash
sudo ip link set eth0 down
```

**When used:**

* After changing IP
    
* Troubleshooting
    
* Resetting interface
    

* * *

# **2. Routing (`ip route`)**

## **2.1 Show routing table**

```bash
ip r
```

**Example output:**

```
default via 192.168.1.1 dev eth0
192.168.1.0/24 dev eth0 proto kernel scope link src 192.168.1.20
```

**Meaning:**

* `default via 192.168.1.1` → all traffic goes to this gateway
    
* `192.168.1.0/24` → direct local network
    

* * *

## **2.2 Add a route**

```bash
sudo ip route add 10.0.0.0/24 via 192.168.1.1 dev eth0
```

**Meaning:**  
Traffic to `10.0.0.0/24` goes through gateway `192.168.1.1`.

* * *

## **2.3 Delete a route**

```bash
sudo ip route del 10.0.0.0/24
```

* * *

# **3. DNS & Name Resolution**

## **3.1 Check DNS config (systemd-resolved)**

```bash
resolvectl status
```

**Shows:**

* Active DNS servers
    
* Per-interface DNS settings
    
* DNSSEC status
    

* * *

## **3.2 Query DNS with `dig`**

```bash
dig google.com
```

**Output meaning:**

* `ANSWER SECTION`: IP addresses
    
* `QUERY TIME`: DNS lookup latency
    

* * *

## **3.3 Query DNS with `nslookup`**

```bash
nslookup github.com
```

**Simple, human-readable DNS lookup.**

* * *

# **4. Port & Connection Monitoring (`ss`)**

## **4.1 Show listening ports**

```bash
ss -tulpn
```

Flags:

* `t` = TCP
    
* `u` = UDP
    
* `l` = listening
    
* `p` = show process
    
* `n` = show numeric ports
    

**Example output:**

```
tcp LISTEN 0 128 0.0.0.0:22 *:* users:(("sshd",pid=900))
```

**Meaning:**  
Port `22` is open and used by SSH.

* * *

## **4.2 Show active TCP connections**

```bash
ss -tan
```

Useful for checking client/server activity.

* * *

## **4.3 Show processes using sockets**
* At the operating system level, a socket(software) binds an application (process) to a port number and protocol on a given IP address.

* More precisely: The OS uses sockets to associate a process with a (IP address, port number, protocol) tuple, so incoming network packets can be delivered to the correct application.
```bash
ss -p
```

Shows which process owns a port.

* * *

# **5. NetworkManager (`nmcli`)**

## **5.1 List connections**

```bash
nmcli con show
```

Shows:

* Ethernet
    
* WiFi
    
* VLANs
    
* VPNs
    

* * *

## **5.2 List devices**

```bash
nmcli dev status
```

Shows:

* Device name
    
* Type
    
* State (connected/disconnected)
    

* * *

## **5.3 Bring connection up/down**

Bring up:

```bash
sudo nmcli con up id "Wired connection 1"
```

Bring down:

```bash
sudo nmcli con down id "Wired connection 1"
```

* * *

## **5.4 Set a static IP**

Step-by-step:

### Set IP:

```bash
nmcli con mod "Wired connection 1" ipv4.addresses "192.168.1.10/24"
```

### Set gateway:

```bash
nmcli con mod "Wired connection 1" ipv4.gateway "192.168.1.1"
```

### Set DNS:

```bash
nmcli con mod "Wired connection 1" ipv4.dns "8.8.8.8"
```

### Switch to manual config:

```bash
nmcli con mod "Wired connection 1" ipv4.method manual
```

### Apply:

```bash
nmcli con up "Wired connection 1"
```

* * *

# **6. Diagnostics & Troubleshooting**

## **6.1 Ping**

```bash
ping -c 4 8.8.8.8
```

**Meaning:**

* `-c 4` → send 4 packets
    

* * *

## **6.2 Traceroute**

```bash
traceroute google.com
```

Shows the path your packets take across the internet.

* * *

## **6.3 Check ARP cache**

```bash
ip neigh
```

Shows:

* IP → MAC mappings
    
* Reachability state (`REACHABLE`, `STALE`, `FAILED`)
    

* * *

## **6.4 Capture packets with tcpdump**

```bash
sudo tcpdump -i eth0
```

Advanced example:

```bash
sudo tcpdump -i eth0 port 80
```

* * *   

# **7. Live Traffic Monitoring**

## **7.1 `iftop` — interface bandwidth**

```bash
sudo iftop -i eth0
```

Shows live traffic: who is talking to whom and how much.

* * *

## **7.2 `nethogs` — per-process usage**

```bash
sudo nethogs
```

Shows:

* `firefox` using bandwidth
    
* `apt` downloads
    
* etc.
    

* * *

## **7.3 `bmon` — graphical bandwidth monitor**

```bash
bmon
```

* * *

# **8. Firewall (`ufw`)**

## **8.1 Check firewall status**

```bash
sudo ufw status verbose
```

* * *

## **8.2 Allow a port**

```bash
sudo ufw allow 22/tcp
```

Opens SSH.

* * *

## **8.3 Deny a port**

```bash
sudo ufw deny 80/tcp
```

* * *

## **8.4 Enable/Disable firewall**

Enable:

```bash
sudo ufw enable
```

Disable:

```bash
sudo ufw disable
```

* * *

# **9. System Services (`systemctl`)**

## **9.1 Check service status**

```bash
systemctl status networking
```

```bash
systemctl status NetworkManager
```

* * *

## **9.2 Restart NetworkManager**

```bash
sudo systemctl restart NetworkManager
```

* * *
# Computer Networking Fundamentals

## TCP(Transmission Control Protocol)
* It consists of four layers: Network Interface, Internet, Transport, and Application.)
## 1. Localhost & Loopback Address

**Localhost** is a special hostname that refers to your own computer, making requests to itself.

### IP Addresses
- **IPv4**: `127.0.0.1`
- **IPv6**: `::1` (:: represents all zeros except the last bit, which is 1)
- Also called **loopback address** (interface: `lo`)

### CIDR Notation: 127.0.0.1/8
- `/8` means the first 8 bits are the network portion
- **Subnet mask**: `255.0.0.0`
- **Range**: `127.0.0.0` – `127.255.255.255` (entire loopback block)
- The `/` indicates how many bits are fixed for the network

### Access Format
```
http://localhost
http://127.0.0.1
https://localhost:3000
```

---

## 2. Host
A **host** is any device on a network that has an address and can send/receive data.

---

## 3. Ports

### Definition
A **port** is a numbered channel (like a "door") on a computer that lets different applications communicate over the network.

### Key Facts
- Each computer has **65,535 ports**
- Different services use different port numbers to avoid conflicts
- Ports enable **processes** in the OS to communicate

### Common Port Numbers
| Port | Service |
|------|---------|
| 80 | HTTP (websites) |
| 443 | HTTPS (secure websites) |
| 3306 | MySQL database |
| 3000 / 5000 / 8000 | Development servers |

### Port Communication Flow
When accessing a website like `https://example.com`:

**Your Computer** → uses random high port (e.g., `52144`)  
**↓** (connects to)  
**Server** → listens on port `443` (default for HTTPS)

- Your OS manages outgoing ports automatically
- The browser (application layer) initiates the connection
- This enables two-way communication

### Accessing Local Server
```
http://localhost:3000
```
- `localhost` → "Go to my own computer"
- `:3000` → "Use port 3000"

---

## 4. Network Configuration Commands

### View Listening Ports
```bash
ss -tuln
```
- `t` = TCP
- `u` = UDP
- `l` = listening
- `n` = numeric ports

### View Network Interfaces & IPs
```bash
ip -br a                    # Brief address info
ip a                        # Full address info
nmcli device show           # Formatted interface details
```

### Get Your Public IP
```bash
curl ifconfig.me
```
Or visit `ifconfig.me` in a browser

---

## 5. Accessing Local Applications on LAN

If you're hosting an application on Linux (e.g., `http://127.0.0.1:5500/index.html`):

### To Access from Other Devices on Your Network:
1. Use your machine's assigned local IP instead of `127.0.0.1`
2. **Disable firewall**:
```bash
   sudo ufw disable
```
3. Access from other devices: `http://<your-local-ip>:5500/index.html`

---

## Summary
- **Localhost** = your own computer (`127.0.0.1` or `::1`)
- **Port** = numbered channel for application communication
- **Host** = any network device with an address
- **Processes** communicate through ports using the OS networking stack
- Use `ss`, `ip`, or `nmcli` to inspect network configuration
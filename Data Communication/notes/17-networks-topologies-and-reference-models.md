# 17. Computer Networks: Types, Topologies, Components & Reference Models

> **Syllabus:** End-term. Background for *local area networks* and *hubs, bridges and switches*.
> **Source:** `topology.pdf` (83 pages): network types pp. 1–9, topologies pp. 10–23, components pp. 24–35, OSI and TCP/IP pp. 36–66, identifiers pp. 71–83.

---

## 🎯 In one line

Networks are classified by **size** (**PAN < LAN < MAN < WAN**) and by **topology** (**bus, ring, star, tree, mesh, hybrid**). They are built from **hardware** (servers, clients, media, connecting devices) and **software** (NOS, protocols), and described by **layered models**: the **7-layer OSI** model and the **TCP/IP** model.

---

## 1. Types of network by size (pp. 1–9) ⭐⭐⭐

| Type | Coverage | Key points |
|---|---|---|
| **PAN** (Personal Area Network) | Within one person's reach, **~10 m (30 ft)** | Connects personal devices: laptop, mobile, media player, PlayStation. The idea came from **Thomas Zimmerman** |
| **LAN** (Local Area Network) | A **building or office** | Connects PCs through **twisted pair, coaxial cable**, etc. **Low cost** (hubs, network adapters, Ethernet cables), **very fast** data transfer, **higher security** |
| **MAN** (Metropolitan Area Network) | A **city** | **Interconnects different LANs** into a larger network, often through **telephone exchange lines**. Protocols: **RS-232, Frame Relay, ATM, ISDN, OC-3, ADSL**. Uses: banks in a city, **airline reservation**, a college across a city, the **military** |
| **WAN** (Wide Area Network) | **States or countries** | Spans large areas via **telephone lines, fibre or satellite links**. **The Internet is the biggest WAN**. Examples: **4G mobile broadband**, **last-mile fibre** to homes, a **bank's private network** of leased lines (44 offices) |

**WAN advantages:** large geographical coverage · **centralised data** (no need to buy e-mail, file or backup servers per site) · **updated files** within seconds (live servers) · fast message exchange · **sharing** of software and resources · **global business** · **high bandwidth** with leased lines.

**WAN disadvantages:** **security issues** (many technologies combined) · needs a **firewall and antivirus** · **high setup cost** (routers, switches) · **troubleshooting** is hard over a large area.

```
  PAN (~10 m)  ⊂  LAN (building)  ⊂  MAN (city)  ⊂  WAN (country / world)
```

---

## 2. Network topology (pp. 10–23) ⭐⭐⭐

**Topology** is the structure of how network components are interconnected.
- **Physical topology:** the geometric arrangement of the nodes.
- **Logical topology:** how data actually flows.

### 2.1 Bus topology

All stations connect to a **single cable, the backbone**, either directly or through **drop cables**. A message put on the bus is **received by every station**, whether addressed to it or not; the backbone is a "**single lane**" broadcast medium.
- Used in **IEEE 802.3 (Ethernet)** and **802.4** networks. The simplest configuration.
- The most common access method is **CSMA**:

| Method | How it works |
|---|---|
| **CSMA/CD** (collision **detection**) | Detect a collision and **stop transmitting**: **"recovery after the collision"** (wired Ethernet) |
| **CSMA/CA** (collision **avoidance**) | **Check whether the medium is busy** and wait until it is idle, which **avoids** collisions. Does **not** rely on recovery after collision (wireless LAN) |

| Advantages | Disadvantages |
|---|---|
| **Low-cost cable** (no hub needed) | **Extensive cabling** |
| Moderate speeds (**up to 10 Mbps** on coax or twisted pair) | **Difficult troubleshooting**: a cable fault disrupts **all** nodes |
| **Familiar technology** | **Signal interference** (collisions) |
| **Limited failure**: a node failure doesn't affect others | **Reconfiguration** difficult; adding devices slows the network |
| | **Attenuation**, so **repeaters** are needed |

### 2.2 Ring topology

Like a bus with the **ends connected**. Each node **retransmits** the message it receives to the next node. Data flows in **one direction (unidirectional, clockwise)** in an **endless loop**, with **no terminated ends**.
- The most common access method is **token passing**. A **token** is a frame that circulates. The sender **modifies the token**, adding the address and data, and it is passed node to node until the destination matches. The destination then sends an **acknowledgement** to the sender.

| Advantages | Disadvantages |
|---|---|
| **Network management**: faulty devices can be removed without bringing the network down | **Difficult troubleshooting** |
| Many monitoring tools are available | **Failure of one station can fail the whole network** |
| **Low cost** (twisted pair) | **Reconfiguration** difficult |
| **Reliable**: not dependent on one host | **Delay ∝ number of nodes** |

### 2.3 Star topology

Every node connects to a **central hub, switch or computer**. The central computer is the **server** and the attached devices are **clients**. Cables are **coaxial or RJ-45**. It is **the most popular topology**.

| Advantages | Disadvantages |
|---|---|
| **Efficient troubleshooting** (check the centre, not kilometres of cable) | **Central point of failure**: if the hub or switch fails, nobody can communicate |
| **Complex network control** is easy | **Cable routing** can be difficult |
| **Limited failure**: one cable fault affects only that node | |
| **Easily expandable** (open hub ports) | |
| **High speed**: ~100 Mbps (**100Base-T** Ethernet) | |

### 2.4 Tree topology

**Combines bus and star.** Computers are connected **hierarchically**: a **root** node with descendants. There is **exactly one path** between any two nodes, forming a **parent–child hierarchy**.

| Advantages | Disadvantages |
|---|---|
| Supports **broadband** transmission over long distances | **Difficult troubleshooting** |
| **Easily expandable** and **manageable** (segments are star networks) | **High cost** (broadband devices) |
| Easy **error detection and correction** | **Failure of the main bus** damages the whole network |
| **Limited failure**; point-to-point wiring for segments | **Reconfiguration** difficult |

### 2.5 Mesh topology ⭐⭐⭐

Computers are interconnected through **redundant connections**: **multiple paths** between any two, and **no central** switch or hub. **The Internet** is an example. It is used for **WANs** where failures are critical, and for **wireless** networks.

$$\boxed{\text{Number of cables (full mesh)} = \frac{n(n-1)}{2}} \qquad \text{(and each device needs } n-1 \text{ ports)}$$

*Example:* 6 nodes need $6 \times 5 / 2 = $ **15** cables, with **5** ports per device.

| Type | Meaning |
|---|---|
| **Full mesh** | Every computer connects to **every other** |
| **Partial mesh** | Only computers that **communicate frequently** are connected |

| Advantages | Disadvantages |
|---|---|
| **Reliable**: a link failure doesn't stop communication | **Cost**: many links and devices (routers, media) |
| **Fast communication** | **Management** is hard; link failures may go undetected |
| **Easy reconfiguration** | **Efficiency** drops because of so many redundant links |

### 2.6 Hybrid topology

A **combination of two or more different topologies**. Joining **similar** topologies does **not** make a hybrid. *Example:* a **ring** in one ICICI branch and a **bus** in another, connected together.

| Advantages | Disadvantages |
|---|---|
| **Reliable** (faults are isolated), **scalable**, **flexible**, **effective** (maximise strengths) | **Complex design**, **costly hubs**, **costly infrastructure** |

### Topologies compared

| | Bus | Ring | Star | Tree | Mesh |
|---|---|---|---|---|---|
| Central device | No | No | **Yes** | Yes (root) | No |
| Single point of failure | Backbone | Any node (single ring) | **Hub** | Root / main bus | **None** |
| Cabling | Least | Low | Medium | Medium | **Most**: $n(n-1)/2$ |
| Access method | **CSMA/CD** | **Token passing** | Hub or switch | – | – |
| Troubleshooting | Hard | Hard | **Easy** | Hard | Hard |

---

## 3. Network components (pp. 24–35) ⭐⭐

| Hardware | Role |
|---|---|
| **Servers** | High-configuration computers that **manage network resources**. The NOS is installed here. File, database and print servers |
| **Clients** | Computers that **request and receive** services from servers |
| **Peers** | Computers that both **provide and receive** services (a workgroup) |
| **Transmission media** | Guided (coax, fibre) or unguided (microwave, infrared). See [Ch. 15](15-transmission-media.md) |
| **Network cables** | Commonly **Cat 5 with an RJ-45 connector** |
| **NIC** (network interface card) | Connects a computer to the network. **Internal or external**. Carries the **MAC address** |
| **Modem** (modulator–demodulator) | Connects a computer to the Internet over a **telephone line**, converting **digital ↔ analog**. *A modem connects to the Internet; a router connects devices (e.g. to Wi-Fi)* |
| **Connecting devices** | **Repeaters, hubs, bridges, switches, routers, gateways**. See [Ch. 19](19-connecting-devices-hubs-bridges-switches.md) |

| Software | Role |
|---|---|
| **Network operating system (NOS)** | Installed on the server; lets workstations share files, databases, applications and printers |
| **Protocol suite** | A set of related protocols (rules for communication). The two popular ones are the **OSI** model and **TCP/IP** |

---

## 4. Layered architecture (pp. 36–38) ⭐⭐

Early communication software was one huge unstructured program that was hard to test and modify, so **ISO** developed a **layered approach**. Each layer does a particular task and **provides services to the layer above**, hiding how they are implemented.

| Element | Meaning |
|---|---|
| **Service** | Actions a layer provides to the **higher** layer |
| **Protocol** | Rules a layer uses to exchange information with its **peer** (layer $n$ on the other machine). This is the **layer-$n$ protocol** |
| **Interface** | How a message passes **between adjacent layers** |

No data goes directly from layer $n$ on one machine to layer $n$ on another. Each layer passes data **down** to the layer below, and below layer 1 is the **physical medium**. **A set of layers and protocols = a network architecture.**

**Why layering?**
- **Divide and conquer** (it reduces complexity).
- **Modularity** (layer independence).
- **Easy to modify** (one layer's implementation can be replaced).
- **Easy to test** (each layer separately).

---

## 5. The OSI reference model (pp. 39–57) ⭐⭐⭐

**OSI (Open System Interconnection)**, developed by **ISO in 1984**, describes how information moves from an application on one computer through a physical medium to an application on another. It has **seven layers**, each **self-contained**. **It is a model, not a protocol.**

**Mnemonic, top to bottom:** **A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing.

| # | Layer | Data unit | Main functions | Devices / protocols |
|---|---|---|---|---|
| 7 | **Application** | Data | A **window** for users to network services: **file transfer (FTAM)**, **mail**, **directory services** | HTTP, FTP, SMTP, DNS |
| 6 | **Presentation** (the **syntax layer**) | Data | **Translation** (sender-dependent ↔ common format), **encryption**, **compression** | |
| 5 | **Session** | Data | **Dialog control** (half- or full-duplex), **synchronisation**: **checkpoints**, e.g. every 50 pages of a 400-page file, so recovery restarts from the last checkpoint | |
| 4 | **Transport** (end-to-end) | **Segment** | **Service-point (port) addressing**, **segmentation and reassembly** (sequence numbers), **connection control**, **end-to-end** flow and error control | **TCP**, **UDP** |
| 3 | **Network** | **Packet** | **Logical addressing**, **routing** (best path), **internetworking**, **packetising** | **Routers**; IP, IPv6 |
| 2 | **Data link** | **Frame** | **Framing** (header + trailer/FCS), **physical (MAC) addressing**, **flow control**, **error control (CRC)**, **access control**. Sub-layers **LLC** and **MAC** | **Switches, bridges** |
| 1 | **Physical** | **Bit** | Transmits **individual bits**: **line configuration**, **transmission mode** (simplex, half-duplex, full-duplex), **topology**, **signals** (encoding bits into electrical or optical signals) | **Hubs, repeaters**, cables |

> ⚠️ The handout says the session layer is "layer 3" (it is **layer 5**) and that "the data link layer is responsible for routing" on the network-layer page (**routing is the network layer's job**). These are typos.

- **Upper layers** (application, presentation, session) deal with **application issues** and are implemented in **software**.
- **Lower layers** deal with **data transport**. Data link and physical are implemented in **hardware and software**.

**Data-link sub-layers:**
- **LLC (Logical Link Control):** hands packets to the receiver's network layer, identifies the network-layer protocol from the header, and provides **flow control**.
- **MAC (Media Access Control):** the link between LLC and the physical layer; transfers packets over the medium.

**Encapsulation** means each layer adds its own **header** (the data link layer adds a **trailer** too) as data moves down.

---

## 6. The TCP/IP model (pp. 58–65) ⭐⭐⭐

Developed **before** OSI and **protocol-oriented**. It is hierarchical: each upper-layer protocol is supported by one or more lower-level protocols. *(The handout describes five layers. The four-layer form merges physical and data link into **network access**.)*

| TCP/IP layer | ≈ OSI layers | Protocols and functions |
|---|---|---|
| **Application** | Application + presentation + session | **HTTP** (web), **SNMP** (network management), **SMTP** (e-mail), **DNS** (name → IP), **TELNET** (remote terminal), **FTP** (file transfer) |
| **Transport** | Transport | **TCP**: reliable, **connection-oriented**, virtual circuit, segments with sequence numbers, acknowledgements and retransmission. **UDP**: **connectionless, unreliable**, no acknowledgements; fields are **source port, destination port, total length and a 16-bit checksum** |
| **Internet** | Network | **IP**: logical **IP addressing**, host-to-host path, encapsulation into **IP datagrams**, **fragmentation** (when a datagram exceeds the **MTU**), **routing** (direct vs indirect delivery). **ARP**: IP → **physical (MAC)** address, using a broadcast **ARP request** and a unicast **ARP reply**. **RARP**: MAC → IP (now replaced by **DHCP**). **ICMP**: **reports** datagram problems back to the source; it does **not correct** them |
| **Network access** (link) | Data link + physical | Puts IP datagrams into **frames**, maps IP to physical addresses. Ethernet, token ring, FDDI, X.25, frame relay |

### OSI vs TCP/IP

| Similarities | Differences: OSI | Differences: TCP/IP |
|---|---|---|
| Both are **layered** | **Generic**, function-based **reference model** | **Protocol-oriented standard**, more **practical** (the Internet runs on it) |
| Layers correspond (network ≈ internet, transport ≈ transport) | **Clearly distinguishes services, interfaces and protocols** | **No clear distinction** |
| Protocols defined per layer | Model **first**, then protocols | Protocols **first**, then the model |
| Data split into packets that may take individual routes | **7 layers** | **4 layers** |

---

## 7. Unique identifiers in a network (pp. 71–83) ⭐⭐

| Identifier | Facts | Command |
|---|---|---|
| **Host name** | A unique device name | `hostname` |
| **IP address** (logical address) | Network address of the system. Assigned by **IANA**. **IPv4 = 32 bits** ($2^{32}$ addresses); **IPv6 = 128 bits** | `ipconfig` |
| **MAC address** (physical address) | The unique ID of the **NIC**, assigned **at manufacture**. **48 bits = 6 bytes = 12 hex digits (nibbles)** | `ipconfig /all` |
| **Port** | A **logical channel** to an application, a **16-bit** number (**65,536** ports, 0–65535): **well-known 0–1023**, **registered 1024–49151**, **ephemeral 49152–65535** | `netstat -a` |
| **Socket** | **IP address + port number** | |
| **DNS** | Translates **URLs** (www.google.com) into **IP addresses** | `nslookup` |
| **ARP / RARP** | IP → MAC / MAC → IP | |

**Open system:** connected to the network and ready to communicate. **Closed system:** not connected.

---

## 8. Common exam questions

1. **Differentiate PAN, LAN, MAN and WAN. Advantages and disadvantages of WAN.** See §1.
2. **Explain bus, ring, star, tree, mesh and hybrid topologies with advantages and disadvantages.** See §2.
3. **How many cables does a full mesh of $n$ nodes need?** $n(n-1)/2$ (§2.5).
4. **Differentiate CSMA/CD and CSMA/CA. What is token passing?** See §2.
5. **What are the hardware and software components of a network?** See §3.
6. **Why layered architecture? Define service, protocol and interface.** See §4.
7. **Explain the seven OSI layers and their functions.** See §5.
8. **Explain the TCP/IP model; ARP, RARP, ICMP; TCP vs UDP.** See §6.
9. **Compare OSI and TCP/IP.** See §6.
10. **What are IP address, MAC address, port and socket?** See §7.

---

## ⚡ Quick revision

- **PAN (10 m) < LAN (building) < MAN (city) < WAN (country, e.g. the Internet).**
- **Bus** (backbone, CSMA/CD, one cable fault kills all) · **Ring** (unidirectional, **token passing**) · **Star** (hub, most popular, single point of failure) · **Tree** (bus + star, hierarchy) · **Mesh** ($n(n-1)/2$ links, most reliable, costliest) · **Hybrid** (different topologies combined).
- **CSMA/CD** = detect then recover (wired). **CSMA/CA** = sense then avoid (wireless).
- **OSI (ISO 1984), 7 layers:** Physical (bits) · Data link (frames, MAC, CRC; LLC + MAC) · Network (packets, routing, IP) · Transport (segments, ports, TCP/UDP) · Session (dialog, checkpoints) · Presentation (translate, encrypt, compress) · Application.
- **TCP/IP:** application · transport · internet (IP, ARP, RARP, ICMP) · network access. Protocols came first; more practical.
- **IPv4 32 bits, IPv6 128 bits, MAC 48 bits, port 16 bits** (0–1023 well-known). **Socket = IP + port.**

---

**Previous:** [← 16. Switching](16-switching.md) · **Next:** [18. LANs: Ethernet, Fast & Gigabit Ethernet, WLAN →](18-lan-ethernet-and-wlan.md)

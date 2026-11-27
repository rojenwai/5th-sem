# 19. Connecting Devices: Repeaters, Hubs, Bridges, Switches, Routers & Gateways

> **Syllabus:** End-term. *Hubs, bridges, and switches*
> **Source:** `topology.pdf` pp. 29–34 (connecting devices), `Switching.pdf` pp. 1–2 and 14 (switches, STP). The learning-bridge and spanning-tree walkthroughs and the collision/broadcast-domain table (§4–§6) are standard additions marked 🆕.

---

## 🎯 In one line

Connecting devices work at different OSI layers. **Repeaters and hubs (layer 1)** just regenerate and copy bits to every port. **Bridges and switches (layer 2)** **filter and forward frames by MAC address**, splitting collision domains. **Routers (layer 3)** route **packets by IP address** between networks. **Gateways** translate between **different protocols**.

---

## 1. Connecting devices by layer ⭐⭐⭐

Connecting devices act as **middleware** between networks or computers, binding the network media together (`topology.pdf` p. 29).

```
 OSI layer           Device                      Forwards on
 ───────────────────────────────────────────────────────────────
 7–4  Application…   GATEWAY (protocol converter) whole message / protocol
 3    Network        ROUTER                      IP address (logical)
 2    Data link      BRIDGE, SWITCH              MAC address (physical)
 1    Physical       REPEATER, HUB               nothing: just bits
```

---

## 2. Repeater (p. 30) ⭐⭐

- **Receives a signal and regenerates it** before retransmitting, so the signal can **travel longer distances** (it counteracts **attenuation**, see [Ch. 15](15-transmission-media.md)).
- **2 ports.** It works at the **physical layer** and has no intelligence: no addresses, no filtering.
- A repeater **regenerates** the original bit pattern. An amplifier boosts the signal **and its noise**.
- It **joins segments of the same LAN**, extending its length; it does not connect different LANs.

---

## 3. Hub (p. 30) ⭐⭐⭐

- **A hub is a multiport repeater**: it has several input/output ports, and **input at any port is available at every other port**.
- It works at the **physical layer** and **broadcasts** every signal to all ports.
- The physical star of a **10Base-T** network (see [Ch. 18](18-lan-ethernet-and-wlan.md)) is wired to a hub, but it still behaves logically as a **bus**. **All ports share one collision domain** and **one bandwidth**.

| Passive hub | Active hub |
|---|---|
| Just a connector; no signal regeneration | **Regenerates** the signal (a multiport repeater). The usual kind |

---

## 4. Bridge (p. 31) ⭐⭐⭐

- **Connects two separate Ethernet network segments** and **forwards packets from the source network to the destination network**.
- **Single input and single output port: a 2-port device** (class handout).
- Works at the **data-link layer (layer 2)**. It reads the **destination MAC address** and **filters**: a frame is forwarded **only if** the destination is on the other segment.
- Each side of a bridge is a **separate collision domain**.

### 🆕 How a transparent (learning) bridge works ⭐⭐

A bridge builds its **forwarding table** automatically by **learning source addresses**:

| Step | Rule |
|---|---|
| 1. **Learn** | When a frame arrives on port P from source S, record **"S is on port P"** |
| 2. **Filter** | If the destination is on the **same** port it came from, **drop** it (no need to cross) |
| 3. **Forward** | If the destination is known on **another** port, send it **only there** |
| 4. **Flood** | If the destination is **unknown** (or broadcast), send it to **all other** ports |

**Example:** stations A and B are on segment 1 (port 1), and C and D are on segment 2 (port 2). The table starts empty.

| Frame | Learned | Action | Table after |
|---|---|---|---|
| A → D | A on port 1 | D unknown → **flood** to port 2 | A:1 |
| D → A | D on port 2 | A known on port 1 → **forward** to port 1 | A:1, D:2 |
| B → A | B on port 1 | A is on port 1, the **same** port → **filter (drop)** | A:1, D:2, B:1 |
| C → D | C on port 2 | D is on port 2, the same port → **filter** | A:1, D:2, B:1, C:2 |

### 🆕 Loops and the Spanning Tree Protocol (`Switching.pdf` p. 14) ⭐⭐

Redundant bridges give **fault tolerance**, but they create **loops**. A broadcast or unknown-destination frame is flooded around the loop **forever** (a **broadcast storm**), and forwarding tables keep changing. *"Loops are deadly to a network."*

**STP (IEEE 802.1D)** runs on **bridges and switches** and builds a **loop-free spanning tree**:
1. Elect the **root bridge**: the one with the **smallest bridge ID**.
2. Each other bridge picks its **root port**: the port with the **least-cost path** to the root.
3. Each LAN segment picks a **designated bridge/port**: the one with the least-cost path to the root.
4. All other ports are **blocked**. They stay physically connected and are **re-activated** if an active link fails.

---

## 5. Switch (p. 30; `Switching.pdf` pp. 1–2) ⭐⭐⭐

- **A switch is a multiport bridge.**
- It receives data on a port, uses the **destination MAC address** to find the destination device, and forwards the data **only to that port**, **rather than broadcasting it as a hub does**.
- It operates at **layer 2**, in **full-duplex** mode, so **collisions are minimal**. **Each port is its own collision domain.**
- It **does not broadcast** ordinary (unicast) frames.

| Advantages (`Switching.pdf`) | Disadvantages |
|---|---|
| **Increases network bandwidth** (each port gets full bandwidth) | **More expensive than a bridge** |
| **Reduces PC workload** (only the addressee receives) | Hard to diagnose **connectivity issues** |
| Better **performance** (less traffic) | Needs proper design to handle **multicast** |
| **Fewer collisions** (a collision domain per connection) | |

*(Standard: **cut-through** switches start forwarding after reading the destination address, which is faster. **Store-and-forward** switches check the whole frame's CRC first, which is more reliable. **Layer-3 switches** add routing.)*

---

## 6. Hub vs bridge vs switch ⭐⭐⭐

| | **Hub** | **Bridge** | **Switch** |
|---|---|---|---|
| OSI layer | 1 (physical) | 2 (data link) | 2 (data link) |
| Ports | Many | **2** | Many (**multiport bridge**) |
| Uses addresses? | **No** | **MAC** | **MAC** |
| Forwarding | **Broadcasts** to all ports | **Filters**: forwards only across segments when needed | Sends **only to the destination port** |
| Collision domains | **1** (all ports share it) | **2** (one per side) | **One per port** |
| Broadcast domains | 1 | 1 | 1 (unless VLANs are used) |
| Duplex | Half | Half/full | **Full** |
| Bandwidth | **Shared** | Shared per segment | **Dedicated** per port |
| Intelligence / cost | Lowest | Medium | Higher |

### 🆕 Collision and broadcast domains

```
 HUB:     [PC1][PC2][PC3][PC4]  ── all in ONE collision domain, ONE broadcast domain
 SWITCH:  [PC1]|[PC2]|[PC3]|[PC4] ── 4 collision domains, still ONE broadcast domain
 ROUTER:  LAN-A ║ LAN-B       ── separates BROADCAST domains too
```

*Example:* 3 hubs, each with 4 PCs, plug into 3 ports of a switch, and a 4th switch port connects to a router. The result is **4 collision domains** (one per hub segment, plus the switch–router link) and **1 broadcast domain** on the LAN side (only the router separates broadcast domains).

---

## 7. Router (p. 34) ⭐⭐

- Transfers **data packets between different computer networks**, e.g. connects a PC or organisation's **LAN to a broadband Internet connection**.
- Has **RJ-45 ports** for wired devices. Routers normally **connect LANs and WANs**.
- Works at **layer 3 (network)**. It uses **IP (logical) addresses** and **routing tables** to choose the best path, and **separates broadcast domains**.

| Switch | Router |
|---|---|
| Layer 2, MAC addresses | Layer 3, IP addresses |
| Connects devices **within** a LAN | Connects **different networks** (LAN ↔ WAN) |
| One broadcast domain | Separates broadcast domains |

---

## 8. Gateway (p. 31) ⭐⭐

- Connects **entirely different networks that use different protocols**. It is the **entry and exit point** of a network and **controls access** to other networks.
- It works as a **messenger**: it takes data from one system, **interprets** it, and transfers it to another. It is also called a **protocol converter**.
- It can operate at **any network layer** (usually all seven), and is **more complex than a switch or router**.

---

## 9. NIC and modem (pp. 32–33)

| Device | Role |
|---|---|
| **NIC** (network interface card) | Connects a computer to the network. **Internal or external**. Holds the **48-bit MAC address** |
| **Modem** | **Mod**ulator/**dem**odulator: connects to the Internet over the **telephone line**, converting **digital → analog** (modulation) and back. Installed in a PCI slot. *A modem connects to the Internet; a router connects devices (e.g. via Wi-Fi)* |

---

## 10. Common exam questions

1. **List the connecting devices and the OSI layer each works at.** See §1.
2. **What is a repeater? How does it differ from an amplifier?** See §2.
3. **What is a hub? Why is a hub-based star still a logical bus?** See §3.
4. **Explain a bridge. How does a learning bridge build its table?** See §4.
5. **What problem do loops cause? Explain the Spanning Tree Protocol.** See §4.
6. **Explain a switch. Why is it called a multiport bridge? Advantages and disadvantages.** See §5.
7. **Differentiate hub, bridge and switch** (a classic table question). See §6.
8. **Count the collision and broadcast domains in the given network.** See §6.
9. **Differentiate a switch and a router; what is a gateway?** See §7–§8.

---

## ⚡ Quick revision

- **Layer 1:** **repeater** (regenerates, 2 ports) and **hub** (**multiport repeater**, broadcasts to all, 1 collision domain).
- **Layer 2:** **bridge** (2 ports, **filters by MAC**, **learns** source addresses: learn → filter → forward → flood) and **switch** (**multiport bridge**, sends only to the destination port, **a collision domain per port**, full duplex).
- **Layer 3:** **router** (IP addresses, connects LAN ↔ WAN, **separates broadcast domains**).
- **All layers:** **gateway** (protocol converter between different networks).
- **STP (802.1D):** root bridge (lowest ID) → root ports → designated ports → **block the rest**, which removes loops and broadcast storms.
- Hub = shared bandwidth, broadcast. Switch = dedicated bandwidth, unicast forwarding.

---

**Previous:** [← 18. LANs: Ethernet & WLAN](18-lan-ethernet-and-wlan.md) · **Back to:** [Data Communication index](../README.md)

# Day 3 – TCP/IP Model (CCNA 200-301)

---

## 1. A Bit of History

- Early work on computer networks that evolved into today’s Internet began in the **1960s**.
- The **US Department of Defense** funded **ARPANET**, which came online in **1969**, connecting universities and research labs.
- ARPANET initially used **NCP (Network Control Program)**.

### Birth of TCP/IP
- **Vint Cerf** and **Bob Kahn** (DARPA) began developing **TCP** in **1974**.
- TCP was later split into two protocols still used today:
  - **Transmission Control Protocol (TCP)**
  - **Internet Protocol (IP)**
- Together, they form the **TCP/IP protocol suite**.
- ARPANET fully switched to TCP/IP on **January 1, 1983**.

### Why TCP/IP Won
- Open standards (not vendor-proprietary)
- Any vendor could implement them
- Could run over many different types of networks

---

## 2. Who Defines Networking Standards?

### IEEE (Institute of Electrical and Electronics Engineers)
- Develops many **LAN technologies**:
  - **Ethernet (802.3)**
  - **Wi‑Fi (802.11)**

### IETF (Internet Engineering Task Force)
- Open community defining **Internet protocols**:
  - TCP, IP, UDP, HTTP, DNS, etc.
- Publishes standards as **RFCs (Requests for Comments)**

---

## 3. Why Layered Models?

- Networks perform many different jobs:
  - Physical transmission
  - Local delivery
  - Routing between networks
  - End‑to‑end communication
  - Applications

### Layered Model Concept
- Related tasks are grouped into **layers**
- Each layer:
  - Has a **specific role**
  - Uses services of the layer below
  - Provides services to the layer above

> A model is a **description**, not a law. Different sources may use 4‑layer, 5‑layer, or 7‑layer models.

---

## 4. TCP/IP 5‑Layer Model Overview

![TCP/IP Model](./images/TCP%20IP%20Model%20diagram.png)

| Layer | Name | Purpose |
|-----|-----|--------|
| 5 | Application | Network services for applications |
| 4 | Transport | Process‑to‑process communication |
| 3 | Internet | Host‑to‑host delivery across networks |
| 2 | Local Network | Hop‑to‑hop delivery (MAC addresses) |
| 1 | Physical | Bits on the wire |

---

## 5. Layer 1 – Physical Layer

![Physical Layer Context](./images/TCP%20IP%20Model%20diagram.png)

- Sends and receives **bits** as electrical, optical, or radio signals
- Defines:
  - Cables and connectors
  - Signal levels
  - Link speeds

### Examples
- Copper UTP cables
- Fiber‑optic cables
- Wi‑Fi radios and antennas
- Network Interface Cards (NICs)

> Network engineers usually don’t need deep signal‑level knowledge.

---

## 6. Layer 2 – Local Network Layer

- Provides **hop‑to‑hop delivery** within a local network
- A **hop** is movement from one host/router to the next
- **Switches don’t count as hops** (they extend the LAN)

### Addressing
- Uses **MAC (Media Access Control) addresses**
- Example path:
  - PC → R1 (MAC of R1)
  - R1 → R2 (MAC of R2)
  - R2 → Server (MAC of server)

### Protocols
- Ethernet (IEEE 802.3)
- Wi‑Fi (IEEE 802.11)

---

## 7. Layer 3 – Internet Layer

- Provides **end‑to‑end delivery across multiple networks**
- Uses **IP addresses** to identify hosts
- Routers operate mainly at this layer

### Example
- PC sends data to **SRV1’s IP address (10.1.1.1)**
- Routers forward packets based on destination IP

### Protocols
- IP (IPv4, IPv6)
- ICMP

---

## 8. Layer 4 – Transport Layer

- Provides **process‑to‑process communication**
- Uses **port numbers**

### Key Points
- Runs mainly on **end hosts**, not routers
- Identifies which application should receive the data

### Protocols
- **TCP** – reliable, ordered, congestion‑controlled
- **UDP** – simple, fast, no reliability

### Example
- Web traffic → **Port 80**
- FTP → **Port 21**

---

## 9. Layer 5 – Application Layer

- Where **applications meet the network**
- Defines how data is formatted and interpreted

### Examples
- HTTP / HTTPS (web browsing)
- FTP / TFTP (file transfer)
- SMTP, POP3, IMAP (email)

> Network devices don’t care about application data — only end hosts do.

---

## 10. Encapsulation and Decapsulation

![Encapsulation Diagram](./images/Encapsulation%20diagram.png)

### Encapsulation (Sender)
1. Application creates **data**
2. Transport layer adds **L4 header**
3. Internet layer adds **L3 header**
4. Local Network layer adds **L2 header + trailer**
5. Physical layer sends bits

### Decapsulation (Receiver)
- Reverse process: headers removed layer by layer

---

## 11. Protocol Data Units (PDUs)

### Segment / Datagram (Layer 4)
![Segment or Datagram](./images/Segment%20or%20Datagram%20diagram.png)

- TCP → Segment
- UDP → Datagram
- Payload = application data

### Packet (Layer 3)
![Packet](./images/Packet%20diagram.png)

- Payload = segment or datagram

### Frame (Layer 2)
![Frame](./images/Frame%20diagram.png)

- Payload = packet
- Actually sent over the wire

---

## 12. Adjacent‑Layer Interaction

- Each layer:
  - Is **serviced by the layer below**
  - **Provides service to the layer above**

### Examples
- L4 → L5: Delivers data to correct application (ports)
- L3 → L4: Delivers data to correct host (IP)
- L2 → L3: Delivers data to next hop (MAC)
- L1 → L2: Sends signals

---

## 13. Same‑Layer Interaction

- Each layer communicates logically with the **same layer on the destination host**

### Addressing Summary
| Layer | Address Used |
|-----|-------------|
| Application | Application protocol |
| Transport | Port number |
| Internet | IP address |
| Local Network | MAC address |
| Physical | Signal on medium |

---

## 14. OSI Model (Comparison)

- Developed by **ISO** in late 1970s–1980s
- 7‑layer model designed to replace TCP/IP
- More complex and slower to deploy
- TCP/IP won in real‑world usage

### Why OSI Still Matters
- Teaching and reference model
- Common language for explaining networking

---

## 15. TCP/IP vs OSI Mapping

| TCP/IP (5‑Layer) | OSI (7‑Layer) |
|-----------------|--------------|
| Application | Application / Presentation / Session |
| Transport | Transport |
| Internet | Network |
| Local Network | Data Link |
| Physical | Physical |

> This is why the TCP/IP Application layer is often called **Layer 7**.

---

## 16. Final Review

- TCP/IP is the foundation of the Internet
- Layered models simplify complexity
- Each layer has:
  - A specific role
  - Specific addressing
- Understanding encapsulation, PDUs, and layer interaction is **critical for CCNA**

---

✅ **End of Day 3 – TCP/IP Model**


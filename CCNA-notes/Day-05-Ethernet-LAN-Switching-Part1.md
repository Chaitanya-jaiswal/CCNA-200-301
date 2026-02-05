# Day 5 - Ethernet LAN Switching

---

## Ethernet LAN Switching Overview

- Ethernet LAN Switching focuses on communication **within a Local Area Network (LAN)**.
- **Switches** forward traffic inside a LAN.
- **Routers** connect different LANs or connect a LAN to a WAN/Internet.
- Traffic destined outside the LAN is sent to the **default gateway (router)**.

---

## OSI Model – Physical Layer (Layer 1)

- Defines the **physical characteristics** of the medium used to transfer data.
- Examples:
  - Voltage levels
  - Maximum transmission distances
  - Physical connectors
  - Cable specifications
- Converts digital bits into:
  - **Electrical signals** (wired)
  - **Radio signals** (wireless)
- Cables, pin layouts, and connectors belong to **Layer 1**.

---

## OSI Model – Data Link Layer (Layer 2)

- Provides **node-to-node connectivity**.
- Examples:
  - PC to switch
  - Switch to router
  - Router to router
- Defines how data is **formatted for transmission** over the physical medium.
- Detects (and sometimes corrects) Physical Layer errors.
- Uses **Layer 2 addressing (MAC addresses)**.
- **Switches operate at Layer 2**.

---

## Local Area Networks (LANs)

- A **LAN** is a local broadcast domain.
- Devices within the same LAN communicate through a **switch**.
- Each LAN is connected to other LANs using a **router**.
- Devices in different LANs **must use a router** to communicate.

---

## OSI Model – Protocol Data Units (PDUs)

As data moves down the OSI model, headers (and trailers) are added.

- **Data**  
  - Upper layers (Layers 7–5)
- **Segment**  
  - Layer 4 (Transport)
  - Data + Layer 4 header
- **Packet**  
  - Layer 3 (Network)
  - Segment + Layer 3 header
- **Frame**  
  - Layer 2 (Data Link)
  - Packet + Layer 2 header + Layer 2 trailer

---

## Ethernet Frame Structure

An Ethernet frame consists of:

- **Ethernet Header**
- **Packet** (Layer 3 data)
- **Ethernet Trailer**

Switches examine the **Ethernet header**, not the packet.

---

## Preamble and Start Frame Delimiter (SFD)

### Preamble
- Length: **7 bytes (56 bits)**
- Pattern: Alternating 1s and 0s (`10101010` × 7)
- Purpose:
  - Synchronizes sender and receiver clocks

### Start Frame Delimiter (SFD)
- Length: **1 byte (8 bits)**
- Pattern: `10101011`
- Marks:
  - End of the preamble
  - Start of the Ethernet frame

---

## Destination and Source MAC Addresses

- Identify the **receiving** and **sending** devices.
- Use **MAC addresses**.
- MAC = **Media Access Control**
- Size:
  - **6 bytes (48 bits)**
- MAC addresses identify **physical network interfaces**.

---

## Type / Length Field

- Size: **2 bytes (16 bits)**

Possible meanings:

### Length
- Value **1500 or less**
- Indicates the **length of the encapsulated packet** (in bytes)

### Type
- Value **1536 or greater**
- Indicates the **protocol type** of the encapsulated packet

Common values:
- IPv4 → `0x0800` (2048 decimal)
- IPv6 → `0x86DD` (34525 decimal)

---

## Ethernet Frame Field Sizes

| Field            | Size (bytes) |
|------------------|--------------|
| Preamble         | 7            |
| SFD              | 1            |
| Destination MAC  | 6            |
| Source MAC       | 6            |
| Type / Length    | 2            |
| FCS              | 4            |

- Total Ethernet overhead: **26 bytes** (header + trailer)

---

## Frame Check Sequence (FCS)

- Located in the **Ethernet trailer**
- Length: **4 bytes (32 bits)**
- Uses **CRC (Cyclic Redundancy Check)**
- Purpose:
  - Detect corrupted frames
- Ethernet **detects errors but does not correct them**

---

## MAC Address

- A **MAC address** is a **6-byte (48-bit)** physical address.
- Assigned to a device when it is manufactured.
- Also called a **Burned-In Address (BIA)**.
- Designed to be **globally unique**.

### MAC Address Structure

- **First 3 bytes (OUI)**  
  - Organizationally Unique Identifier  
  - Identifies the manufacturer
- **Last 3 bytes**  
  - Unique to the device

- Written as **12 hexadecimal characters**.

---

## MAC Address Table (CAM Table)

- Switches maintain a **MAC address table**.
- Maps:
  - **MAC address → Interface**

### MAC Learning Rule
- Switches learn MAC addresses from the **source MAC** of incoming frames.

---

## Unicast Frames

- **Unicast frame**:
  - Frame sent to **one specific destination**

### Unknown Unicast
- Destination MAC **not found** in the MAC address table.
- Switch action:
  - **Flood** the frame out all ports except the incoming port.

### Known Unicast
- Destination MAC **found** in the MAC address table.
- Switch action:
  - **Forward** the frame only to the correct port.

---

## MAC Address Aging

- MAC addresses learned dynamically are **not permanent**.
- If a MAC address is inactive for **5 minutes (300 seconds)**:
  - The entry is removed from the MAC address table.
- This is called **MAC address aging**.
- After aging out:
  - Frames to that MAC become **unknown unicast**
  - Flooding occurs again until relearned.

---

## Key CCNA Exam Takeaways

- Switches operate at **Layer 2**
- MAC addresses are **6-bytes**
- Switches learn from **source MAC addresses**
- Unknown unicast → **Flood**
- Known unicast → **Forward**
- Dynamic MAC entries age out after **5 minutes**
```

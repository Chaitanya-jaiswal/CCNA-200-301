# Day 6 – Ethernet LAN Switching (Part 2)

## Ethernet Frame

### Ethernet Frame Structure

* Ethernet frame consists of:

  * Ethernet Header
  * Payload (Packet)
  * Ethernet Trailer

### Fields

* **Preamble (7 bytes)**

  * Synchronization
  * Not counted as Ethernet header

* **SFD – Start Frame Delimiter (1 byte)**

  * Marks start of the frame
  * Not counted as Ethernet header

* **Destination MAC Address (6 bytes)**

  * Receiver MAC address

* **Source MAC Address (6 bytes)**

  * Sender MAC address

* **Type / EtherType (2 bytes)**

  * Identifies Layer 3 protocol
  * Common values:

    * IPv4 → `0x0800`
    * ARP → `0x0806`

* **FCS – Frame Check Sequence (4 bytes)**

  * Error detection using CRC

### Ethernet Header + Trailer Size

* Destination MAC: 6 bytes
* Source MAC: 6 bytes
* Type: 2 bytes
* FCS: 4 bytes

**Total = 18 bytes**

---

## Ethernet Frame Size and Padding

### Minimum Ethernet Frame Size

* Minimum Ethernet frame size = **64 bytes**
* Preamble + SFD are excluded

### Minimum Payload Size

```
64 − 18 = 46 bytes
```

* Minimum payload = **46 bytes**

### Padding

* If payload < 46 bytes:

  * Padding is added
* Padding:

  * Added at Layer 2
  * Consists of zeroes

### Example (ICMP Ping)

* Ping payload size: **36 bytes**
* Required payload: **46 bytes**
* Padding added: **10 bytes**

Wireshark shows:

* Ethernet II frame
* Padding displayed as `00000000000000000000`

---

## Ethernet Frame – Practical Observation

* Frame size shown in Wireshark: **60 bytes**
* Reason:

  * 14 bytes header + 46 bytes payload
  * Preamble and SFD not included

---

## ARP (Address Resolution Protocol)

* ARP resolves:

  * **IP address → MAC address**

### ARP Messages

* **ARP Request**

  * Broadcast
  * Destination MAC: `FFFF.FFFF.FFFF`

* **ARP Reply**

  * Unicast
  * Sent only to requesting host

---

## ARP Operation (Same Subnet)

### Scenario

* Network: `192.168.1.0/24`
* PC1 → `192.168.1.1`
* PC3 → `192.168.1.3`

PC1 wants to ping PC3.

### ARP Request

* Src IP: `192.168.1.1`

* Dst IP: `192.168.1.3`

* Src MAC: PC1 MAC

* Dst MAC: `FFFF.FFFF.FFFF`

* Switches flood the frame

### ARP Reply

* Src IP: `192.168.1.3`

* Src MAC: PC3 MAC

* Dst MAC: PC1 MAC

* Known unicast

* Switches forward (no flooding)

---

## ARP Table

### Viewing ARP Table

```
arp -a
```

* Available on Windows, macOS, Linux

### ARP Table Fields

* **Internet Address** → IP address (Layer 3)
* **Physical Address** → MAC address (Layer 2)
* **Type**:

  * Dynamic → learned via ARP
  * Static → default or manual

### After ARP Resolution

* Dynamic entry created:

  * IP → MAC mapping
* Entry may age out over time

---

## Ping (ICMP)

* Used to test reachability
* Measures round-trip time

### ICMP Messages

* ICMP Echo Request
* ICMP Echo Reply

### Command

```
ping <ip-address>
```

---

## Ping + ARP Interaction

* If destination MAC unknown:

  * ARP occurs first
* After ARP resolution:

  * ICMP frames are unicast

---

## MAC Address Table

* Maintained by switches
* Maps:

  * **MAC address → Interface**

### Viewing MAC Address Table

```
show mac address-table
```

### Fields

* VLAN
* MAC Address
* Type

  * Dynamic
  * Static
* Port

### MAC Learning Rule

* Switch learns MAC addresses from:

  * **Source MAC only**

---

## MAC Address Table Aging

* Dynamic MAC entries age out
* Default aging time (Cisco):

  * **300 seconds**

---

## Clearing the MAC Address Table

### Clear All Dynamic Entries

```
clear mac address-table dynamic
```

### Clear Specific MAC Address

```
clear mac address-table dynamic address <mac-address>
```

### Clear Entries on an Interface

```
clear mac address-table dynamic interface <interface>
```

---

## CCNA Exam Key Takeaways

* Minimum Ethernet frame size = **64 bytes**
* Header + trailer = **18 bytes**
* Minimum payload = **46 bytes**
* Padding added if payload too small
* ARP:

  * Request = broadcast
  * Reply = unicast
* Switches:

  * Learn MAC from source MAC
  * Flood broadcasts
  * Forward known unicasts

# Module 9: Address Resolution <!-- omit in toc -->

[Return to overview](../README.md)

---

- [MAC and IP](#mac-and-ip)
  - [Destination on Same Network](#destination-on-same-network)
  - [Destination on Remote Network](#destination-on-remote-network)
- [ARP](#arp)
  - [ARP Functions](#arp-functions)
  - [Removing Entries from an ARP Table](#removing-entries-from-an-arp-table)
  - [ARP Issues - ARP Broadcasting and ARP Spoofing](#arp-issues---arp-broadcasting-and-arp-spoofing)
- [Neighbor Discovery](#neighbor-discovery)

---

## MAC and IP

<u>Compare the roles of the MAC address and the IP address.</u>

### Destination on Same Network

There are two primary addresses assigned to a device on an Ethernet LAN:

- **Layer 2 physical address (the MAC address)** - Used for NIC to NIC communication on the same network.
- **Layer 3 logical address (the IP address)** - Used to send the packet from the source device to the destination device.

### Destination on Remote Network

When the destination IP address is on a remote network, the destination MAC address is that of the default gateway:

- **ARP is used by IPv4** to associate the IPv4 address of a device with the MAC address of the device NIC.
- **ICMPv6 is used by IPv6** to associate the IPv6 address of a device with the MAC address of the device NIC.

---

## ARP

<u>Describe the purpose of ARP.</u>

The purpose of an ARP is to **couple the MAC Address to an IP address**. It does this with an ARP table. Which has to be updated with **request and replies**.

### ARP Functions

To send a frame, a device will search its ARP table for a destination IPv4 address and a corresponding MAC address.

- If destination on the same network: the device will search the ARP table for the destination IPv4 address.
- If destination on a different network: the device will search the ARP table for the IPv4 address of the default gateway.
- If the device locates the IPv4 address, its corresponding MAC address is used as the destination MAC address in the frame.
- If there is no ARP table entry, than the device **sends and ARP request**

### Removing Entries from an ARP Table

Entries in the ARP table are not permanent and are removed when an ARP cache timer expires after a specified period of time.
The duration of the ARP cache timer differs depending on the operating system. ARP table entries can also be removed manually by the administrator. `arp -d`

Cisco IOS: `show ip arp`
Desktop: `arp -a`

### ARP Issues - ARP Broadcasting and ARP Spoofing

**ARP Broadcasting:** Excessive usage can cause some reduction in performance, but for gigabit this is not an issue only for fast ethernet.

**ARP replies can be spoofed:** A threat actor could perform an ARP poisoning attack and build its own ARP table. Recent switches have security software for this.

---

## Neighbor Discovery

<u>Describe the operation of IPv6 neighbor discovery.</u>

**Important:**

- IPv6 uses Neighbor Discovery (ND) instead of ARP
- ND works with solicitations and is more efficient than ARP

**Not important fun to know:**

IPv6 Neighbor Discovery (ND) protocol provides:

- Address resolution
- Router discovery
- Redirection services
- ICMPv6 Neighbor Solicitation (NS) and Neighbor Advertisement (NA)
- ICMPv6 Router Solicitation (RS) and Router Advertisement (RA) messages are used for messaging between devices and routers for router discovery.
- ICMPv6 redirect messages are used by routers for better next-hop selection.

ND looks a lot like ARP.
# Experiment 4: Demonstration of Network Communication Models (OSI / TCP-IP) Using a Network Simulation Tool

## 1. Aim

To demonstrate how data moves through the layers of the OSI and TCP/IP models using a network simulation tool (Cisco Packet Tracer), and to observe encapsulation and decapsulation.

## 2. Objectives

- Understand the layers of the OSI and TCP/IP models and how they map to each other.
- Build a small network and configure IP addressing.
- Use simulation mode to inspect protocol data units (PDUs) at each layer.
- Relate observed packets to layer functions.

## 3. Requirements

| Item | Details |
|---|---|
| Software | Cisco Packet Tracer (free with a Cisco Networking Academy account). Alternatives: GNS3, or Wireshark for real traffic capture |
| Devices (simulated) | 2 to 3 PCs, 1 switch, 1 router (optional for part B), straight-through and crossover cables |
| Knowledge | Basic IP addressing |

## 4. Theory

### 4.1 OSI and TCP/IP Layers

| OSI Layer | TCP/IP Layer | PDU | Function | Example Protocols / Devices |
|---|---|---|---|---|
| 7 Application | Application | Data | User-facing network services | HTTP, DNS, FTP, SMTP |
| 6 Presentation | Application | Data | Formatting, encryption, compression | TLS, JPEG |
| 5 Session | Application | Data | Session setup and management | NetBIOS, RPC |
| 4 Transport | Transport | Segment / Datagram | End-to-end delivery, ports, reliability | TCP, UDP |
| 3 Network | Internet | Packet | Logical addressing and routing | IP, ICMP, routers |
| 2 Data Link | Network Access | Frame | Physical addressing, framing | Ethernet, ARP, switches |
| 1 Physical | Network Access | Bits | Transmission of raw bits | Cables, hubs, Wi-Fi |

### 4.2 Encapsulation and Decapsulation

- **Encapsulation (sender):** Each layer adds its own header (and trailer at layer 2) around the data from the layer above.
- **Decapsulation (receiver):** Each layer strips its header and passes the payload upward.

## 5. Procedure

### Part A: Two PCs Connected Through a Switch

1. Open Packet Tracer and create a new file.
2. Add **two PCs** and **one switch** (for example, 2960).
3. Connect each PC's FastEthernet port to a switch port using a **copper straight-through** cable.
4. Configure IP addresses (Desktop > IP Configuration):

| Device | IP Address | Subnet Mask |
|---|---|---|
| PC0 | 192.168.1.10 | 255.255.255.0 |
| PC1 | 192.168.1.20 | 255.255.255.0 |

5. Wait for the link lights to turn green.
6. Open PC0 > Desktop > Command Prompt and run:

```
ping 192.168.1.20
```

7. Confirm replies are received.

### Part B: Observing Layers in Simulation Mode

1. Switch to **Simulation Mode** (bottom right).
2. Click **Edit Filters** and show only ICMP (and ARP).
3. Click **Add Simple PDU** (the closed envelope icon), click PC0, then PC1.
4. Click **Auto Capture / Play** or step with **Capture / Forward**.
5. Observe the envelope moving between devices. Note the ARP request first, then ICMP.
6. Click an envelope or a PDU entry in the event list to open **PDU Information**.
7. In the **OSI Model** tab, note what happens at each layer on the sending device (outbound) and receiving device (inbound).
8. In the **Inbound PDU Details / Outbound PDU Details** tabs, inspect the headers: Ethernet (MAC addresses), IP (source and destination IP), ICMP.

### Part C: TCP/IP Model with a Web Request (Optional)

1. Add a **Server** and connect it to the switch; set IP 192.168.1.100/24.
2. On the server, open Services > HTTP and ensure HTTP is on.
3. In Simulation Mode, filter for HTTP, DNS and TCP.
4. From PC0, open Desktop > Web Browser and enter `http://192.168.1.100`.
5. Observe the TCP three-way handshake (SYN, SYN-ACK, ACK), the HTTP request and response, and the TCP close.
6. Inspect the TCP header (source and destination ports, sequence numbers, flags).

### Part D: Routing Between Two Networks (Optional)

1. Add a router and two switches, each with a PC (Network A 192.168.1.0/24, Network B 192.168.2.0/24).
2. Configure router interfaces (example):

```
Router> enable
Router# configure terminal
Router(config)# interface gigabitEthernet 0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
Router(config)# interface gigabitEthernet 0/1
Router(config-if)# ip address 192.168.2.1 255.255.255.0
Router(config-if)# no shutdown
```

3. Set each PC's default gateway to its router interface address.
4. Ping across networks and observe how the MAC addresses change at each hop while IP addresses stay the same.

## 6. Observations

### Layer Activity Table

| Layer | Observation (what you saw in Packet Tracer) |
|---|---|
| Application | |
| Transport | |
| Network (IP) | |
| Data Link (MAC) | |
| Physical | |

### Header Details Captured

| Field | Value Observed |
|---|---|
| Source MAC | |
| Destination MAC | |
| Source IP | |
| Destination IP | |
| Protocol (ICMP/TCP) | |
| Source / destination ports (if TCP) | |

### Ping Results

| Source | Destination | Packets Sent | Received | Loss % | Avg Time (ms) |
|---|---|---|---|---|---|
| PC0 | PC1 | | | | |

## 7. Result

Data flow through the OSI and TCP/IP layers was demonstrated using a network simulator, and encapsulation and decapsulation were observed through PDU inspection.

## 8. Conclusion

Layered models divide network communication into manageable functions. Each layer adds or removes headers, and devices operate at specific layers (switches at layer 2, routers at layer 3). Simulation makes these abstract concepts visible.

## 9. Troubleshooting Tips

| Problem | Likely Cause | Fix |
|---|---|---|
| Ping fails on first try | ARP resolution delay | Ping again |
| Link light is red or amber | Wrong cable type or interface down | Check cable and `no shutdown` |
| No reply across networks | Missing default gateway | Set gateway on each PC |

## 10. Viva Questions

1. List the seven layers of the OSI model.
2. How do the OSI and TCP/IP models differ?
3. What is encapsulation?
4. At which layer does a switch operate? A router?
5. Why do MAC addresses change at every hop while IP addresses do not?
6. Explain the TCP three-way handshake.

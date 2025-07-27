IP Address Basics – Cybersecurity Notes
---

## What is an IP Address?

An **IP (Internet Protocol) address** is a unique identifier for a device on a network — like a phone number for your computer.

---

## IPv4 Format

- Made of **4 numbers** separated by dots, e.g., `192.168.1.1`
- Each number (called an **octet**) ranges from `0–255`
- Total of **32 bits** → `8 bits x 4 octets`

**Binary example**:
**11000000.10101000.00000001.00000001 = 192.168.1.1**


---

## Public vs Private IP Addresses

| Type   | Used For         | Example Ranges                  |
|--------|------------------|---------------------------------|
| Public | Internet traffic | Assigned by ISP                |
| Private| Local networks   | Internal devices (needs NAT)   |

Private IP ranges:
- `10.0.0.0 – 10.255.255.255` (Class A)
- `172.16.0.0 – 172.31.255.255` (Class B)
- `192.168.0.0 – 192.168.255.255` (Class C)

 **Tip**: Private IPs use **NAT** (Network Address Translation) to access the internet in other words, Private IP -> NAT -> Public IP.

---

##  IP Classes (for Subnetting)

| Class | Start Range                | Subnet Mask     | Host Capacity      |
|-------|----------------------------|------------------|--------------------|
| A     | `1.0.0.0 – 126.255.255.255`| `255.0.0.0` (/8) | ~16 million hosts |
| B     | `128.0.0.0 – 191.255.255.255`| `255.255.0.0` (/16) | ~65,000 hosts   |
| C     | `192.0.0.0 – 223.255.255.255`| `255.255.255.0` (/24) | 254 hosts     |

>  Class D = Multicast (skip for now)  
>  Class E = Experimental (also skip)

---

##  Why Were IP Classes Created?

To handle organizations of different sizes:
- Big companies → Class A
- Medium networks → Class B
- Small networks → Class C

Classes determined:
- How many bits are used for **network**
- How many for **host**

---

##  Why They're Outdated: CIDR

Modern networks use **CIDR (Classless Inter-Domain Routing)** for:
- Flexible subnetting
- More efficient IP address allocation

Still, classful networking is taught because:
- It builds a foundation for subnetting
- Helps understand different behaviors in IP ranges

---

##  What’s a Bit?

- A **bit** = smallest unit of data → `0` or `1`
- **8 bits** = 1 byte (or 1 octet)
- IP addresses are **32 bits**: 4 parts × 8 bits

---
#  Subnetting – Breaking Down IP Networks

---

##  What is Subnetting?

**Subnetting** = Dividing a large network into smaller, more manageable chunks (called *subnets*).

It helps devices figure out:
- "Which part of my IP address tells me where I live (network)?"
- "Which part tells me who I am (host)?"

---

## Example

- IP Address: `192.168.1.10`  
- Subnet Mask: `255.255.255.0`

This means:
- `192.168.1` → network part
- `.10` → host (your specific device)

---

### Benefits of Subnetting

- Better network organization  
- Improved security  
- Efficient IP address use  

---

## Key Subnet Terms

| Term              | Meaning |
|------------------|---------|
| **Network Address** | First IP in the subnet (represents the subnet itself) |
| **Broadcast Address** | Last IP (used to send messages to all devices in the subnet) |
| **Host Addresses** | All the usable IPs in between |

---

## Subnet Masks & CIDR Notation

- **Subnet mask**: Tells the system what portion of the IP is the network
- **CIDR** = *Classless Inter-Domain Routing*  
  Written as a slash (`/`) with number of bits used for the network

---

### CIDR Subnet Table

| CIDR | Subnet Mask         | Usable Hosts |
|------|---------------------|--------------|
| /24  | 255.255.255.0       | 254          |
| /25  | 255.255.255.128     | 126          |
| /26  | 255.255.255.192     | 62           |
| /27  | 255.255.255.224     | 30           |

>  Always subtract 2 from total hosts (1 for the network, 1 for broadcast)

---

## CIDR = “Cider” (like the drink)

`192.168.1.0/24`  
- `24 bits` used for network  
- `8 bits` left for hosts → `2^8 = 256` addresses  
- Minus 2 → `254 usable hosts`

---

##  Subnetting Analogy

Imagine hosting a giant party.

- IP address = name tag  
- Subnet = the table they're assigned to  
- CIDR = how many tables and how many seats per table  
---
# Why Do We Borrow Bits in Subnetting?

## Goal:
To divide a large network (like `192.168.1.0/24`) into smaller **sub-networks (subnets)**.

---

## IP Address Structure:
An IP address is **32 bits** total, split into:

- **Network bits** – identify the network or subnet
- **Host bits** – identify individual devices (hosts) within the subnet

---

##  Why Borrow Bits?

We **borrow bits from the host portion** to create more subnets.

**When you subnet, you borrow bits from the host portion to create more networks, which means more subnets, but fewer hosts in each one.**

## Think of it Like This

| What You Do                              | What Happens                                   |
|--------------------------------------------|--------------------------------------------------|
| Borrow bits from host portion              | You get **more subnets**                         |
| Increase subnet mask (e.g., /24 → /26)     | Each subnet gets **fewer usable host IPs**       |
| Shrink host space                          | **Reduce broadcast traffic**, increase **security & control** |
| Trade big flat network                     | For **multiple smaller, organized subnets**      |


### Formula:
2^n ≥ number of required subnets

Solve for `n` → this is the number of bits to borrow.

| Bits Borrowed | # of Subnets |
|---------------|--------------|
| 1 bit         | 2 subnets    |
| 2 bits        | 4 subnets    |
| 3 bits        | 8 subnets    |
| ...           | ...          |

---

## What Changes When You Borrow Bits?

| What Changes | Result |
|--------------|--------|
| Subnet mask increases (e.g. `/24` → `/26`) | More network bits |
| Hosts per subnet decrease | Fewer devices per subnet |
| Subnet count increases | More divisions, more control |

---

## Subnetting Example:

**Task:** Divide `192.168.1.0/24` into **4 subnets**

1. Use formula: `2^n ≥ 4` → `n = 2`
2. Add bits to CIDR: `/24 + 2 = /26`
3. Block size = `2^(32 - 26) = 64 IPs per subnet`
   - 62 usable (1 for network, 1 for broadcast)

### Resulting Subnets:

| Subnet | IP Range | Broadcast |
|--------|----------|-----------|
| Subnet 1 | 192.168.1.0 – 192.168.1.63 | 192.168.1.63 |
| Subnet 2 | 192.168.1.64 – 192.168.1.127 | 192.168.1.127 |
| Subnet 3 | 192.168.1.128 – 192.168.1.191 | 192.168.1.191 |
| Subnet 4 | 192.168.1.192 – 192.168.1.255 | 192.168.1.255 |

---

## Summary

> Borrowing bits allows you to create more subnets by shrinking the number of available host IPs.  
> This helps you organize, secure, and scale your network more efficiently.

---

## Remember:

- CIDR notation saves space and adds flexibility.
- Subnetting helps isolate traffic, secure systems, and better use IP ranges.
---
## Default Gateway

A **default gateway** is the IP address of a device (usually a router) that connects your local subnet to external networks — like the internet.

- Devices send packets to this IP if the destination is outside their subnet.
- Every subnet usually has **one default gateway**.
---

## 🔐 What Is a MAC Address?

A **MAC (Media Access Control) address** is a **unique identifier** burned into the **network interface card (NIC)** of a device.

> Think of it like the **serial number** for your network hardware.

**Example:**  
`00:1A:2B:3C:4D:5E`

---

## 📌 Why You Should Know It — Especially in Cybersecurity

| 🧪 Use Case                      | 💡 Why It Matters                                                                 |
|----------------------------------|------------------------------------------------------------------------------------|
| **Device Tracking**              | Each MAC is unique — helps **identify specific devices** even if their IP changes. |
| **Network Access Control (NAC)** | Allows you to **whitelist/block devices** based on MAC addresses.                 |
| **Packet Sniffing**              | Tools like **Wireshark** show MACs — you need to **read/analyze** them.           |
| **MITM Defense**                 | MAC spoofing is used in **Man-in-the-Middle attacks**. Helps detect rogue actors. |
| **DHCP/IP Assignments**          | Routers assign IPs **based on MACs**. Great for setting static IPs in a network.  |
| **ARP Poisoning Attacks**        | ARP attacks rely on spoofed MACs. Knowing MAC behavior helps defend against this. |

---

## 🧠 TL;DR

> MAC addresses are your **hardware-level identity** on a network.  
> If **IP addresses** are your **street address**, then **MAC addresses** are your **fingerprints**.





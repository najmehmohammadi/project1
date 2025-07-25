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

 **Tip**: Private IPs use **NAT** (Network Address Translation) to access the internet.

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

Example:

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

##  Subnetting Example

**Goal**: Divide `192.168.1.0/24` into 4 subnets

**Step 1**: How many bits do you need?  
→ `2^n ≥ 4` → `n = 2`

**Step 2**: Add to the CIDR  
→ `/24 + 2 = /26`

**Step 3**: Block size  
→ `2^(32 - 26) = 64` addresses per subnet

---

### 🧾 Final Subnets:

| Subnet # | IP Range                     |
|----------|------------------------------|
| 1        | 192.168.1.0 – 192.168.1.63    |
| 2        | 192.168.1.64 – 192.168.1.127  |
| 3        | 192.168.1.128 – 192.168.1.191 |
| 4        | 192.168.1.192 – 192.168.1.255 |

---

###  For Subnet `192.168.1.0/26`

- **Network Address**: `192.168.1.0`
- **Broadcast Address**: `192.168.1.63`
- **Valid Hosts**: `192.168.1.1 – 192.168.1.62`

---

## Remember:

- CIDR notation saves space and adds flexibility.
- Subnetting helps isolate traffic, secure systems, and better use IP ranges.




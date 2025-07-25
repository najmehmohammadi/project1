IP Address Basics – Cybersecurity Notes
---

## 📌 What is an IP Address?

An **IP (Internet Protocol) address** is a unique identifier for a device on a network — like a phone number for your computer.

---

## 📎 IPv4 Format

- Made of **4 numbers** separated by dots, e.g., `192.168.1.1`
- Each number (called an **octet**) ranges from `0–255`
- Total of **32 bits** → `8 bits x 4 octets`

**Binary example**:
**11000000.10101000.00000001.00000001 = 192.168.1.1**


---

## 🔓 Public vs 🔒 Private IP Addresses

| Type   | Used For         | Example Ranges                  |
|--------|------------------|---------------------------------|
| Public | Internet traffic | Assigned by ISP                |
| Private| Local networks   | Internal devices (needs NAT)   |

Private IP ranges:
- `10.0.0.0 – 10.255.255.255` (Class A)
- `172.16.0.0 – 172.31.255.255` (Class B)
- `192.168.0.0 – 192.168.255.255` (Class C)

🔑 **Tip**: Private IPs use **NAT** (Network Address Translation) to access the internet.

---

## 🧮 IP Classes (for Subnetting)

| Class | Start Range                | Subnet Mask     | Host Capacity      |
|-------|----------------------------|------------------|--------------------|
| A     | `1.0.0.0 – 126.255.255.255`| `255.0.0.0` (/8) | ~16 million hosts |
| B     | `128.0.0.0 – 191.255.255.255`| `255.255.0.0` (/16) | ~65,000 hosts   |
| C     | `192.0.0.0 – 223.255.255.255`| `255.255.255.0` (/24) | 254 hosts     |

> 🛑 Class D = Multicast (skip for now)  
> 🧪 Class E = Experimental (also skip)

---

## 🧠 Why Were IP Classes Created?

To handle organizations of different sizes:
- Big companies → Class A
- Medium networks → Class B
- Small networks → Class C

Classes determined:
- How many bits are used for **network**
- How many for **host**

---

## 🚫 Why They're Outdated: CIDR

Modern networks use **CIDR (Classless Inter-Domain Routing)** for:
- Flexible subnetting
- More efficient IP address allocation

Still, classful networking is taught because:
- It builds a foundation for subnetting
- Helps understand different behaviors in IP ranges

---

## 🧬 What’s a Bit?

- A **bit** = smallest unit of data → `0` or `1`
- **8 bits** = 1 byte (or 1 octet)
- IP addresses are **32 bits**: 4 parts × 8 bits

Example:

---

## 📚 Coming Soon
- Subnetting basics
- CIDR notation examples
- Practice problems

---

✍️ Written by a cybersecurity student learning the ropes.



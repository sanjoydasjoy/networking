

# Network Layer Characteristics

The Network Layer is the third layer of the OSI (Open Systems Interconnection) model that is responsible for enabling devices across different networks to communicate with each other. It plays a key role in the delivery of data from the source to the destination across multiple networks (internetworks).

<br>

#### Key Services:
- Provides services to allow end devices (like computers, phones, routers) to exchange data across networks.
- Utilizes protocols like:
  - IPv4 (Internet Protocol version 4)
  - IPv6 (Internet Protocol version 6)  
    These are the principal communication protocols at the network layer.
<br>

#### Basic Operations of the Network Layer:

1. Addressing End Devices  
   Assigns logical addresses (IP addresses) to devices so they can be identified on a network.

2. Encapsulation  
   Wraps data from the upper layers with a network layer header (which includes the IP address info) to form packets.

3. Routing  
   Determines the best path for data to travel from the source to the destination. Routers at this layer use routing tables and algorithms.

4. De-encapsulation  
   At the destination, the network layer removes the network layer header and passes the remaining data to the upper layer (Transport Layer).

<br>

___

<br>

# Why Can't the Network Layer Use MAC Addresses for Addressing?

first lets see what mac address is-

<br>

#### What is a MAC Address?

A MAC address (Media Access Control address) is a hardware identifier that’s permanently assigned to a device’s network interface card (NIC) by the manufacturer at the factory.

#### Key Characteristics:
- Unique: No two devices should have the same MAC address.
- Permanent: It’s “burned into” the hardware, although some systems let you change it temporarily (called "MAC spoofing").
- Layer: It operates at Layer 2 (Data Link Layer) of the OSI model.
- Local Communication: When devices talk on the same local network, they use MAC addresses to find each other (via ARP in IPv4).
- Switches Use It: Network switches use MAC addresses to learn and forward frames to the correct port.
- Format: A MAC address is 48 bits long (6 bytes), usually written in hexadecimal and it's divided into two parts: 
  `00:1A:2B:3C:4D:5E` or `00-1A-2B-3C-4D-5E`.

<br>

| Part | Length | Meaning |
|------|--------|---------|
| OUI (Organizationally Unique Identifier) | First 24 bits (3 bytes) | Assigned to the manufacturer (e.g., Intel, Cisco) |
| Device ID (NIC Specific) | Last 24 bits (3 bytes) | Unique for each device the manufacturer makes |

Example:
```
MAC Address: 00:1A:2B:3C:4D:5E
             └──────┘ └──────┘
             OUI        Device ID
```

- If two devices are from the same company (say, Dell), their first 3 bytes (OUI) might be the same.
- The last 3 bytes will be different, ensuring global uniqueness.

<br>
<br>

<br>

now lets back to Why Can't the Network Layer Use MAC Addresses for Addressing-

#### 1. MAC Address is a Flat Address (Not Hierarchical)
- MAC addresses are unique identifiers assigned to network interfaces by the manufacturer.
- They are flat addresses, meaning there's no structure to indicate location in a network.
- Routers and large networks need hierarchical addressing to efficiently route data across different networks — this is something IP addresses provide.

#### 2. MAC Addresses Are Vendor-Based
- The first part of a MAC address identifies the vendor or manufacturer (e.g., Dell, Intel).
- This has nothing to do with where the device is on a network.
- If we used MAC addresses for internet routing, routers would have no clue how to forward data based on them — there’s no geographic or topological info.

#### 3. IP Address Provides Logical, Hierarchical Addressing
- IP addresses (e.g., `192.168.1.10`) are structured to show:
  - Network ID (where the device is),
  - and Host ID (which device on that network).
- This structure helps routers determine the best path across interconnected networks — something MAC addresses can't support.

#### 4. MAC Addresses Work Only on Local Networks
- MAC addresses are used within the same LAN (Local Area Network).
- When data needs to go outside the LAN, it requires a Network Layer (IP) address to route it globally.

<br>

So basically:
- MAC = flat, vendor-based, local
- IP = hierarchical, logical, globally routable

<br>

___

<br>

# How a Host Routes

### **How a Host Sends Data (Routing Basics):**

1. **Every device** (PC, phone, etc.) creates its **own data packets**.
2. Each device has a **routing table** to decide **where to send the data**.

<br><br>

### **Where can a device send data?**

- **To itself** → uses `127.0.0.1` (loopback).
- **To local device** → same network (LAN).
- **To remote device** → different network.

<br><br>

### **How does it decide if local or remote?**

- Uses its **IP address**, **subnet mask**, and the **destination IP**.
- If destination is:
  - **Same network → send directly.**
  - **Different network → send to default gateway.**

<br><br>

### **What is a Default Gateway (DGW)?**

- It’s the **router**.
- Helps send data to **other networks (outside the LAN)**.
- Must be in the **same IP range** as the device.

<br><br>

### **How does a device know its Default Gateway?**

- **IPv4:** Given by **DHCP** or set manually.
- **IPv6:** Learns using **Router Solicitation (RS)** or set manually.

<br><br>

### **If no default gateway → can’t access the internet.**

<br><br>

### **How to see routing table on Windows:**

- Use command:  
  `route print` or `netstat -r`




<br>

___

<br>

# **What is Routing?**  
Routing means **choosing the best path** for data to travel from one network to another. Routers do this job.

<br><br>

### **When a router gets a packet, it:**
1. Looks at the **destination IP**.
2. Checks its **routing table**.
3. Decides **where to send** the packet next.

<br><br>

### **Types of Routes in Routing Table:**

1. **Directly Connected**  
   - Router is directly connected to that network.

2. **Remote Routes**  
   - Router is **not directly connected**.  
   - Learned by:
     - **Static route** (manually set)
     - **Dynamic route** (learned automatically)

3. **Default Route**  
   - Used when no specific route is found.  
   - Sends packet to a general direction.

<br><br>

### **Static Routing**
- Manually configured
- Doesn’t change by itself
- Good for **small or simple networks**

<br><br>

### **Dynamic Routing**
- Learns routes automatically
- Updates when the network changes
- Good for **large or changing networks**


<br>

___

<br>

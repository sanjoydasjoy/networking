# MAC and IP Addresses

### What Are These Two Types of Addresses?

Every network device (like your laptop, phone, or printer) connected to a wired or wireless network has two types of addresses:

### 1. MAC Address (Media Access Control)

- Think of it as a device's fingerprint  
- It is a unique hardware address built into the Network Interface Card (NIC)  
- It's assigned by the manufacturer and usually looks like this:  
  `00:1A:2B:3C:4D:5E`  
- This address never changes, no matter what network the device connects to  
- Used for communication inside the same local network (like between devices in your home or office)

### 2. IP Address (Internet Protocol)

- Think of it as your home address  
- It can change, depending on what network you connect to (Wi-Fi at home vs. school)  
- Example of an IPv4 address: `192.168.1.5`  
- Example of an IPv6 address: `fe80::1`  
- It helps your device send and receive data over the internet or between different networks

<br><br>

## When Two Devices Are on the Same Network

Let’s say your laptop wants to send something to your printer, both connected to the same Wi-Fi or LAN

Here’s what happens:

1. Your laptop already knows the IP address of the printer (like 192.168.1.10)  
2. It uses ARP to ask: "Who has this IP address? Please tell me your MAC address"  
3. The printer replies: "That's me, my MAC address is 00:AA:BB:CC:DD:EE"  
4. The laptop now sends the data directly to that MAC address  
5. This all stays within your local network — no internet involved

Summary:  
The IP helps identify the destination,  
The MAC is used to actually deliver the message inside the local network

<br><br>

## When the Devices Are on Different Networks

Let’s say you want to access Google from your laptop

Here’s what happens:

1. Your laptop sees Google’s IP address (like 142.250.64.78) is not on your home network  
2. It knows it must send the packet to the default gateway (your router)  
3. It uses ARP to ask: "Who is my default gateway? I need your MAC address"  
4. The router replies with its MAC address  
5. Your laptop sends the packet to the router's MAC address, even though the final destination is Google  
6. The router takes care of sending it over the internet to reach Google

It’s like mailing a letter to another city:  
You drop it at your local post office (router), and they take care of the delivery

<br><br>

## Address Resolution (How Do Devices Find Each Other?)

When your device knows the IP address but needs the MAC address, it uses:

- For IPv4:  
  ARP (Address Resolution Protocol) is used to resolve an IP address to a MAC address by sending a broadcast request.

- For IPv6:  
  Neighbor Discovery Protocol (NDP), which uses ICMPv6 messages, is used for the same purpose but with additional functions (like router discovery).





<br>

___

<br>



# ARP Table and Its Location

## What is an ARP Table?
The ARP (Address Resolution Protocol) table is a network database that stores the mappings between IP addresses and MAC addresses. When a device wants to communicate with another device on the same local network, it uses this table to find the corresponding MAC address for the target IP address. This mapping allows the device to send the data correctly over the network.

## Where Does the ARP Table Reside?

The ARP table resides in the memory (RAM) of each device on the network. Each device, including PCs, smartphones, routers, and switches, keeps its own ARP table to resolve IP-to-MAC address mappings for communication within the local network.

### Types of Devices and Their ARP Tables:

- Windows/Linux/macOS Computer:  
  On personal computers, the ARP table is stored in the computer’s RAM. You can view and manage this table using network commands like:  
  - Windows: `arp -a`  
  - Linux/macOS: `ip neigh` or `arp`

- Routers/Switches:  
  Routers and switches also keep ARP tables to map IP addresses to MAC addresses of devices on their interfaces. This helps them forward packets to the correct destination device.

## How Long Does the ARP Table Last?

- Dynamic Entries: These are learned automatically via ARP requests and time out after a short period (usually minutes). If the device does not need the mapping again in that time, it will remove the entry.

- Static Entries: These are manually configured and remain in the ARP table until the device is restarted or the entry is manually deleted.

## Why is the ARP Table Important?

The ARP table is essential for devices to communicate effectively on the same network. By maintaining a list of IP-to-MAC address mappings, devices can avoid unnecessary ARP requests and ensure that data packets reach their correct destination. Without the ARP table, devices would need to broadcast requests for every communication, leading to inefficiency.



<br><br>

## How ARP Works 

### Local Communication (Same Network)

Say your computer (192.168.1.2) wants to send data to a printer (192.168.1.10)

1. The computer first checks its ARP table, which stores recently learned IP-to-MAC pairs
2. If the MAC address for 192.168.1.10 is already known, it uses it directly
3. If it’s not found, the computer sends out a broadcast message asking, "Who has 192.168.1.10?"
4. The printer replies with its MAC address
5. The computer stores that info in the ARP table and sends the message to that MAC

The next time it needs to send something to the printer, it won’t ask again — it already knows <br><br>


another example:

<br><br>

Say **Phone A** (192.168.1.2) wants to send a photo to **Phone B** (192.168.1.10) over the same Wi-Fi network:

- Phone A first checks its ARP table, which stores recently learned IP-to-MAC address mappings  
- If the MAC address for 192.168.1.10 is already there, it uses it directly to send the photo  
- If it’s not found, Phone A sends out a message to everyone on the network:  
  "Who has 192.168.1.10?"  
- Phone B sees this and replies with its MAC address  
- Phone A stores this info in its ARP table and sends the photo to that MAC address  
- Next time it wants to send something to Phone B, it uses the stored MAC address — no need to ask again

  
<br><br>
question is how they finds out the ip of the device to send:

1. Pre-configured IP  
Devices may be manually assigned and told to use a specific IP, like 192.168.1.10 for a printer.

2. DNS or name resolution  
Names like printer.local are resolved to IPs using DNS, NetBIOS, or mDNS/Bonjour.

3. Broadcast discovery  
Devices scan the network or send broadcast messages to find others, which reply with their IPs.

4. Router or DHCP table  
The router keeps a list of connected devices and their IPs, which can be checked or scanned.



<br><br>

### Remote Communication (Different Network)

When your computer wants to access something outside your network (like a website)

1. It checks the IP and sees it’s not on the local network
2. The computer knows it must send the data to the default gateway (router)
3. It checks the ARP table for the router’s MAC address
4. If the MAC isn’t there, it sends a broadcast asking, "Who has 192.168.1.1?" (the gateway IP)
5. The router replies with its MAC, and the computer sends the data to that MAC

The router then forwards the data to the wider internet

<br><br>

## ARP Table – Where These Mappings Are Stored

Every device maintains an ARP table with a list of IP addresses and their corresponding MAC addresses

You can view this table:

- On a Windows PC:  
  Open Command Prompt and type `arp -a`

- On a Cisco router:  
  Use the command `show ip arp`

Example output:
```
192.168.1.10    AA-BB-CC-DD-EE-FF    dynamic
```

<br><br>

| Type     | How It's Added                   | Lifespan            | Example Use                                                                 |
|----------|----------------------------------|----------------------|------------------------------------------------------------------------------|
| Dynamic  | Learned via ARP                  | Temporary (expires)  | Communication with a specific device like a printer or another computer     |
| Static   | Manually set or built-in mappings | Permanent            | Broadcast (192.168.1.255 → ff-ff-ff-ff-ff-ff), or multicast (224.0.0.251 → 01-00-5e-00-00-fb for mDNS) |

<br><br>

## ARP Table Timeout and Maintenance

- Entries in the ARP table are temporary
- Each entry has a timeout (usually a few minutes)
- If an entry isn’t used for a while, it expires and is removed
- Administrators can also manually clear the ARP table if needed

<br><br>

## ARP Weaknesses and Risks

### Broadcast Overhead

- ARP requests are broadcast to all devices on the network
- On large networks, frequent broadcasts can cause unnecessary traffic and slow things down

### ARP Spoofing or Poisoning

- An attacker can send fake ARP replies to trick devices into updating their ARP table with incorrect information
- For example, the attacker might pretend to be the gateway
- This allows the attacker to intercept or modify traffic — a type of man-in-the-middle attack

### Protection Measures

- Enterprise-grade network switches may offer features like Dynamic ARP Inspection (DAI) to prevent spoofed ARP replies
- In very secure environments, some admins use static ARP entries to lock mappings in place




<br>

___

<br>

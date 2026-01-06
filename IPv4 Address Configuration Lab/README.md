## Overview

This hands-on lab provides practical experience configuring IPv4 addresses on Cisco router interfaces using Packet Tracer. This lab is part of the free CCNA 200-301 Complete Course by Jeremy's IT Lab.

**Video Source:** [Day 8 Lab - IPv4 Address Configuration](https://www.youtube.com/watch?v=e1jbvyMeS5I&list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ&index=15)

**Duration:** 10 minutes 5 seconds

**Lab File:** Download the Packet Tracer lab file from Jeremy's IT Lab website

---

## Prerequisites

- Cisco Packet Tracer installed (download from Cisco NetAcad)
- Basic understanding of IPv4 addressing
- Completion of Day 8 lecture material
- Familiarity with Cisco IOS command line interface

---

## Learning Objectives

By completing this lab, you will be able to:

1. Configure IPv4 addresses on router interfaces
2. Enable router interfaces using the `no shutdown` command
3. Add interface descriptions for network documentation
4. Verify interface configurations using show commands
5. Interpret interface status indicators (up/up, administratively down, etc.)
6. Save running configuration to NVRAM

---

## Lab Topology

The lab consists of a Cisco router with three interfaces:

- **GigabitEthernet0/0:** Connected to LAN 1 (192.168.1.0/24)
- **GigabitEthernet0/1:** Connected to LAN 2 (192.168.2.0/24)
- **GigabitEthernet0/2:** Point-to-point link (10.0.0.0/30)

---

## Tasks

### Task 1: Access Router CLI

- [ ]  Open the Packet Tracer lab file
- [ ]  Click on the router device
- [ ]  Select the CLI tab
- [ ]  Press Enter to activate the command prompt

### Task 2: Enter Privileged EXEC Mode

```
Router> enable
Router#
```

- [ ]  Verify you see the `#` prompt

### Task 3: Enter Global Configuration Mode

```
Router# configure terminal
Router(config)#
```

- [ ]  Verify you see the `(config)#` prompt

### Task 4: Configure GigabitEthernet0/0

```
Router(config)# interface gigabitethernet0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# description ## Connection to LAN 1 ##
Router(config-if)# exit
```

- [ ]  Enter interface configuration mode
- [ ]  Assign IP address 192.168.1.1 with subnet mask 255.255.255.0
- [ ]  Enable the interface
- [ ]  Add meaningful description
- [ ]  Return to global configuration mode

### Task 5: Configure GigabitEthernet0/1

```
Router(config)# interface gigabitethernet0/1
Router(config-if)# ip address 192.168.2.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# description ## Connection to LAN 2 ##
Router(config-if)# exit
```

- [ ]  Enter interface configuration mode
- [ ]  Assign IP address 192.168.2.1 with subnet mask 255.255.255.0
- [ ]  Enable the interface
- [ ]  Add meaningful description
- [ ]  Return to global configuration mode

### Task 6: Configure GigabitEthernet0/2

```
Router(config)# interface gigabitethernet0/2
Router(config-if)# ip address 10.0.0.1 255.255.255.252
Router(config-if)# no shutdown
Router(config-if)# description ## Point-to-Point Link ##
Router(config-if)# exit
```

- [ ]  Enter interface configuration mode
- [ ]  Assign IP address 10.0.0.1 with subnet mask 255.255.255.252 (/30)
- [ ]  Enable the interface
- [ ]  Add meaningful description
- [ ]  Return to global configuration mode

### Task 7: Verify Configuration

```
Router(config)# exit
Router# show ip interface brief
```

- [ ]  Exit to privileged EXEC mode
- [ ]  Verify all interfaces show assigned IP addresses
- [ ]  Confirm all interfaces are in **up/up** state

**Additional verification commands:**

```
Router# show interfaces description
Router# show running-config
```

- [ ]  Verify interface descriptions are visible
- [ ]  Review full running configuration

### Task 8: Save Configuration

```
Router# write memory
```

or

```
Router# copy running-config startup-config
```

- [ ]  Save configuration to NVRAM
- [ ]  Confirm successful save message

---

## Lab Questions

### Question 1: IPv4 Address Classes

What class is the network 192.168.1.0/24?

**Answer:** Class C. The first octet is 192, which falls in the range 192-223 for Class C networks.

---

### Question 2: Calculating Usable Hosts

How many usable host addresses are available in a /24 network?

**Answer:** 254 usable hosts

**Calculation:**

- Host bits: 32 - 24 = 8 bits
- Formula: 2^n - 2 = 2^8 - 2 = 256 - 2 = 254
- We subtract 2 for the network address and broadcast address

---

### Question 3: Usable Hosts in /30 Network

How many usable host addresses are in the 10.0.0.0/30 network configured on Gi0/2?

**Answer:** 2 usable hosts

**Calculation:**

- Host bits: 32 - 30 = 2 bits
- Formula: 2^2 - 2 = 4 - 2 = 2
- /30 networks are commonly used for point-to-point links between routers

---

### Question 4: First and Last Usable Addresses

For the network 192.168.1.0/24, what are the first usable address, last usable address, and broadcast address?

**Answer:**

- **Network address:** 192.168.1.0
- **First usable address:** 192.168.1.1
- **Last usable address:** 192.168.1.254
- **Broadcast address:** 192.168.1.255

---

### Question 5: Interface Status Meanings

What does each interface status combination mean?

a) up/up

b) administratively down/down

c) up/down

d) down/down

**Answers:**

**a) up/up:** Both Layer 1 (physical) and Layer 2 (data link) are functioning properly. This is the desired state.

**b) administratively down/down:** The interface has been manually disabled with the `shutdown` command or has never been enabled with `no shutdown`.

**c) up/down:** Layer 1 is functioning but Layer 2 has a problem. This could indicate an encapsulation mismatch or other data link layer issue.

**d) down/down:** Layer 1 has a problem. This typically means a cable is unplugged or there's a physical connectivity issue.

---

### Question 6: Command Mode Identification

What command mode is indicated by each prompt?

a) Router>

b) Router#

c) Router(config)#

d) Router(config-if)#

**Answers:**

**a) Router>** User EXEC mode - Limited read-only access with basic monitoring commands only.

**b) Router#** Privileged EXEC mode - Full read access to device, can view all configurations.

**c) Router(config)#** Global Configuration mode - Used to configure device-wide settings.

**d) Router(config-if)#** Interface Configuration mode - Used to configure specific interfaces.

---

### Question 7: Why Use Dotted Decimal?

Why must you use dotted decimal notation (255.255.255.0) instead of CIDR notation (/24) when configuring IP addresses?

**Answer:** The Cisco IOS `ip address` command requires the subnet mask in dotted decimal format. CIDR notation (/24) is not accepted in the configuration command syntax, although it can be used in documentation and is displayed in some show commands.

---

### Question 8: Common Configuration Mistake

What is the most common mistake when configuring router interfaces?

**Answer:** Forgetting to use the `no shutdown` command. Cisco router interfaces are administratively shutdown by default. Even with a correct IP address configured, the interface will remain in "administratively down/down" state until you enable it with `no shutdown`.

---

### Question 9: Verification Command

What is the most commonly used command to get a quick overview of all interfaces and their IP addresses?

**Answer:** `show ip interface brief`

This command displays:

- Interface names
- IP addresses (or "unassigned")
- Configuration status (OK? column)
- Configuration method
- Status (Layer 1 physical status)
- Protocol (Layer 2 data link status)

---

### Question 10: Subnet Mask Calculation

What is the subnet mask in dotted decimal notation for a /30 network?

**Answer:** 255.255.255.252

**Explanation:** A /30 means the first 30 bits are network bits:

- First three octets: 255.255.255 (24 bits)
- Fourth octet: 11111100 in binary = 252 in decimal
- Result: 255.255.255.252

---

## Troubleshooting Guide

### Problem: Interface shows "administratively down/down"

**Cause:** Interface has not been enabled

**Solution:**

```
Router(config)# interface gigabitethernet0/0
Router(config-if)# no shutdown
```

### Problem: Interface shows "up/down"

**Cause:** Physical layer is up but data link layer has an issue

**Solution:**

- Check cable connections
- Verify connected device is powered on and operational
- Check for encapsulation mismatches

### Problem: Cannot enter configuration mode

**Cause:** Not in privileged EXEC mode

**Solution:**

```
Router> enable
Router# configure terminal
```

### Problem: Configuration lost after router reload

**Cause:** Configuration not saved to NVRAM

**Solution:**

```
Router# write memory
```

or

```
Router# copy running-config startup-config
```

### Problem: IP address command rejected

**Cause:** Used CIDR notation instead of dotted decimal

**Solution:** Use `255.255.255.0` instead of `/24`

---

## Command Reference

### Navigation Commands

| Command | Purpose |
| --- | --- |
| `enable` | Enter privileged EXEC mode from user EXEC mode |
| `configure terminal` | Enter global configuration mode (can be abbreviated as `conf t`) |
| `interface <name>` | Enter interface configuration mode (can be abbreviated as `int`) |
| `exit` | Return to previous command mode |
| `end` | Return directly to privileged EXEC mode from any config mode |

### Configuration Commands

| Command | Purpose |
| --- | --- |
| `ip address <ip> <mask>` | Assign IP address and subnet mask to interface |
| `no shutdown` | Enable an interface (can be abbreviated as `no shut`) |
| `shutdown` | Disable an interface (can be abbreviated as `shut`) |
| `description <text>` | Add description to interface for documentation |
| `no ip address` | Remove IP address from interface |
| `no description` | Remove interface description |

### Verification Commands

| Command | Purpose |
| --- | --- |
| `show ip interface brief` | Quick overview of all interfaces and IP addresses |
| `show interfaces` | Detailed information and statistics for all interfaces |
| `show interfaces <name>` | Detailed info for specific interface |
| `show interfaces description` | Shows interface descriptions and status |
| `show running-config` | Display current active configuration |
| `show startup-config` | Display saved configuration in NVRAM |
| `show ip route` | Display routing table |

### Save Commands

| Command | Purpose |
| --- | --- |
| `write memory` | Save running-config to startup-config (can be abbreviated as `wr`) |
| `copy running-config startup-config` | Save running-config to startup-config |
| `copy run start` | Abbreviated version of above |

---

## Practice Exercises

### Exercise 1: Different Subnet Sizes

Reconfigure the router with these addresses:

- Gi0/0: 172.16.10.1 with mask 255.255.255.0
- Gi0/1: 172.16.20.1 with mask 255.255.255.0
- Gi0/2: 10.1.1.1 with mask 255.255.255.252

### Exercise 2: Calculate Subnet Information

For each network, calculate:

- Number of usable hosts
- Network address
- First usable address
- Last usable address
- Broadcast address

Networks:

1. 10.0.0.0/8
2. 172.16.50.0/24
3. 192.168.100.0/26
4. 10.10.10.0/30

### Exercise 3: Intentional Troubleshooting

1. Configure an interface but forget `no shutdown`
2. Use show commands to identify the problem
3. Fix the issue
4. Verify the fix worked

---

## Key Takeaways

✅ Router interfaces are **administratively shutdown by default** - always use `no shutdown`

✅ Subnet masks must be in **dotted decimal format** in configuration commands

✅ Interface descriptions improve **documentation and troubleshooting**

✅ `show ip interface brief` is the **most commonly used verification command**

✅ Always **save your configuration** to NVRAM with `write memory`

✅ Interface status **up/up** means both Layer 1 and Layer 2 are operational

✅ Use **Tab completion** and **command abbreviations** to work faster

✅ The formula for usable hosts is **2^n - 2** where n is the number of host bits

---

## Additional Resources

- **Free Packet Tracer Lab Files:** Jeremy's IT Lab website
- **Free Flashcards:** Available at Jeremy's IT Lab
- **CCNA 200-301 Complete Course:** Full playlist on YouTube
- **Practice Software:** Cisco Packet Tracer or GNS3
- **Books:** "Acing the CCNA Exam" Volume 1 & 2 by Jeremy McDowell

---

## Lab Completion Checklist

- [ ]  All three interfaces configured with correct IP addresses
- [ ]  All interfaces enabled with `no shutdown`
- [ ]  All interfaces show up/up status
- [ ]  Meaningful descriptions added to all interfaces
- [ ]  Verified configuration with `show ip interface brief`
- [ ]  Verified descriptions with `show interfaces description`
- [ ]  Configuration saved to NVRAM
- [ ]  Can answer all lab questions correctly
- [ ]  Understand common troubleshooting scenarios

---

## Author

Lab based on **CCNA 200-301 Complete Course** by **Jeremy's IT Lab**

Documented by: Eebbaa Dhugaasaa

Date: January 6, 2026
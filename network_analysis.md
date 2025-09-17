# 📡 Network PCAP Analysis Notes  

---

## 🔎 Summary  
- **Total Packets Analyzed:** ~2400  
- **Protocols Observed:** DHCP, DNS, STP, CDP, SNMP, HSRP, NTP  
- **Key IPv4 Range:** 192.168.x.x (local lab traffic)  
- **Key IPv6 Range:** 2003:51:6012:110::/64  
- **Focus Areas:** Device discovery, DHCP requests, STP topology changes, HSRP redundancy, SNMP queries  

---

## 🧪 Key Observations  
- **Primary Client IPv4:** 192.168.20.11  
- **Primary Client MAC:** 00:0c:29:82:f5:94 (observed in DHCP handshake)  
- **DHCP Behavior:** Client starts with 0.0.0.0 → broadcasts to 255.255.255.255 until lease granted.  
- **STP (Spanning Tree):** VLAN 20 had first topology change event.  
- **HSRP:** Virtual IP 192.168.121.1 observed for redundancy group 121.  
- **NTP:** IPv6 NTP server response identified.  
- **SNMP:** Device interface FA0/1 was queried.  

---

## 🔧 Analysis Tools & Filters Used  
**Wireshark Filters Applied:**  
- `dhcp` – to isolate DHCP packets  
- `dns` – to review DNS queries/responses  
- `stp` – to capture Spanning Tree Protocol events  
- `cdp` – to check Cisco Discovery Protocol announcements  
- `snmp` – to locate SNMP queries and responses  
- `hsrp` – to identify HSRP traffic and virtual IP  
- `ntp` – to check NTP server communication  
- `ipv6` – for IPv6-specific traffic inspection  

---

## ❓ Questions & Answers  

 ### Q18: What is the first IP address that is requested by the DHCP client?  
**Answer:** `192.168.20.11`  
**Filter Used:**  
```wireshark
dhcp.option.dhcp == 3


### Q19: What is the first authoritative name server returned for the domain that is being queried?
**Answer:** `ns1.hans.hosteurope.de`  
**Filter Used:**  
```wireshark
dns.flags.response == 1 && dns.ns

### Q20 What is the port for CDP for CCNP-LAB-S2?
**Answer:** `GigabitEthernet0/2`  
**Filter Used:**  
```wireshark
cdp


### Q22: What is the MAC address for the root bridge for VLAN 60?
**Answer:** `00:21:1b:ae:31:80`  
**Filter Used:**  
```wireshark
stp && vlan.id == 60


### What is the IOS version running on CCNP-LAB-S2?
**Answer:** `12.1(22)EA14`  
**Filter Used:**  
```wireshark
cdp


###Q24: What is the virtual IP address used for HSRP group 121??
**Answer:** `192.168.121.1`  
**Filter Used:**  
```wireshark
hsrp


###Q25: How many router solicitations were sent?
**Answer:** `3`  
**Filter Used:**  
```wireshark
icmpv6.type == 133


### Q26: What is the management address of CCNP-LAB-S2?
**Answer:** `192.168.121.20`  
**Filter Used:**  
```wireshark
cdp


### Q27: What is the interface being reported on in the first SNMP query?
**Answer:** `FA0/1`  
**Filter Used:**  
```wireshark
snmp



### Q28 When was the NVRAM config last updated?
**Answer:** `2017-03-03 21:02`  
**Filter Used:**  
```wireshark
snmp


### Q29: What is the IPv6 of the RADIUS server?
**Answer:** `2003:51:6012:110::dcf7:123`  
**Filter Used:**  
```wireshark
radius && ipv6



### Q30: What is the first authoritative name server returned for the domain that is being queried?
**Answer:** `ns1.hans.hosteurope.de`  
**Filter Used:**  
```wireshark
dns.flags.response == 1 && dns.ns





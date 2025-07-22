# phantom-iot-security

# 📡 The Phantom Network: Isolating IoT Threats

## 🔒 Overview
This project documents the segmentation of IoT devices from a home network using dedicated 2.4 GHz and 5 GHz networks to reduce the attack surface and contain vulnerabilities common to IoT environments. By isolating smart devices like TVs, printers, thermostats, and lights onto a separate VLAN, we prevent lateral movement from compromised IoT endpoints to more sensitive systems.

## 🎯 Project Scope
The goal was to create two isolated IoT networks—one for 2.4 GHz and another for 5 GHz-capable devices—and evaluate the effectiveness of that segmentation using Nessus Essentials scans.

**Devices Isolated:**
- Vizio 65” Smart TV
- Vizio 55” Smart TV
- Ecobee 3 Smart Thermostat
- HP DeskJet 2700 Series Printer
- 9x Feit Color-Changing Smart Lightbulbs

All devices were assigned IP addresses via DHCP and scanned using Nessus Essentials after segmentation.

## 📶 Network Setup
Using the TP-Link AX3000 (Archer AX55) router’s built-in IoT Network feature:

- **SSID 1:** `DroidVault` (2.4 GHz)
- **SSID 2:** `DroidVault_5G` (5 GHz)
- **Security:** WPA3-Personal + WPA2-PSK [AES]
- **Device Isolation:** Enabled via the IoT_Security setting on the router

## 🔌 Device Migration & Isolation
Each IoT device was connected to its appropriate network based on connectivity type. Device isolation was enforced, blocking communication with the main network (`TheEnterWebs`). Grouped IoT devices (e.g., lights) continued to function normally. Ping tests were performed via the Linux CLI to verify that devices were no longer reachable from the main network.

## 🔍 Vulnerability Scanning
Vulnerability scans were conducted using [Nessus Essentials](https://www.tenable.com/products/nessus/nessus-essentials). Two scans were created using the Advanced Scan template:

- **2.4 GHz Scan:** Feit smart lights + Ecobee thermostat
- **5 GHz Scan:** Vizio TVs + HP printer

Each scan was targeted by IP, set to random order, and included printer detection where applicable.

## 🧪 Results Summary

### ✅ 2.4 GHz Network
- 6 low-severity vulnerabilities detected
- Most notable: **ICMP Timestamp Request Disclosure (Plugin #10114)**
- All expected and internal-only; ping disabled externally
- Risk minimized through segmentation and isolation

### ⚠️ 5 GHz Network
- 26 vulnerabilities across 3 hosts
- Notable findings:
  - SNMP Agent Default Community Name (Plugin #41028)
  - SWEET32 Cipher Suites (Plugin #42873)
  - Deprecated TLS versions and untrusted SSL certificate

Due to limited firmware and UI controls, many vulnerabilities cannot be remediated. The self-signed SSL certificate was expected from TP-Link's internal access page.

**Crucially, isolation prevents these issues from impacting the main network.**

## 🧠 Conclusion
By segmenting vulnerable IoT devices into a separate network—**The Phantom Network**—this project significantly reduced risk to critical systems. Even without patching device-level vulnerabilities, network-level controls such as segmentation, isolation, and regular scanning provide meaningful defense against lateral attacks.

---

## 📁 Files Included

- All Nessus scan results, screenshots, and the network diagram are included in the full project report:  
📁 [`The_Phantom_Network_ Isolating_IoT_Threats.pdf`](The_Phantom_Network_%20Isolating_IoT_Threats.pdf)


---

## 💬 Author
**Zachary Andrew Carriker**  
Open to feedback, collaboration, and security discussions!  

# Cyber Security Internship - Task 1: Network Port Scanning

## Menu
- [Objective](#objective)
- [Tools Used](#tools-used)
- [Process](#process)  
  1. [Setup and Tool Installation](#1-setup-and-tool-installation)  
  2. [Identifying Network Range](#2-identifying-network-range)  
  3. [Executing the Nmap Scan](#3-executing-the-nmap-scan)  
  4. [Packet Analysis with Wireshark](#4-packet-analysis-with-wireshark)  
- [Scan Results](#scan-results)  
- [Interview Questions & Answers](#interview-questions--answers)  
- [Supporting Files](#supporting-files-in-this-repository)  

---

## Objective
The primary objective of this task was to learn and apply basic network reconnaissance techniques. This includes discovering open ports on devices within a local network to better understand the security posture and potential exposure to threats.

---

## Tools Used
- **Nmap**: A powerful command-line tool for network discovery and security auditing. Used for port scanning.  
- **Wireshark**: A widely-used network protocol analyzer. Used to capture and inspect the packets generated during the Nmap scan.

---

## Process

### 1. Setup and Tool Installation
The necessary tools, Nmap and Wireshark, were installed on a Kali Linux environment using the `apt` package manager.

**Command:**
```bash
sudo apt install nmap wireshark
```

2. Identifying Network Range

The ifconfig command was used to identify the local IP address and determine the network range to be scanned.

IP Address: 41.41.41.45

Network Range: 41.41.41.0/24

3. Executing the Nmap Scan

An Nmap TCP SYN scan (-sS) was performed on the entire /24 network range to efficiently find open ports on all potential hosts. The results were saved to a text file.

Command:

sudo nmap -sS -oN nmap_results.txt 41.41.41.0/24

4. Packet Analysis with Wireshark

Simultaneously with the Nmap scan, Wireshark was used to capture the network traffic. This provided a clear analysis of how the TCP SYN scan works by observing the exchange of SYN and SYN/ACK packets between the scanner and the target host.

Scan Results

The Nmap scan identified 5 active hosts within the 41.41.41.0/24 network range. The most notable findings were from host 41.41.41.43, which had a wide variety of open ports.

Summary of Open Ports on 41.41.41.43:

Port	State	Service	Potential Risk
21	open	ftp	Unencrypted data transfer, including credentials
22	open	ssh	Secure if configured correctly, but a target for brute force
23	open	telnet	Unencrypted communication, highly insecure
80	open	http	Potential for web-based vulnerabilities
139	open	netbios-ssn	Legacy service, can be vulnerable (e.g., WannaCry)
445	open	microsoft-ds	File sharing, common vector for malware (e.g., SMB exploits)
3306	open	mysql	Database access, could be vulnerable to SQL injection
5900	open	vnc	Remote desktop, potential for unauthorized access

For a complete list of all hosts and open ports, see the nmap_results.txt file.

Interview Questions & Answers

1. What is an open port?
An open port is a specific port on a computer that is configured to accept incoming packets. It indicates that a specific service or application is listening for communication on that port.

2. How does an Nmap TCP SYN scan work?
A TCP SYN scan (also known as a “half-open” scan) sends a TCP packet with the SYN flag set to a target port.

If the port is open, the target responds with a SYN/ACK packet. The scanner then sends an RST packet to close the connection before a full three-way handshake is completed.

If the port is closed, the target responds with an RST packet.

If there is no response, the port is considered filtered (likely by a firewall).

3. What risks are associated with open ports?
Open ports expose services that could potentially be exploited. If the services are unpatched, misconfigured, or unnecessary, they may provide attackers with an entry point into the system.

4. Explain the difference between TCP and UDP scanning.

TCP Scanning: Establishes connections using the Transmission Control Protocol, which is connection-oriented. It involves a three-way handshake (SYN, SYN/ACK, ACK), making detection easier.

UDP Scanning: Scans for services using the User Datagram Protocol, which is connectionless. Since UDP doesn’t send an acknowledgment for a received packet, scanners typically send a UDP packet and wait for an ICMP “Port Unreachable” message. If no message is received, the port is assumed open or filtered. UDP scanning is slower and less reliable than TCP scanning.

5. How can open ports be secured?
Open ports can be secured by:

Closing any ports that are not needed.

Using a firewall to restrict access to specific IP addresses.

Keeping the software and services running on those ports updated and patched.

Implementing strong authentication and access controls.

6. What is a firewall’s role regarding ports?
A firewall acts as a filter, controlling incoming and outgoing network traffic based on predefined security rules. It can be configured to block or allow traffic to specific services, helping to protect the Internet or intranet network from unauthorized access.

7. What is a port scan, and how do attackers perform it?
A port scan is a method used to identify open services on target ports. Attackers perform port scans to gather information, identify active services, explore vulnerabilities, and potential weaknesses that may be exploited to gain unauthorized access.

8. How does Wireshark complement port scanning?
Wireshark allows us to see the raw packets being exchanged during a port scan. This is useful for:

Verifying scan results: Confirming the responses (SYN/ACK, RST) from target ports.

Understanding scan techniques: Visualizing how different scan types (SYN, FIN, XMAS) look in network traffic.

Detecting scans: Identifying port scanning activity on a network by looking for patterns of connection attempts.

Supporting Files In This Repository

nmap_results.txt - The full text output from the Nmap scan.

wireshark_capture.pcap - The packet capture file from Wireshark.

screenshots/ - Directory containing all screenshots (1.png, 2.png, 3.png) taken during the process

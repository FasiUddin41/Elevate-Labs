# Interview Questions & Answers

## 1. What is an open port?
An open port is a specific port on a computer that is configured to accept incoming packets. It indicates that a specific service or application is listening for communication on that port.

## 2. How does an Nmap TCP SYN scan work?
A TCP SYN scan (also known as a “half-open” scan) sends a TCP packet with the SYN flag set to a target port.

If the port is open, the target responds with a SYN/ACK packet. The scanner then sends an RST packet to close the connection before a full three-way handshake is completed.

If the port is closed, the target responds with an RST packet.

If there is no response, the port is considered filtered (likely by a firewall).

## 3. What risks are associated with open ports?
Open ports expose services that could potentially be exploited. If the services are unpatched, misconfigured, or unnecessary, they may provide attackers with an entry point into the system.

## 4. Explain the difference between TCP and UDP scanning.

TCP Scanning: Establishes connections using the Transmission Control Protocol, which is connection-oriented. It involves a three-way handshake (SYN, SYN/ACK, ACK), making detection easier.

UDP Scanning: Scans for services using the User Datagram Protocol, which is connectionless. Since UDP doesn’t send an acknowledgment for a received packet, scanners typically send a UDP packet and wait for an ICMP “Port Unreachable” message. If no message is received, the port is assumed open or filtered. UDP scanning is slower and less reliable than TCP scanning.

## 5. How can open ports be secured?
Open ports can be secured by:

Closing any ports that are not needed.

Using a firewall to restrict access to specific IP addresses.

Keeping the software and services running on those ports updated and patched.

Implementing strong authentication and access controls.

## 6. What is a firewall’s role regarding ports?
A firewall acts as a filter, controlling incoming and outgoing network traffic based on predefined security rules. It can be configured to block or allow traffic to specific services, helping to protect the Internet or intranet network from unauthorized access.

## 7. What is a port scan, and how do attackers perform it?
A port scan is a method used to identify open services on target ports. Attackers perform port scans to gather information, identify active services, explore vulnerabilities, and potential weaknesses that may be exploited to gain unauthorized access.

## 8. How does Wireshark complement port scanning?
Wireshark allows us to see the raw packets being exchanged during a port scan. This is useful for:

Verifying scan results: Confirming the responses (SYN/ACK, RST) from target ports.

Understanding scan techniques: Visualizing how different scan types (SYN, FIN, XMAS) look in network traffic.

Detecting scans: Identifying port scanning activity on a network by looking for patterns of connection attempts.


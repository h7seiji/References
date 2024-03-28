# Network

## Open Systems Interconnection (OSI) Model

- 7 - Application Layer
  - Specific type of application itself and its standardized communication methods.
  - Ex.: HTTPS, POP3, SMTP
- 6 - Presentation Layer
  - Syntax of the data itself for applications to send and consume.
  - Ex.: HTML, JSON, CSV
- 5 - Session Layer
  - Network coordination between two separate applications in a session.
  - Ex.: NFS, SMB
- 4 - Transport Layer
  - Ensure that data packets arrive in the right order, without losses or errors, or can be seamlessly recovered if required. Flow control, along with error control, is often a focus at the transport layer.
  - Ex.: TCP, UDP
- 3 - Network Layer
  - Routing, forwarding, and addressing across a dispersed network or multiple connected networks of nodes or machines. The network layer may also manage flow control.
  - Ex.: IP, ICMP
- 2 - Data Link Layer
  - Connect two machines across a network where the physical layer already exists. It manages data frames, which are digital signals encapsulated into data packets. Flow control and error control of data are often key focuses of the data link layer.
  - Split into two sub-layers:
    - MAC
    - LLC
  - Ex.: Ethernet
- 1 - Physical Layer
  - Physical communication medium and the technologies to transmit data across that medium. At its core, data communication is the transfer of digital and electronic signals through various physical channels like fiber-optic cables, copper cabling, and air.
  - Ex.: Bluetooth, NFC

## TCP/IP Model

- Physical layer
- Data link layer
- Network layer
- Transport layer
- Application layer

## IP

### Subnets

## ICMP

The Internet Control Message Protocol (ICMP) is a network layer protocol used by network devices to diagnose network communication issues. ICMP is mainly used to determine whether or not data is reaching its intended destination in a timely manner.

- Used for error reporting
- Used for network diagnostics
- Connectionless protocol (not associated with a transport layer protocol)

## SSH

## RDP

## Proxy

## NGINX

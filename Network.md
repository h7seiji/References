# Network

## Open Systems Interconnection (OSI) Model

- 7 - Application Layer
  - Specific type of application itself and its standardized communication methods.
  - Ex.: HTTP, HTTPS, POP3, SMTP, XMPP
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

## XMPP (Jabber)

Extensible Messaging and Presence Protocol

Key XMPP technologies:

- Core — information about the core XMPP technologies for XML streaming
- Jingle — SIP-compatible multimedia signalling for voice, video, file transfer, and other applications
- Multi-User Chat — flexible, multi-party communication
- PubSub — alerts and notifications for data syndication, rich presence, and more
- BOSH — an HTTP binding for XMPP (and other) traffic

### Core

At its core, XMPP is a technology for streaming XML over a network.

Originally designed to provide an open, secure, decentralized alternative to consumer-oriented instant messaging (IM) services like ICQ, AIM, and MSN.

Core technologies:

- The base XML streaming layer
- Channel encryption using Transport Layer Security (TLS)
- Strong authentication using the Simple Authentication and Security Layer (SASL)
- Use of UTF-8 for complete Unicode support, including fully internationalized addresses
- Built-in information about network availability (“presence”)
- Presence subscriptions for two-way authorization
- Presence-enabled contact lists (“rosters”)

### Jingle (Multimedia)

Jingle provides a way for Jabber clients to set up, manage, and tear down multimedia sessions (voice chat, video chat, file transfer).
Can use a wide range of media transport methods (such as TCP, UDP, RTP, or even in-band XMPP itself).
The signalling to establish a Jingle session is sent over XMPP, and typically the media is sent directly peer-to-peer or through a media relay.
Jingle provides a pluggable framework for both application types and media transports; in the case of voice and video chat, a Jingle negotiation usually results in use of the Real-time Transport Protocol (RTP) as the media transport and thus is compatible with existing multimedia technologies such as the Session Initiation Protocol (SIP).

### Multi-User-Chat (MUC) (Group chat)

MUC is an XMPP extension for multi-party information exchange similar to Internet Relay Chat (IRC), whereby multiple XMPP users can exchange messages in the context of a room or channel. In addition to standard chatroom features such as room topics and invitations, the protocol defines a strong room control model, including the ability to kick and ban users, to name room moderators and administrators, to require membership or passwords in order to join the room, etc. Because MUC rooms are based on XMPP, they can be used to exchange not only plaintext message bodies but a wide variety of XML payloads.

### PubSub

PubSub is a protocol extension for generic publish-subscribe functionality, specified in XEP-0060. The protocol enables XMPP entities to create nodes (topics) at a pubsub service and publish information at those nodes; an event notification (with or without payload) is then broadcasted to all entities that have subscribed to the node. Pubsub therefore adheres to the classic Observer design pattern and can serve as the foundation for a wide variety of applications, including news feeds, content syndication, rich presence, geolocation, workflow systems, network management systems, and any other application that requires event notifications. The personal eventing protocol (PEP), specified in XEP-0163, provides a presence-aware profile of PubSub that enables every user’s JabberID to function as a virtual pubsub service for rich presence, microblogging, social networking, and real-time interactions.

### BOSH

BOSH is “Bidirectional-streams Over Synchronous HTTP”, a technology for two-way communication over the Hypertext Transfer Protocol (HTTP). BOSH emulates many of the transport primitives that are familiar from the Transmission Control Protocol (TCP). For applications that require both “push” and “pull” communications, BOSH is significantly more bandwidth-efficient and responsive than most other bidirectional HTTP-based transport protocols and the techniques known as AJAX. BOSH achieves this efficiency and low latency by avoiding HTTP polling, yet it does so without resorting to chunked HTTP responses as is done in the technique known as Comet. To date, BOSH has been used mainly as a transport for traffic exchanged between Jabber/XMPP clients and servers (e.g., to facilitate connections from web clients and from mobile clients on intermittent networks). However, BOSH is not tied solely to XMPP and can be used for other kinds of traffic, as well.

## MQTT

MQTT is a standards-based messaging protocol, or set of rules, used for machine-to-machine communication.

The MQTT protocol has become a standard for IoT data transmission.

- Pub/Sub

### Components

- Client: Any device that runs an MQTT library.
  - Publisher: Sends messages
  - Receiver: Receives messages
- Broker: Backend system which coordinates messages between the different clients.
  - Receiving and filtering messages
  - Identifying clients subscribed to each message, and sending them the messages
  - Authorizing and authenticating MQTT clients
  - Passing messages to other systems for further analysis
  - Handling missed messages and client sessions
- Connection: Clients and brokers begin communicating by using an MQTT connection.
  - Clients initiate the connection by sending a CONNECT message to the MQTT broker.
  - The broker confirms that a connection has been established by responding with a CONNACK message.
  - Both the MQTT client and the broker require a TCP/IP stack to communicate.

## SIP

Session Initiation Protocol

Application Layer

## WebRTC

## Websocket

## SMTP

Simple Mail Transfer Protocol

Think of SMTP as a digital postman that first, picks up your package (email) and takes it from your email client to the server, aptly named SMTP server (as it’s used solely for sending out messages). Another postman then picks up the package and takes it all the way to the recipient’s server where it’s picked up and stored for milliseconds at the recipient’s POP3/IMAP server. When all the pleasantries are exchanged, the incoming mail is then delivered to the recipient, without the involvement of SMTP anymore but with separate IMAP/POP3 protocols.

## POP3

## IMAP

## TLS

SSL (Secure Socket Layer) and its successor TLS (Transport Layer Security) are two cryptographic protocols.
Both rely on a set of private and public keys to turn messages into useless strings of characters.

### STARTTLS

STARTTLS is not a protocol but an email protocol command. It’s used to tell an email server that an email client (such as Gmail, Outlook, etc.) wants to upgrade an existing insecure connection to an encrypted one using SSL or TLS.

## SASL

Simple Authentication and Security Layer (SASL) is a framework for authentication and data security in Internet protocols. It decouples authentication mechanisms from application protocols, in theory allowing any authentication mechanism supported by SASL to be used in any application protocol that uses SASL.

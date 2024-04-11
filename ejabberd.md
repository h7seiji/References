# ejabberd

<https://docs.ejabberd.im/tutorials/>

Basic Tutorial: <https://www.process-one.net/blog/how-to-move-the-office-to-real-time-im-on-ejabberd/>

- ejabberd is a free and open source instant messaging server written in Erlang/OTP.
- ejabberd is cross-platform, distributed, fault-tolerant, and based on open standards to achieve real-time communication.
- ejabberd is designed to be a rock-solid and feature rich XMPP server.
- ejabberd is suitable for small deployments, whether they need to be scalable or not, as well as extremely large deployments.

## Key Features

- Cross-platform
- Distributed
- Fault-tolerant
- Administrator Friendly
- Internationalized
- Open Standards

## API

ejabberd comes with a powerful API serving two goals:

- Manage the XMPP service and integrate the platform with back-end platforms and script tools.
- Allow users to perform tasks via the client, allowing simple basic clients that do not need to use XMPP protocol. This can be handy, for example to send a message from your smartwatch, or show the number of offline messages.

## Modules

Thanks to the modular architecture of ejabberd, the platform is becoming a core component for messaging applications.

Messaging applications require to transfer more than text messages. ejabberd has grow a full set of media related features that makes ejabberd a great choice to support voice and video applications, but also to proxy various kind of media transfer (images, audio and video files for example).

As such, ejabberd support:

Jingle, XMPP based voice protocol
SIP (Session Initiation Protocol): Yes, you can pass SIP calls using ejabberd
ICE (Interactive Connectivity Establishment: A Protocol for Network Address Translator (NAT) Traversal)
STUN
TURN
Proxy65 media relay
This makes ejabberd the best XMPP server to support SIP and WebRTC based communication tools.

## Core

### Network Layer

Once ejabberd is started, some external events should obviously make it doing something. Besides explicit administrative commands, the most relevant such events are incoming connections. Incoming connections are handled inside Network Layer. The layer implemented by ejabberd_listener.erl, ejabberd_receiver.erl and ejabberd_socket.erl modules.

Once a connection is accepted by ejabberd_listener.erl, an instance (a process) of ejabberd_receiver.erl is started and it becomes the socket owner, where it performs the following operations:

- Throttles a connection using shapers from shaper.erl module
- Performs TLS decoding using fast_tls library
- Performs stream decompression using ezlib library
- Parses incoming raw XML data into #xmlel{} packets using fast_xml library

ejabberd_socket.erl does the same but in a reverse order, i.e. it performs stream compression and/or TLS encoding, serializes #xmlel{} packets into raw XML data and puts them into a socket (note that shapers do not apply for outgoing data).

Once xmlel{} packet is constructed by ejabberd_receiver.erl it's passed to XMPP Stream Layer.

### XMPP Stream Layer

XMPP Stream Layer is represented by xmpp_stream_in.erl and xmpp_stream_out.erl modules. An instance (i.e. a process) of xmpp_stream_in.erl is started along with an instance of ejabberd_receiver.erl and all incoming #xmlel{} packets are passed from the latter to the former. xmpp_stream_in.erl module does the following:

- Encodes/decodes #xmlel{} packets using xmpp library from/to internal structures (records) defined in xmpp_codec.hrl.
- Performs negotiation of inbound XMPP streams
- Performs STARTTLS negotiation (if needed)
- Performs compression negotiation (if needed)
- Performs SASL authentication

During these procedures xmpp_stream_in.erl calls functions from its callback modules, i.e. the modules of xmpp_stream_in behaviour: ejabberd_c2s.erl, ejabberd_s2s_in.erl or ejabberd_service.erl, depending on the stream namespace.

#### ejabberd_c2s, ejabberd_s2s_in and ejabberd_service

These are modules of xmpp_stream_in behavior. The only purpose of these modules is to provide callback functions for xmpp_stream_in.erl module. Examples of such callback functions are:

- tls_enabled/1: tells whether or not TLS is enabled in the configuration
- check_password_fun/1: provides a function for SASL authentication
- handle_authenticated_packet/2: what to do with packets after authentication is completed

Roughly, they represent an intermediate (or "glue") code between XMPP Stream Layer and Routing Layer for inbound XMPP streams.

### Routing Layer

#### ejabberd_router

ejabberd_router.erl module is the main dispatcher of XMPP stanzas.

#### ejabberd_local

ejabberd_local.erl handles stanzas destined to the local server itself.

#### ejabberd_sm

ejabberd_sm.erl handles stanzas destined to local users.

#### route-registered processes

Any process can register a route to itself. It's done by calling to ejabberd_router:route/2 function.

#### ejabberd_s2s and ejabberd_s2s_out

If a stanza is destined neither to local virtual host not to a route-registered process, it's passed to ejabberd_s2s.erl module via ejabberd_s2s:route/1 function call.

## Backends

Backends are pluggable modules you can configure to define where you would like to store part or all of your data.

## MQTT

<https://www.process-one.net/blog/starting-with-mqtt-protocol-and-ejabberd-mqtt-broker/>

ejabberd MQTT broker is included in every installation of latest ejabberd versions and is available on port 1883 out-of-the-box.

## Authentication

<https://docs.ejabberd.im/developer/guide/#external-authentication>

## Databases

<https://docs.ejabberd.im/admin/configuration/database/>

# HACO: a highly available, causally ordered, distributed group chat

**Politecnico di Milano - Distributed Systems (A.Y. 2023/2024)**

This project implements a fully distributed group chat application, where users can create chat rooms, post messages, and participate in conversations with causal message delivery, all without relying on any centralized server.

## Project Description

The application supports:
- **Room Management**: Users can create and delete chat rooms with a fixed set of participants specified at room creation.
- **Fully Distributed Architecture**: Communication between users (peers) occurs without a central server.
- **High Availability**: Users can continue using the chat even during temporary network disconnections.
- **Causal Delivery**: Messages within each room are delivered in causal order to ensure consistency in conversation history.

### Key Features
- **Distributed Messaging**: All communication is done in a peer-to-peer (P2P) manner.
- **LAN Connectivity**: Peers are connected over LAN.
- **Reliable Clients**: Clients can join and leave the network at any time. Failures or partitions in the network are tolerated.
- **Java Serialization**: Messages are serialized using Java's native serialization.
- **UDP Multicast/Unicast**: Communication between peers uses unicast and multicast.

## Software Architecture

### P2P Model - **Gnutella-like Architecture**
- **Fully Distributed**: There is no central authority or supernode in the network. Peers discover each other dynamically.
- **Dynamic Topology**: No fixed topology is required. New peers join the network via a broadcast-based discovery mechanism.
- **Ping-Pong Protocol**: When a peer joins the network, it sends a `PING` message to discover other peers. Peers respond with a `PONG`, sharing their information for future communication.

### Distributed Protocol Overview
- **Messaging**: Peers exchange messages via **UDP multicast**. A dedicated multicast listener runs on a separate thread for each room.
- **Acknowledgements**: Communication is made reliable using an acknowledgment system for message delivery.
- **Vector Clocks**: Causal delivery of messages is ensured using vector clocks to maintain message ordering within each chat room.

## Technologies Used
- **Language**: Java
- **Networking**: UDP sockets (unicast and multicast)
- **Serialization**: Java Object Serialization
- **Multithreading**: Each room runs a separate listener for handling multicast messages.

## Assumptions and Constraints
- **Reliable Clients**: Clients are assumed to close the application in expected ways, ensuring that they do not leave the network abruptly.
- **No Centralized Authority**: The application is fully distributed, with no supernode or server.
- **Network Failures**: The system is resilient to network partitions, allowing peers to reconnect and continue messaging.

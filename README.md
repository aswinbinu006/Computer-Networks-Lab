# Computer Networks Laboratory

[![C](https://img.shields.io/badge/Language-C-blue.svg)](https://en.wikipedia.org/wiki/C_(programming_language))
[![Wireshark](https://img.shields.io/badge/Traffic_Analysis-Wireshark-1679A7.svg)](https://www.wireshark.org/)
[![Socket Programming](https://img.shields.io/badge/Networking-POSIX_Sockets-orange.svg)](https://man7.org/linux/man-pages/man7/socket.7.html)
[![License](https://img.shields.io/badge/License-Academic_Use-green.svg)](#)

A comprehensive repository containing practical lab experiments, C implementations, packet capture analyses, and theoretical studies for the **Computer Networks Laboratory** curriculum.

---

## 📑 Table of Contents

- [Overview](#-overview)
- [Experiment Index](#-experiment-index)
- [Detailed Lab Summaries](#-detailed-lab-summaries)
  - [Exp 1A: Fundamental Elements of Networking](#experiment-1a-fundamental-elements-of-computer-networking)
  - [Exp 1B: File Sharing Within LAN Using IP](#experiment-1b-file-sharing-within-an-organization-using-ip-address)
  - [Exp 2 & 3: TCP Client-Server Socket Programming](#experiment-2--3-tcp-client-server-socket-programming)
  - [Exp 4 & 5: UDP Client-Server Socket Programming](#experiment-4--5-udp-client-server-socket-programming)
  - [Exp 6: DNS Packet Analysis via Wireshark](#experiment-6-dns-packet-analysis)
  - [Exp 7: Application Layer Analysis (DNS & HTTP)](#experiment-7-application-layer-packet-analysis-dns--http)
  - [Exp 8: Sliding Window Protocol (Go-Back-N ARQ)](#experiment-8-sliding-window-protocol-go-back-n-arq)
  - [Exp 9: Traffic Shaping (Leaky Bucket & Token Bucket)](#experiment-9-traffic-shaping-algorithms-leaky-bucket--token-bucket)
  - [Exp 10: Distance Vector Routing Algorithm](#experiment-10-distance-vector-routing-algorithm)
- [Repository Structure](#-repository-structure)
- [Prerequisites & Compilation Guide](#-prerequisites--compilation-guide)

---

## 🔍 Overview

This repository covers the fundamental layers and protocols of computer networks through hands-on implementation and packet-level inspection:
- **Physical & Data Link Layers:** Topologies, cabling standards (T568A/B), flow control (Go-Back-N ARQ).
- **Network Layer:** IP addressing, routing protocols (Distance Vector / Bellman-Ford algorithm), traffic policing and shaping (Leaky Bucket & Token Bucket).
- **Transport Layer:** POSIX socket programming in C implementing connection-oriented (TCP) and connectionless (UDP) communications.
- **Application Layer:** Packet inspection and protocol verification of DNS and HTTP using Wireshark.

---

## 📚 Experiment Index

| No. | Experiment Title | Layer / Protocol | Key Tools / Files | Description |
| :---: | :--- | :--- | :--- | :--- |
| **1A** | [Fundamental Elements of Networking](./Experiment%20%201A) | Physical Layer | Network Hardware, RJ-45 | Study of network topologies, transmission media, devices, and cable termination (T568A / T568B). |
| **1B** | [File Sharing Within LAN Using IP](./Experiment%20%201B) | Application / Session | SMB/CIFS, ICMP (`ping`) | Configuring peer-to-peer and client-server file sharing within a local subnet using IP addressing. |
| **2** | [TCP Server Socket Programming](./Experiment%20%202) | Transport Layer (TCP) | [`server1222.c`](./Experiment%20%202/server1222.c) | Iterative connection-oriented TCP server using stream sockets (`SOCK_STREAM`). |
| **3** | [TCP Client Socket Programming](./Experiment%20%203) | Transport Layer (TCP) | [`client1222.c`](./Experiment%20%203/client1222.c) | TCP client establishing an active handshake connection to exchange data with the TCP server. |
| **4** | [UDP Server Socket Programming](./Experiment%20%204) | Transport Layer (UDP) | [`server_udp222.c`](./Experiment%20%204/server_udp222.c) | Connectionless iterative UDP server utilizing datagram sockets (`SOCK_DGRAM`). |
| **5** | [UDP Client Socket Programming](./Experiment%20%205) | Transport Layer (UDP) | [`client_udp_222.c`](./Experiment%20%205/client_udp_222.c) | Connectionless UDP client transmitting datagrams directly to server endpoints. |
| **6** | [DNS Packet Analysis](./Experiment%20%206) | Application / Transport | Wireshark, DNS (UDP 53) | Inspection of DNS query/response structures, flags, and resource record types (A, NS, CNAME, MX). |
| **7** | [DNS & HTTP Packet Analysis](./Experiment%20%207) | Application Layer | Wireshark, HTTP & DNS | Deep packet inspection of HTTP requests (GET/POST), status codes (200, 301, 404), and headers. |
| **8** | [Sliding Window Protocol (Go-Back-N)](./Experiment%208) | Data Link / Transport | [`sliding_window222.c`](./Experiment%208/sliding_window222.c) | Simulation of Go-Back-N sliding window ARQ with window sizing, timeouts, and frame retransmission. |
| **9** | [Traffic Shaping Algorithms](./Experiment%209) | Network / Transport | [`exp9_222.c`](./Experiment%209/exp9_222.c), [`exp9_2_222.c`](./Experiment%209/exp9_2_222.c) | Implementation of **Leaky Bucket** (constant rate leak) and **Token Bucket** (burst handling). |
| **10** | [Distance Vector Routing Algorithm](./Experiment_10) | Network Layer | [`exp10_222.c`](./Experiment_10/exp10_222.c) | Dynamic routing table calculation based on the distributed Bellman-Ford shortest path equation. |

---

## 🔬 Detailed Lab Summaries

### Experiment 1A: Fundamental Elements of Computer Networking
- **Focus:** Physical infrastructure, connectivity standards, and transmission media.
- **Key Concepts:**
  - **Topologies:** Bus, Star, Ring, Mesh, Tree, and Hybrid architectures.
  - **Transmission Media:** Guided media (Shielded/Unshielded Twisted Pair, Coaxial cable, Fiber Optic) vs. Unguided media.
  - **Networking Devices:** Hubs, Layer-2 Switches, Layer-3 Routers, Repeaters, Gateways, and Bridges.
  - **Cabling & RJ-45 Standards:** TIA/EIA-568A vs. TIA/EIA-568B color codes, Straight-through cables vs. Crossover cables.

### Experiment 1B: File Sharing Within an Organization Using IP Address
- **Focus:** Local Area Network (LAN) subnetting and resource sharing protocols.
- **Key Concepts:**
  - IPv4 network adapter configuration (`ipconfig` / `ip addr`).
  - Network reachability and latency verification with ICMP echo requests (`ping`).
  - Configuring network share permissions using SMB (Server Message Block) / CIFS over port 445.

### Experiment 2 & 3: TCP Client-Server Socket Programming
- **Focus:** Reliable, connection-oriented byte-stream transport over TCP (`SOCK_STREAM`).
- **Server (`server1222.c`):**
  - Workflow: `socket()` $\rightarrow$ `bind()` $\rightarrow$ `listen()` $\rightarrow$ `accept()` $\rightarrow$ `recv()` / `send()` $\rightarrow$ `close()`.
  - Operates passively on port `10222` waiting for incoming connections.
- **Client (`client1222.c`):**
  - Workflow: `socket()` $\rightarrow$ `connect()` $\rightarrow$ `send()` / `recv()` $\rightarrow$ `close()`.
  - Initiates 3-way handshake with server IP `127.0.0.1` and port `10222`.

### Experiment 4 & 5: UDP Client-Server Socket Programming
- **Focus:** Connectionless, low-overhead datagram transport over UDP (`SOCK_DGRAM`).
- **Server (`server_udp222.c`):**
  - Workflow: `socket()` $\rightarrow$ `bind()` $\rightarrow$ `recvfrom()` $\rightarrow$ `sendto()` $\rightarrow$ `close()`.
  - Receives packets from remote clients without requiring prior connection handshakes on port `10222`.
- **Client (`client_udp_222.c`):**
  - Workflow: `socket()` $\rightarrow$ `sendto()` $\rightarrow$ `recvfrom()` $\rightarrow$ `close()`.
  - Dispatches independent UDP datagrams targeting destination socket address.

### Experiment 6: DNS Packet Analysis
- **Focus:** Domain Name System resolution inspection via Wireshark.
- **Key Concepts:**
  - DNS transport mechanics running over UDP port 53.
  - Structure of DNS message: Identification (Transaction ID), Flags (QR, Opcode, AA, TC, RD, RA, RCODE), Question count, Answer count.
  - Analysis of Resource Records: `A` (IPv4 host address), `NS` (Authoritative Name Server), `CNAME` (Canonical name alias), `MX` (Mail Exchange).

### Experiment 7: Application Layer Packet Analysis (DNS & HTTP)
- **Focus:** Web protocol packet sniffing and protocol transactions.
- **Key Concepts:**
  - Analysis of HTTP/1.1 message structures over TCP port 80.
  - HTTP Request methods: `GET`, `POST`, `HEAD`.
  - HTTP Response status codes: `200 OK`, `301 Moved Permanently`, `404 Not Found`.
  - Analysis of connection models: Non-persistent (HTTP/1.0) vs. Persistent Keep-Alive (HTTP/1.1).

### Experiment 8: Sliding Window Protocol (Go-Back-N ARQ)
- **Focus:** Flow control and automatic repeat request (ARQ) error handling.
- **Implementation (`sliding_window222.c`):**
  - Sender window size $N$, allowing up to $N$ frames in transit before requiring acknowledgment.
  - Cumulative acknowledgment mechanism.
  - Timeout and retransmission logic: if an acknowledgment is lost or corrupt, the sender retreats and retransmits all outstanding unacknowledged frames starting from the lost frame sequence number.

### Experiment 9: Traffic Shaping Algorithms (Leaky Bucket & Token Bucket)
- **Focus:** Congestion management and policing in packet-switched networks.
- **Leaky Bucket (`exp9_222.c`):**
  - Enforces a strictly constant output leak rate regardless of arrival bursts.
  - Packets entering a full buffer are discarded immediately (overflow protection).
- **Token Bucket (`exp9_2_222.c`):**
  - Tokens accumulate in a bucket of capacity $B$ at a constant rate $R$.
  - Allows transmission bursts up to available token count, providing flexible bandwidth utilization.

### Experiment 10: Distance Vector Routing Algorithm
- **Focus:** Dynamic shortest-path calculation in distributed networks.
- **Implementation (`exp10_222.c`):**
  - Implements the distributed **Bellman-Ford equation**:
    $$DV_i[j] = \min_k \left\{ C[i][k] + DV_k[j] \right\}$$
  - Routers periodically exchange distance vectors with immediate neighbors until convergence is achieved.
  - Generates the complete routing table showing Destination, Next Hop, and Minimum Distance.

---

## 📁 Repository Structure

```text
Computer-Networks-Lab/
├── Experiment  1A/
│   └── README.md                  # Network topologies, media, devices, RJ-45 standards
├── Experiment  1B/
│   └── README.md                  # LAN file sharing & IP reachability
├── Experiment  2/
│   ├── README.md                  # TCP Server theory & documentation
│   └── server1222.c               # TCP Server C implementation
├── Experiment  3/
│   ├── README.md                  # TCP Client theory & documentation
│   └── client1222.c               # TCP Client C implementation
├── Experiment  4/
│   ├── README.md                  # UDP Server theory & documentation
│   └── server_udp222.c            # UDP Server C implementation
├── Experiment  5/
│   ├── README.md                  # UDP Client theory & documentation
│   └── client_udp_222.c           # UDP Client C implementation
├── Experiment  6/
│   └── README.md                  # DNS packet capture & Wireshark analysis
├── Experiment  7/
│   └── README.md                  # Application layer (DNS & HTTP) Wireshark analysis
├── Experiment 8/
│   ├── README.md                  # Sliding Window Protocol (Go-Back-N) documentation
│   └── sliding_window222.c        # Go-Back-N ARQ simulation in C
├── Experiment 9/
│   ├── README.md                  # Traffic shaping theoretical guide
│   ├── exp9_222.c                 # Leaky Bucket algorithm implementation in C
│   └── exp9_2_222.c               # Token Bucket algorithm implementation in C
├── Experiment_10/
│   ├── README.md                  # Distance Vector Routing documentation
│   └── exp10_222.c                # Bellman-Ford Distance Vector Routing in C
└── README.md                      # Main repository documentation
```

---

## 🛠️ Prerequisites & Compilation Guide

### Requirements
- **Operating System:** Linux (Ubuntu/Debian) or Windows Subsystem for Linux (WSL).
- **C Compiler:** `gcc` (GNU Compiler Collection).
- **Network Tools:** `wireshark`, `ping`, `iproute2` / `net-tools`.

```bash
# Ubuntu / Debian installation
sudo apt-get update
sudo apt-get install build-essential wireshark net-tools
```

---

### Step-by-Step Compilation & Execution

#### 1. TCP Socket Programming (Experiments 2 & 3)
Open two separate terminal windows:

```bash
# Terminal 1: Run TCP Server
cd "Experiment  2"
gcc server1222.c -o server
./server

# Terminal 2: Run TCP Client
cd "Experiment  3"
gcc client1222.c -o client
./client
```

#### 2. UDP Socket Programming (Experiments 4 & 5)
Open two separate terminal windows:

```bash
# Terminal 1: Run UDP Server
cd "Experiment  4"
gcc server_udp222.c -o server_udp
./server_udp

# Terminal 2: Run UDP Client
cd "Experiment  5"
gcc client_udp_222.c -o client_udp
./client_udp
```

#### 3. Sliding Window Protocol - Go-Back-N (Experiment 8)
```bash
cd "Experiment 8"
gcc sliding_window222.c -o sliding_window
./sliding_window
```

#### 4. Traffic Shaping Algorithms (Experiment 9)
```bash
cd "Experiment 9"

# Leaky Bucket
gcc exp9_222.c -o leaky_bucket
./leaky_bucket

# Token Bucket
gcc exp9_2_222.c -o token_bucket
./token_bucket
```

#### 5. Distance Vector Routing Algorithm (Experiment 10)
```bash
cd "Experiment_10"
gcc exp10_222.c -o distance_vector
./distance_vector
```

---

## 📄 License & Attribution

This repository is maintained for academic and laboratory educational purposes. All implementations comply with POSIX socket standards and network protocol specifications.

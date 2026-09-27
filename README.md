# 🌐 Networking Essentials for System Design Interviews

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)
[![System Design](https://img.shields.io/badge/System%20Design-Interview%20Prep-blue.svg)](#)

> A comprehensive, battle-tested reference guide on networking fundamentals, layer-by-layer protocol selection, load balancing, and fault tolerance strategies for System Design Interviews (SDIs).

---

## 📌 Table of Contents

- [🍰 Overview & The OSI Layered Model](#-overview--the-osi-layered-model)
- [🔌 Layer-by-Layer Protocol Breakdown](#-layer-by-layer-protocol-breakdown)
  - [Layer 3: IP (v4 vs v6, Public vs Private)](#-layer-3-network-layer-ip)
  - [Layer 4: Transport (TCP, UDP, QUIC)](#-layer-4-transport-layer-tcp-udp-quic)
  - [Layer 7: Application Protocols (REST, GraphQL, gRPC, SSE, WebSockets, WebRTC)](#-layer-7-application-layer-protocols)
- [⚖️ Scaling & Load Balancing (L4 vs L7, Algorithms)](#%EF%B8%8F-scaling--load-balancing)
- [🛡️ Resilience & Practical Interview Patterns](#%EF%B8%8F-resilience--practical-interview-patterns)
- [📊 Protocol Decision Matrix](#-protocol-decision-matrix)
- [📖 Full Detailed Guide](./docs/networking-essentials-guide.md)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)

---

## 🍰 Overview & The OSI Layered Model

Networking in distributed systems functions like a **layered cake**, where each layer acts as an abstraction hiding lower-level mechanics.

```
┌─────────────────────────────────────────────────────────┐
│ 💬 Layer 7: Application Layer (HTTP, REST, gRPC, SSE, WS)│
├─────────────────────────────────────────────────────────┤
│ 🚚 Layer 4: Transport Layer   (TCP, UDP, QUIC)          │
├─────────────────────────────────────────────────────────┤
│ 🌐 Layer 3: Network Layer     (IP - v4/v6)              │
└─────────────────────────────────────────────────────────┘
```

### 🎯 Key System Design Trade-offs
- ⏳ **Latency Overhead:** Establishing lower-layer connections introduces multiple roundtrips (e.g., TCP **3-Way Handshake**: `SYN` ➔ `SYN-ACK` ➔ `ACK`).
- 🧠 **Statefulness:** Maintaining active transport connections consumes memory and CPU. Managing state across failovers is a critical architecture choice.

---

## 📊 Protocol Decision Matrix

| Protocol | Transport | Paradigm | Primary SDI Use Case | Key Advantages & Trade-offs |
| :--- | :--- | :--- | :--- | :--- |
| 📜 **REST / HTTP** | TCP | Request-Response | Public External APIs, Standard CRUD | 🟢 Universal adoption; 🔴 JSON parsing overhead |
| 🕸️ **GraphQL** | TCP | Client-Defined Query | Complex Front-ends, Newsfeeds | 🟢 Eliminates under/over-fetching; 🔴 Query complexity |
| ⚡ **gRPC** | TCP (HTTP/2) | Binary RPC / Streaming | High-Throughput Microservices | 🟢 Up to 10x throughput; 🔴 Lacks native browser support |
| 📡 **SSE** | TCP | Unidirectional Push | Live Stock Tickers, LLM Streaming | 🟢 Lightweight HTTP streaming; 🔴 Unidirectional only |
| 🔌 **WebSockets** | TCP | Bi-directional Stream | Chat Apps, Live Dashboards, Games | 🟢 Full-duplex persistent stream; 🔴 Memory stateful at edge |
| 📹 **WebRTC** | UDP | Peer-to-Peer Stream | Video/Audio Calls, CRDT Collab | 🟢 Sub-second P2P latency; 🔴 Complex STUN/TURN setup |

---

## 🛡️ Resilience & Fault Tolerance Highlights

### 🔄 Exponential Backoff + Jitter
Never implement unthrottled retries during an outage. Combine **Timeouts + Retries + Exponential Backoff + Jitter** to break synchronized load spikes (**thundering herd problem**).

```
  Naive Retries (Retry Storm)          Exponential Backoff + Jitter
  Client 1: ───[Retry]───[Retry]      Client 1: ─────[Retry]───────[Retry]
  Client 2: ───[Retry]───[Retry]      Client 2: ──[Retry]─────────[Retry]
  Client 3: ───[Retry]───[Retry]      Client 3: ───────[Retry]──────────[Retry]
             ▲           ▲                       ▲         ▲       ▲
             └───────────┴── Synchronized Load Spikes      └─────────┴───────┴── Distributed Retries
```

---

## 📖 Full Guide

For the complete, topic-by-topic deep dive covering IP addressing, L4 vs L7 load balancing algorithms, regionalization, CDNs, and circuit breakers, check out:

👉 **[Read the Complete System Design Networking Guide](./docs/networking-essentials-guide.md)**

---

## 🚀 How to Use This Repository

1. **Clone the Repo:**
   ```bash
   git clone https://github.com/YOUR_USERNAME/networking-essentials-system-design.git
   ```
2. **Star ⭐ this repo** if you found it helpful for your interview preparation!

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the [issues page](../../issues) or submit a Pull Request.

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

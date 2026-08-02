# CN · Rapid Fire — your only CN revision file

Cover the right column. Answer out loud. 5 min for anchors, 15 for the full set.

---

## The 12 anchors

| Anchor | → |
|---|---|
| "Each layer talks only to the same layer on the other side." | CN-01 OSI vs TCP/IP |
| "TCP is registered post. UDP is a postcard." | CN-02 TCP vs UDP |
| "Can you hear me? Yes, can you hear me? Yes." | CN-03 Handshake |
| "Flow control protects the receiver. Congestion control protects the network." | CN-04 Flow vs congestion |
| "The internet's phone book — names in, IPs out." | CN-05 DNS |
| **"Resolve, connect, secure, request, render."** | CN-06 ⭐ typing google.com |
| "HTTP is stateless. Every request starts from nothing." | CN-07 HTTP · HTTPS |
| "Sessions remember on the server. Tokens remember on the client." | CN-08 REST · JWT |
| "One public address, many private machines behind it." · *"Ek ghar, ek pata — andar sab alag"* | CN-09 IP · NAT |
| "IP is the postal address. MAC is the face at the door." · *"Pata maloom hai, darwaza nahi"* | CN-10 MAC · ARP · devices |
| "Forward proxy hides the client. Reverse proxy hides the server." | CN-11 LB · proxy · CDN |
| "HTTP asks. WebSockets keep the line open." | CN-12 WebSockets · ports |

---

## 40 questions, 1-line answers

### Layers & Transport
| Q | A |
|---|---|
| Seven OSI layers? | Physical, Data Link, Network, Transport, Session, Presentation, Application. |
| Which layer owns ports / IP / MAC? | Transport (4) / Network (3) / Data Link (2). |
| OSI vs TCP/IP? | OSI is a 7-layer teaching model; TCP/IP's 4 layers are what's implemented. |
| Encapsulation? | Each layer adds a header going down, strips it going up. |
| Segment / packet / frame? | Layer 4 / Layer 3 / Layer 2 unit names. |
| TCP vs UDP? | Connection-oriented, reliable, ordered, slower vs connectionless, best-effort, fast. |
| Header sizes? | TCP 20 bytes, UDP 8. |
| When is UDP better? | Live video/gaming — a resent frame arrives too late to matter. |
| Which use UDP? | DNS, DHCP, VoIP, streaming, games. |
| Three-way handshake? | SYN(x) → SYN-ACK(y, x+1) → ACK(y+1). |
| Why three, not two? | Both sides must confirm each other's sequence numbers. |
| Why does closing take four? | Half-close — each side closes independently, so ACK and FIN can't merge. |
| Flow vs congestion control? | Protects the receiver / protects the network. |
| How does the sender know about congestion? | Packet loss. Then slow start + AIMD. |

### DNS & the Web
| Q | A |
|---|---|
| DNS lookup order? | Browser cache → OS cache → resolver → root → TLD → authoritative. |
| Why DNS over UDP? | One small request/reply; a handshake would triple the cost. Port 53. |
| A / AAAA / CNAME / MX? | IPv4 / IPv6 / alias / mail server. |
| ⭐ Typing google.com? | **Resolve → Connect → Secure → Request → Render.** |
| Where's ARP in that? | Stage 2 — finding the gateway's MAC. |
| Where's the load balancer? | Between connect and request — the IP you reached is often the LB or CDN edge. |
| Why is a second visit faster? | DNS cached, connection possibly reused, browser cache. |
| What does TLS give you? | Encryption, integrity, server identity via certificate. |
| Why asymmetric *then* symmetric? | Asymmetric is secure but slow; use it only to agree a fast symmetric key. |
| Idempotent methods? | GET, PUT, DELETE. Not POST or PATCH. |
| What does idempotent mean? | Doing it twice has the same effect as once. |
| 401 vs 403? | Don't know who you are / know you, still not allowed. |
| 301 vs 302? | Permanent vs temporary redirect. |
| 502 vs 503? | Bad gateway (upstream gave garbage) vs service unavailable (overloaded/down). |
| Why is HTTP stateless? | The server keeps no memory between requests — hence cookies and tokens. |
| REST principles? | Stateless, resources as nouns, HTTP verbs, standard status codes, JSON. |
| Session vs JWT? | Revocable but needs server storage / stateless but can't revoke before expiry. |
| Is a JWT encrypted? | **No — signed.** Anyone can read the payload. Never put secrets in it. |

### Addressing & Devices
| Q | A |
|---|---|
| IPv4 vs IPv6? | 32-bit vs 128-bit; IPv6 exists because IPv4 ran out. |
| Private IP ranges? | `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`. |
| What does NAT solve? | IPv4 exhaustion — many devices share one public IP via port rewriting. |
| Why haven't we run out of IPv4? | NAT and CIDR. |
| Subnet mask? | Splits an IP into network part and host part. |
| IP vs MAC? | IP changes with the network; MAC is burned into the hardware. |
| What does ARP do? | Finds the MAC for a known IP on the local network. |
| Hub vs switch vs router? | Repeats to all (L1) / learns MACs (L2) / connects networks by IP (L3). |
| Switch vs router, one line? | Within a network vs between networks. |
| Forward vs reverse proxy? | Hides the client / hides the servers. |
| Load balancing algorithms? | Round robin, least connections, IP hash — plus health checks. |
| What does a CDN do? | Serves static content from a nearby edge — lower latency, less origin load. |
| Polling vs long polling vs WebSocket? | Ask repeatedly / server holds the request / permanent two-way pipe. |
| Why can't HTTP push? | It's request–response; the server can't start a conversation. |
| How does a WebSocket start? | An HTTP request with `Upgrade: websocket`, then switches protocol. |
| Key ports? | 22 SSH · 53 DNS · 80 HTTP · 443 HTTPS · 3306 MySQL · 5432 Postgres · 6379 Redis. |

---

## The 6 answers to have word-perfect

1. **⭐ "What happens when you type google.com?"** — five stages, 2 minutes, then offer to go deeper.
2. **TCP vs UDP** — end on the trade-off and the video-call example.
3. **Three-way handshake** — include *why three*.
4. **HTTP vs HTTPS** — encryption, integrity, identity.
5. **Switch vs router** — within a network vs between networks.
6. **Session vs JWT** — revocation vs statelessness.

---

## The one diagram to be able to draw anywhere

```
① RESOLVE   browser → OS → resolver → root → TLD → authoritative      [DNS/UDP]
② CONNECT   ARP for the gateway MAC · routing · TCP handshake :443    [IP/TCP]
③ SECURE    TLS: certificate → verify → agree symmetric key           [TLS]
④ REQUEST   GET / · 200 OK + HTML  (via LB / CDN)                     [HTTP]
⑤ RENDER    DOM → fetch CSS/JS/images → paint
```

---

## If you have 5 minutes before an interview

Read the **12 anchors** out loud, then say the five stages of google.com once.

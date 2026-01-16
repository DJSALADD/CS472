-----
Part 1
------

| Problem (from 1974 paper OR modern problem) | Solution Proposed by Paper OR Why Not Addressed | How We See This Today |
|---------------------------------------------|------------------------------------------------|----------------------|
| Different Networks can have different incompatible addressing schemes. How can this be circumvented to make it possible to uniquely identify a host across multiple networks? | Global Internetwork Addresses - addresses that had the destination network and destination host, which allowed gateways to route packets between networks without needing comp | Whenever I am using the internet, regardless of device type, my device has an IP address that works anywhere on the internet allowing me to communicate with any server. |
| Packets can get lost while traveling across multiple networks, so how can networks ensure if that happens they know it does so they can send it again? | The host sending information needs to use different techniques including acknoledgements, retransmissions, and flow control to determine that the information was recieved and to try again if not. | Whenever I am on a webpage and then my Wifi turns off for 30 seconds and then turns back on, my browser knows to wait for the given data to be received so it does this by not displaying the incomplete corrupted data caused by the internet outage. | 
| Bad actors could send massive amounts of unwanted traffic in the form of spam which could overwhelm networks. | The paper doesn't address this at all - Cerf and Kahn created this paper when connecting networks would be between universities and other agencies so trust between the networks was assumed and not considered. They were focused on connectivity being possible at all and not any nuances like security. | In various competitive video games, hackers like to overload the server the game is hosted on in using DDoS attacks order to cause game crashes in opponents in order to get free wins. The same type of attack is used on all kinds of servers. |
| How do you efficiently deliver the same popular content like a viral tik tok to millions of people? | The paper doesn't address this at all - Cerf and Kahn where focused on basic network communication between two networks and were not concerned with large scale distribution. | The main way this problem is resolved is by having a series of servers that are all interlinked. This problem is further solved by having multiple of these large interconnected servers in various locations around the user base like the United States allowing for distributed networking that can be distributed to other servers in case of failure. |
| How to different networks establish a communication? Specifically, how does a network know which program the destination machine should recieve? | Process level addressing - using ports layered on top of host addressing to allow for different programs to have data sent to the RAM in a dedicated spot linked to the port to then be used in the program. | I am able to have multiple processes going on at once like listening to music and typing on this webpage without interference. This is able to happen because the data is being sent to different ports. |
| When I see the lock icon in my browser, what actually happened behind the scenes to make that appear? How does this relate to what Cerf-Kahn built? | The paper doesn't address this at all - Cerf and Kahn assumed that the connectivity between networks would not include any sensitive information, as their focus was on just being able to reliably send information between networks. | I know there are a lot of encryption techniques used to send data to all kinds of websites. Also I know the most important sign of a website I am connecting to having good security is HTTPS with the lock icon, otherwise it is very unsafe for me to put in personal details. |

-----
Part 2
-----

#### A. Investigation Overview

- **Problem chosen from table:** From Row 4: Packets can get lost while traveling across multiple networks, so how can networks ensure if that happens they know it does so they can send it again?
- **Specific scenario:** What modern case are you investigating? (2-3 sentences explaining your concrete scenario)
The modern case I am investigating is: Why does my Zoom call sometimes drop completely but when I download a file, it always completes eventually? What's different about how these handle reliability?
This scenario is related to how the TCP protocol created in this paper is used when downloading a file but not used by Zoom. TCP is not used by Zoom because it can not display outdated information and
simply has to drop and move on from information, while downloading a file can take longer and requires full accurary in order to avoid corruption. 

#### B. Key Questions You Asked

List 4-6 questions showing how your investigation evolved. These should show progression - later questions should build on earlier answers.

1. Why does my Zoom call sometimes drop completely but when I download a file, it always completes eventually? What's different about how these handle reliability?
2. Can you talk more about UDP? Sepcficially about what it is and how Zoom interacts with it in order to have smooth zoom calls?
3. How does this relate to VINTON G. CERF AND ROBERT E. KAHN paper: A Protocol for Packet Network Intercommunication? Specifically how did this paper's introduction of TCP allow for the creation of UDP?
4. Is it possible that IP and therefore UDP could have been developed outside of using the TCP architecture? Was Cerf and Kahn's creation of TCP fully necessary for the creation of UDP?
5. Are there any cases where a host would need/want to switch between TCP and UDP protocols, and if so how would they do so?

#### C. Connection to 1974 Paper (1-2 paragraphs)

How does the modern implementation relate to what Cerf-Kahn proposed? Consider:

- What parts of their solution are still used today?
- What changed and why?
- What did they not anticipate that had to be added later?

The modern implementation relates to what Cerf-Kahn proposed in that the way in which standard non time sensitive data transfers like downloading a file still use the TCP protocol created by Cerf-Kahn, while 
time sensitive data transfers like live Zoom calls can not use TCP due to the time sensitive nature. 

#### D. Surprise Finding (4-5 sentences)

What assumption of yours turned out wrong? What did you learn that contradicted what you thought you knew? Be specific about what surprised you and why.

I honestly assumed that there was only one networking protocol in the form of TCP that managed both the communication types being consistent loseless data and data that would get lost and not resent. Once I learned about UDP from this conversation I was further surprised that technically the creation of UDP was not necessarily necessitated by the creation of TCP from a technical perspective. It is interesting to me how the two are so interconnected by there was a true technical possiblity that both protocols could have been developed independently and simultaneously. I have always held the common view of technology being a steady stream of innovations that build on top of eachother so it was interesting to see a case where UDP did build upon the foundation of the TCP protocol, but only the IP part of it, which could have technically been created without the influence of Cerf-Kahn.

#### E. AI Conversation Documentation

Include either:

- Full transcript of your conversation (can be copy-pasted), OR
- Condensed summary hitting the key exchanges (minimum 400 words showing the progression of your investigation)

You can format the transcript as:

```
ME: [your question]
AI: [relevant parts of response]
ME: [follow-up]
AI: [relevant parts of response]
```
----------------------------------------------------------------------------------------------------
FULL TRANSCRIPT OF THE CONVERSATION:
----------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------
ME: Why does my Zoom call sometimes drop completely but when I download a file, it always completes eventually? What's different about how these handle reliability?
----------------------------------------------------------------------------------------------------
AI: Two very different philosophies of “reliability” are at work here — one for real‑time communication (Zoom) and one for bulk data transfer (file downloads). Even though both run over the internet, they use the network in fundamentally different ways.

🧠 The core difference
Zoom prioritizes timeliness over perfection.  
File downloads prioritize perfection over timeliness.

That single trade‑off explains almost everything.

🎥 Why Zoom calls can drop
Zoom is a real‑time, interactive application. It uses protocols and strategies optimized for low latency, not guaranteed delivery.

🔹 1. Zoom uses UDP for media
Zoom primarily sends audio/video over UDP, which does not guarantee delivery, ordering, or retransmission. If a packet is lost, Zoom can’t wait — it just skips it.

Lost packets → frozen video, robotic audio

Too many lost packets → call collapse

This aligns with what users report: packet loss causes severe Zoom degradation.

🔹 2. Zoom has strict timing requirements
If your network hiccups for even a second:

Zoom can’t buffer much (or the call would lag)

It can’t retransmit old frames (they’d be stale)

It may decide the connection is unusable and drop

Real‑time apps must deliver each frame right now, or not at all.

🔹 3. Zoom is sensitive to jitter and congestion
Even if your bandwidth is “fast,” unstable conditions (mobile hotspots, Wi‑Fi interference, bufferbloat) can cause:

High jitter

Bursts of packet loss

Temporary upstream starvation

These conditions are exactly what users describe when Zoom fails despite “good internet”.

📥 Why file downloads almost always finish
File downloads use TCP, a protocol designed for reliability.

🔹 1. TCP guarantees delivery
TCP ensures:

Every packet arrives

In the correct order

With retransmissions for anything lost

With congestion control to avoid overwhelming the network

Even if your connection stalls for a moment, TCP simply slows down and retries.

🔹 2. Downloads can buffer indefinitely
A file download doesn’t care if:

A packet arrives 10 ms late

Or 2 seconds late

Or 20 seconds late

As long as the connection eventually recovers, the download continues.

🔹 3. TCP adapts to bad networks
If your network becomes unstable:

TCP reduces its sending rate

Retries lost packets

Slowly ramps back up

This is why downloads “eventually complete” even on terrible Wi‑Fi.

⚖️ Side‑by‑side comparison
Feature	Zoom (Real‑Time)	File Download (Bulk Transfer)
Transport	Mostly UDP	TCP
Goal	Low latency	Perfect reliability
Packet loss	Causes glitches or drops	Retransmitted automatically
Can buffer?	Very little	As much as needed
Can wait for retransmission?	No	Yes
Sensitive to jitter?	Extremely	Barely
Behavior on bad network	Freezes, drops	Slows down but completes
🧩 The intuitive analogy
Zoom is like a live phone call.  
If you miss a word, you can’t go back — the conversation moves on.

A file download is like receiving a written letter.  
If a page is missing, the sender just mails it again until you have the full set.

🎯 Bottom line
Your Zoom call drops because real‑time communication can’t tolerate delays, packet loss, or jitter. It needs data now, not eventually.

Your file download succeeds because bulk transfer protocols are designed to retry forever until every byte arrives.

If you want, I can break down how Zoom tries to mitigate these issues (FEC, jitter buffers, adaptive bitrate), or how to diagnose which part of your network is causing the drops.

----------------------------------------------------------------------------------------------------
ME: Can you talk more about UDP? Sepcficially about what it is and how Zoom interacts with it in order to have smooth zoom calls?
----------------------------------------------------------------------------------------------------

AI: Absolutely — UDP is one of those deceptively simple protocols that ends up shaping the entire feel of real‑time apps like Zoom. Since you’re already thinking in systems‑level terms, let’s dig into what UDP is, why it behaves the way it does, and how Zoom builds a whole adaptive media engine on top of it.

🧩 What UDP actually is
UDP — User Datagram Protocol — is one of the two major transport protocols on the internet (the other being TCP). It’s intentionally minimal:

🚀 Core characteristics
Connectionless  
No handshake, no session setup. Packets just get sent.

No delivery guarantees  
Packets may be lost, duplicated, or arrive out of order.

No congestion control  
UDP itself doesn’t slow down when the network is overloaded.

No retransmissions  
If a packet disappears, UDP doesn’t try again.

Low overhead  
The header is tiny (8 bytes), so it’s fast.

This makes UDP unreliable in the formal networking sense — but perfect for real‑time media where timeliness matters more than perfection.

🎥 Why Zoom prefers UDP
Zoom’s audio and video streams are time‑sensitive. A video frame that arrives 300 ms late is useless — it’s already stale. So Zoom chooses UDP because:

It can send frames immediately

It doesn’t wait for acknowledgments

It doesn’t retransmit old data

It avoids TCP’s slow‑start and congestion backoff

It keeps latency extremely low

This matches what public documentation and network analyses show: Zoom primarily uses UDP on ports like 8801, 3478, and 3479 for media.

🛠️ How Zoom makes UDP feel reliable
UDP alone is too raw. Zoom layers a ton of intelligence on top of it to smooth out the experience.

1. Adaptive bitrate (ABR)
Zoom constantly measures:

packet loss

jitter

available bandwidth

round‑trip time

Then it dynamically adjusts:

video resolution

frame rate

compression level

audio codec bitrate

If your network degrades, Zoom drops from 1080p → 720p → 360p → audio‑only before dropping the call.

2. Forward Error Correction (FEC)
Zoom sends extra redundant packets that allow the client to reconstruct missing data without retransmission.

Think of it like:

“If you lose 1 out of every 10 packets, I’ve already given you enough parity data to rebuild it.”

This is crucial because UDP doesn’t retry.

3. Jitter buffers
Packets don’t arrive evenly. Zoom uses a small buffer (tens of milliseconds) to smooth out timing variations.

Too small → choppy
Too big → laggy

Zoom dynamically tunes this buffer based on network conditions.

4. Packet prioritization
Audio is prioritized over video because:

humans tolerate video glitches

but audio dropouts destroy comprehension

Zoom will drop video frames to preserve audio continuity.

5. Fallback to TCP when UDP is blocked
If UDP ports like 8801 or 3478 are blocked by a firewall, Zoom falls back to TCP 443 or 8801.

This is slower and less smooth, but it keeps the call alive.

🧬 Putting it all together
UDP gives Zoom:

low latency

no retransmission delays

no congestion‑control pauses

minimal overhead

Zoom adds:

redundancy

buffering

dynamic quality scaling

prioritization

fallback mechanisms

The result is a system that feels “smooth” even though the underlying transport is unreliable.

🎯 If you want, I can go deeper
I can break down:

how Zoom’s media packets are structured

how STUN/TURN/ICE help Zoom traverse NATs

how Zoom detects and reacts to packet loss

how Zoom’s codecs (H.264, Opus) behave under UDP

how Zoom chooses between UDP and TCP on startup

Just tell me what direction you want to explore.

----------------------------------------------------------------------------------------------------
ME: How does this relate to VINTON G. CERF AND ROBERT E. KAHN paper: A Protocol for Packet Network Intercommunication? Specifically how did this paper's introduction of TCP allow for the creation of UDP?
This is a fantastic question, because it gets at something subtle: UDP didn’t come first — TCP did. And TCP itself came directly out of the Cerf & Kahn 1974 paper. UDP only appears later as a deliberate “carve‑out” from TCP’s design.
----------------------------------------------------------------------------------------------------

AI: Let’s unpack how the original TCP design created the conceptual space that made UDP possible.

🌐 1. What Cerf & Kahn actually invented in 1974
Their paper A Protocol for Packet Network Intercommunication introduced the first version of TCP, but this early TCP was not the TCP we know today.

In the 1974 design:

TCP handled everything:

packet fragmentation

routing across networks

reliability

sequencing

flow control

error recovery

process‑to‑process connections

This is visible in the paper’s abstract, which describes TCP as providing “sequencing, flow control, end‑to‑end error checking, and the creation and destruction of logical process‑to‑process connections”.

In other words, TCP was originally a monolithic internetworking protocol.

There was no IP.
There was no UDP.
There was only TCP.

🔧 2. The key shift: splitting TCP into TCP + IP
As the internet grew, engineers realized that the original “everything in TCP” design was too rigid. Different applications needed different levels of reliability and timing.

So in the late 1970s, TCP was split into:

IP — an unreliable, connectionless datagram service

TCP — a reliable, connection‑oriented service built on top of IP

This split is the moment that makes UDP possible.

Why?

Because once IP existed as a bare‑bones datagram layer, you could build multiple transport protocols on top of it — not just TCP.

🧱 3. How this leads directly to UDP
After the split, engineers recognized that not all applications needed TCP’s heavy machinery (retransmissions, ordering, congestion control). Some applications needed:

low latency

no retransmissions

no connection setup

no ordering guarantees

So they created a second transport protocol:

UDP — a “minimal TCP” without reliability features
UDP is literally defined as:

“IP datagrams plus port numbers.”

It inherits the addressing model and multiplexing ideas from TCP, but strips away:

sequencing

flow control

retransmissions

connection state

This is why UDP is sometimes described as “TCP without the reliability.”

🧬 4. How the Cerf & Kahn paper enabled UDP
The 1974 paper introduced several foundational ideas that UDP depends on:

1. End‑to‑end principle
Cerf & Kahn emphasized that reliability should be handled at the endpoints, not inside the network. This principle is what allows UDP to exist — the network doesn’t guarantee anything.

2. Process‑to‑process communication
The paper introduced the idea of ports (though not yet called that). UDP inherits this model directly.

3. Uniform packet format across networks
Their design allowed packets to traverse heterogeneous networks. UDP simply uses the same packet model but with a smaller header.

4. Layered architecture
The paper’s architecture made it possible to later split TCP into layers. UDP occupies the same “transport layer” slot as TCP, but with fewer responsibilities.

🧩 5. Why UDP wasn’t in the original paper
Because the original TCP already included reliability, ordering, and flow control. There was no concept yet of a “lightweight transport protocol.”

UDP only becomes meaningful after TCP is decomposed into:

a universal datagram layer (IP)

a reliable transport layer (TCP)

Once that decomposition exists, UDP emerges naturally as:

“What if we want the datagram layer, but still need ports and multiplexing?”

🎯 Final summary
Cerf & Kahn’s 1974 paper didn’t define UDP, but it created the architecture that made UDP possible.

Their original TCP was a monolithic protocol.

It was later split into TCP + IP.

Once IP existed, engineers could build multiple transport protocols on top of it.

UDP was created as a minimalist alternative to TCP, inheriting the addressing model but not the reliability features.

Without the Cerf & Kahn paper, there is no TCP.
Without TCP, there is no TCP/IP split.
Without the split, there is no UDP.

If you want, I can map this evolution on a timeline or show how Zoom’s use of UDP fits perfectly into the end‑to‑end principle Cerf & Kahn articulated.

----------------------------------------------------------------------------------------------------
ME: Is it possible that IP and therefore UDP could have been developed outside of using the TCP architecture? Was Cerf and Kahn's creation of TCP fully necessary for the creation of UDP?
This is a sharp, historically aware question — and the honest answer is a mix of “yes in theory” and “no in practice.” The nuance is where things get interesting.
----------------------------------------------------------------------------------------------------

AI: Let’s break it down in a way that respects the actual history of networking research in the early 1970s.

🧠 Short answer
In theory: Yes, someone could have invented a connectionless datagram protocol like IP (and a lightweight transport like UDP) without first inventing TCP.

In practice: Cerf & Kahn’s TCP architecture directly created the conceptual and architectural space that made IP and UDP possible. Without their TCP, the specific IP/UDP we have today would not exist.

The key is that IP and UDP were not invented independently — they were carved out of TCP.

🧬 Why TCP had to come first (historically)
The 1974 Cerf & Kahn paper proposed a single, monolithic protocol called TCP that handled:

addressing

fragmentation

routing

reliability

sequencing

flow control

process‑to‑process communication

This “everything in one protocol” design was the first serious attempt to unify multiple incompatible packet networks.

Once researchers tried to implement it, they realized:

“This is too much responsibility for one protocol.”

That realization forced the split:

IP → the bare‑bones, unreliable datagram service

TCP → the reliable, connection‑oriented service built on top of IP

And once IP existed, it became obvious that:

“We can build more than one transport protocol on top of IP.”

That’s where UDP comes from.

UDP is literally defined as:

“IP datagrams plus port numbers.”

It inherits the addressing/multiplexing model from TCP, but drops all the reliability machinery.

🧩 Could someone have invented IP without TCP?
Yes, in principle.  
The idea of connectionless packet switching existed before TCP:

Donald Davies (UK, NPL network)

Louis Pouzin (CYCLADES network)

Pouzin’s CYCLADES in particular had a strong influence on Cerf & Kahn. CYCLADES emphasized:

host‑based reliability

datagrams

end‑to‑end responsibility

So the conceptual seeds of IP existed elsewhere.

But here’s the key:

No one had unified these ideas into a global, interoperable architecture until Cerf & Kahn.
Their TCP design was the first to:

define a universal packet format

define a universal addressing scheme

define process‑to‑process communication

define end‑to‑end reliability

define how to interconnect heterogeneous networks

Once that architecture existed, splitting TCP into layers was a natural evolution.

🧩 Could UDP have been invented without TCP?
Not the UDP we know.

UDP depends on:

IP’s datagram format

IP’s addressing

TCP’s concept of ports

TCP’s process‑to‑process communication model

The layered architecture created by the TCP/IP split

So while someone could have invented a lightweight transport protocol in another universe, UDP as a protocol is a direct descendant of TCP’s original design.

🧠 The deeper truth
Cerf & Kahn didn’t just invent a protocol — they invented a way of thinking about networks:

layering

end‑to‑end responsibility

universal interoperability

host‑based reliability

network‑agnostic packet formats

Once that worldview existed, the creation of IP and UDP was almost inevitable.

Without that worldview, it’s unlikely the internet would look anything like it does today.

🎯 Final verdict
Was TCP strictly necessary for UDP to exist?  
In a theoretical sense, no.  
Someone else could have invented a datagram protocol.

Was TCP historically necessary for UDP to exist?  
Yes, absolutely.  
UDP is a direct byproduct of the TCP → TCP/IP split.

Would UDP look the same without TCP?  
No.  
Its structure, header, semantics, and role are all inherited from TCP’s original architecture.

If you want, I can map out a timeline showing exactly when each idea emerged (CYCLADES → 1974 TCP → 1978 split → 1980 UDP), or show how Zoom’s use of UDP fits perfectly into the end‑to‑end principle that Pouzin and Cerf/Kahn championed.

----------------------------------------------------------------------------------------------------
ME: Are there any cases where a host would need/want to switch between TCP and UDP protocols, and if so how would they do so?
----------------------------------------------------------------------------------------------------

AI: Absolutely — and this is one of those questions where your instincts about protocol behavior, application design, and the Cerf/Kahn lineage all converge. There are real cases where a host switches between TCP and UDP, but the key is this:

⭐ A host never “switches” protocols mid‑stream.
Instead, the application chooses which protocol to use for each connection or flow, and it can open new flows using a different protocol when conditions change.

Think of it like choosing different lanes on a highway — you don’t transform your car while driving; you pick the lane that fits your needs.

Let’s break down the real scenarios where this happens.

🧩 1. When UDP is blocked → fallback to TCP
This is extremely common in real‑time apps:

Zoom

WebRTC

Discord

Online games

VoIP systems

If the client tries to send media over UDP and detects:

no response

firewall blocking

NAT failure

excessive packet loss

…it will open a new TCP connection and send media over that instead.

How it works technically
App attempts UDP first (e.g., STUN binding requests).

If no response, it opens a TCP connection to the same server.

Media flows over TCP until UDP becomes available again (rare).

This is not “switching” the same connection — it’s establishing a new transport flow.

🎮 2. Online games: TCP for control, UDP for gameplay
Games often use:

TCP for login, matchmaking, inventory, chat

UDP for real‑time movement, physics, hit registration

Why?

TCP ensures reliability for important state

UDP ensures low latency for gameplay

How switching happens
The game client simply opens two sockets:

text
TCP socket → reliable game state
UDP socket → real-time updates
If UDP becomes unusable (e.g., hotel Wi‑Fi), the game may fall back to TCP for movement — usually with terrible lag.

📺 3. Streaming services: TCP for control, UDP for media
Protocols like RTP/RTCP (used in WebRTC, SIP, VoIP) run over UDP.

But:

Session setup uses TCP (HTTP, SIP INVITE, WebSockets)

Media uses UDP

If UDP fails, many systems fall back to TCP or TLS.

🌐 4. QUIC vs TCP fallback
Modern browsers try to use QUIC (UDP‑based) for HTTPS.

If QUIC fails:

Browser retries the same URL over TCP/TLS

This is a protocol switch at the transport layer, but again via a new connection

This is one of the most widespread examples of transport switching today.

🧪 5. Applications that probe both and choose the best
Some systems actively test both protocols:

VPN clients

Multiplayer games

WebRTC ICE

Zoom

Microsoft Teams

They send “probe packets” over UDP and TCP, then choose whichever path:

has lower latency

is not blocked

has lower jitter

This is called happy eyeballs for transport protocols.

🧠 6. Why a host can’t switch a single connection from TCP to UDP
TCP and UDP have fundamentally incompatible semantics:

TCP is connection‑oriented

UDP is connectionless

TCP has sequence numbers, ACKs, congestion control

UDP does not

You can’t “convert” a TCP stream into UDP mid‑flight.
You can only close one socket and open another.

🛠️ How a host actually performs the switch
At the OS level, switching means:

1. Create a new socket
c
int udp_sock = socket(AF_INET, SOCK_DGRAM, IPPROTO_UDP);
or

c
int tcp_sock = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);
2. Connect or bind it
c
connect(tcp_sock, ...);
3. Start sending data over the new socket
The application decides when to stop using the old socket.

4. Optionally close the old connection
c
close(old_sock);
The OS doesn’t “switch protocols” — the application chooses which socket to use.

🎯 Summary
Yes, hosts often need or want to switch between TCP and UDP, but:

They never switch a single connection.

They open a new connection using the other protocol.

The application decides when and why to do this.

Real examples
Zoom: UDP → TCP fallback

WebRTC: ICE chooses UDP or TCP

Games: TCP for state, UDP for gameplay

QUIC: UDP → TCP fallback

VPNs: probe both and choose best

If you want, I can walk through a concrete example of Zoom’s fallback logic or show how ICE candidates are gathered and selected in WebRTC — both are beautiful demonstrations of transport switching in action.

## Part 3: Reflection

Write a brief paragraph (4-5 sentences) reflecting on your overall learning from this assignment:

The problem from the paper I found the most interesting was: Different Networks can have different incompatible addressing schemes. How can this be circumvented to make it possible to uniquely identify a host across
multiple networks? This question is most interesting to me because I always thought the concept of IP address to be quite interesting and impressive how the rapid setting of addresses is even possible and is effective.
My AI investigation taught me about the evolution that occured from the original TCP protocol to TCP/IP to then the creation of the UDP protocol based on the IP part of TCP/IP. I would not have learned about this
from just the reading as these creations occured after the paper was published. 
This assignment changed my understanding by allowing me to develop a deeper understanding of how the baseline protocol of TCP works and then I was able to see how this protocol evolved and changed, leading to the
creation of new modern standards like UDP and IPv6. 

A **Gateway Load Balancer (GWLB)** is a specialized AWS load balancer that makes it easy to deploy, scale, and manage a fleet of virtual security and network appliances, like firewalls, intrusion detection and prevention systems (IDS/IPS), and deep packet inspection (DPI) systems.

GWLB acts as a transparent network gateway that directs all traffic through your appliances before it reaches its final destination.
![[GWLB.png]]
## 🔹 How it Works

The GWLB is often described as a "bump-in-the-wire." It doesn't terminate the connection like an ALB or NLB; instead, it encapsulates incoming and outgoing traffic using the [^1]**GENEVE protocol** and sends it to your appliance fleet. The appliances inspect the traffic and, if it's approved, they send it back to the GWLB. The GWLB then decapsulates the traffic and forwards it to its final destination (either to your application servers or to the internet).

This process ensures that all traffic, regardless of its protocol (TCP, UDP, ICMP, etc.), passes through your security appliances for inspection. The GWLB also maintains **flow stickiness**, meaning it ensures that all packets for a given flow (e.g., a single TCP connection) are consistently sent to the same appliance for the duration of the flow.

[^1]: ## 🔹 What is GENEVE?
	
	- **GENEVE = Generic Network Virtualization Encapsulation**
	    
	- It’s an **open standard protocol** used to encapsulate (wrap) traffic inside another packet.
	    
	- Think of it like putting a letter inside an envelope so it can travel through different routes but still reach the right receiver.
	    
	
	---
	
	## 🔹 Why AWS GWLB Uses GENEVE?
	
	When GWLB forwards traffic to a firewall EC2 (or any appliance), it needs a way to:
	
	1. Carry the **original packet untouched** (so the firewall sees the real client IP, headers, etc.).
	    
	2. Add some **extra metadata** (like flow info, which target group, etc.).
	    
	3. Ensure the firewall can send the packet back to GWLB safely.
	    
	
	👉 GENEVE provides this tunneling mechanism.
	
	---
	
	## 🔹 Port 6081
	
	- By default, GENEVE traffic runs on **UDP port 6081**.
	    
	- This is reserved for GENEVE.
	    
	- So when your firewall EC2 instances are registered as GWLB targets, they must **listen for GENEVE traffic on port 6081**.
	    
	
	---
	
	## 🔹 Example Flow
	
	1. Client → sends packet → GWLB.
	    
	2. GWLB wraps the packet inside **GENEVE (UDP 6081)** and sends it to firewall EC2.
	    
	3. Firewall → opens packet, inspects original data.
	    
	4. Firewall → re-encaps
	5. ulates it → sends back via GENEVE.
	    
	5. GWLB → unwraps → forwards to destination EC2.
	    
	
	---
	
	⚡ **In simple words:**
	
	- GENEVE = A special tunnel format.
	    
	- Port 6081 = The “door” through which GWLB sends/receives these tunnels.
	    
	- Without this, GWLB can’t transparently pass traffic to appliances.

### Key Features

- **Transparent Integration:** The GWLB inserts your virtual appliances into the network path without requiring complex routing changes or re-architecting your network.
    
- **Centralized Security:** It allows you to centralize your security appliances in a dedicated "security VPC," which can then be used by multiple application VPCs, improving consistency and management.
    
- **High Availability and Scaling:** The GWLB handles **health checks** and automatically scales your appliance fleet up or down based on traffic, ensuring that your security layer is always available and can handle demand.
    
- **Protocol Support:** Unlike ALBs and NLBs, which are protocol-specific (HTTP/HTTPS for ALB, TCP/UDP for NLB), a GWLB can handle any IP-based traffic.
---
### How it Differs from ALB and NLB

| Feature              | **Gateway Load Balancer (GWLB)**                               | **Application Load Balancer (ALB)**      | **Network Load Balancer (NLB)**             |
| -------------------- | -------------------------------------------------------------- | ---------------------------------------- | ------------------------------------------- |
| **OSI Layer**        | Layer 3 (Network)                                              | Layer 7 (Application)                    | Layer 4 (Transport)                         |
| **Primary Use Case** | Deploying virtual appliances (firewalls, IDS/IPS)              | Distributing web traffic to applications | High-performance TCP/UDP traffic forwarding |
| **Protocol**         | Any IP protocol (encapsulated by GENEVE)                       | HTTP, HTTPS, gRPC                        | TCP, UDP, TLS                               |
| **Traffic Handling** | Transparent "bump-in-the-wire"; does not terminate connections | Proxy; terminates HTTP/HTTPS connections | Proxy; forwards TCP/UDP connections         |
| **Routing Logic**    | Flow-based (IP address, port, protocol) to appliances          | Content-based (URL path, host header)    | Connection-based (IP, port) to targets      |
 
**Implementation**
![[GWLB Design.png]]


> [!question] Why Two VPC???
> ![[Screenshot 2025-09-08 012245.png]]


Because Businessess have multiple server in multiple VPC.
In this way dadicating one vpc to Security appliance result in protection to multiple vpc server. 

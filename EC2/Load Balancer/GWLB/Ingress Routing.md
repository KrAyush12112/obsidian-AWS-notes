# 🔹 What is Ingress Routing?

**Ingress Routing** = A feature in AWS that lets you redirect **incoming traffic (ingress)** at the **VPC edge** to a different destination (like a Gateway Load Balancer endpoint) before it goes inside your VPC.
- Normally: Traffic → Internet Gateway → Direct to EC2.
- With Ingress Routing: Traffic → Internet Gateway → **GWLB Endpoint** → Firewall (inspection) → Back to VPC.

👉 Basically, it’s the steering wheel that makes sure **all traffic first passes through your security appliances** instead of going straight inside.
This capability forces inbound traffic to first pass through a specific virtual appliance, like a firewall, before it reaches its final destination within the VPC

# 🔹 Why is it Necessary in GWLB?

Without Ingress Routing, traffic would bypass the GWLB and go directly to your EC2/application.  
That means:

- Your firewall/IDS/IPS EC2s sitting behind GWLB never even see the packets.
- Security layer = useless.

So AWS gave us **Ingress Routing** to enforce that traffic is always **routed via GWLB** before entering your workload VPC.

# 🔹 How Ingress Routing Works

1. You create a **VPC Ingress Routing table** for your Internet Gateway (IGW).
2. In that table, you add a **route rule** like this:
    `0.0.0.0/0  →  GWLB Endpoint`
    (means: send all inbound internet traffic first to GWLB).
3. GWLB Endpoint sends traffic to GWLB → target group (firewall EC2).
4. After inspection, traffic is returned back to GWLB → VPC route tables → your application EC2

---
# 🔹 Example Architecture

- Internet user → hits your app at `app.example.com`.
- Instead of directly hitting EC2:
    - Internet Gateway (IGW) + Ingress Routing → forwards packets to GWLB endpoint.
    - GWLB → Firewall EC2 → inspects.
    - If allowed → packet forwarded to app EC2.
    - If denied → dropped.

---

# 🔹 Benefits of Ingress Routing with GWLB

✅ Ensures **all inbound traffic** passes through security appliances.  
✅ Centralized security: multiple VPCs can share the same GWLB for inspection.  
✅ Mandatory for compliance setups (banking, healthcare, etc.).  
✅ Protects against direct bypass of firewall.

---

⚡ **In short:**

- **Ingress Routing = mandatory traffic redirection at VPC entry point.**
    
- It’s what makes GWLB actually useful, otherwise traffic would ignore your firewall.


![[WithSecurityAppliance.png]]

![[directserverAccess.png]]
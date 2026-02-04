A **DHCP option set** in AWS is a group of network configurations that you can apply to your Amazon VPC. It dictates how instances within that VPC receive crucial networking information, such as their DNS server and domain name. Every VPC is automatically assigned a default DHCP option set, but you can create a custom one and associate it with your VPC to override the default settings.

---

### All Options That Come Under This

While there are many possible DHCP options, AWS lets you configure a specific, common set. Here are the options you can define in an AWS DHCP option set:

- **Domain name:** The domain name that an instance should use when resolving hostnames.
    
- **Domain name servers:** The IP addresses of the DNS servers for your instances. You can use **AmazonProvidedDNS** (the default AWS DNS servers) or provide your own custom DNS server addresses.
    
- **NTP servers:** The IP addresses of Network Time Protocol (NTP) servers for time synchronization. AWS provides a public NTP service, but you can also use your own servers.
    
- **NetBIOS name servers:** The IP addresses of NetBIOS over TCP/IP (WINS) name servers.
    
- **NetBIOS node type:** Specifies the method a Windows instance uses to resolve NetBIOS names to IP addresses. AWS recommends setting this to a value of **2**, which corresponds to P-node (point-to-point), as broadcast and multicast are not supported.
    
- **IPv6 Preferred Lease Time:** Specifies how often an instance with an IPv6 address should renew its DHCPv6 lease.
    

Note that once you create a DHCP option set, you **cannot modify it**. If you need to change any settings, you have to create a new DHCP option set with the desired configurations and then associate it with your VPC.
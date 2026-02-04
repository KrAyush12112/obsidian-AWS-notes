
A **VPC endpoint** is a feature that allows you to privately connect your Virtual Private Cloud (VPC) to supported Amazon Web Services (AWS) services without using the public internet.

This means traffic between your VPC and the AWS service stays entirely within the AWS network, improving both security and performance.2

---

### Types of VPC Endpoints

There are two main types of VPC endpoints:

- **Interface Endpoints:** These endpoints are powered by AWS PrivateLink. They create an [elastic network interface](obsidian://open?vault=Obsidian%20Vault&file=EC2%2F1.%20Network%20Part%2FNetwork%20Interface) (ENI) with a private IP address in your subnets. You can then use this private IP to access the AWS service. Interface endpoints are the more common type and are used for a wide range of services, including Amazon S3, DynamoDB, and many others. It's like having a private, internal gateway to an AWS service that lives within your own network.
    
- **Gateway Endpoints:** These are a specific type of endpoint that acts as a target for a route in your route table.8 They only support two services: **Amazon S3** and **DynamoDB**. They do not use an ENI or a private IP address. Instead, they provide a route to the AWS service from within your VPC.9 Think of it as a routing rule that says, "to get to S3, go through this internal gateway."
    

### Why Use a VPC Endpoint?

VPC endpoints are used primarily for two reasons:

1. **Enhanced Security:** By keeping all traffic within the AWS network, you eliminate the need for an internet gateway, a NAT gateway, or a VPN connection to access services. This reduces the attack surface and ensures your data isn't exposed to the public internet. For example, a Lambda function in your VPC can put an object in an S3 bucket without ever leaving the AWS network.
    
2. **Improved Performance and Cost Savings:** Traffic through VPC endpoints is often faster and has lower latency.10 Additionally, using VPC endpoints can help you save on data transfer costs, as traffic between a VPC and an endpoint is not charged at the same rate as traffic over the internet.11
    

### Next Topic for Further Learning

To gain a deeper understanding of VPC endpoints and how they fit into the broader AWS networking landscape, the next logical topic to explore is **AWS PrivateLink**.

**AWS PrivateLink** is the underlying technology that powers most VPC interface endpoints.12 Understanding PrivateLink will give you a clearer picture of how AWS establishes these private, one-to-one connections between your VPCs and various AWS services or even third-party services. Learning about it will help you understand:

- How PrivateLink connections are set up and managed.
    
- The difference between a service provider and a service consumer in the PrivateLink context.
    
- How to create and manage your own PrivateLink-powered services for your clients or other VPCs.
    

This knowledge will not only solidify your understanding of VPC endpoints but also open up the possibility of building your own private services within the AWS ecosystem.
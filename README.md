**Walkthrough Lab Sessions**
___
# [AZ-700: Designing and Implementing Microsoft Azure Networking Solutions](https://learn.microsoft.com/en-us/credentials/certifications/azure-network-engineer-associate/?practice-assessment-type=certification)

### Traditional Computer Network
Computer Network is a system of interconnected devices (computers, servers, routers, switches, and other hardware) that communicate using standardized protocols to share resources, exchange data, and provide services, whether locally (LAN) or over large distances (WAN, Internet).


### Cloud Computer Network
Azure Network is a cloud-based infrastructure that enables secure, scalable, and high-performance connectivity between Azure resources, on-premises networks, and the internet. It leverages virtual networks (VNets), subnets, network security groups (NSGs), load balancers, and other networking services to facilitate communication, enforce security policies, and optimize traffic flow across distributed environments. 


### Computer (On-Premises) [Cloud] Network
Is the **organizational representation** of an *(Available, Isolated) [Scalable, Available, Isolated]* **infrastructure** containing all the resources *(Computers, Servers, Routers, Switches etc.) [VNets, Subnets, DNS, VM’s etc.]* their local and global interconnections *(Cat5, Fiber, Satellite) [VNets, VNet Peerings, Hybrid etc.]* to communicate over standardized and secure protocols *[SSH, RDP, HTTPS etc.]* to share services [DB, File, App etc.] and how to access it externally [Internet, VPN] using authentic and authorized signature.


### Prerequisites
- An active Azure subscription.
- Basic understanding of networking concepts.


### Azure Products/Services:
1. Virtual Network (VNet)
2. Domain Name System (DNS)


### Cloud Industry Best Practices for Naming a Resource in Cloud

Using **consistent naming conventions** improves manageability, avoids conflicts, and aligns with **enterprise cloud governance**.

`<Company/Project>-<Product>-<Environment>-<Location>`

| **Product**        | **Naming Convention**        | **Example**                |
|--------------------|------------------------------|----------------------------|
| Resource Group     | `<Proj>-rg-<Env>-<Loc>`      | `az700-rg-lab-useast`      |
| Virtual Network 01 | `<Proj>-vnet-<Env>-<Loc>-01` | `az700-vnet-lab-useast-01` |
| Virtual Network 02 | `<Proj>-vnet-<Env>-<Loc>-02` | `az700-vnet-lab-useast-02` |
| Subnet             | `<Proj>-snet-<Env>-<Loc>`    | `az700-vnet-lab-useast`    |
| Public IP          | `<Proj>-pip-<Env>-<Loc>`     | `az700-pip-lab-useast`     |
| Firewall           | `<Proj>-fw-<Env>-<Loc>`      | `az700-fw-lab-useast`      |


### Private IP Address Prefixes

These RFC 1918 addresses are for private, nonroutable address spaces:

    10.0.0.0 - 10.255.255.255 (10/8 prefix)
    172.16.0.0 - 172.31.255.255 (172.16/12 prefix)
    192.168.0.0 - 192.168.255.255 (192.168/16 prefix)

In addition, you can't add the following address ranges:

    224.0.0.0/4 (Multicast)
    255.255.255.255/32 (Broadcast)
    127.0.0.0/8 (Loopback)
    169.254.0.0/16 (Link-local)
    168.63.129.16/32 (Internal DNS)


### Lab: IP Address Space - CIDR Block: `10.1.0.0/16`

- Provides 65,536 IPs (too many for small deployments, but flexible for subnetting).
- Easy to segment into multiple /24 subnets (each with 256 IPs).
- Avoids conflict with the commonly used 10.0.0.0/16 block in default Azure examples.
- Fits well in private RFC 1918 address space.